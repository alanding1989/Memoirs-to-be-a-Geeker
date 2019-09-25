
<!-- vim-markdown-toc GFM -->

- [Web 备忘录](#web-备忘录)
  - [业务状况分类](#业务状况分类)
- [后端技术体系：](#后端技术体系)
  - [Web服务器(Tomcat，Nginx)](#web服务器tomcatnginx)
  - [框架](#框架)
  - [数据库](#数据库)
  - [分布式系统](#分布式系统)
  - [虚拟化 docker，kubernates](#虚拟化-dockerkubernates)
  - [安全](#安全)

<!-- vim-markdown-toc -->


### Web 备忘录

---


#### 业务状况分类
> 游戏、广告、媒体、社交、金融等

服务端/后端  
├系统类型  
│├B/S  
││├企业内部应用  
││├电子商务应用  
│││└淘宝、京东、各银行的商城。。。。  
││└传统web应用  
││　└论坛、博客、微博。。。。  
│├C/S  
││└数据库  
│├专门TCP/UDP服务  
││├QQ、IQC等IM后台  
││├各种金融交易的后台  
││└各种游戏的后台  
│└Client/Webserver  
│　└前端是浏览器、Win32桌面应用、手机应用  
└涉及技术  
　├网络设备、负载均衡、CDN等，但不用程序员操心  
　├SQL数据库（及其中间件，如连接池）  
　├NOSQL  
　├WebServer，基本不用程序员操心  
　├WebApp  
　│├php、asp、jsp。。。  
　│├基于tomcat/weblogic/...的XXXX框架的java应用  
　│└cgi、fastcgi、isapi应用  
　└C/C++/Java/Python/NodeJs/Php写服务端  

---


### 后端技术体系：

#### Web服务器(Tomcat，Nginx)
  - 浏览器请求解析、响应生成底层原理

  - 对底层接口的封装实现，Java中Servlet，Python中WSGI。
    - 请求和响应
    - 基本运行过程
    - 生命周期
    - 异步和同步运行区别
    - 会话和cookie状态管理，作用，区别
    - 过滤器中间件实现转码

    - 监听器实现会话统计，实时状态


#### 框架
- MVC框架，Java-Spring，Python-Django, flask, tornado
  - 替代了jsp作为view的作用，用于展现与用户交互的前端界面。

  - 集成后端Model持久层框架，数据库(mysql)及ORM框架，封装简化JDBC接口，处理真正的业务逻辑。

  - 底层Controller还是基于Servlet，分发前端各种请求到对应的业务逻辑进行处理。

  - 集成其他后端组件


#### 数据库
- 分页

- 索引

- 常用demo
  - 查询：
    "select * from table order by id desc limit ?,?"

- MySQL

- Redis

- 全文检索 elasticSearch


#### 分布式系统
- 分布式：一个业务分拆多个子业务，部署在不同的服务器上。

- 集群：同一个业务，部署在多个服务器上。

- 为什么要有分布式系统？
  - 冗余，不要把鸡蛋放在一个篮子里。
  - 可扩展性，横向水平扩展。

- 数据通信
  - 消息队列 RMQ，Kafka

  - RPC、RMI、RestFul

- 分布式缓存
  - redis缓存

- 分布式文件系统

- 微服务


#### 虚拟化 docker，kubernates


#### 安全


