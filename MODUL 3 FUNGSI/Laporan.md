<h1 align="center">Laporan Praktikum Modul 3</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Golang atau **Go** adalah bahasa pemrograman open-source yang dikembangkan oleh Google pada tahun 2009. Bahasa ini dirancang untuk memiliki **kinerja tinggi**, **sintaks sederhana**, serta mendukung **pemrograman konkuren (concurrency)** dengan mudah. Struktur dasar program Golang selalu diawali dengan **package main** dan fungsi utama **func main()** sebagai entry point. Program Go juga mendukung berbagai tipe data seperti **numerik** (`int`, `float32`, `float64`), **boolean** (`bool`), **string**, serta tipe **komposit** seperti `array`, `slice`, `map`, dan `struct`. Variabel dalam Go dapat dideklarasikan menggunakan kata kunci `var`, sedangkan konstanta menggunakan `const`. Selain itu, terdapat shorthand deklarasi variabel menggunakan `:=`. Dalam hal kontrol alur, Go mendukung struktur seperti **if-else**, **for loop**, dan **switch-case** untuk pengambilan keputusan dan perulangan. Fungsi dalam Golang dideklarasikan dengan kata kunci `func` dan dapat memiliki parameter serta nilai yang dikembalikan.


## Unguided

### -Soal 1
Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian membantu Jonas? (tidak tentunya ya :p) 
Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi, dengan syarat 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑. 
Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂 terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑. Catatan: permutasi (P) dan kombinasi (C) dari 𝑛 terhadap 𝑟 (𝑛 ≥ 𝑟) dapat dihitung dengan menggunakan persamaan berikut!

```go
package main
import "fmt"

func faktorial(n int) int {
    if n == 0 {
        return 1
    }
    return n * faktorial(n-1)
}
  
func permutasi(n, r int) int {
    return faktorial(n) / faktorial(n-r)
}
  
func kombinasi(n, r int) int {
    return faktorial(n) / (faktorial(r) * faktorial(n-r))
}  

func main() {
    var a, b, c, d int
    fmt.Scan(&a, &b, &c, &d)
  
   fmt.Println(permutasi(a, c), kombinasi(a, c))
    fmt.Println(permutasi(b, d), kombinasi(b, d))
}
```

![[soal 1.png]]

Kode di atas ditulis dalam bahasa Go dan berfungsi untuk menghitung nilai permutasi dan kombinasi dari dua pasang bilangan yang dimasukkan oleh pengguna. Fungsi faktorial(n int) int menggunakan rekursi untuk menghitung faktorial suatu bilangan. Fungsi permutasi(n, r int) int menghitung permutasi dengan rumus P(n,r)=n!/(n−r)!, sedangkan fungsi kombinasi(n, r int) int menghitung kombinasi dengan rumus C(n,r)=n!r!/(n−r)!. Dalam fungsi main(), program membaca empat bilangan dari input pengguna, kemudian menghitung dan mencetak nilai permutasi dan kombinasi untuk dua pasang bilangan tersebut.

### -Soal 2
Diberikan tiga buah fungsi matematika yaitu 𝑓 (𝑥) = 𝑥 2 , 𝑔 (𝑥) = 𝑥 − 2 dan ℎ (𝑥) = 𝑥 + 1. Fungsi komposisi (𝑓𝑜𝑔𝑜ℎ)(𝑥) artinya adalah 𝑓(𝑔(ℎ(𝑥))). Tuliskan 𝑓(𝑥), 𝑔(𝑥) dan ℎ(𝑥) dalam bentuk function. Masukan terdiri dari sebuah bilangan bulat 𝑎, 𝑏 dan 𝑐 yang dipisahkan oleh spasi. Keluaran terdiri dari tiga baris. Baris pertama adalah (𝑓𝑜𝑔𝑜ℎ)(𝑎), baris kedua (𝑔𝑜ℎ𝑜𝑓)(𝑏), dan baris ketiga adalah (ℎ𝑜𝑓𝑜𝑔)(𝑐)!

```go
package main
  
import "fmt"
  
func f(x int) int {
    return x * x
}
  
func g(x int) int {
    return x - 2
}
  
func h(x int) int {
    return x + 1
}

func main() {
    var a, b, c int
    fmt.Scan(&a, &b, &c)
  
    fogoh := f(g(h(a)))
    gohof := g(h(f(b)))
    hofog := h(f(g(c)))
  
    fmt.Println(fogoh)
    fmt.Println(gohof)
    fmt.Println(hofog)
}
```

![[soal 2.png]]
Kode di atas merupakan implementasi dalam bahasa Go yang menghitung komposisi tiga fungsi matematika:𝑓 (𝑥) = 𝑥 2 , 𝑔 (𝑥) = 𝑥 − 2 dan ℎ (𝑥) = 𝑥 + 1. Dalam fungsi main(), program membaca tiga bilangan bulat a, b, dan c dari input user. Kemudian, program menghitung hasil dari tiga komposisi fungsi: `(f o g o h)(a)`, yang berarti `f(g(h(a)))`; `(g o h o f)(b)`, yang berarti `g(h(f(b)))`; dan `(h o f o g)(c)`, yang berarti `h(f(g(c)))`. Hasil dari masing-masing komposisi kemudian dicetak ke layar dalam tiga baris terpisah.


### -Soal 3
Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

```go
package main
  
import "fmt"
 
func main() {
        var cx1, cy1, r1 int
        var cx2, cy2, r2 int
        var x, y int
  
        fmt.Scan(&cx1, &cy1, &r1)
        fmt.Scan(&cx2, &cy2, &r2)
        fmt.Scan(&x, &y)
  
        dalamLingkaran1 := diDalam(cx1, cy1, r1, x, y)
        dalamLingkaran2 := diDalam(cx2, cy2, r2, x, y)
  
        if dalamLingkaran1 && dalamLingkaran2 {
                fmt.Println("Titik di dalam lingkaran 1 dan 2")
        } else if dalamLingkaran1 {
                fmt.Println("Titik di dalam lingkaran 1")
        } else if dalamLingkaran2 {
                fmt.Println("Titik di dalam lingkaran 2")
        } else {
                fmt.Println("Titik di luar lingkaran 1 dan 2")
        }
}
  
func diDalam(cx, cy, r, x, y int) bool {
        dx := x - cx
        dy := y - cy
        jarakKuadrat := dx*dx + dy*dy
        jariJariKuadrat := r * r
        return jarakKuadrat <= jariJariKuadrat
}
```

![[soal 3.png]]

Kode di atas adalah program dalam bahasa Go yang menentukan posisi sebuah titik terhadap dua lingkaran. Program membaca koordinat pusat dan radius dua lingkaran, serta koordinat titik sembarang dari input pengguna. Fungsi `diDalam(cx, cy, r, x, y) bool` digunakan untuk mengecek apakah titik berada di dalam lingkaran dengan membandingkan jarak kuadrat antara titik dan pusat lingkaran dengan kuadrat radiusnya. Jika jarak kuadrat lebih kecil atau sama dengan kuadrat radius, maka titik berada di dalam lingkaran. Program kemudian mencetak salah satu dari empat kemungkinan hasil: titik berada di dalam kedua lingkaran, hanya di dalam lingkaran pertama, hanya di dalam lingkaran kedua, atau di luar kedua lingkaran.