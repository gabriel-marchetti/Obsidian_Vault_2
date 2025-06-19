---
tags:
  - algorithms
  - sorting
---
O algoritmo de Selection_Sort geralmente atua pior que o [[Algorithms/Sorting/Insertion_Sort]]. Contudo, a sua vantagem com relação a algoritmos mais sofisticados de ordenação se refere ao fato de ele não consumir mais memória. 
Vantagens:
- O consumo de memória é praticamente o consumo do vetor
- Simplicidade implementação

# Ideia:
Começamos buscando o menor elemento do vetor A[1..n] encontrado o menor valor seja ele o valor A[j] troque-o de posição com A[1]. Agora iremos buscar o segundo menor elemento, achado o segundo menor elemento, troque-o de posição com o elemento A[2]. Faça esse processo até que não sobre nenhum elemento.

![[Selection-Sort-Animation.gif |center]]

Pseudocódigo:
```python
# Ordena o vetor A de tamanho n usando o SelectionSort.
SelectionSort(A, n):
	for i = 2 .. n:
		min = A[i]	
		for j = i + 1 .. n:
			min = Minimum(min, A[j])
		Troque a posição de A[j] com A[i]
```

O programa em c++ é:
```cpp
void selection_sort(std::vector<int> &arr)
{
    int n = arr.size();
    for(int i{0}; i < n; i++)
    {
        int cur_min = i;
        for(int j{i+1}; j < n; j++)
        {
            if(arr[cur_min] > arr[j])
            {
                cur_min = j;
            }
        }
        swap(arr, i, cur_min); 
    }
}
```
Onde $\texttt{swap}$ define uma função que troca $\texttt{i}$ com $\texttt{cur\_min}$.

## Complexidade:
Aqui não estamos tratando de uma relação de recorrência, então podemos simplesmente resolver através do somatório:
$$
\sum_{i=1}^{n} \sum_{j=i+1}^{n} \Theta(1) \approx \sum_{i=1}^{n} \sum_{j=i+1}^{n}1 = \frac{n \cdot (n-1)}{2} \in O(n^2)
$$
Note que tanto o pior caso quanto melhor caso estão englobados pela complexidade demonstrada acima, porque sempre temos que verificar qual o menor valor no vetor remanescente.

## Flashcards
Quais são os pontos positivos do SelectionSort?
?
- Pouco consumo de memória
- Fácil implementação
- Intuitivo

O SelectionSort possui vantagem em ser utilizado dentro de um vetor quase ordenado?
?
Não, pois sua complexidade sempre é $O(n^2)$
<!--SR:!2025-05-16,4,270-->

Implemente o SelectionSort
?
Resposta em [[Selection_Sort]]
