# Abstract Factory Pattern

Abstract Factory Pattern says that just **define an interface or abstract class for creating families of related (or dependent) objects but without specifying their concrete sub-classes.** That means Abstract Factory lets a class returns a factory of classes. So, this is the reason that Abstract Factory Pattern is one level higher than the Factory Pattern.

An Abstract Factory Pattern is also known as **Kit/Factory of Factories**.

## _Advantage of Abstract Factory Design Pattern_

- Abstract Factory Pattern isolates the client code from concrete (implementation) classes.
- It eases the exchanging of object families.
- It promotes consistency among objects.

## _Usage of Abstract Factory Design Pattern_

- When the system needs to be independent of how its object are created, composed, and represented.
- When the family of related objects has to be used together, then this constraint needs to be enforced.
- When you want to provide a library of objects that does not show implementations and only reveals interfaces.
- When the system needs to be configured with one of a multiple family of objects.

## _UML Example_

![UML Example](https://www.tutorialspoint.com/design_pattern/images/abstractfactory_pattern_uml_diagram.jpg)

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

_Child Class **RoundRectangle** that inherits **Shape**_
```csharp
public class RoundRectangle : Shape {
   public void draw() {
      Console.WriteLine("Inside RoundRectangle::draw() method.");
   }
}
```

_Child class **RoundSquare** that inherits **Shape**_
```csharp
public class RoundSquare : Shape {
   public void draw() {
      Console.WriteLine("Inside RoundSquare::draw() method.");
   }
}
```

_Abstract interface factory **Shape**_
```csharp
using System;
public interface AbstractFactory {
   Shape getShape(String shapeType);
}
```

_The **ShapeFactory Class** with the **Factory Method** --> `getShape()`_
```csharp
public class ShapeFactory : AbstractFactory {
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      } 
      else if(shapeType.Equals("RECTANGLE")){
         return new Rectangle();
      }
      else if(shapeType.Equals("SQUARE")){
         return new Square();
      }
      return null;
   }
}
```

_The **RoundShapeFactory Class** with the **Factory Method** --> `getShape()`_
```csharp
public class RoundShapeFactory : AbstractFactory {
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      } 
      else if(shapeType.Equals("RECTANGLE")){
         return new RoundRectangle();
      }
      else if(shapeType.Equals("SQUARE")){
         return new RoundSquare();
      }
      return null;
   }
}
```

_The **FactoryProducer Class** that creates the appropriate **Factory**_
```csharp
public static class FactoryProducer {
   public static AbstractFactory getFactory(bool round){   
      if(round){
         return new RoundShapeFactory();         
      }else{
         return new ShapeFactory();
      }
   }
}
```

_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
    static void Main() {
        AbstractFactory shapeFactory = FactoryProducer.getFactory(true); //get a Round Shape Factory
        
        //get an object of SQUARE and call its draw method.
        //will create a Round square, because RoundShapeFactory
        Shape shape1 = shapeFactory.getShape("SQUARE");
        
        //call draw method of Round Square
        shape1.draw();
        
        //get an object of Round Rectangle and call its draw method.
        Shape shape2 = shapeFactory.getShape("RECTANGLE");
        
        //call draw method of Round Rectangle
        shape2.draw();
    }
}
```
