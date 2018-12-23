---
layout: post
comments: true
title: "Deep Learn on Graphs简述"
date: 2017-06-21 01:09:00
tags: Review DeepLearn Graphs
image: "Deep Learn on Graphs简述.jpg"
---

> 近期工作的方向多集中在社交网络相关，结合之前在研究一些交通、NLP方面经验，觉得深度学习在Graphs方面会有比较大的应用。当然另一方面觉得但就个人业余研究而言图像、视频类似乎比较“无趣”，想试一下能否在Deep Learning on Graphs方面有所收货。本文将从Deep Learning on Graph目前主要研究方向的进展、这些方向之间的差异和相互组合以及潜在的应用和方向进行梳理。

<!--more-->

{: class="table-of-content"}
* TOC
{:toc}

---

## Deep Learn on Graphs的大概情况

大体上可以将Deep Learn on Graphs的方向分为半监督、非监督和一些比较新的尝试3大类，具体如图：

1. 半监督，如：Graph Neural Networks和Graph Convolutional Networks
2. 非监督，如：Graph Autoencoders
3. 前沿，如：Graph Recurrent Neural Networks和Graph Reinforcement Learning

<img src="http://ww1.sinaimg.cn/large/88162db8ly1fygshoty69j219v0aqglu.jpg"/>

## Deep Learn on Graphs的困难

1. Graph是一个irregular domain，，很难形成一些比较基础的、通用的计算规则和方法，比如关于convolution和pooling类的操作；
2. Graph类问题会有很多种数据结构和任务，关于graph可以分成同构/异构、有权/无权、有向/无向等，关于任务又可以分成关于节点或者关注图本身的学习任务
    <img src="http://ww1.sinaimg.cn/large/88162db8ly1fygsg413idj20ed0713ye.jpg"/>
3. Graph类问题的数据量往往很大，而且即使对一个node/edge进行计算也需要考虑整个graph，此外graph类问题的计算往往并行性要求高
4. 跨领域和跨专业，诸如在生物、化学、社交网络等都有很多的应用场景，不过这个倒也是选择研究这个领域的主要原因之一。