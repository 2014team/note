





# Vue

## Vue简介

Vue.js 是一个用于构建用户界面的渐进式 JavaScript 框架。

- 采用**组件化**模式，提高代码复用率，且让代码更好的维护。
- **声明式**编码，让编程人员直接操作DOM,提高开发效率。

### **声明式编码的特点**

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

### 声明式 vs 命令式

#### 命令式编码示例

```
let numbers = [1, 2, 3, 4, 5];
let doubled = [];
for (let i = 0; i < numbers.length; i++) {
  doubled.push(numbers[i] * 2);
}
```

在命令式编码中，你详细描述了如何通过遍历数组来创建一个新的数组。

#### 声明式编码示例

```
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(n => n * 2);
```

在声明式编码中，你使用 `map` 函数声明了你想要将每个数字乘以 2 而不需要描述遍历数组的具体步骤。

### 结论

声明式编码的优势在于简化代码、提高可读性和维护性，使得开发者可以专注于描述问题的本质而不是解决问题的具体步骤。在现代前端开发中，诸如 Vue.js、React 等框架广泛使用声明式编码范式来简化 UI 开发。

## Vue开发环境搭建

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

## Hello world 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello word</title>
    <script type="text/javascript"  src="../js/vue.js"></script>
</head>
<body>
<div id="app">
   {{name}}
</div>
<script  type="text/javascript" >
    /*数据对象*/
    var data = {
        name:'Hello word'
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

## 数据与方法

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

```
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的 property
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置 property 也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3
```

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时就已经存在于 `data` 中的 property 才是**响应式**的。也就是说如果你添加一个新的 property，比如：

```javascript
vm.b = 'hi'
```

这里唯一的例外是使用 `Object.freeze()`，这会阻止修改现有的 property，也意味着响应系统无法再*追踪*变化。

```javascript
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})
<div id="app">
  <p>{{ foo }}</p>
  <!-- 这里的 `foo` 不会更新！ -->
  <button v-on:click="foo = 'baz'">Change it</button>
</div>
```

## 模板语法

#### [文本](https://v2.cn.vuejs.org/v2/guide/syntax.html#文本)

```html
<span>Message: {{ msg }}</span>
```

#### [v-once 指令](https://v2.cn.vuejs.org/v2/api/#v-once)

通过使用 [v-once 指令](https://v2.cn.vuejs.org/v2/api/#v-once)，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。

```html
<span v-once>这个将不会改变: {{ msg }}</span>
```

#### [`v-html`](https://v2.cn.vuejs.org/v2/api/#v-html)

```
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

#### [Attribute](https://v2.cn.vuejs.org/v2/guide/syntax.html#Attribute)

 [`v-bind` 指令](https://v2.cn.vuejs.org/v2/api/#v-bind)

```
<div v-bind:id="dynamicId"></div>
```

于布尔 attribute (它们只要存在就意味着值为 `true`)，`v-bind` 工作起来略有不同，在这个例子中：

```
<button v-bind:disabled="isButtonDisabled">Button</button>
```

如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` attribute 甚至不会被包含在渲染出来的<button> 元素中。

#### [使用 JavaScript 表达式](https://v2.cn.vuejs.org/v2/guide/syntax.html#使用-JavaScript-表达式)

<div v-bind:id="'list-' + id"></div>

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```

#### [指令](https://v2.cn.vuejs.org/v2/guide/syntax.html#指令)

##### v-if

```
<p v-if="seen">现在你看到我了</p>
```

这里，`v-if` 指令将根据表达式 `seen` 的值的真假来插入/移除 <p> 元素。

#### [参数](https://v2.cn.vuejs.org/v2/guide/syntax.html#参数)

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，`v-bind` 指令可以用于响应式地更新 HTML attribute：

```
<a v-bind:href="url">...</a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。

另一个例子是 `v-on` 指令，它用于监听 DOM 事件：

```
<a v-on:click="doSomething">...</a>
```

在这里参数是监听的事件名。我们也会更详细地讨论事件处理。

#### [动态参数](https://v2.cn.vuejs.org/v2/guide/syntax.html#动态参数)

2.6.0 新增

例如，如果你的 Vue 实例有一个 `data` property `attributeName`，其值为 `"href"`，那么这个绑定将等价于 `v-bind:href`

```
<!--
注意，参数表达式的写法存在一些约束，如之后的“对动态参数表达式的约束”章节所述。
-->
<a v-bind:[attributeName]="url"> ... </a>
```

```
<a v-on:[eventName]="doSomething"> ... </a>
```

当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`。













## Vue-cli



## Vue-router



## Vuex



## element-ui



## vue3