<h1 align="center">Laporan Praktikum Modul 2 <br> FUNGSI </h1>
___
<h5 align="center">Zidane Aji Noegroho - 103112430006 </h5>
### Unguided
___
### Soal 1
Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian membantu Jonas? (tidak tentunya ya :p)
Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi, dengan syarat 𝑎≥ 𝑐 dan 𝑏≥ 𝑑.
Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂 terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑.

```go
package main

import "fmt"

func faktorial(n int) int {
    result := 1
    for i := 2; i <= n; i++ {
        result *= i
    }
    return result
}

func permutasi(n, r int) int {
    if n < r {
        return 0
    }
    return faktorial(n) / faktorial(n-r)
}

func kombinasi(n, r int) int {
    if n < r {
        return 0
    }
    return permutasi(n, r) / faktorial(r)
}

func main() {
    var a, b, c, d int
    fmt.Scan(&a, &b, &c, &d)

    fmt.Println(permutasi(a, c), kombinasi(a, c))
    fmt.Println(permutasi(b, d), kombinasi(b, d))
}
```

![](soal1.png)

program yang dibuat untuk menghitung faktorial, permutasi, dan kombinasi. Fungsi faktorial(n) menghitung faktorial dari angka n menggunakan perulangan for. Fungsi permutasi(n, r) menghitung banyaknya susunan berbeda dari r elemen yang diambil dari n, menggunakan rumus n! / (n-r)!. Fungsi kombinasi(n, r) menghitung jumlah cara memilih r elemen dari n tanpa memperhatikan urutan, menggunakan rumus n! / (r! (n-r)!). 
Di dalam main(), program membaca empat bilangan yang diinputkan oleh user. Lalu, program mencetak hasil permutasi dan kombinasi dari (a, c) dan (b, d). Jika n < r, maka permutasi dan kombinasi akan menghasilkan 0 karena tidak mungkin memilih lebih banyak elemen daripada yang tersedia.

### Soal 2
Diberikan tiga buah fungsi matematika yaitu 𝑓 (𝑥) = 𝑥^2 , 𝑔 (𝑥)= 𝑥−2 dan ℎ (𝑥)= 𝑥+1. Fungsi komposisi (𝑓𝑜𝑔𝑜ℎ)(𝑥) artinya adalah 𝑓(𝑔(ℎ(𝑥))). Tuliskan 𝑓(𝑥), 𝑔(𝑥) dan ℎ(𝑥) dalam bentuk function.
Masukan terdiri dari sebuah bilangan bulat 𝑎, 𝑏 dan 𝑐 yang dipisahkan oleh spasi.
Keluaran terdiri dari tiga baris. Baris pertama adalah (𝑓𝑜𝑔𝑜ℎ)(𝑎), baris kedua (𝑔𝑜ℎ𝑜𝑓)(𝑏), dan baris ketiga adalah (ℎ𝑜𝑓𝑜𝑔)(𝑐)!

```go
package main

import "fmt"

func komposisi(a, b, c int) (int, int, int) {
    f := func(x int) int { return x * x }
    g := func(x int) int { return x - 2 }
    h := func(x int) int { return x + 1 }

    fogoh := f(g(h(a)))
    gohof := g(h(f(b)))
    hofog := h(f(g(c)))

    return fogoh, gohof, hofog
}

func main() {
    var a, b, c int
    fmt.Scan(&a, &b, &c)

    x, y, z := komposisi(a, b, c)

    fmt.Println(x)
    fmt.Println(y)
    fmt.Println(z)
}
```

![](soal2.png)

program yang dibuat untuk menghitung hasil dari komposisi tiga fungsi matematika sederhana. Ada tiga fungsi yang didefinisikan: pertama untuk mengkuadratkan angka, kedua untuk mengurangi angka dengan dua, dan ketiga untuk menambahkan angka dengan satu. Fungsi komposisi mengambil tiga angka sebagai input dan menerapkan kombinasi dari ketiga fungsi yang sebelumnya dalam urutan yang berbeda. Hasil dari setiap komposisi fungsi dihitung dan dikembalikan sebagai tiga nilai. Di dalam fungsi main, program membaca tiga angka dari user, lalu memanggil fungsi komposisi untuk menghitung hasilnya dan mengeluarkan output angka yang telah diolah.

### soal 3
Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥,𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥,𝑦) berdasarkan dua lingkaran tersebut. 
Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat.
Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

```go
package main

import (
    "fmt"
    "math"
)

func jarak(X1, Y1, X2, Y2 int) float64 {
    return math.Sqrt(math.Pow(float64(X2-X1), 2) + math.Pow(float64(Y2-Y1), 2))
}

func diDalam(x, y, radius, titikX, titikY int) bool {
    return jarak(x, y, titikX, titikY) <= float64(radius)
}

func main() {
    var x1, y1, x2, y2, r1, r2, titikX, titikY int
    fmt.Scan(&x1, &y1, &r1)
    fmt.Scan(&x2, &y2, &r2)
    fmt.Scan(&titikX, &titikY)

    lingkaran1 := diDalam(x1, y1, r1, titikX, titikY)
    lingkaran2 := diDalam(x2, y2, r2, titikX, titikY)

    if lingkaran1 && lingkaran2 {
        fmt.Println("Titik di dalam lingkaran 1 dan 2")
    } else if lingkaran1 {
        fmt.Println("Titik di dalam lingkaran 1")
    } else if lingkaran2 {
        fmt.Println("Titik di dalam lingkaran 2")
    } else {
        fmt.Println("Titik di luar lingkaran 1 dan 2")
    }
}
```

![](soal3.png)

Program ini dibuat untuk menentukan apakah suatu titik berada di dalam satu atau dua lingkaran berdasarkan koordinat dan jari-jari lingkaran yang diberikan oleh user.
Pertama, program membaca koordinat pusat dan jari-jari dua lingkaran serta koordinat titik yang akan diperiksa. Kemudian, jarak antara titik dan pusat lingkaran dihitung menggunakan rumus jarak. Jika jarak tersebut lebih kecil atau sama dengan jari-jari lingkaran, maka titik dianggap berada di dalam lingkaran.
Setelah memeriksa kedua lingkaran, program mencetak hasil yang menunjukkan apakah titik berada di dalam lingkaran pertama, kedua, keduanya, atau di luar keduanya.