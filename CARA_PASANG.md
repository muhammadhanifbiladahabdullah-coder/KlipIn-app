# Cara Pasang Klipin (biar bisa dipakai mandiri, di luar Claude)

Folder ini isinya 3 file penting:
- `index.html` → tampilan aplikasinya
- `api/analyze.js` → "perantara" yang aman nyimpen API key & manggil Claude
- `package.json` → file konfigurasi kecil, biarkan saja

Total waktu: sekitar 10-15 menit, semua gratis (untuk pemakaian skala pribadi).

---

## Langkah 1 — Bikin API Key dari Anthropic

1. Buka **console.anthropic.com** di browser, daftar/login pakai email kamu.
2. Di menu sebelah kiri, cari **"Get API keys"** atau **"API Keys"**.
3. Klik **"Create Key"**, kasih nama bebas (misal: "klipin"), lalu klik buat.
4. **Salin key yang muncul** (formatnya diawali `sk-ant-...`) — simpan sementara di notes, karena ini **cuma ditampilkan sekali**, kalau hilang harus bikin baru.
5. Biasanya ada jatah kredit gratis di awal untuk akun baru. Kalau habis, kamu perlu isi saldo (isi sesuai kebutuhan, pemakaian tool ini per analisis biayanya sangat kecil, recehan).

⚠️ **Jangan pernah share key ini ke siapapun atau taruh di tempat publik** (grup chat, GitHub publik, dll) — anggap kayak PIN ATM.

---

## Langkah 2 — Bikin Akun Vercel

1. Buka **vercel.com**, klik **Sign Up**.
2. Paling gampang: daftar pakai akun **GitHub** kamu (kalau belum punya GitHub, bikin dulu di github.com, gratis).

---

## Langkah 3 — Upload Folder Ini ke GitHub

1. Di GitHub, klik **New repository** → kasih nama (misal `klipin-app`) → Create repository.
2. Di halaman repo yang baru dibuat, klik **"uploading an existing file"**.
3. Seret/upload semua isi folder `klipin-backend` ini (index.html, folder `api`, package.json) ke situ.
4. Klik **Commit changes**.

---

## Langkah 4 — Deploy ke Vercel

1. Di dashboard Vercel, klik **Add New → Project**.
2. Pilih repo GitHub `klipin-app` yang tadi dibuat → klik **Import**.
3. Biarkan semua pengaturan default → klik **Deploy**. Tunggu sekitar 1 menit.
4. Setelah selesai, JANGAN buka linknya dulu — kita perlu pasang API key dulu di langkah 5, kalau belum tombol AI-nya masih akan gagal.

---

## Langkah 5 — Pasang API Key di Vercel

1. Di halaman project Vercel kamu, klik tab **Settings → Environment Variables**.
2. Isi:
   - **Name**: `ANTHROPIC_API_KEY`
   - **Value**: tempel key yang kamu salin di Langkah 1 (`sk-ant-...`)
3. Klik **Save**.
4. Kembali ke tab **Deployments**, klik titik tiga (⋯) di deployment paling atas → **Redeploy** (supaya environment variable-nya kepakai).

---

## Selesai!

Buka URL yang dikasih Vercel (biasanya `https://klipin-app-xxxx.vercel.app`) — sekarang:
- ✅ Upload video dari galeri jalan normal (karena ini browser asli, bukan sandbox artifact)
- ✅ Tombol "Analisis dengan AI" jalan penuh (API key aman tersimpan di server Vercel, nggak kelihatan di kode browser)

## Kalau ada error
- **"ANTHROPIC_API_KEY belum diset"** → cek lagi Langkah 5, pastikan sudah redeploy setelah nambah env variable.
- **Analisis gagal / error dari Anthropic** → cek saldo/kredit API key kamu di console.anthropic.com.
