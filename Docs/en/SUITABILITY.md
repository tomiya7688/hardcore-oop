# Applicability and Trade-offs

Hardcore OOP is not intended as a universal design method for every kind of software.

It deliberately restricts responsibilities, dependencies, construction paths, and visibility in order to make program structure easier to read unambiguously. This creates strong benefits in systems that profit from explicit structure, while becoming a burden in systems that depend heavily on dynamic extension or broad sharing.

## Suitable scale

| Scale | Suitability | Why |
| --- | --- | --- |
| Small | High | The dependency tree remains easy to understand, and structural clarity usually outweighs the extra ceremony. |
| Medium | High | Effective when responsibility boundaries are clear. Class count and Composition Root size need active control. |
| Large | Conditional | Whole-system adoption is often too restrictive. Applying it to clearly bounded parts is usually more practical. |
| Very large | Low | Shared infrastructure, multiple entry points, dynamic extension, and organizational boundaries often conflict with the tree constraint. |

Scale should not be judged by lines of code alone.

The number of executable responsibilities, dependencies, entry points, shared facilities, and external boundaries matters more.

## Good fits

Hardcore OOP tends to work well for business applications with clear request-to-result flows, batch processing, small long-running services, libraries with a single public facade, and small-to-medium codebases expected to be maintained for a long time.

It is especially useful when maintainability, traceability, and constrained change impact matter more than minimizing code volume.

## Poor fits

It is usually a poor fit for disposable prototypes, systems built around runtime plugin discovery, very large systems with heavily shared infrastructure, systems that inherently require multiple independent entry points, event-distribution architectures, or frameworks that require mutable models, dynamic proxies, concrete inheritance, or broad static behavior.

For those cases, applying Hardcore OOP only inside a well-defined boundary can be more practical than enforcing it across the entire system.

## Advantages

### Traceable dependencies

Constructor injection and single-parent relationships make it easier to identify where an object comes from and who uses it.

### Smaller change impact

One responsibility per object helps localize reasons for change and reduces accidental coupling between unrelated behavior.

### Fewer hidden dependencies

Restrictions on static behavior, service location, and global mutable state make hidden inputs and control paths harder to introduce.

### Predictable reading model

With one public operation per object and consistent dependency direction, unfamiliar code has a more predictable shape.

### Small test units

Small responsibilities and explicit dependencies make individual objects easier to test in isolation.

### Design ambiguity becomes visible earlier

Questions such as “what is this class responsible for?” or “why does this dependency exist?” are forced into the open during implementation.

## Disadvantages

### More classes and files

Fine-grained responsibilities naturally increase the number of types and files.

### More ceremony

Explicit construction, dependency passing, adapters, and concrete types require more code than less constrained designs.

### Shared behavior becomes harder

The single-caller rule can make ordinary shared services awkward and may encourage unnecessary forwarding objects.

### More duplication in some cases

Because concrete types are preferred over premature generic abstraction, similar code may exist in multiple places until a genuine shared change point appears.

### A larger Composition Root

Centralized object construction can become large as the application grows and must be kept free of business behavior.

### Not every domain is a tree

Real systems often contain shared resources, many-to-many relationships, and fan-out event flows. Forcing these into a tree can make the design less clear rather than more clear.

### Expensive retrofitting

Applying Hardcore OOP to an existing large codebase can require extensive restructuring. Greenfield development or clearly isolated components are better candidates.

## Adoption guidance

Full adoption is most appropriate when there is one entry point, mostly one-way control flow, small separable responsibilities, little need for dynamic extension, no need for shared mutable state, a long maintenance horizon, and a preference for structural clarity over minimal code.

Whole-system adoption should be avoided when multiple entry points are fundamental, many objects must share the same behavior, dynamic type resolution is central, events fan out to many consumers, framework requirements conflict with the rules, the code is a short-lived prototype, or minimizing ceremony is the primary goal.

Hardcore OOP should not be treated as successful merely because every rule is obeyed. Its value comes from making responsibilities and dependencies clearer. If complying with the rules requires large amounts of forwarding, duplication, or adaptation, the chosen scope is probably too broad.
