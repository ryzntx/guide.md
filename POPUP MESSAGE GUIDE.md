### POP-UP Message with alert from javascript without any library

perhatikan baris kode dibawah ini

```````` php
return redirect()->to('mahasiswa');
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
->  return redirect()->to('mahasiswa')->with('success', 'Masukan pesan disini!');
->  return redirect()->to('matakuliah')->with('success', 'Masukan pesan disini!');
````````

-------------------------------------
### MENAMPILKAN PESAN DI TAMPILAN
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
`````` html
<script>
    <?php if(session('success')) { ?>
        alert('<?= session('success') ?>')
    <?php } ?>
</script>
``````
###### PENJELASAN

pada baris kode `<?php if(session('success')) { ?>` disini dilakukan pengecekan key dari session yang nama key nya 'success'
Key ini dari mana?? Key ini berasal dari sebuah fungsi 'with' di controller yang ada pada baris kode 
`````` php
return redirect()->to('mahasiswa')->with('success', 'Pesan disini!');
                                        ^^^^^^^^^^
                                    Inilah key nya
``````

lalu pada baris kode `alert('<?= session('success') ?>')` ini berfungsi untuk menampilkan pop-up dan pesan yang dikirim dari controller
pesan nya dapet dari mana?? pesan nya kan dari sebuah fungsi `with` yang ada di controller yang ada pada baris kode 
`````` php
return redirect()->to('mahasiswa')->with('success', 'Pesan disini!');
                                                      ^^^^^^^^^^
                                                    Inilah pesan nya
``````

contoh kode yang di file template.php

`````` html
<script>
    <?php if(session('success')) { ?>
        alert('<?= session('success') ?>')
    <?php } ?>
</script>
</body>
``````

contoh kode yang di folder controller file mahasiswa.php

`````` php
public function simpan() { // pada function simpan
    return redirect()->to('mahasiswa')->with('success', 'Data berhasil di simpan!');
}
public function update() { // pada function update
    return redirect()->to('mahasiswa')->with('success', 'Data berhasil di perbaharui!');
}
public function delete() { // pada function delete
    return redirect()->to('mahasiswa')->with('success', 'Data berhasil di hapus!');
}

``````

contoh kode yang di folder controller file matakuliah.php

`````` php
public function simpan() { // pada function simpan
    return redirect()->to('matakuliah')->with('success', 'Data berhasil di simpan!');
}
public function update() { // pada function update
    return redirect()->to('matakuliah')->with('success', 'Data berhasil di perbaharui!');
}
public function delete() { // pada function delete
    return redirect()->to('matakuliah')->with('success', 'Data berhasil di hapus!');
}
  
