
<!-- vim-markdown-toc GFM -->

- [Linux 系统 IO 模型](#linux-系统-io-模型)
  - [参考资料](#参考资料)
  - [五种IO模型](#五种io模型)

<!-- vim-markdown-toc -->

---


### Linux 系统 IO 模型

#### 参考资料
- [Socket IO 详解](https://github.com/CyC2018/CS-Notes/blob/master/notes/Socket.md)

- [IO多路复用select，poll，epoll比较-1](https://www.cnblogs.com/aspirant/p/9166944.html)

- [IO多路复用select，poll，epoll比较-2](https://www.jianshu.com/p/397449cadc9a)


#### 五种IO模型

- 阻塞IO： IO请求系统调用直到数据被拷贝到用户空间才返回，过程中当前进程被阻塞傻等。

- 非阻塞IO： IO请求立即返回错误，之后**忙**轮询系统调用检查IO数据是否就绪(不返回错误)，占用CPU时间片，CPU利用率不高。

- I/O多路复用： IO请求立即返回，同一个进程可监听多个IO事件(多路广播)，返回优先就绪者。

- 信号IO： IO请求立即返回，IO数据就绪后内核通知用户进程可以进行下一步操作，用户进程系统调用复制数据到用户空间。

- 异步IO： 用户IO请求立即返回，内核自动把IO数据拷贝到用户空间，完成后给用户进程一个反馈信号。

> 只有异步IO是真正的异步操作，其他四个都需要在数据准备好后由用户进程进行系统调用，将数据从内核
  空间拷贝到用户空间。


内核缓冲区只有4KB。

