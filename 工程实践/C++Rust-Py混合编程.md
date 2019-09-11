
<!-- vim-markdown-toc GFM -->

- [混合编程](#混合编程)
  - [C/C++ 和 Python 混合编程](#cc-和-python-混合编程)
  - [Rust 和 Python 混合编程](#rust-和-python-混合编程)

<!-- vim-markdown-toc -->


### 混合编程

#### C/C++ 和 Python 混合编程

从调用的角度细分，有两种方式：  
- 单向调用，只从Python中调用C/C++代码。
- 双向调用，C/C++也会回调Python的内容。 
此外，从C/C++中调用Python代码，也偶尔出现，因为Python的某些标准库功能非常实用，
比如http.server。 大部分情况下，都是从Python单向调用C/C++。

从C/C++代码的编译情况，还能细分成两类：  
- 已编译，直接使用C/C++的动态链接库，如第三方库自己无法修改源码时。
- 未编译，需要在setup.py中编译成可导入模块。 前者往往用在使用某些著名的库，比
  如libc.so。 而后者则是往往出现在使用C/C++来提升Python运行效率、或者需要与C/C++
  交换复杂的数据结构。

相关工具特点：
- ctypes : 动态链接库，方便，无依赖，性能适中，不支持C++，移植性不好。
- pybind : 简单，无依赖，文档齐全，支持C++，开发效率高，生态丰富。
- cython : 需编译成模块，比直接写C模块方便，支持C++，性能也快，是numpy，scipy，
  scikit-learn的封装方式。
- swig  : 接口简单，无依赖，支持C++，配置稍麻烦，是tensorflow的封装方式。
- boost.python: 只需要考虑C++端就行，需boost库，构建需要许多Cpp前置知识。
- opencv: 不需要写module文件，只要在类和方法前标注，兼容性好。


#### Rust 和 Python 混合编程
参考书籍
