- ### 数组

    #### 1. arr.toString();
    ```
    // 将数组转换为以逗号分隔的字符串
    var arr = [1, 2, 3, 4];
    var returnedValue = arr.toString();
    console.log(arr, returnedValue);
    // 原数组 [1, 2, 3, 4 ]
    // 返回值 "1,2,3,4"
    // 可以使用此方法实现多维数组的合并
    var arr2 = [[1,2],[3,4],[5,6,[7,8]]]
    var newArr = arr2.toString().split(',');
    console.log(newArr);
    // ["1", "2", "3", "4", "5", "6", "7", "8"]
    ```
    
    #### 2. arr.join();
    ```
    // 也是讲数组转换为字符串，只是join方法接受一个作为分隔符的参数，如果没有参数，则默认是以逗号分隔
    var arr = [1,2,3,4];
    var returnedValue = arr.join();
    console.log(arr, returnedValue);
    // 原数组 [1, 2, 3, 4]
    // 返回值 "1,2,3,4"
    ```
    
    #### 3. arr.push();
    ```
    // push可以接受任意数量的参数，将参数放在原数组的尾部，该方法返回的是最终数组的长度
    var arr = [1,2,3,4];
    var returnedValue = arr.push(1);
    console.log(arr, returnedValue);
    // 原数组 [1, 2, 3, 4, 1] 
    // 返回值(数组的长度) 5
    ```
    
    #### 4. arr.unshift();
    ```
    // 用法和push()相同，只是unshift方法是将参数放入原数组的前面
    var arr = [1,2,3,4];
    var returnedValue = arr.unshift(15);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 15,1,2,3,4
    // 返回值 5
    ```
    
    #### 5. arr.pop();
    ```
    // 删除数组的最后一项，返回的是被删除的元素
    var arr = [1,2,3,4];
    var returnedValue = arr.pop();
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,2,3
    // 返回值 4
    ```
    
    #### 6. arr.shift();
    ```
    // 删除数组的第一项，返回被删除的元素
    var arr = [1,2,3,4];
    var returnedValue = arr.shift();
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 2,3,4
    // 返回值 1
    ```
    
    #### 7. arr.reverse();
    ```
    // 翻转数组的顺序
    var arr = [1,2,3,4];
    var returnedValue = arr.reverse();
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 4,3,2,1
    // 返回值 4,3,2,1
    ```
    
    #### 8. arr.sort();
    ```
    // 将数组进行排序，但需要注意的是这个方法是按Ascii码排序
    var arr = [3,1,14,5,25,6,11];
    var returnedValue = arr.sort();
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,11,14,25,3,5,6
    // 返回值 1,11,14,25,3,5,6
    var sortArr = arr.sort(function(a,b){
        return a-b;
    });
    console.log(sortArr);
    // 1,3,5,6,11,14,25
    ```
    
    #### 9. arr.concat();
    ```
    // 将数组进行合并，不会改变原数组，会返回一个合并以后的新数组
    var arr = [1,2];
    var returnedValue = arr.concat([3,4]);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 [1,2]
    // 返回值 [1,2,3,4]
    ```
    
    #### 9. arr.slice();
    ```
    // 基于当前数组，创建一个或多个项，他可以接受一个或两个参数，
    // 当参数有一个，他返回的是从参数位置到数组最后的新数组，
    // 当参数是两个，他返回的是从开始到结束的位置，但不包括最后的位置，
    // 注：可传负值，从后开始
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.slice(1);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,2,3,4,5,6
    // 返回值 2,3,4,5,6
    
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.slice(1,4);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,2,3,4,5,6
    // 返回值 2,3,4
    ```
    
    #### 10. arr.splice();
    // 这个方法可以实现数组的增删改功能
    1. 删除
    ```
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.splice(1,2);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,4,5,6
    // 返回值 2,3
    
    ```
    2. 添加
    ```
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.splice(1,0, 'tom', 'lucy');
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,tom,lucy,2,3,4,5,6
    // 返回值 
    ```
    3. 替换
    ```
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.splice(1,2, 'tom', 'lucy');
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,tom,lucy,4,5,6
    // 返回值 2,3
    ```
    
    #### 11. arr.indexOf() arr.lastIndexOf();
    ```
    // 查询元素的位置,参数为1个或2个，第一个是要查找的元素，第二是要开始查找的位置（可选的），
    // 他返回的是查找到的第一个元素的下标，indexOf()是从头开始查询，lastIndexOf()是从末尾开始查询
    var arr = [1,2,3,4,5,6];
    var returnedValue = arr.indexOf(4);
    console.log('原数组 '+arr);
    console.log('返回值 '+returnedValue);
    // 原数组 1,2,3,4,5,6
    // 返回值 3
    ```
    
- ### 字符串

    #### 1. str.charAt();
    ```
    // 返回字符串的第 n 个字符，如果不在 0~str.length-1之间，则返回一个空字符串。
    var str = 'javascript';
    console.log(str.charAt(3));
    // 'a';
    ```
    
    #### 2. str.indexOf(substr[,start]);
    ```
    //返回 substr 在字符串 str 中首次出现的位置,从 start 位置开始查找，如果不存在，则返回 -1。
    // start可以是任意整数，默认值为 0。如果 start < 0 则查找整个字符串（如同传进了 0）。如果 start >= str.length，则该方法返回 -1，
    //除非被查找的字符串是一个空字符串，此时返回 str.length.
    var str = "javascript";
    str.indexOf('s'); // 4
    str.indexOf('s',6); // -1
    str.indexOf('',11); // 10 返回str的length
    str.indexOf('',8); // 8 直接返回start
    ```
    
    #### 3. str.lastIndexOf();
    ```
    // 返回 substr 在字符串 str 中首次出现的位置,从 start 位置开始查找，如果不存在，则返回 -1。
    // start可以是任意整数，默认值为 0。如果 start < 0 则查找整个字符串（如同传进了 0）。如果 start >= str.length，则该方法返回 -1，
    // 除非被查找的字符串是一个空字符串，此时返回 str.length.
    'lastindex'.lastIndexOf('a'); // 1
    ```
    
    #### 4. str.split();
    
    #### 5. str.trim();
    ```
    // 去除 str 开头和结尾处的空白字符，返回 str 的一个副本，不影响字符串本身的值
    var str = ' abc ';
    str.trim(); // 'abc'
    console.log(str); // ' abc '
    ```
    
    #### 6. str.toLowerCase();
    ```
    var str = 'JavaScript';
    str.toLowerCase(); // 'javascript'
    console.log(str); // 'JavaScript'
    ```
    
    #### 7. str.toUpperCase();
    ```
    var str = 'JavaScript';
    str.toUpperCase(); // 'JAVASCRIPT'
    console.log(str); // 'JavaScript'
    ```
    
    #### 8. str.substring(start[, end]);
    ```
    // 返回从 start 到 end（不包括）之间的字符，start、end均为非负整数。若结束参数(end)省略，则表示从start位置一直截取到最后。
    var str = 'abcdefg';
    str.substring(1, 4); //"bcd"
    str.substring(1); // "bcdefg"
    str.substring(-1); //"abcdefg" 传入负值时会视为0
    ```
    
    #### 9. str.slice(start[, end]);
    ```
    // 用法同substring，但可传负值
    var str = 'javascript';
    str.slice(1,4); // 'ava'
    str.slice(1,-1); // 'avascrip'
    ```
    
    #### 10. str.substr(start[, length]);
    ```
    //  返回 str 中从指定位置开始到指定长度的子字符串，start可为负值
    var str = 'javascript';
    str.substr(2, 2); // 'va'
    ```
    
- ### 数字
    
    1. Number对象属性
    
        属性 | 描述
        --- | ---
        MAX_VALUE | 可表示的最大的数
        MIN_VALUE | 可表示的最小的数
        NaN | 非数字
        NEGATIVE_INFINITY | 负无穷大
        POSITIVE_INFINITY | 正无穷大
        constructor | 返回对创建此对象的 Number 函数的引用
        prototype | 原型

    2. Number.toFixed()
    ```
    // toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。
    var num = 12.37;
    console.log(num.toFixed(1)); // 12.4
    ```
    
    3. Math对象
        
        1. Math.abs(x) 返回x的绝对值
        2. Math.ceil(x) 向上取整
        3. Math.floor(x) 向下取整
        4. Math.round(x) 四舍五入取整，效果等同于x.toFixed();
        5. Math.max(x,y...n) 返回参数中最大值
        6. Math.min(x,y...n) 返回参数中最小值
        7. Math.random() 返回介于0（包含）~1（不包含）之间的一个随机数
        
        ```
        // 例：返回1-100之间的随机整数
        Math.floor(Math.random() * 100) + 1;
        // 返回0-100之间的随机整数
        Math.ceil(Math.random() * 100); // 理论上可以，但是0的概率非常非常小，故不使用这种方法
        Math.floor(Math.random() * 101);
        ```
        
        ```javascript
        var arr = [1,2,3,4,5,6]; 
        // 取出arr中最大一项
        Math.max(...arr);
        Math.max.apply(null, arr);
        ```


- ### 正则

    #### 1. 在常见的字符串检索或替换中，我们需要提供一种模式表示检索或替换的规则。正则表达式使用单个字符串来描述、匹配一系列符合某个句法规则的字符串。
    ```
    /\d\d\d/.test('123'); // true
    /\d\d\d/.test('abc'); // false
    new RegExp('reg').test('hi,reg'); // true
    RegExp('reg').test('hi,reg'); // new 可以省略
    ```
    
    #### 2. 正则基础
    符号 | 含义 | 示例
    ---|---|---
    . | 任意字符（除换行符以外：\n,\r,\u2028 or \u2029）| /.../.test('1a@');
    \d | 数字0-9 | /\d\d\d/.test('123')
    \D | 非\d，即不是数字0-9的字符 | /\D\D\D/.test('ab!');
    \w | 数字0-9，或字母a-z及A-z，或下划线的组合 | /\w\w\w\w/.test('aB8_');
    \W | 非\w | /\W\W\W/.test('@#!');
    \s | 空格符、TAB、换页符、换行符 | /\sabc/.test(' abc');
    \S | 非\s
    \t\r\n\v\f | tab 回车 换行 垂直制表符 换页符
    
    #### 3. 范围符号
    符号 | 含义 | 示例
    ---|---|---
    [...] | 字符范围 | [a-z] [0-9] [a-zA-Z0-9_]
    [^...] | 字符范围以外 | [^a-z] [^abc]
    ^ | 行首 | ^Hi
    $ | 行尾 | test$
    \b | 零宽单词边界 | \bno
    \B | 非\b
    
    #### 4. 特殊字符转义 \
    ```
    /\^abc/.test('^abc'); // true
    ```
    
    #### 5. 分组
    
    符号 | 含义 | 示例
    ---|---|---
    (x) | 分组，并记录匹配到的字符串 | /(abc)/
    \n | 表示使用分组符(x)匹配到的字符串 | /(abc)\1/.test('abcabc'); // true
    (?:abc) | 仅分组 | /(?:abc)(def)\1/.test('abcdefdef'); // true  /(abc)(?:def)\1/.test('abcdefdef'); // false
    | | | /(abc)(?:def)\1/.test('abcdefdef'); // false
    
    #### 6. 重复
    
    符号 | 含义 | 示例
    ---|---|---
    x* x+ | 重复次数>=0 重复次数>=1 贪婪算法 | abc*将匹配ab、abc、abcccc；abc+将匹配abc、abcccc；并且会匹配出现最多的一次（贪婪算法）
    x*? x+? | 同x* x+，非贪婪算法 | abc*?在字符串abcccc中将匹配ab，abc+?将匹配abc
    x? | 出现0次或1次
    x\|y | x或者y
    x{m} x{m,} x{m,n} | 重复m次 重复>=m次 重复次数x满足：n<=x<=m
    
    #### 7. 三个标志类Flag
    1. global 全局匹配，匹配所有
    2. ignoreCase 忽略大小写
    3. multiline 跨行检索或替换
    
    ```
    /abc/igm.test('AbC'); // true
    RegExp('abc', 'igm'); // true
    ```
    
    #### 8. RegExp对象属性
    ```
    /abc/g.global // true
    /abc/g.ignoreCase // false
    /abc/g.multiline // false
    /abc/g.source // 'abc'
    ```
    
    #### 9. RegExp对象方法
    1. exec
    2. test
    3. toString
    4. compile
    ```
    /abc/.exec('abcdef'); // 'abc'
    /abc/.test('abcde'); // true
    /abc/ig.toString(); // /abc/gi
    var reg = /abc/;
    reg.complie('def');
    reg.test('def'); // true
    ```
    
    #### 10. String类型与正则相关的方法
    1. String.prototype.search
    2. String.prototype.replace
    3. String.prototype.match
    4. String.prototype.split
    ```javascript
    'abcabcdef'.search(/(abc)\1/); // 0
    'aabbbbcc'.replace(/b+?/, 1); // aa1bbbcc
    'aabbbbcc'.match(/b+/); // ['bbbb']
    'aabbbbccbbaa'.match(/b+/g); // ['bbbb','bb'];
    'aabbbbccbbaa'.split(/b+/); // ['aa','cc','aa']
    ```
    
- ### Date 对象

    1. 创建Date对象的四种方式： 
        1. new Date();
        2. new Date(milliseconds);
        3. new Date(dateStr);
        4. new Date(year, month, day, hours, minutes, seconds, milliseconds);
    
    2. Date 对象属性
    
    3. Date 对象常用方法
    
        方法 | 描述 | 说明
        --- | --- | ---
        getMonth() | 返回一年中的某一个月（0-11）
        getDate() | 从Date对象返回一个月中的某一天（1-31）
        getDay() | 返回一周中的某一天（0-6） | 0代表星晴日，以此类推
        getFullYear() | 返回四位数年份
        getHours() | 返回小时数（0-23）
        getMinutes() | 返回分钟（0-59）
        getSeconds() | 返回秒数（0-59）
        getMilliseconds() | 返回毫秒数（0-999）
        getTime() | 返回 1970 年 1 月 1 日至今的毫秒数
        toDateString() | 把 Date 对象的日期部分转换为字符串 | "Wed Mar 07 2018"
        toTimeString() | 把 Date 对象的时间部分转换为字符串 | "16:37:42 GMT+0800 (中国标准时间)"
        toString() | 把 Date 对象转换为字符串 | "Wed Mar 07 2018 16:37:42 GMT+0800 (中国标准时间)"
        toLocaleDateString() | 根据本地时间格式，把 Date 对象的日期部分转换为字符串 | "2018/3/7"
        toLocaleTimeString() | 根据本地时间格式，把 Date 对象的时间部分转换为字符串 | 下午4:37:42
        toLocaleString() | 据本地时间格式，把 Date 对象转换为字符串 | "2018/3/7 下午4:37:42"
        
        
