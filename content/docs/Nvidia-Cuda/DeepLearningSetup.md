---
title: "NVIDIA GPU and CUDA Setup Guide"
date: 2024-08-15
draft: false
---

## Verifying NVIDIA Hardware and CUDA Installation

### Check NVIDIA GPU

First, let's verify if your system recognizes the NVIDIA GPU:

Open a terminal and run:

```bash
lspci | grep -i nvidia
```

This should display information about your NVIDIA GPU.

1. Right-click on the Windows Start button and select "Device Manager"
2. Expand the "Display adapters" section
3. You should see your NVIDIA GPU listed here
   Recent Macs don't use NVIDIA GPUs. For older Macs:

4. Click the Apple menu and select "About This Mac"
5. Click on "System Report"
6. Select "Graphics/Displays" in the sidebar

### Verify NVIDIA Drivers

To check if NVIDIA drivers are installed:

Open a terminal and run:

```bash
nvidia-smi
```

This should display information about your GPU, driver version, and CUDA version.

1. Open Command Prompt or PowerShell
2. Run:
   ```
   nvidia-smi
   ```

### Check CUDA Installation

To verify your CUDA installation:

1. Check CUDA version:
   ```bash
   nvcc --version
   ```
2. Verify CUDA location:

   ```bash
   ls /usr/local/cuda
   ```

3. Open Command Prompt or PowerShell
4. Run:
   ```
   nvcc --version
   ```
5. Check CUDA installation directory:
   ```
   dir "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA"
   ```

## Installing CUDA Drivers

If CUDA is not installed or you need to update it:

1. Visit the [NVIDIA CUDA Downloads page](https://developer.nvidia.com/cuda-downloads)
2. Select your Linux distribution and version
3. Follow the installation instructions provided
4. Typically, you'll run commands like:
   ```bash
   wget https://developer.download.nvidia.com/compute/cuda/repos/<distro>/<arch>/cuda-<distro>.pin
   sudo mv cuda-<distro>.pin /etc/apt/preferences.d/cuda-repository-pin-600
   wget https://developer.download.nvidia.com/compute/cuda/<version>/local_installers/cuda-<version>-<arch>.run
   sudo sh cuda-<version>-<arch>.run
   ```
5. Add CUDA to your PATH in `~/.bashrc`:
   ```bash
   export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
   export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
   ```
6. Reload your shell:

   ```bash
   source ~/.bashrc
   ```

7. Visit the [NVIDIA CUDA Downloads page](https://developer.nvidia.com/cuda-downloads)
8. Select Windows and your version
9. Download and run the installer
10. Follow the on-screen instructions
11. Restart your computer after installation

Recent versions of macOS do not support CUDA. For older systems:

1. Visit the [NVIDIA CUDA Downloads page](https://developer.nvidia.com/cuda-downloads)
2. Select macOS and your version
3. Download and run the installer
4. Follow the on-screen instructions
5. Restart your computer after installation

## Accessing Compute

To use your NVIDIA GPU for computation:

1. **CUDA-enabled Applications**: Many scientific and machine learning applications are CUDA-enabled and will automatically use your GPU if properly installed.

2. **Programming with CUDA**:

   - Use CUDA C/C++ for direct GPU programming
   - Use libraries like cuDNN for deep learning
   - Use frameworks like PyTorch or TensorFlow, which leverage CUDA

3. **Jupyter Notebooks**:
   To check GPU availability in a Jupyter notebook:

   ```python
   import torch
   print(torch.cuda.is_available())
   print(torch.cuda.get_device_name(0))
   ```

4. **Docker with GPU Support**:
   - Install [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
   - Run Docker containers with GPU access:
     ```bash
     docker run --gpus all nvidia/cuda:11.0-base nvidia-smi
     ```
5. **Cloud GPU Instances**:
   - Use cloud providers like AWS, GCP, or Azure for GPU instances
   - Install CUDA drivers and libraries on cloud instances

Always ensure you're using the correct CUDA version compatible with your GPU and the software you're using.
