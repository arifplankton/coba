# Kubernetes

Kita mulai kita perlu meluncurkan cluster Kubernetes.
Jalankan perintah di bawah ini untuk memulai komponen kluster dan unduh Kubectl CLI.
![Step-1](image/kub-01.png)

Tunggu sampai Node menjadi Siap dengan memeriksa
![Step-2](image/kub-02.png)

## Langkah 2 - Jalankan Kubectl
Perintah jalankan membuat penyebaran berdasarkan parameter yang ditentukan, seperti gambar atau replika. Penempatan ini dikeluarkan untuk master Kubernetes yang meluncurkan Pods dan kontainer yang diperlukan. Kubectl run_ mirip dengan docker run tetapi pada level cluster.

Format perintahnya adalah kubectl menjalankan <name of deployment> <properties>

Perintah berikut akan meluncurkan penyebaran yang disebut http yang akan memulai sebuah wadah berdasarkan Docker Image katacoda / docker-http-server: terbaru.
![Step-3](image/kub-03.png)

Kemudian dapat menggunakan kubectl untuk melihat status penyebaran
![Step-4](image/kub-04.png)

Untuk mencari tahu apa yang dibuat Kubernetes, Anda bisa mendeskripsikan proses penyebaran.
![Step-5](image/kub-05.png)

## Langkah 3 - Kubectl Expose
Dengan penyebaran yang dibuat, kita dapat menggunakan kubectl untuk membuat layanan yang memaparkan Pods pada port tertentu.

Gunakan perintah berikut untuk mengekspos port kontainer 80 pada host 8000 yang mengikat ip eksternal host.
![Step-6](image/kub-06.png)

kemudian dapat melakukan ping host dan melihat hasilnya dari layanan HTTP.
![Step-7](image/kub-07.png)

## Langkah 4 - Jalankan Kubectl dan Ekspos
Dengan menjalankan kubectl dimungkinkan untuk membuat penyebaran dan mengeksposnya sebagai satu perintah.

Gunakan perintah perintah untuk membuat layanan http kedua yang terbuka di port 8001.
![Step-8](image/kub-8.png)

mengaksesnya menggunakan
![Step-09](image/kub-09.png)
![Step-10](image/kub-10.png)

Untuk menemukan detail yang bisa di gunakan
![Step-11](image/kub-11.png)

## Langkah 5 - Skala Kontainer
Dengan menjalankan penyebaran kami, kami sekarang dapat menggunakan kubectl untuk mengukur jumlah replika.

Skala perintah kubectl memungkinkan kita untuk menyesuaikan jumlah Pods yang berjalan untuk pengendali penempatan atau replikasi tertentu.
![Step-12](image/kub-12.png)

Mendaftar semua pod, Anda akan melihat tiga berjalan untuk penyebaran http
![Step-13](image/kub-13.png)

Setelah setiap Pod dimulai, ia akan ditambahkan ke layanan penyeimbang beban. Dengan menjelaskan layanan, Anda dapat melihat titik akhir dan Pod terkait yang disertakan.
![Step-14](image/kub-14.png)

# Membuat permintaan ke layanan akan meminta di beberapa node memproses permintaan tersebut.

# Langkah 1 - Buat Penempatan
Salah satu objek Kubernetes yang paling umum adalah objek penyebaran.

Salin definisi berikut ke editor.
![Step-15](image/kub-15.png)

Ini digunakan untuk cluster dengan perintah
![Step-16](image/kub-16.png)

Karena ini adalah objek Penerapan, daftar semua objek yang digunakan dapat diperoleh melalui
![Step-17](image/kub-17.png)

## Langkah 2 - Buat Layanan
Kubernetes memiliki kemampuan jaringan yang kuat yang mengontrol cara aplikasi berkomunikasi. Konfigurasi jaringan ini juga dapat dikontrol melalui YAML

Salin definisi Layanan ke editor. 
![Step-18](image/kub-18.png)

Menyebarkan Layanan dengan
![Step-19](image/kub-19.png)

Seperti sebelumnya, detail semua objek Layanan yang digunakan dengan perintah `kubectl get svc`
![Step-20](image/kub-20.png)

Dengan menjelaskan objek, Anda dapat menemukan detail lebih lanjut tentang konfigurasi dengan perintah `kubectl describe svc webapp-svc`
![Step-21](image/kub-21.png)
![Step-22](image/kub-22.png)

## Langkah 3 - Skala Penempatan
Rincian YAML dapat diubah karena konfigurasi yang berbeda diperlukan untuk penerapan. Ini mengikuti infrastruktur sebagai pola pikir kode.

Pembaruan definisi yang ada diterapkan menggunakan kubectl apply. Untuk skala jumlah replika, gunakan file YAML yang diperbarui menggunakan
![Step-23](image/kub-23.png)

Seketika, keadaan yang diinginkan dari kluster kami telah diperbarui, dapat dilihat dengan
![Step-24](image/kub-24.png)

Pod tambahan akan dijadwalkan agar sesuai dengan permintaan.
![Step-25](image/kub-25.png)

Mengeluarkan permintaan ke pelabuhan akan menghasilkan berbagai wadah memproses permintaan
![Step-26](image/kub-26.png)