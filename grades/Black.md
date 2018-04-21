# Overview
Nothing to do here . Just a reminder you started this. However the clean code page has rather high goals. So I added some basic principles from the original book.

# Principles (by Marcel)

## Use Intention-Revealing Names

Stupid Name:
```java
int d; // elapsed time in days
```

Better Name:
```java
int elapsedTimeInDays;
```

## Explain Yourself in Code
I used a comment:

```java
// Check to see if the employee is eligible for full benefits 
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```

I do not need comments:

```java
if (employee.isEligibleForFullBenefits())
```

I need to write all the Javadoc:

```java
/** * * @param title The title of the CD 
* @param author The author of the CD 
* @param tracks The number of tracks on the CD 
* @param durationInMinutes The duration of the CD in minutes 
*/ 
public void addCD(String title, String author, int tracks, int durationInMinutes) {    
  CD cd = new CD();    
  cd.title = title;    
  cd.author = author;    
  cd.tracks = tracks;    
  cd.duration = duration;    
  cdList.add(cd); 
}
```

# Practices (by Marcel)

## Team Rules
Ground rules are an important tool for helping individuals function together as a team. 
They reflect what is important to the members about how they work together. 
Ideally, the rules are set at the first meeting, allowing them to become second nature to the team. 
Discussing ground rules after problems arise is much more difficult. Ground rules should focus on three elements:

* Tasks – Expected activities and deliverables for the team. 
* Process – How the activities will be carried out. 
* Norms – Ways in which team members will interact with each other.
