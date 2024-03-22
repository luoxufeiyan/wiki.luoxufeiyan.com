# ValueTuple

ValueTuple is a structure introduced in [C# 7.0](https://learn.microsoft.com/en-us/dotnet/api/system.valuetuple?view=net-8.0) which represents the value type Tuple. It provides strong naming conventions.

Tuple is of reference type, but ValueTuple is of [value type](https://learn.microsoft.com/en-us/dotnet/api/system.valuetuple?view=net-8.0).


## Example

For example:

### define
Define a value tuple:

```c#
var drinkTuple = (name: "coke", cty: 2);
```

Access item by ites name:

```c#
Console.WriteLine($"The drink {drinkTuple.name} have {drinkTuple.cty} items.");
```

### use in function

```c#
public (string FirstName, string LastName) GetNames(string! fullName)
{
  string[] names = fullName.Split(" ", 2);
  return (names[0], names[1]);
}
public void Main()
{
  // ...
  (string first, string last) = GetNames("Inigo Montoya");
  // ...
}
```

Access tuple item by its name:

```c#
Console.WriteLine($”My name is { names.first } { names.last }.”);
```

