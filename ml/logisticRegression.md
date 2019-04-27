

# 概述

1. 特点：
    - 优点：模型简单，可解释性强；计算代价不高，易于理解实现
    - 缺点：容易欠拟合，精度不高
2. 给定样本$\vec x$，其中$\vec x=(x_1,x_2,\dots,x_n)^T$,$x_i$为样本的第i个特征，特征n种，linear的形式

$$f(\vec x)=\vec w \cdot \vec x + b$$

2. sigmoid函数

$$\sigma(z)=\frac{1}{1+e^{-z}}$$

