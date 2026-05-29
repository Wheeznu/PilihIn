---
name: pilih-in
description: >
    Skill utama untuk mengembangkan website pilih.in — platform streaming film Indonesia
    berbasis Vanilla HTML/CSS/JS dengan localStorage sebagai database. Gunakan skill ini
    setiap kali mengerjakan task apapun di project pilih.in: membuat halaman baru,
    komponen UI, logika data, CRUD, routing, styling, atau integrasi antar modul.
    Trigger: menyebut "pilih.in", "buatkan halaman", "tambah fitur", "perbaiki komponen",
    "buat CRUD", "connect data ke UI", atau task frontend/backend apapun di project in/home/wisnu/Projects/pilihin-project/skill.mdi.
---

# Pilih.in — Master Development Skill

Panduan lengkap dan mengikat untuk AI agent mengembangkan **pilih.in**, platform streaming
film Indonesia. Semua keputusan teknis, naming, struktur file, dan pola kode harus mengikuti
dokumen ini secara konsisten.

---

## ATURAN KERAS — BACA SEBELUM MENULIS SATU BARIS PUN

```
WAJIB:
  Vanilla HTML5 + CSS3 + JavaScript ES6+ SAJA
  Ikuti struktur folder yang sudah ada (lihat bagian File Structure)
  Gunakan CSS variables dari design-system.css — jangan hardcode nilai apapun
  Semua data via Repository pattern → DatabaseManager → localStorage
  Nama file: kebab-case  |  Class JS: PascalCase  |  Variabel JS: camelCase
  Setiap halaman HTML import CSS-nya sendiri + design-system.css
  Semua ikon WAJIB menggunakan Feather Icons — TIDAK BOLEH emoji atau SVG inline
  index.html (di root frontend/) adalah halaman Home — bukan sekadar entry point

DILARANG KERAS:
  React, Vue, Angular, Svelte, atau framework apapun
  npm, Webpack, Vite, Parcel, atau build tool apapun
  TypeScript, SASS, LESS, Tailwind, atau preprocessor apapun
  Menyimpan data langsung ke localStorage tanpa melalui DatabaseManager
  Hardcode warna, ukuran, atau spacing — selalu pakai CSS variable
  Inline style di HTML kecuali untuk nilai dinamis dari JavaScript
  Menaruh logika bisnis di file HTML — semua JS ada di folder js/
  Membuat struktur folder baru di luar yang sudah didefinisikan
  Emoji sebagai ikon UI — gunakan Feather Icons
  Library ikon lain (Font Awesome, Material Icons, Heroicons, dsb)
  SVG ikon inline di HTML — selalu pakai <i data-feather="...">
```

---

## Struktur Folder Tetap (Jangan Diubah)

```
pilih-in/
├── data/
│   ├── initialData.json          ← Sample data 19 koleksi, jangan edit manual
│   └── schema.js                 ← Definisi schema database
│
└── frontend/
    ├── index.html                ← HALAMAN HOME (beranda utama, bukan sekadar entry point)
    │
    ├── css/
    │   ├── reset.css             ← Browser normalization
    │   ├── design-system.css     ← SATU-SATUNYA tempat CSS variables
    │   ├── components/           ← Satu file per komponen
    │   │   ├── navbar.css
    │   │   ├── sidebar.css
    │   │   ├── button.css
    │   │   ├── card.css
    │   │   ├── modal.css
    │   │   ├── form.css
    │   │   └── video-player.css
    │   └── pages/                ← Satu file per halaman
    │       ├── home.css
    │       ├── auth.css
    │       ├── film-catalog.css
    │       ├── film-detail.css
    │       ├── user-profile.css
    │       └── admin-panel.css
    │
    ├── js/
    │   ├── main.js               ← App init, component registry
    │   ├── router.js             ← Client-side routing
    │   ├── state.js              ← App state (user session, filters)
    │   │
    │   ├── db/                   ← Lapisan data — jangan akses localStorage langsung
    │   │   ├── DatabaseManager.js
    │   │   ├── Repository.js
    │   │   ├── BackupManager.js
    │   │   ├── Validator.js
    │   │   ├── init.js           ← Export semua repository instances
    │   │   ├── repositories/
    │   │   │   ├── FilmRepository.js
    │   │   │   ├── UserRepository.js
    │   │   │   ├── ActorRepository.js
    │   │   │   ├── DirectorRepository.js
    │   │   │   ├── GenreRepository.js
    │   │   │   ├── ReviewRepository.js
    │   │   │   ├── FavoriteRepository.js
    │   │   │   ├── WatchListRepository.js
    │   │   │   ├── WatchHistoryRepository.js
    │   │   │   ├── NotificationRepository.js
    │   │   │   ├── ArticleRepository.js
    │   │   │   ├── FaqRepository.js
    │   │   │   ├── PricingRepository.js
    │   │   │   ├── PromotionRepository.js
    │   │   │   └── TransactionRepository.js
    │   │   └── services/
    │   │       ├── AuthService.js
    │   │       └── FilmService.js
    │   │
    │   ├── components/           ← Class JS per komponen UI
    │   │   ├── navbar.js
    │   │   ├── sidebar.js
    │   │   ├── modal.js
    │   │   ├── video-player.js
    │   │   └── card.js
    │   │
    │   ├── pages/                ← Logic per halaman
    │   │   ├── home.js
    │   │   ├── login.js
    │   │   ├── register.js
    │   │   ├── film-catalog.js
    │   │   ├── film-detail.js
    │   │   ├── user-profile.js
    │   │   └── admin-panel.js
    │   │
    │   └── utils/
    │       ├── dom.js
    │       ├── validation.js
    │       ├── storage.js
    │       └── date.js
    │
    ├── pages/
    │   ├── main/                 ← index.html, login.html, register.html,
    │   │                            forgot-password.html, artikel.html,
    │   │                            faq.html, promo.html, pricing.html,
    │   │                            payment.html, about.html, contact.html
    │   ├── film/                 ← katalog.html, search.html, genre.html,
    │   │                            detail.html, actor-profile.html,
    │   │                            director-profile.html
    │   ├── user/                 ← profile.html, subscription.html,
    │   │                            settings.html, security.html,
    │   │                            history.html, favorites.html,
    │   │                            watchlist.html, notifications.html,
    │   │                            transactions.html
    │   ├── admin/                ← dashboard.html, films-crud.html,
    │   │                            actors-crud.html, directors-crud.html,
    │   │                            articles-crud.html, users-management.html,
    │   │                            pricing-vouchers.html, faq-crud.html,
    │   │                            reviews-moderation.html
    │   └── manager/             ← dashboard.html, earnings.html,
    │                               traffic-stats.html, top-films.html,
    │                               approvals.html, reports-export.html
    │
    └── assets/
        ├── images/
        ├── icons/
        └── fonts/
```

---

## Design System — CSS Variables Wajib

Semua nilai visual **harus** mengacu ke variable berikut. Jangan pernah hardcode.

### Font

Pilih.in menggunakan **Google Sans Flex** — variable font dari Google Fonts.
Wajib diimport di `<head>` setiap halaman HTML:

```html
<!-- Taruh di <head> sebelum semua CSS lain -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
    href="https://fonts.googleapis.com/css2?family=Google+Sans+Flex:wght@100..900&display=swap"
    rel="stylesheet"
/>
```

```css
/* Di design-system.css — gunakan variable ini di seluruh project */
--font-family:
    "Google Sans Flex", -apple-system, BlinkMacSystemFont, sans-serif;
```

> **Jangan** menggunakan font lain (Inter, Roboto, Segoe UI, dll). Selalu fallback ke
> `-apple-system, BlinkMacSystemFont, sans-serif` jika Google Sans Flex tidak tersedia.

---

### Ikon — Feather Icons (Wajib)

Pilih.in menggunakan **Feather Icons** sebagai sistem ikon satu-satunya.
Feather Icons adalah library ikon SVG ringan (3KB gzip) berbasis CDN.

**Import via CDN — taruh sebelum `</body>` di setiap halaman:**

```html
<!-- Taruh sebelum tag </body> penutup, SETELAH semua konten HTML -->
<script src="https://cdn.jsdelivr.net/npm/feather-icons/dist/feather.min.js"></script>
```

**Cara pakai ikon:**

```html
<!-- Cukup tulis tag <i> dengan data-feather, feather.replace() akan menggantinya dengan SVG -->
<i data-feather="home"></i>
<i data-feather="film"></i>
<i data-feather="search"></i>
<i data-feather="heart"></i>
<i data-feather="bookmark"></i>
```

**Inisialisasi — wajib dipanggil setelah DOM siap (sudah ada di main.js):**

```javascript
// js/main.js — dipanggil di akhir DOMContentLoaded, setelah semua komponen diinit
document.addEventListener("DOMContentLoaded", () => {
    // ... init komponen lain dulu ...
    feather.replace(); // Konversi semua <i data-feather="..."> menjadi SVG inline
});
```

> **Penting**: `feather.replace()` hanya perlu dipanggil **satu kali** di `main.js`.
> Jika konten dirender secara dinamis (innerHTML), panggil ulang `feather.replace()`
> setelah DOM diperbarui.

**Mengatur ukuran & warna ikon:**

```css
/* css/design-system.css — aturan global untuk semua ikon Feather */
[data-feather],
.feather {
    width: 1em; /* Mengikuti font-size elemen induk */
    height: 1em;
    stroke: currentColor; /* Mengikuti color CSS elemen induk */
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
    fill: none;
    vertical-align: middle;
    flex-shrink: 0;
}

/* Override ukuran spesifik */
.icon-sm {
    width: 16px;
    height: 16px;
}
.icon-md {
    width: 20px;
    height: 20px;
} /* Default */
.icon-lg {
    width: 24px;
    height: 24px;
}
.icon-xl {
    width: 32px;
    height: 32px;
}
```

**Referensi ikon yang digunakan di Pilih.in:**

| Konteks             | Nama Ikon Feather |
| ------------------- | ----------------- |
| Beranda / Home      | `home`            |
| Film / Katalog      | `film`            |
| Cari                | `search`          |
| Favorit             | `heart`           |
| Daftar Tonton       | `bookmark`        |
| Riwayat             | `clock`           |
| Profil              | `user`            |
| Pengaturan          | `settings`        |
| Notifikasi          | `bell`            |
| Transaksi           | `credit-card`     |
| Langganan           | `star`            |
| Keamanan            | `shield`          |
| Admin Dashboard     | `grid`            |
| CRUD Film           | `video`           |
| CRUD Aktor          | `users`           |
| CRUD Sutradara      | `camera`          |
| Artikel             | `file-text`       |
| Manajemen User      | `user-check`      |
| Harga & Voucher     | `tag`             |
| FAQ                 | `help-circle`     |
| Moderasi Review     | `message-square`  |
| Manager Dashboard   | `bar-chart-2`     |
| Pendapatan          | `dollar-sign`     |
| Statistik           | `trending-up`     |
| Top Film            | `award`           |
| Persetujuan         | `check-circle`    |
| Laporan             | `download`        |
| Logout              | `log-out`         |
| Tema Gelap / Terang | `moon` / `sun`    |
| Menu (hamburger)    | `menu`            |
| Tutup / Hapus       | `x`               |
| Edit                | `edit-2`          |
| Tambah              | `plus`            |
| Tonton / Play       | `play-circle`     |
| Rating / Bintang    | `star`            |
| Kembali             | `arrow-left`      |
| Maju                | `arrow-right`     |
| Chevron bawah       | `chevron-down`    |
| Filter              | `sliders`         |
| Urutkan             | `list`            |
| Salin               | `copy`            |
| Bagikan             | `share-2`         |

**Re-render ikon setelah update DOM dinamis:**

```javascript
// Setiap kali innerHTML diperbarui dengan konten berisi <i data-feather="...">,
// panggil feather.replace() setelahnya:
DOM.$("#filmGrid").innerHTML = paged.data
    .map((f) => this._filmCardHTML(f))
    .join("");
feather.replace(); // ← wajib setelah set innerHTML
```

---

### Tema Warna — Dual Theme (Dark & Light)

Pilih.in mendukung **dark mode dan light mode** via atribut `data-theme` pada elemen `<html>`.
Default adalah `dark`. Toggle tema disimpan di `localStorage` key `pilih-in-theme`.

```css
/* frontend/css/design-system.css */

/* ~~~ Dark Mode (default) ~~~ */
:root[data-theme="dark"] {
    /* Background */
    --bg-primary: #121212;
    --bg-secondary: #181818;
    --bg-tertiary: #242424;
    --bg-card: #1e1e1e;
    --bg-hover: #2a2a2a;

    /* Text */
    --text-primary: #ffffff;
    --text-secondary: #b3b3b3;
    --text-muted: #8a8a8a;

    /* Accent */
    --accent-primary: #1db954; /* Hijau — tombol utama, CTA, active state */
    --accent-secondary: #1ed760; /* Hover/focus accent */
    --accent-dark: #14833b; /* Pressed state accent */

    /* Status */
    --danger: #e22134;
    --warning: #f5c518;
    --info: #3498ff;
    --success: #1db954;

    /* Border & Shadow */
    --border-color: #353535;
    --shadow-color: rgba(0, 0, 0, 0.45);

    /* Overlay */
    --overlay-dark: rgba(0, 0, 0, 0.65);
    --overlay-light: rgba(255, 255, 255, 0.08);
}

/* ~~~ Light Mode ~~~ */
:root[data-theme="light"] {
    /* Background */
    --bg-primary: #ffffff;
    --bg-secondary: #f7f7f7;
    --bg-tertiary: #ebebeb;
    --bg-card: #ffffff;
    --bg-hover: #e2e2e2;

    /* Text */
    --text-primary: #121212;
    --text-secondary: #535353;
    --text-muted: #7a7a7a;

    /* Accent */
    --accent-primary: #1db954;
    --accent-secondary: #1ed760;
    --accent-dark: #14833b;

    /* Status */
    --danger: #e22134;
    --warning: #f5c518;
    --info: #3498ff;
    --success: #1db954;

    /* Border & Shadow */
    --border-color: #d4d4d4;
    --shadow-color: rgba(0, 0, 0, 0.12);

    /* Overlay */
    --overlay-dark: rgba(0, 0, 0, 0.12);
    --overlay-light: rgba(255, 255, 255, 0.65);
}
```

---

### Variable Sistem (Tidak Bergantung Tema)

Variable di bawah ini dideklarasikan di `:root` biasa karena nilainya sama di kedua tema.

```css
/* frontend/css/design-system.css — lanjutan */
:root {
    /* === TIPOGRAFI === */
    --font-family:
        "Google Sans Flex", -apple-system, BlinkMacSystemFont, sans-serif;
    --font-xs: 0.75rem; /* 12px */
    --font-sm: 0.875rem; /* 14px */
    --font-md: 1rem; /* 16px */
    --font-lg: 1.125rem; /* 18px */
    --font-xl: 1.25rem; /* 20px */
    --font-2xl: 1.5rem; /* 24px */
    --font-3xl: 1.875rem; /* 30px */
    --font-4xl: 2.25rem; /* 36px */
    --fw-normal: 400;
    --fw-medium: 500;
    --fw-semibold: 600;
    --fw-bold: 700;

    /* === SPACING === */
    --space-xs: 0.25rem; /*  4px */
    --space-sm: 0.5rem; /*  8px */
    --space-md: 1rem; /* 16px */
    --space-lg: 1.5rem; /* 24px */
    --space-xl: 2rem; /* 32px */
    --space-2xl: 3rem; /* 48px */
    --space-3xl: 4rem; /* 64px */

    /* === BORDER RADIUS === */
    --radius-sm: 0.25rem;
    --radius-md: 0.5rem;
    --radius-lg: 0.75rem;
    --radius-xl: 1rem;
    --radius-full: 9999px;

    /* === SHADOW — gunakan --shadow-color agar responsif terhadap tema === */
    --shadow-sm: 0 1px 3px var(--shadow-color);
    --shadow-md: 0 4px 6px var(--shadow-color);
    --shadow-lg: 0 10px 15px var(--shadow-color);
    --shadow-xl: 0 20px 25px var(--shadow-color);

    /* === TRANSISI === */
    --transition-fast: 150ms ease-in-out;
    --transition-base: 250ms ease-in-out;
    --transition-slow: 350ms ease-in-out;

    /* === Z-INDEX === */
    --z-dropdown: 100;
    --z-sticky: 200;
    --z-backdrop: 900;
    --z-modal: 1000;
    --z-tooltip: 1100;
    --z-toast: 1200;

    /* === LAYOUT === */
    --sidebar-width: 220px;
    --navbar-height: 64px;
    --content-max-width: 1280px;
}
```

---

### Toggle Tema — JavaScript

```javascript
// js/utils/theme.js
export const Theme = {
    STORAGE_KEY: "pilih-in-theme",
    DEFAULT: "dark",

    init() {
        const saved = localStorage.getItem(this.STORAGE_KEY) || this.DEFAULT;
        this.apply(saved);
    },

    apply(theme) {
        document.documentElement.setAttribute("data-theme", theme);
        localStorage.setItem(this.STORAGE_KEY, theme);
    },

    toggle() {
        const current =
            document.documentElement.getAttribute("data-theme") || this.DEFAULT;
        this.apply(current === "dark" ? "light" : "dark");
    },

    current() {
        return (
            document.documentElement.getAttribute("data-theme") || this.DEFAULT
        );
    },
};

// Panggil Theme.init() di awal main.js agar tidak ada flash of wrong theme
```

```javascript
// js/main.js — baris pertama sebelum apapun
import { Theme } from "./utils/theme.js";
Theme.init();
```

```html
<!-- Tombol toggle di navbar -->
<button
    class="btn btn-ghost btn-icon"
    id="themeToggle"
    aria-label="Ganti tema"
    onclick="Theme.toggle()"
>
    <i data-feather="moon" id="themeIcon"></i>
</button>
```

```javascript
// Update ikon sesuai tema aktif — panggil di Theme.apply()
apply(theme) {
  document.documentElement.setAttribute('data-theme', theme);
  localStorage.setItem(this.STORAGE_KEY, theme);
  // Update ikon toggle
  const icon = document.getElementById('themeIcon');
  if (icon) {
    icon.setAttribute('data-feather', theme === 'dark' ? 'moon' : 'sun');
    feather.replace(); // Re-render ikon yang diubah
  }
},
```

---

### Referensi Cepat Variable per Konteks

| Konteks                     | Variable yang Digunakan     |
| --------------------------- | --------------------------- |
| Background halaman          | `var(--bg-primary)`         |
| Background sidebar/navbar   | `var(--bg-secondary)`       |
| Background card/panel       | `var(--bg-card)`            |
| Hover state elemen          | `var(--bg-hover)`           |
| Input / dropdown background | `var(--bg-tertiary)`        |
| Teks utama                  | `var(--text-primary)`       |
| Teks label/meta             | `var(--text-secondary)`     |
| Placeholder / teks lemah    | `var(--text-muted)`         |
| Tombol CTA / aksi utama     | `var(--accent-primary)`     |
| Hover tombol CTA            | `var(--accent-secondary)`   |
| Pressed / active tombol     | `var(--accent-dark)`        |
| Border garis pemisah        | `var(--border-color)`       |
| Box shadow                  | `var(--shadow-sm/md/lg/xl)` |
| Overlay di atas gambar      | `var(--overlay-dark)`       |
| Overlay glass-morphism      | `var(--overlay-light)`      |
| Error / hapus               | `var(--danger)`             |
| Peringatan                  | `var(--warning)`            |
| Info / link                 | `var(--info)`               |
| Sukses / konfirmasi         | `var(--success)`            |

---

### Penggunaan Benar vs Salah

```css
/* BENAR — pakai variable, responsif terhadap tema */
.card {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
}
.btn-primary {
    background: var(--accent-primary);
    color: var(--bg-primary);
}
.btn-primary:hover {
    background: var(--accent-secondary);
}
.text-muted {
    color: var(--text-muted);
}
.overlay {
    background: var(--overlay-dark);
}

/* SALAH — hardcode, tidak akan menyesuaikan tema */
.card {
    background: #1e1e1e;
    border: 1px solid #353535;
}
.btn-primary {
    background: #1db954;
    color: black;
}
.text-muted {
    color: #8a8a8a;
}
```

---

## Database & Data Flow

### Arsitektur Data (Wajib Diikuti)

```
User Action (klik, submit form)
        ↓
Event Handler di js/pages/ atau js/components/
        ↓
Import { repositories } from '../db/init.js'
        ↓
repositories.namaKoleksi.method(params)    ← SATU-SATUNYA cara akses data
        ↓
Repository → DatabaseManager.saveCollection()
        ↓
localStorage.setItem('pilih-in-db', JSON.stringify(db))
        ↓
Update DOM dengan data terbaru
        ↓
User melihat hasil
```

**Aturan kritis**: Tidak boleh ada `localStorage.setItem` atau `localStorage.getItem`
di luar file `DatabaseManager.js`. Semua akses data lewat `repositories.*`.

### 19 Koleksi Database

| Koleksi             | Keterangan                                       | ID Contoh           |
| ------------------- | ------------------------------------------------ | ------------------- |
| `users`             | Akun pengguna (role: user/admin/manager)         | `user-001`          |
| `films`             | Konten film streaming                            | `film-001`          |
| `actors`            | Data aktor                                       | `actor-001`         |
| `directors`         | Data sutradara                                   | `director-001`      |
| `genres`            | Kategori genre (8 genre)                         | `genre-001`         |
| `articles`          | Artikel & berita                                 | `article-001`       |
| `faqs`              | Konten FAQ                                       | `faq-001`           |
| `pricingTiers`      | Paket langganan (Free, Basic, Standard, Premium) | `tier-001`          |
| `promotions`        | Kode voucher & promo                             | `promo-001`         |
| `reviews`           | Rating & ulasan film                             | `review-001`        |
| `transactions`      | Riwayat pembayaran                               | `trans-001`         |
| `favorites`         | Film favorit user                                | `fav-001`           |
| `watchLists`        | Daftar tonton user                               | `wl-001`            |
| `watchHistory`      | Riwayat tonton                                   | `wh-001`            |
| `actorFavorites`    | Aktor favorit user                               | `af-001`            |
| `directorFavorites` | Sutradara favorit user                           | `df-001`            |
| `notifications`     | Notifikasi user                                  | `notif-001`         |
| `userPoints`        | Poin loyalitas                                   | (indexed by userId) |
| `metadata`          | Versi & timestamp DB                             | —                   |

### Schema Entitas Penting

```javascript
// FILM — entitas inti
{
  id: "film-001",
  title: "Gundala",
  description: "string",
  poster: "URL atau base64",
  banner: "URL atau base64",
  releaseDate: "2019-08-29",       // ISO date
  duration: 98,                     // menit
  rating: "PG-13",                  // G|PG|PG-13|R|NC-17
  genres: ["genre-001", "genre-006"],  // array of genre IDs
  director: "director-001",            // single director ID
  actors: ["actor-001", "actor-002"],  // array of actor IDs
  averageRating: 8.2,               // float 0-10
  reviewCount: 245,
  watchCount: 5420,
  streamingUrl: "string",
  videoQuality: ["720p", "1080p"],
  subtitles: ["id", "en"],
  status: "published",              // draft|published|archived
  createdAt: "ISO timestamp",
  updatedAt: "ISO timestamp",
  createdBy: "user-001"
}

// USER — dengan role-based access
{
  id: "user-001",
  username: "admin_pilih",
  email: "admin@pilih.in",
  password: "hashed",              // JANGAN plain text
  role: "admin",                   // user|admin|manager
  profilePhoto: "URL",
  fullName: "string",
  phone: "+62...",
  status: "active",                // active|suspended|banned
  subscriptionTier: "tier-003",
  subscriptionExpiry: "2025-05-24",
  preferences: { theme, language, notifications, privateProfile },
  createdAt, updatedAt, lastLogin
}

// REVIEW — relasi ke film & user
{
  id: "review-001",
  filmId: "film-001",
  userId: "user-003",
  rating: 9,                       // integer 1-10
  title: "string",
  content: "string",
  helpful: 42,
  status: "approved",              // pending|approved|rejected
  createdAt, updatedAt
}
```

---

## Pola Kode Standar

### 1. DatabaseManager (Dasar)

```javascript
// js/db/DatabaseManager.js
class DatabaseManager {
    constructor(dbName = "pilih-in-db") {
        this.dbName = dbName;
        this._initIfEmpty();
    }

    _initIfEmpty() {
        if (!localStorage.getItem(this.dbName)) {
            localStorage.setItem(
                this.dbName,
                JSON.stringify(this._defaultDb()),
            );
        }
    }

    getDatabase() {
        try {
            return (
                JSON.parse(localStorage.getItem(this.dbName)) ||
                this._defaultDb()
            );
        } catch {
            return this._defaultDb();
        }
    }

    saveDatabase(db) {
        try {
            localStorage.setItem(this.dbName, JSON.stringify(db));
            return true;
        } catch (err) {
            if (err.name === "QuotaExceededError")
                console.warn("localStorage penuh!");
            return false;
        }
    }

    getCollection(name) {
        return this.getDatabase()[name] || [];
    }

    saveCollection(name, data) {
        const db = this.getDatabase();
        db[name] = data;
        return this.saveDatabase(db);
    }

    _defaultDb() {
        return {
            users: [],
            films: [],
            actors: [],
            directors: [],
            genres: [],
            articles: [],
            faqs: [],
            pricingTiers: [],
            promotions: [],
            reviews: [],
            transactions: [],
            favorites: [],
            watchLists: [],
            watchHistory: [],
            notifications: [],
            actorFavorites: [],
            directorFavorites: [],
            userPoints: [],
            metadata: {
                version: "1.0",
                lastInitialized: new Date().toISOString(),
            },
        };
    }
}

export default DatabaseManager;
```

### 2. Repository Base (CRUD Universal)

```javascript
// js/db/Repository.js
class Repository {
    constructor(dbManager, collectionName) {
        this.db = dbManager;
        this.collection = collectionName;
    }

    create(data) {
        const items = this.db.getCollection(this.collection);
        const record = {
            id: this._uuid(),
            ...data,
            createdAt: new Date().toISOString(),
            updatedAt: new Date().toISOString(),
        };
        items.push(record);
        this.db.saveCollection(this.collection, items);
        return record;
    }

    findById(id) {
        return (
            this.db.getCollection(this.collection).find((i) => i.id === id) ||
            null
        );
    }

    findAll() {
        return this.db.getCollection(this.collection);
    }

    findWhere(predicate) {
        return this.db.getCollection(this.collection).filter(predicate);
    }

    update(id, data) {
        const items = this.db.getCollection(this.collection);
        const idx = items.findIndex((i) => i.id === id);
        if (idx === -1)
            throw new Error(`${this.collection}#${id} tidak ditemukan`);
        items[idx] = {
            ...items[idx],
            ...data,
            updatedAt: new Date().toISOString(),
        };
        this.db.saveCollection(this.collection, items);
        return items[idx];
    }

    delete(id) {
        const items = this.db.getCollection(this.collection);
        const idx = items.findIndex((i) => i.id === id);
        if (idx === -1)
            throw new Error(`${this.collection}#${id} tidak ditemukan`);
        const [deleted] = items.splice(idx, 1);
        this.db.saveCollection(this.collection, items);
        return deleted;
    }

    paginate(page = 1, size = 12, predicate = null) {
        const all = predicate ? this.findWhere(predicate) : this.findAll();
        const start = (page - 1) * size;
        return {
            data: all.slice(start, start + size),
            total: all.length,
            page,
            size,
            totalPages: Math.ceil(all.length / size),
        };
    }

    search(fields, query) {
        const q = query.toLowerCase();
        return this.findAll().filter((item) =>
            fields.some((f) =>
                String(item[f] ?? "")
                    .toLowerCase()
                    .includes(q),
            ),
        );
    }

    count(predicate = null) {
        return predicate
            ? this.findWhere(predicate).length
            : this.findAll().length;
    }

    _uuid() {
        return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, (c) => {
            const r = (Math.random() * 16) | 0;
            return (c === "x" ? r : (r & 0x3) | 0x8).toString(16);
        });
    }
}

export default Repository;
```

### 3. Contoh Repository Spesifik

```javascript
// js/db/repositories/FilmRepository.js
import Repository from "../Repository.js";

class FilmRepository extends Repository {
    constructor(dbManager) {
        super(dbManager, "films");
    }

    findPublished() {
        return this.findWhere((f) => f.status === "published");
    }
    findByGenre(genreId) {
        return this.findWhere((f) => f.genres.includes(genreId));
    }
    findByDirector(directorId) {
        return this.findWhere((f) => f.director === directorId);
    }
    findByActor(actorId) {
        return this.findWhere((f) => f.actors.includes(actorId));
    }
    findPopular(limit = 10) {
        return this.findPublished()
            .sort((a, b) => b.watchCount - a.watchCount)
            .slice(0, limit);
    }
    findLatest(limit = 10) {
        return this.findPublished()
            .sort((a, b) => new Date(b.releaseDate) - new Date(a.releaseDate))
            .slice(0, limit);
    }
    findTrending(limit = 10) {
        return this.findPublished()
            .sort(
                (a, b) =>
                    b.averageRating * 10 +
                    b.watchCount -
                    (a.averageRating * 10 + a.watchCount),
            )
            .slice(0, limit);
    }
    search(query) {
        return super.search(["title", "description"], query);
    }
}

export default FilmRepository;
```

```javascript
// js/db/repositories/FavoriteRepository.js
import Repository from "../Repository.js";

class FavoriteRepository extends Repository {
    constructor(dbManager) {
        super(dbManager, "favorites");
    }

    add(userId, filmId) {
        if (this.exists(userId, filmId))
            throw new Error("Sudah ada di favorit");
        return this.create({
            userId,
            filmId,
            addedAt: new Date().toISOString(),
        });
    }

    remove(userId, filmId) {
        const fav = this.findWhere(
            (f) => f.userId === userId && f.filmId === filmId,
        )[0];
        if (!fav) throw new Error("Favorit tidak ditemukan");
        return this.delete(fav.id);
    }

    exists(userId, filmId) {
        return (
            this.findWhere((f) => f.userId === userId && f.filmId === filmId)
                .length > 0
        );
    }

    getByUser(userId) {
        return this.findWhere((f) => f.userId === userId);
    }
}

export default FavoriteRepository;
```

### 4. init.js — Titik Akses Tunggal ke Semua Repository

```javascript
// js/db/init.js
import DatabaseManager from "./DatabaseManager.js";
import BackupManager from "./BackupManager.js";
import FilmRepository from "./repositories/FilmRepository.js";
import UserRepository from "./repositories/UserRepository.js";
import ActorRepository from "./repositories/ActorRepository.js";
import DirectorRepository from "./repositories/DirectorRepository.js";
import GenreRepository from "./repositories/GenreRepository.js";
import ReviewRepository from "./repositories/ReviewRepository.js";
import FavoriteRepository from "./repositories/FavoriteRepository.js";
// ... import semua repository lainnya

export const dbManager = new DatabaseManager("pilih-in-db");
export const backupManager = new BackupManager(dbManager);

// Inisialisasi data awal (hanya saat pertama kali)
if (!localStorage.getItem("pilih-in-initialized")) {
    const res = await fetch("/data/initialData.json");
    const data = await res.json();
    const db = dbManager.getDatabase();
    Object.assign(db, data);
    dbManager.saveDatabase(db);
    backupManager.createBackup("Initial Setup");
    localStorage.setItem("pilih-in-initialized", "true");
}

// Ekspor semua repository sebagai objek tunggal
export const repositories = {
    films: new FilmRepository(dbManager),
    users: new UserRepository(dbManager),
    actors: new ActorRepository(dbManager),
    directors: new DirectorRepository(dbManager),
    genres: new GenreRepository(dbManager),
    reviews: new ReviewRepository(dbManager),
    favorites: new FavoriteRepository(dbManager),
    watchLists: new WatchListRepository(dbManager),
    watchHistory: new WatchHistoryRepository(dbManager),
    notifications: new NotificationRepository(dbManager),
    articles: new ArticleRepository(dbManager),
    faqs: new FaqRepository(dbManager),
    pricingTiers: new PricingRepository(dbManager),
    promotions: new PromotionRepository(dbManager),
    transactions: new TransactionRepository(dbManager),
};
```

---

## Pola Komponen UI

### Template HTML Komponen

Setiap komponen menggunakan `data-component` untuk auto-init, `data-action` untuk events.

```html
<!-- Contoh: Modal -->
<div
    class="modal"
    id="deleteModal"
    data-component="modal"
    role="dialog"
    aria-modal="true"
>
    <div class="modal-overlay" data-action="close"></div>
    <div class="modal-content">
        <button class="modal-close" data-action="close" aria-label="Tutup">
            <i data-feather="x"></i>
        </button>
        <h2 class="modal-title">Hapus Film</h2>
        <div class="modal-body">Yakin ingin menghapus film ini?</div>
        <div class="modal-footer">
            <button class="btn btn-secondary" data-action="close">Batal</button>
            <button class="btn btn-danger" data-action="confirm">
                <i data-feather="trash-2"></i> Hapus
            </button>
        </div>
    </div>
</div>
```

### Template Class JS Komponen

```javascript
// js/components/modal.js
class Modal {
    constructor(element) {
        this.el = element;
        this._onConfirm = null;
        this._bindEvents();
    }

    _bindEvents() {
        this.el
            .querySelectorAll('[data-action="close"]')
            .forEach((btn) =>
                btn.addEventListener("click", () => this.close()),
            );
        this.el
            .querySelector('[data-action="confirm"]')
            ?.addEventListener("click", () => {
                this._onConfirm?.();
                this.close();
            });
        document.addEventListener("keydown", (e) => {
            if (e.key === "Escape" && this.isOpen()) this.close();
        });
    }

    open() {
        this.el.classList.add("active");
        document.body.style.overflow = "hidden";
    }
    close() {
        this.el.classList.remove("active");
        document.body.style.overflow = "";
    }
    isOpen() {
        return this.el.classList.contains("active");
    }

    onConfirm(callback) {
        this._onConfirm = callback;
        return this;
    }
}

export default Modal;
```

### Auto-Init Komponen di main.js

```javascript
// js/main.js
import Modal from "./components/modal.js";
import Navbar from "./components/navbar.js";
import Sidebar from "./components/sidebar.js";
import VideoPlayer from "./components/video-player.js";

const registry = {
    modal: Modal,
    navbar: Navbar,
    sidebar: Sidebar,
    "video-player": VideoPlayer,
};

document.addEventListener("DOMContentLoaded", () => {
    Object.entries(registry).forEach(([name, Component]) => {
        document
            .querySelectorAll(`[data-component="${name}"]`)
            .forEach((el) => new Component(el));
    });

    // Inisialisasi Feather Icons — konversi semua <i data-feather="..."> ke SVG
    feather.replace();
});
```

### Template Class JS Halaman

```javascript
// js/pages/film-catalog.js
import { repositories } from "../db/init.js";
import { DOM } from "../utils/dom.js";

class FilmCatalogPage {
    constructor() {
        this.currentPage = 1;
        this.currentGenre = null;
        this.currentSort = "latest";
        this.searchQuery = "";
        this._bindEvents();
        this.render();
    }

    _bindEvents() {
        DOM.$("#searchInput")?.addEventListener(
            "input",
            this._debounce((e) => {
                this.searchQuery = e.target.value;
                this.currentPage = 1;
                this.render();
            }, 300),
        );

        DOM.$("#genreFilter")?.addEventListener("change", (e) => {
            this.currentGenre = e.target.value || null;
            this.currentPage = 1;
            this.render();
        });

        DOM.$("#sortFilter")?.addEventListener("change", (e) => {
            this.currentSort = e.target.value;
            this.render();
        });
    }

    _getFilms() {
        let films = this.searchQuery
            ? repositories.films.search(this.searchQuery)
            : repositories.films.findPublished();

        if (this.currentGenre)
            films = films.filter((f) => f.genres.includes(this.currentGenre));

        return films.sort((a, b) => {
            if (this.currentSort === "rating")
                return b.averageRating - a.averageRating;
            if (this.currentSort === "popular")
                return b.watchCount - a.watchCount;
            return new Date(b.releaseDate) - new Date(a.releaseDate); // latest (default)
        });
    }

    render() {
        const films = this._getFilms();
        const paged = {
            data: films.slice(
                (this.currentPage - 1) * 20,
                this.currentPage * 20,
            ),
            total: films.length,
            totalPages: Math.ceil(films.length / 20),
        };
        DOM.$("#filmGrid").innerHTML = paged.data
            .map((f) => this._filmCardHTML(f))
            .join("");
        feather.replace(); // Re-render ikon Feather setelah innerHTML diperbarui
        this._renderPagination(paged);
    }

    _filmCardHTML(film) {
        const genres = repositories.genres.findAll();
        const genreNames = film.genres
            .map((id) => genres.find((g) => g.id === id)?.name)
            .filter(Boolean)
            .join(", ");

        return `
      <div class="film-card" data-film-id="${film.id}">
        <div class="film-card__poster">
          <img src="${film.poster}" alt="${film.title}" loading="lazy">
          <div class="film-card__overlay">
            <a href="/pages/film/detail.html?id=${film.id}" class="btn btn-primary btn-sm">
              <i data-feather="play-circle"></i> Tonton
            </a>
          </div>
          <span class="film-card__rating"><i data-feather="star"></i> ${film.averageRating}</span>
        </div>
        <div class="film-card__info">
          <h3 class="film-card__title">${film.title}</h3>
          <p class="film-card__meta">${new Date(film.releaseDate).getFullYear()} • ${film.duration} mnt</p>
          <p class="film-card__genre text-secondary">${genreNames}</p>
        </div>
      </div>`;
    }

    _renderPagination({ totalPages }) {
        const el = DOM.$("#pagination");
        if (!el) return;
        el.innerHTML = Array.from(
            { length: totalPages },
            (_, i) => `
      <button class="btn btn-sm ${i + 1 === this.currentPage ? "btn-primary" : "btn-ghost"}"
              onclick="this._page(${i + 1})">${i + 1}</button>
    `,
        ).join("");
    }

    _page(n) {
        this.currentPage = n;
        this.render();
    }

    _debounce(fn, delay) {
        let t;
        return (...args) => {
            clearTimeout(t);
            t = setTimeout(() => fn(...args), delay);
        };
    }
}

export default FilmCatalogPage;
```

---

## Autentikasi & Role-Based Access

### AuthService

```javascript
// js/db/services/AuthService.js
import { repositories } from "../init.js";

class AuthService {
    static SESSION_KEY = "pilih-in-session";

    login(email, password) {
        const user = repositories.users.findWhere((u) => u.email === email)[0];
        if (!user) throw new Error("Email tidak ditemukan");
        if (!this._verify(password, user.password))
            throw new Error("Password salah");
        if (user.status !== "active") throw new Error("Akun dinonaktifkan");

        const session = {
            userId: user.id,
            role: user.role,
            loginAt: new Date().toISOString(),
        };
        localStorage.setItem(AuthService.SESSION_KEY, JSON.stringify(session));
        repositories.users.update(user.id, {
            lastLogin: new Date().toISOString(),
        });
        return user;
    }

    logout() {
        localStorage.removeItem(AuthService.SESSION_KEY);
    }

    getSession() {
        try {
            return JSON.parse(localStorage.getItem(AuthService.SESSION_KEY));
        } catch {
            return null;
        }
    }

    getCurrentUser() {
        const session = this.getSession();
        return session ? repositories.users.findById(session.userId) : null;
    }

    isLoggedIn() {
        return !!this.getSession();
    }
    isAdmin() {
        return this.getSession()?.role === "admin";
    }
    isManager() {
        return this.getSession()?.role === "manager";
    }
    isUser() {
        return this.getSession()?.role === "user";
    }

    requireAuth(redirectTo = "/pages/main/login.html") {
        if (!this.isLoggedIn()) {
            window.location.href = redirectTo;
            return false;
        }
        return true;
    }

    requireRole(role, redirectTo = "/") {
        if (this.getSession()?.role !== role) {
            window.location.href = redirectTo;
            return false;
        }
        return true;
    }

    register(data) {
        const existing = repositories.users.findWhere(
            (u) => u.email === data.email,
        )[0];
        if (existing) throw new Error("Email sudah terdaftar");
        return repositories.users.create({
            ...data,
            password: this._hash(data.password),
            role: "user",
            status: "active",
            subscriptionTier: "tier-001", // Free
            preferences: {
                theme: "dark",
                language: "id",
                notifications: true,
                privateProfile: false,
            },
        });
    }

    _hash(pwd) {
        return btoa(unescape(encodeURIComponent(pwd)));
    }
    _verify(pwd, hash) {
        return this._hash(pwd) === hash;
    }
}

export const authService = new AuthService();
export default AuthService;
```

### Penggunaan di Halaman Admin

```javascript
// Taruh di awal setiap file js/pages/admin-*.js
import { authService } from "../db/services/AuthService.js";

// Cek akses sebelum render apapun
if (!authService.requireRole("admin", "/pages/main/login.html")) {
    throw new Error("Akses ditolak"); // Hentikan eksekusi
}
```

---

## Utilitas DOM

```javascript
// js/utils/dom.js
export const DOM = {
    $(sel, ctx = document) {
        return ctx.querySelector(sel);
    },
    $$(sel, ctx = document) {
        return [...ctx.querySelectorAll(sel)];
    },

    create(tag, props = {}) {
        const el = document.createElement(tag);
        const { className, html, text, ...attrs } = props;
        if (className) el.className = className;
        if (html) el.innerHTML = html;
        if (text) el.textContent = text;
        Object.entries(attrs).forEach(([k, v]) => el.setAttribute(k, v));
        return el;
    },

    // Event delegation — efisien untuk daftar dinamis
    delegate(parent, event, selector, handler) {
        parent.addEventListener(event, (e) => {
            const target = e.target.closest(selector);
            if (target) handler.call(target, e, target);
        });
    },

    show(el) {
        el?.classList.remove("hidden");
    },
    hide(el) {
        el?.classList.add("hidden");
    },
    toggle(el) {
        el?.classList.toggle("hidden");
    },

    setHTML(el, html) {
        if (el) el.innerHTML = html;
    },
    setText(el, text) {
        if (el) el.textContent = text;
    },

    showToast(message, type = "success", duration = 3000) {
        const toast = DOM.create("div", {
            className: `toast toast--${type}`,
            text: message,
        });
        document.body.appendChild(toast);
        setTimeout(() => toast.remove(), duration);
    },
};
```

---

## Validasi Data

```javascript
// js/utils/validation.js
export const Rules = {
    required: (v) => (v?.toString().trim() ? null : "Field wajib diisi"),
    email: (v) =>
        /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v) ? null : "Email tidak valid",
    minLen: (n) => (v) => (v?.length >= n ? null : `Minimal ${n} karakter`),
    maxLen: (n) => (v) => (v?.length <= n ? null : `Maksimal ${n} karakter`),
    phone: (v) => (/^\+?[0-9]{10,15}$/.test(v) ? null : "Nomor tidak valid"),
    rating: (v) =>
        Number.isInteger(v) && v >= 1 && v <= 10 ? null : "Rating 1-10",
    positiveNum: (v) =>
        typeof v === "number" && v > 0 ? null : "Harus bilangan positif",
};

export function validate(data, schema) {
    const errors = {};
    for (const [field, rules] of Object.entries(schema)) {
        for (const rule of rules) {
            const err = rule(data[field]);
            if (err) {
                errors[field] = err;
                break;
            }
        }
    }
    return Object.keys(errors).length ? errors : null;
}

export function showFormErrors(form, errors) {
    form.querySelectorAll(".field-error").forEach((el) => el.remove());
    form.querySelectorAll(".input--error").forEach((el) =>
        el.classList.remove("input--error"),
    );
    for (const [field, msg] of Object.entries(errors)) {
        const input = form.querySelector(`[name="${field}"]`);
        if (!input) continue;
        input.classList.add("input--error");
        const span = document.createElement("span");
        span.className = "field-error";
        span.textContent = msg;
        input.parentNode.appendChild(span);
    }
}

// Contoh penggunaan di form tambah film
const filmSchema = {
    title: [Rules.required, Rules.minLen(2), Rules.maxLen(200)],
    description: [Rules.required, Rules.minLen(10)],
    duration: [Rules.required, Rules.positiveNum],
};
```

---

## Template HTML Halaman Baru

Gunakan boilerplate ini setiap membuat halaman baru:

```html
<!DOCTYPE html>
<html lang="id" data-theme="dark">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>[Nama Halaman] - Pilih.in</title>

        <!-- Google Sans Flex -->
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link
            href="https://fonts.googleapis.com/css2?family=Google+Sans+Flex:wght@100..900&display=swap"
            rel="stylesheet"
        />

        <!-- Urutan import CSS: reset → design-system → components → page-specific -->
        <link rel="stylesheet" href="../../css/reset.css" />
        <link rel="stylesheet" href="../../css/design-system.css" />
        <link rel="stylesheet" href="../../css/components/navbar.css" />
        <link rel="stylesheet" href="../../css/components/sidebar.css" />
        <link rel="stylesheet" href="../../css/components/card.css" />
        <link rel="stylesheet" href="../../css/pages/[nama-halaman].css" />
    </head>
    <body>
        <div class="app-layout">
            <!-- Sidebar -->
            <aside class="sidebar" id="sidebar" data-component="sidebar">
                <div class="sidebar__logo">
                    <a href="/frontend/index.html"
                        >Pilih<span class="text-primary">.in</span></a
                    >
                </div>
                <nav class="sidebar__nav" aria-label="Navigasi utama">
                    <a href="/frontend/index.html" class="nav-item"
                        ><i data-feather="home"></i> Beranda</a
                    >
                    <a href="/frontend/pages/film/katalog.html" class="nav-item"
                        ><i data-feather="film"></i> Film</a
                    >
                    <a href="/frontend/pages/film/search.html" class="nav-item"
                        ><i data-feather="search"></i> Cari</a
                    >
                    <a
                        href="/frontend/pages/user/favorites.html"
                        class="nav-item"
                        ><i data-feather="heart"></i> Favorit</a
                    >
                    <a
                        href="/frontend/pages/user/watchlist.html"
                        class="nav-item"
                        ><i data-feather="bookmark"></i> Daftar Tonton</a
                    >
                </nav>
            </aside>

            <!-- Area Utama -->
            <div class="app-main">
                <header class="navbar" id="navbar" data-component="navbar">
                    <!-- Navbar content -->
                </header>

                <main class="page-content" id="mainContent">
                    <!-- Konten halaman -->
                </main>
            </div>
        </div>

        <!-- Feather Icons CDN — taruh sebelum script JS module -->
        <script src="https://cdn.jsdelivr.net/npm/feather-icons/dist/feather.min.js"></script>

        <!-- JS: db init dulu, baru page logic -->
        <script type="module">
            import { repositories } from "../../js/db/init.js";
            import NamaHalamanPage from "../../js/pages/nama-halaman.js";
            new NamaHalamanPage();
        </script>
    </body>
</html>
```

---

## Komponen CSS Standar

### Button

```css
/* css/components/button.css */
.btn {
    display: inline-flex;
    align-items: center;
    gap: var(--space-xs);
    padding: var(--space-sm) var(--space-lg);
    border: none;
    border-radius: var(--radius-md);
    font-family: var(--font-family);
    font-size: var(--font-sm);
    font-weight: var(--fw-semibold);
    cursor: pointer;
    transition: all var(--transition-base);
    text-decoration: none;
    white-space: nowrap;
}

.btn-primary {
    background: var(--accent-primary);
    color: var(--bg-primary);
}
.btn-secondary {
    background: var(--bg-tertiary);
    color: var(--text-primary);
}
.btn-danger {
    background: var(--danger);
    color: #fff;
}
.btn-ghost {
    background: transparent;
    border: 1px solid var(--border-color);
    color: var(--text-primary);
}
.btn-sm {
    padding: var(--space-xs) var(--space-md);
    font-size: var(--font-xs);
}
.btn-lg {
    padding: var(--space-md) var(--space-xl);
    font-size: var(--font-lg);
}

.btn-primary:hover {
    background: var(--accent-secondary);
}
.btn-secondary:hover {
    background: var(--bg-hover);
}
.btn-danger:hover {
    opacity: 0.85;
}
.btn-ghost:hover {
    background: var(--bg-hover);
}
.btn:disabled {
    opacity: 0.4;
    cursor: not-allowed;
}
```

### Film Card

```css
/* css/components/card.css */
.film-card {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    overflow: hidden;
    transition: transform var(--transition-base);
    cursor: pointer;
}

.film-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
}

.film-card__poster {
    position: relative;
    aspect-ratio: 2 / 3;
    overflow: hidden;
}

.film-card__poster img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform var(--transition-slow);
}

.film-card:hover .film-card__poster img {
    transform: scale(1.05);
}

.film-card__overlay {
    position: absolute;
    inset: 0;
    background: var(--overlay-dark);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity var(--transition-base);
}

.film-card:hover .film-card__overlay {
    opacity: 1;
}

.film-card__rating {
    position: absolute;
    top: var(--space-sm);
    right: var(--space-sm);
    background: rgba(0, 0, 0, 0.8);
    color: var(--text-primary);
    font-size: var(--font-xs);
    font-weight: var(--fw-bold);
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-sm);
}

.film-card__info {
    padding: var(--space-md);
}

.film-card__title {
    color: var(--text-primary);
    font-size: var(--font-md);
    font-weight: var(--fw-semibold);
    margin-bottom: var(--space-xs);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.film-card__meta {
    color: var(--text-secondary);
    font-size: var(--font-sm);
}
.film-card__genre {
    color: var(--text-muted);
    font-size: var(--font-xs);
    margin-top: var(--space-xs);
}
```

### Layout Grid Film

```css
.film-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: var(--space-lg);
}

@media (max-width: 768px) {
    .film-grid {
        grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
        gap: var(--space-md);
    }
}
```

---

## Layout Responsif

### Breakpoint Standar

```css
/* Mobile first — tambahkan media query untuk tablet & desktop */
/* Mobile:  < 768px  — default */
/* Tablet:  768px    */
/* Desktop: 1024px   */
/* Wide:    1280px   */

/* App Layout */
.app-layout {
    display: flex;
    min-height: 100vh;
    background: var(--bg-primary);
    color: var(--text-primary);
}

.sidebar {
    width: var(--sidebar-width);
    flex-shrink: 0;
    background: var(--bg-secondary);
    border-right: 1px solid var(--border-color);
    position: fixed;
    height: 100vh;
    overflow-y: auto;
    z-index: var(--z-sticky);
    transform: translateX(-100%); /* Hidden di mobile */
    transition: transform var(--transition-base);
}

.sidebar.open,
@media (min-width: 1024px) {
    .sidebar {
        transform: translateX(0);
    }
}

.app-main {
    flex: 1;
    margin-left: 0;
    transition: margin-left var(--transition-base);
}

@media (min-width: 1024px) {
    .app-main {
        margin-left: var(--sidebar-width);
    }
}

.page-content {
    padding: var(--space-xl);
    max-width: var(--content-max-width);
}

@media (max-width: 768px) {
    .page-content {
        padding: var(--space-md);
    }
}
```

---

## Naming Convention Wajib

| Konteks          | Aturan        | Contoh                            |
| ---------------- | ------------- | --------------------------------- |
| File HTML        | kebab-case    | `film-detail.html`                |
| File CSS         | kebab-case    | `film-catalog.css`                |
| File JS          | kebab-case    | `film-repository.js`              |
| Class JS         | PascalCase    | `FilmRepository`                  |
| Fungsi/metode JS | camelCase     | `findByGenre()`                   |
| Variabel JS      | camelCase     | `currentPage`                     |
| CSS class        | kebab-case    | `.film-card__poster`              |
| CSS variable     | `--kata-kata` | `--space-lg`                      |
| ID localStorage  | `pilih-in-*`  | `pilih-in-db`, `pilih-in-session` |
| ID entitas DB    | `koleksi-NNN` | `film-001`, `user-003`            |
| data-attribute   | kebab-case    | `data-film-id`, `data-action`     |
| Event custom     | kebab-case    | `film:added`, `auth:logout`       |

### BEM untuk CSS Komponen

```
.block {}                    → .film-card {}
.block__element {}           → .film-card__poster {}
.block--modifier {}          → .film-card--featured {}
.block__element--modifier {} → .film-card__title--truncated {}
```

---

## 🚀 Checklist Saat Membuat Fitur Baru

Ikuti urutan ini setiap menambahkan fitur:

```
1. Tentukan koleksi data mana yang terlibat (lihat tabel 19 koleksi)
2. Apakah perlu Repository baru? Jika ya, buat di js/db/repositories/
3. Daftarkan repository baru di js/db/init.js
4. Buat/edit file HTML di pages/[dashboard]/
5. Buat CSS di css/pages/[nama].css menggunakan CSS variables
6. Buat class JS di js/pages/[nama].js — import repositories dari db/init.js
7. Tambahkan link navigasi ke sidebar jika halaman baru
8. Validasi semua input sebelum CRUD menggunakan utils/validation.js
9. Tampilkan feedback user (toast/error) setiap operasi berhasil/gagal
10. Test role access — apakah halaman ini perlu authService.requireRole()?
11. Cek responsif di mobile (< 768px) dan desktop (> 1024px)
```

---

## Pola Operasi CRUD Lengkap

### Create dengan Validasi

```javascript
async function createFilm(formData) {
    // 1. Validasi
    const errors = validate(formData, filmSchema);
    if (errors) {
        showFormErrors(form, errors);
        return;
    }

    // 2. Backup sebelum mutasi penting
    backupManager.autoBackup("pre-create-film");

    try {
        // 3. Simpan via repository
        const film = repositories.films.create({
            ...formData,
            status: "draft",
            averageRating: 0,
            reviewCount: 0,
            watchCount: 0,
        });

        // 4. Feedback & redirect
        DOM.showToast(`Film "${film.title}" berhasil ditambahkan`, "success");
        window.location.href = `/frontend/pages/admin/films-crud.html`;
    } catch (err) {
        DOM.showToast(err.message, "error");
    }
}
```

### Read dengan Relasi

```javascript
function getFilmDetail(filmId) {
    const film = repositories.films.findById(filmId);
    if (!film) return null;

    // Populate relasi
    return {
        ...film,
        director: repositories.directors.findById(film.director),
        actors: film.actors
            .map((id) => repositories.actors.findById(id))
            .filter(Boolean),
        genres: film.genres
            .map((id) => repositories.genres.findById(id))
            .filter(Boolean),
        reviews: repositories.reviews.findWhere(
            (r) => r.filmId === filmId && r.status === "approved",
        ),
    };
}
```

### Update

```javascript
function updateFilm(filmId, data) {
    const errors = validate(data, filmSchema);
    if (errors) {
        showFormErrors(form, errors);
        return;
    }

    try {
        const updated = repositories.films.update(filmId, data);
        DOM.showToast("Film berhasil diperbarui", "success");
        return updated;
    } catch (err) {
        DOM.showToast(err.message, "error");
    }
}
```

### Delete dengan Konfirmasi

```javascript
function deleteFilm(filmId) {
    const modal = document.querySelector("#deleteModal");
    const modalInstance = new Modal(modal);

    modalInstance.onConfirm(() => {
        backupManager.autoBackup("pre-delete-film");
        try {
            repositories.films.delete(filmId);
            DOM.showToast("Film dihapus", "success");
            renderFilmList(); // Re-render tabel
        } catch (err) {
            DOM.showToast(err.message, "error");
        }
    });

    modalInstance.open();
}
```

---

## Tips Debug & Troubleshooting

```javascript
// Cek isi database di console browser
const db = JSON.parse(localStorage.getItem("pilih-in-db"));
console.table(db.films);

// Cek storage usage
const size = new Blob([localStorage.getItem("pilih-in-db")]).size;
console.log(`DB size: ${(size / 1024).toFixed(1)} KB`);

// Reset database (hati-hati!)
localStorage.removeItem("pilih-in-db");
localStorage.removeItem("pilih-in-initialized");
location.reload();
```

**Masalah umum & solusi:**

| Masalah              | Penyebab                                | Solusi                                 |
| -------------------- | --------------------------------------- | -------------------------------------- |
| Komponen tidak init  | `data-component` salah/tidak ada        | Cek atribut HTML & nama di registry    |
| CSS tidak berlaku    | File tidak diimport atau selector salah | Cek urutan import & specificity        |
| Data tidak tersimpan | QuotaExceededError                      | Hapus data lama, cek storage size      |
| Module import error  | Path relatif salah                      | Hitung `../../` dari lokasi file       |
| Halaman kosong       | JS error di init                        | Cek Console, pastikan db/init.js jalan |

---

**Versi**: 2.0
**Dibuat**: Mei 2026
**Project**: Pilih.in - GEMASTIK Competition
**Stack**: 100% Vanilla HTML5 + CSS3 + JavaScript ES6+
