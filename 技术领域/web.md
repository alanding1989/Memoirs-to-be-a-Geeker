


#### 浏览器请求到生成页面的过程
1. 浏览器向服务器发送一个请求，请求包括：
- 方法：GET还是POST，GET仅请求资源，POST会附带用户数据(表单等)。
- URL地址：其中包括域名与资源路径。
- 如果方法是POST，请求还包括一个Body，包含用户数据。
- 其他相关的Header。

2. 域名解析系统DNS对域名进行解析，获得服务器IP地址，请求TCP连接。

3. 服务器接收到客户端请求，进行三次握手，成功则建立连接，返回HTTP响应，响应包括。
- 响应码　： 如200表示成功，3xx表示重定向，4xx表示客户端发送请求有错误，5xx表示服务器处理发生错误。
- 响应类型： 由 **Content-Type** 决定，表示响应类型是HTML文本、js脚本、图片、视频还是音乐。
- 其他相关的Header。
- Body，响应的内容。


#### 前端：　　
HTTP/TCP/UDP、会话、cookie
Web基础（HTML/CSS/JS/ES6/Ajax/jQuery)、
Bootstrap框架


#### 后端：
- Web服务器(Tomcat，Ningx)、

- 浏览器请求解析、响应生成底层原理

- 对底层的接口封装实现，Java中Servlet，Python中WSGI。
  - 请求和响应
  - 基本运行过程
  - 生命周期
  - 异步和同步运行区别
  - 会话和cookie状态管理，作用，区别
  - 过滤器中间件实现转码
  - 监听器实现会话统计，实时状态

- MVC框架，Java-Spring，Python-Django, flask, tornado
  - 替代了jsp作为view的作用
  - 集成后端持久层框架，数据库(mysql)及ORM框架，封装简化JDBC接口
  - 集成其他后端组件

- redis缓存

- 消息队列 RMQ，Kafka
- 分布式、分布式文件系统、RPC、微服务
- 虚拟化 docker，kubernates
- 搜索引擎 elasticSearch
- 安全
