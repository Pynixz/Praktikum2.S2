# Praktikum2.S2
# Tugas Praktikum { Pertemuan ke 7 } <img src=https://qph.fs.quoracdn.net/main-qimg-648763cc041459725b62108f4fdf5b91 width="110px" >


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|---------------------|----------|-------|----------|
|Dhiyaulhaq Al Maududi|312310508|TI.23.A5|Basis Data|

# Soal Latihan Praktikum
## Data Model Mapping

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```
- Buat DDL Script berdasarkan skema ERD tersebut diatas. 
- Jalankan script DDL tersebut pada DBMS MySQL.

**Langkah-langkahnya :**

**1. Buat dulu script untuk table Mahasiswa :**

```
create table Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

![1](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/aaea3a9c-094c-4140-a981-bd779e1ce07c)


**Tampilkan hasil table :**

`desc Mahasiswa;`

![2](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/7bd4d0f2-2bb6-4a2f-b6ed-dfbe88b9fb09)

**2. Buat script untuk table Dosen :**
```
create table Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );
```

![3](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/9723693b-152f-4fce-a071-7b225a79d396)

**Tampilkan tabel :**

`desc Dosen;`

![4](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/0a7f8eb0-7d92-4d9e-99a2-c3afc47561e8)

**3. Buat script untuk Mata kuliah :**
```
create table Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );
```

![5](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/7eb6a574-5fd8-463c-b010-924948846709)


**Tampilkan table :**

`desc Matakuliah;`

![6](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/b55d391a-a7cc-4d16-a64e-f9cbd7574ac9)

**4. Buat script untuk jadwal mengajar :**
```
create table JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    ); 
```

![7](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/69119949-13f8-4c90-953e-fd20ab7c6d43)


**Tampilkan table :**

`desc JadwalMengajar;`

![8](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/f1d78e06-3f80-451b-a72a-6595a3609135)


**5. Buat script untuk KRSMahasiswa :**
```
CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

![9](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/fa523765-e7fa-4375-8dca-f6089e837bda)


**Tampilkan table :**

`desc KRSMahasiswa;`

![10](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/4120c135-a075-403c-906b-8232c1ce0d6b)


# Soal Latihan Praktikum

Berdasarkan table Mahasiswa pada praktikum sebelumnya: (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

***Isi data pada table tersebut sebanyak minimal 5 record data. Tampilkan semua isi/record tabel!***

- Ubah data tanggal lahir Mahasiswa yang bernama Ari menjadi: 1979-08-31!

- Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!

- Hapus Mahasiswa yang bernama Dina!

- Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!

- Tampilkan data nama dan alamat Mahasiswa saja dari tabel tersebut

- Tampilkan data Mahasiswa terurut berdasarkan nama.

**1. Mengisi tabel dengan minimal 5 record data :**
```
insert into Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");
```

![11](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/41adbe6c-6301-4782-af13-e01953379b01)


**2. Menampilkan semua isi/record pada tabel bisa menggunakan kode berikut :**

`select*from Mahasiswa;`

![12](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/ec7ba6cf-86fa-4acd-8fcd-6a2ce29372ee)


**3. Mengubah data tanggal lahir Mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :**

`update Mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;`

![13](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/abc13295-82f0-4094-add2-b4e5ffb5f1f2)


**4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :**

`select*from Mahasiswa where nim=11223344;`

![14](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/955caec7-04fd-4e97-97b8-81e40a1f6ae0)


**5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:**

`delete from Mahasiswa where nim=11223346;`

![15](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/f7d334f8-edab-4ea9-a0da-57771afdc070)


**6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :**

`select*from Mahasiswa where tgl_lahir<='1996-1-2';`

![16](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/162a80b9-fe7d-47f6-8482-0d31c95439a5)


**7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :**

`select*from Mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';`

![17](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/5c626fcc-de4a-4788-b98a-c67a31e9a410)


**8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :**
```
select * from Mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' 
or tgl_lahir<='2002-4-22' 
and jenis_kelamin='Perempuan';
```

![18](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/0b8fb64d-f606-497e-8bf5-5568c8ada9d8)


**9. Menampilkan data nama dan jalan Mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :**

`select nama, jalan from Mahasiswa;`

![19](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/b4ca51e7-3140-4b70-be4d-9ec228abacda)


**10. Menampilkan data Mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :**

`select*from Mahasiswa -> order by nama asc;`

![20](https://github.com/Pynixz/Praktikum2.S2/assets/147568964/75ad5123-18d9-4d7a-9e11-ec25be453e92)


# Evaluasi dan Pertanyaan

***Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!***

**1. Menambah data :**

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

*Contoh :*

`INSERT INTO biodata (nim, nama, alamat) VALUE ('1234','Uyun','Bekasi');`

![alt text](Screenshot/21.png)

**2. Menampilkan data :**

`SELECT * FROM <table> SELECT [field1, ..., fieldn] FROM <table>`

*Contoh :*

`SELECT*FROM biodata;`

![alt text](Screenshot/22.png)

**3. Mengubah data :**

`UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>;`

*Contoh :*

`UPDATE biodata SET nama='Nurul', alamat='Setu' WHERE nim='1234';`

![alt text](Screenshot/23.png)

**4. Menghapus data :**

`DELETE FROM <table> WHERE <kondisi>`

*Contoh :*

`DELETE FROM biodata WHERE nim=‘1234’`

![alt text](Screenshot/24.png)

***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

**Jawaban nya :**

Operator BETWEEN ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan untuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>

***Berikan kesimpulan anda!***

Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekkan diatas.

***Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen.***

<img src=https://pngimg.com/uploads/google_drive/google_drive_PNG9.png width="110px" >

- [Link Laporan Praktikum](https://docs.google.com/document/d/11nxeeY7RrJtV7LY4_I90JiMloq9qy-ov/edit?usp=drivesdk&rtpof=true&sd=true)
