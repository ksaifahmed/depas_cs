# Singleton Design Pattern

Singleton Pattern says that just **define a class that has only one instance** and **provide a global point of access to it**.

In other words, a class must ensure that only **single instance should be created** and single object can be used by all other classes.

## _There are two forms of singleton design pattern_
- **Early Instantiation**: creation of instance at load time.
- **Lazy Instantiation**: creation of instance when required.

## _Advantage of Singleton design pattern_
- Saves memory because object is not created at each request. Only single instance is reused again and again.

## _Usage of Singleton design pattern_
- Singleton pattern is mostly used in multi-threaded and database applications. It is used in logging, caching, thread pools, configuration settings etc.

## _UML Example_
![UML Example](https://www.tutorialspoint.com/design_pattern/images/singleton_pattern_uml_diagram.jpg)

## _Code Snippet_

> _Early Instantiation: already thread safe_
```csharp
using System;
public class SingleDatabase{
    private static SingleDatabase dbms = new SingleDatabase();
    
    private SingleDatabase() {
        Console.WriteLine("Pgsql Database Connection created via Early Instantiation");
    }
    
    public static SingleDatabase getInstance() {
        return dbms;
    }
    
    public void getData() {
        Console.WriteLine("Here's your data");
    }
}


public class HelloWorld {
    static void Main() {
        SingleDatabase dbms = SingleDatabase.getInstance();
        dbms.getData();
    }
}
```



> _Lazy Instantiation: use of lock variable to make it thread safe_
```csharp
using System;

public sealed class SingleDatabase {
    private static SingleDatabase dbms = null;
    private static readonly object padlock = new object();

    private SingleDatabase() {
        Console.WriteLine("Pgsql Database Connection created via Lazy Instantiation");
    }

    public static SingleDatabase getInstance (){
        lock (padlock) {
            if (dbms == null) 
                dbms = new SingleDatabase();
            return dbms;
        }
    }
    
    public void getData() {
        Console.WriteLine("Here's your data");
    }
}


public class HelloWorld {
    static void Main() {
        SingleDatabase dbms = SingleDatabase.getInstance();
        dbms.getData();
    }
}
```
