# webpack

## 1.你对 webpack 的理解，解决了什么问题？

### 1.1 背景

Webpack 最初的目标是实现前端项目的模块化，旨在更高效地管理和维护项目中的每一个资源。

#### 模块化

最早的时候，我们会通过文件划分的形式实现模块化，也就是将每个功能及其相关状态数据各自单独放到不同的 JS 文件中。

约定每个文件是一个独立的模块，然后再将这些 js 文件引入到页面，一个 script 标签对应一个模块，然后调用模块化的成员。

```javascript
<script src="module-a.js"></script>
<script src="module-b.js"></script>
```

但这种模块弊端十分明显，模块都是在全局中工作，大量模块成员污染了环境，模块与模块之间并没有依赖关系、维护困难、没有私有空间等问题。

项目一旦变大，上述问题会尤其明显。

随后，就出现了命名空间方式，规定每个模块只暴露一个全局对象，然后模块的内容都挂载到这个对象中

```javascript
// module-a.js
(function ($) {
  var name = "module-a";

  function method1() {
    console.log(name + "#method1");
    $("body").animate({ margin: "200px" });
  }

  window.moduleA = {
    method1: method1,
  };
})(jQuery);
```

上述的方式都是早期解决模块的方式，但是仍然存在一些没有解决的问题。例如，我们是用过 script 标签在页面引入这些模块的，这些模块的加载并不受代码的控制，时间一久维护起来也十分的麻烦

理想的解决方式是，在页面中引入一个 JS 入口文件，其余用到的模块可以通过代码控制，按需加载进来

除了模块加载的问题以外，还需要规定模块化的规范，如今流行的则是 CommonJS、ES Modules

### 1.2 问题

从后端渲染的 JSP、PHP，到前端原生 JavaScript，再到 jQuery 开发，再到目前的三大框架 Vue、React、Angular

开发方式，也从 javascript 到后面的 es5、es6、7、8、9、10，再到 typescript，包括编写 CSS 的预处理器 less、scss 等

现代前端开发已经变得十分的复杂，所以我们开发过程中会遇到如下的问题：

- 需要通过模块化的方式来开发
- 使用一些高级的特性来加快我们的开发效率或者安全性，比如通过 ES6+、TypeScript 开发脚本逻辑，通过 sass、less 等方式来编写 css 样式代码
- 监听文件的变化来并且反映到浏览器上，提高开发的效率
- JavaScript 代码需要模块化，HTML 和 CSS 这些资源文件也会面临需要被模块化的问题
- 开发完成后我们还需要将代码进行压缩、合并以及其他相关的优化

而 webpack 恰巧可以解决以上问题

### 1.3 是什么

webpack 是一个用于现代 JavaScript 应用程序的静态模块打包工具

> 静态模块:这里的静态模块指的是开发阶段，可以被 webpack 直接引用的资源（可以直接被获取打包进 bundle.js 的资源）

当 webpack 处理应用程序时，它会在内部构建一个依赖图，此依赖图对应映射到项目所需的每个模块（不再局限 js 文件），并生成一个或多个 bundles

webpack 的能力：

- **编译代码能力**，提高效率，解决浏览器兼容问题
- **模块整合能力**，提高性能，可维护性，解决浏览器频繁请求文件的问题
- **万物皆可模块能力**，项目维护性增强，支持不同种类的前端模块类型，统一的模块化方案，所有资源文件的加载都可以通过代码控制

## 2.webpack 的构建流程

通过分析项目的资源依赖关系，将各种资源，如 JavaScript、CSS、图片等，打包成静态资源文件，以便在浏览器中使用。

- 初始化参数：Webpack 会从配置文件和 Shell 语句中读取与合并参数，得到最终的参数配置。
- 初始化 Compiler 对象：根据上一步得到的参数，初始化一个 Compiler 对象，该对象包含了 Webpack 环境的所有配置信息，包括 options、loaders、plugins 等。
- 加载插件：Webpack 根据配置文件中的 plugins 配置，加载所有的插件，以便后续使用。
- 执行编译：调用 Compiler 对象的 run 方法开始执行编译过程。
- 解析入口文件：Webpack 根据 entry 配置找到入口文件，从入口文件开始递归解析项目依赖的所有模块。
- 调用 Loader：Webpack 通过配置的 Loader 对模块进行转换，将各种类型的文件转换为 Webpack 能够处理的模块。
- 递归依赖：Webpack 递归解析项目依赖的所有模块，构建依赖关系图。
- 构建 Chunk：根据入口文件和依赖关系图，将模块组合成 Chunk（代码块），每个 Chunk 包含多个模块。
- 输出文件：将 Chunk 输出到指定的目录中，生成最终的静态资源文件。
- 完成编译：编译过程完成，Webpack 返回编译结果或触发相应的事件。

## 3.webpack 中常见的 Loader？解决了什么问题？

### 3.1 是什么

loader 用于对模块的"源代码"进行转换，在 import 或"加载"模块时预处理文件

webpack 做的事情，仅仅是分析出各种模块的依赖关系，然后形成资源列表，最终打包生成到指定的文件中。

在 webpack 内部中，任何文件都是模块，不仅仅只是 js 文件

默认情况下，在遇到 import 或者 require 加载模块的时候，**webpack 只支持对 js 和 json 文件打包**

像 css、sass、png 等这些类型的文件的时候，webpack 则无能为力，这时候就需要配置对应的 loader 进行文件内容的解析

所以**当 webpack 碰到不识别的模块的时候，webpack 会在配置的中查找该文件解析规则**

### 3.2 配置方式

关于配置 loader 的方式有三种：

- 配置方式（推荐）：在 webpack.config.js 文件中指定 loader
- 内联方式：在每个 import 语句中显式指定 loader
- CLI 方式：在 shell 命令中指定它们

好的，下面是三种方式的示例：

1. **配置方式**（推荐）：在 webpack.config.js 文件中指定 loader

   ```javascript
   // webpack.config.js

   module.exports = {
     module: {
       rules: [
         {
           test: /\.css$/,
           use: ["style-loader", "css-loader"],
         },
       ],
     },
   };
   ```

2. **内联方式**：在每个 import 语句中显式指定 loader

   ```javascript
   import Styles from "style-loader!css-loader!./styles.css";
   ```

3. **CLI 方式**：在 shell 命令中指定它们

   ```bash
   webpack --module-bind 'css=style-loader!css-loader'
   ```

这些示例中都是针对处理 CSS 文件的 loader，你可以根据需要替换成其他类型的 loader。

### 3.3 常见的 loader

在页面开发过程中，我们经常性加载除了 js 文件以外的内容，这时候我们就需要配置响应的 loader 进行加载

常见的 loader 如下：

- style-loader:将 css 添加到 DOM 的内联样式标签 style 里
- css-loader：允许将 css 文件通过 require 的方式引入，并返回 css 代码
- less-loader：处理 less
- sass-loader：处理 sass
- postcss-loader：用 postcss 来处理 CSS
- autoprefix-loader：处理 CSS3 属性前缀，已被弃用，建议直接使用 postcss
- file-loader：分发文件到 output 目录并返回相对路径
- url-loader：和 file-loader 类似，但是当文件小于设定的 limit 时可以返回一个 Data Url
- html-minify-loader：压缩 HTML
- babel-loader：用 babel 来转换 ES6 文件到 ES

下面给出一些常见的 loader 的使用：

#### css-loader

分析 css 模块之间的关系，并合成⼀个 css

```sh
npm install --save-dev css-loader
```

```javascript
rules: [
  ...,
 {
  test: /\.css$/,
    use: {
      loader: "css-loader",
      options: {
     // 启用/禁用 url() 处理
     url: true,
     // 启用/禁用 @import 处理
     import: true,
        // 启用/禁用 Sourcemap
        sourceMap: false
      }
    }
 }
]
```

如果只通过 css-loader 加载文件，这时候页面代码设置的样式并没有生效

原因在于，css-loader 只是负责将.css 文件进行一个解析，而并不会将解析后的 css 插入到页面中

如果我们希望再完成插入 style 的操作，那么我们还需要另外一个 loader，就是 style-loader

#### style-loader

把 css-loader 生成的内容，用 style 标签挂载到页面的 head 中

```sh
npm install --save-dev style-loader
```

```js
rules: [
  ...,
 {
  test: /\.css$/,
    use: ["style-loader", "css-loader"]
 }
]
```

同一个任务的 loader 可以同时挂载多个，处理顺序为：从右到左，从下往上

#### less-loader

开发中，我们也常常会使用 less、sass、stylus 预处理器编写 css 样式，使开发效率提高，这里需要使用 less-loader

```sh
npm install less-loader -D
```

```js
rules: [
  ...,
 {
  test: /\.css$/,
    use: ["style-loader", "css-loader","less-loader"]
 }
]
```

#### raw-loader

在 webpack 中通过 import 方式导入文件内容，该 loader 并不是内置的，所以首先要安装

```sh
npm install --save-dev raw-loader
```

然后在 webpack.config.js 中进行配置

```js
module.exports = {
  ...,
  module: {
      rules: [
      {
        test: /\.(txt|md)$/,
        use: 'raw-loader'
     }
    ]
 }
}
```

#### file-loader

把识别出的资源模块，移动到指定的输出⽬目录，并且返回这个资源在输出目录的地址(字符串)

```sh
npm install --save-dev file-loader
```

```js
rules: [
  ...,
 {
  test: /\.(png|jpe?g|gif)$/,
    use: {
      loader: "file-loader",
      options: {
        // placeholder 占位符 [name] 源资源模块的名称
        // [ext] 源资源模块的后缀
        name: "[name]_[hash].[ext]",
        //打包后的存放位置
        outputPath: "./images",
        // 打包后文件的 url
        publicPath: './images',
      }
    }
 }
]
```

#### url-loader

可以处理理 file-loader 所有的事情，但是遇到图片格式的模块，可以选择性的把图片转成 base64 格式的字符串，并打包到 js 中，对小体积的图片比较合适，大图片不合适。

```sh
npm install --save-dev url-loader
```

```js
rules: [
  ...,
 {
  test: /\.(png|jpe?g|gif)$/,
    use: {
      loader: "url-loader",
      options: {
        // placeholder 占位符 [name] 源资源模块的名称
        // [ext] 源资源模块的后缀
        name: "[name]_[hash].[ext]",
        //打包后的存放位置
        outputPath: "./images"
        // 打包后文件的 url
        publicPath: './images',
        // 小于 100 字节转成 base64 格式
        limit: 100
      }
    }
 }
]
```

## 4.常见的 plugin？解决了什么问题？

### 4.1 是什么

Plugin（Plug-in）是一种计算机应用程序，它和主应用程序互相交互，以提供特定的功能

是一种遵循一定规范的应用程序接口编写出来的程序，只能运行在程序规定的系统下，因为其需要调用原纯净系统提供的函数库或者数据

webpack 中的 plugin 也是如此，plugin 赋予其各种灵活的功能，例如打包优化、资源管理、环境变量注入等，它们会运行在 webpack 的不同阶段（钩子 / 生命周期），贯穿了 webpack 整个编译周期

目的在于解决 loader 无法实现的其他事

**配置方式**：

这里讲述文件的配置方式，一般情况，通过配置文件导出对象中 plugins 属性传入 new 实例对象。如下所示：

```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 访问内置的插件
module.exports = {
  ...
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({ template: './src/index.html' }),
  ],
};
```

### 4.2 特性

其本质是一个具有 apply 方法 javascript 对象

apply 方法会被 webpack compiler 调用，并且在整个编译生命周期都可以访问 compiler 对象

```js
const pluginName = "ConsoleLogOnBuildWebpackPlugin";

class ConsoleLogOnBuildWebpackPlugin {
  apply(compiler) {
    compiler.hooks.run.tap(pluginName, (compilation) => {
      console.log("webpack 构建过程开始！");
    });
  }
}

module.exports = ConsoleLogOnBuildWebpackPlugin;
```

compiler hook 的 tap 方法的第一个参数，应是驼峰式命名的插件名称

关于整个编译生命周期钩子，有如下：

- entry-option ：初始化 option
- run
- compile： 真正开始的编译，在创建 compilation 对象之前
- compilation ：生成好了 compilation 对象
- make 从 entry 开始递归分析依赖，准备对每个模块进行 build
- after-compile： 编译 build 过程结束
- emit ：在将内存中 assets 内容写到磁盘文件夹之前
- after-emit ：在将内存中 assets 内容写到磁盘文件夹之后
- done： 完成所有的编译过程
- failed： 编译失败的时候

### 4.3 常见的 Plugin

常见的 Plugin：

|                           |     |
| :-----------------------: | :-: |
| AggressiveSplittingPlugin |     |
| BabelMinifyWebpackPlugin  |     |
|                           |     |
|                           |     |
|                           |     |
|                           |     |
|                           |     |
|                           |     |
|                           |     |

#### HtmlWebpackPlugin

在打包结束后，⾃动生成⼀个 html ⽂文件，并把打包生成的 js 模块引⼊到该 html 中

```sh
npm install --save-dev html-webpack-plugin
```

```js
// webpack.config.js
const HtmlWebpackPlugin = require("html-webpack-plugin");
module.exports = {
 ...
  plugins: [
     new HtmlWebpackPlugin({
       title: "My App",
       filename: "app.html",
       template: "./src/html/index.html"
     })
  ]
};
```

```html
<!--./src/html/index.html-->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title><%=htmlWebpackPlugin.options.title%></title>
  </head>
  <body>
    <h1>html-webpack-plugin</h1>
  </body>
</html>
```

在 html 模板中，可以通过 <%=htmlWebpackPlugin.options.XXX%> 的方式获取配置的值

#### clean-webpack-plugin

删除（清理）构建目录

```sh
npm install --save-dev clean-webpack-plugin
```

```js
const {CleanWebpackPlugin} = require('clean-webpack-plugin');
module.exports = {
 ...
  plugins: [
    ...,
    new CleanWebpackPlugin(),
    ...
  ]
}
```

#### mini-css-extract-plugin

提取 CSS 到一个单独的文件中

```sh
npm install --save-dev mini-css-extract-plugin
```

```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
module.exports = {
 ...,
  module: {
   rules: [
    {
     test: /\.s[ac]ss$/,
     use: [
      {
       loader: MiniCssExtractPlugin.loader
     },
          'css-loader',
          'sass-loader'
        ]
   }
   ]
 },
  plugins: [
    ...,
    new MiniCssExtractPlugin({
     filename: '[name].css'
    }),
    ...
  ]
}
```

#### DefinePlugin

允许在编译时创建配置的全局对象，是一个 webpack 内置的插件，不需要安装

```js
const { DefinePlugun } = require('webpack')

module.exports = {
 ...
    plugins:[
        new DefinePlugin({
            BASE_URL:'"./"'
        })
    ]
}
```

这时候编译 template 模块的时候，就能通过下述形式获取全局对象

```html
<link rel="icon" href="<%= BASE_URL%>favicon.ico>"
```

#### copy-webpack-plugin

复制文件或目录到执行区域，如 vue 的打包过程中，如果我们将一些文件放到 public 的目录下，那么这个目录会被复制到 dist 文件夹中

```sh
npm install copy-webpack-plugin -D
```

```js
new CopyWebpackPlugin({
  parrerns: [
    {
      from: "public",
      globOptions: {
        ignore: ["**/index.html"],
      },
    },
  ],
});
```

复制的规则在 patterns 属性中设置：

- from：设置从哪一个源中开始复制
- to：复制到的位置，可以省略，会默认复制到打包的目录下
- globOptions：设置一些额外的选项，其中可以编写需要忽略的文件

## 5.plugin 和 loader 的区别

### 5.1 区别

前面两节我们有提到 Loader 与 Plugin 对应的概念，先来回顾下

- loader 是文件加载器，能够加载资源文件，并对这些文件进行一些处理，诸如编译、压缩等，最终一起打包到指定的文件中
- plugin 赋予了 webpack 各种灵活的功能，例如打包优化、资源管理、环境变量注入等，目的是解决 loader 无法实现的其他事

两者在运行时机上的区别：

- loader 运行在打包文件之前
- plugins 在整个编译周期都起作用

在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果

对于 loader，实质是一个转换器，将 A 文件进行编译形成 B 文件，操作的是文件，比如将 A.scss 或 A.less 转变为 B.css，单纯的文件转换过程

### 5.2 编写 loader

在编写 loader 前，我们首先需要了解 loader 的本质

其本质为函数，函数中的 this 作为上下文会被 webpack 填充，因此我们不能将 loader 设为一个箭头函数

函数接受一个参数，为 webpack 传递给 loader 的文件源内容

函数中 this 是由 webpack 提供的对象，能够获取当前 loader 所需要的各种信息

函数中有异步操作或同步操作，异步操作通过 this.callback 返回，返回值要求为 string 或者 Buffer

代码如下所示：

```js
// 导出一个函数，source为webpack传递给loader的文件源内容
module.exports = function (source) {
  const content = doSomeThing2JsString(source);

  // 如果 loader 配置了 options 对象，那么this.query将指向 options
  const options = this.query;

  // 可以用作解析其他模块路径的上下文
  console.log("this.context");

  /*
   * this.callback 参数：
   * error：Error | null，当 loader 出错时向外抛出一个 error
   * content：String | Buffer，经过 loader 编译后需要导出的内容
   * sourceMap：为方便调试生成的编译后内容的 source map
   * ast：本次编译生成的 AST 静态语法树，之后执行的 loader 可以直接使用这个 AST，进而省去重复生成 AST 的过程
   */
  this.callback(null, content); // 异步
  return content; // 同步
};
```

一般在编写 loader 的过程中，保持功能单一，避免做多种功能

如 less 文件转换成 css 文件也不是一步到位，而是 less-loader、css-loader、style-loader 几个 loader 的链式调用才能完成转换

### 5.3 编写 plugin

由于 webpack 基于发布订阅模式，在运行的生命周期中会广播出许多事件，插件通过监听这些事件，就可以在特定的阶段执行自己的插件任务

在之前也了解过，webpack 编译会创建两个核心对象：

- compiler：包含了 webpack 环境的所有的配置信息，包括 options，loader 和 plugin，和 webpack 整个生命周期相关的钩子
- compilation：作为 plugin 内置事件回调函数的参数，包含了当前的模块资源、编译生成资源、变化的文件以及被跟踪依赖的状态信息。当检测到一个文件变化，一次新的 Compilation 将被创建

如果自己要实现 plugin，也需要遵循一定的规范：

- 插件必须是一个函数或者是一个包含 apply 方法的对象，这样才能访问 compiler 实例
- 传给每个插件的 compiler 和 compilation 对象都是同一个引用，因此不建议修改
- 异步的事件需要在插件处理完任务时调用回调函数通知 Webpack 进入下一个流程，不然会卡住

实现 plugin 的模板如下：

```js
class MyPlugin {
  // Webpack 会调用 MyPlugin 实例的 apply 方法给插件实例传入 compiler 对象
  apply(compiler) {
    // 找到合适的事件钩子，实现自己的插件功能
    compiler.hooks.emit.tap("MyPlugin", (compilation) => {
      // compilation: 当前打包构建流程的上下文
      console.log(compilation);

      // do something...
    });
  }
}
```

在 emit 事件发生时，代表源文件的转换和组装已经完成，可以读取到最终将输出的资源、代码块、模块及其依赖，并且可以修改输出资源的内容

## 6.webpack 的热更新是如何做到的

### 6.1 是什么

HMR 全称 Hot Module Replacement，可以理解为模块热替换，指在应用程序运行过程中，替换、添加、删除模块，而无需重新刷新整个应用

例如，我们在应用运行过程中修改了某个模块，通过自动刷新会导致整个应用的整体刷新，那页面中的状态信息都会丢失

如果使用的是 HMR，就可以实现只将修改的模块实时替换至应用中，不必完全刷新整个应用

在 webpack 中配置开启热模块也非常的简单，如下代码：

```js
const webpack = require("webpack");
module.exports = {
  // ...
  devServer: {
    // 开启 HMR 特性
    hot: true,
    // hotOnly: true
  },
};
```

通过上述这种配置，如果我们修改并保存 css 文件，确实能够以不刷新的形式更新到页面中

但是，当我们修改并保存 js 文件之后，页面依旧自动刷新了，这里并没有触发热模块

所以，HMR 并不像 Webpack 的其他特性一样可以开箱即用，需要有一些额外的操作

我们需要去指定哪些模块发生更新时进行 HRM，如下代码：

```js
if (module.hot) {
  module.hot.accept("./util.js", () => {
    console.log("util.js更新了");
  });
}
```

### 6.2 原理

- webpack complie : 将 JS 源代码编译成 bundle.js
- HMR Server : 用来将 热更新的文件输出给 HMR Runtime

## 7.webpack 如何优化前端性能

Webpack 是一个强大的前端打包工具，通过其丰富的插件和配置选项，可以有效地优化前端项目的性能。下面是一些常见的优化手段和对应的 Webpack 配置。

### 7.1 JS 代码压缩

使用 TerserPlugin 来压缩 JavaScript 代码，减小文件体积。

```javascript
const TerserPlugin = require("terser-webpack-plugin");

module.exports = {
  // ...其它配置
  optimization: {
    minimize: true,
    minimizer: [
      new TerserPlugin({
        parallel: true, // 多线程压缩
        terserOptions: {
          compress: {},
          mangle: true,
        },
      }),
    ],
  },
};
```

### 7.2 CSS 代码压缩

使用 css-minimizer-webpack-plugin 来压缩 CSS 代码。

```javascript
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");

module.exports = {
  // ...其它配置
  optimization: {
    minimize: true,
    minimizer: [
      new CssMinimizerPlugin({
        parallel: true, // 多线程压缩
      }),
    ],
  },
};
```

### 7.3 HTML 文件代码压缩

使用 HtmlWebpackPlugin 来生成 HTML 文件时进行压缩。

```javascript
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  // ...其它配置
  plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html",
      minify: {
        collapseWhitespace: true, // 折叠空白
        removeComments: true, // 移除注释
        minifyCSS: true, // 压缩内联css
      },
    }),
  ],
};
```

### 7.4 文件大小压缩

使用 CompressionWebpackPlugin 来对文件进行 Gzip 压缩。

```javascript
const CompressionPlugin = require("compression-webpack-plugin");

module.exports = {
  // ...其它配置
  plugins: [
    new CompressionPlugin({
      test: /\.(js|css)$/, // 哪些文件需要压缩
      threshold: 10240, // 文件大小大于这个值时会被压缩，单位是 bytes
      minRatio: 0.8, // 只有压缩率比这个值小的资源才会被处理
    }),
  ],
};
```

### 7.5 图片压缩

使用 image-webpack-loader 对图片进行压缩。

```javascript
module.exports = {
  // ...其它配置
  module: {
    rules: [
      {
        test: /\.(png|jpe?g|gif|webp)$/i,
        use: [
          {
            loader: "file-loader",
            options: {
              outputPath: "images/",
            },
          },
          {
            loader: "image-webpack-loader",
            options: {
              mozjpeg: {
                progressive: true,
                quality: 65,
              },
              optipng: {
                enabled: false,
              },
              pngquant: {
                quality: [0.65, 0.9],
                speed: 4,
              },
              gifsicle: {
                interlaced: false,
              },
              webp: {
                quality: 75,
              },
            },
          },
        ],
      },
    ],
  },
};
```

### 7.6 Tree Shaking

使用 Webpack 自带的配置来移除项目中未使用的代码。

```javascript
module.exports = {
  // ...其它配置
  optimization: {
    usedExports: true, // 开启 Tree Shaking
  },
};
```

### 7.7 代码分离

通过配置 splitChunksPlugin 实现代码分割，优化加载性能。

```javascript
module.exports = {
  // ...其它配置
  optimization: {
    splitChunks: {
      chunks: "all",
    },
  },
};
```

### 7.8 内联 chunk

使用 InlineChunkHtmlPlugin 将 runtime 等 chunk 内联到 HTML 文件中，减少 HTTP 请求次数。

```javascript
const HtmlWebpackPlugin = require("html-webpack-plugin");
const InlineChunkHtmlPlugin = require("react-dev-utils/InlineChunkHtmlPlugin");

module.exports = {
  // ...其它配置
  plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html",
    }),
    new InlineChunkHtmlPlugin(HtmlWebpackPlugin, [/runtime.+\.js/]),
  ],
};
```

### 7.9 总结

通过上述优化手段，可以显著提升前端项目的性能，包括减小文件体积、减少 HTTP 请求、优化加载速度等。Webpack 提供了丰富的插件和配置选项，可以根据具体的项目需求来选择合适的优化策略，以达到最佳的性能提升效果。
