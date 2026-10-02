<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>عمارت دانستنی</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@400;600;800&display=swap" rel="stylesheet">
<style>
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent}

  :root{
    --blood:#8b0000;
    --blood-light:#c0392b;
    --ghost:#e8e8e8;
    --accent:#e74c3c;
    --gold:#c9a959;
  }

  body{
    margin:0;
    min-height:100vh;
    font-family:'Vazirmatn',Tahoma,sans-serif;
    background:radial-gradient(ellipse at 50% 0%, #1a0a0a 0%, #0a0a0f 40%, #050508 100%);
    color:var(--ghost);
    display:flex;
    align-items:center;
    justify-content:center;
    padding:20px;
    overflow-x:hidden;
  }

  body::before{
    content:'';
    position:fixed;
    inset:-50%;
    background:
      radial-gradient(circle at 20% 30%, rgba(139,0,0,.08) 0%, transparent 50%),
      radial-gradient(circle at 80% 70%, rgba(139,0,0,.05) 0%, transparent 50%);
    animation:fog 20s ease-in-out infinite alternate;
    pointer-events:none;
    z-index:0;
  }

  @keyframes fog{
    0%{transform:translate(0,0) scale(1)}
    50%{transform:translate(-5%,3%) scale(1.05)}
    100%{transform:translate(5%,-2%) scale(1.1)}
  }

  .app{
    position:relative;
    z-index:1;
    width:100%;
    max-width:900px;
  }

  /* ============ توکن کاربر ============ */
  .token-badge{
    position:fixed;
    top:16px;
    right:16px;
    z-index:10;
    background:linear-gradient(135deg,rgba(20,10,10,.95),rgba(10,5,5,.98));
    border:1px solid rgba(139,0,0,.5);
    padding:8px 14px;
    border-radius:8px;
    font-size:.72rem;
    color:#a0a0b0;
    display:flex;
    align-items:center;
    gap:8px;
    box-shadow:0 4px 20px rgba(139,0,0,.3);
    backdrop-filter:blur(8px);
    transition:.3s;
    cursor:pointer;
  }
  .token-badge:hover{
    border-color:var(--accent);
    box-shadow:0 4px 24px rgba(192,57,43,.5);
  }
  .token-badge .label{color:#5a5a6a;font-size:.65rem}
  .token-badge .value{
    color:#c9a959;
    font-weight:800;
    letter-spacing:1px;
    font-family:monospace;
    direction:ltr;
  }

  /* ============ دکمه صدا ============ */
  .mute-btn{
    position:fixed;
    top:16px;
    left:16px;
    z-index:10;
    width:44px;
    height:44px;
    border-radius:50%;
    background:linear-gradient(135deg,rgba(20,10,10,.95),rgba(10,5,5,.98));
    border:1px solid rgba(139,0,0,.5);
    color:#c9a959;
    font-size:1.2rem;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    transition:.3s;
    box-shadow:0 4px 20px rgba(139,0,0,.3);
  }
  .mute-btn:hover{
    border-color:var(--accent);
    transform:scale(1.08);
    box-shadow:0 4px 24px rgba(192,57,43,.5);
  }

  /* ============ منو ============ */
  .menu-screen{text-align:center;animation:fadeIn .8s ease}
  .menu-screen:not(.active){display:none}

  @keyframes fadeIn{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}

  .title{
    font-size:clamp(2rem,6vw,3.5rem);
    font-weight:800;
    margin:0 0 8px;
    background:linear-gradient(180deg,#e8e8e8 0%,#8b0000 100%);
    -webkit-background-clip:text;
    background-clip:text;
    color:transparent;
    text-shadow:0 0 40px rgba(139,0,0,.6);
    line-height:1.2;
    animation:titlePulse 4s ease-in-out infinite;
  }

  @keyframes titlePulse{
    0%,100%{filter:drop-shadow(0 0 20px rgba(139,0,0,.4))}
    50%{filter:drop-shadow(0 0 40px rgba(139,0,0,.8))}
  }

  .subtitle{
    color:#6a6a7a;
    font-size:.9rem;
    margin:0 0 40px;
    letter-spacing:2px;
    text-transform:uppercase;
  }

  .menu-buttons{
    display:flex;
    flex-direction:column;
    gap:14px;
    max-width:340px;
    margin:0 auto;
  }

  .menu-btn{
    position:relative;
    font-family:inherit;
    font-size:1.05rem;
    font-weight:600;
    padding:18px 24px;
    border:1px solid rgba(139,0,0,.4);
    background:linear-gradient(135deg,rgba(20,10,10,.9),rgba(10,5,5,.95));
    color:#c9c9d0;
    border-radius:4px;
    cursor:pointer;
    transition:all .3s;
    overflow:hidden;
    text-align:right;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }

  .menu-btn::before{
    content:'';
    position:absolute;
    inset:0;
    background:linear-gradient(90deg,transparent,rgba(139,0,0,.15),transparent);
    transform:translateX(-100%);
    transition:transform .5s;
  }
  .menu-btn:hover::before{transform:translateX(100%)}

  .menu-btn:hover{
    border-color:rgba(192,57,43,.8);
    color:#fff;
    box-shadow:0 0 30px rgba(139,0,0,.3),inset 0 0 30px rgba(139,0,0,.1);
    transform:translateX(-4px);
  }
  .menu-btn .icon{font-size:1.4rem;filter:drop-shadow(0 0 8px rgba(139,0,0,.8))}
  .menu-btn.danger{border-color:rgba(192,57,43,.6)}
  .menu-btn.danger .icon{filter:drop-shadow(0 0 8px rgba(192,57,43,1))}

  /* ============ کوییز ============ */
  .quiz-screen{display:none;animation:fadeIn .5s ease}
  .quiz-screen.active{display:block}

  .quiz-header{
    display:flex;align-items:center;justify-content:space-between;
    margin-bottom:24px;padding-bottom:16px;
    border-bottom:1px solid rgba(139,0,0,.2);
  }
  .quiz-header h2{margin:0;font-size:1.2rem;color:#c9a959;font-weight:600}

  .back-btn{
    font-family:inherit;font-size:.85rem;padding:8px 16px;
    background:transparent;border:1px solid rgba(139,0,0,.4);
    color:#8a8a9a;border-radius:4px;cursor:pointer;transition:.3s;
  }
  .back-btn:hover{border-color:var(--accent);color:var(--accent)}

  .progress-bar{
    height:4px;background:rgba(139,0,0,.15);border-radius:2px;
    margin-bottom:28px;overflow:hidden;
  }
  .progress-fill{
    height:100%;background:linear-gradient(90deg,var(--blood),var(--accent));
    border-radius:2px;transition:width .4s ease;
    box-shadow:0 0 12px rgba(139,0,0,.6);
  }

  .question-box{
    background:linear-gradient(135deg,rgba(15,10,10,.9),rgba(8,5,5,.95));
    border:1px solid rgba(139,0,0,.25);border-radius:8px;
    padding:32px 28px;margin-bottom:24px;position:relative;overflow:hidden;
  }
  .question-box::before{
    content:'';position:absolute;top:0;right:0;width:80px;height:80px;
    background:radial-gradient(circle at top right,rgba(139,0,0,.15),transparent 70%);
  }
  .question-num{
    font-size:.75rem;color:#6a6a7a;letter-spacing:2px;
    margin-bottom:12px;text-transform:uppercase;
  }
  .question-text{
    font-size:1.15rem;line-height:1.9;color:#d0d0d8;
    margin:0;font-weight:600;
  }

  .options{display:flex;flex-direction:column;gap:10px}

  .option{
    font-family:inherit;font-size:.95rem;padding:16px 20px;
    background:rgba(15,10,10,.7);border:1px solid rgba(139,0,0,.2);
    color:#b0b0bc;border-radius:6px;cursor:pointer;
    transition:all .25s;text-align:right;
    position:relative;overflow:hidden;
  }
  .option:hover:not(:disabled){
    border-color:rgba(192,57,43,.6);
    background:rgba(30,15,15,.8);color:#fff;transform:translateX(-3px);
  }
  .option:disabled{cursor:default;opacity:.5}

  .option.correct{
    border-color:#27ae60;background:rgba(39,174,96,.15);
    color:#7dcea0;box-shadow:0 0 20px rgba(39,174,96,.2);
    animation:correctPulse .5s ease;
  }
  @keyframes correctPulse{
    0%,100%{box-shadow:0 0 20px rgba(39,174,96,.2)}
    50%{box-shadow:0 0 40px rgba(39,174,96,.6)}
  }

  .option.wrong{
    border-color:#c0392b;background:rgba(192,57,43,.15);
    color:#e74c3c;animation:wrongShake .4s ease;
  }
  @keyframes wrongShake{
    0%,100%{transform:translateX(0)}
    25%{transform:translateX(-6px)}
    75%{transform:translateX(6px)}
  }

  .option .mark{
    position:absolute;left:16px;top:50%;transform:translateY(-50%);
    font-size:1.1rem;opacity:0;transition:.3s;
  }
  .option.correct .mark,.option.wrong .mark{opacity:1}

  /* ============ نتیجه ============ */
  .result-screen{display:none;text-align:center;animation:fadeIn .6s ease}
  .result-screen.active{display:block}
  .result-icon{font-size:4rem;margin-bottom:16px;filter:drop-shadow(0 0 30px rgba(139,0,0,.8))}
  .result-title{font-size:1.8rem;font-weight:800;margin:0 0 8px;color:#e8e8e8}
  .result-score{
    font-size:2.5rem;font-weight:800;color:#c9a959;
    margin:0 0 8px;text-shadow:0 0 30px rgba(201,169,89,.5);
  }
  .result-msg{color:#7a7a8a;margin:0 0 32px;line-height:1.8}
  .result-actions{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}

  .action-btn{
    font-family:inherit;font-size:.95rem;font-weight:600;
    padding:14px 28px;border-radius:6px;cursor:pointer;
    transition:.3s;border:none;
  }
  .action-btn.primary{
    background:linear-gradient(135deg,#8b0000,#c0392b);color:#fff;
    box-shadow:0 8px 24px rgba(139,0,0,.4);
  }
  .action-btn.primary:hover{filter:brightness(1.15);box-shadow:0 8px 32px rgba(139,0,0,.6)}
  .action-btn.secondary{
    background:transparent;border:1px solid rgba(139,0,0,.4);color:#8a8a9a;
  }
  .action-btn.secondary:hover{border-color:var(--accent);color:var(--accent)}

  /* ============ نفرات برتر ============ */
  .leaderboard-screen{display:none;animation:fadeIn .5s ease}
  .leaderboard-screen.active{display:block}

  .leaderboard-title{
    font-size:1.6rem;font-weight:800;text-align:center;margin:0 0 8px;
    color:#c9a959;text-shadow:0 0 30px rgba(201,169,89,.4);
  }
  .leaderboard-sub{text-align:center;color:#5a5a6a;font-size:.85rem;margin-bottom:28px}

  .leaderboard-list{display:flex;flex-direction:column;gap:8px}

  .leaderboard-item{
    display:flex;align-items:center;gap:14px;
    padding:16px 20px;background:rgba(15,10,10,.8);
    border:1px solid rgba(139,0,0,.15);border-radius:6px;transition:.3s;
  }
  .leaderboard-item:hover{border-color:rgba(139,0,0,.4)}

  .leaderboard-item.me{
    border-color:rgba(201,169,89,.6);
    background:linear-gradient(135deg,rgba(201,169,89,.08),rgba(15,10,10,.9));
    box-shadow:0 0 20px rgba(201,169,89,.15);
  }

  .leaderboard-item .rank{
    font-size:1.2rem;font-weight:800;width:40px;
    text-align:center;color:#6a6a7a;flex:none;
  }
  .leaderboard-item:nth-child(1) .rank{color:#c9a959}
  .leaderboard-item:nth-child(2) .rank{color:#a0a0b0}
  .leaderboard-item:nth-child(3) .rank{color:#8b6914}

  .leaderboard-item .info{
    flex:1;display:flex;justify-content:space-between;
    align-items:center;flex-wrap:wrap;gap:8px;
  }
  .leaderboard-item .name{
    font-weight:600;color:#c0c0cc;font-family:monospace;
    direction:ltr;letter-spacing:1px;
  }
  .leaderboard-item.me .name{color:#c9a959}

  .leaderboard-item .you-tag{
    display:inline-block;font-size:.65rem;padding:2px 8px;
    background:rgba(201,169,89,.2);color:#c9a959;
    border-radius:10px;margin-right:8px;font-family:Vazirmatn,sans-serif;
    direction:rtl;
  }

  .leaderboard-item .stats{
    display:flex;gap:10px;align-items:center;font-size:.8rem;
  }
  .leaderboard-item .correct-n{color:#7dcea0;font-weight:700}
  .leaderboard-item .wrong-n{color:#e74c3c;font-weight:700}
  .leaderboard-item .score{
    font-weight:800;font-size:1.05rem;color:#c9a959;
    min-width:52px;text-align:center;
  }

  .empty-state{text-align:center;padding:60px 20px;color:#3a3a4a}
  .empty-state .icon{font-size:3rem;margin-bottom:12px;opacity:.4}

  .loading{text-align:center;padding:60px 20px;color:#5a5a6a}
  .loading .spinner{
    width:40px;height:40px;border:3px solid rgba(139,0,0,.2);
    border-top-color:var(--blood);border-radius:50%;
    margin:0 auto 16px;animation:spin 1s linear infinite;
  }
  @keyframes spin{to{transform:rotate(360deg)}}

  .error-msg{text-align:center;padding:40px 20px;color:#c0392b}

  /* ============ ذرات ============ */
  .particles{position:fixed;inset:0;pointer-events:none;z-index:0;overflow:hidden}
  .particle{
    position:absolute;width:2px;height:2px;background:rgba(139,0,0,.4);
    border-radius:50%;animation:float linear infinite;
  }
  @keyframes float{
    0%{transform:translateY(100vh) translateX(0);opacity:0}
    10%{opacity:1}
    90%{opacity:1}
    100%{transform:translateY(-10vh) translateX(30px);opacity:0}
  }

  @media(max-width:600px){
    .question-box{padding:24px 18px}
    .question-text{font-size:1rem}
    .menu-btn{font-size:.95rem;padding:16px 18px}
    .token-badge{font-size:.65rem;padding:6px 10px}
    .mute-btn{width:38px;height:38px;font-size:1rem}
    .leaderboard-item{padding:12px 14px;gap:8px}
    .leaderboard-item .name{font-size:.75rem}
    .leaderboard-item .stats{font-size:.7rem}
  }
</style>
</head>
<body>

<div class="particles" id="particles"></div>

<!-- توکن کاربر -->
<div class="token-badge" id="tokenBadge" title="کلیک برای کپی توکن">
  <span class="label">توکن شما:</span>
  <span class="value" id="tokenValue">—</span>
</div>

<!-- دکمه صدا -->
<button class="mute-btn" id="muteBtn" title="روشن/خاموش کردن صدا">🔊</button>

<div class="app">

  <!-- منو -->
  <div class="menu-screen active" id="menuScreen">
    <h1 class="title">🏚️ عمارت دانستنی</h1>
    <p class="subtitle">دانش خود را در تاریکی محک بزنید</p>

    <div class="menu-buttons">
      <button class="menu-btn" id="startQuizBtn">
        <span>دانستنی</span>
        <span class="icon">💀</span>
      </button>
      <button class="menu-btn danger" id="leaderboardBtn">
        <span>نفرات برتر</span>
        <span class="icon">🏆</span>
      </button>
    </div>
  </div>

  <!-- کوییز -->
  <div class="quiz-screen" id="quizScreen"></div>

  <!-- نتیجه -->
  <div class="result-screen" id="resultScreen">
    <div class="result-icon" id="resultIcon">💀</div>
    <h2 class="result-title" id="resultTitle">پایان بازی</h2>
    <div class="result-score" id="resultScore">۰ / ۱۰</div>
    <p class="result-msg" id="resultMsg"></p>

    <div class="result-actions">
      <button class="action-btn primary" id="retryBtn">🔄 دوباره</button>
      <button class="action-btn secondary" id="homeBtn">🏠 خانه</button>
    </div>
  </div>

  <!-- نفرات برتر -->
  <div class="leaderboard-screen" id="leaderboardScreen">
    <div class="quiz-header">
      <h2>🏆 نفرات برتر</h2>
      <button class="back-btn" id="lbBackBtn">→ بازگشت</button>
    </div>
    <p class="leaderboard-sub">هر پاسخ درست یا غلط شما در این جدول ثبت می‌شود</p>
    <div class="leaderboard-list" id="leaderboardList"></div>
  </div>

</div>

<script>
/* ============================================================
   ثابت‌ها
   ============================================================ */
const API_URL = 'https://raw.githubusercontent.com/qwerggggggggg/tst/refs/heads/main/README.md';
const TOKEN_KEY = 'mansion_user_token_v1';
const LOG_KEY   = 'mansion_answer_log_v1';
const MUTE_KEY  = 'mansion_mute_v1';
const QUESTIONS_PER_ROUND = 10;

const FA = '۰۱۲۳۴۵۶۷۸۹';
const fa = n => String(n).replace(/\d/g, d => FA[+d]);
const sleep = ms => new Promise(r => setTimeout(r, ms));

/* ============================================================
   سیستم صدا (Web Audio API)
   ============================================================ */
const Audio = (() => {
  let ctx = null;
  let muted = localStorage.getItem(MUTE_KEY) === '1';
  let musicNodes = [];
  let musicTimer = null;
  let musicPlaying = false;

  function init(){
    if (!ctx){
      try{
        ctx = new (window.AudioContext || window.webkitAudioContext)();
      }catch(e){
        console.warn('Web Audio پشتیبانی نمی‌شود', e);
        return null;
      }
    }
    if (ctx.state === 'suspended') ctx.resume();
    return ctx;
  }

  function isMuted(){ return muted; }

  function setMuted(v){
    muted = v;
    localStorage.setItem(MUTE_KEY, v ? '1' : '0');
    if (v){
      stopMusic();
    } else {
      startMusic();
    }
  }

  // پخش یک نُت
  function tone(freq, dur, {type='sine', vol=0.1, delay=0, slideTo=null, attack=0.01}={}){
    if (muted) return;
    const c = init();
    if (!c) return;

    const t0 = c.currentTime + delay;
    const osc = c.createOscillator();
    const g = c.createGain();

    osc.type = type;
    osc.frequency.setValueAtTime(freq, t0);
    if (slideTo) osc.frequency.exponentialRampToValueAtTime(slideTo, t0 + dur);

    g.gain.setValueAtTime(0.0001, t0);
    g.gain.exponentialRampToValueAtTime(vol, t0 + attack);
    g.gain.exponentialRampToValueAtTime(0.0001, t0 + dur);

    osc.connect(g);
    g.connect(c.destination);
    osc.start(t0);
    osc.stop(t0 + dur + 0.05);
  }

  // صدای کلیک (منو)
  function click(){
    tone(880, 0.06, {type:'triangle', vol:0.05});
    tone(440, 0.12, {type:'sine', vol:0.04, delay:0.03});
    // زمزمه کوتاه
    tone(220, 0.25, {type:'sine', vol:0.025, delay:0.05, slideTo:110});
  }

  // صدای پاسخ درست (آرپژ صعودی)
  function correct(){
    const notes = [523.25, 659.25, 783.99, 1046.5]; // C5 E5 G5 C6
    notes.forEach((f, i) => {
      tone(f, 0.35, {type:'sine', vol:0.10, delay: i * 0.075});
      tone(f * 2, 0.2, {type:'triangle', vol:0.03, delay: i * 0.075});
    });
    // نویز جشن
    tone(1568, 0.6, {type:'sine', vol:0.05, delay:0.32, slideTo:2093});
  }

  // صدای پاسخ غلط (باز پایین‌رونده)
  function wrong(){
    tone(220, 0.18, {type:'sawtooth', vol:0.08});
    tone(185, 0.18, {type:'sawtooth', vol:0.08, delay:0.1});
    tone(140, 0.45, {type:'sawtooth', vol:0.09, delay:0.2, slideTo:70});
    tone(90, 0.5, {type:'square', vol:0.05, delay:0.25, slideTo:45});
  }

  // شروع موسیقی منو (درون + ناقوس‌های تصادفی)
  function startMusic(){
    if (muted || musicPlaying) return;
    const c = init();
    if (!c) return;

    musicPlaying = true;
    musicNodes = [];

    // درون پایین (A1)
    const drone1 = c.createOscillator();
    drone1.type = 'sine';
    drone1.frequency.value = 55;

    const g1 = c.createGain();
    g1.gain.value = 0.035;

    // LFO برای تنفس
    const lfo = c.createOscillator();
    lfo.frequency.value = 0.08;
    const lfoGain = c.createGain();
    lfoGain.gain.value = 0.02;
    lfo.connect(lfoGain);
    lfoGain.connect(g1.gain);

    drone1.connect(g1);
    g1.connect(c.destination);
    drone1.start();
    lfo.start();
    musicNodes.push(drone1, lfo);

    // درون دوم (E2)
    const drone2 = c.createOscillator();
    drone2.type = 'sine';
    drone2.frequency.value = 82.41;

    const g2 = c.createGain();
    g2.gain.value = 0.02;

    const lfo2 = c.createOscillator();
    lfo2.frequency.value = 0.05;
    const lfo2Gain = c.createGain();
    lfo2Gain.gain.value = 0.012;
    lfo2.connect(lfo2Gain);
    lfo2Gain.connect(g2.gain);

    drone2.connect(g2);
    g2.connect(c.destination);
    drone2.start();
    lfo2.start();
    musicNodes.push(drone2, lfo2);

    // درون سوم (A2 ضعیف)
    const drone3 = c.createOscillator();
    drone3.type = 'triangle';
    drone3.frequency.value = 110;
    const g3 = c.createGain();
    g3.gain.value = 0.008;
    drone3.connect(g3);
    g3.connect(c.destination);
    drone3.start();
    musicNodes.push(drone3);

    // ناقوس‌های تصادفی خفاش‌گونه
    const bellNotes = [220, 261.63, 329.63, 392, 440, 523.25];
    musicTimer = setInterval(() => {
      if (muted || !musicPlaying) return;
      if (Math.random() < 0.35){
        const f = bellNotes[Math.floor(Math.random() * bellNotes.length)];
        tone(f, 2.5, {type:'sine', vol:0.012, attack:0.6});
        tone(f * 2.01, 1.8, {type:'sine', vol:0.006, attack:0.8, delay:0.15});
      }
      // گاهی صدای نفس/خش
      if (Math.random() < 0.08){
        tone(60, 1.5, {type:'sawtooth', vol:0.008, attack:0.4, slideTo:40});
      }
    }, 2200);
  }

  function stopMusic(){
    musicNodes.forEach(n => { try{ n.stop(); }catch(e){} });
    musicNodes = [];
    if (musicTimer){ clearInterval(musicTimer); musicTimer = null; }
    musicPlaying = false;
  }

  return { init, click, correct, wrong, startMusic, stopMusic, isMuted, setMuted };
})();

/* ============================================================
   مدیریت توکن کاربر
   ============================================================ */
function getOrCreateToken(){
  let token = localStorage.getItem(TOKEN_KEY);
  if (!token){
    const hex = () => Math.floor(Math.random() * 65536).toString(16).padStart(4,'0').toUpperCase();
    token = `${hex()}-${hex()}`;
    localStorage.setItem(TOKEN_KEY, token);
  }
  return token;
}

const USER_TOKEN = getOrCreateToken();
document.getElementById('tokenValue').textContent = USER_TOKEN;

// کپی توکن با کلیک
document.getElementById('tokenBadge').addEventListener('click', () => {
  navigator.clipboard?.writeText(USER_TOKEN).then(() => {
    const badge = document.getElementById('tokenBadge');
    const orig = badge.querySelector('.label').textContent;
    badge.querySelector('.label').textContent = 'کپی شد!';
    Audio.click();
    setTimeout(() => { badge.querySelector('.label').textContent = orig; }, 1200);
  });
});

/* ============================================================
   ثبت پاسخ‌ها (لاگ)
   ============================================================ */
function getLog(){
  try{
    return JSON.parse(localStorage.getItem(LOG_KEY) || '[]');
  }catch{ return []; }
}

function recordAnswer(isCorrect, questionText){
  const log = getLog();
  log.push({
    token: USER_TOKEN,
    correct: isCorrect,
    q: questionText.slice(0, 60),
    t: Date.now()
  });
  // فقط ۵۰۰ رکورد آخر را نگه دار
  if (log.length > 500) log.splice(0, log.length - 500);
  localStorage.setItem(LOG_KEY, JSON.stringify(log));
}

/* ============================================================
   وضعیت
   ============================================================ */
const state = {
  allQuestions: [],
  currentQuestions: [],
  currentIndex: 0,
  score: 0,
  answered: false
};

/* ============================================================
   عناصر
   ============================================================ */
const $ = id => document.getElementById(id);
const menuScreen = $('menuScreen');
const quizScreen = $('quizScreen');
const resultScreen = $('resultScreen');
const leaderboardScreen = $('leaderboardScreen');
const leaderboardList = $('leaderboardList');
const muteBtn = $('muteBtn');

/* ============================================================
   ناوبری
   ============================================================ */
function showScreen(screen){
  [menuScreen, quizScreen, resultScreen, leaderboardScreen].forEach(s => s.classList.remove('active'));
  screen.classList.add('active');
}

/* ============================================================
   ذرات
   ============================================================ */
function createParticles(){
  const c = $('particles');
  for (let i = 0; i < 30; i++){
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.left = Math.random() * 100 + '%';
    p.style.animationDuration = (8 + Math.random() * 12) + 's';
    p.style.animationDelay = Math.random() * 10 + 's';
    p.style.opacity = 0.2 + Math.random() * 0.5;
    c.appendChild(p);
  }
}

/* ============================================================
   بارگذاری سوالات
   ============================================================ */
async function loadQuestions(){
  if (state.allQuestions.length > 0) return true;
  try{
    const res = await fetch(API_URL);
    if (!res.ok) throw new Error('HTTP ' + res.status);
    const data = JSON.parse(await res.text());
    const all = [];

    if (data.categories){
      for (const [cat, catData] of Object.entries(data.categories)){
        if (catData.questions && Array.isArray(catData.questions)){
          catData.questions.forEach(q => {
            if (q.question && q.options && Array.isArray(q.options)){
              all.push({
                question: q.question,
                options: q.options,
                correct: q.correct,
                category: cat
              });
            }
          });
        }
      }
    }

    if (all.length === 0) throw new Error('هیچ سوالی یافت نشد');
    state.allQuestions = all;
    return true;
  }catch(err){
    console.error('خطا در بارگذاری:', err);
    return false;
  }
}

/* ============================================================
   شروع کوییز
   ============================================================ */
async function startQuiz(){
  showScreen(quizScreen);
  quizScreen.innerHTML = `
    <div class="loading">
      <div class="spinner"></div>
      <p>در حال فراخوانی ارواح دانش...</p>
    </div>`;

  const ok = await loadQuestions();

  if (!ok){
    quizScreen.innerHTML = `
      <div class="error-msg">
        <p>⚠️ اتصال به سرور برقرار نشد</p>
        <p style="font-size:.85rem;color:#5a5a6a">لطفاً اینترنت خود را بررسی کنید</p>
        <button class="action-btn secondary" onclick="location.reload()" style="margin-top:20px">تلاش مجدد</button>
      </div>`;
    return;
  }

  quizScreen.innerHTML = `
    <div class="quiz-header">
      <h2>دانستنی</h2>
      <button class="back-btn" id="quizBackBtn">→ بازگشت</button>
    </div>
    <div class="progress-bar">
      <div class="progress-fill" id="progressFill" style="width:0%"></div>
    </div>
    <div class="question-box">
      <div class="question-num" id="questionNum"></div>
      <p class="question-text" id="questionText"></p>
    </div>
    <div class="options" id="optionsContainer"></div>`;

  $('quizBackBtn').addEventListener('click', () => {
    Audio.click();
    showScreen(menuScreen);
  });

  const shuffled = [...state.allQuestions].sort(() => Math.random() - 0.5);
  state.currentQuestions = shuffled.slice(0, QUESTIONS_PER_ROUND);
  state.currentIndex = 0;
  state.score = 0;

  renderQuestion();
}

/* ============================================================
   نمایش سوال
   ============================================================ */
function renderQuestion(){
  const q = state.currentQuestions[state.currentIndex];
  if (!q) return;
  state.answered = false;

  $('questionNum').textContent = `سوال ${fa(state.currentIndex + 1)} از ${fa(state.currentQuestions.length)}`;
  $('questionText').textContent = q.question;

  const prog = (state.currentIndex / state.currentQuestions.length) * 100;
  $('progressFill').style.width = prog + '%';

  const optsEl = $('optionsContainer');
  optsEl.innerHTML = '';

  q.options.forEach((opt, idx) => {
    const btn = document.createElement('button');
    btn.className = 'option';
    btn.textContent = opt;

    const mark = document.createElement('span');
    mark.className = 'mark';
    btn.appendChild(mark);

    btn.addEventListener('click', () => handleAnswer(idx, btn, q));
    optsEl.appendChild(btn);
  });
}

/* ============================================================
   پردازش پاسخ
   ============================================================ */
async function handleAnswer(selectedIdx, btn, q){
  if (state.answered) return;
  state.answered = true;

  const isCorrect = selectedIdx === q.correct;
  const allBtns = document.querySelectorAll('.option');
  allBtns.forEach(b => b.disabled = true);

  allBtns.forEach((b, i) => {
    if (i === q.correct){
      b.classList.add('correct');
      b.querySelector('.mark').textContent = '✓';
    }
  });

  if (!isCorrect){
    btn.classList.add('wrong');
    btn.querySelector('.mark').textContent = '✗';
  } else {
    state.score++;
  }

  // ثبت در لاگ (هر پاسخ درست یا غلط)
  recordAnswer(isCorrect, q.question);

  // صدای پاسخ
  if (isCorrect) Audio.correct();
  else Audio.wrong();

  await sleep(isCorrect ? 1000 : 1500);

  state.currentIndex++;
  if (state.currentIndex >= state.currentQuestions.length){
    finishQuiz();
  } else {
    renderQuestion();
  }
}

/* ============================================================
   پایان کوییز
   ============================================================ */
function finishQuiz(){
  const total = state.currentQuestions.length;
  const score = state.score;
  const pct = score / total;

  let icon, title, msg;
  if (pct >= 0.9){ icon='👑'; title='افسانه‌ای!'; msg='شما دیوارهای عمارت را شکستید. دانش شما تاریکی را تسخیر کرد.'; }
  else if (pct >= 0.7){ icon='🔥'; title='عالی!'; msg='تقریباً تمام ارواح را فراری دادید. فقط چند قدم تا کمال باقی است.'; }
  else if (pct >= 0.5){ icon='🌙'; title='خوب'; msg='از تاریکی عبور کردید، اما برخی سایه‌ها هنوز در کمین هستند.'; }
  else if (pct >= 0.3){ icon='💀'; title='ضعیف'; msg='ارواح عمارت پیروز شدند. زمان مطالعه فرا رسیده است.'; }
  else { icon='🕯️'; title='شکست'; msg='عمارت شما را بلعید. اما همیشه فرصتی دوباره هست...'; }

  $('resultIcon').textContent = icon;
  $('resultTitle').textContent = title;
  $('resultScore').textContent = `${fa(score)} / ${fa(total)}`;
  $('resultMsg').textContent = msg;

  showScreen(resultScreen);

  // صدای پایان
  if (pct >= 0.7) Audio.correct();
  else if (pct < 0.4) Audio.wrong();
}

/* ============================================================
   نفرات برتر — تجمیع بر اساس توکن
   ============================================================ */
function renderLeaderboard(){
  const log = getLog();
  const container = leaderboardList;

  if (log.length === 0){
    container.innerHTML = `
      <div class="empty-state">
        <div class="icon">🏚️</div>
        <p>هنوز کسی در عمارت پاسخ نداده است.</p>
        <p style="font-size:.8rem;margin-top:8px">اولین نفر باش!</p>
      </div>`;
    return;
  }

  // تجمیع بر اساس توکن
  const byToken = {};
  log.forEach(entry => {
    if (!byToken[entry.token]){
      byToken[entry.token] = { token: entry.token, correct: 0, wrong: 0, last: entry.t };
    }
    if (entry.correct) byToken[entry.token].correct++;
    else byToken[entry.token].wrong++;
    if (entry.t > byToken[entry.token].last) byToken[entry.token].last = entry.t;
  });

  const entries = Object.values(byToken).map(e => {
    const total = e.correct + e.wrong;
    return { ...e, total, pct: total ? e.correct / total : 0 };
  }).sort((a, b) => {
    if (b.pct !== a.pct) return b.pct - a.pct;
    if (b.correct !== a.correct) return b.correct - a.correct;
    return b.last - a.last;
  });

  container.innerHTML = '';

  entries.forEach((e, idx) => {
    const item = document.createElement('div');
    item.className = 'leaderboard-item';
    if (e.token === USER_TOKEN) item.classList.add('me');

    let rankIcon = fa(idx + 1);
    if (idx === 0) rankIcon = '🥇';
    else if (idx === 1) rankIcon = '🥈';
    else if (idx === 2) rankIcon = '🥉';

    const youTag = e.token === USER_TOKEN ? '<span class="you-tag">شما</span>' : '';
    const pctDisplay = fa(Math.round(e.pct * 100));

    item.innerHTML = `
      <div class="rank">${rankIcon}</div>
      <div class="info">
        <div class="name">${youTag}${e.token}</div>
        <div class="stats">
          <span class="correct-n">✓ ${fa(e.correct)}</span>
          <span class="wrong-n">✗ ${fa(e.wrong)}</span>
          <span class="score">${pctDisplay}٪</span>
        </div>
      </div>`;
    container.appendChild(item);
  });
}

/* ============================================================
   رویدادها
   ============================================================ */

// راه‌اندازی صدا در اولین تعامل کاربر
let audioUnlocked = false;
function unlockAudio(){
  if (audioUnlocked) return;
  audioUnlocked = true;
  Audio.init();
  if (!Audio.isMuted()) Audio.startMusic();
  updateMuteBtn();
}
document.addEventListener('pointerdown', unlockAudio, { once: true });
document.addEventListener('keydown', unlockAudio, { once: true });

// دکمه صدا
function updateMuteBtn(){
  muteBtn.textContent = Audio.isMuted() ? '🔇' : '🔊';
  muteBtn.title = Audio.isMuted() ? 'روشن کردن صدا' : 'خاموش کردن صدا';
}
muteBtn.addEventListener('click', (ev) => {
  ev.stopPropagation();
  Audio.init();
  Audio.setMuted(!Audio.isMuted());
  updateMuteBtn();
  if (!Audio.isMuted()) Audio.click();
});
updateMuteBtn();

// شروع کوییز
$('startQuizBtn').addEventListener('click', () => {
  Audio.click();
  startQuiz();
});

// نفرات برتر
$('leaderboardBtn').addEventListener('click', () => {
  Audio.click();
  renderLeaderboard();
  showScreen(leaderboardScreen);
});

// بازگشت از نفرات برتر
$('lbBackBtn').addEventListener('click', () => {
  Audio.click();
  showScreen(menuScreen);
});

// دوباره
$('retryBtn').addEventListener('click', () => {
  Audio.click();
  startQuiz();
});

// خانه
$('homeBtn').addEventListener('click', () => {
  Audio.click();
  showScreen(menuScreen);
});

/* ============================================================
   راه‌اندازی
   ============================================================ */
createParticles();
showScreen(menuScreen);

// پیش‌بارگذاری سوالات
loadQuestions().then(ok => {
  if (ok) console.log(`✅ ${state.allQuestions.length} سوال آماده است`);
});
</script>

</body>
</html>
