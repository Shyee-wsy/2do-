## 使用 axios 访问 API  
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
