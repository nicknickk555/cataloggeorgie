<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Quad Poster — Intro + Pages 22–25 (Fixed)</title>
  <script>
    window.MathJax = { tex: { tags: 'ams' } };
  </script>
  <script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
  <style>
    :root {
      --ink: #0b2a4a;
      --line: #1f4e79;
      --air: #9b59b6;
      --soil: #27ae60;
      --mid: #3498db;
      --text: #333;
      --card: #fff;
      --bg: #fafafa;
    }
    html, body { height: 100%; }
    body {
      font-family: Segoe UI, Helvetica, Arial, sans-serif;
      margin: 0; padding: 40px; color: var(--text);
      background: repeating-linear-gradient(to bottom, var(--bg), var(--bg) 118px, #f0f0f0 120px);
      background-position-y: 0;
      transition: background-position 1.2s ease;
    }

    .section { margin-bottom: 60px; position: relative; }
    .page-marker { position: absolute; top: -28px; right: 12px; font-size: 12px; color: #999; font-weight: 500; letter-spacing: 0.5px; }
    .title-block { text-align: center; margin-bottom: 24px; }
    .title-main { font-size: 26px; font-weight: 700; letter-spacing: 1px; color: var(--ink); text-shadow: 1px 1px 2px rgba(0,0,0,0.08); }
    .title-sub {
      font-size: 18px; font-weight: 500;
      background: linear-gradient(90deg, var(--ink), var(--line));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      margin-top: 4px;
    }
    .divider { height: 2px; background: linear-gradient(90deg, var(--line), var(--ink)); margin-top: 8px; }

    .card { background: var(--card); border: 1px solid #ddd; padding: 20px; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.08); }
    .block-title { display: flex; align-items: center; gap: 8px; font-weight: 600; color: var(--ink); margin: 10px 0 6px; }
    .icon { width: 14px; height: 14px; display: inline-block; border-radius: 2px; }
    .icon.soil { background: var(--soil); } .icon.air { background: var(--air); } .icon.ink { background: var(--ink); }

    ul { list-style: none; padding-left: 0; margin: 8px 0 12px; }
    li { margin: 6px 0; }
    .bullet { display: inline-block; width: 0.75em; height: 0.75em; border-radius: 2px; margin-right: 8px; vertical-align: middle; }
    .bullet.soil { background: var(--soil); } .bullet.air { background: var(--air); } .bullet.ink { background: var(--ink); } .bullet.mid { background: var(--mid); }

    .formula { text-align: center; margin: 12px 0 16px; font-size: 16px; color: var(--ink); }
    .subnote { text-align: center; font-size: 12px; color: #586b80; margin-top: -6px; }

    .footer-epigraph { margin-top: 20px; text-align: center; }
    .footer-epigraph em { color: #0f5a3b; font-size: 16px; font-weight: 700; letter-spacing: 1px; }

    .var-soil { color: var(--soil); font-weight: 600; }
    .var-air { color: var(--air); font-weight: 600; }
    .var-ink { color: var(--ink); font-weight: 600; }

    .intro-logo { display: inline-block; margin-bottom: 16px; filter: drop-shadow(0 2px 4px rgba(0,0,0,0.08)); }

    /* Page24 controls */
    .controls { display: grid; grid-template-columns: repeat(3, minmax(180px, 1fr)); gap: 10px 16px; margin-bottom: 12px; }
    .controls label { font-size: 12px; color: var(--ink); display: flex; align-items: center; gap: 8px; }
    .controls input { flex: 1; padding: 6px 8px; border: 1px solid #ccd6e0; border-radius: 6px; font-size: 12px; color: var(--text); }
    .btn {
      display: inline-block; padding: 8px 12px; margin: 10px 0 6px;
      background: linear-gradient(90deg, var(--line), var(--ink));
      color: #fff; border: none; border-radius: 6px; cursor: pointer; font-size: 13px; font-weight: 600;
    }
    .legend { font-size: 12px; color: var(--ink); background: #f7fbff; border: 1px solid #d0e4f2; border-radius: 6px; padding: 8px 10px; width: fit-content; margin-top: 6px; }
    .legend-item { display: flex; align-items: center; gap: 8px; margin: 4px 0; }
    .dot { width: 8px; height: 8px; border-radius: 50%; }
    .dot.soil { background: var(--soil); } .dot.mid { background: var(--mid); } .dot.air { background: var(--air); }
    pre#output { background:#f7f9fc; border:1px solid #e3edf7; border-radius:6px; padding:8px; font-size:12px; color:#2b3f55; }

    /* Fade-in */
    .fade-in { opacity: 0; transform: translateY(20px); animation: fadeInUp 1.2s ease-out forwards; }
    .delay-1 { animation-delay: 0.2s; } .delay-2 { animation-delay: 0.8s; } .delay-3 { animation-delay: 1.2s; } .delay-4 { animation-delay: 1.6s; }
    @keyframes fadeInUp { to { opacity: 1; transform: translateY(0); } }

    /* Overlay and intro fade-out */
    #overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 100; opacity: 0; pointer-events: none; transition: opacity 0.8s ease; }
    #overlay.visible { opacity: 1; pointer-events: auto; }
    #intro { position: relative; z-index: 101; transition: opacity 1.2s ease, transform 1.2s ease; }
    #intro.fade-out { opacity: 0; transform: translateY(-40px); pointer-events: none; }

    /* Music tiny UI */
    #musicStatus {
      position: fixed; left: 12px; bottom: 12px; background: rgba(15,30,45,0.75); color: #eaf3ff;
      padding: 6px 10px; border-radius: 8px; font-size: 12px; z-index: 200; backdrop-filter: blur(4px);
    }
  </style>
</head>
<body>

<!-- Overlay -->
<div id="overlay" aria-hidden="true"></div>

<!-- Intro -->
<div class="section fade-in delay-1" id="intro">
  <div class="page-marker">Intro</div>
  <div class="title-block">
    <div class="intro-logo">
      <svg width="92" height="46" viewBox="0 0 92 46" aria-label="Intro logo">
        <circle cx="36" cy="23" r="16" fill="#27ae60" opacity="0.85"/>
        <circle cx="56" cy="23" r="16" fill="#9b59b6" opacity="0.85"/>
      </svg>
    </div>
    <div class="title-main">Moisture Gradient and Pruning Point</div>
    <div class="title-sub">Quad poster — Intro to Pages 22–25</div>
    <div class="divider"></div>
  </div>
  <div class="footer-epigraph">
    <em>⚖️ “Geometry reshapes resistance — Venturi flow decides pruning.”</em><br>
    <button class="btn" onclick="enterExhibit()">Enter the exhibit</button>
  </div>
</div>

<!-- Page 22 -->
<div class="section fade-in delay-2" id="page22">
  <div class="page-marker">Page 22</div>
  <div class="title-block">
    <div class="title-main">Page 22 — Initial Parameters</div>
    <div class="title-sub">Moisture, geometry, and fill conditions</div>
    <div class="divider"></div>
  </div>
  <div class="card">
    <div class="block-title"><span class="icon ink"></span>Starting conditions</div>
    <ul>
      <li><span class="bullet ink"></span>\(C(0),\, C_\infty,\, C_{\text{crit}}\) — concentration values</li>
      <li><span class="bullet ink"></span>\(L,\, \ell_f\) — generatrix length and fill length</li>
      <li><span class="bullet soil"></span>\(D_p,\, A_p\) — porous compost parameters</li>
      <li><span class="bullet air"></span>\(D_a^{\mathrm{eff}},\, A_a,\, k_g,\, A_h\) — air gap and transfer area</li>
    </ul>

    <div class="block-title"><span class="icon ink"></span>Coordinates and regions</div>
    <ul>
      <li><span class="bullet ink"></span>Coordinate: \(s \in (0,L)\)</li>
      <li><span class="bullet ink"></span>Fill fraction: \(\ell_f = f\,L\), for \(f \in \{0,\,0.5,\,0.75\}\)</li>
      <li><span class="bullet soil"></span>Porous compost: \(s \in [0,\ell_f]\) with \(D_p,\, A_p\)</li>
      <li><span class="bullet air"></span>Air gap: \(s \in [\ell_f, L]\) with \(D_a^{\mathrm{eff}},\, A_a\)</li>
    </ul>

    <div class="block-title"><span class="icon ink"></span>Flow calculation</div>
    <div class="formula">
      

\[
      J = -D\,\frac{dC}{ds},\quad C(s)\ \text{continuous}
      \]


      

\[
      R_p = \frac{\ell_f}{D_p\,A_p},\quad
      R_a = \frac{L-\ell_f}{D_a^{\mathrm{eff}}\,A_a},\quad
      R_h = \frac{1}{k_g\,A_h}
      \]


      

\[
      R_{\text{tot}} = R_p + R_a + R_h,\quad
      J = \frac{C(0) - C_\infty}{R_{\text{tot}}}
      \]


    </div>
  </div>
</div>

<!-- Page 23 -->
<div class="section fade-in delay-3" id="page23">
  <div class="page-marker">Page 23</div>
  <div class="title-block">
    <div class="title-main">Page 23 — Flow and pruning point</div>
    <div class="title-sub">Resistance balance and root cutoff</div>
    <div class="divider"></div>
  </div>
  <div class="card">
    <div class="block-title"><span class="icon ink"></span>Flow</div>
    <div class="formula">
      

\[
      J = \frac{C(0) - C_\infty}{R_p + R_a + R_h}
      \]


    </div>

    <div class="block-title"><span class="icon ink"></span>Pruning point \(s^\*\)</div>
    <ul>
      <li>
        <span class="bullet soil"></span><strong class="var-soil">Inside compost:</strong>
        

\[
          s^\* = \frac{\big(C(0) - C_{\text{crit}}\big)\,D_p\,A_p}{J},\quad s^\* \le \ell_f
        \]


      </li>
      <li>
        <span class="bullet air"></span><strong class="var-air">Inside air gap:</strong>
        

\[
          s^\* = \ell_f + \frac{\big(C(0) - C_{\text{crit}} - J\,R_p\big)\,D_a^{\mathrm{eff}}\,A_a}{J},\quad s^\* \ge \ell_f
        \]


      </li>
    </ul>
  </div>
</div>

<!-- Page 24 -->
<div class="section fade-in delay-4" id="page24">
  <div class="page-marker">Page 24</div>
  <div class="title-block">
    <div class="title-main">Page 24 — Moisture Gradient and Pruning Point</div>
    <div class="title-sub">Three scenarios — qualitative outcome</div>
    <div class="divider"></div>
  </div>

  <div class="card">
    <div class="block-title"><span class="icon ink"></span>Scenarios</div>
    <ul>
      <li><span class="bullet soil"></span><strong>0% fill:</strong> only \(R_a+R_h\); linear drop across air; pruning near outlet.</li>
      <li><span class="bullet mid"></span><strong>50% fill:</strong> balanced \(R_p, R_a, R_h\); pruning near compost–air interface.</li>
      <li><span class="bullet air"></span><strong>75% fill:</strong> dominant \(R_p\); slow decline; pruning shifts outward.</li>
    </ul>

    <div class="formula">
      

\[
      s^\* = \begin{cases}
      \dfrac{(C(0) - C_{\mathrm{crit}})\,D_p\,A_p}{J}, & s^\* \le \ell_f \\
      \ell_f + \dfrac{(C(0) - C_{\mathrm{crit}} - J\,R_p)\,D_a^{\mathrm{eff}}\,A_a}{J}, & s^\* > \ell_f
      \end{cases}
      \]


    </div>                                                                                                                                                                                            <!-- Page24 -->
<div class="section fade-in" id="page24">
  <div class="page-marker">Page 24</div>
  <div class="title-block"><div class="title-main">Page 24 — Moisture Gradient and Pruning Point</div></div>
  <div class="card">
    <div class="controls">
      <label>L (mm): <input id="L" type="number" step="0.1" value="20"></label>
      <label>k_g: <input id="kg" type="number" step="0.0001" value="0.001"></label>
      <label>A_h: <input id="Ah" type="number" step="0.1" value="1"></label>
      <label>C(0): <input id="C0" type="number" step="0.001" value="0.02"></label>
      <label>C∞: <input id="Cinf" type="number" step="0.001" value="0.005"></label>
      <label>Ccrit: <input id="Ccrit" type="number" step="0.001" value="0.01"></label>
      <label>D_p: <input id="Dp" type="number" step="1e-7" value="0.000002"></label>
      <label>D_a^eff: <input id="Da" type="number" step="1e-7" value="0.00001"></label>
      <label>A_p: <input id="Ap" type="number" step="0.1" value="1"></label>
      <label>A_a: <input id="Aa" type="number" step="0.1" value="1"></label>
    </div>
    <button class="btn" onclick="compute()">Compute & Update Graph</button>
    <svg id="chart" viewBox="0 0

       <div class="legend">
      <div class="legend-item"><span class="dot soil"></span> 0% fill — air gap only</div>
      <div class="legend-item"><span class="dot mid"></span> 50% fill — compost + air</div>
      <div class="legend-item"><span class="dot air"></span> 75% fill — long compost</div>
    </div>

    <svg id="chart" viewBox="0 0 640 240" width="100%" height="240" aria-label="Moisture gradient and pruning point">
      <!-- Axes -->
      <line x1="60" y1="200" x2="600" y2="200" stroke="#0b2a4a"/>
      <line x1="60" y1="30"  x2="60"  y2="200" stroke="#0b2a4a"/>
      <text x="605" y="205" font-size="12" fill="#0b2a4a">s</text>
      <text x="20" y="32" font-size="12" fill="#0b2a4a" transform="rotate(-90 20,32)">C(s)</text>

      <!-- Threshold -->
      <line x1="60" y1="120" x2="600" y2="120" stroke="#e67e22" stroke-dasharray="6 4" stroke-width="2"/>
      <text x="66" y="112" font-size="12" fill="#e67e22">Ccrit</text>

      <!-- Profiles -->
      <polyline id="profile0"  fill="none" stroke="#27ae60" stroke-width="3"/>
      <polyline id="profile50" fill="none" stroke="#3498db" stroke-width="3"/>
      <polyline id="profile75" fill="none" stroke="#9b59b6" stroke-width="3"/>

      <!-- Markers -->
      <circle id="marker0"  r="5" fill="#27ae60" stroke="#0b2a4a"/>
      <circle id="marker50" r="5" fill="#3498db" stroke="#0b2a4a"/>
      <circle id="marker75" r="5" fill="#9b59b6" stroke="#0b2a4a"/>
    </svg>

    <pre id="output"></pre>
  </div>
</div>

<!-- Page 25 -->
<div class="section fade-in delay-4" id="page25">
  <div class="page-marker">Page 25</div>
  <div class="title-block">
    <div class="title-main">Page 25 — Main conclusion</div>
    <div class="title-sub">Influence of new bevel geometry</div>
    <div class="divider"></div>
  </div>
  <div class="card">

    <!-- SVG scheme (transparent background) -->
    <svg viewBox="0 0 600 200" width="100%" height="200" aria-label="Bevel geometry scheme">
      <!-- No background rect -->
      <!-- Optional: soft shadow filter -->
      <defs>
        <filter id="shadow" x="-20%" y="-20%" width="140%" height="140%">
          <feDropShadow dx="1" dy="1" stdDeviation="2" flood-color="#999"/>
        </filter>
      </defs>

      <!-- Cone outlines -->
      <polyline points="40,160 160,120 300,120 520,160" fill="none" stroke="#1f4e79" stroke-width="2" filter="url(#shadow)"/>
      <polyline points="60,160 180,130 300,130 500,160" fill="none" stroke="#6c7a89" stroke-width="1.5" stroke-dasharray="4 3"/>

      <!-- Shelf -->
      <rect x="160" y="120" width="140" height="10" fill="#27ae60" opacity="0.25"/>
      <text x="162" y="115" font-size="12" fill="#27ae60">🟩 Shelf → ℓf ↑</text>

      <!-- Venturi -->
      <path d="M300,120 C360,120 380,145 520,160" fill="none" stroke="#9b59b6" stroke-width="2"/>
      <text x="360" y="95" font-size="12" fill="#9b59b6">🟪 Venturi → u_eff ↑, k_g ↑, D_a^eff ↑</text>

      <!-- Rp ↑ -->
      <line x1="220" y1="105" x2="220" y2="85" stroke="#27ae60" stroke-width="2"/>
      <polygon points="220,80 215,88 225,88" fill="#27ae60"/>
      <text x="230" y="92" font-size="12" fill="#27ae60">R_p ↑</text>

      <!-- R_a ↓ -->
      <line x1="410" y1="115" x2="410" y2="135" stroke="#9b59b6" stroke-width="2"/>
      <polygon points="410,140 405,132 415,132" fill="#9b59b6"/>
      <text x="420" y="135" font-size="12" fill="#9b59b6">R_a ↓</text>

      <!-- R_h ↓ -->
      <line x1="450" y1="115" x2="450" y2="135" stroke="#9b59b6" stroke-width="2"/>
      <polygon points="450,140 445,132 455,132" fill="#9b59b6"/>
      <text x="470" y="135" font-size="12" fill="#9b59b6">R_h ↓</text>

      <!-- Balance bar -->
      <rect x="240" y="160" width="160" height="8" fill="#d0e4f2" stroke="#1f4e79" stroke-width="0.5"/>
      <rect x="240" y="160" width="70" height="8" fill="#27ae60"/>
      <rect x="330" y="160" width="70" height="8" fill="#9b59b6"/>
      <text x="240" y="178" font-size="11" fill="#3e5d79">⚖️ Balance: R_p ↑ vs R_a,R_h ↓ → decides s*</text>
    </svg>

    <ul>
      <li><span class="bullet soil"></span><strong class="var-soil">Local shelf effect:</strong> increases fill length \(\ell_f\) → thicker porous zone → larger \(R_p\).</li>
      <li><span class="bullet air"></span><strong class="var-air">Venturi acceleration:</strong> narrows and speeds up flow → raises \(k_g\) and \(D_a^{\mathrm{eff}}\) approximately proportional to \(u_{\mathrm{eff}}\).</li>
      <li><span class="bullet ink"></span><em>Resulting balance:</em> horizontal sections simplify filling but increase \(R_p\). Venturi acceleration reduces “air” resistances \(R_a,\,R_h\). The balance determines the pruning location \(s^\*\).</li>
    </ul>

    <div class="formula">
      

\[
      Sh = \frac{k_g\,\ell}{D_a} \sim a\,\mathrm{Re}^{m}\,\mathrm{Sc}^{1/3},\quad
      u_{\mathrm{eff}} \approx \frac{u_0}{\cos\theta}
      \]


    </div>
    <div class="subnote">
      Air‑side transfer dominance: <span class="var-air">\(k_g, D_a^{\mathrm{eff}}\)</span>. Porous‑side dominance: <span class="var-soil">\(R_p\)</span>.
    </div>

    <div class="footer-epigraph">
      <div style="height:2px; background:linear-gradient(90deg,var(--ink),var(--line)); margin-bottom:8px;"></div>
      <em>⚖️ “Geometry reshapes resistance — Venturi flow decides pruning.”</em>
      <div style="height:2px; background:linear-gradient(90deg,var(--line),var(--ink)); margin-top:8px;"></div>
    </div>
  </div>
</div>

<!-- Music (optional, replace src if needed) -->
<audio id="introMusic" src="intro.mp3" preload="auto"></audio>
<div id="musicStatus" aria-live="polite">Sound: off</div>

<script>
// Flexible getter: tries multiple ids, returns parsed float or default
function val(ids, def=0) {
  const list = Array.isArray(ids) ? ids : [ids];
  for (const id of list) {
    const el = document.getElementById(id);
    if (el && el.value !== '') {
      const num = parseFloat(el.value);
      if (!Number.isNaN(num)) return num;
    }
  }
  return def;
}

function enterExhibit() {
  const overlay = document.getElementById('overlay');
  const intro = document.getElementById('intro');
  overlay.classList.add('visible');
  intro.classList.add('fade-out');

  // Shift background grid (hall entry effect)
  document.body.style.backgroundPositionY = '-80px';

  // Music fade-in
  const audio = document.getElementById('introMusic');
  const status = document.getElementById('musicStatus');
  try {
    audio.volume = 0;
    audio.play().then(()=>{
      status.textContent = 'Sound: on';
      let v = 0;
      const step = setInterval(()=>{
        v += 0.05;
        audio.volume = Math.min(v, 0.6);
        if (v >= 0.6) clearInterval(step);
      }, 120);
    }).catch(()=>{
      status.textContent = 'Sound: click allowed';
    });
  } catch(e) {
    status.textContent = 'Sound: click allowed';
  }

  // Remove overlay and trigger page animations
  setTimeout(() => {
    overlay.classList.remove('visible');
    document.getElementById('page22').style.animationDelay = '0s';
    document.getElementById('page23').style.animationDelay = '0.2s';
    document.getElementById('page24').style.animationDelay = '0.4s';
    document.getElementById('page25').style.animationDelay = '0.6s';
  }, 900);
}

// Page24 compute logic (robust to mixed id names)
function compute() {
  const C0    = val(['C0']);
  const Cinf  = val(['Cinf']);
  const Ccrit = val(['Ccrit']);
  const L     = val(['L']);

  // Accept alternate ids from your UI (photos)
  const Dp    = val(['Dp','D_g']);
  const Da    = val(['Da','D_ap^eff','D_a^eff']);
  const kg    = val(['kg','K_sg']);
  const Ap    = val(['Ap','A_p']);
  const Aa    = val(['Aa','A_ac','A_a']);
  const Ah    = val(['Ah','A_h','A_h_alt']);

  // Guards
  const DpSafe = Dp > 0 ? Dp : 1e-9;
  const DaSafe = Da > 0 ? Da : 1e-9;
  const kgSafe = kg > 0 ? kg : 1e-9;
  const ApSafe = Ap > 0 ? Ap : 1e-9;
  const AaSafe = Aa > 0 ? Aa : 1e-9;
  const AhSafe = Ah > 0 ? Ah : 1e-9;
  const LSafe  = L  > 0 ? L  : 1;

  const fills   = [0, 0.5, 0.75];
  const ids     = ["marker0","marker50","marker75"];
  const profIds = ["profile0","profile50","profile75"];
  let results = "";

  fills.forEach((f,i)=>{
    const lf = f * LSafe;

    const Rp = (lf > 0) ? lf / (DpSafe * ApSafe) : 0;
    const Ra = (LSafe - lf) / (DaSafe * AaSafe);
    const Rh = 1 / (kgSafe * AhSafe);
    const Rtot = Rp + Ra + Rh;

    const J = (C0 - Cinf) / (Rtot > 0 ? Rtot : 1e-9);

    // Build piecewise-linear profile
    const pts = [];
    let step = lf > 0 ? lf/5 : 0;
    for (let s=0; s<=lf; s += (step || lf)) {
      const C = C0 - (J / (DpSafe * ApSafe)) * s;
      const x = 60 + (s / LSafe) * 540;
      const y = 200 - (C / C0) * 140;
      pts.push(`${x},${y}`);
      if (step === 0) break;
    }
    step = (LSafe - lf)/5;
    for (let s=lf; s<=LSafe; s+=step) {
      const C = (C0 - J * Rp) - (J / (DaSafe * AaSafe)) * (s - lf);
      const x = 60 + (s / LSafe) * 540;
      const y = 200 - (C / C0) * 140;
      pts.push(`${x},${y}`);
    }
    const poly = document.getElementById(profIds[i]);
    if (poly) poly.setAttribute("points", pts.join(" "));

    // Pruning point s*
    const scomp = (C0 - Ccrit) * DpSafe * ApSafe / (J || 1e-9);
    let sstar;
    if (scomp <= lf) {
      sstar = scomp;
    } else {
      sstar = lf + (C0 - Ccrit - J * Rp) * DaSafe * AaSafe / (J || 1e-9);
    }
    const x = 60 + (sstar / LSafe) * 540;
    const y = 120;

    const mk = document.getElementById(ids[i]);
    if (mk) {
      mk.setAttribute("cx", x);
      mk.setAttribute("cy", y);
    }

    results += `Fill ${Math.round(f*100)}%: s* = ${sstar.toFixed(2)} mm\n`;
  });

  const out = document.getElementById('output');
  if (out) out.textContent = results;
}

// Initialize graph
compute();
</script>

</body>
</html>
