Para compilar o pacote **Temis** posso rodar dentro da raiz do projeto o seguinte comando.
```
pip install -e .
```
Após isso as modificações foram:
- Importei o pacote **german** e armazenei-o dentro de datasets.
- Criei uma pasta **notebooks** para criar jupyter notebooks para desenvolvimento das funções e exploração.
- Criei a pasta **Temis** que armazena todo o pacote **Temis**.
- Implementei algumas funções de métrica de fairness e métricas comuns de machine learning.
- Métricas implementadas: Accuracy, Precision, Recall, F1-Score e Brier-Score.
- Métricas de fairness implementadas: SPD, DIR, AOD e AAOD.

**Próximos-Passos**:
- Implementar outras métricas de fairness como APVD (Average Predictive Value Difference).
- Comparar o resultado do meu LogisticRegression com o LogisticRegression de outro pacote como o scikit-learn.
- Implementar Intersectional Group Fairness.

**Dúvidas**:
- Qual a diferença entre sufficiency e separation?
