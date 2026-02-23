# 50-General-Knowledge-Questions-
In this file we will test 50 GK Objective questions mostly repeated in STS, LAT, CSS, and many more tests.

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
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    color: white;
}

.quiz-container {
    background: rgba(0, 0, 0, 0.75);
    padding: 30px;
    border-radius: 15px;
    width: 95%;
    max-width: 500px;
    text-align: center;
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
    transition: 0.2s;
}

.answers button:hover {
    background: #ffd700;
}

#next-btn {
    margin-top: 15px;
    padding: 8px 20px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background: #00c853;
    color: white;
    font-weight: bold;
    display: none;
}

.hidden {
    display: none;
}
</style>
</head>

<body>

<div class="quiz-container">
    <h1>General Knowledge Quiz (50 Questions)</h1>

    <div id="quiz">
        <h2 id="question"></h2>
        <div id="answers" class="answers"></div>
        <button id="next-btn">Next</button>
    </div>

    <div id="result" class="hidden">
        <h2>Your Score: <span id="score"></span></h2>
        <button onclick="restartQuiz()">Restart Quiz</button>
    </div>
</div>

<script>

const questions = [

{question:"Capital of Pakistan?",answers:["Lahore","Karachi","Islamabad","Peshawar"],correct:2},
{question:"Largest continent?",answers:["Africa","Asia","Europe","Australia"],correct:1},
{question:"Largest ocean?",answers:["Indian","Pacific","Atlantic","Arctic"],correct:1},
{question:"Inventor of telephone?",answers:["Newton","Einstein","Bell","Tesla"],correct:2},
{question:"Red Planet?",answers:["Earth","Mars","Jupiter","Saturn"],correct:1},
{question:"National animal of Pakistan?",answers:["Lion","Markhor","Tiger","Leopard"],correct:1},
{question:"Fastest land animal?",answers:["Lion","Cheetah","Tiger","Horse"],correct:1},
{question:"Smallest continent?",answers:["Asia","Europe","Australia","Africa"],correct:2},
{question:"Mount Everest is in?",answers:["India","China","Nepal","Bhutan"],correct:2},
{question:"Currency of UK?",answers:["Dollar","Euro","Pound","Rupee"],correct:2},

{question:"Who wrote Hamlet?",answers:["Shakespeare","Dickens","Milton","Keats"],correct:0},
{question:"H2O is?",answers:["Salt","Oxygen","Water","Hydrogen"],correct:2},
{question:"Largest desert?",answers:["Sahara","Gobi","Arabian","Thar"],correct:0},
{question:"How many continents?",answers:["5","6","7","8"],correct:2},
{question:"National sport of Pakistan?",answers:["Hockey","Cricket","Football","Squash"],correct:0},
{question:"Who discovered gravity?",answers:["Newton","Galileo","Tesla","Darwin"],correct:0},
{question:"Capital of France?",answers:["Rome","Paris","Madrid","Berlin"],correct:1},
{question:"First man on moon?",answers:["Buzz","Yuri","Neil Armstrong","Michael"],correct:2},
{question:"Plants absorb?",answers:["Oxygen","Carbon Dioxide","Nitrogen","Hydrogen"],correct:1},
{question:"Largest country?",answers:["USA","China","Russia","Canada"],correct:2},

{question:"Capital of Turkey?",answers:["Istanbul","Ankara","Tehran","Athens"],correct:1},
{question:"Currency of Japan?",answers:["Won","Yuan","Yen","Ringgit"],correct:2},
{question:"Heart chambers?",answers:["2","3","4","5"],correct:2},
{question:"National flower of Pakistan?",answers:["Rose","Tulip","Jasmine","Lily"],correct:2},
{question:"Largest planet?",answers:["Earth","Mars","Jupiter","Venus"],correct:2},
{question:"Inventor of bulb?",answers:["Edison","Tesla","Newton","Faraday"],correct:0},
{question:"Speed of light?",answers:["300k km/s","150k","500k","1k"],correct:0},
{question:"Great Wall country?",answers:["India","China","Japan","Mongolia"],correct:1},
{question:"UN founded?",answers:["1945","1939","1918","1950"],correct:0},
{question:"Universal donor?",answers:["A","B","AB","O-"],correct:3},

{question:"Capital of Canada?",answers:["Toronto","Ottawa","Vancouver","Montreal"],correct:1},
{question:"Longest river?",answers:["Amazon","Nile","Yangtze","Indus"],correct:1},
{question:"Pakistan independence year?",answers:["1945","1946","1947","1948"],correct:2},
{question:"Organ pumps blood?",answers:["Brain","Lungs","Heart","Kidney"],correct:2},
{question:"Currency USA?",answers:["Dollar","Euro","Peso","Pound"],correct:0},
{question:"Largest island?",answers:["Greenland","Iceland","Madagascar","Borneo"],correct:0},
{question:"Mona Lisa painter?",answers:["Van Gogh","Picasso","Da Vinci","Michelangelo"],correct:2},
{question:"Hardest natural substance?",answers:["Gold","Iron","Diamond","Silver"],correct:2},
{question:"Pyramids country?",answers:["Mexico","Peru","Egypt","India"],correct:2},
{question:"Solar system center?",answers:["Earth","Moon","Sun","Mars"],correct:2},

{question:"Vitamin from sunlight?",answers:["A","B","C","D"],correct:3},
{question:"Tallest animal?",answers:["Elephant","Giraffe","Horse","Camel"],correct:1},
{question:"Freezing point of water?",answers:["0°C","10°C","-5°C","5°C"],correct:0},
{question:"Indus originates from?",answers:["India","China","Tibet","Nepal"],correct:2},
{question:"Quaid-e-Azam full name?",answers:["Iqbal","Jinnah","Liaquat","Sir Syed"],correct:1},
{question:"Metal liquid at room temp?",answers:["Iron","Mercury","Gold","Copper"],correct:1},
{question:"FIFA 2022 winner?",answers:["France","Brazil","Argentina","Germany"],correct:2},
{question:"Smallest planet?",answers:["Mercury","Mars","Venus","Pluto"],correct:0},
{question:"Human bones?",answers:["206","210","201","196"],correct:0},
{question:"City of Lights (Pakistan)?",answers:["Lahore","Karachi","Islamabad","Quetta"],correct:1}

];

let currentQuestion = 0;
let score = 0;

const questionEl = document.getElementById("question");
const answersEl = document.getElementById("answers");
const nextBtn = document.getElementById("next-btn");
const resultEl = document.getElementById("result");
const scoreEl = document.getElementById("score");

function loadQuestion() {
    const q = questions[currentQuestion];
    questionEl.textContent = (currentQuestion+1) + ". " + q.question;
    answersEl.innerHTML = "";
    nextBtn.style.display = "none";

    q.answers.forEach((answer, index) => {
        const btn = document.createElement("button");
        btn.textContent = answer;
        btn.onclick = () => selectAnswer(index);
        answersEl.appendChild(btn);
    });
}

function selectAnswer(index) {
    if (index === questions[currentQuestion].correct) {
        score++;
    }
    nextBtn.style.display = "block";
}

nextBtn.onclick = () => {
    currentQuestion++;
    if (currentQuestion < questions.length) {
        loadQuestion();
    } else {
        showResult();
    }
};

function showResult() {
    document.getElementById("quiz").classList.add("hidden");
    resultEl.classList.remove("hidden");
    scoreEl.textContent = score + " / " + questions.length;
}

function restartQuiz() {
    currentQuestion = 0;
    score = 0;
    resultEl.classList.add("hidden");
    document.getElementById("quiz").classList.remove("hidden");
    loadQuestion();
}

loadQuestion();

</script>

</body>
</html>
