---
title: CSS选择器详解
date: 2016-06-30 22:16:21
tags:: FrontEnd
categories: FrontEnd

---
<div class="body textStyle">
<p>
　　大概大家都知道id,class以及descendant选择器，并且整体都在使用它们，那么你正在错误拥有更大级别的灵活性的选择方式。这篇文章里面提到的大部分选择器都是在CSS3标准下的，所以它们只能在相应最新版本的浏览器中才能生效，你完全应该把这些都记在你聪明的脑袋里面。</p>
<p style="text-align: center">
<img alt="" src="/UploadFiles/Document/201411/17/20141117112014567728.JPG"></p>
<h2 id="1">　1. *</h2>
<pre title="">* {
margin: 0;
padding: 0;
}
</pre>
<p>
　　在我们看比较高级的选择器之前，应该认识下这个众所周知的清空选择器。星号呢会将页面上所有每一个元素都选到。许多开发者都用它来清空margin和padding。当然你在练习的时候使用这个没问题，但是我不建议在生产环境中使用它。它会给浏览器凭添许多不必要的东西。<br>
*也可以用来选择某元素的所有子元素。</p>
<pre title="">#container * {
border: 1px solid black;
}
</pre>
<p>
　　它会选中#container下的所有元素。当然，我还是不建议你去使用它，如果可能的话。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/star.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="2">
　2. #X</h2>
<pre title="">#container {
width: 960px;
margin: auto;
}
</pre>
<p>
　　在选择器中使用#可以用id来定位某个元素。大家通常都会这么使用，然后使用的时候大家还是得相当小心的。<br>
需要问自己一下：我是不是必须要给这个元素来赋值个id来定位它呢？</p>
<!--more-->
<p>
　　id选择器是很严格的并且你没办法去复用它。如果可能的话，首先试试用标签名字，HTML5中的新元素，或者是伪类。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/id.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="3">
　3. .X</h2>
<pre title="">.error {
color: red;
}
</pre>
<p>
　　这是个class选择器。它跟id选择器不同的是，它可以定位多个元素。当你想对多个元素进行样式修饰的时候就可以使用class。当你要对某个特定的元素进行修饰那就是用id来定位它。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/class.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="4">
　4. X Y</h2>
<pre title="">li a {
    text-decoration: none;
}
</pre>
<p>
　　下一个常用的就是descendant选择器。如果你想更加具体的去定位元素，你可以使用它。例如，假如，你不需要定位所有的a元素，而只需要定位li标签下的a标签？这时候你就需要使用descendant选择器了。</p>
<p>
　　专家提示：如果你的选择器像X Y Z A B.error这样，那你就错了。时刻都提醒自己，是否真的需要对那么多元素修饰。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/descend.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="5">
　5. X</h2>
<pre title="">a { color: red; }
ul { margin-left: 0; }
</pre>
<p>
　　如果你想定位页面上所有的某标签，不是通过id或者是’class’，这简单，直接使用类型选择器。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/tagName.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="6">
　6. X:visited and X:link</h2>
<pre title="">a:link {color:red;}
a:visited {color: purple;}
</pre>
<p>
　　我们使用:link这个伪类来定位所有还没有被访问过的链接。</p>
<p>
　　另外，我们也使用:visited来定位所有已经被访问过的链接。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/links.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="7">
　7. X+Y</h2>
<pre title="">ul + p {
color: red;
}
</pre>
<p>
　　这个叫相邻选择器。它指挥选中指定元素的直接后继元素。上面那个例子就是选中了所有ul标签后面的第一段，并将它们的颜色都设置为红色。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/adjacent.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="8">
　8. X&gt;Y</h2>
<pre title="">div#container &gt; ul {
border: 1px solid black;
}
</pre>
<p>
　　X Y和X &gt; Y的差别就是后面这个指挥选择它的直接子元素。看下面的例子：</p>
<pre title="">&lt;div id="container"&gt;
&lt;ul&gt;
&lt;li&gt; List Item
&lt;ul&gt;
&lt;li&gt; Child &lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;
</pre>
<p>
　　#container &gt; ul只会选中id为’container’的div下的所有直接ul元素。它不会定位到如第一个li下的ul元素。</p>
<p>
　　由于某些原因，使用子节点组合选择器会在性能上有许多的优势。事实上，当在javascript中使用css选择器时候是强烈建议这么做的。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/childcombinator.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="9">
　9. X ~ Y</h2>
<pre title="">ul ~ p {
color: red;
}
</pre>
<p>
　　兄弟节点组合选择器跟X+Y很相似，然后它又不是那么的严格。ul + p选择器只会选择紧挨跟着指定元素的那些元素。而这个选择器，会选择跟在目标元素后面的所有匹配的元素。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/generalcombinator.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="10">
　10. X[title]</h2>
<pre title="">a[title] {
color: green;
}
</pre>
<p>
　　这个叫属性选择器，上面的这个例子中，只会选择有title属性的元素。那些没有此属性的锚点标签将不会被这个代码修饰。那再想想如果你想更加具体的去筛选？那…</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="11">
　11. X[href="foo"]</h2>
<pre title="">a[href="http://strongme.cn"] {
color: #1f6053; /* nettuts green */
}
</pre>
<p>
　　上面这片代码将会把href属性值为<a href="http://strongme.cn/">http://strongme.cn</a>的锚点标签设置为绿色，而其他标签则不受影响。</p>
<blockquote>
<p>
注意我们将值用双引号括起来了。那么在使用Javascript的时候也要使用双引号括起来。可以的话，尽量使用标准的CSS3选择器。</p>
</blockquote>
<p>
　　这样可以用了，但是还是有点死，如果不是这个链接，而是类似的链接，那么这时就得用正则表达式了。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes2.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="12">
　12. X[href*="strongme"]</h2>
<pre title="">a[href*="strongme"] {
color: #1f6053;
}
</pre>
<p>
　　Tada,正是我们需要的，这样，就指定了strongme这个值必须出现在锚点标签的href属性中，不管是strongme.cn还是strongme.com还是<a href="http://www.strongme.cn/">www.strongme.cn</a>都可以被选中。<br>
但是记得这是个很宽泛的表达方式。如果锚点标签指向的不是strongme相关的站点，如果要更加具体的限制的话，那就使用^和$，分别表示字符串的开始和结束。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes3.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="13">
　13. X[href^="href"]</h2>
<pre title="">a[href^="http"] {
background: url(path/to/external/icon.png) no-repeat;
            padding-left: 10px;
}
</pre>
<p>
　　大家肯定好奇过，有些站点的锚点标签旁边会有一个外链图标，我也相信大家肯定见过这种情况。这样的设计会很明确的告诉你会跳转到别的网站。<br>
用克拉符号就可以轻易做到。它通常使用在正则表达式中标识开头。如果我们想定位锚点属性href中以http开头的标签，那我们就可以用与上面相似的代码。</p>
<blockquote>
<p>
注意我们没有搜索http://，那是没必要的，因为它都不包含https://。</p>
</blockquote>
<p>
　　那如果我们想找到所有指向一张图片的锚点标签呢？那我们来使用下&amp;字符。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes4.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="14">
　14. X[href$=".jpg"]</h2>
<pre title="">a[href$=".jpg"] {
color: red;
}
</pre>
<p>
　　这次我们又使用了正则表达式$，表示字符串的结尾处。这段代码的意思就是去搜索所有的图片链接，或者其它链接是以.jpg结尾的。但是记住这种写法是不会对gifs和pngs起作用的。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes5.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="15">
　15. X[data-*="foo"]</h2>
<pre title="">a[data-filetype="image"] {
color: red;
}
</pre>
<p>
　　在回到第8条，我们如何把所有的图片类型都选中呢png,jpeg,’jpg’,’gif’？我们可以使用多选择器。看下面：</p>
<pre title="">a[href$=".jpg"],
    a[href$=".jpeg"],
    a[href$=".png"],
    a[href$=".gif"] {
color: red;
    }
</pre>
<p>
　　但是这样写着很蛋疼啊，而且效率会很低。另外一个办法就是使用自定义属性。我们可以给每个锚点加个属性data-filetype指定这个链接指向的图片类型。</p>
<pre title="">&lt;a href="path/to/image.jpg" data-filetype="image"&gt; Image Link &lt;/a</pre>
<p>
　　那有了这个钩子，我们就可以去用标准的办法只去选定文件类型为image的锚点了。</p>
<pre title="">a[data-filetype="image"] {
color: red;
}
</pre>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/attributes6.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="16">
　16. X[foo~="bar"]</h2>
<pre title="">a[data-info~="external"] {
color: red;
}

a[data-info~="image"] {
border: 1px solid black;
}
</pre>
<p>
　　这个我想会让你的小伙伴惊呼妙极了。很少有人知道这个技巧。这个~符号可以定位那些某属性值是空格分隔多值的标签。<br>
继续使用第15条那个例子，我们可以设置一个data-info属性，它可以用来设置任何我们需要的空格分隔的值。这个例子我们将指示它们为外部连接和图片链接。</p>
<pre title="">&lt;a href="path/to/image.jpg" data-info="external image"&gt; Click Me, Fool &lt;/a&gt;
</pre>
<p>
　　给这些元素设置了这个标志之后，我们就可以使用~来定位这些标签了。</p>
<pre title="">/* Target data-info attr that contains the value "external" */
a[data-info~="external"] {
color: red;
}

/* And which contain the value "image" */
a[data-info~="image"] {
border: 1px solid black;
}
</pre>
<h2 id="17">
　17. X:checked</h2>
<pre title="">input[type=radio]:checked {
border: 1px solid black;
}
</pre>
<p>
　　上面这个伪类写法可以定位那些被选中的单选框和多选框，就是这么简单。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/checked.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="18">
　18. X:after</h2>
<p>
　　before和after这俩伪类。好像每天大家都能找到使用它们的创造性方法。它们会在被选中的标签周围生成一些内容。<br>
当使用.clear-fix技巧时许多属性都是第一次被使用到里面的。</p>
<pre title="">.clearfix:after {
content: "";
display: block;
clear: both;
visibility: hidden;
            font-size: 0;
height: 0;
}

.clearfix {
    *display: inline-block;
_height: 1%;
}
</pre>
<p>
　　上面这段代码会在目标标签后面补上一段空白，然后将它清除。这个方法你一定得放你的聚宝盆里面。特别是当overflow:hidden方法不顶用的时候，这招就特别管用了。<br>
还想看其他创造性的使用这个伪类，看<a href="http://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-getting-clever-with-css3-shadows/">这里</a>。</p>
<blockquote>
<p>
根据CSS3标准规定，可以使用两个冒号`::`。然后为了兼容性，浏览器也会接受一个双引号的写法。其实在这个情况下，用一个冒号还是比较明智的。</p>
</blockquote>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE8+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="19">
　19. X::hover</h2>
<pre title="">div:hover {
background: #e3e3e3;
}
</pre>
<p>
　　不用说，大家肯定知道它。官方的说法是user action pseudo class.听起来有点儿迷糊，其实还好。如果想在用户鼠标飘过的地方涂点儿彩，那这个伪类写法可以办到。</p>
<blockquote>
<p>
注意旧版本的IE只会对加在锚点`a`标签上的`:hover`伪类起作用。</p>
</blockquote>
<p>
　　通常大家在鼠标飘过锚点链接时候加下边框的时候用到它。</p>
<pre title="">a:hover {
    border-bottom: 1px solid black;
}
</pre>
<blockquote>
<p>
专家提示：border-bottom:1px solid black;比text-decoration:underline;要好看很多。</p>
</blockquote>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+(IE6只能在锚点标签上起作用)</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="20">
　20. X:not(selector)</h2>
<pre title="">div:not(#container) {
color: blue;
}
</pre>
<p>
　　取反伪类是相当有用的，假设我们要把除id为container之外的所有div标签都选中。那上面那么代码就可以做到。</p>
<p>
　　或者说我想选中所有出段落标签之外的所有标签。</p>
<pre title="">*:not(p) {
color: green;
}
</pre>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/not.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="21">
　21. X::pseudoElement</h2>
<pre title="">p::first-line {
    font-weight: bold;
    font-size:1.2em;
}
</pre>
<p>
　　我们可以使用::来选中某标签的部分内容，如地一段，或者是第一个字没有。但是记得必须使用在块式标签上才起作用。</p>
<blockquote>
<p>
伪标签是由两个冒号`::`组成的。</p>
</blockquote>
<p>
　　定位第一个字</p>
<pre title="">p::first-letter {
float: left;
       font-size: 2em;
       font-weight: bold;
       font-family: cursive;
       padding-right: 2px;
}
</pre>
<p>
　　上面这段代码会找到页面上所有段落，并且指定为每一段的第一个字。</p>
<p>
　　它通常在一些新闻报刊内容的重点突出会使用到。</p>
<p>
<storng>　　定位某段的第一行</storng></p>
<pre title="">p::first-line {
    font-weight: bold;
    font-size: 1.2em;
}
</pre>
<p>
　　跟::first-line相似，会选中段落的第一行 。</p>
<p>
　　为了兼容性，之前旧版浏览器也会兼容单冒号的写法，例如:first-line,:first-letter,:before,:after.但是这个兼容对新介绍的特性不起作用。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/pseudoElements.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE6+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="22">
　22. X:nth-child(n)</h2>
<pre title="">li:nth-child(3) {
color: red;
}
</pre>
<p>
　　还记得我们面对如何取到推跌式标签的第几个元素是无处下手的时光么，有了nth-child那日子就一去不复返了。</p>
<p>
　　请注意nth-child接受一个整形参数，然后它不是从0开始的。如果你想获取第二个元素那么你传的值就是li:nth-child(2).</p>
<p>
　　我们甚至可以获取到由变量名定义的个数个子标签。例如我们可以用li:nth-child(4n)去每隔3个元素获取一次标签。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/nth.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
</ul>
<h2 id="23">
　23. X:nth-last-child(n)</h2>
<pre title="">li:nth-last-child(2) {
color: red;
}
</pre>
<p>
　　假设你在一个ul标签中有N多的元素，而你只想获取最后三个元素，甚至是这样li:nth-child(397)，你可以用nth-last-child伪类去代替它。</p>
<p>
　　这个技巧可以很正确的代替第16个TIP，不同的就是它是从结尾处开始的，倒回去的。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/nthLast.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="24">
　24. X:nth-of-type(n)</h2>
<pre title="">ul:nth-of-type(3) {
border: 1px solid black;
}
</pre>
<p>
　　曾几何时，我们不想去选择子节点，而是想根据元素的类型来进行选择。</p>
<p>
　　想象一下有5个ul标签。如果你只想对其中的第三个进行修饰，而且你也不想使用id属性，那你就可以使用nth-of-type(n)伪类来实现了，上面的那个代码，只有第三个ul标签会被设置边框。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/nthOfType.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
</ul>
<h2 id="25">
　25. X:nth-last-of-type(n)</h2>
<pre title="">ul:nth-last-of-type(3) {
border: 1px solid black;
}
</pre>
<p>
　　同样，也可以类似的使用nth-last-of-type来倒序的获取标签。</p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="26">
　26. X:first-child</h2>
<pre title="">ul li:first-child {
    border-top: none;
}
</pre>
<p>
　　这个结构性的伪类可以选择到第一个子标签，你会经常使用它来取出第一个和最后一个的边框。</p>
<p>
　　假设有个列表，没个标签都有上下边框，那么效果就是第一个和最后一个就会看起来有点奇怪。这时候就可以使用这个伪类来处理这种情况了。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstChild.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE7+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="27">
　27. X:last-child</h2>
<pre title="">ul &gt; li:last-child {
color: green;
}
</pre>
<p>
　　跟first-child相反，last-child取的是父标签的最后一个标签。</p>
<p>
　　例如标签</p>
<pre title="">&lt;ul&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;li&gt; List Item &lt;/li&gt;
&lt;/ul&gt;
</pre>
<pre title="">ul {
width: 200px;
background: #292929;
color: white;
       list-style: none;
       padding-left: 0;
}

li {
padding: 10px;
         border-bottom: 1px solid black;
         border-top: 1px solid #3c3c3c;
}
</pre>
<p>
　　上面的代码将设置背景色，移除浏览器默认的内边距，为每个li设置边框以凸显一定的深度。</p>
<style type="text/css">
.demo27 {
width: 200px;
background: #292929;
color: white;
       list-style: none;
       padding-left: 0;
}
.demo27-li {
padding: 10px;
         border-bottom: 1px solid black;
         border-top: 1px solid #3c3c3c;
}</style>
<ul>
<li>
List Item</li>
<li>
List Item</li>
<li>
List Item</li>
</ul>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstChild.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="28">
　28. X:only-child</h2>
<pre title="">div p:only-child {
color: red;
}
</pre>
<p>
　　说实话，你会发现你几乎都不会用到这个伪类。然而，它是可用的，有会需要它的。</p>
<p>
　　它允许你获取到那些只有一个子标签的父标签。就像上面那段代码，只有一个段落标签的div才被着色。</p>
<pre title="">&lt;div&gt;&lt;p&gt; My paragraph here. &lt;/p&gt;&lt;/div&gt;

&lt;div&gt;
&lt;p&gt; Two paragraphs total. &lt;/p&gt;
&lt;p&gt; Two paragraphs total. &lt;/p&gt;
&lt;/div&gt;
</pre>
<p>
　　上面例子中，第二个div不会被选中。一旦第一个div有了多个子段落，那这个就不再起作用了。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/onlyChild.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="29">
　29. X:only-of-type</h2>
<pre title="">li:only-of-type {
    font-weight: bold;
}
</pre>
<p>
　　结构性伪类可以用的很聪明。它会定位某标签只有一个子标签的目标。设想你想获取到只有一个子标签的ul标签？</p>
<p>
　　使用ul li会选中所有li标签。这时候就要使用only-of-type了。</p>
<pre title="">ul &gt; li:only-of-type {
    font-weight: bold;
}
</pre>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/onlyOfType.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox 3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="30">
　30. X:first-of-type</h2>
<p>
　　first-of-type伪类可以选择指定标签的第一个兄弟标签。</p>
<p>
　　<strong>测试</strong></p>
<pre title="">&lt;div&gt;
&lt;p&gt; My paragraph here. &lt;/p&gt;
&lt;ul&gt;
&lt;li&gt; List Item 1 &lt;/li&gt;
&lt;li&gt; List Item 2 &lt;/li&gt;
&lt;/ul&gt;

&lt;ul&gt;
&lt;li&gt; List Item 3 &lt;/li&gt;
&lt;li&gt; List Item 4 &lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;
</pre>
<p>
　　来你把List Item 2取出来，如果你已经取出来或者是放弃了，来继续。</p>
<p>
<storng>　　<strong>解决办法1</strong></storng></p>
<p>
<storng>
</storng></p><p>
&nbsp;</p>
　　办法很多，我们看一些比较方便的。首先是first-of-type。<p></p>
<p>
&nbsp;</p>
<p>
&nbsp;</p>
<pre title="">ul:first-of-type &gt; li:nth-child(2) {
    font-weight: bold;
}
</pre>
<p>
　　找到第一个ul标签，然后找到直接子标签li，然后找到第二个子节点。</p>
<p>
　　<strong>解决办法2</strong></p>
<p>
　　另一个解决办法就是邻近选择器。</p>
<pre title="">p + ul li:last-child {
    font-weight: bold;
}
</pre>
<p>
　　这种情况下，找到p下的直接ul标签，然后找到它的最后一个直接子标签。</p>
<p>
　<strong>　解决办法3</strong></p>
<p>
　　我们可以随便玩耍这些选择器。来看看：</p>
<pre title="">ul:first-of-type li:nth-last-child(1) {
    font-weight: bold;
}
</pre>
<p>
　　先获取到页面上第一个ul标签，然后找到最后一个子标签。</p>
<p>
　　<a href="http://cdn.tutsplus.com/net/uploads/legacy/840_cssSelectors/selectors/firstOfType.html" target="_blank" title="DEMO">DEMO</a></p>
<p>
　　<strong>兼容性</strong></p>
<ul>
<li>
IE9+</li>
<li>
Firefox 3.5+</li>
<li>
Chrome</li>
<li>
Safari</li>
<li>
Opera</li>
</ul>
<h2 id="31">
　结论</h2>
<p>
　　如果你想向旧版本浏览器妥协，比如IE6，那你用这些新的选择器的时候还是得小心点。但别别让IE6阻止你去学这些新的技能。那你就对自己太残忍了。记得多查查<a href="http://www.quirksmode.org/css/contents.html">兼容性列表</a>，或者使用<a href="http://code.google.com/p/ie7-js/">Dean Edward’s excellent IE9.js script </a>来让你的浏览器具有这些特性。</p>
<p>
　　第二个，使用向jQuery的时候，尽量使用原生的CSS3选择器。可能 活让你的代码跑的很快。这样选择器引擎就可以使用浏览器原生解析器，而不是选择器自己的。</p>
<p>
　　英文原文：<a href="http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048" target="_blank">tutsplus</a></p>

</div>
