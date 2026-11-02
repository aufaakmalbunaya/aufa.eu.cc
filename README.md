# aufa.eu.cc — QRIS + Admin /ngadimin

Situs statis GitHub Pages (branch `main`, root `/`, custom domain `aufa.eu.cc`).

## File

- `index.html` — halaman web pengunjung. QRIS hanya tampil kalau `config.json` memilih A, B, atau C. Gaya terang dan bersih, terinspirasi situs personal devrangga.dev dan hidaffa.com (headline besar, ruang putih lega, kartu putih berbayang lembut, animasi masuk halus) — isinya tetap payment QRIS, bukan meniru konten mereka. Di bawah QR ada tombol **Unduh QRIS** yang mengunduh file PNG QRIS yang sedang tampil (`qris-A/B/C-aufa-eu-cc.png`). Tombol ini ikut tersembunyi kalau QRIS belum diset.
- `config.json` — satu-satunya pengaturan: `{"selected": null}` = belum diset, web tidak menampilkan QRIS. `{"selected": "A"}` (atau `"B"` / `"C"`) = tampilkan QRIS itu.
- `qris-A.png`, `qris-B.png`, `qris-C.png` — QRIS v2 yang dipilih user (A = QRIS lama di web, B = lampiran pertama, C = lampiran kedua).
- `ngadimin/index.html` dan `ngadimin.html` — halaman admin, bisa dibuka lewat `https://aufa.eu.cc/ngadimin/` (atau `/ngadimin.html`). Isinya sama, gayanya diselaraskan dengan web utama. Setiap kartu QRIS di admin juga punya tautan unduh, begitu juga pratinjau dan QRIS yang sedang tampil.
- `CNAME` — `aufa.eu.cc`.

## Cara admin mengatur QRIS

1. Buka `https://aufa.eu.cc/ngadimin/`.
2. Klik QRIS A / B / C, atau **Kosongkan** kalau tidak mau menampilkan QRIS.
3. Simpan dengan salah satu cara:
   - **Pakai token GitHub (langsung jadi):** buat fine-grained token di github.com/settings/tokens, hanya repo `aufaakmalbunaya/aufa.eu.cc`, permission `Contents: Read and write`. Tempel di halaman admin, tekan Simpan. Token hanya dikirim dari browser admin ke `api.github.com`, tidak ditulis ke repo, dan bisa dicabut kapan saja.
   - **Tanpa token:** tekan "unduh config.json", lalu upload/timpa `config.json` di repo lewat web GitHub.
4. Tunggu GitHub Pages deploy (biasanya sekitar 1 menit), lalu hard refresh di web.

## Keamanan — penting

`/ngadimin` itu hanya alamat yang tidak umum, **bukan** password. Siapa pun yang menebak alamat itu bisa melihat halaman admin, tapi tidak bisa mengubah yang tampil di web tanpa token GitHub di atas. Jangan pernah membagikan token, dan jangan menulis token ke file repo mana pun.

## Catatan deploy

File `qris.jpg` lama tidak lagi dipakai halaman ini dan tidak ada di folder ini. Kalau folder ini di-push menimpa repo, `qris.jpg` lama masih akan ada di repo sampai dihapus manual — itu tidak masalah karena tidak ditampilkan, tapi boleh dihapus supaya rapi.
