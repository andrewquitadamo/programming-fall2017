class: center, middle

#Introduction to Python  

---

###Why Choose Python? 

* Its readable

--

* Its object oriented  

--

* Its built to enable software reuse  

--

* Python programs tend to be smaller than equivalent C or Java programs  

--

* No need to compile   

--

* Python code is portable across platforms 

--

* Python has lots of pre-written libraries  

--

* Dynamic Typing

--

* Automatic Memory Management

---

.center[![](https://imgs.xkcd.com/comics/python.png)]

---

###Cons

* Execution speed

---

###Uses

* System Programming

--

* GUI Programming

--

* Servers and Web Programming

--

* Prototyping

--

* Numeric and Scientific Programming

	* SciPy

	* NumPy

---

###The Zen of Python

```
import this
```  

--

```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

---

### Python Interpreter

.center[<img src="https://pclib.github.io/safari/program/learning-python/Text/httpatomoreillycomsourceoreillyimages1695840.png" style="max-width:75%; height:auto"/>]

---

### Python Implementations

* CPython

* Jython

* IronPython

* Stackless

* PyPy

---

### Frozen Binaries

* Provide a way to distribute Python programs

--

* No need for the recipient to have Python, frozen binaries come with PVM

--

* Several different ways to make a frozen binary depending on who you want to run it

	* py2exe

	* PyInstaller

	* py2app

---

### Interactive Prompt

* In the terminal type `python` or `python3`  

--

* You should see something like  
```
Python 3.4.2 (v3.4.2:ab2c023a9432, Oct  5 2014, 20:42:22) 
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```  

--

* This is a Python specific prompt -- it is not the command line

--

* You can use it to test programs and experiment with Python expressions

--

* It isn't good for writing complicated programs  

--

* Everything you enter will be deleted after you close the prompt

---

###Interactive Prompt (cont.)

* The output of your expressions will be displayed below the command

```
>>>print('hello world!')
hello world!
>>>print(2**8)
256
```

--

* Compound statements need to be ended with an extra blank line

```
>>> for x in 'spam':
...     print(x)
... 
s
p
a
m
```

--

* Indentation for the compound statements can be either tabs or spaces, but they can not be mixed.

---

###Python 2 vs Python 3

* There are currently two different versions of Python

--

* There are a few differences between the two, but the vast majority is the same

--

* These differences occur in the print statement, how Python handles strings, division, exception handling and others

--

* We will try to point out differences between Python 2 and 3 when they exist

--

* I will try to write example code that works with both

---

###Python Scripts

* More commonly you can write your code in a file and execute it from there

--

* Open up a file titled `script.py` in your favorite text editor type the following lines.
```
#First Script
import sys
print(sys.platform)
print(2 ** 100)
x = 'Spam!'
print(x * 8)
```

--
* Save the file and close

--

* To run type `python script.py`

--

* You should see something like: 
```
darwin
1267650600228229401496703205376
Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
```
---

###Comments

* Comments are text that aren't executed by the runtime

--

* They are delimited by # 
```
#This is a comment
print('hello')
```

--

* You should comment code to tell others about tricky parts, or to remind yourself about something

--

* You can use triple quotes ''' or """ to make multiline comments
```
'''
This is a 
multiline comment.
'''
```

---

###Filename extensions

* The standard extension for a Python script is `.py` however it is not required

--

* If you are using a "fancy" text editor you need to be careful about automatic file extensions like `.doc` or `.txt`. 

--

* Use vim, emacs or nano to avoid these problems

---

###Module Imports

* You can import any script into the python interpreter

```
>>>import script
darwin
1267650600228229401496703205376
Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
```

--

* If you attempt to import the script again it won't show any output

--

* This will happen even if you have changed the script

--

* You can use the `reload` module to repeat imports and reload code

--

```
from imp import reload
reload(script)
darwin
1267650600228229401496703205376
Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
```

---

###Module Attributes

* Open up `script.py` and add a line like
```
name = Andrew
```

--

* Go to the interpreter and reload script.py

```
>>> import script
>>> script.name
Andrew
```

--

* You can import name directly
```
>>> from script import name
>>> name
Andrew
```

--

* You can examine a module by using `dir`
```
dir(script)
['__builtins__', '__doc__', '__file__', '__name__', '__package__', 'name', 'sys', 'x']
```

--

* Each module has its own namespace which is helpful to prevent name collisions

--

* This will become important in OO programming

--

###Quitting
