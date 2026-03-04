---
tags:
  - python
  - coursera
---
# Constants:
**Numeric Constants** ou **Strings Constants**. 
# Reserved Words: 
![[Pasted image 20260222215428.png|center]]
Não use palavras reservadas em nomes de variáveis e etc... 
# Variables:
É um nome de uma posição de memória que desejamos manipular.
## Variable names:
- Case Sensitive.
- Must start with a letter or underscore.
- Mnemonic - Choose a variable name that makes sense to the code you are writing.
Os dois seguintes trechos de código realizam a mesma tarefa, contudo uma implementa de modo mais claro a lógica:
```python
a = 35.00
b = 12.50
c = a * b
print(c)

hours = 35.00
rate = 12.50
pay = hours * rate
print(pay)
```
# Numerical Expressions:
- Operator precedence. **PEMDAS**
P: Parenthesis
E: Exponentiation
M: Multiplication
D: Division
A: Addition
S: Subtraction

# Variable Types:
- Type of variables matter for operations.
- $\texttt{type(...)}$ pode ser usado para obter o tipo da variável.
- Dentro do Python 3, temos que **Integer Division** são convertidas para o tipo *float*.
## String Conversions:
- O Python geralmente recebe valores que são *strings* inicialmente.
- Conversão de *strings* para outros valores é uma operação comum.
```python
name = input('Who are you?')
print(f'Welcome, {name}')
```
# Documentation:
Bons nomes de variável já fazem parte da documentação de um código, contudo existem vezes que comentários podem ajudar a entender melhor um código.


# I-P-O - Input, Process and Output:
Almost all programs (if not all) will follow this process of **Input** the data, **Process** the data and **Output** the processed data.
