---
tags:
  - math
---
## Sum of Squares

Queremos resolver (encontrar uma fórmula fechada) para o seguinte somatório: $\displaystyle \sum_{k=1}^{n} k^2$
Para isso podemos observar que:
$$
\begin{align}
  n^3 - &(n-1)^3 = &3n^2 - &3n  &+1 \\
  (n-1)^3 - &(n-2)^3 = &3(n-1)^2 - &3(n-1)  &+1  \\
  (n-2)^3 - &(n-3)^3 = &3(n-2)^2 - &3(n-2)  &+1 \\
  &\vdots &\vdots &\vdots &\vdots \\
1^3 &- 0^3 &= 3\cdot 1^2 &- 3 \cdot 1 &+ 1
\end{align}
$$
Veja que se somarmos todas as linhas, teremos que os fatores ao cubo se cancelarão e ficaremos com:
$$
\begin{align}
n^3 &= 3\cdot\sum_{k=1}^{n} k^2 - 3\sum_{k=1}^{n}k+n  \\
n^3 &= 3\cdot\sum_{k=1}^{n} k^2 - 3\frac{(n+1)\cdot n}{2} + n \\
n^3 +3\cdot \frac{(n+1)\cdot n}{2} - n &= 3\cdot\sum_{k=1}^{n} k^2  \\
\sum_{k=1}^{n} k^2 &= \frac{n\cdot(n+1)\cdot(2n+1)}{6}
\end{align}
$$
## Flashcards
Tente deduzir a fórmula para $\sum k^2$
?
A resposta está em [[Summations]]




