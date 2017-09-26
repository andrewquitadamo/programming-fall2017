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
