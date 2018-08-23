# Principles
## Open Closed Principle
  * :white_check_mark: Open for extension
  * :x: Closed for modification

### Example

<details><summary>Lots of Modifications</summary>
<p>

```java
public class Rectangle {
    public double getWidth();
    public double getHeight();
}

public class Circle {
    public double getRadius();
}


public class AreaCalculator {
    public double Area(Object[] shapes) {
        double area = 0;
        foreach(Object shape: shapes) {
            if (shape is Rectangle) {
                Rectangle rectangle = (Rectangle) shape;
                area += rectangle.getWidth() * rectangle.getHeight();
            } else {
                Circle circle = (Circle) shape;
                area += circle.getRadius() * circle.getRadius() * Math.PI;
            } //here you can add new calculations :) 
        }
        return area;
    }
}
```

</p>
</details>

<details><summary>Better</summary>
<p>

```java
public interface Shape {
    public double getArea();
}


public class Rectangle implements Shape {
    private double width;
    private doulbe height;

    public double getArea() {
        return width * height;
    }
}

public class Circle implements Shape {
    private double radius;
    public double getArea() {
        return radius * radius * Math.PI;
    }
}

//if you need a new shape you can create a new one by extending. you do not need to change anything existing. Horray.
public class AreaCalculator {
    public double Area(Shape[] shapes) {
        double area = 0;
        foreach(Shape shape: shapes) {
            area += shape.getArea();
        }
        return area;
    }
}
```

</p>
</details>

## Tell, don't ask
Helps people remembering that object-orientation is about bundling data with the functions that operate on that data. 
In an extreme way try to program without getter methods.

```java
//ask
Widget w = ...;
if (w.getParent() != null) {
    Panel parent = w.getParent();
    parent.remove(w);
}
```

```java
//tell
Widget w = ...;
w.removeFromParent();
```

## Law of Demeter
Objects only talk to there immediate friends. 
This law did not apply to data structures, because they naturally expose their internal structure.

1. O itself 
2. M's parameters 
3. Any objects created/instantiated within M 
4. O's direct component objects 
5. A global variable, accessible by O, in the scope of M

> The Law of Demeter is not a law, and it's not as simple as counting the number of dots in your statements.
> It's really about developing a sense for constructing your code so that each object is confident in what it is telling other objects to do, 
> and what it is responsible for understanding

### Example
## collapsible markdown?

<details><summary>Please kill me</summary>
<p>

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
String outFile = outputDir + "/" + className.replace('.', '/') + ".class";
FileOutputStream fout = new FileOutputStream(outFile);
BufferedOutputStream bos = new BufferedOutputStream(fout);
```

</p>
</details>

<details><summary>"Tell, Don't Ask</summary>
<p>

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

</p>
</details>

# Practices
## Continuous Integration
Will compile and test the software which each change.
Removes error-prone manual building. 
Solves the problem that a software only rune on one machine and that developer are scared to checkout changes.
 * [Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html)
 
# Static Codeanalyse
Tests ensure the software does what the customer expects. 
Codeanalyse tries to meassure the quality of the code by applying static checks and converting it to metrics. 
Also they can check if the team rules are applied like "comment all public methods".

# Inversion of Control Container
A Tool to achieve Dependecy Inversion. In the yellow grade this was done manually by the developer. With an IoC Container this can be Dependency Inversion done by the software and the developer only needs to define the relationships.

# Share Knowledge
Learning and teaching establish a stable knowledge. 
When you teach someone you will automatically reflect everything which will lead to a better understanding.

# Measure Errors
Only if you know how many errors happen you can try to reduce them. 
If you measure them it is also easier to find common error spots which maybe need some redesign. 


