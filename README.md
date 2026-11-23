# Ex04 - Simple Calculator built with React Project

## Name: Deepak J G
## Reg No: 212224220019

---

## AIM
To develop a Simple Calculator using React.js with a clean and responsive design, ensuring a smooth user experience across different screen sizes.

---

## ALGORITHM

**Step 1:** Create a React App.

**Step 2:** Open a terminal and run:
```bash
npx create-react-app simple-calculator
cd simple-calculator
npm start
```

**Step 3:** Inside the `src/` folder, create a new file `Calculator.js` and define the basic structure.

**Step 4:** Plan the UI: display screen, number buttons (0-9), operators (+, -, *, /), clear (C), and equal (=).

**Step 5:** Create a new file `Calculator.css` in `src/` and add the styling.

**Step 6:** Open `src/App.js` and modify it.

**Step 7:** Start the development server:
```bash
npm start
```

**Step 8:** Open `http://localhost:3000/` in the browser.

**Step 9:** Test the calculator by entering numbers and operations.

**Step 10:** Fix styling issues and refine content placement.

**Step 11:** Deploy the website.

**Step 12:** Upload to GitHub Pages for free hosting.

---

## PROGRAM

### `src/Calculator.js`
```jsx
import React, { useState } from "react";
import "./Calculator.css";

const Calculator = () => {
  const [display, setDisplay] = useState("0");
  const [prev, setPrev] = useState(null);
  const [operator, setOperator] = useState(null);
  const [waiting, setWaiting] = useState(false);

  const inputDigit = (d) => {
    if (waiting) {
      setDisplay(String(d));
      setWaiting(false);
    } else {
      setDisplay(display === "0" ? String(d) : display + d);
    }
  };

  const inputDot = () => {
    if (waiting) {
      setDisplay("0.");
      setWaiting(false);
      return;
    }
    if (!display.includes(".")) setDisplay(display + ".");
  };

  const compute = (a, b, op) => {
    let result;
    switch (op) {
      case "+": result = a + b; break;
      case "-": result = a - b; break;
      case "*": result = a * b; break;
      case "/":
        if (b === 0) return null;
        result = a / b;
        break;
      default: return b;
    }
    return parseFloat(result.toFixed(10));
  };

  const handleOperator = (nextOp) => {
    const current = parseFloat(display);
    if (prev !== null && operator && !waiting) {
      const result = compute(prev, current, operator);
      if (result === null) {
        setDisplay("Error");
        setPrev(null);
        setOperator(null);
        setWaiting(true);
        return;
      }
      setDisplay(String(result));
      setPrev(result);
    } else {
      setPrev(current);
    }
    setOperator(nextOp);
    setWaiting(true);
  };

  const handleEquals = () => {
    if (operator === null || prev === null) return;
    const result = compute(prev, parseFloat(display), operator);
    setDisplay(result === null ? "Error" : String(result));
    setPrev(null);
    setOperator(null);
    setWaiting(true);
  };

  const handleClear = () => {
    setDisplay("0");
    setPrev(null);
    setOperator(null);
    setWaiting(false);
  };

  return (
    <div className="calculator">
      <div className="display">{display}</div>
      <div className="buttons">
        <button className="btn clear" onClick={handleClear}>C</button>
        <button className="btn operator" onClick={() => handleOperator("/")}>÷</button>
        <button className="btn operator" onClick={() => handleOperator("*")}>×</button>
        <button className="btn operator" onClick={() => handleOperator("-")}>−</button>

        {[7, 8, 9].map((n) => (
          <button key={n} className="btn" onClick={() => inputDigit(n)}>{n}</button>
        ))}
        <button className="btn operator" onClick={() => handleOperator("+")}>+</button>

        {[4, 5, 6].map((n) => (
          <button key={n} className="btn" onClick={() => inputDigit(n)}>{n}</button>
        ))}
        <button className="btn equals" onClick={handleEquals}>=</button>

        {[1, 2, 3].map((n) => (
          <button key={n} className="btn" onClick={() => inputDigit(n)}>{n}</button>
        ))}

        <button className="btn zero" onClick={() => inputDigit(0)}>0</button>
        <button className="btn" onClick={inputDot}>.</button>
      </div>
    </div>
  );
};

export default Calculator;
```

### `src/Calculator.css`
```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #1e3c72, #2a5298);
  font-family: "Segoe UI", Arial, sans-serif;
}

.calculator {
  width: 90%;
  max-width: 340px;
  padding: 20px;
  background: #1c1c1e;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.display {
  background: #2c2c2e;
  color: #fff;
  font-size: 2.2rem;
  text-align: right;
  padding: 20px;
  margin-bottom: 15px;
  border-radius: 12px;
  min-height: 80px;
  overflow-x: auto;
  word-break: break-all;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.btn {
  padding: 18px 0;
  font-size: 1.3rem;
  border: none;
  border-radius: 12px;
  background: #3a3a3c;
  color: #fff;
  cursor: pointer;
  transition: transform 0.1s, filter 0.2s;
}

.btn:hover {
  filter: brightness(1.2);
}

.btn:active {
  transform: scale(0.95);
}

.operator { background: #ff9500; }
.clear    { background: #ff3b30; }
.equals   {
  background: #34c759;
  grid-row: span 2;
}
.zero {
  grid-column: span 2;
}

@media (max-width: 400px) {
  .display { font-size: 1.8rem; padding: 15px; }
  .btn { padding: 14px 0; font-size: 1.1rem; }
}
```

### `src/App.js`
```jsx
import React from "react";
import Calculator from "./Calculator";

function App() {
  return (
    <div className="App">
      <Calculator />
    </div>
  );
}

export default App;
```


## OUTPUT
<img width="495" height="683" alt="image" src="https://github.com/user-attachments/assets/3206f961-5124-4da3-8bcc-b6170d4942e4" />

<img width="495" height="683" alt="image" src="https://github.com/user-attachments/assets/d0813755-4876-4a71-8538-ecc599b505d3" />

---

## RESULT
The program for developing a simple calculator in React.js is executed successfully.
