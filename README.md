//I started by coding in code.org's App Lab, then pasted to GitHub. AI assisted me in one line of code. Also somewhat helped with debugging, however i did most of it. My own original code and project driven by my passion for hands-on research. Spent 2 days brainstorming, then 3 hours a week for 1 week making code, then 4 hours a week finding a control group to conduct research. 
 (java)
import.java util.Randaom
import. java util.scanner

public class ReactionGame { 

static scannerInput = new Scanner(System.in)
static Random rand = new Random();
static int sleep;
static int ReactionTime;
static int screenTime;
static int bestTime = Interger.MAX_VALUE;
static int totalTime = 0;

static final int MAX_ROUNDS = 5;

public static void main(String[] args) throws InterruptedException {
System.out.println("This is a reaction Time test."
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


                     
