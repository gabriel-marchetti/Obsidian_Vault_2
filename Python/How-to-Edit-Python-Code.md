---
tags:
  - python
link: https://wiki.python.org/moin/HowToEditPythonCode
---
# History:
[[Python]] started development in 1989 no CWI - Centrum Wiskunde & Informatica by [[Guido-van-Rossum]].
# Programming Philosophy:
The mindset behind [[Python]] involved creating a solid base with extensible packages. This mentality was originated due to [[ABC]] problems that Guido suffered.
# Name and Neologisms:
- One of the goals of Python developers is to make Python fun to use. This is shown in plenty of examples with humorous aspects, most of examples have variables names such as **spam** and **eggs** referring to Monty Python.
# Syntax and Semantics:
- Readable Language
- Uncluttered visual layout
## Indentation:
- It uses whitespaces as indentation - this feature is called *offside-rule*.
## Statements and Control Flow:
- **If** - alongside with **elif** and **else**
- **For**
- **While**
- **Try**
- **Class**
- **Def**
- **With**
- **Pass**
- **Assert**
- **Yield**
## Expressions:
- Simple divisions always return floating-point number, even when the operands are integer.
- // serve as integer division.
- == compares by value, in contraposition of what [[Java]] does.
- Comparison by reference can be done via *is*.
- **List comprehensions** and **Generator Expressions**.
- Anonymous functions can be done via lambda functions and it's body can only be a single expression.
- **Lists** are mutable, so they **cannot** be used as keys for dictionaries.
- **Tuples** are imutable, so they **can** be used as keys for dictionaries.
# Implementations:
## CPython:
The mainstream implementation of Python. It is a portable implementation of Python and it is made in C, these implementation generates a intermediate bytecode that run on a virtual machine. This implementation is present in platforms such Windows, Unix-like, Android and IOS (unofficial). This is mainly to the reason that Python was designed to run on esoteric platform Amoeba.
## Alternative Implementation:
There is Jython that generate java byte code as intermediate and can be run on a JVM (Java Virtual Machine).
IronPython is similar byt for .NET Common Language Runtime.
PyPy can export to different types of bytecode.
There are alternatives such as Cython that compile the code into C language.