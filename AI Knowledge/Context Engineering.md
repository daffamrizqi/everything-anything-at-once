# Context Engineering

> Disiplin memastikan agen memiliki informasi yang tepat pada waktu yang tepat di jendela konteksnya. Subset dari [[Harness Engineering]] — cakupannya jendela konteks model, bukan seluruh sistem agen.

## Dua jenis konteks
- **Statis:** dokumentasi repo (spesifikasi arsitektur, kontrak API, panduan gaya), [[AGENTS.md]]/[[CLAUDE.md]], dokumen desain tervalidasi linter
- **Dinamis:** log/metrik/trace, pemetaan struktur repo saat startup, status CI/CD & hasil tes

Tip: pemetaan direktori saat startup (seperti yang dipakai LangChain) naikkan skor benchmark tanpa mengganti model.

## Aturan kritis
Apa yang tidak bisa diakses agen dalam konteksnya = **tidak ada**. Pengetahuan di Slack, Google Docs, atau kepala orang tidak terlihat oleh sistem.

→ Konsekuensi: **repositori harus satu-satunya [[Single Source of Truth]]**.

## Instrumen nyata
- [[AGENTS.md]] / [[CLAUDE.md]] / `.cursorrules` — aturan proyek yang dibaca agen
- LLM-based dokumentasi yang divalidasi linter (docs-as-code)
- Data observability yang diakses agen (bukan hanya dasbor manusia)

**Tautan keluar:** [[Harness Engineering]] · [[AGENTS.md]] · [[Single Source of Truth]]
