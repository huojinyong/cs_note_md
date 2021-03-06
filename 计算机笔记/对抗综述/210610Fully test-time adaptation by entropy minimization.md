---
title: 210610Fully test-time adaptation by entropy minimization
date: 2021-06-10 13:17
---

解决模型在不同数据分布的数据集之间的迁移问题。

# 1、INTRODUCTION  
**dataset shift**(数据集偏移)
我们注意到，在这两个阶段使用的数据集也不一样，分别是历史数据（historical data）与新数据（live data）。在机器学习中，很多模型都是假设数据的分布是一定的，不变的，即历史数据与将来的数据都服从相同的分布。但是，在现实生活中，这种假设往往是不成立的，即数据的分布会随着时间的移动而改变，有时甚至变化得很急剧，这种现象称为分布漂移。   

- training data(又称为source)
- testing data(又称为target)
在测试阶段，只需要给定 target data 和模型参数，模型就可以自适应(**adaptation**)，不需要 source data

虽然dataset shift 现象存在，但**在不同的数据分布上部署一个模型有时是必要的，因此 adaptation 是被需要的**。  **为了在测试时自适应，我们采用`模型预测的熵的最小化`**  
`orange:为了使熵最小，tent通过逐批估计统计量和优化仿射参数来归一化并转换对目标数据的推断。`    

熵越大，(分类)错误率越高:
![](./_image/2021-06-10/2021-06-10-15-19-23@2x.png)
(图像)损坏越多，熵越大，损失(loss)越大:
![](./_image/2021-06-10/2021-06-10-15-19-32@2x.png)
```mermaid
graph TB
id1("在不同的数据分布上部署一个模型") --> id2("dataset shift 现象存在") --> id3("需要 adaptation") --> id4("采用模型预测的熵的最小化") --> id("为了使熵最小，tent通过逐批估计统计量和优化仿射参数来归一化并转换对目标数据的推断")
```   

# 2、SETTING: FULLY TEST-TIME ADAPTATION
**领域自适应(Domain Adaptation)**
"首先Domain Adaptation基本思想是既然源域和目标域数据分布不一样，那么就把数据都映射到一个特征空间中，在特征空间中找一个度量准则，使得源域和目标域数据的特征分布尽量接近，于是基于源域数据特征训练的判别器，就可以用到目标域数据上。"来自[迁移学习_知乎](https://zhuanlan.zhihu.com/p/50710267)  

"cross-domain loss L(xs , xt )"
说明 domain 就是 s 和 t。

**测试时训练(TEST-TIME TRAINING)**
来自[TEST-TIME TRAINING_知乎](https://zhuanlan.zhihu.com/p/93641365)   

