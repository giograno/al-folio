---
layout: post
title:  main module in python
date: 2017-12-17 9:00:00
description: something from an Informatik 1 lecture
comments: true
---

Recently, I had to give a lecture for the Informatik 1 course at the University of Zürich. Such a course is really the first introductory one for the students enrolled for the Bachelor studies. Therefore, they are supposed to have no prior knowledge about any programming concepts.

I gave a *live coding* lecture, solving some small assignments in order to prepare students for the final. Thus, I prepared some code snippets with the description of the task to do and the correspondent function to implement. Nothing more than the following example.

```python
# Write a function with the signature recursive_sum that accepts a nested list of integers as an argument
# [1, 2, 3, [4, 5, 6]] and returns the sum of each element of the list.

def recursive_sum(x):
	pass

if __name__ == '__main__':
	print(recursive_sum([1, 2, 3, [4, 5, 6]]))
```

After the lecture more that a student came asking the meaning of `if__name__ == '__main__'`.

### Python Modules
To fully explain the answer, we should first  clarify the concept of modules in Python. In simple words, every file filled with some Python code is a module. Organizing your project in modules allows you to do modularization and to group together classes and methods that have somehow a common goal.

Giving some examples, imagine to write a `some_func.py` file with the following content.

```python
def fib(n):   
    """ Returns the Finonacci series set up to n """
    result = []
    a, b = 0, 1
    while b < n:
        result.append(b)
        a, b = b, a+b
    return result

def add(a, b):
   """ Add two numbers and return the result """
   result = a + b
   return result
```

Now, we are able to reuse  the defined function in a new file (or module) simply importing the one above.

```python
import some_func
r = some_func.add(10, 10)
print(r)
```

In this case, `import` (sorry for the wordplay) imports *everything* that is in the `some_func.py` file. It means that we have available all the methods and the classes, but that means also that all the directly executable statements will be immediately ran. 
For instance, let’s say the our `some_func` module would contain a `print('Hey I am a module')` just at its beginning, the `import some_func` would immediately result in the execution of the `print` statement. Whether we are interested only in one (or more) function or class of a specific module, we might want to use a slightly different kind of import, like `from some_func import fib`. In this way, the only function imported with the module is `fib` and the print statement will no be longer executed. 

If we are using another module and we are interested in the function it provides, we can use `help(module)` that, in the previous case, will return something like that:

```
Help on module some_func:

NAME
    some_func

FILE
    /Users/grano/Desktop/some_func.py

FUNCTIONS
    fib(n)

    add(a, b)
```

But that’s not all.  In Python, when you are importing the code (i.e., a module) written in another file, you are handling a *module object*, an actual Python object that has its methods, properties and classes.

By default, every module comes with a set of *properties*. You can have a look at them with the command `dir(some_func)`. 
For our example, it will return something like the following:

```
['__builtins__', '__doc__', '__file__', '__name__', '__package__', 'add', 'fib']
```

As you can notice, there is a `__name__` property in the returned list and that’s exactly that we were looking for!

### The `__name__` property
If we open our shell, and import the `some_func` module, printing its `__name__` we have this.

```python
>>> import some_func
>>> print(some_func.__name__)	
some_func
```

That will print `some_func`, i.e., the name of the imported module.
But, what if we actually print the `__name__` of the current file?

```python
>>> import some_func
>>> print(__name__)
__main__
```

The script above will print `__main__`! 
That’s why this is a top level development script, i.e., the execution is starting directly from here.
We are going to have the same behavior if we save the script above in a file called `example.py` and we run `python example.py` from our shell!
Therefore, the `__name__` attribute for the entry point assumes in Python the value `__main__`. 

Let’s  see another example. Assuming that we modify our `some_func.py` in the following way. We basically added a `print` statement in the middle of the function that prints the module name, and the condition 
`if __name__ == '__main__'` at the bottom.

```python
def fib(n):   
    """ Returns the Finonacci series set up to n """
    print('Executing the module {}'.format(__name__))
    result = []
    a, b = 0, 1
    while b < n:
        result.append(b)
        a, b = b, a+b
    return result

def add(a, b):
   """ Add two numbers and return the result """
   result = a + b
   return result

if __name__ == '__main__':
    print(fib(10))
```

If we run that file directly with `python some_func.py` (the file is the starting point)  the output will be the following.

```
Executing the module __main__
[1, 1, 2, 3, 5, 8]
```

On the contrary, that is what would happen importing and executing the module from our shell.

```python
>>> import some_func
>>> some_func.fib(10)
Executing the module some_func
[1, 1, 2, 3, 5, 8]
```

So, why do often Python scripts report that `if __name__ == ‘__main__’`? Well, often is because we might want to have a different execution happening if our module is called as top level script or if is imported.
You might want to put into the `if __name__ == '__main__'` something that you need to execute only when your module is actually the starting point of your Python execution, like in the exercise that I was showing to my students.

*Note: at that time, the students were still missing their lecture on modules* 😜!