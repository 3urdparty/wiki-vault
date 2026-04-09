It's the **matrix of partial derivatives** of a vector-valued function. If your function maps a 6D state to a 3D measurement, the Jacobian is a 3×6 matrix where each entry is ∂output_i/∂input_j.

Geometrically: it tells you the _local slope_ of a curved function — essentially fitting a flat plane tangent to the curve at the current point. The EKF uses this tangent plane as its linearization.