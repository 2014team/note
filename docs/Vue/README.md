# 第一章核心

## Vue简介

Vue.js 是一个用于构建用户界面的渐进式 JavaScript 框架。

- 采用**组件化**模式，提高代码复用率，且让代码更好的维护。
- **声明式**编码，让编程人员直接操作DOM,提高开发效率。

**声明式编码的特点**

1. **关注结果**：声明式编程更关注结果而非过程。开发者定义期望的输出，框架或库负责实现细节。
2. **高层次抽象**：声明式代码通常比命令式代码更简洁和易读，因为它省略了许多低层次的实现细节。
3. **可维护性强**：由于高层次的抽象，声明式代码更易于理解和维护。

**声明式编码的例子**

**1. HTML**

HTML 是声明式编程的一个典型例子。你定义页面元素及其属性，而不需要描述如何绘制这些元素。

```
<div id="app">
  <p>{{ message }}</p>
</div>
```

在这个例子中，你声明了一个包含文本的 `<p>` 元素，而不需要详细描述如何在页面上绘制这个文本。

**声明式 vs 命令式**

**命令式编码示例**

```
let numbers = [1, 2, 3, 4, 5];
let doubled = [];
for (let i = 0; i < numbers.length; i++) {
  doubled.push(numbers[i] * 2);
}
```

在命令式编码中，你详细描述了如何通过遍历数组来创建一个新的数组。

**声明式编码示例**

```
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(n => n * 2);
```

在声明式编码中，你使用 `map` 函数声明了你想要将每个数字乘以 2 而不需要描述遍历数组的具体步骤。

**结论**

声明式编码的优势在于简化代码、提高可读性和维护性，使得开发者可以专注于描述问题的本质而不是解决问题的具体步骤。在现代前端开发中，诸如 Vue.js、React 等框架广泛使用声明式编码范式来简化 UI 开发。

## Vue基础

### Vue开发环境搭建

官网地址： https://cn.vuejs.org/

![image-20240725134202917](upload\image-20240725134202917.png)



开发工具

![image-20240725142146064](upload\image-20240725142146064.png)



![image-20240725142207322](upload\image-20240725142207322.png)

**解决**Download the Vue Devtools extension for a better development experience:
https://github.com/vuejs/vue-devtools

直接点击链接

或者

https://v2.cn.vuejs.org/v2/guide/installation.html

![image-20240725142507139](upload\image-20240725142507139.png)



![image-20240725142524455](upload\image-20240725142524455.png)



![image-20240725142629945](upload\image-20240725142629945.png)

![image-20240725142703964](upload\image-20240725142703964.png)

![image-20240725142739179](upload\image-20240725142739179.png)

![image-20240725142805191](upload\image-20240725142805191.png)



**解决**You are running Vue in development mode.
Make sure to turn on production mode when deploying for production.
See more tips at https://vuejs.org/guide/deployment.html

![image-20240725143450858](upload\image-20240725143450858.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>认识Vue</title>
    <script type="text/javascript"  src="../js/vue.js"></script>
</head>
<body>
<script  type="text/javascript" >
    Vue.config.productionTip = false // 设置为 false 以阻止 vue 在启动时生成生产提示。
</script>
</body>
</html>
```

初识Vue
1.加让Vue工作，就必须倒建一个Vue实例，且要传入一个配置对象
2.app容器型的代码依然符合htm1规范。只不过混入了一些特的Vue比法
3.app容器型的代码被称为【Vue模板】

### Hello小案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello word</title>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
<!--    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>-->
    <!-- 生产环境版本，优化了尺寸和速度 -->
<!--    <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>-->
    <script type="text/javascript"  src="../js/vue.js"></script>
</head>
<body>
<div id="app">
   {{name}}
</div>
<script  type="text/javascript" >
    /*数据对象*/
    var data = {
        name:'Hello Vue'
    }
    /*创建一个Vue实例*/
    const vm = new Vue({
        el: '#app',
        data: data
    })
</script>
</body>
</html>
```

### 模板语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>模板语法</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h1>插值语法</h1>
    <h3>你好，{{name}}</h3>
    <hr/>
    <h1>指令语法</h1>
    <a v-bind:href="school.url.toUpperCase()">点我去{{school.name}}学习1</a>
    <a :href="school.url">点我去{{school.name}}学习2</a>
</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    new Vue({
        el: '#root',
        data: {
            name: 'jack',
            school: {
                name: 'zhuzq',
                url: 'http://www.zhuzq.com'
            }
        }
    });
</script>
</html>
```

Vue模板语法有2大类:
**插值语法:**
功能:用于解析标签体内容。
写法:{{xxx}}，xxx是js表达式，且可以直接读取data中的所有属性。
**指令语法:**
功能:用于解析标签(包括:标签属性、标签体内容、绑定事件.....) 。  
 举例:v-bind:href="xxx”或 简写为 :href="xxx"，xxx同样要写js表达式，
且可以直接读取到data中的所有属性。
各注:Vue中有很多的指令，且形式都是:v-????，此处只是拿v-bind举个例子。

### 数据绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>数据绑定</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    单向数据绑定：<input type="text" v-bind:value="name"><br/><br/>
    双休数据绑定：<input type="text" v-model:value="name">

<!--    如下代码是错误的，因为v-model只能应用在表单类元素(输入类元素)-->
  <!--  <h2 v-bind:x="name">你好啊</h2>-->
</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    new Vue({
        el: '#root',
        data: {
            name: 'jack',
        }
    });
</script>
</html>
```

Vue中有2种数据绑定的方式:
**单向绑定(v-bind)**:数据只能从data流向页面。

**双向绑定(v-model)**:数据不仅能从data流向页面，还可以从页面流向data。

备注:
双向绑定一般都应用在表单类元素上(如:input、select等)

v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

### data与el的2种写法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>el与Data两种写法</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h1>{{name}}</h1>
</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    // const  vm = new Vue({
    //     // el: '#root',  // 第一种写法
    //
    //     // data 第一种写法 ：对象式
    //     data: {
    //         name: 'jack',
    //     }
    // });
    //
    // console.log(vm);
    // vm.$mount("#root")  // 第二种写法



    new Vue({
        el: '#root',
         //  data第二种写法：函数式
        data: function(){
            console.log('@@',this) // this对象是Vue实例对象
            return{
                name:'jack'
            }
        }
    });



</script>
</html>
```

el有2种写法

- new Vue时候配置e1属性。
- 先创建Vue实例，随后再通过vm.$mount('#root')指定e1的值。

data有2种写法

- 对象式
- 函数式

如何选择:目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

一个重要的原则:
由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了

### MVVM模型

M：模型（Model）对应data中的数据

V：视图（View）模板

VM：视图模型（ViewModel）Vue实例对象

![img](upload\webp)


data中所有的属性，最后都出现在了vm身上。
vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。

### Object.defineProperty

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Object中defineProperty</title>
</head>
<body>
</body>
<script type="text/javascript">

    let number = 20
    let person = {
        name:'张三',
        sex : '男'
    }

    Object.defineProperty(person,'age',{
        // value:18,
        // enumerable:true,//控制属性是否可以枚举，默认值是false
        // writable:true,// 控制属性是否被修改，默认值是false
        // configurable:true,// 控制属性是否被删除，默认值是false
        // 当有人读取person的age属性时，get函数就会被调用，且返回值就是age的值
        get(){
            console.log('有人读取age属性了')
            return number;
        },
        set(value){
            console.log('有人修改了age属性了，且值是',value)
            number = value
        }
    })
    console.log(person)



</script>
</html>
```

![image-20240729142303310](upload\image-20240729142303310.png)

### 数据代理理解

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>数据代理</title>
</head>
<body>
</body>

<!--数据代理：通过一个对象代理对另外一个对象中的属性操作（读/写）-->
<script type="text/javascript">

    let obj1 = {x:100}
    let obj2 = {y:200}

    Object.defineProperty(obj2,'x',{
        get(){
            return obj1.x;
        },
        set(value){
            obj1.x = value
        }
    })



</script>
</html>
```

![image-20240729144158790](upload\image-20240729144158790.png)

### Vue中的数据代理

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue中的数据代理</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h1>学校名称：{{name}}</h1>
    <h2>学校地址：{{address}}</h2>
</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
    let data = {
        name:'湖南大学',
        address:'湖南长沙市'
    }
    const vm = new Vue({
        el: '#root',
        data: data
    });



</script>
</html>
```

![image-20240729145740278](upload\image-20240729145740278.png)



**Vue中的数据代理:**
通过vm对象来代理data对象中属性的操作(读/写)

**Vue中数据代理的好处:**
更加方便的操作data中的数据
**基本原理:**
通过object.defineProperty()把data对象中所有属性添加到vm上。
为每一个添加到vm上的属性，都指定一个getter/setter。
在getter/setter内部去操作(读/号)data中对应的属性。

### 事件处理

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件处理</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
<div id="root">
    <h1>欢迎来到：{{name}} 学习</h1>
    <button v-on:click="showInfo" >点我提示信息</button><br/><br/>
    <button v-on:click="showInfo1($event,66)" >点我提示信息1</button><br/><br/>
    <button @click="showInfo" >点我提示信息2</button>
</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name:'http://www.zhuzq.com'
        },
        methods:{
            showInfo(event){
                console.log(event.target.innerText)
                console.log(this)
            },
            showInfo1(event,number){
                console.log(number)
            }
        }
    });



</script>
</html>
```

事件的基本使用:

- 使用v-on:xxx或@x绑定事件，其中xxx是事件名:
- 事件的回调需要配置在methods对象中，最终会在vm上;
- methods中配置的函数，不要用箭头函数!否则this就不是vm了;
- methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象;
- @click="demo"和 @click="demo($event)”效果一致，但后者可以传参;

### 事件修饰符

Vue中的事件修饰符:

- prevent:阳止默认事件(常用);
- stop:阳止事件冒泡(常用);
- once:事件只触发一次(常用);
- capture:使用事件的捕获模式:
- self:只有event.target是当前操作的元素是才触发事件:
- passive:事件的默认行为立即执行，无需等待事件回调执行完毕:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件修饰符</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
<style type="text/css">
    .demo{
        background-color: aquamarine;
        padding: 20px;
    }

    .box1{
        background-color: oldlace;
        padding: 20px;
    }

    .box2{
        background-color: orchid;
        padding: 20px;
    }

    .list{
        background-color: bisque;
        width: 200px;
        height: 200px;
        overflow: auto;
    }

    li{
        height: 100px;
    }

</style>


<div id="root">

       <!-- Vue中的事件修饰符:
        1.prevent:阳止默认事件(常用);
        2.stop:阳止事件冒泡(常用);
        3.once:事件只触发一次(常用);
        4.capture:使用事件的捕获模式:
        5.self:只有event.target是当前操作的元素是才触发事件:
        6.passive:事件的默认行为立即执行，无需等待事件回调执行完毕:-->

    <!--prevent-->
    <a href="http://www.baidu.com" @click.prevent="showInfo" >prevent事件修饰符</a><br/><br/>

    <!--stop-->
    <div class="demo" @click="showInfo">
        <button @click.stop="showInfo" >stop事件修饰符</button><br/><br/>
    </div>

    <!--once-->
    <button @click.once="showInfo" >once事件修饰符</button><br/><br/>


    <!--capture  冒泡由里向外  2 1  -->
    <div class="box1" @click="showMsg(1)">
        div1
        <div class="box2" @click="showMsg(2)"></div>
        div2
    </div>


    <!--self-->
    <div class="demo"  @click.self="selfMethod">
        <button @click="selfMethod" >selfMethod事件修饰符</button><br/><br/>
    </div>

  <!--  <ul @scroll.passive="scrollMethod" class="list">-->
    <ul @wheel.passive="scrollMethod" class="list">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>

    </ul>


</div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name:'http://www.zhuzq.com'
        },
        methods:{
            showInfo(event){
                alert('你好！')
            },
            showMsg(value){
                console.log(value)
            },
            selfMethod(e){
                console.log(e.target)
            },
            scrollMethod(){
                for(let i=0;i<10000; i++){
                    console.log('@')
                }
                console.log('加载完毕')
            }
        }
    });



</script>
</html>
```

### 键盘事件

Vue中常用的按键别名:

- 回车=>enter
- 删除 => delete(捕荻“删除”和“退格”键)
- 退出 =>esc
- 空格 =>space
- 换行 => tab
- 上=> up
- 下 => down
- 左 =>left
- 右=>right



vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case(短横线命名)

系统修饰键(用法特殊):ctrl、alt、shift、meta

配合keyup使用:按下修饰健的同时，再按下其他键，随后释放其他键，事件才被触发。

- 配合keydown使用:正常触发事件。
- 也可以使用keycode去指定具体的按键(不推荐)

Vue.config.keycodes.自定义键名 =键码，可以去定制按键别名

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>键盘事件</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>


   <!-- Vue中常用的按键别名:

    - 回车=>enter
    - 删除 => delete(捕荻“删除”和“退格”键)
    - 退出 =>esc
    - 空格 =>space
    - 换行 => tab
    - 上=> up
    - 下 => down
    - 左 =>left
    - 右=>right



    vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case(短横线命名)

    系统修饰键(用法特殊):ctrl、alt、shift、meta

    配合keyup使用:按下修饰健的同时，再按下其他键，随后释放其他键，事件才被触发。

    - 配合keydown使用:正常触发事件。
    - 也可以使用keycode去指定具体的按键(不推荐)

    Vue.config.keycodes.自定义键名 =键码，可以去定制按键别名-->



    <div id="root">
        <h1>欢迎来到：{{name}} 学习</h1>
        <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo"><br/><br/>
        <input type="text" placeholder="按下回车提示输入" @keyup.caps-lock="showInfo"><br/><br/>
        <input type="text" placeholder="按下回车提示输入" @keydown.ctrl="showInfo"><br/><br/>
        <input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo"><br/><br/>
    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    Vue.config.keyCodes.huiche = 13  // 定义一个别名按键

    const vm = new Vue({
        el: '#root',
        data: {
            name:'http://www.zhuzq.com'
        },
        methods:{
            showInfo(e){
             // if(e.keyCode != 13){
             //    return;
             // }

                console.log(e.keyCode)
                // console.log(e.target.value)
            }
        }

    });


</script>
</html>
```

### 计算属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>计算属性——姓名案例</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        姓：<input type="text" v-model="firstName"><br/><br/>
        名：<input type="text" v-model="lastName"><br/><br/>
        姓名：<span>{{fullName()}}</span><br/><br/>

        姓名：<span>{{fullNameByComputed}}</span>

    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            firstName:'张',
            lastName:'三'
        },
        methods:{
            fullName(){
                return this.firstName+'-'+this.lastName
            }
        },
        computed:{
            fullNameByComputed:{
                get(){
                    console.log('get被调用了')
                    return this.firstName+'-'+this.lastName
                },
                set(value){
                    debugger
                    console.log('set',value)
                    let  arr = value.splice("-");
                    this.firstName = arr[0]
                    this.lastName = arr[1]
                }
            }
        }
    });


</script>
</html>
```

### 计算属性-简写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>计算属性简写——姓名案例</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        姓：<input type="text" v-model="firstName"><br/><br/>
        名：<input type="text" v-model="lastName"><br/><br/>
        姓名：<span>{{fullName}}</span><br/><br/>


    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            firstName:'张',
            lastName:'三'
        },

        computed:{
            fullName(){
                console.log('get被调用了')
                return this.firstName+'-'+this.lastName
            }
        }
    });


</script>
</html>
```

### 天气案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>天气案例</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button>

    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            isHot:true,
        },
        computed:{
            info(){
               return this.isHot ? '炎热' :'凉爽'
            }
        },
        methods:{
            changeWeather(){
                this.isHot =  !this.isHot
            }
        }
    });


</script>
</html>
```

### 监视属性

监视屈性watch:
当被监视的属性变化时，回调函数自动调用，进行相关操作

监视的属性必须存在，才能进行监视!!

监视的两种写法:
new Vue时传入watch配置
通过vm.$watch监视

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>监视属性</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button>

    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            isHot:true,
        },
        computed:{
            info(){
               return this.isHot ? '炎热' :'凉爽'
            }
        },
        methods:{
            changeWeather(){
                this.isHot =  !this.isHot
            }
        },
        // watch:{
        //     isHot:{
        //         immediate:true,// 初始化的时候调用一下handler
        //         handler(newValue,oldValue){
        //             // 当isHost发送改变时候调用一下
        //             console.log('isHost修改了',newValue,oldValue)
        //         }
        //     }
        // }
    });

    vm.$watch('isHot',{
                immediate:true,// 初始化的时候调用一下handler
                handler(newValue,oldValue){
                    // 当isHost发送改变时候调用一下
                    console.log('isHost修改了',newValue,oldValue)
                }
    });



</script>
</html>
```





## Vue-cli



## Vue-router



## Vuex



## element-ui



## vue3