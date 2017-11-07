class: center, middle

#Testing in Python

---

#Overview

* Motivation for testing

--

* Testing functions 

--

* Continuous Integration with Travis CI

---

#Motivation

* You manually test your programs during and after you write them, why not make the process automatic?

--

* Testing can help find errors, and reducing errors should be an important 

--

* [A recent paper](http://f1000research.com/articles/3-303/v2) suggested that many scientific papers have errors in them due to software bugs

--

* Testing is included in the paper [Best practices for Scientific Computing](http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745).

--

* According to Mick Watson not testing your code is one of the [Five habits of bad bioinformaticians](http://www.opiniomics.org/the-five-habits-of-bad-bioinformaticians/)

--

* Testing also is an important part of refactoring. You probably will refactor as you test. 

--

* You will also be able to change your code in the future and be able to tell if you broke the functionality.

---

# A functional example

* We will be creating tests for a function that calculates the GC content of a sequence

--

* In a file called `gc_calc.py` add the following code 

```Python
def gc(sequence):
    gc_count = 0
    for nuc in sequence:
        if nuc == 'G':
            gc_count += 1
        if nuc == 'C':
            gc_count += 1

    return (float(gc_count) / len(sequence))
```

--

```python
>>> from gc_calc import gc
>>> gc1('ACGT')
0.5
```

---

# Your first test

* Python comes with a built in testing library called `unittest`

--

* In a file called `test_gc.py` add the follwing code

```Python
import unittest

class GcTests(unittest.TestCase):
	def test_the_simplest(self):
		pass

if __name__ == '__main__':
	unittest.main()
```

--

* All `unittest` functions need to start with `test`  

--

* You can run the tests just like you would run a normal python script `python test_gc.py`  

--

* You should see output like this:  
`.`  
`----------------------------------------------------------------------`  
`Ran 1 test in 0.000s`  
`OK`  

---

# Testing the gc function

* Before we can test `gc` we need to import it from `gc_calc.py`

--

* Add `gc` to your imports
```Python
from gc_calc import gc
```

--

* Our first test will replicate the manual testing we did

--

* Replace the `test_the_simplest` function with:
```Python
def test_gc(self):
		self.assertEqual(gc('ACTG'), 0.5)
```

--

* Rerun the test using `python test_gc.py`. Make sure the test passes

---

# Adding more tests

* We currently have a very simple test, lets add one for a longer sequence

--

* Underneath your first function add
```Python
def test_long(self):
		self.assertAlmostEqual(gc('ACTGCAGATCTGAAATTCAGTAAGGG'), 0.4230769)```

--

* We can also add tests for inputs that we don't expect

--

* We'll add a test that checks the functionality when no input is given

--

```Python
def test_empty(self):
	self.assertRaises(TypeError, gc, )
```

--

* Rerun your tests, and make sure they pass

---

#Asserts

* Asserts are used by unittest to asses the validity of the tests

--

* We've used `assertEqual`, `assertAlmostEqual`, and `assertRaises`

--

* There are also `assertTrue`, `assertFalse`, `assertIsNone`, `assertIsNotEqual`, `assertIn`, `assertIsInstance`, `assertGreater`, `assertRegex`, `assertListEqual` and many more.

--

* Each can be used to help you test the full range of functionality of your program

---

# Thinking about the intended function

* While testing we should think about what we really want our function to do, compared to what it actually does

--

* What would happen if our sequence was lowercase? Or if our sequence was mixed case?

--

```Python
>>> gc('actg')
0.0
>>> gc('aCTg')
0.25
```

--

* What would happen if we gave an empty string as the sequence?

--

```Python
>>> gc('')
Traceback (most recent call last):
		  File "<stdin>", line 1, in <module>
		    File "complement.py", line 10, in gc1
		      return (float(gc_count) / len(sequence))
		  ZeroDivisionError: float division by zero
```

---

# Thinking about the intended function (cont.)

* What would happen if our input string isn't a nucleotide string?

--

```Python
>>> gc('This is just a random sentence, but we still get a GC content back.')
0.029850746268656716
```

---
# Refactoring

* How you handle inputs is something you should think about when programming, but you can also think about them during testing

--

* Lets refactor our GC function to take into account these different types of inputs

--

My version is below:
```Python
def gc(sequence):
    gc_count = 0
    valid_nucleotides = ['A','C','T','U','G','N']
    for nuc in sequence:
        nuc = nuc.upper()
        if nuc not in valid_nucleotides:
            raise Exception(nuc + ' is not a valid nucleotide.')
        if nuc == 'G':
            gc_count += 1
        if nuc == 'C':
            gc_count += 1

    if len(sequence)==0:
        return 0 
    return (float(gc_count) / len(sequence))
```

---

# Testing the refactored function

* Now we can add tests for our refactored function

--

```Python
def test_lowercase(self):
	self.assertEqual(gc('AcTg'), 0.5)
```

--

```Python
def test_random(self):
	self.assertRaises(Exception, gc, 'This is just a random sentence, but we still get a gc content back.')
```

--

```Python
def test_empty_string(self):
	self.assertEqual(gc(''), 0)
```

--

* Add these tests and rerun `test_gc.py`. Make sure that the test pass

---

# Unintended changes

* Well written tests allow you to catch any changes that break your functionality

--

* Let's make a breaking change to the `gc` function

--

* Save your changes and rerun the tests

---

# Conclusions

* Writing tests require an initial upfront effort, but may have benefits down the road

--

* In my experience, writing tests makes you think about the code you've written, and can lead to improvements in the readability and functionality

---

# Travis CI

* Travis CI is a service that integrates with GitHub and will automatically run your tests whenever you push a commit to GitHub

--

* This reduces a barrier for you running tests. Instead of having to run them yourselves, Travis CI handles all of it for you

--

* Travis CI supports many different languages including Python, Perl, R, Java, C, C++, Go, Haskell, Julia, JavaScript, Rust, Scala and others
--

* You can also test on multiple different versions of a language, we'll use it to run our tests on Python 2.6, 2.7, 3.2, 3.3, 3.4, and 3.5

---

# Creating a GitHub Repo

* Before we can run our tests with Travis CI we need to put our code on GitHub

--

* Log into your GitHub account and create a new repository. 

--

* It doesn't matter what you call it. `testing-demo` will work if you aren't feeling creative

--

* Make sure you initialize the repo with a README, and then clone the repo to your local machine

---

# Commit your code

* Move the `gc_calc.py` file and the `test_gc.py` file into the repository

--

* Use `git add` and `git commit -m` to commit your code.  
(Remember the commit message)
--

* Use `git push` to push your code up to GitHub

---

# Setting up Travis CI

* Go to the [Travis CI site](https://travis-ci.org/) and click the big green "Sign Up" button. 

--

* You'll need to use your GitHub credentials to login.

--

* When you are signed up, find the repositories tab, and flip the switch for your `testing-demo` repo 

--

* Next we need to add a .travis.yml file

---

#.travis.yml file

* The `.travis.yml` file is used to tell Travis CI how to run the tests for your repository

--

* Create a file in your `testing-demo` repo called `.travis.yml`, and paste the following code into it.

```yaml
language: python
python:
  - "2.6"
  - "2.7"
  - "3.2"
  - "3.3"
  - "3.4"
  - "3.5"
script: python test_gc.py
```

--

* The `language` section species what language environment Travis CI should use, and what versions to test with

--

* The `script` section tells Travis CI how to run your tests. In this case it is exactly the same as how you run the tests on the commandline

---

# Commit .travis.yml

* Use `git add` and `git commit` to commit your `.travis.yml` file 

--

* `git push` the changes up to GitHub

--

* Check your Travis CI page, if all has gone well, a new build will start

--

* In a minute or so your builds should finish

--

* If everything works all the builds should turn green as your tests pass

--

* If your tests fail, the build will turn red, and Travis CI will send you an email letting you know

---

# Other uses

* You can add a Travis CI build badge to your repository README, to let other people know that you are using CI and the status of the build.

--

* You can also use Travis CI for code coverage statistics

--

* Code coverage tells you how much of your code has tests

--

* [coveralls.io](https://coveralls.io/) is a service that interacts with Travis CI to do code coverage

--

* Like the build badge, you can also add a code coverage badge to your repo
