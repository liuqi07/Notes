## node + MongoDB 分享

### <一> Nodejs

#### 一、介绍
简单的说 [Node.js](http://nodejs.cn/api/) 就是运行在服务端的 JavaScript，Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

#### 二、安装
1. 下载[Node.js](https://nodejs.org/en/download/)安装包，选择长期稳定版本下载；
2. 一路下一步进行安装，安装结束后，在命令行中输入node -v查看安装版本

#### 三、创建第一个应用
1. 引入http模块
2. 使用createServer方法创建服务器，并使用listen监听8888端口，通过req和res来接受和响应数据
3. 使用node命令来运行js文件
```
var http = require('http');

http.createServer(function (request, response) {

    // 发送 HTTP 头部 
    // HTTP 状态值: 200 : OK
    // 内容类型: text/plain
    response.writeHead(200, {'Content-Type': 'text/plain'});

    // 发送响应数据 "Hello World"
    response.end('Hello World\n');
}).listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');

```
4. Node.js 异步编程的直接体现就是回调，Node 所有 API 都支持回调函数。我们可以一边读取文件，一边执行其他操作，待文件请求回来以后，以回调函数的参数返回，这样执行代码时就没有阻塞或等待文件I/O操作，大大提高了node.js的性能，可以处理大量的并发请求。
    
- 创建一个test.txt
    ```
    云钱袋 www.yunqiandai.com
    ```
    #### 阻塞代码实例
    - 创建main.js
    ```
    var fs = require('fs');
    var data = fs.readFileSync('test.txt');
    console.log(data.toString());
    console.log('程序执行结束！');
    ```
    #### 非阻塞代码实例
    ```
    var fs = require('fs');
    var data = fs.readFile('test.txt', function(err, data){
        console.log(data.toString());
    });
    console.log('程序执行结束！');
    ```


#### 四、npm的使用
1. NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题
2. 查看版本号 npm -v
3. 国内镜像[cnpm](https://npm.taobao.org/)
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
4. 用法
```
npm install [module]
npm install express
```
安装后可直接通过require引入，无需指定路径，会自动查找node_modules文件夹
```
var express = require('express');
```
5. package.json文件

***

#### 五、[express](http://www.expressjs.com.cn/)


### <二> MongoDB

#### 1. 介绍
MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。
MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。
#### 2. 安装
1. 下载对应版本[MongoDB](https://www.mongodb.com/download-center#community)
2. 新建对应文件夹用于存储数据以及配置和日志
```
c:\MongoDB
    data\db
    conf\mongod.conf
    logs\mongod.log
```
#### 3. 启动
1. 管理员身份运行命令行
```
C:\Program Files\MongoDB\Server\3.4\bin> mongod --dbpath c:\MongoDB\data\db --logpath c:\MongoDB\logs\mongod.log 
```
2. 通过conf配置运行，编辑mongod.conf
```
#数据库路径
dbpath=c:\MongoDB\data\db
#日志输出文件路径
logpath=c:\MongoDB\logs\mongod.log
#错误日志采用追加模式，配置这个选项后mongodb的日志会追加到现有的日志文件，而不是从新创建一个新文件
logappend=true
#端口号 默认为27017
port=27017
#指定存储引擎（默认是WiredTiger，不兼容mongoVue）
storageEngine=mmapv1
#过滤无用日志信息，若需要调试请设置为false
journal=true
#端口号，默认27017
prot=27017
```
命令行运行：mongod -f c:\MongoDB\conf\mongod.conf

#### 4. MongoDB后台管理 Shell
1. 如果你需要进入MongoDB后台管理，你需要先打开mongodb装目录的下的bin目录，然后执行mongo.exe文件，MongoDB Shell是MongoDB自带的交互式Javascript shell，用来对MongoDB进行操作和管理的交互式环境。
2. 配置环境变量，全局使用mongo指令

#### 5. 基本操作
- 新建数据库
> use demo
- 查看数据库
> show dbs
- 创建集合
> db.createCollection('goods')
> db.goods.insert({id:101,name:'mi6',salePrice:2499})
- 查看集合
> show collections
- 删除数据库
> db.dropDatabase()
- 删除集合
> db.goods.drop()
- 插入文档
> db.goods.insert({id:101,name:'mi6',salePrice:2499})
- 查看集合
> db.goods.find({name:'mi6'})
> db.goods.find().skip(2).limit(2).sort({x:1})
> db.goods.find({salePrice:{$gt:1999}})
- 数据更新
> db.goods.update({name:'mi6'},{name:'hongmi'})
> db.goods.update({name:'mi6'},{$set:{name:'hongmi'}})
> db.goods.update({name:'mi6'},{$set:{name:'hongmi'},true})
> db.goods.update({name:'mi6'},{$set:{name:'hongmi'}},false,true)
- 删除数据
> db.goods.remove({name:'mi6'})
- 批量导入
> mongoimport -d demo -c goods --file

#### 6. [mongoose](http://www.nodeclass.com/api/mongoose.html)

#### 7. MongoVue
