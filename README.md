<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tamweel Corporate Services Ltd – Tax, Accounting & Outsourcing | Mauritius</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700;900&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --navy:    #1A3A6B;
    --navy-dk: #0D2347;
    --teal:    #00B5B8;
    --teal-dk: #009A9C;
    --gold:    #D4A017;
    --gold-lt: #E8BC3A;
    --sky:     #4A90C4;
    --white:   #FFFFFF;
    --ivory:   #F6F9FC;
    --mid:     #D6E6F2;
    --ink:     #0D1B2A;
    --muted:   #5A6E82;
  }

  html { scroll-behavior: smooth; }
  body { font-family: 'Inter', sans-serif; background: var(--white); color: var(--ink); line-height: 1.6; }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 0 5%; height: 70px;
    background: rgba(13, 35, 71, 0.98);
    backdrop-filter: blur(10px);
    border-bottom: 2px solid var(--teal);
  }
  .nav-logo { display: flex; align-items: center; gap: 12px; text-decoration: none; }
  .logo-mark {
    width: 42px; height: 42px;
    background: var(--teal);
    display: flex; align-items: center; justify-content: center;
    position: relative;
  }
  .logo-mark svg { width: 26px; height: 26px; }
  .logo-text-wrap { display: flex; flex-direction: column; }
  .logo-name { font-weight: 700; font-size: 1rem; color: var(--white); letter-spacing: 0.08em; line-height: 1; }
  .logo-name span { color: var(--teal); }
  .logo-tagline { font-size: 0.58rem; color: rgba(255,255,255,0.45); letter-spacing: 0.07em; margin-top: 3px; }
  .nav-links { display: flex; gap: 30px; list-style: none; align-items: center; }
  .nav-links a {
    color: rgba(255,255,255,0.7); text-decoration: none;
    font-size: 0.78rem; letter-spacing: 0.1em; text-transform: uppercase; font-weight: 500;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--teal); }
  .nav-cta {
    background: var(--teal) !important; color: var(--white) !important;
    padding: 8px 20px; font-weight: 600 !important; transition: background 0.2s !important;
  }
  .nav-cta:hover { background: var(--teal-dk) !important; }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    background: linear-gradient(135deg, var(--navy-dk) 0%, var(--navy) 60%, #1E5080 100%);
    display: grid; grid-template-columns: 1fr 1fr;
    align-items: center;
    padding: 110px 5% 80px;
    position: relative; overflow: hidden;
    gap: 60px;
  }
  .hero-bg-shape {
    position: absolute; top: -80px; right: -80px;
    width: 500px; height: 500px;
    background: var(--teal); opacity: 0.06;
    border-radius: 50%;
    pointer-events: none;
  }
  .hero-bg-shape2 {
    position: absolute; bottom: -120px; left: 40%;
    width: 400px; height: 400px;
    background: var(--gold); opacity: 0.04;
    border-radius: 50%;
    pointer-events: none;
  }
  .hero-left { position: relative; z-index: 2; }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(0,181,184,0.12);
    border: 1px solid rgba(0,181,184,0.4);
    padding: 6px 16px; margin-bottom: 24px;
    font-size: 0.68rem; letter-spacing: 0.18em;
    text-transform: uppercase; color: var(--teal); font-weight: 700;
  }
  .badge-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--teal); animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.4} }
  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.2rem, 4vw, 3.4rem);
    color: var(--white); line-height: 1.1; font-weight: 900;
    margin-bottom: 6px;
  }
  .hero h1 em { color: var(--teal); font-style: normal; display: block; }
  .hero-sub-head {
    font-size: 0.85rem; color: rgba(255,255,255,0.45);
    letter-spacing: 0.1em; text-transform: uppercase;
    margin-bottom: 20px; padding-bottom: 20px;
    border-bottom: 1px solid rgba(0,181,184,0.25);
  }
  .hero-confidence {
    display: inline-block;
    font-size: 1.05rem; font-style: italic;
    color: var(--gold-lt); font-weight: 400;
    margin-bottom: 28px;
  }
  .hero-desc {
    font-size: 0.95rem; color: rgba(255,255,255,0.62);
    line-height: 1.8; font-weight: 300; margin-bottom: 36px;
  }
  .hero-values { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 36px; }
  .val-pill {
    border: 1px solid rgba(0,181,184,0.35);
    color: rgba(255,255,255,0.7);
    padding: 5px 14px; font-size: 0.75rem;
    letter-spacing: 0.06em; font-weight: 500;
  }
  .hero-btns { display: flex; gap: 14px; flex-wrap: wrap; }
  .btn-teal {
    background: var(--teal); color: var(--white);
    padding: 14px 30px; font-weight: 700; font-size: 0.8rem;
    letter-spacing: 0.1em; text-transform: uppercase;
    text-decoration: none; transition: background 0.2s, transform 0.15s;
    display: inline-block; border: none; cursor: pointer;
  }
  .btn-teal:hover { background: var(--teal-dk); transform: translateY(-1px); }
  .btn-ghost {
    border: 1.5px solid rgba(255,255,255,0.3); color: rgba(255,255,255,0.8);
    padding: 14px 30px; font-size: 0.8rem;
    letter-spacing: 0.1em; text-transform: uppercase;
    text-decoration: none; transition: border-color 0.2s, color 0.2s;
    display: inline-block;
  }
  .btn-ghost:hover { border-color: var(--teal); color: var(--teal); }

  /* hero right card */
  .hero-right { position: relative; z-index: 2; }
  .hero-card {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(0,181,184,0.2);
    backdrop-filter: blur(4px);
    padding: 36px 32px;
  }
  .hero-card-title {
    font-size: 0.68rem; letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--teal); font-weight: 700; margin-bottom: 20px;
    display: flex; align-items: center; gap: 10px;
  }
  .hero-card-title::after { content: ''; flex: 1; height: 1px; background: rgba(0,181,184,0.25); }
  .service-list { list-style: none; }
  .service-list li {
    display: flex; align-items: flex-start; gap: 12px;
    padding: 11px 0; border-bottom: 1px solid rgba(255,255,255,0.06);
    font-size: 0.9rem; color: rgba(255,255,255,0.75); font-weight: 400;
  }
  .service-list li:last-child { border-bottom: none; }
  .sli-check {
    width: 20px; height: 20px; border-radius: 50%;
    background: rgba(0,181,184,0.15); border: 1px solid var(--teal);
    display: flex; align-items: center; justify-content: center;
    color: var(--teal); font-size: 0.65rem; flex-shrink: 0; margin-top: 2px;
  }
  .hero-exp-bar {
    margin-top: 24px; padding-top: 24px;
    border-top: 1px solid rgba(0,181,184,0.2);
    display: flex; gap: 24px;
  }
  .exp-item { text-align: center; flex: 1; }
  .exp-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem; font-weight: 700;
    color: var(--gold-lt); display: block; line-height: 1;
  }
  .exp-lbl { font-size: 0.66rem; letter-spacing: 0.1em; text-transform: uppercase; color: rgba(255,255,255,0.38); margin-top: 5px; }

  /* ── WAVE ── */
  .wave-wrap { line-height: 0; background: var(--navy-dk); }
  .wave-wrap svg { display: block; }

  /* ── SERVICES SECTION ── */
  .services-section { padding: 90px 5%; background: var(--ivory); }
  .sec-header { margin-bottom: 56px; }
  .sec-label {
    font-size: 0.68rem; letter-spacing: 0.22em; text-transform: uppercase;
    color: var(--teal); font-weight: 700; margin-bottom: 10px;
  }
  .sec-h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.7rem, 3vw, 2.5rem);
    font-weight: 700; line-height: 1.2; color: var(--navy-dk);
    margin-bottom: 12px;
  }
  .sec-sub { font-size: 0.93rem; color: var(--muted); max-width: 520px; line-height: 1.7; }
  .services-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
  .svc-card {
    background: var(--white);
    border-left: 4px solid var(--teal);
    padding: 32px 26px 28px;
    transition: box-shadow 0.25s, transform 0.2s;
    position: relative; overflow: hidden;
  }
  .svc-card::after {
    content: ''; position: absolute;
    bottom: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(to right, var(--teal), var(--gold));
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.3s;
  }
  .svc-card:hover { box-shadow: 0 10px 32px rgba(26,58,107,0.13); transform: translateY(-3px); }
  .svc-card:hover::after { transform: scaleX(1); }
  .svc-tag {
    display: inline-block; background: var(--navy);
    color: var(--white); font-size: 0.65rem; font-weight: 700;
    letter-spacing: 0.14em; text-transform: uppercase;
    padding: 4px 12px; margin-bottom: 16px;
  }
  .svc-icon-wrap {
    width: 46px; height: 46px;
    background: rgba(0,181,184,0.08);
    border: 1px solid rgba(0,181,184,0.2);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem; margin-bottom: 16px;
  }
  .svc-title { font-weight: 700; font-size: 1rem; color: var(--navy-dk); margin-bottom: 10px; line-height: 1.3; }
  .svc-desc { font-size: 0.84rem; color: var(--muted); line-height: 1.75; }
  .svc-items { list-style: none; margin-top: 12px; }
  .svc-items li {
    font-size: 0.82rem; color: var(--muted);
    padding: 4px 0; padding-left: 16px;
    position: relative;
  }
  .svc-items li::before { content: '—'; position: absolute; left: 0; color: var(--teal); font-size: 0.7rem; }

  /* ── ABOUT STRIP ── */
  .about-strip {
    background: var(--navy);
    padding: 80px 5%;
    display: grid; grid-template-columns: 1fr 1fr; gap: 72px; align-items: center;
  }
  .about-left .sec-h2 { color: var(--white); }
  .about-left .sec-sub { color: rgba(255,255,255,0.52); max-width: 100%; }
  .about-quote {
    font-style: italic; font-size: 1.1rem;
    color: var(--teal); line-height: 1.65; margin-bottom: 24px;
    padding-left: 20px;
    border-left: 3px solid var(--teal);
  }
  .about-tags { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 28px; }
  .atag {
    border: 1px solid rgba(0,181,184,0.35);
    color: rgba(255,255,255,0.7);
    padding: 6px 16px; font-size: 0.78rem; font-weight: 500;
  }
  .about-right-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .astat {
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(0,181,184,0.18);
    padding: 28px 22px; text-align: center;
    transition: border-color 0.2s;
  }
  .astat:hover { border-color: var(--teal); }
  .astat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2rem; font-weight: 700;
    color: var(--teal); display: block; line-height: 1; margin-bottom: 8px;
  }
  .astat-lbl { font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; color: rgba(255,255,255,0.38); }
  .professional-badge {
    grid-column: span 2;
    background: linear-gradient(135deg, var(--teal-dk), var(--navy-dk));
    border: none; padding: 22px;
    font-style: italic; color: rgba(255,255,255,0.85);
    font-size: 0.88rem; line-height: 1.65; text-align: center;
  }
  .professional-badge strong { color: var(--gold-lt); font-style: normal; display: block; margin-bottom: 4px; font-size: 0.95rem; }

  /* ── WHY US ── */
  .why-section {
    padding: 90px 5%; background: var(--white);
    display: grid; grid-template-columns: 1fr 1fr; gap: 72px; align-items: start;
  }
  .why-left .sec-sub { max-width: 100%; margin-bottom: 32px; }
  .why-points { display: flex; flex-direction: column; gap: 20px; }
  .why-point {
    display: flex; gap: 16px; align-items: flex-start;
    padding: 20px 22px;
    border: 1px solid var(--mid);
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  .why-point:hover { border-color: var(--teal); box-shadow: 0 4px 16px rgba(0,181,184,0.08); }
  .why-icon {
    width: 44px; height: 44px; flex-shrink: 0;
    background: var(--navy); color: var(--teal);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.1rem;
  }
  .why-point-title { font-weight: 700; font-size: 0.9rem; color: var(--navy-dk); margin-bottom: 4px; }
  .why-point-desc { font-size: 0.83rem; color: var(--muted); line-height: 1.65; }
  .why-right {
    background: var(--teal);
    padding: 44px 38px;
  }
  .cta-card-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem; font-weight: 700;
    color: var(--white); margin-bottom: 10px; line-height: 1.2;
  }
  .cta-card-sub { font-size: 0.88rem; color: rgba(255,255,255,0.75); margin-bottom: 28px; line-height: 1.65; }
  .cta-phone {
    display: flex; align-items: center; gap: 12px;
    background: rgba(255,255,255,0.15);
    padding: 16px 20px; margin-bottom: 20px;
  }
  .cta-phone-icon { font-size: 1.4rem; }
  .cta-phone-num { font-size: 1.4rem; font-weight: 700; color: var(--white); }
  .cta-phone-lbl { font-size: 0.7rem; color: rgba(255,255,255,0.6); letter-spacing: 0.08em; text-transform: uppercase; }
  .cta-email-row {
    display: flex; align-items: center; gap: 10px;
    font-size: 0.88rem; color: rgba(255,255,255,0.8); margin-bottom: 28px;
  }
  .cta-email-row a { color: var(--white); font-weight: 600; text-decoration: none; }
  .cta-divider { height: 1px; background: rgba(255,255,255,0.2); margin: 24px 0; }
  .cta-addr { font-size: 0.85rem; color: rgba(255,255,255,0.7); line-height: 1.7; }
  .cta-addr strong { color: var(--white); display: block; margin-bottom: 4px; font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase; }
  .btn-white {
    display: block; text-align: center;
    background: var(--white); color: var(--teal-dk);
    padding: 14px; font-weight: 700; font-size: 0.82rem;
    letter-spacing: 0.1em; text-transform: uppercase;
    text-decoration: none; margin-top: 24px;
    transition: background 0.2s;
  }
  .btn-white:hover { background: rgba(255,255,255,0.88); }

  /* ── CONTACT FORM ── */
  .contact-section {
    padding: 90px 5%; background: var(--ivory);
    display: grid; grid-template-columns: 1.1fr 0.9fr; gap: 64px; align-items: start;
  }
  .contact-form-wrap {
    background: var(--white);
    border-top: 4px solid var(--teal);
    padding: 44px 38px;
    box-shadow: 0 4px 24px rgba(26,58,107,0.07);
  }
  .form-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem; font-weight: 700;
    color: var(--navy-dk); margin-bottom: 28px;
  }
  .form-group { margin-bottom: 18px; }
  .form-group label {
    display: block; font-size: 0.7rem;
    letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--muted); margin-bottom: 7px; font-weight: 600;
  }
  .form-group input,
  .form-group select,
  .form-group textarea {
    width: 100%; padding: 11px 15px;
    border: 1.5px solid var(--mid);
    background: var(--ivory);
    font-family: 'Inter', sans-serif; font-size: 0.9rem;
    color: var(--ink); outline: none; transition: border-color 0.2s; appearance: none;
  }
  .form-group input:focus,
  .form-group select:focus,
  .form-group textarea:focus { border-color: var(--teal); background: var(--white); }
  .form-group textarea { resize: vertical; min-height: 100px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .submit-btn {
    width: 100%; background: var(--navy); color: var(--white);
    border: none; padding: 15px;
    font-family: 'Inter', sans-serif; font-size: 0.8rem;
    letter-spacing: 0.14em; text-transform: uppercase; font-weight: 700;
    cursor: pointer; transition: background 0.2s; margin-top: 6px;
  }
  .submit-btn:hover { background: var(--teal); }
  .contact-info-side { padding-top: 4px; }
  .contact-info-side .sec-h2 { color: var(--navy-dk); margin-bottom: 10px; }
  .contact-info-side .sec-sub { margin-bottom: 36px; }
  .cdet { display: flex; align-items: flex-start; gap: 14px; margin-bottom: 20px; }
  .cdet-icon {
    width: 40px; height: 40px; flex-shrink: 0;
    background: var(--navy); color: var(--teal);
    display: flex; align-items: center; justify-content: center; font-size: 1rem;
  }
  .cdet-body strong {
    display: block; font-size: 0.68rem;
    letter-spacing: 0.12em; text-transform: uppercase; color: var(--muted); margin-bottom: 3px;
  }
  .cdet-body span { font-size: 0.9rem; color: var(--ink); line-height: 1.5; }
  .cdet-body a { color: var(--teal); text-decoration: none; }
  .cdet-body a:hover { text-decoration: underline; }
  .conf-badge {
    margin-top: 32px; padding: 18px 20px;
    background: var(--navy-dk); display: flex; gap: 12px; align-items: center;
  }
  .conf-icon { font-size: 1.4rem; flex-shrink: 0; }
  .conf-text strong { display: block; color: var(--teal); font-size: 0.82rem; font-weight: 700; margin-bottom: 3px; }
  .conf-text span { font-size: 0.78rem; color: rgba(255,255,255,0.5); }

  /* ── FOOTER ── */
  footer {
    background: var(--navy-dk);
    padding: 56px 5% 28px;
    border-top: 3px solid var(--teal);
  }
  .footer-top {
    display: grid; grid-template-columns: 1.5fr 1fr 1fr 1fr; gap: 40px;
    padding-bottom: 40px; border-bottom: 1px solid rgba(255,255,255,0.07); margin-bottom: 28px;
  }
  .footer-brand-name { font-weight: 700; font-size: 1.05rem; color: var(--white); letter-spacing: 0.06em; margin-bottom: 4px; }
  .footer-brand-name span { color: var(--teal); }
  .footer-brand-tag { font-size: 0.62rem; color: rgba(255,255,255,0.35); letter-spacing: 0.05em; margin-bottom: 14px; }
  .footer-brand p { font-size: 0.82rem; color: rgba(255,255,255,0.35); line-height: 1.75; }
  .footer-col-title { font-size: 0.66rem; letter-spacing: 0.18em; text-transform: uppercase; color: var(--teal); font-weight: 700; margin-bottom: 18px; }
  .footer-col ul { list-style: none; }
  .footer-col ul li { margin-bottom: 9px; }
  .footer-col ul li a { color: rgba(255,255,255,0.4); text-decoration: none; font-size: 0.83rem; transition: color 0.2s; }
  .footer-col ul li a:hover { color: var(--teal); }
  .footer-bottom {
    display: flex; justify-content: space-between; align-items: center;
    font-size: 0.74rem; color: rgba(255,255,255,0.22);
  }
  .footer-bottom a { color: rgba(255,255,255,0.3); text-decoration: none; }
  .footer-bottom a:hover { color: var(--teal); }

  /* ── RESPONSIVE ── */
  @media (max-width: 960px) {
    .nav-links { display: none; }
    .hero { grid-template-columns: 1fr; gap: 40px; padding-bottom: 60px; }
    .services-grid { grid-template-columns: 1fr 1fr; }
    .about-strip { grid-template-columns: 1fr; gap: 40px; }
    .why-section { grid-template-columns: 1fr; gap: 40px; }
    .contact-section { grid-template-columns: 1fr; gap: 40px; }
    .footer-top { grid-template-columns: 1fr 1fr; }
  }
  @media (max-width: 560px) {
    .services-grid { grid-template-columns: 1fr; }
    .form-row { grid-template-columns: 1fr; }
    .about-right-grid { grid-template-columns: 1fr 1fr; }
    .footer-top { grid-template-columns: 1fr; }
    .footer-bottom { flex-direction: column; gap: 8px; text-align: center; }
    .hero-exp-bar { flex-direction: column; gap: 16px; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="nav-logo" href="#">
    <div class="logo-mark">
      <svg viewBox="0 0 26 26" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="2" y="14" width="5" height="10" fill="white" opacity="0.9"/>
        <rect x="9" y="8" width="5" height="16" fill="white" opacity="0.9"/>
        <rect x="16" y="2" width="5" height="22" fill="white" opacity="0.9"/>
        <polyline points="2,15 9,9 16,3 21,3" stroke="white" stroke-width="1.5" fill="none" opacity="0.5"/>
      </svg>
    </div>
    <div class="logo-text-wrap">
      <span class="logo-name">TAMWEEL <span>CORPORATE</span></span>
      <span class="logo-tagline">Accounting · Tax · Outsourcing · Secretarial</span>
    </div>
  </a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#why">Why Us</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="tel:54991117" class="nav-cta">Call Now</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg-shape"></div>
  <div class="hero-bg-shape2"></div>

  <div class="hero-left">
    <div class="hero-badge"><span class="badge-dot"></span>Professional &amp; Confidential</div>
    <h1>Tamweel<br><em>Corporate Services</em></h1>
    <p class="hero-sub-head">Accounting &amp; Tax Systems &nbsp;|&nbsp; Outsourcing Solutions</p>
    <p class="hero-confidence">"Unmatched Tailor Made Solutions"</p>
    <p class="hero-desc">We are a team of professionals with wide experience in Practice and Industry, providing high quality services to individuals and businesses across Mauritius.</p>
    <div class="hero-values">
      <div class="val-pill">Professionalism</div>
      <div class="val-pill">Competency</div>
      <div class="val-pill">Integrity</div>
      <div class="val-pill">Commitment</div>
    </div>
    <div class="hero-btns">
      <a href="#services" class="btn-teal">Our Services</a>
      <a href="#contact" class="btn-ghost">Book a Consultation</a>
    </div>
  </div>

  <div class="hero-right">
    <div class="hero-card">
      <div class="hero-card-title">What We Provide</div>
      <ul class="service-list">
        <li><span class="sli-check">✓</span>Income Tax Preparation — Individual &amp; Business</li>
        <li><span class="sli-check">✓</span>Tax Returns &amp; Tax Planning</li>
        <li><span class="sli-check">✓</span>Payroll Services</li>
        <li><span class="sli-check">✓</span>Accounting &amp; Bookkeeping</li>
        <li><span class="sli-check">✓</span>Financial Reports</li>
        <li><span class="sli-check">✓</span>Budget Analyst &amp; Corporate Finance</li>
        <li><span class="sli-check">✓</span>Certified Internal Auditor Services</li>
        <li><span class="sli-check">✓</span>Company Formation &amp; Administration</li>
        <li><span class="sli-check">✓</span>Consultancy</li>
      </ul>
      <div class="hero-exp-bar">
        <div class="exp-item">
          <span class="exp-num">10+</span>
          <div class="exp-lbl">Years Experience</div>
        </div>
        <div class="exp-item">
          <span class="exp-num">5★</span>
          <div class="exp-lbl">Client Rated</div>
        </div>
        <div class="exp-item">
          <span class="exp-num">100%</span>
          <div class="exp-lbl">Confidential</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section class="services-section" id="services">
  <div class="sec-header">
    <div class="sec-label">Available Systems</div>
    <h2 class="sec-h2">Comprehensive Services for Individuals &amp; Businesses</h2>
    <p class="sec-sub">Tax &amp; consulting services tailored to meet the needs of both individuals and businesses — delivered with professionalism and confidentiality.</p>
  </div>

  <div class="services-grid">
    <div class="svc-card">
      <div class="svc-icon-wrap">🧾</div>
      <div class="svc-tag">Tax</div>
      <div class="svc-title">Tax Returns &amp; Planning</div>
      <p class="svc-desc">Personal and company tax preparation and strategic planning to minimise liability and ensure full compliance.</p>
      <ul class="svc-items">
        <li>Income Tax Preparation</li>
        <li>Individual &amp; Business Tax Returns</li>
        <li>VAT, PAYE &amp; TDS</li>
        <li>Tax Planning Strategies</li>
      </ul>
    </div>
    <div class="svc-card">
      <div class="svc-icon-wrap">📊</div>
      <div class="svc-tag">Accounting</div>
      <div class="svc-title">Accounting &amp; Bookkeeping</div>
      <p class="svc-desc">Accurate, timely financial records and reporting to keep your business informed and audit-ready at all times.</p>
      <ul class="svc-items">
        <li>Bookkeeping &amp; Financial Reporting</li>
        <li>Financial Reports</li>
        <li>Budget Analysis</li>
        <li>Certified Internal Auditing</li>
      </ul>
    </div>
    <div class="svc-card">
      <div class="svc-icon-wrap">⚙️</div>
      <div class="svc-tag">Outsourcing</div>
      <div class="svc-title">Payroll &amp; Business Process</div>
      <p class="svc-desc">Reliable payroll management and business process outsourcing so your team can stay focused on what matters most.</p>
      <ul class="svc-items">
        <li>Payroll Services</li>
        <li>Business Process Outsourcing</li>
        <li>PAYE Administration</li>
      </ul>
    </div>
    <div class="svc-card">
      <div class="svc-icon-wrap">💼</div>
      <div class="svc-tag">Advisory</div>
      <div class="svc-title">Business Plan &amp; Corporate Finance</div>
      <p class="svc-desc">Strategic advisory services to help you plan, grow, and navigate complex financial and corporate decisions.</p>
      <ul class="svc-items">
        <li>Business Plan &amp; Forecasting</li>
        <li>Business System Design</li>
        <li>Corporate Finance</li>
        <li>Consultancy</li>
      </ul>
    </div>
    <div class="svc-card">
      <div class="svc-icon-wrap">🏛️</div>
      <div class="svc-tag">Secretarial</div>
      <div class="svc-title">Company Formation &amp; Administration</div>
      <p class="svc-desc">End-to-end company registration and ongoing secretarial support to keep your corporate structure compliant.</p>
      <ul class="svc-items">
        <li>Company Formation</li>
        <li>Corporate Administration</li>
        <li>Statutory Compliance</li>
      </ul>
    </div>
    <div class="svc-card" style="background:var(--navy); border-left-color:var(--gold);">
      <div class="svc-icon-wrap" style="background:rgba(212,160,23,0.1); border-color:rgba(212,160,23,0.3);">⭐</div>
      <div class="svc-tag" style="background:var(--gold); color:var(--navy-dk);">Experience</div>
      <div class="svc-title" style="color:var(--white);">10 Years as an Income Tax &amp; Accounting Professional</div>
      <p class="svc-desc" style="color:rgba(255,255,255,0.55);">Our lead professional brings a decade of hands-on experience as an income tax and accounting specialist — providing the expertise your business deserves.</p>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section class="about-strip" id="about">
  <div class="about-left">
    <div class="sec-label">About Us</div>
    <h2 class="sec-h2" style="color:#fff;">Tamweel Corporate Services Ltd</h2>
    <p class="about-quote">"We are a team of professionals with wide experience in Practice and Industry providing high quality services to our clients."</p>
    <p class="sec-sub">Based in Quatre Bornes, Mauritius, Tamweel Corporate Services Ltd combines deep technical expertise across tax, accounting, and corporate services with a genuine commitment to client outcomes. Every solution is tailor-made — no templates, no one-size-fits-all.</p>
    <div class="about-tags">
      <div class="atag">Professionalism</div>
      <div class="atag">Competency</div>
      <div class="atag">Integrity</div>
      <div class="atag">Commitment</div>
    </div>
  </div>
  <div class="about-right-grid">
    <div class="astat">
      <span class="astat-num">10+</span>
      <div class="astat-lbl">Years Experience</div>
    </div>
    <div class="astat">
      <span class="astat-num">5</span>
      <div class="astat-lbl">Service Areas</div>
    </div>
    <div class="astat">
      <span class="astat-num">2</span>
      <div class="astat-lbl">Contact Emails</div>
    </div>
    <div class="astat">
      <span class="astat-num">MU</span>
      <div class="astat-lbl">Mauritius-Based</div>
    </div>
    <div class="professional-badge">
      <strong>Professional &amp; Confidential</strong>
      All client information and engagements are handled with the strictest professional confidentiality and discretion.
    </div>
  </div>
</section>

<!-- WHY US -->
<section class="why-section" id="why">
  <div class="why-left">
    <div class="sec-label">Why Choose Us</div>
    <h2 class="sec-h2">The Tamweel Difference</h2>
    <p class="sec-sub">We combine professional expertise, personal attention, and tailor-made solutions to deliver results that genuinely support your goals — for individuals and businesses alike.</p>
    <div class="why-points">
      <div class="why-point">
        <div class="why-icon">🎯</div>
        <div>
          <div class="why-point-title">Tailor-Made Solutions</div>
          <p class="why-point-desc">We take the time to understand each client's unique context and design a service plan specifically built for their needs — not off-the-shelf packages.</p>
        </div>
      </div>
      <div class="why-point">
        <div class="why-icon">🔒</div>
        <div>
          <div class="why-point-title">Professional &amp; Confidential</div>
          <p class="why-point-desc">Your business affairs are handled with absolute discretion. Confidentiality is a core value, not just a policy.</p>
        </div>
      </div>
      <div class="why-point">
        <div class="why-icon">📅</div>
        <div>
          <div class="why-point-title">10+ Years of Experience</div>
          <p class="why-point-desc">Over a decade of hands-on experience in income tax, accounting, and corporate services — knowledge that translates directly to better outcomes for clients.</p>
        </div>
      </div>
      <div class="why-point">
        <div class="why-icon">🤝</div>
        <div>
          <div class="why-point-title">Individual &amp; Business Focus</div>
          <p class="why-point-desc">Whether you're an individual taxpayer or a growing business, our services are structured to serve both with equal care and expertise.</p>
        </div>
      </div>
    </div>
  </div>

  <div class="why-right">
    <div class="cta-card-title">Book a Consultation</div>
    <p class="cta-card-sub">Call or email us to arrange an appointment. We'll discuss your needs and outline how Tamweel Corporate Services can help.</p>

    <div class="cta-phone">
      <div class="cta-phone-icon">📞</div>
      <div>
        <div class="cta-phone-lbl">Call for an appointment</div>
        <div class="cta-phone-num">54991117</div>
      </div>
    </div>

    <div class="cta-email-row">
      ✉ <span>General: <a href="mailto:info@tamweelltd.com">info@tamweelltd.com</a></span>
    </div>
    <div class="cta-email-row">
      ✉ <span>Consulting: <a href="mailto:consultant@tamweelltd.com">consultant@tamweelltd.com</a></span>
    </div>

    <div class="cta-divider"></div>

    <div class="cta-addr">
      <strong>Our Address</strong>
      Avenue 1 Trianon, Quatre Bornes<br>
      Crn. Trianon No. 1 &amp; Ave. Tulipes<br>
      Mauritius
    </div>

    <div class="cta-divider"></div>
    <div class="cta-addr">
      <strong>Fax</strong>
      (230) 465 56 20
    </div>

    <a href="#contact" class="btn-white">Send Us a Message</a>
  </div>
</section>

<!-- CONTACT FORM -->
<section class="contact-section" id="contact">
  <div class="contact-form-wrap">
    <div class="form-title">Send Us a Message</div>
    <div class="form-row">
      <div class="form-group">
        <label>First Name</label>
        <input type="text" placeholder="John">
      </div>
      <div class="form-group">
        <label>Last Name</label>
        <input type="text" placeholder="Smith">
      </div>
    </div>
    <div class="form-group">
      <label>Email Address</label>
      <input type="email" placeholder="john@email.com">
    </div>
    <div class="form-group">
      <label>Phone Number</label>
      <input type="tel" placeholder="+230 XXXX XXXX">
    </div>
    <div class="form-group">
      <label>Service Required</label>
      <select>
        <option value="">— Select a service —</option>
        <option>Tax – Income Tax Preparation (Individual)</option>
        <option>Tax – Company Tax Returns</option>
        <option>Tax – VAT / PAYE / TDS</option>
        <option>Tax – Tax Planning</option>
        <option>Accounting – Bookkeeping &amp; Financial Reporting</option>
        <option>Accounting – Budget Analysis</option>
        <option>Accounting – Internal Audit</option>
        <option>Outsourcing – Payroll Services</option>
        <option>Advisory – Business Plan &amp; Forecast</option>
        <option>Advisory – Corporate Finance</option>
        <option>Secretarial – Company Formation</option>
        <option>General Consultancy</option>
      </select>
    </div>
    <div class="form-group">
      <label>Message</label>
      <textarea placeholder="Tell us about your requirements…"></textarea>
    </div>
    <button class="submit-btn">Send Message</button>
  </div>

  <div class="contact-info-side">
    <div class="sec-label">Contact Details</div>
    <h2 class="sec-h2">Get In Touch</h2>
    <p class="sec-sub">We're based in Quatre Bornes, Mauritius and available to assist individuals and businesses. Reach out by phone, email, or the contact form.</p>

    <div class="cdet">
      <div class="cdet-icon">📍</div>
      <div class="cdet-body">
        <strong>Address</strong>
        <span>Crn. Trianon No. 1 &amp; Ave. Tulipes<br>Avenue 1 Trianon, Quatre Bornes<br>Mauritius</span>
      </div>
    </div>
    <div class="cdet">
      <div class="cdet-icon">📞</div>
      <div class="cdet-body">
        <strong>Telephone / Mobile</strong>
        <span><a href="tel:54991117">(230) 5449 0217</a><br><a href="tel:54991117">(230) 5499 1117</a></span>
      </div>
    </div>
    <div class="cdet">
      <div class="cdet-icon">📠</div>
      <div class="cdet-body">
        <strong>Fax</strong>
        <span>(230) 465 56 20</span>
      </div>
    </div>
    <div class="cdet">
      <div class="cdet-icon">✉</div>
      <div class="cdet-body">
        <strong>Email</strong>
        <span><a href="mailto:info@tamweelltd.com">info@tamweelltd.com</a><br><a href="mailto:consultant@tamweelltd.com">consultant@tamweelltd.com</a></span>
      </div>
    </div>
    <div class="cdet">
      <div class="cdet-icon">📘</div>
      <div class="cdet-body">
        <strong>Facebook</strong>
        <span><a href="https://www.facebook.com/TamweelCorporateServicesLTD" target="_blank">Tamweel Corporate Services LTD</a></span>
      </div>
    </div>

    <div class="conf-badge">
      <div class="conf-icon">🔒</div>
      <div class="conf-text">
        <strong>Professional &amp; Confidential</strong>
        <span>All information you share with us is handled with full professional discretion.</span>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div class="footer-brand">
      <div class="footer-brand-name">TAMWEEL <span>CORPORATE SERVICES LTD</span></div>
      <div class="footer-brand-tag">Accounting &amp; Tax Systems | Outsourcing Solutions | Mauritius</div>
      <p>"Unmatched Tailor Made Solutions" — We are a team of professionals with wide experience in Practice and Industry, providing high quality services to our clients with professionalism, competency, integrity, and commitment.</p>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Services</div>
      <ul>
        <li><a href="#services">Tax Returns &amp; Planning</a></li>
        <li><a href="#services">Accounting &amp; Bookkeeping</a></li>
        <li><a href="#services">Payroll Services</a></li>
        <li><a href="#services">Business Advisory</a></li>
        <li><a href="#services">Company Formation</a></li>
        <li><a href="#services">Consultancy</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Company</div>
      <ul>
        <li><a href="#about">About Us</a></li>
        <li><a href="#why">Why Choose Us</a></li>
        <li><a href="#contact">Contact</a></li>
        <li><a href="https://www.facebook.com/TamweelCorporateServicesLTD" target="_blank">Facebook</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Contact</div>
      <ul>
        <li><a href="tel:54490217">5449 0217</a></li>
        <li><a href="tel:54991117">5499 1117</a></li>
        <li><a href="mailto:info@tamweelltd.com">info@tamweelltd.com</a></li>
        <li><a href="mailto:consultant@tamweelltd.com">consultant@tamweelltd.com</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span>&copy; 2025 Tamweel Corporate Services Ltd. All rights reserved. &nbsp;|&nbsp; Quatre Bornes, Mauritius</span>
    <span><a href="#">Privacy Policy</a> &nbsp;·&nbsp; <a href="#">Terms</a></span>
  </div>
</footer>

</body>
</html>
