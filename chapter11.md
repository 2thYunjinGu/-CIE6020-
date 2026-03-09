# Chapter 11 Notes on Information Theory  
# 第 11 章 信息论笔记

---

# Chapter 11 Huffman Code  
# 第 11 章 Huffman 编码

## 11.1 Optimal Solution  
## 11.1 最优解

Recall the codeword-length optimization problem from the previous chapter.

回忆上一章中的码长优化问题。

We want to minimize the average code length

我们希望最小化平均码长

$$
L=\sum_i p_i l_i
$$

subject to McMillan's inequality

并满足 McMillan 不等式约束

$$
\sum_i 2^{-l_i}\le 1
$$

with integer lengths

且码长必须为整数

$$
l_i \in \mathbb{Z}_{>0}
$$

This is the exact discrete optimization problem for binary uniquely decodable codes.

这就是二元唯一可译码的精确离散优化问题。

---

### Shannon Code Is Not Always Optimal  
### Shannon 编码并不总是最优

Shannon code first solves the relaxed real-valued problem and then rounds the result to integers:

Shannon 编码先求解实数松弛问题，再把解向上取整到整数：

$$
l_i^{\text{Shannon}}=\left\lceil \log \frac{1}{p_i}\right\rceil
$$

However, Shannon code can be suboptimal.

但是，Shannon 编码可能不是最优的。

---

### Counterexample  
### 反例

Consider a binary source

考虑一个二元信源

$$
X=
\begin{cases}
0, & 2^{-10} \\
1, & 1-2^{-10}
\end{cases}
$$

Clearly, the optimal code is simply

显然，最优编码可以直接取为

- $c(0)=0$
- $c(1)=1$

So

因此

$$
l_0=l_1=1
$$

But Shannon code gives

但 Shannon 编码会给出

$$
l_0=\left\lceil \log \frac{1}{2^{-10}}\right\rceil=10,\qquad l_1=\left\lceil \log \frac{1}{1-2^{-10}}\right\rceil=1
$$

So Shannon code is not optimal here.

所以在这个例子里，Shannon 编码不是最优的。

---

### Huffman Code Gives the Optimal Solution  
### Huffman 编码给出最优解

The lecture states that the optimal solution to the discrete problem is given by **Huffman coding**.

讲义指出，这个离散优化问题的最优解由 **Huffman 编码**给出。

The basic Huffman algorithm is:

Huffman 算法的基本步骤是：

1. Sort the symbols by probability.  
   按概率对符号排序。

2. Repeatedly merge the two least likely symbols.  
   反复合并两个概率最小的符号。

3. Build a binary tree.  
   构造一棵二叉树。

4. The codeword of each symbol is the concatenation of the edge labels along the path from the root to that symbol.  
   每个符号的码字，就是从根节点到该符号叶节点路径上的边标签拼接而成。

---

### Example of Huffman Construction  
### Huffman 构造例子

Suppose

设

$$
p_1=0.15,\quad p_2=0.20,\quad p_3=0.25,\quad p_4=0.15,\quad p_5=0.25
$$

Sort them from large to small:

按从大到小排序可写成：

$$
p_3,\; p_5,\; p_2,\; p_1,\; p_4
$$

Then repeatedly merge the two least likely symbols:

然后不断合并两个最小概率符号：

- merge $p_1$ and $p_4$ into $0.30$  
  把 $p_1$ 和 $p_4$ 合并成 $0.30$

- merge $p_2$ and the new $0.30$ into $0.50$  
  把 $p_2$ 和新的 $0.30$ 合并成 $0.50$

- merge $p_3$ and $p_5$ into $0.50$  
  把 $p_3$ 和 $p_5$ 合并成 $0.50$

- merge the two $0.50$ nodes into $1$  
  最后把两个 $0.50$ 节点合并成 $1$

One valid Huffman code from the lecture is:

讲义中给出的一个合法 Huffman 码是：

- $c_3=01$
- $c_5=10$
- $c_2=11$
- $c_1=000$
- $c_4=001$

The exact left/right bit labels may vary, but the code lengths are what matter for optimality.

左右子树分配的比特标签可能不同，但对最优性真正重要的是码长而不是具体 0/1 排列。

---

## 11.2 Optimality Proof  
## 11.2 最优性证明

### Key Lemma  
### 关键引理

For an optimal prefix-free code, the following properties must hold.

对于一个最优前缀码，必须满足以下性质。

#### Property 1  
#### 性质 1

If

如果

$$
p_i>p_j
$$

then

那么

$$
l_i\le l_j
$$

Otherwise, if a more probable symbol had a longer codeword than a less probable symbol, swapping them would reduce the expected length.

否则，如果高概率符号反而拥有更长码字，那么交换二者会进一步降低平均码长。

---

#### Property 2  
#### 性质 2

The two longest codewords in an optimal prefix-free code must have the same length and must be siblings under the same parent node.

最优前缀码中，两个最长码字必须有相同长度，并且它们必须是同一个父节点下的兄弟叶节点。

This is because in a full binary tree, the deepest leaves can be arranged as sibling leaves.

这是因为在一棵最优二叉树里，最深的叶子可以整理成同一个父节点下的一对兄弟叶子。

---

#### Property 3  
#### 性质 3

Those two longest codewords must be assigned to the two least probable symbols.

这两个最长码字必须分配给概率最小的两个符号。

By Property 1, less probable symbols should not get shorter codewords than more probable ones.

由性质 1 可知，概率更小的符号不应该得到比高概率符号更短的码字。

---

### Reduction Step  
### 归约步骤

Assume without loss of generality that

不失一般性，设

$$
p_1\ge p_2\ge \cdots \ge p_n
$$

Now merge the two least probable symbols $p_{n-1}$ and $p_n$ into one combined symbol

现在把两个最小概率符号 $p_{n-1}$ 和 $p_n$ 合并成一个新符号

$$
q = p_{n-1}+p_n
$$

This gives a new distribution over $n-1$ symbols.

于是得到一个含 $n-1$ 个符号的新分布。

The central idea of the proof is:

整个证明的核心思想是：

- an optimal tree for the original distribution can be reduced to a tree for the merged distribution  
  原分布的最优树可以压缩成合并后分布的一棵树

- an optimal tree for the merged distribution can be expanded back to an optimal tree for the original distribution  
  合并后分布的最优树，也可以展开回原分布的一棵最优树

So optimality is preserved through the merge step.

因此，在“合并两个最小概率符号”这一步里，最优性会被保留下来。

---

### Cost Relation  
### 代价关系

Let $L_p$ be the average code length for the original distribution $p$, and let $L_q$ be that for the merged distribution $q$.

设原分布 $p$ 的平均码长为 $L_p$，合并后分布 $q$ 的平均码长为 $L_q$。

Then the lecture gives the key relation

讲义给出了关键关系

$$
L_q = L_p - (p_{n-1}+p_n)
$$

because when two sibling leaves are merged into their parent, their code lengths each decrease by 1.

因为当两个兄弟叶节点被并入父节点时，它们各自的码长都会减少 1。

Conversely, expanding a merged node into two children increases the cost by exactly

反过来，如果把合并节点展开成两个孩子，那么总代价会增加

$$
p_{n-1}+p_n
$$

So we also have

因此也有

$$
L_p = L_q + (p_{n-1}+p_n)
$$

---

### Recursive Optimality  
### 递归最优性

If the merged tree is optimal for the reduced distribution, then the expanded tree is optimal for the original distribution.

如果合并后的树对缩减分布是最优的，那么展开后的树对原分布也是最优的。

Since Huffman coding repeatedly performs exactly this merge operation, we get a recursive proof.

由于 Huffman 编码正是不断重复这个合并操作，因此就得到一个递归证明。

At the end, when only two symbols remain, the optimal tree is obvious:

最后，当只剩两个符号时，最优树显然是

- one codeword is `0`
- the other codeword is `1`

So by recursion, the entire Huffman tree is optimal.

因此由递归可知，整个 Huffman 树都是最优的。

---

## 11.3 Some Remarks  
## 11.3 一些说明

### Remark 1: Huffman Code Is Not Unique  
### 说明 1：Huffman 码不唯一

Huffman code is generally **not unique**.

Huffman 码一般**不是唯一的**。

Whenever there are ties in probabilities, or whenever left/right branches are labeled differently, multiple optimal Huffman trees may exist.

当概率出现并列，或者左右子树的 0/1 标记方式不同的时候，就可能存在多个不同的最优 Huffman 树。

The lecture gives an example with probabilities

讲义给出的一个例子中，概率为

$$
0.7,\; 0.1,\; 0.1,\; 0.05,\; 0.05
$$

Different merging orders or branch labels produce different codewords, but they all give the same optimal expected length.

不同的合并顺序或边标签会产生不同的码字，但它们的平均码长是相同的，仍然都是最优的。

---

### Remark 2: Minimizing Variance  
### 说明 2：最小化码长方差

The lecture notes mention that if we also want to minimize the variance

讲义还提到，如果我们还希望最小化码长方差

$$
\frac{1}{n}\sum_{i=1}^n (l_i-L)^2
$$

then we should place the combined probability node as high as possible in the tree.

那么应尽量让合并出来的概率节点在树中放得更高。

In other words, among multiple optimal Huffman trees, some may have smaller variance in codeword lengths.

也就是说，在多个同样最优的 Huffman 树中，有些树的码长波动会更小。

This is a refinement beyond merely minimizing the average code length.

这是在“最小平均码长”之外的进一步优化目标。

---

### Remark 3: D-ary Huffman Code  
### 说明 3：D 元 Huffman 码

The Huffman algorithm generalizes from binary trees to $D$-ary trees.

Huffman 算法可以从二叉树推广到 $D$ 叉树。

A $D$-ary code has alphabet

一个 $D$ 元码使用的码字符号表为

$$
\{1,2,\dots,D\}
$$

Instead of merging two least likely nodes each time, we now merge the $D$ least likely nodes.

此时不再每次合并两个最小概率节点，而是每次合并 $D$ 个最小概率节点。

---

### Need for Dummy Nodes  
### 为什么需要虚节点

For binary Huffman coding, every merge combines exactly 2 nodes.

在二元 Huffman 编码中，每次合并正好是 2 个节点。

For $D$-ary Huffman coding, every merge should combine exactly $D$ nodes.

而在 $D$ 元 Huffman 编码中，每次合并应该正好合并 $D$ 个节点。

If the number of symbols does not fit this structure, we add **dummy nodes** with zero probability.

如果符号个数不满足这个结构，就需要加入概率为 0 的**虚节点**。

The lecture gives an example for $D=3$.

讲义里给了一个 $D=3$ 的例子。

Without dummy nodes, one branch would be “wasted” in the final merge.

如果不加虚节点，最后一次合并时就会出现一个分支被“浪费”。

So we add dummy nodes to ensure that every internal node has exactly $D$ children.

因此我们加入虚节点，保证每个内部节点都恰好有 $D$ 个孩子。

---

### Remark 4: Relation to Entropy  
### 说明 4：与熵的关系

Recall that the real-valued optimal solution to the relaxed problem is

回忆一下，松弛问题的实数最优解是

$$
l_i=\log \frac{1}{p_i}
$$

Hence

因此

$$
\sum_i p_i \log \frac{1}{p_i}=H(X)
$$

is a lower bound on the exact discrete optimization problem.

就是离散最优化问题的一个下界。

So for any uniquely decodable code, including Huffman code,

所以对任意唯一可译码，包括 Huffman 码在内，都有

$$
L\ge H(X)
$$

---

### Remark 5: Approaching Entropy More Closely  
### 说明 5：如何更逼近熵

To make

为了让

$$
L\to H(X)
$$

more closely, we can compress blocks of symbols together.

更加逼近成立，我们可以把多个符号打包一起编码。

That is, instead of coding single symbols, code the super-symbol

也就是说，不去编码单个符号，而是编码超级符号

$$
(X_1,\dots,X_n)
$$

based on the joint distribution

基于联合分布

$$
p(x_1,\dots,x_n)
$$

and then apply Huffman coding to all possible sequences.

再对所有可能序列应用 Huffman 编码。

Then the per-symbol average length can approach the entropy arbitrarily well.

这样，每个符号的平均码长就可以任意逼近熵。

But the drawback is that the codebook becomes exponentially large.

但代价是：码书规模会变得指数级巨大。

---

# Summary  
# 总结

This chapter introduces **Huffman coding**, which solves the exact discrete codeword-length optimization problem.

本章介绍了 **Huffman 编码**，它解决了离散码长优化的精确最优问题。

- Shannon code is based on rounding the relaxed real solution, so it is sometimes suboptimal.  
  Shannon 编码是把实数松弛解取整得到的，因此有时并不是最优的。

- Huffman coding builds an optimal binary prefix-free code by repeatedly merging the two least probable symbols.  
  Huffman 编码通过反复合并两个最小概率符号，构造出最优的二元前缀码。

- The optimality proof is based on the fact that the two least probable symbols must be siblings at the maximum depth in an optimal tree.  
  它的最优性证明基于这样一个事实：在最优树中，两个最小概率符号必须作为最深层的一对兄弟叶节点出现。

- Huffman code is not unique, but all Huffman trees achieve the same minimum expected length.  
  Huffman 码并不唯一，但所有 Huffman 树都达到相同的最小平均码长。

- Huffman coding can be generalized to $D$-ary codes, sometimes with dummy zero-probability symbols added.  
  Huffman 编码可以推广到 $D$ 元编码，有时需要额外加入零概率虚节点。

- Entropy remains a lower bound:

$$
L\ge H(X)
$$

- By grouping long symbol blocks together, Huffman coding can approach entropy arbitrarily closely, at the cost of exponential codebook size.  
  通过把长符号块打包一起编码，Huffman 编码可以任意逼近熵，但代价是码书大小呈指数增长。
