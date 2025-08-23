# React

## 1.React 的理解

### 1.1 是什么

React，用于构建用户界面的 JavaScript 库，只提供了 UI 层面的解决方案

遵循组件设计模式、声明式编程范式和函数式编程概念，以使前端应用程序更高效

使用虚拟 DOM 来有效地操作 DOM，遵循从高阶组件到低阶组件的单向数据流

帮助我们将界面成了各个独立的小块，每一个块就是组件，这些组件之间可以组合、嵌套，构成整体页面

react 类组件使用一个名为 render() 的方法或者函数组件 return，接收输入的数据并返回需要展示的内容

```jsx
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

ReactDOM.render(
  <HelloMessage name="Taylor" />,
  document.getElementById("hello-example")
);
```

上述这种类似 XML 形式就是 JSX，最终会被 babel 编译为合法的 JS 语句调用

被传入的数据可在组件中通过 this.props 在 render() 访问

### 1.2 特性

React 特性有很多，如：

- JSX 语法
- 单向数据绑定
- 虚拟 DOM
- 声明式编程
- Component

着重介绍下声明式编程及 Component

#### 声明式编程

声明式编程是一种编程范式，它关注的是你要做什么，而不是如何做

它表达逻辑而不显式地定义步骤。这意味着我们需要根据逻辑的计算来声明要显示的组件

如实现一个标记的地图：

通过命令式创建地图、创建标记、以及在地图上添加的标记的步骤如下：

```jsx
// 创建地图
const map = new Map.map(document.getElementById("map"), {
  zoom: 4,
  center: { lat, lng },
});

// 创建标记
const marker = new Map.marker({
  position: { lat, lng },
  title: "Hello Marker",
});

// 地图上添加标记
marker.setMap(map);
```

而用 React 实现上述功能则如下：

```jsx
<Map zoom={4} center={(lat, lng)}>
  <Marker position={(lat, lng)} title={"Hello Marker"} />
</Map>
```

声明式编程方式使得 React 组件很容易使用，最终的代码简单易于维护

#### Component

在 React 中，一切皆为组件。通常将应用程序的整个逻辑分解为小的单个部分。 我们将每个单独的部分称为组件

组件可以是一个函数或者是一个类，接受数据输入，处理它并返回在 UI 中呈现的 React 元素

函数式组件如下：

```jsx
const Header = () => {
  return (
    <Jumbotron style={{ backgroundColor: "orange" }}>
      <h1>TODO App</h1>
    </Jumbotron>
  );
};
```

类组件（有状态组件）如下：

```jsx
class Dashboard extends React.Component {
  constructor(props) {
    super(props);

    this.state = {};
  }
  render() {
    return (
      <div className="dashboard">
        <ToDoForm />
        <ToDolist />
      </div>
    );
  }
}
```

一个组件该有的特点如下：

- 可组合：每个组件易于和其它组件一起使用，或者嵌套在另一个组件内部
- 可重用：每个组件都是具有独立功能的，它可以被使用在多个 UI 场景
- 可维护：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护

### 1.3 优势

通过上面的初步了解，可以感受到 React 存在的优势：

- 高效灵活
- 声明式的设计，简单使用
- 组件式开发，提高代码复用率
- 单向响应的数据流会比双向绑定的更安全，速度更快

## 2.hooks 组件

### useState

首先给出一个例子，如下：

```jsx
import React, { useState } from "react";

function Example() {
  // 声明一个叫 "count" 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

在函数组件中通过 useState 实现函数内部维护 state，参数为 state 默认的值，返回值是一个数组，第一个值为当前的 state，第二个值为更新 state 的函数

该函数组件等价于的类组件如下：

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

从上述两种代码分析，可以看出两者区别：

- state 声明方式：在函数组件中通过 useState 直接获取，类组件通过 constructor 构造函数中设置
- state 读取方式：在函数组件中直接使用变量，类组件通过 this.state.count 的方式获取
- state 更新方式：在函数组件中通过 setCount 更新，类组件通过 this.setState()

总的来讲，useState 使用起来更为简洁，减少了 this 指向不明确的情况

### useEffect

useEffect 可以让我们在函数组件中进行一些带有副作用的操作

同样给出一个计时器示例：

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }
  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

从上面可以看见，组件在加载和更新阶段都执行同样操作

而如果使用 useEffect 后，则能够将相同的逻辑抽离出来，这是类组件不具备的方法

对应的 useEffect 示例如下：

```jsx
import React, { useState, useEffect } from "react";
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

useEffect 第一个参数接受一个回调函数，默认情况下，useEffect 会在第一次渲染和更新之后都会执行，相当于在 componentDidMount 和 componentDidUpdate 两个生命周期函数中执行回调

如果某些特定值在两次重渲染之间没有发生变化，你可以跳过对 effect 的调用，这时候只需要传入第二个参数，如下：

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // 仅在 count 更改时更新
```

上述传入第二个参数后，如果 count 的值是 5，而且我们的组件重渲染的时候 count 还是等于 5，React 将对前一次渲染的 [5] 和后一次渲染的 [5] 进行比较，如果是相等则跳过 effects 执行

回调函数中可以返回一个清除函数，这是 effect 可选的清除机制，相当于类组件中 componentwillUnmount 生命周期函数，可做一些清除副作用的操作，如下：

```jsx
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
});
```

所以， useEffect 相当于 componentDidMount，componentDidUpdate 和 componentWillUnmount 这三个生命周期函数的组合

### useReducer

### useCallback

### useMemo

### useRef

## 3.函数组件

函数组件，顾名思义，就是通过函数编写的形式去实现一个 React 组件，是 React 中定义组件最简单的方式

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### 3.1 编写形式

函数第一个参数为 props 用于接收父组件传递过来的参数

```jsx
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### 3.2 状态管理

在 hooks 出来之前，函数组件就是无状态组件，不能保管组件的状态，不像类组件中调用 setState

### 3.3 生命周期

在 hooks 出来之前，函数组件没有生命周期

### 3.4 调用方式

如果是一个函数组件，调用则是执行函数即可：

```jsx
// 你的代码
function SayHi() {
  return <p>Hello, React</p>;
}
// React内部
const result = SayHi(props); // » <p>Hello, React</p >
```

### 3.5 获取渲染的值

首先给出一个示例

函数组件对应如下：

```jsx
function ProfilePage(props) {
  const showMessage = () => {
    alert("Followed " + props.user);
  };

  const handleClick = () => {
    setTimeout(showMessage, 3000);
  };

  return <button onClick={handleClick}>Follow</button>;
}
```

## 4.类组件

类组件，顾名思义，也就是通过使用 ES6 类的编写形式去编写组件，该类必须继承 React.Component

如果想要访问父组件传递过来的参数，可通过 this.props 的方式去访问

在组件中必须实现 render 方法，在 return 中返回 React 对象，如下：

```jsx
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### 4.1 编写形式

```jsx
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### 4.2 状态管理

state setstate

### 4.3 生命周期

### 4.4 调用方式

类组件，则需要将组件进行实例化，然后调用实例对象的 render 方法：

```jsx
// 你的代码
class SayHi extends React.Component {
  render() {
    return <p>Hello, React</p>;
  }
}
// React内部
const instance = new SayHi(props); // » SayHi {}
const result = instance.render(); // » <p>Hello, React</p >
```

### 4.5 获取渲染的值

```jsx
class ProfilePage extends React.Component {
  showMessage() {
    alert("Followed " + this.props.user);
  }

  handleClick() {
    setTimeout(this.showMessage.bind(this), 3000);
  }

  render() {
    return <button onClick={this.handleClick.bind(this)}>Follow</button>;
  }
}
```

## 5.RealDOM 和 VirtualDOM

### 5.1 是什么

Real DOM，真实 DOM，意思为文档对象模型，是一个结构化文本的抽象，在页面渲染出的每一个结点都是一个真实 DOM 结构。

Virtual Dom，本质上是以 JavaScript 对象形式存在的对 DOM 的描述。

创建虚拟 DOM 目的就是为了更好将虚拟的节点渲染到页面视图中，虚拟 DOM 对象的节点与真实 DOM 的属性一一照应。

在 React 中，JSX 是其一大特性，可以让你在 JS 中通过使用 XML 的方式去直接声明界面的 DOM 结构。

```js
// 创建 h1 标签，右边千万不能加引号
const vDom = <h1>Hello World</h1>;
// 找到 <div id="root"></div> 节点
const root = document.getElementById("root");
// 把创建的 h1 标签渲染到 root 节点上
ReactDOM.render(vDom, root);
```

上述中，ReactDOM.render() 用于将你创建好的虚拟 DOM 节点插入到某个真实节点上，并渲染到页面上

JSX 实际是一种语法糖，在使用过程中会被 babel 进行编译转化成 JS 代码，上述 VDOM 转化为如下：

```js
const vDom = React.createElement(
  'h1'，
  { className: 'hClass', id: 'hId' },
  'hello world'
)
```

可以看到，JSX 就是为了简化直接调用 React.createElement() 方法：

- 第一个参数是标签名，例如 h1、span、table...

- 第二个参数是个对象，里面存着标签的一些属性，例如 id、class 等

- 第三个参数是节点中的文本

通过 console.log(VDOM)，则能够得到虚拟 VDOM 消息

所以可以得到，JSX 通过 babel 的方式转化成 React.createElement 执行，返回值是一个对象，也就是虚拟 DOM

### 5.2 区别

两者的区别如下：

- 虚拟 DOM 不会进行排版与重绘操作，而真实 DOM 会频繁重排与重绘
- 虚拟 DOM 的总损耗是“虚拟 DOM 增删改+真实 DOM 差异增删改+排版与重绘”，真实 DOM 的总损耗是“真实 DOM 完全增删改+排版与重绘”

传统的原生 api 或 jQuery 去操作 DOM 时，浏览器会从构建 DOM 树开始从头到尾执行一遍流程

当你在一次操作时，需要更新 10 个 DOM 节点，浏览器没这么智能，收到第一个更新 DOM 请求后，并不知道后续还有 9 次更新操作，因此会马上执行流程，最终执行 10 次流程

而通过 VNode，同样更新 10 个 DOM 节点，虚拟 DOM 不会立即操作 DOM，而是将这 10 次更新的 diff 内容保存到本地的一个 js 对象中，最终将这个 js 对象一次性 attach 到 DOM 树上，避免大量的无谓计算

### 5.3 优缺点

真实 DOM 的优势：

- 易用

缺点：

- 效率低，解析速度慢，内存占用量过高
- 性能差：频繁操作真实 DOM，易于导致重绘与回流

使用虚拟 DOM 的优势如下：

- 简单方便：如果使用手动操作真实 DOM 来完成页面，繁琐又容易出错，在大规模应用下维护起来也很困难
- 性能方面：使用 Virtual DOM，能够有效避免真实 DOM 数频繁更新，减少多次引起重绘与回流，提高性能
- 跨平台：React 借助虚拟 DOM，带来了跨平台的能力，一套代码多端运行

缺点：

- 在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化
- 首次渲染大量 DOM 时，由于多了一层虚拟 DOM 的计算，速度比正常稍慢

## 6.super 和 super(props)

## 7.生命周期

### 7.1 旧的生命周期

在 React 16 版本之前，React 生命周期包括：

1. **Initialization（初始化）**：组件实例被创建并初始化状态。
   - `constructor(props)`：构造函数，用于初始化组件的状态和绑定方法。
   - `componentWillMount()`：在组件即将挂载到 DOM 之前被调用（已弃用，不推荐使用）。
2. **Mounting（挂载）**：组件被插入到 DOM 中。
   - `render()`：渲染函数，返回组件的 React 元素。
   - `componentDidMount()`：在组件挂载到 DOM 之后被调用。
3. **Updating（更新）**：组件更新并重新渲染。
   - Props
     - `componentWillReceiveProps(nextProps)`：在接收到新的 props 之前被调用（已弃用，不推荐使用）。
     - `shouldComponentUpdate(nextProps, nextState)`：在更新之前被调用，用于判断是否需要重新渲染组件。
     - `componentWillUpdate(nextProps, nextState)`：在更新之前被调用（已弃用，不推荐使用）。
     - `render()`
     - `componentDidUpdate(prevProps, prevState)`：在更新之后被调用。
   - States
     - `shouldComponentUpdate()`：在更新之前被调用，用于判断是否需要重新渲染组件。
     - `componentWillUpdate()`：在更新之前被调用（已弃用，不推荐使用）。
     - `render()`
     - `componentDidUpdate()`：在更新之后被调用。
4. **Unmounting（卸载）**：组件从 DOM 中移除。
   - `componentWillUnmount()`：在组件从 DOM 中移除之前被调用。

需要注意的是，一些生命周期方法（如 `componentWillMount`、`componentWillReceiveProps`、`componentWillUpdate`）已经被标记为过时（deprecated），不建议在新的代码中使用，而是推荐使用它们的替代方法。

React 团队淘汰某些生命周期钩子的原因主要有以下几点：

1. **副作用难以管理**：一些生命周期钩子存在副作用，例如在 `componentWillMount` 中进行数据获取，容易导致组件渲染时出现逻辑混乱或数据不一致的问题。随着 React 生态的发展，更多的解决方案（如 Hooks）出现，能够更清晰地管理组件的副作用。

2. **性能优化难度**：某些生命周期钩子的存在会增加组件的重渲染次数，例如 `componentWillReceiveProps` 和 `componentWillUpdate`，这会导致不必要的性能损耗。为了提高性能并降低副作用，React 团队决定废弃这些生命周期钩子。

3. **统一性和易用性**：React 团队希望提供一种更加统一和易用的开发体验，使得开发者能够更容易地理解和管理组件的生命周期。废弃一些生命周期钩子能够使得 React 的 API 更加简洁和一致，同时也有利于未来框架的维护和更新。

总的来说，React 团队的决策是为了提高开发效率、降低维护成本，并使得 React 应用更加可靠和稳定。

### 7.2 新的生命周期

#### 创建阶段

- constructor

  实例过程中自动调用的方法，在方法内部通过 super 关键字获取来自父组件的 props

  在该方法中，通常的操作为初始化 state 状态或者在 this 上挂载方法

- getDerivedStateFromProps

  该方法是新增的生命周期方法，是一个静态的方法，因此不能访问到组件的实例

  执行时机：组件创建和更新阶段，不论是 props 变化还是 state 变化，也会调用

  在每次 render 方法前调用，第一个参数为即将更新的 props，第二个参数为上一个状态的 state，可以比较 props 和 state 来加一些限制条件，防止无用的 state 更新

  该方法需要返回一个新的对象作为新的 state 或者返回 null 表示 state 状态不需要更新

- render

  类组件必须实现的方法，用于渲染 DOM 结构，可以访问组件 state 与 prop 属性

  注意： 不要在 render 里面 setState, 否则会触发死循环导致内存崩溃

- componentDidMount

  组件挂载到真实 DOM 节点后执行，其在 render 方法之后执行

  此方法多用于执行一些数据获取，事件监听等操作

#### 更新阶段

该阶段的函数主要为如下方法：

- getDerivedStateFromProps

  该方法是新增的生命周期方法，是一个静态的方法，因此不能访问到组件的实例

  执行时机：组件创建和更新阶段，不论是 props 变化还是 state 变化，也会调用

  在每次 render 方法前调用，第一个参数为即将更新的 props，第二个参数为上一个状态的 state，可以比较 props 和 state 来加一些限制条件，防止无用的 state 更新

  该方法需要返回一个新的对象作为新的 state 或者返回 null 表示 state 状态不需要更新

- shouldComponentUpdate

  用于告知组件本身基于当前的 props 和 state 是否需要重新渲染组件，默认情况返回 true

  执行时机：到新的 props 或者 state 时都会调用，通过返回 true 或者 false 告知组件更新与否

  一般情况，不建议在该周期方法中进行深层比较，会影响效率

  同时也不能调用 setState，否则会导致无限循环调用更新

- render

  类组件必须实现的方法，用于渲染 DOM 结构，可以访问组件 state 与 prop 属性

  注意： 不要在 render 里面 setState, 否则会触发死循环导致内存崩溃

- getSnapshotBeforeUpdate

  该周期函数在 render 后执行，执行之时 DOM 元素还没有被更新

  该方法返回的一个 Snapshot 值，作为 componentDidUpdate 第三个参数传入

  ```js
  getSnapshotBeforeUpdate(prevProps, prevState) {
      console.log('#enter getSnapshotBeforeUpdate');
      return 'foo';
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
      console.log('#enter componentDidUpdate snapshot = ', snapshot);
  }
  ```

  此方法的目的在于获取组件更新前的一些信息，比如组件的滚动位置之类的，在组件更新后可以根据这些信息恢复一些 UI 视觉上的状态

- componentDidUpdate

  执行时机：组件更新结束后触发

  在该方法中，可以根据前后的 props 和 state 的变化做相应的操作，如获取数据，修改 DOM 样式等

#### 卸载阶段

- componentWillUnmount

  此方法用于组件卸载前，清理一些注册是监听事件，或者取消订阅的网络请求等

  一旦一个组件实例被卸载，其不会被再次挂载，而只可能是被重新创建

## 8.state 和 props

### 8.1 state

一个组件的显示形态可以由数据状态和外部参数所决定，而数据状态就是 state，一般在 constructor 中初始化

当需要修改里面的值的状态需要通过调用 setState 来改变，从而达到更新组件内部数据的作用，并且重新调用组件 render 方法，如下面的例子：

```jsx
class Button extends React.Component {
  constructor() {
    super();
    this.state = {
      count: 0,
    };
  }

  updateCount() {
    this.setState((prevState, props) => {
      return { count: prevState.count + 1 };
    });
  }

  render() {
    return (
      <button onClick={() => this.updateCount()}>
        Clicked {this.state.count} times
      </button>
    );
  }
}
```

setState 还可以接受第二个参数，它是一个函数，会在 setState 调用完成并且组件开始重新渲染时被调用，可以用来监听渲染是否完成

```jsx
this.setState(
  {
    name: "JS 每日一题",
  },
  () => console.log("setState finished")
);
```

### 8.2 props

React 的核心思想就是组件化思想，页面会被切分成一些独立的、可复用的组件

组件从概念上看就是一个函数，可以接受一个参数作为输入值，这个参数就是 props，所以可以把 props 理解为从外部传入组件内部的数据

react 具有单向数据流的特性，所以他的主要作用是从父组件向子组件中传递数据

props 除了可以传字符串，数字，还可以传递对象，数组甚至是回调函数，如下：

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello {this.props.name}</h1>;
  }
}

const element = <Welcome name="Sara" onNameChanged={this.handleName} />;
```

上述 name 属性与 onNameChanged 方法都能在子组件的 props 变量中访问

在子组件中，props 在内部不可变的，如果想要改变它看，只能通过外部组件传入新的 props 来重新渲染子组件，否则子组件的 props 和展示形式不会改变

### 8.3 区别

相同点：

- 两者都是 JavaScript 对象
- 两者都是用于保存信息
- props 和 state 都能触发渲染更新

区别：

- props 是外部传递给组件的，而 state 是在组件内被组件自己管理的，一般在 constructor 中初始化
- props 在组件内部是不可修改的，但 state 在组件内部可以进行修改
- state 是多变的、可以修改

## 9.事件绑定方式

在 react 应用中，事件名都是用小驼峰格式进行书写，例如 onclick 要改写成 onClick

最简单的事件绑定如下：

```jsx
class ShowAlert extends React.Component {
  showAlert() {
    console.log("Hi");
  }

  render() {
    return <button onClick={this.showAlert}>show</button>;
  }
}
```

从上面可以看到，事件绑定的方法需要使用{}包住

上述的代码看似没有问题，但是当将处理函数输出代码换成 console.log(this)的时候，点击按钮，则会发现控制台输出 undefined

为了解决上面正确输出 this 的问题，常见的绑定方式有如下：

- render 方法中使用 bind
- render 方法中使用箭头函数
- constructor 中 bind
- 定义阶段使用箭头函数绑定

### render 方法中使用 bind

如果使用一个类组件，在其中给某个组件/元素一个 onClick 属性，它现在并会自定绑定其 this 到当前组件，解决这个问题的方法是在事件函数后使用.bind(this)将 this 绑定到当前组件中

```jsx
class App extends React.Component {
  handleClick() {
    console.log("this > ", this);
  }
  render() {
    return <div onClick={this.handleClick.bind(this)}>test</div>;
  }
}
```

这种方式在组件每次 render 渲染的时候，都会重新进行 bind 的操作，影响性能

### render 方法中使用箭头函数

通过 ES6 的上下文来将 this 的指向绑定给当前组件，同样再每一次 render 的时候都会生成新的方法，影响性能

```jsx
class App extends React.Component {
  handleClick() {
    console.log("this > ", this);
  }
  render() {
    return <div onClick={(e) => this.handleClick(e)}>test</div>;
  }
}
```

### constructor 中 bind

在 constructor 中预先 bind 当前组件，可以避免在 render 操作中重复绑定

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    console.log("this > ", this);
  }
  render() {
    return <div onClick={this.handleClick}>test</div>;
  }
}
```

### 定义阶段使用箭头函数绑定

跟上述方式三一样，能够避免在 render 操作中重复绑定，实现也非常的简单，如下：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  handleClick = () => {
    console.log("this > ", this);
  };
  render() {
    return <div onClick={this.handleClick}>test</div>;
  }
}
```

## 10.组件通信方式

我们将组件间通信可以拆分为两个词：

- 组件
- 通信

相比 vue，React 的组件更加灵活和多样，按照不同的方式可以分成很多类型的组件

而通信指的是发送者通过某种媒体以某种格式来传递信息到收信者以达到某个目的，广义上，任何信息的交通都是通信

组件间通信即指组件通过某种方式来传递信息以达到某个目的

### 如何通信

组件传递的方式有很多种，根据传送者和接收者可以分为如下：

- 父组件向子组件传递
- 子组件向父组件传递
- 兄弟组件之间的通信
- 父组件向后代组件传递
- 非关系组件传递

#### 父组件向子组件传递

由于 React 的数据流动为单向的，父组件向子组件传递是最常见的方式

父组件在调用子组件的时候，只需要在子组件标签内传递参数，子组件通过 props 属性就能接收父组件传递过来的参数

```jsx
function EmailInput(props) {
  return (
    <label>
      Email: <input value={props.email} />
    </label>
  );
}

const element = <EmailInput email="123124132@163.com" />;
```

#### 子组件向父组件传递

子组件向父组件通信的基本思路是，父组件向子组件传一个函数，然后通过这个函数的回调，拿到子组件传过来的值

##### 父组件对应代码如下

```jsx
class Parents extends Component {
  constructor() {
    super();
    this.state = {
      price: 0,
    };
  }

  getItemPrice(e) {
    this.setState({
      price: e,
    });
  }

  render() {
    return (
      <div>
        <div>price: {this.state.price}</div>
        {/* 向子组件中传入一个函数  */}
        <Child getPrice={this.getItemPrice.bind(this)} />
      </div>
    );
  }
}
```

##### 子组件对应代码如下

```jsx
class Child extends Component {
  clickGoods(e) {
    // 在此函数中传入值
    this.props.getPrice(e);
  }

  render() {
    return (
      <div>
        <button onClick={this.clickGoods.bind(this, 100)}>goods1</button>
        <button onClick={this.clickGoods.bind(this, 1000)}>goods2</button>
      </div>
    );
  }
```

#### 兄弟组件之间的通信

如果是兄弟组件之间的传递，则父组件作为中间层来实现数据的互通，通过使用父组件传递

```js
class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }
  setCount = () => {
    this.setState({ count: this.state.count + 1 });
  };
  render() {
    return (
      <div>
        <SiblingA count={this.state.count} />
        <SiblingB onClick={this.setCount} />
      </div>
    );
  }
}
```

#### 父组件向后代组件传递

父组件向后代组件传递数据是一件最普通的事情，就像全局数据一样

使用 context 提供了组件之间通讯的一种方式，可以共享数据，其他数据都能读取对应的数据

通过使用 React.createContext 创建一个 context

```jsx
const PriceContext = React.createContext("price");
```

context 创建成功后，其下存在 Provider 组件用于创建数据源，Consumer 组件用于接收数据，使用实例如下：

Provider 组件通过 value 属性用于给后代组件传递数据：

```jsx
<PriceContext.Provider value={100}></PriceContext.Provider>
```

如果想要获取 Provider 传递的数据，可以通过 Consumer 组件或者或者使用 contextType 属性接收，对应分别如下：

```jsx
class MyClass extends React.Component {
  static contextType = PriceContext;
  render() {
    let price = this.context;
    /* 基于这个值进行渲染工作 */
  }
}
```

Consumer 组件：

```jsx
<PriceContext.Consumer>
  {/*这里是一个函数*/}
  {(price) => <div>price：{price}</div>}
</PriceContext.Consumer>
```

#### 非关系组件传递

如果组件之间关系类型比较复杂的情况，建议将数据进行一个全局资源管理，从而实现通信，例如 redux。关于 redux 的使用后续再详细介绍

## 12.key 的作用

首先，先给出 react 组件中进行列表渲染的一个示例：

```jsx
const data = [
  { id: 0, name: "abc" },
  { id: 1, name: "def" },
  { id: 2, name: "ghi" },
  { id: 3, name: "jkl" },
];

const ListItem = (props) => {
  return <li>{props.name}</li>;
};

const List = () => {
  return (
    <ul>
      {data.map((item) => (
        <ListItem name={item.name}></ListItem>
      ))}
    </ul>
  );
};
```

然后在输出就可以看到 react 所提示的警告信息：

Each child in a list should have a unique "key" prop.
根据意思就可以得到渲染列表的每一个子元素都应该需要一个唯一的 key 值

在这里可以使用列表的 id 属性作为 key 值以解决上面这个警告

```jsx
const List = () => {
  return (
    <ul>
      {data.map((item) => (
        <ListItem name={item.name} key={item.id}></ListItem>
      ))}
    </ul>
  );
};
```

作用
跟 Vue 一样，React 也存在 Diff 算法，而元素 key 属性的作用是**用于判断元素是新创建的还是被移动的元素，从而减少不必要的元素渲染**

因此 key 的值需要为每一个元素赋予一个确定的标识

如果列表数据渲染中，在数据后面插入一条数据，key 作用并不大，如下：

```jsx
this.state = {
numbers:[111,222,333]
}

insertMovie() {
const newMovies = [...this.state.numbers, 444];
this.setState({
movies: newMovies
})
}

<ul>
    {
        this.state.movies.map((item, index) => {
            return <li>{item}</li>
        })
    }
</ul>
```

前面的元素在 diff 算法中，前面的元素由于是完全相同的，并不会产生删除创建操作，在最后一个比较的时候，则需要插入到新的 DOM 树中

因此，在这种情况下，元素有无 key 属性意义并不大

下面再来看看在前面插入数据时，使用 key 与不使用 key 的区别：

```jsx
insertMovie() {
  const newMovies = [000 ,...this.state.numbers];
  this.setState({
    movies: newMovies
  })
}
```

当拥有 key 的时候，react 根据 key 属性匹配原有树上的子元素以及最新树上的子元素，像上述情况只需要将 000 元素插入到最前面位置

当没有 key 的时候，所有的 li 标签都需要进行修改

同样，并不是拥有 key 值代表性能越高，如果说只是文本内容改变了，不写 key 反而性能和效率更高

主要是因为不写 key 是将所有的文本内容替换一下，节点不会发生变化

而写 key 则涉及到了节点的增和删，发现旧 key 不存在了，则将其删除，新 key 在之前没有，则插入，这就增加性能的开销

## 14.受控组件和非受控组件

## 15.高阶组件（HOC）

**高阶组件（Higher-Order Component，HOC）** 是 React 中的一种用于复用组件逻辑的模式。它是一个函数，接收一个组件作为参数，并返回一个新的组件。

### **高阶组件的定义**

HOC 是一个纯函数，它并不修改传入的组件，而是通过组合方式，扩展其功能并返回一个增强后的组件。它常用于以下场景：

- 代码复用、逻辑抽象
- 渲染劫持
- 状态管理
- 增强组件的性能

其定义形式如下：

```js
const higherOrderComponent = (WrappedComponent) => {
  class HOC extends React.Component {
    render() {
      return <WrappedComponent {...this.props} />;
    }
  }
  return HOC;
};
```

### **工作原理**

1. **接收组件**：HOC 接收一个 React 组件（称为 `WrappedComponent`）。
2. **增强逻辑**：在 HOC 内部，可以在渲染前、渲染后、或者修改传递给 `WrappedComponent` 的 props，添加增强逻辑。
3. **返回增强组件**：HOC 返回一个新的组件，这个组件包裹了原始的 `WrappedComponent`，并且可以根据需要进行扩展。

### **常见使用场景**

#### 1. **逻辑复用**

高阶组件最常见的用途是共享组件之间的逻辑。例如，多个组件可能需要访问相同的数据源或响应相同的事件处理逻辑。你可以通过 HOC 将这些逻辑抽象出来并复用。

```js
const withLogger = (WrappedComponent) => {
  return class extends React.Component {
    componentDidMount() {
      console.log("Component has mounted");
    }
    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
};

// 使用 HOC
const ButtonWithLogger = withLogger(Button);
```

#### 2. **条件渲染**

高阶组件可以用于条件渲染。你可以在 HOC 中控制是否渲染 `WrappedComponent`，或者在渲染之前执行一些预处理。

```js
const withLoading = (WrappedComponent) => {
  return function WithLoadingComponent({ isLoading, ...props }) {
    if (isLoading) {
      return <div>Loading...</div>;
    }
    return <WrappedComponent {...props} />;
  };
};

// 使用 HOC
const UserListWithLoading = withLoading(UserList);
```

#### 3. **操作 props**

HOC 可以修改传递给 `WrappedComponent` 的 props，增加额外的功能。例如，注入一些额外的配置或数据。

```js
const withExtraProps = (WrappedComponent) => {
  return function (props) {
    return <WrappedComponent {...props} extraProp="Injected Prop" />;
  };
};

// 使用 HOC
const EnhancedComponent = withExtraProps(MyComponent);
```

### **HOC 的注意事项**

1. **不要在 `render` 方法中调用 HOC**：每次 `render` 重新调用 HOC 会导致组件树重新创建，这会影响性能。应该在组件外部定义 HOC，确保只在组件创建时调用一次。

2. **避免 `ref` 丢失**：HOC 不会自动传递 `ref`。如果需要访问包裹组件的 DOM 节点或实例，可以使用 `React.forwardRef`。

3. **保持静态方法和属性**：HOC 包装组件时，会丢失原始组件的静态方法和属性。可以使用 `hoist-non-react-statics` 库将静态方法从 `WrappedComponent` 复制到 HOC。

### **HOC 的实际使用**

HOC 被广泛用于第三方库中，比如 Redux 的 `connect` 函数，就是一个经典的 HOC 用法。

```js
import { connect } from "react-redux";

const mapStateToProps = (state) => ({
  user: state.user,
});

const mapDispatchToProps = (dispatch) => ({
  login: () => dispatch(loginAction()),
});

// 使用 HOC 连接 Redux 状态和动作到组件
const ConnectedComponent = connect(
  mapStateToProps,
  mapDispatchToProps
)(MyComponent);
```

### **总结**

高阶组件是一种强大的模式，允许你通过组合的方式来复用逻辑，而不是重复编写相同的代码。虽然 React 也引入了其他技术（如 Hooks）来复用逻辑，但 HOC 仍然是 React 生态中的一个重要工具。

## 19.React DIFF 的原理

React 的 **Diff 算法** 是 React 在虚拟 DOM 更新过程中，用于高效比较新旧虚拟 DOM 树差异的一种算法。它的核心目标是 **最小化对真实 DOM 的操作**，从而提升性能。React 的 Diff 算法遵循一系列优化规则来快速识别变化的节点，避免不必要的 DOM 更新。

### **React Diff 的工作原理**

React 的 Diff 算法并不是通用的树对比算法，因为通用算法的复杂度较高。为了提高效率，React 使用了一些 **假设和策略** 来简化对比过程，使时间复杂度从 O(n^3) 降低到 O(n)。

### **1. 同层级比较**

React 的 Diff 算法假设 **节点之间的变化只会发生在同一个层级上**，不会跨层级移动节点。例如，React 只会比较同一层级的子节点，而不会递归比较所有节点。

### **2. 不同节点类型的直接替换**

React 认为，如果两个节点的类型不同，就认为这两个节点是完全不同的元素，不会尝试复用，直接销毁旧节点并创建新节点。

- 如果新旧节点类型相同，React 会保留节点，并比较其属性和子节点。
- 如果新旧节点类型不同，React 会卸载旧节点，并插入一个新节点。

例如：

```jsx
<div>Old Content</div>
// 被更新为
<span>New Content</span>
```

React 认为 `<div>` 和 `<span>` 是不同类型的元素，因此它会卸载 `<div>` 并新建 `<span>`，不会尝试复用。

### **3. 比较同类型节点的属性**

对于同类型的元素，React 会对它们的属性进行逐一比较，找出需要更新的部分。例如：

```jsx
<div className="old" />
// 被更新为
<div className="new" />
```

React 会只更新 `className` 属性，而不会重新创建整个 `div` 元素。

### **4. 对比子节点**

对于子节点，React 通过以下三种策略来优化对比过程：

- **逐一对比**：React 会从左到右依次对比每个子节点。如果发现相同位置的节点类型相同，则只更新属性。
- **“Key” 优化**：React 提供了 `key` 属性，帮助唯一标识列表中的元素。使用 `key` 能够帮助 React 更加精确地识别哪些子节点被移动、添加或删除，从而提高对比的效率。

  如果没有 `key`，React 会默认按照节点的顺序进行比较，这在处理有序列表时可能导致性能问题和不必要的 DOM 操作。`key` 能够有效避免重新渲染整个列表。

### **5. 节点的插入、删除和移动**

- **插入节点**：React 发现新的虚拟 DOM 中存在旧虚拟 DOM 没有的节点时，会创建并插入新的节点。
- **删除节点**：如果旧虚拟 DOM 中的节点在新虚拟 DOM 中不存在，React 会将这个节点从真实 DOM 中移除。
- **移动节点**：如果新旧虚拟 DOM 的顺序发生了变化，React 会通过 `key` 确定哪些节点需要移动，并尽可能减少 DOM 操作。

### **Diff 算法的具体过程**

假设有两个组件对应的虚拟 DOM 结构：

**旧虚拟 DOM**:

```jsx
<ul>
  <li key="A">A</li>
  <li key="B">B</li>
  <li key="C">C</li>
</ul>
```

**新虚拟 DOM**:

```jsx
<ul>
  <li key="B">B</li>
  <li key="C">C</li>
  <li key="A">A</li>
</ul>
```

React 通过 `key` 来标识每个节点，比较的过程如下：

1. React 发现 `B` 和 `C` 都存在于新旧虚拟 DOM 中，且 `key` 相同，因此保留这些节点。
2. React 发现 `A` 节点在新虚拟 DOM 中移动了位置，于是 React 会将 `A` 节点移动到新位置，而不会重新创建 `A` 节点。
3. React 只执行必要的节点移动操作，最小化对真实 DOM 的修改。

### **Key 的作用**

在 React 中，`key` 属性用于帮助 React 更高效地识别哪些节点发生了变化，避免不必要的重渲染。当渲染列表或可变动的元素时，`key` 提供了对每个元素的唯一标识，使得 React 可以根据 `key` 的变化进行节点的插入、删除和重新排序。

- 没有 `key` 或使用索引作为 `key` 时，React 会根据元素位置依次对比，这可能导致错误的重渲染。
- 使用唯一且稳定的 `key`（例如数据库 ID）能提高性能，准确更新节点。

例如：

```jsx
const list = [1, 2, 3, 4];
list.map((item) => <li key={item.toString()}>{item}</li>);
```

### **Diff 算法的性能优势**

1. **O(n) 复杂度**：由于 React 只比较同级元素，并通过 `key` 进行优化，其 Diff 算法的复杂度为 O(n)，其中 n 是节点数。相比于传统的 O(n^3) 复杂度的树比较算法，React 的 Diff 算法在实际应用中极大提升了性能。

2. **最小化 DOM 操作**：React 通过虚拟 DOM 和 Diff 算法，在更新过程中只修改有变化的部分，减少了直接操作真实 DOM 的开销。由于操作 DOM 是性能瓶颈所在，减少操作次数能够显著提高应用性能。

---

### **总结**

- React 通过虚拟 DOM 和 Diff 算法来高效更新页面，避免了直接操作真实 DOM 的性能开销。
- React 的 Diff 算法遵循一系列优化策略：同层级比较、同类型元素直接对比属性、通过 `key` 标识节点，尽可能减少 DOM 操作。
- 这些策略使得 React 的 Diff 算法复杂度为 O(n)，可以快速处理大量节点更新，并提升渲染性能。

Diff 算法是 React 的核心之一，它帮助 React 高效地更新用户界面，使得 React 在构建复杂的动态应用时具有出色的性能表现。

## 20.Fiber 架构

**Fiber** 是 React 16 引入的一种新的架构，旨在解决 React 在大型复杂应用中的性能和用户体验问题。React 通过 Fiber 改变了更新和渲染任务的调度方式，使得 React 在处理复杂更新时更加灵活和高效。

### **1. Fiber 是什么？**

**Fiber** 是 React 中一种用于管理组件更新的**数据结构和渲染架构**。它将 React 的更新过程拆分成了**更小的任务单元**，使得渲染任务可以被中断、暂停、恢复、甚至是重新执行，类似于操作系统中的“协程”（coroutines）或者“线程”。

每个 Fiber 对象对应一个组件，包含了有关该组件的所有信息，比如状态、props、DOM 结构等。它以链表的形式组织起来，形成一个 **Fiber 树**，代替了 React 原来的虚拟 DOM 树。

### **2. 为什么要引入 Fiber？**

引入 Fiber 是为了解决**性能问题**，特别是以下几个方面：

1. **同步渲染的局限性**：在 React 引入 Fiber 之前，React 是**同步渲染**的。也就是说，当你触发一次状态更新时，React 会从根节点开始，一直递归遍历整个虚拟 DOM 树，直到所有组件都完成更新。这种同步渲染意味着，React 在处理复杂的、深层嵌套的组件树时，可能会导致浏览器主线程被长时间阻塞，导致用户界面出现卡顿或延迟。

2. **任务优先级的缺乏**：在传统的 React 中，所有更新都是同步且平等的。无论是用户的交互事件（如点击、输入）还是复杂组件的渲染更新，React 都没有办法区分它们的优先级，所有任务都会一次性执行，无法中途暂停。这导致了用户体验不佳，特别是在处理动画、用户输入等高优先级任务时。

3. **无法分片的更新任务**：React 的更新任务是不可拆分的，如果一个复杂的更新任务需要很长时间才能完成，那么在此期间用户的输入或其他操作将无法被及时响应。

### **3. Fiber 解决了什么问题？**

引入 Fiber 后，React 解决了以下问题：

1. **可中断的渲染**：Fiber 允许 React 的渲染过程被中断和恢复。这意味着当浏览器需要处理其他高优先级的任务（例如用户输入）时，React 可以暂停渲染，优先处理这些任务，之后再继续渲染未完成的部分。这样避免了长时间的 UI 卡顿问题。

2. **任务优先级调度**：Fiber 让 React 能够为不同的任务分配不同的优先级。比如用户输入、动画更新等高优先级任务会被优先处理，而渲染更新等可以稍后执行。React 内部引入了一个**调度器（Scheduler）**，根据任务的重要性和紧急性来安排它们的执行顺序。

3. **分片的渲染**：通过 Fiber，React 的更新过程可以被拆分为多个“渲染单元”，这些单元可以在浏览器空闲的时间段内执行，从而避免主线程被长时间占用。这种机制被称为 **“时间切片（Time Slicing）”**，它保证了 React 的更新过程更加流畅。

### **4. 在引入 Fiber 之前，React 是如何工作的？**

在引入 Fiber 之前，React 使用的是**同步渲染**，也就是说每次状态更新时，React 会从根节点开始，递归遍历整个虚拟 DOM 树。以下是传统 React 的工作方式：

1. **递归遍历虚拟 DOM**：在没有 Fiber 之前，React 使用的是基于递归的算法，一旦更新触发，React 会从根节点一直向下遍历整个组件树，无论组件树有多复杂，更新是**一次性**完成的。

2. **阻塞式渲染**：这种方式的主要问题是，React 的更新是不可中断的，如果组件树非常深，更新过程可能会持续很长时间。在这段时间里，浏览器的主线程被完全占用，用户的输入、交互等操作会被卡住，导致用户体验不佳。

3. **没有任务优先级**：传统的 React 对不同的任务一视同仁，无论是渲染更新还是用户输入，都没有优先级的区分，这意味着 React 无法对关键任务（如用户输入、动画）优先处理。

### **5. Fiber 的具体改进**

引入 Fiber 后，React 的渲染机制得到了显著改进：

1. **Fiber 树**：Fiber 树是一个与组件树一一对应的数据结构，它是链表形式的，每个 Fiber 节点代表一个组件或 DOM 节点。Fiber 树的结构允许 React 更灵活地控制渲染过程。

2. **增量渲染**：React 可以在 Fiber 树的基础上对更新进行拆分，逐步渲染，不再一次性完成整个更新任务。通过这种**增量渲染**，React 可以在浏览器空闲时间执行更新任务，从而避免主线程的长时间阻塞。

3. **优先级调度**：React 为不同的任务引入了优先级系统，允许 React 在高优先级的任务（如用户输入）与低优先级的任务（如渲染）之间进行灵活调度。

4. **中断与恢复**：Fiber 允许 React 在中途暂停渲染任务，等到浏览器空闲时再恢复未完成的渲染工作。这种灵活性大大提高了 React 的响应速度。

### **6. Fiber 的核心原理**

Fiber 通过引入**链表结构**来代替传统树结构，每个 Fiber 节点指向下一个兄弟节点和父节点，使得 React 可以灵活地在 Fiber 树中移动，而不是像传统树那样进行深度优先遍历。此外，Fiber 还将每个渲染任务**拆分成多个小的单元任务**，并使用调度器来动态管理这些任务的执行。

Fiber 是一种调度机制的实现，它能够通过任务的优先级，合理分配时间片来执行渲染任务。

### **总结**

**Fiber** 是 React 的一个重大架构改进，引入它的主要原因是为了解决同步渲染带来的性能问题，特别是在大型应用中可能引发的卡顿和用户体验不佳。Fiber 通过可中断的渲染、任务优先级调度和增量更新等机制，让 React 能够更灵活地处理复杂更新，显著提升了应用的响应速度和流畅性。

## 21.React 中 render 方法的原理

## 22.渲染流程

当使用 React 构建的应用程序通过浏览器访问时，页面从服务器返回到最终渲染到浏览器中的过程，涉及到 React 的客户端渲染（CSR）和服务器端渲染（SSR）两种不同模式。这里我们重点梳理 **React 文件** 从服务器返回到页面渲染的流程，涵盖了两种模式。

### **React 客户端渲染（CSR）流程**

1. **用户请求页面**：

   - 用户在浏览器中输入 URL，浏览器向服务器发送 HTTP 请求。

2. **服务器返回基础 HTML 文件**：

   - 服务器响应请求，返回一个基础的 HTML 文件，通常只包含一个 `div` 容器（例如 `<div id="root"></div>`），以及指向打包的 JavaScript 文件的 `<script>` 标签。

3. **浏览器下载 JavaScript 文件**：

   - 浏览器解析 HTML，并开始下载 HTML 中引用的 JavaScript 文件（通常是打包后的 React 代码），这些 JavaScript 文件中包含了 React 组件和框架的核心逻辑。

4. **React 初始化**：

   - 浏览器下载并执行 React 的 JavaScript 代码，React 的虚拟 DOM 开始构建，并通过 `ReactDOM.render` 将组件渲染到 `root` 容器中。
   - React 会根据组件的结构生成虚拟 DOM 树（Virtual DOM），然后将其渲染为实际的 DOM 元素。

5. **页面内容渲染**：

   - 当 JavaScript 代码完成后，React 将生成的实际 DOM 插入到 `root` 容器中，浏览器显示页面内容。此时，用户可以看到页面并与之交互。

6. **用户交互与后续操作**：
   - React 通过虚拟 DOM 进行高效的 DOM 更新。用户的交互（如点击、输入）会通过事件监听器触发状态更新，React 会根据状态变化计算新的虚拟 DOM，并只更新有差异的部分。

#### **React 客户端渲染的关键点**

- 页面初始加载时，HTML 仅包含基本的框架，内容需要依赖 JavaScript 动态生成。
- **首屏渲染延迟**：因为浏览器必须等待 JavaScript 加载完成后才能渲染页面内容，因此首屏可能会有一定的加载延迟。
- **SEO 不友好**：由于 HTML 中没有直接的内容，搜索引擎爬虫可能无法有效抓取页面内容。

---

### **React 服务器端渲染（SSR）流程**

React 服务器端渲染（SSR）通过服务器预先生成 HTML，将其直接发送给浏览器，提升首屏渲染速度。

1. **用户请求页面**：

   - 用户在浏览器中输入 URL，浏览器向服务器发送 HTTP 请求。

2. **服务器执行 React 代码**：

   - 服务器接收到请求后，执行 React 代码。服务器会调用 `ReactDOMServer.renderToString()`，将 React 组件渲染为一个完整的 HTML 字符串。
   - 服务器生成的 HTML 包含完整的页面结构和内容，而不是像客户端渲染那样仅仅返回一个空的 `div` 容器。

3. **服务器返回完整的 HTML 页面**：

   - 服务器将生成的 HTML 页面返回给浏览器。这个 HTML 页面已经包含了渲染好的内容，因此浏览器可以立即显示页面，而无需等待 JavaScript 的加载。

4. **浏览器渲染 HTML 页面**：

   - 浏览器接收到 HTML 后，直接解析并渲染页面内容。此时用户可以看到页面的首屏内容。

5. **浏览器下载 JavaScript 文件并进行“水合”（Hydration）**：

   - 浏览器在渲染 HTML 页面后，继续下载 HTML 中引用的 React JavaScript 文件。
   - 一旦 JavaScript 文件下载完成，React 开始执行“水合”（Hydration）过程。Hydration 是指 React 将已经渲染好的静态 HTML 与 React 的虚拟 DOM 进行关联，确保页面具备交互能力。
   - React 在不重新创建 DOM 的情况下，将事件监听器等交互逻辑绑定到已有的 DOM 元素上。

6. **用户交互与后续操作**：
   - 完成水合后，用户可以像在客户端渲染一样与页面进行交互。React 的虚拟 DOM 机制在后续的交互中继续发挥作用，更新页面内容。

#### **React 服务器端渲染的关键点**

- **首屏渲染快**：因为服务器直接返回渲染好的 HTML，用户在首屏阶段就能看到页面内容。
- **SEO 友好**：页面的 HTML 中已经包含了内容，搜索引擎可以直接抓取这些内容，提升 SEO 效果。
- **水合过程**：在浏览器渲染完 HTML 之后，React 会进行“水合”，绑定事件处理逻辑，使页面具备交互性。

---

### **CSR 与 SSR 的对比**

| **流程步骤**        | **CSR（客户端渲染）**                                        | **SSR（服务器端渲染）**                                    |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| **服务器响应**      | 返回基础 HTML 和打包的 JavaScript 文件                       | 服务器直接返回渲染好的 HTML 页面                           |
| **首屏渲染**        | 等待 JavaScript 加载完成后，React 才能生成页面并渲染         | 服务器直接返回可见内容，首屏渲染快                         |
| **JavaScript 加载** | 页面内容依赖于 JavaScript 动态生成，必须等其加载完成才能渲染 | 页面内容在 JavaScript 加载前已经渲染，之后水合绑定交互功能 |
| **SEO 支持**        | 内容由 JavaScript 动态生成，SEO 效果较差                     | 页面包含内容，SEO 友好                                     |
| **用户交互**        | 通过 React 虚拟 DOM 实现动态更新                             | 需要水合后，用户交互逻辑与 CSR 类似                        |
| **开发复杂度**      | 开发简单，主要在客户端处理渲染和交互                         | 开发较为复杂，需要处理服务器端与客户端的渲染逻辑           |

### **混合渲染：SSR + CSR**

在 React 中，混合渲染方式很常见，尤其是使用 Next.js 等框架。页面初始使用 SSR 加载，提供快速的首屏渲染和 SEO 支持，之后通过 CSR 提供更快的页面更新和用户交互。

这种混合方式既能利用 SSR 的首屏优化优势，又能使用 CSR 提供的高效交互体验。

### **原生 JS 渲染**

使用原生 HTML、CSS、JavaScript（无框架）开发的页面渲染流程更加直接：

1. 用户请求页面：

   - 用户在浏览器中输入 URL，浏览器发送 HTTP 请求到服务器。

2. 服务器返回完整的 HTML 文件：

   - 服务器返回一个完整的 HTML 文件，里面包含所有的静态页面内容，以及引用的 CSS 和 JavaScript 文件（如果有）。

3. 浏览器解析并渲染 HTML：

   - 浏览器从上到下解析 HTML 文件，遇到 \<link> 标签时下载 CSS 文件，遇到 \<script> 标签时下载并执行 JavaScript 文件。
   - 浏览器根据 HTML 的内容直接生成 DOM 树，根据 CSS 生成 CSSOM（CSS Object Model），并将两者结合生成渲染树。
   - 浏览器根据渲染树进行布局（Layout），计算各个元素的位置和大小，接着绘制页面（Paint）。

4. 页面显示：
   - 页面内容已经被浏览器渲染，用户可以看到并与页面进行交互。
5. JavaScript 处理交互：
   - 如果页面中有 JavaScript 代码，它将负责处理用户的交互，例如表单验证、按钮点击事件等。JavaScript 可以直接操作 DOM，动态更新页面内容。

原生前端页面渲染的特点：

- 直接渲染：服务器返回的是完整的 HTML 内容，浏览器只需要解析和渲染即可，因此首屏渲染速度通常很快。
- DOM 操作：使用原生 JavaScript 操作 DOM 可能会比较繁琐，需要手动查询元素并更新内容。
- 状态管理复杂：如果页面状态复杂，使用原生 JavaScript 进行状态管理和页面更新会增加代码复杂度。
- 页面切换方式：传统的页面切换方式通常是通过刷新整个页面，或者使用 window.location 进行导航，不像 React 这样的前端框架可以通过虚拟 DOM 和路由实现局部更新。

## 23.diff 的伪代码

理解 React 的 Diff 算法后，手写其伪代码可以帮助理解核心流程。以下是简化版的 Diff 算法伪代码，用于对比新旧虚拟 DOM 树，并生成更新操作列表：

### **伪代码结构**

```js
function diff(oldTree, newTree) {
  // 初始化补丁对象
  let patches = {};

  // 从根节点开始对比，index 从 0 开始
  walk(oldTree, newTree, 0, patches);

  // 返回生成的补丁集
  return patches;
}

function walk(oldNode, newNode, index, patches) {
  let currentPatch = [];

  // 如果新的节点不存在，说明该节点被删除
  if (newNode === null) {
    currentPatch.push({ type: "REMOVE", index });
  }
  // 如果旧节点是文本节点且新节点也是文本节点，比较文本内容
  else if (typeof oldNode === "string" && typeof newNode === "string") {
    if (oldNode !== newNode) {
      currentPatch.push({ type: "TEXT", text: newNode });
    }
  }
  // 如果节点类型不同，直接替换
  else if (oldNode.type !== newNode.type) {
    currentPatch.push({ type: "REPLACE", newNode });
  }
  // 如果节点类型相同，比较属性和子节点
  else {
    // 比较属性
    let attrsPatches = diffAttributes(oldNode.props, newNode.props);
    if (Object.keys(attrsPatches).length > 0) {
      currentPatch.push({ type: "ATTRS", attrs: attrsPatches });
    }

    // 递归比较子节点
    diffChildren(
      oldNode.children,
      newNode.children,
      index,
      patches,
      currentPatch
    );
  }

  // 如果有任何变化，将当前的补丁保存到 patches
  if (currentPatch.length > 0) {
    patches[index] = currentPatch;
  }
}

function diffAttributes(oldAttrs, newAttrs) {
  let patches = {};

  // 找出属性变化
  for (let key in oldAttrs) {
    if (oldAttrs[key] !== newAttrs[key]) {
      patches[key] = newAttrs[key]; // 新的属性值
    }
  }

  // 找出新增的属性
  for (let key in newAttrs) {
    if (!oldAttrs.hasOwnProperty(key)) {
      patches[key] = newAttrs[key];
    }
  }

  return patches;
}

function diffChildren(oldChildren, newChildren, index, patches, currentPatch) {
  oldChildren.forEach((child, i) => {
    walk(child, newChildren[i], ++index, patches);
  });

  // 如果新节点比旧节点多，处理新增的子节点
  if (newChildren.length > oldChildren.length) {
    for (let i = oldChildren.length; i < newChildren.length; i++) {
      currentPatch.push({ type: "ADD", newNode: newChildren[i] });
    }
  }
}
```

### **伪代码讲解**

1. **`diff` 函数**：这是主函数，接受两个虚拟 DOM 树（旧树和新树），并初始化一个 `patches` 对象来存储所有变化。

2. **`walk` 函数**：这是递归比较两个节点的函数。从根节点开始，递归遍历旧树和新树的每个节点，并生成补丁集：

   - 如果新节点不存在，说明旧节点需要被删除。
   - 如果两个节点都是文本节点，比较其内容是否相同，不同则更新文本。
   - 如果两个节点类型不同，生成替换操作。
   - 如果节点类型相同，递归处理其属性和子节点。

3. **`diffAttributes` 函数**：对比新旧节点的属性，生成属性变化的补丁。如果属性有变化或新增，记录这些变化。

4. **`diffChildren` 函数**：递归遍历子节点，处理新增、删除或修改的子节点。如果新节点列表比旧节点多，处理新增的子节点。

### **操作类型说明**

- **`REMOVE`**：旧节点被删除。
- **`TEXT`**：文本节点内容发生变化。
- **`REPLACE`**：新节点替换旧节点。
- **`ATTRS`**：节点的属性发生变化。
- **`ADD`**：新增节点。

### **伪代码应用场景**

1. **基本对比**：从根节点开始，递归遍历每个节点，对比新旧虚拟 DOM 树的不同。
2. **生成补丁**：每次发现节点类型、属性或内容不同，生成相应的补丁。
3. **最小化 DOM 操作**：通过最小化修改生成的补丁，React 可以减少对真实 DOM 的操作。

### **总结**

这段伪代码展示了 React Diff 算法的核心思路，主要通过同层级递归遍历、对比属性和子节点的方式高效地查找差异。这段算法简化了真实的 React Diff 机制，但已经能够处理大部分场景。
