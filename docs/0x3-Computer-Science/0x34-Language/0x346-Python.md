# 0x346 Python

- [1. Data Structure](#1-data-structure)
    - [1.1. cpython internals](#11-cpython-internals)
        - [1.1.1. PyObject](#111-pyobject)
        - [1.1.2. int (PyLongObject)](#112-int-pylongobject)
    - [1.2. Sequence](#12-sequence)
- [Functions](#functions)
- [2. Classes and Protocols](#2-classes-and-protocols)
    - [2.1. Iterable, Iterator and Generator](#21-iterable-iterator-and-generator)
- [CPython Interpreter Internal](#cpython-interpreter-internal)
    - [Lexical Analysis](#lexical-analysis)
    - [Bytecode Compile](#bytecode-compile)
    - [Virtual Machine](#virtual-machine)
- [Compiler](#compiler)
    - [Cython](#cython)
    - [Numba](#numba)
        - [Nopython mode](#nopython-mode)
        - [object mode](#object-mode)
    - [Pypi](#pypi)
- [Numpy](#numpy)
    - [API](#api)
- [3. Reference](#3-reference)

## 1. Data Structure
### 1.1. cpython internals

#### 1.1.1. PyObject
The object definition in cpython is [here](https://github.com/python/cpython/blob/master/Include/object.h)
where the most basic type is defined as 

```c
typedef struct _object {
    _PyObject_HEAD_EXTRA // struct _object *_ob_next; struct _object *_ob_prev;
    Py_ssize_t ob_refcnt;
    PyTypeObject *ob_type;
} PyObject;
```

So basically each python object looks to be a item in a double-linked list with ref count.

The variable length objects is using `PyVarObject` defined as
```c
typedef struct {
    PyObject ob_base;
    Py_ssize_t ob_size; /* Number of items in variable part */
} PyVarObject;
```


#### 1.1.2. int (PyLongObject)
Integer related struct are as follows, reference is from [include/longintrepr.h](https://github.com/python/cpython/blob/master/Include/longintrepr.h)
```c
struct _longobject {
    PyObject_VAR_HEAD
    digit ob_digit[1];
};
```

There are some optimizations for small integers (-5 ~ 256) where python allocated in advance, so do not need to malloc everytime for those integers. Note that tuple has the same type of optimizations.

### 1.2. Sequence
There are two types of sequences from the standard library
- **container sequences**:  contains the reference (e.g: list, tuple, collections.deque)
- **flat sequences**:  contains the value directly (e.g: str, bytes, bytearray, memoryview, array.array)


## Functions
Functions in python are first-class objects, which means they can be

- created at runtime
- assigned to a variable
- passed as an arg to a function
- return as the result from a function


Btw, Guido van Rossum did not view python as a functional programming.




## 2. Classes and Protocols
### 2.1. Iterable, Iterator and Generator

- Iterable: An object which can generator iterator. In python, either `__iter__` or `__getitem__` should be implemented to be an Iterable
- Iterator: An object that implement `__next__` and `raise StopIteration` when items exhausted
- Generator: simple lazy iterator, any function using coroutine yield

use itertools library

## CPython Interpreter Internal

### Lexical Analysis


### Bytecode Compile
The compiler here takes the AST and compile it into python bytecode, we can see how they get compiled with `dis` module. There is also a 3rd party disassembler `uncompyle6` translate pyc back to bytecode


The compiler implementation is [cpython/Python/compiler.c](https://github.com/python/cpython/blob/145bf269df3530176f6ebeab1324890ef7070bf8/Python/compile.c)

```python
dis.dis('a=1') # compile this get following bytecodes
# 0 LOAD_CONST               0 (1)
# 2 STORE_NAME               0 (a)
# 4 LOAD_CONST               1 (None)
# 6 RETURN_VALUE
```

Current bytecode is available here in [cpython/include/opcode](https://github.com/python/cpython/blob/145bf269df3530176f6ebeab1324890ef7070bf8/Include/opcode.h). It has around 165 bytecodes.

Some examples of bytecodes
```text
# arithmetic examples
# BINARY operation here means takes the top 2 from stack and perform operation then put it back
BINARY_ADD
BINARY_MULTIPLY
INPLACE_ADD // for case such as i += 1

# logic examples
UNARY_NOT
BINARY_AND

# variable ops examples
LOAD_CONST //  load const variables to stack
LOAD_FAST  // this loads local variables to stack
SAVE_FAST  // save local variables to stack
LOAD_GLOBAL // loads global variables to stack

# function ops examples
CALL_FUNCTION // execute function
RETURN_VALUE  // return

# stack related examples
POP_TOP // pop from stack, this has the op number 1!
SET_TOP 

# others
ROT_TWO // swap two vars on top of the stack, used in cases like (a,b)=(b,a)
BUILD_STRING // build string
BUILD_TUPLE // for most commonly used python data structures, it looks we have this type of ops
```

### Virtual Machine
CPython VM executes those bytecode with a stack machine architecture (e.g: push, pop, execute ops)

The main VM is implemented [cpython/python/ceval.c](https://github.com/python/cpython/blob/145bf269df3530176f6ebeab1324890ef7070bf8/Python/ceval.c)

```c
// for example, this is BINARY_ADD impl and some of my comments
        case TARGET(BINARY_ADD): {
            PyObject *right = POP(); // this is roughly doing (*--stack_pointer)
            PyObject *left = TOP();  // this is defined as stack_pointer[-1]

            PyObject *sum;
            if (PyUnicode_CheckExact(left) &&
                     PyUnicode_CheckExact(right)) {
                sum = unicode_concatenate(tstate, left, right, f, next_instr);
                /* unicode_concatenate consumed the ref to left */
            }
            else {
                sum = PyNumber_Add(left, right); // of course, this is adding big integer not int32
                Py_DECREF(left); // decrement reference
            }
            Py_DECREF(right);
            SET_TOP(sum);
            if (sum == NULL)
                goto error;
            DISPATCH(); // this is roughly defined as `goto` fast_next_opcode
        }
```

## Compiler
There is a couple of options to compile python code into machine code to improve speed. Mathematical code with many loops can benefit from these compiling approach.

### Cython
Cython is a ahead-of-time (AOT) compiler

### Numba
Numba is a just-in-time (JIT) compiler. It compiles the bytecode into machine code on the first time the function get executed.

#### Nopython mode
aggressive compilation. Numba need to be able to infer the types of all variables.
numpy arrays and simple scalar types are reasonably well supported. For list and dict, use numba's typed containers: *typed-list*, *typed-dict*

#### object mode
permissive compilation. 


### Pypi

## Numpy

### API
Summary of some commonly used API

**API (np.random)**

The following API are consistent with np.ones and np.zeros
- np.random.randint(high, size=()): generate random uniform int with a target shape
- np.random.random_sample(size=()): generate random uni(0,1) with a target shape
- np.random.standard_normal(size=()): generate random $n(0,1)$ with a target shape


## 3. Reference
[1] cpython Github (https://github.com/python/cpython)

[2] cpython internals (https://github.com/zpoint/CPython-Internals)

[3] Ramalho, Luciano. Fluent Python: clear, concise, and effective programming. " O'Reilly Media, Inc.", 2015.

