# Kotlin vs. Swift

In this file I will be comparing and contrasting some of the differences between Swift and Kotlin

# **Purpose**

### **Why was the Language Created? What Problems was the Language trying to Address? Is the Language a Reaction to a previous Language or a replacement for another Langauge?**
* **Swift:**

Swift is a general-purpose, multi-paradigm, compiled programming language developed by Apple Inc. for iOS, macOS, watchOS, tvOS, and Linux. Swift is designed to work with Apple's Cocoa and Cocoa Touch frameworks and the large body of existing Objective-C (ObjC) code written for Apple products. It is built with the open source LLVM compiler framework and has been included in Xcode since version 6. On platforms other than Linux, it uses the Objective-C runtime library which allows C, Objective-C, C++ and Swift code to run within one program.

Swift incorporates a lot of aspects from modern languages and puts them into a single package.  It has the performance of a compiled language like C++, but the elegance of a modern language.  It solves the memory management problem with ARC. Without the performance issues of garbage collection.  And perhaps most importantly it can work with pre existing ObjC code. So programmers can exploit the existing libraries and codebase.

Apple created Swift to introduce a newer language that conforms to the modern methods of app developement. At the time that Swift was created ObjC was celebrating it's 30th year in existence. Swift is a reaction to ObjC. However Swift runs faster, Swift is easier to read and easier to learn than Objective-C,No pointers means Swift is ‘safer.’, Better memory management , and Swift has type inference       

* **Kotlin:** 

Kotlin is a general purpose, open source, statically typed “pragmatic” programming language for the JVM and Android that combines object-oriented and functional programming features. It is focused on interoperability, safety, clarity, and tooling support. 

Kotlin was created by JetBrains. After getting frustrated with some of its features. They saw features from other programming languages like Scala that they liked. However, Scala didn't have the desired compile time. So, Jetbrains decided to create Kotlin, and they wanted Kotlin to be compatible with Java so they did not need to rewrite applications that they had written in Java. Kotlin addresses several problems with Java including null safety, shorter syntax, support for functional programming, better comparison operators. Kotlin is more concice than Java, and it is estimated that Kotlin code can be 40% shorter than the same code written in Java. Kotlin also supports non-nullable types, which prevents null pointer exceptions. Kotlin is a reaction to Java. Except Kotlin has |Null references are controlled by the type system No raw types, Arrays in Kotlin are invariant, Kotlin has proper function types, as opposed to Java's SAM-conversions, Use-site variance without wildcards, and Kotlin does not have checked exceptions 

# **Unique Features of the Language**

### **Does the language have any particularly unique features?**

* **Swift**

Closures unified with function pointers
Null safety
Optionals
Tuples and Multiple return values 
Generics
Fast and Concise Iteration over a Range or Collection
Functional programming patterns.
Structs that support methods, extensions, protocols

**Generics**

Generic code enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define. You can write code that avoids duplication and expresses its intent in a clear, abstracted manner. 
```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```
The above function can be used with any type because it uses generics.
```swift 
var someInt = 3
var anotherInt = 107
swapTwoValues(&someInt, &anotherInt)
// someInt is now 107, and anotherInt is now 3
 
var someString = "hello"
var anotherString = "world"
swapTwoValues(&someString, &anotherString)
// someString is now "world", and anotherString is now "hello"
```


**Multiple Return Values**

In Swift, we can use tuples to return more than one element from a function. We use the tuple type as return type, and return a tuple:
```swift
func okStatus() -> (code: Int, name: String, hasBody: Bool) {
    return (200, "OK", true)
}
let status = okStatus()
println(status.name) // Prints "OK"
```

* **Kotlin** 

Null safety
Functional Programming

**Inter-operable with java**

Kotlin is designed with Java Interoperability in mind. Existing Java code can be called from Kotlin in a natural way, and Kotlin code can be used from Java rather smoothly as well. In this section we describe some details about calling Java code from Kotlin.

Pretty much all Java code can be used without any issues:
```kotlin
import java.util.*

fun demo(source: List<Int>) {
    val list = ArrayList<Int>()
    // 'for'-loops work for Java collections:
    for (item in source) {
        list.add(item)
    }
    // Operator conventions work as well:
    for (i in 0..source.size - 1) {
        list[i] = source[i] // get and set are called
    }
}
```

**High order function**

If your function accepts function as a parameter or returns function as a result than it’s called high order function. 
```kotlin
fun addValue(operation:(Int,Int) -> Int):Int {
    return operation(10,20)
}
addValue{num1,num2 -> num1 * num2} //This will print 200
addValue{num1,num2 -> num1 - num2} //This will print -10
```

**Defaulted parameters**

In Java, you often have to duplicate code in order to define different variants of a method or a constructor:
```java
public class OperatorInfoInJava {

    private final String uuid;
    private final String name;
    private final Boolean hasAccess;
    private final Boolean isAdmin;
    private final String notes;

    public OperatorInfoInJava(String uuid, String name, Boolean hasAccess, 
                              Boolean isAdmin, String notes) {
        this.uuid = uuid;
        this.name = name;
        this.hasAccess = hasAccess;
        this.isAdmin = isAdmin;
        this.notes = notes;
    }

    public OperatorInfoInJava(String uuid, String name) {
        this(uuid, name, true, false, "");
    }

    public OperatorInfoInJava(String name, Boolean hasAccess) {
        this(UUID.randomUUID().toString(), name, hasAccess, false, "");
    }
```
You can simply remove all of this when you switch to Kotlin by using default arguments.
```kotlin
class OperatorInfoInKotlin(val uuid: String = UUID.randomUUID().toString(),
                           val name: String,
                           val hasAccess: Boolean = true,
                           val isAdmin: Boolean = false,
                           val notes: String = "") {}
```
# Name spaces
## How the name spaces are implemented?
### Swift
Swift currently doesn't offer a direct solution to namespace types and constants within modules, however you can use structs or enums to simulate name spaces.
### Kotlin
In Kotlin packages are the closest analog of C# namespaces. You can define package with the **package** keyword in the beginning of the file.

## How the name spaces are used?
### Swift
```kotlin
struct API {
    static let BaseURL = "https://postmats.com/v1/"
    static let Token = "ddnlka"
}
```
```kotlin
enum API {
    static let BaseURL = "https://postmats.com/v1/"
    static let Token = "sd920dnn"
}
```
This solution is almost identical to the one that uses a struct. The main difference is you cannot create an instance of the **API** enum without having an error thrown at you.
### Kotlin
A source file may start with a package declaration:
```Swift
package food.bar

fun menu() {}

class Entree {}

// ...
```
All the contents (such as classes and functions) of the source file are contained by the package declared. So, in the example above, the full name of **baz()** is **menu.bar.baz**, and the full name of **Drink** is **Drink.bar.food**.

When a package is not specified, it is assigned as "default" package that has no name.

# **Types**

### **What types does the language support?**
* **Swift:** Use let to make a constant and var to make a variable.
```swift
let x=5 //constant
var y=5
```
The following types of basic data types are most frequently when declaring variables −
Int or UInt, Float, Double, Bool, String, Character, Optional, Tuples.

You can create a new name for an existing type using typealias. Here is the simple syntax to define a new type using typealias 
```swift
typealias newname = type
```

* **Kotlin:** Use val to make a constant and var to make a variable.
```kotlin
val x=5 //constant
var y=5
```
In Kotlin, all types are objects.
The basic data types available in Kotlin are:
Long, Int, Short, Byte, Double, Float, Char, Boolean. 
Every number type supports the following conversions:
toByte(): Byte, toShort(): Short, toInt(): Int, toLong(): Long, toFloat(): Float, toDouble(): Double, toChar(): Char. For example:
```kotlin
var x: Long=5
var y: Int=x.toInt()
```
Strings: 
Strings are represented by the type String. Strings are immutable. Elements of a string are characters that can be accessed by the indexing operation: s[i]. A string can be iterated over with a for-loop

### **Are both reference and value types supported?**
* **Swift:** Yes, types in Swift fall into one of two categories: first, “value types”, where each instance keeps a unique copy of its data, usually defined as a struct, enum, or tuple. The second, “reference types”, where instances share a single copy of the data, and the type is usually defined as a class. 
```swift
// Value type example
struct S { var data: Int = -1 }
var a = S()
var b = a						// a is copied to b
a.data = 42						// Changes a, not b
println("\(a.data), \(b.data)")	// prints "42, -1"
```
```swift
// Reference type example
class C { var data: Int = -1 }
var x = C()
var y = x						// x is copied to y
x.data = 42						// changes the instance referred to by x (and y)
println("\(x.data), \(y.data)")	// prints "42, 42"
```
* **Kotlin:** Since all types are objects, Kotlin only supports reference types. 

### **Can new value types be created?**
* **Swift:** Swift offers built-in as well as user-defined data types. 
* **Kotlin:** New classes can be created but new value types cannot

# **Classes**

### **Defining**
* **Swift:** Use class followed by the class’s name to create a class.
```swift
Class classname{
}
```
* **Kotlin:** Classes in Kotlin are declared using the keyword class:
```kotlin
Class classname{
}
```
### **Creating new instances**
* **Swift:** Create an instance of a class by putting parentheses after the class name. We do not use the new keyword. 
```swift
var shape = Shape()
```
* **Kotlin:** Note that Kotlin does not have a new keyword. To create an instance of a class, we call the constructor as if it were a regular function:
```kotlin
val invoice = Invoice()

val customer = Customer("Joe Smith")
```
### **Constructing/initializing**
* **Swift:** Use init to create a constructor inside a class.
```swift
class Polygon {
    var numberOfSides: Int = 0
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides.
    }
}
```
* **Kotlin:** A class in Kotlin can have a primary constructor and one or more secondary constructors. The primary constructor is part of the class header: it goes after the class name (and optional type parameters).
```kotlin
class Pet constructor(Name: String) {
}
```
If the primary constructor does not have any annotations or visibility modifiers, the constructor keyword can be omitted:
```kotlin
class Pet(Name: String) {
}
```
Secondary Constructors:
The class can also declare secondary constructors, which are prefixed with constructor:
```kotlin
class Person {
    constructor(parent: Person) {
        parent.children.add(this)
    }
}
```
### **Destructing/de-initializing**
* **Swift:**
Use deinit to create a deinitializer if you need to perform some cleanup before the object is deallocated.

* **Kotlin:**
Kotlin currently does not have a way to deinitialize objects.

# **Instance reference name in data type**
* **Swift**
Every instance of a type has an implicit property called self, which is exactly equivalent to the instance itself. You use the self property to refer to the current instance within its own instance methods. For example:

```swift
func increment() {
    self.count += 1
}
```

* **Kotlin:**
In Kotlin this refers to the current object of that class. For example:
```kotlin
fun increment() {
    this.count += 1
}
```
# **Properties**

## **Swift**

#### **Computed vs Stored**

In Swift properties have two categories, stored properties and computed properties.
In general, a property is defined as a value that associates with a particular class, structure, or enumeration.
Stored properties store constant and variable values to a defined instance where as a computer property will calculate the value.

#### **Stored Properties**

Stored properties are either a constant or a variable that is stored as part of an instance the two ways to do that are by the var and let keyword.

```swift
var example1: int //stored as variable
let example2: int //stored as constant
```

These properties function just like a normal constant or variable would in any other language holding the value it is assigned to at that instance.

 #### **Computed Properties**
 
 Computed properties are very similar to stored properties except when they are referred to they do not actual store value but instead calculate and provide a getter function and an optional setter function to the property.
  
  ```swift
  struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
                  size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
square.center = Point(x: 15.0, y: 15.0)
print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// Prints "square.origin is now at (10.0, 10.0)"
```
The documentation provided by apple explains how a computed property works extremely well.  As you can see in this example the struct rect has a computed property for its center where it takes in the other information and computes at runtime.  It uses getters and setters to be able to update and change with in an instant and allows for dynamic functionality and applications to be able to react to state and data changes and to not be static or constant.


## **Kotlin**

Properties and Kotlin are differentiated by two keywords var which defines a mutable or can be changed property or with val which defines a read only property.

```kotlin
var name: String =
var score: Int? =
val speed: Double =
```

For val type properties a default getter is constructed on initialization but does not allow for a setter since these properties are read only

```kotlin
val simple: Int? // has type Int, default getter, must be initialized in constructor
val inferredType = 1 // has type Int and a default getter
```

For a default var property a getter and setter are initialized by default but for a var? property they are implied but must be implemented by the programmer.

```kotlin
var allByDefault: Int? // error: explicit initializer required, default getter and setter implied
var initialized = 1 // has type Int, default getter and setter
```

Kotlin does allow for manipulation of the getter and setter functions which allows you to add or remove functionality from the default getter and setter provided by the language.

```koltin
var stringRepresentation: String
    get() = this.toString()
    set(value) {
        setDataFromString(value) // parses the string and assigns values to other properties
    }
```

#### **Backing Properties**

Kotlin does allow for a backing property similar to Java so you can manipulate and access public and private properties over many methods.  The way this is implemented is shown below.

```kotlin
private var _table: Map<String, Int>? = null
public val table: Map<String, Int>
    get() {
        if (_table == null) {
            _table = HashMap() // Type parameters are inferred
        }
        return _table ?: throw AssertionError("Set to null by another thread")
    }
    
# Interfaces & Protocols
## What does the language support?
##### Swift: Protocols
##### Kotlin: Interfaces
## What abilities does it have?
### Swift
* A protocol can have type methods or instance methods.
* Methods are declared in exactly the same way as for normal instance and type methods, but without curly braces or a method body.
* Variadic parameters are allowed.
* Default values are not allowed.
* A protocol can inherit one or more other protocols.
* Protocols support mutating methods: methods that are allowed to modify the instance it belongs to and any properties of that instance
* Protocols can have specific initializers like normal methods which the confirming types can implement.
* You can limit protocol adoption to class types (and not structures or enumerations) by adding the *AnyObject* or *class* protocol to a protocol’s inheritance list.
### Kotlin
* Two or more interfaces can be implemented in the same class.
* A class can implement as many interfaces as you want, but it can only extend a single class (similar to Java).
* The override modifier is compulsory in Kotlin—unlike in Java. 
* Along with methods, we can also declare properties in a Kotlin interface. 
* A Kotlin interface method can have a default implementation (similar to Java 8). 

## How is it used?
### Swift
A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be *adopted* by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to *conform* to that protocol.

They list off the function prototypes and variable declarations, as well as stating whether they are required or optional, but don’t actually do anything.  It is up to class, structs, or enumerations that claim to conform to the protocol to actually provide the functionality.
```Swift
protocol SomeProtocol {
    // protocol definition goes here
}
```

A problem is to decide when to use a protocol to class inheritance. The best cheat to determine when to use a protocol compare to class inheritance is to know when the type of relationship that determine between your classes. Is it an IS-A relationship or a HAS-A.

IS-A relationship is a type of relationship where a child will have every thing the parent has as well as have additional properties. A good example is an Airplane and a JetPlane. A JetPlane is basically an Airplane with additional properties / methods

HAS-A relationship is a type of relationship where two classes are not the same but share similar properties / method. A good example is a Bird and an Airplane. A Bird can fly as well as an Airplane. This is the best time to use a protocol.
```Swift
protocol Farm {
  func farm() -> String
}

class Pig: Farm {
  
  func farm() -> String {
    return ("Pigs live on the farm")
  }
  
}

class Bird: Farm {
  
  func farm() -> String {
    return ("Chickens live on the farm too")
  }
  
}
```
### Kotlin
Interfaces in Kotlin is similar to Java. They can contain declarations of abstract methods, as well as method implementations. What makes them different from abstract classes is that interfaces cannot store state. They can have properties but these need to be abstract or to provide accessor implementations.
```Kotlin
interface MyInterface {
    val prop: Int // abstract

    val propertyWithImplementation: String
        get() = "menu"

    fun Menu() {
        print(prop)
    }
}

class Child : MyInterface {
    override val prop: Int = 29
}
```
# Inheritance and Extension

## Swift
A class can inherit methods, properties, and other characteristics from another class. When one class inherits from another, the inheriting class is known as a subclass, and the class it inherits from is known as its superclass. Inheritance is a fundamental behavior that differentiates classes from other types in Swift.

Classes in Swift can call and access methods, properties, and subscripts belonging to their superclass and can provide their own overriding versions of those methods, properties, and subscripts to refine or modify their behavior. Swift helps to ensure your overrides are correct by checking that the override definition has a matching superclass definition.

Classes can also add property observers to inherited properties in order to be notified when the value of a property changes. Property observers can be added to any property, regardless of whether it was originally defined as a stored or computed property.

Subclassing is the act of basing a new class on an existing class. The subclass inherits characteristics from the existing class, which you can then refine. You can also add new characteristics to the subclass.

To indicate that a subclass has a superclass, write the subclass name before the superclass name, separated by a colon:
```Swift
class SomeSubclass: SomeSuperclass {
    // subclass definition goes here
}
```
#### Overriding
A subclass can provide its own custom implementation of an instance method, type method, instance property, type property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.

To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the override keyword. Doing so clarifies that you intend to provide an override and have not provided a matching definition by mistake. Overriding by accident can cause unexpected behavior, and any overrides without the override keyword are diagnosed as an error when your code is compiled.

The override keyword also prompts the Swift compiler to check that your overriding class’s superclass (or one of its parents) has a declaration that matches the one you provided for the override. This check ensures that your overriding definition is correct.

##### Accessing Superclass Methods, Properties, and Subscripts
When you provide a method, property, or subscript override for a subclass, it is sometimes useful to use the existing superclass implementation as part of your override. For example, you can refine the behavior of that existing implementation, or store a modified value in an existing inherited variable.

Where this is appropriate, you access the superclass version of a method, property, or subscript by using the super prefix:

* An overridden method named someMethod() can call the superclass version of someMethod() by calling super.someMethod() within the overriding method implementation.

* An overridden property called someProperty can access the superclass version of someProperty as super.someProperty within the overriding getter or setter implementation.

* An overridden subscript for someIndex can access the superclass version of the same subscript as super[someIndex] from within the overriding subscript implementation.

##### Overriding Methods
You can override an inherited instance or type method to provide a tailored or alternative implementation of the method within your subclass.

The following example defines a new subclass of Vehicle called Train, which overrides the makeNoise() method that Train inherits from Vehicle:
```Swift
class Train: Vehicle {
    override func makeNoise() {
        print("Choo Choo")
    }
}
```
If you create a new instance of Train and call its makeNoise() method, you can see that the Train subclass version of the method is called:
```Swift
let train = Train()
train.makeNoise()
// Prints "Choo Choo"
```
##### Overriding Properties
You can override an inherited instance or type property to provide your own custom getter and setter for that property, or to add property observers to enable the overriding property to observe when the underlying property value changes.

##### Overriding Property Getters and Setters
You can provide a custom getter (and setter, if appropriate) to override any inherited property, regardless of whether the inherited property is implemented as a stored or computed property at source. The stored or computed nature of an inherited property is not known by a subclass—it only knows that the inherited property has a certain name and type. You must always state both the name and the type of the property you are overriding, to enable the compiler to check that your override matches a superclass property with the same name and type.

You can present an inherited read-only property as a read-write property by providing both a getter and a setter in your subclass property override. You cannot, however, present an inherited read-write property as a read-only property.

**NOTE**
If you provide a setter as part of a property override, you must also provide a getter for that override. If you don’t want to modify the inherited property’s value within the overriding getter, you can simply pass through the inherited value by returning super.someProperty from the getter, where someProperty is the name of the property you are overriding.
*****

The following example defines a new class called Car, which is a subclass of Vehicle. The Car class introduces a new stored property called gear, with a default integer value of 1. The Car class also overrides the description property it inherits from Vehicle, to provide a custom description that includes the current gear:
```Swift
class Car: Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}
```
The override of the description property starts by calling super.description, which returns the Vehicle class’s description property. The Car class’s version of description then adds some extra text onto the end of this description to provide information about the current gear.

If you create an instance of the Car class and set its gear and currentSpeed properties, you can see that its description property returns the tailored description defined within the Car class:
```Swift
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```
## Kotlin
All classes in Kotlin have a common superclass Any, that is the default superclass for a class with no supertypes declared:

```Kotlin
class Example // Implicitly inherits from Any
```
Code in a derived class can call its superclass functions and property accessors implementations using the super keyword:

```Kotlin
open class Foo {
    open fun f() { println("Foo.f()") }
    open val x: Int get() = 1
}

class Bar : Foo() {
    override fun f() { 
        super.f()
        println("Bar.f()") 
    }
    
    override val x: Int get() = super.x + 1
}
```
If the derived class has a primary constructor, the base class can (and must) be initialized right there, using the parameters of the primary constructor.

If the class has no primary constructor, then each secondary constructor has to initialize the base type using the super keyword, or to delegate to another constructor which does that. Note that in this case different secondary constructors can call different constructors of the base type:

```Kotlin
class MyView : View {
    constructor(ctx: Context) : super(ctx)

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
}
```

#### Overriding Methods
As we mentioned before, we stick to making things explicit in Kotlin. And unlike Java, Kotlin requires explicit annotations for overridable members (we call them open) and for overrides:
```Kotlin
open class Base {
    open fun v() {}
    fun nv() {}
}
class Derived() : Base() {
    override fun v() {}
}
```

The override annotation is required for Derived.v(). If it were missing, the compiler would complain. If there is no open annotation on a function, like Base.nv(), declaring a method with the same signature in a subclass is illegal, either with override or without it. In a final class (e.g. a class with no open annotation), open members are prohibited.

A member marked override is itself open, i.e. it may be overridden in subclasses. If you want to prohibit re-overriding, use final:
```Kotlin
open class AnotherDerived() : Base() {
    final override fun v() {}
}
```

#### Overriding Properties
Overriding properties works in a similar way to overriding methods; properties declared on a superclass that are then redeclared on a derived class must be prefaced with override, and they must have a compatible type. Each declared property can be overridden by a property with an initializer or by a property with a getter method.
```Kotlin
open class Foo {
    open val x: Int get() { ... }
}

class Bar1 : Foo() {
    override val x: Int = ...
}
```

You can also override a val property with a var property, but not vice versa. This is allowed because a val property essentially declares a getter method, and overriding it as a var additionally declares a setter method in the derived class.

Note that you can use the override keyword as part of the property declaration in a primary constructor.
```Kotlin
interface Foo {
    val count: Int
}

class Bar1(override val count: Int) : Foo

class Bar2 : Foo {
    override var count: Int = 0
}
```
#### Calling the superclass implementation
Code in a derived class can call its superclass functions and property accessors implementations using the super keyword:
```Kotlin
open class Foo {
    open fun f() { println("Foo.f()") }
    open val x: Int get() = 1
}

class Bar : Foo() {
    override fun f() { 
        super.f()
        println("Bar.f()") 
    }
    
    override val x: Int get() = super.x + 1
}
```
# Reflection

## Swift
Reflection is something that you normally don’t use with statically typed languages like Swift. However, reflection support has been present since Swift 2, offering a read-only access to the properties of an instance, and, although still very limited (you can’t access computed properties and functions with it), it finds application in some cases.

Swift reflection should rather be called *introspection*, as its current functionality allows us to look at the objects’ properties without modifying them. The concept is represented by **Mirror structure**. The API’s overview explicitly states it’s focused on a particular instance rather than on type. Let’s explore what’s available.

A mirror describes the parts that make up a particular instance, such as the instance’s stored properties, collection or tuple elements, or its active enumeration case. Mirrors also provide a “display style” property that suggests how this mirror might be rendered.

Playgrounds and the debugger use the **Mirror** type to display representations of values of any type. For example, when you pass an instance to the dump(_:_:_:_:) function, a mirror is used to render that instance’s runtime contents.
```swift
struct Point {
    let x: Int, y: Int
}

let p = Point(x: 21, y: 30)
print(String(reflecting: p))
// Prints "▿ Point
//           - x: 21
//           - y: 30"
```

## Kotlin
Kotlin makes functions and properties first-class citizens in the language, and introspecting them (i.e. learning a name or a type of a property or function at runtime) is closely intertwined with simply using a functional or reactive style.

### Class References
The most basic reflection feature is getting the runtime reference to a Kotlin class. To obtain the reference to a statically known Kotlin class, you can use the class literal syntax:
```kotlin
val c = MyClass::class
```
The reference is a value of type KClass.
### Bound Class References
You can get the reference to a class of a specific object with the same ::class syntax by using the object as a receiver:
```kotlin
val widget: Widget = ...
assert(widget is GoodWidget) { "Bad widget: ${widget::class.qualifiedName}" }
```
You obtain the reference to an exact class of an object, for instance GoodWidget or BadWidget, despite the type of the receiver expression (Widget).
### Callable references
References to functions, properties, and constructors, apart from introspecting the program structure, can also be called or used as instances of function types.

The common supertype for all callable references is KCallable<out R>, where R is the return value type, which is the property type for properties, and the constructed type for constructors.
#### Function References
When we have a named function declared like this:

fun isOdd(x: Int) = x % 2 != 0
We can easily call it directly (isOdd(5)), but we can also use it as a function type value, e.g. pass it to another function. To do this, we use the :: operator:

```kotlin
val numbers = listOf(1, 2, 3)
println(numbers.filter(::isOdd))
```
Here ::isOdd is a value of function type (Int) -> Boolean.
### Property References
To access properties as first-class objects in Kotlin, we can also use the :: operator:

```kotlin
val x = 1

fun main(args: Array<String>) {
    println(::x.get())
    println(::x.name) 
}
```

The expression ::x evaluates to a property object of type KProperty<Int>, which allows us to read its value using get() or retrieve the property name using the name property. For more information, please refer to the docs on the KProperty class.
### Interoperability With Java Reflection
On the Java platform, standard library contains extensions for reflection classes that provide a mapping to and from Java reflection objects (see package kotlin.reflect.jvm). For example, to find a backing field or a Java method that serves as a getter for a Kotlin property, you can say something like this:
```kotlin
import kotlin.reflect.jvm.*
 
class A(val p: Int)
 
fun main(args: Array<String>) {
    println(A::p.javaGetter) // prints "public final int A.getP()"
    println(A::p.javaField)  // prints "private final int A.p"
}
```
To get the Kotlin class corresponding to a Java class, use the .kotlin extension property:
```kotlin
fun getKClass(o: Any): KClass<Any> = o.javaClass.kotlin
  
  # Memory Management

## **Kotlin**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kotlin uses the same memory management that Java uses or any other JVM like language uses.  With this it comes with the same garbage collection system that Java uses as well.  This provides a semi safe runtime environment that should usually be without memory leaks.  Although the garbage collection system catches most unused references memory leaks can still occur.  The best way to prevent this in Kotlin is to make sure you still set references to null once you are done using them.  The reason the Kotlin memory management system almost identically reflects Java's memory management is to allow for easy code transfer between languages since Kotlin is the successor to Java.

#### **Kotlin/Native**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In Kotlin/Native the newer platform developed by jet brains to allow Kotlin to run on many modern applications.  In this platform automatic reference counting is planned to be implemented to address the Null pointer issue that many java applications can run into.  With this it will remove the garbage collector similar to the JVM and will handle memory management in a similar way as Swift.

  
## **Swift**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Swift handles memory management through a proccess called ARC or Automatic Reference Counting.  This process allows for easy memory management for the programmer because Swift will do deallocates and allocates for you.  Swift will not deallocate an object unless it leaves the scope that it is contained in.

**For Example:**
```swift
let test = Test(number: 1)   // Will not be deallocated until main program is over

vs

while(counter!= 2){
  let test = Test(number: 1)  // Will be deallocated after the while loop is over
}
```
#### **The Process**
Objects in swift go through a 5 stage process after allocation.  The 5 steps are:

&nbsp;&nbsp; -Allocation (memory taken from stack or heap)

&nbsp;&nbsp; -Initialization (init code runs)

&nbsp;&nbsp; -Usage (the object is used)

&nbsp;&nbsp; -Deinitialization (deinit code runs)

&nbsp;&nbsp; -Deallocation (memory returned to stack or heap)

#### **The good**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The advantages of the ARC cycle is the developer does not have to worry about memory leaks because as soon as something leaves its scope the reference count will be updated for the current scope of the program.  With this as soon as the reference counter hits 0 Swift will automatically deinitalize the object and return the memory back to the stack or heap.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Swift’s automatic reference counting allows for easy garbage collection because as soon as the reference count hits 0 it will be marked as garbage and the memory will be returned.

#### **The Bad**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The ARC cycle has issues when multithreading occurs and objects are shared across many threads. Deinitalizing objects from multiple threads introduces a whole lot of complexity since the references are split across many threads and the ARC cycle has trouble tracking and keeping up with the references as some are dereferenced at the same time.

# **Comparisons of references and values**

### **How are values compared? (i.e. comparing two strings)**
* **Swift:** 

 Swift Comparison Operators: 
------------ 
Value Equal to (a == b)
Value Not equal to (a != b)
Reference Equal to (a===b)
Reference not Equal(a!==b)
Greater than (a > b)
Less than (a < b)
Greater than or equal to (a >= b)
Less than or equal to (a <= b)
Each of the comparison operators returns a Bool value to indicate whether or not the statement is true
```swift
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 is not equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 is not less than or equal to 1
```
String and character equality is checked with the “equal to” operator (==) and the “not equal to” operator (!=)
```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

* **Kotlin:** 

Kotlin Comparison Operators: 
------------ 
Value Equal to (a == b)
Value Not equal to (a != b)
Reference Equal to (a===b)
Reference not Equal(a!==b)
Greater than (a > b)
Less than (a < b)
Greater than or equal to (a >= b)
Less than or equal to (a <= b)

All comparison operators are translated to calls of compareTo which returns an Int. 
|a > b	    | a.compareTo(b) > 0
|a < b	    | a.compareTo(b) < 0
|a >= b	    | a.compareTo(b) >= 0
|a <= b	    | a.compareTo(b) <= 0

String and character equality is checked with the “equal to” operator (==) and the “not equal to” operator (!=)
```kotlin
val quotation = "We're a lot alike, you and I."
val sameQuotation = "We're a lot alike, you and I."
if (quotation == sameQuotation) {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```
# **Null/nil references**


### **Which does the language use? (null/nil/etc)**

* **Swift:** Swift uses nil

* **Kotlin** Kotlin uses null


### **Does the language have features for handling null/nil references?**

## **Swift:**

### Optional Chaining
Optional chaining is a process for querying and calling properties, methods, and subscripts on an optional that might currently be *nil*. If the optional contains a value, the property, method, or subscript call succeeds; if the optional is *nil*, the property, method, or subscript call returns *nil*. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is *nil*.

To reflect the fact that optional chaining can be called on a nil value, the result of an optional chaining call is always an optional value, even if the property, method, or subscript you are querying returns a nonoptional value. You can use this optional return value to check whether the optional chaining call was successful (the returned optional contains a value), or did not succeed due to a nil value in the chain (the returned optional value is *nil*).

Specifically, the result of an optional chaining call is of the same type as the expected return value, but wrapped in an optional. A property that normally returns an **Int** will return an **Int?** when accessed through optional chaining.

The next several code snippets demonstrate how optional chaining differs from forced unwrapping and enables you to check for success.

First, two classes called **Person** and **Residence** are defined:

```Swift
class Person {
    var residence: Residence?
}
 
class Residence {
    var numberOfRooms = 1
}
```
**Residence** instances have a single **Int** property called **numberOfRooms**, with a default value of 1. **Person** instances have an optional **residence** property of type **Residence?**.

If you create a new **Person** instance, its **residence** property is default initialized to *nil*, by virtue of being optional. In the code below, **john** has a **residence** property value of *nil*:

```Swift
let john = Person()
```

If you try to access the **numberOfRooms** property of this person’s **residence**, by placing an exclamation mark after **residence** to force the unwrapping of its value, you trigger a runtime error, because there is no **residence** value to unwrap:

```Swift
let roomCount = john.residence!.numberOfRooms
// this triggers a runtime error
```

The code above succeeds when **john.residence** has a non-*nil* value and will set **roomCount** to an **Int** value containing the appropriate number of rooms. However, this code always triggers a runtime error when **residence** is *nil*, as illustrated above.

Optional chaining provides an alternative way to access the value of **numberOfRooms**. To use optional chaining, use a question mark in place of the exclamation mark:

```Swift
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Unable to retrieve the number of rooms."
```

This tells Swift to “chain” on the optional **residence** property and to retrieve the value of **numberOfRooms** if **residence** exists.

Because the attempt to access **numberOfRooms** has the potential to fail, the optional chaining attempt returns a value of type **Int?**, or “optional **Int**”. When **residence** is *nil*, as in the example above, this optional **Int** will also be *nil*, to reflect the fact that it was not possible to access **numberOfRooms**. The optional **Int** is accessed through optional binding to unwrap the integer and assign the nonoptional value to the **roomCount** variable.

Note that this is true even though **numberOfRooms** is a nonoptional **Int**. The fact that it is queried through an optional chain means that the call to **numberOfRooms** will always return an **Int?** instead of an **Int**.

You can assign a **Residence** instance to **john.residence**, so that it no longer has a *nil* value:
```Swift
john.residence = Residence()
```

**john.residence** now contains an actual **Residence** instance, rather than *nil*. If you try to access **numberOfRooms** with the same optional chaining as before, it will now return an **Int?** that contains the default **numberOfRooms** value of 1:

```Swift
if let roomCount = john.residence?.numberOfRooms {
    print("Moe's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Moe's residence has 1 room(s)."
```
#### **Defining Model Classes for Optional Chaining**
You can use optional chaining with calls to properties, methods, and subscripts that are more than one level deep. This enables you to drill down into subproperties within complex models of interrelated types, and to check whether it is possible to access properties, methods, and subscripts on those subproperties.

The code snippets below define four model classes for use in several subsequent examples, including examples of multilevel optional chaining. These classes expand upon the **Person** and **Residence** model from above by adding a **Room** and **Address** class, with associated properties, methods, and subscripts.

The **Person** class is defined in the same way as before:
```Swift
class Person {
    var residence: Residence?
}
```
The **Residence** class is more complex than before. This time, the **Residence** class defines a variable property called **rooms**, which is initialized with an empty array of type **Room**:
```Swift
class Residence {
    var rooms = [Room]()
    var numberOfRooms: Int {
        return rooms.count
    }
    subscript(i: Int) -> Room {
        get {
            return rooms[i]
        }
        set {
            rooms[i] = newValue
        }
    }
    func printNumberOfRooms() {
        print("The number of rooms is \(numberOfRooms)")
    }
    var address: Address?
}
```
Because this version of **Residence** stores an array of **Room** instances, its **numberOfRooms** property is implemented as a computed property, not a stored property. The computed **numberOfRooms** property simply returns the value of the **count** property from the **rooms** array.

As a shortcut to accessing its **rooms** array, this version of **Residence** provides a read-write subscript that provides access to the room at the requested index in the **rooms** array.

This version of **Residence** also provides a method called **printNumberOfRooms**, which simply prints the number of rooms in the residence.

Finally, **Residence** defines an optional property called **address**, with a type of **Address?.** The **Address** class type for this property is defined below.

The **Room** class used for the **rooms** array is a simple class with one property called **name**, and an initializer to set that property to a suitable room name:
```Swift
class Room {
    let name: String
    init(name: String) { self.name = name }
}
```
The final class in this model is called **Address**. This class has three optional properties of type **String?**. The first two properties, **buildingName** and **buildingNumber**, are alternative ways to identify a particular building as part of an address. The third property, **street**, is used to name the street for that address:
```Swift
class Address {
    var buildingName: String?
    var buildingNumber: String?
    var street: String?
    func buildingIdentifier() -> String? {
        if let buildingNumber = buildingNumber, let street = street {
            return "\(buildingNumber) \(street)"
        } else if buildingName != nil {
            return buildingName
        } else {
            return nil
        }
    }
}
```
The **Address** class also provides a method called **buildingIdentifier()**, which has a return type of **String?**. This method checks the properties of the address and returns **buildingName** if it has a value, or **buildingNumber** concatenated with **street** if both have values, or *nil* otherwise.

## **Kotlin:**

Kotlin's type system is aimed to eliminate NullPointerExceptions from its code. The only possible causes of NPEs may be:

* An explicit call to throw **NullPointerException()**;
* Usage of the **!!** operator that is described below;
* Some data inconsistency with regard to initialization, such as when:
  * An uninitialized _**this**_ available in a constructor is passed and used somewhere ("leaking _**this**_");
  * A superclass constructor calls an open member whose implementation in the derived class uses uninitialized state;
* Java interoperation:
  * Attempts to access a member on a **null** reference of a platform type;
  * Generic types used for Java interoperation with incorrect nullability, e.g. a piece of Java code might add **null** into a Kotlin **MutableList<String>**, meaning that **MutableList<String?>** should be used for working with it;
  * Other issues caused by external Java code.


In Kotlin, the type system distinguishes between references that can hold _**null**_ (nullable references) and those that can not (non-null references). For example, a regular variable of type **String** can not hold _**null**_:

```kotlin
var a: String = "abc"
a = null // compilation error
```

To allow nulls, we can declare a variable as nullable string, written String?:
```kotlin
var b: String? = "abc"
b = null // ok
```
Now, if you call a method or access a property on a, it's guaranteed not to cause an NPE, so you can safely say:

```kotlin
val l = a.length
```
But if you want to access the same property on b, that would not be safe, and the compiler reports an error:
```kotlin
val l = b.length // error: variable 'b' can be null
```
### Checking for **null** in conditions:

#### 1. Explicitly check if **b** is *null*, and handle the two options separately:
```kotlin
val l = if (b != null) b.length else -1
```
The compiler tracks the information about the check you performed, and allows the call to length inside the if. More complex conditions are supported as well:
```kotlin
if (b != null && b.length > 0) {
    print("String of length ${b.length}")
} else {
    print("Empty string")
}
```
Note that this only works where b is immutable (i.e. a local variable which is not modified between the check and the usage or a member val which has a backing field and is not overridable), because otherwise it might happen that b changes to null after the check.
#### 2. Safe Calls --- the safe call operator, written **__?.__** :
```kotlin
b?.length
```
This returns **b.length** if **b** is *not null*, and *null* otherwise. The type of this expression is **Int?**.

Safe calls are useful in chains. For example, if Bob, an Employee, may be assigned to a Department (or not), that in turn may have another Employee as a department head, then to obtain the name of Bob's department head (if any), we write the following:

```kotlin
bob?.department?.head?.name
```
Such a chain returns null if any of the properties in it is null.

To perform a certain operation only for non-null values, you can use the safe call operator together with let:
```kotlin
val listWithNulls: List<String?> = listOf("A", null)
for (item in listWithNulls) {
     item?.let { println(it) } // prints A and ignores null
}
```
A safe call can also be placed on the left side of an assignment. Then, if one of the receivers in the safe calls chain is null, the assignment is skipped, and the expression on the right is not evaluated at all:
```kotlin
// If either `person` or `person.department` is null, the function is not called:
person?.department?.head = managersPool.getManager()
```
#### Elvis Operator

When we have a nullable reference __*r*__, we can say "if __*r*__ is not *null*, use it, otherwise use some non-null value __*x*__":
```kotlin
val l: Int = if (b != null) b.length else -1
```
Along with the complete if-expression, this can be expressed with the Elvis operator, written **__?.__**:
```kotlin
val l = b?.length ?: -1
```
If the expression to the left of **__?.__** is not null, the elvis operator returns it, otherwise it returns the expression to the right. Note that the right-hand side expression is evaluated only if the left-hand side is null.

Note that, since throw and return are expressions in Kotlin, they can also be used on the right hand side of the elvis operator. This can be very handy, for example, for checking function arguments:
```kotlin
fun foo(node: Node): String? {
    val parent = node.getParent() ?: return null
    val name = node.getName() ?: throw IllegalArgumentException("name expected")
    // ...
}
```
#### 3. The !! Operator
The third option is for NPE-lovers: the not-null assertion operator (**!!**) converts any value to a non-null type and throws an exception if the value is null. We can write **b!!**, and this will return a non-null value of **b** (e.g., a **String** in our example) or throw an NPE if **b** is *null*:
```kotlin
val l = b!!.length
```
Thus, if you want an NPE, you can have it, but you have to ask for it explicitly, and it does not appear out of the blue.

#### Safe Casts
Regular casts may result into a **ClassCastException** if the object is not of the target type. Another option is to use safe casts that return *null* if the attempt was not successful:

```kotlin
val aInt: Int? = a as? Int
```
#### Collections of Nullable Type
If you have a collection of elements of a nullable type and want to filter non-null elements, you can do so by using filterNotNull:
```kotlin
val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()
```
# **Errors and exception handling**
* **Swift:**

In Swift, errors are represented by values of types that conform to the Error protocol. This empty protocol indicates that a type can be used for error handling.

Swift enumerations are particularly well suited to modeling a group of related error conditions, with associated values allowing for additional information about the nature of an error to be communicated. For example, here’s how you might represent the error conditions of operating a vending machine inside a game:

```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

Throwing an error lets you indicate that something unexpected happened and the normal flow of execution can’t continue. You use a throw statement to throw an error. For example, the following code throws an error to indicate that five additional coins are needed by the vending machine:

```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```
Handling Errors Using Do-Catch:

You use a do-catch statement to handle errors by running a block of code. If an error is thrown by the code in the do clause, it is matched against the catch clauses to determine which one of them can handle the error.

Here is the general form of a do-catch statement:
```swift
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch {
    statements
}
```

* **Kotlin:**

All exception classes in Kotlin are descendants of the class Throwable. Every exception has a message, stack trace and an optional cause.

To throw an exception object, use the throw-expression:
```kotlin
throw MyException("Hi There!")
```

To catch an exception, use the try-expression:
```kotlin
try {
    // some code
}
catch (e: SomeException) {
    // handler
}
finally {
    // optional finally block
}
```
There may be zero or more catch blocks. 

try is an expression, i.e. it may have a return value and a try catch can be written as:

```kotlin
val a: Int? = try { parseInt(input) } catch (e: NumberFormatException) { null }
```
# **Errors and exception handling**
* **Swift:**

In Swift, errors are represented by values of types that conform to the Error protocol. This empty protocol indicates that a type can be used for error handling.

Swift enumerations are particularly well suited to modeling a group of related error conditions, with associated values allowing for additional information about the nature of an error to be communicated. For example, here’s how you might represent the error conditions of operating a vending machine inside a game:

```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

Throwing an error lets you indicate that something unexpected happened and the normal flow of execution can’t continue. You use a throw statement to throw an error. For example, the following code throws an error to indicate that five additional coins are needed by the vending machine:

```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```
Handling Errors Using Do-Catch:

You use a do-catch statement to handle errors by running a block of code. If an error is thrown by the code in the do clause, it is matched against the catch clauses to determine which one of them can handle the error.

Here is the general form of a do-catch statement:
```swift
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch {
    statements
}
```

* **Kotlin:**

All exception classes in Kotlin are descendants of the class Throwable. Every exception has a message, stack trace and an optional cause.

To throw an exception object, use the throw-expression:
```kotlin
throw MyException("Hi There!")
```

To catch an exception, use the try-expression:
```kotlin
try {
    // some code
}
catch (e: SomeException) {
    // handler
}
finally {
    // optional finally block
}
```
There may be zero or more catch blocks. 

try is an expression, i.e. it may have a return value and a try catch can be written as:

```kotlin
val a: Int? = try { parseInt(input) } catch (e: NumberFormatException) { null }
```

# **Lambda Expressions or Closures**


## **Swift**

In Swift, a lambda function is expressed as a closure.  The purpose of a closure is to allow for contained functionality to be easily transferred and used in your code. They contain many functions and interactions that are shorten and contained for easy reuse and interpretation.

#### **The 3 Forms**
There are three forms of closures. 

-Global functions are closures that have a name and do not capture any values.

-Nested functions are closures that have a name and can capture values from their enclosing function.

-Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

#### **Example**

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

In this example it shows how a closure can be used to change functionality of library function to do a desired task.  Here a backward function is defined as a closure and then sent to swift library sorted function but used as its parameter providing it with additional functionality.  This shows the benefit of closures and how it can extend functionality and allow for easy code reuse and manipulation.


## **Kotlin**

Kotlin like it predecessor, Java, used the term Lambda to define its form of functional programming.  The first key to Kotlin lambdas is to understand what a higher order function is.

#### **Higher order function**

Kotlin facilitates its lambda expressions through the use of higher order functions.  A higher order function is simiply a function that can take another function as its parameter.  This feature allows for the concept of a lambda expression to emerge.

#### **Lambda Expressions**

The definition of a lambda function is a function that takes in a function that is never declared but instead immediately sent to the calling function for direct use.

```kotlin
//Here is an example of a function that will compare two strings written as a traditional function

fun compare(a: String, b: String): Boolean = a.length < b.length

//Now we will convert it to a lambda using a higher order function

max(strings, { a, b -> a.length < b.length })

```

This example shows the benefit of a lambda reducing the length of your code will still implementing the same functionality and having the same readability.

# Implementation of Listeners and Event Handlers

### Swift
"Apps receive and handle events using responder objects. A responder object is any instance of the UIResponder class, and common subclasses include UIView, UIViewController, and UIApplication. Responders receive the raw event data and must either handle the event or forward it to another responder object. When your app receives an event, UIKit automatically directs that event to the most appropriate responder object, known as the first responder. Unhandled events are passed from responder to responder in the active responder chain, which is a dynamic configuration of your app’s responder objects. There is no single responder chain within your app. UIKit defines default rules for how objects are passed from one responder to the next, but you can always change those rules by overriding the appropriate properties in your responder objects.Figure 1 shows the default responder chains in an app whose interface contains a label, a text field, a button, and two background views. If the text field does not handle an event, UIKit sends the event to the text field’s parent UIView object, followed by the root view of the window. From the root view, the responder chain diverts to the owning view controller before directing the event to the window. If the window does not handle the event, UIKit delivers the event to the UIApplication object, and possibly to the app delegate if that object is an instance of UIResponder and not already part of the responder chain."

You can use property overriding to add property observers to an inherited property. This enables you to be notified when the value of an inherited property changes, regardless of how that property was originally implemented


### Kotlin
Event listeners/handlers are similar to those in Java. In Kotlin anonymous classes (lambdas can be used for these) and named classes can be used as listeners in Kotlin:
```Kotlin
cancelImage.setOnClickListener(object : View.OnClickListener { //1
    override fun onClick(v: View?) { // 2
        dismiss()
    }
})
```

```Kotlin
class OnCancelSnackListener(
    val snackbar: Snackbar
): View.OnClickListener {
    override fun onClick(v: View?) {
        snackbar.dismiss()
    }
}
```
Lambda expression example:
```Kotlin
cancelImage.setOnClickListener { dismiss() }

# **Singleton**

## **Swift**

Apple decided to inherit a lot of the concepts of how to singleton was designed in objective-c and implement it into Swift.  Their goal in the singleton was to provide a global access shared instance of an object.  With this it allows for the programmer to a create a unified access point for resources within their code.

#### **Implementation**

```swift
class Singleton {
    static let sharedInstance = Singleton()
}
///this is guaranteed to be lazily intiliazed once
```

In swift you can also manually do a lazy singleton to lessen the load since the idea behind lazy properties is they are not calculated until the first time they are used. 

```swift
class Singleton {
    static lazy let sharedInstance = Singleton()
    private init() {}
}
```

#### **Thread Safety**

Even though Swift makes singletons seem incredibly easy they leave a lot of information out on how to correctly write one. They do talk about thread safety and the way you implement a thread safe singleton is to wrap you code in a __dispatch_once__ block to ensure it while only execute once in its lifetime.

```swift
//Thread safe singelton
+ (instancetype)sharedInstance {
    static id _sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _sharedInstance = [[self alloc] init];
    });
 
    return _sharedInstance;
}
```

Learn how write singletons[blog post](https://krakendev.io/blog/the-right-way-to-write-a-singleton). 


## **Kotlin**

Kotlin does their form of a singleton in versions after Scala in a way called an __object declaration__.  With this they are very easy and are thread safe.  With object declaration it is implied that it is a lazy property and won't be calculated until execution.

```kotlin
object DataProviderManager {
    fun registerDataProvider(provider: DataProvider) {
        // ...
    }

    val allDataProviders: Collection<DataProvider>
        get() = // ...
}
```

# Procedural Programming
Procedural Programming takes on applications by solving problems from the top of the code down to the bottom.

A program following this programming technique breaks a problem down into smaller sub-problems or sub-procedures. These sub-procedures are continually broken down in the process called functional decomposition until the sub-procedure is simple enough to be solved.

The issue that is obvious in Procedural Programming is that if an edit is needed to the program, the developer must edit every line of code that corresponds to the original change in the code. 

## Swift
Swift does not support procedural programming.

## Kotlin
Although Kotlin is an OOP language, it also supports procedural programming. Kotlin functions and variables can be defined without placing them explicitly in classes. 

```Kotlin
val rectangle = mutableMapOf("Width" to 10, "Height" to 10, "Color" to "Red")
 
fun calcArea(shape : Map<String, Any>) : Int {
    return shape["Height"] as Int * shape["Width"] as Int
}
 
fun toString(shape : Map<String, Any>) : String {
    return "Width = ${shape["Width"]}, Height = ${shape["Height"]}, Color = ${shape["Color"]}, Area = ${calcArea(shape)}"
}
```
# **Functional Programming**

### **Does the language support functional programming?**
* **Swift:**

Swift does supports functional programming. 

Functional programming is a programming paradigm — a style of building the structure and elements of computer programs — that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

For Swift, functional programming means using lets instead of vars when dealing with data. This has its benefits, mainly that functional code is less prone to bugs and easier to understand than imperative code. Imperative programming is the opposite of functional programming — it’s a paradigm that uses statements that change a program’s state.

Imperative Approach:

```swift
let numbers = [1, 2, 3, 4, 5]
var evenNumbers = [Int]()
for i in 0..<numbers.count {
    let number = numbers[i]
    if number % 2 == 0 {
        evenNumbers.append(number)
    }
}
```
Functional Approach:
```swift
let evenNumbers = [1, 2, 3, 4, 5].filter { (number) -> Bool in
    if number % 2 == 0 {
        return true
    } else {
        return false
    }
}
```

OR

```swift
let evenNumbers = [1, 2, 3, 4, 5].filter { $0 % 2 == 0 }
```

* **Kotlin:**

Kotlin also supports functional programming. A combination of lambda expression and the Kotlin library makes our life easier when working with collections. For example a program that takes an array and keeps only the positive numbers can be written as:

```kotlin
val numbers = arrayListOf(10 ,5 , -9, 9, 11, 5, -6)
val nonNegative = numbers.filter { it >= 0}

println(nonNegative) // [10, 5, 9, 11, 5]

# **Multithreading**

## **Swift**

Swift contains thread like abilities similar to many other languages.  The goal for Apple in their development of Swift was to make sure that applications can have multiple paths of execution that can run at the same time as the main thread.  The benefits of multithreading is it can improve an applications perceived response time and can also can benefit the application's real time performance.

#### **Multitasking and Concurrency**

Multitasking and concurrency can be essential to a well run application but it comes with its positives and negatives. Having multitasking occurring in your application allows for more functionality to be available to the user at a touch of a button.  The downside of implementing this feature is synchronization has be to exact and perfect or a concurrent program will not function correctly at all.  The way Swift implements these features is through the old objC way.


Swift allows it to do it through concurrent programing with GCD.


## **Kotlin**

In Kotlin the term for multithreading is __coroutines__.  The difference of a coroutine from your standard thread is it allows provides a way to avoid block a thread and instead implements a suspension feature.

#### **Suspension**

The idea behind implementing a suspension is when you have to block a thread it usually expensive and can cause a lot of stress in a high load operation.  When using a suspension the work load is almost free and does not stress the system.  They are easy to implement and their functionality can be user controlled by libraries. 

##### **Example**

```kotlin
fun main(args: Array<String>) {
    doSomething() // ERROR: Suspending function called from a non-coroutine context 
    
    async { 
        ...
        computations.forEach { // `forEach` is an inline function, the lambda is inlined
            it.await() // OK
        }
            
        thread { // `thread` is not an inline function, so the lambda is not inlined
            doSomething() // ERROR
        }
    }
}

/// how a suspension function is declared
suspend fun doSomething(foo: Foo): Bar {
    ...
}
```

Many API's implement suspension of coroutines for Kotlin allowing for easy implementation and all that is required is a slight tweaking to get the functionality you want out of the coroutine.



