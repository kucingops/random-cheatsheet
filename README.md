# randomcheatsheet

## SOLID Principle
SOLID adalah lima prinsip dasar dalam desain perangkat lunak berorientasi objek. Prinsip ini diperkenalkan oleh Robert C. Martin (Uncle Bob) dan bertujuan agar kode lebih mudah dipelihara, dikembangkan, serta lebih fleksibel.
### 1. S – Single Responsibility Principle (SRP)

“Satu kelas harus hanya memiliki satu alasan untuk berubah.”

Artinya:
Setiap kelas hanya boleh punya satu tanggung jawab utama.
Jika sebuah kelas menangani terlalu banyak hal, maka perubahan kecil di satu bagian bisa berdampak besar ke bagian lain.

Contoh:
❌ Salah: Kelas Invoice menangani data invoice, hitung total, dan cetak PDF.
✅ Benar: Pecah menjadi Invoice, InvoiceCalculator, dan InvoicePrinter.

### 2. O – Open/Closed Principle (OCP)

“Sebuah entitas harus terbuka untuk perluasan, tetapi tertutup untuk modifikasi.”

Artinya:
Kita bisa menambah fitur baru tanpa harus mengubah kode yang sudah ada, biasanya dengan inheritance atau interface.

Contoh:
Jika ada sistem pembayaran, jangan ubah kode lama untuk tambah metode pembayaran baru.
Cukup buat kelas baru CreditCardPayment, PaypalPayment, dll.

### 3. L – Liskov Substitution Principle (LSP)

“Objek turunan harus bisa menggantikan objek induknya tanpa mengubah kebenaran program.”

Artinya:
Jika B adalah subclass dari A, maka objek B harus bisa digunakan di mana pun A dipakai tanpa error atau perilaku aneh.

Contoh:
Jika ada class Bird dengan method fly(), maka class Penguin tidak boleh jadi subclass Bird karena penguin tidak bisa terbang.

### 4. I – Interface Segregation Principle (ISP)

“Jangan memaksa klien untuk bergantung pada interface yang tidak mereka gunakan.”

Artinya:
Lebih baik banyak interface kecil dan spesifik daripada satu interface besar yang gemuk.

Contoh:
❌ Salah: IMachine punya print(), scan(), fax().
Padahal tidak semua mesin butuh fax().
✅ Benar: Buat IPrinter, IScanner, IFax terpisah.

### 5. D – Dependency Inversion Principle (DIP)

“Bergantunglah pada abstraksi, bukan pada implementasi konkret.”

Artinya:
Kelas jangan langsung bergantung pada kelas lain yang konkret. Gunakan interface atau abstraksi supaya kode lebih fleksibel.

Contoh:
❌ Salah: OrderService langsung membuat objek MySQLRepository.
✅ Benar: OrderService bergantung pada IRepository, lalu implementasi bisa MySQLRepository, PostgresRepository, dll.

### 📌 Ringkasan

SRP → Satu kelas = satu tanggung jawab

OCP → Tambah fitur tanpa ubah kode lama

LSP → Subclass bisa ganti superclass tanpa masalah

ISP → Gunakan interface kecil yang spesifik

DIP → Gunakan abstraksi, bukan implementasi langsung

## Stack dan Heap di Java

### 📌 Konsep Dasar
Dalam Java (dan bahasa pemrograman lain yang menggunakan JVM), memori program dibagi menjadi dua area utama: **Stack** dan **Heap**.

### 🧱 Stack Memory
#### Fungsi
Stack digunakan untuk menyimpan informasi **eksekusi method**:
- Variabel lokal (misalnya `int x = 5`)
- Referensi objek (alamat objek di heap)
- Informasi pemanggilan method (call frame)

#### Karakteristik
- **Last In First Out (LIFO)** → method terakhir yang dipanggil akan selesai lebih dulu.
- Ukurannya **lebih kecil** daripada heap.
- Dialokasikan otomatis oleh JVM, sangat cepat.
- Tidak ada garbage collection di stack → ketika method selesai, frame-nya langsung hilang.

#### Contoh
```java
public void test() {
    int a = 10;       // variabel lokal → disimpan di stack
    String s = "hi";  // referensi s → stack, objek "hi" ada di heap
}
```
### 🗂 Heap Memory di Java

#### 📌 Fungsi
Heap digunakan untuk menyimpan semua **objek** yang dibuat dengan `new`, termasuk:
- Object
- Array
- String (kecuali literal, yang ada di String Pool)

Heap adalah area memori global, sehingga objek di dalamnya bisa diakses lintas method selama masih ada referensi yang menunjuk ke sana.

#### ⚙️ Karakteristik
- Dikelola oleh **Garbage Collector (GC)**.
- Ukurannya lebih besar dibandingkan Stack.
- Akses relatif lebih lambat karena lebih kompleks.
- Data di heap bertahan lebih lama → selama masih ada referensi.
- Objek yang tidak lagi direferensikan akan dianggap **sampah** dan dibersihkan oleh GC.

#### 💻 Contoh Kode
```java
public void testHeap() {
    String s1 = new String("Hello"); // objek "Hello" disimpan di heap
    String s2 = s1; // s2 mereferensikan objek yang sama di heap
}
```
Bayangkan Heap sebagai sebuah gudang besar:

Semua barang (objek) disimpan di gudang.

Di tanganmu (Stack) hanya ada kunci loker (referensi).

Jika semua kunci hilang, barang di gudang akan dianggap tak terpakai dan dibuang oleh petugas (Garbage Collector).



