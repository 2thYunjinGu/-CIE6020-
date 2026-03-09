# Chapter 8 Notes on Information Theory  
# 第 8 章 信息论笔记

---

# Chapter 8 AEP  
# 第 8 章 渐近等概率性质（AEP）

## 8.1 LLN and AEP  
## 8.1 大数定律与 AEP

We now aim to show that $H(X)$ is the minimum number of bits needed to describe i.i.d. samples $X_i \sim p(x)$.

我们现在要说明：对于独立同分布样本 $X_i \sim p(x)$，$H(X)$ 就是描述它们所需的最小平均 bit 数。

The main mathematical tool is the **Asymptotic Equipartition Property (AEP)**.

这里的核心数学工具是 **渐近等概率性质（AEP）**。

---

### Theorem: Law of Large Numbers  
### 定理：大数定律

For i.i.d. random variables $X_i$,

对于独立同分布随机变量 $X_i$，

$$
\frac{1}{n}\sum_{i=1}^n X_i \to \mathbb{E}[X]
$$

in probability.

依概率收敛到其期望 $\mathbb{E}[X]$。

That is,

也就是说，

$$
\lim_{n\to\infty}\Pr\left\{\left|\frac{1}{n}\sum_{i=1}^n X_i-\mathbb{E}[X]\right|>\varepsilon\right\}=0, \qquad \forall \varepsilon>0
$$

---

### Theorem: Asymptotic Equipartition Property (AEP)  
### 定理：渐近等概率性质（AEP）

For i.i.d. random variables $X_i \sim p(x)$,

对于独立同分布随机变量 $X_i \sim p(x)$，

$$
-\frac{1}{n}\log p(X_1,\dots,X_n)\to H(X)
$$

in probability.

依概率收敛到熵 $H(X)$。

This means that for a long i.i.d. sequence, the quantity

这意味着：对于一个很长的独立同分布序列，

$$
-\frac{1}{n}\log p(X_1,\dots,X_n)
$$

is typically very close to $H(X)$.

这个量通常会非常接近 $H(X)$。

---

### Proof Idea  
### 证明思路

Since the samples are i.i.d.,

由于样本是独立同分布的，

$$
p(X_1,\dots,X_n)=\prod_{i=1}^n p(X_i)
$$

So

因此

$$
-\frac{1}{n}\log p(X_1,\dots,X_n)=-\frac{1}{n}\sum_{i=1}^n \log p(X_i)
$$

Let

令

$$
Y_i=-\log p(X_i)
$$

Then $\{Y_i\}$ are also i.i.d., and

那么 $\{Y_i\}$ 也是独立同分布的，并且

$$
\mathbb{E}[Y_i]=H(X)
$$

By the law of large numbers,

由大数定律，

$$
\frac{1}{n}\sum_{i=1}^n Y_i \to \mathbb{E}[Y_i]=H(X)
$$

Therefore,

因此

$$
-\frac{1}{n}\log p(X_1,\dots,X_n)\to H(X)
$$

---

### Definition: $\varepsilon$-Typical Sequence  
### 定义：$\varepsilon$-典型序列

For $\varepsilon>0$, a sequence $(x_1,\dots,x_n)$ is called **$\varepsilon$-typical** if

对于 $\varepsilon>0$，如果一个序列 $(x_1,\dots,x_n)$ 满足

$$
\left|-\frac{1}{n}\log p(x_1,\dots,x_n)-H(X)\right|\le \varepsilon
$$

then it is called an **$\varepsilon$-typical sequence**.

则称它为一个 **$\varepsilon$-典型序列**。

---

### Equivalent Characterization  
### 等价刻画

A sequence $(x_1,\dots,x_n)$ is $\varepsilon$-typical if and only if

一个序列 $(x_1,\dots,x_n)$ 是 $\varepsilon$-典型的，当且仅当

$$
2^{-n[H(X)+\varepsilon]}\le p(x_1,\dots,x_n)\le 2^{-n[H(X)-\varepsilon]}
$$

So all typical sequences have probabilities that are approximately the same on the exponential scale.

因此，所有典型序列在指数尺度上看，概率都差不多相同。

This is why the property is called **asymptotic equipartition**.

这也就是它被称为 **渐近等概率性质** 的原因。

---

### Definition: Typical Set  
### 定义：典型集

The set of all $\varepsilon$-typical sequences is called the **typical set**, denoted by

所有 $\varepsilon$-典型序列组成的集合称为 **典型集**，记作

$$
A_\varepsilon^{(n)}
$$

---

## 8.2 Size of the Typical Set  
## 8.2 典型集的大小

A natural question is:

一个自然的问题是：

How many sequences are in the typical set?

典型集中到底有多少个序列？

That is, what is

也就是，下面这个量有多大：

$$
\left|A_\varepsilon^{(n)}\right|
$$

---

### Binary Example  
### 二元例子

Suppose

设

$$
X_i=
\begin{cases}
0, & p \\
1, & 1-p
\end{cases}
$$

and denote the sequence by

并把长度为 $n$ 的序列记为

$$
X^n=(X_1,\dots,X_n)
$$

A typical sequence contains about $np$ zeros and $n(1-p)$ ones.

一个典型序列大约包含 $np$ 个 0 和 $n(1-p)$ 个 1。

Important note:

一个重要说明：

A **typical sequence** is not necessarily the **most likely sequence**.

**典型序列** 不一定是 **最可能序列**。

For example, when $p=0.1$, a typical sequence contains about 10 percent zeros and 90 percent ones, while the single most likely sequence is often something like all ones.

例如，当 $p=0.1$ 时，典型序列大约有 10% 的 0 和 90% 的 1；但单个最可能序列往往更像“全 1 序列”。

---

### Counting Typical Sequences  
### 典型序列个数的估计

The number of such sequences is approximately

这类序列的个数大约是

$$
\binom{n}{np}=\frac{n!}{(np)!(n-np)!}
$$

Using Stirling's formula,

利用 Stirling 公式，

$$
n!\approx \sqrt{2\pi n}\left(\frac{n}{e}\right)^n
$$

we obtain the approximation

可以得到近似

$$
\binom{n}{np}\approx 2^{nH(X)}
$$

So the size of the typical set is exponential in $nH(X)$.

所以典型集的大小大约是指数级的，数量级为 $2^{nH(X)}$。

---

### Theorem 1: Most Probability Mass Lies in the Typical Set  
### 定理 1：绝大多数概率质量集中在典型集上

For any $\varepsilon>0$,

对任意 $\varepsilon>0$，

$$
\Pr\left\{A_\varepsilon^{(n)}\right\}\ge 1-\varepsilon
$$

for sufficiently large $n$.

当 $n$ 足够大时，上式成立。

This means that with overwhelming probability, a long i.i.d. sequence is typical.

这意味着：当序列足够长时，它几乎一定是典型的。

---

### Proof Idea  
### 证明思路

By AEP,

由 AEP，

$$
\Pr\left\{\left|-\frac{1}{n}\log p(X_1,\dots,X_n)-H(X)\right|>\varepsilon\right\}\to 0
$$

So

因此

$$
\Pr\left\{(X_1,\dots,X_n)\notin A_\varepsilon^{(n)}\right\}\to 0
$$

Equivalently,

等价地，

$$
\Pr\left\{(X_1,\dots,X_n)\in A_\varepsilon^{(n)}\right\}\to 1
$$

Hence, for large enough $n$,

因此，当 $n$ 足够大时，

$$
\Pr\left\{A_\varepsilon^{(n)}\right\}\ge 1-\varepsilon
$$

---

### Theorem 2: Size of the Typical Set  
### 定理 2：典型集大小的界

For sufficiently large $n$,

当 $n$ 足够大时，

$$
(1-\varepsilon)\,2^{n[H(X)-\varepsilon]}\le |A_\varepsilon^{(n)}|\le 2^{n[H(X)+\varepsilon]}
$$

So the size of the typical set is roughly

因此典型集的大小大致为

$$
|A_\varepsilon^{(n)}|\approx 2^{nH(X)}
$$

---

### Proof of the Upper Bound  
### 上界证明

Since total probability is at most 1,

因为总概率不超过 1，

$$
1=\sum_{x^n} p(x^n)\ge \sum_{x^n\in A_\varepsilon^{(n)}} p(x^n)
$$

For each typical sequence,

对于每个典型序列，

$$
p(x^n)\ge 2^{-n[H(X)+\varepsilon]}
$$

Therefore,

因此

$$
1\ge |A_\varepsilon^{(n)}|\,2^{-n[H(X)+\varepsilon]}
$$

which implies

从而得到

$$
|A_\varepsilon^{(n)}|\le 2^{n[H(X)+\varepsilon]}
$$

---

### Proof of the Lower Bound  
### 下界证明

We know that

我们知道

$$
\Pr\left\{A_\varepsilon^{(n)}\right\}=\sum_{x^n\in A_\varepsilon^{(n)}} p(x^n)\ge 1-\varepsilon
$$

For each typical sequence,

而对每个典型序列，

$$
p(x^n)\le 2^{-n[H(X)-\varepsilon]}
$$

Hence,

因此

$$
1-\varepsilon \le |A_\varepsilon^{(n)}|\,2^{-n[H(X)-\varepsilon]}
$$

which implies

从而得到

$$
|A_\varepsilon^{(n)}|\ge (1-\varepsilon)\,2^{n[H(X)-\varepsilon]}
$$

---

### Intuition  
### 直观理解

Think of probability as “mass”.

把概率想象成“质量”。

Although the typical set is only a tiny fraction of the whole space $\mathcal{X}^n$, it contains almost all of the total probability mass.

尽管典型集只占整个空间 $\mathcal{X}^n$ 的很小一部分，但它却包含了几乎全部的概率质量。

This is exactly the key reason why compression is possible.

这正是数据压缩之所以可行的根本原因。

---

## 8.3 Fundamental Limit of Data Compression  
## 8.3 数据压缩的基本极限

### Theorem: Achievability  
### 定理：可达性

For i.i.d. random variables $X_i \sim p(x)$ and any $\delta>0$, for sufficiently large $n$, the sequence $(X_1,\dots,X_n)$ can be described using about

对于独立同分布随机变量 $X_i \sim p(x)$ 和任意 $\delta>0$，当 $n$ 足够大时，序列 $(X_1,\dots,X_n)$ 可以用大约

$$
n[H(X)+\delta]
$$

bits.

个 bit 来描述。

Equivalently, the average number of bits per symbol can be made arbitrarily close to $H(X)$.

等价地，平均每个符号所需的 bit 数可以任意逼近 $H(X)$。

---

### Idea of the Coding Scheme  
### 编码方案的思路

If a sequence $x^n$ is typical, assign it an index inside the typical set, together with a leading bit 1.

如果一个序列 $x^n$ 是典型的，就给它在典型集里分配一个编号，并在前面加一个前缀位 1。

If a sequence is not typical, assign it a code using a leading bit 0 and then describe it explicitly.

如果一个序列不是典型的，就给它加一个前缀位 0，然后直接把它显式写出来。

So:

因此：

- typical sequences use about  
  典型序列大约需要

$$
1+\log |A_\varepsilon^{(n)}|
$$

bits;

个 bit；

- non-typical sequences use about  
  非典型序列大约需要

$$
1+\log\left(|\mathcal{X}|^n-|A_\varepsilon^{(n)}|\right)
$$

bits.

个 bit。

---

### Typical Sequence Code Length  
### 典型序列的码长

For a typical sequence,

对于典型序列，

$$
1+\log |A_\varepsilon^{(n)}|\le 1+\log 2^{n[H(X)+\varepsilon]}=n[H(X)+\varepsilon]+1
$$

So each typical sequence needs at most about

因此每个典型序列最多只需要大约

$$
n[H(X)+\varepsilon]+1
$$

bits.

个 bit。

---

### Non-Typical Sequence Code Length  
### 非典型序列的码长

For a non-typical sequence,

对于非典型序列，

$$
1+\log\left(|\mathcal{X}|^n-|A_\varepsilon^{(n)}|\right)\le 1+\log |\mathcal{X}|^n
$$

Thus

因此

$$
1+\log |\mathcal{X}|^n = 1+n\log |\mathcal{X}|
$$

So non-typical sequences may require a longer description, but they occur with very small probability.

所以非典型序列可能需要更长的描述长度，但它们发生的概率非常小。

---

### Average Code Length  
### 平均码长

On average, the expected description length is at most approximately

平均来看，期望描述长度最多大约是

$$
\Pr\left\{A_\varepsilon^{(n)}\right\}\,[n(H(X)+\varepsilon)+1]
+
\left(1-\Pr\left\{A_\varepsilon^{(n)}\right\}\right)\,[n\log |\mathcal{X}|+1]
$$

Since

由于

$$
\Pr\left\{A_\varepsilon^{(n)}\right\}\to 1
$$

the second term becomes negligible, and the average number of bits per symbol approaches $H(X)$.

第二项会变得可以忽略，因此平均每个符号所需的 bit 数会逼近 $H(X)$。

---

### Can We Do Better?  
### 我们还能做得更好吗？

A natural question is:

一个自然问题是：

Can we find a set $B$ such that

能不能找到一个集合 $B$，满足

- $\Pr\{B\}\to 1$, and  
  $\Pr\{B\}\to 1$
- $|B|<|A_\varepsilon^{(n)}|$ ?  
  同时 $|B|<|A_\varepsilon^{(n)}|$ 呢？

The answer is **no**.

答案是：**不能**。

---

### Converse Idea  
### 反面结论的思路

Let $B_\delta^{(n)}$ be any set such that

设 $B_\delta^{(n)}$ 是任意一个集合，并满足

$$
\Pr\left\{B_\delta^{(n)}\right\}\ge 1-\delta
$$

Then for large $n$,

那么当 $n$ 足够大时，

$$
|B_\delta^{(n)}|\ge (1-\varepsilon-\delta)\,2^{n[H(X)-\varepsilon]}
$$

So any set that captures almost all the probability mass must have size at least about $2^{nH(X)}$.

因此，任何一个想要承载几乎全部概率质量的集合，其大小都至少要达到大约 $2^{nH(X)}$ 的量级。

This means that the typical set is essentially as small as possible.

这意味着：典型集在量级上已经是最小的了。

---

## 8.4 Main Conclusion  
## 8.4 主要结论

For i.i.d. data, the number of highly probable sequences is about

对于独立同分布数据，高概率序列的个数大约是

$$
2^{nH(X)}
$$

Each such sequence therefore needs roughly

因此，每个这样的序列大约需要

$$
\log 2^{nH(X)}=nH(X)
$$

bits to index.

个 bit 来编号。

So the minimum average number of bits per symbol is

所以平均每个符号所需的最小 bit 数就是

$$
H(X)
$$

This gives the fundamental limit of lossless data compression.

这就给出了无损数据压缩的基本极限。

---

# Summary  
# 总结

This chapter introduces the AEP and uses it to explain why entropy is the fundamental limit of lossless compression.

本章介绍了 AEP，并利用它解释了为什么熵就是无损压缩的基本极限。

- By the **AEP**, for i.i.d. samples,

  由 **AEP** 可知，对于独立同分布样本，

$$
-\frac{1}{n}\log p(X_1,\dots,X_n)\to H(X)
$$

- The **typical set** $A_\varepsilon^{(n)}$ contains almost all probability mass.

  **典型集** $A_\varepsilon^{(n)}$ 包含了几乎全部的概率质量。

- Its size is approximately

  它的大小大约为

$$
|A_\varepsilon^{(n)}|\approx 2^{nH(X)}
$$

- Therefore, a typical sequence can be indexed using about $nH(X)$ bits.

  因此，一个典型序列可以用大约 $nH(X)$ 个 bit 来编号。

- No much smaller set can still contain almost all the probability mass.

  任何远小于这个规模的集合，都不可能仍然包含几乎全部的概率质量。

So entropy is the minimum achievable average rate for lossless compression.

因此，熵就是无损压缩所能达到的最小平均码率。
