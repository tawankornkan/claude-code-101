# Product Requirements Document
**Product:** SquadFit
**Version:** 1.0 — MVP
**Author:** กรณ์กาญจน์
**Last Updated:** 5 มิถุนายน 2569
**Status:** Draft

---

## 1. Overview

SquadFit คือ closed accountability app สำหรับ personal trainer และ squad ลูกค้า core loop คือ **log → rank → flex**: trainee log cardio พร้อม photo proof, coach log strength data, และมี weekly leaderboard reset ทุกวันจันทร์เพื่อให้ competition ยังมีชีวิตอยู่เสมอ

**Tagline:** Log it. Rank it. Flex it.

---

## 2. Problem Statement

Personal trainer จัดการ squad ผ่าน Line กลุ่มและ spreadsheet ทำให้ admin งานกินเวลามาก trainee ขาด accountability เพราะไม่มีระบบ verify ว่าออกกำลังกายจริง และไม่มี visibility ว่าตัวเองอยู่อันดับไหนเมื่อเทียบกับ squad

---

## 3. Target User

**Primary Persona — Trainee (Member)**
สมาชิก squad อายุ 22–38 ปี ที่มี trainer อยู่แล้ว ต้องการ accountability และ friendly competition เพื่อ stay consistent Context: มือถือ ระหว่างหรือหลัง session ต้องการ log ได้ใน 15 วินาที

**Secondary Persona — Coach (Trainer)**
Personal trainer ที่มี squad 5–20 คน ต้องการ dashboard จัดการ squad แทน Line กลุ่ม ใช้ตอน admin งานระหว่าง session บนมือถือ ไม่แข่ง leaderboard

---

## 4. Goals & Success Metrics

| Goal | Metric | Target (3 เดือนหลัง launch) |
|------|--------|----------------------------|
| Trainee adoption | Active trainees logging per week | 80% ของ squad |
| Speed | Average time to submit a session log | ≤ 15 วินาที |
| Engagement | Leaderboard views per trainee per week | 3+ |
| Coach retention | Coach churn rate | < 10% ต่อเดือน |

---

## 5. MVP Scope

### 5.1 Features ที่รวมใน MVP

**Cardio Log (Trainee)**
- เปิดแอป กด Log Session
- ถ่ายหรือ upload รูปเป็น proof บังคับ
- เลือก session type (วิ่ง, ปั่น, ว่ายน้ำ ฯลฯ) และ duration
- กด Submit — เสร็จสิ้น

**Weekly Leaderboard**
- แสดง rank ของ trainee ทุกคนใน squad
- คิดคะแนนจากจำนวน session และ duration รายสัปดาห์
- Reset ทุกวันจันทร์ 00:00 Bangkok time (UTC+7)
- Trainee เห็นเฉพาะ squad ตัวเอง

**Coach Dashboard**
- เห็น session log ล่าสุดของ trainee ทุกคน
- Verify หรือ reject session พร้อม comment
- Log strength data (น้ำหนัก, reps, sets) ให้ trainee

### 5.2 Features ที่ไม่รวมใน MVP (Phase 2)

- Push Notification — weekly summary และ reminder
- Streak Counter — แสดงสถิติการออกกำลังกายต่อเนื่อง
- Squad Chat — chat ภายใน squad
- Custom Exercise Types — trainer กำหนด exercise เองได้

---

## 6. User Flow

**Trainee:**
```
เปิดแอป
    ↓
กด "Log Session"
    ↓
ถ่ายรูป proof (บังคับ)
    ↓
เลือก type + duration
    ↓
กด Submit → เห็น rank อัปเดต
```

**Coach:**
```
เปิดแอป → Coach Dashboard
    ↓
เห็น session ที่รอ verify
    ↓
กด Verify / Reject
    ↓
(Optional) Log strength data ให้ trainee
```

---

## 7. Non-Functional Requirements

- **Performance:** Submit session เสร็จใน 3 วินาทีหลังกด (รวม photo upload)
- **Speed:** Trainee ต้องสามารถ complete flow ได้ใน 15 วินาที
- **Photo:** จำกัดขนาด photo ≤ 5 MB, เก็บไว้ 90 วันแล้ว auto-delete
- **Leaderboard Reset:** ต้อง reset ตรงเวลา 00:00 Bangkok time ทุกสัปดาห์โดยไม่ fail

---

## 8. Open Questions

- [ ] คะแนน leaderboard คิดจาก session count, duration, หรือทั้งคู่?
- [ ] Coach verify ภายในกี่ชั่วโมงถึงจะนับคะแนนให้ trainee?
- [ ] ถ้า coach reject session trainee จะได้รับ notification ไหม?
- [ ] Photo proof เก็บที่ไหน และใครมีสิทธิ์เห็น?
- [ ] Pricing tier สุดท้ายสำหรับ coach subscription คือเท่าไหร่?
