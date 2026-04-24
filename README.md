<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Brian Barrios | Dev & Redes</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #0a0a0f;
      --surface: #111118;
      --card: #16161f;
      --border: #1e1e2e;
      --accent: #00e5c0;
      --accent2: #7c5cfc;
      --text: #e8e8f0;
      --muted: #6b6b88;
      --mono: 'Space Mono', monospace;
      --sans: 'Syne', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--sans);
      overflow-x: hidden;
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none; z-index: 0; opacity: .45;
    }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.2rem 3rem;
      background: rgba(10,10,15,.85);
      backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border);
    }
    .nav-logo {
      font-family: var(--mono);
      font-size: .85rem;
      color: var(--accent);
      letter-spacing: .1em;
    }
    .nav-links { display: flex; gap: 2rem; list-style: none; }
    .nav-links a {
      font-family: var(--mono);
      font-size: .78rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: .08em;
      transition: color .2s;
    }
    .nav-links a:hover { color: var(--accent); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      padding: 8rem 3rem 4rem;
      gap: 4rem;
      position: relative;
    }
    .hero-glow {
      position: absolute;
      width: 600px; height: 600px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(0,229,192,.08) 0%, transparent 70%);
      top: 50%; right: -100px;
      transform: translateY(-50%);
      pointer-events: none;
    }
    .hero-tag {
      display: inline-block;
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--accent);
      letter-spacing: .15em;
      background: rgba(0,229,192,.08);
      border: 1px solid rgba(0,229,192,.2);
      padding: .35rem .9rem;
      border-radius: 2px;
      margin-bottom: 1.5rem;
    }
    .hero-name {
      font-family: var(--sans);
      font-weight: 800;
      font-size: clamp(3rem, 5vw, 5rem);
      line-height: .95;
      letter-spacing: -.02em;
      margin-bottom: 1.5rem;
    }
    .hero-name span { color: var(--accent); }
    .hero-desc {
      font-size: 1.05rem;
      color: var(--muted);
      line-height: 1.75;
      max-width: 480px;
      margin-bottom: 2.5rem;
    }
    .btn-row { display: flex; gap: 1rem; flex-wrap: wrap; }
    .btn {
      display: inline-block;
      padding: .8rem 2rem;
      font-family: var(--mono);
      font-size: .82rem;
      letter-spacing: .08em;
      text-decoration: none;
      border-radius: 3px;
      transition: all .2s;
      cursor: pointer;
    }
    .btn-primary {
      background: var(--accent);
      color: #0a0a0f;
      font-weight: 700;
    }
    .btn-primary:hover { background: #00ffd5; transform: translateY(-2px); }
    .btn-outline {
      border: 1px solid var(--border);
      color: var(--text);
      background: transparent;
    }
    .btn-outline:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

    /* Hero right: stats */
    .hero-stats {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
    }
    .stat-card {
      background: var(--card);
      border: 1px solid var(--border);
      padding: 1.75rem 1.5rem;
      border-radius: 4px;
      position: relative;
      overflow: hidden;
    }
    .stat-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
    }
    .stat-num {
      font-family: var(--mono);
      font-size: 2.2rem;
      font-weight: 700;
      color: var(--accent);
      display: block;
    }
    .stat-label {
      font-size: .82rem;
      color: var(--muted);
      margin-top: .25rem;
    }

    /* ── SECTIONS COMMON ── */
    section { padding: 6rem 3rem; position: relative; }
    .section-label {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--accent);
      letter-spacing: .2em;
      text-transform: uppercase;
      margin-bottom: .75rem;
    }
    .section-title {
      font-size: clamp(2rem, 3.5vw, 3rem);
      font-weight: 800;
      line-height: 1.1;
      margin-bottom: 3rem;
    }
    .divider {
      height: 1px;
      background: linear-gradient(90deg, var(--accent), transparent);
      opacity: .25;
      margin-bottom: 3rem;
      width: 80px;
    }

    /* ── SOBRE MÍ ── */
    #sobre {
      background: var(--surface);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
    }
    .sobre-grid {
      display: grid;
      grid-template-columns: 1.2fr 1fr;
      gap: 5rem;
      align-items: start;
    }
    .sobre-text p {
      color: var(--muted);
      line-height: 1.8;
      font-size: 1rem;
      margin-bottom: 1.25rem;
    }
    .skills-block { margin-top: 2rem; }
    .skills-category {
      margin-bottom: 1.75rem;
    }
    .skills-category h4 {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--accent);
      letter-spacing: .15em;
      margin-bottom: .75rem;
    }
    .skill-tags { display: flex; flex-wrap: wrap; gap: .5rem; }
    .tag {
      font-family: var(--mono);
      font-size: .75rem;
      padding: .3rem .75rem;
      border: 1px solid var(--border);
      border-radius: 2px;
      color: var(--text);
      background: var(--card);
      transition: border-color .2s, color .2s;
    }
    .tag:hover { border-color: var(--accent); color: var(--accent); }

    /* ── PROYECTOS ── */
    #proyectos { background: var(--bg); }
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 1.5rem;
    }
    .project-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: 2rem;
      position: relative;
      overflow: hidden;
      transition: border-color .25s, transform .25s;
    }
    .project-card:hover {
      border-color: var(--accent);
      transform: translateY(-4px);
    }
    .project-card::after {
      content: '';
      position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      transform: scaleX(0);
      transform-origin: left;
      transition: transform .3s;
    }
    .project-card:hover::after { transform: scaleX(1); }
    .project-icon {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }
    .project-title {
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: .5rem;
    }
    .project-desc {
      font-size: .88rem;
      color: var(--muted);
      line-height: 1.65;
      margin-bottom: 1.25rem;
    }
    .project-stack { display: flex; flex-wrap: wrap; gap: .4rem; }
    .stack-badge {
      font-family: var(--mono);
      font-size: .68rem;
      padding: .2rem .55rem;
      background: rgba(0,229,192,.07);
      border: 1px solid rgba(0,229,192,.15);
      color: var(--accent);
      border-radius: 2px;
    }

    /* ── SERVICIOS ── */
    #servicios {
      background: var(--surface);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
    }
    .services-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1.5rem;
    }
    .service-card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 4px;
      padding: 2rem;
      transition: border-color .25s;
    }
    .service-card:hover { border-color: var(--accent2); }
    .service-header {
      display: flex; align-items: center; gap: 1rem;
      margin-bottom: 1rem;
    }
    .service-icon {
      width: 42px; height: 42px;
      background: rgba(124,92,252,.1);
      border: 1px solid rgba(124,92,252,.2);
      border-radius: 8px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.2rem;
    }
    .service-name { font-size: 1rem; font-weight: 700; }
    .service-desc {
      font-size: .88rem;
      color: var(--muted);
      line-height: 1.65;
      margin-bottom: 1.5rem;
    }
    .service-price {
      font-family: var(--mono);
      font-size: .82rem;
      color: var(--accent);
      border-top: 1px solid var(--border);
      padding-top: 1rem;
    }
    .service-price strong {
      font-size: 1.4rem;
      display: block;
      margin-bottom: .15rem;
    }

    /* ── CONTACTO ── */
    #contacto { background: var(--bg); }
    .contact-wrap {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }
    .contact-info p {
      color: var(--muted);
      line-height: 1.75;
      margin-bottom: 2rem;
    }
    .contact-links { display: flex; flex-direction: column; gap: .75rem; }
    .contact-link {
      display: flex; align-items: center; gap: .9rem;
      font-family: var(--mono);
      font-size: .82rem;
      color: var(--muted);
      text-decoration: none;
      padding: .9rem 1rem;
      border: 1px solid var(--border);
      border-radius: 3px;
      transition: all .2s;
    }
    .contact-link:hover {
      border-color: var(--accent);
      color: var(--accent);
      background: rgba(0,229,192,.04);
    }
    .contact-link span { font-size: 1.1rem; }

    /* Form */
    .contact-form { display: flex; flex-direction: column; gap: 1rem; }
    .form-group { display: flex; flex-direction: column; gap: .4rem; }
    .form-group label {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--muted);
      letter-spacing: .1em;
    }
    .form-group input,
    .form-group textarea {
      background: var(--card);
      border: 1px solid var(--border);
      color: var(--text);
      font-family: var(--sans);
      font-size: .92rem;
      padding: .85rem 1rem;
      border-radius: 3px;
      outline: none;
      transition: border-color .2s;
    }
    .form-group input:focus,
    .form-group textarea:focus { border-color: var(--accent); }
    .form-group textarea { min-height: 130px; resize: vertical; }
    .form-submit {
      background: var(--accent);
      color: #0a0a0f;
      font-family: var(--mono);
      font-weight: 700;
      font-size: .82rem;
      letter-spacing: .1em;
      padding: .9rem;
      border: none;
      border-radius: 3px;
      cursor: pointer;
      transition: background .2s, transform .2s;
    }
    .form-submit:hover { background: #00ffd5; transform: translateY(-2px); }

    /* ── FOOTER ── */
    footer {
      padding: 2rem 3rem;
      border-top: 1px solid var(--border);
      display: flex; align-items: center; justify-content: space-between;
      background: var(--surface);
    }
    footer p {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--muted);
    }
    footer a { color: var(--accent); text-decoration: none; }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    .fade-up { animation: fadeUp .7s ease forwards; }
    .delay-1 { animation-delay: .1s; opacity: 0; }
    .delay-2 { animation-delay: .25s; opacity: 0; }
    .delay-3 { animation-delay: .4s; opacity: 0; }
    .delay-4 { animation-delay: .55s; opacity: 0; }

    /* ── RESPONSIVE ── */
    @media (max-width: 860px) {
      nav { padding: 1rem 1.5rem; }
      .nav-links { display: none; }
      #hero { grid-template-columns: 1fr; padding: 7rem 1.5rem 3rem; gap: 3rem; }
      .hero-stats { grid-template-columns: 1fr 1fr; }
      section { padding: 4rem 1.5rem; }
      .sobre-grid, .contact-wrap { grid-template-columns: 1fr; gap: 3rem; }
      footer { flex-direction: column; gap: .5rem; text-align: center; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">BB.dev</div>
  <ul class="nav-links">
    <li><a href="#sobre">Sobre mí</a></li>
    <li><a href="#proyectos">Proyectos</a></li>
    <li><a href="#servicios">Servicios</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div>
    <div class="hero-tag fade-up">// disponible para proyectos</div>
    <h1 class="hero-name fade-up delay-1">Brian<br><span>Barrios</span></h1>
    <p class="hero-desc fade-up delay-2">
      Analista en Sistemas & Técnico en Redes. Desarrollo webs, sistemas de gestión y soluciones IT para empresas y emprendedores. Basado en CABA, trabajo remoto y presencial.
    </p>
    <div class="btn-row fade-up delay-3">
      <a href="#contacto" class="btn btn-primary">Hablemos</a>
      <a href="#proyectos" class="btn btn-outline">Ver proyectos</a>
    </div>
  </div>
  <div class="hero-stats fade-up delay-4">
    <div class="stat-card">
      <span class="stat-num">7+</span>
      <span class="stat-label">Años en infraestructura</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">3+</span>
      <span class="stat-label">Proyectos de software</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">2</span>
      <span class="stat-label">Carreras universitarias</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">3</span>
      <span class="stat-label">Idiomas</span>
    </div>
  </div>
  <div class="hero-glow"></div>
</section>

<!-- SOBRE MÍ -->
<section id="sobre">
  <p class="section-label">01 — sobre mí</p>
  <h2 class="section-title">Desarrollo + Infraestructura.<br>Todo en uno.</h2>
  <div class="sobre-grid">
    <div class="sobre-text">
      <p>
        Soy Brian, Analista en Sistemas y Técnico en Redes egresado de la Universidad ISIPP. Me especializo en construir soluciones digitales completas: desde sitios web y sistemas de gestión hasta infraestructura de redes y soporte IT.
      </p>
      <p>
        Con más de 7 años gestionando redes Wi-Fi e infraestructura de forma independiente, y proyectos propios de software que incluyen sistemas para ISPs y plataformas de gestión de negocios, entiendo tanto el código como la red que lo sustenta.
      </p>
      <p>
        Busco sumarme a proyectos donde pueda aportar creatividad técnica y soluciones concretas que generen valor real.
      </p>
    </div>
    <div>
      <div class="skills-block">
        <div class="skills-category">
          <h4>// Web & Programación</h4>
          <div class="skill-tags">
            <span class="tag">HTML</span>
            <span class="tag">CSS</span>
            <span class="tag">JavaScript</span>
            <span class="tag">Python</span>
            <span class="tag">SQL</span>
            <span class="tag">Java</span>
          </div>
        </div>
        <div class="skills-category">
          <h4>// Redes & Sistemas</h4>
          <div class="skill-tags">
            <span class="tag">MikroTik RouterOS</span>
            <span class="tag">LAN / WAN</span>
            <span class="tag">VPN</span>
            <span class="tag">Ubuntu Linux</span>
            <span class="tag">Windows Server</span>
          </div>
        </div>
        <div class="skills-category">
          <h4>// Herramientas</h4>
          <div class="skill-tags">
            <span class="tag">VSCode</span>
            <span class="tag">Git / GitHub</span>
            <span class="tag">Excel</span>
            <span class="tag">Ansible</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROYECTOS -->
<section id="proyectos">
  <p class="section-label">02 — proyectos</p>
  <h2 class="section-title">Lo que construí.</h2>
  <div class="projects-grid">

    <div class="project-card">
      <div class="project-icon">🌐</div>
      <h3 class="project-title">Sistema de Gestión ISP</h3>
      <p class="project-desc">Panel de administración para proveedor de internet. Automatización de tareas de red, gestión de clientes y facturación. Reduce tiempo operativo hasta un 60%.</p>
      <div class="project-stack">
        <span class="stack-badge">Python</span>
        <span class="stack-badge">SQL</span>
        <span class="stack-badge">Visual Studio</span>
        <span class="stack-badge">Excel</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">🏪</div>
      <h3 class="project-title">Sistema de Administración de Negocios</h3>
      <p class="project-desc">Plataforma de gestión para pequeños comercios. Control de stock, ventas y clientes con base de datos local. Ideal para minimercados y negocios de barrio.</p>
      <div class="project-stack">
        <span class="stack-badge">Java</span>
        <span class="stack-badge">SQLite</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">📡</div>
      <h3 class="project-title">Infraestructura Wi-Fi Corporativa</h3>
      <p class="project-desc">Diseño e instalación de redes inalámbricas de largo alcance con equipos Ubiquiti y TpLink. Configuración de routers MikroTik cliente/servidor y cámaras IP.</p>
      <div class="project-stack">
        <span class="stack-badge">MikroTik</span>
        <span class="stack-badge">Ubiquiti</span>
        <span class="stack-badge">TpLink</span>
        <span class="stack-badge">DVR</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">💻</div>
      <h3 class="project-title">Desarrollo Web — Sitios a Medida</h3>
      <p class="project-desc">Diseño y desarrollo de sitios web para negocios locales. Responsive, rápidos y optimizados. Desde landing pages hasta portales con formularios y reservas.</p>
      <div class="project-stack">
        <span class="stack-badge">HTML</span>
        <span class="stack-badge">CSS</span>
        <span class="stack-badge">JavaScript</span>
      </div>
    </div>

  </div>
</section>

<!-- SERVICIOS -->
<section id="servicios">
  <p class="section-label">03 — servicios & precios</p>
  <h2 class="section-title">¿En qué puedo ayudarte?</h2>
  <div class="services-grid">

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">🖥️</div>
        <span class="service-name">Landing Page</span>
      </div>
      <p class="service-desc">Sitio de una página profesional para tu negocio o emprendimiento. Diseño responsive, formulario de contacto y entrega en 5-7 días.</p>
      <div class="service-price">
        <strong>desde $80.000 ARS</strong>
        entrega en 5–7 días hábiles
      </div>
    </div>

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">🌐</div>
        <span class="service-name">Sitio Web Completo</span>
      </div>
      <p class="service-desc">Multi-página con secciones personalizadas, galería, blog o tienda. Optimizado para móviles y motores de búsqueda.</p>
      <div class="service-price">
        <strong>desde $180.000 ARS</strong>
        entrega en 2–3 semanas
      </div>
    </div>

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">⚙️</div>
        <span class="service-name">Sistema de Gestión</span>
      </div>
      <p class="service-desc">Software a medida para tu negocio: stock, ventas, clientes o empleados. Desarrollado en Python o Java con base de datos local o en la nube.</p>
      <div class="service-price">
        <strong>desde $350.000 ARS</strong>
        según complejidad
      </div>
    </div>

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">📡</div>
        <span class="service-name">Redes & Soporte IT</span>
      </div>
      <p class="service-desc">Instalación y configuración de redes Wi-Fi, routers MikroTik, cámaras IP, servidores Linux/Windows y soporte técnico presencial o remoto.</p>
      <div class="service-price">
        <strong>desde $30.000 ARS</strong>
        visita técnica o por hora
      </div>
    </div>

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">📱</div>
        <span class="service-name">Web + Redes Sociales</span>
      </div>
      <p class="service-desc">Pack completo: diseño del sitio + gestión mensual de redes sociales. Presencia digital integral para PyMEs y emprendedores.</p>
      <div class="service-price">
        <strong>desde $120.000 ARS/mes</strong>
        contrato mensual
      </div>
    </div>

    <div class="service-card">
      <div class="service-header">
        <div class="service-icon">🔧</div>
        <span class="service-name">Mantenimiento Web</span>
      </div>
      <p class="service-desc">Actualizaciones, backups, seguridad y cambios de contenido para tu sitio ya existente. Sin sorpresas, con respuesta rápida.</p>
      <div class="service-price">
        <strong>desde $25.000 ARS/mes</strong>
        plan mensual
      </div>
    </div>

  </div>
</section>

<!-- CONTACTO -->
<section id="contacto">
  <p class="section-label">04 — contacto</p>
  <h2 class="section-title">Hablemos de tu proyecto.</h2>
  <div class="contact-wrap">
    <div class="contact-info">
      <p>¿Tenés una idea, un negocio que necesita presencia online, o un sistema que simplificar? Escribime y te respondo en menos de 24hs.</p>
      <div class="contact-links">
        <a href="mailto:bbarrios526@gmail.com" class="contact-link">
          <span>✉️</span> bbarrios526@gmail.com
        </a>
        <a href="https://wa.me/5493751365752" target="_blank" class="contact-link">
          <span>💬</span> +54 9 3751 365752 (WhatsApp)
        </a>
        <a href="https://github.com/BrianBarrios" target="_blank" class="contact-link">
          <span>🐙</span> github.com/BrianBarrios
        </a>
        <a href="https://www.linkedin.com/in/barrios-briann" target="_blank" class="contact-link">
          <span>💼</span> linkedin.com/in/barrios-briann
        </a>
      </div>
    </div>
    <form class="contact-form" onsubmit="handleSubmit(event)">
      <div class="form-group">
        <label>NOMBRE</label>
        <input type="text" id="nombre" placeholder="Tu nombre" required />
      </div>
      <div class="form-group">
        <label>EMAIL</label>
        <input type="email" id="email" placeholder="tu@email.com" required />
      </div>
      <div class="form-group">
        <label>MENSAJE</label>
        <textarea id="mensaje" placeholder="Contame sobre tu proyecto..." required></textarea>
      </div>
      <button type="submit" class="form-submit">ENVIAR MENSAJE →</button>
    </form>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p>© 2026 Brian Emanuel Barrios — Hecho con HTML, CSS & JS</p>
  <p><a href="mailto:bbarrios526@gmail.com">bbarrios526@gmail.com</a></p>
</footer>

<script>
  // Smooth reveal on scroll
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.style.opacity = '1';
        e.target.style.transform = 'translateY(0)';
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.project-card, .service-card, .stat-card').forEach(el => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(24px)';
    el.style.transition = 'opacity .5s ease, transform .5s ease';
    observer.observe(el);
  });

  // Form handler — abre WhatsApp con el mensaje
  function handleSubmit(e) {
    e.preventDefault();
    const nombre = document.getElementById('nombre').value;
    const email = document.getElementById('email').value;
    const mensaje = document.getElementById('mensaje').value;
    const texto = `Hola Brian! Soy ${nombre} (${email}). ${mensaje}`;
    window.open(`https://wa.me/5493751365752?text=${encodeURIComponent(texto)}`, '_blank');
  }
</script>

</body>
</html>