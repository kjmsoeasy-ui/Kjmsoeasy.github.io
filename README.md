<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>GitHub Mobile</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Outfit:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #0d1117;
      --surface: #161b22;
      --surface2: #21262d;
      --border: #30363d;
      --accent: #58a6ff;
      --accent2: #3fb950;
      --accent3: #f78166;
      --accent4: #d2a8ff;
      --text: #e6edf3;
      --text-muted: #7d8590;
      --text-dim: #484f58;
      --tag-bg: #1f6feb26;
      --radius: 12px;
      --radius-sm: 8px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

    body {
      font-family: 'Outfit', sans-serif;
      background: var(--bg);
      color: var(--text);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
    }

    /* Phone frame */
    .phone {
      width: 375px;
      height: 812px;
      background: var(--bg);
      border-radius: 48px;
      border: 2px solid var(--border);
      box-shadow:
        0 0 0 6px #0d1117,
        0 0 0 8px #30363d,
        0 40px 80px rgba(0,0,0,0.8);
      overflow: hidden;
      position: relative;
      display: flex;
      flex-direction: column;
    }

    /* Notch */
    .notch {
      position: absolute;
      top: 0; left: 50%; transform: translateX(-50%);
      width: 120px; height: 28px;
      background: #0d1117;
      border-radius: 0 0 18px 18px;
      z-index: 100;
      border: 2px solid var(--border);
      border-top: none;
    }

    /* Status bar */
    .statusbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 14px 24px 4px;
      font-size: 11px;
      font-weight: 600;
      color: var(--text);
      flex-shrink: 0;
      font-family: 'JetBrains Mono', monospace;
    }
    .statusbar-right { display: flex; gap: 5px; align-items: center; }
    .status-icon { font-size: 12px; }

    /* Screen content area */
    .screen {
      flex: 1;
      overflow: hidden;
      position: relative;
    }

    /* Page */
    .page {
      position: absolute;
      inset: 0;
      overflow-y: auto;
      display: none;
      flex-direction: column;
      scrollbar-width: none;
      animation: slideIn 0.28s cubic-bezier(0.4,0,0.2,1);
    }
    .page::-webkit-scrollbar { display: none; }
    .page.active { display: flex; }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(18px); }
      to   { opacity: 1; transform: translateX(0); }
    }
    @keyframes slideOut {
      from { opacity: 1; transform: translateX(0); }
      to   { opacity: 0; transform: translateX(-18px); }
    }

    /* ── HOME page ── */
    .home-header {
      padding: 18px 20px 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border);
      background: var(--bg);
      position: sticky; top: 0; z-index: 10;
    }
    .home-logo {
      display: flex; align-items: center; gap: 8px;
    }
    .home-logo svg { width: 26px; height: 26px; fill: var(--text); }
    .home-logo-text {
      font-family: 'JetBrains Mono', monospace;
      font-weight: 700; font-size: 18px; color: var(--text);
    }
    .avatar {
      width: 32px; height: 32px; border-radius: 50%;
      background: linear-gradient(135deg, var(--accent), var(--accent4));
      display: flex; align-items: center; justify-content: center;
      font-size: 14px; font-weight: 700; color: #fff;
      flex-shrink: 0;
    }

    .search-bar {
      margin: 14px 20px 10px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      padding: 10px 14px;
      display: flex; align-items: center; gap: 8px;
      cursor: pointer;
    }
    .search-bar span { color: var(--text-muted); font-size: 14px; flex: 1; }
    .search-icon { font-size: 15px; color: var(--text-muted); }

    .section-label {
      padding: 14px 20px 8px;
      font-size: 11px; font-weight: 700;
      color: var(--text-muted); letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    /* Activity feed */
    .feed-item {
      display: flex; gap: 12px;
      padding: 12px 20px;
      border-bottom: 1px solid var(--border);
      cursor: pointer;
      transition: background 0.15s;
    }
    .feed-item:active { background: var(--surface); }
    .feed-avatar {
      width: 36px; height: 36px; border-radius: 50%;
      background: linear-gradient(135deg, #f78166, #ff6b6b);
      display: flex; align-items: center; justify-content: center;
      font-size: 13px; font-weight: 700; color: #fff;
      flex-shrink: 0;
    }
    .feed-avatar.green { background: linear-gradient(135deg, var(--accent2), #56d364); }
    .feed-avatar.purple { background: linear-gradient(135deg, var(--accent4), #bc8cff); }
    .feed-avatar.blue { background: linear-gradient(135deg, var(--accent), #79c0ff); }
    .feed-content { flex: 1; min-width: 0; }
    .feed-content p { font-size: 13px; line-height: 1.5; color: var(--text); }
    .feed-content p strong { color: var(--accent); }
    .feed-meta { font-size: 11px; color: var(--text-muted); margin-top: 3px; }
    .feed-tag {
      display: inline-block;
      background: var(--tag-bg);
      color: var(--accent);
      border-radius: 4px;
      padding: 1px 6px;
      font-size: 11px;
      font-family: 'JetBrains Mono', monospace;
      margin-top: 4px;
    }

    /* ── REPOS page ── */
    .page-header {
      padding: 16px 20px 12px;
      border-bottom: 1px solid var(--border);
      background: var(--bg);
      position: sticky; top: 0; z-index: 10;
      display: flex; align-items: center; gap: 12px;
    }
    .page-header h1 { font-size: 17px; font-weight: 700; }
    .back-btn {
      background: none; border: none; color: var(--accent);
      font-size: 22px; cursor: pointer; line-height: 1;
      padding: 0; display: flex; align-items: center;
    }
    .filter-tabs {
      display: flex; gap: 6px;
      padding: 10px 20px;
      overflow-x: auto; scrollbar-width: none;
      border-bottom: 1px solid var(--border);
    }
    .filter-tabs::-webkit-scrollbar { display: none; }
    .tab-chip {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 5px 14px;
      font-size: 12px; font-weight: 500;
      white-space: nowrap; cursor: pointer;
      transition: all 0.15s; color: var(--text-muted);
    }
    .tab-chip.active {
      background: var(--accent);
      border-color: var(--accent);
      color: #fff;
    }

    .repo-card {
      padding: 16px 20px;
      border-bottom: 1px solid var(--border);
      cursor: pointer;
      transition: background 0.15s;
    }
    .repo-card:active { background: var(--surface); }
    .repo-name {
      font-size: 15px; font-weight: 600;
      color: var(--accent); margin-bottom: 4px;
      display: flex; align-items: center; gap: 6px;
    }
    .repo-badge {
      font-size: 10px; font-weight: 600;
      border: 1px solid var(--border);
      border-radius: 10px; padding: 1px 7px;
      color: var(--text-muted);
    }
    .repo-desc { font-size: 13px; color: var(--text-muted); line-height: 1.4; margin-bottom: 10px; }
    .repo-langs { display: flex; gap: 14px; flex-wrap: wrap; }
    .lang-dot {
      display: flex; align-items: center; gap: 5px;
      font-size: 12px; color: var(--text-muted);
    }
    .dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
    .dot.js { background: #f1e05a; }
    .dot.ts { background: #3178c6; }
    .dot.py { background: #3572A5; }
    .dot.go { background: #00ADD8; }
    .dot.rust { background: #dea584; }
    .dot.css { background: #563d7c; }
    .star-count { margin-left: auto; display: flex; align-items: center; gap: 3px; font-size: 12px; color: var(--text-muted); }

    /* ── EXPLORE page ── */
    .trending-card {
      margin: 10px 20px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 14px;
      cursor: pointer;
      transition: border-color 0.15s, transform 0.1s;
    }
    .trending-card:active { transform: scale(0.98); }
    .trending-rank {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px; color: var(--text-dim);
      margin-bottom: 6px;
    }
    .trending-name { font-size: 14px; font-weight: 600; color: var(--accent); margin-bottom: 4px; }
    .trending-desc { font-size: 12px; color: var(--text-muted); line-height: 1.4; margin-bottom: 10px; }
    .trending-meta { display: flex; gap: 12px; align-items: center; }
    .trend-up { color: var(--accent2); font-size: 12px; font-weight: 600; margin-left: auto; }

    /* ── PROFILE page ── */
    .profile-hero {
      background: linear-gradient(180deg, var(--surface) 0%, var(--bg) 100%);
      padding: 24px 20px 20px;
      border-bottom: 1px solid var(--border);
      text-align: center;
    }
    .profile-avatar {
      width: 80px; height: 80px; border-radius: 50%;
      background: linear-gradient(135deg, var(--accent), var(--accent4));
      display: flex; align-items: center; justify-content: center;
      font-size: 32px; font-weight: 700; color: #fff;
      margin: 0 auto 12px;
      border: 3px solid var(--border);
    }
    .profile-name { font-size: 20px; font-weight: 700; margin-bottom: 2px; }
    .profile-handle { font-size: 14px; color: var(--text-muted); margin-bottom: 8px; font-family: 'JetBrains Mono', monospace; }
    .profile-bio { font-size: 13px; color: var(--text-muted); line-height: 1.5; margin-bottom: 14px; max-width: 260px; margin-left: auto; margin-right: auto; }
    .follow-btn {
      background: var(--accent);
      color: #fff; border: none;
      border-radius: var(--radius-sm);
      padding: 8px 28px;
      font-size: 14px; font-weight: 600;
      cursor: pointer; font-family: 'Outfit', sans-serif;
      transition: opacity 0.15s;
    }
    .follow-btn:active { opacity: 0.8; }
    .profile-stats {
      display: flex; justify-content: center; gap: 32px;
      padding: 16px 20px;
      border-bottom: 1px solid var(--border);
    }
    .stat-item { text-align: center; }
    .stat-num { font-size: 18px; font-weight: 700; display: block; }
    .stat-lbl { font-size: 11px; color: var(--text-muted); }
    .contrib-section { padding: 16px 20px; }
    .contrib-title { font-size: 13px; color: var(--text-muted); margin-bottom: 10px; }
    .contrib-grid {
      display: grid;
      grid-template-columns: repeat(17, 1fr);
      gap: 3px;
    }
    .contrib-cell {
      width: 100%; aspect-ratio: 1;
      border-radius: 2px;
      background: var(--surface2);
    }
    .contrib-cell.l1 { background: #0e4429; }
    .contrib-cell.l2 { background: #006d32; }
    .contrib-cell.l3 { background: #26a641; }
    .contrib-cell.l4 { background: #39d353; }

    /* ── NOTIFICATIONS page ── */
    .notif-item {
      display: flex; gap: 12px;
      padding: 14px 20px;
      border-bottom: 1px solid var(--border);
      cursor: pointer;
      transition: background 0.15s;
      position: relative;
    }
    .notif-item:active { background: var(--surface); }
    .notif-item.unread::before {
      content: '';
      position: absolute;
      left: 8px; top: 50%; transform: translateY(-50%);
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--accent);
    }
    .notif-icon {
      width: 36px; height: 36px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      display: flex; align-items: center; justify-content: center;
      font-size: 16px; flex-shrink: 0;
    }
    .notif-content { flex: 1; min-width: 0; }
    .notif-title { font-size: 13px; font-weight: 500; line-height: 1.4; }
    .notif-title strong { color: var(--accent); }
    .notif-sub { font-size: 11px; color: var(--text-muted); margin-top: 3px;
      white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .notif-time { font-size: 11px; color: var(--text-dim); flex-shrink: 0; align-self: flex-start; }

    /* ── Bottom Nav ── */
    .bottom-nav {
      display: flex;
      background: var(--surface);
      border-top: 1px solid var(--border);
      padding: 8px 0 20px;
      flex-shrink: 0;
    }
    .nav-item {
      flex: 1;
      display: flex; flex-direction: column;
      align-items: center; gap: 3px;
      cursor: pointer;
      padding: 6px 0;
      border: none; background: none;
      transition: transform 0.1s;
      color: var(--text-muted);
    }
    .nav-item:active { transform: scale(0.9); }
    .nav-item.active { color: var(--accent); }
    .nav-icon { font-size: 20px; position: relative; }
    .nav-badge {
      position: absolute; top: -4px; right: -6px;
      background: var(--accent3);
      color: #fff; border-radius: 10px;
      font-size: 9px; font-weight: 700;
      padding: 1px 4px; line-height: 1.4;
    }
    .nav-label { font-size: 10px; font-weight: 500; }

    /* Home indicator */
    .home-indicator {
      position: absolute; bottom: 6px; left: 50%; transform: translateX(-50%);
      width: 100px; height: 4px;
      background: var(--border);
      border-radius: 2px;
      pointer-events: none;
    }
  </style>
</head>
<body>

<div class="phone">
  <div class="notch"></div>

  <!-- Status Bar -->
  <div class="statusbar">
    <span>9:41</span>
    <div class="statusbar-right">
      <span class="status-icon">▲▲▲</span>
      <span class="status-icon">🛜</span>
      <span class="status-icon">🔋</span>
    </div>
  </div>

  <!-- Screens -->
  <div class="screen">

    <!-- HOME -->
    <div class="page active" id="page-home">
      <div class="home-header">
        <div class="home-logo">
          <svg viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
            <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38
              0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13
              -.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66
              .07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15
              -.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27
              .68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12
              .51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48
              0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/>
          </svg>
          <span class="home-logo-text">GitHub</span>
        </div>
        <div class="avatar">K</div>
      </div>

      <div class="search-bar">
        <span class="search-icon">🔍</span>
        <span>Search or jump to...</span>
      </div>

      <div class="section-label">Recent Activity</div>

      <div class="feed-item">
        <div class="feed-avatar blue">T</div>
        <div class="feed-content">
          <p><strong>torvalds</strong> pushed to <strong>linux/linux</strong></p>
          <div class="feed-tag">kernel: mm: fix memory leak</div>
          <div class="feed-meta">2분 전</div>
        </div>
      </div>
      <div class="feed-item">
        <div class="feed-avatar green">V</div>
        <div class="feed-content">
          <p><strong>vuejs/core</strong>에 새 PR이 열렸습니다</p>
          <div class="feed-tag">#10241 feat: improve Suspense</div>
          <div class="feed-meta">15분 전</div>
        </div>
      </div>
      <div class="feed-item">
        <div class="feed-avatar">M</div>
        <div class="feed-content">
          <p><strong>microsoft/vscode</strong>가 1.89.0을 릴리즈했습니다 🎉</p>
          <div class="feed-meta">1시간 전</div>
        </div>
      </div>
      <div class="feed-item">
        <div class="feed-avatar purple">S</div>
        <div class="feed-content">
          <p><strong>shadcn</strong>이 <strong>ui</strong>에 스타를 주었습니다 ⭐</p>
          <div class="feed-meta">3시간 전</div>
        </div>
      </div>
      <div class="feed-item">
        <div class="feed-avatar green">D</div>
        <div class="feed-content">
          <p><strong>denoland/deno</strong>에서 이슈가 닫혔습니다</p>
          <div class="feed-tag">#23011 Fixed!</div>
          <div class="feed-meta">5시간 전</div>
        </div>
      </div>

      <div class="section-label">Pinned Repos</div>
      <div class="feed-item">
        <div style="font-size:20px;flex-shrink:0;">📦</div>
        <div class="feed-content">
          <p><strong>my-awesome-project</strong></p>
          <div class="feed-meta">TypeScript • ⭐ 142 • Updated today</div>
        </div>
      </div>
      <div class="feed-item">
        <div style="font-size:20px;flex-shrink:0;">🤖</div>
        <div class="feed-content">
          <p><strong>ai-chatbot-clone</strong></p>
          <div class="feed-meta">Python • ⭐ 87 • Updated 2일 전</div>
        </div>
      </div>
    </div>

    <!-- REPOS -->
    <div class="page" id="page-repos">
      <div class="page-header">
        <h1>📁 Repositories</h1>
      </div>
      <div class="filter-tabs">
        <div class="tab-chip active">All</div>
        <div class="tab-chip">Public</div>
        <div class="tab-chip">Private</div>
        <div class="tab-chip">Forked</div>
        <div class="tab-chip">Archived</div>
      </div>

      <div class="repo-card">
        <div class="repo-name">my-awesome-project <span class="repo-badge">Public</span></div>
        <div class="repo-desc">Next.js 14 + TypeScript로 만든 풀스택 웹 애플리케이션</div>
        <div class="repo-langs">
          <div class="lang-dot"><span class="dot ts"></span> TypeScript</div>
          <div class="star-count">⭐ 142</div>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">ai-chatbot-clone <span class="repo-badge">Public</span></div>
        <div class="repo-desc">OpenAI API를 활용한 GPT 챗봇 클론 프로젝트</div>
        <div class="repo-langs">
          <div class="lang-dot"><span class="dot py"></span> Python</div>
          <div class="star-count">⭐ 87</div>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">portfolio-v3 <span class="repo-badge">Public</span></div>
        <div class="repo-desc">세 번째 리뉴얼 포트폴리오. Astro + TailwindCSS</div>
        <div class="repo-langs">
          <div class="lang-dot"><span class="dot js"></span> JavaScript</div>
          <div class="lang-dot"><span class="dot css"></span> CSS</div>
          <div class="star-count">⭐ 34</div>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">rust-cli-tools <span class="repo-badge">Private</span></div>
        <div class="repo-desc">일상 자동화를 위한 Rust CLI 도구 모음</div>
        <div class="repo-langs">
          <div class="lang-dot"><span class="dot rust"></span> Rust</div>
          <div class="star-count">⭐ 12</div>
        </div>
      </div>
      <div class="repo-card">
        <div class="repo-name">go-microservices <span class="repo-badge">Private</span></div>
        <div class="repo-desc">Go로 구현한 마이크로서비스 아키텍처 예제</div>
        <div class="repo-langs">
          <div class="lang-dot"><span class="dot go"></span> Go</div>
          <div class="star-count">⭐ 28</div>
        </div>
      </div>
    </div>

    <!-- EXPLORE -->
    <div class="page" id="page-explore">
      <div class="page-header">
        <h1>🔥 Trending</h1>
      </div>

      <div style="padding:10px 20px 0;display:flex;gap:8px;">
        <div class="tab-chip active">Today</div>
        <div class="tab-chip">This Week</div>
        <div class="tab-chip">This Month</div>
      </div>

      <div class="trending-card">
        <div class="trending-rank">#1 Trending Today</div>
        <div class="trending-name">vercel / ai</div>
        <div class="trending-desc">Build AI-powered streaming text and chat UIs with React, Svelte, Vue, and Solid</div>
        <div class="trending-meta">
          <div class="lang-dot"><span class="dot ts"></span> TypeScript</div>
          <span>⭐ 41.2k</span>
          <span class="trend-up">▲ 2,341 stars today</span>
        </div>
      </div>
      <div class="trending-card">
        <div class="trending-rank">#2 Trending Today</div>
        <div class="trending-name">ollama / ollama</div>
        <div class="trending-desc">Get up and running with large language models locally</div>
        <div class="trending-meta">
          <div class="lang-dot"><span class="dot go"></span> Go</div>
          <span>⭐ 78.5k</span>
          <span class="trend-up">▲ 1,890 stars today</span>
        </div>
      </div>
      <div class="trending-card">
        <div class="trending-rank">#3 Trending Today</div>
        <div class="trending-name">microsoft / TypeScript</div>
        <div class="trending-desc">TypeScript is a superset of JavaScript that compiles to clean JS output</div>
        <div class="trending-meta">
          <div class="lang-dot"><span class="dot ts"></span> TypeScript</div>
          <span>⭐ 100k</span>
          <span class="trend-up">▲ 1,124 stars today</span>
        </div>
      </div>
      <div class="trending-card">
        <div class="trending-rank">#4 Trending Today</div>
        <div class="trending-name">facebook / react</div>
        <div class="trending-desc">The library for web and native user interfaces</div>
        <div class="trending-meta">
          <div class="lang-dot"><span class="dot js"></span> JavaScript</div>
          <span>⭐ 226k</span>
          <span class="trend-up">▲ 987 stars today</span>
        </div>
      </div>
    </div>

    <!-- NOTIFICATIONS -->
    <div class="page" id="page-notifications">
      <div class="page-header">
        <h1>🔔 Notifications</h1>
      </div>

      <div class="notif-item unread">
        <div class="notif-icon">💬</div>
        <div class="notif-content">
          <div class="notif-title"><strong>@gaeun_dev</strong>이 PR에 댓글을 남겼습니다</div>
          <div class="notif-sub">my-awesome-project · LGTM! 코드 스타일이 깔끔하네요 👍</div>
        </div>
        <div class="notif-time">2m</div>
      </div>
      <div class="notif-item unread">
        <div class="notif-icon">✅</div>
        <div class="notif-content">
          <div class="notif-title">CI/CD가 성공적으로 완료됐습니다</div>
          <div class="notif-sub">my-awesome-project · deploy to production ✓</div>
        </div>
        <div class="notif-time">18m</div>
      </div>
      <div class="notif-item unread">
        <div class="notif-icon">🔀</div>
        <div class="notif-content">
          <div class="notif-title"><strong>@dev_junho</strong>가 PR을 열었습니다</div>
          <div class="notif-sub">go-microservices · feat: add gRPC health check</div>
        </div>
        <div class="notif-time">1h</div>
      </div>
      <div class="notif-item">
        <div class="notif-icon">⭐</div>
        <div class="notif-content">
          <div class="notif-title"><strong>@minsu_codes</strong>가 스타를 눌렀습니다</div>
          <div class="notif-sub">ai-chatbot-clone</div>
        </div>
        <div class="notif-time">3h</div>
      </div>
      <div class="notif-item">
        <div class="notif-icon">⚠️</div>
        <div class="notif-content">
          <div class="notif-title">보안 취약점이 발견됐습니다</div>
          <div class="notif-sub">portfolio-v3 · lodash 4.17.15 → 업데이트 필요</div>
        </div>
        <div class="notif-time">5h</div>
      </div>
      <div class="notif-item">
        <div class="notif-icon">🍴</div>
        <div class="notif-content">
          <div class="notif-title"><strong>@jiyeon_k</strong>가 포크했습니다</div>
          <div class="notif-sub">ai-chatbot-clone</div>
        </div>
        <div class="notif-time">1d</div>
      </div>
    </div>

    <!-- PROFILE -->
    <div class="page" id="page-profile">
      <div class="profile-hero">
        <div class="profile-avatar">K</div>
        <div class="profile-name">김개발</div>
        <div class="profile-handle">@kimgaebal_dev</div>
        <div class="profile-bio">풀스택 개발자 🧑‍💻 · TypeScript / Go / Rust 좋아함 · 커피 없이 못 살아 ☕</div>
        <button class="follow-btn">Follow</button>
      </div>

      <div class="profile-stats">
        <div class="stat-item">
          <span class="stat-num">42</span>
          <span class="stat-lbl">Repos</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">1.2k</span>
          <span class="stat-lbl">Followers</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">387</span>
          <span class="stat-lbl">Following</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">3.4k</span>
          <span class="stat-lbl">Stars</span>
        </div>
      </div>

      <div class="contrib-section">
        <div class="contrib-title">1,247 contributions in the last year</div>
        <div class="contrib-grid" id="contrib-grid"></div>
      </div>
    </div>

  </div><!-- /screen -->

  <!-- Bottom Nav -->
  <div class="bottom-nav">
    <button class="nav-item active" onclick="navigate('home', this)">
      <span class="nav-icon">🏠</span>
      <span class="nav-label">Home</span>
    </button>
    <button class="nav-item" onclick="navigate('repos', this)">
      <span class="nav-icon">📁</span>
      <span class="nav-label">Repos</span>
    </button>
    <button class="nav-item" onclick="navigate('explore', this)">
      <span class="nav-icon">🔭</span>
      <span class="nav-label">Explore</span>
    </button>
    <button class="nav-item" onclick="navigate('notifications', this)">
      <span class="nav-icon" style="position:relative">🔔<span class="nav-badge">3</span></span>
      <span class="nav-label">Inbox</span>
    </button>
    <button class="nav-item" onclick="navigate('profile', this)">
      <span class="nav-icon">👤</span>
      <span class="nav-label">Profile</span>
    </button>
  </div>

  <div class="home-indicator"></div>
</div>

<script>
  // Tab chip toggle
  document.querySelectorAll('.filter-tabs').forEach(tabs => {
    tabs.querySelectorAll('.tab-chip').forEach(chip => {
      chip.addEventListener('click', () => {
        tabs.querySelectorAll('.tab-chip').forEach(c => c.classList.remove('active'));
        chip.classList.add('active');
      });
    });
  });

  // Navigation
  function navigate(pageId, btn) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById('page-' + pageId).classList.add('active');
    if (btn) btn.classList.add('active');
  }

  // Generate contribution grid
  const grid = document.getElementById('contrib-grid');
  const levels = ['', 'l1', 'l2', 'l3', 'l4'];
  for (let i = 0; i < 17 * 7; i++) {
    const cell = document.createElement('div');
    cell.className = 'contrib-cell';
    const rand = Math.random();
    if (rand > 0.6) {
      const lvl = levels[Math.floor(rand * 4) + 1] || levels[4];
      cell.classList.add(lvl);
    }
    grid.appendChild(cell);
  }
</script>

</body>
</html>
