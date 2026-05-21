---
tags:
  - engenharia-de-software
---
# O que será abordado:
- **Tipos de requisitos de software**.
- **Engenharia de Requisitos**.
- **História de Usuários**.
- **Casos de Uso**.
- **Produto Mínimo Viável (MVP)**.
- **Testes A/B**.

# Tipos de Requisitos de Software:
**Requisitos Funcionais** - O que o software deve fazer.
**Requisitos Não-Funcionais** - Sob quais condições deve fazer.

Essa parte se destaca, uma vez que de nada adianta ter o sistema mais desenvolvido no sentido de tecnologia se ele não atende aos seus usuários. 

**Requisitos Funcionais** são geralmente escritos em linguagem natural. Enquanto, **Requisitos Não-Funcionais** geralmente são especificados de forma quantitativa.

Alguns outros autores também gostam de classificar requisitos como **Requisitos de Usuário** e **Requisitos de Sistema**. 

# Engenharia de Requisitos:
Processo que engloba as atividades que conseguem ajudar na descoberta, análise, especificação e manutenção dos requisitos do sistema. Essa atividade deve ser **sistemática** e ser feita ao longo do ciclo de vida da aplicação.

**Elicitação de Requisitos**: Descoberta e entendimento dos requisitos.
- Entrevistas com Stakeholders.
- Aplicação de Questionários.
- Leitura de Documentos.
- Implementação de Protótipos.
- Análise de cenários de uso.

Uma atividade que pode ser feita é que o desenvolvedor esteja envolvido nas atividades da empresa e observe os comportamentos dos usuários. Assim, haverá documentos com requisitos que devem ser **documentados, verificados e validades e priorizados**.

No desenvolvimento Ágil esses documentos são geralmente **História de Usuários**, enquanto uma abordagem mais rigorosa envolve a criação de um **Documento de Especificação de Requisitos**. NO geral, um requisito deve ter as seguintes características: **Correto, Preciso, Completo, Consistente e Verificável**.

## O que vamos estudar?
Veja que os requisitos atuam como ponte entre um problema do mundo real e uma solução dentro do mundo do software.

![[Pasted image 20260519172059.png]]
A questão é: Construir documentos de Detalhamento de Requisitos pode demorar muito tempo, portanto, para o mercado atual muitas vezes é inviável. Dessa forma, surgiram estilos de documentação menos rigorosos como o de **História de Usuários**.

Para aplicações que estão sujeitas a menos variações, podemos utilizar o método mais tradicional de especificação de requisitos. Nesses casos podemos utilizar os **Casos de Uso**.

Para sistemas desconhecidos e que não sabemos se de fato é necessário uma solução por software, podemos utilizar o **MVP**. No geral são implementados para resolver problemas em mercados desconhecidos ou incertos.

# História de Usuários:

$$
\texttt{História de Usuário} = \texttt{Cartão} + \texttt{Conversas} + \texttt{Confirmação}
$$
**Cartão:** Cliente descreve em poucas sentenças qual funcionalidade espera do sistema.
**Conversas**: Um representante dos clientes deve fazer parte do time e deve elucidar problemas durante o desenvolvimento.
**Confirmação**: Você pode escrever uma história que envolva um **teste de aceitação**, ou seja, escrever uma descrição do cenário com exemplos e casos de testes especulativos.

Algumas características podem ser encontradas em boas **Histórias de Usuários**.
**Independentes**: Dadas duas histórias X e Y, elas podem ser implementadas em qualquer ordem.
**Negociação**: Deve haver negociação entre cliente e desenvolvedor sobre alguns requisitos, seja por detalhe técnico ou requisito ainda não levantado.
**Valor**: Histórias são propostas, escritas e priorizadas pelos clientes.
**Estimar**: É possível estimar quanto tempo irá demorar para implementar uma história.
**Sucintas**: Histórias complexas e grandes são chamadas de épicos. Histórias de usuários idealmente devem implementadas em menos de uma semana.
**Testáveis**: Toda história deve possuir um elemento testável.

Antes de começar a escrever história de usuários é legal levantar os papéis de usuários (user roles). 

>>> Como um $\texttt{<user-role>}$, eu gostaria de $\texttt{<realizar algo no sistema>}$


## Exemplo: Sistema de Controle de Bibliotecas.
*user-roles*: usuário típico, professor e funcionário da biblioteca.

O livro contempla diversos exemplos de user-stories. Contudo, o mais interessante é que ele mostra alguns testes de aceitação com um user-story. 
Suponha que o user-story seja "Como funcionária da biblioteca, eu gostaria de pesquisar por livros".
- Pesquisar por livros, informando ISBN.
- Pesquisar por livros, informando autor; retorna livros cujo autor contém a string de busca.
- Pesquisar por livros, informando título; retorna livros cujo título contém a string de busca.
- Pesquisar por livros cadastrados na biblioteca desde uma data até a data atual.

Dentro de engenharia de software, procura-se reduzir o que é chamado de **gold plating**, que é o efeito de um desenvolvedor modificar uma user-story por vontade própria.

# Casos de Uso:
São documentos textuais de especificação de requisitos que são mais detalhados que histórias de usuários. São documentos que são principalmente desenvolvido pelos desenvolvedores do projeto, mas deve ser acessível para qualquer usuário.

A ideia é escrever um cenário com um **ator** que deseja usar o sistema. A ideia é enumerar os passos realizados por um ator. Nesse sentido, primeiro é descrito o **fluxo normal**, enquanto **extensões de fluxo normal** também são adicionadas. 

- Todo caso de uso deve ter um nome, cuja primeira palavra é um verbo no infinitivo.
- O caso de uso deve definir o ator principal do caso de uso.
- Incluir casos do tipo "se" dentro da extensão de um fluxo.
- Alguns casos de uso podem conter seções adicionais como 
- (1) Propósitos de caso de uso.
- (2) Pré-condições.
- (3) Pós-condições.
- (4) Uma lista de casos de uso relacionados.

OBS:
-  Tente manter no máximo nove passos no fluxo normal.
-  Documente como o sistema realizará algo de modo bem abstrato, sem especificar tecnologias.
- Bom sistemas de casos de uso envolvem a criação de um **glossário**.


# Exercícios:
1) [POSCOMP 2010, adaptado] Sobre Engenharia de Requisitos, marque Verdadeiro (V) ou Falso (F).
( ) - A Engenharia de Requisitos, como todas as outras atividades de Engenharia de Software, precisa ser adaptada às necessidades do processo, do projeto, do produto e do pessoal que está fazendo o trabalho.
( ) - No estágio de levantamento e análise dos requisitos, os membros da equipe técnica de desenvolvimento do software trabalham com o cliente e os usuários finais do sistema para descobrir mais informações sobre o domínio da aplicação, que serviços o sistema deve oferecer, o desempenho exigido do sistema, as restrições de hardware, dentre outras informações.
( ) - 