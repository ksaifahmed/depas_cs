# Prototype Design Pattern 

Prototype Pattern says that cloning of an existing object instead of creating new one and can also be customized as per the requirement.

This pattern should be followed, if the cost of creating a new object is expensive and resource intensive.

## _Advantage of Prototype Pattern_

The main advantages of prototype pattern are as follows:
- It reduces the need of sub-classing.
- It hides complexities of creating objects.
- The clients can get new objects without knowing which type of object it will be.
- It lets you add or remove objects at runtime.

## _Usage of Prototype Pattern_
- When the classes are instantiated at runtime.
- When the cost of creating an object is expensive or complicated.
- When you want to keep the number of classes in an application minimum.
- When the client application needs to be unaware of object creation and representation.

## _UML Example_
![UML Example](https://refactoring.guru/images/patterns/diagrams/prototype/structure-prototype-cache.png)

## _Code Snippet_


_the **Prototype** interface forces classes who implement it to implement the **clone()** method_
```csharp
using System;
using System.Collections.Generic;

public interface Prototype{
    string getColor();
    Prototype clone();
}
```

_The **Button** class implements the **Prototype** interface_
```csharp
public class Button : Prototype {
    int x, y;
    string color;
    
    public Button(){}
    
    public Button(int x, int y, string color) {
        this.x = x;
        this.y = y;
        this.color = color;
    }
    
    public Button(Prototype button) {
        Button b = (Button) button;
        this.x = b.x;
        this.y = b.y;
        this.color = b.color;
    }
    
    public string getColor() {
        return this.color;
    }
    
    public Prototype clone() {
        return new Button(this);
    }
    
    public override string ToString()
    {
        return $"Button: Position ->({x},{y}), Color-> {color}";
    }
}
```


_The **PrototypeRegistry** is a cache/list of frequency cloned items for convenience of code_
```csharp
public class PrototypeRegistry{
    private Dictionary<string, Prototype> items = new Dictionary<string, Prototype>();
    
    public void addItem(string btnType, Prototype btn) {
        items.Add(btnType, btn);
    }
    public Prototype getById(string key) {
        return new Button(items[key]);
    }
    public Prototype getByColor(string color) {
        foreach (KeyValuePair<string, Prototype> item in items) {
            Button b = (Button) item.Value;
            if (b.getColor().Equals(color))
                return new Button(item.Value);
        }
        return new Button();
    } 
}
```

_The Driver Code AKA **Client**_
```csharp
class HelloWorld {
  static void Main() {
    Button b = new Button(10,40, "red");
    Console.WriteLine(b);
    
    Button b1 = (Button) b.clone();
    Console.WriteLine(b1);
    
    PrototypeRegistry registry = new PrototypeRegistry();
    registry.addItem("red", b);
    
    Button b3 = (Button) registry.getByColor("red");
    Console.WriteLine(b3);
  }
}
```