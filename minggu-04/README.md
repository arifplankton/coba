# Komunikasi Antar KOntainer

## Langkah 1 - Mulai Redis
Skenario yang paling umum untuk menghubungkan ke wadah adalah aplikasi yang menghubungkan ke penyimpanan data. 

### Mulai Penyimpanan Data
Jalankan server redis dengan nama ramah redis-server yang akan kita sambungkan pada langkah berikutnya. Ini akan menjadi wadah sumber.

![Step-1](image/kont-01.png)

## Langkah 2 - Buat Tautan
Untuk menghubungkan ke wadah sumber, Anda menggunakan opsi --link <container-name | id>: <alias> saat meluncurkan wadah baru. Nama kontainer merujuk ke sumber kontainer yang kami tentukan di langkah sebelumnya sementara alias mendefinisikan nama host yang ramah.

Anda dapat menampilkan semua variabel lingkungan dengan perintah env. Sebagai contoh:
![Step-2](image/kont-02.png)

Kedua, Docker akan memperbarui file HOSTS wadah dengan entri untuk wadah sumber dengan tiga nama, asli, alias dan hash-id. Anda dapat menampilkan entri host kontainer menggunakan cat / etc / hosts
![Step-3](image/kont-03.png)

Dengan tautan yang dibuat, dapat melakukan ping wadah sumber dengan cara yang sama seolah-olah itu server yang berjalan di jaringan Anda.

![Step-4](image/kont-04.png)

## Langkah 3 - Sambungkan Ke Aplikasi
Dengan tautan yang dibuat, aplikasi dapat terhubung dan berkomunikasi dengan wadah sumber dengan cara biasa, terlepas dari kenyataan bahwa kedua layanan berjalan dalam wadah.

Mengirim permintaan HTTP ke aplikasi akan menyimpan permintaan di Redis dan mengembalikan hitungan.
![Step-5](image/kont-05.png)

## Langkah 4 - Hubungkan ke Redis CLI
Dengan cara yang sama, Anda dapat menghubungkan wadah sumber ke aplikasi, Anda juga dapat menghubungkannya dengan alat CLI mereka sendiri.
### Meluncurkan Redis CLI
Perintah di bawah ini akan meluncurkan sebuah instance dari alat Redis-cli dan terhubung ke server redis melalui aliasnya.
![Step-6](image/kont-06.png)
### Perintah Penerbitan
Perintah KEYS * akan menampilkan konten yang disimpan saat ini dalam wadah sumber redis.
Ketik QUIT untuk keluar dari CLI.

# Docker  Network
## Langkah 1 - Buat Jaringan
Langkah pertama adalah membuat jaringan menggunakan CLI. Jaringan ini akan memungkinkan  untuk melampirkan banyak wadah yang dapat saling menemukan.

### Buat Jaringan
Untuk memulai, kami membuat jaringan dengan nama yang telah ditentukan sebelumnya.
![Step-6](image/Net-01.png)

### Sambungkan ke Jaringan
Saat kami meluncurkan kontainer baru, dapat menggunakan atribut --net untuk menetapkan jaringan mana yang harus dihubungkan.

![Step-7](image/Net-02.png)

## Langkah 2 - Komunikasi Jaringan
Tidak seperti menggunakan tautan, jaringan buruh pelabuhan berperilaku seperti jaringan tradisional tempat simpul dapat dilampirkan / dilepaskan.

![Step-8](image/Net-03.png)
![Step-9](image/Net-04.png)

Cara wadah dapat berkomunikasi melalui Server DNS Tertanam di Docker. Server DNS ini ditugaskan untuk semua kontainer melalui `IP 127.0.0.11` dan diatur dalam file resolv.conf.
![Step-10](image/Net-05.png)

Ketika wadah mencoba mengakses wadah lain melalui nama yang terkenal, seperti Redis, server DNS akan mengembalikan alamat IP wadah yang benar.
![Step-11](image/Net-06.png)

## Hubungkan Dua Kontainer
Docker mendukung beberapa jaringan dan wadah yang terhubung ke lebih dari satu jaringan sekaligus.

membuat jaringan baru dengan cara yang sama.
![Step-12](image/Net-07.png)

Saat menggunakan perintah hubungkan, dimungkinkan untuk melampirkan wadah yang ada ke jaringan.
![Step-13](image/Net-08.png)

Ketika kami meluncurkan server web, mengingat itu terlampir pada jaringan yang sama itu akan dapat berkomunikasi dengan instance Redis.
![Step-14](image/Net-09.png)

Untuk mengujinya dengan `curl docker:3000`
![Step-15](image/Net-10.png)

## Langkah 4 - Buat Alias
Tautan masih didukung saat menggunakan jaringan buruh pelabuhan dan menyediakan cara untuk mendefinisikan Alias dengan nama wadah.

### Hubungkan Kontainer dengan Alias
Perintah berikut akan menghubungkan instance Redis ke jaringan frontend dengan alias dari db.
![Step-16](image/Net-11.png)

Ketika kontainer mencoba mengakses layanan melalui nama db, mereka akan diberi alamat IP dari kontainer Redis.
![Step-17](image/Net-12.png)

## Langkah 5 - Putuskan Kontainer
Dengan jaringan yang dibuat,dapat menggunakan CLI untuk menjelajahi detailnya.

Perintah berikut akan mencantumkan semua jaringan di host.
![Step-18](image/Net-13.png)

kemudian dapat menjelajahi jaringan untuk melihat wadah mana yang dilampirkan dan alamat IP.
![Step-19](image/Net-14.png)

Perintah berikut ini memutus wadah redis dari jaringan frontend.
![Step-20](image/Net-15.png)
