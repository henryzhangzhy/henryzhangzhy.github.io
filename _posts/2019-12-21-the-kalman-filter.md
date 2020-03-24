---
author: Henry
topic: Robotics
comments: true
hide: true
---

The Kalman Filter is famous for its application in space exploration. It is also one of the most beautiful results in optimal filter and estimation theory. This article is intended to summarize a few related sources and present the way I understand the Kalman Filter.


## 1 Introduction

### 1.1 General background

In robotics, we often care about some unknown states about a dynamic system, such as the position and velocity of a moving obstacle or the position and orientation of ourselves. We usually have sensors that provide measurements about the state, i.e. odometry counters, radar returns and camera images. We want to know what the state is based on the observations.

If we have no idea about the system dynamics, all we can do is to rely on the measurements. This makes the state estimation a standalone task for each observation. However, when some belief about the system dynamics is encooperated, we can make use of the relation of the measurements over time. The easiest case is when the system is static, we can estimation the state by the well known least squares method.

### 1.2 System Model

We assume that we have the motion model is linear in state and control. The process noise sequence $v(k)$ is white and gaussian $\mathcal{N}(0, V)$.

\begin{equation}
    x(k+1) = F(k)x(k) + G(k)u(k) + v(k).
\end{equation}

We also assume that we have the measurement model is linear in state. The measurement noise sequence $w(k)$ is white and gaussian $\mathcal{N}(0, W)$.

\begin{equation}
    z(k) = H(k)x(k) + w(k).
\end{equation}

Also, assume that the process noise and the measurement noise are uncorrelated, which leads to independent in the gaussian case. assume that the prior distribution is a know gaussian distribution. These conditions ensures that we are all dealing with gaussian distributions, which is fully described by its first and second moment and enables a convenient recursive formulation.

## 2 Background

### 2.1 least squares

### 2.2 Gaussian

#### 2.2.1 uncorrelated and independent

#### 2.2.2 passing gaussian through linear systems

#### 2.2.3 marginalization

#### 2.2.4 conjugate prior

### 2.3 Estimation theory

## 3 Gaussian derivation approach to the Kalman Filter

### 3.1 Passing through the linear system

Based on the system model decribed in 1.2, suppose that we have a prior about the state distribution in time k=0, then we received a measurement $z(k=1)$, what is the distribution of $x(k=1)$?

Well, since we assume that we know the motion model, even without the observation $z(1)$, we have some knowledge about where $x(1)$ is based on $x(0)$ and the motion model. This is just by passing the Gaussian prior through the linear system as what we described in 2.2.2. Since this is based on the prior, we denote this as $x(k=1\|k=0)$, or simply $x(1\|0)$, which means the conditional probability distribution of $x(k=1)$ given on $x(k=0)$.

\begin{equation}
    \bar{x}(1|0) = F\bar{x}(0),
\end{equation}

\begin{equation}
    \Sigma(1|0) = F\Sigma(0)F^T + V.
\end{equation}

### 3.2 Using observation

We have an estimate about the $x(1)$ based on $x(0)$, which is $x(1\|0)$. But passing through the linear system add up noise covariance to the state covariance. Since we have an observation available, how would that influence our belief about x(1)?
We can think about this as x(1) condition on z(1), with the prior $x(1\|0)$.
\begin{equation}
    p(x|z) = \frac{p(z|x)p(x)}{\int p(z|x)p(x)dx}.
\end{equation}


### 3.3 Is the two stage formulation reasonable?


