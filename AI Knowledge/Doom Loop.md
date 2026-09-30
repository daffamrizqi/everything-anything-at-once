# Doom Loop

> Mode kegagalan [[AI Agent]]: agen berputar melakukan perubahan yang berulang tanpa konvergen — mengedit file yang sama berulang kali, membuang token dan waktu tanpa kemajuan.

## Penanganan dalam [[Harness Engineering]]
- **Loop detection middleware** — melacak pengeditan file yang berulang; LangChain pakai ini untuk lompat Top 30 → Top 5 Terminal Bench 2.0
- **Feedback loop yang jelas** — tanpa umpan balik, agen tidak tahu gagal → "harness tanpa umpan balik adalah sangkar, bukan panduan"
- **Kebijakan eskalasi** (L3) — agen yang macet diserahkan ke manusia

## Sumber umum
- Konteks kurang → agen menebak dan menebak lagi
- Tanpa constraint → agen menjelajahi jalan buntu tanpa batas
- Tanpa verifikasi mandiri sebelum menyatakan "selesai"
- **Context rot + weak verification** (Databricks): riwayat yang membusuk menurunkan kualitas reasoning, dan tanpa loop cek agen mengklaim selesai prematur — kombinasi pemicu langsung doom loop; daftar lengkap: [[Mode Kegagalan Harness]]

**Tautan keluar:** [[AI Agent]] · [[Harness Engineering]] · [[Context Engineering]] · [[Mode Kegagalan Harness]]
