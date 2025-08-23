# HTML 总结

HTML，即超文本标记语言，是构建网页和 Web 应用的标准标记语言。它通过标签来描述网页的结构和内容。一个基本的 HTML 文档包含文档声明、根元素`<html>`、头部`<head>`和主体`<body>`。头部用于包含元数据，比如标题和字符集设置，主体则包含实际显示的内容。

常用的 HTML 标签包括标题标签`<h1>`至`<h6>`、段落标签`<p>`、链接标签`<a>`、块级元素`<div>`和行内元素`<span>`等。此外，还有列表标签`<ul>`、`<ol>`和`<li>`，表格标签`<table>`、`<tr>`、`<td>`、`<th>`，以及表单标签`<form>`、`<input>`、`<label>`、`<button>`和`<select>`。

HTML5 引入了许多新特性，比如语义化标签（如`<header>`、`<footer>`、`<article>`、`<section>`）、多媒体标签（如`<audio>`、`<video>`）、图形和绘图标签（如`<canvas>`、`<svg>`），以及本地存储 API（`localStorage`和`sessionStorage`）。

在使用 HTML 时，应该遵循最佳实践，包括使用语义化标签来提高页面结构的清晰度和可访问性，保持代码风格的一致性，以及组织良好的代码结构以提高可维护性。

总的来说，HTML 是 Web 开发的基石，掌握它的基本结构和常用标签，以及新特性和最佳实践，对于创建高效、可维护的网页至关重要。

## 1.meta 元素都有什么

meta 元素是 HTML 中的一个重要标签，用于提供关于文档的元数据。以下是一些常见的 meta 元素：

1. `<meta charset="字符集">`：指定文档使用的字符集，通常是 UTF-8。
2. `<meta name="viewport" content="参数">`：用于控制页面在移动设备上的显示，如设置适口的宽度、缩放比例等。
3. `<meta name="keywords" content="关键词列表">`：指定页面的关键词，有助于搜索引擎优化（SEO）。
4. `<meta name="description" content="描述内容">`：指定页面的描述，同样有助于 SEO。
5. `<meta name="author" content="作者名">`：指定页面的作者。
6. `<meta http-equiv="X-UA-Compatible" content="IE=edge">`：告诉 IE 浏览器使用最新的渲染引擎来渲染页面。
7. `<meta http-equiv="refresh" content="秒数;URL=重定向地址">`：设置页面自动刷新或重定向到其他页面。
8. `<meta name="robots" content="robots">`：指定搜索引擎爬虫对页面的索引和抓取行为。

这些是常见的 meta 元素，它们用于提供文档的元数据信息，有助于浏览器正确解析和渲染页面，同时也有利于 SEO

## 2.script 的 async 跟 defer 的区别

`async` 和 `defer` 是用于控制 javascript 脚本加载和执行顺序的属性，它们的区别在于：

1. **async**:

   - 当浏览器遇到带有`async`属性的`<script>`标签时，它会立即开始下载脚本，但不会组织 HTML 解析。
   - 脚本下载完成后，会立即执行，不等待其他脚本或文档解析完成。
   - 执行时机是在文档加载过程中，可能在 DOMContentLoaded 事件触发之前或之后，取决于脚本加载和执行的速度。
   - 适用于不依赖其他脚本和文档内容的独立脚本

2. **defer**:

   - 当浏览器遇到带有`defer`属性的`<script>`标签时，它会立即开始下载脚本，但不会立即执行。
   - 脚本下载完成后，会等待 HTML 解析完成，然后按照顺序执行，但会在 DOMContentLoaded 事件之前执行。
   - 执行时机是在文档解析完成、DOMContentLoaded 事件触发之前。
   - 适用于需要等待文档解析完成后执行的脚本，可以确保脚本执行时可以访问到文档中的元素。

总的来说，`async` 和 `defer` 都是用于异步加载脚本，但它们的执行时机和行为有所不同。`async` 是立即下载并执行，不阻塞文档解析，而`defer`是立即下载但延迟执行，等待文档解析完成后按照顺序执行。

## 3.html 标签 b 和 strong 的区别

`<b>` 和 `<strong>` 标签都用于对文本进行加粗显示，但它们在语义上有所不同：

1. `<b>` 标签是用来表示文本的样式加粗，没有特定的语义含义，仅仅是为了使文本显示为粗体。因此，搜索引擎通常不会将 `<b>` 标签内的文本视为重要内容，也不会为其增加额外的权重。

2. `<strong>` 标签除了使文本加粗外，还具有强调的语义含义，表示文本的重要性或紧急程度。搜索引擎会将 `<strong>` 标签内的文本视为更为重要的内容，可能会为其增加一定的权重，从而提升页面在搜索结果中的排名。

因此，应根据文本的语义含义来选择使用 `<b>` 还是 `<strong>` 标签。如果文本仅仅需要加粗显示而没有强调的语义含义，可以使用 `<b>` 标签；如果文本需要强调重要性或紧急程度，应使用 `<strong>` 标签。

## 4.a 标签默认事件禁掉之后做了什么才实现了跳转

禁用 `<a>` 标签的默认事件后，可以通过 JavaScript 来手动实现跳转。通常可以通过以下几种方式实现：

1. **使用 `window.location.href` 属性**：将页面的 `location.href` 属性设置为目标 URL，实现页面的跳转。

   ```javascript
   document.querySelector("a").addEventListener("click", function (event) {
     event.preventDefault(); // 阻止默认事件
     window.location.href = this.href; // 设置页面的 URL 为目标 URL
   });
   ```

2. **使用 `window.location.replace()` 方法**：将页面的 URL 替换为目标 URL，实现页面的跳转。

   ```javascript
   document.querySelector("a").addEventListener("click", function (event) {
     event.preventDefault(); // 阻止默认事件
     window.location.replace(this.href); // 替换当前页面的 URL 为目标 URL
   });
   ```

3. **使用 `window.open()` 方法**：在新窗口中打开目标 URL，实现页面的跳转。

   ```javascript
   document.querySelector("a").addEventListener("click", function (event) {
     event.preventDefault(); // 阻止默认事件
     window.open(this.href, "_self"); // 在当前窗口打开目标 URL
   });
   ```

以上方法都是通过 JavaScript 来手动处理页面跳转，可以根据具体需求选择合适的方式来实现。

## 5.请说明 Html 布局元素的分类有哪些？并描述每种布局元素的应用场景

HTML 布局元素可以根据其作用和用途进行分类，常见的分类包括：

1. **块级元素（Block-level Elements）：**

   - 这些元素在页面上以块的形式显示，即它们会占据一整行的宽度，并且在上下文中始终换行。
   - 常见的块级元素包括 `<div>、<p>、<h1> - <h6>、<header>、<footer>、<section>、<nav>、<article>` 等。
   - 应用场景：用于构建页面的主要结构，如页面的头部、底部、侧边栏、内容区域等。

2. **行内元素（Inline Elements）：**

   - 这些元素在页面上以行内的形式显示，即它们不会强制换行，而是在同一行内按照文本的排列顺序显示。
   - 常见的行内元素包括 `<span>、<a>、<strong>、<em>、<img>、<input>、<button>、<label>` 等。
   - 应用场景：用于包裹文本、内联元素的装饰、按钮等小的交互元素。

3. **行内块级元素（Inline-block Elements）：**

   - 这些元素在页面上以行内的形式显示，但是它们的内容表现为块级元素，即它们会占据一定的宽度和高度，并且可以在同一行内显示多个元素。
   - 常见的行内块级元素包括 `<div style="display: inline-block">、<img style="display: inline-block">、<span style="display: inline-block">` 等。
   - 应用场景：用于实现水平排列的元素，如导航菜单、图片列表等。

4. **隐藏元素（Hidden Elements）：**
   - 这些元素在页面上不会显示，但是它们仍然存在于 DOM 结构中，并且可以通过 CSS 或 JavaScript 控制显示和隐藏。
   - 常见的隐藏元素包括 `<input type="hidden">、<meta name="viewport" content="width=device-width, initial-scale=1.0">` 等。
   - 应用场景：用于存储或传递数据，或者控制页面布局和行为。

这些布局元素的选择和应用取决于页面的设计和需求，合适的布局元素可以帮助构建清晰、结构化和易于维护的页面布局。

## 6.单页面应用（SPA）

### 6.1 定义

单页面应用是一种 Web 应用程序，用户与之交互时，不需要重新加载整个页面。相反，所有的页面内容都被动态加载，通过 JavaScript 操作 DOM 来更新页面。

### 6.2 特点

1. **用户体验好**：由于不需要每次都重新加载页面，用户体验更加流畅，感觉更像是桌面应用。
2. **快速响应**：通过局部更新，减少了页面刷新和重绘的时间，响应速度快。
3. **前端路由**：使用 JavaScript 库（如 React Router，Vue Router）进行路由管理，实现页面间的导航和状态管理。
4. **复杂性增加**：由于需要在前端处理更多的逻辑，开发和维护的复杂性增加。
5. **SEO 挑战**：传统的 SPA 对 SEO 不友好，因为搜索引擎爬虫难以抓取动态生成的内容。不过，可以使用服务器端渲染（SSR）或静态站点生成（SSG）技术来改善这一问题。

### 6.3 技术栈

- 框架/库：React、Vue.js、Angular
- 路由管理：React Router、Vue Router、Angular Router
- 状态管理：Redux、Vuex、MobX

### 6.4 适用场景

- 需要丰富交互和动态内容的应用，如社交媒体平台、在线编辑器、管理后台等。

## 7.多页面应用（MPA）

### 7.1 定义

多页面应用是传统的 Web 应用，每次用户请求一个新页面时，服务器会返回一个完整的 HTML 页面，整个页面刷新。

### 7.2 特点

1. **传统开发模式**：每个页面都是独立的 HTML 文件，用户请求时服务器返回整个页面。
2. **SEO 友好**：由于每个页面都是一个独立的 HTML 文件，搜索引擎可以轻松抓取和索引。
3. **开发简单**：页面逻辑较为简单，每个页面的状态和数据管理较为独立。
4. **加载速度慢**：每次请求新页面时，都需要重新加载整个页面，可能导致用户体验不如 SPA 流畅。
5. **服务器压力大**：每次页面请求都会给服务器带来压力，需要处理更多的请求。

### 7.3 技术栈

- 后端框架：Django、Ruby on Rails、ASP.NET、Express.js
- 前端：传统的 HTML、CSS、JavaScript

### 7.4 适用场景

- 内容驱动的网站，如博客、企业官网、新闻网站等，需要良好的 SEO 支持和相对简单的交互。

## 8.SPA 和 MPA 的比较

1. **用户体验**：

   - SPA：页面切换快速，用户体验好。
   - MPA：页面切换需要重新加载，用户体验稍逊。

2. **开发复杂度**：

   - SPA：前端逻辑复杂，需要处理路由、状态管理等。
   - MPA：开发简单，每个页面独立，逻辑较为清晰。

3. **SEO**：

   - SPA：需要额外处理 SEO 问题，如服务器端渲染（SSR）。
   - MPA：天然支持 SEO，每个页面都是独立的 HTML 文件。

4. **性能**：
   - SPA：初次加载可能较慢，但之后交互迅速。
   - MPA：每次页面请求都需要完整加载，可能会影响性能。

### 结论

单页面应用和多页面应用各有优缺点，选择哪种架构模式应根据具体的项目需求和场景来决定。对于需要高度互动和动态内容的应用，SPA 可能是更好的选择。而对于内容驱动、需要良好 SEO 支持的网站，MPA 则更为适合。

## 9.SPA 和 MPA 的实现原理

### 9.1 单页面应用（SPA）的实现原理

#### 9.1.1 核心思想

单页面应用的核心思想是在首次加载时获取所有必要的资源（HTML、CSS、JavaScript），之后通过 JavaScript 来动态更新页面内容，而无需重新加载整个页面。

#### 9.1.2 实现步骤

1. **初始加载**：

   - 客户端请求服务器，服务器返回包含基础 HTML 结构、CSS 样式和 JavaScript 脚本的页面。
   - 加载页面后，JavaScript 框架初始化，并通过 AJAX 请求获取必要的数据。

2. **前端路由**：

   - 前端路由管理器（如 React Router、Vue Router）拦截 URL 变化，控制页面组件的切换和渲染。
   - 路由变化时，前端路由管理器根据当前路径选择相应的组件进行渲染，更新页面内容。

3. **动态数据加载**：

   - 使用 AJAX（如 fetch API、Axios）向服务器请求数据，根据用户操作或路由变化加载新数据。
   - 服务器返回数据，JavaScript 根据数据更新 DOM，动态渲染新内容。

4. **状态管理**：
   - 使用状态管理库（如 Redux、Vuex）集中管理应用状态，确保不同组件之间的状态同步。
   - 组件可以从状态管理库获取数据，并订阅状态变化，当状态变化时重新渲染组件。

#### 9.1.3 优化技术

- **懒加载**：按需加载组件或模块，减少初始加载时间。
- **代码拆分**：使用 Webpack 等工具将代码分成多个小包，按需加载。
- **服务端渲染（SSR）**：在服务器端预渲染页面，提高首屏加载速度，并改善 SEO。

#### 9.1.4 简单实现示例

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>SPA Example</title>
    <script defer src="app.js"></script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

```javascript
// app.js
const routes = {
  "/": "Home Page",
  "/about": "About Page",
  "/contact": "Contact Page",
};

function renderRoute() {
  const path = window.location.pathname;
  const appDiv = document.getElementById("app");
  appDiv.textContent = routes[path] || "404 Not Found";
}

window.addEventListener("popstate", renderRoute);

document.addEventListener("click", (event) => {
  if (event.target.tagName === "A") {
    event.preventDefault();
    const path = event.target.getAttribute("href");
    window.history.pushState({}, "", path);
    renderRoute();
  }
});

renderRoute();
```

### 9.2 多页面应用（MPA）的实现原理

#### 9.2.1 核心思想

多页面应用的核心思想是每个页面都是一个独立的 HTML 文件，用户每次请求新页面时，服务器返回一个完整的 HTML 页面。

#### 9.2.2 实现步骤

1. **初始加载**：

   - 用户请求服务器上的某个页面，服务器返回对应的 HTML 文件，包括 CSS 和 JavaScript。
   - 浏览器加载并渲染 HTML 文件，执行 JavaScript。

2. **页面跳转**：

   - 用户点击链接，浏览器发送 HTTP 请求到服务器，服务器返回新的 HTML 页面。
   - 浏览器卸载当前页面，加载并渲染新页面。

3. **服务器端渲染**：

   - 每个页面请求都是独立的，服务器根据 URL 路径生成相应的 HTML 页面并返回给客户端。
   - 服务器可能使用模板引擎（如 EJS、Pug）动态生成 HTML 页面。

4. **数据处理**：
   - 服务器处理业务逻辑和数据请求，将数据嵌入生成的 HTML 页面中。
   - 前端 JavaScript 处理页面上的动态交互（如表单验证、AJAX 请求），但每个页面的 JavaScript 通常是独立的。

#### 9.2.3 优化技术

- **页面缓存**：使用浏览器缓存减少服务器请求，提高加载速度。
- **CDN**：将静态资源（如 CSS、JavaScript、图像）放在内容分发网络上，提高资源加载速度。
- **服务器端渲染优化**：通过优化模板引擎和数据库查询，提高服务器生成页面的效率。

#### 9.2.4 简单实现示例

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Home Page</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Home Page</h1>
    <nav>
      <a href="/about.html">About</a>
      <a href="/contact.html">Contact</a>
    </nav>
  </body>
</html>
```

```html
<!-- about.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>About Page</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>About Page</h1>
    <nav>
      <a href="/index.html">Home</a>
      <a href="/contact.html">Contact</a>
    </nav>
  </body>
</html>
```

### 总结

SPA 和 MPA 的实现原理各有不同，SPA 依赖于 JavaScript 在客户端进行页面的动态更新和路由管理，提供流畅的用户体验；MPA 则依赖于服务器端的独立页面生成和返回，简单而有效，但每次页面跳转需要重新加载整个页面。选择哪种架构模式应根据具体的项目需求和应用场景来决定。
