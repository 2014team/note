## Vue-cli

### 创建脚手架

**说明**

Vue脚手架是Vue官网提供的标准开发工具（开发平台）

文档: https://cli.vuejs.org/zh/

![image-20240808141652090](upload\image-20240808141652090.png)

![image-20240808141713873](upload\image-20240808141713873.png)



![image-20240808141734840](upload\image-20240808141734840.png)

**具体步骤**

设置镜像，下载缓慢请配置 npm 淘宝镜像

详细配置https://npmmirror.com/

**前提**

npm config set registry https://registry.npmmirror.com

![image-20240808141835840](upload\image-20240808141835840.png)

**第一步(仅第一次执行):全局安装@vue/cli**
npm install -g @vue/cli

![image-20240808141855666](upload\image-20240808141855666.png)

**第二步:切换到你要创建项目的目录，然后使用命令创建项目**
vue create 项目名称

示例：

![image-20240808141950464](upload\image-20240808141950464.png)

**第三步:启动项目**
npm run serve

![image-20240808142426250](upload\image-20240808142426250.png)

浏览器访问http://localhost:8080/

备注:
1.如出现下载缓慢请配置 npm 淘宝镜像

npm config set registry https://registry.npmmirror.com

2.Vue 脚手架隐藏了所有 webpack相关的配置，若想查看具体的 webpakc 配查，请执
行:vue inspect > output.js

### 脚手架文件结构

|——node_modules

|——public

​          |——favicon.ico：页签图标

​          |——index.html：主页面

|——src

​          |——assets：存放静态资源

​					|——logo.png

​          |——components：存放组件

​					|——HelloWorld.vue

​          |——App.vue：汇总所有组件

​          |——main.js：入口文件

|——.gitignore：git版本管制忽略的配置

|——babel.config.js：babel的配置文件

|——jsconfig.json：配置JavaScript项目文件

|——package.json：应用包配置文件

|——package-lock.json：包版本控制文件

|——vue.config.js： 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载

|——README.md：应用描述文件



**vue.config.js**

使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
使用vue.config.js可以对脚手架进行个性化定制，详情见:https://cli.vuejs.org/zh

### ref属性

1.被用来给元素或子组件注册引用信息(id的替代者)
2.应用在htm1标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象(vc)
3.使用方式:
	打标识:<h1 ref="xxx">.....</h1>或<School ref="xxx"></School>
	获取:this.$refs.xxx

![image-20240809142859236](upload\image-20240809142859236.png)



### props配置

功能:让组件接收外部传过来的数据
**(1).传递数据:**
<Demo name="xxx"/>
**(2).接收数据:**
第一种方式(只接收):
props:['name"]
第二种方式(限制类型):
props:{
name:Number
第三种方式(限制类型、限制必要性、指定默认值):
props:{
 	 name:{
	  type:string，//类型
	  required:true，//必要性
 	 default:'老王’//默认值

​	}

}

备注:
props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

App.vue

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <h1 v-text="msg" ref="title"></h1>

    <!--age="20"：age的值字符串   :age="20"  age的值是数字类型-->
   <!-- <TestStudent name="张三" sex="男" age="20"/>-->
    <TestStudent name="张三" sex="男" :age="20"/>
    <TestStudent name="张三" sex="男" />

    <!--
    如果name属性没有的话，前端报如下错误
    vue.runtime.esm.js?c320:4625 [Vue warn]: Missing required prop: "name"

    found in

    -&ndash;&gt; <TestStudent> at src/components/TestStudent.vue
    <App> at src/App.vue
      <Root>-->
    <!--<TestStudent  sex="男" :age="20"/>-->
  </div>
</template>
<script>

import TestStudent from './components/TestStudent.vue'

export default {
  name: 'App',
  components: {
    TestStudent,
  },
  data(){
    return {
      msg:'欢迎学习Vue'
    }
  },
  methods:{

  }
}
</script>



```

TestStudent.vue

```vue
<template>
    <div class="demo">
        <h1 v-text="msg"></h1>
        <h2>学生姓名：{{name}}</h2>
        <h2>学生性别：{{sex}}</h2>
        <h2>学生年龄：{{myAge}}</h2>

        <button @click="updateAge">尝试修改接收到的年龄</button>
    </div>

</template>

<script>
    export default {
        name:'TestStudent',
        data() {
            return {
                msg: '我是一个学生',
                myAge:this.age,
            }
        },
        methods:{
            updateAge(){
                this.myAge ++
            }
        },
        // props:['name','sex','age'] // 简单声明接收

        // 接受同时对数据类型限制
        // props:{
        //     name:String,
        //     sex:String,
        //     age:Number
        // }

        //接收的同时对数据:进行类型限制+默认值的指定+必要性的限制

        props:{
            name:{
                type:String, // 字符串类型
                required:true, // 必须字段
            },
            age:{
                type:Number, // 数字类型
                default:99, // 默认值
            }
            ,
            sex:{
                type:String, // 字符串类型
                required:true, // 必须字段
            }
        }

    }

</script>

<style>
    .demo{
        background-color: antiquewhite;
    }

</style>
```

![image-20240809152730962](upload\image-20240809152730962.png)

### mixin混入

功能:可以把多个组件共用的配置提取成一个混入对象使用方式:
第一步定义混合，例如:
{
data(){....},
methods:{....}
}

第二步使用混入，例如:
(1).全局混入:Vue.mixin(xxx)
(2).局部混入:mixins:['xxx']



![](upload\image-20240809163252564.png)

mixin.js

```js
 export const hunhe = {
   methods:{
      showName(){
         alert(this.name)
      }
   },
    mounted(){
      console.log('你好啊！')
    },
}

 export const hunhe2 = {
     data(){
         return {
             x:100,
             y:200
         }
     },


 }
```

main.js

```js
//引入Vue
import Vue from 'vue'
//引入App组件，它是所有组件的父组件
import App from './App.vue'
//关闭vue的生产提示
Vue.config.productionTip = false


import {hunhe,hunhe2} from './mixin'

Vue.mixin(hunhe)
Vue.mixin(hunhe2)


//创建Vue实例对象---vm
new Vue({
  //将App组件放入容器中
  render: h => h(App),
}).$mount('#app')

```

TestSchool.vue

```vue
<template>
    <div class="demo">
        <h2 @click="showName">学校名称：{{name}}</h2>
        <h2>学校地址：{{address}}</h2>
    </div>

</template>

<script>

    // import {hunhe,hunhe2} from '../mixin'

    export default {
        name:'TestSchool',
        data() {
            return {
                name:'湖南大学',
                address:'广东深圳市',
                x:999
            }
        },
        // methods:{
        //     showName(){
        //         alert(this.name)
        //     }
        // },
        // mixins:[hunhe,hunhe2],
        mounted(){
            console.log('你好啊!!!!!!!!!!!！')
        },
    }

</script>

<style>
    .demo{
        background-color: antiquewhite;
    }

</style>
```

### 插件

1. 功能：用于增强Vue

2. 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

3. 定义插件：

   ```
   对象.install = function (Vue, options) {
       // 1. 添加全局过滤器
       Vue.filter(....)
   
       // 2. 添加全局指令
       Vue.directive(....)
   
       // 3. 配置全局混入(合)
       Vue.mixin(....)
   
       // 4. 添加实例方法
       Vue.prototype.$myMethod = function () {...}
       Vue.prototype.$myProperty = xxxx
   }
   ```

   

4. 使用插件：`Vue.use()`

### scoperd样式

查看插件版本

```
npm view 插件名称 versions
```

示例：

```
npm view less-loader versions
```

根据版本安装插件

```
npm i 插件名称@版本号
```

示例

```
npm i less-loader@8
```

1. 作用：让样式在局部生效，防止冲突。
   2. 写法：`<style scoped>`

### 总结TodoList案例

1. 组件化编码流程：

    (1).拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。

    (2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

    1).一个组件在用：放在组件自身即可。

    2). 一些组件在用：放在他们共同的父组件上（状态提升）。

    (3).实现交互：从绑定事件开始。

2. props适用于：

    (1).父组件 ==> 子组件 通信

    (2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！

4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。

### webStorage

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。

3. 相关API：

   1. `xxxxxStorage.setItem('key', 'value');` 该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

   2. `xxxxxStorage.getItem('person');`

       该方法接受一个键名作为参数，返回键名对应的值。

   3. `xxxxxStorage.removeItem('key');`

       该方法接受一个键名作为参数，并把该键名从存储中删除。

   4. ` xxxxxStorage.clear()`

       该方法会清空存储中的所有数据。

4. 备注：

   1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。
   2. LocalStorage存储的内容，需要手动清除才会消失。
   3. `xxxxxStorage.getItem(xxx)`如果xxx对应的value获取不到，那么getItem的返回值是null。
   4. `JSON.parse(null)`的结果依然是null。

### 组件的自定义事件

1. 一种组件间通信的方式，适用于：**子组件 ===> 父组件**

2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（事件的回调在A中）。

3. 绑定自定义事件：

   1. 第一种方式，在父组件中：`` 或 ``

   2. 第二种方式，在父组件中：

      ```
      <Demo ref="demo"/>
      ......
      mounted(){
         this.$refs.xxx.$on('atguigu',this.test)
      }
      ```

      

   3. 若想让自定义事件只能触发一次，可以使用`once`修饰符，或`$once`方法。

4. 触发自定义事件：`this.$emit('atguigu',数据)`

5. 解绑自定义事件`this.$off('atguigu')`

6. 组件上也可以绑定原生DOM事件，需要使用`native`修饰符。

7. 注意：通过`this.$refs.xxx.$on('atguigu',回调)`绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题！

### 全局事件总线（GlobalEventBis）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 安装全局事件总线：

   ```
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

   

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身。

      ```
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

      

   2. 提供数据：`this.$bus.$emit('xxxx',数据)`

4. 最好在beforeDestroy钩子中，用$off去解绑当前组件所用到的事件。

### 消息定于与发布（pubsub）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 使用步骤：

   1. 安装pubsub：`npm i pubsub-js`

   2. 引入: `import pubsub from 'pubsub-js'`

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

      ```
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

      

   4. 提供数据：`pubsub.publish('xxx',数据)`

   5. 最好在beforeDestroy钩子中，用`PubSub.unsubscribe(pid)`去取消订阅。

### nextTick

1. 语法：`this.$nextTick(回调函数)`
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行

### Vue封装的过度与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

2. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

   2. 使用``包裹要过度的元素，并配置name属性,注意如果配置了appear属性的话就代表一开始挂载真实dom的时候就开启动画的效果：

      ```
      <transition name="hello" appear>
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

      

   3. 备注：若有多个元素需要过度，则需要使用：<transition-group>，且每个元素都要指定`key`值。

第三方插件

https://animate.style/



