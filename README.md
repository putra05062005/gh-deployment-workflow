# Workflow Deployment ke GitHub Pages
# Proyek: Workflow Deployment Otomatis dengan GitHub Actions

Selamat datang di proyek workflow deployment otomatis! Proyek ini mendemonstrasikan cara membangun sebuah pipeline CI/CD (Continuous Integration/Continuous Deployment) sederhana untuk sebuah website statis menggunakan **GitHub Actions** dan **GitHub Pages**.

Tujuan utamanya adalah setiap kali ada perubahan pada file konten website (`index.html`), perubahan tersebut secara otomatis dipublikasikan ke website yang live tanpa perlu campur tangan manual.

## Konsep Kunci

Proyek ini dibangun di atas tiga teknologi inti dari ekosistem GitHub:

1.  **GitHub Pages**: Layanan hosting gratis dari GitHub yang mampu menayangkan file statis (HTML, CSS, JS) langsung dari sebuah repository sebagai sebuah website.

2.  **GitHub Actions**: Platform otomasi dari GitHub. Kita bisa menggunakannya untuk membuat alur kerja (workflow) kustom untuk membangun, menguji, dan melakukan deployment kode secara otomatis. "Robot" yang bekerja untuk kita ada di sini.

3.  **CI/CD (Continuous Integration & Continuous Deployment)**: Ini adalah praktik pengembangan modern yang kita implementasikan.
    -   **CI**: Setiap kali kode baru di-push, proses otomatis berjalan untuk memastikan kode tersebut terintegrasi dengan baik.
    -   **CD**: Jika integrasi berhasil, kode tersebut secara otomatis diterbitkan (deploy) ke lingkungan produksi (website live).

## Bagaimana Cara Kerjanya?

Keajaiban proyek ini terletak pada file instruksi workflow di `.github/workflows/deploy.yml`. Berikut adalah cara kerjanya secara rinci:

### 1. Pemicu (The Trigger)

Workflow ini tidak berjalan setiap saat. Ia hanya akan terpicu jika kondisi berikut terpenuhi:

-   Ada event `push` (misalnya, dari perintah `git push`).
-   Push tersebut terjadi pada branch `main`.
-   Perubahan yang di-push **harus menyertakan modifikasi pada file `index.html`**.

Jika hanya file lain (seperti `README.md` ini) yang diubah, workflow tidak akan berjalan. Ini memastikan kita hanya melakukan deployment saat konten website benar-benar berubah.

### 2. Proses (The Job & Steps)

Jika terpicu, sebuah "job" bernama `deploy` akan berjalan di mesin virtual Ubuntu. Job ini mengikuti langkah-langkah berikut:

1.  **Checkout Code**: Langkah pertama adalah mengunduh kode terbaru dari repository Anda ke dalam mesin virtual menggunakan `actions/checkout@v4`.

2.  **Setup Pages**: Lingkungan disiapkan secara khusus untuk proses deployment ke GitHub Pages menggunakan `actions/configure-pages@v5`.

3.  **Upload Artifact**: Semua file website kita (dalam kasus ini, hanya `index.html`) dibungkus menjadi sebuah "paket" atau artefak yang siap untuk di-deploy. Ini dilakukan oleh `actions/upload-pages-artifact@v3`.

4.  **Deploy to GitHub Pages**: Langkah terakhir adalah mengambil "paket" artefak tadi dan mempublikasikannya ke server GitHub Pages menggunakan `actions/deploy-pages@v4`. Setelah langkah ini selesai, website Anda akan diperbarui.

## Cara Menguji Workflow Ini

1.  Clone repository ini ke komputer lokal Anda.
2.  Lakukan perubahan apa pun pada file `index.html`.
3.  Lakukan `commit` dan `push` perubahan tersebut ke branch `main`.
    ```bash
    git add index.html
    git commit -m "Menguji perubahan pada konten website"
    git push
    ```
4.  Buka tab **"Actions"** pada repository GitHub untuk melihat workflow berjalan secara real-time.
5.  Setelah workflow selesai (centang hijau), kunjungi URL website Anda untuk melihat perubahan terbaru:
    [https://putra05062005.github.io/gh-deployment-workflow/](https://putra05062005.github.io/gh-deployment-workflow/)

##PROJECT URL
https://roadmap.sh/projects/github-actions-deployment-workflow
