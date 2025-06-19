Dada a lista de números $\texttt{numeros = [1,2,3,4,5]}$ imprima o dobro de cada número:
?
A primeira implementação é:
```python
numeros = [1, 2, 3, 4, 5]

for numero in numeros:
    print(2*numero, end=',')
```
Mas um jeito melhor de fazer isso é através de:
```python
numeros = [1, 2, 3, 4, 5]

print(','.join(str(2*n) for n in numeros))
```