
<!-- vim-markdown-toc GFM -->

- [泛型](#泛型)
  - [原理及局限：](#原理及局限)
  - [extends 与 super 通配符](#extends-与-super-通配符)

<!-- vim-markdown-toc -->

---


### 泛型


#### 原理及局限：

- 类型擦除：  
  编译时将所有类型参数替换为Object，运行时对具体实例类型进行安全的**强制类型转型**。  
  (Object 底层实现是不是通用指针？ void \* )

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


#### extends 与 super 通配符

- 使用类似 <? extends Number> 或 <? super Integer> 定义**泛型方法**时：
  当传入限定类型的变量或返回限定类型变量时，主要考虑是否能进行安全的向上或向下转型。  
  - 前者只能获取Number类型变量，即只读。  

  - 后者只能传入Integer类型变量，即只写。

  - 例外是Object 类型。

- 使用无限定通配符<?>时，?既包括extends的语义，又有super的语义：
  - 只能读取Object的引用。
  - Pair<?> 和 Pair 不同。

- 使用类似<T extends Number> 定义**泛型类**时：
  T 类型只能是 Number 的子类。

- 使用类似<T super Number> 定义**泛型类**时：
  T 类型只能是 Number 的超类。

