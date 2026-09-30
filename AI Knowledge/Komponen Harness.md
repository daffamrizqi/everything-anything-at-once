# Komponen Harness

> Delapan blok pembangun harness produksi (sumber: [Databricks, "What is an AI Agent Harness?"](https://www.databricks.com/blog/ai-harness), 2026-06-17). Tiap komponen menjawab satu keterbatasan model mentah. Bagian dari [[Harness Engineering]].

## Persamaan dasar
**Agent = Model + Harness.** Model = "otak" (reasoning, keputusan). Harness = "tubuh + ruang kerja" (eksekusi, memori, aturan). Tanpa harness, model bisa menjawab tapi tidak bisa andal menjalankan kode, memanggil API, mengakses file, mengingat pekerjaan sebelumnya, atau menyelesaikan alur multi-langkah.

| Komponen | Peran | Analogi |
| --- | --- | --- |
| Model | Reasoning & generasi output | Otak |
| [[Harness Engineering\|Harness]] | Eksekusi, memori, tools, aturan | Tubuh & workspace |
| [[AI Agent]] | Sistem utuh gabungan keduanya | Pekerja yang berpikir dan bertindak |

## Delapan komponen
1. **System prompt** — instruksi tetap yang dimuat setiap run: identitas, tujuan, aturan. Prompt buruk = penyebab paling umum perilaku tidak konsisten. (Padanan per-proyek: [[AGENTS.md]].)
2. **Tools & tool execution** — model memutuskan tool mana & kapan; harness yang benar-benar menjalankannya. Tren: mundur dari banyak tool sempit → satu kemampuan umum **tulis & eksekusi kode** (workflow dibangun dinamis).
3. **Sandbox / execution environment** — workspace terisolasi agar kode agen tidak menyentuh sistem asli; bisa di-monitor, di-reset, dimatikan; memungkinkan banyak agen paralel.
4. **Filesystem & durable storage** — tempat persisten untuk kode, catatan, plan, kerja antara; agen mengakumulasi progres lintas sesi dan berkolaborasi via file bersama, bukan cuma chat.
5. **Memory & context management** — model tidak ingat di luar context window. Harness mengatur: **context compaction** (ringkas/trim riwayat lama saat percakapan tumbuh) + penyimpanan & retrieval riwayat lintas sesi. Basis: [[Context Engineering]].
6. **Feedback loop & self-verification** — harness mengecek hasil kerja: jalankan tes, inspeksi hasil, minta model review output sendiri sebelum lanjut. Tanpa ini agen berhenti prematur atau mengklaim selesai pada kerja setengah jadi.
7. **Guardrails & human-in-the-loop** — aturan yang memblokir aksi tidak aman: approval manusia sebelum hapus file, kirim pesan pelanggan, pembelian. Wajib di lingkungan enterprise/ter-regulasi.
8. **Observability & logging** — log, trace, dasbor: apa yang agen lakukan, kenapa, di mana salah. Kebutuhan compliance (audit trail: aksi + otoritas) sekaligus input infrastruktur evaluasi berskala ribuan run.

## Kaitan
- Komponen #5–6 = pilar Context & Verify dalam [[Harness Engineering]]; kegagalannya terdaftar di [[Mode Kegagalan Harness]].
- Loop reason→act→observe yang dieksekusi komponen #2–6: [[ReAct Loop]].
- Komponen #3–4 memungkinkan pola *disposable harness* (lihat [[Harness Engineering#Arah ke depan]]).

**Tautan keluar:** [[Harness Engineering]] · [[AI Agent]] · [[Context Engineering]] · [[AGENTS.md]] · [[ReAct Loop]] · [[Mode Kegagalan Harness]]
