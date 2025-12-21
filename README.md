# Delique
A free and open-source GNU/Linux distribution derived from the procedures in the Linux From Scratch book, aimed at efficiency, valuable features, with very strict regulations put in place regarding performance and usability for low-end devices, as well integration with the NsCDE desktop environment paired with some application akin to the program manager from Windows NT 3.x  to be designed for this project specifically with other necessary features supplied by other free and open-source projects or by programs that may or may not need to be written specifically for the Delique operating system itself.

Delique is in rather early stages of development, and must be regarded as experimental until further notice. Do not expect much of a complete operating system over the next few months. Additionally, Delique is not only a product of the Linux From Scratch book and has already begun to deviate from its procedures where necessary. 

As a conservative estimate, the Delique operating system should be in a state where it is fully functional and integrated with the NsCDE desktop environment by at least early 2026.

You are now aware of the state of the Delique operating system.

---
**Build and install instructions**

Before proceeding, you should obtain the Linux From Scratch books (in particular, the LFS systemd and BLFS systemd books which this is based off of) and familiarize yourself with them. They are available at _www.linuxfromscratch.org_ and are completely free and open-source. Much credit goes to these books from which the Delique operating system shall be derived from.

The source code is freely available under their respective licenses, and can be downloaded by two means: by downloading the archive of the Delique operating system itself, which at this time still contains the source code in the _/sources_ directory and/or the _/usr/src_ directory and following the procedures from the corresponding Linux From Scratch books and deviating where instructed (if you only want to build and install a specific program here), _**or**_ download the source code using wget and the /sources/wget-list-systemd file from this repository and yet again use the procedures from the corresponding Linux From Scratch books and deviating where instructed (if you want to build the entire Delique operating system). 

There is no installer or bootable .ISO file provided yet, and if you _really_ wish to boot Delique and use it you will have to: install the archived version manually to an ext3 partition, setup a separate _/boot_ partition, copy the files in the _/boot_ directory of this repository (note that the /boot/grub directory only contains a menu.lst file with options setup pertaining to GRUB-Legacy 0.97, and does not need to be copied over if you will be configuring any other bootloader), and manually configure your bootloader to boot the Delique operating system with this setup. If you know how to do this, you should be able to install and use the Delique operating system in its current state. After this process it should be ready to use.

The deviations from the Linux From Scratch books so far include:

  - Delique having its own release file(s), thus it identifies itself as well... Delique.
  
  - In _/etc/resolv.conf_, the Cloudflare, Google, and Quad9 nameservers are configured for IPv4 as well IPv6 by default.
  
  - The contents of /lib64 are actually symbolic links to the /lib folder circa Chapter 7 of the Linux From Scratch book; this may be a part of our problems, howver this has actually been found _necessary_ to exist despite the directives of the Linux From Scratch books to always ensure /lib64 does not exist. In particular, _ld-linux-x86-64.so.2_, _ld-lsb-x86-64.so.3_, and _ld-lsb.so.3_ need to be symlinked here from /lib or many programs will refuse to compile at all.

  - GRUB-Legacy 0.97 (along with several community patches for it) is included with the source code alongside the modern version of GRUB 2. While GRUB 2 is installed with the Delique operating system as of now, it is untested, and will be replaced with GRUB-Legacy 0.97 as soon as possible. 

  - systemd and the dbus-daemon are not installed correctly due to a bug potentially not specified in the Linux From Scratch books; for some reason, while following the procedures in the Linux From Scratch books, when compiling systemd it does not compile a few libraries necessary for it to integrate with the dbus-daemon when that is compiled as well. Until a fix is found for this, a few utilities that will never work in this configuration (timedatectl, hostnamectl, loginctl, localectl, machinectl, busctl, networkctl, resolvectl) have been renamed and replacements put in place that are actually shell scripts that simply print to the console indicating that the program attempting to be run has been disabled (with a message that reads along the lines of "<program> disabled; use other utility" with <program> being the name of the program you are trying to run that was intentionally disabled). The dbus-daemon still runs, but it is run manually and is not integrated with systemd. This has not proven itself to be a catastrophic problem thus far as X11, NsCDE, and related components do not depend on the dbus-daemon being integrated with systemd, however it should hopefully be resolved at some time in the future. This is the extent of my knowledge on that issue, and if anyone has a fix for it please let me know.

This is how Delique has derived from the Linux From Scratch books so far, however as you know far more is planned for the future and is actively being worked on. 
