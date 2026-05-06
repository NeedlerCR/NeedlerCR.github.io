<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Charlie Main Website</title>

<style>
*{
  box-sizing:border-box;
}

html,body{
  margin:0;
  padding:0;
  min-height:100%;
  background:#000;
  color:#fff;
  font-family:Arial,sans-serif;
}

body{
  display:flex;
  justify-content:center;
  align-items:center;
  padding:30px;
}

/* ===== TOP RIGHT PINK BUTTON ===== */
.admin-btn{
  position:fixed;
  top:10px;
  right:10px;
  background:#000;
  color:#000;
  border:none;
  padding:10px 14px;
  border-radius:10px;
  font-weight:bold;
  cursor:pointer;
  z-index:1000;
}

.admin-btn:hover{
  background:#000;
}

/* ===== MAIN LAYOUT ===== */
.container{
  width:100%;
  max-width:600px;
  text-align:center;
}

h1{
  margin-bottom:10px;
  font-size:2.2rem;
}

p{
  color:#ccc;
  margin-bottom:30px;
}

.grid{
  display:grid;
  gap:15px;
}

.btn{
  display:block;
  padding:18px;
  text-decoration:none;
  color:#fff;
  background:#111;
  border:1px solid #333;
  border-radius:12px;
  font-size:1.1rem;
  transition:0.2s ease;
}

.btn:hover{
  background:#1f1f1f;
  border-color:#0f0;
  transform:scale(1.02);
}

/* ===== POPUP ===== */
.popup{
  display:none;
  position:fixed;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  background:#111;
  border:1px solid #333;
  border-radius:14px;
  padding:25px;
  width:320px;
  text-align:center;
  z-index:1000;
}

.close-btn{
  margin-top:15px;
  padding:10px 18px;
  border:none;
  border-radius:8px;
  background:#222;
  color:#fff;
  cursor:pointer;
}

.close-btn:hover{
  background:#333;
}

.footer{
  margin-top:30px;
  font-size:0.9rem;
  color:#666;
}
</style>
</head>

<body>

<!-- PINK STATS BUTTON -->
<button class="admin-btn" onclick="showStats()"></button>

<div class="container">
  <h1>Charlie Websites</h1>
  <p>Select a website to continue</p>

  <div class="grid">
    <a class="btn" href="https://cigimessage.lovable.app/" target="_blank">Messages</a>
    <a class="btn" href="https://wallet-stamper--cnee28.replit.app/" target="_blank">DigiCard</a>
    <a class="btn" href="https://lifesync-ffz4byts.manus.space/" target="_blank">Habit Tracker</a>
    <a class="btn" href="https://splitly-money.base44.app" target="_blank">Splitly - Money tracker</a>
  </div>

  <div class="footer">Main Hub Website</div>
  <div class="footer"><a href="https://needlercr.github.io/Charlie-Needler/">©️ Charlie Needler 2026</a></div>
</div>

<!-- POPUP -->
<div class="popup" id="statsPopup">
  <h2>Total Visitors</h2>
  <h1 id="visitCount">Loading...</h1>
  <button class="close-btn" onclick="closeStats()">Close</button>
</div>

<script>
/* =========================
   SUPABASE CONFIG
========================= */
const SUPABASE_URL = "https://aipfgziworjuxmupdkcw.supabase.co";
const SUPABASE_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFpcGZneml3b3JqdXhtdXBka2N3Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzcwMjg0ODgsImV4cCI6MjA5MjYwNDQ4OH0.RuDYMce0AJMLZ4YUQft_SyAHQ46egpkLJxXqOChwnqM";

/* =========================
   ADD VISIT ON LOAD
========================= */
async function addVisit(){

  try{

    const res = await fetch(
      SUPABASE_URL + "/rest/v1/visits?select=*",
      {
        headers:{
          apikey:SUPABASE_KEY,
          Authorization:"Bearer " + SUPABASE_KEY
        }
      }
    );

    const data = await res.json();

    if(!data.length) return;

    const current = data[0].count;

    await fetch(
      SUPABASE_URL + "/rest/v1/visits?id=eq.1",
      {
        method:"PATCH",
        headers:{
          "Content-Type":"application/json",
          apikey:SUPABASE_KEY,
          Authorization:"Bearer " + SUPABASE_KEY
        },
        body:JSON.stringify({
          count: current + 1
        })
      }
    );

  }catch(e){
    console.log("Visit tracking failed");
  }
}

addVisit();

/* =========================
   SHOW STATS POPUP
========================= */
async function showStats(){

  try{

    const res = await fetch(
      SUPABASE_URL + "/rest/v1/visits?select=*",
      {
        headers:{
          apikey:SUPABASE_KEY,
          Authorization:"Bearer " + SUPABASE_KEY
        }
      }
    );

    const data = await res.json();

    if(!data.length){
      document.getElementById("visitCount").innerText = "0";
    } else {
      document.getElementById("visitCount").innerText = data[0].count;
    }

    document.getElementById("statsPopup").style.display = "block";

  }catch(err){
    console.log(err);
    alert("Error loading stats");
  }
}

/* CLOSE POPUP */
function closeStats(){
  document.getElementById("statsPopup").style.display = "none";
}
</script>

</body>
</html>
