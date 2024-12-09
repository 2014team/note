## 原型、原型链

在 JavaScript 中，原型和原型链是理解继承和对象关系的关键概念。以下是对这两个概念的详细解释。

### 原型（Prototype）

每个 JavaScript 对象都有一个内部链接到另一个对象，这个对象就是原型。原型也是对象，并且可以有自己的原型，从而形成一个链条。所有对象最终都会链接到 `Object.prototype`，这是原型链的顶端。

#### 创建对象和原型

当使用构造函数创建一个对象时，这个对象会继承构造函数的 `prototype` 属性。

```
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log('Hello, ' + this.name);
};

const alice = new Person('Alice');
alice.greet(); // 输出: Hello, Alice
```

在上面的例子中，`Person` 构造函数有一个 `prototype` 属性，它是一个对象，包含了所有实例共享的方法和属性。`alice` 对象通过 `Person` 构造函数创建，因此 `alice` 对象的原型是 `Person.prototype`。

### 原型链（Prototype Chain）

原型链是指对象与其原型之间的链式结构。通过这种结构，一个对象可以继承其他对象的属性和方法。访问一个对象的属性时，如果该对象没有这个属性，JavaScript 引擎会沿着原型链向上查找，直到找到该属性或到达原型链的顶端（即 `Object.prototype`）。

```
function Animal() {
  this.species = 'animal';
}

Animal.prototype.walk = function() {
  console.log(this.species + ' is walking.');
};

function Dog(name) {
  this.name = name;
  this.species = 'dog';
}

Dog.prototype = new Animal();
Dog.prototype.constructor = Dog;

const bingo = new Dog('Bingo');
console.log(bingo.name); // 输出: Bingo
console.log(bingo.species); // 输出: dog
bingo.walk(); // 输出: dog is walking.
```

在这个例子中：

1. `Animal` 构造函数的 `prototype` 上定义了 `walk` 方法。
2. `Dog` 构造函数的 `prototype` 设置为一个新的 `Animal` 对象，因此 `Dog` 的实例会继承 `Animal` 的方法。
3. 创建 `bingo` 对象时，它具有 `Dog` 的属性和方法，同时通过原型链继承了 `Animal` 的 `walk` 方法。

### 检查对象的原型

- **`__proto__` 属性**：所有对象都有一个 `__proto__` 属性，指向其原型。

  ```
  console.log(bingo.__proto__ === Dog.prototype); // 输出: true
  console.log(Dog.prototype.__proto__ === Animal.prototype); // 输出: true
  ```

- **`Object.getPrototypeOf` 方法**：用于获取对象的原型。

  ```
  javascript
  复制代码
  console.log(Object.getPrototypeOf(bingo) === Dog.prototype); // 输出: true
  ```

### 原型链的顶端

所有对象的原型链最终都会指向 `Object.prototype`，这是原型链的顶端。`Object.prototype` 上的方法和属性对所有对象可用，比如 `toString`、`hasOwnProperty` 等。

```
console.log(Object.getPrototypeOf(Dog.prototype) === Animal.prototype); // 输出: true
console.log(Object.getPrototypeOf(Animal.prototype) === Object.prototype); // 输出: true
console.log(Object.getPrototypeOf(Object.prototype) === null); // 输出: true
```

### 总结

- **原型**：对象的原型是其继承属性和方法的来源，可以通过 `__proto__` 属性或 `Object.getPrototypeOf` 方法访问。
- **原型链**：对象通过原型链继承属性和方法，原型链最终指向 `Object.prototype`。
- **继承**：通过设置构造函数的 `prototype` 属性，可以实现对象之间的继承关系。

理解原型和原型链是深入掌握 JavaScript 对象和继承机制的关键，有助于编写更高效和灵活的代码