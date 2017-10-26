class: center, middle

#Statements and Syntax
	
---

###Compound Statements

* The general syntax for all compound statements is below

```Python
header line:
	nested statement block
```

--

* The colon in the header line is necessary

--

* Indentation (spaces or tabs) marks the blocks

--

```Python
for x in range(10):
	if x % 2 == 0:
		print('even')
	else:
		print('odd')
```

--

* Things on the same indentation level are in the same block

---

###Assignment Statements

* Variable assignments create object references

--

* Variable names need to be assigned before they can be referenced

--

* Some operations perform assignments implicitly

--

```Python
>>> spam = 'SPAM'
>>> spam, ham = 'Ew', 'Yum'
>>> spam, ham, *rest = ['Ew', 'Yum', 2, 4, 6]
>>> rest
[2, 4, 6]
```

--

* You can assign to multiple variables at once. But remember about mutable and immutable variables. 

```Python
>>> c = [1,2,3]
>>> a = b = c
>>> a[0]=100
>>> b[1]=283
>>> c
[100, 283, 3]
>>> a
[100, 283, 3]
>>> b
[100, 283, 3]
```

---

###Variable names

* Start with underscore or letter, then letters, numbers and underscores can follow

--

* The case matters `name` is a different variable than `Name`

--

* There are reserved words that you can't use like `if`, `and`, `global`, `except` and others

--

* Variables that start with a single underscore like `_name` aren't imported by `from module import *`

--

* Variables that begin and end with two underscores like `__add__` are special variables in modules and classes that Python can use

---

###Expression Statements

* Expression statements are single line statements like function calls and method calls

--

* Because you don't use a variable in an expression statement they need to have side effects if you want to do anything

--

* In fact expression statements return `None` saving the results to a variable will yield weird results

```Python
>>> list = ['z','s','u','a','n','h','l']
>>> list.sort()
>>> list
['a', 'h', 'l', 'n', 's', 'u', 'z']
>>> sorted_list = list.sort()
>>> sorted_list
>>> type(sorted_list)
<class 'NoneType'>
```

---

###Print Function

* To use the Python 3 print function in Python 2 use

```Python
from __future__ import print_function
```

--

* The print function has several options that you can use

--

* The `sep` option allows you to change the separator, which is a space by default

```Python
>>> print('hello','world',sep=':::')
hello:::world
```

--

* The `end` option allows you to change the end character, which is a newline by default

```Python
>>> print('hello','world',end='--')
hello world-->>>
```

---
###Print Function (cont.)

* The `file` option allows you to specify the output file. The default is `stdout`, which prints to your command line

```Python
>>> file = open('filename','w')
>>> print('Hello',file=file)
>>> file.close()
```

---

###`if` statements

* The general form of `if` statements is:

```Python
>>> if test1:
...     statement1
... elif test2:
...     statement2
... else:
...     statement3
... 
```

--

* `elif` and `else` are optional in an `if` statement

---

###if/else Ternary Expression

* The ternary operator reduces and if/else statement to one line

--

* The general format is:

```Python
true_statement if test else false_statement
```

--

```Python
>>> print('True') if 5>4 else print('False')
True
```

---

###You Can't Handle the Truth

* All objects are `True` or `False`

--

* Nonzero numbers, non-empty objects are `True`

--

* Zeros, empty objects and `None` are `False`

--

```Python
>>> bool(1)
True
>>> bool(0)
False
>>> bool(0.0)
False
>>> bool([])
False
>>> bool(None)
False
```

---

###Boolean Operators

* `and`, `or` and `not` are boolean operators

--

* Boolean operators short-circuit, that is they stop testing as soon as the result is known

```Python
>>> True and True
True
>>> True and False
False
>>> False and True
False
```

--

```Python
>>> True or False
True
>>> not True
False
```

---

###Comparison

* Comparison (`<`,`>,`,`<=`,`>=`,`==`,`!=`) operators return a boolean value

--

* `==` tests for equality, `=` is for assignment

--

* `!=` tests if the two objects aren't equal

--

```Python
>>> [1,3,4] == [1,3]
False
>>> [1,3,4] != [1,3]
True
```

---

###While Loops

* `while` loops perform a function as long as the condition it is testing for is true

```Python
>>> while test:
...     statement
... else:
...     statement
... 
```

--

* The else is optional and only runs if the loop exits normally

--

```Python
>>> a = 0
>>> while a < 5:
...     print(a)
...     a += 1
... 
0
1
2
3
4
```

--

* `a += 1` is the equivalent of `a = a + 1`

---

###Loop Control

* `break` allows you to jump out of a loop

```Python
>>> a=0
>>> while a < 7:
...     a+=1
...     if a == 4:
...         break
...     print(a)
... 
1
2
3
```

--

* `continue` allows you to end the current loop cycle

```Python
>>> a=0
while a < 7:
...     a+=1
...     if a % 2 == 0:
...         continue
...     print(a)
... 
1
3
5
7
```

---

###For Loops

* `for` loops step through items in a sequence or object

--

* They can be used on strings, lists, tuples, dictionaries or anything that is an iterable object in Python

--

```Python
>>> for item in object:
...     do(something)
... else:
...     do(something_else)
... 
```

--

* Like `while` loops you can use `break` and `continue` and the `else` clause is optional

--

```Python
>>> tup = (1,2,5,6)
>>> for number in tup:
...     print(number**2)
... 
1
4
25
36
```

---

###For Loops (cont.)

```Python
>>> list = [(1,2),(5,6),(8,9)]
>>> for (first,second) in list:
...     print(first,second,sep=',')
... 
1,2
5,6
8,9
```

--

* You can use the `range` function to construct for loops

```Python
>>> for x in range(10):
...     print(x*2)
... 
0
2
4
6
8
10
12
14
16
18
```

---

###`range` function

* The range function takes an optional start (the default is 0), an end, and an optional step size

```Python
>>> for x in range(3,8):
...     print(x)
... 
3
4
5
6
7
```

--

```Python
>>> for x in range(8,3,-2):
...     print(x)
... 
8
6
4
```

---

###Nested Loops

* `for` and `while` loops can be nested

```Python
>>> for x in [1,2]:
...     for y in range(5):
...         print(x*y)
... 
0
1
2
3
4
0
2
4
6
8
```

--

* Nesting loops allows you to repeat an inner loop and to change its input

---

### `enumerate`

* The `enumerate` function allows you to step through an object and gives you the element number and the element at the same time

```Python
>>> for i, character in enumerate("hello"):
...     print(character,i,sep="=>")
... 
h=>0
e=>1
l=>2
l=>3
o=>4
```

---

###Common Usage

* One of the most common uses of for loops is to step through lists and perform an operation on each element

```Python
for id in unique_ids:
	if id_count[id] > 1:
		print(id + ' is not unique')
```

--

```Python
for counter, id_val in enumerate(ids):
	if id_val in id_dict:
		id_dict[id_val] += 1
	else:
		id_dict[id_val] = 1
```
