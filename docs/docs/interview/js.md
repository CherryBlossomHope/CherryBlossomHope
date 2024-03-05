## JS 的设计原理

- **基于原型**：JavaScript的对象模型是基于原型的，这意味着对象可以直接从其他对象继承属性和方法，而不是使用类。这种模型提供了灵活的对象创建和继承机制。

- **动态类型**：JavaScript是一种动态类型语言，这意味着变量在运行时可以改变类型，不需要在编译时声明变量类型。

- **事件驱动**：JavaScript在浏览器中通常用于响应用户操作，如点击、移动等事件，从而执行相应的代码。

- **异步编程**：JavaScript通过事件循环和回调函数支持异步编程，允许代码在等待某些操作（如网络请求）完成时继续执行，提高了程序的性能和响应性。

- **函数是一等公民**：在JavaScript中，函数是对象，可以作为参数传递给其他函数，可以作为其他函数的返回值，也可以拥有属性。

- **解释执行**：JavaScript通常在运行时由JavaScript引擎（如V8、SpiderMonkey等）解释执行，而不是编译成机器码执行。

- **跨平台**：JavaScript被设计为可以在不同的设备和操作系统上运行，只要有支持JavaScript的解析器。

- **安全性**：JavaScript在设计时考虑到了安全性，例如，它不允许访问用户的文件系统，以防止恶意代码造成安全威胁。

- **单线程执行**：JavaScript在浏览器中通常是单线程执行的，这意味着它一次只能执行一个任务。为了处理耗时的操作，JavaScript使用异步编程模型。

- **标准化和扩展性**：随着ECMAScript（JavaScript语言的国际标准）的发展，JavaScript不断更新和扩展，引入了新的语法和功能，以适应不断变化的编程需求。

## 深浅拷贝

- 浅拷贝
  
  - 使用`Object.assign`方法
  
  - 使用扩展运算符（...）
  
  - 使用Array.prototype.slice()或Array.prototype.concat()进行数组浅拷贝

- 深拷贝
  
  - 使用JSON.parse(JSON.stringify(obj))（这种方法有局限性，不能拷贝函数、undefined、循环引用等）
  
  - 使用递归函数手动实现深拷贝
  
  - 使用第三方库，如lodash的_.cloneDeep方法
  
  - 原生深拷贝`structuredClone`

## 数组扁平化

- 使用`Array.prototype.flat()`
  ES2019引入了Array.prototype.flat()方法，可以用来扁平化数组。
  
  ```js
  const arr = [1, [2, [3, [4]], 5]];
  const flatArr = arr.flat(Infinity); // 使用Infinity作为深度，扁平化所有层级
  console.log(flatArr); // 输出：[1, 2, 3, 4, 5]
  ```

- 使用`Array.prototype.reduce()`和`Array.prototype.concat()`
  
  ```js
  const arr = [1, [2, [3, [4]], 5]];
  const flatArr = arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(...val) : acc.concat(val), []);
  console.log(flatArr); // 输出：[1, 2, 3, 4, 5]
  ```

- 使用递归
  
  ```js
  function flattenArray(arr) {
    let result = [];
    arr.forEach(item => {
      if (Array.isArray(item)) {
        result = result.concat(flattenArray(item));
      } else {
        result.push(item);
      }
    });
    return result;
  }
  
  const arr = [1, [2, [3, [4]], 5]];
  const flatArr = flattenArray(arr);
  console.log(flatArr); // 输出：[1, 2, 3, 4, 5]
  ```

- 使用`Array.prototype.some()`和`Array.prototype.concat()`
  
  ```js
  function flattenArray(arr) {
    while (arr.some(item => Array.isArray(item))) {
      arr = [].concat(...arr);
    }
    return arr;
  }
  
  const arr = [1, [2, [3, [4]], 5]];
  const flatArr = flattenArray(arr);
  console.log(flatArr); // 输出：[1, 2, 3, 4, 5]
  ```

- 使用lodash库的 `_.flattenDeep()`

## null 和 undefined 的区别

### `undefined`

表示一个声明了但没有被赋值的变量，或者一个不存在的对象属性。以下是一些产生undefined的场景

- 声明变量但是没有初始化

- 访问对象不存的属性

- 函数没有返回值时，默认返回

- 使用`void`表达式，如`void(0)`

### `null`

null是一个表示无值的特殊值，需要显式赋值给变量。它表示故意的空值，通常用于以下情况：

- 初始化一个将来可能被赋值为对象的变量

- 表示函数的参数或返回值没有对象

- 作为对象原型链的终点`（Object.prototype.__proto__）`

### 区别

- `undefined`表示变量声明了但没有赋值，而`null`是一个表示无值的特殊值，需要显式赋值。

- 在类型转换时，`undefined`转换为数字时为`NaN`，而`null`转换为数字时为`0`。

- 在`JSON`格式中，`null`是合法的值，而`undefined`不是。

- `undefined`是全局对象的一个属性，而`null`是一个字面量。

### 类型检查

`undefined`和`null`在类型检查时会被视为不同的类型：

```js
typeof undefined; // 输出："undefined"
typeof null; // 输出："object" (历史上的错误，现在被视为JavaScript语言的保留行为)
```

## Promise 的静态方法

### `Promise.all()`

### `Promise.race()`

### `Promise.any()`

## 改变this指向
