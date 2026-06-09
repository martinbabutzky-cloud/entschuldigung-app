<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interaktive Lern-App: Entschuldigen</title>
<style>
body { font-family: Arial, sans-serif; margin: 0; background: #f4f6f8; }
header { background: #2f3e46; color: white; padding: 15px; text-align: center; }
nav { display: flex; justify-content: center; gap: 10px; padding: 10px; }
button { padding: 10px 15px; border: none; border-radius: 8px; cursor: pointer; }
.section { display: none; padding: 20px; }
.active { display: block; }
.card { background: white; padding: 15px; border-radius: 12px; margin-bottom: 15px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); }
.correct { color: green; }
.wrong { color: red; }
</style>
</head>
<body>
<header>
<h1>Sich richtig entschuldigen</h1>
<p>Selbstlern-App für den Ethikunterricht</p>
</header>

<nav>
<button onclick="showSection('theorie')">Theorie</button>
<button onclick="showSection('quiz')">Quiz</button>
<button onclick="showSection('analyse')">Fallanalyse</button>
<button onclick="showSection('schreiben')">Selbst schreiben</button>
</nav>

<div id="theorie" class="section active">
<div class="card">
<h2>Warum ist Entschuldigen schwer?</h2>
<p>Entschuldigen bedeutet, Verantwortung zu übernehmen und Verletzlichkeit zu zeigen. Das fällt schwer, weil es unser Selbstbild bedroht.</p>
</div>
<div class="card">
<h2>Die 5 Schritte einer echten Entschuldigung</h2>
<ol>
<li>Fehler klar benennen</li>
<li>Verantwortung übernehmen</li>
<li>Gefühle des anderen anerkennen</li>
<li>Wiedergutmachung anbieten</li>
<li>Veränderung zeigen</li>
</ol>
</div>
<div class="card">
<h2>Pseudo-Entschuldigungen vermeiden</h2>
<ul>
<li>"Tut mir leid, aber ..."</li>
<li>"Falls du dich verletzt fühlst..."</li>
<li>"Ich hatte so viel Stress..."</li>
</ul>
</div>
</div>

<div id="quiz" class="section">
<div class="card">
<h2>Quiz: Echte oder falsche Entschuldigung?</h2>
<p id="quizQuestion"></p>
<button onclick="checkAnswer(true)">Echt</button>
<button onclick="checkAnswer(false)">Falsch</button>
<p id="quizFeedback"></p>
</div>
</div>

<div id="analyse" class="section">
<div class="card">
<h2>Fallanalyse</h2>
<p>Du hast einen Mitschüler öffentlich ausgelacht. Was wäre eine gute Entschuldigung?</p>
<textarea id="analyseInput" rows="4" style="width:100%"></textarea>
<button onclick="analyseText()">Überprüfen</button>
<p id="analyseFeedback"></p>
</div>
</div>

<div id="schreiben" class="section">
<div class="card">
<h2>Eigene Entschuldigung schreiben</h2>
<p>Denke an eine Situation aus deinem Alltag und formuliere eine echte Entschuldigung:</p>
<textarea rows="5" style="width:100%"></textarea>
</div>
</div>

<script>
function showSection(id) {
 document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
}

const questions = [
 { text: "Es tut mir leid, aber du hast angefangen.", answer: false },
 { text: "Ich habe dich verletzt. Das war falsch.", answer: true },
 { text: "Sorry, wenn du dich schlecht fühlst.", answer: false },
 { text: "Ich übernehme Verantwortung und möchte es wiedergutmachen.", answer: true }
];
let current = 0;

function loadQuestion() {
 document.getElementById('quizQuestion').textContent = questions[current].text;
 document.getElementById('quizFeedback').textContent = '';
}

function checkAnswer(ans) {
 const correct = questions[current].answer;
 const feedback = document.getElementById('quizFeedback');
 if (ans === correct) {
 feedback.textContent = "Richtig!";
 feedback.className = 'correct';
 } else {
 feedback.textContent = "Leider falsch.";
 feedback.className = 'wrong';
 }
 current = (current + 1) % questions.length;
 setTimeout(loadQuestion, 1000);
}

function analyseText() {
 const text = document.getElementById('analyseInput').value.toLowerCase();
 let feedback = "";
 if (text.includes("aber")) {
 feedback += "Vermeide 'aber' – das schwächt die Entschuldigung. ";
 }
 if (!text.includes("ich")) {
 feedback += "Übernimm klar Verantwortung (Ich-Botschaften). ";
 }
 if (text.length < 20) {
 feedback += "Versuche ausführlicher zu schreiben. ";
 }
 if (feedback === "") feedback = "Gute Entschuldigung!";
 document.getElementById('analyseFeedback').textContent = feedback;
}

loadQuestion();
</script>

</body>
</html>
