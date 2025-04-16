<h1 align="center">Laporan Praktikum Modul 10</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Pencarian nilai ekstrem pada himpunan data di Golang adalah proses untuk menemukan nilai minimum dan maksimum dari sebuah kumpulan data, seperti slice atau array. Teknik ini biasanya dilakukan dengan cara menginisialisasi nilai awal sebagai acuan, kemudian melakukan iterasi untuk membandingkan setiap elemen dalam data. Selama iterasi, nilai minimum diperbarui jika ditemukan angka yang lebih kecil, dan nilai maksimum diperbarui jika ditemukan angka yang lebih besar. Proses ini sederhana namun penting dalam analisis data, statistik, atau pengambilan keputusan berbasis nilai tertinggi dan terendah.


## Unguided

### -Soal 1
Sebuah program digunakan untuk mendata berat anak kelinci yang akan dijual ke pasar.
Program ini menggunakan array dengan kapasitas 1000 untuk menampung data berat anak
kelinci yang akan dijual.
Masukan terdiri dari sekumpulan bilangan, yang mana bilangan pertama adalah bilangan
bulat N yang menyatakan banyaknya anak kelinci yang akan ditimbang beratnya. Selanjutnya
N bilangan riil berikutnya adalah berat dari anak kelinci yang akan dijual.
Keluaran terdiri dari dua buah bilangan riil yang menyatakan berat kelinci terkecil dan
terbesar.

```go
package main

import "fmt"

func main() {
	var N int
	fmt.Print("Masukkan jumlah anak kelinci: ")
	fmt.Scan(&N)

	var berat [1000]float64
	fmt.Println("Masukkan berat anak kelinci:")
	for i := 0; i < N; i++ {
		fmt.Scan(&berat[i])
	}

	min := berat[0]
	max := berat[0]

	for i := 1; i < N; i++ {
		if berat[i] < min {
			min = berat[i]
		}
		if berat[i] > max {
			max = berat[i]
		}
	}

	fmt.Printf("Berat terkecil: %.2f kg\n", min)
	fmt.Printf("Berat terbesar: %.2f kg\n", max)
}
```

![[MODUL 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/Output/soal1.png]]

Program di atas ditulis dalam bahasa Go dan berfungsi untuk mencatat serta mencari berat terkecil dan terbesar dari sejumlah anak kelinci yang akan dijual. Pertama, program meminta input berupa jumlah anak kelinci (`N`), yang dibatasi maksimal 1000 sesuai kapasitas array yang disediakan. Setelah itu, program meminta pengguna memasukkan `N` buah data berupa berat masing-masing anak kelinci dalam satuan kilogram, yang disimpan dalam array bertipe `float64`. Program kemudian menginisialisasi nilai minimum dan maksimum dengan berat pertama dalam array, lalu melakukan iterasi untuk membandingkan setiap elemen dan memperbarui nilai minimum dan maksimum jika ditemukan berat yang lebih kecil atau lebih besar. Terakhir, program mencetak berat terkecil dan terbesar dengan format dua angka di belakang koma.


### -Soal 2
Sebuah program digunakan untuk menentukan tarif ikan yang akan dijual ke pasar. Program
ini menggunakan array dengan kapasitas 1000 untuk menampung data berat ikan yang akan
dijual.
Masukan terdiri dari dua baris, yang mana baris pertama terdiri dari dua bilangan bulat x dan
y. Bilangan x menyatakan banyaknya ikan yang akan dijual, sedangkan y adalah banyaknya
ikan yang akan dimasukan ke dalam wadah. Baris kedua terdiri dari sejumlah x bilangan riil
yang menyatakan banyaknya ikan yang akan dijual.
Keluaran terdiri dari dua baris. Baris pertama adalah kumpulan bilangan riil yang menyatakan
total berat ikan di setiap wadah (jumlah wadah tergantung pada nilai x dan y, urutan ikan yang
dimasukan ke dalam wadah sesuai urutan pada masukan baris ke-2). Baris kedua adalah
sebuah bilangan riil yang menyatakan berat rata-rata ikan di setiap wadah

```go
package main

import "fmt"

func main() {
	var x, y int
	fmt.Print("Masukkan jumlah ikan dan jumlah ikan per wadah: ")
	fmt.Scan(&x, &y)

	var ikan [1000]float64
	fmt.Printf("Masukkan %d berat ikan:\n", x)
	for i := 0; i < x; i++ {
		fmt.Scan(&ikan[i])
	}

	// Hitung total berat per wadah
	jumlahWadah := (x + y - 1) / y // Pembulatan ke atas
	totalBeratPerWadah := make([]float64, jumlahWadah)

	for i := 0; i < x; i++ {
		idxWadah := i / y
		totalBeratPerWadah[idxWadah] += ikan[i]
	}

	// Tampilkan total berat tiap wadah
	fmt.Println("Total berat tiap wadah:")
	var totalSemuaWadah float64
	for _, berat := range totalBeratPerWadah {
		fmt.Printf("%.2f ", berat)
		totalSemuaWadah += berat
	}
	fmt.Println()

	// Hitung dan tampilkan rata-rata berat tiap wadah
	rataRata := totalSemuaWadah / float64(jumlahWadah)
	fmt.Printf("Rata-rata berat per wadah: %.2f kg\n", rataRata)
}
```

![[MODUL 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/Output/soal2.png]]

Program ini membaca jumlah ikan x dan jumlah ikan per wadah y, lalu membaca x buah berat ikan. Data berat disimpan dalam array. Setiap y ikan dikelompokkan ke dalam satu wadah, dan total berat per wadah dihitung serta disimpan dalam slice. Akhirnya, program mencetak total berat setiap wadah dan rata-rata berat antar wadah.

### -Soal 3
Pos Pelayanan Terpadu (posyandu) sebagai tempat pelayanan kesehatan perlu mencatat data berat balita (dalam kg). Petugas akan memasukkan data tersebut ke dalam array. Dari data yang diperoleh akan dicari berat balita terkecil, terbesar, dan reratanya.

```go
package main

import "fmt"

// Tipe data array tetap untuk menampung berat balita
type arrBalita [100]float64

// Subprogram untuk menghitung nilai minimum dan maksimum dari array berat balita
func hitungMinMax(arrBerat arrBalita, n int, bMin, bMax *float64) {
	*bMin = arrBerat[0]
	*bMax = arrBerat[0]

	for i := 1; i < n; i++ {
		if arrBerat[i] < *bMin {
			*bMin = arrBerat[i]
		}
		if arrBerat[i] > *bMax {
			*bMax = arrBerat[i]
		}
	}
}

// Subprogram untuk menghitung rerata berat balita
func rerata(arrBerat arrBalita, n int) float64 {
	if n <= 0 {
		return 0
	}

	var total float64 = 0
	for i := 0; i < n; i++ {
		total += arrBerat[i]
	}
	return total / float64(n)
}

// Program utama
func main() {
	var n int
	var data arrBalita

	fmt.Print("Masukkan jumlah balita: ")
	fmt.Scan(&n)

	fmt.Println("Masukkan berat balita:")
	for i := 0; i < n; i++ {
		fmt.Printf("Berat balita ke-%d: ", i+1)
		fmt.Scan(&data[i])
	}

	var min, max float64
	hitungMinMax(data, n, &min, &max)
	rerataBerat := rerata(data, n)

	fmt.Printf("\nBerat terkecil  : %.2f kg\n", min)
	fmt.Printf("Berat terbesar  : %.2f kg\n", max)
	fmt.Printf("Rata-rata berat : %.2f kg\n", rerataBerat)
}
```

![[MODUL 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/Output/soal3.png]]

type arrBalita [100]float64 mendefinisikan tipe array untuk menampung maksimal 100 data berat balita. hitungMinMax menerima array dan pointer ke bMin dan bMax, lalu mencari nilai minimum dan maksimum. rerata menghitung rata-rata dari data berat balita dalam array. Program utama meminta jumlah data, mengisi array, memanggil subprogram, dan mencetak hasilnya.