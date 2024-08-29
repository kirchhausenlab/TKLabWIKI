---
title: Remotely Access Machines/Access Compute
type: docs
---

## Access Remote Machines

The TKLAB has 10% of the total compute of Harvard Med with the following severs:

- 3 DGXs equipped with 24 Nvidia A100 GPUs,
- tkl1, tkl2, tkl3, tkl4,
- Datasync folders with terrabytes of capacity
- Scratch folders for developers
- In total having over 800 CPUs and 30 GPUs

To access one of the machines, we have the following:

1. On the Harvard Ethernet Network:
   Run the following commands from your terminal

```bash
ssh username@tkdgx3.med.harvard.edu
>> your password
```

An example would be:

```
❯ ssh ajain@tkdgx3.med.harvard.edu                                                                (base)
(ajain@tkdgx3.med.harvard.edu) Password:
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-190-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu 29 Aug 2024 02:39:04 PM EDT

  System load:  8.5              Processes:             2903
  Usage of /:   5.1% of 1.72TB   Users logged in:       4
  Memory usage: 5%               IPv4 address for eth0: 10.117.38.24
  Swap usage:   0%

Expanded Security Maintenance for Applications is enabled.

96 updates can be applied immediately.
33 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable


*** System restart required ***
Last login: Tue Aug 13 16:50:32 2024 from 10.117.38.196
ajain@tkdgx3:~$
```

2. For a remote machine, please first ssh into xtal200 and have a duo account setup.

```bash
ssh username@xtal200.med.harvard.edu
```

You will be prompted to authenticate yourself on duo before a request for your password. Once done, type the ssh commands as if you would for your local machine

**Example**

```
(ajain@xtal200.harvard.edu) Password:
(ajain@xtal200.harvard.edu) Duo two-factor login for ajain

Enter a passcode or select one of the following options:

 1. Duo Push to XXX-XXX-6117
 2. Phone call to XXX-XXX-6117
 3. SMS passcodes to XXX-XXX-6117 (next code starts with: 1)

Passcode or option (1-3): 1
Success. Logging you in...
Last failed login: Thu Aug 29 14:54:52 EDT 2024 from 10.117.38.251 on ssh:notty
There were 5 failed login attempts since the last successful login.
Last login: Thu Aug  8 10:57:38 2024 from 10.119.223.56
 _______________________________________
/ Welcome to xtal200.harvard.edu ajain. \
\ You have landed on xtal1.             /
 ---------------------------------------
       \   ,__,
        \  (oo)____
           (__)    )\
              ||--|| *
===================================================
 - OS X Software Installer is available for download.
 - Visit our wiki for more information: https://sbgrid.org/wiki/client_install
 - Please support SBGrid by citing the Consortium manuscript:
 - eLife 2013;2:e01456, "Collaboration gets the most out of software".
 - X-ray diffraction datasets should be deposited with SBGrid Data Bank
 - http://data.sbgrid.org/.
===================================================
NOTE:
 - We recommend using ssh keys https://sbgrid.org/corewiki/faq-setting-up-key-based-ssh
 - Remote access FAQ at https://sbgrid.org/corewiki/faqs-remote
 - 2FA SSH ACCESS is coming in October! See https://sbgrid.org/corewiki/duo-ssh-faq
===================================================
   Email help@sbgrid.org for assistance, questions, or feedback.
[ajain@xtal1 ~]$ ssh ajain@tkdgx1.med.harvard.edu
Password:
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-190-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu 29 Aug 2024 02:55:27 PM EDT

  System load:  244.41            Processes:             2802
  Usage of /:   11.2% of 1.72TB   Users logged in:       4
  Memory usage: 75%               IPv4 address for eth0: 10.117.38.22
  Swap usage:   0%

Expanded Security Maintenance for Applications is enabled.

53 updates can be applied immediately.
40 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable


*** System restart required ***
Web console: https://tkdgx1.med.harvard.edu:9090/ or https://10.117.38.22:9090/

Last login: Thu Aug 29 10:55:49 2024 from 10.0.8.2
ajain@tkdgx1:~$
```

3. To Use a remote desktop, please log onto a tklab server remotely (\*\*not the dgxs or xtal200) or locally and run the following command:
   `xdesk.sh`

```
Last login: Mon Aug 19 09:11:40 2024 from 10.117.38.200
ajain@tkl1:~$ xdesk.sh
duplicate session: xpra-desktop
Session already running. - Connect to http://tkl1.med.harvard.edu:8660 with password ***
- ssh -L 9999:tkl1.med.harvard.edu:8660 ajain@xtal200.harvard.edu - leave this running
- Then open a web browser to http://localhost:9999 and fill the password field with ***
For troubleshooting see session with \'tmux a -t xpra-desktop\' then use Ctrl-c to terminate
Or use the command xpra stop
ajain@tkl1:~$
```

Then navigate to the link given (localhost:9999) from above and enter the password to access a desktop remotely

4. Chrome Remote Desktop:
   - Install the Chrome Remote Desktop extension from the Chrome Web Store
   - Follow the instructions to set up the extension
   - Once set up, you can access the remote desktop from the Chrome Remote Desktop app on your local machine

Or from a web browser, navigate to [remotedesktop.google.com](https://remotedesktop.google.com) and sign in with your Google account. You can then access the remote desktop from the web interface.
The email address associated with the Google account must be added to the list of users who can access the remote desktop. Ours is:

```bash
link - https://remotedesktop.google.com/u/4/access?pli=1
tklab@tklab.hms.harvard.edu
```

We also have a PIN and password which can be shared with you upon request.
