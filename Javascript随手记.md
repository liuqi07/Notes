* #### 多维数组转一维数组

    ```javascript
    // 递归
    var arr = [1,[2,[[3,4],5],6]];
    var newArr = [];
    function arrFn (arr) {
    	arr.forEach(item => {
    		if(item instanceof Array){
    			arrFn(item);
    		}else {
    			newArr.push(item)
    		}
    	});
    	return newArr;
    }
    console.log(arrFn(arr)); // [1, 2, 3, 4, 5, 6]
    ```
    ```javascript
    // Array.prototype.toString()
    var arr = [1,[2,[[3,4],5],6]];
    var newArr = arr.toString().split(',');
    console.log(newArr); // ["1", "2", "3", "4", "5", "6"]
    ```
    
* #### i++ 与 ++i 区别
    
    ```javascript
    // i++；先赋值在自加；
    // ++i；先自加在赋值；
    // 在赋值运算中有区别，单独使用没有区别
    var i = 1;
    var num = ++i + i++ + i++ + i++ + ++i;
    console.log(num,i); // 17,6
    ```
    
* #### 判断是否是个数组
    
    1. instanceof 操作符
    
    ```javascript
    // 判断Array的prorotype属性是不是在arr的原型链上，是返回true,否返回false;
    var arr = [];
    console.log(arr instanceof Array); // true
    ```
    2. 对象的constructor属性
    
    ```javascript
    // arr.__proto__.constructor返回的结果为构造函数本身
    var arr = [];
    console.log(arr.__proto__constructor === Array); // true
    ```
    
    3. Array.isArray()
    
        ECMAScript5中引入了Array.isArray()方法，用于专门判断一个对象是不是数组，是返回true，不是返回false;目前所有主流浏览器和IE9+都对其进行了支持，IE8及以下浏览器不支持该方法。
        
    ```
    var arr = [];
    console.log(Array.isArray(arr)); // true
    ```
    
* #### 逻辑运算符
    
    ```javascript
    console.log( 0 || 1 ); // 1
    console.log( 1 || 2 ); // 1
    console.log( 0 && 1 ); // 0
    console.log( 1 && 2 ); // 2
    // 在JavaScript中， || 和 && 都是逻辑运算符，用于在从左至右计算时，返回第一个可完全确定的“逻辑值”。
    ```
    
* #### 递归
    
    1. 递归函数：是指函数直接或间接调用函数本身，则称该函数为递归函数。
    
    ```javascript
    // 例：5的阶乘
    function func (n) {
        if(n<=1){
            return 1;
        }
        return n * func(n-1)
    }
    func(5); // 120
    ```
    2. 在使用递增归策略时，必须有一个明确的递归结束条件，称为递归出口，否则将无限进行下去（内存溢出）
    
    3. 递归函数趣味实例
    
        古典问题——有一对兔子，从出生后第3个月起每个月都生一对兔子，小兔子长到第三个月后每个月又生一对兔子，假如兔子都不死，问第三年每个月的兔子总数为多少？
        
        ```
        function fn (n) {
            if (n == 0 || n == 1){
                return 1;
            }
            return func(n-1) + func(n-2);
        }
        console.log(fn(22));
        ```
    
* #### call() 与 apply()

    1. 每个函数都包含两个非继承而来的方法：call()方法和apply()方法。
    
        都是在特定的作用域中调用函数，等于设置函数体内this对象的值，以扩充函数赖以运行的作用域。
        
        一般来说，this总是指向调用某个方法的对象，但是使用call()和apply()方法时，就会改变this的指向。
        
    ```javascript
    function add(c,d){
    	return this.a + this.b + c + d;
    }
    var o = {a:1, b:2};
    add.call(o, 3, 4); // 10
    add.apply(o, [3, 4]); // 10
    ```
    
    2. 拓展
    
        1. apply可以将一个数组默认的转换为一个参数列表([param1,param2,param3] 转换为 param1,param2,param3)，故可以实现一些特殊的需求
        
            ```javascript
            var arr = [1,2,3,4,5];
            Math.max(...arr); // 5
            Math.max.apply(null, arr); // 5
            ```
            ```javascript
            // 数组排序，仅看思路，方法不推荐
            var arr = [2,3,1,4,0,6];
            var newArr = [];
            for(var i=0,len=arr.length;i<len;i++){
            	var min = Math.min.apply(null,arr);
                newArr.push(min);
                var index = arr.indexOf(min);
                arr.splice(index,1);
            }
            console.log(newArr)
            ```
            ```javascript
            var arr1 = [1,2,3];
            var arr2 = [4,5,6];
            Array.prototype.push.apply(arr1, arr2);
            console.log(arr1); // [1,2,3,4,5,6]
            ```
        
        2. Array.prototype.slice.call(arguments)
        
            Array.prototype.slice.call(arguments)能将具有length属性的对象转成数组
            
            ```javascript
            var a={length:2,0:'first',1:'second'};
            Array.prototype.slice.call(a);//  ["first", "second"]
            var a={length:2};
            Array.prototype.slice.call(a);//  [undefined, undefined]
            // 原理剖析
            // Array.prototype.slice内部猜想
            Array.prototype.slice = function(start, end){
                var result = new Array();
                start = start || 0;
                end = end || this.length; // this指向调用slice方法时的对象，通过call能改变this指向，也就是传进来的第一个参数，这是关键
                for(var i=start; i<end; i++){
                    result.push(this[i]);
                }
                return result;
            }
            ```
            
- ### 基本类型 与 引用类型

- ### 深拷贝 与 浅拷贝
    
    深复制和浅复制最根本的区别在于**是否是真正获取了一个对象的复制实体而不是一个引用**，从深层次上讲深复制在计算机中开辟了一块内存地址用于存放复制的对象，而浅复制仅仅是指向被复制的内存地址，如果原地址中对象被改变了，那么浅复制出来的对象也会相应改变。

    #### 1. 数组
    ```javascript
    // 深拷贝，支持多维数组，但是数组中有对象不支持
    var arr1 = [1,2,3];
    var arr2 = arr1.slice();
    var arr3 = arr1.concat([]);
    // ------- 分割线 --------
    var arr = [{x:1, y:2},3,4];
    var newArr = arr.slice();
    arr[0].x = 10;
    console.log(newArr);
    // [{x:10, y:2},3,4]
    ```
    
    #### 2. 对象
    
    - 浅拷贝：只拷贝对象的第一层属性，对于属性中包含的属性不会复制；由于JavaScript对象均以地址的方式存贮，所以浅复制导致多个对象的属性均指向同一块地址。
    
    - 深拷贝：对对象的每一层属性进行递归复制，深层次的属性也不会指向同一块地址【同一个对象】。
    
    ```javascript
    // 浅拷贝，只能拷贝一层
    function shallowCopy (obj) {
        var newObj = {};
        for(var key in obj){
            if(obj.hasOwnProperty(key)){
                newObj[key] = obj[key];
            }
        }
        return newObj;
    }
    var obj = { a:1, b:2, c: { x: true, y: false } };
    var newObj = shallowCopy(obj);
    obj.a = 10;
    obj.c.x = false;
    console.log(obj);
    // { a:10, b:2, c: { x: false, y: false } }
    console.log(newObj);
    // { a:1, b:2, c: { x: false, y: false } }
    
    // 深拷贝
    function deepCopy (obj) {
        if(obj instanceof Array){
            var result = [];
            for(var i=0, len=obj.length; i<len; i++){
                result[i] = deepCopy(obj[i])
            }
            return result;
        }
        else if (obj instanceof Object) {
            var result = {};
            for(var key in obj) {
                result[key] = deepCopy(obj[key]);
            }
            return result;
        }
        else {
            return obj;
        }
    }
    var obj = [{x:1, y:2},3,4];
    var newObj = deepCopy(obj);
    obj[0].x = 10;
    console.log(obj); // [{x:10, y:2},3,4]
    console.log(newObj); // [{x:1, y:2},3,4]
    ```
- ### arguments 对象
    
    在函数代码中，使用特殊对象 arguments，开发者无需明确指出参数名，就能访问它们

    它是一个包含所有传给函数的参数的伪数组。为什么是伪数组？—— 你不能修改它，也不能用push来添加新元素等。但是你可以访问其中的元素，并且同时具有.length属性

    ```javascript
    function test(){
        console.log(arguments);
        for(var i=0,len=arguments.length; i<len; i++){
            console.log(arguments[i])
        }
    }
    test(1,2,3); 
    // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    // 1 2 3
    ```
    
    可以用 arguments 对象检测函数的参数个数，引用属性 arguments.length 即可
    ```javascript
    function test(){
        console.log(arguments.length);
    }
    test(1,2,3); // 3
    ```
    
    根据之前说到过的Array.prototype.slice可以将arguments对象提取成数组
    ```javascript
    function test() {
        var argu = Array.prototype.slice.call(arguments);
        return argu;
    }
    console.log(test(1,2,3)); // [1,2,3]
    ```
    
    通过arguments对象可以实现函数重载
    ```javascript
    function test(){
        switch(arguments.length) {
            case 0: 
                // 要执行的代码
                break;
            case 1:
                // 要执行的代码
                break;
            // 更多的 case...
            default: 
                // 要执行的代码
        }
    }
    ```
    
- ### 闭包

    需要满足三个条件：
    1. 调用的函数是父级作用域内部声明的
    2. 调用的函数是在父级作用域之外进行调用
    3. 调用的函数内部使用了父级作用域的内部变量
    
    ```javascript
    // 例1
    function create_counter(num){
        var x = num || 0;
        return {
            inc: function(){
                return ++x; // 注，这里若是x++，则最后调用返回10
            }
        }
    }
    var fn = create_counter(10);
    fn.inc() // 11
    ```
    ```javascript
    // 例2
    // 判断用户是否第一次加载
    function isFirstLoad () {
        var _list = [];
        return function (id){
            if(_list.indexOf(id)>0){ return false; }
            else { _list.pusn(id); return true;}
        }
    }
    let firstLoad = isFirstLoad();
    firstLoad(10); // true
    firstLoad(10); // false
    firstLoad(20); // true
    ```
    
- ### 函数重载
    

> [参考链接](https://www.cnblogs.com/bluedream2009/archive/2011/01/05/1925963.html)

- ### 构造函数 与 原型对象

> [参考链接](http://www.cnblogs.com/xiaohuochai/p/5753952.html)

> [阮一峰Javascript标准参考教程--面向对象编程概述](http://javascript.ruanyifeng.com/oop/basic.html)

- ### Cookie
    
    cookie是浏览器提供的一种机制，它将document对象的cookie属性提供给javascript。可以由javascript对其进行控制。

    要实现跨页面的全局变量，可以使用javascript中的cookie来实现
    
    cookie机制是将信息存储于用户硬盘，因此可以作为全局变量
    
    1. 设置、查询、修改cookie
    ```javascript
    document.cookie="userId=20";
    // 如果要一次存储多个，可以使用分号加空格隔开
    document.cookie='userId=20; userName=lili';
    // 在cookie的键值对中不能使用分号、逗号、等号以及空格，如果必须有，可以使用escape进行编码
    document.cookie = 'userName='+escape('liu qi');
    console.log(document.cookie); // str=liu%20qi
    // 当使用escape编码后，在取出值以后需要使用unescape()进行解码
    document.cookie="userId=20";
    document.cookie='userName=lili';
    console.log(document.cookie); // userId=20; userName=lili;
    // 当执行上面的代码后，键名不同则会往cookie中添加一个新值，键名相同则会更新旧值
    ```
    
    2. 给cookie设置过期时间
    ```
    document.cookie = 'userId=20; expiress=GMT_String';
    // 其中GMT_String是以GMT格式表示的时间字符串，
    // 这条语句就是将userId这个cookie设置为GMT_String表示的过期时间，超过这个时间，cookie将消失，不可访问
    var date = new Date().getTime() + 1000 * 60 * 24;
    document.cookie = 'userId=20; expires='+date.toGMTString()
    ```
    
    3. 删除cookie
    ```
    // 设置一个过去的时间
    var date = new Date().getTime() - 1000;
    document.cookie = 'userId=20; expires='+date.toGMTString();
    ```
    
    4. 通用方法封装
    ```javascript
    // 设置cookie
    function setCookie (key, value, expiresHours) {
        var cookieStr = key + '=' + escape(value);
        if(expiresHours>0){
            var date = new Date();
            date.setTime(date.getTime() + (1000 * 60 * 60 * expiresHours))
            cookieStr = cookieStr + ('; expires=' + date.toGMTString());
        }
        document.cookie = cookieStr;
    }
    setCookie('name', 'liuqi', 2);
    // 获取cookie
    function getCookie (key){
        var tempArr = document.cookie.split('; ');
        for(var i=0;i<tempArr.length;i++){
            var item = tempArr[i].split('='), val = '';
            if(item[0]===key){
                val = unescape(item[1]);
                break;
            }
        }
        return val;
    }
    function getCookie2(key){
        var tempArr = document.cookie.split('; '), val='';
        for(var i=0;i<tempArr.length;i++){
            if(tempArr[i].indexOf(key+'=')>-1){
                val = tempArr[i].slice(key.length+1);
                break;
            }
        }
        return unescape(val);
    }
    // 删除cookie
    function removeCookie(key) {
        var ckey = key + '=';
        var cookie = document.cookie;
        if(cookie.indexOf(ckey)>-1){
            document.cookie = key + '=; expires=Thu, 01 Jan 1970 00:00:00 GMT';
        }else{
            console.log('key值为'+key+'的cookie不存在');
        }
    }
    ```
    
- ### Web Storage
    
    >  对浏览器来说，使用 Web Storage 存储键值对比存储 Cookie方式更直观，而且容量更大，它包含两种：localStorage和sessionStorage

    #### 1. sessionStorage（临时存储）
        
    为每一个数据源维持一个存储区域，在浏览器打开期间存在，包括页面重新加载
        
    #### 2. localStorage（长期存储）
    
    与sessionStorage一样，但是浏览器关闭后，数据依然会一直存在
    
    #### 3. API
    
    > sessionStorage 和 localStorage 的用法基本一致，引用类型的值要转换成JSON
    
    ```javascript
    var info = {
        name: 'liuqi',
        age: '28'
    }
    // 存储
    sessionStorage.setItem('key', JSON.stringify(info));
    localStorage.setItem('key', JSON.stringify(info));
    // 获取
    sessionStorage.getItem('key');
    localStorage.getItem('key');
    // 删除
    sessionStorage.removeItem('key');
    localStorage.removeItem('key');
    // 删除所有数据
    sessionStorage.clear();
    localStorage.clear();
    ```
    
    #### 4. 监听本地存储的变化
    ```javascript
    window.addEventListener('storage', function(e){
        console.log(e)
    })
    ```
    
- ### 三种编码解码方式
    
    ##### 1. escape 和 unescape
    
    > 对除ASCII字母、数字、标点符号（@ * _ + - . /）以外的其他字符进行编码

    ```javascript
    var url = 'http://www.baidu.com?name=liu@qi&age=28';
    var escapeUrl = escape(url); // http%3A//www.baidu.com%3Fname%3Dliu@qi%26age%3D28
    unescape(escapeUrl);
    ```
    
    ##### 2. encodeURI 和 decodeURI
    
    > 返回编码为有效的统一资源标识符 (URI) 的字符串，不会被编码的字符：! @ # $ & * ( ) = : / ; ? + '
    
    > encodeURI()是Javascript中真正用来对URL编码的函数。

    ```javascript
    var url = 'http://www.baidu.com?name=刘奇&age=28岁';
    var encodeURIUrl = encodeURI(url); // http://www.baidu.com?name=%E5%88%98%E5%A5%87&age=28%E5%B2%81
    decodeURI(encodeURIUrl);
    ```
    
    ##### 3. encodeURIComponent 和 decodeURIComponent
    
    > 对URL的组成部分进行个别编码，而不用于对整个URL进行编码
    
    ```javascript
    var url = 'http://www.baidu.com?name=liu@qi&age=28';
    var encodeComUrl = encodeURIComponent(url); // http%3A%2F%2Fwww.baidu.com%3Fname%3Dliu%40qi%26age%3D28
    decodeURIComponent(encodeComUrl);
    ```
    
- ### 事件循环