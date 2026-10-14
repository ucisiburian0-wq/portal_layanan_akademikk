<?php
require __DIR__ . '/config.php';

$layanan = db()->query('SELECT id, nama, deskripsi, estimasi FROM layanan WHERE aktif = 1 ORDER BY id')->fetchAll();
$idValid = array_map('intval', array_column($layanan, 'id'));

$lama = ['nama' => '', 'nim' => '', 'email' => '', 'layanan_id' => (int)($_GET['layanan'] ?? 0),
         'cara_ambil' => 'loket', 'keperluan' => '', 'setuju' => ''];
$galat = [];

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $lama = [
        'nama' => trim((string)($_POST['nama'] ?? '')),
        'nim' => trim((string)($_POST['nim'] ?? '')),
        'email' => trim((string)($_POST['email'] ?? '')),
        'layanan_id' => (int)($_POST['layanan'] ?? 0),
        'cara_ambil' => (string)($_POST['ambil'] ?? ''),
        'keperluan' => trim((string)($_POST['keperluan'] ?? '')),
        'setuju' => isset($_POST['setuju']) ? '1' : '',
    ];
    if (!csrf_cek()) { $galat['umum'] = 'Sesi formulir kedaluwarsa. Muat ulang halaman lalu coba lagi.'; }
    $n = mb_strlen($lama['nama']);
    if ($n < 3 || $n > 80) { $galat['nama'] = 'Nama harus 3–80 karakter.'; }
    if (!preg_match('/^[0-9]{10,12}$/', $lama['nim'])) { $galat['nim'] = 'NIM harus berupa angka 10–12 digit.'; }
    if (!filter_var($lama['email'], FILTER_VALIDATE_EMAIL) || mb_strlen($lama['email']) > 120) { $galat['email'] = 'Format email tidak valid, contoh: nama@gmail.com.'; }
    if (!in_array($lama['layanan_id'], $idValid, true)) { $galat['layanan-pilih'] = 'Pilih salah satu jenis layanan.'; }
    if (!in_array($lama['cara_ambil'], ['loket', 'pdf'], true)) { $lama['cara_ambil'] = 'loket'; }
    $k = mb_strlen($lama['keperluan']);
    if ($k < 10 || $k > 300) { $galat['keperluan'] = 'Keperluan harus 10–300 karakter (sekarang ' . $k . ').'; }
    if ($lama['setuju'] !== '1') { $galat['setuju'] = 'Centang pernyataan kebenaran data.'; }

    if (!$galat) {
        $kode = kode_tiket();
        $sql = 'INSERT INTO permohonan (kode_tiket, nama, nim, email, layanan_id, cara_ambil, keperluan) VALUES (?,?,?,?,?,?,?)';
        db()->prepare($sql)->execute([$kode, $lama['nama'], $lama['nim'], $lama['email'], $lama['layanan_id'], $lama['cara_ambil'], $lama['keperluan']]);
        $_SESSION['sukses'] = ['kode' => $kode, 'nim' => $lama['nim']];
        header('Location: index.php#permohonan');   // Post/Redirect/Get: cegah kirim ganda saat refresh
        exit;
    }
}
$sukses = $_SESSION['sukses'] ?? null;
unset($_SESSION['sukses']);

function atribut(array $g, string $id, string $bantu = ''): string {
    $ids = trim($bantu . (isset($g[$id]) ? ' galat-' . $id : ''));
    return ($ids !== '' ? ' aria-describedby="' . $ids . '"' : '') . (isset($g[$id]) ? ' aria-invalid="true"' : '');
}
function pesan(array $g, string $id): string {
    return isset($g[$id]) ? '<p class="galat" id="galat-' . e($id) . '">' . e($g[$id]) . '</p>' : '';
}

$halaman = 'beranda';
$judul = 'Portal Layanan Akademik';
require __DIR__ . '/includes/atas.php';
?>
  <main id="konten-utama" class="wadah">
    <section id="beranda" class="intro" aria-labelledby="judul-intro">
      <h1 id="judul-intro">Urus keperluan akademik tanpa antre di loket</h1>
      <p>Pilih layanan, isi formulir, lalu catat kode tiket Anda. Status permohonan dapat dipantau kapan saja di halaman Cek status. Proses umumnya 1–3 hari kerja.</p>
      <dl class="info">
        <div><dt>Jam layanan</dt><dd>Senin–Jumat, 08.00–15.00 WIT</dd></div>
        <div><dt>Lokasi pengambilan</dt><dd>Bagian Akademik FST, Kampus Poka, Ambon</dd></div>
      </dl>
    </section>

    <section id="layanan" aria-labelledby="judul-layanan">
      <h2 id="judul-layanan">Layanan tersedia</h2>
      <div class="kartu-grid">
        <?php foreach ($layanan as $l): ?>
        <article class="kartu">
          <h3><?= e($l['nama']) ?></h3>
          <p><?= e($l['deskripsi']) ?></p>
          <p class="kartu__meta">Estimasi: <?= e($l['estimasi']) ?></p>
          <a class="tombol tombol--garis" href="index.php?layanan=<?= (int)$l['id'] ?>#permohonan">Ajukan <?= e($l['nama']) ?></a>
        </article>
        <?php endforeach; ?>
      </div>
    </section>

    <section id="permohonan" aria-labelledby="judul-form">
      <h2 id="judul-form">Formulir permohonan</h2>

      <?php if ($sukses): ?>
      <div class="sukses" role="status">
        <p><strong>Permohonan berhasil dikirim.</strong> Simpan kode tiket berikut:</p>
        <p class="kode"><?= e($sukses['kode']) ?></p>
        <p><a href="status.php?kode=<?= e(urlencode($sukses['kode'])) ?>&amp;nim=<?= e(urlencode($sukses['nim'])) ?>">Lihat status permohonan</a></p>
      </div>
      <?php endif; ?>

      <?php if ($galat): ?>
      <div class="ringkas" role="alert" tabindex="-1">
        <h3>Formulir belum dapat dikirim</h3>
        <ul>
          <?php foreach ($galat as $id => $teks): ?>
            <li><?= $id === 'umum' ? e($teks) : '<a href="#' . e($id) . '">' . e($teks) . '</a>' ?></li>
          <?php endforeach; ?>
        </ul>
      </div>
      <?php endif; ?>

      <p>Kolom bertanda <span aria-hidden="true">*</span><span class="sr-only">bintang</span> wajib diisi.</p>

      <form class="form" action="index.php#permohonan" method="post">
        <?= csrf_input() ?>
        <div class="bidang">
          <label for="nama">Nama lengkap <span aria-hidden="true">*</span></label>
          <input type="text" id="nama" name="nama" autocomplete="name" required minlength="3" maxlength="80" value="<?= e($lama['nama']) ?>"<?= atribut($galat, 'nama') ?>>
          <?= pesan($galat, 'nama') ?>
        </div>

        <div class="bidang">
          <label for="nim">NIM <span aria-hidden="true">*</span></label>
          <input type="text" id="nim" name="nim" inputmode="numeric" required pattern="[0-9]{10,12}" maxlength="12" value="<?= e($lama['nim']) ?>"<?= atribut($galat, 'nim', 'bantu-nim') ?>>
          <p class="bantu" id="bantu-nim">Angka saja, 10–12 digit.</p>
          <?= pesan($galat, 'nim') ?>
        </div>

        <div class="bidang">
          <label for="email">Email aktif <span aria-hidden="true">*</span></label>
          <input type="email" id="email" name="email" autocomplete="email" required maxlength="120" value="<?= e($lama['email']) ?>"<?= atribut($galat, 'email', 'bantu-email') ?>>
          <p class="bantu" id="bantu-email">Notifikasi status permohonan dikirim ke alamat ini.</p>
          <?= pesan($galat, 'email') ?>
        </div>

        <div class="bidang">
          <label for="layanan-pilih">Jenis layanan <span aria-hidden="true">*</span></label>
          <select id="layanan-pilih" name="layanan" required<?= atribut($galat, 'layanan-pilih') ?>>
            <option value="">Pilih layanan</option>
            <?php foreach ($layanan as $l): ?>
              <option value="<?= (int)$l['id'] ?>"<?= (int)$l['id'] === $lama['layanan_id'] ? ' selected' : '' ?>><?= e($l['nama']) ?></option>
            <?php endforeach; ?>
          </select>
          <?= pesan($galat, 'layanan-pilih') ?>
        </div>

        <fieldset class="bidang bidang--penuh">
          <legend>Cara pengambilan dokumen</legend>
          <div class="pilihan">
            <input type="radio" id="ambil-loket" name="ambil" value="loket"<?= $lama['cara_ambil'] === 'loket' ? ' checked' : '' ?>>
            <label for="ambil-loket">Ambil di Bagian Akademik</label>
          </div>
          <div class="pilihan">
            <input type="radio" id="ambil-pdf" name="ambil" value="pdf"<?= $lama['cara_ambil'] === 'pdf' ? ' checked' : '' ?>>
            <label for="ambil-pdf">Kirim berkas PDF ke email</label>
          </div>
        </fieldset>

        <div class="bidang bidang--penuh">
          <label for="keperluan">Keperluan <span aria-hidden="true">*</span></label>
          <textarea id="keperluan" name="keperluan" rows="4" required minlength="10" maxlength="300"<?= atribut($galat, 'keperluan', 'bantu-keperluan') ?>><?= e($lama['keperluan']) ?></textarea>
          <p class="bantu" id="bantu-keperluan">Jelaskan singkat, 10–300 karakter.</p>
          <?= pesan($galat, 'keperluan') ?>
        </div>

        <div class="bidang bidang--penuh">
          <div class="pilihan">
            <input type="checkbox" id="setuju" name="setuju" value="1" required<?= $lama['setuju'] === '1' ? ' checked' : '' ?><?= atribut($galat, 'setuju') ?>>
            <label for="setuju">Data yang saya isi benar dan dapat dipertanggungjawabkan.</label>
          </div>
          <?= pesan($galat, 'setuju') ?>
        </div>

        <div class="bidang--penuh">
          <button class="tombol" type="submit">Kirim permohonan</button>
          <a class="tombol tombol--garis" href="index.php#permohonan">Kosongkan formulir</a>
        </div>
      </form>
    </section>
  </main>
<?php require __DIR__ . '/includes/bawah.php'; ?>
