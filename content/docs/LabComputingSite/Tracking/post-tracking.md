---
title: Post-tracking Processing
type: docs
---

# 7. Post-tracking Processing

### Introduction

In this section, we provide a list of codes developed for post-tracking analysis. The following procedures outline how to back up data from the scratch directory to `/nfs/datasync4` and various post-processing techniques applied to the tracked data.

---

### Data Backup After Processing

**Name of the code**: `transfer_from_scratch_to_datasync.m`

Once the data collected by the LLSMs has been deskewed and stored temporarily on `/datasync4/tklab-llsm` or `/datasync4/AO-llsm`, users can begin their processing, which includes detection, tracking, and post-tracking analysis. After completing the processing, users are required to back up the outputs and delete the corresponding folders from scratch. This code assists in copying the contents of the Analysis folders, maintaining the nested data folder structure, but excluding the TIFF stacks. If further analysis is needed, data can be copied back to scratch by merging the folder from `/datasync4/tklab-llsm` or `/datasync4/AO-llsm` with the corresponding folder in `/datasync4/username`.

---

### Bleach Correction

**Name of the code**: `bleach_in_a_box.m`

This code estimates the extent of fluorescence bleaching and corrects the tracks accordingly. Since illumination is not uniform in the vertical direction, the field of view (FOV) is divided into three parts, and the bleaching rate is estimated in each section by fitting the average signal background-subtracted with an exponential decay function. The output includes the fitted function in the three dimensions. The corrected data is saved as `ProcessedTracks.mat`, while the original tracks are preserved as `orig_ProcessedTracks.mat`.

```matlab
data = GU_loadConditionData3D;
bleach_in_a_box(data);
```

---

### Rotate LLSM Frames for Spinning Disk Orientation

**Name of the code**: `rotateFrame3D.m`

This code rotates de-skewed light sheet microscope frames for visualization. The angle between the LLS beam and the coverslip is 31.5°. The `zxRatio` parameter is calculated as follows: The distance between planes can be deduced from the experiment folder name, for example, in `Ex01_..._z0p5`, the sampling distance between planes is 0.5 μm. Here, `zxRatio = (0.5 * sind(31.5))/0.1`.

The paths in the example are indicative; users should adapt them to their specific cases.

```matlab
path_in = '/scratch/username/experiment_date/CS#/experiment#/ch#/DS/filename.tiff';
path_out = '/scratch/username/experiment_date/CS#/rotated_experiment#/ch#/DS/filename.tiff';
vol = readtiff(path_in);
[volout] = rotateFrame3D(vol, angle, zxRatio);
writetiff(volout, path_out);
```

---

### Split and Cluster Analysis

**Name of the code**: `bleach_in_a_box.m`

This script can be used to estimate co-localization between two compartments that have been tracked independently, estimate intensities based on 3D segmentation of non-PSF-like structures (e.g., endosomes), calculate the distance from the membrane, and create a cell outline mask from the PSF signal on the membrane.

---

### Save Tracks in AMIRA and Imaris Formats

**Name of the code**: `save_tracks_to_Amira.m`

This code is used to save tracks in formats compatible with AMIRA and Imaris for further analysis and visualization.

---

This documentation outlines the specific procedures and codes used in post-tracking processing for LLSM data. The steps described ensure proper data handling, including backup, bleaching correction, image orientation adjustment, and format conversion, enabling comprehensive analysis and visualization of tracked data.

---
