# CVInsight

Notebook untuk membaca CV PDF dan mencocokkannya dengan job requirement berbentuk teks menggunakan Gemini.

## Alur

1. PyMuPDF membaca teks PDF secara lokal. Jika teks kurang terbaca, notebook mengirim PDF ke Gemini untuk ditranskripsikan.
2. Gemini menyusun profil kandidat dan kutipan bukti dalam JSON.
3. Gemini membandingkan profil dengan job requirement dan memberi status `match`, `partial`, `not_found`, atau `uncertain`.
4. Notebook memeriksa kutipan terhadap teks CV, menampilkan JSON, lalu membuat laporan PDF.

## Menjalankan

Gunakan Python 3.11 atau lebih baru. Dari folder proyek, jalankan: 

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
```

Isi `GEMINI_API_KEY` di `.env`. Model `gemini-3.1-flash-lite-preview` sudah ditetapkan di notebook. Letakkan satu CV PDF di folder `data/` dan sesuaikan job requirement di `data/job_requirements.txt`. Jika ada lebih dari satu PDF di folder `data/`, pindahkan file lain terlebih dahulu.

Buka `notebooks/RizaAnwarFadil_AIEngineer_SKBatch2.ipynb`, lalu jalankan cell dari atas ke bawah. PDF laporan dan JSON muncul setelah analisis selesai. Laporan disimpan di `reports/` dengan nama kandidat dan waktu pembuatan.

CV dibaca dari folder `data/`, sedangkan laporan PDF disimpan di `reports/`. Keduanya tidak dikecualikan dari Git.

