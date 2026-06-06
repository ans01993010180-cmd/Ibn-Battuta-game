<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>رحلة ابن بطوطة</title>
<style>
body { margin: 0; background: #e8dcc6; font-family: 'Tajawal', sans-serif; overflow: hidden; }
#game { width: 100vw; height: 100vh; position: relative; padding-top: 20px; }
h1 { text-align: center; color: #5c3d2e; font-size: 32px; }
.start-btn { display: block; margin: 50px auto; padding: 15px 40px; background: #8b5a2b; color: #fff8e1; border: 3px solid #5c3d2e; border-radius: 10px; font-size: 20px; cursor: pointer; }
.map-dot { position: absolute; width: 30px; height: 30px; background: #c0392b; border-radius: 50%; border: 2px solid #5c3d2e; cursor: pointer; }
#coins-display { position: absolute; top: 20px; left: 20px; background: #8b5a2b; color: #ffd700; padding: 10px 20px; border-radius: 20px; font-size: 18px; }
</style>
</head>
<body>
<div id="game">
  <div id="coins-display">💰 <span id="coins">0</span></div>
  <h1>رحلة ابن بطوطة</h1>
  <p style="text-align:center; color:#5c3d2e">اجمع معلومات الرحالة واضرب رقم قياسي جديد!</p>
  <button class="start-btn" onclick="startGame()">ابدأ الرحلة</button>
  <div class="map-dot" style="top:60%; left:20%;" onclick="askQuestion('طنجة')"></div>
  <div class="map-dot" style="top:65%; left:28%;" onclick="askQuestion('مكة')"></div>
</div>

<script>
let coins = 0;
function startGame() {
  alert("مرحباً! أنت الآن ابن بطوطة سنة 1325م\nأول محطة: طنجة");
}
function askQuestion(city) {
  let answer = prompt("ما اسم الكتاب؟ 1. ألف ليلة 2. تحفة النظار 3. مقدمة ابن خلدون");
  if(answer == "2") {
    coins += 10;
    document.getElementById('coins').innerText = coins;
    alert("صحيح! رصيدك: " + coins);
  } else {
    alert("حاول مرة ثانية! الإجابة: تحفة النظار");
  }
}
</script>
</body>
</html>
