---
tags:
  - lista
---
# Introdução: 

## 1)
**Pergunta**: Explique cada um dos componentes de hardware e de software em um sistema distribuído.
**Resposta**: Vamos começar listando e explicando os componentes presentes dentro da parte de hardware de um sistema distribuído. Eles são a memória que cada computador possui, além da sua capacidade de processamento, assim como uma rede que conecte esses diferentes computadores, veja que a memória e o processamento são características presentes em sistemas computacionais, então é esperado que um sistema distribuído também apresente essas questões, já a rede possui a utilidade de tornar essas entidades inicialmente independentes em um sistema distribuído.
Para os componentes de software podemos listar a própria lógica do sistema distribuído, que irá guiar como cada entidade deve se comportar dentro desse sistema. Assim como o Sistema Operacional, que deve orquestrar as ferramentas dos computadores, assim como o Middleware que deve atuar como ferramenta para organizar como os computadores devem se comunicar, assim como oferece transparência para a heterogeneidade desses sistemas. Por fim, podemos citar os protocolos de rede que atuam dentro do sistema para oferecer um sistema de troca de mensagens.

## 2)
**Pergunta**: Quais são os principais desafios relacionados a confiabilidade em sistemas distribuídos, e como eles podem ser mitigados?
**Resposta**: 
Os principais problemas relacionadas à confiabilidade em sistemas distribuídos são: integridade, disponibilidade e tolerância à falhas.
Integridade: Um sistema distribuído possui, usualmente, diversos computadores com memória e processamento distribuídos, de forma que podem haver problemas como condições de corrida, por exemplo, na modificação de um valor de dado armazenado em um dos computadores. Assim como, alterações locais devem ser vistas pelo sistema para não gerar incongruências, uma pessoa não deve receber informações distintas dependendo do servidor. Esse desafio pode ser superado através de mecanismos replicação e sincronização, além de controle de concorrência (como mutex).
Disponibilidade: Um sistema distribuído deve estar sempre visível para seus usuários. Nesse sentido dizemos que ele está sempre disponível (idealmente) de forma que se fosse um sistema centralizado manutenções atrapalhariam que ele esteja sempre disponível. Uma maneira de superar esse desafio seria através da replicação de sistemas, além de oferecer políticas como atribuição de servidores para clientes através de um método de ranqueamento.
Tolerância à falhas: Um sistema não deve ser corrompido por conta de falhas de poucas requisições, nesse sentido ele deve ser resiliente. Veja que uma maneira de superar esse desafio é através do tratamento de falhas tanto a nível de execução, quanto a nível de pré-processamento (como através de validações). Além disso, devem haver manutenções sistemáticas, além de reinícios preparados e bem agendados. Por exemplo, aplicar essas atualizações em momentos que o sistema é pouco utilizado.

## 3) 
**Pergunta**: Qual a importância do middleware em um sistema distribuído e como ele facilita a transparência da heterogeneidade dos componentes do sistema?
**Resposta**:
A importância de um middleware é justamente para oferecer um mecanismo do controle da funcionalidade de um sistema distribuído, assim como oferecer transparência da heterogeneidade de um sistema. Para o primeiro, veja que o middleware atua como ferramenta para controle dos diferentes aspectos 
