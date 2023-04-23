# การจัดการ Static Files บน Vercel

โดย ผู้ช่วยศาสตราจารย์พิศาล สุขขี

Youtube : https://youtu.be/19ik7cS8A5Q

เนื้อหา : กระบวนการติดตั้ง Django Application และการจัดการ Static Files บน Vercel ผ่าน Github

โดยมีขั้นตอนในการเตรียมการ

1. (2:30) โคลน Project จาก Github remote repository
2. (5:15) สร้าง repository ใหม่
3. (6:18) กำหนดค่า git remote url
4. (7:50) สร้าง virtual environment ของ python สำหรับโปรเจค
5. (9:14) ติดตั้งแพคเก็จที่จำเป็นต้องใช้ในโปรเจคจากไฟล์ requirement.txt
6. (10:30) การเพิ่มเทมเพลต และการจัดการ Static Files
7. (19:25) การสร้าง Static Root
8. (23:00) ตั้งค่าไฟล์ vercel.json
9. (24:50) สร้างไฟล์ build_files.sh
10. (27:00) พุช Source ไปที่ Origin repository บน Github
11. (27:55) สร้างโปรเจคใหม่บน Vercel
12. (29:00) คอมเมนต์ดาต้าเบสใน settings.py

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
  "version": 2,
  "builds": [
    {
      "src": "deploy_demo/wsgi.py",
      "use": "@vercel/python"
    },
    {
      "src": "build_files.sh",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "staticfiles_build"
      }
    }
  ],
  "routes": [
    {
      "src": "/static/(.*)",
      "dest": "/static/$1"
    },
    {
      "src": "/(.*)",
      "dest": "deploy_demo/wsgi.py"
    }
  ]
}
```

ทำการสร้างไฟล์ build_fiiles.sh

```shell
pip install -r requirements.txt
python3.9 manage.py collectstatic --noinput --clear
```

ทำการตั้งต่า Static
settings.py

```python
import os
.
.
STATIC_URL = '/static/'

STATICFILES_DIRS = [BASE_DIR / 'statics', ]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles_build', 'static')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```
