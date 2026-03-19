<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>祥真一職人微型電動車電池診斷系統</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
*{
  box-sizing:border-box;
}

html,body{
  margin:0;
  padding:0;
  overflow-x:hidden;
}

body{
  font-family:Arial,"Noto Sans TC",sans-serif;
  color:#1d2a3a;
  background:
    radial-gradient(circle at 12% 18%, rgba(255,255,255,0.95) 0%, rgba(255,255,255,0) 28%),
    radial-gradient(circle at 86% 78%, rgba(255,255,255,0.78) 0%, rgba(255,255,255,0) 26%),
    linear-gradient(180deg,#eef5ff 0%, #e5eefb 48%, #dde8f6 100%);
  position:relative;
}

body::before{
  content:"";
  position:fixed;
  inset:0;
  pointer-events:none;
  z-index:0;
  background:
    radial-gradient(circle at 18% 26%, rgba(38,110,255,0.10) 0 2px, transparent 3px),
    radial-gradient(circle at 82% 22%, rgba(38,110,255,0.08) 0 2px, transparent 3px),
    radial-gradient(circle at 72% 74%, rgba(38,110,255,0.08) 0 2px, transparent 3px),
    radial-gradient(circle at 28% 78%, rgba(38,110,255,0.06) 0 2px, transparent 3px);
  opacity:.8;
}

body::after{
  content:"";
  position:fixed;
  inset:0;
  pointer-events:none;
  z-index:0;
  background:
    radial-gradient(80% 40% at 18% 10%, rgba(65,125,255,0.08) 0%, rgba(65,125,255,0) 60%),
    radial-gradient(70% 38% at 92% 76%, rgba(65,125,255,0.06) 0%, rgba(65,125,255,0) 62%);
  opacity:.9;
}

header{
  background:
    linear-gradient(135deg,rgba(8,74,163,0.96),rgba(45,117,232,0.96)),
    linear-gradient(180deg,#0c56b6,#1e73dd);
  color:#fff;
  text-align:center;
  padding:28px 14px 24px;
  box-shadow:0 10px 28px rgba(12,67,150,0.18);
  position:relative;
  z-index:1;
  overflow:hidden;
}

header::before{
  content:"";
  position:absolute;
  width:260px;
  height:260px;
  border-radius:50%;
  top:-150px;
  left:-80px;
  background:radial-gradient(circle, rgba(255,255,255,0.20), rgba(255,255,255,0));
  pointer-events:none;
}

header::after{
  content:"";
  position:absolute;
  width:240px;
  height:240px;
  border-radius:50%;
  right:-100px;
  top:-90px;
  background:radial-gradient(circle, rgba(255,255,255,0.14), rgba(255,255,255,0));
  pointer-events:none;
}

.header-inner{
  width:min(580px, calc(100% - 24px));
  margin:0 auto;
  position:relative;
  z-index:1;
}

.header-title{
  font-size:28px;
  font-weight:800;
  letter-spacing:1px;
  text-shadow:0 2px 10px rgba(0,0,0,0.10);
}

.header-sub{
  margin-top:10px;
  font-size:13px;
  opacity:0.97;
  line-height:1.8;
  letter-spacing:.3px;
}

.hero{
  width:min(580px, calc(100% - 24px));
  margin:16px auto 0;
  background:rgba(255,255,255,0.94);
  border-radius:22px;
  box-shadow:
    0 16px 34px rgba(39,85,155,0.10),
    0 2px 10px rgba(255,255,255,0.45) inset;
  border:1px solid rgba(108,149,214,0.15);
  padding:20px 20px 18px;
  position:relative;
  z-index:1;
  backdrop-filter:blur(4px);
}

.hero::before{
  content:"";
  position:absolute;
  inset:0;
  border-radius:22px;
  pointer-events:none;
  background:
    linear-gradient(135deg, rgba(53,122,235,0.06), rgba(255,255,255,0) 40%),
    linear-gradient(315deg, rgba(53,122,235,0.04), rgba(255,255,255,0) 42%);
}

.hero-title{
  text-align:center;
  color:#0f5fcb;
  font-size:20px;
  font-weight:800;
  margin-bottom:8px;
  letter-spacing:.4px;
  position:relative;
  z-index:1;
}

.hero-note{
  text-align:center;
  font-size:13px;
  color:#5a6879;
  line-height:1.8;
  position:relative;
  z-index:1;
}

.tab-bar{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:10px;
  margin-top:16px;
  position:relative;
  z-index:1;
}

.tab-btn{
  border:none;
  border-radius:16px;
  padding:14px 10px;
  font-size:14px;
  font-weight:800;
  cursor:pointer;
  color:#18519d;
  background:linear-gradient(180deg,#f8fbff,#ebf3ff);
  box-shadow:
    inset 0 0 0 1px #d8e5f7,
    0 6px 14px rgba(50,96,170,0.08);
  transition:all .25s ease;
  letter-spacing:.2px;
}

.tab-btn:hover{
  transform:translateY(-2px);
  box-shadow:
    inset 0 0 0 1px #cfe0f7,
    0 10px 18px rgba(50,96,170,0.12);
}

.tab-btn.active{
  color:#fff;
  background:linear-gradient(135deg,#0e5fc6,#3084ea);
  box-shadow:
    0 10px 20px rgba(31,96,188,0.22),
    inset 0 1px 0 rgba(255,255,255,0.14);
}

.container{
  width:min(580px, calc(100% - 24px));
  margin:16px auto 24px;
  background:rgba(255,255,255,0.95);
  padding:24px 22px;
  border-radius:22px;
  box-shadow:
    0 16px 34px rgba(39,85,155,0.10),
    0 2px 10px rgba(255,255,255,0.45) inset;
  border:1px solid rgba(108,149,214,0.15);
  position:relative;
  z-index:1;
  backdrop-filter:blur(4px);
}

.hidden{
  display:none;
}

.section-title{
  text-align:center;
  font-weight:800;
  color:#0e5fca;
  margin-top:2px;
  margin-bottom:10px;
  font-size:20px;
  letter-spacing:.3px;
}

.section-subtitle{
  text-align:center;
  font-size:13px;
  color:#6b7887;
  margin-bottom:12px;
  line-height:1.7;
}

label{
  font-weight:800;
  display:block;
  margin-top:13px;
  color:#2d3b4c;
  font-size:14px;
}

select,input{
  width:100%;
  padding:12px 12px;
  margin-top:7px;
  border:1px solid #d2deec;
  border-radius:12px;
  font-size:14px;
  background:#fff;
  color:#253649;
  outline:none;
  transition:border-color .2s ease, box-shadow .2s ease;
  box-shadow:0 2px 6px rgba(0,0,0,0.02);
}

select:focus,input:focus{
  border-color:#7aa7eb;
  box-shadow:0 0 0 4px rgba(82,133,220,0.12);
}

button.calc-btn{
  width:100%;
  padding:15px;
  margin-top:20px;
  background:linear-gradient(90deg,#1672dc,#3c8ff2);
  color:#fff;
  border:none;
  border-radius:15px;
  font-size:17px;
  font-weight:800;
  cursor:pointer;
  transition:all .25s ease;
  letter-spacing:.4px;
  box-shadow:0 10px 20px rgba(27,109,215,0.18);
}

button.calc-btn:hover{
  transform:translateY(-2px);
  box-shadow:0 14px 24px rgba(27,109,215,0.22);
}

.result{
  margin-top:18px;
  background:linear-gradient(180deg,#f9fbff,#f3f8ff);
  padding:18px;
  border-radius:16px;
  line-height:1.95;
  border-left:5px solid #36b56d;
  box-shadow:
    inset 0 0 0 1px #e9f0f8,
    0 8px 16px rgba(32,78,150,0.05);
  color:#2a3a4f;
}

.warning{
  color:#d63031;
  font-weight:800;
}

.error-box{
  margin-top:16px;
  background:#fff4f4;
  color:#c62828;
  padding:13px;
  border-radius:14px;
  border-left:5px solid #e53935;
  display:none;
  line-height:1.7;
  font-weight:800;
  box-shadow:0 6px 16px rgba(206,65,65,0.08);
}

.input-error{
  border:2px solid #e53935 !important;
  box-shadow:0 0 0 4px rgba(229,57,53,0.12) !important;
}

table{
  width:100%;
  max-width:100%;
  margin:16px auto 0 auto;
  border-collapse:collapse;
  border-radius:14px;
  overflow:hidden;
  table-layout:fixed;
  background:#fff;
  box-shadow:0 8px 16px rgba(31,78,145,0.05);
}

td{
  width:50%;
  border:1px solid #e4edf7;
  padding:11px 8px;
  text-align:center;
  vertical-align:middle;
  font-size:13px;
  word-break:break-word;
  color:#2d3b4c;
}

tr:first-child td{
  background:linear-gradient(180deg,#f6f9ff,#edf4ff);
  font-weight:800;
  color:#1b4f95;
}

#li_segment,
#pb_segment{
  width:100%;
  display:block;
}

#li_segment table,
#pb_segment table{
  width:100%;
}

canvas{
  margin-top:20px;
  width:100% !important;
  max-width:100%;
  background:linear-gradient(180deg, rgba(255,255,255,0.72), rgba(246,250,255,0.72));
  border-radius:16px;
  box-shadow:inset 0 0 0 1px rgba(213,226,242,0.8);
}

.info-strong{
  font-size:17px;
  font-weight:800;
  color:#0e5fc8;
}

.health-a{color:#14944a;font-weight:800;}
.health-b{color:#1e81c4;font-weight:800;}
.health-c{color:#c78408;font-weight:800;}
.health-d{color:#d45f06;font-weight:800;}
.health-e{color:#c0392b;font-weight:800;}

.bar{
  width:100%;
  height:22px;
  background:linear-gradient(180deg,#dde5ef,#cfd9e6);
  border-radius:12px;
  overflow:hidden;
  margin-top:14px;
  box-shadow:inset 0 2px 5px rgba(0,0,0,0.12);
}

.bar-fill{
  height:100%;
  width:0%;
  background:linear-gradient(90deg,#16c96b,#6de46d);
  transition:width .5s ease;
  box-shadow:0 0 12px rgba(49,210,111,0.25);
}

.status{
  margin-top:10px;
  font-weight:800;
  font-size:15px;
  color:#2b3f56;
}

.small-note{
  font-size:13px;
  color:#667587;
  margin-top:12px;
  line-height:1.8;
}

.stats-box{
  margin-top:18px;
  background:linear-gradient(180deg,#f8fbff,#eef5ff);
  padding:15px;
  border-radius:16px;
  box-shadow:
    inset 0 0 0 1px #e0eaf6,
    0 8px 16px rgba(39,85,155,0.06);
  line-height:1.9;
  text-align:center;
  color:#38516d;
}

.notice-card{
  margin-top:14px;
  padding:14px 14px 12px;
  border-radius:14px;
  background:linear-gradient(180deg,#f7fbff,#eef5ff);
  border:1px solid #dbe8f7;
  border-left:5px solid #4c8fe8;
  box-shadow:0 6px 14px rgba(39,85,155,0.06);
}

.notice-title{
  font-size:14px;
  font-weight:800;
  color:#1e5fb8;
  margin-bottom:6px;
  letter-spacing:.2px;
}

.notice-text{
  font-size:14px;
  line-height:1.8;
  color:#3d5168;
}

.notice-store{
  margin-top:8px;
  font-size:13px;
  color:#5d7088;
  font-weight:700;
}

footer{
  margin-top:22px;
  text-align:center;
  font-size:13px;
  color:#718093;
  padding-bottom:18px;
}

@media (max-width:540px){
  .header-title{
    font-size:22px;
  }

  .header-sub{
    font-size:12px;
  }

  .container,
  .hero{
    padding:18px;
    border-radius:18px;
  }

  .tab-bar{
    grid-template-columns:1fr;
  }

  .section-title{
    font-size:18px;
  }

  .tab-btn{
    padding:13px 12px;
  }
}
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="header-title">⚡ 祥真一職人</div>
    <div class="header-sub">
      微型電動車電池診斷系統<br>
      鋰電池充電診斷系統｜鉛酸電池充電診斷系統｜續航距離評估系統
    </div>
  </div>
</header>

<div class="hero">
  <div class="hero-title">微型電動車專用工具首頁</div>
  <div class="hero-note">
    本系統針對微型電動車使用情境設計，可用於充電時間估算、電池健康判讀與續航距離評估。
  </div>

  <div id="systemTimeBox" class="small-note" style="text-align:center;margin-top:10px;">
    系統時間讀取中...
  </div>

  <div class="stats-box" style="margin-top:12px;">
    📊 系統使用統計<br>
    👀 系統瀏覽：<span id="systemViews">讀取中...</span><br>
    🔋 系統計算：<span id="systemCalc">讀取中...</span>
  </div>

  <div class="tab-bar">
    <button id="tabLithium" class="tab-btn active" onclick="switchTool('lithium')">🔋 鋰電池充電診斷系統</button>
    <button id="tabLead" class="tab-btn" onclick="switchTool('lead')">🔋 鉛酸電池充電診斷系統</button>
    <button id="tabRange" class="tab-btn" onclick="switchTool('range')">🛵 續航距離評估系統</button>
  </div>
</div>

<div id="lithiumBox" class="container">
  <div class="section-title">祥真一職人鋰電池充電診斷系統</div>
  <div class="section-subtitle">適用微型電動車鋰電池充電時間、SOC 與充電曲線判讀</div>

  <label>電池電壓</label>
  <select id="li_vtype" onchange="li_updateCapacityOptions()">
    <option value="58">48V</option>
    <option value="60">60V</option>
    <option value="72">72V</option>
    <option value="76">76V</option>
  </select>

  <label>電池容量</label>
  <select id="li_cap" onchange="li_updateChargerCurrent()"></select>

  <label>充電器電流 (A)</label>
  <select id="li_chargerCurrent" disabled></select>

  <label>電池安裝日期</label>
  <input id="li_installDate" type="date">

  <label>靜置電壓</label>
  <input id="li_voltage" type="number" step="0.1" placeholder="例如 49">

  <div class="small-note">
    建議充電前先打開電門查看儀表板電壓作為參考<br>
    ⚠ 專業建議：騎乘後務必靜置30分鐘以上再充電，避免高溫直接充電造成電池壽命縮短<br>
    （此步驟非常重要，請務必遵守）<br>
    靜置後再量測電壓，數據判讀會更準確
  </div>

  <button class="calc-btn" onclick="li_calc()">開始計算</button>

  <div id="li_errorBox" class="error-box"></div>
  <div class="result" id="li_result"></div>

  <div class="bar">
    <div id="li_batteryBar" class="bar-fill"></div>
  </div>
  <div id="li_statusText" class="status"></div>

  <canvas id="li_chart" height="240"></canvas>

  <div id="li_segment"></div>

  <footer>
    祥真一職人版權所有<br>
    <div class="stats-box">
      👀 已有 <span id="li_view"></span> 人使用本工具<br>
      🔋 完成 <span id="li_count"></span> 次電池計算
    </div>
  </footer>
</div>

<div id="leadBox" class="container hidden">
  <div class="section-title">祥真一職人鉛酸電池充電診斷系統</div>
  <div class="section-subtitle">適用微型電動車鉛酸電池健康度、充電模式與充電時間估算</div>

  <label>電池電壓</label>
  <select id="pb_vtype" onchange="pb_updateVoltageInputLimit(); pb_updateCapacityOptions()">
    <option value="48">48V</option>
    <option value="60">60V</option>
    <option value="72">72V</option>
  </select>

  <label>電池容量</label>
  <select id="pb_cap"></select>

  <label>電池安裝日期</label>
  <input id="pb_installDate" type="date">

  <label>靜置電壓</label>
  <input id="pb_voltage" type="number" step="0.1" placeholder="例如 45">

  <div class="small-note">
    建議充電前先打開電門查看儀表板電壓作為參考<br>
    ⚠ 專業建議：騎乘後務必靜置30分鐘以上再充電，避免高溫直接充電造成電池壽命縮短<br>
    （此步驟非常重要，請務必遵守）<br>
    靜置後再量測電壓，數據判讀會更準確
  </div>

  <button class="calc-btn" onclick="pb_calc()">開始計算</button>

  <div id="pb_errorBox" class="error-box"></div>
  <div class="result" id="pb_result"></div>

  <div class="bar">
    <div id="pb_batteryBar" class="bar-fill"></div>
  </div>
  <div id="pb_statusText" class="status"></div>

  <canvas id="pb_chart" height="240"></canvas>

  <div id="pb_segment"></div>

  <footer>
    祥真一職人版權所有<br>
    <div class="stats-box">
      👀 已有 <span id="pb_view"></span> 人使用本工具<br>
      🔋 完成 <span id="pb_count"></span> 次電池計算
    </div>
  </footer>
</div>

<div id="rangeBox" class="container hidden">
  <div class="section-title">祥真一職人續航距離評估系統</div>
  <div class="section-subtitle">依電池類型、電壓、容量、路況與載重估算微型電動車續航距離</div>

  <label>電池類型</label>
  <select id="rg_batteryType" onchange="rg_updateCapacity()">
    <option value="lead">鉛酸電池</option>
    <option value="lithium">鋰電池</option>
  </select>

  <label>電壓</label>
  <select id="rg_voltage" onchange="rg_updateCapacity()"></select>

  <label>容量</label>
  <select id="rg_capacity"></select>

  <label>電池使用年齡</label>
  <select id="rg_age"></select>

  <label>騎乘環境</label>
  <select id="rg_road">
    <option value="1">平路通勤</option>
    <option value="0.92">市區走停</option>
    <option value="0.85">山路 / 坡道</option>
  </select>

  <label>騎乘載重類型</label>
  <select id="rg_weight">
    <option value="1.03">單人輕量</option>
    <option value="1">單人一般</option>
    <option value="0.9">單人偏重</option>
    <option value="0.82">雙載 / 載貨</option>
  </select>

  <button class="calc-btn" onclick="rg_calculate()">開始計算</button>

  <div class="result" id="rg_output"></div>

  <div class="small-note">
    台南祥真一職人｜本系統為估算參數，實際續航依騎乘習慣、車況、胎壓、路段略有差異。<br>
    本系統採保守值設計。
  </div>

  <footer>
    祥真一職人版權所有<br>
    <div class="stats-box">
      👀 已有 <span id="rg_view"></span> 人使用本工具<br>
      🔋 完成 <span id="rg_count"></span> 次續航估算
    </div>
  </footer>
</div>

<script>
function switchTool(type){
  document.getElementById("lithiumBox").classList.toggle("hidden", type!=="lithium")
  document.getElementById("leadBox").classList.toggle("hidden", type!=="lead")
  document.getElementById("rangeBox").classList.toggle("hidden", type!=="range")

  document.getElementById("tabLithium").classList.toggle("active", type==="lithium")
  document.getElementById("tabLead").classList.toggle("active", type==="lead")
  document.getElementById("tabRange").classList.toggle("active", type==="range")
}

function updateSystemTime(){
  const now = new Date()
  const year = now.getFullYear()
  const month = String(now.getMonth()+1).padStart(2,"0")
  const day = String(now.getDate()).padStart(2,"0")
  let hour = now.getHours()
  const minute = String(now.getMinutes()).padStart(2,"0")
  const second = String(now.getSeconds()).padStart(2,"0")
  const period = hour >= 12 ? "下午" : "上午"
  hour = hour % 12
  if(hour === 0) hour = 12

  document.getElementById("systemTimeBox").innerHTML =
    "系統時間："+year+" / "+month+" / "+day+"　"+period+" "+hour+":"+minute+":"+second
}

function formatTimeRange(date){
  let h = date.getHours()
  let m = date.getMinutes()
  const period = h >= 12 ? "下午" : "上午"
  h = h % 12
  if(h === 0) h = 12
  return period + " " + h + "點" + String(m).padStart(2,"0") + "分"
}

function loadSystemStats(){
  fetch("https://api.counterapi.dev/v1/xiangzhen/views/up")
  .then(res=>res.json())
  .then(data=>{
    document.getElementById("systemViews").innerText = data.count
  })
  .catch(()=>{
    document.getElementById("systemViews").innerText = "讀取失敗"
  })

  fetch("https://api.counterapi.dev/v1/xiangzhen/calc")
  .then(res=>res.json())
  .then(data=>{
    document.getElementById("systemCalc").innerText = data.count
  })
  .catch(()=>{
    document.getElementById("systemCalc").innerText = "讀取失敗"
  })
}

function increaseSystemCalcCounter(){
  fetch("https://api.counterapi.dev/v1/xiangzhen/calc/up")
  .then(res=>res.json())
  .then(data=>{
    document.getElementById("systemCalc").innerText = data.count
  })
  .catch(()=>{})
}

let li_view=localStorage.getItem("li_view")||0
li_view++
localStorage.setItem("li_view",li_view)
document.getElementById("li_view").innerText=li_view

let li_count=localStorage.getItem("li_count")||0
document.getElementById("li_count").innerText=li_count

let pb_view=localStorage.getItem("pb_view")||0
pb_view++
localStorage.setItem("pb_view",pb_view)
document.getElementById("pb_view").innerText=pb_view

let pb_count=localStorage.getItem("pb_count")||0
document.getElementById("pb_count").innerText=pb_count

let rg_view=localStorage.getItem("rg_view")||0
rg_view++
localStorage.setItem("rg_view",rg_view)
document.getElementById("rg_view").innerText=rg_view

let rg_count=localStorage.getItem("rg_count")||0
document.getElementById("rg_count").innerText=rg_count

function getHealthBadge(healthPercent){
  if(healthPercent >= 90) return "<span class='health-a'>🟢 極佳</span>"
  if(healthPercent >= 70) return "<span class='health-b'>🟢 正常</span>"
  if(healthPercent >= 50) return "<span class='health-c'>🟡 建議觀察</span>"
  if(healthPercent >= 35) return "<span class='health-d'>🟠 建議檢測</span>"
  return "<span class='health-e'>🔴 建議更換</span>"
}

const li_lithiumData={
  58:{full:58.0, charger:58.4, currents:{12:3,16:3,20:3,30:5,40:8,50:8}, low:45.0, minInput:43.0},
  60:{full:71.0, charger:71.4, currents:{20:3,30:5,40:8,50:8}, low:56.0, minInput:54.0},
  72:{full:84.0, charger:84.2, currents:{30:5,40:8,50:8}, low:65.5, minInput:63.0},
  76:{full:88.0, charger:88.2, currents:{30:5,40:8,50:8}, low:68.5, minInput:66.0}
}

const li_socCurve={
  58:[[45.0,5],[46.5,10],[48.0,20],[49.5,30],[51.0,45],[52.5,60],[54.0,75],[55.5,85],[57.0,95],[58.0,100]],
  60:[[56.0,5],[57.5,10],[59.5,20],[61.5,30],[63.5,45],[65.5,60],[67.0,75],[68.5,85],[70.0,95],[71.0,100]],
  72:[[65.5,5],[67.0,10],[69.0,20],[71.5,30],[74.0,45],[76.5,60],[78.5,75],[80.5,85],[82.5,95],[84.0,100]],
  76:[[68.5,5],[70.5,10],[72.5,20],[75.0,30],[77.5,45],[80.0,60],[82.5,75],[84.5,85],[86.5,95],[88.0,100]]
}

const li_socPercent=[0,20,40,60,80,100]
let li_chart=null
let li_chartAnimationTimer=null

function li_clearFieldErrors(){
  document.getElementById("li_vtype").classList.remove("input-error")
  document.getElementById("li_cap").classList.remove("input-error")
  document.getElementById("li_chargerCurrent").classList.remove("input-error")
  document.getElementById("li_installDate").classList.remove("input-error")
  document.getElementById("li_voltage").classList.remove("input-error")
}

function li_showError(message, fieldId){
  const box=document.getElementById("li_errorBox")
  box.style.display="block"
  box.innerHTML="⚠ "+message
  li_clearFieldErrors()
  if(fieldId){
    const field=document.getElementById(fieldId)
    field.classList.add("input-error")
    field.focus()
  }
}

function li_clearError(){
  const box=document.getElementById("li_errorBox")
  box.style.display="none"
  box.innerHTML=""
  li_clearFieldErrors()
}

function li_updateCapacityOptions(){
  const v=parseInt(document.getElementById("li_vtype").value)
  const capSelect=document.getElementById("li_cap")
  capSelect.innerHTML=""

  let capacities=[]
  if(v===58) capacities=[12,16,20,30,40,50]
  if(v===60) capacities=[20,30,40,50]
  if(v===72) capacities=[30,40,50]
  if(v===76) capacities=[30,40,50]

  capacities.forEach(c=>{
    const opt=document.createElement("option")
    opt.value=c
    opt.text=c+"Ah"
    capSelect.appendChild(opt)
  })

  li_updateChargerCurrent()
  li_updateVoltageInputLimit()
}

function li_updateChargerCurrent(){
  const v=parseInt(document.getElementById("li_vtype").value)
  const cap=parseInt(document.getElementById("li_cap").value)
  const charger=document.getElementById("li_chargerCurrent")
  charger.innerHTML=""
  const current=li_lithiumData[v].currents[cap]
  const opt=document.createElement("option")
  opt.value=current
  opt.text=current+"A"
  charger.appendChild(opt)
}

function li_updateVoltageInputLimit(){
  const type=parseInt(document.getElementById("li_vtype").value)
  const voltageInput=document.getElementById("li_voltage")
  const minV=li_lithiumData[type].minInput
  const maxV=li_lithiumData[type].full
  voltageInput.min=minV
  voltageInput.max=maxV
  voltageInput.placeholder="請輸入 "+minV+" ~ "+maxV+" V"
}

function li_getSOC(voltage,type){
  const table=li_socCurve[type]
  for(let i=0;i<table.length-1;i++){
    const v1=table[i][0]
    const s1=table[i][1]
    const v2=table[i+1][0]
    const s2=table[i+1][1]
    if(voltage>=v1 && voltage<=v2){
      const ratio=(voltage-v1)/(v2-v1)
      return s1+(s2-s1)*ratio
    }
  }
  if(voltage<table[0][0]) return 0
  if(voltage>table[table.length-1][0]) return 100
  return 0
}

function li_getHealthFromDate(dateStr){
  let months=Math.floor((new Date()-new Date(dateStr))/1000/3600/24/30)
  if(months<0) months=0
  if(months>=24) months=24

  let health=1
  if(months<=6) health = 0.95 - (months/6)*0.05
  else if(months<=12) health = 0.9 - ((months-6)/6)*0.25
  else if(months<=18) health = 0.65 - ((months-12)/6)*0.15
  else health = 0.5 - ((months-18)/6)*0.15

  if(health<0.3) health=0.3
  return health
}

function li_getChargeModeBySoc(soc){
  if(soc < 80) return "CC 恒流充電"
  if(soc < 95) return "CV 恒壓充電"
  return "尾段平衡 / 接近充滿"
}

function li_calc(){
  increaseSystemCalcCounter()
  li_clearError()

  const vtypeSelect=document.getElementById("li_vtype")
  const capSelect=document.getElementById("li_cap")
  const chargerSelect=document.getElementById("li_chargerCurrent")
  const installDate=document.getElementById("li_installDate").value
  const voltageText=document.getElementById("li_voltage").value

  if(!vtypeSelect.value){ li_showError("請選擇電池電壓","li_vtype"); return }
  if(!capSelect.value){ li_showError("請選擇電池容量","li_cap"); return }
  if(!chargerSelect.value){ li_showError("請確認充電器電流","li_chargerCurrent"); return }
  if(!installDate){ li_showError("請選擇電池安裝日期","li_installDate"); return }
  if(voltageText===""){ li_showError("請輸入靜置電壓","li_voltage"); return }

  const type=parseInt(vtypeSelect.value)
  const cap=parseFloat(capSelect.value)
  const voltage=parseFloat(voltageText)
  const charger=parseFloat(chargerSelect.value)

  const minV=li_lithiumData[type].minInput
  const maxV=li_lithiumData[type].full

  if(isNaN(voltage)){ li_showError("靜置電壓格式錯誤","li_voltage"); return }

  if(voltage<minV || voltage>maxV){
    li_showError("靜置電壓輸入錯誤，"+vtypeSelect.options[vtypeSelect.selectedIndex].text+" 可輸入範圍為 "+minV+"V ~ "+maxV+"V","li_voltage")
    return
  }

  const health=li_getHealthFromDate(installDate)
  const healthPercent=(health*100).toFixed(0)

  let months=Math.floor((new Date()-new Date(installDate))/1000/3600/24/30)
  if(months<0) months=0
  const years=Math.floor(months/12)
  const remainMonths=months%12

  let ageText=""
  if(years<=0){
    ageText=remainMonths+" 個月"
  }else if(remainMonths===0){
    ageText=years+" 年"
  }else{
    ageText=years+" 年 "+remainMonths+" 個月"
  }

  const soc=li_getSOC(voltage,type)
  const remain=cap*(100-soc)/100
  const baseTime=(remain/charger)*1.08*(1 + (1-health)*0.12)
  const minTime=baseTime*0.93
  const maxTime=baseTime*1.08

  const finishMin=new Date(Date.now()+minTime*3600000)
  const finishMax=new Date(Date.now()+maxTime*3600000)
  const finishTextMin=formatTimeRange(finishMin)
  const finishTextMax=formatTimeRange(finishMax)

  let warn=""
  if(voltage<=li_lithiumData[type].low){
    warn="<div class='warning'>⚠ 電壓過低，電量幾乎耗盡</div>"
  }

  document.getElementById("li_result").innerHTML=
    "剩餘電量 <span class='info-strong'>"+soc.toFixed(1)+"%</span><br>"+
    "電池健康度 <span class='info-strong'>"+healthPercent+"%</span><br>"+
    "健康判定 <span class='info-strong'>"+getHealthBadge(parseFloat(healthPercent))+"</span><br>"+
    "電池年齡 <span class='info-strong'>"+ageText+"</span><br>"+
    "目前充電模式 <span class='info-strong'>"+li_getChargeModeBySoc(soc)+"</span><br>"+
    "預估充電時間 <span class='info-strong'>約 "+minTime.toFixed(1)+" ～ "+maxTime.toFixed(1)+" 小時</span><br>"+
    "預計完成時間 <span class='info-strong'>約 "+finishTextMin+" ～ "+finishTextMax+"</span><br>"+
    warn+
    "<br>提醒：騎乘後請靜置30分鐘再充電"+
    "<div class='small-note'>※ 充電時間為預估區間，鋰電理論值主要以 電池容量 Ah ÷ 充電器電流 A 為基礎，實際仍會依剩餘電量、電池狀況與末段充電時間略有差異。</div>"+
    "<div class='notice-card'>"+
    "<div class='notice-title'>到店檢測提醒</div>"+
    "<div class='notice-text'>若檢測結果顯示電池老化或續航下降，歡迎到店免費檢測。</div>"+
    "<div class='notice-store'>台南永康｜祥真一職人二輪電動車</div>"+
    "</div>"

  document.getElementById("li_batteryBar").style.width=soc+"%"

  let status="🟢 電量正常"
  if(soc<20) status="🔴 電量過低"
  else if(soc<40) status="🟡 電量偏低"
  else if(soc>=90) status="🔵 接近滿電"
  document.getElementById("li_statusText").innerHTML=status

  li_count++
  localStorage.setItem("li_count",li_count)
  document.getElementById("li_count").innerText=li_count

  li_drawChart(type,soc)
  li_buildSegment(cap,charger,health,soc)
}

function li_getVoltageAtSOC(type,targetSoc){
  const curve=li_socCurve[type]
  for(let i=0;i<curve.length-1;i++){
    const v1=curve[i][0], s1=curve[i][1]
    const v2=curve[i+1][0], s2=curve[i+1][1]
    if(targetSoc>=s1 && targetSoc<=s2){
      const ratio=(targetSoc-s1)/(s2-s1)
      return v1+(v2-v1)*ratio
    }
  }
  if(targetSoc<=curve[0][1]) return curve[0][0]
  return curve[curve.length-1][0]
}

function li_drawChart(type,startSoc){
  const fullCurve=[]
  const progressCurve=[]
  const currentPoint=[]

  for(let i=0;i<li_socPercent.length;i++){
    const targetSoc=li_socPercent[i]
    const voltagePoint=li_getVoltageAtSOC(type,targetSoc)
    fullCurve.push({x:targetSoc,y:voltagePoint})
    if(targetSoc>=Math.ceil(startSoc/20)*20){
      progressCurve.push({x:targetSoc,y:voltagePoint})
    }
  }

  currentPoint.push({
    x:startSoc,
    y:li_getVoltageAtSOC(type,startSoc)
  })

  const ctx=document.getElementById("li_chart").getContext("2d")

  if(li_chartAnimationTimer){
    clearInterval(li_chartAnimationTimer)
    li_chartAnimationTimer=null
  }

  if(li_chart) li_chart.destroy()

  li_chart=new Chart(ctx,{
    type:"line",
    data:{
      datasets:[
        {
          label:"新電池曲線",
          data:fullCurve,
          borderColor:"#888",
          borderWidth:3,
          tension:0.35,
          pointRadius:5,
          pointHoverRadius:7,
          parsing:false,
          fill:false
        },
        {
          label:"充電進度",
          data:[],
          borderColor:"green",
          borderWidth:4,
          tension:0.35,
          pointBackgroundColor:"red",
          pointBorderColor:"green",
          pointRadius:6,
          pointHoverRadius:8,
          parsing:false,
          fill:false
        },
        {
          label:"目前位置",
          data:currentPoint,
          showLine:false,
          backgroundColor:"red",
          borderColor:"red",
          pointRadius:8,
          pointHoverRadius:10,
          parsing:false
        }
      ]
    },
    options:{
      responsive:true,
      animation:{duration:600,easing:"easeOutQuart"},
      interaction:{mode:"nearest",axis:"xy",intersect:false},
      plugins:{
        legend:{labels:{font:{size:14}}},
        tooltip:{
          callbacks:{
            title:function(context){
              const soc=context[0].raw.x
              return "SOC " + soc.toFixed(1) + "%"
            },
            label:function(context){
              return context.dataset.label+"： "+context.raw.y.toFixed(1)+" V"
            },
            afterBody:function(context){
              const soc=context[0].raw.x
              return "充電模式： "+li_getChargeModeBySoc(soc)
            }
          }
        }
      },
      scales:{
        x:{
          type:"linear",
          min:0,
          max:100,
          title:{display:true,text:"SOC (%)"},
          grid:{color:"#e5e5e5"},
          ticks:{stepSize:20,callback:(value)=>value+"%"}
        },
        y:{
          title:{display:true,text:"電壓 V"},
          grid:{color:"#e5e5e5"}
        }
      }
    }
  })

  let step=0
  li_chartAnimationTimer=setInterval(()=>{
    if(step >= progressCurve.length){
      clearInterval(li_chartAnimationTimer)
      li_chartAnimationTimer=null
      return
    }
    li_chart.data.datasets[1].data.push(progressCurve[step])
    li_chart.update()
    step++
  },700)
}

function li_buildSegment(cap,current,health,startSoc){
  let html="<table><tr><td>區段</td><td>充電時間</td></tr>"

  let points=[startSoc]
  li_socPercent.forEach(p=>{
    if(p>startSoc) points.push(p)
  })
  if(points[points.length-1]!==100) points.push(100)

  for(let i=0;i<points.length-1;i++){
    const from=points[i]
    const to=points[i+1]
    const diff=to-from
    const ah=cap*(diff/100)
    const t=(ah/current)*1.08*(1 + (1-health)*0.12)

    html+="<tr><td>"+from.toFixed(1)+"% → "+to.toFixed(0)+"%</td><td>"+t.toFixed(2)+" 小時</td></tr>"
  }

  html+="</table>"
  document.getElementById("li_segment").innerHTML=html
}

const pb_voltageLimit={
  48:{min:44,max:52,low:44},
  60:{min:55,max:65,low:55},
  72:{min:66,max:78,low:66}
}

const pb_socTable={
  48:[42,44,46,48,50,52],
  60:[53,56,58,60,62,65],
  72:[63,67,70,72,75,78]
}

const pb_socPercent=[0,20,40,60,80,100]
let pb_chart=null
let pb_chartAnimationTimer=null

function pb_clearFieldErrors(){
  document.getElementById("pb_vtype").classList.remove("input-error")
  document.getElementById("pb_cap").classList.remove("input-error")
  document.getElementById("pb_installDate").classList.remove("input-error")
  document.getElementById("pb_voltage").classList.remove("input-error")
}

function pb_showError(message, fieldId){
  const box=document.getElementById("pb_errorBox")
  box.style.display="block"
  box.innerHTML="⚠ "+message
  pb_clearFieldErrors()
  if(fieldId){
    const field=document.getElementById(fieldId)
    field.classList.add("input-error")
    field.focus()
  }
}

function pb_clearError(){
  const box=document.getElementById("pb_errorBox")
  box.style.display="none"
  box.innerHTML=""
  pb_clearFieldErrors()
}

function pb_updateVoltageInputLimit(){
  const type=document.getElementById("pb_vtype").value
  const voltageInput=document.getElementById("pb_voltage")
  const minV=pb_voltageLimit[type].min
  const maxV=pb_voltageLimit[type].max
  voltageInput.min=minV
  voltageInput.max=maxV
  voltageInput.placeholder="請輸入 "+minV+" ~ "+maxV+" V"
}

function pb_updateCapacityOptions(){
  const type=document.getElementById("pb_vtype").value
  const capSelect=document.getElementById("pb_cap")
  capSelect.innerHTML=""

  let capacities=[]
  if(type==="48") capacities=[12,13,15,20,24,30]
  if(type==="60") capacities=[20,24,30]
  if(type==="72") capacities=[20,24,30]

  capacities.forEach(c=>{
    const opt=document.createElement("option")
    opt.value=c
    opt.text=c+"Ah"
    capSelect.appendChild(opt)
  })
}

function pb_getLeadChargeModeBySoc(soc){
  if(soc < 40) return "初期補電"
  if(soc < 80) return "中段充電"
  if(soc < 95) return "吸收充電"
  return "接近充滿"
}

function pb_getBatteryAgeText(months){
  const years=Math.floor(months/12)
  const remainMonths=months%12
  if(years<=0) return remainMonths+" 個月"
  if(remainMonths===0) return years+" 年"
  return years+" 年 "+remainMonths+" 個月"
}

function pb_getBatteryAdvice(months, health){
  if(months < 12) return "狀況正常"
  if(months < 18) return "建議持續觀察"
  if(months < 24) return "建議檢測"
  if(health <= 0.40) return "建議更換"
  return "建議留意使用狀況"
}

function pb_calc(){
  increaseSystemCalcCounter()
  pb_clearError()

  const type=document.getElementById("pb_vtype").value
  const cap=parseFloat(document.getElementById("pb_cap").value)
  const installDate=document.getElementById("pb_installDate").value
  const voltageText=document.getElementById("pb_voltage").value

  if(!type){ pb_showError("請選擇電池電壓","pb_vtype"); return }
  if(!cap){ pb_showError("請選擇電池容量","pb_cap"); return }
  if(!installDate){ pb_showError("請選擇電池安裝日期","pb_installDate"); return }
  if(voltageText===""){ pb_showError("請輸入靜置電壓","pb_voltage"); return }

  const v=parseFloat(voltageText)
  if(isNaN(v)){ pb_showError("靜置電壓格式錯誤","pb_voltage"); return }

  const minV=pb_voltageLimit[type].min
  const maxV=pb_voltageLimit[type].max

  if(v<minV || v>maxV){
    pb_showError(type+"V 靜置電壓必須介於 "+minV+"V ~ "+maxV+"V","pb_voltage")
    return
  }

  let health=1
  let months=0

  if(installDate){
    months=Math.floor((new Date()-new Date(installDate))/1000/3600/24/30)
    if(months < 0) months=0

    if(months <= 6){
      health = 1.00 - (months/6)*0.10
    }
    else if(months <= 12){
      health = 0.90 - ((months-6)/6)*0.15
    }
    else if(months <= 18){
      health = 0.75 - ((months-12)/6)*0.20
    }
    else if(months <= 24){
      health = 0.55 - ((months-18)/6)*0.15
    }
    else if(months <= 30){
      health = 0.40 - ((months-24)/6)*0.05
    }
    else{
      health = 0.30
    }

    if(health < 0.30) health = 0.30
  }

  const healthPercent=(health*100).toFixed(0)
  const voltList=pb_socTable[type]
  let soc=0

  for(let i=0;i<voltList.length-1;i++){
    if(v>=voltList[i] && v<=voltList[i+1]){
      const ratio=(v-voltList[i])/(voltList[i+1]-voltList[i])
      soc=pb_socPercent[i]+ratio*(pb_socPercent[i+1]-pb_socPercent[i])
    }
  }

  let current=2.8
  if(type==="48" && cap<=15) current=1.8
  if(type==="48" && cap>15) current=2.8
  if(type==="60") current=2.8
  if(type==="72") current=3

  const remain=cap*(100-soc)/100
  const baseTime=(remain/current)*1.18*(1 + (1-health)*0.18)
  const minTime=baseTime*0.95
  const maxTime=baseTime*1.12

  const finishMin=new Date(Date.now()+minTime*3600000)
  const finishMax=new Date(Date.now()+maxTime*3600000)
  const finishTextMin=formatTimeRange(finishMin)
  const finishTextMax=formatTimeRange(finishMax)

  let warn=""
  if(v<=pb_voltageLimit[type].low){
    warn="<div class='warning'>⚠ 電壓過低</div>"
  }

  const ageText=pb_getBatteryAgeText(months)
  const adviceText=pb_getBatteryAdvice(months, health)

  document.getElementById("pb_result").innerHTML=
    "剩餘電量 <span class='info-strong'>"+soc.toFixed(1)+"%</span><br>"+
    "電池健康度 <span class='info-strong'>"+healthPercent+"%</span><br>"+
    "健康判定 <span class='info-strong'>"+getHealthBadge(parseFloat(healthPercent))+"</span><br>"+
    "電池年齡 <span class='info-strong'>"+ageText+"</span><br>"+
    "建議狀態 <span class='info-strong'>"+adviceText+"</span><br>"+
    "目前充電模式 <span class='info-strong'>"+pb_getLeadChargeModeBySoc(soc)+"</span><br>"+
    "預估充電時間 <span class='info-strong'>約 "+minTime.toFixed(1)+" ～ "+maxTime.toFixed(1)+" 小時</span><br>"+
    "預計完成時間 <span class='info-strong'>約 "+finishTextMin+" ～ "+finishTextMax+"</span><br>"+
    warn+
    "<br>※ 健康度為推估值，實際仍需依電池負載測試判斷"+
    "<br>提醒：騎乘後請靜置30分鐘再充電"+
    "<div class='small-note'>※ 充電時間為預估區間，鉛酸理論值同樣以 電池容量 Ah ÷ 充電器電流 A 為基礎，但因後段吸收充電較明顯，實際通常會比理論值再長一些。</div>"+
    "<div class='notice-card'>"+
    "<div class='notice-title'>到店檢測提醒</div>"+
    "<div class='notice-text'>若檢測結果顯示電池老化或續航下降，歡迎到店免費檢測。</div>"+
    "<div class='notice-store'>台南永康｜祥真一職人二輪電動車</div>"+
    "</div>"

  document.getElementById("pb_batteryBar").style.width=soc+"%"

  let status="🟢 電量正常"
  if(soc<20) status="🔴 電量過低"
  else if(soc<40) status="🟡 電量偏低"
  else if(soc>=90) status="🔵 接近滿電"
  document.getElementById("pb_statusText").innerHTML=status

  pb_count++
  localStorage.setItem("pb_count",pb_count)
  document.getElementById("pb_count").innerText=pb_count

  pb_drawChart(voltList,soc,health)
  pb_buildSegment(cap,current,health,soc)
}

function pb_drawChart(voltList,startSoc,health){
  const fullCurve=[]
  const progressCurve=[]
  const oldCurve=[]
  const currentPoint=[]

  for(let i=0;i<pb_socPercent.length;i++){
    fullCurve.push({x:pb_socPercent[i], y:voltList[i]})
    oldCurve.push({x:pb_socPercent[i], y:voltList[i]*health})
    if(pb_socPercent[i] >= Math.ceil(startSoc/20)*20){
      progressCurve.push({x:pb_socPercent[i], y:voltList[i]})
    }
  }

  for(let i=0;i<voltList.length-1;i++){
    if(startSoc>=pb_socPercent[i] && startSoc<=pb_socPercent[i+1]){
      const ratio=(startSoc-pb_socPercent[i])/(pb_socPercent[i+1]-pb_socPercent[i])
      const y=voltList[i]+(voltList[i+1]-voltList[i])*ratio
      currentPoint.push({x:startSoc,y:y})
      break
    }
  }

  const ctx=document.getElementById("pb_chart").getContext("2d")

  if(pb_chartAnimationTimer){
    clearInterval(pb_chartAnimationTimer)
    pb_chartAnimationTimer=null
  }

  if(pb_chart) pb_chart.destroy()

  pb_chart=new Chart(ctx,{
    type:"line",
    data:{
      datasets:[
        {
          label:"新電池曲線",
          data:fullCurve,
          borderColor:"#888",
          borderWidth:3,
          tension:0.35,
          pointRadius:5,
          pointHoverRadius:7,
          parsing:false,
          fill:false
        },
        {
          label:"老化電池曲線",
          data:oldCurve,
          borderColor:"#f39c12",
          borderWidth:2,
          borderDash:[6,6],
          tension:0.35,
          pointRadius:4,
          parsing:false,
          fill:false
        },
        {
          label:"充電進度",
          data:[],
          borderColor:"green",
          borderWidth:4,
          tension:0.35,
          pointBackgroundColor:"red",
          pointBorderColor:"green",
          pointRadius:6,
          pointHoverRadius:8,
          parsing:false,
          fill:false
        },
        {
          label:"目前位置",
          data:currentPoint,
          showLine:false,
          backgroundColor:"red",
          borderColor:"red",
          pointRadius:8,
          pointHoverRadius:10,
          parsing:false
        }
      ]
    },
    options:{
      responsive:true,
      animation:{duration:600,easing:"easeOutQuart"},
      interaction:{mode:"nearest",axis:"xy",intersect:false},
      plugins:{
        legend:{labels:{font:{size:14}}},
        tooltip:{
          callbacks:{
            title:function(context){
              const soc=context[0].raw.x
              return "SOC " + soc.toFixed(1) + "%"
            },
            label:function(context){
              return context.dataset.label+"： "+context.raw.y.toFixed(1)+" V"
            },
            afterBody:function(context){
              const soc=context[0].raw.x
              return "充電模式： "+pb_getLeadChargeModeBySoc(soc)
            }
          }
        }
      },
      scales:{
        x:{
          type:"linear",
          min:0,
          max:100,
          title:{display:true,text:"SOC (%)"},
          grid:{color:"#e5e5e5"},
          ticks:{stepSize:20,callback:(value)=>value+"%"}
        },
        y:{
          title:{display:true,text:"電壓 V"},
          grid:{color:"#e5e5e5"}
        }
      }
    }
  })

  let step=0
  pb_chartAnimationTimer=setInterval(()=>{
    if(step >= progressCurve.length){
      clearInterval(pb_chartAnimationTimer)
      pb_chartAnimationTimer=null
      return
    }
    pb_chart.data.datasets[2].data.push(progressCurve[step])
    pb_chart.update()
    step++
  },700)
}

function pb_buildSegment(cap,current,health,startSoc){
  let html="<table><tr><td>區段</td><td>充電時間</td></tr>"
  const agingFactor=(1 + (1-health)*0.18)

  for(let i=0;i<pb_socPercent.length-1;i++){
    if(pb_socPercent[i]>=startSoc){
      const diff=pb_socPercent[i+1]-pb_socPercent[i]
      const ah=cap*(diff/100)
      const t=(ah/current)*1.18*agingFactor
      html+="<tr><td>"+pb_socPercent[i]+"% → "+pb_socPercent[i+1]+"%</td><td>"+t.toFixed(2)+" 小時</td></tr>"
    }
  }

  html+="</table>"
  document.getElementById("pb_segment").innerHTML=html
}

function rg_updateAgeOptions(){
  const ageSelect=document.getElementById("rg_age")
  ageSelect.innerHTML=""

  const options = [
    {text:'全新', value:1.00},
    {text:'使用3個月', value:0.95},
    {text:'使用6個月', value:0.90},
    {text:'使用約1年', value:0.85},
    {text:'使用1年6個月', value:0.78},
    {text:'使用2年以上', value:0.70}
  ]

  options.forEach(function(item){
    const opt=document.createElement("option")
    opt.value=item.value
    opt.text=item.text
    ageSelect.appendChild(opt)
  })
}

function rg_updateCapacity(){
  const batteryType=document.getElementById("rg_batteryType").value
  const voltageSelect=document.getElementById("rg_voltage")
  const currentVoltage=voltageSelect.value
  const capacitySelect=document.getElementById("rg_capacity")

  voltageSelect.innerHTML=""
  capacitySelect.innerHTML=""

  if(batteryType==="lead"){
    ;["48","60","72"].forEach(function(v){
      const opt=document.createElement("option")
      opt.value=v
      opt.text=v+"V"
      voltageSelect.appendChild(opt)
    })

    if(["48","60","72"].includes(currentVoltage)){
      voltageSelect.value=currentVoltage
    }else{
      voltageSelect.value="48"
    }

    const voltage=voltageSelect.value
    let options=[]

    if(voltage==="48"){ options=[13,15,20,24,30] }
    if(voltage==="60"){ options=[20,24,30] }
    if(voltage==="72"){ options=[20,24,30] }

    rg_updateAgeOptions()

    options.forEach(function(ah){
      const opt=document.createElement("option")
      opt.value=ah
      opt.text=ah+"Ah"
      capacitySelect.appendChild(opt)
    })

  }else{
    ;["48","60","72","76"].forEach(function(v){
      const opt=document.createElement("option")
      opt.value=v
      opt.text=v+"V"
      voltageSelect.appendChild(opt)
    })

    if(["48","60","72","76"].includes(currentVoltage)){
      voltageSelect.value=currentVoltage
    }else{
      voltageSelect.value="48"
    }

    const voltage=voltageSelect.value
    let options=[]

    if(voltage==="48"){ options=[12,16,20,30,40,50] }
    if(voltage==="60"){ options=[20,30,40,50] }
    if(voltage==="72"){ options=[30,40,50] }
    if(voltage==="76"){ options=[30,40,50] }

    rg_updateAgeOptions()

    options.forEach(function(ah){
      const opt=document.createElement("option")
      opt.value=ah
      opt.text=ah+"Ah"
      capacitySelect.appendChild(opt)
    })
  }
}

function rg_calculate(){
  increaseSystemCalcCounter()
  rg_count++
  localStorage.setItem("rg_count",rg_count)
  document.getElementById("rg_count").innerText=rg_count

  const voltage=parseInt(document.getElementById("rg_voltage").value)
  const ah=parseInt(document.getElementById("rg_capacity").value)
  const batteryType=document.getElementById("rg_batteryType").value
  const ageFactor=parseFloat(document.getElementById("rg_age").value)
  const roadFactor=parseFloat(document.getElementById("rg_road").value)
  const weightFactor=parseFloat(document.getElementById("rg_weight").value)

  const rawWh=voltage*ah
  let efficiency=batteryType==="lead" ? 0.78 : 0.90
  const effectiveWh=rawWh*efficiency*ageFactor*roadFactor*weightFactor

  let consumption=24
  if(voltage===48) consumption=22
  if(voltage===60) consumption=25
  if(voltage===72) consumption=30
  if(voltage===76) consumption=30

  let range=effectiveWh/consumption
  if((voltage===72 || voltage===76) && range>100){ range=100 }
  range=range.toFixed(1)

  let halfYearDecay=batteryType==="lead" ? 12 : 8
  let oneYearDecay=batteryType==="lead" ? 25 : 18
  let cycleInfo=batteryType==="lead" ? "約 250～400 次循環" : "約 600～900 次循環"

  document.getElementById("rg_output").innerHTML=
    "🔋 電池總電量：<span class='info-strong'>"+rawWh+" Wh</span><br>"+
    "⚙ 有效可用電量：約 <span class='info-strong'>"+effectiveWh.toFixed(0)+" Wh</span><br><br>"+
    "🛣 預估安全續航距離：約 <span class='info-strong'>"+range+" km</span><br><br>"+
    "📉 電池衰退參考：<br>"+
    "半年：約 "+halfYearDecay+"%<br>"+
    "一年：約 "+oneYearDecay+"%<br><br>"+
    "🔄 預估循環壽命：<span class='info-strong'>"+cycleInfo+"</span><br>"+
    "<div class='small-note'>🔋⚠️ 電池壽命會因騎乘習慣、充電方式、環境溫度、濕度、灰塵與載重影響，每位車主實際狀況可能有所不同。</div>"+
    "<div class='notice-card'>"+
    "<div class='notice-title'>到店檢測提醒</div>"+
    "<div class='notice-text'>若評估結果顯示續航下降或電池衰退，歡迎到店免費檢測。</div>"+
    "<div class='notice-store'>台南永康｜祥真一職人二輪電動車</div>"+
    "</div>"
}

li_updateCapacityOptions()
pb_updateVoltageInputLimit()
pb_updateCapacityOptions()
rg_updateCapacity()
switchTool('lithium')

updateSystemTime()
setInterval(updateSystemTime,1000)
loadSystemStats()
</script>

</body>
</html>
