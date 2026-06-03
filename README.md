# Ex06 BMI Calculator
## Date: 03.06.2026
## Name: Arshiya M
## REG NO: 212224040029
## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
## App.jsx:
```
import React, { useState } from "react";
import "./App.css";

function App() {

  const [weight, setWeight] = useState("");

  const [height, setHeight] = useState("");

  const [bmi, setBmi] = useState(null);

  const [category, setCategory] = useState("");

  const calculateBMI = () => {

    if (
      !weight ||
      !height ||
      weight <= 0 ||
      height <= 0
    ) {

      alert("Enter valid values");

      return;

    }

    const heightInMeters =
      height / 100;

    const result = (

      weight /

      (

        heightInMeters *
        heightInMeters

      )

    ).toFixed(2);

    setBmi(result);

    if (result < 18.5) {

      setCategory(
        "Underweight"
      );

    }

    else if (result < 24.9) {

      setCategory(
        "Normal Weight"
      );

    }

    else if (result < 29.9) {

      setCategory(
        "Overweight"
      );

    }

    else {

      setCategory(
        "Obesity"
      );

    }

  };

  return (

    <div className="page">

      <div className="card">

        <h1>

          BMI Calculator ⚡

        </h1>

        <p className="subtitle">

          Check your body mass index instantly

        </p>

        <input

          type="number"

          placeholder="Weight (kg)"

          value={weight}

          onChange={(e) =>

            setWeight(
              e.target.value
            )

          }

        />

        <input

          type="number"

          placeholder="Height (cm)"

          value={height}

          onChange={(e) =>

            setHeight(
              e.target.value
            )

          }

        />

        <button

          onClick={calculateBMI}

        >

          Calculate BMI

        </button>

        {

          bmi && (

            <div className="result">

              <h2>

                BMI : {bmi}

              </h2>

              <h3>

                {category}

              </h3>

            </div>

          )

        }

      </div>

    </div>

  );

}

export default App;
```
## Home.jsx:
```
import React from "react";

import { Link } from "react-router-dom";

function Home() {

  return (

    <div className="page">

      <div className="card">

        <p className="subtitle">

          Measure your BMI and stay healthy

        </p>

        <Link to="/calculate">

          <button>

            Start Calculator

          </button>

        </Link>

      </div>

    </div>

  );

}

export default Home;
```

## main.jsx:
```
import React from "react";

import ReactDOM from "react-dom/client";

import App from "./App";

ReactDOM.createRoot(

  document.getElementById("root")

).render(

  <React.StrictMode>

    <App />

  </React.StrictMode>

);
```

## App.css:
```
* {

  margin: 0;

  padding: 0;

  box-sizing: border-box;

}

html,
body,
#root {

  width: 100%;

  height: 100%;

  font-family:

    Segoe UI,

    sans-serif;

  overflow: hidden;

}

body {

  background:

    linear-gradient(
      135deg,
      #0f172a,
      #1e1b4b,
      #312e81,
      #000000
    );

  background-size:

    400% 400%;

  animation:

    gradient 12s ease infinite;

}

@keyframes gradient {

  0% {

    background-position:

      0% 50%;

  }

  50% {

    background-position:

      100% 50%;

  }

  100% {

    background-position:

      0% 50%;

  }

}

.page {

  width: 100%;

  height: 100%;

  display: flex;

  justify-content: center;

  align-items: center;

  padding: 20px;

}

.card {

  background:

    rgba(
      255,
      255,
      255,
      0.95
    );

  padding: 40px;

  border-radius: 22px;

  box-shadow:

    0px 10px 35px

    rgba(
      0,
      0,
      0,
      0.35
    );

  display: flex;

  flex-direction: column;

  align-items: center;

  gap: 18px;

  min-width: 380px;

  color: #222;

}

.card h1 {

  font-size: 2.2rem;

  color: #222;

}

.subtitle {

  color: #555;

}

input {

  width: 260px;

  padding: 14px;

  border:

    1px solid #ccc;

  border-radius: 10px;

  font-size: 16px;

  outline: none;

  transition: .3s;

}

input:focus {

  border:

    1px solid #7c3aed;

  box-shadow:

    0 0 8px

    rgba(
      124,
      58,
      237,
      0.4
    );

}

button {

  padding:

    14px 28px;

  border: none;

  border-radius: 10px;

  background:

    #7c3aed;

  color: white;

  font-size: 16px;

  cursor: pointer;

  transition: .3s;

}

button:hover {

  transform:

    translateY(-2px);

  background:

    #6d28d9;

}

.result {

  margin-top: 15px;

  display: flex;

  flex-direction: column;

  gap: 10px;

  align-items: center;

  color: #222;

}
```
## OUTPUT
<img width="1870" height="954" alt="image" src="https://github.com/user-attachments/assets/8da22b10-0015-48a0-a030-bf62133004b7" />

<img width="1865" height="959" alt="image" src="https://github.com/user-attachments/assets/f235375e-a779-4a80-8416-583fe2b16e52" />
<img width="1871" height="964" alt="image" src="https://github.com/user-attachments/assets/f948b03e-ca27-4e1b-bdb1-e5beff64b1bf" />



## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
