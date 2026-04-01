# Edutrack
Pembantu untuk belajar 
<!DOCTYPE html><html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aplikasi Pengumpulan Tugas</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 700px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
    }
    button {
      background: black;
      color: white;
      cursor: pointer;
    }
    .task {
      border: 1px solid #ddd;
      padding: 12px;
      margin-top: 10px;
      border-radius: 10px;
    }
    .done {
      color: green;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Aplikasi Pengumpulan Tugas Sekolah</h2><input type="text" id="nama" placeholder="Nama Tugas">
<input type="text" id="mapel" placeholder="Mata Pelajaran">
<input type="date" id="deadline">
<input type="text" id="link" placeholder="Link Google Drive / File">
<button onclick="tambahTugas()">Tambah Tugas</button>

<div id="daftarTugas"></div>

  </div>  <script>
    let tugas = [];

    function tambahTugas() {
      const nama = document.getElementById('nama').value;
      const mapel = document.getElementById('mapel').value;
      const deadline = document.getElementById('deadline').value;
      const link = document.getElementById('link').value;

      if (!nama || !mapel || !deadline) {
        alert('Isi semua data tugas terlebih dahulu!');
        return;
      }

      tugas.push({ nama, mapel, deadline, link, status: 'Belum Dikumpulkan' });
      tampilkanTugas();

      document.getElementById('nama').value = '';
      document.getElementById('mapel').value = '';
      document.getElementById('deadline').value = '';
      document.getElementById('link').value = '';
    }

    function kumpulkan(index) {
      tugas[index].status = 'Sudah Dikumpulkan';
      tampilkanTugas();
    }

    function tampilkanTugas() {
      const daftar = document.getElementById('daftarTugas');
      daftar.innerHTML = '';

      tugas.forEach((item, index) => {
        daftar.innerHTML += `
          <div class="task">
            <p><b>Tugas:</b> ${item.nama}</p>
            <p><b>Mapel:</b> ${item.mapel}</p>
            <p><b>Deadline:</b> ${item.deadline}</p>
            <p><b>Status:</b> <span class="${item.status === 'Sudah Dikumpulkan' ? 'done' : ''}">${item.status}</span></p>
            ${item.link ? `<p><a href="${item.link}" target="_blank">Lihat File</a></p>` : ''}
            ${item.status === 'Belum Dikumpulkan' ? `<button onclick="kumpulkan(${index})">Kumpulkan</button>` : ''}
          </div>
        `;
      });
    }
  </script></body>
</html>
