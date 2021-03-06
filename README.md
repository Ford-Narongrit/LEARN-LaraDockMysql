# ทดลอง Docker => laravel + mysql

## Setup

1. สร้าง folder สำหรับ Database Mysql => `mkdir mysql`
2. สั่งสร้าง image และ container ตามลำดับ => ``docker-compose build && docker-compose up -d``
3. เช็คว่า container run ทุกตัวหรือไม่ => ``docker ps``
4. เข้าไปใน ./src แล้ว =>
* ```
    composer update
    cp .env.example .env
    php artisan key:generate
    ```
* ในขั้นตอนนี้สามารถใช้ ``docker-compose exec php`` เพื่อเข้าไปใช้ command ในเครื่อง docker แทนได้เช่น ``docker-compose exec php php artisan key:generate``

5. ลองเข้าไปที่ http://localhost:8088 เพื่อดูผลลัพธ์

## Migrate 

1. เข้าไปแก้ไข .env ให้ DB_HOST=mysql เพื่อเชื่อมกับ container mysql
2. นำค่าของ environment ของ mysql มาใส่ลงใน .env (DB_DATABASE, DB_DATABASE, DB_PASSWORD)
3. สั่ง ``docker-compose exec php php artisan migrate`` เพื่อ migrate ตารางใน Mysql container
4. ลองเรียก API 
    * `get` http://localhost:8088/api/posts
    * `post` http://localhost:8088/api/posts

## structure
```
.
|-- mysql => ที่เก็บ Database
|
|-- nginx => webserve
|     |-- default.conf => config websever
|
|-- src => !edit in here
|    |-- pubilc => ตัวเริ่มจำเป็นต้องมี index.php หรือ index.html
|
|-- Dockerfile
|-- docker-compose.yml
```

## ref
* คลิปสอน: https://www.youtube.com/watch?v=5N6gTVCG_rw

* github ของคลิปสอน: https://github.com/aschmelyun/docker-compose-laravel
