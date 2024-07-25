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

## Vue实例

每个 Vue 应用都是通过用 `Vue` 函数创建一个新的 **Vue 实例**开始的：

### 创建实例

```js
var vm = new Vue({
  // 选项
})
```

### 数据与方法

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





## Vue-cli



## Vue-router



## Vuex



## element-ui



## vue3