# Games
Dice Guessing Game

var myHand = [1,2,3,4,5]
var opHand = [1,2,3,4,5]

var diceRoll = function(hand) {
  var tempHand = []
  for (var i = hand.length; i > 0; i--) {
    var newRoll = Math.floor(Math.random() * 6 + 1);
    tempHand.push(newRoll);
  }
  return tempHand;
};

function dicePrompt() {
  var callDice = parseInt(prompt("Your Roll: " + myHand + "\nWhat number will you be calling?"))
  return callDice;
};

function numberPrompt(dice) {
  var callNumber = parseInt(prompt("Your Roll: " + myHand + "\nHow many " + dice + " dices do you think there are?"));
  return callNumber;
}

function callDiceNumber() {
  var playerGuess = dicePrompt();
  while (isNaN(playerGuess) || playerGuess > 6 || playerGuess < 0) {
    alert("You selected, " + playerGuess + ". Please select a number from 1 - 6");
    playerGuess = dicePrompt();
  }
  var guessConfirm = confirm("You've called a " + playerGuess +" dice. Is this correct?");
  if (guessConfirm) {
    return playerGuess;
  } else {
    callDiceNumber();
  }
};

function callNumberOfDices(dice) {
  var playerGuess = numberPrompt(dice);
  while (isNaN(playerGuess) || playerGuess < 0) {
    alert("Please input the number of " + dice + " dices you think there are");
    playerGuess = numberPrompt(dice);
  }
  var guessConfirm = confirm("You've called a quantity of " + playerGuess +", is this correct?");
  if (guessConfirm) {
    return playerGuess;
  } else {
    callNumberOfDices(dice);
  }
};

function opTurn() {
  myHand = diceRoll(myHand);
  opHand = diceRoll(opHand);
  if (myHand.length === 0) {
    alert("You've lost all your dices! You lose!")
  } else if (opHand.length === 0) {
    alert("The computer has lost all of his dices! You win!")
  } else {
    var calledDice = Math.floor(Math.random() * 6 + 1);
    var numberOfDies = (myHand.length + opHand.length) / 2;
    var calledNumber = Math.floor(Math.random() * numberOfDies + 1);
    var counter = 0;
    for (var x = 0; x < myHand.length; x++) {
      if (calledDice === myHand[x]) {
        counter+= 1
      }
    }
    for (var x = 0; x < opHand.length; x++) {
      if (calledDice === opHand[x]) {
        counter+= 1
      }
    }
    if (calledNumber === counter) {
      alert("The computer guessed correctly! \nThere were actually " + counter + " " + "\[" + calledDice + "\]" + " dices");
      myHand.pop();
      opTurn();
    } else {
      alert("The computer was wrong! \nYour Hand " + myHand + " and your Opponents Hand " + opHand + "\nThe computer guessed there were " + calledNumber + " " + "\[" + calledDice + "\]" + " dices");
      alert("There were actually " + counter + " " + "\[" + calledDice + "\]" + " dices");
      roundStart();
    }
  }
};
  

function roundStart() {
  myHand = diceRoll(myHand);
  opHand = diceRoll(opHand);
  if (myHand.length === 0) {
    alert("You've lost all your dices! You lose!")
  } else if (opHand.length === 0) {
    alert("The computer has lost all of his dices! You win!")
  } else {
    var calledDice = callDiceNumber()
    var calledNumber = callNumberOfDices(calledDice)
    var playerGuess = confirm("You are guessing there are " + calledNumber + " " + "\[" + calledDice + "\]" + " dices. Is this correct?");
    if (playerGuess) {
      var counter = 0;
      for (var x = 0; x < myHand.length; x++) {
        if (calledDice === myHand[x]) {
          counter+= 1
        }
      }
      for (var x = 0; x < opHand.length; x++) {
        if (calledDice === opHand[x]) {
          counter+= 1
        }
      }
      if (calledNumber === counter) {
        alert("You've guessed correctly! \nThere were actually " + counter + " " + "\[" + calledDice + "\]" + " dices");
        alert("Your opponent loses a die!");
        opHand.pop();
        roundStart();
      } else {
        alert("You were wrong! \nYour Hand " + myHand + " and your Opponents Hand " + opHand);
        alert("You guessed there were " + calledNumber + " " + "\[" + calledDice + "\]" + " dices \nThere were actually " + counter + " " + "\[" + calledDice + "\]" + " dices");
        alert("It is now the computers turn!")
        opTurn();
      }
    } else {
      roundStart();
    }
  }
};

alert("The following game is a dice guessing game. You and the computer will start with 5 dices each. \n\nEvery time you guess the total number of dices correctly, the computer will lose a dice; however, every time the computer guesses correctly, you will lose a dice instead. \n\nThe first one to lose all their dices first will lose.")
var startGame = confirm("Would you like to start now?")
if (startGame) {
  roundStart()
};
