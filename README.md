# everything-anything-at-once
cramping everything I wanted to know in md format lol

## Harness Engineering — rangkuman NxCode (2026-03-01)

Sumber: [Harness Engineering: Panduan Lengkap Membangun Sistem yang Membuat Agen AI Benar-benar Bekerja (2026)](https://www.nxcode.io/id/resources/news/harness-engineering-complete-guide-ai-agent-codex-2026)

### Inti
Yang menentukan keandalan coding agent bukan modelnya, tapi *harness*-nya — sistem berisi batasan, loop umpan balik, dokumentasi, dan manajemen siklus hidup di sekeliling model. Tim Codex OpenAI merilis produk 1jt+ baris kode **nol baris tulisan manusia** dalam 5 bulan (~1/10 waktu normal); insinyurnya hanya merancang harness, menentukan niat, memberi feedback.

Harness = 4 fungsi: **Constrain** (batasi ruang gerak agen) → **Inform** (beri konteks yang tepat) → **Verify** (uji output) → **Correct** (feedback loop/perbaikan mandiri). Metafora: model = kuda, harness = tali kekang, insinyur = penunggang. Kutipan Fowler: "perkakas & praktik menjaga agen tetap terkendali" — tapi harness yang baik bikin agen *lebih mampu*, bukan cuma lebih aman.

### Bukti utama: model bukan moat
LangChain naik **52,8% → 66,5%** di Terminal Bench 2.0 (Top 30 → Top 5) tanpa ganti model, hanya ganti harness: self-verification loop, context mapping saat startup, loop detection, reasoning sandwich (penalaran tinggi untuk planning/verifikasi, medium untuk implementasi).

### 3 pilar
1. **Context engineering** — statis (docs, AGENTS.md/CLAUDE.md, desain) dan dinamis (log, metrik, struktur repo). Aturan kritis: apa yang tak bisa diakses agen = tidak ada → **repo harus satu-satunya source of truth** (bukan Slack/Google Docs).
2. **Architectural constraints** — tegakkan secara mekanis, bukan "tulis kode bagus" via prompt. Contoh: pelapisan dependensi `Types → Config → Repo → Service → Runtime → UI` ditegakkan oleh deterministic linter, LLM auditor, structural test, pre-commit hooks. Paradoks: membatasi ruang solusi bikin agen **konvergen lebih cepat** (tidak buang token eksplorasi jalan buntu).
3. **Entropy management** — agen pembersih periodik (konsistensi dokumen, scanner pelanggaran constraint, pattern enforcement, dependency auditor) mencegah docs menyimpang, kode mati, penyimpangan pola.

### Contoh implementasi
- **OpenAI**: insinyur tidak pernah menulis kode; debug = analisis perilaku agen, review = menilai output agen + efektivitas harness.
- **Stripe "Minions"**: >1.000 PR merged/minggu; dev posting tugas di Slack → Minion koding → lolos CI → buka PR → manusia review-merge, tanpa interaksi di antaranya.
- **LangChain**: harness = middleware satu per satu: `LocalContext → LoopDetection → ReasoningSandwich → PreCompletionChecklist` — reusable tanpa menyentuh logika agen inti.

### Tingkatan adopsi
- **L1 solo** = `CLAUDE.md`/`.cursorrules` + pre-commit hooks + test suite (1-2 jam).
- **L2 tim** = + `AGENTS.md` tim, constraint di CI, checklist review khusus PR agen (watch out pola khas agen: abstraksi berlebihan, error handling tidak perlu).
- **L3 organisasi** = + middleware, observability, entropy agents terjadwal, A/B harness, eskalasi saat agen macet.

### 5 kesalahan umum
1. Over-engineering alur kontrol — model berkembang cepat, bikin harness *rippable*/mudah dilepas.
2. Memperlakukan harness statis.
3. Dokumentasi lemah — peningkatan paling berdampak justru paling sederhana.
4. Tanpa feedback loop = "sangkar, bukan panduan".
5. Dokumentasi hanya untuk manusia (keputusan arsitektur di kepala orang/Confluence).

### Posisi vs konsep lain
Mencakup context engineering, lebih tinggi dari prompt/agent engineering — cakupannya **seluruh sistem agen**, bukan satu interaksi. Peran insinyur bergeser: menulis kode → merancang lingkungan, debug kode → debug perilaku agen. Keterampilan inti baru: systems thinking, menegakkan batas, penulisan spesifikasi, observability, kecepatan iterasi.

> Catatan sumber: blog vendor (NxCode) untuk platform no-code mereka sendiri; angka-angka klaim 1jt baris/LangChain dari OpenAI blog dan pihak LangChain sendiri, tidak diverifikasi mandiri.
