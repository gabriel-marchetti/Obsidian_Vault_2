**Contexto**: Algoritmos de IA estão sendo usados para tomar decisões importantes. Aliado a isso, há uma grande preocupação com o viés introduzido em Sistemas de Machine Learning. Portanto, o paper propõe o estudo de técnicas na fase de **Pre-Processing**.

# Introduction:
As áreas que IA atuam hoje em dia são mais abrangentes: Decidir se devemos aceitar um empréstimo, decidir a liberação de um detento ou prosseguir com a aceitação de aplicações dentro de um trabalho. Ou seja, muitas decisões importantes são feitas por sistemas de Machine Learning.

Uma crença prévia era de que algoritmos de Machine Learning iriam introduzir mais justiça e objetividade para decisões, contudo isso não é verdade pois tanto os **Datasets** possuem viés, assim como os próprios algoritmos escolhidos introduzem viéses humanos.

Exemplo real disso: **COMPAS** - sistema americano para decidir se um detento pode ser liberado. Populações Negras eram duas vezes mais prováveis de não serem aceitos.

![[Pasted image 20250926094434.png|center]]
A imagem mostra que **Unfairness** vem de diversas fontes de **Bias**, nesse sentido **Unwanted Bias**. 
Além disso, temos a segmentação dos métodos de **Fairness** em **Três** partes:
![[Pasted image 20250926094622.png|center]]
**Pre-Processing**: Foca em reduzir ou eliminar **bias** no **dataset** através de processamento.
**In-Processing**: Foca em utilizar o estágio de treinamento para reduzir **bias**.
**Post-Processing**: Foca em utilizar os resultados para avaliar **bias**. (Não sei se tem muitas técnicas sobre reduzir no Post-Processing, a questão é que como foi comentado no TrustWorthy Machine Learning você pode utilizar essa técnica para modelos já pré-treinados).

A ideia do texto em focar no **Pre-Processing** é de: A parte inicial é a mais importante, porque viés no **dataset** influencia bem mais nas decisões.

# Measures of ML Fairness.
- Não há uma definição universal de **Fairness**.
- Divisão em **Group Fairness** e **Individual Fairness**.

$\mathbb{D}$ : Binary Classification Dataset
$p$ : Binary Protected Attribute in $\mathbb{D}$. $p=0$ (Grupo em desvantagem) e $p=1$ (Grupo em vantagem).

## Group Fairness:
**Disparate Impact Ratio**: 
$$
\texttt{DIR} = \frac{Pr(y'=1|p=0)}{Pr(y1=1 |p=1)}
$$
- Aplicações positivas devem ter proporções similares entre grupos distintos.
- A ideia aqui também é introduzida pelo Trustworthy ML devemos aceitar valores entre $0.8 \leq \texttt{DIR} \leq 1.25$

**Demographic Parity**:
Está relacionado com o **Statistical Parity Difference**.
$$
Pr(y'=1|p=0) = Pr(y'=1 |p=1)
$$
- A ideia aqui também é introduzir aceitação semelhante entre grupos diferentes.

**Pergunta:** Qual a diferença em impacto de usar **DIR** e **SPD**.

**Equalized Odds**:
- A relação $FPR$ (False-Positive Rate) e $TPR$ (True-Positive Rate) devem ser iguais entre os dois grupos.
$$
\begin{cases}
Pr(y'=1|p=0,y=0) = Pr(y'=1|p=1,y=0) \\ \\
Pr(y'=1|p=0,y=1) = Pr(y'=1|p=1, y=1)
\end{cases}
$$
## Individual Fairness:
- Se dois indivíduos são parecidos (excluindo features protegidas), então eles receberão previsões similares.
$$
y'_i = y'_j \qquad \texttt{Se, } s(i,j) = 1
$$
Onde $s(\cdot,\cdot)$ representa uma métrica de similaridade.

# Pre-Processing Approach:
- A ideia é: **Bias** vem dos dados, então vamos modificar e transformar o **dataset** para eliminar descriminações.

**Benefícios**:
- Treinar um modelo sobre um **dataset** sem **bias**, naturalmente gera um sistema mais justo.
- É o método mais geral, independente do algoritmo utilizado na parte de **In-Processing**.

(1) **Relabeling**.
(2) **Resampling**.
(3) **Reweighting**.
(4) **Fair Representation**.
(5) **Adversarial Learning-Based**.

## Relabeling.
- Modificar o **Dataset** de modo ativo até que uma métrica de **Fairness** seja atendida. PERGUNTA: **Como fazer isso sem o modelo treinado??**

- Método introduzido por "Luong et al." [24] - Utiliza um KNN para avaliar quais pontos são mais duvidosos.
- Método introduzido por "Kamiran et al." [25] - Utiliza a **Decision-Boundary** para optar por quais pontos serão invertidos. (**Massaging**).
- Método introduzido por "Hajian et al." [26] - Utiliza **Rule Protection** e **Rule Generalization**. 
- Método introduzido por "Wang et al." [27] - Utiliza uma técnica para identificar atributos proxy para features protegidas. Parece usar alguma técnica de **Counterfactual Distribution**, mas não sei o que é isso direito...

# Resampling.
- Selecionar um conjunto de dados do **Dataset** de modo a formar um **Mini-Dataset** com métricas de **Fairness**. 

- Método introduzido por "Kamiran et al." [25] - Ele amostra baseado nos pesos das instâncias. **PERGUNTA**: Como ele define os pesos das instâncias?
  Selecionar pontos perto da **Decision-Boundary** são preferencialmente selecionados, visto que eles são mais discriminados dentro do **Modelo**.
- Método introduzido por "Celis et al." [28] - Propõe uma generalização **P-DPP** de **k-DPP**. **PERGUNTA**: O que é **P-DPP** e **k-DPP**?
  O método final gera um **dataset** com diversidade combinatorial e diversidade geométrica, além de garantir **Fairness**.
- Método introduzido por "Chouldechova et al." [30] - Identifica os grupos que diferem mais dentro do **Dataset**.
- Método introduzido por "Iosifidis et al." [29] - Gera novos dados que estão não-balanceados e injustos.
- Método introduzido por "Ustun et al." [10] - Usa diferentes classificadores para diferentes grupos.
- Método introduzido por "Oneto et al." [9] - Usa **Multi-task Learning** (MTL) com **fairness** para aprender classificadores sem viés.

# Reweighting.
- Atribuir peso a cada datapoint sem modificar o **dataset**.

- Método introduzido por "Kamiran et al." [25] - Cria pesos para cada datapoint de modo a introduzir independência entre protected attributes e predictions.
  **PERGUNTA**: Como uma coisa influencia a outra?
- Método introduzido por "Krasanakis et al." [11] - Criar um classificador para aprender os pesos de cada **datapoint**. 
- Método introduzido por "Jiang et al." [12] - Identifica instâncias sensíveis (instâncias de dados ou atributos?) e depois cria um atribuidor de pesos para ser otimizado.

# Fair Representation.
- Aprender uma representação intermediária do **dataset**.

- Método introduzido por "Zemel et al." [13] - Utiliza uma técnica de **Supervised Representation Learning** para otimizar três objetivos **Acurácia, Individual Fairness e Demographic Parity**. 
- Método introduzido por "Feldman et al." [14] - Modifica as features para que ela fique indistinguível entre protected e unprotected attributes. (**INTERESSANTE**).
- Método introduzido por "Louizos et al." [15] - Aprender uma representação intermediária do **dataset** através de um **Autoencoder** mirando a independência entre diversos atributos e os atributos protegidos. Também se preocupam em reter o máximo de **Residual Information**.
- Método introduzido por "Calmon et al." [16] - definição probabilística para reduzir discriminação. Utilização de tríplex de ideias: **Controlar Discriminação, Limitar distorção de datapoints, Preservar Utilidade**
- Método introduzido por "Samadi et al." [17] - Redução de dimensionalidade através de **PCA** de modo a preservar similaridade entre diferentes grupos.
- Método introduzido por "Backurs et al." [4] - Fair representation learning em fair clustering.
- Método introduzido por "Lahoti et al." [6] - Unsupervised Representation Learning com objetivo em **Individual Fairness baseado em grafos de k-nearest neighbors** e **Individual Fairness baseados em Fairness Graphs**. 
	**Pergunta**: O que são **FAIRNESS GRAPHS**?

# Adversarial Learning-Based.
- Usar **Generative Adversarial Networks (GANs)** para gerar **datapoints**. o artigo [5] introduz mais essa ideia

- Método introduzido por "Xu et al." [8] - **FairGAN** (fairness-aware GAN). 
