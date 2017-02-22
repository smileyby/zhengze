Js 正则表达式学习和总结
====================

> 新建正则表达式
> 
> * 方法一：直接量语法

```js
	var reg = /pattern/attribute;
```

> * 创建RegExp对象的语法

```js
	var reg = new RegExp(pattern, attributes);
```

> 参数说明：
> * 参数 pattern 是一个字符串，指定了正则表达式的魔石或其他正则表达式
> * 参数 attributes 是一个可选的字符串，包含属性 'g'、'i'和'm'，分别用于指定全局匹配、区分大小写的匹配和多行匹配。ECMAScript标准化之前，不支持 m 属性。如果 pattern 是正则表达式，而不是字符串，则省略改参数。
> 
> 两者的区别在于：
> * 采用直接量语法新建的正则表达式对象在代码编辑时就会产生，是平常开发模式中常用的方式；
> * 采用构造函数生成的正则对象要在代码运行时生成
> 
> 正则表达式使用：
> * 正则对象的方法是指这样使用的： RegExp对象.方法（字符串）
> * 字符串对象的方法是这样使用： 字符串。方法（RegExp对象）

### 正则对象的属性和方法

#### 属性
> * ignoreCase 返回布尔值，表示RegExp对象是否具有标志 i
> * global 返回布尔值，表示RegExp对象是否具有表示 g
> * multiline 返回布尔值，表示RegExp对象是否具有表示 m
> * lastIndex 一个整数，标识开始下一次匹配的字符位置
> * soure 返回正则表达式的原文本 （不包括反斜杠）
> * i 执行对大小写不敏感的匹配
> * g 执行全局匹配 （查找所有匹配而非在找到第一个匹配后停止）
> * m 执行多行匹配

#### 正则表达式作用
##### 验证
> 由于验证时，通常需要在前后加上 ^ 和 $,以匹配整个待验证字符串；
##### 搜索替换
> 搜索、替换时是否加上此限定规则更具搜索的需求而定，此外，也有可能在前后加上 \b 而不是 ^ 和 $

##### 字符类匹配

> * [...]查找方括号之间的任何字符
> * [^..]查找任何不在方括号之间的字符
> * [a-z]查找任何从小写a到小写z的字符
> * [A-Z]查找任何从大写A到大写Z的字符
> * [A-z]查找任何从大写A到小写z的字符
> * . 查找单个字符，除了换行和行结束符
> * \w 查找单词字符，等价于 [a-zA-Z0-9]
> * \W 查找非单词字符，等价于 [^a-zA-Z0-9]
> * \s 查找空白字符
> * \S 查找非空白字符
> * \d 查找数字，等价于[0-9]
> * \D 查找分数字字符，等价于[^0-9]
> * \b 匹配单词边界
> * \r 查找回车符
> * \t 查找制表符
> * \0 查找NULL字符
> * \n 查找换行符

##### 重复字符匹配

> * {n,m}匹配前一项至少n次，但不能超过m次
> * {n,}匹配前一项n次或更多次
> * {n}匹配前一项n次
> * n?匹配前一项0次或者1次，也就是说前一项是可选的，等价于{0,1}
> * n+匹配前一项一次或多次，等价于{1,}
> * n*匹配前一项0次或多次，等价于{0，}
> * n$匹配任何结尾为n的字符串
> * ^n匹配任何开头为n的字符串
> * ？=n匹配任何其后紧接指定字符串n的字符串
> * ?!n匹配任何其后没有紧接指定字符串n的字符串 

##### 匹配特定数字(看的我头晕死！！)

> * ^[1-9]\d*$ 匹配正整数
> * ^-[1-9]\d*$ 匹配负整数
> * ^-?[0-9]\d*$ 匹配整数
> * ^[1-9]\d*|0$ 匹配非负整数（正整数 + 0）
> * ^-[1-9]\d*|0$ 匹配非正整数（负整数 + 0）
> * ^[1-9]\d*.\d*|0.\d*[1-9]\d*$ 匹配正浮点数   
> * ^-([1-9]\d*.\d*|0.\d*[1-9]\d*)$ 匹配负浮点数
> * ^-?([1-9]\d*.\d*|0.\d*[1-9]\d*|0?.0+|0)$ 匹配浮点数
> * ^[1-9]\d*.\d*|0.\d*[1-9]\d*|0?.0+|0$ 匹配非负浮点数（正浮点数 + 0）
> * ^(-([1-9]\d*.\d*|0.\d*[1-9]\d*))|0?.0+|0$ 匹配非正浮点数（负浮点数 + 0）

##### 匹配特定字符串

> * ^[A-Za-z]+$ 匹配由26个英文字母组成的字符串
> * ^[A-Z]+$ 匹配由26个英文字母的大写组成的字符串
> * ^[a-z]+$ 匹配由26个英文字母的小写组成的字符串
> * ^[A-Za-z0-9]+$ 匹配由数字和26个英文字母组成的字符串
> * ^\w+$ 匹配由数字、26个英文字母或者下划线组成的字符串

### 方法

##### test方法

> * 检索字符串中指定的值。返回true或者false
> * 如果字符串string中含有与RegExpObject匹配的文本，则返回true，否则返回false

##### Demo1

> * 如果正则表达式带有g修饰符，则每一次test方法都从上一次匹配结束的位置开始匹配。
> * 使用了g修饰符的正则表达式，表示要记录每一次搜索的位置，直接使用test方法，每次开始搜索的位置都是上一次匹配的最后一个位置。

```html
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>test方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	        var reg = /abc/g;
	        var str = "123abc456abc";
	        console.log(reg.lastIndex);//0
	        console.log(reg.test(str));//true
	        console.log(reg.lastIndex);//6
	        console.log(reg.test(str));//true
	        console.log(reg.lastIndex);//12
	        console.log(reg.test(str));//false
	    </script>
	</body>
	</html>
	
```

##### Demo2

> 如果正则表达式使一个空字符串，则会匹配所有的字符串，但需要使用new RegExp()方式

```html

	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>test方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	        console.log(new RegExp('').test('abc'));//true
	        console.log(/''/.test('abc'));//false
	        console.log(/''/.test("''"));//true
	    </script>
	</body>
	</html>

```

#### exec方法

> * exec() 方法用于检索字符串中的正则表达式的匹配
> * 返回一个数组，其中存放匹配的结果。如果未找到，则返回值为null

##### Demo1

```html
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>exec方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	    var str = "xyz";
	    var reg1 = /x/;
	    var reg2 = /a/;
	    var res1 = reg1.exec(str);
	    var res2 = reg2.exec(str);
	    console.log(res1);//["x", index: 0, input: "xyz"]
	    console.log(res2);//null
	    </script>
	</body>
	</html>
	
```

##### Demo2

> 如果正则表达式包括圆括号，则返回的数组会包括多个元素。首先是整个匹配成功的结果，后面是圆括号匹配的结果，如果有多个圆括号，他们的匹配成功结果都会成为数组元素

```html
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>exec方法2</title>
	</head>
	<body>
	    <script type="text/javascript">
	    var str = 'abcdabc';
	    var reg = /(a)b(c)/;
	    var res = reg.exec(str);
	    console.log(res);//["abc", "a", "c", index: 0, input: "abcdabc"]
	    </script>
	</body>
	</html>

```

> 对于调用exec方法返回的数组具有以下两个属性
> * input 整个原待匹配的字符串
> * index 整个魔石匹配成功的开始位置

#### 支持正则表达式的String对象的方法

##### search方法

> * search方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的字符串。
> * 返回值： stringObject中第一个与regexp相匹配的子串的起始位置
> * 注释： 如果没有找到任何匹配的子串，则返回 -1（和indexOf方法类似）
> * search() 方法不执行全局匹配，它将忽略标志g。它同时忽略regexp 的 lastIndex属性，并且总是从字符串的开始进行检索，这意味着它总是返回 stringObject 的第一个匹配的位置。

##### Demo

```html
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>search方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	    var str = "abcdcef";
	    console.log(str.search(/c/g));//2
	     </script>
	</body>
	</html>
	
```

##### match 方法

> * match() 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。改方法类似indexOf()和lastIndexOf()，凡是它返回指定的值，而不是字符串的位置。
> * 字符串对象的match方法与正则对象的exec方法比较类似
> * 但是如果正则表达式带有g修饰符，那么match方法与exec方法就有差别
> * 可以看到match返回了所有成功匹配的结果，但是exec方法只返回了一个

##### Demo

```html

	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>match方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	    var str = "abcd";
	    var reg1 = /a/;
	    var reg2 = /x/;
	    console.log(str.match(reg1));//["a", index: 0, input: "abcd"]
	    console.log(str.match(reg2));//null
	
	    var str = "abcdabc";
	    var reg = /a/g;
	    console.log(str.match(reg));//["a", "a"]
	    console.log(reg.exec(str));//["a", index: 0, input: "abcdabc"]
	     </script>
	</body>
	</html>

```

##### replace方法

> * replace() 方法用于在字符串中用一些替换另一些字符，或者换一个与正则表达式匹配的子串
> * 返回值：一个新的字符串，使用replacement替换regexp的第一次匹配或所有匹配之后得到的
> * 字符串stringObject 的 replace() 方法执行的查找替换的操作。它将在stringObject中查找与regexp相匹配的子字符串，然后用replacement来替换这些子串。如果regexp具有全局标志g，那么replace() 方法将替换所有匹配的子串。否则，它只替换第一个匹配子串。

```html
	
	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <title>replace方法</title>
	</head>
	<body>
	    <script type="text/javascript">
	    var str = "xxx";
	    console.log(str.replace('x','y'));//yxx
	    console.log(str.replace(/x/,'y'));//yxx
	    console.log(str.replace(/x/g,'y'));//yyy
	     </script>
	</body>
	</html>
	
```

啦啦啦
=====



