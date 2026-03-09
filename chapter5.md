# Chapter 5 Notes on Information Theory  
# 第 5 章 信息论笔记

---

# Chapter 5 Conditional Mutual Information  
# 第 5 章 条件互信息

## 5.1 Basics  
## 5.1 基础内容

### Definition: Conditional Mutual Information  
### 定义：条件互信息

For $(X,Y,Z) \sim p(x,y,z)$, the **conditional mutual information** is defined as

对于随机变量三元组 $(X,Y,Z) \sim p(x,y,z)$，**条件互信息**定义为

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)
$$

It can also be interpreted symmetrically as

它也可以对称地理解为

$$
I(X;Y \mid Z)=H(Y \mid Z)-H(Y \mid X,Z)
$$

This quantity measures how much additional information $Y$ provides about $X$ when $Z$ is already known.

这个量衡量的是：在已经知道 $Z$ 的前提下，$Y$ 还能额外提供多少关于 $X$ 的信息。

---

### Interpretation 1: Side Information in Compression  
### 理解 1：带边信息的压缩

$H(X \mid Z)$ is the minimum number of bits needed to describe $X$ when side information $Z$ is available at both the encoder and decoder.

$H(X \mid Z)$ 表示：当编码器和解码器都已知边信息 $Z$ 时，描述 $X$ 所需的最小平均 bit 数。

So

因此

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)
$$

means the reduction in the description cost of $X$ after additionally observing $Y$.

表示在已知 $Z$ 的前提下，再额外观察 $Y$ 后，描述 $X$ 的代价减少了多少。

---

### Interpretation 2: Communication through a Channel  
### 理解 2：带边信息的通信

If $Z$ is known to both the transmitter and the receiver, then

如果发送端和接收端都知道 $Z$，那么

$$
I(X;Y \mid Z)
$$

can be interpreted as the maximum number of bits that can be reliably communicated through the channel, conditioned on $Z$.

可以把它理解为：在给定边信息 $Z$ 的情况下，通过信道能够可靠传输的最大信息量。

---

### Important Note  
### 重要说明

Usually,

通常，

$$
H(X \mid Z)\le H(X)
$$

but it is **not** always true that

但是**并不总是有**

$$
I(X;Y \mid Z)\le I(X;Y)
$$

In fact, conditional mutual information can be either smaller or larger than ordinary mutual information.

实际上，条件互信息既可能比普通互信息小，也可能比普通互信息大。

---

### Example 1  
### 例 1

Let

设

$$
X \sim \text{Bern}(0.5)
$$

and suppose $Y=X$.

并且 $Y=X$。

Then clearly,

那么显然，

$$
I(X;Y)=1
$$

Now let

现在令

$$
Z=X
$$

Then

则

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)
$$

Since $Z$ already tells us everything about $X$, we have

由于 $Z$ 已经把关于 $X$ 的信息全部告诉我们了，所以

$$
H(X \mid Z)=0
$$

and also

并且

$$
H(X \mid Y,Z)=0
$$

Hence

因此

$$
I(X;Y \mid Z)=0
$$

So in this case, conditioning reduces the mutual information.

所以在这个例子中，条件化会使互信息变小。

---

### Example 2  
### 例 2

Suppose

设

- $X \sim \text{Bern}(0.5)$
- $Z \sim \text{Bern}(0.1)$
- $X$ and $Z$ are independent
- $Y = X \oplus Z$

其中 $\oplus$ 表示异或运算。

Then without knowing $Z$, the channel from $X$ to $Y$ is noisy, so

那么在不知道 $Z$ 的情况下，从 $X$ 到 $Y$ 的信道是有噪声的，因此

$$
I(X;Y)=H(Y)-H(Y \mid X)=H(Y)-H(Z)
$$

In the lecture notes, this value is approximately

在讲义里，这个值大约为

$$
I(X;Y)\approx 0.53
$$

However, if $Z$ is known to both sides, then the receiver can subtract the noise $Z$ from $Y$, so the channel becomes noiseless.

但是如果通信双方都知道 $Z$，那么接收端就可以把噪声 $Z$ 从 $Y$ 中“减掉”，于是信道就变成无噪声信道。

Therefore,

因此

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)=H(X)=1
$$

So in this example,

所以在这个例子中，

$$
I(X;Y \mid Z)>I(X;Y)
$$

Conditioning on side information can increase mutual information.

知道边信息之后，条件互信息反而会变大。

---

### Theorem  
### 定理

If $X$ and $Z$ are independent, then

如果 $X$ 和 $Z$ 相互独立，那么

$$
I(X;Y \mid Z)\ge I(X;Y)
$$

### Proof  
### 证明

We have

我们有

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)
$$

Since $X$ and $Z$ are independent,

由于 $X$ 与 $Z$ 独立，

$$
H(X \mid Z)=H(X)
$$

Also, conditioning cannot increase entropy, so

并且条件化不会增加熵，所以

$$
H(X \mid Y,Z)\le H(X \mid Y)
$$

Thus

于是

$$
I(X;Y \mid Z)=H(X)-H(X \mid Y,Z)\ge H(X)-H(X \mid Y)=I(X;Y)
$$

---

## 5.2 Chain Rule for Mutual Information  
## 5.2 互信息的链式法则

### Theorem  
### 定理

For $(X_1,\dots,X_n,Y)\sim p(x_1,\dots,x_n,y)$,

对于 $(X_1,\dots,X_n,Y)\sim p(x_1,\dots,x_n,y)$，有

$$
I(X_1,\dots,X_n;Y)=I(X_1;Y)+I(X_2;Y \mid X_1)+\cdots+I(X_n;Y \mid X_1,\dots,X_{n-1})
$$

This is the **chain rule for mutual information**.

这称为**互信息的链式法则**。

---

### Proof  
### 证明

Start with

从下面开始：

$$
I(X_1,\dots,X_n;Y)=H(X_1,\dots,X_n)-H(X_1,\dots,X_n \mid Y)
$$

Expand the first entropy by the entropy chain rule:

对第一个熵用熵的链式法则展开：

$$
H(X_1,\dots,X_n)=H(X_1)+H(X_2 \mid X_1)+\cdots+H(X_n \mid X_1,\dots,X_{n-1})
$$

Similarly,

同理，

$$
H(X_1,\dots,X_n \mid Y)=H(X_1 \mid Y)+H(X_2 \mid X_1,Y)+\cdots+H(X_n \mid X_1,\dots,X_{n-1},Y)
$$

Subtracting term by term gives

逐项相减得到

$$
I(X_1,\dots,X_n;Y)=I(X_1;Y)+I(X_2;Y \mid X_1)+\cdots+I(X_n;Y \mid X_1,\dots,X_{n-1})
$$

---

### Interpretation: Multiple Access Channel  
### 理解：多址信道

Suppose $X_1,\dots,X_n$ all want to communicate with the same receiver $Y$ through a common channel.

假设 $X_1,\dots,X_n$ 都想通过同一个信道向接收端 $Y$ 发送信息。

If we treat the whole vector

如果把整个向量

$$
\mathbf{X}=(X_1,\dots,X_n)
$$

as one big input, then the total amount of information that can be conveyed to $Y$ is

看成一个整体输入，那么能够传给 $Y$ 的总信息量就是

$$
I(\mathbf{X};Y)=I(X_1,\dots,X_n;Y)
$$

The chain rule says that this total information can be decomposed user by user.

互信息链式法则说明：这个总信息量可以按用户逐个分解。

---

### Successive Decoding Interpretation  
### 逐次解码的理解

To transmit $(X_1,\dots,X_n)$ to $Y$:

为了把 $(X_1,\dots,X_n)$ 传给 $Y$：

1. Decode $X_1$ first at rate $I(X_1;Y)$, treating $X_2,\dots,X_n$ as noise.  
   先以速率 $I(X_1;Y)$ 解码 $X_1$，把 $X_2,\dots,X_n$ 当成噪声。

2. Once $X_1$ is known, subtract its effect from $Y$, then decode $X_2$ at rate $I(X_2;Y \mid X_1)$.  
   当 $X_1$ 已知后，把它对 $Y$ 的影响去掉，再以速率 $I(X_2;Y \mid X_1)$ 解码 $X_2$。

3. Continue in this way.  
   后面依此类推。

So the total rate becomes

所以总速率就是

$$
I(X_1,\dots,X_n;Y)=I(X_1;Y)+I(X_2;Y \mid X_1)+\cdots+I(X_n;Y \mid X_1,\dots,X_{n-1})
$$

---

## 5.3 Stochastic Process and Markov Chain  
## 5.3 随机过程与马尔可夫链

### Definition: Markov Chain  
### 定义：马尔可夫链

We say

我们称

$$
X \to Y \to Z
$$

forms a **Markov chain** if

构成一个**马尔可夫链**，如果

$$
p(x,y,z)=p(x)\,p(y \mid x)\,p(z \mid y)
$$

Intuitively, $Z$ depends on $X$ only through $Y$.

直观地说，$Z$ 对 $X$ 的依赖只能通过 $Y$ 来传递。

So the information flow is

因此信息流是

$$
X \to Y \to Z
$$

That means once $Y$ is given, $X$ no longer directly influences $Z$.

这意味着一旦 $Y$ 已知，$X$ 就不再直接影响 $Z$。

---

### Theorem 1  
### 定理 1

If

如果

$$
X \to Y \to Z
$$

is a Markov chain, then

是马尔可夫链，那么

$$
Z \to Y \to X
$$

is also a Markov chain.

也是一个马尔可夫链。

### Proof  
### 证明

Starting from

从

$$
p(x,y,z)=p(x)\,p(y \mid x)\,p(z \mid y)
$$

we can rewrite it as

可把它改写为

$$
p(x,y,z)=p(x,y)\,p(z \mid y)
$$

Then

于是

$$
p(x,y,z)=p(x \mid y)\,p(y)\,p(z \mid y)
$$

Also,

又因为

$$
p(y,z)=p(y)\,p(z \mid y)
$$

so we obtain

所以可得

$$
p(x,y,z)=p(x \mid y)\,p(y \mid z)\,p(z)
$$

Thus

因此

$$
Z \to Y \to X
$$

is also Markov.

也满足马尔可夫性。

---

### Theorem 2  
### 定理 2

For a Markov chain

对于马尔可夫链

$$
X \to Y \to Z
$$

$X$ and $Z$ are conditionally independent given $Y$.

在给定 $Y$ 的条件下，$X$ 和 $Z$ 条件独立。

That is,

也就是

$$
p(x,z \mid y)=p(x \mid y)\,p(z \mid y)
$$

### Proof  
### 证明

By definition,

由定义，

$$
p(x,y,z)=p(x)\,p(y \mid x)\,p(z \mid y)
$$

So

因此

$$
p(x,z \mid y)=\frac{p(x,y,z)}{p(y)}
$$

Substituting gives

代入得到

$$
p(x,z \mid y)=\frac{p(x)\,p(y \mid x)\,p(z \mid y)}{p(y)}
$$

But

而

$$
p(x \mid y)=\frac{p(x)\,p(y \mid x)}{p(y)}
$$

Therefore,

因此

$$
p(x,z \mid y)=p(x \mid y)\,p(z \mid y)
$$

So $X$ and $Z$ are conditionally independent once $Y$ is known.

所以一旦给定 $Y$，$X$ 和 $Z$ 就条件独立了。

---

## 5.4 Conditional Mutual Information in a Markov Chain  
## 5.4 马尔可夫链中的条件互信息

### Theorem  
### 定理

For a Markov chain

对于马尔可夫链

$$
X \to Y \to Z
$$

we have

有

$$
I(X;Y \mid Z)\le I(X;Y)
$$

### Proof  
### 证明

By the chain rule for mutual information,

由互信息的链式法则，

$$
I(X;Y,Z)=I(X;Z)+I(X;Y \mid Z)
$$

On the other hand,

另一方面，

$$
I(X;Y,Z)=I(X;Y)+I(X;Z \mid Y)
$$

For the Markov chain $X \to Y \to Z$, once $Y$ is known, $Z$ carries no additional information about $X$, so

对于马尔可夫链 $X \to Y \to Z$，一旦 $Y$ 已知，$Z$ 就不再携带额外的关于 $X$ 的信息，因此

$$
I(X;Z \mid Y)=0
$$

Hence

所以

$$
I(X;Z)+I(X;Y \mid Z)=I(X;Y)
$$

Since mutual information is nonnegative,

由于互信息总是非负的，

$$
I(X;Z)\ge 0
$$

we get

于是得到

$$
I(X;Y \mid Z)\le I(X;Y)
$$

---

## 5.5 Data Processing Inequality  
## 5.5 数据处理不等式

### Theorem: Data Processing Inequality  
### 定理：数据处理不等式

For a Markov chain

对于马尔可夫链

$$
X \to Y \to Z
$$

we have

有

$$
I(X;Y)\ge I(X;Z)
$$

### Proof  
### 证明

Recall that for the Markov chain,

回忆上面已经得到，对于这个马尔可夫链，

$$
I(X;Z)+I(X;Y \mid Z)=I(X;Y)
$$

Since

由于

$$
I(X;Y \mid Z)\ge 0
$$

it follows that

所以

$$
I(X;Z)\le I(X;Y)
$$

This is the **data processing inequality**.

这就是**数据处理不等式**。

---

### Interpretation  
### 直观解释

Information can only be lost through further processing; it cannot be increased.

信息在进一步处理的过程中只能损失，不能凭空增加。

If $X$ talks to $Y$, and then $Y$ talks to $Z$, then $Z$ cannot know more about $X$ than $Y$ does.

如果信息先从 $X$ 传到 $Y$，再从 $Y$ 传到 $Z$，那么 $Z$ 不可能比 $Y$ 更了解 $X$。

So

因此

$$
I(X;Z)\le I(X;Y)
$$

---

### Extra Remark  
### 额外说明

The lecture note also states another inequality:

讲义最后还写了另一个不等式：

$$
I(Y;Z)\le I(X;Z)
$$

for the Markov chain

对应马尔可夫链

$$
X \to Y \to Z
$$

This can be understood as another consequence of the information flow structure: once information about $X$ is passed through $Y$ and then to $Z$, the dependence patterns are constrained by the Markov property.

它可以理解为信息流结构的另一个结果：当关于 $X$ 的信息先经过 $Y$ 再传到 $Z$ 时，由于马尔可夫性质，变量之间的依赖关系会受到严格约束。

---

# Summary  
# 总结

This chapter introduces conditional mutual information and its role in channels with side information.

本章介绍了条件互信息，以及它在带边信息信道中的作用。

- **Conditional mutual information**  
  **条件互信息**

$$
I(X;Y \mid Z)=H(X \mid Z)-H(X \mid Y,Z)
$$

measures how much additional information $Y$ provides about $X$ when $Z$ is already known.  
衡量在已知 $Z$ 时，$Y$ 还能为 $X$ 提供多少额外信息。

- The **chain rule for mutual information** decomposes total information into successive pieces.  
  **互信息链式法则**可以把总信息量分解成逐步解码的信息量之和。

- A **Markov chain**  
  **马尔可夫链**

$$
X \to Y \to Z
$$

means that $Z$ depends on $X$ only through $Y$.  
表示 $Z$ 对 $X$ 的依赖只能通过 $Y$ 传递。

- In a Markov chain, $X$ and $Z$ are conditionally independent given $Y$.  
  在马尔可夫链中，给定 $Y$ 后，$X$ 与 $Z$ 条件独立。

- The **data processing inequality**

$$
I(X;Y)\ge I(X;Z)
$$

says that processing cannot increase information.  
说明“处理”不会增加信息量。

So this chapter builds a bridge from mutual information to information flow in stochastic systems.

因此，本章把互信息进一步推广到了随机系统中的信息流分析。
