<h1 align="center">Laporan Praktikum Modul 4</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Golang atau **Go** adalah bahasa pemrograman open-source yang dikembangkan oleh Google pada tahun 2009. Bahasa ini dirancang untuk memiliki **kinerja tinggi**, **sintaks sederhana**, serta mendukung **pemrograman konkuren (concurrency)** dengan mudah. Struktur dasar program Golang selalu diawali dengan **package main** dan fungsi utama **func main()** sebagai entry point. Program Go juga mendukung berbagai tipe data seperti **numerik** (`int`, `float32`, `float64`), **boolean** (`bool`), **string**, serta tipe **komposit** seperti `array`, `slice`, `map`, dan `struct`. Variabel dalam Go dapat dideklarasikan menggunakan kata kunci `var`, sedangkan konstanta menggunakan `const`. Selain itu, terdapat shorthand deklarasi variabel menggunakan `:=`. Dalam hal kontrol alur, Go mendukung struktur seperti **if-else**, **for loop**, dan **switch-case** untuk pengambilan keputusan dan perulangan. Fungsi dalam Golang dideklarasikan dengan kata kunci `func` dan dapat memiliki parameter serta nilai yang dikembalikan.


## Unguided

### -Soal 1
Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian membantu Jonas? (tidak tentunya ya :p) Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi, dengan syarat 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑. Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂 terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑. Catatan: permutasi (P) dan kombinasi (C) dari 𝑛 terhadap 𝑟 (𝑛 ≥ 𝑟) dapat dihitung dengan menggunakan persamaan berikut!

```go
package main
import "fmt"

func faktorial(n int, hasil *int) {
    *hasil = 1
    for i := 1; i <= n; i++ {
        *hasil *= i
    }
}

func permutasi(n, r int, hasil *int) {
    var nFact, nrFact int
    faktorial(n, &nFact)
    faktorial(n-r, &nrFact)
    *hasil = nFact / nrFact
}

func kombinasi(n, r int, hasil *int) {
    var nFact, rFact, nrFact int
    faktorial(n, &nFact)
    faktorial(r, &rFact)
    faktorial(n-r, &nrFact)
    *hasil = nFact / (rFact * nrFact)
}
  
func main() {
    var a, b, c, d int
  
    fmt.Scan(&a, &b, &c, &d)
  
    if a < c || b < d {
        fmt.Println("Input tidak valid")
        return
    }
  
    // Menghitung permutasi dan kombinasi untuk a dan c
    var permAC, combAC int
    permutasi(a, c, &permAC)
    kombinasi(a, c, &combAC)
  
    // Menghitung permutasi dan kombinasi untuk b dan d
    var permBD, combBD int
    permutasi(b, d, &permBD)
    kombinasi(b, d, &combBD)
  
    fmt.Printf("%d %d\n", permAC, combAC)
    fmt.Print(permBD, combBD)
}
```

![[soal1.png]]

Program ini menghitung permutasi dan kombinasi berdasarkan input empat bilangan asli a, b, c, dan d dengan syarat a≥c dan b≥d. Program menggunakan tiga prosedur utama: `factorial` untuk menghitung faktorial suatu bilangan, `permutation` untuk menghitung permutasi P(n,r)=n!/(n−r)!​, dan `combination` untuk menghitung kombinasi C(n,r)=n!/r!⋅(n−r)!​. Setelah menerima input, program memvalidasi syarat a≥c dan b≥d, lalu menghitung permutasi dan kombinasi untuk pasangan (a,c) dan (b,d). Hasilnya ditampilkan dalam dua baris, masing-masing berisi nilai permutasi dan kombinasi untuk setiap pasangan. 


### -Soal 2
Kompetisi pemrograman tingkat nasional berlangsung ketat. Setiap peserta diberikan 8 soal yang harus dapat diselesaikan dalam waktu 5 jam saja. Peserta yang berhasil menyelesaikan soal paling banyak dalam waktu paling singkat adalah pemenangnya. Buat program gema yang mencari pemenang dari daftar peserta yang diberikan. Program harus dibuat modular, yaitu dengan membuat prosedur hitungSkor yang mengembalikan total soal dan total skor yang dikerjakan oleh seorang peserta, melalui parameter formal. Pembacaan nama peserta dilakukan di program utama, sedangkan waktu pengerjaan dibaca di dalam prosedur. prosedure hitungSkor(in/out soal, skor : integer) Setiap baris masukan dimulai dengan satu string nama peserta tersebut diikuti dengan adalah 8 integer yang menyatakan berapa lama (dalam menit) peserta tersebut menyelesaikan soal. Jika tidak berhasil atau tidak mengirimkan jawaban maka otomatis dianggap menyelesaikan dalam waktu 5 jam 1 menit (301 menit). Satu baris keluaran berisi nama pemenang, jumlah soal yang diselesaikan, dan nilai yang diperoleh. Nilai adalah total waktu yang dibutuhkan untuk menyelesaikan soal yang berhasil diselesaikan

```go
package main
import "fmt"
  
func hitungSkor(waktuPengerjaan [8]int, totalSoal *int, totalSkor *int) {
    *totalSoal = 0
    *totalSkor = 0
    for _, waktu := range waktuPengerjaan {
        if waktu <= 300 {
            *totalSoal++
            *totalSkor += waktu
        }
    }
}
  
func main() {
    var jumlahPeserta int
    fmt.Scan(&jumlahPeserta)
  
    var pemenang string
    var maxSoal, minSkor int
 
    for i := 0; i < jumlahPeserta; i++ {
        var nama string
        var waktuPengerjaan [8]int
  
        fmt.Scan(&nama)
  
        for j := 0; j < 8; j++ {
            fmt.Scan(&waktuPengerjaan[j])
            if waktuPengerjaan[j] > 300 {
                waktuPengerjaan[j] = 301
            }
        }
  
        var totalSoal, totalSkor int
        hitungSkor(waktuPengerjaan, &totalSoal, &totalSkor)
  
        if totalSoal > maxSoal || (totalSoal == maxSoal && totalSkor < minSkor) {
            pemenang = nama
            maxSoal = totalSoal
            minSkor = totalSkor
        }
    }
 
    fmt.Printf("%s\n", pemenang)
    fmt.Printf("%d\n", maxSoal)
    fmt.Print(minSkor)
}
```

![[soal2.png]]

Program ini dirancang untuk menentukan pemenang dalam kompetisi pemrograman berdasarkan jumlah soal yang berhasil diselesaikan dan total waktu yang digunakan. Program menggunakan prosedur `hitungSkor` yang menerima waktu pengerjaan 8 soal dari setiap peserta dan menghitung total soal yang selesai (waktu ≤ 300 menit) serta total waktu yang digunakan. Di program utama, input nama peserta dan waktu pengerjaan dibaca, dengan waktu > 300 menit dianggap tidak selesai (di-set ke 301 menit). Prosedur `hitungSkor` dipanggil untuk setiap peserta, dan pemenang ditentukan berdasarkan peserta dengan jumlah soal terbanyak. Jika jumlah soal sama, pemenang adalah peserta dengan total waktu terkecil. Hasilnya mencakup nama pemenang, jumlah soal yang diselesaikan, dan total waktu yang digunakan.


### -Soal 3
Skiena dan Revilla dalam Programming Challenges mendefinisikan sebuah deret bilangan. Deret dimulai dengan sebuah bilangan bulat n. Jika bilangan n saat itu genap, maka suku berikutnya adalah ½n, tetapi jika ganjil maka suku berikutnya bernilai 3n+1. Rumus yang sama digunakan terus menerus untuk mencari suku berikutnya. Deret berakhir ketika suku terakhir bernilai 1. Sebagai contoh jika dimulai dengan n=22, maka deret bilangan yang diperoleh adalah: 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 Untuk suku awal sampai dengan 1000000, diketahui deret selalu mencapai suku dengan nilai 1. Buat program skiena yang akan mencetak setiap suku dari deret yang dijelaskan di atas untuk nilai suku awal yang diberikan. Pencetakan deret harus dibuat dalam prosedur cetakDeret yang mempunyai 1 parameter formal, yaitu nilai dari suku awal. prosedure cetakDeret(in n : integer ) Masukan berupa satu bilangan integer positif yang lebih kecil dari 1000000. Keluaran terdiri dari satu baris saja. Setiap suku dari deret tersebut dicetak dalam baris yang dan dipisahkan oleh sebuah spasi.

```go
package main
import "fmt"
  
func cetakDeret(n int) {
    for n != 1 {
        fmt.Printf("%d ", n)
        if n%2 == 0 {
            n = n / 2
        } else {
            n = 3*n + 1
        }
    }
    fmt.Println(1)
}
  
func main() {
    var n int
  
    fmt.Scan(&n)
    cetakDeret(n)
}
```

![[soal3.png]]

Program ini mencetak deret bilangan berdasarkan aturan yang dijelaskan oleh Skiena dan Revilla. Deret dimulai dengan bilangan bulat positif `n` (kurang dari 1.000.000), dan setiap suku berikutnya dihitung berdasarkan aturan: jika suku saat ini genap, suku berikutnya adalah n/2, sedangkan jika ganjil, suku berikutnya adalah ( 3n + 1 ). Deret berhenti ketika mencapai nilai 1. Program menggunakan prosedur `cetakDeret` yang menerima suku awal `n` dan mencetak setiap suku dalam satu baris, dipisahkan oleh spasi. Di program utama, input suku awal divalidasi untuk memastikan n adalah bilangan positif dan kurang dari 1.000.000. Jika valid, prosedur `cetakDeret` dipanggil untuk mencetak deret tersebut. Program ini sederhana, modular, dan memastikan deret selalu berakhir pada 1.