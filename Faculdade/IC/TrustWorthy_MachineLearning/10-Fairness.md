# Contexto:
**Sospital** é uma agência de *health insurance* nos EUA. Você deve ajudar o *problem owner* a encarar a tarefa de automatização da escolha de pacientes que devem fazer parte do sistema de **Care Management**.
**Care Management**: Se trata de um setor de diversos profissionais que atuam em conjunto para tratar de modo preventivo situações crônicas ou situações complexas.

**Problema principal**: Automatizar um processo que é feito principalmente de modo manual para escolha de pacientes que devem fazer parte desse programa.
Contudo, você como um bom projetista de sistemas de *machine learning* começa a consultar os diferentes *stakeholders*. Nesse sentido, uma rápida entrevista com pacientes **negros** possibilitou identificar uma desconfiança com os planos de saúde que não estão oferecendo esses serviços de modo satisfatório para essa população.

> O Sistema precisa ser justo e não conter viés indesejado.

**Solução**: Projetar uma solução que considere ,através da fase de *problem specification*, um modelo *fair* para alocação de recursos dentro do *Care Management* para a empresa **Sospital**.
- Comparar as diferentes definições de *fairness* no contexto de *machine learning*.
- Selecionar a definição que mais se adequa ao problema.
- Mitigar viés indesejado através de uma fase de modelagem que considere questões de *fairness*.

**Perguntas Iniciais**:
- Por que existem diferentes tipos de definições de *fairness*?
- Como uma definição específica se adequará a um tipo específico de problema?
- Como garantir que viés indesejado não seja introduzido na fase de modelagem.

# Diferentes definições de *Fairness*.
Existem diferentes tipos de *fairness* justamente pela dificuldade de conseguir modelar sem o contexto social explícito. Além disso, como diferentes situações sociais geram diferentes respostas à questões de desigualdade, então não é muito viável apresentar uma definição técnica. Apesar disso, o tratamento de *fairness* dentro do contexto de solução para sistemas de *machine learning* apresentará uma robustez técnica.

Veja que a definição de um sistema *fair* possuir diversas ramificações
1) Um sistema pode prezar pela *equality* de serviços oferecidos por diferentes grupos - *distributive justice*.
2) Um sistema pode prezar por escolher de modo similar entre diferentes grupos - *procedural justice*.
3) Um sistema pode prezar por optar por situações de reparo - **restorative justice**.
4) Um sistema pode introduzir justiça penalizando pessoas que tomam ações erradas - **retributive justice**.

Uma *Rule of Thumb* é sempre fazer o design de um sistema através de *distributive justice*, pois a maioria dos sistemas focam apenas no contexto de analisar fins de uma determinada ação. Isto é, a pessoa recebe o benefício de receber o serviço e pronto. Veja que a adição desses outros tipos de *justice* podem ajudar a descobrir onde certos sistemas podem ser inseridos e onde não podem ser inseridos.
**OBS**: Acho que no trabalho do *Caio* a ideia de atribuir empréstimos para as pessoas é mais guiado pela política de *retributive justice*. Então podemos perceber um contexto em que *distributive justice* não se insere bem. 
**OBS**: Eu não entendi como isso acontece muito bem, porque se você fizer *retributive justice* e um determinado grupo tiver mais probabilidade de fazer ações erradas, então eles não serão incluídos na distribuição. Assim isso acaba afetando *distributive justice*. É isso?

Pensando na questão do serviço oferecido pelo **Sospital**, como são recursos limitados o mais correto não seria introduzir *procedural justice*?
- Mas outra pessoa poderia introduzir a questão de oferecer o serviço para pessoas mais afetadas por uma questão - *restorative justice*.

Esses tipos de vantagens são aceitáveis dentro do contexto de desenvolver um sistema de *machine learning*. 

**Reconhecer vantagens inaceitáveis e injustas**: Quando o sistema claramente classifica um grupo privilegiado e outro desprivilegiado.
A questão aqui é considerar que esses grupos privilegiados e desprivilegiados são definidos através de uma questão histórica e cultural. Por exemplo, pessoas brancas podem ter mais acesso aos recursos financeiros de uma instituição bancária, pois historicamente os grupos de negros foram afetados pela escravidão.

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
Quando $SPD=0$, então os grupos estão sendo selecionados *equal rates*.
Portanto, o modelo deve ter e buscar **SPD** próximo de 0. 
$$
DIR = \frac{Pr(\hat{y}(X) = \text{fav} | Z = \text{unpr})}{Pr(\hat{y}(X) = \text{fav} | Z = \text{priv})}
$$
Nesse caso, queremos que $DIR$ se aproxime de 1.

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