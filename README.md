# Notes

This repo contains my personal notes in many different academic domains. I find it easier for me to learn new materials and refresh old concepts when I summarized in this style. I have been writing these notes from 2017, and will keep updating regularly. 

The contents in this repo are built and hosted at [https://note.xinjianl.com](https://note.xinjianl.com)

## Install

You can build the website by youself with following commands
```
# you need to install mkdocs to build
pip install mkdocs

# build static pages
mkdocs build
```

## Contents

Each md file is typically organized to follow the structures of textbooks in that domain, but I have re-organized many structures so that it makes more sense to me. All notes here are roughly sorted and indexed from theoretical topics to practical topics (abstract to concrete). It starts from the most fundamental ZF(C) axioms to the "most" practical topics of speech recognition (which is my research focus). Some notes are merely placeholders to keep the tree structure.


The tree of main contents is as follows
```
├── 0x0-Mathematics
│   ├── 0x00-Foundation
│   │   ├── 0x000-Set-And-Logic.md
│   │   ├── 0x001-Topology.md
│   │   └── 0x002-Sequence-And-Series.md
│   ├── 0x01-Algebra
│   │   ├── 0x010-Abstract-Algebra.md
│   │   ├── 0x011-Linear-Algebra.md
│   │   └── 0x012-Matrix-Algebra.md
│   ├── 0x02-Analysis
│   │   ├── 0x020-Foundation.md
│   │   ├── 0x022-Real-Analysis.md
│   │   └── 0x023-Convex-Analysis.md
│   ├── 0x03-Geometry
│   │   ├── 0x030-Foundation.md
│   │   └── 0x031-Differential-Geometry.md
│   ├── 0x04-Applied
│   │   ├── 0x040-Probability.md
│   │   ├── 0x041-Stochastics.md
│   │   └── 0x042-Cryptography.md
│   └── Table-of-Contents.md
├── 0x1-Natural-Science
│   ├── 0x10-Subatom
│   │   ├── 0x100-Standard-Model.md
│   │   └── 0x101-Quantum-Mechanics.md
│   ├── 0x11-Classical-Physics
│   │   ├── 0x110-Classical-Mechanics.md
│   │   ├── 0x111-Electrodynamics.md
│   │   ├── 0x112-Thermodynamics.md
│   │   └── 0x113-Statistical-Mechanics.md
│   ├── 0x12-Chemistry
│   │   └── 0x120-Foundation.md
│   ├── 0x13-Biology
│   │   └── 0x130-Cell.md
│   ├── 0x14-Earth-Science
│   │   └── 0x140-Geology.md
│   ├── 0x15-Astronomy
│   │   ├── 0x150-Foundation.md
│   │   ├── 0x151-Astrophysics.md
│   │   ├── 0x152-Observatory.md
│   │   ├── 0x153-Planet.md
│   │   ├── 0x154-Star.md
│   │   └── 0x155-Galaxy.md
│   └── Table-of-Contents.md
├── 0x2-Engineering
│   ├── 0x20-Mechanical-Engineering
│   │   ├── 0x200-Foundation.md
│   │   └── 0x201-Mechanism.md
│   ├── 0x21-Electronic-Engineering
│   │   ├── 0x210-Signal-Processing.md
│   │   ├── 0x211-Semiconductor.md
│   │   ├── 0x212-Analog-Circuits.md
│   │   ├── 0x213-Digital-Circuits.md
│   │   └── 0x214-Integrated-Circuits.md
│   ├── 0x22-Computer-Engineering
│   │   ├── 0x220-Foundation.md
│   │   ├── 0x221-Microarchitecture.md
│   │   ├── 0x222-Architecture.md
│   │   └── 0x223-Computer-Organization.md
│   ├── 0x23-Quantum-Engineering
│   │   └── 0x230-Foundation.md
│   └── Table-of-Contents.md
├── 0x3-Computer-Science
│   ├── 0x30-Theory
│   │   ├── 0x300-Computation.md
│   │   ├── 0x301-Complexity.md
│   │   └── 0x302-Information-Theory.md
│   ├── 0x31-Algorithm
│   │   ├── 0x310-Arithmetic.md
│   │   ├── 0x311-Numerical.md
│   │   ├── 0x312-Continuous-Optimization.md
│   │   ├── 0x313-Search.md
│   │   ├── 0x314-Combinatorial-Optimization.md
│   │   └── 0x315-Sequence.md
│   ├── 0x32-Operating-System
│   │   ├── 0x320-Foundation.md
│   │   ├── 0x321-Kernel.md
│   │   ├── 0x322-Linux-Interface.md
│   │   └── 0x323-Windows-Interface.md
│   ├── 0x33-Execution
│   │   ├── 0x330-Assembler.md
│   │   ├── 0x331-Linker.md
│   │   ├── 0x332-Compiler.md
│   │   ├── 0x333-Build.md
│   │   └── 0x334-Runtime.md
│   ├── 0x34-Language
│   │   ├── 0x340-Foundation.md
│   │   ├── 0x341-C.md
│   │   ├── 0x342-C++.md
│   │   ├── 0x343-Java.md
│   │   ├── 0x344-JavaScript.md
│   │   ├── 0x345-Go.md
│   │   ├── 0x346-Python.md
│   │   └── 0x347-SQL.md
│   ├── 0x35-Computing
│   │   ├── 0x351-Distributed-Systems.md
│   │   └── 0x352-Distributed-Applications.md
│   ├── 0x36-Network
│   │   ├── 0x360-Physical-And-Link.md
│   │   ├── 0x361-Network-And-Transport.md
│   │   ├── 0x362-Application.md
│   │   └── 0x363-Security.md
│   ├── 0x37-System
│   │   ├── 0x370-Browser.md
│   │   ├── 0x371-Server.md
│   │   └── 0x372-Database.md
│   ├── 0x38-Software-Engineering
│   │   └── 0x380-Design-Pattern.md
│   └── Table-of-Contents.md
├── 0x4-Artificial-Intelligence
│   ├── 0x40-Statistics
│   │   ├── 0x400-Distribution.md
│   │   └── 0x401-Frequentist.md
│   ├── 0x41-Machine-Learning
│   │   ├── 0x410-Foundation.md
│   │   ├── 0x411-Supervised-Learning.md
│   │   ├── 0x412-Unsupervised-Learning.md
│   │   └── 0x413-PGM.md
│   ├── 0x42-Deep-Learning
│   │   ├── 0x420-Foundation.md
│   │   ├── 0x421-Module.md
│   │   └── 0x423-Unsupervised.md
│   ├── 0x43-Natural-Language-Processing
│   │   ├── 0x430-Foundation.md
│   │   ├── 0x431-Language-Model.md
│   │   ├── 0x432-Syntax.md
│   │   ├── 0x433-Semantics.md
│   │   ├── 0x434-Translation.md
│   │   └── 0x435-Search-Engine.md
│   ├── 0x44-Computer-Vision
│   │   ├── 0x440-Foundation.md
│   │   ├── 0x441-Classification.md
│   │   ├── 0x442-Segmentation.md
│   │   └── 0x443-Generation.md
│   ├── 0x45-Speech
│   │   ├── 0x450-Phonetics.md
│   │   ├── 0x451-Phonology.md
│   │   ├── 0x452-Speech-Synthesis.md
│   │   └── 0x453-Speech-Recognition.md
│   └── Table-of-Contents.md
```
