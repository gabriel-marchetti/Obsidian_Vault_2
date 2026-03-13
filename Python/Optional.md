---
tags:
  - python
  - python-concept
---
Usado para complementar o "Type Hinting" do Python. Refere-se à habilidade de uma variável (ou mesmo argumento de função) de assumir um valor específico ou o tipo None. $\texttt{Optional[X]} = \texttt{Union[X, None]}$ 
CODE:
```python
def greeting(name : str | None = None) -> str:
    if name is None:
        return "Hello, World!"
    return f"Hello, {name}!"

from typing import Optional
def greeting_compat(name : Optional[str] = None) -> str:
    if name is None:
        return "Hello, World!"
    return f"Hello, {name}!"

print("------ NEW WAY ------")
print(greeting(None))
print(greeting("Sabrina"))

print("------ OLD WAY ------")
print(greeting_compat(None))
print(greeting_compat("Sabrina"))
```
OUTPUT:
```
------ NEW WAY ------
Hello, World!
Hello, Sabrina!
------ OLD WAY ------
Hello, World!
Hello, Sabrina!
```
The $\texttt{Optional}$ way seems to have backward compatibility.