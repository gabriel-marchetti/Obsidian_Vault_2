---
tags:
  - python
---
A referência de tópicos está presente em [[Python/ToC|ToC]] 
# Perguntas envolvendo tópicos 1, 2 e 3:
**O que define tecnicamente a linguagem Python e quais são os seus principais paradigmas de programação?**
?
Python é uma linguagem **interpretada, interativa e orientada a objetos**, que incorpora módulos, exceções e tipagem dinâmica. Ela é considerada **multi-paradigma**, suportando programação estruturada, orientada a objetos e funcional

**Qual foi a principal motivação de Guido van Rossum ao criar o Python e como sua experiência com a linguagem ABC influenciou esse processo?**
?
Guido van Rossum buscava uma forma melhor de administrar sistemas do que escrever programas em C ou scripts de shell. Ele se baseou na linguagem ABC por sua legibilidade, mas decidiu criar o Python porque o ABC carecia de **extensibilidade**, uma característica que ele tornou central no Python desde o início.

**Como o Python utiliza a indentação e por que essa característica é central para a filosofia da linguagem?**
?
Ao contrário de outras linguagens que usam chaves ou palavras-chave, o Python usa **indentação de espaço em branco** (regra _off-side_) para delimitar blocos de código. Isso foi desenhado para garantir que a linguagem seja altamente legível e tenha um layout visual limpo

**No contexto de estruturas de dados, qual é a diferença fundamental entre uma lista e uma tupla, e como isso afeta seu uso como chaves de dicionários?**
?
Por serem imutáveis, as tuplas podem ser usadas como chaves em dicionários (desde que todos os seus elementos também sejam imutáveis), o que não é permitido com listas

**O que significa o termo "batteries included" (baterias incluídas) em relação à biblioteca padrão do Python?**
?
Essa filosofia refere-se ao fato de o Python vir com uma **grande biblioteca padrão** que oferece ferramentas pré-escritas para diversas tarefas, como protocolos de internet (HTTP, FTP), processamento de strings e engenharia de software. Isso permite que os desenvolvedores criem aplicações realistas rapidamente sem depender excessivamente de terceiros no início

**Como funciona o sistema de tipagem do Python, especificamente as distinções entre tipagem forte, dinâmica e "duck typing"?**
?
Python utiliza **duck typing** e possui objetos tipados, mas nomes de variáveis não tipados. A linguagem é **dinamicamente tipada** (tipos são verificados em tempo de execução), mas **fortemente tipada**, o que significa que ela proíbe operações mal definidas, como somar um número a uma string.

**que são as PEPs (Python Enhancement Proposals) e qual sua importância para a evolução da linguagem e para a carreira de um desenvolvedor?**
?
As PEPs são **documentos de design** que descrevem novos recursos sugeridos para o Python, fornecendo especificações técnicas e justificativas. Elas são o principal fórum para discussão sobre o desenvolvimento da linguagem, sendo essenciais para que profissionais acompanhem as mudanças e o roteiro de lançamentos futuros.

**Qual a diferença entre o CPython e outras implementações como Jython e PyPy, e por que essa distinção é relevante para o desempenho?** 
?
**CPython** é a implementação de referência escrita em C. O **Jython** compila programas para bytecode Java, permitindo o uso de bibliotecas Java. O **PyPy** é uma implementação focada em velocidade, escrita no próprio Python, que pode gerar diferentes tipos de código intermediário para otimizar a execução.

**Como funciona o esquema de numeração de versões do Python e por que os desenvolvedores devem ter cuidado com mudanças na versão principal (Major)?**
?
As versões seguem o formato "A.B.C", onde "A" é a versão principal, incrementada apenas para mudanças drásticas que podem ser **incompatíveis com versões anteriores**. "B" representa a versão secundária (recursos novos) e "C" a micro versão (correções de bugs). Manter o código compatível é uma prioridade, pois mudanças incompatíveis podem invalidar milhões de linhas de código existentes.

**Qual a diferença técnica entre os operadores** == **e** **is** **no Python, e por que essa distinção é importante para evitar erros de lógica?**
?
Em Python, o operador == **compara por valor**, verificando se o conteúdo dos objetos é igual. Já o operador **is** **é usado para comparar identidades de objetos**, ou seja, verifica se ambos os nomes referenciam exatamente o mesmo objeto na memória (comparação por referência)

**Como o Python trata a divisão de inteiros e o operador de módulo, e de que forma esse comportamento difere de outras linguagens de programação?**
?
No Python 3, o resultado do operador de divisão `/` com operandos inteiros é **sempre um valor de ponto flutuante**. Para realizar a divisão inteira (truncada), utiliza-se o operador `//`. Além disso, o Python define a divisão inteira para **arredondar em direção ao infinito negativo** (ex: `7 // 3` resulta em `2`, mas `(-7) // 3` resulta em `-3`), o que consequentemente afeta o cálculo do resto com o operador `%`.