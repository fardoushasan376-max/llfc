
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>DREADLORDS DASHBOARD</title>

<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-storage-compat.js"></script>
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
  h1, h2, h3 {
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
  }
  #rankingTable {
    background: #0A103D !important;
    color: #fff !important;
  }
  #rankingTable th, #rankingTable td {
    background: #0A103D !important;
    color: #fff !important;
    border: 1px solid #1B46A3 !important;
  }
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
    background: #1e2a78 !important;
    color: #ffffff !important;
    padding: 10px;
    text-align: center;
    font-weight: 600;
  }
  #performanceTable td {
    padding: 8px 10px;
    text-align: center;
    background: #0a1128 !important;
    color: #e6e6e6 !important;
  }
  #performanceTable tr:nth-child(even) td {
    background: #16225a !important;
  }
  #performanceTable tr:hover td {
    background: #243b7a !important;
    color: #ffffff !important;
  }
  #topPerformanceContainer table, #topPerformanceContainer th, #topPerformanceContainer td {
    background: #0A103D !important;
    color: #fff !important;
    border: 1px solid #1B46A3 !important;
  }
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
  #topPerformanceContainer h3 {
    font-family: 'Orbitron', sans-serif;
    color: #fff;
    text-shadow: 0 0 8px #1B46A3;
    margin-bottom: 6px;
    font-size: 24px;
  }
  /* UCL Style for Hall of Fame */
  .hof-card {
    display: flex;
    align-items: center;
    margin: 12px 0;
    padding: 15px;
    border: 2px solid #FFD700;
    border-radius: 10px;
    background: linear-gradient(135deg, rgba(27, 70, 163, 0.3), rgba(128, 0, 255, 0.3));
    box-shadow: 0 0 15px rgba(255, 215, 0, 0.5);
  }
  .hof-card img {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    border: 3px solid #FFD700;
    box-shadow: 0 0 10px rgba(255, 215, 0, 0.7);
    margin-right: 15px;
  }
  .hof-card .title {
    position: absolute;
    top: -20px;
    left: 0;
    right: 0;
    text-align: center;
    background: #FFD700;
    color: #000;
    border: 2px solid #FFFFFF;
    border-radius: 8px;
    padding: 4px 8px;
    font-family: 'Orbitron', sans-serif;
    font-size: 20px;
    font-weight: 800;
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
  }
  .hof-card .period {
    position: absolute;
    bottom: -20px;
    left: 0;
    right: 0;
    text-align: center;
    background: #FF4500;
    color: #FFF;
    border: 2px solid #FFFFFF;
    border-radius: 8px;
    padding: 4px 8px;
    font-family: 'Orbitron', sans-serif;
    font-size: 16px;
    font-weight: 600;
  }
  .hof-card .player-name {
    font-size: 24px;
    font-family: 'Orbitron', sans-serif;
    font-weight: 800;
    color: #FFD700;
    text-shadow: 0 0 5px rgba(255, 215, 0, 0.7);
  }
  .hof-card .stats {
    font-size: 20px;
    font-family: 'Montserrat', sans-serif;
    color: #FFF;
  }
  .record-card {
    margin: 10px;
    padding: 10px;
    border: 2px solid #FFD700;
    border-radius: 10px;
    background: linear-gradient(135deg, rgba(27, 70, 163, 0.2), rgba(128, 0, 255, 0.2));
    box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
    text-align: center;
    width: 220px;
  }
  .record-card img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 3px solid #FFD700;
    box-shadow: 0 0 8px rgba(255, 215, 0, 0.7);
  }
  .record-card .title {
    position: absolute;
    top: -20px;
    left: 0;
    right: 0;
    text-align: center;
    background: #FFD700;
    color: #000;
    border: 2px solid #FFFFFF;
    border-radius: 8px;
    padding: 4px 8px;
    font-family: 'Orbitron', sans-serif;
    font-size: 18px;
    font-weight: 800;
  }
  .record-card .player-name {
    font-size: 22px;
    font-family: 'Orbitron', sans-serif;
    font-weight: 800;
    color: #FFD700;
    margin-top: 10px;
  }
  .record-card .stat {
    font-size: 18px;
    font-family: 'Montserrat', sans-serif;
    color: #FFF;
  }
</style>
</head>

<body>
<h1>DREADLORDS DASHBOARD</h1>

<!-- 🔑 ADMIN SECTION -->
<div id="adminSection" style="display:none">
  <h2>Admin Section</h2>
  <h3>1) Paste Scorecard</h3>
  <textarea id="scorecardText" placeholder="Paste scorecard here"></textarea>
  <br>
  <button onclick="previewScorecard()">Preview Scorecard</button>

  <h3>2) Preview</h3>
  <div id="previewContainer" class="notice">Preview will be shown here.</div>

  <label>Submission date: <input type="date" id="submissionDate"></label>
  <label>Password: <input type="text" id="submitPassword" placeholder="Enter admin password"></label>
  <button onclick="submitScorecard()">Submit Scorecard</button>

  <h3>3) Archive</h3>
  <div id="archiveContainer"></div>
</div>

<!-- 👥 VIEWER SECTION -->
<div id="viewerSection">
  <!-- HALL OF FAME SECTION -->
  <h2 style="font-size:28px;">Hall of Fame</h2>
  <div id="hofAdmin" style="display:none">
    <h3 style="font-size:24px;">Set Player of the Week / Month</h3>
    <label>Period Type:
      <select id="hofType">
        <option value="weekly">Weekly</option>
        <option value="monthly">Monthly</option>
      </select>
    </label>
    <label>Player:
      <select id="hofPlayer"></select>
    </label>
    <label>Start Date: <input type="date" id="hofStartDate"></label>
    <label>End Date: <input type="date" id="hofEndDate"></label>
    <button onclick="setHallOfFame()">Set</button>
  </div>
  <div id="hofContainer" style="margin-top:12px;"></div>

  <!-- PLAYER RANKINGS & STATISTICS -->
  <h2 style="font-size:28px;">Player Rankings & Statistics</h2>
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
        <th>WIN RATIO</th><th>GS</th><th>GC</th><th>GD</th>
        <th>MOTM</th><th>Rating</th><th>Upload</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <h2 style="font-size:28px;">Download Rankings</h2>
  <select id="downloadRange">
    <option value="1-10">1-10</option>
    <option value="11-20">11-20</option>
  </select>
  <button onclick="downloadRankingCard()">Download Card</button>
  <div id="rankingCard" style="padding:10px;background:#fff;margin-top:8px"></div>

  <!-- 🔥 TOP PERFORMANCE SECTION -->
  <h2 style="font-size:28px;">Top Performance</h2>
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
  <button onclick="toggleAdmin()">Admin Login</button>
</div>

<script>
/* ---------- Firebase Config ---------- */
const firebaseConfig = {
  apiKey: "AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLctDopPq4",
  authDomain: "llfc-4d2df.firebaseapp.com",
  projectId: "llfc-4d2df",
  storageBucket: "llfc-4d2df.firebasestorage.app",
  messagingSenderId: "697058785471",
  appId: "1:697058785471:web:e7df63d4e9caadec762e0a"
};
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();
const storage = firebase.storage();

/* ---------- Config: Known LLFC Team Names ---------- */
const LLFCTeams = [
  "DREADLORDS OF LLFC",
  "Luminous Legends EFootball Club",
  "Luminous Legends",
  "LLFC",
  "Luminous Legends EFootball"
];

/* ---------- Helpers ---------- */
const getLastNumber = (str) => { const m = str.match(/(\d+)(?!.*\d)/); return m ? parseInt(m[1], 10) : 0; };
const getFirstNumber = (str) => { const m = str.match(/(\d+)/); return m ? parseInt(m[1], 10) : 0; };
const uidFor = (name) => name.replace(/\s+/g, '_').replace(/[^\w\-]/g, '').toLowerCase() + '_' + Date.now();
const escapeHtml = (s) => String(s || '').replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;').replace(/'/g, '&#39;');
const containsAnyIgnoreCase = (haystack, needles) => {
  const l = String(haystack || '').toLowerCase();
  return needles.some(n => l.includes(String(n || '').toLowerCase()));
};
const DEFAULT_PHOTO = 'https://via.placeholder.com/60?text=No+Photo';
let isAdmin = false;

/* ---------- Extract & Parse Functions ---------- */
function extractPlayersFromSide(sideRaw, goalPos) {
  if (!sideRaw || !sideRaw.trim()) return [];
  const original = sideRaw;
  if (goalPos === 'start') sideRaw = sideRaw.replace(/^\s*\d+\s*/, '');
  else if (goalPos === 'end') sideRaw = sideRaw.replace(/\s*\d+\s*$/, '');
  let separators = [];
  if (/@/.test(original)) separators.push('@');
  if (/\s{2,}/.test(original)) separators.push('doubleSpace');
  if (/[|,\/]/.test(original)) separators.push(/[|,\/]/);
  if (separators.length === 0) {
    if (/\s\/\s/.test(original)) separators.push(/\s\/\s/);
    else if (/\s-\s/.test(original)) separators.push(/\s-\s/);
  }
  let cleaned = sideRaw.replace(/[🔑⚽🟣🟡🔴•★✔✖]/g, ' ').replace(/[,:;“”‘’{}<>]/g, ' ').replace(/\s+/g, ' ').trim();
  let parts = [];
  if (separators.length > 0) {
    let sep = separators[0];
    if (sep === '@') parts = cleaned.split('@').map(p => p.trim()).filter(Boolean);
    else if (sep === 'doubleSpace') parts = original.split(/\s{2,}/).map(p => p.replace(/[🔑⚽]/g, '').trim()).filter(Boolean);
    else if (sep instanceof RegExp) parts = cleaned.split(sep).map(p => p.trim()).filter(Boolean);
    else parts = cleaned.split(' ').map(p => p.trim()).filter(Boolean);
  } else if (cleaned) parts = [cleaned];
  return parts.map(p => p.replace(/\d+/g, '').replace(/^[\W_]+|[\W_]+$/g, '').replace(/\s+/g, ' ').trim()).filter(Boolean);
}

function parseScorecard(text) {
  const lines = text.split(/\r?\n/).map(l => l.trim()).filter(Boolean);
  const players = {};
  let currentLeftTeam = null, currentRightTeam = null;
  for (let i = 0; i < lines.length; i++) {
    const line = lines[i], ll = line.toLowerCase();
    if (ll.includes('deadline') || ll.includes('referee') || ll.includes('referees') || ll.includes('official') || ll.includes('points') || ll.includes('room settings')) continue;
    if (!line.includes('🆚')) continue;
    const parts = line.split('🆚');
    if (parts.length < 2) continue;
    let leftRaw = parts[0].trim(), rightRaw = parts.slice(1).join('🆚').trim();
    const leftHasTeamName = containsAnyIgnoreCase(leftRaw, LLFCTeams);
    const rightHasTeamName = containsAnyIgnoreCase(rightRaw, LLFCTeams);
    
    if (leftHasTeamName && !rightHasTeamName) {
      currentLeftTeam = leftRaw.replace(/[\r\n]+/g, ' ').trim();
      currentRightTeam = rightRaw.replace(/[\r\n]+/g, ' ').trim();
      continue;
    } else if (rightHasTeamName && !leftHasTeamName) {
      currentLeftTeam = leftRaw.replace(/[\r\n]+/g, ' ').trim();
      currentRightTeam = rightRaw.replace(/[\r\n]+/g, ' ').trim();
      continue;
    } else if (leftHasTeamName && rightHasTeamName) {
      if (containsAnyIgnoreCase(leftRaw, LLFCTeams)) {
        currentLeftTeam = leftRaw;
        currentRightTeam = rightRaw;
      } else {
        currentLeftTeam = rightRaw;
        currentRightTeam = leftRaw;
      }
      continue;
    }

    let leftIsLLFC = null;
    if (currentLeftTeam || currentRightTeam) {
      if (containsAnyIgnoreCase(currentLeftTeam, LLFCTeams)) leftIsLLFC = true;
      else if (containsAnyIgnoreCase(currentRightTeam, LLFCTeams)) leftIsLLFC = false;
    }
    if (leftIsLLFC === null) {
      if (containsAnyIgnoreCase(leftRaw, LLFCTeams)) leftIsLLFC = true;
      else if (containsAnyIgnoreCase(rightRaw, LLFCTeams)) leftIsLLFC = false;
      else continue;
    }

    const llfcSideRaw = leftIsLLFC ? leftRaw : rightRaw;
    const oppSideRaw = leftIsLLFC ? rightRaw : leftRaw;
    const llfcGoals = leftIsLLFC ? getLastNumber(leftRaw) : getFirstNumber(rightRaw);
    const oppGoals = leftIsLLFC ? getFirstNumber(rightRaw) : getLastNumber(leftRaw);
    const playerNames = extractPlayersFromSide(llfcSideRaw, leftIsLLFC ? 'end' : 'start');
    if (playerNames.length === 0) {
      const cleaned = llfcSideRaw.replace(/[🔑⚽@]/g, ' ').replace(/\d+/g, ' ').replace(/\s+/g, ' ').trim();
      if (cleaned) playerNames.push(cleaned);
    }
    playerNames.forEach(name => {
      const cleanName = name.trim();
      if (!cleanName) return;
      if (!players[cleanName]) {
        players[cleanName] = {
          id: uidFor(cleanName),
          player: cleanName,
          matches: 1,
          win: llfcGoals > oppGoals ? 1 : 0,
          draw: llfcGoals === oppGoals ? 1 : 0,
          loss: llfcGoals < oppGoals ? 1 : 0,
          gs: llfcGoals,
          gc: oppGoals,
          gd: llfcGoals - oppGoals,
          motm: line.includes('⚽') ? 1 : 0,
          rating: 0,
          photo: ''
        };
      } else {
        const o = players[cleanName];
        o.matches += 1;
        o.win += llfcGoals > oppGoals ? 1 : 0;
        o.draw += llfcGoals === oppGoals ? 1 : 0;
        o.loss += llfcGoals < oppGoals ? 1 : 0;
        o.gs += llfcGoals;
        o.gc += oppGoals;
        o.gd = o.gs - o.gc;
        o.motm += line.includes('⚽') ? 1 : 0;
      }
    });
  }
  return Object.values(players);
}

/* ---------- Preview / Rendering / Rating ---------- */
let previewPlayers = [], currentScorecardID = null;
const calcRating = (p) => (p.win * 10) + (p.draw * 5) + (p.loss * -5) + ((p.gd || 0) * 1) + ((p.motm || 0) * 1);

function renderPreviewTable() {
  const container = document.getElementById('previewContainer');
  if (!previewPlayers || previewPlayers.length === 0) {
    container.innerHTML = '<div class="small">Preview is empty - paste scorecard and click Preview.</div>';
    return;
  }
  let html = '<table><thead><tr><th>Player</th><th>Matches</th><th>W</th><th>D</th><th>L</th><th>GS</th><th>GC</th><th>GD</th><th>MOTM</th><th>Rating</th></tr></thead><tbody>';
  previewPlayers.forEach((p, idx) => {
    p.rating = p.rating || calcRating(p);
    html += `<tr>
      <td style="text-align:left">
        <input type="text" data-idx="${idx}" data-field="player" value="${escapeHtml(p.player)}">
      </td>
      <td><input data-idx="${idx}" data-field="matches" type="number" min="0" value="${p.matches}"></td>
      <td><input data-idx="${idx}" data-field="win" type="number" min="0" value="${p.win}"></td>
      <td><input data-idx="${idx}" data-field="draw" type="number" min="0" value="${p.draw}"></td>
      <td><input data-idx="${idx}" data-field="loss" type="number" min="0" value="${p.loss}"></td>
      <td><input data-idx="${idx}" data-field="gs" type="number" min="0" value="${p.gs}"></td>
      <td><input data-idx="${idx}" data-field="gc" type="number" min="0" value="${p.gc}"></td>
      <td><input data-idx="${idx}" data-field="gd" type="number" value="${p.gd}" readonly></td>
      <td><input data-idx="${idx}" data-field="motm" type="number" min="0" value="${p.motm}"></td>
      <td><input type="number" value="${(p.rating || 0).toFixed(2)}" readonly></td>
    </tr>`;
  });
  html += '</tbody></table>';
  container.innerHTML = html;

  document.querySelectorAll('#previewContainer input').forEach(inp => {
    inp.addEventListener('input', (e) => {
      const idx = parseInt(e.target.getAttribute('data-idx')), field = e.target.getAttribute('data-field');
      if (!Number.isInteger(idx) || !field) return;
      const val = field === 'player' ? e.target.value : Math.max(0, parseInt(e.target.value) || 0);
      previewPlayers[idx][field] = val;
      if (['gs', 'gc', 'matches', 'win', 'draw', 'loss', 'motm'].includes(field)) {
        previewPlayers[idx].gd = (previewPlayers[idx].gs || 0) - (previewPlayers[idx].gc || 0);
        previewPlayers[idx].rating = calcRating(previewPlayers[idx]);
        const row = e.target.closest('tr');
        if (row) {
          row.querySelector('[data-field="gd"]').value = previewPlayers[idx].gd;
          row.querySelector('td:last-child input').value = previewPlayers[idx].rating.toFixed(2);
        }
      }
    });
  });
}

/* ---------- Preview Button ---------- */
function previewScorecard() {
  const text = document.getElementById('scorecardText').value || '';
  if (!text.trim()) {
    alert('Please paste the scorecard first.');
    return;
  }
  previewPlayers = parseScorecard(text);
  if (previewPlayers.length === 0) {
    alert('No LLFC players detected.');
    document.getElementById('previewContainer').innerHTML = '<div class="small">No LLFC players found in pasted text.</div>';
    return;
  }
  previewPlayers.forEach(p => p.rating = calcRating(p));
  currentScorecardID = Date.now();
  renderPreviewTable();
}

/* ---------- Submit Scorecard ---------- */
async function submitScorecard() {
  const pw = document.getElementById('submitPassword').value || '';
  if (pw !== 'Fardous') { // Replace with Firebase Authentication in production
    alert('Incorrect password. Use Firebase Authentication for secure access.');
    return;
  }
  const date = document.getElementById('submissionDate').value;
  if (!date || isNaN(new Date(date))) {
    alert('Please select a valid submission date.');
    return;
  }
  if (!previewPlayers || previewPlayers.length === 0) {
    alert('Please create a preview first.');
    return;
  }
  try {
    document.querySelectorAll('#previewContainer input').forEach(inp => {
      const idx = parseInt(inp.getAttribute('data-idx')), field = inp.getAttribute('data-field');
      if (Number.isInteger(idx) && field) {
        previewPlayers[idx][field] = field === 'player' ? inp.value : Math.max(0, parseInt(inp.value) || 0);
      }
    });
    previewPlayers.forEach(p => {
      p.gd = p.gs - p.gc;
      p.rating = calcRating(p);
      delete p.team; // Ensure team field is removed
    });
    const docId = String(currentScorecardID || Date.now());
    await db.collection('scorecards').doc(docId).set({ id: docId, date, players: previewPlayers });
    alert('Scorecard submitted successfully.');
    document.getElementById('previewContainer').innerHTML = '<div class="small">Submitted - preview cleared.</div>';
    document.getElementById('scorecardText').value = '';
    previewPlayers = [];
    currentScorecardID = null;
    await Promise.all([displayArchive(), displayRanking(), displayTopPerformance(), populateHOFPlayers(), displayHallOfFame()]);
  } catch (err) {
    console.error('Submit error:', err);
    alert('Submit failed: ' + err.message);
  }
}

/* ---------- Archive ---------- */
async function displayArchive() {
  const container = document.getElementById('archiveContainer');
  container.innerHTML = '<div class="small">Loading archive...</div>';
  try {
    const snapshot = await db.collection('scorecards').orderBy('id', 'desc').get();
    container.innerHTML = '';
    if (snapshot.empty) {
      container.innerHTML = '<div class="small">No archive entries yet.</div>';
      return;
    }
    snapshot.forEach(doc => {
      const d = doc.data();
      const el = document.createElement('div');
      el.className = 'archive-item';
      el.innerHTML = `<strong>${escapeHtml(d.date || '--')}</strong> &nbsp; <button onclick="loadArchive('${d.id}')">Load</button> <button onclick="deleteArchive('${d.id}')">Delete</button>`;
      container.appendChild(el);
    });
  } catch (err) {
    console.error('Archive load error:', err);
    container.innerHTML = '<div class="small">Failed to load archive: ' + err.message + '</div>';
  }
}

async function loadArchive(id) {
  try {
    const doc = await db.collection('scorecards').doc(String(id)).get();
    if (!doc.exists) {
      alert('Archive not found.');
      return;
    }
    previewPlayers = (doc.data().players || []).map(p => ({ ...p }));
    previewPlayers.forEach(p => {
      p.rating = calcRating(p);
      delete p.team; // Ensure team field is removed
    });
    currentScorecardID = id;
    renderPreviewTable();
    alert('Archive loaded to preview.');
  } catch (err) {
    console.error('Load archive error:', err);
    alert('Load failed: ' + err.message);
  }
}

async function deleteArchive(id) {
  if (!confirm('Are you sure you want to delete this archive?')) return;
  try {
    await db.collection('scorecards').doc(String(id)).delete();
    await Promise.all([displayArchive(), displayRanking(), displayTopPerformance(), displayHallOfFame()]);
    alert('Archive deleted successfully.');
  } catch (err) {
    console.error('Delete archive error:', err);
    alert('Delete failed: ' + err.message);
  }
}

/* ---------- Rankings ---------- */
async function displayRanking() {
  const type = document.getElementById('rankingType').value;
  const tbody = document.querySelector('#rankingTable tbody');
  tbody.innerHTML = `<tr><td colspan="12" class="small">Loading...</td></tr>`;
  try {
    const stats = {};
    const now = new Date();
    const snapshot = await db.collection('scorecards').get();
    snapshot.forEach(doc => {
      const card = doc.data();
      if (!card || !card.players) return;
      const cardDate = new Date(card.date);
      let include = false;
      if (type === 'overall') include = true;
      else if (type === 'monthly') include = (cardDate.getMonth() === now.getMonth() && cardDate.getFullYear() === now.getFullYear());
      else if (type === 'weekly') {
        const ws = new Date(now); ws.setDate(now.getDate() - now.getDay());
        const we = new Date(ws); we.setDate(ws.getDate() + 6);
        include = (cardDate >= ws && cardDate <= we);
      }
      if (!include) return;
      card.players.forEach(p => {
        if (!stats[p.player]) stats[p.player] = { ...p, team: undefined };
        else {
          const o = stats[p.player];
          o.matches += p.matches; o.win += p.win; o.draw += p.draw; o.loss += p.loss;
          o.gs += p.gs; o.gc += p.gc; o.gd = o.gs - o.gc; o.motm += p.motm; o.rating += p.rating;
          if (p.photo) o.photo = p.photo;
        }
      });
    });
    const arr = Object.values(stats).sort((a, b) => (b.rating || 0) - (a.rating || 0));
    if (arr.length === 0) {
      tbody.innerHTML = '<tr><td colspan="12" class="small">No ranking data available.</td></tr>';
      return;
    }
    tbody.innerHTML = '';
    arr.forEach((p, i) => {
      const medal = i === 0 ? '🥇' : i === 1 ? '🥈' : i === 2 ? '🥉' : '';
      const row = document.createElement('tr');
      const winPerc = p.matches > 0 ? ((p.win / p.matches) * 100).toFixed(2) : '0.00';
      row.innerHTML = `
        <td><img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';"></td>
        <td style="text-align:left">${medal} ${escapeHtml(p.player)}</td>
        <td>${p.matches}</td><td>${p.win}</td><td>${p.draw}</td><td>${p.loss}</td>
        <td>${winPerc}%</td>
        <td>${p.gs}</td><td>${p.gc}</td><td>${p.gd}</td>
        <td>${p.motm}</td><td>${(p.rating || 0).toFixed(2)}</td>
        <td><input type="file" onchange='uploadPhoto(event, ${JSON.stringify(escapeHtml(p.player))})'></td>
      `;
      tbody.appendChild(row);
    });
  } catch (err) {
    console.error('Ranking load error:', err);
    tbody.innerHTML = `<tr><td colspan="12" class="small">Failed to load rankings: ${err.message}</td></tr>`;
  }
}

/* ---------- Photo Upload ---------- */
async function uploadPhoto(e, playerName) {
  const file = e.target.files[0];
  if (!file) return;
  try {
    const storageRef = storage.ref(`player_photos/${playerName}_${Date.now()}.${file.name.split('.').pop()}`);
    await storageRef.put(file);
    const photoUrl = await storageRef.getDownloadURL();
    const snapshot = await db.collection('scorecards').get();
    let updated = false;
    for (const doc of snapshot.docs) {
      const d = doc.data();
      (d.players || []).forEach(p => {
        if (p.player === playerName) {
          p.photo = photoUrl;
          updated = true;
        }
      });
      if (updated) await db.collection('scorecards').doc(doc.id).set(d);
    }
    await displayRanking();
    alert('Photo uploaded successfully.');
  } catch (err) {
    console.error('Photo upload error:', err);
    alert('Photo upload failed: ' + err.message);
  }
}

/* ---------- Download Rankings ---------- */
async function downloadRankingCard() {
  const range = document.getElementById('downloadRange').value.split('-').map(n => parseInt(n, 10));
  const tbody = document.querySelector('#rankingTable tbody');
  if (!tbody || tbody.rows.length === 0) {
    alert('Ranking table is empty.');
    return;
  }
  try {
    let html = `<table style="border-collapse:collapse;border:1px solid #ddd;"><thead>${document.querySelector('#rankingTable thead').innerHTML}</thead><tbody>`;
    for (let i = range[0] - 1; i < range[1] && i < tbody.rows.length; i++) {
      const cloneRow = tbody.rows[i].cloneNode(true);
      cloneRow.querySelectorAll('input').forEach(inp => inp.remove());
      html += '<tr>' + cloneRow.innerHTML + '</tr>';
    }
    html += '</tbody></table>';
    const div = document.getElementById('rankingCard');
    div.innerHTML = html;
    const canvas = await html2canvas(div);
    const link = document.createElement('a');
    link.download = `LLFC_Ranking_${range[0]}-${range[1]}.png`;
    link.href = canvas.toDataURL('image/png');
    link.click();
  } catch (err) {
    console.error('Download error:', err);
    alert('Download failed: ' + err.message);
  }
}

/* ---------- Top Performance ---------- */
async function displayTopPerformance() {
  const type = document.getElementById('topPerformanceType').value;
  const container = document.getElementById('topPerformanceContainer');
  container.innerHTML = '<div class="small">Loading...</div>';
  try {
    const stats = {};
    const now = new Date();
    const snapshot = await db.collection('scorecards').get();
    snapshot.forEach(doc => {
      const card = doc.data();
      if (!card || !card.players) return;
      const cardDate = new Date(card.date);
      let include = false;
      if (type === 'overall') include = true;
      else if (type === 'monthly') include = (cardDate.getMonth() === now.getMonth() && cardDate.getFullYear() === now.getFullYear());
      else if (type === 'weekly') {
        const ws = new Date(now); ws.setDate(now.getDate() - now.getDay());
        const we = new Date(ws); we.setDate(ws.getDate() + 6);
        include = (cardDate >= ws && cardDate <= we);
      }
      if (!include) return;
      card.players.forEach(p => {
        if (!stats[p.player]) stats[p.player] = { ...p, maxGoals: p.gs, sevenPlusMatches: p.gs >= 7 ? 1 : 0, team: undefined };
        else {
          const o = stats[p.player];
          o.matches += p.matches; o.win += p.win; o.draw += p.draw; o.loss += p.loss;
          o.gs += p.gs; o.gc += p.gc; o.gd = o.gs - o.gc; o.motm += p.motm; o.rating += p.rating;
          if (p.photo) o.photo = p.photo;
          o.maxGoals = Math.max(o.maxGoals || 0, p.gs);
          if (p.gs >= 7) o.sevenPlusMatches = (o.sevenPlusMatches || 0) + 1;
        }
      });
    });
    const players = Object.values(stats);
    const createTable = (title, headers, rows) => {
      let html = `<h3>${escapeHtml(title)}</h3><table><thead><tr>`;
      headers.forEach(h => html += `<th>${escapeHtml(h)}</th>`);
      html += '</tr></thead><tbody>';
      rows.forEach(r => {
        html += '<tr>';
        r.forEach(c => html += `<td>${c}</td>`);
        html += '</tr>';
      });
      html += '</tbody></table>';
      return html;
    };
    let html = '';
    const motmTop = players.sort((a, b) => b.motm - a.motm).slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), p.motm]);
    if (motmTop.length) html += createTable('Most MOTM', ['Photo', 'Player', 'MOTM'], motmTop);
    const scorerTop = players.sort((a, b) => b.gs - a.gs).slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), p.gs]);
    if (scorerTop.length) html += createTable('Top Scorer', ['Photo', 'Player', 'Goals'], scorerTop);
    const winTop = players.sort((a, b) => b.win - a.win).slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), p.win]);
    if (winTop.length) html += createTable('Most Wins', ['Photo', 'Player', 'Wins'], winTop);
    const sevenPlus = players.filter(p => p.sevenPlusMatches > 0)
      .sort((a, b) => b.sevenPlusMatches - a.sevenPlusMatches)
      .slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), p.sevenPlusMatches]);
    if (sevenPlus.length) html += createTable('7+ Goals in a Single Match', ['Photo', 'Player', 'Times'], sevenPlus);
    const winPercTop = players.filter(p => p.matches > 0).sort((a, b) => ((b.win / b.matches) * 100) - ((a.win / a.matches) * 100)).slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), ((p.win / p.matches) * 100).toFixed(2) + '%']);
    if (winPercTop.length) html += createTable('Highest Win Percentage', ['Photo', 'Player', 'Win %'], winPercTop);
    const avgRatingTop = players
      .filter(p => p.matches >= 10 && p.rating !== undefined)
      .map(p => ({ ...p, avgRating: p.rating / p.matches }))
      .sort((a, b) => b.avgRating - a.avgRating)
      .slice(0, 10)
      .map(p => [`<img class="player-photo" src="${escapeHtml(p.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">`, escapeHtml(p.player), p.avgRating.toFixed(2)]);
    if (avgRatingTop.length) html += createTable('Top 10 Players by Average Rating (Min 10 Matches)', ['Photo', 'Player', 'Average Rating'], avgRatingTop);
    container.innerHTML = html || '<div class="small">No top performance data for the selected range.</div>';
  } catch (err) {
    console.error('Top performance error:', err);
    container.innerHTML = '<div class="small">Failed to load top performance: ' + err.message + '</div>';
  }
}

/* ---------- Admin Toggle ---------- */
function toggleAdmin() {
  const pw = prompt("Enter admin password:");
  if (pw === "Fardous") { // Replace with Firebase Authentication in production
    isAdmin = true;
    document.getElementById('adminSection').style.display = "block";
    document.getElementById('hofAdmin').style.display = "block";
    alert("Welcome Admin!");
    displayHallOfFame();
  } else {
    alert("Incorrect password! Use Firebase Authentication.");
  }
}

/* ---------- Hall of Fame Functions ---------- */
async function populateHOFPlayers() {
  const select = document.getElementById('hofPlayer');
  select.innerHTML = '<option value="">Loading players...</option>';
  try {
    console.log('Fetching scorecards for HOF player dropdown...');
    const players = {};
    const snapshot = await db.collection('scorecards').get();
    if (snapshot.empty) {
      console.warn('No scorecards found for HOF player dropdown.');
      select.innerHTML = '<option value="">No players available</option>';
      alert('No players found in scorecards. Add a scorecard first.');
      return;
    }
    snapshot.forEach(doc => {
      (doc.data().players || []).forEach(p => {
        players[p.player] = p;
      });
    });
    const playerCount = Object.keys(players).length;
    console.log(`HOF player dropdown: Found ${playerCount} players`);
    if (playerCount === 0) {
      select.innerHTML = '<option value="">No players available</option>';
      return;
    }
    select.innerHTML = '<option value="">Select Player</option>';
    Object.keys(players).sort().forEach(name => {
      const opt = document.createElement('option');
      opt.value = name;
      opt.text = name;
      select.appendChild(opt);
    });
    console.log('HOF player dropdown populated successfully');
  } catch (err) {
    console.error('Populate HOF players error:', err);
    select.innerHTML = '<option value="">Error loading players</option>';
    alert('Failed to load players for Hall of Fame: ' + err.message);
  }
}

async function setHallOfFame() {
  const type = document.getElementById('hofType').value;
  const player = document.getElementById('hofPlayer').value;
  const startDateStr = document.getElementById('hofStartDate').value;
  const endDateStr = document.getElementById('hofEndDate').value;
  if (!player || !startDateStr || !endDateStr) {
    alert('Please select a player and both start and end dates.');
    return;
  }
  const startDate = new Date(startDateStr);
  const endDate = new Date(endDateStr);
  endDate.setHours(23, 59, 59, 999);
  if (isNaN(startDate) || isNaN(endDate)) {
    alert('Invalid date selected.');
    return;
  }
  if (startDate > endDate) {
    alert('Start date must be before end date.');
    return;
  }
  const options = { month: 'short', day: 'numeric' };
  const startFmt = startDate.toLocaleDateString('en-US', options);
  const endFmt = endDate.toLocaleDateString('en-US', options);
  const period = `${startFmt} - ${endFmt}`;
  try {
    console.log(`Setting HOF: type=${type}, player=${player}, period=${period}`);
    const stats = {};
    const snapshot = await db.collection('scorecards').get();
    if (snapshot.empty) {
      console.warn('No scorecards found for HOF stats.');
      alert('No scorecard data available to set Hall of Fame.');
      return;
    }
    snapshot.forEach(doc => {
      const card = doc.data();
      if (!card || !card.players) return;
      const cardDate = new Date(card.date);
      if (cardDate >= startDate && cardDate <= endDate) {
        card.players.forEach(p => {
          if (p.player !== player) return;
          if (!stats[p.player]) stats[p.player] = { matches: 0, win: 0, gs: 0, motm: 0, photo: p.photo || DEFAULT_PHOTO };
          const o = stats[p.player];
          o.matches += p.matches || 0;
          o.win += p.win || 0;
          o.gs += p.gs || 0;
          o.motm += p.motm || 0;
          if (p.photo) o.photo = p.photo;
        });
      }
    });
    const pStats = stats[player];
    if (!pStats || pStats.matches === 0) {
      console.warn(`No stats for player ${player} in the period.`);
      alert('No stats found for the selected player in the given period.');
      return;
    }
    const docId = `${type}_${Date.now()}`;
    console.log(`Saving HOF entry: docId=${docId}`);
    await db.collection('hallOfFame').doc(docId).set({
      id: docId,
      type,
      player,
      period,
      stats: {
        matches: pStats.matches,
        win: pStats.win,
        gs: pStats.gs,
        motm: pStats.motm
      },
      photo: pStats.photo,
      timestamp: firebase.firestore.FieldValue.serverTimestamp()
    });
    console.log('HOF entry saved successfully');
    alert('Hall of Fame updated successfully!');
    await displayHallOfFame();
  } catch (err) {
    console.error('Set HOF error:', err);
    alert('Failed to update Hall of Fame: ' + err.message);
  }
}

async function deleteHOF(id) {
  if (!isAdmin) return;
  if (!confirm('Are you sure you want to delete this Hall of Fame entry?')) return;
  try {
    await db.collection('hallOfFame').doc(id).delete();
    await displayHallOfFame();
    alert('Deleted successfully.');
  } catch (err) {
    console.error('Delete HOF error:', err);
    alert('Delete failed: ' + err.message);
  }
}

async function editHOF(id) {
  if (!isAdmin) return;
  try {
    const doc = await db.collection('hallOfFame').doc(id).get();
    if (!doc.exists) {
      alert('Entry not found.');
      return;
    }
    const d = doc.data();
    const newType = prompt('Type (weekly/monthly):', d.type);
    if (!['weekly', 'monthly'].includes(newType)) {
      alert('Invalid type. Use "weekly" or "monthly".');
      return;
    }
    const newPlayer = prompt('Player:', d.player);
    if (!newPlayer) return;
    const newStartDateStr = prompt('Start Date (YYYY-MM-DD):', d.period.split(' - ')[0].split(' ').reverse().join('-'));
    const newEndDateStr = prompt('End Date (YYYY-MM-DD):', d.period.split(' - ')[1].split(' ').reverse().join('-'));
    if (!newStartDateStr || !newEndDateStr) return;
    const newStartDate = new Date(newStartDateStr);
    const newEndDate = new Date(newEndDateStr);
    newEndDate.setHours(23, 59, 59, 999);
    if (isNaN(newStartDate) || isNaN(newEndDate)) {
      alert('Invalid date selected.');
      return;
    }
    if (newStartDate > newEndDate) {
      alert('Start date must be before end date.');
      return;
    }
    const options = { month: 'short', day: 'numeric' };
    const newStartFmt = newStartDate.toLocaleDateString('en-US', options);
    const newEndFmt = newEndDate.toLocaleDateString('en-US', options);
    const newPeriod = `${newStartFmt} - ${newEndFmt}`;
    const stats = {};
    const snapshot = await db.collection('scorecards').get();
    snapshot.forEach(doc => {
      const card = doc.data();
      if (!card || !card.players) return;
      const cardDate = new Date(card.date);
      if (cardDate >= newStartDate && cardDate <= newEndDate) {
        card.players.forEach(p => {
          if (p.player !== newPlayer) return;
          if (!stats[p.player]) stats[p.player] = { matches: 0, win: 0, gs: 0, motm: 0, photo: p.photo || DEFAULT_PHOTO };
          const o = stats[p.player];
          o.matches += p.matches || 0;
          o.win += p.win || 0;
          o.gs += p.gs || 0;
          o.motm += p.motm || 0;
          if (p.photo) o.photo = p.photo;
        });
      }
    });
    const pStats = stats[newPlayer];
    if (!pStats || pStats.matches === 0) {
      alert('No stats found for the player in the new period.');
      return;
    }
    await db.collection('hallOfFame').doc(id).update({
      type: newType,
      player: newPlayer,
      period: newPeriod,
      stats: {
        matches: pStats.matches,
        win: pStats.win,
        gs: pStats.gs,
        motm: pStats.motm
      },
      photo: pStats.photo,
      timestamp: firebase.firestore.FieldValue.serverTimestamp()
    });
    alert('Updated successfully.');
    await displayHallOfFame();
  } catch (err) {
    console.error('Edit HOF error:', err);
    alert('Edit failed: ' + err.message);
  }
}

async function displayHallOfFame() {
  const container = document.getElementById('hofContainer');
  container.innerHTML = '<div class="small">Loading Hall of Fame...</div>';
  try {
    console.log('Fetching Hall of Fame data...');
    const hofSnapshot = await db.collection('hallOfFame').orderBy('timestamp', 'desc').get();
    let html = '<h3 style="font-size:26px;">Player of the Week / Month</h3>';
    if (hofSnapshot.empty) {
      console.warn('No Hall of Fame entries found.');
      html += '<div class="small">No Player of the Week/Month entries yet. Add one using the form above.</div>';
    } else {
      console.log(`Found ${hofSnapshot.size} HOF entries`);
      hofSnapshot.forEach(doc => {
        const d = doc.data();
        const title = `Player of the ${d.type.charAt(0).toUpperCase() + d.type.slice(1)}`;
        html += `
          <div class="hof-card">
            <div style="position:relative; margin-right:20px;">
              <img src="${escapeHtml(d.photo || DEFAULT_PHOTO)}" onerror="this.src='${DEFAULT_PHOTO}';">
              <div class="title">${escapeHtml(title)}</div>
              <div class="period">${escapeHtml(d.period)}</div>
            </div>
            <div>
              <div class="player-name">${escapeHtml(d.player)}</div>
              <div class="stats">Matches: ${d.stats.matches || 0}, Wins: ${d.stats.win || 0}, Goals: ${d.stats.gs || 0}, MOTM: ${d.stats.motm || 0}</div>
              ${isAdmin ? `<br><button onclick="editHOF('${d.id}')">Edit</button> <button onclick="deleteHOF('${d.id}')">Delete</button>` : ''}
            </div>
          </div>`;
      });
    }

    // Record Holders
    console.log('Fetching scorecards for record holders...');
    const stats = {};
    const scorecardSnapshot = await db.collection('scorecards').get();
    if (scorecardSnapshot.empty) {
      console.warn('No scorecards found for record holders.');
      html += '<h3 style="font-size:26px;">Record Holders</h3><div class="small">No scorecard data available for record holders.</div>';
    } else {
      scorecardSnapshot.forEach(doc => {
        (doc.data().players || []).forEach(p => {
          if (!stats[p.player]) stats[p.player] = { matches: 0, win: 0, gs: 0, motm: 0, photo: p.photo || DEFAULT_PHOTO };
          const o = stats[p.player];
          o.matches += p.matches || 0;
          o.win += p.win || 0;
          o.gs += p.gs || 0;
          o.motm += p.motm || 0;
          if (p.photo) o.photo = p.photo;
        });
      });
      const arr = Object.values(stats);
      if (arr.length === 0) {
        console.warn('No players found in scorecards for record holders.');
        html += '<h3 style="font-size:26px;">Record Holders</h3><div class="small">No player data available.</div>';
      } else {
        const mostWins = arr.sort((a, b) => (b.win || 0) - (a.win || 0))[0];
        const topScorer = arr.sort((a, b) => (b.gs || 0) - (a.gs || 0))[0];
        const mostMOTM = arr.sort((a, b) => (b.motm || 0) - (a.motm || 0))[0];
        const mostMatches = arr.sort((a, b) => (b.matches || 0) - (a.matches || 0))[0];
        const records = [
          { p: mostWins, title: 'Most Wins', stat: 'win', label: 'Wins' },
          { p: topScorer, title: 'Top Scorer', stat: 'gs', label: 'Goals' },
          { p: mostMOTM, title: 'Most MOTM', stat: 'motm', label: 'MOTM' },
          { p: mostMatches, title: 'Most Matches', stat: 'matches', label: 'Matches' }
        ];
        html += `
          <h3 style="font-size:26px;">Record Holders</h3>
          <div style="display:flex;flex-wrap:wrap;gap:15px;justify-content:center;">`;
        records.filter(r => r.p).forEach(r => {
          html += `
            <div class="record-card">
              <div style="position:relative;">
                <img src="${escapeHtml(r.p.photo)}" onerror="this.src='${DEFAULT_PHOTO}';">
                <div class="title">${escapeHtml(r.title)}</div>
              </div>
              <div class="player-name">${escapeHtml(r.p.player)}</div>
              <div class="stat">${r.label}: ${r.p[r.stat]}</div>
            </div>`;
        });
        html += `</div>`;
      }
    }

    console.log('Rendering Hall of Fame HTML');
    container.innerHTML = html;
  } catch (err) {
    console.error('HOF display error:', err);
    container.innerHTML = `<div class="small">Failed to load Hall of Fame: ${err.message}</div>`;
  }
}

/* ---------- Initialize ---------- */
(async () => {
  try {
    console.log('Initializing dashboard...');
    await Promise.all([
      displayArchive(),
      displayRanking(),
      displayTopPerformance(),
      populateHOFPlayers(),
      displayHallOfFame()
    ]);
    console.log('Dashboard initialization complete');
  } catch (err) {
    console.error('Initialization error:', err);
    alert('Initialization failed: ' + err.message);
  }
})();
</script>
</body>
</html>
