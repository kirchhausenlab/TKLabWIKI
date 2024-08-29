# Updating Lab Wiki for Everyone

To get the code on your computer, please ensure you have git installed and ask Arkash Jain to add you to the repo

```bash
git clone https://github.com/kirchhausenlab/TKLabWIKI.git
```

Simply go under **contents > docs ** and make a new folder for wiki if it doesn't exist. Please make an empty `_index.md` file first.

Then name whatever file you want to create and end it with a **.md** extension

## Making Docs

**Setup**

Make a title, date, and say draft as false for the new page

```bash
---
title: "GitHub"
date: 2024-08-15
draft: false
---
```

After this, treat every "webpage" as a readme and format it as you would a README

```bash
├── README.md
├── archetypes
│   └── default.md
├── assets
│   └── _custom.scss
├── content
│   ├── .DS_Store
│   ├── _index.md
│   ├── docs
│   │   ├── .DS_Store
│   │   ├── Active Projects
│   │   │   ├── .DS_Store
│   │   │   ├── Asem
│   │   │   │   ├── Project.md
│   │   │   │   └── _index.md
│   │   │   ├── CARE
│   │   │   │   └── _index.md
│   │   │   ├── Cryosamba
│   │   │   │   ├── Advanced.md
│   │   │   │   ├── Paper.md
│   │   │   │   ├── Project.md
│   │   │   │   ├── _index.md
│   │   │   │   └── cryosamba.png
│   │   │   ├── Image Recognition
│   │   │   │   └── _index.md
│   │   │   └── _index.md
│   │   ├── GitHub
│   │   │   ├── Github.md
│   │   │   ├── _index.md
│   │   │   └── github.png
│   │   ├── LabComputingSite
│   │   │   ├── CARE
│   │   │   │   ├── _index.md
│   │   │   │   └── care.md
│   │   │   ├── GettingStartedAtTKLAB
│   │   │   │   ├── Quickstart.md
│   │   │   │   ├── SLURM.md
│   │   │   │   └── _index.md
│   │   │   ├── LLSM_AO-LLS_(MOSAIC)
│   │   │   │   ├── LLSM.md
│   │   │   │   └── _index.md
│   │   │   ├── LabComputingSite.md
│   │   │   ├── References
│   │   │   │   ├── _index.md
│   │   │   │   └── references.md
│   │   │   ├── Tracking
│   │   │   │   ├── _index.md
│   │   │   │   ├── detection_and_tracking.md
│   │   │   │   ├── lab_view.md
│   │   │   │   └── post-tracking.md
│   │   │   ├── _index.md
│   │   │   ├── neuroglancer.md
│   │   │   ├── remote_access.md
│   │   │   ├── ssh.md
│   │   │   └── wiki.png
│   │   ├── Nvidia-Cuda
│   │   │   ├── DeepLearningSetup.md
│   │   │   └── _index.md
│   │   ├── Python
│   │   │   ├── _index.md
│   │   │   ├── conda_env.md
│   │   │   ├── production_poetry.md
│   │   │   └── python-virtual-environment.md
│   │   └── SBGRID_WIKI
│   │       ├── .DS_Store
│   │       ├── SBgrid.md
│   │       ├── _index.md
│   │       └── sbgrid.png
│   └── menu
│       └── _index.md
├── hugo.toml
├── layouts
│   ├── _default
│   │   └── index.html
│   └── shortcodes
│       └── toc.html
```
