<h1 align="center">Laporan Praktikum Modul 17</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>
## Dasar Teori

Skema pemrosesan sekuensial dalam bahasa Go (Golang) adalah metode eksekusi di mana instruksi dijalankan satu per satu secara berurutan, dari atas ke bawah, tanpa ada paralelisme atau concurrency. Setiap baris kode akan dieksekusi setelah baris sebelumnya selesai.

## Guided

### -Soal 1
Aldi memiliki daftar nilai ulangan matematika temannya: 75, 60, 90, 85, dan 70. Ia ingin mengurutkan nilai tersebut dari yang terkecil ke yang terbesar menggunakan metode Bubble Sort. Pertanyaan:
1. Tunjukkan proses pengurutan nilai menggunakan Bubble Sort hingga semua nilai terurut.
2. Berapa kali pertukaran (swap) terjadi dalam proses ini?

```go
package main

import "fmt"

func BubbleSort(nilai []int) []int {

    swap := 0

    for i := 0; i < len(nilai)-1; i++ {
        for j := 0; j < len(nilai)-i-1; j++ {
            if nilai[j] > nilai[j+1] {
                nilai[j], nilai[j+1] = nilai[j+1], nilai[j]
                swap++
            }
        }
    }

    fmt.Println(swap)
    return nilai
}

  

func main() {
    nilai := []int{75, 60, 90, 85, 70}
    fmt.Println(BubbleSort(nilai))
}
```

## Unguided

### -Soal 1
Diberikan sejumlah bilangan real yang diakhiri dengan marker 9999, cari rerata dari bilanganbilangan tersebut.

```go
package main

import "fmt"

func main() {
	var jumlah, total, angka int
	for {
		fmt.Scan(&angka)
		if angka == 9999 {
			break
		}
		jumlah += angka
		total++
	}
	rataRata := float64(jumlah) / float64(total)
	fmt.Printf("Rata-rata dari angka yang dimasukkan: %.2f\n", rataRata)
}
```

![[MODUL 17 SKEMA PEMROSESAN SEKUENSIAL/Output/soal1.png]]

>Program Go di atas membaca sejumlah bilangan bulat dari input pengguna hingga menemukan angka penanda `9999` sebagai akhir input. Setiap angka yang dibaca sebelum `9999` akan dijumlahkan ke variabel `jumlah`, dan `total` akan menghitung berapa banyak angka yang dimasukkan. Setelah perulangan berhenti, program menghitung rata-rata dengan membagi `jumlah` dengan `total`, lalu menampilkannya dengan format dua angka di belakang koma. Karena perhitungan rata-rata memerlukan pembagian desimal, tipe data `float64` digunakan agar hasil lebih akurat.

### -Soal 2
Diberikan string x dan n buah string. x adalah data pertama yang dibaca, n adalah data bilangan yang dibaca kedua, dan n data berikutnya adalah data string. Buat algoritma untuk menjawab pertanyaan berikut:
1. Apakah string x ada dalam kumpulan n data string tersebut?
2. Pada posisi ke berapa string x tersebut ditemukan?
3. Ada berapakah string x dalam kumpulan n data string tersebut?
4. Adakah sedikitnya dua string x dalam n data string tersebut?

```go
package main

import (
	"fmt"
)

func main() {
	var x string
	var n int

	fmt.Scan(&x, &n)

	data := make([]string, n)
	fmt.Println("Masukkan", n, "string:")

	for i := 0; i < n; i++ {
		fmt.Printf("Data ke-%d: ", i+1)
		fmt.Scan(&data[i])
	}

	ditemukan := false
	posisi := -1
	jumlah := 0

	for i, s := range data {
		if s == x {
			jumlah++
			if !ditemukan {
				posisi = i + 1
				ditemukan = true
			}
		}
	}

	//1
	if ditemukan {
		fmt.Println("String x ditemukan")
	} else {
		fmt.Println("String x tidak ditemukan")
	}

	//2
	if ditemukan {
		fmt.Printf("String x ditemukan pada posisi ke-%d\n", posisi)
	} else {
		fmt.Println("String x tidak ditemukan")
	}

	//3
	fmt.Printf("String x ditemukan sebanyak %d kali.\n", jumlah)

	//4
	if jumlah >= 2 {
		fmt.Println("Ada sedikitnya dua string x")
	} else {
		fmt.Println("tidak ada sedikitnya dua string x")
	}
}

```

![[MODUL 17 SKEMA PEMROSESAN SEKUENSIAL/Output/soal2.png]]

>Program Go ini membaca sebuah string `x` sebagai data acuan, lalu menerima `n` buah string yang disimpan dalam slice. Program kemudian memeriksa apakah `x` ada dalam kumpulan string tersebut, menentukan posisi pertama kemunculannya, menghitung jumlah total kemunculan `x`, dan mengecek apakah `x` muncul sedikitnya dua kali. Hasil dari pemeriksaan ini dijawab dalam empat poin, sesuai dengan pertanyaan yang diberikan, menggunakan logika perulangan dan kondisi sederhana.

### -Soal 3
Misal curah hujan dihitung berdasarkan banyaknya tetesan air hujan. Setiap tetesan
berukuran 0.0001 ml curah hujan. Tetesan air hujan turun secara acak dari titik (0,0) sampai
(1,1). Jika diterima input yang menyatakan banyaknya tetesan air hujan. Tentukan curah
hujan untuk keempat daerah tersebut.
Buatlah program yang menerima input berupa banyaknya tetesan air hujan. Kemudian buat
koordinat/titik (x, y) secara acak dengan menggunakan fungsi rand.Float64(). Hitung dan
tampilkan banyaknya tetesan yang jatuh pada daerah A, B, C dan D. Konversikan satu tetesan
berukuran 0.0001 milimeter.
Catatan: Lihat lampiran untuk informasi menggunakan paket math/rand untuk menggunakan
rand.Float64() yang menghasilkan bilangan riil acak [0..1]

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	var totalTetesan int
	fmt.Print("Masukkan jumlah tetesan air hujan: ")
	fmt.Scan(&totalTetesan)

	rand.Seed(time.Now().UnixNano())
	countA := 0
	countB := 0
	countC := 0
	countD := 0

	for i := 0; i < totalTetesan; i++ {
		x := rand.Float64()
		y := rand.Float64()

		if x < 0.5 && y < 0.5 {
			countA++
		} else if x >= 0.5 && y < 0.5 {
			countB++
		} else if x >= 0.5 && y >= 0.5 {
			countC++
		} else if x < 0.5 && y >= 0.5 {
			countD++
		}
	}

	const volumePerTetes = 0.0001
	curahA := float64(countA) * volumePerTetes
	curahB := float64(countB) * volumePerTetes
	curahC := float64(countC) * volumePerTetes
	curahD := float64(countD) * volumePerTetes

	fmt.Printf("Curah hujan daerah A: %.4f millimeter\n", curahA)
	fmt.Printf("Curah hujan daerah B: %.4f millimeter\n", curahB)
	fmt.Printf("Curah hujan daerah C: %.4f millimeter\n", curahC)
	fmt.Printf("Curah hujan daerah D: %.4f millimeter\n", curahD)
}
```

![[MODUL 17 SKEMA PEMROSESAN SEKUENSIAL/Output/soal3.png]]

>Program Go ini mensimulasikan curah hujan dengan menerima input jumlah tetesan air hujan, lalu secara acak menghasilkan koordinat `(x, y)` untuk setiap tetesan di area 1×1. Berdasarkan posisi koordinat tersebut, program mengelompokkan tetesan ke dalam empat daerah: A, B, C, dan D. Setiap tetesan dihitung sebagai 0.0001 mm curah hujan, kemudian dijumlahkan untuk masing-masing daerah. Hasil akhirnya menampilkan curah hujan total (dalam milimeter) yang diterima oleh setiap daerah berdasarkan jumlah tetesan yang jatuh di wilayahnya.

### -Soal 4
Berdasarkan formula Leibniz, nilai π dapat dinyatakan sebagai deret harmonik ganti sebagai berikut: 1 − 1 3 + 1 5 − 1 7 + 1 9 − ⋯ = 𝜋 4 Suku ke-i dinyatakan sebagai 𝑆𝑖 dan jumlah deret adalah 𝑆. Apabila diketahui suku pertama 𝑆1 = 1, suku kedua 𝑆2 = −1 3 . Temukan rumus untuk suku ke-𝒊 atau 𝑆𝑖 . Berdasarkan rumus tersebut, buatlah program yang menghitung 𝑆 untuk 1000000 suku pertama. Perhatikan contoh sesi interaksi program di bawah ini (teks bergaris bawah adalah input/read):
N suku pertama: 1000000
Hasil PI: 3.1415951
Setelah jalan, modifikasi program tersebut agar menyimpan nilai dua suku yang
bersebelahan, 𝑆𝑖 dan 𝑆𝑖+1. Buatlah agar program tersebut sekarang berhenti apabila selisih
dari kedua suku tersebut tidak lebih dari 0.00001.

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var N int
	print("N suku pertama:")
	fmt.Scan(&N)

	pi := 0.0
	for i := 0; i < N; i++ {
		term := 1.0 / float64(2*i+1)
		if i%2 == 0 {
			pi += term
		} else {
			pi -= term
		}
	}
	pi *= 4

	pi1 := 0.0
	pi2 := 0.0
	var i int

	for i = 0; i < N; i++ {
		term := 1.0 / float64(2*i+1)
		if i%2 == 0 {
			pi2 = pi1 + term
		} else {
			pi2 = pi1 - term
		}

		if math.Abs((pi2-pi1)*4) <= 0.00001 {
			break
		}
		pi1 = pi2
	}

	fmt.Printf("Hasil PI: %.10f\n", pi1*4)
	fmt.Printf("Hasil PI: %.10f\n", pi2*4)
	fmt.Printf("Pada i ke: %d\n", i+1)
}
```

![[MODUL 17 SKEMA PEMROSESAN SEKUENSIAL/Output/soal4.png]]
>Program Go di atas menghitung nilai pendekatan π menggunakan deret Leibniz. Pertama, program membaca input `N` sebagai jumlah suku dan menghitung π dengan menjumlahkan `N` suku pertama dari deret tersebut. Setelah itu, program melanjutkan perhitungan dan membandingkan dua nilai π berturut-turut (`pi1` dan `pi2`), lalu menghentikan iterasi jika selisih hasilnya (dikalikan 4) kurang dari atau sama dengan `0.00001`. Hasil akhir menampilkan dua nilai pendekatan π dan pada iterasi keberapa batas toleransi tersebut tercapai. Program ini berguna untuk memahami konvergensi deret terhadap nilai π.

### -Soal 5
Monti bekerja pada sebuah kedai pizza, saking ramainya kedai tersebut membuat Monti tidak ada waktu untuk bersantai. Suatu ketika saat sedang menaburkan topping pada pizza yang diletakkan pada wadah berbentuk persegi, terpikirkan oleh Monti cara menghitung berapa banyak topping yang dia butuhkan, dan cara menghitung nilai 𝝅. Ilustrasi seperti gambar yang diberikan di bawah, topping adalah lingkaran-lingkaran kecil. Ada yang tepat berada di atas pizza, dan ada yang jatuh di dalam kotak tetapi berada di luar pizza.
Apabila luas pizza yang memiliki radius r adalah 𝐿𝑢𝑎𝑠𝑃𝑖𝑧𝑧𝑎 = 𝜋𝑟 2 dan luas wadah pizza yang memiliki panjang sisi 𝑑 = 2𝑟 adalah 𝐿𝑢𝑎𝑠𝑊𝑎𝑑𝑎ℎ = 𝑑 2 = 4𝑟 2 , maka diperoleh perbandingan luas kedua bidang tersebut 𝐿𝑢𝑎𝑠𝑃𝑖𝑧𝑧𝑎 𝐿𝑢𝑎𝑠𝑊𝑎𝑑𝑎ℎ = 𝜋𝑟 2 4𝑟 2 = 𝜋 4 Persamaan lingkaran adalah (𝑥 − 𝑥𝑐) 2 + (𝑦 − 𝑦𝑐) 2 = 𝑟 2 dengan titik pusat lingkaran adalah (𝑥𝑐 , 𝑦𝑐). Suatu titik sembarang (𝑥, 𝑦) dikatakan berada di dalam lingkaran apabila memenuhi ketidaksamaan: (𝑥 − 𝑥𝑐) 2 + (𝑦 − 𝑦𝑐) 2 ≤ 𝑟 2 Pada ilustrasi topping berbentuk bulat kecil merah dan biru pada gambar adalah titik-titik (𝑥, 𝑦) acak pada sebuah wadah yang berisi pizza. Dengan jumlah yang sangat banyak dan ditaburkan merata (secara acak), maka kita bisa mengetahui berapa banyak titik/topping yang berada tepat di dalam pizza menggunakan ketidaksamaan di atas. Buatlah program yang menerima input berupa banyaknya topping yang akan ditaburkan, kemudian buat titik acak (𝑥, 𝑦) dari bilangan acak riil pada kisaran nilai 0 hingga 1 sebanyak topping yang diberikan. Hitung dan tampilkan berapa banyak topping yang jatuh tepat di atas pizza. Titik pusat pizza adalah (0.5, 0.5) dan jari-jari pizza adalah 0.5 satuan wadah.

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func inputJumlahTopping() int {
	var jumlahTopping int
	fmt.Print("Banyak topping: ")
	fmt.Scan(&jumlahTopping)
	return jumlahTopping
}

func titikDalamLingkaran(x, y, cx, cy, r float64) bool {
	dx := x - cx
	dy := y - cy
	return dx*dx+dy*dy <= r*r
}

func hitungToppingDalamLingkaran(jumlah int, cx, cy, r float64) int {
	hits := 0
	for i := 0; i < jumlah; i++ {
		px := rand.Float64()
		py := rand.Float64()
		if titikDalamLingkaran(px, py, cx, cy, r) {
			hits++
		}
	}
	return hits
}

func estimasiPi(jumlahTopping, hits int) float64 {
	return (float64(hits) / float64(jumlahTopping)) * 4.0
}

func main() {
	rand.Seed(time.Now().UnixNano())

	jumlahTopping := inputJumlahTopping()

	pusatX, pusatY := 0.5, 0.5
	jariJari := 0.5

	hits := hitungToppingDalamLingkaran(jumlahTopping, pusatX, pusatY, jariJari)

	fmt.Printf("Jumlah topping di pizza: %d\n", hits)

	piTaksiran := estimasiPi(jumlahTopping, hits)
	fmt.Printf("PI: %.10f\n", piTaksiran)
}
```

![[MODUL 17 SKEMA PEMROSESAN SEKUENSIAL/Output/soal5.png]]

>Program ini mensimulasikan pelemparan titik-titik acak ke dalam sebuah kotak satuan untuk memperkirakan nilai π (pi) menggunakan metode Monte Carlo. Titik-titik tersebut dianggap sebagai "topping" yang dijatuhkan ke atas pizza berbentuk lingkaran yang berada di tengah kotak. Program menghitung berapa banyak topping yang jatuh di dalam lingkaran, lalu menggunakan proporsinya terhadap total titik untuk memperkirakan nilai π. Semakin banyak titik yang dijatuhkan, hasil estimasi π akan semakin mendekati nilai sebenarnya.

