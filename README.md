# การจัดการ Static Files บน Vercel

โดย ผู้ช่วยศาสตราจารย์พิศาล สุขขี

Youtube : https://youtu.be/LGdMVUoMG24

เนื้อหา : กระบวนการติดตั้ง Django Application และการจัดการ Static Files บน Vercel ผ่าน Github

โดยมีขั้นตอนในการเตรียมการ

1. โคลน Project จาก Github remote repository
2. สร้าง virtual environment ของ python สำหรับโปรเจค
3. ติดตั้งแพคเก็จที่จำเป็นต้องใช้ในโปรเจคจากไฟล์ requirement.txt
4. ตั้งค่าไฟล์ vercel.json
5. สร้าง Origin repository บน Github
6. นำไฟล์ส่งไปเก็บบน Origin
7. สร้าง Project บน Vercel ผ่าน Dash Board
8. เชื่อมโยงระหว่าง Vercel App และ Origin repository บน Github
9. ทำการ Deploy Application ลงบน Vercel

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
