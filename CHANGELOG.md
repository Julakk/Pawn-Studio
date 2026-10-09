# Changelog

Semua perubahan penting pada project PawnStudio dicatat di file ini.

## [1.8.0] - 2026-10-10

### Added
- npm di dalam app. Tombol npm di header Explorer: ketik perintah, contoh `install discord.js`, `uninstall express`, `ls`, `init`. npm 10 (JavaScript murni) dibundel di APK dan dijalankan lewat runtime Node.js yang sama, jadi tidak perlu Termux. Paket masuk ke node_modules di folder project aktif dan langsung bisa di-require dari file .js. Explorer dimuat ulang otomatis setelah npm selesai.
- package.json dibuat otomatis kalau belum ada, supaya paket tidak terpasang di folder induk.
- Workflow build.yml membundel npm ke assets APK saat build.

### Changed
- Perintah npm dibatasi: install, i, add, uninstall, remove, rm, update, ls, list, init. Nama paket hanya dari registry npm (tanpa URL atau path). Script lifecycle (preinstall/postinstall) dimatikan dan symlink .bin tidak dibuat, karena Android tidak punya /bin/sh dan penyimpanan eksternal tidak mendukung symlink.
- Label status bar untuk Node/npm dipersingkat (contoh: "✓ Node OK (0.7s)") supaya tidak memotong nama file dan bahasa.
- Tombol di header Explorer diperkecil sedikit supaya kelima tombol (termasuk npm) muat.

### Known Issues
- Paket yang butuh kompilasi native (node-gyp) tidak bisa dipasang. Paket JavaScript murni seperti discord.js dan express adalah target utamanya.
- Butuh internet saat npm install. Belum diuji di perangkat.

## [1.7.0] - 2026-10-09

### Added
- Menjalankan Node.js langsung di dalam app. Runtime Node.js 18 (nodejs-mobile, arm64-v8a) ikut tertanam di APK, jadi tidak perlu Termux atau setup apa pun. Tekan Run di file .js/.mjs/.cjs, output tampil live di panel Output, tekan tombol yang sama lagi (berubah jadi Stop) untuk menghentikan. Proses jalan di folder project aktif.
- Plugin native NodeRunner (status, run, stop) dan launcher android/native/nodeexec.c.
- Workflow build.yml menyiapkan runtime Node.js otomatis saat build (unduh libnode.so, strip, build launcher dengan NDK).

### Changed
- Tombol Run di file Node.js sekarang benar-benar menjalankan file, bukan lagi menampilkan petunjuk. File .ts tetap menampilkan petunjuk (compile ke .js dulu).
- Ukuran APK bertambah karena runtime Node.js ikut dibundel.

### Known Issues
- Hanya arm64-v8a dan Node.js 18; npm belum tersedia (node_modules yang sudah ada di folder project tetap bisa di-require).
- Sebagian modul bawaan yang butuh akses sistem Android (misalnya os.networkInterfaces) bisa gagal. Belum diuji di perangkat.

## [1.6.0] - 2026-10-09

### Added
- Icon folder & file berwarna ala Material Icon Theme (icons.js): gamemodes, filterscripts, plugins, scriptfiles, npcmodes, database, logs, compiled, dan lainnya punya warna + simbol sendiri. File .pwn, .inc, .amx, .dll, .so, .bat, .cfg, .json, .zip, .png juga punya icon sendiri.
- Tombol "..." di tiap item Explorer buat nampilin Rename dan Hapus.
- Dukungan penulisan Node.js: file .mjs, .cjs, dan .ts dikenali. Auto-complete dan hover untuk require/process/Buffer dan modul bawaan Node (fs, path, os, http, https, events, util, child_process, url, crypto, readline), termasuk alias node:. Tipe dimuat hanya saat file JS/TS dibuka.
- Snippet Node.js: req, reqfs, readfile, httpserver, express, discordbot, asyncfn, trycatch.
- Tombol Run di file .js/.mjs/.cjs/.ts menampilkan petunjuk, tidak lagi dikirim ke compiler PAWN. Menjalankan Node.js di dalam app direncanakan untuk versi berikutnya.

### Changed
- Tombol Rename/Hapus di Explorer disembunyikan secara default, cuma tampil di file yang lagi aktif atau item yang diketuk tombol "...". Daftar file jadi lebih rapi dan nama file lebih lega.
- File binary (.dll, .amx, .so) tidak lagi diabu-abukan, icon tetap berwarna dengan opacity 0.85.
- Versi APK dinaikkan ke 1.6.0 (versionCode 25).

## [1.5.9] - 2026-10-09

### Added
- Auto-complete konstanta SA-MP (234 nama, mis. INVALID_PLAYER_ID, DIALOG_STYLE_*, WEAPON_*, KEY_*) lengkap dengan keterangan grup.
- Petunjuk parameter saat kursor di dalam kurung fungsi, parameter yang sedang diisi disorot.
- Hover di nama fungsi dan konstanta.

## [1.5.8] - 2026-10-09

### Added
- Dukungan include open.mp: kode yang memakai <open.mp> atau <omp_*> dicompile dengan include open.mp bawaan (omp-stdlib, MPL-2.0). Kode SA-MP klasik tidak berubah.

## [1.5.7] - 2026-10-08

### Fixed
- Tombol Cari / Ganti: coba beberapa aksi Monaco dan tampilkan pesan jika panel pencarian tidak bisa dibuka.

## [1.5.6] - 2026-10-08

### Added
- Tombol Cari / Ganti di header dan di ikon pencarian sidebar (memakai panel Find/Replace bawaan Monaco).

## [1.5.5] - 2026-10-08

### Fixed
- Label versi di Settings dan Pengaturan Lanjutan sekarang sesuai versi rilis (sebelumnya masih menampilkan v1.5.2 di build 1.5.3 dan 1.5.4).

## [1.5.4] - 2026-10-08

### Added
- Snippet callback baru: OnGameModeExit, OnPlayerDeath, OnPlayerText, OnDialogResponse, OnPlayerEnterVehicle, OnPlayerKeyStateChange.

## [1.5.3] - 2026-10-08

### Changed
- Auto-complete: daftar fungsi SA-MP diperlengkap (player, kendaraan, textdraw, object, server, string, float, PVar, file).

## [1.5.2] - 2026-10-07

### Fixed
- Toolbar simbol numpuk: sebelumnya ada dua bar sekaligus di atas keyboard (`#symbol-bar` lama dan `#v151-bar`), sehingga baris simbol kepotong. Sekarang tinggal satu bar.
- Ikon Settings (gear) di activity bar dan daftar file paling bawah di explorer tidak lagi ketutup toolbar saat toolbar tampil.

### Changed
- Bar simbol lama (`#symbol-bar`) dinonaktifkan, semua simbolnya dipakai lewat `#v151-bar`.
- Toolbar ditambah simbol `_` dan `:`.

## [1.5.1] - 2026-10-07

### Removed
- Fitur Git di dalam app (init, commit, push, pull) beserta plugin native GitPlugin dan dependensi JGit, karena APK dirilis publik.

### Added
- Lisensi MIT (LICENSE.md).
- **Pengecekan pra-compile (preflight)**: sebelum pawncc jalan, app mengecek kurung `{ }` `( )` `[ ]` yang tidak seimbang, pola karakter nyasar seperti `}(;`, dan karakter aneh di nama `#include`. Temuan muncul di panel Output lengkap dengan nomor baris. Pengecekan ini cuma peringatan, compile tetap dijalankan

### Fixed
- Error "Binary compiler tidak ditemukan" saat compile: native library (libpawncc.so) sekarang di-extract ke disk lewat useLegacyPackaging = true.
- Bar simbol: karakter tidak lagi ter-insert saat bar digeser, insert hanya saat tap (sebelumnya bisa menyelipkan `}`, `(`, `;` ke kode dan bikin compile gagal)

### Changed
- Preflight sekarang mendeteksi string/karakter yang belum ditutup.
- Bar simbol: ditambah simbol `" % = / \ , & | ! + - * _ : ' @` dan bisa digeser
- README: fitur dan roadmap disamakan dengan kondisi app

## [1.5.0] - HUD Overhaul (Header, Explorer, Status Bar, Symbol Bar)

### Added
- **Bar simbol di atas keyboard**: tombol cepat `Tab` `{` `}` `;` `(` `)` `[` `]` `#` `<` `>` yang muncul otomatis saat editor difokus. Tombol tidak menutup keyboard, dan simbol diketik lewat Monaco sehingga auto-close bracket tetap jalan
- **Status compile** di status bar: Siap / Compiling... / Compile OK / Compile gagal, lengkap dengan durasi compile
- **Tombol toggle Word Wrap** di status bar (`Wrap: On/Off`), sinkron dengan pengaturan di Settings
- Versi aplikasi ditampilkan di Settings
- Ikon file baru yang lebih jelas per tipe: kode (`.pwn`, `.inc`, `.js`, dll), teks, dan binary

### Changed
- **Word Wrap sekarang mati secara default** (termasuk untuk user lama, lewat migrasi pengaturan satu kali). Baris panjang seperti `#include` tidak lagi terpotong jadi beberapa baris; geser horizontal untuk melihat sisanya
- Header: nama workspace tampil sebagai badge, tombol aksi dirapikan dan rata kanan, tombol Run diberi warna aksen
- Explorer: tombol aksi di header jadi satu baris dengan area tap lebih besar, item file/folder lebih lega, ikon folder berwarna, garis indentasi pada isi folder
- File binary (`.dll`, `.exe`, `.so`, `.amx`, dan sejenisnya) diredupkan agar file kode lebih menonjol
- Badge error/warning di status bar ditampilkan sebagai pill berwarna (merah/kuning) dan bisa diketuk untuk membuka Output Panel
- `windowSoftInputMode` diset `adjustResize` agar layout (termasuk bar simbol) naik mengikuti keyboard
- Versi APK dinaikkan ke `1.5.0` (`versionName` 1.5.0, `versionCode` 15); sebelumnya `versionName` masih `1.0`

## [1.4.0] - Bulk Import & Compiler Include Path

### Added
- Plugin `BulkImport` baru: import folder besar/kompleks pakai izin "All Files Access" (`MANAGE_EXTERNAL_STORAGE`) + `java.io.File` murni, tanpa lewat SAF/DocumentFile yang terbukti tidak reliable untuk folder dengan ribuan entry (misal folder `pawno` penuh)
- Compiler sekarang otomatis mencari folder `include/` dan `pawno/include/` di dalam project sendiri, selain include bawaan PawnStudio — memperbaiki error "cannot read from file" untuk include pihak ketiga (contoh: `a_mysql.inc`)
- Log persisten (`_upload_log.txt`) selama proses extract `.zip`, ditulis per-item dan di-flush langsung ke disk — tetap bisa dibaca walau proses crash di tengah jalan
- Baris `CMD:` di Output Panel menampilkan command compiler lengkap (termasuk semua flag `-i`) untuk memudahkan debug masalah include path

### Fixed
- `FolderPickerPlugin` sekarang copy file byte-per-byte (bukan mode teks), menghilangkan kebutuhan menebak binary/teks dan risiko file ter-corrupt
- Proses extract `.zip` tidak lagi berhenti total kalau 1 file gagal ditulis — lanjut ke file berikutnya dan dicatat sebagai gagal di log

### Known Issues
- Folder dengan ribuan entry kecil (misal folder `pawno` penuh berisi seluruh aplikasi editor Windows) sebaiknya diimport lewat `BulkImport`, bukan upload folder berbasis SAF/zip biasa
- GitHub Actions storage quota bisa penuh kalau build terlalu sering dalam waktu singkat; penghitungan ulang kuota oleh GitHub butuh 6-12 jam setelah menghapus artifact/release lama

## [1.3.0] - Welcome Screen & Problems Indicator

### Added
- Welcome Screen yang muncul saat tidak ada file terbuka: tombol File Baru/Folder Baru, dan daftar Recent Files (5 terakhir)
- Badge jumlah error/warning di status bar, update otomatis setiap kali compile
- Filter ekstensi file di FolderPicker dihapus — sekarang semua jenis file bisa diupload lewat folder picker native (dengan catatan file binary dibaca sebagai teks)


## [1.2.0] - Native Storage Plugin (Major Stability Fix)

### Fixed
- **Bug kritis**: file/folder yang dihapus muncul kembali secara misterius, bahkan setelah uninstall total aplikasi. Setelah investigasi panjang (cek race condition, cek Android Auto Backup, cek Google/Samsung Cloud backup), akar masalah dilacak ke plugin resmi `@capacitor/filesystem` yang tidak konsisten pada operasi delete+recreate+list secara berurutan di Android.

### Changed
- **BREAKING:** Seluruh lapisan penyimpanan file dipindah dari `@capacitor/filesystem` ke plugin native custom (`NativeStoragePlugin.java`) yang menggunakan `java.io.File` secara langsung — tanpa lapisan abstraksi tambahan yang berpotensi menyimpan bug
- `fileManager.js` ditulis ulang total untuk memanggil plugin native ini, dengan signature fungsi yang tetap sama persis (tidak ada perubahan di `main.js`)
- `android:allowBackup` dinonaktifkan di `AndroidManifest.xml` sebagai langkah pencegahan tambahan

### Added
- `data_extraction_rules.xml` untuk mengunci aturan no-backup secara eksplisit di Android 12+


## [1.1.0] - VSCode-style Sidebar & Filesystem Fixes

### Added
- Section "OPEN EDITORS" di sidebar, menampilkan daftar tab yang sedang terbuka (mirror dari tab bar), bisa switch/close langsung dari situ
- Root project folder ("PAWNSTUDIO") kini collapsible dengan chevron, konsisten dengan pola VSCode desktop

### Fixed
- Error `FILE_NOTCREATED` saat upload/extract folder `.zip` — ditambahkan flag `recursive: true` langsung pada setiap pemanggilan `Filesystem.writeFile`, karena `mkdir` saja tidak selalu cukup untuk memastikan direktori induk tersedia saat file ditulis
- Callback inisialisasi utama kini benar-benar `async`/`await` mengikuti Filesystem API, memperbaiki potential race condition yang tersisa dari migrasi storage sebelumnya

## [1.0.0] - Real Filesystem Storage & Full File Management

### Added
- Tombol Upload File dan Upload Folder di File Explorer
- Rename dan delete kini tersedia untuk folder juga, tidak hanya file
- Upload folder mendukung struktur bersarang (nested) lewat ekstraksi `.zip` menggunakan JSZip

### Changed
- **BREAKING:** Storage project dimigrasikan total dari `localStorage` ke `@capacitor/filesystem` — file kini disimpan sebagai file asli di `Documents/PawnStudio/` pada penyimpanan perangkat, bukan lagi terbatas kuota browser (~5-10MB)
- Seluruh fungsi di `fileManager.js` diubah menjadi asynchronous (Promise-based) mengikuti Filesystem API
- JSZip dimuat sebelum AMD loader Monaco untuk mencegah konflik sistem modul

### Fixed
- Error `Setting the value of 'pawnstudio_vfs' exceeded the quota` saat upload folder besar
- Error `Directory is not defined` — enum `Directory`/`Encoding` Capacitor di-hardcode karena tidak tersedia di runtime tanpa bundler
- Error install "Aplikasi tidak terinstal" akibat perbedaan debug signing key antar build CI (workaround: uninstall versi lama sebelum install baru)

### Known Issues
- Upload folder masih memerlukan format `.zip`, belum bisa langsung pilih folder mentah (keterbatasan `webkitdirectory` pada WebView Android)
- Signing key debug build belum konsisten antar build CI — kadang perlu uninstall manual sebelum update

## [0.9.0] - Fully Offline

### Changed
- Monaco Editor dibundel langsung ke dalam APK (folder `www/vs/`), tidak lagi di-load dari CDN eksternal
- App sekarang bisa dibuka dan dipakai 100% offline dari awal — editor, syntax highlighting, auto-complete, hingga compiler — tanpa membutuhkan koneksi internet sama sekali, tervalidasi lewat pengujian Airplane Mode penuh

### Removed
- Dependency ke `cdnjs.cloudflare.com` untuk loading Monaco Editor

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
