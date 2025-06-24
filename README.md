# Software/Machine Learning Engineer
Engineer with a strong foundation in deep learning, embedded systems, and performance optimization. Experienced in building scalable, GPU-accelerated pipelines for real-time AI applications—ranging from image processing and automation to scientific computing. Passionate about making machine learning models fast, efficient, and production-ready.


#### Technical Skills
**Languages:** Python, C/C++, CUDA, Rust, Java, MATLAB, VHDL  
**Frameworks:** PyTorch, Scikit-learn, Pandas, SciPy, NumPy, FastAPI  
**Technologies:** ML, DL, CV, Real-Time Systems, Embedded Software, Microservices, Model Optimization, FPGA (Xilinx/AMD)
**Tools & Platforms:** Git, Linux, Docker, Jupyter, VSCode, AWS(learning)  

## Education
- MSc., Embedded and Computer Engineering | TU Delft (_October 2024_)
- BSc., Electrical Engineering | Inholland Alkmaar (_July 2022_)

## Work Experience
**Research Scientist @ TU Delft | Grussmayer Lab (_Januari 2025 - Present_)**
- Developed a **[Focus Lock](https://ir.amolf.nl/pub/10774/16893publishedVersion.pdf)** system to stabilize the microscope’s axial position, correcting for lateral drift during live-cell and single-molecule imaging. [Repo](https://github.com/GrussmayerLab/gFocus). 
- Contributed to the development of **Fast [SOFI](https://en.wikipedia.org/wiki/Super-resolution_optical_fluctuation_imaging)** system for real-time super-resolution microscopy. The DL model reconstructs high-resolution images from just 8 low-resolution input frames, achieving a 2× spatial resolution boost. [Repo (coming soon)](https://github.com/GrussmayerLab/SOFI-MISRGRU) 
- Supporting the preparation of a **scientific publication** based on this work, focused on accelerating fluctuation-based super-resolution imaging with deep learning.
- Presented findings at two conferences: **SMLMS Lisbon** and **NWO Biophysics**.

**Software Engineer @ VU Amsterdam | Electronics Group (_August 2022 - Present_)**
- Co-developing **LabOrch**, a Python-based lab orchestration system built on a modular microservices architecture. Enables unified control, real-time feedback, and metadata handling for diverse scientific instruments.
- Designed and implemented the embedded software architecture for the **Line Controller**—an industrial Ethernet (Modbus-based) system for interfacing with digital and analog lab hardware.

**Intern Electronics Engineer @ LUMICKS (_Februari 2022 - June 2022_)**
-  Designed an FPGA-based demo system for the **C-Trap optical tweezer**, integrating beam steering (Piezo, EOD, AOD) and force sensing (PSDs, sCMOS) via a high-bandwidth PID control loop.

## Projects
### Real-Time eSRRF
To sharpen my CUDA programming skills, I optimized eSRRF (enhanced Super-Resolution Radial Fluctuations), a widely used algorithm in live-cell super-resolution microscopy. eSRRF analyzes radial intensity fluctuations in fluorescent images to generate super-resolved outputs—but its high computational cost limits real-time use.

I re-implemented the algorithm in C and further optimized it with CUDA. While preserving its core structure, I replaced the temporal analysis step with incremental versions of AVG, VAR, and TAC2. This eliminated redundant recomputation by updating statistics on-the-fly as new frames arrive, drastically reducing memory and compute overhead.

As a result, the system outputs super-resolved images at the camera’s frame rate, enabling real-time modality switching, microscope tuning, and seamless integration with machine learning pipelines.

> Benchmarks (NVIDIA RTX 3090):
> - 2048×2048 → 18 FPS
> - 1024×1024 → 73 FPS
> 
> Parameters: magnification=5, radius=2, sensitivity=1, weighting=1, temporal type=TAC2
>
> [Repo](https://github.com/Jelle1212/RT-eSRRF)

![optimized vs default eSRRF](assets/esrrf_comparison_plot.png)

<style>
  .responsive-video {
    width: 100%;
    height: auto;
    max-width: 800px;
  }
</style>

<video class="responsive-video" controls>
  <source src="/assets/output_res.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


### Enabling Real-Time Fluctuation-Based Super Resolution Imaging
As part of my MSc thesis, I adapted [MISGRU](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w11/Arefin_Multi-Image_Super-Resolution_for_Remote_Sensing_Using_Deep_Recurrent_Networks_CVPRW_2020_paper.pdf
)—a deep recurrent neural network originally designed for remote sensing—to accelerate super-resolution optical fluctuation imaging (SOFI).

SOFI typically requires hundreds to thousands of frames and heavy post-processing. My goal was to **reduce both latency and frame count** using MISGRU while preserving SOFI’s twofold spatial resolution boost.

I trained the model using 8- to 20-frame sequences, with second-order SOFI images as the ground truth. After optimizing the architecture and inference pipeline, the model achieved:

- **27 ms latency** per output (400× faster than baseline)

- Super-resolution from as few as **8 input frames**

This work demonstrates that MISGRU can bridge the gap between post hoc and real-time live-cell super-resolution imaging.

![Latency](assets/Ext6_Latency_compare512-1.png)

The image below compares 20-frame MISGRU reconstructions with SOFI using up to 10,000 frames on DNA-PAINT microtubule data.
**Left to right**: single diffraction-limited frame, 20-frame bilinear upsample, SOFI (500 & 10k frames), and MISGRU (20 frames).
White arrows highlight filament continuity recovered by MISGRU.

Scale bar: 1000 nm.
![microtubules](assets/results_exp2-1.png)
## Publications
- **Enabling Real-Time Fluctuation-Based Super Resolution Imaging**
[bioRxiv(2025)](https://www.biorxiv.org/content/10.1101/2025.06.05.658028v1)
- **gFocus** - Coming soon.
