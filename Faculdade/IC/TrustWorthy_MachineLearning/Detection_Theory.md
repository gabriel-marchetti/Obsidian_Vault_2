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


