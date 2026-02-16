**Theory: Low-Pass and High-Pass Filtering in the Frequency Domain**

**1. The Frequency Domain Representation of Images**

In image processing, an image can be represented in two domains:

-   **Spatial domain:** The image is represented by pixel intensities as
    a function of position

$$f(x,y)
$$

-   **Frequency domain:** The image is represented by its frequency
    components

$$F(u,v)
$$

The frequency domain describes how rapidly the intensity values change
across the image.

-   **Low frequencies:** Represent slowly varying intensity regions such
    as smooth areas and backgrounds.

-   **High frequencies:** Represent rapidly changing intensity regions
    such as edges, fine details, and noise.

Low frequencies correspond to the overall structure of the image, while
high frequencies correspond to details and sharp transitions.

**2. Fourier Transform in Image Processing**

To convert an image from the spatial domain to the frequency domain, the
**2D Discrete Fourier Transform (DFT)** is used:

$$F(u,v) = \sum_{x = 0}^{M - 1}{\sum_{y = 0}^{N - 1}{f(x,y)}}e^{- j2\pi\left( \frac{ux}{M}+\frac{vy}{N} \right)}
$$

Where:

-   $f(x,y)$= input image in spatial domain

-   $F(u,v)$= frequency domain representation

-   $M,N$= image dimensions

-   $u,v$= frequency coordinates

-   $j$= imaginary unit

The inverse DFT reconstructs the original image:

$$f(x,y) = \frac{1}{MN}\sum_{u = 0}^{M - 1}{\sum_{v = 0}^{N - 1}{F(u,v)}}e^{j2\pi\left( \frac{ux}{M}+\frac{vy}{N} \right)}
$$

**3. Frequency Domain Filtering**

Filtering in the frequency domain is performed by multiplying the
Fourier transform of the image by a filter function:

$$G(u,v) = H(u,v) \cdot F(u,v)
$$

Where:

-   $F(u,v)$= Fourier transform of input image

-   $H(u,v)$= filter transfer function

-   $G(u,v)$= filtered frequency image

The filtered image is then converted back using the inverse DFT.

**4. Low-Pass Filtering (LPF)**

A Low-Pass Filter allows low frequencies to pass and blocks high
frequencies.

Mathematically:

$$G(u,v) = H_{LPF}(u,v) \cdot F(u,v)
$$

Where:

$$H_{LPF}(u,v) = \left\{ \begin{matrix}
1, & D(u,v) \leq D_{0} \\
0, & D(u,v) > D_{0} \\
\end{matrix} \right.\ 
$$

$D(u,v)$= distance from center\
$D_{0}$= cutoff frequency

**Effect of Low-Pass Filter**

-   Removes high-frequency components

-   Smooths the image

-   Reduces noise

-   Causes blurring

Applications:

-   Noise reduction

-   Image smoothing

-   Preprocessing for segmentation

**5. High-Pass Filtering (HPF)**

A High-Pass Filter allows high frequencies to pass and blocks low
frequencies.

Mathematically:

$$G(u,v) = H_{HPF}(u,v) \cdot F(u,v)
$$

Where:

$$H_{HPF}(u,v) = \left\{ \begin{matrix}
0, & D(u,v) \leq D_{0} \\
1, & D(u,v) > D_{0} \\
\end{matrix} \right.\ 
$$

**Effect of High-Pass Filter**

-   Removes low frequencies

-   Enhances edges

-   Enhances fine details

-   Sharpens the image

Applications:

-   Edge detection

-   Image sharpening

-   Feature extraction

**6. Distance Function in Frequency Domain**

The distance from the center of the frequency domain is:

$$D(u,v) = \sqrt{\left( u - M/2)^{2} + (v - N/2)^{2} \right.\ }
$$

This determines whether a frequency is low or high.

**7. Summary of Effects**

+----------------+----------------+-----------------+-----------------+
| **Filter       | **Filter       | **Blocks**      | **Effect**      |
| Type**         | Type**         |                 |                 |
+================+================+=================+=================+
| Low-Pass       | Low            | High            | Blurring,       |
|                | frequencies    | frequencies     | smoothing       |
+----------------+----------------+-----------------+-----------------+
| High-Pass      | High           | Low frequencies | Edge            |
|                | frequencies    |                 | enhancement     |
|                |                |                 |                 |
|                |                |                 |   ---           |
|                |                |                 | --------------- |
|                |                |                 |                 |
|                |                |                 |    , sharpening |
|                |                |                 |   --            |
|                |                |                 | -- ------------ |
|                |                |                 |                 |
|                |                |                 |   ---           |
|                |                |                 | --------------- |
+----------------+----------------+-----------------+-----------------+

  ------------------ --------------- --------------- ---------------------
                                                     

  ------------------ --------------- --------------- ---------------------

**8. Conceptual Interpretation**

-   Low-Pass Filter → removes detail → smooth image

-   High-Pass Filter → removes smooth regions → highlights edges
