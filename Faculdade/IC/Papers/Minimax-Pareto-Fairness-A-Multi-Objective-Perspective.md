# Escritores:

# Conteúdo:
## Introdução.
- Tomar decisões que impactam a vida das pessoas deve ser feito de modo justo e certeiro.
- Treinar classificadores de modo ingênuo pode resultar em classificadores com **Bias** e previsões **Ruins**.
- Classificadores que levam em consideração **Demographic Parity**, **Equality of Odds** e **Individual Fairness** parecem não ser adequados o suficiente para serviços em que a qualidade do serviço é essencial. - Introduzir um modelo que não cause **No Unnecessary Harm**.
- Desse modo, o artigo introduz um classificador que leva em conta **Predictive Risk Disparities**.
- Formular um problema de **MOOP** e introduzir aspectos de **Pareto Otimalidade**.
- Eu não entendi porque o conceito de aumentar o risco de um grupo causar a diminuição de risco em outro grupo é chamado de **No Unnecessary Harm** - O **Unnecessary Harm** não ocorre quando conseguimos apenas reduzir o risco de um grupo?
  Eu acho que o que ele quis dizer aqui é o fato de que aumentar o risco de um grupo vem sempre acompanhado da diminuição do risco de outro grupo, isso não quer dizer que a diminuição do risco de um grupo causa o aumento do risco de outro grupo. Portanto, faz sentido entender isso como um otimizador do tipo **No Unnecessary Harm**.
- Find the Model such that it has the **smallest maximum group risk among all other models** (que estão presentes nessa fronteira de Pareto).
- A ideia de **Zero Risk Disparity** só é alcançada quando isso propõe algum ganho para o grupo em desvantagem. Desse modo não introduz uma política de **Zero Risk Disparity** como Design.
- Além disso o modelo proposto não precisa de acesso à **Sensible Feature** em tempo de teste.
- Consegue identificar o **Pareto-Efficient Classifier** a partir de **Convex Models** e **Convex Risk Functions**.
- Real-World applications: **Adult Dataset, MIMIC-III Dataset, HAM10000 Dataset, German Credit Dataset**




# Artigos Citados e suas contribuições:
Artigos que comentam sobre algumas definições de group fairness através de independência com o **Sensitive Feature**. (**Demographic Parity**).
- Louizos et al. - 2015
- Zemel et al. - 2013
- Feldman et al. - 2015
Artigos que comentam sobre obtenção de fairness através de independência da **Sensitive Feature** dado **Objective Ground Truth** (Equality of Odds).
- Hardt et al. - 2016
- Woodworth et al. - 2017
Artigos que comentam sobre noção de Individual Fairness.
- Dwork et al. - 2013
- Joseph et al. - 2016
- Zemel et al. - 2013
Artigos que comentam sobre a introdução do Decoupled Classifiers para não introduzir Unnecessary Harm.
- Ustun et al. - 2019
Artigos que comentam sobre **Zero Disparity Risk** por Design.
- Hardt et al. - 2016
- Woodworth et al. - 2017



---
# Perguntas
Como o risco de cada grupo é computado?

Como o conceito de MOOP é introduzido para resolver o problema de Fairness?

1) Qual é o papel dos algoritmos de aprendizado de máquina que motivou a necessidade de critérios de justiça (fairness)?
   ?
   O papel dos algoritmos de aprendizado de máquina que motivou a necessidade de adicionar fairness vem do fato de esses algoritmos estarem sendo utilizados para tomar decisões que afetam (e bastante) a vida das pessoas.
   
2) Quais são alguns exemplos de **decisões de alto impacto** mencionadas no texto onde é crucial que as previsões sejam precisas e imparciais?
   ?
   Hiring, Credit-Lending and Predicting Mortality at Intensive Care Units are some of the examples.

3) O que o texto sugere que pode acontecer com um modelo treinado de forma ingênua (naively)?
   ?
   Pode ocorrer de que um classificador treinado de modo ingênuo tenha características como baixa taxa de acerto nas suas decisões, assim como um viés muito forte para decidir baseado em questões sensíveis.

4) Quais são as duas categorias principais de **justiça de grupo** (group fairness) amplamente conhecidas na literatura que o texto menciona, e quais exemplos de definições se encaixam nelas?
	?
	  

5) Em domínios críticos, como saúde (healthcare), qual critério de justiça o artigo defende que deve ser buscado, além de apenas tentar a justiça perfeita (perfeitamente fair)?

6) Qual é a definição central de justiça que o artigo adota para formalizar o conceito de "não causar dano desnecessário" (no unnecessary harm fairness)?

7) Como o problema de **justiça de grupo** é formalmente caracterizado no trabalho, e o que representa cada "objetivo" na estrutura proposta?

8) O que é o critério de **Minimax Risk** (Risco Minimax) no contexto da justiça de grupo?
