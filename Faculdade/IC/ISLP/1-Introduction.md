# An Overview of Statistical Learning
A distinção adotada pelo livro no estudo de métodos de aprendizado estatístico é: **Supervised Learning** e **Unsupervised Learning**.

**Supervised Learning**: Se refere a técnicas usadas para "predict" ou "estimating" alguma saída que tenha alguma validação externa.
**Unsupervised Learning**: Se refere a técnicas usadas em "datasets" que não apresentam uma validação externa. O foco desse paradigma é encontrar padrões dentro dos dados.

# Three Real World Applications:

## Wage Data:
- O nome desse dataset a partir de agora será <mark style="background: #FFB86CA6;">Wage</mark>.
- Wage é traduzido como remuneração.
- Analisa a remuneração de um grupo de Americanos na região Pacífica.

Queremos ver a relação entre o conjunto $\texttt{(Age, Year, Education Level) -> (Wage)}$. 
![[Pasted image 20250825105046.png|center]]
**Pontos Principais do Gráfico**:
- Salários não decaem até aproximadamente 60 anos.
- Há um constante ajuste salarial conforme os anos.
- Nível educacional proporciona um aumento no salário.

Veja que se quisermos utilizar apenas $\texttt{Age}$ como fator para decidir o salário de uma pessoa não é uma boa decisão. Veja que o gráfico apesenta alta variabilidade. Desse modo, podemos pensar que uma estimativa mais precisa é alcançada quando mesclamos os dados dos três gráficos. 

Aqui desejamos classificar um novo indivíduo a partir desses três dados, portanto, desejamos classificar um novo indivíduo a um ponto contínuo que é seu salário. Portanto, estamos "predicting a continuous value". -> Regression Problem.
## Stock Market Data.
- O nome desse dataset a partir de agora será <mark style="background: #FFB86CA6;">SMarket</mark>.

Contém dados da movimentação diária de ações do tipo S&P (Standard & Poor's 500). Nesse problema queremos dizer se no dia seguinte haverá uma queda ou uma subida no índice. Veja que esse problema agora está dentro do problema de classificação

![[Pasted image 20250825111553.png|center]]
Aqui temos um gráfico que mostra um simples estratégia baseada em inferir se hoje irá haver uma subida ou descida do índice baseado na variação do índice no dia anterior, dois dias anteriores e três dias anteriores.

## Gene Expression Data.
- Aqui é utilizado o dataset <mark style="background: #FFB86CA6;">NCI60</mark>.

Nesse dataset não temos um tipo de "output". Um exemplo disso é através de uma empresa de marketing que coleta dados de seus usuários e deve classificar usuários com perfis de consumo similares apenas nos dados coletados. Esse tipo de problema é conhecido como *clustering* problem. 
O dataset $\texttt{NCI60}$ consiste em medidas da expressão de genes relacionadas a células cancerígenas. Desse modo, podemos encontrar um grupo de valores que indica uma maior pré-disposição ao desenvolvimento da doença.

![[Pasted image 20250825112357.png|center]]
Aqui está uma imagem da classificação do modelo à esquerda e do problema de fato à direita. Veja que mesmo sem contexto, conseguimos deixar os pontos parecidos próximos entre si. Como sabemos o contexto parece ser uma atividade boba, mas pensando que o painel da esquerda não possui contexto nenhum, os resultados parecem ser expressivos.

# A Brief History of Statistical Learning.

# Notation and Simple Matrix Algebra
$n$: representa o número de data-points.
$p$: representa o número de variáveis disponíveis para as predições.

$x_{ij}$, sendo que $i$ está entre $[1,\cdots, n]$ e $j$ está entre $[1,\cdots,p]$. Portanto, veja que $x_{ij}$ representa a $j$-ésima característica do $i$-ésima observação.

$x_{i}$ representa o $i$-ésimo data-point com as $p$ características dessa linha.
$\mathbf{x}_j$: representa o vetor com a $j$-ésima característica e todos os data-points.

