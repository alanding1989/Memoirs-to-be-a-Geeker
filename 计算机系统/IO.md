
<!-- vim-markdown-toc GFM -->

- [Linux 系统 IO 模型](#linux-系统-io-模型)

<!-- vim-markdown-toc -->



### Linux 系统 IO 模型

> 只有异步IO是真正的异步操作，其他四个都需要在数据准备好后由用户程序调用内核函数，将
  内核区数据拷贝到用户区内存。


**参考资料：[Socket IO 详解](https://github.com/CyC2018/CS-Notes/blob/master/notes/Socket.md)**


- 阻塞IO： 阻塞干等型

- 非阻塞IO： 定时轮询检查

- I/O多路复用： 广播多路选择，返回优先就绪者。

- 信号IO： 

- 异步IO： 基于事件驱动循环，后台非阻塞执行，完毕后通知调用方。
