<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Терминал Архива</title>
  <style>
    body {
      background: black;
      color: #33ff33;
      font-family: 'Courier New', monospace;
      padding: 20px;
      overflow-x: hidden;
      overflow-y: auto;
      position: relative;
    }
    .scanlines {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-image: repeating-linear-gradient(to bottom, rgba(0,0,0,0.1), rgba(0,0,0,0.1) 1px, transparent 1px, transparent 3px);
      pointer-events: none;
      z-index: 100;
      animation: flicker 0.15s infinite;
    }
    @keyframes flicker {
      0% { opacity: 0.95; }
      50% { opacity: 0.85; }
      100% { opacity: 0.95; }
    }
    .section {
      margin-bottom: 40px;
    }
    .hidden {
      display: none;
    }
    input[type="text"] {
      background-color: black;
      border: 1px solid #33ff33;
      color: #33ff33;
      font-family: 'Courier New', monospace;
      padding: 4px;
      margin-top: 10px;
    }
    button {
      background-color: #000;
      color: #33ff33;
      border: 1px solid #33ff33;
      padding: 4px 8px;
      cursor: pointer;
      margin-top: 10px;
    }
    button:hover {
      background-color: #111;
    }
  </style>
</head>
<body>
<div class="scanlines"></div>
<audio id="bgm" loop>
  <source src="eyes-of-fear-1.mp3" type="audio/mpeg">
  Ваш браузер не поддерживает аудио.
</audio>
<button onclick="playBgm()">▶ Включить атмосферу</button>

<h1>Добро пожаловать в Терминал Архива</h1>

<div class="section">
  <p>Экран тускло мерцает в пыли. Пахнет озоном и чем-то гниющим. Что вы хотите осмотреть?</p>
  <ul>
    <li><button onclick="document.getElementById('locker').classList.remove('hidden')">📁 Шкафчик у стены</button></li>
    <li><button onclick="document.getElementById('desk').classList.remove('hidden')">🗂 Письменный стол</button></li>
    <li><button onclick="document.getElementById('monitor').classList.remove('hidden')">🖥 Мигающий монитор</button></li>
  </ul>
</div>

<div class="section hidden" id="locker">
  <h3>Шкафчик</h3>
  <p>На грязной записке надпись: <i>URMW WVHP</i>. Кривой почерк гласит: «Атбаш».</p>
  <button onclick="document.getElementById('riddle1').classList.remove('hidden')">Рассшифровать</button>
</div>

<div class="section hidden" id="desk">
  <h3>Письменный стол</h3>
  <p>Вы находите выцветший журнал. Среди странных заметок выделены заглавные буквы:<br>
  <i><b>S</b>hifted <b>P</b>aths <b>E</b>merge <b>C</b>louded <b>T</b>rails <b>R</b>evealed <b>A</b>new</i></p>
</div>

<div class="section hidden" id="monitor">
  <h3>Монитор</h3>
  <p>Морзянка вспыхивает на экране: <code>..-. .. -. .- .-..</code></p>
</div>

<!-- Первая загадка -->
<div class="section hidden" id="riddle1">
  <p>Введите расшифровку записки из шкафчика:</p>
  <input type="text" id="input1" placeholder="Введите ответ">
  <button onclick="checkAnswer('input1', 'riddle2', 'FIND DESK')">Проверить</button>
</div>

<!-- Вторая загадка -->
<div class="section hidden" id="riddle2">
  <p>Введите перевод морзянки:</p>
  <input type="text" id="input2" placeholder="Введите ответ">
  <button onclick="checkAnswer('input2', 'riddle3', 'ФИНАЛ')">Проверить</button>
</div>

<!-- Третья загадка -->
<div class="section hidden" id="riddle3">
  <p>Какое слово складывается из выделенных букв в журнале?</p>
  <input type="text" id="input3" placeholder="Введите ответ">
  <button onclick="solveThird()">Проверить</button>
</div>

<!-- Тайная ячейка после 3 загадки -->
<div class="section hidden" id="secretCompartment">
  <h3>Тайная ячейка в столе</h3>
  <p>Под столешницей спрятаны странные символы (шифр Wingdings)...</p>
  <button onclick="document.getElementById('riddle4').classList.remove('hidden')">📜 Попробовать расшифровать</button>
</div>

<!-- Четвёртая загадка -->
<div class="section hidden" id="riddle4">
  <p>Ответ на странные символы:</p>
  <input type="text" id="input4" placeholder="Введите ответ">
  <button onclick="checkAnswer('input4', 'newSignal', 'ВРЕМЕННАЯ ПЕТЛЯ')">Проверить</button>
</div>

<!-- Новый сигнал после 4 загадки -->
<div class="section hidden" id="newSignal">
  <h3>Новый сигнал на мониторе</h3>
  <p>Появляется фраза: <i>"цикл будет вечен"</i></p>
  <button onclick="document.getElementById('riddle5').classList.remove('hidden')">📜 Ввести фразу</button>
</div>

<!-- Пятая загадка -->
<div class="section hidden" id="riddle5">
  <p>Введите точную фразу:</p>
  <input type="text" id="input5" placeholder="Введите ответ">
  <button onclick="checkAnswer('input5', 'riddle6', 'ЦИКЛ БУДЕТ ВЕЧЕН')">Проверить</button>
</div>

<!-- Шестая загадка -->
<div class="section hidden" id="riddle6">
  <p>Последний запрос системы:<br><b>Введите время активации:</b></p>
  <input type="text" id="input6" placeholder="Формат 03:12">
  <button onclick="checkAnswer('input6', 'finalLog', '03:12')">Проверить</button>
</div>

<!-- Финальный лог -->
<div class="section hidden" id="finalLog">
  <h2>ФИНАЛЬНЫЙ ЛОГ</h2>
  <p>
    Активация центрального сервера.<br>
    Подключение к A.V.A.<br><br>
    Получено сообщение:<br>
    «Ты приходил сюда десять раз. Ты умирал десять раз. Ты выбирал один и тот же путь. Единственной переменной было твоё сознание. И теперь ты очнулся. Цикл заканчивается, когда сознание = 1».
  </p>

  <p><b>Вы хотите прервать цикл? Или попробовать ещё раз?</b></p>
  <button onclick="restartGame()">🔄 Попробовать ещё раз</button>
  <button onclick="endGame()">🚪 Прервать цикл</button>
</div>

<!-- Концовка -->
<div class="section hidden" id="goodbye">
  <h2>До встречи в следующем измерении.</h2>
</div>

<script>
function playBgm() {
  const audio = document.getElementById('bgm');
  if (audio) audio.play();
  this.style.display = 'none';
}

function checkAnswer(inputId, nextId, correctAnswer) {
  const val = document.getElementById(inputId).value.trim().toUpperCase();
  if (val === correctAnswer.toUpperCase()) {
    document.getElementById(inputId).parentElement.classList.add("hidden");
    document.getElementById(nextId).classList.remove("hidden");
  } else {
    alert("Неверно. Попробуйте снова...");
  }
}

function solveThird() {
  const val = document.getElementById('input3').value.trim().toUpperCase();
  if (val === 'SPECTRA') {
    document.getElementById('riddle3').classList.add("hidden");
    document.getElementById('secretCompartment').classList.remove("hidden");
  } else {
    alert("Неверно. Попробуйте снова...");
  }
}

function restartGame() {
  location.reload();
}

function endGame() {
  document.getElementById('finalLog').classList.add('hidden');
  document.getElementById('goodbye').classList.remove('hidden');
}
</script>

</body>
</html>
