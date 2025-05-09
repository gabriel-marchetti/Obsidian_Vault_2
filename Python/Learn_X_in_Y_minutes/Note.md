---
tags:
  - python
  - programação
---

## Comentários:
Há duas maneiras de fazer comentários dentro do python:
```python
# Esse é um comentário de uma única linha.

'''
	Esse tipo de estrutura é uma String com múltiplas linhas, 
	contudo é muitas vezes utilizado para fins de documentação.
'''
```
## Operações com números:
```python

# Vou pular as coisas que eu já sei como, por exemplo, como fazer soma, multiplicação e etc...
# Contudo, é legal citar aqui a divisão-chão.
5 // 3 # Deve retornar 1
-5 // 3 # Deve retornar 2
5.0 // 3 # Deve retornar 1.0

# Exponenciação:
2 ** 3 # Deve retornar o resultado de 2^3
```
## Booleanos:
```python
'''
	Assim como no C, as variáveis Booleanas True e False são armazenadas como 1 e 0, respectivamente.
'''
True + True # Deve retornar 2
True * 3 # Deve retornar 3

# Se fizermos cast de algumas estruturas de dados conhecidas como
bool(0)
bool("")
bool([])
bool({})
bool(())
bool(set())
bool(None)
# Devem retornar falso.
```
## is vs ==
```python
# is verifica se os objetos se tratam da mesma referência, isto é, se são o mesmo objeto.
a = [1,2,3,4]
b = a
b is a # True
b == a # True

b = [1,2,3,4]
b is a # False
b == a # True

# Parece ser intuitivo que se 
# b is a, então b == a
```
## Strings:
```python
# Strings literais podem ser concatenados sem o uso do '+'
print("Hello" " world!")

# Podemos usar f-Strings para formatar Strings.
name = "Sabrina"
print(f'Ela disse seu nome, {name}')
```
## Python ternary Operator:
```python
"Isso" if 0 > 1 else "Aquilo"
```
## Array Slice:
```python
# First task:
#   Print sliding window of consecutive numbers...
print("First Task:")

numbers = []
for i in range(1, 10):
    numbers.append(i)

for i in range(10):
    try:
        if(len(numbers[i:i+3]) == 3):
            print("\t", end='')
            print(numbers[i:i+3])
    except IndexError:
        None

# Second task:
#   Print only the even numbers...
print("Second Task:")

print('\t', end='')
print(numbers[1::2])

# Third task:
#   Print the reversed list...
print("Third Task:")

print('\t', end='')
print(numbers[::-1])

# Forth task:
#   Check what happens when stop is out of bound.

print('Forth Task:')
print('\t', end='')
print(numbers[:100:])
```
## Shallow Copy vs Deep Copy:
```python
# Making a deep copy of a list.
print("Testing Deep Copy.")

numbers_copy = numbers[:] # Makes a deep copy of numbers.
print('\t',end='')
print(numbers is numbers_copy)
print('\t',end='')
print(numbers == numbers_copy)

# Note que se você rodar
print("Testing Shallow Copy.")
numbers_shallow_copy = numbers

print('\t',end='')
print(numbers is numbers_shallow_copy)
print('\t',end='')
print(numbers == numbers_shallow_copy)
```

## List functions:
```

```