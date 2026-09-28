<<<<<<< HEAD
# Mini Project 2 PBO - Sistem Manajemen Stok Bahan Baku Coffee Shop

**Nama**  : Ananta Hanif Fidzya Pratama  
**NIM**   : 2509116023  
**Kelas** : Sistem Informasi A 2025

---

## Latar Belakang

Pengelolaan stok bahan baku pada usaha *coffee shop*, seperti biji kopi, susu, dan sirup, memerlukan pencatatan yang teliti agar ketersediaan bahan baku tetap terjaga dan operasi harian berjalan lancar. Pencatatan stok secara manual rentan terhadap kesalahan input, kerancuan data, hingga hilangnya riwayat bahan. Oleh karena itu, dibuat program sederhana berbasis Java untuk membantu mencatat, memperbarui, dan memantau stok bahan baku *coffee shop* sebagai pengembangan dari Mini Project 1 dengan menerapkan prinsip-prinsip Pemrograman Berorientasi Objek (PBO).

---

## Deskripsi Program

Program ini merupakan aplikasi berbasis konsol (*Command Line Interface* / CLI) yang digunakan untuk mengelola data stok bahan baku *coffee shop*. Data yang dikelola meliputi ID bahan, nama bahan, jumlah stok, serta atribut khusus sesuai jenis bahan baku, yaitu **jenis kemasan** untuk Bahan Padat dan **kemasan cair** untuk Bahan Cair.

Program menyediakan lima fitur utama:
1. **Tampilkan Semua Bahan** - Menampilkan seluruh data bahan baku yang tersimpan.
2. **Tambah Bahan Baru** - Menambahkan data bahan baku padat atau cair baru.
3. **Update Stok Bahan** - Memperbarui jumlah stok bahan berdasarkan ID.
4. **Hapus Bahan** - Menghapus data bahan baku dari sistem berdasarkan ID.
5. **Cari Bahan** - Mencari data bahan baku berdasarkan ID atau Nama (demo *Method Overloading*).

---

## MVC yang Digunakan

Program ini menerapkan arsitektur **MVC (Model-View-Controller)** untuk memisahkan tanggung jawab tiap bagian kode:

### 1. Model
Berisi class Bahan, BahanCair, dan BahanPadat. Bagian ini bertugas merepresentasikan dan menyimpan data entitas bahan baku.

### 2. View / Main
Berisi class Minpro2 pada package utama. Bagian ini bertugas menampilkan antarmuka konsol (menu utama), menerima input pengguna, serta melakukan validasi awal terhadap input.

### 3. Controller
Berisi class StokController. Bagian ini bertugas mengelola logika bisnis program, mengoperasikan ArrayList, menyediakan data awal (*dummy data*), serta menjembatani interaksi antara View dan Model.

---

## Struktur Package MVC

```text
com.mycompany.minpro2
│
├── Minpro2.java (Main / View)
│
├── model
│   ├── Bahan.java (Superclass)
│   ├── BahanCair.java (Subclass)
│   └── BahanPadat.java (Subclass)
│
└── controller
    └── StokController.java (Controller & CRUD Logic)
```

<img width="337" height="234" alt="image" src="https://github.com/user-attachments/assets/e8b0edff-876c-4647-9e15-a59640219d38" />

Gambar di atas menunjukkan struktur package project, yaitu package Model berisi 3 class, package Controller berisi 1 class, serta package utama yang berisi class main. Pembagian ini menunjukkan bahwa program sudah dipisahkan sesuai perannya masing-masing dalam MVC.

---

## Alur Program

Program dimulai dari method main() pada class Minpro2. Program membuat objek Scanner untuk membaca input dan objek StokController. Saat StokController diinstansiasi, *constructor*-nya secara otomatis memuat data awal (*dummy data*) ke dalam ArrayList. Selanjutnya, perulangan while (berjalan) akan menampilkan menu utama dan memproses pilihan pengguna menggunakan switch-case.

### Menu Utama

<img width="344" height="214" alt="image" src="https://github.com/user-attachments/assets/04ddb84e-e45a-4fdf-a810-60eda917e3e0" />


Potongan logika *switch-case* pada Minpro2.java:

```java
switch (pilihan) {
    case 1:
        controller.tampilkanSemuaBahan();
        break;
    case 2:
        // Proses Tambah Bahan
        break;
    case 3:
        // Proses Update Stok
        break;
    case 4:
        // Proses Hapus Bahan
        break;
    case 5:
        // Proses Cari Bahan (Overloading Demo)
        break;
    case 0:
        berjalan = false;
        System.out.println(">> Terima kasih, program selesai.");
        break;
    default:
        System.out.println(">> Pilihan menu tidak tersedia!");
}
```

---

## Operasi CRUD

Seluruh fungsi pengelolaan data ditangani oleh class StokController yang menyimpan objek-objek bertipe Bahan di dalam ArrayList<Bahan> listBahan.

### 1. Create (`tambahBahan()`)

* **Fungsi:** Menambahkan data bahan baku baru (padat atau cair) ke dalam ArrayList.
* **Proses:** Pengguna memilih jenis bahan (Padat/Cair), lalu memasukkan ID, nama, stok awal, serta informasi kemasan khusus.

```java
public void tambahBahan(Bahan bahan) {
    listBahan.add(bahan);
    System.out.println(">> Bahan berhasil ditambahkan!");
}
```

<img width="361" height="447" alt="image" src="https://github.com/user-attachments/assets/4f9cffef-ea72-4a2c-a673-6e60abd6f9c8" />


---

### 2. Read (`tampilkanSemuaBahan()`)

* **Fungsi:** Menampilkan seluruh data bahan baku yang tersimpan.
* **Proses:** Program mengecek apakah ArrayList kosong. Jika ada data, program mengiterasi list menggunakan *for-each* dan memanggil method tampilkanInfo() milik masing-masing objek.

```java
public void tampilkanSemuaBahan() {
    if (listBahan.isEmpty()) {
        System.out.println(">> Belum ada data bahan baku.");
        return;
    }
    System.out.println("\n=== DAFTAR STOK BAHAN BAKU ===");
    for (Bahan b : listBahan) {
        b.tampilkanInfo(); // Polymorphism Overriding
        System.out.println("---------------------------------");
    }
}
```

<img width="384" height="584" alt="image" src="https://github.com/user-attachments/assets/a5ea1f79-5500-4b0d-91c0-9a61009f84e7" />


---

### 3. Update (`updateStok()`)

* **Fungsi:** Memperbarui jumlah stok bahan berdasarkan ID.
* **Proses:** Pengguna memasukkan ID bahan dan nilai stok baru. Program mencari bahan yang cocok di ArrayList dan memperbarui nilainya melalui setter setStok().

```java
public boolean updateStok(String id, int stokBaru) {
    for (Bahan b : listBahan) {
        if (b.getIdBahan().equalsIgnoreCase(id)) {
            b.setStok(stokBaru);
            return true;
        }
    }
    return false;
}
```

<img width="450" height="287" alt="image" src="https://github.com/user-attachments/assets/b6fc9132-7556-4a5b-b4ce-9ec97d020094" />

Hasil setelah di update:

<img width="370" height="351" alt="image" src="https://github.com/user-attachments/assets/dc1f7229-46ee-4c0e-b1a1-33363fcfea44" />



---

### 4. Delete (`hapusBahan()`)

* **Fungsi:** Menghapus data bahan baku dari ArrayList berdasarkan ID.
* **Proses:** Program mencari posisi elemen berdasar ID, lalu menghapusnya dengan method remove().

```java
public boolean hapusBahan(String id) {
    for (int i = 0; i < listBahan.size(); i++) {
        if (listBahan.get(i).getIdBahan().equalsIgnoreCase(id)) {
            listBahan.remove(i);
            return true;
        }
    }
    return false;
}
```

<img width="431" height="264" alt="image" src="https://github.com/user-attachments/assets/6faff1a8-95ba-406e-b29e-4ddb6fbb6fd2" />

Hasil setelah stok di hapus:

<img width="383" height="484" alt="image" src="https://github.com/user-attachments/assets/4c358523-30dc-40a6-98d4-09de420f678a" />



---

### 5. Search (`cariBahan()` - Demo Overloading)

* **Fungsi:** Mencari bahan berdasarkan ID atau Nama menggunakan konsep *Method Overloading*.

```java
// Overloading 1: Cari berdasarkan ID
public Bahan cariBahan(String id) {
    for (Bahan b : listBahan) {
        if (b.getIdBahan().equalsIgnoreCase(id)) {
            return b;
        }
    }
    return null;
}

// Overloading 2: Cari berdasarkan Nama
public Bahan cariBahan(String nama, boolean byNama) {
    for (Bahan b : listBahan) {
        if (b.getNama().equalsIgnoreCase(nama)) {
            return b;
        }
    }
    return null;
}
```

Screenshot Hasil Pencarian Bahan:

<img width="403" height="489" alt="image" src="https://github.com/user-attachments/assets/c96ce8df-9225-4573-9812-eb7e06207154" />


---

## Validasi Input (Input Validation)

Untuk mencegah program mengalami *crash* saat pengguna memasukkan tipe data yang salah, diterapkan validasi input berupa penanganan eksepsi InputMismatchException pada method inputAngka() di class Minpro2:

```java
private static int inputAngka(Scanner scanner) {
    while (true) {
        try {
            int val = scanner.nextInt();
            scanner.nextLine(); // Bersihkan newline
            return val;
        } catch (InputMismatchException e) {
            System.out.print(">> Input harus berupa angka! Masukkan lagi: ");
            scanner.nextLine();
        }
    }
}
```

Selain itu, pada class Bahan, nilai stok yang diinputkan juga divalidasi agar tidak menerima angka negatif:

```java
public void setStok(int stok) {
    if (stok >= 0) {
        this.stok = stok;
    }
}
```

Screenshot Saat Pengguna Memasukkan Input Salah / Invalid Input:

<img width="462" height="358" alt="image" src="https://github.com/user-attachments/assets/a4a9683f-ea1d-4dec-99a2-236d977b0bbd" />


---

## Konsep PBO yang Diterapkan

### 1. Encapsulation

Atribut-atribut pada class Bahan dibuat dengan modifier private atau protected. Pengaksesan dan pengubahan nilai atribut dilakukan secara aman melalui method *getter* dan *setter*. Atribut idBahan dibuat final sehingga nilainya tidak dapat diubah setelah objek diinstansiasi.

```java
private final String idBahan;
protected String nama;
protected int stok;

public String getIdBahan() { return idBahan; }
public String getNama() { return nama; }
public void setNama(String nama) { this.nama = nama; }
```

---

### 2. Inheritance

Superclass Bahan diturunkan ke dua subclass, yaitu BahanCair dan BahanPadat, menggunakan kata kunci extends. Subclass mewarisi atribut dan method milik superclass serta menggunakan super() untuk memanggil *constructor* induk.

```java
public class BahanCair extends Bahan {
    private String kemasan;

    public BahanCair(String idBahan, String nama, int stok, String kemasan) {
        super(idBahan, nama, stok);
        this.kemasan = kemasan;
    }
}
```

---

### 3. Polymorphism

#### A. Method Overriding

Method tampilkanInfo() di-override oleh kelas BahanCair dan BahanPadat untuk menampilkan detail spesifik jenis kemasan masing-masing.

```java
@Override
public void tampilkanInfo() {
    super.tampilkanInfo();
    System.out.println("Jenis       : Cair (" + kemasan + ")");
}
```

#### B. Method Overloading

Diterapkan pada method tampilkanInfo() di class Bahan dan method cariBahan() pada class StokController dengan menggunakan parameter yang berbeda.

```java
// Overloading pada class Bahan
public void tampilkanInfo() { ... }
public void tampilkanInfo(boolean ringkas) { ... }
```

```
=================================
 SISTEM STOK BAHAN BAKU COFFEE SHOP 
=================================
1. Tampilkan Semua Bahan (Read Data)
2. Tambah Bahan Baru (Create)
3. Update Stok Bahan (Update)
4. Hapus Bahan (Delete)
5. Cari Bahan (Demo Overloading)
0. Keluar
Pilih menu: 1

=== DAFTAR STOK BAHAN BAKU ===
ID Bahan    : B001
Nama Bahan  : Biji Kopi Arabika
Stok        : 50
Jenis       : Padat (Pouch 1kg)       <-- Hasil Override milik BahanPadat
---------------------------------
ID Bahan    : B002
Nama Bahan  : Susu UHT Fresh
Stok        : 20
Jenis       : Cair (Karton 1 Liter)   <-- Hasil Override milik BahanCair
---------------------------------
```

---

## Dummy Data

Agar daftar stok tidak kosong saat program pertama kali dijalankan, *constructor* StokController secara otomatis memuat dua data awal:

```java
public StokController() {
    listBahan.add(new BahanPadat("B001", "Biji Kopi Arabika", 50, "Pouch 1kg"));
    listBahan.add(new BahanCair("B002", "Susu UHT Fresh", 20, "Karton 1 Liter"));
}
```

Tampilan Dummy Data saat Pertama Kali Pilih Menu Tampilkan:

<img width="476" height="488" alt="image" src="https://github.com/user-attachments/assets/1ea461a3-8ec3-46ab-84f6-faaa76ea4288" />


---

## Kesimpulan dan Pengembangan dari Minpro 1

Mini Project 2 ini dikembangkan sebagai perbaikan dan peningkatan dari Mini Project 1. Beberapa poin pengembangan utamanya meliputi:

1. Penerapan arsitektur **MVC** yang memisahkan layer tampilan, logika bisnis, dan model data.
2. Penerapan konsep PBO lanjutan, seperti **Inheritance** (Superclass & Subclass) serta **Polymorphism** (*Overriding* & *Overloading*).
3. Peningkatan sistem **Validasi Input** untuk menangani kesalahan tipe data pengguna sehingga mencegah program dari *crash*.
4. Penambahan fitur pencarian data dan ketersediaan *dummy data* awal.
=======
# UTS-PBO-AnantaHanif-2509116023-SistemManajemenBahanBaku
>>>>>>> 71ed53446b17ac8613e1bd540f85d1d471a4a42d
