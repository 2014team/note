# Axios

Axios 是一个基于 Promise 的 HTTP 客户端，可以用于浏览器和 Node.js。它用于发起 HTTP 请求并处理响应，常用于与服务器进行数据交互。Axios 提供了许多功能，如拦截请求和响应、取消请求、自动转换 JSON 数据等。

### 安装 Axios

使用 npm 或 yarn 安装 Axios：

```
npm install axios
# 或
yarn add axios
```

### 基本用法

#### 发起 GET 请求

```
const axios = require('axios');

// 发起 GET 请求
axios.get('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

#### 发起 POST 请求

```
const axios = require('axios');

// 发起 POST 请求
axios.post('https://jsonplaceholder.typicode.com/posts', {
  title: 'foo',
  body: 'bar',
  userId: 1
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 设置请求头

```
const axios = require('axios');

// 设置请求头
axios.get('https://jsonplaceholder.typicode.com/posts/1', {
  headers: {
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
  }
})
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 创建 Axios 实例

可以创建一个 Axios 实例来自定义配置。

```
const axios = require('axios');

// 创建 Axios 实例
const instance = axios.create({
  baseURL: 'https://jsonplaceholder.typicode.com',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});

// 使用实例发起请求
instance.get('/posts/1')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 拦截请求和响应

Axios 提供了拦截器，可以在请求或响应被 then 或 catch 处理前拦截它们。

```
const axios = require('axios');

// 添加请求拦截器
axios.interceptors.request.use(config => {
  console.log('Request Interceptor:', config);
  return config;
}, error => {
  return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(response => {
  console.log('Response Interceptor:', response);
  return response;
}, error => {
  return Promise.reject(error);
});

// 发起请求
axios.get('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 取消请求

可以使用 `CancelToken` 来取消请求。

```
const axios = require('axios');
const CancelToken = axios.CancelToken;
let cancel;

// 发起请求
axios.get('https://jsonplaceholder.typicode.com/posts/1', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
}).catch(error => {
  if (axios.isCancel(error)) {
    console.log('Request canceled:', error.message);
  } else {
    console.error('Error:', error);
  }
});

// 取消请求
cancel('Operation canceled by the user.');
```

### 全局配置

可以在默认配置中设置全局配置选项。

```
const axios = require('axios');

// 设置全局配置
axios.defaults.baseURL = 'https://jsonplaceholder.typicode.com';
axios.defaults.headers.common['Authorization'] = 'Bearer YOUR_ACCESS_TOKEN';
axios.defaults.headers.post['Content-Type'] = 'application/json';

// 发起请求
axios.get('/posts/1')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### 使用 async/await

Axios 支持 async/await 语法，使得异步代码更加简洁。

```
const axios = require('axios');

async function fetchData() {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/posts/1');
    console.log(response.data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchData();
```

### 常用配置选项

- `url`: 请求的 URL。
- `method`: 请求方法（GET、POST、PUT、DELETE 等）。
- `baseURL`: 将自动加在 `url` 前面，除非 `url` 是绝对路径。
- `headers`: 自定义请求头。
- `params`: URL 参数。
- `data`: 请求体数据，适用于 `POST`、`PUT` 等请求方法。
- `timeout`: 请求超时时间。

### 完整示例

以下是一个使用 Axios 进行 GET 和 POST 请求的完整示例：

```
const axios = require('axios');

// 发起 GET 请求
axios.get('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    console.log('GET Response:', response.data);
  })
  .catch(error => {
    console.error('GET Error:', error);
  });

// 发起 POST 请求
axios.post('https://jsonplaceholder.typicode.com/posts', {
  title: 'foo',
  body: 'bar',
  userId: 1
})
  .then(response => {
    console.log('POST Response:', response.data);
  })
  .catch(error => {
    console.error('POST Error:', error);
  });
```

Axios 是一个强大的 HTTP 客户端，可以极大地简化 HTTP 请求的处理和数据的交互。通过掌握 Axios 的各种功能和配置选项，你可以更高效地进行前后端通信。