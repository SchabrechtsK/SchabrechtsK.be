---
title: How to solve the install error of Virtualbox on Ubuntu 16.04
author: Kenneth Schabrechts
type: post
date: 2016-12-04T00:00:00+00:00
url: /development/how-to-solve-the-install-error-of-virtualbox-on-ubuntu/
categories:
  - Development
tags: ['Development', 'Tools', 'VirtualBox', 'OSS']
summary: 'I recently changed from Mac to Linux. But my machine gave an install error on VirtualBox. This post will explain how I fixed it.'

---
As most programmers I prefer to program on my local machine. To this end I use Virtualbox in combination with Vagrant.  
A few months back I changed from a Mac to a Linux machine and I decided to use Ubuntu 16.04 at the time.

After installing all my tool I ran my vagrant box to start working on a project. But as quick as vagrant box started it halted and I got an installation error.  
According to the system my Virtual box installation was incomplete.  
Some closer investigation showed that `vboxdrv` was not loaded.

Research pointed out out that since Kernel version 4.4.0–20 there was a signifanct change. **Unsigned** kernel modules were no longer allowed to run with **Secure Boot** enabled.  
So the next logical step is to sign the modules that Virtual box uses.

The `vboxdrv` is not the only module you need to sign. You also need to sign the following modules: `vboxnetflt`, `vboxnetadp`, and `vboxpci`.

After signing all the modules you need to do step 4 and reboot. After the reboot you can enroll the MOK keys. For a visual guide you of the enrollment you can see here: [SecureBoot Graph](https://sourceware.org/systemtap/wiki/SecureBoot "SecureBoot Graph").

For more information about signing modules I suggest you go read [here](https://github.com/Canonical-kernel/Ubuntu-kernel/blob/master/Documentation/module-signing.txt "Module Signing Homepage").

After following these steps your Virtual Box should be good to go.  
Happy developing!