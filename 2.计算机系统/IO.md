
<!-- vim-markdown-toc GFM -->

- [Linux 系统 IO 模型](#linux-系统-io-模型)
  - [参考资料](#参考资料)
  - [五种IO模型](#五种io模型)
  - [selcet，poll，epoll](#selcetpollepoll)

<!-- vim-markdown-toc -->

---


### Linux 系统 IO 模型

#### 参考资料
- [Socket IO 详解](https://github.com/CyC2018/CS-Notes/blob/master/notes/Socket.md)

- [IO多路复用select，poll，epoll比较-1](https://www.cnblogs.com/aspirant/p/9166944.html)

- [IO多路复用select，poll，epoll比较-2](https://www.jianshu.com/p/397449cadc9a)


#### 五种IO模型

- 阻塞IO： IO请求系统调用直到数据被拷贝到用户空间才返回，过程中当前进程被阻塞傻等。

- 非阻塞IO： IO请求立即返回错误，之后**忙**轮询进行系统调用检查IO数据是否就绪(不返回错误)，占用CPU时间片，还会有空轮询情况，CPU利用率不高。

- I/O多路复用： IO请求立即返回，同一个进程可监听多个IO事件(多路广播)，返回优先就绪者。

- 信号IO： IO请求立即返回，IO数据就绪后内核通知用户进程可以进行下一步操作，用户进程系统调用复制数据到用户空间。

- 异步IO： 用户IO请求立即返回，内核自动把IO数据拷贝到用户空间，完成后给用户进程一个反馈信号。

> 只有异步IO是真正的异步操作，其他四个都需要在数据准备好后由用户进程进行系统调用，将数据从内核
  空间拷贝到用户空间。


#### selcet，poll，epoll

- select和poll对监听事件判断是否就绪是无差别轮询，采用遍历机制，时间复杂度O(n)。

- epoll底层实现采用回调机制，对每个IO事件注册一个对应的处理函数(hashmap实现)，某个事件就绪，就调用该函数将事件加
  入就绪队列，时间复杂度O(1)。


内核缓冲区只有4KB。


