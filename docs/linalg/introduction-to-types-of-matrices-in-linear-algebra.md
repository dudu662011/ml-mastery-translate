# 用于机器学习的线性代数中的矩阵类型简介

> 原文： [https://machinelearningmastery.com/introduction-to-types-of-matrices-in-linear-algebra/](https://machinelearningmastery.com/introduction-to-types-of-matrices-in-linear-algebra/)

许多线性代数涉及向量和矩阵的运算，并且存在许多不同类型的矩阵。

在线性代数入门时，您可能会遇到几种类型的矩阵，特别是与机器学习相关的线性代数部分。

在本教程中，您将发现一系列不同类型的矩阵，这些矩阵来自线性代数领域，您可能会在机器学习中遇到这些矩阵。

完成本教程后，您将了解：

*   正方形，对称，三角形和对角矩阵，正如它们的名字所暗示的那样。
*   除了沿值为 1 的主对角线以外的所有零值的标识矩阵。
*   正交矩阵，概括了垂直向量的概念并具有有用的计算属性。

让我们开始吧。

*   **更新 Feb / 2018** ：修正了正交矩阵等价方程中的小错字。

![A Gentle Introduction to Types of Matrices in Linear Algebra](img/ba987b1139b049cdf8ad2efdd0b63d5e.jpg)

线性代数中矩阵类型的温和介绍
[Tony](https://www.flickr.com/photos/triplea4/15206281696/) 的照片，保留一些权利。

## 教程概述

本教程分为 6 个部分，涵盖了主要的矩阵类型;他们是：

1.  方阵
2.  对称矩阵
3.  三角矩阵
4.  对角矩阵
5.  身份矩阵
6.  正交矩阵

## 方阵

方阵是矩阵，其中行数（n）等于列数（m）。

```
n = m
```

方矩阵与矩形矩阵形成对比，矩形矩阵的行数和列数不相等。

假设行数和列数匹配，则尺寸通常表示为 n，例如 n x n。矩阵的大小称为顺序，因此 4 阶矩阵是 4 x 4。

沿着从左上到右下的矩阵对角线的值向量称为主对角线。

以下是 3 阶矩阵的示例。

```
     1, 2, 3
M = (1, 2, 3)
     1, 2, 3
```

方形矩阵很容易相加并相乘，并且是许多简单线性变换的基础，例如旋转（如图像的旋转）。

## 对称矩阵

对称矩阵是一种方形矩阵，其中右上角三角形与左下角三角形相同。

> 毫不夸张地说，对称矩阵 S 是世界上最重要的矩阵 - 在线性代数理论和应用中。

- 第 338 页，[线性代数导论](http://amzn.to/2AZ7R8j)，第五版，2016 年。

为了对称，对称轴始终是矩阵的主要对角线，从左上角到右下角。

下面是 5×5 对称矩阵的示例。

```
     1, 2, 3, 4, 5
     2, 1, 2, 3, 4
M = (3, 2, 1, 2, 3)
     4, 3, 2, 1, 2
     5, 4, 3, 2, 1
```

对称矩阵总是正方形并且等于它自己的转置。

```
M = M^T
```

## 三角矩阵

三角矩阵是一种方矩阵，其在矩阵的右上或左下具有所有值，其余元素填充零值。

仅在主对角线上方具有值的三角矩阵称为上三角矩阵。然而，仅在主对角线下方具有值的三角矩阵被称为下三角矩阵。

下面是 3×3 上三角矩阵的示例。

```
     1, 2, 3
M = (0, 2, 3)
     0, 0, 3
```

下面是 3×3 下三角矩阵的示例。

```
     1, 0, 0
M = (1, 2, 0)
     1, 2, 3
```

LU 分解将给定矩阵解析为上三角矩阵和下三角矩阵。

NumPy 提供从现有方阵中计算三角矩阵的函数。 tril（）函数用于从给定矩阵计算下三角矩阵，triu（）用于从给定矩阵计算上三角矩阵

下面的例子定义了一个 3×3 方阵，并从中计算出下三角矩阵和上三角矩阵。

```
# triangular matrices
from numpy import array
from numpy import tril
from numpy import triu
M = array([[1, 2, 3], [1, 2, 3], [1, 2, 3]])
print(M)
lower = tril(M)
print(lower)
upper = triu(M)
print(upper)
```

运行该示例将打印定义的矩阵，然后是下三角矩阵和上三角矩阵。

```
[[1 2 3]
 [1 2 3]
 [1 2 3]]

[[1 0 0]
 [1 2 0]
 [1 2 3]]

[[1 2 3]
 [0 2 3]
 [0 0 3]]
```

## 对角矩阵

对角矩阵是主对角线外部的值具有零值的矩阵，其中主对角线从矩阵的左上角到右下角。

对角矩阵通常用变量 D 表示，并且可以表示为完整矩阵或主对角线上的值向量。

> 对角矩阵主要由零组成，并且仅沿主对角线具有非零条目。

- 第 40 页，[深度学习](http://amzn.to/2B3MsuU)，2016 年。

下面是 3×3 方形对角矩阵的示例。

```
     1, 0, 0
D = (0, 2, 0)
     0, 0, 3
```

作为向量，它将表示为：

```
d = (d11, d22, d33)
```

或者，使用指定的标量值：

```
d = (1, 2, 3)
```

对角矩阵不必是正方形。在矩形矩阵的情况下，对角线将覆盖最短的维度;例如：

```
     1, 0, 0, 0
     0, 2, 0, 0
D = (0, 0, 3, 0)
     0, 0, 0, 4
     0, 0, 0, 0
```

NumPy 提供了函数 diag（），它可以从现有矩阵创建对角矩阵，或者将向量转换为对角矩阵。

下面的示例定义了一个 3×3 方阵，将主对角线提取为向量，然后从提取的向量中创建一个对角矩阵。

```
# diagonal matrix
from numpy import array
from numpy import diag
M = array([[1, 2, 3], [1, 2, 3], [1, 2, 3]])
print(M)
# extract diagonal vector
d = diag(M)
print(d)
# create diagonal matrix from vector
D = diag(d)
print(D)
```

首先运行该示例打印定义的矩阵，然后是主对角线的向量和从向量构造的对角矩阵。

```
[[1 2 3]
 [1 2 3]
 [1 2 3]]

[1 2 3]

[[1 0 0]
 [0 2 0]
 [0 0 3]]
```

## 身份矩阵

单位矩阵是一个方形矩阵，在乘法时不会改变向量。

单位矩阵的值是已知的。沿主对角线（左上角到右下角）的所有标量值都具有值 1，而所有其他值都为零。

> 单位矩阵是当我们将该向量乘以该矩阵时不改变任何向量的矩阵。

- 第 36 页，[深度学习](http://amzn.to/2B3MsuU)，2016 年。

单位矩阵通常使用符号“I”或维度“In”表示，其中 n 是表示方形单位矩阵的维数的下标。在一些符号中，标识可以被称为单位矩阵或“U”，以兑现它包含的一个值（这与单位矩阵不同）。

例如，大小为 3 或 I3 的单位矩阵如下：

```
     1, 0, 0
I = (0, 1, 0)
     0, 0, 1
```

在 NumPy 中，可以使用 identity（）函数创建具有特定大小的单位矩阵。

以下示例创建 I3 单位矩阵。

```
# identity matrix
from numpy import identity
I = identity(3)
print(I)
```

运行该示例将打印创建的标识矩阵。

```
[[ 1\.  0\.  0.]
 [ 0\.  1\.  0.]
 [ 0\.  0\.  1.]]
```

单独，单位矩阵并不那么有趣，尽管它是其他导入矩阵运算中的一个组件，例如矩阵求逆。

## 正交矩阵

当它们的点积等于零时，两个向量是正交的，称为正交。

```
v . w = 0
```

要么

```
v . w^T = 0
```

当我们认为一条线与另一条线垂直于它时，这是直观的。

正交矩阵是一种方形矩阵，其列和行是正交单位向量，例如，正交矩阵。垂直，长度或大小为 1。

> 正交矩阵是方形矩阵，其行是相互正交的并且其列是相互正交的

- 第 41 页，[深度学习](http://amzn.to/2B3MsuU)，2016 年。

正交矩阵通常表示为大写“Q”。

> 通过正交矩阵的乘法保留长度。

- 第 277 页，[无线性代数废话指南](http://amzn.to/2k76D4C)，2017 年

正交矩阵的形式正式定义如下：

```
Q^T . Q = Q . Q^T = I
```

其中 Q 是正交矩阵，Q ^ T 表示 Q 的转置，I 是单位矩阵。

如果矩阵的转置等于其反转，则矩阵是正交的。

```
Q^T = Q^-1
```

正交矩阵的另一个等价是矩阵和它自身的点积等于单位矩阵。

```
Q . Q^T = I
```

正交矩阵用于线性变换，例如反射和置换。

下面列出了简单的 2×2 正交矩阵，其是反射矩阵或坐标反射的示例。

```
     1,  0
Q = (0, -1)
```

下面的示例创建此正交矩阵并检查上述等价。

```
# orthogonal matrix
from numpy import array
from numpy.linalg import inv
Q = array([[1, 0], [0, -1]])
print(Q)
# inverse equivalence
V = inv(Q)
print(Q.T)
print(V)
# identity equivalence
I = Q.dot(Q.T)
print(I)
```

首先运行该示例打印正交矩阵，正交矩阵的逆，然后打印正交矩阵的转置并且显示为等效的。最后，打印单位矩阵，其由正交矩阵的点积与其转置计算。

```
[[ 1  0]
 [ 0 -1]]

[[ 1  0]
 [ 0 -1]]

[[ 1\.  0.]
 [-0\. -1.]]

[[1 0]
 [0 1]]
```

正交矩阵是有用的工具，因为它们在计算上是便宜的并且可以稳定地计算它们的逆，就像它们的转置一样。

## 扩展

本节列出了一些扩展您可能希望探索的教程的想法。

*   使用您自己的小型人为数据修改每个示例。
*   编写自己的函数来实现每个操作。
*   研究一个例子，其中每个操作都用于机器学习。

如果你探索任何这些扩展，我很想知道。

## 进一步阅读

如果您希望深入了解，本节将提供有关该主题的更多资源。

### 图书

*   第 6.2 节特殊类型的矩阵。 [线性代数无废话指南](http://amzn.to/2k76D4)，2017 年。
*   [线性代数](http://amzn.to/2j2J0g4)简介，2016 年。
*   第 2.3 节身份和反向矩阵，[深度学习](http://amzn.to/2B3MsuU)，2016 年。
*   第 2.6 节特殊种类的矩阵和向量，[深度学习](http://amzn.to/2B3MsuU)，2016。

### API

*   [numpy.tril（）API](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.tril.html)
*   [numpy.triu（）API](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.triu.html)
*   [numpy.diag（）API](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.diag.html)
*   [numpy.identity（）API](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.identity.html)

### 用品

*   [维基百科上的方阵](https://en.wikipedia.org/wiki/Square_matrix)
*   [维基百科上的主对角线](https://en.wikipedia.org/wiki/Main_diagonal)
*   [维基百科上的对称矩阵](https://en.wikipedia.org/wiki/Symmetric_matrix)
*   [维基百科上的三角矩阵](https://en.wikipedia.org/wiki/Triangular_matrix)
*   [维基百科上的对角矩阵](https://en.wikipedia.org/wiki/Diagonal_matrix)
*   维基百科上的[身份矩阵](https://en.wikipedia.org/wiki/Identity_matrix)
*   维基百科上的[正交矩阵](https://en.wikipedia.org/wiki/Orthogonal_matrix)

## 摘要

在本教程中，您发现了一组来自线性代数领域的不同类型的矩阵，您可能会在机器学习中遇到这些矩阵。

具体来说，你学到了：

*   正方形，对称，三角形和对角矩阵，顾名思义。
*   除了沿值为 1 的主对角线以外的所有零值的标识矩阵。
*   正交矩阵，概括了垂直向量的概念并具有有用的计算属性。

你有任何问题吗？
在下面的评论中提出您的问题，我会尽力回答。