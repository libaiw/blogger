---
title: Cython, the first lesson: Helloworld
---
## Installation
a great man once said:
>> the elephant into the refrigerator first step, open the refrigerator;

it is written first step cython, installation cython. 

Here we have direct input on the command line pip install cython,then there is no error message, so long installed.

### hello world
pyx create a new file named helloworld.pyx,the statement added:
```Python
print ("Helloworld")
```

There are two ways, the easiest start the helloworld.pyx to program python directory, input

## Method 1, pyximport 
```python
import pyximport; 
pyximport.install ()
import  helloworld
```
c is not referenced in the python modules when the  pyx import code,automatically compiles.py and .pyx file. Automatic build process in the user directory for my users to automatically compile the pyx file. 
![cython01.jpg](img/cython01.jpg)
If it will automatically compile most of the python standard library, if you use the following statement.
```
(pyimport install pyximport. = True)
```
Under automatically compiled FIG.timeit Module
![cython02.jpg](img/cython02.jpg)

## Method 2:setup.py
In the second embodiment is prepared setup.py and run it;
```python
from distutils.core import setup
from Cython.Build import cythonize

setup(
    ext_modules = cythonize("helloworld.pyx")
)
```

   
The setup.py with helloworld.pyx in a file at home, and run python setup.py build_ext--in place.Therefore, as shown in the compilation process 
![cython03.jpg](img/cython03.jpg)

and finally we get the helloworld.pyd (windows platform), if linux is get a helloworld.
So, then open a command line to run python in the same directory, enter import helloworld,you will get the whole world.
## Summary
For large module, or the need to write using distutils setup.py file. pyximport usually applied to test myself writing code.
Good luck.

<!-- http://blog.csdn.net/sgoal/article/details/77247461 -->
