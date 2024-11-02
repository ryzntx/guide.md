### Validasi Input pada CodeIgniter 4

##### - Controller -

````` php
// Membuat peraturan pada setiap input yang masuk
$rules = [
    'nama' => 'required',
    'email' => 'required|valid_email|is_unique[t_users.email,id_user,' . $id . ']',
    'foto' => 'max_size[foto,1024]|is_image[foto]|mime_in[foto,image/jpg,image/jpeg,image/png]',
    ^^^^^       ^^^^^^^^^^^^^^^^^^^^^^
    input           rule / peraturan
];
// Kustom pesan yang akan di kirimkan jika ada bagian input yang error
$messages = [
    'nama' => [
        'required' => 'Nama lengkap harus diisi',
        ^^^^^^^^        ^^^^^^^^^^^^^
       nama aturan          isi pesan
    ],
    'email' => [
        'required' => 'Email harus diisi',
        'valid_email' => 'Email tidak valid',
        'is_unique' => 'Email sudah terdaftar',
    ],
    'foto' => [
        'max_size' => 'Ukuran gambar terlalu besar',
        'is_image' => 'File yang diupload bukan gambar',
        'mime_in' => 'File yang diupload bukan gambar',
    ],
];

// Melakukan validasi terhadap data dengan rule dan message yang di berikan
if (!$this->validate($rules, $messages)) {
    // Mengembalikan ke halaman sebelumnya dengan mengirimkan data error dan input
    return redirect()->to('MASUKAN URL NYA!')->withInput()->with('errors', $this->validator->getErrors());
}
`````
Untuk daftar rule / peraturan dapat dilihat pada dokumentasi CodeIgniter4
[Peraturan yang tersedia](https://codeigniter4.github.io/userguide/libraries/validation.html#available-rules)

untuk memasukan 2 aturan dalam 1 input yang masuk
bisa gunakan seperator (|) pada setiap rule nya
contoh: 
````` php
'nama' => 'required|alpha',
`````

pada input nama terdapat 2 rule/aturan yang digunakan


##### - VIEW -

Simpan kode dibawah ini ke tampilan form input atau di sesuaikan dengan lokasi yang di inginkan
````` php
<?php if (session()->getFlashdata('errors')): ?>
<div class="alert alert-danger">
    Ada kesalahan dalam pengisian form:
    <ul>
        <?php foreach (session()->getFlashdata('errors') as $error): ?>
            <li><?=$error?></li>
        <?php endforeach;?>
    </ul>
</div>
<?php endif;?>
`````

