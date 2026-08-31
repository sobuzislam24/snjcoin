<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>NJ Mining</title>

<script src="https://telegram.org/js/telegram-web-app.js"></script>

<style>
*{
 box-sizing:border-box;
 margin:0;
 padding:0;
 font-family:Arial,sans-serif;
}

body{
 background:#0b1020;
 color:#fff;
 min-height:100vh;
}

.app{
 max-width:480px;
 margin:auto;
 padding:18px;
 padding-bottom:95px;
}

.header{
 display:flex;
 justify-content:space-between;
 align-items:center;
 margin-bottom:20px;
}

.logo{
 font-size:22px;
 font-weight:bold;
}

.user{
 background:#171e35;
 padding:8px 12px;
 border-radius:20px;
 font-size:13px;
}

.page{
 display:none;
}

.page.active{
 display:block;
}

.balance-card{
 background:linear-gradient(135deg,#1b2550,#111936);
 border:1px solid #2c3970;
 border-radius:22px;
 padding:25px;
 text-align:center;
}

.balance-title{
 color:#9ca9d9;
 font-size:14px;
}

.balance{
 font-size:38px;
 font-weight:bold;
 margin:10px 0;
}

.coin{
 color:#ffd84d;
}

.rate{
 color:#7ee787;
 font-size:14px;
}

.mine-btn{
 width:100%;
 margin-top:20px;
 padding:16px;
 border:0;
 border-radius:15px;
 background:#4f7cff;
 color:white;
 font-size:17px;
 font-weight:bold;
}

.mine-btn.mining{
 background:#e05252;
}

.timer{
 margin-top:14px;
 color:#b9c3e8;
 font-size:14px;
}

.grid{
 display:grid;
 grid-template-columns:1fr 1fr;
 gap:12px;
 margin-top:18px;
}

.card{
 background:#131a31;
 border:1px solid #252f54;
 border-radius:17px;
 padding:18px;
}

.card-icon{
 font-size:25px;
}

.card-title{
 color:#8e9bc5;
 font-size:12px;
 margin-top:8px;
}

.card-value{
 font-size:18px;
 font-weight:bold;
 margin-top:5px;
}

.section{
 margin-top:22px;
}

.section h2{
 font-size:18px;
 margin-bottom:12px;
}

.bonus{
 background:linear-gradient(135deg,#3a2869,#20234f);
 border-radius:18px;
 padding:18px;
 display:flex;
 justify-content:space-between;
 align-items:center;
}

button{
 cursor:pointer;
}

.bonus button{
 background:#ffd84d;
 color:#171717;
 border:0;
 padding:10px 15px;
 border-radius:10px;
 font-weight:bold;
}

.referral{
 background:#131a31;
 border:1px solid #252f54;
 border-radius:18px;
 padding:18px;
}

.ref-link{
 margin-top:12px;
 background:#0b1020;
 padding:12px;
 border-radius:10px;
 font-size:12px;
 overflow:hidden;
 white-space:nowrap;
}

.copy-btn{
 width:100%;
 margin-top:10px;
 padding:12px;
 border:0;
 border-radius:10px;
 background:#26345e;
 color:white;
}

/* TASKS */

.task{
 background:#131a31;
 border:1px solid #252f54;
 border-radius:17px;
 padding:16px;
 margin-bottom:12px;
}

.task-top{
 display:flex;
 align-items:center;
 gap:12px;
}

.task-icon{
 width:45px;
 height:45px;
 border-radius:13px;
 background:#202b4d;
 display:flex;
 align-items:center;
 justify-content:center;
 font-size:24px;
}

.task-name{
 font-weight:bold;
}

.task-desc{
 color:#8e9bc5;
 font-size:12px;
 margin-top:4px;
}

.task-bottom{
 display:flex;
 justify-content:space-between;
 align-items:center;
 margin-top:15px;
}

.reward{
 color:#ffd84d;
 font-weight:bold;
}

.task-btn{
 background:#4f7cff;
 color:white;
 border:0;
 border-radius:10px;
 padding:9px 15px;
 font-weight:bold;
}

.task-btn.done{
 background:#263047;
 color:#7ee787;
}

/* AD SPACE */

.ad-space{
 margin-top:25px;
}

.ad-label{
 text-align:center;
 color:#657092;
 font-size:10px;
 letter-spacing:1px;
 margin-bottom:7px;
}

.ad-box{
 min-height:180px;
 background:#11182d;
 border:1px solid #202b4c;
 border-radius:15px;
 display:flex;
 flex-direction:column;
 align-items:center;
 justify-content:center;
 color:#68759a;
}

.ad-box span{
 font-size:32px;
}

.ad-box p{
 margin-top:8px;
 font-size:12px;
}

/* PROFILE */

.profile-card{
 background:#131a31;
 border:1px solid #252f54;
 border-radius:20px;
 padding:25px;
 text-align:center;
}

.avatar{
 width:70px;
 height:70px;
 border-radius:50%;
 background:#4f7cff;
 display:flex;
 align-items:center;
 justify-content:center;
 font-size:30px;
 margin:auto;
}

.profile-name{
 font-size:20px;
 font-weight:bold;
 margin-top:12px;
}

.profile-id{
 color:#8e9bc5;
 font-size:12px;
 margin-top:5px;
}

/* BOTTOM NAV */

.bottom-nav{
 position:fixed;
 bottom:0;
 left:50%;
 transform:translateX(-50%);
 width:100%;
 max-width:480px;
 height:70px;
 background:#10162b;
 border-top:1px solid #273153;
 display:flex;
 justify-content:space-around;
 align-items:center;
 z-index:50;
}

.nav-item{
 text-align:center;
 color:#7f8bb2;
 font-size:11px;
}

.nav-item.active{
 color:#6d91ff;
}

.nav-icon{
 display:block;
 font-size:21px;
 margin-bottom:3px;
}

/* TOAST */

.toast{
 position:fixed;
 bottom:85px;
 left:50%;
 transform:translateX(-50%);
 background:#252e4c;
 padding:12px 18px;
 border-radius:12px;
 display:none;
 z-index:100;
 font-size:13px;
}

/* AD MODAL */

.ad-modal{
 position:fixed;
 inset:0;
 background:rgba(0,0,0,.78);
 display:none;
 align-items:center;
 justify-content:center;
 z-index:200;
 padding:20px;
}

.ad-modal-box{
 width:100%;
 max-width:350px;
 background:#151d35;
 border:1px solid #303d68;
 border-radius:20px;
 padding:25px;
 text-align:center;
}

.ad-icon{
 font-size:45px;
}

.ad-modal-box h3{
 margin-top:10px;
}

.ad-status{
 margin-top:15px;
 color:#7ee787;
 font-size:13px;
}

.progress{
 height:9px;
 background:#0b1020;
 border-radius:10px;
 margin-top:15px;
 overflow:hidden;
}

.progress-bar{
 height:100%;
 width:0%;
 background:#4f7cff;
}
</style>
</head>

<body>

<div class="app">

<div class="header">
 <div class="logo">⛏️ NJ Mining</div>
 <div class="user" id="username">@User</div>
</div>


<!-- ================= HOME ================= -->

<div id="homePage" class="page active">

<div class="balance-card">

 <div class="balance-title">
 YOUR BALANCE
 </div>

 <div class="balance">
   <span id="balance">0.00</span>
   <span class="coin"> NJM</span>
 </div>

 <div class="rate">
   ⚡ +0.25 NJM / hour
 </div>

 <button
   class="mine-btn"
   id="mineBtn"
   onclick="toggleMining()">

   ⛏️ START MINING

 </button>

 <div class="timer">
   Mining time:
   <span id="timer">00:00:00</span>
 </div>

</div>


<div class="grid">

 <div class="card">
   <div class="card-icon">👥</div>
   <div class="card-title">REFERRALS</div>
   <div class="card-value" id="referrals">0</div>
 </div>

 <div class="card">
   <div class="card-icon">🔥</div>
   <div class="card-title">MINING STREAK</div>
   <div class="card-value">1 Day</div>
 </div>

</div>


<div class="section">

<h2>🎁 Daily Bonus</h2>

<div class="bonus">

 <div>
   <b>Daily Reward</b><br>
   <small>Claim your daily coins</small>
 </div>

 <button id="bonusBtn" onclick="claimBonus()">
   +10 NJM
 </button>

</div>

</div>


<div class="section">

<h2>👥 Invite Friends</h2>

<div class="referral">

 Invite friends and increase your mining rewards.

 <div class="ref-link" id="refLink">
   Loading...
 </div>

 <button class="copy-btn" onclick="copyReferral()">
   📋 Copy Referral Link
 </button>

</div>

</div>


<!-- AD AREA -->

<div class="ad-space">

<div class="ad-label">
ADVERTISEMENT
</div>

<div class="ad-box">
 <span>📢</span>
 <p>Advertisement</p>
</div>

</div>

</div>


<!-- ================= MINING PAGE ================= -->

<div id="miningPage" class="page">

<h2>⛏️ Mining</h2>

<div class="section">

<div class="card">

 <div class="card-title">
 CURRENT MINING RATE
 </div>

 <div class="card-value">
 +0.25 NJM / Hour
 </div>

 <br>

 <div class="card-title">
 AVAILABLE MINING TIME
 </div>

 <div class="card-value" id="miningTimeText">
 00:00:00
 </div>

 <button
   class="mine-btn"
   onclick="toggleMining()"
   id="mineBtn2">

   ⛏️ START MINING

 </button>

</div>

</div>

</div>


<!-- ================= TASKS PAGE ================= -->

<div id="tasksPage" class="page">

<h2>🎯 Tasks</h2>

<div class="section">

<p style="color:#8e9bc5;font-size:13px;margin-bottom:15px;">
Complete tasks and earn NJM rewards.
</p>


<!-- TASK 1 -->

<div class="task">

<div class="task-top">

<div class="task-icon">
📢
</div>

<div>
<div class="task-name">
NJ Official Channel
</div>

<div class="task-desc">
Join our official Telegram channel
</div>
</div>

</div>

<div class="task-bottom">

<div class="reward">
⭐ +5 NJM
</div>

<button
class="task-btn"
onclick="completeTask(this, 'task1', 5, 'https://t.me/YOUR_CHANNEL')">

JOIN

</button>

</div>

</div>


<!-- TASK 2 -->

<div class="task">

<div class="task-top">

<div class="task-icon">
👥
</div>

<div>
<div class="task-name">
NJ Community
</div>

<div class="task-desc">
Join our Telegram community
</div>
</div>

</div>

<div class="task-bottom">

<div class="reward">
⭐ +10 NJM
</div>

<button
class="task-btn"
onclick="completeTask(this, 'task2', 10, 'https://t.me/YOUR_GROUP')">

JOIN

</button>

</div>

</div>


<!-- WATCH AD TASK -->

<div class="task">

<div class="task-top">

<div class="task-icon">
📺
</div>

<div>
<div class="task-name">
Watch Advertisement
</div>

<div class="task-desc">
Watch an advertisement and earn a small reward
</div>
</div>

</div>

<div class="task-bottom">

<div class="reward">
⭐ +0.10 NJM
</div>

<button
class="task-btn"
onclick="watchTaskAd(this)">

WATCH

</button>

</div>

</div>

</div>

</div>


<!-- ================= FRIENDS ================= -->

<div id="friendsPage" class="page">

<h2>👥 Friends</h2>

<div class="section">

<div class="card">

<div class="card-icon">
👥
</div>

<div class="card-title">
TOTAL INVITED
</div>

<div class="card-value" id="friendsCount">
0
</div>

</div>

</div>

<div class="section">

<div class="referral">

<b>Invite friends</b>

<p style="color:#8e9bc5;font-size:13px;margin-top:8px;">
Share your referral link and receive rewards.
</p>

<div class="ref-link" id="friendReferral">
Loading...
</div>

<button class="copy-btn" onclick="copyReferral()">
📋 Copy Link
</button>

</div>

</div>

</div>


<!-- ================= PROFILE ================= -->

<div id="profilePage" class="page">

<h2>👤 Profile</h2>

<div class="section">

<div class="profile-card">

<div class="avatar">
👤
</div>

<div class="profile-name" id="profileName">
User
</div>

<div class="profile-id">
Telegram ID:
<span id="telegramId">-</span>
</div>

</div>

</div>


<div class="grid">

<div class="card">
<div class="card-title">
BALANCE
</div>
<div class="card-value">
<span id="profileBalance">0.00</span>
NJM
</div>
</div>

<div class="card">
<div class="card-title">
REFERRALS
</div>
<div class="card-value">
<span id="profileReferrals">0</span>
</div>
</div>

</div>

</div>

</div>


<!-- BOTTOM NAV -->

<div class="bottom-nav">

<div
class="nav-item active"
onclick="openPage('homePage',this)">

<span class="nav-icon">🏠</span>
Home

</div>

<div
class="nav-item"
onclick="openPage('miningPage',this)">

<span class="nav-icon">⛏️</span>
Mining

</div>

<div
class="nav-item"
onclick="openPage('tasksPage',this)">

<span class="nav-icon">🎯</span>
Tasks

</div>

<div
class="nav-item"
onclick="openPage('friendsPage',this)">

<span class="nav-icon">👥</span>
Friends

</div>

<div
class="nav-item"
onclick="openPage('profilePage',this)">

<span class="nav-icon">👤</span>
Profile

</div>

</div>


<!-- TOAST -->

<div class="toast" id="toast"></div>


<!-- AD MODAL -->

<div class="ad-modal" id="adModal">

<div class="ad-modal-box">

<div class="ad-icon">
📺
</div>

<h3>
Rewarded Advertisement
</h3>

<p style="color:#9ca9d9;font-size:13px;margin-top:8px;">
Please watch the advertisement completely.
</p>

<div class="progress">

<div
class="progress-bar"
id="progressBar">
</div>

</div>

<div class="ad-status" id="adStatus">
Preparing advertisement...
</div>

</div>

</div>


<script>

/* TELEGRAM */

const tg =
window.Telegram.WebApp;

tg.ready();
tg.expand();


/* USER */

const user =
tg.initDataUnsafe?.user;

if(user){

 document.getElementById("username")
 .innerText =
 "@" +
 (
  user.username ||
  user.first_name ||
  "User"
 );

 document.getElementById("profileName")
 .innerText =
 user.first_name || "User";

 document.getElementById("telegramId")
 .innerText =
 user.id;

}


/* BOT USERNAME */

const botUsername =
"YOUR_BOT_USERNAME";


if(user){

 const link =
 "https://t.me/" +
 botUsername +
 "?start=" +
 user.id;

 document.getElementById("refLink")
 .innerText = link;

 document.getElementById("friendReferral")
 .innerText = link;

}


/* =========================
   MINING
========================= */

const miningRate = 0.25;

let balance = 0;

let miningTime = 0;

let mining = false;

let miningInterval = null;

let lastMiningUpdate = null;


/*
 Number of completed
 2-ad cycles
*/

let adCycle = 0;


/* Mining minutes */

function getMiningMinutes(){

 const minutes =
 60 -
 (
  adCycle * 10
 );

 return Math.max(
  minutes,
  10
 );

}


/* START MINING */

async function toggleMining(){

 if(mining){

  stopMining();

  return;

 }


 /*
 First rewarded ad
 */

 const ad1 =
 await showRewardedAd(1);

 if(!ad1){

  showToast(
   "❌ First ad not completed"
  );

  return;

 }


 /*
 Second rewarded ad
 */

 const ad2 =
 await showRewardedAd(2);

 if(!ad2){

  showToast(
   "❌ Second ad not completed"
  );

  return;

 }


 /*
 Add mining time
 */

 const minutes =
 getMiningMinutes();

 miningTime +=
 minutes * 60;

 adCycle++;

 updateTimer();

 if(!mining){

  startMining();

 }

 showToast(
  "⛏️ +" +
  minutes +
  " minutes added!"
 );

}


/* START */

function startMining(){

 mining = true;

 lastMiningUpdate =
 Date.now();

 document.getElementById("mineBtn")
 .innerText =
 "⛔ STOP MINING";

 document.getElementById("mineBtn")
 .classList.add("mining");


 document.getElementById("mineBtn2")
 .innerText =
 "⛔ STOP MINING";

 document.getElementById("mineBtn2")
 .classList.add("mining");


 if(miningInterval){

  clearInterval(
   miningInterval
  );

 }

 miningInterval =
 setInterval(
  updateMining,
  1000
 );

}


/* UPDATE */

function updateMining(){

 if(!mining)return;

 const now =
 Date.now();

 const elapsed =
 (now -
 lastMiningUpdate) /
 1000;

 lastMiningUpdate =
 now;

 miningTime -=
 elapsed;


 balance +=
 (
  elapsed /
  3600
 ) *
 miningRate;


 document.getElementById("balance")
 .innerText =
 balance.toFixed(4);


 document.getElementById("profileBalance")
 .innerText =
 balance.toFixed(4);


 updateTimer();


 if(miningTime <= 0){

  miningTime = 0;

  stopMining();

  showToast(
   "⏰ Mining completed!"
  );

 }

}


/* STOP */

function stopMining(){

 mining = false;

 clearInterval(
  miningInterval
 );

 miningInterval = null;


 document.getElementById("mineBtn")
 .innerText =
 "⛏️ START MINING";

 document.getElementById("mineBtn")
 .classList.remove("mining");


 document.getElementById("mineBtn2")
 .innerText =
 "⛏️ START MINING";

 document.getElementById("mineBtn2")
 .classList.remove("mining");


 updateTimer();

}


/* TIMER */

function updateTimer(){

 let total =
 Math.max(
 0,
 Math.floor(
  miningTime
 )
 );


 const hours =
 Math.floor(
  total / 3600
 );


 const minutes =
 Math.floor(
  (total % 3600) / 60
 );


 const seconds =
 total % 60;


 const text =
 String(hours).padStart(2,"0")
 + ":" +
 String(minutes).padStart(2,"0")
 + ":" +
 String(seconds).padStart(2,"0");


 document.getElementById("timer")
 .innerText = text;


 document.getElementById("miningTimeText")
 .innerText = text;

}


/* =========================
   REWARDED AD
========================= */

function showRewardedAd(adNumber){

 return new Promise(
  resolve => {

   const modal =
   document.getElementById("adModal");

   const bar =
   document.getElementById("progressBar");

   const status =
   document.getElementById("adStatus");


   modal.style.display =
   "flex";

   bar.style.width =
   "0%";

   status.innerText =
   "Watching Ad " +
   adNumber +
   "...";


   /*
    DEMO ONLY.

    Replace this with the
    real rewarded-ad SDK.
   */

   let progress = 0;

   const interval =
   setInterval(
    () => {

     progress += 10;

     bar.style.width =
     progress + "%";


     if(progress >= 100){

      clearInterval(
       interval
      );

      status.innerText =
      "✅ Advertisement completed";


      setTimeout(
       () => {

        modal.style.display =
        "none";

        resolve(true);

       },
       500
      );

     }

    },
    300
   );

  }
 );

}


/* =========================
   TASKS
========================= */

function completeTask(
 button,
 taskId,
 reward,
 link
){

 /*
  Open Telegram group/channel
 */

 window.open(
  link,
  "_blank"
 );


 /*
  DEMO VERIFY

  Real version must verify
  Telegram membership on server.
 */

 setTimeout(
  () => {

   if(
    button.classList.contains(
     "done"
    )
   ){

    return;

   }


   button.innerText =
   "VERIFY";


   button.onclick =
   function(){

    verifyTask(
     button,
     taskId,
     reward
    );

   };


  },
  500
 );

}


/* VERIFY TASK */

function verifyTask(
 button,
 taskId,
 reward
){

 /*
  DEMO verification.

  Real app:
  Telegram Bot API +
  backend verification.
 */


 if(
  localStorage.getItem(
   "completed_" + taskId
  )
 ){

  showToast(
   "✅ Task already completed"
  );

  return;

 }


 balance +=
 reward;


 document.getElementById("balance")
 .innerText =
 balance.toFixed(4);


 document.getElementById("profileBalance")
 .innerText =
 balance.toFixed(4);


 localStorage.setItem(
  "completed_" + taskId,
  "true"
 );


 button.innerText =
 "✓ COMPLETED";

 button.classList.add(
  "done"
 );

 button.disabled =
 true;


 showToast(
  "🎉 +" +
  reward +
  " NJM received!"
 );

}


/* =========================
   WATCH AD TASK
========================= */

async function watchTaskAd(button){

 if(
  button.classList.contains(
   "done"
  )
 ){

  return;

 }


 const completed =
 await showRewardedAd(
  "Task"
 );


 if(!completed){

  return;

 }


 /*
  Small reward
 */

 const reward =
 0.10;


 balance +=
 reward;


 document.getElementById("balance")
 .innerText =
 balance.toFixed(4);


 document.getElementById("profileBalance")
 .innerText =
 balance.toFixed(4);


 button.innerText =
 "✓ COMPLETED";

 button.classList.add(
  "done"
 );

 button.disabled =
 true;


 showToast(
  "📺 +" +
  reward +
  " NJM received!"
 );

}


/* =========================
   DAILY BONUS
========================= */

function claimBonus(){

 if(
  localStorage.getItem(
   "dailyBonus"
  )
 ){

  showToast(
   "🎁 Bonus already claimed"
  );

  return;

 }


 balance += 10;


 document.getElementById("balance")
 .innerText =
 balance.toFixed(4);


 document.getElementById("profileBalance")
 .innerText =
 balance.toFixed(4);


 localStorage.setItem(
  "dailyBonus",
  new Date().toDateString()
 );


 document.getElementById("bonusBtn")
 .innerText =
 "CLAIMED";


 document.getElementById("bonusBtn")
 .disabled =
 true;


 showToast(
  "🎁 +10 NJM received!"
 );

}


/* =========================
   REFERRAL
========================= */

function copyReferral(){

 const link =
 document.getElementById(
  "refLink"
 ).innerText;


 if(!link){

  return;

 }


 navigator.clipboard
 .writeText(link)
 .then(
  () => {

   showToast(
    "📋 Referral link copied!"
   );

  }
 );

}


/* =========================
   NAVIGATION
========================= */

function openPage(
 pageId,
 element
){

 document.querySelectorAll(
  ".page"
 ).forEach(
  page => {

   page.classList.remove(
    "active"
   );

  }
 );


 document.getElementById(
  pageId
 ).classList.add(
  "active"
 );


 document.querySelectorAll(
  ".nav-item"
 ).forEach(
  item => {

   item.classList.remove(
    "active"
   );

  }
 );


 element.classList.add(
  "active"
 );

}


/* =========================
   TOAST
========================= */

function showToast(message){

 const toast =
 document.getElementById(
  "toast"
 );

 toast.innerText =
 message;

 toast.style.display =
 "block";


 setTimeout(
  () => {

   toast.style.display =
   "none";

  },
  2500
 );

}


/* INITIAL */

updateTimer();

</script>

</body>
</html>
