### Http 头部信息  
  http的头域包括（1）通用头、（2）请求头、（3）响应头 和 （4）实体头四个部分， 请求头包含请求的方法、URI、协议版本、以及包含请求修饰符、客户信息和内容的类似于MIME 的消息结构。服务器以一个状态行作为响应，相应的内容包括消息协议的版本，成功或者错误编码加上包含服务器信息、实体元信息以及可能的实体内容。  
  格式： 域名：域值  
  1. HTTP 通用头  
  通用头是客户端和服务器端都可以使用的头部，可以在客户端、服务器端和其他应用程序之间提供一些非常有用的通用功能，如Date头部；  
  
  2. HTTP请求头  
  请求头部是请求报文持有的，它们为服务器提供一些额外的信息，比如客户端希望接受什么类型的数据，如Accept头部；
  ```
  Accept: 浏览器能够处理的内容类型；
  Accept-Charset: 浏览器能够显示的字符集；
  Accept-Encoding: 浏览器能够处理的压缩编码；
  Accept-Language： 浏览器当前设置的语言；
  Connection: 浏览器与服务器之间连接的类型；
  Cookie: 当前页面设置的任何Cookie；
  Host: 发送请求的页面所在的域；
  Referer: 发送请求的页面URI.(注：正确拼写为： referrer)
  ```
  不同浏览器实际发送的头部信息会有所不同，但以上列出的基本上所有浏览器都会发送的；使用 setRequestHeader()方法可以设置自定义的请求头部信息；  
  
  3. 响应头部信息   
  响应头部便于客户端提供信息，比如，客户端在与哪种类型的服务器进行交互，如Server头部；
  例子：
  ```
  {
   "data": [], 
   "status": 200, 
   "statusText": "OK", 
   "headers": { "content-type": "application/json" }, 
   "config": { "url": "http://192.168.188.45:5000/get_todo",
   "method": "get",
   "headers": { "Accept": "application/json, text/plain, */*" },
   "transformRequest": [ null ], 
   "transformResponse": [ null ],
   "timeout": 0, 
   "xsrfCookieName": "XSRF-TOKEN", 
   "xsrfHeaderName": "X-XSRF-TOKEN", 
   "maxContentLength": -1 }, 
   "request": {} 
  }
  ```  
  4. 实体头部  
  实体头部指的是用于应对实体主体部分的头部，比如，可以用实体头部来说明实体主体部分的数据结构，如Content-type头部；    
  
  参考文章： https://www.cnblogs.com/onepixel/articles/7545959.html  
  
