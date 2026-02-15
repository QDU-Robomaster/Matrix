# Matrix

## 1. 模块作用
矩阵数学基础模块。为控制与估计模块提供固定维度矩阵运算能力。

## 2. 主要函数说明
1. Matrixf 类: 提供加减乘除、Block、Row、Col 操作。
2. Trans / Trace / Norm: 常用矩阵运算接口。
3. matrixf::zeros / ones / eye / diag / inv: 常用构造与求逆工具。

## 3. 接入步骤
1. 该模块通常作为基础库被 include 使用。
2. 在业务模块中直接使用 Matrixf 与 matrixf 命名空间函数。
3. 无需单独创建 Application 实例。
