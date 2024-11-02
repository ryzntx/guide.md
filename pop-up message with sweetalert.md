### Pop-up alert dan Confirm prompt dengan Library Sweetalert2 pada PHP

##### - VIEW -
Masukan css dan javascript pada tempatnya (template/template.php) atau sesuaikan dimana base layoutnya
``````html
<!-- CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@11.8.0/dist/sweetalert2.min.css">

<!-- Javascript -->
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11.8.0/dist/sweetalert2.all.min.js"></script>
``````

Dokumentasi sweetalert bisa dilihat di 
https://sweetalert2.github.io/

#### Controller

perhatikan baris kode dibawah ini

```````` php
return redirect()->to('mahasiswa');
````````
atau
```````` php
return redirect()->to('matakuliah');
````````
pada setiap controller mahasiswa dan matakuliah memilliki baris kode diatas pada function simpan, update, dan delete

untuk mengirimkan sebuah pesan dari controller dengan sifat sementara ke halaman tampilan dapat menggunakan function "with"
*maksud sementara ini ketika pesan sudah di tampilkan maka ketika kalian melakukan reload pada halaman web kalian,
maka pesan tersebut tidak akan muncul lagii

untuk menggunakan fungsi "with" ini dapat di implementasikan dengan cara menambahkan fungsi "with" ini di baris return 
*contoh
```````` php
return redirect()->to('mahasiswa')->with('success', 'Masukan pesan disini!');
````````

pada fungsi "with" ini memperlukan dua parameter penting yaitu 'key' dan 'message'

```````` php
return redirect()->to('mahasiswa')->with('success', 'Masukan pesan disini!');
                                          ^^^^^^^    ^^^^^^^^^^^^^^^^^^^^^
                                        INI KEY NYA     INI MESSAGE NYA
````````                                        
*dua parameter ini wajib di isi!

jadi aplikasi kan cara diatas pada controller mahasiswa dan matakuliah di function simpan, update, dan delete pada baris kode return
```````` php
->  return redirect()->to('mahasiswa')->with('success', 'Masukan pesan disini!'); //ini buat mahasiswa
->  return redirect()->to('matakuliah')->with('success', 'Masukan pesan disini!'); //ini buat matakuliah
````````

-------------------------------------
#### Menampilkan Alert dengan Sweetalert2

Untuk menampilkan pesan pada View buka file template.php pada folder template atau tempat kalian simpan file template.php

lalu scroll kebawah cari tag / kode 
`````` html
</body>
``````

letakan kursor kalian pada awal baris kode body seperti dibawah ini
`````` html
|</body>

``````
lalu tekan enter maka akan membuat baris baru di atas `</body>`
`````` html
//baris baru disini
<body/>
``````

lalu tambahkan tag ini
`````` html
<script>

</script>
``````

diatas tag `</body>`

lalu di tag script tambah sebuah kode seperti dibawah ini

`````` php
<script>
<?php if (session('success')) : ?>
        Swal.fire({
            title: 'Sukses!',
            text: '<?= session('success') ?>',
            icon: 'success',
            timer: 3500
        })
    <?php endif ?>
    <?php if (session('warning')) : ?>
        Swal.fire({
            title: 'Peringatan!',
            text: '<?= session('warning') ?>',
            icon: 'warning',
            timer: 3500
        })
    <?php endif ?>
    <?php if (session('error')) : ?>
        Swal.fire({
            title: 'Eror!',
            text: '<?= session('error') ?>',
            icon: 'error',
            timer: 3500
        })
    <?php endif ?>
    <?php if (session('info')) : ?>
        Swal.fire({
            title: 'Info!',
            text: '<?= session('info') ?>',
            icon: 'info',
            timer: 3500
        })
    <?php endif ?>
</script>
``````

#### Membuat Confirm Prompt dengan SweetAlert2

`````` html
<script>
function confirmDeleteAlert(e, target) {
    e.preventDefault()
    Swal.fire({
        title: 'Apakah anda yakin?',
        text: "Data yang dihapus tidak bisa dikembalikan!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#d33',
        cancelButtonColor: '#3085d6',
        confirmButtonText: 'Ya, hapus!',
        cancelButtonText: 'Batal'
    }).then((result) => {
        if (result.isConfirmed) {
            window.location.href = target.href
        }
    })
}
</script>
``````

Gunakan atribut onclick pada tag button atau a untuk mengimplementasikan 
`````` html

onclick="return confirmDeleteAlert(event, this)"

``````

Contoh implementasi fungsi confirm sweetalert pada sebuah tombol

<a href="<?=base_url('admin/manajemenAkun/hapus/' . $row->id)?>" id="hapusData"
onclick="return confirmDeleteAlert(event, this)" class="btn btn-sm btn-danger"><i
    class="fa fa-trash"></i></a>

*script di simpan pada file template/template.php atau tempat code layout di posisi atas kode `</body>`*

