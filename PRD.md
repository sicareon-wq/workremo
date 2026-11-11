# PRD — WorkRemo: Panduan Interaktif Freelance Remote AI Trainer (IT & Non-IT)

| | |
|---|---|
| **Produk** | WorkRemo — halaman web interaktif satu halaman (one-pager) |
| **Versi PRD** | v1.0 (draft untuk review) |
| **Status** | Menunggu persetujuan |
| **Teknologi** | HTML5 + CSS3 + JavaScript vanilla (tanpa framework, tanpa CDN eksternal) |
| **Prioritas fitur** | Alur (learning path & navigasi) dan animasi motion |

---

## 1. Latar Belakang

Pekerjaan freelance remote sebagai **AI Trainer** tumbuh cepat, baik untuk latar belakang **IT** (coding, RLHF, data engineering) maupun **non-IT** (anotasi data, penulisan konten, domain expert). Median tarif ±$40/jam (agregat 51 platform), namun informasi tentang *cara memulai*, *skill apa yang dibutuhkan*, dan *jalur belajarnya* tersebar dan tidak terstruktur.

## 2. Tujuan Produk

Memberikan **gambaran interaktif** yang memandu calon freelancer AI trainer memahami:
1. **Pengenalan** — apa itu AI trainer, pasar & peluangnya (IT vs non-IT).
2. **Skill umum** — kompetensi yang dibutuhkan per segmen.
3. **Tujuan & penerapan** — ke mana jalur ini bisa dibawa (karier, income, portofolio) dan di mana dipakai (platform, jenis tugas).
4. **Alur belajar** — roadmap bertahap dari nol sampai siap kerja, dengan estimasi durasi.

## 3. Target Pengguna

| Persona | Kebutuhan |
|---|---|
| Mahasiswa/fresh graduate IT | Ingin side income remote dengan skill coding |
| Profesional non-IT (guru, penulis, penerjemah) | Ingin memanfaatkan keahlian domain untuk kerja remote |
| Freelancer aktif | Ingin membandingkan segmen & naik level ke expert |

## 4. Ruang Lingkup

**In-scope (v1)**
- One-pager HTML5 responsif, 5 seksi: Hero + 4 seksi konten di atas.
- Roadmap alur belajar interaktif (fokus utama).
- Animasi motion berbasis CSS3 + IntersectionObserver.
- Data ilustratif berbasis riset pasar 2025–2026 (dengan catatan sumber).

**Out-of-scope (v1)**
- Backend, database, autentikasi.
- Library visualisasi eksternal (Chart.js dkk) — semua visual dibuat dengan HTML5/CSS/SVG murni.
- Multibahasa (v1 Bahasa Indonesia).

## 5. Struktur Halaman & Konten

### 5.1 Hero
- Judul + subjudul satu kalimat, CTA "Mulai Lihat Alur Belajar" (smooth-scroll ke seksi Alur).
- Animated counter (mis. "$40/jam median", "+34% premium skill AI", "28% full remote").

### 5.2 Pengenalan
- Penjelasan singkat peran AI trainer + perbandingan dua jalur: **IT** vs **Non-IT**.
- Layout: dua kartu berdampingan (slide-in dari kiri/kanan saat scroll).
- Tiap kartu: definisi, contoh pekerjaan, rentang upah ilustratif.

### 5.3 Skill Umum
- Daftar skill per segmen dengan *skill bar* yang terisi (width animation) saat masuk viewport.
  - IT: Python/JS dasar, pemahaman LLM & prompting, evaluasi kualitas kode, Git, dasar data.
  - Non-IT: menulis & merangkum, riset & fact-checking, keahlian domain, ketelitian anotasi, bahasa Inggris.
- Filter/klik segmen IT ↔ Non-IT (toggle) yang menganimasikan pergantian daftar.

### 5.4 Tujuan & Penerapan
- "Ke mana jalur ini membawa": kartu tujuan (income sampingan, karier AI, portofolio, remote lifestyle).
- "Di mana dipakai": daftar platform (Upwork, Mercor, Outlier, dll) dengan pangsa pasar ilustratif sebagai progress bar animasi.

### 5.5 Alur Belajar (fokus utama)
- Roadmap vertikal berbentuk **SVG path** yang "tergambar" mengikuti scroll (animasi `stroke-dashoffset`).
- 6 tahap (node) dengan konten:
  1. **Fondasi** (minggu 1–2) — pahami ekosistem AI training, pilih jalur IT/non-IT.
  2. **Skill Inti** (minggu 3–6) — latih skill segmen terpilih.
  3. **Portofolio Mini** (minggu 7–8) — contoh anotasi/evaluasi/prompt.
  4. **Daftar Platform & Kualifikasi** (minggu 9) — tes masuk platform.
  5. **Gig Pertama** (minggu 10–12) — tugas kecil, bangun rating.
  6. **Naik Level** (bulan 4+) — spesialisasi expert, tarif premium.
- Interaksi: klik node → panel detail expand (accordion dengan transisi height); node yang sudah "dilalui" scroll berubah warna (state visited).
- Tombol "Tandai progress" per tahap (disimpan di `localStorage`).

## 6. Fitur & Persyaratan Fungsional

| ID | Fitur | Prioritas | Kriteria Terima |
|---|---|---|---|
| F1 | Navigasi sticky + scroll-spy (seksi aktif ter-highlight) | Tinggi | Nav mengikuti posisi scroll tanpa jank |
| F2 | Progress bar baca di atas halaman | Tinggi | Lebar bar = persentase scroll |
| F3 | Scroll-reveal semua seksi (fade + translate) | Tinggi | Elemen muncul sekali, tidak flicker saat scroll naik-turun |
| F4 | Roadmap SVG tergambar mengikuti scroll | Tinggi | Garis progres mengikuti posisi viewport ±10% |
| F5 | Node roadmap klik → expand detail | Tinggi | Transisi halus ≤300ms, hanya satu terbuka |
| F6 | Toggle segmen IT/Non-IT (skill & kartu) | Sedang | Pergantian konten dianimasikan (fade/slide) |
| F7 | Animated counter di hero | Sedang | Angka menghitung naik saat pertama terlihat |
| F8 | Skill bar & progress bar platform terisi saat terlihat | Sedang | Animasi width dengan easing |
| F9 | Simpan progress roadmap di localStorage | Sedang | Status tetap setelah reload |
| F10 | CTA smooth-scroll | Rendah | Scroll halus ke target, offset nav |

## 7. Persyaratan Non-Fungsional

- **Performa**: satu file `index.html` (+ aset inline), tanpa request eksternal; animasi memakai `transform`/`opacity` (compositor-friendly), `prefers-reduced-motion` dihormati.
- **Responsif**: breakpoint mobile-first; roadmap berubah dari vertikal → garis sederhana di layar sempit.
- **Aksesibilitas**: kontras AA, fokus keyboard terlihat, `aria-expanded` pada node, struktur heading semantik.
- **Browser**: versi terbaru Chrome, Firefox, Edge, Safari.

## 8. Data Ilustratif

Angka upah/demand/pangsa pasar merupakan aproksimasi dari riset terbuka 2025–2026 (Upwork 2025, Mercor/ZipRecruiter, AITraining.jobs) dan ditandai "ilustratif" di footer halaman.

## 9. Metrik Keberhasilan

- Pengunjung mencapai seksi Alur Belajar ≥60% (scroll depth).
- Waktu di halaman ≥2 menit.
- Feedback kualitatif: alur belajar dianggap jelas (survei sederhana v1.1).

## 10. Milestone

| Tahap | Isi |
|---|---|
| M1 | PRD disetujui |
| M2 | Kerangka HTML5 + konten 4 seksi (statis) |
| M3 | Motion & alur: scroll-reveal, roadmap SVG, toggle, counter |
| M4 | Polish responsif + aksesibilitas, rilis ke `main` |

## 11. Risiko

| Risiko | Mitigasi |
|---|---|
| Animasi SVG roadmap rumit di mobile | Fallback garis sederhana + media query |
| Tanpa CDN = tanpa font/icon eksternal | Sistem font + emoji/SVG inline |
| Data ilustratif disangka resmi | Disclaimer eksplisit + tautan sumber |
