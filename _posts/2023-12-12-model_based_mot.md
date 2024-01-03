---
layout: post
title: A Demo of MOT Tutorial use Matlab2023
date: 2023-12-31 22:25:00
description: this is a post of my main study.
tags: MOT
categories: learn-posts
related_posts: false
toc:
  sidebar: left
---

## 引言

这是一个多目标跟踪例程，建立在运动模型和卡尔曼滤波的基础上的实现。

## 模型构建

首先我们明确系统的运动模型为：

$$
\mathrm{x}_{t} = [ 
    x_t,y_t,\phi_t,v_t,\omega_t
]
$$

根据运动模型:

$$
\begin{cases}
\dot{x} =v_x=v cos(\phi+\gamma ) \\
\dot{y}=v_y=vsin(\phi+\gamma ) 
\end{cases}
$$

$$
\begin{cases}
v_{xv}=v cos(\gamma ) \\
v_{yv}=v sin(\gamma )
\end{cases}
$$

$$
\dot{\phi}=\frac{v_{yv}}{L}=\frac{vsin(\gamma)}{L}
$$

所以车体的运动模型是:

$$
\begin{cases}
\dot{x}=v cos(\phi+\gamma ) \\
\dot{y}=vsin(\phi+\gamma ) \\
\dot{\phi}=\frac{vsin(\gamma)}{L}
\end{cases}
$$

离散化得:

$$
\begin{cases}
  \frac{x_{k+1}-x_{k}}{\Delta T}=v_{k+1}cos(\phi_{k}+\gamma_{k+1})  \\
  \frac{y_{k+1}-y_{k}}{\Delta T}=v_{k+1}sin(\phi_{k}+\gamma_{k+1})  \\
  \frac{\phi_{k+1}-\phi_{k}}{\Delta T}=\frac{v_{k+1}sin(\gamma_{k+1})}{L}      
\end{cases}
$$

转为迭代的形式就是:

$$
\begin{cases}
  x_{k+1} = x_k + \Delta Tv_{k+1}cos(\phi_k + \gamma_{k+1}) + q_{x_{k+1}} \\
  y_{k+1} = y_k + \Delta Tv_{k+1}sin(\phi_k + \gamma_{k+1}) + q_{y_{k+1}} \\
  \phi_{k+1} = \phi_{k} + \frac{\Delta T v_{k+1}sin(\gamma_{k+1})}{L} + q_{\phi_{k+1}}     
\end{cases}
$$

写为矩阵的形式就是:

$$
\begin{bmatrix}
    x_{k+1} \\
    y_{k+1} \\
    \phi_{k+1}
\end{bmatrix} = 

\begin{bmatrix}
    x_{k} \\
    y_{k} \\
    \phi_{k} 
\end{bmatrix} +

\begin{bmatrix}
    \Delta Tv_{k+1}cos(\phi_k + \gamma_{k+1}) \\
    \Delta Tv_{k+1}sin(\phi_k + \gamma_{k+1}) \\
    \frac{\Delta T v_{k+1}sin(\gamma_{k+1})}{L}
\end{bmatrix} +

\begin{bmatrix}
    q_{x_{k+1}} \\
    q_{y_{k+1}} \\
    q_{\phi_{k+1}}   
\end{bmatrix}
$$

贴近真实模型需要对速度, 最大角度, 最大角速度等进行限制: 

$$
\begin{cases}
    |\gamma| < \gamma_{max} \\
    |\dot{\gamma}| < Rate_{max} \\
    v < v_{max}
\end{cases}
$$


如果对于一个多目标跟踪系统, 系统在时刻 $$t$$ 检测到 $$k$$ 辆车, 则对应的每辆车都有一个独立的运动模型. 所以需要有一个数据库保存所有跟踪到的每个 $$id$$ 的车辆的运动模型的信息. 且这个信息是随着系统的时间更新而更新的. 

对于车辆搭载的传感器, 这里为了简单我们假设传感器可以直接观测到目标点的 $$x,y$$ 坐标. 所以我们可以定义观测为:



$$
\mathrm{z}_{i_t} = 

\begin{bmatrix}
    x_t \\
    y_t \\
    \theta_t
\end{bmatrix}=

\begin{bmatrix}
    cos(\phi)x_i^w+sin(\phi)y_i^w - \sqrt{x_t^2+y_t^2} \\
    -sin(\phi)x_i^w+cos(\phi)y_i^w \\
    \phi_{t}-\phi_{i_{t}}
\end{bmatrix}
$$

上式的观测表示的是对 $$t$$ 时刻, 第 $$i$$ 个物体在智能车坐标系下的 $$x,y$$ 坐标. 


## 代码实现

```matlab
clc; % 清空
while

end

```

## 结果展示


