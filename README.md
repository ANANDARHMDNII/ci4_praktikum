# Pertemuan ke 2 
## Profil
|  |  |
| -------- | --- |
| *Nama* |Ananda Rahmadani |
| *Kelas* | TI.23.A.5 |
| *Mata Kuliah* | Pemrograman Web 2 |
## Praktikum 1: PHP Framework (Codeigniter)
### Langkah-langkah Praktikum
### Persiapan
Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi pada webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan pengembangan Codeigniter 4. Berikut beberapa ekstensi yang perlu diaktifkan:

* php-json ekstension untuk bekerja dengan JSON;
* php-mysqlnd native driver untuk MySQL;
* php-xml ekstension untuk bekerja dengan XML;
* php-intl ekstensi untuk membuat aplikasi multibahasa;
* libcurl (opsional), jika ingin pakai Curl.
  
Untuk mengetahui ekstensi tersebut telah aktif atau belum, kita bisa mengetahui nya melalui powershell atau command prompt dengan cara:

### Catatan : mulai dari PHP 7.0, ekstensi JSON biasanya sudah termasuk secara bawaan.
![cmd 1](https://github.com/user-attachments/assets/100a9d84-dc66-45ac-9ca9-0e702a395df5)


Lalu kalian bisa mencari ekstensi yang kalian butuhkan, jika ada yang belum diaktivasi kalian dapat mengaktifkan ekstensi tersebut, melalu XAMPP Control Panel, pada bagian Apache klik Config -> PHP.ini :

![image](https://github.com/user-attachments/assets/98e59d08-d429-4e81-8d79-ff525d9b89da)

![image](https://github.com/user-attachments/assets/8148e2ab-b664-4482-a306-4f90a4732256)

* Contohnya disini extension=intl belum aktif, maka cara mengaktivasinya adalah dengan menghilangkan tanda ; (titik koma) pada ekstensi yang akan diaktifkan. Kemudian simpan kembali filenya dan restart Apache web server.
## Instalasi Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.

* Unduh Codeigniter dari website https://codeigniter.com/download
* Extrak file zip Codeigniter ke direktori htdocs/lab11_ci.
* Ubah nama direktory codeigniter4-framework-v4.x.xx menjadi ci4.
* Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/
  
![image](https://github.com/user-attachments/assets/608bc518-a8b7-4a7b-a96f-9f3288749278)

## Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka Shell pada XAMPP.

![cmd 2](https://github.com/user-attachments/assets/ce930a98-8274-40ae-b380-d33683edd746)

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat (Contoh : cd htdocs/lab11_ci/ci4)

Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah:

### php spark
![cmd 3](https://github.com/user-attachments/assets/08e1d239-32f2-42dd-a744-8dbbedf250b7)

## Mengaktifkan Mode Debugging
Codeigniter 4 menyediakan fitur debugging untuk memudahkan developer untuk mengetahui pesan error apabila terjadi kesalahan dalam membuat kode program.

Secara default fitur ini belum aktif. Ketika terjadi error pada aplikasi akan ditampilkan pesan kesalahan seperti berikut.

![image](https://github.com/user-attachments/assets/0bcf5084-85ce-4bf2-b7fa-e257bccc6e60)

Semua jenis error akan ditampilkan sama. Untuk memudahkan mengetahui jenis errornya, maka perlu diaktifkan mode debugging dengan mengubah nilai konfigurasi pada environment variable CI_ENVIRONMENT menjadi development. 

![image](https://github.com/user-attachments/assets/4548caf6-bed5-452d-b66a-315d1cc1806f)

Ubah nama file env menjadi .env kemudian buka file tersebut dan ubah nilai variable CI_ENVIRONMENT menjadi development.

### Catatan : Kadang, CodeIgniter tidak membaca file .env karena masih dikomentari, pastikan tidak ada tanda # di depan CI_ENVIRONMENT.

![image](https://github.com/user-attachments/assets/09fbe89c-f19e-4af4-999d-94a854cac9af)

Contoh error yang terjadi. Untuk mencoba error tersebut, ubah kode pada file app/Controller/Home.php hilangkan titik koma pada akhir kode return view('welcome_message'). 

![image](https://github.com/user-attachments/assets/74b6feea-41e2-438b-9725-16865ac1b9b6)

### Memahami konsep MVC
Codeigniter menggunakan konsep MVC. MVC meripakan singkatan dari Model-View- Controller. MVC merupakan konsep arsitektur yang umum digunakan dalam pengembangan aplikasi. Konsep MVC adalah memisahkan kode program berdasarkan logic proses, data, dan tampilan. Untuk logic proses diletakkan pada direktori Contoller, Objek data diletakkan pada direktori Model, dan desain tampilan diletakkan pada direktori View.

Codeigniter menggunakan konsep pemrograman berorientasi objek dalam mengimplementasikan konsep MVC.

Model merupakan kode program yang berisi pemodelan data. Data dapat berupa database ataupun sumber lainnya.

View merupakan kode program yang berisi bagian yang menangani terkait tampilan user interface sebuah aplikasi. didalam aplikasi web biasanya pasti akan berhubungan dengan html dan css.

Controller merupakaan kode program yang berkaitan dengan logic proses yang menghubungkan antara view dan model. Controller berfungsi untuk menerima request dan data dari user kemudian diproses dengan menghubungkan bagian model dan view.

### Routing dan Controller
Routing merupakan proses yang mengatur arah atau rute dari request untuk menentukan fungsi/bagian mana yang akan memproses request tersebut. Pada framework CI4, routing bertujuan untuk menentukan Controller mana yang harus merespon sebuah request. Controller adalah class atau script yang bertanggung jawab merespon sebuah request.

Pada Codeigniter, request yang diterima oleh file index.php akan diarahkan ke Router untuk meudian oleh router tesebut diarahkan ke Controller.

Router terletak pada file app/config/Routes.php 

![image](https://github.com/user-attachments/assets/2dcc1651-c8f0-4f8e-b86d-8b64e018f17d)

Pada file tersebut kita dapat mendefinisikan route untuk aplikasi yang kita buat. Contoh:

```php
$routes->get('/', 'Home::index');
```

Kode tersebut akan mengarahkan rute untuk halaman home.

## Membuat Route Baru.

Tambahkan kode berikut di dalam Routes.php

```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan perintah berikut.

php spark routes 
![image](https://github.com/user-attachments/assets/394573fa-b8ee-4c5e-98e4-6f4a898eb7aa)

Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url http://localhost:8080/about

![image](https://github.com/user-attachments/assets/1f5599b6-ef02-4361-af6a-9be66ed92b9e)

Ketika diakses akan mucul tampilan error 404 file not found, itu artinya file/page tersebut tidak ada. Untuk dapat mengakses halaman tersebut, harus dibuat terlebih dahulu Contoller yang sesuai dengan routing yang dibuat yaitu Contoller Page.

### Membuat Controller
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama page.php pada direktori Controller kemudian isi kodenya seperti berikut.

```php
<?php

namespace App\Controllers;

class Page extends BaseController
{
    public function about()
    {
        echo "Ini halaman About";
    }
    public function contact()
    {
        echo "Ini halaman Contact";
    }
    public function faqs()
    {
        echo "Ini halaman FAQ";
    }
}
```

![image](https://github.com/user-attachments/assets/6bf57a17-bb44-4d9e-a88c-d5be1ae59fea)

#### Auto Routing
Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai true menjadi false.

```php
$routes->get('page/tos', 'Page::tos');
$routes->setAutoRoute(true);
```

Tambahkan method baru pada Controller Page seperti berikut.
```php
public function tos()
{
    echo "ini halaman Term of Services";
}
```

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan alamat: http://localhost:8080/page/tos alt text
![tos](https://github.com/user-attachments/assets/d3df16bb-ae90-4c0d-a3b4-1e09ce025415)

#### Membuat View
Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru dengan nama about.php pada direktori Views (app/Views/about.php) kemudian isi kodenya seperti berikut.
```php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
</head>

<body>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
</body>

</html>
```
Ubah method about pada class Controller Page menjadi seperti berikut:
```php
    public function about()
    {
        return view('about', [
            'title' => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }
```
Kemudian lakukan refresh pada halaman tersebut.

alt text

### Membuat Layout Web dengan CSS
Pada dasarnya layout web dengan css dapat diimplamentasikan dengan mudah pada codeigniter. Yang perlu diketahui adalah, pada Codeigniter 4 file yang menyimpan asset css dan javascript terletak pada direktori public.

Buat file css pada direktori public dengan nama style.css

[alt text](https://github.com/nurulfir/Lab7Web/raw/main/img/style.png)

Kemudian buat folder template pada direktori view kemudian buat file header.php dan footer.php

File app/Views/template/header.php
```php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css'); ?>">
</head>

<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/'); ?>" class="active">Home</a>
            <a href="<?= base_url('/artikel'); ?>">Artikel</a>
            <a href="<?= base_url('/about'); ?>">About</a>
            <a href="<?= base_url('/contact'); ?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main"></section>
```
File app/Views/template/footer.php
```php
</section>
<aside id="sidebar">
    <div class="widget-box">
        <h3 class="title">Widget Header</h3>
        <ul>
            <li><a href="#">Widget Link</a></li>
            <li><a href="#">Widget Link</a></li>
        </ul>
    </div>
    <div class="widget-box">
        <h3 class="title">Widget Text</h3>
        <p>Vestibulum lorem elit, iaculis in nisl volutpat,
            malesuada tincidunt arcu. Proin in leo fringilla, vestibulum mi porta,
            faucibus felis. Integer pharetra est nunc, nec pretium nunc pretium ac.</p>
    </div>
</aside>
</section>
<footer>
    <p>&copy; 2021 - Universitas Pelita Bangsa</p>
</footer>
</div>
</body>

</html>
```
Kemudian ubah file app/Views/about.php seperti berikut.
```php
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```
Selanjutnya refresh tampilan pada alamat http://localhost:8080/about 
![image](https://github.com/user-attachments/assets/ec2ea91f-d2cf-42fa-99ce-04b3e4138483)

# Praktikum 2: Framework Lanjutan (CRUD) - CodeIgniter 4
### Tujuan Praktikum
1. Memahami konsep dasar penggunaan Model di CodeIgniter.
2. Mengenal dan menerapkan konsep CRUD (Create, Read, Update, Delete).
3. Membuat aplikasi sederhana menggunakan Framework CodeIgniter 4.

### Persiapan
* Gunakan text editor seperti VSCode.
* Buka folder lab7_php_ci yang ada di dalam folder htdocs.
* Jalankan XAMPP, lalu aktifkan MySQL Server.
### Langkah-Langkah
#### Membuat Database
Buat database dan tabel artikel dengan perintah berikut di phpMyAdmin atau terminal MySQL:

```php
CREATE DATABASE lab_ci4;
```
```sql
CREATE TABLE artikel (
  id INT(11) auto_increment,
  judul VARCHAR(200) NOT NULL,
  isi TEXT,
  gambar VARCHAR(200),
  status TINYINT(1) DEFAULT 0,
  slug VARCHAR(200),
  PRIMARY KEY(id)
);
```
### Konfigurasi Koneksi Database
* Edit file .env dan sesuaikan pengaturan database sesuai konfigurasi lokal kamu, contohnya:

```sql
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password =
database.default.DBDriver = MySQLi
```
### Membuat Model
* Buat file ArtikelModel.php di folder app/Models/:

```php
<?php
namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```
### Membuat Controller
Buat file Artikel.php di folder app/Controllers/:

```php
<?php

namespace App\Controllers;
use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }
}
```
### Membuat View
* Buat folder artikel di dalam app/Views, lalu buat file index.php:

```php
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2><a href="<?= base_url('/artikel/' . $row['slug']); ?>"><?= $row['judul']; ?></a></h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']); ?>" alt="<?= $row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```
Akses halaman ini melalui browser: http://localhost:8080/artikel

![image](https://github.com/user-attachments/assets/98444585-b0a4-4d97-94fe-fe7aa304e799)

### Menambah Data Artikel
Tambahkan data manual ke database:

```sql
INSERT INTO artikel (judul, isi, slug) VALUES
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy...', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang...', 'artikel-kedua');
```
Refresh kembali browser, sehingga akan ditampilkan hasilnya.
![image](https://github.com/user-attachments/assets/26c7b254-5785-4c6d-aa8e-2e4cfaf1e68c)

### Menampilkan Detail Artikel
Tambahkan method view() di controller Artikel:

```php

public function view($slug)
{
    $model = new ArtikelModel();
    $artikel = $model->where(['slug' => $slug])->first();

    if (!$artikel) {
        throw PageNotFoundException::forPageNotFound();
    }

    $title = $artikel['judul'];
    return view('artikel/detail', compact('artikel', 'title'));
}
```
### Lalu buat file detail.php:
```php

<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']); ?>" alt="<?= $artikel['judul']; ?>">
    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```
### Tambahkan routing di app/Config/Routes.php:
```php
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```
![image](https://github.com/user-attachments/assets/d7c72e83-ab9e-4f52-b70e-862e2af7a462)

### Membuat Halaman Admin
Tambahkan method admin_index() di controller:

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();
    $artikel = $model->findAll();
    return view('artikel/admin_index', compact('artikel', 'title'));
}
```
Lalu buat view admin_index.php untuk halaman admin.
Tambahkan grup route untuk admin:
``php
<?= $this->include('template/admin_header'); ?>
<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>AKsi</th>
        </tr>
    </thead>
    <tbody>
    <?php if($artikel): foreach($artikel as $row): ?>
    <tr>
        <td><?= $row['id']; ?></td>
        <td>
            <b><?= $row['judul']; ?></b>
            <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
        </td>
        <td><?= $row['status']; ?></td>
        <td>
            <a class="btn" href="<?= base_url('/admin/artikel/edit/' . $row['id']);?>">Ubah</a>
            <a class="btn btn-danger" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . $row['id']);?>">Hapus</a>
        </td>
    </tr>
    <?php endforeach; else: ?>
    <tr>
        <td colspan="4">Belum ada data.</td>
    </tr>
    <?php endif; ?>
    </tbody>
    <tfoot>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>AKsi</th>
        </tr>
    </tfoot>
</table>

<?= $this->include('template/admin_footer'); ?>
```
Tambahkan routing untuk menu admin seperti berikut:
```php
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```
Akses melalui: http://localhost:8080/admin/artikel
![Admin](https://github.com/user-attachments/assets/9ad8405b-1b5a-415f-9d7a-8c1800aaaade)

### Menambahkan Artikel Baru
Tambahkan method add() di controller:
```php
public function add()
{
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid) {
        $artikel = new ArtikelModel();
        $artikel->insert([
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
            'slug' => url_title($this->request->getPost('judul')),
        ]);
        return redirect('admin/artikel');
    }

    $title = "Tambah Artikel";
    return view('artikel/form_add', compact('title'));
}
```
Buat file form_add.php untuk form tambah artikel.
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul">
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```
![form_add](https://github.com/user-attachments/assets/9fae90fe-dd4e-416a-987d-7603e70f1787)

### Mengubah Data
Tambahkan fungsi/method baru pada Controller Artikel dengan nama edit().
```php
public function edit($id)
{
    $artikel = new ArtikelModel();

    // validasi data.
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid)
    {
        $artikel->update($id, [
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
        ]);
        return redirect('admin/artikel');
    }

    // ambil data lama
    $data = $artikel->where('id', $id)->first();
    $title = "Edit Artikel";
    return view('artikel/form_edit', compact('title', 'data'));
}
```
Kemudian buat view untuk form tambah dengan nama form_edit.php
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul" value="<?= $data['judul'];?>" >
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"><?=$data['isi'];?></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```
![form_edit](https://github.com/user-attachments/assets/b70a2b5b-659a-4c87-bdfe-d82a53ae8013)

### Menghapus Bagian Data
Tambahkan fungsi/method baru pada Controller Artikel dengan nama delete().
```php
public function delete($id)
{
    $artikel = new ArtikelModel();
    $artikel->delete($id);
    return redirect('admin/artikel');
}
```

# Praktikum 3: View Layout dan View Cell
### Langkah-langkah Praktikum
#### Persiapan
* vBuka folder lab7_php_ci yang digunakan pada praktikum sebelumnya.
* Gunakan text editor seperti VSCode.
#### Membuat Layout Utama
* Buat folder layout di dalam app/Views/.
* Buat file main.php di dalam folder tersebut.
* Buat file main.php di dalam folder layout dengan kode berikut:
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title ?? 'My Website' ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>"> 
</head>
<body>
    <div id="container">
        <header><h1>Layout Sederhana</h1></header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
                <?= $this->renderSection('content') ?>
            </section>
            <aside id="sidebar">
                <?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>
                <!-- Widget lainnya -->
            </aside>
        </section>
        <footer><p>&copy; 2021 - Universitas Pelita Bangsa</p></footer>
    </div>
</body>
</html>
```
#### Modifikasi File View
Ubah app/Views/home.php agar sesuai dengan layout baru:
```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->endSection() ?>
```
#### Menampilkan Data Dinamis dengan View Cell
View Cell adalah fitur yang memungkinkan pemanggilan tampilan dalam bentuk komponen yang dapat digunakan ulang. Cocok digunakan untuk elemen-elemen yang sering muncul di berbagai halaman seperti sidebar, widget, atau menu navigasi.

#### Membuat class View Cell
* Buat folder Cells di dalam app/.
* Buat file ArtikelTerkini.php di dalam app/Cells/ dengan kode berikut:
```php
namespace App\Cells;

use CodeIgniter\View\Cell;
use App\Models\ArtikelModel;

class ArtikelTerkini extends Cell
{
    public function render()
    {
        $model = new ArtikelModel();
        $artikel = $model->orderBy('created_at', 'DESC')->limit(5)->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```
#### Membuat View untuk View Cell
* Buat folder components di dalam app/Views/.
* Buat file artikel_terkini.php:
```php
<h3>Artikel Terkini</h3>
<ul>
<?php foreach ($artikel as $row): ?>
    <li><a href="<?= base_url('/artikel/' . $row['slug']) ?>"><?= $row['judul'] ?></a></li>
<?php endforeach; ?>
</ul>
```
## Pertanyaan dan Tugas
### 1. Sesuaikan data dengan praktikum sebelumnya, perlu melakukan perubahan field pada database dengan menambahkan tanggal agar dapat mengambil data artikel terbaru.
##### Jawab:
```php
ALTER TABLE artikel ADD COLUMN created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP;
```
![image](https://github.com/user-attachments/assets/5c5a82da-f508-489f-8ad7-554d480a81a2)

## 2. Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan improvisasi.
## 3. Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?
##### Jawab:
"Membuat tampilan aplikasi lebih konsisten, menghemat waktu pengembangan, dan memudahkan pemeliharaan."
Dengan layout, bagian seperti header, footer, dan sidebar cukup dibuat sekali dan bisa dipakai ulang di semua halaman.
## 4. Jelaskan perbedaan antara View Cell dan View biasa.
##### Jawab:
Perbedaan View Cell dan View biasa secara simpel:

* View biasa: digunakan untuk menampilkan tampilan utama halaman, seperti konten artikel atau halaman login.
* View Cell: digunakan untuk menampilkan bagian kecil/komponen tertentu yang bisa dipakai ulang, seperti daftar kategori, widget terbaru, atau sidebar.
###### Contoh:
* View biasa: ```php return view('artikel/index'); ```
* View Cell: ```php <?= view_cell('Sidebar::kategori') ?> ```
  
## 5. Ubah View Cell agar hanya menampilkan post dengan kategori tertentu.
###  Langkah:
* Tambahkan field kategori di tabel artikel
```sql
ALTER TABLE artikel ADD kategori VARCHAR(50);
```
![image](https://github.com/user-attachments/assets/837d7243-d585-4b41-a0d9-ca9cc1fcea7d)

* Tambahkan parameter kategori di method render:
```sql
public function render($kategori = null)
{
    $model = new ArtikelModel();
    $query = $model->orderBy('created_at', 'DESC');

    if ($kategori) {
        $query->where('kategori', $kategori);
    }

    $artikel = $query->limit(5)->findAll();

    return view('components/artikel_terkini', ['artikel' => $artikel]);
}
```
* Isi setiap kolom pada tabel, bisa manual atau lewat fitur tambah artikel
* Modifikasi View Cell agar filter berdasarkan kategori Buka app/Cells/ArtikelTerkini.php, ubah fungsi render() jadi seperti ini:
```php
<?php

namespace App\Cells;

use App\Models\ArtikelModel;

class ArtikelTerkini
{
    public function render($kategori = null)
    {
        $model = new ArtikelModel();

        $query = $model->orderBy('created_at', 'DESC')->limit(5);
        if ($kategori) {
            $query->where('kategori', $kategori);
        }

        $artikel = $query->findAll();

        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```
* Panggil View Cell dengan parameter kategori Pada app/Views/layout/main.php:
```php
<?= view_cell('App\\Cells\\ArtikelTerkini::render', ['kategori' => 'Teknologi']) ?>
```
* Tambahkan route agar URL seperti /kategori/teknologi bisa diakses:
```php
$routes->get('/kategori/(:segment)', 'Artikel::kategori/$1');
```
* Tambah View-nya (app/Views/artikel/kategori.php)
```php
<?= $this->extend('layout/main') ?>
<?= $this->section('content') ?>

<h2><?= $title ?></h2>
<ul>
    <?php foreach ($artikel as $row): ?>
        <li>
            <a href="<?= base_url('/artikel/' . $row['slug']) ?>">
                <?= esc($row['judul']) ?>
            </a>
        </li>
    <?php endforeach; ?>
</ul>

<?= $this->endSection() ?>
```
## Screenshot Hasil
![Olahraga](https://github.com/user-attachments/assets/347837e7-ad35-403b-bb37-627c7b14125b)
![Teknologi](https://github.com/user-attachments/assets/b7612b41-b51f-481a-bde4-11f9212052da)

