# DIGIBHEM3
CALCULATOR
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Advanced Calculator</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background: linear-gradient(135deg, #1a1a1a, #000000);
      margin: 0;
      color: #fff;
    }
    .calculator {
      background: #121212;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.7);
      max-width: 400px;
      width: 100%;
    }
    .display {
      width: 100%;
      height: 70px;
      background: #1e1e1e;
      border: none;
      border-radius: 8px;
      margin-bottom: 20px;
      font-size: 2rem;
      text-align: right;
      padding: 10px;
      color: #00ff00;
      box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.5);
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
    }
    button {
      height: 60px;
      background: #333;
      color: #fff;
      font-size: 1.2rem;
      border: none;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }
    button:hover {
      background: #444;
      transform: scale(1.05);
    }
    button:active {
      transform: scale(0.95);
    }
    .operator {
      background: #b30000;
      color: #fff;
    }
    .operator:hover {
      background: #800000;
    }
    .equal {
      background: #006400;
      grid-column: span 2;
    }
    .equal:hover {
      background: #004d00;
    }
    .clear {
      background: #8b0000;
      grid-column: span 2;
    }
    .clear:hover {
      background: #600000;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <input type="text" class="display" id="display" disabled />
    <div class="buttons">
      <button onclick="appendNumber('7')">7</button>
      <button onclick="appendNumber('8')">8</button>
      <button onclick="appendNumber('9')">9</button>
      <button class="operator" onclick="chooseOperator('/')">/</button>
      <button onclick="appendNumber('4')">4</button>
      <button onclick="appendNumber('5')">5</button>
      <button onclick="appendNumber('6')">6</button>
      <button class="operator" onclick="chooseOperator('*')">*</button>
      <button onclick="appendNumber('1')">1</button>
      <button onclick="appendNumber('2')">2</button>
      <button onclick="appendNumber('3')">3</button>
      <button class="operator" onclick="chooseOperator('-')">-</button>
      <button onclick="appendNumber('0')">0</button>
      <button onclick="appendDecimal()">.</button>
      <button class="equal" onclick="calculate()">=</button>
      <button class="operator" onclick="chooseOperator('+')">+</button>
      <button class="clear" onclick="clearDisplay()">C</button>
    </div>
  </div>

  <script>
    let currentInput = '';
    let previousInput = '';
    let operator = null;

    function appendNumber(number) {
      if (currentInput.includes('.') && number === '.') return;
      currentInput += number;
      updateDisplay();
    }

    function appendDecimal() {
      if (!currentInput.includes('.')) {
        currentInput += '.';
      }
      updateDisplay();
    }

    function chooseOperator(selectedOperator) {
      if (currentInput === '') return;
      if (previousInput !== '') {
        calculate();
      }
      operator = selectedOperator;
      previousInput = currentInput;
      currentInput = '';
    }

    function calculate() {
      let result;
      const prev = parseFloat(previousInput);
      const curr = parseFloat(currentInput);
      if (isNaN(prev) || isNaN(curr)) return;
      switch (operator) {
        case '+':
          result = prev + curr;
          break;
        case '-':
          result = prev - curr;
          break;
        case '*':
          result = prev * curr;
          break;
        case '/':
          result = curr === 0 ? 'Error' : prev / curr;
          break;
        default:
          return;
      }
      currentInput = result;
      operator = null;
      previousInput = '';
      updateDisplay();
    }

    function clearDisplay() {
      currentInput = '';
      previousInput = '';
      operator = null;
      updateDisplay();
    }

    function updateDisplay() {
      const display = document.getElementById('display');
      display.value = currentInput;
    }

    updateDisplay();
  </script>
</body>
</html>
