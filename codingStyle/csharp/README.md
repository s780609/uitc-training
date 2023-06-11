# CSharp Coding style

## Naming conventions
Pascal case
Use pascal casing ("PascalCasing") when naming a class, record, or struct.

```C#
public class DataService
{
}
```
```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```
```C#
public struct ValueCoordinate
{
}
```
When naming an interface, use pascal casing in addition to prefixing the name with an I. This clearly indicates to consumers that it's an interface.

```C#
public interface IWorkerQueue
{
}
```
When naming public members of types, such as fields, properties, events, methods, and local functions, use pascal casing.

```C#
public class ExampleEvents
{
    // A public field, these should be used sparingly
    public bool IsValid;

    // An init-only property
    public IWorkerQueue WorkerQueue { get; init; }

    // An event
    public event Action EventProcessing;

    // Method
    public void StartEventProcessing()
    {
        // Local function
        static int CountQueueItems() => WorkerQueue.Count;
        // ...
    }
}
```
When writing positional records, use pascal casing for parameters as they're the public properties of the record.

```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```
For more information on positional records, see Positional syntax for property definition.

Camel case
Use camel casing ("camelCasing") when naming private or internal fields, and prefix them with _.

```C#
public class DataService
{
    private IWorkerQueue _workerQueue;
}
```
Tip

When editing C# code that follows these naming conventions in an IDE that supports statement completion, typing _ will show all of the object-scoped members.

When working with static fields that are private or internal, use the s_ prefix and for thread static use t_.

```C#
public class DataService
{
    private static IWorkerQueue s_workerQueue;

    [ThreadStatic]
    private static TimeSpan t_timeSpan;
}
```
When writing method parameters, use camel casing.

```C#
public T SomeMethod<T>(int someNumber, bool isValid)
{
}
```
For more information on C# naming conventions, see [C# Coding Style](https://github.com/dotnet/runtime/blob/main/docs/coding-guidelines/coding-style.md).

Additional naming conventions
Examples that don't include using directives, use namespace qualifications. If you know that a namespace is imported by default in a project, you don't have to fully qualify the names from that namespace. Qualified names can be broken after a dot (.) if they are too long for a single line, as shown in the following example.

```C#
var currentPerformanceCounterCategory = new System.Diagnostics.PerformanceCounterCategory();
```
You don't have to change the names of objects that were created by using the Visual Studio designer tools to make them fit other guidelines.

## Layout conventions
`return` 的上方必須空一行，除非是該scope第一行
```C#
public string SomeMethod(string input)
{
    string a = "" + input;

    return a;
}
```

`if` and `for loop` block 結束後，要空一行
```C#
public void SomeMethod(string input)
{
    string a = "" + input;

    if (string.IsNullOrEmpty(a)) {
        a = "do something";
    }

    for (int i = 0; i < 10;i++) {
        a += i.ToString();
    }

    a = "do something" + "number 2";
}
```

## Commenting conventions

### 註解(`//`)都必須使用新的一行，不要把註解寫在 code 後面   
❌
```C#
var Case = "b"; // 不要寫註解在這
```
✔️
```C#
// 寫註解在這
var Case = "b";
```

### 註解符號後面都要空一格
❌
```C#
//The following declaration creates a query. It does not run
//the query.
```
✔️
```C#
// The following declaration creates a query. It does not run
// the query.
```

### 註解上方必須空一行，除非是該scope第一行
❌
```C#
public string test (string input) {
    var a = "a" + input;
    // 註解上方要空一行
    var b = "b";
}
```
✔️
```C#
public string test (string input) {
    var a = "a" + input;

    // 註解上方要空一行
    var b = "b";
}
```