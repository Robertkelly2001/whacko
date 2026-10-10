# whacko
same again whack a mole classic 

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no">
<meta name="theme-color" content="#6844da">
<title>Mole Mayhem!</title>
<style>
:root{
  --purple:#6844da;
  --dark:#30245c;
  --yellow:#ffdb58;
  --cream:#fff8df;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{
  margin:0;width:100%;height:100%;overflow:hidden;
  font-family:system-ui,-apple-system,"Segoe UI",sans-serif;
  user-select:none;-webkit-user-select:none;
  touch-action:none;
}
body{
  background:#6844da;
  display:flex;align-items:center;justify-content:center;
}
button,input{font:inherit}
button{cursor:pointer;touch-action:manipulation}
#app{
  position:relative;width:100%;max-width:520px;
  height:100vh;height:100dvh;overflow:hidden;
  background:linear-gradient(180deg,#8a65ff 0%,#bba0ff 49%,#86df8e 49%,#5fb96b 100%);
  isolation:isolate;
}
#app:before{
  content:"";position:absolute;inset:0;pointer-events:none;
  background:
    radial-gradient(circle at 14% 18%,#ffffff22 0 6%,transparent 6.3%),
    radial-gradient(circle at 83% 31%,#ffffff20 0 8%,transparent 8.3%);
}
.screen{
  position:absolute;inset:0;display:flex;
  flex-direction:column;align-items:center;justify-content:center;
  padding:24px;z-index:20;text-align:center;
  background:linear-gradient(155deg,#7953eced,#a576f1f2);
  transition:opacity .25s,visibility .25s;
}
.screen.hidden{
  opacity:0;visibility:hidden;pointer-events:none;
}
.logo{
  font-size:clamp(43px,12vw,69px);
  font-weight:1000;line-height:.96;letter-spacing:-3px;
  color:var(--yellow);
  text-shadow:0 5px 0 #c46d44,0 9px 0 #49327a;
  transform:rotate(-4deg);
  margin:12px 0 24px;
}
.subtitle{color:white;font-weight:800;font-size:18px;margin-bottom:22px}
.mascot{
  width:145px;height:145px;margin:0 auto 12px;
  display:grid;place-items:center;font-size:100px;
  border-radius:50%;background:#ffffff25;
  border:5px solid #ffffff65;
  animation:bob 2s ease-in-out infinite;
}
@keyframes bob{50%{transform:translateY(-9px) rotate(5deg)}}
.panel{
  width:100%;max-width:335px;border-radius:26px;
  background:var(--cream);padding:23px;
  box-shadow:0 10px 0 #4d2e91,0 20px 35px #2a125655;
}
.panel label{
  display:block;text-align:left;color:var(--dark);
  font-weight:900;font-size:13px;margin-bottom:9px;
  text-transform:uppercase;letter-spacing:1px;
}
input{
  display:block;width:100%;padding:15px;
  border:3px solid #ddd0f6;border-radius:13px;
  background:white;outline:none;color:var(--dark);
  font-size:18px;font-weight:800;
  user-select:text;-webkit-user-select:text;
  touch-action:manipulation;
}
input:focus{border-color:var(--purple)}
.main-btn{
  display:block;width:100%;margin-top:17px;
  background:#ffcf45;color:#4d2d52;
  border:0;border-bottom:6px solid #d89125;
  border-radius:17px;padding:17px 12px;
  font-size:23px;font-weight:1000;
  box-shadow:0 5px 15px #ffb52e45;
  transition:transform .1s;
}
.main-btn:active{transform:translateY(4px);border-bottom-width:2px}
.hint{font-size:12px;color:#70558e;margin-top:16px;line-height:1.5}
.best-line{margin-top:22px;color:white;font-size:16px;font-weight:800}
#game{position:absolute;inset:0;display:flex;flex-direction:column}
#hud{
  position:relative;z-index:5;padding:calc(env(safe-area-inset-top) + 12px) 15px 0;
}
.player-tag{
  text-align:center;color:white;font-weight:1000;
  font-size:15px;text-shadow:0 2px 3px #49327a;
  letter-spacing:1px;margin-bottom:10px;
}
.stats{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px}
.stat{
  background:#fff7df;border-radius:15px;
  padding:10px 5px 8px;text-align:center;
  box-shadow:0 5px 0 #5944a8;
  min-width:0;
}
.stat small{
  display:block;color:#80649d;font-size:10px;
  font-weight:1000;letter-spacing:1px;
}
.stat strong{
  display:block;font-size:clamp(23px,7vw,32px);
  color:var(--dark);font-weight:1000;line-height:1.2;
}
#timeValue.danger{color:#f04458;animation:pulse .5s infinite alternate}
@keyframes pulse{to{transform:scale(1.13)}}
.progress{
  height:10px;border-radius:15px;
  background:#ffffff55;margin-top:13px;overflow:hidden;
  border:2px solid #ffffff77;
}
#timeBar{
  height:100%;width:100%;background:var(--yellow);
  border-radius:15px;transition:width .1s linear;
}
#level{
  text-align:center;color:#fff;text-shadow:0 2px #5d3a9d;
  font-weight:900;font-size:13px;margin-top:9px;
}
#field{
  position:relative;flex:1;min-height:0;
  display:flex;align-items:center;justify-content:center;
  padding:14px 12px calc(env(safe-area-inset-bottom) + 22px);
}
#board{
  width:100%;max-width:450px;
  display:grid;grid-template-columns:repeat(3,minmax(0,1fr));
  gap:clamp(8px,2.5vw,16px);
  align-content:center;
  perspective:700px;
}
.hole{
  aspect-ratio:1/1.04;position:relative;
  cursor:pointer;touch-action:none;
  outline:none;
}
.hole:focus-visible{
  outline:3px solid white;outline-offset:3px;border-radius:18px;
}
.hole:before{
  content:"";position:absolute;left:3%;right:3%;
  bottom:3%;height:49%;border-radius:50%;
  background:#347942;box-shadow:0 6px 0 #2a6936;
}
.pit{
  position:absolute;bottom:7%;left:9%;width:82%;height:38%;
  border-radius:50%;
  background:radial-gradient(ellipse,#271934 20%,#43304e 65%,#674259);
  box-shadow:inset 0 8px 9px #170e28;
}
.mole-wrap{
  position:absolute;inset:0 0 15% 0;
  overflow:hidden;pointer-events:none;
  clip-path:inset(0 0 20% 0);
}
.mole{
  position:absolute;width:75%;height:74%;
  left:12.5%;bottom:-61%;
  transition:bottom .16s cubic-bezier(.22,1.5,.45,1);
  filter:drop-shadow(0 4px 1px #301e4666);
}
.hole.active .mole{bottom:3%}
.hole.hit .mole{bottom:-65%;transition:bottom .12s ease-in}
.ear{
  position:absolute;top:16%;width:30%;height:32%;
  border-radius:50%;background:#b8724c;border:4px solid #8d4a3a;
}
.ear.left{left:-8%}.ear.right{right:-8%}
.ear:after{
  content:"";position:absolute;inset:23%;background:#edab9a;border-radius:50%;
}
.head{
  position:absolute;inset:13% 1% 0;
  border-radius:49% 49% 37% 37%;
  background:linear-gradient(120deg,#b9774b,#9d583b);
  box-shadow:inset -9px -6px #7b4239;
}
.belly{
  position:absolute;left:21%;right:21%;bottom:0;height:46%;
  border-radius:45%;background:#eac395;
}
.eye{
  position:absolute;top:34%;width:10%;height:13%;
  background:#30243a;border-radius:50%;z-index:2;
}
.eye.left{left:28%}.eye.right{right:28%}
.eye:after{
  content:"";position:absolute;background:white;
  width:38%;height:38%;left:12%;top:12%;border-radius:50%;
}
.snout{
  position:absolute;top:49%;left:31%;width:38%;height:27%;
  background:#f2cbad;border-radius:50%;z-index:2;
}
.nose{
  position:absolute;top:9%;left:36%;width:28%;height:37%;
  background:#f4849f;border-radius:50%;
}
.tooth{
  position:absolute;bottom:0;left:42%;width:17%;height:31%;
  background:white;border-radius:0 0 4px 4px;
}
.mole.gold .head{
  background:linear-gradient(120deg,#ffe66b,#f9a925);
  box-shadow:inset -9px -6px #d48421;
}
.mole.gold .ear{background:#f9c64a;border-color:#d68b29}
.mole.gold .belly{background:#fff4bd}
.mole.gold .snout{background:#fff5da}
.mole.gold:after{
  content:"✦";position:absolute;top:-15%;right:0;
  color:#fff8ad;font-size:25px;animation:twinkle .45s infinite alternate;
}
@keyframes twinkle{to{transform:scale(1.4) rotate(30deg)}}
.rim{
  position:absolute;left:2%;right:2%;bottom:0;height:29%;
  border-radius:50%;
  border-bottom:clamp(9px,3vw,17px) solid #966042;
  background:linear-gradient(#bb8053,#a36c49);
  clip-path:inset(49% 0 0 0);
  pointer-events:none;
}
.grass{
  position:absolute;bottom:5%;height:13%;width:23%;
  background:#4fa95a;border-radius:90% 0 90% 0;
  pointer-events:none;
}
.grass.left{left:-3%;transform:rotate(16deg)}
.grass.right{right:-3%;transform:rotate(75deg)}
.pop{
  position:absolute;left:50%;top:10%;transform:translateX(-50%);
  color:#fff;font-weight:1000;font-size:24px;
  text-shadow:0 3px #422a7c;z-index:9;
  pointer-events:none;animation:scorePop .65s forwards;
  white-space:nowrap;
}
@keyframes scorePop{
  0%{opacity:0;transform:translate(-50%,15px) scale(.5)}
  30%{opacity:1;transform:translate(-50%,-10px) scale(1.2)}
  100%{opacity:0;transform:translate(-50%,-52px) scale(.85)}
}
.spark{
  position:absolute;left:50%;top:40%;height:8px;width:8px;
  border-radius:2px;background:var(--spark);
  pointer-events:none;z-index:10;
  animation:sparkFly .48s ease-out forwards;
}
@keyframes sparkFly{
  to{transform:translate(var(--dx),var(--dy)) rotate(210deg);opacity:0}
}
#combo{
  position:absolute;top:0;left:0;right:0;
  text-align:center;pointer-events:none;
  color:#fff037;text-shadow:0 3px #98533a;
  font-weight:1000;font-size:22px;opacity:0;
}
#combo.show{animation:comboPop .75s forwards}
@keyframes comboPop{
  0%{opacity:0;transform:scale(.5)}
  25%{opacity:1;transform:scale(1.15)}
  75%{opacity:1}
  100%{opacity:0;transform:translateY(-20px)}
}
#footer{
  position:absolute;bottom:calc(env(safe-area-inset-bottom) + 5px);
  width:100%;text-align:center;color:#ffffffdd;font-size:11px;
  font-weight:800;pointer-events:none;
}
.end-score{
  color:var(--dark);font-size:70px;font-weight:1000;
  line-height:1;margin:12px 0;
}
.end-best{font-weight:900;color:#8b65bd;font-size:19px}
.new-record{
  background:#ffe05e;border-radius:9px;padding:7px;
  color:#814b24;font-weight:1000;margin-top:12px;
}
#pauseBtn{
  position:absolute;right:14px;top:calc(env(safe-area-inset-top) + 16px);
  z-index:9;border:0;border-radius:50%;
  width:38px;height:38px;background:#ffffff55;color:white;
  font-size:20px;font-weight:900;
}
#pauseOverlay{background:#402979e8;z-index:14}
#pauseOverlay h2{color:white;font-size:39px;margin:10px}
@media(max-height:690px){
  .screen{padding:12px}
  .mascot{width:95px;height:95px;font-size:70px;margin-bottom:3px}
  .logo{font-size:43px;margin:8px 0 13px}
  .subtitle{margin-bottom:10px;font-size:15px}
  .panel{padding:15px}
  .main-btn{padding:12px}
  .best-line{margin-top:12px}
  #hud{padding-top:calc(env(safe-area-inset-top) + 6px)}
  .stat{padding:5px}
  .stat strong{font-size:24px}
  .progress{margin-top:8px}
  #level{margin-top:5px}
  #field{padding-top:4px}
  #board{max-width:min(380px,100%)}
}
@media(min-width:600px){
  #app{height:min(950px,100dvh);border-radius:24px;box-shadow:0 15px 60px #28175888}
}
@media(prefers-reduced-motion:reduce){
  .mascot{animation:none}
  .mole{transition-duration:.08s}
}
</style>
</head>
<body>
<div id="app">

  <!-- TITLE SCREEN -->
  <section id="titleScreen" class="screen">
    <div class="mascot" aria-hidden="true">🐹</div>
    <h1 class="logo">MOLE<br>MAYHEM!</h1>
    <div class="subtitle">THE ULTIMATE BACKYARD BASH</div>
    <div class="panel">
      <label for="nameInput">What's your first name?</label>
      <input id="nameInput" type="text" maxlength="18"
             placeholder="Enter your name" autocomplete="given-name">
      <button id="playBtn" class="main-btn">▶ PLAY NOW!</button>
      <div class="hint">
        Tap the moles before they vanish!<br>
        Golden moles = 3 points ⭐<br>
        Swipe to whack multiple targets!
      </div>
    </div>
    <div class="best-line">🏆 YOUR BEST: <span id="titleBest">0</span></div>
  </section>

  <!-- GAME -->
  <main id="game" aria-label="Whack a mole game">
    <button id="pauseBtn" aria-label="Pause game">Ⅱ</button>
    <header id="hud">
      <div class="player-tag">🌟 <span id="playerName">PLAYER</span>'S GARDEN 🌟</div>
      <div class="stats">
        <div class="stat"><small>SCORE</small><strong id="scoreValue">0</strong></div>
        <div class="stat"><small>TIME</small><strong id="timeValue">45</strong></div>
        <div class="stat"><small>BEST</small><strong id="bestValue">0</strong></div>
      </div>
      <div class="progress"><div id="timeBar"></div></div>
      <div id="level">LEVEL 1 • WARM UP</div>
    </header>
    <div id="field">
      <div id="combo"></div>
      <div id="board" aria-label="Nine mole holes"></div>
    </div>
    <div id="footer">TAP • SWIPE • OR PRESS KEYS 1–9</div>
  </main>

  <!-- PAUSE -->
  <section id="pauseOverlay" class="screen hidden">
    <div class="mascot">💤</div>
    <h2>PAUSED!</h2>
    <p style="color:white;font-weight:700">
      The moles are taking a breather...
    </p>
    <div style="width:100%;max-width:290px">
      <button id="resumeBtn" class="main-btn">▶ RESUME</button>
    </div>
  </section>

  <!-- GAME OVER -->
  <section id="gameOver" class="screen hidden">
    <div class="mascot">🏆</div>
    <h1 class="logo">TIME'S<br>UP!</h1>
    <div class="panel">
      <div id="endMessage" style="font-weight:900;color:#6844da">
        AMAZING WHACKING!
      </div>
      <div class="end-score" id="finalScore">0</div>
      <div style="font-size:13px;color:#856c9c;font-weight:900">TOTAL POINTS</div>
      <div class="end-best">🏆 BEST: <span id="finalBest">0</span></div>
      <div id="newRecord" class="new-record" hidden>🎉 NEW PERSONAL BEST! 🎉</div>
      <button id="againBtn" class="main-btn">↻ PLAY AGAIN!</button>
      <button id="menuBtn" style="border:0;background:none;color:#7655b2;font-weight:900;margin-top:15px;padding:8px">
        BACK TO MENU
      </button>
    </div>
  </section>

</div>

<script>
"use strict";

(() => {
  const $ = id => document.getElementById(id);
  const GAME_LENGTH = 45;
  const BEST_KEY = "moleMayhemBestV1";
  const NAME_KEY = "moleMayhemNameV1";

  let score = 0;
  let best = 0;
  let combo = 0;
  let timeLeft = GAME_LENGTH;
  let elapsed = 0;
  let level = 1;
  let running = false;
  let paused = false;
  let lastFrame = 0;
  let nextSpawn = 0;
  let audioCtx = null;
  let player = "PLAYER";
  let pointerHeld = false;
  const holes = [];
  const pointerHits = new Set();

  function stored(key, fallback) {
    try { return localStorage.getItem(key) ?? fallback; }
    catch { return fallback; }
  }
  function save(key, value) {
    try { localStorage.setItem(key, String(value)); }
    catch {}
  }

  best = Math.max(0, Number(stored(BEST_KEY, "0")) || 0);
  $("titleBest").textContent = best;
  $("bestValue").textContent = best;
  $("nameInput").value = stored(NAME_KEY, "");

  // Procedurally generated cute mole illustrations.
  function moleHTML() {
    return `
      <div class="mole-wrap">
        <div class="mole">
          <div class="ear left"></div>
          <div class="ear right"></div>
          <div class="head"></div>
          <div class="belly"></div>
          <div class="eye left"></div>
          <div class="eye right"></div>
          <div class="snout">
            <div class="nose"></div>
            <div class="tooth"></div>
          </div>
        </div>
      </div>`;
  }

  const board = $("board");
  for (let i = 0; i < 9; i++) {
    const el = document.createElement("div");
    el.className = "hole";
    el.tabIndex = 0;
    el.setAttribute("role", "button");
    el.setAttribute("aria-label", `Hole ${i + 1}`);
    el.innerHTML = `
      <div class="pit"></div>
      ${moleHTML()}
      <div class="rim"></div>
      <div class="grass left"></div>
      <div class="grass right"></div>
    `;
    board.appendChild(el);
    holes.push({
      el, active:false, gold:false,
      until:0, availableAt:0
    });
    el.addEventListener("click", () => {
      if (!pointerHeld) whack(i);
    });
    el.addEventListener("keydown", e => {
      if (e.key === "Enter" || e.key === " ") {
        e.preventDefault();
        whack(i);
      }
    });
  }

  // Sound effects generated entirely using the Web Audio API.
  function initAudio() {
    const AudioContextClass = window.AudioContext || window.webkitAudioContext;
    if (!AudioContextClass) return;
    try {
      if (!audioCtx) audioCtx = new AudioContextClass();
      if (audioCtx.state === "suspended") audioCtx.resume();
    } catch {}
  }

  function tone(frequency, duration, type="sine", volume=.08, endingFrequency=null) {
    if (!audioCtx || audioCtx.state !== "running") return;
    try {
      const now = audioCtx.currentTime;
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.type = type;
      osc.frequency.setValueAtTime(frequency, now);
      if (endingFrequency) {
        osc.frequency.exponentialRampToValueAtTime(
          Math.max(1, endingFrequency), now + duration
        );
      }
      gain.gain.setValueAtTime(volume, now);
      gain.gain.exponentialRampToValueAtTime(.001, now + duration);
      osc.connect(gain);
      gain.connect(audioCtx.destination);
      osc.start(now);
      osc.stop(now + duration + .01);
    } catch {}
  }

  function soundHit(gold) {
    tone(gold ? 680 : 330, .11, "triangle", .1, gold ? 1050 : 180);
    if (gold) {
      setTimeout(() => tone(1100,.13,"sine",.07,1450), 65);
    }
  }

  function soundMiss() {
    tone(160,.075,"triangle",.025,90);
  }

  function soundEnd() {
    [550,440,330,660].forEach((f,i) => {
      setTimeout(() => tone(f,.23,"triangle",.08), i*145);
    });
  }

  function show(id) {
    ["titleScreen","gameOver","pauseOverlay"].forEach(screen => {
      $(screen).classList.toggle("hidden",screen !== id);
    });
  }

  function updateHUD() {
    $("scoreValue").textContent = score;
    $("bestValue").textContent = Math.max(score,best);
    $("timeValue").textContent = Math.ceil(timeLeft);
    $("timeValue").classList.toggle("danger",timeLeft <= 10);
    $("timeBar").style.width = (timeLeft/GAME_LENGTH*100)+"%";
    $("level").textContent =
      "LEVEL " + level + " • " +
      (level===1?"WARM UP":level<4?"GETTING FASTER":level<7?"MOLE MADNESS":"TOTAL CHAOS");
  }

  function startGame() {
    initAudio();
    player = $("nameInput").value.trim().slice(0,18) || "PLAYER";
    save(NAME_KEY,player === "PLAYER" ? "" : player);
    $("playerName").textContent = player.toUpperCase();
    score=0;
    combo=0;
    timeLeft=GAME_LENGTH;
    elapsed=0;
    level=1;
    running=true;
    paused=false;
    nextSpawn=.25;
    lastFrame=0;
    pointerHeld=false;
    pointerHits.clear();

    holes.forEach(h => {
      h.active=false;
      h.gold=false;
      h.until=0;
      h.availableAt=0;
      h.el.classList.remove("active","hit");
      h.el.querySelector(".mole").classList.remove("gold");
      h.el.querySelectorAll(".pop,.spark").forEach(n=>n.remove());
    });

    $("pauseBtn").textContent="Ⅱ";
    updateHUD();
    show("none");
    requestAnimationFrame(loop);
    tone(540,.13,"sine",.07,840);
  }

  function spawnMole() {
    const choices = holes.filter(h => !h.active && elapsed>=h.availableAt);
    if (!choices.length) return;

    const h = choices[Math.floor(Math.random()*choices.length)];
    h.gold = Math.random() < Math.min(.12+level*.012,.25);
    h.active=true;
    h.until=elapsed+Math.max(.52,1.58-level*.115);
    h.el.classList.remove("hit");
    h.el.querySelector(".mole").classList.toggle("gold",h.gold);
    h.el.classList.add("active");
  }

  function hideMole(h, wasHit=false) {
    if (!h.active) return;
    h.active=false;
    h.el.classList.remove("active");
    if (wasHit) h.el.classList.add("hit");
    h.availableAt=elapsed+(wasHit?.18:.13);
    if (!wasHit) combo=0;
  }

  function burst(el,gold,points) {
    const pop = document.createElement("div");
    pop.className="pop";
    pop.textContent="+"+points+(gold?" ★":"");
    if (gold) pop.style.color="#ffe85c";
    el.appendChild(pop);
    setTimeout(()=>pop.remove(),700);

    for(let i=0;i<8;i++){
      const spark=document.createElement("div");
      spark.className="spark";
      const angle=i*Math.PI/4;
      const distance=30+Math.random()*25;
      spark.style.setProperty("--dx",Math.cos(angle)*distance+"px");
      spark.style.setProperty("--dy",Math.sin(angle)*distance+"px");
      spark.style.setProperty("--spark",gold?"#ffe34d":i%2?"#fff":"#ff90bd");
      el.appendChild(spark);
      setTimeout(()=>spark.remove(),520);
    }
  }

  function whack(index) {
    if (!running || paused) return;
    const h=holes[index];
    if (!h || !h.active) return;

    const points=h.gold?3:1;
    score+=points;
    combo++;
    soundHit(h.gold);
    burst(h.el,h.gold,points);
    hideMole(h,true);

    if (combo>=5 && combo%5===0){
      const c=$("combo");
      c.textContent="🔥 "+combo+" HIT STREAK!";
      c.classList.remove("show");
      void c.offsetWidth;
      c.classList.add("show");
    }
    if(navigator.vibrate) navigator.vibrate(h.gold?30:12);
    updateHUD();
  }

  function loop(timestamp) {
    if (!running) return;
    if (!lastFrame) lastFrame=timestamp;
    const dt=Math.min((timestamp-lastFrame)/1000,.1);
    lastFrame=timestamp;

    if (!paused) {
      elapsed+=dt;
      timeLeft=Math.max(0,GAME_LENGTH-elapsed);
      level=Math.min(10,1+Math.floor(elapsed/5));

      holes.forEach(h=>{
        if(h.active && elapsed>=h.until) hideMole(h);
      });

      nextSpawn-=dt;
      if(nextSpawn<=0){
        spawnMole();
        const interval=Math.max(.19,.87-level*.072);
        nextSpawn=interval*(.75+Math.random()*.5);
      }

      updateHUD();
      if(timeLeft<=0){
        finishGame();
        return;
      }
    }
    requestAnimationFrame(loop);
  }

  function finishGame() {
    running=false;
    paused=false;
    const isRecord=score>best;
    if(isRecord) {
      best=score;
      save(BEST_KEY,best);
    }
    holes.forEach(h=>{
      h.active=false;
      h.el.classList.remove("active");
    });
    $("finalScore").textContent=score;
    $("finalBest").textContent=best;
    $("titleBest").textContent=best;
    $("newRecord").hidden=!isRecord;
    $("endMessage").textContent=
      score>=75?"LEGENDARY MOLE MASTER, "+player.toUpperCase()+"!":
      score>=40?"INCREDIBLE WORK, "+player.toUpperCase()+"!":
      score>=20?"NICE WHACKING, "+player.toUpperCase()+"!":
      "KEEP PRACTISING, "+player.toUpperCase()+"!";
    show("gameOver");
    soundEnd();
  }

  function togglePause() {
    if(!running) return;
    paused=!paused;
    if(paused){
      show("pauseOverlay");
    }else{
      show("none");
      lastFrame=0;
    }
  }

  // Touch, pen and mouse swiping.
  // Each target can only score once per continuous swipe.
  function hitAt(x,y){
    const target=document.elementFromPoint(x,y);
    const hole=target?.closest(".hole");
    if(!hole) return;
    const index=holes.findIndex(h=>h.el===hole);
    if(index>=0 && !pointerHits.has(index)){
      pointerHits.add(index);
      whack(index);
    }
  }

  board.addEventListener("pointerdown",e=>{
    if(!running||paused) return;
    e.preventDefault();
    initAudio();
    pointerHeld=true;
    pointerHits.clear();
    try{board.setPointerCapture(e.pointerId)}catch{}
    hitAt(e.clientX,e.clientY);
  });

  board.addEventListener("pointermove",e=>{
    if(!pointerHeld) return;
    e.preventDefault();
    hitAt(e.clientX,e.clientY);
  });

  function releasePointer(){
    pointerHeld=false;
    pointerHits.clear();
  }
  board.addEventListener("pointerup",releasePointer);
  board.addEventListener("pointercancel",releasePointer);
  window.addEventListener("blur",()=>{
    releasePointer();
    if(running&&!paused) togglePause();
  });

  // Keyboard layout:
  // 1 2 3
  // 4 5 6
  // 7 8 9
  // Also supports Q W E / A S D / Z X C.
  const keyMap={
    "1":0,"2":1,"3":2,
    "4":3,"5":4,"6":5,
    "7":6,"8":7,"9":8,
    q:0,w:1,e:2,
    a:3,s:4,d:5,
    z:6,x:7,c:8
  };

  document.addEventListener("keydown",e=>{
    if(document.activeElement===$("nameInput")){
      if(e.key==="Enter") {
        e.preventDefault();
        $("nameInput").blur();
        startGame();
      }
      return;
    }
    if(e.repeat) return;
    const key=e.key.toLowerCase();
    if(key==="escape"||key==="p"){
      if(running){
        e.preventDefault();
        togglePause();
      }
      return;
    }
    if(key in keyMap && running && !paused){
      e.preventDefault();
      initAudio();
      whack(keyMap[key]);
    }
  });

  $("playBtn").addEventListener("click",startGame);
  $("againBtn").addEventListener("click",startGame);
  $("pauseBtn").addEventListener("click",togglePause);
  $("resumeBtn").addEventListener("click",togglePause);
  $("menuBtn").addEventListener("click",()=>{
    running=false;
    paused=false;
    $("titleBest").textContent=best;
    show("titleScreen");
  });

  // Prevent page dragging during the game.
  document.addEventListener("dragstart",e=>e.preventDefault());

  // Pause when app is hidden.
  document.addEventListener("visibilitychange",()=>{
    if(document.hidden && running && !paused) togglePause();
  });

  show("titleScreen");
})();
</script>
</body>
</html>
