---
title: Access Resources Directly from Off-site with Key-Based SSH
type: docs
---

## Accessing Resources Off-site with Key-Based SSH

### Purpose

When accessing resources from off-site, such as running a Jupyter notebook on `tkl1` or `tkl3` or exploring data with Neuroglancer, it can be cumbersome to first SSH onto `xtal200` and authenticate with 2FA. This guide will show you how to streamline this process by using key-based SSH, allowing you to access applications served by on-site resources in a single SSH step.

### Reference

This guide is based on the steps outlined in the [SBGrid FAQ on the topic](#), with minor edits to accommodate Windows machines and our lab's computing setup.

### Step 1: Create an SSH Key

1. **Generate an SSH Key:**

   On your local machine (Mac/Linux/Windows), run the following command:

   ```bash
   ssh-keygen -t rsa
   ```

2. **Store the Key:**

   You will be prompted to choose where to store the key. Either accept the default location or specify a different one. Make note of this address.

3. **Set a Password:**

   Set a password for the SSH key when prompted.

### Step 2: Upload the SSH Key to SBGrid Authentication Servers

1. **Access `xtal200`:**

   SSH into `xtal200.harvard.edu` as usual:

   ```bash
   ssh your_username@xtal200.harvard.edu
   ```

2. **Copy Your Public Key:**

   Open a text editor on your local machine and navigate to the `id_rsa.pub` file. This file contains the public part of the SSH key you just created. Copy its contents.

3. **Upload the Key:**

   In your `xtal200` terminal, run the following command, replacing the placeholder with your copied key:

   ```bash
   ipa user-mod $USER --sshpubkey="ssh-rsa AAAlkf35sj7sl8kfjsadkjflkdsadj"
   ```

   You can now close the `xtal200` session.

### Step 3: Modify the SSH Configuration File on Your Local Computer

#### For Mac/Linux

1. **Create/Modify the SSH Config File:**

   If you do not have a `config` file at `~/.ssh/config`, create one. Edit the file to include the following:

   ```bash
   Host *
       ForwardAgent yes
       UseKeychain yes
       AddKeysToAgent yes

   Host tkl1_p
       HostName tkl1
       User your_sbgrid_username
       ProxyJump xtal200

   Host tkl3_p
       HostName tkl3
       User your_sbgrid_username
       ProxyJump xtal200

   Host dgx1_p
       HostName tkdgx1.med.harvard.edu
       User your_sbgrid_username
       ProxyJump xtal200
       IdentityFile /path/to/your/id_rsa

   Host xtal200
       HostName np.sbgrid.org
       User your_sbgrid_username
       IdentityFile /path/to/your/id_rsa
   ```

2. **Access Resources:**

   You can now access these resources with a single SSH command, e.g.:

   ```bash
   ssh tkl1_p
   ```

#### For Windows

1. **Create/Modify the SSH Config File:**

   If you do not have a `config` file at `\Users\YourUsername\.ssh\config`, create one. Edit the file to include the following:

   ```bash
   Host *
       ForwardAgent yes
       UseKeychain yes

   Host tkl1_p
       HostName tkl1
       User your_sbgrid_username
       ProxyJump xtal200
       IdentityFile \path\to\your\id_rsa

   Host tkl3_p
       HostName tkl3
       User your_sbgrid_username
       ProxyJump xtal200
       IdentityFile \path\to\your\id_rsa

   Host dgx1_p
       HostName tkdgx1.med.harvard.edu
       User your_sbgrid_username
       ProxyJump xtal200
       IdentityFile \path\to\your\id_rsa

   Host xtal200
       HostName np.sbgrid.org
       User your_sbgrid_username
       IdentityFile \path\to\your\id_rsa
   ```

2. **Access Resources:**

   Access the resources with a single SSH command, e.g.:

   ```bash
   ssh tkl1_p
   ```

### Example: Using CARE Off-site

To run CARE off-site, follow these steps:

1. **Open a Connection:**

   SSH into `tkl1` or `tkl3` via `xtal200`:

   ```bash
   ssh tkl1_p
   ```

2. **Activate Conda Environment:**

   Activate the CARE environment:

   ```bash
   conda activate care
   ```

3. **Start Jupyter Notebook:**

   Start a Jupyter notebook on a specific port (e.g., 1234):

   ```bash
   jupyter notebook --no-browser --port 1234
   ```

   Copy the generated link.

4. **Set Up SSH Tunneling:**

   Open a new terminal on your local machine and run:

   ```bash
   ssh -NL 1234:localhost:1234 tkl1_p
   ```

   Keep this terminal open.

5. **Access Jupyter Notebook:**

   Paste the copied link into your local web browser to access the Jupyter notebook running on the remote machine.

---
