# kosbos-uptime

Cek berkala https://www.kosbos.com/api/health dari GitHub Actions, di luar Vercel.

Saat endpoint gagal, workflow membuka satu issue berlabel `uptime-down`. Saat pulih, issue itu dikomentari dan ditutup. Selama masih mati tidak ada alarm ulang.

Uji notifikasi: jalankan workflow secara manual dengan input `url` berisi URL yang gagal. Uji memakai label `uptime-uji`, jadi tidak mengganggu status produksi.

## Pemicu 15 menit (rantai)

Jadwal `schedule` GitHub di repo ini hanya terpicu tiap 5–8 jam, jadi pemicu utamanya adalah rantai: tiap run berjudul `rantai` mengecek, menunggu 15 menit lewat wait timer environment `jeda-15-menit`, lalu memicu run berikutnya. Run terjadwal (`jaga`) menyalakan rantai lagi bila putus.

- Cek rantai hidup: `gh run list -R farusfa-hub/kosbos-uptime --limit 5` (harus ada run `rantai` berstatus `waiting`, dan run `rantai` terakhir berumur kurang dari 20 menit).
- Nyalakan manual: `gh workflow run uptime.yml -R farusfa-hub/kosbos-uptime -f rantai=1`.
- Hentikan: batalkan run `rantai` yang sedang `waiting` dan nonaktifkan workflow.
