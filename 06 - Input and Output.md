## 6. Input and Output
1. How do you convert values to strings? Luckily, Python has ways to convert any value to a string: pass it to the `repr()` and `str()` functions. The `str()` function is meant to return representations of values which are fairly human-readable, which `repr()` is meant to generate representations which can be read by the interpreter.<br/>
<font color=#3333ff>如何将数值转换为字符串呢？幸运的是Python有办法把任意值转换为字符串，只需要将它传给`repr()`函数或者`str()`函数。`str()`函数意味着返回的数值表现形式相当于人类可读的，而`repr()`函数意味着产生的表现形式是可被解释器阅读的。</font> 

	```python
	>>> s = 'Hello world'
	>>> str(s)
	'Hello world'
	>>> repr(s)
	"'Hello world'"
	
	>>> # The repr() of a string adds string quotes and backslashes.
	>>> s2 = 'Hello\n'
	>>> str(s2)
	'Hello\n'
	>>> repr(s2)
	"'Hello\\n'"
	```
	
2. The method `str.rjust()` of string objects, which right-justifies a string in a field of a given width by padding it with spaces on the left. There are similar methods `str.ljust()` and `str.center()`.<br/>
<font color=#3333ff>字符串对象的`str.rjust()`方法是右对齐字符串，在左侧加入空白直至指定的宽度。类似的方法还有`str.ljust()`和`str.center`。</font>

	```python
	>>> for x in range(1, 6):
	... 	print(repr(x).rjust(2), repr(x * x).rjust(3), repr(x * x * x).rjust(4))
	 1   1    1
	 2   4    8
	 3   9   27
	 4  16   64
	 5  25  125
	```

3. There is another method, `str.zfill()`, which pads a numeric string on the left with zero. It understoods about plus and minus signs.<br/>
<font color=#3333ff>有另外一个方法，`str.zfill()`，它在一个数字字符串左侧加入前导零。它可以自己区分正、负符号。</font>

	```python
	>>> '12'.zfill(5)
	'00012'
	>>> '-3.14'.zfill(7)
	'-003.14'
	```
	
4. The backets and characters with them (called format field) are replaced with the objects passed into the `str.format()` method. A number in the brackets can be used to refer to the position of the object passed into the `str.format()` method. if keyword arguments are used in the `str.format()` method, their values are refer to by using the name of the argument. Position and keyword argument can be arbitrarily combined.<br/>
<font color=#3333ff>花括号与括号中的字符（称为格式符），将会被传入`str.format()`方法的对象替换。花括号中的数字用于表示传入`str.format()`方法的对象的位置。如果在`str.format()`方法中使用关键字，那么这些关键字表示传入同名参数的值。位置和关键字参数可以任意组合。</font>

	```python
	>>> print('{1} and {0}'.format('spam', 'eggs'))
	eggs and spam
	
	>>> print('This {food} is {adjective}.'.format(food='spam', adjective='absolutely horrible.'))
	This spam is absolutely horrible.
	
	>>> print('The story of {0}, {1} and {other}.'.format('Bill', 'Manfred', other='Georg'))
	The story of Bill, Manfred and Georg.
	```
	
5. '`!a`' (apply `ascii()`), '`!s`' (apply `str()`) and '`!r`' (apply `repr()`) can be used to convert the value before it is formatted.<br/>
<font color=#3333ff>'`!a`'（应用`ascii()`）,'`!s`'（应用`str()`）和'`!r`'（应用`repr()`）可以用于在数值被格式化之前转换它。</font>

	```python
	>>> content = 'elle'
	>>> print('My hovercraft is full of {}.'.format(content))
	My hovercraft is full of elle.
	>>> print('My hovercraft is full of {!r}.'.format(content))
	My hovercraft is full of 'elle'.
	```
	
6. An optional '`:`' and format specifier can follow the field name. This allows greater controll over how the value is formatted. Passing an integer after the '`:`' will cause that field to be a minimum number of characters wide.<br/>
<font color=#3333ff>一个可选的“`:`”和格式限定符可以跟在格式符后，这允许对数值被如何格式化做更多控制。在“`:`”后传入一个整数会导致数值格式化后字符串的长度达到其指定的最小字符宽度。</font>

	```python
	>>> table = {'Sjoerd': 4127, 'Jack': 4098}
	>>> for name, phone in table.items():
	... 	print('{0:10} ==> {1:10d}'.format(name, phone))
	Jack       ==>       4098
	Sjoerd     ==>       4127
	```
	
7. It would be nice if you could reference the variables to be formatted by name instead of by position. This can be done by simply passing the dict and using square brackets '`[]`' to access the keys. This could also be done by passing the table as keyword arguments with the '`**`' notation. This is particularly useful in combination withe the built-in function `vars()`, which returns a dictionary containing all local variables.<br/>
<font color=#3333ff>如果能使用被格式化的变量名称代替位置引入，那就好了。这是可以实现的，只需要简单的传入一个字典并使用方括号“`[]`”访问key就可以了。还可以这样实现，传入一个表格用“`**`”标记。这种方法结合内置函数`vars()`一起使用特别有用，函数会返回一个包含所有本地变量的字典。</font>

	```python
	>>> table = {'Sjoerd': 4127, 'Jack': 4098}
	>>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}'.format(table))
	Jack: 4098; Sjoerd: 4127
	
	>>> a, b = 123, 456
	>>> print('a: {a}; b: {b}'.format(**vars()))
	a: 123; b: 456
	```
	
8. In text mode, the default when reading is to convert platform-specific line endings (`\n` on Unix, `\r\n` on Windows) to just `\n`. When writing in text mode, the default is to convert occurrences of `\n` back to platform-specific line endings.<br/>
<font color=#3333ff>在文本模式下，默认是在读取时，将平台特定的行结束符（Unix的`\n`，Windows的`\r\n`）转换为`\n`。在文本模式下写入时，默认将`\n`变回平台特定的行结束符。</font>

9. It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using `with` is also much shorter than writing equivalent `try-finally` blocks.<br/>
<font color=#3333ff>在处理文件对象时，使用`with`关键字是好习惯。它的好处是即使某处抛出异常，在代码块结束后，文件都能被正确地关闭。使用`with`比书写同效的`try-finally`块更简洁。</font> 

	```python
	>>> with open('workfile') as f:
	... 	read_data = f.read()
	>>> f.closed
	True
	```
	
10. After a file object is closed, either by a `with` statement or by calling `f.close()`, attempt to use the file object will automatic fail.<br/>
<font color=#3333ff>在一个文件对象被关闭后，无论是使用`with`表达式或者调用`f.close()`，试图再次使用此对象将自动失败。</font>

	```python
	>>> f.close()
	>>> f.read()
	Traceback ...
	...
	ValueError: I/O operation on closed file.
	```
	
11. In the end of the file has been reached, `f.read()` will return an empty string (''). If `f.readline()` returns an empty string, the end of the file has been reached. while a blank line is represented by '`\n`', a string containing only a single newline.<br/>
<font color=#3333ff>如果到达文件结束处，`f.read()`将返回一个空字符串（''）。如果`f.readline()`返回一个空字符串，就是已到达文件结束处，一个空行将表现为’`\n`‘，一个只包含单个换行符的字符串。</font>

	```python
	>>> f.read()
	'This is the entire file.\n'
	>>> f.read()
	''
	
	>>> f.readline()
	'This is the first line of the file.\n'
	>>> f.readline()
	'Second line of the file.'
	>>> f.readline()
	''
	```
	
12. `f.write(string)` writes the content of *string* to the file, returning the number of characters written. Other types of objects need to be converted - either to a string (in text mode) or bytes object (in binary mode) - before writing them.<br/>
<font color=#3333ff>函数`f.write(string)`将一个*字符串*的内容写入文件，返回被写入的字符数量。其他类型的对象在被写入前需要转换为 - 无论转为一个字符串（文本模式）或转为字节对象（字节模式）。</font>

	```python
	>>> f.write('This is a test.\n')
	16
	>>> value = ('the answer', 42)
	>>> s = str(value)     # convert the tuple to string
	>>> f.write(s)     # write '("the answer", 42)'
	18
	```
	
13. `f.tell()` returns an integer giving the file object's current position in the file represented as number of bytes from the beginning of the file when in binary mode and an opaque number when in text mode.<br/>
<font color=#3333ff>函数`f.tell()`返回一个整数表示文件对象在文件中的当前位置。当在字节模式下，代表从文件开始处到当前位置的字节数，在文本模式下，代表不确定的数目。</font>

14. To change the file object's position, use `f.seek(offset, from_what)`. The position is computed from adding `offset` to a reference point; the reference point is selected by the `from_what` argument. A `from_what`value of **0** measures from the beginning of the file, **1** uses the current file position, and **2** uses the end of the file as the reference point. `from_what` can be omitted and defaults to 0.<br/>
<font color=#3333ff>为了改变文件对象的位置，使用`f.seek(offset, from_what)`。位置的计算方法是从参考点加上*偏差*；参考点是由`from_what`参数来选择。`from_what`的值为**0**，从文件开始处测量，使用**1**代表当前文件位置，使用**2**代表以文件结束处为参考点。缺省`from_what`的默认值为0。</font>

	```python
	>>> f = open('workfile', 'rb+')
	>>> f.write(b'0123456789abcdef')
	16
	>>> f.seek(5)     # Go to the 6th byte in the file
	5
	>>> f.read(1)
	b'5'
	>>> f.seek(-3, 2)     # Go to the 3rd byte before the end
	13
	>>> f.read(1)
	b'd'
	```
	
------
> * 本文英文内容摘抄至 [Python官网](https://docs.python.org/) 教程 [The Python Tutorial](https://docs.python.org/3/tutorial/) 中的 [Input and Output](https://docs.python.org/3/tutorial/inputoutput.html) 章节。
> * 本文中文内容为本人翻译，我已经尽力了。

 

	