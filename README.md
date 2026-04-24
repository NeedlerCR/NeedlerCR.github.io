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

/* Hidden admin button */
.admin-btn{
  position:fixed;
  top:10px;
  right:10px;
  width:25px;
  height:25px;
  background:transparent;
  border:none;
  cursor:pointer;
  opacity:0.03;
}

.admin-btn:hover{
  opacity:0.2;
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
  width:300px;
  text-align:center;
  z-index:1000;
}

.popup h2{
  margin-top:0;
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

<!-- Hidden top-right button -->
<button class="admin-btn" onclick="showVisits()"></button>

<div class="container">
  <h1>Charlie Websites</h1>
  <p>Select a website to continue</p>

  <div class="grid">
    <a class="btn" href="https://cigimessage.lovable.app/" target="_blank">Messages</a>
    <a class="btn" href="https://wallet-stamper--cnee28.replit.app/" target="_blank">DigiCard</a>
    
  </div>

  <div class="footer">
    Main Hub Website
  </div>
</div>

<!-- Popup -->
<div class="popup" id="visitPopup">
  <h2>Website Visits</h2>
  <p>Total Visitors:</p>
  <h1 id="visitCount">0</h1>
  <button class="close-btn" onclick="closePopup()">Close</button>
</div>

<script>
/* Count visits using browser localStorage */
let visits = localStorage.getItem("siteVisits");

if(!visits){
  visits = 0;
}

visits++;
localStorage.setItem("siteVisits", visits);

function showVisits(){
  document.getElementById("visitCount").innerText = visits;
  document.getElementById("visitPopup").style.display = "block";
}

function closePopup(){
  document.getElementById("visitPopup").style.display = "none";
}
</script>

</body>
</html>
