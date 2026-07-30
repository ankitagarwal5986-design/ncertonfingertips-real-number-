<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NCERT on Finger Tips - Brain and Mind Academy</title>
<style>
    :root {
        --primary-blue: #1e3a8a;
        --secondary-gold: #d97706;
        --bg-light: #f8fafc;
        --card-bg: #ffffff;
        --text-dark: #0f172a;
        --correct-green: #059669;
        --incorrect-red: #dc2626;
    }

    * {
        box-sizing: border-box;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
        margin: 0;
        padding: 20px;
        background-color: var(--bg-light);
        color: var(--text-dark);
        display: flex;
        justify-content: center;
    }

    .quiz-card {
        width: 100%;
        max-width: 750px;
        background: var(--card-bg);
        border-radius: 12px;
        box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
        overflow: hidden;
    }

    .header {
        background: linear-gradient(135deg, #0f172a 0%, var(--primary-blue) 100%);
        color: white;
        padding: 25px 20px;
        text-align: center;
        border-bottom: 5px solid var(--secondary-gold);
    }

    .header h1 {
        margin: 0;
        font-size: 22px;
        letter-spacing: 1px;
        text-transform: uppercase;
    }

    .header h2 {
        margin: 5px 0 0 0;
        font-size: 14px;
        color: #fcd34d;
        font-weight: 500;
    }

    .controls {
        padding: 15px 20px;
        background: #e2e8f0;
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        gap: 10px;
    }

    select {
        padding: 8px 12px;
        border-radius: 6px;
        border: 1px solid #cbd5e0;
        font-size: 14px;
        font-weight: 600;
        color: var(--text-dark);
        background: white;
        cursor: pointer;
    }

    .progress-bar-container {
        height: 6px;
        background: #cbd5e0;
        width: 100%;
    }

    .progress-bar {
        height: 100%;
        width: 0%;
        background: var(--secondary-gold);
        transition: width 0.3s ease;
    }

    .quiz-body {
        padding: 25px 20px;
    }

    .q-number {
        font-size: 13px;
        font-weight: 700;
        color: #2563eb;
        text-transform: uppercase;
        margin-bottom: 8px;
    }

    .question-text {
        font-size: 16px;
        font-weight: 600;
        margin-bottom: 20px;
        line-height: 1.5;
    }

    .options-list {
        list-style: none;
        padding: 0;
        margin: 0 0 20px 0;
    }

    .option-item {
        padding: 12px 16px;
        margin-bottom: 10px;
        border: 2px solid #e2e8f0;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.2s ease;
        display: flex;
        align-items: center;
        font-size: 14px;
    }

    .option-item:hover {
        border-color: #93c5fd;
        background-color: #eff6ff;
    }

    .option-item.selected {
        border-color: #2563eb;
        background-color: #dbeafe;
        font-weight: 600;
    }

    .option-item.correct {
        border-color: var(--correct-green);
        background-color: #d1fae5;
        color: #065f46;
        font-weight: 600;
    }

    .option-item.wrong {
        border-color: var(--incorrect-red);
        background-color: #fee2e2;
        color: #991b1b;
    }

    .explanation-box {
        display: none;
        padding: 15px;
        border-radius: 8px;
        background: #f1f5f9;
        border-left: 4px solid #2563eb;
        margin-bottom: 20px;
        font-size: 13.5px;
        line-height: 1.5;
    }

    .explanation-box strong {
        color: #1e293b;
    }

    .footer-btn-group {
        display: flex;
        justify-content: space-between;
        gap: 10px;
    }

    button {
        padding: 10px 20px;
        border: none;
        border-radius: 6px;
        font-size: 14px;
        font-weight: 600;
        cursor: pointer;
        transition: background 0.2s;
    }

    .btn-check {
        background: #2563eb;
        color: white;
    }

    .btn-check:hover {
        background: #1d4ed8;
    }

    .btn-next {
        background: var(--secondary-gold);
        color: white;
    }

    .btn-next:hover {
        background: #b45309;
    }

    button:disabled {
        opacity: 0.5;
        cursor: not-allowed;
    }

    .score-screen {
        text-align: center;
        padding: 40px 20px;
        display: none;
    }

    .score-screen h2 {
        font-size: 24px;
        color: var(--primary-blue);
    }

    .score-badge {
        font-size: 40px;
        font-weight: 800;
        color: var(--secondary-gold);
        margin: 15px 0;
    }
</style>
</head>
<body>

<div class="quiz-card">
    <div class="header">
        <h1>NCERT ON FINGER TIPS</h1>
        <h2>BY BRAIN AND MIND ACADEMY</h2>
    </div>

    <div class="controls">
        <label for="chapterSelect"><strong>Select Chapter:</strong></label>
        <select id="chapterSelect" onchange="loadChapter()">
            <option value="ch1">Ch 1: Real Numbers</option>
            <option value="ch2">Ch 2: Polynomials</option>
            <option value="ch3">Ch 3: Pair of Linear Equations</option>
            <option value="ch4">Ch 4: Quadratic Equations</option>
            <option value="ch5">Ch 5: Arithmetic Progressions</option>
            <option value="ch6">Ch 6: Triangles</option>
        </select>
    </div>

    <div class="progress-bar-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <!-- Interactive Quiz View -->
    <div class="quiz-body" id="quizBody">
        <div class="q-number" id="qNumber">Question 1 of 10</div>
        <div class="question-text" id="questionText">Loading Question...</div>

        <ul class="options-list" id="optionsList"></ul>

        <div class="explanation-box" id="explanationBox">
            <strong>Rationale:</strong> <span id="explanationText"></span>
        </div>

        <div class="footer-btn-group">
            <button class="btn-check" id="checkBtn" onclick="checkAnswer()" disabled>Check Answer</button>
            <button class="btn-next" id="nextBtn" onclick="nextQuestion()" style="display: none;">Next Question →</button>
        </div>
    </div>

    <!-- Final Score View -->
    <div class="score-screen" id="scoreScreen">
        <h2>Chapter Completed!</h2>
        <p>Your Final Score:</p>
        <div class="score-badge" id="finalScore">0 / 0</div>
        <button class="btn-check" onclick="restartQuiz()">Restart Chapter</button>
    </div>
</div>

<script>
// Master Question Bank (Chapters 1 to 6)
const quizData = {
    ch1: [
        { q: "If two positive integers a and b are written as a = x³y² and b = xy³, where x, y are prime numbers, then HCF(a, b) is:", opts: ["xy", "xy²", "x³y³", "x²y²"], ans: 1, rat: "HCF is product of smallest power of each common prime factor: x¹ · y² = xy²." },
        { q: "If LCM(77, 99) = 693, then HCF(77, 99) is:", opts: ["11", "7", "9", "22"], ans: 0, rat: "HCF × LCM = a × b ⇒ HCF = (77 × 99)/693 = 11." },
        { q: "The largest number which divides 70 and 125, leaving remainders 5 and 8 respectively, is:", opts: ["13", "65", "875", "1750"], ans: 0, rat: "HCF(70-5, 125-8) = HCF(65, 117) = 13." },
        { q: "If p and q are co-prime numbers, then p² and q² are:", opts: ["Co-prime", "Not co-prime", "Even numbers", "Odd numbers"], ans: 0, rat: "Squares of co-prime numbers share no common factors and are always co-prime." },
        { q: "The ratio of LCM and HCF of the least composite and the least prime number is:", opts: ["1 : 2", "2 : 1", "1 : 1", "1 : 3"], ans: 1, rat: "Least prime = 2, least composite = 4. LCM(2,4)=4, HCF(2,4)=2. Ratio = 4:2 = 2:1." }
    ],
    ch2: [
        { q: "If one zero of the quadratic polynomial x² + 3x + k is 2, then the value of k is:", opts: ["10", "-10", "-7", "-2"], ans: 1, rat: "2² + 3(2) + k = 0 ⇒ 4 + 6 + k = 0 ⇒ k = -10." },
        { q: "A quadratic polynomial, whose zeroes are -3 and 4, is:", opts: ["x² - x - 12", "x² + x + 12", "x²/2 - x/2 - 6", "x² + 2x - 24"], ans: 2, rat: "S = 1, P = -12. Polynomial k(x² - x - 12). For k = 1/2, it is x²/2 - x/2 - 6." },
        { q: "If the zeroes of the quadratic polynomial ax² + bx + c are equal, then:", opts: ["c and a have opposite signs", "c and b have opposite signs", "c and a have the same sign", "c and b have same sign"], ans: 2, rat: "D = b² - 4ac = 0 ⇒ b² = 4ac > 0 ⇒ a and c must have the same sign." },
        { q: "If α, β are zeroes of f(x) = x² - p(x + 1) - c, then (α + 1)(β + 1) =", opts: ["c", "1 - c", "c - 1", "1 + c"], ans: 1, rat: "f(x) = x² - px - (p + c). α+β = p, αβ = -(p+c). (α+1)(β+1) = αβ + α + β + 1 = -(p+c) + p + 1 = 1 - c." }
    ],
    ch3: [
        { q: "If the system x + 2y = 3 and 5x + ky + 7 = 0 has no solution, then k is:", opts: ["10", "-10", "5/2", "-5/2"], ans: 0, rat: "a₁/a₂ = b₁/b₂ ≠ c₁/c₂ ⇒ 1/5 = 2/k ⇒ k = 10." },
        { q: "The pair of equations y = 0 and y = -7 has:", opts: ["One solution", "Two solutions", "Infinitely many solutions", "No solution"], ans: 3, rat: "Horizontal parallel lines never intersect, so no solution." },
        { q: "If 217x + 131y = 913 and 131x + 217y = 827, then x + y =", opts: ["5", "6", "7", "8"], ans: 0, rat: "Adding both equations: 348x + 348y = 1740 ⇒ x + y = 5." }
    ],
    ch4: [
        { q: "Which of the following is a quadratic equation?", opts: ["x² + 2x + 1 = (4 - x)² + 3", "-2x² = (5 - x)(2 - 2/5 x)", "(k + 1)x² + 3/2 x = 7 (k = -1)", "x³ - x² = (x - 1)³"], ans: 3, rat: "x³ - x² = x³ - 3x² + 3x - 1 ⇒ 2x² - 3x + 1 = 0 (Degree 2)." },
        { q: "The quadratic equation 2x² - √5 x + 1 = 0 has:", opts: ["Two distinct real roots", "Two equal real roots", "No real roots", "More than 2 real roots"], ans: 2, rat: "D = (-√5)² - 4(2)(1) = 5 - 8 = -3 < 0 (No real roots)." },
        { q: "Values of k for which 2x² - kx + k = 0 has equal roots are:", opts: ["0 only", "4", "8 only", "0, 8"], ans: 3, rat: "D = k² - 8k = 0 ⇒ k(k - 8) = 0 ⇒ k = 0, 8." }
    ],
    ch5: [
        { q: "If 11th term of an AP is 38 and 16th term is 73, then 31st term is:", opts: ["178", "170", "150", "185"], ans: 0, rat: "a+10d=38, a+15d=73 ⇒ 5d=35 ⇒ d=7, a=-32. a₃₁ = -32 + 30(7) = 178." },
        { q: "The sum of first 100 positive integers is:", opts: ["5050", "5005", "5500", "50500"], ans: 0, rat: "S₁₀₀ = 100(101)/2 = 5050." },
        { q: "If sum of first n terms of AP is 3n² + 5n, then 2nd term is:", opts: ["14", "11", "8", "17"], ans: 0, rat: "S₁ = 8 = a₁, S₂ = 22. a₂ = S₂ - S₁ = 22 - 8 = 14." }
    ],
    ch6: [
        { q: "In ΔABC, DE || BC such that AD = 3 cm, DB = 5 cm, AC = 5.6 cm. Length of AE is:", opts: ["2.1 cm", "3.1 cm", "1.8 cm", "2.4 cm"], ans: 0, rat: "AD/AB = AE/AC ⇒ 3/8 = AE/5.6 ⇒ AE = (3 × 5.6)/8 = 2.1 cm." },
        { q: "If ΔABC ~ ΔDEF such that 2AB = DE and BC = 8 cm, then EF =", opts: ["16 cm", "12 cm", "8 cm", "4 cm"], ans: 0, rat: "AB/DE = BC/EF ⇒ 1/2 = 8/EF ⇒ EF = 16 cm." },
        { q: "Length of altitude of an equilateral triangle of side 8 cm is:", opts: ["4√3 cm", "2√3 cm", "8√3 cm", "4 cm"], ans: 0, rat: "h = (√3/2) × 8 = 4√3 cm." }
    ]
};

let currentChapter = "ch1";
let currentIndex = 0;
let selectedOption = null;
let score = 0;

function loadChapter() {
    currentChapter = document.getElementById("chapterSelect").value;
    currentIndex = 0;
    score = 0;
    document.getElementById("quizBody").style.display = "block";
    document.getElementById("scoreScreen").style.display = "none";
    showQuestion();
}

function showQuestion() {
    const questions = quizData[currentChapter];
    const qData = questions[currentIndex];

    // Reset State
    selectedOption = null;
    document.getElementById("checkBtn").disabled = true;
    document.getElementById("checkBtn").style.display = "inline-block";
    document.getElementById("nextBtn").style.display = "none";
    document.getElementById("explanationBox").style.display = "none";

    // Progress
    const progressPercent = ((currentIndex) / questions.length) * 100;
    document.getElementById("progressBar").style.width = progressPercent + "%";

    // Header info
    document.getElementById("qNumber").innerText = `Question ${currentIndex + 1} of ${questions.length}`;
    document.getElementById("questionText").innerText = qData.q;

    // Render Options
    const optionsList = document.getElementById("optionsList");
    optionsList.innerHTML = "";
    
    qData.opts.forEach((optText, i) => {
        const li = document.createElement("li");
        li.className = "option-item";
        li.innerHTML = `<strong>${String.fromCharCode(65 + i)})</strong>&nbsp; ${optText}`;
        li.onclick = () => selectOption(i, li);
        optionsList.appendChild(li);
    });
}

function selectOption(index, element) {
    // Clear previous selection
    const items = document.querySelectorAll(".option-item");
    items.forEach(item => item.classList.remove("selected"));

    selectedOption = index;
    element.classList.add("selected");
    document.getElementById("checkBtn").disabled = false;
}

function checkAnswer() {
    const questions = quizData[currentChapter];
    const qData = questions[currentIndex];
    const items = document.querySelectorAll(".option-item");

    // Disable all options click
    items.forEach(item => item.onclick = null);

    if (selectedOption === qData.ans) {
        items[selectedOption].classList.add("correct");
        score++;
    } else {
        items[selectedOption].classList.add("wrong");
        items[qData.ans].classList.add("correct");
    }

    // Display Explanation
    document.getElementById("explanationText").innerText = qData.rat;
    document.getElementById("explanationBox").style.display = "block";

    // Toggle Buttons
    document.getElementById("checkBtn").style.display = "none";
    document.getElementById("nextBtn").style.display = "inline-block";
}

function nextQuestion() {
    const questions = quizData[currentChapter];
    currentIndex++;

    if (currentIndex < questions.length) {
        showQuestion();
    } else {
        showScoreScreen();
    }
}

function showScoreScreen() {
    const questions = quizData[currentChapter];
    document.getElementById("progressBar").style.width = "100%";
    document.getElementById("quizBody").style.display = "none";
    document.getElementById("scoreScreen").style.display = "block";
    document.getElementById("finalScore").innerText = `${score} / ${questions.length}`;
}

function restartQuiz() {
    loadChapter();
}

// Initial Load
loadChapter();
</script>

</body>
</html>
