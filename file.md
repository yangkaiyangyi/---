

# 前端开发规范
## 1. 规范目的
为了提高工作效率，便于后台人员添加功能及前端后期优化维护，输出高质量的文档，在平台建设中，使结构更加清晰，代码简明有序，有一个更好的前端架构。<br>
规范基本准则：符合web标准，使用具有语义的标签，使结构、表现、行为分离，兼容性优良。页面性能优化，代码简洁、明了、有序，尽可能的减少服务器的负载，保证最快的解析速度。

## 2. 基本原则
### 2.1 结构、样式、行为分离 (A)
确保文档和模板只包含 HTML 结构，样式都放到样式表里，行为都放到脚本里。
### 2.2 缩进 (A)
统一两个空格缩进（总之缩进统一即可），不要使用 Tab 或者 Tab、空格混搭（使用统一的代码编辑器并设置相同的编辑配置也可）。
### 2.3 文件编码 (A)
使用不带 BOM 的 UTF-8 编码。
- 在 HTML中指定编码 <meta charset="utf-8"> ；
-	无需使用 @charset 指定样式表的编码，它默认为 UTF-8 （参考 @charset）；
### 2.4 一律使用小写字母 (A)

``` html
<!-- Recommended -->
<img src="google.png" alt="Google">

<!-- Not recommended -->
<A HREF="/">Home</A>
```

``` css
/* Recommended */
color: #e5e5e5;

/* Not recommended */
color: #E5E5E5;
```

### 2.5 省略外链资源 URL 协议部分 (A)
省略外链资源（图片及其它媒体资源）URL 中的 http / https 协议，使 URL 成为相对地址，避免Mixed Content 问题，减小文件字节数。
其它协议（ftp 等）的 URL 不省略。

``` html
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

``` css
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}

/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
```




#### 5.1.4 接口命名规范 (B)
1. 可读性强，见名晓义；
2. 尽量不与 jQuery 社区已有的习惯冲突；
3. 尽量写全，不用缩写，除非是下面列表中约定的；（变量以表达清楚为目标，uglify 会完成压缩体积工作）

常用词	| 说明
 --- | ---
options	| 表示选项，与 jQuery 社区保持一致，不要用 config, opts 等
active | 表示当前，不要用 current 等
index	| 表示索引，不要用 idx 等
trigger	| 触点元素
triggerType |	触发类型、方式
context	| 表示传入的 this 对象
object | 推荐写全，不推荐简写为 o, obj 等
element	| 推荐写全，不推荐简写为 el, elem 等
length | 不要写成 len, l
prev | previous 的缩写
next | next 下一个
constructor	| 不能写成 ctor
easing | 表示动画平滑函数
min	| minimize的缩写
max	| maximize的缩写
DOM	| 不要写成 dom, Dom
.hbs | 使用 hbs 后缀表示模版
btn | button 的缩写
link | 超链接
title | 主要文本
img | 图片路径（img标签src属性）
dataset | html5 data-xxx 数据接口
theme | 主题
className | 类名
classNameSpace | class 命名空间





### 5.3 性能优化
#### 5.3.1 避免不必要的 DOM 操作 (B)
浏览器遍历 DOM 元素的代价是昂贵的。最简单优化 DOM 树查询的方案是，当一个元素出现多次时，将它保存在一个变量中，就避免多次查询 DOM 树了。
``` js
// Recommended
var myList = "";
var myListHTML = document.getElementById("myList").innerHTML;

for (var i = 0; i < 100; i++) {
  myList += "<span>" + i + "</span>";
}

myListHTML = myList;

// Not recommended
for (var i = 0; i < 100; i++) {
  document.getElementById("myList").innerHTML += "<span>" + i + "</span>";
}
```

#### 5.3.2 缓存数组长度  (C)
循环无疑是和 JavaScript 性能非常相关的一部分。通过存储数组的长度，可以有效避免每次循环重新计算。
注: 虽然现代浏览器引擎会自动优化这个过程，但是不要忘记还有旧的浏览器。
``` js
var arr = new Array(1000),
    len, i;
// Recommended - size is calculated only 1 time and then stored
for (i = 0, len = arr.length; i < len; i++) {

}

// Not recommended - size needs to be recalculated 1000 times
for (i = 0; i < arr.length; i++) {

}
```
#### 5.3.3 异步加载第三方内容  (A)
当你无法保证嵌入第三方内容比如 Youtube 视频或者一个 like/tweet 按钮可以正常工作的时候，你需要考虑用异步加载这些代码，避免阻塞整个页面加载。
``` js
(function() {

    var script,
        scripts = document.getElementsByTagName('script')[0];

    function load(url) {
      script = document.createElement('script');
      script.async = true;
      script.src = url;
      scripts.parentNode.insertBefore(script, scripts);
    }

    load('//apis.google.com/js/plusone.js');
    load('//platform.twitter.com/widgets.js');
    load('//s.widgetsite.com/widget.js');

}());
```



