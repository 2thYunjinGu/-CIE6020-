# Chapter 7 Notes on Information Theory  
# 第 7 章 信息论笔记

---

# Chapter 7 Entropy Rate  
# 第 7 章 熵率

## 7.1 Motivation  
## 7.1 动机

If $(X_1, X_2, \dots, X_n)$ is a text sequence or a natural language sequence, then the variables $X_i$ are usually **not i.i.d.**, so we cannot directly use the single-letter entropy $H(X)$ to measure the information per symbol.

如果 $(X_1, X_2, \dots, X_n)$ 是一段文本或自然语言序列，那么各个随机变量 $X_i$ 通常**不是独立同分布的**，因此我们不能直接用单个随机变量的熵 $H(X)$ 来衡量每个符号的信息量。

Instead, we model the whole sequence

相反，我们把整个序列

$$
(X_1, X_2, \dots, X_n)
$$

as part of a stochastic process

看作一个随机过程的一部分

$$
X=\{X_i\}
$$

We know that

我们知道

$$
H(X_1,\dots,X_n)\ge H(X_1,\dots,X_{n-1})
$$

because adding one more random variable cannot decrease the total joint entropy.

因为加入一个新的随机变量不会让总联合熵减少。

A natural question is:

一个自然的问题是：

How fast does $H(X_1,\dots,X_n)$ grow with $n$?

$H(X_1,\dots,X_n)$ 随着 $n$ 增大到底增长得有多快？

---

### Definition: Entropy Rate  
### 定义：熵率

The **entropy rate** of a stochastic process $X=\{X_i\}$ is defined as

随机过程 $X=\{X_i\}$ 的**熵率**定义为

$$
H(X)=\lim_{n\to\infty}\frac{1}{n}H(X_1,\dots,X_n)
$$

if the limit exists.

如果这个极限存在。

It measures the average amount of information per symbol in a long sequence.

它衡量的是：当序列很长时，平均每个符号所包含的信息量。

---

### Example 1: i.i.d. Process  
### 例 1：独立同分布过程

Suppose

设

$$
X_i \overset{iid}{\sim} p(x)
$$

Then

则

$$
H(X_1,\dots,X_n)=H(X_1)+\cdots+H(X_n)=nH(X_1)
$$

Therefore,

因此

$$
\frac{1}{n}H(X_1,\dots,X_n)=H(X_1)
$$

So the entropy rate is

所以熵率为

$$
H(X)=H(X_1)
$$

This means that in an i.i.d. process, the total entropy grows linearly with $n$.

这意味着在独立同分布过程中，总熵会随 $n$ 线性增长。

---

### Example 2: Completely Repeated Process  
### 例 2：完全重复过程

Suppose

设

$$
X_i=X_1,\qquad \forall i=1,\dots,n
$$

Then the whole sequence is fully determined by the first symbol.

那么整个序列完全由第一个符号决定。

So

因此

$$
H(X_1,\dots,X_n)=H(X_1)
$$

and

并且

$$
\frac{1}{n}H(X_1,\dots,X_n)=\frac{1}{n}H(X_1)\to 0
$$

Hence the entropy rate is

因此熵率为

$$
H(X)=0
$$

So in this case, the total entropy does not grow linearly with $n$.

所以在这个例子里，总熵不会随着 $n$ 线性增长。

---

## 7.2 Stationary Stochastic Process  
## 7.2 平稳随机过程

### Definition: Stationary Process  
### 定义：平稳过程

A stochastic process $X=\{X_i\}$ is called **stationary** if for all $n$ and all shifts $k$,

如果随机过程 $X=\{X_i\}$ 满足：对任意 $n$ 和任意平移量 $k$，

$$
p(X_1,\dots,X_n)=p(X_{k+1},\dots,X_{k+n})
$$

then the process is called **stationary**.

那么这个过程称为**平稳过程**。

This means the distribution does not change with time shift.

这表示：过程的统计分布不会随着时间平移而改变。

---

### Theorem 1  
### 定理 1

For a stationary process $\{X_i\}$, the limit

对于平稳过程 $\{X_i\}$，极限

$$
\lim_{n\to\infty} H(X_n \mid X_1,\dots,X_{n-1})
$$

exists.

是存在的。

---

### Proof Idea  
### 证明思路

Let

令

$$
a_n=H(X_n \mid X_1,\dots,X_{n-1})
$$

We want to show that $\{a_n\}$ converges.

我们想证明数列 $\{a_n\}$ 收敛。

It is enough to show:

只需要证明：

1. $a_n$ is non-increasing  
   $a_n$ 单调不增

2. $a_n$ is lower bounded  
   $a_n$ 有下界

Since entropy is always nonnegative,

由于熵总是非负，

$$
a_n\ge 0
$$

so the lower bound is clear.

所以下界显然成立。

Now we show monotonicity.

下面说明单调性。

We have

我们有

$$
a_{n+1}=H(X_{n+1}\mid X_1,\dots,X_n)
$$

By the fact that conditioning never increases entropy,

由“条件化不会增加熵”可得

$$
H(X_{n+1}\mid X_1,\dots,X_n)\le H(X_{n+1}\mid X_2,\dots,X_n)
$$

By stationarity,

再利用平稳性，

$$
H(X_{n+1}\mid X_2,\dots,X_n)=H(X_n\mid X_1,\dots,X_{n-1})=a_n
$$

Thus

因此

$$
a_{n+1}\le a_n
$$

So $\{a_n\}$ is decreasing and bounded below by 0, hence it converges.

所以 $\{a_n\}$ 是单调递减且下有界，因此必然收敛。

---

### Theorem 2  
### 定理 2

For a stationary stochastic process,

对于平稳随机过程，

$$
H(X)=\lim_{n\to\infty}H(X_n\mid X_1,\dots,X_{n-1})
$$

That is, the entropy rate equals the limiting conditional entropy.

也就是说，熵率等于极限条件熵。

---

### Proof Idea  
### 证明思路

Let

令

$$
a_n=H(X_n\mid X_1,\dots,X_{n-1})
$$

and define

并定义

$$
b_n=\frac{1}{n}H(X_1,\dots,X_n)
$$

Using the chain rule for entropy,

由熵的链式法则，

$$
H(X_1,\dots,X_n)=H(X_1)+H(X_2\mid X_1)+\cdots+H(X_n\mid X_1,\dots,X_{n-1})
$$

So

因此

$$
b_n=\frac{1}{n}\sum_{i=1}^n a_i
$$

If $a_n\to a_\infty$, then the average of the first $n$ terms also converges to the same limit:

如果 $a_n\to a_\infty$，那么前 $n$ 项平均值也会收敛到同一个极限：

$$
b_n\to a_\infty
$$

Hence

因此

$$
H(X)=\lim_{n\to\infty}\frac{1}{n}H(X_1,\dots,X_n)=\lim_{n\to\infty}H(X_n\mid X_1,\dots,X_{n-1})
$$

So the entropy rate can be computed via long-term conditional entropy.

所以熵率可以通过长期条件熵来计算。

---

## 7.3 Markov Process  
## 7.3 马尔可夫过程

### Definition: Markov Process  
### 定义：马尔可夫过程

A stochastic process $X=\{X_i\}$ is called **Markov** if

随机过程 $X=\{X_i\}$ 称为**马尔可夫过程**，如果

$$
p(X_n\mid X_1,\dots,X_{n-1})=p(X_n\mid X_{n-1})
$$

That is, the present depends on the past only through the immediately previous state.

也就是说，当前状态对过去的依赖只通过前一个状态体现。

---

### Theorem  
### 定理

If $X=\{X_i\}$ is both stationary and Markov, then

如果 $X=\{X_i\}$ 同时是平稳的和马尔可夫的，那么

$$
H(X)=H(X_2\mid X_1)
$$

So for a stationary Markov process, the entropy rate is simply the one-step conditional entropy.

因此，对于平稳马尔可夫过程，熵率就是一步条件熵。

---

### Proof  
### 证明

From the previous theorem for stationary processes,

由前面关于平稳过程的定理，

$$
H(X)=\lim_{n\to\infty}H(X_n\mid X_1,\dots,X_{n-1})
$$

By the Markov property,

由马尔可夫性质，

$$
H(X_n\mid X_1,\dots,X_{n-1})=H(X_n\mid X_{n-1})
$$

By stationarity, the distribution of $(X_{n-1},X_n)$ is the same as that of $(X_1,X_2)$, so

再利用平稳性，$(X_{n-1},X_n)$ 的分布与 $(X_1,X_2)$ 相同，因此

$$
H(X_n\mid X_{n-1})=H(X_2\mid X_1)
$$

Hence

所以

$$
H(X)=H(X_2\mid X_1)
$$

---

### Example  
### 例子

Suppose

设

$$
X_{n+1}=\alpha X_n+Z_n
$$

where

其中

$$
Z_n \overset{iid}{\sim} p(z)
$$

Then

那么

$$
H(X)=H(X_2\mid X_1)
$$

and

并且

$$
H(X_2\mid X_1)=H(\alpha X_1+Z_1\mid X_1)=H(Z_1)
$$

So the entropy rate is determined by the innovation noise.

因此，熵率由“创新噪声” $Z_n$ 的熵决定。

---

## 7.4 Entropy of English  
## 7.4 英文的熵

Consider an English text sequence

考虑一段英文文本序列

$$
(X_1,X_2,\dots,X_n)
$$

where each symbol $X_i$ belongs to an alphabet such as

其中每个符号 $X_i$ 取自一个字母表，例如

$$
\{a,b,c,\dots,z,\text{space},.\}
$$

We may model English text as a stationary stochastic process.

我们可以把英文文本看作一个平稳随机过程。

Then its entropy rate is

那么它的熵率就是

$$
H(X)=\lim_{n\to\infty}H(X_n\mid X_1,\dots,X_{n-1})
$$

In practice, however, we cannot really let $n\to\infty$.

但在实际中，我们不可能真的让 $n\to\infty$。

When $n$ is finite, there are many possible contexts

当 $n$ 有限时，会有许多可能的上下文

$$
(X_1,\dots,X_n)
$$

For example, in a text containing 1000 symbols, if $n=5$, then there are 996 possible length-5 contexts.

例如，在一段长度为 1000 的文本中，如果 $n=5$，那么长度为 5 的上下文大约有 996 个可能位置。

So we can estimate the entropy rate by averaging conditional entropies over these contexts:

因此，我们可以通过对这些上下文下的条件熵做平均来估计熵率：

$$
H(X)\approx \mathbb{E}[H(X_n\mid X_1,\dots,X_{n-1})]
$$

---

### Shannon's Estimates  
### Shannon 的估计结果

The lecture mentions Shannon's classical estimates for English entropy:

讲义中提到了 Shannon 对英文熵的经典估计：

- when $n=0$,  
  当 $n=0$ 时，

$$
H(X)\approx 4.76
$$

- when $n=1$,  
  当 $n=1$ 时，

$$
H(X)\approx 4.03
$$

- when $n=4$,  
  当 $n=4$ 时，

$$
H(X)\approx 2.8
$$

- when $n\gg 1$,  
  当 $n\gg 1$ 时，

$$
H(X)\approx 1.3
$$

These values show that the more context we know, the less uncertainty remains about the next symbol.

这些数值说明：我们知道的上下文越多，下一个字符的不确定性就越小。

This is why natural language has much lower entropy rate than an i.i.d. random string over the same alphabet.

这也解释了为什么自然语言的熵率远低于同一字母表上的独立随机字符串。

---

### Final Question  
### 最后一个问题

The lecture ends by asking:

讲义最后提出了一个问题：

What is the entropy of Chinese?

中文的熵是多少？

This suggests that the same entropy-rate framework can be used to study other languages as well.

这说明：同样的熵率框架也可以用于研究其他语言。

---

# Summary  
# 总结

This chapter introduces the concept of **entropy rate** for stochastic processes.

本章介绍了随机过程中的**熵率**概念。

- For a general process $X=\{X_i\}$, the entropy rate is

  对于一般随机过程 $X=\{X_i\}$，熵率定义为

$$
H(X)=\lim_{n\to\infty}\frac{1}{n}H(X_1,\dots,X_n)
$$

- For a stationary process, the entropy rate equals the limiting conditional entropy

  对于平稳过程，熵率等于极限条件熵

$$
H(X)=\lim_{n\to\infty}H(X_n\mid X_1,\dots,X_{n-1})
$$

- For a stationary Markov process, this simplifies to

  对于平稳马尔可夫过程，这进一步简化为

$$
H(X)=H(X_2\mid X_1)
$$

- For natural language such as English, entropy rate captures the average uncertainty per symbol in long text.

  对于英语这样的自然语言，熵率刻画了长文本中平均每个符号的不确定性。

- Shannon's estimates show that language has strong dependence structure, so its entropy rate is much smaller than the entropy of isolated symbols.

  Shannon 的估计说明，语言中存在很强的依赖结构，因此它的熵率远小于单个孤立符号的熵。
