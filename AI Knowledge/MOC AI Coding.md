# MOC — AI Coding & Harness

> [!info] Index of notes. Status: seed awal, tautan `[[...]]` menuju note yang akan ditulis (kosong jika belum ada).

## Domain utama
- [[Harness Engineering]] — disiplin di sekeliling agen (<- rangkuman NxCode 2026-03-01 + Databricks 2026-06-17, klaim vendor belum diverifikasi mandiri)
- [[AI Agent]] — sistem otonom, tipe, mode kegagalan khas

## Anatomi harness
- [[Komponen Harness]] — 8 blok pembangun harness produksi (Databricks)
- [[ReAct Loop]] — siklus reason → act → observe
- [[Agent Sprawl]] — masalah skala organisasi & shared harness infrastructure

## Mode kegagalan
- [[Doom Loop]] — agen berputar tanpa kemajuan
- [[Mode Kegagalan Harness]] — 7 kegagalan desain harness produksi (Databricks)

## Prinsip
- [[Single Source of Truth]]
- [[Documentation as Code]]

## Struktur
- [[AGENTS.md]] — file aturan proyek untuk agen
- [[Context Engineering]] — konteks statis & dinamis

## Peta tautan
[[Harness Engineering]] ← covers → [[Context Engineering]] · [[Komponen Harness]] · [[Single Source of Truth]] · [[Documentation as Code]] · [[AGENTS.md]] · [[Doom Loop]] · [[Mode Kegagalan Harness]]
[[AI Agent]] ← target semua di atas ← [[Harness Engineering]] ← [[AI Agent]] (sirkular disengaja, biar graph terhubung)
[[Komponen Harness]] ↔ [[ReAct Loop]] ↔ [[Mode Kegagalan Harness]] — siklus, penyusun, dan titik patahnya
[[Agent Sprawl]] ← skala organisasi dari [[Harness Engineering]]
