1 - O que diferencia o plano de controle do plano de dados em uma rede? Explique como essas duas funções se relacionam no processo de encaminhamento de pacotes
**Resposta**: O plano de controle se diferencia do plano de dados pelo escopo que eles atuam dentro de uma rede. O plano de dados está preocupado principalmente com o problema de "forwarding", ou seja, como um roteador deve encaminhar dados de chegada para a devida interface de saída, nesse sentido perceba que se trata de uma ação local. Enquanto o plano de controle está preocupado com o "routing" desses dados, portanto, ele se preocupa com uma visão global de como enviar esses dados entre hosts que passam por roteadores. Veja que eles se relacionam com o encaminhamento de pacotes, pois eles devem transitar esses pacotes pela rede com finalidades distintas, uma mais local e outra mais global.

2 - Compare algoritmos de roteamento centralizados e distribuídos. Em seguida, compare o roteamento estático e dinâmico. Em cada comparação, destaque uma vantagem e uma limitação.
**Resposta**: Temos dois grandes exemplos de algoritmos de roteamento, sendo um deles centralizado e outro distribuído, eles são, respectivamente, o algoritmo de Dijkstra e o algoritmo de Bellman-Ford, veja que uma vantagem do algoritmo distribuído é sua escalabilidade, pois possibilita que a computação de rotas seja distribuída entre os roteadores pertencentes da rede, mesmo que isso acabe gerando problemas de sincronia entre os roteadores gerando problemas como o "counting-to-infinity". Enquanto o algoritmo de Dijkstra possibilita encontrar o caminho mínimo de uma malha de rede de modo real, não sendo uma estimativa iterativa, contudo a limitação clara desse algoritmo é a complexidade de computação, exigindo não só a troca de mensagens na ordem de O(n^2) como também uma entidade que consiga conter as informações de toda a rede para fazer o roteamento.
Veja que o roteamento estático se refere a redes que possuem pouca variação das condições de links e dos roteadores, enquanto roteamento dinâmico é o contrário, portanto, está sugestível a grandes mudanças. O benefício de um roteamento estático é sua simplicidade, enquanto sua limitação é o fato de não lidar bem com variações. Enquanto o roteamento dinâmico tem como aspecto positivo o fato de possibilitar que dispositivos móveis se conectem com a rede, pois esses estão sujeitos a mudanças constantes. Enquanto a limitação é o aumento da complexidade da análise.

3 - Explique a diferença entre os algoritmos de estado de enlace e de vetor distância. Sua resposta deve comentar que informação cada roteador mantém, como ela é obtida e como a decisão de rota é tomada
**Resposta**: O algoritmo de estado de enlace se refere ao algoritmo de Dijkstra, enquanto o algoritmo de vetor de distância se refere ao algoritmo de Bellman-Ford. Dentro do algoritmo de Dijkstra, temos a obtenção de um caminho mínimo entre dois nós (ou hosts dentro de redes), contudo para adquirir essa resposta o algoritmo deve ter como entrada a topologia completa da rede e retornará a distância mínima entre um nó source e todos os outros nós, assim como uma árvore de ancestralidade. O processo ocorre através de uma fila que irá adicionar o nó source e itera sobre as arestas computando os valores de distância, sendo que uma nova distância mínima é adquirida quando um novo nó inserido na fila possui distância atual + peso de aresta menor que a distância para o nó de destino. Enquanto o algoritmo de Bellman-Ford atua com uma tabela de distância para cada roteador, os roteadores trocam mensagens de distância entre outros roteadores, então o próprio roteador computa a nova distância para com seus vizinhos, o retorno desse algoritmo é uma malha de caminhos mínimos que idealmente converge.

5 - Qual é a complexidade de mensagens do roteamento por estado de enlace? Explique por que esse algoritmo tende a exigir mais disseminação de informação do que o vetor distância
**Resposta:** A complexidade de mensagens do roteamento por estado de enlace é O(n^2) e esse processo é conhecido como "flood" de mensagens, veja que essa complexidade pode ser adquirida pensando que um roteador irá compartilhar suas informações de topologia com todos os outros roteadores, sendo n a quantidade de roteadores, então teremos que O(n^2) mensagens trocadas entre os roteadores. Esse algoritmo exige mais disseminação de informação, pois o algoritmo de Dijkstra precisa do conhecimento da topologia completa da rede para gerar os caminhos mínimos.

7 - Descreva o fenômeno da contagem ao infinito característico de protocolos de vetor de distância. Explique a origem dessa falha e de que maneira ela propicia a criação de loops na rede.
**Resposta**: O fenômeno de contagem ao infinito ocorre quando há uma atualização que aumenta a distância de um link de uma rede. Esse fenômeno ocorre pela natureza assíncrona do algoritmo do vetor de distâncias, em que um atualização má feita é propagada por toda a rede.
Vamos fazer um exemplo, considere a rede:
A -(2)- B -(4)- C
dA = [0, 2, 6]
dB = [2, 0, 4]
dC = [6, 4, 0]

Considere que:
A -(2)- B -(X)- C
- Como A não percebe a mudança inicialmente então:
t0:
dA = [0, 2, 6]
dB = [2, 0, X]
dC = [X, X, 0]

Note que A não é notificado de que o caminho de C foi impedido, então ele propaga para B.
t1:
dA = [0, 2, 6]
dB = [2, 0, 8]
dC = [X, X, 0]

Só que A pede a tabela de DV para B para recalcular a sua rota para C, então
t2:
dA = [0, 2, 10]
dB = [2, 0, 8]
dC = [X, X, 0]

Isso ocorre, pois o nó A e B não sabem da topologia da rede, portanto, precisam propagar a informação.

8 - O emprego da técnica de reverso envenenado (poisoned reverse) é capaz de sanar integralmente o problema da contagem ao infinito? Apresente sua justificativa
**Resposta**: Não,

10 - No contexto do protocolo OSPF, o que define uma área? Explique a motivação por trás desse conceito, relacionando-o com ganhos de escalabilidade e a mitigação de mensagens de controle.
**Resposta**: Dentro do contexto do OSPF o que define uma área é uma partição lógica de um sistema autônomo, dentro dessa área geralmente utilizam-se algoritmos de Link State para confirmar uma melhor topologia dentro da rede. A motivação por trás desse conceito é que definir uma topologia geral para a rede é pouco viável pela sua escala, então há a hierarquia que define OSPF para comunicações intra-AS, assim torna viável a escala da rede atualmente.
Veja que se toda a rede fosse feita através desse modelo, apenas o custo de mensageria seria na ordem de O(n^2) tornando o processo inviável à medida que a rede crescesse. Além disso, podemos perceber certos benefícios de controle, uma vez que segmentamos o problema.

11 - Explique a finalidade dos atributos NEXT-HOP e AS-PATH dentro do protocolo BGP. Comente como cada um deles atua na determinação do encaminhamento e no processo de seleção de rotas
**Resposta**: 
AS-PATH: Armazena uma lista de caminhos de sistemas autônomos pelo qual o anúncio já passou para chegar no roteador atual. Ele serve para evitar loops dentro da rede, pois evita caminhos que já percorreu, além disso pode servir de critério de escolha dentre dois anúncios, sendo a escolha daquele com menor AS-PATH.
O NEXT-HOP armazena o endereço IP do roteador que inicia o caminho em direção ao destino final.

12 -
**Resposta**:
O critério de escolha nesse exemplo será o caminho com menor AS-PATH, portanto, aquele que faz menos saltos. Contudo, o BGP nem sempre escolhe caminhos com menos ASes, pois esse atua como algoritmo baseado em política. Por exemplo, uma ISP pode ter acordo de livre transmissão para uma outra ISP e, portanto, prefere caminhos que passem por ela. Além disso, não necessariamente menor quantidade de ASes implicará em melhor desempenho, pois podem haver questões de gerenciamento de tráfego e também de estado dos links