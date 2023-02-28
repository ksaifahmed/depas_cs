# Chain of Responsibility Design Pattern

In chain of responsibility, sender sends a request to a chain of objects. The request can be handled by any object in the chain.

A Chain of Responsibility Pattern says that just **avoid coupling the sender of a request to its receiver by giving multiple objects a chance to handle the request**. 

> For example, an ATM uses the Chain of Responsibility design pattern in money giving process.

In other words, we can say that normally each receiver contains reference of another receiver. If one object cannot handle the request then it passes the same to the next receiver and so on.

## _Advantage of Chain of Responsibility Pattern_
- It reduces the coupling.
- It adds flexibility while assigning the responsibilities to objects.
- It allows a set of classes to act as one; events produced in one class can be sent to other handler classes with the help of composition.


## _Usage of Chain of Responsibility Pattern_

- When more than one object can handle a request and the handler is unknown.
- When the group of objects that can handle the request must be specified in dynamic way.

## _UML Example_

![UML Example](https://refactoring.guru/images/patterns/diagrams/chain-of-responsibility/structure-2x.png)

## _Code Snippet_

_The **Handler** interface_
```csharp
using System;

public interface Handler
{
    void setNext(Handler h);
    void handle(string request);
}
```

_**Base Handler** for handling requests_
```csharp
public class BaseHandler : Handler
{
    private Handler next;
    public void setNext(Handler h)
    {
        next = h;
    }
    public virtual void handle(string request)
    {
        if (next != null)
        {
            next.handle(request);
        }
    }
}
```

_**Concrete Handler** that handles specific requests_
```csharp
public class Handler1 : BaseHandler
{
    public override void handle(string request)
    {
        if (request == "one")
        {
            Console.WriteLine("Handler1 handled request");
        }
        else
        {
            base.handle(request);
        }
    }
}
```

_Another **Concrete Handler** that handles specific requests_
```csharp
public class Handler2 : BaseHandler
{
    public override void handle(string request)
    {
        if (request == "two")
        {
            Console.WriteLine("Handler2 handled request");
        }
        else
        {
            base.handle(request);
        }
    }
}
```

_Yet another **Concrete Handler** that handles specific requests_
```csharp
public class Handler3 : BaseHandler
{
    public override void handle(string request)
    {
        if (request == "three")
        {
            Console.WriteLine("Handler3 handled request");
        }
        else
        {
            base.handle(request);
        }
    }
}
```


_The Driver Code AKA **Client**_
```csharp
public class HelloWorld {
  static void Main() {
        Handler h1 = new Handler1();
        Handler h2 = new Handler2();
        Handler h3 = new Handler3();
        h1.setNext(h2);
        h2.setNext(h3);
        h1.handle("one");
        h1.handle("two");
        h1.handle("three");
        h1.handle("four");
  }
}
```