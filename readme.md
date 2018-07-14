# study-python
A small study project on the [python](https://www.python.org/) programming language.

## Introduction
Python is a programming language created by [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum) in the
1990's. Python is a cross platform programming language that runs on Linux, Unix, Windows and Mac, and is used
for rapid prototyping, web applications, cloud development, data processing and data science.

Python can do everything traditional programming languages like Java can do, but is more expressive in some places and
can express complex actions with a single line that will take multiple lines of code in a language like Java.

Like Java, Python has a more than complete offering of libraries that can be used to create complex applications by
reusing functions and data types that other developers already have created like eg. [Django](https://www.djangoproject.com/)
and [Flask](http://flask.pocoo.org/) for web development, [Pandas](http://pandas.pydata.org/) for data analysis
and [PyQt](https://riverbankcomputing.com/software/pyqt/intro) for GUI development. Python also has a very complete
standard library, for handling operating system calls, access databases and more.

## Static typing and Python
Python is a dynamically typed language. Variables are used as labels, and don't have carry type hints of the underlying
object they reference to. Of course, the object the variable is referencing is typed, so how you interact with the
object determines whether or not a statement executes successfully or end in a failure, at runtime of course.

With Python 3.6, it is possible to add type annotations:

```python
def add(x: int, y: int) -> int:
    result: int = x + y
    return result

add(1, 2)
```

The example shows a function `add` that takes two parameters, variable x, y of type `int`. The function has a
local variable `result` of type `int`. The function can be applied by passing the argument `1` for x, and `2` for
y which are both of type `int`.

Note that the Python runtime doesn't do anything with these type annotations. In Python you use external tools to
validate the code eg. for typing. When developing code in an IDE like [PyCharm](https://www.jetbrains.com/pycharm/),
the editor does the static type checking when you are actually typing the code, and for integrating code in de CI chain,
the tool [mypy](http://mypy-lang.org/) - a static type checker for Python - can be used to fail the build if there are
any typing problems found; but in runtime, Python is still untyped and dynamic.

## Where is Python Installed?
On a mac, python comes pre-installed, but where is it located and what is the version of python?

The default Python installation on mac osx is in `/System/Library/Frameworks/Python.framework`. There can be multiple
versions of Python installed on your system and they can be found in `/System/Library/Frameworks/Python.framework/Versions`
where there is a special `Current` directory that points to the latest version installed eg:

```bash
/System/Library/Frameworks/Python.framework/Versions $ ls -alh
drwxr-xr-x   7 root  wheel   224B  6 okt  2017 .
drwxr-xr-x   5 root  wheel   160B  6 okt  2017 ..
lrwxr-xr-x   1 root  wheel     3B  6 okt  2017 2.3 -> 2.7
lrwxr-xr-x   1 root  wheel     3B  6 okt  2017 2.5 -> 2.7
lrwxr-xr-x   1 root  wheel     3B  6 okt  2017 2.6 -> 2.7
drwxr-xr-x  10 root  wheel   320B  7 apr 06:34 2.7
lrwxr-xr-x   1 root  wheel     3B  6 okt  2017 Current -> 2.7
```

## Brew and Python
[Brew](https://brew.sh/) - a package manager for osx - installs packages to `/usr/local/Cellar`, and when you've
installed Python using brew with `brew install python`, or `brew install python2` it will install python to the
`Cellar`. Here we will find three directories, `python`, `python@2` and `python3`.

## Installing Python
Python can be installed with [Brew](https://brew.sh/) - `brew install python3`.

## See Python version
To see the Python version type:

```bash
$ python -V
Python 2.7.14

$ python3 -V
Python 3.7.0b3
```

## Python Main Environment
todo

## Python Virtual Environment
A virtual environment is a self-contained directory structure that contains both an installation of Python and
additional packages. A virtual environment is isolated from other environments and thus libraries and library versions
cannot conflict with other environments nor the main Python environment.

## Python Interpreter
Python code is compiled to a byte-code form, and that byte code form is then executed by a Python interpreter.
A downside of interpreted languages is that the speed of execution is not on par as compiled languages like C.
For real world solutions though, Python is fast enough and for some architectures like eg. AWS Lambda, Python in even
faster than JVM based solutions because of the startup time, code optimization phase and garbage collection strategies
that are in place.

## IPython
IPython is a command shell for interactive computing in multiple programming languages, originally developed for the
Python programming language, that offers introspection, rich media, shell syntax, tab completion, and history.

It can be installed with:

```
$ pip3 install ipython
```

## Python programming FAQ
Python has great documentation and a must read is the [FAQ](https://docs.python.org/3/faq/programming.html).

## Python anti-patterns
Another good read is [The Little Book of Python Anti-Patterns](https://docs.quantifiedcode.com/python-anti-patterns/index.html) 

## Projects and Build Tools
Apache Maven has set the standard for creating projects. A lot of build tools for programming languages are influenced 
by the workflow and configuration of Maven. Fortunately, there is a build tool for Python called [pybuilder](https://github.com/pybuilder/pybuilder) 
that does the same which is:

- has the notion of a project
- has a project configuration
- fixed directories for source and test
- a project lifecycle
- developer workflow
- extensible by means of plugins
- dependency management

__note__: as of 2018-07-14, pybuild is not 3.7 compatible.

## Modules
A Python [module](https://docs.python.org/3/tutorial/modules.html) is simply a Python source file, which can expose classes,
functions and global variables. When imported from another Python source file, the file name is treated as a namespace.

As stated, a module is a file containing Python definitions and statements. The file name is the module name with the
suffix `.py` appended. Within a module, the module’s name (as a string) is available as the value of the local
variable __name__.

## Global, local and in scope variables
In Python, variables that are only referenced inside a function are implicitly global. If a variable is assigned a value 
anywhere within the function’s body, it’s assumed to be a local unless explicitly declared as global.

Though a bit surprising at first, a moment’s consideration explains this. On one hand, requiring global for assigned variables 
provides a bar against unintended side-effects. On the other hand, if global was required for all global references, 
you’d be using global all the time. You’d have to declare as global every reference to a built-in function or to a component 
of an imported module. This clutter would defeat the usefulness of the global declaration for identifying side-effects.

To find out what variables are available in which scope type:

- `dir()` will give you the list of in scope variables:
- `globals()` will give you a dictionary of global variables
- `locals()` will give you a dictionary of local variables

## Executable modules
Python supports [executable modules](https://docs.python.org/3/tutorial/modules.html#executing-modules-as-scripts).
When you run a Python module with:

```bash
python foo.py <arguments>
```

the code in the module will be executed, just as if you imported it, but with the `__name__` set to "__main__".
That means that by adding this code at the end of your module:

```python
if __name__ == "__main__":
    print("Hello World!")
```

you can make the file usable as a script as well as an importable module, because the code that parses the command line
only runs if the module is executed as the 'main' file. Ie. when the module is imported, the `__name__` value will be the
name of the file, thus the code block of the if statement will not be executed.

## Module Search Path
When a module named `foo` is imported, the interpreter first searches for a built-in module with that name. If not found,
it then searches for a file named `spam.py` in a list of directories given by the variable `sys.path`.

`sys.path` is initialized from these locations:

- The directory containing the input script (or the current directory when no file is specified).
- PYTHONPATH (a list of directory names, with the same syntax as the shell variable PATH).
- The installation-dependent default.

## The dir() function
The built-in function [dir](https://docs.python.org/3/tutorial/modules.html#the-dir-function) is used to find out which
names a module defines. It returns a sorted list of strings. Without arguments, dir() lists the names you have defined currently.
Note that dir() lists all types of names - variables, modules, functions, etc. Note that dir() does not list the names of
built-in functions and variables. If you want a list of those, they are defined in the standard module builtins:

```
import builtins
>>> dir(builtins)
```

The following is interesting:

```
>>> xs = [1, 2, 3]
>>> dir(xs)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__',
'__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__',
'__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__',
'__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count',
'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
>>> help(xs.sort)
Help on built-in function sort:
sort(...) method of builtins.list instance
    L.sort(key=None, reverse=False) -> None -- stable sort *IN PLACE*
```

## Packages
A Python package is simply a directory of Python module(s). As with Java or Scala, these directories can be nested
and the directory can contain Python modules. The names of these modules can be imported by other modules eg.
`from com.github.dnvriend.foo import add` when the file `foo.py` has been put in the `com/github/dnvriend` directory.
Before Python treats the directories as containing packages though, an `__init__.py` file must be contained in the directory.
In the simplest case, `__init__.py` can just be an empty file, but it can also execute initialization code for the package.

For example:

```
── com
│   ├── __init__.py
│   ├── __pycache__
│   │   └── __init__.cpython-36.pyc
│   └── github
│       ├── __init__.py
│       ├── __pycache__
│       │   └── __init__.cpython-36.pyc
│       └── dnvriend
│           ├── __init__.py
│           ├── __pycache__
│           │   ├── __init__.cpython-36.pyc
│           │   └── foo.cpython-36.pyc
│           └── foo.py
├── main.py
```

## Importing '*' from a package
When a module imports everything from a package `from com.github.dnvriend import *`, the following happens:

if a package’s `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should
be imported when `from package import *` is encountered. It is up to the package author to keep this list up-to-date when
a new version of the package is released. Package authors may also decide not to support it, if they don’t see a use
for importing * from their package. For example, the file com/github/dnvriend/__init__.py could contain the following code:

```
__all__ = ["foo", "bar", "baz"]
```

This would mean that `from com.github.dnvriend import *` would import the three named submodules `foo`, `bar` and `baz`
which equals to the files `foo.py`, `bar.py` and `baz.py` in the `com/github/dnvriend` directory.

If `__all__` is not defined in `__init__.py`, no modules are imported into the current namespace, moreover,
`import *`, is considered bad practice in production code, so don't import `*`.

## Higher order functions and typing
Python supports higher order functions and [as of Python 3.6, typing](https://docs.python.org/3/library/typing.html), also see
[PEP-526](https://www.python.org/dev/peps/pep-0526/):

```python
from typing import List

xs: List[int] = [1, 2, 3]

list(map(lambda x: x + 1, xs))
[2, 3, 4]

list(filter(lambda x: x < 2, xs))
[1]

from functools import reduce

reduce(lambda x, y: x + y, xs)
6
```

## Data Classes
Python 3.7 onwards support, [Data Classes - PEP-557](https://www.python.org/dev/peps/pep-0557/) are classes which exist primarily to store values
which are accessible by attribute lookup:

```python
from dataclasses import dataclass

@dataclass
class Person:
   name: str
   age: int   

p: Person = Person("dennis", 42)

p
Person(name='dennis', age=42)
```

## Literal String Interpolation
Python 3.6 onwards support [Literal String Interpolation - PEP-498](https://www.python.org/dev/peps/pep-0498/) which
add a string formatting mechanism called 'Literal String Interpolation'. Such strings will be referred to as `f-strings`,
taken from the leading character used to denote such strings, and standing for "formatted strings".

```python
# without interpolation
for x in [1, 2, 3]:
    ...:     for y in [2, 4, 6]:
    ...:         print(str(x) + " * " + str(y) + " = " + str(x * y))

# with interpolation
for x in [1, 2, 3]:
    ...:     for y in [2, 4, 6]:
    ...:         print(f"{x} * {y} = {x * y}")
    ...:
```

## String Format
Python has a way to [format strings](https://docs.python.org/3/library/string.html).
String literals have a `format` method, that can be used to format a string:

```python
"Hello {0}, my name is {1}".format("foo", "bar")
'Hello foo, my name is bar'
```

Formatting strings have more options that can be read in the [Format String Syntax](https://docs.python.org/3/library/string.html#format-string-syntax),
and there is even a [Format Specification Mini Language](https://docs.python.org/3/library/string.html#format-specification-mini-language)
to define how individual values are presented.

## Loops
Python supports looping over iterables:

```python
for x in [1, 2]: print(x)

countdown = 10

while countdown >= 0:
    ...:     print(str(countdown))
    ...:     countdown -= 1

[x * y for x in [1, 2, 3] for y in [2, 4, 6] if x > 2 and y <= 4]
[6, 12]

[x * x for x in range(10) if x % 2 == 0]
[0, 4, 16, 36, 64]
```

## List operations
The following are handy list operations:

```python
xs = [1, 2, 3]

while xs: print(f"The value is: {xs.pop()}")
The value is: 3
The value is: 2
The value is: 1
xs = [1 ,2 ,3]

xs.append(4)

xs
[1, 2, 3, 4]

xs[1]
2

xs[1::]
[2, 3, 4]

xs[1:3]
[2, 3]

xs[::2]
[1, 3]

In [10]: sum([1, 2, 3])
Out[10]: 6

In [11]: max([1, 2, 3])
Out[11]: 3

In [12]: min([1, 2, 3])
Out[12]: 1

In [13]: sorted([3,2,1])
Out[13]: [1, 2, 3]

In [14]: list(reversed([3,2,1]))
Out[14]: [1, 2, 3]

In [15]: list(range(10))
Out[15]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]v

In [16]: list(range(1, 10))
Out[16]: [1, 2, 3, 4, 5, 6, 7, 8, 9]

In [17]: list(range(1, 10, 2))
Out[17]: [1, 3, 5, 7, 9]

In [18]: xs = ['a','b','c']

In [19]: for (i, c) in enumerate(xs): print(f"{i} -> {c}")
0 -> a
1 -> b
2 -> c

In [20]: ys = [1, 2, 3, 4]

# xs runs out of elements, so the iteration stops
In [21]: for (x, y) in zip(xs, ys): print(f"{x} -> {y}")
a -> 1
b -> 2
c -> 3


```

# String operations
The following are handy string operations:

```python
str = "a,b,c,d,e"

xs = str.split(",")

xs
['a', 'b', 'c', 'd', 'e']

# note for a join, you first choose a character and then join with the list
",".join(xs)
'a,b,c,d,e'
```

## Functions
Functions can be written as follows:

```python
# def <name>(params): <function-body or function-block>
def noop(): pass

# function need 'return', when you need to return a value
def filter_even(x: int) -> bool: return x % 2 == 0

list(filter(filter_even, [1, 2, 3, 4]))
[2, 4]

# no 'return' necessary for lambdas
list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))
[2, 4]

# functions that don't explicitly return a value, actually do return a value
# this value is of type 'None'.
def greet(name: str) -> None: print(f"Hello {name}")

# lets apply the function 'greet' with the argument "Dennis"
greet("Dennis")
Hello Dennis
```

## None
None represents 'null', 'nothing', 'void', and must be used as follows:

```python
x = None

# note the 'is' keyword
if x is None: print("None")
None

x = 1

if x is None: print("None")
```

## Dictionary
A dictionary is a key -> value pair, also known as a Map[K, V]:

```python
from typing import Dict

cats: Dict[str, int] = {}

cats['dennis'] = 5

cats
{'dennis': 5}

cats['bar'] = 2

cats
{'dennis': 5, 'bar': 2}

for cat in cats: print(cat)
dennis
bar

for cat in cats.keys(): print(cat)
dennis
bar

for cat in cats.values(): print(cat)
5
2

In [10]: for (k, v) in cats.items(): print(f"{k} -> {v}")
dennis -> 5
bar -> 2
```

## Binary types
Python supports working with bytes and the [core types for working with binary data are bytes and bytearray](https://docs.python.org/3/library/stdtypes.html#binary-sequence-types-bytes-bytearray-memoryview).

[Bytes objects](https://docs.python.org/3/library/stdtypes.html#bytes-objects) are *immutable* sequences of single bytes.
Since many major binary protocols are based on the ASCII text encoding, bytes objects offer several methods that are only
valid when working with ASCII compatible data and are closely related to string objects in a variety of other ways.

```python
xs = b"Hello World!"

xs
b'Hello World!'

for x in xs: print(x)
72
101
...

# decode() return a string decoded from the given bytes. Default encoding is 'utf-8'.
xs.decode()
'Hello World!'
```

[bytearray](https://docs.python.org/3/library/stdtypes.html#bytearray-objects) bytearray objects are a mutable counterpart to bytes objects.
As bytearray objects are mutable, they support the mutable sequence operations in addition to the common bytes and bytearray operations.

```python
xs = bytearray()

xs += b"Hello World!"

xs
bytearray(b'Hello World!')
```

## Tuples
Python supports tuples, a tuple is similar to a list, but is *immutable*, a list is not:

```python
fruits = ("Apple", "Banana", "Orange", "Lemon")

for fruit in fruits: print(f"Would you like a {fruit}?")
Would you like a Apple?
Would you like a Banana?
Would you like a Orange?
Would you like a Lemon?

# you can convert a tuple to a list, and a list to a tuple
tuple(list(fruits))
('Apple', 'Banana', 'Orange', 'Lemon')
```

## Sets
Python supports the Set type; an unordered collection of unique items. Python uses the `{}` symbols to define
a set. A Dictionary also uses `{}`, but in a dictionary you give key/value pairs. There is also the
`frozenset`, which is just a set, but immutable:

```python
xs = {1, 2, 3, 3, 3, 2, 1, 4 }

xs
{1, 2, 3, 4}

xs = {'a', 'z', 'b', 'z', 'a' }

xs
{'a', 'b', 'z'}

xs.intersection({'x', 'y', 'z'})
{'z'}

xs.union({'x', 'y', 'z'})
{'a', 'b', 'x', 'y', 'z'}
```

## os module
The [os module](https://docs.python.org/3/library/os.html) provides features relating to your operating system.
The following are handy methods:

```python
# getting environment variables
import os

os.getenv('USER')
'dennis'

os.path.abspath('.')
'/Users/dennis/projects'
```

## sys module
The [sys module](https://docs.python.org/3/library/sys.html) provides access to some variables used or maintained by the 
interpreter and to functions that interact strongly with the interpreter.

The following are handy methods:

`sys.argv` returns list of command line arguments passed to a Python script. 
argv[0] is the script name (it is operating system dependent whether this is a full pathname or not). 
If the command was executed using the -c command line option to the interpreter, argv[0] is set to the string '-c'. 
If no script name was passed to the Python interpreter, argv[0] is the empty string.

```python
import sys

sys.argv
['']
```

## re module
The [re module](https://docs.python.org/3/library/re.html) provides regular expression matching operations - whether a string matches a given pattern.

```python
import re

if re.search('foo', 'foobar'): print("foo is in foobar")
foo is in foobar

if 'foo' in 'foobar': print("foo is in foobar")
foo is in foobar

if re.search('.bar', 'foobar'): print("Matched!")
Matched!

if re.search('(foo)(bar)', 'foobar'): print("Matched!")
Matched!

res = re.search('(foo)(bar)', 'foobar')

res.groups()
('foo', 'bar')
```

## Asynchronous programming
see: http://masnun.com/2016/03/29/python-a-quick-introduction-to-the-concurrent-futures-module.html

The [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html) module is part of the Python standard 
library from v3.2, and provides a high level API for launching asynchronous tasks. 
The module contains the [Executor](https://docs.python.org/3/library/concurrent.futures.html#executor-objects) class which 
is an abstract class and it can not be used directly. The `Executor` class has two very concrete subclasses, 
the [ThreadPoolExecutor](https://docs.python.org/3/library/concurrent.futures.html#threadpoolexecutor) which is used for 
network operations or I/O, and [ProcessPoolExecutor](https://docs.python.org/3/library/concurrent.futures.html#processpoolexecutor).
which is used for CPU intensive tasks. The `ProcessPoolExecutor` uses the `multiprocessing` module and is not affected by the 
Global Interpreter Lock. However, we can not use any objects that is not picklable. So we need to carefully choose what we 
use/return inside the callable passed to process pool executor. 

### as_completed()
The `as_completed()` function takes an iterable of Future objects and starts yielding values as soon as the futures start resolving:

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from time import sleep
from random import randint

def return_after_5_secs(num):
    sleep(randint(1, 5))
    return "Return of {}".format(num)

pool = ThreadPoolExecutor(5)
futures = []
for x in range(5):
    futures.append(pool.submit(return_after_5_secs, x))

for x in as_completed(futures):
    print(x.result())
```

output:

```
Return of 0
Return of 2
Return of 1
Return of 3
Return of 4
```

alternatively, you can manage the Threadpool:

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from time import sleep
from random import randint

def return_after_5_secs(num):
    sleep(randint(1, 5))
    return "Return of {}".format(num)

with ThreadPoolExecutor(max_workers=5) as executor:
	futures = [ executor.submit(return_after_5_secs, x) for x in range(5) ]	   
	for x in as_completed(futures):
	    print(x.result())
```

The main difference between the `map` method with `as_completed` is that `map` returns the results in the order in which we pass the iterables. 
That is the first result from the `map` method is the result for the first item. On the other hand, the first result from the `as_completed` 
function is from whichever future completed first:

```python
from concurrent.futures import ProcessPoolExecutor, as_completed
import math

PRIMES = [
    112272535095293,
    112582705942171,
    112272535095293,
    115280095190773,
    115797848077099,
    1099726899285419]

def is_prime(n):
    if n % 2 == 0:
        return False
 
    sqrt_n = int(math.floor(math.sqrt(n)))
    for i in range(3, sqrt_n + 1, 2):
        if n % i == 0:
            return False
    return True

with ProcessPoolExecutor() as executor:
	for number, prime in zip(PRIMES, executor.map(is_prime, PRIMES)):
		print('%d is prime: %s' % (number, prime))
```

Output:

```
112272535095293 is prime: True
112582705942171 is prime: True
112272535095293 is prime: True
115280095190773 is prime: True
115797848077099 is prime: True
1099726899285419 is prime: False
```

### wait()
The `wait()` function would return a named tuple which contains two set – one set contains the futures which completed (either got result or exception) 
and the other set containing the ones which didn’t complete:

```python
from concurrent.futures import ThreadPoolExecutor, wait
from time import sleep
from random import randint
 
def return_after_5_secs(num):
    sleep(randint(1, 5))
    return "Return of {}".format(num)
 
pool = ThreadPoolExecutor(5)
futures = []
for x in range(5):
    futures.append(pool.submit(return_after_5_secs, x))
 
print(wait(futures))

# decomposing the tuple
(done, not_done) = wait(futures)

# iterating across 'done' futures
for x in done: print(x.result())
```

output:

```
Return of 0
Return of 1
Return of 3
Return of 2
Return of 4
```

```python
from concurrent.futures import ThreadPoolExecutor
from time import sleep
from random import randint

def return_after_random_seconds(num: int):
    sleep(randint(1, 5))
    return "Return of {}".format(num)

with ThreadPoolExecutor(max_workers=5) as executor:
	for y in executor.map(return_after_random_seconds, [1, 2, 3, 4, 5]):
		print(y)
```

## pip and pypi
Pypi is the [Python Package Index](https://pypi.python.org/pypi) - a repository of software for the Python programming language,
that contains software developed by third-party developers that is not part of the Python standard library. Although the
Python standard library is very complete, it does not offer all the functionality your project could need. Instead of
programming a specific feature from scratch, it is good to take a look at the Pypi index, and see if a specific feature
is already available. When a package is found, it can be installed using [pip](https://pypi.python.org/pypi),
either to the global python environment or a virtual python environment to be used by your program.

## pipenv
[Pipenv](https://docs.pipenv.org/) is a project that aims to bring the best of all packaging worlds to the Python world.
It harnesses Pipfile, pip, and virtualenv into one single toolchain. It features very pretty terminal colors.
Pipenv, automatically manages a separate virtual environment for each project and application that you work on, and
is the officially recommended Python packaging tool.

Pipenv is a tool that aims to bring the best of all packaging worlds to the Python world. It automatically creates and
manages a virtualenv for your projects, as well as adds/removes packages from your Pipfile as you install/uninstall packages.
It also generates the ever-important Pipfile.lock, which is used to produce deterministic builds.

Pipenv is primarily meant to provide users and developers of applications with an easy method to setup a working environment.
For the distinction between libraries and applications and the usage of setup.py vs Pipfile to define dependencies.

The problems that Pipenv seeks to solve are multi-faceted:

- You no longer need to use pip and virtualenv separately. They work together.
- Managing a `requirements.txt` file can be problematic, so Pipenv uses `Pipfile` and `Pipfile.lock` to separate
  abstract dependency declarations from the last tested combination.
- Hashes are used everywhere, always. Security. Automatically expose security vulnerabilities.
- Strongly encourage the use of the latest versions of dependencies to minimize security risks arising from outdated components.
- Give you insight into your dependency graph (e.g. $ pipenv graph).
- Streamline development workflow by loading .env files.

To install pipenv, just type `pip3 install pipenv`

Usage Examples:

```
# Create a new project using Python 3.6, specifically:
$ pipenv --python 3.6

# Install all dependencies for a project (including dev):
$ pipenv install --dev

# Install ipython but only for development
$ pipenv install -d ipython

# Create a lockfile containing pre-releases:
$ pipenv lock --pre

# Show a graph of your installed dependencies:
$ pipenv graph

# Check your installed dependencies for security vulnerabilities:
$ pipenv check

# Install a local setup.py into your virtual environment/Pipfile:
$ pipenv install -e .

# Use a lower-level pip command:
$ pipenv run pip freeze

# Spawn a shell in the virtual environment (of the project)
$ pipenv shell
```

Commands:
- check      Checks for security vulnerabilities and against PEP 508 markers provided in Pipfile.
- clean      Uninstalls all packages not specified in Pipfile.lock.
- graph      Displays currently–installed dependency graph information.
- install    Installs provided packages and adds them to Pipfile, or (if none is given), installs all packages.
- lock       Generates Pipfile.lock.
- open       View a given module in your editor.
- run        Spawns a command installed into the virtualenv.
- shell      Spawns a shell within the virtualenv.
- sync       Installs all packages specified in Pipfile.lock.
- uninstall  Un-installs a provided package and removes it from Pipfile.
- update     Runs lock, then sync.

## toolz
[Toolz](https://github.com/pytoolz/toolz) provides a set of utility functions for iterators, functions, and dictionaries.
These functions interoperate well and form the building blocks of common data analytic operations. They extend the standard
libraries [itertools](https://docs.python.org/3/library/itertools.html) and [functools](https://docs.python.org/3/library/functools.html)
and borrow heavily from the standard libraries of contemporary functional languages. It can be installed with `pip3 install toolz`.

The [Itertools](https://docs.python.org/3/library/itertools.html) module implements a number of iterator building blocks
inspired by constructs from APL, Haskell, and SML. Each has been recast in a form suitable for Python.

The [functools](https://docs.python.org/3/library/functools.html) module is for higher-order functions:
functions that act on or return other functions. In general, any callable object can be treated as a function for the purposes of this module.

## boto3
[Boto](https://boto3.readthedocs.io/en/latest/) is the Amazon Web Services (AWS) SDK for Python, which allows Python 
developers to write software that makes use of Amazon services like S3 and EC2. Boto provides an easy to use, 
object-oriented API as well as low-level direct service access.

Boto3 can be installed with:

```bash
$ pipenv install boto3
```

Using boto3:

```python
import boto3

session = boto3.Session(profile_name='your_profile_name')

ec2 = session.resource('ec2')

```

## click
[Click](http://click.pocoo.org/5/) is a Python package for creating beautiful command line interfaces in a composable way 
with as little code as necessary. 

CLI programs have the following format:

```
$ python mytool.py [OPTIONS] COMMAND [ARGS]...
```

For example, we can make a tool `mytool.py instances stop` where `instances` is a *command* and `stop` is an *argument* and
things like `--aws_profile` and `--project` are *options*. Without click, these kinds of applications are quite difficult
to create, maintain and extend. 

For example:

```bash
$ python mytool/mytool.py --help
Usage: mytool.py [OPTIONS]

  Simple program that greets NAME for a total of COUNT times.

Options:
  --count INTEGER  Number of greetings.
  --name TEXT      The person to greet.
  --help           Show this message and exit.
```

## setuptools
[Setuptools](https://setuptools.readthedocs.io/en/latest/) is a library to facilitate packaging Python projects.

```
$ pipenv install -d setuptools
```

Create a `setup.py` file in the root of your project containing:

```python
from setuptools import setup

setup(
    name='shotty',
    version='0.1',
    author='Dennis Vriend',
    author_email='dnvriend@gmail.com',
    description="a tool for managing ec2 snapshots",
    licence='Apache 2.0',
    packages=['shotty'],
    url="http://foo.bar",
    install_requires=[
        'click',
        'boto3'
    ],
    entry_points='''
        [console_scripts]
        shotty=shotty.shotty:cli
    ''',
)
```

To create a distribution type:

```
$ pipenv run "python setup.py bdist_wheel"
```

The 'wheel' - package - is available in the `dist` directory.

To install the package type:

```
$ pip3 install dist/shotty-0.1-py3-none-any.whl
```

To get information from the package type:

```
$ pip3 show shotty
Name: shotty
Version: 0.1
Summary: a tool for managing ec2 snapshots
Home-page: http://foo.bar
Author: Dennis Vriend
Author-email: dnvriend@gmail.com
License: Apache 2.0
Location: /usr/local/lib/python3.7/site-packages
Requires: boto3, click
```

To uninstall the package type:

```
$ pip3 uninstall shotty
```

To distribute a private package use S3 and give everyone read access. To install the package from an S3 bucket type: 

```
$ pip3 install https://s3.amazonaws.com/shotty-dist/hotty-0.1-py3-none-any.whl
```

## pandas
[pandas](https://pandas.pydata.org/) is an open source library, providing high-performance, easy-to-use data structures and data analysis tools 
for the Python programming language.

```
pipenv install pandas
```

## jupyter
[jupyter](http://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/index.html) is a Python notebook
running inside the browser.

```
pipenv install jupyter
```

## flask
[Flask](http://flask.pocoo.org/) is a microframework for Python based on Werkzeug, Jinja 2 and good intentions.

## Handy scripts
The following are handy python scripts. You can just execute them with ipython

## Removing all non-empty 'target' directories

```python
import glob
import shutil
# listing all dirs
for filename in glob.iglob('**/target/', recursive=True):
    print(filename)
# delete all non-empty directories    
for filename in glob.iglob('**/target/', recursive=True):
    shutil.rmtree(filename)
``` 

## Resources
- [Python tutorial](https://docs.python.org/3/tutorial/index.html)
- [Python standard library](https://docs.python.org/3/library/index.html)
- [Python built-in functions](https://docs.python.org/3/library/functions.html)
- [Python Package Index - pypi](https://pypi.python.org/pypi)
- [pipenv](https://docs.pipenv.org/)
- [IPython reference](https://ipython.org/ipython-doc/3/interactive/reference.html)
- [Flake8](http://flake8.pycqa.org/en/latest/)
- [Click - create CLI interfaces](http://click.pocoo.org/5/)
- [boto3 - AWS SDK for Python](https://github.com/boto/boto3) - [docs](https://boto3.readthedocs.io/en/latest/)
- [Setuptools - packaging python projects](https://setuptools.readthedocs.io/en/latest/)
- [???](https://blog.sideci.com/about-style-guide-of-python-and-linter-tool-pep8-pyflakes-flake8-haking-pyling-7fdbe163079d)
- [pythonprogramming.net](https://pythonprogramming.net/)
- [mutable - immutable](https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747)

## modules
- [shutil](https://docs.python.org/3/library/shutil.html)
- [glob](https://docs.python.org/3/library/glob.html)
- [os](https://docs.python.org/3/library/os.html)

## Database Drivers
- [Python Database API Spec - PEP-249](https://www.python.org/dev/peps/pep-0249/)
- [psycopg - PostgreSQL adapter for Python](http://initd.org/psycopg/) - [docs](http://initd.org/psycopg/docs/)
- [MySQL Connector/Python](https://github.com/mysql/mysql-connector-python) - [docs](https://dev.mysql.com/doc/connector-python/en/)

## Youtube
- [JetBrains TV - What's new in PyCharm 2018.1](https://www.youtube.com/watch?v=Q9YcMvgc0js)
- [Structuring your first Python project](https://www.youtube.com/watch?v=RKHMnevITF0)