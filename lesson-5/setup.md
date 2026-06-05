# Lesson 5 — Setup: เชื่อม Claude Code กับ Supabase

## สิ่งที่ต้องมีก่อน

- Supabase project ที่สร้างไว้แล้ว
- Project Reference ID (ดูได้จาก Supabase Dashboard → Settings → General)

---

## Step 1 — เพิ่ม Supabase MCP ใน Claude Code

สร้างไฟล์ `.mcp.json` ที่ root ของ project (ตำแหน่งเดียวกับ `CLAUDE.md`) แล้วใส่ content นี้:

```json
{
  "mcpServers": {
    "supabase": {
      "type": "http",
      "url": "https://mcp.supabase.com/mcp",
      "queryParams": {
        "project_ref": "YOUR_PROJECT_REF",
        "read_only": "true"
      }
    }
  }
}
```

แทน `YOUR_PROJECT_REF` ด้วย Project Reference ID เช่น `abcdefghijklmnop`

> **ทำไมต้องแยก `queryParams` ออกจาก URL?**
> Supabase ใช้ OAuth — ตอน authenticate ระบบจะตรวจสอบว่า URL ตรงกับ MCP endpoint
> ถ้าใส่ `?project_ref=...` ต่อท้าย URL ตรงนั้นเลย จะเจอ error: `Resource must be a valid MCP endpoint`
> การแยกออกมาเป็น `queryParams` ทำให้ base URL สะอาด → auth ผ่าน → Claude ส่ง query params ตอนเรียก tool

> `read_only: true` ทำให้ Claude query ได้อย่างเดียว — ไม่สามารถแก้ไขหรือลบข้อมูลได้

---

## Step 2 — Authenticate

1. Reload หน้าต่าง VSCode (`Cmd+Shift+P` → "Reload Window")
2. พิมพ์ `/mcp` ใน Claude Code
3. กด **Auth** ที่ชื่อ Supabase — browser จะเปิดให้ login กับ Supabase account

---

## Step 3 — ทดสอบว่า connect ได้แล้ว

ลอง prompt นี้กับ Claude Code:

```
จาก database SquadFit มี user กี่คน แบ่งตาม role
```

ถ้า Claude ตอบกลับมาพร้อมข้อมูลจริงจาก Supabase แสดงว่า setup สำเร็จ

---

## Schema ที่ใช้ใน Lesson นี้

ดูรายละเอียด table และ column ได้ที่ [db.md](db.md)

Table หลักที่ใช้บ่อย:

| Table | ใช้สำหรับ |
|-------|----------|
| `profiles` | ข้อมูล user ทุกคน + role (coach / member) |
| `cardio_entries` | session log ของ member |
| `squad_memberships` | ใครอยู่ squad ไหน |
| `strength_entries` | strength data ที่ coach log ให้ |

---

## Prompt ตัวอย่างที่ใช้ใน Lesson

```
จาก database มี user กี่คนที่สมัครในเดือนที่แล้ว แบ่งตาม role
```

```
member คนไหน log cardio มากที่สุดใน 7 วันล่าสุด
```

```
squad ไหนมี member active มากที่สุด
```
