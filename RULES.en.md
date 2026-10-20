# Hardcore OOP Rules Specification

**Rule specification version: v0.1.1**

This document is a compatible English translation of the authoritative Hardcore OOP rules.

The authoritative Japanese version is [RULES.md](RULES.md). If there is any discrepancy in interpretation, the Japanese version takes precedence.

## Terms

- **Object**: An instance of a class that has behavior at runtime.
- **Public method**: A method that can be invoked directly by users of the type.
- **Responsibility**: A single role that gives an object one reason to change.
- **Operation**: A single action performed to achieve one purpose.
- **Dependency**: A relationship in which one class uses the behavior of another type or object.
- **Entry Point**: The single point from which program execution starts.
- **Composition Root**: The place where objects are created and dependencies are assembled, normally adjacent to the Entry Point.
- **Model**: A type representing data or domain state.

## Rules

### HC-OOP-001: At most one public method

An object must not expose multiple public methods.

The object must provide at most one operation that can be invoked directly from outside.

### HC-OOP-002: One object, one responsibility

An object must not have two or more responsibilities.

If multiple responsibilities exist, they must be separated into different objects.

### HC-OOP-003: One function, one operation

A function or method must not perform two or more independent operations.

If multiple independent purposes exist, they must be separated into different functions or objects.

### HC-OOP-004: Do not inherit from concrete classes

A class must not inherit from anything other than an interface or an abstract class.

Concrete-to-concrete inheritance is prohibited. Composition must be preferred for reuse.

### HC-OOP-005: One public type per file

A file must not contain two or more public types.

Public classes, interfaces, enums, records, and other publicly visible types are limited to at most one per file.

### HC-OOP-006: Only one public concrete class

The entire system must contain only one public concrete class.

Public interfaces and public abstract classes are not subject to this restriction.

### HC-OOP-007: Match namespaces to the folder structure

Logical ownership such as namespaces, packages, or modules must match the physical folder structure.

Logical code ownership and filesystem ownership must not define conflicting structures.

### HC-OOP-008: No processing outside classes

No processing may exist outside classes except the minimum startup code required by the Entry Point.

Top-level functions, business logic at module scope, and global executable logic are prohibited.

### HC-OOP-009: Do not split one class across files

The same class must not be defined across multiple files.

Features such as partial classes that split a single class definition across files must not be used.

### HC-OOP-010: Models must be identifiable

A model class must be clearly identifiable as a model from its name, location, namespace, or other structural information.

It must not be necessary to inspect the implementation in detail merely to determine whether a class is a model.

### HC-OOP-011: At most one direct caller

A class must not be called directly from multiple locations.

In the dependency graph, an executable class must have at most one parent.

### HC-OOP-012: Dependencies form a tree rooted at the Entry Point

Dependencies between executable classes must form a tree with the Entry Point as the single root.

Every executable class must be reachable from the Entry Point, and circular dependencies are prohibited.

### HC-OOP-013: Non-inheritable classes must be explicitly sealed

If the language can prohibit inheritance, every class not intended for inheritance must explicitly prohibit it.

Examples include `sealed` in C# and `final` in Java.

### HC-OOP-014: Dependencies are provided through constructors

Every dependency required by an object must be provided explicitly through its constructor.

Service Locator, global dependency lookup, hidden dependency resolution, and similar mechanisms are prohibited.

### HC-OOP-015: No global mutable state

The system must not contain globally shared mutable state.

Mutable static fields and mutable internal state in globally shared Singletons are prohibited.

### HC-OOP-016: Constructors only initialize

A constructor must perform only the initialization required to establish the object.

Database access, file access, network communication, logging, business logic, and similar operations must not be executed by constructors.

### HC-OOP-017: Depend on abstractions for collaborators

When depending on a collaborating object that provides behavior, the dependency must use an interface or abstract class whenever the language can express it.

Types that represent models or values themselves are excluded from this restriction.

### HC-OOP-018: No runtime type-based branching

Behavior must not branch based on the concrete runtime type of an object.

Mechanisms such as `instanceof`, `is`, `GetType()`, or switches on class names must not be used for business-logic branching.

### HC-OOP-019: No downcasting

An object handled through an abstraction must not be downcast to a concrete type by its consumer.

Required behavior must be expressed by the abstraction itself.

### HC-OOP-020: Models are immutable

Models should be immutable after construction.

When state must change, a new model must be created rather than mutating the existing model.

### HC-OOP-021: No public mutable fields

An object must not expose fields that external code can modify directly.

Exposed state must be represented in a form that consumers cannot mutate directly.

### HC-OOP-022: Centralize object creation in the Composition Root

Creation of dependency objects must be centralized in the Composition Root.

Ordinary executable classes must not directly construct their own dependencies. Dependencies must be created in the Composition Root and provided through constructors.

### HC-OOP-023: No duplicate function names within the same scope

A scope must not contain multiple functions or methods with the same name.

This prohibition applies even when parameter counts, parameter types, generic parameters, return types, or other parts of the signature differ.

Function and method overloading is therefore prohibited. A function name alone must uniquely identify the operation within its scope.

## Structural consequence

A runtime structure that satisfies these rules conceptually has the following form:

```text
Entry Point
└── Application
    ├── A
    │   └── B
    └── C
        └── D
```

Each executable class normally:

- has one responsibility,
- exposes one public operation,
- has at most one parent,
- has no circular dependency,
- receives dependencies through its constructor, and
- does not construct its own dependencies.

## Versioning

The rule specification version and versions of tools such as CLIs, linters, and IDE extensions are managed independently.

Every tool must explicitly declare which rule specification versions it supports.

Example:

```text
Hardcore OOP Rules: v1.2.0
hardcore-oop-cli: v0.8.4
Supported Rules: >=1.2.0 <2.0.0
```
