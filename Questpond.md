

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


