## 3. More Control Flow Tools

1. The keyword '`elif`' is short for '`else if`', and is useful to avoid excessive indentation. An `if...elif...elif...` sequence is a substitute for the `switch` and `case` statements found in other language.<br/>
<font color=#3333FF>关键字“`elif`”是“`else if`”的简化版，它对于避免多余的缩进很有用处。一个`if...elif...elif...`序列是其它语言中`switch`和`case`语句的替代品。</font>
		
2. Python's `for` statement iterates over the item of any sequence (a list or a string), in the order that they appear in the sequence. If you need a modify the sequence you are iterating over while inside the loop, it is recommended that you first make a copy.<br/>
<font color=#3333FF>Python的`for`语句使用在序列中出现的顺序来遍历任意一个序列（一个列表或一个字符串）中的成员。如果你需要在循环中修改正在循环的序列，建议你先对序列做一个复制。</font>
	
	``` python
	>>> words = ['cat', 'window', 'defenstrate']     # Measure some strings
	>>> for w in words[:]     # Loop over a slice copy of the entire list
	...    if len(w) > 6:
	...        words.insert(0, w)
	>>> words
	['defenstrate', 'cat', 'window', 'defenstrate']
	```
	
3. It is possible to let the range start at another number, or to specify a different increment (even negative; sometimes this is called the 'step').<br/>
<font color=#3333FF>使用另外一个数字作为 *range* 的开始或者指定一个不同的增长量（甚至是负数；有时这被称为“步伐”）是可以的。</font>
	
	``` python
	range(5, 10)              # 5 through 9
	range(0, 10, 3)           # 0, 3, 6, 9
	range(-10, -100, -30)     # -10, -40, -70
	```

4. In many ways the object returned by `range()` hehaves as if it is a list, but in fact it isn't. It is an object which returns the successive items of the desired sequence when you iterate over it, but is doesn't really make the list. We say such an object is **iterable**.
<br/><font color=#3333FF>在通常情况下，`range()`返回的对象表现得仿佛它是一个列表，但实际上它不是。它是这样一个对象，当你遍历它是，它会返回你所希望的连续的序列的成员，但他没有实际的创建列表。我们称呼这样的对象为**可遍历的**。</font>
	
5. The function `list()`, it create list from iterables.<br/>
<font color=#3333FF>函数`list()`，它可以用可遍历的对象创建一个列表。</font>
	
	```python
	>>> list(range(5))
	[0, 1, 2, 3, 4]
	```
	
6. More precisely, all variables assignments in a function store the value in the local symbol table; whereas variable references first look in the local symbol table, then in the local symbol tables of encloseing functions, then in the global symbol table, and finally in the table of built-in names. Thus, global variables cannot be directly assigned a value within a function (unless named in a ```global``` statement), although they may be referenced.<br/>
<font color=#3333FF>更准确地说，在一个函数中所有变量的赋值都是存储在本地符号表中，然而变量的引用查找顺序是，首先在本地符号表查找，然后是包含此函数的本地符号表，再然后是全局符号表，最后是内置名称。所以，在函数中不能直接给全局变量赋值（除非使用`global`语句，**否则值会被认为赋值给本地变量**），虽然它们也被引用了。</font>
	
	```python
	>>> a = 1
	>>> def func():
	... 	a = 2
	... 	print('In func a is:', a)
	>>> a
	1
	>>> func()
	In func a is 2
	>>> a
	1
	```
	
7. A function definition introduces the function name in the current symbol table. The value of the function name has a type that is recognized by the interpreter as a *user-defined function*. The value can be assigned to another name which can then also be used as a function.<br/>
<font color=#3333FF>函数定义语句在当前符号表中引入函数名。函数名的值是一个被解释器识别为 *用户自定义函数* 的类型。这个值可以被赋给另外一个名字，它也可以当做是一个函数来使用。</font>
	
	```python
	>>> fib     # a function name which defined before
	<function fib at 10042ed0>
	>>> f = fib
	>>> f(100)
	0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89
	```
	
8. The `return` statement returns with a value from a function. `return` without expession argument returns `None`. Falling off the end of a function also return `None`.<br/>
<font color=#3333FF>`return`语句从函数中返回一个值。没有带表达式作参数的`return`返回`None`。离开函数结尾也返回`None`。</font>
	
9. The most useful form is to specify a default value for one or more arguments. The default values are evaluated at the point of function definition in the **defining** scope.<br/>
<font color=#3333FF>最有用的方式是为一个或多个参数指定默认值。默认值是在函数定义中的**定义**范围处被计算的。</font>
	
10. **IMPORTANT WARNING: The default value is evaluated only once.** This makes a difference when the default is a mutable object as a list, dictionary, or instance of most classes.
<br/><font color=#3333FF>**重要警示：默认值只会被计算一次。**当默认值是一个可以改变的对象，比如列表、字典、或大部分类的实例时，会有不同的表现。</font>
	
	```python
	>>> i = 5
	>>> def f(arg=i):
	... 	print(arg)
	>>> i = 6     # assign i to another value
	>>> f()
	5
	
	>>> from datetime import datetime
	>>> def print_time(now=datetime.now()):
	...		print(now.isoformat())
	>>> print_time()
	2018-02-02T23:00:58.122250
	>>> print_time()
	2018-02-02T23:00:58.122250     # the same with the before call.
	
	>>> def f(a, L=[]):
	... 	L.append(a)
	... 	return L
	>>> print(f(1))
	[1]
	>>> print(f(2))
	[1, 2]
	>>> print(f(3))
	[1, 2, 3]
	```
		
11. All the keyword arguments passed must match one of the arguments accepted by the function, and their order is not important. This also includes non-optional arguments. No argument may receive a value more than once.<br/>
<font color=#3333FF>所有传递的关键字参数必须与函数参数的其中之一匹配，而它们的顺序并不重要。这同样适用于必选参数。没有参数可以接收超过一次的传值。</font>
	
	```python
	>>> def function(a):
	...		pass
	>>> function(0, a=0)
	Traceback...
	...
	TypeError: function() got multiple values for keyword argument 'a'
	```
	
12. When a final formal parameter of the form `**name` is present, it receives a **dictonary** containing all keyword arugment except for those corresponding to a formal parameter. This may be combined with a formal parameters of the form `*name` which receives a **tuple** containing the postional arguments beyond the formal parameter list. `*name` must occur before `**name`.<br/>
<font color=#3333FF>当函数最后一个参数是以`**name`这种形式出现时，它接受一个容纳了除对应于正式参数以外的所有关键字参数的**字典**。同样，以`*name`形式出现的参数，将与正式参数组合，接受一个容纳了正式参数之后所有位置参数的**元组**。`*name`必须出现在`**name`之前。</font>
	
	```python
	>>> def cheeseshop(kind, *arguments, **keywords):
	... 	print(kind)
	... 	print(arguments)
	... 	print(keywords)	
	>>> cheeseshop('Limburger", "It's very runny, sir", "It's realy very, VERY runny, sir.",
	... 	shopkeeper="Michael Palim", client="John Cleese", sketch="cheese shop sketch")
	Limburger
	("It's very runny, sir", "It's realy very, VERY runny, sir.")
	{'shopkeeper': 'Michael Palim', 'client': 'John Cleese', 'sketch': 'cheese shop sketch'}
	```
	
13. The reverse situation occurs when the arguments are already in a list or tuple but need to be unpacked for a function call requiring seperate positional arguments. If they are not available seperately, write the function call with the `*` operator to **unpack** the arguments out of a list or tuple.<br/>
<font color=#3333FF>当参数已经在一个列表或元组中时，相反的情况出现了，需要把它们拆开为函数调用所需要的分离的位置参数。如果它们不能有效地分离， 书写函数调用时，使用`*`运算符把列表或元组中的参数**拆包**出来。</font>
	
	```python
	>>> list(range(3, 6))     # normal call with seperate arguments
	[3, 4, 5]
	>>> args = [3, 6]
	>>> list(range(*args))     # call with arguments unpacked from a list
	[3, 4, 5]
	```
	
14. In the same fashion, dictionaies can deliver keyword arguments with the `**` operator.
<br/><font color=#3333FF>同样的样式，字典也可以用`**`运算符来传递关键字参数。</font>
	
	```python
	>>> def parrot(voltage, state='a stiff', action='voom'):
	... 	print("-- This parrot wouldn't", action, end=' ')
	... 	print("if you put", voltage, "volts through it.", end=' ')
	... 	print("E's", state, "!")
	>>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
	>>> parrot(**d)
	-- This parrot wouldn't VOOM fi you put four million volts through it. E's bleedin' demised !
	```
	
15.  `Lambda` functions can be used wherever function ojbects are required. They are syntacitically restricted to a single expression. Like nested function definitions, `Lambda` functions can reference variables from the containing scope.<br/>
<font color=#3333FF>`Lambda`函数可以被用在任何需要函数对象的地方。它们在语法上被约束为单个表达式。和嵌套函数一样，`Lambda`函数也可以从被包含的的作用域范围内引用变量。</font>
	
	```python
	>>> def make_incrementor(n):
	... 	return lambda x: x + n
	>>> f = make_incrementor(42)
	>>> f(1)
	43
	>>> f(3)
	45
	```
	
16. Function annotations have no effect on anyother part of the function. Function annotations are completely optional metadata information about the types used by user-defined functions.<br/>
<font color=#3333FF>函数注解对于函数任何部分都不会有效果，它是一种完全可选的原型信息，关于用户兹定于函数的类型信息。</font>	  
	- Parameters annotations are defined by a colon after the parameter name, followed by an expression evaluating to the value of the annotation.
	- <font color=#3333FF>参数注解由参数后的冒号定义，紧跟着一个表达式，用于评估注解的值。</font>
	- Return annotations are defined by a literal `->`, followed by an expression, between the parameter list and the colon denoting the end of the `def` statement.
	- <font color=#3333FF>返回值注解由一个文本字符`->`定义，其后跟随一个表达式，它处于参数列表和表示`def`语句结束的某号之间。</font>
	
	```python
	>>> def f(ham: str, eggs: str='eggs') -> str:
	... 	print("Annotations:", f.__annotations__)
	... 	print("Arguments:", ham, eggs)
	... 	return ham + ' and ' + eggs
	```
	
------
> * 本文英文内容摘抄至 [Python官网](https://docs.python.org/) 教程 [The Python Tutorial](https://docs.python.org/3/tutorial/) 中的 [More Control Flow Tools](https://docs.python.org/3/tutorial/controlflow.html) 章节。
> * 本文中文内容为本人翻译，我已经尽力了。

