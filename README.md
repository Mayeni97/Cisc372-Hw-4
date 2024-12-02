
# CUDA Fractal Zoom Project

---

## Overview

This project focuses on exploring General Purpose GPU (GPGPU) programming with CUDA by parallelizing a serial program that generates fractal images at increasing zoom levels. The final outputs are fractal images, which can be combined into animations or even printed as creative gifts.

**Key Features:**
- Converts nested for loops in serial code into GPU kernels for parallel execution.
- Allows the creation of fractal animations using a series of images.
- Optimized for execution on NVIDIA GPU-enabled systems.

---

## Instructions

### 1. Initial Setup
1. Extract the provided archive `fractal.tgz` from the `fractal_serial` folder:
   ```bash
   tar -xvzf fractal.tgz
   ```
2. Compile the serial code:
   ```bash
   cc -O3 fractal.c -o fractal
   ```
3. Run the serial program with parameters for resolution and frame count:
   ```bash
   ./fractal <width> <height> <frames>
   ```
   Example:
   ```bash
   ./fractal 320 200 10
   ```
4. Convert output BMP images into an animated GIF:
   ```bash
   convert -delay 1x30 fractal*.bmp fractal.gif
   ```

---

### 2. CUDA Parallelization
1. Modify the serial implementation:
   - Replace the nested loops with a CUDA kernel to execute one thread per pixel.
   - Use a sufficient number of threads and blocks to cover all pixels.
2. Compile the CUDA code:
   ```bash
   nvcc -O3 fractal.cu -o fractal_cuda
   ```
3. Run the parallelized program:
   ```bash
   ./fractal_cuda <width> <height> <frames>
   ```
   Example:
   ```bash
   ./fractal_cuda 4096 2160 60
   ```
4. Verify correctness by comparing output images with the serial implementation for small resolutions.

---

### 3. Performance Analysis
1. Execute the CUDA program on the DARWIN cluster for various resolutions and frame counts (up to 4K resolution and 60 frames).
2. Record runtimes for at least 10 input parameter sets in a table with increasing problem sizes.
3. Save the runtime results into a file (e.g., `runtime_table.txt`).

---

## Submission Guidelines

### Required Files:
1. **`fractal.cu`**: CUDA source code.
2. **`runtime_table.txt`**: Table of runtimes for various input sizes.
3. **`output.txt`**: Execution log from the DARWIN cluster.

### Excluded Files:
- Do not include images, animations, or header files unless modified.

### Submission Steps:
- Submit all files via Gradescope.
- Ensure all submitted code compiles and produces correct output.

---

## Grading Criteria
| Criterion                                         | Points |
|--------------------------------------------------|--------|
| Program compiles successfully                    | 20     |
| Correct execution of kernel with proper threads/blocks | 20 |
| Accurate fractal computation                     | 30     |
| Performance gains showing ~1000x speedup         | 30     |
| **Extra Credit**: Top 4 runtimes                 | 5      |

---

## Tools and Resources
- **CUDA Toolkit**: Install on your local NVIDIA GPU system.
- **DARWIN Cluster**: Final runs and performance analysis must be conducted here.
- **ImageMagick Convert**: Used to create animated GIFs from BMP images.

---

## Additional Notes
- Brighter areas of the fractal require less computation, while darker areas are more compute-intensive.
- Properly configure the kernel launch parameters to maximize GPU utilization.
- Ensure disk space is managed properly when generating large or numerous output files.

Happy fractal computing! 🎨
