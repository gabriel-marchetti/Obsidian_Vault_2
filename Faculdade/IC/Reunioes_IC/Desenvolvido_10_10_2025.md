# Comparação meu LogisticRegression vs LogisticRegression do SKLearn.

- Comparei com o LogisticRegression do SKLearn para alguns solvers específicos.
- Escolhi comparar como base o LogisticRegression com o 'liblinear', porque esse gerou uma AUC melhor.

**OBS**:
- Não entendi porque o AUC-Score precisa ser comparado com o predict_probability e não com o predict_label? Acho que deve ser, porque o predict tem embutido o threshold que não quero incluir na análise.