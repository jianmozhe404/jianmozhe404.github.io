# SVD讲解
#### 赵佳琦 2025.4.9
---
layout: center
---

# 奇异值分解 (SVD)

奇异值分解 (Singular Value Decomposition, SVD) 是一种强大的矩阵分解方法，广泛应用于数据降维、图像压缩和推荐系统等领域。

对于任意 $m \times n$ 矩阵 $A$，其 SVD 表示为：
$$
A = U \Sigma V^T
$$
其中：
- $U$: $m \times m$ 正交矩阵，表示输出空间的基向量（左奇异向量）。
- $\Sigma$: $m \times n$ 对角矩阵，对角线元素为奇异值 $\sigma_1 \geq \sigma_2 \geq \dots \geq \sigma_r > 0$。
- $V^T$: $n \times n$ 正交矩阵的转置，表示输入空间的基向量（右奇异向量）。

---

# SVD 的计算步骤

1. **计算协方差矩阵**:
   - 计算 $A^T A$ 和 $A A^T$,这两个矩阵是对称半正定矩阵，因此可以通过特征值分解得到它们的特征值和特征向量。
   
2. **特征值分解**:
   - 对 $A^T A$ 进行分解，得到特征值$\lambda_i$和对应的特征向量$v_i$,这些特征向量构成$V$。
   -对 $AT A^T$ 进行分解，得到特征值$\lambda_i$和对应的特征向量$u_i$,这些特征向量构成$U$。
3. **构造奇异值矩阵 $\Sigma$**:
   - 奇异值 $\sigma_i = \sqrt{\lambda_i}$，其中 $\lambda_i$ 是 $A^T A$ 或 $A A^T$ 的特征值。
   - 将奇异值按从大到小排列，构造对角矩阵 $\Sigma$。

---

# SVD 与 特征值分解的对比

#### 奇异值分解 (SVD)

##### 输入矩阵 $A$
$$
A=\begin{bmatrix}
3 & 1 \\
1 & 3
\end{bmatrix}
$$

##### 步骤 1: 计算协方差矩阵
- 计算 $A^TA$ 和 $AA^T$:
$$
A^TA=\begin{bmatrix}
10 & 6 \\
6 & 10
\end{bmatrix},\quad
AA^T=\begin{bmatrix}
10 & 6 \\
6 & 10
\end{bmatrix}
$$

##### 步骤 2: 特征值分解
- 对 $A^TA$ 进行特征值分解，得到右奇异向量 $V$ 和奇异值 $\sigma_i$。
- 对 $AA^T$ 进行特征值分解，得到左奇异向量 $U$。

---

##### 步骤 3: 构造分解结果
$$
A=U\Sigma V^T
$$

其中：
$$
U=\begin{bmatrix}
\frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\
\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}}
\end{bmatrix},\quad
\Sigma=\begin{bmatrix}
4 & 0 \\
0 & 2
\end{bmatrix},\quad
V^T=\begin{bmatrix}
\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
-\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}}
\end{bmatrix}
$$

---

# 示例: SVD 与 特征值分解
#### 特征值分解 (EVD)

##### 输入矩阵 $A$
$$
A=\begin{bmatrix}
3 & 1 \\
1 & 3
\end{bmatrix}
$$

##### 步骤 1: 直接计算特征值和特征向量
- 计算特征值 $\lambda$:
$$
\det(A-\lambda I)=0\implies\lambda_1=4,\lambda_2=2
$$

- 计算对应的特征向量 $v_1,v_2$:
$$
v_1=\begin{bmatrix}\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}\end{bmatrix},\quad
v_2=\begin{bmatrix}-\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}\end{bmatrix}
$$
---

##### 步骤 2: 构造分解结果
$$
A=Q\Lambda Q^{-1}
$$
其中：
$$
Q=\begin{bmatrix}
\frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\
\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}}
\end{bmatrix},\quad
\Lambda=\begin{bmatrix}
4 & 0 \\
0 & 2
\end{bmatrix},\quad
Q^{-1}=\begin{bmatrix}
\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
-\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}}
\end{bmatrix}
$$
# ***
### 对于对称半正定方阵来说, SVD和特征值分解是等价的 ! ! !   

---

## 异同点总结

### 相同点
1. 都计算出三个矩阵：
   - SVD: $U,\Sigma,V^T$
   - EVD: $Q,\Lambda,Q^{-1}$
2. 奇异值（SVD）和特征值（EVD）相同：$\sigma_i=\sqrt{\lambda_i}$。

### 不同点
1. **输入矩阵类型**:
   - SVD: 适用于任意形状矩阵。
   - EVD: 仅适用于方阵。
2. **协方差矩阵**:
   - SVD: 需要计算 $A^TA$ 或 $AA^T$。
   - EVD: 直接对原矩阵进行分解。

---

# 奇异值分解 (SVD) 的几何意义

#### 1. 矩阵 $A$ 的作用：从输入到输出的映射

矩阵 $A$ 将输入向量 $x\in\mathbb{R}^n$ 映射到输出向量 $b\in\mathbb{R}^m$：
$$
b=Ax
$$

从几何上看，$A$ 对输入空间中的向量进行了某种变换。这种变换可分解为三个步骤：
整个 SVD 过程可以总结为以下三步：
1. **输入空间的旋转或反射 ($V^T$)**：
   - 将输入向量对齐到新坐标系。
2. **沿主方向的拉伸或压缩 ($\Sigma$)**：
   - 对每个主方向上的分量进行拉伸或压缩。
3. **输出空间的旋转或反射 ($U$)**：
   - 将拉伸后的向量旋转或反射到最终的输出空间。
---

## 6. 示例计算

1. **旋转输入向量 ($V^T$)**：
   $$
   V^Tx=\begin{bmatrix}\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\\-\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\end{bmatrix}\begin{bmatrix}1\\0\end{bmatrix}=\begin{bmatrix}\frac{1}{\sqrt{2}}\\-\frac{1}{\sqrt{2}}\end{bmatrix}
   $$
2. **拉伸 ($\Sigma$)**：
   $$
   \Sigma V^Tx=\begin{bmatrix}4&0\\0&2\end{bmatrix}\begin{bmatrix}\frac{1}{\sqrt{2}}\\-\frac{1}{\sqrt{2}}\end{bmatrix}=\begin{bmatrix}4/\sqrt{2}\\-2/\sqrt{2}\end{bmatrix}
   $$
3. **旋转到输出空间 ($U$)**：
   $$
   U\Sigma V^Tx=\begin{bmatrix}\frac{1}{\sqrt{2}}&-\frac{1}{\sqrt{2}}\\\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\end{bmatrix}\begin{bmatrix}4/\sqrt{2}\\-2/\sqrt{2}\end{bmatrix}=\begin{bmatrix}1\\3\end{bmatrix}
   $$


