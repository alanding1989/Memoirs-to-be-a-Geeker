
<!-- vim-markdown-toc GFM -->

- [个人码农学习笔记](#个人码农学习笔记)
  - [技术书阅读方法论](#技术书阅读方法论)
  - [为什么要阅读源代码？](#为什么要阅读源代码)

<!-- vim-markdown-toc -->


### 个人码农学习笔记

---


#### 技术书阅读方法论


1. 速读一遍(最好在1~2天内完成)。人的大脑记忆力有限，在一天内快速看完一本书会在大
   脑里留下深刻印象，对于之后复习以及总结都会有特别好的作用。  
   对于每一章的知识，先阅读标题，弄懂大概讲的是什么主题，再去快速看一遍，不懂也
   没有关系，但是一定要在不懂的地方做记号，什么记号无所谓，但是要让自己后面再看
   的时候有个提醒的作用，看看第二次看有没有懂了些。  

2. 精读一遍(在2周内看完)。有了前面速读的感觉，第二次看会有慢慢深刻了思想和意识的作
   用。具体为什么不要问我，去问30年后的神经大脑专家，现在人类可能还没有总结出为什
   么大脑对记忆的完全方法论。但是，程序员打代码都是先实践，然后就渐渐懂了过程，慢
   慢懂了原理，所以第二遍读的时候稍微慢下来，2周内搞定。  
   注意：每看完一个章节后，总结一下这个章节讲了啥。很关键！  

3. 实践。在实践的时候要注意不用都去实践，最好看着书，敲下代码，把重点的内容敲一遍
   有个肌肉记忆就很不错了。以及到自己做过的项目中去把每个有涉及到原理的代码，研究
   一遍，就可以了。

---

#### 为什么要阅读源代码？

1. 自己不清楚应该怎么实现，看代码了解。
2. 真牛b为什么这么高效，看代码学习。
3. 真sb, 为什么这么低效，看代码然后修改。


在阅读源代码之前，先完成下面工作：

1. 阅读源码之前储备一些设计模式的知识，阅读起来将更省力。

2. 整体上了解这份代码是要解决什么问题。了解要阅读的框架或模块拥有的功能，在理论上能大
   致明白功能的流程。
   初次阅读的目的是为了能掌握源码实现功能的流程，最好能自己画个类的时序图。  
   列举出自己对该框架的实现的疑问点，带着问题去研究源码，从代码中找答案。
   并且从疑问中自己试着去解答，去验证自己的猜想，这样能更有兴趣的读下去。
3. 接着再次重复阅读（带着目的的）查看具体的实现细节。再次阅读实现细节上了解有哪些接口，
   有哪些类，为什么要这些接口和类。
4. 根据什么样的原理来实现的。
