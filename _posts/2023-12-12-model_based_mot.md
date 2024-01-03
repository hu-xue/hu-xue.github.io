---
layout: post
title: A Demo of MOT Tutorial use Matlab2023
date: 2023-12-31 22:25:00
description: this is what included TikZ code could look like
tags: MOT
categories: learn-posts
tikzjax: true
---

## 引言

这是一个多目标跟踪例程，建立在运动模型和卡尔曼滤波的基础上的实现。

## 模型构建

首先我们明确系统的运动模型为：

$$
\mathrm{x}_{t} = [ 
    x_t,y_t,\theta_t,v_t,\omega_t
]
$$

根据运动模型:

$$

$$

然后我们系统的控制量是

$$
\mathrm{u}_t= [
    v_t, \omega_t
]
$$

如果对于一个多目标跟踪系统, 系统在时刻 $$t$$ 检测到 $$k$$ 辆车, 则对应的每辆车都有一个独立的运动模型. 所以需要有一个数据库保存所有跟踪到的每个 $$id$$ 的车辆的运动模型的信息. 且这个信息是随着系统的时间更新而更新的. 

对于车辆搭载的传感器, 这里为了简单我们假设传感器可以直接观测到目标点的 $$x,y$$ 坐标. 所以我们可以定义观测为:

$$
\mathrm{z}_t= [x_t,y_t]
$$



## 代码实现



## 结果展示


