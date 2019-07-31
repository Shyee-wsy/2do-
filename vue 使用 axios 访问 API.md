## 使用 axios 访问 API    
### 为什么实用axios？    
1. 使用axios的拦截器可以统一做请求拦截和响应拦截；比如请求拦截可以在发送请求之前进行登录等操作，响应拦截可以对响应信息进行处理，判断状态码，从而弹出报错信息等等；  
2. 可以设定请求超时的时间  
3. 基于promise，可以很方便地使用then或者catch处理响应信息；  
4. 自动转换JSON数据，即在发送请求之前，先将js对象转换成JSON字符串，相当于使用JSON.stringgify（obj）；请求成功之后，将后端返回的JSON字符串转换成js对象，相当于默认使用JSON.parse(str)方法；
### 如何使用？  

1. 安装 axios  
``` 
npm install axios  
```
2. 在 mounted 生命周期钩子函数中获取数据  
```
mounted () {
  axios
    .get('http://192.168.188.45:5000/get_todo')
    .then(response => (this.info = response))
    .catch(error => console.log(error))
}
```
3. 得到的数据如下:  
```
{ 
  "data": [], 
  "status": 200, 
  "statusText": "OK", 
  "headers": { "content-type": "application/json" }, 
  "config": { "url": "http://192.168.188.45:5000/get_todo", 
  "method": "get", 
  "headers": { "Accept": "application/json, text/plain, */*" }, 
  "transformRequest": [ null ], "transformResponse": [ null ], 
  "timeout": 0, 
  "xsrfCookieName": "XSRF-TOKEN", 
  "xsrfHeaderName": "X-XSRF-TOKEN", 
  "maxContentLength": -1 }, 
  "request": {} 
} 

```
其中，"data" 中存放需要的数据；
参考文献：https://cn.vuejs.org/v2/cookbook/using-axios-to-consume-apis.html#%E6%9B%BF%E4%BB%A3%E6%96%B9%E6%A1%88
