# Observer Design Pattern

An Observer Pattern says that **just define a one-to-one dependency so that when one object changes state, all its dependents are notified and updated automatically**.

The observer pattern is also known as **Dependents** or **Publish-Subscribe**.

## _Advantage of Observer Pattern_

- It describes the coupling between the objects and the observer.
- It provides the support for broadcast-type communication.


## _Usage of Observer Pattern_
- When the change of a state in one object must be reflected in another object without keeping the objects tight coupled.
- When the framework we writes and needs to be enhanced in future with new observers with minimal changes.

## _UML Example_

![UML Example](https://www.dofactory.com/img/diagrams/net/observer.png)

## _Code Snippet_

_The **Subject** contains the list of **Observers/Subscribers**_
```csharp
using System;
using System.Collections.Generic;

public abstract class Subject
{
    private List<Observer> observers = new List<Observer>();

    public void Attach(Observer observer)
    {
        observers.Add(observer);
    }

    public void Detach(Observer observer)
    {
        observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (Observer o in observers)
        {
            o.Update();
        }
    }
}
```

_Concrete Subjects have their own **state** to notify **Observers/Subscribers**_
```csharp
public class ConcreteSubject : Subject
{
    private string subjectState;

    // Gets or sets subject state
    public string SubjectState
    {
        get { return subjectState; }
        set { subjectState = value; }
    }
}
```

_**Observers/Subscribers** base class_
```csharp
public abstract class Observer
{
    public abstract void Update();
}
```

_**Observers/Subscribers** Concrete class whose **state** gets set by the **Subject** they are **subscribed** to_
```csharp
public class ConcreteObserver : Observer
{
    private string name;
    private string observerState;
    private ConcreteSubject subject;

    // Constructor
    public ConcreteObserver(
        ConcreteSubject subject, string name)
    {
        this.subject = subject;
        this.name = name;
    }

    public override void Update()
    {
        observerState = subject.SubjectState;
        Console.WriteLine("Observer {0}'s new state is {1}",
            name, observerState);
    }

    // Gets or sets subject
    public ConcreteSubject Subject
    {
        get { return subject; }
        set { subject = value; }
    }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWord
{
    public static void Main()
    {
        ConcreteSubject s = new ConcreteSubject();

        s.Attach(new ConcreteObserver(s, "X"));
        s.Attach(new ConcreteObserver(s, "Y"));
        s.Attach(new ConcreteObserver(s, "Z"));

        // Change subject and notify observers
        s.SubjectState = "ABC";
        s.Notify();

        // Wait for user
        Console.ReadKey();        
    }
}
```
