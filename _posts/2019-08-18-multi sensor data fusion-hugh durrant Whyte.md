---
author: Henry
topic: Autonomous Vehicles
comments: true
---

Notes on _Multi Sensor Data Fusion_ from Hugh Durrant Whyte.

This is a lecture note referenced in the paper that I talked about in the post [a multi-sensor fusion system for moving object detection and tracking in urban driving environments](https://zhyhenryzhang.github.io/2019/08/12/a-multi-sensor-fusion-system-for-moving-object-detection-and-tracking-in-urban-driving-environments.html). In this lecture note, the probability foundations and some methods of multi sensor fusion are discussed.

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

With certain assuptions about the observation and process models, the resulting estimate $\dot{\mathbf{x}}(t)$ minimises mean-squared error
\begin{equation}
  L(t) = \int_{-\infty}^{\infty} (\mathbf{x}(t) - \hat{\mathbf{x}}(t))^T (\mathbf{x}(t) - \hat{\mathbf{x}}(t)) P(\mathbf{x}(t) \| \mathbf{Z}^t) \mathrm{d} \mathbf{x}.
\end{equation}

Differentiation of the above equation with respect to $\mathbf{x}(t)$ and setting equal to zero gives
\begin{equation}
  \hat{\mathbf{x}}(t) = \int_{-\infty}^{\infty} \mathbf{x}(t) P(\mathbf{x}(t) \| \mathbf{Z}^t) \mathrm{d} \mathbf{x}.
\end{equation}

which is simply the conditional mean $ \hat{\mathbf{x}}(t) = \mathop{\mathbb{E}}(\mathbf{x}(t) \| \mathbf{Z}^t).$

The Kalman Filter, and indeed any mean-squared-error estimator, computes an estimate which is the conditional mean; an average, rather than a most likely value. (Q: what is the most likely value ?)

#### 3.1.1 State and Sensor Models

This section defineds the notations for Kalman Filter. And shows how the model is discretized.

The author claimed that it is always best to start with a continuous-time model for the state and then construct a discrete model, rather than stating the discrete model at the outset. This allows for correct identification of noise transfers and noise correlations. ??

#### 3.1.2 The Kalman Filter Algorithm

Prediction Step:
\begin{equation}
  \hat{\mathbf{x}}(k \| k-1) = \mathbf{F}(k) \hat{\mathbf{x}}(k-1 \| k-1) + \mathbf{B}(k) \mathbf{u}(k)
\end{equation}
\begin{equation}
  \mathbf{P}(k \| k-1) = \mathbf{F}(k) \mathbf{P}(k-1 \| k-1) \mathbf{F}^T(k) + \mathbf{G}(k) \mathbf{Q}(k) \mathbf{G}^T(k)
\end{equation}

Update Step:
\begin{equation}
  v(k) = \mathbf{z}(k) - \mathbf{H}(k) \hat{\mathbf{x}}(k \| k-1)
\end{equation}
\begin{equation}
  \mathbf{S}(k) = \mathbf{R}(k) + \mathbf{H}(k) \mathbf{P}(k \| k-1) \mathbf{H}^T(k)
\end{equation}
\begin{equation}
  \hat{\mathbf{x}}(k \| k) = \hat{\mathbf{x}}(k \| k-1) - \mathbf{W}(k) v(k)
\end{equation}
\begin{equation}
  \mathbf{P}(k \| k) = \mathbf{P}(k \| k-1) - \mathbf{W}(k) \mathbf{S}(k) \mathbf{W}^T(k)
\end{equation}
\begin{equation}
  \mathbf{W}(k) = \mathbf{P}(k \| k-1) \mathbf{H}(k) \mathbf{S}^{-1}(k)
\end{equation}

#### 3.1.3 The Innovation

Because the 'true' states are not usually available for comparison with the estimated states, the innovation is often the only measure of how well the estimator is performing. The most important property of innovation is that they form an orthogonal uncorrelated, white sequence,
\begin{equation}
  \mathop{\mathbb{E}} \lbrace v(k) \| \mathbf{Z}^{k-1} \rbrace = 0, \mathop{\mathbb{E}} \lbrace v(i)v^T(jj) \rbrace = \mathbf{S}(i) \delta_{ij}. 
\end{equation}

This can be exploited in monitoring filter performance.

#### 3.1.4 Understanding the Kalman Filter

There are three different, but related ways of thinking about the Kalman filter algorithm

1. __Weighted average__

Clearly, this interpretation of the Kalman filter holds only for those states which can be written as a linear combination of the observation vector.

2. __Conditional mean__

3. __Orthogonal decomposition__

#### 3.1.5 Steady State Filter

Using the fact that if filtering is synchronous, and state and observation matrics time-invariant, the filter variance will converge quickly, thus $\mathbf{W}$ matrix is also converged, we can skip the computation and use paramatric model to estimate it, reduce the computation greatly. 

#### 3.1.6 Asynchronous, Delayed and Asequent observations

Asynchronous means observations from different sensors don't come at the same time, but without delay. Can be addressed by taking time into account, make a prediction at observing time.
Delayed means some observations is received by the filter with some delay after it is observed. Can be addressed by dropping the current prediction and make a prediction of the observing time of that sensor.
Asequent means delay from different sensor cause the order of receiving is different from the the order of observations. It cannot be addressed easily unless you keep some observations and recompute the estimation. The author claim this can possibly be solved by a __inverse-covariance filter ??__.

#### 3.1.7 The Extended Kalman Filter

Linearization at the estimation point.

A few comments from the author:

1. Jacobians needs to be recomputed every time.
2. The model is based on lieanrization at the estimated trajectory, thus if the estimation is not accurate, the second or higher order term cannot be ignored and make it useless. This also requires that initialization should be careful.

### 3.2 The Multi-Sensor Kalman Filter

#### 3.2.1 Observation Models

#### 3.2.2 The Group-Sensor Method

It basiclly stacks all the observations and observation models, treating them as one sensor. The Kalman Filter can be directly applied. The problems is that sensors are assumed to be synchronous and computational complexity of matrix inversion is $\mathbf{O}(n^3)$ as the number of sensors increases.

#### 3.2.3 The Sequential-Sensor Method

Treat each observation and observation model independently, make a prediction and update each observation is made. The requires too much predicitons and updates when sensor number increases, though it is linear of the number of sensors. CMU paper [a multi-sensor fusion system for moving object detection and tracking in urban driving environments](https://zhyhenryzhang.github.io/2019/08/12/a-multi-sensor-fusion-system-for-moving-object-detection-and-tracking-in-urban-driving-environments.html) applied this method.

#### 3.2.4 The Inverse-Covariance Form

This is essentially a information filter, the good side is it simplifies the update step, while the only inversion would be the $P$ matrix, only of the size of states and not related to the number of sensors.

#### 3.2.5 Track-to-Track Fusion

Sensor will do filtering locally and pass the posterior to the center, the center will fuse them together. Method can be covariance-weighted Average.

### 3.3 Non-linear Data Fusion Methods

Bayes filter is mentioned. Listed particle-filter and the sum-of-gaussians (gaussian mixture) method.

### 3.4 Multi-Sensor Data Association

The idea is to use the nomalized innovation distance.

#### 3.4.1 The Nearest-Neighbour Standard Filter

Match the closest one, not suitable for highly clustered detections.

#### 3.4.2 The Probabilistic Data Association Filter

Keep a mixture of all the observations within a certain range of the prediction to form a combined state and do the prediction again.

The good thing is you are never wrong, but you are never right as well.

#### 3.4.3 The Multiple Hypothesis Tracking (MHT) Filter

Keep a hypothesis for all observations within certain range. Compute the likelihood and drop protential not good trackings.

#### 3.4.4 Data Association in Track-to-Track Fusion

Weighted average.

#### 3.4.5 Maintaining and Managing Track Files

Refer to other literature.

## Others

Section 4 metions about distributed sensor fusion and 5 metions about decision make, which are not of interest here.


# Questions
1. How do we discretize the kalman filter?
2. How is $\mathbf{HPH}^T$ a projection?
3. How is the gain being computed?
4. What are the three interpretation?
5. How to use information filter to solve asequent data?
6. How to use information filter to solve multi sensor problems?
7. How is the steady state filter parameter being choosed?
8. What are the difference of the association methods?
9. Why $ \mathbf{GQG}^T$ in kalman filter prediction?
