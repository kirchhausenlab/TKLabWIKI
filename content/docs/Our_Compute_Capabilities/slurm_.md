---
title: "SLURM Nodes"
draft: false
---

# SLURM Information

## Summary of SLURM Nodes

**TKL1-4 and DGX1-3 are not part of SLURM**
Below is a summary of the nodes:

### Node tkl1

- **Cores**: 32 (8 cores per socket, 2 sockets)
- **Memory**: 514646 MB
- **State**: DOWN\*
- **Reason**: Not in queue

### Node tkl2

- **Cores**: 32 (8 cores per socket, 2 sockets)
- **Memory**: 514646 MB
- **State**: DOWN\*+DRAIN
- **Reason**: Not in queue

### Node tkl3

- **Cores**: 32 (8 cores per socket, 2 sockets)
- **Memory**: 514638 MB
- **State**: DOWN\*+DRAIN
- **Reason**: OK

### Node tkv1

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv2

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv3

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv4

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv5

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv6

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv7

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv8

- **Cores**: 48 (12 cores per socket, 2 sockets)
- **Memory**: 1020251 MB
- **State**: IDLE+DRAIN
- **Reason**: Cause

### Node tkv9

- **Cores**: 80 (20 cores per socket, 2 sockets)
- **Memory**: 1544769 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv10

- **Cores**: 80 (20 cores per socket, 2 sockets)
- **Memory**: 1544769 MB
- **State**: IDLE
- **Partitions**: tk-cpu

### Node tkv11

- **Cores**: 80 (20 cores per socket, 2 sockets)
- **Memory**: 1544769 MB
- **State**: IDLE
- **Partitions**: tk-cpu

## Scripts

1. Determine the specs of each node in the cluster. Note you need access to all nodes in the cluster.

```bash
#!/bin/bash

# Create a directory to store the output
mkdir -p node_specs

# Loop over all nodes in the cluster
for node in $(sinfo -hN -o "%n"); do
  echo "Gathering specs for node: $node"
  # SSH into the node and run commands
  ssh $node "
    echo '### Node: $node' > /tmp/specs.txt
    echo '' >> /tmp/specs.txt
    echo '### CPU Information' >> /tmp/specs.txt
    lscpu >> /tmp/specs.txt
    echo '' >> /tmp/specs.txt
    echo '### Memory Information' >> /tmp/specs.txt
    free -h >> /tmp/specs.txt
    echo '' >> /tmp/specs.txt
    echo '### Disk Information' >> /tmp/specs.txt
    df -h >> /tmp/specs.txt
  "
  # Copy the specs file to your local machine
  scp $node:/tmp/specs.txt node_specs/$node-specs.txt
done
```

2. One script to rule them all

```bash
scontrol show node > node_info.txt
```
