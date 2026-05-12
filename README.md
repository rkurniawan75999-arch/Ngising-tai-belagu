<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cek Bau</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #0a0a0f;
    font-family: 'Cormorant Garamond', serif;
    overflow: hidden;
  }

  /* Animated background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 60% 50% at 30% 40%, rgba(180, 120, 60, 0.08) 0%, transparent 70%),
      radial-gradient(ellipse 50% 60% at 70% 60%, rgba(100, 60, 20, 0.06) 0%, transparent 70%);
    z-index: 0;
    animation: bgPulse 6s ease-in-out infinite alternate;
  }

  @keyframes bgPulse {
    from { opacity: 0.6; }
    to   { opacity: 1; }
  }

  /* Floating particles */
  .particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
  }
  .particle {
    position: absolute;
    width: 2px;
    height: 2px;
    background: rgba(210, 160, 80, 0.3);
    border-radius: 50%;
    animation: float linear infinite;
  }
  @keyframes float {
    0%   { transform: translateY(100vh) translateX(0); opacity: 0; }
    10%  { opacity: 1; }
    90%  { opacity: 0.5; }
    100% { transform: translateY(-10vh) translateX(40px); opacity: 0; }
  }

  /* Card wrapper */
  .scene {
    position: relative;
    z-index: 1;
    perspective: 1000px;
  }

  .card {
    width: 360px;
    background: linear-gradient(145deg, #13100d, #1c1610, #0e0c09);
    border: 1px solid rgba(210, 160, 80, 0.25);
    border-radius: 4px;
    padding: 48px 40px 44px;
    position: relative;
    box-shadow:
      0 0 0 1px rgba(210, 160, 80, 0.06),
      0 8px 40px rgba(0, 0, 0, 0.7),
      0 2px 8px rgba(0, 0, 0, 0.5),
      inset 0 1px 0 rgba(210, 160, 80, 0.12);
    animation: cardReveal 1s cubic-bezier(0.16, 1, 0.3, 1) both;
    transform-style: preserve-3d;
  }

  @keyframes cardReveal {
    from { opacity: 0; transform: translateY(30px) rotateX(8deg); }
    to   { opacity: 1; transform: translateY(0) rotateX(0deg); }
  }

  /* Corner ornaments */
  .card::before, .card::after {
    content: '';
    position: absolute;
    width: 18px;
    height: 18px;
    border-color: rgba(210, 160, 80, 0.5);
    border-style: solid;
  }
  .card::before { top: 12px; left: 12px; border-width: 1px 0 0 1px; }
  .card::after  { bottom: 12px; right: 12px; border-width: 0 1px 1px 0; }

  .corner-br::before, .corner-br::after {
    content: '';
    position: absolute;
    width: 18px;
    height: 18px;
    border-color: rgba(210, 160, 80, 0.5);
    border-style: solid;
  }
  .corner-br::before { top: 12px; right: 12px; border-width: 1px 1px 0 0; }
  .corner-br::after  { bottom: 12px; left: 12px; border-width: 0 0 1px 1px; }

  /* Phase 1: Big Title */
  .phase-1 {
    text-align: center;
    animation: phaseIn 0.8s 0.3s cubic-bezier(0.16, 1, 0.3, 1) both;
  }

  .big-title {
    font-family: 'Cinzel Decorative', cursive;
    font-size: 2.6rem;
    font-weight: 700;
    color: #d4a044;
    letter-spacing: 0.12em;
    line-height: 1.1;
    text-shadow:
      0 0 30px rgba(212, 160, 68, 0.4),
      0 0 60px rgba(212, 160, 68, 0.15);
    animation: titleGlow 3s ease-in-out infinite alternate;
  }

  @keyframes titleGlow {
    from { text-shadow: 0 0 20px rgba(212, 160, 68, 0.3), 0 0 40px rgba(212, 160, 68, 0.1); }
    to   { text-shadow: 0 0 40px rgba(212, 160, 68, 0.6), 0 0 80px rgba(212, 160, 68, 0.25); }
  }

  /* Divider */
  .divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 28px 0 26px;
    animation: phaseIn 0.8s 0.5s cubic-bezier(0.16, 1, 0.3, 1) both;
  }
  .divider-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(210, 160, 80, 0.5), transparent);
  }
  .divider-icon {
    color: rgba(210, 160, 80, 0.7);
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
  }

  /* Phase 2: Result card */
  .phase-2 {
    animation: phaseIn 0.9s 0.7s cubic-bezier(0.16, 1, 0.3, 1) both;
  }

  @keyframes phaseIn {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .elegant-title {
    text-align: center;
    font-family: 'Cinzel Decorative', cursive;
    font-size: 0.62rem;
    letter-spacing: 0.35em;
    color: rgba(210, 160, 80, 0.55);
    text-transform: uppercase;
    margin-bottom: 20px;
  }

  .result-block {
    background: rgba(210, 160, 80, 0.04);
    border: 1px solid rgba(210, 160, 80, 0.15);
    border-radius: 2px;
    padding: 22px 24px;
    position: relative;
  }

  .result-block::before {
    content: '❧';
    position: absolute;
    top: -10px;
    left: 50%;
    transform: translateX(-50%);
    background: #13100d;
    padding: 0 8px;
    color: rgba(210, 160, 80, 0.5);
    font-size: 1rem;
  }

  .row {
    display: flex;
    align-items: baseline;
    gap: 10px;
    margin-bottom: 14px;
  }
  .row:last-child { margin-bottom: 0; }

  .label {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-weight: 300;
    font-size: 0.85rem;
    color: rgba(210, 160, 80, 0.55);
    min-width: 52px;
    letter-spacing: 0.05em;
  }

  .value {
    font-family: 'Cormorant Garamond', serif;
    font-weight: 400;
    font-size: 1.05rem;
    color: #e8d5a8;
    letter-spacing: 0.04em;
  }

  .value.result-text {
    font-size: 1.1rem;
    color: #c87941;
    font-style: italic;
    text-shadow: 0 0 20px rgba(200, 121, 65, 0.3);
  }

  .emoji {
    font-style: normal;
    filter: drop-shadow(0 0 6px rgba(200, 121, 65, 0.4));
  }

  /* Separator row */
  .row-sep {
    border-top: 1px solid rgba(210, 160, 80, 0.1);
    padding-top: 14px;
    margin-top: 14px;
  }

  /* Footer */
  .footer {
    margin-top: 26px;
    text-align: center;
    animation: phaseIn 0.8s 1s cubic-bezier(0.16, 1, 0.3, 1) both;
  }
  .footer-text {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-size: 0.72rem;
    color: rgba(210, 160, 80, 0.25);
    letter-spacing: 0.18em;
  }
</style>
</head>
<body>

<!-- Floating particles -->
<div class="particles" id="particles"></div>

<div class="scene">
  <div class="card corner-br">

    <!-- Phase 1: Judul besar -->
    <div class="phase-1">
      <div class="big-title">CEK BAU</div>
    </div>

    <!-- Divider -->
    <div class="divider">
      <div class="divider-line"></div>
      <div class="divider-icon">── 「 」 ──</div>
      <div class="divider-line"></div>
    </div>

    <!-- Phase 2: Detail hasil -->
    <div class="phase-2">
      <div class="elegant-title">Hasil Pemeriksaan</div>

      <div class="result-block">
        <div class="row">
          <span class="label">Nama</span>
          <span class="value">malz</span>
        </div>
        <div class="row row-sep">
          <span class="label">Hasil</span>
          <span class="value result-text">Bau Nggak Enak <span class="emoji">🤮</span></span>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <div class="footer">
      <div class="footer-text">~ verified by sistem ~</div>
    </div>

  </div>
</div>

<script>
  // Generate floating particles
  const container = document.getElementById('particles');
  for (let i = 0; i < 22; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.cssText = `
      left: ${Math.random() * 100}%;
      width: ${Math.random() * 2 + 1}px;
      height: ${Math.random() * 2 + 1}px;
      animation-duration: ${Math.random() * 12 + 10}s;
      animation-delay: ${Math.random() * 12}s;
      opacity: ${Math.random() * 0.4 + 0.1};
    `;
    container.appendChild(p);
  }
</script>
</body>
</html>
