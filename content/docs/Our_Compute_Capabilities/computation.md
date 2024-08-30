---
title: "Computation"
draft: false
---

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

## **3 x NVIDIA DGX A100**

**FAQ: "We have not integrated TKL1-4 into the SLURM system, nor our DGX systems. Sharing demanding jobs in a single DGX poses a risk for crashes. To mitigate this, I have compartmentalized our resources. We have given away our first DGX to Steve and his team, which is located in their lab or EM suite. Some individuals have access to our DGX-100, specifically #3, although we have priority in its use. Additionally, We have decided to exclusively use our DGX systems for our AI work, such as Jose et al. This includes ASEM and cryoSAMBA, but does not encompass CARE runs."**

Our lab has three NVIDIA DGX A100 systems, each with the following specifications:

### CPU Information

```markdown
- CPU(s): 256
- Thread(s) per core: 2
- Core(s) per socket: 64
- Socket(s): 2
- CPU Family: 23
- Model: 49
```

### Memory Information

```markdown
- L1d Cache: 4
- L1i Cache: 4
- L2 Cache: 64
- L3 Cache: 512
```

### GPU Information

```markdown
- GPU:
  GPU 0: NVIDIA A100-SXM4-40GB (UUID: GPU-dea86db9-8b18-0785-912e-0cd7c365ebdd)
  GPU 1: NVIDIA A100-SXM4-40GB (UUID: GPU-4fbb6ffc-aa85-14bc-5dc6-6f4078927b72)
  GPU 2: NVIDIA A100-SXM4-40GB (UUID: GPU-91964961-3010-9dbc-262e-0a383a42e457)
  GPU 3: NVIDIA A100-SXM4-40GB (UUID: GPU-1ee21c93-0fbe-31fc-82f2-fbb6e0291e7a)
  GPU 4: NVIDIA A100-SXM4-40GB (UUID: GPU-712321e3-5a60-95f8-0762-d8e1017239d0)
  GPU 5: NVIDIA A100-SXM4-40GB (UUID: GPU-ff394415-d24d-8b0a-bb56-80a667851ca3)
  GPU 6: NVIDIA A100-SXM4-40GB (UUID: GPU-3b8e3a00-cb2f-4d61-8223-cd1aac7f6f1c)
  GPU 7: NVIDIA A100-SXM4-40GB (UUID: GPU-13c54766-2328-c07d-455d-47ce4766928b)
- GPU Utilization: 100,100,100,99,100,100,0,0,
- Total Memory: 2.0Ti
- Used Memory: 106Gi
- Free Memory: 824Gi
- Total Swap: 0B
```

### Disk Information

```markdown
- Free Swap: 0B
- Disk Info: /dev/md0: 91G / 1.8T (Used: 91G)
```

### Summary

- This system is powered by 256 CPUs, with 64 cores per socket and 2 threads per core.
- The system's memory is 2.0Ti, with 106Gi currently in use.

## TKL1, TKL2, TKL3, TKL4

## **TKL1**

### CPU Information

```markdown
- CPU(s): 32
- Thread(s) per core: 2
- Core(s) per socket: 8
- Socket(s): 2
- CPU Family: 6
- Model: 85
```

### Memory Information

```markdown
- L1d Cache: 512
- L1i Cache: 512
- L2 Cache: 16
- L3 Cache: 49.5
```

### GPU Information

```markdown
- GPU:
  GPU 0: Quadro RTX 8000 (UUID: GPU-fd24d982-1c85-59b4-c28a-1e7c7ff5f8f5)
  GPU 1: Quadro RTX 8000 (UUID: GPU-484f1900-66f0-8f8b-8f11-0904d97eb14c)
  GPU 2: Quadro RTX 8000 (UUID: GPU-ba8d9f76-b21f-f876-8ae4-c42d2997f8fe)
- GPU Utilization: 0,0,0,
- Total Memory: 502Gi
- Used Memory: 113Gi
- Free Memory: 386Gi
- Total Swap: 2.0Gi
```

### Disk Information

```markdown
- Free Swap: 8.0Mi
- Disk Info: /dev/md0: / (Used: )
```

### Summary

```markdown
- This system is powered by 32 CPUs, with 8 cores per socket and 2 threads per core.
- The system's memory is 502Gi, with 113Gi currently in use.
```

## **TKL2**

### CPU Information

```markdown
- CPU(s): 32
  scaling
- Thread(s) per core: 2
- Core(s) per socket: 8
- Socket(s): 2
- CPU Family: 6
- Model: 85
```

### Memory Information

```markdown
- L1d Cache: 512
- L1i Cache: 512
- L2 Cache: 16
- L3 Cache: 49.5
```

### GPU Information

```markdown
- GPU:
  GPU 0: Quadro RTX 8000 (UUID: GPU-6770c0eb-8341-142d-ab75-e6778cd83cb8)
- GPU Utilization: 0,
- Total Memory: 502Gi
- Used Memory: 15Gi
- Free Memory: 444Gi
- Total Swap: 511Mi
```

### Disk Information

```markdown
- Free Swap: 511Mi
- Disk Info: /dev/md0: / (Used: )
```

### Summary

```markdown
- This system is powered by 32
  scaling CPUs, with 8 cores per socket and 2 threads per core.
- The system's memory is 502Gi, with 15Gi currently in use.
```

## **TKL3**

### CPU Information

```markdown
- CPU(s): 32
- Thread(s) per core: 2
- Core(s) per socket: 8
- Socket(s): 2
- CPU Family: 6
- Model: 85
```

### Memory Information

```markdown
- L1d Cache: 512
- L1i Cache: 512
- L2 Cache: 16
- L3 Cache: 49.5
```

### GPU Information

```markdown
- GPU:
  GPU 0: Quadro RTX 8000 (UUID: GPU-5d942e4e-2827-48c5-24d8-c9a608746f52)
  GPU 1: Quadro RTX 8000 (UUID: GPU-af341257-d26c-244b-4108-2e3bf21da9c5)
  GPU 2: Quadro RTX 8000 (UUID: GPU-10134818-e46b-588b-0d8a-e254a6695c7c)
- GPU Utilization: 0,0,0,
- Total Memory: 502Gi
- Used Memory: 11Gi
- Free Memory: 475Gi
- Total Swap: 2.0Gi
```

### Disk Information

```markdown
- Free Swap: 2.0Gi
- Disk Info: /dev/md0: / (Used: )
```

### Summary

```markdown
- This system is powered by 32 CPUs, with 8 cores per socket and 2 threads per core.
- The system's memory is 502Gi, with 11Gi currently in use.
```

## **TKL4**

### CPU Information

```markdown
- CPU(s): 32
- Thread(s) per core: 2
- Core(s) per socket: 8
- Socket(s): 2
- CPU Family: 6
- Model: 85
```

### Memory Information

```markdown
- L1d Cache: 512
- L1i Cache: 512
- L2 Cache: 16
- L3 Cache: 49.5
```

### GPU Information

```markdown
- GPU:
  GPU 0: Quadro RTX 8000 (UUID: GPU-5d942e4e-2827-48c5-24d8-c9a608746f52)
  GPU 1: Quadro RTX 8000 (UUID: GPU-af341257-d26c-244b-4108-2e3bf21da9c5)
  GPU 2: Quadro RTX 8000 (UUID: GPU-10134818-e46b-588b-0d8a-e254a6695c7c)
- GPU Utilization: 0,0,0,
- Total Memory: 502Gi
- Used Memory: 11Gi
- Free Memory: 475Gi
- Total Swap: 2.0Gi
```

### Disk Information

```markdown
- Free Swap: 2.0Gi
- Disk Info: /dev/md0: / (Used: )
```

### Summary

```markdown
- This system is powered by 32 CPUs, with 8 cores per socket and 2 threads per core.
- The system's memory is 502Gi, with 11Gi currently in use.
```

## **TKhpc**

### CPU Information

```markdown
- CPU(s): 64
- Thread(s) per core: 2
- Core(s) per socket: 8
- Socket(s): 4
- CPU Family: 6
- Model: 62
```

### Memory Information

```markdown
- L1d Cache: 1
- L1i Cache: 1
- L2 Cache: 8
- L3 Cache: 80
```

### GPU Information

```markdown
- GPU:
  GPU 0: Quadro K6000 (UUID: GPU-1bc43f96-9d1c-bd6b-a8d5-01a99f2a76fa)
- GPU Utilization: 0,
- Total Memory: 503Gi
- Used Memory: 2.6Gi
- Free Memory: 495Gi
- Total Swap: 511Gi
```

### Disk Information

```markdown
- Free Swap: 511Gi
- Disk Info: /dev/md0: / (Used: )
```

### Summary

```markdown
- This system is powered by 64 CPUs, with 8 cores per socket and 2 threads per core.
- The system's memory is 503Gi, with 2.6Gi currently in use.
```

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
