
<!-- vim-markdown-toc GFM -->

- [OSI 模型](#osi-模型)
- [通信协议](#通信协议)
  - [TCP和UDP](#tcp和udp)
  - [HTTP](#http)

<!-- vim-markdown-toc -->


### OSI 模型
- 应用
- 传输
- 网络
- 数据链路
- 物理


### 通信协议
#### TCP和UDP


#### HTTP
- [**浏览器请求到生成页面的过程**](https://github.com/biaochenxuying/blog/issues/3)

  1. 浏览器向服务器发送一个请求，请求包括：
     - 方法：GET 还是 POST，GET 仅请求资源，POST 会附带用户数据(表单等)。
     - URL 地址：其中包括域名与资源路径。
     - 如果方法是 POST，请求还包括一个 Body，包含用户数据。
     - 其他相关的 Header。

  2. 域名解析系统 DNS 对域名进行解析，获得服务器 IP 地址，请求 TCP 连接。

  3. 服务器接收到客户端请求，进行三次握手，成功则建立连接，返回 HTTP 响应，响应包括。
     - 响应码：如 200 表示成功，3xx 表示重定向，4xx 表示客户端发送请求有错误，5xx 表示服务器处理错误。
     - 响应类型：由 **Content-Type** 决定，表示响应类型是 HTML 文本、js 脚本、图片、视频还是音乐。
     - 其他相关的 Header。
     - Body，响应的内容。

-   会话、cookie


