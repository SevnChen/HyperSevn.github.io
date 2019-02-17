---
layout: post
comments: true
title: "Graph Neural Network 基础"
date: 2018-12-13 01:09:00
tags: Review DeepLearn Graphs GNN
image: "Deep Learn on Graphs简述.jpg"
---

最近Graph Neural Network (GNN)热了起来，给网络分析、知识图谱、推荐系统、甚至是图像理解等领域带来了新的思路。这里简单介绍一下最基本的图神经网络模型，以及1个比较基础的算法（DeepWalk）。

<!--more-->

{: class="table-of-content"}
* TOC
{:toc}

---

这里就不再介绍Graph的内容了，默认已知。但做一点符号说明：
$$G=(V,E)$$
其中$G$就是图，就是我们研究的对象Graph，$V$是图中点（vertices/nodes），$E$是途中的边（edges）。

## 1. Graph Neural Network

Graph Neural Network也是Neural Network的一种，是神经网络再Graph数据结构中的一种应用。虽然由于Graph数据本身的复制和不确定性导致Graph Neural Network在操作和计算上有些特殊，但本质上的结构还是与传统的 Neural Network 没有太大差异。
### 1.1 任务

Graph Neural Network要解决的最经典的任务是`Node Classification`，传统的机器学习做法是对每个node构造本身的特征，然后带入模型中进行训练，但忽略了*物以类聚*。
在Node Classification任务中，每一个node都应该有一个label（实际上有部分node是缺失label的），现在我们的工作就是对于每个$node_v$，利用他自身的特征$x_v$以及关联node的真实label$t_v$去预测$node_v$的lable。
一句话：**对于给定部分节点label的Graph G，预测没有给定label的节点的真实label**。

### 1.2 模型

这个模型实际上是半监督的模型，利用灭个node的特征信息以及一部分一直label的node预测剩余node的label。

1. **每个node的表示**
    第一步需要学习如何通过node本身的信息以及邻近node的信息得到$d$维的向量，用以表示一个node。对于$node_v$：
    $$h_v=f(X_v,X_{co[v]},h_{ne[v]},x_{ne[v]})$$
    其中：
        - $x_v$：$node_v$的特征
        - $X_{co[v]}$：$node_v$的边的特征
        - $h_{ne[v]}$：$node_v$的邻接点的的嵌入（embedding）
        - $x_{ne[v]}$：$node_v$的邻接点的特征
        - $f$：将以上信息转换成d维空间的函数
2. **$h_v$的解**
    将上式根据Banach不动点定理改造成：
    $$H^{t+1}=F(H^t,X)$$
3. **输出node的预测label**
    $$o_v=g(h_v,x_v)$$
    $f$与$g$可以理解为前馈全连接的NN
4. **模型优化目标（损失函数）**
    $$loss=\sum_{i=1}^p(t_i-o_i)$$
    - 通过graditent dscent对这个目标函数进行优化
    - $loss$可以引入L1正则

### 1.3 模型局限

1. 可以使用多层感知机（MLP）去学习node的稳定表达。原模型中不同的迭代使用相同参数的$f$函数进行转换，而MLP可以在不同层使用不同的参数用以分层特征提取，当然这里可以将MLP设计成multi-layer GNN；
2. 没法处理edge上的信息；
3. 不动点回阻碍节点分布的多样性，不适合学习节点表示，因为不动点的表示分布在数值上很平滑，而且用以区分node的信息也很少。

## Pytorch实现

待续