# 总结

## 1.Js 中的数据类型

### 基础数据类型

- number
- string
- boolean
- null
- undefined
- symbol

#### Number

数值最常见的整数类型格式则为十进制，还可以设置八进制（零开头）、十六进制（0x 开头）

```javascript
let initNum = 55; // 10进制的55
let num1 = 070; // 8进制的56
let hexNum1 = 0xa; // 16进制的10
```

浮点类型则在数值汇总必须包含小数点，还可通过科学计数法表示

```javascript
let floatNum1 = 1.1;
let floatNum2 = 0.1;
let floatNum3 = 0.1; // 有效，但不推荐
let floatNum = 3.125e7; // 等于 31250000
```

在数值类型中，存在一个特殊数值 NaN，意为“不是数值”，用于表示本来要返回数值的操作失败了（而不是抛出错误）

```javascript
console.log(0 / 0);
console.log(-0 / +0);
```

#### Undefined

Undefined 类型只有一个值，就是特殊值 undefined。当使用 var 或 let 声明了变量但没有初始化时，就相当于给变量赋予了 undefined 值

```javascript
let message;
console.log(message === undefined); // true
```

包含 undefined 值的变量跟未定义变量是有区别的

```javascript
let message; // 这个变量被声明了，只是值为undefined
console.log(message); // "undefined"
console.log(age); // 没有声明过这个变量，报错
```

#### String

字符串可以使用双引号("")、单引号('')或反引号(``)标示

```javascript
let firstName = "John";
let lastName = "Jacob";
let lastName = `Jingleheimerschmidt`;
```

字符串是不可变的，意思是一旦创建，它们的值就不能变了

```javascript
let lang = "Java";
lang = lang + "Script"; // 先销毁再创建
```

#### Null

Null 类型同样只有一个值，即特殊值 null

逻辑上来讲，null 值表示一个空对象指针，这也是给 typeof 传一个 null 会返回"Object"的原因

```javascript
let car = null;
console.log(typeof car); // "object"
```

undefined 值是由 null 值派生而来

```javascript
console.log(null === undefined); // true
```

只要变量要保存对象，而当时又没有那个对象可以保存，就可以用 null 来填充该变量

#### Boolean

Boolean（布尔值）类型有两个字面值：true 和 false

通过 Boolean 可以将其他类型的数据转化为布尔值

规则如下：

| 数据类型  |    转换为 true 的值    | 转换为 false 的值 |
| :-------: | :--------------------: | :---------------: |
|  String   |       非空字符串       |         "         |
|  Number   | 非零数值（包括无穷值） |      0、NaN       |
|  Object   |        任意对象        |       null        |
| Undefined |     N/A（不存在）      |     undefined     |

#### Symbol

Symbol（符号）是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险

```javascript
let genericSymbol = Symbol();
let otherGenericSymbol = Symbol();
console.log(genericSymbol == otherGenericSymbol); // false

let fooSymbol = Symbol("foo");
let otherFooSymbol = Symbol("foo");
console.log(fooSymbol == otherFooSymbol); // false
```

### 引用类型

- Object
- Array
- Function

#### Object

#### Array

#### Function

### 存储区别

基本数据类型和引用数据类型存储在内存中的位置不同：

- 基本数据类型存储在栈中
- 引用类型的对象存储在堆中

当我们把变量赋值给一个变量时，解析器首先要确定的就是这个值是基本类型值还是引用类型值

### 数据类型的总结

- 声明变量时不同的内存地址分配
  - 简单类型的值存放在栈中，在栈中存放的是对应的值
  - 引用类型对应的值存储在堆中，在栈中存放的是指向对内存的地址
- 不同的类型数据导致赋值变量时的不同
  - 简单类型赋值，是生成相同的值，两个对象对应不同的地址
  - 复杂类型肤质，是将保存对象的内存地址赋值给另一个变量。也就是两个变量指向堆内存中同一个对象

## 2.var let const 的区别

## 3.数组常用的方法有哪些

### 3.1 操作方法

数组基本操作可以归纳为增、删、改、查，需要留意的是哪些方法会对原数组产生影响，哪些方法不会

#### 3.1.1 增

下面前三种是对原数组产生影响的增添方法，第四种则不会对原数组产生影响

- push()

```javascript
// push方法接收任意数量的参数，并将它们添加到数组末尾，返回数组的最新长度
let colors = []; // 创建一个数组
let count = colors.push("red", "green"); // 推入两项
console.log(count); // 2
```

- unshift()

```javascript
// unshift()在数组开头添加任意多个值，然后返回新的数组长度
let colors = new Array(); // 创建一个数组
let count = colors.unshift("red", "green"); // 从数组开头推入两项
alert(count); // 2
```

- splice()

```javascript
// 传入三个参数，分别是开始位置、0（要删除的元素数量）、插入的元素，返回空数组
let colors = ["red", "green", "blue"];
let removed = colors.splice(1, 0, "yellow", "orange");
console.log(colors); // red,yellow,orange,green,blue
console.log(removed); // []
```

- concat()

```javascript
// 首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个新创建的数组，不会影响到原始数组
let colors = ["red", "green", "blue"];
let colors2 = colors.concat("yellow", ["black", "brown"]);
console.log(colors); // ["red", "green","blue"]
console.log(colors2); // ["red", "green", "blue", "yellow", "black", "brown"]
```

#### 3.1.2 删

下面三种都会影响原数组，最后一项不影响原数组：

- pop()

```javascript
// pop()方法用于删除数组的最后一项，同时减少数组的length值，返回被删除的项
let colors = ["red", "green"];
let item = colors.pop(); // 取得最后一项
console.log(item); // green
console.log(colors.length); // 1
```

- shift()

```javascript
// shift()方法用于删除数组的第一项，同时减少数组的length值，返回被删除的项
```

- splice()
- slice()

## 4.字符串的常用方法

### 4.1 操作方法

我们可以将字符串常用的方法归纳为增、删、改、查，需要知道字符串的特点是一旦创建了，就不可变

#### 4.1.1 增

这里的增的意思并不是说直接添加内容，而是创建字符串的一个副本，再进行操作

除了常用+以及${}进行字符串拼接之外，还可以通过 concat

- concat
  用于将一个或多个字符串拼接成一个新字符串

  ```javascript
  let stringValue = "hello";
  let result = stringValue.concat("world");
  console.log(result); // "hello world"
  console.log(stringValue); // "hello"
  ```

#### 4.1.2 删

这里的删不是说删除原字符串的内容，而是创建字符串的一个副本，再进行操作

常见的有：

- slice()
- substr()
- substring()

这三个方法都返回调用它们的字符串的一个子字符串，而且都接收一个或两个参数。

```javascript
let stringValue = "hellor world";
console.log(stringValue.slice(3)); // "lo world"
console.log(stringValue.substring(3)); // "lo world"
console.log(stringValue.substr(3)); // "lo world"
console.log(stringValue.slice(3, 7)); // "lo w"
console.log(stringValue.substring(3, 7)); // "lo worl"
```

#### 4.1.3 改

这里改的意思也不是改变原字符串，而是创建字符串的一个副本，再进行操作

常见的有：

- trim()、trimLeft()、trimRight()
  删除前、后或前后所有空格符，再返回新的字符串

  ```javascript
  let stringValue = " hello world  ";
  let trimmedStringValue = stringValue.trim();
  console.log(stringValue); // " hello world "
  console.log(trimmedStringValue); // "hello world"
  ```

- repeat()
  接收一个整数参数，表示要将字符串复制多少次，然后返回拼接所有副本后的结果

  ```javascript
  let stringValue = "na ";
  let copyResult = stringValue.repeat(2); // na na
  ```

- padStart()、padEnd()
  复制字符串，如果小于指定长度，则在相应一边填充字符，直至满足长度条件

  ```javascript
  let stringValue = "foo";
  console.log(stringValue.padStart(6)); // " foo"
  console.log(stringValue.padStart(9, ".")); // "......foo"
  ```

- toLowerCase()、toUpperCase()
  大小写转化

  ```javascript
  let stringValue = "hello world";
  console.log(stringValue.toUpperCase()); // "HELLO WORLD"
  console.log(stringValue.toLowerCase()); // "hello world"
  ```

#### 4.1.4 查

除了通过索引的方式获取字符串的值，还可通过：

- chatAt()
  返回给定索引位置的字符，由传给方法的整数参数指定

  ```javascript
  let message = "abcde";
  console.log(message.charAt(2)); // "c"
  ```

- indexOf()
  从字符串开头去搜索传入的字符串，并返回位置（如果没找到，则返回-1）

  ```javascript
  let stringValue = "hello world";
  console.log(stringValue.indexOf("o")); // 4
  ```

- startWith()、includes()
  从字符串中搜索传入的字符串中，并返回一个表示是否包含的布尔值

  ```javascript
  let message = "foobarbaz";
  console.log(message.startsWith("foo")); // true
  console.log(message.startsWith("bar")); // false
  console.log(message.includes("bar")); // true
  console.log(message.includes("qux")); // false
  ```

### 4.2 转换方法

- split
  把字符串按照指定的分割符，拆分成数组中的每一项

  ```javascript
  let str = "12+23+24";
  let arr = str.split("+"); // [12,23,34]
  ```

### 4.3 模版匹配方法

针对正则表达式，字符串设计了几个方法：

- match()
  接收一个参数，可以是一个正则表达式字符串，也可以是一个 RegExp 对象，返回数组

  ```javascript
  let text = "cat, bat, sat, fat";
  let pattern = /.at/;
  let matches = text.match(pattern);
  console.log(matched[0]); // "cat"
  ```

- search()
  接收一个参数，可以是一个正则表达式字符串，也可以是一个 RegExp 对象，找到则返回匹配索引，否则返回-1

  ```javascript
  let text = "cat, bat, sat, fat";
  let pos = text.search(/at/);
  console.log(pos); // 1
  ```

- replace()
  接收两个参数，第一个参数为匹配的内容，第二个参数为替换的元素（可用函数）

  ```javascript
  let text = "cat, bat, sat, fat";
  let result = text.replace("at", "ond");
  console.log(result); // "cond, bat, sat, fat"
  ```

## 5.ES6 数组

### 5.1 扩展运算符的应用

ES6 通过扩展运算符...，好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列

```javascript
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

主要用于函数调用的时候，将一个数组变为参数序列

```javascript
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers); // 42
```

可以将某些数据结构转为数组

```javascript
[...document.querySelectorAll("div")];
```

能够简单的实现数组复制

```javascript
const a1 = [1, 2];
const [...a2] = a1;
```

数组的合并也更为简洁了

```javascript
const arr1 = ["a", "b"];
const arr2 = ["c"];
const arr3 = ["d", "e"];
[...arr1, ...arr2, ...arr3];
// ['a','b','c','d','e']
```

注意：通过扩展运算符实现的是浅拷贝，修改了引用指向的值，会同步放映到新数组

下面看个例子就清楚多了

```javascript
const arr1 = ["a", "b", [1, 2]];
const arr2 = ["c"];
const arr3 = [...arr1, ...arr2];
arr[1][0] = 9999; // 修改arr1里面数组成员值
console.log(arr[3]); // 影响到arr3,['a','b',[9999,2],'c']
```

扩展运算符可以与解构赋值结合起来，用于生成数组

```javascript
const [first, ...rest] = [1, 2, 3, 4, 5];
first; // 1
rest; // [2, 3, 4, 5]

const [first, ...rest] = [];
first; // undefined
rest; // []

const [first, ...rest] = ["foo"];
first; // "foo"
rest; // []
```

如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错

```javascript
const [...butLast, last] = [1, 2, 3, 4, 5];
// 报错

const [first, ...middle, last] = [1, 2, 3, 4, 5];
// 报错
```

可以将字符串转为真正的数组

```javascript
[..."hello"];
// [ "h", "e", "l", "l", "o" ]
```

定义了遍历器（iterator）接口的对象，都可以用扩展运算符转为真正的数组

```javascript
let nodeList = document.querySelectorAll("div");
let array = [...nodeList];

let map = new Map({
  [1, 'one'],
  [2, 'two'],
  [3, 'three']
});

let arr = [...map.keys()]; // [1,2,3]
```

如果没有 iterator 接口的对象，使用扩展运算符，将会报错

```javascript
const obj = { a: 1, b: 2 };
let arr = [...obj]; // TypeError: Cannot spread non-iterable object
```

### 5.2 构造函数新增的方法

关于构造函数，数组新增的方法有如下：

- Array.from()
- Array.of()

#### Array.from()

将两类对象转为真正的数组：类似数组的对象和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）

```javascript
let arrayLike = {
  0: "a",
  1: "b",
  2: "c",
  length: 3,
};

let arr = Array.from(arrayLike); // ['a','b','c']
```

还可以接受第二个参数，用来对每个元素进行处理，将处理后的值放入返回的数组

```javascript
Array.from([1, 2, 3], (x) => x * x);
// [1,4,9]
```

#### Array.of()

用于将一组值，转换为数组

```javascript
Array.of(3, 11, 8);
```

没有参数的时候，返回一个空数组

当参数只有一个的时候，实际上是指定数组的长度

参数个数不少于 2 个时，Array()才会返回由参数组成的新数组

```javascript
Array(); // []
Array(3); // [, , ,]
Array(3, 11, 8); // [3, 11, 8]
```

### 5.3 实例对象新增的方法

关于数组实例对象新增的方法有如下：

- copyWithin()
- find()、findIndex()
- fill()
- entries()、keys()、values()
- includes()
- flat()、flatMap()

#### copyWithin()

#### find()、findIndex()

####

## 箭头函数与普通函数的区别

### 1.语法

- 箭头函数:

  - 使用 => 符号定义函数。
  - 如果只有一个参数，可以省略参数的括号。
  - 如果函数体只有一行返回语句，可以省略大括号和 return 关键字。

- 普通函数:

  - 使用 function 关键字定义函数。
  - 无论参数个数多少，都需要使用参数括号。
  - 函数体可以有任意复杂的逻辑，需要用大括号包裹。

### 2.this 绑定

- 箭头函数:

  - 箭头函数没有自己的 this，它会捕获上下文中最近的 this 作为自己的 this。
  - 适用于需要保留上下文 this 的场景，比如回调函数、事件处理函数。

- 普通函数:

  - 普通函数的 this 由调用者决定，在非严格模式下，默认指向全局对象（window 或 global）；在严格模式下，如果未被绑定，则为 undefined。
  - 需要用 bind、call、apply 手动绑定 this，否则 this 可能指向意外的对象。

### 3.arguments 对象

- 箭头函数没有自己的 arguments 对象，访问 arguments 会取到外层函数的 arguments。

  - 如果需要参数列表，可以使用 ...rest 参数语法。

- 普通函数普通函数有自己的 arguments 对象，包含所有调用时传入的参数。

### 4.new 关键字

- 箭头函数:

  - 箭头函数不能作为构造函数使用，不能与 new 关键字一起使用。
  - 因为箭头函数没有 prototype 属性。

- 普通函数:

  - 普通函数可以作为构造函数使用，可以与 new 关键字一起使用。
  - 当用 new 调用时，this 指向新创建的对象。

## import 和 require 的原理

### 语法

- import 语法:

  - 使用 import 关键字引入模块，支持按需导入、默认导入和重命名导入。
  - 只能在模块的顶层作用域使用。

- require 语法:

  - 使用 require 函数引入模块，支持引入整个模块或特定的部分。
  - 可以在代码的任何地方调用（例如在函数内部）。

### 加载时机

- import:

  - 是静态加载，在编译时解析模块依赖，提升到模块的顶部进行加载。
  - 导入的模块在脚本执行之前已经加载完毕。

- require:

  - 是动态加载，在代码执行时按需加载。
  - 当执行到 require 语句时才加载模块。

### 模块类型

- import:

  - 使用 ES6 模块（ESM），它支持 import 和 export。
  - ES6 模块是默认启用严格模式的。

- require:

  - 使用 CommonJS 模块系统，主要在 Node.js 环境中使用。
  - CommonJS 模块使用 module.exports 和 exports 导出，require 引入。

### 静态分析

- import:

  - 支持静态分析，编译器和工具链（如 Webpack、Rollup 等）可以提前解析依赖关系，进行优化如 Tree Shaking。
  - 有助于代码的优化和性能提升。

- require:

  - 不支持静态分析，因为 require 是动态的，编译时无法确定模块的依赖关系。
  - 在动态情况下可能影响代码优化，例如代码分割。

### 导出方式

- import:支持多种导出方式，包括默认导出、命名导出和导出集合。

  - ```javascript
    // 默认导出
    export default function () {}
    // 命名导出
    export const namedExport = () => {};

    // 多个命名导出
    export { namedExport1, namedExport2 };
    ```

- CommonJS 主要使用 module.exports 和 exports 导出。通常以对象形式导出，无法原生支持按需导出

  - ```javascript
    // 导出单个对象
    module.exports = function () {};

    // 导出多个值
    module.exports = {
      namedExport1: () => {},
      namedExport2: () => {},
    };
    ```

## get、post、put 的区别

- GET
  - 用于从服务器中获取资源，通常用于获取页面、数据等。
  - 请求参数会附加在 URL 的查询字符串中。
  - 传输数据量有限，因为查询字符串的长度限制。
  - 可以被缓存，且可以被收藏为书签。
  - 可以通过地址栏访问，因为请求参数明文显示在 URL 中。
  - 幂等的，即多次请求会得到相同的结果。
- POST
  - 用于向服务器提交数据，通常用于表单提交、文件上传等。
  - 请求参数通常包含在请求体中，不会暴露在 URL 中。
  - 传输数据量相对较大，没有长度限制。
  - 不能被缓存，也不能被收藏为书签。
  - 不能通过浏览器地址直接访问，因为请求参数不会显示在 URL 中。
  - 非幂等的，即多次请求可能会产生不同的结果。
- PUT
  - 用于向服务器提交数据，但是和 POST 的语义略有不同
  - 通常用于更新资源，客户端提供完整的更新后的资源。
  - 请求参数通常包含在请求体中，不会暴露在 URL 中
  - 通常用于替换掉指定的 URL 对应的资源
  - 一般情况下也不会被缓存，但与 POST 不同的是，PUT 请求可以是幂等的，即多次请求会得到相同的结果。
- 总结：
  - GET 主要用于获取资源，POST 主要用于提交资源，而 PUT 则主要用于更新资源。
  - GET 请求参数在 URL 中，适合获取数据；POST 和 PUT 请求参数在请求体中，适合提交大量数据。
  - GET 请求可以被缓存，而 POST 和 PUT 请求通常不会被缓存。
  - GET 请求是幂等的，POST 和 PUT 请求是幂等的，但不一定。

## generate

generator 函数会返回一个遍历器对象，即具有 Symbol.iterator 属性，并且返回给自己

通过 yield 关键字可以暂停 generator 函数返回的遍历器对象的状态。

## 异步解决方案

- 回调函数
  - 最早的异步编程方式，通过将一个函数作为参数传递给另一个函数，在异步操作完成后调用回调函数。
  - 由于函数嵌套层级可能较深，容易出现“回调地狱”问题，即代码难以维护和调试。
- promise
  - 引入于 ES6（ES2015），Promise 是一个对象，代表一个异步操作的最终完成（或失败）及其结果值。
  - 通过 then、catch 方法链式调用，解决了回调地狱问题，增强了代码的可读性。
  - 复杂的业务逻辑时，.then 链式调用依然显得冗长。
- async/await
  - 引入于 ES8（ES2017），async/await 是基于 Promise 之上的语法糖。
  - 使用 async 关键字定义一个异步函数，await 用于等待一个 Promise 完成，使异步代码看起来像同步代码。
- generator

## proxy

- new Proxy(target,handler)
- target 指的是要拦截的对象
- handler 解析器对象
- 一般和 Reflect 搭配使用

## 装饰器

就是在不改变原类和使用继承的情况下，扩充类的属性和方法

## set、map 和 weekset、weekmap

- set

  - 一个数据结构，成员的值都是唯一的，没有重复的值，我们一般称为集合
  - add() delete() has() clear()
  - keys() values() entries() forEach()

- Map

  - 本身一个构造函数，用来生成 Map 数据结构
  - set() get() has() delete() clear()
  - keys() values() entries() forEach()

- WeekSet

  - 没有遍历的 API
  - 没有 size 属性
  - WeakSet 里面的引用只要在外部消失，它在 WeakSet 里面的引用就会自动消失

- WeekMap

  - 没有遍历操作的 API
  - 没有 clear 清空方法
  - WeakSet 里面的引用只要在外部消失，它在 WeakSet 里面的引用就会自动消失

## web 常见攻击

### CSRF

### XSS

## 闭包

## 作用域链

## 原型、原型链、特点

## 继承

### 原型链式继承

原型链式继承是比较常见的继承方式之一，其中涉及的构造函数、原型和实例，三者之间存在着一定的关系，即每一个构造函数都有一个原型对象，原型对象又包含一个指向构造函数的指针，而实例则包含一个原型对象的指针

```javascript
function Parent() {
  this.name = "parent";
  this.play = [1, 2, 3];
}
function Child() {
  this.type = "child2";
}
Child.prototype = new Parent();
console.log(new Child());
```

- 缺点：
  两个实例使用的是同一个原型对象

### 构造函数式继承（基于 call）

```javascript
function Parent() {
  this.name = "parent";
}
Parent.prototype.getName = function () {
  return this.name;
};
function Child() {
  Parent1.call(this);
  this.type = "child";
}
let child = new Child();
console.log(child); // 没问题
console.log(child.getName()); // 会报错
```

- 缺点：
  只能继承父类的实例属性和方法，不能继承原型属性或者方法

### 组合继承

前面的两种继承方法，各有优缺点，组合继承就是将两种继承方法继承起来

```javascript
function Parent() {
  this.name = "parent";
  this.play = [1, 2, 3];
}

Parent3.prototype.getName = function () {
  return this.name;
};

function Child() {
  Parent.call(this);
  this.type = "child";
}

// 第一次调用 Parent3()
Child3.prototype = new Parent3();
// 手动挂上构造器，指向自己的构造函数
Child3.prototype.constructor = Child3;
```

### 原型式继承

这里主要借助 Object.create 方法实现普通对象的继承

```javascript
let parent = {
  name: "parent",
  friends: ["p1", "p2", "p3"],
  getName: function () {
    return this.name;
  },
};

let person = Object.create();
```

### 寄生式继承

### 寄生组合式继承

## this 对象

## new 操作符号

在 Javascript 中，new 关键字用于创建一个新的对象实例，并调用一个构造函数来初始化这个对象。new 关键字的主要作用包括以下几点：

1. 创建一个新的对象
2. 将构造函数的作用域付给新的对象：在创建的空对象上，设置构造函数的作用域链（即原型链）。
3. 调用构造函数：使用新对象作为 this 上下文，调用构造函数
4. 返回新对象：如果构造函数没有显示返回一个对象，则 new 表达式会自动返回这个新对象。

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person = new Person("Alice", 30);
```

在这个例子中，new 这个表达式做了以下几件事：

```javascript
function mynew(Func, ...args) {
  const obj = {};
  obj.__proto__ = Func.prototype;
  let result = Func.apply(obj, args);
  return result instanceof
}
```

## 执行上下文和执行栈

## 事件模型

## 事件代理

## 检查变量属性

### typeof

### instanceof

### Object.string.call()

## forin 和 forof 的区别

### 1.遍历的对象类型

- for...in 循环用于遍历对象的可枚举属性，包括继承的属性
- for...of 循环用于遍历可迭代对象（iterable objects），如数组、字符串、Map、Set 等。

### 2.遍历顺序

- for...in 循环遍历对象属性时，不保证属性的顺序，因为对象的属性没有固定的顺序
- for...of 循环遍历可迭代对象时，会按照对象内部元素的顺序进行遍历

### 3.遍历的值

- for...in 循环遍历对象时，返回的是属性名（字符串）
- for...of 循环遍历可迭代对象时，返回的是对象的元素值

### 4.适用场景

- for...in 通常用于遍历对象的属性，进行对象的属性检查或操作
- for...of 通常用于遍历数组、集合等数据结构中的元素值

```javascript
// for...in遍历对象
const obj = { a: 1, b: 2, c: 3 };
for (const key in obj) {
  console.log(key); // 输出：a,b,c
}

// for...of遍历数组
const arr = [1, 2, 3];
for (const value of arr) {
  console.log(value); // 输出：1，2，3
}
```

## 浏览器都有哪些进程，渲染进程中都有什么线程

现代浏览器通常采用多进程架构，常见的进程包括：

1. **浏览器进程（Browser Process）**：浏览器的主进程，负责协调和管理所有其他进程。它负责处理用户界面、提供浏览器功能、管理子进程等。

2. **渲染进程（Renderer Process）**：负责将 HTML、CSS 和 JavaScript 转换成用户可以与之交互的可视化页面。一个浏览器通常会有多个渲染进程，每个标签页（Tab）通常对应一个渲染进程。

在渲染进程中，常见的线程包括：

- **主线程（Main Thread）**：负责解析 HTML、构建 DOM 树、布局（Layout）、绘制（Paint）和交互响应等任务。

- **渲染线程（Renderer Thread）**：在大多数浏览器中，渲染线程通常与主线程合并，负责将 HTML、CSS 和 JavaScript 转换成用户可以看到的位图，然后交给合成线程进行显示。

- **合成线程（Compositor Thread）**：负责将渲染线程生成的位图进行合成，以及处理用户输入、页面滚动等交互操作。在一些浏览器中也称为图层线程（Layer Thread）。

- **工作线程（Worker Thread）**：用于执行 JavaScript 的 Web Worker，可以在后台进行复杂的计算或操作，以免阻塞主线程。

总的来说，渲染进程中的线程协同工作，共同实现了页面的解析、渲染和交互功能。

## 说说浏览器渲染流程，分层之后在什么时候合成，什么是重排、重绘、怎么避免

浏览器渲染流程可以简单描述为以下几个步骤：

1. **构建 DOM 树**：解析 HTML 文件，构建 DOM 树，这是由主线程完成的。

2. **构建 CSSOM 树**：解析 CSS 文件，构建 CSSOM 树，与 DOM 树一起用于计算元素的样式。这也是由主线程完成的。

3. **合成 Render 树**：将 DOM 树和 CSSOM 树结合起来，形成 Render 树，Render 树中的每个节点都是一个可视化的对象，包含了元素的样式和几何信息。这个过程也是由主线程完成的。

4. **布局（Layout）**：根据 Render 树中的节点信息计算元素的几何属性（如位置、大小等），并确定元素在页面上的具体位置。这个过程也被称为回流（Reflow），由主线程完成。

5. **绘制（Paint）**：根据 Render 树和布局信息，将页面内容绘制成位图，即绘制每个元素的像素。这个过程也被称为重绘（Repaint），由主线程完成。

6. **合成（Composite）**：将绘制的位图进行合成，生成最终的页面内容，并将其显示在屏幕上。这个过程由合成线程（Compositor Thread）完成。

在浏览器渲染过程中，重排（Reflow）和重绘（Repaint）是性能开销较大的操作：

- **重排（Reflow）**：当页面的结构或布局发生变化时，浏览器需要重新计算元素的几何属性，这就触发了重排操作。例如，改变元素的尺寸、位置、内容等都会导致重排。

- **重绘（Repaint）**：当元素的样式发生变化，但是不影响其几何属性时，浏览器只需要重新绘制元素的外观，而不需要重新计算布局。这就触发了重绘操作。

为了避免频繁的重排和重绘，可以采取以下几个策略：

1. **批量修改样式**：避免通过 JavaScript 逐个修改元素的样式，而是通过修改元素的 class 或一次性设置元素的样式，以减少重排和重绘的次数。

2. **使用 CSS3 动画**：CSS3 动画利用了 GPU 加速，可以降低页面的重绘开销，提高动画的性能。

3. **使用文档片段（Document Fragment）**：在动态添加多个 DOM 元素时，可以先将它们添加到文档片段中，然后一次性将文档片段添加到文档中，以减少重排的次数。

4. **使用分层和合成**：合理使用 CSS 属性（如 transform、opacity）触发 GPU 加速，将页面的渲染分层，并使用合成线程对页面进行合成，以提高页面的渲染性能。

## eventLoop

### 1.进程和线程

#### 进程

- CPU 承担了所有的计算任务
- 进程是 CPU 资源分配的最小单位
- 在同一个时间内，单个 CPU 只能执行一个任务，只能运行一个进程
- 如果有一个进程正在执行，其他进程就得暂停
- CPU 使用了时间片轮转的算法实现多进程的调度

#### 线程

- 线程是 CPU 调度的最小单位
- 一个进程可以包括多个线程 这些线程共享这个进程的资源

### 2.chrome 浏览器进程

- 浏览器是多进程的
- 每一个 TAB 页就是一个进程
- 浏览器主进程

  - 控制其他子进程的创建和销毁
  - 浏览器界面显示，比如用户交互、前进、后退等操作
  - 将渲染的内容绘制到用户界面上

- 渲染进程就是我们说的浏览器内核

  - 负责页面的渲染、脚本的执行、事件处理
  - 每个 TAB 页面都有一个渲染进程

- 网络进程 处理网络请求、文件访问等操作

- GPU 进程 用于 3D 绘制

### 3.渲染的线程

- GUI 渲染线程

  - 渲染、布局和绘制页面
  - 当页面需要绘制和回流时，此线程就会执行
  - 与 JS 引擎互斥

- JS 引擎线程

  - 负责解析执行 JS 脚本
  - 只有一个 JS 引擎线程
  - 与 GUI 渲染线程互斥

- 事件触发线程

  - 用来控制事件循环（鼠标点击、setTimeout、Ajax 等）
  - 当事件满足触发条件时，把事件放入到 JS 引擎所有的执行队列中

- 定时器触发线程

  - setInterval 和 setTimeout 所在线程
  - 定时任务并不是由 JS 引擎计时，而是由定时触发线程来计时
  - 计时完毕之后会通知触发线程

- 异步 HTTP 请求线程
  - 浏览器有一个单独的线程处理 AJAX 请求
  - 当请求完毕后，如果有回调函数，会通知事件触发线程

### 4.宏任务

- 页面的大部分任务是在主线程上执行的，比如下面这些都是宏任务

  - 渲染事件（DOM 解析、布局、绘制）
  - 用户交互（鼠标点击、页面缩放）
  - Javascript 脚本执行
  - 网络请求
  - 文件读写

- 宏任务会添加到消息到消息队列的尾部，当主线程执行到该消息的时候就会执行
- 每次从事件队列中获取一个事件回调并且放到执行栈中的就是一个宏任务，宏任务执行过程中不会执行其他内容
- 每次宏任务执行完毕后进行 GUI 渲染线程的渲染，然后再执行下一个宏任务
- 宏任务：script（整体代码），setTimeout，setInterval、setImmediate、I/O、UI rendering
- 宏任务颗粒度较大，不适合需要精确控制的任务
- 宏任务是由宿主方控制的
