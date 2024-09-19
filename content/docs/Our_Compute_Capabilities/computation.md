---
title: "Our Compute Capabilities and what they are used for"
draft: false
---

--

# Our Compute Capabilities

Summary of the compute capabilities of our lab's systems:

| System                                  | CPU(s) | Thread(s) per core | Core(s) per socket | Socket(s) | CPU Family | Model | Memory | GPU                       | Disk       |
| --------------------------------------- | ------ | ------------------ | ------------------ | --------- | ---------- | ----- | ------ | ------------------------- | ---------- |
| [NVIDIA DGX A100](#3-x-nvidia-dgx-a100) | 256    | 2                  | 64                 | 2         | 23         | 49    | 2.0Ti  | 8 x NVIDIA A100-SXM4-40GB | 91G / 1.8T |
| [TKL1](#tkl1-tkl2-tkl3-tkl4)            | 32     | 2                  | 8                  | 2         | 6          | 85    | 502Gi  | 3 x Quadro RTX 8000       | /          |
| [TKL2](#tkl2)                           | 32     | 2                  | 8                  | 2         | 6          | 85    | 502Gi  | 1 x Quadro RTX 8000       | /          |
| [TKL3](#tkl3)                           | 32     | 2                  | 8                  | 2         | 6          | 85    | 502Gi  | 3 x Quadro RTX 8000       | /          |
| [TKL4](#tkl4)                           | 32     | 2                  | 8                  | 2         | 6          | 85    | 502Gi  | 3 x Quadro RTX 8000       | /          |
| [TKhpc](#tkhpc)                         | 64     | 2                  | 8                  | 4         | 6          | 62    | 503Gi  | 1 x Quadro K6000          | /          |

Excluding the NVIDIA DGX A100, we have a total of 192 CPUs CORES, with 8 cores per socket and 2 threads per core.

## **SLURM Nodes**

```
NODELIST NODES PARTITION STATE CPUS S:C:T MEMORY TMP_DISK WEIGHT AVAIL_FE REASON
tkv1 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv2 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv3 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv4 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv5 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv6 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv7 1 tk-cpu* idle 48 2:12:2 102025 0 1 (null) none
tkv8 1 tk-cpu* drained 48 2:12:2 102025 0 1 (null) cause
tkv9 1 tk-cpu* idle 80 2:20:2 154476 0 1 (null) none
tkv10 1 tk-cpu* idle 80 2:20:2 154476 0 1 (null) none
tkv11 1 tk-cpu* idle 80 2:20:2 154476 0 1 (null) none
tkv12 1 tk-cpu* idle 80 2:20:2 154476 0 1 (null) none
```

## **3 x NVIDIA DGX A100**

**FAQ: "We have not integrated TKL1-4 into the SLURM system, nor our DGX systems. Sharing demanding jobs in a single DGX poses a risk for crashes. To mitigate this, I have compartmentalized our resources. We have given away our first DGX to Steve and his team, which is located in their lab or EM suite. Some individuals have access to our DGX-100, specifically #3, although we have priority in its use. Additionally, We have decided to exclusively use our DGX systems for our AI work, such as Jose et al. This includes ASEM and cryoSAMBA, but does not encompass CARE runs."**

DGX2 is exclusively for the TKLAB while Steve's lab uses DGX1 and DGX3 from time to time

--

# Computational Resources

## On-Site

| Hostname | OS                      | Location | Software        | Remote Desktop | CPU                      | GPU                         |
| -------- | ----------------------- | -------- | --------------- | -------------- | ------------------------ | --------------------------- |
| tkhpc32  | Ubuntu 20.04/Windows 10 | WA 133D  | Amira           | xdesk.sh       | 32 Dual Core x86_64 CPUs | 1 X Quadro K6000 - 12 Gb    |
| tkhpc32b | Ubuntu 20.04/Windows 10 | WA 133C  |                 | xdesk.sh       | 32 Dual Core x86_64 CPUs | 1 X Quadro K6000 - 12 Gb    |
| tkhpc32c | Ubuntu 20.04/Windows 10 | WA 133C  |                 | xdesk.sh       | 32 Dual Core x86_64 CPUs | 1 X Quadro P6000 - 23 Gb    |
| tkhpc36a | Ubuntu 20.04/Windows 10 | WA 133C  |                 | xdesk.sh       | 36 Dual Core x86_64 CPUs | 1 X Quadro K6000 - 12 Gb    |
| tkhpc36b | Ubuntu 20.04/Windows 10 | WA 133C  |                 | xdesk.sh       | 36 Dual Core x86_64 CPUs | 1 X Quadro K6000 - 12 Gb    |
| tkhpc36c | Windows 10              | WA 133C  | LabView; Imaris | CRD            | 36 Dual Core x86_64 CPUs | 1 X GeForce Titan X - 12 Gb |

## On-Line

| Hostname       | OS                      | Location | Software       | Remote Desktop | CPU                      | GPU                         |
| -------------- | ----------------------- | -------- | -------------- | -------------- | ------------------------ | --------------------------- |
| tkhpc48        | Ubuntu 20.04/Windows 10 | WAB 149  |                | xdesk.sh       | 48 Dual Core x86_64 CPUs | 1 X Quadro K8000 - 11 Gb    |
| tkl1           | Ubuntu 20.04/Windows 10 | WAB 149  |                | xdesk.sh       | 16 Dual Core x86_64 CPUs | 3 X Quadro RTX 8000 - 49 Gb |
| tkl2           | Ubuntu 20.04/Windows 10 | WAB 149  | Amira, LabView | xdesk.sh       | 16 Dual Core x86_64 CPUs | 1 X Quadro RTX 8000 - 49 Gb |
| tkl3           | Ubuntu 20.04/Windows 10 | WAB 149  |                | xdesk.sh       | 16 Dual Core x86_64 CPUs | 3 X Quadro RTX 8000 - 49 Gb |
| superscope     | Windows 10              | WAB 149  | LabView        | CRD            | N/A                      | N/A                         |
| dreamspace III | Windows 10              | WAB 133D | LabView        | CRD            | N/A                      | N/A                         |
| tkl4           | Ubuntu 20.04            | WAB 149  |                | xdesk.sh       | 16 Dual Core x86_64 CPUs | 3 X Quadro RTX 8000 - 49 Gb |

## Filesystem Resources

| Filesystem                           | Location | Space                                 | Usage                                   |
| ------------------------------------ | -------- | ------------------------------------- | --------------------------------------- |
| /nfs/scratch                         | CLSB     | 65 TB                                 | LLSM/AO-LLSM                            |
| /nfs/scratch1                        | WAB 149  | 108 TB                                | Cryo-EM data                            |
| /nfs/scratch2                        | WAB 149  | 66 TB                                 | FIB-SEM ASEM                            |
| /nfs/data1expansion/FIBSEM-datasync3 | CLSB     | 258 TB (shared with datasync3)        | Storage of data acquired at the FIB-SEM |
| /nfs/datasync2                       | CLSB     | 134 TB                                | LLSM/AO-LLSM Backup from 12-14 to 12-17 |
| /nfs/data1expansion/datasync3        | CLSB     | 258 TB (shared with FIBSEM-datasync3) | LLSM/AO-LLSM Backup from 01-18 to 04-22 |
| /nfs/datasync4                       | CLSB     | 336 TB                                | LLSM/AO-LLSM Backup from 04-22          |
| /nfs/datasync5                       | CLSB     | 336 TB                                | LLSM/AO-LLSM Backup from 04-22          |
| /nfs/datasync6                       | CLSB     | 336 TB                                | LLSM/AO-LLSM Backup from 04-22          |
