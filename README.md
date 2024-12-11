- 👋 Hi, I’m @Mohamedelhacimi
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Mohamedelhacimi/Mohamedelhacimi is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
بالطبع! سأقوم بتعديل السكريبت لجعله أكثر تفاعلية ووضوحًا. سأجعل الميكانيكية واضحة مع بعض التعديلات على الشكل والمحتوى ليكون أكثر واقعية.

التعديلات التي سأضيفها:
	1.	زيادة المضاعف بشكل تدريجي حتى الوصول إلى نقطة التفجير.
	2.	إظهار الوقت المتبقي قبل التحطم.
	3.	إعطاء اللاعب فرصة للسحب بشكل واضح، مع إظهار رسالة توضح إذا تم السحب بنجاح أو إذا تحطمت الطائرة.
	4.	حساب الأرباح بناءً على المبلغ الذي راهن به اللاعب.

السكريبت المعدل:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crash Game</title>
    <style>
        body { font-family: Arial, sans-serif; padding: 20px; background-color: #f4f4f9; }
        #multiplier { font-size: 30px; color: green; }
        #timeLeft { font-size: 20px; color: red; }
        #message { font-size: 20px; color: black; }
        button { padding: 10px 20px; font-size: 16px; margin-top: 20px; }
    </style>
</head>
<body>
    <h1>لعبة Crash</h1>
    <div id="multiplier">مضاعف: 1.00</div>
    <div id="timeLeft">الوقت المتبقي: 0 ثانية</div>
    <div id="message">اضغط على "ابدأ اللعبة" للبدء!</div>
    <button onclick="startGame()">ابدأ اللعبة</button>
    <button onclick="cashOut()" disabled>اسحب أرباحك</button>

    <script>
        let multiplier = 1.00;  // قيمة المضاعف
        let incrementRate = 0.01;  // معدل الزيادة
        let isCrashed = false;  // حالة التحطم
        let crashTime = 0;  // وقت التحطم العشوائي
        let gameStarted = false;  // حالة اللعبة
        let userBet = 100;  // مبلغ الرهان
        let userWinnings = 0;  // الأرباح بعد السحب
        let countdownInterval;  // متغير لتوقيت العد التنازلي

        // دالة لزيادة المضاعف
        function increaseMultiplier() {
            if (!isCrashed) {
                multiplier += incrementRate;  // زيادة المضاعف
                document.getElementById("multiplier").innerText = `مضاعف: ${multiplier.toFixed(2)}`;

                // تحديث الوقت المتبقي
                let timeLeft = Math.max(0, (crashTime - multiplier).toFixed(2));
                document.getElementById("timeLeft").innerText = `الوقت المتبقي: ${timeLeft} ثانية`;

                // التحقق من تحطم الطائرة
                if (multiplier >= crashTime) {
                    isCrashed = true;
                    document.getElementById("message").innerText = `تفجرت الطائرة عند مضاعف: ${multiplier.toFixed(2)}! خسرت الرهان.`;
                    document.querySelector('button[onclick="cashOut()"]').disabled = true;  // تعطيل زر السحب بعد التحطم
                }
            }
        }

        // دالة لسحب الأرباح
        function cashOut() {
            if (gameStarted && !isCrashed) {
                userWinnings = userBet * multiplier;  // حساب الأرباح
                document.getElementById("message").innerText = `تم السحب بنجاح! أرباحك: ${userWinnings.toFixed(2)}$`;
                document.querySelector('button[onclick="cashOut()"]').disabled = true;  // تعطيل زر السحب بعد السحب
            } else if (!gameStarted) {
                document.getElementById("message").innerText = "الرجاء بدء اللعبة أولاً!";
            } else {
                document.getElementById("message").innerText = "لا يمكنك السحب بعد التحطم!";
            }
        }

        // دالة لبدء اللعبة
        function startGame() {
            isCrashed = false;
            multiplier = 1.00;
            gameStarted = true;
            crashTime = Math.random() * (3 - 1) + 1;  // تحديد وقت التحطم بشكل عشوائي بين 1 و 3 ثواني
            document.getElementById("message").innerText = `اللعبة بدأت! الطائرة ستنفجر عند مضاعف ${crashTime.toFixed(2)}!`;
            document.querySelector('button[onclick="cashOut()"]').disabled = false;  // تفعيل زر السحب بعد بدء اللعبة
            clearInterval(countdownInterval);  // إيقاف أي عد تنازلي سابق
            countdownInterval = setInterval(increaseMultiplier, 100);  // زيادة المضاعف كل 100 مللي ثانية
        }
    </script>
</body>
</html>

التعديلات الرئيسية:
	1.	زيادة المضاعف بشكل تدريجي: يتم زيادة المضاعف كل 100 مللي ثانية، ويظهر الوقت المتبقي حتى حدوث التحطم.
	2.	وقت التحطم العشوائي: يتم تحديد وقت التحطم بين 1 و 3 ثوانٍ عشوائيًا عند بدء اللعبة.
	3.	إظهار الوقت المتبقي: يظهر العد التنازلي للوقت المتبقي قبل أن تتحطم الطائرة.
	4.	السحب: يمكن للاعب السحب في أي وقت قبل التحطم، وفي حال التحطم، يتم تعطيل زر السحب.

كيفية اللعب:
	1.	اضغط على “ابدأ اللعبة” لبدء اللعبة.
	2.	راقب المضاعف أثناء زيادة قيمته.
	3.	حاول السحب قبل أن تصل الطائرة إلى نقطة التحطم.
	4.	إذا تحطمت الطائرة، ستظهر رسالة تُخبرك بأنك خسرت.

تحسينات مستقبلية:
	•	إضافة رسوميات للطائرة والعقبات.
	•	إضافة أصوات للتحطم أو السحب.
	•	تخصيص الوقت العشوائي ليصبح أكثر تحديًا.

إذا كنت بحاجة لتعديل آخر أو إضافة، لا تتردد في سؤالي!
