# AGENTS.md

> File markdown di root repositori yang mengodekan aturan, konvensi, dan konteks proyek untuk [[AI Agent]] — standar terbuka; [[CLAUDE.md]] dan `.cursorrules` adalah padanan vendor-spesifik.

## Fungsi dalam [[Harness Engineering]]
- Sumber **konteks statis** paling berdampak — peningkatan harness termurah dan paling efektif
- `AGENTS.md` samar → output agen samar (salah satu kesalahan umum harness ke #3)
- Di L2/tim: berisi konvensi seluruh tim, bukan preferensi individu

## Praktik
- Simpan di repo — jangan di Confluence/Slack; [[Single Source of Truth]]
- [[Documentation as Code]]: tervalidasi deterministically oleh linter, agar tidak menyimpang dari kode
- Agen pembersih periodik (entropy management) memverifikasi isinya sesuai kode saat ini

## Padanan antar vendor
| File | Mesin |
| --- | --- |
| `AGENTS.md` | vendor-agnostik (Codex dll) |
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |

**Tautan keluar:** [[Harness Engineering]] · [[Context Engineering]] · [[Documentation as Code]] · [[Single Source of Truth]]
