import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class WorkoutApp extends Application {

    private int currentExerciseIndex = 0;
    private String[] exercises = {"Push-ups", "Squats", "Lunges", "Plank"};
    private String[] imagePaths = {
        "images/pushups.jpg",
        "images/squats.jpg",
        "images/lunges.jpg",
        "images/plank.jpg"
    };

    private Label exerciseLabel;
    private ImageView exerciseImage;

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Workout Application");

        exerciseLabel = new Label();
        exerciseImage = new ImageView();
        exerciseImage.setFitWidth(300);
        exerciseImage.setFitHeight(300);

        Button nextButton = new Button("Next Exercise");
        nextButton.setOnAction(e -> showNextExercise());

        VBox layout = new VBox(10);
        layout.setPadding(new Insets(20));
        layout.getChildren().addAll(exerciseLabel, exerciseImage, nextButton);

        Scene scene = new Scene(layout, 350, 450);
        primaryStage.setScene(scene);

        showExercise(currentExerciseIndex);

        primaryStage.show();
    }

    private void showExercise(int index) {
        exerciseLabel.setText(exercises[index]);
        Image image = new Image(getClass().getResourceAsStream(imagePaths[index]));
        exerciseImage.setImage(image);
    }

    private void showNextExercise() {
        currentExerciseIndex = (currentExerciseIndex + 1) % exercises.length;
        showExercise(currentExerciseIndex);
    }

    public static void main(String[] args) {
        launch(args);
    }
}
