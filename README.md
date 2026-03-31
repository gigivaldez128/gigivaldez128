<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap');

  :root {
    --bg: #080b10;
    --surface: #0d1117;
    --surface2: #141921;
    --green: #49F707;
    --cyan: #00f5ff;
    --pink: #ff2d78;
    --yellow: #ffe600;
    --text: #e6edf3;
    --muted: #7d8590;
    --border: rgba(73,247,7,0.15);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* Animated grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(73,247,7,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(73,247,7,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
    animation: gridShift 20s linear infinite;
  }

  @keyframes gridShift {
    0% { background-position: 0 0; }
    100% { background-position: 40px 40px; }
  }

  .noise {
    position: fixed;
    inset: 0;
    opacity: 0.025;
    pointer-events: none;
    z-index: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  }

  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 780px;
    margin: 0 auto;
    padding: 40px 24px 80px;
  }

  /* ── HERO ── */
  .hero {
    position: relative;
    padding: 48px 0 40px;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeUp 0.7s ease forwards 0.1s;
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--green);
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .hero-tag::before {
    content: '';
    display: inline-block;
    width: 28px; height: 1px;
    background: var(--green);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(44px, 8vw, 72px);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -2px;
    margin-bottom: 8px;
  }

  .hero-name .first { color: var(--text); }
  .hero-name .last {
    color: transparent;
    -webkit-text-stroke: 2px var(--green);
    position: relative;
  }

  .hero-name .last::after {
    content: attr(data-text);
    position: absolute;
    left: 0; top: 0;
    color: var(--green);
    clip-path: inset(0 100% 0 0);
    animation: revealText 1.2s cubic-bezier(0.77,0,0.175,1) forwards 0.8s;
  }

  @keyframes revealText {
    to { clip-path: inset(0 0% 0 0); }
  }

  .hero-alias {
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 24px;
    letter-spacing: 1px;
  }

  .hero-alias span {
    color: var(--cyan);
    font-weight: 700;
  }

  /* Typing animation */
  .typing-line {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 14px;
    margin-bottom: 32px;
    color: var(--muted);
  }
  .typing-text {
    color: var(--green);
    font-weight: 700;
    border-right: 2px solid var(--green);
    padding-right: 2px;
    animation: blink 0.75s step-end infinite;
    white-space: nowrap;
    overflow: hidden;
  }
  @keyframes blink { 50% { border-color: transparent; } }

  /* contact pills */
  .contact-row {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 48px;
  }

  .pill {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    padding: 7px 14px;
    border: 1px solid var(--border);
    border-radius: 4px;
    font-size: 11px;
    letter-spacing: 1px;
    text-decoration: none;
    color: var(--muted);
    background: var(--surface);
    transition: all 0.2s ease;
    position: relative;
    overflow: hidden;
  }

  .pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--green);
    transform: translateX(-100%);
    transition: transform 0.2s ease;
    z-index: 0;
  }

  .pill:hover::before { transform: translateX(0); }
  .pill:hover { color: #000; border-color: var(--green); }
  .pill > * { position: relative; z-index: 1; }

  .pill .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--green);
    transition: background 0.2s;
  }
  .pill:hover .dot { background: #000; }

  /* ── SECTION ── */
  .section {
    margin-bottom: 48px;
    opacity: 0;
    transform: translateY(20px);
  }

  .section.visible {
    animation: fadeUp 0.6s ease forwards;
  }

  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
  }

  .section-num {
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--green);
    opacity: 0.7;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 700;
    letter-spacing: -0.5px;
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── STATUS CARDS ── */
  .status-grid {
    display: grid;
    gap: 10px;
  }

  .status-card {
    display: flex;
    align-items: flex-start;
    gap: 14px;
    padding: 16px 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    transition: border-color 0.2s, transform 0.2s;
    cursor: default;
  }

  .status-card:hover {
    border-color: rgba(73,247,7,0.5);
    transform: translateX(4px);
  }

  .status-icon {
    font-size: 18px;
    flex-shrink: 0;
    margin-top: 1px;
  }

  .status-label {
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--green);
    text-transform: uppercase;
    margin-bottom: 4px;
    opacity: 0.8;
  }

  .status-text {
    font-size: 13px;
    color: var(--text);
    line-height: 1.5;
  }

  .status-text strong {
    color: var(--cyan);
  }

  /* ── TECH GRID ── */
  .tech-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .tech-chip {
    padding: 6px 13px;
    font-size: 11px;
    letter-spacing: 1px;
    border-radius: 3px;
    border: 1px solid var(--border);
    background: var(--surface);
    color: var(--muted);
    transition: all 0.2s ease;
    position: relative;
    cursor: default;
  }

  .tech-chip:hover {
    background: var(--green);
    color: #000;
    border-color: var(--green);
    transform: translateY(-2px);
    box-shadow: 0 4px 16px rgba(73,247,7,0.3);
  }

  .tech-chip.featured {
    border-color: rgba(73,247,7,0.4);
    color: var(--green);
  }

  /* ── STATS ROW ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .stat-cell {
    background: var(--surface);
    padding: 24px 20px;
    text-align: center;
    transition: background 0.2s;
  }

  .stat-cell:hover { background: var(--surface2); }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    color: var(--green);
    display: block;
    line-height: 1;
    margin-bottom: 6px;
    counter-reset: num var(--n);
  }

  .stat-label {
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--muted);
    text-transform: uppercase;
  }

  /* ── TERMINAL BLOCK ── */
  .terminal {
    background: #0a0f0a;
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .terminal-bar {
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 10px 16px;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
  }

  .t-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
  }
  .t-dot.red { background: #ff5f57; }
  .t-dot.yellow { background: #ffbd2e; }
  .t-dot.green { background: #28c840; }

  .terminal-title {
    font-size: 11px;
    color: var(--muted);
    margin-left: 6px;
    letter-spacing: 1px;
  }

  .terminal-body {
    padding: 20px 20px;
    font-size: 12px;
    line-height: 2;
  }

  .t-line { display: flex; align-items: center; gap: 8px; }
  .t-prompt { color: var(--green); }
  .t-cmd { color: var(--cyan); }
  .t-out { color: var(--muted); padding-left: 20px; }
  .t-out .hl { color: var(--yellow); }
  .t-out .hl2 { color: var(--pink); }

  /* ── FOOTER ── */
  .footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 32px;
    border-top: 1px solid var(--border);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
    flex-wrap: wrap;
    gap: 12px;
  }

  .footer-pulse {
    display: flex;
    align-items: center;
    gap: 7px;
  }

  .pulse-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--green);
    position: relative;
  }

  .pulse-dot::after {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    border: 1px solid var(--green);
    animation: pulse 1.5s ease-out infinite;
  }

  @keyframes pulse {
    0% { opacity: 1; transform: scale(1); }
    100% { opacity: 0; transform: scale(2.5); }
  }

  /* scan line effect */
  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, rgba(73,247,7,0.15), transparent);
    animation: scanDown 6s linear infinite;
    pointer-events: none;
    z-index: 9;
  }

  @keyframes scanDown {
    0% { top: -2px; }
    100% { top: 100vh; }
  }

  /* Glitch title effect */
  .glitch {
    position: relative;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    inset: 0;
    opacity: 0;
  }
  .glitch:hover::before {
    color: var(--cyan);
    clip-path: polygon(0 0,100% 0,100% 33%,0 33%);
    transform: translateX(-2px);
    opacity: 0.8;
    animation: glitch1 0.3s steps(2) forwards;
  }
  .glitch:hover::after {
    color: var(--pink);
    clip-path: polygon(0 67%,100% 67%,100% 100%,0 100%);
    transform: translateX(2px);
    opacity: 0.8;
    animation: glitch2 0.3s steps(2) forwards;
  }
  @keyframes glitch1 { 0%,100% { transform: translateX(-2px); } 50% { transform: translateX(2px); } }
  @keyframes glitch2 { 0%,100% { transform: translateX(2px); } 50% { transform: translateX(-2px); } }
</style>
</head>
<body>
<div class="noise"></div>
<div class="scanline"></div>

<div class="wrapper">

  <!-- HERO -->
  <header class="hero">
    <div class="hero-tag">Portfolio · 2025</div>
    <h1 class="hero-name">
      <span class="first">GIGI </span><br>
      <span class="last glitch" data-text="VALDEZ">VALDEZ</span>
    </h1>
    <p class="hero-alias">Call me <span>GIGI</span> — not GEGE, ever.</p>
    <div class="typing-line">
      &gt; <span class="typing-text" id="typing"></span>
    </div>
    <div class="contact-row">
      <a class="pill" href="mailto:gigivaldez128@gmail.com">
        <div class="dot"></div> gigivaldez128@gmail.com
      </a>
      <a class="pill" href="https://www.linkedin.com/in/gigivaldez/">
        <div class="dot"></div> LinkedIn
      </a>
      <a class="pill" href="https://gigivaldez128.github.io/portfolio/">
        <div class="dot"></div> Portfolio
      </a>
      <a class="pill" href="https://www.instagram.com/ionictech1/">
        <div class="dot"></div> @gigivaldez128
      </a>
    </div>
  </header>

  <!-- TERMINAL -->
  <div class="section visible" style="animation-delay:0.2s">
    <div class="terminal">
      <div class="terminal-bar">
        <div class="t-dot red"></div>
        <div class="t-dot yellow"></div>
        <div class="t-dot green"></div>
        <span class="terminal-title">gigi@dev ~ bash</span>
      </div>
      <div class="terminal-body">
        <div class="t-line"><span class="t-prompt">$</span><span class="t-cmd">whoami</span></div>
        <div class="t-line t-out"><span class="hl">Gigi Valdez</span> — Full-Stack Developer, 23 y/o</div>
        <div class="t-line"><span class="t-prompt">$</span><span class="t-cmd">cat skills.txt</span></div>
        <div class="t-line t-out">React.js · Node.js · PHP · MongoDB · Angular</div>
        <div class="t-line"><span class="t-prompt">$</span><span class="t-cmd">echo $STATUS</span></div>
        <div class="t-line t-out"><span class="hl2">open to work</span> · seeking Web Dev &amp; SWE roles</div>
        <div class="t-line"><span class="t-prompt">$</span><span class="t-cmd">_</span></div>
      </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="section" id="s1">
    <div class="stats-row">
      <div class="stat-cell">
        <span class="stat-num" id="cnt-years">0</span>
        <span class="stat-label">Years XP</span>
      </div>
      <div class="stat-cell">
        <span class="stat-num" id="cnt-stack">0</span>
        <span class="stat-label">Tech Stack</span>
      </div>
      <div class="stat-cell">
        <span class="stat-num" id="cnt-focus">2</span>
        <span class="stat-label">Disciplines</span>
      </div>
    </div>
  </div>

  <!-- STATUS -->
  <div class="section" id="s2">
    <div class="section-header">
      <span class="section-num">01</span>
      <h2 class="section-title">Current Status</h2>
      <div class="section-line"></div>
    </div>
    <div class="status-grid">
      <div class="status-card">
        <div class="status-icon">💼</div>
        <div>
          <div class="status-label">Role</div>
          <div class="status-text">Full-Stack <strong>React.js / Node.js</strong> Developer</div>
        </div>
      </div>
      <div class="status-card">
        <div class="status-icon">🔍</div>
        <div>
          <div class="status-label">Looking For</div>
          <div class="status-text">Connections in <strong>Web Development</strong> &amp; <strong>Software Engineering</strong></div>
        </div>
      </div>
      <div class="status-card">
        <div class="status-icon">💬</div>
        <div>
          <div class="status-label">Let's Talk About</div>
          <div class="status-text">Full Stack Development · <strong>NFT Projects</strong> · Open Source</div>
        </div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section" id="s3">
    <div class="section-header">
      <span class="section-num">02</span>
      <h2 class="section-title">Tech Stack</h2>
      <div class="section-line"></div>
    </div>
    <div class="tech-grid">
      <div class="tech-chip featured">React.js</div>
      <div class="tech-chip featured">Node.js</div>
      <div class="tech-chip featured">JavaScript</div>
      <div class="tech-chip">HTML5</div>
      <div class="tech-chip">CSS3</div>
      <div class="tech-chip">PHP</div>
      <div class="tech-chip">Angular</div>
      <div class="tech-chip">MongoDB</div>
      <div class="tech-chip">Bootstrap</div>
      <div class="tech-chip">Babel</div>
      <div class="tech-chip">Git</div>
      <div class="tech-chip">VS Code</div>
      <div class="tech-chip">Figma</div>
      <div class="tech-chip">Canva</div>
      <div class="tech-chip">Eclipse</div>
    </div>
  </div>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer-pulse">
      <div class="pulse-dot"></div>
      Available for opportunities
    </div>
    <span>Last updated · 2025</span>
    <span style="color:var(--green)">gigivaldez128</span>
  </footer>

</div>

<script>
  // Typing animation
  const phrases = [
    "Front-end Web Developer",
    "Back-end Developer",
    "Full-Stack React / Node",
    "Open to Collaborate 🚀"
  ];
  let pi = 0, ci = 0, deleting = false;
  const el = document.getElementById('typing');

  function type() {
    const current = phrases[pi];
    if (!deleting) {
      el.textContent = current.slice(0, ++ci);
      if (ci === current.length) { deleting = true; return setTimeout(type, 1800); }
    } else {
      el.textContent = current.slice(0, --ci);
      if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; }
    }
    setTimeout(type, deleting ? 40 : 70);
  }
  type();

  // Count-up animation
  function countUp(el, target, duration = 1200) {
    const start = performance.now();
    function update(now) {
      const t = Math.min((now - start) / duration, 1);
      el.textContent = Math.round(t * target);
      if (t < 1) requestAnimationFrame(update);
    }
    requestAnimationFrame(update);
  }

  // Scroll-triggered sections
  const sections = document.querySelectorAll('.section:not(.visible)');
  let statsTriggered = false;

  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        if ((e.target.id === 's1') && !statsTriggered) {
          statsTriggered = true;
          setTimeout(() => {
            countUp(document.getElementById('cnt-years'), 3);
            countUp(document.getElementById('cnt-stack'), 15);
          }, 200);
        }
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  sections.forEach(s => obs.observe(s));
</script>
</body>
</html>
