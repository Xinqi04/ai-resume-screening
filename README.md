# CVInsight

Assignment ini saya kerjakan dalam satu notebook `notebooks/RizaAnwarFadil_AIEngineer_SKBatch2.ipynb`: PDF dibaca, informasi kandidat disusun ke JSON, lalu dibandingkan dengan job requirement dari file teks. Gemini dipakai untuk ekstraksi dan pencocokan; hasilnya berupa bahan review, bukan keputusan otomatis.

## Alur dan hasil

1. PyMuPDF mencoba membaca teks PDF secara lokal. Jika teksnya tidak cukup terbaca, PDF dikirim ke Gemini untuk ditranskripsikan.
2. Gemini mengambil nama (jika tertulis), pendidikan, keahlian, pengalaman, sertifikasi, dan kutipan pendukung. Status pendidikan hanya ditentukan dari petunjuk yang tertulis di CV.
3. Gemini memecah job requirement menjadi butir, lalu memberi status `match`, `partial`, `not_found`, atau `uncertain`, disertai bukti dan catatan.
4. Notebook mencari kembali kutipan pada teks sumber. Pemeriksaan ini memastikan kutipan ada, tetapi tidak memastikan maknanya benar-benar mendukung klaim.
5. Hasil JSON ditampilkan di notebook dan dibuatkan laporan PDF bernama `Laporan_Kecocokan_NamaKandidat_YYYY-MM-DD_HH-MM-SS_WIB.pdf`.

Overlap tanggal kerja tidak dianggap masalah dengan sendirinya karena beberapa pekerjaan dapat berjalan bersamaan. Tanggal masa depan dinilai terhadap tanggal saat notebook dijalankan.

## Menjalankan

Gunakan Python 3.11 atau lebih baru. Dari folder proyek, jalankan:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
```

Isi `GEMINI_API_KEY` di `.env`. Model `gemini-3.1-flash-lite-preview` sudah diatur di notebook. Letakkan satu PDF CV di folder `data/`; notebook akan memilihnya. Jika ada lebih dari satu PDF, pindahkan file lain terlebih dahulu. Job requirement dibaca dari `data/job_requirements.txt`; ubah file itu sebelum menjalankan notebook dari atas ke bawah.

PDF dibatasi hingga 10 MB. Ekstraksi profil memakai maksimal 30.000 karakter teks CV dan pencocokan maksimal 12.000 karakter job requirement; laporan akan mencatat jika batas tersebut terlewati. Pastikan kuota Gemini tersedia. Jangan mengaktifkan billing berbayar hanya untuk assignment ini.

## Cara meninjau hasil

Periksa kutipan di PDF asli, terutama untuk status `match`. `not_found` berarti bukti belum ditemukan di CV yang diberikan, bukan berarti kandidat tidak memiliki kemampuan tersebut. Tinjau juga status pendidikan, syarat wajib, caveat, dan langkah berikutnya.

Pemeriksaan otomatis memvalidasi bentuk JSON dan mencari kutipan secara literal. Untuk evaluasi sederhana, cek apakah kutipan benar, apakah status tiap requirement masuk akal, dan apakah caveat memang didukung CV atau lowongan. Penilaian performa yang lebih kuat memerlukan beberapa pasangan CV dan lowongan dengan label acuan dari reviewer.

## Privasi

Isi CV dikirim ke Gemini saat analisis dijalankan; file scan dikirim sebagai PDF. Notebook juga menampilkan teks CV dan menyimpan output cell saat dijalankan. Hapus output sebelum membagikan notebook. Repository ini tidak menyertakan laporan hasil kandidat agar data CV tidak ikut terpublikasi; JSON dan PDF dibuat saat notebook dijalankan. `.gitignore` mengecualikan `.env`, PDF di `data/`, laporan, dan file sementara. Jangan menambahkan CV atau laporan kandidat ke repository.

## Catatan penggunaan AI

OpenAI Codex membantu menyusun dan meninjau notebook serta dokumentasi. Gemini digunakan oleh notebook untuk ekstraksi dan pencocokan. Hasil tetap perlu saya periksa sebelum dipakai.
