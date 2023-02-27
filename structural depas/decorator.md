# Decorator Design Pattern
A Decorator Pattern says that just **attach a flexible additional responsibilities to an object dynamically**.

In other words, The Decorator Pattern uses **Composition/Aggregation** instead of **Inheritance** to extend the functionality of an object at runtime.

The Decorator Pattern is also known as **Wrapper**.

## _Advantage of Decorator Pattern_
- It provides greater flexibility than static inheritance.
- It enhances the extensibility of the object, because changes are made by coding new classes.
- It simplifies the coding by allowing you to develop a series of functionality from targeted classes instead of coding all of the behavior into the object.

## _Usage of Decorator Pattern_
- When you want to transparently and dynamically add responsibilities to objects without affecting other objects.
- When you want to add responsibilities to an object that you may want to change in future.
Extending functionality by sub-classing is no longer practical.


## _Differences With **Composite Design Pattern**_
Composite and Decorator have similar structure diagrams since both rely on **recursive composition** to organize an open-ended number of objects.

- A Decorator is like a Composite but **only has one child component**.
- Decorator **adds additional responsibilities** to the wrapped object, while Composite just **sums up its children’s results**.


## _UML Example_
![UML Example](https://media.licdn.com/dms/image/C4D12AQGTXpXALbXXjA/article-cover_image-shrink_423_752/0/1597684217471?e=1683158400&v=beta&t=pe3cvbc2OTn-yN4EXkNnkgn6IvVa_derrX-LjrxedrU)


## _Code Snippet_

_The Component Interface_
```csharp
public interface INotifier
{
    void Send(string message);
}
```

_Concrete Component class **EmailNotifier**_
```csharp
public class EmailNotifier : INotifier
{
    private readonly List<string> _emailAddresses;

    public EmailNotifier(List<string> emailAddresses)
    {
        _emailAddresses = emailAddresses;
    }

    public void Send(string message)
    {
        Console.WriteLine("Sending email notification to:");
        foreach (var email in _emailAddresses)
        {
            Console.WriteLine(email);
        }
        Console.WriteLine($"Message: {message}");
    }
}
```

_Decorator abstract class called NotifierDecorator that will wrap around an initial **Notifier**_
```csharp
public abstract class NotifierDecorator : INotifier
{
    protected INotifier Notifier;

    public NotifierDecorator(INotifier notifier)
    {
        Notifier = notifier;
    }

    public virtual void Send(string message)
    {
        Notifier.Send(message);
    }
}
```

_Concrete Decorator class called **SMSNotifier**_
```csharp
// Concrete Decorator class
public class SMSNotifier : NotifierDecorator
{
    private readonly List<string> _phoneNumbers;

    public SMSNotifier(INotifier notifier, List<string> phoneNumbers) : base(notifier)
    {
        _phoneNumbers = phoneNumbers;
    }

    public override void Send(string message)
    {
        Notifier.Send(message);
        Console.WriteLine("Sending SMS notification to:");
        foreach (var phoneNumber in _phoneNumbers)
        {
            Console.WriteLine(phoneNumber);
        }
        Console.WriteLine($"Message: {message}");
    }
}
```

_Another Concrete Decorator class called **FacebookNotifier**_
```csharp
public class FacebookNotifier : NotifierDecorator
{
    private readonly List<string> _facebookIds;

    public FacebookNotifier(INotifier notifier, List<string> facebookIds) : base(notifier)
    {
        _facebookIds = facebookIds;
    }

    public override void Send(string message)
    {
        Notifier.Send(message);
        Console.WriteLine("Sending Facebook notification to:");
        foreach (var facebookId in _facebookIds)
        {
            Console.WriteLine(facebookId);
        }
        Console.WriteLine($"Message: {message}");
    }
}
```



_The Driver Code AKA **Client**_
```csharp
class HelloWorld {
    static void Main(string[] args)
    {
        var emailNotifier = new EmailNotifier(new List<string> {"john@example.com", "jane@example.com"});
        emailNotifier.Send("Hello, email!"); // email only

        var smsNotifier = new SMSNotifier(emailNotifier, new List<string> {"555-1234"});
        smsNotifier.Send("Hello, SMS!"); //sends to sms and email

        var facebookNotifier = new FacebookNotifier(smsNotifier, new List<string> {"123456789"});
        facebookNotifier.Send("Hello, Facebook!"); //sends to all three
    }
}
```
