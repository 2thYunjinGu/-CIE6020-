# Chapter 4 Notes on Information Theory  
# 第 4 章 信息论笔记

---

# Chapter 4 Mutual Information  
# 第 4 章 互信息

## 4.1 Basics  
## 4.1 基础内容

### Definition: Mutual Information  
### 定义：互信息

For a pair of random variables $(X,Y)$ with joint distribution $p(x,y)$, the **mutual information** between $X$ and $Y$ is defined as

对于一对随机变量 $(X,Y)$，若其联合分布为 $p(x,y)$，则 $X$ 与 $Y$ 的**互信息**定义为

$$
I(X;Y)=H(X)-H(X \mid Y)
$$

It can also be written as

它也可以写成

$$
I(X;Y)=\sum_{x,y} p(x,y)\log \frac{p(x,y)}{p(x)p(y)}
$$

This quantity measures how much uncertainty about $X$ is reduced after observing $Y$.

这个量衡量的是：在观察到 $Y$ 之后，关于 $X$ 的不确定性减少了多少。

---

### Equivalent Forms  
### 等价形式

We also have

我们还有

$$
I(X;Y)=H(Y)-H(Y \mid X)
$$

and

以及

$$
I(X;Y)=H(X)+H(Y)-H(X,Y)
$$

So mutual information is symmetric:

因此互信息是对称的：

$$
I(X;Y)=I(Y;X)
$$

### Interpretation  
### 直观理解

- $H(X)$ is the uncertainty of $X$ before observing $Y$  
  $H(X)$ 是观测 $Y$ 之前 $X$ 的不确定性
- $H(X \mid Y)$ is the remaining uncertainty of $X$ after observing $Y$  
  $H(X \mid Y)$ 是观测 $Y$ 之后 $X$ 剩余的不确定性
- Therefore, $I(X;Y)$ is the amount of information that $Y$ provides about $X$  
  因此，$I(X;Y)$ 就是 $Y$ 向我们提供的关于 $X$ 的信息量

---

### Theorem 1  
### 定理 1

For any random variables $X$ and $Y$,

对任意随机变量 $X$ 和 $Y$，都有

$$
I(X;Y)\ge 0
$$

### Proof  
### 证明

Since

因为

$$
I(X;Y)=H(Y)-H(Y \mid X)
$$

and conditioning cannot increase entropy, we have

而条件化不会增加熵，所以有

$$
H(Y)\ge H(Y \mid X)
$$

Hence

因此

$$
I(X;Y)\ge 0
$$

This is sometimes summarized as: **information never hurts**.

这有时也概括为：**信息不会带来坏处**。

---

### Theorem 2  
### 定理 2

If $X$ and $Y$ are independent, then

如果 $X$ 和 $Y$ 相互独立，那么

$$
I(X;Y)=0
$$

### Proof  
### 证明

If $X$ and $Y$ are independent, then knowing $X$ gives no information about $Y$, so

如果 $X$ 和 $Y$ 独立，那么知道 $X$ 不会帮助我们了解 $Y$，所以

$$
H(Y \mid X)=H(Y)
$$

Thus

因此

$$
I(X;Y)=H(Y)-H(Y \mid X)=0
$$

---

### Theorem 3  
### 定理 3

If $X$ and $Y$ are identical, then

如果 $X$ 和 $Y$ 完全相同，那么

$$
I(X;Y)=H(X)
$$

### Proof  
### 证明

If $Y=X$, then

如果 $Y=X$，则

$$
I(X;X)=H(X)-H(X \mid X)
$$

But once $X$ is known, there is no uncertainty left about $X$, so

但在已知 $X$ 的条件下，关于 $X$ 已经没有任何不确定性，因此

$$
H(X \mid X)=0
$$

Hence

所以

$$
I(X;X)=H(X)
$$

---

### Venn Diagram Interpretation  
### 韦恩图式理解

A common picture is:

一个常见的图示理解是：

- $H(X)$ is the total uncertainty of $X$  
  $H(X)$ 是 $X$ 的总不确定性
- $H(Y)$ is the total uncertainty of $Y$  
  $H(Y)$ 是 $Y$ 的总不确定性
- the overlap between them is $I(X;Y)$  
  两者重叠的部分就是 $I(X;Y)$
- the non-overlapping parts are $H(X \mid Y)$ and $H(Y \mid X)$  
  不重叠的部分分别是 $H(X \mid Y)$ 和 $H(Y \mid X)$
- the union corresponds to $H(X,Y)$  
  并集对应 $H(X,Y)$

So we can think of

因此我们可以把它理解为

$$
H(X,Y)=H(X \mid Y)+I(X;Y)+H(Y \mid X)
$$

---

### Channel Interpretation  
### 信道视角的理解

Suppose $X$ is transmitted through a channel and produces output $Y$.

设 $X$ 经过信道传输后产生输出 $Y$。

Before observing $Y$, the uncertainty in $X$ is

在观察 $Y$ 之前，$X$ 的不确定性是

$$
H(X)
$$

After observing $Y$, the uncertainty in $X$ becomes

在观察 $Y$ 之后，$X$ 的不确定性变成

$$
H(X \mid Y)
$$

Thus the knowledge gained from $Y$ is

因此，从 $Y$ 中获得的知识量就是

$$
I(X;Y)
$$

---

### Channel Capacity  
### 信道容量

The **channel capacity** is the maximum mutual information over all possible input distributions.

**信道容量**就是在所有可能输入分布中，互信息所能达到的最大值。

$$
C=\max I(X;Y)
$$

So channel capacity tells us the maximum amount of information that can be reliably conveyed through the channel.

因此，信道容量告诉我们：这个信道每次使用最多能可靠传递多少信息。

---

## 4.2 KL Divergence  
## 4.2 KL 散度

### Definition: KL Divergence  
### 定义：KL 散度

For two distributions $p(x)$ and $q(x)$, their **Kullback-Leibler divergence** is defined as

对于两个分布 $p(x)$ 和 $q(x)$，它们的 **Kullback-Leibler 散度** 定义为

$$
D(p \| q)=\sum_x p(x)\log \frac{p(x)}{q(x)}
$$

It can also be written as

它也可以写成

$$
D(p \| q)=\mathbb{E}_{X \sim p}\left[\log \frac{p(X)}{q(X)}\right]
$$

KL divergence measures how different $q$ is from $p$ when the true distribution is $p$.

KL 散度衡量的是：当真实分布是 $p$ 时，用 $q$ 来近似它究竟有多不一样。

---

### Theorem  
### 定理

For any two distributions $p$ and $q$,

对于任意两个分布 $p$ 和 $q$，都有

$$
D(p \| q)\ge 0
$$

### Proof  
### 证明

We have

我们有

$$
D(p \| q)=\mathbb{E}\left[\log \frac{p(X)}{q(X)}\right]=\mathbb{E}\left[-\log \frac{q(X)}{p(X)}\right]
$$

Since $-\log a$ is a convex function, Jensen's inequality gives

由于 $-\log a$ 是凸函数，由 Jensen 不等式可得

$$
D(p \| q)\ge -\log \mathbb{E}\left[\frac{q(X)}{p(X)}\right]
$$

Now

而

$$
\mathbb{E}\left[\frac{q(X)}{p(X)}\right]=\sum_x p(x)\frac{q(x)}{p(x)}=\sum_x q(x)=1
$$

Hence

因此

$$
D(p \| q)\ge -\log 1=0
$$

---

### Equality Condition  
### 取等条件

Since $-\log a$ is strictly convex, equality holds if and only if

由于 $-\log a$ 是严格凸函数，等号成立当且仅当

$$
p=q
$$

So

因此

$$
D(p \| q)=0 \iff p=q
$$

---

### Important Note  
### 重要说明

KL divergence behaves like a kind of distance, but it is **not** a true metric.

KL 散度有点像一种“距离”，但它**不是**真正的距离度量。

In particular,

特别地，

$$
D(p \| q)\ne D(q \| p)
$$

So KL divergence is not symmetric.

因此 KL 散度不是对称的。

---

### Mutual Information as KL Divergence  
### 互信息可以写成 KL 散度

We have

我们有

$$
I(X;Y)=\mathbb{E}_{(X,Y)\sim p(x,y)}\left[\log \frac{p(X,Y)}{p(X)p(Y)}\right]
$$

Therefore,

因此

$$
I(X;Y)=D\bigl(p(x,y)\,\|\,p(x)p(y)\bigr)
$$

This shows that mutual information measures how far the joint distribution is from the product of marginals.

这说明：互信息衡量的是联合分布 $p(x,y)$ 与边缘分布乘积 $p(x)p(y)$ 的差异有多大。

If $X$ and $Y$ are independent, then

如果 $X$ 和 $Y$ 独立，那么

$$
p(x,y)=p(x)p(y)
$$

and hence

于是

$$
I(X;Y)=0
$$

---

### Definition: Cross Entropy  
### 定义：交叉熵

The **cross entropy** between $p$ and $q$ is

分布 $p$ 与 $q$ 之间的**交叉熵**定义为

$$
CE(p,q)=\sum_x p(x)\log \frac{1}{q(x)}
$$

---

### Special Case  
### 特殊情形

If the two distributions are the same, then

如果这两个分布相同，那么

$$
CE(p,p)=H(X)
$$

because

因为

$$
CE(p,p)=\sum_x p(x)\log \frac{1}{p(x)}=H(X)
$$

---

### Theorem: Relation among Cross Entropy, Entropy, and KL  
### 定理：交叉熵、熵与 KL 散度的关系

If $X \sim p(x)$, then

如果 $X \sim p(x)$，那么

$$
CE(p,q)-H(X)=D(p \| q)
$$

Equivalently,

等价地，

$$
CE(p,q)=H(X)+D(p \| q)
$$

### Proof  
### 证明

We compute

直接计算可得

$$
CE(p,q)-H(X)=\sum_x p(x)\log \frac{1}{q(x)}-\sum_x p(x)\log \frac{1}{p(x)}
$$

So

因此

$$
CE(p,q)-H(X)=\sum_x p(x)\log \frac{p(x)}{q(x)}=D(p \| q)
$$

---

### Interpretation  
### 直观解释

Suppose the true distribution of $X$ is $p(x)$, but we mistakenly believe it is $q(x)$ and design a code according to $q(x)$.

假设 $X$ 的真实分布是 $p(x)$，但我们错误地认为它是 $q(x)$，并按照 $q(x)$ 来设计编码。

Then:

这时：

- $H(X)$ is the number of bits needed when the code is designed using the correct distribution $p(x)$  
  $H(X)$ 是按照真实分布 $p(x)$ 设计编码时所需的平均 bit 数

- $CE(p,q)$ is the number of bits needed when we use the wrong code designed from $q(x)$  
  $CE(p,q)$ 是按照错误分布 $q(x)$ 设计编码时所需的平均 bit 数

- $D(p \| q)$ is the extra number of bits caused by using the wrong code  
  $D(p \| q)$ 就是由于使用错误编码而多出来的 bit 数

When $q(x)=p(x)$, the code is correct and

当 $q(x)=p(x)$ 时，编码是正确的，并且

$$
D(p \| q)=0
$$

---

### Cross Entropy in Machine Learning  
### 机器学习中的交叉熵

Cross entropy is often used as a loss function in machine learning.

交叉熵常常被用作机器学习中的损失函数。

For example, in classification:

例如在分类任务中：

- the model outputs a predicted distribution $q(x)$  
  模型输出一个预测分布 $q(x)$
- the ground-truth label corresponds to the target distribution $p(x)$  
  真实标签对应目标分布 $p(x)$

Since

由于

$$
CE(p,q)=H(X)+D(p \| q)
$$

and $H(X)$ is fixed with respect to the model, minimizing cross entropy is equivalent to minimizing KL divergence.

而其中 $H(X)$ 对模型来说是固定项，所以最小化交叉熵等价于最小化 KL 散度。

---

## 4.3 Hypothesis Testing  
## 4.3 假设检验

Let

设

$$
X_1,X_2,\dots,X_n
$$

be i.i.d. random variables.

是独立同分布随机变量。

Suppose we are not sure whether their true distribution is $p(x)$ or $q(x)$.

假设我们不确定它们的真实分布究竟是 $p(x)$ 还是 $q(x)$。

We consider two hypotheses:

我们考虑两个假设：

$$
H_1: X_i \sim p(x)
$$

$$
H_2: X_i \sim q(x)
$$

---

### Goal  
### 目标

We want to use the observations

我们希望利用观测数据

$$
X_1,X_2,\dots,X_n
$$

to decide which hypothesis is true.

来判断哪一个假设是真的。

The basic idea is:

基本思想是：

- if the sample is more likely under $p$, choose $H_1$  
  如果样本在 $p$ 下更可能出现，就选 $H_1$
- otherwise choose $H_2$  
  否则就选 $H_2$

That is, compare

也就是比较

$$
p(X_1,\dots,X_n)
$$

and

和

$$
q(X_1,\dots,X_n)
$$

Choose $H_1$ if

如果满足下式，就判定 $H_1$

$$
p(X_1,\dots,X_n)\ge q(X_1,\dots,X_n)
$$

Equivalently,

等价地，

$$
\log \frac{p(X_1,\dots,X_n)}{q(X_1,\dots,X_n)}\ge 0
$$

---

### Definition: Log-Likelihood Ratio  
### 定义：对数似然比

Define the **log-likelihood ratio** (LLR) by

定义**对数似然比**（LLR）为

$$
LLR=\frac{1}{n}\log \frac{p(X_1,\dots,X_n)}{q(X_1,\dots,X_n)}
$$

Then the hypothesis test becomes:

那么假设检验规则就变成：

- choose $H_1$ if $LLR \ge 0$  
  若 $LLR \ge 0$，选择 $H_1$
- choose $H_2$ if $LLR < 0$  
  若 $LLR < 0$，选择 $H_2$

---

### Asymptotic Behavior of LLR  
### LLR 的渐近行为

#### Case 1: $H_1$ is true  
#### 情形 1：$H_1$ 为真

If $H_1$ is true, then $X_i \sim p(x)$, so

如果 $H_1$ 为真，那么 $X_i \sim p(x)$，所以

$$
LLR=\frac{1}{n}\sum_{i=1}^n \log \frac{p(X_i)}{q(X_i)}
$$

As $n \to \infty$, by the law of large numbers,

当 $n \to \infty$ 时，由大数定律，

$$
LLR \to \mathbb{E}_{X\sim p}\left[\log \frac{p(X)}{q(X)}\right]=D(p \| q)>0
$$

So when $H_1$ is true, the LLR tends to a positive number.

因此当 $H_1$ 为真时，LLR 趋向于一个正数。

#### Case 2: $H_2$ is true  
#### 情形 2：$H_2$ 为真

If $H_2$ is true, then $X_i \sim q(x)$, so

如果 $H_2$ 为真，那么 $X_i \sim q(x)$，所以

$$
LLR=\frac{1}{n}\sum_{i=1}^n \log \frac{p(X_i)}{q(X_i)}
$$

As $n \to \infty$,

当 $n \to \infty$ 时，

$$
LLR \to \mathbb{E}_{X\sim q}\left[\log \frac{p(X)}{q(X)}\right]
$$

and this equals

而这个值等于

$$
-\mathbb{E}_{X\sim q}\left[\log \frac{q(X)}{p(X)}\right]=-D(q \| p)<0
$$

So when $H_2$ is true, the LLR tends to a negative number.

因此当 $H_2$ 为真时，LLR 趋向于一个负数。

---

### Conclusion  
### 结论

As $n \to \infty$, the test based on $LLR$ becomes correct with probability approaching 1.

当 $n \to \infty$ 时，基于 LLR 的检验会越来越正确，正确概率趋近于 1。

---

### Two Types of Error  
### 两类错误

When $n$ is finite, there are two types of error.

当 $n$ 有限时，会有两类错误。

- **Miss probability**: the test decides $H_2$ but $H_1$ is actually true  
  **漏检概率**：检验判成 $H_2$，但实际上 $H_1$ 为真

Denote it by

记为

$$
P_M
$$

- **False alarm probability**: the test decides $H_1$ but $H_2$ is actually true  
  **虚警概率**：检验判成 $H_1$，但实际上 $H_2$ 为真

Denote it by

记为

$$
P_F
$$

As $n$ grows, both $P_M$ and $P_F$ go to zero.

随着 $n$ 增大，$P_M$ 和 $P_F$ 都会趋近于 0。

---

### Error Exponent Intuition  
### 错误指数的直观解释

A natural question is:

一个自然的问题是：

How fast do these error probabilities go to zero?

这些错误概率究竟以多快的速度趋近于 0？

Consider the false alarm probability $P_F$.

以虚警概率 $P_F$ 为例。

When $H_2$ is true, the LLR is typically near

当 $H_2$ 为真时，LLR 通常接近

$$
-D(q \| p)
$$

But in the false alarm event, the LLR is wrongly close to a positive value near

但在发生虚警时，LLR 会错误地跑到接近正值的位置，大约靠近

$$
D(p \| q)
$$

Let $\mathcal{E}$ denote that error event.

把这个错误事件记为 $\mathcal{E}$。

Then

那么

$$
P_F=\sum_{(x_1,\dots,x_n)\in \mathcal{E}} q(x_1,\dots,x_n)
$$

For sequences in $\mathcal{E}$, we have approximately

对于落在 $\mathcal{E}$ 中的序列，大致有

$$
\frac{1}{n}\log \frac{p(x_1,\dots,x_n)}{q(x_1,\dots,x_n)}\approx D(p \| q)
$$

which implies

这意味着

$$
q(x_1,\dots,x_n)\approx p(x_1,\dots,x_n)\,2^{-nD(p \| q)}
$$

Therefore,

因此

$$
P_F \approx \sum_{(x_1,\dots,x_n)\in \mathcal{E}} p(x_1,\dots,x_n)\,2^{-nD(p \| q)}
$$

and hence

从而

$$
P_F \le 2^{-nD(p \| q)}
$$

Similarly,

类似地，

$$
P_M \le 2^{-nD(q \| p)}
$$

So KL divergence determines the exponential decay rate of the testing errors.

因此，KL 散度决定了假设检验中错误概率的指数衰减速度。

---

# Summary  
# 总结

This chapter introduces several closely related ideas in information theory.

本章介绍了信息论中几个彼此紧密相关的重要概念。

- **Mutual information** $I(X;Y)$ measures how much information $X$ and $Y$ share.  
  **互信息** $I(X;Y)$ 衡量 $X$ 和 $Y$ 共享了多少信息。

- It can be written as the reduction in uncertainty, or as a KL divergence.  
  它既可以写成不确定性的减少量，也可以写成一个 KL 散度。

- **KL divergence** $D(p \| q)$ measures the mismatch between two distributions.  
  **KL 散度** $D(p \| q)$ 衡量两个分布之间的不匹配程度。

- **Cross entropy** satisfies  
  **交叉熵** 满足

$$
CE(p,q)=H(X)+D(p \| q)
$$

- In machine learning, minimizing cross entropy is equivalent to minimizing KL divergence when the target distribution is fixed.  
  在机器学习中，当目标分布固定时，最小化交叉熵等价于最小化 KL 散度。

- In hypothesis testing, the log-likelihood ratio converges to a KL divergence, and the error probabilities decay exponentially at KL rates.  
  在假设检验中，对数似然比会收敛到 KL 散度，而两类错误概率也会以 KL 散度决定的指数速度衰减。
