//I started by coding in code.org's App Lab, then pasted to GitHub. Then, AI helped me translate to Java. The user inputs factors then plays a reaction game. The program then gives the user a rating.
import java.util.Random;
import java.util.Timer;
import java.util.TimerTask;
import java.util.Scanner;

public class ReactionGame {

    // Game state
    private long startTime = 0;
    private long reactionTime = 0;
    private long bestTime = Long.MAX_VALUE;
    private long totalTime = 0;
    private int round = 0;
    private final int maxRounds = 5;

    private boolean waiting = false;
    private boolean canReact = false;

    private final Random random = new Random();
    private final Timer timer = new Timer();

    public void startGame() {
        round = 0;
        totalTime = 0;
        bestTime = Long.MAX_VALUE;
        nextRound();
    }

    private void nextRound() {
        if (round >= maxRounds) {
            showResults();
            return;
        }

        round++;
        System.out.println("\nRound " + round);
        System.out.println("Wait for GREEN...");

        waiting = true;
        canReact = false;

        int delay = 2000 + random.nextInt(3000); // 2000–5000 ms

        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println("CLICK NOW! (GREEN)");
                startTime = System.currentTimeMillis();
                canReact = true;
                waiting = false;
            }
        }, delay);
    }

    public void react() {
        if (waiting) {
            System.out.println("Too early!");
            return;
        }

        if (canReact) {
            reactionTime = System.currentTimeMillis() - startTime;
            totalTime += reactionTime;

            System.out.println("Reaction: " + reactionTime + " ms");

            if (reactionTime < bestTime) {
                bestTime = reactionTime;
            }

            canReact = false;

            timer.schedule(new TimerTask() {
                @Override
                public void run() {
                    nextRound();
                }
            }, 1000);
        }
    }

    private void showResults() {
        double average = (double) totalTime / maxRounds;

        System.out.println("\nDONE!");
        System.out.println("Avg: " + average + " ms");
        System.out.println("Best: " + bestTime + " ms");
        System.out.println("Machine: 10 ms (placeholder)");
    }

    // Simple test runner
    public static void main(String[] args) {
        ReactionGame game = new ReactionGame();
        Scanner scanner = new Scanner(System.in);

        game.startGame();

        System.out.println("Press ENTER when you see GREEN...");
while (true) {
            scanner.nextLine();
            game.react();
        }
    }
}
