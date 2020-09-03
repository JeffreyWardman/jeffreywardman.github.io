---
title: "Visualizing the Mandelbrot Set"
published: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# High-definition Mandelbrot Set Visualization with CUDA in Python

The Mandelbrot set is a facinating component of fractal geometry and opened my eyes to more beauties such as the Julia set and Buddhabrot set.

Below is a high definition image and the code used to generate it. Written with numba, the code is reasonably fast, although it can definitely be sped up (e.g. iterating over a 1D array that's reshaped at the end).

Grab the code and have a play around with the colour maps, zoom in and look at the amazingness that is fractal geometry.

{: style="text-align:center"}
![mandelbrot_set](/assets/posts/mandelbrot-set/mandelbrot_set.png){:height="512px" width="512px"}

# Code

```
import matplotlib.pyplot as plt
import numba as nb
import numpy as np
from numba import cuda

@nb.jit
def mandelbrot*set(x: int, y: int, max_iters: int = 10):
c = complex(x, y)
z = 0.0j
for i in nb.prange(max_iters):
z = z**2 + c
if (z.real**2 + z.imag\*\_2) >= 4:
return (i << 21) + (i << 10) + i * 8 # i
return max_iters

@cuda.jit
def mandelbrot_kernel(img: cuda.cudadrv.devicearray.DeviceNDArray,
x_min: float,
x_max: float,
y_min: float,
y_max: float,
max_iters: int = 10):
height = img.shape[0]
width = img.shape[1]

    x_pixel_size = (x_max - x_min) / width
    y_pixel_size = (y_max - y_min) / height

    x_start, y_start = cuda.grid(2)
    x_grid = cuda.gridDim.x * cuda.blockDim.x
    y_grid = cuda.gridDim.y * cuda.blockDim.y

    for x in nb.prange(x_start, width, x_grid):
        real = x * x_pixel_size + x_min
        for y in nb.prange(y_start, height, y_grid):
            imaginary = y * y_pixel_size + y_min
            img[y, x] = mandelbrot_gpu(real, imaginary, max_iters)

dim_size = 2\*\*13
block_dim = (32, 8)
grid_dim = (32, 16)

mandelbrot_gpu = cuda.jit(device=True)(mandelbrot_set)
img_np = np.zeros((dim_size, dim_size), dtype=np.uint16)
img_cuda = cuda.to_device(img_np)
mandelbrot_kernel[grid_dim, block_dim](img_cuda, -2.0, 1.0, -2.0, 2.0, 75)
img_cuda.to_host()

plt.imsave('mandelbrot_set.png', img_np, cmap='plasma')
```

Requirements

```

matplotlib==2.2.2
numba==0.38.0
numpy==1.17.3
```
