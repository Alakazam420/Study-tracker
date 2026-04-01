# Study-tracker
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Study Tracker — 60 Days</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
:root {
  --bg: #0d0f14;
  --surface: #13161e;
  --surface2: #1a1e28;
  --surface3: #222736;
  --accent: #6c63ff;
  --accent2: #ff6584;
  --accent3: #43e97b;
  --gold: #f5c842;
  --text: #e8eaf2;
  --text2: #8b90a7;
  --text3: #555a72;
  --border: #2a2f42;
  --mono: 'Space Mono', monospace;
  --sans: 'DM Sans', sans-serif;
  --radius: 12px;
  --radius-lg: 20px;
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  font-family:var(--sans);
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  overflow-x:hidden;
}

/* BG grid */
body::before{
  content:'';
  position:fixed;
  inset:0;
  background-image:
    linear-gradient(rgba(108,99,255,.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(108,99,255,.03) 1px, transparent 1px);
  background-size:40px 40px;
  pointer-events:none;
  z-index:0;
}

.wrap{position:relative;z-index:1;max-width:960px;margin:0 auto;padding:24px 16px 60px}

/* ── HEADER ── */
header{
  display:flex;align-items:center;justify-content:space-between;
  margin-bottom:32px;flex-wrap:wrap;gap:12px;
}
.logo{
  font-family:var(--mono);
  font-size:13px;
  color:var(--text2);
  letter-spacing:.1em;
  text-transform:uppercase;
}
.logo span{color:var(--accent)}
.date-badge{
  font-family:var(--mono);
  font-size:11px;
  color:var(--text2);
  background:var(--surface2);
  border:1px solid var(--border);
  border-radius:6px;
  padding:6px 12px;
}

/* ── DAY COUNTDOWN ── */
.countdown-section{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  padding:28px;
  margin-bottom:20px;
  position:relative;
  overflow:hidden;
}
.countdown-section::after{
  content:'';
  position:absolute;top:-60px;right:-60px;
  width:200px;height:200px;
  background:radial-gradient(circle, rgba(108,99,255,.12) 0%, transparent 70%);
  pointer-events:none;
}
.countdown-top{display:flex;align-items:flex-start;justify-content:space-between;flex-wrap:wrap;gap:16px;margin-bottom:24px}
.countdown-main{}
.day-big{
  font-family:var(--mono);
  font-size:64px;
  font-weight:700;
  color:var(--accent);
  line-height:1;
  margin-bottom:4px;
}
.day-label{font-size:14px;color:var(--text2);font-weight:300}
.day-label strong{color:var(--text);font-weight:500}
.countdown-stats{display:flex;gap:20px;flex-wrap:wrap}
.cstat{text-align:center}
.cstat .cv{font-family:var(--mono);font-size:22px;font-weight:700;color:var(--text)}
.cstat .cl{font-size:11px;color:var(--text3);margin-top:2px;text-transform:uppercase;letter-spacing:.06em}

/* Progress bar row */
.bar-label{display:flex;justify-content:space-between;font-size:11px;color:var(--text3);margin-bottom:6px;font-family:var(--mono)}
.seg-bar{display:flex;gap:2px;height:10px}
.seg{flex:1;border-radius:2px;background:var(--surface3);transition:background .3s}
.seg.done-seg{background:var(--accent)}
.seg.today-seg{background:var(--accent2)}

/* ── DAILY STUDY TIMER ── */
.timer-section{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  padding:28px;
  margin-bottom:20px;
}
.section-title{
  font-family:var(--mono);
  font-size:11px;
  text-transform:uppercase;
  letter-spacing:.1em;
  color:var(--text3);
  margin-bottom:20px;
}
.timer-core{display:flex;align-items:center;gap:24px;flex-wrap:wrap;margin-bottom:20px}
.timer-display{
  font-family:var(--mono);
  font-size:52px;
  font-weight:700;
  color:var(--text);
  letter-spacing:.05em;
  min-width:230px;
}
.timer-display.running{color:var(--accent3)}
.timer-display.done-color{color:var(--gold)}
.timer-controls{display:flex;gap:10px;flex-wrap:wrap}
.btn{
  font-family:var(--mono);font-size:12px;
  padding:10px 20px;
  border-radius:8px;
  border:1px solid var(--border);
  background:var(--surface2);
  color:var(--text2);
  cursor:pointer;
  letter-spacing:.05em;
  transition:all .2s;
}
.btn:hover{background:var(--surface3);color:var(--text);border-color:var(--text3)}
.btn.primary{background:var(--accent);border-color:var(--accent);color:#fff}
.btn.primary:hover{opacity:.85}
.btn.danger{background:transparent;border-color:var(--accent2);color:var(--accent2)}
.btn.success-btn{background:var(--accent3);border-color:var(--accent3);color:#0d0f14}

/* Radial progress */
.timer-radial{position:relative;width:120px;height:120px;flex-shrink:0}
.timer-radial svg{transform:rotate(-90deg)}
.radial-bg{fill:none;stroke:var(--surface3);stroke-width:8}
.radial-fg{fill:none;stroke:var(--accent3);stroke-width:8;stroke-linecap:round;transition:stroke-dashoffset .5s,stroke .3s}
.radial-label{
  position:absolute;inset:0;display:flex;align-items:center;justify-content:center;
  font-family:var(--mono);font-size:14px;font-weight:700;color:var(--text);
  flex-direction:column;gap:2px;
}
.radial-label span{font-size:10px;color:var(--text3)}

/* Goal hours bar */
.goal-bar-wrap{margin-bottom:8px}
.goal-bar-track{height:8px;background:var(--surface3);border-radius:4px;overflow:hidden;margin:6px 0}
.goal-bar-fill{height:100%;border-radius:4px;background:linear-gradient(90deg,var(--accent3),var(--gold));transition:width .5s}
.goal-info{display:flex;justify-content:space-between;font-size:11px;color:var(--text3);font-family:var(--mono)}

/* session log */
.session-log{margin-top:14px}
.session-log-title{font-size:11px;color:var(--text3);margin-bottom:8px;font-family:var(--mono);text-transform:uppercase;letter-spacing:.06em}
.log-entries{display:flex;flex-wrap:wrap;gap:6px}
.log-chip{
  font-family:var(--mono);font-size:10px;
  background:var(--surface2);border:1px solid var(--border);
  border-radius:6px;padding:4px 10px;color:var(--text2);
}

/* ── SUBJECTS ── */
.subjects-section{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  padding:28px;
  margin-bottom:20px;
}
.subj-grid{display:flex;flex-direction:column;gap:8px}
.subj-card{
  display:grid;
  grid-template-columns:32px 1fr auto auto auto;
  align-items:center;
  gap:12px;
  padding:14px 16px;
  background:var(--surface2);
  border:1px solid var(--border);
  border-radius:var(--radius);
  transition:border-color .2s,background .2s;
  position:relative;
  overflow:hidden;
}
.subj-card.active-subj{border-color:var(--accent);background:rgba(108,99,255,.06)}
.subj-card.done-subj{border-color:var(--accent3);opacity:.75}
.subj-card::before{
  content:'';
  position:absolute;left:0;top:0;bottom:0;width:3px;
  background:var(--c,var(--border));
  border-radius:2px 0 0 2px;
}
.subj-num{
  font-family:var(--mono);font-size:12px;
  color:var(--text3);text-align:center;
  font-weight:700;
}
.active-subj .subj-num{color:var(--accent)}
.done-subj .subj-num{color:var(--accent3)}
.subj-info{}
.subj-name{font-size:14px;font-weight:500;color:var(--text);margin-bottom:2px}
.subj-dates{font-size:11px;color:var(--text3);font-family:var(--mono)}
.subj-bar-wrap{width:80px}
.subj-bar-bg{height:4px;background:var(--surface3);border-radius:2px;overflow:hidden}
.subj-bar-fg{height:100%;border-radius:2px;transition:width .4s}
.subj-pct{font-family:var(--mono);font-size:11px;color:var(--text2);min-width:30px;text-align:right}
.subj-btn{
  font-family:var(--mono);font-size:10px;
  padding:5px 12px;
  border-radius:6px;
  border:1px solid var(--border);
  background:transparent;
  color:var(--text3);
  cursor:pointer;
  white-space:nowrap;
  transition:all .2s;
}
.subj-btn:hover{color:var(--text);border-color:var(--text3)}
.done-subj .subj-btn{border-color:var(--accent3);color:var(--accent3)}

/* ── CALENDAR ── */
.cal-section{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  padding:28px;
}
.cal-legend{display:flex;flex-wrap:wrap;gap:10px;margin-bottom:16px}
.leg-item{display:flex;align-items:center;gap:6px;font-size:11px;color:var(--text3)}
.leg-dot{width:8px;height:8px;border-radius:50%}
.wday-hdr{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;margin-bottom:4px}
.wday-hdr span{font-size:10px;color:var(--text3);text-align:center;font-family:var(--mono)}
.week-row{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;margin-bottom:4px}
.dcell{
  border-radius:8px;min-height:56px;
  border:1px solid var(--border);
  background:var(--surface2);
  position:relative;padding:4px 5px;cursor:default;
  transition:border-color .2s;
}
.dcell.inactive{background:transparent;border-color:transparent}
.dcell.past-day{opacity:.5}
.dcell.today-day{border-color:var(--accent);box-shadow:0 0 0 1px rgba(108,99,255,.3)}
.dcell.studied-day{background:rgba(67,233,123,.07)}
.dnum{font-size:10px;color:var(--text3);font-family:var(--mono)}
.today-day .dnum{color:var(--accent)}
.ddot-row{display:flex;flex-wrap:wrap;gap:2px;margin-top:3px}
.ddot{width:6px;height:6px;border-radius:50%;opacity:.8}
.dcheck{
  position:absolute;top:4px;right:4px;
  width:15px;height:15px;border-radius:50%;
  border:1px solid var(--border);
  background:var(--surface3);
  cursor:pointer;
  display:flex;align-items:center;justify-content:center;
  font-size:8px;color:transparent;
  transition:all .2s;
}
.dcheck.checked{background:var(--accent3);border-color:var(--accent3);color:var(--bg)}
.dhours{font-size:9px;color:var(--text3);font-family:var(--mono);margin-top:2px}

/* scrollbar */
::-webkit-scrollbar{width:6px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--surface3);border-radius:3px}

/* toast */
.toast{
  position:fixed;bottom:24px;right:24px;
  background:var(--surface2);border:1px solid var(--border);
  border-radius:10px;padding:12px 18px;
  font-size:13px;color:var(--text);
  z-index:1000;
  transform:translateY(80px);opacity:0;
  transition:all .35s cubic-bezier(.34,1.56,.64,1);
  pointer-events:none;
}
.toast.show{transform:translateY(0);opacity:1}

@media(max-width:600px){
  .day-big{font-size:44px}
  .timer-display{font-size:36px;min-width:160px}
  .subj-card{grid-template-columns:28px 1fr auto;gap:8px}
  .subj-bar-wrap,.subj-pct{display:none}
  .wrap{padding:12px 10px 60px}
}
</style>
</head>
<body>
<div class="wrap">

  <!-- HEADER -->
  <header>
    <div class="logo"><span>//</span> study.tracker</div>
    <div class="date-badge" id="hdr-date">—</div>
  </header>

  <!-- COUNTDOWN -->
  <div class="countdown-section">
    <div class="countdown-top">
      <div class="countdown-main">
        <div class="day-big" id="cd-big">—</div>
        <div class="day-label" id="cd-label">Loading...</div>
      </div>
      <div class="countdown-stats">
        <div class="cstat"><div class="cv" id="cd-left">—</div><div class="cl">Days left</div></div>
        <div class="cstat"><div class="cv" id="cd-done-s">0</div><div class="cl">Subjects done</div></div>
        <div class="cstat"><div class="cv" id="cd-streak">0</div><div class="cl">Streak</div></div>
        <div class="cstat"><div class="cv" id="cd-studied">0</div><div class="cl">Days studied</div></div>
      </div>
    </div>
    <div class="bar-label">
      <span>Apr 2, 2026</span>
      <span id="cd-pct-lbl">0 / 60 days</span>
      <span>May 31, 2026</span>
    </div>
    <div class="seg-bar" id="seg-bar"></div>
  </div>

  <!-- DAILY STUDY TIMER -->
  <div class="timer-section">
    <div class="section-title">// daily study timer</div>
    <div class="timer-core">
      <div class="timer-radial">
        <svg width="120" height="120" viewBox="0 0 120 120">
          <circle class="radial-bg" cx="60" cy="60" r="52"/>
          <circle class="radial-fg" id="radial-fg" cx="60" cy="60" r="52"
            stroke-dasharray="327" stroke-dashoffset="327"/>
        </svg>
        <div class="radial-label">
          <div id="radial-pct">0%</div>
          <span>of goal</span>
        </div>
      </div>
      <div>
        <div class="timer-display" id="timer-disp">00:00:00</div>
        <div style="font-size:12px;color:var(--text3);margin-top:4px;font-family:var(--mono)" id="timer-status">Ready to start</div>
        <div class="timer-controls" style="margin-top:14px">
          <button class="btn primary" id="btn-startstop" onclick="timerToggle()">START</button>
          <button class="btn" onclick="timerReset()">RESET</button>
          <button class="btn success-btn" onclick="markTodayStudied()">LOG DAY ✓</button>
        </div>
      </div>
    </div>

    <div class="goal-bar-wrap">
      <div class="goal-info">
        <span>Daily goal: <span id="goal-sel-lbl">8.5 hrs</span></span>
        <span id="goal-elapsed">0h 0m elapsed</span>
        <span id="goal-remain-lbl">8h 30m left</span>
      </div>
      <div class="goal-bar-track"><div class="goal-bar-fill" id="goal-bar" style="width:0%"></div></div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <button class="btn" style="font-size:10px;padding:5px 10px" onclick="setGoal(8)">8h goal</button>
        <button class="btn" style="font-size:10px;padding:5px 10px" onclick="setGoal(8.5)">8.5h goal</button>
        <button class="btn" style="font-size:10px;padding:5px 10px" onclick="setGoal(9)">9h goal</button>
      </div>
    </div>

    <div class="session-log">
      <div class="session-log-title">today's sessions</div>
      <div class="log-entries" id="log-entries"><span style="font-size:11px;color:var(--text3);font-family:var(--mono)">No sessions yet</span></div>
    </div>
  </div>

  <!-- SUBJECTS -->
  <div class="subjects-section">
    <div class="section-title">// subjects — serial schedule</div>
    <div class="subj-grid" id="subj-grid"></div>
  </div>

  <!-- CALENDAR -->
  <div class="cal-section">
    <div class="section-title">// 60-day calendar</div>
    <div class="cal-legend" id="cal-legend"></div>
    <div class="wday-hdr">
      <span>Sun</span><span>Mon</span><span>Tue</span><span>Wed</span><span>Thu</span><span>Fri</span><span>Sat</span>
    </div>
    <div id="cal-grid"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const SUBJECTS = [
  {id:0, name:'Bangla 1st paper',  color:'#6c63ff'},
  {id:1, name:'Bangla 2nd paper',  color:'#43e97b'},
  {id:2, name:'English 1st paper', color:'#ff6584'},
  {id:3, name:'ICT',               color:'#f5c842'},
  {id:4, name:'Psychology 1st paper', color:'#38b2f5'},
  {id:5, name:'Psychology 2nd paper', color:'#f97316'},
  {id:6, name:'Geography 1st paper',  color:'#a78bfa'},
  {id:7, name:'Geography 2nd paper',  color:'#fb7185'},
  {id:8, name:'Economics 1st paper',  color:'#34d399'},
  {id:9, name:'Economics 2nd paper',  color:'#fbbf24'},
  {id:10,name:'Sociology 1st paper',  color:'#60a5fa'},
  {id:11,name:'Sociology 2nd paper',  color:'#f472b6'},
  {id:12,name:'GK',                   color:'#94a3b8'},
];
const START = new Date(2026,3,2);
const TOTAL = 60;
const PER = Math.floor(TOTAL / SUBJECTS.length);
const SA = SUBJECTS.map((s,i)=>({
  ...s,
  fromDay: i*PER,
  toDay: i===SUBJECTS.length-1 ? TOTAL-1 : i*PER+PER-1
}));

function dayIdx(date){
  const d=new Date(date); d.setHours(0,0,0,0);
  const s=new Date(START); s.setHours(0,0,0,0);
  return Math.floor((d-s)/86400000);
}
const today=new Date(); today.setHours(0,0,0,0);
const todayI=dayIdx(today);
const todayKey='d'+todayI;

// State
let state = {
  subjDone: [],
  checked: {},
  dayHours: {},
  sessions: {},
  goalHours: 8.5,
};
function loadState(){
  try{
    const s=JSON.parse(localStorage.getItem('stp2_state')||'{}');
    state={...state,...s};
  }catch(e){}
}
function saveState(){
  try{ localStorage.setItem('stp2_state', JSON.stringify(state)); }catch(e){}
}
loadState();

// Timer
let timerRunning=false, timerSecs=0, timerInterval=null, sessionStart=null;
// Restore today's elapsed
timerSecs = Math.round((state.dayHours[todayKey]||0)*3600);

function fmtTime(s){
  const h=Math.floor(s/3600), m=Math.floor((s%3600)/60), sec=s%60;
  return [h,m,sec].map(v=>String(v).padStart(2,'0')).join(':');
}
function timerToggle(){
  if(timerRunning){
    timerRunning=false;
    clearInterval(timerInterval);
    const elapsed=(Date.now()-sessionStart)/1000;
    recordSession(elapsed);
    document.getElementById('btn-startstop').textContent='START';
    document.getElementById('btn-startstop').className='btn primary';
    document.getElementById('timer-status').textContent='Paused — session saved';
    showToast('Session saved!');
  } else {
    timerRunning=true;
    sessionStart=Date.now();
    timerInterval=setInterval(()=>{
      timerSecs++;
      state.dayHours[todayKey]=timerSecs/3600;
      if(timerSecs%10===0)saveState();
      updateTimerUI();
    },1000);
    document.getElementById('btn-startstop').textContent='PAUSE';
    document.getElementById('btn-startstop').className='btn danger';
    document.getElementById('timer-status').textContent='Studying...';
  }
}
function timerReset(){
  if(timerRunning){timerRunning=false;clearInterval(timerInterval);}
  if(confirm('Reset today\'s timer? Logged sessions will be cleared.')){
    timerSecs=0;
    state.dayHours[todayKey]=0;
    state.sessions[todayKey]=[];
    saveState();
    document.getElementById('btn-startstop').textContent='START';
    document.getElementById('btn-startstop').className='btn primary';
    document.getElementById('timer-status').textContent='Ready to start';
    updateTimerUI();renderSessions();
  }
}
function recordSession(secs){
  if(!state.sessions[todayKey]) state.sessions[todayKey]=[];
  const now=new Date();
  const endStr=now.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true});
  const startD=new Date(now-secs*1000);
  const startStr=startD.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',hour12:true});
  const m=Math.round(secs/60);
  state.sessions[todayKey].push({start:startStr,end:endStr,min:m});
  saveState();
  renderSessions();
}
function updateTimerUI(){
  const goalSecs=state.goalHours*3600;
  const pct=Math.min(100,Math.round((timerSecs/goalSecs)*100));
  const disp=document.getElementById('timer-disp');
  disp.textContent=fmtTime(timerSecs);
  disp.className='timer-display'+(timerRunning?' running':timerSecs>=goalSecs?' done-color':'');
  // radial
  const circ=327;
  document.getElementById('radial-fg').style.strokeDashoffset=circ-(circ*(pct/100));
  document.getElementById('radial-pct').textContent=pct+'%';
  // goal bar
  document.getElementById('goal-bar').style.width=Math.min(100,pct)+'%';
  document.getElementById('goal-sel-lbl').textContent=state.goalHours+'h';
  const elapsed_h=Math.floor(timerSecs/3600), elapsed_m=Math.floor((timerSecs%3600)/60);
  document.getElementById('goal-elapsed').textContent=elapsed_h+'h '+elapsed_m+'m elapsed';
  const remSecs=Math.max(0,goalSecs-timerSecs);
  const rem_h=Math.floor(remSecs/3600), rem_m=Math.floor((remSecs%3600)/60);
  document.getElementById('goal-remain-lbl').textContent=rem_h+'h '+rem_m+'m left';
  if(timerSecs>=goalSecs && !timerRunning){
    document.getElementById('timer-status').textContent='Goal reached! Great work today.';
  }
}
function setGoal(h){
  state.goalHours=h;
  saveState();updateTimerUI();
}
function renderSessions(){
  const wrap=document.getElementById('log-entries');
  const ses=state.sessions[todayKey]||[];
  if(!ses.length){
    wrap.innerHTML='<span style="font-size:11px;color:var(--text3);font-family:var(--mono)">No sessions yet</span>';
    return;
  }
  wrap.innerHTML=ses.map(s=>`<span class="log-chip">${s.start}–${s.end} (${s.min}m)</span>`).join('');
}
function markTodayStudied(){
  state.checked[todayI]=true;
  saveState();render();
  showToast('Day marked as studied!');
}

// Toast
function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg;t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
}

// Main render
function render(){
  // Header date
  documen
