# Master Prompt — GitHub Profile README Design

## Tujuan

Buat atau redesign **GitHub Profile README (`README.md`)** agar terlihat profesional, modern, rapi, informatif, dan memiliki visualisasi aktivitas GitHub yang terinspirasi dari referensi video yang diberikan.

README ini harus digunakan pada **special profile repository** GitHub, yaitu repository yang memiliki nama **sama persis dengan username GitHub**.

Contoh:

```text
github.com/USERNAME
        ↓
USERNAME/USERNAME
        └── README.md
```

Jangan membuat website terpisah. Fokus utama adalah **README.md yang tampil langsung pada halaman profil GitHub**.

---

# 1. Prinsip Desain

Gunakan prinsip berikut:

- Modern dan profesional.
- Minimalis tetapi tetap visual.
- Tidak terlalu banyak emoji.
- Spacing antarbagian harus jelas.
- Mudah dibaca di desktop maupun mobile.
- Jangan membuat README terlalu panjang tanpa alasan.
- Semua informasi harus berasal dari data pengguna.
- Jangan mengarang pengalaman, proyek, sertifikasi, statistik, atau kontribusi.
- Jika data belum tersedia, gunakan placeholder yang jelas atau hilangkan bagian tersebut.
- Gunakan bahasa Inggris untuk tampilan utama README agar cocok untuk profil GitHub internasional.
- Gunakan HTML Markdown hanya jika diperlukan untuk layout.
- Hindari layout yang mudah rusak pada GitHub Mobile.
- Semua gambar eksternal harus berasal dari layanan yang stabil dan relevan.

---

# 2. Struktur Utama README

Gunakan urutan berikut:

```text
1. Hero / Header
2. About Me
3. Tech Stack
4. GitHub Statistics
5. GitHub Trophies
6. Contribution Activity
7. Contribution Heatmap / Snake
8. Featured Projects
9. Experience
10. Education
11. Currently Learning / Focus
12. Connect With Me
13. Footer
```

---

# 3. Hero / Header

Buat bagian pembuka yang sederhana dan kuat.

Contoh struktur:

```text
Hi 👋, I'm [NAME]

[Short professional headline]

[Portfolio] · [LinkedIn] · [Email] · [GitHub]
```

Headline harus menjelaskan identitas profesional pengguna secara singkat.

Contoh:

```text
Informatics Student | Web & Mobile Developer | Technology Enthusiast
```

Jangan menggunakan klaim yang tidak didukung data pengguna.

---

# 4. About Me

Buat section:

```md
## 👨‍💻 About Me
```

Isi maksimal 3–5 bullet atau satu paragraf pendek.

Prioritaskan:

- status pendidikan
- bidang yang diminati
- teknologi utama
- jenis proyek yang dikerjakan
- tujuan profesional

Jangan membuat paragraf panjang.

---

# 5. Tech Stack

Buat section:

```md
## 🛠️ Tech Stack
```

Kelompokkan teknologi agar tidak menjadi satu daftar panjang.

Struktur:

```text
Languages
Frontend
Mobile
Backend
Database
Tools
```

Contoh:

```text
Languages:
C · Java · Python · Dart · JavaScript

Frontend:
HTML · CSS · React

Mobile:
Flutter · Android

Backend:
PHP · REST API

Database:
MySQL · Firebase

Tools:
Git · GitHub · VS Code
```

Gunakan badge/icon yang konsisten.

Jangan memasukkan teknologi hanya karena pernah menyentuhnya sekali. Prioritaskan teknologi yang benar-benar dikuasai atau sedang digunakan.

---

# 6. GitHub Statistics

Buat section:

```md
## 📊 GitHub Statistics
```

Gunakan statistik seperti:

- total contributions
- commits
- repositories
- pull requests
- issues
- stars

Jika menggunakan layanan eksternal, pilih layanan yang aktif dan dapat dipercaya.

Layout yang disarankan:

```text
┌──────────────────────┐  ┌──────────────────────┐
│ GitHub Stats         │  │ Top Languages        │
│                      │  │                      │
│ Contributions        │  │ JavaScript           │
│ Commits              │  │ Dart                 │
│ PRs                  │  │ Java                 │
│ Issues               │  │ Python               │
└──────────────────────┘  └──────────────────────┘
```

Jangan menampilkan terlalu banyak kartu statistik karena dapat membuat README terlihat penuh.

---

# 7. GitHub Trophies

Buat section:

```md
## 🏆 GitHub Trophies
```

Jika menggunakan layanan trophy, tampilkan secara horizontal atau responsive.

Jangan membuat trophy palsu.

---

# 8. Contribution Activity

Ini adalah bagian visual utama yang terinspirasi dari video referensi.

Buat section:

```md
## 📈 Contribution Activity
```

Tujuan:

Menampilkan aktivitas kontribusi pengguna dalam bentuk **line chart** atau visualisasi aktivitas yang dinamis.

Konsep:

```text
Contributions
│
│              ╭──╮
│        ╭────╯  ╰──╮
│   ╭────╯           ╰──╮
│───╯                    ╰────
└──────────────────────────────
             Time
```

Ketentuan:

- Data harus berasal dari aktivitas GitHub nyata.
- Jangan membuat data kontribusi palsu.
- Grafik harus responsive.
- Jangan menggunakan grafik yang terlalu tinggi.
- Hindari dekorasi berlebihan.
- Jika layanan chart eksternal tidak stabil, gunakan alternatif yang lebih sederhana.

---

# 9. Contribution Heatmap / Snake

Buat section:

```md
## 🐍 Contribution Journey
```

Gunakan **GitHub Contribution Snake** sebagai visualisasi tambahan.

Konsep:

```text
Contribution Grid

░ ░ ▒ ▓ ▓ ░ ░ ▒ ▓ ▓
░ ▒ ▓ ▓ ░ ░ ▒ ▓ ▓ ░
▒ ▓ ▓ ░ ░ ▒ ▓ ▓ ░ ▒
      🐍 → → →
```

Implementasi yang direkomendasikan menggunakan:

```text
Platane/snk
```

dengan GitHub Actions.

Output yang dihasilkan:

```text
github-contribution-grid-snake.svg
```

Workflow:

```text
GitHub Contributions
        ↓
GitHub Actions
        ↓
Platane/snk
        ↓
Generated SVG
        ↓
README.md
```

---

# 10. Snake Workflow

Buat file:

```text
.github/
└── workflows/
    └── snake.yml
```

Workflow harus:

1. berjalan otomatis melalui `schedule`
2. dapat dijalankan manual melalui `workflow_dispatch`
3. membaca username repository owner
4. menghasilkan SVG snake
5. menyimpan output pada branch `output`
6. menggunakan `GITHUB_TOKEN`
7. tidak menggunakan token pribadi jika tidak diperlukan

Contoh konsep:

```yaml
name: Generate Contribution Snake

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest

    permissions:
      contents: write

    steps:
      - name: Generate Snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Publish
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Sebelum menggunakan dependency/action tersebut, verifikasi bahwa versi yang digunakan masih valid dan kompatibel dengan GitHub Actions.

---

# 11. Dark Mode

README harus mendukung dark/light mode jika memungkinkan.

Gunakan:

```html
<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="DARK_IMAGE_URL"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="LIGHT_IMAGE_URL"
  />
  <img
    src="LIGHT_IMAGE_URL"
    alt="GitHub contribution activity"
  />
</picture>
```

Pastikan gambar tidak rusak jika salah satu mode tidak tersedia.

---

# 12. Featured Projects

Buat section:

```md
## 🚀 Featured Projects
```

Tampilkan maksimal 3–6 proyek terbaik.

Format:

```text
Project Name
Short description

Tech:
React · Node.js · MySQL

[Repository] [Live Demo]
```

Prioritaskan proyek yang:

- selesai atau usable
- relevan dengan bidang pengguna
- memiliki repository yang rapi
- memiliki README
- memiliki demo jika tersedia

Jangan memasukkan semua repository.

---

# 13. Experience

Buat section:

```md
## 💼 Experience
```

Gunakan format:

```text
Role / Activity
Organization
Period

Short description
```

Untuk pengguna, data pengalaman dapat berasal dari:

- internship / PKL
- project
- organization
- volunteer
- freelance

Jangan melebih-lebihkan tanggung jawab.

---

# 14. Education

Buat:

```md
## 🎓 Education
```

Format:

```text
[Program]
[University]
[Period]
```

Tambahkan detail hanya jika relevan.

---

# 15. Currently Learning / Focus

Buat:

```md
## 🌱 Currently Learning
```

Isi 3–5 item yang benar-benar sedang dipelajari.

Contoh:

```text
- Advanced Flutter
- React & modern frontend
- Backend development
- Cloud deployment
- Software architecture
```

Jangan mengklaim skill sebagai mastered jika masih dipelajari.

---

# 16. Connect With Me

Buat:

```md
## 📫 Connect With Me
```

Gunakan:

```text
Portfolio
GitHub
LinkedIn
Email
```

Jangan memasukkan link yang tidak tersedia.

---

# 17. Footer

Gunakan footer sederhana.

Contoh:

```text
Thanks for visiting my profile!

⭐ Feel free to explore my repositories.
```

Jangan menggunakan terlalu banyak animasi.

---

# 18. Layout Final

Struktur final harus kira-kira:

```text
╔══════════════════════════════════════════════╗
║              👋 HI, I'M NAME                ║
║         Professional Headline               ║
║       Portfolio · LinkedIn · GitHub         ║
╚══════════════════════════════════════════════╝

## 👨‍💻 About Me
Short professional introduction

## 🛠️ Tech Stack
Languages
Frontend
Mobile
Backend
Database
Tools

## 📊 GitHub Statistics
┌──────────────┐ ┌──────────────┐
│ GitHub Stats │ │ Top Languages│
└──────────────┘ └──────────────┘

## 🏆 GitHub Trophies
[Trophy cards]

## 📈 Contribution Activity
[Dynamic contribution line/activity chart]

## 🐍 Contribution Journey
[Animated contribution snake]

## 🚀 Featured Projects
[Project 1] [Project 2] [Project 3]

## 💼 Experience
[Experience]

## 🎓 Education
[Education]

## 🌱 Currently Learning
[Learning topics]

## 📫 Connect With Me
[Portfolio] [GitHub] [LinkedIn] [Email]

──────────────────────────────────────────────
        Thanks for visiting my profile!
```

---

# 19. Important Technical Rules

Saat menghasilkan implementasi:

1. README harus valid di GitHub.
2. Jangan menggunakan JavaScript karena GitHub README tidak menjalankan JavaScript.
3. Jangan menggunakan CSS eksternal untuk layout utama.
4. Gunakan Markdown + HTML yang didukung GitHub.
5. Jangan menggunakan `<script>`.
6. Jangan mengandalkan iframe.
7. Semua gambar harus memiliki `alt`.
8. Gunakan URL yang benar-benar valid.
9. Jangan membuat statistik palsu.
10. Jangan membuat contribution palsu.
11. Jangan menggunakan token pribadi jika `GITHUB_TOKEN` sudah cukup.
12. Workflow harus memiliki permission yang diperlukan.
13. Pastikan branch output dapat ditulis oleh GitHub Actions.
14. Pastikan nama repository profile sama dengan username.
15. Pastikan semua action/dependency menggunakan versi yang masih tersedia.
16. Jika layanan eksternal gagal, README harus tetap memiliki fallback yang masuk akal.

---

# 20. Responsive Design

README harus tetap terlihat bagus pada:

- Desktop
- Laptop
- Tablet
- GitHub Mobile

Jangan membuat tabel dengan terlalu banyak kolom.

Untuk statistik:

```html
<p align="center">
  <img ... />
  <img ... />
</p>
```

Tetapi jika dua gambar menyebabkan overflow pada layar kecil, ubah menjadi layout vertikal.

---

# 21. Data Pengguna

Sebelum menghasilkan README final, kumpulkan atau gunakan data berikut jika tersedia:

```text
GitHub username:
Full name:
Headline:
University:
Major:
Location:
About:
Programming languages:
Frontend:
Backend:
Mobile:
Database:
Tools:
Featured projects:
Experience:
Education:
Current learning:
Portfolio:
LinkedIn:
Email:
Other links:
```

Jika informasi belum tersedia, jangan mengarang.

---

# 22. Output yang Diminta

Ketika prompt ini dijalankan, hasil akhirnya harus menyediakan:

```text
README.md
.github/workflows/snake.yml
```

Jika diperlukan:

```text
assets/
```

atau file konfigurasi tambahan.

Jelaskan:

1. file harus diletakkan di mana
2. repository mana yang digunakan
3. cara menjalankan GitHub Action
4. cara memeriksa hasil snake
5. cara mengganti username
6. cara mengganti warna/theme
7. cara memperbaiki jika workflow gagal

---

# 23. Target Visual

Target desain:

```text
Professional
      +
Minimal
      +
Developer-focused
      +
Data visualization
      +
GitHub-native
```

Jangan membuatnya terlihat seperti dashboard perusahaan.

README harus tetap terasa seperti **personal developer profile**, bukan website marketing.

---

# 24. Prinsip Anti-Fake

Ini wajib.

Contribution graph, stats, achievements, project count, commit count, dan aktivitas lainnya harus menggambarkan data nyata.

Jangan:

- membuat commit palsu
- mengubah tanggal commit untuk memanipulasi grafik
- membuat statistik palsu
- membuat project palsu
- membuat achievement palsu

Visualisasi boleh dibuat menarik, tetapi **datanya harus tetap jujur**.

---

# 25. Master Instruction

Bertindak sebagai **GitHub Profile README Designer + GitHub Actions Engineer**.

Analisis seluruh data pengguna sebelum membuat desain.

Kemudian:

1. Tentukan informasi paling relevan.
2. Buat hierarchy README yang jelas.
3. Buat desain visual yang modern.
4. Buat README.md lengkap.
5. Buat workflow Contribution Snake.
6. Integrasikan statistik GitHub.
7. Integrasikan contribution activity visualization jika memungkinkan.
8. Tambahkan dark/light mode.
9. Optimalkan mobile readability.
10. Validasi Markdown dan HTML.
11. Validasi workflow YAML.
12. Pastikan tidak ada data yang dibuat-buat.
13. Jelaskan lokasi setiap file.
14. Berikan langkah instalasi dan penggunaan.
15. Jika ada dependency eksternal, gunakan versi yang valid dan jelaskan kegunaannya.
16. Jangan mengubah contribution GitHub asli.
17. Jangan membuat sistem yang memalsukan aktivitas GitHub.

Prioritas:

```text
Accuracy
   ↓
Functionality
   ↓
Readability
   ↓
Visual Quality
   ↓
Decoration
```

Hasil akhir harus siap ditempatkan pada **GitHub Profile README** dan dapat dipelihara dengan mudah.
