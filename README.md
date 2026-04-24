<!DOCTYPE html>
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

/* Hidden top-right admin button */
.admin-btn{
  position:fixed;
  top:8px;
  right:8px;
  width:28px;
  height:28px;
  background:#fff;
  border:none;
  opacity:0.02;
  cursor:pointer;
}

.admin-btn:hover{
  opacity:0.08;
}

/* Popup */
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

input{
  width:100%;
  padding:12px;
  margin-top:12px;
  border-radius:8px;
  border:1px solid #333;
  background:#000;
  color:#fff;
}

button{
  margin-top:15px;
  padding:10px 18px;
  border:none;
  border-radius:8px;
  background:#222;
  color:#fff;
  cursor:pointer;
}

button:hover{
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

<!-- Hidden Admin Button -->
<button class="admin-btn" onclick="openLogin()"></button>

<div class="container">
  <h1>Charlie Websites</h1>
  <p>Select a website to continue</p>

  <div class="grid">
    <a class="btn" href="https://cigimessage.lovable.app/" target="_blank">Messages</a>
    <a class="btn" href="https://yourdigicardlink.com" target="_blank">DigiCard</a>
    <a class="btn" href="https://yourstorelink.com" target="_blank">Store</a>
    <a class="btn" href="https://yourportfolio.com" target="_blank">Portfolio</a>
  </div>

  <div class="footer">Main Hub Website</div>
</div>

<!-- Login Popup -->
<div class="popup" id="loginPopup">
  <h2>Admin Access</h2>
  <input type="password" id="password" placeholder="Enter password">
  <button onclick="checkPassword()">Login</button>
</div>

<!-- Stats Popup -->
<div class="popup" id="statsPopup">
  <h2>Total Visitors</h2>
  <h1 id="visitCount">0</h1>
  <button onclick="closePopups()">Close</button>
</div>

<script>
/* ===============================
   YOUR SETTINGS
================================= */

const SUPABASE_URL = "https://aipfgziworjuxmupdkcw.supabase.co";
const SUPABASE_KEY = "PASTE_YOUR_ANON_KEY_HERE";
const PASSWORD = "admin123";

/* ===============================
   COUNT VISITS
================================= */

async function addVisit(){

  try{

    const response = await fetch(
      SUPABASE_URL + "/rest/v1/visits?id=eq.1",
      {
        headers:{
          apikey:SUPABASE_KEY,
          Authorization:"Bearer " + SUPABASE_KEY
        }
      }
    );

    const data = await response.json();

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

  }catch(error){
    console.log("Visit counter error");
  }

}

addVisit();

/* ===============================
   ADMIN PANEL
================================= */

function openLogin(){
  document.getElementById("loginPopup").style.display="block";
}

function closePopups(){
  document.getElementById("loginPopup").style.display="none";
  document.getElementById("statsPopup").style.display="none";
}

async function checkPassword(){

  const pass = document.getElementById("password").value;

  if(pass !== PASSWORD){
    alert("Wrong password");
    return;
  }

  const response = await fetch(
    SUPABASE_URL + "/rest/v1/visits?id=eq.1",
    {
      headers:{
        apikey:SUPABASE_KEY,
        Authorization:"Bearer " + SUPABASE_KEY
      }
    }
  );

  const data = await response.json();

  document.getElementById("visitCount").innerText = data[0].count;

  document.getElementById("loginPopup").style.display="none";
  document.getElementById("statsPopup").style.display="block";
}
</script>

</body>
</html>
