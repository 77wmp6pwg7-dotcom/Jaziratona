# Jaziratona<!DOCTYPE html>

<html lang="ar" dir="rtl">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>جزيرتنا 🏝️</title>

<style>

* {

    box-sizing: border-box;

}

body {

    margin: 0;

    overflow: hidden;

    font-family: Arial, sans-serif;

    background: #74d4f0;

    color: white;

}

#game {

    width: 100vw;

    height: 100vh;

    position: relative;

    overflow: hidden;

}

/* السماء */

.sky {

    position: absolute;

    inset: 0;

    background: linear-gradient(

        #71d5f3 0%,

        #b9ecff 55%,

        #73d2e9 100%

    );

}

/* الشمس */

.sun {

    position: absolute;

    width: 90px;

    height: 90px;

    border-radius: 50%;

    background: #ffe36e;

    top: 7%;

    left: 8%;

    box-shadow: 0 0 50px #ffe36e;

}

/* الجزيرة */

.island {

    position: absolute;

    width: 75vw;

    height: 35vh;

    left: 12.5vw;

    bottom: 8vh;

    background: #e8c879;

    border-radius: 50%;

    box-shadow: 0 18px 0 rgba(0,0,0,.12);

}

/* الماء */

.water {

    position: absolute;

    inset: 55% 0 0 0;

    background: rgba(0,150,190,.28);

}

/* العنوان */

.title {

    position: absolute;

    top: 4vh;

    right: 4vw;

    background: rgba(0,0,0,.35);

    padding: 15px 22px;

    border-radius: 20px;

    text-align: center;

}

.title h1 {

    margin: 0;

    font-size: clamp(25px, 5vw, 50px);

}

.title p {

    margin: 5px 0 0;

    font-size: clamp(16px, 3vw, 25px);

}

/* البيت */

.house {

    position: absolute;

    bottom: 28vh;

    left: 42vw;

    font-size: clamp(60px, 12vw, 150px);

}

/* الشجرة */

.tree {

    position: absolute;

    bottom: 27vh;

    left: 22vw;

    font-size: clamp(55px, 11vw, 130px);

}

/* الجسر */

.bridge {

    position: absolute;

    bottom: 25vh;

    right: 20vw;

    font-size: clamp(55px, 11vw, 130px);

    display: none;

}

/* لوحة المهمة */

.task {

    position: absolute;

    bottom: 4vh;

    left: 50%;

    transform: translateX(-50%);

    width: 90vw;

    max-width: 650px;

    background: rgba(0,0,0,.65);

    padding: 15px 20px;

    border-radius: 22px;

    text-align: center;

}

.taskText {

    font-size: clamp(20px, 4vw, 32px);

    font-weight: bold;

}

.counter {

    margin-top: 7px;

    font-size: clamp(25px, 6vw, 45px);

}

/* زر البداية */

.start {

    position: absolute;

    top: 50%;

    left: 50%;

    transform: translate(-50%, -50%);

    padding: 20px 35px;

    border: none;

    border-radius: 25px;

    background: white;

    color: #176c83;

    font-size: 25px;

    font-weight: bold;

    cursor: pointer;

    z-index: 20;

}

/* رسالة النجاح */

.success {

    position: absolute;

    inset: 0;

    display: none;

    align-items: center;

    justify-content: center;

    background: rgba(0,0,0,.25);

    z-index: 30;

}

.successBox {

    background: white;

    color: #176c83;

    padding: 30px;

    border-radius: 30px;

    text-align: center;

    width: 80%;

    max-width: 500px;

}

.successBox h2 {

    font-size: 40px;

    margin: 0 0 10px;

}

.successBox p {

    font-size: 22px;

}

</style>

</head>

<body>

<div id="game">

    <div class="sky"></div>

    <div class="sun"></div>

    <div class="water"></div>

    <div class="island"></div>

    <div class="tree">🌴</div>

    <div class="house">🏠</div>

    <div id="bridge" class="bridge">🌉</div>

    <div class="title">

        <h1>🏝️ جزيرتنا</h1>

        <p>أنت تبنيها بنفسك!</p>

    </div>

    <div class="task">

        <div id="taskText" class="taskText">

            اضغط ابدأ ثم اقفز 10 مرات!

        </div>

        <div id="counter" class="counter">

            0 / 10

        </div>

    </div>

    <button id="startButton" class="start">

        🚀 ابدأ المغامرة

    </button>

    <div id="success" class="success">

        <div class="successBox">

            <h2>🎉 رائع!</h2>

            <p>

                لقد بنيت الجسر في جزيرتك!

            </p>

            <p>

                غدًا نكتشف المنطقة الجديدة 🏝️

            </p>

        </div>

    </div>

</div>

<script>

let count = 0;

let running = false;

const startButton =

    document.getElementById("startButton");

const counter =

    document.getElementById("counter");

const taskText =

    document.getElementById("taskText");

const bridge =

    document.getElementById("bridge");

const success =

    document.getElementById("success");

/*

    النسخة الأولى لا تحتاج كاميرا حتى الآن.

    نريد أولاً التأكد أن تجربة الجزيرة نفسها ممتعة.

*/

startButton.addEventListener("click", function() {

    startButton.style.display = "none";

    running = true;

    taskText.innerHTML =

        "اقفز أمام الشاشة! 🐸";

    counter.innerHTML =

        "0 / 10";

    /*

      مؤقت تجريبي:

      كل ضغطة على الشاشة تعتبر قفزة.

      سنستبدلها بالكاميرا في النسخة التالية.

    */

    document.body.addEventListener("click", fakeJump);

});

function fakeJump() {

    if (!running) return;

    count++;

    if (count > 10) {

        count = 10;

    }

    counter.innerHTML =

        count + " / 10";

    /*

       اهتزاز بسيط للجزيرة

    */

    document.querySelector(".island").animate(

        [

            { transform: "scale(1)" },

            { transform: "scale(1.03)" },

            { transform: "scale(1)" }

        ],

        {

            duration: 250

        }

    );

    if (count >= 10) {

        running = false;

        document.body.removeEventListener(

            "click",

            fakeJump

        );

        bridge.style.display = "block";

        setTimeout(function() {

            success.style.display = "flex";

        }, 500);

    }

}

</script>

</body>

</html>
