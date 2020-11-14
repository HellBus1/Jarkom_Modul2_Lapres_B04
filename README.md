# Jarkom_Modul2_Lapres_B04
**Setting utama server dan client**
![soal-utama](img/utama1.jpg)
![soal-utama2](img/utama2.jpg)

#### 1. Website utama dengan alamat http://semerub04.pw
![soal-satu](img/nomor01.jpg)
![soal-satu1](img/nomor1.jpg)

#### 2. Alias http://www.semerub04.pw
![soal-dua](img/nomor2.jpg)

#### 3. Subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO 
![soal-tiga](img/nomor3.jpg)

#### 4. reverse domain untuk domain utama
![soal-empat](img/nomor4.jpg)
![soal-empat1](img/nomor41.jpg)

#### 5. subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO.
![soal-lima](img/nomor5.jpg)
![soal-lima1](img/nomor51.jpg)
![soal-lima2](img/nomor52.jpg)
![soal-lima](img/nomor53.jpg)

#### 6. subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.
![soal-enam](img/nomor6.jpg)

#### 7. Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home.
![soal-tujuh](img/soal7.jpg)
![soal-tujuh1](img/soal71.jpg)
![soal-tujuh2](img/soal73.jpg)
![soal-tujuh3](img/soal74.jpg)

#### 8. diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.

#### 9. Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut: 

/var/www/penanjakan.semeruyyy.pw

/public/javascripts

/public/css

/public/images

/errors


#### 10. Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan. (12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.

#### 11. Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js.

#### 12. sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw.

#### 13. web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya.

#### 14. setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw.

#### 15. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.
