# 面试题目汇总

## 技术

## JAVA
**不通过构造函数也能创建对象吗？** 可以

Java创建对象的几种方式

  * 用new语句创建对象，这是最常见的创建对象的方法。
  * 运用反射手段,调用java.lang.Class或者java.lang.reflect.Constructor类的newInstance()实例方法。
  * 调用对象的clone()方法。
  * 运用反序列化手段，调用java.io.ObjectInputStream对象的 readObject()方法。

(1)和(2)都会明确的显式的调用构造函数 ；(3)是在内存上对已有对象的影印，所以不会调用构造函数 ；(4)是从文件中还原类的对象，也不会调用构造函数。


**在MVC模型中，业务逻辑应该写在哪一层？** Model


## Linux

**目录为什么不可做硬链接？**

[Linux面试题](https://github.com/trimstray/test-your-sysadmin-skills)

## MySQL

**char与varchar的区别？**

(1)、varchar与char的区别char是一种固定长度的类型，varchar则是一种可变长度的类型
(2)、varchar(50)中50的涵义最多存放50个字符，varchar(50)和(200)存储hello所占空间一样，但后者在排序时会消耗更多内存，因为order by col采用fixed_length计算col长度(memory引擎也一样)

**MySQL数据类型？**

**myisam与innodb的区别？**

1>.InnoDB支持事物，而MyISAM不支持事物
2>.InnoDB支持行级锁，而MyISAM支持表级锁
3>.InnoDB支持MVCC, 而MyISAM不支持
4>.InnoDB支持外键，而MyISAM不支持
5>.InnoDB不支持全文索引，而MyISAM支持。
(2)、innodb引擎的4大特性
插入缓冲（insert buffer),二次写(double write),自适应哈希索引(ahi),预读(read ahead)
(3)、2者selectcount(*)哪个更快，为什么 myisam更快，因为myisam内部维护了一个计数器，可以直接调取。



## redis
**mySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据？**

 

相关知识：redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。redis 提供 6种数据淘汰策略：

 

volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰

volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰

volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰

allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰

allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰

no-enviction（驱逐）：禁止驱逐数据

redis和memcache 区别。

* Cookie和Session的区别
HTTP是无状态协议，但是在实际应用中有跟踪客户端状态的需求，Cookie和Session是两种不同的实现方案。

Cookie保存在客户端，Session保存在服务端
Cookie没有Session安全，侵入者可以通过分析客户端的cookie信息侵入网站；
使用Session存储重要信息，使用Cookie存储不那么重要的信息；
使用Session方案时，常常需要依赖Cookie传递SID的值，如果客户端禁用了Cookie，则转而采取URL重写技术（但是这种技术有安全风险）；


## 人品

为何从上家公司离职？
最近看的一本书是什么？