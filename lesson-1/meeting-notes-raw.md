# บันทึกการประชุม — SquadFit
วันที่: 5 มิถุนายน 2569

---

## ประชุมครั้งที่ 1 — Product Kickoff
เวลา: 10:00 น.
ผู้เข้าร่วม: กรณ์กาญจน์ (Product Lead), บีม (Marketing), พลอย (UX), ตุ้ม (Engineering Lead)

คุยภาพรวม product vision กรณ์กาญจน์พรีเซนต์ concept SquadFit ว่าเป็น accountability app สำหรับ personal trainer กับ squad ลูกค้า core loop คือ log → rank → flex: trainee ส่ง photo proof ว่าออกกำลังกายจริง coach log strength data แล้วมี leaderboard รายสัปดาห์ reset ทุกวันจันทร์ตี 0 ตามเวลากรุงเทพ

บีมถามว่า target market ชัดแค่ไหน กรณ์กาญจน์บอกเริ่มจาก personal trainer ที่มี squad อยู่แล้ว ไม่ได้เป็น marketplace หา trainer ใหม่ เป็น closed tool เฉพาะ squad เดียวกัน บีมบอกต้องทำ competitive analysis ก่อนเพราะมี fitness app เยอะแต่อาจยังไม่มีใครทำ closed squad model แบบนี้โดยตรง

พลอยถามเรื่อง UX ว่า use case หลักของ trainee คืออะไร กรณ์กาญจน์บอกต้อง log ได้ใน 15–30 วินาที เปิดแอป ถ่ายรูป กด submit แล้วปิดได้เลย พลอยบอกถ้า constraint ชัดขนาดนี้ต้อง design flow ให้ minimal มากๆ ต้องทำ usability test ก่อน

คุยเรื่อง success metric ยังไม่ได้ข้อสรุปชัดเจน มีคนเสนอทั้ง DAU, session log rate, และ leaderboard engagement แต่ยังไม่ได้ตั้ง target

ตุ้มถามว่า photo storage จะ handle ยังไง ยังไม่ได้ตอบ บอกจะคุยละเอียดช่วงบ่าย

---

## ประชุมครั้งที่ 2 — Go-to-Market & Business Model
เวลา: 13:30 น.
ผู้เข้าร่วม: กรณ์กาญจน์, บีม, พลอย

บีมพรีเซนต์ draft GTM strategy เบื้องต้น เสนอให้เริ่มจาก pilot กับ trainer 5–10 คนที่รู้จักก่อน แล้วค่อย expand กรณ์กาญจน์โอเคกับ approach นี้ พลอยบอกการทำ pilot เล็กๆ จะช่วยให้เก็บ feedback ได้ดีกว่า open launch

คุยเรื่อง business model กัน 3 แบบ
- แบบแรก per-squad subscription — trainer จ่ายรายเดือนต่อ squad ไม่จำกัด trainee
- แบบสอง per-trainee fee — trainer จ่ายตาม head count ของ trainee ในรายเดือน
- แบบสาม trainee จ่ายเอง — trainer ไม่ต้องจ่าย แต่ trainee unlock feature เพิ่ม

บีมเสนอแบบแรกเพราะ simple และ trainer control ได้ predictable cost พลอยเป็นห่วงว่า trainer จะยอมจ่ายไหมถ้าตัวเองไม่ได้ benefit โดยตรง กรณ์กาญจน์บอกต้องทำ pricing research กับ trainer ก่อน ยังไม่ได้ตัดสินใจ

คุยเรื่อง leaderboard mechanics บีมบอกต้องระวัง leaderboard เป็น stressful สำหรับบาง trainee พลอยเห็นด้วย กรณ์กาญจน์บอกจะ design ให้ reset ทุกสัปดาห์เพื่อให้ทุกคนมีโอกาสใหม่ ไม่ให้คนที่เริ่มช้า feel bad ถาวร

ยังไม่ได้คุยเรื่อง onboarding flow สำหรับ trainer บีมบอกอันนี้สำคัญมากเพราะถ้า trainer setup squad ยากจะ churn ทันที

---

## ประชุมครั้งที่ 3 — Roadmap & Resource Planning
เวลา: 16:00 น.
ผู้เข้าร่วม: กรณ์กาญจน์, ตุ้ม

ตุ้มถามตรงๆว่า photo proof storage cost จะเยอะไหม กรณ์กาญจน์บอกจะ limit photo size และอาจ auto-delete หลัง 90 วัน ตุ้มบอกต้องวาง data retention policy ชัดก่อน build เพราะ storage ไม่ใช่ถูก

คุยเรื่อง MVP scope ตุ้มเสนอให้ตัดเหลือแค่ 3 feature สำหรับ MVP คือ trainee cardio log พร้อม photo proof, leaderboard รายสัปดาห์, และ coach dashboard ส่วน strength log และ session verification ทำใน phase 2 กรณ์กาญจน์เห็นด้วยบางส่วน แต่กังวลว่าถ้าไม่มี verification ตั้งแต่แรก data จะไม่สะอาดและ squad จะไม่ trust ระบบ ยังหาข้อสรุปไม่ได้

ตุ้ม estimate คร่าวๆ ว่า MVP ใช้เวลาประมาณ 6–8 สัปดาห์ถ้าทีม engineer 2 คน กรณ์กาญจน์บอกอยากได้เร็วกว่านั้น ตุ้มบอกถ้าอยากเร็วต้องตัด scope หรือเพิ่มคน

ยังไม่ได้คุยเรื่อง timezone handling สำหรับ leaderboard reset ตอน 00:00 Bangkok time และ push notification system สำหรับ weekly recap ต้องนัดประชุมเพิ่ม
