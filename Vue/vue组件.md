## Vue-组件

### 什么是组件
组件（Component）是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素， Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。

### 组件的使用

#### 1. 注册
1. 要注册一个全局组件，你可以使用Vue.component(tagName, options)。例如：
```javascript
Vue.component('my-component', {
    //选项
});
```
2. 组件在注册之后，便可以在父实例的模块中以自定义元素```<my-component></my-component>```的形式使用。**要确保在初始化根实例之前注册了组件：**
```html
<div id="example">
    <my-component></my-component>
</div>
```
```javascript
// 先注册
Vue.component('my-component', {
    template: '<div>A custom component !</div>'
});
// 再创建根实例
new Vue({
    el: '#example',
});
```
#### 2. 局部注册
##### 不必在全局注册每个组件。通过使用组件实例选项注册，可以使组件仅在另一个实例/组件的作用域中可用：
    ```
    var Child = {
      template: '<div>A custom component!</div>'
    }
    new Vue({
      // ...
      components: {
        // <my-component> 将只在父模板可用
        'my-component': Child
      }
    })
    ```
#### 4. DOM模板解析说明
##### 当使用 DOM 作为模版时（例如，将 el 选项挂载到一个已存在的元素上）, 你会受到 HTML 的一些限制，因为 Vue 只有在浏览器解析和标准化 HTML 后才能获取模版内容。尤其像这些元素 <ul> ，<ol>，<table> ，<select> 限制了能被它包裹的元素， 而一些像 <option> 这样的元素只能出现在某些其它元素内部。