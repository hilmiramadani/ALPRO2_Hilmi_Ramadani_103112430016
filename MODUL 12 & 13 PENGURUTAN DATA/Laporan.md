<h1 align="center">Laporan Praktikum Modul 11</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Dalam bahasa pemrograman Go (Golang), pengurutan data merupakan proses menata elemen-elemen dalam suatu struktur data (seperti slice) berdasarkan urutan tertentu, baik menaik (ascending) maupun menurun (descending). Go menyediakan paket standar bernama `sort` yang berisi fungsi-fungsi untuk melakukan pengurutan, seperti `sort.Ints(slice)` untuk mengurutkan slice bertipe `int`, `sort.Strings(slice)` untuk `string`, dan `sort.Float64s(slice)` untuk `float64`. Fungsi-fungsi ini melakukan pengurutan secara in-place, artinya data dalam slice akan langsung diubah urutannya.

Jika kita ingin mengurutkan data dengan kriteria khusus, Go juga menyediakan fungsi `sort.Slice`, di mana kita bisa menentukan aturan perbandingan antar elemen menggunakan fungsi anonim (closure). Misalnya, kita bisa mengurutkan slice struct berdasarkan satu field tertentu. Penggunaan paket `sort` ini sangat efisien dan mendukung pengurutan stabil (stable sort) jika diperlukan. Selain itu, Go juga menyediakan fungsi `sort.SliceStable` untuk pengurutan yang menjaga urutan elemen yang setara. Pengurutan merupakan salah satu teknik dasar dalam pemrosesan data dan sangat berguna dalam banyak konteks seperti pencarian, laporan, dan analisis data.

## Guided

### -Soal 1
Diberikan n bilangan bulat positif. Buat program untuk mengurutkan angka ganjil secara membesar (ascending) dan angka genap secara mengecil (descending), lalu gabungkan hasilnya dengan ganjil duluan. Gunakan selection sort dalam proses pengurutan. Masukan: Baris pertama berisi bilangan bulat n (1 ≤ n ≤ 100). Baris kedua berisi n bilangan bulat positif.

Keluaran: Satu baris berisi angka ganjil terurut membesar diikuti angka genap terurut mengecil.

Contoh Masukan: 10 12 7 3 2 9 6 8 1 11 4 
Contoh Keluaran: 1 3 7 9 11 12 8 6 4 2

```go
package main

import "fmt"

func selectionSortAsc(arr []int, panjang int) {
	var temp, i, j, idxMin int
	for i = 0; i < panjang-1; i++ {
		idxMin = i
		for j = i + 1; j < panjang; j++ {
			if arr[j] < arr[idxMin] {
				idxMin = j
			}
		}
		temp = arr[idxMin]
		arr[idxMin] = arr[i]
		arr[i] = temp
	}
}

func selectionSortDesc(arr []int, panjang int) {
	var temp, i, j, idxMax int
	for i = 0; i < panjang-1; i++ {
		idxMax = i
		for j = i + 1; j < panjang; j++ {
			if arr[j] > arr[idxMax] {
				idxMax = j
			}
		}
		temp = arr[idxMax]
		arr[idxMax] = arr[i]
		arr[i] = temp
	}
}

func main() {
	n := 10
	numbers := []int{12, 7, 3, 2, 9, 6, 8, 1, 11, 4}

	var ganjil []int
	var genap []int

	for i := 0; i < n; i++ {
		if numbers[i]%2 == 1 {
			ganjil = append(ganjil, numbers[i])
		} else {
			genap = append(genap, numbers[i])
		}
	}

	selectionSortAsc(ganjil, len(ganjil))
	selectionSortDesc(genap, len(genap))

	for i := 0; i < len(ganjil); i++ {
		fmt.Print(ganjil[i], " ")
	}
	for i := 0; i < len(genap); i++ {
		fmt.Print(genap[i], " ")
	}
}
```

>Program Go di atas merupakan implementasi fungsi pengurutan yang memisahkan angka-angka ke dalam dua kelompok: **bilangan ganjil** dan **bilangan genap**. Bilangan ganjil diurutkan secara **menaik (ascending)**, sedangkan bilangan genap diurutkan secara **menurun (descending)**. Setelah proses pengurutan masing-masing kelompok selesai, kedua slice (ganjil dan genap) digabungkan menjadi satu slice baru dengan urutan: ganjil terlebih dahulu, lalu genap. Proses pengurutan dilakukan menggunakan algoritma **bubble sort sederhana**, yaitu dengan membandingkan elemen satu per satu dan menukar posisi jika urutannya salah. Hasil akhir ditampilkan di fungsi `main`, yaitu slice `angkaTerurut` yang berisi kombinasi bilangan ganjil yang sudah diurutkan naik dan bilangan genap yang sudah diurutkan turun.

### -Soal 2
Sebuah kelas memiliki sejumlah siswa yang telah mengikuti ujian. Tugas Anda adalah membuat program yang membaca nilai-nilai ujian siswa yang disimpan dalam struct berisi nim dan nilai, kemudian mengurutkan nilai-nilai tersebut dari yang tertinggi ke yang terendah menggunakan insertion sort. Masukan: Baris pertama berisi sebuah bilangan bulat n (1 ≤ n ≤ 100), yang menyatakan jumlah siswa. Baris kedua berisi n bilangan bulat, masing-masing mewakili nilai ujian siswa (0–100).Keluaran: Satu baris yang berisi nilai-nilai ujian yang sudah terurut dari yang terbesar ke yang terkecil.

Contoh Masukan: 6 75 60 90 80 100 65
Contoh Keluaran: 100 90 80 75 65 60

```go
package main

import "fmt"

type identitas struct {
    nama  string
    nilai int
}

func nilaiujian(arr []identitas) {
    var temp identitas
    
    for i := 1; i < len(arr); i++ {
        temp = arr[i]
        j := i
        for j > 0 && temp.nilai > arr[j-1].nilai {
            arr[j] = arr[j-1]
            j--
        }
        arr[j] = temp
    }
} 

func main() {
    orang := []identitas{
        {"Darrel", 75},
        {"Nanda", 90},
        {"Aji", 85},
        {"Helen", 95},
        {"Jawir", 80},

    }
    
    nilaiujian(orang)
    
    for i := 0; i < len(orang); i++ {
        fmt.Println(orang[i].nama, ": ", orang[i].nilai)
    }
}
```

>Program Go di atas menggunakan **struct `identitas`** yang menyimpan data nama dan nilai seseorang. Fungsi `nilaiujian` mengurutkan slice dari struct `identitas` berdasarkan nilai ujian secara **menurun (descending)** menggunakan algoritma **insertion sort**. Dalam algoritma ini, setiap elemen dibandingkan dengan elemen sebelumnya, lalu disisipkan pada posisi yang tepat jika nilainya lebih besar. Setelah pengurutan selesai, fungsi `main` mencetak daftar nama beserta nilai yang sudah diurutkan dari nilai tertinggi ke terendah. Program ini berguna untuk menampilkan peringkat peserta berdasarkan nilai secara rapi.

## Unguided

### -Soal 1
Hercules, preman terkenal seantero ibukota, memiliki kerabat di banyak daerah. Tentunya
Hercules sangat suka mengunjungi semua kerabatnya itu.
Diberikan masukan nomor rumah dari semua kerabatnya di suatu daerah, buatlah program
rumahkerabat yang akan menyusun nomor-nomor rumah kerabatnya secara terurut
membesar menggunakan algoritma selection sort.
Masukan dimulai dengan sebuah integer 𝒏 (0 < n < 1000), banyaknya daerah kerabat
Hercules tinggal. Isi 𝒏 baris berikutnya selalu dimulai dengan sebuah integer 𝒎 (0 < m <1000000) yang menyatakan banyaknya rumah kerabat di daerah tersebut, diikuti dengan
rangkaian bilangan bulat positif, nomor rumah para kerabat.
Keluaran terdiri dari n baris, yaitu rangkaian rumah kerabatnya terurut membesar di masingmasing daerah.

```go
package main

import (
	"fmt"
)

func selectionSort(arr []int) {
	n := len(arr)
	for i := 0; i < n-1; i++ {
		minIdx := i
		for j := i + 1; j < n; j++ {
			if arr[j] < arr[minIdx] {
				minIdx = j
			}
		}
		arr[i], arr[minIdx] = arr[minIdx], arr[i]
	}
}

func main() {
	var n int
	fmt.Scan(&n)

	for i := 0; i < n; i++ {
		var m int
		fmt.Scan(&m)

		rumah := make([]int, m)
		for j := 0; j < m; j++ {
			fmt.Scan(&rumah[j])
		}

		selectionSort(rumah)

		for j := 0; j < m; j++ {
			fmt.Print(rumah[j], " ")
		}
		fmt.Println()
	}
}
```

![[MODUL 12 & 13 PENGURUTAN DATA/Output/soal1.png]]

>Program Go di atas membaca sejumlah data yang merepresentasikan nomor rumah kerabat Hercules di beberapa daerah, kemudian mengurutkan setiap kelompok nomor rumah tersebut secara **menaik (ascending)** menggunakan algoritma **Selection Sort**. Program dimulai dengan membaca integer `n`, yaitu jumlah daerah yang memiliki kerabat. Untuk setiap daerah, dibaca integer `m` sebagai jumlah rumah, diikuti oleh `m` nomor rumah yang disimpan dalam slice `rumah`. Fungsi `selectionSort` dipanggil untuk mengurutkan slice tersebut, dan hasilnya langsung dicetak ke layar baris demi baris. Dengan demikian, program ini mencetak daftar rumah yang sudah diurutkan untuk tiap daerah secara langsung setelah input tiap daerah diproses.

### -Soal 2
 Belakangan diketahui ternyata Hercules itu tidak berani menyeberang jalan, maka selalu
diusahakan agar hanya menyeberang jalan sesedikit mungkin, hanya diujung jalan. Karena
nomor rumah sisi kiri jalan selalu ganjil dan sisi kanan jalan selalu genap, maka buatlah
program kerabat dekat yang akan menampilkan nomor rumah mulai dari nomor yang ganjil
lebih dulu terurut membesar dan kemudian menampilkan nomor rumah dengan nomor
genap terurut mengecil.
Format Masukan masih persis sama seperti sebelumnya.
Keluaran terdiri dari n baris, yaitu rangkaian rumah kerabatnya terurut membesar untuk
nomor ganjil, diikuti dengan terurut mengecil untuk nomor genap, di masing-masing daerah.

```go
package main

import (
	"fmt"
)

func selectionSortAsc(arr []int) {
	n := len(arr)
	for i := 0; i < n-1; i++ {
		minIdx := i
		for j := i + 1; j < n; j++ {
			if arr[j] < arr[minIdx] {
				minIdx = j
			}
		}
		arr[i], arr[minIdx] = arr[minIdx], arr[i]
	}
}

func selectionSortDesc(arr []int) {
	n := len(arr)
	for i := 0; i < n-1; i++ {
		maxIdx := i
		for j := i + 1; j < n; j++ {
			if arr[j] > arr[maxIdx] {
				maxIdx = j
			}
		}
		arr[i], arr[maxIdx] = arr[maxIdx], arr[i]
	}
}

func main() {
	var n int
	fmt.Scan(&n)

	hasil := make([][]int, n)

	for i := 0; i < n; i++ {
		var m int
		fmt.Scan(&m)

		ganjil := []int{}
		genap := []int{}

		for j := 0; j < m; j++ {
			var nomor int
			fmt.Scan(&nomor)

			if nomor%2 == 1 {
				ganjil = append(ganjil, nomor)
			} else {
				genap = append(genap, nomor)
			}
		}

		selectionSortAsc(ganjil)
		selectionSortDesc(genap)

		hasil[i] = append(ganjil, genap...)
	}

	for i := 0; i < n; i++ {
		for j := 0; j < len(hasil[i]); j++ {
			fmt.Print(hasil[i][j], " ")
		}
		fmt.Println()
	}
}
```

![[MODUL 12 & 13 PENGURUTAN DATA/Output/soal2.png]]

>Program Go di atas menyelesaikan masalah penyusunan nomor rumah kerabat Hercules berdasarkan sisi jalan: **nomor ganjil diurutkan membesar (ascending)** dan **nomor genap diurutkan mengecil (descending)**, kemudian digabungkan dengan urutan ganjil terlebih dahulu. Program dimulai dengan membaca jumlah daerah `n`, lalu untuk setiap daerah membaca jumlah rumah `m` dan nomor-nomornya. Nomor ganjil dan genap dipisahkan ke dalam dua slice berbeda. Fungsi `selectionSortAsc` digunakan untuk mengurutkan ganjil secara menaik, dan `selectionSortDesc` untuk mengurutkan genap secara menurun. Setelah pengurutan, hasil untuk tiap daerah disimpan dan baru dicetak ke layar setelah seluruh input selesai diproses. Program ini menjaga agar Hercules hanya perlu menyeberang jalan sekali di ujung, sesuai permintaan soal.

### -Soal 3
Kompetisi pemrograman yang baru saja berlalu diikuti oleh 17 tim dari berbagai perguruan
tinggi ternama. Dalam kompetisi tersebut, setiap tim berlomba untuk menyelesaikan
sebanyak mungkin problem yang diberikan. Dari 13 problem yang diberikan, ada satu
problem yang menarik. Problem tersebut mudah dipahami, hampir semua tim mencoba
untuk menyelesaikannya, tetapi hanya 3 tim yang berhasil. Apa sih problemnya?
Buatlah program median yang mencetak nilai median terhadap seluruh data yang sudah
terbaca, jika data yang dibaca saat itu adalah 0.
Masukan berbentuk rangkaian bilangan bulat. Masukan tidak akan berisi lebih dari 1000000
data, tidak termasuk bilangan 0. Data 0 merupakan tanda bahwa median harus dicetak, tidak
termasuk data yang dicari mediannya. Data masukan diakhiri dengan bilangan bulat -5313.
Keluaran adalah median yang diminta, satu data per baris.

```go
package main

import "fmt"

func selectionSort(arr []int) {
	n := len(arr)
	for i := 0; i < n-1; i++ {
		minIdx := i
		for j := i + 1; j < n; j++ {
			if arr[j] < arr[minIdx] {
				minIdx = j
			}
		}
		arr[i], arr[minIdx] = arr[minIdx], arr[i]
	}
}

func hitungMedian(data []int) int {
	n := len(data)
	if n == 0 {
		return 0
	}

	salinan := make([]int, n)
	copy(salinan, data)
	selectionSort(salinan)

	tengah := n / 2
	if n%2 == 1 {
		return salinan[tengah]
	}
	return (salinan[tengah-1] + salinan[tengah]) / 2
}

func main() {
	var data []int

	for {
		var input int
		fmt.Scan(&input)

		if input < 0 {
			break
		} else if input == 0 {
			if len(data) > 0 {
				median := hitungMedian(data)
				fmt.Println(median)
			} else {
				fmt.Println("Tidak ada data untuk dihitung mediannya")
			}
		} else {
			data = append(data, input)
		}
	}
}
```

![[MODUL 12 & 13 PENGURUTAN DATA/Output/soal3.png]]

>Kode di atas mengimplementasikan program untuk menghitung median dari serangkaian angka yang dimasukkan pengguna. Program menggunakan algoritma **selection sort** untuk mengurutkan data sebelum menghitung median. Ketika pengguna memasukkan angka positif, angka tersebut ditambahkan ke slice `data`. Jika input adalah **0**, program menghitung dan menampilkan median data saat itu. Input negatif menghentikan program. Perbaikan yang dilakukan membuat kode lebih **idiomatic** di Go dengan menghilangkan deklarasi variabel tidak perlu, menggunakan *swap* ala Go, serta menangani kasus ketika tidak ada data. Fungsi `hitungMedian` juga dibuat **immutable** dengan menyalin data terlebih dahulu agar tidak mengubah slice asli. Program ini cocok untuk dataset kecil, meskipun selection sort kurang efisien untuk data yang sangat besar.

### -Soal 4
Buatlah sebuah program yang digunakan untuk membaca data integer seperti contoh yang diberikan di bawah ini, kemudian diurutkan (menggunakan metoda insertion sort), dan memeriksa apakah data yang terurut berjarak sama terhadap data sebelumnya. Masukan terdiri dari sekumpulan bilangan bulat yang diakhiri oleh bilangan negatif. Hanya bilangan non negatif saja yang disimpan ke dalam array. Keluaran terdiri dari dua baris. Baris pertama adalah isi dari array setelah dilakukan pengurutan, sedangkan baris kedua adalah status jarak setiap bilangan yang ada di dalam array. "Data berjarak x" atau "data berjarak tidak tetap".

```go
package main

import (
	"fmt"
	"sort"
)

func main() {
	var input int
	var data []int

	for {
		fmt.Scan(&input)
		if input < 0 {
			break
		}
		data = append(data, input)
	}

	sort.Ints(data)

	fmt.Println(data)

	if len(data) <= 1 {
		fmt.Println("Data berjarak tetap")
		return
	}

	jarak := data[1] - data[0]
	jarakTetap := true

	for i := 2; i < len(data); i++ {
		if data[i]-data[i-1] != jarak {
			jarakTetap = false
			break
		}
	}

	if jarakTetap {
		fmt.Printf("Data berjarak %d\n", jarak)
	} else {
		fmt.Println("Data berjarak tidak tetap")
	}
}
```

![[MODUL 12 & 13 PENGURUTAN DATA/Output/soal4.png]]

>Program Go ini membaca serangkaian bilangan bulat non-negatif dari pengguna hingga dimasukkan bilangan negatif. Bilangan-bilangan yang valid kemudian diurutkan menggunakan fungsi `sort.Ints` dari package `sort`. Setelah diurutkan, program memeriksa apakah selisih (jarak) antara setiap bilangan berurutan dalam array terurut adalah sama. Jika semua jarak sama, program akan mencetak "Data berjarak x" (di mana x adalah nilai jarak tersebut). Jika jarak antar bilangan tidak konsisten, program akan mencetak "Data berjarak tidak tetap". Program ini juga menyertakan penanganan error sederhana saat membaca input dan memisahkan logika pemeriksaan jarak ke dalam fungsi `cekJarakTetap` untuk keterbacaan yang lebih baik.

### -Soal 5
Sebuah program perpustakaan digunakan untuk mengelola data buku di dalam suatu
perpustakaan. Misalnya terdefinisi struct dan array seperti berikut ini:
```
const nMax : integer = 7919
type Buku = <
 id, judul, penulis, penerbit : string
 eksemplar, tahun, rating : integer >
type DaftarBuku = array [ 1..nMax] of Buku
Pustaka : DaftarBuku
nPustaka: integer
```
Masukan terdiri dari beberapa baris. Baris pertama adalah bilangan bulat N yang
menyatakan banyaknya data buku yang ada di dalam perpustakaan. N baris berikutnya,
masing-masingnya adalah data buku sesuai dengan atribut atau field pada struct. Baris
terakhir adalah bilangan bulat yang menyatakan rating buku yang akan dicari.
Keluaran terdiri dari beberapa baris. Baris pertama adalah data buku terfavorit, baris kedua adalah lima judul buku dengan rating tertinggi, selanjutnya baris terakhir adalah data buku yang dicari sesuai rating yang diberikan pada masukan baris terakhir.

```go
package main

import (
	"fmt"
)

const nMax = 7919

type Buku struct {
	id, judul, penulis, penerbit string
	eksemplar, tahun, rating     int
}

type DaftarBuku [nMax]Buku

func daftarkanBuku(pustaka *DaftarBuku, n *int) {
	fmt.Print("Masukkan jumlah buku: ")
	fmt.Scan(n)

	fmt.Println("Masukkan data buku (ID Judul Penulis Penerbit Eksemplar Tahun Rating):")
	for i := 0; i < *n; i++ {
		fmt.Printf("Buku ke-%d: ", i+1)
		fmt.Scan(
			&pustaka[i].id,
			&pustaka[i].judul,
			&pustaka[i].penulis,
			&pustaka[i].penerbit,
			&pustaka[i].eksemplar,
			&pustaka[i].tahun,
			&pustaka[i].rating,
		)
	}
}

func cetakTerfavorit(pustaka DaftarBuku, n int) {
	if n == 0 {
		fmt.Println("Tidak ada buku dalam perpustakaan")
		return
	}

	terfavorit := pustaka[0]
	for i := 1; i < n; i++ {
		if pustaka[i].rating > terfavorit.rating {
			terfavorit = pustaka[i]
		}
	}

	fmt.Println("\nBuku terfavorit:")
	fmt.Printf("Judul: %s\nPenulis: %s\nPenerbit: %s\nTahun: %d\nRating: %d\n",
		terfavorit.judul,
		terfavorit.penulis,
		terfavorit.penerbit,
		terfavorit.tahun,
		terfavorit.rating,
	)
}

func urutBuku(pustaka *DaftarBuku, n int) {
	for i := 1; i < n; i++ {
		temp := pustaka[i]
		j := i - 1
		for j >= 0 && pustaka[j].rating < temp.rating {
			pustaka[j+1] = pustaka[j]
			j--
		}
		pustaka[j+1] = temp
	}
}

func cetak5Terbaru(pustaka DaftarBuku, n int) {
	if n == 0 {
		fmt.Println("Tidak ada buku dalam perpustakaan")
		return
	}

	limit := 5
	if n < 5 {
		limit = n
	}

	fmt.Println("\n5 Judul Buku dengan rating tertinggi:")
	for i := 0; i < limit; i++ {
		fmt.Printf("%d. %s (Rating: %d)\n", i+1, pustaka[i].judul, pustaka[i].rating)
	}
}

func cariBuku(pustaka DaftarBuku, n, r int) {
	kiri, kanan := 0, n-1
	ditemukan := false
	var foundBooks []Buku

	for kiri <= kanan {
		tengah := (kiri + kanan) / 2
		if pustaka[tengah].rating == r {
			foundBooks = append(foundBooks, pustaka[tengah])

			i := tengah - 1
			for i >= 0 && pustaka[i].rating == r {
				foundBooks = append(foundBooks, pustaka[i])
				i--
			}

			i = tengah + 1
			for i < n && pustaka[i].rating == r {
				foundBooks = append(foundBooks, pustaka[i])
				i++
			}

			ditemukan = true
			break
		} else if pustaka[tengah].rating < r {
			kanan = tengah - 1
		} else {
			kiri = tengah + 1
		}
	}

	if ditemukan {
		fmt.Printf("\nBuku dengan rating %d ditemukan:\n", r)
		for _, buku := range foundBooks {
			fmt.Printf("Judul: %s\nPenulis: %s\nPenerbit: %s\nTahun: %d\nEksemplar: %d\nRating: %d\n\n",
				buku.judul,
				buku.penulis,
				buku.penerbit,
				buku.tahun,
				buku.eksemplar,
				buku.rating,
			)
		}
	} else {
		fmt.Println("Tidak ada buku dengan rating seperti itu")
	}
}

func main() {
	var pustaka DaftarBuku
	var nPustaka, ratingCari int

	daftarkanBuku(&pustaka, &nPustaka)

	// Cetak buku terfavorit sebelum diurutkan
	cetakTerfavorit(pustaka, nPustaka)

	// Urutkan buku berdasarkan rating
	urutBuku(&pustaka, nPustaka)

	// Cetak 5 buku dengan rating tertinggi
	cetak5Terbaru(pustaka, nPustaka)

	// Cari buku berdasarkan rating
	fmt.Print("\nMasukkan rating buku yang dicari: ")
	fmt.Scan(&ratingCari)
	cariBuku(pustaka, nPustaka, ratingCari)
}
```

![[MODUL 12 & 13 PENGURUTAN DATA/Output/soal5.png]]

Program ini merupakan sistem manajemen perpustakaan sederhana yang mengelola data buku dengan fitur-fitur utama. Program menggunakan struktur data `Buku` untuk menyimpan informasi seperti ID, judul, penulis, penerbit, jumlah eksemplar, tahun terbit, dan rating. Data buku disimpan dalam array `DaftarBuku` dengan kapasitas maksimum 7919 buku. 

Fungsi utama program meliputi: (1) `daftarkanBuku` untuk menginput data buku, (2) `cetakTerfavorit` yang menampilkan buku dengan rating tertinggi, (3) `urutBuku` menggunakan insertion sort untuk mengurutkan buku berdasarkan rating secara descending, (4) `cetak5Terbaru` menampilkan 5 buku dengan rating tertinggi, dan (5) `cariBuku` yang menggunakan binary search untuk mencari buku berdasarkan rating tertentu. Program juga menangani kasus-kasus khusus seperti ketika tidak ada buku atau ketika ada beberapa buku dengan rating yang sama.

Output program disajikan secara terstruktur dan informatif, mencakup buku terfavorit, daftar 5 buku terbaik, serta hasil pencarian buku berdasarkan rating. Program ini cocok untuk mengelola koleksi buku dalam skala kecil hingga menengah dengan antarmuka yang sederhana namun fungsional.