# PRD: porter-strategy-analysis

Diperbarui: 2026-10-10 · Status: live · Repo: https://github.com/rizkiadpra/porter-strategy-analysis

## Masalah dan tujuan
Evaluasi strategi sebuah produk, paket, atau inisiatif sering berhenti di klaim seperti "terbaik" atau "terlengkap", tanpa pilihan nyata tentang siapa yang dilayani dan apa yang sengaja dikorbankan. Analisis yang dibuat agen AI tanpa kerangka cenderung berupa daftar observasi lepas yang terdengar rapi tetapi tidak bisa diuji.

Skill ini memberi agen kerangka kerja Michael Porter, sebagaimana dijabarkan Joan Magretta di buku "Understanding Michael Porter", dengan urutan langkah yang tetap. Skill menganalisis, menguji, dan membantu merancang strategi kompetitif.

Kondisi berhasil: agen memakai kerangka ini saat percakapan menyentuh topik strateginya, menyajikan hasil mengikuti lima langkah secara eksplisit, menandai red flag yang terdeteksi, dan menyatakan terus terang bila data belum cukup untuk menyimpulkan.

## Pengguna
Pemilik produk atau pendiri yang ingin menguji apakah sebuah inisiatif punya diferensiasi yang nyata. Analis strategi yang menyusun value proposition atau memetakan value chain. Agen AI di harness yang memuat skill ini (Claude Code dan harness lain yang membaca folder skill), yang menjalankan instruksinya atas permintaan salah satu peran di atas. Instruksi skill berbahasa Indonesia.

## Lingkup saat ini
Memuat satu skill, `SKILL.md`, dengan isi berikut.
- Menjelaskan prinsip inti: kompetisi untuk menjadi unik, dan definisi sempit keunggulan kompetitif (harga relatif lebih tinggi atau biaya relatif lebih rendah).
- Menjalankan analisis Five Forces di level industri dalam lima langkah, dari batas industri sampai tren tiap force.
- Menjalankan Five Tests of Strategy di level unit bisnis atau inisiatif: value proposition, value chain dan biaya relatif, trade-off, fit, continuity.
- Mengaudit pola varian paket atau kontrak lewat klasterisasi kebutuhan inti (Langkah 0), sebelum value proposition didefinisikan.
- Menguji trade-off bersamaan dengan perancangan value chain, bukan sesudahnya.
- Memetakan fit lewat activity map dan tiga jenis fit: konsistensi, penguatan timbal balik, substitusi.
- Memeriksa tiga kondisi genuine sebelum menyarankan pivot.
- Mendaftar red flag per tahap, termasuk straddling dan mission creep.
- Menetapkan format output lima bagian dan kewajiban menyatakan data yang belum cukup.
- Aktif otomatis lewat frasa pemicu di deskripsi (value proposition, trade-off, fit, five forces, competitive advantage, positioning strategis, pressure-test), tanpa perlu menyebut nama Porter.

## Di luar lingkup
Skill tidak menyediakan skrip, template dokumen, atau data pasar. Isinya hanya instruksi untuk agen, sehingga data industri dan angka kompetitor harus datang dari pengguna.

Repo tidak memuat folder references, docs, atau contoh keluaran. Belum ada alasan tertulis di repo mengapa semua materi ditaruh di satu file.

## Ukuran keberhasilan
Belum ditetapkan angka apa pun, dan repo tidak mencatat jumlah pengguna atau frekuensi pemakaian. Tanda kualitatif yang bisa diamati:
- Agen memicu skill pada permintaan strategi tanpa disebut nama Porter.
- Keluaran mengikuti urutan lima langkah dan menunjukkan proses klasterisasi bila ada data mentah.
- Agen menolak value proposition "terbaik" tanpa spesifikasi, dan menyebut red flag secara eksplisit.
- Agen mengakui data yang kurang, tidak mengisinya dengan asumsi.

## Arsitektur dan stack ringkas
Satu repo berisi satu skill. `SKILL.md` (frontmatter `name` dan `description`, lalu instruksi markdown) adalah sumber tunggal.
`README.md` menjelaskan isi dan cara instal. `AGENTS.md` memuat catatan agen, `CLAUDE.md` hanya mengimpor `AGENTS.md`, `HANDOFF.md` menyimpan status terbaru.
Tidak ada kode, dependensi, atau build. Aturan penyuntingan: jaga frontmatter tetap valid.

## Deploy dan lingkungan
Untuk repo ini, deploy berarti memasang atau menautkan skill ke harness agen dan mendorong ke GitHub.

| | |
|---|---|
| Produksi | Salinan terpasang di `~/.agents/skills/porter-strategy-analysis` (Mac lokal), isi `SKILL.md` identik dengan repo per 2026-10-10. Skill bernama sama juga muncul sebagai `anthropic-skills:porter-strategy-analysis` |
| Hosting | GitHub, rizkiadpra/porter-strategy-analysis. Tidak ada server |
| Data | Tidak ada. Tidak ada rahasia atau variabel lingkungan |
| Cara deploy | Menurut README: `git clone https://github.com/rizkiadpra/porter-strategy-analysis.git ~/.claude/skills/porter-strategy-analysis`. Pembaruan: tarik perubahan lalu salin atau tautkan ke harness |
| Deploy terakhir | Belum diketahui. Commit isi terakhir 2026-08-26, 0cd62cd. Commit terbaru repo 2026-09-25, 18ba0fc (hanya HANDOFF.md) |

## Riwayat rilis
| Tanggal | Versi / commit | Perubahan |
|---|---|---|
| 2026-09-25 | 18ba0fc | Menambah HANDOFF.md untuk kelanjutan lintas harness. Isi skill tidak berubah |
| 2026-08-26 | 0cd62cd | Menambah skill porter-strategy-analysis (SKILL.md dan README.md) |

Repo tidak memakai nomor versi. Tanggal pemasangan ke harness tidak tercatat, jadi baris di atas berasal dari commit, bukan dari catatan deploy.

## Keputusan produk
- Dua alat dipisah menurut levelnya: Five Forces untuk industri, Five Tests untuk unit bisnis atau inisiatif. Keduanya tidak dicampur.
- Urutan Five Tests tetap, dan trade-off diuji bersamaan dengan value chain, bukan sesudahnya.
- Value proposition didefinisikan di level segmen kebutuhan, bukan per fitur dan bukan otomatis per kontrak.
- Langkah 0 (audit pola) wajib bila data berupa varian paket atau kontrak, dan prosesnya ditunjukkan ke pengguna.
- Data yang belum cukup dinyatakan terus terang, bukan diisi asumsi.
- Instruksi berbahasa Indonesia.

## Risiko dan pertanyaan terbuka
- Angka peluang peniruan (90%, sekitar 66%, sekitar 59%) tertulis di SKILL.md tanpa rujukan halaman. Sebaiknya dicek ke buku sebelum dikutip sebagai fakta.
- Sumber isi adalah satu buku, dan repo tidak mencatat apakah isinya sudah dicek ulang ke buku itu.
- Skill bernama sama ada di `anthropic-skills`. Belum diketahui mana yang dimuat bila keduanya aktif, dan apakah isinya sama.
- Metode instal di README menempatkan skill di `~/.claude/skills`, sedangkan salinan terpasang yang ditemukan ada di `~/.agents/skills`. Cara pemasangan salinan itu tidak terdokumentasi.
- Tidak ada uji atau contoh keluaran, sehingga kualitas pemicu otomatis dan format output belum bisa diverifikasi dari repo.

## Backlog
Belum ada backlog yang disepakati. HANDOFF.md mencatat tidak ada pekerjaan berjalan atau langkah berikutnya.
