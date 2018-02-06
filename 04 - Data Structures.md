## 4. Data Structures
1. The list methods make it very easy to user a list as a stack ("last-in, first-out"). To add an item to the top of the stack, user `append()`. To retrieve an item from the top of the stack, use `pop()` witout an explicit index.<br/>
<font color=#3333FF>列表的方法使它可以容易地被当作堆使用（后进，先出）。使用`append()`方法，添加一个成员到堆顶。使用不带参数的`pop()`方法，从堆顶提取一个成员。</font>

	```python
	>>> stack = [3, 4, 5]
	>>> stack.append(6)
	>>> stack
	[3, 4, 5, 6]
	>>> stack.pop()
	6
	>>> stack
	[3, 4, 5]
	```
	
2. It is possible to use a list as a queue ("first-in, first-out"), however, lists are not efficient for the purpose. To implement a queue, use `collections.deque` which was designed to have fast appends and pops from both ends.<br/>
<font color=#3333FF>列表同样也可以被当作队列使用（先进，先出），但是，列表用于这个目的不是有效率的用法。为了实现队列，使用`collections.deque`，它是被设计为可以从两端快速地添加和弹出。</font>

	```python
	>>> from collections import deque
	>>> queue = deque(["Eric", "John", "Michael"])
	>>> queue.append("Terry")     # Terry arrives
	>>> queue.popleft()     # The first to arrive, now leaves
	'Eric'
	>>> queue     # Remaining queue in order of arrival
	deque(["John", "Michael", "Terry"])
	```
	
3. A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clause. The result will be a new list resulting from evaluating the expression in the context of the `for` and `if` clauses which follow it. **Note**, how the order of the `for` and `if` statements is the same in both these snippets. <br/><font color=#3333ff>列表推导式由方括号组成，括号中包含一个表达式和一个跟随的`for`子句，以及零个或多个`for`或`if`子句。推导式的结果是一个新的列表，列表中的成员由表达式在跟随其后的`for`和`if`子句的上下文语境中计算所得。**注意**，下列两端代码中`for`和`if`语句的顺序是相同的。</font>

	```python
	>>> [(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
	[(1, 3), (1,, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
	
	>>> combos = []
	>>> for i in [1, 2, 3]:
	... 	for y in [3, 1, 4]:
	... 		if x != y:
	... 			combos.append((x, y))
	>>> combos
	[(1, 3), (1,, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
	```
	
4. If the expression is a tuple, it must be parenthesized.<br/>
<font color=#3333ff>如果列表推导式中的表达式是一个元组，它必须使用括号包围。</font> 
	
	```python
	>>> [(x, x ** 2) for x in range(6)]     # Create a list of 2-tuple like (n, square)
	[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
	>>> [x, x ** 2 for x in range(6)]     # the tuple must be parenthesized
	SyntaxError: invalid syntax
	```
	
5. A tuple consists of a number of values seperated by commas. They may be input with or without surrounding parentheses, although often parentheses are nessary anyway.<br/>
<font color=#3333ff>元组是由一组逗号分隔的值组成。虽然括号通常是必须的，但它们也可以带上或者不带上括号输入。</font>

	```python
	>>> t = 12345, 54321, 'hello!'
	>>> t
	(12345, 54321, 'hello!')
	```
	
6. Tuples are **immutable**, and usually contain a heterogeneous sequence of elements that are accessed via unpacking or indexing. Lists are **mutable**, and their elements are usually homogeneous and are accessed by iterating over the list.<br/>
<font color=#3333ff>元组是**不可变**的，通常包含一个异类型的序列，而且通过拆封或索引来访问成员。列表是**可变**的，它的成员通常都是同类型的，并且可以在列表中遍历访问。</font>

7. A special problem is the construction fo tuples containing *0* or *1* items. Empty tuples are constructed by a empty pair of parentheses; a tuple with one item is constructed by following a value with a comma.<br/>
<font color=#3333ff>有一个特殊的问题是关于包含 *0*个或 *1*个成员的元组的构建。空元组是由一对空括号构建；只有一个成员的元组是由一个带有逗号的值构建的。</font>

	```python
	>>> empty = ()
	>>> singleton = 'hello',     # <- note trailing comma
	>>> len(empty)
	0
	>>> len(singleton)
	1
	>>> singleton
	('hello',)
	```
	
8. The statement `t = 12345, 54321, 'hello!'` is a example of **tuple packing**: the values are packed together in a tuple. The reverse operation is also possible. This is called, **sequence unpacking** and works for any sequence on the right-hand side. Sequence unpakcing requires that there are as many variables on the left-hand side of the equals sign as there are elements in the sequence.<br/>
<font color=#3333ff>语句`t = 12345, 54321, 'hello!'`是一个**元组封装**的示例：所有的值一起被封装进一个元组。反向操作也是可以的。这被称为**序列拆封**，对于右手边的任何序列都适用。序列拆封要求等号左侧的变量个数与右侧的系列中的成员个数一样多。</font>

	```python
	>>> t = 12345, 54321, 'hello!'
	>>> x, y, z = t
	>>> x
	12345
	>>> a, b, c, d = t
	Traceback...
	...
	ValueError: not enough values to unpack (expected 4, got 3)
	```
	
9. A set is an unordered collection with no duplicate elements. Basic uses include membership testing and eliminating duplicat entries. Curly braces and `set()` function can be used to create sets.<br/>
**Note**: to create an empty set you have to use `set()`, not `{}`; the latter creates an empty dictionary.<br/>
<font color=#3333ff>集合是一个没有重复数据的无序组。基本用于成员测试和消除重复实体。花括号和`set()`函数可以用于创建集合。<br/>
**注意**：创建一个空集合，你必须使用`set()`，而不是`{}`；后者创建的是一个空字典。</font>

	```python
	>>> basket= {'apple', 'oragne', 'apple', 'pear', 'orange', 'banana'}
	>>> print(basket)     # show that dupliates have been removed
	{'orange', 'banana', 'apple', 'pear'}
	>>> 'orange' in basket     # fast membership testing
	True
	>>> 'crabgrass' in basket
	False
	```
	
10. Similarly to list comprehensions, set comprehensions are also supported.<br/>
<font color=#3333ff>与列表推导式类似，也同样支持集合推导式。</font>

	```python
	>>> a = {x for x in 'abracadabra' if x not in 'abc'}
	>>> a
	{ 'r', 'd'}
	```
	
11. Unlike sequences, which are indexed by a range of numbers, dictionaries are indexed by keys, which can be any immutable type; strings and numbers can always be keys. Tuples can be used as keys if they contain only string, number or tuples; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key.<br/>
<font color=#3333ff>与使用数字作为索引的序列不同，字典使用键值作为索引，键值可以是任何不可变的类型；字符串和数字通常用于作为键值。元组如果只包含字符串、数字或元组也能用于作键值；如果一个元组包含了可变对象，无论是直接或者间接包含，都不能用于作键值。</font>

12. A pair of braces creates an empty dictionary: `{}`. Placing a comma-seperated list of key:value pair within the braces add initial key:value pairs to the dictionary; this is also the way dictionaries are written on output.<br/>
<font color=#3333ff>一对花括号创建一个空的字典：`{}`。在花括号内放置一个逗号分隔的键值对列表，可以为这个字典添加初始键值对，这也是字典在输出中的表示方式。</font>

	```python
	>>> tel = {'jack': 4098, 'sape': 4139}
	>>> tel['guido'] = 4127
	>>> tel
	{'sape': 4139, 'guido': 4127, 'jack': 4098}
	```
	
13. In addition, dict comprehensions can be used to create dictionaries from abitrary key and value expressions. When the keys are simple strings, it is sometimes easier to specify pairs using keyword arguments.<br/>
<font color=#3333ff>另外，字典推导式可以从任意的键和值表达式创建字典。当键值都是简单字符串是，有时可以用关键字参数来更简便地指定键值对。</font>
	
	```python
	>>> {x, x ** 2 for x in (2, 4, 6)}
	{2: 4, 4: 16, 6: 36}
	>>> dict(sape=4139, guido=4127, jack=4098)
	{'sape': 4139, 'guido': 4127, 'jack': 4098}
	```
	
14. When looping through dictionaries, the key and corresponding value can be retrieved at the same time using the `items()` method.<br/>
<font color=#3333ff>当在字典中循环是，使用`items()`方法可以将键值及其对应的值一同提取出来。</font>

	```python
	>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
	>>> for k, v in knights.items():
	... 	print(k, v)
	gallahad the pure
	robin the brave
	```
	
15. When looping through a sequence, the position index and corresponding value can be retrieved at the same time using the `enumerate()` function.<br/>
<font color=#3333ff>当在序列中循环时，使用`enumerate()`函数可以将位置索引和其对应的值一同提取出来。</font>

	```python
	>>> for i, v im enumerate(['tc', 'tac', 'toe'])
	... 	print(i, v)
	0 tc
	1 tac
	2 toe
	```
	
16. Comparisons can be chained. For example, `a < b == c` tests whether `a` is less than `b` and moreover `b` equals `c`. It is possible to assign the result of a comparison or other Boolean expression to a variable. **Note** that in Python, assignment cannot occur inside expressions.<br/>
<font color=#3333FF>比较是可以串联起来的。例如，`a < b == c`测试的是`a`是否小于`b`并且`b`等于`c`。可以把一个比较的结果或者布尔表达式赋值给一个变量。**注意**，在Python中，赋值不能发生在一个表达式内部的（内部不能有=）。</font>

	```python
	>>> string1, string2, string3 = '', 'Trondheirn', 'Hammer Dance'
	>>> non_null = string1 or string2 or string3
	>>> non_null
	'Trondheirn'
	```
	
17. **Note** that comparing objects of different types with `<` or `>` is legal provided that the objects have appropriate comparison methods. Otherwise, rather than providing an arbitrary ordering, the interpreter will raise a `TypeError` exception.<br/>
<font color=#3333ff>**注意**，不同类型的对象进行比较，如果它们有合适的比较方法的话，是合法的。否则，解释器宁可抛出一个`TypeError`的异常也不返回一个随意的排序。</font>

------
> * 本文英文内容摘抄至 [Python官网](https://docs.python.org/) 教程 [The Python Tutorial](https://docs.python.org/3/tutorial/) 中的 [Data Structures](https://docs.python.org/3/tutorial/datastructures.html) 章节。
> * 本文中文内容为本人翻译，我已经尽力了。

