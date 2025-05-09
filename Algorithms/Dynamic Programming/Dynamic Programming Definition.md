Programação Dinâmica se trata de uma estratégia para resolver problemas dentro da computação. Muitas vezes tratamos de um problema recursivo, em que um mesmo subproblema é chamado diversas vezes para verificar uma solução. Dessa maneira, o método de Programação Dinâmica se utiliza dos princípios básicos:
- Armazenar soluções dos subproblemas.
- Subproblemas idênticos aparecerão na árvore de recursão da solução recursiva.
- Podemos usar a "Top-Down" ou "Bottom-Up".

## Quando utilizar DP?
- Subestrutura Ótima: Soluções ótimas dos subproblemas serão utilizadas para os problemas maiores.
- Problemas Sobrepostos: um Subproblema da solução recursiva é resolvido diversas vezes.

## Maneiras de utilizar DP:

#### Top-Down (Memoization).
Nós armazenamos soluções dos subproblemas ótimos em Cache. Antes de chamar uma chamada recursiva, verificamos se já computamos o valor na tabela de memorização. Caso não tivermos computado, computamos e salvamos na tabela de memorização.

#### Bottom-Up (Tabulation).
Nós começamos com o problema de menor "tamanho" e construímos a solução até que chegamos no problema desejado. Aqui utilizamos um Loop Iterativo para construir a solução. Utilizamos uma "DP table" e computamos todos os valores. Nesse sentido, veja que a fórmula de recursão será útil, mas aqui a ideia é não utilizar recursão.

