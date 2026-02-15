# Modern_Java

# 1️⃣ Java Program Structural Architecture

Every Java program follows this hierarchy:

```
Project
 └── Package
      └── Class
           ├── Fields
           ├── Constructors
           └── Methods
```

Example:

```java
package org.totalbeginner.tutorial;

public class Person {
    private String name;
    private int maximumBooks;

    public Person() {
        name = "unknown name";
        maximumBooks = 3;
    }

    public String getName() {
        return name;
    }
}
```

### Core Structural Components

| Component   | Purpose               |
| ----------- | --------------------- |
| Package     | Organizes classes     |
| Class       | Blueprint for objects |
| Field       | Stores object state   |
| Constructor | Initializes object    |
| Method      | Defines behavior      |

---

# 2️⃣ JVM Architecture (The Engine)

Java is **compiled but platform independent**.

### Step 1 — Compile

```bash
javac Person.java
```

Produces:

```
Person.class  (bytecode)
```

### Step 2 — Run

```bash
java Person
```

The `.class` file runs inside the **Java Virtual Machine (JVM)**.

---

## JVM Core Components

```
        Class Loader
              ↓
        Bytecode Verifier
              ↓
        Runtime Data Areas
              ↓
        Execution Engine
```

---

## Class Loader

Loads `.class` files into memory.

Types:

* Bootstrap ClassLoader
* Extension ClassLoader
* Application ClassLoader

---

## Bytecode Verifier

Ensures:

* No illegal memory access
* Stack integrity
* Type safety

This is why Java is secure.

---

## Runtime Data Areas

This is extremely important.

### JVM Memory Layout

```
┌─────────────────────┐
│ Method Area         │
├─────────────────────┤
│ Heap                │
├─────────────────────┤
│ Stack (per thread)  │
├─────────────────────┤
│ PC Register         │
├─────────────────────┤
│ Native Method Stack │
└─────────────────────┘
```

---

### Heap

Stores:

* Objects
* Instance variables

Example:

```java
Person p1 = new Person();
```

`p1` → reference on Stack
`new Person()` → object stored in Heap

---

### Stack

Stores:

* Local variables
* Method calls
* References

Each thread has its own stack.

---

### Method Area

Stores:

* Class definitions
* Static variables
* Constant pool

---

# 3️⃣ Java Memory Model (Object Lifecycle)

Example:

```java
Person p = new Person();
```

### What Happens:

1. Stack frame created
2. Reference variable `p` created
3. `new` allocates memory in heap
4. Constructor runs
5. Reference stored in stack

When no references exist → Garbage Collector removes object.

---

# 4️⃣ Core OOP Architecture in Java

Java is built on 4 Pillars:

---

## 🔹 Encapsulation

Hide internal data.

```java
private int maximumBooks;
```

Access via:

```java
public int getMaximumBooks()
```

Why?

* Prevent invalid state
* Control logic
* Maintain invariants

---

## 🔹 Abstraction

Expose what matters, hide complexity.

Example:
You call:

```java
System.out.println()
```

You don’t know how it prints — abstraction.

---

## 🔹 Inheritance

Reuse behavior.

```java
public class Student extends Person {
}
```

---

## 🔹 Polymorphism

Same method, different behavior.

```java
Person p = new Student();
```

---

# 5️⃣ Execution Flow of a Java Program

Entry point:

```java
public static void main(String[] args)
```

Breakdown:

| Keyword       | Meaning                |
| ------------- | ---------------------- |
| public        | Accessible everywhere  |
| static        | No object required     |
| void          | Returns nothing        |
| String[] args | Command-line arguments |

Execution Flow:

```
JVM starts
 ↓
Loads Main class
 ↓
Calls main()
 ↓
Executes instructions
 ↓
Terminates when stack empty
```

---

# 6️⃣ Static vs Instance Architecture

## Instance Members

Belong to object.

```java
private String name;
```

Requires:

```java
Person p = new Person();
```

---

## Static Members

Belong to class.

```java
public static int population;
```

Access:

```java
Person.population
```

Stored in Method Area.

---

# 7️⃣ Packages and Namespaces

```java
package org.totalbeginner.tutorial;
```

Why packages?

* Prevent naming conflicts
* Logical grouping
* Large system organization

Example large architecture:

```
com.company.project
    ├── model
    ├── service
    ├── controller
    ├── util
```

---

# 8️⃣ Java Type System Architecture

Java is:

* Strongly typed
* Statically typed

Two type categories:

### Primitive Types

Stored directly in stack.

```
int
double
boolean
char
```

---

### Reference Types

Stored in heap, referenced by stack.

```
String
Person
ArrayList
```

---

# 9️⃣ Compilation Architecture

```
Source Code (.java)
        ↓
Java Compiler (javac)
        ↓
Bytecode (.class)
        ↓
JVM
        ↓
Machine Code (JIT compiler)
        ↓
CPU Execution
```

Java uses:

* JIT (Just-In-Time compilation)
* HotSpot optimization
* Runtime optimization

---

# 🔟 Garbage Collection Architecture

Java automatically manages memory.

GC tracks:

* Reachable objects
* Unreachable objects

Algorithms:

* Mark & Sweep
* Generational GC
* G1 GC (modern default)

---

# 11️⃣ Thread Architecture

Each thread has:

* Own Stack
* Own PC register

But shares:

* Heap
* Method Area

That’s why concurrency needs:

* Synchronization
* Locks
* Volatile

---

# 12️⃣ High-Level Java Program Architecture Summary

```
                Java Program
                     │
         ┌───────────┴───────────┐
         │                       │
     Source Code            JVM Runtime
         │                       │
  Classes / Methods        Heap / Stack
         │                       │
     Bytecode             Execution Engine
         │                       │
      JIT Compiler → Native Machine Code
```

---

