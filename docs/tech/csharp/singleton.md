# Singleton 


单例模式确保一个类只有一个实例。此模式有一个私有的构造函数，避免有多个实例。

普通写法:

```c#
public class Singleton
{
    private static Singleton? instance;

    public Singleton()
    {

    }

    public static Singleton Create()
    {
        return instance ??= new Singleton();
    }
}
```

普通写法下无法避免多线程时有多个实例。

饿汉模式 Hunger mode:

```c#
public class SingleTon
{
    private static readonly SingleTon instance = new SingleTon();

    public SingleTon()
    {

    }

    public static SingleTon Create()
    {
        return instance;
    }
}
```

将实例加上 `readonly` 关键字，将初始化由静态函数实现。