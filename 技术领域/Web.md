
<!-- vim-markdown-toc GFM -->

- [Web 备忘录](#web-备忘录)
  - [业务状况分类](#业务状况分类)
  - [网络及前端基础：](#网络及前端基础)
  - [后端技术体系：](#后端技术体系)
  - [数据库](#数据库)

<!-- vim-markdown-toc -->


### Web 备忘录

---


#### 业务状况分类

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


#### 网络及前端基础：
- OSI模型，通信协议(HTTP/TCP/UDP)
  - **浏览器请求到生成页面的过程**
    1. 浏览器向服务器发送一个请求，请求包括：  
        - 方法：GET还是POST，GET仅请求资源，POST会附带用户数据(表单等)。
        - URL地址：其中包括域名与资源路径。
        - 如果方法是POST，请求还包括一个Body，包含用户数据。

        - 其他相关的Header。

    2. 域名解析系统DNS对域名进行解析，获得服务器IP地址，请求TCP连接。

    3. 服务器接收到客户端请求，进行三次握手，成功则建立连接，返回HTTP响应，响应包括。
        - 响应码：如200表示成功，3xx表示重定向，4xx表示客户端发送请求有错误，5xx表示服务器处理错误。
        - 响应类型：由 **Content-Type** 决定，表示响应类型是HTML文本、js脚本、图片、视频还是音乐。
        - 其他相关的Header。

        - Body，响应的内容。

  - 会话、cookie

- 前端基础（HTML/CSS/JS/ES6/Ajax/jQuery)

- 框架
  - Bootstrap

---


#### 后端技术体系：
- Web服务器(Tomcat，Nginx)、

  - 浏览器请求解析、响应生成底层原理

  - 对底层接口的封装实现，Java中Servlet，Python中WSGI。
    - 请求和响应
    - 基本运行过程
    - 生命周期
    - 异步和同步运行区别
    - 会话和cookie状态管理，作用，区别
    - 过滤器中间件实现转码

    - 监听器实现会话统计，实时状态

- MVC框架，Java-Spring，Python-Django, flask, tornado
  - 替代了jsp作为view的作用，用于展现与用户交互的前端界面。
  - 集成后端Model持久层框架，数据库(mysql)及ORM框架，封装简化JDBC接口，处理真正的业务逻辑。
  - 底层Controller还是基于Servlet，分发前端各种请求到对应的业务逻辑进行处理。

  - 集成其他后端组件

- redis缓存

- 消息队列 RMQ，Kafka

- 分布式、分布式文件系统、RPC、微服务

- 虚拟化 docker，kubernates

- 搜索引擎 elasticSearch

- 安全


#### 数据库
- 分页

- 索引

- 常用demo
  - 查询：
    "select * from table order by id desc limit ?,?"

