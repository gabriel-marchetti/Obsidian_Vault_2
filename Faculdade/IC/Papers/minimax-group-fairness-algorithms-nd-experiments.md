# O que o Abstract propõe?
- Oracle-efficient learning algorithms.
- Minimize the maximum loss between various groups. Rather than equalizing group losses.
- Relaxations over fairness constraints - this allow a study on the trade-off between fairness and correctness.
- Minimax fairness is preferable than Equal-Outcome

# Implicações práticas:
- Aplicações onde a minimização de dados ao grupo mais desfavorecido é crucial. Pois, Equal-Error pode aumentar o erro base dos grupos desfavorecidos.

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
![[Pasted image 20251107105732.png|center]]
**Figura-1:** O algoritmo **MinimaxFair** apresentou as seguinte características: **Group errors tendem a ficar similares** (Será que threshold dos grupos eram frouxos?), **Peso dos grupos em desvantagem sobem**, **Existe correção entre popularion-error e max-group-error**.
![[Pasted image 20251107110012.png|center]]
**Figura-2**: A restrição de não possibilitar pesos de amostra negativos deixa o processo de otimização mais simples (função é convexa). Dentro do Dataset pode ser visto o fenômeno de aumentar o error-rate de **Winter** e **Autumn** apenas para cumprir com o Equal-Error.
![[Pasted image 20251107110211.png|center]]
**Figura-3**: Trade-off entre **Acurácia** e **Fairness**. O modelo parece seguir bem estritamente o bound de $\gamma$.
![[Pasted image 20251107110650.png|center]]
**Figure-4**: Equal-Error infla o erro de todos os grupos, isto é, mesmo grupos em desvantagem sofrerão o impacto de ser fair. A menor loss com o Minimax é de 0.325, enquanto a menor loss do Equal-Error é de 0.38. A ideia aqui é entender que o modelo Equal-Error tenta minimizar as populações injustiçadas, contudo chega um ponto em que é impossível minimizar isso e, portanto, ela começa a errar de propósito em grupos que tem loss baixa.
![[Pasted image 20251107110930.png|center]]
**Figure-5**: Quando a loss é modelada através de *log-loss* há um comportamento muito bom. Contudo, utilizar a loss como *0/1 loss* deixa o modelo bem mais caótico.


# Perguntas
- O que é um **Oracle-Efficient**?
- O que quer dizer "substantial Pareto Improvement"?
- O que quer dizer "Domina fortemente Pareto"?