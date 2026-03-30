
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Llfc Dashboard</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Montserrat:wght@500;700&display=swap');

body {
  font-family: 'Montserrat', sans-serif;
  background: #1a1a1a;
  background-image: linear-gradient(45deg, #1a1a1a 25%, #2c2c2c 25%, #2c2c2c 50%, #1a1a1a 50%, #1a1a1a 75%, #2c2c2c 75%, #2c2c2c);
  background-size: 20px 20px;
  color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  min-height: 100vh;
}

h1, h2, h3 {
  font-family: 'Orbitron', sans-serif;
  color: #d4af37;
  text-shadow: 0 0 5px rgba(212, 175, 55, 0.5);
}

.tabs {
  display: flex;
  gap: 15px;
  margin-bottom: 20px;
}

.tab-btn {
  padding: 12px 25px;
  background: #2c2c2c;
  border: 2px solid #d4af37;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 700;
  color: #ffffff;
  transition: all 0.3s ease;
  font-family: 'Orbitron', sans-serif;
}

.tab-btn:hover {
  background: #d4af37;
  color: #1a1a1a;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.7);
}

.tab-btn.active {
  background: #d4af37;
  color: #1a1a1a;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.7);
}

section {
  display: none;
  width: 1080px;
  max-width: 100%;
}

section.active {
  display: block;
}

/* Original Scorecard */
.scorecard {
  width: 1080px;
  max-width: 100%;
  background: #2c2c2c;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
  border: 2px solid #d4af37;
  margin-bottom: 20px;
}

/* Alternative Scorecard */
.scorecard-alt {
  width: 1080px;
  max-width: 100%;
  background: #ffffff;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
  border: 2px solid #87CEFA;
  margin-bottom: 20px;
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
  border: 3px solid #87CEFA;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.5);
  object-fit: cover;
}

.scorecard .title {
  font-size: 48px;
  font-family: 'Orbitron', sans-serif;
  color: #ffffff;
  text-shadow: 0 0 10px rgba(212, 175, 55, 0.7);
  border: 3px solid #87CEFA;
  padding: 10px 20px;
  border-radius: 10px;
  background: #1a1a1a;
}

.scorecard-alt .title {
  font-size: 48px;
  font-family: 'Orbitron', sans-serif;
  color: #000000;
  border: 3px solid #87CEFA;
  padding: 10px 20px;
  border-radius: 10px;
  background: #ffffff;
}

.scorecard .date {
  font-size: 24px;
  font-family: 'Orbitron', sans-serif;
  color: #d4af37;
  text-align: center;
  margin-bottom: 25px;
}

.scorecard-alt .date {
  font-size: 24px;
  font-family: 'Orbitron', sans-serif;
  color: #000000;
  text-align: center;
  margin-bottom: 25px;
}

.teams {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.scorecard .team-panel {
  flex: 1;
  text-align: center;
  font-size: 28px;
  font-weight: 800;
  padding: 15px;
  border-radius: 10px;
  border: 3px solid #87CEFA;
  font-family: 'Orbitron', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  color: #ffffff;
  background: #2c2c2c;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.5);
}

.scorecard-alt .team-panel {
  flex: 1;
  text-align: center;
  font-size: 28px;
  font-weight: 800;
  padding: 15px;
  border-radius: 10px;
  border: 3px solid #87CEFA;
  font-family: 'Orbitron', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  color: #000000;
  background: #ffffff;
}

.team-score {
  width: 80px;
  height: 50px;
  background: #ffffff;
  color: #000000;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 24px;
  font-weight: 700;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
  border: 3px solid #87CEFA;
}

.team-logo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #87CEFA;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.5);
}

.scorecard #team1panel, .scorecard #team2panel {
  color: #ffffff;
  text-shadow: 0 0 8px rgba(212, 175, 55, 0.5);
}

.scorecard-alt #team1panel-alt, .scorecard-alt #team2panel-alt {
  color: #000000;
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
  border: 2px solid #87CEFA;
  border-radius: 5px;
  height: 40px;
  box-sizing: border-box;
  position: relative;
}

.scorecard .player-container {
  background: #2c2c2c;
}

.scorecard-alt .player-container {
  background: #ffffff;
}

.scorecard .player-left, .scorecard .player-right {
  font-family: 'Orbitron', sans-serif;
  font-size: 22px;
  font-weight: 600;
  color: #ffffff;
  text-shadow: 0 0 5px rgba(212, 175, 55, 0.5);
  font-style: italic;
  text-align: center;
  width: 100%;
}

.scorecard-alt .player-left, .scorecard-alt .player-right {
  font-family: 'Orbitron', sans-serif;
  font-size: 22px;
  font-weight: 600;
  color: #000000;
  font-style: italic;
  text-align: center;
  width: 100%;
}

.motm-player {
  border: 3px solid #00ff00;
}

.scorecard .motm-player .player-left, .scorecard .motm-player .player-right {
  font-family: 'Montserrat', sans-serif;
  font-size: 26px;
  font-weight: 800;
  color: ##FF4500;
  text-shadow: none;
  font-style: normal;
}

.scorecard-alt .motm-player .player-left, .scorecard-alt .motm-player .player-right {
  font-family: 'Montserrat', sans-serif;
  font-size: 26px;
  font-weight: 800;
  color: #FF4500;
  font-style: normal;
}

.motm-player::before {
  content: '👑';
  position: absolute;
  top: -18px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 16px;
  border-radius: 5px;
  padding: 0 5px;
}

.scorecard .motm-player::before {
  background: #1a1a1a;
}

.scorecard-alt .motm-player::before {
  background: #ffffff;
}

.score-box {
  width: 100px;
  height: 40px;
  background: #ffffff;
  color: #000000;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 20px;
  margin: 0 15px;
  border: 3px solid #87CEFA;
}

.results-summary {
  margin-top: 20px;
  text-align: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 22px;
}

.scorecard .results-summary {
  color: #ffffff;
}

.scorecard-alt .results-summary {
  color: #000000;
}

.scorecard #winner {
  color: #d4af37;
  font-size: 26px;
  font-weight: 800;
}

.scorecard-alt #winner-alt {
  color: #d4af37;
  font-size: 26px;
  font-weight: 800;
}

.scorecard #motmScorecard {
  color: #ffffff;
  font-size: 24px;
  font-weight: 700;
  margin-top: 10px;
  text-shadow: 0 0 5px rgba(212, 175, 55, 0.5);
}

.scorecard-alt #motmScorecard-alt {
  color: #000000;
  font-size: 24px;
  font-weight: 700;
  margin-top: 10px;
}

textarea {
  width: 100%;
  height: 200px;
  margin: 20px 0;
  padding: 12px;
  background: #2c2c2c;
  border: 1px solid #87CEFA;
  color: #ffffff;
  border-radius: 10px;
  font-family: 'Montserrat', sans-serif;
}

button {
  padding: 12px 25px;
  font-size: 16px;
  margin: 8px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  background: #87CEFA;
  color: #1a1a1a;
  font-weight: 700;
  font-family: 'Orbitron', sans-serif;
  transition: all 0.3s ease;
}

button:hover {
  background: #b8972a;
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.7);
}

.delete-btn {
  background: #ff3333;
  color: #ffffff;
}

.delete-btn:hover {
  background: #cc0000;
  box-shadow: 0 0 10px rgba(255, 51, 51, 0.7);
}

.admin-panel, .invitation-panel {
  background: #2c2c2c;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(212, 175, 55, 0.2);
  border: 2px solid #d4af37;
}

.admin-panel input, .admin-panel button, .invitation-panel input, .invitation-panel button, .invitation-panel select {
  margin: 8px 0;
}

.admin-player, .admin-team, .admin-group, .admin-matchday, .admin-archive, .admin-tournament {
  margin: 5px 0;
  padding: 5px;
  background: #1a1a1a;
  border-radius: 5px;
  display: flex;
  align-items: center;
  gap: 8px;
  color: #ffffff;
}

.url-input, select, input[type="date"], input[type="text"], input[type="password"], input[type="number"] {
  width: 100%;
  padding: 8px;
  background: #1a1a1a;
  border: 1px solid #d4af37;
  color: #ffffff;
  border-radius: 5px;
  font-family: 'Montserrat', sans-serif;
}

.invitation-text, .archive-text {
  background: #1a1a1a;
  padding: 15px;
  border: 1px solid #d4af37;
  border-radius: 10px;
  white-space: pre-wrap;
  font-family: 'Montserrat', sans-serif;
  margin-top: 10px;
  color: #ffffff;
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
  box-shadow: 0 0 10px rgba(212, 175, 55, 0.5);
}

.success-message {
  background: #1a1a1a;
  color: #d4af37;
  border: 1px solid #d4af37;
}

.error-message {
  background: #1a1a1a;
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
  <!-- Original Scorecard -->
  <h2>Original Scorecard</h2>
  <div class="scorecard" id="scorecard">
    <div class="title-container">
      <img src="https://i.ibb.co/QmTqf2K/default-logo.png" class="tournament-logo" id="tournamentLogo">
      <div class="title" id="tournamentName">Gkec Unity Cup</div>
    </div>
    <div class="date" id="tournamentDate">Group Stage</div>
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
  <!-- Alternative Scorecard -->
  <h2>Alternative Scorecard</h2>
  <div class="scorecard-alt" id="scorecard-alt">
    <div class="title-container">
      <img src="https://i.ibb.co/QmTqf2K/default-logo.png" class="tournament-logo" id="tournamentLogo-alt">
      <div class="title" id="tournamentName-alt">Gkec Unity Cup</div>
    </div>
    <div class="date" id="tournamentDate-alt">Group Stage</div>
    <div class="teams">
      <div class="team-panel" id="team1panel-alt">Team 1</div>
      <div class="team-score" id="team1score-alt">0</div>
      <div class="team-score" id="team2score-alt">0</div>
      <div class="team-panel" id="team2panel-alt">Team 2</div>
    </div>
    <div class="matches" id="matches-alt"></div>
    <div class="results-summary">
      <div id="winner-alt">Winner: -</div>
      <div id="motmScorecard-alt">Man of the Match: -</div>
    </div>
  </div>
  <textarea id="pasteText" placeholder="Paste matches here"></textarea><br>
  <button onclick="generateScorecard()">Generate & Archive Scorecard</button>
  <button onclick="downloadScorecard('scorecard')">Download Original Scorecard</button>
  <button onclick="downloadScorecard('scorecard-alt')">Download Alternative Scorecard</button>
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
      <select id="groupSelect">
        <option value="">Select Group</option>
      </select>
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
    </div>
    <hr>
    <h3>Tournament Date/Stage</h3>
    <input type="text" id="tournamentStageInput" placeholder="Enter Date or Stage (e.g., 11 October 2025 or Group Stage)">
    <button onclick="saveTournamentStage()">Save Date/Stage</button>
    <h3>Current Date/Stage</h3>
    <div id="tournamentStageDisplay"></div>
    <hr>
    <h3>Add Tournament Logo</h3>
    <input type="text" id="tournamentNameInput" placeholder="Tournament Name">
    <input type="file" id="tournamentLogoInput" accept="image/*">
    <input type="text" id="tournamentLogoUrl" class="url-input" placeholder="Tournament Logo URL">
    <button onclick="addTournamentLogo()">Add Tournament Logo</button>
    <h3>Saved Tournament Logos</h3>
    <div id="tournamentLogoList"></div>
    <hr>
    <h3>Select Current Tournament</h3>
    <select id="currentTournamentNameSelect" onchange="updateCurrentTournament()">
      <option value="">Select Tournament Name</option>
    </select>
    <select id="currentTournamentLogoSelect" onchange="updateCurrentTournament()">
      <option value="">Select Tournament Logo</option>
    </select>
    <h3>Current Tournament</h3>
    <div id="currentTournamentDisplay"></div>
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
    <hr>
    <h3>Overall Invitation by Date</h3>
    <input type="date" id="overallDate" onchange="displayOverallInvitation()">
    <div id="overallInvitationDisplay"></div>
  </div>
</section>

<!-- Success and Error Message Overlays -->
<div id="successMessage" class="success-message" style="display: none;"></div>
<div id="errorMessage" class="error-message" style="display: none;"></div>

<!-- Firebase SDK -->
<script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-storage-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore-compat.js"></script>
<!-- html2canvas for download -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
const firebaseConfig = {
  apiKey: "AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLtDopPq4",
  authDomain: "llfc-4d2df.firebaseapp.com",
  projectId: "llfc-4d2df",
  storageBucket: "llfc-4d2df.firebasestorage.app",
  messagingSenderId: "697058785471",
  appId: "1:697058785471:web:7481cae8fe6b682d762e0a"
};

let storage, db;
try {
  if (typeof firebase === 'undefined') {
    throw new Error("Firebase SDK not loaded");
  }
  firebase.initializeApp(firebaseConfig);
  storage = firebase.storage();
  db = firebase.firestore();
  console.log("Firebase initialized successfully");
} catch (e) {
  console.error("Firebase initialization failed:", e.message);
  showError("Failed to load Firebase SDK. Check your internet connection or try again later.");
}

let playerPhotoMap = {};
let teamLogoMap = {};
let matchdays = [];
let groups = [];
let squadSubmitLink = "";
let tournamentLogos = [];
let tournamentNames = [];
let currentTournament = { name: "Gkec Unity Cup", logo: "https://i.ibb.co/QmTqf2K/default-logo.png" };
let currentStage = "Group Stage";
let archives = [];
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

async function saveToFirestore(collection, id, data) {
  if (!db) {
    showError("Firestore is not initialized.");
    return false;
  }
  try {
    const sanitizedData = {};
    for (const [key, value] of Object.entries(data)) {
      if (value !== undefined) {
        sanitizedData[key] = value;
      }
    }
    await db.collection(collection).doc(id).set(sanitizedData);
    console.log(`Saved to ${collection}/${id}:`, sanitizedData);
    return true;
  } catch (e) {
    console.error(`Firestore save error for ${collection}/${id}:`, e.message, data);
    showError('Firestore save error: ' + e.message);
    return false;
  }
}

async function getFromFirestore(collection, id) {
  if (!db) {
    showError("Firestore is not initialized.");
    return null;
  }
  try {
    const doc = await db.collection(collection).doc(id).get();
    console.log(`Retrieved from ${collection}/${id}:`, doc.exists ? doc.data() : null);
    return doc.exists ? doc.data() : null;
  } catch (e) {
    console.error(`Firestore retrieve error for ${collection}/${id}:`, e.message);
    showError('Firestore retrieve error: ' + e.message);
    return null;
  }
}

async function deleteFromFirestore(collection, id) {
  if (!db) {
    showError("Firestore is not initialized.");
    return false;
  }
  try {
    await db.collection(collection).doc(id).delete();
    console.log(`Deleted from ${collection}/${id}`);
    return true;
  } catch (e) {
    console.error(`Firestore delete error for ${collection}/${id}:`, e.message);
    showError('Firestore delete error: ' + e.message);
    return false;
  }
}

async function getAllFromFirestore(collection) {
  if (!db) {
    showError("Firestore is not initialized.");
    return [];
  }
  try {
    const snapshot = await db.collection(collection).get();
    const data = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
    console.log(`Retrieved all from ${collection}:`, data);
    return data;
  } catch (e) {
    console.error(`Firestore retrieve all error for ${collection}:`, e.message);
    showError('Firestore retrieve all error: ' + e.message);
    return [];
  }
}

function validateImageUrl(url) {
  return new Promise((resolve) => {
    const img = new Image();
    img.crossOrigin = "Anonymous";
    img.onload = () => {
      console.log(`Image loaded successfully: ${url}`);
      resolve(true);
    };
    img.onerror = () => {
      console.warn(`Image failed to load: ${url}`);
      resolve(false);
    };
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
    console.log(`Uploaded image to Firebase: ${url}`);
    return url;
  } catch (e) {
    console.error("Firebase upload error:", e.message);
    throw new Error("Failed to upload to Firebase: " + e.message);
  }
}

async function ensureImagesLoaded(element) {
  const images = element.querySelectorAll('img');
  const promises = Array.from(images).map(img => {
    return new Promise((resolve) => {
      if (img.complete && img.naturalHeight !== 0) {
        console.log(`Image already loaded: ${img.src}`);
        resolve();
        return;
      }
      img.crossOrigin = "Anonymous";
      img.onload = () => {
        console.log(`Image loaded: ${img.src}`);
        resolve();
      };
      img.onerror = () => {
        console.warn(`Image failed to load, using default: ${img.src}`);
        img.src = defaultLogo;
        resolve();
      };
      img.src = img.src;
    });
  });
  await Promise.all(promises);
  console.log("All images ensured loaded");
}

async function clearStorage() {
  if (confirm('Are you sure you want to clear all saved data (logos, photos, matchdays, groups, archives, tournaments, stage)?')) {
    try {
      await Promise.all([
        db.collection('playerPhotoMap').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('teamLogoMap').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('matchdays').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('groups').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('archives').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('tournamentNames').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('tournamentLogos').get().then(s => s.forEach(d => d.ref.delete())),
        db.collection('config').doc('squadSubmitLink').delete(),
        db.collection('config').doc('currentTournament').delete(),
        db.collection('config').doc('currentStage').delete()
      ]);
      playerPhotoMap = {};
      teamLogoMap = {};
      matchdays = [];
      groups = [];
      squadSubmitLink = "";
      tournamentLogos = [];
      tournamentNames = [];
      currentTournament = { name: "Gkec Unity Cup", logo: defaultLogo };
      currentStage = "Group Stage";
      archives = [];
      updatePlayerList();
      updateTeamList();
      updateMatchdayList();
      updateGroupList();
      updateSquadLinkDisplay();
      updateTournamentLogoList();
      updateTournamentSelects();
      updateCurrentTournamentDisplay();
      updateTournamentStageDisplay();
      updateArchiveList();
      showSuccess("All storage cleared!");
    } catch (e) {
      showError("Failed to clear Firestore: " + e.message);
    }
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

function updateGroupSelect() {
  const groupSelect = document.getElementById("groupSelect");
  groupSelect.innerHTML = '<option value="">Select Group</option>';
  groups.forEach(group => {
    groupSelect.innerHTML += `<option value="${group.name}">${group.name}</option>`;
  });
}

async function addMatchday() {
  const date = document.getElementById("matchdayDate").value;
  let team1 = document.getElementById("team1Select").value || document.getElementById("team1Manual").value.trim();
  let team2 = document.getElementById("team2Select").value || document.getElementById("team2Manual").value.trim();
  const groupName = document.getElementById("groupSelect").value;

  if (!date || !team1 || !team2 || !groupName) {
    showError("Please fill in all fields (date, teams, group).");
    return;
  }

  if (Object.keys(teamLogoMap).length >= 48 && !teamLogoMap[team1]) {
    showError("Maximum 64 teams allowed. Add team via 'Add Team' first.");
    return;
  }

  const matchday = { date, team1, team2, groupName };
  const id = Date.now().toString();
  if (await saveToFirestore('matchdays', id, matchday)) {
    matchdays.push({ id, ...matchday });
    updateMatchdayList();
    document.getElementById("matchdayDate").value = "";
    document.getElementById("team1Select").value = "";
    document.getElementById("team1Manual").value = "";
    document.getElementById("team2Select").value = "";
    document.getElementById("team2Manual").value = "";
    document.getElementById("groupSelect").value = "";
    showSuccess("Matchday added!");
  }
}

function updateMatchdayList() {
  const list = document.getElementById("matchdayList");
  list.innerHTML = "";
  matchdays.forEach((m, index) => {
    list.innerHTML += `
      <div class="admin-matchday">
        ${m.date}: ${m.team1} vs ${m.team2} (Group ${m.groupName})
        <button class="delete-btn" onclick="deleteMatchday(${index})">Delete</button>
      </div>
    `;
  });
  updateOfficialSelect();
}

async function deleteMatchday(index) {
  const matchday = matchdays[index];
  if (await deleteFromFirestore('matchdays', matchday.id)) {
    matchdays.splice(index, 1);
    updateMatchdayList();
    showSuccess("Matchday deleted!");
  }
}

async function addGroup() {
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

  const group = { name, link, officials: [official1, official2] };
  const id = Date.now().toString();
  if (await saveToFirestore('groups', id, group)) {
    groups.push({ id, ...group });
    updateGroupList();
    updateGroupSelect();
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

async function deleteGroup(index) {
  const group = groups[index];
  if (await deleteFromFirestore('groups', group.id)) {
    groups.splice(index, 1);
    updateGroupList();
    updateGroupSelect();
    showSuccess("Group deleted!");
  }
}

async function saveSquadLink() {
  const link = document.getElementById("squadSubmitLink").value.trim();
  if (!link) {
    showError("Please enter a squad submit link.");
    return;
  }
  if (await saveToFirestore('config', 'squadSubmitLink', { link })) {
    squadSubmitLink = link;
    updateSquadLinkDisplay();
    document.getElementById("squadSubmitLink").value = "";
    showSuccess("Squad submit link saved!");
  }
}

function updateSquadLinkDisplay() {
  document.getElementById("squadLinkDisplay").innerHTML = squadSubmitLink ? `<a href="${squadSubmitLink}" target="_blank">${squadSubmitLink}</a>` : "No link set";
}

async function saveTournamentStage() {
  const stage = document.getElementById("tournamentStageInput").value.trim();
  if (!stage) {
    showError("Please enter a date or stage.");
    return;
  }
  if (await saveToFirestore('config', 'currentStage', { stage })) {
    currentStage = stage;
    updateTournamentStageDisplay();
    document.getElementById("tournamentStageInput").value = "";
    document.getElementById("tournamentDate").textContent = currentStage;
    document.getElementById("tournamentDate-alt").textContent = currentStage;
    showSuccess("Tournament date/stage saved!");
  }
}

function updateTournamentStageDisplay() {
  document.getElementById("tournamentStageDisplay").textContent = currentStage || "No date/stage set";
}

async function addTournamentLogo() {
  const name = document.getElementById("tournamentNameInput").value.trim();
  const fileInput = document.getElementById("tournamentLogoInput");
  const urlInput = document.getElementById("tournamentLogoUrl");
  let imageUrl = urlInput.value.trim();
  const file = fileInput.files[0];

  try {
    if (!name) {
      showError("Please enter a tournament name.");
      return;
    }
    if (tournamentNames.length >= 5) {
      showError("Maximum 5 tournament names allowed.");
      return;
    }
    if (tournamentLogos.length >= 5) {
      showError("Maximum 5 tournament logos allowed.");
      return;
    }
    if (file) {
      imageUrl = await uploadToFirebase(file, `images/tournaments/${encodeURIComponent(name)}.jpg`);
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

    if (!tournamentNames.includes(name)) {
      if (await saveToFirestore('tournamentNames', name, { name })) {
        tournamentNames.push(name);
      }
    }
    if (!tournamentLogos.some(t => t.url === imageUrl)) {
      if (await saveToFirestore('tournamentLogos', name, { url: imageUrl })) {
        tournamentLogos.push({ name, url: imageUrl });
      }
    }
    updateTournamentLogoList();
    updateTournamentSelects();
    document.getElementById("tournamentNameInput").value = '';
    document.getElementById("tournamentLogoInput").value = '';
    document.getElementById("tournamentLogoUrl").value = '';
    showSuccess("Tournament logo and name saved!");
  } catch (e) {
    showError("Upload failed: " + e.message);
  }
}

function updateTournamentLogoList() {
  const list = document.getElementById("tournamentLogoList");
  list.innerHTML = "";
  tournamentLogos.forEach((t, index) => {
    list.innerHTML += `
      <div class="admin-tournament">
        <img src="${t.url}" onerror="this.src='${defaultLogo}'" style="width: 40px; height: 40px; border-radius: 50%;">
        ${t.name}
        <button class="delete-btn" onclick="deleteTournamentLogo(${index})">Delete</button>
      </div>
    `;
  });
}

async function deleteTournamentLogo(index) {
  const tournament = tournamentLogos[index];
  try {
    await Promise.all([
      deleteFromFirestore('tournamentNames', tournament.name),
      deleteFromFirestore('tournamentLogos', tournament.name)
    ]);
    tournamentNames = tournamentNames.filter(name => name !== tournament.name);
    tournamentLogos = tournamentLogos.filter(t => t.name !== tournament.name);
    if (currentTournament.name === tournament.name) {
      currentTournament = { name: "Gkec Unity Cup", logo: defaultLogo };
      await saveToFirestore('config', 'currentTournament', currentTournament);
      document.getElementById("tournamentLogo").src = currentTournament.logo;
      document.getElementById("tournamentLogo-alt").src = currentTournament.logo;
      document.getElementById("tournamentName").textContent = currentTournament.name;
      document.getElementById("tournamentName-alt").textContent = currentTournament.name;
    }
    updateTournamentLogoList();
    updateTournamentSelects();
    updateCurrentTournamentDisplay();
    showSuccess("Tournament logo and name deleted!");
  } catch (e) {
    showError("Failed to delete tournament: " + e.message);
  }
}

function updateTournamentSelects() {
  const nameSelect = document.getElementById("currentTournamentNameSelect");
  const logoSelect = document.getElementById("currentTournamentLogoSelect");
  nameSelect.innerHTML = '<option value="">Select Tournament Name</option>';
  logoSelect.innerHTML = '<option value="">Select Tournament Logo</option>';
  tournamentNames.forEach(name => {
    nameSelect.innerHTML += `<option value="${name}">${name}</option>`;
  });
  tournamentLogos.forEach(t => {
    logoSelect.innerHTML += `<option value="${t.url}">${t.name}</option>`;
  });
  nameSelect.value = currentTournament.name;
  logoSelect.value = currentTournament.logo;
}

async function updateCurrentTournament() {
  const name = document.getElementById("currentTournamentNameSelect").value;
  const logo = document.getElementById("currentTournamentLogoSelect").value;
  if (name && logo) {
    currentTournament = { name, logo };
    if (await saveToFirestore('config', 'currentTournament', currentTournament)) {
      document.getElementById("tournamentName").textContent = name;
      document.getElementById("tournamentName-alt").textContent = name;
      document.getElementById("tournamentLogo").src = logo;
      document.getElementById("tournamentLogo-alt").src = logo;
      updateCurrentTournamentDisplay();
      showSuccess("Current tournament updated!");
    }
  } else {
    showError("Please select both a tournament name and logo.");
  }
}

function updateCurrentTournamentDisplay() {
  const display = document.getElementById("currentTournamentDisplay");
  display.innerHTML = `
    <div class="admin-tournament">
      <img src="${currentTournament.logo}" onerror="this.src='${defaultLogo}'" style="width: 40px; height: 40px; border-radius: 50%;">
      ${currentTournament.name}
    </div>
  `;
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

    if (await saveToFirestore('playerPhotoMap', name, { url: imageUrl })) {
      playerPhotoMap[name] = imageUrl;
      updatePlayerList();
      document.getElementById("playerNameInput").value = '';
      document.getElementById("playerPhotoInput").value = '';
      document.getElementById("playerPhotoUrl").value = '';
      showSuccess("Player successfully saved!");
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
    if (Object.keys(teamLogoMap).length >= 48) {
      showError("Maximum 64 teams allowed.");
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

    if (await saveToFirestore('teamLogoMap', name, { url: imageUrl })) {
      teamLogoMap[name] = imageUrl;
      updateTeamList();
      updateTeamSelect();
      document.getElementById("teamNameInput").value = '';
      document.getElementById("teamLogoInput").value = '';
      document.getElementById("teamLogoUrl").value = '';
      showSuccess("Team logo successfully saved!");
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
  return `🔔 LLFC CLUB WORLD CUP Group ${group.name}\n\nDate: ${formatDate(matchday.date)}\n\n🔴 ${matchday.team1}\n🔵 ${matchday.team2}\n\n📌 PLEASE JOIN YOUR MATCHDAY GROUP\n${group.link}\n\n✅ Squad Submit Link\n${squadSubmitLink}\n⚠️ PLEASE SUBMIT YOUR SQUAD BEFORE 5:00 PM\n🏅 Officials: ${group.officials.join(", ")}`;
}

function displayInvitation() {
  const official = document.getElementById("officialSelect").value;
  const display = document.getElementById("invitationDisplay");
  display.innerHTML = "";
  if (!official) return;

  const officialGroups = groups.filter(g => g.officials.includes(official));
  officialGroups.forEach(group => {
    const groupMatchdays = matchdays.filter(m => m.groupName === group.name);
    groupMatchdays.forEach(matchday => {
      const text = generateInvitationText(matchday, group);
      const div = document.createElement("div");
      div.innerHTML = `
        <h3>Group ${group.name} - ${matchday.date}</h3>
        <div class="invitation-text"></div>
        <button onclick="copyText(\`${text.replace(/`/g, "\\`")}\`)">Copy Text</button>
      `;
      div.querySelector(".invitation-text").textContent = text;
      display.appendChild(div);
    });
  });
}

function displayOverallInvitation() {
  const selectedDate = document.getElementById("overallDate").value;
  const display = document.getElementById("overallInvitationDisplay");
  display.innerHTML = "";
  if (!selectedDate) return;

  const dateMatchdays = matchdays.filter(m => m.date === selectedDate);
  if (dateMatchdays.length === 0) {
    display.innerHTML = "<p>No matchdays on this date.</p>";
    return;
  }

  let combinedText = "";
  dateMatchdays.forEach(matchday => {
    const group = groups.find(g => g.name === matchday.groupName);
    if (group) {
      const text = generateInvitationText(matchday, group);
      combinedText += text + "\n\n---\n\n";
    }
  });

  if (combinedText) {
    const div = document.createElement("div");
    div.innerHTML = `
      <h3>All Matchdays on ${formatDate(selectedDate)}</h3>
      <div class="invitation-text"></div>
      <button onclick="copyText(\`${combinedText.replace(/`/g, "\\`")}\`)">Copy All Text</button>
    `;
    div.querySelector(".invitation-text").textContent = combinedText;
    display.appendChild(div);
  } else {
    display.innerHTML = "<p>No groups found for matchdays on this date.</p>";
  }
}

function copyText(text) {
  navigator.clipboard.writeText(text).then(() => {
    showSuccess("Invitation text copied!");
  }).catch(err => {
    console.error("Clipboard error:", err);
    showError("Failed to copy text. Try again or check browser permissions.");
  });
}

function cleanName(name) {
  if (!name) return "";
  return name.replace(/[👑🔑@]/g, '').trim();
}

async function saveToArchive(team1, team2, team1Points, team2Points, matches, motmPlayer) {
  const archive = {
    id: Date.now().toString(),
    timestamp: new Date().toISOString(),
    team1: team1 || "Unknown Team 1",
    team2: team2 || "Unknown Team 2",
    team1Points: parseInt(team1Points) || 0,
    team2Points: parseInt(team2Points) || 0,
    matches: matches || [],
    motmPlayer: motmPlayer || "",
    inputText: document.getElementById("pasteText").value || "",
    tournamentName: currentTournament.name,
    tournamentLogo: currentTournament.logo,
    stage: currentStage
  };
  try {
    if (await saveToFirestore('archives', archive.id, archive)) {
      archives.push(archive);
      updateArchiveList();
      showSuccess("Scorecard archived!");
      console.log("Archive saved:", archive);
    }
  } catch (e) {
    console.error("Archive save failed:", e);
    showError("Failed to archive scorecard: " + e.message);
  }
}

function updateArchiveList() {
  const list = document.getElementById("archiveList");
  list.innerHTML = archives.length ? "" : "<p>No archives available.</p>";
  archives.forEach((archive, index) => {
    const timestamp = new Date(archive.timestamp).toLocaleString('en-GB', { 
      day: '2-digit', month: 'short', year: 'numeric', hour: '2-digit', minute: '2-digit' 
    });
    list.innerHTML += `
      <div class="admin-archive">
        ${timestamp}: ${archive.team1} vs ${archive.team2} (${archive.team1Points}-${archive.team2Points})
        <button onclick="loadArchive(${index})">Load</button>
        <button onclick="editArchive(${index})">Edit</button>
        <button class="delete-btn" onclick="deleteArchive(${index})">Delete</button>
      </div>
    `;
  });
  console.log("Updated archive list with", archives.length, "archives");
}

function loadArchive(index) {
  const archive = archives[index];
  document.getElementById("pasteText").value = archive.inputText;
  document.getElementById("tournamentName").textContent = archive.tournamentName;
  document.getElementById("tournamentName-alt").textContent = archive.tournamentName;
  document.getElementById("tournamentLogo").src = archive.tournamentLogo;
  document.getElementById("tournamentLogo-alt").src = archive.tournamentLogo;
  document.getElementById("tournamentDate").textContent = archive.stage;
  document.getElementById("tournamentDate-alt").textContent = archive.stage;
  generateScorecard();
  showSuccess("Archive loaded!");
}

async function editArchive(index) {
  const newText = prompt("Edit scorecard text:", archives[index].inputText);
  if (newText) {
    archives[index].inputText = newText;
    if (await saveToFirestore('archives', archives[index].id, archives[index])) {
      updateArchiveList();
      showSuccess("Archive updated!");
    }
  }
}

async function deleteArchive(index) {
  const archive = archives[index];
  if (await deleteFromFirestore('archives', archive.id)) {
    archives.splice(index, 1);
    updateArchiveList();
    showSuccess("Archive deleted!");
  }
}

async function generateScorecard() {
  const text = document.getElementById("pasteText").value.trim();
  if (!text) {
    showError("Please paste match data.");
    return;
  }

  const lines = text.split('\n').map(line => line.trim()).filter(line => line);
  if (lines.length < 1) {
    showError("No valid input provided.");
    return;
  }

  // Extract team names from the first line containing ⚒️, 🆚, or |
  let team1 = "", team2 = "";
  let teamLineFound = false;
  for (const line of lines) {
    if (line.includes('⚒️') || line.includes('🆚') || line.includes('|')) {
      const separator = line.includes('⚒️') ? '⚒️' : line.includes('🆚') ? '🆚' : '|';
      const teams = line.split(separator).map(t => t.trim());
      if (teams.length >= 2) {
        team1 = teams[0].replace(/🅻🅻🅵🅲/, 'LLFC').trim(); // Normalize team names
        team2 = teams[1].replace(/🅲🅿︎🅲/, 'CPC').trim();
        teamLineFound = true;
        break;
      }
    }
  }

  if (!teamLineFound || !team1 || !team2) {
    showError("Could not find valid team names separated by ⚒️, 🆚, or |.");
    return;
  }

  // Parse match lines
  const matchRegex = /(.+?)\s*\(?(\d+)\)?\s*🆚\s*\(?(\d+)\)?\s*(.+)/;
  const matches = [];
  let motmPlayer = "";
  for (const line of lines) {
    const match = line.match(matchRegex);
    if (match) {
      const [, p1, s1, s2, p2] = match;
      matches.push([p1.trim(), s1, s2, p2.trim()]);
      if (p1.includes('👑')) motmPlayer = cleanName(p1);
      else if (p2.includes('👑')) motmPlayer = cleanName(p2);
    }
  }

  if (matches.length === 0) {
    showError("No valid matches found. Use format 'Player1 X🆚Y Player2'.");
    return;
  }

  if (!motmPlayer) {
    showError("No Man of the Match (👑) specified in any match.");
    return;
  }

  // Calculate team points based on match outcomes
  let team1Points = 0, team2Points = 0;
  matches.forEach(([p1, s1, s2, p2]) => {
    const score1 = parseInt(s1);
    const score2 = parseInt(s2);
    if (score1 > score2) {
      team1Points += 3; // Team 1 wins
    } else if (score2 > score1) {
      team2Points += 3; // Team 2 wins
    } else {
      team1Points += 1; // Draw
      team2Points += 1;
    }
  });

  const team1Logo = teamLogoMap[team1] || defaultLogo;
  const team2Logo = teamLogoMap[team2] || defaultLogo;

  // Update Original Scorecard
  document.getElementById("team1panel").innerHTML = `<img src="${team1Logo}" class="team-logo" onerror="this.src='${defaultLogo}'">${team1}`;
  document.getElementById("team2panel").innerHTML = `<img src="${team2Logo}" class="team-logo" onerror="this.src='${defaultLogo}'">${team2}`;
  document.getElementById("team1score").textContent = team1Points;
  document.getElementById("team2score").textContent = team2Points;
  document.getElementById("tournamentName").textContent = currentTournament.name;
  document.getElementById("tournamentLogo").src = currentTournament.logo;
  document.getElementById("tournamentDate").textContent = currentStage;

  // Update Alternative Scorecard
  document.getElementById("team1panel-alt").innerHTML = `<img src="${team1Logo}" class="team-logo" onerror="this.src='${defaultLogo}'">${team1}`;
  document.getElementById("team2panel-alt").innerHTML = `<img src="${team2Logo}" class="team-logo" onerror="this.src='${defaultLogo}'">${team2}`;
  document.getElementById("team1score-alt").textContent = team1Points;
  document.getElementById("team2score-alt").textContent = team2Points;
  document.getElementById("tournamentName-alt").textContent = currentTournament.name;
  document.getElementById("tournamentLogo-alt").src = currentTournament.logo;
  document.getElementById("tournamentDate-alt").textContent = currentStage;

  // Generate match rows
  const matchesDiv = document.getElementById("matches");
  const matchesDivAlt = document.getElementById("matches-alt");
  matchesDiv.innerHTML = "";
  matchesDivAlt.innerHTML = "";
  matches.forEach(([p1, s1, s2, p2]) => {
    const cleanP1 = cleanName(p1);
    const cleanP2 = cleanName(p2);
    const isMotmP1 = p1.includes("👑");
    const isMotmP2 = p2.includes("👑");
    const player1Class = isMotmP1 ? "motm-player" : "";
    const player2Class = isMotmP2 ? "motm-player" : "";
    matchesDiv.innerHTML += `
      <div class="match-row">
        <div class="player-container ${player1Class}">
          <span class="player-left">${cleanP1}</span>
        </div>
        <div class="score-box">${s1} - ${s2}</div>
        <div class="player-container ${player2Class}">
          <span class="player-right">${cleanP2}</span>
        </div>
      </div>
    `;
    matchesDivAlt.innerHTML += `
      <div class="match-row">
        <div class="player-container ${player1Class}">
          <span class="player-left">${cleanP1}</span>
        </div>
        <div class="score-box">${s1} - ${s2}</div>
        <div class="player-container ${player2Class}">
          <span class="player-right">${cleanP2}</span>
        </div>
      </div>
    `;
  });

  // Update winner and MOTM
  const winnerText = team1Points > team2Points ? `${team1} wins!` : team2Points > team1Points ? `${team2} wins!` : "Draw!";
  document.getElementById("winner").textContent = `Winner: ${winnerText}`;
  document.getElementById("winner-alt").textContent = `Winner: ${winnerText}`;
  document.getElementById("motmScorecard").textContent = `Man of the Match: ${motmPlayer}`;
  document.getElementById("motmScorecard-alt").textContent = `Man of the Match: ${motmPlayer}`;

  await saveToArchive(team1, team2, team1Points, team2Points, matches, motmPlayer);
  showSuccess("Scorecard generated and archived!");
}

async function downloadScorecard(scorecardId) {
  const scorecard = document.getElementById(scorecardId);
  await ensureImagesLoaded(scorecard);
  try {
    const canvas = await html2canvas(scorecard, {
      backgroundColor: scorecardId === 'scorecard' ? '#2c2c2c' : '#ffffff',
      scale: 2,
      useCORS: true
    });
    const link = document.createElement('a');
    link.href = canvas.toDataURL('image/png');
    link.download = `llfc_scorecard_${new Date().toISOString().split('T')[0]}_${scorecardId === 'scorecard' ? 'dark' : 'light'}.png`;
    link.click();
    showSuccess(`${scorecardId === 'scorecard' ? 'Original' : 'Alternative'} scorecard downloaded!`);
  } catch (e) {
    console.error("Download error:", e);
    showError("Failed to download scorecard: " + e.message);
  }
}

function openTab(tabId, button) {
  document.querySelectorAll('section').forEach(section => {
    section.classList.remove('active');
  });
  document.getElementById(tabId).classList.add('active');
  document.querySelectorAll('.tab-btn').forEach(btn => {
    btn.classList.remove('active');
  });
  button.classList.add('active');
}

async function initializeData() {
  try {
    const [playerPhotos, teams, matchdaysData, groupsData, archivesData, configSquad, configTournament, configStage, tournamentNamesData, tournamentLogosData] = await Promise.all([
      getAllFromFirestore('playerPhotoMap'),
      getAllFromFirestore('teamLogoMap'),
      getAllFromFirestore('matchdays'),
      getAllFromFirestore('groups'),
      getAllFromFirestore('archives'),
      getFromFirestore('config', 'squadSubmitLink'),
      getFromFirestore('config', 'currentTournament'),
      getFromFirestore('config', 'currentStage'),
      getAllFromFirestore('tournamentNames'),
      getAllFromFirestore('tournamentLogos')
    ]);

    playerPhotoMap = playerPhotos.reduce((acc, p) => ({ ...acc, [p.id]: p.url }), {});
    teamLogoMap = teams.reduce((acc, t) => ({ ...acc, [t.id]: t.url }), {});
    matchdays = matchdaysData;
    groups = groupsData;
    archives = archivesData;
    squadSubmitLink = configSquad ? configSquad.link : "";
    currentTournament = configTournament || { name: "Gkec Unity Cup", logo: defaultLogo };
    currentStage = configStage ? configStage.stage : "Group Stage";
    tournamentNames = tournamentNamesData.map(t => t.name);
    tournamentLogos = tournamentLogosData.map(t => ({ name: t.id, url: t.url }));

    document.getElementById("tournamentLogo").src = currentTournament.logo;
    document.getElementById("tournamentLogo-alt").src = currentTournament.logo;
    document.getElementById("tournamentName").textContent = currentTournament.name;
    document.getElementById("tournamentName-alt").textContent = currentTournament.name;
    document.getElementById("tournamentDate").textContent = currentStage;
    document.getElementById("tournamentDate-alt").textContent = currentStage;
    updateTournamentLogoList();
    updateTournamentSelects();
    updateCurrentTournamentDisplay();
    updateTournamentStageDisplay();
    updatePlayerList();
    updateTeamList();
    updateMatchdayList();
    updateGroupList();
    updateSquadLinkDisplay();
    updateArchiveList();
    console.log("Initialization complete");
  } catch (e) {
    console.error("Initialization error:", e.message);
    showError("Failed to initialize data: " + e.message);
  }
}

// Initialize on page load
document.addEventListener('DOMContentLoaded', () => {
  initializeData();
});

// Handle Enter key for password input
document.getElementById("adminPassword").addEventListener("keypress", (e) => {
  if (e.key === "Enter") {
    unlockMatchdaySetup();
  }
});
</script>
</body>
</html>
