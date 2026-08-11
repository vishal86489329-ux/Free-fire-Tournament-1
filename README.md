# Free-fire-Tournament-1

html = r'''<!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Free Fire Tournament Registration</title>
<style>
*{box-sizing:border-box}body{margin:0;font-family:Arial,sans-serif;background:#080d1b;color:#fff}
.wrap{max-width:900px;margin:auto;padding:18px}.hero{text-align:center;padding:25px 5px}
h1{font-size:32px;margin:5px}.hero p{color:#aeb9d4}.card{background:#121a2d;border:1px solid #2b3858;border-radius:18px;padding:20px;margin:16px 0}
h2{margin-top:0}.fee{padding:13px;background:#0d2630;border-radius:10px;margin-bottom:18px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}label{display:block;margin:12px 0 6px;font-weight:bold}
input,select{width:100%;padding:13px;border-radius:10px;border:1px solid #3a4766;background:#0a1122;color:white;font-size:15px}
button{border:0;border-radius:10px;padding:13px 18px;margin-top:18px;font-weight:bold;cursor:pointer;background:#16d39a;color:#03130d}
button.alt{background:#34415f;color:#fff}.msg{padding:12px;border-radius:10px;margin-top:15px;background:#102c38}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}.stat{background:#0b1224;padding:14px;border-radius:12px}.stat b{display:block;font-size:24px;margin-top:5px}
.team{padding:13px;border:1px solid #303d5d;border-radius:12px;margin-top:10px;background:#0e1629}.paid{color:#55efaa}.pending{color:#ffd166}
.small{font-size:13px;color:#aeb9d4}.hidden{display:none}@media(max-width:650px){.grid,.stats{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="wrap">
<div class="hero">
<h1>🔥 FREE FIRE TOURNAMENT</h1>
<p>Official Team Registration Portal</p>
</div>

<div class="card">
<h2>Team Registration</h2>
<div class="fee">Entry Fee: <b>₹200 per team (4 players)</b></div>

<form id="registrationForm">
<label>Team Name</label>
<input id="teamName" required placeholder="Enter team name">

<div class="grid">
<div><label>Captain Name</label><input id="captainName" required></div>
<div><label>Mobile / WhatsApp</label><input id="mobile" required inputmode="tel"></div>
</div>

<h3>Player UID</h3>
<div class="grid">
<div><label>Player 1 UID</label><input id="p1" required></div>
<div><label>Player 2 UID</label><input id="p2" required></div>
<div><label>Player 3 UID</label><input id="p3" required></div>
<div><label>Player 4 UID</label><input id="p4" required></div>
</div>

<label>Payment Status</label>
<select id="paymentStatus">
<option value="Pending">Pending</option>
<option value="Paid">Paid</option>
</select>

<label>Transaction ID / UTR</label>
<input id="transactionId" placeholder="Enter transaction ID if paid">

<button type="submit">Submit Registration</button>
</form>
<div id="success" class="msg hidden"></div>
</div>

<div class="card">
<h2>Admin Dashboard — Demo</h2>
<p class="small">This demo stores data in this browser. For a shared online dashboard, connect Supabase using the configuration section in the code.</p>
<div class="stats">
<div class="stat">Teams<b id="teamCount">0</b></div>
<div class="stat">Paid Teams<b id="paidCount">0</b></div>
<div class="stat">Collected<b id="totalAmount">₹0</b></div>
</div>
<button class="alt" onclick="renderTeams()">Refresh</button>
<button class="alt" onclick="exportCSV()">Export CSV</button>
<div id="teamList"></div>
</div>
</div>

<script>
// ============================================================
// SUPABASE SETUP
// Put your Supabase Project URL and Publishable key here.
// Do NOT put a service-role/secret key in this file.
// ============================================================
const SUPABASE_URL = "YOUR_SUPABASE_PROJECT_URL";
const SUPABASE_PUBLISHABLE_KEY = "YOUR_SUPABASE_PUBLISHABLE_KEY";

// Current demo storage:
const STORAGE_KEY = "ff_tournament_registrations";

function readData(){
  try{return JSON.parse(localStorage.getItem(STORAGE_KEY)||"[]")}catch(e){return[]}
}
function writeData(data){localStorage.setItem(STORAGE_KEY,JSON.stringify(data))}

function escapeHTML(value){
  return String(value).replace(/[&<>"']/g,c=>({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
  }[c]));
}

registrationForm.addEventListener("submit",function(e){
  e.preventDefault();

  const data=readData();
  const number="FF-"+String(data.length+1).padStart(4,"0");

  const item={
    registration_no:number,
    team_name:teamName.value.trim(),
    captain_name:captainName.value.trim(),
    mobile:mobile.value.trim(),
    player1_uid:p1.value.trim(),
    player2_uid:p2.value.trim(),
    player3_uid:p3.value.trim(),
    player4_uid:p4.value.trim(),
    payment_status:paymentStatus.value,
    transaction_id:transactionId.value.trim(),
    created_at:new Date().toLocaleString("en-IN")
  };

  data.push(item);
  writeData(data);
  updateStats();

  success.innerHTML="✅ Registration successful!<br>Registration No: <b>"+number+"</b>";
  success.classList.remove("hidden");

  registrationForm.reset();
  renderTeams();
});

function updateStats(){
  const data=readData();
  const paid=data.filter(x=>x.payment_status==="Paid");
  teamCount.textContent=data.length;
  paidCount.textContent=paid.length;
  totalAmount.textContent="₹"+(paid.length*200);
}

function renderTeams(){
  const data=readData();

  if(!data.length){
    teamList.innerHTML='<p class="small">No registrations yet.</p>';
    updateStats();
    return;
  }

  teamList.innerHTML=data.map(x=>`
    <div class="team">
      <b>${escapeHTML(x.registration_no)} — ${escapeHTML(x.team_name)}</b><br>
      Captain: ${escapeHTML(x.captain_name)}<br>
      Mobile: ${escapeHTML(x.mobile)}<br>
      Players: ${escapeHTML(x.player1_uid)} • ${escapeHTML(x.player2_uid)} •
      ${escapeHTML(x.player3_uid)} • ${escapeHTML(x.player4_uid)}<br>
      Payment:
      <b class="${x.payment_status==="Paid"?"paid":"pending"}">
        ${escapeHTML(x.payment_status)}
      </b>
      ${x.transaction_id?" | Transaction: "+escapeHTML(x.transaction_id):""}
      <br><span class="small">${escapeHTML(x.created_at)}</span>
    </div>
  `).join("");

  updateStats();
}

function exportCSV(){
  const data=readData();
  if(!data.length){alert("No registrations found.");return}

  const header=[
    "Registration No","Team Name","Captain","Mobile",
    "Player 1 UID","Player 2 UID","Player 3 UID","Player 4 UID",
    "Payment Status","Transaction ID","Created At"
  ];

  const rows=data.map(x=>[
    x.registration_no,x.team_name,x.captain_name,x.mobile,
    x.player1_uid,x.player2_uid,x.player3_uid,x.player4_uid,
    x.payment_status,x.transaction_id,x.created_at
  ]);

  const csv=[header,...rows]
    .map(row=>row.map(v=>'"'+String(v).replace(/"/g,'""')+'"').join(","))
    .join("\n");

  const blob=new Blob([csv],{type:"text/csv;charset=utf-8"});
  const a=document.createElement("a");
  a.href=URL.createObjectURL(blob);
  a.download="free_fire_registrations.csv";
  a.click();
}

renderTeams();
</script>
</body>
</html>
'''

(root/"index.html").write_text(html,encoding="utf-8")

readme = """FREE FIRE TOURNAMENT WEBSITE

1. Open index.html in a browser to test the form.
2. The current demo stores registrations in the browser.
3. To make registrations shared between different phones, create a Supabase project.
4. Put ONLY the Supabase Project URL and Publishable key into index.html.
5. Do not put a Supabase service-role/secret key in browser code.
6. The Supabase database table and secure admin authentication still need to be configured before using this as a public tournament system.
"""
(root/"README.txt").write_text(readme,encoding="utf-8")

zipfile_path=Path("/mnt/data/free_fire_tournament_complete_html.zip")
with zipfile.ZipFile(zipfile_path,"w",zipfile.ZIP_DEFLATED) as z:
    z.write(root/"index.html","index.html")
    z.write(root/"README.txt","README.txt")

print(f"[Download complete HTML website](sandbox:{zipfile_path})")
