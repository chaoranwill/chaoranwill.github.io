---
layout:     post
title:      "Computational Models for Social Network Analysis"
subtitle:   "Ideas and process"
date:       2018-05-02 22:00:00
author:     "Chaoran"
header-img: "img/post-bg-name-dis.jpg"
noToc:      true
tags:
    - 论文阅读
---

> “To be a better girl ”

* 目录
{:toc #toc}

## 1. History of SNA
#### 1.1. Background
![history](/img/in-post/post-paper-cm-sna/history.png)

#### 1.2. Roadmap
![roadmap](/img/in-post/post-paper-cm-sna/roadmap.png)

#### 1.3. Example
* Example in AMiner
* Expert Search
* Researcher Profile
* Collaboration Recommendation
    - sparse connection

        比较难找到跨学科的合作者
    - topic skewness
    
        not all topics are relevant for crossdomain collaborations
* Reviewer Suggestion

## 2. Social Tie and Social Influence
![space](/img/in-post/post-paper-cm-sna/space.png)
* finding boss in email networks
* finding friends in mobile networks

    挑战：
    - 背后的作用力（fundamental forces ）
    - 是否可以自动推断社会纽带类型

#### 2.1. social tie
**Problem Formulation**
![problem](/img/in-post/post-paper-cm-sna/problem.png)
* input--social network（partially labeled）

    包含用户集合，部分标记
* objective--learn a mapping function（predict the relationship semantics）

    不仅要考虑已标记信息，也要考虑未标记的网络结构

**basic idea**
![basic idea](/img/in-post/post-paper-cm-sna/basic-idea.png)
two ways
* model each user as a node 
* model each relationship as a node 

*第一种更加直观，但难以描述不同关系间的关系*
![plp-fgm](/img/in-post/post-paper-cm-sna/plp-fgm.png)
目标： 对于每一个关系，识别最有可能的类型
* 左边为input，右边是模型
* 对每一个关系节点，都有一个相关潜在变量y，表示该关系的类型
* 三个因子
    - is attribute factor
    - correlation factor
    - constraint factor

**solutions**
* exponential-linear functions
* Log-Likelihood of labeled Data
![Log-Likelihood](/img/in-post/post-paper-cm-sna/Log-Likelihood.png)

**challenge**
* 更有效的训练数据
* 从其他网络借鉴



#### 2.2. Inferring Social Ties across Heterogeneous Networks
#### social theories
* social balance theory
* structural hole theory
* social status theory
* two-step-flow theory
![Transfer Factor Graph Model](/img/in-post/post-paper-cm-sna/graph-model.png)


####2.3. Peer Influence
* Formulation: Topic-based Social Influence Analysis
    - The Solution: Topical Affinity Propagation
![Transfer Factor Graph Model](/img/in-post/post-paper-cm-sna/tfgm.png)

#### 2.4. Structural Influence
Influence
* Peer influence
* Conformity influence
* Individual influence


## 3. Group and Structure [slides]
* Group Lyfecyle
* Structural Hole in Diffusion

[Computational Models for Social Network Analysis](http://keg.cs.tsinghua.edu.cn/jietang/www17tutorial-sna.html)
