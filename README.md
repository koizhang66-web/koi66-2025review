<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>曠野 2024–2025</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;700;900&family=Noto+Sans+TC:wght@300;400;500&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f5f0e8;
  --bg2: #ede7d9;
  --ink: #1a1814;
  --ink2: #4a4540;
  --ink3: #8a837a;
  --ink4: #c4bdb4;
  --gold: #b8864e;
  --gold2: #d4a574;
  --forest: #4a7a50;
  --forest2: #5a8a60;
  --forest3: #6a9e70;
  --teal: #3d7a6e;
  --red: #b84a3a;
  --cream: #faf6ee;
  --serif: 'DM Serif Display', 'Noto Serif TC', serif;
  --sans: 'Noto Sans TC', sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{background:var(--bg);color:var(--ink);font-family:var(--sans);font-weight:300;overflow-x:hidden;cursor:default;}

/* ── VIEWS ── */
.view{display:none;min-height:100vh;}
.view.active{display:block;}

/* ── HOME ── */
#home{
  min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:2rem;position:relative;overflow:hidden;
}
.home-grain{
  position:absolute;inset:0;opacity:0.04;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  pointer-events:none;
}
.home-year{
  font-size:11px;letter-spacing:0.25em;color:var(--forest3);margin-bottom:1.5rem;
  opacity:0;animation:up 0.7s ease 0.2s forwards;
}
.home-title{
  font-family:var(--serif);font-size:clamp(2.8rem,7vw,5.5rem);line-height:1.15;
  text-align:center;margin-bottom:0.5rem;
  opacity:0;animation:up 0.7s ease 0.4s forwards;
}
.home-title .alt{font-style:italic;color:var(--forest);}
.home-sub{
  font-size:13px;color:var(--ink3);letter-spacing:0.06em;margin-bottom:3rem;text-align:center;
  opacity:0;animation:up 0.7s ease 0.6s forwards;
}
.chapters{
  display:flex;flex-direction:column;
  gap:10px;width:100%;max-width:660px;
  opacity:0;animation:up 0.7s ease 0.8s forwards;
}
.chapters-row{display:flex;gap:10px;}
.chapters-row.top .chapter-btn{flex:1;min-width:0;}
.chapters-row.bottom{justify-content:center;}
.chapters-row.bottom .chapter-btn{flex:0 0 calc(33.33% - 7px);}
.chapter-btn{
  background:var(--cream);border:1px solid var(--ink4);border-radius:12px;
  padding:1.25rem 1rem;cursor:pointer;transition:all 0.2s;text-align:left;
  position:relative;overflow:hidden;
}
.chapter-btn::before{
  content:'';position:absolute;inset:0;background:var(--ink);opacity:0;
  transition:opacity 0.2s;
}
.chapter-btn:hover{border-color:var(--forest);transform:translateY(-2px);box-shadow:0 8px 24px rgba(74,122,80,0.12);}
.chapter-btn:hover::before{opacity:0.03;}
.ch-num{font-size:10px;color:var(--ink4);letter-spacing:0.12em;margin-bottom:6px;}
.ch-icon{font-size:1.5rem;margin-bottom:6px;display:block;}
.ch-title{font-size:14px;font-weight:500;color:var(--ink);line-height:1.3;}
.ch-sub{font-size:11px;color:var(--ink3);margin-top:3px;}

.back-btn{
  position:fixed;top:1rem;left:1rem;z-index:99;
  background:var(--cream);border:1px solid var(--ink4);border-radius:20px;
  padding:6px 14px;font-size:12px;color:var(--ink2);cursor:pointer;
  display:none;align-items:center;gap:6px;transition:all 0.2s;
}
.back-btn:hover{border-color:var(--forest);color:var(--forest);}
.back-btn.show{display:flex;}

/* ── CHAPTER HEADER ── */
.ch-header{
  padding:4rem 2rem 2rem;max-width:800px;margin:0 auto;
  border-bottom:1px solid var(--ink4);margin-bottom:2rem;
}
.ch-header-tag{font-size:10px;letter-spacing:0.2em;color:var(--forest3);margin-bottom:0.5rem;font-weight:500;}
.ch-header-title{font-family:var(--serif);font-size:clamp(2rem,5vw,3.5rem);}
.ch-header-title .alt{font-style:italic;color:var(--forest);}
.ch-body{max-width:800px;margin:0 auto;padding:0 2rem 4rem;}

/* ── FIRSTS (flip cards) ── */
.firsts-intro{font-size:14px;color:var(--ink2);line-height:1.8;margin-bottom:2rem;}
.cards-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:16px;}
.flip-card{height:200px;cursor:pointer;perspective:1000px;}
.flip-inner{
  position:relative;width:100%;height:100%;
  transform-style:preserve-3d;transition:transform 0.55s cubic-bezier(.4,0,.2,1);
}
.flip-card.flipped .flip-inner{transform:rotateY(180deg);}
.flip-front,.flip-back{
  position:absolute;inset:0;border-radius:12px;
  backface-visibility:hidden;-webkit-backface-visibility:hidden;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:1.25rem;text-align:center;
}
.flip-front{background:var(--cream);border:1px solid var(--ink4);}
.flip-back{background:#3a6640;transform:rotateY(180deg);border:1px solid #3a6640;}
.flip-front-icon{font-size:2.2rem;margin-bottom:10px;}
.flip-front-label{font-size:13px;font-weight:500;color:var(--ink);}
.flip-front-hint{font-size:10px;color:var(--ink4);margin-top:6px;letter-spacing:0.05em;}
.flip-back-text{font-size:13px;color:rgba(255,255,255,0.85);line-height:1.7;}
.flip-back-year{font-size:10px;color:#a8c89a;letter-spacing:0.1em;margin-bottom:8px;}

/* ── PLACES (horizontal scroll) ── */
.places-scroll-wrap{overflow-x:auto;padding-bottom:1rem;cursor:grab;}
.places-scroll-wrap:active{cursor:grabbing;}
.places-track{display:flex;gap:16px;width:max-content;padding:1rem 0;}
.place-card{
  width:240px;flex-shrink:0;background:var(--cream);border:1px solid var(--ink4);
  border-radius:16px;overflow:hidden;transition:transform 0.2s,box-shadow 0.2s;cursor:pointer;
}
.place-card:hover{transform:translateY(-4px);box-shadow:0 12px 32px rgba(0,0,0,0.1);}
.place-emoji{
  height:120px;display:flex;align-items:center;justify-content:center;font-size:3.5rem;
  position:relative;
}
.place-body{padding:1rem;}
.place-name{font-size:15px;font-weight:500;margin-bottom:4px;}
.place-period{font-size:11px;color:var(--gold);letter-spacing:0.06em;margin-bottom:8px;}
.place-desc{font-size:12px;color:var(--ink2);line-height:1.7;}
.place-tags{display:flex;flex-wrap:wrap;gap:4px;margin-top:10px;}
.place-tag{font-size:10px;padding:2px 8px;border-radius:20px;background:rgba(74,122,80,0.07);color:var(--forest2);}

/* ── DAILY (vibe grid) ── */
.vibe-intro{font-size:14px;color:var(--ink2);line-height:1.8;margin-bottom:2rem;}
.vibe-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--ink4);border:1px solid var(--ink4);border-radius:12px;overflow:hidden;}
.vibe-cell{
  background:var(--cream);padding:1.25rem;cursor:pointer;transition:background 0.15s;
  position:relative;
}
.vibe-cell:hover{background:rgba(74,122,80,0.05);}
.vibe-cell-icon{font-size:1.6rem;margin-bottom:8px;}
.vibe-cell-title{font-size:13px;font-weight:500;margin-bottom:4px;}
.vibe-cell-text{font-size:12px;color:var(--ink3);line-height:1.6;}
.vibe-popup{
  position:fixed;inset:0;z-index:200;display:flex;align-items:center;justify-content:center;
  background:rgba(26,24,20,0.6);backdrop-filter:blur(4px);
  opacity:0;pointer-events:none;transition:opacity 0.2s;
}
.vibe-popup.show{opacity:1;pointer-events:all;}
.vibe-popup-inner{
  background:var(--cream);border-radius:20px;padding:2rem;max-width:420px;width:90%;
  transform:scale(0.95);transition:transform 0.2s;
}
.vibe-popup.show .vibe-popup-inner{transform:scale(1);}
.vibe-popup-icon{font-size:3rem;margin-bottom:1rem;}
.vibe-popup-title{font-family:var(--serif);font-size:1.6rem;margin-bottom:0.75rem;}
.vibe-popup-text{font-size:14px;color:var(--ink2);line-height:1.8;}
.vibe-popup-close{
  margin-top:1.5rem;padding:8px 20px;border-radius:20px;border:1px solid var(--ink4);
  background:transparent;cursor:pointer;font-size:13px;color:var(--ink2);transition:all 0.15s;
}
.vibe-popup-close:hover{background:var(--forest);color:var(--cream);}

/* ── FEELINGS (draggable timeline) ── */
.feelings-wrap{position:relative;}
.feelings-track-container{
  margin:2rem 0;background:var(--cream);border:1px solid var(--ink4);
  border-radius:16px;overflow:hidden;
}
.feelings-scrubber{padding:1.5rem 1.5rem 0.5rem;}
.feelings-label{font-size:11px;color:var(--ink3);letter-spacing:0.08em;margin-bottom:10px;}
input[type=range].f-range{
  width:100%;-webkit-appearance:none;height:3px;
  background:linear-gradient(to right,var(--forest) 0%,var(--forest) var(--pct,30%),var(--ink4) var(--pct,30%));
  border-radius:2px;outline:none;cursor:pointer;
}
input[type=range].f-range::-webkit-slider-thumb{
  -webkit-appearance:none;width:18px;height:18px;border-radius:50%;
  background:var(--forest);border:2px solid var(--cream);box-shadow:0 2px 8px rgba(74,122,80,0.25);
  cursor:grab;
}
.feelings-periods{display:flex;justify-content:space-between;font-size:10px;color:var(--ink4);padding:0 2px;margin-top:4px;}
.feelings-card{padding:1.5rem;border-top:1px solid var(--ink4);transition:all 0.3s;}
.feelings-date{font-size:11px;letter-spacing:0.1em;color:var(--gold);margin-bottom:6px;}
.feelings-headline{font-family:var(--serif);font-size:1.4rem;margin-bottom:8px;}
.feelings-body{font-size:13px;color:var(--ink2);line-height:1.8;}
.feelings-mood{display:flex;align-items:center;gap:6px;margin-top:10px;}
.mood-bar-wrap{flex:1;height:4px;background:var(--bg2);border-radius:2px;overflow:hidden;}
.mood-bar{height:100%;border-radius:2px;transition:width 0.5s ease;background:var(--forest);}
.mood-label{font-size:11px;color:var(--ink3);min-width:32px;text-align:right;}

/* ── WORK chapter (minimal) ── */
.work-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.work-card{background:var(--cream);border:1px solid var(--ink4);border-radius:12px;padding:1.5rem;}
.work-num{font-family:var(--serif);font-size:2.5rem;color:var(--forest);line-height:1;}
.work-label{font-size:12px;color:var(--ink3);margin-top:4px;}
.work-desc{font-size:13px;color:var(--ink2);margin-top:8px;line-height:1.6;}
.offer-row{margin-top:2rem;}
.offer-title{font-size:13px;font-weight:500;margin-bottom:10px;color:var(--ink3);letter-spacing:0.06em;}
.offer-chips{display:flex;flex-wrap:wrap;gap:8px;}
.offer-chip{
  font-size:12px;padding:6px 14px;border-radius:20px;
  border:1px solid var(--ink4);color:var(--ink3);position:relative;
}
.offer-chip.declined::after{
  content:'✕';position:absolute;top:-6px;right:-6px;
  width:16px;height:16px;background:var(--red);color:white;
  border-radius:50%;font-size:9px;display:flex;align-items:center;justify-content:center;
  line-height:16px;text-align:center;
}
.offer-chip.accepted{border-color:var(--gold);color:var(--gold);background:rgba(184,134,78,0.06);}

/* ── LETTER ── */
.letter-paper{
  background:var(--cream);border:1px solid var(--ink4);border-radius:16px;
  padding:2.5rem;font-family:var(--serif);font-size:1rem;line-height:2.1;
  color:var(--ink2);position:relative;
}
.letter-paper::before{
  content:'';position:absolute;top:3rem;left:0;right:0;
  height:1px;background:repeating-linear-gradient(90deg,var(--ink4) 0,var(--ink4) 40px,transparent 40px,transparent 60px);
  opacity:0.3;
}
.letter-paper p{margin-bottom:1rem;}
.letter-paper strong{color:var(--gold);font-weight:400;}
.letter-date{font-size:11px;color:var(--ink4);letter-spacing:0.1em;margin-bottom:2rem;font-family:var(--sans);}
.letter-sig{font-size:13px;color:var(--ink3);margin-top:1.5rem;font-family:var(--sans);}

/* ── ANIMATIONS ── */
@keyframes up{from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);}}
@keyframes tokyoGlow{0%,100%{box-shadow:0 0 0 4px rgba(184,134,78,0.2),0 8px 32px rgba(74,122,80,0.2);}50%{box-shadow:0 0 0 7px rgba(184,134,78,0.3),0 8px 40px rgba(74,122,80,0.35);}}
@keyframes starSpin{0%{transform:rotate(0deg) scale(1);}50%{transform:rotate(180deg) scale(1.2);}100%{transform:rotate(360deg) scale(1);}}
@keyframes pop{from{opacity:0;transform:scale(0.9);}to{opacity:1;transform:scale(1);}}

/* scrollbar */
.places-scroll-wrap::-webkit-scrollbar{height:4px;}
.places-scroll-wrap::-webkit-scrollbar-track{background:var(--bg2);}
.places-scroll-wrap::-webkit-scrollbar-thumb{background:var(--ink4);border-radius:2px;}

@media(max-width:600px){
  .chapters{grid-template-columns:1fr 1fr;}
  .work-grid{grid-template-columns:1fr;}
  .cards-grid{grid-template-columns:1fr 1fr;}
}
</style>
</head>
<body>

<button class="back-btn" id="back-btn" onclick="goHome()">← 回主頁</button>

<!-- ══ HOME ══ -->
<div class="view active" id="home">
  <div class="home-grain"></div>
  <div class="home-year">2024 — 2025</div>
  <h1 class="home-title">在曠野中<br>找到<span class="alt">軌道</span><br>再走入新的曠野</h1>
  <p class="home-sub">選一個章節，開始探索</p>
  <div class="chapters">
    <div class="chapters-row top">
      <div class="chapter-btn" onclick="go('firsts')">
        <div class="ch-num">01</div>
        <span class="ch-icon">✨</span>
        <div class="ch-title">人生第一次</div>
        <div class="ch-sub">翻牌解鎖</div>
      </div>
      <div class="chapter-btn" onclick="go('places')">
        <div class="ch-num">02</div>
        <span class="ch-icon">🗺</span>
        <div class="ch-title">去過的地方</div>
        <div class="ch-sub">滑動探索</div>
      </div>
      <div class="chapter-btn" onclick="go('daily')">
        <div class="ch-num">03</div>
        <span class="ch-icon">☕</span>
        <div class="ch-title">日常小事</div>
        <div class="ch-sub">點擊發現</div>
      </div>
    </div>
    <div class="chapters-row bottom">
      <div class="chapter-btn" onclick="go('feelings')">
        <div class="ch-num">04</div>
        <span class="ch-icon">🌊</span>
        <div class="ch-title">那些感受</div>
        <div class="ch-sub">拉動時間軸</div>
      </div>
      <div class="chapter-btn" onclick="go('work')">
        <div class="ch-num">05</div>
        <span class="ch-icon">💼</span>
        <div class="ch-title">工作那些事</div>
        <div class="ch-sub">數字 + 故事</div>
      </div>
    </div>
  </div>
</div>

<!-- ══ FIRSTS ══ -->
<div class="view" id="firsts">
  <div class="ch-header">
    <div class="ch-header-tag">CHAPTER 01 · 人生第一次</div>
    <h2 class="ch-header-title">翻開看看<span class="alt">你做過的事</span></h2>
  </div>
  <div class="ch-body">
    <p class="firsts-intro">這兩年，很多事都是第一次。有些嚇到自己，有些笑著想起來。點擊卡片翻面 👇</p>
    <div class="cards-grid" id="firsts-grid"></div>
  </div>
</div>

<!-- ══ PLACES ══ -->
<div class="view" id="places">
  <div class="ch-header">
    <div class="ch-header-tag">CHAPTER 02 · 足跡</div>
    <h2 class="ch-header-title">這兩年<span class="alt">去過的地方</span></h2>
  </div>
  <div class="ch-body">
    <p style="font-size:14px;color:var(--ink2);line-height:1.8;margin-bottom:1rem;">往右滑，看看那些城市留下了什麼。</p>
    <div class="places-scroll-wrap" id="places-scroll">
      <div class="places-track" id="places-track"></div>
    </div>
  </div>
</div>

<!-- ══ DAILY ══ -->
<div class="view" id="daily">
  <div class="ch-header">
    <div class="ch-header-tag">CHAPTER 03 · 日常小事</div>
    <h2 class="ch-header-title">那些<span class="alt">細碎的美好</span></h2>
  </div>
  <div class="ch-body">
    <p class="vibe-intro">大事好說，但讓人記住的往往是這些小事。點一格進去看。</p>
    <div class="vibe-grid" id="vibe-grid"></div>
  </div>
</div>

<!-- popup -->
<div class="vibe-popup" id="vibe-popup" onclick="closeVibe(event)">
  <div class="vibe-popup-inner">
    <div class="vibe-popup-icon" id="vp-icon"></div>
    <div class="vibe-popup-title" id="vp-title"></div>
    <div class="vibe-popup-text" id="vp-text"></div>
    <button class="vibe-popup-close" onclick="closeVibe()">關上</button>
  </div>
</div>

<!-- ══ FEELINGS ══ -->
<div class="view" id="feelings">
  <div class="ch-header">
    <div class="ch-header-tag">CHAPTER 04 · 內心感受</div>
    <h2 class="ch-header-title">不同時期<span class="alt">你的心情</span></h2>
  </div>
  <div class="ch-body">
    <p style="font-size:14px;color:var(--ink2);line-height:1.8;margin-bottom:1.5rem;">拖動下方的進度條，看看這兩年每個階段的心情。</p>
    <div class="feelings-track-container">
      <div class="feelings-scrubber">
        <div class="feelings-label">拖動時間軸</div>
        <input type="range" class="f-range" id="f-range" min="0" max="8" value="0" step="1" oninput="updateFeelings(this.value)">
        <div class="feelings-periods" id="f-periods"></div>
      </div>
      <div class="feelings-card" id="feelings-card"></div>
    </div>

  </div>
</div>

<!-- ══ WORK ══ -->
<div class="view" id="work">
  <div class="ch-header">
    <div class="ch-header-tag">CHAPTER 05 · 工作那些事</div>
    <h2 class="ch-header-title">職涯上<span class="alt">發生的事</span></h2>
  </div>
  <div class="ch-body">
    <div class="work-grid">
      <div class="work-card">
        <div class="work-num">14</div>
        <div class="work-label">個月遠端工作</div>
        <div class="work-desc">從多倫多到台灣，時區跨了 13 小時，一直在線。</div>
      </div>
      <div class="work-card">
        <div class="work-num">3</div>
        <div class="work-label">位下屬</div>
        <div class="work-desc">從被管理到管人，不是計畫好的，是被推著長大的。</div>
      </div>
      <div class="work-card">
        <div class="work-num">凌晨<br>8點</div>
        <div class="work-label" style="font-size:11px">才睡覺的每一天</div>
        <div class="work-desc">每晚 10 點上班，凌晨 8 點才睡。身體記得那段時間，很久才忘掉。</div>
      </div>
      <div class="work-card">
        <div class="work-num">16週</div>
        <div class="work-label">AI 訓練營</div>
        <div class="work-desc">交大 · Crew AI · AI Agent。迷茫中選擇學習，這個決定值得的。</div>
      </div>
    </div>
    <div class="offer-row">
      <div class="offer-title">OFFER 紀錄</div>
      <div class="offer-chips">
        <div class="offer-chip declined">Netflix</div>
        <div class="offer-chip declined">國際美妝大品牌</div>
        <div class="offer-chip accepted">心中那個 ✓</div>
      </div>
      <p style="font-size:12px;color:var(--ink3);margin-top:10px;line-height:1.7;">說不，是另一種勇氣。選了感覺對的，雖然還不確定對不對。</p>
    </div>
  </div>
</div>


<script>
// ── DATA ──
const FIRSTS = [
  {icon:'🍁',label:'一個人 Working Holiday',story:'沒有任何人認識，帶著一個背包降落多倫多。那種又怕又興奮的感覺，現在還記得。',year:'2024.04'},
  {icon:'🍹',label:'飲料店打工',story:'在異國城市，先求生存再談夢想。這份工作讓我知道自己能在任何地方活下去。',year:'2024.04'},
  {icon:'🌿',label:'體驗大麻',story:'在多倫多，這是合法的。就試試看吧，然後笑了一整晚哈哈。',year:'2024夏'},
  {icon:'🏔',label:'夢蓮湖',story:'大學時就說要來。站在那片藍綠色的湖面前，突然很感謝自己出發的勇氣。',year:'2024.09'},
  {icon:'🎣',label:'冰釣',story:'在冰面上鑿洞釣魚，坐在零下的空氣裡，安靜得出奇地舒服。',year:'2025.02'},
  {icon:'🎭',label:'看英語舞台劇',story:'在多倫多的劇院，全英文的演出。有些聽懂有些沒懂，但氛圍完全不一樣。',year:'2025.02'},
  {icon:'🏂',label:'單板滑雪',story:'第一次踩上雪板，摔了很多次，但滑下去那一刻真的很爽。',year:'2025.02'},
  {icon:'👗',label:'參加日本人的婚禮',story:'特別買了禮服。日本式的婚禮，莊重又溫馨，跟台灣很不一樣。男友也一起。',year:'2025.10'},
  {icon:'🤖',label:'學 AI Agent',story:'人生第一次學寫程式不是為了轉行，是因為真的想知道 AI 到底能做什麼。用 Crew AI 讓多個 AI 一起工作，很神奇。',year:'2025.10'},
];

const PLACES = [
  {emoji:'🍁',name:'多倫多',period:'2024.04 — 2025.06',bg:'#e8f0ea',desc:'一個人落地，找工作、交朋友、爬升為 leader。多倫多給了我很多，我也在這裡耗盡了自己。',tags:['Working Holiday','PR工作','WFH','脫單']},
  {emoji:'❄️',name:'Montreal',period:'2024.12 — 2025.02',bg:'#e8ecf0',desc:'和男友短暫搬去住，法語的城市，雪地裡跨年。兩個月的另一種生活節奏。',tags:['跨年','兩個人','下雪']},
  {emoji:'🏔',name:'Banff · Calgary',period:'2024.09',bg:'#eaf0e8',desc:'大學時許下的願望。站在夢蓮湖面前，那個藍綠色真的很真實。',tags:['完成願望','夢蓮湖','朋友旅遊']},
  {emoji:'🌴',name:'Los Angeles',period:'2025.03',bg:'#f0ece8',desc:'離開多倫多前先去LA玩了四五天。陽光、Freeway、完全不同的氣氛。',tags:['短暫停留','陽光','轉機']},
  {emoji:'🗼',name:'東京 ✦',period:'2025.03',bg:'#f5e6d0',highlight:true,desc:'帶著爸媽一起去。全款出國，看了富士山。那個當下覺得這一切都值得了。',tags:['帶家人','富士山','達成目標']},
  {emoji:'🏮',name:'香港 · 桂林 · 上海',period:'2025.05',bg:'#ece8f0',desc:'處理事情的旅程，後半段男友加入，桂林的山水和上海的城市感形成超強對比。',tags:['男友同行','山水','城市']},
  {emoji:'⛩',name:'日本（婚禮）',period:'2025.10',bg:'#f0eae8',desc:'參加日本人的婚禮。穿了特別買的禮服，體驗了完全不一樣的婚禮文化。',tags:['婚禮','禮服','文化體驗']},
  {emoji:'🎄',name:'香港 · 湛江 · 海南 · 深圳',period:'2025.12 聖誕節',bg:'#eaf0ec',desc:'聖誕節的南方之旅。從香港出發一路往南，湛江、海南的海岸線，再到深圳。過了一個完全不一樣的聖誕節。',tags:['聖誕節','南方','海邊','城市']},
  {emoji:'🇰🇷',name:'韓國釜山',period:'2026.03',bg:'#eceaf0',desc:'2026年初的釜山之行。海雲台的海、광안리的夜景、還有吃不完的海鮮。新的一年，新的出發。',tags:['釜山','海鮮','2026','新出發']},
];

const VIBES = [
  {icon:'☕',title:'多倫多的咖啡館文化',text:'每個社區都有自己的咖啡館，坐下來就能遇到不同國家的人。在裡面工作、交朋友，甚至被搭訕 😂'},
  {icon:'🌨',title:'第一次看到真正的雪',text:'不是台灣那種可有可無的冷，是積在地上幾十公分、呼吸都是白煙的那種。'},
  {icon:'🧑‍🍳',title:'自己開始煮飯當大廚',text:'在多倫多的廚房裡，從只會煮泡麵到能做出像樣的料理。一個人煮飯，其實挺療癒的。'},
  {icon:'🎵',title:'在多倫多的派對',text:'不同語言、不同背景的人全擠在一起，音樂很大聲，但大家都在笑。'},
  {icon:'🌅',title:'凌晨八點的天空',text:'因為倒時差，常常在台灣的凌晨八點才準備睡覺，看著窗外天色漸亮、陽光開始照進來。很孤獨，但也很特別。'},
  {icon:'🗓',title:'突然就是休假了',text:'離職後第一週，什麼計畫都沒有，就是待著。那種茫然和輕鬆同時存在的感覺。'},
  {icon:'🛁',title:'Montreal 的慢早晨',text:'和男友住在一起，週末睡到自然醒，煮咖啡，什麼計畫都沒有。那種生活節奏好像在另一個宇宙。'},
  {icon:'🌸',title:'台灣的夏天',text:'離職回來後，才發現自己已經忘記台灣的夏天是什麼感覺。那種悶熱、蟬鳴、便利商店的涼氣——原來這也是家的味道。'},
  {icon:'✈️',title:'一個人在機場',text:'這兩年坐了很多次飛機，有時興奮，有時疲憊。但每次坐在登機口等待的那個當下，都有一種「又要開始了」的感覺。'},
];

const PERIODS = [
  {date:'2024.01',headline:'分手，然後出發',body:'感情破裂。但沒有等很久——決定把這個空缺填成一個冒險。訂機票，飛多倫多。',mood:40,moodLabel:'忐忑'},
  {date:'2024.04–05',headline:'生存模式：多倫多前三個月',body:'不到兩週找到飲料店工作，一個月後進 PR 公司。那種「我可以的」的感覺，很真實。',mood:72,moodLabel:'充實'},
  {date:'2024.06–08',headline:'多倫多夏天',body:'工作穩了，開始玩。認識很多不同國家的朋友，瘋狂參加活動，被很多人搭訕哈哈。',mood:85,moodLabel:'自由'},
  {date:'2024.09',headline:'Banff，一個願望完成了',body:'站在夢蓮湖面前。大學時說要來的地方，今年來了。感謝那個出發的自己。',mood:95,moodLabel:'滿足'},
  {date:'2024.10–12',headline:'脫單 + Montreal 跨年',body:'被追了三個月後在一起。冬天搬去 Montreal，在雪地裡跨年。有點像夢。',mood:82,moodLabel:'幸福'},
  {date:'2025.01–05',headline:'最忙也最累的時候',body:'每晚 10 點上班，凌晨 8 點睡。帶下屬、管預算、倒時差工作。身體開始說不。',mood:38,moodLabel:'燃燒殆盡'},
  {date:'2025.06',headline:'說「夠了」，飛回家',body:'在多倫多待了兩週多。一切都不對勁。匆匆離職，登出多倫多，回台灣。',mood:52,moodLabel:'解脫'},
  {date:'2025.07–09',headline:'什麼都不做的那段時間',body:'休息。運動、減肥（為了禮服哈哈）。允許自己迷茫，也允許自己停下來。',mood:65,moodLabel:'漂浮'},
  {date:'2025.10–2026.02',headline:'又開始走了',body:'AI 訓練營、面試、拒 offer、選 offer。不確定，但是在動。曠野裡，但是自己選的。',mood:70,moodLabel:'再出發'},
];

// ── RENDER ──
function renderFirsts(){
  const g=document.getElementById('firsts-grid');
  g.innerHTML=FIRSTS.map((f,i)=>`
    <div class="flip-card" onclick="this.classList.toggle('flipped')">
      <div class="flip-inner">
        <div class="flip-front">
          <div class="flip-front-icon">${f.icon}</div>
          <div class="flip-front-label">${f.label}</div>
          <div class="flip-front-hint">點我翻面</div>
        </div>
        <div class="flip-back">
          <div class="flip-back-year">${f.year}</div>
          <div class="flip-back-text">${f.story}</div>
        </div>
      </div>
    </div>`).join('');
}

function renderPlaces(){
  const t=document.getElementById('places-track');
  t.innerHTML=PLACES.map(p=>`
    <div class="place-card" style="${p.highlight ? 'border:2px solid var(--gold);box-shadow:0 0 0 4px rgba(184,134,78,0.15),0 8px 32px rgba(74,122,80,0.15);animation:tokyoGlow 2s ease-in-out infinite;position:relative;' : ''}">
    ${p.highlight ? '<div style="position:absolute;top:-10px;right:12px;z-index:10;display:flex;gap:3px;"><span style="animation:starSpin 3s linear infinite;display:inline-block;font-size:14px;">✦</span><span style="animation:starSpin 3s linear infinite 0.5s;display:inline-block;font-size:10px;">✦</span><span style="animation:starSpin 3s linear infinite 1s;display:inline-block;font-size:14px;">✦</span></div>' : ''}
      <div class="place-emoji" style="background:${p.bg}">${p.emoji}</div>
      <div class="place-body">
        <div class="place-name" style="${p.highlight ? 'color:var(--gold);font-weight:600;' : ''}">${p.name}</div>
        <div class="place-period">${p.period}</div>
        <div class="place-desc">${p.desc}</div>
        <div class="place-tags">${p.tags.map(t=>`<span class="place-tag">${t}</span>`).join('')}</div>
      </div>
    </div>`).join('');
  // drag to scroll
  const wrap=document.getElementById('places-scroll');
  let isDown=false,startX,scrollLeft;
  wrap.addEventListener('mousedown',e=>{isDown=true;startX=e.pageX-wrap.offsetLeft;scrollLeft=wrap.scrollLeft;});
  wrap.addEventListener('mouseleave',()=>isDown=false);
  wrap.addEventListener('mouseup',()=>isDown=false);
  wrap.addEventListener('mousemove',e=>{if(!isDown)return;e.preventDefault();const x=e.pageX-wrap.offsetLeft;wrap.scrollLeft=scrollLeft-(x-startX)*1.2;});
}

function renderVibes(){
  const g=document.getElementById('vibe-grid');
  g.innerHTML=VIBES.map((v,i)=>`
    <div class="vibe-cell" onclick="openVibe(${i})">
      <div class="vibe-cell-icon">${v.icon}</div>
      <div class="vibe-cell-title">${v.title}</div>
      <div class="vibe-cell-text">${v.text.substring(0,40)}…</div>
    </div>`).join('');
}

function openVibe(i){
  const v=VIBES[i];
  document.getElementById('vp-icon').textContent=v.icon;
  document.getElementById('vp-title').textContent=v.title;
  document.getElementById('vp-text').textContent=v.text;
  document.getElementById('vibe-popup').classList.add('show');
}
function closeVibe(e){
  if(!e||e.target===document.getElementById('vibe-popup'))
    document.getElementById('vibe-popup').classList.remove('show');
}

function renderFeelings(){
  const wrap=document.getElementById('f-periods');
  wrap.innerHTML=PERIODS.map(p=>`<span>${p.date.split('.')[0].replace('2024','\'24').replace('2025','\'25').replace('2026','\'26')}</span>`).join('');
  updateFeelings(0);
}
function updateFeelings(i){
  const p=PERIODS[i];
  const card=document.getElementById('feelings-card');
  card.innerHTML=`
    <div class="feelings-date">${p.date}</div>
    <div class="feelings-headline">${p.headline}</div>
    <div class="feelings-body">${p.body}</div>
    <div class="feelings-mood">
      <span style="font-size:11px;color:var(--ink3);min-width:52px">心情指數</span>
      <div class="mood-bar-wrap"><div class="mood-bar" style="width:${p.mood}%"></div></div>
      <span class="mood-label">${p.moodLabel}</span>
    </div>`;
  const range=document.getElementById('f-range');
  range.style.setProperty('--pct',(i/(PERIODS.length-1)*100)+'%');
}

// ── NAV ──
function go(id){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  document.getElementById('back-btn').classList.add('show');
  window.scrollTo(0,0);
  if(id==='firsts') renderFirsts();
  if(id==='places') renderPlaces();
  if(id==='daily') renderVibes();
  if(id==='feelings') renderFeelings();
}
function goHome(){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('home').classList.add('active');
  document.getElementById('back-btn').classList.remove('show');
  window.scrollTo(0,0);
}
</script>
</body>
</html>
