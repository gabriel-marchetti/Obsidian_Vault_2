
# Contexto
Dentro desse capítulo estamos no contexto de uma empresa chamada $JCN$ que deseja migrar sua área de atuação. Para isso, eles desejam criar um modelo de machine learning que avalia a expertise dos seus atuais funcionários baseado em diversos dados.

Já foram feitas as fases de: $\texttt{problem specification, data understanding, data preparation}$. Agora devemos ir para a fase de $\texttt{Modeling}$. Para isso primeiro precisamos escolher uma **decision function** que se adeque ao problema. A questão é:
- Existem diversos algoritmos para lidar com problemas de decisão. Como escolher o melhor?

Podemos adentrar melhor nessa discussão pensando que: Não existe um modelo de Machine Learning que performe melhor que todos os outros em todas as situações. Isso ocorre, porque cada dataset possui uma estrutura específica que o modelo selecionado pode não se adequar muito bem ou adequar-se muito bem. Desse modo, devemos nos preocupar com *Overfitting* e *Underfitting*, eventos onde ocorre justamente uma alta especificação do modelo no dataset treinado que ele não generaliza para casos fora do treino e o evento totalmente oposto, onde não deixamos a função livre para se adequar aos dados.

Um modo de atacar esse problema é através da força-bruta: Para cada modelo, treine ele e teste os resultados. Contudo, isso pode ser um pouco trabalhoso. Então, podemos estudar características de cada modelo e ver qual o seu **Domain of Competence**, que consiste no ambiente onde esse modelo irá se destacar, assim como em quais situações ele não irá performar bem.

# Domains of Competence.
Podemos primeiramente nos perguntar:
- Quais características dentro de um dataset podem favorecer um modelo?
- Quais são os parâmetros para determinar um Domain of Competence?
Para isso podemos pensar na **Decision Boundary.**

Pense que cada feature do seu modelo $x^{(1)}, \cdots, x^{(d)}$ pode ser mapeada a uma função de **Likelihood-Test**. A questão é que se invertermos essa função, iremos gerar uma superfície para cada feature. De modo que, o conjunto dessas superfícies gera a **Decision Boundary**.
![[Pasted image 20250828154413.png|center]]
Existem três características que definem se o **inductive bias** de um modelo são adequados para o dataset:
1) overlap of data points from the two class labels near the decision boundary
2) linearity or nonlinearity of the decision boundary
3) number of data points, their density, and amount of clustering

# Two ways of approaching supervised-learning.
Veja que não temos acesso direto à distribuição que envolve os dados coletados na feature junto do label desse data-point. Portanto, diretamente minimizar o **Bayes-Risk** não irá funcionar, pois não temos nem função para trabalhar. Desse modo, surgem duas estratégias:
- **Plug-In Approach:** Estimar as **likelihood-functions** e as **prior-probabilities** baseado no dataset e minimizar o **Bayesian-Risk**.
- **Risk Minimization:** Escolher um classificador específico e minimizar o risco.

![[Pasted image 20250828155416.png|center]]
# Plug-In Approach:
A estratégia desse método é estimar tanto $p_{X|Y} (x | y=0)$, quanto $p_{X|Y} (x | y=1)$ e utilizá-las para adquirir uma **likelihood-test function** para obter o classificador.

# Discriminant Analysis.
Assumir uma versão parametrizada da **Likelihood-function** e estimar tais parâmetros. A partir disso obtemos uma razão entre essas funções e descobrimos um threshold. 
Veja que o viés aqui vem justamente da forma parametrizada da **Likelihood-function**.
A hipótese da distribuição gaussiana multivariada -> Quadratic Discriminant Analysis.
Se ainda tivermos que as matrizes de covariância são idênticas -> Linear Discriminant Analysis.

![[Pasted image 20250828160620.png|center]]
Portanto, podemos perceber que o **Domain of Competence** desses métodos abrange métodos com uma fronteira quase linear e que apresentem uma alta densidade de pontos na fronteira de decisão, isso porque deve se a função irá se adaptar à essa fronteira de decisão.

## Non-Parametric Density Estimation.
Quando é dito que o método é não paramétrico, queremos dizer que os parâmetros são associados aos pontos e não a uma funções específica.

**Kernel Density Estimation:** Place a smooth pdf into every datapoint such that the normalized sum of all pdf is the likelihood function estimation. O número de parâmetros é o número de centros em que colocamos a pdf. Fazendo isso para pontos que $y=0$ e $y=1$ e depois gerando a razão entre as funções irá nos gerar um threshold que poderá ser utilizado como classificador.

Se assumirmos que cada feature é mutuamente independentes, então temos que as funções de likelihood irão se tornar produtos de pdf de uma variável, cada feature, Nesse caso temos uma **Naive-Bayes Classifier**. É difícil classificar uma região de competência do algoritmo do **naive-bayes**, pois ele não performa muito bem na vida real.

**k-Nearest Neighbor:** É um algoritmo extremamente simples. Peguemos os $k$ vizinhos mais próximos do datapoint em questão e avaliamos o label mais frequente, desse modo, temos que o ponto em questão recebe esse label.
A região de competência desse método ocorre quando temos diversas componentes ou regiões dentro da fronteira de decisão, além disso, regiões de mescla muito grande na fronteira de decisão tendem a tornar o algoritmo pior.

# Risk Minimization Basics:
Instead of estimating the functions plugged into the likelihood-test function, we try estimating the decision-function that minimizes a certain bayesian-risk.

One metric that can be used is the $p_{E}$ the probability of error. 
$$
p_{E} = p_0 \cdot Pr(\hat{y}(X)=1 |Y=0) + p_1 \cdot Pr(\hat{y}(X) = 0 | Y=1)
$$
Contudo, não temos acesso direto às distribuições de probabilidades em questão. Desse modo, podemos usar uma aproximação do risco empírico, dada por:
![[Pasted image 20250828165255.png|center]]
Sendo que $L(y_j, \hat{y}(x_j))$ é zero quando $\hat{y}(x_j)=y_j$ e um quando $\hat{y}(x_j)\neq y_j$

Mas vejamos que apenas considerar essas questões não é suficiente.

## Structural Risk Minimization.
A questão aqui é que podemos ser criativos com a decisão da decision-function, de modo que se escolhermos uma função específica pode haver overfitting ou underfitting. A questão aqui é escolher classes de funções que balanceiem a complexidade e simplicidade da função de decisão, chamamos esse conjunto de *Hypothesis Space* e atribuímos à essa característica o nome: *Structural Risk Minimization Principle.*

![[Pasted image 20250828165950.png|center]]
Ilustração da ideia de *Structural Risk Minimization Principle.*

A escolha de um *Hypothesis Space* $\mathcal{F}$ determinará o bias do seu modelo. Portanto, a escolha desse espaço influencia diretamente no **Domain of Competence** do seu modelo. Funções mais restritas provavelmente atuam melhor em fronteiras de decisão lineares, por exemplo.

# Risk Minimization Algorithms:
![[Pasted image 20250828170446.png|center]]
Basicamente o problema é encontrar essa função que minimiza o problema. Veja que ao final desse problema de otimização iremos adquirir uma função e não um valor. A resposta desse processo é justamente uma $\hat{y}$. Podemos também adicionar a regularização dentro do modelo:
![[Pasted image 20250828170742.png|center]]
Cada novo parâmetro adicionado afetará o bias do modelo.

## Decision Tress and Forests.
![[Pasted image 20250828175127.png|center]]
Decision-Stump.
![[Pasted image 20250828175148.png|center]]
Decision-Tree.
![[Pasted image 20250828175206.png|center]]
Podemos ver que o *Hypothesis Space* de decision-tress podem se tornar complexos. Contudo, temos que o modelo é bem interpretável.
Uma decision-forest é composta por **ensembles** de decision-trees em que cada decision-tree pode ter um peso associado ao seu voto.
![[Pasted image 20250828175434.png|center]]
Exemplo de uma decision-forest.

O Algoritmo mais tradicional para se chegar numa árvore de decisão é através de um algoritmo guloso que irá decidir o particionamento de uma folha em dois ramos a partir de um corte que torne cada região a mais pura possível, isto é, cada região deve conter apenas datapoints com uma certa classificação idealmente. A pureza desse corte pode ser quantificada através de duas grandezas de **Information-Theoretic Measures** que são: **Information Gain** e **Gini Index**.

### C5.0 Decision Tree:
Utiliza o critério de **Information Gain** para decidir um corte.

### CART (Classification and Regression Tree):
Utiliza o critério do **Gini Index** para decidir um corte.

Além disso, para árvores de decisão devemos controlar a **profundidade** máxima, pois deixar esse parâmetro livre pode gerar *Overfitting*.

### Domain of Competence for decision-trees
Árvores de decisão são especialmente úteis quando conseguimos estabelecer thresholds de corte para características que favorecem a classificação de um datapoint. Além disso, regiões com overlap de datapoints de classes diferentes são ruins para a classificação através de árvores.

### Training Decision-Trees.
Os métodos principais para se treinar árvores de decisão são **Bagging** e **Boosting**.
**Bagging:** Diferentes conjuntos de features são apresentadas para árvores diferentes, cada árvore é treinada separadamente. No fim, juntamos os resultados através de um voto majoritário com pesos iguais.
**Boosting:** Um processo sequencial é seguido. A primeira árvore é treinada do modo usual, O segundo treino é focado para os datapoints que a primeira árvore errou. O terceiro treinamento foca nos erros de ambas as árvores anteriores e assim por diante. As primeiras árvores terão maior peso na votação.

A capacidade de generalização vem justamente da decisão de diversas árvores.

**OBS:** *Random Forests* é o método mais conhecido de **Bagging**, enquanto *XGBoost* é o método mais conhecido de **Boosting**.

Ambos métodos possuem um **Domain of Competence** grande e funcionam em diversos datasets.

## Margin-Based Methods

Essa família de métodos de classificadores engloba os métodos de: *Logistic Regression* e *Support Vector Machine(SVM)*.

A questão aqui é que podemos utilizar tanto uma decision-boundary linear ou não-linear. Chamamos essas funções de *Kernel functions.*
Nesse caso, temos que o modelo gira em torno de uma *Margin*, a distância dos pontos para a decision-boundary. 
$$
\hat{y}(x_j) = step(w^T x_j) = \frac{sign(w^T x_j) + 1}{2}
$$
Em que $w$ é um vetor de pesos que será treinado. Note que o hiperplano definido por $w$ irá dividir o espaço em dois semi-espaços. Desse modo, temos que o ponto que está em direção ao vetor $w$ terá $w^T x_j > 0$ e caso esteja na direção contrária ao vetor $w$, então $w^T x_j < 0$. 

Veja que idealmente temos que $\hat{y}(x_j) = y_j$, portanto, podemos fazer que:
$$
y_j = \frac{sign(w^T x_j) + 1}{2} \implies sign(w^T x_j) = 2y_j - 1
$$
Portanto, conseguimos mapear a *Margin* tanto do label quanto do ponto em questão.

Uma maneira de quantificar isso é através de $(2y_j-1)(w^T x_j)$ que é positivo para classificações corretas e negativas para classificações incorretas. Desse modo, podemos utilizar essa medida como argumento de algum tipo de *Loss function*.

**Logistic Regression:** $L\left( (2y_j-1)(w^T x_j) \right) = \log\left( 1+e^{-(2y_j-1)(w^T x_j)}\right)$
**SVM:** $L\left( (2y_j-1)(w^T x_j) \right) = \max \left\{ 0, 1-(2y_j-1)(w^T x_j)\right\}$ 
Que irá nos gerar os seguintes esboços:

![[Pasted image 20250829094417.png|center]]
Aliado a isso podemos adicionar uma regularização do tipo $||w||^2$ na *loss function*. Outro jeito de regularização é através da $l_1$-norm que é a soma do valor absoluto de cada elemento do vetor de pesos.

O **bias** desses métodos vem conjuntamente da *loss function*, *regularization* e *non-linear feature mapping*.

## Domain of Competence:
**SVM**s e **Logistic Regression** são especialmente bons em datasets estruturados de tamanho moderado. Além disso, **SVM**s funcionam melhor quando o dado é ruidoso.

# Neural Networks:
*Artificial Neural Networks* atualmente é o modelo mais em evidência quando tratamos de performance pura, além disso, redes neurais podem ser utilizada em uma gama muito grande de tarefas envolvendo *large-scale semi structured datasets* que define seu **Domain of Competence**.

*Hypothesis Space*: engloba uma combinação de composições de funções chamadas neurons.

**Deep Learning**: se refere a arquitetura que possuem uma alto foco dentro das *hidden layers* de uma rede neural.
![[Pasted image 20250829103526.png|center]]
Dentro do problema de classificação, desejamos que a camada de saída possua uma função mais abrupta para determinar a classificação. Contudo, dentro das camadas escondidas temos que a função de ativação de cada neuron tende a ser mais suave. Cada função de ativação irá introduzir um **bias** distinto. 
**Exemplos funções de ativação:** 
**ReLU (Rectified Linear Unit):** $\max{(0,z)}$
**Sigmoid or Logistic Activation**: $\displaystyle \frac{1}{1+e^{-z}}$

A função **ReLU** geralmente é utilizada devido às suas propriedades na questão de otimização da função.

Dado que escolhemos utilizar *Neural Networks* como arquitetura para nosso modelo, então devemos optar por escolher uma *loss function*. A função mais comum para redes neurais é a *Cross-Entropy Loss*. 
$$
L(y_j, \phi(x_j)) = - y_j \log(\phi(x_j)) + (1-y_j) \log(1-\phi(x_j))
$$
Onde $\phi(\cdot)$ define uma *soft-prediction* do label de $x_j$.

A regularização pode ser feita através de $l_1$-norm e $l_2$-norm. Contudo, o método mais comum é através do *dropout*. A ideia aqui é remover alguns nós durante o processo de treino. A ideia aqui pode ser similar a um *bagging* em que a cada passo, uma conjunto de desativações irá formar uma nova rede neural, que durante o processo de treinamento deve manter alguns nível de generalização e diversidade.

# Conclusão:
É importante definir o **Domain of Competence** e **Inductive Bias** para não só escolher o melhor modelo para sua tarefa, mas também será útil para discussão envolvendo *fairness*, *robustness* e *explainability*.


# Questões:
1) Quais são as principais características que contribuem para o **inductive bias**?
