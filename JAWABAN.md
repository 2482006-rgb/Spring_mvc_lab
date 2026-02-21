# Jawaban Week 4 Lab

## Latihan 1

### Eksperimen 1: @Controller vs @RestController
- /test/view → Menampilkan halaman HTML (view/template)
- /test/text → Menampilkan teks langsung di browser 
- Kesimpulan: - @Controller dipakai kalau kita mau menampilkan halaman (view/template HTML).
              - @RestController dipakai kalau kita mau mengirim data langsung ke browser (biasanya teks atau JSON), bukan halaman HTML.

### Eksperimen 2: Template Tidak Ada
- HTTP Status: 500
- Error: nternal Server Error

### Eksperimen 3: @RequestParam vs @PathVariable
| URL              | Hasil                  |
|------------------|------------------------|
| /greet           | selamat pagi mahasiswa |
| /greet?name=Budi | Selamat pagi Budi!     |
| /greet/Joedy     | Helo Joedy             |

### Pertanyaan Refleksi
1. - @Controller dipakai kalau kita mau balikin halaman HTML (biasanya pakai template seperti Thymeleaf).
   - @RestController dipakai kalau kita mau balikin data langsung (biasanya dalam bentuk JSON).
2. KARENA :
   - Tidak perlu bikin file HTML baru setiap fitur.
   - Kode jadi lebih rapi dan tidak duplikasi.
   - Kalau mau ubah desain, cukup ubah 1 file saja.
   - Lebih hemat waktu dan lebih profesional.
3. Karena kita pakai konsep pemisahan tugas (separation of concerns).
   - Controller → tugasnya terima request & kirim response
   Service → tugasnya ngatur logic / data
   - Kalau Controller langsung kelola ArrayList:
   Kode jadi berantakan
   Susah dikembangkan
   Tidak sesuai konsep arsitektur MVC
   Kalau suatu saat data pindah ke database (MySQL misalnya), kita cuma ubah di Service, Controller tidak perlu diubah.
4.  - model.addAttribute(...)
     → Dipakai di @Controller
     → Data dikirim ke HTML untuk ditampilkan 
    - return products
     → Dipakai di @RestController
     → Data dikirim langsung sebagai JSON 
5. Biasanya akan muncul error 400 (Bad Request) Artinya id harus angka (Long).
   Kalau kita isi abc, Spring tidak bisa mengubah string jadi angka → jadi error.
6.  - Lebih ringkas
    - Tidak berulang-ulang
    - Lebih mudah kalau mau ubah path
   Kalau suatu saat mau ubah jadi /items, cukup ubah 1 tempat saja.
7.  - Model di parameter method Controller : Ini adalah object untuk mengirim data ke HTML (View).
    - Folder model/ : Ini adalah bagian dari konsep MVC, tempat menyimpan struktur data.
    - Class Product : Ini juga disebut model, tapi maksudnya adalah representasi data (misalnya id, nama, harga).

## Latihan 2

### Eksperimen 1: Fragment Tidak Ada
   - Apakah error?:             [Ya] 
   - Error message:             [type=Internal Server Error, status=500].
   KESIMPULAN : Jika nama fragment salah, Thymeleaf akan menampilkan error (TemplateInputException) dan halaman tidak bisa dirender.
### Eksperimen 2: Static Resource
  - CSS masih bekerja?:         [Ya] 
  - Apakah halaman error?:      [Tidak]
  - Apakah CSS diterapkan?:     [Tidak] 
  KESIMPULAN : Kesimpulan: th:href="@{}" lebih baik karena Thymeleaf akan membantu mengelola path secara otomatis sesuai dengan context path aplikasi.
  Jadi lebih aman dan fleksibel. Jika file CSS tidak ada, halaman tetap bisa dibuka tetapi CSS tidak diterapkan karena file tidak ditemukan (404).

### Pertanyaan Refleksi
1. Kalau kita pakai fragment, navbar dan footer cukup dibuat satu kali saja, misalnya di file fragments/navbar.
    html dan fragments/footer.html.Lalu di halaman lain tinggal dipanggil.
    Kenapa ini enak?
        - Tidak perlu copy–paste navbar di setiap halaman
        - Kalau mau ubah menu, cukup ubah di satu tempat 
        - Kode jadi lebih rapi dan tidak berulang-ulang
        - Lebih mudah dirawat (maintenance)
2.  - Folder templates/ itu untuk file HTML yang diproses oleh Thymeleaf. Jadi biasanya dipakai untuk halaman yang ada datanya dari Controller.
    - Sedangkan folder static/ itu untuk file biasa seperti CSS, JavaScript, dan gambar. File di dalam static/ bisa langsung dibaca oleh browser.
    - CSS ada di static/ karena CSS itu cuma file tampilan biasa, tidak perlu diproses oleh Thymeleaf
3.  - th:replace itu artinya mengganti tag yang ada dengan isi fragment. Jadi tag lama hilang, diganti isi yang baru.
    - th:insert itu artinya memasukkan isi fragment ke dalam tag yang sudah ada. Jadi tag lamanya tetap ada.
       Sederhananya:
            th:replace → diganti total
            th:insert → dimasukkan ke dalam
4. Karena @{} itu otomatis menyesuaikan dengan alamat aplikasi (context path).
   Kalau nanti alamat aplikasi berubah, URL tetap aman dan tidak error.
   Jadi lebih fleksibel dan lebih aman dibanding tulis langsung /products misalnya.
5. Kalau langsung pakai new, memang bisa jalan, tapi itu bukan cara yang benar di Spring.
   Kalau pakai Dependency Injection (DI), Spring yang akan mengatur dan membuat object-nya. Itu lebih rapi, lebih mudah diatur, dan lebih mudah untuk testing.
   Jadi lebih baik pakai DI daripada buat object sendiri di dalam Controller.