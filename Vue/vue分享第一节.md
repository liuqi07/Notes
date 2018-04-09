## Vue.js

### 一、初步了解[vue.js](http://cn.vuejs.org/)框架
1. 轻量级的[MVVM](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)框架
2. react的组件化以及angular灵活的指令
3. 中文支持非常好

官方示例：
```html
<div id="demo">
    <p> {{ message }} </p>
    <input v-model="message">
</div>
```
```javascript
var demo = new Vue({
    el: '#demo',
    data: {
        message: 'Hello Vue.js!'
    }
});
```

组件化：

```
graph LR
A[*.vue] --> B[webpack]
B --> C{编译打包}
C --> | telplate | D[*.html]
C --> | script | E[*.js]
C --> | style | F[*.css]
```


### 二、vuejs的开发环境搭建以及脚手架工具的使用
1. 直接下载并用` <script> `标签引入，`Vue` 会被注册为一个全局变量。**重要提示：在开发时请用开发版本，遇到常见错误它会给出友好的警告。**
    1. 开发版本：包含完整的警告和调试模式
    2. 生产版本：删除了警告
2. CDN
    1. 官方推荐unpkg：https://unpkg.com/vue@2.3.2/dist/vue.js    
3. npm
    1. 使用vue构建大型应用时推荐使用npm安装
    ```
    # 最新稳定版本
    $ npm install vue
    ```
4. 命令行工具
    1. Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目：
    ```
    # 全局安装 vue-cli
    $ npm install --global vue-cli
    # 创建一个基于 webpack 模板的新项目
    $ vue init webpack my-project
    # 安装依赖
    $ cd my-project
    $ npm install
    $ npm run dev
    ```
    
### 三、vuejs具体指令和简单项目实践
1. Vue.js组件的重要选项 - **data**

```javascript
new Vue({
    data: {
        a: 1,
        b: []
    }
});
```
```html
<p> {{ a }} </p>
```

2. **methods**

```javascript
new Vue({
    data: {
        a: 1,
        b: []
    },
    methods: {
        doSomething: function(){
            console.log(this.a);
        }
    }
});
```

3. **watch**

```javascript
new Vue({
    data: {
        a: 1,
        b: []
    },
    methods: {
        doSomething: function(){
            this.a ++;
        }
    },
    watch: {
        'a': function(val, oldVal){
            console.log(val, oldVal);
        }
    }
});
```

#### 模板指令
1. 数据渲染： v-text, v-html, {{ }}

```html
<p> {{ a }} </p>
<p v-text="a"></p>
<p v-html="b"></p>
```
```javascript
new Vue({
    data: {
        a: 1,
        b: []
    }
});
```

2. 控制模块隐藏： v-if, v-show

```html
<p v-if="isShow"></p>
<p v-show="isShow"></p>
```
```javascript
new Vue({
    data: {
        isShow: true
    }
});
```

3. 渲染循环列表： v-for

```html
<ul>
    <li v-for="item in items">
        <p v-text="item.label"></p>
    </li>
</ul>
```
```javascript
data: {
    items: [
        {label: 'apple'},
        {label: 'banana'}
    ]
}
```

4. 事件绑定: v-on

```html
<button v-on:click="doThis"></button>
<button @click="doThis"></button>
```
```javascript
methods: {
    doThis: function(someThing){
    
    }
}
```

5. 属性绑定： v-bind

```html
<img v-bind:src="imageSrc">
<div :class="{red: isRed }">
<div :class="[classA, classB]">
<div :class="[classA, { classB: isB, classC: isC }]">
```
