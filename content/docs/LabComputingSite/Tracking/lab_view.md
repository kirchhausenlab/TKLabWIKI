---
title: Tracks Visualizer - Matlab
type: docs
---

# 8. Tracks Visualizer - Matlab

### Introduction

Visualizing 3D data can be challenging, but several tools are available to help browse data and tracks effectively. These tools allow users to view 2D projections of the data in XY, XZ, and YZ planes, facilitating easier analysis of tracked data.

---

### Tools and Commands

**Commands**:

- `GU_calcImageProjections.m`
- `GU_cme3d2dViewer.m`

**Usage**:

1. **Load and Project Data**:

   Use the following commands to load the 3D data and calculate the 2D projections:

   ```matlab
   data = GU_loadConditionData3D;
   GU_calcImageProjections(data);
   ```

   The `GU_calcImageProjections` command generates 2D projections of the data in XY, XZ, and YZ planes. Ensure that you load the data before calculating the projections and save the data variable, as the command will not function properly without it.

2. **Visualize Tracks**:

   After generating the projections, you can use the viewer to interact with the data:

   ```matlab
   GU_cme3d2dViewer(data);
   ```

   The `GU_cme3d2dViewer` command allows users to:

   - Select tracks by duration and category.
   - Highlight detections for better visualization.

---

### Description

- **GU_calcImageProjections.m**: This script calculates 2D projections (XY, XZ, YZ) of 3D tracked data. It is essential to load the data and save the variable before using this command, as it will not work with unsaved data.

- **GU_cme3d2dViewer.m**: This viewer tool provides an interactive interface to explore and visualize tracks and detections. Users can filter tracks based on duration and category and highlight specific detections to facilitate detailed analysis.

---

This section provides the necessary tools and commands for effectively visualizing 3D data by projecting it into 2D planes and interacting with the tracks through an intuitive viewer interface.

---
