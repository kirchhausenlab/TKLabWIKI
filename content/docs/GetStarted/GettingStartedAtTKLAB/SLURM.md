---
title: SLURM for the CPU Cluster
type: docs
---

## SLURM for the CPU Cluster

### Overview

The Slurm Workload Manager, previously known as Simple Linux Utility for Resource Management (SLURM), is a free and open-source job scheduler for Linux and Unix-like systems. This tool is utilized to run jobs on the CPU cluster, particularly within Matlab. SLURM enables users to allocate exclusive or non-exclusive access to computer nodes for a specified time period, allowing them to perform computational work efficiently.

### Prerequisites

- **Account**: Ensure you have an account and password provided by SBgrid.
- **Network Connection**: Log into a Linux/Ubuntu/Unix computer connected to the Harvard network.

### Steps to Install and Configure SLURM

1. **Verify SLURM Installation**  
   Open the terminal and execute the following command:

   ```bash
   sview
   ```

   If successful, a new window will pop up, confirming that SLURM is available on your network.

2. **Open a New Terminal Tab**  
   Click on the new tab icon in the terminal to open a new tab.

3. **Launch Matlab**  
   In the terminal, execute the command:

   ```bash
   matlab
   ```

   The Matlab window should open.

4. **Configure Matlab for SLURM**

   - Go to **Home > Preferences > Parallel Computing Toolbox** in Matlab.
   - Click on **Cluster Profile Manager**.
   - If a pop-up appears, click **OK**. The Matlab parallel server should be visible.
   - A new cluster profile, `SlurmProfile1`, will be added. Select this profile and click **Edit**.
   - Under **Number of workers available to cluster (NumWorkers)**, enter `384`.
   - Click **Done**, then click **Validate**. This process may take anywhere from a few minutes to several hours.

5. **Finalizing Setup**

   - If the job test (create job) passes, the setup is successful.
   - Close the setup window, and in the **Preferences** window, set the default cluster to `SlurmProfile1`.
   - Click **Apply**, then close the window.

6. **Running Jobs with SLURM in Matlab**

   - In Matlab’s command window, type:

     ```matlab
     parpool(N)
     ```

     where `N` is the number of workers you wish to allocate (maximum of 384).

   - To check the number of available workers, refer to the `sview` window from step 1 and click **Visible Table**. This will display the number of busy and available workers.

   - If all requested workers are available, Matlab will establish the connection and configure the session. This process may take between 1 to 15 minutes.

   - Once the configuration is successful, you can proceed to run your Matlab programs using the cluster.

### Additional Information

- If another user is utilizing some of the workers, your program will wait until those resources become available.

---
