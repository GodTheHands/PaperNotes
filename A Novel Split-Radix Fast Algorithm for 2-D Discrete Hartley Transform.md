# 一种用于二维离散 Hartley 变换的新型 Split-Radix 快速算法

## 摘要

### 创新内容

本文提出了一种快速 split-redix-$(2\times 2)/(8\times 8)$ 算法，用以计算长度为 $N\times N$（其中 $N=q*2^m$，且 $q$ 是奇数）的 2-D 离散 Hartley 变换（DHT）。该方法将一个 $N\times N$ 的 DHT 分解为一个 $N/2\times N/2$ 的 DHT 和 48 个 $N/8\times N/8$ 的 DHT。

### 论文成果

该方法与 split-radix-$(2\times 2)/(4\times 4)$ 算法相比，有效地减少了算术运算、数据传输和旋转因子的数量。此外，在简单矩阵中表达的特性导致算法的简易实现。

## 结论

与已有的最佳算法相比，所提出的算法不仅保留了良好特性，如提供了更广泛的序列长度选择，具有规则的计算结构和就地计算，而且具有较低的算术复杂度，减少了约 30% 的数据传输和 35% 的旋转因子，这对 FHT 算法的执行时间有很大贡献。

## 提出的 Radix-$(2\times 2)/(8\times 8)$ 算法

二维实序列 $x(n_1,n_2)$（$0\le n_1,n_2\le N-1$）的二维 DHT $X(k_1,k_2)$ 定义为 
$$
\begin{equation}
X(k_1,k_2)=\sum_{n_1=0}^{N-1}\sum_{n_2=0}^{N-1}x(n_1,n_2)\text{cas}\left(\frac{2\pi}{N}\sum_{i=1}^2n_ik_i\right),\qquad 0\le k_1,k_2\le N-1
\end{equation}
$$
其中 $\text{cas}(\theta)=\cos(\theta)+\sin(\theta)$。假设序列长度 $N$ 可以写成 $q\times 2^m$，其中 $q$ 是奇数且 $m>0$。

让我们首先考虑当 $m=1$ 时（此时 $N=2q$）。

### 当 $m=1$ 时，即 $N=2q$

现在，使用 radix-$2\times 2$ 算法来分解一个长度为 $2q\times 2q$ 的 DHT。偶偶索引输出由下式获得
$$
\begin{equation}
    X(2k_1,2k_2)=\sum_{n_1=0}^{q-1}\sum_{n_2}^{q-1}y_{00}(n_1,n_2)\text{cas}\left(\frac{2\pi}{q}\sum_{i=1}^2n_ik_i\right),\qquad 0\le k_1,k_2\le q-1.
\end{equation}
$$
偶奇索引、奇偶索引和奇奇索引输出可以计算如下
$$
\begin{equation}
    X(2k_1+p_1q,2k_2+p_2q)=\sum_{n_1=0}^{q-1}\sum_{n_2=0}^{q-1}(-1)^{(n_1p_1+n_2p_2)}\times y_{p_1p_2}(n_1,n_2)\text{cas}\left(\frac{2\pi}{q}\sum_{i=1}^2n_ik_i\right)
\end{equation}
$$
其中 $p_1,p_2=0,1,(p_1,p_2)\ne(0,0),0\le k_1,k_2\le q-1$。

对于序列 $y_{p_1p_2}(n_1,n_2)$，其中 $p_1,p_2=0,1$，在公式 2 和公式 3 中出现，其可以从原始输入如下得到
$$
\begin{equation}
    \begin{aligned}
   &(y_{00}(n_1,n_2),y_{01}(n_1,n_2),y_{10}(n_1,n_2),y_{11}(n_1,n_2))^{T}\\
    &=(H_2\otimes H_2)(x(n_1,n_2),x(n_1,n_2+q),x(n_1+q,n_2),x(n_1+q,n_2+q))^T
    \end{aligned}
\end{equation}
$$
