### 5.2 jQuery 规范

#### 5.2.1 使用最新版本的 jQuery (C)
最新版本的 jQuery 会改进性能和增加新功能，若不是为了兼容旧浏览器，建议使用最新版本的 jQuery。以下是三条常见的 jQuery 语句，版本越新，性能越好：<br>
$('.elem')<br>
$('.elem', context)<br>
context.find('.elem')<br>
分别使用 1.4.2、1.4.4、1.6.2 三个版本测试浏览器在一秒内能够执行多少次，结果 1.6.2 版执行次数远超两个老版本。
#### 5.2.2 jQuery 变量 (A)
1.	存放 jQuery 对象的变量以 $ 开头；
2.	将 jQuery 选择器返回的对象缓存到本地变量中复用；
3.	使用驼峰命名变量；
``` js
var $myDiv = $("#myDiv");
$myDiv.click(function(){...});
```
#### 5.2.3	选择器 (B)
1.	尽可能的使用 ID 选择器，因为它会调用浏览器原生方法 document.getElementById 查找元素。当然直接使用原生 document.getElementById 方法性能会更好；
2.	在父元素中选择子元素使用 .find() 方法性能会更好, 因为 ID 选择器没有使用到 Sizzle 选择器引擎来查找元素；
``` js
// Not recommended
var $productIds = $("#products .class");

// Recommended
var $productIds = $("#products").find(".class");
```

#### 5.2.4	DOM 操作 (B)
1.	当要操作 DOM 元素的时候，尽量将其分离节点，操作结束后，再插入节点；
2.	使用字符串连接或 array.join 要比 .append()性能更好；
``` js
var $myList = $("#list-container > ul").detach();
//...a lot of complicated things on $myList
$myList.appendTo("#list-container");

// Not recommended
var $myList = $("#list");
for(var i = 0; i < 10000; i++){
    $myList.append("<li>"+i+"</li>");
}

// Recommended
var $myList = $("#list");
var list = "";
for(var i = 0; i < 10000; i++){
    list += "<li>"+i+"</li>";
}
$myList.html(list);

// Much to recommended
var array = [];
for(var i = 0; i < 10000; i++){
    array[i] = "<li>"+i+"</li>";
}
$myList.html(array.join(''));
```

#### 5.2.5 事件 (B)
1.	如果需要，对事件使用自定义的 namespace，这样容易解绑特定的事件，而不会影响到此 DOM 元素的其他事件监听；
2.	对 Ajax 加载的 DOM 元素绑定事件时尽量使用事件委托。事件委托允许在父元素绑定事件，子代元素可以响应事件，也包括 Ajax 加载后添加的子代元素；
``` js
$("#myLink").on("click.mySpecialClick", myEventHandler); //绑定mySpecialClick事件
$("#myLink").unbind("click.mySpecialClick"); //解绑mySpecialClick事件

// Not recommended
$("#list a").on("click", myClickHandler);

// Recommended
$("#list").on("click", "a", myClickHandler);
```

#### 5.2.6 链式写法 (B)
1.	尽量使用链式写法而不是用变量缓存或者多次调用选择器方法；
2.	当链式写法超过三次或者因为事件绑定变得复杂后，使用换行和缩进保持代码可读性；

``` js
$("#myDiv").addClass("error").show();
$("#myLink")
  .addClass("bold")
  .on("click", myClickHandler)
  .on("mouseover", myMouseOverHandler)
  .show();
```

#### 5.2.7 其他 (C)
1.	多个参数使用对象字面量存储；
2.	不要将 CSS 写在 jQuery 里面；
3.	正则表达式仅准用 .test() 和 .exec() 。不准用 "string".match() ；
