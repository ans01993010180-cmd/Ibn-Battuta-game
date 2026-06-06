

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>رحلة ابن بطوطة</title>
<style>
body {
  margin: 0;
  background: #e8dcc6;
  font-family: 'Tajawal', sans-serif;
  overflow: hidden;
}
#game {
  width: 100vw;
  height: 100vh;
  background: url('https://i.imgur.com/old-map-texture.jpg') repeat;
  position: relative;
}
h1 {
  text-align: center;
  color: #5c3d2e;
  padding-top: 30px;
  font-size: 32px;
  text-shadow: 2px 2px #fff8e1;
}
.start-btn {
  display: block;
  margin: 50px auto;
  padding: 15px 40px;
  background: #8b5a2b;
  color: #fff8e1;
  border: 3px solid #5c3d2e;
  border-radius: 10px;
  font-size: 20px;
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);
}
.map-dot {
  position: absolute;
  width: 30px;
  height: 30px;
  background: #c0392b;
  border-radius: 50%;
  border: 2px solid #5c3d2e;
  cursor: pointer;
  animation: pulse 2s infinite;
}
@keyframes pulse {
 0%, 100% { transform: scale(1); }
 50% { transform: scale(1.2); }
}
.coin {
  position: absolute;
  font-size: 30px;
  animation: fall 1s ease-in;
}
@keyframes fall {
 0% { top: 50%; opacity: 1; }
 100% { top: 90%; opacity: 0; }
}
#coins-display {
  position: absolute;
  top: 20px;
  left: 20px;
  background: #8b5a2b;
  color: #ffd700;
  padding: 10px 20px;
  border-radius: 20px;
  font-size: 18px;
  border: 2px solid #5c3d2e;
}
</style>
</head>
<body>
<div id="game">
  <div id="coins-display">💰 <span id="coins">0</span></div>
  <h1>رحلة ابن بطوطة</h1>
  <p style="text-align:center; color:#5c3d2e">اجمع معلومات الرحالة واضرب رقم قياسي جديد!</p>
  <button class="start-btn" onclick="startGame()">ابدأ الرحلة</button>
  
  <div class="map-dot" style="top:40%; left:20%;" onclick="askQuestion('طنجة')"></div>
  <div class="map-dot" style="top:45%; left:28%;" onclick="askQuestion('مكة')"></div>
</div>

<!-- موسيقى عود -->
<audio id="oud-music" loop>
  <source src="https://cdn.pixabay.com/audio/2022/08/04/audio_8f3e3e6c5d.mp3" type="audio/mpeg">
</audio>

<script>
let coins = 0;
let synth = window.speechSynthesis;

function startGame() {
  document.getElementById('oud-music').play(); // 1. تشغيل موسيقى العود
  alert("مرحباً! أنت الآن ابن بطوطة سنة 1325م\nأول محطة: طنجة");
}

function speak(text) {
  // 2. صوت الراوي
  let msg = new SpeechSynthesisUtterance(text);
  msg.lang = 'ar-SA';
  msg.rate = 0.9;
  synth.speak(msg);
}

function dropCoins() {
  // 3. عملات ذهبية تطيح
  for(let i=0; i<5; i++) {
    setTimeout(() => {
      let coin = document.createElement('div');
      coin.className = 'coin';
      coin.innerHTML = '🪙';
      coin.style.left = Math.random() * 80 + 10 + '%';
      document.getElementById('game').appendChild(coin);
      setTimeout(() => coin.remove(), 1000);
    }, i * 200);
  }
}

function askQuestion(city) {
  let question = "ما اسم الكتاب اللي كتب فيه ابن بطوطة رحلاته؟\n1. ألف ليلة وليلة\n2. تحفة النظار\n3. مقدمة ابن خلدون";
  
  speak(question); // الصوت يقول السؤال
  let answer = prompt(question);
  
  if(answer == "2") {
    coins += 10;
    document.getElementById('coins').innerText = coins;
    dropCoins(); // العملات تطيح
    speak("إجابة صحيحة! ربحت 10 عملات ذهبية");
    alert("صحيح! ربحت 10 عملات ذهبية ✨\nرصيدك: " + coins + "\nالآن تقدر تسافر لمكة");
  } else {
    speak("إجابة خاطئة، حاول مرة ثانية");
    alert("حاول مرة ثانية! الإجابة: تحفة النظار");
  }
}
</script>
</body>
</html>

const questions = {
  "طنجة": { q: "ما اسم الكتاب اللي كتب فيه ابن بطوطة رحلاته؟", a: ["2", "تحفة", "نظار"] },
  "مكة": { q: "ماذا وصف ابن بطوطة عن الكعبة في طوافه الأول؟\n1. بنيت من الذهب\n2. كان الناس يطوفون ليل نهار\n3. ارتفاعها 50 متر", a: ["2", "ليل نهار"] },
  "القاهرة": { q: "ماذا قال عن نهر النيل؟\n1. ماؤه شفاء\n2. يجف في الصيف\n3. فيه تماسيح فقط", a: ["1", "شفاء"] }
};

function askQuestion(city) {
  let data = questions[city];
  if(!data) return;

  speak(data.q);
  setTimeout(() => {
    let answer = prompt(data.q);
    if (answer) {
      let normalized = answer.trim().toLowerCase();
      let correct = data.a.some(keyword => normalized.includes(keyword.toLowerCase()) || normalized === keyword);

      if (correct) {
        coins += 10;
        document.getElementById('coins').innerText = coins;
        dropCoins();
        speak("إجابة صحيحة! ربحت 10 عملات ذهبية");
        alert("صحيح! +10 عملات ✨ رصيدك: " + coins);
      } else {
        speak("إجابة خاطئة، حاول مرة ثانية");
        alert("الإجابة الصحيحة: " + data.a[1]);
      }
    }
  }, 800);
}
