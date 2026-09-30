# Agent Sprawl

> Masalah skala organisasi: puluhan agen dibangun lintas tim/workflow/model tanpa pendekatan harness yang konsisten → agen-agen terputus yang tak bisa digovern, dievaluasi, atau ditingkatkan oleh satu pihak mana pun. Sumber: [Databricks, "What is an AI Agent Harness?"](https://www.databricks.com/blog/ai-harness).

## Kenapa jadi masalah kontrol
Saat agen mendekati workflow produksi, dibutuhkan kontrol terpusat atas:
- Akses: apa yang bisa diakses agen, aksi apa yang boleh
- Evaluasi: bagaimana output dinilai terus-menerus (bukan cuma demo)
- Audit: observability + audit trail (kebutuhan compliance di industri teregulasi)
- Fleksibilitas: ganti model tanpa membangun ulang sistem di sekelilingnya

## Jawaban: shared harness infrastructure
Alih-alih tiap tim memelihara harness sendiri, organisasi menyediakan **satu control plane** untuk build, deploy, govern, dan evaluasi agen (contoh produk: Databricks Agent Bricks — governance via Unity Catalog, observability/evaluasi via MLflow, multi-provider OpenAI/Anthropic/Google/open-source).

Padanan konsep di tingkat organisasi = **L3** dalam tingkatan adopsi [[Harness Engineering]] (observability terpusat, entropy agents terjadwal, versi harness + A/B testing).

## Arah ke depan (dari sumber yang sama)
- **Disposable harness** — harness ringan spesifik-tugas, dibuat untuk satu workflow lalu dibuang, bukan infrastruktur long-running; makin praktis karena execution environment makin cepat & murah diprovisi.
- **Natural-language agent harness (NLAH)** — harness dikonfigurasi lewat instruksi bahasa natural, dieksekusi shared runtime; menurunkan siapa yang bisa membangun/memodifikasi harness.

**Tautan keluar:** [[Harness Engineering]] · [[Komponen Harness]] · [[AI Agent]]
