---
tags:
  - python
  - learning
link: https://wiki.python.org/moin/BeginnersGuide
---
# Overview
Python is an oriented-object programming language such as [[Perl]], [[Ruby]], [[Scheme]] or [[Java]]. 
- It comes with a Standard Library that can connect to the Web, search text with regex and interact with files.
- It can be extended with other languages with new modules.
## More technical features:
- Comes with basic data types such as **numbers** (floating-point, complex and arbitrary precision integers), **strings** (ASCII and Unicode), **lists** and **dictionaries**.
- Code can be grouped into **modules** and **packages**.
- **raise** and **catching** exceptions.
- it supports **Generators** and **List Comprehension**.
## Here is a list of simple programs 
The full list of [Simple Programs](https://wiki.python.org/moin/SimplePrograms)
### Hello World!
The first program that everyone should make:
```python
print("Hello, World!")
```
### Input:
Program that handles an input from the terminal:
```python
name=input("What's your name?")
print(f"Hi, {name}")
```
### For with built-in Enumerate function:
```python
friends = ['sabrina', 'raul', 'eduarda', 'lucas']
for i, name in enumerate(friends):
	print(f'{i}:{name}')
```
### Fibonacci with Tuple assignment:
```python
parents, babies = (1, 1)
while babies < 100:
	print(f'This generation has {babies} babies')
	parents, babies = (babies, parents+babies)
```
### Create function:
```python
def greetings(name):
	print(f'Hello, {name}')
	
greetings('sabrina')
greetings('gabriel')
```
### Regex Phone Validation example:
```python
import re
test_strings = ['555-1212', 'ILL-EGAL']
for i, test_string in enumerate(test_strings):
    if re.match(r'^\d{3}-\d{4}$', test_string):
        print(f'{i}:',test_string, 'is a valid US local phone number')
    else:
        print(f'{i}:',test_string, 'rejected')
```
Vou deixar mais para o futuro para entender como que essas regex funcionam.
### Dictionaries, generator expressions:
```python
prices = {
    'apple' : 0.40,
    'banana' : 0.50
}

purchase = {
    'apple' : 1,
    'banana' : 6
}

grocery_bill = sum(prices[fruit] * purchase[fruit] for fruit in purchase)
print(f'I owe the grocer ${grocery_bill:.2f}')
```
Uma coisa interessante de se notar é que podemos fazer a listagem de frutas através de $\texttt{for fruit in purchase}$, sendo que purchase possui um dicionário. Isto é, esse for lista os elementos-chave dentro da relação chave-valor do dicionário. Veja que alternativamente poderíamos fazer $\texttt{for fruit in prices}$.
### Using arguments from the command line:
```python
import sys
try:
	total = sum(int(arg) for arg in sys.argv[1:])
except ValueError:
	-> Lidar com um erro esperado
```
### Opening Files:
```python
from pathlib import Path 

python_files = Path().glob('*.py')
for python_file in python_files:
    print(f'---------{python_file}---------')
    with open(python_file) as f:
        for line in f:
            print('    ' + line.rstrip())
```
This code uses the **pathlib** package.
### Time and Conditionals:
```python
from time import localtime

activities = {
    8 : 'Sleeping',
    9 : 'Commuting',
    17 : 'Working',
    18 : 'Commuting',
    20 : 'Eating',
    22 : 'Resting'
}

time_now = localtime()
hour = time_now.tm_hour
minute = time_now.tm_min
seconds = time_now.tm_sec

print(f'Local time hour is {hour}:{minute}:{seconds}')
for activity_time in sorted(activities.keys()):
    if hour < activity_time:
        print(activities[activity_time])
        break
else:
    print('Unknown, AFK or sleeping!')
```
### Triple Quote Strings:
```python
REFRAIN = '''{} bottles of beer on the wall,
{} bottles of beer,
take one down, pass it around,
{} bottles of beer on the wall!'''
bottles_of_beer = 9
while bottles_of_beer > 1:
    print(REFRAIN.format(bottles_of_beer, bottles_of_beer, bottles_of_beer-1))
    bottles_of_beer -= 1
```
### Classes:
```python
class BankAccount:
    def __init__(self, initial_balance=0):
        self.balance = initial_balance
    def deposit(self, amount):
        self.balance += amount
    def withdraw(self, amount):
        self.balance -= amount
    def overdrawn(self):
        return self.balance < 0
    
my_account = BankAccount(15)
my_account.withdraw(50)
print(my_account.balance, my_account.overdrawn())
```

## IDEs divulgated:
There is an extensive list of IDEs at this [link](https://wiki.python.org/moin/IntegratedDevelopmentEnvironments), there is a especial one that is [Thonny](https://thonny.org/)

## Learning Python:
There are plenty of resources to learn to program. 
[Python for new programmers](https://wiki.python.org/moin/BeginnersGuide/NonProgrammers)
[Python for programmers](https://wiki.python.org/moin/BeginnersGuide/Programmers)
[Materiais em Português](https://wiki.python.org/moin/PortugueseLanguage)
[List of Introductory Books](https://wiki.python.org/moin/IntroductoryBooks)
[General List of Books](https://wiki.python.org/moin/PythonBooks)
## Quiz and Exercises:


## Interesting Topics:
[Math related to Python](https://wiki.python.org/moin/BeginnersGuide/Mathematics)