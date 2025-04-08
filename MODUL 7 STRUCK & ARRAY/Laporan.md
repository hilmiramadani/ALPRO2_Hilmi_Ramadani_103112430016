<h1 align="center">Laporan Praktikum Modul 7</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>
## Dasar Teori

Dalam bahasa Go (Golang), **struct** dan **array** merupakan dua tipe data yang sering digunakan untuk mengelola dan mengorganisasi data. **Struct** atau struktur adalah tipe data buatan pengguna yang digunakan untuk mengelompokkan beberapa data dengan tipe yang berbeda ke dalam satu kesatuan. Misalnya, kita bisa membuat struct bernama `Mahasiswa` yang memiliki atribut seperti `Nama`, `Umur`, dan `Jurusan`. Struct sangat berguna untuk merepresentasikan entitas atau objek dalam program. Sementara itu, **array** adalah kumpulan elemen dengan tipe data yang sama dan memiliki jumlah elemen tetap (fixed size). Misalnya, array bertipe `int` dengan panjang 5 hanya bisa menampung lima bilangan bulat. Elemen array diakses menggunakan indeks, dimulai dari 0. Namun karena keterbatasannya dalam hal fleksibilitas ukuran, dalam praktiknya array sering digantikan dengan **slice**, yaitu struktur data yang lebih dinamis. Keduanya—struct dan array—dapat digabungkan, seperti membuat array atau slice berisi struct, untuk menyusun data dalam bentuk yang lebih kompleks dan terstruktur.

## Unguided

### -Soal 1
Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Gunakan tipe bentukan titik untuk menyimpan koordinat, dan tipe bentukan lingkaran untuk menyimpan titik pusat lingkaran dan radiusnya. Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

```go
package main

import (
    "fmt"
    "math"
)
  
type Titik struct {
    x, y int
}
  
type Lingkaran struct {
    pusat  Titik
    radius int
}
  
func hitungJarak(a, b Titik) float64 {
    return math.Sqrt(math.Pow(float64(a.x-b.x), 2) + math.Pow(float64(a.y-b.y), 2))
}
  
func dalamLingkaran(t Titik, l Lingkaran) bool {
    return hitungJarak(t, l.pusat) <= float64(l.radius)
}
  
func main() {
    var l1, l2 Lingkaran
    var t Titik
  
    fmt.Scan(&l1.pusat.x, &l1.pusat.y, &l1.radius)
    fmt.Scan(&l2.pusat.x, &l2.pusat.y, &l2.radius)
    fmt.Scan(&t.x, &t.y)
  
    dalam1 := dalamLingkaran(t, l1)
    dalam2 := dalamLingkaran(t, l2)
  
    if dalam1 && dalam2 {
        fmt.Println("Titik di dalam lingkaran 1 dan 2")
    } else if dalam1 {
        fmt.Println("Titik di dalam lingkaran 1")
    } else if dalam2 {
        fmt.Println("Titik di dalam lingkaran 2")
    } else {
        fmt.Println("Titik di luar lingkaran 1 dan 2")
    }
}
```

![[MODUL 7 STRUCK & ARRAY/Output/soal1.png]]

Program di atas ditulis dalam bahasa Go dan bertujuan untuk menentukan posisi sebuah titik terhadap dua buah lingkaran. Program menggunakan dua tipe bentukan (`struct`), yaitu `Titik` untuk menyimpan koordinat `(x, y)` dan `Lingkaran` untuk menyimpan titik pusat serta radius lingkaran. Fungsi `hitungJarak` digunakan untuk menghitung jarak Euclidean antara dua titik, sedangkan fungsi `dalamLingkaran` menentukan apakah sebuah titik berada di dalam lingkaran berdasarkan perbandingan antara jarak titik ke pusat lingkaran dan radiusnya. Pada fungsi `main`, program membaca input koordinat dan radius untuk dua lingkaran serta koordinat titik sembarang, lalu mengevaluasi posisinya dan mencetak keterangan posisi titik tersebut apakah berada di dalam salah satu, kedua, atau di luar kedua lingkaran.

### -Soal 2
Sebuah array digunakan untuk menampung sekumpulan bilangan bulat. Buatlah program yang digunakan untuk mengisi array tersebut sebanyak N elemen nilai. Asumsikan array memiliki kapasitas penyimpanan data sejumlah elemen tertentu. Program dapat menampilkan beberapa informasi berikut: 
a. Menampilkan keseluruhan isi dari array. 
b. Menampilkan elemen-elemen array dengan indeks ganjil saja.
c. Menampilkan elemen-elemen array dengan indeks genap saja (asumsi indek ke-0 adalah genap). 
d. Menampilkan elemen-elemen array dengan indeks kelipatan bilangan x. x bisa diperoleh dari masukan pengguna. 
e. Menghapus elemen array pada indeks tertentu, asumsi indeks yang hapus selalu valid. Tampilkan keseluruhan isi dari arraynya, pastikan data yang dihapus tidak tampil 
f. Menampilkan rata-rata dari bilangan yang ada di dalam array. 
g. Menampilkan standar deviasi atau simpangan baku dari bilangan yang ada di dalam array tersebut. 
h. Menampilkan frekuensi dari suatu bilangan tertentu di dalam array yang telah diisi tersebut.

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var n int
	fmt.Print("Masukkan jumlah elemen array: ")
	fmt.Scan(&n)

	arr := make([]int, n)

	fmt.Println("Masukkan elemen-elemen array:")
	for i := 0; i < n; i++ {
		fmt.Printf("Data ke-%d: ", i)
		fmt.Scan(&arr[i])
	}

	// a. Tampilkan semua isi array
	fmt.Println("\nSemua elemen array:", arr)

	// b. Indeks ganjil
	fmt.Print("Elemen dengan indeks ganjil: ")
	for i := 1; i < len(arr); i += 2 {
		fmt.Print(arr[i], " ")
	}
	fmt.Println()

	// c. Indeks genap
	fmt.Print("Elemen dengan indeks genap: ")
	for i := 0; i < len(arr); i += 2 {
		fmt.Print(arr[i], " ")
	}
	fmt.Println()

	// d. Indeks kelipatan x
	var x int
	fmt.Print("Masukkan nilai x (untuk kelipatan indeks): ")
	fmt.Scan(&x)
	fmt.Printf("Elemen dengan indeks kelipatan %d: ", x)
	for i := 0; i < len(arr); i++ {
		if i%x == 0 {
			fmt.Print(arr[i], " ")
		}
	}
	fmt.Println()

	// e. Hapus elemen pada indeks tertentu
	var indexHapus int
	fmt.Print("Masukkan indeks yang ingin dihapus: ")
	fmt.Scan(&indexHapus)

	if indexHapus >= 0 && indexHapus < len(arr) {
		arr = append(arr[:indexHapus], arr[indexHapus+1:]...)
		fmt.Println("Array setelah penghapusan:", arr)
	} else {
		fmt.Println("Indeks tidak valid.")
	}

	// f. Rata-rata
	var total int
	for _, val := range arr {
		total += val
	}
	rata := float64(total) / float64(len(arr))
	fmt.Printf("Rata-rata elemen array: %.2f\n", rata)

	// g. Simpangan baku (standar deviasi)
	var sum float64
	for _, val := range arr {
		sum += math.Pow(float64(val)-rata, 2)
	}
	stdev := math.Sqrt(sum / float64(len(arr)))
	fmt.Printf("Standar deviasi: %.2f\n", stdev)

	// h. Frekuensi bilangan tertentu
	var cari int
	fmt.Print("Masukkan bilangan yang ingin dicari frekuensinya: ")
	fmt.Scan(&cari)

	count := 0
	for _, val := range arr {
		if val == cari {
			count++
		}
	}
	fmt.Printf("Frekuensi %d dalam array: %d kali\n", cari, count)
}
```

### -Soal 3
Sebuah program digunakan untuk menyimpan dan menampilkan nama-nama klub yang memenangkan pertandingan bola pada suatu grup pertandingan. Buatlah program yang digunakan untuk merekap skor pertandingan bola 2 buah klub bola yang berlaga. Pertama-tama program meminta masukan nama-nama klub yang bertanding, kemudian program meminta masukan skor hasil pertandingan kedua klub tersebut. Yang disimpan dalam array adalah nama-nama klub yang menang saja. Proses input skor berhenti ketika skor salah satu atau kedua klub tidak valid (negatif). Di akhir program, tampilkan daftar klub yang memenangkan pertandingan.

```go
package main
import "fmt"  

func main() {
    var klubA, klubB string
    var hasilPertandingan []string
    var skorA, skorB []int
  
    // Input nama klub
    fmt.Print("Klub A: ")
    fmt.Scanln(&klubA)
    fmt.Print("Klub B: ")
    fmt.Scanln(&klubB)
  
    // Proses input skor pertandingan
    pertandingan := 1
    for {
        var a, b int
  
        fmt.Printf("Pertandingan %d:", pertandingan)
        _, err := fmt.Scan(&a)
        if err != nil || a < 0 {
            break
        }
  
        _, err = fmt.Scan(&b)
        if err != nil || b < 0 {
            break
        }
  
        skorA = append(skorA, a)
        skorB = append(skorB, b)
        pertandingan++
    }
  
    // Tentukan hasil pertandingan
    for i := 0; i < len(skorA); i++ {
        if skorA[i] > skorB[i] {
            hasilPertandingan = append(hasilPertandingan, klubA)
        } else if skorB[i] > skorA[i] {
            hasilPertandingan = append(hasilPertandingan, klubB)
        } else {
            hasilPertandingan = append(hasilPertandingan, "Draw")
        }
    }
  
    // Tampilkan semua hasil pertandingan
    for i, hasil := range hasilPertandingan {
        fmt.Printf("Hasil %d:%s\n", i+1, hasil)
    }
  
    fmt.Println("Pertandingan selesai")
}
```

![[MODUL 7 STRUCK & ARRAY/Output/soal3.png]]

Program di atas ditulis dalam bahasa Go untuk merekap hasil pertandingan antara dua klub sepak bola. Program dimulai dengan meminta input nama kedua klub, lalu dilanjutkan dengan pengisian skor tiap pertandingan secara berulang. Input skor akan dihentikan ketika pengguna memasukkan nilai negatif pada salah satu skor. Program menyimpan hasil pertandingan dalam slice berdasarkan skor yang lebih tinggi: jika klub A menang, nama klub A disimpan, jika klub B menang, nama klub B disimpan, dan jika skornya sama, disimpan sebagai "Draw". Setelah semua data dimasukkan, program mencetak hasil setiap pertandingan dan mengakhiri dengan pesan "Pertandingan selesai". Program ini sederhana namun efektif untuk mencatat hasil dari serangkaian pertandingan dua klub.

### -Soal 4
Sebuah array digunakan untuk menampung sekumpulan karakter, Anda diminta untuk membuat sebuah subprogram untuk melakukan membalikkan urutan isi array dan memeriksa apakah membentuk palindrom.

```go
package main
import "fmt"

const NMAX int = 127
type tabel [NMAX]rune
  
// Fungsi untuk mengisi array karakter
func isiArray(t *tabel, n *int) {
    var ch rune
    *n = 0
  
    for *n < NMAX {
        fmt.Scanf("%c", &ch)
        if ch == '.' {
            break
        }
        t[*n] = ch
        *n++
    }
}
  
// Fungsi untuk mencetak array karakter
func cetakArray(t tabel, n int) {
    for i := 0; i < n; i++ {
        fmt.Printf("%c", t[i])
    }
    fmt.Println()
}
  
// Fungsi untuk membalik isi array karakter
func balikanArray(t *tabel, n int) {
    for i := 0; i < n/2; i++ {
        t[i], t[n-1-i] = t[n-1-i], t[i]
    }
}
  
// Fungsi untuk memeriksa apakah array adalah palindrom
func Palindrom(t tabel, n int) bool {
    for i := 0; i < n/2; i++ {
        if t[i] != t[n-1-i] {
            return false
        }
    }
    return true
}
  
func main() {
    var tab tabel
    var m int
  
    isiArray(&tab, &m)
    balikanArray(&tab, m)
  
    fmt.Print("Teks: ")
    cetakArray(tab, m)
  
    fmt.Print("Reverse: ")
    cetakArray(tab, m)
  
    if Palindrom(tab, m) {
        fmt.Println("Palindrom", true)
    } else {
        fmt.Println("Palindrom", false)
    }
}
```

![[MODUL 7 STRUCK & ARRAY/Output/soal4.png]]

Program di atas ditulis dalam bahasa Go untuk mengolah array karakter yang dimasukkan pengguna. Pengguna diminta memasukkan karakter satu per satu hingga karakter titik (.) sebagai tanda akhir input. Program menyimpan karakter tersebut dalam array bertipe rune. Setelah input selesai, array dibalik menggunakan fungsi `balikanArray`, kemudian ditampilkan. Program juga memeriksa apakah karakter-karakter tersebut membentuk palindrom yaitu susunan karakter yang sama jika dibaca dari depan maupun belakang menggunakan fungsi `Palindrom`. Hasil akhirnya menampilkan array yang telah dibalik dan status apakah array tersebut merupakan palindrom atau tidak.