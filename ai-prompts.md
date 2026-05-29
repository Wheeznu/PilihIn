# 🎬 Pilih.in — Gemini CLI Prompt Bertahap
> Referensi visual: StreamFlix UI (dark theme, sidebar kiri, navbar atas, hero banner, card grid)
> Stack: Vanilla HTML5 + CSS3 + JS ES6+ | No framework, no build tool

---

## 📋 CARA PAKAI

Jalankan setiap **TAHAP** secara berurutan di Gemini CLI.
Tunggu output setiap tahap selesai sebelum lanjut ke tahap berikutnya.
Setiap prompt sudah self-contained — Gemini tidak perlu mengingat konteks sebelumnya.

---

---

# ═══════════════════════════════════════
# TAHAP 1 — FONDASI: Struktur Folder + Design System
# ═══════════════════════════════════════

```
Buat fondasi project website streaming film "pilih.in" dengan struktur berikut.
Buat SEMUA file yang disebutkan — jangan ada yang terlewat.

## STACK
Vanilla HTML5 + CSS3 + JavaScript ES6+.
Tidak boleh ada: React, Vue, Angular, npm, TypeScript, Tailwind, SASS, build tool apapun.

## STRUKTUR FOLDER YANG HARUS DIBUAT

data/
└── initialData.json
frontend/
├── index.html
├── css/
│   ├── reset.css
│   ├── design-system.css
│   └── components/
│       ├── navbar.css
│       ├── sidebar.css
│       ├── button.css
│       ├── card.css
│       ├── modal.css
│       └── form.css
└── js/
    ├── main.js
    ├── router.js
    ├── state.js
    └── db/
        ├── DatabaseManager.js
        ├── Repository.js
        ├── Validator.js
        ├── init.js
        ├── repositories/
        │   ├── UserRepository.js
        │   ├── FilmRepository.js
        │   ├── FaqRepository.js
        │   ├── PricingRepository.js
        │   └── PromotionRepository.js
        └── services/
            └── AuthService.js

## SPESIFIKASI design-system.css

Buat file css/design-system.css dengan ISI PERSIS seperti ini:

### Import font di setiap HTML (instruksi, bukan kode CSS):
Setiap file HTML wajib import di <head>:
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Google+Sans+Flex:wght@100..900&display=swap" rel="stylesheet">

### CSS Variables (tulis semua ini di design-system.css):

:root {
  --font-family: 'Google Sans Flex', -apple-system, BlinkMacSystemFont, sans-serif;
  --sidebar-width: 220px;
  --navbar-height: 64px;
  --content-max-width: 1400px;

  /* Spacing */
  --space-xs: 4px; --space-sm: 8px; --space-md: 16px;
  --space-lg: 24px; --space-xl: 32px; --space-2xl: 48px; --space-3xl: 64px;

  /* Font size */
  --font-xs: 0.75rem; --font-sm: 0.875rem; --font-md: 1rem;
  --font-lg: 1.125rem; --font-xl: 1.25rem; --font-2xl: 1.5rem;
  --font-3xl: 2rem; --font-4xl: 2.5rem; --font-5xl: 3rem;

  /* Font weight */
  --fw-light: 300; --fw-regular: 400; --fw-medium: 500;
  --fw-semibold: 600; --fw-bold: 700; --fw-extrabold: 800;

  /* Border radius */
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px;
  --radius-xl: 16px; --radius-full: 9999px;

  /* Z-index */
  --z-base: 1; --z-sticky: 100; --z-navbar: 200;
  --z-modal: 300; --z-toast: 400; --z-tooltip: 500;

  /* Transition */
  --transition-fast: 0.15s ease; --transition-base: 0.25s ease; --transition-slow: 0.4s ease;

  /* Shadow */
  --shadow-sm: 0 1px 3px var(--shadow-color);
  --shadow-md: 0 4px 12px var(--shadow-color);
  --shadow-lg: 0 8px 24px var(--shadow-color);
  --shadow-xl: 0 16px 48px var(--shadow-color);
}

/* Dark Mode (default) */
:root, :root[data-theme="dark"] {
  --bg-primary: #121212; --bg-secondary: #181818;
  --bg-tertiary: #242424; --bg-card: #1e1e1e; --bg-hover: #2a2a2a;
  --text-primary: #ffffff; --text-secondary: #b3b3b3; --text-muted: #8a8a8a;
  --accent-primary: #1db954; --accent-secondary: #1ed760; --accent-dark: #14833b;
  --danger: #e22134; --warning: #f5c518; --info: #3498ff; --success: #1db954;
  --border-color: #353535; --shadow-color: rgba(0,0,0,0.45);
  --overlay-dark: rgba(0,0,0,0.65); --overlay-light: rgba(255,255,255,0.08);
}

/* Light Mode */
:root[data-theme="light"] {
  --bg-primary: #ffffff; --bg-secondary: #f7f7f7;
  --bg-tertiary: #ebebeb; --bg-card: #ffffff; --bg-hover: #e2e2e2;
  --text-primary: #121212; --text-secondary: #535353; --text-muted: #7a7a7a;
  --accent-primary: #1db954; --accent-secondary: #1ed760; --accent-dark: #14833b;
  --danger: #e22134; --warning: #f5c518; --info: #3498ff; --success: #1db954;
  --border-color: #d4d4d4; --shadow-color: rgba(0,0,0,0.12);
  --overlay-dark: rgba(0,0,0,0.12); --overlay-light: rgba(255,255,255,0.65);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { font-family: var(--font-family); font-size: 16px; }
body { background: var(--bg-primary); color: var(--text-primary); min-height: 100vh; }
a { color: inherit; text-decoration: none; }
img { max-width: 100%; display: block; }

## SPESIFIKASI reset.css
Browser normalization minimal — normalize heading sizes, remove list styles, box-sizing border-box global.

## SPESIFIKASI DatabaseManager.js
Class DatabaseManager:
- constructor(): inisialisasi localStorage dengan key 'pilih-in-db'
- getDB(): return parsed JSON dari localStorage
- saveDB(data): simpan data ke localStorage
- getCollection(name): return array koleksi
- saveCollection(name, data): simpan koleksi

## SPESIFIKASI Repository.js
Class Repository (base class):
- constructor(collectionName, dbManager)
- findAll(): return semua item
- findById(id): return item by id
- findWhere(predicate): return array item yang memenuhi kondisi
- create(data): buat item baru dengan auto-generate id, createdAt, updatedAt
- update(id, data): update item, set updatedAt
- delete(id): hapus item by id

## SPESIFIKASI AuthService.js
Class AuthService:
- login(email, password): validasi user, simpan session ke localStorage key 'pilih-in-session'
- logout(): hapus session
- getCurrentUser(): return user dari session atau null
- isLoggedIn(): return boolean
- requireAuth(): redirect ke login.html jika tidak login
- requireRole(role): redirect jika role tidak sesuai

## SPESIFIKASI init.js
Export semua repository instances:
export const repositories = {
  users: new UserRepository(dbManager),
  films: new FilmRepository(dbManager),
  faqs: new FaqRepository(dbManager),
  pricing: new PricingRepository(dbManager),
  promotions: new PromotionRepository(dbManager),
}
export const authService = new AuthService(repositories.users);

## SPESIFIKASI initialData.json
Buat data sample untuk:
- users: 3 user (1 admin role:"admin", 1 user biasa role:"user", 1 manager role:"manager")
  Password admin: "admin123", user biasa: "user123"
  Simpan password sebagai plain text (simulasi saja)
- films: 8 film dengan field: id, title, genre, year, rating, poster (gunakan picsum.photos URL), description, isPremium
- faqs: 6 FAQ dengan question & answer seputar layanan streaming
- pricing: 3 paket (Basic Rp29.000, Standard Rp49.000, Premium Rp89.000) dengan fitur masing-masing
- promotions: 3 promo aktif dengan kode voucher, diskon persen, tanggal berlaku

## SPESIFIKASI router.js
Client-side router sederhana:
- Routing berbasis hash (#/home, #/login, dll)
- navigate(path): ganti hash
- onRouteChange(callback): listen hashchange event
- getCurrentRoute(): return current hash path

## SPESIFIKASI state.js
App state global:
- currentUser: null atau object user
- currentPage: string
- theme: 'dark' | 'light'
- setTheme(theme): set data-theme di <html>, simpan ke localStorage 'pilih-in-theme'
- getTheme(): return saved theme atau 'dark'

## SPESIFIKASI main.js
App initialization:
- Load theme dari localStorage
- Init database (seed data jika belum ada)
- Init router
- Export app state

## SPESIFIKASI index.html (entry point)
HTML sederhana yang redirect ke pages/main/home.html atau login.html tergantung session.
```

---

---

# ═══════════════════════════════════════
# TAHAP 2 — KOMPONEN REUSABLE: Navbar + Sidebar
# ═══════════════════════════════════════

```
Lanjutkan project pilih.in. Buat komponen NAVBAR dan SIDEBAR yang akan digunakan
di SEMUA halaman website. Ini adalah komponen terpenting karena dipakai di mana-mana.

## REFERENSI VISUAL
Desain seperti StreamFlix/Netflix:
- Sidebar kiri: lebar 220px, background gelap (#181818), logo di atas, navigasi vertikal
- Navbar atas: tinggi 64px, background semi-transparan atau solid gelap, logo di kiri, nav links di tengah, search + avatar di kanan
- Sidebar collapsed di mobile, tampil penuh di desktop (>1024px)

## FILE YANG HARUS DIBUAT

### 1. frontend/css/components/navbar.css
Styling navbar dengan CSS variables dari design-system.css.
Navbar fixed di top, z-index: var(--z-navbar).
Berisi: logo kiri, nav links tengah (Beranda/Film/Serial TV/Daftar Saya), search bar + avatar kanan.
Search bar dengan icon kaca pembesar, border rounded, expand on focus.
Avatar dengan dropdown menu (Profile, Settings, Logout).
Tombol theme toggle (icon matahari/bulan).
Responsive: di mobile sembunyikan nav links, tampilkan hamburger menu.

### 2. frontend/css/components/sidebar.css
Sidebar fixed kiri, lebar 220px.
Berisi: logo pilih.in (ikon film + teks hijau), navigasi vertikal dengan icon + label.
Section Genre: Aksi, Drama, Komedi, Horor, Romansa, Dokumenter.
Section bawah: box Premium dengan background gradient hijau gelap, tombol "Upgrade Sekarang".
Active state: background var(--accent-primary) dengan text putih.
Hover state: background var(--bg-hover).
Di mobile: hidden by default, slide in saat hamburger diklik (class .open).

### 3. frontend/js/components/navbar.js
Class Navbar:
- render(): inject HTML navbar ke element dengan data-component="navbar"
- initSearch(): handle input search, redirect ke katalog dengan query param
- initDropdown(): toggle dropdown avatar
- initThemeToggle(): toggle dark/light mode via state.setTheme()
- updateUserUI(): tampilkan nama user / tombol login tergantung session

### 4. frontend/js/components/sidebar.js
Class Sidebar:
- render(): inject HTML sidebar ke element dengan data-component="sidebar"
- setActiveLink(path): highlight link yang sedang aktif
- initMobileToggle(): handle hamburger open/close
- initGenreLinks(): navigate ke katalog dengan filter genre

## SPESIFIKASI HTML TEMPLATE NAVBAR (tulis sebagai template string di navbar.js)

<nav class="navbar">
  <div class="navbar__left">
    <button class="navbar__hamburger" id="hamburgerBtn">☰</button>
    <a href="/frontend/pages/main/home.html" class="navbar__logo">
      <span class="navbar__logo-icon">▶</span>
      <span class="navbar__logo-text">pilih<span class="navbar__logo-accent">.in</span></span>
    </a>
  </div>
  <div class="navbar__center">
    <a href="home.html" class="navbar__link" data-page="home">Beranda</a>
    <a href="../film/katalog.html" class="navbar__link" data-page="katalog">Film</a>
    <a href="../film/katalog.html?type=series" class="navbar__link" data-page="series">Serial TV</a>
    <a href="../user/favorites.html" class="navbar__link" data-page="favorites">Daftar Saya</a>
  </div>
  <div class="navbar__right">
    <div class="navbar__search">
      <input type="text" placeholder="Cari film, serial, genre..." class="navbar__search-input" id="searchInput">
      <button class="navbar__search-btn">🔍</button>
    </div>
    <button class="navbar__theme-toggle" id="themeToggle" title="Toggle tema">🌙</button>
    <div class="navbar__user" id="navbarUser">
      <!-- Diisi JS: avatar + dropdown atau tombol Login -->
    </div>
  </div>
</nav>

## SPESIFIKASI HTML TEMPLATE SIDEBAR (tulis sebagai template string di sidebar.js)

<aside class="sidebar" id="sidebar">
  <div class="sidebar__logo">
    <span class="sidebar__logo-icon">🎬</span>
    <span class="sidebar__logo-text">pilih<span class="sidebar__logo-accent">.in</span></span>
  </div>

  <nav class="sidebar__nav">
    <a href="home.html" class="sidebar__link" data-page="home">🏠 Beranda</a>
    <a href="#" class="sidebar__link" data-page="explore">🔍 Jelajahi</a>
    <a href="../film/katalog.html" class="sidebar__link" data-page="film">🎬 Film</a>
    <a href="../film/katalog.html?type=series" class="sidebar__link" data-page="series">📺 Serial TV</a>
    <a href="#" class="sidebar__link" data-page="trending">⚡ Baru & Populer</a>
    <a href="../user/favorites.html" class="sidebar__link" data-page="favorites">📋 Daftar Saya</a>
  </nav>

  <div class="sidebar__section-title">Genre</div>
  <nav class="sidebar__genre">
    <a href="../film/katalog.html?genre=aksi" class="sidebar__link">Aksi</a>
    <a href="../film/katalog.html?genre=drama" class="sidebar__link">Drama</a>
    <a href="../film/katalog.html?genre=komedi" class="sidebar__link">Komedi</a>
    <a href="../film/katalog.html?genre=horor" class="sidebar__link">Horor</a>
    <a href="../film/katalog.html?genre=romansa" class="sidebar__link">Romansa</a>
    <a href="../film/katalog.html?genre=dokumenter" class="sidebar__link">Dokumenter</a>
  </nav>

  <div class="sidebar__premium">
    <div class="sidebar__premium-icon">👑</div>
    <div class="sidebar__premium-title">Premium</div>
    <p class="sidebar__premium-desc">Tonton tanpa iklan dengan kualitas terbaik.</p>
    <a href="../main/pricing.html" class="sidebar__premium-btn">Upgrade Sekarang</a>
  </div>
</aside>

## CARA PAKAI KOMPONEN DI SETIAP HALAMAN
Setiap halaman HTML akan punya:
<div data-component="navbar"></div>  ← di awal body
<div class="app-layout">
  <div data-component="sidebar"></div>
  <main class="app-main">...</main>
</div>

Dan di bagian bawah script:
import Navbar from '../../js/components/navbar.js';
import Sidebar from '../../js/components/sidebar.js';
new Navbar().render();
new Sidebar().render();
```

---

---

# ═══════════════════════════════════════
# TAHAP 3 — HALAMAN AUTH: Login + Register + Lupa Sandi
# ═══════════════════════════════════════

```
Lanjutkan project pilih.in. Buat 3 halaman autentikasi berikut.
Semua file ada di folder: frontend/pages/main/

## DESAIN REFERENSI
Halaman auth pilih.in menggunakan layout 2 kolom di desktop:
- Kolom kiri (40%): form login/register dengan background var(--bg-secondary)
- Kolom kanan (60%): hero image/poster film dengan overlay gradient + tagline
- Di mobile: full kolom, hero image jadi background dengan overlay gelap
- Warna aksen: --accent-primary (#1db954) untuk tombol utama

## FILE 1: frontend/pages/main/login.html + frontend/css/pages/auth.css + frontend/js/pages/login.js

### login.html
- Import: reset.css, design-system.css, auth.css, Google Sans Flex font
- Layout 2 kolom
- Kolom kiri: Logo pilih.in, form email+password, tombol "Masuk" (hijau), link "Lupa sandi?", divider, link "Daftar sekarang"
- Kolom kanan: Background image poster film (gunakan https://picsum.photos/800/1000?random=1), overlay gradient gelap, teks tagline "Nikmati ribuan film dan serial TV favoritmu."
- Redirect ke home.html jika sudah login
- data-component="navbar" TIDAK perlu di halaman auth

### auth.css
Styling halaman auth: layout split screen, form styling dengan focus states hijau, tombol submit dengan loading state, error message styling, responsive mobile.

### login.js
- Ambil form, handle submit
- Validasi: email tidak kosong, password minimal 6 karakter
- Panggil authService.login(email, password)
- Jika berhasil: redirect ke home.html
- Jika gagal: tampilkan error message di bawah form
- Loading state: disable tombol + tampilkan spinner saat proses

## FILE 2: frontend/pages/main/register.html + frontend/js/pages/register.js

### register.html
- Struktur sama dengan login.html tapi kolom kanan pakai gambar berbeda (picsum.photos?random=2)
- Form field: Nama Lengkap, Email, Password, Konfirmasi Password
- Tombol "Daftar Sekarang"
- Link balik ke login

### register.js
- Validasi: semua field wajib, email valid, password ≥ 8 karakter, konfirmasi password cocok
- Cek email sudah terdaftar (dari repositories.users)
- Buat user baru dengan repositories.users.create({name, email, password, role: 'user', isPremium: false, createdAt: new Date()})
- Auto-login setelah register berhasil, redirect ke home.html
- Tampilkan toast "Akun berhasil dibuat!" sebelum redirect

## FILE 3: frontend/pages/main/forgot-password.html + frontend/js/pages/forgot-password.js

### forgot-password.html
- Layout 1 kolom centered (max-width: 480px, margin auto) dengan background gelap
- Logo pilih.in di atas
- Judul "Lupa Sandi?" + deskripsi singkat
- STEP 1 tampil default: input email + tombol "Kirim Kode"
- STEP 2 (muncul setelah step 1): input kode OTP (6 digit, 6 kotak terpisah), tombol "Verifikasi"
- STEP 3 (muncul setelah step 2): input password baru + konfirmasi, tombol "Reset Sandi"
- Link kembali ke login
- Indicator step (1-2-3) di atas form

### forgot-password.js
- Step 1: cek email ada di database, simpan ke sessionStorage, generate kode OTP acak 6 digit (tampilkan di console/alert sebagai simulasi), tampilkan step 2
- Step 2: verifikasi kode OTP yang diinput user vs yang disimpan, tampilkan step 3
- Step 3: update password user di database via repositories.users.update(), tampilkan toast sukses, redirect ke login setelah 2 detik

## KOMPONEN TOAST (buat di frontend/js/utils/dom.js)
Fungsi showToast(message, type='success', duration=3000):
- Buat element div dengan class 'toast toast--{type}'
- Append ke body, position fixed bottom-right
- Auto remove setelah duration
- CSS toast di design-system.css atau component terpisah

## CATATAN
- Semua path import JS menggunakan relative path yang benar dari lokasi file
- Gunakan ES6 module: <script type="module" src="...">
- Semua CSS variable dari design-system.css, jangan hardcode
```

---

---

# ═══════════════════════════════════════
# TAHAP 4 — HALAMAN HOME (Halaman Utama)
# ═══════════════════════════════════════

```
Lanjutkan project pilih.in. Buat halaman HOME — ini adalah halaman utama dan paling
penting secara visual, menampilkan konten streaming seperti Netflix/StreamFlix.

## TARGET FILE
- frontend/pages/main/home.html
- frontend/css/pages/home.css
- frontend/js/pages/home.js

## DESAIN REFERENSI (ikuti dengan detail)
Seperti screenshot StreamFlix yang diberikan:
1. Navbar atas (dari komponen navbar.js)
2. Sidebar kiri (dari komponen sidebar.js)
3. Area konten utama (margin-left: 220px di desktop):
   a. HERO BANNER — full width, tinggi ~60vh
   b. Section "Lanjutkan Menonton" — horizontal scroll card
   c. Section "Populer Minggu Ini" — list ranking di kanan, cards di kiri

## SPESIFIKASI home.html
Struktur HTML:
```html
<!DOCTYPE html>
<html lang="id" data-theme="dark">
<head>
  [meta, title "Beranda — pilih.in", font import, CSS imports]
</head>
<body>
  <div data-component="navbar"></div>
  <div class="app-layout">
    <div data-component="sidebar"></div>
    <main class="app-main">
      <!-- Hero Banner -->
      <section class="hero" id="heroBanner">
        <div class="hero__bg" id="heroBg"></div>
        <div class="hero__overlay"></div>
        <div class="hero__content">
          <span class="hero__badge">FILM TERBARU</span>
          <h1 class="hero__title" id="heroTitle"></h1>
          <p class="hero__desc" id="heroDesc"></p>
          <div class="hero__actions">
            <button class="btn btn--primary btn--lg" id="heroPlayBtn">▶ Tonton Sekarang</button>
            <button class="btn btn--ghost btn--lg" id="heroWatchlistBtn">+ Daftar Saya</button>
          </div>
          <div class="hero__dots" id="heroDots"></div>
        </div>
      </section>

      <div class="home-content">
        <!-- Continue Watching -->
        <section class="content-section" id="continueWatching">
          <h2 class="content-section__title">Lanjutkan Menonton</h2>
          <div class="film-row" id="continueWatchingRow"></div>
        </section>

        <!-- Popular This Week -->
        <section class="content-section content-section--split">
          <div class="content-section__main">
            <h2 class="content-section__title">Film Terbaru</h2>
            <div class="film-row" id="latestFilmsRow"></div>
          </div>
          <div class="content-section__sidebar">
            <h2 class="content-section__title">Populer Minggu Ini</h2>
            <ol class="popular-list" id="popularList"></ol>
          </div>
        </section>

        <!-- Genre Sections -->
        <section class="content-section" id="actionSection">
          <h2 class="content-section__title">Film Aksi 🔥</h2>
          <div class="film-row" id="actionRow"></div>
        </section>
      </div>
    </main>
  </div>
  <script type="module" src="../../js/pages/home.js"></script>
</body>
</html>
```

## SPESIFIKASI home.css

### Hero
- Position relative, height: 65vh, overflow: hidden
- .hero__bg: background-image, background-size: cover, background-position: center top
- .hero__overlay: gradient dari transparent ke var(--bg-primary) di bawah, dan gradient gelap di kiri
- .hero__content: position absolute, bottom 15%, left var(--sidebar-width) + 40px, max-width: 500px
- .hero__badge: text hijau, font-size kecil, letter-spacing, uppercase
- .hero__title: font-size var(--font-5xl), font-weight 800, line-height 1.1, text-shadow
- .hero__desc: color var(--text-secondary), max-width 400px, margin: 16px 0
- .hero__dots: indicator dots horizontal (carousel indicator)

### Film Row (horizontal scroll)
.film-row: display flex, gap: 16px, overflow-x auto, padding-bottom: 12px, scrollbar-width: thin
.film-row::-webkit-scrollbar: height 4px, color aksen hijau

### Film Card di row
.film-card: flex-shrink 0, width 180px, border-radius var(--radius-lg), overflow hidden, cursor pointer
.film-card:hover: transform scale(1.05), transition, shadow
.film-card__poster: height 260px, object-fit cover, width 100%
.film-card__overlay: absolute, bottom 0, gradient, padding 8px
.film-card__progress: progress bar hijau di bawah (untuk continue watching)
.film-card__title: font-weight semibold, font-size sm

### Popular List
.popular-list: list-style none
.popular-list li: display flex, gap 12px, padding 12px 0, border-bottom var(--border-color)
.popular-list__rank: font-size 2xl, font-weight 800, color var(--accent-primary), min-width 32px
.popular-list__thumb: width 60px, height 80px, object-fit cover, border-radius sm
.popular-list__info: flex, flex-direction column, justify-content center

### Content Section
.content-section: padding 0 var(--space-xl) var(--space-2xl)
.content-section--split: display grid, grid-template-columns: 1fr 320px, gap var(--space-2xl)
.content-section__title: font-size var(--font-xl), font-weight 700, margin-bottom var(--space-md)

### Tombol
.btn: base button style
.btn--primary: background var(--accent-primary), color white, hover var(--accent-secondary)
.btn--ghost: background rgba(255,255,255,0.15), color white, hover rgba(255,255,255,0.25), backdrop-filter blur
.btn--lg: padding 12px 28px, font-size var(--font-md)

Responsive:
- Mobile: hero height 50vh, hero content padding 16px, .content-section--split jadi 1 kolom, film-card width 140px

## SPESIFIKASI home.js

```javascript
import { repositories, authService } from '../../js/db/init.js';
import Navbar from '../../js/components/navbar.js';
import Sidebar from '../../js/components/sidebar.js';
import { showToast } from '../../js/utils/dom.js';

// 1. Init komponen
new Navbar().render();
new Sidebar().render();

// 2. Load hero — ambil film pertama / featured dari repositories.films.findAll()
// Set background image hero, title, description
// Buat carousel dots, auto-rotate setiap 5 detik

// 3. Load "Lanjutkan Menonton"
// Jika user login: ambil dari watchHistory (simulasi: 3 film pertama)
// Render film-card dengan progress bar

// 4. Load "Film Terbaru" — ambil 8 film terbaru, render film-card

// 5. Load "Populer Minggu Ini" — ambil 5 film dengan rating tertinggi,
// render sebagai ordered list dengan thumbnail + info

// 6. Load "Film Aksi" — filter genre aksi, render film-card row

// 7. Tombol "Tonton Sekarang" → redirect ke film detail atau login jika belum auth
// 8. Tombol "Daftar Saya" → tambah ke watchlist, tampilkan toast
```

Pastikan semua data diambil dari repositories (localStorage), bukan hardcode.
Gunakan data dari initialData.json yang sudah di-seed oleh DatabaseManager.
```

---

---

# ═══════════════════════════════════════
# TAHAP 5 — HALAMAN INFORMASI: FAQ + About Us + Contact Us
# ═══════════════════════════════════════

```
Lanjutkan project pilih.in. Buat 3 halaman informasi statis berikut.
Semua file ada di folder: frontend/pages/main/

## DESAIN UMUM
Semua halaman informasi menggunakan layout dengan navbar atas + sidebar kiri (komponen reuse).
Content area memiliki max-width: 900px, margin auto, padding var(--space-2xl).
Desain bersih, professional, menggunakan CSS variables.

---

## FILE 1: faq.html + frontend/js/pages/faq.js

### Deskripsi
Halaman FAQ dengan accordion interaktif. Data FAQ diambil dari repositories.faqs.

### faq.html
- Judul halaman: "Pertanyaan yang Sering Diajukan"
- Subtitle: "Temukan jawaban atas pertanyaan umum tentang layanan pilih.in"
- Search bar untuk filter FAQ (opsional tapi bagus)
- Container accordion: id="faqContainer"
- Tidak ada CSS page terpisah — gunakan styling inline di design-system atau buat faq.css minimal

### faq.js
- Ambil data dari repositories.faqs.findAll()
- Render accordion: setiap FAQ adalah item dengan question (header) dan answer (body)
- Click header: toggle class .active, animasi slide down/up answer
- Search: filter FAQ berdasarkan input teks (client-side filter)
- Accordion hanya satu terbuka setiap saat (close yang lain saat buka baru)

### Styling accordion
```css
.accordion-item { border-bottom: 1px solid var(--border-color); }
.accordion-header { padding: var(--space-md) 0; cursor: pointer; display: flex; justify-content: space-between; }
.accordion-header:hover { color: var(--accent-primary); }
.accordion-icon { transition: transform var(--transition-base); }
.accordion-item.active .accordion-icon { transform: rotate(180deg); }
.accordion-body { max-height: 0; overflow: hidden; transition: max-height var(--transition-slow); }
.accordion-item.active .accordion-body { max-height: 500px; }
.accordion-body p { padding: var(--space-md) 0; color: var(--text-secondary); line-height: 1.7; }
```

---

## FILE 2: about.html + frontend/js/pages/about.js

### Deskripsi
Halaman About Us yang menampilkan informasi perusahaan, visi misi, tim, dan statistik.

### about.html
Konten section (semua data hardcode di HTML):

**Section 1 — Hero About**
Background gradient hijau gelap, teks putih
Judul besar: "Tentang pilih.in"
Tagline: "Platform streaming film Indonesia terdepan untuk semua kalangan."

**Section 2 — Visi & Misi**
2 kolom: Visi (ikon 🎯) dan Misi (ikon 🚀)
Visi: "Menjadi platform streaming film nomor satu di Indonesia yang menjangkau seluruh lapisan masyarakat."
Misi: 4 poin misi dalam bullet list

**Section 3 — Statistik Angka**
4 stat card dalam grid: "50.000+ Film", "2 Juta+ Pengguna", "99.9% Uptime", "4.8★ Rating"
Card dengan background var(--bg-tertiary), angka besar hijau, label abu-abu

**Section 4 — Tim Inti**
Grid 4 kartu tim: Founder & CEO, CTO, Head of Content, Head of Design
Setiap kartu: avatar placeholder (gunakan picsum.photos/100/100?random=10,11,12,13), nama, jabatan

**Section 5 — Kontak Cepat**
CTA untuk ke halaman Contact Us

### about.js
Hanya init Navbar dan Sidebar. Tidak ada logika khusus.

---

## FILE 3: contact.html + frontend/js/pages/contact.js

### Deskripsi
Halaman Contact Us dengan form kontak + informasi kontak.

### contact.html
Layout 2 kolom:
- Kolom kiri (60%): Form kontak
- Kolom kanan (40%): Info kontak + map placeholder

**Form kontak (kolom kiri):**
- Judul: "Hubungi Kami"
- Field: Nama*, Email*, Subjek* (dropdown: Pertanyaan Umum/Masalah Teknis/Berlangganan/Lainnya), Pesan* (textarea 4 baris)
- Tombol: "Kirim Pesan" (hijau)
- Pesan sukses muncul di bawah form setelah submit

**Info kontak (kolom kanan):**
- 📧 Email: support@pilih.in
- 📞 Telepon: +62 812-3456-7890
- 📍 Alamat: Jl. Sudirman No. 123, Jakarta Selatan, 12190
- ⏰ Jam Operasional: Senin-Jumat 08.00-17.00 WIB
- Social media icons: Instagram, Twitter/X, YouTube, TikTok (link dummy)
- Map placeholder: div dengan background var(--bg-tertiary), teks "Peta akan ditampilkan di sini", border-radius, height 200px

### contact.js
- Init Navbar & Sidebar
- Handle form submit
- Validasi semua field required
- Validasi format email
- Simulasi submit: loading state 1.5 detik, lalu tampilkan pesan sukses
- Tidak perlu kirim ke server — cukup tampilkan "Pesan berhasil dikirim! Tim kami akan menghubungi Anda dalam 1x24 jam."
```

---

---

# ═══════════════════════════════════════
# TAHAP 6 — HALAMAN KEBIJAKAN + PROMO + HARGA
# ═══════════════════════════════════════

```
Lanjutkan project pilih.in. Buat 3 halaman terakhir berikut.
Semua file ada di: frontend/pages/main/

---

## FILE 1: privacy-policy.html (Kebijakan & Privasi)

### Deskripsi
Halaman legal yang menampilkan kebijakan privasi dan syarat penggunaan layanan pilih.in.
Menggunakan navbar + sidebar. Content area centered, max-width 800px.

### Struktur Halaman
- Header: Judul "Kebijakan Privasi & Syarat Penggunaan", tanggal berlaku "Berlaku sejak: 1 Januari 2025"
- Sidebar navigasi di dalam konten (sticky di desktop): daftar section dengan anchor link
- Konten utama dengan section-section berikut:

**1. Pendahuluan**
Penjelasan singkat bahwa pilih.in berkomitmen melindungi privasi pengguna.

**2. Data yang Kami Kumpulkan**
Sub-poin: Data Akun (nama, email, password terenkripsi), Data Penggunaan (film ditonton, preferensi), Data Perangkat (browser, OS, IP address)

**3. Cara Kami Menggunakan Data**
4 poin: Personalisasi konten, Perbaikan layanan, Komunikasi, Keamanan akun

**4. Berbagi Data dengan Pihak Ketiga**
Penjelasan bahwa data tidak dijual. Pengecualian: mitra pembayaran, kepatuhan hukum.

**5. Hak Pengguna**
Hak akses data, koreksi, penghapusan, keberatan pemrosesan.

**6. Keamanan Data**
Enkripsi SSL, audit keamanan berkala, akses terbatas karyawan.

**7. Cookie**
Jenis cookie yang digunakan (esensial, analitik, preferensi).

**8. Perubahan Kebijakan**
Notifikasi via email jika ada perubahan signifikan.

**9. Hubungi Kami**
Email privacy@pilih.in untuk pertanyaan seputar privasi.

### Styling
Typography-focused: headings hijau, body text var(--text-secondary), line-height 1.8
Sticky in-page navigation di kanan (di desktop) untuk jump ke section
"Back to top" button floating kanan bawah
Tidak perlu JS khusus selain init Navbar + Sidebar + smooth scroll

---

## FILE 2: promo.html + frontend/js/pages/promo.js (Info Promo)

### Deskripsi
Halaman menampilkan promo dan voucher aktif. Data dari repositories.promotions.

### Desain
Hero kecil di atas: background gradient hijau, judul "🎉 Promo & Voucher Spesial", subtitle
Filter tabs: Semua | Aktif | Akan Datang | Kadaluarsa
Grid kartu promo (3 kolom di desktop, 1 di mobile)

### Promo Card Spec (.promo-card)
- Background var(--bg-card), border-radius lg, overflow hidden
- Header card: background gradient sesuai tipe promo, padding lg
  - Badge tipe (DISKON / GRATIS / CASHBACK) dengan warna berbeda
  - Kode voucher besar: font-size 2xl, font-weight 800, letter-spacing, background gelap
  - Tombol copy "📋 Salin Kode" → copy ke clipboard, ubah teks ke "✓ Tersalin!"
- Body card: deskripsi promo, syarat & ketentuan ringkas
- Footer card: tanggal berlaku, progress bar menunjukkan sisa waktu

### promo.js
- Init Navbar & Sidebar
- Load dari repositories.promotions.findAll()
- Render promo cards
- Filter tabs: filter array berdasarkan status (active/upcoming/expired berdasarkan tanggal)
- Copy kode: navigator.clipboard.writeText(kode), feedback visual
- Countdown timer untuk promo yang akan berakhir dalam 24 jam

---

## FILE 3: pricing.html + frontend/js/pages/pricing.js (List Harga Langganan)

### Deskripsi
Halaman pricing dengan 3 paket berlangganan. Desain premium, visual menarik.

### Desain
**Hero Section:**
Judul: "Pilih Paket Terbaikmu"
Toggle billing: Bulanan / Tahunan (hemat 20%)
Subtitle kecil

**Pricing Cards (3 paket dalam grid 3 kolom):**

Paket BASIC (Rp 29.000/bln):
- Header warna normal (var(--bg-tertiary))
- Fitur: 1 perangkat, resolusi SD, tanpa download, ada iklan, akses film terbatas
- Tombol outline "Pilih Basic"

Paket STANDARD (Rp 49.000/bln) — RECOMMENDED:
- Header background aksen hijau, badge "PALING POPULER"
- Sedikit lebih besar dari dua kartu lain (scale atau shadow)
- Fitur: 2 perangkat, Full HD, 10 download/bulan, minim iklan, akses semua film
- Tombol solid hijau "Pilih Standard"

Paket PREMIUM (Rp 89.000/bln):
- Header background gradient gelap premium, badge "BEST VALUE"
- Fitur: 4 perangkat, 4K Ultra HD, unlimited download, tanpa iklan, akses semua + eksklusif
- Tombol "Pilih Premium"

**Tabel Perbandingan Fitur** (di bawah cards):
Tabel full-width membandingkan semua fitur antar paket
Centang (✓ hijau) / Silang (✗ merah) / Teks untuk setiap fitur

**FAQ Singkat** (3-4 item accordion):
Pertanyaan umum seputar berlangganan

**CTA Bottom:**
"Masih ragu? Coba gratis 7 hari. Batalkan kapan saja."
Tombol "Mulai Uji Coba Gratis"

### pricing.js
- Init Navbar & Sidebar
- Load data dari repositories.pricing.findAll()
- Toggle billing bulanan/tahunan: kalkulasi harga tahunan (harga_bulanan × 12 × 0.8), animasi perubahan harga
- Tombol pilih paket:
  - Jika belum login: redirect ke login.html?redirect=pricing
  - Jika sudah login: redirect ke halaman payment (simulasi)
  - Highlight paket yang sedang aktif user (cek dari session)
- Accordion FAQ: toggle show/hide

---

## CATATAN TAMBAHAN UNTUK SEMUA FILE DI TAHAP INI
1. Import Navbar & Sidebar di setiap file JS halaman
2. Semua CSS menggunakan variable dari design-system.css
3. Pastikan responsive di mobile (max-width: 768px)
4. Tambahkan breadcrumb navigasi di setiap halaman: Beranda > [Nama Halaman]
5. Setiap halaman punya <title> yang sesuai di <head>
```

---

---

# ═══════════════════════════════════════
# TAHAP 7 — POLISH & INTEGRASI: Koneksi Antar Halaman + Testing
# ═══════════════════════════════════════

```
Tahap terakhir: pastikan semua halaman pilih.in terkoneksi dan berfungsi dengan benar.
Buat file-file utilitas yang masih kurang, perbaiki koneksi antar module, dan pastikan
flow utama bekerja end-to-end.

## TASK 1: Lengkapi frontend/js/utils/dom.js

Buat file ini dengan fungsi-fungsi berikut:

```javascript
// Toast notification
export function showToast(message, type = 'success', duration = 3000) { ... }

// Loading spinner
export function showLoading(element) { ... }  // tambah class .loading ke element
export function hideLoading(element) { ... }  // hapus class .loading

// Error display di form
export function showFormError(inputElement, message) { ... }  // tambah error message di bawah input
export function clearFormError(inputElement) { ... }

// Confirm dialog
export function showConfirm(message, onConfirm, onCancel) { ... }  // modal konfirmasi sederhana

// Format tanggal Indonesia
export function formatDate(dateString) { ... }  // "25 Mei 2025"

// Format Rupiah
export function formatRupiah(number) { ... }  // "Rp 49.000"

// Truncate text
export function truncate(text, maxLength) { ... }
```

CSS untuk toast (tambahkan ke design-system.css):
```css
.toast { position: fixed; bottom: 24px; right: 24px; padding: 12px 20px;
  border-radius: var(--radius-md); color: white; font-weight: var(--fw-medium);
  z-index: var(--z-toast); transform: translateY(20px); opacity: 0;
  transition: all var(--transition-base); pointer-events: none; }
.toast.show { transform: translateY(0); opacity: 1; }
.toast--success { background: var(--success); }
.toast--error { background: var(--danger); }
.toast--warning { background: var(--warning); color: #000; }
.toast--info { background: var(--info); }
```

## TASK 2: Lengkapi frontend/js/utils/validation.js

```javascript
export function validateEmail(email) { ... }  // regex check
export function validatePassword(password) { ... }  // min 8 char, return {valid, message}
export function validateRequired(value, fieldName) { ... }
export function validateMinLength(value, min, fieldName) { ... }
export function validateMatch(value1, value2, fieldName) { ... }

// Validate seluruh form
export function validate(data, schema) {
  // schema: { fieldName: [rule1, rule2, ...] }
  // return null jika valid, atau {fieldName: errorMessage} jika tidak valid
}
```

## TASK 3: Seed Data di DatabaseManager.js

Pastikan DatabaseManager.js punya method initializeIfEmpty():
```javascript
async initializeIfEmpty() {
  const db = this.getDB();
  if (db && db.initialized) return;
  
  // Load dan seed initialData.json
  const response = await fetch('/data/initialData.json');
  const data = await response.json();
  
  this.saveDB({ ...data, initialized: true });
}
```

Dan panggil ini di main.js saat startup.

## TASK 4: Pastikan Path dan Link Semua Benar

Buat checklist dan PERBAIKI semua link navigasi:
- Logo di navbar/sidebar → /frontend/pages/main/home.html
- "Beranda" nav link → home.html (relative dari lokasi file)  
- "Film" → ../film/katalog.html (buat file placeholder jika belum ada)
- Login/Register → link dua arah
- Dari home → pricing, promo, faq, about, contact
- Semua tombol "Upgrade Sekarang" → pricing.html
- Breadcrumbs di setiap halaman mengarah ke home.html

## TASK 5: Buat frontend/pages/film/katalog.html (Placeholder)

Buat halaman katalog sederhana (bukan full implementation, tapi functional):
- Navbar + Sidebar
- Grid film-card yang diload dari repositories.films.findAll()
- Filter sederhana berdasarkan genre (query param ?genre=xxx)
- Search sederhana
- Ini placeholder, cukup functional untuk link navigasi bekerja

## TASK 6: index.html di Root

Buat pilih-in/frontend/index.html yang:
- Redirect langsung menggunakan JavaScript
- Jika ada session (pilih-in-session di localStorage) → redirect ke pages/main/home.html
- Jika tidak ada session → redirect ke pages/main/login.html

```javascript
const session = localStorage.getItem('pilih-in-session');
if (session) {
  window.location.replace('./pages/main/home.html');
} else {
  window.location.replace('./pages/main/login.html');
}
```

## TASK 7: Cek dan Perbaiki Import Paths

Untuk setiap file JS di pages/main/, path import ke db/init.js adalah:
../../js/db/init.js

Untuk file JS di pages/film/:
../../js/db/init.js

Untuk file JS di pages/user/:
../../js/db/init.js

Verifikasi semua import path di setiap file JS sudah benar.

## TASK 8: README.md

Buat file pilih-in/README.md yang menjelaskan:
- Cara menjalankan project (buka dengan live-server atau langsung buka index.html)
- Akun demo: admin@pilih.in / admin123, user@pilih.in / user123
- Struktur folder
- Teknologi yang digunakan
- Cara reset database (dari browser console)
- Daftar semua halaman yang sudah dibuat
```

---

## 🎯 RINGKASAN SEMUA PROMPT

| Tahap | Target | Hasil |
|-------|--------|-------|
| 1 | Fondasi + Design System | Struktur folder, CSS vars, DB layer |
| 2 | Navbar + Sidebar | Komponen reusable di semua halaman |
| 3 | Auth Pages | Login, Register, Lupa Sandi |
| 4 | Home Page | Hero, cards, popular list |
| 5 | Info Pages | FAQ, About, Contact |
| 6 | Commerce Pages | Privacy, Promo, Pricing |
| 7 | Polish + Integrasi | Utils, seed data, link fix, README |

**Total: 10 halaman utama + foundation + komponen reusable**
