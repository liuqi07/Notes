## webpack笔记

### 什么是webpack？

现今的很多网页其实可以看做是功能丰富的应用，它们拥有着复杂的JavaScript代码和一大堆依赖包。为了简化开发的复杂度，前端社区涌现出了很多好的实践方法


- **模块化**，让我们可以把复杂的程序细小化为小的文件；
- 类似于TypeScript这种在JavaScript基础上拓展的开发语言：使我们能够实现目前版本的JavaScript不能直接使用的特性，并且之后还能能装换为JavaScript文件使浏览器可以识别；
- Scss,Less等css预处理器
- ...

## 开始使用webpack

### **安装**
1. `npm install -g webpack` 全局安装
2. `npm install webpack --save-dev` 安装到你的项目
3. `npm init` 项目初始化，可以自动生成package.json
4. `npm install --save-dev webpack`


```
module.exports = {
  entry:  __dirname + "/app/main.js",//已多次提及的唯一入口文件
  output: {
    path: __dirname + "/public",//打包后的文件存放的地方
    filename: "bundle.js"//打包后输出文件的文件名
  }
}
```

### package.json
```
{
  "name": "webpack-sample-project",
  "version": "1.0.0",
  "description": "Sample webpack project",
  "scripts": {
    "start": "webpack" //配置的地方就是这里，相当于把npm的start命令指向webpack命令
  },
  "author": "zhang",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^1.12.9"
  }
}
```

---
### 处理多个文件

只需要通过修改 entry 对象就可以指定任意数量所期望的 entry 或 output 点。

1. ##### 多个文件，打包在一起
```
const webpack = require("webpack");

module.exports = {
  context: __dirname + "/src",
  entry: {
    app: ["./home.js", "./events.js", "./vendor.js"],
  },
  output: {
    path: __dirname + "/dist",
    filename: "[name].bundle.js",
  },
};
```
所有文件会按数组顺序一起打包到 dist/app.bundle.js 一个文件当中。
    
2. ##### 多个文件，多个输出
```
const webpack = require("webpack");

module.exports = {
  context: __dirname + "/src",
  entry: {
    home: "./home.js",
    events: "./events.js",
    contact: "./contact.js",
  },
  output: {
    path: __dirname + "/dist",
    filename: "[name].bundle.js",
  },
};
```
你还可以选择打包成多个 JS 文件来将应用拆解成几个部分。像上面这样做就可以打包成三个文件： `dist/home.bundle.js` 、 `dist/events.bundle.js` 和 ` dist/contact.bundle.js` 。

3. ##### 进阶自动打包

如果你正在将应用拆解，打包成多个 output的话（如果应用的某部分有大量不需要提前加载的 JS 的话，这样做会很有用），那么在这些文件里就有可能出现重复的代码，因为在解决依赖问题的时候它们是互相不干预的。幸好，Webpack 有一个内建插件 **CommonsChunk** 来处理这个问题。

```
module.exports = {
  // …
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: "commons",
      filename: "commons.js",
      minChunks: 2,
    }),
  ],
// …
};
```

现在，在 output 的文件里，如果有任意模块加载了两次或更多（通过 minChunks 设置该值），它就会被打包进一个叫 commons.js 的文件里，后面你就可以在客户端缓存这个文件了。当然，这肯定会造成一次额外的请求，但是却避免了客户端多次下载相同库的问题。所以在很多场景下，这都是提升速度的举措。


