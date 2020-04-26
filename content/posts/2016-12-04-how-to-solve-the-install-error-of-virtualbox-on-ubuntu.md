---
title: How to solve the install error of Virtualbox on Ubuntu 16.04
author: Kenneth
type: post
date: 2016-12-04T00:00:00+00:00
url: /development/how-to-solve-the-install-error-of-virtualbox-on-ubuntu/
featured_image: /wp-content/uploads/2016/12/1lRxHIeTWmlSvXWJtNC-EwQ.jpeg
categories:
  - Development

---
<p id="1499" class="graf graf--p graf-after--figure">
  As most programmers I prefer to program on my local machine. To this end I use Virtualbox in combination with Vagrant.<br /> A few months back I changed from a Mac to a Linux machine and I decided to use Ubuntu 16.04 at the time.
</p>

<p id="ec82" class="graf graf--p graf-after--p">
  After installing all my tool I ran my vagrant box to start working on a project. But as quick as vagrant box started it halted and I got an installation error.<br /> According to the system my Virtual box installation was incomplete.<br /> Some closer investigation showed that <code class="markup--code markup--p-code">vboxdrv</code> was not loaded.
</p>

<p id="8366" class="graf graf--p graf-after--p">
  Research pointed out out that since Kernel version 4.4.0–20 there was a signifanct change. <strong class="markup--strong markup--p-strong">Unsigned</strong> kernel modules were no longer allowed to run with <strong class="markup--strong markup--p-strong">Secure Boot</strong> enabled.<br /> So the next logical step is to sign the modules that Virtual box uses.
</p>

<p id="708c" class="graf graf--p graf-after--figure">
  The <code class="markup--code markup--p-code">vboxdrv</code> is not the only module you need to sign. You also need to sign the following modules: <code class="markup--code markup--p-code">vboxnetflt</code>, <code class="markup--code markup--p-code">vboxnetadp</code>, and <code class="markup--code markup--p-code">vboxpci.</code>
</p>

<p id="b168" class="graf graf--p graf-after--p">
  After signing all the modules you need to do step 4 and reboot. After the reboot you can enroll the MOK keys. For a visual guide you of the enrollment you can see here: <a class="markup--anchor markup--p-anchor" href="https://sourceware.org/systemtap/wiki/SecureBoot" target="_blank" rel="nofollow noopener noreferrer" data-href="https://sourceware.org/systemtap/wiki/SecureBoot">https://sourceware.org/systemtap/wiki/SecureBoot</a>.
</p>

<p id="3bd4" class="graf graf--p graf-after--p">
  For more information about signing modules I suggest you go read <a class="markup--anchor markup--p-anchor" href="https://github.com/Canonical-kernel/Ubuntu-kernel/blob/master/Documentation/module-signing.txt" target="_blank" rel="nofollow noopener noreferrer" data-href="https://github.com/Canonical-kernel/Ubuntu-kernel/blob/master/Documentation/module-signing.txt">https://github.com/Canonical-kernel/Ubuntu-kernel/blob/master/Documentation/module-signing.txt</a>
</p>

<p id="a45f" class="graf graf--p graf-after--p graf--trailing">
  After following these steps your Virtual Box should be good to go.<br /> Happy developing!
</p>