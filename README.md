# daddy moon 

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Daddy Moon - Play Free Color Challenge Game Online</title>

<meta name="description" content="Daddy Moon is a free online color challenge game. Play daily challenge, beat leaderboard and share with friends.">

<style>
body{
margin:0;
font-family:Arial, sans-serif;
background:#0f0f1a;
color:white;
text-align:center;
}

h1{
color:#00e0ff;
margin-top:20px;
}

#colorBox{
width:200px;
height:200px;
margin:20px auto;
border-radius:15px;
box-shadow:0 0 20px #00e0ff;
}

button{
padding:10px 20px;
margin:8px;
border:none;
border-radius:8px;
background:#00e0ff;
color:black;
font-weight:bold;
cursor:pointer;
}

button:hover{
background:#00b3cc;
}

#leaderboard{
margin-top:20px;
}

footer{
margin-top:30px;
font-size:14px;
opacity:0.7;
}
</style>
</head>

<body>

<h1>🌙 Daddy Moon Color Challenge</h1>
<p>Guess the correct color before time ends!</p>

<div id="colorBox"></div>

<div id="options"></div>

<h2 id="score">Score: 0</h2>
<h3 id="timer">Time: 30</h3>

<button onclick="shareScore()">Share Score</button>

<div id="leaderboard">
<h3>🏆 Top Score</h3>
<p id="topScore">0</p>
</div>

<footer>
© 2026 Daddy Moon | Free Online Color Game
</footer>

<script>

let score = 0;
let timeLeft = 30;
let topScore = localStorage.getItem("topScore") || 0;

document.getElementById("topScore").innerText = topScore;

const colors = ["red","blue","green","yellow","purple","orange","pink"];

function startTimer(){
setInterval(()=>{
timeLeft--;
document.getElementById("timer").innerText="Time: "+timeLeft;

if(timeLeft<=0){
if(score>topScore){
localStorage.setItem("topScore",score);
}
alert("Game Over! Your Score: "+score);
location.reload();
}

},1000);
}

function newGame(){
const randomColor = colors[Math.floor(Math.random()*colors.length)];
document.getElementById("colorBox").style.background=randomColor;

let shuffled = [...colors].sort(()=>0.5-Math.random()).slice(0,4);

let optionsHTML="";
shuffled.forEach(color=>{
optionsHTML+=`<button onclick="check('${color}','${randomColor}')">${color}</button>`;
});

document.getElementById("options").innerHTML=optionsHTML;
}

function check(selected,correct){
if(selected===correct){
score+=10;
document.getElementById("score").innerText="Score: "+score;
}
newGame();
}

function shareScore(){
let text = "I scored "+score+" points in Daddy Moon 🌙🔥 Can you beat me? Play now!";
window.open("https://wa.me/?text="+encodeURIComponent(text));
}

startTimer();
newGame();

</script>

</body>
</html>

