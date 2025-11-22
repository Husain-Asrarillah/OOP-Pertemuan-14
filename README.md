# 📚 Aplikasi Manajemen Data Komik (Manga Management System)

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![NetBeans](https://img.shields.io/badge/NetBeans-1B6AC6?style=for-the-badge&logo=apache-netbeans-ide&logoColor=white)

Aplikasi desktop berbasis **Java Swing** untuk mengelola data Komik, Pengarang, dan hubungan kerja sama (kolaborasi) di antara keduanya. Proyek ini dibuat untuk memenuhi tugas Praktikum Pemrograman Berorientasi Objek (PBO), dengan fokus pada implementasi **CRUD**, **JPA (Java Persistence API)**, dan **Relasi Database Many-to-Many**.

---

## ✨ Fitur Utama

### 🔐 Autentikasi & Keamanan
* **Login & Register:** Sistem autentikasi admin.
* **Lupa Password:** Fitur pemulihan akun menggunakan *Security Question*.
* **Validasi:** Pengecekan username ganda dan input kosong.

### 📂 Manajemen Data (CRUD)
* **Data Komik:** Mengelola judul, genre, tahun, dan harga.
* **Data Pengarang:** Mengelola nama, negara asal, dan status.
* **Detail Karya (Many-to-Many):** Menghubungkan Komik dan Pengarang dengan peran spesifik (misal: *Story Writer*, *Illustrator*).
* **Reusable Dialog:** Form input menggunakan JDialog yang dinamis (Satu form untuk Insert & Edit).

### 🛠️ Tools & Laporan
* **Upload CSV:** Import data massal dari file Excel/CSV.
* **Download CSV:** Export data database ke file CSV.
* **Cetak Laporan:** Generate laporan PDF menggunakan **JasperReports**.
* **Auto Refresh:** Data tabel otomatis diperbarui saat berpindah tab.

---

## 💻 Teknologi yang Digunakan

* **Bahasa:** Java (JDK 8+)
* **GUI Framework:** Java Swing (JFrame, JDialog, JTabbedPane)
* **Database:** PostgreSQL
* **ORM / Persistence:** EclipseLink (JPA 2.1)
* **Reporting:** JasperReports 6.x
* **IDE:** Apache NetBeans

---

## 🗄️ Skema Database

Aplikasi ini menggunakan skema relasional **Many-to-Many** dengan tabel junction `detail_karya`.

```sql
-- 1. Tabel Admin
CREATE TABLE login (
    username VARCHAR(50) PRIMARY KEY,
    password VARCHAR(255) NOT NULL,
    full_name VARCHAR(100),
    security_question VARCHAR(255),
    security_answer VARCHAR(255)
);

-- 2. Master Komik
CREATE TABLE komik (
    komik_id SERIAL PRIMARY KEY,
    judul VARCHAR(150) NOT NULL,
    genre VARCHAR(50),
    tahun_terbit INT,
    harga DECIMAL(12, 2)
);

-- 3. Master Pengarang
CREATE TABLE pengarang (
    pengarang_id SERIAL PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    negara VARCHAR(50),
    status VARCHAR(20)
);

-- 4. Relasi (Junction Table)
CREATE TABLE detail_karya (
    id SERIAL PRIMARY KEY,
    komik_id INT REFERENCES komik(komik_id) ON DELETE CASCADE,
    pengarang_id INT REFERENCES pengarang(pengarang_id) ON DELETE CASCADE,
    peran VARCHAR(50) -- Contoh: 'Writer', 'Illustrator'
);
````

-----

## 🚀 Cara Instalasi & Menjalankan

1.  **Clone Repositori**

    ```bash
    git clone [https://github.com/username-kamu/nama-repo.git](https://github.com/Husain-Asrarillah/OOP-Pertemuan-14)
    ```

2.  **Setup Database**

      * Buka pgAdmin atau terminal PostgreSQL.
      * Buat database baru (misal: `db_komik`).
      * Jalankan script SQL di atas untuk membuat tabel.

3.  **Konfigurasi Koneksi (NetBeans)**

      * Buka project di NetBeans.
      * Masuk ke folder `Configuration Files` \> `META-INF` \> `persistence.xml`.
      * Sesuaikan properti berikut dengan database lokal kamu:
        ```xml
        <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://localhost:5432/db_komik"/>
        <property name="javax.persistence.jdbc.user" value="postgres"/>
        <property name="javax.persistence.jdbc.password" value="password_kamu"/>
        ```

4.  **Tambahkan Library (JAR)**
    Pastikan library berikut sudah ada di folder `Libraries` NetBeans:

      * `postgresql-jdbc.jar`
      * `eclipselink.jar` & `javax.persistence.jar`
      * `jasperreports` (dan dependensinya: commons-logging, commons-collections, dll).

5.  **Run Project**

      * Jalankan file `LoginPage.java` sebagai entry point.

-----

## 📷 Screenshots

Halaman Login
<img width="525" height="583" alt="image" src="https://github.com/user-attachments/assets/4f3ff560-57cb-48c4-af72-f52394e54713" />
 Dashboard Utama 
<img width="924" height="651" alt="image" src="https://github.com/user-attachments/assets/4b6d5b2d-9f01-49db-8ebe-f020bae24dfd" />


Input Dialog
<img width="302" height="385" alt="image" src="https://github.com/user-attachments/assets/0fb79193-9dce-4e16-adc9-cb37a19c34d0" />
Laporan Jasper
<img width="488" height="320" alt="image" src="https://github.com/user-attachments/assets/0fe40f65-81af-4b3d-8534-d84ed3275c6e" />


-----

## 📄 Format CSV untuk Upload

Jika ingin menggunakan fitur Upload, format CSV seperti berikut:

**Komik.csv**

```csv
Naruto; Action; 1999; 35000
One Piece; Adventure; 1997; 40000
```
`

-----
