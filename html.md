# HTML代码规范

## 语言规范

  1. `doctype`声明使用`html5`。

    ```html
    <!doctype html>
    ```

  2. 统一页面编码格式为`utf-8` , `meta`标签`charset`设置为`utf-8`;

    ```html
    <meta charset="utf-8" />
    ```

  3. 标签、标签属性全部小写。

    **(√)**

    ```html
    <a href="/" data-attr="attr">Home</a>

    ```

    **(╳)**

    ```html
    <A HREF="/" attr="attr">Home</A>
    ```

  4. 所有html标签必须有结束符，`<img />`, `<col />`, `<base />`, `<link />`, `<meta />`, `<input />` 除外。

  5. 标签自定义属性使用`data-name="value"`的形式来写, 如果自定义属性特别多, 可以考虑使用标准 json 的方式去写: `data-json='{"a":"a", "b":"b"}'`。

    **(√)**

    ```html
    <div data-json='{"a":1, "b":true, "c":[1, 2]}' ></div>
    ```

    **(╳)**

    ```html
    <div data-json="{a:1, b:true, c:[1, 2]}" ></div>
    <!--对于这样的写法,直接JSON.parse会出错-->
    ```

  6. 对于 JS 钩子, 以 `jCamelCase` 的驼峰形式来命名。

  7. 对于普通`class`或者`id`命名（此处id仅做样式，不做js钩子）, 统一使用小写字母, 第一个字符必须为字母, 连接符用中划线 `-`。

    **(√)**

    ```html
    <div class="sns-box"></div>
    <div class="box"></div>
    ```

    **(╳)**

    ```html
    <div class="Sns-box"></div>  
    <div class="snsBox"></div>  
    <div class="Box"></div>
    ```

  8. css 引用置于头部`<head>`标签内。

  9. js 引用置于底部`</body>`标签前。

## 标签使用

  1. `<base>`标签必须放在`<head>`内。

  2. `<strong>`标签用于强调重要性, `<em>`标签用于表示内容的着重点。[参考](http://www.css88.com/archives/644)

  3. 当`link`元素用于引用CSS文档时, 默认`media`是`screen`, 如为特殊终端提供样式, 请指定`media`属性, 如`media=“print”`;

  4. `img`标签必须加`alt`，尤其是logo、商品图片等关键图片信息，对SEO友好。

## 注释规范

  1. 主要的`html`模块需加注释

  2. 修改别人代码时, 加入修改信息。至少加入修改者大名和修改时间。

    ```html
    <!--主要修改IE8浏览器兼容性问题 djune 2013-09-26 13:21 -->
    ```

## 3. HTML
尽量遵循 HTML 标准和语义，但是不要以牺牲实用性为代价。任何时候都要尽量使用最少的标签并保持最小的复杂度。
### 3.1 通用约定
#### 3.1.1 标签 (B)
-	自闭合（self-closing）标签，无需闭合 ( 例如： `<img>` `<input>` `<br>` `<hr>` 等 )
-	可选的闭合标签（closing tag），需闭合 ( 例如：`</li>` 或 `</body>` )
-	尽量减少标签数量

``` html
<img src="images/google.png" alt="Google">
<input type="text" name="title">
```

``` html
<ul>
  <li>Style</li>
  <li>Guide</li>
</ul>
```

``` html
<!-- Not recommended -->
<span class="avatar">
  <img src="...">
</span>

<!-- Recommended -->
<img class="avatar" src="...">
```

#### 3.1.2 Class 与 ID (A)
- class 应以功能或内容命名，不以表现形式命名
- class 与 id 单词字母小写，多个单词组成时，采用中划线-分隔
- 使用唯一的 id 作为 Javascript hook, 同时避免创建无样式信息的 class

``` html
<!-- Not recommended -->
<div class="j-hook left contentWrapper"></div>

<!-- Recommended -->
<div id="j-hook" class="sidebar content-wrapper"></div>
```

#### 3.1.3 属性顺序 (A)
HTML 属性应该按照特定的顺序出现以保证易读性。<br>
id > class > name >	data-xxx > src, for, type, href >	title > alt > aria-xxx > role
``` html
<a id="..." class="..." data-modal="toggle" href="###"></a>

<input class="form-control" type="text">

<img src="..." alt="...">
```
#### 3.1.4 引号 (A)
属性的定义，统一使用双引号。
``` html
<!-- Not recommended -->
<span id='j-hook' class=text>Google</span>

<!-- Recommended -->
<span id="j-hook" class="text">Google</span>
```

#### 3.1.5 嵌套 (A)
a 不允许嵌套 div 这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束，比如a 不允许嵌套 a。
严格嵌套约束在所有的浏览器下都不被允许；而语义嵌套约束，浏览器大多会容错处理，生成的文档树可能相互不太一样。
语义嵌套约束
-	`<li>` 用于 `<ul>` 或 `<ol>` 下；
-	`<dd>`, `<dt>` 用于 `<dl>` 下；
- `<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<td>` 用于 `<table>` 下；
严格嵌套约束
-	inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
-	`<a>`里不可以嵌套交互式元素`<a>、<button>、<select>`等;
-	`<p>`里不可以嵌套块级元素`<div>、<h1>~<h6>、<p>、<ul>/<ol>/<li>、<dl>/<dt>/<dd>、<form>`等。
更多详情，参考WEB标准系列-HTML元素嵌套
#### 3.1.6 布尔值属性 (A)
HTML5 规范中 disabled、checked、selected 等属性不用设置值。
``` html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

### 3.2 语义化
没有 CSS 的 HTML 是一个语义系统而不是 UI 系统。<br>
通常情况下，每个标签都是有语义的。<br>
此外语义化的 HTML 结构，有助于机器（搜索引擎）理解，另一方面多人协作时，能迅速了解开发者意图。<br>
#### 3.2.1 常见标签语义 (B)
 标签 | 语义 | 标签 | 语义 
 --- | --- | --- | --- 
 `<p>` | 段落 | `<h1> <h2> <h3>` |	标题
`<ul>` |	无序列表 | `<blockquote>`	|大段引用
`<ol>` |	有序列表 | `<cite>`	| 一般引用
`<b>`	| 为样式加粗而加粗 | `<i>` | 为样式倾斜而倾斜
`<strong>` | 为强调内容而加粗 | `<em>` | 为强调内容而倾斜
`<code>` | 代码标识 | `<abbr>` | 缩写

#### 3.2.2 示例 (B)
将你构建的页面当作一本书，将标签的语义对应的其功能和含义
-	书的名称：`<h1>`
-	书的每个章节标题: `<h2>`
-	章节内的文章标题: `<h3>`
-	小标题/副标题: `<h4> <h5> <h6>`
-	章节的段落: `<p>`

### 3.3 HEAD
#### 3.3.1 文档类型 (A)
为每个 HTML 页面的第一行添加标准模式（standard mode）的声明， 这样能够确保在每个浏览器中拥有一致的表现。
``` html
<!DOCTYPE html>
```

#### 3.3.2 语言属性 (C)
为什么使用 lang="zh-cmn-Hans" 而不是我们通常写的 lang="zh-CN" 呢? 请参考知乎上的讨论: 网页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"？
``` html
<!-- 中文（直接用这个就好了） --> 
<html lang="zh-Hans">

<!-- 简体中文 -->
<html lang="zh-cmn-Hans">

<!-- 繁体中文 -->
<html lang="zh-cmn-Hant">

<!-- English -->
<html lang="en">
```

#### 3.3.3 字符编码  (A)
- 以无 BOM 的 utf-8 编码作为文件格式
-	指定字符编码的 meta 必须是 head 的第一个直接子元素
``` html
<html>
  <head>
    <meta charset="utf-8">
    ......
  </head>
  <body>
    ......
  </body>
</html>
```

#### 3.3.4 IE 兼容模式 (A)
优先使用最新版本的IE 和 Chrome 内核
``` html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

#### 3.3.5 SEO 优化 (C)
``` html
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <!-- SEO -->
    <title>Style Guide</title>
    <meta name="keywords" content="your keywords">
    <meta name="description" content="your description">
    <meta name="author" content="author,email address">
</head>
```

#### 3.3.6 viewport (C)
-	viewport: 一般指的是浏览器窗口内容区的大小，不包含工具条、选项卡等内容
-	width: 浏览器宽度，输出设备中的页面可见区域宽度
-	device-width: 设备分辨率宽度，输出设备的屏幕可见宽度
-	initial-scale: 初始缩放比例
-	maximum-scale: 最大缩放比例

**当需要为移动端设备作优化，设置可见区域的宽度和初始缩放比例为必须项。**
``` html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
#### 3.3.7 iOS 图标 (B)
-	apple-touch-icon 图片自动处理成圆角和高光等效果
-	apple-touch-icon-precomposed 禁止系统自动添加效果，直接显示设计原图
``` html
<!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

<!-- iPad，72x72 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-72x72-precomposed.png" sizes="72x72">

<!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-114x114-precomposed.png" sizes="114x114">

<!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-144x144-precomposed.png" sizes="144x144">
```
#### 3.3.8 favicon (A)
在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保证 favicon 可访问，避免404，必须遵循以下两种方法之一：
-	在 Web Server 根目录放置 favicon.ico 文件
-	使用 link 指定 favicon
``` html
<link rel="shortcut icon" href="path/to/favicon.ico">
```

#### 3.3.9 HEAD 模板 (B)
``` html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <title>Style Guide</title>
    <meta name="description" content="不超过150个字符">
    <meta name="keywords" content="">
    <meta name="author" content="name, email@gmail.com">

    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- iOS 图标 -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png">

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" />
    <link rel="shortcut icon" href="path/to/favicon.ico">
</head>
```
## 其他注意

  1. 开发时页面原则上不内嵌`style`、`script`代码，如特殊情况请标明并注释。

  2. 缩进以4个空格为基本单位，为每个块级元素或表格元素标签新起一行，并且对每个子元素进行缩进。[参考](http://www.cnblogs.com/kungfupanda/archive/2012/09/05/2671597.html)