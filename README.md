//I started by coding in code.org's App Lab, then pasted to GitHub. AI assisted me in one line of code. Also somewhat helped with debugging, however i did most of it. My own original code and project driven by my passion for hands-on research. Spent 2 days brainstorming, then 3 hours a week for 1 week making code, then 4 hours a week finding a control group to conduct research. 
 (javascript)
var time = 0;
var sleep = 0;
var screenTime = 0;
var reactionTime = 0;
var score;
var startTime = 0;
var bestTime = 999;
var totalTime = 0;
var round = 0;
var maxRounds = 5;
var waiting = false;
var canReact = false;
var timeScore;
hideElement("Upbutton");
onEvent("startBut", "click", function( ) {
  showElement("Upbutton");
  hideElement("dropdown4");
  hideElement("dropdown2");
  hideElement("dropdown3");
  round = 0;
  totalTime = 0;
  bestTime = 999;
  nextRound();
  hideElement("startBut");
});
if (score == 14) {
  setText("text_area1", "Very good!");
} else if ((score == 10)) {
  setText("text_area1", "Its ok.");
} else {
  setText("text_area1", "You need some help.");
}
score = (sleep * 2 + time * 3) + (screenTime * 1.5 + reactionTime * 2);
sleep = getNumber("dropdown4");
screenTime = getNumber("dropdown2");
time = getText("dropdown3");
if (getText("dropdown3") == "Afternoon") {
  timeScore = 5;
} else if ((getText("dropdown3") == "Evening")) {
  timeScore = 10;
} else {
  timeScore = 1;
}
if (reactionTime == 510) {
  setText("text_area2", "Too slow! You need help!");
}
function nextRound() {
  if (round >= maxRounds) {
   showResults();
   return;
  }

  round++;
  setText("text_area2", "Wait for green...");
  setProperty("screen1", "background-color", "red");

  canReact = false;
  waiting = true;

  var delay = randomNumber(2000, 5000);

  setTimeout(function() {
    setProperty("screen1", "background-color", "green");
    setText("text_area2", "CLICK!");
    startTime = getTime();
    canReact = true;
    waiting = false;
  }, delay);
}
onEvent("Upbutton", "click", function() {
 setProperty("Upbutton", "x", randomNumber(1, 200));

if (waiting) {
    setText("text_area2", "Too early!");
    return;
  }

if (canReact) {
    reactionTime = getTime() - startTime;

    totalTime += reactionTime;


    setText("text_area2", "Reaction: " + reactionTime + " ms");

    canReact = false;

    setTimeout(nextRound, 1000);
  }
if (reactionTime < bestTime) {
  bestTime = reactionTime;
}
});
function showResults() {
  var average = totalTime / maxRounds;

  setScreen("screen2");
  setText("text_area2", "Done!");
  setText("text_area4",
    "Avg: " + average + " ms\n" +
    "Best: " + bestTime + " ms\n" +
    "Machine: 10 ms"
  );
  return average;
}
showScore();
function showScore() {
  setText("text_area3", score);
  return score;
}
