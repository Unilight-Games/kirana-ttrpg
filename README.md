# Kirana TTRPG Online

เว็บเล่น Kirana TTRPG: วิซาร์ดสร้างตัวละคร 8 ขั้น ชีทที่กดทอยได้ และโต๊ะเล่นแบบ Theater of the Mind
ข้อมูลกฎดึงจาก `Kirana Core System TTRPG (V.2)`, `Kins of Kirana V.2`, `Skill & Sorceries`, `Talent & Knowledge Proficiency`, `Starter Set`

## ใช้งาน
เปิด `index.html` ได้ทันที (ไฟล์เดียว ไม่ต้องติดตั้งอะไร) หรือเปิดผ่าน GitHub Pages ของ repo นี้

ตัวละคร ห้อง และแชตซิงก์ผ่าน Firebase เมื่อเปิดจาก GitHub Pages ถ้าเปิดไฟล์แบบออฟไลน์จะบันทึกในเบราว์เซอร์เครื่องนั้นแทน
ส่วนโต๊ะเล่นร่วมกันแบบเรียลไทม์ใช้ Firebase (Firestore + ล็อกอินนิรนาม) ค่าเชื่อมต่ออยู่ใน `firebase-config.js` และกติกาความปลอดภัยอยู่ใน `firestore.rules`

## เปิด GitHub Pages
Settings → Pages → Source: Deploy from a branch → Branch `main` / `(root)` → Save
รอ 1-2 นาที แล้วเปิด `https://<ชื่อผู้ใช้>.github.io/<ชื่อ repo>/`

## โครงสร้าง
- `index.html` หน้าเว็บที่ build แล้ว (ฝังข้อมูลกฎไว้ในไฟล์)
- `src/` ซอร์ส: `shell.html` (โครง+CSS), `core.js` (เต๋า คำนวณ เก็บข้อมูล), `wizard.js`, `sheet.js`, `table.js`, `main.js`
- `tools/` สคริปต์แปลงไฟล์กฎ .md เป็น `data.json` และ `build.py` รวมเป็น `index.html`
- `test/run.js` ทดสอบเดินวิซาร์ดด้วย Playwright

## build ใหม่หลังแก้ซอร์ส
```
python3 tools/build.py
```


## v0.7 (8 พ.ย. 2026)
- ล็อกอิน/ออกจากระบบ (Google) ที่แถบบน · รายชื่อผู้เล่นที่ออนไลน์อยู่ (`presence/<uid>`)
- ชีทเป็นของบัญชีเจ้าของเท่านั้น (Rules ใหม่ใน `firestore.rules`) · GM และเพื่อนร่วมโต๊ะเห็นชีทผ่านสำเนา `rooms/<id>/chars/<cid>` เฉพาะตัวละครที่ถูกหยิบลงบอร์ด · ผู้พัฒนาเห็นทั้งหมด
- แผนที่ต่อสู้ 20×20 แทนโซน: สุ่มตามสถานที่ 24 แบบ (`src/map.js`) หมากมีรูปตัวละคร เลือกหมากแล้วคลิกช่องเพื่อเดิน วงสีบอกเขตปะทะ/ใกล้เคียง GM มีพู่กันแก้แผนที่
- Insight Point ใช้ตามบทที่ 13 (ประตู ส่วนลดครู/ตำรา บุคคลในตำนาน) แทนการ์ดสุ่ม
