# Context Engineering

> Disiplin memastikan agen memiliki informasi yang tepat pada waktu yang tepat di jendela konteksnya. Subset dari [[Harness Engineering]] — cakupannya jendela konteks model, bukan seluruh sistem agen.

## Dua jenis konteks
- **Statis:** dokumentasi repo (spesifikasi arsitektur, kontrak API, panduan gaya), [[AGENTS.md]]/[[CLAUDE.md]], dokumen desain tervalidasi linter
- **Dinamis:** log/metrik/trace, pemetaan struktur repo saat startup, status CI/CD & hasil tes

Tip: pemetaan direktori saat startup (seperti yang dipakai LangChain) naikkan skor benchmark tanpa mengganti model.

## Aturan kritis
Apa yang tidak bisa diakses agen dalam konteksnya = **tidak ada**. Pengetahuan di Slack, Google Docs, atau kepala orang tidak terlihat oleh sistem.

→ Konsekuensi: **repositori harus satu-satunya [[Single Source of Truth]]**.

## Dinamika konteks jangka panjang (Databricks)
Model tidak menyimpan memori di luar context window; harness yang mengatur:
- **Dalam satu tugas:** *context compaction* — saat percakapan memanjang, ringkas/trim bagian lama agar model tidak kewalahan. Kegagalannya: [[Mode Kegagalan Harness#Context rot]].
- **Lintas sesi:** simpan & ambil riwayat relevan sehingga agen bisa melanjutkan pekerjaan dengan kesadaran atas apa yang sudah dilakukan (workspace file bersama, bukan cuma chat).

## Instrumen nyata
- [[AGENTS.md]] / [[CLAUDE.md]] / `.cursorrules` — aturan proyek yang dibaca agen
- LLM-based dokumentasi yang divalidasi linter (docs-as-code)
- Data observability yang diakses agen (bukan hanya dasbor manusia)

**Tautan keluar:** [[Harness Engineering]] · [[AGENTS.md]] · [[Single Source of Truth]] · [[Komponen Harness]] · [[Mode Kegagalan Harness]]
