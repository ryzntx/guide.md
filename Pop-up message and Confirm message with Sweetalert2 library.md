### Pop-up dan Confirm prompt dengan Library Sweetalert2 pada PHP

##### - VIEW -
Masukan css dan javascript pada tempatnya (template/template.php)
``````html
<!-- CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@11.8.0/dist/sweetalert2.min.css">

<!-- Javascript -->
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11.8.0/dist/sweetalert2.all.min.js"></script>
``````

Dokumentasi sweetalert bisa dilihat di 
https://sweetalert2.github.io/

#### Membuat Confirm Prompt dengan Sweetalert2

`````` html
<script>
Swal.fire({
        title: 'Apakah Anda yakin?', // Judul pada dialog
        text: "Anda akan menghapus data ini!", // Text pada dialog
        icon: 'warning', // Tipe ikon, bisa warning, error, success, info
        showCancelButton: true, // Menampilkan tombol cancel
        confirmButtonColor: '#3085d6', // Warna tombol konfirmasi
        cancelButtonColor: '#d33', // Warna tombol cancel
        confirmButtonText: 'Ya, Hapus!' // Tombol Konfirmasi
    }).then((result) => {
        //lakukan sesuatu disini
        if(result.isConfirmed){
            // lakukan sesuatu disini jika tekan tombol 'Ya'
        }
})
</script>
``````
Implementasi pada tugas codeigniter4
`````` html
<!-- Tombol hapus pada halaman data_mahasiswa.php -->
<a href="#" url="mahasiswa/hapus/<?= $key['id']?>" id="delete">Hapus</a>

<!-- script sweetalert -->
<script>
    document.getElementById('delete').addEventListener('click', function() {
        event.preventDefault()
        const href = this.getAttribute('url');

        Swal.fire({
            title: 'Apakah Anda yakin?', // Judul pada dialog
            text: "Anda akan menghapus data ini!", // Text pada dialog
            icon: 'warning', // Tipe ikon, bisa warning, error, success, info
            showCancelButton: true, // Menampilkan tombol cancel
            confirmButtonColor: '#3085d6', // Warna tombol konfirmasi
            cancelButtonColor: '#d33', // Warna tombol cancel
            confirmButtonText: 'Ya, Hapus!' // Tombol Konfirmasi
        }).then((result) => {
            //lakukan sesuatu disini
            if(result.isConfirmed){
                // lakukan sesuatu disini jika tekan tombol 'Ya'
                window.location = href
            }
        })
    })
</script>
``````
