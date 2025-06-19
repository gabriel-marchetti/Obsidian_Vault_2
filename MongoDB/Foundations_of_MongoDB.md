A database "MongoDB" surge para superar os problemas apresentados pelas bases relacionais como apresentado em [[Advantages_NoSQL]].

A primeira vantagem de utilizar um sistema como o "MongoDB" é o fato de ser distribuído. Isso traz vantagens como:
- Se fornecedor de dados ficar indisponível, então podemos utilizar outro fornecedor. Note que isso também introduz redundância para o sistema, entretanto, muitas vezes isso é desejado e preferível. 
- Reduz latência de envio de dados para os usuários, uma vez que podemos mandar os dados a partir de servidores mais próximos dele.

O método de armazenamento de dados é feita através de documentos. Esses documentos armazenam dados na forma de JSON-Like files. Note que isso traz uma certa flexibilidade para o Schema do banco de dados, vantajoso para banco de dados ainda não estruturados.

## Arquitetura de um banco de dados Mongo.

Há uma pirâmide de hierarquia dos dados.

![[Pasted image 20250513163852.png | center]]
Essa estrutura se refere que uma "Collection" é um conjunto de "Document"s.
Uma "Database" é um conjunto de "Collection"s.
Um "Node" é um conjunto de "Database"s
Um "Cluster" é um conjunto de "Node"s

Nesse sentido veja que "Database" é diferente de DBMS.
Além disso, um "Node" é uma instância de um MongoDB. Enquanto que um "Cluster" é um conjunto de "Node"s utilizando "Replica sets" e "Sharded Clusters" para armazenar as informações.

### CAP Theorem 
Um banco de dados não pode fornecer em conjunto consistência, disponibilidade e tolerância à particionamento.

![[Pasted image 20250513164329.png | center]]
Podemos no máximo garantir a existência de duas dessas características em um banco de dados. 
O MongoDB prioriza a clusterização, então a tolerância a particionamento é sempre utilizada. Desse modo, cabe ao usuário decidir se deve haver prioridade entre consistência ou disponibilidade.

A disponibilidade pode ser garantida através dos Replica-Sets.
A consistência pode ser garantida através do Read-Concern (Checagem através dos Replica-Sets e Sharded-Clusters) e Write-Concern (Maioria dos Replica-Sets confirmam escrita).
