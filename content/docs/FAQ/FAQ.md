---
title: "FAQ"
type: docs
---

# Table of Contents

**1. Freezing a fork for a specific commit to prevent code from being outdate or broken**

**2. Documenting Your work after a Security Update**

## **FAQ: Freezing a Fork at a Specific Commit**

This FAQ explains how to fork a repository at a specific commit and ensure that it doesn't get updated in the future.

---

### 1. **How do I fork a repository?**

To fork a repository on GitHub:

1. Navigate to the repository you want to fork.
2. Click the **Fork** button in the top-right corner.
3. A copy of the repository will now appear under your GitHub account.

---

### 2. **How can I clone the forked repository?**

After forking, you can clone your copy of the repository with the following steps:

1. Open your terminal or Git Bash.
2. Run the following command, replacing `<your-username>` and `<repository>`:
   ```bash
   git clone https://github.com/<your-username>/<repository>.git
   cd <repository>
   ```

---

### 3. **How can I check out a specific commit?**

To freeze your fork at a specific commit, follow these steps:

1. Identify the commit hash of the commit you want to freeze.
2. Use the `git checkout` command to move to that commit:
   ```bash
   git checkout <commit-hash>
   ```

---

### 4. **Can I create a branch at that specific commit?**

Yes, creating a branch at a specific commit allows you to work on it while keeping the rest of the repository unchanged. Use the following command:

```bash
git checkout -b frozen-branch
```

---

### 5. **How do I prevent my fork from pulling updates from the original repository?**

To prevent updates, you can remove the original repository as a remote:

```bash
git remote remove origin
```

This ensures no new changes are pulled from the upstream repository.

---

### 6. **How do I push my frozen branch to my forked repository?**

To push the frozen branch to your GitHub fork, first make sure the remote is set to your fork, then push:

```bash
git remote add origin https://github.com/<your-username>/<repository>.git
git push -u origin frozen-branch
```

---

### 7. **What can I do to ensure the branch remains frozen?**

To ensure the branch doesn’t receive any updates:

- **Lock the Branch on GitHub:** You can lock the branch from the repository settings in GitHub.
- **Avoid Merging PRs:** Do not accept pull requests to this branch.

By following these steps, your repository will stay at the specific commit you selected.

---

### 8. **Can I still work on other branches without affecting the frozen one?**

Yes, you can freely create and work on other branches in the repository. Just avoid merging changes into your frozen branch.

---

### 9. **How can I restore the frozen state if someone makes a change by mistake?**

If someone accidentally updates the frozen branch:

1. Reset the branch to the specific commit using:
   ```bash
   git reset --hard <commit-hash>
   ```
2. Force-push the branch back to GitHub:
   ```bash
   git push origin frozen-branch --force
   ```

---

### 10. **Is there a way to enforce protection for the frozen branch?**

Yes, you can configure branch protection rules on GitHub:

1. Go to the **Settings** of your repository.
2. Under **Branches**, add a **Branch protection rule**.
3. Select the frozen branch and apply protection rules, such as disallowing force pushes or requiring pull request reviews.

---

## **Machine and File Space Checklist Reporting**

### **Sample Checklist**

### **Machines Used Commonly**

- **DGX1, DGX2, DGX3, TKL1, TK2, TKL3, others as applicable**

#### **File Spaces Used Commonly**

- **scratch1, scratch2, datasyncs, tkhome**

---

### **Example Checklist Entries**

#### **Arkash Jain**

- Machines used: `DGX1`, `DGX2`
- File spaces: `scratch1`
- Ran ASEM, CryoSamba, and Image Recognition.
- ✅ Verified access to `scratch1`, uploaded and downloaded files.
- ✅ Ran MATLAB script without issues.
- ✅ Checked GPU/CPU resource usage, no slowdown encountered.

---
### Notes from Team Members

- **@Ewa Sitarska**  
  Logging onto a remote machine and running MATLAB scripts.

- **@Adrian Coscia**  
  No current use for DGXs.  
  Running MATLAB scripts.

- **@Ricky**  
  The microscope computers can access `scratch` and the datasyncs.  
  Verified network access using `tkhpc32c` from outside the lab.  
  Accessed MATLAB and/or Fiji remotely.

- **@Beren Aylan**  
  Opened files and ran MATLAB code.  
  Accessed `Datasync 5` and `scratch` from both workstations.

- **@Nicholas Chow**  
  Remote access to confocal server.  
  Remote computer to run Fiji scripts.  
  Dreamspace computers: accessed scratch, ran Fiji and MATLAB codes.

- **@Anwesha**  
  **TBD**

- **@Anand**  
  **TBD**

- **@Bryan Zuniga**  
  Access to `scratch`.  
  Access to `Datasync 5`.

- **@Elliott Somerville**  
  Usage of Dreamspace computers.  
  Running MATLAB, Fiji, and Imaris.  
  Access to data storage spaces (`scratch`, `Datasyncs`).  
  Running Fiji scripts and MATLAB scripts.

- **@Gustavo**  
  No use of DGXs.  
  SSH to `tkl1` to use GPU.  
  Running MATLAB and Fiji scripts.

- **@Mari De Sautu**  
  Access to DGXs for denoising.  
  Running tomograms.

---

Let me know if you need further adjustments or additional sections for the wiki!


---

### **General Checklist:**

Here’s a general checklist to guide you:

1. **Task Execution:** Can you log into your assigned machine (e.g., DGX1, TKL1) and run your specific task (e.g., MATLAB, ASEM, Image Recognition)?
2. **File Space Access:** Can you upload and download files from `scratch1`, `scratch2`, or `datasyncs`? Do you have the correct permissions?
3. **System Performance:** Are the GPUs/CPUs responding as expected? Is there any slowdown or inconsistency in resource usage?
4. **Software Accessibility:** Can you access all necessary software (e.g., MATLAB, Fiji)?
5. **Remote Access:** Can you log into the machines remotely? (e.g., from outside the lab)

---
