---
tags:
  - algorithms
  - sorting
---

O Insertion Sort apesar de não ser muito eficiente para um array de tamanho grande, ainda sim apresenta vantagens como:
- Implementação Simples
- Eficiente para dados pequenos arrays
- Mais eficiente que outros algoritmos com complexidade $O(n^2)$ como o [[Bubble_Sort]] ou o [[Selection_Sort]].
- Eficiente para arrays já parcialmente ordenados.

O motivo dele ser eficiente para problemas que apresentam estruturas já ordenadas é o seguinte: Imagine que o elemento original não esteja mais do que $k$ elementos distante da sua posição final. Então o algoritmo roda em $O(nk)$. (Por quê?) -> O algoritmo "explica".

# Aplicações:
- Uma primeira aplicação é justamente a ordenação de vetores de tamanho pequeno.
- Ordenar as cartas na sua mão em um jogo de baralho. Veja que se você não segura mais do que 5 cartas, então o comportamento é $O(5n)$.


# Funcionamento:
![[Insertion-sort-example-300px.gif | center]]
O funcionamento do insertion sort é apresentado como na figura. Suponha que tenhamos um vetor que já esteja ordenado, para inserir um novo elemento de modo que o vetor ainda permaneça ordenado é preciso encontrar a posição em que o novo elemento deve ser inserido (dai o nome). Assim, basta que todos os elementos maiores que tal elemento sejam movidos à direita abrindo espaço para o elemento.
A prova indutiva desse processo pode ser feita através de:
Seja P(i) o predicado do vetor com $i$ elementos estar ordenado:
Para o caso do InsertionSort(1): Temos que um vetor com um único elemento está ordenado, portanto, P(1).
Assumindo por Indução temos que a chamada InsertionSort(n) ordene o vetor com $n$ elementos. Dada a inserção de um novo elemento, se soubermos dividir o vetor em uma sequência dos valores menores ou iguais que o novo elemento (e ordenados entre si) e os elementos maiores que esse novo elemento. Então basta colocar tal elemento entre as duas sequências. Desse modo temos que $P(n) \implies P(n+1)$ e, portanto, InsertionSort(n+1) ordena o vetor com n+1 elementos.

# Algoritmo:
```python
function insertion_sort_recursive(array A, int n)
	if( n <= 0 ) return # Caso base
	insertion_sort_recursive(A, n - 1) # Chamada recursiva
	x <-- A[n]
	j <-- n - 1
	while( j > 0 && A[j] > x )
		A[j+1] <-- A[j]
		j <-- j - 1
	A[j+1] = x
```

Uma maneira iterativa do problema é fazer um for
```python
function insertion_sort(array A, int n)
	for i = 2 .. n:
		x <-- A[i]
		j <-- i - 1
		while j > 0 and A[j] < x:
			A[j+1] <-- A[j]
			j <-- j - 1
		A[j+1] <-- target
```
Note que os algoritmos não diferem em questão da complexidade temporal, contudo a versão recursiva fará O(n) chamadas na pilha, portanto, a complexidade espacial é O(n)

# Complexidade:
$$
\begin{cases}
T(1) = \Theta(1) \\ \\
T(n) = T(n-1) + \Theta(n)
\end{cases}
$$
Essa complexidade resulta em $O(n^2)$ para a complexidade temporal para o pior caso.
Contudo, para o melhor caso há apenas uma verificação por iteração, então o problema se torna $O(n)$.

Complexidade melhor caso: $O(n)$
Complexidade pior caso (array ordenado invertido): $O(n^2)$

### Flashcards
Quais são as principais vantagens de se usar o InsertionSort?
?
- Simples implementação
- Eficiente para entradas de tamanho pequeno
- Já eficiente para arrays parcialmente ordenados
- Tende a ser mais eficiente que outros algoritmos de ordenação que estão na classe $O(n^2)$
<!--SR:!2025-05-10,3,250-->

Dê um argumento do porquê o algoritmo de ordenação por inserção é eficiente para ordenar vetores parcialmente ordenados
?
Se os vetores estão parcialmente ordenados, então cada elemento deve mover no máximo $k$ vezes até atingir sua posição. Desse modo, a complexidade fica $O(k*n) = O(n)$. Pense que daí vem a eficiência para vetores de pequeno tamanho.
<!--SR:!2025-05-11,4,270-->

Quais são as complexidades (melhor caso e pior caso) para o InsertionSort
?
Complexidade Melhor caso: $O(n)$
Complexidade Pior caso: $O(n^2)$
<!--SR:!2025-05-11,4,270-->

Implemente o Insertion Sort
?
Resposta em [[Insertion_Sort]]
