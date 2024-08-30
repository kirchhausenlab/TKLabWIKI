---
title: "Commands to determine compute"
draft: false
---

## CPU Information

Run the following command to get information about the CPU:

```bash
lscpu | grep -e "^CPU(s)" -e "Thread(s)" -e "Core(s)" -e "Socket(s)" -e "^CPU family" -e "Model" -e "Model name" -e "cache"
```

## GPU Information

Run the following command to get information about the GPU:

```
nvidia-smi --query-gpu=index,utilization.gpu,memory.free,memory.total,memory.used --format=csv
nvidia-smi -L
```

## System Information

Run the following command to get information about the system:

```
free -h
```

## Disk Information

Run the following command to get information about the disk:

```
df -h | grep -e "udev" -e "tmpfs" -e "^/dev/md0"
```

## Script

The following script can be used to get all the information at once and store it in a markdown format:

```
#!/bin/bash
generate_markdown() {
echo "### CPU Information"
echo ""
echo '`markdown'
    echo "- CPU(s): $cpus"
    echo "- Thread(s) per core: $threads_per_core"
    echo "- Core(s) per socket: $cores_per_socket"
    echo "- Socket(s): $sockets"
    echo "- CPU Family: $cpu_family"
    echo "- Model: $model"
    echo '`'
echo ""
echo "### Memory Information"
echo ""
echo '`markdown'
    echo "- L1d Cache: $l1d_cache"
    echo "- L1i Cache: $l1i_cache"
    echo "- L2 Cache: $l2_cache"
    echo "- L3 Cache: $l3_cache"
    echo '`'
echo ""
echo "### GPU Information"
echo ""
echo '`markdown'
    echo "- GPU:"
    echo "  $gpu_info"
    echo "- GPU Utilization: $gpu_utilization"
    echo "- Total Memory: $total_mem"
    echo "- Used Memory: $used_mem"
    echo "- Free Memory: $free_mem"
    echo "- Total Swap: $total_swap"
    echo '`'
echo ""
echo "### Disk Information"
echo ""
echo '`markdown'
    echo "- Free Swap: $free_swap"
    echo "- Disk Info: /dev/md0: $disk_used / $disk_total (Used: $disk_used)"
    echo '`'
}

# Capture CPU information

cpus=$(lscpu | grep "^CPU(s)" | awk '{print $2}')
threads_per_core=$(lscpu | grep "Thread(s) per core" | awk '{print $4}')
cores_per_socket=$(lscpu | grep "Core(s) per socket" | awk '{print $4}')
sockets=$(lscpu | grep "Socket(s)" | awk '{print $2}')
cpu_family=$(lscpu | grep "CPU family" | awk '{print $3}')
model=$(lscpu | grep "Model:" | awk '{print $2}')
l1d_cache=$(lscpu | grep "L1d cache" | awk '{print $3}')
l1i_cache=$(lscpu | grep "L1i cache" | awk '{print $3}')
l2_cache=$(lscpu | grep "L2 cache" | awk '{print $3}')
l3_cache=$(lscpu | grep "L3 cache" | awk '{print $3}')

# Capture GPU information

gpu_info=$(nvidia-smi -L | sed 's/^/  /')
gpu_utilization=$(nvidia-smi --query-gpu=utilization.gpu --format=csv,noheader,nounits | tr '\n' ', ' | sed 's/, $//')

# Capture Memory information

total_mem=$(free -h | grep "Mem:" | awk '{print $2}')
used_mem=$(free -h | grep "Mem:" | awk '{print $3}')
free_mem=$(free -h | grep "Mem:" | awk '{print $4}')
total_swap=$(free -h | grep "Swap:" | awk '{print $2}')
free_swap=$(free -h | grep "Swap:" | awk '{print $4}')

# Capture Disk information

disk_info=$(df -h | grep "/dev/md0")
disk_used=$(echo $disk_info | awk '{print $3}')
disk_total=$(echo $disk_info | awk '{print $2}')

generate_markdown

# Summary

echo -e "\n### Summary"
echo '`markdown'
echo "- This system is powered by $cpus CPUs, with $cores_per_socket cores per socket and $threads_per_core threads per core."
echo "- The system's memory is $total_mem, with $used_mem currently in use."
echo '`'

```
