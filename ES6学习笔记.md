- ### let const命令


- ### 结构赋值


- ### 正则扩展


- ### 字符串扩展


- ### 数值扩展


- ### 数组扩展

    #### 1. Array.of
    ```javascript
    let arr = Array.of(3,4,7,9,11);
    console.log('arr=', arr);
    // arr= [3,4,7,9,11]
    ```
    #### 2. Array.from
    ```javascript
    console.log(Array.from([1,2,3], function(item){
        return item * 2;
    }));
    // [2,4,6];
    ```
    #### 3. Array.fill
    ```javascript
    console.log([1,'a', 3].fill(7));
    // [7,7,7];
    console.log([1,'a', 3].fill(7, 1, 3));
    // [1, 7, 7]
    // Array.fill(x,y,z)
    // x 替换为的值 y 从什么位置开始替换（含） 3替换的结束位置（不含）
    ```
    #### 4. Array.keys() Array.values() Array.entries()
    ```javascript
    var arr = ['a', 'b', 'c'];
    console.log(arr.keys)
    // Array Iterator {}
    for(let index of arr.keys()){
        console.log(index)
    }
    // 0 1 2
    
    for(let value of arr.values()){
        console.log(value);
    }
    // 'a' 'b' 'c'
    // 注：Array.values()是ES7提案中的方法，需引入解析包兼容解决
    // import 'babel-polyfill'
    
    for(let [index, value] of arr.entries()){
        console.log(index, value)
    }
    // 0 "a"
    // 1 "b"
    // 2 "c"
    // 注：Array.entries()为ES6支持，无兼容问题
    ```
    
    #### 5. Array.copyWithin
    ```javascript
    var arr = [1, 2, 3, 4, 5, 6, 7];
    console.log(arr.copyWithin(0, 3, 5))
    // [4, 5, 3, 4, 5, 6, 7]
    // Array.copyWithin(x, y, z)
    // 匹配第x位, 将从y（含）到z（不含）之间的内容替换到x的位置
    ```
    
    #### 6. Array.find Array.findIndex
    ```javascript
    var arr = [1, 2, 3, 4, 5, 6, 7];
    console.log(arr.find(function(item){
        return item > 3
    }));
    // 4
    // 只匹配第一个匹配到的内容
    
    console.log(arr.findIndex(function(item){
        return item > 3;
    }))
    // 3
    // 只匹配第一个匹配的下标索引
    ```
    
    #### 7. Array.includes
    ```javascript
    var arr = [1, 2, 3, NaN];
    console.log(arr.includes(1)); // true
    console.log(arr.includes(NaN)); // true
    // 注：includes方法可以匹配数组中是否存在NaN，虽然NaN===NaN  => false
    ```
    
- ### 函数扩展
    #### 1. 参数默认值

    ```javascript
    function test (x, y='world') {
        console.log(x, y)
    }
    test('hello'); // hello world
    test('hello', 'es6'); // hello es6
    // 注：带有默认值的参数后面不允许再有没有默认值的参数，但可以接有默认值的参数
    // 例：function test (x, y='hello', z) {} 错误
    ```
    
    #### 2. 作用域
    ```javascript
    let x = 'hello';
    function test (x, y=x) {
        console.log(x, y);
    }
    test('world'); // world world
    test(); // undefined undefined
    ```
    
    #### 3. rest参数
    ```javascript
    function test (...arg) {
        console.log(arg)
    }
    test(1,2,3,4,5);
    // [1,2,3,4,5];
    console.log('a', ...[1,2,5])
    // 'a' 1 2 5
    ```
    
    #### 4. 箭头函数
    ```javascript
    let arrow = v => v * 2;
    console.log(arrow(3)); // 6
    ```
    
    #### 5. 伪调用
    ```javascript
    function tail(x) {
        console.log(x);
    }
    function fx(x) {
        return tail(x);
    }
    console.log(fx(123));
    ```
    
- ### 对象扩展
    #### 1. 简洁表示法

    ```javascript
    let o = 1; 
    let k = 2;
    let obj = {o, k};
    
    let es5_method = {
        hello: function(){
            console.log('hello');
        }
    }
    let es6_methods = {
        hello () {
            console.log('hello');
        }
    }
    console.log(es5_method.hello(), es6_method.hello());
    // 'hello' 'hello'
    ```
    
    #### 2. 属性表达式
    ```javascript
    let a = 'b';
    let es5_obj = {
        a: 'c'
    }
    let es6_obj = {
        [a]: 'c'
    }
    console.log(es5_obj, es6_obj);
    // {a: 'c'} {b: 'c'}
    ```
    
    #### 3. 新增API
    ```javascript
    console.log('字符串', Object.is('abc', 'abc'), 'abc'==='abc')
    // 字符串 true true
    console.log('数组', Object.is([], []), []===[])
    // 数组 false false
    // 注：Object.is()从功能上和===一样
    
    console.log('拷贝', Object.assign({a: 'a'}, {b: 'b'}));
    // {a: 'a', b: 'b' };
    // 注：浅复制
    
    let test = {K: 123, o: 456};
    for(let [key, value] of Object.entries(test)) {
        console.log([key, value])
    }
    // ["K", 123]
    // ["o", 456]
    ```
    
    #### 4. 扩展运算符
    ```javascript
    let {a, b, ...c} = {a: 'aaa', b: 'bbb', c: 'ccc', d: 'ddd'}
    console.log(c);
    // {c:'ddd', d:'ddd'}
    // 注：E6暂不支持，不推荐使用
    ```
    
- ### Symbol类型
    #### 1. Symbol的概念
    1. ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。
    2. 基本数据类型有6种：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object），
    这里新添加了一种：Symbol
    3. 注意，Symbol函数前不能使用new命令，否则会报错。这是因为生成的Symbol是一个原始类型的值，不是对象，Symbol函数可以接受一个字符串作为参数，表示对Symbol实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。
    

    ```javascript
    let a1 = Symbol();
    let a2 = Symbol();
    console.log(a1===a2); // false
    
    let a3 = Symbol.for('a3');
    let a4 = Symbol.for('a3');
    console.log(a3===a4); // true
    ```
    
    #### 2. Symbol的作用
    ```javascript
    let a1 = Symbol.for('abc');
    let obj = {
        [a1]: 123,
        abc: 456,
        c: 789
    }
    console.log(obj); // {abc: 456, c: 789, Symbol(abc): 123}
    for(let [key, value] of Object.entries(obj)){
        console.log(key, value);
    }
    // abc 456
    // c 789
    
    Object.getOwnPropertySymbols(obj).forEach(item => {
        console.log(item)
    })
    // Symbol(abc)
    
    Reflect.ownKeys(obj).forEach( item => {
        console.log(item, obj[item])
    })
    // abc 456
    // c 789
    // Symbol(abc) 123
    ```
    
- ### 数据结构
    #### 1. Set

    ```javascript
    let list = new Set();
    list.add(5);
    list.add(7);
    console.log(list.size); // 2
    ```
    ```javascript
    let arr = [1,2,3,4,5];
    let list = new Set(arr);
    console.log(list.size); // 5
    ```
    ```javascript
    let list = new Set();
    list.add(1);
    list.add(2);
    list.add(1);
    console.log(list);
    // Set(2) {1, 2}
    ```
    ```javascript
    let arr = [1,2,3,4,3,2,1];
    console.log(new Set(arr));
    // Set(4) {1, 2, 3, 4};
    console.log(list.has('add')); // true
    console.log(list.delete('add')); // true
    list.clear();
    console.log(list); // Set(0) {}
    ```
    ```javascript
    // Set的遍历
    let arr=['add','delete','clear','has'];
    let list=new Set(arr);
    
    for(let key of list.keys()){
        console.log(key);
    }
    for(let value of list.values()){
        console.log(value);
    }
    for(let [key,value] of list.entries()){
        console.log(key,value);
    }
    
    list.forEach(function(item){console.log(item);})
    ```
    
    #### 2. WeakSet
    ```javascript
    let weakList = new WeakSet();
    let arg = {};
    weakList.add(arg); // 写法正确
    weakList.add(2); // 写法错误，WeakList只能添加对象属性
    ```
    
    #### 4. Map
    ```javascript
    let map = new Map();
    let arr = ['123'];
    map.set(arr, 456);
    console.log('map',map,map.get(arr));
    ```
    ```javascript
    let map = new Map([['a',123],['b',456]]);
    console.log('map args',map);
    console.log('size',map.size);
    console.log('delete',map.delete('a'),map);
    console.log('clear',map.clear(),map);
    ```
    注：Map的属性操作和遍历和Set基本一样。
    #### 4. WeakMap
    ```javascript
    let weakmap=new WeakMap();
    let o={};
    weakmap.set(o,123);
    console.log(weakmap.get(o));
    ```
    
- ### Proxy Reflect
    #### 1. Proxy

    ```javascript
    {
        let obj = {
            time: '2017-03-11',
            name: 'net',
            _r: 123
        };
        let monitor = new Proxy(obj, {
            // 拦截对象属性的读取
            get(target, key) {
                return target[key].replace('2017', '2018')
            },
            // 拦截对象设置属性
            set(target, key, value) {
                if (key === 'name') {
                    return target[key] = value;
                } else {
                    return target[key];
                }
            },
            // 拦截key in object操作
            has(target, key) {
                if (key === 'name') {
                    return target[key]
                } else {
                    return false;
                }
            },
            // 拦截delete
            deleteProperty(target, key) {
                if (key.indexOf('_') > -1) {
                    delete target[key];
                    return true;
                } else {
                    return target[key]
                }
            },
            // 拦截Object.keys,Object.getOwnPropertySymbols,Object.getOwnPropertyNames
            ownKeys(target) {
                return Object.keys(target).filter(item = > item != 'time')
            }
        });
        console.log('get', monitor.time);
        monitor.time = '2018';
        monitor.name = 'mukewang';
        console.log('set', monitor.time, monitor);
        console.log('has', 'name' in monitor, 'time' in monitor);
        // delete monitor.time;
        // console.log('delete',monitor);
        //
        // delete monitor._r;
        // console.log('delete',monitor);
        console.log('ownKeys', Object.keys(monitor));
    }
    ```

    #### 2. Reflect
    
    ```javascript
    let obj = {
        time: '2017-03-11',
        name: 'net',
        _r: 123
    };
    console.log('Reflect get', Reflect.get(obj, 'time'));
    Reflect.set(obj, 'name', 'mukewang');
    console.log(obj);
    console.log('has', Reflect.has(obj, 'name'));
    ```
    
- ### class 类
    
    #### 1. 基本定义 和 生成实例

    ```javascript
    class Parent {
        constructor(name="xx"){
            this.name = name;
        }
    }
    let v_parent = new Parent('v');
    console.log('构造函数和实例', v_parent);
    
    ```
    
    #### 2. 继承
    
    ```javascript
    class Parent {
        constructor(name="x"){
            this.name = name;
        }
    }
    class Child extends Parent {
        constructor(name="child"){
            super(name); // 需要放在第一行
            this.type = 'child'
        }
    }
    
    console.log('继承', new Child());
    ```
    
    #### 3. getter , setter
    
    ```javascript
    class Parent {
        constructor (name="qi"){
            this.name = name;
        }
        
        get longName () {
            return 'liu' + this.name
        }
        
        set longName (value) {
            this.name = value;
        }
    }
    
    let v = new Parent();
    console.log('getter', v.longName);
    v.longName = 'xiao';
    console.log('setter', v.longName);
    ```
    
    #### 4. 静态方法
    
    静态方法是通过类去调用，而不是通过类的实例去调用
    
    ```javascript
    class Parent {
        constructor (name='qi'){
            this.name = name;
        }
        
        static tell(){
            console.log('hello world');
        }
    }
    
    Parent.tell();
    
    ```
    
    #### 5. 静态属性
    
    ```javascript
    class Parent {
        constructor (name='qi'){
            this.name = name;
        }
        
    }
    Parent.type = 'test';
    
    console.log('静态属性', Parent.type);
    
    ```
    
    

- ### Promise
    #### 1. 传统异步回调

    ```javascript
    let ajax = function(cb){
        console.log('执行');
        setTimeout(function(){
            cb && cb.call();
        }, 1000)
    }
    function fn () {
        console.log('timeout1');
    }
    ajax(fn);
    // 执行
    // timeout1
    ```
    
    #### 2. 使用Promise
    
    ```javascript
    let ajax = function(){
        console.log('执行');
        return new Promise(function(resolve, reject){
            setTimeout(function(){
                resolve();
            }, 1000)
        });
    }
    ajax().then(function(){
        console.log('promise', 'timeout2');
    })
    ```
    ```javascript
    let ajax = function(){
        console.log('执行');
        return new Promise(function(resolve, reject){
            setTimeout(function(){
                resolve();
            }, 1000)
        });
    }
    ajax()
    .then(function(){
        console.log('promise', 'timeout2');
        return new Promise(function(resolve, reject){
            setTimeout(function(){
                resolve();
            }, 2000)
        })
    })
    .then(function(){
        console.log('promise', 'timeout3')
    });
    ```
    
    #### 3. 错误捕获
    ```javascript
    let ajax = function(num){
        console.log('执行');
        return new Promise(function(resolve, reject){
            if(num>5){
                resolve();
            }else{
                throw new Error('出错了');
            }
        })
    }
    ajax(5)
    .then(function(){
        console.log('promise', 'timeout4')
    })
    .catch(function(err){
        console.log('catch', err);
    })
    ```
    
    #### 4. Promise.all
    ```javascript
    // 需图片全部加载完
    function loadImg (src) {
        return new Promise(function(resolve, reject){
            let img = document.createElement('img');
            img.src = src;
            img.onload = function(){
                resolve(img);
            }
            img.onerror = function(){
                reject(err);
            }
        })
    }
    function showImgs(imgs){
        imgs.forEach(function(item){
            document.body.appendChild(img);
        })
    }
    
    Promise.all([
        loadImg('http://placehold.it/300/f00/000.png"'),
        loadImg('http://placehold.it/300/f00/000.png"'),
        loadImg('http://placehold.it/300/f00/000.png"')
    ])
    .then(showImgs)
    ```
    
    #### 5. Promise.rece
    ```javascript
    // 有一个图片加载完毕即可
    function loadImg (src) {
        return new Promise(function(resolve, reject) {
            let img = document.createElement('img');
            img.src = src;
            img.onload = function(){
                resolve(img)
            }
            img.onerror = function(err){
                reject(err);
            }
        })
    }
    function showImg (img){
        document.body.appendChild(img)
    }
    Promise.race([
        loadImg('http://placehold.it/300/f00/000.png"'),
        loadImg('http://placehold.it/300/f00/000.png"'),
        loadImg('http://placehold.it/300/f00/000.png"')
    ])
    .then(showImg);
    ```
    
- ### Iterator 和 for...of循环

    #### 1. 示例
    ```javascript
    let arr = ['hello', 'world'];
    let map = arr[Symbol.iterator]();
    console.log(map.next());
    onsole.log(map.next());
    onsole.log(map.next());
    ```