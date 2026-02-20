<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🛵 祥真一職人｜電池壽命與續航評估系統</title>

<style>
body{
    font-family: Arial;
    background:#0f0f0f;
    color:#fff;
    padding:20px;
}
.container{
    max-width:500px;
    margin:auto;
    background:#1a1a1a;
    padding:20px;
    border-radius:15px;
}
h2{
    text-align:center;
    color:#00ff99;
}
select,button{
    width:100%;
    padding:12px;
    margin-top:10px;
    border-radius:8px;
    border:none;
    font-size:16px;
}
button{
    background:#00ff99;
    color:#000;
    font-weight:bold;
}
.result{
    margin-top:20px;
    padding:15px;
    background:#222;
    border-radius:10px;
    line-height:1.6;
}
.footer{
    margin-top:20px;
    font-size:12px;
    text-align:center;
    color:#aaa;
}
</style>
</head>

<body>

<div class="container">
<h2>🛵祥真一職人 電池壽命與續航評估系統🛵</h2>

<label>電池類型</label>
<select id="batteryType" onchange="updateCapacity()">
<option value="lead">鉛酸電池</option>
<option value="lithium">鋰電池</option>
</select>

<label>電壓</label>
<select id="voltage" onchange="updateCapacity()">
<option value="48">48V</option>
<option value="60">60V</option>
<option value="72">72V</option>
</select>

<label>容量</label>
<select id="capacity"></select>

<label>使用狀況</label>
<select id="age"></select>

<label>騎乘環境</label>
<select id="road">
<option value="1">平路通勤</option>
<option value="0.92">市區走停</option>
<option value="0.85">山路 / 坡道</option>
</select>

<label>騎乘載重類型</label>
<select id="weight">
<option value="1.03">單人輕量</option>
<option value="1">單人一般</option>
<option value="0.9">單人偏重</option>
<option value="0.82">雙載 / 載貨</option>
</select>

<button onclick="calculate()">開始計算</button>

<div class="result" id="output"></div>

<div class="footer">
台南祥真一職人｜本系統為估算參數，實際續航依騎乘習慣與車況(胎壓)路段略有差異<br>
© 祥真一職人 版權所有
</div>
</div>

<script>
function updateCapacity(){
    const batteryType = document.getElementById("batteryType").value;
    const voltage = document.getElementById("voltage").value;
    const capacitySelect = document.getElementById("capacity");
    capacitySelect.innerHTML = "";

    let options = [];

    if(batteryType === "lead"){
        options = [13,15,20,30];
        updateAgeOptions(['全新','一年以上']);
    }else{
        if(voltage == "48"){ options = [12,16,20,30,40]; }
        if(voltage == "60"){ options = [12,16,20,30,40,50]; }
        if(voltage == "72"){ options = [12,16,30,40,50]; }
        updateAgeOptions(['全新','使用約1年','使用2年以上']);
    }

    options.forEach(function(ah){
        let opt = document.createElement("option");
        opt.value = ah;
        opt.text = ah + "Ah";
        capacitySelect.appendChild(opt);
    });
}

function updateAgeOptions(list){
    const ageSelect = document.getElementById("age");
    ageSelect.innerHTML = "";
    list.forEach(function(item){
        let opt = document.createElement("option");
        if(item === '全新'){ opt.value = 1; }
        else if(item === '一年以上' || item === '使用約1年'){ opt.value = 0.88; }
        else if(item === '使用2年以上'){ opt.value = 0.75; }
        opt.text = item;
        ageSelect.appendChild(opt);
    });
}

function calculate(){
    const voltage = parseInt(document.getElementById("voltage").value);
    const ah = parseInt(document.getElementById("capacity").value);
    const batteryType = document.getElementById("batteryType").value;
    const ageFactor = parseFloat(document.getElementById("age").value);
    const roadFactor = parseFloat(document.getElementById("road").value);
    const weightFactor = parseFloat(document.getElementById("weight").value);

    const rawWh = voltage * ah;
    let efficiency = batteryType === "lead" ? 0.78 : 0.90;
    const effectiveWh = rawWh * efficiency * ageFactor * roadFactor * weightFactor;

    let consumption = 24;
    if(voltage == 48) consumption = 22;
    if(voltage == 60) consumption = 25;
    if(voltage == 72) consumption = 30;

    let range = effectiveWh / consumption;
    if(voltage == 72 && range > 100){ range = 100; }
    range = range.toFixed(1);

    let halfYearDecay = batteryType === "lead" ? 12 : 8;
    let oneYearDecay = batteryType === "lead" ? 25 : 18;
    let cycleInfo = batteryType === "lead" ? "約 250～400 次循環" : "約 600～900 次循環";

    document.getElementById("output").innerHTML = `
    🔋 電池總電量：${rawWh} Wh<br>
    ⚙ 有效可用電量：約 ${effectiveWh.toFixed(0)} Wh<br><br>

    🛣 預估安全續航距離：約 ${range} km

    <hr>
    📉 電池衰退參考：
    - 半年：約 ${halfYearDecay}%  
    - 一年：約 ${oneYearDecay}%

    <br>
    🔄 預估循環壽命：${cycleInfo}

    <p style="font-size:14px; color:#ccc; margin-top:10px;">
    🔋⚠️ 電池壽命會因受到騎乘習慣、充電方式、環境溫度、濕度、灰塵與載重影響，每位車主實際狀況可能有所不同。
    本系統為實際估算參數，數據採保守值設計。
    </p>
    `;
}

updateCapacity();
</script>

</body>
</html>
