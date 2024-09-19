---
title: Lab Computing and Image Analysis Tools
type: docs
---

## Using Labviewer for Track Observation

### Converting Tracked Traces to Labview File

1. Access MATLAB on tkl1 or tkl3
2. Open MATLAB
3. Navigate to: scratch → alex_labviewcodes → matlab_tools → microscopy
4. Open the file "MicroscopyBrowser_v(highest value).mlapp"
5. Click "Run" at the top
6. Follow the interface from left to right, ending at the bottom:
   - Change folder in left column to the analysis folder containing "ProcessedTracks.mat"
   - Check all Cat ID in the middle
   - Change folder in right column to the Deskewed data
   - Click the green arrow to load data in the middle
   - For multiple channels, use primary channel at the top and others below
   - At the bottom, change the analysis folder to where you want to save the Labview file
   - Click top left green arrow to load "ProcessedTracks.mat" (click once and wait for "DONE" status)
7. Let it run, then open and use Labviewer in Dream space

## Accessing Harvard Network

### Login to Scratch Network

1. Open terminal and use one of these commands:
   ```bash
   ssh "username"@tkl1.med.harvard.edu
   ssh "username"@tkl3.med.harvard.edu
   ```

### Using Apps on Scratch Network

To use applications like MATLAB or ImageJ via your own computer:

```bash
ssh -Y username@computername.med.harvard.edu
```

### Web Browser Access

After logging in:

1. Run `xdesk.sh`
2. Copy the provided link into your web browser and use the given code

### Long Computational Runs (e.g., CARE)

Use tmux for a solid connection:

```bash
tmux
```

Remember to log out when done:

```bash
tmux kill-session
```

### Non-Harvard Network Access

```bash
ssh username@xtal200.harvard.edu
```

### Accessing Files on Scratch via macOS

1. In Finder, press `Cmd+K`
2. Enter: `smb://tkfastfs`
3. Use credentials: tklabuser + Clathrin2016

### Checking GPU Availability

```bash
nvidia-smi
```

To watch continuously:

```bash
watch -n2 nvidia-smi
```

## Accessing BCH Network (Confocal)

For macOS:

1. In Finder, press `Cmd+K`
2. Enter: `smb://tk-fs.tch.harvard.edu`
3. Use username and password provided by sb-grid

## Accessing xdesk (Outside Harvard Network)

Optimized for Mac:

1. Open terminal and type: `ssh "account name"@xtal200.harvard.edu`
2. Enroll in Duo security if not done already
3. Accept push - you're now on the Harvard network
4. Type `ssh tkl1` or `ssh tkl3` for the desired server
5. Type `xdesk.sh` - This will show several alternatives
6. Open a new terminal and use the off-site solution
7. Copy the ssh command into the new terminal and enter your password
8. Accept the Duo security push
9. Return to the first terminal and copy the browser login (http://localhost:XXXX) into a browser
10. Use the accompanying password

You now have access to the server via xdesk

## 3D Image Presentation Tools

### Syglass - Virtual Reality

Notes from meeting with Michael Morehead:

- Clean up fluorescent images in Fiji before importing into Syglass (e.g., remove background)
- For streaming VR at conferences: [NVIDIA CloudXR SDK](https://developer.nvidia.com/nvidia-cloudxr-sdk)
  (Note: Requires fast internet connection, e.g., 5G mobile hotspot)

### Augmented Reality / 3D Image Presentation

Current status:

- Augmented reality of 3D surfaces possible via Imaris and Fiji
- Single image files can be exported to .stl or .wrl format and uploaded to Sketchfab
  (Note: 100MB file size limit; may require using fewer pixels)
- Giuseppe has experimented with creating .stl files via MATLAB (single images only, not animations)

#### Imaris Workflow

1. Import image and create surface (blue icon - follow instructions)
2. Export selected surface: "3D view" → "export selected"
3. Export as .wrl file
4. Upload to Sketchfab

#### Fiji Workflow

1. Open image and edit:
   - Apply background subtraction
   - Apply Gaussian filter
   - Convert to 8-bit image
2. Go to "Analyze" → "3D Objects counter"
3. Use slider to choose threshold and execute
4. Select the produced image ("Objects map" or "Surface map")
5. Go to "Plugins" → "3D viewer"
6. Choose the image for 3D view:
   - Display as "Surface"
   - Choose color
   - Set Threshold to 0
7. Go to "File" → "export surfaces" → "STL (ASCII)"
8. Upload the produced file to Sketchfab

#### Future Developments

- Exploring Python/MATLAB methods for STL file creation
- Python package `stl-numpy` can be used for this purpose
- Giuseppe has developed code to convert images to STL files
