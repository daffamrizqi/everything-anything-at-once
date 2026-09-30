# Harness Engineering

> Disiplin merancang lingkungan, batasan, dan loop umpan balik yang membuat [[AI Agent]] pengkodean andal dalam skala produksi.

**Agent = Model + Harness** ([Databricks](https://www.databricks.com/blog/ai-harness)): model = "otak" yang menalar dan memutuskan; harness = "tubuh + workspace" yang mengeksekusi, mengelola memori, menjalankan tools, menegakkan aturan. Tanpa harness, model bisa menjawab tapi tidak andal bertindak. Blok pembangunnya dirinci di [[Komponen Harness]]; siklus kerjanya di [[ReAct Loop]].

**4 fungsi harness:**
1. **Constrain** — batasi ruang gerak agen (batas arsitektural, aturan dependensi)
2. **Inform** — beri konteks yang tepat ([[Context Engineering]], dokumentasi)
3. **Verify** — uji output ([[Automated Testing|pengujian]], linting, validasi CI)
4. **Correct** — feedback loop / perbaikan mandiri

**Metafora:** model = kuda kuat tapi tidak tahu arah; harness = tali kekang; insinyur = penunggang yang memberi arah, bukan yang berlari. Kutipan Martin Fowler: *"perkakas dan praktik yang menjaga agen AI tetap terkendali"* — tapi harness yang baik membuat agen **lebih mampu**, bukan sekadar lebih terkontrol.

## Bukti inti: model bukan moat

Yang menentukan keandalan coding agent bukan modelnya, tapi sistem di sekelilingnya.

- **OpenAI / Codex**: produk produksi 1jt+ baris kode, **0 baris tulisan manusia**, 5 bulan (~1/10 waktu normal). Insinyur hanya merancang harness, menentukan niat, memberi feedback.
- **LangChain**: skor Terminal Bench 2.0 naik **52,8% → 66,5%** (Top 30 → Top 5) **tanpa mengganti model** — hanya mengubah harness:
	- Self-verification loop (checklist pra-penyelesaian)
	- Context mapping struktur repo saat startup
	- Loop detection (mencegah "doom loops")
	- Reasoning sandwich (penalaran tinggi untuk planning/verifikasi, medium untuk implementasi)

- **Databricks**: GPT-5.5 + OfficeQA Pro Agent Harness (tugas dokumen enterprise multi-bagian) → skor **52,63%, naik dari 36,10%** dengan GPT-5.4 — error nyaris terpangkas separuh. Model membaik, tapi *harness yang menerjemahkan peningkatan itu* jadi performa produksi. Kesimpulan umum: model yang sama bisa dapat skor benchmark sangat berbeda tergantung harness; harness kuat di model kelas menengah dapat mengungguli harness lemah di model lebih kuat.

**8 blok pembangun harness produksi** (Databricks) → dipetakan ke pilar di bawah: system prompt, tools & tool execution, sandbox, filesystem/durable storage, memory & context compaction, feedback loop/self-verification, guardrails & human-in-the-loop, observability & logging. Rincian tiap blok: [[Komponen Harness]]. Mode gagal khasnya: [[Mode Kegagalan Harness]].

## Tiga pilar

### 1. Context Engineering ← [[Context Engineering]]
- **Statis:** dokumentasi repo (spesifikasi arsitektur, kontrak API, panduan gaya), [[AGENTS.md]]/[[CLAUDE.md]], dokumen desain tervalidasi linter
- **Dinamis:** log/metrik/trace, pemetaan direktori saat startup, status CI/CD
- **Aturan kritis:** apa yang tidak bisa diakses agen = tidak ada. **Repositori harus satu-satunya [[Single Source of Truth]]** — bukan Slack, Google Docs, atau kepala orang.

### 2. Architectural Constraints
Tegakkan secara mekanis, bukan "tulis kode bagus" via prompt:
- Deterministic linter
- LLM-based auditor (agen meninjau kode agen lain)
- Structural tests (semacam ArchUnit untuk kode hasil AI)
- Pre-commit hooks

Contoh pelapisan dependensi: `Types → Config → Repo → Service → Runtime → UI` — hanya boleh impor dari kiri; ditegakkan CI, bukan sekadar saran.

**Paradoks produktivitas:** membatasi ruang solusi membuat agen *konvergen lebih cepat* — tanpa batas, agen buang token eksplorasi jalan buntu.

### 3. Entropy Management ("Garbage Collection")
Komponen paling kurang dihargai. Kode hasil AI mengakumulasi entropi: docs menyimpang, kode mati, pola terpecah. Jawabannya **agen pembersih periodik** (harian/mingguan/event-triggered):
- Documentation consistency agents
- Constraint violation scanners
- Pattern enforcement agents
- Dependency auditors

## Contoh implementasi

| Organisasi | Pendekatan | Hasil |
| --- | --- | --- |
| OpenAI | Nol kode manusia; insinyur merancang harness, review = nilai output agen + efektivitas harness; debug = analisis perilaku agen | 1jt+ baris produksi |
| Stripe (Minions) | Dev posting tugas di Slack → Minion koding → lolos CI → buka PR → manusia review-merge; tanpa interaksi di antaranya | >1.000 PR merged/minggu |
| LangChain | Harness sebagai middleware composable: `LocalContext → LoopDetection → ReasoningSandwich → PreCompletionChecklist` | Modular, dapat diuji |

## Tingkatan adopsi

- **L1 — solo (1-2 jam):** `CLAUDE.md`/`.cursorrules`, pre-commit hooks, test suite yang bisa dijalankan agen, struktutr direktori konsisten
- **L2 — tim 3-10 orang (1-2 hari):** + `AGENTS.md` konvensi tim, constraint arsitektural di CI, template prompt bersama, docs-as-code tervalidasi linter, checklist review khusus PR agen (watch out pola khas agen: abstraksi berlebihan, error handling tidak perlu, penyimpangan dokumentasi)
- **L3 — organisasi (1-2 minggu):** + middleware custom, observability, entropy agents terjadwal, versi harness + A/B testing, dashboard performa agen, kebijakan eskalasi saat agen macet

## Kesalahan umum

1. **Over-engineering alur kontrol** — model berkembang cepat; pipeline kompleks 2024 bisa jadi satu prompt 2026. Bangun harness **rippable** (mudah dilepas saat model cukup pintar)
2. **Harness dianggap statis** — review ulang komponen tiap rilis model besar
3. **Dokumentasi lemah** — peningkatan paling berdampak justru paling sederhana; `AGENTS.md` samar → output samar
4. **Tanpa feedback loop** — harness tanpa umpan balik adalah *sangkar, bukan panduan*; agen perlu tahu kapan berhasil/gagal
5. **Dokumentasi hanya untuk manusia** — keputusan arsitektur di Confluence/kepala orang = celah harness

## Posisi vs konsep lain

| Konsep | Cakupan | Fokus |
| --- | --- | --- |
| Prompt Engineering | satu interaksi | prompt efektif |
| [[Context Engineering]] | jendela konteks model | informasi yang dilihat model |
| **Harness Engineering** | **seluruh sistem agen** | lingkungan, batasan, feedback, siklus hidup |
| Agent Engineering | arsitektur agen | desain internal & routing |
| Platform Engineering | infrastruktur | deployment, scaling, operasi |

Harness **mencakup** context engineering; ia beroperasi di level di atasnya. Formulasi Databricks: prompt & context engineering keduanya *berada di dalam* harness engineering — evolusi bertahap: prompt (aplikasi LLM awal) → context (era RAG: retrieval pipeline, desain memori) → harness (sistem agentic).

## Arah ke depan (Databricks, 2026-06)
Seiring model makin pintar dalam planning/reasoning multi-langkah/koreksi mandiri, sebagian kerja harness akan bergeser ke dalam model — tapi harness engineering tidak hilang: eksekusi, orkestrasi tool, guardrails, observability tetap menentukan keandalan. Dua ide emerging (detail: [[Agent Sprawl]]):
- **Disposable harness** — harness ringan spesifik-tugas, dibuang setelah pakai, bukan infrastruktur long-running
- **Natural-language agent harness (NLAH)** — harness dikonfigurasi lewat bahasa natural yang dieksekusi shared runtime

Ini sejalan dengan kesalahan umum #1 (over-engineering alur kontrol): bangun **rippable**, bukan permanen.

## Implikasi untuk insinyur

| Sebelum | Sesudah |
| --- | --- |
| Menulis kode | Merancang lingkungan tempat AI menulis kode |
| Debug kode | Debug **perilaku agen** |
| Review kode | Review output agen + efektivitas harness |
| Menulis tes | Merancang strategi pengujian |
| Memelihara docs | Membangun dokumentasi sebagai infrastruktur machine-readable |

Keterampilan inti baru: systems thinking, menegakkan batas, penulisan spesifikasi, observability, kecepatan iterasi harness.

---
> **Catatan sumber:** artikel vendor [NxCode](https://www.nxcode.io/id/resources/news/harness-engineering-complete-guide-ai-agent-codex-2026) (2026-03-01) — vendor platform no-code sendiri. Klaim 1jt baris/LangChain dari blog OpenAI dan LangChain, tidak diverifikasi mandiri.
> Sumber kedua: [Databricks, "What is an AI Agent Harness?"](https://www.databricks.com/blog/ai-harness) (2026-06-17) — definisi, 8 komponen, bukti OfficeQA, arah ke depan.

**Tautan keluar:** [[Context Engineering]] · [[AGENTS.md]] · [[AI Agent]] · [[Single Source of Truth]] · [[Automated Testing]] · [[Komponen Harness]] · [[ReAct Loop]] · [[Mode Kegagalan Harness]] · [[Agent Sprawl]]
