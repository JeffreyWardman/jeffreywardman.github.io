---
title: "Exploring Newton's Method for Septic Polynomials"
published: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Exploring Newton's Method for Septic Polynomials

A lot of mathematical pleasures go unnoticed in the world. There are simple beauties that we see every day. The Barnsley fern is an example of this. In fact, I had the great pleasure of being taught fractal geometry by Michael Barnsley when at university. Fractal geometry is a new field of mathematics that began in the 1970s. Self-similarity, in particular, is an amazing showing of fractal geometry being able to, at times, more accurately represent the real world than Euclidean geometry. Barnsley's fern is self-similar, which means as you zoom in on the fern, there are multiple mini-duplicates of itself. When someone asks how to find the roots of a quadratic, we mathematicians solve $$a x^2 + bx + c$$ by using the quadratic formula:

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

This is fine for quadratics, and there are other methods for solving cubics and quartics. However, quintics, sextics, septics, etc. do not have algebraic solutions. In fact, this was first claimed to be true by Niels Henrik Abel with his impossibility theorem. Paolo Ruffini was noted for his contributions to the proof of this theorem but it was only in 1824 that it was finally proved by Abel. While there may be no algebraic solution, the fundamental theorem of algebra states that there is at least one complex number as a solution for polynomials with a single variable.

One way to find the roots to these equations is to use Newton's method. This is a numerical method that finds complex roots to equations through an iterative approximation process. An estimation of the root is used as an initial value and, after a large number of iterations (repeats of the simulation), will converge to an approximate fixed point: the root of the equation. This method relies on the point-slope formula:

$$
f(x) - f(x_0) = f'(x)(x - x0)
$$

where $$n \in N$$.

By substituting $$x$$ for the complex number $$z = a + bi$$, we can solve for the complex root. Furthermore, setting $$z$$ as $$z_n$$ and rearranging the equation to find the z-intercept gives the Generalised Newton's map: $$N(z_n) := z_{n+1} = z_n - \frac{f(z_n)}{f'(z_n)}$$, where $$f'(z_n) \neq 0$$, $$k \in \mathbb{R}$$. Septic equations will be investigated to show the true beauty of both this method and the field of fractal geometry itself:

$$
az^7 + bz^6 + cz^5 + dz^4 + ez^3 + fz^2 + gz + h = 0
$$

where $$a \neq 0$$, and $$a$$, $$b$$, $$c$$, $$d$$, $$e$$, $$f$$, $$g$$, $$h$$, $$z$$ $$\in \mathbb{C}$$.

This project aims to analyze the behaviour of the system when $$\frac{f(z_n)}{f'(z_n)}$$ is multiplied by parameter $$k$$, where $$0.5 \leq k \leq 2$$, for two septic functions:

1. $$f_1(z) = z^7 - 1$$, $$N_1(z) = z - k \frac{z^7 - 1}{7 z^6}$$

{: style="text-align:center"}
![](/assets/posts/newton-method/f1_roots.png)

<sup>Figure 1: Roots of $$f_2$$ septic function (from Wolfram Alpha)</sup>

- Roots of $$f_1(z)$$ are:
- $$z = 1$$,
- $$z = - \sqrt[7]{-1}$$,
- $$z = (-1)^\frac{2}{7}$$,
- $$z = -(-1)^\frac{3}{7}$$,
- $$z = (-1)^\frac{4}{7}$$,
- $$z = -(-1)^\frac{5}{7}$$,
- $$z = (-1)^\frac{6}{7}$$.

2. $$f_2(z) = z^7 + z^6 + z^5 + z^4 + z^3 + z^2 + z - 4$$,
   $$N_2(z) = z - k \frac{z^7 + z^6 + z^5 + z^4 + z^3 + z^2 + z - 4}{7 z^6 + 6 z^5 + 5 z^4 + 4 z^3 + 3 z^2 + 2 z + 1}$$

{: style="text-align:center"}
![](/assets/posts/newton-method/f2_roots.png)

<sup>Figure 2: Roots of $f_2$ septic function (from Wolfram Alpha)</sup>

- Roots of $$f_2(z)$$ are:
  - $$z \approx 0.859648$$,
  - $$z \approx -1.221390 \pm 0.554496 i$$,
  - $$z \approx -0.374730 \pm 1.253618 i$$,
  - $$z \approx 0.666296 \pm 1.302783 i$$.

# Methodology

Newton's method was applied to functions $$f_1(z)$$ and $$f_2(z)$$ with $$k \in [0.5, 2]$$ and incrementing by 0.25. Values outside this range resulted in black images, meaning the map failed to converge in the 512 iterations conducted.

### Pseudo-code

1. Define the Newton map of the function.
2. Choose parameter $$k$$.
3. Set a colour to display the convergence of a point to a particular root of the function that the map can converge to.
4. For any point on the plane, apply Newtons method until either the function has converged, or 512 iterations have occurred meaning it did not converge at a root.

# Proofs

Proof that $$z_{n+1} = z_n - k \frac{f(z_n)}{f'(z_n)}$$ is affected by $$k$$:

Consider the Newton's map for a function, $$f^m$$, where $$m \in \mathbb{N}$$. The derivative of the function is $$(f^m)' = m f^{m-1}(z) f'(z)$$.
Therefore, the Newton map of the function is:

$$
\begin{align}
N(z_{m+1}) &:= z_m - \frac{f^m(z)}{(f^m)'(z)} \\\\
&= z_m - \frac{f^m(z)}{m f^{m-1}(z) f'(z)} \\\\
&= z_m - k\frac{f(z)}{f'(z)}
\end{align}
$$

where $$k = \frac{1}{m}$$, $$m \neq 0$$.
Therefore, the Newton map is affected by parameter $$k$$.

# Results

### $$f_1(z) = z^7 - 1$$

Root colours:

- Blue: $$z = 1$$
- Red: $$z = - \sqrt[7]{-1}$$
- Yellow: $$z = (-1)^\frac{2}{7}$$
- Green: $$z = -(-1)^\frac{3}{7}$$
- Beige: $$z = (-1)^\frac{4}{7}$$
- Pink: $$z = -(-1)^\frac{5}{7}$$
- Brown: $$z = (-1)^\frac{6}{7}$$

|                                       $$k=0.5$$                                       |                                       $$k=0.75$$                                        |                                       $$k=1$$                                       |                                       $$k=1.25$$                                        |
| :-----------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: |
| ![f1_k0.5](/assets/posts/newton-method/f1/f1_k0.5.png){:height="256px" width="256px"} | ![f1_k0.75](/assets/posts/newton-method/f1/f1_k0.75.png){:height="256px" width="256px"} | ![f1_k1](/assets/posts/newton-method/f1/f1_k1.0.png){:height="256px" width="256px"} | ![f1_k1.25](/assets/posts/newton-method/f1/f1_k1.25.png){:height="256px" width="256px"} |
|                                       $$k=1.5$$                                       |                                       $$k=1.75$$                                        |                                       $$k=2$$                                       |
| :-----------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: |  :-------------------------------------------------------------------------------:  | :-------------------------------------------------------------------------------------: |
| ![f1_k1.5](/assets/posts/newton-method/f1/f1_k1.5.png){:height="256px" width="256px"} | ![f1_k1.75](/assets/posts/newton-method/f1/f1_k1.75.png){:height="256px" width="256px"} |  ![f1_k2](/assets/posts/newton-method/f1/f1_k2.png){:height="256px" width="256px"}  |

As can be seen in the images above, the method fails to converge (resulting in black pixels) after 512 iterations for the $$f_1$$ function at $$k = 0.5$$ and $$k = 2$$. There is also some failure of convergence at $$k = 0.75$$. As reducing $$k$$ ($$k < 1$$) reduces the rate at which the function changes, the pixels that failed to converge may have converged with more iterations.
The chaos (the noise between each of the colours) between which root the method converges to varies greater as $$k$$ exceeds 1. This suggests that somwhere between $$k = 0.75$$ and $$k = 1.25$$ is the optimal constant parameter for convergence for this function.

Below are 4K resolution images of the $$f_1$$ function as $$k = 2$$ is approached ($$k = 1.988$$ and $$k = 1.989$$ respectively). What's interesting is that the somewhat circular blobs of each colour that get smaller and smaller at the center are also within the chaotic sections between colours. This shows that there is fractal repetition. It also shows how the fractal starts, from a single point of non-convergence. What's also interesting is the snowflake-like pattern towards the center of the colours, resulting in a black dot in the less chaotic sections. Both patterns, and their origin become more prevalent in the second image.

{: style="text-align:center"}
![f1_k1.988](/assets/posts/newton-method/f1/f1_k1.988_4096.png){:height="1024px" width="1024px"}
![f1_k1.989](/assets/posts/newton-method/f1/f1_k1.989_4096.png){:height="1024px" width="1024px"}

### $$f_2(z) = z^7 + z^6 + z^5 + z^4 + z^3 + z^2 + z - 4$$

Root colours:

- Blue: $$z \approx 0.859648$$
- Red: $$z \approx -1.221390 - 0.554496 i$$
- Yellow: $$z \approx -1.221390 + 0.554496 i$$
- Green: $$z \approx -0.374730 - 1.253618 i$$
- Beige: $$z \approx -0.374730 + 1.253618 i$$
- Pink: $$z \approx 0.666296 - 1.302783 i$$
- Brown: $$z \approx 0.666296 + 1.302783 i$$

|                                       $$k=0.5$$                                       |                                       $$k=0.75$$                                        |                                      $$k=1$$                                      |                                       $$k=1.25$$                                        |
| :-----------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: |
| ![f2_k0.5](/assets/posts/newton-method/f2/f2_k0.5.png){:height="256px" width="256px"} | ![f2_k0.75](/assets/posts/newton-method/f2/f2_k0.75.png){:height="256px" width="256px"} | ![f2_k1](/assets/posts/newton-method/f2/f2_k1.png){:height="256px" width="256px"} | ![f2_k1.25](/assets/posts/newton-method/f2/f2_k1.25.png){:height="256px" width="256px"} |
|                                       $$k=1.5$$                                       |                                       $$k=1.75$$                                        |                                      $$k=2$$                                      |
| :-----------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: |
| ![f2_k1.5](/assets/posts/newton-method/f2/f2_k1.5.png){:height="256px" width="256px"} | ![f2_k1.75](/assets/posts/newton-method/f2/f2_k1.75.png){:height="256px" width="256px"} | ![f2_k2](/assets/posts/newton-method/f2/f2_k2.png){:height="256px" width="256px"} |                                                                                         |

$$f_2$$ has identical conclusions made about the fractal patterns as $$f_1$$. Inspection into the high-resolution images shows that the chaos is asymmetrical. Below are 4K resolution images of the $$f_1$$ function as $$k = 2$$ is approached ($$k = 1.988$$ and $$k = 1.989$$ respectively). It is interesting to note that the function fails to converge at $$k = 1.989$$ more often than $$f_1$$. This is most likely due to needing more iterations to converge due to being a more complex function.

Both functions fail to converge when $$k = 2$$. This is due to stepping double the distance per iteration in comparison to when $$k = 1$$. This causes the chaotic areas for the roots around the boundary between two colours. After approaching the root, $$N(z) = z_n - k \frac{f(z_n)}{f'(z_n)}$$ causes the function to end up further from the conjugate root (which is two times further than the imaginary component of the root) and thus, the functions do not converge for $$k \geq 2$$.

{: style="text-align:center"}
![f2_k1.988](/assets/posts/newton-method/f2/f2_k1.988_4096.png){:height="1024px" width="1024px"}
![f2_k1.989](/assets/posts/newton-method/f2/f2_k1.989_4096.png){:height="1024px" width="1024px"}

# Conclusion

For Newton maps, functions converge to different roots with different amounts of iterations. Increasing $$k$$ will cause the function to converge faster, but will be more chaotic due to not reaching the minimum local minima of 0.0001. It was identified that Newton’s method can accurately find the roots of a septic polynomial with a parameter of $$0.5 < k < 2$$ for the equation $$z_{n+1} = z_n - k \frac{f(z_n)}{f'(z_n)}$$.

# Code

Example for $$f_1(z) = z^7 - 1$$

```
from PIL import Image, ImageDraw
from tqdm import tqdm


def N(z, k):
    """Newton's method: z_(n+1) = zn - f(z_n)/f'(z_n)"""
    new = z - k * (z**7 - 1) / (7 * z**6)
    return new


def generate_image(k: int = 1, SIZE: int = 512, num_iters: int = 512, epsilon: float = 0.0001):
    image = Image.new("RGB", (SIZE, SIZE))  # Create an image of size SIZE x SIZE
    d = ImageDraw.Draw(image)

    yellow = (255, 255, 0)
    green = (50, 205, 50)
    blue = (0, 0, 205)
    red = (255, 0, 0)
    beige = (240, 230, 140)
    pink = (255, 105, 180)
    brown = (100, 0, 0)
    black = (0, 0, 0)

    # Range of axes
    XMIN = -10.
    XMAX = 10.
    YMIN = -10.
    YMAX = 10.

    for x in tqdm(range(SIZE)):
        for y in range(SIZE):
            real = XMIN + x * (XMAX - XMIN) / SIZE
            imaginary = YMIN + y * (YMAX - YMIN) / SIZE
            z = real + imaginary * 1j
            for _ in range(num_epochs):
                if abs(z) < epsilon or abs(z - N(z, k)) < epsilon:
                    break

                # Overwrite z with new z value
                z = N(z, k)

                col = black
                # Colour if the absolute of z-root of the equation
                # is less than epsilon (converged).
                # Leave black if failed to converge
                if abs(z - 1) < epsilon:
                    col = blue
                elif abs(z + ((1j)**2)**(1 / 7)) < epsilon:
                    col = red
                elif abs(z - ((1j)**2)**(2 / 7)) < epsilon:
                    col = yellow
                elif abs(z + ((1j)**2)**(3 / 7)) < epsilon:
                    col = green
                elif abs(z - ((1j)**2)**(4 / 7)) < epsilon:
                    col = beige
                elif abs(z + ((1j)**2)**(5 / 7)) < epsilon:
                    col = pink
                elif abs(z - ((1j)**2)**(6 / 7)) < epsilon:
                    col = brown
                d.point((x, y), col)

    image.save(f"f1_k{k}.png", "PNG")
    image.show()
```
