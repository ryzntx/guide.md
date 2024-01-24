---
marp: true
---

### Step pada di View / Tampilan
pada tag ```<form action="" ....```
tambahkan sebuah attribute enctype
```enctype="multipart/form-data"```

contoh lengkap nya 
```<form action="url_kalian" method="post" enctype="multipart/form-data">```

buat sebuah form input dengan tipe file

```<input type="file" name="gambar" id="" class="form-control">```

form input tersebut di simpan di dalam tag ```<form>disini</form>```

### Step pada controller

tambahkan kode ini pada sebuah fungsi

```
$file = $this->request->getFile('gambar');
//Upload File
if ($file->isValid()) {
    $file->move('uploads/berita');
    $namaFile = $file->getName();
}
```

pada variabel 
```
$file = $this->request->getFile('gambar');
                               ^^^^^^^^^^
```
bisa di lihat terdapat string gambar, gambar tersebut dari sebuah form input
```
<input type="file" name="gambar" id="" class="form-control">
                    ^^^^^^^^^^^^^
                dari sini nihhh
```

lalu pada baris kode ```if ($file->isValid()) {``` disini untuk mengecek apakah file yang di upload itu ada / benar kah?

pada baris kode ```$file->move('uploads/berita');``` disini kode untuk memindahkan file yang sudah di upload ke folder public, secara otomatis akan membuat folder baru dengan nama uploads, lalu di dalam folder uploads akan terbuat folder berita.

```uploads/berita``` kalian bisa ganti penamaan folder ini

lalu pada baris kode ```$namaFile = $file->getName();``` disini untuk mendapatkan nama file setelah di pindahkan

jadi kalian untuk menyimpan nama file ke database bisa panggil saja variabel ```$namaFile``` ini

### Tahap menampilkan sebuah gambar atau apapun itu dari folder public

kalian bisa gunakan fungsi ```base_url()``` untuk mendapatkan assets/apapun itu dari folder public, dengan syarat baseURL pada .env / App.php sudah kalian atur dan sesuaikan

misal disini saya akan menampilkan sebuah gambar yang telah saya uploads dan di tersimpan di folder ```public/uploads/gambar```

saya akan lakukan beberapa cara

```<img src="<?= base_url('path ke folder uploads') ?>"/>```

```<img src="<?= base_url('uploads/gambar/nama_file') ?>"/>```

kalau kalian ingin mengambil gambar itu sesuai dengan nama_file yang ada di database kalian bisa gunakan cara dibawah

```<img src="<?= base_url('uploads/gambar/' . $nama_file) ?>"/>```

untuk yang melakukan foreach
```<img src="<?= base_url('uploads/gambar/' . $item['nama_field']) ?>"/>```
