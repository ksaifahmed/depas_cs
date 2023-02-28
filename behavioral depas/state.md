# State Design Pattern
A State Pattern says that **the class behavior changes based on its state**. 

In State Pattern, we create objects which represent various states and a context object whose behavior varies as its state object changes.

The State Pattern is also known as **Objects for States**.

## _Advantage of State Pattern_
- It keeps the state-specific behavior.
- It makes any state transitions explicit.


## _Usage of State Pattern_
- When the behavior of object depends on its state and it must be able to change its behavior at runtime according to the new state.
- It is used when the operations have large, multipart conditional statements that depend on the state of an object.

## _UML Example_

![UML Example](https://1.bp.blogspot.com/-psGfYQ-eDzc/Xy4GsW1DqTI/AAAAAAAAAi4/o6yv3wYnF-EVkMixEcV4fYhcL8meqh30wCNcBGAsYHQ/s0/State_Pattern.jpg)

## _Code Snippet_

_The **State** interface that has one **change state** method_
```csharp
using System;

public interface State {
    void toggle(Switch sw);
}
```

_A Concrete state **OnState** that implements **State** and changes to **OffState**_
```csharp
public class OnState : State {
    public void toggle(Switch sw) {
        Console.WriteLine("turning off...");
        sw.setState(new OffState());
    }
}
```

_A Concrete state **OffState** that implements **State** and changes to **OnState**_
```csharp
public class OffState : State {
    public void toggle(Switch sw) {
        Console.WriteLine("turning on...");
        sw.setState(new OnState());
    }
}
```

_A Concrete Class **Switch** that is in one single **State** at a time_
```csharp
public class Switch {
    private State state;
    public Switch() {
        state = new OffState();
    }
    public void setState(State state) {
        this.state = state;
    }
    public void toggle() {
        state.toggle(this);
    }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
    static void Main() {
        Switch sw = new Switch(); // initially off
        sw.toggle(); // switch on
        sw.toggle(); // switch off
        sw.toggle(); // switch on
  }
}
```
