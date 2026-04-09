System to describe multi-joint robot state. $H$ describes the transform from frame $n-1$ to $n$
$H_i = R(Z_i, O_i) \cdot T(Z_i, d_i) \cdot T(X_i, a_i) \cdot R(X_i, \alpha_i)$
Expanded:

$H_i^{i-1}(\theta_i, d_i, a_i, \alpha_i) = \begin{bmatrix} \cos(\theta_i) & -\sin(\theta_i)\cos(\alpha_i) & \sin(\theta_i)\sin(\alpha_i) & a_i\cos(\theta_i) \\ \sin(\theta_i) & \cos(\theta_i)\cos(\alpha_i) & -\cos(\theta_i)\sin(\alpha_i) & a_i\sin(\theta_i) \\ 0 & \sin(\alpha_i) & \cos(\alpha_i) & d_i \\ 0 & 0 & 0 & 1 \end{bmatrix}$
Block matrix form:
$H_i^{i-1}(\theta_i, d_i, a_i, \alpha_i) = \begin{bmatrix} R_i^{i-1} & d_i^{i-1} \\ 0 & 1 \end{bmatrix}$
$R_i^{i-1}$ - 3x3 rotation matrix
$d_i^{i-1}$ - 3x1 translation 

