- title : Introduction to F# 
- description : Introduction to F#
- author : Tomasz Heimowski
- theme : white
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
3. Outstanding F# features
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

|                     | F#                  | Scala               |
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

//active patterns

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

## Outstanding F# features

* Type providers
* Type inference
* One-pass compiler
* Units of measure

---

### Type providers

// TODO: explain type providers

---

#### JSON Type Provider
#### Open Weather API

http://openweathermap.org/api

![type-provider-json.gif](images/type-provider-json.gif)

---

#### CSV Type Provider
#### Yahoo Finance Stocks

![type-provider-csv.gif](images/type-provider-csv.gif)

---

#### World Bank Type Provider

http://data.worldbank.org/

![type-provider-wb.gif](images/type-provider-wb.gif)

---

#### And many more!

* F# Data library: CSV, HTML, JSON, XML, World Bank
* F# Management library: FileSystem, Registry, WMI, Powershell, SystemTimeZones
* F# Configuration library: AppSettings, Resources, Yaml, *.ini
* SQL Clients, R language
* Apiary, Freebase, Excel, Graph, Math, Xaml, CRM, DbPedia
* Twitter, RSS, NuGet, DGML, DataStore, Hadoop/Hive/Hdfs, MiniCvs, COM
* FunScript, Matlab, IKVM, Python, Azure, S3, Neo4j, Swagger
* ...

More on type providers [in this presentation](http://sergey-tihon.github.io/Talks/typeproviders)

---

### Type inference

Hindley-Milner type system

---

### One-pass compiler

---

### Units of measure

    [lang=fsharp]
    [<Measure>] type km           // Define the measure units
    [<Measure>] type mi           // as simple types decorated
    [<Measure>] type h            // with Measure attribute

    let speedKmh = 90<km> / 1<h>  // Can be combined through
    let speedMph = 55<mi> / 1<h>  // arithmetic operations

    let v1, v2, v3 = 3.1<km/h>, 2.7<km/h>, 1.5<mi/h>
    let sum = v1 + v2
    //let sum' = v1 + v3          // Error: doesn't compile

    // Can be used in a generic way
    type Vector3D<[<Measure>] 'u> =
        { x: float<'u>; y: float<'u>; z: float<'u> }

Units of measure is a compile-time only feature

***

## What's missing???

* HKT
* Macros

***

## Evolution of the language

* F# Software Foundation
* Community-driven
* X-Plat support
* Commercial use
* Known projects

---

### F# Software Foundation

![fsharp.org.png](images/fsharp.org.png)

http://fsharp.org/

> The mission of the F# Software Foundation is to promote,
> protect, and advance the F# programming language, 
> and to support and facilitate the growth of a diverse 
> and international community of F# programmers.

---

### Community-driven

---

### X-Plat support

---

### Commercial use

http://fsharp.org/testimonials/

<div>
    <img class="use" style="display: inline-block;vertical-align:middle" src="images/use-microsoft.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:50px" src="images/use-jet.png" />
    <img class="use" style="display: inline-block;vertical-align:middle" src="images/use-tachyus.png" />
    <img class="use" style="display: inline-block;vertical-align:middle" src="images/use-credit_suisse.png" />
</div>


<div>
    <img class="use" style="display: inline-block;vertical-align:middle;height:35px" src="images/use-handelsbanken.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:40px" src="images/use-prolucid.jpg" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:55px" src="images/use-greeneagle.png" />
</div>

<div>
    <img class="use" style="display: inline-block;vertical-align:middle;height:40px" src="images/use-kaggle.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:60px" src="images/use-grange.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:60px" src="images/use-gamesys.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:50px" src="images/use-15below.png" />
    <img class="use" style="display: inline-block;vertical-align:middle;height:65px" src="images/use-readify.png" />
</div>

<div>
    <img class="use" style="display: inline-block;vertical-align:middle;height:35px" src="images/use-waagnerbiro.png" />    
    <img class="use" style="display: inline-block;vertical-align:middle;height:65px" src="images/ihsmarkit.svg" />    
</div>

---

### Commercial use

![walmart.png](images/walmart.png)

<img style="height:350px" src="images/twitter_for_scala.png" />

---

### Known projects

* FsReveal meta

***

## Using F# at work

* Safe ways for introducing new language
* Practical example

***

## Q&A