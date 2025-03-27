# Assignment
Distributed system

Repositories (`csc-435-ea-abhipatil99`, `csc-435-pa5-abhipatil99`, `csc-435-pa4-abhipatil99`, `csc-435-pa3-abhipatil99`, `csc-435-pa2-abhipatil99`, `csc-435-pa1-abhipatil99`) are likely Java-based assignments, I’ll provide a tailored **design pattern** and **repository structure** for each one. Without knowing the exact requirements of each assignment, I’ll make educated assumptions based on typical computer science coursework (e.g., data structures, algorithms, or software design). I’ll assign a plausible pattern to each, explain why it fits, and provide a basic Java implementation outline along with a GitHub repository structure.

---

### General Repository Setup
For each assignment, use this consistent structure under your personal GitHub account (`https://github.com/abhipatil99/`):
```
csc-435-paX/                  # Replace X with pa1, pa2, etc.
├── src/                     # Source code
│   ├── main/java/org/abhipatil99/  # Package structure
│   └── test/java/org/abhipatil99/  # Unit tests
├── docs/                    # Documentation (e.g., assignment specs)
├── .gitignore               # Ignore .class files, IDE files, etc.
├── README.md                # Instructions and overview
└── pom.xml                  # Maven build file (if using Maven)
```
- **`.gitignore` Example:**
  ```
  *.class
  target/
  .idea/
  *.iml
  ```
- **README.md Template:**
  ```
  # CSC-435 Programming Assignment X
  ## Description
  [Briefly describe the assignment's purpose]

  ## How to Run
  1. Clone the repo: `git clone https://github.com/abhipatil99/csc-435-paX.git`
  2. Compile: `javac src/main/java/org/abhipatil99/*.java`
  3. Run: `java -cp src/main/java org.abhipatil99.Main`

  ## Technologies
  - Java [version, e.g., 17]
  ```

Now, let’s assign a design pattern to each assignment and outline how to build it.

---

### 1. `csc-435-pa1-abhipatil99` - Singleton Pattern
- **Assumption:** A simple program, possibly managing a single resource (e.g., a logger, configuration, or counter).
- **Why Singleton?** Ensures only one instance exists, useful for shared resources in early assignments.
- **Java Implementation:**
  ```java
 // src/main/java/org/abhipatil99/Singleton.java
package org.abhipatil99;

public class Singleton {
    private static Singleton instance;
    private int counter; // Example state

    private Singleton() {
        // TO-DO: Initialize any necessary state or resources here
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void incrementCounter() {
        // TO-DO: Implement logic to modify or manage the resource (e.g., increment a counter)
    }
}

// src/main/java/org/abhipatil99/Main.java
package org.abhipatil99;

public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        // TO-DO: Add code to test or utilize the Singleton instance
    }
}
  ```
- **Why It Fits:** Teaches object-oriented basics and resource management.

-----------------------------------------------------------------------------------------------------------

### 2. `csc-435-pa2-abhipatil99` - Factory Pattern
- **Assumption:** Create different types of objects (e.g., shapes, algorithms, or data structures).
- **Why Factory?** Encapsulates object creation, making it flexible and extensible.
- **Java Implementation:**
  ```java
  // src/main/java/org/abhipatil99/Shape.java
  package org.abhipatil99;

  public interface Shape {
      void draw();
  }

  // src/main/java/org/abhipatil99/Circle.java
  package org.abhipatil99;

  public class Circle implements Shape {
      @Override
      public void draw() {
          System.out.println("Drawing a Circle");
      }
  }

  // src/main/java/org/abhipatil99/Square.java
  package org.abhipatil99;

  public class Square implements Shape {
      @Override
      public void draw() {
          System.out.println("Drawing a Square");
      }
  }

  // src/main/java/org/abhipatil99/ShapeFactory.java
  package org.abhipatil99;

  public class ShapeFactory {
      public Shape createShape(String type) {
          if ("circle".equalsIgnoreCase(type)) return new Circle();
          if ("square".equalsIgnoreCase(type)) return new Square();
          return null;
      }
  }

  // src/main/java/org/abhipatil99/Main.java
  package org.abhipatil99;

  public class Main {
      public static void main(String[] args) {
          ShapeFactory factory = new ShapeFactory();
          Shape circle = factory.createShape("circle");
          circle.draw(); // Drawing a Circle
          Shape square = factory.createShape("square");
          square.draw(); // Drawing a Square
      }
  }
  ```
- **Why It Fits:** Common in assignments requiring polymorphism.

---

### 3. `csc-435-pa3-abhipatil99` - Strategy Pattern
- **Assumption:** Implement interchangeable algorithms (e.g., sorting, searching).
- **Why Strategy?** Allows runtime algorithm selection, promoting flexibility.
- **Java Implementation:**
  ```java
  // src/main/java/org/abhipatil99/SortStrategy.java
  package org.abhipatil99;

  public interface SortStrategy {
      void sort(int[] array);
  }

  // src/main/java/org/abhipatil99/BubbleSort.java
  package org.abhipatil99;

  public class BubbleSort implements SortStrategy {
      @Override
      public void sort(int[] array) {
          for (int i = 0; i < array.length - 1; i++) {
              for (int j = 0; j < array.length - i - 1; j++) {
                  if (array[j] > array[j + 1]) {
                      int temp = array[j];
                      array[j] = array[j + 1];
                      array[j + 1] = temp;
                  }
              }
          }
      }
  }

  // src/main/java/org/abhipatil99/QuickSort.java
  package org.abhipatil99;

  public class QuickSort implements SortStrategy {
      @Override
      public void sort(int[] array) {
          // Simplified placeholder (implement actual quicksort logic)
          System.out.println("QuickSort placeholder");
      }
  }

  // src/main/java/org/abhipatil99/Sorter.java
  package org.abhipatil99;

  public class Sorter {
      private SortStrategy strategy;

      public void setStrategy(SortStrategy strategy) {
          this.strategy = strategy;
      }

      public void performSort(int[] array) {
          strategy.sort(array);
      }
  }

  // src/main/java/org/abhipatil99/Main.java
  package org.abhipatil99;

  public class Main {
      public static void main(String[] args) {
          int[] array = {5, 2, 9, 1, 5};
          Sorter sorter = new Sorter();

          sorter.setStrategy(new BubbleSort());
          sorter.performSort(array);
          System.out.println("Bubble Sorted: " + java.util.Arrays.toString(array));

          sorter.setStrategy(new QuickSort());
          sorter.performSort(array);
          System.out.println("Quick Sorted: " + java.util.Arrays.toString(array));
      }
  }
  ```
- **Why It Fits:** Perfect for algorithm-focused assignments.

---

### 4. `csc-435-pa4-abhipatil99` - Observer Pattern
- **Assumption:** Event-driven system (e.g., a subject notifying observers of state changes).
- **Why Observer?** Models relationships where objects need to react to changes.
- **Java Implementation:**
  ```java
  // src/main/java/org/abhipatil99/Observer.java
  package org.abhipatil99;

  public interface Observer {
      void update(String message);
  }

  // src/main/java/org/abhipatil99/Subject.java
  package org.abhipatil99;

  import java.util.ArrayList;
  import java.util.List;

  public class Subject {
      private List<Observer> observers = new ArrayList<>();
      private String state;

      public void addObserver(Observer observer) {
          observers.add(observer);
      }

      public void setState(String state) {
          this.state = state;
          notifyObservers();
      }

      private void notifyObservers() {
          for (Observer observer : observers) {
              observer.update(state);
          }
      }
  }

  // src/main/java/org/abhipatil99/ConcreteObserver.java
  package org.abhipatil99;

  public class ConcreteObserver implements Observer {
      private String name;

      public ConcreteObserver(String name) {
          this.name = name;
      }

      @Override
      public void update(String message) {
          System.out.println(name + " received update: " + message);
      }
  }

  // src/main/java/org/abhipatil99/Main.java
  package org.abhipatil99;

  public class Main {
      public static void main(String[] args) {
          Subject subject = new Subject();
          subject.addObserver(new ConcreteObserver("Observer1"));
          subject.addObserver(new ConcreteObserver("Observer2"));
          subject.setState("State Changed!"); // Both observers notified
      }
  }
  ```
- **Why It Fits:** Useful for UI or simulation assignments.

---

### 5. `csc-435-pa5-abhipatil99` - Decorator Pattern
- **Assumption:** Extend functionality dynamically (e.g., adding features to a base object).
- **Why Decorator?** Adds behavior without modifying existing code.
- **Java Implementation:**
  ```java
  // src/main/java/org/abhipatil99/Component.java
  package org.abhipatil99;

  public interface Component {
      String operation();
  }

  // src/main/java/org/abhipatil99/ConcreteComponent.java
  package org.abhipatil99;

  public class ConcreteComponent implements Component {
      @Override
      public String operation() {
          return "Base Component";
      }
  }

  // src/main/java/org/abhipatil99/Decorator.java
  package org.abhipatil99;

  public abstract class Decorator implements Component {
      protected Component component;

      public Decorator(Component component) {
          this.component = component;
      }

      @Override
      public String operation() {
          return component.operation();
      }
  }

  // src/main/java/org/abhipatil99/ExtraFeature.java
  package org.abhipatil99;

  public class ExtraFeature extends Decorator {
      public ExtraFeature(Component component) {
          super(component);
      }

      @Override
      public String operation() {
          return component.operation() + " with Extra Feature";
      }
  }

  // src/main/java/org/abhipatil99/Main.java
  package org.abhipatil99;

  public class Main {
      public static void main(String[] args) {
          Component base = new ConcreteComponent();
          Component decorated = new ExtraFeature(base);
          System.out.println(decorated.operation()); // Base Component with Extra Feature
      }
  }
  ```
- **Why It Fits:** Great for assignments requiring feature extension.

---

### 6. `csc-435-ea-abhipatil99` - MVC (Model-View-Controller) Pattern
- **Assumption:** Extra assignment (EA) might be a capstone with a UI or complex logic (e.g., a small application).
- **Why MVC?** Separates data, presentation, and logic for clarity.
- **Java Implementation:**
  ```java
  // src/main/java/org/abhipatil99/Model.java
  package org.abhipatil99;

  public class Model {
      private String data;

      public void setData(String data) {
          this.data = data;
      }

      public String getData() {
          return data;
      }
  }

  // src/main/java/org/abhipatil99/View.java
  package org.abhipatil99;

  public class View {
      public void display(String data) {
          System.out.println("View: " + data);
      }
  }

  // src/main/java/org/abhipatil99/Controller.java
  package org.abhipatil99;

  public class Controller {
      private Model model;
      private View view;

      public Controller(Model model, View view) {
          this.model = model;
          this.view = view;
      }

      public void updateData(String data) {
          model.setData(data);
          view.display(model.getData());
      }
  }

  // src/main/java/org/abhipatil99/Main.java
  package org.abhipatil99;

  public class Main {
      public static void main(String[] args) {
          Model model = new Model();
          View view = new View();
          Controller controller = new Controller(model, view);
          controller.updateData("Hello, MVC!"); // View: Hello, MVC!
      }
  }
  ```
- **Why It Fits:** Ideal for a culminating project with multiple components.

---

### Building and Uploading to GitHub
1. **Local Setup:**
   - Create each folder structure locally (e.g., `csc-435-pa1`).
   - Add the Java files as shown above.
   - Initialize Git:
     ```bash
     git init
     git add .
     git commit -m "Initial commit for CSC-435 PA1 with Singleton pattern"
     ```

2. **Push to GitHub:**
   - Create the repository on GitHub (`abhipatil99/csc-435-pa1`).
   - Link and push:
     ```bash
     git remote add origin https://github.com/abhipatil99/csc-435-pa1.git
     git push -u origin main
     ```
   - Repeat for `pa2`, `pa3`, etc.

3. **Verify:** Check each repo online to ensure code and README are correct.

---

### Tailoring to Your Assignments
If you can share specific details about what each assignment does (e.g., "PA1 is a calculator," "PA3 is a sorting program"), I can refine these patterns further. Otherwise, these are solid starting points for typical Java assignments. Let me know if you need help implementing or adjusting any of these!
