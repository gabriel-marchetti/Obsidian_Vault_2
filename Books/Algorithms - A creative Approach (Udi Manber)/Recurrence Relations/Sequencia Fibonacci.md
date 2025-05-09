Temos a relação de recorrência:
$$
F(n) = F(n-1) + F(n-2) \hspace{50pt} F(1) = 1,\quad F(2) = 1
$$
Queremos encontrar uma função $g(n)$ tal que $F(n) \in O\left( g(n)\right)$. Um primeiro chute, pode ser pensar que cada nova chamada invoca duas outras chamadas, isto é:
![[Pasted image 20250409143127.png]]
Veja que, assumir que cada chamada invoca outras duas chamadas é um teto para o problema. Logo, $F(n) \in O(2^n)$, contudo, veja que:
$$
F(n) = F(n-1) + F(n-2) \implies c \cdot 2^n = c \cdot 2^{n-1} + c \cdot 2^{n-2} \implies 2^n = 2^{n-1} + 2^{n-2}
$$
Note que o lado direito é superior ao lado esquerdo da equação, então o fator verdadeiro não é de $2^n$, supondo que $F(n) \in O(a^n)$. Podemos perceber que:
$$
a^n = a^{n-1} + a^{n-2} \implies a^2 = a + 1 \implies a^2 - a - 1 =0
$$
Utilizando Bháskara
$$
\begin{align}
\Delta = b^2 - 4ac \implies & \Delta = 5 \\ 
 & a_{12} =  \frac{-b \pm \sqrt{\Delta}}{2a} \implies a_{12} = \frac{1 \pm \sqrt{5}}{2}
\end{align}
$$
Note que $a_1 \approx 1.61$, então o fator de crescimento de Fibonacci é $F(n) \in 1.61^n$

