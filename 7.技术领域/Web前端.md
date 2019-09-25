
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
  - CSS Bootstrap
  - UI Vue React Angular

---


