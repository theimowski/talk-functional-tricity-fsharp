- title : Introduction to F# 
- description : Introduction to F#
- author : Tomasz Heimowski
- theme : night
- transition : default

***

![fsharp256.png](images/fsharp256.png)

## Introduction to F#

### Tomasz Heimowski

http://theimowski.com/

@theimowski

![ihsmarkit](images/ihsmarkit.svg)

---

## Agenda

1. Brief history
2. Basics - comparison with Scala
3. Greatest features
4. Evolution of the language
5. Using F# at work

***

## Brief history

* Origins
* Influencing languages

---

### Origins

* Born in 2005 (bundled with VS 2005), from Microsoft Research initiative
* Development lead by Don Syme
* Aimed to incorporate Functional Programming into .NET platform 
* Originally closed source

---

### Influencing languages

* OCaml - syntax
* Haskell - functional
* C# - .NET interop
* **Scala** - FP on OOP platform
* Python - whitespace
* Erlang - actor model

***

## Basics - comparison with Scala

* General assumptions
* Semantics
* Syntax

![fs_vs_sc.png](images/fs_vs_sc.png)

---

* [F# for Scala developers](https://alfonsogarciacaro.github.io/fsharp-for-scala-developers) by Alfonso Garcia-Caro
* [Comparing Scala to F#](http://mikhail.io/2016/08/comparing-scala-to-fsharp/) by Mikhail Shilkov

---

### General similarities
### Both F# and Scala:

* Introduce FP to an OOP platform (.NET and JVM respectively),
* Enable interoperability with the existing ecosystem,
* Fall into the category of non-purely functional languages,
* Provide static typing with type inference,
* Ship with a set of base libraries.

---

### General differences

|                     | ![fsharp](images/fsharp.png)                  | ![scala](images/scala.png)               |
| :------------------ | :-----------------: | :-----------------: |
| **Paradigm**        | Functional-first    | Both OOP and FP     |
| **Functional bits** | Baked into platform | On compiler level   |
| **Syntax**          | Strict, concise     | Loose, verbose      |
| **Scopes**          | Whitespace sensitive| Curly braces        |

---

### Mutable and immutable bindings

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let x = 28         // immutable
    let mutable y = 29 // mutable
    y <- 28            // mutation
    let z = x = y      // equality test

![scala](images/scala.png)

    [lang=scala]
    val x = 28         // immutable
    var y = 29         // mutable
    y = 28             // mutation
    val z = x == y     // equality test

---

### Nulls?

---

### Functions

---

### Discriminated unions (ADT sum types)

---

### Tuples and Records (ADT product types)

---

### Pattern matching

---

### Classes?

---

### Pipes

---

### Generics, HKT?

---

### Computation Expressions

---

### Summary

***

## Greatest features

* Type inference
* Type providers
* One-pass compiler
* Miscellaneous (Active patterns, UOM)

***

## Evolution of the language

* Commercial use
* Community-driven
* X-Plat support
* Known projects
* FsReveal meta

***

## Using F# at work

* Safe ways for introducing new language
* Practical example

***

## Q&A