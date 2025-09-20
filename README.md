
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>DREADLORDS DASHBOARD— Fixed</title>

<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>
<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Montserrat:wght@400;600&display=swap');

  body {
    font-family: 'Montserrat', sans-serif;
    background: radial-gradient(circle at top, #0A103D 0%, #000 100%);
    margin: 0;
    padding: 20px;
    color: #fff;
  }
  h1,h2 {
    text-align: center;
    font-family: 'Orbitron', sans-serif;
    color: #fff;
    text-shadow: 0 0 12px #1B46A3;
    letter-spacing: 1px;
  }
  textarea {
    width: 100%;
    height: 160px;
    font-family: monospace;
    margin-bottom: 8px;
    padding: 10px;
    border: 1px solid #1B46A3;
    border-radius: 6px;
    background: #0A103D;
    color: #fff;
  }
  button, input, select {
    padding: 10px 16px;
    margin: 6px 4px;
    border: none;
    border-radius: 6px;
    background: linear-gradient(135deg, #1B46A3, #8000FF);
    color: #fff;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
  }
  button:hover, input[type="submit"]:hover {
    transform: scale(1.05);
    box-shadow: 0 0 12px #1B46A3;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    background: rgba(255,255,255,0.05);
    margin-bottom: 12px;
    border: 1px solid #1B46A3;
    border-radius: 8px;
    overflow: hidden;
  }
  th, td {
    border: 1px solid rgba(255,255,255,0.1);
    padding: 8px;
    text-align: center;
    color: #fff;
  }
  th {
    background: linear-gradient(135deg, #1B46A3, #8000FF);
    font-family: 'Orbitron', sans-serif;
    font-size: 14px;
    letter-spacing: 0.5px;
  }
  .archive-item {
    background: rgba(255,255,255,0.05);
    padding: 8px;
    border: 1px solid #1B46A3;
    margin-bottom: 6px;
    border-radius: 6px;
  }
  img.player-photo {
    width: 48px;
    height: 48px;
    object-fit: cover;
    border-radius: 50%;
    border: 2px solid #1B46A3;
    box-shadow: 0 0 8px #8000FF;
  }
  .small { font-size: 13px; color: #bbb; }
  .notice {
    background: rgba(255,255,255,0.08);
    border: 1px solid #1B46A3;
    padding: 10px;
    margin: 8px 0;
    border-radius: 6px;
    color: #fff;
  }#rankingTable {
  background: #0A103D !important; /* solid dark background */
  color: #fff !important;           /* white text */
}

#rankingTable th, 
#rankingTable td {
  background: #0A103D !important;   /* dark cells */
  color: #fff !important;           /* white text */
  border: 1px solid #1B46A3 !important;
}
/* UCL THEME for Top Performance Table */
#performanceTable {
  width: 100%;
  border-collapse: collapse;
  margin-top: 15px;
  font-size: 14px;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}

#performanceTable th {
  background: #1e2a78 !important; /* UCL Deep Blue */
  color: #ffffff !important;      /* White text */
  padding: 10px;
  text-align: center;
  font-weight: 600;
}

#performanceTable td {
  padding: 8px 10px;
  text-align: center;
  background: #0a1128 !important; /* Dark navy row background */
  color: #e6e6e6 !important;      /* Light grey text */
}

#performanceTable tr:nth-child(even) td {
  background: #16225a !important; /* Slightly lighter navy for even rows */
}

#performanceTable tr:hover td {
  background: #243b7a !important; /* Hover effect */
  color: #ffffff !important;
}
#topPerformanceContainer table,
#topPerformanceContainer th,
#topPerformanceContainer td {
  background: #0A103D !important;
  color: #fff !important;
  border: 1px solid #1B46A3 !important;
}
</style>
</head>
<body>

<h1>DREADLORDS DASHBOARD</h1>

<!-- 🔑 ADMIN SECTION -->
<div id="adminSection" style="display:none">
  <h2>Admin Section</h2>

  <h3>1) স্কোরকার্ড পেস্ট করুন</h3>
  <textarea id="scorecardText" placeholder="স্কোরকার্ড এখানে পেস্ট করুন"></textarea>
  <br>
  <button onclick="previewScorecard()">Preview Scorecard</button>

  <h3>2) Preview</h3>
  <div id="previewContainer" class="notice">Preview এখানে দেখাবে।</div>

  <label>Submission date: <input type="date" id="submissionDate"></label>
  <label>Password: <input type="text" id="submitPassword" placeholder="Fardous"></label>
  <button onclick="submitScorecard()">Submit Scorecard</button>

  <h3>3) Archive</h3>
  <div id="archiveContainer"></div>
</div>

<!-- 👥 VIEWER SECTION + TOP PERFORMANCE -->
<div id="viewerSection">
  <h2>Player Rankings & Statistics</h2>
  <label>Filter:
    <select id="rankingType" onchange="displayRanking()">
      <option value="overall">Overall</option>
      <option value="monthly">Monthly</option>
      <option value="weekly">Weekly</option>
    </select>
  </label>
  <table id="rankingTable">
    <thead>
      <tr>
        <th>Photo</th><th>Player</th><th>Matches</th>
        <th>W</th><th>D</th><th>L</th>
        <th>WIN RATIO </th><th>GS</th><th>Gc</th><th>GD</th>
        <th>MOTM</th><th>Rating</th><th>Upload</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <h2>Download Rankings</h2>
  <select id="downloadRange">
    <option value="1-10">1-10</option>
    <option value="11-20">11-20</option>
  </select>
  <button onclick="downloadRankingCard()">Download Card</button>
  <div id="rankingCard" style="padding:10px;background:#fff;margin-top:8px"></div>

  <!-- 🔥 TOP PERFORMANCE SECTION -->
  <h2>Top Performance</h2>
  <label>View: 
    <select id="topPerformanceType" onchange="displayTopPerformance()">
      <option value="weekly">Weekly</option>
      <option value="monthly">Monthly</option>
      <option value="overall">Overall</option>
    </select>
  </label>

  <div id="topPerformanceContainer" style="margin-top:12px;"></div>
</div>

<!-- 🔑 ADMIN LOGIN BUTTON -->
<div style="margin-top:20px;text-align:center">
  <button onclick="toggleAdmin()">🔑 Admin Login</button>
</div>

<style>
/* Top Performance tables */
#topPerformanceContainer table {
  width: 100%;
  border-collapse: collapse;
  background: rgba(255,255,255,0.05);
  margin-bottom: 16px;
  border: 1px solid #1B46A3;
  border-radius: 6px;
  overflow: hidden;
}
#topPerformanceContainer th, #topPerformanceContainer td {
  border: 1px solid rgba(255,255,255,0.1);
  padding: 6px;
  text-align: center;
  color: #fff;
}
#topPerformanceContainer th {
  background: linear-gradient(135deg, #1B46A3, #8000FF);
  font-family: 'Orbitron', sans-serif;
  font-size: 13px;
}
#topPerformanceContainer h3 {
  font-family: 'Orbitron', sans-serif;
  color: #fff;
  text-shadow: 0 0 8px #1B46A3;
  margin-bottom: 6px;
}
</style>

<script>
function displayTopPerformance(){
  const type=document.getElementById('topPerformanceType').value;
  const container=document.getElementById('topPerformanceContainer');
  container.innerHTML='Loading…';
  
  db.collection('scorecards').get().then(snapshot=>{
    const stats={}; const now=new Date();
    snapshot.forEach(doc=>{
      const card=doc.data(); if(!card || !card.players) return;
      const cardDate=new Date(card.date);
      let include=false;
      if(type==='overall') include=true;
      else if(type==='monthly') include=(cardDate.getMonth()===now.getMonth() && cardDate.getFullYear()===now.getFullYear());
      else if(type==='weekly'){ 
        const ws=new Date(now); ws.setDate(now.getDate()-now.getDay()); 
        const we=new Date(ws); we.setDate(ws.getDate()+6); 
        include=(cardDate>=ws && cardDate<=we); 
      }
      if(!include) return;
      card.players.forEach(p=>{
        if(!stats[p.player]) stats[p.player]={...p};
        else{
          const o=stats[p.player];
          o.matches+=p.matches; o.win+=p.win; o.draw+=p.draw; o.loss+=p.loss;
          o.gs+=p.gs; o.gc+=p.gc; o.gd=o.gs-o.gc; o.motm+=p.motm; o.rating+=p.rating;
          if(p.photo) o.photo=p.photo;
          o.maxGoals = Math.max(o.maxGoals||0, p.gs);
          if(p.gs>=7) o.sevenPlusMatches=(o.sevenPlusMatches||0)+1;
        }
      });
    });

    const players=Object.values(stats);
    const createTable=(title, headers, rows)=>{
      let html=`<h3>${title}</h3><table><thead><tr>`;
      headers.forEach(h=>html+=`<th>${h}</th>`); html+='</tr></thead><tbody>';
      rows.forEach(r=>{ html+='<tr>'; r.forEach(c=>html+=`<td>${c}</td>`); html+='</tr>'; });
      html+='</tbody></table>'; return html;
    };

    let html='';

    const motmTop=players.sort((a,b)=>b.motm-a.motm).slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), p.motm]);
    html+=createTable('Most MOTM', ['Photo','Player','MOTM'], motmTop);

    const scorerTop=players.sort((a,b)=>b.gs-a.gs).slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), p.gs]);
    html+=createTable('Top Scorer', ['Photo','Player','Goals'], scorerTop);

    const winTop=players.sort((a,b)=>b.win-a.win).slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), p.win]);
    html+=createTable('Most Wins', ['Photo','Player','Wins'], winTop);

    const sevenPlus=players.filter(p=>p.sevenPlusMatches>0)
      .sort((a,b)=>b.sevenPlusMatches-a.sevenPlusMatches)
      .slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), p.sevenPlusMatches]);
    html+=createTable('7+ Goals in a Single Match', ['Photo','Player','Times'], sevenPlus);

    const winPercTop=players.filter(p=>p.matches>0).sort((a,b)=>((b.win/b.matches)*100)-((a.win/a.matches)*100)).slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), ((p.win/p.matches)*100).toFixed(2)+'%']);
    html+=createTable('Highest Win Percentage', ['Photo','Player','Win %'], winPercTop);

    const ratingTop=players.sort((a,b)=>b.rating-a.rating).slice(0,10)
      .map(p=>[`<img class="player-photo" src="${p.photo||''}" onerror="this.src='';">`, escapeHtml(p.player), (p.rating||0).toFixed(2)]);
    html+=createTable('Average Rating', ['Photo','Player','Rating'], ratingTop);

    container.innerHTML=html;

  }).catch(err=>{ console.error(err); container.innerHTML='Failed to load top performance.'; });
}

// Initialize Top Performance
displayTopPerformance();
</script>

<!-- 🔑 ADMIN LOGIN BUTTON -->
<div style="margin-top:20px;text-align:center">
  <button onclick="toggleAdmin()">🔑 Admin Login</button>
</div>

<script>
function toggleAdmin(){
  const pw = prompt("Enter admin password:");
  if(pw === "Fardous"){
    document.getElementById('adminSection').style.display="block";
    alert("Welcome Admin ✅");
  } else {
    alert("Wrong password!");
  }
}
</script>
</body>
</table>

<h2>5) Download</h2>
<select id="downloadRange"><option value="1-10">1-10</option><option value="11-20">11-20</option></select>
<button onclick="downloadRankingCard()">Download Card</button>
<div id="rankingCard" style="padding:10px;background:#fff;margin-top:8px"></div>

<script>
/* ---------- Firebase config ---------- */
const firebaseConfig = {
  apiKey:"AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLctDopPq4",
  authDomain:"llfc-4d2df.firebaseapp.com",
  projectId:"llfc-4d2df",
  storageBucket:"llfc-4d2df.firebasestorage.app",
  messagingSenderId:"697058785471",
  appId:"1:697058785471:web:e7df63d4e9caadec762e0a"
};
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

/* ---------- Config: known LLFC team names ---------- */
const LLFCTeams = [
  "DREADLORDS OF LLFC",
  "Luminous Legends EFootball Club",
  "Luminous Legends",
  "LLFC",
  "Luminous Legends EFootball"
];

/* ---------- Helpers ---------- */
function getLastNumber(str){ const m=str.match(/(\d+)(?!.*\d)/); return m?parseInt(m[1],10):0; }
function getFirstNumber(str){ const m=str.match(/(\d+)/); return m?parseInt(m[1],10):0; }
function uidFor(name){ return name.replace(/\s+/g,'_').replace(/[^\w\-]/g,'').toLowerCase() + '_' + Date.now(); }
function escapeHtml(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function containsAnyIgnoreCase(haystack, needles){ const l = String(haystack||'').toLowerCase(); return needles.some(n => l.includes(String(n||'').toLowerCase())); }

/* ---------- Extract & parse functions ---------- */
function extractPlayersFromSide(sideRaw, goalPos){
  if(!sideRaw || !sideRaw.trim()) return [];
  const original = sideRaw;
  if(goalPos === 'start') sideRaw = sideRaw.replace(/^\s*\d+\s*/,'');
  else if(goalPos === 'end') sideRaw = sideRaw.replace(/\s*\d+\s*$/,'');
  let separators = [];
  if(/@/.test(original)) separators.push('@');
  if(/\s{2,}/.test(original)) separators.push('doubleSpace');
  if(/[|,\/]/.test(original)) separators.push(/[|,\/]/);
  if(separators.length === 0){ if(/\s\/\s/.test(original)) separators.push(/\s\/\s/); else if(/\s-\s/.test(original)) separators.push(/\s-\s/);}
  let cleaned = sideRaw.replace(/[🔑⚽🟣🟡🔴•★✔✖]/g,' ').replace(/[,:;�"“”‘’{}<>]/g,' ').replace(/\s+/g,' ').trim();
  let parts = [];
  if(separators.length > 0){
    let sep = separators[0];
    if(sep === '@') parts = cleaned.split('@').map(p=>p.trim()).filter(Boolean);
    else if(sep==='doubleSpace') parts = original.split(/\s{2,}/).map(p=>p.replace(/[🔑⚽]/g,'').trim()).filter(Boolean);
    else if(sep instanceof RegExp) parts = cleaned.split(sep).map(p=>p.trim()).filter(Boolean);
    else parts = cleaned.split(' ').map(p=>p.trim()).filter(Boolean);
  } else if(cleaned) parts = [cleaned];
  parts = parts.map(p => p.replace(/\d+/g,'').replace(/^[\W_]+|[\W_]+$/g,'').replace(/\s+/g,' ').trim()).filter(Boolean);
  return parts;
}

function parseScorecard(text){
  const lines = text.split(/\r?\n/).map(l=>l.trim()).filter(Boolean);
  const players = {}; let currentLeftTeam=null; let currentRightTeam=null;
  for(let i=0;i<lines.length;i++){
    const line=lines[i], ll=line.toLowerCase();
    if(ll.includes('deadline')||ll.includes('referee')||ll.includes('referees')||ll.includes('official')||ll.includes('points')||ll.includes('room settings')) continue;
    if(!line.includes('🆚')) continue;
    const parts=line.split('🆚'); if(parts.length<2) continue;
    let leftRaw=parts[0].trim(), rightRaw=parts.slice(1).join('🆚').trim();
    const leftHasTeamName=containsAnyIgnoreCase(leftRaw,LLFCTeams);
    const rightHasTeamName=containsAnyIgnoreCase(rightRaw,LLFCTeams);
    if(leftHasTeamName || rightHasTeamName){ currentLeftTeam=leftRaw.replace(/[\r\n]+/g,' ').trim(); currentRightTeam=rightRaw.replace(/[\r\n]+/g,' ').trim(); continue; }
    let leftIsLLFC=null;
    if(currentLeftTeam || currentRightTeam){
      if(containsAnyIgnoreCase(currentLeftTeam,LLFCTeams)) leftIsLLFC=true;
      else if(containsAnyIgnoreCase(currentRightTeam,LLFCTeams)) leftIsLLFC=false;
    }
    if(leftIsLLFC===null){
      if(containsAnyIgnoreCase(leftRaw,LLFCTeams)) leftIsLLFC=true;
      else if(containsAnyIgnoreCase(rightRaw,LLFCTeams)) leftIsLLFC=false;
      else continue;
    }
    const llfcSideRaw = leftIsLLFC?leftRaw:rightRaw;
    const oppSideRaw = leftIsLLFC?rightRaw:leftRaw;
    const llfcGoals = leftIsLLFC?getLastNumber(leftRaw):getFirstNumber(rightRaw);
    const oppGoals = leftIsLLFC?getFirstNumber(rightRaw):getLastNumber(leftRaw);
    const playerNames=extractPlayersFromSide(llfcSideRaw,leftIsLLFC?'end':'start');
    if(playerNames.length===0){ const cleaned=llfcSideRaw.replace(/[🔑⚽@]/g,' ').replace(/\d+/g,' ').replace(/\s+/g,' ').trim(); if(cleaned) playerNames.push(cleaned); }
    let teamNameForPlayer=currentLeftTeam||currentRightTeam||'LLFC';
    playerNames.forEach(name=>{
      const cleanName=name.trim(); if(!cleanName) return;
      if(!players[cleanName]) players[cleanName]={id:uidFor(cleanName),player:cleanName,team:teamNameForPlayer,matches:1,win:llfcGoals>oppGoals?1:0,draw:llfcGoals===oppGoals?1:0,loss:llfcGoals<oppGoals?1:0,gs:llfcGoals,gc:oppGoals,gd:llfcGoals-oppGoals,motm:line.includes('⚽')?1:0,rating:0,photo:''};
      else { const o=players[cleanName]; o.matches+=1; o.win+=llfcGoals>oppGoals?1:0; o.draw+=llfcGoals===oppGoals?1:0; o.loss+=llfcGoals<oppGoals?1:0; o.gs+=llfcGoals; o.gc+=oppGoals; o.gd=o.gs-o.gc; o.motm+=line.includes('⚽')?1:0; }
    });
  }
  return Object.values(players);
}

/* ---------- preview / rendering / rating ---------- */
let previewPlayers=[],currentScorecardID=null;
function calcRating(p){return (p.win*7)+(p.draw*5)+(p.loss*-5)+((p.gd||0)*0.3)+(p.motm||0)*1;}

function renderPreviewTable(){
  if(!previewPlayers || previewPlayers.length===0){
    document.getElementById('previewContainer').innerHTML='<div class="small">Preview খালি — প্রথমে scorecard পেস্ট করে Preview চাপুন।</div>';
    return;
  }
  let html='<table><thead><tr><th>Player</th><th>Matches</th><th>W</th><th>D</th><th>L</th><th>GS</th><th>GC</th><th>GD</th><th>MOTM</th><th>Rating</th></tr></thead><tbody>';
  
  previewPlayers.forEach((p,idx)=>{
    p.rating=p.rating||calcRating(p);
    html+=`<tr>
      <td style="text-align:left">
        <input type="text" data-idx="${idx}" data-field="player" value="${escapeHtml(p.player)}">
      </td>
      <td><input data-idx="${idx}" data-field="matches" type="number" value="${p.matches}"></td>
      <td><input data-idx="${idx}" data-field="win" type="number" value="${p.win}"></td>
      <td><input data-idx="${idx}" data-field="draw" type="number" value="${p.draw}"></td>
      <td><input data-idx="${idx}" data-field="loss" type="number" value="${p.loss}"></td>
      <td><input data-idx="${idx}" data-field="gs" type="number" value="${p.gs}"></td>
      <td><input data-idx="${idx}" data-field="gc" type="number" value="${p.gc}"></td>
      <td><input data-idx="${idx}" data-field="gd" type="number" value="${p.gd}"></td>
      <td><input data-idx="${idx}" data-field="motm" type="number" value="${p.motm}"></td>
      <td><input type="number" value="${(p.rating||0).toFixed(2)}" readonly></td>
    </tr>`;
  });
  html+='</tbody></table>';
  document.getElementById('previewContainer').innerHTML=html;

  // add event listeners for all inputs
  document.querySelectorAll('#previewContainer input').forEach(inp=>{
    inp.addEventListener('input',(e)=>{
      const idx=parseInt(e.target.getAttribute('data-idx')), field=e.target.getAttribute('data-field');
      if(Number.isInteger(idx) && field){
        const val=field==='player'?e.target.value:(parseInt(e.target.value)||0);
        previewPlayers[idx][field]=val;
        if(['gs','gc','matches','win','draw','loss','motm'].includes(field)){
          previewPlayers[idx].gd=(previewPlayers[idx].gs||0)-(previewPlayers[idx].gc||0);
          previewPlayers[idx].rating=calcRating(previewPlayers[idx]);
          const row=e.target.closest('tr');
          if(row){ const ratingInput=row.querySelector('td:last-child input'); if(ratingInput) ratingInput.value=previewPlayers[idx].rating.toFixed(2); }
        }
      }
    });
  });
}
/* ---------- Preview button ---------- */
function previewScorecard(){
  const text=document.getElementById('scorecardText').value||''; if(!text.trim()){ alert('প্রথমে scorecard পেস্ট করুন।'); return; }
  previewPlayers=parseScorecard(text);
  if(previewPlayers.length===0){ alert('কোনো LLFC player detect করা যায়নি।'); document.getElementById('previewContainer').innerHTML='<div class="small">No LLFC players found in pasted text.</div>'; return; }
  previewPlayers.forEach(p=>p.rating=calcRating(p));
  currentScorecardID=Date.now();
  renderPreviewTable();
}

/* ---------- Submit ---------- */
function submitScorecard(){
  const pw=document.getElementById('submitPassword').value||''; if(pw!=='Fardous'){ alert('Password ভুল।'); return; }
  const date=document.getElementById('submissionDate').value; if(!date){ alert('Submission date নির্বাচন করুন।'); return; }
  if(!previewPlayers || previewPlayers.length===0){ alert('প্রথমে preview তৈরি করুন।'); return; }
  document.querySelectorAll('#previewContainer input[type="number"]').forEach(inp=>{ const idx=parseInt(inp.getAttribute('data-idx')),field=inp.getAttribute('data-field'); if(Number.isInteger(idx)&&field) previewPlayers[idx][field]=parseInt(inp.value)||0; });
  previewPlayers.forEach(p=>{ p.gd=p.gs-p.gc; p.rating=calcRating(p); });
  const docId=String(currentScorecardID||Date.now());
  db.collection('scorecards').doc(docId).set({id:docId,date:date,players:previewPlayers})
    .then(()=>{ alert('Submitted ✅'); document.getElementById('previewContainer').innerHTML='<div class="small">Submitted — preview cleared.</div>'; document.getElementById('scorecardText').value=''; previewPlayers=[]; currentScorecardID=null; displayArchive(); displayRanking(); })
    .catch(err=>{ console.error(err); alert('Submit failed: '+err.message); });
}

/* ---------- Archive ---------- */
function displayArchive(){
  const container=document.getElementById('archiveContainer'); container.innerHTML='<div class="small">Loading archive…</div>';
  db.collection('scorecards').orderBy('id','desc').get().then(snapshot=>{
    container.innerHTML='';
    snapshot.forEach(doc=>{
      const d=doc.data();
      const el=document.createElement('div'); el.className='archive-item';
      el.innerHTML=`<strong>${escapeHtml(d.date||'--')}</strong> &nbsp; <button onclick="loadArchive('${d.id}')">Load</button> <button onclick="deleteArchive('${d.id}')">Delete</button>`;
      container.appendChild(el);
    });
    if(snapshot.empty) container.innerHTML='<div class="small">No archive yet.</div>';
  }).catch(err=>{ console.error(err); container.innerHTML='<div class="small">Archive load failed.</div>'; });
}

function loadArchive(id){
  db.collection('scorecards').doc(String(id)).get().then(doc=>{
    if(!doc.exists){ alert('Not found'); return; }
    previewPlayers=(doc.data().players||[]).map(p=>({...p})); previewPlayers.forEach(p=>p.rating=calcRating(p)); currentScorecardID=id;
    renderPreviewTable(); alert('Archive loaded to preview.');
  }).catch(err=>{ console.error(err); alert('Load failed: '+err.message); });
}

function deleteArchive(id){ if(!confirm('Delete this?')) return; db.collection('scorecards').doc(String(id)).delete().then(()=>{ displayArchive(); displayRanking(); }); }

/* ---------- Rankings ---------- */
function displayRanking(){
  const type=document.getElementById('rankingType').value;
  const tbody=document.querySelector('#rankingTable tbody');
  tbody.innerHTML='<tr><td colspan="12" class="small">Loading…</td></tr>';
  db.collection('scorecards').get().then(snapshot=>{
    const stats={}; const now=new Date();
    snapshot.forEach(doc=>{
      const card=doc.data();if(!card || !card.players) return;
      const cardDate=new Date(card.date);
      let include=false;
      if(type==='overall') include=true;
      else if(type==='monthly') include=(cardDate.getMonth()===now.getMonth() && cardDate.getFullYear()===now.getFullYear());
      else if(type==='weekly'){ 
        const ws=new Date(now); ws.setDate(now.getDate()-now.getDay()); 
        const we=new Date(ws); we.setDate(ws.getDate()+6); 
        include=(cardDate>=ws && cardDate<=we); 
      }
      if(!include) return;
      card.players.forEach(p=>{
        if(!stats[p.player]) stats[p.player]={...p};
        else{
          const o=stats[p.player];
          o.matches+=p.matches; o.win+=p.win; o.draw+=p.draw; o.loss+=p.loss;
          o.gs+=p.gs; o.gc+=p.gc; o.gd=o.gs-o.gc; o.motm+=p.motm; o.rating+=p.rating;
          if(p.photo) o.photo=p.photo;
        }
      });
    });

    const arr=Object.values(stats).sort((a,b)=>(b.rating||0)-(a.rating||0));
    if(arr.length===0){ tbody.innerHTML='<tr><td colspan="12" class="small">No ranking data.</td></tr>'; return; }
    tbody.innerHTML='';
    arr.forEach((p,i)=>{
      const medal=i===0?'🥇':i===1?'🥈':i===2?'🥉':'';
      const row=document.createElement('tr');
      const winPerc = p.matches > 0 ? ((p.win / p.matches) * 100).toFixed(2) : '0.00';
row.innerHTML=`<td><img class="player-photo" src="${p.photo||''}" onerror="this.src='';"></td>
  <td style="text-align:left">${medal} ${escapeHtml(p.player)}</td>
  <td>${p.matches}</td><td>${p.win}</td><td>${p.draw}</td><td>${p.loss}</td>
  <td>${winPerc}%</td>
  <td>${p.gs}</td><td>${p.gc}</td><td>${p.gd}</td>
  <td>${p.motm}</td><td>${(p.rating||0).toFixed(2)}</td>
  <td><input type="file" onchange="uploadPhoto(event,'${escapeHtml(p.player)}')"></td>`;`<td><img class="player-photo" src="${p.photo||''}" onerror="this.src='';"></td>
        <td style="text-align:left">${medal} ${escapeHtml(p.player)}</td>
        <td>${p.matches}</td><td>${p.win}</td><td>${p.draw}</td><td>${p.loss}</td>
        <td>${p.gs}</td><td>${p.gc}</td><td>${p.gd}</td><td>${p.motm}</td><td>${(p.rating||0).toFixed(2)}</td>
        <td><input type="file" onchange="uploadPhoto(event,'${escapeHtml(p.player)}')"></td>`;
      tbody.appendChild(row);
    });
  }).catch(err=>{ console.error(err); tbody.innerHTML='<tr><td colspan="12" class="small">Failed to load.</td></tr>'; });
}

/* ---------- Photo upload ---------- */
function uploadPhoto(e, playerName){
  const file=e.target.files[0]; if(!file) return;
  const reader=new FileReader();
  reader.onload=function(ev){
    const dataUrl=ev.target.result;
    db.collection('scorecards').get().then(snapshot=>{
      snapshot.forEach(doc=>{
        const d=doc.data(); let updated=false;
        (d.players||[]).forEach(p=>{ if(p.player===playerName){ p.photo=dataUrl; updated=true; } });
        if(updated) db.collection('scorecards').doc(doc.id).set(d);
      });
      displayRanking();
      alert('Photo uploaded.');
    }).catch(err=>{ console.error(err); alert('Upload failed'); });
  };
  reader.readAsDataURL(file);
}

/* ---------- Download ---------- */
function downloadRankingCard(){
  const range=document.getElementById('downloadRange').value.split('-').map(n=>parseInt(n,10));
  const tbody=document.querySelector('#rankingTable tbody');
  if(!tbody || tbody.rows.length===0){ alert('Ranking empty'); return; }
  let html=`<table style="border-collapse:collapse;border:1px solid #ddd;"><thead>${document.querySelector('#rankingTable thead').innerHTML}</thead><tbody>`;
  for(let i=range[0]-1;i<range[1] && i<tbody.rows.length;i++) html+='<tr>'+tbody.rows[i].innerHTML+'</tr>';
  html+='</tbody></table>';
  const div=document.getElementById('rankingCard'); div.innerHTML=html;
  html2canvas(div).then(canvas=>{
    const link=document.createElement('a'); link.download=`LLFC_Ranking_${range[0]}-${range[1]}.png`;
    link.href=canvas.toDataURL('image/png'); link.click();
  });
}

/* ---------- Init ---------- */
displayArchive();
displayRanking();
</script>
</body>
</html>
