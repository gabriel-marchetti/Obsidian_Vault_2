# What is Statistical Learning:
Contexto é: Imagine que somos uma agência de consultoria de marketing que decide explorar a correlação entre investimento em marketing e vendas. Para isso, temos o dataset <mark style="background: #FFB86CA6;">Advertising</mark> que consiste na venda de certos produtos em $200$ tipos diferentes de mercados. Além disso, temos o budget para cada modalidade como $TV$, $Radio$, $Newspaper$ e a respectiva quantidade de vendas.
![[Pasted image 20250827112059.png|center]]
A ideia é que cada mercado explorado irá ter uma reação de acordo o investimento naquele canal. Desse modo, podemos quantizar quanto efeito uma injeção de $x$ dólares pode afetar as nossas vendas. Veja que essa relação é importante, pois não conseguimos controlar quem compra os produtos, contudo podemos certamente alterar a quantidade de dinheiro investido em propagandas.

Veja que cada budget consiste em uma variável que podemos alterar, enquanto as vendas são saídas do sistema em questão. Portanto, temos que o budget da $TV$ pode ter o nome $X_{1}$, o do $Radio$ pode ter o nome $X_{2}$ e o do $Newspaper$ pode ter o nome $X_{3}$. Essas variáveis são conhecidas como: **Predictors, Independent Variables, Features or Variables**. 
Além disso, não temos controle absoluto sobre vendas, portanto, chamamos essa variável de **Response ou Dependent Variable**. Essa variável será chamada de $Y$.

Assumindo que desejamos condensar toda essa informação em um vetor, podemos utilizar $X=(X_1, X_2, X_3, \cdots, X_p)$ e escrevemos $Y = f(X) + \epsilon$.
$\epsilon$: é uma variável independente de $X$ e possui média zero.

Quando desejamos aplicar um método para de aprendizado estatístico, desejamos encontrar a função $f(\cdot)$ que descreve a relação entre os dados de entrada e a saída. Portanto, no mundo real não conhecemos as funções que regem as nossas observações.

## Why estimate $f$?

**Prediction:**
	Predizer eventos pode ser considerada uma habilidade muito poderosa. Imagine que o exemplo do <mark style="background: #FFB86CA6;">SMarket</mark> gerasse uma previsão correta em $95\%$ dos casos, então seríamos ricos. Contudo, para além disso, a questão serve de simplicidade. Uma amostra de sangue é facilmente adquirida hoje em dia, contudo, pode ser usada para descobrir diversas características de um sujeito que podem comprometer sua vida.
	Suponha que $X=(X_1,X_2,\cdots,X_p)$ são as variáveis da coleta de sangue e $Y$ é a probabilidade da pessoa em ter uma certa doença. Desse modo, temos que se encontrarmos uma $\hat{f} \approx f$, então esperamos que $\hat{f}(X) = \hat{Y} \approx Y$. 
	Note que nesse processo não queremos descobrir como a função $\hat{f}$ é, então tratamos como uma caixa-preta.
	Além disso, é importante ter conhecimento que existem dois grandes "erros" que se manifestam: **Irreducible error** and **Reducible error**.
	**Reducible Error**: Tem haver com escolher os modelos corretos para prever o comportamento de uma função $f$. Note que se estamos encaixando uma reta em um modelo de crescimento exponencial, é claro que haverá erro e isso pode ser reduzido.
	**Irreducible Error:** Mesmo que escolhemos a função $\hat{f} = f$, ainda temos que nos preocupar com diversas variáveis de erro. Por exemplo, se a coleta de sangue apresentar uma certa variância e tudo mais. Nesses casos, dados com alto $\epsilon$ e variado apresentarão predições ruins.
- Aqui parece que a discussão tem muito a ver com a discussão feita no *Trustworthy Machine Learning* sobre a questão de **Aleatoric Uncertainty** e **Epistemic Uncertainty**. A questão aqui é que o erro aleatório não pode ser reduzido, enquanto o erro epistêmico está mais relacionado com erros de conhecimentos não inseridos no seu modelo, então há sim uma clara relação entre **Epistemic Uncertainty $\approx$ Reducible Error** e **Aleatoric Uncertainty $\approx$ Irreducible Error**.

**Inference:**
	Aqui **NÃO** podemos tratar a $\hat{f}(X)$ como **Caixa-Preta**, porque precisamos saber sua forma exata para extrair informações. Existe um grupo de perguntar que entra no campo de inferência.
- Quais **Preditores** estão associados com a **Resposta** do sistema?
- Qual a relação com cada **Preditor** e a variável de **Resposta**?
- Qual função pode ser utilizada para sumarizar a relação entre **Preditor** e **Resposta**?

**Exemplos**:
- Uma campanha de Marketing decide pesquisar se determinados anúncios serão bem vistos pelos seus clientes. Desse modo, apenas desejamos uma resposta boa -> **Prediction**.
Já algumas perguntar relacionadas com a imagem mostrada em cima podem ser:
- Qual canais de comunicação estão associados com venda?
- Qual dos canais gera mais resposta em vendas?
Essas questões entram no campo de **Inference**.
- Qual será o aumento de valor nessa casa, caso ela tenha vista para um rio? (**INFERENCE**).
- Essa casa está abaixo ou acima do seu valor de mercado? (**PREDICT**).

# How do we estimate f?
Queremos encontrar $\hat{f}(\cdot)$ tal que $Y \approx \hat{f}(X)$. Para isso podemos utilizar duas abordagens: **Parametric Methods** e **Non-parametric Methods**.

## Parametric Methods.
1) Assuma uma forma para $f(\cdot)$
2) Use os dados de **Treino** para treinar (*fit/train*) à fim de estimar os parâmetros.

**Exemplo (Regressão Linear)**.
Assuma que:
$$
f(X) = \beta_{0} + \beta_{1} \cdot X_{1} + \cdots + \beta_{p} \cdot X_{p}
$$
Treine os parâmetros de modo que:
$$
Y \approx f(X)
$$
O método mais comum para a **regressão linear** é o **Ordinary Least Squares**. 

Veja que fizemos um **Desvio de Problema**. Antes o problema era encontrar uma $f(\cdot)$ que descrevesse o fenômeno observado. Agora o problema é um problema de **Otimização**. 
### Problemas da Abordagem Paramétrica:
- Assumir é uma responsabilidade grande, pois isso determinará o formato da função de predição. Veja que isso pode implicar em uma estimativa ruim caso a função fornecida seja distante da função real.
- Aqui temos um *tradeoff* entre **Flexibilidade vs Explicabilidade**.
- Um modelo muito flexível pode gerar **Overfitting**.

**OBS**:
O modelo linear pode ser utilizado para propor ajustes em *datasets* com poucos dados.

## Non-parametric Methods.
Não assumimos uma forma concreta para a função de $f(\cdot)$. A vantagem clara aqui é que modelos nessa categoria conseguem capturar um conjunto muito maior de situações distintas. 

### Problemas da Abordagem Não-Paramétrica:
- Um número muito grande de *datapoints* deve ser usado para garantir convergência estimativa da função $f(\cdot)$, pois não assumimos forma concreta dela.

Algumas abordagens são:
- *Thin-Plate Spline*.
![[Pasted image 20250919182709.png|center]]
Veja que nesse caso cada ponto do treino é utilizado para invocar uma leve curvatura na sua vizinhança. Esses métodos de **Splines** possuem a configuração de suavidade do modelo. 

# Trade-Off entre Acurácia e Explicabilidade.
**Pergunta**: Se podemos escolher métodos mais flexíveis, porque devemos pensar em escolher métodos mais restritos? 
- Em inferência, modelos mais restritivos são melhor interpretáveis.
![[Pasted image 20250919183407.png|center]]
A imagem apresenta justamente o **Trade-Off** entre **Flexibilidade e Interpretabilidade**. 

**Lasso:** É um modelo que atua como uma regressão linear, contudo tenta tornar alguns parâmetros para o número zero. Contudo, é super interpretável, pois teremos um conjunto menor de parâmetros.
**GAMs (Generalized Additive Models)**: Amplia o campo da regressão linear, introduzindo algumas não-linearidades.

Além disso, mesmo os modelos mais flexíveis podem acabar tendo problemas mesmo em configuração de predição. 
> Em algumas situações um modelo mais restritivo gera um aumento da acurácia.