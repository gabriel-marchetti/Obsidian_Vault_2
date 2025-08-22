# Árvores Enraizadas:
Uma árvore enraizada é uma árvore que possui uma raiz. Se a árvore for direcionada, então deve haver um vértice, de modo que, se $T=(V,E)$ é uma árvore enraizada, então existe $r$ tal que:
$$
\begin{cases}
g^{-}(r) = 0 \\
g^{+}(v) = 1, \forall v \in V-\{ r \}
\end{cases}
$$
Obs: 
	$g^{-}(v)$ indica a quantidade de arestas que chegam em $v$.
	$g^{+}(v)$ indica a quantidade de arestas que saem de $v$.

Uma maneira de representar árvore enraizadas é através do vetor de predecessores.

## Vetor de predecessores.
![[Pasted image 20250818110058.png|center]]

