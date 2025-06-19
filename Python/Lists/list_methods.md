Dentro do python temos diversos métodos para lidar com listas eles são:
- [[#list.append(x)]]
- [[#list.extend(iterable)]]
- [[#list.insert(i, x)]]
- [[#list.remove(x)]]
- [[#list.pop([i])]]
- [[#list.clear()]]
- [[#list.index(x [, start[, end )]]
- [[#list.count(x)]]
- [[#list.reverse()]]
- [[#list.copy()]]
- [[#list.sort()]]

### list.append(x)
Adiciona um elemento no final da lista. É similar a utilizar o seguinte comando:
```python
a[len(a):] = [x]
```
Exemplo:
```python
a = [1, 2, 3, 4]
a.append(5)
print(a) # deve retornar [1, 2, 3, 4, 5]

a = [1, 2, 3, 4]
a[len(a):] = [5]
print(a) # deve retornar [1, 2, 3, 4, 5]
```
### list.extend(iterable)
Estende uma lista com o conteúdo de uma outra lista ou iterable. A lista invocando o comando é modificada. Além disso é equivalente a:
```python
a[len(a):] = iterable
```
```python
a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
a.extend(b) # Modifico a
print('Conteudo a: ', a) # deve retornar [1, 2, 3, 4, 5, 6, 7, 8]
print('Conteudo b: ', b) # deve retornar [5, 6, 7, 8]


a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
a[len(a):] = b
print('Conteudo a: ', a) # deve retornar [1, 2, 3, 4, 5, 6, 7, 8]
print('Conteudo b: ', b) # deve retornar [5, 6, 7, 8]
```
### list.insert(i, x)
Aqui inserimos um elemento na posição 'i' só que com o adicional de que os elementos que ocupavam as posições [i..len(list)-1] são movidos em uma unidade à direita, abrindo espaço para o elemento x.
Note que podemos fazer um análogo do append através de:
```python
a.append(x) === a.insert(len(a), x)
```
Exemplo:
```python
print('Insert')
a = [1, 2, 3, 4]
a.insert(1, 10) # [1, 10, 2, 3, 4]
a.insert(0, 11) # [11, 1, 10, 2, 3, 4]
```
### list.remove(x)
Remove a primeira aparição do elemento 'x' dentro da lista. Caso o elemento não seja encontrado haverá o erro <mark style="background: #FF5582A6;">ValueError</mark>, portanto, podemos utilizar o try...except para verificar a existência de um elemento dentro da lista.
```python
a = [x for x in range(10)]
a.remove(5) # [0, 1, 2, 3, 4, 6, 7, 8, 9]
try:
    a.remove(11)
except ValueError:
    print('Elemento não encontrado') # Essa linha deve ser rodada
```
Note que também podemos remover todos os elementos x dentro do vetor
```python
a = [x % 10 for x in range(58)]
try:
    while(True):
        a.remove(5)
except:
    print('Todos os 5s foram removidos')
```
### list.pop([i])
Quando especificado o índice 'i' remove o elemento da posição e desloca todos os elementos que antes ocupavam posição à direta uma unidade à esquerda. Caso não seja especificado nenhum índice ocorre a remoção do último elemento.
Para índices que não fazem sentido haverá o erro 
### list.clear()
Remove todos os elementos da lista em questão. É similar ao comando:
```python
del a[:]
```
### list.index(x [, start[, end]])
Encontra a primeira ocorrência de $x$ dentro do vetor. Caso não seja encontrado o valor há um <mark style="background: #FF5582A6;">ValueError</mark>.
Os parâmetros adicionais $start$ e $stop$ sever pare definir o campo da lista que estamos buscando. Com o mesmo detalhe de que se um elemento não está dentro da lista então há um <mark style="background: #FF5582A6;">ValueError</mark>.
### list.count(x)
Conta o número de ocorrências de $x$ dentro de $list$.
### list.reverse()
Inverte a lista. Pode ser útil para fazer um sort invertido.
### list.copy()
Aqui fazemos um Shallow Copy para estruturas de dados através de referência. Veja que para estruturas básicas como um inteiro, serve praticamente como um deep copy. É similar a:
```python
a = []
b = [i for i in range(10)]
a = b[:]
# É igual a 
a = b.copy()
```
### list.sort()
Pode ser basicamente utilizado para ordenar a lista.
Nem toda estrutura de dado pode ser comparável.

## OBS:
O retorno para métodos de mutação de lista como o $reverse$,$remove$,$sort$ retornam None. Isso parte de um princípio de design em python que estruturas de dados mutáveis não retornam nada quando mutadas.


# Creating a Stack with Lists.
Seguindo a ideia de que uma $Stack$ possui o princípio Last-In First-Out(LIFO) para adicionar um item na lista basta realizar o $append$ e para descobrir o próximo elemento basta fazer um $pop$ do último elemento.

# Creating Queues with Lists.
É possível implementar uma estrutura de Fila através de listas. Contudo, o problema aqui é que é extremamente ineficiente retirar elementos da primeira posição de uma lista.

Um modo de comparar isso é através de:
```python
import time
import timeit
from collections import deque

class Queue:
    def __init__(self, queue):
        self.queue = queue
        self.nElem = len(queue)
    def __str__(self):
        return f"nElem:{self.nElem}\n{self.queue}"
    def pop(self):
        if self.nElem == 0:
            print('Não há nenhum elemento na fila.')
            return None
        self.nElem -= 1
        return self.queue.pop(0)
    def add(self, elem):
        self.queue.append(elem)
        self.nElem += 1 

def add_python_queue():
    pQueue.append(400)

def add_my_queue():
    mQueue.add(400)

def pop_my_queue():
    mQueue.pop()

def pop_python_queue():
    pQueue.pop()

a = [i for i in range(10000)]
mQueue = Queue(a[:])
pQueue = deque(a[:])

if __name__ == '__main__':
    time_my_queue = timeit.timeit(add_my_queue, number = 1000)
    time_python_queue = timeit.timeit(add_python_queue, number = 1000)

    print(f'Tempo médio execução de Add em MyQueue: {time_my_queue/1000:.8f} segundos')
    print(f'Tempo médio execução de Add em PythonQueue: {time_python_queue/1000:.8f} segundos')
    print(f'myQueue/pythonQueue = {time_my_queue/time_python_queue}')

    time_my_queue = timeit.timeit(pop_my_queue, number = 1000)
    time_python_queue = timeit.timeit(pop_python_queue, number = 1000)

    print(f'Tempo médio execução de Pop em MyQueue: {time_my_queue/1000:.8f} segundos')
    print(f'Tempo médio execução de Pop em PythonQueue: {time_python_queue/1000:.8f} segundos')
    print(f'myQueue/pythonQueue = {time_my_queue/time_python_queue}')
```
Nos retornar:
```
Tempo médio execução de Add em MyQueue: 0.00000013 segundos
Tempo médio execução de Add em PythonQueue: 0.00000005 segundos
myQueue/pythonQueue = 2.722689486672161
Tempo médio execução de Pop em MyQueue: 0.00000125 segundos
Tempo médio execução de Pop em PythonQueue: 0.00000004 segundos
myQueue/pythonQueue = 27.919826388168676
```
Veja que o tempo de execução do Add está bem mais próximo. A minha implementação demora cerca de três vezes mais que a implementação do Python. Enquanto a implementação do pop demora cerca de 28 vezes mais em tempo de execução.

# List Comprehensions.
É um método de criar listas dentro do python bem útil. Veja que um método verboso de criar uma lista como:
```python
squares = []
for i in range(10):
	squares.append(i**2)
```
Se torna mais compacto através de:
```python
squares = [x**2 for x in range(10)]
```
Outro modo de fazer isso é através de:
```python
squares = list(map(lambda x : x**2, range(10)))
```
Os dois modos apresentados destroem a variável $x$ enquanto o primeiro método ainda deixa possível utilizá-lo. Isso pode ser verificado tentando printar a variável $x$ após execução do programa.

Um lugar onde pode ser útil utilizar listcomp é na criação de listas com propriedades específicas como:
```python
points = [(x, y) for x in [1, 4, 9] for y in [1, 2, 3] if x != y]
print(points)
```
A lista criada será (1, 2), (1, 3), (4, 1), (4, 2), (4, 3), (9, 1), (9, 2), (9, 3).
Note que uma forma equivalente de fazer isso seria através de:
```python
points = []
for x in [1, 4, 9]:
	for y in [1, 2, 3]:
		if x != y:
			points.append((x, y))
```
Note que uma forma de decorar a forma apresentada com listcomp é a ordem dos operadores na ordem convencional.
Um exercício legal de se fazer com listcomp é o flatten de um vetor de vetores:
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flatten = [n for row in matrix for n in row]
print(flatten)
```
Árvore do pi:
```python
from math import pi
pies = [round(pi, i) for i in range(1,10)]
for e in pies:
    print(e)
```
Transposta de uma matrix através de listcomp:
```python
matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
matrix_T = [[row[i] for row in matrix] for i in range(4)]
print(matrix_T)
```