# SquadFit — Database Reference

> Read-only guide for querying via Claude Code + Supabase MCP.
> All tables live in the `public` schema on Supabase (Postgres).

---

## Tables

### `profiles`
ข้อมูล user ทุกคน (ต่อจาก `auth.users`)

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | ตรงกับ `auth.users.id` |
| `role` | text | `'coach'` หรือ `'member'` |
| `display_name` | text | ชื่อที่แสดงในแอป (nullable — null = ยังไม่ onboard) |
| `is_active` | boolean | false = deactivated account |
| `line_user_id` | text | LINE sub claim (unique) |
| `line_picture_url` | text | รูป avatar จาก LINE |
| `line_synced_at` | timestamptz | ครั้งล่าสุดที่ sync profile จาก LINE |
| `created_at` | timestamptz | |

---

### `squads`
หนึ่ง coach มีได้หนึ่ง squad (active)

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | |
| `name` | text | ชื่อ squad |
| `coach_id` | uuid FK → profiles | เจ้าของ squad |
| `invite_code` | text | 4-char hex code สำหรับ join (case-insensitive) |
| `is_active` | boolean | false = squad archived (coach deactivated) |
| `created_at` | timestamptz | |

---

### `squad_memberships`
ติดตามว่า member คนไหนอยู่ใน squad ไหน (soft-delete pattern — ไม่ลบแถว)

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | |
| `squad_id` | uuid FK → squads | |
| `member_id` | uuid FK → profiles | |
| `is_active` | boolean | false = ออกจาก squad แล้ว |
| `joined_at` | timestamptz | ครั้งล่าสุดที่ join |
| `left_at` | timestamptz | null ถ้ายังอยู่ใน squad |

---

### `cardio_entries`
บันทึก cardio แต่ละครั้ง — member เป็นคน log เอง, ไม่สามารถแก้ไขหรือลบได้

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | |
| `member_id` | uuid FK → profiles | คนที่ log |
| `squad_id` | uuid FK → squads | |
| `duration_minutes` | integer | ระยะเวลา (> 0) |
| `proof_photo_url` | text | path ของภาพใน storage bucket `workout-proofs` |
| `logged_at` | timestamptz | เวลาที่ submit |

---

### `exercises`
รายการท่าออกกำลังกาย — coach เป็นคน config ต่อ squad

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | |
| `squad_id` | uuid FK → squads | |
| `name` | text | ชื่อท่า เช่น "Bench Press" |
| `unit` | text | `'kg'` หรือ `'time'` |
| `icon` | text | lucide icon name เช่น `'dumbbell'` |
| `created_at` | timestamptz | |

---

### `strength_entries`
บันทึก strength — coach เป็นคน log ให้ member (Verified by Coach)
ใช้ personal best (น้ำหนักสูงสุดตลอดกาล) สำหรับ leaderboard

| Column | Type | Description |
|--------|------|-------------|
| `id` | uuid PK | |
| `member_id` | uuid FK → profiles | member ที่ทำ |
| `coach_id` | uuid FK → profiles | coach ที่ verify |
| `exercise_id` | uuid FK → exercises | |
| `weight_kg` | numeric(6,2) | น้ำหนัก (> 0) |
| `logged_at` | timestamptz | |

---

## Relationships

```
auth.users
    └── profiles (1:1)
            ├── squads (1:1 per coach, via coach_id)
            ├── squad_memberships (1:many per member)
            ├── cardio_entries (1:many)
            └── strength_entries (1:many as member or coach)

squads
    ├── squad_memberships (1:many)
    ├── cardio_entries (1:many)
    └── exercises (1:many)
            └── strength_entries (1:many)
```

---

## Query Examples

```
-- Members ที่ active อยู่ใน squad
SELECT p.display_name, sm.joined_at
FROM squad_memberships sm
JOIN profiles p ON p.id = sm.member_id
WHERE sm.is_active = true;

-- Cardio รวมของแต่ละ member ใน 7 วันล่าสุด
SELECT p.display_name,
       COUNT(*) AS sessions,
       SUM(ce.duration_minutes) AS total_minutes
FROM cardio_entries ce
JOIN profiles p ON p.id = ce.member_id
WHERE ce.logged_at >= now() - interval '7 days'
GROUP BY p.display_name
ORDER BY total_minutes DESC;

-- Personal best ต่อท่าต่อ member
SELECT p.display_name, e.name AS exercise, MAX(se.weight_kg) AS personal_best
FROM strength_entries se
JOIN profiles p ON p.id = se.member_id
JOIN exercises e ON e.id = se.exercise_id
GROUP BY p.display_name, e.name
ORDER BY p.display_name, e.name;
```

---

## Notes

- **Soft-delete everywhere** — ไม่มีการลบแถวจริง ใช้ `is_active = false` แทน
- **Cardio entries are immutable** — ไม่มี UPDATE/DELETE policy
- **Strength = Verified by Coach** — ต้อง coach เป็นคน insert เท่านั้น
- **RLS is on** — query ผ่าน MCP จะเห็นข้อมูลตาม permission ของ Supabase token ที่ใช้
- **Storage bucket** `workout-proofs` — เก็บรูปภาพ proof ของ cardio, ไม่ได้อยู่ใน DB โดยตรง
