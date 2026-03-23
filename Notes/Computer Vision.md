### Key Concepts:

1. **Computer Vision Tasks** (coarse to fine):
    - **Classification**: One image in, one class label out (e.g. "cat")
    - **Object Detection**: Bounding boxes + class labels for each object
    - **Semantic Segmentation**: Per-pixel class labels (can't separate instances)
    - **[[Instance Segmentation]]**: Per-pixel labels + distinguishes individual objects
    - Common datasets: MNIST, CIFAR-10, ImageNet, Pascal VOC, MS-COCO, Cityscapes
2. **Image Representation**:
    - Grayscale image = a matrix ($m \times n$), each element is a pixel intensity $[0, 255]$
    - RGB colour image = $m \times n \times 3$ array (one channel each for R, G, B)
    - Can treat an image as a function: $f(x, y)$ returns intensity at location $(x, y)$
3. **[[Point Operations]]**:
    - Operate on each pixel independently: $g(x,y) = a \cdot f(x,y) + b$
    - $a$ (gain) controls contrast, $b$ (bias) controls brightness
    - $a > 1$ increases contrast; $b > 0$ increases brightness
4. **[[Image Filtering (Cross-Correlation)]]**:
    - Replace each pixel with a weighted combination of its neighbours
    - Kernel/mask $H[u,v]$ defines the weights
    - $G[i,j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u,v] \cdot F[i+u, j+v]$
    - Output size (no padding): $(N - K + 1)$ for an $N \times N$ image with $K \times K$ kernel
5. **[[Convolution]]**:
    - Same as cross-correlation but flip the kernel 180 degrees first
    - $G[i,j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u,v] \cdot F[i-u, j-v]$
    - Properties: commutative ($f * g = g * f$), associative ($(f * g) * h = f * (g * h)$), distributive over addition
    - For symmetric kernels (box, Gaussian), identical to cross-correlation
6. **Key Filters**:
    - **Box filter**: All weights equal ($\frac{1}{K^2}$), produces uniform blur/smoothing
    - **Gaussian filter**: Weights follow a bell curve, more weight to centre pixels
    - **Sharpening filter**: $2 \cdot \text{identity} - \text{box filter}$, accentuates edges and detail
    - **Identity filter**: Single 1 in centre, zeros elsewhere, no change to image
    - **Shift filter**: Single 1 off-centre, shifts image in opposite direction
7. **[[Gaussian Filter Properties]]**:
    - Formula: $G_\sigma = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2 + y^2}{2\sigma^2}}$
    - Low-pass filter: removes high-frequency components (fine detail)
    - Separable: 2D kernel = column vector $\times$ row vector ($2K$ ops instead of $K^2$)
    - Convolving with itself gives another Gaussian (tw-o passes at $\sigma$ = one pass at $\sigma\sqrt{2}$)
    - Rule of thumb: set filter half-width to about $3\sigma$

**Computing Analogy**: Think of image filtering like a magnifying glass sliding over a newspaper:

- The [[Kernel]] is the magnifying glass — it defines how big a region you look at and how much each part matters.
- Point operations are like adjusting the brightness on your monitor — every pixel changes the same way regardless of its neighbours.
- A box filter is like squinting at the page — everything blurs equally because you're averaging nearby letters together.
- A Gaussian filter is like squinting through reading glasses — nearby things stay sharper than things further from the centre of your focus.
- Sharpening is like using a highlighter on the words that stand out from their background — the differences get amplified.
- Separability is like reading a page row-by-row then column-by-column instead of scanning every character against every other character — same result, way less effort.

See also:
- [[Filter Kernel]]
- [[Image Filtering (Cross-Correlation)]]
- 