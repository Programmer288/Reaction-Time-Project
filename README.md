//I started by coding in code.org's App Lab, then pasted to GitHub. Then, AI helped me translate to Java using JavaFX. The user inputs factors then plays a reaction game. The program then gives the user a rating.


import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;
import javafx.geometry.Pos;
import javafx.scene.paint.Color;
import javafx.animation.PauseTransition;
import javafx.util.Duration;

public class ReactionGameFX extends Application {

    int round = 0;
    int maxRounds = 5;

    long startTime;
    long reactionTime;
    long totalTime = 0;
    long bestTime = Long.MAX_VALUE;

    boolean waiting = false;
    boolean canReact = false;

    int sleep = 0;
    int screenTime = 0;
    int timeScore = 0;
    double score = 0;

    Label status = new Label("Press Start");
    Label results = new Label();

    ComboBox<Integer> sleepBox = new ComboBox<>();
    ComboBox<Integer> screenBox = new ComboBox<>();
    ComboBox<String> timeBox = new ComboBox<>();

    Button startBtn = new Button("Start");
    Button clickBtn = new Button("Click!");

    VBox root = new VBox(10);

    @Override
    public void start(Stage stage) {

        // Dropdown setup
        sleepBox.getItems().addAll(1,2,3,4,5,6,7,8);
        screenBox.getItems().addAll(1,2,3,4,5,6,7,8);

        timeBox.getItems().addAll("Morning", "Afternoon", "Evening");

        root.getChildren().addAll(
            new Label("Sleep Hours"), sleepBox,
            new Label("Screen Time"), screenBox,
            new Label("Time of Day"), timeBox,
            startBtn, clickBtn, status, results
        );

        root.setAlignment(Pos.CENTER);

        clickBtn.setDisable(true);

        startBtn.setOnAction(e -> startGame());
        clickBtn.setOnAction(e -> handleClick());

        stage.setScene(new Scene(root, 400, 400));
        stage.setTitle("Reaction Game");
        stage.show();
    }

    void startGame() {
        // Get inputs
        sleep = sleepBox.getValue();
        screenTime = screenBox.getValue();
        String time = timeBox.getValue();

        if (time.equals("Afternoon")) timeScore = 5;
        else if (time.equals("Evening")) timeScore = 10;
        else timeScore = 1;

        round = 0;
        totalTime = 0;
        bestTime = Long.MAX_VALUE;

        startBtn.setDisable(true);
        clickBtn.setDisable(false);

        nextRound();
    }

    void nextRound() {
        if (round >= maxRounds) {
            showResults();
            return;
        }

        round++;
        status.setText("Wait for green...");
        root.setStyle("-fx-background-color: red;");

        waiting = true;
        canReact = false;

        int delay = 2000 + (int)(Math.random() * 3000);

        PauseTransition pause = new PauseTransition(Duration.millis(delay));
        pause.setOnFinished(e -> {
            root.setStyle("-fx-background-color: green;");
            status.setText("CLICK!");
            startTime = System.currentTimeMillis();
            canReact = true;
            waiting = false;
        });
        pause.play();
    }

    void handleClick() {
        if (waiting) {
            status.setText("Too early!");
            return;
        }

        if (canReact) {
            reactionTime = System.currentTimeMillis() - startTime;
            totalTime += reactionTime;

            if (reactionTime < bestTime) {
                bestTime = reactionTime;
            }

            status.setText("Reaction: " + reactionTime + " ms");
            canReact = false;

            PauseTransition pause = new PauseTransition(Duration.seconds(1));
            pause.setOnFinished(e -> nextRound());
            pause.play();
        }
    }

    void showResults() {
        long avg = totalTime / maxRounds;

        // Score calculation (your formula)
        score = (sleep * 2 + timeScore * 3) + (screenTime * 1.5 + avg * 0.01);

        String message;
        if (score == 14) message = "Very good!";
        else if (score == 10) message = "It's ok.";
        else message = "You need some help.";

        results.setText(
            "Done!\n" +
            "Avg: " + avg + " ms\n" +
            "Best: " + bestTime + " ms\n" +
            "Score: " + score + "\n" +
            message
        );

        status.setText("Finished!");
        root.setStyle("-fx-background-color: white;");
        startBtn.setDisable(false);
    }

    public static void main(String[] args) {
        launch();
    }
}
