---
title: Getting Started with the TKLAB Compute
type: docs
---

## Getting Started

[**Starter Page**](https://sites.google.com/tklab.hms.harvard.edu/tkdataprocessing/home/1-getting-started?authuser=0)

### Request Access

Welcome to TKlab. In order to access our online resources, a formal request needs to be filed by Patrick(stock@tklab.hms.harvard.edu) and Catherine(Catherine.Swan@childrens.harvard.edu). You will receive an email with instructions to activate your xtal200 account. You will be able to access the on-site machines in the dreamspace using your network account credentials. Please report any issues with the network in a timely manner contacting SBgrid(help@sbgrid.org), with Tom and Patrick in copy.
You can use the same credentials to connect via terminal to all the machines using a Linux based OS. The list of the machines hostnames is provided in the following paragraphs.

```
ssh username@xtal200.harvard.edu
ssh username@hostname
```

You can VPN to access the HMS network, instructions can be found at this [link](https://it.hms.harvard.edu/service/vpn). In case you are already on the HMS network, you can ssh directly to the host. You can also access a remote desktop on these machines by typing:
`xdesk.sh`
from terminal and following the instructions. More info can be found at this [link](https://sbgrid.org/corewiki/bch3-kirchhausen.md).
Machines running on Windows can be accessed by using Chrome remote Desktop (CRD). Please contact Patrick to know about how to access, and if you are prompted to input a temporary code to verify your identity.
Patrick will be also in charge to create an email addres on the domain tklab.hms.harvard.edus.

### Computational Access

**Machines accessible both on-line and on-site (from Dreamspace)**

In the following spreadsheet we list the machines accessible both online and on-site. On all machined both Matlab and Fiji are installed.

`https://docs.google.com/spreadsheets/d/1y-CXGBtFuOFbws3o7nWxWLtgcu1jEGh0M_QC-VAO9so/edit`

**Machines accessible online**

The following machines are only accessible via ssh or remote desktop (see above). On all machined both Matlab and Fiji are installed.

`https://docs.google.com/spreadsheets/d/1qtBn-swzXb_8CqOBhnKE7kEH1oCFwBqPNZ330fdrv-g/edit?usp=drive_open&ouid=104608780451973055923`

### CPU cluster

The CPU cluster is composed by 704 multicore CPUs and it is divided between 12 machines (tkv\*). Users are not supposed to connect to these machines via terminal. Install SLURM on your account to utilize of the CPU cluster. Each CPU in the cluster has the following properties:

```bash
model name : Intel(R) Xeon(R) Gold 6246 CPU @ 3.30GHz
cpu MHz : 1200.807
siblings : 24
cpu cores : 12
```

`https://docs.google.com/spreadsheets/d/1AP6MNF6-IWHaD_GDA85GDylcuBNrgevsLlSvjZf3WUE/edit?gid=0#gid=0`

### GPU Cluster

GPU cluster
The cluster is composed of 3 dgx-a100, for a total of 24 GPUs (model A100-SXM4-40GB) located in WAB 149. They are accessed directly as such:
`ssh username@tkdgx1.med.harvard.edu`
`https://docs.google.com/spreadsheets/d/1BcF1kL65NJvA5vabtX3bmEwW9F_vAde0x-aStjU-LWQ/edit?usp=drive_open&ouid=104608780451973055923`

### Online Servers

Data from the Lattice Light Sheet Microscope (LLSM) and the the Adaptive Optics Lattice Light Sheet Microscope (AO-LLSM) are transferred temporarily for processing in project folders /nfs/scratch, and permanently for storage in project folders - /nfs/datasync4

Data from the FIB-SEM are transferred temporarily for processing in project folders /nfs/scratch2, and permanently for storage in project folders - /nfs/data1expansion/FIBSEM_datasync3

Data for GPU processing are stored in DGX Cluster scratch storage /nfs/scratch2.
`https://docs.google.com/spreadsheets/d/13cDELynp5yGQpzeT5oCeIjYWrrhCd4h6i7xPGWuhzCk/edit?usp=drive_open&ouid=104608780451973055923`

### Software Package

The software can be found in the folder `/nfs/scratch/Gokul/GU_Repository`, and on our GitHub (also available at this link https://github.com/francois-a/llsmtools). All software runs under Matlab, unless stated otherwise.
