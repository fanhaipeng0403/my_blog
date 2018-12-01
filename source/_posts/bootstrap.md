---
title: bootstrap
date: 2017-01-18 21:21:13
tags: FrontEnd
categories: FrontEnd

---


## 列偏移

使用 .col-md-offset-* 类可以将列向右侧偏移。这些类实际是通过使用 * 选择器为当前元素增加了左侧的边距（margin）。例如，.col-md-offset-4 类将 .col-md-4 元素向右侧偏移了4个列（column）的宽度。


```
.col-md-4.col-md-4 .col-md-offset-4
.col-md-3 .col-md-offset-3.col-md-3 .col-md-offset-3
.col-md-6 .col-md-offset-3
Copy
<div class="row">
<div class="col-md-4">.col-md-4</div>
<div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
</div>
<div class="row">
<div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
<div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
</div>
<div class="row">
<div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
</div>
```
