---
title: Lab Computing Site/CARE
type: docs
---

## CARE Installation Guide

### Overview

The **Content-Aware image REstoration (CARE)** package is a Python-based routine for data augmentation and image restoration. The following steps outline the installation process and how to set up your environment for running [CARE](https://csbdeep.bioimagecomputing.com/doc/) on the lab's GPU machines.

### Installation Steps

1. **Create a Working Directory:**

   Open your terminal and create a new folder for CARE.

   ```bash
   cd ~
   mkdir care
   cd care
   ```

2. **Create and Activate a Conda Environment:**

   Set up a new Conda environment with Python 3.7.

   ```bash
   conda create --name care python=3.7
   conda activate care
   ```

3. **Install TensorFlow with GPU Support:**

   Install TensorFlow with GPU support in your Conda environment.

   ```bash
   conda install tensorflow-gpu
   ```

4. **Verify TensorFlow Installation:**

   To check if TensorFlow is installed with CUDA support, run the following commands in Python:

   ```python
   import tensorflow as tf
   tf.config.list_physical_devices('GPU')
   ```

   Exit Python by pressing `Ctrl + D`.

5. **Install CSBdeep and scikit-image:**

   Install the necessary libraries for CARE, including CSBdeep and scikit-image.

   ```bash
   pip install csbdeep
   pip install scikit-image
   ```

6. **Optional: Install JupyterLab:**

   If you want to use Jupyter notebooks, install JupyterLab.

   ```bash
   conda install -c conda-forge jupyterlab
   ```

### Running Jupyter on a Remote Machine via SSH

1. **Connect to the Remote Machine:**

   The machines dedicated to CARE are `tkl1` and `tkl3`. You can also use the `tkhpc*` machines, but they have smaller GPU memory, which might result in longer processing times. Connect to the remote machine via SSH:

   ```bash
   ssh username@hostname
   ```

2. **Start a tmux Session (Recommended):**

   Open a tmux session to keep your environment running even if the connection drops. Then, activate the Conda environment:

   ```bash
   conda activate care
   ```

3. **Run Jupyter Notebook on a Specific Port:**

   Start the Jupyter notebook server on a specified port (e.g., 1234):

   ```bash
   jupyter notebook --no-browser --port 1234
   ```

   Copy the generated link (e.g., `http://localhost:1234/...`) for later use.

4. **Set Up SSH Tunneling:**

   In a new terminal tab, set up SSH tunneling to forward the port from the remote machine to your local machine:

   ```bash
   ssh -NL 1234:localhost:1234 username@hostname
   ```

   Keep this shell open. Ensure the port number matches the one used in the Jupyter link.

5. **Access Jupyter Notebook:**

   Paste the copied link into your local web browser to access the Jupyter notebook running on the remote machine.

### SSH Tunneling from Off-site

If you need to access the Jupyter notebook from off-site, first SSH into `xtal200.harvard.edu`. Follow the detailed instructions provided [here](https://sites.google.com/tklab.hms.harvard.edu/tkdataprocessing/home/3-care/key-based-ssh?authuser=0) to set up the tunnel.

### Running Jupyter on a Remote Machine via SSH

1. **Connect to the Remote Machine:**
   The machines dedicated to CARE are `tkl1` and `tkl3`. You can also use the `tkhpc*` machines, but they have smaller GPU memory, which might result in longer processing times. Connect to the remote machine via SSH:

   ```bash
   ssh username@hostname
   ```

2. **Start a tmux Session (Recommended):**
   Open a tmux session to keep your environment running even if the connection drops. Then, activate the Conda environment:

   ```bash
   tmux
   conda activate care
   ```

3. **Run Jupyter Notebook on a Specific Port:**
   Start the Jupyter notebook server on a specified port (e.g., 1234):

   ```bash
   jupyter notebook --no-browser --port 1234
   ```

   Copy the generated link (e.g., `http://localhost:1234/...`) for later use.

4. **Set Up SSH Tunneling:**
   In a new terminal tab on your local machine, set up SSH tunneling to forward the port from the remote machine to your local machine:

   ```bash
   ssh -NL 1234:localhost:1234 username@hostname
   ```

   Keep this shell open. Ensure the port number matches the one used in the Jupyter link.

5. **Access Jupyter Notebook:**
   Paste the copied link into your local web browser to access the Jupyter notebook running on the remote machine.

### SSH Tunneling from Off-site

If you need to access the Jupyter notebook from off-site, first SSH into `xtal200.harvard.edu`. Follow the detailed instructions provided [here](https://sites.google.com/tklab.hms.harvard.edu/tkdataprocessing/home/3-care/key-based-ssh?authuser=0) to set up the tunnel.

### Using CARE Analysis

1. Open the Jupyter notebook interface in your web browser.
2. Navigate to the 'care' folder, then to 'notebook'.
3. Use `2_train_model_LLSM.ipynb` to train your model.
4. Use `3_predict_datasets_LLSM.ipynb` to predict data based on the trained model.

Remember to log out when done by killing the tmux session:

```bash
tmux kill-session
```

### Tips

- To check GPU availability, use the command `nvidia-smi`.
- To continuously monitor GPU usage, use `watch -n2 nvidia-smi`.

For more detailed instructions or troubleshooting, please consult the lab's internal documentation or contact the IT support team.
