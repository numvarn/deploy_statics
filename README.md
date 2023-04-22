# การติดตั้ง Django บน Vercel ผ่าน Github

โดย ผู้ช่วยศาสตราจารย์พิศาล สุขขี

Youtube : https://youtu.be/LGdMVUoMG24

เนื้อหา : กระบวนการติดตั้ง Django บน Heroku ผ่าน Github โดยมีขั้นตอนในการเตรียมการ

1. สร้างโปรเจคด้วย django-admin
2. สร้าง virtual environment ของ python สำหรับโปรเจค
3. สร้างไฟล์ requirement.txt และระบุแพคเก็จที่จำเป็นต้องใช้ในโปรเจค
4. ติดตั้งแพคเก็จที่จำเป็น ผ่าน pip install -r requirement.txt
5. สร้างไฟล์ vercel.json
6. เตรียมไฟล์ .gitignore
7. สร้าง Origin repository บน Github
8. นำไฟล์ส่งไปเก็บบน Origin
9. สร้าง Project บน Vercel ผ่าน Dash Board
10. เชื่อมโยงระหว่าง Vercel App และ Origin repository บน Github
11. ทำการ Deploy Application ลงบน Vercel

## การเตรียมค่า Config ก่อนการ Deploy

ไฟล์ /<โปรเจค>/wsgi.py

```python
.
.
application = get_wsgi_application()

app = application
```

ไฟล์ /<โปรเจค>/settings.py

```python
ALLOWED_HOSTS = ['127.0.0.1', '.vercel.app']
```

ไฟล์ /vercel.json

```json
{
  "builds": [
    {
      "src": "deploy_demo/wsgi.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "deploy_demo/wsgi.py"
    }
  ]
}
```
