<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RAMBLE.SU — Проверки</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{--orange:#ff6a00;--bg:#100c09;--card:#1b1410;--muted:#a99a90}
body{
 font-family:Arial,sans-serif;background:var(--bg);color:#fff;
 min-height:100vh;
 background-image:radial-gradient(ellipse at top,#3b1b09 0%,transparent 55%);
}
header{
 padding:22px 7%;display:flex;justify-content:space-between;
 align-items:center;border-bottom:1px solid #382014;
}
.logo{font-size:26px;font-weight:900;letter-spacing:2px}
.logo span{color:var(--orange)}
.status{color:#ffad73;font-size:12px}
main{max-width:950px;margin:65px auto;padding:0 20px}
.tag{color:var(--orange);font-size:12px;letter-spacing:3px;font-weight:bold}
h1{font-size:clamp(36px,7vw,65px);margin:15px 0}
h1 span{color:var(--orange)}
.subtitle{color:var(--muted);line-height:1.7;max-width:600px}
.panel{
 margin-top:35px;background:var(--card);border:1px solid #482817;
 border-radius:16px;padding:26px;
}
h2{font-size:21px;margin-bottom:10px}
label{display:block;color:#cbbab0;font-size:13px;margin:18px 0 8px}
input,select{
 width:100%;padding:14px;background:#100c09;color:white;
 border:1px solid #51301e;border-radius:9px;font-size:15px;outline:none;
}
input:focus,select:focus{border-color:var(--orange)}
button{
 width:100%;margin-top:20px;padding:15px;border:0;border-radius:9px;
 background:var(--orange);color:white;font-weight:bold;font-size:15px;
 cursor:pointer;transition:.2s;
}
button:hover{background:#e65e00;transform:translateY(-1px)}
.result{
 display:none;margin-top:20px;padding:17px;border-radius:10px;
 background:#26190f;border:1px solid #633719;line-height:1.7;
 overflow-wrap:anywhere;
}
.note{font-size:12px;color:var(--muted);margin-top:14px;line-height:1.6}
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:15px;margin-top:25px}
.card{padding:22px;background:#19120e;border:1px solid #382014;border-radius:12px}
.card b{color:var(--orange);display:block;margin-bottom:9px}
footer{text-align:center;color:#76665c;padding:35px 15px;font-size:12px}
footer span{color:var(--orange)}
</style>
</head>
<body>
<header>
 <div class="logo">RAMBLE<span>.SU</span></div>
 <div class="status">● SERVER PROJECT</div>
</header>

<main>
 <div class="tag">OFFICIAL COMMUNITY TOOL</div>
 <h1>Проверка <span>игроков.</span></h1>
 <p class="subtitle">
  Инструменты сообщества RAMBLE.SU.
  Введи игровой ник, чтобы сформировать карточку проверки.
 </p>

 <section class="panel">
  <h2>Проверка игрока</h2>
  <p class="subtitle">Minecraft Java Edition</p>

  <label for="nickname">Игровой ник</label>
  <input id="nickname" maxlength="16" placeholder="Например, Steve">

  <label for="reason">Тип проверки</label>
  <select id="reason">
   <option value="Проверка игрока">Общая проверка</option>
   <option value="Проверка на читы">Проверка на читы</option>
   <option value="Проверка жалобы">Проверка жалобы</option>
   <option value="Проверка нарушения правил">Нарушение правил</option>
  </select>

  <button onclick="checkPlayer()">Сформировать проверку</button>

  <div class="result" id="result" aria-live="polite"></div>
  <button id="copy" onclick="copyResult()" style="display:none">
   Скопировать результат
  </button>

  <p class="note">
   Внимание: эта форма не проверяет читы, историю банов или реальные
   данные аккаунта. Она только формирует карточку проверки.
  </p>
 </section>

 <div class="cards">
  <div class="card">
   <b>01 / COMMUNITY</b>
   <p>Инструменты для команды проекта.</p>
  </div>
  <div class="card">
   <b>02 / MODERATION</b>
   <p>Удобное оформление проверок игроков.</p>
  </div>
  <div class="card">
   <b>03 / RAMBLE.SU</b>
   <p>Честная игра и порядок на сервере.</p>
  </div>
 </div>
</main>

<footer>
 Сделано <span>R1gnazh</span> · RAMBLE.SU
</footer>

<script>
let report = "";

function checkPlayer(){
 const nick = document.getElementById("nickname").value.trim();
 const reason = document.getElementById("reason").value;
 const result = document.getElementById("result");
 const copy = document.getElementById("copy");

 if(!/^[a-zA-Z0-9_]{1,16}$/.test(nick)){
  result.style.display="block";
  result.textContent="Введи корректный Minecraft-ник (до 16 символов: латинские буквы, цифры и _).";
  copy.style.display="none";
  return;
 }

 report =
  "RAMBLE.SU — КАРТОЧКА ПРОВЕРКИ\n"+
  "Игрок: "+nick+"\n"+
  "Тип: "+reason+"\n"+
  "Статус: Требует проверки модератором\n"+
  "Создано через сайт RAMBLE.SU";

 result.style.display="block";
 result.textContent=report;
 copy.style.display="block";
}

async function copyResult(){
 try{
  await navigator.clipboard.writeText(report);
  document.getElementById("copy").textContent="Скопировано!";
 }catch(e){
  const area=document.createElement("textarea");
  area.value=report;
  document.body.appendChild(area);
  area.select();
  document.execCommand("copy");
  area.remove();
  document.getElementById("copy").textContent="Скопировано!";
 }
}
</script>
</body>
</html>
