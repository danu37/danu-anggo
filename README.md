<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600&family=Sora:wght@300;400;500;600;700&display=swap');
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Sora', sans-serif; background: #0d1117; color: #e6edf3; min-height: 100vh; }

  .gh-header {
    background: #161b22; border-bottom: 1px solid #30363d;
    padding: 12px 24px; display: flex; align-items: center; gap: 16px; font-size: 13px;
  }
  .search-bar {
    background: #0d1117; border: 1px solid #30363d; border-radius: 6px;
    padding: 4px 12px; color: #8b949e; font-family: 'Sora',sans-serif;
    font-size: 13px; width: 220px; outline: none;
  }
  .search-bar:focus { border-color: #f05340; box-shadow: 0 0 0 3px rgba(240,83,64,0.15); }
  .gh-nav { display: flex; gap: 4px; margin-left: auto; }
  .gh-nav a {
    color: #e6edf3; text-decoration: none; padding: 5px 10px;
    border-radius: 6px; font-size: 13px; opacity: 0.7;
    transition: opacity 0.15s, background 0.15s; cursor: pointer;
  }
  .gh-nav a:hover { opacity: 1; background: #30363d; }

  .layout {
    display: grid; grid-template-columns: 280px 1fr;
    gap: 24px; max-width: 1200px; margin: 24px auto; padding: 0 24px; align-items: start;
  }
  .sidebar { position: sticky; top: 24px; }

  .avatar {
    width: 260px; height: 260px; border-radius: 50%;
    background: linear-gradient(135deg, #f05340 0%, #ff7b5c 40%, #e03020 80%);
    display: flex; align-items: center; justify-content: center;
    font-size: 76px; font-weight: 700; color: white;
    border: 3px solid #30363d; font-family: 'JetBrains Mono', monospace;
    position: relative; overflow: hidden; margin-bottom: 12px;
  }
  .avatar::before {
    content: ''; position: absolute; inset: 0;
    background: radial-gradient(circle at 35% 30%, rgba(255,255,255,0.18), transparent 60%);
  }
  .av-text { position: relative; z-index: 1; letter-spacing: -3px; }
  .online { position: absolute; bottom: 14px; right: 14px; width: 20px; height: 20px; background: #3fb950; border: 3px solid #161b22; border-radius: 50%; }

  .name { font-size: 22px; font-weight: 600; color: #e6edf3; margin-bottom: 2px; }
  .username { font-size: 17px; font-weight: 300; color: #8b949e; margin-bottom: 12px; font-family: 'JetBrains Mono', monospace; }
  .bio { font-size: 13px; color: #8b949e; line-height: 1.6; margin-bottom: 16px; }

  .follow-btn {
    width: 100%; padding: 6px 0; background: #21262d;
    border: 1px solid #363b42; border-radius: 6px; color: #e6edf3;
    font-family: 'Sora', sans-serif; font-size: 14px; font-weight: 500;
    cursor: pointer; margin-bottom: 16px; transition: background 0.15s, border-color 0.15s;
  }
  .follow-btn:hover { background: #30363d; border-color: #8b949e; }

  .stats-row { display: flex; gap: 8px; margin-bottom: 16px; font-size: 13px; align-items: center; }
  .stat { color: #8b949e; display: flex; align-items: center; gap: 4px; }
  .stat strong { color: #e6edf3; font-weight: 600; }
  .stat-dot { color: #30363d; }

  .sl { font-size: 11px; font-weight: 600; color: #6e7681; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 8px; margin-top: 16px; }
  .si { display: flex; align-items: center; gap: 8px; font-size: 13px; color: #8b949e; padding: 3px 0; }
  .si .i { font-size: 15px; color: #6e7681; }
  .si a { color: #f05340; text-decoration: none; }
  .si a:hover { text-decoration: underline; }

  .pills { display: flex; flex-wrap: wrap; gap: 6px; }
  .pill {
    border: 1px solid #30363d; border-radius: 20px; padding: 3px 10px;
    font-size: 11px; font-weight: 600; font-family: 'JetBrains Mono', monospace;
  }
  .p-red { background: #1a0f0e; color: #f05340; border-color: #3d1a16; }
  .p-blue { background: #0d1f33; color: #61a8ff; border-color: #1a3a5c; }
  .p-orange { background: #1a1200; color: #f0a030; border-color: #3a2800; }
  .p-teal { background: #0a1a18; color: #3fb9a0; border-color: #1a3834; }

  .tab-nav { display: flex; border-bottom: 1px solid #21262d; margin-bottom: 20px; }
  .tab {
    padding: 10px 16px; font-size: 14px; color: #8b949e; cursor: pointer;
    border-bottom: 2px solid transparent; display: flex; align-items: center; gap: 8px;
    transition: color 0.15s; margin-bottom: -1px;
  }
  .tab.active { color: #e6edf3; border-bottom-color: #f05340; }
  .tab:hover:not(.active) { color: #e6edf3; }
  .tc {
    background: #30363d; border-radius: 20px; padding: 0 7px;
    font-size: 12px; font-family: 'JetBrains Mono', monospace; color: #8b949e;
  }
  .tab.active .tc { background: #3a1a14; color: #f05340; }

  .sec-title { font-size: 14px; font-weight: 600; color: #e6edf3; margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
  .sec-title i { color: #8b949e; font-size: 16px; }

  .pin-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 28px; }
  .repo-card {
    background: #161b22; border: 1px solid #30363d; border-radius: 10px;
    padding: 16px; transition: border-color 0.15s, transform 0.1s;
    cursor: pointer; display: flex; flex-direction: column; gap: 8px;
  }
  .repo-card:hover { border-color: #f05340; transform: translateY(-1px); }
  .rh { display: flex; align-items: center; gap: 8px; }
  .rh i { font-size: 16px; color: #f05340; }
  .rn { font-size: 14px; font-weight: 600; color: #f05340; font-family: 'JetBrains Mono', monospace; }
  .rd { font-size: 12px; color: #8b949e; line-height: 1.5; flex: 1; }
  .rf { display: flex; align-items: center; gap: 10px; margin-top: 4px; }
  .ld { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
  .rm { display: flex; align-items: center; gap: 4px; font-size: 12px; color: #8b949e; }

  .stats-cards { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; margin-bottom: 24px; }
  .sc { background: #161b22; border: 1px solid #30363d; border-radius: 10px; padding: 16px; text-align: center; }
  .sc-n { font-size: 26px; font-weight: 700; font-family: 'JetBrains Mono', monospace; color: #f05340; display: block; margin-bottom: 4px; }
  .sc-l { font-size: 11px; color: #8b949e; }

  .contrib-box { background: #161b22; border: 1px solid #30363d; border-radius: 10px; padding: 16px; margin-bottom: 24px; }
  .cb-header { display: flex; justify-content: space-between; font-size: 13px; color: #8b949e; margin-bottom: 12px; }
  .cb-count { color: #e6edf3; font-weight: 600; }
  .cg { display: grid; grid-template-columns: repeat(53, 1fr); gap: 2px; }
  .cc { width: 100%; aspect-ratio: 1; border-radius: 2px; border: 1px solid rgba(255,255,255,0.03); }

  .lang-wrap { margin-bottom: 28px; }
  .lb-row { margin-bottom: 12px; }
  .lb-hdr { display: flex; justify-content: space-between; margin-bottom: 5px; font-size: 12px; }
  .lb-bg { background: #30363d; border-radius: 4px; height: 6px; overflow: hidden; }
  .lb-fill { height: 100%; border-radius: 4px; transition: width 1.1s cubic-bezier(0.4,0,0.2,1); }

  .activity-box { background: #161b22; border: 1px solid #30363d; border-radius: 10px; overflow: hidden; margin-bottom: 24px; }
  .ah { padding: 12px 16px; border-bottom: 1px solid #21262d; font-size: 13px; font-weight: 600; color: #e6edf3; display: flex; align-items: center; gap: 8px; }
  .ar { display: flex; align-items: flex-start; gap: 10px; padding: 10px 16px; border-bottom: 1px solid #21262d; font-size: 13px; color: #8b949e; }
  .ar:last-child { border-bottom: none; }
  .ar i { font-size: 16px; margin-top: 1px; flex-shrink: 0; }
  .at { flex: 1; line-height: 1.5; }
  .at strong { color: #e6edf3; font-weight: 500; }
  .at .ref { color: #f05340; }
  .at2 { font-size: 12px; color: #6e7681; flex-shrink: 0; font-family: 'JetBrains Mono', monospace; }

  .trophy-row { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 24px; }
  .trophy { background: #161b22; border: 1px solid #30363d; border-radius: 8px; padding: 8px 14px; display: flex; align-items: center; gap: 8px; font-size: 12px; color: #8b949e; }
  .trophy i { font-size: 18px; color: #d29922; }
</style>
</head>
<body>

<div class="gh-header">
  <svg width="28" height="28" viewBox="0 0 24 24" fill="#e6edf3"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
  <input class="search-bar" type="text" placeholder="Search or jump to...">
  <nav class="gh-nav">
    <a>Pull requests</a><a>Issues</a><a>Marketplace</a><a>Explore</a>
  </nav>
</div>

<div class="layout">
  <!-- Sidebar -->
  <aside class="sidebar">
    <div class="avatar">
      <span class="av-text">DA</span>
      <div class="online"></div>
    </div>

    <div class="name">Danu Anggo</div>
    <div class="username">@danu-anggo</div>
    <div class="bio">Fullstack Developer · Laravel & React enthusiast. Building scalable web apps with clean architecture. Open to collaboration.</div>
    <button class="follow-btn">Follow</button>

    <div class="stats-row">
      <span class="stat"><strong>834</strong> followers</span>
      <span class="stat-dot">·</span>
      <span class="stat"><strong>196</strong> following</span>
    </div>

    <div class="sl">Info</div>
    <div class="si"><i class="ti ti-building i" aria-hidden="true"></i> Freelance · Open to Work</div>
    <div class="si"><i class="ti ti-map-pin i" aria-hidden="true"></i> Indonesia 🇮🇩</div>
    <div class="si"><i class="ti ti-link i" aria-hidden="true"></i> <a href="#">danuanggo.dev</a></div>
    <div class="si"><i class="ti ti-mail i" aria-hidden="true"></i> hi@danuanggo.dev</div>

    <div class="sl">Tech Stack</div>
    <div class="pills">
      <span class="pill p-red">Laravel</span>
      <span class="pill p-red">PHP</span>
      <span class="pill p-blue">React</span>
      <span class="pill p-blue">JavaScript</span>
      <span class="pill p-orange">MySQL</span>
      <span class="pill p-teal">Docker</span>
      <span class="pill p-blue">Inertia.js</span>
      <span class="pill p-teal">Nginx</span>
      <span class="pill p-orange">Redis</span>
      <span class="pill p-red">Livewire</span>
    </div>

    <div class="sl">Organizations</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;">
      <div style="width:32px;height:32px;border-radius:6px;background:#1a0f0e;border:1px solid #3d1a16;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:#f05340;font-family:'JetBrains Mono',monospace;cursor:pointer;">PHP</div>
      <div style="width:32px;height:32px;border-radius:6px;background:#0d1f33;border:1px solid #1a3a5c;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:#61a8ff;font-family:'JetBrains Mono',monospace;cursor:pointer;">RCT</div>
      <div style="width:32px;height:32px;border-radius:6px;background:#0a1a18;border:1px solid #1a3834;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:#3fb9a0;font-family:'JetBrains Mono',monospace;cursor:pointer;">OSS</div>
    </div>
  </aside>

  <!-- Main -->
  <main>
    <div class="tab-nav">
      <div class="tab active"><i class="ti ti-layout-2"></i> Overview</div>
      <div class="tab"><i class="ti ti-book"></i> Repositories <span class="tc">34</span></div>
      <div class="tab"><i class="ti ti-activity"></i> Activity</div>
      <div class="tab"><i class="ti ti-star"></i> Stars <span class="tc">218</span></div>
    </div>

    <!-- Stats -->
    <div class="stats-cards">
      <div class="sc"><span class="sc-n" id="c1">0</span><span class="sc-l">Commits tahun ini</span></div>
      <div class="sc"><span class="sc-n" id="c2">0</span><span class="sc-l">Pull Requests</span></div>
      <div class="sc"><span class="sc-n" id="c3">0</span><span class="sc-l">Issues closed</span></div>
    </div>

    <!-- Trophies -->
    <div class="trophy-row">
      <div class="trophy"><i class="ti ti-trophy"></i> Arctic Code Vault</div>
      <div class="trophy"><i class="ti ti-star"></i> Pull Shark x2</div>
      <div class="trophy"><i class="ti ti-bolt"></i> YOLO</div>
      <div class="trophy"><i class="ti ti-flame"></i> 90 day streak</div>
    </div>

    <!-- Pinned -->
    <div class="sec-title"><i class="ti ti-pin"></i> Pinned repositories</div>
    <div class="pin-grid">
      <div class="repo-card">
        <div class="rh"><i class="ti ti-book"></i><span class="rn">laravel-shop</span></div>
        <div class="rd">E-commerce fullstack pakai Laravel 11 + React + Inertia.js. Fitur lengkap: cart, payment gateway, admin panel.</div>
        <div class="rf">
          <div class="ld" style="background:#f05340;"></div>
          <span class="rm">PHP</span>
          <span class="rm"><i class="ti ti-star" style="font-size:13px;"></i> 892</span>
          <span class="rm"><i class="ti ti-git-fork" style="font-size:13px;"></i> 134</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="rh"><i class="ti ti-book"></i><span class="rn">react-dashboard</span></div>
        <div class="rd">Admin dashboard SPA dengan React 18, Vite, Tailwind CSS, dan REST API Laravel sebagai backend.</div>
        <div class="rf">
          <div class="ld" style="background:#f7df1e;"></div>
          <span class="rm">JavaScript</span>
          <span class="rm"><i class="ti ti-star" style="font-size:13px;"></i> 541</span>
          <span class="rm"><i class="ti ti-git-fork" style="font-size:13px;"></i> 87</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="rh"><i class="ti ti-book"></i><span class="rn">docker-laravel-stack</span></div>
        <div class="rd">Docker Compose template siap pakai: Laravel, MySQL 8, Redis, Nginx, dan Queue worker. Satu command langsung jalan.</div>
        <div class="rf">
          <div class="ld" style="background:#3fb9a0;"></div>
          <span class="rm">Dockerfile</span>
          <span class="rm"><i class="ti ti-star" style="font-size:13px;"></i> 1.2k</span>
          <span class="rm"><i class="ti ti-git-fork" style="font-size:13px;"></i> 203</span>
        </div>
      </div>
      <div class="repo-card">
        <div class="rh"><i class="ti ti-book"></i><span class="rn">pos-system</span></div>
        <div class="rd">Point of Sale berbasis web — Laravel backend, React frontend, MySQL dengan full transaksi, laporan harian & stok.</div>
        <div class="rf">
          <div class="ld" style="background:#f05340;"></div>
          <span class="rm">PHP</span>
          <span class="rm"><i class="ti ti-star" style="font-size:13px;"></i> 376</span>
          <span class="rm"><i class="ti ti-git-fork" style="font-size:13px;"></i> 61</span>
        </div>
      </div>
    </div>

    <!-- Contribution Graph -->
    <div class="contrib-box">
      <div class="cb-header">
        <span><span class="cb-count">1,423 contributions</span> in the last year</span>
        <span>2024 · 2025</span>
      </div>
      <div class="cg" id="cg"></div>
      <div style="display:flex;align-items:center;gap:4px;margin-top:10px;justify-content:flex-end;font-size:11px;color:#6e7681;">
        Less
        <div style="width:10px;height:10px;border-radius:2px;background:#161b22;border:1px solid #30363d;"></div>
        <div style="width:10px;height:10px;border-radius:2px;background:#3a0d08;"></div>
        <div style="width:10px;height:10px;border-radius:2px;background:#6b1a12;"></div>
        <div style="width:10px;height:10px;border-radius:2px;background:#b03020;"></div>
        <div style="width:10px;height:10px;border-radius:2px;background:#f05340;"></div>
        More
      </div>
    </div>

    <!-- Languages -->
    <div class="lang-wrap">
      <div class="sec-title"><i class="ti ti-code"></i> Most used languages</div>
      <div class="lb-row">
        <div class="lb-hdr">
          <span style="color:#f05340;font-weight:500;font-size:13px;display:flex;align-items:center;gap:6px;"><div style="width:10px;height:10px;border-radius:50%;background:#f05340;"></div>PHP (Laravel)</span>
          <span style="color:#8b949e;font-size:12px;">48.2%</span>
        </div>
        <div class="lb-bg"><div class="lb-fill" id="b1" style="width:0%;background:#f05340;"></div></div>
      </div>
      <div class="lb-row">
        <div class="lb-hdr">
          <span style="color:#61a8ff;font-weight:500;font-size:13px;display:flex;align-items:center;gap:6px;"><div style="width:10px;height:10px;border-radius:50%;background:#61a8ff;"></div>JavaScript (React)</span>
          <span style="color:#8b949e;font-size:12px;">32.5%</span>
        </div>
        <div class="lb-bg"><div class="lb-fill" id="b2" style="width:0%;background:#61a8ff;"></div></div>
      </div>
      <div class="lb-row">
        <div class="lb-hdr">
          <span style="color:#f0a030;font-weight:500;font-size:13px;display:flex;align-items:center;gap:6px;"><div style="width:10px;height:10px;border-radius:50%;background:#f0a030;"></div>SQL (MySQL)</span>
          <span style="color:#8b949e;font-size:12px;">11.8%</span>
        </div>
        <div class="lb-bg"><div class="lb-fill" id="b3" style="width:0%;background:#f0a030;"></div></div>
      </div>
      <div class="lb-row">
        <div class="lb-hdr">
          <span style="color:#3fb9a0;font-weight:500;font-size:13px;display:flex;align-items:center;gap:6px;"><div style="width:10px;height:10px;border-radius:50%;background:#3fb9a0;"></div>Dockerfile / Shell</span>
          <span style="color:#8b949e;font-size:12px;">7.5%</span>
        </div>
        <div class="lb-bg"><div class="lb-fill" id="b4" style="width:0%;background:#3fb9a0;"></div></div>
      </div>
    </div>

    <!-- Recent Activity -->
    <div class="activity-box">
      <div class="ah"><i class="ti ti-activity"></i> Recent activity</div>
      <div class="ar">
        <i class="ti ti-git-commit" style="color:#3fb950;"></i>
        <div class="at">Pushed 5 commits ke <span class="ref">laravel-shop</span> — <strong>feat: integrasi Midtrans payment gateway</strong></div>
        <span class="at2">1j lalu</span>
      </div>
      <div class="ar">
        <i class="ti ti-git-merge" style="color:#8957e5;"></i>
        <div class="at">Merged PR <span class="ref">#58</span> di <span class="ref">docker-laravel-stack</span> — <strong>add PHP 8.3 support + healthcheck</strong></div>
        <span class="at2">6j lalu</span>
      </div>
      <div class="ar">
        <i class="ti ti-git-commit" style="color:#3fb950;"></i>
        <div class="at">Pushed ke <span class="ref">react-dashboard</span> — <strong>refactor: pisah AuthContext dari AppProvider</strong></div>
        <span class="at2">1h lalu</span>
      </div>
      <div class="ar">
        <i class="ti ti-star" style="color:#d29922;"></i>
        <div class="at">Starred <span class="ref">laravel/framework</span> dan <span class="ref">vitejs/vite</span></div>
        <span class="at2">2h lalu</span>
      </div>
      <div class="ar">
        <i class="ti ti-package" style="color:#f05340;"></i>
        <div class="at">Released <span class="ref">docker-laravel-stack v3.1.0</span> — support multi-service, queue worker otomatis</div>
        <span class="at2">4h lalu</span>
      </div>
    </div>
  </main>
</div>

<script>
  const levels = ['#161b22','#3a0d08','#6b1a12','#b03020','#f05340'];
  function rLevel() {
    const r = Math.random();
    if (r < 0.35) return 0;
    if (r < 0.55) return 1;
    if (r < 0.72) return 2;
    if (r < 0.88) return 3;
    return 4;
  }
  const cg = document.getElementById('cg');
  for (let i = 0; i < 371; i++) {
    const c = document.createElement('div');
    c.className = 'cc';
    c.style.background = levels[rLevel()];
    cg.appendChild(c);
  }

  function animateCount(el, target, duration) {
    let v = 0;
    const step = target / (duration / 16);
    const t = setInterval(() => {
      v += step;
      if (v >= target) { v = target; clearInterval(t); }
      el.textContent = Math.floor(v).toLocaleString();
    }, 16);
  }
  setTimeout(() => {
    animateCount(document.getElementById('c1'), 1423, 1200);
    animateCount(document.getElementById('c2'), 187, 1000);
    animateCount(document.getElementById('c3'), 94, 900);
  }, 300);

  setTimeout(() => {
    document.getElementById('b1').style.width = '48.2%';
    document.getElementById('b2').style.width = '32.5%';
    document.getElementById('b3').style.width = '11.8%';
    document.getElementById('b4').style.width = '7.5%';
  }, 400);
</script>
</body>
</html>
