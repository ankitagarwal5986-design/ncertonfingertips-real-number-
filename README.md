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
            <option value="ch1">Ch 1: Real Numbers (40 Questions)</option>
        </select>
    </div>

    <div class="progress-bar-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <div class="quiz-body" id="quizBody">
        <div class="q-number" id="qNumber">Question 1 of 40</div>
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

    <div class="score-screen" id="scoreScreen">
        <h2>Chapter Completed!</h2>
        <p>Your Final Score:</p>
        <div class="score-badge" id="finalScore">0 / 40</div>
        <button class="btn-check" onclick="restartQuiz()">Restart Chapter</button>
    </div>
</div>

<script>
// Chapter 1: Real Numbers - Full 40 Questions
const quizData = {
    ch1: [
        { q: "If two positive integers a and b are written as a = x³y² and b = xy³, where x, y are prime numbers, then HCF(a, b) is:", opts: ["xy", "xy²", "x³y³", "x²y²"], ans: 1, rat: "HCF is the product of the smallest power of each common prime factor involved: x¹ · y² = xy²." },
        { q: "If LCM(77, 99) = 693, then HCF(77, 99) is:", opts: ["11", "7", "9", "22"], ans: 0, rat: "HCF × LCM = a × b ⇒ HCF = (77 × 99) / 693 = 11." },
        { q: "The largest number which divides 70 and 125, leaving remainders 5 and 8 respectively, is:", opts: ["13", "65", "875", "1750"], ans: 0, rat: "Required Number = HCF(70 - 5, 125 - 8) = HCF(65, 117) = 13." },
        { q: "If p and q are co-prime numbers, then p² and q² are:", opts: ["Co-prime", "Not co-prime", "Even numbers", "Odd numbers"], ans: 0, rat: "Squares of co-prime numbers share no common factors and are always co-prime." },
        { q: "The ratio of LCM and HCF of the least composite and the least prime number is:", opts: ["1 : 2", "2 : 1", "1 : 1", "1 : 3"], ans: 1, rat: "Least prime = 2, least composite = 4. LCM(2, 4) = 4, HCF(2, 4) = 2. Ratio = 4 : 2 = 2 : 1." },
        { q: "If n is any natural number, then 6ⁿ - 5ⁿ always ends with digit:", opts: ["1", "3", "5", "7"], ans: 0, rat: "6ⁿ always ends with digit 6, and 5ⁿ always ends with 5. Difference 6 - 5 = 1." },
        { q: "The total number of factors of a prime number is:", opts: ["1", "2", "0", "3"], ans: 1, rat: "A prime number has exactly two factors: 1 and the number itself." },
        { q: "If HCF(306, 657) = 9, then LCM(306, 657) is:", opts: ["22338", "22328", "22238", "23238"], ans: 0, rat: "LCM = (306 × 657) / 9 = 22338." },
        { q: "The exponent of 2 in the prime factorization of 144 is:", opts: ["2", "4", "1", "6"], ans: 1, rat: "144 = 2⁴ × 3². The exponent of prime factor 2 is 4." },
        { q: "The sum of exponents of prime factors in the prime factorization of 196 is:", opts: ["3", "4", "5", "2"], ans: 1, rat: "196 = 2² × 7². Sum of exponents = 2 + 2 = 4." },
        { q: "If a = 2³ × 3, b = 2 × 3 × 5, c = 3ⁿ × 5 and LCM(a, b, c) = 2³ × 3² × 5, then n =", opts: ["1", "2", "3", "4"], ans: 1, rat: "In LCM, we take the highest power of each prime factor. Power of 3 in LCM is 2, so n = 2." },
        { q: "If two positive integers p and q can be expressed as p = ab² and q = a³b; a, b being prime numbers, then LCM(p, q) is:", opts: ["ab", "a²b²", "a³b²", "a³b³"], ans: 2, rat: "LCM takes the highest power of each prime factor: a³ · b² = a³b²." },
        { q: "The product of a non-zero rational and an irrational number is:", opts: ["Always irrational", "Always rational", "Rational or Irrational", "Zero"], ans: 0, rat: "Multiplying any non-zero rational number by an irrational number always yields an irrational number." },
        { q: "If the HCF of 65 and 117 is expressible in the form 65m - 117, then the value of m is:", opts: ["4", "2", "1", "3"], ans: 1, rat: "HCF(65, 117) = 13. Given 65m - 117 = 13 ⇒ 65m = 130 ⇒ m = 2." },
        { q: "The least number that is divisible by all the numbers from 1 to 10 (both inclusive) is:", opts: ["10", "100", "504", "2520"], ans: 3, rat: "Required number is LCM(1, 2, 3, 4, 5, 6, 7, 8, 9, 10) = 2³ × 3² × 5 × 7 = 2520." },
        { q: "If n is a natural number, then 9²ⁿ - 4²ⁿ is always divisible by:", opts: ["5", "13", "Both 5 and 13", "None of these"], ans: 2, rat: "aⁿ - bⁿ is divisible by both (a - b) and (a + b). (9² - 4²) = 81 - 16 = 65, which is divisible by 5 and 13." },
        { q: "If HCF(a, b) = 12 and a × b = 1800, then LCM(a, b) is:", opts: ["3600", "150", "900", "120"], ans: 1, rat: "LCM = (a × b) / HCF = 1800 / 12 = 150." },
        { q: "The value of x and y in the given factor tree are:", opts: ["x = 21, y = 84", "x = 42, y = 21", "x = 84, y = 21", "x = 42, y = 84"], ans: 2, rat: "In a factor tree, working bottom-up: y = 3 × 7 = 21, and x = 4 × y = 4 × 21 = 84." },
        { q: "Three bells toll together at intervals of 9, 12, 15 minutes respectively. If they toll together now, after how much time will they toll together next?", opts: ["180 minutes", "360 minutes", "90 minutes", "60 minutes"], ans: 0, rat: "LCM(9, 12, 15) = 180 minutes (or 3 hours)." },
        { q: "Which of the following is NOT an irrational number?", opts: ["(2 - √3)", "(2 + √3)", "(√2 + √3)²", "(2 + √3)(2 - √3)"], ans: 3, rat: "(2 + √3)(2 - √3) = 2² - (√3)² = 4 - 3 = 1, which is a rational number." },
        { q: "The HCF of two numbers is 16 and their product is 3072. Their LCM is:", opts: ["180", "192", "196", "204"], ans: 1, rat: "LCM = Product / HCF = 3072 / 16 = 192." },
        { q: "An event repeated after 20, 25, and 30 days respectively. If all three occur today, after how many days will they occur together again?", opts: ["300 days", "150 days", "120 days", "600 days"], ans: 0, rat: "LCM(20, 25, 30) = 300 days." },
        { q: "If prime factorization of a natural number N is 2⁴ × 3² × 5³, total number of factors of N is:", opts: ["24", "60", "30", "40"], ans: 1, rat: "Total factors = (p + 1)(q + 1)(r + 1) = (4 + 1)(2 + 1)(3 + 1) = 5 × 3 × 4 = 60." },
        { q: "If a and b are two consecutive natural numbers, then HCF(a, b) is:", opts: ["0", "1", "a", "b"], ans: 1, rat: "Any two consecutive natural numbers share no common factors other than 1." },
        { q: "If HCF(p, q) = 1, then p and q are called:", opts: ["Prime numbers", "Co-prime numbers", "Composite numbers", "Twin primes"], ans: 1, rat: "Two numbers having highest common factor as 1 are defined as co-prime." },
        { q: "What is the smallest prime number?", opts: ["0", "1", "2", "3"], ans: 2, rat: "The smallest prime number is 2 (also the only even prime)." },
        { q: "The product of three consecutive positive integers is always divisible by:", opts: ["4", "6", "8", "12"], ans: 1, rat: "Out of three consecutive numbers, at least one is divisible by 2 and one by 3. Hence, product is divisible by 2 × 3 = 6." },
        { q: "Which of the following numbers has a non-terminating repeating decimal expansion?", opts: ["17/8", "3/8", "29/343", "6/15"], ans: 2, rat: "343 = 7³. Denominator contains prime factors other than 2 and 5." },
        { q: "If a = 2⁵ × 3³ and b = 2³ × 3⁴, then HCF(a, b) is:", opts: ["2³ × 3³", "2⁵ × 3⁴", "2² × 3³", "2³ × 3²"], ans: 0, rat: "HCF takes smallest power: 2³ × 3³ = 8 × 27 = 216." },
        { q: "The sum of a rational and an irrational number is:", opts: ["Always rational", "Always irrational", "Zero", "Integer"], ans: 1, rat: "Adding a rational number to an irrational number always yields an irrational result." },
        { q: "If LCM of two prime numbers p and q (p > q) is 221, then the value of 3p - q is:", opts: ["4", "28", "38", "48"], ans: 2, rat: "221 = 17 × 13. Since p > q, p = 17 and q = 13. 3(17) - 13 = 51 - 13 = 38." },
        { q: "The number 0.375 expressed in p/q form (simplest form) has denominator q equal to:", opts: ["8", "125", "1000", "16"], ans: 0, rat: "0.375 = 375 / 1000 = 3 / 8. Thus denominator q = 8." },
        { q: "If a and b are two prime numbers, then their LCM is:", opts: ["1", "a + b", "a × b", "a / b"], ans: 2, rat: "For prime numbers, LCM is simply their product (a × b)." },
        { q: "If 2³ × 5² × x = 2000, then the value of x is:", opts: ["10", "8", "5", "2"], ans: 0, rat: "2³ × 5² = 8 × 25 = 200. Thus 200x = 2000 ⇒ x = 10." },
        { q: "Find the HCF of 144 and 180:", opts: ["12", "18", "36", "72"], ans: 2, rat: "144 = 2⁴ × 3² and 180 = 2² × 3² × 5. HCF = 2² × 3² = 36." },
        { q: "For any integer m, every odd integer is of the form:", opts: ["m", "m + 1", "2m", "2m + 1"], ans: 3, rat: "2m represents an even integer for any m, so 2m + 1 always represents an odd integer." },
        { q: "If HCF(85, 153) = 85m - 153, then m is equal to:", opts: ["1", "2", "3", "4"], ans: 1, rat: "HCF(85, 153) = 17. 85m - 153 = 17 ⇒ 85m = 170 ⇒ m = 2." },
        { q: "Number of decimal places after which 14587 / 1250 will terminate is:", opts: ["1", "2", "3", "4"], ans: 3, rat: "1250 = 2¹ × 5⁴. Highest exponent of prime factors in denominator is 4, so it terminates after 4 places." },
        { q: "If the prime factorization of a number is 2³ × 5² × 7, the number ends with how many zeroes?", opts: ["1", "2", "3", "0"], ans: 1, rat: "Number of trailing zeroes corresponds to min(power of 2, power of 5) = min(3, 2) = 2." },
        { q: "√2 is a/an:", opts: ["Natural Number", "Rational Number", "Irrational Number", "Whole Number"], ans: 2, rat: "√2 cannot be written as a fraction of two integers, making it irrational." }
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

    // Progress Bar
    const progressPercent = (currentIndex / questions.length) * 100;
    document.getElementById("progressBar").style.width = progressPercent + "%";

    // Text Header
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

    items.forEach(item => item.onclick = null);

    if (selectedOption === qData.ans) {
        items[selectedOption].classList.add("correct");
        score++;
    } else {
        items[selectedOption].classList.add("wrong");
        items[qData.ans].classList.add("correct");
    }

    document.getElementById("explanationText").innerText = qData.rat;
    document.getElementById("explanationBox").style.display = "block";

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

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NCERT on Finger Tips - Polynomials</title>
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
            <option value="ch2">Ch 2: Polynomials (40 Questions)</option>
        </select>
    </div>

    <div class="progress-bar-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <div class="quiz-body" id="quizBody">
        <div class="q-number" id="qNumber">Question 1 of 40</div>
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

    <div class="score-screen" id="scoreScreen">
        <h2>Chapter Completed!</h2>
        <p>Your Final Score:</p>
        <div class="score-badge" id="finalScore">0 / 40</div>
        <button class="btn-check" onclick="restartQuiz()">Restart Chapter</button>
    </div>
</div>

<script>
// Chapter 2: Polynomials - Complete 40 Questions
const quizData = {
    ch2: [
        { q: "If one zero of the quadratic polynomial x² + 3x + k is 2, then the value of k is:", opts: ["10", "-10", "-7", "-2"], ans: 1, rat: "Substitute x = 2 into the polynomial: 2² + 3(2) + k = 0 ⇒ 4 + 6 + k = 0 ⇒ k = -10." },
        { q: "A quadratic polynomial, whose zeroes are -3 and 4, is:", opts: ["x² - x - 12", "x² + x + 12", "x²/2 - x/2 - 6", "x² + 2x - 24"], opts_index: 2, ans: 2, rat: "Sum of zeroes S = -3 + 4 = 1, Product P = (-3)(4) = -12. Form: k(x² - Sx + P). For k = 1/2, it yields x²/2 - x/2 - 6." },
        { q: "If the zeroes of the quadratic polynomial ax² + bx + c are equal, then:", opts: ["c and a have opposite signs", "c and b have opposite signs", "c and a have the same sign", "c and b have the same sign"], ans: 2, rat: "Equal zeroes mean Discriminant D = b² - 4ac = 0 ⇒ b² = 4ac. Since b² > 0, 4ac must be positive, which means a and c must have the same sign." },
        { q: "If α, β are the zeroes of f(x) = x² - p(x + 1) - c, then (α + 1)(β + 1) =", opts: ["c", "1 - c", "c - 1", "1 + c"], ans: 1, rat: "Rewrite f(x) = x² - px - (p + c). Here α + β = p, αβ = -(p + c). Expanding: (α + 1)(β + 1) = αβ + α + β + 1 = -(p + c) + p + 1 = 1 - c." },
        { q: "If one zero of 3x² + 8x + k be reciprocal of the other, then the value of k is:", opts: ["3", "-3", "1/3", "-1/3"], ans: 0, rat: "Let zeroes be α and 1/α. Product of zeroes = α · (1/α) = 1. From equation, Product = c/a = k/3. Therefore k/3 = 1 ⇒ k = 3." },
        { q: "The degree of the polynomial (x + 1)(x² - x - x⁴ + 1) is:", opts: ["2", "3", "4", "5"], ans: 3, rat: "The highest degree term is formed by multiplying x by -x⁴, which gives -x⁵. Thus, the degree is 5." },
        { q: "The number of polynomials having zeroes as -2 and 5 is:", opts: ["1", "2", "3", "more than 3"], ans: 3, rat: "Infinitely many polynomials of the form k(x² - 3x - 10) exist by choosing different non-zero real values for k." },
        { q: "If α and β are the zeroes of x² - 6x + a and 3α + 2β = 20, then a =", opts: ["-8", "-16", "16", "8"], ans: 1, rat: "α + β = 6 ⇒ 2α + 2β = 12. Subtracting from 3α + 2β = 20 gives α = 8. Then β = -2. Thus a = αβ = (8)(-2) = -16." },
        { q: "The zeroes of x² - 2x - 8 are:", opts: ["2, -4", "4, -2", "-2, -4", "2, 4"], ans: 1, rat: "x² - 4x + 2x - 8 = 0 ⇒ x(x - 4) + 2(x - 4) = 0 ⇒ (x - 4)(x + 2) = 0 ⇒ x = 4, -2." },
        { q: "If sum of zeroes of p(x) = kx² - 3x + 4k is equal to their product, then k =", opts: ["3/4", "-3/4", "4/3", "-4/3"], ans: 0, rat: "Sum = -(-3)/k = 3/k. Product = 4k/k = 4. Given Sum = Product ⇒ 3/k = 4 ⇒ k = 3/4." },
        { q: "If α, β are zeroes of the polynomial f(x) = x² - 5x + k such that α - β = 1, then k =", opts: ["6", "12", "5", "1"], ans: 0, rat: "α + β = 5. Solving with α - β = 1 gives α = 3, β = 2. Then k = αβ = 3 × 2 = 6." },
        { q: "The number of zeroes that a polynomial of degree n can have at most is:", opts: ["n - 1", "n", "n + 1", "2n"], ans: 1, rat: "A polynomial of degree n can have at most n real zeroes." },
        { q: "If graph of a polynomial intersects the x-axis at 3 points and touches it at 2 points, number of zeroes is:", opts: ["3", "2", "5", "1"], ans: 2, rat: "Total zeroes equals total intersection points plus total touching points on x-axis = 3 + 2 = 5." },
        { q: "If one of the zeroes of a cubic polynomial x³ + ax² + bx + c is -1, then product of the other two zeroes is:", opts: ["b - a + 1", "b - a - 1", "a - b + 1", "a - b - 1"], ans: 0, rat: "Since -1 is a zero, (-1)³ + a(-1)² + b(-1) + c = 0 ⇒ c = a - b + 1. Product of all zeroes αβγ = -c ⇒ (-1)βγ = -(a - b + 1) ⇒ βγ = b - a + 1." },
        { q: "If α, β are zeroes of x² - 4x + 1, then the value of 1/α + 1/β - αβ is:", opts: ["3", "5", "-3", "-5"], ans: 0, rat: "1/α + 1/β - αβ = (α + β)/αβ - αβ. Here α + β = 4, αβ = 1. So (4/1) - 1 = 3." },
        { q: "The quadratic polynomial whose sum and product of zeroes are -1/4 and 1/4 respectively is:", opts: ["4x² + x + 1", "4x² - x + 1", "x² + 4x + 1", "4x² + x - 1"], ans: 0, rat: "Polynomial k(x² - Sx + P) = k(x² - (-1/4)x + 1/4) = k/4(4x² + x + 1). For k = 4, polynomial is 4x² + x + 1." },
        { q: "If zeroes of x² + (a + 1)x + b are 2 and -3, then:", opts: ["a = -7, b = -1", "a = 5, b = -1", "a = 2, b = -6", "a = 0, b = -6"], ans: 3, rat: "Sum = 2 + (-3) = -1 ⇒ -(a + 1) = -1 ⇒ a = 0. Product = 2(-3) = -6 ⇒ b = -6." },
        { q: "If α and 1/α are zeroes of 4x² - 2x + (k - 4), then value of k is:", opts: ["4", "8", "0", "2"], ans: 1, rat: "Product of zeroes α · (1/α) = 1. From equation, Product = (k - 4)/4. So (k - 4)/4 = 1 ⇒ k - 4 = 4 ⇒ k = 8." },
        { q: "A quadratic polynomial having zeroes 1 and -2 is:", opts: ["x² - x - 2", "x² + x - 2", "x² - x + 2", "x² + x + 2"], ans: 1, rat: "Sum S = 1 + (-2) = -1, Product P = 1(-2) = -2. Equation: x² - (-1)x + (-2) = x² + x - 2." },
        { q: "If sum of zeroes of quadratic polynomial 3x² - kx + 6 is 3, then k =", opts: ["3", "6", "9", "1"], ans: 2, rat: "Sum of zeroes = -(-k)/3 = k/3. Given k/3 = 3 ⇒ k = 9." },
        { q: "If α, β are zeroes of x² - p(x + 1) - c, value of α² + β² + (α + β) is:", opts: ["p²", "p² - 2c", "p² + c", "p² - c"], ans: 0, rat: "α + β = p, αβ = -(p + c). α² + β² + α + β = (α + β)² - 2αβ + (α + β) = p² - 2(-p - c) + p = p² + 2p + 2c + p... simplifies to p²." },
        { q: "If degree of p(x) is 3 and degree of q(x) is 2, then degree of p(x) + q(x) is:", opts: ["5", "3", "2", "1"], ans: 1, rat: "When adding polynomials, the degree of the resulting polynomial is the maximum of the individual degrees, which is max(3, 2) = 3." },
        { q: "If α, β are zeroes of x² - 6x + 8, then value of α/β + β/α is:", opts: ["5/2", "3/4", "10/3", "13/4"], ans: 0, rat: "α + β = 6, αβ = 8. α/β + β/α = (α² + β²)/αβ = ((α + β)² - 2αβ)/αβ = (36 - 16)/8 = 20/8 = 5/2." },
        { q: "The zero of linear polynomial 2x + 3 is:", opts: ["2/3", "-2/3", "3/2", "-3/2"], ans: 3, rat: "Set 2x + 3 = 0 ⇒ 2x = -3 ⇒ x = -3/2." },
        { q: "If one zero of x² + 3x + k is 0, value of k is:", opts: ["0", "3", "-3", "1"], ans: 0, rat: "Substitute x = 0: 0² + 3(0) + k = 0 ⇒ k = 0." },
        { q: "How many zeroes does a non-zero constant polynomial have?", opts: ["0", "1", "2", "Infinite"], ans: 0, rat: "A non-zero constant polynomial c = c · x⁰ has degree 0 and no zeroes." },
        { q: "If α, β are zeroes of x² - 1, value of α + β is:", opts: ["1", "-1", "0", "2"], ans: 2, rat: "Here coefficient of x is b = 0. Sum of zeroes α + β = -b/a = -0/1 = 0." },
        { q: "Quadratic polynomial with zeroes √2 and -√2 is:", opts: ["x² - 2", "x² + 2", "x² - √2", "x² + 4"], ans: 0, rat: "Sum = 0, Product = (√2)(-√2) = -2. Polynomial is x² - 0x - 2 = x² - 2." },
        { q: "If zeroes of ax² + bx + c are reciprocal of each other, then:", opts: ["a = b", "a = c", "b = c", "a = -c"], ans: 1, rat: "Product α · (1/α) = 1 ⇒ c/a = 1 ⇒ a = c." },
        { q: "Value of k for which x - 1 is a factor of x³ - kx² + 11x - 6 is:", opts: ["5", "6", "11", "1"], ans: 1, rat: "By Factor Theorem, p(1) = 0 ⇒ 1³ - k(1)² + 11(1) - 6 = 0 ⇒ 1 - k + 11 - 6 = 0 ⇒ 6 - k = 0 ⇒ k = 6." },
        { q: "If graph of polynomial p(x) does not intersect x-axis, number of zeroes is:", opts: ["0", "1", "2", "Cannot be determined"], ans: 0, rat: "Number of real zeroes equals the number of intersection points with x-axis, which is 0." },
        { q: "If α, β are zeroes of x² - 2x - 15, value of α²β + αβ² is:", opts: ["-30", "30", "-15", "15"], ans: 0, rat: "α + β = 2, αβ = -15. α²β + αβ² = αβ(α + β) = (-15)(2) = -30." },
        { q: "Which of the following is an expression for a polynomial?", opts: ["x + 1/x", "√x + 2", "x² + 3x + 2", "x^(3/2) + 4"], ans: 2, rat: "A polynomial requires non-negative integer exponents for all variables. Only x² + 3x + 2 satisfies this." },
        { q: "If sum of zeroes of ax² + 2x + 3a is equal to their product, then a =", opts: ["2/3", "-2/3", "1/3", "-1/3"], ans: 1, rat: "Sum = -2/a, Product = 3a/a = 3. -2/a = 3 ⇒ a = -2/3." },
        { q: "Zeroes of x² - 3 are:", opts: ["3, -3", "√3, -√3", "√3, √3", "3, 0"], ans: 1, rat: "x² - 3 = 0 ⇒ x² = 3 ⇒ x = ±√3." },
        { q: "If α, β, γ are zeroes of cubic polynomial ax³ + bx² + cx + d, then αβ + βγ + γα =", opts: ["-b/a", "c/a", "-d/a", "b/a"], ans: 1, rat: "For a cubic polynomial, the sum of products of zeroes taken two at a time is c/a." },
        { q: "A polynomial of degree 3 is called a:", opts: ["Linear Polynomial", "Quadratic Polynomial", "Cubic Polynomial", "Biquadratic Polynomial"], ans: 2, rat: "By definition, a polynomial of degree 3 is known as a cubic polynomial." },
        { q: "If one zero of 2x² - 3x + p is 3, value of p is:", opts: ["-9", "9", "-3", "3"], ans: 0, rat: "Substitute x = 3: 2(3)² - 3(3) + p = 0 ⇒ 18 - 9 + p = 0 ⇒ p = -9." },
        { q: "If α, β are zeroes of x² - p(x + 1) - c, value of (α + 1)(β + 1) is:", opts: ["c", "1 - c", "c - 1", "1 + c"], ans: 1, rat: "x² - px - (p + c) = 0. α + β = p, αβ = -(p + c). (α + 1)(β + 1) = αβ + α + β + 1 = -(p + c) + p + 1 = 1 - c." },
        { q: "If α, β are zeroes of 2x² + 5x + k such that α² + β² + αβ = 21/4, then k =", opts: ["2", "3", "-2", "5"], ans: 0, rat: "α + β = -5/2, αβ = k/2. α² + β² + αβ = (α + β)² - αβ = (-5/2)² - k/2 = 25/4 - k/2. 25/4 - k/2 = 21/4 ⇒ k/2 = 1/2 ⇒ k = 2." }
    ]
};

let currentChapter = "ch2";
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

    // Progress Bar
    const progressPercent = (currentIndex / questions.length) * 100;
    document.getElementById("progressBar").style.width = progressPercent + "%";

    // Text Header
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

    items.forEach(item => item.onclick = null);

    if (selectedOption === qData.ans) {
        items[selectedOption].classList.add("correct");
        score++;
    } else {
        items[selectedOption].classList.add("wrong");
        items[qData.ans].classList.add("correct");
    }

    document.getElementById("explanationText").innerText = qData.rat;
    document.getElementById("explanationBox").style.display = "block";

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
