---
description: A comprehensive guide to mastering C# for developers with Python and TypeScript backgrounds.
author: Your Name/Handle # Placeholder for author
version: 1.0 # Placeholder for version
category: "General Development"
globs: ["**/*.cs"] # Relevant for C# files
tags: ["csharp", ".net", "guide", "programming-language", "typescript-transition", "python-transition"]
---
A Comprehensive Guide to Mastering C# for Python and TypeScript Developers
This guide is designed for proficient software engineers with a background in Python and TypeScript who are looking to achieve an expert level of understanding and capability in C#. It delves into the core paradigms of C#, its rich feature set, and the intricacies of the.NET ecosystem, highlighting common "gotchas" and providing strategies for a smooth transition.
1. Introduction: Bridging from TypeScript/Python to C#
Transitioning from dynamically or structurally typed languages like Python and TypeScript to a statically and nominally typed language such as C# involves more than learning new syntax. It necessitates a shift in architectural thinking, a deeper comprehension of compile-time versus runtime behaviors, and an appreciation for the.NET ecosystem's design philosophies, particularly concerning type safety, memory management, and concurrency.
1.1. C# as a Statically-Typed, Nominally-Typed Language: Core Paradigm Shifts
C# is fundamentally a statically typed language, meaning that the type of every variable and expression is known at compile time.1 This contrasts sharply with Python, which is dynamically typed, where type checking occurs primarily at runtime.1 TypeScript, while adding a layer of static typing to JavaScript, employs a structural type system that is generally less strict than C#'s nominal system.4 In a nominal system, type compatibility is determined by explicit declarations and names; for two types to be compatible, one must typically inherit from or implement the other, or they must be the same named type. Structural typing, as in TypeScript, determines compatibility based on the "shape" or structure of the types—if an object possesses the required properties and methods, it's considered compatible, regardless of its declared name.
This distinction is a primary conceptual hurdle. The static typing in C# allows the compiler to catch a wide array of type-related errors before the program is ever run, contributing significantly to the robustness and maintainability of large-scale applications.1 Developers accustomed to the runtime flexibility of Python or the structural flexibility of TypeScript will need to adapt to a more disciplined approach of defining types explicitly and early in the development process. This upfront type definition is not merely a syntactic requirement; it is a core design principle in C# that underpins its powerful tooling, facilitates safer refactoring, and enables performance optimizations due to the wealth of information available to the compiler. The development workflow in C# thus encourages more deliberation on type design before writing implementation code, rather than discovering type mismatches or inconsistencies at runtime.
The emphasis on static and nominal typing in C# profoundly influences the design of its ecosystem and libraries. APIs within the.NET framework and third-party C# libraries are typically constructed with strong contracts, often defined by interfaces and explicit class hierarchies. This results in a different experience when consuming libraries compared to Python, where duck typing (if it walks like a duck and quacks like a duck, it's a duck) is prevalent, or TypeScript, where structural compatibility often suffices. Developers transitioning to C# will find that an object cannot simply "look like" what a method expects; it must be of the expected nominal type or implement the required interface. This necessitates a learning curve focused on understanding.NET's interface-driven design patterns and the importance of explicit type conformance, which ultimately leads to more predictable and maintainable integrations.
1.2. Overview of the.NET Ecosystem
.NET is a comprehensive developer platform comprising tools, programming languages (with C# being the most prominent), and an extensive set of libraries.6 At its core are two major components: the Common Language Runtime (CLR) and the Base Class Library (BCL) (formerly known as the.NET Framework Class Library).6 The CLR serves as the execution engine, providing essential services such as automatic memory management (garbage collection), type safety, exception handling, and thread management.6 The BCL offers a vast collection of pre-built functionalities, ranging from basic data types and collections to networking, file I/O, and more.6
To ensure API consistency across different.NET implementations (like.NET Framework,.NET (Core), and Xamarin),.NET Standard was introduced as a formal specification of.NET APIs.7 Modern.NET (which evolved from.NET Core) is a significant advancement: it is cross-platform (running on Windows, Linux, and macOS), open-source, and represents the current focus of innovation within the.NET ecosystem. This is distinct from the older, Windows-only.NET Framework.7 Understanding these foundational components is crucial for any developer aiming to leverage the full power of the.NET platform.
For developers coming from Python, with its "batteries-included" standard library and the extensive Python Package Index (PyPI) 1, the BCL and NuGet (C#'s package manager 4) fulfill analogous roles. However, the.NET ecosystem tends to be more integrated and, for core functionalities, often provides a Microsoft-stewarded (though modern.NET is open-source) solution. TypeScript developers, accustomed to the npm ecosystem and the often-fragmented JavaScript library landscape, may find.NET's BCL more comprehensive and opinionated. The BCL provides a large, coherent set of libraries directly with the runtime, offering a consistent "Microsoft-blessed" approach for many common tasks. This can be advantageous in terms of consistency and support, though it might offer less variety for certain niche functionalities compared to PyPI. Consequently, Python developers will need to adjust their library discovery process, typically looking first to the BCL and then to NuGet for third-party packages. TypeScript developers might find the.NET ecosystem more centrally managed, which can simplify dependency management and ensure a baseline level of quality and interoperability among libraries.
1.3. Setting Up Your C# Development Environment
A robust development environment is key to productivity. For C# and.NET development, Microsoft offers Visual Studio, a full-featured Integrated Development Environment (IDE) 7, and supports Visual Studio Code (VS Code) as a powerful, lightweight alternative, particularly when augmented with the C# Dev Kit extension.13 Regardless of the chosen editor, the.NET Software Development Kit (SDK) is essential. The SDK includes the.NET Command Line Interface (CLI), the.NET runtime, and the necessary libraries to build and run.NET applications.13
Visual Studio is often the preferred choice for large, complex C# projects, especially those targeting Windows-specific frameworks, due to its rich set of integrated tools for debugging, profiling, and UI design. VS Code, coupled with the C# Dev Kit, provides a modern, cross-platform development experience that is gaining popularity. The C# Dev Kit for VS Code is a suite of extensions that includes the base C# language service, an extension for solution management, project templates, and integrated testing and debugging capabilities, and an optional IntelliCode extension for AI-assisted development.13 This aims to bring Visual Studio-level productivity to the VS Code environment. This means developers accustomed to VS Code from their Python or TypeScript work can transition to C# with a familiar editor, although Visual Studio may still offer more advanced features for certain specialized.NET workloads.
Getting Started:
Install the.NET SDK: Download and install the latest.NET SDK from the official.NET website.13 This will provide the dotnet CLI tool. The SDK components include the.NET CLI, the.NET runtime and libraries, and the dotnet driver program.16
Choose and Configure Your IDE:
Visual Studio Code: Install VS Code, then install the "C# Dev Kit" extension from the VS Code Marketplace.13 This kit often includes the base C# extension and other tools for a comprehensive experience.
Visual Studio: Download and run the Visual Studio Installer. During installation, select appropriate workloads such as ".NET desktop development" for console or desktop applications, or "ASP.NET and web development" for web projects.12
Create a "Hello World" Application: Open a terminal or command prompt and run the following.NET CLI command to create a new console application 13:
Bash
dotnet new console -o MyFirstApp
cd MyFirstApp
dotnet run
This will create a simple C# application and execute it, printing "Hello, World!" to the console.
2. C# Language Fundamentals Revisited for Experts
While many C# syntax elements will feel familiar to Python and TypeScript developers due to their common C-family heritage, a deeper understanding of C#'s specific implementations and type system is crucial for mastery.
2.1. Syntax Deep Dive: Beyond the Basics
C# syntax employs curly braces {} for defining code blocks and semicolons ; to terminate statements, a structure familiar to TypeScript developers.4 Identifiers in C# are case-sensitive. The traditional entry point for a C# application is a static Main method within a class, which can also be asynchronous (async Task Main()).18 Since C# 9.0, top-level statements are supported, allowing for simpler program structures, especially for smaller applications or scripts, by omitting the explicit Program class and Main method declaration.18 Namespaces are used to organize code and prevent naming conflicts, similar to packages in Java or modules in Python.18
Python developers must make a significant adjustment from Python's indentation-based scoping to C#'s brace-delimited blocks and explicit semicolon statement terminators.1 While C# coding conventions advocate for indentation for readability, it is not syntactically enforced as it is in Python. TypeScript developers will generally find C#'s syntax familiar but may perceive it as stricter in its parsing and type rules.4
The introduction of top-level statements in C# 9.0 18 significantly lowers the barrier to entry for simple programs and scripts. Python developers, accustomed to writing executable code directly at the top level of a .py file, will find this feature makes initial C# exploration more intuitive. Instead of the traditional ceremony of class Program { static void Main(string args) {... } }, one can now write directly:

C#


// Contained in Program.cs (by convention)
using System;

Console.WriteLine("Hello from a top-level statement!");
MyClass.MyMethod();

public class MyClass
{
    public static void MyMethod() => Console.WriteLine("MyMethod called");
}


This reduces boilerplate for small console applications and scripts, allowing a more direct transition for developers used to Python's scripting capabilities.
2.2. The C# Type System In-Depth
The C# type system is a cornerstone of the language, characterized by its strong, static, and nominal nature. Understanding its intricacies is paramount.
2.2.1. Value Types vs. Reference Types
C# categorizes all types into two fundamental kinds: value types and reference types.20
Value Types: Variables of value types directly contain their data. Common value types include primitive types like int, float, bool, char, decimal, all struct types, and enum types.21 When a value type variable is assigned to another, the data is copied. Value types implicitly inherit from System.ValueType, which in turn inherits from System.Object.21
Reference Types: Variables of reference types store a reference (similar to a pointer or memory address) to the actual data, which resides on the heap. Common reference types include class types, interface types, delegate types, array types, and the built-in string and object types.20 When a reference type variable is assigned to another, only the reference is copied, not the underlying object. Both variables then point to the same object in memory.
This distinction is fundamental and has profound implications for memory allocation, data manipulation, parameter passing, and null handling. Python developers, accustomed to a model where all variables are essentially references to objects, must internalize this difference. For instance, assigning one struct variable to another creates an independent copy of the data, whereas in Python, assigning one object reference to another means both variables point to the same object. Misunderstanding this can lead to subtle bugs, particularly when dealing with mutable structs (though mutable structs are generally discouraged, as discussed in Section 6.4.2). TypeScript developers will recognize the concept of primitive types versus object types, but C#'s struct versus class distinction is more explicit and carries deeper implications for performance and memory layout.
2.2.2. Stack vs. Heap Allocation: Performance Implications
The distinction between value and reference types directly relates to how memory is managed:
Stack Allocation: Value types, when declared as local variables or method parameters, are typically allocated on the stack.25 The stack is a region of memory that operates in a Last-In, First-Out (LIFO) manner. Allocation and deallocation on the stack are extremely fast, typically involving just moving a stack pointer.
Heap Allocation: Reference types are always allocated on the managed heap.25 The variable itself (the reference) might reside on the stack (if it's a local variable) or within another heap object, but the object's data is on the heap. Heap allocation is more complex and involves the Garbage Collector (GC) for deallocation.
It's important to note that if a value type (like a struct) is a field within a class (a reference type), that struct's data will reside on the heap as part of the containing class object.26
The choice between using a class (reference type) or a struct (value type) is therefore not merely a semantic one but carries direct performance implications. Small, short-lived data structures are often good candidates for structs to take advantage of efficient stack allocation and reduce pressure on the GC. Conversely, large data structures, even if they logically represent a single "value," are usually better implemented as classes to avoid the overhead of copying large blocks of data during assignments or parameter passing. This nuanced performance consideration is something Python and TypeScript developers might not have encountered with the same directness, as memory management is generally more abstracted in those languages.
2.2.3. Boxing and Unboxing: Mechanics and Performance Costs
C# features a unified type system where any type, value or reference, can be treated as an instance of System.Object. To enable this for value types, C# uses boxing and unboxing operations.21
Boxing: This is the process of converting a value type instance to a reference type. When a value type is boxed, the CLR allocates a new object on the managed heap and copies the value type's data into this new "box" object.27 The result is a reference to this heap object. Boxing is an implicit conversion.
C#
int myValue = 123;
object boxedValue = myValue; // Implicit boxing: myValue is copied to the heap


Unboxing: This is the process of converting a boxed value type (which is now an object on the heap) back to its original value type. Unboxing is an explicit conversion and involves two steps: first, checking if the object instance is indeed a boxed value of the target value type, and second, copying the value from the heap object back into a value type variable.27
C#
int unboxedValue = (int)boxedValue; // Explicit unboxing


While boxing and unboxing provide flexibility by allowing value types to be used where reference types are expected (e.g., in older non-generic collections like System.Collections.ArrayList), they are computationally expensive operations.27 Boxing requires heap allocation and data copying. Unboxing involves a type check and data copying. These operations can significantly degrade performance if they occur frequently, especially within loops or performance-critical code paths. For instance, adding value types to an ArrayList causes boxing for each element, and retrieving them often requires unboxing. This overhead was a key motivation for the introduction of generic collections (e.g., System.Collections.Generic.List<T>) in.NET, which avoid boxing for value types by allowing the collection to be strongly typed to the specific value type. Python and TypeScript developers, while dealing with type conversions, might not encounter this specific form of performance penalty tied to a distinction between stack-based values and heap-based objects being treated polymorphically.
2.2.4. Static Typing, Type Inference (var), and the dynamic Type
C# is, at its core, a statically typed language.1 This means the type of every variable and expression is determined and checked by the compiler at compile time. This early type checking helps catch many errors before runtime.
To ease some of the verbosity associated with explicit type declarations, C# introduced the var keyword.1 When var is used to declare a local variable, the compiler infers the type of the variable from the expression used to initialize it. It's crucial to understand that var does not mean the variable is dynamically typed; the type is still fixed at compile time once inferred.1

C#


var count = 10; // Compiler infers 'count' as int
var message = "Hello"; // Compiler infers 'message' as string
// count = "text"; // Compile-time error: cannot convert string to int


var is a notational convenience and should be used when the type is obvious from the right-hand side of the assignment to improve readability without sacrificing type safety.
C# also includes a dynamic type.4 Variables declared as dynamic bypass compile-time type checking. Operations on dynamic objects are resolved at runtime. This behavior is much closer to how variables work in dynamically typed languages like Python.

C#


dynamic anything = 10;
Console.WriteLine(anything.GetType()); // System.Int32
anything = "Hello";
Console.WriteLine(anything.GetType()); // System.String
// anything.NonExistentMethod(); // Runtime error: 'string' does not contain a definition for 'NonExistentMethod'


Python developers might be tempted to use dynamic extensively to replicate the flexibility they are used to. However, this approach largely negates the benefits of C#'s static type system, such as early error detection, better performance, and richer IntelliSense. The dynamic type is primarily intended for specific interoperability scenarios, such as working with COM objects, dynamic languages like Python (via IronPython), or processing JSON structures where the schema is not known at compile time. For general application development, embracing static typing and using var judiciously is the recommended C# practice.
2.2.5. Nullable Reference Types (NRTs) and Nullable Value Types
Handling null values is a common source of bugs, particularly NullReferenceException (or its equivalents like Python's AttributeError: 'NoneType' object has no attribute...). C# provides robust mechanisms to manage nullability for both value types and reference types.
Nullable Value Types: By default, value types (like int, struct) cannot hold a null value. To allow a value type to represent null, you use the ? suffix, for example, int?.21 This is syntactic sugar for the generic struct System.Nullable<T>. A nullable value type T? has two important members: HasValue (a bool indicating if it holds a value) and Value (of type T, which throws an exception if HasValue is false).
C#
int? age = null;
if (age.HasValue)
{
    Console.WriteLine($"Age: {age.Value}");
}
else
{
    Console.WriteLine("Age is not specified.");
}


Nullable Reference Types (NRTs): Historically, reference types in C# (like string or custom classes) were always nullable. C# 8.0 introduced Nullable Reference Types (NRTs) as an opt-in feature (enabled via <Nullable>enable</Nullable> in the .csproj file, now default for new.NET 6+ projects).4 When NRTs are enabled:
Reference types are non-nullable by default. The compiler issues warnings if you try to assign null to them or use them before initialization.
To declare a reference type as nullable, you must explicitly use the ? suffix, e.g., string?. The compiler performs sophisticated static flow analysis to track the null state of variables.29 It warns if you attempt to dereference a potentially null variable without a prior null check.
C#
#nullable enable // Enable NRT context
string name = "Alice"; // Non-nullable, cannot be null
string? middleName = null; // Nullable, can be null

// Console.WriteLine(name.Length); // OK
// Console.WriteLine(middleName.Length); // Compiler warning: middleName may be null

if (middleName!= null)
{
    Console.WriteLine(middleName.Length); // OK, compiler knows it's not null here
}


Python developers, accustomed to None being a pervasive and often unchecked value, will find C#'s NRTs a significant paradigm shift towards proactive null management. TypeScript's strictNullChecks option 31 provides a similar benefit by introducing null and undefined into the type system and requiring checks. However, C#'s NRT system is arguably more deeply integrated with language features and compiler analysis, especially with the use of nullable attributes.30 These attributes (e.g., [NotNullWhen(true)], [MaybeNull], [AllowNull], ``, [NotNullIfNotNull]) allow developers to provide more detailed nullability contracts for APIs, giving the compiler finer-grained information for its flow analysis. For instance, bool TryGetValue(string key, [NotNullWhen(true)] out string? value) informs the compiler that if TryGetValue returns true, the out parameter value will not be null. This level of annotation and compiler-assisted null safety is a powerful tool in C# for building robust applications and reducing runtime NullReferenceExceptions, requiring a disciplined approach to annotating code and addressing compiler warnings.
2.3. Operators and Control Flow: Advanced Usage
C# supports a comprehensive suite of operators and control flow statements, many of which will be familiar to developers from C-family languages, including Python and TypeScript.
Operators:
C# provides a rich set of operators 18, including:
Arithmetic: +, -, *, /, %
Relational: ==, !=, <, >, <=, >=
Logical: && (conditional AND), || (conditional OR), ! (NOT)
Bitwise: &, |, ^, ~, <<, >>
Assignment: =, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=
Increment/Decrement: ++, --
Member Access: .
Indexing: ``
Type Testing/Conversion: is (type pattern), as (safe cast), typeof (gets System.Type object), () (explicit cast)
Null-Coalescing: ?? (provides a default value if an expression is null)
Null-Conditional (Elvis Operator): ?., ? (accesses members or elements only if the object is not null, otherwise returns null) 5
Conditional (Ternary): ?:
Lambda Declaration: =>
nameof Operator: Obtains the string name of a variable, type, or member.
Python developers will find operators like foreach (similar to Python's for...in) intuitive. TypeScript developers will recognize most of the syntax. The null-coalescing (??) and null-conditional (?., ?) operators are particularly vital when working with nullable types, providing concise ways to handle potential nulls.
Control Flow:
Standard control flow statements include if-else, switch, for, foreach, while, do-while, break, continue, return, and goto (though goto is generally discouraged).18
C#'s switch statement is notably more powerful than in traditional C-style languages or basic TypeScript switches. It supports pattern matching, allowing case labels to match based on types, property values, relational patterns, and more, often in conjunction with when clauses for additional conditions.38

C#


object shape = GetShape();
switch (shape)
{
    case Circle c when c.Radius > 10:
        Console.WriteLine("Large circle");
        break;
    case Circle c:
        Console.WriteLine("Small circle");
        break;
    case Square s when s.Side > 5:
        Console.WriteLine($"Large square with area {s.Side * s.Side}");
        break;
    case Square s:
        Console.WriteLine("Small square");
        break;
    case null:
        Console.WriteLine("Shape is null");
        break;
    default:
        Console.WriteLine("Unknown shape");
        break;
}


This advanced pattern matching offers a more declarative and readable way to handle complex conditional logic compared to lengthy if-else if chains common in Python or simpler switch statements in TypeScript.
C# Operators Overview Table:
Category
Operators
Brief Description
Arithmetic
+, -, *, /, %, ++, --
Standard mathematical operations, increment, decrement.
Relational
==, !=, <, >, <=, >=
Comparison of values.
Logical (Boolean)
&&, `
,!`
Bitwise & Shift
&, `
,^,~,<<,>>`
Assignment
=, +=, -=, *=, /=, %=, &=, etc.
Assigning values, compound assignment.
Member Access
.
Accessing members of a type.
Indexing
``
Accessing elements of an array or indexer.
Type Information
is, as, typeof
Type checking, safe casting, obtaining System.Type object.
Null-Handling
??, ?., ?
Null-coalescing, null-conditional member access, null-conditional element access.
Conditional (Ternary)
?:
Concise if-else expression.
Lambda Expression
=>
Declares a lambda expression.
Other
new, sizeof, nameof, await, checked, unchecked
Object creation, size of value type, getting name, awaiting tasks, overflow control.

This table provides a quick reference, especially for operators that have more specific C# semantics or are less common in Python or TypeScript, such as as, typeof, ??, ?., and nameof. Understanding these is key to writing idiomatic C# code.
3. Mastering Object-Oriented Programming in C#
C# is a deeply object-oriented language. While Python and TypeScript also support OOP principles, C# enforces them more rigorously through its static type system and provides a rich set of language features for building complex, maintainable object hierarchies.
3.1. Classes and Structs: Design Considerations
As established (Section 2.2.1), C# distinguishes between classes (reference types) and structs (value types).21 This choice is fundamental to design.
Classes: Suitable for complex objects, entities with identity, and when inheritance is needed. Instances are allocated on the heap and managed by the GC.
Structs: Best for small, lightweight data structures that primarily encapsulate a few related values and behave like primitive types (e.g., Point, Color).43 They are value types, meaning assignment copies the entire data.
A crucial best practice for struct design is immutability.44 Because structs are copied on assignment, if a mutable struct is modified after being copied, the original and the copy will diverge, which can lead to confusing and hard-to-debug behavior.

C#


public struct MutablePoint { public int X; public int Y; }
//...
var p1 = new MutablePoint { X = 10, Y = 20 };
var p2 = p1; // p2 is a copy of p1
p2.X = 30;
// Now p1.X is still 10, but p2.X is 30. This can be unexpected.


To enforce immutability, C# provides the readonly modifier. A struct can be declared as readonly struct, which ensures all its instance fields are also readonly and its properties are get-only or init-only.44

C#


public readonly struct ImmutablePoint
{
    public int X { get; } // Or public int X { get; init; }
    public int Y { get; } // Or public int Y { get; init; }

    public ImmutablePoint(int x, int y)
    {
        X = x;
        Y = y;
    }
}


The readonly modifier provides stronger, compiler-enforced guarantees of immutability compared to conventions often used in Python (e.g., naming convention for private fields, properties with only getters) or TypeScript (e.g., readonly properties in interfaces/classes). This is particularly important for structs due to their copy-by-value semantics. Mutable structs are generally considered an anti-pattern in C#.45
3.2. Inheritance: sealed, abstract, virtual, override, new, base
C# supports single class inheritance and allows a class to implement multiple interfaces.41 The language provides several keywords to control inheritance and polymorphism:
virtual: When applied to a method or property in a base class, virtual allows that member to be overridden by a derived class.47 Without virtual, a member cannot be polymorphically overridden.
override: Used in a derived class to provide a new implementation for an inherited member that was marked virtual, abstract, or override in the base class.47 An override member participates in polymorphism.
abstract:
When applied to a class, indicates that the class cannot be instantiated directly and is intended to be a base class. Abstract classes can contain abstract members.
When applied to a member (method, property, indexer, or event) within an abstract class, it declares the member without an implementation. Derived non-abstract classes must provide an implementation for all inherited abstract members using override.47
sealed:
When applied to a class, sealed prevents other classes from inheriting from it.47
When applied to an override member, sealed prevents further overriding of that member in subsequent derived classes.47
new (modifier): When used on a member in a derived class that has the same name as a member in a base class (and the base member is not virtual or is not being overridden), the new keyword explicitly hides the base class member.47 This is different from overriding; the method called depends on the compile-time type of the variable, not the runtime type of the object, unless the object is cast.
base: Used within a derived class to access members (constructors, methods, properties) of its direct base class.47 For example, base.MyMethod() calls the base class version of MyMethod, and base(args) calls a base class constructor.
Python's method overriding is implicit—if a derived class defines a method with the same name as a base class method, it overrides it. TypeScript's concept of overriding is tied to its structural type system, focusing on signature compatibility. C#'s explicit use of virtual and override makes the intent of polymorphism much clearer and less prone to accidental overriding or hiding. This explicitness is a design choice favoring clarity and maintainability in larger codebases. For instance, if a base class method is not marked virtual, a derived class cannot polymorphically override it; if it defines a method with the same name, it hides the base method (and the compiler will issue a warning unless new is used to explicitly state this intent). This prevents subtle bugs where a developer might think they are overriding a method when they are actually just hiding it.
3.3. Polymorphism: Overloading and Overriding in Detail
Polymorphism ("many forms") is a core OOP principle. C# supports it through method overloading (compile-time polymorphism) and method overriding (runtime polymorphism).
Method Overloading (Compile-Time Polymorphism): This allows multiple methods within the same class to share the same name, provided their parameter signatures are different.50 The signature differences can be in the number of parameters, the types of parameters, or the order of parameters. The return type alone is not sufficient to differentiate overloaded methods. The correct overload to call is determined by the compiler at compile-time based on the arguments provided in the method call.
C#
public class Calculator
{
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b; // Overload
    public int Add(int a, int b, int c) => a + b + c; // Overload
}

While Python achieves overload-like behavior using default arguments, *args, and **kwargs, with runtime checks to determine behavior, C#'s static typing enables true signature-based overloading resolved at compile time. This provides strong type safety and clearer API contracts. For Python developers, this means learning to leverage C#'s static type system to define distinct, type-safe method overloads rather than relying on runtime argument inspection.
Method Overriding (Runtime Polymorphism): This occurs when a derived class provides a specific implementation for a method that is defined in its base class and marked as virtual, abstract, or override.48 The decision of which method implementation to execute (base class's or derived class's) is made at runtime, based on the actual type of the object instance.
C#
public class Animal
{
    public virtual void MakeSound() => Console.WriteLine("Generic animal sound");
}

public class Dog : Animal
{
    public override void MakeSound() => Console.WriteLine("Woof");
}

public class Cat : Animal
{
    public override void MakeSound() => Console.WriteLine("Meow");
}

//...
Animal myPet = new Dog();
myPet.MakeSound(); // Calls Dog's MakeSound() - "Woof"
myPet = new Cat();
myPet.MakeSound(); // Calls Cat's MakeSound() - "Meow"

The access modifier of the overriding method cannot be more restrictive than that of the overridden method.50
3.4. Encapsulation: Access Modifiers
Encapsulation, the bundling of data with the methods that operate on that data and restricting direct access to some of an object's components, is enforced in C# using access modifiers. These keywords control the visibility and accessibility of types and their members.41
public: Accessible from any code in any assembly.
private: Accessible only within the body of the class or struct in which it is declared. This is the default accessibility for class/struct members.
protected: Accessible within its class and by derived class instances.
internal: Accessible only within files in the same assembly (.dll or .exe). This is the default accessibility for types declared directly within a namespace.
protected internal: Accessible within its own assembly, or by derived classes in another assembly. It's a logical OR of protected and internal.
private protected: Accessible by types derived from the containing class, but only within its containing assembly. It's a logical AND of private and protected (more restrictive than protected internal).
file (C# 11+): The type or member is accessible only within the same source file.
A summary table from 52 illustrates this:
Caller's location
public
protected internal
protected
internal
private protected
private
file
Within the file
✔️
✔️
✔️
✔️
✔️
✔️
✔️
Within the class
✔️
✔️
✔️
✔️
✔️
✔️
❌
Derived class (same assembly)
✔️
✔️
✔️
✔️
✔️
❌
❌
Non-derived class (same assembly)
✔️
✔️
❌
✔️
❌
❌
❌
Derived class (different assembly)
✔️
✔️
✔️
❌
❌
❌
❌
Non-derived class (different assembly)
✔️
❌
❌
❌
❌
❌
❌

Python relies on naming conventions (e.g., a leading underscore _ for "internal" use, a double leading underscore __ for name mangling to simulate "private") which are not strictly enforced by the interpreter.53 TypeScript provides public, private, and protected modifiers.4 C#'s internal access modifier is particularly powerful for library design. It allows types and members to be publicly accessible within the assembly (e.g., for helper classes or internal frameworks used by various parts of the library) but completely hidden from external assemblies that consume the library. This provides a more granular level of encapsulation than typically available in Python or standard TypeScript, enabling cleaner public APIs and better internal organization for complex components.
3.5. Interfaces: Explicit, Implicit, and Default Interface Methods (DIMs)
Interfaces in C# define a contract consisting of a set of public members (methods, properties, events, indexers) that a class or struct can implement.41 A type can implement multiple interfaces.
Implicit Implementation: This is the most common way. The implementing class provides public members that match the interface's signatures. These members are directly callable on an instance of the class.
C#
public interface ILogger { void Log(string message); }
public class ConsoleLogger : ILogger
{
    public void Log(string message) => Console.WriteLine(message); // Implicit
}
// ConsoleLogger logger = new ConsoleLogger(); logger.Log("test");
// ILogger ilogger = logger; ilogger.Log("test");


Explicit Implementation: A class member is explicitly tied to an interface member using the interface name. Such members are not part of the class's public interface and can only be accessed through an instance of the interface type.54 This is useful for:
Resolving name collisions when a class implements multiple interfaces that have members with the same signature.
Hiding interface members from the class's direct public API, making them accessible only when the object is treated as the interface type.
C#
interface IControl { void Paint(); }
interface ISurface { void Paint(); }
public class MyComponent : IControl, ISurface
{
    void IControl.Paint() => Console.WriteLine("IControl.Paint"); // Explicit
    void ISurface.Paint() => Console.WriteLine("ISurface.Paint"); // Explicit
}
// MyComponent comp = new MyComponent();
// comp.Paint(); // Compile error
// IControl ctrl = comp; ctrl.Paint(); // Calls IControl.Paint
// ISurface surf = comp; surf.Paint(); // Calls ISurface.Paint


Default Interface Methods (DIMs): Introduced in C# 8.0, DIMs allow interfaces to provide a default implementation for some of their members.56 This enables API authors to add new members to existing interfaces without breaking existing classes that implement them.
C#
public interface IWorker
{
    void DoWork();
    void DoMoreWork() => Console.WriteLine("Default DoMoreWork implementation"); // DIM
}
public class OldWorker : IWorker
{
    public void DoWork() => Console.WriteLine("OldWorker doing work.");
    // Does not need to implement DoMoreWork if default is acceptable.
}

DIMs bring a form of "trait" or "mixin" capability to C#, allowing interfaces to carry behavior, not just define contracts. This is powerful for API evolution and code reuse. However, it introduces complexities in method resolution, especially with multiple interface inheritance where a class might inherit conflicting default implementations. C# resolves this using a "most specific override" rule: a class's own implementation always takes precedence over a DIM. If a class inherits multiple interfaces with the same default method and doesn't provide its own override, it can lead to ambiguity unless one interface's implementation is considered more specific (e.g., one interface inherits from another that provides the DIM).56 Developers need to be aware of these resolution rules. Structs can also inherit DIMs, but this can have performance implications due to potential boxing if the DIM operates on the interface type itself.57
3.6. Properties: Auto-implemented, Full, and Init-only Setters
Properties are first-class members in C# that provide flexible and controlled access to an object's state, typically by encapsulating private fields.41 They use get and set accessors.
Auto-Implemented Properties: Provide a concise syntax when no additional logic is needed in the accessors. The compiler automatically generates a private backing field.
C#
public string Name { get; set; }


Full Properties (with explicit backing field): Used when custom logic is required in the get or set accessors (e.g., validation, raising events, lazy loading).
C#
private string _name;
public string Name
{
    get { return _name; }
    set
    {
        if (string.IsNullOrWhiteSpace(value))
            throw new ArgumentException("Name cannot be empty.");
        _name = value;
    }
}


Init-only Setters (init): Introduced in C# 9.0, init accessors allow a property to be set only during object initialization (either in a constructor or using an object initializer).59 After initialization, the property becomes effectively read-only. This is crucial for creating immutable objects with a more flexible initialization syntax.
C#
public class Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}
var person = new Person { FirstName = "Ada", LastName = "Lovelace" };
// person.FirstName = "Grace"; // Compile error: FirstName can only be set in an initializer.
Traditionally, achieving immutability for properties often meant having get-only properties initialized solely via the constructor, or using readonly backing fields. This made object initializer syntax (e.g., new Person { Name = "X" }) unusable for these immutable properties. init-only setters bridge this gap, providing the conciseness of object initializers while still enforcing immutability after the object is constructed.59 This is a significant enhancement for creating immutable Data Transfer Objects (DTOs) and records (see Section 3.10). The compiler emits init accessors as standard set accessors but marks them with a special IsExternalInit modifier type, which signals to other C# 9.0+ compilers that this setter has init-only semantics.59
3.7. Indexers: Syntax and Usage
Indexers in C# allow instances of a class or struct to be accessed using array-like syntax (e.g., myObject[index]).41 They are particularly useful for creating custom collection types or types that logically represent an indexable set of data.
Indexers are declared using the this keyword followed by parameters enclosed in square brackets, and they can have get and set accessors, similar to properties:

C#


public class TempRecord
{
    private float temps = new float;
    public float this[int index] // Indexer declaration
    {
        get
        {
            if (index < 0 |
| index >= temps.Length)
                throw new IndexOutOfRangeException("Index out of range.");
            return temps[index];
        }
        set
        {
            if (index < 0 |
| index >= temps.Length)
                throw new IndexOutOfRangeException("Index out of range.");
            temps[index] = value;
        }
    }
}
// Usage:
// TempRecord record = new TempRecord();
// record = 32.5f;
// float firstTemp = record;


Indexers can be overloaded based on the number and types of their parameters (e.g., an int indexer and a string indexer can coexist in the same class).61 By default, the compiler generates a property named Item for the indexer, but this can be changed using the System.Runtime.CompilerServices.IndexerNameAttribute.61
C# 8.0 and later versions enhanced indexing capabilities by introducing System.Index and System.Range types, which can be used with arrays, Span<T>, and types that provide appropriate indexer support.62 This allows for more expressive indexing from the end of a collection (e.g., myArray[^1] for the last element) and slicing (e.g., myArray[1..^1] for a sub-section).
This feature provides syntactic sugar that makes custom types feel more like built-in collections. Python achieves similar functionality through special methods like __getitem__ and __setitem__. TypeScript relies on JavaScript's native array/object indexing or can define index signatures in interfaces/types. C#'s indexers offer a dedicated language construct that integrates cleanly with its property and method syntax, allowing for clear, type-safe, and potentially complex indexing logic within the get and set accessors.
3.8. Constructors: Default, Parameterized, Copy, Static, and Constructor Chaining (this, base)
Constructors are special methods responsible for initializing new objects of a class or struct.41 Proper constructor design is vital for ensuring objects are created in a valid state.
Default Constructor: A parameterless constructor. If no constructors are explicitly defined in a class, the C# compiler provides a public default constructor that initializes all fields to their default values (e.g., 0 for numeric types, null for reference types).64 If any constructor is defined, the default constructor is not automatically provided unless explicitly declared. For structs, a default parameterless constructor always exists (implicitly or explicitly) and initializes fields to their default values.
Parameterized Constructor: Takes arguments to initialize the object's state. Classes and structs can have multiple parameterized constructors (overloading).
C#
public class Point { public int X, Y; public Point(int x, int y) { X = x; Y = y; } }


Copy Constructor: A constructor that takes an instance of the same type as a parameter and creates a new object by copying the state from the provided instance. C# does not automatically provide copy constructors; they must be manually implemented if needed.64
C#
public class Point { /*... */ public Point(Point other) { X = other.X; Y = other.Y; } }


Static Constructor: Declared with the static keyword. It is used to initialize static members of a type or to perform any one-time setup action required for the type itself.63 A static constructor is parameterless, cannot have access modifiers, and is called automatically by the CLR before the first instance of the class is created or any static members are referenced. It is guaranteed to run at most once per application domain.
C#
public class AppConfig
{
    public static readonly string ConnectionString;
    static AppConfig() // Static constructor
    {
        // Load configuration, e.g., from a file
        ConnectionString = LoadConnectionStringFromConfig();
        Console.WriteLine("Static constructor called, ConnectionString initialized.");
    }
    private static string LoadConnectionStringFromConfig() => "some_connection_string";
}


Constructor Chaining: C# allows a constructor to call another constructor in the same class (using : this(...)) or a constructor in its direct base class (using : base(...)).64 This is useful for reducing code duplication and ensuring proper initialization order. The chained constructor call occurs before the body of the calling constructor executes.
C#
public class BaseClass
{
    protected int A;
    public BaseClass(int a) { A = a; Console.WriteLine("BaseClass constructor"); }
}
public class DerivedClass : BaseClass
{
    public int B { get; set; }
    public DerivedClass() : this(0) // Chains to DerivedClass(int b)
    {
        Console.WriteLine("DerivedClass parameterless constructor");
    }
    public DerivedClass(int b) : base(b * 10) // Chains to BaseClass(int a)
    {
        B = b;
        Console.WriteLine("DerivedClass parameterized constructor");
    }
}
// new DerivedClass(); will output:
// BaseClass constructor (A will be 0)
// DerivedClass parameterized constructor (B will be 0)
// DerivedClass parameterless constructor

The order of initialization actions is well-defined 63:
Instance fields are set to their default values (typically by the runtime).
Field initializers in the most derived type run.
Field initializers run from the direct base type up to System.Object.
Base class instance constructors run, starting from System.Object down to the direct base class (respecting constructor chaining).
The instance constructor for the current type runs.
If object initializers are used in the creation expression, they run after the instance constructor.
C#'s explicit constructor chaining syntax (: this() and : base()) provides a clear and controlled mechanism for managing initialization logic across constructor overloads and inheritance hierarchies. This is more structured than Python's __init__ and super().__init__() calls, which, while functional, can sometimes be less obvious in their execution order within complex hierarchies if not meticulously managed. The C# approach ensures that base class initialization happens predictably before derived class constructor bodies execute.
3.9. Finalizers, IDisposable, and Garbage Collection
C# relies on automatic memory management via the Garbage Collector (GC). However, for resources not managed by the GC (unmanaged resources like file handles, database connections, network sockets, OS handles), C# provides mechanisms for deterministic and non-deterministic cleanup.
3.9.1. The Dispose Pattern and using Statement/Declaration
The primary mechanism for deterministic resource cleanup in C# is the IDisposable interface and the Dispose Pattern.66
IDisposable Interface: This interface defines a single method, void Dispose(). Types holding unmanaged resources or other managed IDisposable resources should implement this interface to provide a way for consumers to explicitly release those resources.
Dispose Pattern Implementation: A common implementation involves:
A public Dispose() method (implementing IDisposable.Dispose).
A protected virtual Dispose(bool disposing) method that does the actual cleanup.
A private boolean flag (e.g., _disposed) to track if Dispose has already been called, making Dispose() calls idempotent (safe to call multiple times).
The Dispose(bool disposing) method is key:
If disposing is true, the method was called directly or indirectly by a user's code (deterministic cleanup). It should release both managed (other IDisposable objects) and unmanaged resources.
If disposing is false, the method was called by the runtime from a finalizer (non-deterministic cleanup). It should only release unmanaged resources. Managed objects should not be touched as they might have already been finalized or collected.66
C#
public class ResourceHolder : IDisposable
{
    private IntPtr unmanagedResource; // Example unmanaged resource
    private Component managedResource; // Example managed disposable resource
    private bool _disposed = false;

    public ResourceHolder()
    {
        // Allocate resources
        unmanagedResource = Marshal.AllocHGlobal(100);
        managedResource = new Component();
    }

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this); // Tell GC not to call the finalizer
    }

    protected virtual void Dispose(bool disposing)
    {
        if (_disposed) return;

        if (disposing)
        {
            // Release managed resources
            if (managedResource!= null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }

        // Release unmanaged resources
        if (unmanagedResource!= IntPtr.Zero)
        {
            Marshal.FreeHGlobal(unmanagedResource);
            unmanagedResource = IntPtr.Zero;
        }
        _disposed = true;
    }

    // Finalizer (destructor) if class owns unmanaged resources directly
    // and no SafeHandle is used.
    ~ResourceHolder()
    {
        Dispose(false);
    }
}
A best practice for managing unmanaged resources is to use classes derived from System.Runtime.InteropServices.SafeHandle, which encapsulate the resource handle and provide their own critical finalizer, often simplifying the Dispose pattern implementation.66
using Statement and Declaration: To ensure Dispose() is always called, even if exceptions occur, C# provides the using statement and using declaration.68
using statement: Defines a scope. When control leaves the scope, Dispose() is called on the object.
C#
using (var reader = new StreamReader("file.txt"))
{
    // Use reader
} // reader.Dispose() is called here


using declaration (C# 8.0+): Declares a disposable variable. Dispose() is called when the variable goes out of scope (typically at the end of the method).
C#
void ProcessFile(string filePath)
{
    using var reader = new StreamReader(filePath);
    // Use reader
} // reader.Dispose() is called here


The using construct in C# is conceptually similar to Python's with statement and context manager protocol (__enter__, __exit__). Both provide a robust way to ensure resources are deterministically released. TypeScript, running in JavaScript environments, typically relies on try...finally blocks or specific library patterns for such resource management. The IDisposable interface and using keyword provide a standardized, language-integrated solution in C#.
3.9.2. Garbage Collector (GC) Overview: Generations, SOH, LOH, Mark-Sweep-Compact
The.NET Garbage Collector (GC) is an automatic memory manager that reclaims memory occupied by objects that are no longer in use.70 Key concepts include:
Generations: The GC is generational, typically with three generations for small objects: Gen 0, Gen 1, and Gen 2.70
Gen 0: New, short-lived objects are allocated here. Gen 0 collections are frequent and fast.
Gen 1: Objects surviving a Gen 0 collection are promoted to Gen 1. It acts as a buffer.
Gen 2: Objects surviving a Gen 1 collection are promoted to Gen 2. This is for long-lived objects. Gen 2 collections are less frequent but more expensive as they involve scanning a larger portion of the heap.
Small Object Heap (SOH): Managed objects smaller than 85,000 bytes are typically allocated on the SOH and participate in the generational collection process.71
Large Object Heap (LOH): Objects 85,000 bytes or larger are allocated on the LOH.71 These objects are logically part of Gen 2 and are collected only during a full Gen 2 collection.
GC Process (Mark-Sweep-Compact for SOH):
Mark Phase: The GC identifies all live (reachable) objects by traversing object graphs starting from application roots (static fields, local variables on thread stacks, CPU registers, GC handles, finalize queue).70
Sweep Phase: The memory occupied by dead (unreachable) objects is identified.72
Compact Phase: For the SOH, live objects are moved together in memory to reduce fragmentation and reclaim space. References to these objects are updated.70 The LOH, by default, is marked and swept, but not compacted due to the high cost of moving large objects. Dead objects on the LOH leave free spaces that can be reused.71
Understanding GC behavior is crucial for writing memory-efficient C# applications. Frequent allocations of large objects or many short-lived objects that get promoted to older generations can increase GC pressure and impact application performance. The non-compacting nature of the LOH (by default) can lead to fragmentation over time in long-running applications that frequently allocate and deallocate large objects. This fragmentation can make it difficult to find contiguous memory blocks for new large allocations, potentially leading to OutOfMemoryExceptions even if total free memory seems sufficient. Strategies like object pooling for large objects or using System.Buffers.ArrayPool<T> for large arrays become important mitigation techniques.73 This level of concern about heap fragmentation, especially for large objects, is a nuance that Python and TypeScript developers might not have encountered as directly, as their respective memory managers often abstract these details more heavily.
3.9.3. Finalization Process: Finalize Method, Finalization Queue, GC.SuppressFinalize
Finalization is a non-deterministic mechanism for resource cleanup, primarily intended as a safeguard for unmanaged resources if Dispose() is not called.
Finalize Method (Destructor Syntax): In C#, a finalizer is declared using destructor syntax (~ClassName()).74 The compiler translates this into an override of the protected virtual void Finalize() method inherited from System.Object. Finalizers cannot be called directly; they are invoked automatically by the GC.
Finalization Queue: When an object with a finalizer is created, a pointer to it is placed on a finalization queue. When the GC deems such an object unreachable, instead of immediately reclaiming its memory, it moves the object's entry from the finalization queue to a separate "f-reachable" queue. A dedicated finalizer thread processes this queue, executing each object's Finalize method.74 Only after the finalizer has run can the object's memory be reclaimed in a subsequent GC cycle.
GC.SuppressFinalize(this): This static method of the System.GC class is typically called at the end of a successful IDisposable.Dispose() implementation.66 It informs the GC that the object has already been cleaned up deterministically, so its Finalize method does not need to be called. This removes the object from the finalization queue, allowing its memory to be reclaimed sooner and avoiding the overhead of finalization.
Relying on finalizers for critical resource cleanup is generally discouraged due to their non-deterministic nature and performance overhead.74 Objects with finalizers are more expensive to create and collect. The recommended practice is to implement IDisposable for deterministic cleanup and use finalizers only as a fallback for unmanaged resources. As mentioned earlier, using SafeHandle-derived classes is the preferred way to manage unmanaged resources, as SafeHandle correctly implements IDisposable and has a critical finalizer, often eliminating the need for developers to write their own finalizers.66 This significantly simplifies resource management and reduces the likelihood of errors common with manual finalizer implementation.
3.9.4. System.GC Class: Key Methods
The System.GC class provides programmatic control over the garbage collector.76 While direct manipulation of the GC is often unnecessary, certain methods can be useful in specific scenarios:
GC.Collect(): Forces an immediate garbage collection. Overloads allow specifying the generation to collect. This should be used sparingly, as it can disrupt the GC's self-tuning heuristics and often harms performance more than it helps. It's primarily for testing or unique situations where an immediate collection is known to be beneficial.76
GC.SuppressFinalize(object obj): Requests that the CLR not call the finalizer for the specified object. Crucial in the Dispose pattern.76
GC.KeepAlive(object obj): Ensures an object remains ineligible for garbage collection until the point this method is called. Useful in interop scenarios where managed objects are passed to unmanaged code that might hold the only reference.76
GC.GetGeneration(object obj): Returns the current generation number of the specified object.76
GC.GetTotalMemory(bool forceFullCollection): Retrieves an estimate of the number of bytes currently allocated in managed memory. If forceFullCollection is true, it may trigger a GC before returning.76
GC.AddMemoryPressure(long bytesAllocated) and GC.RemoveMemoryPressure(long bytesAllocated): These methods inform the GC about large allocations or deallocations of unmanaged memory.76 The GC primarily tracks managed memory. If an application uses significant unmanaged memory (e.g., via P/Invoke or native libraries), the GC might be unaware of the true memory pressure on the system. AddMemoryPressure tells the GC that additional unmanaged memory has been allocated, potentially prompting it to collect more aggressively. RemoveMemoryPressure is called when that unmanaged memory is freed. This helps the GC make more informed decisions and can prevent out-of-memory situations when managed memory seems plentiful but total process memory is high. This level of GC interaction is generally not something Python or TypeScript developers engage with.
GC.WaitForPendingFinalizers(): Suspends the current thread until all objects for which finalizers were called have had their finalizers completed.76 This is sometimes used after a GC.Collect() in specific cleanup scenarios, but like GC.Collect(), it should be used with caution.
3.10. Records: For Immutable Data Structures
Introduced in C# 9.0, records provide a concise syntax for creating types whose primary purpose is to encapsulate data.82 They are designed to be excellent for immutable data models. Records can be reference types (record class, or just record) or value types (record struct since C# 10).82
Key features and benefits of records:
Concise Syntax for Immutability: Positional records allow you to declare immutable properties and a primary constructor in a single line.
C#
public record Person(string FirstName, string LastName, int Age);
// Equivalent to a class with init-only properties for FirstName, LastName, Age
// and a constructor that initializes them.


Value-Based Equality: The compiler automatically generates implementations for Equals(), GetHashCode(), and the equality operators (==, !=) based on the values of all public properties and fields.82 This means two record instances are considered equal if all their corresponding data members are equal, which is often desired for DTOs or value objects. This contrasts with classes, which default to reference equality.
ToString() Override: The compiler generates a ToString() method that outputs the type name and the names and values of all public properties, useful for debugging and logging.82
Deconstructor: For positional records, the compiler synthesizes a Deconstruct method, allowing easy deconstruction into individual variables.
C#
var person = new Person("John", "Doe", 30);
var (fn, ln, ag) = person; // Deconstruction


Nondestructive Mutation (with-expressions): Records support with-expressions, which create a new record instance that is a copy of an existing instance, with specified properties modified. This facilitates working with immutable data by providing an easy way to create "changed" versions without altering the original.82
C#
var person1 = new Person("Jane", "Doe", 28);
var person2 = person1 with { LastName = "Smith" };
// person1 is unchanged. person2 is a new record: ("Jane", "Smith", 28)


Inheritance: Record classes can inherit from other record classes (but not from regular classes, and regular classes cannot inherit from record classes). Record structs cannot inherit but can implement interfaces.82
Records significantly reduce the boilerplate code traditionally required in C# to create immutable data types with value-based semantics. This makes C# more competitive with languages like Python (which has dataclasses, especially with frozen=True) or functional languages like Scala (with case classes) for concisely defining data-centric types. For developers coming from Python or TypeScript, where defining simple data structures is often less verbose, C# records offer a much-improved experience for these common scenarios, addressing a historical pain point of C# verbosity for DTOs.
4. Advanced C# Features and Concepts
Beyond its core OOP capabilities, C# offers a suite of advanced features that enable developers to write highly efficient, expressive, and maintainable code.
4.1. Generics: Defining Generic Classes, Methods, Interfaces, Delegates; Type Parameters (T); Constraints; Covariance and Contravariance (in, out)
Generics in C# allow the design of classes, methods, interfaces, and delegates that can operate on various data types without sacrificing type safety.85 The specific type is deferred until the generic type or method is used.
Type Parameters (<T>): A placeholder for a specific type, conventionally named T (or TKey, TValue, etc.).
C#
public class GenericList<T> // T is a type parameter
{
    public void Add(T item) { /*... */ }
    public T GetItem(int index) { /*... */ return default(T); }
}
// Usage: GenericList<int> intList = new GenericList<int>();
//        GenericList<string> stringList = new GenericList<string>();


Constraints (where clause): Restrict the types that can be used as arguments for a type parameter.85 This allows the generic code to safely use methods or properties of the constrained type.
where T : class (T must be a reference type)
where T : struct (T must be a non-nullable value type)
where T : new() (T must have a public parameterless constructor)
where T : <BaseClassName> (T must be or derive from BaseClassName)
where T : <InterfaceName> (T must implement InterfaceName)
where T : U (T must be or derive from type U, another type parameter)
C#
public class DataProcessor<T> where T : IComparable<T>, new()
{
    public T Process(T input)
    {
        T temp = new T(); // Possible due to new() constraint
        if (input.CompareTo(temp) > 0) { /*... */ } // Possible due to IComparable<T>
        return input;
    }
}


Covariance (out) and Contravariance (in): Provide greater flexibility in assigning and using generic types, but apply only to generic interfaces and delegates, and only for reference types.87
Covariance (out T): Allows using a more derived type than specified. An IEnumerable<string> can be assigned to IEnumerable<object>. The type parameter T can only appear in output positions (e.g., return types of methods).
Contravariance (in T): Allows using a less derived type than specified. An Action<object> can be assigned to Action<string>. The type parameter T can only appear in input positions (e.g., method parameters).
C#'s generics are a compile-time and runtime feature; the CLR is aware of generic types. This contrasts with TypeScript's generics, which provide compile-time safety but are erased during transpilation to JavaScript. Python collections are inherently "generic" due to dynamic typing but lack compile-time type safety for their elements. The strong type safety provided by C# generics, especially when combined with constraints, allows for the creation of highly reusable and robust libraries (e.g., System.Collections.Generic.List<T> avoids boxing for value types like int, offering significant performance benefits over older non-generic collections). Covariance and contravariance, while adding a layer of complexity, enable more sophisticated and natural generic API designs, particularly for library authors.
4.2. Delegates and Events
Delegates and events are fundamental to C#'s event-driven programming model and enable powerful callback mechanisms.
4.2.1. Syntax: Declaration, Instantiation (Named Methods, Anonymous Methods, Lambda Expressions)
A delegate is a type that safely encapsulates a reference to a method (or multiple methods).89 It defines the signature (return type and parameters) of the methods it can reference.
Declaration:
C#
public delegate int MathOperation(int a, int b); // Declares a delegate type


Instantiation:
Named Methods:
C#
public static int Add(int x, int y) => x + y;
MathOperation op = Add; // or new MathOperation(Add);


Anonymous Methods (C# 2.0+): Inline method definition without a name. Less common now due to lambdas. 90
C#
MathOperation op = delegate(int x, int y) { return x - y; };


Lambda Expressions (C# 3.0+): The most concise way to create delegate instances.89
C#
MathOperation op = (x, y) => x * y;


Delegates are essentially type-safe function pointers. This compile-time type safety is a key differentiator from more loosely typed callback patterns sometimes seen in Python or JavaScript, where signature mismatches might only be caught at runtime.
4.2.2. Singlecast vs. Multicast Delegates
Delegates in C# can be either singlecast or multicast.92
Singlecast: References a single method.
Multicast: References a list of methods (an invocation list). When a multicast delegate is invoked, all methods in its list are called in the order they were added. The + or += operators are used to combine delegates (add methods to the list), and - or -= to remove them.
C#
public delegate void Notify(string message);
public static void LogToConsole(string msg) => Console.WriteLine($"Console: {msg}");
public static void LogToFile(string msg) { /*... write to file... */ }

Notify notifier = LogToConsole;
notifier += LogToFile; // Now notifier is multicast
notifier("System critical event!"); // Calls both LogToConsole and LogToFile
notifier -= LogToConsole; // Removes LogToConsole


The built-in multicast capability simplifies the implementation of the observer pattern compared to manually managing lists of callbacks, as is often done in Python or JavaScript.
4.2.3. The event Keyword, Event Accessors (add, remove)
The event keyword declares a special kind of multicast delegate within a class, providing a controlled mechanism for publishing notifications.92

C#


public class Button
{
    // Define the delegate type for the event
    public delegate void ClickHandler(object sender, EventArgs e);

    // Declare the event using the event keyword
    public event ClickHandler Clicked;

    // Method to raise the event
    protected virtual void OnClicked(EventArgs e)
    {
        Clicked?.Invoke(this, e); // Safely invoke if there are subscribers
    }

    public void SimulateClick()
    {
        OnClicked(EventArgs.Empty);
    }
}


The event keyword enforces encapsulation:
External code can only subscribe (+=) or unsubscribe (-=) to the event.
External code cannot directly assign to the event (which would wipe out other subscribers) or directly invoke (raise) the event. Only the containing class can invoke the event. This provides a much safer and more robust publisher-subscriber pattern.
By default, the compiler provides simple add and remove accessors for an event, which manage the underlying delegate's invocation list. However, you can define custom event accessors if you need more control over the subscription process (e.g., for custom storage of handlers, thread safety, or interop scenarios like with UWP events that use tokens 95).

C#


private ClickHandler _clicked; // Custom backing field
public event ClickHandler Clicked
{
    add
    {
        // Custom logic for adding a handler
        lock (this) { _clicked += value; }
        Console.WriteLine("Handler added.");
    }
    remove
    {
        // Custom logic for removing a handler
        lock (this) { _clicked -= value; }
        Console.WriteLine("Handler removed.");
    }
}


4.2.4. EventHandler, EventArgs, and Custom EventArgs
.NET provides standardized delegate types and base classes for events to promote consistency 94:
System.EventHandler: A predefined delegate for events that do not pass custom data. Its signature is void EventHandler(object sender, EventArgs e).
System.EventHandler<TEventArgs>: A generic delegate for events that pass custom data. TEventArgs must be a type derived from System.EventArgs. Its signature is void EventHandler<TEventArgs>(object sender, TEventArgs e).
System.EventArgs: The base class for all event data. If an event has no custom data, EventArgs.Empty is typically passed.
Custom EventArgs: To pass custom data with an event, create a class that inherits from EventArgs.
C#
public class ThresholdReachedEventArgs : EventArgs
{
    public int Threshold { get; }
    public DateTime TimeReached { get; }
    public ThresholdReachedEventArgs(int threshold, DateTime time)
    { Threshold = threshold; TimeReached = time; }
}

public class Counter
{
    public event EventHandler<ThresholdReachedEventArgs> ThresholdReached;
    //...
}


This standardized (object sender, EventArgs e) pattern, while sometimes appearing verbose, allows for generic event handling infrastructure (e.g., logging, routing) and promotes uniformity across.NET applications. Python and TypeScript might use more varied callback signatures, but C#'s convention aids in framework design and interoperability.
4.3. Lambda Expressions: Syntax, Type Inference, Closures, Captured Variables
Lambda expressions, introduced in C# 3.0, provide a concise syntax for creating anonymous functions.91 They are extensively used in LINQ, Task-based asynchronous programming, and for instantiating delegates.
Syntax: (input-parameters) => expression (expression lambda) or (input-parameters) => { statements } (statement lambda).
C#
// Expression lambda
Func<int, int> square = x => x * x;

// Statement lambda
Action<string> print = message => { Console.WriteLine(message.ToUpper()); };


Type Inference: The compiler can often infer the types of lambda parameters from the context (e.g., the delegate type it's being assigned to).91 Explicit types can also be provided.
Conversion: Lambda expressions can be converted to compatible delegate types or expression tree types (Expression<TDelegate>).91
Closures and Captured Variables: Lambdas can "capture" variables from their enclosing scope. This means the lambda can access and use these variables even after the enclosing scope has exited. This phenomenon is known as a closure.91
C#
int factor = 10;
Func<int, int> multiplier = n => n * factor; // 'factor' is captured
Console.WriteLine(multiplier(5)); // Output: 50
factor = 20;
Console.WriteLine(multiplier(5)); // Output: 100 (captures the variable, not its value at definition)
A common pitfall with closures involves capturing loop variables directly in a loop. Due to deferred execution (common with LINQ) or how closures work, the lambda might see the final value of the loop variable for all its invocations. The fix is to copy the loop variable to a local variable within the loop's scope and capture that local copy. (See Section 4.4.4).
A particularly powerful aspect of C# lambdas is their ability to be converted into expression trees when assigned to a variable of type System.Linq.Expressions.Expression<TDelegate>.91 Instead of compiling the lambda into executable IL, the compiler generates an object model (the expression tree) that represents the lambda's code structure as data. This tree can then be analyzed and manipulated at runtime. This "code as data" capability is heavily utilized by LINQ providers (like Entity Framework for LINQ to SQL) to translate C# query logic into other languages, such as SQL queries executed by a database.98 This is a more advanced metaprogramming feature than typically available directly in Python or TypeScript.
4.4. LINQ (Language Integrated Query)
LINQ provides a powerful and unified way to query data from various sources (in-memory collections, databases, XML, etc.) directly within the C# language.
4.4.1. Query Syntax vs. Method Syntax
LINQ queries can be written in two equivalent forms 98:
Query Syntax: A declarative, SQL-like syntax using keywords such as from, where, select, orderby, join, group by.
C#
int numbers = { 1, 2, 3, 4, 5, 6 };
var evenNumbersQuery = from num in numbers
                       where num % 2 == 0
                       orderby num descending
                       select num * 10;


Method Syntax (Fluent Syntax): Uses extension methods (Standard Query Operators) chained together, often with lambda expressions for predicates and transformations.
C#
var evenNumbersMethod = numbers.Where(num => num % 2 == 0)
                            .OrderByDescending(num => num)
                            .Select(num => num * 10);


The C# compiler translates query syntax into method syntax calls.99 While query syntax can be more readable for complex queries, especially those involving joins, method syntax is more concise for simpler queries and is necessary for operators that don't have a query syntax keyword (e.g., Count(), FirstOrDefault(), ToList()). Proficient C# developers are comfortable with both, as even query-syntax users often need to append method-syntax calls (e.g., .ToList() to execute the query).
4.4.2. Standard Query Operators
The Standard Query Operators (SQOs) are a set of extension methods, primarily defined in the System.Linq.Enumerable class (for querying IEnumerable<T> objects in-memory) and System.Linq.Queryable class (for querying IQueryable<T> data sources, which can translate queries for remote execution, like databases).98 They provide a rich vocabulary for data manipulation, including:
Filtering: Where
Projection: Select, SelectMany
Ordering: OrderBy, OrderByDescending, ThenBy, ThenByDescending
Grouping: GroupBy
Joining: Join, GroupJoin
Partitioning: Take, Skip, TakeWhile, SkipWhile
Aggregation: Count, Sum, Min, Max, Average, Aggregate
Element Operations: First, FirstOrDefault, Single, SingleOrDefault, Last, LastOrDefault, ElementAt
Quantifiers: Any, All, Contains
Conversion: ToList, ToArray, ToDictionary, ToLookup, OfType, Cast
These operators provide a consistent and composable API for querying data, abstracting away the specifics of the underlying data source. This unification is a core strength of LINQ, reducing the need to learn different query languages for different data types.
4.4.3. LINQ to Objects, LINQ to XML, LINQ to SQL/Entities (Overview)
LINQ's architecture allows it to work with various data sources 98:
LINQ to Objects: Queries in-memory collections that implement IEnumerable<T> (e.g., List<T>, T). Operations are performed locally.
LINQ to XML: Uses classes in System.Xml.Linq (like XDocument, XElement) to query and manipulate XML data using LINQ syntax.
LINQ to SQL/Entities (e.g., Entity Framework Core): Queries relational databases. These providers work with IQueryable<T>. LINQ queries are translated into expression trees, which the provider then converts into native SQL queries for execution on the database server.
The IQueryable<T> interface is pivotal for LINQ's effectiveness with external, queryable data sources like databases. When a LINQ query is constructed against an IQueryable<T> source, the operations are not executed immediately in C#. Instead, an expression tree is built.98 This tree is a data structure representing the logic of the query. The LINQ provider (e.g., Entity Framework Core) then analyzes this expression tree and translates it into an optimized query language (like SQL) specific to the backend data store. This allows complex filtering, sorting, projections, and joins to be performed efficiently on the database server, minimizing data transfer and client-side processing. This is a critical performance optimization and a fundamental difference from LINQ to Objects, which processes data entirely in the application's memory. Python and TypeScript developers working with databases often use ORMs or query builders that have different mechanisms for query translation.
4.4.4. Deferred Execution: Benefits and Common Pitfalls
A key characteristic of most LINQ queries that return a sequence is deferred execution.98 This means the query is not executed when it is defined; rather, the query's logic is stored. The actual execution happens only when the results are enumerated (e.g., in a foreach loop, or by calling a conversion method like ToList(), ToArray(), or an aggregation method like Count()). Operators that return a single value (e.g., Count(), Sum(), First()) typically execute immediately.98
Benefits of Deferred Execution:
Efficiency: Avoids computation if the results are never used or only partially used.
Dynamic Queries: Allows building up queries step-by-step before final execution.
Fresh Data: The query is executed against the current state of the data source each time it's enumerated.
Common Pitfalls:
Multiple Enumeration: If a deferred query is enumerated multiple times, the query is re-executed each time. If the query involves significant computation or database access, this can lead to severe performance degradation or unexpected results if the underlying data source has changed between enumerations.100
Solution: If results need to be accessed multiple times, force immediate execution and cache the results in a collection like a List<T> by calling .ToList() or .ToArray() on the query once.
C#
var expensiveQuery = dataSource.Where(x => x.IsActive).OrderBy(x => x.Name); // Deferred
// Bad: multiple enumerations
// var count = expensiveQuery.Count(); // Enumerates once
// foreach(var item in expensiveQuery) { /*... */ } // Enumerates again

// Good: force execution once
var results = expensiveQuery.ToList(); // Executes query, stores in list
var count = results.Count; // Uses cached list
foreach(var item in results) { /*... */ } // Uses cached list


Closure Issues with Loop Variables (Side Effects of Deferred Execution): When a LINQ query is defined inside a loop and captures the loop variable in its lambda expression, deferred execution can cause problems. The lambda captures the variable itself, not its value at the time of definition. If the query is executed after the loop has completed, the lambda will see the final value of the loop variable for all its operations.100
C#
var predicates = new List<Func<int, bool>>();
for (int i = 0; i < 3; i++)
{
    predicates.Add(num => num == i); // Captures 'i'
}
// At this point, 'i' is 3 (after loop termination)
// All predicates will effectively be 'num => num == 3'

// To fix, create a local copy within the loop:
predicates.Clear();
for (int i = 0; i < 3; i++)
{
    int local_i = i; // Local copy
    predicates.Add(num => num == local_i); // Captures 'local_i'
}
// Now each predicate captures a different value of local_i (0, 1, 2)
This pitfall is common and requires careful attention when combining loops with deferred LINQ queries. Understanding that the lambda closes over the variable, and that the query executes later, is key to avoiding this.
4.5. Asynchronous Programming with async and await
C# has robust language-level support for asynchronous programming, primarily through the async and await keywords, built upon the Task-based Asynchronous Pattern (TAP).
4.5.1. Task-based Asynchronous Pattern (TAP): Task and Task<TResult>
The core of TAP are the System.Threading.Tasks.Task and System.Threading.Tasks.Task<TResult> types.105
Task: Represents an asynchronous operation that does not return a value.
Task<TResult>: Represents an asynchronous operation that returns a value of type TResult.
The async modifier is used to mark a method as asynchronous. Inside an async method, the await keyword can be used to non-blockingly wait for a Task or Task<TResult> to complete.105 When await is encountered:
If the awaited task is not yet complete, control is returned to the caller of the async method. The current method's execution is suspended.
When the awaited task completes, execution resumes at the point after the await keyword.

C#


public async Task<string> DownloadDataAsync(string url)
{
    using (var httpClient = new HttpClient())
    {
        // await suspends DownloadDataAsync, returns control to caller.
        // Execution resumes here when GetStringAsync completes.
        string content = await httpClient.GetStringAsync(url);
        return content;
    }
}


This model simplifies writing non-blocking code for I/O-bound operations (like network requests, file operations) and CPU-bound operations (which can be offloaded to a background thread using Task.Run).
TypeScript developers will find the async/await syntax very familiar, as it's similar to JavaScript/TypeScript's async/await with Promises.4 However, the underlying Task API in C# has its own characteristics and a richer set of functionalities compared to JavaScript Promises.107 For example, C# Tasks have properties like IsCompleted, IsFaulted, IsCanceled 110, and methods like ContinueWith for explicit continuation chaining (though await is generally preferred). C# also features a structured CancellationToken mechanism for cooperative cancellation of asynchronous operations 109, which is often more robust than ad-hoc cancellation strategies in Promise-based systems. While the high-level async/await flow feels similar, understanding the nuances of the Task API is essential for advanced C# asynchronous programming.
4.5.2. ValueTask<TResult>: When to Use for Performance
For performance-critical scenarios, especially in library code or frequently called methods where an asynchronous operation might complete synchronously (e.g., data is already cached), C# offers ValueTask and ValueTask<TResult>.112 These are struct-based alternatives to Task and Task<TResult>.
The primary benefit of ValueTask<T> is that it can avoid heap allocation if the operation completes synchronously, as it can wrap the result directly (being a struct).112 If the operation is genuinely asynchronous, ValueTask<T> will typically wrap an underlying Task<T> instance, so an allocation still occurs in that path.
Gotchas and Considerations for ValueTask<T>:
Consume Once: A ValueTask<T> should generally be awaited only once. Awaiting it multiple times can lead to undefined behavior or errors, especially if it's backed by a pooled IValueTaskSource object that might be reused.112 If multiple awaits are necessary, convert it to a Task<T> using .AsTask().
Struct Overhead: Being a struct, ValueTask<T> is larger than a Task<T> reference. Copying it (e.g., as a return value or parameter) can have a small overhead.
Complexity: It's generally more complex to use correctly than Task<T>.
The default choice for asynchronous methods should still be Task or Task<TResult>. ValueTask<T> is an optimization tool. It should be considered only after profiling indicates a significant performance bottleneck due to task allocations in hot paths, or when designing library APIs that might be consumed in such high-performance scenarios.
4.5.3. ConfigureAwait(false): Usage, Best Practices, Avoiding Deadlocks
By default, when an async method awaits a task, it captures the current SynchronizationContext (if one exists, like in UI applications or older ASP.NET versions).114 After the awaited task completes, the continuation (the rest of the method) is posted back to this captured context. This is usually desired in UI applications to safely update UI elements from the UI thread.
However, this context capturing can lead to deadlocks if the original thread (that owned the context) synchronously blocks waiting for the async method to complete (e.g., by calling .Result or .Wait() on the returned task). The original thread is blocked, and the async method's continuation is waiting for that same thread to become free to execute.
ConfigureAwait(false) is used to tell the awaited task that the continuation does not need to be executed on the captured context. Instead, the continuation can run on a Thread Pool thread.114

C#


public async Task DoWorkAsync()
{
    // Some work
    await SomeLibraryAsync().ConfigureAwait(false); // Continuation may run on a ThreadPool thread
    // More work that doesn't need the original context
}


Best Practices for ConfigureAwait(false) 114:
Library Code: General-purpose library code should almost always use ConfigureAwait(false) on all its internal awaits. Libraries should not assume they are running in a specific synchronization context and should not block callers that might have one.
Application-Level Code (UI/ASP.NET Classic): In UI event handlers or ASP.NET (classic) controller actions, if the code after an await needs to interact with UI elements or HttpContext, you should not use ConfigureAwait(false) (or use ConfigureAwait(true), which is the default) to ensure the continuation runs on the correct context.
ASP.NET Core: ASP.NET Core does not have a SynchronizationContext by default. Therefore, ConfigureAwait(false) is less critical for avoiding deadlocks but can still provide minor performance benefits by avoiding unnecessary attempts to capture and post to a non-existent context.115 It's often still recommended as a general good practice.
Consistency: To be effective in preventing deadlocks, ConfigureAwait(false) often needs to be used "all the way down" the asynchronous call chain.114 If a library method uses ConfigureAwait(false) but calls another async method that doesn't, the deadlock potential might still exist.
4.5.4. SynchronizationContext: Its Role in async/await
A SynchronizationContext represents a way to queue units of work (delegates) to a specific context, often a particular thread.116
UI frameworks (Windows Forms, WPF, MAUI) have a SynchronizationContext that marshals work to the UI thread.
Classic ASP.NET had a context to tie work to the current HTTP request.
Console applications and Thread Pool threads typically have no (or a default, thread-pool-based) SynchronizationContext.
When an async method is invoked, SynchronizationContext.Current is captured. When an await completes, if a non-null context was captured, the continuation of the async method is posted to that context.116 This is what allows UI updates to happen safely on the UI thread after an await.
The implicit capturing of SynchronizationContext.Current by await is a convenience that simplifies UI programming but is also the root cause of the deadlocks that ConfigureAwait(false) aims to prevent. A clear understanding of when a context exists and how await interacts with it is crucial for writing robust asynchronous C# code.
4.5.5. Dangers of async void
Methods marked as async void are generally discouraged, with a primary exception being top-level event handlers.118
Dangers:
Error Handling: Exceptions thrown from an async void method cannot be caught by the caller using a standard try-catch block around the method call. Such exceptions are typically propagated directly to the SynchronizationContext that was active when the async void method started, often leading to application crashes if unhandled.118
Testability: async void methods are difficult to unit test because the test runner cannot await their completion or easily catch exceptions thrown by them.118
Lifecycle Management: The caller of an async void method has no way to know when the asynchronous operations within it have completed.
When is async void acceptable?
The main legitimate use case is for event handlers whose signatures are defined as returning void (e.g., button.Click += async (s, e) => {... };). Even in this scenario, the best practice is to keep the async void handler minimal and have it immediately await an async Task method that contains the actual asynchronous logic.118

C#


private async void MyButton_Clicked(object sender, EventArgs e)
{
    try
    {
        await PerformClickActionsAsync();
    }
    catch (Exception ex)
    {
        // Log or display the error appropriately for an event handler
        LogError(ex);
    }
}

private async Task PerformClickActionsAsync()
{
    // All actual asynchronous work here
    await Task.Delay(1000);
    //... more async operations
}


This pattern localizes the async void risk and allows the core logic (PerformClickActionsAsync) to be testable and its exceptions properly managed.
4.6. Reflection and Attributes
Reflection allows a program to inspect its own metadata (or that of other assemblies) at runtime. Attributes are declarative tags that can be added to code elements to associate metadata with them.
4.6.1. Inspecting Assemblies, Types, and Members using System.Type
Reflection capabilities are primarily exposed through the System.Type class and other types in the System.Reflection namespace.122
Obtaining Type objects:
object.GetType(): Gets the runtime type of an instance.
typeof(TypeName): Gets the Type object for a known type at compile time.
Inspecting Metadata: Once you have a Type object, you can:
Get information about the type itself (name, namespace, base type, implemented interfaces, etc.).
Discover its members: methods (GetMethods()), properties (GetProperties()), fields (GetFields()), constructors (GetConstructors()), events (GetEvents()). These return collections of MethodInfo, PropertyInfo, etc., which provide detailed metadata about each member.
Examine attributes applied to the type or its members.
Reflection is the backbone of many.NET frameworks and tools, such as:
Serialization libraries (e.g., System.Text.Json, Newtonsoft.Json) use reflection to discover properties to serialize/deserialize.
Object-Relational Mappers (ORMs) like Entity Framework Core use reflection to map class properties to database columns and to read attributes for configuration.
Dependency Injection containers scan assemblies for types and their dependencies.
Unit testing frameworks use reflection to find test methods.
4.6.2. Custom Attributes: Definition and Application
Developers can define custom attributes by creating classes that inherit from System.Attribute.122 These custom attributes can then be applied to code elements to associate domain-specific metadata.

C#


// Define a custom attribute

public class AuthorAttribute : Attribute
{
    public string Name { get; }
    public double Version; // Positional parameter for constructor

    public AuthorAttribute(string name)
    {
        Name = name;
        Version = 1.0;
    }
}

// Apply the custom attribute

 // AllowMultiple = true
public class MyClassWithAuthors
{
   
    public void MyMethod() { /*... */ }
}


Attributes can have constructors (for positional parameters) and public fields/properties (for named parameters). The AttributeUsage attribute controls how a custom attribute can be used (e.g., which targets it applies to, whether it can be applied multiple times).
Custom attributes, when combined with reflection, enable developers to create powerful, declarative programming models and frameworks. For example, a custom validation framework might use attributes like or on model properties, and then use reflection at runtime to find these attributes and perform validation. This allows for expressive and configurable systems.
4.6.3. Late Binding and Dynamic Invocation
Reflection allows for late binding, where types can be loaded and their members invoked dynamically at runtime, even if the types are not known at compile time.122
Dynamic Instantiation: Activator.CreateInstance(type, constructorArgs) can create an instance of a type.
Dynamic Method Invocation: MethodInfo.Invoke(objectInstance, parameters) can call a method.
C#
Type myType = Type.GetType("MyNamespace.MyClass, MyAssembly");
if (myType!= null)
{
    object instance = Activator.CreateInstance(myType);
    MethodInfo method = myType.GetMethod("DoSomething");
    if (method!= null)
    {
        method.Invoke(instance, new object { "hello" });
    }
}


This is essential for scenarios like plugin architectures, scripting engines, or tools that need to operate on types discovered at runtime. However, dynamic invocation through reflection is significantly slower than direct, compile-time bound calls due to the overhead of metadata lookup and parameter marshalling. It also bypasses compile-time type safety for the invocation itself. Therefore, it should be used judiciously, primarily when static alternatives are not feasible. The dynamic keyword (Section 2.2.4) can sometimes offer a simpler syntax for late binding if the full power of reflection isn't required, but it also carries performance costs and a loss of static type safety.
4.7. Unsafe Code and Pointers
While C# is primarily a managed, memory-safe language, it provides an unsafe context for scenarios requiring direct memory manipulation, pointer arithmetic, or interoperability with native code.124 Using unsafe code requires enabling the "Allow unsafe code" compiler option for the project.
4.7.1. The unsafe Context and fixed Statement
unsafe Context: Code within a block marked unsafe, or methods/types declared as unsafe, can use pointers and perform operations not allowed in safe C#.
C#
public unsafe void ProcessData(byte* data, int length)
{
    for (int i = 0; i < length; i++)
    {
        data[i] = (byte)(data[i] * 2); // Pointer arithmetic and dereferencing
    }
}


fixed Statement: When working with pointers to data within managed objects (e.g., elements of an array, fields of a class/struct), the fixed statement is crucial.124 It "pins" the managed object in memory, preventing the Garbage Collector from moving it during the execution of the fixed block. This ensures that the pointer remains valid.
C#
int numbers = { 10, 20, 30 };
unsafe
{
    fixed (int* pNumbers = numbers) // or &numbers
    {
        // pNumbers is a valid pointer to the start of the 'numbers' array
        // within this block. The array 'numbers' will not be moved by the GC.
        int* current = pNumbers;
        for (int i = 0; i < numbers.Length; i++)
        {
            Console.WriteLine(*current);
            current++; // Pointer arithmetic
        }
    }
}


Unsafe code is a powerful but potentially dangerous feature. It bypasses C#'s inherent type and memory safety guarantees. It should be minimized, localized, and used only when absolutely necessary. Modern C# features like Span<T> and Memory<T> (see Section 4.8) often provide safe and efficient alternatives for many scenarios that previously required unsafe code, such as high-performance array manipulation.
4.7.2. Pointer Types and Direct Memory Manipulation
In an unsafe context, C# supports various pointer types 124:
type*: A pointer to a variable of type. The type must be an unmanaged type (primitives, enums, other pointer types, or structs containing only unmanaged types).
void*: A generic pointer to an unknown type. It cannot be dereferenced directly but can be cast to other pointer types.
Pointer operations include:
Dereferencing: *ptr (accesses the value at the pointer's address).
Address-of: &var (gets the address of a variable).
Member access: ptr->member (accesses a member of a struct via a pointer, equivalent to (*ptr).member).
Pointer arithmetic: ptr++, ptr + offset, etc. (arithmetic is scaled by the size of the referent type).
Comparison: ==, !=, <, >, etc.
While these capabilities offer fine-grained control for interop or micro-optimizations, they are error-prone (e.g., buffer overflows, dangling pointers) and make code harder to verify and maintain. They are generally a feature of last resort.
4.7.3. Interoperability Scenarios
A primary use case for unsafe code and pointers is Platform Invoke (P/Invoke), which allows C# code to call functions in unmanaged (native) libraries (e.g., C/C++ DLLs, OS APIs).124 Native functions often expect pointers as parameters or return pointers.

C#


using System.Runtime.InteropServices;

public class NativeMethods
{
   
    public static extern unsafe int memcpy(void* dest, void* src, int count);
}
//...
// byte source =...; byte destination = new byte[source.Length];
// unsafe
// {
//     fixed (byte* pSrc = source, pDest = destination)
//     {
//         NativeMethods.memcpy(pDest, pSrc, source.Length);
//     }
// }


Effective interop requires not only understanding C# pointers but also data marshalling: how.NET types are converted to and from their native representations. This can involve attributes like `` to control struct memory layout and [MarshalAs] to specify how parameters should be marshalled. This is a complex area beyond simple pointer usage.
4.8. Efficient Memory Management: Span<T>, Memory<T>, and stackalloc
To address the need for high-performance, low-allocation memory manipulation without always resorting to unsafe code,.NET introduced Span<T>, ReadOnlySpan<T>, Memory<T>, and ReadOnlyMemory<T>.
Span<T> and ReadOnlySpan<T>: These are ref struct types, meaning they are restricted to living on the stack.126 They provide a type-safe, allocation-free "view" or "window" over a contiguous region of memory. This memory can be part of a managed array, a string, stack-allocated memory (stackalloc), or even native memory. Because they don't own the memory and avoid allocations, operations like slicing a Span<T> are very efficient as they don't involve copying the underlying data.
C#
int numbers = { 0, 1, 2, 3, 4, 5, 6 };
Span<int> slice = numbers.AsSpan().Slice(2, 3); // Represents { 2, 3, 4 }
slice = 99; // Modifies numbers
// numbers is now { 0, 1, 99, 3, 4, 5, 6 }


Memory<T> and ReadOnlyMemory<T>: These types are similar to Span<T> but are regular structs (not ref structs), so they can be stored on the managed heap.127 This makes them suitable for use in async methods or as fields in classes, where Span<T> cannot be used. A Memory<T> can expose its data as a Span<T> via its .Span property for synchronous processing.
stackalloc: In an unsafe context (or with compiler support in safe contexts for certain types like Span<T>), stackalloc can be used to allocate a block of memory directly on the stack.126 This is extremely fast and avoids GC overhead. The allocated memory is automatically reclaimed when the method exits. stackalloc is often used in conjunction with Span<T> for temporary buffers.
C#
public unsafe void ProcessWithStackAlloc()
{
    Span<byte> buffer = stackalloc byte; // Allocates 1KB on the stack
    // Use buffer for temporary operations
}
// In C# 7.2+, stackalloc can be used in safe contexts if assigned to Span<T>
public void ProcessWithSafeStackAlloc()
{
    Span<int> numbers = stackalloc int {1, 2, 3};
    // Use numbers
}


These types are crucial for writing high-performance C# code, especially in scenarios involving data parsing, network I/O, and image processing, by minimizing allocations and data copying. Python and TypeScript developers typically don't have language features with this level of direct, safe control over memory buffers.
5. Project Structure and Deployment in.NET
Understanding how C# projects are organized and deployed is essential for building and distributing applications.
5.1. Solutions (.sln) and Projects (.csproj)
.NET development typically revolves around solutions and projects.129
Solution (.sln file): A solution is a container for one or more related projects.129 It organizes these projects, defines their build dependencies, and solution-level configurations (e.g., Debug, Release). The .sln file is a text-based file that Visual Studio and the dotnet CLI use to manage the overall application structure.132
Project (.csproj file): A project defines a single buildable unit, such as a class library (producing a .dll assembly), a console application (producing an .exe assembly), or a web application.129 The .csproj file is an XML-based MSBuild file that contains:
Project settings (e.g., target framework like net8.0, output type like Exe or Library).
A list of source code files included in the project (often implicit in modern SDK-style projects, including all .cs files in the project directory).
References to other projects within the same solution (<ProjectReference>).
References to external libraries (NuGet packages) (<PackageReference>).
Build configurations and compilation options.
A common architectural pattern, like Clean Architecture, often involves structuring a solution into multiple projects representing different layers (e.g., Domain, Application, Infrastructure, Web/Presentation).129 Each layer is a separate project, and dependencies between layers are managed via project references in the .csproj files. This promotes separation of concerns, testability, and maintainability. For example, the Application layer project would reference the Domain layer project, but the Domain layer would not reference the Application layer.
This multi-project solution structure in C#/.NET, where projects compile into distinct assemblies (DLLs), contrasts with typical TypeScript monorepo setups. TypeScript monorepos (often managed with tools like Lerna, Nx, or pnpm/yarn workspaces) also contain multiple "projects" or "packages," but the compilation and bundling process (e.g., using Webpack or Rollup) often aims to produce optimized JavaScript bundles for deployment, rather than distinct, independently versionable DLLs in the same way.NET does.133 While.NET projects can be packaged as NuGet packages for versioned distribution, inter-project dependencies within a single solution are typically direct project references, leading to a more tightly coupled build process for the entire solution compared to the potentially more independent package management within some TypeScript monorepo tools. Deployment units in.NET are often assemblies, whereas in TypeScript/JavaScript web projects, they are bundled script files.
5.2. Assemblies, Namespaces, and Code Organization
Assemblies: The fundamental unit of deployment, versioning, security, and type identity in.NET.6 An assembly is a collection of types and resources built to work together and form a logical unit of functionality. It's typically a .dll (Dynamic Link Library) or .exe (Executable) file. Each assembly contains a manifest with metadata about the assembly itself (name, version, culture, public key token) and the types it defines.6
Namespaces: Provide a hierarchical way to organize types (classes, structs, interfaces, enums, delegates) within an assembly and across assemblies to prevent naming conflicts.18 A fully qualified type name includes its namespace (e.g., System.Collections.Generic.List<T>). The using directive allows types in a namespace to be used without full qualification.
C#
using System.Collections.Generic; // Allows using List<T> instead of System.Collections.Generic.List<T>

namespace MyCompany.MyApp.DataAccess
{
    public class UserRepository { /*... */ }
}
File-scoped namespaces (C# 10+) simplify namespace declarations for an entire file:
C#
namespace MyCompany.MyApp.BusinessLogic; // Applies to the whole file

public class OrderService { /*... */ }


In C#, code is organized into namespaces (logical grouping for preventing name collisions and organizing code) and compiled into assemblies (physical deployment units, typically DLLs or EXEs).6 TypeScript uses ES modules (or older namespace/internal module patterns) for code organization.135 Each TypeScript file is typically its own module, with explicit import and export statements to manage dependencies. This is similar to Python's module system.
Key Differences in Code Organization and Deployment:
Compilation Unit: In C#, a project (.csproj) compiles into a single assembly. This assembly can contain multiple namespaces and types. In TypeScript, each .ts file is often treated as a module. Bundlers like Webpack or Rollup then combine these modules into one or more JavaScript files for deployment, especially for web applications.
Encapsulation Boundary: C# assemblies provide a strong encapsulation boundary. The internal access modifier restricts visibility to within the assembly. TypeScript modules also provide encapsulation, but the "assembly" concept as a formal deployment and versioning unit with its own manifest is specific to.NET.
Deployment: C# applications are deployed as a set of assemblies (the main executable and any referenced DLLs). For web applications, TypeScript is transpiled to JavaScript and bundled. Node.js TypeScript applications are transpiled to JavaScript and run with Node.js, with dependencies managed in node_modules.
Versioning:.NET assemblies have strong versioning capabilities, including support for side-by-side execution of different versions of the same assembly (though this can be complex). TypeScript/JavaScript package versioning is typically managed by npm or yarn via package.json and node_modules.
For developers coming from TypeScript, the concept of an "assembly" as a compiled, versionable, and deployable unit containing multiple namespaces and types is a key.NET concept to grasp. While TypeScript modules provide code organization,.NET assemblies add layers of deployment, versioning, and security context.
5.3..NET Runtime and Deployment Models
Modern.NET (since.NET Core) offers flexible deployment models:
Framework-Dependent Deployment (FDD): The application is deployed with only its own code and third-party dependencies. It relies on a globally installed.NET runtime on the target machine.138 This results in smaller deployment packages.
The application is typically launched using the dotnet command (e.g., dotnet MyWebApp.dll).
Self-Contained Deployment (SCD): The application is deployed with its own code, third-party dependencies, and the.NET runtime and libraries necessary to run it.138 This creates larger deployment packages but allows the application to run on machines without a pre-installed.NET runtime.
Produces a platform-specific executable (e.g., MyWebApp.exe on Windows).
Trimming (for SCDs): To reduce the size of self-contained deployments,.NET supports trimming.139 Trimming analyzes the application and removes unused code from the.NET runtime libraries and third-party assemblies included in the deployment. This is particularly useful for client-side applications like Blazor WebAssembly or mobile apps where deployment size is critical. Trimming can sometimes be aggressive and remove code that is used dynamically (e.g., via reflection), so careful testing is required. PublishTrimmed property in .csproj enables this.
These deployment models offer choices based on application needs, target environments, and deployment size considerations.
5.4. Application Domains (AppDomains) and AssemblyLoadContext - A Note on Evolution
In the traditional.NET Framework (Windows-only), Application Domains (AppDomains) were a crucial concept for isolation within a single process.140 They provided boundaries for security, reliability, versioning, and unloading assemblies. Multiple applications could run in separate AppDomains within one process, isolated from each other, without the overhead of separate processes.141 Benefits included fault isolation (an error in one AppDomain wouldn't crash others), the ability to unload an AppDomain (and its assemblies) without stopping the entire process, and scoped configuration.141 Threads could execute code within an AppDomain, and a single thread could cross AppDomain boundaries (though this involved marshalling).141
However, with the advent of.NET Core (and subsequent versions like.NET 5-8+), the concept of AppDomains has been largely deprecated and is not fully supported.140 The modern.NET platform moved towards cross-platform compatibility and microservices architectures, where process-level isolation (e.g., using containers like Docker) or lighter-weight in-process isolation mechanisms are preferred.
The replacement for some of AppDomain's assembly loading and isolation capabilities in modern.NET is the AssemblyLoadContext.140 AssemblyLoadContext provides a mechanism for loading assemblies into an isolated context, allowing for scenarios like loading multiple versions of the same assembly or dynamically loading and unloading plugins. However, AssemblyLoadContext does not provide the same strong isolation boundary (especially for security and fault tolerance) as.NET Framework AppDomains.140 For true application isolation in modern.NET, separate processes or containerization are the recommended approaches.
This evolution is important for developers to understand, especially if migrating older.NET Framework applications or encountering literature that heavily features AppDomains. While the underlying principles of isolation are still relevant, the mechanisms have changed in modern.NET.
6. Common Pitfalls and Gotchas in C#
Transitioning to C# from Python or TypeScript, while often smooth due to syntactic similarities, can present several "gotchas" or common pitfalls related to language differences and the.NET environment.
6.1. For Python Developers
6.1.1. Static Typing and Verbosity
Pitfall: Python's dynamic typing offers flexibility and conciseness. C#'s static typing requires explicit type declarations for variables, method parameters, and return types, which can feel verbose initially.1 The compiler enforces these types strictly.
C#
// C# - Explicit typing
int count = 10;
string name = "example";
List<User> users = new List<User>();


Concern: Developers might try to overuse the dynamic type to mimic Python's behavior, thereby losing the benefits of C#'s static type safety and performance.
Mitigation:
Embrace static typing: Understand that it catches errors early and improves code maintainability and tooling.
Use var for type inference when the type is obvious from the right-hand side of an assignment, reducing some verbosity without sacrificing static typing: var age = 30;.1
Focus on the benefits: better IntelliSense, refactoring support, and performance due to compile-time type information.
6.1.2. Case Sensitivity of Keywords and Identifiers
Pitfall: Python keywords are lowercase. C# keywords are also generally lowercase (e.g., class, int, if), but.NET BCL type names and often custom type names use PascalCase (e.g., String, List<T>, MyCustomClass).18 Identifiers are case-sensitive in both, but the conventions around casing differ.
Concern: Confusion or errors due to incorrect casing of types or keywords.
Mitigation: Familiarize oneself with C#/.NET naming conventions (PascalCase for types, methods, properties; camelCase for local variables and method parameters).18 Rely on IDE IntelliSense, which will suggest correct casing.
6.1.3. Differences in Standard Library (Python StdLib vs..NET BCL)
Pitfall: Python has a rich "batteries-included" standard library with modules for many common tasks (e.g., os.path, json, requests). C# has the extensive Base Class Library (BCL).1 While comprehensive, the BCL's organization and specific class/method names will be different.
File I/O: Python's open(), os.path vs. C#'s System.IO.File, System.IO.StreamReader, System.IO.Path.145
Collections: Python's list, dict, set vs. C#'s List<T>, Dictionary<TKey, TValue>, HashSet<T>, etc., in System.Collections.Generic. C# collections are strongly typed.
Networking: Python's requests (popular third-party) or http.client vs. C#'s System.Net.Http.HttpClient.147
Concern: Time spent finding equivalent functionalities and adapting to different APIs.
Mitigation: Invest time in learning the structure of the BCL, particularly common namespaces like System, System.IO, System.Collections.Generic, System.Linq, System.Net.Http. Use.NET API documentation extensively.
6.1.4. List Comprehensions vs. LINQ
Pitfall: Python's list/dict/set comprehensions are a concise and idiomatic way to create collections.1 C# uses LINQ (Language Integrated Query) for similar data manipulation tasks, which has a different syntax (query syntax or method syntax).1
Python
# Python: Squares of odd numbers
numbers = 
squares_of_odds = [x*x for x in numbers if x % 2!= 0]

C#
// C# LINQ equivalent
int numbers = { 1, 2, 3, 4, 5 };
var squaresOfOdds = numbers.Where(x => x % 2!= 0).Select(x => x * x).ToList();
// Or query syntax:
// var squaresOfOddsQuery = from x in numbers where x % 2!= 0 select x * x;
// var results = squaresOfOddsQuery.ToList();


Concern: Initial learning curve for LINQ syntax and its deferred execution model (see Section 4.4.4).
Mitigation: Study LINQ examples. Understand that LINQ is more powerful, capable of querying databases and XML, not just in-memory collections. Start with method syntax as it's often more straightforward for simple transformations.
6.1.5. Decorators vs. Attributes
Pitfall: Python decorators (@my_decorator) are a syntactic sugar for applying higher-order functions to modify or enhance functions/classes.1 C# uses attributes ([MyAttribute]) for declarative metadata, which can be queried at runtime using reflection to influence behavior (e.g., for serialization, validation, AOP-like features).1
Concern: Conceptual difference: Python decorators are more about direct behavioral modification via wrapping, while C# attributes are metadata that require reflection or framework support to act upon.
Mitigation: Understand that C# attributes are passive metadata. To achieve decorator-like behavior (e.g., logging, timing), one typically combines attributes with reflection or Aspect-Oriented Programming (AOP) frameworks (like PostSharp, or manual interception patterns). For simple "wrapping" behavior, higher-order functions or extension methods might be more direct in C#.
6.1.6. Duck Typing vs. Nominal Typing & Interfaces
Pitfall: Python's duck typing ("if it walks like a duck and quacks like a duck, it's a duck") allows objects to be used interchangeably if they support the required methods/attributes, regardless of their explicit type.1 C# uses nominal typing: types are compatible based on their declared names and explicit inheritance or interface implementation.5
Concern: Code that works in Python due to duck typing will cause compile-time errors in C# unless types explicitly implement a common interface or share a base class.
Mitigation: Learn to define and use interfaces in C# to establish contracts for behavior. If objects need to be treated polymorphically based on shared functionality, define an interface and have the classes implement it.
C#
// C# interface approach
public interface IQuackable { void Quack(); }
public class Duck : IQuackable { public void Quack() => Console.WriteLine("Quack!"); }
public class Person : IQuackable { public void Quack() => Console.WriteLine("I'm quacking like a duck!"); }

public void MakeItQuack(IQuackable quacker) => quacker.Quack();


6.1.7. Global Interpreter Lock (GIL) vs..NET Concurrency
Pitfall: CPython's GIL limits true parallelism for CPU-bound tasks in a single process by allowing only one thread to execute Python bytecode at a time.1 Python often uses multiprocessing for CPU-bound parallelism.
Concern: Misunderstanding C#'s threading capabilities or applying Python's GIL-constrained thinking.
Mitigation: C# and.NET have robust support for true multithreading and parallelism via System.Threading.Thread, Task Parallel Library (TPL), and async/await on Tasks, without a GIL-like limitation.1 Developers can leverage multi-core processors effectively for both I/O-bound and CPU-bound tasks within a single process.
6.1.8. Exception Handling Philosophy (EAFP vs. LBYL)
Pitfall: Python often encourages an "Easier to Ask for Forgiveness than Permission" (EAFP) style, using try-except blocks to handle expected errors or alternative code paths.160 C# tends to favor a "Look Before You Leap" (LBYL) approach for many common scenarios, using conditional checks or methods like TryParse before attempting an operation.160
Python
# Python EAFP
my_dict = {"key": "value"}
try:
    val = my_dict["another_key"]
except KeyError:
    val = "default"

C#
// C# LBYL equivalent
var myDict = new Dictionary<string, string> { { "key", "value" } };
string val;
if (!myDict.TryGetValue("another_key", out val))
{


Works cited
C# vs Python: A Look at Performance, Syntax, and Key Differences - CodePorting, accessed May 9, 2025, https://www.codeporting.com/blog/csharp_vs_python_a_look_at_performance_syntax_and_key_differences
C Sharp (programming language) - Wikipedia, accessed May 9, 2025, https://en.wikipedia.org/wiki/C_Sharp_(programming_language)
Transitioning from TypeScript and Python to C#: Key Takeaways - Innova, accessed May 9, 2025, https://www.innova.co.ke/transitioning-from-typescript-and-python-to-c-key-takeaways/
Tips for JavaScript and TypeScript Developers - A tour of C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tips-for-javascript-developers
TypeScript vs. C#: Key Differences & Similarities | FatCat Coders, accessed May 9, 2025, https://fatcatcoders.com/it-glossary/csharp/how-similar-are-c-and-typescript
.NET Framework - Wikipedia, accessed May 9, 2025, https://en.wikipedia.org/wiki/.NET_Framework
What is .NET Framework? A software development framework | .NET, accessed May 9, 2025, https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet-framework
4. Base Class Library Overview - C# Essentials [Book] - O'Reilly Media, accessed May 9, 2025, https://www.oreilly.com/library/view/c-essentials/0596000790/ch04.html
.NET-Stack/.NETFrameworkBasic/readme.md at master · AdyKalra ..., accessed May 9, 2025, https://github.com/AdyKalra/.NET-Stack/blob/master/.NETFrameworkBasic/readme.md
Overview of ASP.NET Core | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-9.0
Comparing WebForms, MVC, ASP.NET Core and React/Next.js - Progress Software, accessed May 9, 2025, https://www.progress.com/blogs/comparing-webforms-mvc-aspnet-core-react-nextjs
C# development with Visual Studio - Visual Studio (Windows ..., accessed May 9, 2025, https://learn.microsoft.com/en-us/visualstudio/get-started/csharp/?view=vs-2022
Using .NET in Visual Studio Code, accessed May 9, 2025, https://code.visualstudio.com/docs/languages/dotnet
C# Dev Kit FAQ - Visual Studio Code, accessed May 9, 2025, https://code.visualstudio.com/docs/csharp/cs-dev-kit-faq
Getting Started with C# in VS Code, accessed May 9, 2025, https://code.visualstudio.com/docs/csharp/get-started
NET SDK overview - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/core/sdk
A tour of the C# language - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/overview
C Sharp syntax - Wikipedia, accessed May 9, 2025, https://en.wikipedia.org/wiki/C_Sharp_syntax
Tips for Python Developers - A tour of C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tips-for-python-developers
Reference types - C# reference | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types
Types - C# language specification - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/types
Data Types - C# (C Sharp) - Codecademy, accessed May 9, 2025, https://www.codecademy.com/resources/docs/c-sharp/data-types
C# Data Types | GeeksforGeeks, accessed May 9, 2025, https://www.geeksforgeeks.org/c-sharp-data-types/
A Thorough Guide to Bond for C# - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/bond/manual/bond_cs.html
What is the difference between a reference type and value type in c#? - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/5057267/what-is-the-difference-between-a-reference-type-and-value-type-in-c
Stack Vs. Heap In C#: What Every Developer Should Know | Nile Bits, accessed May 9, 2025, https://www.nilebits.com/blog/2024/06/stack-vs-heap-in-csharp/
docs/docs/csharp/programming-guide/types/boxing-and-unboxing ..., accessed May 9, 2025, https://github.com/dotnet/docs/blob/main/docs/csharp/programming-guide/types/boxing-and-unboxing.md
Type Inference vs. Static/Dynamic Typing - Herb Sutter, accessed May 9, 2025, https://herbsutter.com/2008/06/20/type-inference-vs-staticdynamic-typing/
Design with nullable reference types - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/tutorials/nullable-reference-types
How did nullable reference types go for you? : r/csharp - Reddit, accessed May 9, 2025, https://www.reddit.com/r/csharp/comments/1i9niuj/how_did_nullable_reference_types_go_for_you/
TSConfig Option: strictNullChecks - TypeScript, accessed May 9, 2025, https://www.typescriptlang.org/tsconfig/strictNullChecks.html
Why I am not getting warnings about StrictNullChecks in typescript - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/53740494/why-i-am-not-getting-warnings-about-strictnullchecks-in-typescript
Nullable Attributes - Essential C#, accessed May 9, 2025, https://essentialcsharp.com/nullable-attributes
Start dealing with Nullable Reference Types! - Xebia, accessed May 9, 2025, https://xebia.com/blog/start-dealing-with-nullable-reference-types/
Operators - Packt+ | Advance your knowledge in tech, accessed May 9, 2025, https://www.packtpub.com/en-us/product/learn-c-programming-9781789805864/chapter/chapter-2-data-types-and-operators-2/section/operators?chapterId=2
C# Operators | GeeksforGeeks, accessed May 9, 2025, https://www.geeksforgeeks.org/c-sharp-operators/
Jump Statement in C#: Break, Continue, Goto, Return and Throw - ScholarHat, accessed May 9, 2025, https://www.scholarhat.com/tutorial/csharp/jump-statement-in-csharp
Flow control in C# - Endjin, accessed May 9, 2025, https://endjin.com/blog/2022/01/flow-control-in-csharp
Patterns - Pattern matching using the is and switch expressions. - C# ..., accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns
Pattern matching overview - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/functional/pattern-matching
C# Object Oriented Programming 2022 - ВКонтакте, accessed May 9, 2025, https://vk.com/@wrefet-c-object-oriented-programming
A Complete Guide To Object Oriented Programming In C# - C# Corner, accessed May 9, 2025, https://www.c-sharpcorner.com/UploadFile/84c85b/object-oriented-programming-using-C-Sharp-net/
Structs - C# language specification - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/structs
Structure types - C# reference | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct
Why are mutable structs “evil”? [closed] - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/441309/why-are-mutable-structs-evil
Beginners Guide To C# Struct vs Class (With Code Examples) | Zero To Mastery, accessed May 9, 2025, https://zerotomastery.io/blog/c-sharp-struct-vs-class/
OO Programming Modifiers (C#) (msdn.microsoft.com), accessed May 9, 2025, https://thales.cs.unipi.gr/modules/document/file.php/TMB121/OOP_modifiers.pdf
override modifier - C# reference | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/override
sealed modifier - C# reference - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/sealed
Method Overloading and Method Overriding in C# - ScholarHat, accessed May 9, 2025, https://www.scholarhat.com/tutorial/csharp/method-overloading-and-method-overriding-in-csharp
Access Modifiers - C# reference - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers
Access Modifiers - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers
What are some common pitfalls in Python programming? - Quora, accessed May 9, 2025, https://www.quora.com/What-are-some-common-pitfalls-in-Python-programming
C# Interface: Definition, Examples, Best Practices, and Pitfalls - SubMain Software, accessed May 9, 2025, https://blog.submain.com/c-interface-definition-examples/
Distinguishing the Explicit and Implicit Interface Implementation in C# - Pluralsight, accessed May 9, 2025, https://www.pluralsight.com/resources/blog/guides/distinguish-explicit-and-implicit-interface-implementation-csharp
A Tour of Default Interface Methods for C# ("traits") · Issue #288 · dotnet/csharplang - GitHub, accessed May 9, 2025, https://github.com/dotnet/csharplang/issues/288
Default interface methods - C# feature specifications | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-8.0/default-interface-methods
Computer Knowledge Centre - C# - Classes - Google Sites, accessed May 9, 2025, https://sites.google.com/site/computerbookscentre/home/c---introduction-features/c-components/c---classes
Init only setters - C# feature specifications | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-9.0/init
C# Init-Only Setters Property - LoginRadius, accessed May 9, 2025, https://www.loginradius.com/blog/engineering/csharp-init-only-setters-property
Using indexers (C# Programming Guide) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/using-indexers
C# 8 – Excelling at Indexes - Twilio, accessed May 9, 2025, https://www.twilio.com/en-us/blog/c-sharp-8-excelling-at-indexes
Constructors (C# programming guide) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors
C# Constructor Syntax & Types Explained - Learn Default Constructor in Hindi | Iqra Academy. - Iqra Technology, accessed May 9, 2025, https://iqratechnology.com/academy/c-sharp-training/c-constructor/
Call Chain of Constructors in C# - Pluralsight, accessed May 9, 2025, https://www.pluralsight.com/resources/blog/guides/call-chain-constructors-csharp
Implement a Dispose method - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/implementing-dispose
How to Correctly Implement IDisposable Interface in C# - Code Maze, accessed May 9, 2025, https://code-maze.com/csharp-how-to-correctly-implement-idisposable-interface/
using statement - ensure the correct use of disposable objects - C# ..., accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using
Pattern based using and using declarations - C# feature specifications | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-8.0/using
Fundamentals of garbage collection - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals
Large object heap (LOH) on Windows - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/large-object-heap
Memory Management in .NET - Garbage Collector - CSHARK, accessed May 9, 2025, https://www.cshark.com/memory-management-in-net-garbage-collector/
Large Object Heap in .NET: Best Practices - Codejack, accessed May 9, 2025, https://codejack.com/2024/11/large-object-heap-in-net-best-practices/
Finalizers - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/finalizers
When should I use GC.SuppressFinalize()? - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/151051/when-should-i-use-gc-suppressfinalize
GC Class (System) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.gc?view=net-9.0
.NET Memory Internals | Infosec, accessed May 9, 2025, https://www.infosecinstitute.com/resources/reverse-engineering/net-memory-internals/
GC.SuppressFinalize(Object) Method (System) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.gc.suppressfinalize?view=net-9.0
GC.GetTotalMemory(Boolean) Method (System) | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.gc.gettotalmemory?view=net-9.0
GC.AddMemoryPressure(Int64) Method (System) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.gc.addmemorypressure?view=net-9.0
GC.WaitForPendingFinalizers Method (System) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.gc.waitforpendingfinalizers?view=net-9.0
Record types - C# - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/records
Records - C# reference - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record
C# Record Vs Class (How It Works For Developers) - IronPDF, accessed May 9, 2025, https://ironpdf.com/blog/net-help/csharp-record-vs-class/
Generic classes and methods - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics
What does "where T : class, new()" mean? - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/4737970/what-does-where-t-class-new-mean
in (Generic Modifier) - C# reference - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/in-generic-modifier
Covariance and Contravariance in Generics - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/generics/covariance-and-contravariance
Work with delegate types in C# - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/
Anonymous Methods - Essential C#, accessed May 9, 2025, https://essentialcsharp.com/anonymous-methods
Lambda expressions and anonymous functions - C# reference - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions
Delegates vs. events - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/distinguish-delegates-events
Delegates in C#: A Practical Guide - Nearsure, accessed May 9, 2025, https://www.nearsure.com/blog/delegates-in-c-a-practical-guide
C# Delegates and Events: Best Practices for Event-Driven Applications - W3computing.com, accessed May 9, 2025, https://www.w3computing.com/articles/csharp-delegates-events-best-practices-event-driven-applications/
windows-dev-docs/uwp/winrt-components/custom-events-and-event-accessors-in-windows-runtime-components.md at docs - GitHub, accessed May 9, 2025, https://github.com/MicrosoftDocs/windows-dev-docs/blob/docs/uwp/winrt-components/custom-events-and-event-accessors-in-windows-runtime-components.md
Handling and raising events - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/events/
Are Lambda expressions in C# closures? - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/9591476/are-lambda-expressions-in-c-sharp-closures
Standard Query Operators Overview - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/linq/standard-query-operators/
Write LINQ queries - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/linq/get-started/write-linq-queries
Common Pitfalls in LINQ Queries and How to Avoid Them - DEV ..., accessed May 9, 2025, https://dev.to/ferhatacar/common-pitfalls-in-linq-queries-and-how-to-avoid-them-42dd
Beware of multiple enumeration of IEnumerable - David's Blog, accessed May 9, 2025, https://www.davidhome.net/blog/beware-of-multiple-enumeration-of-ienumerable/
7 Common MISTAKES made by C# developers (+ How to avoid them) - ByteHide, accessed May 9, 2025, https://blog.ndepend.com/7-common-mistakes-made-by-c-developers-how-to-avoid-them/
Deferred execution example - LINQ to XML - .NET - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/linq/deferred-execution-example
The pitfalls of LINQ deferred execution - marcusclasson, accessed May 9, 2025, https://marcusclasson.com/2014/08/18/the-pitfalls-with-linq-deferred-execution/comment-page-1/
Asynchronous programming scenarios - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/async-scenarios
Asynchronous programming - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/
How to control C# Task (async/await in same way as javascript Promise)? - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/70992438/how-to-control-c-sharp-task-async-await-in-same-way-as-javascript-promise
Should I be using await Task.WhenAll rather than Task.WaitAll in a Web API controller, accessed May 9, 2025, https://stackoverflow.com/questions/75688310/should-i-be-using-await-task-whenall-rather-than-task-waitall-in-a-web-api-contr
C# async, await, Task, CancellationToken equivalent in JavaScript - Website-Development, accessed May 9, 2025, https://website-development.ch/blog/c-sharp-async-task-cancellationtoken-javascript
Difference Between Await and ContinueWith Keyword in C#, accessed May 9, 2025, https://www.c-sharpcorner.com/UploadFile/pranayamr/difference-between-await-and-continuewith-keyword-in-C-Sharp/
Task Continuations: Checking IsFaulted, IsCompleted, and TaskStatus - Jeremy Bytes, accessed May 9, 2025, https://jeremybytes.blogspot.com/2015/01/task-continuations-checking-isfaulted.html
asynchronous - Why would one use Task
Task
c# - Why ConfigureAwait(false) does not work while Task.Run ..., accessed May 9, 2025, https://stackoverflow.com/questions/36654472/why-configureawaitfalse-does-not-work-while-task-run-works
When to use ConfigureAwait(false) : r/dotnet - Reddit, accessed May 9, 2025, https://www.reddit.com/r/dotnet/comments/7nk0uj/when_to_use_configureawaitfalse/
SynchronizationContext Class (System.Threading) | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.threading.synchronizationcontext?view=net-9.0
C# Async/Await Explained: Complete Guide with Examples [2025] - NDepend Blog, accessed May 9, 2025, https://blog.ndepend.com/c-async-await-explained/
Async/Await - Best Practices in Asynchronous Programming ..., accessed May 9, 2025, https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming
The Dangers of Async Void | Dissecting the Code, accessed May 9, 2025, https://sergeyteplyakov.github.io/Blog/csharp/2025/01/28/The_Dangers_Of_Async_Void.html
www.devleader.ca, accessed May 9, 2025, https://www.devleader.ca/2024/03/07/async-void-methods-in-c-the-dangers-that-you-need-to-know#:~:text=The%20Dangers%20of%20async%20void%20Methods%20in%20C%23,-The%20common%20theme&text=Error%20Propagation%3A%20async%20void%20methods,that%20can%20crash%20the%20application.
async void Methods In C# - The Dangers That You Need to Know - Dev Leader, accessed May 9, 2025, https://www.devleader.ca/2024/03/07/async-void-methods-in-c-the-dangers-that-you-need-to-know
Attributes and reflection - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/reflection-and-attributes/
Tutorial: Define and read custom attributes. - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/reflection-and-attributes/attribute-tutorial
Unsafe code, pointers to data, and function pointers - C# reference ..., accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/unsafe-code
Unsafe code - C# language specification - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/unsafe-code
Improve C# code performance with Span - NDepend Blog, accessed May 9, 2025, https://blog.ndepend.com/improve-c-code-performance-with-spant/
Memory and Span usage guidelines - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/standard/memory-and-spans/memory-t-usage-guidelines
Why can I return a ref struct but not a stackalloc span? : r/csharp - Reddit, accessed May 9, 2025, https://www.reddit.com/r/csharp/comments/1gs38o9/why_can_i_return_a_ref_struct_but_not_a/
C# Solution Structure | TutorialsEU, accessed May 9, 2025, https://tutorials.eu/c-sharp-solution-structure/
Structure your modeling solution - Visual Studio (Windows) | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/visualstudio/modeling/structure-your-modeling-solution?view=vs-2022
What purpose does a .csproj file serve? - Quora, accessed May 9, 2025, https://www.quora.com/What-purpose-does-a-csproj-file-serve
Project Solution (.sln) file - Visual Studio (Windows) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/visualstudio/extensibility/internals/solution-dot-sln-file?view=vs-2022
What I've learnt about monorepos with .NET - Francis Phan, accessed May 9, 2025, https://www.phan.nz/posts/doing-monorepo-dotnet
c# - What are the benefits of multiple projects over namespaces in a solution?, accessed May 9, 2025, https://softwareengineering.stackexchange.com/questions/414586/what-are-the-benefits-of-multiple-projects-over-namespaces-in-a-solution
Documentation - Namespaces and Modules - TypeScript, accessed May 9, 2025, https://www.typescriptlang.org/docs/handbook/namespaces-and-modules.html
TypeScript Namespace vs Module: Essential Guide to Code Organization - Ceos3c, accessed May 9, 2025, https://www.ceos3c.com/javascript/typescript-namespace-vs-module-differences/
Module vs Namespace - Import vs Require Typescript - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/38582352/module-vs-namespace-import-vs-require-typescript
Different Types of .NET Core Deployment, accessed May 9, 2025, https://www.microfocus.com/documentation/visual-cobol/vc70/EclUNIX/GUID-6BC68A29-60F6-49CD-913C-AFA4BD214D11.html
Trim self-contained applications - .NET | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/core/deploying/trimming/trim-self-contained
Understanding AppDomains in .NET Framework and .NET 5 to 8 | Joche Ojeda, accessed May 9, 2025, https://www.jocheojeda.com/2024/03/07/understanding-appdomains-in-net-framework-and-net-5-to-8/
Application domains - .NET Framework | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/framework/app-domains/application-domains
ASP.NET vs Python: Picking Your Tech Champion - WireFuture, accessed May 9, 2025, https://wirefuture.com/post/asp-net-vs-python-picking-your-tech-champion
.NET Coding Conventions - C# | Microsoft Learn, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions
Python vs. C#: Frameworks, Libraries and Ecosystems - OnStartups, accessed May 9, 2025, https://www.onstartups.com/tabid/3339/bid/125/Python-vs-C-Frameworks-Libraries-and-Ecosystems.aspx
Path Class (System.IO) - Learn Microsoft, accessed May 9, 2025, https://learn.microsoft.com/en-us/dotnet/api/system.io.path?view=net-9.0
os.path — Common pathname manipulations — Python 3.13.3 documentation, accessed May 9, 2025, https://docs.python.org/3/library/os.path.html
Python HTTP Clients: Requests vs. HTTPX vs. AIOHTTP - Speakeasy, accessed May 9, 2025, https://www.speakeasy.com/blog/python-http-clients-requests-vs-httpx-vs-aiohttp
Python Request to C# - Stack Overflow, accessed May 9, 2025, https://stackoverflow.com/questions/75478168/python-request-to-c-sharp
Python List Comprehensions and Generators for C# Developers, accessed May 9, 2025, https://markheath.net/post/python-list-comprehensions-and
List comprehension - Wikipedia, accessed May 9, 2025, https://en.wikipedia.org/wiki/List_comprehension
Python Internals Explained: A Comprehensive Technical Guide for C# Developers, accessed May 9, 2025, https://thedeveloperspace.com/python-internals-explained-a-comprehensive-technical-guide-for-c-developers/
Python Decorators - Tutorialspoint, accessed May 9, 2025, https://www.tutorialspoint.com/python/python_decorators.htm
About Decorators In Python - Blog of Jérémie Litzler, accessed May 9, 2025, https://iamjeremie.me/post/2025-03/about-decorators-in-python/
Documentation - Decorators - TypeScript, accessed May 9, 2025, https://www.typescriptlang.org/docs/handbook/decorators.html
Duck Typing - Devopedia, accessed May 9, 2025, https://devopedia.org/duck-typing
Duck Typing in Python: Writing Flexible and Decoupled Code, accessed May 9, 2025, https://realpython.com/duck-typing-python/
Nominal And Structural Typing, accessed May 9, 2025, https://eclipse.dev/n4js/features/nominal-and-structural-typing.html
Documentation - TypeScript for Java/C# Programmers - TypeScript, accessed May 9, 2025, https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html
C# Vs. Python: Choosing the Best Programming Language for Your ..., accessed May 9, 2025, https://www.orientsoftware.com/blog/csharp-vs-python/
Idiomatic Python: EAFP versus LBYL - Microsoft for Python ..., accessed May 9, 2025, https://devblogs.microsoft.com/python/idiomatic-python-eafp-versus-lbyl/
Pythonic style – EAFP versus LBYL - Packt+ | Advance your knowledge in tech, accessed May 9, 2025, https://www.packtpub.com/en-in/product/the-python-apprentice-9781788293181/chapter/exceptions-6/section/pythonic-style-eafp-versus-lbyl-ch06lvl1sec67
EAFP and LBYL coding styles | Pydon't - mathspp, accessed May 9, 2025, https://mathspp.com/blog/pydonts/eafp-and-lbyl-coding-styles
