<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CareerCraft — AI-Powered Placement Prep for India</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,700;0,9..144,900;1,9..144,400&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --ink:       #0D0D12;
    --paper:     #F9F5EE;
    --cream:     #F2EBD9;
    --saffron:   #E8681A;
    --saffron2:  #F58B40;
    --teal:      #1A6B5A;
    --teal2:     #23896F;
    --gold:      #C9960C;
    --muted:     #6B6560;
    --line:      rgba(13,13,18,.10);
    --r:         12px;
    --font-head: 'Fraunces', serif;
    --font-body: 'DM Sans', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--font-body);
    background: var(--paper);
    color: var(--ink);
    overflow-x: hidden;
    font-size: 16px;
    line-height: 1.6;
  }

  /* ── Utility ── */
  .container { max-width: 1160px; margin: 0 auto; padding: 0 28px; }
  .tag { display: inline-block; font-size: 11px; font-weight: 600; letter-spacing: .08em; text-transform: uppercase; padding: 5px 13px; border-radius: 99px; }
  .tag-saffron { background: rgba(232,104,26,.12); color: var(--saffron); }
  .tag-teal    { background: rgba(26,107,90,.12);  color: var(--teal); }
  .tag-gold    { background: rgba(201,150,12,.14); color: var(--gold); }
  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    font-family: var(--font-body); font-weight: 600; font-size: 15px;
    padding: 14px 28px; border-radius: 99px; cursor: pointer;
    border: none; text-decoration: none; transition: all .22s ease;
  }
  .btn-primary { background: var(--saffron); color: #fff; }
  .btn-primary:hover { background: #cf5a14; transform: translateY(-1px); box-shadow: 0 8px 24px rgba(232,104,26,.35); }
  .btn-outline { background: transparent; color: var(--ink); border: 1.5px solid rgba(13,13,18,.2); }
  .btn-outline:hover { border-color: var(--saffron); color: var(--saffron); }
  .btn-teal { background: var(--teal); color: #fff; }
  .btn-teal:hover { background: var(--teal2); transform: translateY(-1px); box-shadow: 0 8px 24px rgba(26,107,90,.3); }

  /* ── Animations ── */
  @keyframes fadeUp { from { opacity: 0; transform: translateY(28px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes floatY { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
  @keyframes spin { to { transform: rotate(360deg); } }
  @keyframes blink { 0%,100%{opacity:1}50%{opacity:0} }

  .reveal { opacity: 0; transform: translateY(32px); transition: opacity .7s ease, transform .7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 18px 0;
    background: rgba(249,245,238,.88);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--line);
    transition: padding .3s;
  }
  nav.scrolled { padding: 12px 0; }
  .nav-inner { display: flex; align-items: center; justify-content: space-between; }
  .nav-logo {
    font-family: var(--font-head); font-size: 22px; font-weight: 900;
    color: var(--ink); text-decoration: none; letter-spacing: -.02em;
  }
  .nav-logo span { color: var(--saffron); }
  .nav-links { display: flex; align-items: center; gap: 32px; list-style: none; }
  .nav-links a { font-size: 14px; font-weight: 500; color: var(--muted); text-decoration: none; transition: color .2s; }
  .nav-links a:hover { color: var(--ink); }
  .nav-cta { display: flex; gap: 10px; align-items: center; }
  .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
  .hamburger span { width: 22px; height: 2px; background: var(--ink); border-radius: 2px; transition: all .3s; }

  /* ── HERO ── */
  .hero {
    padding: 148px 0 80px;
    position: relative;
    overflow: hidden;
    min-height: 92vh;
    display: flex; align-items: center;
  }
  .hero-bg {
    position: absolute; inset: 0; z-index: 0;
    background:
      radial-gradient(ellipse 60% 55% at 70% 40%, rgba(232,104,26,.10) 0%, transparent 70%),
      radial-gradient(ellipse 45% 45% at 20% 70%, rgba(26,107,90,.08) 0%, transparent 65%);
  }
  .hero-grain {
    position: absolute; inset: 0; z-index: 0; opacity: .025;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 180px;
  }
  .hero-content { position: relative; z-index: 1; max-width: 700px; }
  .hero-tag { margin-bottom: 24px; animation: fadeUp .6s ease both; }
  .hero h1 {
    font-family: var(--font-head); font-size: clamp(44px, 6vw, 78px);
    font-weight: 900; line-height: 1.05; letter-spacing: -.03em;
    color: var(--ink); margin-bottom: 24px;
    animation: fadeUp .6s .12s ease both;
  }
  .hero h1 em { font-style: italic; color: var(--saffron); }
  .hero p {
    font-size: clamp(17px, 2vw, 19px); color: var(--muted); max-width: 520px;
    margin-bottom: 36px; font-weight: 400; line-height: 1.65;
    animation: fadeUp .6s .22s ease both;
  }
  .hero-actions {
    display: flex; gap: 12px; flex-wrap: wrap;
    animation: fadeUp .6s .32s ease both;
  }
  .hero-stats {
    display: flex; gap: 40px; margin-top: 60px; flex-wrap: wrap;
    animation: fadeUp .6s .44s ease both;
  }
  .stat-item {}
  .stat-num { font-family: var(--font-head); font-size: 32px; font-weight: 700; color: var(--ink); line-height: 1; }
  .stat-label { font-size: 13px; color: var(--muted); margin-top: 4px; }
  .hero-visual {
    position: absolute; right: -20px; top: 50%; transform: translateY(-50%);
    width: 42%; max-width: 480px; z-index: 1;
    animation: fadeIn .9s .4s ease both;
    display: grid; grid-template-columns: 1fr 1fr; gap: 14px;
  }
  .hero-card {
    background: #fff; border: 1px solid var(--line); border-radius: 16px;
    padding: 20px; box-shadow: 0 4px 24px rgba(0,0,0,.07);
    animation: floatY 5s ease-in-out infinite;
  }
  .hero-card:nth-child(2) { animation-delay: .8s; }
  .hero-card:nth-child(3) { animation-delay: .4s; }
  .hero-card:nth-child(4) { animation-delay: 1.2s; }
  .hero-card-icon { font-size: 24px; margin-bottom: 10px; }
  .hero-card-label { font-size: 12px; font-weight: 600; color: var(--muted); letter-spacing: .04em; text-transform: uppercase; }
  .hero-card-val { font-family: var(--font-head); font-size: 22px; font-weight: 700; color: var(--ink); margin-top: 4px; }
  .hero-card-sub { font-size: 12px; color: var(--muted); margin-top: 4px; }
  .hero-card.accent { background: var(--saffron); border-color: transparent; }
  .hero-card.accent .hero-card-label,
  .hero-card.accent .hero-card-val,
  .hero-card.accent .hero-card-sub { color: #fff; }
  .hero-card.teal { background: var(--teal); border-color: transparent; }
  .hero-card.teal .hero-card-label,
  .hero-card.teal .hero-card-val,
  .hero-card.teal .hero-card-sub { color: #fff; }

  /* ── TRUST BAR ── */
  .trust-bar {
    background: var(--cream); border-top: 1px solid var(--line); border-bottom: 1px solid var(--line);
    padding: 20px 0;
  }
  .trust-inner { display: flex; align-items: center; gap: 40px; flex-wrap: wrap; justify-content: center; }
  .trust-item { display: flex; align-items: center; gap: 8px; font-size: 13px; font-weight: 500; color: var(--muted); }
  .trust-icon { font-size: 16px; }
  .trust-sep { width: 4px; height: 4px; border-radius: 50%; background: var(--line); }

  /* ── SECTION TITLES ── */
  .section-head { text-align: center; margin-bottom: 56px; }
  .section-head .tag { margin-bottom: 14px; }
  .section-head h2 {
    font-family: var(--font-head); font-size: clamp(32px, 4.5vw, 52px);
    font-weight: 900; line-height: 1.1; letter-spacing: -.025em; color: var(--ink);
  }
  .section-head h2 em { font-style: italic; color: var(--saffron); }
  .section-head p { font-size: 17px; color: var(--muted); max-width: 500px; margin: 16px auto 0; }

  /* ── HOW IT WORKS ── */
  .how { padding: 100px 0; }
  .steps-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; }
  .step-card {
    background: #fff; border: 1px solid var(--line); border-radius: 16px;
    padding: 28px 24px; position: relative; transition: transform .22s, box-shadow .22s;
  }
  .step-card:hover { transform: translateY(-5px); box-shadow: 0 16px 40px rgba(0,0,0,.09); }
  .step-num {
    width: 36px; height: 36px; border-radius: 50%;
    background: var(--saffron); color: #fff;
    font-family: var(--font-head); font-weight: 700; font-size: 16px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 16px;
  }
  .step-arrow {
    position: absolute; top: 28px; right: -18px; z-index: 2;
    font-size: 20px; color: var(--saffron);
  }
  .step-card:last-child .step-arrow { display: none; }
  .step-card h3 { font-size: 16px; font-weight: 700; color: var(--ink); margin-bottom: 8px; }
  .step-card p { font-size: 14px; color: var(--muted); line-height: 1.6; }

  /* ── FEATURES ── */
  .features { padding: 100px 0; background: var(--cream); }
  .features-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .feat-card {
    background: var(--paper); border: 1px solid var(--line); border-radius: 20px;
    padding: 36px; transition: transform .22s, box-shadow .22s;
  }
  .feat-card:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,.08); }
  .feat-card.wide { grid-column: span 2; display: grid; grid-template-columns: 1fr 1fr; gap: 40px; align-items: center; }
  .feat-icon { font-size: 36px; margin-bottom: 16px; }
  .feat-card h3 { font-family: var(--font-head); font-size: 22px; font-weight: 700; color: var(--ink); margin-bottom: 10px; }
  .feat-card p { font-size: 15px; color: var(--muted); line-height: 1.65; }
  .feat-visual {
    background: var(--ink); border-radius: 14px; padding: 24px;
    font-family: 'Courier New', monospace; font-size: 13px; line-height: 1.7;
  }
  .feat-visual .line-g { color: #4EC9A1; }
  .feat-visual .line-y { color: #E8C86A; }
  .feat-visual .line-w { color: rgba(255,255,255,.75); }
  .feat-visual .line-d { color: rgba(255,255,255,.3); }
  .feat-tag { display: inline-flex; align-items: center; gap: 5px; font-size: 12px; font-weight: 600; padding: 4px 10px; border-radius: 6px; margin-bottom: 6px; }
  .feat-bullets { list-style: none; margin-top: 18px; display: flex; flex-direction: column; gap: 8px; }
  .feat-bullets li { display: flex; align-items: flex-start; gap: 10px; font-size: 14px; color: var(--muted); }
  .feat-bullets li::before { content: "✓"; color: var(--teal); font-weight: 700; flex-shrink: 0; margin-top: 1px; }

  /* ── PRICING ── */
  .pricing { padding: 100px 0; }
  .pricing-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; max-width: 960px; margin: 0 auto; }
  .price-card {
    background: #fff; border: 1.5px solid var(--line); border-radius: 20px;
    padding: 36px 32px; position: relative; transition: transform .22s, box-shadow .22s;
  }
  .price-card:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,.09); }
  .price-card.featured { border-color: var(--saffron); background: var(--ink); color: #fff; }
  .price-badge {
    position: absolute; top: -13px; left: 50%; transform: translateX(-50%);
    background: var(--saffron); color: #fff;
    font-size: 11px; font-weight: 700; letter-spacing: .06em; text-transform: uppercase;
    padding: 4px 14px; border-radius: 99px;
  }
  .price-name { font-size: 13px; font-weight: 600; color: var(--muted); text-transform: uppercase; letter-spacing: .06em; margin-bottom: 12px; }
  .price-card.featured .price-name { color: rgba(255,255,255,.6); }
  .price-amount { font-family: var(--font-head); font-size: 44px; font-weight: 900; color: var(--ink); line-height: 1; }
  .price-card.featured .price-amount { color: #fff; }
  .price-amount sup { font-size: 20px; vertical-align: super; }
  .price-per { font-size: 13px; color: var(--muted); margin-top: 4px; }
  .price-card.featured .price-per { color: rgba(255,255,255,.5); }
  .price-divider { height: 1px; background: var(--line); margin: 24px 0; }
  .price-card.featured .price-divider { background: rgba(255,255,255,.12); }
  .price-features { list-style: none; display: flex; flex-direction: column; gap: 10px; margin-bottom: 28px; }
  .price-features li { display: flex; gap: 10px; font-size: 14px; color: var(--muted); }
  .price-card.featured .price-features li { color: rgba(255,255,255,.75); }
  .price-features li::before { content: "✓"; color: var(--teal); font-weight: 700; flex-shrink: 0; }
  .price-card.featured .price-features li::before { color: var(--saffron2); }
  .price-card .btn { width: 100%; justify-content: center; }

  /* ── TESTIMONIALS ── */
  .testimonials { padding: 100px 0; background: var(--cream); }
  .testi-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
  .testi-card {
    background: var(--paper); border: 1px solid var(--line); border-radius: 18px;
    padding: 28px; position: relative;
  }
  .testi-quote { font-size: 40px; line-height: 1; color: var(--saffron); font-family: var(--font-head); margin-bottom: 12px; }
  .testi-text { font-size: 15px; color: var(--ink); line-height: 1.65; margin-bottom: 20px; font-style: italic; }
  .testi-author { display: flex; align-items: center; gap: 12px; }
  .testi-avatar {
    width: 40px; height: 40px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: var(--font-head); font-weight: 700; font-size: 16px; color: #fff;
  }
  .testi-name { font-size: 14px; font-weight: 600; color: var(--ink); }
  .testi-role { font-size: 12px; color: var(--muted); }
  .stars { color: var(--gold); font-size: 14px; margin-bottom: 6px; }

  /* ── COMPARISON ── */
  .comparison { padding: 100px 0; }
  .compare-table { width: 100%; border-collapse: collapse; margin-top: 48px; border-radius: 16px; overflow: hidden; border: 1px solid var(--line); }
  .compare-table th { padding: 18px 20px; font-size: 13px; font-weight: 700; text-align: left; background: var(--ink); color: #fff; }
  .compare-table th:first-child { background: var(--ink); }
  .compare-table th.highlight { background: var(--saffron); }
  .compare-table td { padding: 16px 20px; font-size: 14px; border-bottom: 1px solid var(--line); }
  .compare-table tr:last-child td { border-bottom: none; }
  .compare-table td:first-child { font-weight: 600; color: var(--ink); }
  .compare-table tr:nth-child(even) td { background: rgba(249,245,238,.5); }
  .compare-table td.highlight { background: rgba(232,104,26,.06); font-weight: 600; }
  .check { color: var(--teal); font-weight: 700; font-size: 16px; }
  .cross { color: #C0392B; }
  .partial { color: var(--gold); }

  /* ── INDIA SECTION ── */
  .india { padding: 100px 0; background: var(--ink); color: #fff; }
  .india .section-head h2 { color: #fff; }
  .india .section-head h2 em { color: var(--saffron2); }
  .india .section-head p { color: rgba(255,255,255,.6); }
  .india-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
  .india-card {
    background: rgba(255,255,255,.06); border: 1px solid rgba(255,255,255,.1);
    border-radius: 18px; padding: 28px; transition: background .22s;
  }
  .india-card:hover { background: rgba(255,255,255,.09); }
  .india-icon { font-size: 32px; margin-bottom: 14px; }
  .india-card h3 { font-size: 17px; font-weight: 700; color: #fff; margin-bottom: 8px; }
  .india-card p { font-size: 14px; color: rgba(255,255,255,.6); line-height: 1.65; }

  /* ── CTA ── */
  .cta-section { padding: 120px 0; text-align: center; position: relative; overflow: hidden; }
  .cta-section::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 70% 60% at 50% 50%, rgba(232,104,26,.10) 0%, transparent 70%);
  }
  .cta-section .container { position: relative; }
  .cta-section h2 {
    font-family: var(--font-head); font-size: clamp(36px, 5vw, 62px);
    font-weight: 900; letter-spacing: -.03em; margin-bottom: 20px; line-height: 1.1;
  }
  .cta-section h2 em { font-style: italic; color: var(--saffron); }
  .cta-section p { font-size: 18px; color: var(--muted); max-width: 480px; margin: 0 auto 36px; }
  .cta-buttons { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
  .whatsapp-btn {
    background: #25D366; color: #fff;
    display: inline-flex; align-items: center; gap: 8px;
    padding: 14px 28px; border-radius: 99px;
    font-weight: 600; font-size: 15px; text-decoration: none;
    transition: all .22s;
  }
  .whatsapp-btn:hover { background: #20b358; transform: translateY(-1px); box-shadow: 0 8px 24px rgba(37,211,102,.35); }

  /* ── FOOTER ── */
  footer {
    background: var(--ink); color: rgba(255,255,255,.5);
    padding: 60px 0 32px;
  }
  .footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 48px; margin-bottom: 48px; }
  .footer-logo { font-family: var(--font-head); font-size: 26px; font-weight: 900; color: #fff; margin-bottom: 12px; }
  .footer-logo span { color: var(--saffron2); }
  .footer-desc { font-size: 14px; line-height: 1.7; max-width: 260px; }
  .footer-col h4 { font-size: 13px; font-weight: 700; color: #fff; text-transform: uppercase; letter-spacing: .06em; margin-bottom: 16px; }
  .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .footer-col a { font-size: 14px; color: rgba(255,255,255,.5); text-decoration: none; transition: color .2s; }
  .footer-col a:hover { color: var(--saffron2); }
  .footer-bottom { border-top: 1px solid rgba(255,255,255,.08); padding-top: 24px; display: flex; justify-content: space-between; align-items: center; flex-wrap: gap; }
  .footer-bottom p { font-size: 13px; }

  /* ── MOBILE NAV ── */
  .mobile-menu {
    display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0;
    background: var(--paper); z-index: 200; flex-direction: column;
    padding: 80px 28px 40px; gap: 24px;
  }
  .mobile-menu.open { display: flex; }
  .mobile-menu a { font-size: 28px; font-family: var(--font-head); font-weight: 700; color: var(--ink); text-decoration: none; }
  .mobile-menu a:hover { color: var(--saffron); }
  .mobile-close { position: absolute; top: 20px; right: 28px; font-size: 28px; cursor: pointer; color: var(--ink); background: none; border: none; }

  /* ── FAQ ── */
  .faq { padding: 100px 0; background: var(--cream); }
  .faq-list { max-width: 720px; margin: 0 auto; display: flex; flex-direction: column; gap: 2px; }
  .faq-item { background: var(--paper); border-radius: 12px; overflow: hidden; border: 1px solid var(--line); }
  .faq-q {
    width: 100%; text-align: left; padding: 20px 24px;
    background: none; border: none; cursor: pointer;
    display: flex; justify-content: space-between; align-items: center;
    font-family: var(--font-body); font-size: 15px; font-weight: 600; color: var(--ink);
  }
  .faq-q span { width: 22px; height: 22px; border-radius: 50%; background: var(--saffron); color: #fff; display: flex; align-items: center; justify-content: center; font-size: 14px; flex-shrink: 0; transition: transform .3s; }
  .faq-item.open .faq-q span { transform: rotate(45deg); }
  .faq-a { max-height: 0; overflow: hidden; transition: max-height .4s ease, padding .3s; padding: 0 24px; font-size: 14px; color: var(--muted); line-height: 1.7; }
  .faq-item.open .faq-a { max-height: 200px; padding: 0 24px 20px; }

  /* ── RESPONSIVE ── */
  @media (max-width: 1024px) {
    .hero-visual { display: none; }
    .features-grid { grid-template-columns: 1fr; }
    .feat-card.wide { grid-column: span 1; grid-template-columns: 1fr; }
    .steps-grid { grid-template-columns: 1fr 1fr; }
  }
  @media (max-width: 768px) {
    .nav-links, .nav-cta { display: none; }
    .hamburger { display: flex; }
    .pricing-grid { grid-template-columns: 1fr; }
    .testi-grid { grid-template-columns: 1fr; }
    .india-grid { grid-template-columns: 1fr; }
    .footer-grid { grid-template-columns: 1fr 1fr; gap: 32px; }
    .steps-grid { grid-template-columns: 1fr; }
    .step-arrow { display: none; }
    .compare-table { font-size: 13px; }
    .compare-table th, .compare-table td { padding: 12px 10px; }
  }
  @media (max-width: 480px) {
    .footer-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav id="navbar">
  <div class="container nav-inner">
    <a href="#" class="nav-logo">Career<span>Craft</span></a>
    <ul class="nav-links">
      <li><a href="#how">How it works</a></li>
      <li><a href="#features">Features</a></li>
      <li><a href="#pricing">Pricing</a></li>
      <li><a href="#testimonials">Reviews</a></li>
      <li><a href="#faq">FAQ</a></li>
    </ul>
    <div class="nav-cta">
      <a href="#pricing" class="btn btn-outline" style="padding:10px 20px;font-size:14px;">View Plans</a>
      <a href="#cta" class="btn btn-primary" style="padding:10px 20px;font-size:14px;">Get Started Free</a>
    </div>
    <div class="hamburger" id="hamburger" onclick="toggleMenu()">
      <span></span><span></span><span></span>
    </div>
  </div>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <button class="mobile-close" onclick="toggleMenu()">✕</button>
  <a href="#how" onclick="toggleMenu()">How it works</a>
  <a href="#features" onclick="toggleMenu()">Features</a>
  <a href="#pricing" onclick="toggleMenu()">Pricing</a>
  <a href="#testimonials" onclick="toggleMenu()">Reviews</a>
  <a href="#cta" onclick="toggleMenu()">Get Started</a>
</div>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-grain"></div>
  <div class="container">
    <div class="hero-content">
      <div class="hero-tag"><span class="tag tag-saffron">🇮🇳 Built for India</span></div>
      <h1>Land your <em>dream job</em> with AI-powered prep</h1>
      <p>CareerCraft gives every Tier-2 college student access to personalised mock interviews, AI resume review, and company-specific question banks — at a price that makes sense.</p>
      <div class="hero-actions">
        <a href="#cta" class="btn btn-primary">Start for ₹99 →</a>
        <a href="#how" class="btn btn-outline">See how it works</a>
      </div>
      <div class="hero-stats">
        <div class="stat-item">
          <div class="stat-num">10M+</div>
          <div class="stat-label">Graduates yearly in India</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">₹99</div>
          <div class="stat-label">Starting price</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">4 hrs</div>
          <div class="stat-label">Report turnaround</div>
        </div>
      </div>
    </div>

    <div class="hero-visual">
      <div class="hero-card">
        <div class="hero-card-icon">📄</div>
        <div class="hero-card-label">Resume Score</div>
        <div class="hero-card-val">87/100</div>
        <div class="hero-card-sub">+24 pts after AI fix</div>
      </div>
      <div class="hero-card accent">
        <div class="hero-card-icon">🎯</div>
        <div class="hero-card-label">Interview Ready</div>
        <div class="hero-card-val">Deloitte</div>
        <div class="hero-card-sub">Case + HR round</div>
      </div>
      <div class="hero-card teal">
        <div class="hero-card-icon">💬</div>
        <div class="hero-card-label">Mock Score</div>
        <div class="hero-card-val">8.4/10</div>
        <div class="hero-card-sub">STAR format</div>
      </div>
      <div class="hero-card">
        <div class="hero-card-icon">🏙️</div>
        <div class="hero-card-label">Salary Data</div>
        <div class="hero-card-val">Nagpur</div>
        <div class="hero-card-sub">₹4.8L median</div>
      </div>
    </div>
  </div>
</section>

<!-- TRUST BAR -->
<div class="trust-bar">
  <div class="container">
    <div class="trust-inner">
      <div class="trust-item"><span class="trust-icon">✅</span> WhatsApp-first delivery</div>
      <div class="trust-sep"></div>
      <div class="trust-item"><span class="trust-icon">🏢</span> Infosys · Deloitte · HDFC · Wipro Q Banks</div>
      <div class="trust-sep"></div>
      <div class="trust-item"><span class="trust-icon">🗣️</span> Hindi + English support</div>
      <div class="trust-sep"></div>
      <div class="trust-item"><span class="trust-icon">🎓</span> 50+ college partnerships</div>
      <div class="trust-sep"></div>
      <div class="trust-item"><span class="trust-icon">💳</span> UPI / Razorpay · Instant access</div>
    </div>
  </div>
</div>

<!-- HOW IT WORKS -->
<section class="how" id="how">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-teal">Process</span>
      <h2>From resume to <em>offer letter</em> in 4 steps</h2>
      <p>No app download. No long signup. Just WhatsApp us your resume and we handle the rest.</p>
    </div>
    <div class="steps-grid reveal">
      <div class="step-card">
        <div class="step-num">1</div>
        <div class="step-arrow">→</div>
        <h3>Upload Your Resume</h3>
        <p>Send your CV and target company/role on WhatsApp or via our web form. Takes under 60 seconds.</p>
      </div>
      <div class="step-card">
        <div class="step-num">2</div>
        <div class="step-arrow">→</div>
        <h3>AI Scores & Rewrites</h3>
        <p>Our AI analyses your resume against the job description, scores keyword match, and rewrites weak bullet points.</p>
      </div>
      <div class="step-card">
        <div class="step-num">3</div>
        <div class="step-arrow">→</div>
        <h3>Mock Interview Session</h3>
        <p>Company-specific interview tailored to your target employer. HR round, case study, or technical — your choice.</p>
      </div>
      <div class="step-card">
        <div class="step-num">4</div>
        <h3>Get Your Report Card</h3>
        <p>Receive a personalised PDF: confidence score, top 3 weaknesses, salary benchmark, and your study plan to close gaps.</p>
      </div>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section class="features" id="features">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-saffron">Features</span>
      <h2>Everything you need to <em>crack</em> placement</h2>
      <p>Purpose-built for India's job market — not a generic global tool.</p>
    </div>
    <div class="features-grid">

      <div class="feat-card wide reveal">
        <div>
          <div class="feat-icon">🤖</div>
          <span class="tag tag-saffron" style="font-size:11px;margin-bottom:12px;">Core Feature</span>
          <h3>Company-Specific Mock Interviewer</h3>
          <p>Train with questions actually asked at Infosys, Deloitte, HDFC, Wipro, Accenture, and 30+ more Indian employers — crowdsourced from students who sat in those exact drives.</p>
          <ul class="feat-bullets">
            <li>HR, technical, and case study rounds</li>
            <li>Voice or text — your preference</li>
            <li>STAR-format scoring and instant feedback</li>
            <li>Confidence score out of 10 per answer</li>
          </ul>
        </div>
        <div class="feat-visual">
          <div class="line-d">// Mock Interview — Deloitte HR Round</div>
          <div class="line-y">Q: "Tell me about a time you led</div>
          <div class="line-y">&nbsp;&nbsp;&nbsp;a team under pressure."</div>
          <br>
          <div class="line-w">Your answer: "During our college fest..."</div>
          <br>
          <div class="line-g">✓ Situation — Clear (9/10)</div>
          <div class="line-g">✓ Task — Specific (8/10)</div>
          <div class="line-y">⚡ Action — Needs more detail (6/10)</div>
          <div class="line-g">✓ Result — Quantified (9/10)</div>
          <br>
          <div class="line-d">Overall STAR Score: 8.0/10</div>
          <div class="line-g">Recommendation: Expand Action step →</div>
        </div>
      </div>

      <div class="feat-card reveal">
        <div class="feat-icon">📄</div>
        <h3>AI Resume Optimiser</h3>
        <p>Paste any job description — our AI scores your resume, flags keyword gaps, and rewrites weak bullet points in plain, recruiter-friendly language in under 60 seconds.</p>
        <ul class="feat-bullets">
          <li>JD keyword match score</li>
          <li>Bullet point rewriter</li>
          <li>ATS compatibility check</li>
        </ul>
      </div>

      <div class="feat-card reveal">
        <div class="feat-icon">📊</div>
        <h3>Salary Benchmarking by City</h3>
        <p>Know what to ask for. Real salary data broken down by role, company, and city tier — so you never undersell yourself in a Nagpur vs Mumbai negotiation.</p>
        <ul class="feat-bullets">
          <li>25+ Indian cities covered</li>
          <li>Updated quarterly</li>
          <li>Role + company breakdown</li>
        </ul>
      </div>

      <div class="feat-card reveal">
        <div class="feat-icon">🏅</div>
        <h3>Verified Skills Portfolio</h3>
        <p>Build your profile year-round, not just during placement season. Earn CareerCraft-certified badges for communication, aptitude, and case analysis that you can share on LinkedIn.</p>
        <ul class="feat-bullets">
          <li>Shareable badge links</li>
          <li>Year-round engagement</li>
          <li>Employer-visible profiles</li>
        </ul>
      </div>

      <div class="feat-card reveal">
        <div class="feat-icon">💬</div>
        <h3>WhatsApp-First Delivery</h3>
        <p>No app to download. No complex onboarding. Send your resume on WhatsApp and get your report back within 4 hours — because we built for how Indian students actually work.</p>
        <ul class="feat-bullets">
          <li>Hindi + English support</li>
          <li>4-hour turnaround</li>
          <li>WhatsApp + web both work</li>
        </ul>
      </div>

    </div>
  </div>
</section>

<!-- PRICING -->
<section class="pricing" id="pricing">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-gold">Pricing</span>
      <h2>Simple pricing, <em>real value</em></h2>
      <p>Pay per session or unlock unlimited prep. Zero hidden fees — pay via UPI in seconds.</p>
    </div>
    <div class="pricing-grid reveal">

      <div class="price-card">
        <div class="price-name">Starter</div>
        <div class="price-amount"><sup>₹</sup>99</div>
        <div class="price-per">one-time, per session</div>
        <div class="price-divider"></div>
        <ul class="price-features">
          <li>1 AI mock interview session</li>
          <li>Resume score + top fixes</li>
          <li>Written feedback report (PDF)</li>
          <li>Salary benchmark for your city</li>
          <li>Delivered via WhatsApp in 4 hrs</li>
        </ul>
        <a href="#cta" class="btn btn-outline" style="justify-content:center;">Start with ₹99</a>
      </div>

      <div class="price-card featured">
        <div class="price-badge">Most Popular</div>
        <div class="price-name">Placement Pack</div>
        <div class="price-amount"><sup>₹</sup>299</div>
        <div class="price-per">30-day unlimited access</div>
        <div class="price-divider"></div>
        <ul class="price-features">
          <li>Unlimited mock interviews</li>
          <li>Full resume rewrite service</li>
          <li>Company Q bank (30+ firms)</li>
          <li>2 live review sessions</li>
          <li>Salary negotiation guide</li>
          <li>Skills portfolio badge</li>
        </ul>
        <a href="#cta" class="btn btn-primary" style="justify-content:center;">Get the Pack →</a>
      </div>

      <div class="price-card">
        <div class="price-name">College Licence</div>
        <div class="price-amount" style="font-size:32px;"><sup>₹</sup>30K+</div>
        <div class="price-per">per college, per year</div>
        <div class="price-divider"></div>
        <ul class="price-features">
          <li>Full batch access (all students)</li>
          <li>TPO placement dashboard</li>
          <li>Monthly workshops included</li>
          <li>Placement rate analytics</li>
          <li>Dedicated account manager</li>
          <li>Custom company Q banks</li>
        </ul>
        <a href="mailto:colleges@careercraft.in" class="btn btn-teal" style="justify-content:center;">Contact Us</a>
      </div>

    </div>
  </div>
</section>

<!-- COMPARISON -->
<section class="comparison" id="compare">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-saffron">Why CareerCraft</span>
      <h2>We do what others <em>don't</em></h2>
      <p>Job boards post listings. We prepare you to win them.</p>
    </div>
    <div class="reveal">
      <table class="compare-table">
        <thead>
          <tr>
            <th>Feature</th>
            <th class="highlight">CareerCraft</th>
            <th>Naukri / LinkedIn</th>
            <th>Internshala</th>
            <th>ChatGPT (free)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Company-specific Q banks (India)</td>
            <td class="highlight"><span class="check">✓ 30+ firms</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
          </tr>
          <tr>
            <td>AI mock interview with STAR scoring</td>
            <td class="highlight"><span class="check">✓</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="partial">~ generic only</span></td>
          </tr>
          <tr>
            <td>Resume review + rewrite</td>
            <td class="highlight"><span class="check">✓ JD-matched</span></td>
            <td><span class="partial">~ basic tips</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="partial">~ no JD match</span></td>
          </tr>
          <tr>
            <td>Salary benchmarks by Indian city</td>
            <td class="highlight"><span class="check">✓ 25+ cities</span></td>
            <td><span class="partial">~ broad ranges</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗ outdated</span></td>
          </tr>
          <tr>
            <td>WhatsApp delivery (no app needed)</td>
            <td class="highlight"><span class="check">✓</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
          </tr>
          <tr>
            <td>Hindi language support</td>
            <td class="highlight"><span class="check">✓</span></td>
            <td><span class="partial">~ partial</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="partial">~ basic</span></td>
          </tr>
          <tr>
            <td>Outcome tracking + proof</td>
            <td class="highlight"><span class="check">✓ placement data</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
            <td><span class="cross">✗</span></td>
          </tr>
          <tr>
            <td>Price for a student</td>
            <td class="highlight"><span class="check">✓ ₹99/session</span></td>
            <td>Free (no prep)</td>
            <td>Free (no prep)</td>
            <td>Free (no depth)</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials" id="testimonials">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-teal">Reviews</span>
      <h2>Students who <em>got shortlisted</em></h2>
      <p>Real feedback from students who used CareerCraft before their placement drives.</p>
    </div>
    <div class="testi-grid">
      <div class="testi-card reveal">
        <div class="stars">★★★★★</div>
        <div class="testi-quote">"</div>
        <p class="testi-text">I had my Deloitte interview in 3 days. The company-specific Q bank had almost the exact questions they asked. Got shortlisted in the first round — I genuinely don't think I would have without this.</p>
        <div class="testi-author">
          <div class="testi-avatar" style="background:var(--saffron);">P</div>
          <div>
            <div class="testi-name">Priya Sharma</div>
            <div class="testi-role">BBA Final Year · Jaipur</div>
          </div>
        </div>
      </div>
      <div class="testi-card reveal">
        <div class="stars">★★★★★</div>
        <div class="testi-quote">"</div>
        <p class="testi-text">My resume was getting zero callbacks. CareerCraft rewrote my bullet points to match the JD and my response rate went from nothing to 4 interviews in 2 weeks. ₹99 was the best money I spent.</p>
        <div class="testi-author">
          <div class="testi-avatar" style="background:var(--teal);">K</div>
          <div>
            <div class="testi-name">Karan Mehta</div>
            <div class="testi-role">B.Com Final Year · Nagpur</div>
          </div>
        </div>
      </div>
      <div class="testi-card reveal">
        <div class="stars">★★★★☆</div>
        <div class="testi-quote">"</div>
        <p class="testi-text">Our TPO got us access through the college licence. The mock interviews are nothing like what our college gives us — they actually ask follow-up questions and score you on STAR. Felt like real prep.</p>
        <div class="testi-author">
          <div class="testi-avatar" style="background:var(--gold);">A</div>
          <div>
            <div class="testi-name">Anjali Verma</div>
            <div class="testi-role">MBA · Lucknow</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- INDIA SECTION -->
<section class="india">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag" style="background:rgba(232,104,26,.2);color:var(--saffron2);">Built for Bharat</span>
      <h2>Designed around how <em>India</em> actually works</h2>
      <p>Not a US tool with an Indian flag. We built from the ground up for Indian students, Indian companies, and Indian realities.</p>
    </div>
    <div class="india-grid">
      <div class="india-card reveal">
        <div class="india-icon">📱</div>
        <h3>WhatsApp-First</h3>
        <p>No app, no login, no friction. India has 500M+ UPI users and 600M+ WhatsApp users. We meet students where they already are.</p>
      </div>
      <div class="india-card reveal">
        <div class="india-icon">🏙️</div>
        <h3>Tier-2 City Focus</h3>
        <p>Salary benchmarks and company insights for Nagpur, Jaipur, Patna, Bhopal, Indore and 20+ more cities — not just Delhi and Mumbai.</p>
      </div>
      <div class="india-card reveal">
        <div class="india-icon">🗣️</div>
        <h3>Hindi + English</h3>
        <p>Ask doubts, get feedback, and prep for interviews in Hindi or English. Code-switching welcome — just like real Indian workplaces.</p>
      </div>
      <div class="india-card reveal">
        <div class="india-icon">🏢</div>
        <h3>Indian Employer Data</h3>
        <p>30+ Indian companies with real question banks crowdsourced from students who actually sat in those interviews — not generic guesses.</p>
      </div>
      <div class="india-card reveal">
        <div class="india-icon">💳</div>
        <h3>UPI Payments</h3>
        <p>Pay in 8 seconds with any UPI app — no credit card needed. Accessible to every student regardless of banking access.</p>
      </div>
      <div class="india-card reveal">
        <div class="india-icon">🎓</div>
        <h3>TPO-Friendly Model</h3>
        <p>College licences that TPOs can adopt to improve their placement rate — without replacing their role or requiring IT integration.</p>
      </div>
    </div>
  </div>
</section>

<!-- FAQ -->
<section class="faq" id="faq">
  <div class="container">
    <div class="section-head reveal">
      <span class="tag tag-gold">FAQ</span>
      <h2>Questions? <em>Answered.</em></h2>
    </div>
    <div class="faq-list reveal">
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">How does the WhatsApp intake work? <span>+</span></button>
        <div class="faq-a">Send your resume as a PDF to our WhatsApp number along with the company and role you're targeting. We process it and send back your AI report within 4 hours. No app download, no login, no forms — just WhatsApp.</div>
      </div>
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">Is this just ChatGPT with a price tag? <span>+</span></button>
        <div class="faq-a">No. ChatGPT has no Indian employer data, no STAR scoring framework, no city-based salary benchmarks, and no outcome tracking. Our company Q banks are crowdsourced from students who sat in actual Infosys, Deloitte, and HDFC interviews — that data doesn't exist anywhere else.</div>
      </div>
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">Can I get help in Hindi? <span>+</span></button>
        <div class="faq-a">Yes, fully. Send us your queries in Hindi, request Hindi-language feedback, or do your entire mock interview in Hindi. We support both languages natively — not just English with a translation layer.</div>
      </div>
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">What companies are covered in the question bank? <span>+</span></button>
        <div class="faq-a">Infosys, TCS, Wipro, HCL, Deloitte, KPMG, EY, PwC, HDFC Bank, ICICI Bank, Axis Bank, Accenture, Cognizant, Capgemini, Zomato, Swiggy, Paytm, and 15+ more — and we add new companies every month based on placement season demand.</div>
      </div>
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">How does the college licence work? <span>+</span></button>
        <div class="faq-a">TPOs pay an annual licence fee (starting ₹30,000/yr) that gives all students in their batch unlimited access to CareerCraft. TPOs also get a placement dashboard showing aggregate preparation data. Students pay nothing directly — the college covers it. Contact us at colleges@careercraft.in for a demo.</div>
      </div>
      <div class="faq-item">
        <button class="faq-q" onclick="toggleFaq(this)">What if I'm not satisfied? <span>+</span></button>
        <div class="faq-a">If your report doesn't meet expectations — feedback is unclear, company Q bank doesn't match your drive, or the AI scoring seems off — message us on WhatsApp and we'll redo your session at no charge. Simple.</div>
      </div>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta-section" id="cta">
  <div class="container">
    <span class="tag tag-saffron" style="margin-bottom:20px;display:inline-block;">Get Started Today</span>
    <h2>Your next interview is<br><em>closer than you think</em></h2>
    <p>Start with a single session for ₹99. No risk, no long commitment — just better preparation before your next drive.</p>
    <div class="cta-buttons">
      <a href="https://wa.me/919999999999?text=Hi%2C%20I%20want%20to%20start%20my%20CareerCraft%20session" class="whatsapp-btn" target="_blank">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        Start on WhatsApp
      </a>
      <a href="mailto:hello@careercraft.in" class="btn btn-primary">Get Placement Pack (₹299)</a>
    </div>
    <p style="font-size:13px;color:var(--muted);margin-top:20px;">Trusted by students from 50+ colleges across India · Pay via UPI in seconds</p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="container">
    <div class="footer-grid">
      <div>
        <div class="footer-logo">Career<span>Craft</span></div>
        <p class="footer-desc">AI-powered career readiness for India's 10 million annual graduates. Built by students, for students.</p>
        <div style="margin-top:20px;display:flex;gap:12px;">
          <a href="#" style="color:rgba(255,255,255,.4);font-size:20px;text-decoration:none;" aria-label="LinkedIn">in</a>
          <a href="#" style="color:rgba(255,255,255,.4);font-size:20px;text-decoration:none;" aria-label="Instagram">IG</a>
          <a href="#" style="color:rgba(255,255,255,.4);font-size:20px;text-decoration:none;" aria-label="WhatsApp">WA</a>
        </div>
      </div>
      <div class="footer-col">
        <h4>Product</h4>
        <ul>
          <li><a href="#features">Features</a></li>
          <li><a href="#pricing">Pricing</a></li>
          <li><a href="#compare">Comparison</a></li>
          <li><a href="#how">How it works</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Resources</h4>
        <ul>
          <li><a href="#">Interview Tips Blog</a></li>
          <li><a href="#">Resume Templates</a></li>
          <li><a href="#">Salary Guide 2025</a></li>
          <li><a href="#">Company Q Banks</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <ul>
          <li><a href="mailto:hello@careercraft.in">hello@careercraft.in</a></li>
          <li><a href="mailto:colleges@careercraft.in">colleges@careercraft.in</a></li>
          <li><a href="https://wa.me/919999999999">WhatsApp Us</a></li>
          <li><a href="#">Privacy Policy</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 CareerCraft. All rights reserved. Made with ❤️ for Bharat.</p>
      <p>CIN: [Pending Registration]</p>
    </div>
  </div>
</footer>

<script>
  // Navbar scroll
  window.addEventListener('scroll', () => {
    document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 40);
  });

  // Mobile menu
  function toggleMenu() {
    document.getElementById('mobileMenu').classList.toggle('open');
  }

  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // FAQ accordion
  function toggleFaq(btn) {
    const item = btn.closest('.faq-item');
    const isOpen = item.classList.contains('open');
    document.querySelectorAll('.faq-item').forEach(i => i.classList.remove('open'));
    if (!isOpen) item.classList.add('open');
  }
</script>
</body>
</html>
