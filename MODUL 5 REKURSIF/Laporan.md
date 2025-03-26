<h1 align="center">Laporan Praktikum Modul 5</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Rekursif dalam bahasa Go adalah teknik pemrograman di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan masalah yang dapat dipecah menjadi sub-masalah serupa. Seperti bahasa lainnya, rekursif di Go membutuhkan dua komponen utama: *base case* yang berfungsi sebagai kondisi penghentian untuk mencegah infinite loop, dan *recursive case* di mana fungsi memanggil dirinya sendiri dengan parameter yang dimodifikasi. Misalnya, dalam menghitung faktorial, fungsi akan terus memanggil dirinya dengan nilai yang semakin kecil hingga mencapai *base case*. Namun, perlu diperhatikan bahwa Go tidak mengoptimalkan *tail recursion*, sehingga rekursi yang terlalu dalam berisiko menyebabkan *stack overflow*. Meskipun solusi rekursif seringkali lebih elegan dan mudah dibaca untuk masalah tertentu seperti traversal pohon atau pencarian biner, solusi iteratif biasanya lebih efisien dalam hal penggunaan memori dan performa di Go. Oleh karena itu, rekursif sebaiknya digunakan dengan pertimbangan yang matang, terutama untuk operasi yang membutuhkan kedalaman pemanggilan yang signifikan.


## Unguided

### -Soal 1
Deret fibonacci adalah sebuah deret dengan nilai suku ke-0 dan ke-1 adalah 0 dan 1, dan nilai suku ke-n selanjutnya adalah hasil penjumlahan dua suku sebelumnya. Secara umum dapat diformulasikan 𝑆𝑛 = 𝑆𝑛−1 + 𝑆𝑛−2 . Berikut ini adalah contoh nilai deret fibonacci hingga suku ke-10. Buatlah program yang mengimplementasikan fungsi rekursif pada deret fibonacci tersebut.

```go
package main
import "fmt"
  
func fibonacci(n int) int {
    if n == 0 {
        return 0
    } else if n == 1 {
        return 1
    } else {
        return fibonacci(n-1) + fibonacci(n-2)
    }
}
  
func main() {
    var n int = 10
    fmt.Println("Deret Fibonacci:")
    for i := 0; i <= n; i++ {
        fmt.Printf("%d ", fibonacci(i))
    }
    fmt.Println()
}
```

![[MODUL 5 REKURSIF/Output/soal1.png]]

Program ini menggunakan fungsi rekursif `fibonacci(n)` untuk menghitung nilai Fibonacci ke-n. Kemudian, dalam fungsi `main()`, program mencetak deret Fibonacci hingga suku ke-10.


### -Soal 2
Buatlah sebuah program yang digunakan untuk menampilkan pola bintang berikut ini dengan menggunakan fungsi rekursif. N adalah masukan dari user.

```go
package main
import "fmt"
  
func cetakBintang(n, i int) {
    if i > n {
        return
    }
  
    for j := 1; j <= i; j++ {
        fmt.Print("*")
    }
    fmt.Println()
  
    cetakBintang(n, i+1)
}

func main() {
    var n int
    fmt.Scan(&n)
  
    cetakBintang(n, 1)
}
```

![[MODUL 5 REKURSIF/Output/soal2.png]]

Kode ini menggunakan rekursi untuk mencetak pola bintang sesuai dengan jumlah baris yang dimasukkan oleh user. Setiap baris memiliki jumlah bintang yang meningkat secara bertahap.


### -Soal 3
Buatlah program yang mengimplementasikan rekursif untuk menampilkan faktor bilangan dari suatu N, atau bilangan yang apa saja yang habis membagi N. 
Masukan terdiri dari sebuah bilangan bulat positif N. 
Keluaran terdiri dari barisan bilangan yang menjadi faktor dari N (terurut dari 1 hingga N ya)

```go
package main
import "fmt"
  
func cetakFaktor(n, i int) {
    if i > n {
        return
    }
  
    if n%i == 0 {
        fmt.Printf("%d ", i)
    }
  
    cetakFaktor(n, i+1)
}
  
func main() {
    var n int
    fmt.Scan(&n)
  
    cetakFaktor(n, 1)
    fmt.Println()
}
```

![[MODUL 5 REKURSIF/Output/soal3.png]]

Kode ini menggunakan rekursi untuk menampilkan faktor dari suatu bilangan N. Fungsi `cetakFaktor` akan memeriksa setiap bilangan dari 1 hingga N dan mencetaknya jika merupakan faktor dari N.


### -Soal 4
Buatlah program yang mengimplementasikan rekursif untuk menampilkan barisan bilangan tertentu. 
Masukan terdiri dari sebuah bilangan bulat positif N. 
Keluaran terdiri dari barisan bilangan dari N hingga 1 dan kembali ke N.

```go
package main
import "fmt"
  
func cetakMenurun(n, i int) {
    if i < 1 {
        return
    }
    fmt.Printf("%d ", i)
    cetakMenurun(n, i-1)
}
  
func cetakMenaik(i, n int) {
    if i > n {
        return
    }
    fmt.Printf("%d ", i)
    cetakMenaik(i+1, n)
}
  
func main() {
    var n int
    fmt.Scan(&n)
  
    cetakMenurun(n, n)
    cetakMenaik(2, n)
    fmt.Println()
}
```

![[soal4.png]]

`cetakMenurun(n, i)`, yang mencetak bilangan dari N ke 1. Sedangkan, `cetakMenaik(i, n)`, yang mencetak bilangan dari 2 kembali ke N (agar angka 1 tidak tercetak dua kali). Hasilnya adalah barisan bilangan yang turun dari N ke 1, lalu naik kembali ke N.

### -Soal 5
Buatlah program yang mengimplementasikan rekursif untuk menampilkan barisan bilangan ganjil.
Masukan terdiri dari sebuah bilangan bulat positif N. 
Keluaran terdiri dari barisan bilangan ganjil dari 1 hingga N.

```go
package main
import "fmt"
  
func cetakGanjil(i, n int) {
    if i > n {
        return
    }
    fmt.Printf("%d ", i)
    cetakGanjil(i+2, n)
}
  
func main() {
    var n int
    fmt.Scan(&n)

    cetakGanjil(1, n)
    fmt.Println()
}
```

![[soal5.png]]

Kode ini menggunakan fungsi rekursif `cetakGanjil(i, n)`, yang mencetak bilangan ganjil mulai dari 1 hingga N dengan langkah 2. Jika N adalah bilangan genap, pencetakan tetap berhenti pada bilangan ganjil terbesar yang lebih kecil atau sama dengan N.

### -Soal 6
Buatlah program yang mengimplementasikan rekursif untuk mencari hasil pangkat dari dua buah bilangan. 
Masukan terdiri dari bilangan bulat x dan y. 
Keluaran terdiri dari hasil x dipangkatkan y. 
Catatan: diperbolehkan menggunakan asterik "*", tapi dilarang menggunakan import "math".

```go
package main
import "fmt"
  
func pangkat(x, y int) int {
    if y == 0 {
        return 1
    }
    return x * pangkat(x, y-1)
}
  
func main() {
    var x, y int
    fmt.Scan(&x, &y)
  
    hasil := pangkat(x, y)
    fmt.Print(hasil)
}
```

![[soal6.png]]

Kode ini menggunakan rekursi untuk menghitung x^y dengan mendekrementasi nilai y hingga mencapai nol, di mana hasil akhirnya adalah 1. Setiap langkah rekursi mengalikan x dengan hasil rekursif dari x^(y-1).