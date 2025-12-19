<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Techview Task - Online Business Platform</title>
<style>
body {font-family: Arial, sans-serif; margin:0; background:#f5f5f5; color:#222;}
header {background:#004080; color:#fff; padding:10px 20px;}
nav a, nav button {color:#fff; margin:0 8px; text-decoration:none; background:none; border:none; cursor:pointer;}
section {display:none; padding:20px;}
.active {display:block;}
button, .btn {background:#004080; color:#fff; border:none; padding:8px 14px; cursor:pointer; border-radius:5px;}
.btn {text-decoration:none;}
input {display:block; margin:8px 0; padding:8px; width:250px;}
.table {width:100%; border-collapse:collapse;}
.table th, .table td {border:1px solid #ccc; padding:6px;}
footer {text-align:center; background:#eee; padding:10px; margin-top:20px;}
.whatsapp-float {position:fixed; bottom:15px; right:15px; width:50px;}
.whatsapp-float img {width:50px;}
.profile-card {text-align:center;}
.profile-card img {width:100px; height:100px; border-radius:50%; margin:10px;}
.faq {background:#fff; margin:10px 0; padding:10px; border-radius:5px;}
</style>
</head>
<body onload="showSection('home')">

<header>
  <h1>Techview Task</h1>
  <nav>
    <a onclick="showSection('home')">Home</a>
    <a onclick="showSection('register')">Register</a>
    <a onclick="showSection('login')">Login</a>
    <a onclick="showSection('dashboard')">Dashboard</a>
    <a onclick="showSection('admin')">Admin</a>
    <a onclick="showSection('support')">Support</a>
  </nav>
</header>

<!-- Home -->
<section id="home" class="active">
  <h2>Welcome to Techview Task</h2>
  <p>Join our online earning platform. Activate your account with a one-time fee of KES 150 via Till No. 4577904.</p>
  <button onclick="showSection('register')">Get Started</button>
</section>

<!-- Register -->
<section id="register">
  <h2>Register & Activate Account</h2>
  <p>Pay activation fee KES 150 to M-Pesa Till No. <strong>4577904</strong> before registration.</p>
  <form onsubmit="registerUser(event)">
    <input type="text" id="regName" placeholder="Full Name" required />
    <input type="email" id="regEmail" placeholder="Email" required />
    <input type="password" id="regPass" placeholder="Password" required />
    <button type="submit">Activate & Register</button>
  </form>
</section>

<!-- Login -->
<section id="login">
  <h2>Login</h2>
  <form onsubmit="loginUser(event)">
    <input type="email" id="logEmail" placeholder="Email" required />
    <input type="password" id="logPass" placeholder="Password" required />
    <button type="submit">Login</button>
  </form>
</section>

<!-- Dashboard -->
<section id="dashboard">
  <h2>User Dashboard</h2>
  <p>Welcome, <span id="userName"></span></p>
  <p>Your fake balance: <strong>KES <span id="balance">0</span></strong></p>
  <button onclick="increaseFakeEarnings()">Simulate Daily Earnings</button>
  <p><a onclick="showSection('referrals')" class="btn">Referrals</a></p>
  <p><a onclick="showSection('payments')" class="btn">Payment History</a></p>
  <p><a onclick="showSection('profile')" class="btn">Profile</a></p>
  <p><a onclick="logout()" class="btn">Logout</a></p>
</section>

<!-- Referrals -->
<section id="referrals">
  <h2>My Referrals</h2>
  <p>Welcome, <span id="refUser"></span></p>
  <p>You have <strong><span id="refCount">0</span></strong> referrals.</p>
  <ul id="refList"></ul>
  <button onclick="addReferral()">Add Fake Referral</button>
</section>

<!-- Payments -->
<section id="payments">
  <h2>Payment History</h2>
  <table class="table">
    <thead><tr><th>Date</th><th>Type</th><th>Amount</th><th>Status</th></tr></thead>
    <tbody id="payTable"></tbody>
  </table>
</section>

<!-- Profile -->
<section id="profile">
  <h2>My Profile</h2>
  <div class="profile-card">
    <img id="profilePic" src="https://cdn-icons-png.flaticon.com/512/149/149071.png" alt="Profile" />
    <input type="file" id="uploadPic" accept="image/*" onchange="updateProfilePic(event)" />
    <h3 id="profileName"></h3>
    <p id="profileEmail"></p>
    <p>Status: <strong>Active</strong></p>
    <form onsubmit="updateProfile(event)">
      <input id="newName" placeholder="New Name" />
      <input id="newEmail" placeholder="New Email" />
      <input id="newPass" placeholder="New Password" />
      <button type="submit">Save Changes</button>
    </form>
  </div>
</section>

<!-- Admin -->
<section id="admin">
  <h2>Admin Panel</h2>
  <form onsubmit="adminLogin(event)">
    <input id="adminUser" placeholder="Username" required />
    <input id="adminPass" type="password" placeholder="Password" required />
    <button type="submit">Login as Admin</button>
  </form>
  <div id="adminArea" style="display:none;">
    <h3>Welcome Admin</h3>
    <p>All user withdrawals must be approved here manually.</p>
    <ul id="userList"></ul>
  </div>
</section>

<!-- Support -->
<section id="support">
  <h2>Support & FAQs</h2>
  <div class="faq"><h4>How to Activate?</h4><p>Pay KES 150 to Till No. 4577904 and register.</p></div>
  <div class="faq"><h4>Withdrawals?</h4><p>Pay KES 1000 withdrawal fee → admin approves manually.</p></div>
  <div class="faq"><h4>Referrals?</h4><p>Each referral adds KES 50 to your balance.</p></div>
  <div class="faq"><h4>Contact?</h4><p>Chat on WhatsApp +254701059192</p><a href="https://wa.me/254701059192" target="_blank" class="btn">WhatsApp Support</a></div>
</section>

<footer><p>© 2025 Techview Task</p></footer>
<a href="https://wa.me/254701059192" class="whatsapp-float" target="_blank">
<img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WA" /></a>

<script>
// Page switching
function showSection(id){
  document.querySelectorAll('section').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// Registration
function registerUser(e){
  e.preventDefault();
  const name=document.getElementById('regName').value;
  const email=document.getElementById('regEmail').value;
  const pass=document.getElementById('regPass').value;
  localStorage.setItem('user',JSON.stringify({name,email,pass,balance:0}));
  record('Account Activation',150);
  alert('Registration successful!');
  showSection('login');
}

// Login
function loginUser(e){
  e.preventDefault();
  const email=document.getElementById('logEmail').value;
  const pass=document.getElementById('logPass').value;
  const user=JSON.parse(localStorage.getItem('user'));
  if(user && user.email===email && user.pass===pass){
    document.getElementById('userName').innerText=user.name;
    showSection('dashboard');
    loadPayments();
  } else alert('Invalid credentials!');
}

// Dashboard
function increaseFakeEarnings(){
  let user=JSON.parse(localStorage.getItem('user'));
  let add=Math.floor(Math.random()*400)+100;
  user.balance+=add;
  document.getElementById('balance').innerText=user.balance;
  localStorage.setItem('user',JSON.stringify(user));
  record('Daily Earnings',add);
}

// Referrals
function loadReferrals(){
  const user=JSON.parse(localStorage.getItem('user'));
  document.getElementById('refUser').innerText=user.name;
  const r=JSON.parse(localStorage.getItem('refs'))||[];
  document.getElementById('refCount').innerText=r.length;
  document.getElementById('refList').innerHTML=r.map(x=>`<li>${x}</li>`).join('');
}
function addReferral(){
  const names=['Chris','Mary','Odongo','Faith','Amina','Joseph'];
  const n=names[Math.floor(Math.random()*names.length)];
  const r=JSON.parse(localStorage.getItem('refs'))||[];
  r.push(n); localStorage.setItem('refs',JSON.stringify(r));
  let u=JSON.parse(localStorage.getItem('user')); u.balance+=50; localStorage.setItem('user',JSON.stringify(u));
  record('Referral Bonus',50); alert(`${n} joined! +KES 50`); loadReferrals();
}

// Payments
function record(type,amt,status='Successful'){
  const tx=JSON.parse(localStorage.getItem('tx'))||[];
  tx.push({date:new Date().toLocaleString(),type,amt,status});
  localStorage.setItem('tx',JSON.stringify(tx));
}
function loadPayments(){
  const tx=JSON.parse(localStorage.getItem('tx'))||[];
  document.getElementById('payTable').innerHTML=tx.map(t=>`<tr><td>${t.date}</td><td>${t.type}</td><td>${t.amt}</td><td>${t.status}</td></tr>`).join('');
}

// Profile
function loadProfile(){
  const u=JSON.parse(localStorage.getItem('user'));
  if(!u){alert('Login first');showSection('login');return;}
  document.getElementById('profileName').innerText=u.name;
  document.getElementById('profileEmail').innerText=u.email;
  const pic=localStorage.getItem('profilePic');
  if(pic) document.getElementById('profilePic').src=pic;
}
function updateProfile(e){
  e.preventDefault();
  let u=JSON.parse(localStorage.getItem('user'));
  const n=document.getElementById('newName').value;
  const em=document.getElementById('newEmail').value;
  const p=document.getElementById('newPass').value;
  if(n)u.name=n;if(em)u.email=em;if(p)u.pass=p;
  localStorage.setItem('user',JSON.stringify(u));alert('Profile updated!');loadProfile();
}
function updateProfilePic(e){
  const r=new FileReader();
  r.onload=function(){localStorage.setItem('profilePic',r.result);document.getElementById('profilePic').src=r.result;};
  r.readAsDataURL(e.target.files[0]);
}

// Admin
function adminLogin(e){
  e.preventDefault();
  const u=document.getElementById('adminUser').value;
  const p=document.getElementById('adminPass').value;
  if(u==='odhiambo40' && p==='47ty7890@CHRIS'){
    document.getElementById('adminArea').style.display='block';
    const user=JSON.parse(localStorage.getItem('user'));
    document.getElementById('userList').innerHTML=`<li>${user?user.name:'No users'} - Balance: KES ${user?user.balance:0}</li>`;
  } else alert('Access Denied');
}

// Logout
function logout(){localStorage.removeItem('user');alert('Logged out!');showSection('home');}
</script>
</body>
</html>
