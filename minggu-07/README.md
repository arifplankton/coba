# GO

## Step 1 — Install Go

Perbarui dan tingkatkan paket Ubuntu laptop. Ini memastikan bahwa Anda memiliki tambalan dan perbaikan keamanan terbaru, serta repo yang diperbarui untuk paket baru Anda.

`sudo apt-get update
sudo apt-get -y upgrade`

unduh paket terbaru untuk Go dengan menjalankan perintah ini.

`curl -O https://storage.googleapis.com/golang/go1.11.2.linux-amd64.tar.gz`

selanjutnya, gunakan tar untuk membongkar paket. Perintah ini akan menggunakan alat Tar untuk membuka dan memperluas file yang diunduh

`tar -xvf go1.11.2.linux-amd64.tar.gzsudo mv go /usr/local`

## Step 2 — Setting Go Paths

menetapkan beberapa jalur yang dibutuhkan Go Path. Biasanya  lokasi instalasi Go Anda di / usr / local. Jika Anda memilih direktori baru, atau meninggalkan file di lokasi unduhan, ubah perintah agar sesuai dengan lokasi baru Anda.

Pertama, atur nilai root Go, yang memberi tahu Go tempat mencari file-nya.

`sudo nano ~/.profile`

di akhir file, tambahkan baris ini:

`export GOPATH=$HOME/work
export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin`

Jika Anda memilih lokasi instalasi alternatif untuk Go, tambahkan baris ini sebagai gantinya.
contoh:
`xport GOROOT=$HOME/go
export GOPATH=$HOME/work
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin`

segarkan profil Anda dengan menjalankan:
`source ~/.profile`

## tep 3 — Testing your go 1.11.2 installation

Sekarang Go telah diinstal. Untuk memastikan bahwa Go berfungsi seperti yang diharapkan.
`go version //and it should print the installed go version 1.11.2`

Buat direktori baru untuk ruang kerja Go Anda, di mana Go akan membangun file-nya.
`mkdir $HOME/work`

sekarang arahkan  ke ruang kerja baru yang baru saja Anda buat dengan mengekspor `GOPATH`, jika Anda belum pernah melakukannya sebelumnya.
`export GOPATH=$HOME/work`


Lalu, buat hierarki direktori di folder ini melalui perintah ini agar Anda dapat membuat file pengujian Anda. Anda dapat mengganti pengguna nilai dengan nama pengguna GitHub Anda jika Anda berencana untuk menggunakan Git untuk melakukan dan menyimpan kode Go Anda di GitHub.
`mkdir -p work/src/github.com/user/hello`

Selanjutnya, dapat membuat file Go “Hello World” sederhana.
`nano work/src/github.com/user/hello/hello.go`

Di dalam editor , tempel konten yang di bawah ini, yang menggunakan paket Go utama.
`package mainimport "fmt"func main() {
    fmt.Printf("hello, world")
}`

file ini akan menampilkan "hello, world" jika berhasil berjalan.

Dengan file yang dikompilasi, dapat menjalankannya dengan hanya merujuk ke file di jalur Go Anda.

`sudo $GOPATH/bin/hello`

