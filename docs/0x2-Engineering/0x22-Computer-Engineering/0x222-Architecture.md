# 0x222 Architecture

- [1. History](#1-history)
    - [1.1. 1950 - 1960](#11-1950---1960)
    - [1.2. 1960 - 1970 (3rd Generation: IC)](#12-1960---1970-3rd-generation-ic)
    - [1.3. 1970 - 1980 (4th Gen: microprocessor 10 micro - 1 micro)](#13-1970---1980-4th-gen-microprocessor-10-micro---1-micro)
    - [1.4. 2000 - 2010 (50nm - 100 nm)](#14-2000---2010-50nm---100-nm)
    - [1.5. 2010 - Now (10nm -50 nm)](#15-2010---now-10nm--50-nm)
- [2. Basic](#2-basic)
- [3. DEC family](#3-dec-family)
    - [3.1. PDP](#31-pdp)
    - [3.2. VAX](#32-vax)
    - [3.3. Alpha](#33-alpha)
- [4. Intel family](#4-intel-family)
        - [4.0.1. History](#401-history)
        - [4.0.2. General Purpose Register](#402-general-purpose-register)
        - [4.0.3. Segmentation Register](#403-segmentation-register)
        - [4.0.4. Control Register](#404-control-register)
        - [4.0.5. SIMD Register](#405-simd-register)
        - [4.0.6. Arithmetic Instruction](#406-arithmetic-instruction)
        - [4.0.7. SIMD Instruction](#407-simd-instruction)
        - [4.0.8. System call](#408-system-call)
- [5. MIPS](#5-mips)
- [6. ARM family](#6-arm-family)
    - [6.1. License](#61-license)
    - [6.2. A32 Architecture](#62-a32-architecture)
        - [6.2.1. A32 Registers](#621-a32-registers)
        - [6.2.2. A32 Assembly](#622-a32-assembly)
        - [6.2.3. Thumb Assembly](#623-thumb-assembly)
    - [6.3. A64 Architecture](#63-a64-architecture)
        - [6.3.1. A64 Registers](#631-a64-registers)
        - [6.3.2. A64 Assembly](#632-a64-assembly)
- [7. RISC-V](#7-risc-v)
- [8. Nvidia family](#8-nvidia-family)
- [9. Reference](#9-reference)

Computer Architecture (or ISA) is an abstract interface between the hardware and the lowest level software.

## 1. History

This section is my summary of processors' history from 1950.

### 1.1. 1950 - 1960

Traitorous eight left Shockley's lab on 1957, found Fairchild semiconductor

1957 development of planar process by Jean Hoerni. 1958, invention of IC (hybrid IC on germanium) by Jack Kilby (Texas Instrument), improved (monolithic IC on silcon) by Robert Noyce (Fairchild).

### 1.2. 1960 - 1970 (3rd Generation: IC)

1968, Noyce, Gordon left Fairchild and found Intel

### 1.3. 1970 - 1980 (4th Gen: microprocessor 10 micro - 1 micro)

### 1.4. 2000 - 2010 (50nm - 100 nm)

Intel released <g class="gr_ gr_9 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar only-ins replaceWithoutSep" id="9" data-gr-id="9">Pentium</g> 4 series, whose strategy then was to improve clock frequency in a single core, which causes much higher power consumption and heat due to leakage. On the other hand, AMD introduced Athlon 64 to shift to 64 bit and focused on efficiency in each clock cycle successfully. To compete with AMD, Intel switched to Core 2 series whose sales was better than AMD Phenom series. (Interestingly, AMD stock price dropped significantly after Core 2 release)

### 1.5. 2010 - Now (10nm -50 nm)

Intel Core series <g class="gr_ gr_116 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar only-ins replaceWithoutSep" id="116" data-gr-id="116">started</g> tick-tock strategy to improve the manufacturing process and microarchitecture alternatively each year until Skylake. (Nehalem/Westmere, Sandy Bridge/Ivy Bridge, Haswell/Broadwell, Skylake)

AMD acquired ATI in 2006 and improved its graphic performance. On GPU side, AMD Radeon 4000 compete with NVIDIA Geforce 200 successfully, but on CPU side, AMD announced Bulldozer (FX series) to compete with Intel Core series. The CPU side was not successful until Zen series.

## 2. Basic

**Instruction Processing Style**

*   0-address: stack machine (op, push A, pop A)
*   1-address: accumulator machine (op ACC, ld A, st A)
*   2-address: 2-operand machine (op S,D; one is both source and dest)
*   3-address: 3-operand machine (op S1, S2, D; source and dest separate)

Stack machine

Advantages are the small instruction size and efficient procedure calls (all params are on stack so no additional cycles for parameter passing)

Downsides are computations that are not easily expressible with postfix notation are difficult to map to stack machines

Not that stack machine is a class of pushdown automaton, therefore not Turing complete. If it has two stacks, It is equivalent to Turing machine.

**Data Types**

Representation of information for which there are instructions that operator on the representation

Example: integer (two endians), float point, char, binary . Some rare examples are queue, doubly linked lists, and even objected oriented (intel 432) !

**Memory Organization**

Address space: How many uniquely identifiable locations in memory

Addressability: how much data does each uniquely identifiable location store

*   bit addressable: Burroughs B1700 (purpose of this was to virtualize ISA)
*   byte-addressable: most ISA
*   64-bit addressable: some supercomputer
*   32-bit addressable: first Alpha

Support for virtual memory

**Registers More vs Less**

benefit or more registers: enable better register allocation by compiler

benefit of fewer registers: save number of bits for encoding register address, small register file.

**Addressing Mode**

Addressing modes specify how to obtain the operands

*   **Absolute**: use the immediate value as address (e.g: LW rt, 10000)
*   **Register Indirect**: use GRP[r_base] as address (e.g: LW rt, (r_base)
*   **Displaced or based**: use offset + GPR[r_base] as address (LW rt, offset(r_base))
*   **Indexed use**: GPR[r_base] + GPR[r_index] as address (LW rt, (r_base, r_index))
*   **Memory Indirect**: use value at M[GPR[r_base]] as address (LW rt((r_base))
*   **Auto inc/decrement**: use GRP[r_base] as address but inc or dec (LW rt, (r_base))

More addressing modes

*   The good point is that it enables better mapping of high-level constructs to the machine such as array, pointer-based accesses. (e.g: array access can be implemented with auto inc).
*   The downside is hard to design and too many choices for compiler.

**RISC vs CISC**

*   RISC: simple instruction, fixed length, uniform decode, few addressing mode
*   CISC: complex instructions, variable length, non-uniform decode, many addressing mode

## 3. DEC family

### 3.1. PDP

### 3.2. VAX

### 3.3. Alpha

## 4. Intel family

Reference: [Intel Manual](https://software.intel.com/en-us/articles/intel-sdm)

#### 4.0.1. History

*   4004(4bit)
*   8080(8bit)
*   8086(16bit)
*   386(32bit)
*   486
*   pentium
*   intel64(64bit)

#### 4.0.2. General Purpose Register

*   rax, rbx, rcx, rdx ... r8 ... r15

#### 4.0.3. Segmentation Register

I found that they are rarely used in recent desktop OS because segmentation has been replaced by paging, <g class="gr_ gr_3 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="3" data-gr-id="3">windbg</g> and <g class="gr_ gr_4 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="4" data-gr-id="4">lldb</g> shows that those registers are constantly zeros on Windows 10 and Linux 4.1

*   cs, ds ...
*   cs: code
*   ds: data
*   es: extra
*   fs: general purpose
*   gs: general purpose
*   ss: stack segment

#### 4.0.4. Control Register

**CR0**

*   PE (0 bit): protected mode enabled
*   PG (31 bit): paging unit (CR3) enabled

**CR3**

*   page table based register

#### 4.0.5. SIMD Register

*   xmm0 ... xmm7 (each has 128bit for SSE)

#### 4.0.6. Arithmetic Instruction

*   expensive arithmetic instruction such as multiply and division are only available at rax

#### 4.0.7. SIMD Instruction

*   MMX, SSE, SSE2, SSE, AVX, AVX512

#### 4.0.8. System call

*   sysenter: fast level 3 to level 0 rountine. stack need to store some registers before entry

## 5. MIPS

Instruction Format

R-type

I-type

J-type

## 6. ARM family

### 6.1. License

Arm's license looks interesting. Basically it runs two types of license

*   Architecture license just license their ISA
*   Cortex license is about their microarchitecture and of course ISA

### 6.2. A32 Architecture

ARMv3 -> .... -> ARMv7 -> ARMv8 (support for 64bit)

Current processors are named in the format of Cortex-(A|R|M)[0-9]+ where A is for server, R for realtime system, M denotes microcontroller.

#### 6.2.1. A32 Registers

*   R0 - R12: general purpose
*   SP (R13): stack pointer
*   LR (R14) link register
*   PC (R15) program counter

#### 6.2.2. A32 Assembly

#### 6.2.3. Thumb Assembly

### 6.3. A64 Architecture

#### 6.3.1. A64 Registers

*   X0-X30: 64bit general purpose
*   W0-W30: 32bit general purpose
*   ZXR, WZR: zero register
*   LR(X30): link register
*   SP: stack pointer
*   PC: program counter

#### 6.3.2. A64 Assembly

**svc** for system call

## 7. RISC-V

*   [official website](https://riscv.org/)

## 8. Nvidia family

PTX

## 9. Reference

[1] CMU 15418 [http://www.cs.cmu.edu/~418/](http://www.cs.cmu.edu/~418/)

[2] Hennessy, John L., and David A. Patterson. _Computer architecture: a quantitative approach_. Elsevier, 2011.

[3] Patterson, David A., and John L. Hennessy. _Computer Organization and Design ARM Edition: The Hardware Software Interface_. Morgan kaufmann, 2016.

[4] arm developer document [https://developer.arm.com/docs](https://developer.arm.com/docs)