# Typescript

## 1.TypeScript 的理解

### 1.1 是什么

TypeScript 是 JavaScript 的类型的超集，支持 ES6 语法，支持面向对象编程的概念，如类、接口、继承、泛型等。

> 超集，不得不说另外一个概念，子集，怎么理解这两个呢，举个例子，如果一个集合 A 里面的的所有元素集合 B 里面都存在，那么我们可以理解集合 B 是集合 A 的超集，集合 A 为集合 B 的子集

其是一种静态类型检查的语言，提供了类型注解，在代码编译阶段就可以检查出数据类型的错误。

同时扩展了 JavaScript 的语法，所以任何现有的 JavaScript 程序可以不加改变的在 TypeScript 下工作。

为了保证兼容性，TypeScript 在编译阶段需要编译器编译成纯 JavaScript 来运行，是为大型应用之开发而设计的语言，如下：

ts 文件如下：

```ts
const hello: string = "Hello World!";
console.log(hello);
```

编译文件后：

```js
const hello = "Hello World!";
console.log(hello);
```

### 1.2 特性

TypeScript 的特性主要有如下：

- **类型批注和编译时类型检查：**在编译时批注变量类型
- **类型推断：**ts 中没有批注变量类型会自动推断变量的类型
- **类型擦除：**在编译过程中批注的内容和接口会在运行时利用工具擦除
- **接口：**ts 中用接口来定义对象类型
- **枚举：**用于取值被限定在一定范围内的场景
- **Mixin：**可以接受任意类型的值
- **泛型编程：**写代码时使用一些以后才指定的类型
- **名字空间：**名字只在该区域内有效，其他区域可重复使用该名字而不冲突
- **元组：**元组合并了不同类型的对象，相当于一个可以装不同类型数据的数组
- ...

#### 类型批注

通过类型批注提供在编译时启动类型检查的静态类型，这是可选的，而且可以忽略而使用 JavaScript 常规的动态类型

```js
function Add(left: number, right: number): number {
  return left + right;
}
```

对于基本类型的批注是 number、bool 和 string，而弱或动态类型的结构则是 any 类型

#### 类型推断

当类型没有给出时，TypeScript 编译器利用类型推断来推断类型，如下：

```js
let str = "string";
```

变量 str 被推断为字符串类型，这种推断发生在初始化变量和成员，设置默认参数值和决定函数返回值时

如果缺乏声明而不能推断出类型，那么它的类型被视作默认的动态 any 类型

#### 接口

接口简单来说就是用来描述对象的类型 数据的类型有 number、null、string 等数据格式，对象的类型就是用接口来描述的

```ts
interface Person {
  name: string;
  age: number;
}

let tom: Person = {
  name: "Tom",
  age: 25,
};
```

### 1.3 区别

- TypeScript 是 JavaScript 的超集，扩展了 JavaScript 的语法
- TypeScript 可处理已有的 JavaScript 代码，并只对其中的 TypeScript 代码进行编译
- TypeScript 文件的后缀名 .ts （.ts，.tsx，.dts），JavaScript 文件是 .js
- 在编写 TypeScript 的文件的时候就会自动编译成 js 文件

## 2.TypeScript 的数据类型

### 2.1 是什么

typescript 和 javascript 几乎一样，拥有相同的数据类型，另外在 javascript 基础上提供了更加实用的类型供开发使用

在开发阶段，可以为明确的变量定义为某种类型，这样 typescript 就能在编译阶段进行类型检查，当类型不合符预期结果的时候则会出现错误提示

### 2.2 有哪些

- boolean（布尔类型）
- number（数字类型）
- string（字符串类型）
- array（数组类型）
- tuple（元组类型）
- enum（枚举类型）
- any（任意类型）
- null 和 undefined 类型
- void 类型
- never 类型
- object 对象类型

#### boolean

布尔类型

```ts
let flag: boolean = true;
// flag = 123; // 错误
flag = false; //正确
```

#### number

数字类型，和 javascript 一样，typescript 的数值类型都是浮点数，可支持二进制、八进制、十进制和十六进制

```ts
let num: number = 123;
// num = '456'; // 错误
num = 456; //正确
```

进制表示：

```ts
let decLiteral: number = 6; // 十进制
let hexLiteral: number = 0xf00d; // 十六进制
let binaryLiteral: number = 0b1010; // 二进制
let octalLiteral: number = 0o744; // 八进制
```

#### string

字符串类型，和 JavaScript 一样，可以使用双引号（"）或单引号（'）表示字符串

```ts
let str: string = "this is ts";
str = "test";
```

作为超集，当然也可以使用模版字符串``进行包裹，通过 ${} 嵌入变量

```ts
let name: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ name }
```

#### array

数组类型，跟 javascript 一致，通过[]进行包裹，有两种写法：

方式一：元素类型后面接上 []

```ts
let arr: string[] = ["12", "23"];
arr = ["45", "56"];
```

方式二：使用数组泛型，Array<元素类型>：

```ts
let arr: Array<number> = [1, 2];
arr = ["45", "56"];
```

#### tuple

元祖类型，允许表示一个已知元素数量和类型的数组，各元素的类型不必相同

```ts
let tupleArr: [number, string, boolean];
tupleArr = [12, "34", true]; //ok
typleArr = [12, "34"]; // no ok
```

赋值的类型、位置、个数需要和定义（生明）的类型、位置、个数一致

#### enum

enum 类型是对 JavaScript 标准数据类型的一个补充，使用枚举类型可以为一组数值赋予友好的名字

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

#### any

可以指定任何类型的值，在编程阶段还不清楚类型的变量指定一个类型，不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查，这时候可以使用 any 类型

使用 any 类型允许被赋值为任意类型，甚至可以调用其属性、方法

```ts
let num: any = 123;
num = "str";
num = true;
```

定义存储各种类型数据的数组时，示例代码如下：

```ts
let arrayList: any[] = [1, false, "fine"];
arrayList[1] = 100;
```

#### null 和 和 undefined

在 JavaScript 中 null 表示 "什么都没有"，是一个只有一个值的特殊类型，表示一个空对象引用，而 undefined 表示一个没有设置值的变量

默认情况下 null 和 undefined 是所有类型的子类型， 就是说你可以把 null 和 undefined 赋值给 number 类型的变量

```ts
let num: number | undefined; // 数值类型 或者 undefined
console.log(num); // 正确
num = 123;
console.log(num); // 正确
```

但是 ts 配置了--strictNullChecks 标记，null 和 undefined 只能赋值给 void 和它们各自

#### void

用于标识方法返回值的类型，表示该方法没有返回值。

```ts
function hello(): void {
  alert("Hello Runoob");
}
```

#### never

never 是其他类型 （包括 null 和 undefined）的子类型，可以赋值给任何类型，代表从不会出现的值

但是没有类型是 never 的子类型，这意味着声明 never 的变量只能被 never 类型所赋值。

never 类型一般用来指定那些总是会抛出异常、无限循环

```ts
let a: never;
a = 123; // 错误的写法

a = (() => {
  // 正确的写法
  throw new Error("错误");
})();

// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message);
}
```

#### object

对象类型，非原始类型，常见的形式通过{}进行包裹

```ts
let obj: object;
obj = { name: "Wang", age: 25 };
```

## 3.TypeScript 中枚举类型

### 3.1 是什么

枚举是一个被命名的整型常数的集合，用于声明一组命名的常数,当一个变量有几种可能的取值时,可以将它定义为枚举类型

通俗来说，枚举就是一个对象的所有可能取值的集合

在日常生活中也很常见，例如表示星期的 SUNDAY、MONDAY、TUESDAY、WEDNESDAY、THURSDAY、FRIDAY、SATURDAY 就可以看成是一个枚举

枚举的说明与结构和联合相似，其形式为：

```ts
enum 枚举名{
    标识符①[=整型常数],
    标识符②[=整型常数],
    ...
    标识符N[=整型常数],
}枚举变量;
```

### 3.2 使用

枚举的使用是通过 enum 关键字进行定义，形式如下：

```ts
enum xxx { ... }
```

声明关键字为枚举类型的方式如下：

```ts
// 声明 d 为枚举类型 Direction
let d: Direction;
```

类型可以分成：

- 数字枚举

- 字符串枚举

- 异构枚举

#### 数字枚举

当我们声明一个枚举类型是,虽然没有给它们赋值,但是它们的值其实是默认的数字类型,而且默认从 0 开始依次累加:

```ts
enum Direction {
  Up, // 值默认为 0
  Down, // 值默认为 1
  Left, // 值默认为 2
  Right, // 值默认为 3
}

console.log(Direction.Up === 0); // true
console.log(Direction.Down === 1); // true
console.log(Direction.Left === 2); // true
console.log(Direction.Right === 3); // true
```

如果我们将第一个值进行赋值后，后面的值也会根据前一个值进行累加 1：

```ts
enum Direction {
  Up = 10,
  Down,
  Left,
  Right,
}

console.log(Direction.Up, Direction.Down, Direction.Left, Direction.Right); // 10 11 12 13
```

#### 字符串枚举

枚举类型的值其实也可以是字符串类型：

```ts
enum Direction {
  Up = "Up",
  Down = "Down",
  Left = "Left",
  Right = "Right",
}

console.log(Direction["Right"], Direction.Up); // Right Up
```

如果设定了一个变量为字符串之后，后续的字段也需要赋值字符串，否则报错：

```ts
enum Direction {
  Up = "UP",
  Down, // error TS1061: Enum member must have initializer
  Left, // error TS1061: Enum member must have initializer
  Right, // error TS1061: Enum member must have initializer
}
```

#### 异构枚举

即将数字枚举和字符串枚举结合起来混合起来使用，如下：

```ts
enum BooleanLikeHeterogeneousEnum {
  No = 0,
  Yes = "YES",
}
```

通常情况下我们很少会使用异构枚举

### 3.3 本质

现在一个枚举的案例如下：

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```

通过编译后，javascript 如下：

```js
var Direction;
(function (Direction) {
  Direction[(Direction["Up"] = 0)] = "Up";
  Direction[(Direction["Down"] = 1)] = "Down";
  Direction[(Direction["Left"] = 2)] = "Left";
  Direction[(Direction["Right"] = 3)] = "Right";
})(Direction || (Direction = {}));
```

上述代码可以看到， Direction[Direction["Up"] = 0] = "Up"可以分成

```ts
Direction["Up"] = 0;
Direction[0] = "Up";
```

所以定义枚举类型后，可以通过正反映射拿到对应的值，如下：

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

console.log(Direction.Up === 0); // true
console.log(Direction[0]); // Up
```

并且多处定义的枚举是可以进行合并操作，如下：

```ts
enum Direction {
  Up = "Up",
  Down = "Down",
  Left = "Left",
  Right = "Right",
}

enum Direction {
  Center = 1,
}
```

编译后，js 代码如下：

```ts
var Direction;
(function (Direction) {
  Direction["Up"] = "Up";
  Direction["Down"] = "Down";
  Direction["Left"] = "Left";
  Direction["Right"] = "Right";
})(Direction || (Direction = {}));
(function (Direction) {
  Direction[(Direction["Center"] = 1)] = "Center";
})(Direction || (Direction = {}));
```

可以看到，Direction 对象属性回叠加

### 3.4 应用场景

就拿回生活的例子，后端返回的字段使用 0 - 6 标记对应的日期，这时候就可以使用枚举可提高代码可读性，如下：

```ts
enum Days {
  Sun,
  Mon,
  Tue,
  Wed,
  Thu,
  Fri,
  Sat,
}

console.log(Days["Sun"] === 0); // true
console.log(Days["Mon"] === 1); // true
console.log(Days["Tue"] === 2); // true
console.log(Days["Sat"] === 6); // true
```

包括后端日常返回 0、1 等等状态的时候，我们都可以通过枚举去定义，这样可以提高代码的可读性，便于后续的维护

## 4.TypeScript 中接口

### 4.1 是什么

**接口**是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法

简单来讲，一个接口所描述的是一个对象相关的属性和方法，但并不提供具体创建此对象实例的方法

typescript 的核心功能之一就是对类型做检测，虽然这种检测方式是“鸭式辨型法”，而接口的作用就是为为这些类型命名和为你的代码或第三方代码定义一个约定

### 4.2 使用方式

接口定义如下：

```ts
interface interface_name {}
```

例如有一个函数，这个函数接受一个 User 对象，然后返回这个 User 对象的 name 属性:

```ts
const getUserName = (user) => user.name;
```

可以看到，参数需要有一个 user 的 name 属性，可以通过接口描述 user 参数的结构

```ts
interface User {
  name: string;
  age: number;
}

const getUserName = (user: User) => user.name;
```

这些属性并不一定全部实现，上述传入的对象必须拥有 name 和 age 属性，否则 typescript 在编译阶段会报错。

如果不想要 age 属性的话，这时候可以采用可选属性，如下表示：

```ts
interface User {
  name: string;
  age?: number;
}
```

这时候 age 属性则可以是 number 类型或者 undefined 类型

有些时候，我们想要一个属性变成只读属性，在 typescript 只需要使用 readonly 声明，如下：

```ts
interface User {
  name: string;
  age?: number;
  readonly isMale: boolean;
}
```

这是属性中有一个函数，可以如下表示：

```ts
interface User {
  name: string;
  age?: number;
  readonly isMale: boolean;
  say: (words: string) => string;
}
```

如果传递的对象不仅仅是上述的属性，这时候可以使用：

- 类型推断

  ```ts
  interface User {
    name: string;
    age: number;
  }

  const getUserName = (user: User) => user.name;
  getUserName({ color: "yellow" } as User);
  ```

- 给接口添加字符串索引签名

  ```ts
  interface User {
    name: string;
    age: number;
    [propName: string]: any;
  }
  ```

- 接口还能实现继承也可以继承多个，父类通过逗号隔开，如下：

  ```ts
  interface Father {
    color: String;
  }

  interface Mother {
    height: Number;
  }

  interface Son extends Father, Mother {
    name: string;
  }
  ```

### 4.3 应用场景

例如在 javascript 中定义一个函数，用来获取用户的姓名和年龄：

```ts
const getUserInfo = function(user) {
    // ...
    return name: ${user.name}, age: ${user.age}
}
```

如果多人开发的都需要用到这个函数的时候，如果没有注释，则可能出现各种运行时的错误，这时候就可以使用接口定义参数变量：

```ts
// 先定义一个接口
interface IUser {
  name: string;
  age: number;
}

const getUserInfo = (user: IUser): string => {
  return `name: ${user.name}, age: ${user.age}`;
};

// 正确的调用
getUserInfo({ name: "koala", age: 18 });
```

包括后面讲到类的时候也会应用到接口

### 4.4 ts 中 interface 和 type 的区别

在 TypeScript 中，`interface` 和 `type` 都用来定义自定义类型，但它们在一些方面有一些区别：

1. **语法差异**：

   - `interface` 使用 `interface` 关键字来定义，例如：`interface Person { name: string; age: number; }`
   - `type` 使用 `type` 关键字来定义，例如：`type Person = { name: string; age: number; }`

2. **可扩展性**：

   - `interface` 可以被继承（`extends`）或者被实现（`implements`），并且可以定义多个同名的 `interface` 并且它们会合并为一个。
   - `type` 不能被继承或者实现，也不能定义同名的 `type`。

3. **使用场景**：

   - 当你定义对象的结构时，通常使用 `interface`，因为它更适合用来描述对象的形状。
   - 当你需要使用联合类型、交叉类型、元组、以及其他更复杂的类型时，通常使用 `type`，因为它更灵活，可以为任意类型起别名。

4. **可读性**：
   - `interface` 语法通常更具可读性，因为它是专门用来描述对象的形状的。
   - `type` 可以描述更广泛的类型，但可能会让代码稍显晦涩。

综上所述，`interface` 和 `type` 在大多数情况下可以互相替代，但在一些特定的情况下，它们的使用场景会有所不同。通常情况下，优先考虑使用 `interface` 来描述对象的形状，如果遇到需要更复杂的类型定义时，再考虑使用 `type`。

## 5.TypeScript 中类

### 5.1 是什么

类（Class）是面向对象程序设计（OOP，Object-Oriented Programming）实现信息封装的基础

> 类是一种用户定义的引用数据类型，也称类类型

传统的面向对象语言基本都是基于类的，JavaScript 基于原型的方式让开发者多了很多理解成本

在 ES6 之后，JavaScript 拥有了 class 关键字，虽然本质依然是构造函数，但是使用起来已经方便了许多

但是 JavaScript 的 class 依然有一些特性还没有加入，比如修饰符和抽象类

TypeScript 的 class 支持面向对象的所有特性，比如 类、接口等

### 5.2 使用方式

定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：

- 字段 ： 字段是类里面声明的变量。字段表示对象的有关数据。
- 构造函数： 类实例化时调用，可以为类的对象分配内存。
- 方法： 方法为对象要执行的操作

```js
class Car {
  // 字段
  engine: string;

  // 构造函数
  constructor(engine: string) {
    this.engine = engine;
  }

  // 方法
  disp(): void {
    console.log("发动机为 :   " + this.engine);
  }
}
```

#### 继承

类的继承使用过 extends 的关键字

```ts
class Animal {
  move(distanceInMeters: number = 0) {
    console.log(`Animal moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
```

Dog 是一个 派生类，它派生自 Animal 基类，派生类通常被称作子类，基类通常被称作 超类

Dog 类继承了 Animal 类，因此实例 dog 也能够使用 Animal 类 move 方法

同样，类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写，通过 super 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法，如下：

```ts
class PrinterClass {
  doPrint(): void {
    console.log("父类的 doPrint() 方法。");
  }
}

class StringPrinter extends PrinterClass {
  doPrint(): void {
    super.doPrint(); // 调用父类的函数
    console.log("子类的 doPrint()方法。");
  }
}
```

#### 修饰符

可以看到，上述的形式跟 ES6 十分的相似，typescript 在此基础上添加了三种修饰符：

- 公共 public：可以自由的访问类程序里定义的成员
- 私有 private：只能够在该类的内部进行访问
- 受保护 protect：除了在该类的内部可以访问，还可以在子类中仍然可以访问

#### 静态属性

这些属性存在于类本身上面而不是类的实例上，通过 static 进行定义，访问这些属性需要通过 类型.静态属性 的这种形式访问，如下所示：

```ts
class Square {
  static width = "100px";
}

console.log(Square.width); // 100px
```

上述的类都能发现一个特点就是，都能够被实例化，在 typescript 中，还存在一种抽象类

#### 抽象类

抽象类做为其它派生类的基类使用，它们一般不会直接被实例化，不同于接口，抽象类可以包含成员的实现细节

abstract 关键字是用于定义抽象类和在抽象类内部定义抽象方法，如下所示：

```ts
abstract class Animal {
  abstract makeSound(): void;
  move(): void {
    console.log("roaming the earch...");
  }
}
```

这种类并不能被实例化，通常需要我们创建子类去继承，如下：

```ts
class Cat extends Animal {
  makeSound() {
    console.log("miao miao");
  }
}

const cat = new Cat();

cat.makeSound(); // miao miao
cat.move(); // roaming the earch...
```

### 5.3 应用场景

除了日常借助类的特性完成日常业务代码，还可以将类（class）也可以作为接口，尤其在 React 工程中是很常用的，如下：

export default class Carousel extends React.Component<Props, State> {}
由于组件需要传入 props 的类型 Props ，同时有需要设置默认 props 即 defaultProps，这时候更加适合使用 class 作为接口

先声明一个类，这个类包含组件 props 所需的类型和初始值：

```ts
// props的类型
export default class Props {
  public children:
    | Array<React.ReactElement<any>>
    | React.ReactElement<any>
    | never[] = [];
  public speed: number = 500;
  public height: number = 160;
  public animation: string = "easeInOutQuad";
  public isAuto: boolean = true;
  public autoPlayInterval: number = 4500;
  public afterChange: () => {};
  public beforeChange: () => {};
  public selesctedColor: string;
  public showDots: boolean = true;
}
```

当我们需要传入 props 类型的时候直接将 Props 作为接口传入，此时 Props 的作用就是接口，而当需要我们设置 defaultProps 初始值的时候，我们只需要:

```ts
public static defaultProps = new Props()
```

Props 的实例就是 defaultProps 的初始值，这就是 class 作为接口的实际应用，我们用一个 class 起到了接口和设置初始值两个作用，方便统一管理，减少了代码量

## 6.TypeScript 中函数的理解

### 6.1 是什么

函数是 JavaScript 应用程序的基础，帮助我们实现抽象层、模拟类、信息隐藏和模块

在 TypeScript 里，虽然已经支持类、命名空间和模块，但函数仍然是主要定义行为的方式，TypeScript 为 JavaScript 函数添加了额外的功能，丰富了更多的应用场景

函数类型在 TypeScript 类型系统中扮演着非常重要的角色，它们是可组合系统的核心构建块

### 6.2 使用方式

跟 javascript 定义函数十分相似，可以通过 funciton 关键字、箭头函数等形式去定义，例如下面一个简单的加法函数：

```ts
const add = (a: number, b: number) => a + b;
```

上述只定义了函数的两个参数类型，这个时候整个函数虽然没有被显式定义，但是实际上 TypeScript 编译器是能够通过类型推断到这个函数的类型

当鼠标放置在第三行 add 函数名的时候，会出现完整的函数定义类型，通过: 的形式来定于参数类型，通过 => 连接参数和返回值类型

当我们没有提供函数实现的情况下，有两种声明函数类型的方式，如下所示：

```ts
// 方式一
type LongHand = {
  (a: number): number;
};

// 方式二
type ShortHand = (a: number) => number;
```

当存在函数重载时，只能使用方式一的形式

#### 可选参数

当函数的参数可能是不存在的，只需要在参数后面加上 ? 代表参数可能不存在，如下：

```ts
const add = (a: number, b?: number) => a + (b ? b : 0);
```

这时候参数 b 可以是 number 类型或者 undefined 类型，即可以传一个 number 类型或者不传都可以

#### 剩余类型

剩余参数与 JavaScript 的语法类似，需要用 ... 来表示剩余参数

如果剩余参数 rest 是一个由 number 类型组成的数组，则如下表示：

```ts
const add = (a: number, ...rest: number[]) => rest.reduce((a, b) => a + b, a);
```

#### 函数重载

允许创建数项名称相同但输入输出类型或个数不同的子程序，它可以简单地称为一个单独功能可以执行多项任务的能力

关于 typescript 函数重载，必须要把精确的定义放在前面，最后函数实现时，需要使用 |操作符或者?操作符，把所有可能的输入类型全部包含进去，用于具体实现

这里的函数重载也只是多个函数的声明，具体的逻辑还需要自己去写，typescript 并不会真的将你的多个重名 function 的函数体进行合并

例如我们有一个 add 函数，它可以接收 string 类型的参数进行拼接，也可以接收 number 类型的参数进行相加，如下：

```ts
// 上边是声明
function add(arg1: string, arg2: string): string;
function add(arg1: number, arg2: number): number;
// 因为我们在下边有具体函数的实现，所以这里并不需要添加 declare 关键字

// 下边是实现
function add(arg1: string | number, arg2: string | number) {
  // 在实现上我们要注意严格判断两个参数的类型是否相等，而不能简单的写一个 arg1 + arg2
  if (typeof arg1 === "string" && typeof arg2 === "string") {
    return arg1 + arg2;
  } else if (typeof arg1 === "number" && typeof arg2 === "number") {
    return arg1 + arg2;
  }
}
```

### 6.3 区别

从上面可以看到：

- 从定义的方式而言，typescript 声明函数需要定义参数类型或者声明返回值类型
- typescript 在参数中，添加可选参数供使用者选择
- typescript 增添函数重载功能，使用者只需要通过查看函数声明的方式，即可知道函数传递的参数个数以及类型

## 7.范型

### 7.1 是什么

泛型程序设计（generic programming）是程序设计语言的一种风格或范式

泛型允许我们在强类型程序设计语言中编写代码时使用一些以后才指定的类型，在实例化时作为参数指明这些类型 在 typescript 中，定义函数，接口或者类的时候，不预先定义好具体的类型，而在使用的时候在指定类型的一种特性

假设我们用一个函数，它可接受一个 number 参数并返回一个 number 参数，如下写法：

```ts
function returnItem(para: number): number {
  return para;
}
```

如果我们打算接受一个 string 类型，然后再返回 string 类型，则如下写法：

```ts
function returnItem(para: string): string {
  return para;
}
```

上述两种编写方式，存在一个最明显的问题在于，代码重复度比较高

虽然可以使用 any 类型去替代，但这也并不是很好的方案，因为我们的目的是接收什么类型的参数返回什么类型的参数，即在运行时传入参数我们才能确定类型

这种情况就可以使用泛型，如下所示：

```ts
function returnItem<T>(para: T): T {
  return para;
}
```

可以看到，泛型给予开发者创造灵活、可重用代码的能力

### 7.2 使用方式

泛型通过<>的形式进行表述，可以声明：

- 函数

- 接口

- 类

#### 函数声明

声明函数的形式如下：

```ts
function returnItem<T>(para: T): T {
  return para;
}
```

定义泛型的时候，可以一次定义多个类型参数，比如我们可以同时定义泛型 T 和 泛型 U：

```ts
function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
}

swap([7, "seven"]); // ['seven', 7]
```

#### 接口声明

声明接口的形式如下：

```ts
interface ReturnItemFn<T> {
  (para: T): T;
}
```

那么当我们想传入一个 number 作为参数的时候，就可以这样声明函数:

```ts
const returnItem: ReturnItemFn<number> = (para) => para;
```

## 8.ts 中命名空间和模块的区别

在 TypeScript 中，命名空间（Namespace）和模块（Module）是两种不同的组织代码结构的方式。

1. **命名空间（Namespace）**：

   - 命名空间是 TypeScript 中用于组织代码的一种方式，类似于其他语言中的命名空间或模块化系统。
   - 使用命名空间可以将相关的代码组织在一起，避免全局命名冲突。
   - 命名空间使用 `namespace` 关键字定义，并且可以嵌套使用。
   - 可以使用 `export` 关键字导出命名空间中的成员，以便在其他文件中使用。
   - 命名空间的成员通过命名空间名称进行访问，例如 `NamespaceName.memberName`。

2. **模块（Module）**：
   - 模块是 TypeScript 中用于封装和组织代码的更现代化的方式，它提供了更好的封装性、可复用性和可维护性。
   - 模块可以包含变量、函数、类等各种类型的成员，并且可以通过 `export` 关键字导出。
   - 可以使用 `import` 关键字导入其他模块中导出的成员。
   - 模块与文件一一对应，一个模块可以包含多个文件，但一个文件只能属于一个模块。
   - 在使用模块时，可以使用模块加载器（如 CommonJS、AMD、ES6 模块加载器）来加载模块。

主要区别：

- 命名空间是 TypeScript 中一种较为传统的组织代码的方式，而模块是更加现代化和推荐的方式。
- 命名空间在编译时会被转换成相应的 JavaScript 代码，而模块不会被转换，而是保留原有的结构，并通过模块加载器进行加载。
- 命名空间更适合在较小的项目中使用，而模块更适合在大型项目中使用，以提供更好的模块化和组织代码的能力。

## ts 中说说你对于声明合并的理解

在 TypeScript 中，声明合并是指当存在多个同名的声明时，TypeScript 会将它们合并成一个单一的声明。这种合并规则适用于接口、类、命名空间和类型别名等类型的声明。

具体来说，声明合并遵循以下几个规则：

1. 对于接口和类型别名，如果它们具有相同的名称，那么它们的成员将会合并为一个接口或类型别名。例如：

   ```typescript
   interface User {
     name: string;
   }

   interface User {
     age: number;
   }

   const user: User = {
     name: "John",
     age: 30,
   };
   ```

   在上面的例子中，TypeScript 会将两个 `User` 接口合并为一个，最终的类型是 `{ name: string; age: number; }`。

2. 对于类，如果存在多个同名的类声明，那么它们将会合并成一个类。这个过程包括静态属性、实例属性和构造函数的合并。例如：

   ```typescript
   class Car {
     static wheels: number;
     engine: string;
     constructor(engine: string) {
       this.engine = engine;
     }
   }

   class Car {
     static wheels: number;
     seats: number;
     constructor(seats: number) {
       this.seats = seats;
     }
   }

   const myCar = new Car(4);
   ```

   在上面的例子中，TypeScript 会将两个 `Car` 类合并为一个，最终的类会包含静态属性 `wheels`、实例属性 `engine` 和 `seats`，以及两个构造函数。

3. 对于命名空间，如果存在多个同名的命名空间声明，那么它们的内容会被合并到一个命名空间中。这个过程包括命名空间中的函数、类、接口等。例如：

   ```typescript
   namespace Utilities {
     export function formatDate(date: Date) {
       // Format date code
     }
   }

   namespace Utilities {
     export function log(message: string) {
       console.log(message);
     }
   }

   Utilities.formatDate(new Date());
   Utilities.log("Hello, world!");
   ```

   在上面的例子中，两个 `Utilities` 命名空间中的内容会被合并为一个命名空间，最终可以通过一个命名空间访问所有的函数。

总的来说，声明合并提供了一种灵活的方式来组织和扩展 TypeScript 代码，使得代码结构更加清晰和易于维护。

## ts 中 as 语法是什么？

在 TypeScript 中，`as` 语法用于类型断言，即显式地告诉编译器某个值的类型。

```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

在上面的例子中，`someValue` 是一个类型为 `any` 的变量，它可以是任意类型。然而，我们想要获取它的长度属性，但是在编译时 TypeScript 并不知道 `someValue` 是什么类型，因此需要使用类型断言告诉 TypeScript，我们确信 `someValue` 是一个字符串类型。这就是通过 `as string` 将 `someValue` 断言为字符串类型的语法。

需要注意的是，使用 `as` 进行类型断言时，如果将一个值断言为一个不同的类型，而且这两种类型之间并没有继承关系，那么编译器不会进行任何类型检查，这可能会导致运行时错误。因此，需要谨慎使用 `as` 语法，并且尽量避免在类型之间进行不安全的类型转换。

## extends 和 implements 有什么区别

在 TypeScript 中，`extends` 和 `implements` 都用于类之间的继承关系，但它们的作用对象和用法有所不同。

1. **extends：**

   - `extends` 用于类之间的继承关系，在类继承中，子类可以继承父类的属性和方法，并且可以通过 `super` 关键字调用父类的构造函数和方法。

   ```typescript
   class Animal {
     name: string;

     constructor(name: string) {
       this.name = name;
     }

     move(distance: number) {
       console.log(`${this.name} moved ${distance} meters.`);
     }
   }

   class Dog extends Animal {
     bark() {
       console.log("Woof! Woof!");
     }
   }

   const dog = new Dog("Buddy");
   dog.move(10); // Output: Buddy moved 10 meters.
   dog.bark(); // Output: Woof! Woof!
   ```

2. **implements：**

   - `implements` 用于实现接口，在接口实现中，类需要实现接口中定义的所有属性和方法，并且可以根据需要添加额外的属性和方法。

   ```typescript
   interface Printable {
     print(): void;
   }

   class Document implements Printable {
     content: string;

     constructor(content: string) {
       this.content = content;
     }

     print() {
       console.log(this.content);
     }
   }

   const doc = new Document("Hello, TypeScript!");
   doc.print(); // Output: Hello, TypeScript!
   ```

综上所述，`extends` 用于类之间的继承关系，子类可以继承父类的属性和方法；`implements` 用于实现接口，类需要实现接口中定义的所有属性和方法。

## 你用过哪些 ts 的高级类型

我可以向你介绍一些 TypeScript 中常用的高级类型：

1. **联合类型（Union Types）：**

   - 联合类型表示一个值可以是多种类型之一。使用 `|` 符号将多个类型连接在一起。

   ```typescript
   let val: string | number;
   val = "hello"; // Valid
   val = 42; // Valid
   val = true; // Error: Type 'boolean' is not assignable to type 'string | number'
   ```

2. **交叉类型（Intersection Types）：**

   - 交叉类型表示一个值具备多种类型的特征。使用 `&` 符号将多个类型连接在一起。

   ```typescript
   interface A {
     a: number;
   }

   interface B {
     b: string;
   }

   let obj: A & B;
   obj = { a: 1, b: "hello" }; // Valid
   ```

3. **类型别名（Type Aliases）：**

   - 类型别名可以为一个类型定义一个别名，提高代码的可读性和可维护性。

   ```typescript
   type ID = string | number;

   function printID(id: ID) {
     console.log(id);
   }
   ```

4. **索引类型（Index Types）：**

   - 索引类型允许您通过索引访问对象的属性，并提供类型安全性。

   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   type PersonKey = keyof Person; // "name" | "age"

   let key: PersonKey = "name";
   ```

5. **条件类型（Conditional Types）：**

   - 条件类型根据一个类型的条件判断结果选择另一个类型。

   ```typescript
   type IsString<T> = T extends string ? true : false;

   type StrOrNum = IsString<string>; // true
   type StrOrBool = IsString<boolean>; // false
   ```

6. **映射类型（Mapped Types）：**

   - 映射类型允许您从一个现有的类型创建一个新的类型，通过遍历已有类型的属性来生成新类型的属性。

   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   type ReadonlyPerson = Readonly<Person>;

   const person: ReadonlyPerson = { name: "John", age: 30 };
   person.name = "Jane"; // Error: Cannot assign to 'name' because it is a read-only property
   ```

这些是 TypeScript 中一些常用的高级类型，它们可以帮助您更好地描述数据的结构和约束。

## 你是怎么优化你的 ts 的代码的

我有几个常见的优化 TypeScript 代码的方法：

1. **严格的类型检查：** 开启 TypeScript 的严格模式 (`strict: true`)，以确保代码的类型安全性和一致性。这包括启用 `strictNullChecks`、`strictFunctionTypes`、`strictPropertyInitialization` 等选项。

2. **使用接口和类型别名：** 使用接口来描述对象的形状，使用类型别名来定义复杂的类型。这可以提高代码的可读性和可维护性。

3. **使用泛型：** 当函数或类与特定类型无关时，使用泛型来增加代码的灵活性和重用性。

4. **尽量避免 any 类型：** 避免使用 `any` 类型，因为它会破坏 TypeScript 的类型检查功能。尽量使用更具体的类型或通过泛型来保持类型安全性。

5. **合理使用类型断言：** 合理地使用类型断言（`as` 语法），但要小心不要滥用。确保只在确定类型的情况下使用断言，并且尽量使用类型推断来避免手动断言。

6. **使用严格的空值检查：** 启用 `strictNullChecks` 来检查可能为 null 或 undefined 的值，以避免空值错误。

7. **使用可选属性和默认参数：** 在接口和函数参数中使用可选属性和默认参数，以提高代码的灵活性和健壮性。

8. **及时更新 TypeScript 版本：** 及时更新到最新版本的 TypeScript，以获取新功能、修复的 bug 和性能优化。

这些是我平时优化 TypeScript 代码时常用的一些方法。通过这些方法，可以提高代码的质量、可维护性和性能。

## 说说你对 typescript 的了解，它和 JS 有什么关系

TypeScript 是一种由微软开发的开源编程语言，它是 JavaScript 的一个超集，意味着所有的 JavaScript 代码都是合法的 TypeScript 代码。TypeScript 在 JavaScript 的基础上添加了静态类型检查、接口、泛型等功能，使得代码更易于理解、维护和调试。

以下是我对 TypeScript 的一些了解：

1. **静态类型系统：** TypeScript 具有静态类型系统，允许开发者在编写代码时声明变量的类型，并在编译时进行类型检查。这有助于发现潜在的类型错误，提高代码的可靠性和健壮性。

2. **编译成 JavaScript：** TypeScript 代码需要经过编译成 JavaScript 才能在浏览器或其他 JavaScript 运行环境中执行。TypeScript 编译器会将 TypeScript 代码转换为符合 ECMAScript 标准的 JavaScript 代码。

3. **提供了更丰富的语法和特性：** TypeScript 支持 JavaScript 中没有的一些语法和特性，如接口、泛型、枚举、命名空间等，这些功能使得 TypeScript 更适合于大型项目的开发。

4. **与现有 JavaScript 生态系统的兼容性：** TypeScript 可以与现有的 JavaScript 库和框架无缝集成，开发者可以使用 TypeScript 编写新的代码，同时使用已有的 JavaScript 代码库。

5. **适用于大型项目的开发：** 由于 TypeScript 具有静态类型检查和更丰富的语法特性，因此特别适用于大型项目的开发，能够帮助开发者更好地管理复杂的代码库。

总的来说，TypeScript 是 JavaScript 的一个超集，它提供了更丰富的语法和功能，使得开发者能够更轻松地编写和维护复杂的应用程序。同时，TypeScript 还保持了与 JavaScript 的兼容性，开发者可以逐步地将现有的 JavaScript 代码迁移到 TypeScript 中，享受到 TypeScript 带来的好处。

## never 和 void 的区别

在 TypeScript 中，`void`和`never`是两个不同的类型，它们表示不同的概念：

1. **void**:

   - `void`类型表示没有任何类型。在函数中，如果函数不返回任何值，你可以将其类型标注为`void`。例如：

     ```typescript
     function greet(): void {
       console.log("Hello!");
     }
     ```

   - 在变量声明中，`void`表示变量可以持有`undefined`或`null`。但通常不建议将变量显式地标注为`void`类型，因为这限制了它们的使用。例如：

     ```typescript
     let unusable: void = undefined;
     ```

2. **never**:

   - `never`类型表示那些永远不会发生的值的类型。通常它用于描述永远不会正常结束的函数的返回值类型，或者永远会抛出异常的函数的返回类型。
   - 在函数中，当函数抛出异常或者永远不会结束时，可以将其返回类型标注为`never`。例如：

     ```typescript
     function throwError(message: string): never {
       throw new Error(message);
     }
     ```

   - `never`类型也用于标识那些总是会抛出异常或者无法正常返回的函数的返回类型。例如：

     ```typescript
     function infiniteLoop(): never {
       while (true) {
         console.log("Infinite loop");
       }
     }
     ```

所以，`void`表示没有返回值的函数或者持有`undefined`或`null`的变量，而`never`表示永远不会返回的函数的返回类型。

## any 和 unknown 的区别

`any` 和 `unknown` 是 TypeScript 中的两种特殊类型，它们在类型系统中具有不同的含义和用途：

1. **any**：

   - `any` 类型表示任意类型，它可以被赋值为任何类型的值，也可以调用任意属性或方法，而不会得到编译时的类型检查或提示。
   - 使用 `any` 类型时，TypeScript 编译器会将其视为一种“逃逸舱”（escape hatch），即放弃对该变量的类型检查，从而允许你绕过类型系统的限制，但同时也带来了类型安全性的风险。
   - 例如：

     ```typescript
     let value: any = 123;
     value = "abc";
     value.foo(); // 不会报错，因为 value 可以是任何类型
     ```

2. **unknown**：

   - `unknown` 类型表示未知类型，它类似于 `any`，但是更加安全，因为它会强制进行类型检查。
   - 当你无法确定变量的类型时，可以将其类型标注为 `unknown`，然后根据需要进行类型断言或类型检查来处理。
   - 与 `any` 不同，对于 `unknown` 类型的变量，你不能直接调用它的方法或访问它的属性，除非你先进行类型检查或类型断言。
   - 例如：

     ```typescript
     let value: unknown = 123;
     // value.foo(); // 报错：无法调用未知类型的方法
     if (typeof value === "string") {
       console.log(value.toUpperCase()); // OK，因为在此分支中 TypeScript 推断 value 为 string 类型
     }
     ```

关键区别：

- 在使用 `any` 类型时，TypeScript 编译器会放弃对变量的类型检查，而在使用 `unknown` 类型时，编译器会强制进行类型检查。
- 使用 `unknown` 类型可以提供更安全的类型检查，因为它要求你在使用变量之前先对其进行类型检查或类型断言，而不会像 `any` 类型那样隐式地接受任何操作。

## null 和 undefined 的区别

在 JavaScript 和 TypeScript 中，`null` 和 `undefined` 是两种特殊的值，用来表示缺失或未定义的状态，它们之间有一些区别：

1. **undefined**：

   - `undefined` 是一个表示“未定义”的原始值。在 JavaScript 中，当声明一个变量但未给它赋值时，默认初始化值为 `undefined`。
   - 例如：

     ```javascript
     let x; // x 的值为 undefined
     ```

2. **null**：

   - `null` 是一个表示“空值”的特殊对象。它通常用来表示一个变量被赋值为一个空对象的情况，或者表示一个操作没有返回值。
   - 例如：

     ```javascript
     let y = null; // y 的值为 null
     ```

关键区别：

- `undefined` 表示一个变量未定义或未赋值，而 `null` 表示一个变量被赋值为一个空对象。
- 在 JavaScript 中，`undefined` 是一个原始值，而 `null` 是一个特殊的对象。这是 JavaScript 早期设计中的一个错误，也是 JavaScript 中的一个常见陷阱。
- 在 TypeScript 中，`null` 和 `undefined` 都是类型的子类型，可以赋值给任意类型的变量。这意味着你可以将 `null` 和 `undefined` 赋值给任意类型的变量，但不可以将其他类型（比如 `number`、`string` 等）赋值给它们。

总的来说，`null` 和 `undefined` 都表示某种形式的缺失或未定义状态，但它们的语义略有不同，应根据具体情况选择使用哪个值。

## void 类型是什么？在什么场景下使用？

`void` 类型表示没有任何类型，通常用来表示函数没有返回值。在 TypeScript 中，`void` 类型用于标识函数的返回值类型，表示该函数不会返回任何值或者返回 `undefined`。下面是一些使用 `void` 类型的场景：

1. **函数没有返回值**：

   ```typescript
   function logMessage(message: string): void {
     console.log(message);
   }
   ```

   这个函数用于在控制台输出一条消息，但是不返回任何值。因此，它的返回类型标注为 `void`。

2. **函数明确声明没有返回值**：

   ```typescript
   function showAlert(): void {
     alert("Alert message");
   }
   ```

   在一些情况下，函数可能明确声明没有返回值，比如在浏览器环境中使用 `alert()` 弹窗函数。因此，可以将函数的返回类型标注为 `void`。

3. **回调函数**：
   在回调函数中，如果不需要返回值，则可以将函数的返回类型标注为 `void`。例如，事件处理函数通常没有返回值：

   ```typescript
   function onClickHandler(event: MouseEvent): void {
     console.log("Button clicked");
   }

   document
     .getElementById("myButton")
     ?.addEventListener("click", onClickHandler);
   ```

4. **Promise 中的 `void`**：
   当一个 Promise 不产生任何值时，可以将其类型标注为 `Promise<void>`。例如，一个异步操作只执行某些操作但不返回任何值的情况：

   ```typescript
   function asyncOperation(): Promise<void> {
     return new Promise((resolve) => {
       // 执行异步操作
       resolve();
     });
   }
   ```

总的来说，`void` 类型用于表示没有任何类型的情况，主要用于标识函数没有返回值或者函数返回 `undefined`。它可以帮助开发人员更清晰地表达函数的行为，提高代码的可读性和可维护性。

## unknow 的使用场景

`unknown` 是 TypeScript 中的一种顶级类型，表示“未知类型”。与 `any` 类型不同，`unknown` 类型提供了更严格的类型检查，因为它确保了类型安全性。`unknown` 类型的主要使用场景包括以下几种：

1. **类型安全的类型转换**：
   `unknown` 类型可以用于类型安全地进行类型转换。与 `any` 类型不同，使用 `unknown` 类型进行类型转换时，必须先进行类型检查或者类型断言，以确保转换的安全性。

   ```typescript
   let userInput: unknown;
   let userName: string;

   userInput = "Alice";
   if (typeof userInput === "string") {
     userName = userInput; // 这里可以安全地将 userInput 转换为 string 类型
   }
   ```

2. **函数参数类型未知**：
   当一个函数的参数类型未知时，可以使用 `unknown` 类型作为参数类型。在函数内部需要对参数进行类型检查或类型断言以确保类型安全。

   ```typescript
   function parseInput(input: unknown): string {
     if (typeof input === "string") {
       return input.toUpperCase();
     } else {
       return "";
     }
   }
   ```

3. **动态类型**：
   在某些情况下，无法确定一个变量的确切类型，但又需要对其进行操作。此时可以使用 `unknown` 类型作为该变量的类型。

   ```typescript
   let value: unknown;
   value = 123;
   value = "Hello";
   // 对 value 进行操作，需要先进行类型检查或类型断言
   ```

总的来说，`unknown` 类型提供了一种更安全的方式来处理未知类型的值，因为它要求在对值进行操作之前进行类型检查或类型断言，以确保类型安全。

## Omit 类型有什么用

`Omit` 类型是 TypeScript 中的一个内置辅助类型，它用于创建一个新类型，该类型排除了原始类型中指定的属性。这个功能非常有用，因为它允许我们从一个类型中快速创建一个新类型，但省略掉其中的一些属性。

以下是 `Omit` 类型的一些常见用途：

1. **创建新类型**：
   当我们需要基于一个已有的类型创建一个新类型，但是不需要其中的某些属性时，可以使用 `Omit` 类型。这在避免重复定义已有类型的情况下非常有用。

   ```typescript
   interface Person {
     name: string;
     age: number;
     address: string;
   }

   type PersonWithoutAddress = Omit<Person, "address">;
   ```

   这样就创建了一个新的类型 `PersonWithoutAddress`，它排除了原始类型 `Person` 中的 `address` 属性。

2. **避免冗余定义**：
   当我们需要从一个已有的类型中排除部分属性来定义一个新类型时，使用 `Omit` 类型可以避免冗余定义已有类型的大部分属性。

   ```typescript
   type PersonSummary = Omit<Person, "address" | "age">;
   ```

   在这个例子中，我们定义了一个 `PersonSummary` 类型，它排除了 `Person` 类型中的 `address` 和 `age` 属性。

3. **提高可读性和可维护性**：
   使用 `Omit` 类型可以使代码更具可读性和可维护性，因为它明确地表达了我们想要创建一个新类型，但是不需要其中的某些属性。

总的来说，`Omit` 类型是 TypeScript 中非常有用的工具，它提供了一种方便的方式来创建新类型，但是省略掉原始类型中的一些属性，**从而使得代码更加灵活和易于维护**。

## 如何实现函数重载

在 TypeScript 中，函数重载（Function Overloading）允许我们定义多个具有相同名称但具有不同参数类型和返回类型的函数声明。这样可以根据传入参数的类型和数量，让编译器在编译时选择正确的函数声明来调用。

以下是一个简单的示例，演示了如何在 TypeScript 中实现函数重载：

```typescript
function add(x: number, y: number): number; // 函数重载签名1
function add(x: string, y: string): string; // 函数重载签名2

// 实现函数重载
function add(x: number | string, y: number | string): number | string {
  if (typeof x === "number" && typeof y === "number") {
    return x + y;
  } else if (typeof x === "string" && typeof y === "string") {
    return x + y;
  } else {
    throw new Error("Invalid arguments");
  }
}

// 调用函数
console.log(add(5, 10)); // 输出：15
console.log(add("Hello", "World")); // 输出：HelloWorld
```

在上面的示例中：

- 我们首先定义了两个函数重载签名，它们分别指定了函数接受的参数类型和返回类型。
- 然后，我们实现了一个具有联合类型参数的函数 `add`，根据传入参数的类型，在运行时选择正确的实现来执行操作。
- 最后，我们调用了函数 `add`，分别传入不同类型的参数，它根据参数类型的不同选择了不同的实现来执行操作。

通过函数重载，我们可以在 TypeScript 中实现函数的多态，从而提高代码的灵活性和可读性。同时，函数重载还可以提供更好的类型检查，避免了在运行时出现意外的错误。

## 在 ts 中解释 rest 参数的作用及规则

在 TypeScript 中，rest 参数允许函数接受任意数量的参数，并将它们作为一个数组处理。rest 参数由省略号 `...` 后跟一个参数名组成，表示该参数将接收函数调用中的所有剩余参数，并将它们收集到一个数组中。

以下是 rest 参数的作用及规则：

1. **接收多个参数**：
   rest 参数可以接收函数调用中的所有剩余参数，并将它们收集到一个数组中。这使得函数可以接受任意数量的参数，而不需要提前指定参数的个数。

2. **数组类型**：
   rest 参数的类型是一个数组，数组中包含了所有传入的剩余参数。因此，rest 参数的类型注解通常是一个数组类型，可以使用数组中的方法和属性对参数进行操作。

3. **必须是最后一个参数**：
   rest 参数必须是函数参数列表中的最后一个参数，因为它将收集所有剩余的参数。如果在 rest 参数后还定义了其他参数，则 TypeScript 编译器会报错。

下面是一个简单的示例，演示了 rest 参数的使用：

```typescript
// 定义一个函数，接收任意数量的数字参数，并返回它们的总和
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

// 调用函数并传入多个参数
console.log(sum(1, 2, 3, 4, 5)); // 输出：15
console.log(sum(10, 20, 30)); // 输出：60
```

在上面的示例中，`sum` 函数定义了一个 rest 参数 `...numbers`，它可以接收任意数量的数字参数，并将它们收集到一个数组中。然后，我们可以使用数组的 `reduce` 方法对这些参数进行求和。
