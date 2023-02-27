# Facade Design Pattern
A Facade Pattern says that just **just provide a unified and simplified interface to a set of interfaces in a subsystem, therefore it hides the complexities of the subsystem from the client**.

In other words, Facade Pattern describes a higher-level interface that makes the sub-system easier to use.

Practically, every **Abstract Factory** is a type of **Facade**.

## _Advantage of Facade Pattern_
- It shields the clients from the complexities of the sub-system components.
- It promotes loose coupling between subsystems and its clients.


## _Usage of Facade Pattern_
- When you want to provide simple interface to a complex sub-system.
- When several dependencies exist between clients and the implementation classes of an abstraction.

## _UML Example_
![UML Example](https://refactoring.guru/images/patterns/diagrams/facade/structure-2x.png)

## _Code Snippet_

_The **Subsystem1** class provides some useful functionality_
```csharp
using System;

class Subsystem1
{
    public void Operation1()
    {
        Console.WriteLine("Subsystem1: Operation1");
    }
}
```

_The **Subsystem1** class provides some useful functionality_
```csharp
class Subsystem2
{
    public void Operation2()
    {
        Console.WriteLine("Subsystem2: Operation2");
    }
}
```

_The **Facade** class provides a simple interface to the complex subsystem_
```csharp
class Facade
{
    private Subsystem1 subsystem1;
    private Subsystem2 subsystem2;

    public Facade()
    {
        subsystem1 = new Subsystem1();
        subsystem2 = new Subsystem2();
    }

    public void Operation()
    {
        Console.WriteLine("Facade performs operation:");
        subsystem1.Operation1();
        subsystem2.Operation2();
    }
}
```


_The Driver Code AKA **Client**_
```csharp
class HelloWorld {
    static void Main(string[] args)
    {
        Facade facade = new Facade();
        facade.Operation();
    }
}
```