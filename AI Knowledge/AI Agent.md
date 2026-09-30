# AI Agent

> Sistem perangkat lunak yang mengeksekusi tugas secara otonom menggunakan model AI — memutuskan sendiri alat apa yang dipanggil, urutan langkah, dan kapan selesai — dalam batasan yang diberikan [[Harness Engineering|harness]].

## Tipe
- **Coding agent:** Claude Code, Codex, Cursor, Gemini CLI — membaca/mengedit repo, menjalankan tes, memakai CLI
- **Agent runtime/host:** infrastruktur tempat agent berjalan — contoh: Orca (GUI host + server runtime, akun terkelola), herdr (TUI multiplexer agent-native, server background), inpapdi (CLI agent sendiri)

## Sifat khas kode hasil agen (mode kegagalan berbeda dari manusia)
- Abstraksi berlebihan
- Error handling tidak perlu
- Dokumentasi menyimpang dari kode
- [[Doom Loop]] (pengeditan file yang berulang)

Ini yang memotivasi checklist review khusus PR agen dan entropy management dalam [[Harness Engineering]].

**Tautan keluar:** [[Harness Engineering]] · [[Doom Loop]] · [[Context Engineering]]
