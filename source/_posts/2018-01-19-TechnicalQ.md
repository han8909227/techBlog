---
layout: blog
title: Conceptual Questions
date: 2018-01-19 17:15:38
tags:
- interview
- cs
- faq
categories:
- Technical interview prep
---

# Difference between the kernal and the OS and the BIOS?
## Kernal
The kernal is part of the operating system and closer to the hardware,
it runs in the privileged mode and providing low level services like:
- memory management
- process management
- system calls

## BIOS
The Basic Input-Output System(BIOS), is responsible to provide drivers for
new devices to OS. BIOS code is stored in read-only memory (ROM) and some
non-volatile RAM. BIOS has 3 main functionality:
- Power on self test(POST), leads to the booting program
- Load and transfer control to boot program
- Provide drivers for all devices

## OS
The operating system(OS), which includes the kernal and BIOS would also has
other applications like the user interface(i.e shell, gui, etc)
<!--more-->

***
# What is virtual memory, paging, and thrashing?
## Virtual Memory
Virtual memory is a technique used in computer to manage physical memories such
as RAM and hard-drive to optimize the utlilization of the memory.
The way it works is by mapping memory addresses used by a program, called virtual
addresses, into physical addresses in computer memory. This memmory space is seemed
by a process as a **contiguous address space** or one segment. So the OS is responsible
to translate physical to virtual address, and part of the CPU called MMU(memory management
unit) translates virtual to physical addresses.

### Advantage of virtual memory
The primary advantage of using virtual memory is the ability to free applications from
havnig to manage a shared memory space, increased security due to memory isolation.

## Paging
Nearly all virtual memory implmentation utlizes technique called paging,
which retrives data from secondary memory(usually RAM) to use for primary
physical memory(usually disk), each retrived storage unit is called page.

## Thrasing
Remember we talked about how to OS and CPU needs to translate virtual and memory addresses back
and forth to access and store things in paging? **Thrasing** is when this swapping activity becomes
a marjo consumer of the CPU time, meaning fewer CPU time is left to run the actual program.
This can be prevented by
- running fewer program
- write program to utilize memory more effectively
- add more RAM to the system
- increase the page size(remember each page is a defined size)

***
*Hope you find these questions helpful! I will be keep writing similar blogs to help me and you
to succeed in technical interviews!*