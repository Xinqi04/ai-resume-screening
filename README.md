# CVInsight

Notebook untuk membaca CV PDF dan mencocokkannya dengan job requirement berbentuk teks menggunakan Gemini.

## Cakupan prototype

- Menerima CV PDF dan mengekstrak informasi kandidat ke struktur JSON.
- Menetapkan schema utama untuk profil kandidat dan hasil pencocokan requirement.
- Memberikan rekomendasi beserta bukti, caveat, dan ketidakpastian; sistem tidak membuat keputusan hiring otomatis.
- Menyediakan prototype notebook yang menunjukkan alur tersebut berjalan dengan Gemini.

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

Isi `GEMINI_API_KEY` di `.env`. Model `gemini-3.1-flash-lite-preview` sudah ditetapkan di notebook. Notebook memakai `data/Budi_Doremi_CV.pdf` dan job requirement dari `data/job_requirements.txt`. CV ini dibuat untuk demonstrasi; notebook tidak memilih PDF lain secara otomatis.

Buka `notebooks/RizaAnwarFadil_AIEngineer_SKBatch2.ipynb`, lalu jalankan cell dari atas ke bawah. PDF laporan dan JSON muncul setelah analisis selesai. Laporan disimpan di `reports/` dengan nama kandidat dan waktu pembuatan.

CV contoh tersimpan di `data/Budi_Doremi_CV.pdf`; PDF contoh laporan ada di `report`.

