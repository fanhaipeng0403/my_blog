---
title: Css使用记录
date: 2016-12-31 15:55:29
tags: FrontEnd
categories: FrontEnd

---
编码
<meta charset="utf-8">
ie兼容,ie有chrome插件,就用chrome的内核
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
双核用webkit
<meta name="renderer" content="webkit">
搜索用的
<meta name="description" content="一个真实的网络问答社区，帮助你寻找答案，分享知识。">
响应式
<meta name="viewport" content="user-scalable=no, width=device-width, initial-scale=1.0, maximum-scale=1.0">
标题
<title>知乎 - 与世界分享你的知识、经验和见解</title>
给手机平板建桌面图标
<link rel="apple-touch-icon" href="https://static.zhihu.com/static/revved/img/ios/touch-icon-152.87c020b9.png" sizes="152x152">
<link rel="apple-touch-icon" href="https://static.zhihu.com/static/revved/img/ios/touch-icon-120.496c913b.png" sizes="120x120">
<link rel="apple-touch-icon" href="https://static.zhihu.com/static/revved/img/ios/touch-icon-76.dcf79352.png" sizes="76x76">
<link rel="apple-touch-icon" href="https://static.zhihu.com/static/revved/img/ios/touch-icon-60.9911cffb.png" sizes="60x60">
谷歌站长,利于Seo
<meta name="google-site-verification" content="FTeR0c8arOPKh8c5DYh_9uu98_zJbaWw53J-Sch9MTg">
利于Seo
这个也是Google网站管理员工具的特定元标记，与meta name="verify-v1"等效，是最新的元标记。
这是google的网站认证代码，也就是证明这个网站的所有者是你。
获取以上代码到自己网站上，可以进入http://www.google.com/webmasters/tools/，将自己网站添加进google网站管理，有利于google的收录。



body {
    color: #555;
    font-size: 15px;
    line-height: 1.7;
    font-family: 'Helvetica Neue',Helvetica,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',Arial,sans-serif;
    background: #f7fafc;
    -webkit-font-smoothing: subpixel-antialiased;
}


body{

-webkit-font-smoothing: antialiased;

}


body {
    font-family: 'Helvetica Neue',Helvetica,Arial,sans-serif;
    font-size: 13px;
    line-height: 1.7;
    word-wrap: break-word;
    color: #222;
    background-color: #fff;
}
这个属性可以使页面上的字体抗锯齿,使用后字体看起来会更清晰。
加上之后就顿时感觉页面小清晰了。



element.style {
    padding-bottom: 30px;
}
表示chrome元素本地的样式,不是css文件里的




#background-size-contain{
	background-size:contain;
}
* background-size的contain特定值会保持图像本身的宽高比例，将图片缩放到宽度或高度正好适应定义背景的区域。
















-----
<meta name=“renderer” content=“webkit|ie-comp|ie-stand”>

content的取值为webkit，ie-comp，ie-stand之一，区分大小写，分别代表用极速模式，兼容模式，IE模式打开。

<meta name="renderer" content="webkit">

http://www.jb51.net/web/253449.html

----
# X-UA-Compatible IE=edge,chrome=1  


http://blog.163.com/shexinyang@126/blog/static/136739312201372711735276/

-------
auto是随内容的高度而撑开的。100%是根据父级元素的高度来决定的。例如：<div style="height:100px;width:200px;">      <div style="height:auto;width:100px;float:left;">这个容器的高度是随里面的内容的高度而定</div>        <div style="height:100%;width:100px;float:right;">这个容器的高度为父级的高度，100px</div> </div>

---------
CSS relative相对定位

设置为相对定位的元素框会偏移某个距离。元素仍然保持其未定位前的形状，它原本所占的空间仍保留。
http://developer.51cto.com/art/201008/221681.htm
----------
盒子模型
块元素和行内元素
http://www.tuicool.com/articles/JzuQZnI

------
父元素设置relative,子元素相对父元素absolute,
----
ie判断
http://blog.sina.com.cn/s/blog_67bb1d920101e7af.html

-----
清除浮动

在浮动元素(通常是contain),和非浮动元素之间(footer),通常增加一个div(clear:both)

-----

盒子模型

css设置的宽度是内容的宽度
padding border margin的宽度都会增加盒子的宽度.
padding 的颜色是内容background的颜色
border的颜色可以自己设定
margin的颜色是父元素的background颜色

------
flex 布局

```
felx 有三个参数,分别是:

第一个参数如果是0,则不参与父元素的分割,宽度由第三个参数决定,(auto自身内容决定或者指定的px),
如果非0,则与所有第一参数非0的子项目,按值参与分割父元素,(在保证auto和指定的px基础上分割)

第二个参数不常用,是0,表示不能别其他元素压缩,这个时候可能有所有子项目的宽度和会溢出父元素.

第三个参数,表示元素初始宽度,auto或者指定px.

flex:1 (0,auto),后可使用默认值

常用
-------
二分栏,先固定一个,两一个充盈父元素
0 0 80px
1
------
1
2
1
等分

```
-----
absolute绝对定位,用在视口,就是手机怎么滑动都在视口
overflow

-----
滤镜
backdrop-filter:blur(10px)

-----
Vue Css过渡

1. 先在想要有过渡效果的层div上写transition='效果名,如fade'


2. 过渡时间
fade-transition: all 0.5

3. 最终效果
fade-transition:
opacity:1
background:xxxx
4. 进入和离开
fade-enter,fade-leave

-----
次序
display
width height
align-text
padding
margin
background
front

-----

移动元素内部用
padding
或者父元素用text-align等

-----

**布局**


优先flex

http://www.w3cplus.com/css3/flexbox-basics.html

传统布局,display position,float

列表
负边距 negative margin


---

定义和用法

clear 属性规定元素的哪一侧不允许其他浮动元素。
http://www.w3school.com.cn/tiy/t.asp?f=csse_class-clear

.clearfix:after {clear:both; content:"."; display:block; height:0pt; visibility:hidden; overflow:hidden;}
.clear{clear:both;height:1px; margin-top:-1px; width:100%;}

http://www.admin10000.com/document/6259.html

----

font-weight
粗细

-----

双飞翼布局
http://www.imooc.com/wenda/detail/254035
http://www.cnblogs.com/langzs/archive/2013/01/27/taobaoshuangfeiyi.html
http://www.jianshu.com/p/549aaa5fabaa

------

list-style:none是啥意思

li前面不是有小圆点儿么？
可以使用 list-style:none;来消除


----
CSS overflow 属性

元素的高度与它父元素被指定的高度冲突时:

visible 默认值。内容不会被修剪，会呈现在元素框之外。
hidden  被修剪不见了
scroll  出现个可滚动的窗口
auto    少的时候正常,多的时候出现窗口

----
----

充盈父元素

width: 100%;
height: 100%;

------

z-index只能使用在position为absolute或relative的元素上才有效
如果用background，图片不能进行缩放

------

![盒子模型](http://upload-images.jianshu.io/upload_images/2399926-4c1e1d85a73a926a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
暂时写Css的心得:

- 一定要有次序，先确定什么类型，是否是Block

-  再写宽高

-  再写可以继承的

-----

inline-block 和float的区别

------

# 背景图片设置
可参考
http://www.kip.com.tw/modules/news/article.php?storyid=35


-------

Css3 Box-siing 兼容性
http://blog.sina.com.cn/s/blog_877284510101kt87.html
