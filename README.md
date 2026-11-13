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

## แก้ไฟล์กฎแล้วสร้าง data.json ใหม่ (ตั้งแต่ v1.22)
ไฟล์กลางที่ `build_data.py` อ่านจากรอบทำงานก่อน ๆ หายไปแล้ว รอบนี้จึงแทนเฉพาะหมวดชุดเริ่มต้นกับคลังไอเทม แล้วคงหมวดอื่นของ `data.json` ไว้
```
KIRANA_OUT=<โฟลเดอร์ชั่วคราว>/ KIRANA_SETS_SRC="<Starter Set - ชุดไอเทมเริ่มต้น.md>" python3 tools/parse_sets.py
KIRANA_OUT=<โฟลเดอร์ชั่วคราว>/ KIRANA_ITEMS_SRC="<Item All.md>" python3 tools/parse_items.py
KIRANA_OUT=<โฟลเดอร์ชั่วคราว>/ python3 tools/splice_data.py
python3 tools/build.py
```
ถ้า Item All มีบรรทัดเพิ่มหรือหายก่อนหัวข้อหมวดใด ให้แก้ช่วงบรรทัด `TOP_FIX` ใน `parse_items.py` ให้ตรงกับหัวข้อหมวดใหม่ก่อน

## v1.22.1 (13 พ.ย. 2026)
- ตัดหนังยางเหวี่ยงหิน (Sling Shot) ออกจากคลังไอเทม The Wanderer ถือสลิงหนัง (Leather Sling) แทน และได้หมึกกับปากกาขนนกและกระดาษ 1 แผ่น มูลค่าชุดอยู่ที่ 50 เกรฟ
- ตัวละครเดิมที่ถือหนังยางเหวี่ยงหินได้สลิงหนังแทนเมื่อเปิดชีท ทั้งชื่อ ข้อความเอฟเฟกต์ และน้ำหนัก 0.2 กก. (ตาราง `tools/renames_v1221.json`) ของที่ผู้เล่นแก้ข้อความหรือน้ำหนักเองคงค่าของผู้เล่นไว้

## v1.22 (13 พ.ย. 2026)
- ชุดเริ่มต้นเพิ่ม 14 ชุด รวม 31 ชุด · แถวที่ขึ้นต้นด้วย "และ" ในตารางชุดคือของที่มาพร้อมทางเลือกในแถวบน · คาตานะเป็นอาวุธระดับ 2 · คลังไอเทมมีอาวุธระดับ 1 และ 2 เพิ่ม 16 ชิ้น
- ระยะเคลื่อนที่ต่อหนึ่ง Maneuver คิดจากความเร็วของตัวละคร Dash เท่าความเร็ว Dash ของวงศา Run เท่าความเร็ววิ่งบวก AGI Mod · เลือกหมากแล้วจุดกลางช่องบอกช่องที่ไปถึง
- ผู้เล่นที่ไม่ใช่ผู้พัฒนาอัปไฟล์ภาพได้ไม่เกิน 2 MB ต่อภาพ
- ของหลายชิ้นในชุดเริ่มต้นเก็บน้ำหนักต่อชิ้น เสบียง 5 หน่วยหนักรวม 2 กก.


## v0.7 (8 พ.ย. 2026)
- ล็อกอิน/ออกจากระบบ (Google) ที่แถบบน · รายชื่อผู้เล่นที่ออนไลน์อยู่ (`presence/<uid>`)
- ชีทเป็นของบัญชีเจ้าของเท่านั้น (Rules ใหม่ใน `firestore.rules`) · GM และเพื่อนร่วมโต๊ะเห็นชีทผ่านสำเนา `rooms/<id>/chars/<cid>` เฉพาะตัวละครที่ถูกหยิบลงบอร์ด · ผู้พัฒนาเห็นทั้งหมด
- แผนที่ต่อสู้ 20×20 แทนโซน: สุ่มตามสถานที่ 24 แบบ (`src/map.js`) หมากมีรูปตัวละคร เลือกหมากแล้วคลิกช่องเพื่อเดิน วงสีบอกเขตปะทะ/ใกล้เคียง GM มีพู่กันแก้แผนที่
- Insight Point ใช้ตามบทที่ 13 (ประตู ส่วนลดครู/ตำรา บุคคลในตำนาน) แทนการ์ดสุ่ม

## เครดิต
- ไอคอนหมากใน `ttrpg-icons.js` (4,085 แบบ โหลดเมื่อเปิดหน้าต่างเลือกไอคอนของคลัง NPC / Asset): [game-icons.net](https://game-icons.net) โดย Lorc, Delapouite และผู้ร่วมสร้าง (aussiesim, felbrigg, guard13007, john-colburn, john-redman, lorc, lord-berandas, lucasms, pierre-leducq, priorblue, rihlsul, sbed, skoll, zajkonur, zeromancer) สัญญาอนุญาต [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) เส้นแปลงจากภาพ PNG เป็นเวกเตอร์ และผู้ใช้ปรับสีได้ในเว็บ
