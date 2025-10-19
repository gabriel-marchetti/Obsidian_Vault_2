# Resultados Experimentais:
``` 
LR:    Logistic Regression WITH Sensitive Feature.
LRns:  Logistic Regression WITHOUT Sensitive Feature.
PR:    Logistic Regression WITH Prejudice Remover Regularizer.
NB:    Naive-Bayes WITH Sensitive Feature.
NBns:  Naive-Bayes WITHOUT Sensitive Feature.
CV2NB: Calders and Verwer 2-Naive-Bayes.
```
OBS: Five-Fold Cross-Validation.

![[Pasted image 20251008111141.png|center]]
```
Acc (Acurárica) : Maior é melhor
NMI (Normalized Mutual Information) : Maior é pior.
NPI (Normalized Prejudice Index) : Maior é pior.
UEI (Underestimation Index) : Maior é pior.
CVS (Calders Verwer Score) : Maior é pior.
PI/MI (Prejudice Index / Mutual Information) : Maior é pior. Indica melhor trade-off entre acurácia e prejudice removal.
```
Análises:
- $\texttt{NBns}$ vs $\texttt{PR} \;\eta=5$ : $\texttt{PR} \;\eta=5$ conseguiu ser melhor tanto em **ACURÁRIA**, **NPI** e indica um melhor trade-off entre acurácia e prejudice removal.
- $\texttt{LRns}$ vs $\texttt{PR-}5$ : Conseguiu remover de fato prejudice em troca de acurácia.

Resultados:
- Aumentar $\eta$ de fato melhora a decisão ser *fair*, mas reduz **Acurácia** -> Existe o trade-off entre acurácia e fairness.
- Aumentar drasticamente o fator $\eta$ parece aumentar muito o fator **PI/MI**, mostrando que o trade-off passa a ser não otimizado.
![[Pasted image 20251008112729.png|center]]
OBS: Comparação geral dos métodos (Muitos valores do CV2NB não podem ser vistos por conta da escala dramaticamente menor).
![[Pasted image 20251008112743.png|center]]
OBS: Escala log no eixo vertical.

**Questão**: Qual a vantagem do $PR$ sobre o modelo $CV2NB$ ? Parece que o $PR$ consegue levar em conta o efeito de cada feature sobre a informação sensível. - Experimento com dados sintéticos.

$$
R_{PR} (D, \Theta) = \sum_{(x_i, s_i) \in D} \left[ 1 - \sigma(x_i^Tw)\right] \left[ \frac{\hat{Pr}(y=0|S=s_i)}{\hat{Pr}(y=0)}\right] + \left[ - \sigma(x_i^T w)\right] \left[ \frac{\hat{Pr}(y=1|S=s_i)}{\hat{Pr}(y=1)}\right]
$$
$$
\hat{Pr}(y|s) \approx \sum_{(x_i, s_i) \in D} \frac{M[y|x_i,s_i;\Theta]}{|\{ (x_i, s_i) \in D , s_i=s\}|}
$$
$$
\hat{Pr}(y) \approx \sum_{(x_i, s_i) \in D}\frac{M[y|x_i, s_i;\Theta]}{|D|}
$$
