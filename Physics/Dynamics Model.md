A dynamic model is a mathematical description of the relationship between the forces and torques applied to the joints and resulting motion (acceleration or velocity or position) accounting for physical properties, mass and [[Inertia|inertia]].


## Linear Dynamics
A system is linear if the next state is a **matrix multiplication** of the current state — no powers, no products of state variables, no trig functions. Example:

A car moving at constant velocity in 1D:

```
x_next = x + v·dt
v_next = v
```

In matrix form: **x** = **F** · **x**, where F is a simple 2×2 matrix. That's linear — the standard Kalman filter handles this exactly.