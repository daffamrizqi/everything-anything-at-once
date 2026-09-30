# Single Source of Truth

> Prinsip bahwa satu sumber data (biasanya repositori kode) adalah tempat KEBENARAN tunggal untuk keputusan, konvensi, dan dokumentasi — sumber lain (Slack, Google Docs, Confluence, kepala orang) adalah kebocoran yang harus disinkronkan.

## Mengapa krusial untuk [[AI Agent]]
Aturan di [[Harness Engineering#Context Engineering]]: apa yang tidak bisa diakses agen dalam konteksnya = **tidak ada**. Jika keputusan arsitektur hanya ada di Confluence atau kepala orang, harness punya **celah** — agen akan melanggar aturan yang tidak pernah ia lihat.

## Praktik
- Semua dokumentasi proyek di repo, terbaca mesin ([[Documentation as Code]])
- Docs tervalidasi linter agar tidak menyimpang dari kode
- Keputusan arsitektur → dokumen desain yang saling tertaut di repo

**Tautan keluar:** [[Harness Engineering]] · [[Context Engineering]] · [[AGENTS.md]] · [[Documentation as Code]]
