<!DOCTYPE html>

<html lang="ar" dir="rtl">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>جزيرتنا 🏝️</title>

<style>

body {

  margin: 0;

  font-family: Arial, sans-serif;

  background: #72d5f2;

  text-align: center;

  color: white;

}

h1 {

  margin-top: 40px;

  font-size: 40px;

}

#island {

  font-size: 100px;

  margin-top: 60px;

  transition: transform 0.3s;

}

button {

  font-size: 24px;

  padding: 18px 30px;

  border: 0;

  border-radius: 20px;

  background: white;

  color: #176c83;

}

#count {

  font-size: 30px;

  margin: 25px;

}

</style>

</head>

<body>

<h1>🏝️ جزيرتنا</h1>

<div id="island">🏝️</div>

<div id="count">0 / 10</div>

<button onclick="jump()">🚀 ابدأ القفز</button>

<script>

let count = 0;

function jump() {

  count++;

  if (count > 10) {

    count = 10;

  }

  document.getElementById("count").innerText = count + " / 10";

  document.getElementById("island").style.transform =

    "scale(1.1)";

  setTimeout(function() {

    document.getElementById("island").style.transform =

      "scale(1)";

  }, 200);

  if (count === 10) {

    alert("🎉 رائع! لقد بنيت أول جزء من جزيرتك!");

  }

}

</script>

</body>

</html>
