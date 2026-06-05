# Product Requirements Document
**Product:** RedFlagFinder
**Version:** 1.0 — MVP
**Author:** กรณ์กาญจน์
**Last Updated:** 5 มิถุนายน 2569
**Status:** Draft

---

## 1. Overview

RedFlagFinder คือ dating app ที่ใช้ AI วิเคราะห์ red flag ในโปรไฟล์และบทสนทนา เพื่อช่วยให้ผู้ใช้ตัดสินใจได้ดีขึ้นก่อนจะ invest เวลาและ emotion กับคนที่ไม่ใช่

**Tagline:** Find love. Spot the warning signs first.

---

## 2. Problem Statement

ผู้ใช้ dating app รู้จัก red flag แต่มักตกหลุมอยู่ดีเพราะ emotion ชนะ logic ปัจจุบันยังไม่มีแอปไหนช่วย "remind" ผู้ใช้อย่างเป็นระบบ หรืออธิบายได้ว่าพฤติกรรมนั้นอันตรายอย่างไร

---

## 3. Target User

**Primary Persona:** ผู้หญิงอายุ 22–32 ปี ที่เคยผ่านความสัมพันธ์ที่ toxic มาก่อน และกำลังกลับมา date ใหม่ด้วยความระวัง

**Secondary Persona:** คนที่เพิ่งเริ่มใช้ dating app และอยากเรียนรู้ว่าควรระวังอะไร

---

## 4. Goals & Success Metrics

| Goal | Metric | Target (3 เดือนหลัง launch) |
|------|--------|----------------------------|
| User acquisition | DAU | 5,000 |
| Engagement | Red flag scans per user per week | 3+ |
| Monetization | Premium conversion rate | 8% |
| Retention | D30 retention | 25% |

---

## 5. MVP Scope

### 5.1 Features ที่รวมใน MVP

**User Profile**
- สมัครด้วย email หรือ phone number
- กรอกข้อมูลส่วนตัว: ชื่อ, อายุ, รูป, bio, และ prompt คำถาม 3 ข้อ
- ระบุ preference: เพศ, ช่วงอายุ, และระยะทาง

**Swipe & Match**
- Swipe left / right แบบ standard
- เมื่อ match กันทั้งคู่ ถึงจะ chat ได้
- แสดง Red Flag Score บนการ์ดก่อน swipe

**Red Flag Score**
- AI วิเคราะห์ bio และ prompt answers ของแต่ละโปรไฟล์
- แสดงคะแนน 1–10 พร้อม breakdown ว่ามาจากอะไร
- อธิบายเป็นภาษาคนว่าทำไมถึงเป็น red flag
- Free tier: ดูได้ 5 scans ต่อวัน / Premium: ไม่จำกัด

### 5.2 Features ที่ไม่รวมใน MVP (Phase 2)

- Chat Analyzer — วิเคราะห์ red flag ในบทสนทนา
- Community Feed — แชร์เรื่อง red flag แบบ anonymous
- Custom Red Flag Settings — ให้ user กำหนด dealbreaker เอง

---

## 6. User Flow

```
สมัคร / Login
    ↓
กรอกโปรไฟล์
    ↓
หน้า Swipe — เห็น Red Flag Score บนการ์ด
    ↓
กด "ดูรายละเอียด" → เห็น breakdown
    ↓
Swipe Right → ถ้า match → เปิด Chat
```

---

## 7. Non-Functional Requirements

- **Performance:** โหลดหน้า swipe ไม่เกิน 2 วินาที
- **Privacy:** ไม่เก็บ chat logs, แจ้งผู้ใช้ชัดเจนว่า AI วิเคราะห์อะไรบ้าง
- **AI Consistency:** Red Flag Score ของโปรไฟล์เดิมต้องได้ผลเดิมทุกครั้ง (cache ผล)

---

## 8. Open Questions

- [ ] Red Flag Score คำนวณจาก criteria อะไรบ้าง? ใครเป็นคนกำหนด?
- [ ] ถ้า user อยากโต้แย้ง score ของตัวเอง มี mechanism ไหม?
- [ ] App Store policy สำหรับ dating app มีข้อจำกัดอะไรบ้าง?
- [ ] จะ handle กรณี AI bias ได้อย่างไร?
- [ ] Pricing tier สุดท้ายคือเท่าไหร่?
