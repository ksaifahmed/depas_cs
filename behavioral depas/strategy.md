# Strategy Design Pattern

A Strategy Pattern **defines a family of functionality, encapsulates each one, and makes them interchangeable**.

The Strategy Pattern is also known as **Policy**.

## _Advantage of Strategy Pattern_

- It provides a substitute to subclassing.
- It defines each behavior within its own class, eliminating the need for conditional statements.
- It makes it easier to extend and incorporate new behavior without changing the application.


## _Usage of Strategy Pattern_

- When the multiple classes differ only in their behaviors.e.g. Servlet API.
- It is used when you need different variations of an algorithm.

## _UML Example_

![UML Example](https://refactoring.guru/images/patterns/diagrams/strategy/structure-2x.png)

## _Code Snippet_

_The **Strategy** interface with one specific **Algorithm/Operation**_
```csharp
using System;

public interface Strategy
{
    int execute(int a, int b);
}
```

_A **Concrete Strategy** class that Adds_
```csharp
public class ConcreteStrategyAdd : Strategy
{
    public int execute(int a, int b)
    {
        return a + b;
    }
}
```

_A **Concrete Strategy** class that Subtracts_
```csharp
public class ConcreteStrategySubtract : Strategy
{
    public int execute(int a, int b)
    {
        return a - b;
    }
}
```

_A **Concrete Strategy** class that Multiplies_
```csharp
public class ConcreteStrategyMultiply : Strategy
{
    public int execute(int a, int b)
    {
        return a * b;
    }
}
```

_The **Context** class contains one single **Strategy** at a time_
```csharp
public class Context
{
    private Strategy strategy;

    public Context(Strategy strategy)
    {
        this.strategy = strategy;
    }

    public void setStrategy(Strategy strategy)
    {
        this.strategy = strategy;
    }

    public int executeStrategy(int a, int b)
    {
        return strategy.execute(a, b);
    }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWorld
{
    static void Main()
    {
        Context context = new Context(new ConcreteStrategyAdd());
        Console.WriteLine("Result: " + context.executeStrategy(3, 4));

        context.setStrategy(new ConcreteStrategySubtract());
        Console.WriteLine("Result: " + context.executeStrategy(3, 4));

        context.setStrategy(new ConcreteStrategyMultiply());
        Console.WriteLine("Result: " + context.executeStrategy(3, 4));
    }
}
```

## _Differences between State and Strategy_

- The Strategy pattern is really about having a different implementation that accomplishes (basically) the same thing, so that one implementation can replace the other as the strategy requires. For example, you might have different sorting algorithms in a strategy pattern. The callers to the object does not change based on which strategy is being employed, but regardless of strategy the goal is the same (sort the collection).

- The State pattern is about doing different things based on the state, while leaving the caller relieved from the burden of accommodating every possible state. So for example you might have a getStatus() method that will return different statuses based on the state of the object, but the caller of the method doesn't have to be coded differently to account for each potential state.

_More from the following url:_
> https://stackoverflow.com/questions/1658192/what-is-the-difference-between-strategy-design-pattern-and-state-design-pattern