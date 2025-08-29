# Conceitos apresentados nesse capítulo:

- Dados são valiosos e gerados pelas pessoas, então não devemos retribuir utilizando esses dados para ferí-las.
- Dados são fornecidos pelas pessoas, então elas devem dar permissão para utilizá-los.
- Mesmo que os dados tenham sido fornecidos, ainda devemos nos preocupar com privacidade.
- Syntactic Anonymity: Dados quasi-identificadores são agrupados e, portanto, difíceis de rastrear pessoas específicas. Usado em Data Publication.
- Differential Anonymity: Dados sensíveis são apresentados com ruído. Usado em Data Mining.

# Presentation:

Chapter context: TraceBridge é um app mobile que irá auxiliar as pessoas a voltarem ao trabalho presencial após uma pandemia. Note que diversas informações serão necessárias como:
- Location Traces
- Health-Related Measurements
- Social Data
- Administrative Data

Contudo, todas essas informações podem gerar perguntas pertinentes para um usuário:
- Does TraceBridge store the data from all employees in a centralized database?
- Who has access to the data?
- What would be revealed if there were a data breach?
- Have the employees been informed about possible uses of the data and agreed to them?
- Does the organization have permission to share their data with other organizations?
- Can employees opt out of the app or would that jeopardize their livelihood?
- Who gets to know that an employee has tested positive for the disease?
- Who gets to know their identity and their contacts?

As questões principais levantadas pelas perguntas são: Existem dados que devem ser ponderados se devem ou não ser inseridos dentro de um contexto de Machine Learning por razões de Consent, Diffusion of Power e Privacy.

As atividades que serão realizadas aqui são:
- weigh the need for consent, diffusion of power, and privacy
- differentiate different kinds of anonymity for privacy
- question whether anonymity is the only way to achieve privacy

# Consent, Power and Privacy.
Note que apesar de ser mais simples e eficiente utilizar a abordagem de extrair informações de redes sociais e movimentação do celular. Introduzimos aqui o poder para uma instituição de decidir quem será empregado ou não através de dados sensíveis e que não seriam expostos. Aqui há um certo paradoxo, pois apesar de o efeito poder ser bem melhor dado a não consideração de privacidade, ainda sim é direito e valor, dentro de diversos sistemas de valor, a privacidade. 
Essas questões são ainda mais importantes quando pensamos que diversos datasets de Machine Learning são, na verdade, dados extraídos de outras atividades. Pense que a maior parte dos datasets de treino para algoritmos de Visão Computacional são extraídos sem permissão explícitas da internet.
Ainda mais, note que essas questões se tornam mais aparentes no momento que instituições passam a exigir isso dos aplicativos.

# Achieving Privacy through Anonymization.
- Data Publishing: non-interactive anonymization.
- Data Mining: interactive anonymization.

Three categories of data:
- Identifies: Reveal identity of a person. (They must be dropped from the dataset).
- Quasi-Identifiers: They don't generate answer by themselves, but can be used in the process of re-identification.
- Sensitive Attributes: Data that people don't want to be revealed.

Syntactic anonymization: Usar um processo de modificação dos dados Quasi-Identifiers para que a informação deles seja reduzida. (Suppressing, Generalizing, Shuffling).
Differential Privacy: Adding noise to sensitive attributes.

![[Pasted image 20250819145629.png|center]]
Sobre os próximos tópicos:
	A Syntactic Anonymity parece ser mais utilizada para resolver problemas de publicação dos dados. 
	A Differential Privacy parece ser mais utilizada para resolver problemas de data mining.
# Data publishing and Syntactic Anonymity.
A forma apresentada aqui é através da **k-anonymity**.
Exemplos desse processo de usar dados Quasi-Identifiers:
- Suppressing: Trocar um valor por um tipo NULL.
- Generalizing: Em vez de usar um Zip-Code utilizar apenas o primeiro dígito.
A ideia aqui é que para cada atributo Quasi-Identifier você consiga encontrar $k$ pessoas com mesmo atributo.
Note que se tivermos $n$ pontos, então haverão agora $n/k$ classificações e o ideal é que todos os grupos tenham mesma cardinalidade.

**Weakness:**
- Homogeneity Attack: Se um grupo com $k$ registros tiver homogeneidade dentro os seus dados, então sabemos que indivíduos daquele grupo são parecidos entre sí. Aqui o processo é identificar padrões sobre características de cada grupo e dado que você tenha dados de uma pessoa que se encaixa nesse grupo, então você infere uma característica dessa pessoa. Por exemplo, se você tem acesso a dados como CEP e Idade de uma pessoa, então se diversas pessoas dentro de um banco tiverem mesmo CEP e Idade e uma característica comum, então a pessoas pode ser colocada nessa caixa. 
- Background Knowledge Attack: A grande estratégia aqui é realizar estatística sobre grupos. Desse modo, padrões como Subgrupos com padrões específicos, Informações auxiliares e Inferência de atributos sensíveis podem tornar o processo de mapeamento de informações possível. Por exemplo, se uma pessoa mora no CEP 1234 e você sabe que dentro do seu dataset pessoas com esse CEP apresentam certa característica, como, por exemplo, pertences de valor alto. Então sabemos que Maria que mora nesse CEP é altamente provável de conter pertences de valores alto.

OBS: Uma coisa legal é simular através de um banco de dados cada um desses ataques.

Uma maneira de superar essas questões é através da **l-diversity**, em que cada **k-group** deve possuir ao menos $l$ valores distintos de valores-sensíveis.
Uma melhor ainda da **l-diversity** é a **t-closeness**. Cada grupo deve apresentar uma distribuição de dados sensíveis similar a presente no dataset total e todos os grupos devem apresentar essa característica também. o $t$ vem de uma distância especificada.

Note que podemos quantificar o processo de re-identificação do nosso processo de anonimicidade.
$X:$ random variable quasi-identifier in original dataset.
$\tilde{X}:$ random variable quasi-identifier in anonymity dataset.
$W:$ random variable sensitive attributes.
- $I(X,\tilde{X}) \leq \log(\frac{n}{k})$ -> k-anonymity.
- $I(W, \tilde{X}) \leq H(W) - \log(l)$ -> l-diversity.
- $I(W, \tilde{X}) \leq t$ -> t-closeness.

# Data Mining and Differential Privacy.
Differential privacy applies to use cases involving querying a dataset, not simply releasing it. Aqui desejamos que os dados sejam expostos aos usuários de modo que um ruído seja adicionado de modo a não revelar a identidade por completo.

Aqui a principal diferença entre o Syntactic Anonymity (Onde a privacidade é atingida e depois não precisamos nos preocupar mais) a organização deve sempre manter controle do anonimato. O método mais comum é **adicionar ruído** nas variáveis sensíveis.

$W_{1}$: Dataset com dados de pessoas com diagnósticos de uma doença viral.
$W_{2}$: Adicione a $W_{1}$ uma pessoa nova.

Se $y(W) \rightarrow \#\text{Pessoas com Cancer}$
Então para um sistema considerar segurança, devemos na verdade retornar $\tilde{y}(W)=y(W) +\text{noise}$
O objetivo é determinar uma função de modo que:
$$
Pr(\tilde{Y}(W_{1}) = \tilde{y}) \leq e^{\epsilon} \cdot Pr(\tilde{Y}(W_2) = \tilde{y}), \forall \tilde{y}
$$
$\epsilon$: Parâmetro (geralmente pequeno) que define o nível de privacidade.
Quando $\epsilon$ é próximo de zero, então não conseguimos distinguir entre probabilidades dos dois datasets. Contudo, adicionamos um novo dado, então é claro que a probabilidade é alterada. De modo que, o objetivo é justamente atingir esse ponto em que os dataset são indistinguíveis. A ideia aqui é que adicionar um novo dado não altera a distribuição de probabilidade significativamente.

Supondo que o dataset seja uma variável aleatória $W$, então $\tilde{Y}$ é um dataset com dados ruidosos. Desse modo, queremos minimizar as correlações entre variações dos dados com ruído e sem ruído. Dado que $Pr(\tilde{Y} | W=w_1)$ define a probabilidade condicional de um dado ruidoso, condicionado pelo dataset. Se tivermos dois datasets quase idênticos, então devemos ter que $Pr(\tilde{Y} | W=w_1)\approx Pr(\tilde{Y} | W=w_2)$, isso garante que não conseguimos rastrear se um dado estava ou não no dataset e, portanto, isolamos o dataset original. Então queremos minimizar $I(W, \tilde{Y})$, pois isso garante que sabermos sobre $\tilde{Y}$ não garante nada sobre o dataset original.
A partir de um desenvolvimento teórico, conseguimos traçar que $\epsilon$ está relacionado com a minimização da informação mútua e, portanto, a minimização dele garante um dataset privado.

Aqui definir o dataset como uma variável aleatório implica que conseguimos quantificar a quantidade de informação que ele carrega.

# Conclusion
- Aqui ele cita um tradeoff de privacidade e utilidade de um dataset. Isso aqui é interessante mesmo, porque se você modifica muito um dataset ele perde toda informação e valor.
- Além disso, note que o campo ideal é utilizar um $\epsilon$ próximo de zero. Só que as pessoas que consultarão os dados irão ver dados cheio de ruído, de modo que devemos conciliar essa questão também.

# Other ways of achieving Privacy.
Um jeito de garantir privacidade de dados é "trancando eles e jogando a chave fora", i.e., não publicar os dados e não garantir meios de query. Mas aqui não temos utilidade.

Uma maneira de garantir privacidade é através de controle institucional de acesso aos dados. Portanto, apenas pessoas qualificadas e com normas bem definidas e controladas de acesso aos dados poderão acessá-los. Além disso, podemos colocar os dados espalhados, em vez de centralizados em um único datacenter.

Outra maneira de garantir privacidade é trazer o algoritmo para os dados e não os dados para o algoritmo. (OBS: Não entendi muito bem como que isso é diferente.)

Uma terceira maneira é através de Criptografia: Fully homomorphic encryption. Podemos fazer computação sobre os dados e adquirir os mesmos resultados.

As três outras maneiras podem ser resumidas em:
- Institutional Controls.
- Secure Multi-Party Computation.
- Fully Homomorphic Encryption.
