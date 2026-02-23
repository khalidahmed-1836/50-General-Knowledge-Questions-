<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GK Quiz Game - 50 Questions</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    color: white;
}

.main-heading {
    margin-bottom: 20px;
    font-size: 28px;
    font-weight: bold;
}

.quiz-container {
    background: rgba(0, 0, 0, 0.85);
    padding: 30px;
    border-radius: 15px;
    width: 95%;
    max-width: 600px;
    text-align: center;
}

.timer {
    font-size: 18px;
    margin-bottom: 15px;
    color: #ffd700;
}

.answers button {
    display: block;
    width: 100%;
    margin: 8px 0;
    padding: 10px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background: #ffffff;
    color: black;
    font-weight: bold;
}

.correct { background-color: #00c853 !important; color:white; }
.wrong { background-color: #d50000 !important; color:white; }

.hidden { display: none; }
</style>
</head>

<body>

<div class="main-heading">General Knowledge Quiz (50 Questions)</div>

<div class="quiz-container">

    <div class="timer">Time Left: <span id="time">10</span>s</div>

    <div id="quiz">
        <h2 id="question"></h2>
        <div id="answers" class="answers"></div>
    </div>

    <div id="result" class="hidden">
        <h2>Your Score: <span id="score"></span></h2>
        <button onclick="restartQuiz()">Restart Quiz</button>
    </div>

</div>

<script>

const questions = [

{question:"What is the capital of Pakistan?",answers:["Lahore","Karachi","Islamabad","Peshawar"],correct:2},
{question:"Which is the largest continent?",answers:["Africa","Asia","Europe","Australia"],correct:1},
{question:"Which is the largest ocean?",answers:["Indian Ocean","Pacific Ocean","Atlantic Ocean","Arctic Ocean"],correct:1},
{question:"Who invented the telephone?",answers:["Isaac Newton","Albert Einstein","Alexander Graham Bell","Nikola Tesla"],correct:2},
{question:"Which planet is known as the Red Planet?",answers:["Earth","Mars","Jupiter","Saturn"],correct:1},
{question:"What is the national animal of Pakistan?",answers:["Lion","Markhor","Tiger","Leopard"],correct:1},
{question:"Which is the fastest land animal?",answers:["Lion","Cheetah","Tiger","Horse"],correct:1},
{question:"Which is the smallest continent?",answers:["Asia","Europe","Australia","Africa"],correct:2},
{question:"Mount Everest lies in which country?",answers:["India","China","Nepal","Bhutan"],correct:2},
{question:"What is the currency of the United Kingdom?",answers:["Dollar","Euro","Pound Sterling","Rupee"],correct:2},

{question:"Who wrote Hamlet?",answers:["William Shakespeare","Charles Dickens","John Milton","William Wordsworth"],correct:0},
{question:"H2O is the chemical formula of?",answers:["Salt","Oxygen","Water","Hydrogen"],correct:2},
{question:"Which is the largest desert in the world?",answers:["Sahara","Gobi","Arabian","Thar"],correct:0},
{question:"How many continents are there?",answers:["5","6","7","8"],correct:2},
{question:"What is the national sport of Pakistan?",answers:["Hockey","Cricket","Football","Squash"],correct:0},
{question:"Who discovered gravity?",answers:["Isaac Newton","Galileo Galilei","Nikola Tesla","Charles Darwin"],correct:0},
{question:"What is the capital of France?",answers:["Rome","Paris","Madrid","Berlin"],correct:1},
{question:"Who was the first man on the Moon?",answers:["Buzz Aldrin","Yuri Gagarin","Neil Armstrong","Michael Collins"],correct:2},
{question:"Plants absorb which gas?",answers:["Oxygen","Carbon Dioxide","Nitrogen","Hydrogen"],correct:1},
{question:"Which is the largest country by area?",answers:["USA","China","Russia","Canada"],correct:2},

{question:"What is the capital of Turkey?",answers:["Istanbul","Ankara","Tehran","Athens"],correct:1},
{question:"What is the currency of Japan?",answers:["Won","Yuan","Yen","Ringgit"],correct:2},
{question:"How many chambers are in the human heart?",answers:["2","3","4","5"],correct:2},
{question:"What is the national flower of Pakistan?",answers:["Rose","Tulip","Jasmine","Lily"],correct:2},
{question:"Which is the largest planet in our solar system?",answers:["Earth","Mars","Jupiter","Venus"],correct:2},
{question:"Who invented the light bulb?",answers:["Thomas Edison","Nikola Tesla","Isaac Newton","Michael Faraday"],correct:0},
{question:"What is the speed of light?",answers:["300,000 km/s","150,000 km/s","500,000 km/s","1,000 km/s"],correct:0},
{question:"The Great Wall is located in which country?",answers:["India","China","Japan","Mongolia"],correct:1},
{question:"In which year was the United Nations founded?",answers:["1945","1939","1918","1950"],correct:0},
{question:"Which blood group is universal donor?",answers:["A","B","AB","O Negative"],correct:3},

{question:"What is the capital of Canada?",answers:["Toronto","Ottawa","Vancouver","Montreal"],correct:1},
{question:"Which is the longest river in the world?",answers:["Amazon","Nile","Yangtze","Indus"],correct:1},
{question:"In which year did Pakistan gain independence?",answers:["1945","1946","1947","1948"],correct:2},
{question:"Which organ pumps blood in the human body?",answers:["Brain","Lungs","Heart","Kidney"],correct:2},
{question:"What is the currency of the United States?",answers:["Dollar","Euro","Peso","Pound"],correct:0},
{question:"Which is the largest island in the world?",answers:["Greenland","Iceland","Madagascar","Borneo"],correct:0},
{question:"Who painted the Mona Lisa?",answers:["Vincent Van Gogh","Pablo Picasso","Leonardo da Vinci","Michelangelo"],correct:2},
{question:"What is the hardest natural substance?",answers:["Gold","Iron","Diamond","Silver"],correct:2},
{question:"The pyramids are located in which country?",answers:["Mexico","Peru","Egypt","India"],correct:2},
{question:"What is the center of our solar system?",answers:["Earth","Moon","Sun","Mars"],correct:2},

{question:"Which vitamin is obtained from sunlight?",answers:["A","B","C","D"],correct:3},
{question:"Which is the tallest animal?",answers:["Elephant","Giraffe","Horse","Camel"],correct:1},
{question:"What is the freezing point of water?",answers:["0°C","10°C","-5°C","5°C"],correct:0},
{question:"The Indus River originates from?",answers:["India","China","Tibet","Nepal"],correct:2},
{question:"Who was Quaid-e-Azam?",answers:["Allama Iqbal","Muhammad Ali Jinnah","Liaquat Ali Khan","Sir Syed Ahmad Khan"],correct:1},
{question:"Which metal is liquid at room temperature?",answers:["Iron","Mercury","Gold","Copper"],correct:1},
{question:"Who won the FIFA World Cup 2022?",answers:["France","Brazil","Argentina","Germany"],correct:2},
{question:"Which is the smallest planet in our solar system?",answers:["Mercury","Mars","Venus","Pluto"],correct:0},
{question:"How many bones are in an adult human body?",answers:["206","210","201","196"],correct:0},
{question:"Which country is called the Land of the Rising Sun?",answers:["China","Japan","Thailand","Korea"],correct:1},
{question:"Fastest bird in the world?",answers:["Eagle","Peregrine Falcon","Sparrow","Hawk"],correct:1},
{question:"National language of Pakistan?",answers:["Urdu","Punjabi","Sindhi","Pashto"],correct:0},
{question:"Chemical symbol for gold?",answers:["Ag","Au","Pb","Fe"],correct:1},
{question:"Longest railway in the world?",answers:["Trans-Siberian","Indian","Canadian","Orient Express"],correct:0},
{question:"Largest mammal?",answers:["Elephant","Blue Whale","Giraffe","Hippopotamus"],correct:1}

];

let currentQuestion = 0;
let score = 0;
let timeLeft = 10;
let timer;

const questionEl = document.getElementById("question");
const answersEl = document.getElementById("answers");
const resultEl = document.getElementById("result");
const scoreEl = document.getElementById("score");
const timeEl = document.getElementById("time");

function startTimer() {
    timeLeft = 10;
    timeEl.textContent = timeLeft;

    timer = setInterval(() => {
        timeLeft--;
        timeEl.textContent = timeLeft;

        if (timeLeft === 0) {
            clearInterval(timer);
            autoNext();
        }
    }, 1000);
}

function loadQuestion() {
    clearInterval(timer);
    const q = questions[currentQuestion];
    questionEl.textContent = (currentQuestion + 1) + ". " + q.question;
    answersEl.innerHTML = "";

    q.answers.forEach((answer, index) => {
        const btn = document.createElement("button");
        btn.textContent = answer;
        btn.onclick = () => selectAnswer(btn, index);
        answersEl.appendChild(btn);
    });

    startTimer();
}

function selectAnswer(button, index) {
    clearInterval(timer);
    const buttons = answersEl.querySelectorAll("button");
    buttons.forEach(btn => btn.disabled = true);

    if (index === questions[currentQuestion].correct) {
        button.classList.add("correct");
        score++;
    } else {
        button.classList.add("wrong");
        buttons[questions[currentQuestion].correct].classList.add("correct");
    }

    setTimeout(autoNext, 1000);
}

function autoNext() {
    currentQuestion++;
    if (currentQuestion < questions.length) {
        loadQuestion();
    } else {
        showResult();
    }
}

function showResult() {
    document.getElementById("quiz").classList.add("hidden");
    resultEl.classList.remove("hidden");
    document.querySelector(".timer").style.display = "none";
    scoreEl.textContent = score + " / " + questions.length;
}

function restartQuiz() {
    currentQuestion = 0;
    score = 0;
    resultEl.classList.add("hidden");
    document.getElementById("quiz").classList.remove("hidden");
    document.querySelector(".timer").style.display = "block";
    loadQuestion();
}

loadQuestion();

</script>
</body>
</html>
