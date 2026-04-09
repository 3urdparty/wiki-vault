### UKF — Unscented Kalman Filter

Instead of linearizing (which introduces approximation error), UKF asks: _what if I just propagated a carefully chosen set of points through the actual nonlinear function?_

**Sigma points** are a small, deterministic set of sample points (typically 2n+1 for an n-dimensional state) chosen to exactly capture the mean and covariance of your current estimate. You push all of them through the true nonlinear function, then fit a Gaussian to the outputs.

The result: better nonlinear approximation than EKF, no Jacobians needed — but more computationally expensive.