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
