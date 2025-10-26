<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lucky Spin Win India</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');
  body {
    margin:0;
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%);
    color: #333;
  }
  .container {
    max-width: 800px;
    margin: auto;
    padding: 20px;
  }
  h1,h2,h3 {text-align:center;}
  button {
    padding:10px 20px;
    margin:5px;
    border:none;
    border-radius:5px;
    cursor:pointer;
    background: #ff6b81;
    color:white;
    font-weight:600;
    transition:0.3s;
  }
  button:hover {background:#ff4757;}
  input {padding:10px;margin:5px;width:calc(100%-24px);border-radius:5px;border:1px solid #ccc;}
  .hidden {display:none;}
  .game-section {margin-top:20px; text-align:center;}
  #spinner {
    width:200px;height:200px;margin:auto;
    border:10px solid #fff;border-radius:50%;
    position:relative;
    background: conic-gradient(#ff6b81 0% 25%, #1e90ff 25% 50%, #2ed573 50% 75%, #ffa502 75% 100%);
    transition: transform 4s cubic-bezier(0.25,1,0.5,1);
  }
  #spinner::after {
    content:'▼';
    position:absolute;
    top:-30px;
    left:50%;
    transform:translateX(-50%);
    font-size:30px;
    color:#fff;
  }
  .wallet, .leaderboard, .puzzle {margin-top:20px;}
  .puzzle button {display:block;margin:10px auto;}
  .success {color:green;font-weight:600;}
  .error {color:red;font-weight:600;}
</style>
</head>
<body>
<div class="container">
  <div id="login-section">
    <h1>Lucky Spin Win India</h1>
    <h3>Login / Signup</h3>
    <input type="text" id="username" placeholder="Enter your name" />
    <button onclick="login()">Login / Signup</button>
    <p id="login-msg"></p>
  </div>

  <div id="main-section" class="hidden">
    <h2>Welcome, <span id="user-name"></span>!</h2>
    <div class="wallet">
      <h3>Your Balance: <span id="balance">100</span> coins</h3>
    </div>

    <div class="game-section">
      <h3>🎡 Spinner Game</h3>
      <div id="spinner"></div>
      <button onclick="spin()">Spin Now</button>
      <p id="spin-result"></p>
    </div>

    <div class="game-section puzzle">
      <h3>🧩 Puzzle Quiz</h3>
      <p id="puzzle-question"></p>
      <div id="puzzle-options"></div>
      <p id="puzzle-msg"></p>
    </div>

    <div class="game-section leaderboard">
      <h3>🏆 Leaderboard</h3>
      <ol id="leaderboard-list">
        <li>Rohit - 500 coins</li>
        <li>Priya - 450 coins</li>
        <li>Amit - 400 coins</li>
      </ol>
    </div>

    <button onclick="logout()">Logout</button>
  </div>
</div>

<script>
  // Login / Signup
  let user = '';
  let balance = 100;
  const puzzles = [
    {q:"What is 5 + 3?", options:["7","8","9","6"], ans:"8"},
    {q:"Which is a fruit?", options:["Carrot","Apple","Potato","Tomato"], ans:"Apple"},
    {q:"What is the capital of India?", options:["Mumbai","Delhi","Kolkata","Chennai"], ans:"Delhi"}
  ];
  let puzzleIndex = 0;

  function login(){
    const username = document.getElementById('username').value.trim();
    if(username===''){document.getElementById('login-msg').innerText="Enter a valid name"; return;}
    user=username;
    document.getElementById('user-name').innerText=user;
    document.getElementById('login-section').classList.add('hidden');
    document.getElementById('main-section').classList.remove('hidden');
    updatePuzzle();
  }

  function logout(){
    document.getElementById('login-section').classList.remove('hidden');
    document.getElementById('main-section').classList.add('hidden');
    document.getElementById('username').value='';
    document.getElementById('login-msg').innerText='';
    balance=100;
    document.getElementById('balance').innerText=balance;
  }

  // Spinner Game
  function spin(){
    const spinner=document.getElementById('spinner');
    const spins = Math.floor(Math.random()*360) + 720; // 2-3 rotations
    spinner.style.transform = `rotate(${spins}deg)`;
    const sectors = ["100","50","200","10"];
    setTimeout(()=>{
      const won=sectors[Math.floor(Math.random()*sectors.length)];
      balance+=parseInt(won);
      document.getElementById('balance').innerText=balance;
      document.getElementById('spin-result').innerText=`You won ${won} coins! 🎉`;
    },4000);
  }

  // Puzzle Game
  function updatePuzzle(){
    const puzzle=document.getElementById('puzzle-question');
    const optionsDiv=document.getElementById('puzzle-options');
    puzzle.textContent=puzzles[puzzleIndex].q;
    optionsDiv.innerHTML='';
    puzzles[puzzleIndex].options.forEach(opt=>{
      const btn=document.createElement('button');
      btn.textContent=opt;
      btn.onclick=()=>checkPuzzle(opt);
      optionsDiv.appendChild(btn);
    });
    document.getElementById('puzzle-msg').textContent='';
  }

  function checkPuzzle(answer){
    const msg=document.getElementById('puzzle-msg');
    if(answer===puzzles[puzzleIndex].ans){
      msg.textContent="Correct! You earned 50 coins 🎉";
      msg.className='success';
      balance+=50;
      document.getElementById('balance').innerText=balance;
    } else {
      msg.textContent="Wrong answer 😢";
      msg.className='error';
    }
    puzzleIndex=(puzzleIndex+1)%puzzles.length;
    setTimeout(updatePuzzle,1500);
  }
</script>
</body>
</html>
