---
author: Henry
topic: Robotics
comments: true
---

I certainly don't know Uncertainty.

This is the first post about the [knowledge upper bound](https://henryzhangzhy.github.io/2019/08/15/knowledge-upper-bound.html) series, as notes about probability.

0. random variable.
1. probability density function (pdf) $P_y(\cdot)$ is defined on a random variable $\mathbf{y}$.
   A pdf $P(y)$ is considered valid if:
   1. It is positive: $P(\mathbf{y}) > 0$ for all $\mathbf{y}$, and
   2. It sums (integrates) to a total probability of 1: 
   \begin{equation}
     \int_y P(\mathbf{y}) \mathrm{d}y=1.
   \end{equation}
2. Joint and marginal probability
   1. Joint distribution $P_{xy}(\mathbf{x}, \mathbf{y})$ is defined in a similar manner.
   2. Marginal pdf $P_y(\mathbf{y})$ is defined as integrate over $\mathbf{x}$ on $P_{xy}(\mathbf{x}, \mathbf{y})$:
   \begin{equation}
     P_y(\mathbf{y}) \triangleq \int_x P_{xy}(\mathbf{x}, \mathbf{y}) \mathrm{d}x.
   \end{equation}
3. Conditional Probability
   1. Conditional pdf $P_{x\|y}(\mathbf{x} \| \mathbf{y})$ is defined by 
   \begin{equation}
     P_{x\|y}(\mathbf{x} \| \mathbf{y}) \triangleq \frac{P_{xy}(\mathbf{x}, \mathbf{y})}{P_y(\mathbf{y})}. 
   \end{equation}
   2. chain rule
      \begin{equation}
        P(\mathbf{x_1}, \cdots, \mathbf{x_n}) = P(\mathbf{x_1} \| \mathbf{x_2}, \cdots, \mathbf{x_n}) \cdots P(\mathbf{x_{n-1}} \| \mathbf{x_n}) P(\mathbf{x_n}), 
      \end{equation}
      where order doesn't matter.
   3. $\mathbf{x}$ and $\mathbf{y}$ are said to be independent as 
      \begin{equation}
        P_{x\|y}(\mathbf{x} \| \mathbf{y}) = P_{x}(\mathbf{x}). 
      \end{equation}
   4. conditional independence: $\mathbf{x}$ and $\mathbf{y}$ are conditional independent if $\mathbf{z}$ is know 
   \begin{equation}
     P(\mathbf{x} \| \mathbf{y},\mathbf{z}) = P(\mathbf{x} \| \mathbf{z}). 
   \end{equation}
   5. Bayes theorem 
   \begin{equation}
     P(\mathbf{x} \| \mathbf{z}) = \frac{P(\mathbf{z} \| \mathbf{x}) P(\mathbf{x})}{P(\mathbf{z})} .
   \end{equation}
      - We interprete $P(\mathbf{x})$ as prior, $P(\mathbf{z} \| \mathbf{x})$ as likelihood of the observation. $P(\mathbf{z})$ as a normalization factor, and $P(\mathbf{x} \| \mathbf{z})$ as the posterior distribution.
      - Bayes theorem provides a direct method to combine prior beliefs and observed information about the world. Another interpretation would consider it as reverse the conditional probability of cause and effect, make inference easier.