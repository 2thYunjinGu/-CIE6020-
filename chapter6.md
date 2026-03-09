# Chapter 6 Notes on Information Theory  
# 第 6 章 信息论笔记

---

# Chapter 6 Three-Party Mutual Information  
# 第 6 章 三方互信息

## 6.1 Basics  
## 6.1 基础内容

### Definition: Three-Party Mutual Information  
### 定义：三方互信息

For $(X,Y,Z) \sim p(x,y,z)$, the **three-party mutual information** is defined as

对于随机变量三元组 $(X,Y,Z) \sim p(x,y,z)$，**三方互信息**定义为

$$
I(X;Y;Z)=I(X;Y)-I(X;Y \mid Z)
$$

This quantity measures how the shared information between $X$ and $Y$ changes after conditioning on $Z$.

这个量衡量的是：在给定 $Z$ 之后，$X$ 和 $Y$ 之间共享信息发生了怎样的变化。

---

### Equivalent Entropy Form  
### 熵形式的等价表达

The lecture notes give the following equivalent form:

讲义中给出了下面这个等价表达式：

$$
I(X;Y;Z)=H(X)+H(Y)+H(Z)-H(X,Y)-H(Y,Z)-H(X,Z)+H(X,Y,Z)
$$

This formula is symmetric in $X$, $Y$, and $Z$.

这个公式对 $X$、$Y$、$Z$ 是对称的。

---

### Other Equivalent Forms  
### 其他等价形式

We also have

我们还有

$$
I(X;Y;Z)=I(X;Z)-I(X;Z \mid Y)
$$

and

以及

$$
I(X;Y;Z)=I(Y;Z)-I(Y;Z \mid X)
$$

So the three-party mutual information is fully symmetric:

因此，三方互信息是完全对称的：

$$
I(X;Y;Z)=I(Y;X;Z)=I(X;Z;Y)=\cdots
$$

---

### Interpretation  
### 直观理解

The lecture uses Venn-diagram style pictures to interpret three-party mutual information.

讲义用类似韦恩图的方式来解释三方互信息。

- $I(X;Y)$ is the overlap between the information of $X$ and $Y$  
  $I(X;Y)$ 是 $X$ 与 $Y$ 信息的重叠部分

- $I(X;Y \mid Z)$ is the overlap between $X$ and $Y$ after $Z$ is already known  
  $I(X;Y \mid Z)$ 是在已知 $Z$ 后，$X$ 与 $Y$ 的重叠信息

- Therefore, $I(X;Y;Z)$ describes the common interaction among all three variables  
  因此，$I(X;Y;Z)$ 描述的是三个变量之间共同的交互部分

---

### Important Note  
### 重要说明

Ordinary mutual information always satisfies

普通互信息总满足

$$
I(X;Y)\ge 0
$$

but three-party mutual information does **not** have to be nonnegative.

但是三方互信息 **不一定非负**。

That is,

也就是说，

$$
I(X;Y;Z)
$$

can be positive, zero, or negative.

既可能为正，也可能为零，还可能为负。

This is an important difference from ordinary mutual information.

这是它和普通互信息的重要区别之一。

---

## 6.2 Information-Theoretic Security  
## 6.2 信息论安全

### Communication Model  
### 通信模型

Let

设

- $X$ = plaintext  
  $X$ = 明文
- $K$ = key  
  $K$ = 密钥
- $Y$ = ciphertext  
  $Y$ = 密文

Encryption is represented by

加密过程表示为

$$
Y=f(X,K)
$$

Decryption is represented by

解密过程表示为

$$
\hat{X}=g(Y,K)
$$

So the legitimate receiver, who knows both $Y$ and $K$, can recover $X$.

因此，合法接收者在知道 $Y$ 和 $K$ 的情况下，可以恢复 $X$。

But an eavesdropper only sees $Y$ and does not know $K$.

但窃听者只能看到 $Y$，并不知道 $K$。

---

### Definition: Information-Theoretic Security  
### 定义：信息论安全

The lecture states that a scheme is information-theoretically secure if it satisfies two conditions.

讲义指出，一个方案若满足下面两个条件，就称为信息论安全。

#### Condition 1  
#### 条件 1

$$
I(X;Y)=0
$$

This means that without knowing the key $K$, one can learn **nothing** about $X$ from the ciphertext $Y$.

这表示：在不知道密钥 $K$ 的情况下，仅从密文 $Y$ 中**什么都学不到**关于明文 $X$ 的信息。

#### Condition 2  
#### 条件 2

$$
H(X \mid Y,K)=0
$$

This means that when both the ciphertext $Y$ and the key $K$ are available, one can recover **everything** about $X$.

这表示：当密文 $Y$ 和密钥 $K$ 都可用时，就能完全恢复明文 $X$。

---

## 6.3 One-Time Pad  
## 6.3 一次一密

### Example: Vernam's One-Time Pad  
### 例子：Vernam 一次一密

The lecture gives the one-time pad scheme proposed by Vernam in 1917.

讲义给出了 Vernam 在 1917 年提出的一次一密方案。

Assume

设

$$
X \sim \text{Bern}(1/2)
$$

and let the key be

并令密钥

$$
K \sim \text{Bern}(1/2)
$$

independently of $X$.

且与 $X$ 独立。

The encryption rule is

加密规则为

$$
Y=f(X,K)=X \oplus K
$$

and the decryption rule is

解密规则为

$$
\hat{X}=g(Y,K)=Y \oplus K
$$

where $\oplus$ denotes XOR.

其中 $\oplus$ 表示异或运算。

---

### Why Decryption Works  
### 为什么可以正确解密

Because XOR satisfies

因为异或满足

$$
(X \oplus K)\oplus K = X
$$

we can recover the original message exactly:

所以我们可以精确恢复原消息：

$$
\hat{X}=Y \oplus K=(X \oplus K)\oplus K=X
$$

Hence

因此

$$
H(X \mid Y,K)=0
$$

So the receiver can decode perfectly.

因此接收端可以无误解码。

---

### Why It Is Perfectly Secret  
### 为什么它具有完美保密性

Since $K$ is uniformly random and independent of $X$, the ciphertext

由于 $K$ 是均匀随机并且与 $X$ 独立，密文

$$
Y=X \oplus K
$$

is also uniformly random.

也会是均匀随机的。

Thus the distribution of $Y$ does not reveal anything about $X$.

因此，$Y$ 的分布不会泄露任何关于 $X$ 的信息。

So

于是

$$
I(X;Y)=0
$$

This means the one-time pad achieves perfect secrecy.

这意味着一次一密实现了完美保密。

---

### Example with Bit Strings  
### 比特串例子

The lecture gives the following example:

讲义给出了如下例子：

Suppose

设

$$
X=01100111\cdots
$$

and

以及

$$
K=11010100\cdots
$$

Then the ciphertext is

则密文为

$$
Y=X \oplus K = 10110011\cdots
$$

And after decryption,

解密后，

$$
\hat{X}=Y \oplus K = 01100111\cdots
$$

So the original plaintext is recovered exactly.

因此原始明文被精确恢复。

---

### Practical Limitation  
### 实际局限

The one-time pad requires the key $K$ to be as long as the message $X$.

一次一密要求密钥 $K$ 的长度与消息 $X$ 一样长。

Therefore, it is **not practical** in many real systems.

因此，它在很多真实系统中**并不实用**。

The lecture then raises the natural question:

讲义随后提出一个自然问题：

Can we do better?

我们能不能做得更好？

---

## 6.4 Shannon's Impossibility Result  
## 6.4 Shannon 的不可能性结论

### Answer  
### 回答

The answer is **no**.

答案是：**不能**。

Shannon proved in 1949 that for a perfectly secure scheme, the key cannot be shorter than the message.

Shannon 在 1949 年证明：对于完美保密方案，密钥不可能比消息更短。

---

### Main Conclusion  
### 主要结论

For a perfectly secure encryption system, we must have

对于完美保密加密系统，必须有

$$
H(X)\le H(K)
$$

So the uncertainty of the key must be at least as large as the uncertainty of the plaintext.

也就是说，密钥的不确定性至少要和明文的不确定性一样大。

In other words, the key cannot be shorter than the message in an information-theoretic sense.

换句话说，从信息论角度看，密钥不能比消息更短。

---

### Proof Idea from the Lecture  
### 讲义中的证明思路

The lecture uses a three-circle entropy diagram involving $X$, $Y$, and $K$.

讲义使用了一个关于 $X$、$Y$、$K$ 的三圆熵图来说明这个结论。

The core assumptions are:

核心假设是：

1. Perfect secrecy:  
   完美保密：

$$
I(X;Y)=0
$$

2. Perfect decoding:  
   完美解码：

$$
H(X \mid Y,K)=0
$$

From the entropy diagram, the lecture derives that

通过熵图分析，讲义推出

$$
H(X)\le H(K)
$$

This means the key entropy must be at least the message entropy.

这意味着密钥熵至少不能小于消息熵。

---

### Intuition  
### 直观理解

If the key had less uncertainty than the message, then the ciphertext could not both:

如果密钥的不确定性小于消息，那么密文就不可能同时满足：

- hide everything about the plaintext from an eavesdropper  
  对窃听者隐藏关于明文的一切信息

- and still allow the receiver to recover the plaintext exactly  
  同时又让合法接收者精确恢复明文

So perfect secrecy fundamentally requires a key at least as large as the message itself.

所以，完美保密从根本上要求密钥至少和消息一样大。

---

## 6.5 Connection to Three-Party Mutual Information  
## 6.5 与三方互信息的联系

This chapter connects the idea of secrecy with the interaction among three variables:

这一章把保密性和三个变量之间的交互联系起来：

- plaintext $X$  
  明文 $X$
- ciphertext $Y$  
  密文 $Y$
- key $K$  
  密钥 $K$

The security condition

安全条件

$$
I(X;Y)=0
$$

says that the ciphertext alone reveals nothing about the plaintext.

表示仅看密文本身，不会泄露任何关于明文的信息。

The recoverability condition

可恢复条件

$$
H(X \mid Y,K)=0
$$

says that ciphertext plus key completely determine the plaintext.

表示“密文 + 密钥”能够完全确定明文。

So the key acts as the missing piece of information that turns useless ciphertext into meaningful plaintext.

因此，密钥就像那块缺失的信息拼图：它把“单独看没有意义的密文”变成“可完全恢复的明文”。

---

# Summary  
# 总结

This chapter introduces two related themes.

本章介绍了两个彼此相关的主题。

### 1. Three-Party Mutual Information  
### 1. 三方互信息

The three-party mutual information is defined by

三方互信息定义为

$$
I(X;Y;Z)=I(X;Y)-I(X;Y \mid Z)
$$

and can also be written in symmetric entropy form.

并且还可以写成对称的熵表达式。

Unlike ordinary mutual information, it may be positive, zero, or negative.

与普通互信息不同，它可以为正、为零、也可以为负。

### 2. Information-Theoretic Security  
### 2. 信息论安全

A perfectly secure encryption scheme should satisfy

一个完美保密加密方案应满足

$$
I(X;Y)=0
$$

and

以及

$$
H(X \mid Y,K)=0
$$

The one-time pad satisfies these conditions, but it requires a key as long as the message.

一次一密满足这些条件，但它要求密钥与消息一样长。

Shannon's theorem shows that this is unavoidable:

Shannon 定理表明，这一点是不可避免的：

$$
H(X)\le H(K)
$$

So perfect secrecy always requires a sufficiently large key.

因此，完美保密总是要求足够大的密钥。
