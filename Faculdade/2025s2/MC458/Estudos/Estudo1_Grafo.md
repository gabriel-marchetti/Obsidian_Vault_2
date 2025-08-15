Nessa sessão de estudos foram contemplados os seguintes conteúdos:
- Multigrafo: Um grafo que possui laço ou múltiplas arestas.
- Grafo Completo: Um grafo com todas as arestas possíveis e sem laço.
- Grau do Vértice: Número de arestas incidentes sobre um vértice (laços contam como dois).
	- [[Estudo1_Grafo#Handshake Theorem|Handshake Theorem]]
- Grafo Complementar:
	- Exercicio1_graf_comp
	- Exercicio2_graf_comp
- Passeios:
	- Passeio fechado
	- Caminho
	- Ciclo
		- Exercicio1_passeio
		- Exercicio2_passeio
		- Exercicio3_passeio


### Handshake Theorem
$$
\sum_{v \in V}^{} d(v) = 2 |E|
$$
OBS: A prova aqui é feita por indução, mas o recurso mais útil é pensar intuitivamente o que está acontecendo. Veja que como $|E|$ arestas são inseridas e cada aresta possui duas extremidade, sendo que cada extremidade aumenta o grau de um vértice em 1, então fica claro o que o teorema quer dizer.

### Grafo Complementar
Dado um grafo $G=(V,E)$ existe 