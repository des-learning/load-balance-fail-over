# Load Balance and Fail Over

Contoh arsitektur aplikasi dengan menggunakan load balancer untuk
membagi beban (load balance) request ke beberapa application server.

Pada arsitektur ini, apabila salah satu application server padam,
request dari client akan diarahkan ke application server yang masih menyala.
Apabila application yang padam tersebut sudah menyala, request dapat diarahkan
kembali ke seluruh application server yang menyala.

Arsitektur aplikasi:

Client ----- Load Balancer ----- Application Server 1
              |
              +----------------- Application Server 2

Load Balancer: nginx
Application Server 1 & 2: php-fpm

## cara penggunaan

1. Pasang docker engine untuk menjalankan container

2. Pasang docker-compose

3. Aktifkan container, `docker-compose up -d`

4. Akses layanan melalui web browser, http://localhost/backends/index.php

5. Matikan salah satu backend, `docker-compose stop backend0`

6. Akses kembali layanan

7. Menyalakan backend, `docker-compose start backend0`


## konfigurasi

Backend 0 dan 1 adalah application server yang menjalankan php-fpm.
Kedua container tersebut sudah di konfigurasikan untuk menjalankan script yang
ada di directory public_html0 dan public_html1.

Konfigurasi nginx berada di file default.conf. Berisikan konfigurasi url dan
deklarasi server backend.
