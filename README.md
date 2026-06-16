cat > /mnt/user-data/outputs/vm2026.html << 'HTMLEOF'
<!DOCTYPE html>
<html lang="no">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VM 2026 Tipping</title>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: 'Segoe UI', system-ui, sans-serif; background: #080c14; color: #e8eaf0; min-height: 100vh; }

header { background: linear-gradient(160deg,#0f1c30,#080c14); border-bottom: 1px solid #1a2a40; padding: 22px 20px 14px; text-align: center; }
.badge { display:inline-block; background:#c8a84b22; border:1px solid #c8a84b55; color:#c8a84b; font-size:10px; letter-spacing:.2em; padding:3px 12px; border-radius:20px; margin-bottom:8px; text-transform:uppercase; }
h1 { font-size:24px; font-weight:900; letter-spacing:.1em; text-transform:uppercase; }
.sub { font-size:11px; color:#5a6b80; margin-top:4px; }

.status-bar { display:flex; align-items:center; justify-content:center; gap:8px; margin-top:10px; flex-wrap:wrap; }
.status-dot { width:8px; height:8px; border-radius:50%; background:#4caf50; flex-shrink:0; }
.status-dot.loading { background:#f0a500; animation: pulse 1s infinite; }
.status-dot.error { background:#f44336; }
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.3} }
.status-txt { font-size:11px; color:#7a8ba8; }
.refresh-btn { background:#c8a84b22; border:1px solid #c8a84b55; color:#c8a84b; font-size:11px; padding:3px 12px; border-radius:12px; cursor:pointer; font-weight:600; }
.refresh-btn:disabled { opacity:.4; cursor:default; }

.tabs { display:flex; gap:8px; padding:14px 14px 0; max-width:560px; margin:0 auto; }
.tab { flex:1; padding:9px 0; background:#0f1520; border:1px solid #1e2d47; border-radius:8px; color:#5a6b80; font-size:13px; font-weight:600; cursor:pointer; text-align:center; transition:all .2s; }
.tab.active { background:#c8a84b; border-color:#c8a84b; color:#080c14; }

.view { display:none; max-width:560px; margin:0 auto; padding:14px 14px 60px; }
.view.active { display:block; }

.card { display:flex; align-items:center; gap:12px; background:#0f1520; border:1px solid #1a2840; border-radius:10px; padding:13px 14px; margin-bottom:8px; }
.card.leader { border-color:#c8a84b55; background:#141c2a; box-shadow:0 0 20px #c8a84b15; }
.rank { font-size:18px; width:28px; text-align:center; flex-shrink:0; }
.rank.num { font-size:13px; color:#5a6b80; font-weight:700; }
.pname { font-size:16px; font-weight:700; flex:1; }
.pts { font-size:22px; font-weight:900; color:#c8a84b; text-align:right; }
.pts-detail { font-size:10px; color:#4a5a70; text-align:right; margin-top:1px; }

.day-header { display:flex; justify-content:space-between; align-items:center; font-size:11px; font-weight:700; color:#8a9ab0; letter-spacing:.1em; text-transform:uppercase; padding:8px 10px; background:#0d1422; border-radius:8px; cursor:pointer; border:1px solid #1a2840; margin-bottom:4px; margin-top:10px; user-select:none; }
.matches-container { display:none; }
.matches-container.open { display:block; }
.match { background:#0f1520; border:1px solid #1a2840; border-radius:8px; padding:10px 12px; margin-bottom:5px; }
.match.pending { opacity:.45; }
.match-top { display:flex; justify-content:space-between; align-items:center; margin-bottom:7px; gap:8px; }
.gbadge { font-size:9px; background:#1a2840; color:#5a6b80; padding:1px 5px; border-radius:3px; margin-right:6px; letter-spacing:.08em; flex-shrink:0; }
.mteams { font-size:12px; font-weight:600; flex:1; }
.chip { font-size:14px; font-weight:900; color:#c8a84b; background:#1a2030; padding:3px 10px; border-radius:5px; border:1px solid #c8a84b33; white-space:nowrap; flex-shrink:0; }
.chip.pending { color:#3a4a5a; border-color:#1a2840; }
.chip.live { color:#f44336; border-color:#f4433655; animation: livepulse 2s infinite; }
@keyframes livepulse { 0%,100%{opacity:1} 50%{opacity:.6} }
.tips { display:grid; grid-template-columns:repeat(6,1fr); gap:3px; }
.tip { text-align:center; padding:4px 2px; border-radius:4px; border:1px solid #222; background:#141414; }
.tip.exact { background:#1a3a1a; border-color:#2a6a2a; }
.tip.hx2 { background:#0f2030; border-color:#1e4a70; }
.tname { font-size:9px; color:#4a5a70; display:block; margin-bottom:2px; }
.tguess { font-size:10px; font-weight:700; color:#444; display:block; }
.tip.exact .tguess { color:#4caf50; }
.tip.hx2 .tguess { color:#42a5f5; }
.tpts { font-size:9px; display:block; color:#333; }
.tip.exact .tpts { color:#4caf50; }
.tip.hx2 .tpts { color:#42a5f5; }

.legend { display:flex; gap:12px; flex-wrap:wrap; margin-bottom:12px; }
.legend span { font-size:11px; color:#5a6b80; display:flex; align-items:center; gap:4px; }
.dot { display:inline-block; width:10px; height:10px; border-radius:2px; }
.section-lbl { font-size:10px; letter-spacing:.15em; text-transform:uppercase; color:#5a6b80; margin:16px 0 10px; }
.spinner { text-align:center; padding:40px; color:#5a6b80; font-size:14px; }
</style>
</head>
<body>

<header>
  <div class="badge">FIFA VM 2026</div>
  <h1>⚽ Tippeligaen</h1>
  <p class="sub">6 deltakere · 4p eksakt · 2p riktig H/U/B</p>
  <div class="status-bar">
    <div class="status-dot" id="sdot"></div>
    <span class="status-txt" id="stxt">Laster...</span>
    <button class="refresh-btn" id="rbtn" onclick="loadScores()">↻ Oppdater</button>
  </div>
</header>

<div class="tabs">
  <button class="tab active" onclick="showTab('standings',this)">🏆 Tabell</button>
  <button class="tab" onclick="showTab('matches',this)">⚽ Kamper</button>
</div>

<div id="standings" class="view active"><div class="spinner">Laster resultater...</div></div>
<div id="matches" class="view"><div class="spinner">Laster kamper...</div></div>

<script>
const PLAYERS = ['Staals','Kong','Dox','Jojo','Marko','Barra'];
const MEDAL = ['🥇','🥈','🥉'];

// All 72 group stage matches with tips
// Tips order matches PLAYERS order: Staals, Kong, Dox, Jojo, Marko, Barra
const MATCHES = [
  {id:1,  day:'Tors 11. jun', g:'A', h:'Mexico',              a:'South Africa',     tips:['3-0','2-1','2-0','3-1','2-1','3-0']},
  {id:2,  day:'Fre 12. jun',  g:'A', h:'South Korea',         a:'Czech Republic',   tips:['2-1','1-1','1-1','2-3','1-0','1-2']},
  {id:3,  day:'Fre 12. jun',  g:'B', h:'Canada',              a:'Bosnia-Herzegovina',tips:['1-1','0-1','2-1','2-0','1-1','2-0']},
  {id:4,  day:'Lør 13. jun',  g:'D', h:'United States',       a:'Paraguay',         tips:['2-1','1-1','0-0','2-3','3-0','2-1']},
  {id:5,  day:'Lør 13. jun',  g:'B', h:'Qatar',               a:'Switzerland',      tips:['0-3','0-3','0-1','1-3','0-2','0-3']},
  {id:6,  day:'Søn 14. jun',  g:'C', h:'Brazil',              a:'Morocco',          tips:['2-2','1-1','3-1','2-2','2-1','2-1']},
  {id:7,  day:'Søn 14. jun',  g:'C', h:'Haiti',               a:'Scotland',         tips:['0-3','0-0','0-3','0-2','0-3','0-2']},
  {id:8,  day:'Søn 14. jun',  g:'D', h:'Australia',           a:'Turkey',           tips:['0-1','0-2','1-3','0-2','1-2','0-2']},
  {id:9,  day:'Søn 14. jun',  g:'E', h:'Germany',             a:'Curaçao',          tips:['6-0','3-0','5-0','4-0','4-0','3-0']},
  {id:10, day:'Søn 14. jun',  g:'F', h:'Netherlands',         a:'Japan',            tips:['1-1','2-1','1-2','1-2','1-1','3-1']},
  {id:11, day:'Man 15. jun',  g:'E', h:"Côte d'Ivoire",       a:'Ecuador',          tips:['1-2','1-0','1-1','0-3','3-3','1-2']},
  {id:12, day:'Man 15. jun',  g:'F', h:'Sweden',              a:'Tunisia',          tips:['2-1','1-1','1-1','2-2','1-1','1-0']},
  {id:13, day:'Man 15. jun',  g:'H', h:'Spain',               a:'Cabo Verde',       tips:['3-0','3-0','3-0','5-0','3-0','3-0']},
  {id:14, day:'Man 15. jun',  g:'G', h:'Belgium',             a:'Egypt',            tips:['2-2','2-0','1-0','2-1','2-1','2-0']},
  {id:15, day:'Man 15. jun',  g:'H', h:'Saudi Arabia',        a:'Uruguay',          tips:['0-2','0-2','0-3','0-3','2-2','0-1']},
  {id:16, day:'Man 15. jun',  g:'G', h:'Iran',                a:'New Zealand',      tips:['2-0','1-1','0-0','2-1','1-1','1-0']},
  {id:17, day:'Tir 16. jun',  g:'I', h:'France',              a:'Senegal',          tips:['2-2','3-1','2-1','2-1','3-1','2-0']},
  {id:18, day:'Tir 16. jun',  g:'I', h:'Iraq',                a:'Norway',           tips:['1-2','1-3','1-1','1-3','1-4','1-2']},
  {id:19, day:'Tir 16. jun',  g:'J', h:'Argentina',           a:'Algeria',          tips:['3-1','2-0','2-0','2-0','2-1','3-1']},
  {id:20, day:'Tir 16. jun',  g:'J', h:'Austria',             a:'Jordan',           tips:['2-2','1-0','2-1','2-0','3-0','2-0']},
  {id:21, day:'Ons 17. jun',  g:'K', h:'Portugal',            a:'DR Congo',         tips:['3-1','3-0','4-1','3-0','3-1','3-1']},
  {id:22, day:'Ons 17. jun',  g:'L', h:'England',             a:'Croatia',          tips:['1-1','2-1','2-2','3-1','2-2','2-1']},
  {id:23, day:'Tors 18. jun', g:'L', h:'Ghana',               a:'Panama',           tips:['1-2','1-0','4-1','2-0','2-0','2-0']},
  {id:24, day:'Tors 18. jun', g:'K', h:'Uzbekistan',          a:'Colombia',         tips:['0-1','0-3','0-2','2-2','1-1','0-2']},
  {id:25, day:'Tors 18. jun', g:'A', h:'Czech Republic',      a:'South Africa',     tips:['1-1','2-0','1-0','0-1','2-0','2-1']},
  {id:26, day:'Tors 18. jun', g:'B', h:'Switzerland',         a:'Bosnia-Herzegovina',tips:['2-0','2-1','2-0','2-0','2-1','2-1']},
  {id:27, day:'Fre 19. jun',  g:'B', h:'Canada',              a:'Qatar',            tips:['1-0','1-1','3-0','1-2','3-1','2-0']},
  {id:28, day:'Fre 19. jun',  g:'A', h:'Mexico',              a:'South Korea',      tips:['3-1','1-2','2-2','2-0','1-1','2-1']},
  {id:29, day:'Fre 19. jun',  g:'D', h:'United States',       a:'Australia',        tips:['2-2','1-0','2-2','2-1','2-2','3-1']},
  {id:30, day:'Lør 20. jun',  g:'C', h:'Scotland',            a:'Morocco',          tips:['0-3','0-2','1-2','1-3','1-2','1-3']},
  {id:31, day:'Lør 20. jun',  g:'C', h:'Brazil',              a:'Haiti',            tips:['4-1','4-0','5-0','4-0','4-1','3-0']},
  {id:32, day:'Lør 20. jun',  g:'D', h:'Turkey',              a:'Paraguay',         tips:['3-1','0-0','2-0','2-0','2-0','2-0']},
  {id:33, day:'Lør 20. jun',  g:'F', h:'Netherlands',         a:'Sweden',           tips:['3-2','3-0','3-1','3-1','3-0','2-0']},
  {id:34, day:'Lør 20. jun',  g:'E', h:'Germany',             a:"Côte d'Ivoire",    tips:['2-1','2-1','3-2','3-0','1-2','4-0']},
  {id:35, day:'Søn 21. jun',  g:'E', h:'Ecuador',             a:'Curaçao',          tips:['3-1','1-1','3-1','2-0','2-0','2-0']},
  {id:36, day:'Søn 21. jun',  g:'F', h:'Tunisia',             a:'Japan',            tips:['0-1','0-2','2-2','0-1','0-2','0-2']},
  {id:37, day:'Søn 21. jun',  g:'H', h:'Spain',               a:'Saudi Arabia',     tips:['1-0','4-0','3-0','3-0','3-1','4-0']},
  {id:38, day:'Søn 21. jun',  g:'G', h:'Belgium',             a:'Iran',             tips:['2-2','3-0','2-0','3-1','3-0','3-0']},
  {id:39, day:'Man 22. jun',  g:'H', h:'Uruguay',             a:'Cabo Verde',       tips:['2-0','2-1','2-0','3-1','2-0','2-0']},
  {id:40, day:'Man 22. jun',  g:'G', h:'New Zealand',         a:'Egypt',            tips:['0-3','1-1','1-2','2-2','0-2','0-1']},
  {id:41, day:'Man 22. jun',  g:'J', h:'Argentina',           a:'Austria',          tips:['3-0','2-1','0-0','2-1','2-1','2-1']},
  {id:42, day:'Man 22. jun',  g:'I', h:'France',              a:'Iraq',             tips:['3-2','3-0','3-0','4-0','2-0','3-0']},
  {id:43, day:'Tir 23. jun',  g:'I', h:'Norway',              a:'Senegal',          tips:['2-2','1-1','2-1','2-2','1-1','1-2']},
  {id:44, day:'Tir 23. jun',  g:'J', h:'Jordan',              a:'Algeria',          tips:['2-3','1-3','0-1','1-1','1-2','0-2']},
  {id:45, day:'Tir 23. jun',  g:'K', h:'Portugal',            a:'Uzbekistan',       tips:['3-1','4-1','2-0','2-2','3-0','3-0']},
  {id:46, day:'Tir 23. jun',  g:'L', h:'England',             a:'Ghana',            tips:['2-0','3-0','1-0','2-0','1-2','3-1']},
  {id:47, day:'Ons 24. jun',  g:'L', h:'Panama',              a:'Croatia',          tips:['1-2','1-2','1-2','1-2','0-2','0-2']},
  {id:48, day:'Ons 24. jun',  g:'K', h:'Colombia',            a:'DR Congo',         tips:['3-2','2-1','1-0','2-0','2-1','2-0']},
  {id:49, day:'Ons 24. jun',  g:'B', h:'Switzerland',         a:'Canada',           tips:['2-1','2-0','1-0','2-1','1-0','2-1']},
  {id:50, day:'Ons 24. jun',  g:'B', h:'Bosnia-Herzegovina',  a:'Qatar',            tips:['2-1','2-0','1-0','2-2','2-0','1-0']},
  {id:51, day:'Tors 25. jun', g:'C', h:'Scotland',            a:'Brazil',           tips:['1-3','1-3','1-1','1-3','1-0','1-3']},
  {id:52, day:'Tors 25. jun', g:'C', h:'Morocco',             a:'Haiti',            tips:['5-0','2-0','4-0','3-0','3-0','2-0']},
  {id:53, day:'Tors 25. jun', g:'A', h:'Czech Republic',      a:'Mexico',           tips:['1-1','2-2','1-2','1-4','1-3','1-3']},
  {id:54, day:'Tors 25. jun', g:'A', h:'South Africa',        a:'South Korea',      tips:['1-2','0-1','0-2','1-2','0-2','1-2']},
  {id:55, day:'Tors 25. jun', g:'E', h:'Ecuador',             a:'Germany',          tips:['1-1','0-1','1-1','1-2','1-2','1-2']},
  {id:56, day:'Tors 25. jun', g:'E', h:'Curaçao',             a:"Côte d'Ivoire",    tips:['1-2','0-2','0-3','4-2','0-2','1-0']},
  {id:57, day:'Fre 26. jun',  g:'F', h:'Tunisia',             a:'Netherlands',      tips:['0-1','1-2','0-1','0-1','1-2','0-3']},
  {id:58, day:'Fre 26. jun',  g:'F', h:'Japan',               a:'Sweden',           tips:['1-0','2-0','1-0','2-1','1-1','2-1']},
  {id:59, day:'Fre 26. jun',  g:'D', h:'Turkey',              a:'United States',    tips:['1-1','2-1','2-1','2-2','2-0','1-2']},
  {id:60, day:'Fre 26. jun',  g:'D', h:'Paraguay',            a:'Australia',        tips:['2-2','1-1','1-1','2-0','1-2','1-0']},
  {id:61, day:'Fre 26. jun',  g:'I', h:'Norway',              a:'France',           tips:['1-3','1-2','1-1','3-2','2-2','0-2']},
  {id:62, day:'Fre 26. jun',  g:'I', h:'Senegal',             a:'Iraq',             tips:['2-0','2-0','2-0','4-0','1-0','2-0']},
  {id:63, day:'Lør 27. jun',  g:'H', h:'Uruguay',             a:'Spain',            tips:['1-1','1-1','1-1','1-2','1-3','1-2']},
  {id:64, day:'Lør 27. jun',  g:'H', h:'Cabo Verde',          a:'Saudi Arabia',     tips:['1-1','2-1','0-0','0-0','1-2','1-2']},
  {id:65, day:'Lør 27. jun',  g:'G', h:'New Zealand',         a:'Belgium',          tips:['0-1','0-2','1-2','0-2','1-3','0-2']},
  {id:66, day:'Lør 27. jun',  g:'G', h:'Egypt',               a:'Iran',             tips:['2-1','1-0','2-1','0-0','1-1','2-1']},
  {id:67, day:'Lør 27. jun',  g:'L', h:'Panama',              a:'England',          tips:['0-0','0-2','0-2','2-2','0-3','0-3']},
  {id:68, day:'Lør 27. jun',  g:'L', h:'Croatia',             a:'Ghana',            tips:['3-1','1-0','1-1','1-2','1-0','2-0']},
  {id:69, day:'Søn 28. jun',  g:'K', h:'Colombia',            a:'Portugal',         tips:['2-2','1-1','1-3','2-2','2-2','1-2']},
  {id:70, day:'Søn 28. jun',  g:'K', h:'DR Congo',            a:'Uzbekistan',       tips:['1-1','2-1','2-1','1-2','1-0','2-0']},
  {id:71, day:'Søn 28. jun',  g:'J', h:'Jordan',              a:'Argentina',        tips:['0-3','0-3','1-3','0-4','0-2','1-4']},
  {id:72, day:'Søn 28. jun',  g:'J', h:'Algeria',             a:'Austria',          tips:['2-2','1-1','2-2','1-1','0-2','2-1']},
];

// Name aliases to match openfootball API team names to our match list
const ALIASES = {
  'Ivory Coast': "Côte d'Ivoire",
  'Cote d\'Ivoire': "Côte d'Ivoire",
  "Côte d'Ivoire": "Côte d'Ivoire",
  'USA': 'United States',
  'US': 'United States',
  'Bosnia & Herzegovina': 'Bosnia-Herzegovina',
  'Bosnia and Herzegovina': 'Bosnia-Herzegovina',
  'Bosnia-Hercegovina': 'Bosnia-Herzegovina',
  'Türkiye': 'Turkey',
  'Türkei': 'Turkey',
  'Korea Republic': 'South Korea',
  'Republic of Korea': 'South Korea',
  'Czechia': 'Czech Republic',
  'Czech Rep.': 'Czech Republic',
  'Cabo Verde': 'Cabo Verde',
  'Cape Verde': 'Cabo Verde',
  'DR Congo': 'DR Congo',
  'Congo DR': 'DR Congo',
  'Democratic Republic of Congo': 'DR Congo',
  'Curacao': 'Curaçao',
};

function norm(name) {
  if (!name) return '';
  return (ALIASES[name] || name).trim();
}

// Confirmed results we already know (fallback + seed)
const SEED = {
  1:'2-0', 2:'2-1', 3:'1-1', 4:'4-1', 5:'1-1',
  6:'1-1', 7:'0-1', 8:'2-0', 9:'7-1', 10:'2-2',
  11:'1-0', 12:'5-1', 13:'0-0', 14:'1-1', 15:'1-1', 16:'2-2',
};

let RESULTS = { ...SEED };

function hx2(s) { const [h,a]=s.split('-').map(Number); return h>a?'H':h<a?'B':'U'; }
function pts(actual, tip) {
  if (!actual) return null;
  if (actual === tip) return 4;
  if (hx2(actual) === hx2(tip)) return 2;
  return 0;
}

function setStatus(state, msg) {
  const dot = document.getElementById('sdot');
  dot.className = 'status-dot' + (state==='loading'?' loading':state==='error'?' error':'');
  document.getElementById('stxt').textContent = msg;
  document.getElementById('rbtn').disabled = state==='loading';
}

async function loadScores() {
  setStatus('loading', 'Henter live resultater...');
  try {
    const url = 'https://raw.githubusercontent.com/openfootball/worldcup.json/master/2026/worldcup.json';
    const res = await fetch(url + '?nocache=' + Date.now());
    if (!res.ok) throw new Error('HTTP ' + res.status);
    const data = await res.json();

    let updated = 0;
    (data.matches || []).forEach(m => {
      if (!m.score || !m.score.ft) return;
      const [hg, ag] = m.score.ft;
      const scoreStr = hg + '-' + ag;
      const h = norm(m.team1);
      const a = norm(m.team2);
      // Find matching match in our list
      const match = MATCHES.find(mx => norm(mx.h) === h && norm(mx.a) === a);
      if (match) {
        if (RESULTS[match.id] !== scoreStr) updated++;
        RESULTS[match.id] = scoreStr;
      }
    });

    const played = Object.keys(RESULTS).length;
    const now = new Date().toLocaleTimeString('no-NO', {hour:'2-digit',minute:'2-digit'});
    setStatus('ok', `✓ Oppdatert ${now} · ${played} kamper spilt`);
    render();
  } catch(e) {
    // Still render with seed data
    setStatus('error', '⚠ Live-henting feilet · viser siste kjente data');
    render();
  }
}

function render() {
  renderStandings();
  renderMatches();
}

function renderStandings() {
  const scores = PLAYERS.map((name, pi) => {
    let tot=0, ex=0, hx=0, played=0;
    MATCHES.forEach(m => {
      const a = RESULTS[m.id];
      if (!a) return;
      played++;
      const p = pts(a, m.tips[pi]);
      tot += p;
      if (p===4) ex++;
      else if (p===2) hx++;
    });
    return {name, tot, ex, hx, played};
  }).sort((a,b) => b.tot-a.tot || b.ex-a.ex);

  const played = Object.keys(RESULTS).length;
  document.getElementById('standings').innerHTML = scores.map((p,i) => `
    <div class="card${i===0?' leader':''}">
      <div class="rank${i<3?'':' num'}">${i<3?MEDAL[i]:i+1}</div>
      <div class="pname">${p.name}</div>
      <div>
        <div class="pts">${p.tot}p</div>
        <div class="pts-detail">${p.ex} eksakte · ${p.hx} H/U/B · ${p.played}/${played}</div>
      </div>
    </div>`).join('');
}

function renderMatches() {
  const byDay = {};
  MATCHES.forEach(m => { if (!byDay[m.day]) byDay[m.day]=[]; byDay[m.day].push(m); });

  let html = `<div class="legend">
    <span><span class="dot" style="background:#2a6a2a;border:1px solid #4caf50"></span>Eksakt (4p)</span>
    <span><span class="dot" style="background:#1e4a70;border:1px solid #42a5f5"></span>H/U/B (2p)</span>
    <span><span class="dot" style="background:#2a2a2a;border:1px solid #444"></span>Bom (0p)</span>
  </div>`;

  Object.entries(byDay).forEach(([day, matches], di) => {
    const played = matches.filter(m => RESULTS[m.id]).length;
    const dayId = 'day' + di;
    // Auto-open first day with unplayed matches, or last played day
    const hasUnplayed = matches.some(m => !RESULTS[m.id]);
    const allPlayed = played === matches.length;

    html += `
      <div class="day-header" onclick="toggleDay('${dayId}')">
        <span>${day}</span>
        <span style="font-size:11px;color:#7a8ba8">${played}/${matches.length} spilt ▾</span>
      </div>
      <div class="matches-container${hasUnplayed||allPlayed?'':''}" id="${dayId}">`;

    matches.forEach(m => {
      const a = RESULTS[m.id];
      const tipCells = m.tips.map((tip,pi) => {
        const p = a ? pts(a,tip) : null;
        const cls = p===4?'exact':p===2?'hx2':'';
        return `<div class="tip ${cls}">
          <span class="tname">${PLAYERS[pi]}</span>
          <span class="tguess">${tip}</span>
          ${p!==null?`<span class="tpts">+${p}</span>`:''}
        </div>`;
      }).join('');

      // Show display name (Norwegian-ish)
      const teamDisplay = m.g + ': ' + m.h.replace('United States','USA').replace('Czech Republic','Tsjekkia').replace("Côte d'Ivoire",'Elfenbenskysten').replace('Bosnia-Herzegovina','Bosnia').replace('South Africa','Sør-Afrika').replace('South Korea','Sør-Korea').replace('Saudi Arabia','Saudi-Arabia').replace('New Zealand','New Zealand').replace('DR Congo','DR Kongo') + ' – ' + m.a.replace('United States','USA').replace('Czech Republic','Tsjekkia').replace("Côte d'Ivoire",'Elfenbenskysten').replace('Bosnia-Herzegovina','Bosnia').replace('South Africa','Sør-Afrika').replace('South Korea','Sør-Korea').replace('Saudi Arabia','Saudi-Arabia').replace('DR Congo','DR Kongo');

      html += `<div class="match${a?'':' pending'}">
        <div class="match-top">
          <div style="display:flex;align-items:center;flex:1;min-width:0">
            <span class="gbadge">Gr.${m.g}</span>
            <span class="mteams">${m.h.replace('United States','USA').replace("Côte d'Ivoire",'Elfenbenskysten').replace('Bosnia-Herzegovina','Bosnia').replace('South Africa','Sør-Afrika').replace('South Korea','Sør-Korea').replace('Saudi Arabia','Saudi-Arabia').replace('Czech Republic','Tsjekkia').replace('DR Congo','DR Kongo')} – ${m.a.replace('United States','USA').replace("Côte d'Ivoire",'Elfenbenskysten').replace('Bosnia-Herzegovina','Bosnia').replace('South Africa','Sør-Afrika').replace('South Korea','Sør-Korea').replace('Saudi Arabia','Saudi-Arabia').replace('Czech Republic','Tsjekkia').replace('DR Congo','DR Kongo')}</span>
          </div>
          <div class="chip${a?'':' pending'}">${a||'–'}</div>
        </div>
        <div class="tips">${tipCells}</div>
      </div>`;
    });
    html += `</div>`;
  });

  document.getElementById('matches').innerHTML = html;

  // Auto-open the most recent played day and the next upcoming day
  const byDayEntries = Object.entries(byDay);
  let lastPlayedIdx = -1;
  byDayEntries.forEach(([day,matches],i) => {
    if (matches.some(m => RESULTS[m.id])) lastPlayedIdx = i;
  });
  if (lastPlayedIdx >= 0) {
    const el = document.getElementById('day'+lastPlayedIdx);
    if (el) el.classList.add('open');
  }
}

function toggleDay(id) {
  document.getElementById(id).classList.toggle('open');
}

function showTab(id, btn) {
  document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  btn.classList.add('active');
}

// Load on start, then auto-refresh every 5 min
loadScores();
setInterval(loadScores, 5 * 60 * 1000);
</script>
</body>
</html>
HTMLEOF
echo "Done. $(wc -c < /mnt/user-data/outputs/vm2026.html) bytes"