---
title: Integration of Objective-C libraries with Xamarin iOS
date: '2016-07-27 05:20:00'
categories:
- objective-c
- xamarin ios
- pinvoke
- cocoapods
summary: ''
layout: post
---

# Create Unit Tests!

- Subclass ApiCtorInitTest
- 

# Objective-C Property Selectors

Assume the property ```@property (readwrite) int foo;```

Objective-C:
* The property is read/write
* The return type is int.
* The selector (pair!) is "foo" (get operations) and "setFoo:") (set operations)

In C# IDL:
```csharp
[Export ("foo")]
int Foo { get; set; }
```

# Objective-C Method Selectors

## Example 1
Assume the method ```(float) getNumber)```

Objective-C:
* "-" means it is an instance method
* The return type is float
* The selector name is "getNumber"

C# IDL:

```csharp
[Export("getNumber")]
float GetNumber();
```

## Example 2
Assumbe the following method ```+(float) add:(int) first and:(int) second;```

Selector is created by removing type declaration and paramater name, internally within Objective-C selectors are just strings.

Objective-C:
* "+" means it is a static method
* The return type is float
* Takes two int arguments
* Selector name is "add:and:"

C# IDL

```csharp
[Export("add:and:")]
float Add (int first, int second)
```

# Class Declarations

|                         | Objective-C                     | C#                                                    | Mapping Result                         |
|-------------------------|---------------------------------|-------------------------------------------------------|----------------------------------------|
| Class Declaration       | ```@interface Foo : Bar```      | ```[BaseType( typeof (Bar))] interfaceFoo```          | C# class                               |
| Class Adopting Protocol | ```@inteface Foo : Bar <Pro>``` | ```[BaseType (typeof (Bar))] interface Foo : Pro```    | C# class with inlined protocol methods |
| Protocol                | ```@protocol Foo <Bar>```       | ```[BaseType (typeof (Bar))] [Model] interface Foo``` | C# class with methods to override      |
| Category                | ```@interface Foo(Cute)```      | ```[BaseType(typeof(Foo))] interface Cute```          | C# extensions method class             |


# Extension Methods
* Also known as categories
* https://stackoverflow.com/questions/2159034/extension-methods-in-objective-c
* https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/CustomizingExistingClasses/CustomizingExistingClasses.html#//apple_ref/doc/uid/TP40011210-CH6-SW1

# Basics of Bindings
* Binding Classes
  * Exactly the same as C# classes  
* Binding Protocols
  * Are like C# interfaces, except they have optional methods (i.e. don't have to implement the entire contract) which makes them weak interfaces.
  * C# doesn't like optional methods on an inferface but can be worked around.
  
  
* Methods, PRoperties
 * Type mappings
 * Arrays
 * Strings
* Delegate classses (and events)
* Exposing Weak and Strong Types
* Binding Blocks
  * Blocks are like callbacks in C# 

# Example

```objc
typedef NS_ENUM(NSInteger, SDStatusBarManagerBluetoothState)
{
  SDStatusBarManagerBluetoothHidden = 0,
  SDStatusBarManagerBluetoothVisibleDimmed,
  SDStatusBarManagerBluetoothVisibleConnected
};

@interface SDStatusBarManager : NSObject

@property (copy, nonatomic) NSString *carrierName;
@property (copy, nonatomic) NSString *timeString;
@property (assign, nonatomic, readonly) BOOL usingOverrides;
@property (assign, nonatomic) SDStatusBarManagerBluetoothState bluetoothState;

// two instance methods
- (void)enableOverrides;
- (void)disableOverrides;

// a static method that belongs to the type
+ (SDStatusBarManager *)sharedInstance;
+
```



# ObjectiveC
 - Constructors in objective c is done via instance methods that follow a naming convention (`initWithString(xxxx`))
 - `+(NSArray*) getAllBeans` - means that it is a static method because of the plus sign.

# Datatypes
Objective-C
.NET

* Objective-C is a dynamic lanaugage, with some type safety but the majority is untyped - arrays, dictionaries.

# Themes
* Adding C# type information to a dynamic language (Obj-C).
* Convert C _DEFINES_ into ENUMS.
* Translate Objective-C idioms into C# idoms.
* Rename Objective-C methods into methods that conform with the .NET framework design guidelines.

# Enums
* Exposed in Objective-C as constants, need converting to C# enum idoims.


# Enumerations and Structures

# Interface Definition

# Concepts
* Zero-copy marshalling (i.e. use existing pointers in memory, no need to copy data)

# Packaging
* Do not need to distribute the native `libmagicbeans.a` just distribute the `libmagicbeans.dll`

# Reading
* https://msdn.microsoft.com/en-us/library/ms229042(v=vs.110).aspx
* 
# Watching
* https://youtu.be/DV7cGR0ySgo
