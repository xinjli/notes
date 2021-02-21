# 0x332 Compiler

- [1. Foundation](#1-foundation)
- [2. Compiler](#2-compiler)
	- [2.1. Lexical Analysis](#21-lexical-analysis)
	- [2.2. Syntax Analysis](#22-syntax-analysis)
	- [2.3. Semantic Analysis](#23-semantic-analysis)
	- [2.4. Security](#24-security)
- [3. Debugger](#3-debugger)
	- [3.1. gdb](#31-gdb)
	- [3.2. lldb](#32-lldb)
- [4. Reference](#4-reference)

## 1. Foundation
- compiler
- JIT compiler
- Interpreter


## 2. Compiler
### 2.1. Lexical Analysis
### 2.2. Syntax Analysis
### 2.3. Semantic Analysis

### 2.4. Security
There are several compilers features to mitigate security risks

**Stack smashing protector**
To mitigate risk of stack buffer overflow.  (only mitigate, can be exploited by overwriting canary by the correct value, maybe overwriting the canary's global reference ?)
insert canary variable into higher stack address before running risk function.
Check whether the canary (expected value is on heap) has been modified after running risk.

``` c
/* Note how buffer overruns are undefined behavior and the compilers tend to
   optimize these checks away if you wrote them yourself, this only works
   robustly because the compiler did it itself. */
extern uintptr_t __stack_chk_guard;
noreturn void __stack_chk_fail(void);
void foo(const char* str)
{
	uintptr_t canary = __stack_chk_guard;  // automatically inserted by compiler
	char buffer[16];
	strcpy(buffer, str);
	if ( (canary = canary ^ __stack_chk_guard) != 0 ) // automatically inserted by compiler
		__stack_chk_fail();
}
```



## 3. Debugger
### 3.1. gdb
i r: print variables
x/(number) (memory or register): print data around memory

### 3.2. lldb
Main Reference is here
frame instructions
bt: print stack frames
fr v (-L): print variables in a frame (with its location)
fr s frame_number: switch to different frames
memory instructions
mem read (memory or register)+(offset): print data around memory
reference
evaluation
eval (expression)

## 4. Reference
[1] [lldb cheat sheet](https://www.nesono.com/sites/default/files/lldb%20cheat%20sheet.pdf)
[2] [lldb documentation](https://lldb.llvm.org/)
[3] [9cc compiler and its explanation (Japanese)](https://www.sigbus.info/compilerbook)