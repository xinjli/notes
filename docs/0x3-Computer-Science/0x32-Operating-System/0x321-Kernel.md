# 0x321 Kernel

This page describes the implementation and design of the kernel (mostly Linux). And this page might be divided into several pages in the future.

![OS](../../img/Unix_history-simple.png)

## Overview
This subsection is a note summarizing history and principles for different kernels.

### Concepts
[UNIX Philosophy](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)
[Tanenbaum–Torvalds debate (microkernel VS monolithic)](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate)

### UNIX like
UNIX
UNIX was first developed in 1969 by Ken Thompson at Bell Labs on PDP-7 with assembly language.

- [UNIX Philosophy](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)
- The UNIX System: Making Computers More Productive
  
#### BSD
#### System V
#### OSX
#### Minix
#### Linux

### Windows
#### Windows NT

### New Kernels
#### GNU Hurd
#### Zircon
new micro-kernel under development derived from Haiku
[syscalls](https://fuchsia.dev/fuchsia-src/reference/syscalls) looks clean

## Process Manangement
### Process Scheduler
#### O(n) Scheduler
#### O(1) Scheduler
#### Completely Fair Scheduler

## Memory Management
### Virtual Memory
There are three types of memory kernel is handling. 

- **logical address**: used in the instruction set, consists of segment + offset. This address is visible in user space.
- **linear address (virtual address)**:  the address translated from logical address by segmentation unit
- **phyiscal address**: actual address in the memory cell, translated from linear address by paging unit.
Kernel is responsible to setup segmentation and paging to perform virtual memory translation. (Actual translation is done by MMU and TLB). Although segmentation looks not enabled in current Desktop OS, because segment registers (cs, ds, ss(stack segment)...) are always set to 0.

Kernel in real mode and protected mode handles two translation differently.  By the way, protected mode is controlled by PE bit on CR0 register in x86.

#### Segmentation translation
real-mode: translation rule is segment address * 16 + offset (20bit). The entire memory space is 1MB (20bit), each segment memory space is 64KB.

protected mode: segment register stores segment selector instead of address. Segment selector is used to select segment descriptor on GDT (global descriptor table), linear address and size of the segment are retrieved from segment descriptor. 
#### Paging translation

### Pages
#### Zones
#### Allocation
- kmalloc/kfree
- vmalloc

## Synchronization
Synchronization Implementation is usually hardware dependent, it can also implemented with software taking advantage of sharing memory (e.g: Peterson's algorithm)

### Busy Waiting
Busy waiting is usually not considered a good strategy because it is wasting CPU time. Another problem with it is priority inversion problem, which high priority process depends on resource acquired by low priority process.

- spinlock: hardware implementation. It can be implemented with test-and-set instruction (e.g.: xchg)
- disable interrupts: crazy...
- Peterson: software implementation. use shared memory to implement busy waiting

### Semaphore
Semaphore is to force precedence relationship $signal(s)_i <= wait(s)_{i+K}$

**wait(semaphore s)**: stall current process if $s<=0$, otherwise decrement s
**signal(semaphore)**: increment s

Producer Consumer Problem
producer wait space, and signal something
consumer wait something and signal space

### Mutex
Mutual Exclusion. Protection of critical section. It can be implemented with semaphore with $k=1$

### Atomic
It has interfaces such as read, increment, decrement to modify an int. Those are implemented by LOCK prefix in x86 and strex/ldrex monitor in arm.

## Interrupt
Interrupts can be viewed as a mean of communication between the CPU and the OS kernel. They may be initiated by the CPU (exceptions - e.g.: divide by zero, page fault), devices (hardware interrupts - e.g: input available), or by a CPU instruction (traps - e.g: syscalls, breakpoints). They are eventually managed by the CPU, which "interrupts" the current task, and invokes an OS-kernel provided ISR/interrupt handle.

### Real/Protected
#### Real mode
routines are stored from linear address 0 to 400H (first 1k byte in memory)
interrupt vector is mapped to routine address by multiplying 4.
#### Protected Mode
interrupt descriptor table's starting address contained in IDT (setup by lidt assembly)
### Exception (Internal Interrupt)
#### Trap
traditional Linux system call entry point was INT 0x80, replaced with sysenter on x86

#### Fault
#### Abort
### Interrupt (Async Interrupt)
#### Maskable Interrupt
#### Nonmaskable Interrupt

## Virtualization
### cgroups

## Kernel API
### memory management
copy_from_user: may block due to page fault
copy_to_user


## Reference
[1] Understanding the Linux Kernel, Third Edition, which covers Linux kernel 2.6. In addition, I will also [2] the dinosaur book
[3] the MINIX book
[4] Windows Internals
[5] Lions' Commentary on UNIX.