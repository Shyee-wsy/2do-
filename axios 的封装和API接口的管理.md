### 目的  
第一次使用axios，按照 Vue 文档上面的使用方法，在每个调用接口的地方都使用如下代码：  
```
getData(){
  axios
    .get("http://wwww.baidu.com:5000/xxx",{
    id: this.id,
    ...
    })
    .then(response => console.log(response)
    .catch(error => console.log(error)
    }
  }
  ```  
  试想，每次调用接口，都要写一遍url， 要是接口发生变化，我们得一个一个去修改，这会让代码看起来繁琐并且难以维护，所以我们需要对axios进行封装，在同一位置管理我们的接口，调用的时候只需传相应的接口函数即可。比如我们对axios的get、post、put、delete方法进行封装，在具体使用的页面只需调用接口函数以及传入params即可，其余例如 url，header我们应该进行封装，以上的代码就会变成  
  ```
  API.getData({id: '01'}).then(resp => {})
  ```
  ### 实现思路  
  1. 新建一个文件apis.js，封装代码写于此处；  
  2. 在main.js 内引用以上文件，配置全局变量；  
  3. 在具体使用的地方使用；   
  ### 封装要点  
  在src目录中，新建一个文件夹，然后在里面新建一个apis.js 文件  
  1. 引入  
  ```
  import axios from 'axios'; // 引入axios  
  ```
  2. 项目环境的切换  
  项目环境可能有三种情况: 开发环境、测试环境和生产环境。我们通过设置node的环境变量来匹配默认的接口url前缀。axios.default.baseURL可以设置axios的默认请求地址；  
  ```
  //环境切换  
  if(process.env.NODE_ENV == 'development'){
      axios.default.baseURL = 'https://www.development.com';
   }
   else if(process.env.NODE_ENV == 'debug'){
      axios.default.baseURL = 'https://www.debug.com';
   }
   else if(process.env.NODE_ENV == 'production'){
      axios.default.baseURL = 'https://www.production.com';
   }
   // 设置axios的默认请求地址(自己写项目练习的时候可只写下面这句代码，配置默认请求地址，不用配置环境切换的情况)  
   axios.default.baseURL = 'http://www.xxx';
   ```
  3. 设置请求超时  
  通过axios.default.timeout 设置默认的请求时间。例如超过了10秒，就会告知用户请求超时，请刷新等。  
  ```
  axios.default.timeout = 10000; 
  ```
  4.  请求拦截  
  有时我们在发送请求之前会进行一个请求拦截，希望在请求之前需完成一些操作。比如有一些请求是需要用户登录之后才能访问的，或者post请求的时候，我们需要序列化我们的操作，所以我们会在请求被发送之前进行一个拦截，从而进行我们想要的操作。  
  ```
  // 添加请求拦截器
  axios.interceptors.request.use(
  // 在发送请求之前做些什么
    config =>{
      config.data => JSON.stringify(config.data);
      config.headers = {
        'Content-type':'application/x-www-form-urlencoded'
      }
      return config;
    },
    error => {
      return Promise.reject(err);
    }
  );
  ```
  5. 响应的拦截 （异常处理） 
  ```
  axios.interceptors.response.use(response => {
    return response
}, err => {
    if (err && err.response) {
      switch (err.response.status) {
        case 400:
            console.log('错误请求')
          break;
        case 401:
            console.log('未授权，请重新登录')
          break;
        case 403:
          console.log('拒绝访问')
          break;
        case 404:
          console.log('请求错误,未找到该资源')
          break;
        case 405:
          console.log('请求方法未允许')
          break;
        case 408:
          console.log('请求超时')
          break;
        case 500:
          console.log('服务器端出错')
          break;
        case 501:
          console.log('网络未实现')
          break;
        case 502:
          console.log('网络错误')
          break;
        case 503:
          console.log('服务不可用')
          break;
        case 504:
          console.log('网络超时')
          break;
        case 505:
          console.log('http版本不支持该请求')
          break;
        default:
          console.log(`连接错误${err.response.status}`)
      }
    } else {
      console.log('连接到服务器失败')
    }
    return Promise.resolve(err.response)
})  
```
6. 封装get，post，delete和put方法  
封装get方法
```
export function get(url, params) {
  return new Promise((resolve, reject) => {
    axios.get(url,{
      params: params
    })
    .then(response =>{
      resolve(response.data);
     })
     .catch(error => {
        reject(error)
     })
   })
 }
 ```
 封装post请求 
 ```
 export function post(url, data) {
    return new Promise((resolve, reject) => {
      axios.post(url, data)
          .then(response => {
             resolve(response.data);
          }
          .catch(error => {
              reject(error.data)
          })
       });
    }
    ```
    axios.get() 方法和axios.post() 在提交数据时参数的书写方式是有区别的。get的第二个参数是一个{}，然后这个对象的params属性
    值是一个参数对象的。而post的第二个参数就是一个参数对象。  
 封装put请求  
 ```
 export function put(url, data){
    return new Promise((resolve, reject) => {
      axios.put(url, data)
        .then(response => {
            resolve(response.data);
         }, err => {
            reject(err)
         })
     })
   }
   
  7. 最后是获取数据的接口  
  ``` 
  export const server = {
      getData: function(params){
          return get('/get_data', paramObj);
      }
  }
  ```
  8. 在main.js 中引用以上apis.js文件，并定义全局变量  
  ```
  import { server } from './apis'
  Vue.prototype.$server = server;
  ```
  9. 最后，在需要调用接口的地方使用  
  ```
  methods: {
    getData: function(){
      let paramObj = { id: '123' }
      this.$server.getData(paramObj).then(data => { console.log(data) })
    }
  }
  ```
  参考地址： https://www.jianshu.com/p/9077baa9d543  
  https://juejin.im/post/5b55c118f265da0f6f1aa354
  Axios 中文说明： https://www.kancloud.cn/yunye/axios/234845
  
  
  
  
  
  
  
