- ## Object 对象的相关方法

    #### 1. Object.getPrototypeOf()
    
    > 此方法返回参数对象的原型。这是获取原型对象的标准方法
    
    ```javascript
    function Foo (){}
    var foo = new Foo();
    Object.getPrototypeOf(foo) === Foo.prototype; // true
    ```
    以下是几种特殊对象的原型。
    ```javascript
    // 空对象的原型是Object.prototype
    Object.getPrototypeOf({}) === Object.prototype // true
    // Object.prototype 的原型是 null
    Object.getPrototypeOf(Object.prototype) === null // true
    // 函数的原型是 Function.prototype
    function f(){}
    Object.getPrototypeOf(f) === Function.prototype
    ```
    
    #### 2. Object.create()
    
    > 生成实例对象的常用方法是，使用**new**命令让构造函数返回一个实例。但更多时候，只能拿到一个实例对象，它根本不不是由构造函数生成的，那么能不能从一个实例对象，生成另一个实例对象呢？
    
    JavaScript提供了**Object.create**方法，用来满足这种需求。该方法接受一个对象作为参数，然后以它为原型，返回一个实例对象。该实例完全继承原型对象的属性。
    
    ```javascript
    var A = {
        text: 'hello',
        print: function(){
            console.log('world');
        }
    }
    var B = Object.create(A);
    Object.getPrototypeOf(B) === A; // true
    B.text; // hello
    A.text = 'hi';
    B.text; // hi
    B.__proto__ === A; // true
    ```
    
    上述代码中，**Object.create**以A对象为原型，生成了**B**对象。**B**继承了**A**的所有属性和方法。
    
    并且，**Object.create** 方法生成的新对象，动态继承了原型。在原型上添加或修改任何方法，会立刻反映在新对象之上。
    
    实际上，Object.create方法可以用下面的代码代替。
    
    ```javascript
    if(typeof Object.create!=='function'){
        Object.create = function(obj){
            function F (){};
            F.prototype = obj;
            return new F();
        }
    }
    ```
    
    上述代码表明，**Object.create**方法的实质是新建一个空的构造函数**F**，然后让F.prototype属性指向对象参数**obj**，最后返回一个**F**的实例，从而实现让该实例继承**obj**的属性
    
    下面三种方式生成的新对象是等价的。
    
    ```javascript
    var obj1 = Object.create({});
    var obj2 = Ojbect.create(Object.prototype);
    var obj3 = new Object();
    ```
    
    如果要生成一个不继承任何属性的对象，可以将**Object.create**的参数设置为**null**
    
    ```
    var obj = Object.create(null);
    ```
    
    除了对象的原型，**Object.create** 方法还可以接收第二个参数。该参数是一个属性描述对象，它所描述的对象属性，会添加到实例对象，作为该对象自身的属性。
    
    ```javascript
    var obj = Object.create({}, {
        p1: {
            value: 123,
            enumerable: true,
            configurable: true,
            writable: true
        },
        p2: {
            value: 'abc',
            enumerable: true,
            configurable: true,
            writable: true
        }
    });
    // 等同于
    var obj1 = Object.create({});
    obj1.p1 = 123;
    obj1.p2 = 'abc';
    ```
    
    **Object.create** 方法生成的对象，继承了它的原型对象的构造函数。
    
    ```javascript
    function Foo(){};
    var foo = new Foo();
    var bar = Object.create(foo);
    
    bar.constructor === Foo; // true
    bar instanceof Foo; // true
    ```
    
    ##### 3. Object.prototype.__proto__
    
    ```javascript
    var A = {
        name: 'zhangsan'
    }
    var B = {
        name: 'lisi'
    }
    var proto = {
        print: function(){
            console.log(this.name);
        }
    }
    A.__proto__ = proto;
    B.__proto__ = proto;
    
    A.print(); // zhangsan
    B.print(); // lisi
    A.print === B.print // true
    A.print === proto.print // true
    B.print === proto.print // true
    ```
    
    上面代码中，A对象和B对象的原型都是proto对象，它们都共享proto对象的print方法。也就是说，A和B的print方法，都是在调用proto对象的print方法。
    
    #### 4. Object.getOwnPropertyNames()
    
    **Object.getOwnPropertyNames** 方法返回一个数组，成员是参数对象本身的所有属性的键名，不包含继承的属性键名。
    
    ```
    Object.getOwnPropertyNames(Array)
    // ["length", "name", "prototype", "isArray", "from", "of"]
    ```
    
    上面代码中，**Object.getOwnPropertyNames** 方法返回Array所有自身的属性名。

    对象本身的属性之中，有的是可以遍历的（enumerable），有的是不可以遍历的。Object.getOwnPropertyNames方法返回所有键名，不管是否可以遍历。只获取那些可以遍历的属性，使用Object.keys方法。
    
    ```
    Object.keys(Array); // []
    ```
    上述代码表明，**Array** 对象所有自身的属性，都是不可以遍历的
    
    #### 5. Object.prototype.hasOwnProperty()
    
    对象实例的 **hasOwnProperty** 方法返回一个布尔值，用于判断某个属性定义在对象自身，还是定义在原型链上。
    
    ```
    Array.hasOwnProperty('length'); // true
    Array.hasOwnProperty('toString'); // false
    ```
    
    上面的代码表明，Array.length是Array自身的属性，Array.toString是继承的属性。
    
    另外，**hasOwnProperty** 方法是JavaScript中唯一一个处理对象属性时，不会遍历原型链的方法。
