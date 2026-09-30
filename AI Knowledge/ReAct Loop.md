# ReAct Loop

> Loop inti [[AI Agent]]: **Reason → Act → Observe → Repeat**. Diperkenalkan pada paper [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) (Shunyu Yao et al., 2022); fondasi mayoritas sistem agen produksi.

## Siklus
1. **Reason** — model membaca seluruh konteks (tugas, memori, hasil sebelumnya), memutuskan aksi berikutnya.
2. **Act** — [[Harness Engineering|harness]] mengeksekusi: jalankan tool, kode di sandbox, panggil API, tulis storage.
3. **Observe** — harness menangkap hasil dan mengembalikannya sebagai konteks baru.
4. **Repeat** — model memakai hasil itu untuk keputusan berikutnya; berhenti saat tugas selesai.

## Contoh (coding agent)
Model mengusulkan perubahan kode → harness menjalankannya di sandbox terisolasi, menangkap hasil tes, mengembalikannya ke model → tes gagal → model menalar penyebab dan mencoba lagi. Harness mengelola interaksi sistem; model fokus menyelesaikan masalah.

## Implikasi harness
- Kualitas loop ditentukan harness, bukan model: kecepatan eksekusi Act, ketepatan Observe (hasil tes/error yang jelas), dan keputusan kapan berhenti.
- Loop tanpa verifikasi ([[Doom Loop]]) atau dengan konteks yang membusuk ([[Mode Kegagalan Harness#Context rot]]) = iterasi tanpa konvergensi.

**Tautan keluar:** [[AI Agent]] · [[Harness Engineering]] · [[Komponen Harness]] · [[Doom Loop]] · [[Mode Kegagalan Harness]]
