# 0x346 Python

- [1. Data Structure](#1-data-structure)
    - [1.1. cpython internals](#11-cpython-internals)
        - [1.1.1. PyObject](#111-pyobject)
        - [1.1.2. int (PyLongObject)](#112-int-pylongobject)
    - [1.2. Sequence](#12-sequence)
- [2. Classes and Protocols](#2-classes-and-protocols)
    - [2.1. Iterable, Iterator and Generator](#21-iterable-iterator-and-generator)
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



## 2. Classes and Protocols
### 2.1. Iterable, Iterator and Generator
- Iterable: An object which can generator iterator. In python, either __iter__ or __getitem__should be implemented to be an Iterable

- Iterator: An object that implement __next__ and raise StopIteration when items exhausted

- Generator: simple lazy iterator, any function using coroutine yield

use itertools library


## 3. Reference
[1] cpython Github (https://github.com/python/cpython)

[2] cpython internals (https://github.com/zpoint/CPython-Internals)

[3] Ramalho, Luciano. Fluent Python: clear, concise, and effective programming. " O'Reilly Media, Inc.", 2015.

