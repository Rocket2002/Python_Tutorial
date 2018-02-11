## 5. Modules
1. A module is a file containing Python definitions and statements. The file name is the module name with the suffix .py appended, the module's name (as string) is available as the value of the global variable `__name__`.<br/>
<font color=#3333ff>一个模块是一个包含Python定义和语句的文件。文件名是模块名后添加.py后缀而成。模块的名字（字符串）可以作为全局变量`__name__`的值。</font>

	```python
	# fibo.py
	# fibonacci numbers module
	def fib(n):     # write Fibonacci series up to n.
		a, b = 0, 1
		while b < n:
			print(b, end=' ')
			a, b = b, a + b
		print()
		
	>>> import fibo
	>>> fibo.fib(100)     # using the module name you can access the functions.
	1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89
	>>> fibo.__name__
	'fibo'
	```
	
2. Each module has its own private symbol table, which is used as the global symbol table by all functions defined in the module. Modules can import other modules. The imported module names are placed in the importing moudle's global symbol table.<br/>
<font color=#3333FF>每一个模块都有自己的私有符号表，这个符号表被模块中定义的函数当作全局符号表使用。模块可以引入其他模块，被引入模块的名字将被引用它的模块放入其全局符号表中。</font>

3. There is a variant of the `import` statement that imports names from a module directly into the importing module's symbol table. This does not introduce the module name from which the imports are token in the local symbol table.<br/>
<font color=#3333ff>有一种不同的`import`语句，它将名称从一个模块中直接引入到另一模块的符号表。这种方式并没有将被导出名称的模块自身的名称引入本地符号表。</font>

	```python
	>>> from fibo import fib
	>>> fib(500)
	1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377
	```
	
4. There is even a variant to import all names that a module defines. This import all names except those beginning with an underscore(`_`). **Note** that in general the practice of import `*` from a module or package is frowned upon, since it often causes poorly readable code.<br/>
<font color=#3333ff>甚至有一种奇特的方法，引入一个模块定义的全部名字。这种方式会引入除了以下划线（`_`）开头的名字以外的全部名字。**注意**，一般情况下，这种从一个模块或包中引入`*`的做法是不推荐的，因为它经常会带来很差可读性的代码。</font>

	```python
	>>> from fibo import *
	>>> fib(500)
	1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377
	```
	
5. When you run a Python module, the code in the module will be executed, just as if you imported it, but with the `__name__` set to `__main__`. That means that by adding this code (see sample) at the end of you module, you can make the file usable as a script as importable module, because the code that parse the command line only run if the module is executed as the "main" file.<br/>
<font color=#3333FF>当你运行一个Python模块时，模块中的代码会被执行，就好像被引入一样，但是会把`__name__`设置为`__main__`。这意味着在你的模块结尾处加上这些代码（见示例），你可以把用于执行的脚本文件像一个可引入的模块一样使用，因为这段代码只有在模块作为主文件被执行是才会被解析。</font>

	```python
	if __name__ == '__main__':
		import sys
		fib(int(sys.argv[1]))
	```
	
6. When a module is imported, the interpreter first searches for a built-in module with that name. If not found, it then searches for a file named \<module_name\>.py in a list of directories given by the variable `sys.path`. `sys.path` is initialized from these locations:<br/>
<font color=#3333ff>当一个模块被已引入，解释器首先在内置模块搜索名称。如果没有找到，它就在`sys.path`变量给出的目录列表中搜索名为\<模块名\>.py的文件。`sys.path`被初始化为一下位置：</font>
	
	* The directory contining the input script (or the current directory when no file is specified)<br/>
<font color=#3333FF>包含当前脚本的目录（或者，如果没有指定文件时，就是当前目录）</font>
	* `PYTHONPATH` (a list of directory names, with the same syntax as the shell PATH)<br/>
<font color=#3333ff>`PYTHONPATH`（一个目录名称的列表，和shell变量PATH一样的语法）</font>
	* The installation-dependent default<br/>
<font color=#3333ff>安装相关的默认值</font>

7. To speed up loading modules, Python caches the compiled version of each modules in the `__pycache__` directory under the named `module.version.pyc`, where the version encodes the format of the compiled files. For example, `__pycache__/spam.cpythono-33.pyc`.<br/>
<font color=#3333ff>为了加速加载模块，Python会在每个模块所在目录的`__pycache__`目录下存放以`module.version.pyc`格式命名的编译版本，其中version部分是编译文件额编号。例如：`__pycache__/spam.cpython-33.pyc`。</font>

8. Python checkes the modification date of the source against the compiled version to see if it's out of date and needs to be recompiled. Python does not check the cache if there is no source module. To support a non-source distribution, the compiled module must be in the same directory, and there must not be a source module.<br/>
<font color=#3333ff>Python比对源码和编译版本的修改时间，以此判断编译版本是否已过期，需要重新编译。Python不检查没有源码的模块的缓存。为了支持无源码分发，编译模块**必须**在源码目录中，并且没有源码模块。</font>

9. A program doesn't run any faster when it is read from a `.pyc` file than when it is read from a `.py` file; the only thing that's faster about `.pyc` file is the speed with which the are loaded.<br/>
<font color=#3333ff>一个程序从`.pyc`文件读取执行不会比从`.py`文件读取执行更快，`.pyc`文件只是加快了模块的加载速度。</font>

10. Some modules are built into the interpreter; these provide access to operations that are not part of the core of the language but are nevertheless built in, either for efficiency or to provide access to operating system primitives such as system call.<br/>
<font color=#3333ff>一些模块是内置在解释器中的；这些模块提供不是语言核心的操作，然而依然是内置的，要么是为了效率，要么是提供对操作系统底层访问，比如，系统调用。</font>

11. The built-in function `dir()` is used to find out which names as module defines. It returns a sorted list of strings. Without arguments, `dir()` list the names you have defined currently. Note that it lists all types of names: variable, modules, function, etc.<br/>
<font color=#3333ff>内置函数`dir()`用于找出一个模块定义的名称。它返回一个已排序的字符串列表。没有参数的`dir()`列出当前你已经定义过的名称。**注意**，它列出所有类型的名称：变量、模块、函数等。</font>

	```python
	>>> import fibo, sys
	>>> dir(fibo)
	['__name__', 'fib']	
	>>> a = [1, 2, 3, 4, 5]
	>>> fib = fibo.fib
	>>> dir()
	['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
	```
	
12. The `__init__.py` files are required to make Python treat the directories as containing packages; this is done to prevent directories with a common name, such as string, from unintentionally hiding valid modules that ocur later on the module seach path.<br/>
<font color=#3333ff>文件`__init__.py`是Python把目录当作闭包处理的必需条件，这可以防止名称是通用名称的目录，例如：string，在无意中隐藏了模块搜索路径后面的有效模块。</font>

13. Note that when using `from package import item`, the item can be either a submodule (or a subpackage) of the package, or some other name defined in the package, like a function, class or variable. Contrarily, when using syntax like `import item.subitem.subsubitem`, each item except for the last must be a package; the last item can be a module or a package but can't be a class or function or variable defined in the previous item.<br/>
<font color=#3333ff>**注意**，当使用`from package import item`时，item可以是一个包中的子模块（或子包），或者是包中定义的其他名字，比如：一个函数、类或变量。相反地，当使用类似`import item.subitem.subsubitem`语法时，除了最后一项外的每一项都必须是包；最后一项可以是一个模块或者一个包，但不能是前一项的类、方法或变量。</font>

14. The `import` statement use the following convention: if a package's `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered. If `__all__` is not defined, the statement `from package import *` does not import all submodules from the package into the current namespace; it only ensure that the package has been imported and the import whatever names are defined in the package.<br/>
<font color=#3333ff>`import`语句使用如下的约定：如果包的`__init__.py`文件的代码定义了一个名为`__all__`的列表，它将被作为遇到`from package import *`时被引入的模块列表。如果没有定义`__all__`，`from package import *`语句**不会**引入包中的所有子模块，它只能引入包自己，然后引入包中定义的所有名字。</font>

	```python
	__all__ = ['echo', 'surround', 'reverse']     # that would import the three submodules
	```
	
15. Note that relative imports are base on the name of the current module, Since the name of the main module is always "`__main__`", modules intended for use as the main module in Python application must always use absolute imports.<br/>
<font color=#3333ff>**注意**，相对引入是基于当前模块的。因为主模块的名字一直是“`__main__”，在Python程序中，想要作为主模块使用的模块必须一直使用绝对引入。</font>

------
> * 本文英文内容摘抄至 [Python官网](https://docs.python.org/) 教程 [The Python Tutorial](https://docs.python.org/3/tutorial/) 中的 [Modules](https://docs.python.org/3/tutorial/modules.html) 章节。
> * 本文中文内容为本人翻译，我已经尽力了。
