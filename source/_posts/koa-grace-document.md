title: koa-grace中文文档
date: 2016-02-22 14:52:28
tags: fe, nodejs
---


# 1. koa-grace简介

koa-grace是基于[koa 1.x](https://github.com/koajs/koa)的新一代Nodejs多站点MVC框架。项目地址：[https://github.com/xiongwilee/koa-grace](https://github.com/xiongwilee/koa-grace)

## 1.1 特征

为什么koa-grace是新一代Nodejs MVC框架：

* 一个node服务，多个站点应用；
* yield 异步语法支持，忘掉回调噩梦；
* 继承koa中间件，扩展性更强；
* 支持`路径即路由`，更优雅的路由方式；
* RESTful数据代理支持，前后端完全解耦；
……

## 1.2 目录结构

```javascript
├── app						// 站点总目录
│   ├── blog 					// 站点：blog目录
│   │   ├── controller 				// 站点：blog的路由（控制器）目录
│   │   ├── model 					// 站点：blog的模型目录，包括公共控制器、mongo等
│   │   ├── static 					// 站点：blog的静态文件目录
│   │   └── views 					// 站点：blog的html模板目录
│   ├── reactjs-boilerplate 	// 站点：reactjs-boilerplate目录
│   └── shop 					// 站点：shop目录
├── bin						// server启动器目录
│   ├── koa-grace 				// TODO:命令行工具
│   └── server.js  				// server启动器
├── config 					// 配置文件目录
│   └── main.js					// 主配置文件
├── package.json
└── src						// 核心文件
    └── app.js					// 主文件
```

# 2. 快速开始

在开始使用koa-grace之前请确保您已经安装并运行了下面的工具:
* Nodejs (v4+)
* MongoDB (DEMO 演示使用，正式环境可以配置不用)
 
### 2.1 安装 

	$ git clone https://github.com/xiongwilee/koa-grace.git 
	$ cd koa-grace && npm install

### 2.2 配置 

在koa-grace目录下，打开配置文件:

	$ vi config/main.js

修改配置项：`config.mongo.blog` 为您的本地mongoDB的路径:

	// mongo configuration
	mongo: {
	  'blog': 'mongodb://localhost:27017/blog'
	}

**更多关于配置项的文档可以看下面的使用文档。

### 2.3 运行

在koa-grace目录下执行，可能需要root权限：	

	$ npm run dev

然后访问  [http://127.0.0.1:3000](http://127.0.0.1:3000/home)  ，就可以看到koa-grace其中的一个案例站点了！

您也可以访问koa-grace的一个线上应用： http://mlsfe.biz 。

# 3. 详细使用文档

虽说koa-grace是一个完整的MVC框架 ， 但其本质是基于一种多站点解决方案的koa中间件的集合。其核心中间件包括但不仅限于： [koa-router](https://github.com/alexmingoia/koa-router) , [koa-views](https://github.com/queckezz/koa-views) , [koa-mount](https://github.com/koajs/mount) , [koa-static](https://github.com/koajs/static/) , [koa-grace-vhost](https://github.com/xiongwilee/koa-grace-vhost) , [koa-grace-router](https://github.com/xiongwilee/koa-grace-router) , [koa-grace-proxy](https://github.com/xiongwilee/koa-grace-proxy) , [koa-grace-model](https://github.com/xiongwilee/koa-grace-model) , [koa-grace-mongo](https://github.com/xiongwilee/koa-grace-mongo) , ...

## 3.1 多站点配置 - Vhost

koa-grace是基于 [koa-grace-vhost](https://github.com/xiongwilee/koa-grace-vhost) 进行vhost管理，基本原理是：

> 一个域名对应一个应用，一个应用对应一个目录

如此一来，配置多站点就很简单了，在配置文件`config/main.js`中：

```javascript
// vhost配置
vhost: {
  'test.mlsfe.biz':'blog',
  '127.0.0.1':'blog',
  'localhost':'shop',
  '0.0.0.0':'reactjs-boilerplate'
}
```

其中，vhost配置中`127.0.0.1`是URI的`hostname`, `blog`是站点总目录app下的一个目录`app/blog`。如果当前请求URI为：http://127.0.0.1/home 则koa-grace会自动访问`app/blog`目录里的路由、模型、静态文件。

需要说明的是，**多站点配置仅以URI的hostname为主键** ；也就是说，访问带端口号的http://127.0.0.1:3000/home 也会定位到app/blog目录。

## 3.2 路由及控制器 - Router&Controller

很好，如果你配置好了一个vhost为`'127.0.0.1':'blog'` , koa-grace就会自动生成一个vhost到`app/blog`目录了！接下来，进入`app/blog/controller`目录进行路由配置。

koa-grace基于 [koa-grace-router](https://github.com/xiongwilee/koa-grace-router) 进行路由管理的，koa-grace-router又是依赖于：[koa-router](https://github.com/alexmingoia/koa-router) 。

### 3.2.1 文件路径即路由

以`blog`站点为例，`koa-grace-router`会找到 `app/blog/*` 目录下的所有`.js`后缀的文件，并以文件路径生成路由。我们再看一下案例中`blog`的路由文件：

```
├── api
│   └── post.js
├── dashboard
│   ├── post.js
│   ├── site.js
│   ├── user.js
│   └── userAuthor.js
├── error.js
├── home.js
├── post.js
└── user.js
```

如果当前请求URI为：http://127.0.0.1/dashboard/post/* 则路由将自动落在`dashboard/post.js`文件中。

那么，如果请求路径如果是http://127.0.0.1/dashboard/post/list ，这个`dashboard/post.js`文件是如何控制的呢？

### 3.2.2 路由文件详细说明

打开`app/blog/controller/dashboard/post.js`文件：

```javascript
/*...*/
exports.list = function* () {
  // 绑定默认控制器
  yield this.bindDefault();
  // 独立权限控制
  if (!userAuthor.checkAuth(this, this.userInfo)) {return};
  
  // 获取请求query参数
  let pageNum = this.query.page;
  // 获取数据
  let PostModel = this.mongo('Post');
  let posts = yield PostModel.page(pageNum,20);
  let page = yield PostModel.count(pageNum,20);

  // 渲染模板
  yield this.render('dashboard/post_list',{
    breads : ['文章管理','文章列表'],
    posts:posts,
    page:page,
    userInfo: this.userInfo,
    siteInfo: this.siteInfo
  })
}
exports.list.__method__ = 'get';
exports.list.__regular__ = null;
/*...*/
```

对，就是你猜的那样：koa-grace-router是通过post.js的module.exports进行下一步的路由控制。

另外，需要说明以下几点：

* 如果需要配置dashboard/post/list请求为`POST`方法，则post.js中声明 `exports.list.__method__ = 'post'`即可（不声明默认为get请求），更多方法类型请参看：[koa-router#routergetputpostpatchdelete--router](https://github.com/alexmingoia/koa-router#routergetputpostpatchdelete--router);
* 如果要进一步配置dashboard/post/list/id路由，则在post.js中声明`exports.list.__regular__ = '/:id';`即可，更多相关配置请参看：[koa-router#named-routes](https://github.com/alexmingoia/koa-router#named-routes)
* 如果当前文件路由就是一个独立的控制器，则`module.exports`返回一个yield方法即可，可以参考案例`blog`中的`controll/home.js`
* 如果当前文件仅仅是一个依赖，仅仅被其他文件引用；则在文件中配置`exports.__controller__ = false`，该文件就不会生成路由了

当然，如果一个路由文件中的控制器方法都是post方法，您可以在控制器文件最底部加入：`module.exports.__method__ = 'post'`即可。`__regular__`的配置同理。

### 3.2.3 控制器

刚刚我们看到了post.js中的exports.list方法，事实上它就是一个控制器（controller）了。

您可以新建一个`app/blog/controller/hello.js`文件

```javascript
exports.koagrace = funtion* (){
	this.body = 'hello koa-grace！';
}
```

访问 http://127.0.0.1/hello/koagrace ，就可以看到“hello koa-grace！”输出。它是典型的一个基于上下文（context）的yield方法。几个关键方法/参数使用如下：

context属性 | 类型 | 说明
---------- | ---- | ------------------
`this.query` | `object` | get参数
`this.request.body` | `object` | post参数，由于koa-grace默认引入了[koa-bodypaser](https://github.com/koajs/body-parser)，您可以直接在this.request.body中获取到post参数
`this.bindDefault` | `function` | 公共控制器，相当于`require('app/blog/model/defaultCtrl.js')`
`this.render` | `function` | 模板引擎渲染方法，请参看：3.5 模板引擎- Template engine
`this.mongo` | `function` | 数据库操作方法，请参看：3.3 数据库 - Database
`this.mongoMap` | `function` | 并行数据库多操作方法，请参看：3.3 数据库 - Database
`this.proxy` | `function` | RESTful数据请求方法，请参看：3.4.1 数据代理
`this.download` | `function` | 文件请求代理方法，请参看：3.4.2 请求代理
`this.upload` | `function` | 文件上传方法，请参看： 3.4.3 文件上传

更多context文档请参看[koa官网](http://koajs.com)，或[http://koajs.in/doc/](http://koajs.in/doc/)

## 3.3 数据库 - Database

koa-grace引入基于[mongoose](mongoosejs.com)的[koa-grace-mongo](https://github.com/xiongwilee/koa-grace-mongo) ，可以非常便捷地使用mongoDB。

### 3.3.1 连接数据库

在配置文件`config/main.js`中进行配置：

```javascript
  // mongo配置
  mongo: {
    options:{
      // mongoose 配置
    },
    api:{
      'blog': 'mongodb://localhost:27017/blog'
    }
  },
```

其中，`mongo.options`配置mongo连接池等信息，`mongo.api`配置站点对应的数据库连接路径。

值得注意的是，**配置好数据库之后，一旦koa-grace server启动mongoose就启动连接，直到koa-grace server关闭**

### 3.3.2 mongoose的schema配置

依旧以案例`blog`为例，参看`app/blog/model/mongo`目录：

```
└── mongo
    ├── Category.js
    ├── Link.js
    ├── Post.js
    └── User.js
```

一个js文件即一个数据库表即相关配置，以`app/blog/model/mongo/Category.js`：

```javascript
'use strict';

// model名称，即表名
let model = 'Category';

// 表结构
let schema = [{
  id: {type: String,unique: true,required: true},
  name: {type: String,required: true},
  numb: {type: Number,'default':0}
}, {
  autoIndex: true,
  versionKey: false
}];

// 静态方法:http://mongoosejs.com/docs/guide.html#statics
let statics = {}

// 方法扩展 http://mongoosejs.com/docs/guide.html#methods
let methods = {
  /**
   * 获取博客分类列表
   */
  list: function* () {
    return this.model('Category').find();
  }
}

module.exports.model = model;
module.exports.schema = schema;
module.exports.statics = statics;
module.exports.methods = methods;
```

主要有四个参数：
* `model` ， 即表名，最好与当前文件同名
*  `schema` ， 即mongoose schema
*  `methods` ， 即schema扩展方法，**推荐把数据库元操作都定义在这个对象中**
*  `statics` ， 即静态操作方法

### 3.3.3 在控制器中调用数据库

在控制器中使用非常简单，主要通过`this.mongo`,`this.mongoMap`两个方法。

#### 1） `this.mongo(name)` 

调用mongoose Entity对象进行数据库CURD操作

**参数说明:**

`@param [string] name` : 在`app/blog/model/mongo`中配置Schema名，

**返回:**

`@return [object]` 一个实例化Schema之后的Mongoose Entity对象，可以通过调用该对象的methods进行数据库操作

**案例**

参考上文中的Category.js的配置，以`app/blog/controller/dashboard/post.js`为例，如果要在博客列表页中获取博客分类数据：

```javascript
// http://127.0.0.1/dashboard/post/list
exports.list = function* (){
	let cates = yield this.mongo('Category').list();
	this.body = cates;
}
```

#### 2）`this.mongoMap(option)`

并行多个数据库操作

**参数说明**

`@param [array] option` 

`@param [Object] option[].model`  mongoose Entity对象，通过this.mongo(model)获取

`@param [function] option[].fun`  mongoose Entity对象方法

`@param [array] option[].arg`  mongoose Entity对象方法参数

**返回**

`@return [array]` 数据库操作结果，以对应数组的形式返回

**案例**

```javascript
  let PostModel = this.mongo('Post');
  let mongoResult = yield this.mongoMap([{
      model: PostModel,
      fun: PostModel.page,
      arg: [pageNum]
    },{
      model: PostModel,
      fun:PostModel.count,
      arg: [pageNum]
    }]);

  let posts = mongoResult[0];// 获取第一个查询PostModel.page的结果
  let page = mongoResult[1]; // 获取第二个查询PostModel.count的结果，两者并发执行
```

## 3.4 代理 - Proxy

除了在控制器中直接进行数据库操作，Web应用还有可能由其他服务进行后端部署。针对这种场景，koa-grace引入了基于 [Request](https://github.com/request/request) 的 [koa-grace-proxy](https://github.com/xiongwilee/koa-grace-proxy)。

### 3.4.1 数据代理

在koa-grace的控制器中使用`this.proxy`方法进行数据代理非常简单：

```javascript
exports.list = function* (){
	yield this.proxy({
		userInfo:'github:post:user/login/oauth/access_token?client_id=****',
		otherInfo:'github:other/info?test=test',
	});
	
	console.log(this.backData);
	/**
	 *	{
	 *		userInfo : {...},
	 *		otherInfo : {...}
	 *	}
	 */
}
```

你也可以不传`this.backData`参数，默认注入到上下文的`this.backData`对象中：

```javascript
exports.list = function* (){
	yield this.proxy({
		userInfo:'github:post:user/login/oauth/access_token?client_id=****',
		otherInfo:'github:other/info?test=test',
	});
	
	console.log(this.backData);
	/**
	 *	{
	 *		userInfo : {...},
	 *		otherInfo : {...}
	 *	}
	 */
}
```
另外，`github:post:user/login/oauth/access_token?client_id=****`说明如下：
* `github`： 为在`config.main.js`的 `api` 对象中进行配置；
* `post` ： 为数据代理请求的请求方法，该参数可以不传，默认为`get`
* `path`： 后面请求路径中的query参数会覆盖当前页面的请求参数（this.query），将query一同传到请求的接口
* 你也可以写完整的路径：`{userInfo:'https://api.github.com/user/login?test=test'}`

### 3.4.2 文件代理

文件请求代理也很简单，比如如果需要从github代理一个图片请求返回到浏览器中，参考：http://mlsfe.biz/user/avatar?img=https://avatars.githubusercontent.com/u/1962352?v=3

```javascript
exports.avatar = function* (){
	let imgUrl = query.img;
    yield this.download(imgUrl);
}
```

### 3.4.3 文件上传

TODO: 文件上传并代理到其他服务或者存储到本地

## 3.5 模板引擎- Template engine

koa-grace引入[koa-views](https://github.com/queckezz/koa-views)  ， 进行模板引擎管理。默认的模板引擎为[swig](paularmstrong.github.io/swig/)， 您可以在`config/main.js`中配置`template`属性您想要模板引擎：

```javascript
  // 模板引擎配置
  template: 'swig'
```

目前支持的模板引擎列表在这里：[consolidate.js#supported-template-engines](https://github.com/tj/consolidate.js#supported-template-engines)

在控制器中调用`this.render`方法渲染模板引擎：

```javascript
exports.home = function* () {
  yield this.bindDefault();

  yield this.render('dashboard/site_home',{
    breads : ['站点管理','通用'],
    userInfo: this.userInfo,
    siteInfo: this.siteInfo
  })
}
```

模板文件在`app/blog/views`目录中。

## 3.6 静态文件服务 - Static server

koa-grace引入[koa-mount](https://github.com/koajs/mount)  及  [koa-static](https://github.com/koajs/static/)，将静态文件代理到`/static`：

```javascript
  // 配置静态文件路由
  vapp.use(mount('/static',
    koastatic(appPath + '/static')
  ));
```

以案例中`blog`的静态文件为例，静态文件在blog项目下的路径为：`app/blog/static/image/bg.jpg`，则访问路径为http://127.0.0.1/static/image/bg.jpg。

## 3.7 启动服务及调试 - Process & DEBUG

### 3.7.1 开发环境

在开发环境可以使用npm命令完成。

1) 普通启动：	

	$ npm run start

2) watch启动：

	$ npm run dev
	# 在80端口启动
	$ npm PORT=80 run dev
	# DEBUG模式启动，默认为DEBUG=koa-grace*
	$ npm DEBUG=* run dev 

### 3.7.2 生产环境

在生产环境推荐使用 [pm2](https://github.com/Unitech/pm2) 进行进程管理：

	$ npm install pm2 -g
	$ pm2 start node ./bin/server.js

更多使用方法，请参看 [pm2](https://github.com/Unitech/pm2)。

# 4. 贡献

* 提ISSUE： https://github.com/xiongwilee/koa-grace/issues 
* 欢迎提PR
* 给作者提问&提建议：[xiongwilee@foxmail.com](xiongwilee@foxmail.com) 
