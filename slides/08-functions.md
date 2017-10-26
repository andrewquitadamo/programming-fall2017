class: center, middle

#Functions, Scopes and Iterables

---

##Functions

* Functions are an important element of code

--

* Functions allow for code reuse and reduce redundancy

--

* Functions help in program design

--

* Good functions do one thing, and one thing only

--

* Well written functions are small

---
	
##Calling a function

* We've seen functions before

```Python
open(filename,'r')
print('Hello')
len(L)
```

--

* Functions are called by using the function name, and then by passing arguments in parentheses

--

* Even if the function doesn't take any arguments the parentheses are still required

--

```Python
empty_function()
```

---

##Defining Functions

* Functions are defined using the `def` keyword

--

```Python
def adder(x,y):
	return(x + y)
```

--

* The `return` keyword ends the function and sends the results back to the caller

--

```Python
>>> adder(4,8)
12
```

---

##Variable Scope

* Local variables are only available inside the function

```Python
>>> x = 12
>>> def count_x():
...     x = 3
...     x +=1
...     print(x)
... 
>>> count_x()
4
>>> x
12
```

--

* The same even holds true for mutable variables

```Python
>>> L = [0]
>>> def mod_L():
...     L = [1,3]
...     L.append(4)
...     print(L)
... 
>>> mod_L()
[1, 3, 4]
>>> L
[0]
```

---

##Variable Scopes (cont.)

* Names inside a `def` block are only available in the block and don't clash with names outside the block

--

* In Python there are global, local, and nonlocal variables

--

* Global variables are available to the entire module/file, but not across modules

--

* You can declare local variables as global, or nonlocal to expand their scope

--

* Each function has its own scope

```Python
def func1():
    x = 3
    print(x)

def func2():
    x = 45
    print(x)

>>> func1()
3
>>> func2()
45
```

---

##Variable Name Resolution

* Python searches the local, the enclosing, the global, and the builtin scope for variables

--

* You can find all the builtin variables and functions by using

```Python
dir(__builtins__)
```

--

* You can redefine a builtin, but unless you really know what you are doing -- don't

```Python
>>> print = ''
>>> print('Hello')
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'str' object is not callable
```

---

##Factory Functions or Closures

* A closure is a function that returns a function with a state attached

--

```Python
>>> def create_exp(x):
...     def exp(y):
...         return(x**y)
...     return exp
... 
>>> square = create_exp(2)
>>> square(2)
4
>>> square(3)
8
>>> cube = create_exp(3)
>>> cube(2)
9
```

--

* Closures aren't commonly used in Python programming

---

##Function Arguments

* In Python arguments are passed by reference, which means objects aren't copied

--

* This means that changing a mutable object that is an argument can change the original

--

```Python
>>> L = [1,2,3]
>>> def change_list(list):
...     list.append(17)
... 
>>> change_list(L)
>>> L
[1, 2, 3, 17]
```

--

* You can explicitly use a copy as an argument

```Python
>>> change_list(L[:])
>>> L
[1, 2, 3, 17]
```

---

##Multiple Returns

* Generally you should return only one value from a function, but you can return multiple values in Python

--

```Python
>>> def add_mult(x,y):
...    sum = x + y
...    prod = x * y
...    return sum,prod
... 
>>> add_mult(4,5)
(9, 20)
```

---

##Argument Matching

* By default Python matches arguments by position

```Python
>>> def print_three(a,b,c):
...    print('a is:',a,'\nb is:',b,'\nc is',c,sep=' ')
... 
>>> print_three(1,2,3)
a is: 1 
b is: 2 
c is 3
```

--

* You can specify arguments by name and ignore the position

```Python
>>> print_three(1,c=2,b=3)
a is: 1 
b is: 3 
c is 2
```

---

##Default Arguments

* You can specify defaults for arguments when you write a function

```Python
>>> def print_three(a,b=2,c=3):
...    print('a is:',a,'\nb is:',b,'\nc is',c,sep=' ')
... 
>>> print_three(1)
a is: 1 
b is: 2 
c is 3

>>> print_three(1,4)
a is: 1 
b is: 4 
c is 3

>>> print_three(1,c=4)
a is: 1 
b is: 2 
c is 4
```

---

##Other Ways of Passing Arguments

* You can pass tuples and dictionaries using the `*` and `**` respectively

--

```Python
>>> arg_tup = (4, 5, 78)
>>> print_three(arg_tup)
a is: (4, 5, 78) 
b is: 2 
c is 3
>>> print_three(*arg_tup)
a is: 4 
b is: 5 
c is 78
```

--

```Python
>>> arg_dict = {'a':4,'b':12,'c':5}
>>> print_three(**arg_dict)
a is: 4 
b is: 12 
c is 5
```

---

##Accepting Multiple Length Arguments

* While you can pass multiple length arguments, you need to specifically write your functions to accept them

```Python
>>> arg_tup = (1,2,3,4)
>>> print_three(*arg_tup)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: print_three() takes from 1 to 3 positional arguments but 4 were given
>>> arg_dict = {'a':4,'b':12,'c':5,'d':84,'e':9}
>>> print_three(**arg_dict)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: print_three() got an unexpected keyword argument 'd'
```

---

##Accepting Multiple Length Arguments (cont.)

```Python
>>> def print_three(a,b=2,c=3, *rest):
...    print('a is:',a,'\nb is:',b,'\nc is',c,sep=' ')
... 
>>> print_three(*arg_tup)
a is: 1 
b is: 2 
c is 3
```

--

```Python
>>> def print_three(a,b=2,c=3, **rest):
...    print('a is:',a,'\nb is:',b,'\nc is',c,sep=' ')
... 
>>> print_three(**arg_dict)
a is: 4 
b is: 12 
c is 5
```

---

##Keyword Only Arguments

* You can specify arguments to be "keyword only" by adding them after `*args` or `**args`

--

```Python
>>> def print_three(a,*args,b):
...    print('a is:',a,'\nb is:',b,sep=' ')
... 
>>> print_three(1,2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: print_three() missing 1 required keyword-only argument: 'b'
>>> print_three(1,b=2)
a is: 1 
b is: 2
```

--

* You can combine keyword only arguments and defaults

```Python
>>> def print_three(a,*args,b=3):
...    print('a is:',a,'\nb is:',b,sep=' ')
... 
>>> print_three(1)
a is: 1 
b is: 3
```

---

##Recursive Functions

* Recursive functions call themselves

--

```Python
>>> def rec_sum(list):
...     if list == []:
...         print(list)
...         return 0
...     else:
...         print(list)
...         return list[0] + rec_sum(list[1:])
```

--

```Python
>>> rec_sum([1,2,3,4,5,6])
[1, 2, 3, 4, 5, 6]
[2, 3, 4, 5, 6]
[3, 4, 5, 6]
[4, 5, 6]
[5, 6]
[6]
[]
21
```

---

##Recursion vs. Loops

* Many times a recursive function can be written as a loop

--

```Python
>>> def for_sum(list):
...     sum = 0
...     for i in list:
...         sum += i
...     return sum
... 
>>> for_sum([1,2,3,4,5,6])
21
```

--

* You can write recursive functions to handle arbitrary functions

--

```Python
>>> def sumtree(L):
...     tot = 0 
...     for x in L:
...         if not isinstance(x, list):
...             tot += x
...         else:
...             tot += sumtree(x)
...     return tot 
... 
>>> sumtree([1,2,3,[4,5],6,[5,[6,8,8]]])
48
```

---

##Recursion limitations

* Simple recursion will have problems with cycles in data structures

--

* In Python the default recursion limit is 1000, but you can change it

--

* Recursion isn't a commonly used strategy in Python coding

---

##Lambda Functions

* Lambda functions are anonymous or unnamed functions

--

* They can be used in places that a `def` statement cannot

--

* We've seen them when sorting dictionaries and dictionary keys

--

* You use the `lambda` keyword to help define a lambda function

--

```Python
>>> f = lambda x,y,z: x+y+z
>>> f(1,2,3)
6
```

---

##Functional Programming Tools

* Roughly defined functional programming applies functions to lists, sequences or other iterables

--

* While not a fully fledged functional programming language, Python has several built in functional programming tools

--

* `map` and `filter` are in the Python standard library, and `reduce` is in the `functools` module

---

##`map`

* `map` is used to apply a function over a sequence

--

```Python
>>> strings = ['hello', 'world']
>>> map(str.upper,strings)
<map object at 0x1024019e8>
>>> list(map(str.upper,strings))
['HELLO', 'WORLD']
```

---

##`filter`

* `filter` returns only values that match the criteria specified

--

```Python
>>> strings = ['hello', 'world']
>>> filter(lambda x: x.startswith('h'), strings)
<filter object at 0x102401a20>
>>> list(filter(lambda x: x.startswith('h'), strings))
['hello']
```

--

```Python
>>> first_10 = list(range(0,10))
>>> first_10
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(filter(lambda x: x%3==0, first_10))
[0, 3, 6, 9]
```

---

##`reduce`

* `reduce` applies a function to combine items in an iterable

--

```Python
>>> from functools import reduce
>>> reduce((lambda x,y: x+y), first_10)
45
```

--

```Python
>>> reduce((lambda x,y: x*y), first_10[1:])
362880
```

---

##Iterables

* We've encountered iterables when dealing with for loops and files

--

* You can manually loop through a file by calling `.readline()`

--

```Python
f = open('testfile','r')
f.readline()
```

--

* This is the equivalent of `.__next__()` (`.next()` in Python 2)

--

```Python
f = open('testfile','r')
f.__next__()
```

--

* Unlike `.readline()` `.next()` will through an exception when the end of the file is reached

--

```Python
>>> f.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

---

##Lists and Iterables

* Technically lists aren't iterables, but they can be made into one

--

```Python
>>> L = [1, 2, 3, 4]
>>> I = iter(L)
>>> I.__next__()
1
>>> I.__next__()
2
>>> I.__next__()
3
>>> I.__next__()
4
>>> I.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

--

* `for` loops call the `iter()` and `__next__()` automatically for you

---

##Dictionaries and Iterables

* The `.keys`, `.values` and `.items` methods for dictionaries return views, which can be turned into iterables either by `iter` or in a `for` loop

```Python
>>> D = {'a':1,'b':2,'c':3}
>>> dk = iter(D.keys())
>>> dk.__next__()
'b'
>>> dk.__next__()
'c'
>>> dk.__next__()
'a'
>>> dk.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

---

##Dictionaries and Iterables (cont.)

* You can call `iter` directly on a dictionary, which will create an iterator for the keys

--

```Python
>>> I = iter(D)
>>> I.__next__()
'b'
>>> I.__next__()
'c'
>>> I.__next__()
'a'
>>> I.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

---

##List Comprehensions

* List comprehensions are similar to `for` loops in lists

--

```Python
>>> L = [1,2,3,4,5]
>>> L = [x + 10 for x in L]
>>> L
[11, 12, 13, 14, 15]
```

--

* You can add `if` clauses to list comprehensions

```Python
>>> L = [1,2,3,4,5,6,7,8,9,10]
>>> L = [x for x in L if x%2==0]
>>> L
[2, 4, 6, 8, 10]
>>> L = ['hello', 'world']
>>> L = [x for x in L if x.startswith('h')]
>>> L
['hello']
```

--

* List comprehensions can be faster than `for` loops

---
