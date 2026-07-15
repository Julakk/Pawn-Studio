# Changelog

Semua perubahan penting pada project PawnStudio dicatat di file ini.

## [Unreleased]

Belum ada perubahan baru yang menunggu rilis.

## [0.8.0] - VSCode-style UI Overhaul

### Added
- Activity Bar di sisi kiri (ikon Explorer, Search, Settings) — layout makin mirip VSCode asli
- Breadcrumb path di atas editor (`PawnStudio › nama_file.pwn`)
- Indikator posisi cursor live di status bar (`Ln X, Col Y`)
- Warna ikon file berbeda per tipe ekstensi (`.pwn` ungu sesuai brand, `.inc` biru muda, `.js`/`.json` kuning, `.css` biru, `.html` oranye) — di file explorer maupun tab
- Ikon file kecil di setiap tab, konsisten dengan warna di file explorer

### Changed
- Status bar dipecah jadi grup kiri (info file) dan kanan (cursor position, bahasa) agar lebih rapi
- Tombol Settings kini juga bisa diakses dari Activity Bar, selain dari topbar

## [0.7.0] - Branding & Polish

### Added
- App icon custom (pawn chess piece + curly braces) untuk semua densitas layar Android
- Splash screen custom sesuai branding PawnStudio
- Icon Play Store (512×512) untuk keperluan publish nanti

### Changed
- Seluruh icon UI (topbar, sidebar, tab) diganti dari emoji menjadi SVG custom — tampilan lebih konsisten dan tajam di semua ukuran layar
- Nama file APK hasil build diseragamkan menjadi `PawnStudio.apk` (sebelumnya `app-debug.apk` di dalam `PawnStudio-debug-apk.zip`)

## [0.6.0] - Settings Panel

### Added
- Panel Settings (ikon gear di topbar) dengan opsi:
  - Font size editor (Kecil/Sedang/Besar/Extra Besar)
  - Tema editor (Dark/Light/High Contrast)
  - Toggle Word Wrap
- Preferensi settings tersimpan permanen di `localStorage`, otomatis diterapkan ulang tiap app dibuka

## [0.5.0] - Compiler Integration (Native, Offline)

### Added
- Integrasi compiler PAWN asli (`pawn-lang/compiler`), di-cross-compile khusus untuk Android arm64-v8a menggunakan Android NDK
- Workflow GitHub Actions terpisah (`build-pawncc-arm64.yml`) untuk build binary compiler dari source
- Custom Capacitor plugin (`PawnCompilerPlugin`) yang menjalankan compiler sebagai native process dari dalam app
- Bundle include standar PAWN (`core.inc`, `float.inc`, `string.inc`, dll) dan SA-MP (`a_samp.inc` dan seluruh `a_*.inc`) langsung di dalam APK
- Tombol ▶ Run sekarang benar-benar meng-compile kode `.pwn` menjadi `.amx`, 100% offline tanpa server
- Output panel dengan pewarnaan pesan (error merah, warning kuning, sukses hijau)
- Fitur jump-to-line: tap pesan error/warning di output panel langsung melompat dan menyorot baris terkait di editor
- Hasil compile (`.amx`) disimpan ke penyimpanan permanen (`Android/data/.../files/compiled/`), tidak lagi ke cache yang bisa terhapus otomatis

### Fixed
- Linker error `-lpthread` saat cross-compile ke Android (dengan stub library kosong)
- Error `cannot find symbol` karena mismatch bahasa plugin (Kotlin vs Java project)
- Error `Permission denied` saat eksekusi binary dari `filesDir` — dipindah ke `jniLibs` sesuai kebijakan W^X Android modern
- Path checkout CMake yang salah pada workflow cross-compile

## [0.4.0] - CI/CD Setup

### Added
- Konfigurasi Capacitor (`capacitor.config.json`, `package.json`)
- GitHub Actions workflow (`build.yml`) untuk build APK otomatis tiap push ke `main`
- Auto-create GitHub Release berisi APK debug tiap build sukses

### Fixed
- Permission `contents: write` pada workflow agar step pembuatan Release tidak gagal dengan error 403

## [0.3.0] - Syntax Highlighting & Auto-complete

### Added
- Syntax highlighting PAWN custom (`pawnLanguage.js`) — keyword, tipe data, string, comment, angka, dan function call
- Auto-complete/IntelliSense (`pawnCompletion.js`) — 30+ fungsi umum SA-MP/Open.MP beserta deskripsi parameter, dan snippet struktur kode (`if`, `for`, callback `OnPlayer*`, dll)

## [0.2.0] - File Management System

### Added
- Sidebar File Explorer — buat, buka, dan hapus file/folder
- Sistem multi-tab dengan indikator unsaved changes (dirty state)
- `fileManager.js` — modul abstraksi storage berbasis `localStorage`, didesain agar mudah diganti ke `@capacitor/filesystem` tanpa mengubah `main.js`
- Keyboard shortcut Ctrl+S untuk save

### Changed
- `index.html` dan `style.css` dirombak untuk mendukung layout sidebar + tab bar

## [0.1.0] - Initial Setup

### Added
- Struktur dasar `index.html`, `style.css`, `main.js`
- Integrasi Monaco Editor via CDN (AMD loader)
- Tema gelap ala VSCode, full-screen layout
- Auto-restore draft terakhir dari `localStorage`
