# Tutorial: Membuat Aplikasi Pengacak Dadu dengan Jetpack Compose


**Nama:** Nabilah Atika Rahma  
**NRP:** 5025221005  
**Kelas:** PPB G - Week 4

Pada tutorial ini, kita akan belajar cara membuat aplikasi pengacak dadu sederhana menggunakan Kotlin dan Jetpack Compose. Tutorial ini akan membawa Anda melalui proses lengkap untuk membuat aplikasi Android yang interaktif dan berfungsi penuh, dimulai dari pembuatan proyek hingga menjalankan aplikasi final.

## Pendahuluan

Jetpack Compose adalah toolkit UI modern untuk Android yang menyederhanakan dan mempercepat pengembangan UI. Dengan Compose, Anda dapat membangun UI dengan lebih sedikit kode, alat visual, dan API Kotlin yang intuitif. Dalam tutorial ini, kita akan memanfaatkan Compose untuk membuat aplikasi pengacak dadu yang memungkinkan pengguna untuk "melempar" dadu virtual dan melihat hasilnya di layar.

## Prasyarat

Sebelum memulai pengembangan aplikasi ini, pastikan Anda memiliki perangkat dan pengetahuan yang diperlukan. Anda akan membutuhkan Android Studio Electric Eel (2022.1.1) atau versi yang lebih baru yang sudah terinstal di komputer Anda. Selain itu, pemahaman dasar tentang bahasa pemrograman Kotlin dan konsep dasar pengembangan Android akan sangat membantu. Meskipun demikian, tutorial ini cukup detail sehingga pemula juga dapat mengikutinya.

## Langkah 1: Membuat Proyek Baru

Untuk memulai, buka Android Studio dan buat proyek baru. Klik opsi "New Project" dari layar selamat datang atau dari menu File. Dalam dialog yang muncul, pilih template "Empty Compose Activity" yang akan memberikan struktur dasar untuk aplikasi Compose. Beri nama proyek "Dice Roller" dan atur nama paket menjadi "com.example.diceroller" atau sesuai preferensi Anda. Pastikan Anda memilih Kotlin sebagai bahasa pemrograman dan pilih API minimum yang sesuai dengan target pengguna Anda. Setelah mengonfigurasi semua pengaturan, klik "Finish" untuk membuat proyek.

## Langkah 2: Memahami Struktur Proyek

Setelah proyek berhasil dibuat, Android Studio akan menampilkan struktur proyek di panel Project. Beberapa file penting yang perlu diperhatikan antara lain: `MainActivity.kt` yang berisi fungsi utama aplikasi dan titik masuk ke aplikasi Anda; folder `ui/theme/` yang berisi definisi tema untuk aplikasi termasuk warna, tipografi, dan bentuk; serta `AndroidManifest.xml` yang berisi konfigurasi penting untuk aplikasi Android. Luangkan waktu untuk memahami struktur ini karena akan membantu Anda menavigasi proyek dengan lebih efisien.

## Langkah 3: Membuat Layout untuk Aplikasi Dadu

Sekarang kita akan mulai membangun UI untuk aplikasi pengacak dadu. Buka file `MainActivity.kt` dan cari fungsi `DiceRollerApp` yang dibuat secara otomatis oleh template. Kita akan memodifikasi fungsi ini dan menambahkan fungsi baru untuk membuat layout aplikasi. Ubah kode menjadi seperti berikut:

```kotlin
@Composable
fun DiceRollerApp() {
    DiceWithButtonAndImage()
}

@Composable
fun DiceWithButtonAndImage(modifier: Modifier = Modifier) {
    Column(
        modifier = modifier
            .fillMaxSize()
            .wrapContentSize(Alignment.Center),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        var result by remember { mutableStateOf(1) }
        val imageResource = when (result) {
            1 -> R.drawable.dice_1
            2 -> R.drawable.dice_2
            3 -> R.drawable.dice_3
            4 -> R.drawable.dice_4
            5 -> R.drawable.dice_5
            else -> R.drawable.dice_6
        }

        Image(
            painter = painterResource(id = imageResource),
            contentDescription = result.toString()
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        Button(onClick = { result = (1..6).random() }) {
            Text(text = "Roll")
        }
    }
}
```

Kode di atas menciptakan layout dengan gambar dadu dan tombol "Roll" yang ditempatkan secara vertikal dan ditengahkan di layar. Kita menggunakan `Column` untuk menata elemen secara vertikal dan `Alignment.CenterHorizontally` untuk menengahkan elemen secara horizontal. Variabel `result` menyimpan nilai dadu saat ini dan diinisialisasi dengan nilai 1. Fungsi `random()` digunakan untuk menghasilkan angka acak antara 1 dan 6 ketika tombol "Roll" ditekan.

## Langkah 4: Menambahkan Gambar Dadu

Untuk menampilkan gambar dadu yang sesuai dengan hasil pelemparan, kita perlu menambahkan gambar dadu ke proyek. Buka panel Project di Android Studio dan klik kanan pada folder `res`. Pilih "New > Android Resource Directory" dan pilih "drawable" sebagai jenis resource. Klik "OK" untuk membuat direktori. Selanjutnya, unduh gambar dadu dari repositori GitHub resmi (https://github.com/google-developer-training/android-basics-kotlin-dice-roller-with-images-app/raw/main/dice_images.zip). Setelah diunduh, ekstrak file zip dan salin semua gambar dadu ke folder `res/drawable` yang baru saja Anda buat.

![image-1](/img/img.png)

## Langkah 5: Menjalankan Aplikasi

Setelah semua kode dan sumber daya ditambahkan, saatnya untuk menjalankan aplikasi dan melihat hasilnya. Klik tombol "Run" (ikon play) di toolbar Android Studio atau tekan Shift+F10. Android Studio akan meminta Anda untuk memilih perangkat atau emulator untuk menjalankan aplikasi. Pilih emulator yang sudah dikonfigurasi atau hubungkan perangkat Android fisik. Setelah aplikasi dimuat, Anda akan melihat gambar dadu dan tombol "Roll". Klik tombol tersebut untuk mengacak dadu dan melihat hasilnya berubah.

[![vid](/img/img.png)](/img/pbb-diceroller.mp4)


## Penjelasan Kode Lebih Dalam

Mari kita memahami lebih dalam tentang kode yang telah kita tulis. Fungsi `DiceWithButtonAndImage` adalah fungsi composable utama yang membuat UI aplikasi kita. Parameter `modifier` memungkinkan pemanggil fungsi untuk mengubah tata letak atau tampilan fungsi. Dalam fungsi ini, kita menggunakan `Column` sebagai container utama yang menata elemen secara vertikal.

Modifier `.fillMaxSize()` membuat kolom mengisi seluruh ruang yang tersedia, sementara `.wrapContentSize(Alignment.Center)` menyusutkan konten dan menempatkannya di tengah ruang yang tersedia. Pengaturan `horizontalAlignment = Alignment.CenterHorizontally` memastikan semua elemen dalam kolom ditengahkan secara horizontal.

Variabel `result` dideklarasikan menggunakan `mutableStateOf` dan dibungkus dalam `remember`. Ini penting dalam Compose karena memungkinkan UI untuk diperbarui secara otomatis ketika nilai `result` berubah. Ketika tombol "Roll" diklik, nilai `result` diperbarui dengan angka acak antara 1 dan 6, dan UI secara otomatis menampilkan gambar dadu yang sesuai.

Pernyataan `when` digunakan untuk memilih gambar dadu yang sesuai berdasarkan nilai `result`. Komposabel `Image` kemudian menampilkan gambar yang dipilih, dengan `contentDescription` yang diatur ke nilai dadu untuk aksesibilitas. Komposabel `Spacer` menambahkan ruang vertikal antara gambar dan tombol, sementara komposabel `Button` membuat tombol yang dapat diklik dengan teks "Roll".

## Kesimpulan

Selamat! Anda telah berhasil membuat aplikasi pengacak dadu menggunakan Jetpack Compose. Tutorial ini telah menunjukkan beberapa konsep penting dalam pengembangan Android modern, termasuk cara membuat layout dengan Compose, mengelola state untuk memperbarui UI secara reaktif, menangani interaksi pengguna melalui tombol, dan menampilkan gambar berdasarkan logika aplikasi.

Aplikasi sederhana ini dapat menjadi dasar untuk proyek yang lebih kompleks. Anda dapat memperluas fungsionalitasnya dengan menambahkan fitur seperti dadu ganda, animasi pelemparan dadu, suara, atau bahkan mengubah jenis dadu (misalnya dadu dengan 20 sisi untuk game role-playing). Dengan pemahaman dasar tentang Jetpack Compose yang Anda peroleh dari tutorial ini, Anda siap untuk mengeksplorasi lebih banyak kemampuan pengembangan Android modern.

Seluruh tutorial ini didasarkan pada codelab resmi dari Android Developer yang dapat diakses di https://developer.android.com/codelabs/basic-android-kotlin-compose-build-a-dice-roller-app untuk informasi lebih lanjut dan materi terkait.
