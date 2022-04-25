# LINQ

LINQ (发音：link) 是一种通用的查询语言。

```c#
static void Main()
{
    List<int>  nums = new List<int>{1,2,5,3,15};
    IEnumerable<int> smallNums = from n in nums where n < 10 select n;
    foreach (int n in smallNums)
    {
        Console.Write("{0} ,", n);
    }
}
```

## 匿名类型

LINQ 的查询结果经常会用到匿名类型，匿名类型不需要指定成员的类型。

```c#
var student = new {Name = "Fanng", Age = 18};
Console.WriteLine("Hi {0}, your age is {1}", student.Name, student.Age);
```

* 匿名类型只能是局部变量，不能做为类成员。
* 匿名类型只能用 `var` 。

## 查询

LINQ 支持方法语法和查询语法（推荐）两种方式查询。两种方法可以混用。

### 方法语法

是一个标准的方法，包括方法名和里面的参数。比如`Count()`。

```c#
List<int> nums = new List<int> {1, 2, 5, 3, 15};
var numsMethod = nums.Where(n => n < 10);
```

### 查询语法（推荐）

类似于SQL写法，更加直观。

```c#
List<int> nums = new List<int> {1, 2, 5, 3, 15};
var numsQuery = from n in nums where n < 10 select n;
```

## LINQ支持的查询方法

### Aggregate

Aggregate 可以做一些复杂的聚合运算，例如累计求和，累计求乘积。它接受2个参数，一般第一个参数是称为累积数（默认情况下等于第一个值），而第二个代表了下一个值。

```c#
List<int> nums = new List<int> {1, 3, 5, 7, 9};
var numsSum = nums.Aggregate(func: (tmpSums, next) => tmpSums + next);
Console.WriteLine("Sum: {0}", numsSum);
var numsMax = nums.Aggregate((tmpMax, next) => tmpMax > next ? tmpMax : next);
Console.WriteLine("Max: {0}", numsMax);
```

可选一个`seed`参数做为初始的累加值。

```c#
var numsCount = nums.Aggregate(0, (cnt, next) => ++cnt);
Console.WriteLine("Count: {0}", numsCount);
```

ref:

* https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.aggregate?view=net-6.0
* https://ithelp.ithome.com.tw/articles/10197334
* https://blog.csdn.net/zhifeiya/article/details/45031655

### join

类似于SQL中的join，可以把两个集合的元素结合起来。

```c#
public class Student
{
    public int    StID;
    public string LastName;
}

public class CourseStudent
{
    public string CourseName;
    public int    StID;
}

static Student[] students = new Student[] {
    new Student { StID = 1, LastName = "Carson" },
    new Student { StID = 2, LastName = "Klassen" },
    new Student { StID = 3, LastName = "Fleming" },
};

static CourseStudent[] studentsInCourses = new CourseStudent[] {
    new CourseStudent { CourseName = "Art", StID     = 1 },
    new CourseStudent { CourseName = "Art", StID     = 2 },
    new CourseStudent { CourseName = "History", StID = 1 },
    new CourseStudent { CourseName = "History", StID = 3 },
    new CourseStudent { CourseName = "Physics", StID = 3 },
};

static void TestJoin()
{
    var query = from s in students
        join c in studentsInCourses on s.StID equals c.StID
        where c.CourseName == "History"
        select s.LastName;

    foreach (var name in query)
    {
        Console.WriteLine(name);
    }
}
```

ref:

* https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/join-clause
