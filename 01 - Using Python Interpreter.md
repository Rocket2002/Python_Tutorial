## 1. Using Python Interpreter

1. Perhaps the quickest check to see whether command line editing is supported is type `Control-P` to the first Python prompt you get. If it beeps, you have command line editing. If nothing appears to happend, or if `^p` is echo, command line editing isn't available, you'll only be able to use backspace to remove characters from the current line.<br/>
<font color=#3333ff>也许检查是否支持“命令行编辑”的最快方法是，在你的第一个Python提示符后键入`Control-P`。如果听见“哔”，那么支持“命令行编辑”。如果什么都没有发生或者显示`^p`，那么不支持“命令行编辑”，你只能使用退格来删除当前命令行的字符。</font>

2. Typing an end-of-file character（`Control-D` on Unix, `Control-Z` on Windows）at the primary prompt causes the interpreter to exit with a zero status. If that doesn't work, you can exit the interpreter by typing the following command: `quit()`.<br/>
<font color=#3333ff>在主提示符后键入“文件结束符”（Unix中为`Control-D`, Windows中为`Control-Z`）将导致解释器以“零状态”退出（正常退出）。如果这样做不起作用，你可以键入命令`quit()`来退出解释器。</font>

3. When known to the interpreter, the scripts name and additional arguments thereafter are turned into a list of strings and assigned to the `argv` variable in the `sys` module. The length of the list is at least one; when no script and no arguments are given, `sys.argv[0]` is an empty string.<br/>
<font color=#3333ff>当解释器知道的时候，脚本名和附加的参数名将被装入一个字符串列表中，并赋予`sys`模块的`argv`变量。这个列表的长度至少是 **1**；当没有脚本和参数时，`sys.argv[0]`是一个空字符串。</font>

4. Be default, Python source files are treated as encoded in `UTF-8`. To declare an encoding other than the default one, a special comment line should be added as the first line of the file. The syntax is as follow:<br/>
<font color=#3333ff>默认情况下，Python的源文件是使用`UTF-8`编码的。若要声明一个与默认编码不同的编码，需要在文件的第一行添加一条特殊的注释。语法如下：</font>
		
	```python 	
	# -*- coding: <encoding> -*-
	```
	
5. One exception to the first line rule is when the source code starts with a Unix "shebang" line. In this case, the encoding declartion should be added as the second line of the file.
<br/><font color=#3333ff>编码声明的“第一行”规则有一个例外：当源码以 Unxi 的“shebang”行开始的时候，编码声明将作为文件的第二行。例如：</font>
	
	```python
	#!/usr/bin/env python3
	```
------
> * 本文英文内容摘抄至 [Python官网](https://docs.python.org/) 教程 [The Python Tutorial](https://docs.python.org/3/tutorial/) 中的 [Using Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html) 章节。  
> * 本文中文内容为本人翻译，我已经尽力了。
