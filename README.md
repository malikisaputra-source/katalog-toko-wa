# Katalog Toko + Checkout WhatsApp

Website katalog toko yang ringan dan statis. Pembeli memilih barang, mengisi keranjang, lalu menekan **Pesan via WhatsApp**. Pesanan terkirim ke nomor admin dalam format yang rapi (daftar barang, varian, subtotal, ongkir, total, nama, alamat).

Tanpa backend, tanpa database, gratis di-hosting di GitHub Pages atau Vercel.

## Fitur
- Semua data toko & produk di **satu berkas `produk.js`**.
- **Opsional**: ambil produk dari **Google Sheet** yang dipublikasikan sebagai CSV, jadi admin cukup edit spreadsheet.
- **Cari**, filter **kategori**, dan **urutkan** (harga terendah/tertinggi, nama).
- **Detail produk**: galeri beberapa gambar, pilihan varian (ukuran, warna, dll) dengan tambahan harga per opsi, jumlah, info stok.
- **Keranjang** tersimpan di browser (tidak hilang saat halaman ditutup).
- **Ongkir per kota** sederhana + **gratis ongkir** di atas nominal tertentu. Opsi "kota lain" akan meminta admin mengecek ongkir.
- **Mode gelap** mengikuti pengaturan HP, bisa diganti manual.
- **Gambar ilustrasi SVG** bawaan, jadi katalog langsung rapi sebelum punya foto. Bisa diganti foto asli kapan saja.
- Responsif HP, cepat (tanpa library).

## Cara menjalankan (pemula)
1. Unduh folder ini.
2. Klik ganda `index.html` untuk melihat di browser. (Fitur Google Sheet butuh dijalankan lewat server/hosting, misal `python3 -m http.server`.)
3. Buka `produk.js` dengan editor teks (VS Code/Notepad), lalu ubah:
   - `nama`, `slogan`
   - `wa`: nomor WhatsApp admin dengan format `628xxxxxxxxxx` (tanpa `+`, spasi, atau tanda hubung)
   - `ongkir`: daftar kota dan biayanya; `gratisOngkirMin` (isi `0` untuk mematikan)
4. Ganti isi `PRODUK`. Tiap produk punya `id` unik, `nama`, `kategori`, `harga`, `hargaCoret` (opsional), `label` (opsional, misal "Baru"), `stok` (`0` = habis), `deskripsi`, `varian`, `gambar`.
5. Simpan, muat ulang browser.

### Pakai foto asli
Buat folder `img/`, taruh fotonya, lalu tulis `gambar: ['img/kaos-hitam.jpg', 'img/kaos-krem.jpg']`. Foto persegi (1:1) ±800 px hasilnya paling rapi. Kalau ada varian `Warna`, urutan gambar mengikuti urutan opsi warna sehingga gambar ikut berganti saat warna dipilih.

### Pakai Google Sheet (opsional)
1. Buat sheet dengan kolom: `id,nama,kategori,harga,hargaCoret,deskripsi,varian,gambar,stok,label`.
   - `varian` contoh: `Ukuran:S,M,L;Warna:Hitam,Putih`
   - `gambar` contoh: `https://.../a.jpg|https://.../b.jpg` (kosongkan untuk ilustrasi otomatis)
2. **File → Bagikan → Publikasikan ke web** → pilih sheet → format **CSV** → Publikasikan. Salin link-nya.
3. Tempel di `produk.js` pada `sheetCSV: '...'`. Jika sheet gagal dimuat, katalog otomatis memakai data lokal.

## Deploy
**GitHub Pages**
1. Buat repository baru, unggah semua berkas (Add file → Upload files).
2. **Settings → Pages → Source: Deploy from a branch → main / (root)** → Save.
3. Tunggu 1–2 menit, situs tampil di `https://namakamu.github.io/nama-repo/`.

**Vercel**
1. Masuk ke vercel.com → **Add New → Project** → impor repo tadi (atau drag & drop folder).
2. Framework: **Other**, tanpa build command. Klik **Deploy**.

## Struktur folder
```
katalog-toko-wa/
├── index.html   # kerangka halaman
├── style.css    # tampilan, mode gelap, responsif
├── produk.js    # PENGATURAN TOKO & DATA PRODUK (ubah di sini)
├── app.js       # logika katalog, keranjang, pesan WA, gambar ilustrasi
├── meta.json, LICENSE, README.md, ss.png
```

## Ubah brand & warna
- Warna di `style.css` bagian `:root` (mode terang) dan `[data-tema=gelap]` (mode gelap). Ubah `--aksen` untuk warna utama brand.
- Huruf judul memakai font serif bawaan sistem (`--serif`); ganti sesukamu.
- Teks pembuka ("Belanja santai…") ada di `index.html`.
- Format pesan WhatsApp bisa diubah di fungsi `buatPesan` dalam `app.js`.

## Lisensi
MIT — bebas dipakai, diubah, dan dipakai untuk klien, asal menyertakan berkas LICENSE.

---
Dibuat oleh **Maliki Studio** — [malikisaputra.biz.id](https://malikisaputra.biz.id), follow TikTok/IG **@malikisaputra**
