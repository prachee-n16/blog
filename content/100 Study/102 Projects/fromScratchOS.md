---
title: A completely from scratch hobby OS
---
Resources:
- https://wiki.osdev.org/Main_Page
- http://www.lowlevel.eu/wiki/Hauptseite

**Overview**
The main board of a computer is connected to hard drive + CPU. The CPU will have several registers, with a Stack Pointer and Instruction Pointer.

When we start our computer, the main board will take data from the BIOS. It will have some assembler code, copying firmware from BIOS to RAM. It then tells the processor to put it into the beginning of firmware in RAM (CPU will execute BIOS firmware). 
- Bootloader: **responsible for bringing up the kernel on a device**, but not something that will be done right now. Will be read by CPU after BIOS. 
	- Bootloader knows about file system and partition tables: /boot/grub/grub.cfg. This file will find list of installed kernels in an array ordered by sequence of installation
	- /boot/kernel-bin: Will load a file from hard drive (kernel bin) into RAM. CPU executes this next and now OS comes to play!!

The two files we write:
- loader.s (will compile to write a loader.o)
- kernel.cpp (will compile to kernel.o)
These are two different programming languages that will need to be compiled into file. ld, a linker will give us the kernel.bin
- The bootloader will not see this as kernel.bin if there's not a **magic number** present within it

The CPU will start out in a 32-bit mode, and then switches to 64-bit. All the files we build will start off in a 32-bit mode. 

**Multi-boot structure**
- Size of RAM is stored in here, if the boot loader gives us this feature, we should use this
	- Boot loader will make this structure, store it in AX register and also copy this magic number into BX register

printf, usually used to print out text onto the screen won't work because we are outside an OS (in fact, that's the goal of this project).
- Usually, we operate under linux OS, and call this library using dynamic linking. 