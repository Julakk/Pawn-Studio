# Pemberitahuan Pihak Ketiga

PawnStudio memakai atau membundel komponen berikut. Hak cipta dan lisensi tiap
komponen dimiliki pemiliknya masing-masing, dan teks lengkap lisensinya ada di
repo asal.

| Komponen | Lisensi | Sumber |
|---|---|---|
| Monaco Editor | MIT | https://github.com/microsoft/monaco-editor |
| Emmet | MIT | https://github.com/emmetio/emmet |
| Capacitor | MIT | https://github.com/ionic-team/capacitor |
| JSZip | MIT (dual MIT/GPLv3, dipakai di bawah MIT) | https://github.com/Stuk/jszip |
| JGit | Eclipse Distribution License v1.0 (BSD-3-Clause) | https://github.com/eclipse-jgit/jgit |
| Node.js dan nodejs-mobile | MIT | https://github.com/nodejs-mobile/nodejs-mobile |
| npm | Artistic License 2.0 | https://github.com/npm/cli |
| Pawn compiler (`pawncc`) | Lisensi Pawn (lihat repo asal) | https://github.com/pawn-lang/compiler |
| omp-stdlib (include open.mp) | MPL-2.0 | https://github.com/openmultiplayer/omp-stdlib |
| Include SA-MP standar (`a_samp.inc`, dll) | Lihat repo asal | https://github.com/pawn-lang/samp-stdlib |

## Catatan modifikasi

- `a_samp.inc` yang dibundel telah dimodifikasi: native khusus 0.3.DL
  (`AddCharModel`, `AddSimpleModel`, `AddSimpleModelTimed`,
  `FindModelFileNameFromCRC`, `FindTextureFileNameFromCRC`, `RedirectDownload`)
  dibungkus kondisi `#if !defined SAMP_TARGET_037`. File include dibundel dalam
  bentuk teks, jadi bisa dibaca langsung.
