# SquadFit — คำแนะนำโปรเจกต์

## ภาพรวม Product

**SquadFit** คือ closed accountability app สำหรับ personal trainer และลูกเทรน

**Tagline:** *"Log it. Rank it. Flex it."*

**กลุ่มเป้าหมาย:** Personal trainer ที่มี squad อยู่แล้ว และ trainee ที่ต้องการ accountability กับ friendly competition

---

## User Roles

| Role | รายละเอียด |
|------|------------|
| **Coach (Trainer)** | เจ้าของ squad คนเดียว log strength data แทน trainee, verify session, และดู squad activity ทำงาน quick admin ระหว่าง session ส่วนใหญ่ใช้บนมือถือ ไม่แข่ง leaderboard |
| **Trainee (Member)** | สมาชิก squad log cardio พร้อม photo proof บังคับ และ track rank รายสัปดาห์ ผู้ใช้หลัก — ต้อง log ได้ภายใน 15 วินาที squad กรุงเทพ ส่วนใหญ่เป็นคนไทย ระดับฟิตเนสหลากหลาย |

---

## Core Features

| Feature | รายละเอียด |
|---------|------------|
| **Cardio Log** | Trainee ส่ง session พร้อม photo proof บังคับ (selfie ที่ location หรือ equipment) |
| **Strength Log** | Coach log strength data (น้ำหนัก, reps, sets) ให้ trainee หลัง session |
| **Weekly Leaderboard** | จัดอันดับ trainee ทุกคนตาม session point; reset ทุกเดือน |

---

## Business Model

- **Per-squad subscription** — coach จ่ายรายเดือน; trainee ใช้ฟรี
- **ไม่มี freemium, ไม่มี marketplace** — เป็น closed squad tool เท่านั้น

---

## Tech Stack

- **Frontend:** Next.js + Tailwind CSS
- **Backend:** Supabase (Database, Auth, Storage)

---
