---
title: "python是如何查找标识符并对其赋值的"
date: 2023-07-28T12:41:37+08:00
draft: false
---

### 函数

The execution of a function **introduces a new symbol table** used for the local variables of the function. More precisely, **all variable assignments in a function store the value in the local symbol table; whereas variable references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names**. Thus, global variables and variables of enclosing functions cannot be directly assigned a value within a function (unless, for global variables, named in a global statement, or, for variables of enclosing functions, named in a nonlocal statement), although they may be referenced.

The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called; thus, arguments are passed using call by value (where the value is always an **object reference**, not the value of the object. Actually, call by object reference would be a better description, since if a mutable object is passed, the caller will see any changes the callee makes to it (items inserted into a list).).  **When a function calls another function, or calls itself recursively, a new local symbol table is created for that call**.

A function definition associates the function name with the function object in the current symbol table. The interpreter recognizes the object pointed to by that name as a user-defined function. Other names can also point to that same function object and can also be used to access the function:

``` python
>>> def fib():
...     pass

>>>fib
<function fib at 10042ed0>
>>>f = fib
>>>f(100)
0 1 1 2 3 5 8 13 21 34 55 89
```

Coming from other languages, you might object that fib is not a function but a procedure since it doesn’t return a value. In fact, even functions without a return statement do return a value, albeit a rather boring one. This value is called None (it’s a built-in name). Writing the value None is normally suppressed by the interpreter if it would be the only value written. You can see it if you really want to using print():

```python
>>>fib(0)
>>>print(fib(0))
None
```

### Default Argument Values

The default values are evaluated(**only once**) at the point of function definition in the **defining scope**, so that

```python
i = 5

def f(arg=i):
    print(arg)

i = 6
f()
```

will print 5. 下面的代码片段会产生什么结果？

```python
def f(a, L=[]):
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))
```
