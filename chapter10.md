# Chapter 10 Notes on Information Theory  
# 第 10 章 信息论笔记

---

# Chapter 10 Shannon Code  
# 第 10 章 Shannon 编码

## 10.1 Optimizing Codeword Length  
## 10.1 码长优化

Suppose the source alphabet is

设信源字母表为

$$
\mathcal{X}=\{1,\dots,M\}
$$

and symbol $i$ has probability

并且符号 $i$ 的概率为

$$
p_i
$$

Let the codeword for symbol $i$ be $c(i)$, and let its length be

设符号 $i$ 的码字为 $c(i)$，其长度记为

$$
l_i
$$

We now seek the "optimal" uniquely decodable code, namely to minimize the expected code length

我们现在希望寻找“最优”的唯一可译码，也就是最小化平均码长

$$
L=\sum_i p_i l_i
$$

subject to the constraint from McMillan's inequality:

并满足 McMillan 不等式约束：

$$
\sum_i 2^{-l_i}\le 1
$$

with each $l_i$ being a positive integer.

其中每个 $l_i$ 都是正整数。

---

### Problem P1  
### 问题 P1

The integer optimization problem is

这个整数优化问题是

$$
\min \sum_i p_i l_i
$$

subject to

满足约束

$$
\sum_i 2^{-l_i}\le 1
$$

and

以及

$$
l_i \in \mathbb{Z}_{>0}
$$

This is the exact discrete optimization problem for codeword lengths.

这就是码长优化的精确离散问题。

---

### Relaxed Problem P2  
### 松弛问题 P2

To make the problem easier, first ignore the integer constraint and consider the relaxed problem:

为了更容易求解，我们先忽略整数约束，考虑松弛问题：

$$
\min \sum_i p_i l_i
$$

subject to

满足

$$
\sum_i 2^{-l_i}\le 1
$$

where now $l_i$ can be real numbers.

此时允许 $l_i$ 为实数。

---

### Lagrangian Method  
### 拉格朗日方法

Define the Lagrangian

定义拉格朗日函数

$$
\mathcal{L}(l_i,\lambda)=\sum_i p_i l_i+\lambda\left(\sum_i 2^{-l_i}-1\right)
$$

At the optimum, we differentiate with respect to $l_i$:

在最优点，对 $l_i$ 求导：

$$
\frac{\partial \mathcal{L}}{\partial l_i}=p_i-\lambda (\ln 2)\,2^{-l_i}=0
$$

So

因此

$$
2^{-l_i}=\frac{p_i}{\lambda \ln 2}
$$

At the optimum, the constraint must be active, so

在最优点，约束必须取等号，因此

$$
\sum_i 2^{-l_i}=1
$$

Substituting the expression above gives

代入上式可得

$$
\sum_i \frac{p_i}{\lambda \ln 2}=1
$$

Since $\sum_i p_i=1$, we get

由于 $\sum_i p_i=1$，可得

$$
\lambda \ln 2 = 1
$$

Hence

因此

$$
2^{-l_i}=p_i
$$

which implies

从而得到

$$
l_i^*=\log \frac{1}{p_i}
$$

---

### Lower Bound on Average Length  
### 平均码长下界

The relaxed problem gives a lower bound on the original discrete problem.

松弛问题给出了原始离散问题的一个下界。

Indeed,

确实如此，

$$
L=\sum_i p_i l_i \ge \sum_i p_i l_i^*
$$

and

而

$$
\sum_i p_i l_i^*=\sum_i p_i \log \frac{1}{p_i}=H(X)
$$

Therefore,

因此

$$
L\ge H(X)
$$

So entropy is a lower bound on the average code length of any uniquely decodable code.

所以，熵是任意唯一可译码平均码长的下界。

---

## 10.2 Shannon Code  
## 10.2 Shannon 编码

The optimal real-valued solution is

最优的实数解是

$$
l_i^*=\log \frac{1}{p_i}
$$

But in an actual code, codeword lengths must be integers.

但在实际编码中，码长必须是整数。

So Shannon's idea is to choose

因此 Shannon 的想法是取

$$
l_i=\left\lceil \log \frac{1}{p_i} \right\rceil
$$

This is called the **Shannon code**.

这称为 **Shannon 编码**。

---

### Average Length of Shannon Code  
### Shannon 编码的平均码长

The average code length is

平均码长为

$$
L=\sum_i p_i \left\lceil \log \frac{1}{p_i} \right\rceil
$$

Since

由于

$$
\left\lceil x \right\rceil < x+1
$$

we have

所以有

$$
L<\sum_i p_i \left(\log \frac{1}{p_i}+1\right)
$$

Thus

因此

$$
L<\sum_i p_i \log \frac{1}{p_i}+1=H(X)+1
$$

Combined with the lower bound $L\ge H(X)$, we obtain

结合前面的下界 $L\ge H(X)$，得到

$$
H(X)\le L < H(X)+1
$$

This is the basic performance guarantee of Shannon coding.

这就是 Shannon 编码的基本性能保证。

---

### Two Notes  
### 两点说明

#### Note 1  
#### 说明 1

If $\log (1/p_i)$ happens to be an integer for every $i$, then

如果对每个 $i$，$\log (1/p_i)$ 恰好都是整数，那么

$$
l_i=\log \frac{1}{p_i}
$$

and we achieve the entropy exactly:

那么就能精确达到熵：

$$
L=H(X)
$$

Otherwise, the overhead is strictly less than 1 bit.

否则，额外开销严格小于 1 bit。

#### Note 2  
#### 说明 2

This 1-bit overhead is not always small in relative terms.

这个 1 bit 的额外开销从相对比例上看并不总是小。

For example, the entropy of an English letter is only around 1.3 bits, so an extra 1 bit is actually significant.

例如，一个英文字符的熵大约只有 1.3 bits，因此多出来的 1 bit 其实是很显著的。

---

### How to Reduce the Overhead  
### 如何减小开销

The lecture suggests the following idea:

讲义给出的思路是：

Group many symbols together as one super-symbol.

把多个符号打包成一个“超级符号”。

Let

设

$$
Y=(X_1,\dots,X_n)
$$

and then design a Shannon code for $Y$.

然后对 $Y$ 设计 Shannon 编码。

By the same theorem,

根据同样的结论，

$$
H(Y)\le L_Y < H(Y)+1
$$

Since $Y=(X_1,\dots,X_n)$, this becomes

由于 $Y=(X_1,\dots,X_n)$，这就变成

$$
H(X_1,\dots,X_n)\le nL < H(X_1,\dots,X_n)+1
$$

For i.i.d. symbols, $H(X_1,\dots,X_n)=nH(X)$, so

对于独立同分布符号，$H(X_1,\dots,X_n)=nH(X)$，因此

$$
nH(X)\le nL < nH(X)+1
$$

Dividing by $n$ gives

两边同时除以 $n$，得到

$$
H(X)\le L < H(X)+\frac{1}{n}
$$

So by grouping many symbols together, the per-symbol overhead can be reduced from less than 1 bit to less than $1/n$ bit.

所以，把多个符号打包后，每个符号的额外开销就可以从“小于 1 bit”降到“小于 $1/n$ bit”。

---

### Practical Limitation  
### 实际局限

As $n\to\infty$, the average code length per symbol approaches $H(X)$.

当 $n\to\infty$ 时，每个符号的平均码长会逼近 $H(X)$。

However, the codebook size grows as

但是码书规模会增长为

$$
M^n
$$

So the complexity grows exponentially with $n$.

因此复杂度会随着 $n$ 指数增长。

---

## 10.3 Wrong Distribution  
## 10.3 分布错配

Suppose the training set has distribution

假设训练集的分布为

$$
p_i
$$

but the test set has true distribution

但测试集的真实分布为

$$
q_i
$$

We design the Shannon code according to the training distribution $p_i$, so

我们按训练分布 $p_i$ 来设计 Shannon 编码，因此

$$
l_i=\left\lceil \log \frac{1}{p_i} \right\rceil
$$

Now apply this code to data drawn from $q_i$.

现在把这个编码用于服从 $q_i$ 的测试数据。

Then the average code length becomes

那么平均码长变为

$$
L=\sum_i q_i l_i=\sum_i q_i \left\lceil \log \frac{1}{p_i} \right\rceil
$$

Using the inequality $\lceil x\rceil < x+1$, we get

利用不等式 $\lceil x\rceil < x+1$，可得

$$
L<\sum_i q_i \log \frac{1}{p_i}+1
$$

Now rewrite it as

把它改写为

$$
L<\sum_i q_i \log \left(\frac{1}{q_i}\cdot \frac{q_i}{p_i}\right)+1
$$

So

因此

$$
L<\sum_i q_i \log \frac{1}{q_i}+\sum_i q_i \log \frac{q_i}{p_i}+1
$$

That is,

也就是

$$
L<H(q)+D(q\|p)+1
$$

Equivalently,

等价地，

$$
L<CE(q,p)+1
$$

where $CE(q,p)$ is the cross entropy.

其中 $CE(q,p)$ 是交叉熵。

---

### Interpretation  
### 直观理解

The quantity

这个量

$$
D(q\|p)
$$

is the penalty for not knowing the true distribution.

就是“不知道真实分布”所带来的额外代价。

So if we design a code using the wrong distribution, the coding cost increases by approximately the KL divergence.

因此，如果我们用错误分布设计编码，那么平均码长会大约增加一个 KL 散度的代价。

The lecture summarizes this as:

讲义把它总结为：

- $D(q\|p)$ is the cost of distribution mismatch  
  $D(q\|p)$ 是分布错配的代价
- $L$ is less than cross entropy plus 1  
  $L$ 小于交叉熵再加 1

---

## 10.4 Value of Side Information  
## 10.4 边信息的价值

Suppose $(X,Y)$ are correlated, and $Y$ is provided as side information to both the encoder and decoder.

假设 $(X,Y)$ 相关，并且 $Y$ 作为边信息同时提供给编码器和解码器。

The question is:

问题是：

How much can side information help compress $X$?

边信息究竟能在多大程度上帮助压缩 $X$？

---

### Main Idea  
### 核心思路

For each possible value $y$ of $Y$, design a codebook

对于 $Y$ 的每一个可能取值 $y$，单独设计一个码书

$$
c(x\mid y)
$$

based on the conditional distribution

基于对应的条件分布

$$
p(x\mid y)
$$

When the codebook $c(x\mid y)$ is used, Shannon coding gives

当使用码书 $c(x\mid y)$ 时，Shannon 编码给出

$$
H(X\mid y)\le L_y < H(X\mid y)+1
$$

where $L_y$ is the average length conditioned on $Y=y$.

其中 $L_y$ 表示在条件 $Y=y$ 下的平均码长。

Since this happens with probability $p(y)$, averaging over all $y$ gives

由于这种情况以概率 $p(y)$ 发生，对所有 $y$ 取平均可得

$$
\sum_y p(y)H(X\mid y)\le L < \sum_y p(y)H(X\mid y)+1
$$

Thus

因此

$$
H(X\mid Y)\le L < H(X\mid Y)+1
$$

So with side information available to both encoder and decoder, the relevant coding limit becomes conditional entropy instead of ordinary entropy.

所以，当编码器和解码器都拥有边信息时，真正相关的压缩极限就从普通熵变成了条件熵。

---

### Why Side Information Is Valuable  
### 为什么边信息有价值

Since

由于

$$
H(X\mid Y)<H(X)
$$

whenever $X$ and $Y$ are correlated, side information reduces the number of bits needed to encode $X$.

只要 $X$ 和 $Y$ 有相关性，边信息就会减少编码 $X$ 所需的 bit 数。

So side information is valuable because it lowers the effective uncertainty of the source.

因此，边信息之所以有价值，是因为它降低了信源的有效不确定性。

---

# Summary  
# 总结

This chapter studies Shannon coding and its performance.

本章研究了 Shannon 编码及其性能。

- By relaxing the integer constraint on codeword lengths, the optimal real-valued solution is

  通过去掉码长必须为整数的约束，可得最优实数解为

$$
l_i^*=\log \frac{1}{p_i}
$$

- This shows that the average code length of any uniquely decodable code must satisfy

  这说明任意唯一可译码的平均码长都必须满足

$$
L\ge H(X)
$$

- Shannon code uses integer lengths

  Shannon 编码采用整数码长

$$
l_i=\left\lceil \log \frac{1}{p_i} \right\rceil
$$

and achieves

并满足

$$
H(X)\le L < H(X)+1
$$

- Grouping many symbols together reduces the per-symbol overhead to below $1/n$.

  把多个符号打包后，每个符号的额外开销可以降到 $1/n$ 以下。

- If the wrong distribution is used for coding, the average length becomes close to cross entropy:

  如果用错误分布设计编码，平均码长会接近交叉熵：

$$
L< H(q)+D(q\|p)+1 = CE(q,p)+1
$$

- With side information available at both encoder and decoder, the effective coding limit becomes conditional entropy:

  当编码器和解码器都拥有边信息时，压缩极限变为条件熵：

$$
H(X\mid Y)\le L < H(X\mid Y)+1
$$

So Shannon coding connects entropy, cross entropy, KL divergence, and side information in a very natural way.

因此，Shannon 编码把熵、交叉熵、KL 散度以及边信息这几个概念自然地联系在了一起。
