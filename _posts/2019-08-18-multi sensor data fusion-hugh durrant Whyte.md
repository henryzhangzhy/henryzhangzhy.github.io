---
author: Henry
topic: Autonomous Vehicles
comments: true
---

Notes on _Multi Sensor Data Fusion_ from Hugh Durrant Whyte.

This is a lecture note referenced in the paper that I talked about in the post [a multi-sensor fusion system for moving object detection and tracking in urban driving environments](https://zhyhenryzhang.github.io/2019/08/12/a-multi-sensor-fusion-system-for-moving-object-detection-and-tracking-in-urban-driving-environments.html). In this lecture note, the probability fundations and some methods of multi sensor fusion are discussed.

## 2 Probabilistic Data Fusion

### 2.1 Probabilistic Models

Introduced definition of probability density function and its property. Conditional Probability and total probability theorem were explained. Details goes my post about [probability notes](https://zhyhenryzhang.github.io/2019/08/15/probability-notes.html)

We use random variable $\mathbf{x}$ to represent the state that we want to estimate. use random variable $\mathbf{z}$ to represent the observation that we get.

### 2.2 Probabilistic Methods

#### 2.2.1 Bayes theorem

Bayes theorem offers the tool to directly combine observations and prior beliefs. 
\begin{equation}
P(\mathbf{x} \| \mathbf{z}) = \frac{P(\mathbf{z} \| \mathbf{x}) P(\mathbf{x})}{P(\mathbf{z})} .
\end{equation}

#### 2.2.2 Data Fusion using Bayes Theorem

For multi sensor fusion, we want to combine the information of multiple observations, thus we have
\begin{equation}
P(\mathbf{x} \| \mathbf{Z^n}) = \frac{P(\mathbf{Z^n} \| \mathbf{x}) P(\mathbf{x})}{P(\mathbf{Z^n})} .
\end{equation}

Since it is often the case that observations are only dependent on the internal state $\mathbf{x}$, or conditionally independent on $\mathbf{x}$. We have
\begin{equation}
P(\mathbf{x} \| \mathbf{Z^n}) = CP(\mathbf{x}) \sum_{i=1}^{n}P(\mathbf{z_i} \| \mathbf{x}).
\end{equation}

#### 2.2.3 Recursive Bayes Updating

Do we have to start from the initial prior all the time, multiplying all the probability of observations? We can actually do it recursively.

\begin{equation}
 P(\mathbf{x}\|\mathbf{Z^k}) = \frac{P(\mathbf{Z^k}\|\mathbf{x})P(\mathbf{x})}{P(\mathbf{Z^k})} 
\end{equation}
\begin{equation}
 = \frac{P(\mathbf{z_k}, \mathbf{Z^{k-1}}\|\mathbf{x})P(\mathbf{x})}{P(\mathbf{Z^k})} 
\end{equation} 
\begin{equation}
 = \frac{P(\mathbf{z_k} \| \mathbf{x})P(\mathbf{Z^{k-1}}\|\mathbf{x})P(\mathbf{x})}{P(\mathbf{Z^k})} 
\end{equation}
\begin{equation}
 = \frac{P(\mathbf{z_k} \| \mathbf{x})P(\mathbf{x}\|\mathbf{Z^{k-1}})P(\mathbf{Z^{k-1}})}{P(\mathbf{Z^k})} 
\end{equation}
\begin{equation}
 = \frac{P(\mathbf{z_k} \| \mathbf{x})P(\mathbf{x}\|\mathbf{Z^{k-1}})}{P(\mathbf{z_k}\|\mathbf{Z^{k-1}})}.  
\end{equation}

#### 2.2.4 Data Dependency and Bayes Networks

Short Introduction to be belief networks.

#### 2.2.5 Distributed Data Fusion with Bayes Theorem

Distributed means raw data is processed in the sensor module. This has the advantage that each sensor is __'modular'__ and talks in a common __'state'__ language. However, it has the disadvantage that a complete likelihood, rather than a single observation, must be communicated.

#### 2.2.6 Data Fusion with Log-Likelihoods

If we take log of the Beyes Theorem, it becomes 
\begin{equation}
 \mathbf{l}(\mathbf{x} \| \mathbf{z}) = \mathbf{l}(\mathbf{z} \| \mathbf{x}) + \mathbf{l}(\mathbf{x}) - \mathbf{l}(\mathbf{z}). 
\end{equation}

This simplifies the calculation.

### 2.3 Information Measures

Information is a measure of the compactness of a distribution. The shannon information (or entropy) and the Fisher information are two probabilistic measures of information of particular value in data fusion problems.

#### 2.3.1 Entropic Information

\begin{equation}
H_P(\mathbf{x}) \triangleq - \mathop{\mathbb{E}} \lbrace \log P(\mathbf{x})\rbrace = - \int_{-\infty}^{\infty}P(\mathbf{x}) \mathrm{d}\mathbf{x}. 
\end{equation}

Note that $H_P(\cdot)$ is not strictly a function of $\mathbf{x}$ but is rather a function of the distribution $P(\cdot)$.

#### 2.3.2 Conditional Entropy

\begin{equation}
H_P(\mathbf{x} \| z_j) \triangleq - \mathop{\mathbb{E}} \lbrace \log P(\mathbf{x} \| z_j) \rbrace = - \int_{-\infty}^{\infty}P(\mathbf{x} \| z_j) \mathrm{d}\mathbf{x}. 
\end{equation}

\begin{equation}
 \bar{H}(\mathbf{x} \| \mathbf{z}) \triangleq - \mathop{\mathbb{E}} \lbrace H(\mathbf{x} \| \mathbf{z}) \rbrace = - \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} P(\mathbf{x}, \mathbf{z}) \log P(\mathbf{x} \| \mathbf{z}) \mathrm{d} \mathbf{x} \mathrm{d}\mathbf{z}. 
\end{equation}

It shows the entropy of an n dimensional Gaussian Distribution is
\begin{equation}
  \- \frac{1}{2} \log \lbrack (2 \pi e)^n \| \mathbf{P} \| \rbrack. 
\end{equation}

The entropy is proportional to the log of the determinant of the covariance. The determinant of a matrix is a volume measure (recall that the determinant is the product of the eigenvalues of a matrix and the eigenvalues define axis lengths in n space).

#### 2.3.3 Mutual Information

\begin{equation}
 I(\mathbf{x}, \mathbf{z}) \triangleq - \mathop{\mathbb{E}} \lbrace \log \frac{P(\mathbf{x}, \mathbf{z})}{P(\mathbf{x}) P(\mathbf{z})} \rbrace. 
\end{equation}

\begin{equation}
 I(\mathbf{x}, \mathbf{z}) = H(\mathbf{x}) + H(\mathbf{z}) - H(\mathbf{x}, \mathbf{z}). 
\end{equation}

The process of predicting information gain, making a decision on sensing action, then sensing, is an efficient and effective way of managing sensing resources and of determining optimal sensing policies.

#### 2.3.4 Fisher Information

The Fisher information $J(\mathbf{x})$ is defined as the second derivative of the log-likelihood
\begin{equation} J(\mathbf{x}) \triangleq \frac{\mathrm{d^2}}{\mathrm{d}\mathbf{x^2}} \log P(\mathbf{x}). 
\end{equation}

Generally in a matrix form while cross entropy is a scaler.

### 2.4 Alternatives to Probability

Interval Calculus, Fuzzy logic and Evidential Reasoning is introduced shortly.

## 3 Multi-Sensor Estimation

### 3.1 The Kalman Filter

### 3.2 The Multi-Sensor Kalman Filter

### 3.3 Non-linear Data Fusion Methods

### 3.4 Multi-Sensor Data Association

## Others

Section 4 metions about distributed sensor fusion and 5 metions about decision make, which are not of interest here.