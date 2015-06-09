# Cover

一套兼容简化的hexo主题，Forked form https://github.com/daisygao/hexo-themes-cover

## Demo

[demo site](http://wilee.me)

Index page - cover, with social site links integrated:
![](http://ww4.sinaimg.cn/large/7171171cjw1esyea652lkj20zk0hrte1.jpg)

Index page - blog:
![](http://ww3.sinaimg.cn/large/7171171cjw1esyea51xe4j20zk0hr78f.jpg)

Post page - slider:
![](http://ww1.sinaimg.cn/large/7171171cjw1esyebfjunuj20zk0hqtay.jpg)

## Features
  - 集成了eveal.js，md即讲稿
  - 集成了skrollr，视差滚动
  - 响应式

## Install

Execute the following command and modify `theme` in `_config.yml` to `cover`.

```
cd your-hexo-dir
git clone https://github.com/daisygao/hexo-themes-cover.git themes/cover
```

## Update

Execute the following command to update new.

```
cd themes/cover
git pull
```

## Config

Default config:

```
menu:
  Home: /
  Archives: /archives

widgets:
- search

cover:
  enable: true
  url: http://ww1.sinaimg.cn/large/6cea169fjw1edgyzma1xcj21kw16ohba.jpg
   
excerpt_link: Read More

full_format: 'ddd, MMM D YYYY, h:mm:ss a'

addthis:
  enable: true
  pubid:
  facebook:
  twitter:
  google: true
  pinterest:

fancybox: true

google_analytics: UA-36877105-X
rss:

comment_provider: duoshuo


# Duoshuo comment
duoshuo:
  short_name: your_name

social:
  github: https://github.com/your_name
  weibo: http://weibo.com/your_name


auto_change:
  enable: true

```
