# Principles

## Interface Segregation Principle (ISP)
A client should not be dependent on details of a service he did not need.  
A smaller interface leads to less coupling between client and service and it becomes easier to swap the service or the client.

### Example 1
Suppose you want to purchase a television and you have two to choose from. 
One has many switches and buttons, and most of those seem confusing and doesn't seem necessary to you. 
Another has a few switches and buttons, which seems familiar and logical to you. 
Given that both televisions offer roughly the same functionality, which one would you choose?

### Example 2

<details><summary>Polluted Interface</summary>
<p>

```java
interface IWorker {
    public void work();
    public void eat();
}

class Worker implements IWorker {
    public void work() { // ....working
    }
    public void eat() { // ...... eating in launch break 
    }
}

class SuperWorker implements IWorker {
    public void work() { //.... working much more
    }
    public void eat() { //.... eating in launch break
    }
}

class Robot implements IWorker {
    public void work() { //.... Beep!    
    }

    public void eat() { //I need no food :( 
    }

}

class Manager {
    IWorker worker;
    public void setWorker(IWorker w) {
        worker = w;
    }
    public void manage() { //I don't care if a worker needs food.  
        worker.work();
    }
}
```

</p>
</details>

<details><summary>Better</summary>
<p>

```java
interface IWorker extends IFeedable, IWorkable {}
interface IWorkable {
    public void work();
}
interface IFeedable {
    public void eat();
}

class Worker implements IWorker {
    public void work() { // ....working
    }
    public void eat() { // ...... eating in launch break
    }
}

class SuperWorker implements IWorker {
    public void work() { //.... working much more
    }
    public void eat() { //.... eating in launch break
    }
}

class Robot implements IWorkable {
    public void work() { //.... Beep!
    }
}

class Manager {
    IWorkable worker;
    public void setWorker(IWorkable w) {
        worker = w;
    }
    public void manage() { //I don't care of the rest of the worker as long as they work.
        worker.work();
    }
}
//Example how to combine two interfaces with Generics class
FeedableWorkerManager < WF extends IWorkable & IFeedable > {
    WF worker;public void setWorker(WF w) {
        worker = w;
    }
    public void manage() { //when he can work 
        worker.work(); //I will feed him 
        worker.eat();
        //sorry robots 
    }
}
```

</p>
</details>

## Dependency Inversion
High-level modules should not depend on low-level modules. 
Both should depend on abstractions. 
Abstractions should not depend on details. Details should depend on abstractions.

### Example

<details><summary>How can I test this? And how I change the Connection?</summary>
<p>
```java
public class Userlist {

    JdbcDatabaseConnection db;

    public Userlist() {
        this db = new JdbcDatabaseConnection();
        db.open();
    }
}

public class JdbcDatabaseConnection {

    String dbUrl = "jdbc://";
    public void open() { //opens a JDBC connection to the Database
    }
}
```

</p>
</details>

<details><summary>Better</summary>
<p>
```java
public class Userlist {

    DatabaseConnection db;

    public Userlist(DatabaseConnection db) {
        db.open();
    }
}

public interface DatabaseConnection {
    open();
}

public class JdbcDatabaseConnection implements DatabaseConnection {

    String dbUrl = "jdbc://";
    public void open() { //opens a JDBC connection to the Database 
    }
}
```

</p>
</details>

## Liskov Substitution
A program working with Class T must also work with Class S, when S extends T.

> If it looks like a duck, quack likes a duck, but needs bateries - You have probally the wrong abstraction.

### Example

<details><summary>Confusing</summary>
<p>

```java
class Rectangle {
    protected int m_width;
    protected int m_height;
    public void setWidth(int width) {
        m_width = width;
    }
    public void setHeight(int height) {
        m_height = height;
    }
    public int getWidth() {
        return m_width;
    }
    public int getHeight() {
        return m_height;
    }
    public int getArea() {
        return m_width * m_height;
    }
}
class Square extends Rectangle {
    public void setWidth(int width) {
        m_width = width;
        m_height = width;
    }
    public void setHeight(int height) {
        m_width = height;
        m_height = height;
    }
}
class LspTest {
    private static Rectangle getNewRectangle() { // it can be an object returned by some factory ...
        return new Square();
    }
    public static void main(String args[]) {
        Rectangle r = LspTest.getNewRectangle();
        r.setWidth(5);
        r.setHeight(10); // user only knows that r is a rectangle. 
        // It assumes that he's able to set the width and height as for the base class
        System.out.println(r.getArea());
        // now he's surprised to see that the area is 100 instead of 50. 
    }
}
```

</p>
</details>


<details><summary>Better</summary>
<p>

```java

```

</p>
</details>

## Principle of Least Astonishment
Do what the people expect from you. Surprises will shock them.

### Example 1
The F1 Function key (in Windows operating systems) is almost always for opening a help program associated with a software. 
Users expect a help screen or similar help services popup when they press the F1 key. 
Software binding this key to some other feature is likely to cause astonishment at the lack of help.

### Example 2
The GUI binds the "ESC" key to the "Apply" button.

## Information Hiding Principle
See https://docs.oracle.com/javase/7/docs/api/java/awt/Point.html and find the problem. Today  [project lombok](https://projectlombok.org/) can help with hidding and 
still writing short and readable classes.

```java
// Use me as you wish
public class Point {
    public double x;
    public double y;
}
```

```java
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```

# Practices
## Automatic UnitTests
To ensure everything which you expect yesterday is still working tomorrow.

## Mocking
Makes testing a lot easier and faster when you do not need a database connection to test a service.

## Code Coverage Analyse
Did you test enough? How do you check if you test enough?

## Conferences
Like reviews and pair programming this is important to get new ideas and discuss solutions. 
It helps to discuss certain problems with people suffering from the same problems. 
When talking to people not located in the same company and working on the same problems it is easier to think out of the box and get new fresh ideas.

## Complex Refactorings
More refactorings! Learn the other useful refactorings and how the IDE can assist you using them.
* [Refactoring Catalog](https://refactoring.com/catalog/)
