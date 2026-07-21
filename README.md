# C# Generics - Part 1: Introduction to Generics

# 📖 Introduction

Imagine you're building a storage box.

Sometimes you want to store:

- Books
- Mobile Phones
- Laptops
- Clothes

Would you create a different box for every item?

```
BookBox

PhoneBox

LaptopBox

ClothesBox
```

That would create a lot of duplicate code.

Instead, you create **one box** that can hold **any type of item**.

```
Box<T>
```

Today it holds books.

Tomorrow it holds laptops.

Next week it holds mobile phones.

The **box doesn't change**.

Only the **type of item** changes.

This is the basic idea behind **Generics**.

---

# What are Generics?

Generics allow us to write **classes, methods, interfaces, delegates, and collections** that work with **different data types** while maintaining **type safety**.

Instead of writing the same code repeatedly for different types, we write it **once** and let the compiler replace the type later.

> **Definition:** Generics allow you to create reusable, type-safe code by using type parameters instead of fixed data types.

---

# Why Were Generics Introduced?

Before Generics were added to C#, developers often used the `object` type.

Why?

Because every type in C# inherits from `object`.

Example

```csharp
object value;

value = 10;
value = "Hello";
value = true;
```

It works because everything can be stored as an `object`.

But this creates several problems.

---

# Problems Before Generics

## Problem 1: No Type Safety

Consider this code:

```csharp
ArrayList list = new ArrayList();

list.Add(10);
list.Add("Hello");
list.Add(true);
```

What is inside the list?

```
10

"Hello"

true
```

Different types are mixed together.

Now imagine another developer assumes that every item is an integer.

```csharp
int number = (int)list[1];
```

What happens?

The second item is actually a string.

At runtime, the application throws an exception.

```
InvalidCastException
```

The compiler couldn't detect the mistake because everything was stored as `object`.

---

## Problem 2: Type Casting

Whenever data is retrieved, it must be converted back.

```csharp
object value = 100;

int number = (int)value;
```

This process is called **casting**.

If you forget to cast, the code won't compile.

If you cast to the wrong type, the program crashes at runtime.

---

## Problem 3: Boxing and Unboxing

When a value type is stored as an `object`, the CLR performs **boxing**.

```
int

↓

object
```

When it is converted back,

the CLR performs **unboxing**.

```
object

↓

int
```

Both operations consume CPU time and memory.

We'll study Boxing and Unboxing in detail later, but it's important to know that Generics help reduce unnecessary boxing for value types.

---

# How Do Generics Solve These Problems?

Instead of storing everything as `object`, Generics let us specify the type.

Example

```csharp
List<int> numbers = new List<int>();

numbers.Add(10);
numbers.Add(20);
numbers.Add(30);
```

Now the compiler knows:

```
Only integers are allowed.
```

If someone writes

```csharp
numbers.Add("Hello");
```

The code won't even compile.

The mistake is caught during compilation instead of at runtime.

---

# What Does `<T>` Mean?

The `<T>` is called a **type parameter**.

It acts like a placeholder.

Think of it as an empty label.

```
Box<T>

↓

T = ?
```

When we create an object, we replace `T`.

Example

```csharp
Box<int>
```

Now

```
T = int
```

Another example

```csharp
Box<string>
```

Now

```
T = string
```

The same class works with different types.

---

# Why is the Letter `T` Used?

`T` is just a naming convention.

It stands for **Type**.

You could technically write

```csharp
Box<DataType>
```

or

```csharp
Box<MyType>
```

But almost every C# developer uses `T`.

Common conventions include:

```
T

TKey

TValue

TItem

TResult

TInput

TOutput
```

These names make the purpose of the type parameter clearer.

---

# Internal Working (Most Important)

Suppose we create

```csharp
Box<int>
```

Internally, the process looks like this:

```
Generic Class

↓

Box<T>

↓

Compiler Sees

↓

Box<int>

↓

Replace T with int

↓

Generate Type Information

↓

CLR Uses int Version

↓

Program Executes
```

Now create

```csharp
Box<string>
```

Internally

```
Box<T>

↓

T = string

↓

CLR Uses string Version
```

Notice something important.

**You wrote the class only once.**

The type changes automatically.

---

# Real-World Analogy

Imagine a water bottle factory.

The factory manufactures one bottle design.

That bottle can contain:

```
Water

Juice

Milk

Cold Drink
```

The bottle is the same.

Only the contents change.

Similarly,

```
Box<T>
```

is the same class.

Only the data type changes.

---

# Example

Imagine we create a storage box.

```
Storage Box

↓

Book
```

Tomorrow

```
Storage Box

↓

Laptop
```

The box didn't change.

Only its contents changed.

That's exactly what Generics do.

---

# Generic Syntax

A generic class is declared like this:

```csharp
public class Box<T>
{
}
```

`T` represents the type that will be supplied later.

When creating objects:

```csharp
Box<int> intBox = new Box<int>();

Box<string> stringBox = new Box<string>();

Box<double> doubleBox = new Box<double>();
```

The same class now works with three different types.

---

# Where Are Generics Used?

Generics are used throughout .NET.

Examples

Collections

```csharp
List<T>

Dictionary<TKey, TValue>

Queue<T>

Stack<T>
```

Methods

```csharp
Swap<T>()
```

Classes

```csharp
Repository<T>
```

Interfaces

```csharp
IEnumerable<T>
```

Delegates

```csharp
Func<T>

Action<T>

Predicate<T>
```

Frameworks

- ASP.NET Core
- Entity Framework Core
- Dependency Injection
- LINQ
- Collections Library

If you build .NET applications, you'll use Generics almost every day.

---

# Advantages

- Code reuse
- Compile-time type safety
- Better performance
- Eliminates unnecessary casting
- Reduces boxing and unboxing
- Easier maintenance
- Cleaner APIs

---

# Disadvantages

- Can be difficult for beginners.
- Complex generic constraints can reduce readability.
- Advanced topics like variance require deeper understanding.

---

# Common Mistakes

## Thinking `T` is a Variable

Incorrect

```
T is a variable
```

Correct

```
T is a type parameter.
```

---

## Assuming Generics Accept Any Operation

Not every operation is valid for every type.

For example, you can't assume every `T` supports arithmetic.

That's why C# provides **generic constraints**, which we'll study later.

---

## Confusing `object` with Generics

`object`

- Accepts everything.
- Requires casting.
- Can cause runtime errors.

Generics

- Accept only the specified type.
- No casting required.
- Type-safe.

---

# Interview Questions

### What are Generics?

Generics allow developers to write reusable, type-safe code by using type parameters instead of fixed data types.

---

### Why were Generics introduced?

To eliminate problems caused by using `object`, such as type casting, runtime errors, and unnecessary boxing/unboxing.

---

### What does `T` represent?

`T` is a type parameter that acts as a placeholder for an actual type.

---

### What is the biggest advantage of Generics?

Compile-time type safety while enabling code reuse.

---

### How are Generics different from using `object`?

`object` stores any type but requires casting and may cause runtime errors.

Generics enforce the type at compile time, avoiding casting and improving safety.

---

# Summary

- Generics allow one piece of code to work with multiple data types.
- They improve code reuse and type safety.
- `T` is a placeholder for a type.
- Generics eliminate many problems associated with using `object`.
- They reduce unnecessary casting and boxing.
- Generics are used throughout modern .NET development, from collections to ASP.NET Core and Entity Framework.


# C# Generics - Part 2: Generic Methods

# 📖 Introduction

In the previous chapter, we learned how a **generic class** can work with different data types.

Example:

```csharp
Box<int>

Box<string>

Box<double>
```

The entire class became reusable.

But what if **only one method** needs to be reusable?

Should we make the whole class generic?

**No.**

That's why C# provides **Generic Methods**.

A Generic Method allows **only the method** to accept different data types, while the rest of the class remains normal.

---

# What is a Generic Method?

A **Generic Method** is a method that uses one or more **type parameters** instead of fixed data types.

Instead of writing separate methods for different types, we write one method that works for all compatible types.

> **Definition:** A Generic Method is a method that uses type parameters, allowing the same method implementation to operate on different data types with compile-time type safety.

---

# Why Do We Need Generic Methods?

Imagine you want to print values.

Without Generic Methods

```csharp
void Print(int value)

void Print(string value)

void Print(double value)

void Print(bool value)
```

Every new type requires another overload.

---

Using a Generic Method

```csharp
Print<T>(T value)
```

Now one method works for

```
int

string

double

bool

Employee

Student

Product
```

No duplicate code.

---

# Problem Without Generic Methods

Suppose we want to swap two values.

Without Generics

```csharp
Swap(int a, int b)

Swap(string a, string b)

Swap(double a, double b)

Swap(Employee a, Employee b)
```

As the number of types grows, the number of methods also grows.

This violates the **DRY (Don't Repeat Yourself)** principle.

---

Using a Generic Method

```csharp
Swap<T>(ref T first, ref T second)
```

One method works for every type.

---

# Generic Method Syntax

```csharp
public void Print<T>(T value)
{
    Console.WriteLine(value);
}
```

Let's break it down.

```
Print<T>
```

The `<T>` declares a **type parameter**.

```
(T value)
```

The parameter type is now determined when the method is called.

---

# How Does the Compiler Know What T Is?

Consider this call.

```csharp
Print(100);
```

The compiler sees

```
100

↓

int
```

So it automatically treats the call as

```csharp
Print<int>(100);
```

Now consider

```csharp
Print("Hello");
```

The compiler infers

```
string
```

and treats it as

```csharp
Print<string>("Hello");
```

This process is called **Type Inference**.

---

# What is Type Inference?

Type Inference means the compiler determines the generic type automatically based on the arguments you pass.

Example

```csharp
Print(10);
```

Compiler infers

```
T = int
```

Example

```csharp
Print(3.14);
```

Compiler infers

```
T = double
```

Example

```csharp
Print(true);
```

Compiler infers

```
T = bool
```

Most of the time, you don't need to specify `<T>` yourself.

---

# Explicit Type Arguments

Although the compiler usually infers the type, you can specify it manually.

Example

```csharp
Print<int>(100);

Print<string>("Hello");

Print<double>(9.81);
```

Both approaches are valid.

The compiler simply skips type inference because you've already provided the type.

---

# Multiple Type Parameters

A method can have more than one type parameter.

Example

```csharp
Compare<T1, T2>(T1 first, T2 second)
```

Now the method accepts two different types.

Example

```csharp
Compare(100, "Alice");
```

Compiler infers

```
T1 = int

T2 = string
```

This is useful when working with keys and values, source and destination objects, or any two different types.

---

# Internal Working (Most Important)

Suppose we write:

```csharp
Print(100);
```

Internally, the process looks like this:

```
Call Generic Method

↓

Print(100)

↓

Compiler Examines Argument

↓

Argument = int

↓

Replace T with int

↓

Generate Type Information

↓

CLR Executes Print<int>()
```

Now consider:

```csharp
Print("Hello");
```

Internally:

```
Call Generic Method

↓

Print("Hello")

↓

Argument = string

↓

Replace T with string

↓

CLR Executes Print<string>()
```

You wrote the method only once.

The compiler and CLR handle the type substitution.

---

# Generic Method vs Method Overloading

Without Generics

```
Print(int)

Print(double)

Print(string)

Print(bool)
```

Many methods.

---

With Generics

```
Print<T>()
```

One method.

---

# Real-World Analogy

Imagine a courier service.

Without a generic process:

```
DeliverBook()

DeliverLaptop()

DeliverPhone()

DeliverDocument()
```

Different procedures for each item.

Instead, the courier follows one process:

```
Deliver<T>()
```

The delivery steps are the same.

Only the package changes.

---

# Example

Suppose you have a display machine.

It can display:

```
Number

↓

Text

↓

Price

↓

Employee Name
```

The display mechanism never changes.

Only the data being displayed changes.

That's exactly what a Generic Method does.

---

# Where Are Generic Methods Used?

Generic Methods are common in .NET.

Examples

Collections

```csharp
List<T>.Add(T item)
```

LINQ

```csharp
FirstOrDefault<T>()
```

Sorting

```csharp
Sort<T>()
```

Searching

```csharp
Find<T>()
```

Entity Framework

```csharp
Set<TEntity>()
```

Dependency Injection

```csharp
GetService<T>()
```

Testing Frameworks

```csharp
Assert.IsType<T>()
```

You'll use Generic Methods frequently in modern .NET development.

---

# Advantages

- Eliminates duplicate methods.
- Compile-time type safety.
- Cleaner code.
- Easier maintenance.
- Better reusability.
- Supports type inference.

---

# Disadvantages

- Complex generic methods can become difficult to read.
- Some operations require generic constraints, which we'll learn in the next chapters.

---

# Common Mistakes

## Thinking Every Generic Method Needs Explicit Types

Incorrect

```csharp
Print<int>(100);
```

when

```csharp
Print(100);
```

is sufficient.

Let the compiler infer the type whenever possible.

---

## Confusing Generic Methods with Generic Classes

A Generic Class makes the entire class generic.

A Generic Method makes only the method generic.

---

## Assuming T Supports Every Operation

Incorrect

```csharp
T result = a + b;
```

Not every type supports the `+` operator.

Use generic constraints when necessary.

---

# Best Practices

- Prefer type inference unless specifying the type improves clarity.
- Use meaningful type parameter names (`T`, `TKey`, `TValue`, `TResult`).
- Keep generic methods focused on one responsibility.
- Add constraints only when required.

---

# Interview Questions

### What is a Generic Method?

A Generic Method uses one or more type parameters, allowing the same method implementation to work with different data types.

---

### Why use a Generic Method instead of method overloading?

It reduces duplicate code and improves maintainability while preserving type safety.

---

### What is Type Inference?

Type Inference is the compiler's ability to determine the generic type automatically from the method arguments.

---

### Can a Generic Method have multiple type parameters?

Yes.

For example:

```csharp
Compare<T1, T2>(T1 first, T2 second)
```

---

### When should you specify the generic type explicitly?

Only when the compiler cannot infer the type correctly or when doing so makes the code clearer.

---

# Summary

- Generic Methods make individual methods reusable across multiple data types.
- They reduce the need for repetitive method overloads.
- The compiler usually infers the generic type automatically.
- You can specify the type explicitly when necessary.
- Generic Methods are used extensively throughout the .NET Framework and modern C# libraries.






# C# Generics - Part 2: Generic Methods

# 📖 Introduction

In the previous chapter, we learned how a **generic class** can work with different data types.

Example:

```csharp
Box<int>

Box<string>

Box<double>
```

The entire class became reusable.

But what if **only one method** needs to be reusable?

Should we make the whole class generic?

**No.**

That's why C# provides **Generic Methods**.

A Generic Method allows **only the method** to accept different data types, while the rest of the class remains normal.

---

# What is a Generic Method?

A **Generic Method** is a method that uses one or more **type parameters** instead of fixed data types.

Instead of writing separate methods for different types, we write one method that works for all compatible types.

> **Definition:** A Generic Method is a method that uses type parameters, allowing the same method implementation to operate on different data types with compile-time type safety.

---

# Why Do We Need Generic Methods?

Imagine you want to print values.

Without Generic Methods

```csharp
void Print(int value)

void Print(string value)

void Print(double value)

void Print(bool value)
```

Every new type requires another overload.

---

Using a Generic Method

```csharp
Print<T>(T value)
```

Now one method works for

```
int

string

double

bool

Employee

Student

Product
```

No duplicate code.

---

# Problem Without Generic Methods

Suppose we want to swap two values.

Without Generics

```csharp
Swap(int a, int b)

Swap(string a, string b)

Swap(double a, double b)

Swap(Employee a, Employee b)
```

As the number of types grows, the number of methods also grows.

This violates the **DRY (Don't Repeat Yourself)** principle.

---

Using a Generic Method

```csharp
Swap<T>(ref T first, ref T second)
```

One method works for every type.

---

# Generic Method Syntax

```csharp
public void Print<T>(T value)
{
    Console.WriteLine(value);
}
```

Let's break it down.

```
Print<T>
```

The `<T>` declares a **type parameter**.

```
(T value)
```

The parameter type is now determined when the method is called.

---

# How Does the Compiler Know What T Is?

Consider this call.

```csharp
Print(100);
```

The compiler sees

```
100

↓

int
```

So it automatically treats the call as

```csharp
Print<int>(100);
```

Now consider

```csharp
Print("Hello");
```

The compiler infers

```
string
```

and treats it as

```csharp
Print<string>("Hello");
```

This process is called **Type Inference**.

---

# What is Type Inference?

Type Inference means the compiler determines the generic type automatically based on the arguments you pass.

Example

```csharp
Print(10);
```

Compiler infers

```
T = int
```

Example

```csharp
Print(3.14);
```

Compiler infers

```
T = double
```

Example

```csharp
Print(true);
```

Compiler infers

```
T = bool
```

Most of the time, you don't need to specify `<T>` yourself.

---

# Explicit Type Arguments

Although the compiler usually infers the type, you can specify it manually.

Example

```csharp
Print<int>(100);

Print<string>("Hello");

Print<double>(9.81);
```

Both approaches are valid.

The compiler simply skips type inference because you've already provided the type.

---

# Multiple Type Parameters

A method can have more than one type parameter.

Example

```csharp
Compare<T1, T2>(T1 first, T2 second)
```

Now the method accepts two different types.

Example

```csharp
Compare(100, "Alice");
```

Compiler infers

```
T1 = int

T2 = string
```

This is useful when working with keys and values, source and destination objects, or any two different types.

---

# Internal Working (Most Important)

Suppose we write:

```csharp
Print(100);
```

Internally, the process looks like this:

```
Call Generic Method

↓

Print(100)

↓

Compiler Examines Argument

↓

Argument = int

↓

Replace T with int

↓

Generate Type Information

↓

CLR Executes Print<int>()
```

Now consider:

```csharp
Print("Hello");
```

Internally:

```
Call Generic Method

↓

Print("Hello")

↓

Argument = string

↓

Replace T with string

↓

CLR Executes Print<string>()
```

You wrote the method only once.

The compiler and CLR handle the type substitution.

---

# Generic Method vs Method Overloading

Without Generics

```
Print(int)

Print(double)

Print(string)

Print(bool)
```

Many methods.

---

With Generics

```
Print<T>()
```

One method.

---

# Real-World Analogy

Imagine a courier service.

Without a generic process:

```
DeliverBook()

DeliverLaptop()

DeliverPhone()

DeliverDocument()
```

Different procedures for each item.

Instead, the courier follows one process:

```
Deliver<T>()
```

The delivery steps are the same.

Only the package changes.

---

# Example

Suppose you have a display machine.

It can display:

```
Number

↓

Text

↓

Price

↓

Employee Name
```

The display mechanism never changes.

Only the data being displayed changes.

That's exactly what a Generic Method does.

---

# Where Are Generic Methods Used?

Generic Methods are common in .NET.

Examples

Collections

```csharp
List<T>.Add(T item)
```

LINQ

```csharp
FirstOrDefault<T>()
```

Sorting

```csharp
Sort<T>()
```

Searching

```csharp
Find<T>()
```

Entity Framework

```csharp
Set<TEntity>()
```

Dependency Injection

```csharp
GetService<T>()
```

Testing Frameworks

```csharp
Assert.IsType<T>()
```

You'll use Generic Methods frequently in modern .NET development.

---

# Advantages

- Eliminates duplicate methods.
- Compile-time type safety.
- Cleaner code.
- Easier maintenance.
- Better reusability.
- Supports type inference.

---

# Disadvantages

- Complex generic methods can become difficult to read.
- Some operations require generic constraints, which we'll learn in the next chapters.

---

# Common Mistakes

## Thinking Every Generic Method Needs Explicit Types

Incorrect

```csharp
Print<int>(100);
```

when

```csharp
Print(100);
```

is sufficient.

Let the compiler infer the type whenever possible.

---

## Confusing Generic Methods with Generic Classes

A Generic Class makes the entire class generic.

A Generic Method makes only the method generic.

---

## Assuming T Supports Every Operation

Incorrect

```csharp
T result = a + b;
```

Not every type supports the `+` operator.

Use generic constraints when necessary.

---

# Best Practices

- Prefer type inference unless specifying the type improves clarity.
- Use meaningful type parameter names (`T`, `TKey`, `TValue`, `TResult`).
- Keep generic methods focused on one responsibility.
- Add constraints only when required.

---

# Interview Questions

### What is a Generic Method?

A Generic Method uses one or more type parameters, allowing the same method implementation to work with different data types.

---

### Why use a Generic Method instead of method overloading?

It reduces duplicate code and improves maintainability while preserving type safety.

---

### What is Type Inference?

Type Inference is the compiler's ability to determine the generic type automatically from the method arguments.

---

### Can a Generic Method have multiple type parameters?

Yes.

For example:

```csharp
Compare<T1, T2>(T1 first, T2 second)
```

---

### When should you specify the generic type explicitly?

Only when the compiler cannot infer the type correctly or when doing so makes the code clearer.

---

# Summary

- Generic Methods make individual methods reusable across multiple data types.
- They reduce the need for repetitive method overloads.
- The compiler usually infers the generic type automatically.
- You can specify the type explicitly when necessary.
- Generic Methods are used extensively throughout the .NET Framework and modern C# libraries.
