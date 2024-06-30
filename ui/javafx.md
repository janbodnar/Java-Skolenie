# JavaFX

JavaFX is a software platform specifically designed for creating and delivering  
rich client applications, also known as desktop applications. It  has the  
capability to build web applications as well.  

## module-info.java

In Java 9 and later versions, `module-info.java` is a special file that acts as  
the *module descriptor* for a Java module. It defines essential information  
about the module, including:  

* *Module name:* This is a unique identifier for your module within the Java  
  ecosystem.  
* *Dependencies:* You can specify other modules that your module relies upon  
  to function correctly.  
* *Exports:*  Declare which packages within your module are visible and  
  accessible to other modules.  
* *Requires:* (Optional) You can indicate specific functionalities or services  
  that your module requires from other modules.  

```java
module QuitButtonEx {
    requires javafx.controls;
    exports com.zetcode;
}
```

The `pom.xml` file should contain:  

```xml
<dependencies>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-controls</artifactId>
        <version>22-ea+11</version>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-maven-plugin</artifactId>
            <version>0.0.8</version>
            <configuration>
                <mainClass>com.zetcode.FirstEx</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
```



## First example

The `module-info.java` file:  

```java
module FirstEx {
    requires javafx.controls;
    exports com.zetcode;
}
```

```java
package com.zetcode;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.StackPane;
import javafx.scene.text.Font;
import javafx.scene.text.FontWeight;
import javafx.stage.Stage;

public class FirstEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new StackPane();

        root.setStyle("-fx-background-color: #606060;");

        var scene = new Scene(root, 500, 450);

        var lbl = new Label("Simple JavaFX application.");
        lbl.setStyle("-fx-text-fill: white;");
        lbl.setFont(Font.font("Arial", FontWeight.NORMAL, 20));
        root.getChildren().add(lbl);

        stage.setTitle("Simple application");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```



## Quit button

```java
package com.zetcode;

import javafx.application.Application;
import javafx.application.Platform;
import javafx.event.ActionEvent;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;

public class QuitButtonEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var btn = new Button();
        btn.setText("Quit");
        btn.setPadding(new Insets(5, 15, 5, 15));
        btn.setOnAction((ActionEvent _) -> {
            Platform.exit();
        });

        var root = new HBox();
        root.setPadding(new Insets(25));
        root.getChildren().add(btn);

        var scene = new Scene(root, 550, 450);

        stage.setTitle("Quit button");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## Styling with CSS

The `style.css` file in `src/main/resources`.  

```css
#root {-fx-background-color: linear-gradient(gray, darkgray); }
#text {-fx-fill:linear-gradient(orange, orangered); }
```

```java
package com.zetcode;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.layout.HBox;
import javafx.scene.text.Font;
import javafx.scene.text.FontWeight;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class StyledEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new HBox();
        root.setPadding(new Insets(20));

        var text = new Text("ZetCode");
        text.setFont(Font.font("Serif", FontWeight.BOLD, 76));

        text.setId("text");
        root.setId("root");

        root.getChildren().addAll(text);

        var scene = new Scene(root);
        scene.getStylesheets().add("style.css");

        stage.setTitle("Styling text");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## CheckBox

`CheckBox` is a tri-state selection control box showing a checkmark or tick mark  
when checked. The control has two states by default: checked and unchecked. The  
`setAllowIndeterminate` enables the third state: indeterminate.  

```java
package com.zetcode;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.CheckBox;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;

public class CheckBoxEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new HBox();
        root.setPadding(new Insets(10, 0, 0, 10));

        var cbox = new CheckBox("Show title");
        cbox.setSelected(true);

        cbox.setOnAction(_ -> {
            if (cbox.isSelected()) stage.setTitle("CheckBox");
            else stage.setTitle("");
        });

        root.getChildren().add(cbox);

        var scene = new Scene(root, 400, 350);

        stage.setTitle("CheckBox");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## Effects

```java
package com.zetcode;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.effect.Light;
import javafx.scene.effect.Lighting;
import javafx.scene.effect.Reflection;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.scene.text.Font;
import javafx.scene.text.FontWeight;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class CombiningEffectsEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new StackPane();

        Light.Distant light = new Light.Distant();
        light.setAzimuth(50);

        var lighting = new Lighting();
        lighting.setLight(light);
        lighting.setSurfaceScale(5);

        var text = new Text();
        text.setText("ZetCode");
        text.setFill(Color.CADETBLUE);
        text.setFont(Font.font(null, FontWeight.BOLD, 60));

        var ref = new Reflection();
        ref.setInput(lighting);
        text.setEffect(ref);

        root.getChildren().add(text);

        var scene = new Scene(root, 300, 250, Color.WHITESMOKE);

        stage.setTitle("Combining effects");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## Animation

`PathTransition` is a class that belongs to the `javafx.animation` package. It  
is specifically designed to animate the movement of a JavaFX node along a  
predefined path over a specified duration.  

```java
package com.zetcode;

import javafx.animation.PathTransition;
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.Pane;
import javafx.scene.paint.Color;
import javafx.scene.shape.Circle;
import javafx.scene.shape.CubicCurveTo;
import javafx.scene.shape.MoveTo;
import javafx.scene.shape.Path;
import javafx.stage.Stage;
import javafx.util.Duration;

public class PathTransitionEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new Pane();

        var path = new Path();
        path.getElements().add(new MoveTo(20, 120));
        path.getElements().add(new CubicCurveTo(180, 60, 250, 340, 420, 240));

        var circle = new Circle(20, 120, 10);
        circle.setFill(Color.CADETBLUE);

        var ptr = new PathTransition();

        ptr.setDuration(Duration.seconds(6));
        ptr.setDelay(Duration.seconds(2));
        ptr.setPath(path);
        ptr.setNode(circle);
        ptr.setCycleCount(2);
        ptr.setAutoReverse(true);
        ptr.play();

        root.getChildren().addAll(path, circle);

        var scene = new Scene(root, 450, 300);

        stage.setTitle("PathTransition");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## Canvas

`Canvas` provides a dedicated area for drawing custom graphics within your  
application. It acts like a virtual canvas where you can use various drawing  
methods to render shapes, images, and text.  

```java
package com.zetcode;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.canvas.Canvas;
import javafx.scene.canvas.GraphicsContext;
import javafx.scene.layout.Pane;
import javafx.scene.paint.Color;
import javafx.scene.shape.ArcType;
import javafx.stage.Stage;

public class ShapesEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new Pane();

        var canvas = new Canvas(320, 300);
        var gc = canvas.getGraphicsContext2D();
        drawShapes(gc);

        root.getChildren().add(canvas);

        var scene = new Scene(root, 300, 200, Color.WHITESMOKE);

        stage.setTitle("Shapes");
        stage.setScene(scene);
        stage.show();
    }

    private void drawShapes(GraphicsContext gc) {

        gc.setFill(Color.GRAY);

        gc.fillOval(30, 30, 50, 50);
        gc.fillOval(110, 30, 80, 50);
        gc.fillRect(220, 30, 50, 50);
        gc.fillRoundRect(30, 120, 50, 50, 20, 20);
        gc.fillArc(110, 120, 60, 60, 45, 180, ArcType.OPEN);
        gc.fillPolygon(new double[]{220, 270, 220},
                new double[]{120, 170, 170}, 3);
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

## Charts

```java
package com.zetcode;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.chart.LineChart;
import javafx.scene.chart.NumberAxis;
import javafx.scene.chart.XYChart;
import javafx.scene.layout.HBox;
import javafx.stage.Stage;


public class LineChartEx extends Application {

    @Override
    public void start(Stage stage) {

        initUI(stage);
    }

    private void initUI(Stage stage) {

        var root = new HBox();

        var scene = new Scene(root, 450, 330);

        var xAxis = new NumberAxis();
        xAxis.setLabel("Age");

        var yAxis = new NumberAxis();
        yAxis.setLabel("Salary (€)");

        var lineChart = new LineChart<>(xAxis, yAxis);
        lineChart.setTitle("Average salary per age");

        var data = new XYChart.Series<Number, Number>();
        data.setName("2016");

        data.getData().add(new XYChart.Data<>(18, 567));
        data.getData().add(new XYChart.Data<>(20, 612));
        data.getData().add(new XYChart.Data<>(25, 800));
        data.getData().add(new XYChart.Data<>(30, 980));
        data.getData().add(new XYChart.Data<>(40, 1410));
        data.getData().add(new XYChart.Data<>(50, 2350));

        lineChart.getData().add(data);

        root.getChildren().add(lineChart);

        stage.setTitle("LineChart");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
