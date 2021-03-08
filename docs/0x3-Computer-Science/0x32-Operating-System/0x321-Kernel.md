# 0x321 Kernel

- [1. Overview](#1-overview)
    - [1.1. Concepts](#11-concepts)
    - [1.2. UNIX like](#12-unix-like)
        - [1.2.1. BSD](#121-bsd)
        - [1.2.2. System V](#122-system-v)
        - [1.2.3. OSX](#123-osx)
        - [1.2.4. Minix](#124-minix)
        - [1.2.5. Linux](#125-linux)
    - [1.3. Windows](#13-windows)
        - [1.3.1. Windows NT](#131-windows-nt)
    - [1.4. New Kernels](#14-new-kernels)
        - [1.4.1. GNU Hurd](#141-gnu-hurd)
        - [1.4.2. Zircon](#142-zircon)
- [2. Process Manangement](#2-process-manangement)
    - [2.1. Process Scheduler](#21-process-scheduler)
        - [2.1.1. O(n) Scheduler](#211-on-scheduler)
        - [2.1.2. O(1) Scheduler](#212-o1-scheduler)
        - [2.1.3. Completely Fair Scheduler](#213-completely-fair-scheduler)
- [3. Memory Management](#3-memory-management)
    - [3.1. Virtual Memory](#31-virtual-memory)
        - [3.1.1. Segmentation translation](#311-segmentation-translation)
        - [3.1.2. Paging translation](#312-paging-translation)
    - [3.2. Pages](#32-pages)
        - [3.2.1. Zones](#321-zones)
        - [3.2.2. Allocation](#322-allocation)
- [4. Synchronization](#4-synchronization)
    - [4.1. Busy Waiting](#41-busy-waiting)
    - [4.2. Semaphore](#42-semaphore)
    - [4.3. Mutex](#43-mutex)
    - [4.4. Atomic](#44-atomic)
- [5. Interrupt](#5-interrupt)
    - [5.1. Real/Protected](#51-realprotected)
        - [5.1.1. Real mode](#511-real-mode)
        - [5.1.2. Protected Mode](#512-protected-mode)
    - [5.2. Exception (Internal Interrupt)](#52-exception-internal-interrupt)
        - [5.2.1. Trap](#521-trap)
        - [5.2.2. Fault](#522-fault)
        - [5.2.3. Abort](#523-abort)
    - [5.3. Interrupt (Async Interrupt)](#53-interrupt-async-interrupt)
        - [5.3.1. Maskable Interrupt](#531-maskable-interrupt)
        - [5.3.2. Nonmaskable Interrupt](#532-nonmaskable-interrupt)
- [6. Virtualization](#6-virtualization)
    - [6.1. cgroups](#61-cgroups)
- [7. Kernel API](#7-kernel-api)
    - [7.1. memory management](#71-memory-management)
- [8. Reference](#8-reference)

This page describes the implementation and design of the kernel (mostly Linux). And this page might be divided into several pages in the future.

![OS](../../img/Unix_history-simple.png)

## 1. Overview
This subsection is a note summarizing history and principles for different kernels.

### 1.1. Concepts
[UNIX Philosophy](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)
[Tanenbaum–Torvalds debate (microkernel VS monolithic)](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate)

### 1.2. UNIX like
UNIX
UNIX was first developed in 1969 by Ken Thompson at Bell Labs on PDP-7 with assembly language.

- [UNIX Philosophy](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html)
- The UNIX System: Making Computers More Productive
  
#### 1.2.1. BSD
#### 1.2.2. System V
#### 1.2.3. OSX
#### 1.2.4. Minix
#### 1.2.5. Linux

### 1.3. Windows
#### 1.3.1. Windows NT

### 1.4. New Kernels
#### 1.4.1. GNU Hurd
#### 1.4.2. Zircon
new micro-kernel under development derived from Haiku
[syscalls](https://fuchsia.dev/fuchsia-src/reference/syscalls) looks clean

## 2. Process Manangement
### 2.1. Process Scheduler
#### 2.1.1. O(n) Scheduler
#### 2.1.2. O(1) Scheduler
#### 2.1.3. Completely Fair Scheduler

## 3. Memory Management
### 3.1. Virtual Memory
There are three types of memory kernel is handling. 

- **logical address**: used in the instruction set, consists of segment + offset. This address is visible in user space.
- **linear address (virtual address)**:  the address translated from logical address by segmentation unit
- **phyiscal address**: actual address in the memory cell, translated from linear address by paging unit.
Kernel is responsible to setup segmentation and paging to perform virtual memory translation. (Actual translation is done by MMU and TLB). Although segmentation looks not enabled in current Desktop OS, because segment registers (cs, ds, ss(stack segment)...) are always set to 0.

Kernel in real mode and protected mode handles two translation differently.  By the way, protected mode is controlled by PE bit on CR0 register in x86.

#### 3.1.1. Segmentation translation
real-mode: translation rule is segment address * 16 + offset (20bit). The entire memory space is 1MB (20bit), each segment memory space is 64KB.

protected mode: segment register stores segment selector instead of address. Segment selector is used to select segment descriptor on GDT (global descriptor table), linear address and size of the segment are retrieved from segment descriptor. 

#### 3.1.2. Paging translation
On 32-bit arch, the address space is `0x00000000 - 0xffffffff`

- user space range `0x00000000 - 0xbfffffff` 
- kernel space is `0xc0000000 - 0xffffffff`


### 3.2. Pages
#### 3.2.1. Zones
#### 3.2.2. Allocation
- kmalloc/kfree
- vmalloc

## 4. Synchronization
Synchronization Implementation is usually hardware dependent, it can also implemented with software taking advantage of sharing memory (e.g: Peterson's algorithm)

### 4.1. Busy Waiting
Busy waiting is usually not considered a good strategy because it is wasting CPU time. Another problem with it is priority inversion problem, which high priority process depends on resource acquired by low priority process.

- spinlock: hardware implementation. It can be implemented with test-and-set instruction (e.g.: xchg)
- disable interrupts: crazy...
- Peterson: software implementation. use shared memory to implement busy waiting

### 4.2. Semaphore
Semaphore is to force precedence relationship $signal(s)_i <= wait(s)_{i+K}$

**wait(semaphore s)**: stall current process if $s<=0$, otherwise decrement s
**signal(semaphore)**: increment s

Producer Consumer Problem
producer wait space, and signal something
consumer wait something and signal space

### 4.3. Mutex
Mutual Exclusion. Protection of critical section. It can be implemented with semaphore with $k=1$

### 4.4. Atomic
It has interfaces such as read, increment, decrement to modify an int. Those are implemented by LOCK prefix in x86 and strex/ldrex monitor in arm.

## 5. Interrupt
Interrupts can be viewed as a mean of communication between the CPU and the OS kernel. They may be initiated by the CPU (exceptions - e.g.: divide by zero, page fault), devices (hardware interrupts - e.g: input available), or by a CPU instruction (traps - e.g: syscalls, breakpoints). They are eventually managed by the CPU, which "interrupts" the current task, and invokes an OS-kernel provided ISR/interrupt handle.

### 5.1. Real/Protected
#### 5.1.1. Real mode
routines are stored from linear address 0 to 400H (first 1k byte in memory)
interrupt vector is mapped to routine address by multiplying 4.
#### 5.1.2. Protected Mode
interrupt descriptor table's starting address contained in IDT (setup by lidt assembly)
### 5.2. Exception (Internal Interrupt)
#### 5.2.1. Trap
traditional Linux system call entry point was INT 0x80, replaced with sysenter on x86

#### 5.2.2. Fault
#### 5.2.3. Abort
### 5.3. Interrupt (Async Interrupt)
#### 5.3.1. Maskable Interrupt
#### 5.3.2. Nonmaskable Interrupt

## 6. Virtualization
### 6.1. cgroups

## 7. Kernel API
### 7.1. memory management
copy_from_user: may block due to page fault
copy_to_user


## 8. Reference
[1] Understanding the Linux Kernel, Third Edition, which covers Linux kernel 2.6. In addition, I will also [2] the dinosaur book
[3] the MINIX book
[4] Windows Internals
[5] Lions' Commentary on UNIX.