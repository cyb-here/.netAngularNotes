## CASTING - Implicit vs Explicit

### 🔹 Implicit Casting (Type Conversion)
Automatic type conversion performed by the compiler when there is no risk of data loss.
- **Key Point:** Smaller → larger type (safe conversion).
- **Example:**
```csharp
int num = 100;       // int (32-bit)
double d = num;      // implicit casting: int → double
Console.WriteLine(d); // prints 100
```

## 🔹 Explicit Casting

**Definition:**  
Manual type conversion using a cast operator or conversion methods.

**Example:**
```csharp
double d = 9.78;     
int num = (int)d;    // explicit casting: double → int
Console.WriteLine(num); // prints 9 (fractional part lost)
```

## 🥊BOXING UNBOXING
Boxing and unboxing are mechanisms to convert between value types (like int, struct) and reference types (object).
-> Have huge performance impact due to frequent boxing unboxing.
```csharp
Boxing
int num = 42;          // value type
object obj = num;      // boxing: int → object
Console.WriteLine(obj); // prints 42

UNBOXING
object obj = 42;       // boxed int
int num = (int)obj;    // unboxing: object → int
Console.WriteLine(num); // prints 42

```


## HEAP vs STACK
STACK - Stores Primitive Data Types, Variable, Data, Memory location are at same location.
HEAP - Stores Object with pointer

## Garbage Collector
Is a background process, And Cleans any **Unused & Managed Resources.**

### IL Code - Intermediate Language Code, Partially Compiled  Code.  
### JIT - Just In Time compiler - Converts IL code to Machine Code.

![alt text]({D64DAE2B-7ECA-4973-B317-CD699F5B06EB}.png)

IL Example
# C# vs .Net Framwework
### C# - Programming Language Features (Syntaxes, Symentics, Loops, If Else)
### .NET - Framework Features such as [ Common Language Runtime (CLR), Liabraries, Garbage Collector. ]

<details>
  <summary>1. Compilation and Execution</summary>

  When we write a C# program, it gets compiled into Intermediate Language (IL) code, which is platform-independent.  
  The CLR then uses a Just-In-Time (JIT) compiler to convert the IL code into machine-specific code while the program runs.

</details>

<details>
  <summary>2. Services Provided by CLR</summary>

  - CLR handles automatic memory management through Garbage Collection, preventing memory leaks.  
  - It ensures that data types are used correctly and safely.  
  - The CLR checks the IL code for security risks before running it.

</details>

<details>
  <summary>3. Cross-Language Integration</summary>

  CLR allows code from different .NET languages (C#, VB.NET, F#) to work together seamlessly through the Common Type System (CTS).

</details>

<details>
  <summary>Key Components of CLR</summary>

  - **Common Language Specification (CLS):** Defines common rules so that code written in different languages can interoperate.  
    - *Managed Code:* The MSIL code which is managed by the CLR is known as the Managed Code. For managed code CLR provides three .NET facilities.  
    - *Unmanaged Code:* Before .NET development, programming languages like COM Components & Win32 API do not generate MSIL code. These are not managed by CLR but by the Operating System.

  - **JIT Compiler:** Converts IL code into machine code specific to the system at runtime, optimizing execution.  
  - **Garbage Collector:** Automatically manages memory by freeing unused objects, reducing the need for manual memory management.  

  - **Common Type System (CTS):** Ensures that different data types across languages are understood by CLR and can work together.  
    - *Value Types:* Store the value directly into the memory location. These types work with stack mechanisms only. CLR allocates memory at compile time.  
    - *Reference Types:* Contain a memory address of value because reference types don’t store the variable value directly in memory. These types work with heap mechanism. CLR allocates memory at runtime.

</details>


