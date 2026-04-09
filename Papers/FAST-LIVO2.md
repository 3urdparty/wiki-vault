---
type: Paper
tags:
  - SLAM
  - Odometry
  - ESIKF
  - VIO
  - LIO
  - LIVO
  - Sensor-Fusion
url: https://arxiv.org/pdf/2408.14035
status: read
---

|                        |                                                                      |
| ---------------------- | -------------------------------------------------------------------- |
| $\boxplus / \boxminus$ | boxplus and boxminus operations on the state [[Manifolds\|manifold]] |
| $G(.)$                 | Vector . in global world frame                                       |
![[Pasted image 20260409150510.png|373]]

![[Pasted image 20260409150016.png]]
![[Pasted image 20260409150036.png|300]]

Discrete state transition model at the $i$-th IMU measurement is:
$x_{i+1} = x_i \ \boxplus \ (\Delta t f(x_i, u_i, w_i))$
where $\Delta t$ is the IMU sample period, state $x$, input $u$, process noise $w$, and function $f$ are:

The [[Manifolds|manifold]] $\mathcal{M}$ is the space containing all passible values for $\mathrm{x}$. It is a space with $\mathrm{dim}(\mathcal{M} = 19)$ as it is a combination of the space of all possible rotation matrices $SO(3)$, and ..
$\mathcal{M} \triangleq \begin{bmatrix}SO(3) \times \mathbb{R}^{16} \end{bmatrix}$

$\mathrm{x} \triangleq \begin{bmatrix} \prescript{G}{}{\mathrm{R}_I^T } & \prescript{G}{}{\mathrm{p}^T_I} & \prescript{G}{}{\mathrm{v}^T_I} &  \mathrm{b}_g^T & \mathrm{b}_a^T & \prescript{G}{}{\mathrm{g}^T} & \tau  \end{bmatrix} \in \mathcal{M}$
$\mathrm{u} \triangleq \begin{bmatrix}  \omega^T_m  & \mathrm{a}_m^T \end{bmatrix}^T$
$\mathrm{w} \triangleq \begin{bmatrix} \mathrm{n}^T_g & \mathrm{n}^T_a & \mathrm{n}^T_{b_g} & \mathrm{n}^T_{b_a} & \mathrm{n}^\tau \end{bmatrix}$

$\prescript{G}{}{\mathrm{R}^T_I}$ : IMU Attitude in $\mathrm{G}$
$\prescript{G}{}{\mathrm{p}^T_I}$ : IMU position  in $\mathrm{G}$
$\prescript{G}{}{\mathrm{v}^T_I}$ : IMU velocity  in $\mathrm{G}$

$\prescript{G}{}{\mathrm{g}^T}$ : Gravity vector in $G$ 
$\tau$ : inverse camera exposure time relative to first frame, $n^\tau$ is the gaussian noise that models $\tau$ as random walk
$\omega^T_m$ and $a_m^T$ are raw IMU measurements and $n^T_g$ and $n^T_a$ are noise in IMU  

$\mathrm{b}_g^T$ and $\mathrm{b}_g^T$ are biases in IMU, modelled as random walk driven by gaussian noise $n^T_{b_g}$ and $n^T_{b_a}$


1 Scan recombination to synchronize LiDAR and image data at the camera rate
2 Forward propagation to obtain state prediction $\hat{\mathrm{x}}$ and its covariance $\hat{\mathrm{P}}$
3 Backward propagation for LiDAR points motion compensation
4 // Point-to-plane LiDAR update
5 $\mathcal{K}=−1$, $\hat{x}^{\mathcal{k}=0}=\hat{x}$ ;
6 repeat
7 κ= κ+ 1;
8 Compute residual zκ l and Jacobin Hκl ;
9 Compute the state update xκ+1;
10 until ∥xκ+1 ⊟xκ∥<ϵ;
11 x = xκ+1, P = (I−KH) P;
12 // Sparse direct visual update
13 level=−1;
14 repeat
15 κ=−1, xκ=0 = x;
16 level= level+ 1;
17 repeat
18 κ= κ+ 1;
19 Compute residual zκc and Jacobin Hκc;
20 Compute the state update xκ+1;
21 until ∥xκ+1 ⊟xκ∥<ϵ;
22 x = xκ+1;
23 until level>= 2;
24x = xκ+1;¯
P = (I−KH) P.

**Scan recombination**: Segment sequentially sampled LiDar points into distinct LiDAR scans at camera sampling timestamps

**Backward Propogation**: Motion between $t_{k-1}$ and $t_k$ distort the LiDAR scans. To compensate, we perform backward propogation to transform them based on how it moved since $t_{k-1}$ 

**Propagation**: propagate $\bar{x}_{k-1}$ (state from last LiDAR scan + image frame received) and $P$ (covariance) from time $t_{k-1}$ to $t_k$ (predict state after each IMU input $u_i$ during $t_{k-1}$ and $t_k$, by setting process noise $\mathrm{w}_i$ to 0). 
Propogated state, $\hat{\mathrm{x}}$ and propagated covariance $\hat{\mathrm{P}}$


**Sequential Update**
$\mathrm{x} \ \boxminus \ \widehat{\mathrm{x}} \sim \mathcal{N}(0, \widehat{\mathbf{P}})$ (the uncertainty in $\mathbf{x}$ is modeled as a normal distribution)
$p(\mathbf{x})$ : uncertainty distribution in $\mathbf{x}$
measurement models:
$\begin{bmatrix} \mathbf{y}_l \\ \mathbf{y}_c  \end{bmatrix} = \begin{bmatrix} \mathbf{h}_l (\mathbf{x}, \mathbf{v}_l) \\ \mathbf{h}_c (\mathbf{x}, \mathbf{v}_c) \end{bmatrix}$, where $\mathbf{v}_l \sim \mathcal{N}(\mathbf{0}, \sum_{\mathbf{v}_l})$






