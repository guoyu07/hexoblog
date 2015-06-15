title: web前端之原生DOM&jQuery-DOM编程讲稿【清华大学】
date: 2015-06-10 11:50:00
type: slider
description: 清华大学web前端之原生DOM&jQuery-DOM编程讲稿
---
# WEB前端开发

### —— 原生DOM&jQuery-DOM编程

<div style="height:80px;"></div>

---

<div style="height:120px;">
    <img src="/image/post/tsinghua_web_frontend_slider/tsinghua.png" style="margin:0px;border:none;background:#eee8d5;height:30px;padding:10px;border-radius:5px;">
    <img src="/image/mls_logo.png" style="margin:0px;border:none;background:#eee8d5;height:30px;padding:10px;border-radius:5px;margin-left:10px;">
</div>

美丽说商业前端负责人&emsp;熊伟烈

<a href="http://weibo.com/wileexiong" target="_blank"><i class="fa fa-weibo"></i> <span>-wilee-</span></a><span>&emsp;|&emsp;</span><a href="http://wilee.me" target="_blank"><i class="fa fa-home"></i> <span>http://wilee.me</span></a>&emsp;|&emsp;</span><a href="/image/weixin.jpg" target="_blank"><i class="fa fa-weixin"></i> <span>xiongwilee</span></a>


<center>![/image/post/tsinghua_web_frontend_slider/slider.png](/image/post/tsinghua_web_frontend_slider/slider.png)</center>




## 课程大纲

### 第一章：DOM基础
#### 1.1 认识DOM
#### 1.2 DOM节点
#### 1.3 DOM节点的查改增删
#### 1.4 DOM相关的几个重要对象
#### 1.5 实例分析

### 第二章：原生DOM事件模型
#### 2.1 事件的分类
#### 2.2 添加事件处理程序
#### 2.3 移除事件处理程序
#### 2.4 深入Event
#### 2.5 实例分析


## 第三章：基于jQuery的DOM编程
#### 3.1 万能的$
#### 3.2 jQuery选择器
#### 3.3 DOM节点的增加与移除
#### 3.4 DOM属性与CSS
#### 3.5 jQuery事件处理
#### 3.6 jQuery动画

## 第四章：利用Chrome DevTool进行DOM调试


## 第五章：有趣的webAPP：微信及手机活动页的开发

## 随堂综合练习

## Q/A时间



## 第一章：DOM基础

### 1.1 认识DOM
### 1.2 DOM节点
### 1.3 DOM节点的查改增删
### 1.4 DOM相关的几个重要对象
### 1.5 实例分析



## 一、认识DOM

### 1.1.1 DOM是什么？

Document Object Model，文档对象模型，可以以一种独立于平台和语言的方式访问和修改一个文档的内容和结构，是表示和处理一个HTML或XML文档的常用方法。

### 1.1.2 DOM能做什么？

能让网页实现更丰富的交互效果，下面随便列几个案例看欣赏一下DOM的奇幻魅力：

* 纸飞机： [/demo/plane_move.html](/demo/plane_move.html)
* 标准时间比例的太阳系：[/demo/solar.html](/demo/solar.html) (来自:[codepen.io](http://codepen.io/kowlor/pen/ZYYQoy))
* 浏览器插件：[Hi一下！](/demo/hi.html)



## 二、DOM节点

### 1.2.1 DOM中对节点的定义

** HTML/XML文档中的所有内容都是节点 **，例如：

* 整个文档是一个文档节点

* 每个 HTML 标签是一个元素节点

* 包含在 HTML 元素中的文本是文本节点

* 每一个 HTML 属性是一个属性节点

* 注释属于注释节点


### 1.2.2 节点类型

常见的DOM节点类型

|元素名称|节点类型|节点值|
|--|--|--|
|元素|Node.ELEMENT_NODE|1|
|属性|Node.ATTRIBUTE_NODE|2|
|文本|Node.TEXT_NODE|3|
|注释|Node.COMMENT_NODE|8|
|文档|Node.DOCUMENT_NODE|9|

[案例分析](/demo/tsinghua_web_frontend_slider_1.html)


### 1.2.3 节点层次

#### 1.2.3.1 HTML文档

```HTML
<!DOCTYPE HTML>
<html lang="en-US">
    <head>
        <meta charset="UTF-8">
        <title>文档标题</title>
    </head>
    <body>
        <h1>我的标题</h1>
        <a href="http://www.baidu.com">我的链接</a>
    </body>
</html>
```

#### 1.2.3.2 DOM树

![/image/post/tsinghua_web_frontend_slider/dom-tree.gif](/image/post/tsinghua_web_frontend_slider/dom-tree.gif)



## 三、DOM节点的查改增删

本节将主要学习HTML DOM节点的查找、修改、创建与插入、删除等操作。

### 1.3.1 节点查询

#### 1.3.1.1 查询DOM节点

简要介绍getElementById、getElementsByTagName、getElementsByClassName，示例代码：

```JavaScrpt
// 查询id为 helloWorld 的节点
var helloWorld = document.getElementById('helloWorld');
 
// 查询页面上的所有 a 标签
var aTags = document.getElementsByTagName('a');
 
// 查询class为 .slide 的节点
var slides = document.getElementsByClassName('slide');

```

感兴趣的可以再试试：querySelector、querySelectorAll

[案例分析](/demo/tsinghua_web_frontend_slider_2.html)


#### 1.3.1.2 访问父节点与子节点

简要介绍parentNode、childNodes、firstChild、lastChild，示例代码：

```JavaScrpt
// 查询id为 helloWorld 的节点
var helloWorld = document.getElementById('helloWorld');
 
// 获得helloWorld的父节点
// 这里使用的是parentNode，在非w3c标准下还有一个parentElement，必须理解二者的区别：
// ElementNode只是Node中的一种，nodeType为1
var parentNodeForHelloWorld = helloWorld.parentNode;
 
// 获得helloWorld的所有子节点
var childNodesForHelloWorld = helloWorld.childNodes;
 
// 获取hellWorld的第一个子节点
var firstChildForHelloWorld = helloWorld.firstChild;
 
// 获取hellWorld的最后一个子节点
var lastChildForHelloWorld = helloWorld.lastChild;
```

** firstChild和lastChild都是获取所有类型的Node，而不仅仅是ElementNode。 **

[案例分析](/demo/tsinghua_web_frontend_slider_3.html)


#### 1.3.1.3 访问兄弟节点

简要介绍previousSibling、nextSibling，示例代码:

```JavaScrpt
// 查询id为 helloWorld 的节点
var helloWorld = document.getElementById('helloWorld');
 
// 获得helloWorld的前一个兄弟节点
var previousNodeForHelloWorld = helloWorld.previousSibling;
 
// 获得helloWorld的后一个兄弟子节点
var nextNodeForHelloWorld = helloWorld.nextSibling;
```

** previousSibling和nextSibling都是获取所有类型的Node，而不仅仅是ElementNode。 **

如果只想获取ElementNode，可以使用previousElementSibling和nextElementSilbling方法， 但这两个属性不是w3c标准，存在浏览器兼容性问题，慎用。

[案例分析](/demo/tsinghua_web_frontend_slider_4.html)


### 1.3.2 节点修改

#### 1.3.2.1 修改节点属性

节点属性的修改，可以通过element.setAttribute、element.attributeName的方式进行修改，比如针对如下节点：

```HTML
<a id="helloWorld" class="cls-demo red" href="http://www.baidu.com">http://www.baidu.com</a>
```

可通过下面的两种方式，直接修改该节点的链接地址：href属性

```JavaScript
// 查询id为 helloWorld 的A节点
var helloWorld = document.getElementById('helloWorld');
 
// 修改helloWorld的href值：通过element.setAttribute的形式
helloWorld.setAttribute('href','http://www.baidu.com');
 
// 修改helloWorld的href值：通过element.attributeName的形式
helloWorld.href = 'http://www.baidu.com';
```

[案例分析](/demo/tsinghua_web_frontend_slider_5.html)


关于节点CSS class的访问，在HTML5标准中新增了classList API，该API中新增了CSS class的add、remove、contains、item、toggle等方法

```JavaScript
// 通过classList的contains方法，判断节点是否包含某个CSS class
var hasClass = helloWorld.classList.contains('red'); // true
// 其他API可线下单独尝试
```


#### 1.3.2.2 修改节点内容

本小节主要介绍节点内容的修改方法，包括修改HTML片段，以及文本内容。主要API为：innerHTML、innerText

```JavaScript
// 继续以上一小节的<a>节点作为示例
var helloWorld = document.getElementById('helloWorld');
 
// 修改链接文本为：清华大学
helloWorld.innerHTML = '清华大学';
// 或通过innerText属性修改
helloWorld.innerText = '清华大学';
 
// 将链接文本替换成一张图片，即插入一个<img/>标签，此时只能使用innerHTML属性
helloWorld.innerHTML = '<img src="static/img/picture.png" alt="图片"/>';
```

*   通过innerHTML属性，可以向节点中插入任意HTML片段，必须明白，不是所有标签都支持innerHTML属性

*   通过innerText属性，只能向节点内插入文本，并且不是w3c标准，所以存在浏览器兼容性问题， 比如在Firefox、Chrome等浏览器中，则是通过 textContent 来实现：

    ```JavaScript
    // 标准浏览器下，通过 textContent 来修改文本内容
    helloWorld.textContent = '清华大学';
    ```

[案例分析](/demo/tsinghua_web_frontend_slider_6.html)


#### 1.3.2.3 增加新节点

本节将介绍如何通过DOM动态创建新节点，并插入到文档中，用到的API：createElement、appendChild，假定文档如下：

```HTML
<div id="helloWorld">
    <div id="inner"></div>
</div>
```

此时则可以通过如下的DOM操作，动态创建一个img节点并插入到helloWorld中

```JavaScript
// 获得helloWorld节点
var helloWorld = docuement.getElementById('helloWorld');
 
// 通过createElement创建img节点，并设置相关属性
var imgElement = document.createElement('img'); // 注意API的使用方法
imgElement.src = '/static/img/picture.png'; // 设置图片地址
imgElement.alt = '图片';
 
// 将img追加到helloWorld子节点之后
helloWorld.appendChild(imgElement); // 采用子节点追加的方式插入文档
```

** 当有大批量的DOM节点需要插入到文档流中，需要用DocumentFragment来实现 **

[案例分析](/demo/tsinghua_web_frontend_slider_7.html)


通过上面的DOM操作，文档片段将发生如下的变化：

```HTML
<div id="helloWorld">
    <div id="inner"></div>
    <img src="/static/img/picture.png" alt="图片"/>
</div>
```

除了通过createElement创建ElementNode之外，还可以通过document.createTextNode创建TextNode
在节点的动态插入方面，除了使用appendChild之外，还可以通过element.insertBefore方法将节点插入到指定节点之前， 通过element.insertAjdacentElement方法在指定节点的指定位置处进行插入。

列举一个简易的DocumentFragment示例：

```JavaScript
// 创建一个文档碎片
var docFrag = document.createDocumentFragment();
// 在碎片上加入100个div节点
for(var i = 0;i < 100;i++){
    docFrag.appendChild(document.createElement('div'));
}
// 加docFrag加入到DOM-Tree
document.body.appendChild(docFrag);
```

** 在项目开发中，用得最多的还是createElement、appendChild，其他API一般都会进行封装后再使用，可留作课后作业自行练习。 **


#### 1.3.2.4 删除节点

本节将简单介绍从文档中将DOM节点进行删除操作，主要通过父节点的removeChild方法来实现。已如下HTML文档为例：

```HTML
<div id="container">
    <div id="helloWorld"></div>
</div>
```

现在通过下面的DOM操作，来实现hellWorld节点的删除操作

```JavaScript
// 获得待删除的节点
var helloWorld = document.getElementById('helloWorld');
 
// 调用父节点的removeChild方法来实现自身节点的删除
helloWorld.parentNode.removeChild(helloWorld); // 注意参数
```

如上代码执行成功后，文档将会发生如下变化：

```HTML
<div id="container"></div>
```

注：目前部分高大上一点的浏览器（如Chrome）已经支持element.remove()直接移除节点本身：

```JavaScript
document.getElementById('helloWorld').remove();
```

[实例分析](/demo/tsinghua_web_frontend_slider_8.html)



## 四、DOM相关的几个重要对象

关于DOM操作，浏览器提供了较多内置对象，具体可以从下面文档中得到参考：

[http://www.w3school.com.cn/htmldom/htmldom_reference.asp](http://www.w3school.com.cn/htmldom/htmldom_reference.asp)

但是本节只简单介绍几个比较典型的对象。

### 1.4.1 window对象

window对象是BOM的核心，扮演着Global对象的角色。

包括了整个WEB页面中所有可执行的JavaScript API；另外，可详细了解alert()、confirm()、prompt()、open()、close()、onload()

### 1.4.2 document对象

DOM编程中，最常用的对象，可详细了解cookie、title、URL、write()、getElementById()


### 1.4.3 navigator对象

通过此对象可以获取操作系统信息、浏览器信息等，在HTML5中，还可以获取地理位置、联网状态等； 可详细了解platform、userAgent、geolocation、onLine

### 1.4.4 location对象

包含当前页面URL相关的信息，并能控制页面的跳转等操作，可详细了解href、hash、search、protocal、reload()、replace()； 另外，location.href值等同于document.URL



## 五、实例分析

1. 纸飞机： [/demo/plane_move.html](/demo/plane_move.html)
1. 标准时间比例的太阳系：[/demo/solar.html](/demo/solar.html)
1. 浏览器插件：[Hi一下！](/demo/hi.html)

用截止目前讲到的DOM操作，分析一下上面实例的实现原理。



## 第二章：原生DOM事件模型

### 2.1 事件的分类

### 2.2 添加事件处理程序

### 2.3 移除事件处理程序

### 2.4 深入Event

### 2.5 实例分析



## 一、事件的分类

1. ** 鼠标事件 **: click、dbclick、mousedown、mouseup、mouseover、mousemove、mouseout等

1. ** 键盘事件 **: kyedown、keyup、keypress等

1. ** 表单事件 **: select、change、submit、focus、blur等

1. ** 媒介事件 **: play、playing、abort、cancel等

1. ** HTML5事件 **: online、offline、message、popstate等

1. ** 页面事件 **: load、error、resize、scroll等

1. ** WebApp事件 **: orientationchange、touchstart、touchmove、touchend等



## 二、添加事件处理程序

给DOM节点增加事件处理程序也有多种方法，本节都将进行简单介绍

### 2.2.1 通过节点属性显式声明

如下示例代码，表示直接在HTML中，显式地为按钮绑定了click事件，当该按钮有用户点击行为时，便会触发myClickFunc方法

```HTML
<button id="btnHello" onclick="myClickFunc()">ClickMe</button>
```

myClickFunc的定义则在js中完成，示例如下：

```JavaScript
// 事件处理程序的定义
var myClickFunc = function(evt){
    // TODO ...
};
```

[实例分析](/demo/tsinghua_web_frontend_slider_9.html)


### 2.2.2 通过节点属性动态绑定
这种事件处理程序的绑定，属于第一种的变种形式

```HTML
<button id="btnHello">ClickMe</button>
```

通过DOM操作进行动态绑定：

```JavaScript
// 事件处理程序的定义
var myClickFunc = function(evt){
    // TODO ...
};
 
// 直接给DOM节点的 onclick 方法赋值，注意这里接收的是一个function
document.getElementById('btnHello').onclick = myClickFunc;
```

[实例分析](/demo/tsinghua_web_frontend_slider_10.html)


### 2.2.3 通过事件监听的方式

相比而言，是事件处理程序的升级模式，是最靠谱的绑定方式，并且能给DOM节点增加多个事件监听，但不能绑定多个onclick事件

```HTML
<button id="btnHello">ClickMe</button>
```

通过DOM操作进行动态绑定：

```JavaScript
// 获取btnHello节点
var btnHello = document.getElementById('btnHello');
 
// 增加第一个 click 事件监听处理程序
btnHello.addEventListener('click',function(evt){
    // TODO sth 1...
},false);
 
// 增加第二个 click 事件监听处理程序
btnHello.addEventListener('click',function(evt){
    // TODO sth 2...
},false);
```

** 通过此种形式，可以给btnHello按钮绑定任意多个click监听； 注意，执行顺序与添加顺序相关 **

[实例分析](/demo/tsinghua_web_frontend_slider_11.html)



## 三、移除事件处理程序

移除的方法必须和添加的方法相对应

*   如果事件是通过onclick的方式来绑定的，要删除该处理程序，可重新给onclick赋值即可，示例如下：

    ```JavaScript
    document.getElementById('btnHello').onclick = function(){}; // 空function即可
    ```

*   如果事件是通过addEventListener监听方式绑定的，要删除处理程序，需要用removeEventListener进行解绑，示例如下：

    ```JavaScript
    // 获取btnHello节点
    var btnHello = document.getElementById('btnHello');
     
    // 定义监听处理程序
    var myClickFunc1 = function(evt){
        // TODO ...
    };
    // 增加事件监听
    btnHello.addEventListener('click',myClickFunc1,false); // 指定句柄
     
    // 移除事件监听
    btnHello.removeEventListener('click',myClickFunc1,false); // 指定句柄
    ```
[实例分析](/demo/tsinghua_web_frontend_slider_12.html)



## 四、深入Event对象

Event 对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。 事件通常与函数结合使用，函数不会在事件发生前被执行！

### 2.4.1 Event对象的一些重要属性和方法

*   键盘的相关状态

    altKey（Alt键是否被按下）、ctrlKey（Ctrl键是否被按下）、metaKey（Meta键是否被按下）、 shiftKey（Shift键是否被按下）、keyCode/which（可通过键盘码判断出具体是那个键被按下）

*   鼠标的相关状态

    button（判断是那个键被按下：左键、右键、中键）、clientX/clienY/screenX/screenY/offsetX/offsetY/x/y （获取事件触发时鼠标的具体位置）

*   其他标准属性与方法
    
    type、target、timeStamp、bubbles、cancelable、currentTarget、preventDefault()、stopPropagation()


### 2.4.2 事件冒泡（传播）

事件触发时，会从目标DOM元素向上传播，直到文档根节点，一般情况下，会是如下形式传播：

    targetDOM → parentNode → ... → body → document → window

如果希望一次事件触发能在整个DOM树上都得到响应，那么就需要用到事件冒泡的机制，如下示例代码：

```HTML
<button id="btnHello">ClickMe</button>
```

```JavaScript
// 给按钮增加click监听
document.getElementById('btnHello').addEventListener('click',function(evt){
    alert('button clicked');
},false);
 
// 给body增加click监听
document.body.addEventListener('click',function(evt){
    alert('body clicked');
},false);
```

在这种情况下，点击按钮“ClickMe”后，其自身的click事件会被触发，同时，该事件将会继续向上传播， 所有的祖先节点都将得到事件的触发命令，并立即触发自己的click事件；所以如上代码，将会连续弹出两个alert

[实例分析](/demo/tsinghua_web_frontend_slider_13.html)


有些情况下，我们的需求要求，每个事件都是独立触发，所以我们必须阻止事件冒泡，针对如上示例代码，可改造为：

```JavaScript
// 给按钮增加click监听
document.getElementById('btnHello').addEventListener('click',function(evt){
    alert('button clicked');
    evt.stopPropagation(); // 这条命令就能将此次事件完全结束掉，阻止冒泡
},false);
 
// 给body增加click监听
document.body.addEventListener('click',function(evt){
    alert('body clicked');
},false);
```

此时，点击按钮后，只会触发按钮本身的click事件，得到一个alert效果；该按钮的点击事件，不会向上传播，body节点就接收不到此次事件命令。

有两点需要注意：

*   不是所有的事件都能冒泡，如：blur、focus、load、unload都不能

*   不同的浏览器，阻止冒泡的方式也不一样，在w3c标准中，通过event.stopPropagation()完成， 在IE中则是通过自身的event.cancelBubble=true来完成

[实例分析](/demo/tsinghua_web_frontend_slider_14.html)


### 2.4.3 事件默认行为

在项目过程中，我们会遇到各种各样的需求，比如：

*   点击form表单中的submit按钮后，表单不允许提交
*   点击a标签后，不允许发送页面跳转
*   对键盘进行控制，禁止输入

其实，这些需求都可以通过阻止事件的默认行为来完成，具体可以看下面的这个示例：

```HTML
<a id="linkToBaidu" href="http://www.baidu.com">Baidu</a>
```

要求：点击Baidu链接后，页面不能发生跳转，而是弹出一个alert

```JavaScript
// 给a标签增加click事件监听
document.getElementById('linkToBaidu').addEventListener('click',function(evt){
    alert('对不起，页面不会发生跳转！');
    evt.preventDefault(); // 阻止默认行为
},false);
```

BTW：其他情况均可通过这样的方式进行事件默认行为的阻止，至于阻止的方法，在不同浏览器中会存在差异，后续章节将会介绍兼容性的处理办法

[实例分析](/demo/tsinghua_web_frontend_slider_15.html)



### 五、实例分析

1. memory：http://wilee.me/demo/memory.html (来自:[codepen.io](http://codepen.io/natewiley/pen/HBrbL))

1. Flappy Dragon：http://js1k.com/2014-dragons/demo/1659

1. 2048：http://js1k.com/2014-dragons/demo/1824

用截止目前学到的DOM操作 & 事件模型 知识，分析如上实例的实现原理



## 第三章：基于jQuery的DOM编程

### 3.1 万能的$

### 3.2 jQuery选择器

### 3.3 DOM节点的增加与移除

### 3.4 DOM属性与CSS

### 3.5 jQuery事件处理

### 3.6 jQuery动画



## 一、万能的$

$符是jQuery的一个别名，通过它，能完成非常丰富的DOM操作，比如拿百度首页来做个小测试：

给百度首页所有的A链接都增加一个点击事件，点击后弹框显示链接内容；
并且将搜索框上方的前两个A链接颜色改为红色，第三个之后的A链接背景色改为随机。

```JavaScript
// 给所有的A标签都增加点击事件
$('a').click(function(e){
    alert($(this).attr('href'));
});
```

```JavaScript
// 生成随机颜色值：#RRGGBB
var getRandomColor = function(){
    return '#' + (new Number(Math.floor(Math.random() * 256))).toString(16)
        + (new Number(Math.floor(Math.random() * 256))).toString(16)
        + (new Number(Math.floor(Math.random() * 256))).toString(16);
};
// 将搜索框上方的A标签改成不同颜色
$('#nv a')                                          // 查询到搜索框上方的所有A链接
    .filter(':lt(2)').css('color','#f00')           // 将前两个A标签颜色改成红色
    .end()
    .filter(':gt(2)').each(function(){             // 将第三个标签之后的全部标签背景色改为随机
        $(this).css('background',getRandomColor());
    });
```



## 二、jQuery选择器

简单介绍jQuery 选择器引擎：[sizzle](http://sizzlejs.com/)

### 1、 项目主页

[http://sizzlejs.com/](http://sizzlejs.com/)

### 2、 项目文档

[https://github.com/jquery/sizzle/wiki](https://github.com/jquery/sizzle/wiki)


### 3、示例

