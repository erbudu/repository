# v-bid
**vue解释**
>Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 v-bind 指令：
```html
    <div v-bind:id="dynamicId"></div>
```
>对于布尔 attribute (它们只要存在就意味着值为 true)，v-bind 工作起来略有不同，在这个例子中：
```html
    <button v-bind:disabled="isButtonDisabled">Button</button>
```
>如果 isButtonDisabled 的值是 null、undefined 或 false，则 disabled attribute 甚至不会被包含在渲染出来的 按钮 元素中。

------------------------------------------------------------------------------

在vue中，与具体的属性绑定用 **v-bind**指令，比如元素中的src、href、等等...
这时候我们可以用v-bind指令：
* 作用：动态绑定属性。（就是根据后台请求数据的值，决定该属性的属性值）
* 缩写： :
* 预期：any(with argument) Object (without argument)
* 参数： attrOrProp(optional)
示例：
```html
<div id="app">
    <pre><a v-bind:href="url">菜鸟教程</a></pre>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    url: 'http://www.runoob.com'
  }
})
</script>
```

## v-bind 动态绑定class

### 1.对象语法（:class="{css1:css1IsDisplay,css2:css2IsDisplay}"）
> v-bin绑定class的对象语法就是v-bind:class后边跟一个对象
  
*:class="{css1:css1IsDisplay,css2:css2IsDisplay}" css1表示样式，css1IsDisplay值为boolean，表示这个样式是否显示，true择显示，false则不显示*
```html
  </head>
<style>
    .active {
        color: red;
    }

</style>
<body>
<script src="../../lib/vue.js"></script>

<div id="app">
    <!--
      1、isActive的值为true，active样式会被添加到h2元素中
      2、v-bind绑定的class可以和普通的class同时存在，如title样式也会被加载到元素中，vue解析时会将动态绑定的calss和一般class合并
      3、在实际的使用中，一般固定的class样式我们会写在class中，对于有可能发生改变的样式我们用v-bind动态绑定。
      -->
    <h2 class="title" :class="{active:isActive}">{{message}}</h2>
      <!-- 要是calss里面样式太多的情况下也可以放在methods中 -->
     <h2 :class="getCalss()">{{message}}</h2>
</div>

<script>

    const app =  new Vue({
        el:"#app",
        data:{
            message:"hello world!",
            isActive:false
        },
        methods:{
          getCalss :function(){
            return {active:this.isActive};
          }
        }
    })
</script>
```

### 2.数组语法

```html
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>

        .active {
            color: red;
        }
        .active1 {
            color: darkblue;
        }
    </style>
</head>
<body>
<script src="../../lib/vue.js"></script>
<div id="app">
    <!--1-->
    <h2 :class="['active','line']">{{message}}</h2>
    <!--2-->
    <!--当数组中不用引号的时候，他在解析的时候会将把他当作变量来处理。-->
    <!--比如具体的样式可能时从服务器请求过来的。-->
    <h2 :class="[active,line]">{{message}}</h2>

</div>

<script>

    const app =  new Vue({
        el:"#app",
        data:{
            message:"hello world!",
            active:"active1",
            line:"line"
        },
        methods:{

        }
    })
</script>
```
