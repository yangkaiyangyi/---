语言规范
---

## 语言规范

JavaScript 是一种客户端脚本语言，这里列出了编写 JavaScript 时需要遵守的规则。

### 类型

- 基本类型
  - 字符串
  - 数值
  - 布尔类型
  - null
  - undefined

  ```js
  const foo = 1
  let bar = foo

  bar = 9

  console.log(foo, bar) // 1, 9
  ```

- 复杂类型
  - object
  - array
  - function

  ```js
  const foo = [1, 2, 3]
  const bar = foo

  bar[0] = 9

  console.log(foo[0], bar[0]) // 9, 9
  ```

### 引用

`const` 和 `let` 都是块级作用域，`var` 是函数级作用域

- 对所有引用都使用 `const`，不要使用 `var`

  ```js
  // bad
  var a = 1
  var b = 2

  // good
  const a = 1
  const b = 2
  ```

- 如果引用是可变动的，则使用 `let`

  ```js
  // bad
  var count = 1
  if (count < 10) {
    count += 1
  }

  // good
  let count = 1
  if (count < 10) {
    count += 1
  }
  ```

### 对象

- 请使用字面量值创建对象

  ```js
  // bad
  const a = new Object{}

  // good
  const a = {}
  ```

- 别使用保留字作为对象的键值，这样在 IE8 下不会运行

  ```js
  // bad
  const a = {
    default: {},  // default 是保留字
    common: {}
  }

  // good
  const a = {
    defaults: {},
    common: {}
  }
  ```

- 请使用对象方法的简写方式

  ```js
  // bad
  const item = {
    value: 1,

    addValue: function (val) {
      return item.value + val
    }
  }

  // good
  const item = {
    value: 1,

    addValue(val) {
      return item.value + val
    }
  }
  ```

- 请使用对象属性值的简写方式

  ```js
  const job = 'FrontEnd'

  // bad
  const item = {
    job: job
  }

  // good
  const item = {
    job
  }
  ```

- 对象属性值的简写方式要和声明式的方式分组

  ```js
  const job = 'FrontEnd'
  const department = 'JDC'

  // bad
  const item = {
    sex: 'male',
    job,
    age: 25,
    department
  }

  // good
  const item = {
    job,
    department,
    sex: 'male',
    age: 25
  }
  ```

### 数组

- 请使用字面量值创建数组

  ```js
  // bad
  const items = new Array()

  // good
  const items = []
  ```

- 向数组中添加元素时，请使用 `push` 方法

  ```js
  const items = []

  // bad
  items[items.length] = 'test'

  // good
  items.push('test')
  ```

- 使用拓展运算符 `...` 复制数组

  ```js
  // bad
  const items = []
  const itemsCopy = []
  const len = items.length
  let i

  // bad
  for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i]
  }

  // good
  itemsCopy = [...items]
  ```

- 使用数组的 `map` 等方法时，请使用 `return` 声明，如果是单一声明语句的情况，可省略 `return`

  ```js
  // good
  [1, 2, 3].map(x => {
    const y = x + 1
    return x * y
  })

  // good
  [1, 2, 3].map(x => x + 1)

  // bad
  const flat = {}
  [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    const flatten = memo.concat(item)
    flat[index] = flatten
  })

  // good
  const flat = {}
  [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
    const flatten = memo.concat(item)
    flat[index] = flatten
    return flatten
  })

  // bad
  inbox.filter((msg) => {
    const { subject, author } = msg
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee'
    } else {
      return false
    }
  })

  // good
  inbox.filter((msg) => {
    const { subject, author } = msg
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee'
    }

    return false
  })
  ```

### 解构赋值

- 当需要使用对象的多个属性时，请使用解构赋值

  ```js
  // bad
  function getFullName (user) {
    const firstName = user.firstName
    const lastName = user.lastName

    return `${firstName} ${lastName}`
  }

  // good
  function getFullName (user) {
    const { firstName, lastName } = user

    return `${firstName} ${lastName}`
  }

  // better
  function getFullName ({ firstName, lastName }) {
    return `${firstName} ${lastName}`
  }
  ```

- 当需要使用数组的多个值时，请同样使用解构赋值

  ```js
  const arr = [1, 2, 3, 4]

  // bad
  const first = arr[0]
  const second = arr[1]

  // good
  const [first, second] = arr
  ```

- 函数需要回传多个值时，请使用对象的解构，而不是数组的解构

  ```js
  // bad
  function doSomething () {
    return [top, right, bottom, left]
  }

  // 如果是数组解构，那么在调用时就需要考虑数据的顺序
  const [top, xx, xxx, left] = doSomething()

  // good
  function doSomething () {
    return { top, right, bottom, left }
  }

  // 此时不需要考虑数据的顺序
  const { top, left } = doSomething()
  ```

### 字符串

- 字符串统一使用单引号的形式 `''`

  ```js
  // bad
  const department = "JDC"

  // good
  const department = 'JDC'
  ```

- 字符串太长的时候，请不要使用字符串连接符换行 `\`，而是使用 `+`

  ```js
  // bad
  const str = '恒企前端 恒企前端\
  恒企前端 恒企前端 恒企前端\
  恒企前端 恒企前端'
  // good
  const str = '恒企前端 恒企前端 恒企前端' +
    '恒企前端 恒企前端 恒企前端' +
    '恒企前端 恒企前端'
  ```

- 程序化生成字符串时，请使用模板字符串

  ```js
  const test = 'test'

  // bad
  const str = ['a', 'b', test].join()

  // bad
  const str = 'a' + 'b' + test

  // good
  const str = `ab${test}`
  ```

### 函数

  - 请使用函数声明，而不是函数表达式
  - 后者可以变量提升

  ```js
  // bad
  const foo = function () {
    // do something
  }

  // good
  function foo () {
    // do something
  }
  ```

- 不要在非函数代码块中声明函数(补充：尽量不要在非函数块中声明变量, 避免bug, 降低空间复杂度)

  ```js
  // bad
  if (isUse) {
    function test () {
      // do something
    }
  }

  // good
  let test
  if (isUse) {
    test = () => {
      // do something
    }
  }
  ```

- 不要使用 `arguments`，可以选择使用 `...`

  > `arguments` 只是一个类数组，而 `...` 是一个真正的数组

  ```js
  // bad
  function test () {
    const args = Array.prototype.slice.call(arguments)
    return args.join('')
  }

  // good
  function test (...args) {
    return args.join('')
  }
  ```

- 不要更改函数参数的值

  ```js
  // bad
  function test (opts) {
    opts = opts || {}
  }

  // good
  function test (opts = {}) {
    // ...
  }
  ```

### 原型

- 使用 `class`，避免直接操作 `prototype`

  ```js
  // bad
  function Queue (contents = []) {
    this._queue = [..contents]
  }
  Queue.prototype.pop = function () {
    const value = this._queue[0]
    this._queue.splice(0, 1)
    return value
  }

  // good
  class Queue {
    constructor (contents = []) {
      this._queue = [...contents]
    }

    pop () {
      const value = this._queue[0]
      this._queue.splice(0, 1)
      return value
    }
  }
  ```

### 模块

- 使用标准的 ES6 模块语法 `import` 和 `export`

  ```js
  // bad
  const util = require('./util')
  module.exports = util

  // good
  import Util from './util'
  export default Util

  // better
  import { Util } from './util'
  export default Util
  ```

- 不要使用 `import` 的通配符 `*`，这样可以确保你只有一个默认的 export

  ```js
  // bad
  import * as Util from './util'

  // good
  import Util from './util'
  ```

### 迭代器

- 不要使用 `iterators`

  ```js
  const numbers = [1, 2, 3, 4, 5]

  // bad
  let sum = 0
  for (let num of numbers) {
    sum += num
  }

  // good
  let sum = 0
  numbers.forEach(num => sum += num)

  // better
  const sum = numbers.reduce((total, num) => total + num, 0)
  ```

### 对象属性

- 使用 `.` 来访问对象属性

  ```js
  const joke = {
    name: 'haha',
    age: 28
  }

  // bad
  const name = joke['name']

  // good
  const name = joke.name
  ```

### 变量声明

- 声明变量时，请使用 `const`、`let` 关键字，如果没有写关键字，变量就会暴露在全局上下文中，这样很可能会和现有变量冲突，另外，也很难明确该变量的作用域是什么。这里推荐使用 `const` 来声明变量，我们需要避免全局命名空间的污染。

  ```js
  // bad
  demo = new Demo()

  // good
  const demo = new Demo()
  ```

- 将所有的 `const` 和 `let` 分组

  ```js
  // bad
  let a
  const b
  let c
  const d
  let e

  // good
  const b
  const d
  let a
  let c
  let e
  ```

### Hoisting

- `var` 存在变量提升的情况，即 `var` 声明会被提升至该作用域的顶部，但是他们的赋值并不会。而 `const` 和 `let` 并不存在这种情况，他们被赋予了 [Temporal Dead Zones, TDZ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)

  ```js
  function example () {
    console.log(notDefined)   // => throws a ReferenceError
  }

  function example () {
    console.log(declareButNotAssigned)  // => undefined
    var declaredButNotAssigned = true
  }

  function example () {
    let declaredButNotAssigned
    console.log(declaredButNotAssigned)   // => undefined
    declaredButNotAssigned = true
  }

  function example () {
    console.log(declaredButNotAssigned)   // => throws a ReferenceError
    console.log(typeof declaredButNotAssigned)  // => throws a ReferenceError
    const declaredButNotAssigned = true
  }
  ```

- 匿名函数的变量名会提升，但函数内容不会

  ```js
  function example () {
    console.log(anonymous)  // => undefined

    anonymous()

    var anonymous = function () {
      console.log('test')
    }
  }
  ```

- 命名的函数表达式的变量名会被提升，但函数名和函数函数内容并不会

  ```js
  function example() {
    console.log(named)  // => undefined

    named()   // => TypeError named is not a function

    superPower()  // => ReferenceError superPower is not defined

    var named = function superPower () {
      console.log('Flying')
    }
  }

  function example() {
    console.log(named)  // => undefined

    named()   // => TypeError named is not a function

    var named = function named () {
      console.log('named')
    }
  }
  ```

### 分号

- 我们遵循 `Standard` 的规范，不使用分号。

  > 关于应不应该使用分号的讨论有很多，本规范认为非必要的时候，应该不使用分号，好的 `JS` 程序员应该清楚场景下是一定要加分号的，相信你也是名好的开发者。

  ```js
  // bad
  const test = 'good';
  (function () {
    const str = 'hahaha';
  })()

  // good
  const test = 'good'
  ;(() => {
    const str = 'hahaha'
  })();
  ```

### 标准特性

为了代码的可移植性和兼容性，我们应该最大化的使用标准方法，例如优先使用 `string.charAt(3)` 而不是 `string[3]`

### eval()

由于 `eval` 方法比较 `evil`，所以我们约定禁止使用该方法

### with() {}

由于 `with` 方法会产生神奇的作用域，所以我们也是禁止使用该方法的

### for-in 循环

推荐使用 `for in` 语法，但是在对对象进行操作时，容易忘了检测 `hasOwnProperty(key)`，所以我们启用了 `ESLint` 的 `guard-for-in` 选项

> 对数组进行 `for in` 的时候，顺序是不固定的

### 修改内置对象的原型

不要修改内置对象，如 `Object` 和 `Array`


#### 5.1.5 True 和 False 布尔表达式  (B)
类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。
下面的布尔表达式都返回 false:
- null
-	undefined
-	'' 空字符串
-	0 数字0
但小心下面的, 可都返回 true:
-	'0' 字符串0
-	[] 空数组
-	{} 空对象

#### 5.1.6 不要在 Array 上使用 for-in 循环 (A)
for-in 循环只用于 object/map/hash 的遍历, 对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值。
``` js
// Not recommended
function printArray(arr) {
  for (var key in arr) {
    print(arr[key]);
  }
}

printArray([0,1,2,3]);  // This works.

var a = new Array(10);
printArray(a);  // This is wrong.

a = document.getElementsByTagName('*');
printArray(a);  // This is wrong.

a = [0,1,2,3];
a.buhu = 'wine';
printArray(a);  // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a);  // This is wrong again.

// Recommended
function printArray(arr) {
  var l = arr.length;
  for (var i = 0; i < l; i++) {
    print(arr[i]);
  }
}
```

#### 5.1.7 二元和三元操作符 (A)
操作符始终写在前一行, 以免分号的隐式插入产生预想不到的问题。
``` js
var x = a ? b : c;

var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

var z = a ?
        moreComplicatedB :
        moreComplicatedC;
```

. 操作符也是如此：
``` js
var x = foo.bar().
    doSomething().
    doSomethingElse();
```

#### 5.1.8 条件(三元)操作符 (?:) (B)
三元操作符用于替代 if 条件判断语句。
``` js
// Not recommended
if (val != 0) {
  return foo();
} else {
  return bar();
}

// Recommended
return val ? foo() : bar();
``` 

#### 5.1.9 && 和 || (B)
二元布尔操作符是可短路的, 只有在必要时才会计算到最后一项。
``` js
// Not recommended
function foo(opt_win) {
  var win;
  if (opt_win) {
    win = opt_win;
  } else {
    win = window;
  }
  // ...
}

if (node) {
  if (node.kids) {
    if (node.kids[index]) {
      foo(node.kids[index]);
    }
  }
}

// Recommended
function foo(opt_win) {
  var win = opt_win || window;
  // ...
}

var kid = node && node.kids && node.kids[index];
if (kid) {
  foo(kid);
}
``` 


## 5 JavaScript
### 5.1 通用约定
#### 5.1.1 注释 (B)
原则
- As short as possible（如无必要，勿增注释）：尽量提高代码本身的清晰性、可读性。
- As long as necessary（如有必要，尽量详尽）：合理的注释、空行排版等，可以让代码更易阅读、更具美感。

单行注释<br>
必须独占一行。// 后跟一个空格，缩进与下一行被注释说明的代码一致。

多行注释<br>
避免使用 /*...*/ 这样的多行注释。有多行注释内容时，使用多个单行注释。

函数/方法注释<br>
1.	函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识
2.	参数和返回值注释必须包含类型信息和说明
3.	当函数是内部函数，外部不可访问时，可以使用 @inner 标识

``` js
/**
 * 函数描述
 *
 * @param {string} p1 参数1的说明
 * @param {string} p2 参数2的说明，比较长
 *     那就换行了.
 * @param {number=} p3 参数3的说明（可选）
 * @return {Object} 返回值描述
 */
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}
```

文件注释<br>
文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息。如下:
``` js
/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@meizu.com (Firstname Lastname)
 * Copyright 2009 Meizu Inc. All Rights Reserved.
 */
```
#### 5.1.2 命名 (B)
变量，使用 Camel 命名法。
``` js
var loadingModules = {};
```

私有属性、变量和方法以下划线 _ 开头。
``` js
var _privateMethod = {};
```
**注：在Vue中使用下划线可能和Vue内置的属性、API方法冲突，可以用 `p_privateMethod` 代替**

常量，使用全部字母大写，单词间下划线分隔的命名方式。
``` js
var HTML_ENTITY = {};
```

函数，使用 Camel 命名法。函数的参数，使用 Camel 命名法。
``` js
function stringFormat(source) {}

function hear(theBells) {}
```

类，使用 Pascal 命名法。类的方法/属性，使用 Camel 命名法
``` js
function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}

TextNode.prototype.clone = function () {
    return this;
};
```

枚举变量 使用 Pascal 命名法。枚举的属性， 使用全部字母大写，单词间下划线分隔的命名方式。
``` js
var TargetState = {
    READING: 1,
    READED: 2,
    APPLIED: 3,
    READY: 4
};
```
由多个单词组成的 缩写词，在命名中，根据当前命名法和出现的位置，所有字母的大小写与首字母的大小写保持一致。
``` js
function XMLParser() {}

function insertHTML(element, html) {}

var httpRequest = new HTTPRequest();
```

#### 5.1.3 命名语法 (B)
类名，使用名词。
``` js
function Engine(options) {}
```
函数名，使用动宾短语。
``` js
function getStyle(element) {}
```
boolean 类型的变量使用 is 或 has 开头。
``` js
var isReady = false;

var hasMoreCommands = false;
``` 
Promise 对象用动宾短语的进行时表达。
``` js
var loadingData = ajax.get('url');

loadingData.then(callback);
```