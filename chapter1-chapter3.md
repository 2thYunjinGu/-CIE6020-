# Chapters 1--3 Notes on Information Theory  
# 信息论第 1--3 章双语笔记

---

# Chapter 1 Introduction  
# 第 1 章 引言

## 1.1 Interpretation of Information  
## 1.1 信息的理解

In information theory, **information** can be understood as the minimum number of bits needed to describe the outcome of a random variable.

在信息论中，**信息（information）** 可以理解为：描述一个随机变量结果所需要的最少比特数。

A bit is a binary symbol taking value `0` or `1`.

一个 bit（二进制位）就是只能取 `0` 或 `1` 的二元符号。

### Example 1: A fair weather variable  
### 例 1：均匀天气变量

Suppose

设

$$
X=\begin{cases}
\text{rain}, & 50\% \\
\text{shine}, & 50\%
\end{cases}
$$

Since there are two equally likely outcomes, one bit is sufficient to encode the result.

由于这里只有两个等可能结果，所以用 1 个 bit 就足以编码结果。

Therefore, $X$ contains **1 bit** of information.

因此，$X$ 含有 **1 bit** 的信息。

### Example 2: A deterministic variable  
### 例 2：确定性变量

Suppose

设

$$
X=\begin{cases}
\text{rain}, & 100\% \\
\text{shine}, & 0\%
\end{cases}
$$

In this case there is no uncertainty, so no information is needed to specify the outcome.

此时结果没有任何不确定性，因此不需要额外信息来说明结果。

Therefore, $X$ contains **0 bits** of information.

因此，$X$ 含有 **0 bit** 的信息。

### Example 3: Winner of an 8-horse race  
### 例 3：8 匹马赛跑的冠军

Suppose the winner of a horse race is one of

设赛马冠军可能是以下 8 匹马中的一匹：

$$
X \in \{A,B,C,D,E,F,G,H\}
$$

If all 8 horses are equally likely, then each outcome can be represented by a 3-bit binary code:

如果 8 匹马获胜的概率都相同，那么每个结果都可以用一个 3 bit 的二进制编码表示：

- $A \to 000$
- $B \to 001$
- $C \to 010$
- $\cdots$
- $H \to 111$

Hence the outcome can be described using **3 bits**.

因此，描述这个结果需要 **3 bits**。

So $X$ contains **3 bits** of information.

所以 $X$ 含有 **3 bits** 的信息。

### Example 4: Non-uniform probabilities  
### 例 4：非均匀概率情形

Now suppose

现在设

$$
X=\begin{cases}A, & 1/2 \\ B, & 1/4 \\ C, & 1/8 \\ D, & 1/16 \\ E, & 1/64 \\ F, & 1/64 \\ G, & 1/64 \\ H, & 1/64 \end{cases}
$$

A more efficient code is:

一种更高效的编码方式是：

- $A \to 0$
- $B \to 10$
- $C \to 110$
- $D \to 1110$
- $E \to 111100$
- $F \to 111101$
- $G \to 111110$
- $H \to 111111$

The average code length is

平均码长为

$$
1 \cdot \frac{1}{2} + 2 \cdot \frac{1}{4} + 3 \cdot \frac{1}{8} + 4 \cdot \frac{1}{16} + 6 \cdot \frac{1}{64} \cdot 4 = 2
$$

Thus, on average, only **2 bits** are needed to describe $X$.

因此，平均只需要 **2 bits** 就能描述 $X$。

This is smaller than 3 bits because more probable outcomes are assigned shorter codewords.

这比 3 bits 更小，因为概率更大的事件被分配了更短的码字。

---

## 1.2 Information Transmission over a Channel  
## 1.2 信道中的信息传输

A communication system can be modeled as

一个通信系统可以建模为

$$
X \longrightarrow \text{channel} \longrightarrow Y
$$

where:

其中：

- $X$ is the channel input  
  $X$ 是信道输入
- $Y$ is the channel output  
  $Y$ 是信道输出

The behavior of the channel is specified by the conditional probabilities

信道的行为由条件概率决定：

$$
\Pr(Y=y \mid X=x)
$$

For example, if $X \in \{0,1\}$ and $Y \in \{0,1\}$, then the channel is completely determined by

例如，如果 $X \in \{0,1\}$ 且 $Y \in \{0,1\}$，那么这个信道完全由下面这些条件概率决定：

$$
\Pr(Y \mid X=0), \qquad \Pr(Y \mid X=1)
$$

### Definition: Channel Capacity  
### 定义：信道容量

The **channel capacity** is the maximum number of bits that can be transmitted **reliably** through the channel.

**信道容量（channel capacity）** 是指：通过该信道能够**可靠传输**的最大比特数。

### Example 1: Perfect binary channel  
### 例 1：完美二元信道

If the channel transmits each bit without error,

如果信道可以无误地传输每一个 bit，

$$
0 \to 0, \qquad 1 \to 1
$$

then the capacity is **1 bit per channel use**.

那么它的容量就是 **每次使用信道传输 1 bit**。

### Example 2: Perfect 4-symbol channel  
### 例 2：完美四符号信道

If the channel can perfectly transmit 4 equally distinguishable symbols, then the capacity is

如果信道可以完美传输 4 个彼此可区分的符号，那么容量为

$$
\log_2 4 = 2
$$

bits per use.

即每次使用信道可以传输 2 bits。

### Example 3: Distinguishable groups  
### 例 3：可区分的输出组

Suppose:

设：

- when $X=0$, the output is always in the set $\{0,1\}$  
  当 $X=0$ 时，输出一定落在集合 $\{0,1\}$ 中
- when $X=1$, the output is always in the set $\{2,3\}$  
  当 $X=1$ 时，输出一定落在集合 $\{2,3\}$ 中

Then from $Y$ we can always determine whether $X=0$ or $X=1$, so the capacity is **1 bit**.

那么从 $Y$ 就总能判断输入究竟是 $0$ 还是 $1$，因此容量为 **1 bit**。

---

## 1.3 Source Coding and Channel Coding  
## 1.3 信源编码与信道编码

A standard communication system is

一个标准通信系统可以写成

$$
\text{message} \to \text{encoder} \to \text{bits} \to \text{channel} \to \text{bits} \to \text{decoder} \to \text{message}
$$

This naturally leads to two fundamental coding problems.

这自然引出了两个基本编码问题。

### Source Coding  
### 信源编码

Compress the source into as few bits as possible.

尽可能用更少的 bit 去压缩信源信息。

### Channel Coding  
### 信道编码

Add redundancy so that the message can still be recovered reliably after passing through a noisy channel.

加入适当冗余，使消息经过有噪声的信道后仍能被可靠恢复。

In summary:

总结来说：

- the minimum number of bits needed to describe a source is related to **entropy**  
  描述信源所需的最小平均比特数，与 **熵（entropy）** 有关
- the maximum number of bits that can be reliably transmitted through a channel is related to **mutual information**  
  通过信道能可靠传输的最大比特数，与 **互信息（mutual information）** 有关

---

# Chapter 2 Entropy  
# 第 2 章 熵

## 2.1 Definition of Entropy  
## 2.1 熵的定义

Let $X$ be a discrete random variable taking values in an alphabet $\mathcal{X}$.

设 $X$ 是一个离散随机变量，其取值集合为字母表 $\mathcal{X}$。

If

如果

$$
\mathcal{X} = \{a,b,c\}
$$

with probabilities

并且对应概率为

$$
\Pr(X=a)=p_1, \qquad \Pr(X=b)=p_2, \qquad \Pr(X=c)=p_3
$$

then the **entropy** of $X$ is defined as

那么 $X$ 的**熵（entropy）** 定义为

$$
H(X)=\sum_{x \in \mathcal{X}} p(x)\log \frac{1}{p(x)}
$$

Equivalently,

等价地，也可写成

$$
H(X) = - \sum_{x \in \mathcal{X}} p(x)\log p(x)
$$

### Units  
### 单位

- If the logarithm is base 2, entropy is measured in **bits**  
  如果对数底为 2，则熵的单位是 **bit**
- If the logarithm is base $e$, entropy is measured in **nats**  
  如果对数底为 $e$，则熵的单位是 **nat**

Also, entropy can be written as an expectation:

此外，熵还可以写成期望形式：

$$
H(X)=\mathbb{E}\left[\log \frac{1}{p(X)}\right]
$$

---

## 2.2 Basic Properties of Entropy  
## 2.2 熵的基本性质

### Theorem 1  
### 定理 1

For any discrete random variable $X$,

对任意离散随机变量 $X$，都有

$$
H(X)\ge 0
$$

### Proof  
### 证明

Since $0 < p(x) \le 1$, we have

由于 $0 < p(x) \le 1$，所以有

$$
\log \frac{1}{p(x)} \ge 0
$$

Taking expectation yields

对其取期望可得

$$
H(X)=\mathbb{E}\left[\log \frac{1}{p(X)}\right]\ge 0
$$

### Theorem 2  
### 定理 2

If $X$ takes values in a set of size $m$, then

如果 $X$ 的取值集合大小为 $m$，那么

$$
H(X)\le \log m
$$

Equality holds if and only if $X$ is uniformly distributed on its alphabet.

当且仅当 $X$ 在其取值集合上服从均匀分布时，等号成立。

### Proof  
### 证明

By Jensen's inequality and the concavity of $\log$,

由 Jensen 不等式以及 $\log$ 函数的凹性可得

$$
H(X)=\mathbb{E}\left[\log \frac{1}{p(X)}\right]\le \log \left( \mathbb{E}\left[\frac{1}{p(X)}\right] \right)
$$

Now

而

$$
\mathbb{E}\left[\frac{1}{p(X)}\right]=\sum_x p(x)\frac{1}{p(x)}=m
$$

Therefore,

因此

$$
H(X)\le \log m
$$

Equality holds only when all probabilities are equal, that is, when $X$ is uniform.

当且仅当所有概率都相等时等号成立，即 $X$ 服从均匀分布。

---

## 2.3 Entropy and Data Compression  
## 2.3 熵与数据压缩

Entropy measures the minimum average number of bits required to describe a random variable.

熵衡量的是：描述一个随机变量所需的最小平均比特数。

This is the central idea of **source coding**.

这正是**信源编码**的核心思想。

### Example 1: Deterministic variable  
### 例 1：确定性变量

If

如果

$$
X=\begin{cases}0, & 1 \\ 1, & 0 \end{cases}
$$

then

则

$$
H(X)=0
$$

Indeed, no bits are needed because the outcome is always known in advance.

确实如此，因为结果总是 заранее确定的，不需要任何额外比特来描述。

### Example 2: Fair binary variable  
### 例 2：均匀二元变量

If

如果

$$
X=\begin{cases}0, & 1/2 \\ 1, & 1/2 \end{cases}
$$

then

则

$$
H(X)=\frac{1}{2}\log 2+\frac{1}{2}\log 2=1
$$

So one bit per symbol is needed on average.

所以平均每个符号需要 1 bit。

### Example 3: Highly skewed binary variable  
### 例 3：高度偏斜的二元变量

If

如果

$$
X=\begin{cases}0, & 0.01 \\ 1, & 0.99 \end{cases}
$$

then

则

$$
H(X)=0.01 \log_2 \frac{1}{0.01}+0.99 \log_2 \frac{1}{0.99}\approx 0.081 \text{ bits}
$$

This means that although a single sample cannot literally be encoded with less than 1 bit, a long sequence of independent samples can be compressed so that the average description length per symbol is close to $0.081$ bits.

这意味着：虽然单个样本不可能真的“少于 1 bit”地被存储，但对一长串独立样本整体压缩后，平均到每个符号上的码长可以逼近 $0.081$ bits。

### Key idea  
### 核心思想

Instead of encoding one symbol at a time, encode a long block:

不要一次编码一个符号，而是整体编码一个长块：

$$
(X_1, X_2, \dots, X_n)
$$

If each $X_i$ equals 0 with probability 0.01 and 1 with probability 0.99, then a typical sequence contains about 1 percent zeros and 99 percent ones.

如果每个 $X_i$ 取 0 的概率为 0.01、取 1 的概率为 0.99，那么一个典型序列中大约有 1% 的 0 和 99% 的 1。

The number of typical sequences is much smaller than $2^n$, so they can be described using approximately

典型序列的总数远小于 $2^n$，因此它们只需要大约

$$
nH(X)
$$

bits.

个 bit 就能描述。

Thus the average number of bits per symbol approaches $H(X)$.

因此，平均每个符号所需的 bit 数会趋近于 $H(X)$。

---

## 2.4 Entropy and Kolmogorov Complexity  
## 2.4 熵与 Kolmogorov 复杂度

The lecture also relates entropy to a concept from theoretical computer science.

讲义还把熵与理论计算机科学中的一个概念联系了起来。

### Definition: Kolmogorov Complexity  
### 定义：Kolmogorov 复杂度

The **Kolmogorov complexity** $K(x)$ of a finite object $x$ is the length of the shortest program that outputs $x$.

一个有限对象 $x$ 的 **Kolmogorov 复杂度** $K(x)$，是指“输出 $x$ 的最短程序”的长度。

### Example 1: A mathematical constant  
### 例 1：数学常数

The number $\pi$ has infinitely many digits, but it has a short algorithmic description.

数 $\pi$ 虽然有无限多位小数，但它有很短的算法描述。

So although the full decimal expansion is infinite, its Kolmogorov complexity is finite.

所以虽然它的十进制展开是无限的，但它的 Kolmogorov 复杂度仍然是有限的。

### Example 2: A repetitive string  
### 例 2：重复字符串

Consider the string

考虑字符串

$$
10101010\cdots10
$$

with `"10"` repeated 50 times.

其中 `"10"` 重复了 50 次。

Instead of explicitly listing all 100 bits, we can describe it as:

我们不必把 100 个 bit 全部逐个写出来，而可以描述为：

> print `"10"` fifty times

So this string has low Kolmogorov complexity.

因此这个字符串的 Kolmogorov 复杂度很低。

Now let

现在设

$$
X_1, X_2, \dots, X_n
$$

be i.i.d. random variables with the same distribution as $X$, and define

为与 $X$ 同分布的 i.i.d. 随机变量，并定义

$$
\mathbf{X} = (X_1, \dots, X_n)
$$

A typical realization of $\mathbf{X}$ can be compressed into about

那么 $\mathbf{X}$ 的一个典型实现可以被压缩到大约

$$
nH(X)
$$

bits.

个 bit。

Hence its Kolmogorov complexity satisfies, heuristically,

因此，从启发式角度看，它的 Kolmogorov 复杂度满足

$$
K(\mathbf{X}) \approx nH(X) + c
$$

where $c$ is a constant independent of $n$.

其中 $c$ 是一个与 $n$ 无关的常数。

Dividing by $n$ gives

两边同时除以 $n$，得到

$$
\frac{1}{n}K(\mathbf{X}) \approx H(X) + \frac{c}{n}
$$

As $n \to \infty$,

当 $n \to \infty$ 时，

$$
\frac{1}{n}K(\mathbf{X}) \to H(X)
$$

So entropy can be viewed as the asymptotic algorithmic description length per symbol.

因此，熵可以被看作“每个符号渐近的算法描述长度”。

---

# Chapter 3 Conditional Entropy  
# 第 3 章 条件熵

## 3.1 Joint Entropy  
## 3.1 联合熵

If $(X,Y)$ is a pair of discrete random variables with joint distribution $p(x,y)$, then the **joint entropy** is

如果 $(X,Y)$ 是一对离散随机变量，联合分布为 $p(x,y)$，则其**联合熵**定义为

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x,y)}
$$

Equivalently,

等价地，

$$
H(X,Y)=-\sum_{x,y} p(x,y)\log p(x,y)
$$

It measures the total uncertainty of the pair $(X,Y)$.

它衡量随机变量对 $(X,Y)$ 的总体不确定性。

It can also be written as

它也可以写成

$$
H(X,Y)=\mathbb{E}\left[\log \frac{1}{p(X,Y)}\right]
$$

---

## 3.2 Conditional Entropy  
## 3.2 条件熵

### Conditional entropy given a specific value of $Y$  
### 给定某个具体 $Y$ 值时的条件熵

For a fixed $y$, define

对一个固定的 $y$，定义

$$
H(X \mid Y=y)=\sum_x p(x \mid y)\log \frac{1}{p(x \mid y)}
$$

This is the uncertainty of $X$ when the value $Y=y$ is known.

它表示：当已知 $Y=y$ 时，$X$ 还剩下多少不确定性。

### Definition: Conditional Entropy  
### 定义：条件熵

The **conditional entropy** of $X$ given $Y$ is

$X$ 关于 $Y$ 的**条件熵**定义为

$$
H(X \mid Y)=\sum_y p(y)\,H(X \mid Y=y)
$$

Equivalently,

等价地，

$$
H(X \mid Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x \mid y)}
$$

It represents the average remaining uncertainty of $X$ after observing $Y$.

它表示：在观察到 $Y$ 之后，$X$ 平均还剩多少不确定性。

Also,

同时也可写成

$$
H(X \mid Y)=\mathbb{E}\left[\log \frac{1}{p(X \mid Y)}\right]
$$

---

## 3.3 Chain Rule for Entropy  
## 3.3 熵的链式法则

### Theorem  
### 定理

For any pair $(X,Y)$,

对任意随机变量对 $(X,Y)$，有

$$
H(X,Y)=H(Y)+H(X \mid Y)
$$

### Proof  
### 证明

Using

利用

$$
p(x,y)=p(y)p(x \mid y)
$$

we obtain

可得

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x,y)}
$$

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(y)p(x \mid y)}
$$

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(y)}+\sum_{x,y} p(x,y)\log \frac{1}{p(x \mid y)}
$$

$$
H(X,Y)=H(Y)+H(X \mid Y)
$$

Similarly,

类似地，也有

$$
H(X,Y)=H(X)+H(Y \mid X)
$$

More generally, for $X_1,\dots,X_n$,

更一般地，对于 $X_1,\dots,X_n$，

$$
H(X_1,\dots,X_n)=H(X_1)+H(X_2 \mid X_1)+\cdots+H(X_n \mid X_1,\dots,X_{n-1})
$$

This is called the **chain rule** for entropy.

这称为熵的**链式法则**。

---

## 3.4 Independence and Entropy  
## 3.4 独立性与熵

### Theorem  
### 定理

If $X$ and $Y$ are independent, then

如果 $X$ 和 $Y$ 相互独立，那么

$$
H(X,Y)=H(X)+H(Y)
$$

### Proof  
### 证明

If $X$ and $Y$ are independent, then

如果 $X$ 和 $Y$ 独立，则

$$
p(x,y)=p(x)p(y)
$$

Therefore,

因此

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x,y)}
$$

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x)p(y)}
$$

$$
H(X,Y)=\sum_{x,y} p(x,y)\log \frac{1}{p(x)}+\sum_{x,y} p(x,y)\log \frac{1}{p(y)}
$$

$$
H(X,Y)=H(X)+H(Y)
$$

### Corollary  
### 推论

If $X$ and $Y$ are independent, then

如果 $X$ 和 $Y$ 独立，那么

$$
H(X \mid Y)=H(X), \qquad H(Y \mid X)=H(Y)
$$

This matches intuition: knowing one variable gives no information about the other.

这与直觉一致：知道其中一个变量，并不会减少另一个变量的不确定性。

---

## 3.5 Information Never Hurts  
## 3.5 信息不会带来坏处

### Theorem  
### 定理

For any discrete random variables $X$ and $Y$,

对于任意离散随机变量 $X$ 和 $Y$，都有

$$
H(X \mid Y)\le H(X)
$$

This means that knowing $Y$ cannot increase our uncertainty about $X$.

这意味着：知道 $Y$ 不会增加我们对 $X$ 的不确定性。

### Proof  
### 证明

Consider

考虑

$$
H(X \mid Y)-H(X)
$$

Using the definitions,

由定义可得

$$
H(X \mid Y)-H(X)=\sum_{x,y} p(x,y)\log \frac{1}{p(x \mid y)}-\sum_x p(x)\log \frac{1}{p(x)}
$$

This can be rewritten as

它可以改写为

$$
H(X \mid Y)-H(X)=\sum_{x,y} p(x,y)\log \frac{p(x)p(y)}{p(x,y)}
$$

Define

定义

$$
Z(x,y)=\frac{p(x)p(y)}{p(x,y)}
$$

Then

则

$$
H(X \mid Y)-H(X)=\mathbb{E}[\log Z(X,Y)]
$$

By Jensen's inequality,

由 Jensen 不等式，

$$
\mathbb{E}[\log Z]\le \log \mathbb{E}[Z]
$$

Now

而

$$
\mathbb{E}[Z]=\sum_{x,y} p(x,y)\frac{p(x)p(y)}{p(x,y)}=\sum_{x,y} p(x)p(y)=1
$$

Hence

因此

$$
H(X \mid Y)-H(X)\le \log 1=0
$$

so

所以

$$
H(X \mid Y)\le H(X)
$$

---

## 3.6 Interpretation in Data Compression  
## 3.6 在数据压缩中的理解

Without any side information, describing $X$ requires about

如果没有任何边信息，那么描述 $X$ 大约需要

$$
H(X)
$$

bits on average.

个 bit 的平均码长。

If both encoder and decoder know another variable $Y$, then the average number of bits needed to describe $X$ drops to

如果编码器和解码器都知道另一个变量 $Y$，那么描述 $X$ 所需的平均 bit 数会下降到

$$
H(X \mid Y)
$$

Thus conditional entropy measures the cost of describing $X$ when side information is available.

因此，条件熵衡量的就是：在有边信息时，描述 $X$ 的代价。

---

## 3.7 Example with Side Information  
## 3.7 带边信息的例子

Suppose the joint distribution of $(X,Y)$ is

设 $(X,Y)$ 的联合分布为

| $Y \backslash X$ | 0 | 1 |
|---|---:|---:|
| 0 | 0.45 | 0.05 |
| 1 | 0.05 | 0.45 |

Then the marginal distribution of $X$ is

则 $X$ 的边缘分布为

$$
\Pr(X=0)=0.5, \qquad \Pr(X=1)=0.5
$$

so

因此

$$
H(X)=1 \text{ bit}
$$

Now define

现在定义

$$
Z=\begin{cases}0, & X=Y \\ 1, & X\ne Y \end{cases}
$$

Then

则

$$
X = Y \oplus Z
$$

where $\oplus$ denotes XOR.

其中 $\oplus$ 表示异或运算。

The distribution of $Z$ is

$Z$ 的分布为

$$
\Pr(Z=0)=0.9, \qquad \Pr(Z=1)=0.1
$$

Hence

因此

$$
H(Z)=-0.9\log_2 0.9 - 0.1\log_2 0.1 \approx 0.469 \text{ bits}
$$

So instead of directly describing $X$, we can describe $Z$ and recover $X$ from $Y$ and $Z$.

所以我们不必直接描述 $X$，而可以转而描述 $Z$，再利用 $Y$ 和 $Z$ 恢复 $X$。

Therefore,

因此

$$
H(X \mid Y)=H(Z)\approx 0.469 < 1 = H(X)
$$

This clearly illustrates that side information reduces the description cost.

这清楚地说明了：边信息能够降低描述代价。

---

## 3.8 Example: Shuffling a Deck  
## 3.8 例子：洗牌

Suppose $X$ represents the ordering of a deck of 52 cards, so it takes values in a set of size $52!$.

设 $X$ 表示一副 52 张扑克牌的排列，因此它有 $52!$ 种可能取值。

Let $T$ be a random shuffle, represented as a permutation. Then $TX$ is the shuffled deck.

设 $T$ 是一个随机洗牌操作，可表示为一个置换，那么 $TX$ 就是洗牌后的牌序。

We claim that

我们声称

$$
H(TX)\ge H(X)
$$

### Reason  
### 原因

First,

首先，

$$
H(TX)\ge H(TX \mid T)
$$

because conditioning cannot increase entropy.

因为条件化不会增加熵。

Second, for each fixed permutation $T=t$, the transformation $x \mapsto tx$ is one-to-one, so it merely relabels the possible values of $X$. Therefore,

其次，对于固定的置换 $T=t$，映射 $x \mapsto tx$ 是一一对应的，所以它只是重新标记了 $X$ 的取值，因此

$$
H(TX \mid T=t)=H(X \mid T=t)
$$

Averaging over $t$ gives

对 $t$ 取平均可得

$$
H(TX \mid T)=H(X \mid T)
$$

If $T$ is independent of $X$, then

如果 $T$ 与 $X$ 独立，那么

$$
H(X \mid T)=H(X)
$$

Combining these facts,

把这些结论合起来，

$$
H(TX)\ge H(TX \mid T)=H(X \mid T)=H(X)
$$

So random shuffling cannot reduce entropy.

因此随机洗牌不会降低熵。

---

# Summary  
# 总结

These three chapters introduce the basic language of information theory:

这三章介绍了信息论的基础语言：

- **Entropy** $H(X)$ measures the uncertainty of a random variable, or equivalently, the minimum average number of bits needed to describe it.  
  **熵** $H(X)$ 衡量随机变量的不确定性，也等价于描述它所需的最小平均比特数。

- **Joint entropy** $H(X,Y)$ measures the total uncertainty of two variables together.  
  **联合熵** $H(X,Y)$ 衡量两个变量合起来的总不确定性。

- **Conditional entropy** $H(X \mid Y)$ measures the remaining uncertainty of $X$ after $Y$ is known.  
  **条件熵** $H(X \mid Y)$ 衡量在已知 $Y$ 之后，$X$ 还剩多少不确定性。

- Knowing more information cannot hurt:  
  知道更多信息不会有坏处：

$$
H(X \mid Y)\le H(X)
$$

These concepts form the foundation for later topics such as mutual information, source coding, and channel coding.

这些概念构成了后续互信息、信源编码和信道编码等内容的基础。
