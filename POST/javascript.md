> 这是什么?
  最近想恶补一下关于javascript的基础知识
  权当一个记录笔记
  反正也不会有人看..

---

# 1.JavaScript 简介
## JavaScript简史
  Netscape：JavaScript

  Internet Explorer:JSscript

  ECMA:ECMAScript
## JavaScript的实现
- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

## 文档对象模型（DOM）

> Document Object Model:是针对XML但经过扩展用于HTML的应用程序编程接口。

- 为什么要使用DOM：通过DOM创建表示文档的树形图，开发人员获得了控制页面内容和结构的主动权，通过DOM提供的API，开发人员可以轻松自如地删除，添加，替换或修改任何节点
- 其他DOM标准：
    - SVG
    - MathML
    - SMIL

## 浏览器对象模型（BOM）
支持可以访问和操作浏览器窗口的浏览器对象模型（Browser Object Model）

---

# 2.在HTML中使用JavaScript

## script元素

定义了下列六个属性

- `async` 表示应该立即下载脚本，但不妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本
- `charset` 指定的代码的字符集
- `defer` 表示脚本可以延迟到文档完全被解析和显示之后再执行
- `language` 已经废弃
- `src` 表示包含要执行代码的外部文件
- `type` 表示编写代码使用的脚本语言的内容类型

### 使用的方式有两种
- 使用`<script>`元素嵌入，指定type属性
- 外部引用`<script type='text/javascript' src='example.js'></script>`
  - 不用在`<script></script>`中再嵌入代码，如果嵌入代码智慧下载并执行外部脚本文件，嵌入的代码会被忽略

### 标签的位置
- 放在`<head></head>`中：必须等到全部JavaScript代码都被解析和执行完成以后才能开始呈现页面的内容，这无疑会导致浏览器在呈现页面时出现明显的延迟 而延迟间的浏览器窗口中将是一片空白。
- 放在`<body>`的后面：在解析包含的javascript代码之前，页面的内容完全呈现在浏览器中，用户会因为浏览器窗口显示空白页面的时间缩短而感到打开的页面的速度加快了

## 将代码放入外部文件的优点:

- 可维护性：能够在不触及HTML标记的情况下集中精力编辑`javascript`代码
- 可缓存： 浏览器能够根据具体的设置缓存链接的所有外部文件，最终结果是加快页面加载的速度
- 适应未来：无须考虑蹩脚的XHTML或注释hack

## 文档模式

- 混杂模式
- 标准模式
- 准标准模式

在Html5中，对于文档类型已经统一，直接写法是`<!DOCTYPE html>`即可。

## `<noscript>`元素

支持JavaScript的平稳退化

    <noscript>
      <p>本页面需要浏览器支持javascript</p>
    </noscript>
---

# 3.基本概念

## 语法
### 区分大小写
变量`huybery`和`Huybery`是两个不同的变量
### 标识符

> 所谓标识符 就是指变量、函数、属性的名字，或者函数的参数。标识符可以按照下列格式规则组合起来的一或多个字符

- 第一个字符必须是字符，下划线_,或者一个美元字符（$）
- 其他字符可以是字母、下划线、美元符号或者数字

标识符中的字符也可以是扩展的ASCII或Unicode字母字符，但我们不推荐那样做

> 我们的标识符最好采用驼峰式大小写格式，也就是第一个字母小写，剩下的每个单词的首字母大写，例如`firstScend`,`myCar`,`doSomethingImportant`

### 注释

ECMAScript 使用C风格的注释，包括单行注释和块级注释。
- 单行注释以两个斜杠开头
`//单行注释`
- 块级注释以一个斜杠和一个星号开头
`/* hahaha`

### 严格模式
ECMAScript5引入`“use strict”`

### 语句

以一个分号结尾；如果省略分号，则由解析器确定语句的结尾

## 保留字和关键字
- 关键字：具有特殊用途
- 保留字：有可能在将来被用作关键字

## 变量
ECMAScript 的变量是松散类型的，所谓的松散类型就是可以用来保存任何类型的数据。定义变量时要用`var`操作符，后跟一个变量名。支持变量初始化。

    var name = "huybery";

## 数据类型
ECMAScript有5种简单数据类型

- Undefined
- Null
- Boolean
- Number
- String

还有1种复杂数据类型

- Object(本质上由一组无序的名值对组成)

### `typeof`操作符
一种手段来检测给定变量的数据类型，可返回的值如下

- `"undefined"` 这个值未定义
- `"Boolean"` 如果这个值是布尔值
- `"string"` 如果这个值是字符串
- `"number"` 如果这个值是数值
- `"object"` 如果这个值是对象或者null
- `"function"` 如果这个值是函数

> 特殊值`null`会被认为是一个空的对象，所以调用`typeof`操作符的时候会返回`object`

### Undefined 类型
未初始化的变量默认为`undefined`

    var message;
    alert(message == undefined); //true

奇怪的东东：
- 对于尚未声明的变量只能执行一项操作：使用`typeof`操作符检测其数据类型。
- 对于未声明的变量返回的值也是`undefined`

### Null 类型

null表示一个空对象指针，所以`typeof`返回的也是一个对象`object`.

undefined 值是派生自`null`的值，因此规定对他们的相等性测试要返回`true`。

### Boolean 类型
这个类型只有两个字面值`true`和`false`

可以对任何类型的值掉用`Boolean()`，而且总返回一个Boolean值，对于返回的是`true`还是`false`，要取决于转换值的数据类型及其实际值

### Number 类型
可以使用10，8，16 进制，在进行算数运算的时候，所有的8，16都将会转换为10进制。

- 浮点数值
 - 不失时机的转换为整数
 - 对于极大极小的数值，可以用e表示法，等于e前面的数值乘以10的指数此幂
 - 浮点数计算会有误差
- 数值范围
 - `Number.MAX_VALUE`
 - `Number.MIN_VALUE`
 - `Infinity`
- NaN：这个数值表示一个本来要返回数值的操作数未返回数值的情况
 - 任何设计NaN的操作都将返回NaN
 - NaN与任何值都不相等（包括NaN）
 - 针对这两个特点 定义了`isNaN()`函数，在接受到一个值后，会尝试将这个值转换为数值，而任何不能被转换为数值的值都会导致这个函数返回true.
- 数值转换
 - Number()
 - parseInt()
 - parseFloat()

### String 类型
用于表示由0或多个16位Unicode字符组成的字符序列

- 字符变量：包含一些特殊的字符字面量 也叫转义序列。任何字符串的长度都可以通过访问其`length`属性取得。
- 字符串的特点：ECMAScript的字符串是不可变的
- 转换为字符串：
  - `num.toString()` ; 可以添加一个参数为输出数值的基数，例如`num.toString(8)`
  - `String(num)`;如果不知道要转换的值是不是null或undefined的情况下，如果有`toString()`方法则调用，否则返回其本身
- 要把某个值转换为字符串，可以使用加法操作符与字符串`""`加在一起

### Object类型
对象其实就是一组数据和功能的集合，两种创建方式：

- `var o = new Object()`
- `new o = new Object`

## 操作符
包括算数操作符，位操作符，关系操作符和相等操作符

### 一元操作符
只能操作一个值的操作符叫做一元操作符

- 递增和递减操作符
- 一元加和减操作符

## 语句
### if 语句
`if(condition) statement1 else statement2`
### do-while 语句
    
    do{
    	statement
    }while(expression)

### while 语句
`while(expression) statement`

### for语句

`for (initialization;expression;post-loop-expression) statement`

### for-in 语句

`for (property in expression) statement`

for-in 循环输出的属性名的顺序是不可预测的，返回的先后次序可能会因浏览器而异

### label 语句

`label:statement`

使用label语句可以在代码还总添加标签，以便将来使用

### break和continue语句
break和continue语句于用在循环中准确地控制代码的执行，其中break语句会立即退出循环，强制执行循环后面的句子。而continue语句虽然也会立即退出循环，但退出循环后从循环的顶部继续执行。

### with语句
`with (expression) statement;`

with语句的作用是将代码的作用域设置到一个特定的对象中
例如下面语句

	var qs = location.search.substring(1)
	var hostName = location.hostname;
	var url = location.href;
	//上面几行代码都包含location对象，如果使用with语句，可以把上面的代码改写成如下所示：
	with(location){
		var qs = search.substring(1);
		var hostName = hostname;
		var url = href;
	}

在这个重写后的例子中，使用with语句关联了location对象，这意味着在with语句的代码块内部 每个变量首先被认为是一个局部变量 而如果在局部环境中找不到该变量的定义 就会查询location对象中是否有同名的属性。

> 由于大量使用with语句会导致性能下降 同时也会给调试代码造成困难 因此在开发大型应用时，不建议使用with语句

### switch 语句
和c基本一致 略。

## 函数

	function functionName(arg0,arg1,...,argN){
		statements
		return sth
	}


任何函数在任何时候都可以通过`return`语句后要返回的值来实现返回值。

### 理解参数
ECMAScript 函数不介意传递进来多少个参数 也不在乎传进来的参数是什么数据类型。

ECMAScript 中的参数在内部是用一个数组表示的。函数接收到的始终都是这个数组 而不关心数组中包含哪些参数

`arguments`对象可以使用`length`属性来确定传递进来多少个参数

> ECMAScript 中所有的参数传递都是值，不可能通过引用传递参数

### 没有重载

ECMAScript 函数不能像传统意义上那样实现重载

在其他语言中 可以为一个函数编写两个定义 只要这两个定义的签名（接受的参数的类型和数量）不同即可

> 通过检查传入函数中的参数的类型和数量并作出不同的反应 可以模仿方法的重载。

---

# 4.变量、作用域和内存问题		
## 基本类型和引用类型

基本类型值：简单的数据段

引用类型值：可能由多个值构成的对象

> javascript不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间

### 传递参数

ECMAScript 中所有的函数的参数都是按值传递的。在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量

> 可以把ECMAScript函数的参数想象成局部变量

### 检测类型

`result = variable instanceof constructor`

根据规定，所有引用类型的值都是Object实例，因此在检测一个引用类型值和Object构造函数时，`instanceof`操作符始终会返回false，因为基本类型不是对象。

## 执行环境及作用域

执行环境定义了变量或函数有权访问其他的数据，决定了它们各自的行为。

执行环境的类型总共就两种：全局和局部（函数）

每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。

当代码在一个环境执行时 会创建变量对象的一个作用域链。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。

### 延长作用域链
- `try-catch`语句的catch块
- `with`语句

### 没有块级作用域

- 声明变量
	如果初始化时没有用var声明，该变量会自动被添加

	> 在编写js代码的过程中，不声明而直接初始化变量是一个常见的错误做法，因为这样可能导致意外。我们建议在初始化变量之前，一定要先声明，这样就可以避免类似问题。在严格模式下，初始化未声明的变量会导致错误

- 查询标识符
	搜索过程从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符。如果在局部变量中找到，搜索过程停止

	如果在局部环境中没有找到该变量名，则沿作用域链向上搜索。搜索过程将一直追溯到全局环境的变量对象。如果在全局环境中也没有找到这个标识符，则意味着该变量尚未声明

	> 变量查询也不是没有代价的，很显然，访问局部变量要比访问全局变量更快，因为不用向上搜索作用域链。javascript引擎在优化标识符查询方面做得不错，因此这个差别在将来恐怕就可以忽略不计了。

## 垃圾收集

javascript 具有自动垃圾收集机制，也就是说，执行环境会负责管理代码执行过程中使用的内存。

这种垃圾收集机制的原理其实很简单：找出哪些不再继续使用的变量，然后释放其占用的内存。为此，垃圾收集器必须跟踪哪个变量有用 哪个变量没有用，对于不再有用的变量打上标记，以备将来收回其占用的内存。

### 标记清除

javascrip 中最常用的垃圾收集机制是标记清除。

可以使用任何方式来标记变量，比如可以通过翻转某个特殊的位来记录一个变量何时进入环境，或者使用一个“进入环境的”变量列表及一个“离开环境的”变量列表来跟踪哪个变量发生了变化。

### 引用计数

另一种不太常见的垃圾收集策略叫做引用计数：跟踪记录每个值引用的次数，当声明了一个变量并将一个引用类型值赋给该变量时，则这个值的引用次数就是1.如果同一个值又被赋给另一个变量。则这个值的引用次数加1.相反如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数减1.当这个值的引用次数变为0时，则说明没有办法再访问这个值了，因而就可以将其占用的内存空间回收回来。这样当垃圾收集器下次再运行时，它就会释放哪些引用次数薇0的值所占的内存。
- 弊端：循环引用（IE


### 管理内存

确保占用最少的内存可以让页面获得最好的性能，而优化内存占用的最佳方式，就是为执行代码只保存必要的数据。

一旦数据不再有用，最好通过将其设置薇`null`来释放其引用-这个做法叫做解除引用

> 解除一个值的引用并不意味着自动回收该值所占用的内存，解除引用的真正作用时让值脱离执行环境，以便垃圾收集器下次运行时将其回收。

---

# 引用类型
引用类型的值（对象）是引用类型的一个实例，引用类型是一种数据结构，用于将数据和功能组织在一起。它也通常被称为类，但这种称呼并不妥当。

尽管ECMAScript从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

> 虽然引用类型与类看起来相似，但它们并不是相同的概念

新对象是使用new 操作符后跟一个 构造函数 来创建的，构造函数本身就是一个函数，只不过该函数时出于创建新对象目的而定义的。

`var person = new Object()`

## Object类型

创建Object实例的方式有两种

- 第一种是new操作符后跟Object构造函数
	
	var person = new Object()
	person.name = 'huybery';
	person.age = 17;

- 第二种时使用对象字面量表示法，目的在于简化创建包含大量属性的对象的过程
	
	var person = {
		name:"huybery",
		age:17
	};

	//如果保留花括号则可以定义只包含默认属性和方法的对象，如下所示

	var person = {}
	person.name = 'huybery';
	person.age = 17;


一般来说 访问对象属性时都是点表示法，不过也可以使用方括号表示法来访问对象的属性

从功能上看 这两种访问对象属性的方法没有任何区别，但方括号语法的主要优点时可以通过变量来访问属性

	alert(person["name"]);
	alert(person.name);
	var propertyName = "name";
	alert(person[propertyName]);

## Array 类型

与其他语言不同 js数组的每一项可以保存任何类型的数据。

创建数组的基本方式有两种：

- 第一种是使用Array构造函数 

	var colors = new Array();
	var colors = new Array(20);
	var colors = new Array("red","blue","green");
	//也可以省略new操作符
	var colors = Array();
- 第二种方式时使用数组字面表示法

	var colors = ["red","blue","green"];
	var values = [1,2,3];

方括号中的索引表示要访问的值`colors[2]='black'`

数组的项数保存在其length属性中，这个属性会返回0或者更大的值

length属性很有特点，它不是只读的，因此通过设置这个属性，可以从数组的末尾移除项或向数组中添加新项。
	
	var colors = ["red","blue","green"];
	colors.length = 2;
	alert[colors[2]];  //undefined

利用这个属性可以方便地在数组末尾添加新项

	var colors = ["red","blue","green"];
	colors[colors.length] =  "black";

> 数组最多可以包含 4294967295 个项这几乎已经能够满足任何编程需求了，如果想添加的项数超过上限值，就会发生异常。而创建一个初始大小与这个上限值接近的数组，则可能会导致运行时间超长的脚本错误

### 检测数组

	if (Array.isArray(value)){
		//对数组执行某些操作
	}
	
### 转换方法

调用数组的`toString()`方法会返回由数组每个值的字符串形式拼接而成的一个以逗号分隔的字符串。

而调用`ValueOf()`返回的还是数组

`join()`方法接受一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串

	var colors = ["red","blue","green"];
	alert(colors.join('||'))

### 栈方法

`push()`方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度
`pop()`方法则从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。

### 队列方法

`shift()`移除数组中的第一个项并返回该项，同时将数组长度减1

结合`shift()`和`push()`方法，可以像使用队列一样使用数组

`unshift()`与`shift()`用途相反，结合`pop()`来模拟反向队列

### 重排序方法

	var values = [12,3,4,2,8]
	values.sort(compare)
	alert(values)
	function compare(value1, value2) {
        return value2-value1;
	}
	values.reverse();
	alert(values)

### 操作方法

`concat()` 创建当前数组一个副本，然后将接收到的参数添加到当前副本的末尾，最后返回新构建的数组。在没有给`concat()`方法传递参数的情况下，它只是复制当前数组并返回副本。

`slice()` 能够基于当前数组中的一或多个项创建一个新数组。
	
- 在只有一个参数的情况下，slice方法返回从该参数指定位置开始到当前末尾的所有项
- 如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项

> `slice()`方法不会影响原始数组

`splice()`主要用途时向数组的中部插入项

- 删除：可以删除任意数量的项，只需要制定2个参数：要删除的第一项的位置和要删除的项数。
	
	splice(0,2) 会删除数组中的前两项

- 插入：可以向指定位置插入任意数量的项，只需提供三个参数：起始位置，要删除的项数，要插入的项。如果要插入多个项，可以继续传入

	splice(2,0,"red","green")

- 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需要三个参数：起始位置，要删除的项数，要插入的任意数量的项，插入的项数不必与删除的项数相等。

	splice(2,1,"red","green")

splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项

### 位置方法

`indexOf()`从数组的开头开始向后查找

`lastIndexOf()`从数组的末尾开始向前查找

这两个方法都返回要查找的项在数组中的位置，或者在没有找到的情况下返回-1.

### 迭代方法

js数组定义了5个迭代方法，每个方法接受两个参数：要在每一项上运行的函数（函数中接受三个参数：数组项的值，该项在数组中的位置和数组对象本身），和运行该函数的作用域对象

- `every()`和`some()` :对数组中的每一项运行给定函数，前者如果全部返回True则返回True,后者只要有一项返回True 则返回True
- `filter()` 对数组中的每一项运行给定函数，返回True的项组成数组
- `forEach()` 对数组的每一项运行指定函数，没有返回值
- `map()`对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组

### 归并方法

`reduce()`和`reduceRight()`这两个方法都会迭代数组的所有项，然后构建一个最终返回值。前者从第一项开始，逐个遍历到最后。后者从数组的最后一项开始，向前遍历到第一项。

这两个方法接受两个参数：一个在每一项上调用的函数和作为归并基础的初始值。传给reduce()和reduceRight()的函数接受四个参数：前一个值，当前值，项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数时数组的第一项，第二个参数时数组的第二项。

使用`reduce()`方法额可以执行数组中所有和的操作

	var values = [1,2,3,4,5]
	var sum = values.reduce(function(prev, cur, index, array){
		return prev + cur;
		});
	alert(sum);

## Date 类型

使用自UTC 1970.1.1午夜开始经过的毫秒数来保存日期。

	var now = new Date();

在调用Date构造函数而不传递参数的情况下，新创建的对象自动获得当前日期和时间 如果想根据特定的日期和时间创建日期对象，必须传入表示该日期的毫秒数 为了简化这一计算过程 ECMAScript提供了两个方法：

- `Date.parse()` : 接受一个表示日期的字符串参数，然后尝试根据这个字符串返回相应日期的毫秒数
	
	var someDate = new Date(Date.parse("May 25,2004"));

- `Date.UTC()` : 也是接受一个字符串 参数分别薇年份，基于0的月份（一月是0,二月是1），月份中的哪一天，小时数，分钟，秒以及毫秒数

	car allFives = new Date(Date.UTC(2005,4,5,17,55,55))

ECMAScript添加了`Date.nao()`方法，返回表示调用这个方法时的日期和时间的毫秒数

	var start = Date.now();

## RegExp类型

js通过 `RegExp` 类型来支持正则表达式

	var expression = / pattern / flags ;

其中的模式部分可以时任何简单或复杂的正则表达式 可以包含字符类 限定符 分组 向前查找以及反向引用 ，每个正则表达式都可带有一或多个标志，用以标明正则表达式的行为。正则表达式的匹配模式支持下列3个标志：

- g:表示全局模式，即模式被应用于所有字符串，而非在发现第一个匹配项时立即停止
- i:表示不区分大小写模式，即在确定匹配项时忽略模式与字符串的大小写
- m：表示多行模式，即在到达一行文本末尾时还会继续查找下一行是否存在与模式匹配的项

### RegExp 实例方法

RegExp对象的主要方法时`exec()`,该方法是专门为捕获组而设计的。

`exec()`接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组;或者在没有匹配项的情况下返回Null

	var text = "mom and dad and baby";
	var pattern = /mom( and dad (and baby)?)?/gi;

	var matches = pattern.exec(text);

## Function 类型

函数实际上是对象

因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定

函数通常是使用`函数声明`语法定义的

	function sum(num1, num2){
		return num1 + num2
	};

这与下面使用`函数表达式`定义的函数的方式几乎相差无几

	var sum = function(num1,num2){
		return num1+num2
	};

要注意函数末尾有一个分号，就像声明其他变量时一样

最后一中定义函数的方式是使用 Function `构造函数`，Function构造函数可以接收任意数量的参数，但最后一个参数始终都被堪称函数体

	var sum = new Function("num1","num2","return num1 + num2");

上述的声明方法不推荐

### 函数声明与函数表达式

解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用;至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。


### 作为值的函数

要访问函数的指针而不执行函数的话，必须去掉函数名后面那对圆括号。

### 函数内部属性

在函数内部有两个特殊的对象：

- `arguments`:保留函数参数,这个对象还有一个名叫`callee`的属性，该属性是一个指针

	function factorial(num){
		if(num<=1){
			return 1;
		} else{
			return num*arguments.callee(num-1)
		}
	}

- `this`:this引用的是函数据以执行的环境对象-或者也可以说是this的值（当网页的全局作用域中调用函数时，this对象引用的就是window）

ECMAScript 5 也规范化了另一个函数对象的属性：`caller`，这个属性中保存着调用当前函数的函数的引用，如果实在全局作用域中调用当前函数，它的值未null。

	function outer(){
		inner();
	}

	function inner(){
		alert(inner.caller);
	}

	outer;

### 函数属性和方法

每个函数都包含两个属性

- `length`：表示函数希望接受的命名参数的个数
- `prototype`:不可枚举，for-in无法找到发现

每个函数都包含两个非继承而来的方法,这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内this对象的值

- `apply()`：接收两个参数，一个实在其中运行函数的作用域，另一个时参数数组。
- `call()` : 和apply基本相同，区别在于接受参数的方式不同，传递给函数的参数必须逐个列举出来
- `bind()`：这个方法会创建一个函数的实例，其this值会被绑定到传给`bind()`的值

它们真正强大的地方是能够扩充函数赖以运行的作用域

	function sum(num1, num2){
		return num1+num2;
	}

	function callsum1(num1, num2){
		return sum.apply(this, arguments);
	}

	function callsum2(num1, num2){
		retrun sum.apply(this, [num1, num2]]);
	}

	function callsum3(num1, num2){
		return sum.call(this, num1, num2);
	}

	alert(callsum1(10, 10));
	alert(callsum2(10, 10));
	alert(callsum3(10, 10));

	window.color = 'red';
	var o = {
		color : "blue"
	};

	function sayColor(){
		alert(this.color);
	}

	sayColor();

	sayColor.call(this);
	sayColor.call(window);
	sayColor.call(o);

	//bind()举例

	window.color = "red";
	var o = {
		color : "blue"
	};

	function sayColor(){
		alert(this.color)
	}

	var objectSayColor = sayColor.bind(o);
	objectSayColor();  //blue

## 基本包装类型

js提供了3个特殊的引用类型

- `Boolean`
- `Number`
- `String`

引用类型与基本包装类型的主要区别就是对象的生存期。

使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。

而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。这意味着我们不能在运行时为基本类型值添加属性和方法。

### Boolean 类型

建议永远不要使用 Boolean 对象

### Number 类型

- `toFixed()` 方法会按照指定的小数位返回数值的字符串表示（0-20位）
- `toExponential()` 方法返回以指数表示法
- `toPrecision()` 向上取整

### String 类型

- 字符方法

	- `charAt()`：以单字符字符串的形式返回给定位置的那个字符
	- `charCodeAt()`：得到的不是字符而是字符编码

- 字符串操作方法（都不会修改字符串本身）

	- `concat()`：用于将一或多个字符串拼接起来，返回拼接得到的新字符串
	- `slice()` : 返回从第一个参数到第二个参数间的字符，如果是负数，从右向左go。
	- `substr()` : 返回从第一个参数开始第二个参数个数的字符。如果是负数，第二个参数会变为0.
	- `substring()` : 与`slice()`相同。负数时返回全部字符串。

- 字符串位置方法
	
	- `indexOf()` 从头开始搜索字符串 找到匹配的字符返回字符的索引
	- `lastindexOf()` 从尾开始搜索字符串，找到匹配的字符返回字符的索引

二者可以接收第二个参数，意味着从某个位置开始搜索

- trim() 方法

这个方法会创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果

- 字符串大小写转换方法 

	- `toLowerCase()`
	- `toUpperCase()`

- 字符串的模式匹配方法

	- `match()` 方法只接受一个参数，要么时一个正则表达式，要么是一个RegExp对象
	- `search()` 返回字符串中第一个匹配项的索引
	- `replace()` 接受两个参数，然后第二个参数替换第一个参数在字符串中的第一个子字符串

## 单体内置对象

### Global 对象

 - URI编码方法
 - `eval()`:相当于一个完整的解析器
 - window 对象：在全局作用域中声明的变量和函数 都成为了window对象的属性

 ### Math 对象

 - `min()`和`max()`用于确定一组数值的最小值和最大值。这两个方法都可以接受任意个数值参数
 - `Math.ceil()` 向上舍入
 - `Math.round()` 四舍五入
 - `Math.floor()` 标准舍入
 - `random()` 返回大于等于0小于1的一个随机数
 - `selectForm()` 接受两个参数 应该返回的最小值和最大值

 