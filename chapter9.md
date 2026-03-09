# Chapter 9 Notes on Information Theory  
# 第 9 章 信息论笔记

---

# Chapter 9 Data Compression  
# 第 9 章 数据压缩

## 9.1 Variable-Length Code  
## 9.1 变长编码

In Chapter 8, we used AEP to compress long i.i.d. sequences.

在第 8 章中，我们使用 AEP 来压缩长的独立同分布序列。

Typical sequences were assigned short descriptions, while non-typical sequences were assigned longer descriptions.

典型序列被赋予较短的描述，而非典型序列则被赋予较长的描述。

This idea is essentially a **fixed-length block coding** strategy for long sequences.

这个思路本质上是一种针对长序列的**定长分组编码**策略。

However, such a codebook can be huge and impractical.

但是，这样的码书可能会非常大，在实际中不够方便。

So we now study **variable-length codes** for single symbols.

因此，我们现在研究针对单个符号的**变长编码**。

---

### Definition: Variable-Length Code  
### 定义：变长编码

A **variable-length code** is a mapping

**变长编码**是一个映射

$$
c:\mathcal{X}\to \{0,1\}^*
$$

that maps each source symbol $x\in\mathcal{X}$ to a binary string.

它把每个源符号 $x\in\mathcal{X}$ 映射成一个二进制串。

Here $\{0,1\}^*$ denotes the set of all finite binary strings.

其中 $\{0,1\}^*$ 表示所有有限长度二进制串的集合。

We clearly require that different symbols have different codewords:

显然，我们至少要求不同符号对应不同的码字：

$$
c(x_1)\ne c(x_2), \qquad \forall x_1\ne x_2
$$

But this condition alone is **not enough** to guarantee correct decoding of sequences.

但这个条件本身**还不足以**保证对符号序列进行正确解码。

---

### Example: Not Uniquely Decodable  
### 例子：不可唯一解码

Suppose

设

$$
\mathcal{X}=\{a,b,c,d\}
$$

and define the code

并定义编码

- $c(a)=0$
- $c(b)=010$
- $c(c)=01$
- $c(d)=10$

Then

那么

$$
c(abd)=c(a)c(b)c(d)=0\,010\,10=001010
$$

Also,

同时，

$$
c(acca)=c(a)c(c)c(c)c(a)=0\,01\,01\,0=001010
$$

and

以及

$$
c(aadd)=c(a)c(a)c(d)c(d)=0\,0\,10\,10=001010
$$

So the same binary string

因此同一个二进制串

$$
001010
$$

can correspond to multiple different source sequences.

可能对应多个不同的源序列。

Hence this code is **not uniquely decodable**.

因此这个码并不是**唯一可译码**的。

---

### Definition: Uniquely Decodable Code  
### 定义：唯一可译码

A code $c$ is called **uniquely decodable (U.D.)** if whenever

如果对于任意两个不同的源序列，只要满足

$$
(x_1,\dots,x_n)\ne (y_1,\dots,y_m)
$$

we always have

就总有

$$
c(x_1)\cdots c(x_n)\ne c(y_1)\cdots c(y_m)
$$

then the code is called **uniquely decodable**.

那么这个编码就称为**唯一可译码**。

That is, no two different source sequences are mapped to the same binary string.

也就是说，不会有两个不同的源序列被映射成同一个二进制串。

---

## 9.2 Prefix-Free Code  
## 9.2 前缀码

### Definition: Prefix-Free Code  
### 定义：前缀码

A code is called **prefix-free** if no codeword is a prefix of another codeword.

如果一个码满足：任意一个码字都不是另一个码字的前缀，那么这个码称为**前缀码**。

In other words, once we finish reading one codeword, we know immediately where it ends.

换句话说，当我们读完一个码字时，就能立刻知道它已经结束了。

---

### Theorem  
### 定理

Every prefix-free code is uniquely decodable.

任何前缀码都是唯一可译码的。

Symbolically,

符号化地说，

$$
\text{prefix-free} \Rightarrow \text{U.D.}
$$

### Proof Idea  
### 证明思路

Suppose a prefix-free code were not uniquely decodable.

假设一个前缀码不是唯一可译码的。

Then there would exist two different symbol sequences whose concatenated codewords are identical.

那么就会存在两个不同的符号序列，它们拼接后的码字串完全相同。

Looking at the first point where the two decompositions differ, one codeword must be a prefix of another.

观察这两个分解第一次出现差异的位置，就会发现某个码字必须是另一个码字的前缀。

This contradicts the prefix-free property.

这与前缀码定义矛盾。

Therefore, prefix-free implies uniquely decodable.

因此，前缀码一定唯一可译。

---

### Important Note  
### 重要说明

The converse is **not** true.

反过来则**不成立**。

That is,

也就是说，

$$
\text{U.D.} \centernot\Rightarrow \text{prefix-free}
$$

There exist codes that are uniquely decodable but not prefix-free.

确实存在一些码，它们是唯一可译的，但不是前缀码。

---

### Example Table  
### 例子表格

The lecture gives three examples over $\mathcal{X}=\{a,b,c,d\}$.

讲义给出了定义在 $\mathcal{X}=\{a,b,c,d\}$ 上的三类例子。

#### 1. Not uniquely decodable  
#### 1. 不是唯一可译码

- $a \to 0$
- $b \to 010$
- $c \to 01$
- $d \to 10$

This is the earlier counterexample.

这就是前面那个反例。

#### 2. Prefix-free  
#### 2. 前缀码

- $a \to 0$
- $b \to 10$
- $c \to 110$
- $d \to 111$

No codeword is a prefix of another.

任一代码字都不是另一个代码字的前缀。

So this code is prefix-free, and hence uniquely decodable.

因此它是前缀码，也就必然唯一可译。

#### 3. Uniquely decodable but not prefix-free  
#### 3. 唯一可译但不是前缀码

- $a \to 10$
- $b \to 00$
- $c \to 11$
- $d \to 110$

Here the code is uniquely decodable, but not prefix-free, because

这里这个码是唯一可译的，但不是前缀码，因为

$$
11
$$

is a prefix of

的确是

$$
110
$$

的前缀。

---

## 9.3 Kraft's Inequality  
## 9.3 Kraft 不等式

Let the codeword length of symbol $i$ be

记符号 $i$ 的码字长度为

$$
l_i = \ell(c(i))
$$

where $\ell(c(i))$ denotes the length of the codeword $c(i)$.

其中 $\ell(c(i))$ 表示码字 $c(i)$ 的长度。

---

### Theorem: Kraft's Inequality  
### 定理：Kraft 不等式

There exists a prefix-free binary code with lengths $l_1,\dots,l_M$ if and only if

存在一个码长分别为 $l_1,\dots,l_M$ 的二元前缀码，当且仅当

$$
\sum_{i=1}^M 2^{-l_i}\le 1
$$

This is called **Kraft's inequality**.

这称为 **Kraft 不等式**。

---

### Proof Idea Using a Binary Tree  
### 用二叉树理解证明

Build a full binary tree of height

构造一棵高度为

$$
l_{\max}=\max_i l_i
$$

的满二叉树。

A codeword of length $l_i$ corresponds to a node at depth $l_i$.

一个长度为 $l_i$ 的码字，对应这棵树中深度为 $l_i$ 的某个节点。

If the code is prefix-free, then no codeword can be an ancestor of another codeword.

如果编码是前缀码，那么任一代码字都不能成为另一个代码字的祖先。

So each codeword occupies its own disjoint subtree.

因此，每个码字都对应一个互不重叠的子树。

A codeword of length $l_i$ has

一个长度为 $l_i$ 的码字，对应的子树中有

$$
2^{l_{\max}-l_i}
$$

leaves at depth $l_{\max}$.

个叶子节点。

Thus the total number of leaves required is

所以总共需要的叶子数为

$$
\sum_{i=1}^M 2^{l_{\max}-l_i}
$$

But the full binary tree has only

但整棵满二叉树总共只有

$$
2^{l_{\max}}
$$

leaves.

个叶子。

Hence we must have

因此必须满足

$$
\sum_{i=1}^M 2^{l_{\max}-l_i}\le 2^{l_{\max}}
$$

Dividing both sides by $2^{l_{\max}}$ gives

两边同时除以 $2^{l_{\max}}$，得到

$$
\sum_{i=1}^M 2^{-l_i}\le 1
$$

This proves the necessity of Kraft's inequality.

这就证明了 Kraft 不等式的必要性。

The sufficiency direction says that whenever this inequality holds, we can actually construct a prefix-free code with those lengths.

而充分性则说明：只要这个不等式成立，我们就真的能构造出相应码长的前缀码。

---

## 9.4 McMillan's Inequality  
## 9.4 McMillan 不等式

Since every prefix-free code is uniquely decodable, one might think the existence condition for uniquely decodable codes could be weaker.

由于每个前缀码都唯一可译，人们可能会以为：唯一可译码的存在条件会比前缀码更宽松。

Surprisingly, the answer is no.

但令人惊讶的是，答案是否定的。

---

### Theorem: McMillan's Inequality  
### 定理：McMillan 不等式

There exists a uniquely decodable binary code with lengths $l_1,\dots,l_M$ if and only if

存在一个码长分别为 $l_1,\dots,l_M$ 的二元唯一可译码，当且仅当

$$
\sum_{i=1}^M 2^{-l_i}\le 1
$$

So uniquely decodable codes satisfy exactly the same length constraint as prefix-free codes.

也就是说，唯一可译码满足的码长约束与前缀码完全一样。

---

### Proof Idea  
### 证明思路

Let

设

$$
\mathcal{X}=\{1,\dots,M\}
$$

and consider all length-$n$ source sequences

并考虑所有长度为 $n$ 的源序列

$$
x^n=(x_1,\dots,x_n)
$$

Then

那么

$$
\sum_{x^n\in\mathcal{X}^n} 2^{-\ell(c(x^n))}
=
\sum_{x^n\in\mathcal{X}^n} 2^{-[\ell(c(x_1))+\cdots+\ell(c(x_n))]}
$$

Since the terms factor,

由于这些项可以分解，

$$
\sum_{x^n\in\mathcal{X}^n} 2^{-\ell(c(x^n))}
=
\left(\sum_{x\in\mathcal{X}}2^{-\ell(c(x))}\right)^n
$$

This is the key algebraic step.

这是证明中的关键代数步骤。

---

### Another Way to Count  
### 另一种计数方式

Now group all source sequences $x^n$ according to their total codeword length.

现在按总码长对所有 $x^n$ 分组。

Let

令

$$
\beta_k = \#\{x^n : \ell(c(x^n))=k\}
$$

Then

那么

$$
\sum_{x^n\in\mathcal{X}^n} 2^{-\ell(c(x^n))}
=
\sum_{k=1}^{nl_{\max}} \beta_k\,2^{-k}
$$

where

其中

$$
l_{\max}=\max_x \ell(c(x))
$$

Because the code is uniquely decodable, each distinct source sequence must map to a different binary string.

由于编码是唯一可译的，每个不同的源序列必须映射成不同的二进制串。

For codewords of total length $k$, there are at most

而长度为 $k$ 的二进制串总共最多只有

$$
2^k
$$

possible binary strings.

个。

So

因此

$$
\beta_k\le 2^k
$$

Hence

于是

$$
\sum_{x^n\in\mathcal{X}^n} 2^{-\ell(c(x^n))}
=
\sum_{k=1}^{nl_{\max}} \beta_k\,2^{-k}
\le
\sum_{k=1}^{nl_{\max}} 1
=
nl_{\max}
$$

Combining this with the earlier factorization gives

把它和前面的分解式结合起来，得到

$$
\left(\sum_{x\in\mathcal{X}}2^{-\ell(c(x))}\right)^n \le nl_{\max}
$$

Taking the $n$-th root,

两边取 $n$ 次方根，

$$
\sum_{x\in\mathcal{X}}2^{-\ell(c(x))}\le (nl_{\max})^{1/n}
$$

Letting $n\to\infty$ yields

让 $n\to\infty$，可得

$$
\sum_{x\in\mathcal{X}}2^{-\ell(c(x))}\le 1
$$

This proves the necessity of McMillan's inequality.

这就证明了 McMillan 不等式的必要性。

The sufficiency direction follows because any length set satisfying this inequality can be realized by a prefix-free code via Kraft's inequality, and every prefix-free code is uniquely decodable.

而充分性来自 Kraft 不等式：只要这个条件成立，就能构造出前缀码；而前缀码一定唯一可译。

---

## 9.5 D-ary McMillan Theorem  
## 9.5 D 元 McMillan 定理

So far we focused on binary coding, where the code alphabet is $\{0,1\}$.

到目前为止，我们一直在讨论二元编码，也就是码字字母表为 $\{0,1\}$。

More generally, we can consider $D$-ary coding, where the code alphabet has size $D$.

更一般地，我们也可以考虑 $D$ 元编码，也就是码字字母表大小为 $D$。

---

### Theorem: D-ary Version  
### 定理：D 元版本

Let

设

$$
c:\mathcal{X}\to \{1,2,\dots,D\}^*
$$

Then:

那么有：

- There exists a prefix-free $D$-ary code if and only if  
  存在一个 $D$ 元前缀码，当且仅当

$$
\sum_{x\in\mathcal{X}} D^{-\ell(c(x))}\le 1
$$

- There exists a uniquely decodable $D$-ary code if and only if  
  存在一个 $D$ 元唯一可译码，当且仅当

$$
\sum_{x\in\mathcal{X}} D^{-\ell(c(x))}\le 1
$$

So the same inequality generalizes from binary coding to $D$-ary coding.

因此，这个不等式可以从二元编码自然推广到 $D$ 元编码。

---

# Summary  
# 总结

This chapter studies variable-length source coding.

本章研究了变长信源编码。

- A **variable-length code** maps each source symbol to a finite binary string.  
  **变长编码**把每个源符号映射成一个有限长二进制串。

- To decode correctly, injectivity on single symbols is not enough; we need stronger conditions such as **unique decodability**.  
  为了正确解码，仅仅保证单个符号映射不同还不够；我们需要更强的条件，例如**唯一可译性**。

- Every **prefix-free code** is uniquely decodable, but not every uniquely decodable code is prefix-free.  
  每个**前缀码**都唯一可译，但并不是每个唯一可译码都是前缀码。

- **Kraft's inequality** characterizes the existence of prefix-free codes with given lengths:

$$
\sum_i 2^{-l_i}\le 1
$$

- **McMillan's inequality** shows that uniquely decodable codes satisfy the same length constraint:

$$
\sum_i 2^{-l_i}\le 1
$$

- The same result extends to **$D$-ary codes**:

  同样的结论也适用于 **$D$ 元编码**：

$$
\sum_x D^{-\ell(c(x))}\le 1
$$

So prefix-free coding is not only convenient for decoding, but also essentially optimal in terms of achievable length constraints.

因此，前缀码不仅解码方便，而且在可实现的码长约束方面本质上已经达到了最优。
