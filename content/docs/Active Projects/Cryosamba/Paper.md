---
title: "BioArchive"
date: 2024-08-15
draft: false
---

# CryoSamba: Self-Supervised Cryo-ET Image Denoising

## Abstract

Cryogenic electron tomography (cryo-ET) has rapidly advanced as a high-resolution imaging tool for visualizing subcellular structures in 3D with molecular detail. Direct image inspection remains challenging due to inherent low signal-to-noise ratios (SNR). We introduce CryoSamba, a self-supervised deep learning-based model designed for denoising cryo-ET images. CryoSamba enhances single consecutive 2D planes in tomograms by averaging motion-compensated nearby planes through deep learning interpolation, effectively mimicking increased exposure. This approach amplifies coherent signals and reduces high-frequency noise, substantially improving tomogram contrast and SNR. CryoSamba operates on 3D volumes without needing pre-recorded images, synthetic data, labels or annotations, noise models, or paired volumes. CryoSamba suppresses high-frequency information less aggressively than do existing cryo-ET denoising methods, while retaining real information, as shown both by visual inspection and by Fourier shell correlation analysis of icosahedrally symmetric virus particles. Thus, CryoSamba enhances the analytical pipeline for direct 3D tomogram visual interpretation.

## BioArchive

[Twitter Link](https://x.com/KirchhausenLab/status/1813651584427184490)

![Cryosamba](/cryosamba.png)

[Bio Archive Link](https://www.biorxiv.org/content/10.1101/2024.07.11.603117v1)
