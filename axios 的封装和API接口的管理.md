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
  试想，每次调用接口，都要写一遍'http://www.baidu.com',要是接口发生变化，我们得一个一个去修改，这会让代码看起来繁琐并且难以维护，所以我们需要对axios进行封装，在同一位置管理我们的接口，调用的时候只需传相应的接口函数即可。比如我们对axios的get、post、put、delete方法进行封装，在具体使用的页面只需调用接口函数以及传入params即可，其余例如 url，header我们应该进行封装，以上的代码就会变成  
  ```
  API.getData({id: '01'}).then(resp => {})
  ```
  ### 实现思路  
  1. 新建一个文件apis.js，封装代码写于此处；  
  2. 在main.js 内引用以上文件，配置全局变量；  
  3. 在具体使用的地方使用；   
  ### 具体实现步骤  
  1. 
