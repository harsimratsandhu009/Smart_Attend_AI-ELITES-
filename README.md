<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Attend AI | Sri Dasmesh School</title>

<script defer src="https://cdn.jsdelivr.net/npm/face-api.js@0.22.2/dist/face-api.min.js"></script>

<style>
:root {
  --brown:#54210f;
  --copper:#a84d20;
  --orange:#c56532;
  --cream:#fff8ed;
  --paper:#fffdf9;
  --line:#ead8c3;
  --red:#a51f29;
  --green:#18803b;
}
*{box-sizing:border-box}
body{
  margin:0;background:linear-gradient(135deg,#fffaf1,#f8e7d3,#fffaf4);
  color:var(--brown);font-family:Arial,sans-serif;min-height:100vh
}
button,input,select{font:inherit}
button{cursor:pointer}
button:disabled{opacity:.5;cursor:not-allowed}
header{
  display:flex;align-items:center;justify-content:space-between;gap:15px;
  padding:17px 4%;border-bottom:1px solid var(--line);
  background:linear-gradient(110deg,#fffaf2,#f9e5ce,#fff8ef)
}
.brand{font-family:Georgia,serif;font-size:clamp(22px,4vw,43px);
  font-weight:bold;color:#984519}
.tagline{font-size:11px;letter-spacing:4px;margin-top:5px}
.datebox{border:1px solid var(--line);border-radius:14px;padding:12px 16px;background:#fffaf2}
.layout{display:grid;grid-template-columns:235px minmax(0,1fr);gap:22px;padding:20px}
.sidebar{
  min-height:calc(100vh - 145px);padding:15px 11px;border:1px solid var(--line);
  border-radius:20px;background:#fffaf2;box-shadow:0 8px 22px #54210f12;
  display:flex;flex-direction:column;gap:7px
}
.nav{
  border:0;background:transparent;color:var(--brown);text-align:left;
  border-radius:10px;padding:15px;font-weight:600
}
.nav:hover,.nav.active{background:linear-gradient(110deg,#b65325,#92401d);color:white}
.logout{margin-top:auto!important;background:linear-gradient(110deg,#b3212c,#861923)!important;color:white!important}
main{min-width:0}
.page{display:none}
.page.active{display:block}
h1,h2,h3{font-family:Georgia,serif}
h1{font-size:clamp(27px,3vw,39px);margin:5px 0}
h2{font-size:25px}
.muted{color:#816b5a;line-height:1.6}
.panel,.stat,.hero{
  background:linear-gradient(130deg,#fffdf9,#fff5e8);
  border:1px solid var(--line);border-radius:15px;
  box-shadow:0 3px 12px #54210f08
}
.panel{padding:18px;margin:14px 0}
.hero{padding:25px;display:flex;align-items:center;justify-content:space-between;gap:20px;flex-wrap:wrap}
.hero h2{font-size:30px;margin:5px 0}
.stats{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px;margin:16px 0}
.stat{padding:17px;min-width:0}
.stat small{color:#816b5a}
.number{font-size:32px;font-weight:bold;margin-top:9px}
.green{color:var(--green)}.red{color:#c6222b}
.btn{
  border:0;border-radius:9px;padding:12px 17px;color:white;font-weight:bold;
  background:linear-gradient(110deg,#bb5b2c,#91401e)
}
.btn.secondary{background:#fff8ef;color:var(--brown);border:1px solid var(--line)}
.btn.danger{background:linear-gradient(110deg,#b3212c,#861923)}
.btnrow{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.filters{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px;align-items:end}
label{font-size:13px;font-weight:bold;display:block;margin-bottom:7px}
input,select{
  width:100%;padding:12px;border:1px solid #dfcbb5;border-radius:9px;
  background:#fffdf9;color:var(--brown);min-width:0
}
input:focus,select:focus{outline:2px solid #d49a71;border-color:transparent}
.tablewrap{overflow:auto;margin-top:15px}
table{border-collapse:collapse;width:100%;min-width:650px;background:#fffdf9}
th,td{padding:12px;text-align:left;border:1px solid #efe2d4;font-size:14px}
th{background:#f9eddf}
.pill{display:inline-block;border-radius:7px;padding:5px 11px;font-weight:bold;background:#e0f1d9;color:#176b2d}
.pill.absent{background:#ffe0df;color:#b61e27}
.low-row{background:#fff0ed}
.summary{display:flex;gap:25px;flex-wrap:wrap;padding:14px;background:#fff6eb;border-radius:10px;margin-top:15px}
#loginScreen{min-height:100vh;display:grid;place-items:center;padding:20px}
.login-card{
  display:grid;grid-template-columns:1fr 1fr;max-width:1080px;width:100%;
  min-height:570px;border:1px solid var(--line);border-radius:25px;overflow:hidden;
  background:#fffdf9;box-shadow:0 15px 45px #54210f16
}
.login-brand{padding:45px;background:linear-gradient(145deg,#fcebd4,#f4d2b0)}
.login-brand h1{font-size:43px;line-height:1.15;margin-top:65px}
.login-form{padding:38px;align-self:center}
.login-form h2{font-size:34px;margin-bottom:8px}
.login-form input,.login-form select{margin-bottom:16px}
.login-form .btn{width:100%;margin-top:6px}
.small{font-size:12px;color:#87786a;line-height:1.5}
a{color:#a84d20;cursor:pointer;font-weight:bold}
.hidden{display:none!important}
#cameraBox{position:relative;max-width:800px;width:100%;margin:15px auto;background:#241b16;border-radius:12px;overflow:hidden}
#video{width:100%;display:block;transform:scaleX(-1)}
#overlay{position:absolute;inset:0;width:100%;height:100%;transform:scaleX(-1)}
.camera-layout{display:grid;grid-template-columns:minmax(0,2fr) minmax(200px,1fr);gap:16px}
#cameraStatus{padding:12px;border-radius:9px;background:#f8eddf;margin:12px 0}
.photo-preview{width:85px;height:85px;object-fit:cover;border-radius:50%;display:none;margin:8px 0}
.bar{height:12px;border-radius:10px;background:#f0e1d2;overflow:hidden;margin-top:8px}
.bar span{height:100%;display:block;background:linear-gradient(90deg,#ba5a2c,#df9c58)}
footer{text-align:center;padding:20px;color:#897564;font-size:13px}
@media(max-width:1000px){
 .layout{grid-template-columns:1fr;padding:12px}
 .sidebar{min-height:auto;display:grid;grid-template-columns:repeat(3,1fr)}
 .logout{margin-top:0!important}.stats{grid-template-columns:repeat(2,minmax(0,1fr))}
 .filters{grid-template-columns:repeat(2,minmax(0,1fr))}
}
@media(max-width:650px){
 header{align-items:flex-start}.tagline{letter-spacing:2px}
 .login-card{grid-template-columns:1fr}.login-brand{padding:25px}
 .login-brand h1{font-size:30px;margin-top:25px}.login-form{padding:25px}
 .sidebar{grid-template-columns:repeat(2,1fr)}.camera-layout{grid-template-columns:1fr}
 .filters{grid-template-columns:1fr 1fr}.hero{padding:17px}
}
</style>
</head>
<body>

<!-- LOGIN AND ACCOUNT CREATION -->
<section id="loginScreen">
 <div class="login-card">
  <div class="login-brand">
   <div style="font-size:38px;color:#a84d20">✦</div>
   <h2 style="font-size:32px;margin:12px 0">SRI DASMESH<br>SCHOOL</h2>
   <p>DISCIPLINE | KNOWLEDGE | EXCELLENCE</p>
   <h1>Smart Attend <span style="color:#ae5128">AI</span></h1>
   <p>Smarter Attendance | Brighter Future</p>
   <p class="muted">A simple and smart way to manage student attendance.</p>
  </div>
  <div class="login-form">
   <div id="loginForm">
    <h2>Welcome Back!</h2>
    <p class="muted">Sign in to continue to your attendance dashboard.</p>
    <label>Email address or name</label>
    <input id="loginIdentity" placeholder="Enter your email or name" autocomplete="username">
    <label>Password</label>
    <input id="loginPassword" type="password" placeholder="Enter your password" autocomplete="current-password">
    <div style="display:flex;justify-content:space-between;gap:10px;font-size:13px;margin:8px 0 17px">
     <label style="font-weight:normal"><input id="remember" type="checkbox" style="width:auto"> Remember me</label>
     <a onclick="forgotPassword()">Forgot password?</a>
    </div>
    <button class="btn" onclick="login()">Sign In →</button>
    <p style="text-align:center;margin-top:24px">Don't have an account? <a onclick="showSignup()">Create account</a></p>
   </div>
   <div id="signupForm" class="hidden">
    <h2>Create Account</h2>
    <p class="muted">Create your school account.</p>
    <label>Full name</label><input id="regName" placeholder="Full name">
    <label>Email address</label><input id="regEmail" type="email" placeholder="Email address">
    <label>Role</label>
    <select id="regRole"><option>Teacher</option><option>Principal</option><option>Administrator</option></select>
    <label>Create password</label><input id="regPassword" type="password" placeholder="At least 6 characters">
    <label>School access code</label><input id="regCode" type="password" placeholder="School access code">
    <button class="btn" onclick="signup()">Create Account</button>
    <p style="text-align:center">Already registered? <a onclick="showLogin()">Sign in</a></p>
   </div>
   <p class="small">Demonstration project. Accounts and records are saved in this browser. Do not use real sensitive student information on a public demonstration website.</p>
  </div>
 </div>
</section>

<!-- MAIN APPLICATION -->
<div id="app" class="hidden">
 <header>
  <div>
   <div class="brand">SRI DASMESH SCHOOL</div>
   <div class="tagline">DISCIPLINE | KNOWLEDGE | EXCELLENCE</div>
  </div>
  <div class="datebox">▦ Today's Date<br><strong id="todayDate"></strong></div>
 </header>
 <div class="layout">
  <aside class="sidebar">
   <button class="nav active" data-page="dashboard" onclick="navigate('dashboard',this)">⌂ &nbsp; Dashboard</button>
   <button class="nav" data-page="attendance" onclick="navigate('attendance',this)">☑ &nbsp; Attendance</button>
   <button class="nav" data-page="students" onclick="navigate('students',this)">♟ &nbsp; Students</button>
   <button class="nav" onclick="toggleReports()">▤ &nbsp; Reports⌄</button>
   <div id="reportNav" class="hidden" style="display:grid;gap:5px;padding-left:15px">
    <button class="nav" onclick="openReport('daily',this)">Daily</button>
    <button class="nav" onclick="openReport('weekly',this)">Weekly</button>
    <button class="nav" onclick="openReport('monthly',this)">Monthly</button>
   </div>
   <button class="nav" data-page="alerts" onclick="navigate('alerts',this)">♧ &nbsp; Alerts</button>
   <button class="nav logout" onclick="logout()">⇥ &nbsp; Logout</button>
  </aside>

  <main>
   <!-- DASHBOARD -->
   <section id="dashboard" class="page active">
    <div class="hero">
     <div><div id="greeting">Good day,</div><h1 id="teacherGreeting">Welcome!</h1>
      <p class="muted">Welcome to Smart Attend AI. Track attendance and manage your students easily.</p></div>
     <div style="font-size:27px;font-family:Georgia,serif">♟ Smart Attend <span style="color:#b9572b">AI</span></div>
    </div>
    <div class="stats">
     <div class="stat"><small>Total Students</small><div class="number" id="totalStudents">0</div></div>
     <div class="stat"><small>Present Today</small><div class="number green" id="presentToday">0</div></div>
     <div class="stat"><small>Absent Today</small><div class="number red" id="absentToday">0</div></div>
     <div class="stat"><small>Classes Today</small><div class="number" id="classesToday">0</div></div>
    </div>
    <div class="panel">
     <h2>Today's Attendance</h2>
     <div style="display:flex;align-items:center;gap:25px;flex-wrap:wrap">
      <svg id="donut" viewBox="0 0 180 180" width="180" height="180" aria-label="Attendance ring chart">
       <circle cx="90" cy="90" r="67" fill="none" stroke="#f2d9cb" stroke-width="20"/>
       <circle id="donutGreen" cx="90" cy="90" r="67" fill="none" stroke="#2ca45c" stroke-width="20" stroke-dasharray="0 421" transform="rotate(-90 90 90)"/>
       <text id="donutPercent" x="90" y="87" text-anchor="middle" font-size="24" font-weight="bold" fill="#54210f">0%</text>
       <text x="90" y="108" text-anchor="middle" font-size="12" fill="#54210f">Present</text>
      </svg>
      <div style="flex:1"><p><span class="green">● Present</span> <strong id="ringPresent">0</strong></p>
       <p><span class="red">● Absent</span> <strong id="ringAbsent">0</strong></p>
       <button class="btn" onclick="navigate('attendance')">▣ Mark Attendance →</button>
      </div>
     </div>
    </div>
    <div class="panel"><h2>Today's Class-wise Attendance</h2><div id="classSummary"></div></div>
   </section>

   <!-- ATTENDANCE -->
   <section id="attendance" class="page">
    <h1>Attendance Management</h1>
    <p class="muted">Select a class and section, then start the camera.</p>
    <div class="panel"><div class="filters">
     <div><label>Class</label><select id="attClass" onchange="updateStreams('att')"></select></div>
     <div><label>Stream</label><select id="attStream"></select></div>
     <div><label>Section</label><select id="attSection"><option>A</option><option>B</option><option>C</option><option>D</option></select></div>
     <div><label>Date</label><input id="attDate" type="date"></div>
    </div>
    <p class="small">Streams are applicable to Classes 11 and 12.</p>
    </div>
    <div class="panel">
     <h2>▣ Mark Attendance</h2>
     <div id="cameraStatus">Camera is stopped. Select your class and click Start Camera.</div>
     <div class="camera-layout">
      <div>
       <div id="cameraBox" class="hidden">
        <video id="video" autoplay muted playsinline></video>
        <canvas id="overlay"></canvas>
       </div>
       <div class="btnrow">
        <button class="btn" id="startCameraBtn" onclick="startCamera()">Start Camera</button>
        <button class="btn secondary" onclick="stopCamera()">Close Camera</button>
        <button class="btn danger" onclick="finishAttendance()">Finish &amp; Mark Remaining Absent</button>
       </div>
      </div>
      <div>
       <h3>Session Students</h3>
       <div id="sessionList" class="muted">Select a class to see its students.</div>
       <hr style="border:0;border-top:1px solid var(--line);margin:18px 0">
       <h3>Manual Backup</h3>
       <label>Student</label><select id="manualStudent"></select>
       <button class="btn secondary" style="width:100%;margin-top:10px" onclick="manualPresent()">Mark Present</button>
      </div>
     </div>
    </div>
   </section>

   <!-- STUDENTS -->
   <section id="students" class="page">
    <div class="hero"><div><h1>Students</h1><p class="muted">Manage registered students and attendance records.</p></div>
     <button class="btn" onclick="showAddStudent()">＋ Add Student</button>
    </div>
    <div class="panel">
     <div class="filters">
      <div><label>Class</label><select id="stuClass" onchange="updateStreams('stu')"></select></div>
      <div><label>Stream</label><select id="stuStream"></select></div>
      <div><label>Section</label><select id="stuSection"><option>All</option><option>A</option><option>B</option><option>C</option><option>D</option></select></div>
      <div><label>Search</label><input id="stuSearch" placeholder="Name or admission number" oninput="renderStudents()"></div>
     </div>
     <div class="btnrow" style="margin-top:12px">
      <button class="btn" onclick="renderStudents()">Go →</button>
      <button class="btn secondary" onclick="document.getElementById('csvImport').click()">Import CSV</button>
      <input id="csvImport" type="file" accept=".csv,text/csv" class="hidden" onchange="importStudents(event)">
     </div>
     <div id="studentTable" class="tablewrap"></div>
     <div id="studentSummary" class="summary"></div>
    </div>
   </section>

   <!-- REPORTS -->
   <section id="reports" class="page">
    <h1 id="reportTitle">Daily Attendance Report</h1>
    <p class="muted">View attendance and export your report.</p>
    <div class="panel">
     <div class="filters">
      <div><label>Class</label><select id="repClass" onchange="updateStreams('rep')"></select></div>
      <div><label>Stream</label><select id="repStream"></select></div>
      <div><label>Section</label><select id="repSection"><option>All</option><option>A</option><option>B</option><option>C</option><option>D</option></select></div>
      <div id="repDateWrap"><label>Date</label><input id="repDate" type="date"></div>
      <div id="repMonthWrap" class="hidden"><label>Month</label><select id="repMonth"></select></div>
     </div>
     <div class="btnrow" style="margin-top:15px">
      <button class="btn" onclick="renderReport()">Go →</button>
      <button class="btn secondary" onclick="exportReport()">Export CSV / Excel</button>
      <button class="btn secondary" onclick="window.print()">Print</button>
     </div>
    </div>
    <div class="panel"><div id="reportTable" class="tablewrap"></div><div id="reportSummary" class="summary"></div></div>
   </section>

   <!-- ALERTS -->
   <section id="alerts" class="page">
    <div class="hero"><div><h1>Attendance Alerts</h1><p class="muted">Students with less than 75% attendance.</p></div>
     <div class="stat"><small>Students Below 75%</small><div class="number red" id="alertCount">0</div></div>
    </div>
    <div class="panel">
     <div class="filters">
      <div><label>Class View</label><select id="alertClass" onchange="renderAlerts()"></select></div>
      <div style="grid-column:span 2"><label>Search students</label><input id="alertSearch" placeholder="Name or admission number" oninput="renderAlerts()"></div>
     </div>
     <div id="alertTable" class="tablewrap"></div>
    </div>
   </section>

   <!-- ADD STUDENT -->
   <section id="addStudent" class="page">
    <div class="panel" style="max-width:850px;margin:0 auto">
     <h1>Add Student</h1>
     <p class="muted">Register a student and upload a clear face photo for recognition.</p>
     <form id="studentForm" onsubmit="saveStudent(event)">
      <div class="filters">
       <div style="grid-column:span 2"><label>Student Face Photo *</label><input id="studentPhoto" type="file" accept="image/*" required onchange="previewPhoto(event)"><img id="photoPreview" class="photo-preview" alt="Student photo preview"><p class="small">Use a clear, front-facing photograph.</p></div>
       <div><label>Student Full Name *</label><input id="studentName" required></div>
       <div><label>Admission Number *</label><input id="studentAdmission" required></div>
       <div><label>Roll Number *</label><input id="studentRoll" required></div>
       <div><label>Class *</label><select id="studentClass" required onchange="updateStreams('form')"></select></div>
       <div><label>Stream</label><select id="studentStream"></select></div>
       <div><label>Section *</label><select id="studentSection" required><option>A</option><option>B</option><option>C</option><option>D</option></select></div>
       <div><label>Father's Phone Number *</label><input id="studentPhone" type="tel" required pattern="[0-9+ -]{7,18}"></div>
      </div>
      <p class="muted" id="faceStatus">Face recognition model will be checked when you save.</p>
      <div class="btnrow"><button class="btn" type="submit">Save Student</button><button class="btn secondary" type="button" onclick="navigate('students')">Cancel</button></div>
     </form>
    </div>
   </section>
  </main>
 </div>
 <footer>Smart Attend AI · Sri Dasmesh School · Smarter Attendance, Brighter Future</footer>
</div>

<script>
"use strict";

const ACCESS_CODE = "DASHMESH09";
const CLASSES = ["Nursery","LKG","UKG",...Array.from({length:12},(_,i)=>"Class "+(i+1))];
const STREAMS = ["Science","Commerce","Humanities"];
const MODEL_URL = "https://cdn.jsdelivr.net/gh/justadudewhohacks/face-api.js@master/weights";
const KEY = "smartAttendAI_v1";

let db = loadDB();
let currentUser = null;
let cameraStream = null;
let cameraRunning = false;
let detectionBusy = false;
let faceModelsReady = false;
let faceModelPromise = null;
let session = null;
let recognizedInSession = new Set();
let lastRecognizedAt = {};
let videoTimer = null;
let currentReport = "daily";

function loadDB(){
 try{
  const data=JSON.parse(localStorage.getItem(KEY)||"{}");
  return {users:data.users||[],students:data.students||[],records:data.records||[],sessions:data.sessions||[]};
 }catch(e){return {users:[],students:[],records:[],sessions:[]};}
}
function saveDB(){localStorage.setItem(KEY,JSON.stringify(db));}
function escapeHTML(v){
 return String(v??"").replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
}
function today(){return new Date().toLocaleDateString("en-CA");}
function fmtDate(d){
 if(!d)return "—";
 return new Date(d+"T12:00:00").toLocaleDateString("en-IN",{day:"2-digit",month:"short",year:"numeric"});
}
function classOrder(c){return CLASSES.indexOf(c);}
function sortStudents(a,b){return classOrder(a.className)-classOrder(b.className)||a.section.localeCompare(b.section)||a.name.localeCompare(b.name);}
function isSenior(c){return c==="Class 11"||c==="Class 12";}
function studentFilter(classId,streamId,sectionId){
 let c=document.getElementById(classId)?.value||"All";
 let s=document.getElementById(streamId)?.value||"All";
 let sec=document.getElementById(sectionId)?.value||"All";
 return db.students.filter(x=>(c==="All"||x.className===c)&&(!isSenior(x.className)||s==="All"||x.stream===s)&&(sec==="All"||x.section===sec)).sort(sortStudents);
}
function populateSelect(id,items,all=false){
 const el=document.getElementById(id);if(!el)return;
 const old=el.value;
 el.innerHTML=(all?'<option value="All">All Classes</option>':'')+items.map(x=>`<option>${escapeHTML(x)}</option>`).join("");
 if(items.includes(old))el.value=old;
}
function initSelects(){
 ["attClass","stuClass","repClass","studentClass"].forEach(id=>populateSelect(id,CLASSES));
 populateSelect("alertClass",CLASSES,true);
 ["attSection","stuSection","repSection","studentSection"].forEach(id=>{
  const el=document.getElementById(id);if(el)el.innerHTML=(id==="stuSection"||id==="repSection"?'<option>All</option>':'')+"<option>A</option><option>B</option><option>C</option><option>D</option>";
 });
 const month=document.getElementById("repMonth");
 month.innerHTML=Array.from({length:12},(_,i)=>`<option value="${i}">${new Date(2025,i,1).toLocaleString("en",{month:"long"})}</option>`).join("");
 month.value=new Date().getMonth();
 ["attDate","repDate"].forEach(id=>document.getElementById(id).value=today());
 ["att","stu","rep","form"].forEach(updateStreams);
}
function updateStreams(prefix){
 const map={att:["attClass","attStream"],stu:["stuClass","stuStream"],rep:["repClass","repStream"],form:["studentClass","studentStream"]};
 const [cId,sId]=map[prefix];const c=document.getElementById(cId),s=document.getElementById(sId);
 if(!c||!s)return;
 const old=s.value;
 s.innerHTML='<option value="All">All Streams</option>'+STREAMS.map(x=>`<option>${x}</option>`).join("");
 if(prefix==="form")s.innerHTML=STREAMS.map(x=>`<option>${x}</option>`).join("");
 s.disabled=!isSenior(c.value);
 if(!isSenior(c.value))s.value=prefix==="form"?"": "All";
 else if([...s.options].some(o=>o.value===old))s.value=old;
}
function showLogin(){
 document.getElementById("signupForm").classList.add("hidden");
 document.getElementById("loginForm").classList.remove("hidden");
}
function showSignup(){
 document.getElementById("loginForm").classList.add("hidden");
 document.getElementById("signupForm").classList.remove("hidden");
}
function signup(){
 const name=document.getElementById("regName").value.trim();
 const email=document.getElementById("regEmail").value.trim().toLowerCase();
 const role=document.getElementById("regRole").value;
 const password=document.getElementById("regPassword").value;
 const code=document.getElementById("regCode").value.replace(/\s/g,"").toUpperCase();
 if(!name||!email||!password){alert("Please fill in all fields.");return;}
 if(password.length<6){alert("Use a password with at least 6 characters.");return;}
 if(code!==ACCESS_CODE){alert("Incorrect school access code.");return;}
 if(db.users.some(u=>u.email===email)){alert("This email is already registered. Please sign in.");return;}
 db.users.push({name,email,role,password});saveDB();
 alert("Account created successfully. You can now sign in.");
 document.getElementById("loginIdentity").value=email;
 document.getElementById("loginPassword").value="";
 showLogin();
}
function login(){
 const id=document.getElementById("loginIdentity").value.trim().toLowerCase();
 const pw=document.getElementById("loginPassword").value;
 const user=db.users.find(u=>(u.email===id||u.name.toLowerCase()===id)&&u.password===pw);
 if(!user){alert("Account not found or password incorrect. Create an account if you have not registered.");return;}
 currentUser=user;
 if(document.getElementById("remember").checked)localStorage.setItem("smartAttendAI_last",user.email);
 else localStorage.removeItem("smartAttendAI_last");
 enterApp();
}
function forgotPassword(){
 const email=prompt("Enter the email address you registered with:");
 if(!email)return;
 const user=db.users.find(u=>u.email===email.trim().toLowerCase());
 if(!user){alert("No account was found for that email.");return;}
 alert("For this demonstration, contact your school administrator to reset your password. Password reset emails are not configured.");
}
function enterApp(){
 document.getElementById("loginScreen").classList.add("hidden");
 document.getElementById("app").classList.remove("hidden");
 document.getElementById("teacherGreeting").textContent=currentUser.name;
 const hour=new Date().getHours();
 document.getElementById("greeting").textContent=hour<12?"Good Morning,":hour<17?"Good Afternoon,":"Good Evening,";
 document.getElementById("todayDate").textContent=new Date().toLocaleDateString("en-IN",{day:"numeric",month:"long",year:"numeric"});
 refreshAll();navigate("dashboard");
}
function logout(){
 stopCamera();
 currentUser=null;
 document.getElementById("app").classList.add("hidden");
 document.getElementById("loginScreen").classList.remove("hidden");
 document.getElementById("loginPassword").value="";
 showLogin();
}
function navigate(id,btn){
 stopCamera();
 document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
 document.getElementById(id)?.classList.add("active");
 document.querySelectorAll(".nav[data-page]").forEach(n=>n.classList.toggle("active",n.dataset.page===id));
 if(btn?.dataset?.page)btn.classList.add("active");
 if(id==="dashboard")renderDashboard();
 if(id==="students")renderStudents();
 if(id==="attendance")renderSessionList();
 if(id==="alerts")renderAlerts();
}
function toggleReports(){document.getElementById("reportNav").classList.toggle("hidden");}
function openReport(type,btn){
 currentReport=type;
 document.getElementById("reportTitle").textContent=type[0].toUpperCase()+type.slice(1)+" Attendance Report";
 document.getElementById("repDateWrap").classList.toggle("hidden",type!=="daily");
 document.getElementById("repMonthWrap").classList.toggle("hidden",type!=="monthly");
 document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
 document.getElementById("reports").classList.add("active");
 document.querySelectorAll(".nav[data-page]").forEach(n=>n.classList.remove("active"));
 renderReport();
}

function getRecord(studentId,date){return db.records.find(r=>r.studentId===studentId&&r.date===date);}
function upsertRecord(studentId,date,status,source="manual"){
 const i=db.records.findIndex(r=>r.studentId===studentId&&r.date===date);
 const record={studentId,date,status,source,updatedAt:new Date().toISOString(),user:currentUser?.email||""};
 if(i>=0)db.records[i]=record;else db.records.push(record);
 saveDB();
}
function getSessionStudents(){
 const c=document.getElementById("attClass").value;
 const stream=document.getElementById("attStream").value;
 const sec=document.getElementById("attSection").value;
 return db.students.filter(s=>s.className===c&&(!isSenior(c)||s.stream===stream)&&s.section===sec).sort(sortStudents);
}
function renderSessionList(){
 const list=getSessionStudents();
 const date=document.getElementById("attDate").value||today();
 document.getElementById("sessionList").innerHTML=list.length?list.map(s=>{
  const r=getRecord(s.id,date);
  return `<p>${escapeHTML(s.name)}<br><small>${escapeHTML(s.admission)} · </small><span class="pill ${r?.status==="Absent"?"absent":""}">${r?.status||"Not marked"}</span></p>`;
 }).join(""):'<p>No registered students in this class and section. Add students first.</p>';
 const m=document.getElementById("manualStudent");
 m.innerHTML=list.map(s=>`<option value="${s.id}">${escapeHTML(s.name)} — ${escapeHTML(s.admission)}</option>`).join("");
}
function manualPresent(){
 const id=document.getElementById("manualStudent").value;
 if(!id){alert("No student available. Add a student first.");return;}
 upsertRecord(id,document.getElementById("attDate").value||today(),"Present","manual");
 renderSessionList();renderDashboard();
}
function markPresent(student,source="face"){
 const date=document.getElementById("attDate").value||today();
 const old=getRecord(student.id,date);
 if(old?.status==="Present")return;
 upsertRecord(student.id,date,"Present",source);
 document.getElementById("cameraStatus").textContent=`Recognized: ${student.name} (${student.admission}) — marked Present.`;
 renderSessionList();renderDashboard();
}
async function loadFaceModels(){
 if(faceModelsReady)return true;
 if(!window.faceapi)throw new Error("Face recognition library did not load. Check your internet connection and refresh.");
 if(!faceModelPromise){
  faceModelPromise=Promise.all([
   faceapi.nets.tinyFaceDetector.loadFromUri(MODEL_URL),
   faceapi.nets.faceLandmark68Net.loadFromUri(MODEL_URL),
   faceapi.nets.faceRecognitionNet.loadFromUri(MODEL_URL)
  ]).then(()=>{faceModelsReady=true;return true;}).catch(e=>{faceModelPromise=null;throw e;});
 }
 return faceModelPromise;
}
async function startCamera(){
 if(cameraRunning)return;
 const students=getSessionStudents();
 if(!students.length){alert("Register at least one student in this class and section first.");return;}
 try{
  document.getElementById("cameraStatus").textContent="Loading face-recognition models…";
  await loadFaceModels();
  cameraStream=await navigator.mediaDevices.getUserMedia({video:{facingMode:"user"},audio:false});
  const video=document.getElementById("video");
  video.srcObject=cameraStream;
  await new Promise(resolve=>video.onloadedmetadata=resolve);
  await video.play();
  cameraRunning=true;
  session={date:document.getElementById("attDate").value||today(),className:document.getElementById("attClass").value,stream:document.getElementById("attStream").value,section:document.getElementById("attSection").value};
  recognizedInSession=new Set();
  document.getElementById("cameraBox").classList.remove("hidden");
  document.getElementById("cameraStatus").textContent="Camera running. Keep one student in front of the camera at a time.";
  runDetection();
 }catch(e){
  stopCamera();
  document.getElementById("cameraStatus").textContent="Camera/model error: "+e.message;
  alert("Could not start face recognition. Open this site on HTTPS, allow camera access, and check your internet connection.");
 }
}
function stopCamera(){
 cameraRunning=false;
 if(videoTimer){clearTimeout(videoTimer);videoTimer=null;}
 if(cameraStream){cameraStream.getTracks().forEach(t=>t.stop());cameraStream=null;}
 const video=document.getElementById("video");if(video)video.srcObject=null;
 const canvas=document.getElementById("overlay");if(canvas)canvas.getContext("2d").clearRect(0,0,canvas.width,canvas.height);
 document.getElementById("cameraBox")?.classList.add("hidden");
}
async function runDetection(){
 if(!cameraRunning||detectionBusy)return;
 detectionBusy=true;
 const video=document.getElementById("video"),canvas=document.getElementById("overlay");
 try{
  if(video.readyState>=2){
   const size={width:video.videoWidth,height:video.videoHeight};
   if(size.width&&size.height){
    canvas.width=size.width;canvas.height=size.height;
    const ctx=canvas.getContext("2d");ctx.clearRect(0,0,canvas.width,canvas.height);
    const results=await faceapi.detectAllFaces(video,new faceapi.TinyFaceDetectorOptions({inputSize:320,scoreThreshold:0.5})).withFaceLandmarks().withFaceDescriptors();
    const resized=faceapi.resizeResults(results,size);
    const students=getSessionStudents().filter(s=>Array.isArray(s.descriptor)&&s.descriptor.length===128);
    resized.forEach((d,i)=>{
     const box=d.detection.box;
     let best=null,bestDistance=Infinity;
     for(const s of students){
      const distance=faceapi.euclideanDistance(d.descriptor,new Float32Array(s.descriptor));
      if(distance<bestDistance){bestDistance=distance;best=s;}
     }
     const matched=best&&bestDistance<0.48?best:null;
     const color=matched?"#22d36b":"#ff3434";
     ctx.strokeStyle=color;ctx.lineWidth=4;ctx.strokeRect(box.x,box.y,box.width,box.height);
     ctx.fillStyle=color;
     const label=matched?`${matched.name} | ${matched.admission}`:"UNKNOWN";
     ctx.font="bold 16px Arial";
     const tw=Math.min(ctx.measureText(label).width+14,canvas.width-box.x);
     ctx.fillRect(box.x,Math.max(0,box.y-27),tw,27);
     ctx.fillStyle="#ffffff";ctx.fillText(label,box.x+6,Math.max(19,box.y-8));
     if(matched){
      const now=Date.now();
      if(!recognizedInSession.has(matched.id)&&now-(lastRecognizedAt[matched.id]||0)>4000){
       recognizedInSession.add(matched.id);lastRecognizedAt[matched.id]=now;
       markPresent(matched,"face");
      }
     }
    });
    if(!results.length)document.getElementById("cameraStatus").textContent="Looking for a face… Stand in front of the camera.";
   }
  }
 }catch(e){document.getElementById("cameraStatus").textContent="Recognition issue: "+e.message;}
 finally{detectionBusy=false;if(cameraRunning)videoTimer=setTimeout(runDetection,450);}
}
async function getDescriptor(file){
 await loadFaceModels();
 const img=await faceapi.bufferToImage(file);
 const result=await faceapi.detectSingleFace(img,new faceapi.TinyFaceDetectorOptions({inputSize:320,scoreThreshold:0.4})).withFaceLandmarks().withFaceDescriptor();
 if(!result)throw new Error("No clear face detected in this photo. Please choose a front-facing photo with good lighting.");
 return Array.from(result.descriptor);
}
function previewPhoto(event){
 const file=event.target.files[0],img=document.getElementById("photoPreview");
 if(!file)return;
 if(!file.type.startsWith("image/")){alert("Please select an image.");event.target.value="";return;}
 if(file.size>2*1024*1024){alert("Please choose a photo smaller than 2 MB.");event.target.value="";return;}
 img.src=URL.createObjectURL(file);img.style.display="block";
}
function showAddStudent(){
 document.getElementById("studentForm").reset();
 document.getElementById("photoPreview").style.display="none";
 document.getElementById("faceStatus").textContent="A clear face photo is required for facial recognition.";
 navigate("addStudent");
}
async function saveStudent(event){
 event.preventDefault();
 const name=document.getElementById("studentName").value.trim();
 const admission=document.getElementById("studentAdmission").value.trim();
 const roll=document.getElementById("studentRoll").value.trim();
 const className=document.getElementById("studentClass").value;
 const stream=isSenior(className)?document.getElementById("studentStream").value:"";
 const section=document.getElementById("studentSection").value;
 const phone=document.getElementById("studentPhone").value.trim();
 const file=document.getElementById("studentPhoto").files[0];
 if(db.students.some(s=>s.admission.toLowerCase()===admission.toLowerCase())){alert("Admission number already exists.");return;}
 if(db.students.some(s=>s.className===className&&s.section===section&&s.roll.toLowerCase()===roll.toLowerCase())){alert("This roll number already exists in the selected class and section.");return;}
 if(!file){alert("Please select a student photo.");return;}
 const status=document.getElementById("faceStatus");
 status.textContent="Preparing the student's face data…";
 try{
  const descriptor=await getDescriptor(file);
  const photo=await compressPhoto(file);
  db.students.push({id:crypto.randomUUID(),name,admission,roll,className,stream,section,phone,photo,descriptor,createdAt:today()});
  saveDB();alert("Student registered successfully. Face recognition is ready.");
  refreshAll();navigate("students");
 }catch(e){
  status.textContent=e.message;
  alert("Student was not saved: "+e.message);
 }
}
function compressPhoto(file){
 return new Promise((resolve,reject)=>{
  const img=new Image(),url=URL.createObjectURL(file);
  img.onload=()=>{
   const canvas=document.createElement("canvas");
   const scale=Math.min(1,320/Math.max(img.width,img.height));
   canvas.width=Math.round(img.width*scale);canvas.height=Math.round(img.height*scale);
   canvas.getContext("2d").drawImage(img,0,0,canvas.width,canvas.height);
   URL.revokeObjectURL(url);resolve(canvas.toDataURL("image/jpeg",0.65));
  };
  img.onerror=reject;img.src=url;
 });
}
async function finishAttendance(){
 const list=getSessionStudents(),date=document.getElementById("attDate").value||today();
 if(!list.length){alert("There are no registered students in this class and section.");return;}
 if(!confirm(`Finish attendance for ${list[0].className} ${list[0].section} on ${fmtDate(date)}? All remaining unmarked students will be marked Absent.`))return;
 stopCamera();
 list.forEach(s=>{if(!getRecord(s.id,date))upsertRecord(s.id,date,"Absent","session-finish");});
 db.sessions.push({date,className:document.getElementById("attClass").value,stream:document.getElementById("attStream").value,section:document.getElementById("attSection").value,finishedBy:currentUser?.email});
 saveDB();session=null;renderSessionList();refreshAll();
 alert("Attendance session finished successfully.");navigate("attendance");
}
function attendancePercent(s,upto=today()){
 const days=new Set(db.records.filter(r=>r.studentId===s.id&&r.date<=upto).map(r=>r.date));
 const present=db.records.filter(r=>r.studentId===s.id&&r.date<=upto&&r.status==="Present").length;
 return days.size?Math.round(present/days.size*100):0;
}
function renderStudents(){
 const students=studentFilter("stuClass","stuStream","stuSection").filter(s=>{
  const q=document.getElementById("stuSearch").value.toLowerCase();
  return s.name.toLowerCase().includes(q)||s.admission.toLowerCase().includes(q);
 });
 document.getElementById("studentTable").innerHTML=students.length?`<table><thead><tr><th>Admission Number</th><th>Roll Number</th><th>Student Name</th><th>Class</th><th>Section</th><th>Attendance %</th><th>Action</th></tr></thead><tbody>${students.map(s=>{
 const p=attendancePercent(s);return `<tr class="${p<75?'low-row':''}"><td>${escapeHTML(s.admission)}</td><td>${escapeHTML(s.roll)}</td><td>${escapeHTML(s.name)}</td><td>${escapeHTML(s.className)}</td><td>${escapeHTML(s.section)}</td><td><span class="pill ${p<75?'absent':''}">${p}%</span></td><td><button class="btn danger" onclick="deleteStudent('${s.id}')">Delete Record</button></td></tr>`;
 }).join("")}</tbody></table>`:"<p>No students found. Click Add Student to register your students.</p>";
 document.getElementById("studentSummary").innerHTML=`<strong>Total students: ${students.length}</strong><span class="green">Above 75%: ${students.filter(s=>attendancePercent(s)>=75).length}</span><span class="red">Below 75%: ${students.filter(s=>attendancePercent(s)<75).length}</span>`;
}
function deleteStudent(id){
 const s=db.students.find(x=>x.id===id);if(!s)return;
 const code=prompt("Enter the school access code to delete this student record:");
 if(!code||code.replace(/\s/g,"").toUpperCase()!==ACCESS_CODE){alert("Incorrect school access code. Record was not deleted.");return;}
 if(!confirm(`Permanently delete ${s.name} and their attendance records from this browser?`))return;
 db.students=db.students.filter(x=>x.id!==id);
 db.records=db.records.filter(r=>r.studentId!==id);
 saveDB();refreshAll();
}
function getDayRecords(date,students=db.students){
 return students.map(s=>({s,r:getRecord(s.id,date)}));
}
function renderDashboard(){
 const date=today(),records=getDayRecords(date);
 const present=records.filter(x=>x.r?.status==="Present").length;
 const absent=records.filter(x=>x.r?.status==="Absent").length;
 const marked=present+absent,rate=marked?Math.round(present/marked*100):0;
 document.getElementById("totalStudents").textContent=db.students.length;
 document.getElementById("presentToday").textContent=present;
 document.getElementById("absentToday").textContent=absent;
 document.getElementById("classesToday").textContent=new Set(db.sessions.filter(s=>s.date===date).map(s=>s.className+"|"+s.section)).size;
 document.getElementById("donutGreen").setAttribute("stroke-dasharray",`${421*rate/100} 421`);
 document.getElementById("donutPercent").textContent=rate+"%";
 document.getElementById("ringPresent").textContent=present;
 document.getElementById("ringAbsent").textContent=absent;
 document.getElementById("classSummary").innerHTML=CLASSES.map(c=>{
  const students=db.students.filter(s=>s.className===c);
  if(!students.length)return "";
  const p=students.filter(s=>getRecord(s.id,date)?.status==="Present").length;
  const a=students.filter(s=>getRecord(s.id,date)?.status==="Absent").length;
  return `<p style="display:flex;justify-content:space-between;gap:10px;border-bottom:1px solid var(--line);padding:7px 0"><span>${escapeHTML(c)}</span><span class="green">${p} Present</span><span class="red">${a} Absent</span><span>${students.length} Total</span></p>`;
 }).join("")||"<p>No students registered yet.</p>";
}
function renderAlerts(){
 const c=document.getElementById("alertClass").value,q=document.getElementById("alertSearch").value.toLowerCase();
 const all=db.students.filter(s=>attendancePercent(s)<75);
 const filtered=all.filter(s=>(c==="All"||s.className===c)&&(s.name.toLowerCase().includes(q)||s.admission.toLowerCase().includes(q))).sort(sortStudents);
 document.getElementById("alertCount").textContent=all.length;
 document.getElementById("alertTable").innerHTML=filtered.length?`<table><thead><tr><th>Admission Number</th><th>Roll Number</th><th>Student Name</th><th>Class</th><th>Section</th><th>Attendance %</th></tr></thead><tbody>${filtered.map(s=>`<tr class="low-row"><td>${escapeHTML(s.admission)}</td><td>${escapeHTML(s.roll)}</td><td>${escapeHTML(s.name)}</td><td>${escapeHTML(s.className)}</td><td>${escapeHTML(s.section)}</td><td><span class="pill absent">${attendancePercent(s)}%</span></td></tr>`).join("")}</tbody></table>`:"<p>No students currently match this alert filter. Students with no recorded attendance are shown at 0%.</p>";
}
function reportDates(){
 const date=document.getElementById("repDate").value||today();
 if(currentReport==="daily")return [date];
 if(currentReport==="monthly"){
  const m=Number(document.getElementById("repMonth").value),year=Number(date.slice(0,4));
  const prefix=`${year}-${String(m+1).padStart(2,"0")}-`;
  return Array.from({length:new Date(year,m+1,0).getDate()},(_,i)=>prefix+String(i+1).padStart(2,"0"));
 }
 const d=new Date(date+"T12:00:00"),day=(d.getDay()+6)%7;
 const monday=new Date(d);monday.setDate(d.getDate()-day);
 return Array.from({length:7},(_,i)=>{const x=new Date(monday);x.setDate(monday.getDate()+i);return x.toLocaleDateString("en-CA");});
}
function renderReport(){
 const students=studentFilter("repClass","repStream","repSection"),dates=reportDates();
 let rows=students.map(s=>{
  const present=dates.filter(d=>getRecord(s.id,d)?.status==="Present").length;
  const absent=dates.filter(d=>getRecord(s.id,d)?.status==="Absent").length;
  return {s,present,absent,days:present+absent,pct:present+absent?Math.round(present/(present+absent)*100):0,dates};
 });
 document.getElementById("reportTable").innerHTML=rows.length?`<table><thead><tr><th>Admission Number</th><th>Roll Number</th><th>Student Name</th><th>Class</th><th>Section</th>${currentReport==="daily"?"<th>Attendance Status</th>":`<th>Days Present</th><th>Days Absent</th><th>Recorded Days</th><th>Attendance %</th>`}</tr></thead><tbody>${rows.map(x=>`<tr><td>${escapeHTML(x.s.admission)}</td><td>${escapeHTML(x.s.roll)}</td><td>${escapeHTML(x.s.name)}</td><td>${escapeHTML(x.s.className)}</td><td>${escapeHTML(x.s.section)}</td>${currentReport==="daily"?`<td><span class="pill ${getRecord(x.s.id,dates[0])?.status==="Absent"?'absent':''}">${getRecord(x.s.id,dates[0])?.status||"Not marked"}</span></td>`:`<td>${x.present}</td><td>${x.absent}</td><td>${x.days}</td><td>${x.pct}%</td>`}</tr>`).join("")}</tbody></table>`:"<p>No registered students in this selection.</p>";
 const p=rows.reduce((n,x)=>n+x.present,0),a=rows.reduce((n,x)=>n+x.absent,0);
 document.getElementById("reportSummary").innerHTML=`<strong>Total Students: ${rows.length}</strong><span class="green">Present: ${p}</span><span class="red">Absent: ${a}</span><span>Recorded attendance: ${p+a?Math.round(p/(p+a)*100):0}%</span>`;
}
function exportReport(){
 const students=studentFilter("repClass","repStream","repSection"),dates=reportDates();
 const header=["Admission Number","Roll Number","Student Name","Class","Stream","Section",...dates.map(d=>fmtDate(d)),"Days Present","Days Absent","Attendance %"];
 const rows=students.map(s=>{
  const statuses=dates.map(d=>getRecord(s.id,d)?.status||"Not marked");
  const p=statuses.filter(x=>x==="Present").length,a=statuses.filter(x=>x==="Absent").length;
  return [s.admission,s.roll,s.name,s.className,s.stream,s.section,...statuses,p,a,p+a?Math.round(p/(p+a)*100)+"%":"0%"];
 });
 downloadCSV([header,...rows],`SmartAttendAI-${currentReport}-${today()}.csv`);
}
function downloadCSV(rows,name){
 const csv="\uFEFF"+rows.map(row=>row.map(v=>'"'+String(v??"").replace(/"/g,'""')+'"').join(",")).join("\r\n");
 const blob=new Blob([csv],{type:"text/csv;charset=utf-8;"});
 const url=URL.createObjectURL(blob),a=document.createElement("a");
 a.href=url;a.download=name;a.click();URL.revokeObjectURL(url);
}
function importStudents(event){
 const file=event.target.files[0];if(!file)return;
 const reader=new FileReader();
 reader.onload=()=>{
  const lines=String(reader.result).split(/\r?\n/).filter(x=>x.trim());
  if(lines.length<2){alert("CSV has no student rows.");return;}
  const parse=line=>line.split(",").map(x=>x.trim().replace(/^"|"$/g,""));
  const headers=parse(lines[0]).map(x=>x.toLowerCase());
  const index=names=>headers.findIndex(h=>names.includes(h));
  const ix={name:index(["name","student name","fullname"]),admission:index(["admission","admission number","admission no"]),roll:index(["roll","roll number"]),className:index(["class","class name"]),section:index(["section"]),stream:index(["stream"])};
  if(ix.name<0||ix.admission<0||ix.className<0||ix.section<0){alert("CSV needs columns for name, admission number, class and section. Photos and face data must be added through Add Student.");return;}
  let added=0,skipped=0;
  for(const line of lines.slice(1)){
   const v=parse(line),name=v[ix.name],admission=v[ix.admission],className=v[ix.className],section=v[ix.section];
   if(!name||!admission||!CLASSES.includes(className)||!["A","B","C","D"].includes(section)||db.students.some(s=>s.admission.toLowerCase()===admission.toLowerCase())){skipped++;continue;}
   db.students.push({id:crypto.randomUUID(),name,admission,roll:ix.roll<0?"":v[ix.roll],className,stream:ix.stream<0?"":v[ix.stream],section,phone:"",photo:"",descriptor:[],createdAt:today()});added++;
  }
  saveDB();refreshAll();alert(`Imported ${added} records. Skipped ${skipped}. Imported records need a face photo registered through Add Student before camera recognition can identify them.`);
  event.target.value="";
 };
 reader.readAsText(file);
}
function refreshAll(){
 renderDashboard();renderStudents();renderAlerts();renderSessionList();
 if(document.getElementById("reports").classList.contains("active"))renderReport();
}
initSelects();
const remembered=localStorage.getItem("smartAttendAI_last");
if(remembered)document.getElementById("loginIdentity").value=remembered;
</script>
</body>
</html>
