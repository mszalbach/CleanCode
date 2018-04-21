# Principles
## Single Level of Abstraction (SLA)
All things a method do should have the same level of abstraction.


```java
// not a real single
private bool ValidPolicyNumber(string policyNumber) {
    return policyNumber.startsWith("POLIC") && followedBy7Digits() && policyNumber.Length == 12;
}
```

```java
// Better
private bool ValidPolicyNumber(string policyNumber) {
    return hasExpectedPrefix() && followedBy7Digits() && hasLengthOf12();
}
```

## Single Responsibility Principle (SRP)

A class should only have one task and a function should only do one thing.
A class or module should have one, and only one, reason to change.

<details><summary>I take care of all content types</summary>
<p>

```java
//what happens if we add new content types like html.
//what happens when we want to support other protocols interface
IEmail {
    public void setSender(String sender);
    public void setReceiver(String receiver);
    public void setContent(String content);
}
class Email implements IEmail {
    public void setSender(String sender) {}
    public void setReceiver(String receiver) {}
    public void setContent(String content) {}
}
```
</p>
</details>

<details><summary>Better</summary>
<p>

```java
interface IEmail {
    public void setSender(String sender);
    public void setReceiver(String receiver);
    public void setContent(IContent content);
}
interface IContent {
    public String getAsString(); // used for serialization 
}
class Email implements IEmail {
    public void setSender(String sender) {}
    public void setReceiver(String receiver) {}
    public void setContent(IContent content) {}
}
```
</p>
</details>

## Separation of Concerns (SoC)
When a class is responsible for more then one thing it becomes difficult to understand and to use this class. 
When a class does only one thing the methods in it gets a high cohesion and all classes together gets loose coupled. 
Sometimes Aspect Orientate Programming can help with this to extract things like Logging, 
Caching and Tracing from Business classes. 

<details><summary>I can do anything</summary>
<p>

```java
public class UserSettingsService {
    public void setBackgroundColor(ConsoleColor color) {
        checkAccess();

        Console.setBackgroundColor = color;
        System.out.println("- Color is changed...");
    }

    private static void checkAccess() {
        if (iIsCurrentUserLogedIn()) {
            throw new SecurityException("Can't change color." +
                "The User is not Authenticated in the system");
        }
    }

    private static boolean isCurrentUserLogedIn() {
        return true;
    }
}
```

</p>
</details>

<details><summary>I only do one thing</summary>
<p>

```java
public class UserSettingsService {
    public void setBackgroundColor(ConsoleColor color) {
        SecurityService.checkAccess();

        Console.setBackgroundColor = color;
        System.out.println("- Color is changed...");
    }
}

public class SecurityService {
    public static void checkAccess() {
        if (isCurrentUserLogedIn()) {
            throw new SecurityException("Can't change color." +
                "The User is not Authenticated in the system");
        }
    }

    private static boolean isCurrentUserLogedIn() {
        return true;
    }
}
```

</p>
</details>

## Source Code Convention
Its easier to read if all people working on the same source agreed to conventions how to format and order code.
So there should be a firm intern website which shows the coding conventions for each language commonly used.

## Practices
## Issue Tracking
When its written down it is easier to plan, delegate and to get an overview. 
When new features arrive it is easier to prioritize them against the already existing things. 
So development becomes something planned and not something chaotic. 
The tool is not important the practice is. 

## Automatic Integrationtesting
Integration testing ensures that the code does what it should. To not automate this recurrent activity would be a waste of time.

## Read, Read, Read
* Effective Java
* Java Concurrency in Practice
* Design Patterns: Elements of Reusable Object-Oriented Software 
** go for a HeadFirst book instead or an online explanation
* Refactoring: Improving the Design of Existing Code 
* Clean Code 
* The Mythical Man-Month: Essays on Software Engineering, Anniversary Edition 
* The Pragmatic Programmer: From Journeyman to Master 
* Mastering Regular Expressions, Second Edition
* [Hacker News](https://news.ycombinator.com/)
* Reddit
* Stackoverflow

## Reviews
Two eyes are better than one.
If you explain someone what you have done it becomes more clear if this is correct or if you have overseen something. 
When you do pair programming you can discuss certain ideas and get a better understanding of the problem and hopefully a better solution. 
