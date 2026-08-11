<!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Free Fire Tournament Registration</title>

<style>
*{box-sizing:border-box}

body{
  margin:0;
  font-family:Arial,sans-serif;
  background:#080d1b;
  color:#fff;
}

.wrap{
  max-width:950px;
  margin:auto;
  padding:18px;
}

.hero{
  text-align:center;
  padding:25px 5px;
}

.hero h1{
  font-size:32px;
  margin:5px;
}

.hero p{
  color:#aeb9d4;
}

.card{
  background:#121a2d;
  border:1px solid #2b3858;
  border-radius:18px;
  padding:20px;
  margin:16px 0;
}

h2{
  margin-top:0;
}

.fees{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:12px;
  margin-bottom:20px;
}

.fee{
  padding:16px;
  background:#0d2630;
  border-radius:12px;
  text-align:center;
}

.fee b{
  display:block;
  font-size:22px;
  margin-top:5px;
}

.grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:14px;
}

label{
  display:block;
  margin:12px 0 6px;
  font-weight:bold;
}

input,select{
  width:100%;
  padding:13px;
  border-radius:10px;
  border:1px solid #3a4766;
  background:#0a1122;
  color:white;
  font-size:15px;
}

button{
  border:0;
  border-radius:10px;
  padding:13px 18px;
  margin-top:18px;
  font-weight:bold;
  cursor:pointer;
  background:#16d39a;
  color:#03130d;
}

button.alt{
  background:#34415f;
  color:#fff;
}

button.danger{
  background:#d84b4b;
  color:#fff;
}

.payment{
  text-align:center;
  background:#0b1224;
  border-radius:14px;
  padding:18px;
  margin-top:18px;
}

.payment img{
  width:220px;
  max-width:100%;
  border-radius:12px;
  background:white;
  padding:8px;
}

.upi{
  font-size:17px;
  margin-top:10px;
}

.msg{
  padding:12px;
  border-radius:10px;
  margin-top:15px;
  background:#102c38;
}

.stats{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
}

.stat{
  background:#0b1224;
  padding:14px;
  border-radius:12px;
}

.stat b{
  display:block;
  font-size:22px;
  margin-top:5px;
}

.team{
  padding:14px;
  border:1px solid #303d5d;
  border-radius:12px;
  margin-top:10px;
  background:#0e1629;
}

.paid{
  color:#55efaa;
}

.pending{
  color:#ffd166;
}

.small{
  font-size:13px;
  color:#aeb9d4;
}

.hidden{
  display:none;
}

.admin-actions{
  display:flex;
  gap:8px;
  flex-wrap:wrap;
}

@media(max-width:650px){
  .grid,
  .fees,
  .stats{
    grid-template-columns:1fr;
  }
}
</style>
</head>

<body>

<div class="wrap">

<div class="hero">
<h1>🔥 FREE FIRE TOURNAMENT</h1>
<p>Official Registration Portal</p>
</div>


<!-- REGISTRATION -->

<div class="card">

<h2>📝 Tournament Registration</h2>

<div class="fees">

<div class="fee">
Team Registration
<b>₹200</b>
<span class="small">4 Players</span>
</div>

<div class="fee">
Solo Registration
<b>₹50</b>
<span class="small">1 Player</span>
</div>

</div>


<form id="registrationForm">

<label>Registration Type</label>

<select id="registrationType" required>

<option value="Team">Team — ₹200</option>
<option value="Solo">Solo — ₹50</option>

</select>


<label>Name / Team Name</label>

<input
id="name"
required
placeholder="Team name or player name"
>


<div class="grid">

<div>

<label>Captain / Player Name</label>

<input
id="captainName"
required
placeholder="Enter name"
>

</div>


<div>

<label>Mobile / WhatsApp</label>

<input
id="mobile"
required
inputmode="tel"
placeholder="Enter mobile number"
>

</div>

</div>


<!-- TEAM PLAYERS -->

<div id="teamPlayers">

<h3>👥 Team Player UIDs</h3>

<div class="grid">

<div>
<label>Player 1 UID</label>
<input id="p1" placeholder="UID">
</div>

<div>
<label>Player 2 UID</label>
<input id="p2" placeholder="UID">
</div>

<div>
<label>Player 3 UID</label>
<input id="p3" placeholder="UID">
</div>

<div>
<label>Player 4 UID</label>
<input id="p4" placeholder="UID">
</div>

</div>

</div>


<!-- SOLO PLAYER -->

<div id="soloPlayer" class="hidden">

<label>Free Fire UID</label>

<input
id="soloUID"
placeholder="Enter your Free Fire UID"
>

</div>


<!-- PAYMENT -->

<div class="payment">

<h3>💳 Payment</h3>

<p>Registration Fee:</p>

<h2 id="feeAmount">₹200</h2>

<p>Scan the QR code below to pay.</p>

<img src="qr-code.png" alt="Tournament Payment QR Code">

<div class="qr">
UPI ID: <b id="8894132310@ptyes"></b>
</div>

<p class="small"> 
Payment karne ke baad UTR / Transaction ID zaroor enter karein.
</p>

</div>


<label>Transaction ID / UTR</label>

<input
id="transactionId"
required
placeholder="Enter UTR / Transaction ID"
>


<button type="submit">
Submit Registration
</button>

</form>


<div id="success" class="msg hidden"></div>

</div>



<!-- ADMIN -->

<div class="card">

<h2>🔐 Admin Dashboard</h2>

<p class="small">
Payment verification yahan se manually ki ja sakti hai.
Registration initially Pending rahegi.
</p>


<div class="stats">

<div class="stat">
Total
<b id="teamCount">0</b>
</div>

<div class="stat">
Teams
<b id="teamOnlyCount">0</b>
</div>

<div class="stat">
Solo
<b id="soloCount">0</b>
</div>

<div class="stat">
Collected
<b id="totalAmount">₹0</b>
</div>

</div>


<div class="admin-actions">

<button class="alt" onclick="renderRegistrations()">
Refresh
</button>

<button class="alt" onclick="exportCSV()">
Export CSV
</button>

<button class="danger" onclick="clearAll()">
Clear All
</button>

</div>


<div id="registrationList"></div>

</div>

</div>


<script>

/* =====================================================
   SETTINGS
===================================================== */

const UPI_ID = "YOUR-UPI-ID@upi";

const TEAM_FEE = 200;
const SOLO_FEE = 50;

const STORAGE_KEY = "free_fire_tournament_registrations";


/* =====================================================
   STORAGE
===================================================== */

function readData(){

try{

return JSON.parse(
localStorage.getItem(STORAGE_KEY) || "[]"
);

}catch(e){

return [];

}

}


function writeData(data){

localStorage.setItem(
STORAGE_KEY,
JSON.stringify(data)
);

}


/* =====================================================
   SECURITY
===================================================== */

function escapeHTML(value){

return String(value).replace(
/[&<>"']/g,

function(c){

return {

"&":"&amp;",
"<":"&lt;",
">":"&gt;",
'"':"&quot;",
"'":"&#39;"

}[c];

}

);

}


/* =====================================================
   REGISTRATION TYPE
===================================================== */

registrationType.addEventListener(
"change",
function(){

if(this.value === "Solo"){

feeAmount.textContent = "₹50";

teamPlayers.classList.add("hidden");

soloPlayer.classList.remove("hidden");

p1.required=false;
p2.required=false;
p3.required=false;
p4.required=false;

soloUID.required=true;

}else{

feeAmount.textContent = "₹200";

teamPlayers.classList.remove("hidden");

soloPlayer.classList.add("hidden");

p1.required=true;
p2.required=true;
p3.required=true;
p4.required=true;

soloUID.required=false;

}

}
);


/* =====================================================
   REGISTRATION
===================================================== */

registrationForm.addEventListener(
"submit",

function(e){

e.preventDefault();


const data = readData();

const type = registrationType.value;

const fee =
type === "Team"
? TEAM_FEE
: SOLO_FEE;


const number =
"FF-" +
String(data.length + 1)
.padStart(4,"0");


const item = {

registration_no:number,

registration_type:type,

name:name.value.trim(),

captain_name:captainName.value.trim(),

mobile:mobile.value.trim(),

player1_uid:
type==="Team"
? p1.value.trim()
: soloUID.value.trim(),

player2_uid:
type==="Team"
? p2.value.trim()
: "",

player3_uid:
type==="Team"
? p3.value.trim()
: "",

player4_uid:
type==="Team"
? p4.value.trim()
: "",

fee:fee,

payment_status:"Pending",

transaction_id:
transactionId.value.trim(),

created_at:
new Date().toLocaleString("en-IN")

};


data.push(item);

writeData(data);

updateStats();


success.innerHTML =
"✅ Registration submitted successfully!<br><br>" +

"Registration No: <b>" +
number +
"</b><br>" +

"Payment Status: <b class='pending'>" +
"Pending Verification" +
"</b><br><br>" +

"Admin UTR verify karne ke baad payment Paid mark karega.";


success.classList.remove("hidden");


registrationForm.reset();

registrationType.value="Team";

teamPlayers.classList.remove("hidden");

soloPlayer.classList.add("hidden");

p1.required=true;
p2.required=true;
p3.required=true;
p4.required=true;

soloUID.required=false;

feeAmount.textContent="₹200";


renderRegistrations();

}

);


/* =====================================================
   STATS
===================================================== */

function updateStats(){

const data=readData();

const teams =
data.filter(
x=>x.registration_type==="Team"
);

const solos =
data.filter(
x=>x.registration_type==="Solo"
);

const paid =
data.filter(
x=>x.payment_status==="Paid"
);


const total =
paid.reduce(
(sum,x)=>sum + Number(x.fee),
0
);


teamCount.textContent=data.length;

teamOnlyCount.textContent=teams.length;

soloCount.textContent=solos.length;

totalAmount.textContent="₹"+total;

}


/* =====================================================
   ADMIN RENDER
===================================================== */

function renderRegistrations(){

const data=readData();

if(!data.length){

registrationList.innerHTML =
'<p class="small">No registrations yet.</p>';

updateStats();

return;

}


registrationList.innerHTML =
data.map(

(x,index)=>`

<div class="team">

<b>
${escapeHTML(x.registration_no)}
—
${escapeHTML(x.name)}
</b>

<br>

Type:
<b>${escapeHTML(x.registration_type)}</b>

<br>

Captain / Player:
${escapeHTML(x.captain_name)}

<br>

Mobile:
${escapeHTML(x.mobile)}

<br>

UID:
${escapeHTML(x.player1_uid)}

${x.registration_type==="Team"
? `<br>
Players:
${escapeHTML(x.player1_uid)}
•
${escapeHTML(x.player2_uid)}
•
${escapeHTML(x.player3_uid)}
•
${escapeHTML(x.player4_uid)}`
:""
}

<br>

Fee:
<b>₹${escapeHTML(x.fee)}</b>

<br>

Transaction ID:
${escapeHTML(x.transaction_id)}

<br>

Payment:

<b class="${
x.payment_status==="Paid"
?"paid"
:"pending"
}">

${escapeHTML(x.payment_status)}

</b>

<br>

<span class="small">
${escapeHTML(x.created_at)}
</span>

<br>


${
x.payment_status==="Pending"

?

`<button
onclick="markPaid(${index})"
>
✅ Mark Payment Paid
</button>`

:

`<button
class="alt"
onclick="markPending(${index})"
>
↩ Mark Pending
</button>`
}


<button
class="danger"
onclick="deleteRegistration(${index})"
>
Delete
</button>

</div>

`

).join("");


updateStats();

}


/* =====================================================
   PAYMENT VERIFICATION
===================================================== */

function markPaid(index){

const data=readData();

data[index].payment_status="Paid";

writeData(data);

renderRegistrations();

}


function markPending(index){

const data=readData();

data[index].payment_status="Pending";

writeData(data);

renderRegistrations();

}


/* =====================================================
   DELETE
===================================================== */

function deleteRegistration(index){

if(!confirm("Delete this registration?")){

return;

}

const data=readData();

data.splice(index,1);

writeData(data);

renderRegistrations();

}


/* =====================================================
   CLEAR
===================================================== */

function clearAll(){

if(
!confirm(
"Are you sure you want to delete ALL registrations?"
)
){

return;

}

localStorage.removeItem(STORAGE_KEY);

renderRegistrations();

}


/* =====================================================
   CSV EXPORT
===================================================== */

function exportCSV(){

const data=readData();

if(!data.length){

alert("No registrations found.");

return;

}


const header=[

"Registration No",
"Type",
"Name / Team",
"Captain / Player",
"Mobile",
"Player 1 UID",
"Player 2 UID",
"Player 3 UID",
"Player 4 UID",
"Fee",
"Payment Status",
"Transaction ID",
"Created At"

];


const rows=data.map(x=>[

x.registration_no,
x.registration_type,
x.name,
x.captain_name,
x.mobile,
x.player1_uid,
x.player2_uid,
x.player3_uid,
x.player4_uid,
x.fee,
x.payment_status,
x.transaction_id,
x.created_at

]);


const csv=[header,...rows]

.map(

row=>
row
.map(
v =>
'"'+
String(v)
.replace(/"/g,'""')+
'"'
)
.join(",")

)

.join("\n");


const blob=new Blob(

[csv],

{
type:"text/csv;charset=utf-8"
}

);


const a=document.createElement("a");

a.href=URL.createObjectURL(blob);

a.download=
"free_fire_registrations.csv";

a.click();

}


/* =====================================================
   INITIAL LOAD
===================================================== */

upiId.textContent=UPI_ID;

renderRegistrations();

</script>

</body>
</html>
