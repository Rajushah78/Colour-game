# Colour-game
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ultimate 5 Second Color Challenge</title>

<style>
body{
margin:0;
font-family:Arial, sans-serif;
text-align:center;
background:linear-gradient(135deg,#ff512f,#dd2476);
color:white;
}

header{
background:black;
padding:15px;
font-size:22px;
font-weight:bold;
}

.container{
padding:20px;
}

button{
padding:12px 20px;
margin:8px;
font-size:16px;
border:none;
border-radius:10px;
cursor:pointer;
transition:0.3s;
}

button:hover{
transform:scale(1.05);
}

.color-btn{
width:40%;
}

#timer{
font-size:20px;
margin:10px;
}

#leaderboard{
background:rgba(0,0,0,0.4);
padding:15px;
border-radius:12px;
margin-top:20px;
}

#adBox{
display:none;
background:white;
color:black;
padding:20px;
position:fixed;
top:50%;
left:50%;
transform:translate(-50%,-50%);
border-radius:15px;
width:80%;
max-width:300px;
}

input{
padding:10px;
border-radius:8px;
border:none;
margin:10px;
width:80%;
}

</style>
</head>

<body>

<header>🔥 Ultimate Color Challenge 🔥</header>

<div class="container">

<input type="text" id="username" placeholder="Enter Your Name">

<h2 id="colorText">Press Start</h2>
<div id="timer">Time: 5</div>

<div>
<button class="color-btn" style="background:red;color:white;" onclick="check('Red')">Red</button>
<button class="color-btn" style="background:green;color:white;" onclick="check('Green')">Green</button><br>
<button class="color-btn" style="background:blue;color:white;" onclick="check('Blue')">Blue</button>
<button class="color-btn" style="background:yellow;color:black;" onclick="check('Yellow')">Yellow</button>
</div>

<h2>Score: <span id="score">0</span></h2>

<button onclick="startGame()">Start Game</button>
<button onclick="shareScore()">Share</button>

<div id="leaderboard">
<h3>🏆 Leaderboard</h3>
<ul id="topScores"></ul>
</div>

</div>

<div id="adBox">
<h3>Advertisement</h3>
<p>Your Ad Code Here</p>
<button onclick="closeAd()">Close</button>
<button onclick="continueGame()">Continue (+Ad)</button>
</div>

<audio id="winSound" src="https://www.soundjay.com/buttons/sounds/button-3.mp3"></audio>
<audio id="loseSound" src="https://www.soundjay.com/buttons/sounds/button-10.mp3"></audio>

<script>

let colors=["Red","Green","Blue","Yellow"];
let currentColor="";
let score=0;
let timeLeft=5;
let timer;

function startGame(){
let name=document.getElementById("username").value;
if(name==""){
alert("Enter Your Name First!");
return;
}
score=0;
document.getElementById("score").innerHTML=score;
nextRound();
}

function nextRound(){
timeLeft=5;
document.getElementById("timer").innerHTML="Time: "+timeLeft;
currentColor=colors[Math.floor(Math.random()*colors.length)];
document.getElementById("colorText").innerHTML=currentColor;

clearInterval(timer);
timer=setInterval(function(){
timeLeft--;
document.getElementById("timer").innerHTML="Time: "+timeLeft;
if(timeLeft<=0){
clearInterval(timer);
gameOver();
}
},1000);
}

function check(choice){
if(choice===currentColor){
score+=10;
document.getElementById("score").innerHTML=score;
document.getElementById("winSound").play();
nextRound();
}else{
document.getElementById("loseSound").play();
clearInterval(timer);
gameOver();
}
}

function gameOver(){
saveScore();
document.getElementById("adBox").style.display="block";
}

function closeAd(){
document.getElementById("adBox").style.display="none";
}

function continueGame(){
document.getElementById("adBox").style.display="none";
nextRound();
}

function saveScore(){
let name=document.getElementById("username").value;
let scores=JSON.parse(localStorage.getItem("scores"))||[];
scores.push({name:name,score:score});
scores.sort((a,b)=>b.score-a.score);
scores=scores.slice(0,5);
localStorage.setItem("scores",JSON.stringify(scores));
displayScores();
}

function displayScores(){
let scores=JSON.parse(localStorage.getItem("scores"))||[];
let list=document.getElementById("topScores");
list.innerHTML="";
scores.forEach(s=>{
let li=document.createElement("li");
li.innerText=s.name+" - "+s.score;
list.appendChild(li);
});
}

function shareScore(){
let text="I scored "+score+" in Ultimate Color Challenge!";
navigator.clipboard.writeText(text);
alert("Score Copied! Share with friends.");
}

displayScores();

</script>

</body>
</html>
