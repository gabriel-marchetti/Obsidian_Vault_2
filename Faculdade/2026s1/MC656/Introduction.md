---
tags:
  - MC656
  - engenharia-de-software
---
# Assuntos comentados:
- O que é Engenharia de Software?
- Principais assuntos estudados dentro dessa área.
- Quais sistemas de software se beneficiam das técnicas utilizadas.

**Engenharia de Software**:
	Aplicação de abordagens *sistemáticas, disciplinadas e quantificáveis* para desenvolver, operar, manter e evoluir um Software. 
	Veja que essa abordagem não surge junto do surgimento do Computador. Computadores eram utilizados para resolver problemas específicos e, portanto, não precisavam de uma abordagem mais sistemática. A demanda por uma abordagem mais sistemática do desenvolvimento de software se mostrou mais claro na **Conferência da OTAN** em que surgiu o termo **Engenharia de Software**. 
	A área da Engenharia de Software é bem diferente das outras áreas da engenharia quando se trata do ciclo de vida dos produtos. 

## **Dificuldades Essenciais** e **Dificuldades Acidentais**
### Dificuldades Essenciais:
**Complexidade** - Desenvolver software é complicado e todas as áreas dependem cada vez mais dele.
**Conformidade** - Software é adaptável conforme a evolução do tempo.
**Facilidade de Mudanças** - Um software sempre precisa de mudanças e modificações.
**Invisibilidade** - Dificuldade em estimar recursos para construção de software.

### Dificuldades Acidentais:
São as dificuldades que por essência não tem a ver com a solução proposta, pense que essa dificuldade está referente a uma decisão que pode dificultar ou facilitar o desenvolvimento.

# O que se estuda em Engenharia de Software:
Utilizada as definições fornecidas pelo **SWEBOK** - *Guide to the Software Engineering Body of Knowledge*. A **Engenharia de Software** consiste em 12 áreas:
1) Engenharia de Requisitos.
2) Projeto de Software.
3) Construção de Software.
4) Testes de Software.
5) Manutenção de Software.
6) Gerência de Configuração.
7) Gerência de Projetos.
8) Processos de Software.
9) Modelos de Software.
10) Qualidade de Software.
11) Prática Profissional.
12) Aspectos Econômicos.

## Engenharia de Requisitos:
**O que** e **Como** um sistema deve operar.
**Requisitos Funcionais** e **Requisitos Não-Funcionais**. Os requisitos funcionais respondem as perguntas relacionadas a o quê o sistema deve fazer e os aspectos não-funcionais devem respondem o como um sistema deve fazer.
Exemplo:
Um sistema de Banco deve realizar a operação de checagem de saldo e transferência de dinheiro.
- A checagem deve ocorrer em 3 segundos.
- A transferência precisa estar disponível 99% do tempo.
## Projeto de Software:
Aqui são definidas as principais **Unidades de Código** no nível de **Interfaces**. Tais interfaces são divididas em **Interfaces Requeridas** e **Interfaces Providas**.
Um exemplo de definição de interface é a seguinte:
```java
class ContaBancaria {
   private Cliente cliente;
   private double saldo;
   public double getSaldo() { ... }
   public String getNomeCliente() { ... }
   public String getExtrato (Date inicio) { ... }
   ...
}
```
Nesse campo, caso estejamos falando sobre uma questão de mais alto nível ainda, podemos classificar esse tipo de abordagem como **Arquitetura de Software**.
## Construção de Software:
Transformação das interfaces conceituais em implementação concreta.
- Definição das estruturas de dados e algoritmos.
- Definição de Frameworks e Bibliotecas.
- Definir técnicas de tratamento de exceções.
- Definir padrões de nome.
- Definir Layout de código e documentação.
- Definir as ferramentas que serão utilizadas: Compiladores, IDEs, Depuradores, Gerenciadores de Bancos de dados, Ferramentas de construção de interfaces.
## Teste de Software:
**Edsger W. Dijkstra:**
> Teste de Software mostram a presença de bugs, mas não dizem respeito à ausência deles.

- **Teste de Unidade**, **Teste de Integração**, **Testes de Performance** e **Testes de Usabilidade**.
- Diferença entre **Validação** e **Verificação**.
- **Defeitos**, **Bugs** e **Falhas** - Uma falha é a concretização de um **bug**.
**Exemplo**: Explosão do Foguete Ariane 5.
## Manutenção e Evolução do Software:
Serão considerados os tipos de manutenção: **Corretiva, Preventiva, Adaptativa, Refactoring** e **Evolutiva**. 
**Corretiva** - Corrigir bugs reportados por usuários ou outros desenvolvedores.
**Preventiva** - Corrigir bugs latentes no código que não ocasionaram falhas. (EXEMPLO - VIRADA DO MILÊNIO).
**Adaptativa** - Promover alteração do sistema utilizado dentro do sistema, isto é, tecnologia ou legislação por exemplo.

