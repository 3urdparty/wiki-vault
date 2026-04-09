### Gaussian Noise

Yes — it follows a bell curve. The assumption is that sensor errors are:

- Centered around zero (no systematic bias)
- Most errors are small, large errors are rare
- Fully described by a mean and variance (σ²)

This matters because the Kalman filter's math is derived specifically assuming this shape. If your noise is wildly non-Gaussian (e.g., spike outliers), the filter degrades.

[![Gaussian_Noise](https://www.sfu.ca/sonic-studio-webdav/handbook/Graphics/Gaussian.gif)![Gaussian_Noise](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgGZpcXMl0JWQCbLR9BAORoyF3cw2sobTP8Q&s)](https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.sfu.ca%2Fsonic-studio-webdav%2Fhandbook%2FGaussian_Noise.html&ved=0CBYQjRxqFwoTCJj66J3y2pMDFQAAAAAdAAAAABAI&opi=89978449)