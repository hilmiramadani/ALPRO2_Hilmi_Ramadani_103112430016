<h1 align="center">Laporan Praktikum Modul 2</h1> 

---
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>
## Dasar Teori

Golang atau **Go** adalah bahasa pemrograman open-source yang dikembangkan oleh Google pada tahun 2009. Bahasa ini dirancang untuk memiliki **kinerja tinggi**, **sintaks sederhana**, serta mendukung **pemrograman konkuren (concurrency)** dengan mudah. Struktur dasar program Golang selalu diawali dengan **package main** dan fungsi utama **func main()** sebagai entry point. Program Go juga mendukung berbagai tipe data seperti **numerik** (`int`, `float32`, `float64`), **boolean** (`bool`), **string**, serta tipe **komposit** seperti `array`, `slice`, `map`, dan `struct`. Variabel dalam Go dapat dideklarasikan menggunakan kata kunci `var`, sedangkan konstanta menggunakan `const`. Selain itu, terdapat shorthand deklarasi variabel menggunakan `:=`. Dalam hal kontrol alur, Go mendukung struktur seperti **if-else**, **for loop**, dan **switch-case** untuk pengambilan keputusan dan perulangan. Fungsi dalam Golang dideklarasikan dengan kata kunci `func` dan dapat memiliki parameter serta nilai yang dikembalikan.

## Unguided

### -Soal 2A1

Telusuri program berikut dengan cara mengkompilasi dan mengeksekusi program. Silakan masukan data yang sesuai sebanyak yang diminta program. Perhatikan keluaran yang diperoleh. Coba terangkan apa sebenarnya yang dilakukan program tersebut?

```go
package main
import "fmt"

func main() {

    var (
        satu, dua, tiga string
        temp            string
    )

    fmt.Print("Masukan input string: ")
    fmt.Scanln(&satu)
    fmt.Print("Masukan input string: ")
    fmt.Scanln(&dua)
    fmt.Print("Masukan input string: ")
    fmt.Scanln(&tiga)
    fmt.Println("Output awal = " + satu + " " + dua + " " + tiga)
    temp = satu
    satu = dua
    dua = tiga
    tiga = temp
    fmt.Println("Output akhir = " + satu + " " + dua + " " + tiga)
}
```

![[2a1.png]]

Program ini dibuat dalam bahasa Go dan berfungsi untuk menukar posisi tiga string yang dimasukkan oleh user. Program akan meminta user untuk memasukkan tiga string secara berurutan, menampilkan susunan awal string tersebut, lalu menukar posisinya sebelum menampilkan hasil akhirnya.

### -Soal 2A2

Tahun kabisat adalah tahun yang habis dibagi 400 atau habis dibagi 4 tetapi tidak habis dibagi 100. Buatlah sebuah program yang menerima input sebuah bilangan bulat dan memeriksa apakah bilangan tersebut merupakan tahun kabisat (true) atau bukan (false).

```go
package main
import "fmt"

func main() {
    var tahun int
    fmt.Print("Tahun: ")
    fmt.Scan(&tahun)

    kabisat := (tahun%400 == 0) || (tahun%4 == 0 && tahun%100 != 0)

    fmt.Println("Kabisat:", kabisat)
}
```

![[2a2.png]]

Program ini secara efisien menentukan apakah suatu tahun adalah tahun kabisat dengan menggunakan operasi modulus (`%`) dan ekspresi logika sederhana.

### -Soal 2A3

Buat program Bola yang menerima input jari-jari suatu bola (bilangan bulat). Tampilkan Volume dan Luas kulit bola. 𝑣𝑜𝑙𝑢𝑚𝑒𝑏𝑜𝑙𝑎 = 4/3 𝜋𝑟^3 dan 𝑙𝑢𝑎𝑠𝑏𝑜𝑙𝑎 = 4𝜋𝑟^2 (π ≈ 3.1415926535).

```go
package main
import "fmt"

func main() {
    var r, pi, v, l float64
    fmt.Print("Jejari = ")
    fmt.Scan(&r)
  
    pi = 3.1415926535
    v = (4.0 / 3.0) * pi * (r * r * r)
    l = 4 * pi * (r * r)

    fmt.Printf("Bola dengan jejari %.0f memiliki volume %.4f dan luas kulit %.4f\n", r, v, l)

}
```

![[2a3.png]]

Program ini menghitung dan menampilkan volume serta luas permukaan bola berdasarkan jejari yang dimasukkan user menggunakan operasi matematika sederhana.

### -Soal 2A4

Dibaca nilai temperatur dalam derajat Celsius. Nyatakan temperatur tersebut dalam Fahrenheit 𝐶𝑒𝑙𝑠𝑖𝑢𝑠 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 − 32) × 5/9 𝑅𝑒𝑎𝑚𝑢𝑟 = 𝐶𝑒𝑙𝑐𝑖𝑢𝑠 × 4/5 𝐾𝑒𝑙𝑣𝑖𝑛 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 + 459.67) × 5/9

```go
package main
import "fmt"

func main() {
    var c, r, f, k float64
    fmt.Print("Temperatur Celsius: ")
    fmt.Scan(&c)
 
    r = (4.0 / 5.0) * c
    f = (9.0/5.0)*c + 32
    k = c + 273

	fmt.Printf("Derajat Reamur: %.0f\n", r)
    fmt.Printf("Derajat Fahrenheit: %.0f\n", f)
    fmt.Printf("Derajat Kelvin: %.0f\n", k)
}
```

![[2a4.png]]

Program ini mengonversi suhu dari Celsius ke Reamur, Fahrenheit, dan Kelvin. Pengguna memasukkan suhu dalam Celsius, lalu program menghitung konversinya menggunakan rumus: R=5/4 ​C, F=9/5 C+ 32, dan K=C+273. Hasilnya ditampilkan dalam format tanpa desimal.

### -Soal 2a5

Tipe karakter sebenarnya hanya apa yang tampak dalam tampilan. Di dalamnya tersimpan dalam bentuk biner 8 bit (byte) atau 32 bit (rune) saja.Buat program ASCII yang akan membaca 5 buat data integer dan mencetaknya dalam format karakter. Kemudian membaca 3 buah data karakter dan mencetak 3 buah karakter setelah karakter tersebut (menurut tabel ASCII) 
Masukan terdiri dari dua baris. Baris pertama berisi 5 buah data integer. Data integer mempunyai nilai antara 32 s.d. 127. Baris kedua berisi 3 buah karakter yang berdampingan satu dengan yang lain (tanpa dipisahkan spasi). 
Keluaran juga terdiri dari dua baris. Baris pertama berisi 5 buah representasi karakter dari data yang diberikan, yang berdampingan satu dengan lain, tanpa dipisahkan spasi. Baris kedua berisi 3 buah karakter (juga tidak dipisahkan oleh spasi).

```go
package main
import "fmt"

func main() {
    var a, b, c, d, e int
    var huruf1, huruf2, huruf3 rune

	fmt.Scan(&a, &b, &c, &d, &e)
    fmt.Scanln()
    fmt.Scanf("%c%c%c\n", &huruf1, &huruf2, &huruf3)
    huruf1 += 1
    huruf2 += 1
    huruf3 += 1

    fmt.Printf("%c%c%c%c%c\n", a, b, c, d, e)
    fmt.Printf("%c%c%c\n", huruf1, huruf2, huruf3)
}
```

![[2a5.png]]

Program ini membaca lima bilangan bulat dan tiga karakter dari input. Lima bilangan bulat pertama dikonversi ke karakter ASCII dan dicetak secara berurutan. Selanjutnya, tiga karakter yang dibaca akan dinaikkan nilainya satu tingkat dalam tabel ASCII, lalu dicetak kembali. Penggunaan `rune` memastikan karakter dapat diubah dengan operasi aritmatika. Program ini memanfaatkan `fmt.Scan` untuk membaca bilangan bulat dan `fmt.Scanf` untuk membaca karakter tanpa spasi di antaranya.

### -Soal 2B1

Siswa kelas IPA di salah satu sekolah menengah atas di Indonesia sedang mengadakan praktikum kimia. Di setiap percobaan akan menggunakan 4 tabung reaksi, yang mana susunan warna cairan di setiap tabung akan menentukan hasil percobaan. Siswa diminta untuk mencatat hasil percobaan tersebut. Percobaan dikatakan berhasil apabila susunan warna zat cair pada gelas 1 hingga gelas 4 secara berturutan adalah ‘merah’, ‘kuning’, ‘hijau’, dan ‘ungu’ selama 5 kali percobaan berulang.
Buatlah sebuah program yang menerima input berupa warna dari ke 4 gelas reaksi sebanyak 5 kali percobaan. Kemudian program akan menampilkan true apabila urutan warna sesuai dengan informasi yang diberikan pada paragraf sebelumnya, dan false untuk urutan warna lainnya.

```go
package main
import "fmt"

func main() {
    var warna1, warna2, warna3, warna4 string
    berhasil := true

    for i := 1; i <= 5; i++ {
        fmt.Scan(&warna1, &warna2, &warna3, &warna4)
        if warna1 != "merah" || warna2 != "kuning" || warna3 != "hijau" || warna4 != "ungu" {
            berhasil = false
        }
    }
    fmt.Println(berhasil)
}
```

![[2b1.png]]

Program ini membaca input warna dari empat tabung reaksi sebanyak lima kali percobaan. Setiap percobaan memeriksa apakah urutan warna yang dimasukkan adalah "merah", "kuning", "hijau", dan "ungu". Jika ada satu percobaan yang tidak sesuai, variabel `berhasil` diubah menjadi `false`. Setelah semua percobaan selesai, program mencetak `true` jika seluruh percobaan berhasil, atau `false` jika ada yang tidak sesuai.

### -Soal 2B2

Suatu pita (string) berisi kumpulan nama-nama bunga yang dipisahkan oleh spasi dan ‘– ‘, contoh pita diilustrasikan seperti berikut ini. Pita: mawar – melati – tulip – teratai – kamboja – anggrek Buatlah sebuah program yang menerima input sebuah bilangan bulat positif (dan tidak nol) N, kemudian program akan meminta input berupa nama bunga secara berulang sebanyak N kali dan nama tersebut disimpan ke dalam pita.

```go
package main
import ("fmt")

func main() {
    var n int
    var bunga, pita string
    jumlah := 0

    fmt.Print("N: ")
    fmt.Scan(&n)
    for i := 1; i <= n; i++ {
        fmt.Printf("Bunga %d: ", i)
        fmt.Scan(&bunga)
 
        if bunga == "SELESAI" {
            break
        }

        if jumlah > 0 {
            pita += " - "
        }

        pita += bunga
        jumlah++
    }

    fmt.Println("Pita:", pita)
    fmt.Println("Bunga:", jumlah)
}
```

![[2b2.png]]

Program ini meminta input sebuah bilangan `N` yang menentukan jumlah nama bunga yang akan dimasukkan. Kemudian, program membaca nama bunga satu per satu dan menggabungkannya dalam variabel `pita`, dipisahkan dengan " - ". Jika pengguna mengetik "SELESAI", proses input dihentikan lebih awal. Setelah selesai, program mencetak pita berisi daftar bunga yang telah dimasukkan serta jumlah bunga yang tercatat.

### -Soal 2b3

Setiap hari Pak Andi membawa banyak barang belanjaan dari pasar dengan mengendarai sepeda motor. Barang belanjaan tersebut dibawa dalam kantong terpal di kiri-kanan motor. Sepeda motor tidak akan oleng jika selisih berat barang di kedua kantong sisi tidak lebih dari 9 kg. Buatlah program Pak Andi yang menerima input dua buah bilangan real positif yang menyatakan berat total masing-masing isi kantong terpal. Program akan terus meminta input bilangan tersebut hingga salah satu kantong terpal berisi 9 kg atau lebih.

```go
package main
import "fmt"

func hitungSelisih(kantong1, kantong2 float32) float32 {
    if kantong1 > kantong2 {
        return kantong1 - kantong2
    }
    return kantong2 - kantong1
}

func cekOleng(selisih float32) bool {
    return selisih >= 9
}

func main() {
    var kantong1, kantong2 float32
    for {
        fmt.Print("Masukan berat belanjaan di kedua kantong: ")
        fmt.Scan(&kantong1, &kantong2)

        if kantong1 < 0 || kantong2 < 0 || kantong1+kantong2 > 150 {
            fmt.Println("Proses selesai")
            break
        }
        selisih := hitungSelisih(kantong1, kantong2)
        oleng := cekOleng(selisih)

        fmt.Println("Sepeda motor pak Andi akan oleng:", oleng)
    }
}
```

![[2b3.png]]

Program ini digunakan untuk menentukan apakah sepeda motor Pak Andi akan oleng berdasarkan perbedaan berat belanjaan di dua kantong. Program meminta input dua nilai berat belanjaan secara berulang. Jika salah satu berat negatif atau total berat melebihi 150, program akan berhenti. Fungsi `hitungSelisih` digunakan untuk menghitung selisih berat antara dua kantong, sementara fungsi `cekOleng` menentukan apakah selisih tersebut mencapai 9 atau lebih, yang berarti motor akan oleng. Program kemudian mencetak hasil apakah motor akan oleng atau tidak berdasarkan perhitungan tersebut.

### -Soal 2B4.a

Diberikan sebuah persamaan sebagai berikut ini. 𝑓(𝑘) = ((4𝑘 + 2)^2)/((4𝑘 + 1)(4𝑘 + 3)) Buatlah sebuah program yang menerima input sebuah bilangan sebagai K, kemudian menghitung dan menampilkan nilai f(K) sesuai persamaan di atas.

```go
package main
import "fmt"

func rumusPersamaan(K float64) float64 {
    return ((4*K + 2) * (4*K + 2)) / ((4*K + 1) * (4*K + 3))
}

func rumusAkar(K float64) float64 {
    jumlah := 1.0
    for i := 0.0; i < K; i++ {
        jumlah *= ((4*i + 2) * (4*i + 2)) / ((4*i + 1) * (4*i + 3))
    }
    return jumlah
}

func main() {
    var n float64
    fmt.Print("Nilai K = ")
    fmt.Scan(&n)
  
    nPers := rumusPersamaan(n)
    nAkar := rumusAkar(n)
 
    fmt.Printf("Nilai f(K) = %.10f\n", nPers)
    fmt.Printf("Nilai akar 2 = %.10f\n", nAkar)
}
```

![[2b4.a.b.png]]

Kode di atas adalah program dalam bahasa Go yang menghitung nilai suatu persamaan menggunakan Fungsi `rumusPersamaan(K float64)` menghitung nilai berdasarkan rumus matematika ((4K+2)2)/((4K+1)(4K+3))
### -Soal 2B4.b

√2 merupakan bilangan irasional. Meskipun demikian, nilai tersebut dapat dihampiri dengan rumus berikut: √2 = ∏ (4𝑘 + 2)^2/(4𝑘 + 1)(4𝑘 + 3) ∞ 𝑘=0 Modifikasi program sebelumnya yang menerima input integer 𝐾 dan menghitung √2 untuk 𝐾 tersebut. Hampiran √2 dituliskan dalam ketelitian 10 angka di belakang koma.

```go
package main
import "fmt"

func rumusPersamaan(K float64) float64 {
    return ((4*K + 2) * (4*K + 2)) / ((4*K + 1) * (4*K + 3))
}

func rumusAkar(K float64) float64 {
    jumlah := 1.0
    for i := 0.0; i < K; i++ {
        jumlah *= ((4*i + 2) * (4*i + 2)) / ((4*i + 1) * (4*i + 3))
    }
    return jumlah
}

func main() {
    var n float64
    fmt.Print("Nilai K = ")
    fmt.Scan(&n)
  
    nPers := rumusPersamaan(n)
    nAkar := rumusAkar(n)
 
    fmt.Printf("Nilai f(K) = %.10f\n", nPers)
    fmt.Printf("Nilai akar 2 = %.10f\n", nAkar)
}
```

![[2b4.a.b.png]]

Kode di atas adalah program dalam bahasa Go yang menghitung perkalian berulang untuk mendekati akar 2. fungsi `rumusAkar(K float64)` menggunakan perulangan untuk mengalikan hasil perhitungan serupa dari K=0 hingga nilai yang diberikan oleh pengguna, mendekati nilai akar 2.

### -Soal 2C1

PT POS membutuhkan aplikasi perhitungan biaya kirim berdasarkan berat parsel. Maka, buatlah program BiayaPos untuk menghitung biaya pengiriman tersebut dengan ketentuan sebagai berikut! Dari berat parsel (dalam gram), harus dihitung total berat dalam kg dan sisanya (dalam gram). Biaya jasa pengiriman adalah Rp. 10.000,- per kg. Jika sisa berat tidak kurang dari 500 gram, maka tambahan biaya kirim hanya Rp. 5,- per gram saja. Tetapi jika kurang dari 500 gram, maka tambahan biaya akan dibebankan sebesar Rp. 15,- per gram. Sisa berat (yang kurang dari 1kg) digratiskan biayanya apabila total berat ternyata lebih dari 10kg.

```go
package main
import "fmt"

func main() {
    var berat int
    fmt.Print("Berat parsel (gram): ")
    fmt.Scan(&berat)
  
    kg := berat / 1000
    gram := berat % 1000
    biayaKg := kg * 10000
    biayaGram := 0
  
    if gram > 0 {
        if gram >= 500 {
            biayaGram = gram * 5
        } else {
            biayaGram = gram * 15
        }
    }
  
    if kg >= 10 {
        biayaGram = 0
    }

    total := biayaKg + biayaGram
  
    fmt.Printf("Detail berat: %d kg + %d gr\n", kg, gram)
    fmt.Printf("Detail biaya: Rp. %d + Rp. %d\n", biayaKg, biayaGram)
    fmt.Printf("Total biaya: Rp. %d\n", total)

}
```

![[2c1.png]]

Program ini menghitung biaya pengiriman parsel berdasarkan berat dalam gram. Pertama, berat dikonversi menjadi **kilogram (kg)** dan **sisa gram**. Biaya dihitung dengan tarif **Rp. 10.000 per kg**. Untuk sisa gram, jika **≥ 500**, dikenakan **Rp. 5 per gram**, sedangkan jika **< 500**, dikenakan **Rp. 15 per gram**. Namun, jika berat mencapai **10 kg atau lebih**, biaya untuk sisa gram dihapus (gratis). Akhirnya, program menampilkan detail berat, rincian biaya, dan total biaya pengiriman.

### -Soal 2C2

```go
package main
import “fmt”

func main() {
 var nam float64
 var nmk string
 
 fmt.Print(“Nilai akhir mata kuliah: “)
 fmt.Scanln(&nam)
 
 if nam > 80 {
 nam = “A”
 }
 if nam > 72.5 {
 nam = “AB”
 }
 if nam > 65 {
 nam = “B”
 }
 if nam > 57.5 {
 nam = “BC”
 }
 if nam > 50 {
 nam = “C”
 }
 if nam > 40 {
 nam = “D”
 } else if nam <= 40 {
 nam = “E”
 }

 fmt.Println(“Nilai mata kuliah: “, nmk)
}
```

#### a. Jika nam diberikan adalah 80.1, apa keluaran dari program tersebut? Apakah eksekusi program tersebut sesuai spesifikasi soal?

outputnya adalah A karena 80.1 > 80 sehingga memenuhi spesifikasi soal

#### b. Apa saja kesalahan dari program tersebut? Mengapa demikian? Jelaskan alur program seharusnya!

1. Pada `import “fmt”`, tanda kutip (`“”`) harus diganti dengan tanda kutip standar (`""`).
2. `nam` dideklarasikan sebagai `float64`, tetapi dalam kondisi `if`, program mencoba menyimpan nilai string (`"A"`, `"AB"`, dll.), yang akan menyebabkan error tipe data.
3. Urutan `if` tidak menggunakan `else if`, sehingga nilai yang lebih besar akan selalu masuk ke semua kondisi yang memenuhi.
4. Nilai `nmk` tidak diubah sama sekali dalam program.
5. `fmt.Println(“Nilai mata kuliah: “, nmk)` akan mencetak string kosong karena `nmk` tidak diisi dengan nilai.

#### c. Perbaiki program tersebut! Ujilah dengan masukan: 93.5; 70.6; dan 49.5. Seharusnya keluaran yang diperoleh adalah ‘A’, ‘B’, dan ‘D’.

```go
package main
import "fmt"

func main() {
	var nam float64
	var nmk string

	fmt.Print("Nilai akhir mata kuliah: ")
	fmt.Scanln(&nam)

	if nam > 80 {
		nmk = "A"
	} else if nam > 72.5 {
		nmk = "AB"
	} else if nam > 65 {
		nmk = "B"
	} else if nam > 57.5 {
		nmk = "BC"
	} else if nam > 50 {
		nmk = "C"
	} else if nam > 40 {
		nmk = "D"
	} else {
		nmk = "E"
	}

	fmt.Println("Nilai mata kuliah:", nmk)
}
```

![[2c2.png]]

### -Soal 2C3

Sebuah bilangan bulat b memiliki faktor bilangan f > 0 jika f habis membagi b. Contoh: 2 merupakan faktor dari bilangan 6 karena 6 habis dibagi 2. Buatlah program yang menerima input sebuah bilangan bulat b dan b > 1. Program harus dapat mencari dan menampilkan semua faktor dari bilangan tersebut!
Bilangan bulat b > 0 merupakan bilangan prima p jika dan hanya jika memiliki persis dua faktor bilangan saja, yaitu 1 dan dirinya sendiri. Lanjutkan program sebelumnya. Setelah menerima masukan sebuah bilangan bulat b > 0. Program tersebut mencari dan menampilkan semua faktor bilangan tersebut. Kemudian, program menentukan apakah b merupakan bilangan prima.

```go
package main
import ("fmt")

func main() {
    var b int
    fmt.Print("Bilangan: ")
    fmt.Scan(&b)
    fmt.Print("Faktor: ")

    for i := 1; i <= b; i++ {
        if b%i == 0 {
            fmt.Print(i, " ")
        }
    }
    fmt.Println()

    prima := true
    if b < 2 {
        prima = false
    } else {
        for i := 2; i*i <= b; i++ {
            if b%i == 0 {
                prima = false
                break
            }
        }
    }
  
    fmt.Println("Prima:", prima)
}
```

![[2c3.png]]

Kode di atas adalah program dalam bahasa Go yang berfungsi untuk menerima input sebuah bilangan bulat **b**, kemudian mencari dan menampilkan semua faktor dari bilangan tersebut, serta menentukan apakah bilangan tersebut merupakan bilangan prima. Program diawali dengan meminta pengguna memasukkan bilangan bulat **b** melalui fungsi `fmt.Scan(&b)`. Selanjutnya, program mencari faktor-faktor bilangan dengan melakukan iterasi dari **1 hingga b**, dan mencetak angka yang dapat membagi **b** tanpa sisa.

Setelah daftar faktor ditemukan, program kemudian menentukan apakah bilangan tersebut adalah bilangan prima. Sebuah bilangan dikatakan **prima** jika dan hanya jika memiliki tepat **dua faktor**, yaitu **1 dan dirinya sendiri**. Jika bilangan kurang dari **2**, maka langsung dikategorikan sebagai **bukan bilangan prima**. Jika bilangan **≥ 2**, program melakukan pengecekan dengan iterasi dari **2 hingga akar b**. Jika dalam rentang tersebut ditemukan bilangan yang dapat membagi **b** tanpa sisa, maka bilangan tersebut bukan prima, dan iterasi dihentikan lebih awal untuk efisiensi.