# Builder Design Pattern

Builder Pattern says that **construct a complex object from simple objects using step-by-step approach**. It is mostly used when object can't be created in single step like in the de-serialization of a complex object.

## _Advantage of Builder Design Pattern_

The main advantages of Builder Pattern are as follows:
- It provides clear separation between the construction and representation of an object.
- It provides better control over construction process.
- It supports to change the internal representation of objects.

## _UML Example_

![UML Example](https://www.dofactory.com/img/diagrams/net/builder.png)

## _Code Snippet_

_Two Types of Builders, for example, that both inherit abstract class **Builder**_
```csharp
public abstract class Builder {
    public abstract void BuildPartA();
    public abstract void BuildPartB();
    public abstract void BuildPartC();
    public abstract Product GetResult();
}
```

```csharp
public class ConcreteBuilder1 : Builder {
    private Product _product = new Product();

    public override void BuildPartA() {
        _product.Add("PartA");
    }

    public override void BuildPartB() {
        _product.Add("PartB");
    }
    
    public override void BuildPartC() {
        _product.Add("PartC");
    }        

    public override Product GetResult() {
        return _product;
    }
}
```

```csharp
public class ConcreteBuilder2 : Builder {
    private Product _product = new Product();

    public override void BuildPartA() {
        _product.Add("PartX");
    }

    public override void BuildPartB() {
        _product.Add("PartY");
    }
    
    public override void BuildPartC() {
        _product.Add("PartY");
    }        

    public override Product GetResult() {
        return _product;
    }
}
```

_The **Product** class which needs building_
```csharp
public class Product {
    private List<string> _parts = new List<string>();

    public void Add(string part) {
        _parts.Add(part);
    }

    public void Show() {
        Console.WriteLine("\nProduct Parts -------");
        foreach (string part in _parts)
            Console.WriteLine(part);
    }
}
```


_The **Director** class which needs calls the **Build Methods** by proper order_
```csharp
public class Director {
    public void Construct(Builder builder) {
        builder.BuildPartA();
        builder.BuildPartB();
        builder.BuildPartC();
    }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
    static void Main() {
        Director director = new Director();
        Builder b1 = new ConcreteBuilder1();
        Builder b2 = new ConcreteBuilder2();
        
        // Construct Product 1
        director.Construct(b1);
        Product p1 = b1.GetResult();
        p1.Show();
        
        // Construct Product 2        
        director.Construct(b2);
        Product p2 = b2.GetResult();
        p2.Show();
        
        // Wait for user
        Console.ReadKey();
    }
}
```