
# 1. xgboost

## 1.1. install

        conda install -c anaconda py-xgboost 

## 1.2. [论文](https://arxiv.org/pdf/1603.02754v1.pdf)

## 1.3. 官网

[e](https://xgboost.readthedocs.io/en/latest/tutorials/model.html)

https://xgboost.apachecn.org/#/docs/3

### 1.3.1. 参数调整注意事项

参数调整是机器学习中的一门暗艺术，模型的最优参数可以依赖于很多场景。所以要创建一个全面的指导是不可能的。

本文档试图为 xgboost 中的参数提供一些指导意见。

#### 理解 Bias-Variance（偏差-方差）权衡

如果你了解一些机器学习或者统计课程，你会发现这可能是最重要的概念之一。 当我们允许模型变得更复杂（例如深度更深）时，模型具有更好的拟合训练数据的能力，会产生一个较少的偏差模型。 但是，这样复杂的模型需要更多的数据来拟合。

xgboost 中的大部分参数都是关于偏差方差的权衡的。最好的模型应该仔细地将模型复杂性与其预测能力进行权衡。 参数文档 会告诉你每个参数是否会使得模型更加conservative （保守）与否。这可以帮助您在复杂模型和简单模型之间灵活转换。

#### 控制过拟合

当你观察到训练精度高，但是测试精度低时，你可能遇到了过拟合的问题。

通常有两种方法可以控制 xgboost 中的过拟合。
1. 直接控制模型的复杂度,这包括 max_depth, min_child_weight 和 gamma
2. 增加随机性，使训练对噪声强健,这包括 subsample, colsample_bytree;你也可以减小步长 eta, 但是当你这么做的时候需要记得增加 num_round 。

#### 处理不平衡的数据集

对于广告点击日志等常见情况，数据集是极不平衡的。 这可能会影响 xgboost 模型的训练，有两种方法可以改善它。
1. 如果你只关心预测的排名顺序（AUC）
        通过 scale_pos_weight 来平衡 positive 和 negative 权重。
        使用 AUC 进行评估
2. 如果你关心预测正确的概率
        在这种情况下，您无法重新平衡数据集
        在这种情况下，将参数 max_delta_step 设置为有限数字（比如说1）将有助于收敛

### 


XGBoost python 模块能够使用以下方式加载数据:

    libsvm txt format file（libsvm 文本格式的文件）
    Numpy 2D array, and（Numpy 2维数组, 以及）
    xgboost binary buffer file. （xgboost 二进制缓冲文件）


libsvm格式：<label> <index1>:<value1> <index2>:<value2> ...


