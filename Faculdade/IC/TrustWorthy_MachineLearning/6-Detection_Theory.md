# Chapter Context
Aqui estamos trabalhando na empresa ThriveGuild, que deve criar um sistema de aprovação de empréstimos, e devemos nos preocupar em definir os indicadores e objetivos do sistema. Lembrando que em um sistema de Machine Learning temos dois grandes problemas de minimização: 
- Minimizing aleatoric uncertainty - relacionado com "basic performance".
- Minimizing epistemic uncertainty - relacionado com "reliability".

Aqui vamos focar na parte de "basic performance", portanto, desejamos minimizar a incerteza aleatória. A questão aqui é que devemos explorar as métricas para criar sistemas. De modo que a métrica é a parte que mais definirá o processo de otimização do modelo. 
Veja que perguntas como:
- As quantidades selecionadas descrevem bem a dinâmica da situação para o modelo de ML?
- Como diferenciar entre modelos bons e ruins?
- Avaliar apenas a questão de aprovação de empréstimos nesse caso é uma boa métrica?

**Detection Theory:** O estudo de tomadas de decisões ótimas para saídas categóricas.
Em contraste com **Estimation Theory** que foca em gerar saídas continuas.

# Selecting Decision Function Metrics.
**Binary Hypothesis Testing:** Queremos decidir dado o contexto apresentado acima, definir quem deve receber o empréstimo e quem não deve receber.

Sendo $Y$ a variável que classifica a resposta do sistema, sendo $y=0$ uma reprovação e $y=1$ uma aprovação.
Para ajudar na tomada de decisão, temos um vetor $X$ contendo **Status de emprego, Renda, ...** 

Encontrar uma função $\hat{y}:X \rightarrow \{0,1\}$. 

Aqui entra uma discussão sobre avaliarmos a qualidade dessa função $\hat{y}$, de modo que podemos quantificar quantos casos tivemos em que ela acertou ou errou. Aqui estamos contando os True Positives, True Negatives, False Positives, False Negatives. Por fim, ele comenta sobre a **CONFUSION MATRIX**.

![[Pasted image 20250821153733.png|center]]
A probabilidade $p_{TN}$ é conhecida como **Specificity** e **Selectivity**. Mas cada uma dessas probabilidades tem um nome específico.

Como orquestrar essas quantidades deve ser um trabalho extremamente bem planejado. Pense que um Banco de um país em boas condições pode preferir minimizar FN, pois isso implica que incluiremos mais pessoas, mas outro banco pode preferir aderir outra política mais restrita de minimizar os FP, pois isso exclui as pessoas más pagadoras.

Além de condicionarmos dessa maneira, podemos fazer o condicionamento pela inversa:

![[Pasted image 20250822091055.png|center]]
A questão que ele comenta aqui é:
Se você se preocupa com a decision function, se concentre no primeiro conjunto de probabilidades
Se você se preocupa com a qualidade dessas predições, se concentre no segundo conjunto de probabilidades

**OBS:** Por que isso acontece?

# Summary Performance Errors
Tanto os falsos positivos como falsos negativos são erros.

Uma métrica é: $p_E = p_0 \cdot p_{FP} + p_1 \cdot p_{FN}$ que define a **probability error**.
Outra métrica é: $p_{BE} = \frac{1}{2} \cdot p_{FP} + \frac{1}{2} \cdot p_{FN}$ que define a balanced probability of error.

A questão aqui é que podem haver discrepâncias quando fazemos essa medida na **probability error** se a taxa entre os falsos positivos e falsos negativos não é proporcional, isto é, existem muitos mais pontos de um tipo do que o outro. Nesse cenário, se o **problem-owner** quiser atribuir relevância proporcional a ambos os tipos de erro, então a métrica balanceada é melhor.

Algumas medidas surgem de tomar o complemento:
Accuracy: $1-p_{E}$
Balanced Accuracy: $1-p_{BE}$

**F1-Score:** $F_1 = 2 \cdot \frac{p_{TP} \cdot p_{PPV}}{p_{TP} + p_{PPV}}$
Essa medida é mais usada para garantir a qualidade das predições do que a qualidade da decision-function.

A questão aqui é que essa descrição de eventos não se traduz em uma consequência para o mundo real. Para isso, podemos utilizar/criar funções de risco, que irão ter interpretação direta para a aplicação. No exemplo da ThriveGuild, escolher um bom pagador é fundamental para o lucro, de modo que uma pessoa que pega mais dinheiro do que devolve deve ser evitada.
Para esse problema de decisão binária, podemos utilizar uma função $c(Y, \hat{y}(X))$ que denota o custo de cada função. 

**Bayesian-Risk:** 
$$
R = \left( c_{10} - c_{00}\right) \cdot p_{0} \cdot p_{FP} + \left( c_{01} - c_{11}\right) \cdot p_{1} \cdot p_{FN} + c_{00} \cdot p_{0} + c_{11} \cdot p_{1}
$$
![[Pasted image 20250824152642.png|center]]
A figura acima apresenta um "roadmap" para quando estamos lindando com um problema de decisão. Veja que Risco é o problema central e os conceitos sobre o problema são resultados disso. O problema principal agora será minimizar Risco. De modo que, decisões corretas $c_{00}$ e $c_{11}$ não serão penalizadas, isto é, $c_{00}=0$ e $c_{11}=0$.

Note que isso nos leva a:
$$
R = c_{10} \cdot p_{0} \cdot p_{FP} + c_{01} \cdot p_{1} \cdot p_{FN}
$$
---
**OBS:** Acho que aqui ele errou... Acho que o certo seria:
$$
R = c_{01} \cdot p_{0} \cdot p_{FP} + c_{10} \cdot p_{1} \cdot p_{FN}
$$
Pois, se $c(Y, \hat{y}(X))$, então não faz muito sentido associar $p_{0}$ com $c_{10}$.

---

Por simplicidade, é assumido que: $c(\cdot, \cdot)$ é constante, mas claramente podemos entender o custo como uma função de $\hat{y}(X)$, isto é, como uma função das features. Pense que no cenário da ThriveGuild se uma das features é o valor do empréstimo, então empréstimos de valor alto devem ter associado um risco maior.

# Accounting for Different Operating Points.

Aqui há a discussão de um novo tipo de métrica, a métrica $\texttt{ROC}$. Note que o método de calcular o Risco Bayesiano apresentado funciona muito bem quando temos um estado constante de probabilidades e custos. Contudo, no contexto de uma fornecedora de empréstimos, temos que a economia pode alterar os custos e também as probabilidades. Um período de crise pode gerar mal-pagadores que antes eram bons pagadores, nesse sentido, se mantivermos os mesmos custos isso pode ser catastrófico.

Veja que alterar os valores que compõem a decision function altera seu comportamento, então podemos avaliar diferentes **Operating Points.**

Muitas das funções de decisão são operadas de acordo um threshold $\eta$. 
Suponha a seguinte função de decisão:
$$
\hat{y} =
\begin{cases}
1, \text{Se } Pr(y=1|x) \geq \eta \\
0, \text{c.c.}
\end{cases}
$$
Então, diminuir $\eta$ implica em um modelo mais flexível.
A questão aqui é que **variar o parâmetro** $\eta$ **te torna mais propício a falsos-positivos ou falsos-negativos, mas nunca ambos**.

Diferentes **Operating Points** corresponde em diferentes distribuição de pares: $(p_{FP}, p_{FN})$ e $(p_{FP}, p_{TP})$. 

## ROC (Receiver Operating Characteristic):
Traçamos a curva $(p_{FP}, p_{TP})$ e vemos os efeitos causados por variar $\eta$.
Ela atua como:
$\eta \rightarrow \infty$, $p_{FP}=0$ e $p_{TP}=0$.
$\eta \rightarrow 0$, $p_{FP}=1$ e $p_{TP}=1$.

É uma função côncava e não-decrescente.

![[Pasted image 20250824161208.png|center]]
Aqui está uma visualização da **ROC-Curve**.
Quanto mais a curva se aproxima da reta pontilhada -> Pior. (RANDOM GUESSING)
Quanto mais a curva se aproxima da quina -> Melhor. 

Uma métrica muito interessante que aparece aqui é a seguinte:
**AUC(Area Under the Curve):** que corresponde a calcular a área abaixo da **ROC**. Veja que essa métrica é especialmente interessante quando iremos operar nosso algoritmo em diferentes situações (**Operating Points**). Então, queremos encontrar o $\eta$ que maximize AUC.

Note que: $0.5 \leq AUC \leq 1.0$.

**OBS:** Em vez de mapearmos $(p_{FP}, p_{TP})$ podemos mapear de $(p_{PPV}, p_{TP})$. É apenas uma interpretação diferente, mas é análogo.
Referência: $\texttt{Jesse Davis and Mark Goadrich. “The Relationship Between Precision-Recall and ROC Curves.” In: Proceedings of the International Conference on Machine Learning}$

# The Best That You Can Ever Do

Após descobrirmos mais sobre as medidas que podemos avaliar sobre um modelo, então temos que definimos uma métrica de Risco.

Queremos minimizar o Risco.

Se $\hat{y}^{*}(\cdot)$ define a melhor função de decisão do problema, isto é, a função que tem $R^{*}$ como mínimo. Então:
$$
\hat{y}^{*}(\cdot) = \texttt{arg min}_{\hat{y}(\cdot)} \mathbb{E} \left[ c(Y,\hat{y}(X))\right]
$$
Essa melhor função de decisão é:
$$
\hat{y}^{*}(\cdot) =
\begin{cases}
1, \Lambda(x) \leq \eta  \\
0, \Lambda(x) > \eta
\end{cases}
$$
$\displaystyle\Lambda(x) = \frac{p_{X|Y}(x|Y=1)}{p_{X|Y}(x|Y=0)}$, é a **likelihood ratio**.
$\displaystyle \eta = \frac{c_{10} \cdot p_{0}}{c_{01} \cdot p_{1}}$

Não é possível adquirir um valor de função menor que o Risco da escolha bayesiana. Portanto, quando mesmo nesse ponto o risco é muito alto, então o processo retorna para o data understanding e o data preparation.

Além disso, temos que se $g(\cdot)$ tal que ela seja monotonamente crescente, então ainda vale que:
$$
\hat{y}^{*}(\cdot) =
\begin{cases}
1, g(\Lambda(x)) \leq g(\eta)  \\
0, g(\Lambda(x)) > g(\eta)
\end{cases}
$$
# Risk Assessment and Calibration
Até agora a questão que estávamos nos preocupando era sobre perguntar para um novo dado se o empréstimo deve ser aceito ou não. Entretanto, devemos pensar que uma pergunta pode ser: Qual a probabilidade desse novo dado ser "default"?
Nesse sentido, o problema deixa de ser um problema de decisão binário e passa a ser um problema de "probabilistic risk assessment".

Veja que essa conversão de problema pode ser transformada em um problema de classificação através de um threshold. 
Veja que se desejamos mudar o contexto dessa discussão para "probabilistic risk assessment", então podemos criar uma função $score(x)\in [0,1]$ que irá contabilizar uma probabilidade da certeza de uma escolha. Pense que nesse sistema, se $score(x)$ está muito próximo de $0$ ou $1$, então temos certeza da escolha. Enquanto $score(x)$ próximo de $0.5$ se trata de uma escolha mais dificil.

## Brier-Score:
Se trata de uma métrica para variáveis que irão dar como resposta uma interpretação de probabilidade da escolha.
$$
\texttt{Brier Score} = \mathbb{E}[(S-Y)^2]= \frac{1}{n} \sum_{j=1}^{n} (s_j - y_j)^2
$$
O $\texttt{Brier Score}$ tem embutido um conceito de $calibration$ e de $refinement$.
Um modelo é dito calibrado quando ocorre que o $score$ é proporcional aos dados observados. Por exemplo, se calculamos que $s=0.7$ mas temos que nos dados essa proporção é diferente, então o modelo não está calibrado. Veja que termos a hipótese que um modelo está calibrado nos dá a interpretação de que a resposta corresponde a uma probabilidade de certo evento ocorrer. (Como ele chegou nisso?)

A questão aqui é que podemos refinar nosso modelo através da escolha certa de uma função $g(\cdot)$ monotonamente crescente na escolha da decision function ideal. De modo que, se temos $\{ (s_1,y_1), (s_2,y_2), \cdots, (s_n, y_n)\}$, e temos $k$ grupos, isto é, $\{B_1, B_2, \cdots, B_k\}$, então podemos encontrar: $\{ (\bar{s}_1, \bar{y}_1), \cdots, (\bar{s}_1, \bar{y}_1)\}$. De modo que:
![[Pasted image 20250828151942.png|center]]
$$
\texttt{calibration loss} + \texttt{refinement loss} = \texttt{Brier Score} 
$$
Podemos desenhar a $\texttt{calibration curve}$ que é um esboço dos grupos $(\bar{s}_k, \bar{y}_k)$ de modo que classificamos como cada grupo se comporta.
![[Pasted image 20250828152206.png|center]]
OBS: Quanto mais próximo da linha diagonal, melhor o modelo.

