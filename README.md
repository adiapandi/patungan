# PATUNGAN! 🧾

Struk digital buat patungan bareng temen" lo — split bill yang gampang dipakai buat urusan iuran makan-makan, ulang tahun temen kerja, dan acara bareng lainnya.

Dibuat dengan HTML/CSS/JS murni, tanpa build tool, tanpa backend wajib. Tinggal buka file-nya di browser.

## ✨ Fitur

- **Item per item, bukan cuma rata-rata** — setiap item bisa di-assign ke orang tertentu aja, gak harus dibagi rata semua orang
- **Bulk add peserta** — paste banyak nama sekaligus (pisahin pakai koma atau baris baru), gak perlu input satu-satu
- **Upload & scan struk otomatis** — foto struk belanja, item + harganya otomatis kebaca dan masuk ke daftar (pakai AI, opsional — lihat bagian [setup](#-opsional-setup-fitur-scan-struk-otomatis) di bawah)
- **Pajak, service, & diskon** — input nominal langsung (Rp), bukan persen, biar sesuai struk asli
- **Info rekening transfer** — tambahin bank/e-wallet, nomor rekening, dan atas nama, otomatis muncul di hasil, teks share, dan gambar export
- **Rincian detail per orang** — tap nama buat lihat item apa aja yang dia tanggung
- **Salin ke WhatsApp** — hasil rincian langsung ke-copy dalam format siap paste ke grup
- **Export ke gambar JPG** — hasil struk bisa disimpan sebagai gambar, kompatibel dengan Android maupun iOS (pakai Web Share API di iOS biar bisa langsung simpan ke Foto)

## 🚀 Cara Pakai

1. Buka `patungan.html` di browser (atau host di GitHub Pages / server kantor)
2. Isi nama acara (opsional)
3. Tambahin peserta
4. Tambahin item — bisa upload foto struk (otomatis kebaca) atau input manual, lalu atur item itu buat siapa aja
5. Isi pajak/service/diskon kalau ada, plus info rekening buat transfer
6. Pencet **GASKEUN, HITUNG!**
7. Share hasilnya ke grup lewat tombol **Salin buat Share ke WA** atau **Simpan sebagai Gambar**

## 📦 Struktur File

```
├── patungan.html   # Aplikasi utama — cukup buka file ini
├── worker.js       # (Opsional) Cloudflare Worker proxy buat fitur scan struk
└── README.md
```

## 🔧 (Opsional) Setup Fitur Scan Struk Otomatis

Fitur upload & scan struk pakai AI vision (Google Gemini, ada free tier) buat baca item + harga dari foto. Fitur ini **opsional** — tanpa setup ini, aplikasi tetap jalan normal lewat input manual.

Karena API key gak boleh ditaruh langsung di kode publik (bisa ke-expose & ke-revoke otomatis), fitur ini butuh proxy kecil biar key-nya aman:

1. Buat API key gratis di [Google AI Studio](https://aistudio.google.com/apikey)
2. Deploy `worker.js` ke [Cloudflare Workers](https://dash.cloudflare.com) (gratis, gak perlu kartu kredit)
3. Di Cloudflare, tambahin secret `GEMINI_API_KEY` (Settings → Variables and Secrets) isinya API key dari langkah 1
4. Di `patungan.html`, cari baris `PROXY_URL` di dalam fungsi `scanReceipt()`, ganti dengan URL Worker kamu
5. Selesai — tombol "Upload Struk" bakal jalan otomatis

## 🛠️ Tech Stack

- HTML, CSS, vanilla JavaScript — tanpa framework, tanpa build step
- [html2canvas](https://html2canvas.hertzen.com/) — buat export hasil jadi gambar
- Google Fonts: Archivo Black, Plus Jakarta Sans, Space Mono
- Google Gemini API (lewat Cloudflare Worker proxy) — buat fitur scan struk (opsional)

## 📝 Catatan

- Data (peserta, item, hasil hitung) cuma tersimpan selama sesi browser berjalan — refresh halaman = data ke-reset. Aplikasi ini gak pakai database/local storage.
- Fitur scan struk butuh koneksi internet dan proxy yang udah disetup (lihat bagian setup).

---

© 2026 adiapandi. All rights reserved.
