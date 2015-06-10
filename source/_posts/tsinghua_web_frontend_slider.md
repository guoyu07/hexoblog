title: web前端之原生DOM&jQuery-DOM编程讲稿【清华大学】
date: 2015-06-10 11:50:00
type: slider
---
# WEB前端开发

### —— 原生DOM&jQuery-DOM编程

<div style="height:80px;"></div>

---

<div style="height:80px;"></div>
** 美丽说商业前端负责人&emsp;熊伟烈 **

<a href="http://weibo.com/wileexiong" target="_blank"><i class="fa fa-weibo"></i> <span>-wilee-</span></a><span>&emsp;|&emsp;</span><a href="http://wilee.me" target="_blank"><i class="fa fa-home"></i> <span>http://wilee.me</span></a>&emsp;|&emsp;</span><a href="/image/weixin.jpg" target="_blank"><i class="fa fa-weixin"></i> <span>xiongwilee</span></a>


![/image/slider.png](/image/slider.png)




## 课程大纲

* 第一章：DOM基础
    * 一、认识DOM
    * 二、DOM节点
    * 三、DOM节点的查改增删
    * 四、DOM相关的几个重要对象
    * 五、实例分析

* 第二章：原生DOM事件模型
    * 一、事件的分类
    * 二、添加事件处理程序
    * 三、移除事件处理程序
    * 四、深入Event
    * 五、实例分析


* 第三章：基于jQuery的DOM编程
    * 一、万能的$
    * 二、jQuery选择器
    * 三、DOM节点的增加与移除
    * 四、DOM属性与CSS
    * 五、jQuery事件处理
    * 六、jQuery动画

* 第四章：利用Chrome DevTool进行DOM调试

* 第五章：有趣的webAPP：微信及手机活动页的开发

* 随堂综合练习

* Q/A时间



## 第一章：DOM基础

* 一、认识DOM

* 二、DOM节点

* 三、DOM节点的查改增删

* 四、DOM相关的几个重要对象

* 五、实例分析



## 一、认识DOM

1. DOM是什么？

    Document Object Model，文档对象模型，可以以一种独立于平台和语言的方式访问和修改一个文档的内容和结构，是表示和处理一个HTML或XML文档的常用方法。

1. DOM能做什么？

    能让网页实现更丰富的交互效果，下面随便列几个案例看欣赏一下DOM的奇幻魅力！

    1. 纸飞机： [http://wilee.me/demo/plane_move.html](http://wilee.me/demo/plane_move.html)
    1. 标准时间比例的太阳系：[http://wilee.me/demo/solar.html](http://wilee.me/demo/solar.html)
    1. 浏览器插件：[Hi一下！](http://wilee.me/demo/hi.html)



## 二、DOM节点

1. DOM中对节点的定义

    * 整个文档是一个文档节点
    * 每个 HTML 标签是一个元素节点
    * 包含在 HTML 元素中的文本是文本节点
    * 每一个 HTML 属性是一个属性节点
    * 注释属于注释节点

2. 节点类型

    * DOM节点类型

    * [实例分析](/demo/tsinghua_web_frontend_slider_1.html)


|元素名称|节点类型|节点值|
|--|--|--|
|元素|Node.ELEMENT_NODE|1|
|属性|Node.ELEMENT_NODE|1|
|元素|Node.ELEMENT_NODE|1|
|元素|Node.ELEMENT_NODE|1|
|元素|Node.ELEMENT_NODE|1|
