# 通过绝对折扣回退实现彩色图像直方图均衡

## 摘要

### 创新内容

本文提出了一种新的彩色图像直方图均衡方法，该方法利用了颜色分量之间的相关性，并通过从统计语言工程中的多级平滑技术进行了增强。此外，所提出的方法通过一种基于色调保持非线性变换的经验技术进行了扩展，以消除色域问题。

### 论文成果

通过所提出的方法，均衡的图像质量更好，判断依据是它们的视觉吸引力和客观品质因数（如熵和生成的彩色直方图与多变量均匀概率密度函数之间的 Kullback-Leibler 散度估计）。

## 结论

实验结果表明，所提出的方法在产生更具视觉吸引力的图像方面具有优越性。通过测量其熵和 Kullback-Leibler 散度，说明了均衡图像具有更均匀的直方图。此外，色域消除（这是导致图像中不需要的色彩伪影的一个因素）也是通过应用方法 5 获得的。

## 相关工作

直方图均衡是增强灰度图像的最简单常用的技术。它假设像素灰度级别是独立的同分布随机变量（rvs），而图像是遍历随机域的实现。因此，当图像的直方图类似于均匀分布时，图像被认为信息量更大。从这个角度来看，灰度直方图均衡利用了单 rv 的函数理论，该理论建议使用像素强度的累积分布函数（CDF）将像素强度转换为均匀分布的 rv。但是，由于数据图像的离散性，均衡图像的直方图可以近似均匀。

由于颜色的矢量性质，在处理彩色图像时，直方图均衡成为一项繁琐的任务。每个颜色像素都由一个矢量表示，该矢量的分量与适当色彩空间中的颜色分量（即 RGB 空间中的红色、绿色和蓝色三个分量）相等。问题的复杂性还在于颜色分量之间的相关性以及人类的颜色感知。本文中描述的方法要么回顾缓解这些问题中的一者或二者的工作，要么重新审视这些工作以提高它们的性能。

从历史上看，直方图均衡对色彩图像的第一个也是最直接的扩展是将灰度直方图均衡分别应用于彩色图像的不同色带，而忽略分量之间的相关性。一些工作还集中在沿原始图像的主成分轴展开直方图，或重复展开三个二维直方图。

随后的系统研究工作产生了两个主要的算法类别。第一类包括使用 3-D 直方图或彩色图像的 1-D 直方图在 RGB 空间上工作的算法，第二类由在非线性色彩空间（如 HSI（色相、饱和度和强度）或 C-Y 空间）中运行的算法，这些算法应用于一个或两个颜色分量。

在 RGB 空间中，更具代表性的方法是 3-D 直方图均衡、直方图爆炸和直方图抽取。Trahanias 和 Venetsanopoulos 提出的 3-D 直方图均衡尝试通过 RGB 颜色立方体中的统一 3-D 直方图规范将累计直方图扩展到更高的维度。而后将原始图像颜色的 3-D CDF 与理想的均匀 CDF 进行比较。

直方图爆炸最初由 Misna 和 Rodriguez 提出，只在利用完整的 3-D RGB 色域。该算法偏好于在 RGB 立方体的对角线上（即灰线）上选择一个工作点以防止色调变化，并绘制从工作点发出的射线，穿过图像中存在的色点，并一直到 RGB 立方体面。然后通过对每条射线的工作点和颜色空间边界上的点之间插入 3-D 直方图数据构建 1-D 直方图。通过均衡 1-D 直方图，可以确定原始色点的新颜色值。因此，颜色点在颜色空间中几乎均匀分布。在该方法的另一种变体中，颜色在 CIE-LUV 空间中表示。

直方图抽取使用迭代算法将色点均匀分散在整个 3D 色域上。该算法使用整个 3-D 色彩空间作为当前空间进行初始化，并通过迭代地应用两个步骤。在第一步中，当前空间的所有颜色点都会发生偏移，以使它们坐标的平均值与空间的集合中心重合。在第二步中，当前色彩空间被划分为 8 个大小相等的子空间。每个新创建的颜色子空间都设置为下一次迭代的当前空间。当子空间大小达到其最小值时，算法将停止。

在 Pichon 等人的方法中，网格最初会变形以使用 RGB 色彩空间中的原始直方图。然后，通过将网格的所有单元线性映射到均匀网格的相应单元，该网格用于定义色彩空间的分段线性变形。因此，生成的均衡图像的直方图始终几乎均匀，但均衡图像本身存在于色相相关的伪影。这一事实使该方法对于伪彩色科学可视化特别有趣。

在 Pitie 等人的工作中，解决了颜色转移问题，并提出了一种估计将 $N$ 维分布映射到另一个分布的变换的新方法。当目标概率分布均匀时，所提出的方法可用于直方图均衡。该算法分三个步骤迭代运行。在第一步中，通过使用适当的旋转矩阵旋转源样本和目标样本来更改 RGB 空间坐标系。在第二步中，所有样本都投影在三个轴上，以获得旋转的源样本和目标样本的边际分布。在第三步中，为每个轴找到将源边缘匹配为目标边缘的一维转换，并将转换后的样本旋转回原始 RGB 空间。当实现每个可能旋转的所有边际收敛时，算法将停止。一种较新的方法将灰度直方图均衡扩展到彩色图像，将问题表述为具有边界约束的非线性优化问题。给定图像在 RGB 色彩空间中的直方图由各向同性高斯混合近似，并且其来自目标均匀分布的最小平方误差最小。

在 Forrest 的工作中，开发了一种测量直方图利用率和对任意数量的维度执行直方图均衡的技术。直方图利用率度量基于这样一个基础实施：可以将来自独立数据的卡方度量相加以给出独立度量。因此，该度量取决于颜色分量（例如 R）的线性直方图在位于其他两个颜色分量（例如 G 和 B）平面上的某个点和相应的线性累计直方图的平均直方图占用率。然后，通过利用直方图利用率度量来实现直方图均衡，该度量生成有关应如何更改直方图的信息。通过这种方式，生成的直方图可以有效地展开，而不会对对比度或颜色平衡产生很大的变化。

上述所有方法都适用于 RGB 空间。通常，它们是计算密集型的，其主要缺点是色调的更改。后一个事实会导致令人类观察者不适的色彩伪影。为了减少色调修改，第二类算法通过在 HSI 空间中执行均衡，方法是仅修改强度或同事修改强度和/或饱和度，同时保持色调不变。

Pitas 和 Kiniklis 提出了一种试图共同平衡强度和饱和度的方法。为了避免均衡后出现不自然的颜色，该方法考虑了 HSI 空间和 RGB 空间之间的几何概念。

另一种直方图均衡方法基于强度和饱和度分量。在这种方法中，RGB 色彩空间首先转换为 HSI 三角形，该三角形被划分为 96 个色调区域。直方图均衡化应用于每个色相区域内的饱和度。该算法的缺点在于需要确定用于每个转换的最大可能饱和度值，并且忽略了强度分量。Weeks 等人通过在色差空间（C-Y）的均衡过程中同时包含饱和度和强度分量，对该方法进行了改进。结果发现，转换会在均衡图像中产生无法实现的 RGB 颜色。该算法将整个 C-Y 色彩空间（转换为 HSI）划分为 $n\times k$ 个子空间，其中 $n$ 和 $k$ 分别是色调和强度分量的分区数。然后，在每个子空间的最大可实现饱和度内，饱和度被均衡一次。接下来，通过考虑整个图像来均衡强度分量。Weeks 等人提出的方法被 Duan 和 Qiu 进一步应用于 HSI 色彩空间。

在 Luccchese 等人的工作中，使用传统的灰度直方图均衡方法对彩色图像的消色差通道进行均衡，并且色度通道的处理方式类似于图像变形。该算法在 $xy$ 色度图中工作，由两个步骤组成。在第一步中，每个颜色像素都转换为相对于特定区域的最大饱和值。在第二步中，新颜色向新的白点去饱和。

## 具体方法

### 颜色直方图均衡方法

#### 方法 1：三种颜色分量的单独均衡

由于许多彩色图像具有三个色基，因此每个颜色的图像由 3 维向量 $\overrightarrow{X}$ 表示，并且三个颜色分量中分别执行灰度直方图均衡。

灰度直方图均衡尝试将图像的像素灰度级均匀分布到所有可用的灰度级 $L$（例如使用 8 位表示每个灰度级时 $L=256$）。让我们将图像像素灰度级别视为 rv $\boldsymbol{x}$。灰度图像的直方图是 $\boldsymbol{x}$ 的概率密度函数（PDF），定义为
$$
\begin{equation}
f_{\boldsymbol{x}}(x_k)=P\{\boldsymbol{x}=x_k\}=\frac{N(x_k)}{\sum_{m=0}^{L-1}N(x_m)}\quad\forall k=0,1,\ldots,L-1,
\end{equation}
$$
其中 $N(x_k)$ 是灰度值为 $x_k$ 的像素数。rv $\boldsymbol{x}$ 的 CDF $F_{\boldsymbol{x}}(x_k)$ 由下式给出
$$
\begin{equation}
y_k=F_{\boldsymbol{x}}(x_k)=P\{\boldsymbol{x}\leqslant x_k\}=\sum_{m=0}^kf(x_m)\quad\forall k=0,1,\ldots,L-1
\end{equation}
$$
如上定义变换函数，用于获取均匀分布的均衡图像的灰度等级 $y_k$。

对于彩色图像，假设每个像素的颜色为随机向量 $\overrightarrow{\boldsymbol{X}}=(\boldsymbol{x}_R,\boldsymbol{x}_G,\boldsymbol{x}_B)^T$，其中 $\boldsymbol{x}_R,\boldsymbol{x}_G,\boldsymbol{x}_B$ 是对红色、绿色和蓝色分量进行建模的 rv。因此，通过应用方程 2 可以估计每个颜色分量的均衡直方图。

#### 方法 2：RGB 空间中的 3-D 均衡

Trahanias 和 Venetsanopoulos 提出的方法实际上是 RGB 色彩空间中的 3-D 直方图规范，其输出直方图是均匀的。方法如下所示：

（1）计算彩色图像的原始 3-D 直方图。

（2）使用公式 3 和公式 4 计算原始随机向量 $\overrightarrow{\boldsymbol{X}}$ 和服从均匀分布的随机向量 $\overrightarrow{\boldsymbol{Y}'}=(\boldsymbol{y}'_R,\boldsymbol{y}_G',\boldsymbol{y}_B')^T$ 的联合 CDF
$$
\begin{equation}
\begin{aligned}
y_{R_kG_sB_t}&=F_{\boldsymbol{x}_R\boldsymbol{x}_G\boldsymbol{x}_B}(x_{R_k},x_{G_s},x_{B_m})=P\{\boldsymbol{x}_R\leqslant x_{R_k},\boldsymbol{x}_G\leqslant x_{G_s},\boldsymbol{x}_B\leqslant x_{B_t}\}\\
&=\sum_{i=0}^k\sum_{j=0}^s\sum_{m=0}^tf(x_{R_i},x_{G_j},x_{B_m})\quad\forall k,s,t=0,1,\ldots,L-1,
\end{aligned}
\end{equation}
$$

$$
\begin{equation}
\begin{aligned}
y'_{R_{k'}G_{s'}B_{t'}}&=\sum_{i=0}^{k'}\sum_{j=0}^{s'}\sum_{m=0}^{t'}\frac{1}{L^3}\\
&=\frac{(k'+1)(s'+1)(t'+1)}{L^3}\quad\forall k',s',t'=0,1,\ldots,L-1,
\end{aligned}
\end{equation}
$$

其中 $f(x_{R_i},x_{G_j},x_{B_m})$ 是联合 PDF。

（3）对于每个颜色像素 $(R_k,G_s,R_t)$，选择最小的满足 $y'_{R_{k'}G_{s'}B_{t'}}-y_{R_kG_sB_t}\geqslant 0$ 的三元组 $(R_{k'},G_{s'},B_{t'})$。更准确的说，最初将 $y_{R_kG_sB_t}$ 的值与 $y'_{R_{k'}G_{s'}B_{t'}}$ 的值进行比较，如果 $y_{R_kG_sB_t}$ 大于（小于）$y'_{R_{k'}G_{s'}B_{t'}}$，则下标 $R_k,G_s,B_t$ 一次增加（减少）一个，直到满足刚才提到的不等式。最终的三元组值构成均衡图像的颜色。

#### 方法 3：HSI 空间中强度分量的均衡

假设彩色像素由随机向量 $\overrightarrow{\boldsymbol{X}}=(\boldsymbol{x}_H,\boldsymbol{x}_S,\boldsymbol{x}_I)^T$ 建模，强度分量的 PDF 由下式给出
$$
\begin{equation}
f_{\boldsymbol{x}_I}(x_{I_k})=\left\{\begin{array}{ll}
12\times x_{I_k}^2 & \text{for }0\leqslant x_{I_k}\leqslant 0.5\\
12\times(1-x_{I_k})^2&\text{for }0.5\leqslant x_{I_k}\leqslant 1
\end{array}\right.
\end{equation}
$$

#### 方法 4：HSI 空间中强度和饱和度的 2-D 均衡
