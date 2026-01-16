<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Valorix Nation - Server Minecraft Indonesia</title>
  <style>
    :root {
      --primary: #23ff4b;
      --primary-dark: #1ed13e;
      --bg: #0a120a;
      --card-bg: rgba(15, 35, 15, 0.75);
      --text: #e0ffe0;
      --text-light: #aaffaa;
      --shadow: 0 10px 30px rgba(0,0,0,0.6);
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    html {
      scroll-behavior: smooth;
    }
    body {
      font-family: Arial, Helvetica, sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      overflow-x: hidden;
    }
    /* Header fixed dengan gambar background dari lo */
    .header {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      text-align: center;
      padding: 20px 10px;
      background: linear-gradient(rgba(10,18,10,0.85), rgba(10,18,10,0.7)), url('https://i.imgur.com/M8B8GHv.jpeg') center/cover no-repeat;
      backdrop-filter: blur(8px);
      border-bottom: 1px solid rgba(35,255,75,0.2);
      z-index: 1000;
      transition: all 0.6s ease;
    }
    .header.hidden {
      transform: translateY(-100%);
    }
    h1 {
      font-size: 3rem;
      color: var(--primary);
      text-shadow: 0 0 40px rgba(35,255,75,0.8), 0 0 80px rgba(35,255,75,0.4);
      margin: 0;
      letter-spacing: 4px;
    }
    .tagline {
      font-size: 1.2rem;
      color: var(--text-light);
      margin-top: 6px;
      text-shadow: 0 0 15px rgba(35,255,75,0.5);
    }
    .main-content {
      padding-top: 120px; /* Ruang header fixed */
      min-height: calc(100vh - 120px);
    }
    .menu-container, .content {
      max-width: 1400px;
      margin: 0 auto;
      padding: 20px;
      max-height: calc(100vh - 160px);
      overflow-y: auto;
      scrollbar-width: thin;
      scrollbar-color: var(--primary) rgba(20,40,20,0.5);
    }
    .menu-container::-webkit-scrollbar, .content::-webkit-scrollbar {
      width: 8px;
    }
    .menu-container::-webkit-scrollbar-track, .content::-webkit-scrollbar-track {
      background: rgba(20,40,20,0.5);
    }
    .menu-container::-webkit-scrollbar-thumb, .content::-webkit-scrollbar-thumb {
      background: var(--primary);
      border-radius: 4px;
    }
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 30px;
      margin-top: 40px;
      transition: opacity 1s ease, transform 1s ease;
    }
    .menu-grid.hidden {
      opacity: 0;
      transform: translateY(80px) scale(0.95);
    }
    .menu-btn {
      background: var(--card-bg);
      border: 2px solid rgba(35,255,75,0.3);
      border-radius: 18px;
      padding: 35px 20px;
      text-align: center;
      cursor: pointer;
      transition: all 0.5s cubic-bezier(0.23, 1, 0.32, 1);
      backdrop-filter: blur(12px);
      box-shadow: var(--shadow);
      opacity: 0;
      transform: translateY(60px);
    }
    .menu-btn:nth-child(1) { animation: staggerIn 0.6s forwards 0.1s; }
    .menu-btn:nth-child(2) { animation: staggerIn 0.6s forwards 0.2s; }
    .menu-btn:nth-child(3) { animation: staggerIn 0.6s forwards 0.3s; }
    .menu-btn:nth-child(4) { animation: staggerIn 0.6s forwards 0.4s; }
    .menu-btn:nth-child(5) { animation: staggerIn 0.6s forwards 0.5s; }
    .menu-btn:nth-child(6) { animation: staggerIn 0.6s forwards 0.6s; }
    .menu-btn:nth-child(7) { animation: staggerIn 0.6s forwards 0.7s; }

    @keyframes staggerIn {
      to { opacity: 1; transform: translateY(0); }
    }

    .menu-btn:hover {
      transform: translateY(-15px) scale(1.06);
      border-color: var(--primary);
      box-shadow: 0 25px 70px rgba(35,255,75,0.5);
    }
    .menu-btn h3 {
      color: var(--primary);
      font-size: 1.8rem;
      margin-bottom: 10px;
      text-shadow: 0 0 12px rgba(35,255,75,0.6);
    }
    .menu-btn p {
      color: var(--text-light);
      font-size: 1rem;
    }
    .content {
      opacity: 0;
      transform: translateY(-40px);
      transition: opacity 1s ease, transform 1s ease;
    }
    .content.active {
      opacity: 1;
      transform: translateY(0);
    }
    .back-btn {
      background: linear-gradient(90deg, var(--primary), var(--primary-dark));
      color: black;
      font-weight: bold;
      font-size: 1.2rem;
      padding: 14px 40px;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      display: block;
      margin: 50px auto 0;
      transition: all 0.4s;
      box-shadow: 0 8px 25px rgba(35,255,75,0.5);
    }
    .back-btn:hover {
      transform: translateY(-6px) scale(1.05);
      box-shadow: 0 15px 40px rgba(35,255,75,0.7);
    }
    .qris-container {
      text-align: center;
      margin: 50px 0;
    }
    .qris-img {
      max-width: 380px;
      border-radius: 18px;
      box-shadow: 0 12px 35px rgba(0,0,0,0.7);
      border: 4px solid rgba(35,255,75,0.3);
    }
    .rules-list {
      background: rgba(20, 40, 20, 0.6);
      border: 1px solid rgba(35,255,75,0.3);
      border-radius: 18px;
      padding: 40px;
      margin: 40px 0;
    }
    .rules-list h3 {
      color: var(--primary);
      margin: 30px 0 15px;
      font-size: 1.8rem;
    }
    .rules-list ul {
      list-style: none;
      padding-left: 0;
    }
    .rules-list li {
      margin: 18px 0;
      padding-left: 35px;
      position: relative;
      font-size: 1.1rem;
      color: var(--text-light);
    }
    .rules-list li::before {
      content: "•";
      position: absolute;
      left: 0;
      color: var(--primary);
      font-size: 2.2rem;
    }
    footer {
      text-align: center;
      padding: 60px 20px;
      color: #88ff88;
      border-top: 1px solid rgba(35,255,75,0.2);
      font-size: 1rem;
    }
    .beli-btn {
      background: linear-gradient(135deg, #23ff4b, #00ff9d);
      color: #000;
      font-weight: 900;
      font-size: 1.05rem;
      padding: 12px 35px;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      width: 100%;
      margin-top: 20px;
      box-shadow: 0 8px 25px rgba(35,255,75,0.5);
      transition: all 0.4s;
      position: relative;
      overflow: hidden;
      text-shadow: 0 1px 2px rgba(0,0,0,0.3);
    }
    .beli-btn:hover {
      transform: translateY(-5px) scale(1.04);
      box-shadow: 0 15px 40px rgba(35,255,75,0.7);
      background: linear-gradient(135deg, #00ff9d, #23ff4b);
    }
    .beli-btn:active {
      transform: scale(0.96);
    }
    .ripple {
      position: absolute;
      background: rgba(255,255,255,0.5);
      border-radius: 50%;
      transform: scale(0);
      animation: ripple 0.8s linear;
      pointer-events: none;
    }
    @keyframes ripple {
      to { transform: scale(4); opacity: 0; }
    }
    @media (max-width: 768px) {
      h1 { font-size: 2.5rem; }
      .tagline { font-size: 1rem; }
      .menu-btn { padding: 30px 15px; }
      .beli-btn { font-size: 1rem; padding: 12px 30px; }
    }
  </style>
</head>
<body>

  <!-- Header fixed dengan background gambar lo -->
  <div class="header" id="header">
    <h1>VALORIX NATION</h1>
    <p class="tagline">Server Minecraft Indonesia - Survival • Economy • Fun • Community</p>
  </div>

  <div class="main-content">
    <div class="menu-container">
      <div class="menu-grid" id="menu">
        <div class="menu-btn" onclick="showContent('rank')">
          <h3>Rank Premium</h3>
          <p>Fitur eksklusif & keuntungan lebih</p>
        </div>

        <div class="menu-btn" onclick="showContent('rules')">
          <h3>Rules Server</h3>
          <p>Baca aturan biar aman main</p>
        </div>

        <div class="menu-btn" onclick="window.open('https://chat.whatsapp.com/Fzh6XsvTnWQ3RvrahXlVV5', '_blank')">
          <h3>WhatsApp</h3>
          <p>Bergabung grup resmi</p>
        </div>

        <div class="menu-btn" onclick="window.open('https://top.gg/servers/valorixnation/vote', '_blank')">
          <h3>Vote</h3>
          <p>Vote harian dapat reward</p>
        </div>

        <div class="menu-btn" onclick="showContent('staff')">
          <h3>Staff Team</h3>
          <p>Kenali tim server</p>
        </div>

        <div class="menu-btn" onclick="showContent('changelog')">
          <h3>Changelog</h3>
          <p>Update terbaru server</p>
        </div>
      </div>
    </div>

    <!-- Halaman Rank -->
    <div id="rank" class="content">
      <h1 style="text-align:center; color:#23ff4b; margin-bottom:20px;">RANK VALORIX NATION</h1>
      <p style="text-align:center; color:#aaffaa; margin-bottom:50px; font-size:1.3rem;">
        Pilih rank premium untuk pengalaman bermain lebih seru di server Valorix Nation!
      </p>

      <div class="rank-grid">
        <div class="rank-card">
          <h2 class="rank-title">VIP</h2>
          <div class="harga">Rp 5.000</div>
          <ul>
            <li>/feed</li>
            <li>/back</li>
            <li>/hat</li>
            <li>/sethome (5 slot)</li>
            <li>150k Money</li>
          </ul>
          <button class="beli-btn" data-rank="VIP" data-harga="Rp 5.000" data-fitur="/feed|/back|/hat|/sethome (5 slot)|150k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">VIP+</h2>
          <div class="harga">Rp 15.000</div>
          <ul>
            <li>/heal</li>
            <li>/enderchest</li>
            <li>/workbench</li>
            <li>/ext</li>
            <li>/sethome (10 slot)</li>
            <li>200k Money</li>
          </ul>
          <button class="beli-btn" data-rank="VIP+" data-harga="Rp 15.000" data-fitur="/heal|/enderchest|/workbench|/ext|/sethome (10 slot)|200k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">MVP</h2>
          <div class="harga">Rp 20.000</div>
          <ul>
            <li>/anvil</li>
            <li>/fly</li>
            <li>/feed</li>
            <li>/sethome (20 slot)</li>
            <li>300k Money</li>
          </ul>
          <button class="beli-btn" data-rank="MVP" data-harga="Rp 20.000" data-fitur="/anvil|/fly|/feed|/sethome (20 slot)|300k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">MVP+</h2>
          <div class="harga">Rp 35.000</div>
          <ul>
            <li>/lightning</li>
            <li>/bigtree</li>
            <li>/compass</li>
            <li>/sethome (30 slot)</li>
            <li>400k Money</li>
          </ul>
          <button class="beli-btn" data-rank="MVP+" data-harga="Rp 35.000" data-fitur="/lightning|/bigtree|/compass|/sethome (30 slot)|400k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">LEGENDS</h2>
          <div class="harga">Rp 50.000</div>
          <ul>
            <li>/me</li>
            <li>/bazooka</li>
            <li>/mail</li>
            <li>/sethome (50 slot)</li>
            <li>500k Money</li>
          </ul>
          <button class="beli-btn" data-rank="LEGENDS" data-harga="Rp 50.000" data-fitur="/me|/bazooka|/mail|/sethome (50 slot)|500k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">MYTHICAL</h2>
          <div class="harga">Rp 70.000</div>
          <ul>
            <li>/nick</li>
            <li>/grindstone</li>
            <li>/sethome (100 slot)</li>
            <li>600k Money</li>
          </ul>
          <button class="beli-btn" data-rank="MYTHICAL" data-harga="Rp 70.000" data-fitur="/nick|/grindstone|/sethome (100 slot)|600k Money">Beli Sekarang</button>
        </div>

        <div class="rank-card">
          <h2 class="rank-title">DEWA</h2>
          <div class="harga">Rp 80.000</div>
          <ul>
            <li>/god</li>
            <li>/nuke</li>
            <li>/sethome (10000 slot)</li>
            <li>800k Money</li>
          </ul>
          <button class="beli-btn" data-rank="DEWA" data-harga="Rp 80.000" data-fitur="/god|/nuke|/sethome (10000 slot)|800k Money">Beli Sekarang</button>
        </div>
      </div>

      <button class="back-btn" onclick="backToMenu()">Kembali ke Menu Utama</button>
    </div>

    <!-- Konten Rules -->
    <div id="rules" class="content">
      <h1 style="text-align:center; color:#23ff4b;">SERVER RULES</h1>
      <p style="text-align:center; color:#aaffaa; margin-bottom:60px;">Patuhi aturan ini biar akun aman dan server nyaman!</p>

      <div class="rules-list">
        <h3>Aturan Umum</h3>
        <ul>
          <li>Tidak boleh cheat/hack/xray/fly/killaura → Ban permanen</li>
          <li>Tidak boleh griefing/mencuri tanpa izin → Ban sementara/permanen</li>
          <li>Bahasa sopan, tidak toxic/rasis/SARA → Mute/kick/ban</li>
          <li>Tidak spam chat/iklan server lain → Mute</li>
          <li>Akun alt hanya boleh 1 per IP (kecuali diizinkan) → Ban</li>
          <li>Tidak bug abuse/exploit → Ban</li>
          <li>Patuhi perintah staff → Ban jika melawan</li>
        </ul>

        <h3>Aturan Ekonomi</h3>
        <ul>
          <li>Money dari mining/farming/job/vote/event/donate</li>
          <li>Dilarang jual-beli akun/item ilegal/RMT</li>
          <li>Dilarang scam/tipu-menipu player</li>
          <li>Harga di /shop resmi tidak boleh dimanipulasi</li>
          <li>Vote harian dapat money + reward</li>
          <li>Server tidak tanggung jawab penipuan antar player</li>
        </ul>

        <h3>Hukuman</h3>
        <ul>
          <li>Peringatan 1 → Mute 1 jam</li>
          <li>Peringatan 2 → Mute 1 hari</li>
          <li>Pelanggaran berat → Ban 3-7 hari</li>
          <li>Cheat/griefing besar → Ban permanen + blacklist IP</li>
        </ul>
      </div>

      <button class="back-btn" onclick="backToMenu()">Kembali ke Menu Utama</button>
    </div>

    <!-- Konten Staff -->
    <div id="staff" class="content">
      <h1 style="text-align:center; color:#23ff4b;">STAFF TEAM</h1>
      <p style="text-align:center; color:#aaffaa; margin:40px 0 60px;">Tim yang menjaga server tetap aman & seru!</p>
      <div style="text-align:center; font-size:1.4rem; margin:50px 0;">
        <p><strong>Owner:</strong> Fadlan</p>
        <p><strong>Admin:</strong> Noir</p>
        <p><strong>Helper:</strong></p>
        <ol style="list-style-position: inside; margin:30px auto; max-width:300px; text-align:left; font-size:1.3rem; line-height:1.8;">
          <li>fullower</li>
          <li>the emperor</li>
          <li>vulkan</li>
        </ol>
        <p style="margin-top:50px;">Ingin join staff? Ajukan via WhatsApp!</p>
      </div>
      <button class="back-btn" onclick="backToMenu()">Kembali ke Menu Utama</button>
    </div>

    <!-- Konten Changelog -->
    <div id="changelog" class="content">
      <h1 style="text-align:center; color:#23ff4b;">CHANGELOG</h1>
      <p style="text-align:center; color:#aaffaa; margin:40px 0 60px;">Update terbaru server Valorix Nation</p>
      <div style="background:rgba(20,40,20,0.5); border-radius:20px; padding:50px;">
        <h3>Update Januari 2026</h3>
        <ul style="font-size:1.2rem; margin:20px 0;">
          <li>Tambah fitur /nick untuk rank Mythical+</li>
          <li>Perbaikan ekonomi & harga /shop</li>
          <li>Event Double Money Weekend</li>
        </ul>
        <p style="margin-top:40px;">Update lebih detail di grup WhatsApp!</p>
      </div>
      <button class="back-btn" onclick="backToMenu()">Kembali ke Menu Utama</button>
    </div>
  </div>

  <footer>
    © 2026 Valorix Nation • IP: play.valorix.net • WhatsApp: <a href="https://chat.whatsapp.com/Fzh6XsvTnWQ3RvrahXlVV5" style="color:var(--primary);">Gabung Grup</a>
  </footer>

  <script>
    function showContent(pageId) {
      document.getElementById('header').classList.add('hidden');
      document.getElementById('menu').classList.add('hidden');

      document.querySelectorAll('.content').forEach(el => el.classList.remove('active'));

      const target = document.getElementById(pageId);
      target.classList.add('active');

      window.scrollTo({ top: 0, behavior: 'smooth' });
      setTimeout(() => {
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }, 800);
    }

    function backToMenu() {
      document.querySelectorAll('.content').forEach(el => el.classList.remove('active'));

      document.getElementById('header').classList.remove('hidden');
      document.getElementById('menu').classList.remove('hidden');

      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    document.querySelectorAll('.back-btn').forEach(btn => btn.addEventListener('click', backToMenu));

    // Scroll reveal rank card
    const rankCards = document.querySelectorAll('.rank-card');
    const rankObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('show');
        }
      });
    }, { threshold: 0.1 });

    rankCards.forEach(card => rankObserver.observe(card));

    // Beli rank - WA polos
    document.querySelectorAll('.beli-btn').forEach(btn => {
      btn.addEventListener('click', function(e) {
        const rank = this.getAttribute('data-rank');
        const harga = this.getAttribute('data-harga');
        const fiturStr = this.getAttribute('data-fitur');
        const fiturArr = fiturStr.split('|');

        let fiturText = '';
        for (let i = 0; i < fiturArr.length; i++) {
          fiturText += (i + 1) + '. ' + fiturArr[i].trim() + '\n';
        }

        const pesan = 'Min saya mau beli rank\n' +
                      'RANK: ' + rank + '\n' +
                      'HARGA: ' + harga + '\n' +
                      'FITUR:\n' +
                      fiturText;

        const waLink = 'https://wa.me/6285755152817?text=' + encodeURIComponent(pesan);
        window.open(waLink, '_blank');

        const ripple = document.createElement('span');
        const rect = this.getBoundingClientRect();
        const size = Math.max(rect.width, rect.height);
        const x = e.clientX - rect.left - size / 2;
        const y = e.clientY - rect.top - size / 2;
        ripple.style.width = ripple.style.height = size + 'px';
        ripple.style.left = x + 'px';
        ripple.style.top = y + 'px';
        ripple.classList.add('ripple');
        this.appendChild(ripple);
        setTimeout(() => ripple.remove(), 900);
      });
    });
  </script>
</body>
</html>
