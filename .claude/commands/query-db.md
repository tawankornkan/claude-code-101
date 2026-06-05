---
name: query-db
description: Query the SquadFit Supabase database using natural language — no SQL required.
---

## Purpose

แปลงคำถามภาษาคน → SQL → ดึงข้อมูลจาก SquadFit Supabase และตอบกลับเป็นภาษาคน

## Usage

- `/query-db มี user กี่คน`
- `/query-db trainee ที่ log cardio เยอะที่สุดคือใคร`
- `/query-db squad ไหนมีสมาชิกเยอะที่สุด`

---

## Workflow

### Step 0: ตรวจสอบ Supabase MCP

ก่อนทำอะไรทั้งหมด ให้เรียก `list_projects` เพื่อตรวจสอบว่า Supabase MCP เชื่อมต่อได้

- **ถ้าสำเร็จ** → ไปต่อ Step 1
- **ถ้า error หรือ tool ไม่พร้อมใช้** → หยุดและแจ้ง user:

  > "Supabase MCP ยังไม่ได้ setup ครับ กรุณาตรวจสอบว่า:
  > 1. ไฟล์ `.mcp.json` มี supabase config อยู่หรือเปล่า
  > 2. ลองรัน `/mcp` เพื่อดูสถานะ MCP servers
  > 3. ถ้ายังไม่มี ให้เพิ่ม Supabase MCP ใน settings ก่อน"

---

### Step 1: เข้าใจคำถาม

อ่านคำถามของ user และระบุว่าต้องการข้อมูลอะไร เช่น:
- นับจำนวน (COUNT)
- หาอันดับ (ORDER BY, RANK)
- หาข้อมูลเฉพาะ (WHERE, FILTER)
- สรุปรวม (SUM, AVG, GROUP BY)

### Step 2: อ่าน Schema จาก db.md

อ่านไฟล์ `docs/db.md` ก่อนเขียน SQL เสมอ — ไฟล์นี้มีรายละเอียดตารางและ columns ครบถ้วนแล้ว ไม่ต้องเรียก `list_tables` หรือ query `information_schema`

```
project_id: yimtgteinfyepappriee
```

### Step 3: แปลงเป็น SQL

เขียน SQL ที่ตรงกับคำถาม โดย:
- ใช้ชื่อตารางและ columns จริงจาก schema
- เลือก columns เฉพาะที่จำเป็น อย่า SELECT *
- ใส่ LIMIT 50 เสมอ ถ้าไม่ได้ถามแบบ aggregate

### Step 4: Execute SQL

ใช้ `execute_sql` กับ project_id `yimtgteinfyepappriee`

### Step 5: ตอบกลับเป็นภาษาคน

แปลงผลลัพธ์จาก SQL กลับเป็นคำตอบภาษาคน (ไทยหรืออังกฤษ ตาม user ถาม) ที่:
- ตอบตรงคำถาม ไม่ต้องแสดง raw SQL หรือ JSON
- ถ้าได้ตาราง ให้แสดงเป็น markdown table
- ถ้าได้ตัวเลข ให้พูดตรงๆ เช่น "มีทั้งหมด 4 คน"
- ถ้าไม่มีข้อมูล ให้บอกว่า "ยังไม่มีข้อมูล" ไม่ใช่แสดง empty array

---

## Error Handling

- ถ้า table หรือ column ไม่ตรง → อ่าน `docs/db.md` อีกครั้ง อย่าเดา
- ถ้า query ช้าหรือ timeout → ให้ใส่ LIMIT และ index hint

---

## Notes

- **Project:** squad-fit-prod
- **Project ID:** `yimtgteinfyepappriee`
- **Auth users:** อยู่ใน `auth.users` (Supabase built-in)
- **Business data:** อยู่ใน schema `public`
- ห้าม query ข้อมูล sensitive เช่น password, token
