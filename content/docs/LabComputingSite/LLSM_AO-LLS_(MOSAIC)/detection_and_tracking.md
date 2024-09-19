---
title: Detection and Tracking
type: docs
---

# 5. Detection and Tracking

### Introduction

The detection and tracking routines are based on methods described in references [1,2].

- **Detection**:

  - The input image is filtered using two separate filters:
    - A detection model to identify pixels with significant signals.
    - A Laplacian-of-Gaussian filter to identify local maxima.
  - Local maxima at significant locations are used to initialize model fitting, which estimates fluorescence signal amplitude, local background, and sub-pixel location [2].
  - This code is designed for PSF-like particles; intensity estimates are less reliable for extended objects (e.g., endosomes). A solution for extended objects is presented in the Post-tracking processing section.

- **Tracking**:

  - Utilizes the u-track software [1], designed for:
    1. Tracking dense particle fields.
    2. Closing gaps in particle trajectories due to detection failures.
    3. Capturing particle merging and splitting events, whether due to occlusion or genuine aggregation/dissociation events.
  - The core algorithm solves correspondence problems as linear assignment problems, seeking a globally optimal solution.

- **cmeAnalysis**:

  - A post-processing algorithm specifically applied to clathrin-mediated endocytosis [2].

- **Software Availability**:
  - The software can be found at `/nfs/scratch/Gokul/GU_Repository` and on GitHub (also available at [this link](https://github.com/francois-a/llsmtools)).
  - All software runs under MATLAB unless stated otherwise.

---

### Particle Tracking on 2D Data

1. **Data Selection**:

   - Load data using:
     ```matlab
     data=loadConditionData
     ```
   - Follow instructions to select channels and indicate corresponding fluorescent markers (e.g., GFP).

2. **Tracking**:

   - Tracking can be performed on multiple compartments across different channels.
   - Tracking occurs on the primary channel; secondary channels' coordinates are probed for significant signals, and corresponding intensities are fitted.

3. **Fixed Position Tracking**:

   - For non-moving particles (e.g., viruses, single molecules):
     - Identify particle coordinates by calculating a max projection of the time series and locating local maxima.
     - Calculate the PSF size using a sub-resolution particle or estimate using the Abbe limit.
     - Example:
       ```matlab
       PSF_size=1.23;
       trackFixedPositions(data, PSF_size)
       ```

4. **Free Position Tracking**:
   - For freely moving particles:
     - Example commands:
       ```matlab
       PSF_size=1.23;
       runDetection(data, 'Sigma',PSF_size);
       runTracking(data);
       runTrackProcessing(data);
       ```

---

### Particle Tracking on 3D Data

1. **Data Selection**:

   - Load data using:
     ```matlab
     data=GU_loadConditionData3D
     ```
   - Follow instructions to select channels and indicate corresponding fluorescent markers.

2. **Evaluate Sigma**:

   - Calculate the PSF sigmas for particle detection:

     ```matlab
     PSFrt = '/scratch/username/experiment_date/LLSM_calibration';
     PSF488 = '488totalPSF.tif';
     PSF560 = '560totalPSF.tif';
     PSF642 = '642totalPSF.tif';

     [sigmaXY488, sigmaZ488] = GU_estimateSigma3D([PSFrt filesep],PSF488);
     [sigmaXY560, sigmaZ560] = GU_estimateSigma3D([PSFrt filesep],PSF560);
     [sigmaXY642, sigmaZ642] = GU_estimateSigma3D([PSFrt filesep],PSF642);

     zRatio = (0.5 * sind(31.5))/0.1;

     sigmaZ488corr = sigmaZ488/zRatio;
     sigmaZ560corr = sigmaZ560/zRatio;
     sigmaZ642corr = sigmaZ642/zRatio;
     ```

3. **Fixed Position Tracking**:

   - For non-moving particles in 3D:
     ```matlab
     GU_trackFixedPositions3D(data, 'Sigma', [sigmaXY488, sigmaZ488corr; sigmaXY560, sigmaZ560corr; sigmaXY642, sigmaZ642corr;])
     ```

4. **Free Position Tracking**:
   - For freely moving particles in 3D:
     ```matlab
     GU_runDetTrack3d(data, 'Sigma', [sigmaXY488, sigmaZ488corr; sigmaXY560, sigmaZ560corr; sigmaXY642, sigmaZ642corr;]);
     ```

---

### How to Run Tracking on Images Restored Using CARE

1. **CARE Background Modulation**:

   - CARE introduces background modulation, which the algorithm detects as valid instances with low intensities. These need to be filtered before tracking.
   - Example procedure:
     ```matlab
     GU_runDetection3D(data, 'Sigma', [SigmaXY,SigmaZ])
     load([data.channels{1} 'Analysis' filesep 'Detection3D.mat'])
     histogram(frameInfo(t).A(1,:))
     ```

2. **Filter Unwanted Detections**:

   - Example to remove unwanted detections:
     ```matlab
     GU_filterDetections3D(data,'Threshold',th)
     ```

3. **Complete Tracking**:
   - After filtering, run:
     ```matlab
     runTracking3D(data)
     GU_runTrackProcessing3D(data)
     ```

---

### Detection and Tracking Metrics

Metrics present in `Detection3D.mat` and `ProcessedTracks.mat` include:

- `t`, `f`, `x`, `y`, `A`, `c`, `x pstd`, `y pstd`, `A_pstd`, `c_pstd`, `sigma_r`, `SE_sigma_r`, `pval_Ar`, `isPSF`, `tracksFeatIndxCG`, `gapVect`, `gapStatus`, `gapIdx`, `seqOfEvents`, `nSeg`, `visibility`, `lifetime_s`, `start`, `end`, `startBuffer`, `endBuffer`, `MotionAnalysis`, `maskA`, `maskN`, `RSS`, `mask_Ar`, `hval Ar`, `hval_AD`, `catIdx`, `isCCP`, `isDetected`, `significantMaster`, `significantVsBackground`, `significantSlave`

- **'t'**: Time in seconds of the traces 
- **'f'**: Frame number of the traces 
- **'x'**: Estimated x-position from Gaussian fit 
- **'y'**: Estimated y-position from Gaussian fit 
- **'z'**: Estimated z-position from Gaussian fit. Please note that the z coordinates are flipped when compared to the TIFF stacks.
- **'A'**: Estimated Intensity (Integrated intensity) from Gaussian fit 
- **'c'**: Estimated background intensity (Integrated intensity) from Gaussian fit 
- **'x pstd'**: Error on 'x' from fit estimated through error probability (hessian) 
- **'y pstd'**: Error on 'y' from fit estimated through error probability (hessian) 
- **'A_pstd'**: Error on 'A' from fit estimated through error probability (hessian) 
- **'c_pstd'**: Error on 'c' from fit estimated through error probability (hessian) 
- **'sigma_r'**: Estimated standard deviation of Gaussian fit 
- **'SE_sigma_r'**: Estimated error standard deviation of Gaussian fit from error probability (hessian) 
- **'pval_Ar'**: P-value for the fit given data comes from Gaussian distribution PSF 
- **'isPSF'**: Anderson-Darling test (normality) on residuals of PSF 
- **'tracksFeatIndxCG'**: Gap closed (CG) Indices of the detections in a movieInfo structure (which detections are in the traces) 
- **'gapVect'**: The gap locations along the trace. Essentially tells you if the trace is compounded (isnan(x)): 00001000 
- **'gapStatus'**: Tells whether the gaps in gapVect are valid (4) or invalid (5). Gap is valid if segments that precede/follow are within 1 frame or if gap is a single frame. For gapVect 00001000, gapStatus would be 4; for 00110, it would be 5 
- **'gapIdx'**: The track index where the gap occurs; for 00110, it would be [2,3] 
- **'seqOfEvents'**: Matrix with the number of rows equal to the number of events happening in a track and 4 columns:
  1st: Frame where event happens
  2nd: 1 - start of track, 2 - end of track
  3rd: -
  4th: NaN - start is a birth and end is a death; number - start is due to a split, end is due to a merge. The number is the index of the track segment for the merge/split. 
- **'nSeg'**: Number of segments appearing in the data. For compounded traces, this would be greater than 1 
- **'visibility'**: Extra grouping of the tracks. 1: complete tracks, 2: incomplete tracks (truncated at the beginning or end of the acquisition), 3: persistent (present throughout the entire acquisition) tracks. 
- **'lifetime_s'**: Duration in seconds 
- **'start'**: The start ID from 'seqOfEvents'. 
- **'end'**: The end ID from 'seqOfEvents'. 
- **'endBuffer' & 'startBuffer'**: CCS fluorescence prior to the first detected time point and following the last detected time point was estimated for a fixed number of “buffer” frames (typically 5), using sub-pixel localization of the 2-D Gaussian model described above. For each frame of these buffer readouts, the localization was initialized with the values of the signal at the first or last time point of the track, respectively. The localization was considered valid if the resulting position was within 2σ pixels (≈200 nm) of the initialization; otherwise, the amplitude and background values were estimated by least squares using the position of the first and last detection, respectively. 
- **'MotionAnalysis'**: Displacement statistics. Only computed if in class 1: (totalDisplacement, MSD, MSDstd) 
- **'maskA'**: Average intensity of the mask pixels for a detection spot 
- **'maskN'**: Number of pixels in the mask. 
- **'RSS'**: Residual sum of squares of the peak detection fit 
- **'mask_Ar'**: Number of significant pixels 
- **'hval Ar'**: Frames where the hypothesis of significance is true from a 1-sided t-test (and a first channel that I don’t understand; it is probably from the slave channel which is just set to 1) 
- **'hval_AD'**: Hypothesis value for being a diffraction-limited spot. 
- **'catIdx'**: Category; possible categories are listed above 
- **'isCCP'**: Whether the spot is CCP. This is based on a whole lot of different criteria, but the essentials are: All tests are almost perfect. 
- **'isDetected'**: Related to significance level in the slave channel. Used to compute whether this channel is significantly above noise. 
- **'significantMaster' & 'significantSlave'**: Test whether the number of significant detections in the slave channel of this track (independent of the master channel) is above chance. The expected number of chance detections for a track of length L is given by the inverse binomial CDF. 
- **'significantVsBackground'**: 1 if above the 95th percentile of amplitude detection significant on the slave channel, 0 otherwise. Used to compute significantSlave from a binomial.---

### Tracks Categories (Metric `catIdx`)

- **Category 1**: Single tracks with clathrin-like behavior.
- **Category 1b**: Single tracks with invalid gaps.
- **Category 1c**: Single tracks cut at the beginning or end.
- **Category 1d**: Persistent single tracks.
- **Category 2a**: Compound tracks with clathrin-like behavior.
- **Category 2b**: Compound tracks with invalid gaps.
- **Category 2c**: Compound tracks cut at the beginning or end.
- **Category 2d**: Persistent compound tracks.

---

