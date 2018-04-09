## 

### Class与Style绑定

### 条件渲染

1. v-if
2. v-else
3. v-else-if
4. 用key管理可复用的元素

### v-for

1. 基本用法
2. 对象迭代
    1. 可以接受三个参数: (value, key, index)
    2. 在遍历对象时，是按 Object.keys() 的结果遍历，但是不能保证它的结果在不同的 JavaScript 引擎下是一致的。
3. 整数迭代

### 数组更新检测

#### 1. 变异方法
vue包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下：
* push()
* pop()
* shift()
* unshift()
* splice()
* sort()
* reverse()
    
#### 2. 重塑数组
这些不会改变原来数组，但总返回一个新数组。
* filter()
* concat()
* slice()
    
#### 3. 注意事项
由于javascript的限制， Vue不能检测一下变动的数组：
1. 当你利用索引值直接设置一个项时：例如： ``vm.items[index] = newValue``
2. 当你修改数组的长度时，例如：``vm.items.length = newLength``

为了解决第一类问题，实现相同效果并且触发状态更新
1. Vue.set(vm.items, index, newVal);
2. vm.items.splice(index, 1, newVal);

为了解决第二类问题
1. vm.items.splice(newLength);

#### 4. 显示过滤/排序结果

有时，我们想要显示一个数组的过滤或排序副本，而不实际改变或重置原始数据。在这种情况下，可以创建返回过滤或排序数组的计算属性。

```html
    <li v-for="n in evenNumbers"> {{ n }} </li>
```
```javascript
data: {
    numbers: [1, 2, 3, 4, 5]
},
computed: {
    evenNumbers(){
        return this.numbers.filter(function(val){
            return val % 2 === 0;
        });
    }
}
```
或者，你也可以在计算属性不适用的情况下（例如：在嵌套v-for循环中）使用methods方法：

```html
<li v-for="n in even(numbers)">{{ n }}</li>
```
```javascript
data: {
    numbers: [1, 2, 3, 4, 5]
},
methods: {
    even(numbers){
        return numbers.filter(function(val){
            return val % 2 === 0;
        });
    }
}
```

#### 5. 事件处理器

1. $event：原生事件对象
```
<button v-on:click="warn('Form cannot be submitted yet.', $event);"></button>
```

2. 事件修饰符
    1. 在事件处理程序中调用 ==event.preventDefault()== 或 ==event.stopPropagation()== 是非常常见的需求。尽管我们可以在 methods 中轻松实现这点，但更好的方式是：methods 只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。
    2. 为了解决这个问题， Vue.js 为 ==v-on== 提供了 **事件修饰符**。通过由点(.)表示的指令后缀来调用修饰符。
    * .stop
    * .prevent
    * .capture
    * .self
    * .once
    ```
    <!-- 阻止单击事件冒泡 -->
    <a v-on:click.stop="doThis"></a>
    <!-- 提交事件不再重载页面 -->
    <form v-on:submit.prevent="onSubmit"></form>
    <!-- 修饰符可以串联  -->
    <a v-on:click.stop.prevent="doThat"></a>
    <!-- 只有修饰符 -->
    <form v-on:submit.prevent></form>
    <!-- 添加事件侦听器时使用事件捕获模式 -->
    <div v-on:click.capture="doThis">...</div>
    <!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
    <div v-on:click.self="doThat">...</div>
    <!-- 点击事件将只会触发一次 -->
    <a v-on:click.once="doThis"></a>
    ```

3. 按键修饰符
    1. 在监听键盘事件时，我们经常需要监测常见的键值。 Vue 允许为 v-on 在监听键盘事件时添加按键修饰符，记住所有的 keyCode 比较困难，所以 Vue 为最常用的按键提供了别名：
    * .enter
    * .tab
    * .delete(捕获‘删除’和‘退格’键)
    * .esc
    * .space
    * .up
    * .down
    * .left
    * .right
    * .ctrl
    * .alt
    * .shift
    * .meta
    ```
    <!-- Ctrl + C -->
    <input @keyup.ctrl.67="clear">
    ```
    ```
    //可以通过全局config.keyCodes对象自定义按键修饰符别名
    //可以使用 v-on:keyup.f1
    Vue.config.keyCodes.f1 = 112;
    ```
    
    