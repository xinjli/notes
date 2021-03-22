# 0x321 Kernel

- [1. Process Manangement](#1-process-manangement)
    - [1.1. Process Scheduler](#11-process-scheduler)
        - [1.1.1. O(n) Scheduler](#111-on-scheduler)
        - [1.1.2. O(1) Scheduler](#112-o1-scheduler)
        - [1.1.3. Completely Fair Scheduler](#113-completely-fair-scheduler)
- [2. Memory Management](#2-memory-management)
    - [2.1. Virtual Memory](#21-virtual-memory)
        - [2.1.1. Segmentation translation](#211-segmentation-translation)
        - [2.1.2. Paging translation](#212-paging-translation)
    - [2.2. Pages](#22-pages)
        - [2.2.1. Zones](#221-zones)
        - [2.2.2. Allocation](#222-allocation)
- [3. Synchronization](#3-synchronization)
    - [3.1. Busy Waiting](#31-busy-waiting)
    - [3.2. Semaphore](#32-semaphore)
    - [3.3. Mutex](#33-mutex)
    - [3.4. Atomic](#34-atomic)
- [4. Interrupt](#4-interrupt)
    - [4.1. Real/Protected](#41-realprotected)
        - [4.1.1. Real mode](#411-real-mode)
        - [4.1.2. Protected Mode](#412-protected-mode)
    - [4.2. Exception (Internal Interrupt)](#42-exception-internal-interrupt)
        - [4.2.1. Trap](#421-trap)
        - [4.2.2. Fault](#422-fault)
        - [4.2.3. Abort](#423-abort)
    - [4.3. Interrupt (Async Interrupt)](#43-interrupt-async-interrupt)
        - [4.3.1. Maskable Interrupt](#431-maskable-interrupt)
        - [4.3.2. Nonmaskable Interrupt](#432-nonmaskable-interrupt)
- [5. Virtualization](#5-virtualization)
    - [5.1. cgroups](#51-cgroups)
- [6. Kernel API](#6-kernel-api)
    - [6.1. memory management](#61-memory-management)
- [7. Reference](#7-reference)

This page describes the implementation and design of the kernel (mostly Linux).

## 1. Process Manangement
### 1.1. Process Scheduler
#### 1.1.1. O(n) Scheduler
#### 1.1.2. O(1) Scheduler
#### 1.1.3. Completely Fair Scheduler

## 2. Memory Management
### 2.1. Virtual Memory
There are three types of memory kernel is handling. 

- **logical address**: used in the instruction set, consists of segment + offset. This address is visible in user space.
- **linear address (virtual address)**:  the address translated from logical address by segmentation unit
- **phyiscal address**: actual address in the memory cell, translated from linear address by paging unit.
Kernel is responsible to setup segmentation and paging to perform virtual memory translation. (Actual translation is done by MMU and TLB). Although segmentation looks not enabled in current Desktop OS, because segment registers (cs, ds, ss(stack segment)...) are always set to 0.

Kernel in real mode and protected mode handles two translation differently.  By the way, protected mode is controlled by PE bit on CR0 register in x86.

#### 2.1.1. Segmentation translation
real-mode: translation rule is segment address * 16 + offset (20bit). The entire memory space is 1MB (20bit), each segment memory space is 64KB.

protected mode: segment register stores segment selector instead of address. Segment selector is used to select segment descriptor on GDT (global descriptor table), linear address and size of the segment are retrieved from segment descriptor. 

#### 2.1.2. Paging translation
On 32-bit arch, the address space is `0x00000000 - 0xffffffff`

- user space range `0x00000000 - 0xbfffffff` 
- kernel space is `0xc0000000 - 0xffffffff`


### 2.2. Pages
#### 2.2.1. Zones
#### 2.2.2. Allocation
- kmalloc/kfree
- vmalloc

## 3. Synchronization
Synchronization Implementation is usually hardware dependent, it can also implemented with software taking advantage of sharing memory (e.g: Peterson's algorithm)

### 3.1. Busy Waiting
Busy waiting is usually not considered a good strategy because it is wasting CPU time. Another problem with it is priority inversion problem, which high priority process depends on resource acquired by low priority process.

- spinlock: hardware implementation. It can be implemented with test-and-set instruction (e.g.: xchg)
- disable interrupts: crazy...
- Peterson: software implementation. use shared memory to implement busy waiting

### 3.2. Semaphore
Semaphore is to force precedence relationship $signal(s)_i <= wait(s)_{i+K}$

**wait(semaphore s)**: stall current process if $s<=0$, otherwise decrement s
**signal(semaphore)**: increment s

Producer Consumer Problem
producer wait space, and signal something
consumer wait something and signal space

### 3.3. Mutex
Mutual Exclusion. Protection of critical section. It can be implemented with semaphore with $k=1$

### 3.4. Atomic
It has interfaces such as read, increment, decrement to modify an int. Those are implemented by LOCK prefix in x86 and strex/ldrex monitor in arm.

## 4. Interrupt
Interrupts can be viewed as a mean of communication between the CPU and the OS kernel. They may be initiated by the CPU (exceptions - e.g.: divide by zero, page fault), devices (hardware interrupts - e.g: input available), or by a CPU instruction (traps - e.g: syscalls, breakpoints). They are eventually managed by the CPU, which "interrupts" the current task, and invokes an OS-kernel provided ISR/interrupt handle.

### 4.1. Real/Protected
#### 4.1.1. Real mode
routines are stored from linear address 0 to 400H (first 1k byte in memory)
interrupt vector is mapped to routine address by multiplying 4.
#### 4.1.2. Protected Mode
interrupt descriptor table's starting address contained in IDT (setup by lidt assembly)
### 4.2. Exception (Internal Interrupt)
#### 4.2.1. Trap
traditional Linux system call entry point was INT 0x80, replaced with sysenter on x86

#### 4.2.2. Fault
#### 4.2.3. Abort
### 4.3. Interrupt (Async Interrupt)
#### 4.3.1. Maskable Interrupt
#### 4.3.2. Nonmaskable Interrupt

## 5. Virtualization
### 5.1. cgroups

## 6. Kernel API
### 6.1. memory management
copy_from_user: may block due to page fault
copy_to_user


## 7. Reference
[1] Understanding the Linux Kernel, Third Edition, which covers Linux kernel 2.6. In addition, I will also [2] the dinosaur book
[3] the MINIX book
[4] Windows Internals
[5] Lions' Commentary on UNIX.