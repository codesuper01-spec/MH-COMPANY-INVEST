<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>MH INVEST</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#101010;color:#fff;font-family:Arial,sans-serif}
:root{--gold:#dfb75f;--panel:#1d1d1d;--line:#594625}
header{background:#171717;border-bottom:1px solid var(--line);padding:17px;display:flex;justify-content:space-between;align-items:center}
.logo{font-size:22px;font-weight:bold;color:var(--gold)}
main{max-width:850px;margin:auto;padding:15px}
nav{display:flex;gap:7px;overflow-x:auto;padding:12px;background:#171717}
button{background:var(--gold);color:#17120a;border:0;border-radius:8px;padding:12px 15px;font-weight:bold;cursor:pointer}
nav button{white-space:nowrap}
.secondary{background:#303030;color:white}
input,select,textarea{width:100%;padding:13px;margin:7px 0;background:#292929;color:white;border:1px solid #67532f;border-radius:8px}
.card{background:var(--panel);border:1px solid var(--line);padding:18px;border-radius:13px;margin:13px 0}
h2,h3{color:var(--gold)}
small,.muted{color:#aaa}
.page{display:none}
.page.active{display:block}
.grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
.tile{background:#282319;padding:18px;border-radius:10px;border:1px solid #4b3c23}
.money{font-size:32px;color:var(--gold)}
.tag{color:var(--gold);font-size:13px}
.notice{background:#292319;border-left:3px solid var(--gold);padding:12px;color:#d7c69d;border-radius:5px;font-size:13px}
footer{text-align:center;padding:25px;color:#888}
.hidden{display:none!important}
button:disabled{opacity:.4}
@media(max-width:520px){.grid{grid-template-columns:1fr 1fr}header{gap:8px}.logo{font-size:18px}}
</style>
</head>
<body>

<header>
 <div class="logo">♛ MH INVEST</div>
 <button class="secondary" onclick="logout()">Logout</button>
</header>

<nav>
 <button onclick="show('home')">Home</button>
 <button onclick="show('account')">Account</button>
 <button onclick="show('kyc')">KYC</button>
 <button onclick="show('deposit')">Deposit</button>
 <button onclick="show('withdraw')">Withdraw</button>
 <button onclick="show('plans')">Invest</button>
 <button onclick="show('history')">History</button>
 <button onclick="show('support')">Support</button>
 <button onclick="show('admin')">Admin</button>
</nav>

<main>

<section id="login" class="page active">
 <div class="card">
  <h2>Welcome to MH INVEST</h2>
  <p class="muted">Login to your account</p>
  <input id="loginPhone" placeholder="Mobile number" inputmode="numeric">
  <input id="loginPass" type="password" placeholder="Password">
  <button onclick="login()">Login</button>
  <hr style="border-color:#514124;margin:22px 0">
  <h3>Create New Account</h3>
  <input id="regPhone" placeholder="01XXXXXXXXX" inputmode="numeric">
  <input id="regPass" type="password" placeholder="Create password">
  <button onclick="register()">Register</button>
  <p id="authMsg" class="muted"></p>
  <div class="notice">Demo only: real account creation and OTP require a secure backend.</div>
 </div>
</section>

<section id="home" class="page">
 <div class="card">
  <small>WALLET BALANCE</small>
  <div class="money">৳ <span id="balance">0.00</span></div>
  <p class="tag" id="status">Account status: Not verified</p>
 </div>
 <div class="grid">
  <div class="tile" onclick="show('deposit')">💳<h3>Deposit</h3><small>Payment request</small></div>
  <div class="tile" onclick="show('withdraw')">💰<h3>Withdraw</h3><small>Withdrawal request</small></div>
  <div class="tile" onclick="show('plans')">📈<h3>Investment</h3><small>Available plans</small></div>
  <div class="tile" onclick="show('kyc')">🛡️<h3>Verification</h3><small>Account KYC</small></div>
 </div>
 <div class="card">
  <h3>My Account</h3>
  <p>Mobile: <span id="homePhone">Not logged in</span></p>
  <p>KYC: <span id="homeKyc">Not submitted</span></p>
  <p class="muted">Investment returns are not guaranteed. Capital may be at risk.</p>
 </div>
</section>

<section id="account" class="page">
 <div class="card">
  <h2>My Account</h2>
  <p>Mobile: <b id="accountPhone">-</b></p>
  <p>Mobile verification: <span id="mobileStatus">Pending</span></p>
  <p>KYC status: <span id="kycStatus">Pending</span></p>
  <p>Account status: <span id="accountStatus">Unverified</span></p>
  <button onclick="show('kyc')">Complete KYC</button>
 </div>
</section>

<section id="kyc" class="page">
 <div class="card">
  <h2>KYC Verification</h2>
  <p class="muted">Identity verification application</p>
  <input id="legalName" placeholder="Full legal name">
  <input id="birthDate" type="date">
  <select id="country"><option>Bangladesh</option></select>
  <div class="notice">
   Required verification documents: NID front and back, Passport identity page and Selfie.
   Real uploads must use private encrypted storage and an authorized KYC service.
  </div>
  <p class="muted">Document upload is not enabled in this frontend demo. Do not enter real NID or passport information here.</p>
  <label><input type="checkbox" id="agree" style="width:auto"> I agree to the privacy policy.</label>
  <button onclick="submitKyc()">Submit Application</button>
  <p id="kycMsg" class="muted"></p>
 </div>
</section>

<section id="deposit" class="page">
 <div class="card">
  <h2>Deposit</h2>
  <select id="depMethod">
   <option>bKash</option><option>Nagad</option>
  </select>
  <input id="depAmount" type="number" placeholder="Amount (BDT)">
  <input id="depTrx" placeholder="Transaction Reference">
  <button onclick="deposit()">Submit Request</button>
  <p id="depMsg" class="muted"></p>
  <div class="notice">Demo request only. No payment will be collected or verified.</div>
 </div>
</section>

<section id="withdraw" class="page">
 <div class="card">
  <h2>Withdraw</h2>
  <p class="muted">Withdrawal will only be allowed to the verified account number.</p>
  <div class="notice">Verified number: <b id="withdrawPhone">Not verified</b></div>
  <select id="withMethod"><option>bKash</option><option>Nagad</option></select>
  <input id="withAmount" type="number" placeholder="Withdraw amount (BDT)">
  <button onclick="withdraw()">Submit Request</button>
  <p id="withMsg" class="muted"></p>
 </div>
</section>

<section id="plans" class="page">
 <div class="card">
  <h2>Investment Plans</h2>
  <div id="planList">No active plans available.</div>
  <div class="notice">Only authorized and legally compliant investment products should be offered. No guaranteed returns.</div>
 </div>
</section>

<section id="history" class="page">
 <div class="card">
  <h2>Transaction History</h2>
  <div id="historyList">No transactions.</div>
 </div>
</section>

<section id="support" class="page">
 <div class="card">
  <h2>Customer Support</h2>
  <div id="chatMessages"></div>
  <textarea id="chatText" placeholder="Write your message"></textarea>
  <button onclick="sendChat()">Send</button>
  <p class="muted">Demo chat. A real-time support server is not connected.</p>
 </div>
</section>

<section id="admin" class="page">
 <div class="card">
  <h2>Admin Panel</h2>
  <p class="muted">Secure administrator authentication is required.</p>
  <p>Admin Mobile: 01339400944</p>
  <div class="notice">Admin access and approval controls will only work after server-side authentication is configured. No frontend password or bypass is provided.</div>
  <h3>Admin Management Modules</h3>
  <p>• User Management</p>
  <p>• KYC Review</p>
  <p>• Deposit Approval</p>
  <p>• Withdrawal Approval</p>
  <p>• Investment Plan Management</p>
  <p>• Audit Logs</p>
 </div>
</section>

</main>
<footer>MH INVEST © 2026 | Demo Website</footer>

<script>
let currentUser=null;
let kycData=[];
let transactions=[];
let balance=0;
let plans=[];

function show(id){
 document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
 document.getElementById(id).classList.add('active');
}

function register(){
 let phone=document.getElementById('regPhone').value.trim();
 let pass=document.getElementById('regPass').value;
 if(!/^01[3-9]\d{8}$/.test(phone)||pass.length<10){
  authMsg.textContent='Enter a valid Bangladesh mobile number and password (10+ characters).';
  return;
 }
 authMsg.textContent='Demo only. Connect OTP and secure backend to create an account.';
}

function login(){
 authMsg.textContent='Login requires the secure backend. Demo authentication is disabled.';
}

function logout(){
 currentUser=null;
 show('login');
}

function submitKyc(){
 if(!currentUser){kycMsg.textContent='Login required.';return}
 if(!legalName.value.trim()||!birthDate.value||!agree.checked){
  kycMsg.textContent='Complete the required fields and consent.';
  return;
 }
 kycMsg.textContent='Demo only. Secure KYC provider is not connected.';
}

function deposit(){
 if(!currentUser){depMsg.textContent='Login required.';return}
 let a=Number(depAmount.value);
 if(a<=0||!depTrx.value.trim()){
  depMsg.textContent='Enter a valid amount and transaction reference.';
  return;
 }
 depMsg.textContent='Payment provider and server verification are not connected. No money was deposited.';
}

function withdraw(){
 if(!currentUser){withMsg.textContent='Login required.';return}
 withMsg.textContent='Secure verified-number withdrawal service is not connected.';
}

function sendChat(){
 let msg=chatText.value.trim();
 if(!msg)return;
 let p=document.createElement('p');
 p.textContent='You: '+msg;
 chatMessages.appendChild(p);
 chatText.value='';
}

</script>
</body>
</html>
