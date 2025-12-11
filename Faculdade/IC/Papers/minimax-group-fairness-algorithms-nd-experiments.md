I will follow the paper reading method suggested by Peter Klein - [[general]]
# 1.a) Abstract:
- **Fairness** as *worst-case* outcomes across groups - contrast between [[Fairness-Aware_Classifier_With_Prejudice_Remover_Regularizer]] that uses a general score.
- Provably convergent oracle-efficient learning algorithms for minimax-group-fairness.
- Main idea: Minimize Maximum loss across all groups.
- Flexibility in using: Regression or Classification / Overall error, False positive rate or False negative rate.
- Supports relaxation of fairness parameter.
- Minimax is preferable in some contexts rather than Equal-outcomes.
# 1.b) Introduction:
- "Equal outcomes" has this hope of achieving lower error rates for disadvantaged group - it is not always the case - creating artificial error (inflating error) in well understanded groups.
- It is not always the case that we are "Taking from the rich and giving to the poor", so inflating the error in well understood groups in not a good idea - predicting domestic situation is an example such that this is not the case.
- Any model that achieves Minimax-group-fairness *Pareto dominates* an equalized-error model with respect to group error rates.
- Apparently you can achieve a minimax-fairness scenario and inflate error rates to achieve and equal-outcomes scenario.
- Advantages over a model for each group (this is a type of minimax-group fairness, because we are trying to minimize every model) 
	(1) groups do not need to be disjoint 
	(2) minimax approach does not require protected attribute as input for the trained model.
**Steps Taken**:
1) Define two algorithms
	1.1) the first one finds a minimax group fair model.
	1.2) Second navigates trade-offs between minimax fairness and accuracy.
2) Both algorithms converge and are oracle-efficient.
3) Framework can be extended to other measures and models - how to handle overlapping groups.
4) Experimental analysis of this two algorithms.
	4.1) Explore learning process of regression model
	4.2) Conduct fairness vs accuracy trade-off in (4.1).
	4.3) Explore learning process of classification model.
	4.4) Conduct fairness vs accuracy trade-off in (4.3).
# 1.c) Conclusion:
- Provably convergent algorithm for solving minimax-group-fairness and error minimization for groups under a upper bound - works if sample weights are being used and generalization guarantee of base class of models.
- Method works for weighted empirical risk minimization problems.
- In Classification settings it can be used as a principled heuristic.
- Better performance than equal-outcomes.

# 1.d) Skim middle section:
## Section Names:
2) **Framework and Preliminaries**.
3) **Two-Player Game Formulation**.
	3.1) Algorithm 1 - MinimaxFair.
	3.2) Algorithm 2 - MinimaxFairRelaxed.
4) **Theoretical Guarantees**.
	4.1) Assumption - Oracle Efficiency.
	4.2) MinimaxFair theoretical guarantees.
	4.3) MinimaxFairRelaxed theoretical guarantees.
	4.4) Generalization.
5) **Extension to False-Positive/False-Negative Rates**.
6) **Experimental Results**.
	6.1) Methodology and Data
		6.1.1) Description of datasets.
		6.1.2) Train/Test Methodology.
		6.1.3) Regression - Finding exact solutions efficiently.
		6.1.4) Classification - Non-convexity of 0/1 Loss.
		6.1.5) Paired Regression Classifier.
		6.1.6) Relaxation Methodology.
	6.2) Linear Regression Experiments.
		6.2.1) Comparing Minimax to Equality.
		6.2.2) Relaxing Fairness Constraints.
	6.3) Classification Experiments.
		6.3.1) Comparing Minimax to Equality.
		6.3.2) Relaxation and Pareto Curves.
		6.3.3) False Positive and False Negative Rates.
	6.4) Demonstrating Generalization.
		6.4.1) Regression.
		6.4.2) Classification.
## Section Tables:
![[Pasted image 20251127154052.png|center]]
Apresentação dos datasets e algumas características presentes nele.
## Section Figures:
![[Pasted image 20251127154230.png|center]]
Location: 6.2 - Linear Regression Experiments.
Figure 1 Description:  We can see that there is no inflation in advantaged groups. This implies in more weight over disadvantaged groups in image at the middle. Moreover we can see in the right image that there is a tradeoff between $\texttt{population error X max group error}$.

![[Pasted image 20251127154259.png|center]]
Location: 6.2.1 - Comparing Minimax to Equality.
Figure 2 Description: As we can see here the Equal-Outcomes way inflated the error in groups that were easier to predict, such as Summer and Autumn. In contrast, the Minimax way inflated the error in easier to predict groups, but it was way less inflated than the Equal-Outcomes.

![[Pasted image 20251127154427.png|center]]
Location: 6.2.2 - Relaxing Fairness Constraints.
Figure 3 Description: As we can see as we relax $\gamma$ we see that $\texttt{max population error}$ increases, as theory suggests. But we can control this trade-off via this $\gamma$ parameter.

![[Pasted image 20251127154526.png|center]]
Location: 6.3.1 - Comparing Minimax to Equality
Figure 4 Description: A less smooth visualization of Figure 2 happens when we are under classification methods, i.e., Equal-Outcomes inflate error, Minimax also does but more controlled.

![[Pasted image 20251127154623.png|center]]
Location: 6.3.2 - Relaxation and Pareto Curves.
Figure 5 Description:  Apparently when you use a convex loss function  this trade-off tends to be smooth.

![[Pasted image 20251127154703.png|center]]
Location: 6.3.3 - False Positive and False Negative Rates.
Figure 6 Description: You can use other ways of measuring max group error (through FP as shown) and all the previous results will still hold.

![[Pasted image 20251127154758.png|center]]
Location: 6.4.1 - Demonstrating Generalization - Regression.
Figure 7 Description: The method can be generalized to hold for $\texttt{train-tess split}$ under regression 

![[Pasted image 20251127154843.png|center]]
Location: Demonstrating Generalization - Classification.
Figure 8 Description: The method can be generalized to hold $\texttt{train-test split}$ under classification.
# 1.e) First Read.
The first argument that tells us that Equal-Error can be worst than Minimax-Group-Error is the simple argument.
Suppose there are errors for groups $g_i$ (error rate on group $i$ in a minimax solution) and $g'$ (common error rate between all groups in Equal-Outcomes). We state that the minimax solution will achieve conditions such that $(\forall i)\;\; g_i \leq g'$.
So if there is only one group $j$ such that $g_j = g'$, then Equal-Error will inflate the errors of all groups that are not $j$.

## Framework and Preliminaries:
We have a **Dataset** such that $\mathbb{D} = (x_i, y_i)_{i=1}^{n}$, where $x_i$ : features and $y_i$ : labels.
$\mathbb{D}$ is divided into $K$ groups - $\left\{ G_1, \cdots, G_K\right\}$
$\mathbb{H}$ is a *class of models* such that $H: x_i \mapsto y_i$
$L$ is a loss function such that $L(x_i, y_i) \in [0, 1]$

Average **population** error: $\epsilon(h) = \frac{1}{n} \sum_{i=1}^{n}  L(h(x_i), y_i)$
Average **group** error: $\epsilon_k(h) = \frac{1}{|G_k|} \sum_{(x,y) \in G_k} L(h(x), y)$ 
When $\Delta H$ is being used it means we have a randomized class of models.

### First Minimax Problem:
$$
h^{*} = \text{argmin}_{h \in \Delta H} \Big\{ \text{max}_k \;\;\epsilon_k(h) \Big\}
$$
**OPT1**: A solution in $\epsilon$-approx to OPT1, if the model is such that $\max_k \;\;\epsilon_k(h) \leq \max_k\;\; \epsilon_k(h^{*}) + \epsilon$
Then we can reverse the problem by stating there is such a $\gamma$ that $\gamma \geq OPT1$. 
This says that $\gamma$ is a **Maximum group error threshold**.

### Second Minimax Problem:
There are numerous $h$'s that satisfies OPT1, then if we define the problem this way:
$$
\begin{align}
\min_{h \in \Delta H} \epsilon(h) & \\
\text{subject to  } & (\forall k \in K), \epsilon_k(h) \leq \gamma
\end{align}
$$
**Advantages**:
- If we define good population error function, there will be only one optimal point.
- We can establish a trade-off between minimizing population error and inflating the $\gamma$ parameter - beneficial conditions are those that a small increase in $\gamma$ can result in a big decrease in $\epsilon(h)$ - **MAYBE EXPLORE A METHOD/ALGORITHM FOR THAT?**

We can define a second optimal condition:
A model $h$ is $\epsilon$-approx in regards of OPT2, if $\epsilon(h) \leq \epsilon(h^*) + \epsilon$

**Idea for implementing the algorithms**: Two-Player Game Formulation. But they define a Weighted Empirical Risk Minimization Oracle over the class H.
**WERM(H)**:
**INPUTS**>
	$\mathbb{D}$ : Dataset.
	W : Weighting of points
	L : Loss Function.
**OUTPUTS**>
	$\hat{h} \in H$, such that, $\hat{h} \in \text{argmin}_{h \in H} \Big[ \sum_{i=1}^{n} w_i \cdot L(h(x_i), y_i)\Big]$

## Two-Player Game Formulation:
- Zero-Sum Game - Learner and Regulator - **QUESTION**
- Exponential Weights Algorithm - **QUESTION**

**Algorithm Properties**:
- Learning Rate can be used as $\eta_t \approx \frac{1}{\sqrt{t}}$
- The model will output a sequence of models such that $\{ h_1, h_2, \cdots, h_T\}$ and you can use two methods for defining the **predict_proba** method.
	(1) Take the uniform weights of all models into the prediction.
	(2) Take a random $h_j$ and use it as the prediction.

**MinimaxFair**:
INPUTS>
- $\mathbb{D}$ : Dataset
- $\eta_t$ : Adaptive learning rate
- $G_k$ : Populations with size $p_k = \frac{|G_k|}{n}$
- T : Iteration count
- L : Loss function
- H : Model class
OUTPUTS>
- Collection of models $\{ h_1, \cdots, h_T \}$



## Classification of the paper:
1) The paper is **Methodological**, **Theoretical** and **Empirical**.
2) The paper proposes a **Novel Theory Contribution** through a new way of achieving fairness in minimax terms.
# 2.d) Reference work:
- [22] - recently proposed the minimax group fairness in context of classification.
- [12, 31] - use a model for each group - kind of a minimax-solution


# Don't know the meaning.
1) Provably Convergent Oracle-Efficient learning algorithm.
2) Minimax-group-fairness *Pareto dominates* an equalized-error model with respect to group error rates
3) Pareto improvement.
4) In the context of game theory what is a zero-sum game between learner and regulator?
5) What are the theoretical guarantees of Exponential Weights Algorithm.
6) $\frac{1}{\sqrt{T}}$-Approximate Nash equilibrium - ref [15].
7) Lagrangian dual function of problem (2) - DONE
   Since the optimization problem is state as:
   $$\text{minimize  } \epsilon(h), \;\;\text{subject to } \epsilon_k(h) \leq \gamma,\;\; k = 1, \cdots, K$$
   Then we have that $F(\lambda, h) = \epsilon(h) + \sum_{k} \lambda_k \left[ \epsilon_k(h) - \gamma\right] \implies F(\lambda,h) = \sum_{k} (p_k + h_k) \epsilon_k - \lambda_k \gamma$
8) Assumption that Learner has WERM Oracle over class H - Whenever we have that objective function is convex.
9) Online Gradient Descent.
