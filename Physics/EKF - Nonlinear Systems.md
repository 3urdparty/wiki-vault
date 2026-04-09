

Most real systems aren't linear. For a robot in 3D, orientation involves **sin and cos** (rotation matrices, quaternions). That breaks the linear assumption.

EKF's solution: at each timestep, **locally approximate** the nonlinear function as linear by computing its derivative — the Jacobian. So yes, if your function has quadratic, cubic, trig, or any nonlinear terms, the Jacobian gives a linear approximation valid near the current operating point.