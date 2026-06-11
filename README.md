# gia.github.io
index.html
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gia Mokshagundam — Aerospace Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@300;400;700&family=Space+Grotesk:wght@300;400;500;600;700&family=Zen+Kaku+Gothic+New:wght@300;400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #0a0a14;
    --deep: #0d0d1f;
    --void: #060610;
    --sakura: #f4a8c7;
    --sakura-dim: #c97da8;
    --gold: #e8c97a;
    --ice: #a8d8f4;
    --fog: #b8b8d4;
    --white: #f0f0fa;
    --jellyfish: #7b68ee;
    --jellyfish-glow: #9d89ff;
    --turbine: #4a9eff;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--void);
    color: var(--white);
    font-family: 'Space Grotesk', sans-serif;
    overflow-x: hidden;
  }

  /* ── CANVAS LAYERS ── */
  #bg-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.2rem 3rem;
    background: linear-gradient(to bottom, rgba(6,6,16,0.95), transparent);
    backdrop-filter: blur(2px);
  }

  .nav-logo {
    font-family: 'Noto Serif JP', serif;
    font-size: 1rem;
    font-weight: 300;
    letter-spacing: 0.3em;
    color: var(--sakura);
    text-decoration: none;
  }

  .nav-logo span {
    display: block;
    font-size: 0.6rem;
    color: var(--fog);
    letter-spacing: 0.5em;
    text-transform: uppercase;
    margin-top: 2px;
  }

  .nav-links {
    display: flex;
    gap: 2.5rem;
    list-style: none;
  }

  .nav-links a {
    color: var(--fog);
    text-decoration: none;
    font-size: 0.78rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--sakura);
    transition: width 0.3s;
  }

  .nav-links a:hover { color: var(--sakura); }
  .nav-links a:hover::after { width: 100%; }

  /* ── HERO ── */
  #hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    overflow: hidden;
  }

  .hero-turbine {
    position: absolute;
    right: 5%;
    top: 50%;
    transform: translateY(-50%);
    width: 420px;
    height: 420px;
    opacity: 0.85;
  }

  .hero-content {
    position: relative;
    z-index: 2;
    max-width: 700px;
    padding: 0 3rem;
  }

  .hero-jp {
    font-family: 'Noto Serif JP', serif;
    font-size: 0.85rem;
    letter-spacing: 0.4em;
    color: var(--sakura-dim);
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 1s 0.3s forwards;
  }

  .hero-name {
    font-family: 'Noto Serif JP', serif;
    font-size: clamp(2.8rem, 5vw, 4.5rem);
    font-weight: 700;
    line-height: 1.1;
    margin-bottom: 0.5rem;
    opacity: 0;
    animation: fadeUp 1s 0.5s forwards;
  }

  .hero-name .given {
    color: var(--white);
  }

  .hero-name .family {
    color: var(--sakura);
    display: block;
    font-weight: 300;
    font-size: 0.65em;
    letter-spacing: 0.2em;
    margin-top: 0.2em;
  }

  .hero-title {
    font-size: 0.9rem;
    letter-spacing: 0.35em;
    color: var(--ice);
    text-transform: uppercase;
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeUp 1s 0.7s forwards;
  }

  .hero-tagline {
    font-family: 'Noto Serif JP', serif;
    font-size: 1.05rem;
    color: var(--fog);
    line-height: 1.9;
    max-width: 480px;
    margin-bottom: 2.5rem;
    opacity: 0;
    animation: fadeUp 1s 0.9s forwards;
  }

  .hero-tagline em {
    color: var(--gold);
    font-style: normal;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 1s 1.1s forwards;
  }

  .btn {
    padding: 0.75rem 2rem;
    border-radius: 2px;
    font-size: 0.8rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    text-decoration: none;
    cursor: pointer;
    transition: all 0.3s;
    font-family: 'Space Grotesk', sans-serif;
  }

  .btn-primary {
    background: var(--sakura);
    color: var(--void);
    border: 1px solid var(--sakura);
    font-weight: 600;
  }

  .btn-primary:hover {
    background: transparent;
    color: var(--sakura);
    box-shadow: 0 0 20px rgba(244,168,199,0.3);
  }

  .btn-ghost {
    background: transparent;
    color: var(--fog);
    border: 1px solid rgba(184,184,212,0.3);
  }

  .btn-ghost:hover {
    border-color: var(--ice);
    color: var(--ice);
    box-shadow: 0 0 20px rgba(168,216,244,0.15);
  }

  /* ── SECTION BASE ── */
  section {
    position: relative;
    z-index: 1;
    padding: 7rem 3rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-label {
    font-size: 0.7rem;
    letter-spacing: 0.5em;
    text-transform: uppercase;
    color: var(--sakura-dim);
    margin-bottom: 0.6rem;
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .section-label::before {
    content: '';
    width: 30px;
    height: 1px;
    background: var(--sakura-dim);
  }

  .section-title {
    font-family: 'Noto Serif JP', serif;
    font-size: clamp(1.8rem, 3vw, 2.8rem);
    font-weight: 700;
    margin-bottom: 0.5rem;
    color: var(--white);
  }

  .section-jp {
    font-family: 'Noto Serif JP', serif;
    font-size: 0.8rem;
    color: var(--fog);
    letter-spacing: 0.3em;
    margin-bottom: 3rem;
  }

  /* ── DIVIDER ── */
  .full-divider {
    width: 100%;
    height: 1px;
    background: linear-gradient(to right, transparent, rgba(244,168,199,0.2), transparent);
    margin: 0;
  }

  /* ── JELLYFISH SECTION ── */
  #about {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6rem;
    align-items: center;
  }

  .about-visual {
    position: relative;
    display: flex;
    justify-content: center;
  }

  #jellyfish-canvas {
    width: 320px;
    height: 400px;
    border-radius: 4px;
  }

  .about-text p {
    color: var(--fog);
    line-height: 1.9;
    font-size: 0.95rem;
    margin-bottom: 1.2rem;
  }

  .about-text p strong {
    color: var(--sakura);
  }

  .stats-row {
    display: flex;
    gap: 2.5rem;
    margin-top: 2.5rem;
    padding-top: 2.5rem;
    border-top: 1px solid rgba(255,255,255,0.06);
  }

  .stat { }

  .stat-num {
    font-family: 'Noto Serif JP', serif;
    font-size: 2rem;
    font-weight: 700;
    color: var(--gold);
    line-height: 1;
  }

  .stat-label {
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    color: var(--fog);
    text-transform: uppercase;
    margin-top: 0.3rem;
  }

  /* ── EXPERIENCE ── */
  #experience {
    max-width: 1200px;
  }

  .exp-grid {
    display: grid;
    gap: 1.5rem;
  }

  .exp-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    border-left: 2px solid var(--sakura-dim);
    padding: 2rem 2.5rem;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }

  .exp-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: linear-gradient(135deg, rgba(244,168,199,0.03), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .exp-card:hover { border-left-color: var(--sakura); transform: translateX(4px); }
  .exp-card:hover::before { opacity: 1; }

  .exp-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 0.8rem;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .exp-role {
    font-size: 1rem;
    font-weight: 600;
    color: var(--white);
  }

  .exp-company {
    font-size: 0.82rem;
    color: var(--sakura);
    margin-top: 0.15rem;
    letter-spacing: 0.05em;
  }

  .exp-date {
    font-size: 0.72rem;
    color: var(--fog);
    letter-spacing: 0.1em;
    text-align: right;
    background: rgba(255,255,255,0.04);
    padding: 0.3rem 0.8rem;
    border-radius: 2px;
    white-space: nowrap;
  }

  .exp-bullets {
    list-style: none;
    margin-top: 0.8rem;
  }

  .exp-bullets li {
    font-size: 0.85rem;
    color: var(--fog);
    line-height: 1.7;
    padding-left: 1.2rem;
    position: relative;
    margin-bottom: 0.3rem;
  }

  .exp-bullets li::before {
    content: '›';
    position: absolute;
    left: 0;
    color: var(--sakura-dim);
  }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .project-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.06);
    padding: 2rem;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }

  .project-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 0; height: 2px;
    background: linear-gradient(to right, var(--turbine), var(--jellyfish-glow));
    transition: width 0.4s;
  }

  .project-card:hover { transform: translateY(-4px); border-color: rgba(74,158,255,0.2); }
  .project-card:hover::after { width: 100%; }

  .project-icon {
    font-size: 1.8rem;
    margin-bottom: 1rem;
  }

  .project-name {
    font-size: 0.95rem;
    font-weight: 600;
    color: var(--white);
    margin-bottom: 0.5rem;
  }

  .project-desc {
    font-size: 0.82rem;
    color: var(--fog);
    line-height: 1.7;
  }

  /* ── SKILLS ── */
  .skills-layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
  }

  .skill-group-title {
    font-size: 0.72rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--sakura-dim);
    margin-bottom: 1.5rem;
  }

  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.6rem;
  }

  .skill-tag {
    padding: 0.4rem 1rem;
    border: 1px solid rgba(255,255,255,0.08);
    font-size: 0.78rem;
    color: var(--fog);
    letter-spacing: 0.05em;
    transition: all 0.2s;
    background: rgba(255,255,255,0.02);
  }

  .skill-tag:hover {
    border-color: var(--turbine);
    color: var(--ice);
    background: rgba(74,158,255,0.06);
  }

  .soft-list {
    list-style: none;
    display: grid;
    gap: 0.8rem;
  }

  .soft-list li {
    display: flex;
    align-items: center;
    gap: 0.8rem;
    font-size: 0.88rem;
    color: var(--fog);
  }

  .soft-list li::before {
    content: '';
    width: 20px;
    height: 1px;
    background: var(--gold);
    flex-shrink: 0;
  }

  /* ── CERTIFICATIONS ── */
  .cert-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 1rem;
  }

  .cert-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    padding: 1.2rem 1.5rem;
    transition: all 0.25s;
  }

  .cert-card:hover {
    border-color: rgba(232,201,122,0.3);
    background: rgba(232,201,122,0.04);
  }

  .cert-name {
    font-size: 0.85rem;
    color: var(--white);
    margin-bottom: 0.3rem;
    line-height: 1.5;
  }

  .cert-issuer {
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--gold);
  }

  /* ── CONTACT ── */
  #contact {
    text-align: center;
    padding-bottom: 6rem;
  }

  .contact-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
    margin-top: 3rem;
  }

  .contact-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    text-decoration: none;
    transition: all 0.3s;
    padding: 1.5rem 2.5rem;
    border: 1px solid rgba(255,255,255,0.06);
    background: rgba(255,255,255,0.02);
    min-width: 160px;
  }

  .contact-item:hover {
    border-color: var(--sakura-dim);
    transform: translateY(-4px);
    background: rgba(244,168,199,0.04);
  }

  .contact-icon { font-size: 1.5rem; }
  .contact-label { font-size: 0.68rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--fog); }
  .contact-value { font-size: 0.82rem; color: var(--white); }

  /* ── FOOTER ── */
  footer {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 2rem 3rem;
    border-top: 1px solid rgba(255,255,255,0.05);
    color: var(--fog);
    font-size: 0.78rem;
    letter-spacing: 0.1em;
  }

  footer .jp-credit {
    font-family: 'Noto Serif JP', serif;
    color: var(--sakura-dim);
    margin-bottom: 0.4rem;
    font-size: 0.85rem;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: none;
  }

  /* ── SCROLL INDICATOR ── */
  .scroll-hint {
    position: absolute;
    bottom: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    opacity: 0;
    animation: fadeUp 1s 1.8s forwards;
  }

  .scroll-hint span {
    font-size: 0.65rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--fog);
  }

  .scroll-line {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--fog), transparent);
    animation: scrollPulse 2s infinite;
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 0.3; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.2); }
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    section { padding: 5rem 1.5rem; }
    #about { grid-template-columns: 1fr; gap: 3rem; }
    .hero-turbine { width: 250px; height: 250px; opacity: 0.3; }
    .hero-content { padding: 0 1.5rem; }
    .skills-layout { grid-template-columns: 1fr; gap: 2.5rem; }
    .stats-row { gap: 1.5rem; }
  }

  /* ── ACTIVITIES ── */
  .activities-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.2rem;
  }

  .activity-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    padding: 1.5rem;
    transition: all 0.3s;
  }

  .activity-card:hover {
    border-color: rgba(123,104,238,0.3);
    background: rgba(123,104,238,0.04);
    transform: translateY(-2px);
  }

  .activity-badge {
    display: inline-block;
    font-size: 0.65rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--jellyfish-glow);
    border: 1px solid rgba(157,137,255,0.3);
    padding: 0.2rem 0.6rem;
    margin-bottom: 0.8rem;
  }

  .activity-title {
    font-size: 0.9rem;
    font-weight: 600;
    color: var(--white);
    margin-bottom: 0.4rem;
    line-height: 1.4;
  }

  .activity-desc {
    font-size: 0.8rem;
    color: var(--fog);
    line-height: 1.6;
  }

</style>
</head>
<body>

<!-- Background canvas -->
<canvas id="bg-canvas"></canvas>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">
    GIA
    <span>航空宇宙エンジニア</span>
  </a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero" style="padding:0; max-width:100%; min-height:100vh; display:flex; align-items:center; justify-content:center; position:relative; z-index:1;">
  <!-- Turbine Engine SVG Animation -->
  <div class="hero-turbine">
    <canvas id="turbine-canvas" width="420" height="420"></canvas>
  </div>

  <div class="hero-content">
    <p class="hero-jp">空を夢見るエンジニア — Engineer Who Dreams of the Sky</p>
    <h1 class="hero-name">
      <span class="given">Gia</span>
      <span class="family">Mokshagundam</span>
    </h1>
    <p class="hero-title">Aerospace Engineer · Robotics · AI Systems</p>
    <p class="hero-tagline">
      Bridging <em>propulsion and precision</em> — from turbine blades to drone autonomy, I build at the intersection of <em>aerospace engineering</em> and intelligent systems.
    </p>
    <div class="hero-cta">
      <a href="#experience" class="btn btn-primary">View Experience</a>
      <a href="#contact" class="btn btn-ghost">Get In Touch</a>
    </div>
  </div>

  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<div class="full-divider"></div>

<!-- ABOUT -->
<section id="about">
  <div class="about-visual reveal">
    <canvas id="jellyfish-canvas" width="320" height="400"></canvas>
  </div>
  <div class="about-text">
    <p class="section-label">About Me</p>
    <h2 class="section-title">Engineer.<br>Researcher.<br>Dreamer.</h2>
    <p class="section-jp">私について — Watashi ni tsuite</p>
    <p>Aerospace Engineering graduate from <strong>Chandigarh University</strong> (B.E., CGPA 7.73/10), currently pursuing a Master's in <strong>Robotics and Automation</strong>. My work lives at the crossroads of intelligent systems, flight mechanics, and human-centered design.</p>
    <p>From designing optronic components at <strong>TATA Advanced Systems</strong> to supporting aircraft reliability workflows at <strong>Airbus</strong>, I've built experience across India's most prestigious aerospace organizations — including DRDO, HAL, and ISRO-adjacent projects.</p>
    <p>Off-hours: amateur astrographer, open-mic poet, guitar player, and <strong>Japanese (N5)</strong> learner. I believe the best engineering is also storytelling.</p>
    <div class="stats-row">
      <div class="stat">
        <div class="stat-num">4+</div>
        <div class="stat-label">Internships</div>
      </div>
      <div class="stat">
        <div class="stat-num">5</div>
        <div class="stat-label">Projects</div>
      </div>
      <div class="stat">
        <div class="stat-num">14+</div>
        <div class="stat-label">Certificates</div>
      </div>
      <div class="stat">
        <div class="stat-num">N5</div>
        <div class="stat-label">Japanese</div>
      </div>
    </div>
  </div>
</section>

<div class="full-divider"></div>

<!-- EXPERIENCE -->
<section id="experience">
  <p class="section-label reveal">Career Path</p>
  <h2 class="section-title reveal">Experience</h2>
  <p class="section-jp reveal">経験 — Keiken</p>

  <div class="exp-grid">

    <div class="exp-card reveal">
      <div class="exp-header">
        <div>
          <div class="exp-role">Reliability Intern (FTM)</div>
          <div class="exp-company">Airbus · Bangalore</div>
        </div>
        <div class="exp-date">Oct 2025 – Apr 2026</div>
      </div>
      <ul class="exp-bullets">
        <li>Supported aircraft reliability monitoring — delay checks and in-service operational data analysis within a CAMO-aligned environment</li>
        <li>Reviewed PIREPs and MAREPs; worked with ATA chapters for A320 and A350 fault classification</li>
        <li>Assisted in technical dossiers and reliability documentation with exposure to EASA / UK CAA-aligned workflows</li>
      </ul>
    </div>

    <div class="exp-card reveal">
      <div class="exp-header">
        <div>
          <div class="exp-role">Aerospace Engineer Intern</div>
          <div class="exp-company">TATA Advanced Systems Ltd · Bengaluru</div>
        </div>
        <div class="exp-date">Jan – May 2024</div>
      </div>
      <ul class="exp-bullets">
        <li>Designed high-precision optronic components to aerospace standards</li>
        <li>Conducted vibration and environmental reliability testing</li>
        <li>Integrated sensors for aerial systems</li>
      </ul>
    </div>

    <div class="exp-card reveal">
      <div class="exp-header">
        <div>
          <div class="exp-role">Aerospace Intern — Helicopter MRO</div>
          <div class="exp-company">Hindustan Aeronautics Limited · Bengaluru</div>
        </div>
        <div class="exp-date">Jun – Jul 2023</div>
      </div>
      <ul class="exp-bullets">
        <li>Evaluated rotorcraft materials — composite and metallic structures</li>
        <li>Analyzed lift, thrust, and aerodynamic characteristics</li>
        <li>Authored documentation for aircraft maintenance processes</li>
      </ul>
    </div>

    <div class="exp-card reveal">
      <div class="exp-header">
        <div>
          <div class="exp-role">UAV Design Intern</div>
          <div class="exp-company">DRDO · Delhi</div>
        </div>
        <div class="exp-date">Jun – Aug 2022</div>
      </div>
      <ul class="exp-bullets">
        <li>Designed fixed-wing UAVs for varied terrain operations</li>
        <li>Performed CFD simulations in ANSYS Fluent for lift-drag validation</li>
        <li>Supervised flight testing and performance reviews</li>
      </ul>
    </div>

  </div>
</section>

<div class="full-divider"></div>

<!-- PROJECTS -->
<section id="projects">
  <p class="section-label reveal">What I've Built</p>
  <h2 class="section-title reveal">Projects</h2>
  <p class="section-jp reveal">プロジェクト — Purojekuto</p>

  <div class="projects-grid">
    <div class="project-card reveal">
      <div class="project-icon">🛸</div>
      <div class="project-name">Modular Surveillance UAV</div>
      <div class="project-desc">Fixed-wing drone with drag optimization using CFD and SolidWorks. Designed for modular payload swaps and terrain adaptability.</div>
    </div>
    <div class="project-card reveal">
      <div class="project-icon">✈️</div>
      <div class="project-name">CJ-1 Jet Trainer Design</div>
      <div class="project-desc">T-tail subsonic jet trainer with full control surface and payload optimization for cadet training environments.</div>
    </div>
    <div class="project-card reveal">
      <div class="project-icon">📡</div>
      <div class="project-name">RC Aircraft</div>
      <div class="project-desc">Servo-controlled radio aircraft demonstrating applied flight dynamics, trim control, and manual override systems.</div>
    </div>
    <div class="project-card reveal">
      <div class="project-icon">🚀</div>
      <div class="project-name">Hybrid Propulsion Rocket</div>
      <div class="project-desc">Lab-tested hybrid rocket using sugar-based propellant — exploring low-cost, accessible propulsion alternatives.</div>
    </div>
    <div class="project-card reveal">
      <div class="project-icon">🔭</div>
      <div class="project-name">Sounding Rocket + 3D Drone</div>
      <div class="project-desc">Built for experimental launches and atmospheric monitoring. Integrating telemetry with real-time position tracking.</div>
    </div>
    <div class="project-card reveal">
      <div class="project-icon">🐉</div>
      <div class="project-name">AeroHack 2023 — Drone Tracker</div>
      <div class="project-desc">Live drone mission tracking interface built with Python + open-source APIs. Finalist project at 48-hr hackathon.</div>
    </div>
  </div>
</section>

<div class="full-divider"></div>

<!-- SKILLS -->
<section id="skills">
  <p class="section-label reveal">Capabilities</p>
  <h2 class="section-title reveal">Skills</h2>
  <p class="section-jp reveal">スキル — Sukiru</p>

  <div class="skills-layout">
    <div>
      <p class="skill-group-title reveal">Technical Stack</p>
      <div class="skill-tags reveal">
        <span class="skill-tag">ANSYS Fluent (CFD)</span>
        <span class="skill-tag">SolidEdge</span>
        <span class="skill-tag">Fusion 360</span>
        <span class="skill-tag">SolidWorks</span>
        <span class="skill-tag">Python</span>
        <span class="skill-tag">Arduino</span>
        <span class="skill-tag">OpenVSP</span>
        <span class="skill-tag">UAV Design</span>
        <span class="skill-tag">Engine Health Monitoring</span>
        <span class="skill-tag">AI Prompt Engineering</span>
        <span class="skill-tag">MS Excel</span>
        <span class="skill-tag">Google Workspace</span>
        <span class="skill-tag">Framer</span>
        <span class="skill-tag">Canva</span>
        <span class="skill-tag">GIS / Satellite</span>
        <span class="skill-tag">Google IoT Core</span>
      </div>
    </div>
    <div>
      <p class="skill-group-title reveal">Soft Skills & Languages</p>
      <ul class="soft-list reveal">
        <li>Problem-Solving & Analytical Thinking</li>
        <li>Team Collaboration & Project Management</li>
        <li>Technical Report Writing</li>
        <li>Effective Communication</li>
        <li>English · Hindi · Telugu · Kannada</li>
        <li>Japanese — N5 Level</li>
      </ul>
    </div>
  </div>
</section>

<div class="full-divider"></div>

<!-- CERTIFICATIONS -->
<section id="certifications">
  <p class="section-label reveal">Credentials</p>
  <h2 class="section-title reveal">Certifications</h2>
  <p class="section-jp reveal">資格 — Shikaku</p>

  <div class="cert-grid">
    <div class="cert-card reveal"><div class="cert-name">Science of the Solar System</div><div class="cert-issuer">Caltech</div></div>
    <div class="cert-card reveal"><div class="cert-name">From the Big Bang to Dark Energy</div><div class="cert-issuer">University of Tokyo</div></div>
    <div class="cert-card reveal"><div class="cert-name">Introduction to Engineering Mechanics</div><div class="cert-issuer">Georgia Tech</div></div>
    <div class="cert-card reveal"><div class="cert-name">Programming for Everybody (Python)</div><div class="cert-issuer">Yale University</div></div>
    <div class="cert-card reveal"><div class="cert-name">Geospatial & GIS Satellite-Based Disaster Management</div><div class="cert-issuer">ISRO (IIRS)</div></div>
    <div class="cert-card reveal"><div class="cert-name">Arduino Training (Intermediate)</div><div class="cert-issuer">Skill Lync</div></div>
    <div class="cert-card reveal"><div class="cert-name">Learning Google IoT Core</div><div class="cert-issuer">Google</div></div>
    <div class="cert-card reveal"><div class="cert-name">Cert Prep 107 Drone License</div><div class="cert-issuer">LinkedIn Learning</div></div>
    <div class="cert-card reveal"><div class="cert-name">Digital Marketing</div><div class="cert-issuer">Google</div></div>
    <div class="cert-card reveal"><div class="cert-name">Applied Computational Fluid Dynamics</div><div class="cert-issuer">Siemens</div></div>
  </div>
</section>

<div class="full-divider"></div>

<!-- ACTIVITIES -->
<section id="activities">
  <p class="section-label reveal">Beyond Engineering</p>
  <h2 class="section-title reveal">Co-Curricular</h2>
  <p class="section-jp reveal">課外活動 — Kagai Katsudo</p>

  <div class="activities-grid">
    <div class="activity-card reveal">
      <span class="activity-badge">Research</span>
      <div class="activity-title">Research Assistant — Kalpana Chawla Lab</div>
      <div class="activity-desc">Literature review and design research for alternative propulsion systems; contributed to technical briefings and lab presentations.</div>
    </div>
    <div class="activity-card reveal">
      <span class="activity-badge">Hackathon</span>
      <div class="activity-title">Finalist — AeroHack 2023</div>
      <div class="activity-desc">Co-developed a live drone mission tracking interface using Python + open-source APIs. Presented to aerospace mentors and industry professionals.</div>
    </div>
    <div class="activity-card reveal">
      <span class="activity-badge">Leadership</span>
      <div class="activity-title">Best Delegate — IIMUN × UNOOSA</div>
      <div class="activity-desc">Represented Japan. Debated space traffic management and orbital debris. Co-drafted resolutions aligned with Artemis Accords and COPUOS.</div>
    </div>
    <div class="activity-card reveal">
      <span class="activity-badge">Community</span>
      <div class="activity-title">Chief Editor — Astronomy Club, CU</div>
      <div class="activity-desc">Organized telescope nights, NASA webinar streams, World Space Week activities, and wrote beginner-friendly guides on aerospace tools.</div>
    </div>
    <div class="activity-card reveal">
      <span class="activity-badge">Art & Voice</span>
      <div class="activity-title">Open Mic — LGBTQ+ Voices</div>
      <div class="activity-desc">Performed original poetry on queer joy, identity, and healing. Featured in a local queer-positive podcast amplifying underrepresented voices.</div>
    </div>
    <div class="activity-card reveal">
      <span class="activity-badge">Design</span>
      <div class="activity-title">No-Code UX/UI Design</div>
      <div class="activity-desc">Amateur programmer and UI designer using Framer and Canva. Also an aviation and astrophotographer.</div>
    </div>
  </div>
</section>

<div class="full-divider"></div>

<!-- CONTACT -->
<section id="contact">
  <p class="section-label" style="justify-content:center; margin-bottom:0.6rem;">
    <span>Let's Connect</span>
  </p>
  <h2 class="section-title reveal" style="text-align:center;">Get In Touch</h2>
  <p class="section-jp reveal" style="text-align:center;">連絡先 — Renrakusaki</p>
  <p class="reveal" style="text-align:center; color:var(--fog); max-width:480px; margin:0 auto 0; font-size:0.92rem; line-height:1.8;">
    Open to opportunities in aerospace reliability, UAV systems, robotics, and AI-integrated aviation. Let's build something that flies.
  </p>
  <div class="contact-links">
    <a href="mailto:giamokshagundam@gmail.com" class="contact-item reveal">
      <span class="contact-icon">✉️</span>
      <span class="contact-label">Email</span>
      <span class="contact-value">giamokshagundam@gmail.com</span>
    </a>
    <a href="https://www.linkedin.com/in/giamokshagundam-849030111" target="_blank" class="contact-item reveal">
      <span class="contact-icon">💼</span>
      <span class="contact-label">LinkedIn</span>
      <span class="contact-value">giamokshagundam</span>
    </a>
    <a href="tel:+917842683056" class="contact-item reveal">
      <span class="contact-icon">📱</span>
      <span class="contact-label">Phone</span>
      <span class="contact-value">+91 78426 83056</span>
    </a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="jp-credit">空は限界ではなく、出発点だ</div>
  <div>The sky is not the limit — it's the starting point. © 2025 Gia Mokshagundam</div>
</footer>

<script>
// ─────────────────────────────────────────────
// BACKGROUND — Stars + Sakura Particles
// ─────────────────────────────────────────────
const bgCanvas = document.getElementById('bg-canvas');
const bgCtx = bgCanvas.getContext('2d');

function resizeBg() {
  bgCanvas.width = window.innerWidth;
  bgCanvas.height = window.innerHeight;
}
resizeBg();
window.addEventListener('resize', resizeBg);

const stars = Array.from({length: 200}, () => ({
  x: Math.random() * window.innerWidth,
  y: Math.random() * window.innerHeight,
  r: Math.random() * 1.2,
  a: Math.random(),
  speed: 0.002 + Math.random() * 0.004
}));

const petals = Array.from({length: 18}, () => ({
  x: Math.random() * window.innerWidth,
  y: Math.random() * window.innerHeight,
  r: 3 + Math.random() * 4,
  vx: -0.3 - Math.random() * 0.5,
  vy: 0.4 + Math.random() * 0.6,
  rot: Math.random() * Math.PI * 2,
  rotSpeed: (Math.random() - 0.5) * 0.04,
  a: 0.3 + Math.random() * 0.5
}));

function drawPetal(ctx, x, y, r, rot, a) {
  ctx.save();
  ctx.translate(x, y);
  ctx.rotate(rot);
  ctx.globalAlpha = a;
  ctx.fillStyle = '#f4a8c7';
  ctx.beginPath();
  ctx.ellipse(0, 0, r, r * 2, 0, 0, Math.PI * 2);
  ctx.fill();
  ctx.restore();
}

let bgT = 0;
function animateBg() {
  bgCtx.clearRect(0, 0, bgCanvas.width, bgCanvas.height);
  bgT += 0.01;

  // Stars
  stars.forEach(s => {
    s.a = 0.3 + 0.5 * Math.abs(Math.sin(bgT * s.speed * 100));
    bgCtx.globalAlpha = s.a;
    bgCtx.fillStyle = '#b8b8d4';
    bgCtx.beginPath();
    bgCtx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    bgCtx.fill();
  });

  // Sakura petals
  petals.forEach(p => {
    drawPetal(bgCtx, p.x, p.y, p.r, p.rot, p.a);
    p.x += p.vx;
    p.y += p.vy;
    p.rot += p.rotSpeed;
    if (p.x < -20) p.x = bgCanvas.width + 20;
    if (p.y > bgCanvas.height + 20) { p.y = -20; p.x = Math.random() * bgCanvas.width; }
  });

  bgCtx.globalAlpha = 1;
  requestAnimationFrame(animateBg);
}
animateBg();

// ─────────────────────────────────────────────
// TURBINE ENGINE — Hero Animation
// ─────────────────────────────────────────────
const tc = document.getElementById('turbine-canvas');
const tx = tc.getContext('2d');
let turbineAngle = 0;

function drawTurbine() {
  const W = tc.width, H = tc.height;
  const cx = W / 2, cy = H / 2;
  tx.clearRect(0, 0, W, H);

  // Glow
  const grd = tx.createRadialGradient(cx, cy, 40, cx, cy, 200);
  grd.addColorStop(0, 'rgba(74,158,255,0.08)');
  grd.addColorStop(1, 'transparent');
  tx.fillStyle = grd;
  tx.fillRect(0, 0, W, H);

  // Outer ring
  tx.save();
  tx.strokeStyle = 'rgba(74,158,255,0.25)';
  tx.lineWidth = 1;
  tx.beginPath();
  tx.arc(cx, cy, 180, 0, Math.PI * 2);
  tx.stroke();
  tx.restore();

  // Middle ring
  tx.save();
  tx.strokeStyle = 'rgba(74,158,255,0.15)';
  tx.lineWidth = 1;
  tx.beginPath();
  tx.arc(cx, cy, 130, 0, Math.PI * 2);
  tx.stroke();
  tx.restore();

  // Rotating blades — outer fan
  const BLADES = 12;
  tx.save();
  tx.translate(cx, cy);
  tx.rotate(turbineAngle);
  for (let i = 0; i < BLADES; i++) {
    const angle = (i / BLADES) * Math.PI * 2;
    tx.save();
    tx.rotate(angle);
    const grad = tx.createLinearGradient(0, -185, 0, -95);
    grad.addColorStop(0, 'rgba(74,158,255,0.7)');
    grad.addColorStop(1, 'rgba(74,158,255,0.05)');
    tx.fillStyle = grad;
    tx.strokeStyle = 'rgba(74,158,255,0.4)';
    tx.lineWidth = 0.5;
    tx.beginPath();
    tx.moveTo(-5, -95);
    tx.quadraticCurveTo(-12, -140, -3, -182);
    tx.quadraticCurveTo(0, -188, 3, -182);
    tx.quadraticCurveTo(12, -140, 5, -95);
    tx.closePath();
    tx.fill();
    tx.stroke();
    tx.restore();
  }
  tx.restore();

  // Inner fan — counter-rotating
  const INNER = 8;
  tx.save();
  tx.translate(cx, cy);
  tx.rotate(-turbineAngle * 1.3);
  for (let i = 0; i < INNER; i++) {
    const angle = (i / INNER) * Math.PI * 2;
    tx.save();
    tx.rotate(angle);
    const grad2 = tx.createLinearGradient(0, -128, 0, -55);
    grad2.addColorStop(0, 'rgba(157,137,255,0.65)');
    grad2.addColorStop(1, 'rgba(157,137,255,0.05)');
    tx.fillStyle = grad2;
    tx.strokeStyle = 'rgba(157,137,255,0.35)';
    tx.lineWidth = 0.5;
    tx.beginPath();
    tx.moveTo(-4, -55);
    tx.quadraticCurveTo(-9, -90, -2, -125);
    tx.quadraticCurveTo(0, -130, 2, -125);
    tx.quadraticCurveTo(9, -90, 4, -55);
    tx.closePath();
    tx.fill();
    tx.stroke();
    tx.restore();
  }
  tx.restore();

  // Center hub
  tx.save();
  const hubGrad = tx.createRadialGradient(cx, cy, 2, cx, cy, 45);
  hubGrad.addColorStop(0, 'rgba(168,216,244,0.9)');
  hubGrad.addColorStop(0.5, 'rgba(74,158,255,0.5)');
  hubGrad.addColorStop(1, 'rgba(74,158,255,0.05)');
  tx.fillStyle = hubGrad;
  tx.beginPath();
  tx.arc(cx, cy, 45, 0, Math.PI * 2);
  tx.fill();

  // Hub ring
  tx.strokeStyle = 'rgba(168,216,244,0.5)';
  tx.lineWidth = 1.5;
  tx.beginPath();
  tx.arc(cx, cy, 45, 0, Math.PI * 2);
  tx.stroke();

  // Center dot
  tx.fillStyle = 'rgba(240,240,250,0.9)';
  tx.beginPath();
  tx.arc(cx, cy, 6, 0, Math.PI * 2);
  tx.fill();
  tx.restore();

  // Exhaust shimmer
  const exhaust = tx.createLinearGradient(cx - 10, cy + 180, cx + 10, cy + 210);
  exhaust.addColorStop(0, 'rgba(74,158,255,0.3)');
  exhaust.addColorStop(1, 'transparent');
  tx.save();
  tx.fillStyle = exhaust;
  const shimmer = Math.sin(turbineAngle * 5) * 3;
  tx.beginPath();
  tx.ellipse(cx, cy + 195, 8 + shimmer, 18, 0, 0, Math.PI * 2);
  tx.fill();
  tx.restore();

  turbineAngle += 0.018;
  requestAnimationFrame(drawTurbine);
}
drawTurbine();

// ─────────────────────────────────────────────
// JELLYFISH — About Section
// ─────────────────────────────────────────────
const jc = document.getElementById('jellyfish-canvas');
const jx = jc.getContext('2d');
let jT = 0;

function drawJellyfish() {
  const W = jc.width, H = jc.height;
  jx.clearRect(0, 0, W, H);

  // Background gradient
  const bg = jx.createLinearGradient(0, 0, 0, H);
  bg.addColorStop(0, 'rgba(6,6,16,0.95)');
  bg.addColorStop(1, 'rgba(13,13,31,0.95)');
  jx.fillStyle = bg;
  jx.fillRect(0, 0, W, H);

  // Floating particles
  for (let i = 0; i < 20; i++) {
    const px = (Math.sin(jT * 0.3 + i * 2.1) * 0.5 + 0.5) * W;
    const py = (((jT * 0.15 + i * 0.5) % 1)) * H;
    jx.globalAlpha = 0.15 + 0.1 * Math.sin(jT + i);
    jx.fillStyle = '#7b68ee';
    jx.beginPath();
    jx.arc(px, py, 1.2, 0, Math.PI * 2);
    jx.fill();
  }
  jx.globalAlpha = 1;

  // Multiple jellyfish
  const jellies = [
    { x: 160, y: 120 + Math.sin(jT * 0.7) * 20, scale: 1, alpha: 1 },
    { x: 70, y: 280 + Math.sin(jT * 0.5 + 1) * 15, scale: 0.55, alpha: 0.6 },
    { x: 255, y: 320 + Math.sin(jT * 0.6 + 2) * 12, scale: 0.4, alpha: 0.45 },
  ];

  jellies.forEach(j => drawSingleJelly(j.x, j.y, j.scale, j.alpha));

  jT += 0.015;
  requestAnimationFrame(drawJellyfish);
}

function drawSingleJelly(cx, cy, scale, alpha) {
  const s = scale;
  jx.save();
  jx.globalAlpha = alpha;

  // Bell body
  const bellPulse = 0.92 + 0.08 * Math.sin(jT * 2);
  const bw = 60 * s * bellPulse;
  const bh = 45 * s * bellPulse;

  const bellGrad = jx.createRadialGradient(cx, cy, 2 * s, cx, cy, bw);
  bellGrad.addColorStop(0, `rgba(180,160,255,${0.9 * alpha})`);
  bellGrad.addColorStop(0.5, `rgba(123,104,238,${0.6 * alpha})`);
  bellGrad.addColorStop(1, `rgba(74,50,180,${0.1 * alpha})`);

  jx.fillStyle = bellGrad;
  jx.beginPath();
  jx.ellipse(cx, cy - bh * 0.1, bw, bh, 0, Math.PI, Math.PI * 2);
  jx.fill();

  // Bell rim glow
  jx.strokeStyle = `rgba(200,180,255,${0.5 * alpha})`;
  jx.lineWidth = 1 * s;
  jx.beginPath();
  jx.ellipse(cx, cy - bh * 0.1, bw, bh, 0, Math.PI, Math.PI * 2);
  jx.stroke();

  // Tentacles
  const tentCount = 8;
  for (let t = 0; t < tentCount; t++) {
    const tx2 = cx + (t - tentCount / 2 + 0.5) * (bw * 2 / tentCount);
    const tentWave = Math.sin(jT * 1.5 + t * 0.8) * 12 * s;
    const tentLen = (50 + Math.random() * 0 + t % 3 * 15) * s;
    const opacity = 0.3 + 0.2 * Math.sin(jT + t);

    jx.strokeStyle = `rgba(180,150,255,${opacity * alpha})`;
    jx.lineWidth = (1.2 - t * 0.05) * s;
    jx.beginPath();
    jx.moveTo(tx2, cy + bh * 0.8);
    jx.quadraticCurveTo(
      tx2 + tentWave, cy + bh * 0.8 + tentLen * 0.5,
      tx2 + tentWave * 1.5, cy + bh * 0.8 + tentLen
    );
    jx.stroke();
  }

  // Inner organs glow
  const orgGrad = jx.createRadialGradient(cx, cy - bh * 0.3, 0, cx, cy - bh * 0.3, 20 * s);
  orgGrad.addColorStop(0, `rgba(220,200,255,${0.4 * alpha})`);
  orgGrad.addColorStop(1, 'transparent');
  jx.fillStyle = orgGrad;
  jx.beginPath();
  jx.arc(cx, cy - bh * 0.3, 20 * s, 0, Math.PI * 2);
  jx.fill();

  jx.restore();
}

drawJellyfish();

// ─────────────────────────────────────────────
// SCROLL REVEAL
// ─────────────────────────────────────────────
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver((entries) => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 80);
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>
