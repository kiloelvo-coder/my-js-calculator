<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vercel Calculator App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="calculator-container">
        <input type="text" id="display" value="" readonly>
        <div class="buttons-grid">
            <button class="btn function-btn" onclick="clearDisplay()">AC</button>
            <button class="btn function-btn" onclick="appendToDisplay('/')">/</button>
            <button class="btn function-btn" onclick="appendToDisplay('*')">×</button>
            <button class="btn operator-btn" onclick="appendToDisplay('-')">−</button>

            <button class="btn num-btn" onclick="appendToDisplay('7')">7</button>
            <button class="btn num-btn" onclick="appendToDisplay('8')">8</button>
            <button class="btn num-btn" onclick="appendToDisplay('9')">9</button>
            <button class="btn operator-btn" onclick="appendToDisplay('+')">+</button>

            <button class="btn num-btn" onclick="appendToDisplay('4')">4</button>
            <button class="btn num-btn" onclick="appendToDisplay('5')">5</button>
            <button class="btn num-btn" onclick="appendToDisplay('6')">6</button>
            <button class="btn equals-btn" onclick="calculate()" style="grid-row: 3 / span 2;">=</button>

            <button class="btn num-btn" onclick="appendToDisplay('1')">1</button>
            <button class="btn num-btn" onclick="appendToDisplay('2')">2</button>
            <button class="btn num-btn" onclick="appendToDisplay('3')">3</button>

            <button class="btn num-btn" onclick="appendToDisplay('0')" style="grid-column: 1 / span 2;">0</button>
            <button class="btn num-btn" onclick="appendToDisplay('.')">.</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
:root {
    --bg-color: #384252;
    --display-bg: #272c36;
    --num-color: #e0e0e0;
    --op-color: #ff9500;
    --func-color: #a6a6a6;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f0f0f0;
    font-family: 'Helvetica Neue', sans-serif;
    padding: 20px;
    margin: 0;
}

.calculator-container {
    width: 100%;
    max-width: 380px; /* Standard phone width */
    background-color: var(--bg-color);
    border-radius: 20px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
    padding: 15px;
}

#display {
    width: 100%;
    height: 90px;
    background-color: var(--display-bg);
    color: var(--num-color);
    font-size: 3em;
    text-align: right;
    border: none;
    border-radius: 10px;
    padding: 10px 15px;
    margin-bottom: 15px;
    box-sizing: border-box;
    overflow: hidden;
}

.buttons-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
}

.btn {
    padding: 0;
    height: 75px;
    font-size: 1.8em;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: background-color 0.1s, transform 0.05s;
    display: flex;
    justify-content: center;
    align-items: center;
}

.num-btn {
    background-color: #505050;
    color: var(--num-color);
}

.num-btn:active {
    background-color: #6a6a6a;
}

.function-btn {
    background-color: var(--func-color);
    color: #000;
}

.function-btn:active {
    background-color: #c9c9c9;
}

.operator-btn, .equals-btn {
    background-color: var(--op-color);
    color: #fff;
}

.operator-btn:active, .equals-btn:active {
    background-color: #ffb84d;
}
const display = document.getElementById('display');

// Function to add the button value to the display
function appendToDisplay(input) {
    // Prevent starting with an operator unless the display is empty
    if (display.value === "" && ['/', '*', '+', '-'].includes(input)) {
        return; 
    }
    display.value += input;
}

// Function to clear the entire display
function clearDisplay() {
    display.value = "";
}

// Function to calculate the result
function calculate() {
    try {
        // Replace 'x' with '*' for multiplication if needed, though this HTML uses '*'
        let expression = display.value.replace(/×/g, '*'); 
        
        // Use Function constructor instead of eval() for safer execution
        // This is a common practice for simple, controlled math
        const result = new Function('return ' + expression)(); 

        display.value = result;
    } catch (error) {
        display.value = "Error";
    }
}
