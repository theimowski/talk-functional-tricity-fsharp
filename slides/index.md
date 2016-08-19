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

* About
* Origins
* Influencing languages

<div style="">
    <img class="use" style="display: inline-block;vertical-align:middle;height:150px" src="images/fsharp_old.png" />
    <span style="font-size:64px">===></span>    
    <img class="use" style="display: inline-block;vertical-align:middle;height:180px;width:50px" src="images/fsharp256.png" />    
</div>

---

### About

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

---

* [F# for Scala developers](https://alfonsogarciacaro.github.io/fsharp-for-scala-developers) by Alfonso Garcia-Caro
* [Comparing Scala to F#](http://mikhail.io/2016/08/comparing-scala-to-fsharp/) by Mikhail Shilkov

---

### General similarities
### Both F# and Scala:

* Introduce FP to an OOP platform (.NET and JVM),
* Enable interoperability with the existing ecosystem,
* Fall into the category of non-purely functional languages,
* Provide static typing with type inference,
* Ship with a set of base libraries.

---

### General differences

|                     | F#                  | Scala               |
| :------------------ | :-----------------: | :-----------------: |
| **Paradigm**        | Functional-first    | Both OOP and FP     |
| **FP features\***   | Native to platform  | Compiler level      |
| **Syntax**          | Strict, concise     | Loose, verbose      |
| **Scopes**          | Whitespace sensitive| Curly braces        |

\* Functional features such as [generics](http://stackoverflow.com/a/31929/1397724) or [tail calls](https://blogs.msdn.microsoft.com/fsharpteam/2011/07/08/tail-calls-in-f/)

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

### Nulls

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let x : Option<string> = None // must use option type
    //let y : string = null       // compile error

![scala](images/scala.png)

    [lang=scala]
    val x: Option[String] = None  // can use option type
    val y: String = null          // but can also use null

---

### Functions

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let add x y = x + y
    let z = add 10 4                    // function application
    let add5 = add 5                    // curried by default

    let lambda = fun x -> x * 2         // explicit arguments

![scala](images/scala.png)

    [lang=scala]
    def add (x:Int, y:Int) = x + y
    val z = add(10,4)                   // function application
    val add5: (Int) => Int = add(5,_)   // underscore for currying

    val lambda: Function[Int,Int] = _*2 // implicit arguments

---

### Type inference

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let x = 28                             // int
    let y = "hello"                        // string
        
    let add x y = x + y                    // generalization
    let addF = fun x y -> x + y            // same with lambda
    let doItTwice f = f >> f               // composed function

==> [Hindley-Milner type system](https://en.wikipedia.org/wiki/Hindley%E2%80%93Milner_type_system)

![scala](images/scala.png)

    [lang=scala]
    val x = 28                             // int
    val y = "hello"                        // string
        
    def add (x:Int, y:Int) = x + y         // explicit types
    val addF: Function[Int,Int,Int] = _+_  // lambda

---

### Discriminated unions (ADT sum types)

![fsharp](images/fsharp.png)

    [lang=fsharp]
    type Shape =
    | Rectangle of width: float * height: float
    | Circle of radius: float

    let area = function
    | Rectangle (width, height) -> width * height
    | Circle radius -> System.Math.PI * (radius ** 2.0)

![scala](images/scala.png)

    [lang=scala]
    sealed abstract class Shape
    case class Rectangle(width: Float, height: Float) extends Shape
    case class Circle(radius: Float) extends Shape

    def area(shape: Shape): Double = shape match {
      case Rectangle(width, height) => width * height
      case Circle(radius) => Math.Pi * radius * radius
    }

---

### Tuples (ADT product types)

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let meetup = 3, "Functional Tricity"   // constructing
    let (_,group) = meetup                 // pattern matching
    let occurence = fst meetup             // extracting
    let f (occurence, group) = ()
    let _ = f meetup                       // as function params

![scala](images/scala.png)

    [lang=scala]
    val meetup = (3, "Functional Tricity") // constructing
    val (_,group) = meetup                 // pattern matching
    val occurence = meetup._1              // extracting

---

### Records (Extended tuples)

![fsharp](images/fsharp.png)

    [lang=fsharp]
    type Meetup = { Occurence : int; Group : string }
    let meetup = { Occurence = 3; Group = "Functional Tricity" }
    let { Group = group } = meetup
    let occurence = meetup.Occurence
    let next = { meetup with Occurence = 4 }
    let equal = meetup = { Occurence = occurence; Group = group }

---

### Active patterns

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let (|Even|Odd|) n = if n % 2 = 0 then Even else Odd
    let test = function Even -> "Even number" | Odd -> "Odd number"

![scala](images/scala.png)

    [lang=scala]
    object Even { def unapply(x: Int) = if (x % 2 == 0) Some(x) else None }
    object Odd  { def unapply(x: Int) = if (x % 2 == 1) Some(x) else None }
    def test(x: Int) =
        x match { case Even(_) => "Even number" case Odd(_) => "Odd number" }

---

### Active patterns - partial & args

![fsharp](images/fsharp.png)

    [lang=fsharp]
    let (|Integer|_|) (str: string) =
        match System.Int32.TryParse str with
        | (true, i) -> Some i | (false, _) -> None

    open System.Text.RegularExpressions
    let (|ParseRegex|_|) regex str =
        match Regex.Match(str, regex) with
        | m when not m.Success -> None
        | m -> [for x in m.Groups -> x.Value] |> List.tail |> Some

    let parseDate str =
        match str with
        | ParseRegex @"^(\d{1,2})/(\d{1,2})/(\d{1,2})$"
                    [Integer m; Integer d; Integer y]
            -> Some (System.DateTime(y + 2000, m, d))
        | _ -> None

---

### Pipes

---

### Generics, HKT?

---

### Computation Expressions

---

### Summary

![fs_vs_sc.png](images/fs_vs_sc.png)

***

## Outstanding F# features

* Type providers
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
* More on type providers [in this presentation](http://sergey-tihon.github.io/Talks/typeproviders)

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

<img style="height:350px" src="images/twitter_for_scala.png" />

<img style="height:150px" src="images/walmart.png" />



---

### Known projects

* FsReveal meta

***

## Using F# at work ???

* Safe ways for introducing new language
* Practical example

***

## Q&A