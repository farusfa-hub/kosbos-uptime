# kosbos-uptime

Cek berkala https://www.kosbos.com/api/health dari GitHub Actions, di luar Vercel.

Saat endpoint gagal, workflow membuka satu issue berlabel `uptime-down`. Saat pulih, issue itu dikomentari dan ditutup. Selama masih mati tidak ada alarm ulang.

Uji notifikasi: jalankan workflow secara manual dengan input `url` berisi URL yang gagal. Uji memakai label `uptime-uji`, jadi tidak mengganggu status produksi.
