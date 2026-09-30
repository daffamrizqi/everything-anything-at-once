# Documentation as Code

> Dokumentasi diperlakukan seperti kode: disimpan di repo, di-review, dan **divalidasi otomatis** oleh linter — bukan sekadar teks statis untuk manusia.

## Dalam [[Harness Engineering]]
- Syarat agar [[Single Source of Truth]] benar-benar kepakai [[AI Agent]] — docs yang hanya bisa dibaca manusia = celah harness
- Dokumen desain yang saling tertaut divalidasi linter (mis. cek link rusak, frasa usang, kontrak API tidak cocok dengan kode)
- Documentation consistency agents (entropy management) memverifikasi docs vs kode saat ini secara berkala

## Praktik nyata (NxCode, dari pengalaman mereka)
"Repositori-pertama": setiap keputusan arsitektur, konvensi penamaan, dan proses deployment ada di repo — tidak ada yang tinggal di Slack/Google Docs.

**Tautan keluar:** [[Harness Engineering]] · [[Single Source of Truth]] · [[AGENTS.md]]
