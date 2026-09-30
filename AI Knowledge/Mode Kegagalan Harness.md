# Mode Kegagalan Harness

> Mayoritas kegagalan agen produksi berasal dari **harness, bukan model** (sumber: [Databricks, "What is an AI Agent Harness?"](https://www.databricks.com/blog/ai-harness)). Melengkapi [[Doom Loop]] (mode kegagalan perilaku agen) dengan kegagalan desain sistem di sekelilingnya.

## Daftar kegagalan
| Mode | Mekanisme | Mitigasi |
| --- | --- | --- |
| **Context rot** | Riwayat tumbuh → kualitas reasoning menurun; performa runtuh di tugas panjang | Context compaction: trim/ringkas konteks lama ([[Komponen Harness]] #5) |
| **Tool overload** | Terlalu banyak tool sekaligus → kebingungan, lambat memutuskan sebelum kerja dimulai | Kurangi tool sempit → satu kemampuan umum: tulis & eksekusi kode |
| **Brittle tool wiring** | Perubahan kecil pada deskripsi/cara memanggil tool → pemakaian salah → **silent failure** sulit didiagnosis | Kunci kontrak tool; observability |
| **Latency** | Agen multi-langkah dengan banyak tool call bisa >10 detik merespons | Desain loop lebih ramping; paralelisasi |
| **Irrelevant retrieval** | Konteks salah dari memori/search → model yakin menghasilkan jawaban salah | Kurasi retrieval ([[Context Engineering]]) |
| **Weak verification** | Tanpa loop tes/self-check → berhenti prematur atau klaim selesai pada kerja setengah jadi | Self-verification, checklist pra-penyelesaian |
| **Missing guardrails** | Aksi ireversibel (kirim pesan, hapus data, beli) tanpa approval | Human-in-the-loop checkpoint ([[Komponen Harness]] #7) |

## Positif vs perilaku agen
- [[Doom Loop]] = agen berputar tanpa konvergensi (perilaku).
- Di sini = cacat konstruksi harness yang memicu/memperparah perilaku itu (contoh: weak verification + context rot → doom loop).

**Tautan keluar:** [[Harness Engineering]] · [[Komponen Harness]] · [[Doom Loop]] · [[Context Engineering]] · [[AI Agent]]
