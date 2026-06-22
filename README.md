
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>¿Quieres ser mi novia? 💕</title>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Lato:wght@300;400&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --rose:    #e8537a;
      --blush:   #f7a8be;
      --deep:    #1a0a10;
      --mid:     #2d1020;
      --gold:    #f9d776;
      --white:   #fff8f9;
    }

    body {
      min-height: 100vh;
      background: radial-gradient(ellipse at 50% 30%, #3a0d24 0%, var(--deep) 70%);
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Lato', sans-serif;
      overflow: hidden;
      position: relative;
    }

    .hearts-bg { position: fixed; inset: 0; pointer-events: none; z-index: 0; }
    .hb {
      position: absolute;
      font-size: 1.2rem;
      opacity: 0;
      animation: floatUp linear infinite;
    }
    @keyframes floatUp {
      0%   { opacity: 0; transform: translateY(0) scale(0.8); }
      10%  { opacity: 0.4; }
      90%  { opacity: 0.15; }
      100% { opacity: 0; transform: translateY(-100vh) scale(1.2); }
    }

    .card {
      position: relative;
      z-index: 10;
      background: linear-gradient(145deg, rgba(45,16,32,.92), rgba(26,10,16,.97));
      border: 1px solid rgba(232,83,122,.25);
      border-radius: 28px;
      padding: 3rem 3.5rem 3.5rem;
      max-width: 520px;
      width: 90vw;
      text-align: center;
      box-shadow: 0 0 60px rgba(232,83,122,.15), 0 0 120px rgba(232,83,122,.06);
    }

    .emoji-top {
      font-size: 3.2rem;
      display: block;
      margin-bottom: 1rem;
      animation: pulse 2s ease-in-out infinite;
    }
    @keyframes pulse {
      0%,100% { transform: scale(1); }
      50%      { transform: scale(1.12); }
    }

    h1 {
      font-family: 'Dancing Script', cursive;
      font-size: clamp(2rem, 6vw, 3rem);
      color: var(--white);
      line-height: 1.25;
      margin-bottom: .6rem;
      text-shadow: 0 0 20px rgba(232,83,122,.6);
    }

    .subtitle {
      font-size: .9rem;
      color: var(--blush);
      letter-spacing: .08em;
      margin-bottom: 2.6rem;
      opacity: .75;
    }

    .btns { display: flex; gap: 1.2rem; justify-content: center; flex-wrap: wrap; }

    .btn {
      font-family: 'Dancing Script', cursive;
      font-size: 1.45rem;
      font-weight: 700;
      padding: .7rem 2.4rem;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      transition: transform .18s ease, box-shadow .18s ease;
    }
    .btn:hover { transform: scale(1.08); }
    .btn:active { transform: scale(.96); }

    .btn-yes {
      background: linear-gradient(135deg, var(--rose), #c0395a);
      color: #fff;
      box-shadow: 0 4px 24px rgba(232,83,122,.45);
    }
    .btn-yes:hover { box-shadow: 0 6px 32px rgba(232,83,122,.65); }

    .btn-no {
      background: transparent;
      color: var(--blush);
      border: 1.5px solid rgba(247,168,190,.35);
    }
    .btn-no:hover { border-color: var(--blush); background: rgba(247,168,190,.07); }

    .result {
      display: none;
      flex-direction: column;
      align-items: center;
      gap: 1rem;
    }
    .result.show { display: flex; }

    .result-emoji { font-size: 4rem; animation: popIn .5s cubic-bezier(.17,.67,.4,1.4) both; }
    @keyframes popIn {
      from { transform: scale(0) rotate(-20deg); opacity: 0; }
      to   { transform: scale(1) rotate(0deg);   opacity: 1; }
    }

    .result-title {
      font-family: 'Dancing Script', cursive;
      font-size: clamp(1.8rem, 5vw, 2.6rem);
      color: var(--white);
      text-shadow: 0 0 24px rgba(232,83,122,.7);
      text-align: center;
    }

    .result-sub {
      font-size: .95rem;
      color: var(--blush);
      opacity: .8;
      text-align: center;
    }

    .btn-back {
      margin-top: .8rem;
      font-size: .85rem;
      background: none;
      border: none;
      color: rgba(247,168,190,.45);
      cursor: pointer;
      text-decoration: underline;
      font-family: 'Lato', sans-serif;
    }
    .btn-back:hover { color: var(--blush); }

    canvas {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 5;
    }

    .broken-piece {
      position: fixed;
      pointer-events: none;
      font-size: 1.6rem;
      animation: fallDown linear forwards;
      z-index: 5;
    }
    @keyframes fallDown {
      0%   { opacity: 1; transform: translateY(0) rotate(0deg); }
      100% { opacity: 0; transform: translateY(100vh) rotate(360deg); }
    }
  </style>
</head>
<body>

<div class="hearts-bg" id="heartsBg"></div>
<canvas id="fw"></canvas>

<div class="card" id="card">

  <div id="question">
    <span class="emoji-top">💕</span>
    <h1>¿Quieres ser mi novia?</h1>
    <p class="subtitle">hay algo que quiero preguntarte…</p>
    <div class="btns">
      <button class="btn btn-yes" onclick="answer('yes')">Sí 🌹</button>
      <button class="btn btn-no"  onclick="answer('no')">No 💔</button>
    </div>
  </div>

  <div class="result" id="resYes">
    <span class="result-emoji">🥰</span>
    <p class="result-title">¡Sabía que dirías que sí!</p>
    <p class="result-sub">Eres la persona más especial de mi mundo ✨</p>
    <button class="btn-back" onclick="reset()">volver al inicio</button>
  </div>

  <div class="result" id="resNo">
    <span class="result-emoji">💔</span>
    <p class="result-title">Me rompiste el corazón…</p>
    <p class="result-sub">Esperaré el tiempo que sea necesario 🥀</p>
    <button class="btn-back" onclick="reset()">volver al inicio</button>
  </div>

</div>

<script>
/* Floating hearts */
const heartsBg = document.getElementById('heartsBg');
const HEART_CHARS = ['💕','💗','💓','✨','🌸','💖'];
for (let i = 0; i < 28; i++) {
  const h = document.createElement('span');
  h.className = 'hb';
  h.textContent = HEART_CHARS[Math.floor(Math.random() * HEART_CHARS.length)];
  h.style.left = Math.random() * 100 + '%';
  h.style.bottom = '-5%';
  h.style.animationDuration = (7 + Math.random() * 12) + 's';
  h.style.animationDelay = (Math.random() * 14) + 's';
  h.style.fontSize = (.6 + Math.random() * 1.2) + 'rem';
  heartsBg.appendChild(h);
}

/* Fireworks */
const canvas = document.getElementById('fw');
const ctx    = canvas.getContext('2d');
let W, H, particles = [], fwActive = false, fwTimer;

function resize() { W = canvas.width = innerWidth; H = canvas.height = innerHeight; }
resize(); addEventListener('resize', resize);

function randomColor() {
  const cols = ['#e8537a','#f9d776','#f7a8be','#ffffff','#a8d8f7','#a8f7c1','#f7a8f7'];
  return cols[Math.floor(Math.random() * cols.length)];
}

function burst(x, y) {
  const count = 90 + Math.random() * 40;
  for (let i = 0; i < count; i++) {
    const angle = (Math.PI * 2 * i) / count + (Math.random() - .5) * .4;
    const speed = 2 + Math.random() * 6;
    particles.push({
      x, y,
      vx: Math.cos(angle) * speed,
      vy: Math.sin(angle) * speed,
      alpha: 1,
      color: randomColor(),
      radius: 2 + Math.random() * 2.5,
      tail: []
    });
  }
}

function launchRandom() {
  if (!fwActive) return;
  burst(W * (.15 + Math.random() * .7), H * (.1 + Math.random() * .55));
  fwTimer = setTimeout(launchRandom, 400 + Math.random() * 700);
}

function stopFireworks() {
  fwActive = false;
  clearTimeout(fwTimer);
  particles = [];
}

function animateFW() {
  requestAnimationFrame(animateFW);
  if (!fwActive && particles.length === 0) { ctx.clearRect(0,0,W,H); return; }
  ctx.fillStyle = 'rgba(26,10,16,.18)';
  ctx.fillRect(0,0,W,H);
  particles = particles.filter(p => p.alpha > .01);
  particles.forEach(p => {
    p.tail.push({x: p.x, y: p.y, a: p.alpha});
    if (p.tail.length > 7) p.tail.shift();
    p.tail.forEach((t, i) => {
      ctx.globalAlpha = t.a * (i / p.tail.length) * .35;
      ctx.beginPath();
      ctx.arc(t.x, t.y, p.radius * .5, 0, Math.PI*2);
      ctx.fillStyle = p.color;
      ctx.fill();
    });
    ctx.globalAlpha = p.alpha;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.radius, 0, Math.PI*2);
    ctx.fillStyle = p.color;
    ctx.fill();
    ctx.globalAlpha = 1;
    p.x  += p.vx;
    p.y  += p.vy;
    p.vy += .09;
    p.vx *= .97;
    p.vy *= .97;
    p.alpha -= .013;
  });
}
animateFW();

/* Broken heart rain */
function brokenHeartRain() {
  const pieces = ['💔','🖤','🥀','💧'];
  let count = 0;
  const iv = setInterval(() => {
    if (count++ > 60) { clearInterval(iv); return; }
    const el = document.createElement('span');
    el.className = 'broken-piece';
    el.textContent = pieces[Math.floor(Math.random() * pieces.length)];
    el.style.left = Math.random() * 100 + 'vw';
    el.style.top  = '-3rem';
    el.style.animationDuration = (2 + Math.random() * 3) + 's';
    el.style.animationDelay   = (Math.random() * 2) + 's';
    document.body.appendChild(el);
    el.addEventListener('animationend', () => el.remove());
  }, 80);
}

/* Answer handler */
function answer(choice) {
  document.getElementById('question').style.display = 'none';
  if (choice === 'yes') {
    document.getElementById('resYes').classList.add('show');
    fwActive = true;
    launchRandom();
    setTimeout(() => { burst(W*.3,H*.4); burst(W*.7,H*.35); burst(W*.5,H*.3); }, 100);
  } else {
    document.getElementById('resNo').classList.add('show');
    brokenHeartRain();
  }
}

function reset() {
  stopFireworks();
  document.getElementById('resYes').classList.remove('show');
  document.getElementById('resNo').classList.remove('show');
  document.getElementById('question').style.display = '';
}
</script>
</body>
</html>
```

Guárdalo como un archivo `.html` y ábrelo en cualquier navegador. ¡Suerte! 🌹
