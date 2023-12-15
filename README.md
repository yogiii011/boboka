<!DOCTYPE html>
<html>
<head>
  <title>Custom Countdown Timer with Text</title>
  <style>
    /* Style for the timer and inputs */
    #categoryInput, #txt2, #textList {
      display: block;
      margin: 10px auto;
      text-align: center;
    }
    #categoryInput {
      width: 80%;
      font-size: 18px;
      padding: 5px;
      margin-top: 20px;
    }
    #timer {
      font-size: 36px;
      text-align: center;
      margin-top: 20px;
    }
    #txt2, #clearButton, #startButton {
      margin-top: 10px;
    }
  </style>
</head>
<body>

<input type="text" id="categoryInput" placeholder="Enter category" />
<input type="text" id="txt2" placeholder="Enter text for timer" />
<div id="timer">15</div>
<div id="textList"></div>
<button id="startButton">START</button>
<button id="clearButton">CLEAR</button>

<script>
  var timerDisplay = document.getElementById("timer");
  var categoryInput = document.getElementById("categoryInput");
  var textInput = document.getElementById("txt2");
  var textList = document.getElementById("textList");
  var clearButton = document.getElementById("clearButton");
  var startButton = document.getElementById("startButton");
  var texts = [];
  var timer;

  function countdown(seconds, text) {
    timerDisplay.textContent = seconds;

    if (seconds <= 0) {
      timerDisplay.textContent = "BOBO KA: " + text;
      return;
    }

    seconds--;
    timer = setTimeout(function() {
      countdown(seconds, text);
    }, 1000); // Update every second
  }

  function resetTimer() {
    clearTimeout(timer);
    timerDisplay.textContent = "15";
    timer = countdown(15, "");
  }

  categoryInput.addEventListener("keypress", function(event) {
    if (event.key === "Enter" && categoryInput.value !== "") {
      categoryInput.disabled = true;
      textInput.focus();
    }
  });

  textInput.addEventListener("keypress", function(event) {
    if (event.key === "Enter" && textInput.value !== "") {
      texts.push(categoryInput.value + ": " + textInput.value);
      textList.innerHTML = texts.map(item => "<div>" + item + "</div>").join("");
      textInput.value = "";
      resetTimer();
    }
  });

  clearButton.addEventListener("click", function() {
    categoryInput.disabled = false;
    categoryInput.value = "";
    texts = [];
    textList.innerHTML = "";
    resetTimer();
  });

  startButton.addEventListener("click", function() {
    resetTimer();
    startButton.disabled = true;
  });

</script>

</body>
</html>
# boboka
