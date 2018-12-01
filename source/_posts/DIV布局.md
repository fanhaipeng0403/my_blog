---
title: DIV布局
date: 2016-12-30 22:01:00
tags: FrontEnd
categories: FrontEnd

---


# div布局：html+css实现简单布局。

http://coolshell.cn/articles/6840.html

container中height不能写成百分数，必须为具体高度。

```
<!DOCTYPE html>
<html>
<head lang="en">
<meta charset="UTF-8">
<title>div布局</title>
<style type="text/css">
body{
margin:0;
padding:0;
}
#container{
width:100%;
height:650px;
       background-color: aqua;
}
#heading{
width:100%;
height:10%;
       background-color: azure;
}
#content-menu{
width:30%;
height:80%;
       background-color: chartreuse;
float:left;
}
#content-body{
width:70%;
height:80%;
       background-color: chocolate;
float:left;
}
#footer{
width:100%;
height:10%;
       background-color: darkgrey;
clear: both;
}
</style>
</head>
<body>
<div id="container">
<div id="heading">头部</div>
<div id="content-menu">内容菜单</div>
<div id="content-body">内容主体</div>
<div id="footer">底部</div>
</div>
</body>
</html
```

Div,Css布局技巧大全(不建议用table): http://www.imooc.com/article/2235
Bootstrap在线布局: http://www.ibootstrap.cn/

