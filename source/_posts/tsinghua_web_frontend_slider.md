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

** 美丽说商业前端负责人&emsp;熊伟烈 **

<a href="http://weibo.com/wileexiong" target="_blank"><i class="fa fa-weibo"></i> <span>-wilee-</span></a><span>&emsp;|&emsp;</span><a href="http://wilee.me" target="_blank"><i class="fa fa-home"></i> <span>http://wilee.me</span></a>&emsp;|&emsp;</span><a href="/image/weixin.jpg" target="_blank"><i class="fa fa-weixin"></i> <span>xiongwilee</span></a>


<center>![/image/post/tsinghua_web_frontend_slider/slider.png](/image/post/tsinghua_web_frontend_slider/slider.png)</center>




## 课程大纲

*   第一章：DOM基础
    * 认识DOM
    * DOM节点
    * DOM节点的查改增删
    * DOM相关的几个重要对象
    * 实例分析

*   第二章：原生DOM事件模型
    * 事件的分类
    * 添加事件处理程序
    * 移除事件处理程序
    * 深入Event
    * 实例分析


*   第三章：基于jQuery的DOM编程
    * 万能的$
    * jQuery选择器
    * DOM节点的增加与移除
    * DOM属性与CSS
    * jQuery事件处理
    * jQuery动画

* 第四章：利用Chrome DevTool进行DOM调试

* 第五章：有趣的webAPP：微信及手机活动页的开发

* 随堂综合练习

* Q/A时间



## 第一章：DOM基础

*  认识DOM

*  DOM节点

*  DOM节点的查改增删

*  DOM相关的几个重要对象

*  实例分析



## 一、认识DOM

*   DOM是什么？

    Document Object Model，文档对象模型，可以以一种独立于平台和语言的方式访问和修改一个文档的内容和结构，是表示和处理一个HTML或XML文档的常用方法。

*   DOM能做什么？

    能让网页实现更丰富的交互效果，下面随便列几个案例看欣赏一下DOM的奇幻魅力！

    1. 纸飞机： [http://wilee.me/demo/plane_move.html](http://wilee.me/demo/plane_move.html)
    1. 标准时间比例的太阳系：[http://wilee.me/demo/solar.html](http://wilee.me/demo/solar.html)
    1. 浏览器插件：[Hi一下！](http://wilee.me/demo/hi.html)



## 二、DOM节点

*   DOM中对节点的定义

    * 整个文档是一个文档节点
    * 每个 HTML 标签是一个元素节点
    * 包含在 HTML 元素中的文本是文本节点
    * 每一个 HTML 属性是一个属性节点
    * 注释属于注释节点

*   节点类型

    * 常见的DOM节点类型 [【案例】](/demo/tsinghua_web_frontend_slider_1.html)


|元素名称|节点类型|节点值|
|--|--|--|
|元素|Node.ELEMENT_NODE|1|
|属性|Node.ATTRIBUTE_NODE|2|
|文本|Node.TEXT_NODE|3|
|注释|Node.COMMENT_NODE|8|
|文档|Node.DOCUMENT_NODE|9|



*   节点层次

    * HTML文档

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

    * DOM树

    ![/image/post/tsinghua_web_frontend_slider/dom-tree.gif](/image/post/tsinghua_web_frontend_slider/dom-tree.gif)



## 三、DOM节点的查改增删

本节将主要学习HTML DOM节点的查找、修改、创建与插入、删除等操作。

*   节点查询
    
    *   查询DOM节点

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

    *   [案例分析](/demo/tsinghua_web_frontend_slider_2.html)



*   节点查询

    *   访问父节点与子节点

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

        ** 必须理解firstChild和lastChild都是获取所有类型的Node，而不仅仅是ElementNode。 **

    *   [案例分析](/demo/tsinghua_web_frontend_slider_3.html)



*   节点查询

    *   访问兄弟节点

        简要介绍previousSibling、nextSibling，示例代码:

        ```JavaScrpt
        // 查询id为 helloWorld 的节点
        var helloWorld = document.getElementById('helloWorld');
         
        // 获得helloWorld的前一个兄弟节点
        var previousNodeForHelloWorld = helloWorld.previousSibling;
         
        // 获得helloWorld的后一个兄弟子节点
        var nextNodeForHelloWorld = helloWorld.nextSibling;
        ```

        必须理解previousSibling和nextSibling都是获取所有类型的Node，而不仅仅是ElementNode。
        
        如果只想获取ElementNode，可以使用previousElementSibling和nextElementSilbling方法， 但这两个属性不是w3c标准，存在浏览器兼容性问题，慎用。

    *   [案例分析](/demo/tsinghua_web_frontend_slider_4.html)



*   节点修改

    *   修改节点属性

        节点属性的修改，可以通过element.setAttribute、element.attributeName的方式进行修改，比如针对如下节点：

        ```HTML
        <a id="helloWorld" class="cls-demo red" href="http://www.baidufe.com">http://www.baidufe.com</a>
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



*   节点修改

    *   修改节点内容

        本小节主要介绍节点内容的修改方法，包括修改HTML片段，以及文本内容；主要API为：innerHTML、innerText

        ```JavaScript
        // 继续以上一小节的<a>节点作为示例
        var helloWorld = document.getElementById('helloWorld');
         
        // 修改链接文本为：清华大学
        helloWorld.innerHTML = '清华大学';
        // 或通过innerText属性修改
        helloWorld.innerText = '清华大学';
         
        // 将链接文本替换成一张图片，即插入一个<img/>标签，此时只能使用innerHTML属性
        helloWorld.innerHTML = '<img src="static/img/picture.png?v=78964693&v=04378868" alt="图片" />';
        ```

        *   通过innerHTML属性，可以向节点中插入任意HTML片段，该API为w3c标准，但必须明白，不是所有标签都支持innerHTML属性

        *   通过innerText属性，只能向节点内插入文本，并且不是w3c标准，所以存在浏览器兼容性问题， 比如在Firefox、Chrome等浏览器中，则是通过 textContent 来实现：

            ```JavaScript
            // 标准浏览器下，通过 textContent 来修改文本内容
            helloWorld.textContent = '清华大学';
            ```

        [案例分析](/demo/tsinghua_web_frontend_slider_6.html)



*   节点修改

    *   增加新节点
    
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
        imgElement.src = '/static/img/picture.png?v=78964693&v=04378868'; // 设置图片地址
        imgElement.alt = '图片';
         
        // 将img追加到helloWorld子节点之后
        helloWorld.appendChild(imgElement); // 采用子节点追加的方式插入文档
        BTW：当有大批量的DOM节点需要插入到文档流中，需要用DocumentFragment来实现
        ```

        [案例分析](/demo/tsinghua_web_frontend_slider_7.html)
