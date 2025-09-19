**Tipos comuns de Viés (Bias)**
- Viés Histórico.
  Modelo para contratar uma pessoa para um cargo pode carregar viés de datasets antigos, pois nessa situação mais homens eram contratados.
- Viés de Amostragem (Sampling Bias)
  A coleta de dados não representa a população de fato. Um sistema de detecção de faces pode conter um dataset com pessoas majoritariamente brancas, assim o modelo pode ter dificuldades em reconhecer pessoas negras.
- Viés de Confirmação.
  Coletar dados que corroborem para perpetuação de crenças existentes.

# Métricas de Fairness.
**Demographic Parity (Paridade Demográfica)**: Todos os grupos possuem mesma proporção de previsões positivas. 
$$
Pr(\hat{Y}=1 |A=a) = Pr(\hat{Y} = 1|A=b)
$$
Onde $a, b$ denotam grupos diferentes.

**Equalized Odds (Probabilidades Equilibradas)**: A taxa de **FP**(falsos-positivos) e **TP**(verdadeiros-positivos) é igual para todos os grupos.
$$
\begin{align}
Pr(\hat{Y} = 1 | Y=1, A=a) = Pr(\hat{Y} = 1 | Y=1, A=b) \\
Pr(\hat{Y} = 0 | Y=0, A=a) = Pr(\hat{Y} = 0 | Y=0, A=b)
\end{align}
$$
**Predictive Parity (Paridade Preditiva)**: A probabilidade de um **TP**(verdadeiro-positivo) é a mesma para todos os grupos. Conceitualmente, desejamos que todos os grupos possuem mesma probabilidade de serem positivos.
$$
Pr(Y = 1 | \hat{Y}=1, A=a) = Pr(Y = 1 | \hat{Y}=1, A=b) 
$$
