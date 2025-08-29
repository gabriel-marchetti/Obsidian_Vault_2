A teoria de grafos é muito poderosa, pois pode modelar uma diversa variedade de problemas. Desse modo, se torna uma ferramenta poderosa para o programador educado. Esse grande poder dos grafos vêm da ideia de que grafos podem ser usados para representar qualquer tipo de "relationship" (eu acho que relacionamento/relação não fica tão claro aqui).
Veja que algumas das aplicações são:
- Representação do esquema rodoviário de uma cidade.
- Representação de um circuito elétrico.
- Representação de uma rede de computadores.
- Representação de um sistema de distribuição de um país.
- Representação de relacionamentos em um grupo de humanos.
Veja que as aplicações são diversas.

A grande questão aqui é converter o seu problema para o contexto de Grafos. Caso essa conversão seja bem sucedida, utilizar a teoria bem estabelecida de grafos irá retornar propriedades muito interessantes do seu problema.
"It is amazing how often messy applied problems have a simple description and solution in terms of classical graph problems."
Além disso, temos que implementar algoritmos de grafos verdadeiramente novos pode ser uma tarefa bem complicada. Portanto, entender os conceitos e aplicações de um algoritmo para grafo pode ser muitas vezes mais importante do que saber a implementação por si só.

# Flavors of Graphs.
Um grafo é uma estrutura $G=(V,E)$ e a sua conversão para um problema deve ser feita de uma maneira até intuitiva em alguns casos:
- Uma malha rodoviária é representada com as cidades sendo os vértices. Uma aresta está presente em $G$ caso as cidades $i$ e $j$ estejam conectadas.
- Uma representação de rede social tem seus usuários como vértices e haverá uma aresta caso duas pessoas sejam amigas dentro dessa rede.
Alguns casos podem ser mais complexos.
- Suponha que desejamos modelar programas através de grafos. Cada linha do código representa um vértice dentro do grafo. Dados os vértices $i$ e $j$, a existência da aresta $(i,j)$ ocorre se a execução da linha $j$ pode ocorrer depois da execução da linha $i$.

## Properties of a Graph.
As propriedades de um grafo (ou as propriedades de um problema) podem determinar as estruturas de dados e algoritmos utilizados para resolver o problema. 

- **Undirected vs Directed**: 
	Um grafo $G=(V,E)$ é **Undirected** $(i,j)\in E \implies (j,i) \in E$. 
	No caso de um grafo **Directed** $(i,j) \in E \centernot\implies (j,i) \in E$.
	Veja que alguns modelos de rodovias podem ser modelados através de um Grafo **Undirected**, pois rodovias geralmente têm vias de mão dupla.
	Contudo, uma malha de uma cidade pequena deve conter ruas/avenidas de mão única.
	No exemplo do fluxo de execução de um código é necessário representar o grafo através de um grafo direcionado, pois o fluxo de um código é constante para "frente" apenas voltando em "Branches".
- **Weighted vs Unweighted**:
	Um grafo **Weighted** podemos ter associado um valor numérico para um vértice ou para uma aresta. 
	Um grafo **Unweighted** não há uma distinção clara entre os valores numéricos entre os vértices e arestas.
	Essa diferença fica mais clara quando olhamos para o algoritmo de caminhos mínimos. Em problemas com grafos **Unweighted** o problema se reduz a encontrar o caminho com menor número de arestas. Veja que essa redução não é tão simples quando colocamos pesos nas arestas. Desse modo, grafos diferentes devem admitir algoritmos diferentes para resolvê-los.
![[Pasted image 20250826111208.png|center|420x300]]
![[Pasted image 20250826111522.png|center|420x300]]
Veja que os grafos apresentam caminhos diferentes sobre óticas diferentes.

- **Simple vs Non-Simple**: 
	*Self-Loops* que consistem em arestas conectando o mesmo vértice podem impedir o funcionamento de alguns algoritmos. Portanto, há um *Self-Loop* caso $(x,x) \in E$, para qualquer $x \in V$.
	*Multi-Edge* que consistem em diversas arestas conectando o mesmo par de vértices.
**OBS:** Ambas propriedades necessitam de uma implementação especial dos algoritmos. (Como são essas implementações?)
- **Sparse vs Dense**:
	Um grafo é dito **Sparse** se há uma quantidade de arestas na ordem de $\Theta(n)$.
	Um grafo é dito **Dense** se há uma quantidade de arestas na ordem de $\Theta(n^2)$.
	Um grafo é **Completo** se possui todas as possíveis arestas, considerando que o grafo seja simples, portanto contém $\displaystyle\binom{n}{2}$ arestas. 
	Veja que a aplicação de grafos esparsos é mais comum do que parece. Você provavelmente encontrará diversas conexões de ruas que conectam no máximo 4 ruas distintas, dificilmente você verá uma conexão com 5, 6, 7, ... ruas em uma mesma junção. Por conta disso, uma modelagem de ruas é através de um grafo esparso.
	O mesmo argumento pode ser feito para circuitos elétricos.

- **Cyclic vs Acyclic**:
	Um grafo é dito Cyclic se existe um caminho fechado com ao menos 3 vértices e todos os vértices são diferentes, excluindo o começo do caminho.
	Um grafo é Acyclic se não é Cyclic.
	Uma árvore é definida através de: É um grafo sem direção, conexo e Acyclic.
	Uma aplicação interessante de grafos Acíclicos é através de **DAG**s(Directed Acyclic Graphs). **DAG**s surgem naturalmente em **Scheduling problems** onde uma ação $x$ deve ocorrer antes de uma ação $y$. Uma outra aplicação é o **Topological Ordering** que é uma ordenação respeitando a ordem de precedência de um **DAG**. Portanto, a primeira ação deve ocorrer antes de qualquer ação subsequente, a segunda ação deve ocorrer antes de todas as ações menos da primeira e assim por diante.

- **Embedded vs Topological**:
	A representação $G=(V,E)$ é uma representação puramente topológica do Grafo. Se houver posicionamento geométricos para cada vértice e aresta dizemos que o grafo é **Embedded**. Desse modo, qualquer desenho de um grafo é um grafo **Embedded**, mas nesse caso isso pode não ter significância algorítmica. 
	O problema do **Traveling Salesman** define um conjunto de pontos no plano cartesiano e devemos escolher o caminho de custo mínimo que conecta esses pontos. Veja que não precisamos armazenar as arestas do grafo, de modo que dado dois pontos nós podemos calcular o comprimento da aresta, desse modo temos que as arestas estão embarcadas dentro do vértices.
	O mesmo pode ser dito para um problema de labirinto dentro de uma matriz de representação. Células vizinhas possuem arestas, mas a utilização de uma representação não é necessária nesse caso.

- **Implicit vs Explicit**:
	Um grafo é implícito quando não precisamos contruí-lo primeiro para depois resolvê-lo. Na medida que resolvemos o problema construímos o grafo. 
	Um problema de **Web-Scale Analysis** é um exemplo em que podemos baixar conteúdos de interesse primeiro antes de baixar uma página completa. Veja que na medida que executamos podemos descartar ou considerar as opções.
	Um outro exemplo é a representação em grafo de um **Backtrack-Search** veja que um ramo pode ser desconsiderado a partir de um certo critério.
	Uma outra questão interessante sobre grafos implícitos é a seguinte, eu só saberei os vizinhos dos meus vizinhos caso eu pergunte para esse vizinhos quais são seus vizinhos.

- **Labeled vs Unlabeled**: 
	Um grafo com rótulo é um grafo que cada vértice possui um identificador único. 
	A maioria das aplicações irá rotular um vértice, contudo uma aplicação que utiliza grafos sem rótulo é através do **Isomorphism Testing** que irá comparar se a estrutura de dois grafo é igual.


**Take-Home Lesson**: Grafos podem ser usados para modelar uma grande variedade de problemas e relacionamentos. Desse modo, saber sobre a terminologia da teoria de grafos nada mais é que uma maneira de se comunicar com o problema e descobrir propriedades interessantes.

# Data Structures for Graphs.
As duas estruturas de dados básicas para armazenar grafos são as **matrizes de adjacência** e **listas de adjacência**.

Para ambos exemplos suponha que $n$ é o número de vértices e $m$ é o número de arestas.
## Matriz de Adjacência.
Representamos um grafo $G$ através de uma matrix $M_{n \times n}$. Se a aresta $\texttt{M[i, j]} = 1$, se $(i,j)\in E$ e $\texttt{M[i, j] = 0}$, caso contrário.
**Vantages**:
- Rapidamente podemos responder se $(i,j)$ pertence ao Grafo.
- Rapidamente podemos inserir e remover arestas do Grafo.
**Desvantagens**:
- Pode usar uma quantidade muito grande de espaço para grafos com muitos vértices e poucas arestas.

# Lista de Adjacência.
Representamos um grafo $G$ através de um array, em que cada elemento corresponde a uma lista encadeada. A lista encadeada armazena os vizinhos do vértice em questão.

