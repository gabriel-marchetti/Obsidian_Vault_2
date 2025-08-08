![[Pasted image 20250626152820.png | center]]
Note que esse problema é similar ao problema da mochila onde devemos maximizar o lucro gerado pelos itens coletados. Desse modo, vamos traduzir o problema de cima para o problema da mochila: Podemos entender que a capacidade de transmissão do Fio que conecta a cidade origem com a cidade destino é a capacidade que a bolsa tem, portanto, B é a capacidade de transmissão. Assim, nos basta selecionar o conjunto de atividades que maximize o lucro.

Vamos definir estados para o nosso problema. Defina um estado do problema Estado(k, M) como: existem os eventos {1, 2, ..., k} e temos M bytes livres para ser transmitidos pelo Fio. Desse modo, veja que podemos montar uma subestrutura ótima para o nosso problema. No estado Estado(k, M) devemos nos perguntar se o evento $k$ deve participar da transmissão, note que temos duas possibilidades:
$$
\texttt{Estado(k, M)} = max(\texttt{Estado(k-1, M), Estado(k-1, M}-b_k))
$$
Veja que a primeira parte indica que escolhemos não transmitir a transmissão $k$ através do cabo, enquanto a segunda considera que estamos transmitindo o evento $k$ através do fio. Desse modo, a subestrutura ótima do nosso problema se reduz a:

$$
Estado(k, M) = 
\begin{cases}
    Estado(k-1, M) \text{, Se } b_k > M  \\ \\
    max(Estado(k-1,M), Estado(k-1, M - b_k)), \text{Se } b_k \leq M
\end{cases}
$$
Veja que os casos base são facilmente definidos:
- $Estado(0, M) = 0$, pois não há eventos a serem transmitidos.
- $Estado(k, 0) = 0$, pois não há capacidade de envio pelo fio.

Portanto, o algoritmo se reduz a preencher uma tabela de Estados do nosso problema:

Segue um vídeo explicando como construir a tabela para encontrar o lucro máximo gerado.
![[mc458_lista2_exerc1.mp4 | center]]

Agora precisamos gerar uma lista que retorne os eventos que devem ser transmitidos através do cabo.


![[mc458_lista2_exerc2p2.mp4]]Um pseudocódigo para esse problema pode ser feito através de:

```
Algoritmo ALM (Acha Lucro Máximo):
Entrada: uma lista de eventos E = {1, 2, ..., n} cada evento possui um custo b_i e gera lucro v_i. Além disso, um valor B denotando o máximo de bytes que pode ser transmitido.
Saída: Tabela de programação dinâmica que resolve o problema.

1. Para j = 0 .. n faça dp[j, 0] <- 0
2. Para j = 0 .. B faça dp[0, j] <- 0

3. Para j = 1 .. n faça:
	3.1 Para M = 1 .. B faça: 
		3.2 dp[j, M] <- dp[j-1, M]
		3.3 Se M - b_j >= 0 e dp[k-1, M - b_j] > dp[k, M] então:
			3.4 dp[k, M] = dp[k-1, M - b_j]
```
A Complexidade desse algoritmo é $O(n \cdot B)$.

Para ver quais transmissões serão transmitidas faça:
```
Algoritmo ETT (Encontra Transmissões Transmitidas):
Entrada: Tabela de programação dinâmica dp.
Saída: Lista de eventos a serem adicionados.

Inicialize:
i <- n
j <- B
lista_eventos <- []

Enquanto dp[i, j] != 0:
	Se dp[i-1, j] == dp[i, j]:
		i <- i - 1
	Senão:
		lista_eventos + {i}
		j <- B - b_i 
		i <- i - 1
```
