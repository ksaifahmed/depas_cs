# Composite Design Pattern
A Composite Pattern says that just **allow clients to operate in generic manner on objects that may or may not represent a hierarchy of objects**.

## _Advantage of Composite Design Pattern_
- It defines class hierarchies that contain primitive and complex objects.
- It makes easier to you to add new kinds of components.
- It provides flexibility of structure with manageable class or interface.

## _Usage of Composite Pattern_
- When you want to represent a full or partial hierarchy of objects.
- When the responsibilities are needed to be added dynamically to the individual objects without affecting other objects.
- Where the responsibility of object may vary from time to time.


## _UML Example_
![UML Example](https://refactoring.guru/images/patterns/diagrams/composite/example-2x.png)


## _Code Snippet_

_The base interface **IGraphic**_
```csharp
using System;
using System.Collections.Generic;

public interface IGraphic
{
    void Move(int x, int y);
    void Draw();
}
```

_The concrete class **Dot** to use as composites_
```csharp
public class Dot : IGraphic
{
    protected int x, y;

    public Dot(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    public void Move(int x, int y)
    {
        this.x += x;
        this.y += y;
    }

    public virtual void Draw()
    {
        Console.WriteLine("Drawing a Dot at {0}, {1}", x, y);
    }
}
```

_Another concrete class **Circle** that inherits **Dot** to use as composites_
```csharp
public class Circle : Dot
{
    private int radius;

    public Circle(int x, int y, int radius) : base(x, y)
    {
        this.radius = radius;
    }

    public override void Draw()
    {
        Console.WriteLine("Drawing a Circle with radius {0}, at ({1},{2})", radius, base.x, base.y);
    }
}
```

_The composite class **CompoundGraphic**_
```csharp
public class CompoundGraphic : IGraphic
{
    private List<IGraphic> children = new List<IGraphic>();

    public void Add(IGraphic child)
    {
        children.Add(child);
    }

    public void Remove(IGraphic child)
    {
        children.Remove(child);
    }

    public void Move(int x, int y)
    {
        foreach (IGraphic child in children)
        {
            child.Move(x, y);
        }
    }

    public void Draw()
    {
        foreach (IGraphic child in children)
        {
            child.Draw();
        }
    }
}
```

_The Driver Code AKA **Client** (ImageEditor)_
```csharp
public class HelloWorld {
    static void Main(string[] args)
    {
        CompoundGraphic innerRing = new CompoundGraphic();
        innerRing.Add(new Circle(5, 3, 7)); //inner circle with smaller radius
        innerRing.Add(new Dot(4, 3));
        
        CompoundGraphic outerRing = new CompoundGraphic();
        outerRing.Add(new Circle(5, 3, 10)); //outer circle with larger radius 
        outerRing.Add(new Dot(3, 4));      
        
        CompoundGraphic top = new CompoundGraphic();
        top.Add(new Dot(1, 2));
        top.Add(outerRing); 
        top.Add(innerRing);        

        top.Draw(); //Draws all it's children which in turn draws their children
    }
}
```

## _The Composite Tree/Hierarchy_
```csharp                 
           CompoundGraphic top
          /        |           \
         /         |            \
        /          |             \
  Dot(1,2)         |              \   
            outerRing           innerRing  
            /    \               /       \
       Circle   Dot(3,4)    Circle        Dot
       (5,3,10)             (5,3,7)       (4,3)  
```    
