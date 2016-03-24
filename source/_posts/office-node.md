title: 在开发机中玩转Node.js
date: 2016-03-24 19:21:00
tags: Node.js
category: 技术
---

# 在开发机中玩转Node.js


## 一、查看Node.js版本

开发机已经预装了Node.js，你可以直接在命令行里输入`node -v`查看Node.js版本。

```
$ node -v
```

## 二、命令行中执行node脚本

也可以输入`node`，然后在命令行里执行Node.js脚本

```
$ node
> console.log('hello world!') # 输入完之后回车
```

![](http://wilee.me/demo/photo/node.gif)

## 三、执行Node.js文件


你还可以在任意目录创建一个`helloworld.js`的文件：

```
console.log('hello world!');
```

然后用`node`命令执行它：

```
$ node helloworld.js
```

![](http://wilee.me/demo/photo/node_1.gif)

## 四、写一个简单的node server(服务器)

首先，创建一个`server.js`：

```
// 端口号自己写，不要与现有的端口号冲突就行
var port = '8000';

// 创建server,并输出'hello world!'
var server = require('http').createServer(function(req, res){
  res.end('hello world!');
});

// 监听刚刚定义的端口，启动server
server.listen(port);

console.log('server started at http://192.168.1.10:'+port);
```

然后，执行`node server.js`。

看到输出`server started at http://192.168.1.10:8000` 说明服务已经启动。

最后，打开浏览器访问：http://192.168.1.10:8000  , 就可以看到'hello world!'了！

![](http://wilee.me/demo/photo/node_2.gif)
