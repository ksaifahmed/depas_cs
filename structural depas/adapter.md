# Adapter Design Pattern

An Adapter Pattern says that just **converts the interface of a class into another interface that a client wants**.
In other words, to provide the interface according to client requirement while using the services of a class with a different interface.
The Adapter Pattern is also known as **Wrapper**.

## _Advantage of Adapter Pattern_

- It allows two or more previously incompatible objects to interact.
- It allows reusability of existing functionality.
- Usage of Adapter pattern:

## _Usage of Prototype Pattern:_

- When an object needs to utilize an existing class with an incompatible interface.
- When you want to create a reusable class that cooperates with classes which don't have compatible interfaces.
- When you want to create a reusable class that cooperates with classes which don't have compatible interfaces.

## _UML Example_
![UML Example](https://refactoring.guru/images/patterns/diagrams/adapter/example.png)

## _Code Snippet_

_The Existing class **RoundHole** in which a **RoundPeg** fits_
```csharp
using System;

class RoundHole {
    private double radius;

    public RoundHole(double radius) {
        this.radius = radius;
    }

    public double GetRadius() {
        return radius;
    }

    public bool Fits(RoundPeg peg) {
        return this.GetRadius() >= peg.GetRadius();
    }
}
```

_The Existing/Legacy class **RoundPeg**. Only a **RoundPeg** fits inside the **RoundHole**_
```csharp
class RoundPeg {
    private double radius;

    public RoundPeg(double radius) {
        this.radius = radius;
    }

    public virtual double GetRadius() {
        return radius;
    }
}
```

_The New class **SquarePeg**. **SquarePeg**s cannot fit inside the **RoundHole**_
```csharp
class SquarePeg {
    private double width;

    public SquarePeg(double width) {
        this.width = width;
    }

    public double GetWidth() {
        return width;
    }
}
```

_So we use a **Wrapper/Adapter** class called **SquarePegAdapter** that **extends original class** and **contains an object of new class** as a field_
```csharp
class SquarePegAdapter : RoundPeg {
    private SquarePeg peg;

    public SquarePegAdapter(SquarePeg peg) : base(0) {
        this.peg = peg;
    }

    public override double GetRadius() {
        // The adapter pretends that it's a round peg with a
        // radius that could fit the square peg that the adapter
        // actually wraps.
        return peg.GetWidth() * Math.Sqrt(2) / 2;
    }
}
```


_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
  static void Main() {
    RoundHole hole = new RoundHole(5);
    RoundPeg rpeg = new RoundPeg(5);
    Console.WriteLine(hole.Fits(rpeg)); // true

    SquarePeg smallSqpeg = new SquarePeg(5);
    SquarePeg largeSqpeg = new SquarePeg(10);
    //hole.Fits(smallSqpeg); // this won't compile (incompatible types)

    SquarePegAdapter smallSqpegAdapter = new SquarePegAdapter(smallSqpeg);
    SquarePegAdapter largeSqpegAdapter = new SquarePegAdapter(largeSqpeg);
    Console.WriteLine(hole.Fits(smallSqpegAdapter)); // true
    Console.WriteLine(hole.Fits(largeSqpegAdapter)); // false
  }
}
```