# 多通道技术在彩色图像增强与建模中的应用

## 摘要

### 创新点

我们在两个目标研究领域提出了新颖的多通道方法。提出了一种彩色图像直方图计算和均衡化的并行算法。

## 具体方法

### 多通道 AR 建模

### 多通道直方图均衡

连续随机向量 $\mathbf{X}=[\mathbf{x}_1,\mathbf{x}_2,\ldots,\mathbf{x}_n]$ 具有下述 PDF：
$$
\begin{equation}
f(X)=f(x_1,\ldots,x_n)=\frac{\partial^nF(x_1,\ldots,x_n)}{\partial x_1\cdots\partial x_n}
\end{equation}
$$
和分布函数
$$
\begin{equation}
F(X)=F(x_1,\ldots,x_n)=P\{\mathbf{x}_1\leq x_1,\ldots,\mathbf{x}_n\leq x_n\}.
\end{equation}
$$
在 $\mathbf{x}_k,\ldots,\mathbf{x}_1$ 的前提下 rvs $\mathbf{x}_n,\ldots,\mathbf{x}_{k+1}$ 的条件概率为
$$
\begin{equation}
f(x_n,\ldots,x_{k+1}/x_k,\ldots,x_1)=\frac{f(x_1,\ldots,x_k,\ldots,x_n)}{f(x_1,\ldots,x_k)}.
\end{equation}
$$
相应的分布函数则通过积分得到
$$
\begin{equation}
\begin{aligned}F&(x_n,\ldots,x_{k+1}/x_k,\ldots,x_1)\\&=\int_{-\infty}^{x_n}\ldots\int_{-\infty}^{x_{k+1}}f(z_n,\ldots,z_{k+1}/x_k,\ldots,x_1)dz_{k+1}\cdots dz_n.\end{aligned}
\end{equation}
$$
随机向量 $\mathbf{X}=[\mathbf{x}_1,\mathbf{x}_2,\ldots,\mathbf{x}_n]$ 的非线性逐点变换可以表示为
$$
\begin{equation}
\mathbf{y}_1=F(\mathbf{x}_1),\mathbf{y}_2=F(\mathbf{x}_2/\mathbf{x}_1),\ldots,\mathbf{y}_n=F(\mathbf{x}_n/\mathbf{x}_{n-1},\ldots,\mathbf{x}_1).
\end{equation}
$$
如果我们想把 $\mathbf{X}=[\mathbf{x}_1,\mathbf{x}_2,\ldots,\mathbf{x}_n]$ 转化为 $\mathbf{Z}=[\mathbf{z}_1,\mathbf{z}_2,\ldots,\mathbf{z}_n]$，其中 $\mathbf{Z}$ 必须有非均匀的联合 PDF $f_Z(Z)$，我们首先推导出变换 $\mathbf{Y}=T(\mathbf{X})$ 和 $\mathbf{S}=G(\mathbf{Z})$ 使得随机向量 $\mathbf{X}$ 和 $\mathbf{Z}$ 相等。然后把这两个变换合成为一个
$$
\begin{equation}
\mathbf{Z}=G^{-1}[T(\mathbf{X})].
\end{equation}
$$
在数字形式下，采用多通道直方图的形式
$$
\begin{equation}
\begin{aligned}f(x_{1i})&=\Pr\{\mathbf{x}_{1}=x_{1i}\},\\f(x_{1i},x_{2j})&=\Pr\{\mathbf{x}_{1}=x_{1i},\mathbf{x}_{2}=x_{2j}\},\ldots\end{aligned}
\end{equation}
$$
其中 $0\le i,j,k,\ldots\le L$。$L$ 是每个图像通道的离散级别数，而 $x_{1i},x_{2j},\ldots$ 是相应 rv 的可能值。多通道直方图均衡化采用如下形式，由公式 9 和 11 组合而成：
$$
\begin{equation}
\begin{aligned}&y_{1i}=\sum_{m=0}^if(x_{1m}),\quad y_{2j}=\sum_{m=0}^j\frac{f(x_{1i},x_{2m})}{f(x_{1i})},\\&y_{3k}=\sum_{m=0}^k\frac{f(x_{1i},x_{2j},x_{3m})}{f(x_{1i},x_{2j})}.\end{aligned}
\end{equation}
$$
下面的 PDF 均匀地填充HSI颜色空间，它们可以用几何概念导出。
$$
\begin{equation}
f_I(I)=\left\{\begin{matrix}12I^2&\mathrm{for~}0\leq I\leq0.5\\12(1-I)^2&\mathrm{for~}0.5\leq I\leq1\end{matrix}\right.
\end{equation}
$$

$$
\begin{equation}
f_S(S)=6S-6S^2\mathrm{~for~}0\leq S\leq1
\end{equation}
$$

$$
\begin{equation}
f_{IS}(I,S)=\begin{cases}6S&\text{for }S\leq2I,I\in[0,1/2]\\0&\text{for }S>2I,I\in[0,1/2]\\6S&\text{for }S\leq2(1-I),I\in[1/2,1]\\0&\text{for }S>2(1-I),I\in[1/2,1].\end{cases}
\end{equation}
$$

