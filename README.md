# Delique
A free and open-source GNU/Linux distribution derived from the procedures in the Linux From Scratch book, intending for a very conservative Linux system with special attention for efficiency, valuable features, with very strict regulations put in place regarding performance and usability for low-end devices, as well integration with the NsCDE desktop environment paired with an application manager to be designed for this project specifically with other necessary features supplied by other free and open-source projects or by programs that may or may not need to be written specifically for the Delique operating system itself.

Delique is in rather early stages of development, and must be regarded as experimental until further notice. In other words, do not expect much of a complete operating system for the next few weeks. Additionally, Delique is not only a product of the Linux From Scratch book and has already begun to deviate from its procedures where necessary. 

As a conservative estimate, the Delique operating system should be in a state where it is fully functional and integrated with the NsCDE desktop environment by January 2026.

You are now aware of the state of the Delique operating system.

Datapool Surface
---
The Delique operating system is a part of the Delique project as a whole, which is an initiative to design and manufacture a complete set of computer hardware and software based solely on the unique design principles of efficiency, valuable features, and free and open-source software. The Delique project, as it were, is an ELORG-associated project and is otherwise known by its full name, ELORG-Associated Project Codename "Delique"; for more information about ELORG and what this means, you can visit the [official webpage for the Delique project](https://elektronorgtechnica.ct.ws/Project%20Codename%20'Delique'.html) on ELORG's website.

The directory structure of this repository represents that of the directory structure in the Delique operating system itself, with directories and the files in them created only to reflect changes that deviate from the procedures in Linux From Scratch books that the Delique operating system is derived from and cannot be obtained from said procedures. It should also be noted it was not possible to mirror the entirety of the source code ourselves, but resources necessary to download and obtain it are provided in the _/sources_ directory. 

The complete Delique operating system is released in archive files and released here tagged as "archives". These archives should be entirely reproducible in almost exactness by following the procedures in the Linux From Scratch books to build the sources and deviating when instructed for the sake of Delique. Usually, it should be possible to install and setup Delique manually from these archives in order to use it.

Build and Install
---
Before proceeding, you should obtain the Linux From Scratch books (in particular, the LFS systemd and BLFS systemd books which this is based off of) and familiarize yourself with them. They are available at _www.linuxfromscratch.org_ and are completely free and open-source. Much credit goes to these books from which the Delique operating system shall be derived from.

The source code is freely available under their respective licenses, and can be built and installed by two means: by downloading the archive of the Delique operating system itself, which at this time still contains the source code in the _/sources_ directory and/or the _/usr/src_ directory and can be built by following the procedures from the corresponding Linux From Scratch books and deviating where instructed (optimal if you only want to build and install a specific program here), _**or**_ download the source code using wget and the /sources/wget-list-systemd file from this repository and build it with the procedures from the corresponding Linux From Scratch books and deviating where instructed (optimal if you want to build the entire Delique operating system from scratch... _but at this point, do you? Ha ha..._). 

There is no installer or bootable .ISO file provided yet, and if you _really_ wish to install Delique and use it you will have to install and setup the Delique operating system manually; the instructions to do this are provided with each release. This will not be the case in the near future.

Linux From Scratch Deviations
---
Any deviations from the Linux From Scratch books are reflected in this repository.

The deviations from the Linux From Scratch books so far include:

  - Delique having its own release file(s), thus it identifies itself as well... Delique.
  
  - In _/etc/resolv.conf_, the Cloudflare, Google, and Quad9 nameservers are configured for IPv4 as well IPv6 by default.
  
  - The contents of /lib64 are actually symbolic links to the /lib folder which were created around Chapter 7 in the procedures from the Linux From Scratch book; this may be a part of our problems, however this has actually been found _necessary_ to exist despite the directives of the Linux From Scratch books to always ensure /lib64 does not exist. In particular, _ld-linux-x86-64.so.2_, _ld-lsb-x86-64.so.3_, and _ld-lsb.so.3_ need to be symlinked here from /lib or many programs will refuse to compile and run at all.

  - GRUB-Legacy 0.97 (along with several community patches for it) is included with the source code alongside the modern version of GRUB 2. While GRUB 2 is installed with the Delique operating system as of now, it is untested, and will be replaced with GRUB-Legacy 0.97 as soon as possible. 

  - systemd and the dbus-daemon are not installed correctly due to a bug potentially not specified in the Linux From Scratch books; for some reason, while following the procedures in the Linux From Scratch books, when compiling systemd it does not compile a few libraries necessary for it to integrate with the dbus-daemon when that is compiled as well. Until a fix is found for this, a few utilities that will never work in this configuration (timedatectl, hostnamectl, loginctl, localectl, machinectl, busctl, networkctl, resolvectl) have been renamed and replacements put in place that are actually shell scripts that simply print to the console indicating that the program attempting to be run has been disabled (with a message that reads along the lines of "-program- disabled; use other utility" with -program- being the name of the program you are trying to run that was intentionally disabled). The dbus-daemon still runs, but it is run manually and is not integrated with systemd. This is the extent of my knowledge on that issue, and if anyone has a fix for it please let me know.

This is how Delique has derived from the Linux From Scratch books so far, however as you know far more is planned for the future and is actively being worked on. 
