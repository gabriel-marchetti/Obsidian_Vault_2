---
tags:
  - python
  - programação
---

Dada a seguinte lista de frutas
```python
frutas = ['Uva', 'Melancia', 'Pessego', 'Abacate', 'Abacaxi']
```
Imprima a primeira fruta, a última fruta e troque o conteúdo do terceiro elemento para 'Banana'.
?
```python
frutas = ['Uva', 'Melancia', 'Pessego', 'Abacate', 'Abacaxi']

if __name__ == '__main__':
    print('Primeira fruta: ', frutas[0])
    print('Última fruta: ', frutas[-1])
    frutas[2] = 'Banana'
    for fruta in frutas:
        print(fruta, end=',')
    print()
```