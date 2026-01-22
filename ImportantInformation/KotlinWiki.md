# Kotlin
[Link to wiki here!](https://en.wikipedia.org/wiki/Kotlin)

# Introduction
Cross platform, statically typed, general purpose, high level language <br>
With type interface.<br>
Interoperate fully with Java<br>
JVM version of Kotlins standLib depends on the Java Class Library.<br>
Type interface allows suntax to be more concise.<br>
JVM is mainly targeted... but Kotlin also compiles into JavaScript!<br>
  Either with React for example... or by native code with LLVM.<br>

7th May 2019: Google said Kotlin programming has become its preferred lang for Android devs.<br>
Since Android Studio 3 release -> Kotlin included as an alt to the standard Java compiler.<br>
Android Kotlin compiler emits Java8 bytecode by default. (Runs on any later JVM)<br>
It also allows Java 9 (up to 24) for optimizing or other features:<br>
  Bidirectional record class interoperability support for JVM.<br>

Kotlin supports web with Kotlin/JS through:<br>
  Itermediate representation based backend (stable since 1.8, released 2022 Dec)<br>
Kotlin/Native declared stable since 1.9.20 (released 2023 Nov)<br>

# History
Name = from Kotlin Island (russian : in gulf of finland)<br>
Andrey Breslav (former lead designer) said team decided to name if after an island... imitating Java's backstory.<br>

First commit was on 8th November 2010<br>
July 2011 -> Project Kotlin revealed by JetBrains.<br>
  new lang for the JVM.<br>
Scala had slow compilation time, once stated that the goal was to have compilation as quick as java.<br>
The project was open sourced in 2021 Feb under the Apache2 license.<br>
1.0 was released 15th Feb 2016 - considered first official stable release.<br>
  Jetbrains committed to long term backw compatability starting with this vers.<br>
Google in 2017 states first class support for Kotlin on Android<br>
  Then 7th May 2019, they stated that Kotlin was the preferred programming lang for android development.<br>

# Design
To be an industrial strength, OO language... 'better than Java' but still fully interoperable. (allowing migrations)<br>
Semicolons = optional (statement terminator)<br>
  A new line is usually sufficient (PERSONAL NOTE: I DO NOT LIKE THIS)<br>
Variable declarations + parameter lists have the data type come AFTER the var name.<br>
  with a colon to seperate. Similar to Rust really...<br>

Influence of Scala seen in extensive support for both OO and functional programming in a num' of features:<br>
  Distinction betw mutable and immutable variables (var vs val keywords)<br>
  All classes = public, final by default (non inheritable)<br>
  Functions + methods support default arguments, var length arg lists and named args.<br>
    remember this from the py module (?)<br>

1.3 added support for contracts<br>
  stable for standLib declarations but experimental for user defined declarations.<br>
Kotlin may be transpiled to JavaScript.<br>
  Interoperability betw code written in 2 langs.<br>
  Used to write full web apps in Kotlin<br>
  or<br>
  To share code between a Kotlin Backend and JS Frontend.<br>

# Syntax
## Procedural programming style
Allows static methods and vars to exist only within a class body.<br>
Static obj and functions can be efined at the top level of the package (no need for a redundant class level)<br>
Kotlin provides JvmName annotation, defining class name used when the package is viewed from a Java project.<br>
Example:<br>
  `@file:JvmName("JavaClassName")`

## Main entry point
Entry point here is also called 'main'<br>
Can be passed an array containing cmd ln args (optional since 1.3)<br>
Type interface also supported.<br>
EXAMPLE<br>
```
// Hello, World! example
fun main() {
    val scope = "World"
    println("Hello, $scope!")
}
```
EXAMPLE WITH PASSED ARGS<br>
```
fun main(args: Array<String>) {
    for (arg in args)
        println(arg)
}
```

## Extension functions
Can add extension functions to a class without formalities of creating a derived class with new functions.<br>
This has access to all the public interface of a class.<br>
Can create a new function interface to a target class.<br>
Just see the bloody code:<br>
```
package com.example.myStringExtensions
fun String.lastChar(): Char = get(length - 1)
>>> println("Kotlin".lastChar())
```
Placing that code in top level of package:<br>
  String class is extended to include lastChar function (not originally included)<br>
```
// Overloading '+' operator using an extension function
operator fun Point.plus(other: Point): Point {
    return Point(x + other.x, y + other.y)
}

>>> val p1 = Point(10, 20)
>>> val p2 = Point(30, 40)
>>> println(p1 + p2)
Point(x=40, y=60)
```

## Scope Functions
5 of them, allows changing of scope within the context of an object.<br>
`let run with apply also`<br>

## Unpack args with spread operator
Similar to python with the asterisk. Unpacks arrays content as indiv args to a function.<br>
```
fun main(args: Array<String>) { 
    val list = listOf("args: ", *args)
    println(list)
}
```

## Destructuring declarations
NOT THE SAME as the destructor method in other OO languages.<br>
This decomposes an object into multiple vars at once<br>
  e.g. 2d coord object might be destructred into two ints: x and y.<br>
An example, Map.Entry object supports this to simplify access to key and val fields.<br>
```
for ((key, value) in map)
    println("$key: $value")
```

## Nested Functions
Local func can be declared in other func (method term used interchangably)<br>
```
class User(val id: Int, val name: String, val address: String)
// outer function
fun saveUserToDb(user: User){
  // inner function
  fun validate(user:User,value:String, fieldName:String){
    require(value.isNotEmpty()){
      "Cant save user ${user.id}: empty $fieldname"
    }
  }
  validate(user,user.name,"Name")
  validate(user,user.address,"Address")
// QUESTION-   still a little unsure here on what the purpose of the outer function is in this scenario???
}
```

## Classes are final by def
I sort of like this actually.<br>
To derive a class from a base class tupe then you must explicitaly specify with "open" keyword at the start.<br>
```
// open on the class means this class will allow derived classes
open class MegaButton {

    // no-open on a function means that 
    //    polymorphic behavior disabled if function overridden in derived class
    fun disable() { ... }

    // open on a function means that
    //    polymorphic behavior allowed if function is overridden in derived class
    open fun animate() { ... }
}

class GigaButton: MegaButton() {

    // Explicit use of override keyword required to override a function in derived class
    override fun animate() { println("Giga Click!") } 
}
```

## Abstract classes = open by default
Quality of life, it seems.<br>
Adding this myself may mean I'm more pragmatic, it becomes more clear as I am learning.<br>
They define abstract of pure virtual placeholder functions (later to be derived)<br>
```
// No need for the open keyword here, it’s already open by default
abstract class Animated {
    // This virtual function is already open by default as well
    abstract fun animate()
    open fun stopAnimating() { }
    fun animateTwice() { }
}
```

## Classes are public by defualt
Keywords to restrict visibility for top level declarations (classes and members)<br>
`public internal protected private` -> seen all these before.<br>
EXAMPLE<br>
```
// Class is visible only to current module
internal open class TalkativeButton {
    // method is only visible to current class 
    private fun yell() = println("Hey!")
    // method is visible to current class and derived classes
    protected fun whisper() = println("Let's talk!")
}
internal class MyTalkativeButton: TalkativeButton() {
    fun utter() = super.whisper()
}
MyTalkativeButton().utter()
```

## Primary vs Secondary Constructors
Primary consists of an arg list following the class name.<br>
  this supports expanded syntax on Kotlins standard function arg lists<br>
  -> Which enable declaration of class properties in the primary constructor:<br>
    Including visibility<br>
    Extensibility<br>
    Mutability attributes.<br>
When defining a subclass: Properties in super-interfaces and super-classes can be overridden in the primary constructor.<br>
```
// Example of class using primary constructor syntax
// (Only one constructor required for this class)
open class BaseUser(open var isSubscribed: Boolean)
open class PowerUser(protected val nickname: String, final override var isSubscribed: Boolean = true):BaseUser(isSubscribed) { }
```
In cases where more than one constr' req for a class:<br>
  A more general constructor can be defined with secondary constructor syntax (similar to most OO langs)<br>
EXAMPLE:<br>
```
// Example of class using secondary constructor syntax
// (more than one constructor required for this class)
class Context
class AttributeSet
open class View(ctx:Context) {
    constructor(ctx: Context, attr: AttributeSet): this(ctx)
}
class MyButton : View {
    // Constructor #1 
    constructor(ctx: Context) : super(ctx) { 
    } 
    // Constructor #2
    constructor(ctx: Context, attr: AttributeSet) : super(ctx, attr) {
        // ... 
    }
}
```

## Sealed Classes
(and interfaces) restrict subclass hierarchies.<br>
More control over interface hierarchy.<br>
`sealed interface Expr`<br>
`sealed class Job`<br>
All subclasses are defined at compile time.<br>
  no new subclasses can be added after the compilation of the module having the sealed class.<br>
EXAMPLE<br>
```
sealed class Vehicle
data class Car(val brandName: String, val owner: String, val color: String): Vehicle()
class Bike(val brandName: String, val owner: String, val color: String): Vehicle()
class Tractor(val brandName: String, val owner: String, val color: String): Vehicle()
val kiaCar = Car("KIA", "John", "Blue")
val hyundaiCar = Car("Hyundai", "Britto", "Green")
```

## Data Classes
Their construct defines classes whose purpose is primarily to store data.<br>
(Similar to java record types)<br>
Costruct is similar to normal classes except the following key methods are auto genned from class properties:<br>
  `equals`, `hashCode`, `toString`<br>
```
$ kotlinc-jvm
type :help for help; :quit for quit
>>> 2 + 2
4
>>> println("Hello, World!")
Hello, World!
```

## Kotlin as a scripting language
Script = source file using .kts extension. (with an executable source code at top level scope)<br>
```
// list_folders.kts
import java.io.File
val folders = File(args[0]).listFiles { file -> file.isDirectory() }
folders?.forEach(::println)
```
They can be ran by passing the -script option and corresponding script file to the compiler.<br>
`$ kotlinc -script list_folders.kts "path_to_folder_to_inspect"`<br>
This may be very useful for testing newly learnt features.<br>
Then again we are installing android studio I believe - or something similar: TODO = due to find out.<br>

## Null safety
All nullable objects must be declared with a ? postfix after the type name.<br>
Ops on nullable objects need care from devs...<br>
A null check must be performed before using the value. (explicitly or using Kotlins null-safe operators)<br>

`?.` = safe navigation operator<br>
  used to safely access a method or property of a POSSIBLY null object.<br>
  if null, method WONT be called, expression evaluates to null.<br>
EXAMPLE<br>
```
// returns null if...
// - foo() returns null,
// - or if foo() is non-null, but bar() returns null,
// - or if foo() and bar() are non-null, but baz() returns null.
// vice versa, return value is non-null if and only if foo(), bar() and baz() are non-null
foo()?.bar()?.baz()
```

`?:` = null coalescing operator. Binary operator returning first operand if non-null.<br>
  else... the second operand. (think defualting values, if one is not provided. Remember php laravel)<br>
Referred to as the 'Elvis Operator'<br>
EXAMPLE:<br>
```
fun sayHello(maybe: String?, neverNull: Int) {
    // use of Elvis operator
    val name: String = maybe ?: "stranger"
    println("Hello $name")
}
```

## Lambdas
Exists support for 'higher order functions' + 'anonymous functions' (or lambdas)<br>
```
// the following function takes a lambda, f, and executes f passing it the string "lambda"
// note that (String) -> Unit indicates a lambda with a String parameter and Unit return type
fun executeLambda(f: (String) -> Unit) {
    f("lambda")
}
```
They are declared using braces \{\}<br>
If a lambda takes params, they are declared within the braces and followed with the -> operator<br>
EXAMPLE:<br>
```
// the following statement defines a lambda that takes a single parameter and passes it to the println function
val l = { c : Any? -> println(c) }
// lambdas with no parameters may simply be defined using { }
val l2 = { print("no parameters") }
```

## Hello world
```
fun main() {
    println("Hello, world!")
    // Hello, world!
}
```
You may also find the following link useful, not quite as heavy as tour of rust, or tour of go.<br>
[Kotlin Tour](https://kotlinlang.org/docs/kotlin-tour-hello-world.html)<br>
This is worth diving into all in its own.<br>
Search up tour of Kotlin.<br>
Theres a beginner and intermediate course on there that should take you plenty far if you apply yourself.<br>

# Tools
(additional list)[https://en.wikipedia.org/wiki/List_of_Kotlin_software_and_tools]<br>
Android studio<br>
Emacs<br>
Eclipse (with plugin)<br>
IntelliJ IDEA (with plugin)<br>
Gradle (a build automation tool)<br>

# Kotlin Multiplatform
Single codebase: targets multiple platforms<br>
  windows, linux, web, android, IOS<br>
Multiplatform UI framewk based on Jetpack Compose.<br>
Jetpack Compose uses Kotlin compiler plugin to transform composable functions into UI elems.<br>
EXAMPLE: Text composable function displays text label on the screen.<br>

# Applications
When announced by Google 2017 May<br>
  It became the 3rd lang fully supported after Java and C++.<br>
As of 2020, it became the most WIDELY used on android, estimating 70%+ of the top 1k apps used it.<br>
Maps and Drive use Kotlin.<br>
Kotlin on android seen beneficial for its null-pointer safety + features that make for more readable code.<br>

Ktor = Jetbrains Kotlin first framewk (for server and client apps)<br>
Sprint framewk officially added Kotlin support with vers5<br>
Spring translated all docs to Kotlin + builtin support for many features such as coroutines.<br>

KOTLIN devs:<br>
56pc used for mobile apps<br>
47pc used for web back end<br>
>1/3 migrating to kotlin from another lang<br>
MOST targetting androud or on the JVM... 6pc using kotlin native.<br>

# Adoption
2018: FASTEST growing lang on github.<br>
4th most loved lang during 2020.<br>

## Orgs that have used Kotlin for backend dev:
Allegro, Amazon, Atlassian, Cash App, Flux, Google, Gradle, Jetbrains, Meshcloud, Norwegian Tax Admin, OLX, Pivotal, Rocket Travel, Shazam, Zalando<br>
## PRGS used Kotlin for web dev:
BaseCamp, Corda, Coursera, DripStat, Duolingo, Meta, Netflix, Pintrest, Trello, Uber<br>

# References
Find these at the bottom of the wiki page.<br>
Additional Reading:<br>
https://kotlinlang.org/docs/reference/js-overview.html<br>
https://adtmag.com/articles/2012/02/22/kotlin-goes-open-source.aspx<br>
https://www.jetbrains.com/lp/mobilecrossplatform/<br>
https://kotlinlang.org/foundation/kotlin-foundation.html<br>
https://kotlinlang.org/docs/components-stability.html<br>
https://kotlinlang.org/docs/js-overview.html#use-cases-for-kotlin-js<br>
https://www.jetbrains.com/kotlin-multiplatform/<br>
https://talkingkotlin.com/Using-Kotlin-for-backend-development-at-Flux/<br>
https://www.youtube.com/watch?v=K8XxaAba65g&list=PLQ176FUIyIUY6SKGl3Cj9yeYibBuRr3Hl&index=22<br>
https://www.infoq.com/news/2022/11/meta-port-java-kotlin/<br>
https://www.uber.com/blog/measuring-kotlin-build-performance/<br>
