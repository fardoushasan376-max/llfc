
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>LLFC Scorecard & Rankings</title>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js"></script>
<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
<style>
body { font-family: Arial, sans-serif; background: #f4f4f4; padding: 20px; }
h1,h2 { text-align: center; color: #333; }
textarea { width: 100%; height: 150px; margin-bottom: 10px; font-family: monospace; }
button, select { padding: 8px 16px; font-size: 14px; cursor: pointer; margin: 5px 0; }
table { width: 100%; border-collapse: collapse; margin-bottom: 20px; background: #fff; }
th, td { border: 1px solid #ccc; padding: 5px; text-align: center; }
th { background: #333; color: #fff; }
input[type="number"], input[type="text"], input[type="date"] { width: 80px; }
input[type="file"] { width: 100px; }
.archive-item { background: #fff; padding: 5px; margin-bottom: 5px; border:1px solid #ccc; }
.rank-1 { border: 2px solid gold; background: #fff7e6; }
.rank-2 { border: 2px solid silver; background: #f0f0f0; }
.rank-3 { border: 2px solid #cd7f32; background: #f9f0e6; }
.medal { font-size: 18px; margin-right:5px; }
img.player-photo { width:50px; height:50px; object-fit:cover; border-radius:5px;}
</style>
</head>
<body>

<h1>LLFC Scorecard Management</h1>

<h2>1. Paste Scorecard</h2>
<textarea id="scorecardText" placeholder="Paste scorecard text here..."></textarea><br>
<button onclick="previewScorecard()">Preview Scorecard</button>

<h2>2. Preview Table (Editable)</h2>
<div id="previewContainer"></div>
<label>Submission Date: <input type="date" id="submissionDate"></label><br>
<button onclick="submitScorecard()">Submit Scorecard</button>

<h2>3. Scorecard Archive</h2>
<div id="archiveContainer"></div>

<h2>4. Rankings (All LLFC Players)</h2>
<label>Filter: 
<select id="rankingType" onchange="displayRanking()">
<option value="overall">Overall</option>
<option value="weekly">Weekly</option>
<option value="monthly">Monthly</option>
</select>
</label>
<table id="rankingTable">
<thead>
<tr>
<th>Photo</th>
<th>Player Name</th>
<th>Matches</th>
<th>Win</th>
<th>Draw</th>
<th>Loss</th>
<th>GS</th>
<th>GC</th>
<th>GD</th>
<th>MOTM</th>
<th>Avg Rating</th>
<th>Upload Photo</th>
</tr>
</thead>
<tbody></tbody>
</table>

<h2>5. Download Rankings Card</h2>
<label>Range:
<select id="downloadRange">
<option value="1-10">1-10</option>
<option value="11-20">11-20</option>
<option value="21-30">21-30</option>
</select>
</label>
<button onclick="downloadRankingCard()">Download as Card</button>
<div id="rankingCard" style="padding:10px; background:#fff;"></div>

<script>
// ------------------ Firebase Setup ------------------
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

// ------------------ Variables ------------------
const LLFCTeams = ["DREADLORDS OF LLFC","Luminous Legends EFootball Club"];
let previewPlayers = [];
let currentScorecardID = null;

// ------------------ Parse Scorecard ------------------
function parseScorecard(text){
    const lines = text.split(/\r?\n/).filter(l=>l.trim());
    let players = {};
    lines.forEach(line=>{
        LLFCTeams.forEach(team=>{
            if(line.includes(team)){
                const regex = /(.*?)\s*(\d+)\s*🆚\s*(\d+)\s*(.*)/;
                const match = line.match(regex);
                if(match){
                    const leftPlayers = match[1].split(/@|\s{2,}/).map(p=>p.replace(/🔑/g,"").trim()).filter(Boolean);
                    const rightPlayers = match[4].split(/@|\s{2,}/).map(p=>p.replace(/🔑/g,"").trim()).filter(Boolean);
                    const llfcSide = match[1].includes(team) ? leftPlayers : rightPlayers;
                    const llfcGoals = match[1].includes(team) ? parseInt(match[2]) : parseInt(match[3]);
                    const oppGoals = match[1].includes(team) ? parseInt(match[3]) : parseInt(match[2]);
                    llfcSide.forEach(p=>{
                        if(!players[p]){
                            players[p] = {player:p, matches:1, win:llfcGoals>oppGoals?1:0, draw:llfcGoals===oppGoals?1:0, loss:llfcGoals<oppGoals?1:0, gs:llfcGoals, gc:oppGoals, gd:llfcGoals-oppGoals, motm:line.includes("⚽")?1:0, rating:0, photo:""};
                        } else {
                            let obj = players[p];
                            obj.matches +=1;
                            obj.win += llfcGoals>oppGoals?1:0;
                            obj.draw += llfcGoals===oppGoals?1:0;
                            obj.loss += llfcGoals<oppGoals?1:0;
                            obj.gs += llfcGoals;
                            obj.gc += oppGoals;
                            obj.gd = obj.gs - obj.gc;
                            obj.motm += line.includes("⚽")?1:0;
                        }
                    });
                }
            }
        });
    });
    return Object.values(players);
}

// ------------------ Preview Table ------------------
function previewScorecard(){
    const text = document.getElementById("scorecardText").value;
    if(!text){ alert("Paste a scorecard!"); return; }
    previewPlayers = parseScorecard(text);
    if(previewPlayers.length===0){ alert("No LLFC players found!"); return; }
    currentScorecardID = Date.now();
    renderPreviewTable();
}

function renderPreviewTable(){
    let html = `<table><thead>
    <tr>
    <th>Player Name</th>
    <th>Matches</th>
    <th>Win</th>
    <th>Draw</th>
    <th>Loss</th>
    <th>GS</th>
    <th>GC</th>
    <th>GD</th>
    <th>MOTM</th>
    <th>Rating</th>
    </tr></thead><tbody>`;
    previewPlayers.forEach(p=>{
        html += `<tr>
            <td contenteditable="true">${p.player}</td>
            <td><input type="number" value="${p.matches}"></td>
            <td><input type="number" value="${p.win}"></td>
            <td><input type="number" value="${p.draw}"></td>
            <td><input type="number" value="${p.loss}"></td>
            <td><input type="number" value="${p.gs}"></td>
            <td><input type="number" value="${p.gc}"></td>
            <td><input type="number" value="${p.gd}"></td>
            <td><input type="number" value="${p.motm}"></td>
            <td><input type="number" value="${p.rating.toFixed(2)}"></td>
        </tr>`;
    });
    html += `</tbody></table>`;
    document.getElementById("previewContainer").innerHTML = html;
}

// ------------------ Submit Scorecard ------------------
async function submitScorecard(){
    const subDate = document.getElementById("submissionDate").value;
    if(!subDate){ alert("Select submission date!"); return; }

    const table = document.querySelector("#previewContainer table tbody");
    previewPlayers.forEach((p,i)=>{
        let row = table.rows[i];
        p.player = row.cells[0].innerText.trim();
        p.matches = parseInt(row.cells[1].children[0].value)||0;
        p.win = parseInt(row.cells[2].children[0].value)||0;
        p.draw = parseInt(row.cells[3].children[0].value)||0;
        p.loss = parseInt(row.cells[4].children[0].value)||0;
        p.gs = parseInt(row.cells[5].children[0].value)||0;
        p.gc = parseInt(row.cells[6].children[0].value)||0;
        p.gd = parseInt(row.cells[7].children[0].value)||0;
        p.motm = parseInt(row.cells[8].children[0].value)||0;

        let points = p.win*7 + p.draw*5 + p.loss*-5 + p.gd*0.3 + p.motm*1;
        p.rating = p.matches ? points / p.matches : 0;
    });

    await db.collection("scorecards").doc(String(currentScorecardID)).set({
        id: currentScorecardID,
        date: subDate,
        players: previewPlayers
    });

    alert("✅ Scorecard submitted to Firebase!");
    previewPlayers = [];
    currentScorecardID = null;
    document.getElementById("previewContainer").innerHTML = "";
    document.getElementById("scorecardText").value = "";
    displayArchive();
    displayRanking();
}

// ------------------ Display Archive ------------------
async function displayArchive(){
    const snapshot = await db.collection("scorecards").get();
    const container = document.getElementById("archiveContainer");
    container.innerHTML = "";
    snapshot.forEach(doc=>{
        let data = doc.data();
        let div = document.createElement("div");
        div.className = "archive-item";
        div.innerHTML = `${data.date} 
        <button onclick="loadArchive(${data.id})">Load</button>
        <button onclick="deleteArchive(${data.id})">Delete</button>`;
        container.appendChild(div);
    });
}

async function loadArchive(id){
    const docSnap = await db.collection("scorecards").doc(String(id)).get();
    if(!docSnap.exists) return;
    let item = docSnap.data();
    previewPlayers = item.players.map(p=>({...p}));
    currentScorecardID = id;
    renderPreviewTable();
}

async function deleteArchive(id){
    if(!confirm("Delete this scorecard?")) return;
    await db.collection("scorecards").doc(String(id)).delete();
    displayArchive();
    displayRanking();
}

// ------------------ Display Rankings ------------------
async function displayRanking(){
    const type = document.getElementById("rankingType").value;
    const tbody = document.getElementById("rankingTable").querySelector("tbody");
    tbody.innerHTML = "";

    const snapshot = await db.collection("scorecards").get();
    let stats = {};
    let now = new Date();

    snapshot.forEach(doc=>{
        let card = doc.data();
        let cardDate = new Date(card.date);
        let include = false;
        if(type==='overall') include = true;
        else if(type==='monthly') include = cardDate.getMonth()===now.getMonth() && cardDate.getFullYear()===now.getFullYear();
        else if(type==='weekly'){
            const weekStart = new Date(now);
            weekStart.setDate(now.getDate()-now.getDay());
            const weekEnd = new Date(weekStart);
            weekEnd.setDate(weekStart.getDate()+6);
            include = cardDate >= weekStart && cardDate <= weekEnd;
        }

        if(include){
            card.players.forEach(p=>{
                if(!stats[p.player]){
                    stats[p.player] = {...p};
                } else {
                    stats[p.player].matches += p.matches;
                    stats[p.player].win += p.win;
                    stats[p.player].draw += p.draw;
                    stats[p.player].loss += p.loss;
                    stats[p.player].gs += p.gs;
                    stats[p.player].gc += p.gc;
                    stats[p.player].gd += p.gd;
                    stats[p.player].motm += p.motm;
                }
                let totalPoints = stats[p.player].win*7 + stats[p.player].draw*5 + stats[p.player].loss*-5 + stats[p.player].gd*0.3 + stats[p.player].motm*1;
                stats[p.player].rating = stats[p.player].matches ? totalPoints/stats[p.player].matches : 0;
            });
        }
    });

    let playersArr = Object.values(stats);
    playersArr.sort((a,b)=>b.rating - a.rating);

    playersArr.forEach((p,i)=>{
        let cls = "";
        let medal = "";
        if(i===0){ cls="rank-1"; medal="🥇"; }
        else if(i===1){ cls="rank-2"; medal="🥈"; }
        else if(i===2){ cls="rank-3"; medal="🥉"; }
        tbody.innerHTML += `<tr class="${cls}">
            <td><img src="${p.photo||''}" class="player-photo"></td>
            <td>${medal}${p.player}</td>
            <td>${p.matches}</td>
            <td>${p.win}</td>
            <td>${p.draw}</td>
            <td>${p.loss}</td>
            <td>${p.gs}</td>
            <td>${p.gc}</td>
            <td>${p.gd}</td>
            <td>${p.motm}</td>
            <td>${p.rating.toFixed(2)}</td>
            <td><input type="file" onchange="uploadPhoto(event,'${p.player}')"></td>
        </tr>`;
    });
}

// ------------------ Upload Player Photo ------------------
async function uploadPhoto(e,player){
    const file = e.target.files[0];
    if(!file) return;
    const reader = new FileReader();
    reader.onload = async function(ev){
        const snapshot = await db.collection("scorecards").get();
        snapshot.forEach(async doc=>{
            let data = doc.data();
            data.players.forEach(p=>{
                if(p.player===player){ p.photo = ev.target.result; }
            });
            await db.collection("scorecards").doc(doc.id).set(data);
        });
        displayRanking();
    };
    reader.readAsDataURL(file);
}

// ------------------ Download Ranking Card ------------------
function downloadRankingCard(){
    const type = document.getElementById("rankingType").value;
    const rangeVal = document.getElementById("downloadRange").value.split("-").map(Number);
    const tbody = document.getElementById("rankingTable").querySelector("tbody");

    let html = `<table style="border-collapse:collapse;"><thead>${document.querySelector("#rankingTable thead").innerHTML}</thead><tbody>`;
    for(let i=rangeVal[0]-1;i<rangeVal[1] && i<tbody.rows.length;i++){
        html += `<tr>${tbody.rows[i].innerHTML}</tr>`;
    }
    html += `</tbody></table>`;
    const div = document.getElementById("rankingCard");
    div.innerHTML = html;

    html2canvas(div).then(canvas=>{
        const link = document.createElement("a");
        link.download = `LLFC_Ranking_${type}_${rangeVal[0]}-${rangeVal[1]}.png`;
        link.href = canvas.toDataURL();
        link.click();
    });
}

// ------------------ Initialize ------------------
displayArchive();
displayRanking();
</script>

</body>
</html>
