---
tags:
  - videos-assistidos
---
1x por Dia leia uma doc que você não leu (10 minutos).
- Se você não souber o que a documentação está dizendo, então você está programando por coincidência.
- por exemplo: floats, decimals, tolerancia relativa e absoluta, performance de strings, boolean, short circuit e memória.

```python
from math import isclose

x = 0.1 + 0.2
y = 0.3

print(isclose(x, y))
```

o $\texttt{isclose()}$ define tolerância absoluta e tolerância relativa. 
Outra maneira de lidar com esse problema é o seguinte:

```python
from decimal import Decimal

x = Decimal("0.1") + Decimal("0.1") + Decimal("0.1")
y = Decimal("0.3")

print(x == y)
```
OBS: Usa-se o argumento em string dentro do decimal para não haver conversão

Comentário sobre comportamento de **True** e **False** como números. 

Short Circuiting - É o comportamento que você utiliza operadores lógicos para definir uma sequência de ações.