<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&family=Rajdhani:wght@300;500;700&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #020510;
    color: #e0f0ff;
    font-family: 'Rajdhani', sans-serif;
    overflow-x: hidden;
    min-height: 100vh;
  }

  canvas#bg {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
  }

  .page {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 2rem 1.5rem 4rem;
  }

  /* HEADER */
  .header {
    text-align: center;
    padding: 3rem 0 2rem;
    position: relative;
  }

  .glitch-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(2rem, 6vw, 3.8rem);
    font-weight: 900;
    letter-spacing: 0.08em;
    color: #00f5ff;
    text-shadow: 0 0 20px #00f5ff88, 0 0 60px #00f5ff33;
    position: relative;
    display: inline-block;
    animation: glitch 4s infinite;
  }

  @keyframes glitch {
    0%, 92%, 100% { text-shadow: 0 0 20px #00f5ff88, 0 0 60px #00f5ff33; transform: none; }
    93% { transform: translateX(-3px); text-shadow: 3px 0 #ff003c, -3px 0 #00f5ff, 0 0 30px #00f5ff88; }
    94% { transform: translateX(3px); text-shadow: -3px 0 #ff003c, 3px 0 #00f5ff, 0 0 30px #00f5ff88; }
    95% { transform: translateX(0); text-shadow: 0 0 20px #00f5ff88; }
    96% { transform: translateX(-2px) skewX(-5deg); text-shadow: 2px 0 #9d00ff, -2px 0 #00f5ff; }
    97% { transform: none; text-shadow: 0 0 20px #00f5ff88, 0 0 60px #00f5ff33; }
  }

  .title-bar {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.85rem;
    color: #00f5ff99;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    margin-top: 0.4rem;
  }

  .title-bar span { color: #9d00ff; }

  .scan-line {
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent, #00f5ff, #9d00ff, #00f5ff, transparent);
    margin: 1.5rem auto;
    animation: scan 3s linear infinite;
    background-size: 200% 100%;
  }
  @keyframes scan { 0% { background-position: 200% 0; } 100% { background-position: -200% 0; } }

  /* STATUS BADGES */
  .status-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    margin: 1rem 0 2rem;
  }

  .badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    padding: 5px 14px;
    border: 1px solid;
    border-radius: 2px;
    letter-spacing: 0.12em;
    position: relative;
    overflow: hidden;
    animation: badgePulse 3s ease-in-out infinite;
  }
  .badge::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.08), transparent);
    animation: shimmer 3s ease-in-out infinite;
  }
  @keyframes shimmer { 0%, 100% { left: -100%; } 50% { left: 100%; } }
  @keyframes badgePulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.7; } }

  .badge-cyan { color: #00f5ff; border-color: #00f5ff44; background: #00f5ff0a; }
  .badge-purple { color: #c084fc; border-color: #9d00ff44; background: #9d00ff0a; animation-delay: 0.5s; }
  .badge-green { color: #4ade80; border-color: #22c55e44; background: #22c55e0a; animation-delay: 1s; }
  .badge-orange { color: #fb923c; border-color: #f9731644; background: #f9731608; animation-delay: 1.5s; }

  /* SECTION PANELS */
  .panel {
    border: 1px solid #00f5ff22;
    background: linear-gradient(135deg, #020d1e 0%, #050820 100%);
    border-radius: 4px;
    margin-bottom: 1.5rem;
    position: relative;
    overflow: hidden;
  }

  .panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, #00f5ff, #9d00ff, transparent);
  }

  .panel-header {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 1rem 1.25rem 0.75rem;
    border-bottom: 1px solid #00f5ff11;
  }

  .panel-icon {
    width: 32px; height: 32px;
    background: #00f5ff15;
    border: 1px solid #00f5ff44;
    border-radius: 3px;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px;
    color: #00f5ff;
  }

  .panel-title {
    font-family: 'Orbitron', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.25em;
    color: #00f5ff;
    text-transform: uppercase;
  }

  .panel-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: #9d00ff;
    margin-left: auto;
    letter-spacing: 0.15em;
  }

  .panel-body { padding: 1.25rem; }

  /* BIO */
  .bio-text {
    font-size: 1.05rem;
    line-height: 1.8;
    color: #a8c8e8;
    font-weight: 300;
  }

  .bio-text .hi { color: #00f5ff; font-weight: 700; }
  .bio-text .accent { color: #c084fc; }
  .bio-text .go { color: #4ade80; }

  .typing-cursor {
    display: inline-block;
    width: 2px;
    height: 1em;
    background: #00f5ff;
    margin-left: 2px;
    vertical-align: middle;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

  /* SKILL GRID */
  .skill-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
    gap: 8px;
  }

  .skill-chip {
    background: #0a1628;
    border: 1px solid #00f5ff1a;
    border-radius: 3px;
    padding: 8px 10px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: #7dd3fc;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
    cursor: default;
  }

  .skill-chip:hover {
    border-color: #00f5ff66;
    color: #00f5ff;
    background: #00f5ff0d;
    transform: translateY(-2px);
    box-shadow: 0 4px 20px #00f5ff22;
  }

  .skill-chip .dot {
    display: inline-block;
    width: 5px; height: 5px;
    border-radius: 50%;
    margin-right: 5px;
    vertical-align: middle;
  }
  .dot-cyan { background: #00f5ff; box-shadow: 0 0 6px #00f5ff; }
  .dot-purple { background: #c084fc; box-shadow: 0 0 6px #9d00ff; }
  .dot-green { background: #4ade80; box-shadow: 0 0 6px #22c55e; }
  .dot-orange { background: #fb923c; box-shadow: 0 0 6px #f97316; }

  /* STAT BARS */
  .stat-row {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 10px;
  }

  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.72rem;
    color: #7dd3fc;
    width: 140px;
    flex-shrink: 0;
  }

  .stat-bar-bg {
    flex: 1;
    height: 6px;
    background: #0a1628;
    border-radius: 0;
    border: 1px solid #00f5ff11;
    overflow: hidden;
    position: relative;
  }

  .stat-bar-fill {
    height: 100%;
    border-radius: 0;
    position: relative;
    animation: fillBar 2s ease-out forwards;
    transform-origin: left;
  }

  @keyframes fillBar {
    from { width: 0% !important; }
  }

  .stat-bar-fill::after {
    content: '';
    position: absolute;
    right: 0; top: 0; bottom: 0;
    width: 6px;
    background: white;
    opacity: 0.9;
    box-shadow: 0 0 6px white;
  }

  .bar-cyan { background: linear-gradient(90deg, #002b3a, #00f5ff); }
  .bar-purple { background: linear-gradient(90deg, #1a0030, #c084fc); }
  .bar-green { background: linear-gradient(90deg, #00200e, #4ade80); }
  .bar-orange { background: linear-gradient(90deg, #230a00, #fb923c); }

  .stat-val {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.68rem;
    color: #9d00ff;
    width: 30px;
    text-align: right;
  }

  /* PROJECTS */
  .project-card {
    background: #040e20;
    border: 1px solid #00f5ff1a;
    border-radius: 3px;
    padding: 1rem 1.1rem;
    margin-bottom: 10px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }

  .project-card:hover {
    border-color: #00f5ff44;
    background: #060f22;
    transform: translateX(4px);
  }

  .project-card::after {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 2px;
    background: linear-gradient(180deg, #00f5ff, #9d00ff);
  }

  .project-name {
    font-family: 'Orbitron', monospace;
    font-size: 0.75rem;
    color: #00f5ff;
    letter-spacing: 0.1em;
  }

  .project-desc {
    font-size: 0.85rem;
    color: #7090a8;
    margin-top: 4px;
    font-weight: 300;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
    margin-top: 8px;
  }

  .ptag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.6rem;
    padding: 2px 8px;
    border-radius: 2px;
    letter-spacing: 0.1em;
  }
  .ptag-c { color: #00f5ff; background: #00f5ff11; border: 1px solid #00f5ff22; }
  .ptag-p { color: #c084fc; background: #9d00ff0d; border: 1px solid #9d00ff22; }
  .ptag-g { color: #4ade80; background: #22c55e0d; border: 1px solid #22c55e22; }
  .ptag-o { color: #fb923c; background: #f9731608; border: 1px solid #f9731622; }

  /* CONTACT */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
    gap: 10px;
  }

  .contact-card {
    border: 1px solid #00f5ff1a;
    border-radius: 3px;
    padding: 14px;
    text-align: center;
    text-decoration: none;
    display: block;
    transition: all 0.3s;
    background: #040e1c;
  }

  .contact-card:hover {
    border-color: #00f5ff66;
    background: #00f5ff0a;
    transform: translateY(-3px);
    box-shadow: 0 8px 30px #00f5ff15;
  }

  .contact-icon {
    font-size: 1.4rem;
    margin-bottom: 6px;
  }

  .contact-name {
    font-family: 'Orbitron', monospace;
    font-size: 0.6rem;
    color: #00f5ff;
    letter-spacing: 0.2em;
    display: block;
  }

  .contact-val {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: #506070;
    margin-top: 3px;
  }

  /* FOOTER */
  .footer {
    text-align: center;
    padding: 2rem 0 1rem;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: #203040;
    letter-spacing: 0.2em;
  }

  .footer span { color: #00f5ff44; }

  /* CORNER DECORATIONS */
  .corner-box {
    position: relative;
    padding: 4px;
  }
  .corner-box::before, .corner-box::after {
    content: '';
    position: absolute;
    width: 10px; height: 10px;
    border-color: #00f5ff44;
    border-style: solid;
  }
  .corner-box::before { top: 0; left: 0; border-width: 1px 0 0 1px; }
  .corner-box::after { bottom: 0; right: 0; border-width: 0 1px 1px 0; }

  /* GITHUB STATS GRID */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
  }

  .stat-card {
    background: #040e20;
    border: 1px solid #00f5ff1a;
    border-radius: 3px;
    padding: 1rem;
    text-align: center;
  }

  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 1.6rem;
    font-weight: 700;
    color: #00f5ff;
    text-shadow: 0 0 20px #00f5ff55;
    display: block;
    animation: countUp 2s ease-out;
  }

  @keyframes countUp {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .stat-desc {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: #405060;
    letter-spacing: 0.1em;
    margin-top: 4px;
  }

  .flicker { animation: flicker 8s infinite; }
  @keyframes flicker {
    0%, 19%, 21%, 23%, 25%, 54%, 56%, 100% { opacity: 1; }
    20%, 24%, 55% { opacity: 0.4; }
  }
</style>
</head>
<body>

<canvas id="bg"></canvas>

<div class="page">

  <!-- HEADER -->
  <div class="header">
    <div style="font-family:'Share Tech Mono',monospace;font-size:0.65rem;color:#9d00ff;letter-spacing:0.3em;margin-bottom:0.5rem;">
      &gt; SYSTEM_BOOT :: PROFILE_LOAD :: v2.0.27
    </div>
    <div class="glitch-name">KUMARESH BISWAS</div>
    <div class="title-bar">
      <span>ECE</span> ENGINEER &bull; <span>DATA</span> SCIENTIST &bull; <span>WEB</span> DEVELOPER &bull; <span>AI</span> BUILDER
    </div>
    <div class="scan-line"></div>

    <div class="status-row">
      <span class="badge badge-cyan">&#9670; B.TECH ECE — 3rd YEAR</span>
      <span class="badge badge-purple">&#9670; TRAINEE @ IT VEDANT</span>
      <span class="badge badge-green">&#9670; OPEN TO WORK</span>
      <span class="badge badge-orange">&#9670; NAGPUR, INDIA</span>
    </div>
  </div>

  <!-- BIO PANEL -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9651;</div>
      <div class="panel-title">OPERATOR BIO</div>
      <div class="panel-tag">[SYS:ACTIVE]</div>
    </div>
    <div class="panel-body">
      <p class="bio-text">
        <span class="hi">&gt; Hello, World.</span><br><br>
        I'm a <span class="accent">data-driven developer</span> fusing electronics engineering with artificial intelligence.
        Currently mastering <span class="go">Data Science &amp; Analytics</span> at IT Vedant while pursuing my ECE degree at TGPCET, Nagpur.
        I build real-world tools — from <span class="accent">AI travel agents</span> powered by IBM Granite to
        <span class="go">BI dashboards</span> that turn raw data into insight.
        I learn by doing, ship by building, and grow by pushing limits.<span class="typing-cursor"></span>
      </p>
    </div>
  </div>

  <!-- SKILL BARS -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9632;</div>
      <div class="panel-title">CAPABILITY INDEX</div>
      <div class="panel-tag">[SCAN COMPLETE]</div>
    </div>
    <div class="panel-body">
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-cyan"></span>Python / Data</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-cyan" style="width:82%"></div></div>
        <div class="stat-val">82%</div>
      </div>
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-purple"></span>Web Dev</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-purple" style="width:88%"></div></div>
        <div class="stat-val">88%</div>
      </div>
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-green"></span>SQL / MongoDB</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-green" style="width:75%"></div></div>
        <div class="stat-val">75%</div>
      </div>
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-cyan"></span>C Programming</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-cyan" style="width:80%"></div></div>
        <div class="stat-val">80%</div>
      </div>
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-orange"></span>AI / ML</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-orange" style="width:68%"></div></div>
        <div class="stat-val">68%</div>
      </div>
      <div class="stat-row">
        <div class="stat-label"><span class="dot dot-purple"></span>UI/UX Design</div>
        <div class="stat-bar-bg"><div class="stat-bar-fill bar-purple" style="width:72%"></div></div>
        <div class="stat-val">72%</div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9670;</div>
      <div class="panel-title">TECH STACK MANIFEST</div>
      <div class="panel-tag">[30 MODULES LOADED]</div>
    </div>
    <div class="panel-body">
      <div style="font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:#304050;letter-spacing:0.2em;margin-bottom:10px;">// LANGUAGES</div>
      <div class="skill-grid" style="margin-bottom:14px;">
        <div class="skill-chip"><span class="dot dot-cyan"></span>Python</div>
        <div class="skill-chip"><span class="dot dot-cyan"></span>C</div>
        <div class="skill-chip"><span class="dot dot-cyan"></span>JavaScript</div>
        <div class="skill-chip"><span class="dot dot-cyan"></span>HTML5</div>
        <div class="skill-chip"><span class="dot dot-cyan"></span>SQL</div>
      </div>
      <div style="font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:#304050;letter-spacing:0.2em;margin-bottom:10px;">// DATA &amp; AI</div>
      <div class="skill-grid" style="margin-bottom:14px;">
        <div class="skill-chip"><span class="dot dot-purple"></span>NumPy</div>
        <div class="skill-chip"><span class="dot dot-purple"></span>Pandas</div>
        <div class="skill-chip"><span class="dot dot-purple"></span>Matplotlib</div>
        <div class="skill-chip"><span class="dot dot-purple"></span>Plotly</div>
        <div class="skill-chip"><span class="dot dot-purple"></span>TensorFlow</div>
        <div class="skill-chip"><span class="dot dot-purple"></span>Chart.js</div>
      </div>
      <div style="font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:#304050;letter-spacing:0.2em;margin-bottom:10px;">// DATABASE &amp; CLOUD</div>
      <div class="skill-grid" style="margin-bottom:14px;">
        <div class="skill-chip"><span class="dot dot-green"></span>MongoDB</div>
        <div class="skill-chip"><span class="dot dot-green"></span>MySQL</div>
        <div class="skill-chip"><span class="dot dot-green"></span>AWS</div>
        <div class="skill-chip"><span class="dot dot-green"></span>GCP</div>
        <div class="skill-chip"><span class="dot dot-green"></span>Vercel</div>
        <div class="skill-chip"><span class="dot dot-green"></span>Netlify</div>
      </div>
      <div style="font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:#304050;letter-spacing:0.2em;margin-bottom:10px;">// TOOLS</div>
      <div class="skill-grid">
        <div class="skill-chip"><span class="dot dot-orange"></span>Git</div>
        <div class="skill-chip"><span class="dot dot-orange"></span>GitHub</div>
        <div class="skill-chip"><span class="dot dot-orange"></span>Canva</div>
        <div class="skill-chip"><span class="dot dot-orange"></span>Lightroom</div>
        <div class="skill-chip"><span class="dot dot-orange"></span>IBM Cloud</div>
      </div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9679;</div>
      <div class="panel-title">PROJECT LOG</div>
      <div class="panel-tag">[4 MISSIONS DEPLOYED]</div>
    </div>
    <div class="panel-body">

      <div class="project-card">
        <div class="project-name">&#62; TRAVEL PLANNER AI AGENT</div>
        <div class="project-desc">IBM Granite-powered agentic travel planner — parses natural language, builds itineraries, integrates real-time cloud APIs.</div>
        <div class="project-tags">
          <span class="ptag ptag-p">IBM Granite</span>
          <span class="ptag ptag-c">IBM Cloud</span>
          <span class="ptag ptag-g">AI Agent</span>
          <span class="ptag ptag-o">NLP</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-name">&#62; BI DASHBOARD — AI TOOL USAGE</div>
        <div class="project-desc">Single-file business intelligence dashboard for student AI tool usage data — KPI cards, interactive filters, multi-chart visualizations.</div>
        <div class="project-tags">
          <span class="ptag ptag-c">Chart.js</span>
          <span class="ptag ptag-p">HTML/CSS/JS</span>
          <span class="ptag ptag-g">Data Analytics</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-name">&#62; TRAFFIC MANAGEMENT SYSTEM</div>
        <div class="project-desc">Smart traffic control web app with live data flow and MongoDB backend for real-time signal management.</div>
        <div class="project-tags">
          <span class="ptag ptag-c">JavaScript</span>
          <span class="ptag ptag-p">MongoDB</span>
          <span class="ptag ptag-g">CSS</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-name">&#62; DARK PORTFOLIO WEBSITE</div>
        <div class="project-desc">Animated dark-themed portfolio showcasing ECE + AI background — animated skill trees, project cards, experience timeline.</div>
        <div class="project-tags">
          <span class="ptag ptag-c">HTML</span>
          <span class="ptag ptag-p">CSS Animations</span>
          <span class="ptag ptag-g">UI/UX</span>
          <span class="ptag ptag-o">JavaScript</span>
        </div>
      </div>

    </div>
  </div>

  <!-- GITHUB STATS -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9651;</div>
      <div class="panel-title">GITHUB TELEMETRY</div>
      <div class="panel-tag">[USER: Kumaresh2005]</div>
    </div>
    <div class="panel-body">
      <div class="stats-grid">
        <div class="stat-card">
          <span class="stat-num flicker">∞</span>
          <div class="stat-desc">COMMITS</div>
        </div>
        <div class="stat-card">
          <span class="stat-num">07+</span>
          <div class="stat-desc">REPOS</div>
        </div>
        <div class="stat-card">
          <span class="stat-num">100%</span>
          <div class="stat-desc">PASSION</div>
        </div>
      </div>
      <div style="margin-top:12px;text-align:center;">
        <img src="https://streak-stats.demolab.com/?user=Kumaresh2005&theme=dark&hide_border=true&background=020510&ring=00f5ff&fire=9d00ff&currStreakLabel=00f5ff&sideLabels=7090a8&dates=405060&currStreakNum=00f5ff&sideNums=c084fc" style="max-width:100%;border-radius:3px;" alt="GitHub Streak Stats"/>
      </div>
      <div style="margin-top:10px;text-align:center;">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Kumaresh2005&theme=dark&hide_border=true&bg_color=020510&title_color=00f5ff&text_color=7090a8&layout=compact" style="max-width:100%;border-radius:3px;" alt="Top Languages"/>
      </div>
    </div>
  </div>

  <!-- CONNECT -->
  <div class="panel">
    <div class="panel-header">
      <div class="panel-icon">&#9671;</div>
      <div class="panel-title">COMMS UPLINK</div>
      <div class="panel-tag">[3 CHANNELS OPEN]</div>
    </div>
    <div class="panel-body">
      <div class="contact-grid">
        <a href="https://www.linkedin.com/in/kumaresh-biswas" class="contact-card">
          <div class="contact-icon">&#128279;</div>
          <span class="contact-name">LINKEDIN</span>
          <div class="contact-val">kumaresh-biswas</div>
        </a>
        <a href="https://instagram.com/kumar_biswas_18" class="contact-card">
          <div class="contact-icon">&#128247;</div>
          <span class="contact-name">INSTAGRAM</span>
          <div class="contact-val">kumar_biswas_18</div>
        </a>
        <a href="mailto:biwaskumaresh89@gmail.com" class="contact-card">
          <div class="contact-icon">&#128140;</div>
          <span class="contact-name">EMAIL</span>
          <div class="contact-val">biwaskumaresh89</div>
        </a>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <span>// PROFILE RENDER COMPLETE</span> &bull; BUILT BY KUMARESH BISWAS &bull; <span>// NAGPUR :: 2026</span>
  </div>

</div>

<script>
  const canvas = document.getElementById('bg');
  const ctx = canvas.getContext('2d');

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = document.body.scrollHeight;
  }
  resize();

  const particles = [];
  for (let i = 0; i < 90; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 1.2 + 0.3,
      vx: (Math.random() - 0.5) * 0.2,
      vy: (Math.random() - 0.5) * 0.2,
      alpha: Math.random() * 0.5 + 0.2,
      color: Math.random() > 0.6 ? '#00f5ff' : (Math.random() > 0.5 ? '#9d00ff' : '#4ade80')
    });
  }

  const lines = [];
  for (let i = 0; i < 6; i++) {
    lines.push({
      x: Math.random() * canvas.width,
      y: 0,
      speed: Math.random() * 1.5 + 0.5,
      alpha: Math.random() * 0.05 + 0.02,
      width: Math.random() * 1.5 + 0.5
    });
  }

  let frame = 0;

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    ctx.strokeStyle = '#00f5ff06';
    ctx.lineWidth = 0.5;
    for (let x = 0; x < canvas.width; x += 50) {
      ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, canvas.height); ctx.stroke();
    }
    for (let y = 0; y < canvas.height; y += 50) {
      ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(canvas.width, y); ctx.stroke();
    }

    lines.forEach(l => {
      ctx.strokeStyle = `rgba(0,245,255,${l.alpha})`;
      ctx.lineWidth = l.width;
      ctx.beginPath(); ctx.moveTo(l.x, l.y); ctx.lineTo(l.x, l.y + 80); ctx.stroke();
      l.y += l.speed;
      if (l.y > canvas.height) { l.y = -80; l.x = Math.random() * canvas.width; }
    });

    particles.forEach(p => {
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = p.color + Math.floor(p.alpha * 255).toString(16).padStart(2,'0');
      ctx.fill();
      p.x += p.vx; p.y += p.vy;
      if (p.x < 0) p.x = canvas.width;
      if (p.x > canvas.width) p.x = 0;
      if (p.y < 0) p.y = canvas.height;
      if (p.y > canvas.height) p.y = 0;
    });

    frame++;
    requestAnimationFrame(draw);
  }

  draw();
  window.addEventListener('resize', () => { resize(); });
</script>
</body>
</html>
