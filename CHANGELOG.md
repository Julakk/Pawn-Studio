# Changelog

Semua perubahan penting pada project PawnStudio dicatat di file ini.

## [Unreleased]

### Added
- Syntax highlighting PAWN (`pawnLanguage.js`) — keyword, tipe data, string, comment, angka, dan function call

## [0.3.0] - CI/CD Setup

### Added
- Konfigurasi Capacitor (`capacitor.config.json`, `package.json`)
- GitHub Actions workflow (`build.yml`) untuk build APK otomatis tiap push ke `main`
- Auto-create GitHub Release berisi APK debug tiap build sukses

### Fixed
- Permission `contents: write` pada workflow agar step pembuatan Release tidak gagal dengan error 403

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
