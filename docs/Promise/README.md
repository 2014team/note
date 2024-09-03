# Promise

Promise 是 JavaScript 中用于处理异步操作的对象。Promise 代表一个异步操作的最终完成（或失败）及其结果值。Promise 可以有三种状态：

1. **Pending（等待中）**：初始状态，既不是成功，也不是失败。
2. **Fulfilled（已成功）**：操作成功完成。
3. **Rejected（已失败）**：操作失败。

### 创建 Promise

你可以通过 `new Promise` 构造函数创建一个 Promise。它接收一个执行函数，执行函数有两个参数：`resolve` 和 `reject`。你可以调用 `resolve` 来将 Promise 状态变为成功，或者调用 `reject` 来将状态变为失败。

```
const myPromise = new Promise((resolve, reject) => {
  const success = true; // 这是一个示例条件

  if (success) {
    resolve('Operation was successful!');
  } else {
    reject('Operation failed.');
  }
});
```

### 使用 Promise

Promise 对象的主要方法有 `then`、`catch` 和 `finally`。这些方法用于处理 Promise 的结果。

- **`then`**：用于处理成功的结果。
- **`catch`**：用于处理失败的结果。
- **`finally`**：无论成功还是失败，都会执行。

```
myPromise
  .then(result => {
    console.log(result); // 输出: Operation was successful!
  })
  .catch(error => {
    console.error(error); // 仅在操作失败时执行
  })
  .finally(() => {
    console.log('Operation completed.'); // 无论成功还是失败都会执行
  });
```

### 链式调用

你可以链式调用 `then` 和 `catch` 方法来处理一系列的异步操作。

```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000); // 1 秒后返回结果
});

promise
  .then(result => {
    console.log(result); // 输出: 1
    return result * 2;
  })
  .then(result => {
    console.log(result); // 输出: 2
    return result * 3;
  })
  .then(result => {
    console.log(result); // 输出: 6
  })
  .catch(error => {
    console.error(error);
  });
```

### 处理异步请求

Promise 通常用于处理异步 HTTP 请求，例如使用 `fetch` 进行 GET 和 POST 请求。

#### GET 请求示例

```
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

#### POST 请求示例

```
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'foo',
    body: 'bar',
    userId: 1
  })
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

### `Promise.all` 和 `Promise.race`

- **`Promise.all`**：当所有给定的 Promise 都已成功或有一个失败时返回结果。

  ```
  const promise1 = Promise.resolve(3);
  const promise2 = 42;
  const promise3 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'foo');
  });
  
  Promise.all([promise1, promise2, promise3]).then(values => {
    console.log(values); // 输出: [3, 42, "foo"]
  });
  ```

- **`Promise.race`**：当第一个 Promise 成功或失败时返回结果。

  ```
  const promise1 = new Promise((resolve, reject) => {
    setTimeout(resolve, 500, 'one');
  });
  
  const promise2 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'two');
  });
  
  Promise.race([promise1, promise2]).then(value => {
    console.log(value); // 输出: "two"
  });
  ```

### 使用 `async` 和 `await`

`async` 和 `await` 是基于 Promise 的语法糖，使得异步代码看起来更像同步代码。`async` 函数始终返回一个 Promise，`await` 关键字用于等待 Promise 完成。

```
async function fetchData() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Fetch error:', error);
  }
}

fetchData();
```

### 总结

Promise 提供了一种处理异步操作的便捷方式，通过链式调用和组合可以实现复杂的异步流程。掌握 Promise 和相关方法，如 `then`、`catch`、`finally`、`Promise.all`、`Promise.race` 以及 `async/await`，可以帮助你更高效地处理异步编程任务。