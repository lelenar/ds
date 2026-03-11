
## 参考资料

- Greg Durrett, 2021-2024, "CS388 Natural Language Processing course materials", retrieved from https://www.cs.utexas.edu/~gdurrett/courses/online-course/materials.html

- Philipp Krähenbühl, 2020-2024, "AI394T Deep Learning course materials", retrieved from https://www.philkr.net/dl_class/material and https://ut.philkr.net/deeplearning/

- Philipp Krähenbühl, 2025, "AI395T Advances in Deep Learning course materials", retrieved from https://ut.philkr.net/advances_in_deeplearning/


- François Fleuret, The Little Book of Deep Learning, [-PDF-](https://fleuret.org/public/lbdl.pdf)
  - 梯度下降部分介绍的很好


## ANN 

- CS229 Lecture Notes, 2023, Stanford University, [7.2 Neural networks](https://cs229.stanford.edu/main_notes.pdf#page=81.24)
  - 写得非常清楚


## 简单 ANN

### 激活函数

> Smets, B. M. N. (2024). Mathematics of Neural Networks (Lecture Notes Graduate Course) (Version 1). arXiv. [Link](https://doi.org/10.48550/arXiv.2403.04807) (rep), [PDF](https://arxiv.org/pdf/2403.04807.pdf), [Google](<https://scholar.google.com/scholar?q=Mathematics of Neural Networks (Lecture Notes Graduate Course) (Version 1)>). 


We list some commonly used scalar activation functions which are also illustrated in Figure 1.2.

![20250910151737](https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/20250910151737.png)

![20250910151811](https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/20250910151811.png)

> Figure 1.2.

- Rectified Linear Unit (ReLU): arguably the most used activation function in modern neural networks, it is calculated as

$$
\sigma(\lambda)=\operatorname{ReLU}(\lambda):=\max \{0, \lambda\} .
$$

- Sigmoid (also known as logistic sigmoid or soft-step):

$$
\sigma(\lambda):=\frac{1}{1+e^{-\lambda}} .
$$


The sigmoid was commonly used as activation function in early neural networks, which is the reason that activations functions in general are still often labeled with a $\sigma$.
- Hyperbolic tangent: very similar to the sigmoid, it is given by

$$
\tanh (\lambda):=\frac{e^\lambda-e^{-\lambda}}{e^\lambda+e^{-\lambda}} .
$$

- Swish: a more recent choice of activation function that can be thought of as a smooth variant of the ReLU. It is given by the multiplication of the input itself with the sigmoid function:

$$
\operatorname{swish}_\beta(\lambda):=\lambda \sigma(\beta \lambda):=\frac{\lambda}{1+e^{-\beta \lambda}},
$$

where $\beta>0$. The $\beta$ parameter is usually chosen to be 1 but could be treated as a trainable parameter if desired. In case of $\beta=1$, this function is also called the sigmoid-weighted linear unit or SiLU.

### 多变量激活函数

Activation functions need not be scalar, we list some common multivariate functions.
- Softmax, also known as the normalized exponential function: softmax : $\mathbb{R}^n \rightarrow[0,1]^n$ is given by

$$
\operatorname{softmax}\left(\left[\begin{array}{c}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{array}\right]\right):=\frac{1}{\sum_{i=1}^n e^{x_i}}\left[\begin{array}{c}
e^{x_1} \\
e^{x_2} \\
\vdots \\
e^{x_n}
\end{array}\right]
$$


Softmax has the useful property that its output is a discrete probability distribution, i.e. each value is a non-negative real in the range [ 0,1 ], and all the values in its output add up to exactly 1 .
- Maxpool: here each output is the maximum of a certain subset of the inputs: the function $\operatorname{maxpool}: \mathbb{R}^n \rightarrow \mathbb{R}^m$ is given by

$$
\text { maxpool }\left(\left[\begin{array}{c}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{array}\right]\right):=\left[\begin{array}{cc}
\max _{j \in I_1} & x_j \\
\max _{j \in I_2} & x_j \\
\vdots & \\
\max _{j \in I_m} & x_j
\end{array}\right] .
$$


Where for each $i \in\{1, \ldots, m\}$ we have a $I_i \subset\{1, \ldots, n\}$ that specifies over which inputs to take the maximum for each output. Maxpooling can easily be generalised by replacing the max operation with $\min$, the average, the mean, etc.

- Normalization, sometimes it is desirable to re-center and re-scale a signal:

$$
\text { normalize }\left(\left[\begin{array}{c}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{array}\right]\right):=\left[\begin{array}{c}
\frac{x_1-\mu}{\sigma} \\
\frac{x_2-\mu}{\sigma} \\
\vdots \\
\frac{x_n-\mu}{\sigma}
\end{array}\right] \text {, }
$$

where $\mu=\mathbb{E}[x]$ and $\sigma^2=\operatorname{Var}(x)$. There are many variants on normalization where the difference is how $\mu$ and $\sigma$ are computed: over time, over subsets of the incoming signals, etc.

All the previous examples of activation functions are deterministic, but stochastic activation functions are also used.

- Dropout is a stochastic function that is often used during the training process but is removed once the training is finished. It works by randomly setting individual values of a signal to zero with probability $p$ :

$$
\left(\operatorname{dropout}_p(x)\right)_i:= \begin{cases}0 & \text { with probability } p \\ x_i & \text { with probability } 1-p\end{cases}
$$

- Heatbath is a scalar function that outputs 1 or -1 with a probability that depends on the input:

$$
\text { heatbath }(\lambda):=\left\{\begin{aligned}
1 & \text { with probability } \frac{1}{1+e^{-\lambda}} \\
-1 & \text { otherwise. }
\end{aligned}\right.
$$


All the activation functions we seen are essentially fixed functions, swish and dropout have a parameter but it is usually fixed to some chosen value. That means that the trainable parameters of a neural network are usually the linear weights and biases. There is however no a-priori reason why that needs to be the case, in fact we will see a class of non-linear operators with trainable parameters at the end of Chapter 3. Regardless, having parameters in the non-linear part of a network is somewhat rare in practice at the time of this writing.


## Gradient Desent




![20250910171507](https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/20250910171507.png)

> <https://www.cs.cmu.edu/~ggordon/MCMC/ggordon.MCMC-tutorial.pdf>

- https://www.cs.cornell.edu/courses/cs4780/2022sp/notes/LectureNotes11.html


![20250910172841](https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/20250910172841.png)
> https://bayen.berkeley.edu/sites/default/files/lecture101.pdf

#### 重点参考

- Ryan Tibshirani Scribes: Cong Lu/Yu Zhao, 2012, [Lecture 5: Gradient Desent Revisited](https://www.cs.cmu.edu/~ggordon/10725-F12/scribes/10725_Lecture5.pdf)


- Ryan Tibshirani Scribes: Cong Lu/Yu Zhao, 2012, [Lecture 2: Optimization](https://www.cs.cmu.edu/~ggordon/10725-F12/scribes/10725_Lecture2.pdf)
Gradient descent is the grandfather of first order methods. It simply starts at an initial point and then repeatedly takes a step opposite to the gradient direction of the function at the current point. The gradient descent algorithm to minimize a function $f(x)$ is as follows:

$
\begin{aligned}
& \text { for } k=0,1,2, \ldots \text { do } \\
& \qquad g_k \leftarrow \nabla f\left(x_k\right) \\
& \quad x_{k+1} \leftarrow x_k-t_k g_k \\
& \text { end for }
\end{aligned}
$


### 随机梯度下降

> <https://ubc-mds.github.io/DSCI_572_sup-learn-2/lectures/03_sgd-intro-to-nn.html>

- But if we have large $n$ and/or $\mathbf{w}$, gradient descent becomes very computationally expensive (when we get to deep learning, we'll have models where the number of weights to optimize is in the millions)
- Say $\mathrm{n}=1,000,000$, we have 1000 parameters to optimize, and we do 1000 iterations $=O\left(10^{12}\right)$ computations
- For each data point, we need to compute gradients with respect to each of model parameter.
- For each iteration, it'll have to compute $10^6 \times 10^3=10^9$ gradients
- We can reduce this workload by using just a fraction of our dataset to update our parameters each iteration (rather than using the whole data set)
- This is called stochastic gradient descent [1]


## Python codes

- [financial-data-science-notebooks](https://github.com/lianxhcn/financial-data-science-notebooks/tree/main) / [6.3\_deep\_learning.ipynb](https://github.com/lianxhcn/financial-data-science-notebooks/blob/main/6.3_deep_learning.ipynb)
