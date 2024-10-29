# Git-Command-Note

ใน Gitflow Workflow ส่วนของ branch release จะมีขั้นตอนที่สำคัญดังนี้:

1. สร้าง Release Branch
เมื่อฟีเจอร์ทั้งหมดที่ต้องการสำหรับ release หนึ่งๆ อยู่ใน branch develop และถูกทดสอบจนมั่นใจแล้ว ให้สร้าง branch ใหม่จาก develop เช่น release/1.0
คำสั่งสำหรับสร้าง branch:
bash
Copy code
git checkout -b release/1.0 develop
2. ทดสอบและแก้ไขข้อบกพร่องใน Release Branch
ทดสอบโค้ดใน branch release และหากพบข้อผิดพลาดเล็กน้อย สามารถแก้ไขได้ใน branch นี้ (ควรหลีกเลี่ยงการเพิ่มฟีเจอร์ใหม่ใน release branch)
คำสั่งแก้ไข commit และ push:
bash
Copy code
git add .
git commit -m "Fix bugs for release 1.0"
git push origin release/1.0
3. เตรียมการปล่อยเวอร์ชัน
เมื่อทุกอย่างเรียบร้อยแล้ว merge branch release ไปยัง main เพื่อเตรียมปล่อย release
คำสั่ง merge:
bash
Copy code
git checkout main
git merge --no-ff release/1.0
4. สร้าง Tag สำหรับ Release Version
สร้าง tag ให้กับ commit ล่าสุดใน main ที่เพิ่ง merge release branch เข้ามา เพื่อระบุ version เช่น v1.0
คำสั่งสร้าง tag:
bash
Copy code
git tag -a v1.0 -m "Release version 1.0"
git push origin v1.0
5. Merge Release กลับไปยัง Develop
เพื่อให้แน่ใจว่า develop มีทุกการแก้ไขจาก release (เช่น bug fixes ที่อาจเกิดขึ้น) ให้ merge release กลับไปยัง develop
คำสั่ง merge:
bash
Copy code
git checkout develop
git merge --no-ff release/1.0
6. ลบ Release Branch (ถ้าไม่ต้องการใช้งานต่อ)
เมื่อเสร็จสิ้นขั้นตอนทั้งหมด สามารถลบ release branch ได้
คำสั่งลบ branch:
bash
Copy code
git branch -d release/1.0
git push origin --delete release/1.0