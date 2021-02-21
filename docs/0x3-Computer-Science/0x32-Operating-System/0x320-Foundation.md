# 0x320 Foundation

- [1. CPU Virtualization](#1-cpu-virtualization)
    - [1.1. Scheduling](#11-scheduling)
        - [1.1.1. Multi-level Feedback Queue](#111-multi-level-feedback-queue)
    - [Threads](#threads)
        - [Kernel-level Threads](#kernel-level-threads)
        - [User-level Threads](#user-level-threads)
- [2. Memory Virtualization](#2-memory-virtualization)
    - [2.1. Segmentation](#21-segmentation)
    - [2.2. Paging](#22-paging)
- [3. Concurrency](#3-concurrency)
    - [3.1. Hardware Primitives](#31-hardware-primitives)
    - [3.2. Lock](#32-lock)
    - [3.3. Concurrent Data Structure](#33-concurrent-data-structure)
    - [3.4. Condition Variable](#34-condition-variable)
    - [3.5. Semaphore](#35-semaphore)
- [4. File Systems](#4-file-systems)
    - [4.1. Basic](#41-basic)
    - [4.2. Inode](#42-inode)
- [5. Reference](#5-reference)

## 1. CPU Virtualization

**Limited Direct Execution** To have a better performance, it is desirable that each process should run on CPU directly, which raises the question of how to enable OS to regain control of CPU when the process is running on CPU. It turns out there are two ways to solve this question.

**cooperative multitasking**
This assumes that each process behaves reasonably and would give control back to CPU frequently. Two approach allows the transfer of control

normal system call: syscall of course would transfer control to kernel
yield system call: there is a yield system call which do nothing but to transfer control
Some early version of OS (e.g: Mac OS 9) applies the approach, but is not a good idea in general, for example, the case of inf loop

**timer interrupt**
Another way is to use timer's interrupt. The timer would raise interrupt at the scale of milliseconds. Kernel can implement the interrupt handler to manage processes. 

### 1.1. Scheduling
The most basic scheduling approaches assumes that run-time of each job is known. Then there are two groups of approaches. 

The first group minimizes the turnaround time, which is the average time of completion time minus arrival time

- **Shortest Job First (SJF)**: literally run the shortest job first
- **Shortest Time-To-Completion First (STCF)**: SJF might run a heavy job when it is the only job. In a preemptive OS, it should reschedule jobs based on their remaining workload.
  
The second group targets the **response time**, which is defined as the time taken to response after the arrival

- **round robin (RR)**: schedule jobs in a for loop for a time slice. The time slice should not be too short (because context switch has non-trivial cost)
There is a trade-off between these two groups. Additionally, the assumption of run-time of each job is unrealistic. In the real word, following schedulers are commonly used.

#### 1.1.1. Multi-level Feedback Queue
There are multiple queues corresponding to different priorities of jobs. It runs with the following rules

- The queue with higher priority run its internal jobs with round-robin
- When a new job arrives, it is put into the highest priority queue
- When a job consumes its time allotment, its priority is reduced
- After some period, all jobs will move up to the top priority (priority boost)


This scheduler can both reduce response time (by putting interactive jobs in the higher priority queue) and alleviate the starvation issue (by the priority boost)

Schedulers can be given hints about priority (e.g: nice command)

Many real worlds OS use this family of scheduler (e.g: Solaris, BSD family, Windows NT family...).

### Threads
#### Kernel-level Threads
#### User-level Threads
The threads implemented by users, OS does not recognize user-level threads.
- Advantages are less context switch time.
- Disadvantages are the blocking operations (e.g: IO), 1 user-thread IO will block the entire process, therefore blocking all users-threads

In general, user-level threads can be implemented using one of four models.
- Many-to-one
- One-to-one
- Many-to-many
- Two-level


## 2. Memory Virtualization
### 2.1. Segmentation
### 2.2. Paging

## 3. Concurrency
Race condition happens when multiple threads enter the critical section at roughly the same time and attempt to modify the shared data. This happens because the update method are usually executed atomically. For instance, the increment operation in x86 usually take three instruction: move memory to register, update register, move back to memory. To prevent those issues, we can build a set of synchronization primitives.

### 3.1. Hardware Primitives
There are a couple of hardware primitives to support concurrency feature

**Test-and-Set (atomic exchange)**: swap a *ptr and immediate value atomically (x86: xchg)

**Compare-and-Set**: compare *ptr with a value, if equal, then set an immediate value. This is the most popular synchronization primitive. (x86: CMPXCHG)

**Load-Link/Store-Conditional (LL/SC)**: load *ptr and store an immediate value to it if no other threads load-link it before. (e.g: RISC-V: lr/sc,  ARM: ldxr/stxr, MIPS: ll/sc...)

**Fetch-and-Add (atomic adder)**: increment a *ptr atomically

### 3.2. Lock
Lock is a mutual exclusion primitive. 

Previous primitives can be used to implement the simple spinlocks, which typically suffer from the performance issue as waiting threads waste the timeslice assigned to them. There are a couple of solutions to this issue:

- yield to deschedule itself instead of spin during waiting 
- put itself into a queue and sleep (park), when the resource is unlocked, this thread is waked up (unpark)

### 3.3. Concurrent Data Structure
Lock based concurrent data structure looks interesting. The most simple approach is to have a big lock on the entire data structure, which has the performance issue. A better approach is to have multiple locks locking parts of the data structure. For example

**Concurrent counter**: An interesting approach is an approximate counter which   maintains a global counter and multiple local counters and corresponding locks on each core, each thread is updating its core's counter and sometimes the local counter propagate its value to the global counter
**Concurrent list**: hand-over-hand locking approach prepares each node a lock, when processing the list, unlock the previous one and lock current one.
Concurrent queue: One implementation is to put a lock on the first and last element respectively. To keep the first and last to be different, always insert a tmp element.
**Concurrent hash**: maintain multiple buckets which have different locks.

### 3.4. Condition Variable
Condition Variable is an ordering primitive.

Condition Variable is an efficient way to send notification among threads. The notification feature itself can be easily implemented with spin, which is not efficient of course.

Condition variable has two interfaces

- wait: put the thread into sleep until the condition changed. need to grab a lock when calling wait. It will wait until condition AND mutex become available. lock is to protect the predicate state.
- signal: wake a sleeping thread waiting this condition. do nothing if no one is waiting. If more than one thread is blocked on a condition variable, the scheduling policy shall determine the order in which threads are unblocked
A simple rule with condition variables is to always use while to check condition instead of if, because condition might change when waiting thread start running. (Mesa semantics)

**Producer/Consumer Problem**
This is a synchronization problem in which producer generate items into buffers and consumers take out items. It is seen in many places (multithread server, shell pipe...)

### 3.5. Semaphore
Semaphore was originally introduced by Dijkstra as a single primitive for all things related to synchronization. Actually, semaphore can be used to implement both locks and condition variables.

It is an object with an integer value that we can modify. In the POSIX standard, it has following interfaces:

- **sem_wait (P)**: decrement the value, go to sleep if it is negative
- **sem_post (V)**: increment the value, wake one if there is a sleeping thread
  
The value of the semaphore, when negative, is equal to the number of waiting threads

## 4. File Systems
### 4.1. Basic
Overview of major file systems

**Disk FS**
- UNIX: FS, FFS
- Linux: ext2, ext3, ext4
- Windows: FAT12,16,32, exFAT, NTFS
- Apple: HFS, HFS+, APFS
- Other: ZFS, XFS
  
**NAS**: AFS, HDFS (Hadoop), GFS

**Special**: tmpfs, procfs...

The minimum element of disk available (from the OS perspective, it might be 512 byte sector from the physical view) is called block, which is usually 4KB (which is also the reason why empty dir size is 4KB)

**Superblock**
contains the metadata of the disk and file system. In Linux, we can use the command dumpe2fs to see metadata details stored in the superblock. It contains information such as total inode count and total block count.

### 4.2. Inode
Inode is the on-disk structures of a file system to store the metadata of files in *nix. Note that Windows file systems do not have inode, they store metadata in the directory data structure (directory entry).

Size of inode is usually 256 bytes.

How to manage large file block pointers ?

multi-level index: store a limited number of direct block in inode and have indirect pointer to another block storing pointers. This is used in ext2,3
extents: store the start and end block for a contiguous ranges. This is used in ext4 and XFS.

## 5. Reference
[1] Operating Systems: Three Easy Pieces

