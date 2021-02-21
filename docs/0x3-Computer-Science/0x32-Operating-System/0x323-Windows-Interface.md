# 0x323 Windows Interface

- [1. Process](#1-process)
- [2. IPC](#2-ipc)
    - [2.1. COM IPC](#21-com-ipc)
    - [2.2. WinRT IPC](#22-winrt-ipc)

## 1. Process
Windows Process
Windows do not have fork, use spawn (fork + exec) or CreateProcess instead

**API (CreateProcess)**
Windows Thread
Unlike Linux, Thread is implemented at OS level in Window and SunOS

## 2. IPC
Windows has following IPC mechanism according to this page
Clipboard, COM, Data Copy, DDE, File Mapping, MailSlot, Pipes, Windows Socket, RPC 

### 2.1. COM IPC
In my personal understanding, COM is doing following things equivalent in linux

- fork a process
- open pipe to share message binary memory
- construct object over binary (COM interface defines how to construct obj) and manage its life
- close the process
  
### 2.2. WinRT IPC
wrapper of COM