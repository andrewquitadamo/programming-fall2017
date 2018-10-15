class: center, middle

#Data Types

---

###Core Data Types

.center[<img src="data-types.png" style="max-width:75%; height:auto"/>]
---

###Numbers

* The two most common Python number types are integers (ints) and floating point (floats)

--

* There are also complex numbers, fixed decimals and rationals

---

###Operations

* You can add (+), subtract (-), multiply (\*), divide (/), exponentiate(\*\*) numbers

--

* There is also integer division (//) and the modulus operator (%)

--

* Division is works slightly different in Python 2 and Python 3

--
* Python 2

```Python
>>> 2/4
0
>>> 3/2
1
>>> 2/4.0
0.5
```

--

* Python 3

```Python
>>> 2/4
0.5
>>> 3/2
1.5
>>> 2/4.0
0.5
```

---

### math module

```Python
>>> import math
>>> math.pi
3.141592653589793
>>> math.sqrt(110)
10.488088481701515
```

--

```Python
>>> help(math)

Help on module math:

NAME
    math

FILE
    /Users/andrewquitadamo/anaconda/lib/python2.7/lib-dynload/math.so

MODULE DOCS
    https://docs.python.org/library/math

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(...)
        acos(x)
        
        Return the arc cosine (measured in radians) of x.

```
---

###Strings

* Generally strings are a collection of text

--

* Technically they are a collection of bytes

--

* String Basics

```Python
>>> S = 'Spam'
>>> len(S)
4
```

--

* Indexing 

```Python
>>> len(S)
4
>>> S[0]
'S'
>>> S[-1]
'm'
>>> S[-2]
'a'
```

--

* Indexing starts at 0

---

###Strings (cont.)

* Slicing

```Python
>>> S[1:3]
'pa'
>>> S[1:4]
'pam'
>>> S[1:]
'pam'
>>> S[0:3]
'Spa'
>>> S[:3]
'Spa'
```

--

* Concatenation

```Python
>>> S + 'alot'
'Spamalot'
>>> S
'Spam'
>>> S*8
'SpamSpamSpamSpamSpamSpamSpamSpam'
```

--

* The `+` for numbers is addition but for strings it is concatenation. This is an example of polymorphism which we will discuss more when we get to OO

---

###Immutability

--

```Python
>>> S[0]='s'
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

--

* Numbers, strings and tuples are immutable

--

* Lists and dictionaries are mutable

--

* You can save the results of a string operation by reassigning back to the variable

```Python
>>> S = S + 'alot'
>>> S
'Spamalot'
```

---

###String Specific Methods

--

```Python
>>> S.find('pa')
1
>>> S.replace('pa','LA')
'SLAm'
>>> S
'Spam'
```

--

```Python
>>> line = 'BI_GS_DEL1_B5_P2682_257\tENSG00000188000.2\t-50.0350478013566\t  
2.19054140417393e-184\t3.06305595087044e-179\t-0.242246304080066'
>>> line.split('\t')
['BI_GS_DEL1_B5_P2682_257', 'ENSG00000188000.2', '-50.0350478013566',  
'2.19054140417393e-184', '3.06305595087044e-179', '-0.242246304080066']
>>> line.split()
['BI_GS_DEL1_B5_P2682_257', 'ENSG00000188000.2', '-50.0350478013566',  
'2.19054140417393e-184', '3.06305595087044e-179', '-0.242246304080066']
```
--

* Escaped characters `\t` is tab, `\n` is newline, `\r` is carriage return, `\\` is backslash

---

### String Specific Methods (cont.)

```Python
>>> S.upper()
'SPAM'
>>> S.lower()
'spam'
>>> S.isalpha()
True
```

--

```Python
>>>line = 'BI_GS_DEL1_B5_P2682_257\tENSG00000188000.2\t-50.0350478013566\t  
2.19054140417393e-184\t3.06305595087044e-179\t-0.242246304080066\n'
>>> line.rstrip()
'BI_GS_DEL1_B5_P2682_257\tENSG00000188000.2\t-50.0350478013566\t  
2.19054140417393e-184\t3.06305595087044e-179\t-0.242246304080066'
```

--

```Python
line.rstrip().split()
['BI_GS_DEL1_B5_P2682_257', 'ENSG00000188000.2', '-50.0350478013566',  
'2.19054140417393e-184', '3.06305595087044e-179', '-0.242246304080066']
```

---

###Unicode

* Python 2 and Python 3 handle unicode differently

--

* Python 2

```Python
>>> S = 'sp\xc4m'
>>> S
'sp\xc4m'
```

--

* Python 3

```Python
>>> S = 'sp\xc4m'
>>> S
'spÄm'
>>> S = '\U0001f62c \U0001f60e hello'
>>> S
'😬 😎 hello'
```

---

###Pattern Matching

* `re` module

--

```Python
>>> S = 'Spam'
>>> re.search('pa',S)
<_sre.SRE_Match object; span=(1, 3), match='pa'>
```

--

* We will cover regular expressions in lab next week

---

###Lists

* Lists are ordered collections

--

* They can contain different data types

--

* Lists are mutable, and can be modified in place

--

```Python
>>> L = [1,2,3,'a','b']
>>> L
[1, 2, 3, 'a', 'b']
```

--

```Python
>>> L[0]
1
```

--

```Python
>>> L[3:]
['a', 'b']
```

---
* List bounding issues

```Python
>>> L[100]
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

--

```Python
>>> L[100]=98
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
IndexError: list assignment index out of range
```

---

### List Nesting

* Lists can contain lists

--

```Python
>>> L = [[1,2,3],[4,5,6],[7,8,9]]
>>> L
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

--

* Indexing Nested Lists

```Python
>>> L[0]
[1, 2, 3]
```

--

```Python
>>> L[0][2]
3
```

---

### Comprehensions

* List comprehensions can build new lists by processing another list

--

```Python
>>> [row[1] for row in L]
[2, 5, 8]
>>> [row[1]*2 for row in L]
[4, 10, 16]
```

--

* You can use `if` statements with list comprehensions

```Python
>>> [row[1]*2 for row in L if row[1] % 2 == 0]
[4, 16]
```

---

###Generators

* A generator is an expression that produces results when called

--

```Python
>>> G = (sum(row) for row in L)
>>> next(G)
6
>>> next(G)
15
>>> next(G)
24
>>> next(G)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
StopIteration
```

--

* The `map` function can apply a function to every element in a list

```Python
>>> list(map(sum,L))
[6, 15, 24]
```

--

* In Python 2 the `list()` surrounding the `map` isn't necessary

---

###Dictionaries

* Dictionaries store key:value mappings

--

* You can create a dictionary with its data

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> D
{'b': 2, 'a': 1, 'c': 3}
```

--

* You can access a value by using the key

```Python
>>> D['b']
2
```

--

* If you try to use a key that doesn't exist you will get an error

```Python
>>> D['xyz']
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
KeyError: 'xyz'
```
---

###Dictionaries (cont.)

* You can check if keys exist before attempting to access them

```Python
>>> 'xyz' in D
>>> if key in D:
...    print(D[key])
... 
```

--

* Because dictionaries are mutable you can create dictionaries element by element

```Python
>>> D['name']='Andrew'
>>> D['age']=27
>>> D
{'age': 27, 'name': 'Andrew'}
```

--

* Like lists dictionaries can be nested

```Python
>>> D = {'name': {'first': 'Andrew', 'last': 'Quitadamo'}}
>>> D['name']
{'first': 'Andrew', 'last': 'Quitadamo'}
>>> D['name']['last']
'Quitadamo'
```

---
###Playing with Keys

* You can get a list of all the keys in a dictionary by using the `.keys()` method

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> list(D.keys())
['b', 'a', 'c']
```

--

* Because the order of dictionaries doesn't matter your keys may appear in a different order than they were entered

--

* To get the keys in a replicable order you can sort them

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> keys = list(D.keys())
>>> keys
['b', 'a', 'c']
>>> keys.sort()
>>> keys
['a', 'b', 'c']
```

--

* Because lists are mutable the `.sort()` method replaces the original list with the sorted version.

---

###Tuples

* Tuples are essentially immutable lists

--

* They are a fixed collection of objects

--

```Python
>>> T=(1,2,3,4)
>>> T
(1, 2, 3, 4)
```

--

* Tuples share many operations with lists

```Python
>>> len(T)
4
>>> T[0]
1
>>> T[:2]
(1, 2)
```

--

* They can be nested and can contain mixed object types

---

###Tuples (cont.)

* Remember tuples are immutable

```Python
>>> T + (5,6)
(1, 2, 3, 4, 5, 6)
>>> T
(1, 2, 3, 4)
>>> T[0]=17
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

--

* To change a tuple you have to reassign the changes back to the variable. You overwrite the current version with the new version.

```Python
>>> T = (17,) + T[1:]
>>> T
(17, 2, 3, 4)
```

--

* The trailing comma is required as this signals to Python that you are creating a one element tuple.

```Python
>>> T = (17) + T[1:]
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'tuple'
```
	
---

###Files

* Interacting with files is something you will end up doing a lot

--

* Thankfully this is really easy to do in Python

--

* To open a file you use the `open` function

```Python
file = open('filename','w')
file.write('This is a string that will end up in the file\n')
file.close()
```

--

* Depending on what you want to do you use `w` for writing, `r` for reading, `r+` to read and write, and `a` to append

---

###Files (cont.)

* To read from a file is just as easy

```Python
file = open('filename','r')
text = file.read()
file.close()
```

--

* This format reads in the entire file into the text variable. If you are working with large files this isn't a good idea. You can use the `with open` syntax instead.

```Python
with open('filename','r') as file:
	for line in file:
		print(line)
```

--

* When you use the `with open` syntax you do not need to use `.close()` Python handles it for you

---

###Sets

* Sets can be used to perform mathematical set operations

--

* You can think of them as keyless dictionaries

--

```Python
>>> S = {1,2,3}
>>> S2 = {3,4,2}
>>> S3 = {1,1,1,2}
>>> S
{1, 2, 3}
>>> S2
{2, 3, 4}
>>> S3
{1, 2}
```

--

* You can perform intersection using `&`, union using `|`, difference using `-` and test if a set is a superset of another set by using `>`

```Python
>>> S & S2
{2, 3}
>>> S | S2
{1, 2, 3, 4}
>>> S - S3
{3}
>>> S > S3
True
```

---
###Sets (cont.)

* You can use sets to filter duplicates

```Python
>>> S3 = {1,1,1,2}
>>> S3
{1, 2}
```
--

* You can also check for set membership

```Python
>>> 'p' in set('spam')
True
```

--

* This isn't unique to sets, you can check membership in dictionaries, lists, tuples and strings using the same syntax

---

###Other Data Types

* Decimals

--

* Fractions

--

* Booleans (`True` and `False`)

--

* `None` Type

--

* User Defined Classes
