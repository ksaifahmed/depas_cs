# Factory Method

A Factory Pattern or Factory Method Pattern says that just **define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate.** In other words, subclasses are responsible for creating the instance of the class.

The Factory Method Pattern is also known as **Virtual Constructor.**

## _Advantage of Factory Design Pattern_

- Factory Method Pattern allows the sub-classes to choose the type of objects to create.
- It promotes the **loose-coupling** by eliminating the need to bind application-specific classes into the code. That means the code interacts solely with the resultant interface or abstract class, so that it will work with any classes that implement that interface or that extends that abstract class.

## _Usage of Factory Design Pattern_

- When a class doesn't know what sub-classes will be required to create
- When a class wants that its sub-classes specify the objects to be created.
- When the parent classes choose the creation of objects to its sub-classes.

## _UML Example_

![UML Example](https://www.tutorialspoint.com/design_pattern/images/factory_pattern_uml_diagram.jpg)

## _Code Snippet_
_Abstract interface called **Shape**_
```csharp
using System;
public interface Shape {
   void draw();
}
```

_Child Class **Rectangle** that inherits **Shape**_
```csharp
public class Rectangle : Shape {
   public void draw() {
      Console.WriteLine("Inside Rectangle::draw() method.");
   }
}
```

_Child class **Square** that inherits **Shape**_
```csharp
public class Square : Shape {
   public void draw() {
      Console.WriteLine("Inside Square::draw() method.");
   }
}
```

_Child class **Circle** that inherits **Shape**_
```csharp
public class Circle : Shape {
   public void draw() {
      Console.WriteLine("Inside Circle::draw() method.");
   }
}
```

_The **Factory Class** with the **Factory Method** --> `getShape()`_
```csharp
public class ShapeFactory {
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }		
      if(shapeType.Equals("CIRCLE")){
         return new Circle();
         
      } else if(shapeType.Equals("RECTANGLE")){
         return new Rectangle();
         
      } else if(shapeType.Equals("SQUARE")){
         return new Square();
      }
      return null;
   }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
    static void Main() {
        ShapeFactory shapeFactory = new ShapeFactory();
        
        //get an object of Circle and call its draw method.
        Shape shape1 = shapeFactory.getShape("CIRCLE");
        
        //call draw method of Circle
        shape1.draw();
        
        //get an object of Rectangle and call its draw method.
        Shape shape2 = shapeFactory.getShape("RECTANGLE");
        
        //call draw method of Rectangle
        shape2.draw();
        
        //get an object of Square and call its draw method.
        Shape shape3 = shapeFactory.getShape("SQUARE");
        
        //call draw method of square
        shape3.draw();
    }
}
```
