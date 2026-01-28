# 向量空间与线性映射笔记

**课程日期**: 2026年1月23日 & 2026年1月26日  
**主题**: Affine Space and its Generation - Vector Space and Linear Mapping

---

## 目录

1. [仿射映射 (Affine Mapping)](#1-仿射映射-affine-mapping)
2. [群 (Group)](#2-群-group)
3. [向量空间 (Vector Space)](#3-向量空间-vector-space)
4. [向量子空间 (Vector Subspace)](#4-向量子空间-vector-subspace)
5. [线性组合与线性相关性](#5-线性组合与线性相关性)
6. [生成集与基](#6-生成集与基)
7. [线性映射 (Linear Mapping)](#7-线性映射-linear-mapping)

---

## 1. 仿射映射 (Affine Mapping)

### 1.1 从神经网络到仿射映射

考虑一个简单的神经网络层：

$$
\begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix} = \begin{bmatrix} W_{11} & W_{21} & W_{31} \\ W_{12} & W_{22} & W_{32} \\ W_{13} & W_{23} & W_{33} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + \begin{bmatrix} b_1 \\ b_2 \\ b_3 \end{bmatrix}
$$

其中：
- $W_{ij}$: 从 $X_j$ 到 $y_i$ 的权重
- $b_i$: 从常数 $1$ 到 $y_i$ 的偏置

**紧凑形式**:
$$
\boxed{y = \boxed{WX} + \boxed{b}} \Rightarrow \text{affine mapping}
$$

**线性映射** $\Rightarrow$ **向量空间**

---

## 2. 群 (Group)

### 2.1 群的定义

考虑一个集合 $G$ 和一个运算 $\boxed{X}: G \times G \mapsto G$。如果满足以下条件，则 $(G, \boxed{X})$ 称为**群**：

1. **封闭性 (Closure)**: $\forall x, y \in G, x \boxed{X} y \in G$
2. **结合律 (Associativity)**: $\forall x, y, z \in G, (x \boxed{X} y) \boxed{Z} = x \boxed{X} (y \boxed{Z})$
3. **单位元 (Identity)**: $\exists e \in G$ 使得 $\forall x \in G, x \boxed{X} e = e \boxed{X} x = x$
4. **逆元 (Inverse)**: $\forall x \in G, \exists y \in G$ 使得 $x \boxed{X} y = y \boxed{X} x = e$，记作 $x^{-1}$

### 2.2 阿贝尔群 (Abelian Group)

如果群 $(G, \boxed{X})$ 还满足：

5. **交换律 (Commutativity)**: $\forall x, y \in G, x \boxed{X} y = y \boxed{X} x$

则称为**阿贝尔群**（交换群）。

### 2.3 例子

**Example 1**: $(\mathbb{R} \setminus \{0\}, \cdot)$ is an Abelian group

**Proof**:
1. **Closure**: $\forall a, b \in \mathbb{R} \setminus \{0\}, a \cdot b \in \mathbb{R} \setminus \{0\}$ ✓
   - For any two non-zero real numbers, their product is also a non-zero real number.

2. **Associativity**: $\forall a, b, c \in \mathbb{R} \setminus \{0\}, (a \cdot b) \cdot c = a \cdot (b \cdot c)$ ✓
   - Multiplication of real numbers is associative.

3. **Identity element**: Consider $1 \in \mathbb{R} \setminus \{0\}$. For all $a \in \mathbb{R} \setminus \{0\}$, we have $a \cdot 1 = 1 \cdot a = a$ ✓
   - The number 1 is the multiplicative identity (unit element).

4. **Inverse element**: For all $a \in \mathbb{R} \setminus \{0\}$, we have $a \cdot \frac{1}{a} = \frac{1}{a} \cdot a = 1$ ✓
   - Every non-zero real number has a multiplicative inverse.

5. **Commutativity**: For all $a, b \in \mathbb{R} \setminus \{0\}, a \cdot b = b \cdot a$ ✓
   - Multiplication of real numbers is commutative.

Therefore, $(\mathbb{R} \setminus \{0\}, \cdot)$ is an Abelian group.

**Exercise**: $(\mathbb{R}, +)$ is an Abelian group

**Proof**:
1. **Closure**: $\forall a, b \in \mathbb{R}, a + b \in \mathbb{R}$ ✓
   - The sum of any two real numbers is a real number.

2. **Associativity**: $\forall a, b, c \in \mathbb{R}, (a + b) + c = a + (b + c)$ ✓
   - Addition of real numbers is associative.

3. **Identity element**: Consider $0 \in \mathbb{R}$. For all $a \in \mathbb{R}$, we have $a + 0 = 0 + a = a$ ✓
   - The number 0 is the additive identity.

4. **Inverse element**: For all $a \in \mathbb{R}$, we have $a + (-a) = -a + a = 0$ ✓
   - Every real number has an additive inverse (its negative).

5. **Commutativity**: For all $a, b \in \mathbb{R}, a + b = b + a$ ✓
   - Addition of real numbers is commutative.

Therefore, $(\mathbb{R}, +)$ is an Abelian group.

**Counterexample**: $(\mathbb{R}, \cdot)$ is not a group

For $0 \in \mathbb{R}$, there does not exist $a \in \mathbb{R}$ such that $a \cdot 0 = 1$ ✗

---

## 3. 向量空间 (Vector Space)

### 3.1 定义

一个**实值向量空间** $V := (V, +, \cdot)$ 是一个集合，配备两种运算：

1. **向量加法**: $+ : V \times V \mapsto V$
2. **标量乘法**: $\cdot : \mathbb{R} \times V \mapsto V$

### 3.2 向量空间的公理

其中满足以下条件：

#### 1) $(V, +)$ 是阿贝尔群

- 封闭性、结合律、单位元（零向量 $\vec{0}$）、逆元、交换律

#### 2) 分配律 (Distributivity)

① $\forall \lambda \in \mathbb{R}, \forall \vec{x}, \vec{y} \in V: \lambda(\vec{x} + \vec{y}) = \lambda \vec{x} + \lambda \vec{y}$

② $\forall \lambda, \varphi \in \mathbb{R}, \forall \vec{x} \in V: (\lambda + \varphi) \vec{x} = \lambda \vec{x} + \varphi \vec{x}$

#### 3) 结合律（外运算）

$\forall \lambda, \psi \in \mathbb{R}, \forall \vec{x} \in V: \lambda \cdot (\psi \cdot \vec{x}) = (\lambda \psi) \cdot \vec{x}$

#### 4) 标量单位元

$\forall \vec{x} \in V: 1 \cdot \vec{x} = \vec{x}$

### 3.3 术语

- **向量 (Vector)**: $V$ 中的元素 $\vec{x} \in V$
- **零向量 (Zero Vector)**: $(V, +)$ 的单位元，记作 $\vec{0} = [0, \ldots, 0]^T$
- **向量加法 (Vector Addition)**: 内运算 $+$
- **标量 (Scalar)**: $\lambda \in \mathbb{R}$
- **标量乘法 (Scalar Multiplication)**: 外运算 $\cdot$

**注意**: 标量乘积（内积/点积）是不同的概念，将在后续章节讨论。

### 3.4 空间的定义

**空间 (Space)**: 具有元素间特殊结构的集合

这种特殊结构通常由**运算 (operation)** 定义。

---

## 4. 向量子空间 (Vector Subspace)

### 4.1 定义

设：
- 向量空间 $V = (V, +, \cdot)$
- $U \subset V$ 且 $U \neq V$

如果 $U := (U, +, \cdot)$ 在限制到 $U \times U$ 和 $\mathbb{R} \times U$ 的运算下也是向量空间，则称 $U$ 是 $V$ 的**向量子空间**，记作 $U \subseteq V$。

---

## 5. 线性组合与线性相关性

### 5.1 线性组合 (Linear Combination)

考虑向量空间 $V := (V, +, \cdot)$ 和有限个向量 $\vec{x}_1, \ldots, \vec{x}_k \in V$。

如果向量 $\vec{v} \in V$ 可以表示为：

$$
\vec{v} = \lambda_1 \vec{x}_1 + \lambda_2 \vec{x}_2 + \cdots + \lambda_k \vec{x}_k = \sum_{i=1}^{k} \lambda_i \vec{x}_i
$$

其中 $\lambda_1, \ldots, \lambda_k \in \mathbb{R}$，则称 $\vec{v}$ 是 $\vec{x}_1, \ldots, \vec{x}_k$ 的**线性组合**。

### 5.2 线性相关性 (Linear Dependency)

考虑向量空间 $V$，$k > 0$，向量 $\vec{x}_1, \ldots, \vec{x}_k \in V$，以及：

$$
\sum_{i=1}^{k} \lambda_i \vec{x}_i = \vec{0}
$$

对于某些 $\lambda_i \in \mathbb{R}, i \in [1, k]$。

我们称 $\vec{x}_1, \ldots, \vec{x}_k$ 是：

1. **线性无关 (Linearly Independent)**: 仅存在平凡解，即 $\lambda_1 = \lambda_2 = \cdots = \lambda_k = 0$
2. **线性相关 (Linearly Dependent)**: 存在非平凡线性组合，即某些 $\lambda_i \neq 0$

---

## 6. 生成集与基

### 6.1 生成集 / 张成集 (Spanning / Generating Set)

考虑向量空间 $V := (V, +, \cdot)$ 和集合 $A := \{\vec{x}_1, \ldots, \vec{x}_k\} \subset V$。

如果 $\forall \vec{v} \in V$，存在 $\lambda_1, \ldots, \lambda_k \in \mathbb{R}$ 使得：

$$
\vec{v} = \sum_{i=1}^{k} \lambda_i \vec{x}_i
$$

其中 $\lambda_i$ 称为**坐标 (coordinate)**，则称 $A$ 是 $V$ 的**生成集**或**张成集**，记作 $\text{Span}(A) = V$ 或 $A$ spans $V$。

### 6.2 基 (Basis) - 最小生成集

$A$ 是 $V$ 的**最小生成集**（即**基**），如果：

1. $A$ 是 $V$ 的生成集
2. 不存在 $A' \subset A$ 使得 $A'$ spans $V$

### 6.3 要点总结

1. **基**: 能够张成 $V$ 的线性无关向量的最小集合
2. **一般情况**: 生成集中的向量可能是线性相关的
3. **维数 (Dimension)**: 基向量的数量，记作 $\text{dim}(V)$

---

## 7. 线性映射 (Linear Mapping)

### 7.1 矩阵乘法的另一种视角

考虑矩阵乘法 $W\vec{x}$，其中 $\vec{x} := [x_1, x_2, x_3]^T$：

$$
\begin{bmatrix}
W_{11} & W_{12} & W_{13} \\
W_{21} & W_{22} & W_{23} \\
W_{31} & W_{32} & W_{33}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
x_3
\end{bmatrix}
= x_1 \begin{bmatrix} W_{11} \\ W_{21} \\ W_{31} \end{bmatrix}
+ x_2 \begin{bmatrix} W_{12} \\ W_{22} \\ W_{32} \end{bmatrix}
+ x_3 \begin{bmatrix} W_{13} \\ W_{23} \\ W_{33} \end{bmatrix}
$$

**关键观察**:
- $W\vec{x}$ 是 $W$ 的列向量的线性组合
- $W\vec{x}$ 位于 $W$ 的**列空间 (column space)** 中
- $W\vec{x}$ 是从向量空间 $V$ 到 $W$ 的列空间的**线性变换**

### 7.2 线性映射的定义

给定两个向量空间 $V, W$，映射 $\phi: V \to W$ 是**线性映射**，如果：

$$
\forall \vec{x}, \vec{y} \in V, \forall \lambda, \varphi \in \mathbb{R}, \quad \phi(\lambda \vec{x} + \varphi \vec{y}) = \lambda \phi(\vec{x}) + \varphi \phi(\vec{y})
$$

**特殊情况**:

1. **加法保持**: 当 $\lambda = \varphi = 1$ 时，$\phi(\vec{x} + \vec{y}) = \phi(\vec{x}) + \phi(\vec{y})$
2. **标量乘法保持**: 当 $\varphi = 0, \lambda = 1$ 时，$\phi(\lambda \vec{x}) = \lambda \phi(\vec{x})$

### 7.3 线性映射的性质

- **线性映射保持向量空间的结构**
- **线性映射与向量空间运算的顺序可以交换**

这意味着线性映射是"结构保持"的映射，它将一个向量空间的结构映射到另一个向量空间。

---

## 总结

### 核心概念关系

```
群 (Group)
  └─> 阿贝尔群 (Abelian Group)
       └─> 向量空间 (Vector Space)
            ├─> 向量子空间 (Subspace)
            ├─> 线性组合 (Linear Combination)
            ├─> 线性相关性 (Linear Dependency)
            ├─> 生成集 (Spanning Set)
            └─> 基 (Basis)

线性映射 (Linear Mapping)
  └─> 保持向量空间结构
       └─> 矩阵乘法是线性映射的表示
```

### 关键要点

1. **向量空间**是配备向量加法和标量乘法的集合，满足8条公理
2. **基**是线性无关向量的最小生成集，其大小定义了空间的**维数**
3. **线性映射**保持向量空间的结构，可以交换运算顺序
4. **仿射映射** = 线性映射 + 平移（$y = Wx + b$）

---

## 参考资料

- 课程幻灯片: `20260123&20260126 Slides.pdf`
- 相关教材: Mathematics for Machine Learning (Deisenroth, Faisal, Ong)

---

**最后更新**: 2026年1月26日

