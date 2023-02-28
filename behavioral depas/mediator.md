# Mediator Design Pattern
A Mediator Pattern says that **to define an object that encapsulates how a set of objects interact**.

Consider the following problem. We have a few classes and these classes interact with each other producing results. When number of classes or functionalities increase, the interactions between them also increases and explosion of communication is difficult to maintain.

Mediator pattern is used to reduce communication complexity between multiple objects or classes. This pattern provides a mediator class which normally handles all the communications between different classes and supports easy maintainability of the code by loose coupling.

## _Advantage of Mediator Pattern_

- It decouples the number of classes.
- It simplifies object protocols.
- It centralizes the control.
- The individual components become simpler and much easier to deal with because they don't need to pass messages to one another.
- The components don't need to contain logic to deal with their intercommunication and therefore, they are more generic.


## _Usage of Mediator Pattern_
- It is commonly used in message-based systems likewise chat applications.
- When the set of objects communicate in complex but in well-defined ways.

## _UML Example_

![UML Example](https://www.dofactory.com/img/diagrams/net/mediator.png)

## _Code Snippet_

_The **Mediator** abstract class with a communication method **send()**_
```csharp
using System;

public abstract class Mediator {
    public abstract void Send(string message, Colleague colleague);
}
```

_**Colleagues** are the ones communicating using their member field **Mediator**_
```csharp
public abstract class Colleague {
    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }
}
```

_The **Concrete Mediator** contains all **Colleagues** as member fields to know whose message will be sent to whom aka the **communication logic**_
```csharp
public class ConcreteMediator : Mediator {
    private ConcreteColleague1 colleague1;
    private ConcreteColleague2 colleague2;

    public ConcreteColleague1 Colleague1 {
        set { colleague1 = value; }
    }

    public ConcreteColleague2 Colleague2 {
        set { colleague2 = value; }
    }

    public override void Send(string message, Colleague colleague) {
        if (colleague == colleague1) {
            colleague2.Notify(message);
        } else {
            colleague1.Notify(message);
        }
    }
}
```

_A **Concrete Colleague** implementation_
```csharp
public class ConcreteColleague1 : Colleague {
    public ConcreteColleague1(Mediator mediator) : base(mediator) { }

    public void Send(string message) {
        mediator.Send(message, this);
    }

    public void Notify(string message) {
        Console.WriteLine("Colleague1 gets message: " + message);
    }
}
```

_Another **Concrete Colleague**_
```csharp
public class ConcreteColleague2 : Colleague {
    public ConcreteColleague2(Mediator mediator) : base(mediator) { }

    public void Send(string message) {
        mediator.Send(message, this);
    }

    public void Notify(string message) {
        Console.WriteLine("Colleague2 gets message: " + message);
    }
}
```


_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
    public static void Main() {
        ConcreteMediator m = new ConcreteMediator();

        ConcreteColleague1 c1 = new ConcreteColleague1(m);
        ConcreteColleague2 c2 = new ConcreteColleague2(m);

        m.Colleague1 = c1;
        m.Colleague2 = c2;

        c1.Send("How are you?");
        c2.Send("Fine, thanks");
    }
}
```
