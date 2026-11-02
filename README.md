# aufa.eu.cc — versi Worker (login password, tampil instan)

**Jangan push folder ini mentah-mentah sebelum Worker di-deploy dan
`__WORKER_URL__` diganti dengan URL Worker yang sebenarnya.**
Kalau halaman ini di-push tanpa Worker, web pengunjung tidak akan
menampilkan QR (aman, tapi kosong).

## File

- `index.html` — halaman pengunjung. Hanya QR + tombol unduh + "scan qr".
  Tidak ada nama penyedia, tidak ada pemetaan, tidak ada nama file QR.
  QR diambil dari Worker `/qr`, unduhan dari `/qr-download`
  (nama file selalu generik `qris-aufa-eu-cc.png`).
- `ngadimin/index.html` + `ngadimin.html` — admin. Login password dulu,
  baru tampil pilihan. Label admin: `1` = SPAY, `2` = GOPAY, `3` = DANA.
- `qris-1.png` (SPAY, dulu A), `qris-2.png` (GOPAY, dulu B),
  `qris-3.png` (DANA, dulu C). Nama file sengaja angka saja, bukan nama penyedia.
- `CNAME` — `aufa.eu.cc`.

## Urutan deploy

Lihat `../worker/README-DEPLOY.md` selengkapnya. Ringkasnya:
1. Push dulu `qris-1/2/3.png` ke GitHub.
2. Buat KV namespace, deploy Worker (`worker/`), set secret `ADMIN_PASSWORD`.
3. Ganti `__WORKER_URL__` di `index.html` dan `ngadimin/*` dengan URL Worker.
4. Push halaman utama + admin ke GitHub.
5. Uji: login di `/ngadimin`, Simpan, web utama langsung tampil QR baru.

## Yang berubah dari versi sebelumnya

- Dulu: admin simpan lewat token GitHub ke `config.json`, web menunggu
  rebuild GitHub Pages (~1 menit), admin tidak pakai password.
- Sekarang: admin login password saja, simpan ke Cloudflare KV lewat
  Worker, web langsung tampil tanpa rebuild. `config.json` tidak lagi
  dipakai halaman utama.
