# Contexto:
**Sospital** é uma agência de *health insurance* nos EUA. Você deve ajudar o *problem owner* a encarar a tarefa de automatização da escolha de pacientes que devem fazer parte do sistema de **Extra Health Care Management**.
**Care Management**: Se trata de um setor de diversos profissionais que atuam em conjunto para tratar de modo preventivo situações crônicas ou situações complexas.

**Problema principal**: Automatizar um processo que é feito principalmente de modo manual para escolha de pacientes que devem fazer parte desse programa.
Contudo, você como um bom projetista de sistemas de **Machine learning**, começa a consultar os diferentes **Stakeholders**. Nesse sentido, uma rápida entrevista com pacientes **Negros** possibilitou identificar uma desconfiança com os planos de saúde que não estão oferecendo esses serviços de modo satisfatório para essa população.

> O Sistema precisa ser justo e não conter viés indesejado.

**Solução**: Projetar uma solução que considere, através da fase de **Problem Specification**, um modelo **Fair** para alocação de recursos dentro do **Care Management** para a empresa **Sospital**.
- Comparar as diferentes definições de **Fairness** no contexto de **Machine Learning**.
- Selecionar a definição que mais se adequa ao problema.
- Mitigar viés indesejado através de uma fase de modelagem que considere questões de **Fairness**.

**Perguntas Iniciais**:
- Por que existem diferentes tipos de definições de **Fairness**?
- Como uma definição específica se adequará a um tipo específico de problema?
- Como garantir que viés indesejado não seja introduzido na fase de modelagem.

# Diferentes definições de Fairness.
Existem diferentes tipos de **Fairness** justamente pela dificuldade de conseguir modelar sem o contexto social explícito. Além disso, como diferentes situações sociais geram diferentes respostas à questões de desigualdade, então não é muito viável apresentar uma definição técnica. Apesar disso, o tratamento de **Fairness** dentro do contexto de solução para sistemas de **Machine Learning** apresentará uma robustez técnica.

Veja que a definição de um sistema *fair* possuir diversas ramificações
1) Um sistema pode prezar pela *equality* de serviços oferecidos por diferentes grupos - **distributive justice**.
2) Um sistema pode prezar por escolher de modo similar entre diferentes grupos - **procedural justice**.
3) Um sistema pode prezar por optar por situações de reparo - **restorative justice**.
4) Um sistema pode introduzir justiça penalizando pessoas que tomam ações erradas - **retributive justice**.

Uma *Rule of Thumb* é sempre fazer o design de um sistema através de *distributive justice*, pois a maioria dos sistemas focam apenas no contexto de analisar fins de uma determinada ação (Por que isso garante que *distributive justice* é uma escolha boa?). Isto é, a pessoa recebe o benefício de receber o serviço e pronto. Veja que a adição desses outros tipos de *justice* podem ajudar a descobrir onde certos sistemas podem ser inseridos e onde não podem ser inseridos.
**OBS**: Acho que no trabalho do *Caio* a ideia de atribuir empréstimos para as pessoas é mais guiado pela política de *retributive justice*. Então podemos perceber um contexto em que *distributive justice* não se insere bem. 
**OBS**: Eu não entendi como isso acontece muito bem, porque se você fizer *retributive justice* e um determinado grupo tiver mais probabilidade de fazer ações erradas, então eles não serão incluídos na distribuição. Assim isso acaba afetando *distributive justice*. É isso?
O que eu quero dizer é: Um tipo de **Fairness** impacta o outro tipo de **Fairness**.

Pensando na questão do serviço oferecido pelo **Sospital**, como são recursos limitados o mais correto não seria introduzir *procedural justice*?
- Mas outra pessoa poderia introduzir a questão de oferecer o serviço para pessoas mais afetadas por uma questão - *restorative justice*.

Esses tipos de vantagens são aceitáveis dentro do contexto de desenvolver um sistema de *machine learning*. 

**Reconhecer vantagens inaceitáveis e injustas**: Quando o sistema claramente classifica um grupo privilegiado e outro desprivilegiado.
A questão aqui é considerar que esses grupos privilegiados e desprivilegiados são definidos através de uma questão histórica e cultural. Por exemplo, pessoas brancas podem ter mais acesso aos recursos financeiros de uma instituição bancária, pois historicamente os grupos de negros foram afetados.

No geral, queremos evitar situações desbalanceadas que envolvem algum **desbalanço de poder**. Nesse sentido, criamos uma classificação de **protected attributes** que podem encapsular diversas questões de poder como raça, etnia, gênero, religião e até idade. Assim, muitas vezes haverá uma **Lei** indicando quais são esses atributos.

> Não existe um conjunto universal de Protected Attributes.

Existem dois tipos de *fairness* que também devemos nos preocupar **Group Fairness** e **Individual Fairness**. 

**Group Fairness**: A aceitação de um *outcome* deve ser similar entre grupos, cada grupo tende a ser definido por um **protected attribute**.
**Individual Fairness**: A aceitação de um *outcome* deve ser similar para pessoas com atributos similares (excluindo **protected attributes**), portanto, isso inclui pessoas exatamente iguais mais com **protected attributes** diferentes (**counterfactual fairness**).

> Para o problema da **Sospital** o principal atributo de *fairness* que deve ser considerado é o **group fairness**.

# De onde *unfairness* vem?
A fonte mais comum de *unfairness* provém de **unwanted bias**. Seja esse processo advindo de **Social Bias** através da mudança do *construct space* para o *observed space*. Ou ainda, através de **Representation Bias** através da mudança do *observed space* para o *raw-data space*.
![[Pasted image 20250919083020.png|center]]

**Social Bias**:
Por mais que muitas vezes seja verdade que mais visitas ao médico implique em uma condição mais sensível pelo paciente, isso não é verdade para todas as populações. Existe algum ponto em qua **Grupos Negros** tendem a saturar o nível de visitar, mesmo estando mais doentes. Além disso, temos que **Crenças** falsas como "Pessoas negras sentem menos dor" podem impedir tratamentos para dores. Por fim, também temos que pensar no viés da pessoa que decidiu os *labels* do *dataset* de treino.
**OBS:** Aqui tem duas referências que eu acho interessante de olhar porque não é possível isso.
[1] Moninder Singh and Karthikeyan Natesan Ramamurthy. “Understanding Racial Bias in Health Using the Medical Expenditure Panel Survey Data.” In: Proceedings of the NeurIPS Workshop on Fair ML for Health. Vancouver, Canada, Dec. 2019
[2] Oluwafunmilayo Akinlade. “Taking Black Pain Seriously.” In: New England Journal of Medicine 383.e68 (Sep. 2020)

Além disso, o **Sampling Bias** pode ser introduzido em serviços que não possuem uma quantidade de pessoas negras proporcional à realidade.

Veja que também podemos introduzir **Unwanted Bias** através da fase de **Problem Specification** e **Data Preparation**. Visto que a definição de um threshold pode acabar optando uma população. Além disso, podemos piorar o cenário de **Unwanted Bias** ao introduzir **Feature Engineering**.

### Distribution Shift e Fairness.
Parece que esses dois temas são bem similares. Mas algumas questões podem ser destacadas. 
1) O cenário de **Distribution Shift** consegue ter mais acesso ao **construct space**. Em cenário de **Fairness** isso nunca ocorre.
2) A especificação do que é buscado. (**Eu não entendi essa diferença**).

**OBS:** Parece haver uma discussão entre grupo privilegiado e grupo desprivilegiado. A questão é, essa classificação binária não parece ser muito bem formulada se formos pensar em um contexto mais complexo, isto é, pode haver mais de um tipo de grupo privilegiado.

# Definindo Group Fairness.

#### Statistical Parity Difference and Disparate Impact Ratio.
**Statistical Parity Difference**: É uma métrica de *fairness* que busca relacionar o *Disparate Impact* do modelo.
$$
\text{SPD} = Pr(\hat{y}(X) = \text{fav} | Z = \text{unpr}) - Pr(\hat{y}(X) = \text{fav} | Z = \text{priv})
$$
**SPD**: Statistical Parity Difference.
Quando $SPD=0$, então os grupos estão sendo selecionados *equal rates*. O caso negativo indica que grupos privilegiados estão sendo favorecidos e o caso positivo indica que os grupos desprivilegiados estão sendo favorecidos.
Portanto, o modelo deve ter e buscar **SPD** próximo de 0. 
$$
DIR = \frac{Pr(\hat{y}(X) = \text{fav} | Z = \text{unpr})}{Pr(\hat{y}(X) = \text{fav} | Z = \text{priv})}
$$
Nesse caso, queremos que $DIR$ (Disparate Impacted Rate) se aproxime de 1, isto é, $DIR=1$ implica em *fairness*.
Note que essas quantidades podem ainda ser classificados para diversos problemas. No caso de problemas de seleção de empregos o valor de $DIR$ deve estar entre $0.8 \leq DIR$

---
Divagação...
$$
\begin{align}
Pr(\hat{y}(X) = \text{fav} | Z = \text{unpr}) = \frac{Pr(\hat{y}(X) = \text{fav} , Z = \text{unpr})}{Pr( Z = \text{unpr})} \\
Pr(\hat{y}(X) = \text{fav} | Z = \text{priv}) = \frac{Pr(\hat{y}(X) = \text{fav} , Z = \text{priv})}{Pr( Z = \text{priv})}
\end{align}
$$
No caso de:
$$
\begin{cases}
Pr(\hat{y}(X) = 1) &= Pr(\hat{y}(X) = 1, Z = \text{unpr}) + Pr(\hat{y}(X) = 1, Z = \text{priv}) \\
Pr(Z=\text{priv}) + Pr(Z=\text{unpr})&= 1
\end{cases}
$$
$$
\begin{equation}
DIR = \frac{Pr(\hat{y}(X) = \text{fav} | Z = \text{unpr})}{Pr(\hat{y}(X) = \text{fav} | Z = \text{priv})} \implies DIR = \frac{Pr(\hat{y}(X) = 1, Z=\text{unpr}) \cdot Pr (Z = \text{priv})}{Pr(\hat{y}(X) = 1, Z=\text{priv}) \cdot Pr (Z = \text{unpriv})}
\end{equation}
$$
$$
DIR = \frac{Pr(\hat{y}(X) = 1) - Pr(\hat{y}(X) = 1, Z=\text{priv})}{Pr(\hat{y}(X)=1, Z=\text{priv})} \cdot \frac{p_{priv}}{p_{unpr}}
$$
Se tivermos que: $Pr(\hat{y}(X) = 1) = p_{ac}$ e $Pr(\hat{y}(X) = 1, Z = \text{priv}) = p_{acpr}$

$$
DIR = \frac{p_{ac} - p_{acpr}}{p_{acpr}} \cdot \frac{p_{priv}}{p_{unpr}} \implies DIR = \frac{p_{ac} - p_{acpr}}{p_{acpr}} \cdot \frac{1-p_{unpr}}{p_{unpr}} = \left( \frac{p_{ac}}{p_{acpr}} - 1\right) \cdot \left( \frac{1}{p_{unpr}} - 1\right) = \left( 1 - \frac{p_{ac}}{p_{acpr}} \right) \cdot \left( 1 -\frac{1}{p_{unpr}} \right) 
$$

---
OBS: Não resolveu nenhum problema esse desenvolvimento.

Parece ser algo meio óbvio de se pensar, mas $SPD$ e $DIR$ estão relacionados com a independência de $\hat{y}(X)$ e $Z$ (atributos protegidos).
Além disso, temos o *dataset fairness metric* e *classifier fairness metric*.
![[Pasted image 20250924203617.png|center]]
Isso é, é uma métrica bem geral. No caso de definir $DIR$ e $SPD$ basta substituir o $\hat{y}(X)$ por $Y$.

#### Average Odds Difference:
É uma métrica que só pode ser utilizada para avaliar um classificar e isso fica claro quando definimos:
$$
AOD = \frac{1}{2} \left[ Pr(\hat{y}(X) = \texttt{fav}|Y=\texttt{fav}, |Z = \texttt{unpr}) - Pr(\hat{y}(X) = \texttt{fav}|Y=\texttt{fav}, |Z = \texttt{priv}) \right] + \frac{1}{2} \left[ Pr(\hat{y}(X) = \texttt{unf}|Y=\texttt{unf}, |Z = \texttt{unpr}) - Pr(\hat{y}(X) = \texttt{unf}|Y=\texttt{unf}, |Z = \texttt{priv})\right]
$$

Mas veja que existem situações que podem esconder situações *unfair*, isto é, $AOD = 0 \centernot\implies \texttt{situação fair}$. Portanto, existe outra métrica associada que é a **Absolute Average Odds Difference**.
$$
AOD = \frac{1}{2} \left| Pr(\hat{y}(X) = \texttt{fav}|Y=\texttt{fav}, |Z = \texttt{unpr}) - Pr(\hat{y}(X) = \texttt{fav}|Y=\texttt{fav}, |Z = \texttt{priv}) \right| + \frac{1}{2} \left| Pr(\hat{y}(X) = \texttt{unf}|Y=\texttt{unf}, |Z = \texttt{unpr}) - Pr(\hat{y}(X) = \texttt{unf}|Y=\texttt{unf}, |Z = \texttt{priv})\right|
$$
**OBS:** Um valor de $AOD \approx 0$ indica que há independência entre $\hat{y}(X)$ e $Z$ condicionados por $Y$, que é justamente o caso de **Equality Odds**.

# Choosing Between Statistical Parity and Average Odds Difference.
Aqui devemos constatar a diferença fundamental entre dois tipos de observações do mundo, que refletem se consideramos que existe viés social na medida dos dados:
## We're all equal:
Aqui assumimos que todas as pessoas estão sujeitos de modo igual ou equivalente a uma situação. Os dados extraem diferenças estruturais e sociais entre cada grupo.
**Exemplo**: Pessoas negras utilizam menos o sistema de saúde por conta de um preconceito e não porque elas são mais saudáveis. Veja que nesse caso assumimos que o grupo de negros não é bem representável nos dados, pois os dados sempre serão enviesados e por isso nem faz muito sentido você avaliar através de acurácia.

Aplicar uma ideia de *distributive justice* é boa, visto que o seu *dataset* não representa a realidade (Por conta disso acurácia não é uma boa métrica). $SPD$ conside

## What you see is what you get:
Aqui assumimos que grupos diferentes possuem realidades diferentes. Então, o modelo deve sim levar em conta padrões diferentes entre grupos. Contudo, o sistema de Machine Learning não deve favorecer grupos de determinadas características.
**Exemplo**: Pessoas negras utilizam menos o sistema de saúde, isso é considerado um fato. Contudo, isso não deve ser considerado quando optamos por oferecer o serviço para uma pessoa branca que utiliza mais o serviço de saúde.

Como os dados são representações boas da realidade, então aplicar métricas como acurácia é uma boa situação. Contudo, devemos nos preocupar com acurácia de diferentes grupos. Veja que $AOD$ considera isso através dos falsos-positivos e verdadeiros-positivos de cada grupo.

#### Calibration by Group of Sufficiency.
A métrica de *sufficiency* é praticamente inverter a posição de $\hat{y}(X)$ e $Y$ no $AOD$. 
**OBS**: Aqui é comentado sobre o *calibrated classifier* que vem do problema de transformar um problema de classificação em um problema de acesso ao risco, isto é, desejamos uma probabilidade para os dados deles serem aceitos ou não. A questão é que eu não entendi muito bem como isso se converte em $Pr(Y=1|S=s) = s$. O que é $S$?
$$
APVD = \frac{1}{2} \left[ Pr(Y = \texttt{fav}|\hat{y}(X)=\texttt{fav}, |Z = \texttt{unpr}) - Pr(Y = \texttt{fav}|\hat{y}(X)=\texttt{fav}, |Z = \texttt{priv}) \right] + \frac{1}{2} \left[ Pr(Y = \texttt{unf}|\hat{y}(X)=\texttt{unf}, |Z = \texttt{unpr}) - Pr(Y = \texttt{unf}|\hat{y}(X)=\texttt{unf}, |Z = \texttt{priv})\right]
$$
OBS: APVD = Average Predictive Value Difference.
e o $AAPVD$ (Absolute APVD) que é análogo ao $AAOD$.

# Choosing Between Average Odds or Average Predicted Value:
A motivação para optar por um ou outro método é qual será a ação do efeito de um *label* dentro do modelo, isto é, o modelo é **Não-Punitivo** ou **Ajudante (Assistive)**.
Em casos **Ajudantes (Assistive)**: É preferível o **Equalized Odds** (Average Odds), pois beneficiamos os $TP$.
	Considere o caso do auxílio no **Sospital** e ainda a situação em que oferecemos um tratamento extra. Queremos oferecer o serviço de *Care Management* para pessoas que de fato apresentem o problema $TP$.
Em casos **Não-Punitivos:** 
	Se o paradigma agora é de optar por quem deve receber o tratamento (Ação não-punitiva), então a melhor métrica é **Sufficiency**. Porque em situações não-punitivas queremos acertar. Isto é, desejamos que $\hat{y}(X) \approx Y$

![[Pasted image 20250925154617.png|center]]
No caso do **Sospital** há um **Social Bias** dentro dos dados. Populações negras não se sentem confortáveis de ir uma certa quantidade de vezes nos serviços médicos. Portanto, a melhor escolha é a de *independência*. 

# Defining Individual and Counterfactual Fairness:
Aqui devemos introduzir a ideia de *interseção* entre grupos privilegiados e não-privilegiados. Por exemplo, você pode modelar para *Group Fairness* para **Homens x Mulheres** e **Negros x Brancos**. Mas uma **Mulher Negra** ainda pode apresentar uma situação *Unfair*.
Desse modo, queremos introduzir **Individual Fairness ou Consistency**. Que nos diz que indivíduos com *features* parecidas estão em regiões parecidas e devem receber *outcomes* parecidos.

## Consistency:
$$
\displaystyle \texttt{consistency} = 1 - \frac{1}{n} \sum_{j=1}^{n} \left| \hat{y}_j - \frac{1}{k} \sum_{i \in \mathbb{N_j}} \hat{y}_i\right|
$$ Aqui $\mathbb{N}_i$ define os $k$ vizinhos mais próximos de $j$.
- $\texttt{consistency} \approx1$, se os vizinhos são parecidos entre sí (Labels iguais).
- $\texttt{consistency} < 1$, se os vizinhos NÃO são parecidos (Labels diferentes)

Como essa distância deve ser computada é outra questão...

## Counterfactual Fairness:
Existem dois dados que são exatamente iguais, apenas diferem por um atributo protegido. A única maneira de isso ser *fair* é que ambos recebam o mesmo rótulo. Um teste dentro do modelo pode ser feito. Para cada atributo protegido faça a intervenção de mudar através de $do(Z)$. Se todos os labels se mantiverem iguais, então o sistema é **Counterfactual Fairness**. 
A verdade é que é muitas vezes impraticável realizar esse experimento, mas isso pode ser feito através da geração da relação causal entre atributos e caso o atributo protegido faça parte dessa relação, então o modelo é *unfair*.

#### Theil Index:
É uma métrica utilizada que combina tanto **Group Fairness**, quanto **Individual Fairness**. A questão aqui é que o **Theil Index** é 1 quando a sociedade é injusta e 0 quando é justa.
$$
\texttt{Theil Index} = \frac{1}{n} \sum_{j=1}^{n} \frac{b_j}{\bar{b}} \log \left( \frac{b_j}{\bar{b}}\right)
$$
- A escolha de $b_j$ deve ser estudada.
	Sugerido pelo leitor:
	$TP$: 1
	$FP$: 2
	$TN$: 1
	$FN$: 0
- dividimos por $\bar{b}$.

# Mitigating unwanted bias.
A questão até agora é que parece ser fácil criar sistemas sem *viés*. Contudo, o problema se torna mais proeminente quando introduzimos outras features que tem relação com atributos protegidos e esses atributos protegidos tem relação com a saída.

Existem métodos para mitigar bias para as três fases principais de um modelo de machine learning, isto é, *pre-processing*, *in-processing* e *post-processing* e quanto mais próximo do começo do pipeline, melhor será o resultado (Contudo, mais difícil de se aplicar).

Para escolher um algoritmo de *bias mitigation* você deve:
1) Saber em que parte do pipeline você irá atuar.
2) Considerar a sua visão de mundo (**We're all the same** or **We are what you see**).
3) Entender se atributos protegidos serão usados como **Features**.

![[Pasted image 20250925201939.png|center]]


# Pre-Processing:
- Não incluem métricas de *fairness* que utilizem a previsão do modelo, pois o modelo não existe.
Desse modo, a MAIORIA (não todos) dos modelos de *mitigating bias* dentro do pre-processing estão associados com a visão de mundo de **We're all the same**. 

1) Inserir novos *datapoints* através da inversão de atributos protegidos de *datapoints* já conhecidos. Aqui podemos gerar uma semelhança com o método de **Counterfactual Fairness**. Parecem haver diversos detalhes em como inserir esses pontos de modo rigoroso, além disso cada maneira de inserir os dados influencia para sua visão de mundo sobre os dados.
2) Inserir *sample weights*, como *probability weighting* e *importance weighting*. Esse método consiste em melhorar a métrica **SPD**, portanto, a visão de mundo é **We're all equal**.
   A ideia aqui é introduzir os pesos de modo que buscamos a característica principal de independência de variáveis aleatórias, isto é, a função de probabilidade conjunta é o produto das funções de probabilidade marginais.
$$
w_j = \frac{Pr_Y (y_j) \cdot Pr_Z (z_j)}{Pr_{Y,Z} (y_j, z_j)}
$$
   - Veja que não precisamos dos atributos protegidos no modelo final, contudo, devemos treinar esses pesos.
   **OBS**: Sinceramente, eu não lembro direito do *probability weighting* e *importance weighting*.
1) Os métodos anteriores não modificam o *dataset*, contudo o método do **Massaging Flips** modifica. A ideia é alterarmos *labels* de grupos desfavorecidos para *labels* favoráveis e vice-versa. Aqui tentamos melhorar a estatística de $SPD$ e estamos na visão de mundo **We're all the same**. 
   Os **datapoints** escolhidos são aqueles que estão mais próximos da **Decision-Boundary**, pois tem menos confiança e, portanto, são naturalmente mais sugestíveis à mudança. 
**OBS:** Como você gera uma **Decision-Boundary** sem um modelo treinado?
2) **Fair Score Transformer**. Não entendi muito bem como funciona.

# In-Processing.
Basicamente, introduzimos algum termo dentro da função de *Risco/Custo*. Existem diversos métodos aqui, mas o autor não entra em muitos detalhes.

# Post-Processing.
Parece que você tenta fazer alguma engenharia reversa dos processos apresentados no **Pre-Processing**. 

# Conclusion.
Algumas perguntas nos guiam a selecionar o método mais adequado.
- Em qual parte do **Pipeline** você consegue fazer alterações?
- Qual visão de mundo você decidiu com o **Problem-Owner**?
- Os atributos protegidos estão dentro do **Dataset**?
![[Pasted image 20250925204744.png|center]]
