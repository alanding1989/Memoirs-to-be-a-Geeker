
<!-- vim-markdown-toc GFM -->

- [泛型](#泛型)
  - [原理及局限：](#原理及局限)
  - [extends 与 super 通配符，协变与逆变](#extends-与-super-通配符协变与逆变)
- [函数式编程，行为参数化](#函数式编程行为参数化)
  - [方法引用](#方法引用)
  - [函数式接口](#函数式接口)
  - [复合Lambda表达式](#复合lambda表达式)
- [Stream API](#stream-api)
  - [创建流](#创建流)
  - [原始类型特化，内置数值类型避免自动装拆箱的操作](#原始类型特化内置数值类型避免自动装拆箱的操作)
  - [处理数据 - 中间过程](#处理数据---中间过程)
  - [流元素收集 - 结尾操作](#流元素收集---结尾操作)
  - [正确并行化](#正确并行化)
- [Optional 类](#optional-类)

<!-- vim-markdown-toc -->

---


### 泛型


#### 原理及局限：

- 类型擦除：  
  编译时将所有类型参数替换为Object，运行时对具体实例类型进行安全的**强制类型转型**。  
  (Object 还有Go 的interface {} 底层实现是不是通用指针？ void \* )

- 类型擦除的局限： 
  - 类型参数不能是基本类型，因为Object 字段无法持有基本类型。

  - 无法取得带泛型的类类型对象Class。

  ``` java
  Pair<String> s = ...; 
  Pair<String> i = ...; 
  Class c1 = s.getClass();
  Class c2 = i.getClass()
  System.out.println(c1 == c2);  // true
  System.out.println(c1 == Pair.class);  // true
  ```
  - 无法判断带泛型的Class。

  ``` java
  if (s instanceof Pair<String>.class) {  // compile error
    do ...
  }
  ```

  - 泛型方法或类中不能实例化**类型参数**的类型，因为是 new Object()。


#### extends 与 super 通配符，协变与逆变
由于参数化类型的参数(参数类型)是可变的，当两个参数化类型的参数是继承关系(可泛化)时，
那被参数化的类型是否也可以泛化呢？

> 对于某个对象消费的值适用逆变，而它产出的值适用协变。  
  如果同时消费和产出，则类型应该保持不变。通常适用于可变数据结构。

- 使用类似 <? extends Number> 或 <? super Integer> 定义**泛型方法**时：
  当传入限定类型的变量或返回限定类型变量时，主要考虑是否能进行安全的向上或向下转型。  
  - 前者只能获取Number类型变量，即只读。  

  - 后者只能传入Integer类型变量，即只写。

  - 例外是Object 类型。

- 使用无限定通配符<?>时，? 既包括extends的语义，又有super的语义：
  - 只能读取Object的引用。
  - Pair<?> 和 Pair 不同。

- 使用类似<T extends Number> 定义**泛型类**时：
  T 类型只能是 Number 的子类。

- 使用类似<T super Number> 定义**泛型类**时：
  T 类型只能是 Number 的超类。



### 函数式编程，行为参数化


#### 方法引用
- 类的静态方法

- 类的实例方法

- 类的构造方法


#### 函数式接口
> 只有一个抽象方法，并用FunctionalInterface注解标记的接口。

- **Predicate**： 返回Boolean，进行元素筛选，行为参数化。

- **Consumer**： 对元素做一堆操作，返回void。

- **Function**： 元素映射操作，返回新的元素序列，。


#### 复合Lambda表达式
- 比较器复合：sort() reversed() thenComparing(), 生成比较器的静态方法Comparator.comparing()

- 谓词复合： negate() and() or() 或与非

- 函数复合： then() compose()



### Stream API

> 流只能遍历一次


#### 创建流
- 用**集合**对象的stream()方法。

- 用静态方法Stream.of()，通过**显式值**创建，如字符串。

- 通过工具类静态方法Arrays.stream()从**数组**创建。

- 用NIO API java.nio.file.Files 中很多静态方法返回一个文件流。

- 用Stream.iterate() 或 Stream.generate() 生成无限流，配合limit()限定流大小。


#### 原始类型特化，内置数值类型避免自动装拆箱的操作
- IntStream，IntSupplier，LongStream，LongSupplier，DoubleStream，DoubleSupplier 

- mapToInt()，mapToLong() ...方法


#### 处理数据 - 中间过程
- 筛选和切片： filter() distinct() skip() limit()

- 数值映射： map() flatMap()

- 查找和匹配： findFirst() findAny() allMatch() noneMatch() anyMatch()

- 归约： reduce()


#### 流元素收集 - 结尾操作
- 预定义收集器工厂方法Collectors
  - 将元素收集到一个集合中：
    toList() toSet() (toCollection()，someCollection::new())

  - 将流元素归约和汇总为一个值： 
    maxBy() minBy() summingInt() averagingInt() summarizingInt()  
    字符串拼接 joining()  
    更一般的泛化方法 reducing()  
  
  - 元素分组，一级分组、多级分组：
    groupingBy()  
    collectingAndThen()，转换收集器返回结果，去掉无用类型
    
  - 元素分区：分组的特殊情况 - 分类函数返回Boolean，分为两组
    partitioningBy()

  - 自定义收集器：


#### 正确并行化
> 并行化并不是没有代价。并行化过程本身需要对流做递归划分，把每个子流的归纳操作分配到不同的
  线程，然后把这些操作的结果合并成一个值。  
  但在多个内核之间移动数据的代价也很大，所以很重要的
  一点是要保证在内核中并行执行工作的时间比在内核之间传输数据的时间长。

- 错用并行流的主要原因就是使用的算法改变了某些共享状态(变量)。因此要避免共享状态(变量)。
  如果代码里面出现了传统并发模型里需要用锁解决同步的共享数据，那并行化代码就是错的。

- 留意装箱机制的开销。

- 较小数据量，没有必要，额外开销也大。

- 考虑背后数据结构是否易于分解。

- 测试，把顺序流转化成并行流很简单。


### Optional 类
- 不支持字段序列化

