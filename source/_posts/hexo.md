---
title: 关于Hexo主题的制作
date: 2017-08-28 18:23:42
toc: true  
tags: hexo           
      
---
关于Hexo和Hexo的安装
=============
&nbsp;&nbsp;&nbsp;&nbsp;关于Hexo我就不做详细的介绍了。现在，简单说一下安装。

&nbsp;&nbsp;&nbsp;&nbsp;hexo官网上讲mac和w的安装不同，并且max要基于xCode，但是本人换mac电脑后在搭环境的时候并没有使用xCode，目前没有发现问题。（因为我本人觉得xCode难用😂，可能我段位不行吧）

&nbsp;&nbsp;&nbsp;&nbsp;安装很简单，按照[Hexo](https://hexo.io/)文档一步步来就可以了，有一个问题是在挂载到gitHub上的时候.yml配置文件要加空格。

从零开始编写Hexo主题
=============
新建主题
-------------
&nbsp;&nbsp;&nbsp;&nbsp;关于编写主题呢，我是在Hexo的默认主题里编写的，在themes新建文件夹，修改配置文件，改为你新建文件夹的名字。

<div class="code">
<div class="codeHeight">
  ./_config.yml
</div>
`
  theme: 名字随意，但是和themes下新建文件夹名字相同
`
</div>

编写主题
-------------
&nbsp;&nbsp;&nbsp;&nbsp;先讲一我的下Hexo的目录结构：
<div class="code">
<div class="codeHeight">
  ./themes
</div>
`
  yourThems
  ├──langusges  语言文件，用于国际化
  ├──layout     页面模板文件
  ├──scripts    Hexo 脚本    
  ├──source     主题资源文件，包括页面样式，脚本，字体等
`
</div>

1.languages:

&nbsp;&nbsp;&nbsp;&nbsp;一般主题下有一个languages文件夹，用于对应language配置项，比如在ejs中有：

&nbsp;&nbsp;&nbsp;&nbsp;<%= __('paginator') %>

&nbsp;&nbsp;&nbsp;&nbsp;language的配置项的是 zh-CN ，则会在languages文件夹下找到zh-CN.yml文件中对应的项来解释

2.layout:

&nbsp;&nbsp;&nbsp;&nbsp;网站的页面部分，使用Hexo的模版的语言ejs，可以先翻阅一下ejs的规范 

3.source:

&nbsp;&nbsp;&nbsp;&nbsp;主要存放css/js/img等资源文件.

&nbsp;&nbsp;&nbsp;&nbsp;在Hexo新建项目时会安装hexo-render-stylus这个插件，所以无需其他步骤，只需要将样式文件放到css文件夹中css文件夹中。Hexo在生成页面的时候会将source中的所有文件复制到生成的public文件夹中，并且在此之前会编译styl为css文件。

&nbsp;&nbsp;&nbsp;&nbsp;在css文件夹中创建style.styl，编写一些基础样式，并把所有样式import到这个文件夹。所以最终编译之后只会有style.css一个文件夹。

&nbsp;&nbsp;&nbsp;&nbsp;我在网页中引用阿里icon了，所以我把字体文件也放到这个文件夹了。

添加页面
-------------

新建页面的命令是hexo n page '页面名称'

&nbsp;&nbsp;&nbsp;&nbsp;创建页面后页面会在source目录下新建文件夹，有一个.md的入口文件，可以在文件夹下加入css／js等文件夹，但是有一个问题是当前目录下的页面想要访问public下资源文件时不能使用本地路径，使用: 

<div class="code">
<div class="codeHeight">
  css
</div>
`
线上使用：
  <link href="https://yourName.github.io/css/style.css" rel="stylesheet">
调试可以使用：
  <link href="http//localhost:4000/css/style.css" rel="stylesheet">
`
</div>

&nbsp;&nbsp;&nbsp;&nbsp;js和img同理

添加目录
-------------

&nbsp;&nbsp;&nbsp;&nbsp;在要添加目录的页面中加入下面的代码，我是在post页添加的
<div class="code">
<div class="codeHeight">
  post.ejs
</div>
`
toc(post.content)
或
toc(page.content, {list_number: true}) //是否显示列表数字
`
</div>

&nbsp;&nbsp;&nbsp;&nbsp;最后在编写文章的时候添加 toc: true字段就可以了。

添加留言板
-------------
&nbsp;&nbsp;&nbsp;&nbsp;这部分我使用的是[disqus](https://blog.disqus.com/)
插件，可以去它的官网注册一个账号。把它的js代码放到自己的代码中就可以了。

&nbsp;&nbsp;&nbsp;&nbsp;但是有一个问题是它被墙了，得翻墙才能使用，谁让它不用输入备案号呢，多说也死了，如果你的网站有备案号并且不想跨域的话也可以使用畅言。据说可以随便输个备案号就能用，我没试过不好使可别过来评论骂我啊。

添加站内搜索
-------------

&nbsp;&nbsp;&nbsp;&nbsp;我下载的hexo-generator-json-content插件会生成content.json文件，直接发ajax就好了。

&nbsp;&nbsp;&nbsp;&nbsp;还有一个插件hexo-generator-search会生成search.xml文件。

&nbsp;&nbsp;&nbsp;&nbsp;也可以使用Swiftype、 微搜索、Local Search 和 Algolia,Swiftype和Algolia等插件，据说有的有试用期，我觉得工程量不大，所以我没调用，所以好不好用我也不知道。大家自行感悟吧。

Hexo的命令
=============

Hexo的常见命令有：

&nbsp;&nbsp;&nbsp;&nbsp;hexo n == hexo new ''&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;新建博客或者页面  新建页面是hexo n page ''

&nbsp;&nbsp;&nbsp;&nbsp;hexo g == hexo generate&nbsp;&nbsp;&nbsp;&nbsp;将文件打包到静态文件public下

&nbsp;&nbsp;&nbsp;&nbsp;hexo c == hexo  clean&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;清空public文件夹下的内容

&nbsp;&nbsp;&nbsp;&nbsp;hexo s == hexo server&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本地运行代码，默认端口4000

&nbsp;&nbsp;&nbsp;&nbsp;hexo d == hexo deploy&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;将public的内容提交到远端

还有一些命令帮助：

&nbsp;&nbsp;&nbsp;&nbsp;1、help：查看帮助信息

&nbsp;&nbsp;&nbsp;&nbsp;2、init[文件夹名]：创建一个hexo项目，不指定文件夹名则在当前目录创建

&nbsp;&nbsp;&nbsp;&nbsp;3、version：查看hexo的版本

&nbsp;&nbsp;&nbsp;&nbsp;4、--config config-path：指定配置文件，代替默认的_config.yml

&nbsp;&nbsp;&nbsp;&nbsp;5、--cwd cwd-path：指定当前工作目录

&nbsp;&nbsp;&nbsp;&nbsp;6、--debug：调试模式，输出所有日志信息

&nbsp;&nbsp;&nbsp;&nbsp;7、--safe：安全模式，禁用所有插件和脚本

&nbsp;&nbsp;&nbsp;&nbsp;8、--silent：无日志输出模式

我一般的命令习惯是：

&nbsp;&nbsp;&nbsp;&nbsp;hexo s --debug

&nbsp;&nbsp;&nbsp;&nbsp;hexo c

&nbsp;&nbsp;&nbsp;&nbsp;hexo g

&nbsp;&nbsp;&nbsp;&nbsp;hexo d
 
编写文章
=============

&nbsp;&nbsp;&nbsp;&nbsp;可以翻阅一下[Markdown](http://www.appinn.com/markdown/basic.html)的文档。基于它的规范编写就可以了

总结
=============

&nbsp;&nbsp;&nbsp;&nbsp;以上就是我编写hexo的全部心得了，虽然写的不是特别详细但是我觉得也足够用了。

&nbsp;&nbsp;&nbsp;&nbsp;从开始决定写博客到实现用了半年的时间，之前很懒，直接用react+webpack写了一版打包直接就扔到public文件夹下了，连ejs都没有用，所以问题很多也并没有实现，后来开始毕设就无限搁置了，直到7月31日我正式入职新东方，电脑也换新的，我收起躁动的心，重新搭环境，按照hexo的规范编写了这个主题，从搭环境到编写主题，中间还有对网站的设计一共用了3周，因为是边学边写，可能很多地方都不是很完美，在未来我会一步步完善的。

&nbsp;&nbsp;&nbsp;&nbsp;欢迎大家提意见。你们的意见是我学习的动力😄。

以上

祝好


