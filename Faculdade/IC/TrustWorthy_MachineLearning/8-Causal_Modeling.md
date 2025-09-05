# Contexto:
Você atualmente deve ajudar uma empresa chamada **ABC Center** que irá orientar seus clientes a atingirem serviços sociais desejados. Os clientes dessa empresa são pessoas que necessitam de auxílio de entidades governamentais, principalmente. A questão aqui é gerenciar as pessoas para centros específicos que podem oferecer um serviço que ajude tal pessoa a sair dessa condição.
Para isso, desejamos descobrir quais centros são mais adequados para cada pessoa. Desse modo, podemos avaliar a partir de dados de entrada e experiências prévias quais são os centros mais recomendados.

**OBS:** Em contraste com capítulos anteriores que cobriam partes bem estreitas e específicas do processo de Machine Learning agora estamos em um contexto mais geral.

## Apresentando o problema de causalidade.
Podemos analisar os dados anteriores para gerar *insights* sobre novos clientes. Por exemplo, uma pessoa que recebeu o serviço do **ABC Center** que consistia em um curso de reparo de carros, teve seu salário aumentado. Contudo, não podemos inferir a uma outra pessoa que esteja em situação semelhante que isso irá ocorrer. Aqui há um problema de *Causality*. Pois, não basta criar um modelo de Machine Learning para avaliar o efeito da *intervenção* do **ABC Center**. Para isso, devemos criar um **Causal Modeling**.
O **Causal Modeling** é essencial para entendermos o mundo. Modelos de Machine Learning não nos oferecem métodos para entender esse sistema de causa-efeito.

A grande questão aqui é que:
- Devemos conseguir diferenciar uma situação que necessite de **Causal-Modeling** e uma situação que entra apenas no campo de **Prediction**.
- Descobrir o grafo de relações causais entre as variáveis aleatórias do modelo.
- Computar uma quantidade que descreva como uma situação de causa-efeito afetou a resposta.

# Contrast Causal Modeling and Predictive Modeling.
*Causality* se refere como *fazer* uma ação, implicará que *outra* ação aconteça. Nesse caso, dizemos que uma ação causou a outra. Nesse sentido, dentro do contexto que estamos estudando, *causalidade* é importante pois pode alterar a probabilidade de eventos.
-> A probabilidade de chover amanhã é de 50%.
-> Agora a probabilidade de que chova amanhã deve ser maior que 50% se os 5 dias anteriores também choveram.

**OBS:** *Causalidade* não há relação com *Correlação*. No sentido de, *Causalidade* está relacionada com eventos que são sequenciais e logicamente conectados.

## Structural Causal Models.
**Causal Modeling** é a tentativa de capturarmos *causalidade* entre variáveis aleatórias através de probabilidades. **Structural Causal Modeling** faz parte de **Causal Modeling**.
**Structural Causal Modeling**: Consiste em um *Grafo Causal* e *Equações estruturais*.
![[Pasted image 20250904171259.png|center]]
Os Nós representam **Variáveis Aleatórias** e a estrutura de grafo além de representar *relação estatística*, representa também *causalidade*. Como **Structural Causal Models** são muito parecidos com **Bayesian Networks**, então existem diversas propriedades que podem ser feitas dentro dessa representação que eram utilizadas em **Bayesian Networks**. Por exemplo, dentro de **Bayesian Networks** podíamos calcular probabilidades através de uma forma fatorada e capturar independência de variáveis.
Para avaliar a *causalidade* dentro dessa rede temos que introduzir um novo operador $do(\cdot)$ que consiste em um operador que condiciona uma certa variável. 
$$
Pr(\;Y|do(t)\;) : \texttt{ Distribuição da variável Y dado que T assume o valor t}.
$$
Então, temos que:
$$
Pr(\;Y|do(t)\;) = f_Y (t, noise_Y)
$$
No grafo causal que conecta $T$ (que pode ser entendido como counseling sessions) e $Y$(que pode ser entendido com ansiedade). E isso faz sentido, justamente porque $T \implies Y$, então $Y$ deve variar apenas em um certo ruído.
Além disso, veja que podemos expandir o entendimento para variáveis aleatórias com diversas variáveis causais.
![[Pasted image 20250904172659.png|center|420x300]]
$$
Pr(\; Y |do(t)\;) = f_Y (t_1, t_2, t_3, noise_Y)
$$
## Causal Modeling vs Predictive Modeling.
Como se perguntar se um problema está mais ligado a um dos tipos de modelagem. Basicamente, podemos nos perguntar se algo está ativamente modificando as *features*. Usar um **Predictive Model** com o intuito de **Causal Model** pode causar grandes danos. A grande questão é que se um **Modelo de decisão** for tão previsível a ponto de mudanças específicas dentro de uma feature afetar a variável de resposta, então não temos um bom avaliador. 
**OBS:** Acho que isso aqui dá para perguntar na reunião...
	Sobre os problemas de utilizar **Predictive Modeling** como **Causal Modeling**.

Veja, em contraposição, que o problema do **ABC Center** é justamente esse. Prever como pequenas variações de uma feature podem afetar a variável de resposta.
Veja que a criação de um **Causal Modeling** pode ser usado justamente para criar um sistema **Trustworthy**. Visto que podemos inferir *validity*, *internal validity* e *external validity* dentro do modelo. Isso ocorre, porque estamos olhando para variações dentro das features e como elas podem interferir na variável de resposta.
**OBS:** Eu não entendi como que isso ocorrer na prática... Basicamente, como podemos atribuir validade a um modelo através de um **Causal Modeling**.

# Two problem formulations.
Existem dois problemas aqui que devem ser tratados. Primeiro, devemos nos preocupar com o grafo causal para entender possíveis relações entre as variáveis do nosso problema. Outro problema é obter um número que nos diga quanto uma determinada saída foi influenciada por uma determinada ação.

Existem dois tipos de dados que podem ser adquiridos e compreendidos tanto na fase de *data understanding* e *data preparation*. Esses dados são *Interventional Data* e *Observational Data*. Definimos esses dados como:
**Interventional Data**: Dados que foram estritamente coletados em um experimento e podem ser muito diretos para criar um *Causal Modeling*.
**Observational Data**: Dados que não foram extraídos de um experimento e podem ser difíceis de gerar um *Causal Modeling*. 

Além dessa separação, dentro de **Observational Data** podemos criar dois métodos para gerir causalidade dentro do modelo.
![[Pasted image 20250905112010.png|center]]
# Quantifying a Causal Effect.
Se pensarmos em uma variável binária dentro do nosso modelo, podemos tentar calcular o efeito dessa variável através da seguinte fórmula:
$$
\tau = \mathbb{E}[Y|do(t=1)] - E[Y|do(t=0)]
$$
Essa quantidade justamente específica o efeito esperado da intervenção de uma variável. Chamamos essa quantidade de *average treatment effect*.

Veja que se 
$Y|do(t=0)$ : gaussian pdf com $\mu = 13$ e $\sigma=1$
$Y|do(t=1)$ : gaussian pdf com $\mu = 18$ e $\sigma=2$

Então:
$$
\tau = 18 - 13 = 5
$$
Portanto, um determinado curso pode oferecer uma aumento de $5$ dólares no pagamento por hora de uma pessoa com esse curso, por exemplo.

## Backdoor Paths and cofounders.
Primeira observação: Notemos que $\tau$ é calculado a partir de $Y|do(t)$ que é diferente de $Y|t$. A diferença ocorre justamente quando não há **backdoor path** entre $T$ e $Y$.
*Backdoor Path*:
	(1) - Começa com uma aresta chegando em $T$.
	(2) - Não é *Blocked*.

Vamos comentar sobre alguns padrões estruturais da **Rede Bayesiana**. Esses padrões são conhecidos como *Motifs*. 
1) Causal Chain Motif.
	$\texttt{X -> M -> Y}$.
	Se condicionarmos através da variável $M$ o caminho de $X$ para $Y$ se "perde".
	Exemplo:
	$\texttt{fumar(X) -> pressão arterial(M) -> risco de AVC(Y)}$.
	Note que se condicionarmos primeiramente em (M) perdemos a relação de (X) para (Y).
2) Common Cause Motif.
	$\texttt{M -> X e M -> Y}$
	Se $M$ é causa comum de $X$ e de $Y$, então condicionar em $M$ bloqueia o caminho para os nós.
3) Common Effect Motif.
	$\texttt{X -> M <- Y}$.
	Condicionar por $X$ fecha o caminho completo, assim como condicionar por $Y$. Mas condicionar por $M$ deixa o caminho aberto.
	Um exemplo para tornar mais claro a questão de fechar caminhos.
	$\texttt{M: Perda de Peso, X: Fazer exercícios, Y: Fazer Dieta}$.
	Podemos apenas gerar uma correlação entre $X$ e $Y$ caso haja uma observação de $M$.

**Confounding Bias**: é o viés introduzido justamente quando olhamos para a motivação do porquê $Pr(Y|do(t)) \neq Pr(Y|t)$. 

## Exemplo:
