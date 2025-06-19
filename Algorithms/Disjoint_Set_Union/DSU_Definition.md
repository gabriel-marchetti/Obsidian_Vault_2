Imagine que tenhamos um grafo não direcionado com N vértices inicialmente sem arestas. De modo que, serão feitas M queries de dois tipos:
1) Para cada query do tipo 1 será adicionada uma nova aresta entre dois vértices U e V.
2) Para cada query do tipo 2 deve ser checado se dois vértices A e B pertencem à mesma componente.

Uma abordagem mais intuitiva seria fazer algo como:
- Em queries do tipo 1 adicione as arestas de U -> V e V -> U.
- Em queries do tipo 2 faça a busca e veja se A atinge B. Pode ser tanto a DFS ou a BFS.

Apesar das queries do tipo 1 serem facilmente resolvidas, pois inserir um vértice em uma lista de adjacência é simples. A parte de busca é O(N), então no total ficaríamos O(M * N).

**Estrutura da DSU:**
Todo grafo é convertido para uma floresta, vértices que pertençam a uma mesma componente pertencerão a uma mesma árvore de uma DSU. Para verificar se dois vértices pertencem a uma mesma componente basta verificar a raiz da árvore que pertence na DSU. 

# **Operações da DSU:**
#### Find:
Basta encontrar o nó raiz da árvore. Então sua chamada será do tipo find(int x) que retorna o nó raiz da árvore de $x$ pertence. Note que podemos representar isso através de um array com o nó raiz de cada vértice, isto é. 

Inicialmente, $parent[i] = i$, para $0 \leq i \leq N$.
#### Join:
Note que sempre iremos juntar dois vértices, desse modo, a sua chamada será join(int a, int b).

Queries do tipo 1: Join(U, V).
Queries do tipo 2: Find(A) == Find(B).

**Problema:** Podemos criar árvores degeneradas. Isto é, se escolhermos arbitrariamente um dos nós raízes para se tornar o ancestral dos vértices, então podemos juntar de modo a formar uma lista ligada. Note que isso provocaria o efeito de que a mesma complexidade do procedimento de busca padrão.

**Otimizações da DSU:**
**Path Compression) O(log N)**
Toda vez que chamarmos uma operação de find iremos fazer um path compression. Enraizamos todos os nós ao nó raiz.

**Union By Ranking) O(log N)**
Atua no Join, além de termos um array com os pais de cada vértice iremos também armazenar o ranking de casa vértice.
$rank[i]$ : árvore com raiz i tem profundidade $rank[i]$.
Desse modo, escolha a árvore com maior $rank$ para que para que ela seja o pai da árvore de menor $rank$a. No caso de ambas árvores possuírem mesmo rank é impossível fazer um Join sem aumentar o rank.

Note que a altura da árvore no método do Union By Ranking é no máximo $log(N)$, pois pensemos o seguinte:
Um nó possui $rank = 0$.
Para que você possua uma árvore com $rank = 1$ você precisa unir duas árvores de $rank = 0$. Então, a árvore com $rank = 1$ possui ao menos dois vértices.
Como a árvore com $rank = 1$ possui ao menos dois vértices, então a árvore com $rank = 2$ possui ao menos 4 vértices.
Se quisermos juntar todos os N vértices, teremos então que o rank dessa árvore será $log (N)$.

OBS: Todos os problemas que envolvem DSU irão conter pelo menos uma das otimizações apresentadas.
Note que o Path compression degenera a estrutura de arestas dos nós.




