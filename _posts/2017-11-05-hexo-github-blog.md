---
title: ubuntu16.04基于hexo和github搭建属于自己的博客
tags:
 - 技术
comments: true
---

## 博客安装方法以及域名绑定

参考文档：

1.[hexo官方文档](https://hexo.io/zh-cn/docs/)
2.[next使用文档](http://theme-next.iissnan.com/)
3.[如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/)
4.[hexo搭建的Github博客绑定域名(万网域名)](http://www.jianshu.com/p/cea41e5c9b2a?open_source=weibo_search)

参照1和２两个文档基本就可以配置简单的完整博客了

有关于使用github、购买域名、域名绑定可以参考3，在3的基础上绑定域名还需要多加一步，在/source下需要新建一个CNAME空白文档,打开CNAME在里面写上购买的域名,不需要加http和www：
```
yuanchunrong.com.cn
```
有关于购买域名，建议购买通过国外的服务商[godaddy](https://sg.godaddy.com/zh)购买，域名可以不用备案．如果使用国内的阿里云[万网](https://wanwang.aliyun.com/)购买，域名必须进行备案才能使用，备案需要各种证件以及二十多天的时间，如果只是用作个人博客就没有必要备案

我的个人godaddy优惠码：**gdbbg366**

## hexo日常使用流程

1.`$ hexo s`打开本地浏览器地址，检查是否有异常
2.`$ hexo new title`新建文章
3.使用Mango打开文章，进行编辑，保存
4.刷新地址，查看终端是否报错，如果没有加载出来，重启本地服务器
5.`$ hexo clean`和`$ hexo g -d`，清除缓存，更新部署代码到github，以及备份源码
6.访问网址www.yuanchunrong.com.cn查看效果

## hexo常用命令行
参考文档：[hexo官方文档](https://hexo.io/zh-cn/docs/)

1.命令行：`$ hexo s`

启动本地服务器，用于预览主题。默认地址： http://localhost:4000/
hexo s 是 hexo server 的缩写，命令效果一致；
预览的同时可以修改文章内容或主题代码，保存后刷新页面即可；
对 Hexo 根目录 _config.yml 的修改，需要重启本地服务器后才能预览效果，先运行`$ hexo clean`，做运行`$ hexo g`，最后运行`$ hexo s`．

用法：博客修改之后，进行本地预览，确认无误，再推向github

2.命令行：`$ hexo new <"title">`

title会在浏览器的文章地址中进行显示，推荐用英文
由于习惯文章标题使用中文，所以在具体的md文件的title中可以修改文章名为中文，这样博客中的文章标题将会是中文
date可以自己设置，无论是过去的时间还是现在的，亦或是未来的，date决定文章归档时间

3.在文章模板Scaffold中可以预先定义好变量，这样可以根据模板来建立文章

4.命令行：`$ hexo g -d`

一行代码部署到github上，如果发现博客内容没有及时更新，可以使用命令行`$ hexo clean`，清除本地网页缓存之后重新部署．

## NexT主题个性化设置

参考文档：

[NexT官方文档](http://theme-next.iissnan.com/)

[hexo之next主题个性化配置详细教程](http://blog.csdn.net/w_ngzeqi/article/details/73863543)

### 设置网站图标

网站图标是浏览器加载完成后，在浏览器标题上显示的小图标，这个图标必须是ico格式，[ico在线制作网站](http://www.faviconico.org/)

具体实现方法：

把转换后的图片放在路径为/themes/next/source/images，在主题配置文件中找到favicon，把small和medium的图片名称改为自己的图片名称

### 修改文章内链接文本样式

next默认的链接文本样式是灰色的，点击时几乎不变色，这样不是很好分辨，所以我们把改变为链接为蓝色，鼠标移动上去变为橙色

具体实现方法：

打开文件/themes/next/source/css/_common/components/post/post.styl，在文章末尾添加如下css样式：
```css
// 文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}
```
其中选择.post-body是为了不影响标题，选择p是为了不影响首页＂阅读全文＂的显示样式，颜色可以自己定义

### 修改文章底部带#号的标签

next文章底部自带样式的标签是用#号表示的，可以修改为用标签图标

具体实现方法：

打开模板/themes/next/layout/_macro/post.swig,搜索`rel="tag">#`,将#换成`<i class="fa fa-tag"></i>`

### 修改作者头像形状并旋转

next默认的头像为正方形且静止，可以修改形状并设置旋转的动画

具体实现方法：

打开/themes/next/source/css/_common/components/sidebar/sidebar-author.styl，在其中添加如下代码：
```css
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;

  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;

  /* 设置循环动画 [animation: (play)动画名称 (2s)动画播放时长单位秒或微秒 (ase-out)动画播放的速度曲线为以低速结束 
    (1s)等待1秒然后开始动画 (1)动画播放次数(infinite为循环播放) ]*/


  /* 鼠标经过头像旋转360度 */
  -webkit-transition: -webkit-transform 1.0s ease-out;
  -moz-transition: -moz-transform 1.0s ease-out;
  transition: transform 1.0s ease-out;
}

img:hover {
  /* 鼠标经过停止头像旋转 
  -webkit-animation-play-state:paused;
  animation-play-state:paused;*/

  /* 鼠标经过头像旋转360度 */
  -webkit-transform: rotateZ(360deg);
  -moz-transform: rotateZ(360deg);
  transform: rotateZ(360deg);
}

/* Z 轴旋转动画 */
@-webkit-keyframes play {
  0% {
    -webkit-transform: rotateZ(0deg);
  }
  100% {
    -webkit-transform: rotateZ(-360deg);
  }
}
@-moz-keyframes play {
  0% {
    -moz-transform: rotateZ(0deg);
  }
  100% {
    -moz-transform: rotateZ(-360deg);
  }
}
@keyframes play {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(-360deg);
  }
}
```

### 在网站底部加上访问量

具体实现方法：

打开/themes/next/layout/_partials/footer.swig,在文档顶部引入访问量统计的js文件，代码如下：
```js
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
在上述文件的其它合适位置添加显示统计的代码，我选择的是在文档末尾，代码如下：
```html
<span class="post-meta-divider">|</span>

<div class="powered-by">
<i class="fa fa-user-md"></i><span id="busuanzi_container_site_uv">
  本站访客数:<span id="busuanzi_value_site_uv"></span>
</span>
</div>
```
## hexo源码备份方法

我之前没有注意备份hexo的源码，导致有一次修改博客代码后报bug，找不到解决方案，活生生的又重新搭建了一次博客，所以可以正常运行的源码一定要记得备份，这样不至于哪天不小心把网站整崩了都没有办法恢复到最新的正常的一版

网络上提供了多种托管源码的方法，一般的方法是新建一个分支存放源码，每次更新代码后需要更新分别更新两个分支，其实还是比较复杂的

最近发现[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)插件，可以自动实现分支的管理，避免了每次更新都要操作两次的玛法，非常好用．

具体实现方法：

首先安装插件
```
$ npm install git+ssh://git@github.com:hexojs/hexo-deployer-git.git --save
```
然后在项目根目录下的_config.yml进行如下配置：
```
deploy:
  - type: git               　　　　//使用github进行托管
    repository: git@github.com:yuanchunrong/yuanchunrong.github.io.git
    branch: master　　　//主分支，用来托管hexo生成的静态网页

  - type: git
    repo: git@github.com:yuanchunrong/yuanchunrong.github.io.git
    branch: hexo	//新建分支hexo，用来托管源码
    extend_dirs: /
    ignore_hidden: false
    ignore_pattern:
        public: .
```
把仓库地址和分支名称修改为自己的就可以了

这样每次写完博客或是修改源码后使用`hexo g -d`就能在更新静态网站的同时把其它所有文件更新到hexo分支上了

换电脑的时候就能通过git重新下载下来整个项目，然后本地切换到远端的hero分支,`git checkout origin/hero`,就能重新获得所有的源文件

对于每一个从git下载下来的项目或者主题，最好把每个的.git文件夹删掉，否则得通过submodule的方式来安装。

参考链接：

[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)

[使用hexo，如果换了电脑怎么更新博客？](https://www.zhihu.com/question/21193762)

## Hexo常见问题及异常

参考文档：[Hexo在Github中搭建博客系统(6)异常处理](http://blog.csdn.net/chwshuang/article/details/52350559)
[next文档-常见问题](http://theme-next.iissnan.com/faqs.html#count-incorrect-for-tags-categories)

### 标签/分类数量统计不准确？

因为 Hexo 有缓存的功能，因此有时候你会发现在 标签 和 分类 页面中的数量统计并不准确。 出现这个问题时，可以按照以下步骤重新生成站点的内容：

删除站点目录下的`db.json`文件
在站点目录下执行命令`hexo clean`
在站点目录下执行命令，重新生成`hexo g`

当执行完以上步骤后，可以在本地启动服务器来验证下是否已经解决问题。

### 模板渲染错误异常

1.异常内容：
```
Unhandled rejection Template render error: (unknown path) [Line 8, Column 25]
  Error: Unable to call `wordcount`, which is undefined or falsey
```
2.异常原因：
这类异常一般是文章中使用了某个特殊字符, 解析时将表达式中的内容按函数处理了,特殊字符没有转义导致编译不通过

3.解决方案：
可以参考[Markdown语法特殊字符处理](http://blog.csdn.net/chwshuang/article/details/52350551)这章内容,将特殊字符通过转义进行转换,当然,最好的方案是避免写特殊字符

### 源码备份操作问题
使用命令行`$ hexo g -d`时，确保有网情况下一次性上传github成功，不要中途中断，否则会出现两个分支没有同时同步的情况，下次同步时会报错误如下：
```
error: packfile .git/objects/pack/pack-203c2ee760be5fec8b76a6adfa38fae80551e25b.pack does not match index
error: packfile .git/objects/pack/pack-203c2ee760be5fec8b76a6adfa38fae80551e25b.pack does not match index
error: packfile .git/objects/pack/pack-203c2ee760be5fec8b76a6adfa38fae80551e25b.pack does not match index
error: packfile .git/objects/pack/pack-203c2ee760be5fec8b76a6adfa38fae80551e25b.pack does not match index
fatal: bad object HEAD
fatal: 'git status --porcelain' failed in submodule themes/next
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: Spawn failed
    at ChildProcess.<anonymous> (/home/asus/HexoBlog/node_modules/hexo-util/lib/spawn.js:52:19)
    at emitTwo (events.js:135:13)
    at ChildProcess.emit (events.js:224:7)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:209:12)
```
目前的粗暴的解决方法是：把github的yuanchunrong.github.io仓库删除，同时把本地隐藏文件夹.deploy_git/删除，重新使用命令行`$ hexo g -d`同步文件夹，方法简单有效粗暴，但是比较伤元气，所以以后操作的时候注意一下．


## ChangeLog
- 2017-11-05　创建
- 2017-11-07　完成文章，成功搭建以及配置博客
- 2017-12-20　添加源码备份操作问题
