<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Llfc Dashboard</title>
<style>
/* Same CSS as previous version */
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Montserrat:wght@500;700&display=swap');

body {
  font-family: 'Montserrat', sans-serif;
  background: #1e2a44;
  background-image: linear-gradient(45deg, #1e2a44 25%, #2a4066 25%, #2a4066 50%, #1e2a44 50%, #1e2a44 75%, #2a4066 75%, #2a4066);
  background-size: 20px 20px;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

h1, h2, h3 {
  font-family: 'Orbitron', sans-serif;
  color: #ffd700;
}

.tabs {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.tab-btn {
  padding: 12px 25px;
  background: #2a4066;
  border: 2px solid #00ffff;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 700;
  color: #fff;
  transition: .3s;
  font-family: 'Orbitron', sans-serif;
}

.tab-btn.active {
  background: #00ffff;
  color: #1e2a44;
  box-shadow: 0 0 15px #00ffff;
}

section {
  display: none;
  width: 1080px;
}

section.active {
  display: block;
}

.scorecard {
  width: 1080px;
  max-width: 100%;
  background: #2a4066;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
  border: 2px solid #00ffff;
}

.title-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  margin-bottom: 10px;
}

.tournament-logo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 3px solid #00ffff;
  box-shadow: 0 0 15px rgba(0, 255, 255, 0.5);
  object-fit: cover;
}

.title {
  font-size: 48px;
  font-family: 'Orbitron', sans-serif;
  color: #00ffff;
  text-shadow: 0 0 10px #00ffff;
  border: 3px solid #ffffff;
  padding: 10px 20px;
  border-radius: 10px;
  background: #1e2a44;
}

.date {
  font-size: 20px;
  font-family: 'Orbitron', sans-serif;
  color: #ffd700;
  text-align: center;
  margin-bottom: 25px;
}

.teams {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.team-panel {
  flex: 1;
  text-align: center;
  font-size: 28px;
  font-weight: 800;
  padding: 15px;
  border-radius: 10px;
  border: 3px solid #ffd700;
  font-family: 'Orbitron', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  color: #ffd700;
  background: #3a5088;
  text-shadow: 0 0 8px #ffd700;
}

.team-score {
  width: 80px;
  height: 50px;
  background: #fff;
  color: #1e2a44;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 24px;
  font-weight: 700;
  box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
  border: 3px solid #00ffff;
}

.team-logo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #00ffff;
  box-shadow: 0 0 15px rgba(0, 255, 255, 0.5);
}

#team1panel, #team2panel {
  color: #ffd700;
  text-shadow: 0 0 8px #ffd700;
}

.matches {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.match-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
}

.player-container {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 5px;
  border: 2px solid #00ffff;
  border-radius: 5px;
  height: 40px;
  box-sizing: border-box;
}

.player-left, .player-right {
  font-family: 'Orbitron', sans-serif;
  font-size: 22px;
  font-weight: 600;
  color: #ffffff;
  text-shadow: 0 0 5px #ffffff, 0 0 10px #ffffff;
  font-style: italic;
  text-align: center;
  width: 100%;
}

.score-box {
  width: 100px;
  height: 40px;
  background: #fff;
  color: #1e2a44;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 20px;
  margin: 0 15px;
  border: 3px solid #00ffff;
}

.results-summary {
  margin-top: 20px;
  text-align: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 22px;
}

#winner {
  color: #ffd700;
  font-size: 26px;
  font-weight: 800;
}

#motmScorecard {
  color: #00ffff;
  font-size: 24px;
  font-weight: 700;
  margin-top: 10px;
}

textarea {
  width: 100%;
  height: 200px;
  margin: 20px 0;
  padding: 12px;
  background: #2a4066;
  border: 1px solid #00ffff;
  color: #fff;
  border-radius: 10px;
}

button {
  padding: 12px 25px;
  font-size: 16px;
  margin: 8px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  background: #00ffff;
  color: #1e2a44;
  font-weight: 700;
  font-family: 'Orbitron', sans-serif;
}

button:hover {
  background: #00cccc;
}

.delete-btn {
  background: #ff0000;
  color: #fff;
}

.delete-btn:hover {
  background: #cc0000;
}

.admin-panel, .invitation-panel {
  background: #2a4066;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
}

.admin-panel input, .admin-panel button, .invitation-panel input, .invitation-panel button, .invitation-panel select {
  margin: 8px 0;
}

.admin-player, .admin-team, .admin-group, .admin-matchday, .admin-archive {
  margin: 5px 0;
  padding: 5px;
  background: #1e2a44;
  border-radius: 5px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.url-input, select, input[type="date"], input[type="text"], input[type="password"], input[type="number"] {
  width: 100%;
  padding: 8px;
  background: #1e2a44;
  border: 1px solid #00ffff;
  color: #fff;
  border-radius: 5px;
  font-family: 'Montserrat', sans-serif;
}

.invitation-text, .archive-text {
  background: #1e2a44;
  padding: 15px;
  border: 1px solid #00ffff;
  border-radius: 10px;
  white-space: pre-wrap;
  font-family: 'Montserrat', sans-serif;
  margin-top: 10px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th, td {
  padding: 8px;
  border: 1px solid #00ffff;
  text-align: left;
  font-family: 'Montserrat', sans-serif;
}

th {
  background: #3a5088;
  color: #ffd700;
}

td input {
  width: 100%;
  background: #1e2a44;
  border: none;
  color: #fff;
}

.success-message, .error-message {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 10px 15px;
  border-radius: 5px;
  font-family: 'Orbitron', sans-serif;
  font-size: 14px;
  z-index: 1000;
  box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
}

.success-message {
  background: #1e2a44;
  color: #ffd700;
  border: 1px solid #ffd700;
}

.error-message {
  background: #1e2a44;
  color: #ff3333;
  border: 1px solid #ff3333;
}
</style>
</head>
<body>

<h1>Llfc Dashboard</h1>
<div class="tabs">
  <div class="tab-btn active" onclick="openTab('scorecardTab', this)">Scorecard</div>
  <div class="tab-btn" onclick="openTab('adminTab', this)">Admin</div>
  <div class="tab-btn" onclick="openTab('invitationTab', this)">Invitation</div>
</div>

<!-- Scorecard -->
<section id="scorecardTab" class="active">
  <div class="scorecard" id="scorecard">
    <div class="title-container">
      <img src="https://i.ibb.co/QmTqf2K/default-logo.png" class="tournament-logo" id="tournamentLogo">
      <div class="title" id="tournamentName">LLFC World Cup 2025</div>
    </div>
    <div class="date" id="tournamentDate">08 October 2025</div>
    <div class="teams">
      <div class="team-panel" id="team1panel">Team 1</div>
      <div class="team-score" id="team1score">0</div>
      <div class="team-score" id="team2score">0</div>
      <div class="team-panel" id="team2panel">Team 2</div>
    </div>
    <div class="matches" id="matches"></div>
    <div class="results-summary">
      <div id="winner">Winner: -</div>
      <div id="motmScorecard">Man of the Match: -</div>
    </div>
  </div>
  <textarea id="pasteText" placeholder="Paste matches here"></textarea><br>
  <button onclick="generateScorecard()">Generate & Archive Scorecard</button>
  <button onclick="downloadScorecard()">Download Scorecard</button>
</section>

<!-- Admin -->
<section id="adminTab">
  <h2>Admin Section</h2>
  <div class="admin-panel">
    <h3>Matchday Invitation Setup (Password Protected)</h3>
    <input type="password" id="adminPassword" placeholder="Enter Password (Fardous)">
    <button onclick="unlockMatchdaySetup()">Unlock</button>
    <div id="matchdaySetup" style="display: none;">
      <h3>Add Matchday</h3>
      <input type="date" id="matchdayDate">
      <select id="team1Select"></select>
      <input type="text" id="team1Manual" placeholder="Or enter Team 1 manually">
      <select id="team2Select"></select>
      <input type="text" id="team2Manual" placeholder="Or enter Team 2 manually">
      <input type="number" id="groupNumber" min="1" max="16" placeholder="Group Number (1-16)">
      <button onclick="addMatchday()">Add Matchday</button>
      <h3>Saved Matchdays</h3>
      <div id="matchdayList"></div>
      <hr>
      <h3>Add Group</h3>
      <input type="text" id="groupName" placeholder="Group Name">
      <input type="text" id="groupLink" placeholder="Group Link (e.g., https://m.me/j/...)">
      <input type="text" id="official1" placeholder="Official 1 Name">
      <input type="text" id="official2" placeholder="Official 2 Name">
      <button onclick="addGroup()">Add Group</button>
      <h3>Saved Groups</h3>
      <div id="groupList"></div>
      <hr>
      <h3>Squad Submit Link</h3>
      <input type="text" id="squadSubmitLink" placeholder="Squad Submit Link (e.g., https://forms.gle/...)">
      <button onclick="saveSquadLink()">Save Squad Link</button>
      <h3>Current Squad Submit Link</h3>
      <div id="squadLinkDisplay"></div>
      <hr>
      <h3>Scorecard Archive</h3>
      <div id="archiveList"></div>
      <hr>
      <h3>Player Rankings</h3>
      <table id="rankingTable">
        <thead>
          <tr>
            <th>Player</th>
            <th>Team</th>
            <th>Matches Played</th>
            <th>Wins</th>
            <th>Draws</th>
            <th>Losses</th>
            <th>Win %</th>
            <th>GD</th>
            <th>MOTM</th>
            <th>Score</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody id="rankingBody"></tbody>
      </table>
      <h3>Merge Players</h3>
      <select id="mergePlayer1"></select>
      <select id="mergePlayer2"></select>
      <button onclick="mergePlayers()">Merge Players</button>
    </div>
    <hr>
    <h3>Add Tournament Logo</h3>
    <input type="file" id="tournamentLogoInput" accept="image/*">
    <input type="text" id="tournamentLogoUrl" class="url-input" placeholder="Tournament Logo URL">
    <button onclick="addTournamentLogo()">Add Tournament Logo</button>
    <button class="delete-btn" onclick="deleteTournamentLogo()">Delete Tournament Logo</button>
    <h3>Current Tournament Logo</h3>
    <div id="tournamentLogoDisplay"></div>
    <hr>
    <h3>Add Player</h3>
    <input type="text" id="playerNameInput" placeholder="Player Name">
    <input type="file" id="playerPhotoInput" accept="image/*">
    <input type="text" id="playerPhotoUrl" class="url-input" placeholder="Player Photo URL">
    <button onclick="addPlayer()">Add Player</button>
    <h3>Saved Players</h3>
    <div id="playerList"></div>
    <hr>
    <h3>Add Team</h3>
    <input type="text" id="teamNameInput" placeholder="Team Name">
    <input type="file" id="teamLogoInput" accept="image/*">
    <input type="text" id="teamLogoUrl" class="url-input" placeholder="Team Logo URL">
    <button onclick="addTeam()">Add Team</button>
    <h3>Saved Teams</h3>
    <div id="teamList"></div>
    <hr>
    <h3>Storage Management</h3>
    <button class="delete-btn" onclick="clearStorage()">Clear All Storage</button>
  </div>
</section>

<!-- Invitation -->
<section id="invitationTab">
  <h2>Matchday Invitation</h2>
  <div class="invitation-panel">
    <h3>Select Official</h3>
    <select id="officialSelect" onchange="displayInvitation()"></select>
    <div id="invitationDisplay"></div>
  </div>
</section>

<!-- Success and Error Message Overlays -->
<div id="successMessage" class="success-message" style="display: none;"></div>
<div id="errorMessage" class="error-message" style="display: none;"></div>

<!-- Firebase SDK -->
<script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-storage-compat.js"></script>
<!-- html2canvas for download -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
// Your Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLctDopPq4",
  authDomain: "llfc-4d2df.firebaseapp.com",
  projectId: "llfc-4d2df",
  storageBucket: "llfc-4d2df.firebasestorage.app",
  messagingSenderId: "697058785471",
  appId: "1:697058785471:web:7481cae8fe6b682d762e0a"
};

// Initialize Firebase with error handling
let storage;
try {
  if (typeof firebase === 'undefined') {
    throw new Error("Firebase SDK not loaded");
  }
  firebase.initializeApp(firebaseConfig);
  storage = firebase.storage();
  console.log("Firebase initialized successfully");
} catch (e) {
  console.error("Firebase initialization failed:", e.message);
  showError("Failed to load Firebase SDK. Check your internet connection or try again later.");
}

let playerPhotoMap = JSON.parse(localStorage.getItem("playerPhotoMap") || "{}");
let teamLogoMap = JSON.parse(localStorage.getItem("teamLogoMap") || "{}");
let matchdays = JSON.parse(localStorage.getItem("matchdays") || "[]");
let groups = JSON.parse(localStorage.getItem("groups") || "[]");
let squadSubmitLink = localStorage.getItem("squadSubmitLink") || "";
let tournamentLogo = localStorage.getItem("tournamentLogo") || "https://i.ibb.co/QmTqf2K/default-logo.png";
let archives = JSON.parse(localStorage.getItem("archives") || "[]");
let playerRankings = JSON.parse(localStorage.getItem("playerRankings") || "{}");
const defaultAvatar = "https://i.ibb.co/3R3p9rV/default-avatar.png";
const defaultLogo = "https://i.ibb.co/QmTqf2K/default-logo.png";

const successDiv = document.getElementById("successMessage");
const errorDiv = document.getElementById("errorMessage");

function showSuccess(message, timeout = 3000) {
  successDiv.textContent = message;
  successDiv.style.display = "block";
  errorDiv.style.display = "none";
  setTimeout(() => successDiv.style.display = "none", timeout);
}

function showError(message, timeout = 3000) {
  errorDiv.textContent = message;
  errorDiv.style.display = "block";
  successDiv.style.display = "none";
  setTimeout(() => errorDiv.style.display = "none", timeout);
}

function safeSetItem(key, value) {
  try {
    localStorage.setItem(key, value);
    return true;
  } catch (e) {
    if (e.name === 'QuotaExceededError') {
      showError('Storage quota exceeded! Clear storage via "Clear All Storage" button and try again.');
    } else {
      showError('Storage error: ' + e.message);
    }
    return false;
  }
}

function validateImageUrl(url) {
  return new Promise((resolve) => {
    const img = new Image();
    img.onload = () => resolve(true);
    img.onerror = () => resolve(false);
    img.src = url;
  });
}

async function uploadToFirebase(file, path) {
  if (!storage) {
    throw new Error("Firebase Storage is not initialized. Check Firebase setup.");
  }
  if (!file || !file.type.startsWith('image/')) {
    throw new Error("Please select a valid image file.");
  }
  try {
    const storageRef = storage.ref(path);
    await storageRef.put(file);
    const url = await storageRef.getDownloadURL();
    return url;
  } catch (e) {
    throw new Error("Failed to upload to Firebase: " + e.message);
  }
}

function clearStorage() {
  if (confirm('Are you sure you want to clear all saved data (logos, photos, matchdays, groups, archives, rankings)?')) {
    localStorage.clear();
    playerPhotoMap = {};
    teamLogoMap = {};
    matchdays = [];
    groups = [];
    squadSubmitLink = "";
    archives = [];
    playerRankings = {};
    tournamentLogo = defaultLogo;
    updatePlayerList();
    updateTeamList();
    updateMatchdayList();
    updateGroupList();
    updateSquadLinkDisplay();
    updateArchiveList();
    updateRankingTable();
    updateMergeSelects();
    document.getElementById("tournamentLogo").src = tournamentLogo;
    showSuccess("All storage cleared!");
  }
}

function unlockMatchdaySetup() {
  const password = document.getElementById("adminPassword").value;
  if (password === "Fardous") {
    document.getElementById("matchdaySetup").style.display = "block";
    showSuccess("Matchday setup unlocked!");
  } else {
    showError("Incorrect password!");
  }
}

function updateTeamSelect() {
  const team1Select = document.getElementById("team1Select");
  const team2Select = document.getElementById("team2Select");
  team1Select.innerHTML = '<option value="">Select Team 1</option>';
  team2Select.innerHTML = '<option value="">Select Team 2</option>';
  Object.keys(teamLogoMap).forEach(team => {
    team1Select.innerHTML += `<option value="${team}">${team}</option>`;
    team2Select.innerHTML += `<option value="${team}">${team}</option>`;
  });
}

function addMatchday() {
  const date = document.getElementById("matchdayDate").value;
  let team1 = document.getElementById("team1Select").value || document.getElementById("team1Manual").value.trim();
  let team2 = document.getElementById("team2Select").value || document.getElementById("team2Manual").value.trim();
  const groupNumber = document.getElementById("groupNumber").value;

  if (!date || !team1 || !team2 || !groupNumber) {
    showError("Please fill in all fields (date, teams, group number).");
    return;
  }

  if (Object.keys(teamLogoMap).length >= 32 && !teamLogoMap[team1]) {
    showError("Maximum 32 teams allowed. Add team via 'Add Team' first.");
    return;
  }

  matchdays.push({ date, team1, team2, groupNumber: parseInt(groupNumber) });
  if (safeSetItem("matchdays", JSON.stringify(matchdays))) {
    updateMatchdayList();
    document.getElementById("matchdayDate").value = "";
    document.getElementById("team1Select").value = "";
    document.getElementById("team1Manual").value = "";
    document.getElementById("team2Select").value = "";
    document.getElementById("team2Manual").value = "";
    document.getElementById("groupNumber").value = "";
    showSuccess("Matchday added!");
  }
}

function updateMatchdayList() {
  const list = document.getElementById("matchdayList");
  list.innerHTML = "";
  matchdays.forEach((m, index) => {
    list.innerHTML += `
      <div class="admin-matchday">
        ${m.date}: ${m.team1} vs ${m.team2} (Group ${m.groupNumber})
        <button class="delete-btn" onclick="deleteMatchday(${index})">Delete</button>
      </div>
    `;
  });
  updateOfficialSelect();
}

function deleteMatchday(index) {
  matchdays.splice(index, 1);
  if (safeSetItem("matchdays", JSON.stringify(matchdays))) {
    updateMatchdayList();
    showSuccess("Matchday deleted!");
  }
}

function addGroup() {
  const name = document.getElementById("groupName").value.trim();
  const link = document.getElementById("groupLink").value.trim();
  const official1 = document.getElementById("official1").value.trim();
  const official2 = document.getElementById("official2").value.trim();

  if (!name || !link || !official1 || !official2) {
    showError("Please fill in all group fields.");
    return;
  }

  if (groups.length >= 16) {
    showError("Maximum 16 groups allowed.");
    return;
  }

  groups.push({ name, link, officials: [official1, official2] });
  if (safeSetItem("groups", JSON.stringify(groups))) {
    updateGroupList();
    document.getElementById("groupName").value = "";
    document.getElementById("groupLink").value = "";
    document.getElementById("official1").value = "";
    document.getElementById("official2").value = "";
    showSuccess("Group added!");
  }
}

function updateGroupList() {
  const list = document.getElementById("groupList");
  list.innerHTML = "";
  groups.forEach((g, index) => {
    list.innerHTML += `
      <div class="admin-group">
        ${g.name}: ${g.link} (Officials: ${g.officials.join(", ")})
        <button class="delete-btn" onclick="deleteGroup(${index})">Delete</button>
      </div>
    `;
  });
  updateOfficialSelect();
}

function deleteGroup(index) {
  groups.splice(index, 1);
  if (safeSetItem("groups", JSON.stringify(groups))) {
    updateGroupList();
    showSuccess("Group deleted!");
  }
}

function saveSquadLink() {
  const link = document.getElementById("squadSubmitLink").value.trim();
  if (!link) {
    showError("Please enter a squad submit link.");
    return;
  }
  if (safeSetItem("squadSubmitLink", link)) {
    squadSubmitLink = link;
    updateSquadLinkDisplay();
    document.getElementById("squadSubmitLink").value = "";
    showSuccess("Squad submit link saved!");
  }
}

function updateSquadLinkDisplay() {
  document.getElementById("squadLinkDisplay").innerHTML = squadSubmitLink ? `<a href="${squadSubmitLink}" target="_blank">${squadSubmitLink}</a>` : "No link set";
}

function updateOfficialSelect() {
  const select = document.getElementById("officialSelect");
  select.innerHTML = '<option value="">Select Official</option>';
  const officials = new Set();
  groups.forEach(g => g.officials.forEach(o => officials.add(o)));
  officials.forEach(o => {
    select.innerHTML += `<option value="${o}">${o}</option>`;
  });
  displayInvitation();
}

function formatDate(dateStr) {
  const date = new Date(dateStr);
  const month = date.toLocaleString('default', { month: 'long' }).toUpperCase();
  const day = date.getDate().toString().padStart(2, '0');
  return `${day} ${month}`;
}

function generateInvitationText(matchday, group) {
  const groupNumber = group.name.match(/\d+/)?.[0] || group.name;
  return `🔔 LLFC CLUB WORLD CUP Group ${groupNumber}\n\nDate: ${formatDate(matchday.date)}\n\n🔴 ${matchday.team1}\n🔵 ${matchday.team2}\n\n📌 PLEASE JOIN YOUR MATCHDAY GROUP\n${group.link}\n\n✅ Squad Submit Link\n${squadSubmitLink}\n⚠️ PLEASE SUBMIT YOUR SQUAD BEFORE 5:00 PM\n🏅 Officials: ${group.officials.join(", ")}`;
}

function displayInvitation() {
  const official = document.getElementById("officialSelect").value;
  const display = document.getElementById("invitationDisplay");
  display.innerHTML = "";
  if (!official) return;

  const officialGroups = groups.filter(g => g.officials.includes(official));
  officialGroups.forEach(group => {
    const groupMatchdays = matchdays.filter(m => m.groupNumber === parseInt(group.name.match(/\d+/)?.[0]) || m.groupNumber);
    groupMatchdays.forEach(matchday => {
      const text = generateInvitationText(matchday, group);
      display.innerHTML += `
        <div>
          <h3>Group ${group.name} - ${matchday.date}</h3>
          <div class="invitation-text">${text}</div>
          <button onclick="copyText(\`${text.replace(/`/g, "\\`")}\`)">Copy Text</button>
        </div>
      `;
    });
  });
}

function copyText(text) {
  navigator.clipboard.writeText(text).then(() => {
    showSuccess("Invitation text copied!");
  }).catch(err => {
    console.error("Clipboard error:", err);
    showError("Failed to copy text. Try again or check browser permissions.");
  });
}

function levenshteinDistance(a, b) {
  const matrix = Array(b.length + 1).fill().map(() => Array(a.length + 1).fill(0));
  for (let i = 0; i <= a.length; i++) matrix[0][i] = i;
  for (let j = 0; j <= b.length; j++) matrix[j][0] = j;
  for (let j = 1; j <= b.length; j++) {
    for (let i = 1; i <= a.length; i++) {
      const indicator = a[i - 1] === b[j - 1] ? 0 : 1;
      matrix[j][i] = Math.min(
        matrix[j][i - 1] + 1,
        matrix[j - 1][i] + 1,
        matrix[j - 1][i - 1] + indicator
      );
    }
  }
  return matrix[b.length][a.length];
}

function isSimilarName(name1, name2) {
  const maxLen = Math.max(name1.length, name2.length);
  const distance = levenshteinDistance(name1.toLowerCase(), name2.toLowerCase());
  return distance / maxLen <= 0.2; // 80% similarity
}

function updatePlayerRankings(team1, team2, matches, motmPlayer, archiveId) {
  matches.forEach(match => {
    const [p1Raw, s1, s2, p2Raw] = match;
    const p1 = cleanName(p1Raw), p2 = cleanName(p2Raw);
    const team1Exact = team1, team2Exact = team2;

    [ { player: p1, team: team1Exact, score: parseInt(s1), oppScore: parseInt(s2), isMotm: p1Raw.includes("👑") },
      { player: p2, team: team2Exact, score: parseInt(s2), oppScore: parseInt(s1), isMotm: p2Raw.includes("👑") } ]
      .forEach(({ player, team, score, oppScore, isMotm }) => {
        let matchedPlayer = player;
        const existingPlayers = Object.keys(playerRankings);
        const match = existingPlayers.find(p => 
          playerRankings[p].team.toLowerCase() === team.toLowerCase() && 
          isSimilarName(p, player)
        );
        if (match) matchedPlayer = match;

        if (!playerRankings[matchedPlayer]) {
          playerRankings[matchedPlayer] = { team, matchesPlayed: 0, wins: 0, draws: 0, losses: 0, gd: 0, motm: 0, score: 0, winPercentage: 0, matches: [] };
        }
        const outcome = score > oppScore ? 'win' : score === oppScore ? 'draw' : 'loss';
        playerRankings[matchedPlayer].matches.push({ id: archiveId, outcome, score, oppScore });
        if (isMotm) playerRankings[matchedPlayer].motm += 1;
      });
  });

  // Recalculate stats
  Object.keys(playerRankings).forEach(player => {
    const data = playerRankings[player];
    data.matchesPlayed = data.matches.length;
    data.wins = data.matches.filter(m => m.outcome === 'win').length;
    data.draws = data.matches.filter(m => m.outcome === 'draw').length;
    data.losses = data.matches.filter(m => m.outcome === 'loss').length;
    data.gd = data.matches.reduce((sum, m) => sum + (m.score - m.oppScore), 0);
    data.winPercentage = data.matchesPlayed > 0 ? ((data.wins / data.matchesPlayed) * 100).toFixed(2) : 0;
    data.score = (data.wins * 10) + (data.draws * 5) + (data.losses * -7) + (data.gd * 1) + (data.motm * 5);
  });

  // Remove players with no matches
  Object.keys(playerRankings).forEach(player => {
    if (playerRankings[player].matchesPlayed === 0) {
      delete playerRankings[player];
    }
  });

  if (safeSetItem("playerRankings", JSON.stringify(playerRankings))) {
    updateRankingTable();
    updateMergeSelects();
  }
}

function recalculateRankings() {
  playerRankings = {};
  archives.forEach(archive => {
    updatePlayerRankings(archive.team1, archive.team2, archive.matches, archive.motmPlayer, archive.id);
  });
}

function updateRankingTable() {
  const tbody = document.getElementById("rankingBody");
  tbody.innerHTML = "";
  Object.keys(playerRankings).sort((a, b) => playerRankings[b].score - playerRankings[a].score)
    .forEach((player, index) => {
      const data = playerRankings[player];
      tbody.innerHTML += `
        <tr>
          <td><input value="${player}" onchange="editRanking(${index}, 'player', this.value)"></td>
          <td><input value="${data.team}" onchange="editRanking(${index}, 'team', this.value)"></td>
          <td><input type="number" value="${data.matchesPlayed}" onchange="editRanking(${index}, 'matchesPlayed', this.value)"></td>
          <td><input type="number" value="${data.wins}" onchange="editRanking(${index}, 'wins', this.value)"></td>
          <td><input type="number" value="${data.draws}" onchange="editRanking(${index}, 'draws', this.value)"></td>
          <td><input type="number" value="${data.losses}" onchange="editRanking(${index}, 'losses', this.value)"></td>
          <td>${data.winPercentage}%</td>
          <td><input type="number" value="${data.gd}" onchange="editRanking(${index}, 'gd', this.value)"></td>
          <td><input type="number" value="${data.motm}" onchange="editRanking(${index}, 'motm', this.value)"></td>
          <td>${data.score}</td>
          <td><button class="delete-btn" onclick="deleteRanking(${index})">Delete</button></td>
        </tr>
      `;
    });
}

function editRanking(index, field, value) {
  const player = Object.keys(playerRankings)[index];
  if (field === 'player') {
    const data = playerRankings[player];
    delete playerRankings[player];
    playerRankings[value] = data;
  } else {
    playerRankings[player][field] = field === 'team' ? value : parseInt(value) || 0;
    playerRankings[player].winPercentage = playerRankings[player].matchesPlayed > 0 ? 
      ((playerRankings[player].wins / playerRankings[player].matchesPlayed) * 100).toFixed(2) : 0;
    playerRankings[player].score = 
      (playerRankings[player].wins * 10) + 
      (playerRankings[player].draws * 5) + 
      (playerRankings[player].losses * -7) + 
      (playerRankings[player].gd * 1) + 
      (playerRankings[player].motm * 5);
  }
  if (safeSetItem("playerRankings", JSON.stringify(playerRankings))) {
    updateRankingTable();
    updateMergeSelects();
  }
}

function deleteRanking(index) {
  const player = Object.keys(playerRankings)[index];
  delete playerRankings[player];
  if (safeSetItem("playerRankings", JSON.stringify(playerRankings))) {
    updateRankingTable();
    updateMergeSelects();
    showSuccess("Player ranking deleted!");
  }
}

function mergePlayers() {
  const player1 = document.getElementById("mergePlayer1").value;
  const player2 = document.getElementById("mergePlayer2").value;
  if (!player1 || !player2 || player1 === player2) {
    showError("Please select two different players to merge.");
    return;
  }
  if (playerRankings[player1].team !== playerRankings[player2].team) {
    showError("Players must be from the same team to merge.");
    return;
  }
  playerRankings[player1].matches = playerRankings[player1].matches.concat(playerRankings[player2].matches);
  playerRankings[player1].motm += playerRankings[player2].motm;
  delete playerRankings[player2];
  recalculateRankings();
  showSuccess(`Merged ${player2} into ${player1}!`);
}

function updateMergeSelects() {
  const merge1 = document.getElementById("mergePlayer1");
  const merge2 = document.getElementById("mergePlayer2");
  merge1.innerHTML = '<option value="">Select Player 1</option>';
  merge2.innerHTML = '<option value="">Select Player 2</option>';
  Object.keys(playerRankings).forEach(player => {
    merge1.innerHTML += `<option value="${player}">${player} (${playerRankings[player].team})</option>`;
    merge2.innerHTML += `<option value="${player}">${player} (${playerRankings[player].team})</option>`;
  });
}

function saveToArchive(team1, team2, team1Points, team2Points, matches, motmPlayer) {
  const archive = {
    id: Date.now(),
    timestamp: new Date().toISOString(),
    team1,
    team2,
    team1Points,
    team2Points,
    matches,
    motmPlayer,
    inputText: document.getElementById("pasteText").value
  };
  archives.push(archive);
  if (safeSetItem("archives", JSON.stringify(archives))) {
    updateArchiveList();
    showSuccess("Scorecard archived!");
  }
}

function updateArchiveList() {
  const list = document.getElementById("archiveList");
  list.innerHTML = "";
  archives.forEach((archive, index) => {
    list.innerHTML += `
      <div class="admin-archive">
        ${archive.timestamp}: ${archive.team1} vs ${archive.team2} (${archive.team1Points}-${archive.team2Points})
        <button onclick="loadArchive(${index})">Load</button>
        <button onclick="editArchive(${index})">Edit</button>
        <button class="delete-btn" onclick="deleteArchive(${index})">Delete</button>
      </div>
    `;
  });
}

function loadArchive(index) {
  const archive = archives[index];
  document.getElementById("pasteText").value = archive.inputText;
  generateScorecard();
  showSuccess("Archive loaded!");
}

function editArchive(index) {
  const newText = prompt("Edit scorecard text:", archives[index].inputText);
  if (newText) {
    archives[index].inputText = newText;
    if (safeSetItem("archives", JSON.stringify(archives))) {
      updateArchiveList();
      recalculateRankings();
      showSuccess("Archive updated!");
    }
  }
}

function deleteArchive(index) {
  archives.splice(index, 1);
  if (safeSetItem("archives", JSON.stringify(archives))) {
    updateArchiveList();
    recalculateRankings();
    showSuccess("Archive deleted and rankings updated!");
  }
}

document.addEventListener("DOMContentLoaded", () => {
  document.getElementById("tournamentLogo").src = tournamentLogo;
  updateTournamentLogoDisplay();
  updatePlayerList();
  updateTeamList();
  updateMatchdayList();
  updateGroupList();
  updateSquadLinkDisplay();
  updateArchiveList();
  updateRankingTable();
  updateMergeSelects();
  updateTeamSelect();
  updateOfficialSelect();
});

function openTab(tabId, btn) {
  document.querySelectorAll("section").forEach(s => s.classList.remove("active"));
  document.getElementById(tabId).classList.add("active");
  document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
  btn.classList.add("active");
}

function cleanName(name) {
  return name.replace(/[@()⭐⛔🔑🔥👑!*\-_]/g, '').trim();
}

function getTeamLogo(teamName) {
  const teamMapKeys = Object.keys(teamLogoMap);
  const matchedKey = teamMapKeys.find(key => key.toLowerCase() === teamName.toLowerCase());
  return teamLogoMap[matchedKey] || defaultLogo;
}

function generateScorecard() {
  const text = document.getElementById("pasteText").value;
  const lines = text.split("\n");

  let teamLine = lines.find(l => l.includes("⚔️"));
  let team1 = teamLine ? cleanName(teamLine.split("⚔️")[0]).trim() : "Team 1";
  let team2 = teamLine ? cleanName(teamLine.split("⚔️")[1]).trim() : "Team 2";

  const matchesContainer = document.getElementById("matches");
  matchesContainer.innerHTML = "";

  let team1Points = 0, team2Points = 0, motmPlayer = "";
  const matches = [];

  lines.forEach(line => {
    if (line.includes("🆚")) {
      let m = line.match(/(.+?)\s*\(?(\d+)\)?\s*🆚\s*\(?(\d+)\)?\s*(.+)/);
      if (m) {
        let p1Raw = m[1].trim(), p2Raw = m[4].trim();
        let p1 = cleanName(p1Raw), p2 = cleanName(p2Raw);
        let s1 = parseInt(m[2]), s2 = parseInt(m[3]);

        if (p1Raw.includes("👑")) motmPlayer = p1;
        if (p2Raw.includes("👑")) motmPlayer = p2;

        matches.push([p1Raw, s1, s2, p2Raw]);
        matchesContainer.innerHTML += `
          <div class="match-row">
            <div class="player-container player-left">${p1}</div>
            <div class="score-box">${s1} - ${s2}</div>
            <div class="player-container player-right">${p2}</div>
          </div>
        `;

        if (s1 > s2) team1Points += 3;
        else if (s2 > s1) team2Points += 3;
        else { team1Points++; team2Points++; }
      }
    }
  });

  let team1LogoSrc = getTeamLogo(team1);
  let team2LogoSrc = getTeamLogo(team2);
  let team1Logo = `<img src="${team1LogoSrc}" class="team-logo" onerror="this.src='${defaultLogo}'">`;
  let team2Logo = `<img src="${team2LogoSrc}" class="team-logo" onerror="this.src='${defaultLogo}'">`;

  document.getElementById("team1panel").innerHTML = `${team1Logo}${team1}`;
  document.getElementById("team2panel").innerHTML = `${team2Logo}${team2}`;
  document.getElementById("team1score").innerText = team1Points;
  document.getElementById("team2score").innerText = team2Points;

  const winner = team1Points > team2Points ? team1 : (team2Points > team1Points ? team2 : "Draw");
  document.getElementById("winner").innerText = "Winner: " + winner;
  document.getElementById("motmScorecard").innerText = "Man of the Match: " + (motmPlayer || "-");
  document.getElementById("tournamentLogo").src = tournamentLogo;

  saveToArchive(team1, team2, team1Points, team2Points, matches, motmPlayer);
  updatePlayerRankings(team1, team2, matches, motmPlayer, archives[archives.length - 1]?.id);
}

async function addTournamentLogo() {
  const fileInput = document.getElementById("tournamentLogoInput");
  const urlInput = document.getElementById("tournamentLogoUrl");
  let imageUrl = urlInput.value.trim();
  const file = fileInput.files[0];

  try {
    if (file) {
      imageUrl = await uploadToFirebase(file, `images/tournament-logo.jpg`);
      urlInput.value = imageUrl;
    } else if (!imageUrl) {
      showError("Please select a file or enter a valid image URL.");
      return;
    }

    const isValid = await validateImageUrl(imageUrl);
    if (!isValid) {
      showError("Invalid image URL or image failed to load.");
      return;
    }

    if (safeSetItem("tournamentLogo", imageUrl)) {
      tournamentLogo = imageUrl;
      document.getElementById("tournamentLogo").src = tournamentLogo;
      updateTournamentLogoDisplay();
      fileInput.value = '';
      showSuccess("Tournament logo successfully saved!");
    }
  } catch (e) {
    showError("Upload failed: " + e.message);
  }
}

function deleteTournamentLogo() {
  if (safeSetItem("tournamentLogo", defaultLogo)) {
    tournamentLogo = defaultLogo;
    document.getElementById("tournamentLogo").src = tournamentLogo;
    updateTournamentLogoDisplay();
    document.getElementById("tournamentLogoInput").value = '';
    document.getElementById("tournamentLogoUrl").value = '';
    showSuccess("Tournament logo reset to default!");
  }
}

function updateTournamentLogoDisplay() {
  const display = document.getElementById("tournamentLogoDisplay");
  display.innerHTML = `<img src="${tournamentLogo}" class="tournament-logo" onerror="this.src='${defaultLogo}'">`;
}

async function addPlayer() {
  const name = document.getElementById("playerNameInput").value.trim();
  const fileInput = document.getElementById("playerPhotoInput");
  const urlInput = document.getElementById("playerPhotoUrl");
  let imageUrl = urlInput.value.trim();
  const file = fileInput.files[0];

  try {
    if (!name) {
      showError("Please enter a player name.");
      return;
    }
    if (file) {
      imageUrl = await uploadToFirebase(file, `images/players/${encodeURIComponent(name)}.jpg`);
      urlInput.value = imageUrl;
    } else if (!imageUrl) {
      showError("Please select a file or enter a valid image URL.");
      return;
    }

    const isValid = await validateImageUrl(imageUrl);
    if (!isValid) {
      showError("Invalid image URL or image failed to load.");
      return;
    }

    playerPhotoMap[name] = imageUrl;
    if (safeSetItem("playerPhotoMap", JSON.stringify(playerPhotoMap))) {
      updatePlayerList();
      document.getElementById("playerNameInput").value = '';
      document.getElementById("playerPhotoInput").value = '';
      document.getElementById("playerPhotoUrl").value = '';
      showSuccess("Player successfully saved!");
    } else {
      delete playerPhotoMap[name];
    }
  } catch (e) {
    showError("Upload failed: " + e.message);
  }
}

function updatePlayerList() {
  const list = document.getElementById("playerList");
  list.innerHTML = "";
  Object.keys(playerPhotoMap).forEach(p => {
    list.innerHTML += `
      <div class="admin-player">
        <img src="${playerPhotoMap[p] || defaultAvatar}" onerror="this.src='${defaultAvatar}'" style="width: 40px; height: 40px; border-radius: 50%;"> ${p}
      </div>
    `;
  });
}

async function addTeam() {
  const name = document.getElementById("teamNameInput").value.trim();
  const fileInput = document.getElementById("teamLogoInput");
  const urlInput = document.getElementById("teamLogoUrl");
  let imageUrl = urlInput.value.trim();
  const file = fileInput.files[0];

  try {
    if (!name) {
      showError("Please enter a team name.");
      return;
    }
    if (Object.keys(teamLogoMap).length >= 32) {
      showError("Maximum 32 teams allowed.");
      return;
    }
    if (file) {
      imageUrl = await uploadToFirebase(file, `images/teams/${encodeURIComponent(name)}.jpg`);
      urlInput.value = imageUrl;
    } else if (!imageUrl) {
      showError("Please select a file or enter a valid image URL.");
      return;
    }

    const isValid = await validateImageUrl(imageUrl);
    if (!isValid) {
      showError("Invalid image URL or image failed to load.");
      return;
    }

    teamLogoMap[name] = imageUrl;
    if (safeSetItem("teamLogoMap", JSON.stringify(teamLogoMap))) {
      updateTeamList();
      updateTeamSelect();
      document.getElementById("teamNameInput").value = '';
      document.getElementById("teamLogoInput").value = '';
      document.getElementById("teamLogoUrl").value = '';
      showSuccess("Team logo successfully saved!");
    } else {
      delete teamLogoMap[name];
    }
  } catch (e) {
    showError("Upload failed: " + e.message);
  }
}

function updateTeamList() {
  const list = document.getElementById("teamList");
  list.innerHTML = "";
  Object.keys(teamLogoMap).forEach(t => {
    list.innerHTML += `
      <div class="admin-team">
        <img src="${teamLogoMap[t] || defaultLogo}" onerror="this.src='${defaultLogo}'" style="width: 40px; height: 40px;"> ${t}
      </div>
    `;
  });
  updateTeamSelect();
}

function downloadScorecard() {
  const card = document.getElementById("scorecard");
  html2canvas(card, {scale: 2}).then(canvas => {
    const link = document.createElement("a");
    link.download = "scorecard.png";
    link.href = canvas.toDataURL("image/png");
    link.click();
  });
}
</script>
</body>
</html>
