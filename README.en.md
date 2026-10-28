# Hardcore OOP

> Object-oriented programming on hardcore mode.

Hardcore OOP is a rule specification that intentionally applies severe constraints to object-oriented programming.

Its goal is to make responsibilities, dependencies, visibility, placement, and object construction paths explicit so that the structure of a codebase can be understood as unambiguously as possible.

## Language

The **Japanese version** is the authoritative specification of this repository.

The English version is provided as a compatible translation. If there is any discrepancy in interpretation between the Japanese and English versions, the Japanese version takes precedence.

- [README (Japanese)](README.md)
- [Rules Specification (Japanese)](RULES.md)
- [Rules Specification (English)](RULES.en.md)

## Versioning

Hardcore OOP manages the **rule specification version** and the **versions of tools** independently.

A tool version does not have to match the version number of the rule specification it supports.

Every tool must explicitly declare which version of the Hardcore OOP rule specification it supports.

Current rule specification: **v0.2.1**

## Core philosophy

Hardcore OOP enforces the following direction:

- One responsibility per object
- One public operation per object
- One operation per function
- No duplicate function names within the same scope
- No concrete-class inheritance
- Explicit dependencies
- No global mutable state
- A dependency tree rooted at the Entry Point
- No circular dependencies
- Separation of construction from execution
- Immutable models
- A single construction path
- No null values
- Restricted static behavior
- No dynamic type resolution
- No optional dependencies
- No boolean arguments
- No exposed mutable collections
- No bidirectional references
- Side-effect-free getters
- At most one function argument
- Prefer concrete types over generics

Hardcore OOP does not claim to be a universal best practice for every software system. It is a deliberately extreme specification intended to reduce design ambiguity by imposing strong constraints on object-oriented design.

See [RULES.en.md](RULES.en.md) for the complete rules.

See [Docs/en/SUITABILITY.md](Docs/en/SUITABILITY.md) for applicability, strengths, and trade-offs.
