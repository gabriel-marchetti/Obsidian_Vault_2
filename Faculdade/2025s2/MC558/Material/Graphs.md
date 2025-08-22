
# Representation of Graphs:
As duas principais representações são: [[Graphs#Matriz de adjacência|Matriz de adjacência]] e [[Graphs#Lista de adjacência|Lista de adjacência]].

## Matriz de adjacência:
Seja $G = (V, E)$ um grafo, então a matriz de adjacência é representada por:
$$
A[i,j] = 
\begin{cases}
1, \text{Se } (i,j) \in E \\ \\
0, c.c.
\end{cases}
$$
Note que a matriz é uma matriz quadrada sendo a dimensão da matriz $|A| \times |A|$
![[Pasted image 20250818105046.png|center]]
## Lista de adjacência:
A lista de adjacência segue uma ideia de não alocar todo o espaço de uma matriz quadrada. De modo que cada vértice do grafo possui uma lista encadeada de modo a guardar os vizinhos desse vértice.
![[Pasted image 20250818105219.png|center]]
