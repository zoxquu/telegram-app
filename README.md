# telegram<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Мой счётчик</title>

  <script src="https://telegram.org/js/telegram-web-app.js"></script>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: var(--tg-theme-bg-color, #ffffff);
      color: var(--tg-theme-text-color, #000000);
      font-family: Arial, sans-serif;
    }

    .app {
      width: 100%;
      max-width: 400px;
      padding: 30px;
      text-align: center;
    }

    .counter {
      font-size: 72px;
      font-weight: bold;
      margin-bottom: 35px;
    }

    .plus-button {
      width: 100%;
      height: 100px;
      border: none;
      border-radius: 24px;
      background: #2481cc;
      color: white;
      font-size: 40px;
      font-weight: bold;
      cursor: pointer;
      transition: transform 0.08s;
    }

    .plus-button:active {
      transform: scale(0.96);
    }
  </style>
</head>

<body>
  <div class="app">
    <div id="counter" class="counter">0</div>

    <button id="plusButton" class="plus-button">
      +1
    </button>
  </div>

  <script>
    const tg = window.Telegram.WebApp;

    tg.ready();
    tg.expand();

    let count = Number(localStorage.getItem("count")) || 0;

    const counter = document.getElementById("counter");
    const button = document.getElementById("plusButton");

    function updateCounter() {
      counter.textContent = count;
      localStorage.setItem("count", count);
    }

    button.addEventListener("click", () => {
      count++;
      updateCounter();

      // Небольшая вибрация в Telegram
      if (tg.HapticFeedback) {
        tg.HapticFeedback.impactOccurred("light");
      }
    });

    updateCounter();
  </script>
</body>
</html>-app