# pattern matching syntax 模式匹配语法

Pattern matching syntax helps developers to write more concise and readable code, particularly when dealing with complex data structures or performing multiple conditional checks on the values and types of objects.

模式匹配用于检查给定值是否符合特定模式，并在符合时进行相应的操作。模式匹配从 C# 7.0 开始引入，并在之后的版本中不断得到扩展和增强，特别是在 C# 8.0 及以后的版本中，模式匹配提供了更强大的功能和更简洁的语法。

常用的使用方式是使用 `{}` 语法，可以有效避免繁琐的 null 检查，并将各种检查和捕获逻辑整合在一起，提高代码的可读性和维护性。

### 基本用法

- **简单非null检查**：
   可以用来简洁地检查对象是否非null。
   ```csharp
   object obj = SomeMethod();
   if (obj is { })
   {
       // obj 是非null的，可以安全使用
   }
   ```
### 复杂表达式模式匹配

- **带有条件的属性模式匹配**：
   可以在检查对象及其属性同时，还能使用逻辑运算符进行更多复杂的条件匹配。
   ```csharp
   if (obj is List<int> { Count: > 0 } list)
   {
       Console.WriteLine($"First element is {list[0]}");
   }
   ```

### 属性模式匹配

- **对象属性捕获**：
   使用模式匹配结合 `{}` 可以直接访问对象中的属性和字段，并将它们捕获到新的变量中。
   ```csharp
   Point point = new Point(1, 2);

   if (point is { X: 1, Y: 2 })
   {
       Console.WriteLine("The point is at (1, 2)");
   }
   ```

- **嵌套对象的属性模式匹配**：
   可以用于匹配嵌套对象及其属性。
   ```csharp
   Person person = new Person { Name = "Alice", Address = new Address { City = "Wonderland" } };

   if (person is { Address: { City: "Wonderland" } })
   {
       Console.WriteLine($"The person lives in Wonderland");
   }
   ```

Ref:
- [Pattern matching overview - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/functional/pattern-matching)

