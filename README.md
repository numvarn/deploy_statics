# การติดตั้ง Django บน Vercel ผ่าน Github

โดย ผู้ช่วยศาสตราจารย์พิศาล สุขขี

Youtube : https://youtu.be/LGdMVUoMG24

เนื้อหา : กระบวนการติดตั้ง Django บน Heroku ผ่าน Github โดยมีขั้นตอนในการเตรียมการ

1. สร้างโปรเจคด้วย django-admin
2. สร้าง virtual environment ของ python สำหรับโปรเจค
3. สร้างไฟล์ requirement.txt และระบุแพคเก็จที่จำเป็นต้องใช้ในโปรเจค
4. ติดตั้งแพคเก็จที่จำเป็น ผ่าน pip install -r requirement.txt
5. สร้างไฟล์ runtime.txt
6. สร้างไฟล์ vercel.json
7. เตรียมไฟล์ .gitignore
8. สร้าง Origin repository บน Github
9. นำไฟล์ส่งไปเก็บบน Origin
10. สร้าง Project บน Vercel ผ่าน Dash Board
11. เชื่อมโยงระหว่าง Vercel App และ Origin repository บน Github
12. ทำการ Deploy Application ลงบน Vercel
