*Link:* https://www.youtube.com/watch?v=E0Hmnixke2g

# Classical Machine Learning:

## Supervised Learning (Pre-Categorized Data):
We can call this methods *Task Driven* algorithms. 

### Regression:
Predict a continuous value from some features.
#### Linear Regression:
Determine a linear relation between input and output. We use Minimum-Squares into the optimization problem.

### Classification:
Assign a discrete categorical label based on features.
#### Logistic Regression:
Use the sigmoid function such that we can infere probabilities of a datapoint class.

### Non-parametric models:
#### KNN - K-nearest neighbors:
We don't use a pre-created function. It can be used both in **Classification** and **Regression** problem.
We define a $k$ such that the model is balanced between *Underfitting* and *Overfitting.*
Ways of estimating $k$ are **Cross-Validation**.

#### SVM - Support Vector Machines:
Can be used both for **Regression** and **Classification**. The hyperplane is used as *Decision-Boundary*. We select the hyperplane with greatest margin. *Support Vectors* are the points that sit close to the *Decision-Boundary* for each class.
Powerful into larger dimensions. We can define new *Kernel-Functions* such that the *Decision-Boundary* can be less linear.

#### Naive-Bayes Classifier:
Used in *Spam Classification* and *Other text based classification*.

#### Decision Trees:
Create leaf nodes that classify the current avaliated datapoint. Can be used into regression and classification
**Ensemble**: Combine weak trees into a more robust one.
	Bagging (majority vote): We can use Bootstrapping and Random Forests
	Boosting : Fixing the errors of previous models. We can use **Adaboost**, **Gradient boosting** and **XGBoost**.

### Neural Networks:
	Originated Deep Neural Networks.

## Unsupervised Learning (Unlabelled Data):
We can call this methods *Data Driven* algorithms. No truth fact about the data is known.
Some algorithms are to categorize types of e-mails in some kind of category or to estimate a closeness between different emails. 

#### Clustering:
Don't have any labels and want to find clusters of data.
**K-means clustering**.
**Hierarquical Clustering**.
**DBScan.**

#### Dimensionality Reduction:
Keep much information into a lower dimensional representation.
Most algorithms use some kind of covariance between features to remove redundant information. 

**PCA (Principal Component Analysis)**
