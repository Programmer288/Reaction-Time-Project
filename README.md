//I started by coding in code.org, then translated to text-console java in https://www.jdoodle.com/online-java-compiler, then pasted to GitHub. AI assisted me in three lines of code. Also somewhat helped with debugging, however i did most of it. My own original code and project driven by my passion for hands-on research. Spent 2 days brainstorming, then 3 hours a week for 1 week making Javascript code, then 4 hours a week finding a control group to conduct research. 
 (java)

import java.util.Random
import java.util.scanner

public class ReactionGame { 

static scanner input = new Scanner(System.in); //AI helped
static Random rand = new Random(); //AI helped
static int sleep;
static int ReactionTime;
static int screenTime;
static int bestTime = Integer.MAX_VALUE;
static int totalTime = 0;

static final int MAX_ROUNDS = 5;

public static void main(String[] args) throws InterruptedException { //assisted with AI
System.out.println("This is a reaction Time test.")
System.out.println("Reaction Time Test");

        System.out.print("Hours of sleep: ");
        sleep = input.nextInt();

        System.out.print("Hours of screen time: ");
        screenTime = input.nextInt();
        input.nextLine();

        System.out.print("Time of day (Morning, Afternoon, Evening): ");
        String time = input.nextLine();

        int timeScore;

        if (time.equalsIgnoreCase("Afternoon")) {
            timeScore = 5;
        } else if (time.equalsIgnoreCase("Evening")) {
            timeScore = 10;
        } else {
            timeScore = 1;
        }

        double score = (sleep * 2) + (timeScore * 3)
                     + (screenTime * 1.5);
System.out.println("\n-Press Enter to start.");
input.nextLine();
for (int round = 1; round <= MAX_Rounds; round++) {
System.out.println(\nRound" + round);
System.out.println("Wait...");
Thread.sleep(rand.nextInt(3000) + 2000);

System.out.println("GO!");

long startTime = System.currentTimeMillis();

input.nextLine();

reactionTime = (int)(System.currentTimeMillis() - startTime);

totalTime += reactionTime;

if (reactionTime < bestTime) {
bestTime = reactionTime;
}

System.out.println("Reaction Time: " + reactionTime + " ms");
}

int average = totalTime / MAX_ROUNDS;

System.out.println("\n===== RESULTS =====");
System.out.println("Average: " + average + " ms");
System.out.println("Best: " + bestTime + " ms");
System.out.println("Machine: 10 ms");

System.out.println("\nHealth Score: " + score);

if (score >= 14) {
System.out.println("Very good!");
} else if (score >= 10) {
System.out.println("It's OK.");
} else {
System.out.println("You need some help.");
}


                     
