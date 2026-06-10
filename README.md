# Reaction-Time-Project
var startTime = 0;
var reactionTime = 0;
var bestTime = 999;
var totalTime = 0;
var round = 0;
var maxRounds = 5;
var waiting = false;
var canReact = false;
var nextRound;
onEvent("startBtn", "click", function() {
  round = 0;
  totalTime = 0;
  bestTime = 999;
  nextRound();
});
function nextRound() {
  if (round >= maxRounds) {
    return showResults;
  }

  round++;
  setText("statusText", "Wait for green...");
  setProperty("screen1", "background-color", "red");

  canReact = false;
  waiting = true;

  var delay = randomNumber(2000, 5000);

  setTimeout(function() {
    setProperty("screen1", "background-color", "green");
    setText("statusText", "CLICK!");
    startTime = getTime();
    canReact = true;
    waiting = false;
  }, delay);
}
onEvent("reactBtn", "click", function() {
 setProperty("reactBtn", "x", randomNumber(1, 200));

if (waiting) {
    setText("statusText", "Too early!");
    return;
  }

if (canReact) {
    reactionTime = getTime() - startTime;

    totalTime += reactionTime;


    setText("statusText", "Reaction: " + reactionTime + " ms");

    canReact = false;

    setTimeout(nextRound, 1000);
  }
if (reactionTime < bestTime) {
  bestTime = reactionTime;
}
});
function showResults() {
  var average = totalTime / maxRounds;

  setText("statusText", "Done!");
  setText("resultText",
    "Avg: " + average + " ms\n" +
    "Best: " + bestTime + " ms\n" +
    "Machine: 10 ms"
  );
}
