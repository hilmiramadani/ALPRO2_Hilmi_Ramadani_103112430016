<h1 align="center">Laporan Praktikum Modul 18</h1>
___
<h5 align="center">Hilmi Hakim Ramadani - 103112430016</h5>

## Dasar Teori

Mesin abstrak dalam konteks bahasa Go (Golang) merujuk pada model konseptual yang digunakan untuk memahami cara kerja program, seperti bagaimana data diproses, dikontrol, dan disimpan. Dalam Go, mesin abstrak bisa diwujudkan melalui kombinasi struktur data, fungsi, dan alur kontrol (seperti `for`, `if`, `switch`). Mesin ini tidak nyata secara fisik, tetapi membantu menggambarkan bagaimana program bekerja layaknya mesin, termasuk bagaimana instruksi dijalankan dan bagaimana memori digunakan selama eksekusi program.

## Unguided

### -Soal 4
Implementasi mesin abstrak karakter yang bekerja terhadap untaian karakter (yang diakhiri
dengan penanda titik (".") dan mempunyai sejumlah operasi dasar.
a) Operasi dasar mesin karakter:
➢ Prosedur start(); yang menyiapkan mesin karakter di awal rangkaian karakter.
➢ Prosedur maju(); yang memajukan pembaca ke posisi karakter berikutnya.
➢ Fungsi eop(); yang mengembalikan nilai true apabila sudah mencapai akhir
rangkaian, sampai ke penanda titik (".").
➢ Fungsi cc(); yang mengembalikan karakter yang sedang terbaca, atau berada pada
posisi pembacaan mesin.
b) Dengan operasi dasar di atas buat algoritma untuk:
➢ Membaca seluruh karakter yang diberikan ke mesin karakter tersebut.
➢ Menghitung berapa banyak karakter yang terbaca.
➢ Menghitung ada berapa huruf "A" yang terbaca.
➢ Menghitung frekuensi kemunculan huruf "A" terhadap seluruh karakter terbaca.
➢ Menghitung ada berapa kata "LE" (pasangan berturutan huruf "L" dan "E") yang
terbaca.

```go
package main

import (
	"fmt"
	"strings"
)

var input string
var pos int
var currentChar byte

func start(text string) {
	input = text
	pos = 0
	if len(input) > 0 {
		currentChar = input[pos]
	}
}

func maju() {
	pos++
	if pos < len(input) {
		currentChar = input[pos]
	}
}

func eop() bool {
	return currentChar == '.'
}

func cc() byte {
	return currentChar
}

func main() {
	var teks string
	fmt.Print("Masukkan teks diakhiri titik: ")
	fmt.Scanln(&teks)

	start(teks)

	totalKarakter := 0
	jumlahA := 0
	jumlahLE := 0

	var prev byte

	for !eop() {
		ch := cc()
		totalKarakter++

		if strings.ToUpper(string(ch)) == "A" {
			jumlahA++
		}

		if strings.ToUpper(string(prev)) == "L" && strings.ToUpper(string(ch)) == "E" {
			jumlahLE++
		}

		prev = ch
		maju()
	}

	var frekuensiA float64
	if totalKarakter > 0 {
		frekuensiA = float64(jumlahA) / float64(totalKarakter)
	}

	fmt.Println("Total karakter terbaca:", totalKarakter)
	fmt.Println("Jumlah huruf 'A':", jumlahA)
	fmt.Printf("Frekuensi huruf 'A': %.2f\n", frekuensiA)
	fmt.Println("Jumlah kata 'LE':", jumlahLE)
}
```

![[MODUL 18 MESIN ABSTRAK/Output/soal4.png]]

>Program di atas merupakan implementasi **mesin abstrak karakter** dalam bahasa Go yang membaca sebuah untaian karakter hingga bertemu tanda titik (`.`) sebagai akhir. Mesin ini memiliki operasi dasar seperti `start`, `maju`, `eop`, dan `cc` untuk mengatur pembacaan karakter satu per satu. Saat dijalankan, program akan menghitung total karakter yang dibaca, jumlah huruf "A" (tidak peka huruf besar atau kecil), frekuensi kemunculan huruf "A" terhadap total karakter, dan jumlah kemunculan pasangan huruf "LE" secara berurutan. Program ini bermanfaat untuk memahami cara kerja pemrosesan teks secara manual menggunakan model mesin karakter.

