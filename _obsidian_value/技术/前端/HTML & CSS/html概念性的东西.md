

HTML用于控制网页的结构，CSS用于控制网页的外观，而JavaScript控制着网页的行为。


HTML→CSS→JavaScript→jQuery→HTML5→CSS3→ES6→Vue.js→webpack→Node.js

```
在HTML中，一般来说，只有6个标签能放在head标签内。

（1）title标签
（2）meta标签
（3）link标签
（4）style标签
（5）script标签
（6）base标签
```

使用p标签会导致段落与段落之间有一定的间隙，而使用br标签则不会。



```
（1）粗体标签：strong、b
（2）斜体标签：i、em、cite
（3）上标标签：sup
（4）下标标签：sub
（5）中划线标签：s
（6）下划线标签：u
（7）大字号标签：big
（8）小字号标签：small
```

在HTML中，我们可以使用“hr标签”来实现一条水平线。hr，是horizon（水平线）的缩写。


```
在HTML中，常见的自闭合标签如下表所示。

表1 自闭合标签
标签	说明
<meta />	定义网页的信息（供搜索引擎查看）
<link />	引入“外部CSS文件”
<br />	换行标签
<hr />	水平线标签
<img />	图片标签
<input />	表单标签
```


```
块元素会独占一行，行内元素则不会

块元素	说明
h1~h6	标题元素
p	段落元素
div	div元素
hr	水平线
ol	有序列表
ul	无序列表
```


```
ol，即ordered list（有序列表）；li，即list（列表项）

在有序列表中，type属性取值如下表所示。

属性值	列表项符号
1	阿拉伯数字：1、2、3……
a	小写英文字母：a、b、c……
A	大写英文字母：A、B、C……
i	小写罗马数字：i、ii、iii……
I	大写罗马数字：I、II、III……
```

```
ul，即unordered list（无序列表）。li，即list（列表项）。

属性值	列表项符号
disc	实心圆●（默认值）
circle	空心圆○
square	正方形■
```

```
dl即definition list（定义列表）；dt即definition term（定义名词）；而dd即definition description（定义描述）。

<dl>
    <dt>名词</dt>
    <dd>描述</dd>
    ……
</dl>
```

```
（1）表格：table标签
（2）行：tr标签
（3）单元格：td标签

tr，指的是table row（表格行）；td，指的是table data cell（表格单元格）。

<td rowspan = "跨越的行数"></td>

<td colspan = "跨越的列数"></td>
```

```
位图：色彩表现丰富
矢量图：放大不失真

<img src="./img/072803185.jpg" alt="naruto" title="naruto">
```

```
<a href="链接地址" target="打开方式"></a>


a标签的target属性取值有4种，如下表所示。

表1 target属性取值
属性值	说明
_self	默认值，在原来窗口打开链接
_blank	在新窗口打开链接
_parent	在父窗口打开链接
_top	在顶层窗口打开超链接
```