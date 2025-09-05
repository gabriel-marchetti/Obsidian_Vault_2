# StatQuest: Logistic Regression:
*Link:* https://www.youtube.com/watch?v=yIYKR4sgzI8

O vídeo primeiro revisa o conceito de regressão linear.
![[Pasted image 20250902104351.png|center|420x300]]
Dado um conjunto de dados. Sejam esses dados baseados em Tamanho e Peso, então enquadramos uma reta dados esses dados:
1) Calculamos $R^2$ para determinar se *Size* e *Weight* são correlacionados.
2) Calculamos *p-valor* para determinar se $R^2$ é estatisticamente significativo.
3) Usamos a linha para prever tanto *Size*, através do *Weight*. Como também podemos fazer a atividade contrária.

Essa habilidade de conseguir prever medidas através de outra medida entra no escopo de problemas de **Machine Learning**, portanto, a regressão linear é um tipo de **Machine Learning**.

Agora vamos falar sobre **Logistic Regression**.
O processo de regressão logística deve determinar se algo é verdadeiro ou falso. 
![[Pasted image 20250902104913.png|center|420x300]]
Para termos significado estatístico podemos controlar para que o valor de pico da sigmoid seja 1, enquanto o valor de mínimo seja 0. Desse modo, o valor será interpretado como uma probabilidade. Apesar da regressão retornar um número que está entre $[0,1]$ o problema de regressão logística se trata de um problema de *classificação*. 

Assim como na regressão linear, podemos criar modelos de regressão logística com diversas features. De modo que, conseguimos testar e comparar modelos através do *Wald's Test*. Contudo, o método de *fitting* da curva logística não é como a regressão linear (MMQ).
Em contrapartida, o método de regressão logística utilizará "Maximum Likelihood".

### Conclusão:
- Regressão Logística pode ser utilizada para classificar amostras.
- Regressão Logística pode ser utilizada para englobar diversos tipos de dados para uma predição.
- Regressão Logística pode inferir a contribuição de uma determinada *feature* de modo que podemos escolher sua participação no modelo.
- Regressão Logística é encaixada nos dados através de um método de *Maximum Likelihood*.


# CodeEmporium: Logistic Regression - THE MATH YOU SHOULD KNOW.
*Link:* https://www.youtube.com/watch?v=YMJtsYIp4kg

Assim como comentado no vídeo do *StatQuest*, um modelo de regressão logística é utilizada para problemas de classificação. Desse modo, podemos nos questionar: 
- Se o modelo de regressão logística é tão similar com o modelo de regressão linear, porque não podemos utilizar a regressão linear para problemas de classificação?

## Why not Linear Regression for Classification:
- **Multi Class classification**: Numericamente embutir um número a uma classe pode tornar o processo de comparação meio complexo.
	Pense no seguinte problema. Dados os dados atmosféricos da sua região devemos decidir se uma amostra desses dados corresponde a um dia ensolarado, nublado ou chuvoso. Veja que se mapearmos algo como:
	0 -> ensolarado.
	1 -> nublado.
	2 -> chuvoso.
	Então, temos que a diferença entre dias nublados e ensolarados é a mesmo do que dias nublados e chuvosos.
- **Binary Classification**: Desse modo, podemos nos perguntar se o modelo de regressão linear pode ser utilizada para classificar pontos em duas classes. Contudo, a questão vêm do fato da imagem de uma reta não ser contida em um intervalo limitado, portanto, perdemos contexto da quantidade em questão. Veja que a definição de thresholds é muito mais complexa. 

## Logistic Regression:
- Supervised Machine Learning method for classification.
- *Logistic* refere-se à *log odds*.
	*odds* = $\frac{Pr(A)}{1-Pr(A)}$

Desejamos chegar em: $Pr(y=1|x) = p(x)$. 
Podemos utilizar: $\displaystyle p(x) = \frac{1}{1-e^{-\beta x}} \implies \beta x=\log\left( \frac{p(x)}{1-p(x)}\right)$.
A questão aqui é como estimar esse valor $\beta$?
O método de regressão logística utiliza o método *Maximum Likelihood*. 
1) Considere $n$ amostras que são rotuladas através de 0 ou 1.
2) Para amostras do tipo '1' desejamos que: $\hat{\beta} \implies \hat{p(x)} \approx 1$.
3) Para amostras do tipo '0' desejamos que: $\hat{\beta} \implies 1 -\hat{p(x)} \approx 1 \implies \hat{p(x)} \approx0$.

Portanto, nosso problema sugere maximizar
$$
\prod_{i: y_i =1} Pr(y=1|x) =\prod_{i: y_i=1} p(x_i) \qquad \wedge \qquad \prod_{i: y_i =0} Pr(y=0|x) = \prod_{i: y_i=0} p(x_i)
$$
Dado que $\displaystyle p(x) = \frac{1}{1-e^{-\beta x}}$
$$
\begin{align}
L(\beta) &=   \prod_{i: y_i=1} p(x_i) \times \prod_{i: y_i=0} p(x_i) = \prod_{i} \left[ p(x_i)\right]^{y_i} \cdot \left[ 1 - p(x_i)\right]^{1-y_i} \\ \\
\log\{ L(\beta)\} = l(\beta)&= \sum_{i=0}^{n} y_i \log\left[p(x_i)\right] + (1-y_i) \log \left[ 1-p(x_i)\right]
\end{align}
$$
Substituindo por $p(x)$
$$
\displaystyle l(\beta) = \sum_{i=1}^{n} \beta \cdot x_i \cdot y_i - \log(1 + e^{\beta x_i})
$$
E por fim $\hat{\beta} = \arg\max_{\beta} l(\beta)$

a função $l(\beta)$ consiste em uma *transcendental equation* e não possui solução exata, então utilizamos métodos numéricos para estimar a sua solução. Considerando *Newton-Raphson Method*. 

$$
\nabla_{\beta} \; l(\beta) = \nabla_{\beta} \; l(\beta^{*}) + (\beta - \beta^{*}) \nabla_{\beta \beta} \; l(\beta^*) 
$$
Atingimos um máximo quando $\nabla_{\beta} \; l(\beta) = 0$, portanto:
$$
\begin{align}
\nabla_{\beta} \; l(\beta^{*}) + (\beta - \beta^{*}) \nabla_{\beta \beta} \; l(\beta^*)  &= 0  \\
\beta &= \beta^{*} - \frac{\nabla_{\beta} \; l(\beta^{*})}{\nabla_{\beta \beta} \; l(\beta^*)} 
\end{align}
$$
Portanto:
$$
\beta^{t+1} = \beta^{t} - \frac{\nabla_{\beta} \; l(\beta^{t})}{\nabla_{\beta \beta} \; l(\beta^t)}
$$

# Implementação:
A grande ideia aqui é que vou fazer a função de predict como:
$$
\sigma(x_i) = \frac{1}{1+e^{-(\mathbb{w^T} x_{i} + b)}}
$$

## Observações código:
```python
xx, yy = np.meshgrid(
	np.linspace(x_min, x_max, 200),
	np.linspace(y_min, y_max, 200)
)
```
Essa função cria uma matriz com os pontos:
```python
xx, yy = np.meshgrid([0, 1, 2], [0, 1])

xx = [[0, 1, 2], [0, 1, 2]]
yy = [[0, 0, 0], [1, 1, 1]]
```
---
Explicando $\texttt{ravel}$ e $\texttt{np.c\_[]}$
```python
xx = [[0,1], [0,1]]
yy = [[0,0], [1,1]]

xx.ravel() -> [0, 1, 0, 1]
yy.ravel() -> [0, 0, 1, 1]

# np.c_[] concatena as duas colunas dos vetores achatados:
grid_points = np.c_[xx.ravel(), yy.ravel()] -> [[0, 0], [1, 0], [0, 1], [1, 1]]
```
Portanto, como é esperado $\texttt{grid\_points}$ contém justamente os pontos da nossa malha criada do plano 2D.

