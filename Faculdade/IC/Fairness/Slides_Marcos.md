# Contexto:
A contextualização dos slides é a mesma da fornecida no Trustworthy Machine Learning. 
- **Sospital** health insurance company.
- Principal problema é identificar clientes que podem se beneficiar do **Extra Care Management**.

## Tipos de Justiça:
1) **Distributive Justice**. - Grupos diferentes recebem o benefício de modo equivalente.
2) **Procedural Justice**. - Indivíduos parecidos recebem o benefício de modo equivalente.
3) **Restorative Justice**. - Repara danos históricos introduzidos.
4) **Retributive Justice**. - Punir *Wrongdoers*.

O foco maior é em **Distributive Justice** para sistemas de **Machine Learning**.

- Razão para implementar **Fairness** -> Diminuir **Privilégios** introduzidos dentro do Sistema.
- **Privilégios**: Resultam de balanços não proporcionais de poder.
# Protected Attributes:
- Não há conjunto universal de atributos protegidos.
- São geralmente determinados por Leis, Regulações e outras políticas.
**PERGUNTA**: Onde podem ser encontradas essas Leis e Regulações. Exemplos no caso Brasileiro.

# Group Fairness and Individual Fairness:
**Group Fairness**: O Classificar deve, na média, introduzir os mesmos comportamentos entre grupos diferentes.
**Individual Fairness**: O Classificador deve, na média, introduzir os mesmos comportamento entre indivíduos parecidos.

# Where Does Unfairness Comes From?
- Principalmente vem de **Unwanted Bias**
- **Social Bias**: Quando vamos do *Constructed Space* para o *Observed Space*.
- **Representation Bias**: Quando vamos do *Observed Space* para o *Raw-Data Space*.

## Social Bias:
- O dataset consiste em decisões tomadas no passado e, portanto, podem conter **Bias** dos Classificadores Humanos.

## Representation Bias:
- A empresa **Sospital** oferece seus serviços, majoritariamente, para pessoas brancas?

## Other Sources of Bias:
Podemos introduzir **Bias** dentro da fase de **Problem Specification** e **Data Preparation**.
- Exemplo: Se introduzirmos uma variável de gradação quanto ao uso do plano, então introduzimos viés que favorece populações brancas.

# Distribution Shift and Fairness.
- O **Distribution Shift** é mais utilizado quando temos acesso imediato ao *Construct Space*.
- Em um cenário de **Fairness** é impossível ter acesso ao *Construct Space*. Portanto, lidamos com **Fairness** através de políticas e métricas quantitativas.

- Accuracy.
- Precision.
- Recall.
- F1-Score.
- AUC -> ROC-curve.
- Calibration Curve -> Brier-Score.
# Exemplo computar Recall e Precision:
**Precision**: $n_{TP} >> n_{FP}$, isto implica que desejamos classificar emails como spam apenas quando temos certeza da decisão.
**Recall**: $n_{TP} >> n_{FN}$, isto implica que desejamos classificar emails spam como spam, sem nos preocupar tanto com a taxa dos verdadeiros.

