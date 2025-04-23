<h1 align="center">Laporan Praktikum Modul 11</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Dalam bahasa Go (Golang), pencarian nilai acak pada himpunan data biasanya dilakukan dengan memanfaatkan paket math/rand. Proses ini melibatkan pengambilan elemen secara acak dari struktur data seperti slice atau array. Pertama-tama, fungsi rand.Intn(n) digunakan untuk menghasilkan indeks acak dari 0 hingga n-1, di mana n adalah jumlah elemen dalam himpunan. Nilai pada indeks tersebut kemudian diambil sebagai hasil pencarian acak. Untuk memastikan variasi hasil pada setiap eksekusi, penting juga untuk melakukan inisialisasi sumber angka acak dengan rand.Seed(time.Now().UnixNano()) dari paket time.

## Guided

### -Soal 1

```go
package main

import (
	"fmt"
	"strings"
)

// Fungsi untuk melakukan sequential search
func cariBarang(barang []string, x string) bool {
	for _, item := range barang {
		if strings.EqualFold(item, x) {
			return true
		}
	}
	return false
}

func main() {
	data := []string{"sabun", "sampo", "odol", "tisu", "minyak"}

	var x string
	fmt.Print("Masukkan nama barang yang dicari: ")
	fmt.Scan(&x)

	if cariBarang(data, x) {
		fmt.Println("Barang ditemukan!")
	} else {
		fmt.Println("Barang tidak ditemukan.")
	}
}

```

Kode di atas merupakan program sederhana dalam bahasa Go untuk mencari sebuah barang dalam daftar menggunakan metode sequential search. Program menyimpan daftar barang dalam sebuah slice data, lalu meminta input pengguna untuk nama barang yang ingin dicari. Fungsi cariBarang melakukan pencarian dengan membandingkan setiap elemen slice menggunakan strings.EqualFold, sehingga pencarian tidak peka terhadap huruf besar atau kecil. Jika barang ditemukan, program akan menampilkan pesan "Barang ditemukan!", jika tidak, maka akan menampilkan "Barang tidak ditemukan."

### -Soal 2

```go
package main

import (
	"fmt"
)

func cariKarakter(kalimat string, huruf rune) []int {
	var posisi []int
	for i, c := range kalimat {
		if c == huruf {
			posisi = append(posisi, i)
		}
	}
	return posisi
}

func main() {
	kalimat := "algoritma pemrograman"
	huruf := 'a'

	posisi := cariKarakter(kalimat, huruf)

	fmt.Println("Kalimat:", kalimat)
	fmt.Println("Karakter yang dicari:", string(huruf))

	if len(posisi) > 0 {
		fmt.Println("Karakter ditemukan di posisi indeks:", posisi)
	} else {
		fmt.Println("Karakter tidak ditemukan di dalam kalimat.")
	}
}
```

Kode di atas adalah program Go yang mencari semua posisi kemunculan karakter tertentu dalam sebuah string. Fungsi cariKarakter menerima input berupa kalimat dan karakter (rune), lalu melakukan iterasi setiap karakter dalam kalimat. Jika karakter cocok, indeksnya ditambahkan ke slice posisi. Pada fungsi main, program mencari semua kemunculan huruf 'a' dalam kalimat "algoritma pemrograman" dan menampilkan hasilnya. Jika karakter ditemukan, program mencetak semua indeks di mana karakter tersebut muncul; jika tidak, akan menampilkan pesan bahwa karakter tidak ditemukan.

### -Soal 3

```go
package main

import (
	"fmt"
)

type Mahasiswa struct {
	Nama string
	NIM  string
}

func binarySearch(mahasiswas []Mahasiswa, targetNIM string) int {
	low := 0
	high := len(mahasiswas) - 1

	for low <= high {
		mid := (low + high) / 2
		if mahasiswas[mid].NIM == targetNIM {
			return mid
		} else if mahasiswas[mid].NIM < targetNIM {
			low = mid + 1
		} else {
			high = mid - 1
		}
	}
	return -1
}

func main() {
	mahasiswas := []Mahasiswa{
		{Nama: "Hilmi", NIM: "220001"},
		{Nama: "Siti", NIM: "220002"},
		{Nama: "Rani", NIM: "220003"},
		{Nama: "Budi", NIM: "220004"},
		{Nama: "Dina", NIM: "220005"},
	}

	var X string
	fmt.Print("Masukkan NIM yang ingin dicari: ")
	fmt.Scanln(&X)

	index := binarySearch(mahasiswas, X)

	if index != -1 {
		fmt.Printf("NIM %s ditemukan di indeks %d (Nama: %s)\n", X, index, mahasiswas[index].Nama)
	} else {
		fmt.Printf("NIM %s tidak ditemukan.\n", X)
	}
}
```

Kode di atas merupakan program Go yang menggunakan algoritma binary search untuk mencari data mahasiswa berdasarkan NIM. Struct Mahasiswa digunakan untuk menyimpan nama dan NIM. Pada fungsi binarySearch, pencarian dilakukan dengan membandingkan NIM target dengan elemen tengah slice yang sudah terurut. Jika cocok, fungsi mengembalikan indeksnya; jika tidak, pencarian dilanjutkan ke bagian kiri atau kanan sesuai urutan NIM. Di fungsi main, program meminta pengguna memasukkan NIM yang dicari, lalu menampilkan nama mahasiswa dan indeks jika ditemukan, atau pesan bahwa NIM tidak ditemukan jika tidak ada kecocokan.


## Unguided

### -Soal 1
Pada pemilihan ketua RT yang baru saja berlangsung, terdapat 20 calon ketua yang bertanding
memperebutkan suara warga. Perhitungan suara dapat segera dilakukan karena warga cukup
mengisi formulir dengan nomor dari calon ketua RT yang dipilihnya. Seperti biasa, selalu ada
pengisian yang tidak tepat atau dengan nomor pilihan di luar yang tersedia, sehingga data juga
harus divalidasi. Tugas Anda untuk membuat program mencari siapa yang memenangkan
pemilihan ketua RT.
Buatlah program pilkart yang akan membaca, memvalidasi, dan menghitung suara yang
diberikan dalam pemilihan ketua RT tersebut.
Masukan hanya satu baris data saja, berisi bilangan bulat valid yang kadang tersisipi dengan
data tidak valid. Data valid adalah integer dengan nilai di antara 1 s.d. 20 (inklusif). Data
berakhir jika ditemukan sebuah bilangan dengan nilai 0.
Keluaran dimulai dengan baris berisi jumlah data suara yang terbaca, diikuti baris yang berisi
berapa banyak suara yang valid. Kemudian sejumlah baris yang mencetak data para calon apa
saja yang mendapatkan suara.

```go
package main

import "fmt"

func main() {
	const jumlahCalon = 20
	var suara [jumlahCalon + 1]int
	var input int
	var totalSuara, suaraValid int

	for {
		fmt.Scan(&input)

		if input == 0 {
			break
		}

		totalSuara++

		if input >= 1 && input <= jumlahCalon {
			suara[input]++
			suaraValid++
		}
	}

	fmt.Println("Suara masuk:", totalSuara)
	fmt.Println("Suara sah:", suaraValid)

	for i := 1; i <= jumlahCalon; i++ {
		if suara[i] > 0 {
			fmt.Printf("%d :%d\n", i, suara[i])
		}
	}
}

```

![[unguided1.png]]

Kode di atas adalah program Go yang membaca dan menghitung suara dalam sebuah pemilihan ketua RT. Program menggunakan array suara untuk menyimpan jumlah suara setiap calon (nomor 1 hingga 20). Input dibaca satu per satu dengan fmt.Scan, dan pengisian dihentikan saat pengguna memasukkan angka 0. Setiap input yang valid (antara 1 dan 20) dihitung sebagai suara sah dan ditambahkan ke array. Setelah semua suara diproses, program menampilkan jumlah total suara masuk, jumlah suara sah, serta jumlah suara yang diterima masing-masing calon.

### -Soal 2
 Berdasarkan program sebelumnya, buat program pilkart yang mencari siapa pemenang
pemilihan ketua RT. Sekaligus juga ditentukan bahwa wakil ketua RT adalah calon yang
mendapatkan suara terbanyak kedua. Jika beberapa calon mendapatkan suara terbanyak yang sama, ketua terpilih adalah dengan nomor peserta yang paling kecil dan wakilnya dengan
nomor peserta terkecil berikutnya.
Masukan hanya satu baris data saja, berisi bilangan bulat valid yang kadang tersisipi dengan
data tidak valid. Data valid adalah bilangan bulat dengan nilai di antara 1 s.d. 20 (inklusif). Data
berakhir jika ditemukan sebuah bilangan dengan nilai 0.
Keluaran dimulai dengan baris berisi jumlah data suara yang terbaca, diikuti baris yang berisi
berapa banyak suara yang valid. Kemudian tercetak calon nomor berapa saja yang menjadi
pasangan ketua RT dan wakil ketua RT yang baru.

```go
package main

import "fmt"

func main() {
	const jumlahCalon = 20
	var suara [jumlahCalon + 1]int
	var input int
	var totalSuara, suaraValid int

	for {
		fmt.Scan(&input)

		if input == 0 {
			break
		}

		totalSuara++

		if input >= 1 && input <= jumlahCalon {
			suara[input]++
			suaraValid++
		}
	}

	ketua := 0
	wakil := 0
	for i := 1; i <= jumlahCalon; i++ {
		if suara[i] > suara[ketua] || (suara[i] == suara[ketua] && i < ketua) {
			wakil = ketua
			ketua = i
		} else if (i != ketua) && (suara[i] > suara[wakil] || (suara[i] == suara[wakil] && i < wakil)) {
			wakil = i
		}
	}

	fmt.Println("Suara masuk:", totalSuara)
	fmt.Println("Suara sah:", suaraValid)

	if suaraValid > 0 {
		fmt.Println("Ketua RT:", ketua)
		fmt.Println("Wakil ketua:", wakil)
	} else {
		fmt.Println("Tidak ada suara sah. Tidak ada ketua dan wakil terpilih.")
	}
}
```

![[unguided2.png]]

Kode tersebut merupakan program pemilihan ketua dan wakil RT yang menghitung suara dari 20 calon. Program menggunakan array suara untuk menyimpan jumlah suara setiap calon (indeks 1-20). Input dibaca dalam loop hingga pengguna memasukkan 0. Setiap suara yang valid (1-20) akan meningkatkan suaraValid dan jumlah suara calon terkait. Setelah input selesai, program mencari calon dengan suara terbanyak sebagai ketua dan calon dengan suara terbanyak kedua sebagai wakil. Jika ada hasil seri, calon dengan nomor lebih kecil diprioritaskan. Hasil akhir menampilkan total suara, suara sah, serta ketua dan wakil terpilih (jika ada suara sah). Jika tidak ada suara sah, program akan menampilkan pesan bahwa tidak ada pemenang.
### -Soal 3
Diberikan n data integer positif dalam keadaan terurut membesar dan sebuah integer lain k,
apakah bilangan k tersebut ada dalam daftar bilangan yang diberikan? Jika ya, berikan
indeksnya, jika tidak sebutkan "TIDAK ADA".
Masukan terdiri dari dua baris. Baris pertama berisi dua buah integer positif, yaitu n dan k. n
menyatakan banyaknya data, dimana 1 < n <= 1000000. k adalah bilangan yang ingin dicari.
Baris kedua berisi n buah data integer positif yang sudah terurut membesar.
Keluaran terdiri dari satu baris saja, yaitu sebuah bilangan yang menyatakan posisi data yang
dicari (k) dalam kumpulan data yang diberikan. Posisi data dihitung dimulai dari angka 0. Atau
memberikan keluaran "TIDAK ADA" jika data k tersebut tidak ditemukan dalam kumpulan.

```go
package main

import "fmt"

const NMAX = 1000000

var data [NMAX]int

func main() {
	var n, k int
	fmt.Scan(&n, &k)

	isiArray(n)

	pos := posisi(n, k)

	if pos == -1 {
		fmt.Println("TIDAK ADA")
	} else {
		fmt.Println(pos)
	}
}

func isiArray(n int) {
	for i := 0; i < n; i++ {
		fmt.Scan(&data[i])
	}
}

func posisi(n, k int) int {
	left := 0
	right := n - 1

	for left <= right {
		mid := (left + right) / 2

		if data[mid] == k {
			return mid
		} else if data[mid] < k {
			left = mid + 1
		} else {
			right = mid - 1
		}
	}

	return -1
}
```

![[unguided3.png]]

Program ini mencari bilangan k dalam array terurut menggunakan binary search. Input terdiri dari n (jumlah data) dan k (nilai yang dicari), diikuti n bilangan terurut. Program menggunakan fungsi isiArray untuk mengisi data dan posisi untuk mencari dengan binary search. Jika ditemukan, indeksnya ditampilkan; jika tidak, menampilkan "TIDAK ADA". Binary search membuat pencarian efisien (O(log n)), cocok untuk data besar hingga 1 juta elemen. Kode dirancang modular untuk memudahkan pemeliharaan.