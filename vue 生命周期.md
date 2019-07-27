### vue 生命周期  
###### vue实例  
1. 每个vue应用都是通过 Vue 函数创建一个新的 Vue实例开始的；  
2. 当创建一个Vue实例时，你可以传入一个选项；  
```
var vm = new Vue ({
// 选项  
}) 
```  
选项指的是：  
（1）选项/数据：data，props，propsData，computed，methods，watch  
（2）选项/dom: el, template, render, renderError,   
（3）选项/生命周期钩子：beforeCreate, created, beforeMount, mounted, befroeUpdate, updated, activated, deactivated, beforeDestory, destroyed, errorCaptured  4
（4）选项/资源：directives, filters, components  
（5）选项/组合: parent, mixins, extends, provide/inject,  
（6）选项/其他: name, delimiters, functional, model, inheritAttrs, comments  
3. 一个Vue应用由一个通过new Vue 创建的根Vue实例，以及可以选的嵌套的、可复用的组件树组成；  
4. 当一个Vue实例被创建时，它将data 对象中的所有的属性加入到 vue 的响应式系统中。当这些属性的值发生改变时，视图将会产生‘响应’，即匹配更新为最新值；  
5. 每个 Vue 实例在被创建时都要经过一系列的初始化过程--例如，需要设置数据监听、编译模板、将实例挂载到DOM 并在数据变变化时更新DOM等。
同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会；  
6. 生命周期钩子的this上下文指向调用它的Vue实例；
#### 钩子函数  
```
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
beforeDestroy
destroyed
```  
运行以下代码  
```<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>
  <title>vue生命周期</title>
</head>

<body>
  <div id="app">
    <h1>{{message}}</h1>
  </div>
</body>
<script>
  var vm = new Vue({
    el: "#app",
    data: {
      message: 'Vue 的生命周期'
    },
    beforeCreate() {
      console.group('-------beforeCreate创建前状态--------');
      console.log("%c%s", "color: red", "el : " + this.$el);
      console.log("%c%s", "color: red", "message  : " + this.message);
      console.log("%c%s", "color: red", "data  :" + this.$data);
    },
    created() {
      console.group('-------Create创建完毕状态--------');
      console.log("%c%s", "color: red", "el : " + this.$el);
      console.log("%c%s", "color: red", "message  : " + this.message);
      console.log("%c%s", "color: red", "data  :" + this.$data);
    },
    beforeMount() {
      console.group('-------beforeMount挂载前的状态--------');
      console.log("%c%s", "color: red", "el : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color: red", "message  : " + this.message);
      console.log("%c%s", "color: red", "data  :" + this.$data);
    },
    mounted() {
      console.group('-------Mounted挂载后的状态--------');
      console.log("%c%s", "color: red", "el : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color: red", "message  : " + this.message);
      console.log("%c%s", "color: red", "data  :" + this.$data);
    },
    beforeUpdate: function () {
      console.group('beforeUpdate 更新前状态===============》');
      console.log("%c%s", "color:red", "el     : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:red", "data   : " + this.$data);
      console.log("%c%s", "color:red", "message: " + this.message);
    },
    updated: function () {
      console.group('updated 更新完成状态===============》');
      console.log("%c%s", "color:red", "el     : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:red", "data   : " + this.$data);
      console.log("%c%s", "color:red", "message: " + this.message);
    },
    beforeDestroy: function () {
      console.group('beforeDestroy 销毁前状态===============》');
      console.log("%c%s", "color:red", "el     : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:red", "data   : " + this.$data);
      console.log("%c%s", "color:red", "message: " + this.message);
    },
    destroyed: function () {
      console.group('destroyed 销毁完成状态===============》');
      console.log("%c%s", "color:red", "el     : " + this.$el);
      console.log(this.$el);
      console.log("%c%s", "color:red", "data   : " + this.$data);
      console.log("%c%s", "color:red", "message: " + this.message)
    }
  })

</script>

</html>
```
得到的结果如下:  


