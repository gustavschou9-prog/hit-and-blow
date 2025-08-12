<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Hit & Blow - Turn Based</title>
<style>
  body { font-family: sans-serif; max-width: 500px; margin: auto; padding: 20px; background: #f9f9f9; }
  h1 { text-align: center; }
  .section { margin: 20px 0; padding: 15px; background: white; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
  input, button { padding: 8px; font-size: 1rem; margin-top: 8px; width: 100%; box-sizing: border-box; }
  button { cursor: pointer; }
  ul { padding: 0; list-style: none; }
  li { padding: 5px 0; border-bottom: 1px solid #ddd; }
</style>
</head>
<body>
<h1>Hit & Blow</h1>
<div id="setup" class="section">
  <h2>Start a New Game</h2>
  <label>Secret Number (4 unique digits):<br><input id="secretInput" maxlength="4" pattern="\\d{4}" /></label>
  <button onclick="createGame()">Create Game & Get Link</button>
  <p id="gameLink"></p>
</div>

<div id="guessSection" class="section" style="display:none;">
  <h2>Make a Guess</h2>
  <input id="guessInput" maxlength="4" pattern="\\d{4}" placeholder="Enter 4 digits" />
  <button onclick="makeGuess()">Submit Guess</button>
  <ul id="history"></ul>
</div>

<script>
function createGame(){
  const secret = document.getElementById('secretInput').value.trim();
  if(!/^\d{4}$/.test(secret) || new Set(secret).size !== 4){
    alert('Please enter 4 unique digits.');
    return;
  }
  const encoded = btoa(secret);
  const link = window.location.origin + window.location.pathname + '?code=' + encoded;
  document.getElementById('gameLink').innerHTML = `<a href="${link}">${link}</a>`;
}

function makeGuess(){
  const guess = document.getElementById('guessInput').value.trim();
  if(!/^\d{4}$/.test(guess) || new Set(guess).size !== 4){
    alert('Guess must be 4 unique digits.');
    return;
  }
  const result = checkGuess(secretNumber, guess);
  const li = document.createElement('li');
  li.textContent = `${guess} → ${result.hits} Hit(s), ${result.blows} Blow(s)`;
  document.getElementById('history').prepend(li);
  document.getElementById('guessInput').value = '';
  if(result.hits === 4){
    alert('You guessed it! 🎉');
  }
}

function checkGuess(secret, guess){
  let hits = 0, blows = 0;
  for(let i=0; i<4; i++){
    if(guess[i] === secret[i]) hits++;
    else if(secret.includes(guess[i])) blows++;
  }
  return {hits, blows};
}

// Load game if ?code= present
let secretNumber = null;
const params = new URLSearchParams(window.location.search);
if(params.has('code')){
  try {
    secretNumber = atob(params.get('code'));
    if(/^\d{4}$/.test(secretNumber)){
      document.getElementById('setup').style.display = 'none';
      document.getElementById('guessSection').style.display = 'block';
    }
  } catch(e){
    console.error('Invalid code');
  }
}
</script>
</body>
</html>
