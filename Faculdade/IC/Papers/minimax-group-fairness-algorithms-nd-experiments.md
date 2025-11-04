# O que o Abstract propõe?
- Oracle-efficient learning algorithms.
- Minimize the maximum loss between various groups. Rather than equalizing group losses.
- Relaxations over fairness constraints - this allow a study on the trade-off between fairness and correctness.
- Minimax fairness is preferable than Equal-Outcome

# O que é mostrado na introdução?
- Equal-Outcome é uma métrica muito restritiva. Podem haver casos em que estamos subindo o erro de todos os grupos em prol de fairness, sendo que o ideal seria reduzir o error-rate dos grupos em desvantagem. Isto é, grupos de fácil previsão estão sendo errados de "propósito".
- Evitar situações em que estamos retirando o benefício de todos em prol de igualdade.
- Ideia - Utilizar um algoritmo para minimizar o maior erro entre os grupos.

Suponha que $g'$ é o erro limitante dos grupos, portanto, se $g_{i}$ define o erro do grupo $i$, então:
$$
g' \geq g_i \;, \forall i
$$
Assim, se existe um grupo $j$ tal que $g_{j} = g'$, então não podemos relaxar esse erro. Desse modo, teremos de aumentar o erro de todos os outros grupos... (SITUAÇÃO RUIM).

**O que esse método propõe de novo**?
- Não existe requisito para utilizar grupo disjuntos - podemos extender fairness para grupos com intersecção (ex. Mulher e Negra).
- Não há necessidade de utilizar um atributo sensível como feature de treinamento.

**Dois algoritmos**:
1) O primeiro encontra um modelo fair.
2) O segundo verifica os trade-offs entre correção e fair.
- Os dois algoritmos convergem e são **Oracle-Efficient**.
- Diferentes tipos de taxa de erros podem ser incorporadas.
# O que as Figuras dizem?
**Figura-1:** O algoritmos **MinimaxFair** apresentou **Group errors tendem a ficar similares** (Será que threshold dos grupos eram frouxos?), **Peso dos grupos em desvantagem sobem**, **Existe correção entre popularion-error e max-group-error**.

**Figura-2**: A restrição de não possibilitar pesos de amostra negativos deixa o processo de otimização mais simples (função é convexa). Dentro do Dataset pode ser visto o fenômeno de aumentar o error-rate de **Winter** e **Autumn** apenas para cumprir com o Equal-Error.

**Figura-3**: Trade-off entre **Acurácia** e **Fairness**. 
# Perguntas
- O que é um **Oracle-Efficient**?
- O que quer dizer "substantial Pareto Improvement"?