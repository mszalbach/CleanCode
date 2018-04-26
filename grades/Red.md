# Overview
The first part of being a clean code developer. 
The red phase describes the first modules which should be included in the daily work. 
The modules are simple and should not require any change to the project structure 
and so you can start with them without anybody noticing you doing it.

# Principles

## Don´t Repeat Yourself (DRY)

### Example 1
<details><summary>Spot the duplicate</summary>
<p>

```java
public class Customer {
    private Address address;
    private Date date;

    public Customer(Address address, Date date) {
        this.address = address;
        this.date = date;
    }

    public Customer(Address address) {
        this.address = address;
        this.date = new Date();
    }
}
```

</p>
</details>
<details><summary>Better</summary>
<p>
    
```java
public class Customer {
    private Address address;
    private Date date;

    public Customer(Address address, Date date) {
        this.address = address;
        this.date = date;
    }

    public Customer(Address address) {
        this(address, new Date());
    }
}
```

</p>
</details>


### Example 2

<details><summary>lot of exception handling code</summary>
<p>

```java
public class FileProcessor {
    public void processXMLFile(File file) {
        InputStream fis = null;
        try {
            fis = new FileInputStream(file);
            processXML(fis);
        } catch (Exception ex) { //take care of me 
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) { //take care of me again  
                }
            }
        }
    }

    public void processJSONFile(File file) {
        InputStream fis = null;
        try {
            fis = new FileInputStream(file);
            processJSON(fis);
        } catch (Exception ex) { //take care of me 
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) { //take care of me again 
                }
            }
        }
    }
}
```
</p>
</details>

<details><summary>Better</summary>
<p>

```java
public interface FileProcessorStrategy {
    void process(InputStream is);
}

public class JSONFileProcessor implements FileProcessorStrategy {
    @Override public void process(InputStream is) {
        processJSON(is);
    }

}

public class XMLFileProcessor implements FileProcessorStrategy {
    @Override public void process(InputStream is) {
        processXML(is);
    }

}


public class FileProcessor {

    public void processFile(File file, FilePrcessorStrategy processor) {
        InputStream fis = null;
        try {
            fis = new FileInputStream(file);
            procrssor.process(fis);
        } catch (Exception ex) { //AH!        
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) { //to many of them. 
                }
            }
        }
    }
}
```

</p>
</details>

## Keep it simple, stupid (KISS)
1+1 = [(27/3)/3]-1

## Beware of Optimizations!

* Rule 1: Don't do it. 
* Rule 2 (for experts only): Don't do it yet.

### Example 

```java
System.out.println( 2 * 2 ); 
//vs 
System.out.println( 2 << 1 );
```

## Favour Composition over Inheritance (FCoI)

<details><summary>Will not work</summary>
<p>

```java
//what happens if HashSet gets a new Method? 
public class InstrumentedHashSet extends HashSet {

    private int addCount = 0;
    public boolean add(Object o) {
        addCount++;
        return super.add(o);
    }

    //using this method with three elements will set addCount to 6!!
    public boolean addAll(Collection c) {
        addCount += c.size();
        return super.addAll(c); //uses HashSet add method   
    }


    public int getAddCount() {
        return addCount;
    }
}
```

</p>
</details>

<details><summary>Using composition</summary>
<p>

```java
//what happens if HasSet gets a Method? 
public class InstrumentedHashSet {

    private int addCount = 0;
    private Set hashSet = new HashSet();
    public boolean add(Object o) {
        addCount++;
        return hashSet.add(o);
    }

    public boolean addAll(Collection c) {
        boolean hasChanged = false;
        for (Object o: c) {
            hasChanged |= add(c);
        }
        return hasChanged;
    }


    public int getAddCount() {
        return addCount;
    }
}
```

</p>
</details>

## Integration Operation Segregation Principle (IOSP)
Methods are separated in two groups:
* A Method only contains logic like control structures, I/O or API calls -> this is named Operation
* A Method only contains of calls to other methods of the same codebase -> this is named Integration

This helps to comply with Single Responsibility Principle. The code will be build like a tree. Operations can only be found at
the leafs, which will do any calculation. 

# Practices

## Boy Scouts Rule
Leave the campground cleaner than you found it.

## Root Cause Analysis
Why? Why? Why?
Only fixing the symptoms will cause a lot more future bugs.

## Use a Version Control System
It works yesterday!
I need this commented code for later!

## Apply Simple Refactoring Patterns
Practising the Boy Scouts Rule. Learn the features of your IDE.
Simple patterns to learn are:
* [rename method](https://refactoring.com/catalog/renameMethod.html)
* [extract method](https://refactoring.com/catalog/extractMethod.html)

## Reflect Daily
You get better when you reflect your achievements and errors. But only when you practice it daily it can be used under heavy pressure.
