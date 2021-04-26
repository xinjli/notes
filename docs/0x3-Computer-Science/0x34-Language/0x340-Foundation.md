# 0x340 Foundation

- [1. History](#1-history)
- [2. Basic](#2-basic)
- [3. Syntax](#3-syntax)
- [4. Semantics](#4-semantics)
- [5. Paradigms](#5-paradigms)
    - [5.1. Declarative Languages](#51-declarative-languages)
        - [5.1.1. Functional Languages](#511-functional-languages)
        - [5.1.2. Logic Languages](#512-logic-languages)
        - [5.1.3. Others](#513-others)
    - [5.2. Imperative Languages](#52-imperative-languages)
        - [5.2.1. Procedure Languages](#521-procedure-languages)
        - [5.2.2. Objected Oriented Languages](#522-objected-oriented-languages)
- [6. Others](#6-others)
- [7. Reference](#7-reference)

## 1. History

- 1957: Fortran by Backus (1977 Turing Award)
- 1958: Lisp by John McCarthy (1971 Turing Award)
- 1960: COBOL by Grace Hopper
- 1960: ALGOL by Backus, Bauer
- 1964: BASIC by John Kemeny and Thomas Kurtz from Dartmouth
- 1967: SIMULA 67 (first OOP) by Ole-Johan Dahl and Kristen Nygaard (2001 Turing Award)
- 1972: C by Dennis Ritchie (1983 Turing Award)

## 2. Basic
**Elements (Programming)**

- **primitive elements**: represents the simplest entities the language is concerned
- **means of combination**: by which compounded elements are built from simpler ones
- **means of abstraction**: by which compounded elements can be named and manipulated as units

**Concept (Declarative vs. Imperative)**
In Mathematics, we are usually concerned with declarative (what is) descriptions, whereas in computer science we are usually concerned with the imperative (how to) descriptions. 

For example,  the following square mathematical description is declarative, i.e. what properties square has, but gives no clue how to compute it

$$\sqrt(x) = \{ y | y \geq 0 \land y^2 = x \} $$ 

In contrast, procedure (imperative) description (e.g. Newton methods) can specify how to compute square root.

**Concept (Normal order vs Applicative Order)**
Lisp uses *applicative-order* evaluation, i.e. interpreter evaluates the operator and operand and then applies. The alternative is *normal-order* evaluation which the interpreter fully substitutes to expand and then reduce.

**Concept (Recursive Process vs. Iterative Process)**
The recursive process expands the procedure by chaining deferred operations

The iterative process keep their info in state variables (in arguments) and call itself using tail-recursive (which can be optimized without adding new stack frame in some languages including Scheme. C looks like not require it, adding O2, O3 might generate it though. )

Note that this tail-call optimziation techniques is not limited to recursion, it can be applied whenever there is a function call (either to itself or to some other functions). In the actual implementation, it is replacing the call instruction with jmp instruction (without updating the return address). [This](https://eklitzke.org/how-tail-call-optimization-works) is an good article about it.

A good technique to design iterative algorithms is to define an invariant quantity that remains unchanged from state to state (SICP exercise 1.16)

**Concept (First-class Citizen vs Second-class Citizen)**
An element is called the First-class citizen in one programming language if it supports most operations available to other elements with the fewest restrictions. 

Some properties of the first-class citizens are

- They may be named by variables
- They may be passed as arguments to procedures
- They may be returned as the results of procedures
- They may be included in data structures
  
For example, array in C language is not first-class because array loses its size when passed to a procedure. Lisp unlike other common languages, awards procedures full first-class status.

**Concept (lexical scope vs dynamic scope)**

**Lexical scope (static scope)** is the scope defined by the portion of source code. The granularity can vary for different languages. In particular, the following scopes are common, sorted roughly from local to global.

- **expression scope**: binding names in an expression (e.g: `let` in functional programming, list comprehension in python)
- **block scope**: variables are available in blocks (originalted from ALGOL), note that block definition are different across languages. (e.g: brace parenthesis, begin, if, ...)
- **function scope**: scope is between when the function starts (or the variable is declared) to when the function returns (e.g: python, `var` in Javascript)
- **file scope**: C and C++
- **Module scope**: Modula (descendant of Pascal), Go
- **Global scope**: available in the entire program

**Dynamic scope** is the scope defined by the running program (e.g.: call stack) rather than the source code. Common among Lisp's dialects (e.g: common lisp)

**Concept (closure)** `closure` is a technique to implement lexically scoped name binding in a language with first-class functions.

```python
def h(x):
    return lambda y: x + y  # Return a closure.
```

## 3. Syntax
**Concept (Prefix Notation vs Postfix Notation)**
- **Prefix notation (Polish Notation)**: Operator comes before the operands. Lisp is this style
- **Postfix Notation (Reverse Polish Notation)**: Operator comes after the operands. It is similar to SOV languages (e.g. Japanese). PostScript is this style.

**Concept (statement vs expression)** Details are different across languages, but roughly speaking, expression is the syntactic unit that usually produces something but statement is the syntactic unit that carries out something. Expressions rarely have side effects in functional languages.

Confusingly, *statement* in mathematical logic is defined to be evaluated to either *true* or *false*



## 4. Semantics

## 5. Paradigms
The programming languages can be roughly classified into following classes, but note that modern languages usually support multiple paradigms.

### 5.1. Declarative Languages
#### 5.1.1. Functional Languages
**Definition (pure function)** A pure function is a function that has the following properties.
- *referential transparency*: The function always gives the same return value for the same arguments, it cannot depends on any mutable states
- *side-effect free*: The function cannot have side-effect (e.g: IO, modify mutable objects, reassignment...)

But how can you write pure functions without IO?!
This [blog](https://alvinalexander.com/scala/fp-book/pure-functions-and-io-input-output/) has an explanation. In short, write your application as much as possible with pure functions, and handle other side-effect components in other ways (e.g: IO monad in Haskell).


#### 5.1.2. Logic Languages

#### 5.1.3. Others
SQL belongs to this class

### 5.2. Imperative Languages

#### 5.2.1. Procedure Languages
 
#### 5.2.2. Objected Oriented Languages


## 6. Others
The followings are Kernighan's summary about successful languages

Why languages succeed?

- solve real problems in a clearly better way
- culturally compatible and familiar
- environmentally compatible
- weak competition
- good luck!
  
Why languages fail to thrive?

- niche or domain disappears
- poor engineering
- poor philosophical choices


## 7. Reference
[1] Abelson, Harold, and Gerald Jay Sussman. Structure and interpretation of computer programs. The MIT Press, 1996.

[2] Brian Kernighan on successful language design https://www.youtube.com/watch?v=Sg4U4r_AgJU&t=2501s
