---
title: LLSM
type: docs
---

## 4. LLSM / AO-LLS (MOSAIC) Deskew

When images are acquired using the Lattice Light Sheet Microscope (LLSM) or the Adaptive Optics - LLS (AO-LLS), from the Multimodal Optical Scope with Advanced Imaging Correction MOSAIC microscope, the orientation of the images are tilted in relation to the sample coverslip. In both microscopes, the excitation (EO) and detection (DO) objectives are at 30 and 60 degree angle towards the sample coverslip, respectively. Thus, the acquired data needs to be "DeSkewed" (DS) to reorient the images to the conventional imaging geometry, at which the imaging axis is orthogonal to the detection objective, like a conventional Confocal or a Spinning Disk microscope.

The following protocol describes the steps to perform DeSkew (DS) on experimental data using a MATLAB script.

### General Notes

The following notes and instructions guide microscope users on how to perform "online" data DeSkew. The term "online" means that the data is being pre-processed while acquired, using the LLSM or the AO-LLS imaging mode from the MOSAIC microscope.

The data pre-processing includes:

- **Data DS**: The 3D-stack data acquired must be DeSkewed (DS) due to the 60° angle of the Detection Objectives (DO) in relation to the sample motion. After DS, the data is transformed as if the sample was moving orthogonally towards the DO, as it is done in any inverted/Upright microscope when a Z-stack is acquired.

- **Data Illumination correction**: The Lattice illumination profile is not constant at the image Field of View (FOV), hence that is corrected for the acquired data.

- **Chromatic offset correction**: Chromatic offset occurs because different wavelengths have different focal planes. The shift between different wavelengths is dependent on the optical elements used along the beam path. When a 2-3 color experiment is performed, complementary empty images are added to each color data 3D-stack, bringing all the colors to the same co-localized z plane. This process is calculated through imaging Tetra-Spectral beads.

- **Lateral chromatic offset**: For at least 2 color experiments, using the images of a single Tetraspec bead, after the z chromatic offset correction, there might be a mismatch for the colors along the xy plane: the same bead imaged with two different wavelengths is not overlapping. Hence the mismatch is calculated in the number of pixels along the xy plane. In case of a 3 color experiment, the lateral chromatic offset is calculated for the two wavelengths imaged at the same camera.

- **Camera lateral offset** (only for 3 color experiment): During the microscope calibration, the microscope's two Cameras, A and B, are manually adjusted to image the same exact plane using Tetraspec beads as reference (i.e., 560nm is imaged with Camera A and 488nm is imaged with Camera B). The offset calculation checks if the same Tetraspec bead imaged with Camera A and B, with their respective wavelengths, is located at the same xy position at both cameras. If a shift of at least 1 pixel is detected, it will be corrected during DS processing.

### 2. Calibration Folder

To perform the "online" DS, the microscope calibration data must be saved in the LLSM/AO-LLS microscope workstation following the structure showed in Figure 1. 

Figure 1 - Calibration folder “LLSCalibrations_p5_p55” / “LLSCalibration” structure examples, for AO-LLS and LLSM.

In Figure 1, the “LLSCalibrations_p5_p55” / “LLSCalibration” folders are found inside the experiment main folder “20220428_p5(…)”. These folders and their name’s structure are created by the microscope operator. In case of doubt on how to name the experiment, calibration folder and subfolders, follow the instructions from Figure 2. 

Figure 2 - Experiment folder, Calibration folder and subfolders naming structure.

It is important to check that the calibration “bk”, “illum” and “chroma” subfolders are not empty. Otherwise, the software might crash, and an error is prompt. In case the experiment is a single-color experiment, the “chroma” folder is not necessary. Therefore, the folder might not be created.

The “PSF” and “XZPSF” subfolders are not required for online data DS, these folders data certify that the system was tunned and the calibration was performed properly. Additionally, for post-data acquisition and DS when running the Matlab Clathrin Mediated Endocytosis (CME) analysis package: the individual beads PSF’s for each of the colors used in the experiment will be required.


### 3. "Online" Data DS

Once the microscope is calibrated by the microscope operator, the first procedure is to upload the microscope calibration data into the DS MATLAB script. The DS MATLAB script will use the calibration data to compute the variables that will be needed to DS the experimental data.

This section of the document is divided in 3 subsections:

-         Calibration data upload for LLSM and AO-LLSM data – the instructions indicated are common to the two microscopes. The instructions guide the user on how to set and run the MATLAB code in order to upload the calibration data necessary for data DS. The user will notice that for data acquired with the LLSM, the user interaction with the code ends when the illumination correction folder is indicated.
-         Lateral chromatic offset and camera lateral offset calculation – the instructions at this subsection are directed to data acquired with the AO-LLS microscope. The user can opt to set the calibration data to use for the lateral chromatic offset/camera offset calculations, namely: the overall PSF or the sample scan PSF acquisition mode. For the LLSM data this is done automatically, using the calibration data acquired under the overall PSF acquisition mode.
-         Experiment data DS – this subsection is valid for both microscopes, the user must indicate the Experiment number with the raw data to be DS.


3.1 Calibration data upload for LLSM and AO-LLS data

1.   		Using one of the TKLab linux machines in the cluster (following the "ssh (...)"), and after opening the machine terminal, following the instructions from Figure 3: MATLAB is opened. Although the example from Figure 3 shows the user "rcorreia" connecting to "tkl1", for data DS upon a Labmeeting from Giuseppe Di Caprio, on 2022-08-16, the machine to use for DS should be "tkhpc48".

Figure 3 - Opening MATLAB after accessing one of the TKLab linux machines in the cluster.

2. 		Once in MATLAB, the DS script file “currentDeskew_20220505.m” must be opened (Figure 4, red rectangle). Whenever an update is performed in the DS script code the users receive an email or a slack message. The most updated Matlab DS scripts can be found in "scratch\llsm-deskew\afterAcquistion_20210617\Code\20220728_MostUpdated_DS". The date in the folder (20220728) reflects the date of the most updated version. The user MUST NOT run the script form this folder, instead the user MUST copy it to their personla scratch folder and running it from there. Additionally, no changes should be performed at the DS core codes. In case of errors, crashs or ideas for changes: reach to TK, Ricky, Gu and/or Giuseppe.
At the DS script the experiment folder, “dirSource”, must be manually inserted (highlighted in blue in Figure 4). 

Figure 4 - The DS script opened in MATLAB, red rectangle. The experiment folder, "dirSource" (highlighted in blue), must be updated accordingly.

3. 		The instructions in Figure 5, illustrate the steps to follow in MATLAB to get the experiment folder name path and set it as “dirSource” in the script. Following the instructions, in Step 2 of Figure 5, if the experiment was performed using the LLSM the user must select the “tklab-llsm” folder or the “AO-LLSM” folder in case of the AO-LLS. In Figure 5, the green rectangle in step 5, the MATLAB “Current Folder”, shows all the experiments’ folders. 

Figure 5 - Following steps 1-5 the user accesses the experiment folder through Matlab. The scope used for the experiment: "tklab-llsm", for LLSM, or "AO-LLSM", for AO-LLS experiment, is needed in step 2. As an example, the green rectangle shows the experiments listed inside the AO-LLSM drive.

Selecting the day experiment folder (one of the folders inside the green rectangle from Figure 5), by double clicking on it, updates the Matlab main folder, and the user can copy that folder path and state it as the “dirSource” in the DS Script. These steps are illustrated in Figure 6. 

Figure 6 - Steps 6-8 show how to set the "dirSource" in the DS script. Step 6 shows two ways to access the experiment main folder, -a and -b.

4. 		The other path to set on the DS script is the destination folder, “dirSink”, for the DS data storage. The “dirSink” folder is defined by the user, and it is usually located inside the scratch drive: it is the user personal folder.  As illustrated in Figure 7.


Figure 7 - Setting the "dirSink" path (highlighted in blue), the DS data destination folder.

5. 		The number of Central Processing Units (CPUs) to use during data parallel DS must be set by the user, “N_CPU” in the DS script as shown in Figure 8. Usually the number of CPUs is selecting to match the number of images acquired in each 3D-stack.

Figure 8 - The number of CPUs, "N_CPU", for parallel DS is defined by the user.

6. 		The user must set the folder path for long term raw and DS data storage, as in Figure 9. 

Figure 9 - Highlighted in blue, “datasync_dirSink”, is the folder path for raw data and DS data long term storage.

7. 		After setting the folder paths indicated previously, the pre-processing and upload of the experiment calibration data is ready to be executed. To proceed, the code must run from the same folder at which the DS script is saved, Figure 10, and that usually is set to be from Scratch.

Figure 10 - Ensure the MATLAB runs from the same folder at which the DS script, "currentDeskew_20220505", is saved. The folder paths inside the red and yellow rectangles must match.

The DS script, is a single script divided in two sections:
- In Matlab the division of the two sections is marked by the symbol ‘%%’, (red arrow in Figure 11).


Figure 11 - DS Script is divided in two sections. The '%%' symbol marks the sections division. The first section of the script has a yellow background color, while the second section have a white background.

- The first section of the script code relates to uploading the experiment calibration data, in Figure 11 with a yellow background.
- The second section of the code relates to performing the experimental data DS, in Figure 11 with a white background.
To select between each of the sections the user must click with the cursor in the section of interest and automatically the background color of the code changes to ‘yellow’ for the section selected as it is illustrated in Figure 12.


Figure 12 - In contrast to Figure 11, now the second section of the script (to perform the experiment data DS) have a yellow background color. It was selected by clicking with the mouse cursor at the portion of the script code below the '%%' symbol (red arrow).

8. Through selecting the first section of the DS script code, identified by the yellow background color, as shown in Figure 13, by clicking at the MATLAB “Run Section” button (red arrow and rectangle in Figure 13) the experiment calibration data starts to be uploaded.

In MATLAB when section is being executed, after clicking in the “Run Section” button (Figure 13) the “Pause” button becomes enabled as it can be observed in Figure 14, red rectangle.


Figure 14 - In Matlab when the "Run Section" button is clicked -> the "Pause" button becomes enabled, indicated by the red rectangle.

9. 		When running the DS script code first section a message dialog box is prompted, Figure 15 blue rectangle.
The dialog box shown in Figure 15, blue rectangle, is related to a specific 4 colors experiment:
- when performing data set acquisition for Content-Aware image REstoration (CARE) training, the user should click on the “Yes” button.
- In case the experiment performed is with 3 colors or less, the user should always click on the “No” button.


Figure 15 - A dialog box (inside the blue rectangle) prompts upon clicking on "Run Section" for the script first section (Figure 13), if the experiment is performed with less than 4 colors the user must click on "No" button.

10. 		While the code runs:
- a job folder and files are created at the script main folder, Figure 16 red square.
- Additionally, information regarding the code execution status will be printed at the MATLAB “Command Window” (Figure 16 green rectangle).
- While the “Pause” button (Figure 14) is enabled, the code is still running.

Figure 16 - While the code is running a job folder and files are created at the script main folder, red square; and, at the Matlab "Command Window" information is printed to update the user about the code running status, green rectangle.

11. 		A new dialog box is prompted, Figure 17, asking for the user interaction to indicate the folder from which the illumination correction calibration images can be uploaded.
Note that the user must select the “nB_Dither” folder, as indicate in Step 2 from Figure 17, and then click on the “Open” button. If the data was acquired with the LLSM the folder name is “illum”.


Figure 17 Dialog box to indicate the illumination correction calibration images, following Steps 1 and 2, the user must select the "nB_Dither" folder followed by clicking on the "Open" button to proceed.

12. 		If the experiment was performed using the LLSM the data calibration upload requiring the user action terminates at the previous point the user can move to subsection 3.3 Experiment Data DS.
13. 		If the data was acquired using the MOSAIC, AO-LLS mode and the experiment is at least 2 color experiment proceed to next subsection. Otherwise, move to 3.3 Experiment Data DS.

3.2   Lateral chromatic offset and camera lateral offset calculations

The following instructions are implemented on experiments performed using the MOSAIC – AO-LLS acquisition mode. Additionally, the following are implemented only for 2-3 color experiments. It is possible to update the code for 4 color experiments and onwards, but at the date of the code and of this manual that is not implemented.

1. 		Upon indicating the illumination calibration folder, “nB_Dither” as illustrated in Figure 17, the user will need to set the folder for which the Lateral chromatic offset should be performed. Figure 18 demonstrates the steps required to perform the lateral chromatic offset.


Figure 18 - Following Steps 1 - 4, the user indicates the folder at which Tetra-spectral beads were imaged with 488 and 514nm laser lines. Upon indicating the folder in step 4 the user clicks at the “Open” button to resume the lateral offset calculation.

- The dialog box will open the “Ex01_(…)” experiment folder inside the “chroma” folder, step 1 from Figure 18.
- Proceeding, the user must select the “LLSCalibrations_p5_p55” folder and then double click on the “PSF” folder, Figure 18 steps 2 and 3, respectively.
- Finally, as in step 4 of Figure 18, the folder is selected with a single mouse click at the only “Ex01_(…)” folder followed by clicking at the “Open” button.
- Hence, the user directs the code to use the tetra-spectral beads data acquired using sample scan motion. 
If the user intents to use the tetra-spectral beads imaged using the overall psf acquisition motion, instead of sample scan motion, the user must indicate the “Ex01_(…)” inside the chroma folder. Although, the best to consider is the tetra-spectral bead imaged with sample motion acquisition mode. The correction result is plotted in a Matlab figure panel, Figure 19.

The user should not close the Matlab figure, with the lateral chromatic offset.


Figure 19 - The images show a tetra-spectral bead imaged with 488nm (green) and 642nm (red) laser lines. On top: the beads don’t overlap, before the lateral chromatic correction. At the bottom: the beads do overlap after the lateral chromatic offset execution.

2. 		If the experiment is a 2-color experiment, the instructions for performing the lateral correction are finished. The user can proceed to the following subsection 3.3 Experiment Data DS of this manual. 

3. 		Note that the previous lateral chromatic offset was calculated for beads imaged with the same camera, CamB (Figure 19). A new dialog box pops and asks for the calibration folder and the user should follow the steps described in Figure 18. For a 3-color experiment, the second lateral chromatic offset is calculated between the beads imaged with Camera A (CamA) and Camera B (CamB), illustrated in Figure 20. 


Figure 20 - The images show a tetra-spectral bead imaged with 488nm (green-CamB) and 560nm (red-CamA) laser lines. On top: the beads don’t overlap, before the lateral chromatic correction. At the bottom: the beads do overlap after the lateral chromatic offset execution.

The user should keep both Matlab figures opened in background, Figure 21. Hence, while the experiment is performed the user can always visually consult what is the computed lateral chromatic offset.


Figure 21 - The 2 lateral chromatic offset results: A) a tetra-spectral bead illuminated with 488 and 642nm laser lines and imaged by the same camera, CamB; B) the same tetra-spectral bead illuminated with 488 and 560nm laser lines and imaged by 2 different cameras, CamB and CamA, respectively.

Additionally, the user can always check what are the chromatic offset values in number of pixels along the horizontal (dx) and vertical (dy) axes (NOTE FOR THE LLSM dx IS VERTICAL AXIS AND dy IS HORIZONTAL AXIS):
- in Figure 22 the variables pointed by the blue arrows, “Chroma_Translation_CamACamB_dx” and “Chroma_Translation_CamACamB_dy”, store the lateral chromatic offset in number of pixels between the 2 cameras, for the 2 laser lines used while imaging with CamA and CamB, respectively.
- In Figure 22 the variables pointed by the yellow arrows, “Chroma_Translation_dx” and “Chroma_Translation_dy”, store the lateral chromatic offset in number of pixels between the 2 cameras, for the 2 laser lines used while imaging with CamA and CamB, respectively.


Figure 22 - The lateral chromatic offset values, for the same camera and for different cameras.

3.3 Experiment Data DS

Once the steps described on subsections 3.1, and 3.2 for AO-LLS data and if a 2-3 color experiment was performed, were followed, then the Matlab Command Window will prompt a message stating that the user can proceed to data DS (Figure 23).


Figure 23 - When the MATLAB code is ready to DS, the MATLAB Command Window prompt the message shown at the image.

The experimental data is DS by clicking at the second section of the DS script, setting the experiment number(s) to DS followed by a click on the “Run Section” button (Figure 24).


Figure 24 - To start DS the data, the number(s) of experiments to DS must be indicated (red rectangle) and then click on the "Run Section" button (black rectangle).

When the DS starts the MATLAB Command Window prompts the Experiments, “Ex”, number(s) inserted and the folders from which the data will be DS, figure 25.



Figure 25 - The Matlab Command Window prompts the Experiment, "Ex", number inserted by the user as well as the number of folders containing that specific Ex. Hence, the DS was initialized.

Once the DS finishes the Matlab command window prompts a final message informing the user that the data was processed and if required a new Experiment number(s) can be inserted as it is shown in Figure 26.
To perform a DS from another Experiment number, the user can insert the number at the beginning of the DS script as exemplified in Figure 24, at the red rectangle.


Figure 26 - When the DS is completed the MATLAB Command Window informs the user that the process was completed and if required the user can insert a new Experiment number(s) to DS.

Following all the previous allow the user to perform "online" data DS.
If errors occurr the user should take a picture of the error, or a screenshot, and send it to Ricky and/or Gu to help understanding what triggered that error. 
