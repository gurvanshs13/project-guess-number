# project-guess-number

let randomNumber = Math.floor(Math.random() * 100+1);

const submit = document.querySelector('#subt');
const userInput = document.querySelector('#guessField');
const guessSlot = document.querySelector('.guesses');
const remaining = document.querySelector('.lastResult');
const lowOrHi = document.querySelector('.lowOrHi');
const startOver = document.querySelector('.resultParas');

const p = document.createElement('p');

let prevGuess = [];
let numGuess = 1;

let playGame = true;

if(playGame){
submit.addEventListener('click', function(e){
  e.preventDefault();
const guess = Math.round(userInput.value) ;
validateGuess(guess)
})
}

function validateGuess(guess){
if(isNaN(guess) ){
  alert("Enter a valid number")
} else if(guess > 100 || guess < 1){
  alert("Enter number in the specified range ")
} else{
  prevGuess.push(guess);
  if(numGuess == 11){
    displayMessage(`GameOver the number was ${randomNumber}`);
    endgame();
  } else {
    checkGuess(guess);
    displayGuess(guess);
  }
}
}

function checkGuess(guess){
  if(guess == randomNumber){
    displayMessage("You Guessed it right");
    endgame()
  } else if(guess > randomNumber){
    displayMessage("The number is lower");
  }else if (guess < randomNumber){
    displayMessage("The number is higher");
  }
}

function displayGuess(guess){
  numGuess++;
  userInput.value = ''
  guessSlot.innerHTML += `${guess}, `
  remaining.innerHTML = `${11 - numGuess}`;
}

function displayMessage(message){
lowOrHi.innerHTML = `${message}`;
}

function endgame(){
  p.classList.add('button');
  p.innerHTML = `<p id = "newgame">Game Over Start Again</p>`;
  startOver.appendChild(p);
  userInput.value = ''
  userInput.setAttribute("disabled", "")

  playGame = false;
  newgame();
}

function newgame(){
  const newGame = document.querySelector('#newgame');
  newGame.addEventListener('mouseover',function(e){
    alert("New Game ??")
    displayMessage('');
    randomNumber = Math.floor(Math.random() * 100+1);
    prevGuess = [];
    numGuess = 1;
    guessSlot.innerHTML = '';
    remaining.innerHTML = `${11 - numGuess}`;
    userInput.removeAttribute('disabled');
    startOver.removeChild(p);
    playGame = true;
  })
  
}
