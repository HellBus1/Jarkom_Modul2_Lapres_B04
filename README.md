# Jarkom_Modul2_Lapres_B04
**Setting utama server dan client**

Untuk setting utama, kita memiliki 2 switch, 1 router SURABAYA, kemudian 2 client SIDOARJO dan GRESIK, lalu 3 server yaitu MALANG, MOJOKERTO, dan probolinggo. Untuk setting topologinya adalah sebagai berikut :

![soal-utama2](img/utama2.jpg)

#### 1. Website utama dengan alamat http://semerub04.pw
pada uml malang kita ketik command berikut
```
nano /etc/bind/named.conf.local
```
lalu akan memunculkan isi dari file tersebut kemudian kita buat zone semerub04.pw seperti gambar berikut

![soal-satu](img/nomor01.jpg)

kemudian buat folder jarkom dengan perintah
```
mkdir /etc/bind/jarkom
```
lalu file db.local pada path **/etc/bind** kedalam folder jarkom yang sudah dibuat tadi dan namanya dirubah menjadi semerub04.pw
```
cp /etc/bind/db.local /etc/bind/jarkom/semerub04.pw
```
kemudian pada file semerub04.pw diedit menjadi seperti berikut :

![soal-satu1](img/nomor1.jpg)

#### 2. Alias http://www.semerub04.pw
Untuk menambahkan alias, kita perlu membuat record CNAME pada file semerub04.pw pada /etc/bind/jarkom seperti berikut :

![soal-dua](img/nomor2.jpg)

#### 3. Subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO 
Untuk menambahkan subdomain, kita perlu membuat record A dengan nama penanjakan di kolom pertama dan ip tujuan disini kita menggunakan ip PROBOLINGGO pada kolom keempat pada file semerub04.pw pada /etc/bind/jarkom seperti berikut :

![soal-tiga](img/nomor3.jpg)

#### 4. reverse domain untuk domain utama
Untuk melakukan reverse domain utama (semerub04.pw) kita buka named.conf.local pada malang lalu ditambahkan perintah seperti berikut :

![soal-empat](img/nomor4.jpg)

setelah membuat config diatas selanjutnya kita buat file dengan nama reverse ip malang yaitu 83.151.10.in-adrr.arpa yang berasal dari copy db.local ke folder jarkom. Lalu file tersebut diedit seperti berikut:

![soal-empat1](img/nomor41.jpg)

#### 5. (5) DNS Server Slave pada MOJOKERTO 

Untuk membuat master slave  kita buat config pada file named.conf.local pada uml MALANG sebagai master dengan menambahkan type lalu ditambah also-notify dan allow-transfer pada ip MOJOKERTO sebagai slave, confignya seperti berikut :

![soal-lima](img/nomor5.jpg)

lalu pada named.conf.local pada uml MOJOKERTO dibuat type slave dengan konfigurasi seperti berikut :

![soal-lima1](img/nomor51.jpg)

Setelah itu kita comment nameserver malang pada salah satu client (GRESIK)

![soal-lima2](img/nomor52.jpg)

Kemudian dilakukan ping, outputnya seperti berikut :

![soal-lima](img/nomor53.jpg)

### 6. subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO.

Pertama kita buat ns1 dengan tipe A mengarah ke IP MOJOKERTO sebagai tujuan kemudian dibuat subdomain gunung lali diberi nilai tujuan ns1, confignya sebagai berikut:

![soal-tujuh](img/soal7.jpg)

kemudian kita comment dnssec-validation auto dan ditambahkan allow-query pada named.conf.options pada malang, confignya sebagai berikut :

![soal-tujuh1](img/soal71.jpg)

Lalu pada named.conf.local MALANGT dibuat seperti berikut :

![soal-tujuh2](img/soal73.jpg)

Kemudian pada MOJOKERTO juga comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options, kemudian kita setting named.conf.local seperti berikut

![soal-tujuh3](img/soal74.jpg)

kemudian kita buat folder delegasi pada /etc/bind/ dan mengkopi db.local dengan nama subdomain yaitu gunung.semerub04.pw seperti berikut

```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/its.jarkom2020.com
```
Lalu edit filenya seperti berikut :

![soal-tujuh4](img/7.5.jpg)

dan dilakukan ping sebagai berikut :

![soal-tujuh5](img/7.6.jpg)

#### 7. subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.

Pada /etc/bind/delegasi/its.jarkom2020.com kita buat seperti berikut :

![soal-tujuh6](img/7.7.jpg)

#### 8. Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home.

pada folder /etc/apache2/sites-available kita buat file bernama semerub04.pw yang merupakan hasil kopi dari file default pada folder tersebut, kemudian kita config sebagai berikut :

![soal-delapan1](img/8.2sites-available.png)

pada DocumentRoot kita arahkan ke /var/www/semerub04.pw yang akan dibuat nanti, folder ini berisi file yang didownload dari 10.151.36.202/semeru.pw.zip. Setelah kita membuat folder semerub04.pw dan diisi file tersebut maka kita bisa langsung mengakses alamat semerub04.pw dan hasilnya seperti berikut :

![soal-delapan](img/8.1websemerub04pw.png)

#### 9. diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.

Pada soal ini dibuat file .htaccess pada folder semerub04.pw di /var/www sebelumnya dan kita config seperti berikut :

![soal-sembilan](img/9.1htaccessrewrite.PNG)

dimana kita rewrite nama /index.php/home menjadi home, sehingga hasilnya seperti dua gambar dibawah :

![soal-sembilan](img/9.2semerub04pwhome.PNG)

![soal-sembilan](img/9.3semerub04pwindexphphome.PNG)

#### 10. Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut: 

/var/www/penanjakan.semeruyyy.pw

/public/javascripts

/public/css

/public/images

/errors

Untuk membuat directory listing, pertama-tama pada konfigurasi web penanjakan.semerub04.pw yang berada di direktori /etc/apache2/sites-available kita arahkah root dari web 
ke direktori /var/www/penanjakan.semerub04.pw. Selanjutnya kita tambahkan 

<Directory /var/www/penanjakan.semerub04.pw>
     Options +Indexes
 </Directory>

Dengan menambah opsi +Indexes maka dihasilkan tampilan directory listing

![soal-sepuluh](img/10.4sitesavailablepenanjakan1.PNG)

![soal-sepuluh](img/10.2directoryroot.PNG)

![soal-sepuluh](img/10.3directorypubliccssimagesjavascript.PNG)

![soal-sepuluh](img/10.1penanjakanlisting.PNG)

#### 11. Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan.

Untuk soal no 11, karna folder didalam direktori public tidak diperbolahkan directory listing, maka pada konfigruasi web
kita  tambahkan 

Option -Indexes

![soal-delapan1](img/10.5sitesavailablepenanjakan2.PNG)

![soal-sebelas](img/11.1listingpublic.PNG)

![soal-sebelas](img/11.2listingpubliccss.PNG)

![soal-sebelas](img/11.3listingpublicimages.PNG)

![soal-sebelas](img/11.4listingpublicjs.PNG)

![soal-sebelas](img/11.5sitesavailablepenanjakanlisting.PNG)

#### 12. Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.

Pada soal ini kita tambahkan 
```
ErrorDocument 404 /errors/404.html
```

pada file penanjakan.semerub04.pw dimana ketika url akan diarahkan ke halaman 404.html pada folder error pada folder penanjakan.semerub04.pw

![soal-duabelas](img/12.1eror404.PNG)

Outputnya akan seperti berikut :

![soal-duabelas](img/12.2eror404web.PNG)

#### 13. Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js.

Pada soal ini dibuat alias pada file penanjakan.semerub04.pw dengan konfigurasi seperti berikut :

![soal-tigabelas](img/13.1alias.PNG)

Maka hasilnya akan seperti berikut :

![soal-tigabelas](img/13.2js.PNG)

#### 14. sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw.

Untuk soal ini kita cukup mengganti 8080 pada virtual host file naik.gunung.semerub04.pw dengan 8888 kemudian ditambahkan listen 8888 pada file /etc/apache2/ports.conf, konfigurasinya akan seperti berikut :

![soal-empatbelas](img/14.1port8888.PNG)

<!-- TODO -->

#### 15. web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya.

<!-- TODO -->

Pada soal ini kita buat file .htpasswd didalam folder naik.gunung.semerub04.pw lalu dibuat config .htaccess sebagai berikut

![soal-limabelas](img/15.2htaccess.PNG)

Kemudian outputnya akan seperti berikut :

![soal-limabelas](img/15.1auth.PNG)

#### 16. setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw.

Pada soal ini kita cukup menambahkan 
```
Redirect / http://www.semerub04.pw 
```

pada file default dan default-ssl pada folder /etc/apache2/sites-available

![soal-enambelas](img/16.1redirect.PNG)

![soal-enambelas](img/16.2redirect2.PNG)

Outputnya akan seperti berikut

![soal-enambelas](img/16.3redirect3.PNG)

#### 17. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.
