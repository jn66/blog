# 第一章 Javascript简介
##Javascript实现
- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

##ECMA-262
- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
- 对象

##文档对象模型
针对XML但经过扩展用于HTML的应用程序变成接口API。把整个页面映射为一个多层节点结构。提供访问和操作网页的方法和接口。
- DOM1映射文档结构
- DOM2
 - DOM视图(Vidws)
 - DOM事件(Events)
 - DOM样式(Style)
 - DOM遍历和范围(Traversal and Range)
- DOM3加载文档的方法、验证文档的方法

##浏览器对象模型
提供与浏览器交互的方法和接口。

# 第二章 在HTML中使用JavaScript
引入外部javascript, 标签之间不能再添加额外的内容。否则不执行。
```html
<script type="text/javascript" src="abc.js"></script>
```
defer属性，脚本延迟到整个页面解析完再执行。每个标签按顺序执行。
async属性，不能保证按先后顺序执行。
charset属性，字符集。

script内嵌文件中出现的内容要\转义。

外部文件的优点：

- 可维护
- 可缓存
- 适应未来

noscript元素
当浏览器不支持JavaScript的时候，显示noscript元素中的内容。“需要启用JavaScript”

所有script元素都会按照他们做页面中出现的先后顺序依次被解析。在不使用defer和async的情况下，只有在解析完前面script元素中的代码之后，才会开始解析后面script中的代码。一般放在文档的后面 。
使用defer属性可以 让脚本在文档完全呈现之后再执行，延迟脚本总是按照指定他们的顺序执行。
使用async属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。

#第三章 基本概念
##语法
- 区分大小写
- 标识符：第一个字符必须是字母、下划线、美元符号，其他字符可以是字母、下划线、美元符号、数字。可以包含ASCII和Unicode字符，驼峰大小写格式。
- 注释 // 单行注释  /****多行注释****/
- 严格模式：不确定的行为得到处理，不安全的行为抛出错误，"use strict" 可以在顶部添加代码，也可以在指定函数下添加。
- 语句：结尾分号不是必须，但推荐使用。控制语句多行使用代码块，建议始终使用。

##关键字和保留字
不一一列举了。

##变量
松散型变量可以保存任何数据
var message; //undefined
var message="hi";
如果在**函数中**var定义一个变量，退出函数后会销毁。如果函数中不用var直接使用，全局变量退出后还能使用。
可以用逗号创建多个变量var message=1 , go="haha", age=29;

##数据类型
基本数据类型 undefined，Null，Bollean，Number，String
复杂数据类型 Object

###typeof操作符
- undefined 未定义
- boolean 布尔值
- string 字符串
- number 数值
- object 对象或者*null*
- function 函数

###instanceof检测对象
person instanceof Array

###undefined类型
声明变量但是没有初始化。没有必要显式的声明。
var message;
alert(message); //undefined
alert(age); //产生错误

但是他们typeof都能输出undefined。

###Null类型
空对象类型 typeof 返回object
未来使用空变量，初始化为null。
null == undefined //ture

###Boolean 类型
在使用if的时候用于默认条件判断。 使用Boolean()进行转换
| 数据类型  | 转换为true的值     | 转换为false的值 |
| --------- | ------------------ | --------------- |
| Boolean   | true               | false           |
| String    | 非空字符串         | 空字符串        |
| Number    | 非零数字包括无穷大 | 0和NaN          |
| Object    | 任何对象           | null            |
| Undefined | 不使用             | undefined       |

###Number类型
八进制第一位是0，如果字面值中数值超出范围。那么前导0忽略。八进制在严格模式无效。
十进制前两位是0x。在进行算数计算时，所有的十六进制和八进制被转换为十进制。
isFinite(123) 判断是否无限大
没有小数部分的浮点数，会转换为整数。
1.2e7
1.2e-7
浮点数表示法

最大能表示的数值 Number.MAX_VALUE
最小能表示的数值 Number.MIN_VALUE
0除以0返回NaN，NaN和任何数值都不相等，包括本身。使用isNaN(123)--false，isNaN(NaN)当然返回true，不能转换为数值的，也会返回true。isNaN("10")就是false，isNaN(true)  可以被转换成数值1，也是false。isNaN("blue")不能转换成数值，是false。

Number()数值转换规则

- 布尔值，转换为0和1
- 数字，简单传入返回
- null，返回0
- undefined，返回NaN
- 字符串，遵循以下规则。
 - 如果只含数字，转换为十进制数字，前导0忽略
 - 如果含浮点格式，转换为浮点数值
 - 如果包含有效的十六进制字符，转换成十进制数字
 - 如果字符串是空的，转换为0
 - 除上述之外，转换为NaN
- 如果是对象，调用valueOf()方法，依照前面的规则返回的数值进行返回。如果结果是NaN，则调用对象的toString()方法，再依照前面进行返回。

parseInt()函数
找到第一个非空字符进行转换，如果第一个字符不是数字，返回NaN。因此，转换空字符串会返回NaN。而Number会返回0.第二个参数可以是基数。"22.5"返回22，小数点不是有效的数字字符。

parseFloat 函数
从第一个字符开始解析每个字符。一直解析到字符串末尾。或者解析遇见一个无效的浮点数字字符为止。第二个小数点无效。

###String类型
字符字面量
\n \t \r 
每个字面量长度是1
字符串不可变，要改变字符串，只能销毁原来的。
toString()方法
返回字符字面量，能传递基数，但是null和undefined没有这个方法。如果想把null和undefined转换成字符串，使用String()转型函数、

###Object类型
var o = new Object()
每个实例都有下列属性和方法
- constructor 创建当前对象的函数
- hasOwnProperty 检查给定的属性在当前对象实例中是否存在
- isPrototypeOf 检查传入对象是否是传入对象的原型
- propertyIsEnumerable 检查给定对象能否使用for in语句
- toLocaleString() 返回对象字符串表示，与执行环境对应
- toString() 返回对象字符串表示
- valueOf() 返回对象字符串，数值，布尔值表示

##操作符
###一元操作符
递增和递减操作符，前置和后置。

- 包含有效数字字符的字符串，转换为数字后操作。
- 不包含有效数字的字符串，变量设置为NaN
- 布尔值转换为0和1再操作。
- 浮点数，执行加减1
- 对于对象，先调用valueOf方法，运用转换规则。如果结果是NaN，则调用toString()方法。

一元加减操作符。如果是非数值，用Number（）转换，如果是对象，先调用valueof和toString方法，然后再转换。

###位操作符
负数是二进制的补码，补码是反码+1.
按位非NOT 负值减1
按位与AND &
按位或OR |
按位异或 XOR ^ 相同为0 不同为1
左移 << 用0填充
右移 >> 用0填充

###布尔操作符
逻辑非! 
对象返回false，
空字符串返回true，
非空字符串返回false，
操作数0返回true，
非零返回false，
null返回true，
NaN返回true，
undefined返回true。
两个逻辑非，可以转换为布尔值。和Boolean() 相同

逻辑与&&

- 第一个操作数是对象，返回第二个操作数
- 第二个操作数是对象，只有在第一个求值结果是true情况下才返回该对象。
- 两个操作数都是对象，返回第二个操作数。
- 有一个操作数是null、NaN、undefined，则返回他
- 短路操作

逻辑或||
- 如果第一个操作数是对象，返回第一个操作数
- 如果第一个操作数的求值结果为false，则返回第二个操作数。
- 如果两个操作数都是对象，则返回第一个操作数
- 如果两个都是null、NaN、undefined。
- 短路操作

###乘性操作符
乘法*
- 如果操作符都是数值，按照常规乘法计算，超出范围变成无穷大。
- 有一个操作数是NaN，结果是NaN
- Infinity与0相乘，结果是NaN
- infinity与非0相乘，结果是infinity或者-infinity
- 两个Infinity相乘，返回Infinity
- 有一个操作数不是数值，调用Number()转换后，在执行上面的操作。

除法/
- 超过范围，结果是infinity或者-infinity
- 有一个操作符是NaN，返回NaN
- infinity除以infinity,返回NaN
- 0除以0，返回NaN
- 非零有限数被0除，结果是infinit或-Infinity
- 有一个操作数不是数值，后台调用Number()转换后，再用上面的规则。

求模%

- 数值返回正常值。
- 被除数无限大除数有限大，返回NaN
- 被除数有限大除数是0，返回NaN
- Infinity被Infinity除，结果是NaN
- 被除数有限大，除数无穷大，结果是被除数。
- 被除数是0，结果是0.
- 有一个操作数不是数值，调用Number（），再应用上述规则。


###加性操作符
加法
- 有一个操作符是NaN，结果就是NaN
- 两个正无穷相加或者两个负无穷相加，结果就是正无穷和负无穷。
- 正无穷和负无穷相加，结果是NaN
- 字符串相加，就拼接
- 一个是字符串，则将另一个转换为字符串，再拼接。
- 如果操作数是对象、数值、布尔值，调用他们的toString()取得相应字符串的数值，对于undefined和null，分别调用string()取得字符串undefined和null

减法

- 两个操作符都是数值，执行常规计算。
- 有一个是NaN，结果都是NaN
- Infinity-Infinity=NaN
- -Infinity- -infinity = NaN
- infinity--infinity=infinity
- -infinity-infinity=-infinity
- 0-0=0
- 0--0=-0
- -0--0=+0
- 如果一个操作数是字符串、布尔值、null、undefined，后台调用number()将转换为数值，再根据前面的规则执行减法计算。如果转换的结果是NaN，那么整个结果是NaN
- 如果有一个操作符是对象，调用valueOf取得对象的数值，如果得到的是NaN，则结果是NaN，如果没有valueOf方法，则调用toString()方法并得到字符串转换为数值。

###关系操作符
- 两个操作符都是数值，执行数值比较。
- 都是字符串，比较编码数值
- 如果一个操作数是数值，则将另一个操作数转换为一个数值进行比较。
- 如果一个操作数是对象，则调用这个对象的valueOf方法，用结果进行比较。如果没有，就调用toString方法。
- 如果一个操作数是布尔值，则现将其转换为数值，进行比较。
- 任何操作符和NaN比较，都是false。

###相等操作符
相等和不相等 先转换再比较
- 有一个操作数是布尔值，转为数值再比较。
- 一个是字符串，另一个是数值，比较相等这钱先将字符串转换为数值。
- 一个是对象另一个不是，调用valueOf方法，用得到的基本类型和前面的比较。
- null和undefined相等。不能将null和undefined转换为其他任何数值。
- 有一个操作数是NaN，相等操作符返回false，不相等返回true。NaN不等于NaN。
    NaN<3 false
    NaN>=3 false
- 两个操作数是对象，比较是否是同一个对象。

全等和不全等 仅比较不转换

###条件操作符
variable = bollean_expression ? true_value : false_value;

###赋值操作符
= += -= *=  /= %= <<= >>= >>>=

###逗号操作符
var num1=1,num2=2,num3=3;
var num=(2,4,5,6,7) //返回最后一个

##语句
if语句
```javascript
if(a>b){
    alert("aaa");
}else if(i<0){
    alert("aaa");
}else{
    alert("aaa");
}

if (condition) statement1 else statement2
```
do-while语句
```javascript
do{
    statement
}while(expression);
```
while语句
```javascript
while(expression) statement
```
for语句
```javascript
for (initialization; expression; post-loop-expression) statement
```
```javascript
for (;;;) statement 无限循环
```
for-in 语句
枚举对象属性,确认对象是不是或者undefined
```javascript
for (property in expression) statement
```

label语句
```javascript
label:statement
```

break和continue语句
可以返回标签

with语句
```javascript
with(expression) statement
with(location){
    var qs =  qs
    var hostname = hostname
}
var qs = location.qs
var hostname = location.qs
```
switch语句 每句要break
```javascript
switch(i){
    case 25:
        alert("25");
        break;
    case 35:
        alert("35");
        break;
    default:
        alert("other");
}
```
如果不写break，就会合并2个的情况。

##函数
```javascript

function functionName(arg0,arg1,...,argN){
    statements
}
```
return语句停止并立即退出，之后的语句不会执行。

ECMAScript函数不介意传递进来多少个参数，也不建议是什么数据类型。
arguments[0]可以获取第一个参数，并且时时保持同步。arguments.length确定传递进来多少参数。可以重写argument对应的值。如果没有赋值，那就是undefined。

###没有重载
后面的函数覆盖前面的

#第四章 变量、作用域和内存问题
##基本类型和引用类型
###动态属性
```javascript  
var person = new Object();
person.name = "abc";
alert(person.name); //"abc"

var name ="abc";
name.age =24;
alert(name.age); //undefied
```
不能给基本类型的数值添加属性。

### 复制变量值
基本类型的数值复制，两个变量相互独立。
引用类型对象复制，复制的为指针。

### 传递参数
所有函数的参数传递是按照数值传递。
```
function setName(obj){
    obj.name = "Nicholas";
    obj = new Object();
    obj.name = "Greg";
}

var person = new Object();
setName(person);
alert(person.name)   //"Nicholas"
```
内部的obj被赋予了其他的指针。

### 检测类型
基本类型使用 typeof
引用类型 result = variable instanceof constructor

##执行环境及作用域
在web浏览器中，全局执行环境是windows对象。
代码在环境中执行，会创建变量对象的作用域链。
内部环境可以通过作用域链访问外部环境，但是外部环境不能访问内部环境中的变量和函数。

##延长作用域链
try-catch语句的catch块
with语句
这两个语句都会在作用域链前端添加一个变量对象。对于with语句来说，会将指定的对象添加到作用域链中。对catch语句来说，会创建一个新的变量对象，其中包含的是被抛出的错误对象的生命。

##没有块级作用域
在括号内的if或者for的变量是全局变量，不是局部变量。
在函数内，var是局部，不添加var是全局
查询标识符，由内部到外部。找到这个变量。

##垃圾收集
**以后再说**标记清除、引用计数、性能问题、管理内存

#第五章引用类型
## Object 类型
创建对象
```javascript
var person = new Object()
//对象字面量表示法
var person = {
    name:"aaa";
    age:29
}
var person = {
    "name":"aaa";
    "age":29
}
//对象最后不能加逗号
var a = {} //与new Object()相同
```

访问属性
```javascript
person['name'] //可以用空格非数字，变量，关键字
person.name
```

## Array 类型
```javascript
var colors = new Array()
var colors = new Array(20) //预先知道长度
var colors = new Array("a","b","c") 
var colors = Array(3) //3项 
var colors = Array("aa")
var colors = Array(3) // 省略new 操作
var names = ['a','b'] //字面量法，
var names = [1,2,] //不要这样
var names = [,,,] //也不要这样
colors[0] //显示第0项，也可以修改，或者对新的项新增。
colors.length  //显示长度
colors[colors.length] = "a" //添加新项

value instanceof Array 检测数组，一个环境
Array.isArray(value) 确定到底是不是数组，不管哪个环境
```

###转换方法
array.valueof() 返回数组，对每一项toString
toLocaleString() 
toString() 返回数组每个值的字符串形式拼接而成的一个以逗号分隔的字符串
array.join("|")

###栈方法
后进先出LIFO(last in first out)
array.push(1,2,3)  返回修改后数组长度
array.pop() 返回移除的数组

###队列方法
先进先出FIFO(first-in-first-out)
array.push(1，2，3)
array.shift()

前进后出
array.pop()
array.unshift 

###重新排列方法
array.reverse() 反序
array.sort(function compare(value1,value2){return value2-value1})
```javascript
function compare(value1,value2){
    if(value1 < value2){
        return -1;
    }   else if (value1 > alue2){
        return 1;
    }   else    {
        return 0
    }
}
```

###操作方法
array.concat([a,b,c])组合成新数组,没有参数的时候，只是返回副本。
array.slice(1,3) 按照python那种方式提取数组，不会影响原始数组
array.splice(1,0,[1,2]) 删除、插入、替换数组

###位置方法
indexOf(4,4) 可以查找某个东西的位置，带参数从那个位置开始找。  
lastIndexOf()

###迭代方法

- every() 每项运行都运行函数，每一项都返回true，则返回true
- filter() 返回true的组成新数组
- forEach() 每一项运行给定函数，没有返回值
- map() 返回每次调用函数的结果
- some() 任何一项返回true，就返回true
function(item,index,array){
    return(item>2);
}

###归并方法
reduce() reduceRight()
```javascript
var values = [1,2,3,4,5]
var sum = values.reduce(function(prev,cur,index,array){
    return prev+cur
})
```

##DATE类型
var now = new Date() 创建日期当前对象，可传入1970.1.1的毫秒数
var someDate = new Date(Date.parse("May 25, 2005")) 按照日期格式转换
var someDate = new Date(Date.UTC(2005,4,5,17,55,55)) 按照0的基数
var start  = Date.now() 取得当前时间
valueOf返回毫秒表示，方便比较
toString和toLocalString 返回字符串

##RexExp类型
以后再说把

##Function类型
function sum(num1, num2){
   return num1 + num2
}
var sum =  function(num1,num2){
    return num1 + num2;
};
末尾分号
###没有重载

###函数声明与函数表达式
率先读取声明，读取到规定地方才读取表达式
function sum(sum1, sum2){}  //这是声明,函数声明提升
var sum = function (){}   //这是表达式

###作为值的函数
把一个函数作为另一个函数的结果返回.return function(){}

###函数内部属性
arguments 传入对象的所有参数
this 执行环境，在不同的环境表示
arguments.callee 是函数自己 比如阶乘可以用
caller 保存着调用当前函数的函数引用。
```javascript 
function outer(){
    inner()
}
function inner(){
    inner.caller;  //outer();
}
```
arguments.callee.caller 更松散的耦合

###函数的属性和方法
length 函数希望接收的命名参数的个数
prototype 属性，不可枚举，for-in无法发现
apply() 可以扩充作用域，在特定作用域中调用函数 
call() 与apply作用相同，区别是接受参数的方式不同，传递的参数必须枚举出来
```javascript
function sum(num1,num2){
    return num1+num2
}
function callSum1(num1,num2){
    return sum.apply(this,arguments);
}
function callSum2(num1,num2){
    return sum.apply(this,[num1,num2]);
}
function callSum3(num1,num2){
    return sum.call(this,num1,num2);
}
扩充作用域
window.color = "red"
var o = {color:blue}
function saycolor(){alert(this.color)}
saycolor.call(0)
```
bind() 绑定作用域
```javascript
window.color = "red"
var o ={color:"blue"}
function sayColor(){
    alert(this.color)
}
var objectSayColor  = sayColor.bind(o);
objectSayColor(); //blue 
```

##基本包装类型
```javascript
var s1 = "some text"
var s2 = s1.substring(2);

实际上完成的是以下操作
var s1 = new String("some text");
var s2 = s1.substring(2)
s1 = null
```

###Boolean类型
因为所有对象会转换成true，所以用处不大。
valueOf() 返回基本类型true和false
toString() 返回字符串true
typeof基本类型会返回boolean，引用类型返回object，理解引用关系非常重要。
永远不要使用Boolean 对象

###Number类型
var numberObject = new Number(10)
valueOf()返回基本类型的数值
toLocalString和toString返回字符串形式
num.toFix(2) 返回指定小数位，四舍五入
typeof基本类型返回number
typeof引用类型返回object

###String类型
valueOf toString toLocalString 返回字符串
使用toString用于将数值格式化为字符串方法

字符方法
stringValue.charAt(1) //访问指定位置
stringValue.charCodeAt(1) //访问指定位置的编码
stringValue[1]  //访问指定位置
操作方法
stringValue.concat("world") //字符串连接
slice substr substring //子字符串

indexOf  lastIndexOf //位置方法
trim() //删除空格
toLowerCase toUpperCase //大小写转换
match()  //接收正则表达式或者RegExp对象
search() //接收正则表达式或者REgExp对象 返回第一个匹配是索引
replace() //替换 可以用正则表达式
localeCompare()  //方法

##单体内置对象
###Golbal对象
URL编码方法
encodeURI() //整个URL编码，不会对本身属于URL字符编码冒号斜杠
encodeURLComponent() //对一段编码，对任何非标准字符编码。
decodeURL() 
decodeURLComponent() 解压

eval方法
解析语句

Golbal对象属性
各种类型，构造函数，错误，日期，regexp等

windows对象
访问Global对象，Web浏览器都是将这个全局对象作为windows对象实现。

###Math对象
底数，自然数，最大值，最小值，四舍五入，随机数

#第六章 面向对象的程序设计
```js
var person = new Object();
person.name = "abc";
person.sayName = function(){
    alert()
}

var person = {
    name:"abc",
    age:29.
    sayName:function(){
        alert(this.name);
    }
}
```
###属性类型
数据属性
[[Configurable]] 能否删除重新定义
[[Enumerable]] 能否通过for-in 循环返回属性
[[writable]]
[[Value]] 这个属性的数值

```js
Object.defineProperty(aaa,"name",{
	writable:false,
	value:"aaaa"
})
```

访问器属性
[[Configurable]] 能否删除重新定义
[[Enumerable]] 能否通过for-in 循环返回属性
[[get]]读取属性调用的函数
[[set]]写入属性调用的函数

aaa._age=87;

```js
Object.defineProperty(aaa,"age",{
	get:function(){
		return this._age;
	},
	set:function(newValue){
		this._age=newValue;
	}
})

aaa.age=88
alert(aaa.age)
```

定义多个属性
```javascript
var book={};
Object.defineproperties(book,{
    _year:{
        value:2004
    },
    edition:{
        value:1;
    }
}
)
```
读取属性的特性
Object.getOwnPropertyDescriptor(book,"year")
如果是访问属性，那么是configurable,enumerable,get,set
如果是数据属性，那这个对象属性有configurable\enumerable\writable和value
var descriptor = Object.getOwnPropertyDescriptor(book,"_year");
descriptor.value

##创建对象
###工厂模式
```js
function createObject(name,age,job){
	var person = new Object;
	person.name = name;
	person.age = age;
	person.job = job;
	person.sayName = function(){
		alert(this.name)
	}
	return person;
}
```
无法解决对象识别问题

###构造函数模式
```js
function Person(name,age,job){
	this.name=name;
	this.age=age;
	this.job=job;
	this.sayName = function(){
		alert(this.name);
	}
}
var person1= new Person("johnny",18,"workker")
```
没有显式创建对象，直接将属性和方法赋给this对象，没有return语句。构造函数要大写。
person1.constructor == Person  //true 
person1 instanceof Person //true
每次执行方法，都要重建一次。两个创造出来的sayname不相同。把函数移到外面，但是没有封装了。

###原型模式

```js
function Person(){}

Person.prototype.name = "Johnny"
Person.prototype.age = 20
Person.prototype.job = "Software Engineer"
Person.prototype.sayName = function(){
	alert (this.name);
}

var person1 = new Person()
person1.sayName();
var person2 = new Person()
person2.sayName();
alert(person1.sayName == person2.sayName); //true 

Person.prototype.isPrototypeOf(person1) //true
Object.getPrototypeOF(person1).name //"Johnny"
```
无法通过对象实例重写原型中的值，重写之后会给实例添加属性，却不能改写原型。使用delete删除属性，从而回复对原型的访问。使用person1.hasOwnProperty('name') 是否存在于实例中。

原型与in操作符
如果对象能通过原型或者实例访问到属性，in返回true。

确定是原型中的属性。
```js
function hasPrototypeProperty(object,name){
	return !object.hasOwnProperty(name) && (name in object);
}
```

使用for-in循环，返回的是所有能够通过对象访问的、可枚举属性，既包括存在于实例中的属性，也包括存在于对象中的属性。

原型简写
```js
function Person(){}
Person.prototype = {
    constrotor : Person,
	name:"abc", 
	sayName : function(){
		alert(this.name);
	}
}
Object.defineProperty(Person.prototype,"constructor",{
    enumerable:false,
    value:Person
}
);
```
取得对象上可枚举实例的属性
```js
var keys = Object.keys(Person.prototype);
alert(keys);  //"name,age,job,sayName"
```
取得所有实例的属性，无论是否可枚举
```js
Object.getOwnPropertyNames(Person.prototype);
```

要不然constructor无法确定对象类型。但是变成可枚举的enumerable。

更简单的原型语法
```js
function Person(){}
Person.prototype = {
    constructor:Person,
    name:"Nicho",
    
    age:18,
    sayName:function(){
        alert(this.name);
    }
};
```
这样从这里创建的新对象的constructor就不再指向Person了。所以要重写constructor.但是会导致constructor 的Enumerable特性被设置成true。

```js
Object.defineProperty(Person.prototype,"constructor",{
    enumerable:false,
    value:Person
})
```
原型的动态性
重写一个原型属性可以，但是重写整个原型会导致指向他的实例失去属性。

原型对象问题
没有传递参数，共享本性。

原型对象的问题
所有的实例在默认情况下都使用相同的属性。

##组合使用构造函数模式和原型模式。
```js
function Person(name, age, job){
	this.name = name;
	this.age=18
}
Person.prototype={
	constructor:Person,
	sayName:function(){
		alert(this.name);
	}
}
```
使用最广泛、认同度最高

###动态原型模式
```js
function Person(name,age,job){
	this.name = name;
	this.age = age;
	this.job = job;
	if (typeof this.sayName != "function"){
		Person.prototype.sayName = function(){
			alert(this.name);
		}
	}
}
```
不能使用对象字面量重写原型，会切断联系。


###寄生构造模式
先不看了

###稳妥构造模式
先不看了

##继承
```js
 function SuperType(){
	this.property = true;
}

SuperType.prototype.getSuperValue = function(){
	return this.property
}
function SubType(){
	this.subproperty = false
}

SubType.prototype = new SuperType();

SubType.prototype.getSubValue = function(){
	return this.subproperty;
}

var instance = new SubType();
alert(instance.getSuperValue())

//确定原型和实例的关系
instance instanceof Object
instance instanceof SuperType
instance instanceof SubType
Object.prototype.isPrototypeOf(instance)
SuperType.prototype.isPrototypeOf(instance)
SubType.prototype.isPrototypeOf(instance)
```

谨慎定义方法，覆盖方法，给原型添加方法一定要放在替换语句之后。
重写subtype会阻断与super之间的联系。
不能通过字面量添加新方法，这样会重写原型。
```js
SubType.prototype  = {
    getSubValue:function(){
        return this.subproperty;
    },
    
    someOtherMethod: function(){
        return false;
    }

}
```

问题1 ，引用类型的原型，原型会变成另一个类型的实例，实例对原型的修改，提现在了其他的实例上。在创建子类型的时候，不能向超类型的构造函数传递参数。

###借用构造函数？？？
function SuperType(name){
	this.color = [1,2,3,"name"]
}
function SubType(){
	SubType.call(this,"haha");
}
var instance1 = new SubType();
instance1.push("black")
var instance2 = new SubType();
instance2.color  //没有变化

可以传递参数.缺点都在构造函数中定义，无法重复使用，超类型中定义的方法，在子类型中不可见。

###组合继承？？？？
function SuperType(name){
	this.name = name;
	this.colors = ["red","blue","green"];
}
SuperType.prototype.sayName = function(){
	alert (this.name);
}
function SubType(name,age){
	SuperType.call(this,name);
	this.age = age;
}

SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
	alert(this.age);
}
var instance1 = new SubType("Nicholas",29);
instance1.color.push("black");
alert(instance1,colors); //四个颜色
instance1.sayName(); //nigulasi
instance1.sayAge(); //29

var instance1 = new SubType("aaa",28);
instance1.color.push("black");
alert(instance1,colors); //三个颜色
instance1.sayName(); //aaa
instance1.sayAge(); //28

既避免了原型链和借用构造函数的缺陷，又融合了有点，是最常用的继承模式。

###原型式继承
以后再说
###寄生式继承
以后再说
###寄生组合式继承
以后再说

#第七章 函数表达式
函数声明，函数声明提升。
函数表达式，类似于赋值语句。

##递归
arguments.callee 返回函数本身，多用于递归。

##闭包