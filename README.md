# Modern_Java

## References:

- **The Java Tutorials (Oracle, archived but still relevant)** – Great for new and intermediate devs; covers classes, objects, packages, JVM basics, and core libraries in a structured way. [interviewbit](https://www.interviewbit.com/blog/java-architecture/)
- **Java Platform, Standard Edition Technical Documentation (Oracle)** – API docs plus guides for JVM, JRE, JDK, memory model, and concurrency; good “source of truth” to back up what you’ve summarized. [interviewbit](https://www.interviewbit.com/blog/java-architecture/)

- **vFunction – “Java Architecture: Components with Examples”** – Explains JVM/JRE/JDK, memory areas (heap, stack, metaspace), JIT, layered architecture (presentation, business, data access), and patterns like MVC, microservices, DDD. This aligns almost 1:1 with your sections on JVM, memory layout, and high‑level architecture and can help devs see how those concepts show up in real application design. [vfunction](https://vfunction.com/blog/java-architecture/)
- **InterviewBit – “Java Architecture – Detailed Explanation”** – Concise explanation of compilation → bytecode → JVM → machine code, plus clear breakdown of JDK/JRE/JVM roles, which complements your compilation architecture and JVM sections. [interviewbit](https://www.interviewbit.com/blog/java-architecture/)
- **NareshIT – “Components of Java Architecture”** – Focuses on the “compile + interpret” pipeline, JVM responsibilities (load, verify, execute), and JVM memory parts (method area, heap, native stack, etc.), which backs up your JVM diagrams and memory explanations. [nareshit](https://nareshit.com/blogs/what-are-the-components-of-java-architecture)
- **GeeksforGeeks – “How JVM Works – JVM Architecture”** – Useful for deeper dives into method area, heap, stack, PC register, native method stack, and class loader/JNI; good as a reference when teaching or debugging memory and thread issues. [geeksforgeeks](https://www.geeksforgeeks.org/java/how-jvm-works-jvm-architecture/)
  - **“JVM & Memory Architecture”** → link to vFunction, GeeksforGeeks JVM, NareshIT/LS Raheja PDF. [vfunction](https://vfunction.com/blog/java-architecture/)
  - “Java Platform Components (JDK, JRE, JVM)” → link to InterviewBit and Oracle docs. [interviewbit](https://www.interviewbit.com/blog/java-architecture/)
  - “From Architecture to Real Projects” → link to booking‑system topic, one or two curated reservation-system repos, and the JDBC hotel tutorial. [github](https://github.com/topics/booking-system?l=java&o=desc&s=updated)
- In your **Wiki**, create short pages like:
  - “JVM Memory Deep Dive” – summarize method area/heap/stack/PC/native stack and point to one or two external resources for each. [geeksforgeeks](https://www.geeksforgeeks.org/java/how-jvm-works-jvm-architecture/)
  - “From Java Architecture to Application Layers” – show how your OOP and JVM sections relate to layered architecture (presentation, service, repository) and microservices examples from vFunction. [vfunction](https://vfunction.com/blog/java-architecture/)


- **“JAVA ARCHITECTURE AND COMPONENTS: Java Virtual Machine” (LS Raheja PDF)** – Short, academic-style summary of compilation to bytecode, JVM role, and core components (JVM/JRE/JDK). This matches your README structure and is easy to skim. [lsraheja](https://www.lsraheja.org/wp-content/uploads/2020/04/SYBSCIT-SEM-IV-Core-Java-Unit-I-II.pdf)


- **Hotel Reservation / Booking system projects in Java (GitHub topic)** – The booking-system topic aggregates Java repos (bus booking, salon booking, airline seat management, etc.) that show layered architectures, persistence, and typical service boundaries in real projects. [github](https://github.com/topics/booking-system?l=java&o=desc&s=updated)
- **Example hotel reservation repo (Java)** – A hotel reservation management project fully in Java; useful to inspect package structure, model/service/controller layering, and basic persistence patterns. [github](https://github.com/zeevolution/hotel-reservation)
- **YouTube + GitHub: “Hotel Reservation System using JDBC in Java”** – Step-by-step tutorial plus source code; shows how JDBC, database schema, and application layers fit together. Good for juniors to connect your abstract architecture sections to a realistic CRUD-style system. [youtube](https://www.youtube.com/watch?v=OBq6vuBCpuE)


\
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

