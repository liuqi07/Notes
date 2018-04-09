## vuejs

### 模板语法
1. 使用Javascript表达式
    1. 迄今为止，在我们的模板中，我们一直都只绑定简单的属性键值。但实际上，对于所有的数据绑定， Vue.js 都提供了完全的 JavaScript 表达式支持。
    ```
    {{ number + 1 }}
    {{ ok ? 'YES' : 'NO' }}
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id"></div>
    ```
    2.这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都不会生效。
    ```
    <!-- 这是语句，不是表达式 -->
    {{ var a = 1 }}
    <!-- 流控制也不会生效，请使用三元表达式 -->
    {{ if (ok) { return message } }}
    ```

### 计算属性
---
- #### 计算属性
    模板内的表达式是非常便利的，但是它们实际上只用于简单的运算。在模板中放入太多的逻辑会让模板过重且难以维护。例如：
    ```html
    <div id="example">
        {{ message.split('').reverse().join('') }}
    </div>
    ```
    在这种情况下，模板不再简单和清晰。在意识到这是反向显示 message 之前，你不得不再次确认第二遍。当你想要在模板中多次反向显示 message 的时候，问题会变得更糟糕。
    这就是对于任何复杂逻辑，你都应当使用**计算属性**的原因。
    
    1. ##### **#** 基础例子
    ```html
    <div id="example">
        <p> Original message: {{ message }} </p>
        <p> Computed reversed message: {{ reversedMessage }} </p>
    </div>
    ```
    ```javascript
    var vm = new Vue({
        el: '#example',
        data: {
            message: 'Hello'
        },
        computed: {
            reversedMessage: function(){
                return this.message.split('').reverse().join('');
            }
        }
    });
    ```
    > vm.reversedMessage的值始终取决于vm.message
    
    2. ##### **#** 计算缓存 vs Methods
    你可能已经注意到我们可以通过调用表达式中的 method 来达到同样的效果：
    ```html
    <p> Reversed message: {{ reversedMessage() }}</p>
    ```
    ```javascript
    methods: {
        reversedMessage(){
            return this.message.split('').reverse().join('');
        }
    }
    ```
    
    我们可以将同一函数定义为一个 method 而不是一个计算属性。对于最终的结果，两种方式确实是相同的。然而，不同的是**计算属性是基于它们的依赖进行缓存的**。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 ==message== 还没有发生改变，多次访问 ==reversedMessage== 计算属性会立即返回之前的计算结果，而不必再次执行函数。
    
    3. ##### **#** Computed 属性 vs Watched 属性
    Vue 确实提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：watch 属性。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 watch——特别是如果你之前使用过 AngularJS。然而，通常更好的想法是使用 computed 属性而不是命令式的 watch 回调。细想一下这个例子：
    ```html
    <div id="demo">{{ fullName }}</div>
    ```
    ```javascript
    var demo = new Vue({
        el: '#demo',
        data: {
            firstName: 'Foo',
            lastName: 'Bar',
            fullName: 'Foo Bar'
        },
        methods: {
            fullName(){
                return this.firstName + ' ' + this.lastName;
            }
        }
        watch: {
            firstName(val){
                this.fullName = val + ' ' + lastName;
            },
            lastName(val){
                this.fullName = firstName + ' ' + val;
            }
        }
    });
    ```
    上面代码是命令式的和重复的。将它与 computed 属性的版本进行比较：
    ```javascript
    var demo = new Vue({
        el: '#demo',
        data: {
            firstName: 'Foo',
            lastName: 'Bar'
        },
        computed: {
            fullName(){
                return this.firstName + ' ' + this.lastName;
            }
        }
    });
    ```
    4. ##### **#** 计算setter
    计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：
    ```javascript
    computed: {
        fullName: {
            get: function(){
                return this.firstName + ' ' + this.lastName;
            },
            set: function(newVal){
                var names = newVal.split(' ');
                this.firstName = names[0];
                this.lastName = names[1];
            }
        }
    }
    ```
    
### 观察 Watchers
---
虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的 ==watcher== 。这是为什么 Vue 提供一个更通用的方法通过 ==watch== 选项，来响应数据的变化。当你想要在数据变化响应时，执行异步操作或开销较大的操作，这是很有用的。
```html
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>
```
```javascript
<!-- Since there is already a rich ecosystem of ajax libraries    -->
<!-- and collections of general-purpose utility methods, Vue core -->
<!-- is able to remain small by not reinventing them. This also   -->
<!-- gives you the freedom to just use what you're familiar with. -->
<script src="https://unpkg.com/axios@0.12.0/dist/axios.min.js"></script>
<script src="https://unpkg.com/lodash@4.13.1/lodash.min.js"></script>
<script>
var watchExampleVM = new Vue({
    el: '#watch-example',
    data: {
        question: '',
        answer: 'I cannot give you an answer until you ask a question!'
    },
    watch: {
        // 如果 question 发生改变，这个函数就会运行
        question: function (newQuestion) {
            this.answer = 'Waiting for you to stop typing...'
            this.getAnswer()
        }
    },
    methods: {
        // _.debounce 是一个通过 lodash 限制操作频率的函数。
        // 在这个例子中，我们希望限制访问yesno.wtf/api的频率
        // ajax请求直到用户输入完毕才会发出
        // 学习更多关于 _.debounce function (and its cousin
        // _.throttle), 参考: https://lodash.com/docs#debounce
        getAnswer: _.debounce(
            function () {
                var vm = this;
                if (this.question.indexOf('?') === -1) {
                    vm.answer = 'Questions usually contain a question mark. ;-)';
                    return;
                }
                vm.answer = 'Thinking...';
                axios.get('https://yesno.wtf/api')
                    .then(function (response) {
                        vm.answer = _.capitalize(response.data.answer);
                    })
                    .catch(function (error) {
                        vm.answer = 'Error! Could not reach the API. ' + error;
                    })
            },
            // 这是我们为用户停止输入等待的毫秒数
            500
        )
    }
})
</script>
```