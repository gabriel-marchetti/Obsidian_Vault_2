---
tags:
  - python
link: https://docs.python.org/3/tutorial/interpreter.html
---
# Argument Passing:
Se você rodar um script python através do terminal você poderá escrever algo como:
```
python src.py 1 2 3 4
```
Os elementos de [src.py, 1, 2, 3, 4] serão armazenados como uma lista de strings na variável $\texttt{argv}$ dentro do módulo $\texttt{sys}$ 