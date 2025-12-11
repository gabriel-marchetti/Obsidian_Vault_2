---
tags:
  - machine-learning
  - supervised-learning
---
# Table of Contents:


---
A linear model take the form:
$$
\begin{align}
\hat{y} (w,x) &= w_0 + w_1 \cdot x_1 + \cdots + w_p \cdot x_p  \\
              &= w_0 + \mathbf{w}^T \cdot \mathbf{x} \\
              &= \mathbf{w}^T \cdot \mathbf{x} 
\end{align}
$$
where $\mathbf{w} = (w_0, w_1, w_2, \cdots, w_p)^T$ and $\mathbf{x} = (1, x_1, x_2, \cdots, x_p)^T$

## Ordinary Least Squares:
The problem statement of Ordinary Least Squares is:
$$
\min_{w} ||X\mathbf{w} - \mathbf{y}||_{2}^{2}
$$
