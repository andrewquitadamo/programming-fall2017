class: center, middle

#Data Types in Depth
	
---

###Dynamic Typing

* In statically typed languages when variables are created they are given a type and they cannot change their type

--

* In a dynamically typed language variables are bound to an object, but not a type.

--

* This means in Python you can change a variable from a string to an integer for example

```Python
>>> name = 1
>>> type(name)
<class 'int'>
>>> name = "one"
>>> type(name)
<class 'str'>
```

--

* In Python the objects themselves have types and not variable names

---

###Garbage Collection 

* Objects are garbage collected when they are no longer in use

--

* When a variable name is assigned a new object the old object is marked for garbage collection (assuming there are no other references to it)

--

* You can get the reference count by using `sys.getrefcount`

```Python
>>> import sys
>>> sys.getrefcount(name)
2
```

---

###Copying Objects

* You cannot simply create copies of immutable objects by creating a new variable

--

* We've seen this with lists, and you can use the `a = b[:]` syntax to avoid it. However with dictionaries and other immutable objects we need a way to create a copy

```Python
>>> D 
{'b': 2, 'a': 1, 'c': 3}
>>> D = {'a':1, 'b':2,'c':3}
>>> D2 = D
>>> D2['a'] = '12'
>>> D
{'b': 2, 'a': '12', 'c': 3}
```

--

```Python
>>> import copy
>>> D = {'a':1, 'b':2,'c':3}
>>> D2 = copy.copy(D)
>>> D2['a'] = 12
>>> D
{'b': 2, 'a': 1, 'c': 3}
```

---

###Equality and id

* You can use the `id()` function to check whether two objects use the same memory reference. In CPython `id()` returns the memory location of an object

```Python
>>> L = [1,2,3]
>>> L2 = L
>>> L == L2
True
>>> id(L)
4327436488
>>> id(L2)
4327436488
```

--

```Python
>>> L2 = copy.copy(L)
>>> L == L2
True
>>> id(L)
4327436488
>>> id(L2)
4327438600
```

--

* When we use the `copy()` function we create a new memory reference

---

###Numeric Types

* Floating point numbers - Number with a decimal and/or an exponent

--

* Binary - base 2

```Python
>>> 0b1010
10
>>> bin(10)
'0b1010'
```

--

* Octal - base 8 

```Python
>>> 0o10
8
>>> oct(10)
'0o12'
```

--

* Hexidecimal - base 16 (0-9, A-F)

```Python
>>> 0xF
15
>>> hex(26)
'0x1a'
```

---

###Numeric Expressions

* `+`, `-`, `*`, `/`, `>>`, `&`, etc  

--

* There are built in mathematical functions in Python that include `pow`, `abs`, `round` and others

---

###Operator Order of Precedence

* Just like in math Python has an order of operations

--

* The entire table can be found in the [Python documentation](https://docs.python.org/3/reference/expressions.html#operator-precedence)

--

* Parentheses before indexing, indexing before exponentiation, `and` before `or`

---

###Mixed Numeric Types

* When performing an operation with mixed numeric types, the "lower" type is converted up

--

* ints are converted to floats

```Python
>>> 2 + 3.0
5.0
```

--

* You can explicitly convert numeric types by using `int()`, `float()` etc

```Python
>>> int(3.9)
3
>>> float(4)
4.0
```

--

* The `int()` function truncates floating point numbers. You can combine it with the `round()` function to get the proper result

---

###Mixed Types

* You cannot combine numeric and nonnumeric types

```Python
>>> 1 + "1"
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

--

```Python
>>> 1 + int("1")
2
```

--

```Python
>>> str(1) + "1"
'11'
```

---

###Floating Point Precision

* Sometimes the results of simple floating point addition can be unexpected

```Python
>>> 0.1 + 0.2
0.30000000000000004
```

--

* This is due to the way numbers are represented internally by Python

--

* If exact computation is necessary (i.e. accounting) you can use the Decimal module 

---

###`Decimal` module

* The `Decimal` module provides a way to perform fixed precision computation

```Python
>>> import decimal
>>> Decimal(0.1)
Decimal('0.1000000000000000055511151231257827021181583404541015625')
>>> Decimal('0.1')
Decimal('0.1')
>>> Decimal('0.1') + Decimal('0.3')
Decimal('0.4')
```

---

###`Fraction` module

* Like the `Decimal` module, the `Fraction` module provides a way to perform calculations and avoid precision issues too

--

```Python
>>> from fractions import Fraction
>>> Fraction(1,2)
Fraction(1, 2)
>>> Fraction(1,2) * 2
Fraction(1, 1)
>>> Fraction(1,2) / 2
Fraction(1, 4)
>>> Fraction(1, 2) + Fraction(1, 9)
Fraction(11, 18)
```

---

###Strings

* There are several ways to represent a string

```Python
>>> str = 'string'
>>> str = "string"
>>> str = '''This
...   is a
... long
...   string'''
>>> str
'This\n  is a\nlong\n  string'
>>> print(str)
This
  is a
long
  string
```

--

* Since strings can be created with either single or double quotes you can use this to your advantage

```Python
>>> 'You can have "double quotes" in a single quoted string'
'You can have "double quotes" in a single quoted string'
>>> "You can have 'single quotes' in a double quoted string"
"You can have 'single quotes' in a double quoted string"
```

---

###String Methods

* Strings have built in methods that you can use to manipulate them

--

* The full list is in the [Python documentation](https://docs.python.org/3.6/library/stdtypes.html#string-methods)

--

* Some useful ones are `.startswith()`, `.split()`, `.rstrip()`, and `.translate()`

--

```Python
>>> str.maketrans('ACTG','TGAC')
{65: 84, 67: 71, 84: 65, 71: 67}
>>> tb = str.maketrans('ACTG','TGAC')
>>> 'ACTG'.translate(tb)
'TGAC'
```

--

* Strings also have a `.join()` method that takes a list as an argument. You can use this to combine a list with a delimiter

```Python
>>> list = ['This','is','a','list']
>>> " ".join(list)
'This is a list'
```

---

###Raw Strings

* Normally Python interprets escaped characters in strings

```Python
>>> print("Hello\nthere")
Hello
there
```

--

* If this isn't what you want you can escape the escape character

```Python
>>> print("Hello\\nthere")
Hello\nthere
```

--

* Or you can use a raw string

```Python
>>> print(r"Hello\nthere")
Hello\nthere
```

--

* Raw strings are useful for creating regular expressions

--

* The only thing you cannot do is end a raw string with a backslash, because this would escape the end quote

---

###Extended Slicing

* We've already seen how you can index and slice strings

```Python
>>> s = "this is a string"
>>> s[5:]
'is a string'
```

--

* Like `range` the slice operator takes an optional third argument which specifies the step size. Using this you can get a slice that contains every second character

```Python
>>> s[::2]
'ti sasrn'
```

--

* You can also use it to reverse a string by providing a negative step size

```Python
>>> s[::-1]
'gnirts a si siht'
```

---

###String Formatting

* There are two ways to format strings the "old" way and the "new" way

--

* The old style is similar to `printf` in C, and uses `%`

```Python
>>> name = 'Andrew'
>>> 'Hello, %s' % name
'Hello, Andrew'
```

--

* You can use a tuple to include more than one variable

```Python
>>> 'Hello, %s. You have %s messages' % (name, number)
'Hello, Andrew. You have 4 messages'
```

--

* You can use named variables and a dictionary to achieve a similar result

```Python
>>> 'Hello, %(name)s. You have %(num)s messages' % {'name':name, 'num':number}
'Hello, Andrew. You have 4 messages'
```

---

###String Formatting (cont.)

* The new style is available in Python 3 and Python 3.7

```Python
>>> 'Hello, {}'.format(name)
'Hello, Andrew'
```

--

* Just like the old style you can include multiple values and named values

```Python
>>> 'Hello, {}. You have {} messages'.format(name, number)
'Hello, Andrew. You have 4 messages'
```

--

```Python
>>> 'Hello, {name}. You have {num} messages'.format(name=name, num=number)
'Hello, Andrew. You have 4 messages'
```

---

###Formatting Floating Point Output

* There will be times when you want to specify the precision of your output. Both string formatting methods provide a way to do this

```Python
>>> import math
>>> '%s' % math.pi
'3.141592653589793'
>>> '{}'.format(math.pi)
'3.141592653589793'
```

--

```Python
>>> '%f' % math.pi
'3.141593'
>>> '%.2f' % math.pi
'3.14'
>>> '%.5f' % math.pi
'3.14159'
```

--

```Python
>>> '{:.2f}'.format(math.pi)
'3.14'
>>> '{:.5f}'.format(math.pi)
'3.14159'
```

---

###Lists

* Lists are ordered collections

--

* They are variable length (you can add and remove items in place) and mutable
	   
--

* Lists can contain objects of different types, 

--

* You can nest lists

---

###List Operations

* You can use `.append()` to add a single object to the end of the list

```Python
>>> L = [1, 2, 3]
>>> L.append(4)
>>> L
[1, 2, 3, 4]
```
--

```Python
>>> L.append([4,5])
>>> L
[1, 2, 3, [4, 5]]
```
--

* `.extend()` can be used to add multiple objects from an iterable to the end of a list

```Python
>>> L = [1, 2, 3]
>>> L.extend([4,5])
>>> L
[1, 2, 3, 4, 5]
```

--

```Python
>>> L = [1, 2, 3]
>>> L.extend((4,5))
>>> L
[1, 2, 3, 4, 5]
```

---

###List Operations (cont.)

* `.insert()` can be used to add elements to a list in any location. It takes two arguments, the position and the object to be inserted

```Python
>>> L = [1, 2, 3]
>>> L.insert(0,10)
>>> L
[10, 1, 2, 3]
```

--

```Python
>>> L = [1, 2, 3]
>>> L.insert(2, [2,4])
>>> L
[1, 2, [2, 4], 3]
```

--

* `.count()` can be used to count the number of occurrences of the search term

```Python
>>> L = [1,2,3,4,1,1]
>>> L.count(1)
3
```

---

###List Operations (cont.)

* `clear()` removes all elements from a list

```Python
>>> L = [1, 2, 3]
>>> L.clear()
>>> L
[]
```

--

* `.pop()` can be used to remove and return single elements. By default it returns the last element, although you can specify the element to remove.

```Python
>>> L = [1, 2, 3, 4, 5]
>>> L.pop()
5
>>> L
[1, 2, 3, 4]
```

--

```Python
>>> L = [1, 2, 3, 4, 5]
>>> L.pop(2)
3
>>> L
[1, 2, 4, 5]
```

---

###List Operations (cont.)

* `remove()` is like `pop()` except it does not return the element. You need to specify the element to remove

```Python
>>> L = [1, 2, 3, 4, 5]
>>> L.remove(3)
>>> L
[1, 2, 4, 5]
>>> L
[1, 2, 4, 5]
```

--

* You can also use `del` to  remove elements from a list

```Python
>>> L = [1, 2, 3, 4, 5]
>>> del L[2]
>>> L
[1, 2, 4, 5]
```

--

* While `.remove()` can only remove one element at a time, `del` can be used to remove a range of elements

```Python
>>> L = [1, 2, 3, 4, 5]
>>> del L[1:3]
>>> L
[1, 4, 5]
```

---

###Sorting Lists

* The `.sort()` method can be used to sort a list in place

```Python
>>> L = [2,3,1,5,1,93,1,5,2,4]
>>> L.sort()
>>> L
[1, 1, 1, 2, 2, 3, 4, 5, 5, 93]
```

--

* In Python 3 you cannot sort lists that contain multiple types

```Python
>>> L = ['a', 1 , [4]]
>>> L.sort()
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unorderable types: int() < str()
```

--

* `sort()` can take optional arguments

```Python
>>> L = [2,3,1,5,1,93,1,5,2,4]
>>> L.sort(reverse=True)
>>> L
[93, 5, 5, 4, 3, 2, 2, 1, 1, 1]
```

---

###Sorting Lists (cont.)

* The default `sort()` can return unexpected results if you want simple alphabetic sorting

```Python
>>> L = ['a', 'A', 'b', 'B']
>>> L.sort()
>>> L
['A', 'B', 'a', 'b']
```

--

* You can use a `key` argument to fix this

```Python
>>> L = ['B', 'A', 'b', 'a']
>>> L.sort(key=lambda str: str.lower())
>>> L
['A', 'a', 'B', 'b']
```

--

* In Python 3 the `lamba` syntax is required, but in Python 2 it isn't

```Python
>>> L = ['a', 'B', 'A', 'b']
>>> L.sort(key=str.lower)
>>> L
>>> ['a', 'A', 'B', 'b']
```

---

###`sorted()` vs `.sort()`

* You can also use the `sorted()` function to sort lists

--

* Unlike `.sort()` `sorted()` does not change the underlying list, but returns a sorted list

```Python
>>> L = ['B', 'A', 'b', 'a']
>>> sorted(L, key=lambda str: str.lower())
['A', 'a', 'B', 'b']
>>> L
['B', 'A', 'b', 'a']
```

---

###Dictionaries

* Dictionaries are unordered collections that are accessed by key

--

* They are variable length, mutable and can be heterogeneous

--

* Python dictionaries are implemented as a hash table which allows for quick retrieval of values

---

###Dictionary Operations

* `.keys()` can be used to get all the keys in a dictionary

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> list(D.keys())
['b', 'a', 'c']
```

--

* `.values()` returns the values in a dictionary

```Python
>>> list(D.values())
[2, 1, 3]
```

--

* `.items()` returns all key:value items in a dictionary

```Python
>>> list(D.items())
[('b', 2), ('a', 1), ('c', 3)]
```

---

###Dictionary Operations (cont.)

* `.get()` can be used to access a value using a key

```Python
>>> D.get('b')
2
```

--

* `.get()` can take an optional default value which will be returned if the key does not exist in the dictionary

```Python
>>> D.get('g', 0)
0
```

--

* Dictionaries do not have a `.remove()` method, but you can use the `del` operator to get rid of entries

```Python
>>> del D['a']
>>> D
{'b': 2, 'c': 3}
```

--

* The `.pop()` method removes and returns an entry, just like in lists

```Python
>>> D.pop('a')
1
>>> D
{'b': 2, 'c': 3}
```

---

###Dictionary Miscellany

* Dictionaries can't be concatenated

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> D2 = {'z':26}
>>> D + D2
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'dict' and 'dict'
```

--

* Adding a new key creates an entry

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> D['z'] = 26
>>> D
{'z': 26, 'b': 2, 'a': 1, 'c': 3}
```

--

* Keys don't have to be strings, they just have to be an immutable type

```Python
>>> D2 = {[0]:1}
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> D2 = {(0,):1}
>>> D2
{(0,): 1}
```

---

###Tuples

* Tuples are immutable, fixed length, ordered collections

--

* Tuples can contain heterogeneous types

---

###Tuple Literals

* The parentheses in a tuple literal are not always necessary

--

```Python
>>> T = (1, 2, 3, 4)
>>> T
(1, 2, 3, 4)
>>> T = 1, 2, 3, 4
>>> T
(1, 2, 3, 4)
```

--

* Single object tuples need a trailing comma

```Python
>>> T = (1,)
>>> T 
(1,)
>>> T = 1,
>>> T
(1,)
```

---

###Sorting Tuples

* Tuples do not have a `.sort()` method

```Python
>>> T = (3, 1 , 4, 5, 10, 2, 4)
>>> T.sort()
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'sort'
```

--

* You can use the `sorted()` function on tuples, however it will get a list, not a tuple

```Python
>>> sorted(T)
[1, 2, 3, 4, 4, 5, 10]
```

---

###Tuple Immutability

* If a tuple contains a mutable object that object is still mutable even in the tuple

```Python
>>> T = ([1,2,3],2,4)
>>> T[0][0] = 4
>>> T
([4, 2, 3], 2, 4)
```

--

* The immutability provides some protection against unintentional changes

--

* This also means that tuples can be used as keys for dictionaries

---

###Named Tuples

* In Python 2.7 and 3.x you can create namedtuples, which are similar to dictionaries

```Python
>>> from collections import namedtuple
>>> record = namedtuple('record', ['name', 'age'])
>>> andrew = record(name="Andrew", age=27)
>>> andrew.name
'Andrew'
>>> andrew.age
27
```

--

* You access the elements in a named tuple by using the `.key` syntax

---

###Files

* `open('filename')` creates a Python file object which you can use to interact with files

--

* If you do not specify `r`, or `w` the default is `r`

--

```Python
file = open('filename')
```

--

* `.read()` reads the entire file into a string

```Python
file = open('filename') 
file.read()
```

--

* You can save the result to a variable

```Python
file = open('filename') 
input = file.read()
```

--

* The `read()` method also takes an optional byte-length argument. Using this you can specify how many bytes to read. 

```Python
>>> file = open('filename')
>>> file.read(256)
```

* You can call file.read() multiple times until you reach the end of the file

---

###File Operations

* `readlines()` will read in a file as a list of lines. The results will include the newline characters.

```Python
>>> file = open('filename')
>>> lines = file.readlines()
>>> lines[0] #access the first line
```

--

* `write()` can be used to write strings to a file. In Python 3 the `write()` method returns the number of characters written.

```Python
>>> file = open('filename','w')
>>> file.write('Testline')
8
```

--

* `writelines()` can be used to write a list of strings to a file

---
###File Operations (cont.)

* `.close()` will close the file object and flush any input

```Python
>>> file = open('filename','w')
>>> file.write('Testline')
8
>>> file.close()
```

--

* `.flush()` will write any output that is currently in the buffer

--

* `.seek()` can be used to jump to a position in a file. The `seek()` method takes a number of bytes as an argument

```Python
file = open('filename')
>>> file.seek(10)
10
>>> file.read(10)
```

---

###File Miscellany

* Files are iterators, and can be used in loops

--

* Files are closed automatically by Python when the file object is garbage collected

--

* Python filenames are portable. You can type them using the / Unix syntax, and Python will translate them into the \ Windows syntax

```Python
file = open('C:/users/')
```

--

* There is a `b` flag that can be added to `w` and `r`. This is used for binary files

```Python
file = open('filename', `rb`)
```

---

###Pickle Objects

* The `pickle` module allows you to save Python objects directly to files

--

* These objects can be read back in as objects

--

```Python
>>> import pickle
>>> D = {'a': 1, 'b': 2}
>>> F = open('testfile','wb')
>>> pickle.dump(D,F)
>>> F.close()
```

--

* If you were to look at the file using `cat` you would get a garbled looking mess

```Python
?}q(XbqKXaqKu.%
```

--

* However you can read this back into Python

```Python
>>> F = open('testfile', 'rb')
>>> D = pickle.load(F)
>>> D
{'b': 2, 'a': 1}
```
