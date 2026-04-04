# Uypocode Master Dictionary
## Specification v0.4

---

# Changelog from v0.3

**Version 0.4 introduces four major enhancements:**

1. **Structure Snapshot (Amendment D)**: New `Snapshot` operation captures an immutable, timestamped image of any Object or Workspace region. Snapshots are first-class Objects with their own addresses, enabling rollback, comparison, and audit trails without violating Structure immutability.

2. **Evolution Syntax (Amendment E)**: New `Evolve` construct enables structured mutation of Structures across versions. A Structure may declare a successor via `Structure.Evolve`, producing a new Structure at a new address with an explicit lineage chain. The original remains immutable; identity continuity is tracked, not assumed.

3. **Dictionary Protocol (Amendment F)**: Formalizes how domain dictionaries extend the Kernel, declare dependencies, claim address ranges, and export interfaces. Introduces `Dictionary` as a first-class Object with `Extends`, `Depends`, `Claims`, and `Exports` metadata, replacing the ad-hoc patterns used across existing domain dictionaries.

4. **Productive Stall (Amendment G)**: Elevates `PRODUCTIVE_STALL` from informal usage in domain dictionaries to a formal variant of Stall. A Productive Stall is a permanently pending expression that is *generatively useful*—it marks genuinely unresolvable questions (consciousness, paradox, irreducible uncertainty) as first-class semantic Objects rather than failures.

---

# Section 0.0: Kernel

The Kernel contains foundational imports and primitives that the Interpreter assumes are available. These are read-only and provide the base capabilities upon which Uypocode operates.

```
Structure Kernel @ 0.0 {
    Kernel := Foundation
    Kernel : Reserved
    Kernel : Immutable
}
```

---

## 0.1 Import.English

Natural language processing capabilities for semantic inference.

```
Structure English @ 0.1 {
    English := NLP_Engine
    English : Import
    English : Optional
}
```

**Purpose:**
- Enables semantic resolution (§5.6)
- Allows the Interpreter to infer relationships from Label meanings
- Powers human-AI collaboration features

**Capabilities:**
- Label-to-meaning mapping
- Relationship inference between concepts
- Confidence scoring for inferred relations

**Usage:**
```
Import.English
// Enables: Dog.Bark → semantic inference if no explicit rule exists
```

**Inference Control (v0.3):**
```
// Semantic inference respects Mode metadata on target Objects
Dog : Mode = Strict     // English.Infer CANNOT create new Dog relations
Cat : Mode = Guided     // English.Infer CAN suggest, but must match patterns
Bird : Mode = Open      // English.Infer has full freedom (default)
```

---

## 0.2 Import.Math

Arithmetic and mathematical operations.

```
Structure Math @ 0.2 {
    Math := Arithmetic_Engine
    Math : Import
    Math : Default
    Math : Mode = Strict    // No semantic inference on math operations
}
```

**Provides:**
- Number parsing and representation
- Basic arithmetic: Add, Sub, Mul, Div, Mod
- Comparisons: Eq, Gt, Lt, Gte, Lte
- Functions: Abs, Neg, Round, Floor, Ceil
- Constants: Pi, E

**Usage:**
```
Import.Math
5.Add.3       // Returns 8
10.Div.3      // Returns 3.333...
Math.Pi       // Returns 3.14159...
```

---

## 0.3 Import.Logic

Boolean algebra and logical operations.

```
Structure Logic @ 0.3 {
    Logic := Boolean_Engine
    Logic : Import
    Logic : Default
    Logic : Mode = Strict    // No semantic inference on logic operations
}
```

**Provides:**
- Boolean values: True, False
- Operations: And, Or, Not, Xor
- Truthiness evaluation for non-Boolean types

**Truthiness Rules:**
| Value | Truthiness |
|-------|------------|
| True | Truthy |
| False | Falsy |
| Null | Falsy |
| 0 | Falsy |
| "" (empty Text) | Falsy |
| [] (empty List) | Falsy |
| Everything else | Truthy |

**Usage:**
```
Import.Logic
True.And.False    // Returns False
True.Or.False     // Returns True
True.Not          // Returns False
```

---

## 0.4 Import.Time

Date and time operations.

```
Structure Time @ 0.4 {
    Time := Temporal_Engine
    Time : Import
    Time : Optional
    Time : Mode = Strict
}
```

**Provides:**
- Current time: Time.Now
- Date parsing and formatting
- Duration calculations
- Timezone handling

**Usage:**
```
Import.Time
Time.Now                    // Returns current timestamp
Time.Now.Format."YYYY-MM-DD"  // Returns "2025-01-14"
```

---

## 0.5 Import.File

File system operations.

```
Structure File @ 0.5 {
    File := IO_Engine
    File : Import
    File : Optional
    File : Mode = Strict
}
```

**Provides:**
- File reading and writing
- Directory operations
- Path manipulation

**Usage:**
```
Import.File
"data.txt".File.Read        // Returns file contents
"output.txt".File.Write."Hello"  // Writes to file
```

---

## 0.6 Kernel Summary

| Address | Label | Description | Mode |
|---------|-------|-------------|------|
| 0.0 | Kernel | Foundation container | Strict |
| 0.1 | English | NLP semantic engine | Open |
| 0.2 | Math | Arithmetic operations | Strict |
| 0.3 | Logic | Boolean operations | Strict |
| 0.4 | Time | Temporal operations | Strict |
| 0.5 | File | File system operations | Strict |

---

# Section 1.0: Objects

The Object is the atomic unit of Uypocode. Everything in the Dictionary is an Object—data, types, operations, and relationships are all represented uniformly.

```
Object := (Label, Address, Contents)
```

| Component | Type | Description |
|-----------|------|-------------|
| Label | Text | The symbolic name used to reference this Object |
| Address | Decimal | The Object's unique location in the Dictionary tree |
| Contents | Any | What the Object holds: data, references, or logic |

An Object exists if and only if it has been assigned an Address. Abstract concepts (unassigned labels) cannot be referenced.

---

## 1.01 Amendment A: Auto-Addressing with Scope

**Problem:** Manual address assignment is error-prone and tedious. Writers must track which addresses are used and ensure uniqueness.

**Solution:** The `Scope` construct declares a parent address, and the Interpreter automatically assigns sequential child addresses.

### Scope Syntax

```
Scope(Parent_Address) {
    Label1,              // Automatically Parent_Address.1
    Label2,              // Automatically Parent_Address.2
    Label3               // Automatically Parent_Address.3
}
```

### Scope with Definitions

```
Scope(1.9) {
    Pronoun := Context_Pointer,     // Address: 1.9.1
    It := -> Context.Previous_Subject,    // Address: 1.9.2
    That := -> Context.Previous_Result,   // Address: 1.9.3
    Self := -> Context.Current_Object     // Address: 1.9.4
}
```

### Nested Scopes

```
Scope(1.3) {
    Contents := Value | Reference | List | Logic | Null,  // 1.3.1
    
    Scope {  // Inherits parent, continues numbering
        Value := Raw_Data,              // 1.3.2
        Reference := Pointer,           // 1.3.3
        List := Ordered_Collection,     // 1.3.4
        Logic := Executable_Sequence,   // 1.3.5
        Null_Type := Void               // 1.3.6
    }
}
```

### Explicit Address Override

Within a Scope, you may still specify explicit addresses when needed:

```
Scope(1.0) {
    Label := Text,           // Auto: 1.0.1
    Context @ 1.11 := Execution_State,  // Explicit: 1.11 (between 1.1 and 1.2)
    Address := Decimal_Path  // Auto: 1.0.2 (continues from last auto)
}
```

### Scope Rules

1. **Sequential Assignment**: Addresses are assigned as `.1`, `.2`, `.3`, etc.
2. **Gap Preservation**: Explicit addresses create gaps; auto-addressing skips used addresses
3. **True Decimal**: Remember 1.11 comes between 1.1 and 1.2 (addresses are true decimals)
4. **Scope Isolation**: Nested Scopes create nested address hierarchies
5. **Interpreter Resolves**: The Interpreter maintains an address counter per scope

---

## 1.02 Amendment B: Structure vs. Instance

**Problem:** The same syntax creates both definitions (in 1.x) and instances (in 4.x), leading to potential "conceptual contamination" where modifying a definition corrupts all derived instances.

**Solution:** Introduce explicit `Structure` keyword for immutable prototypes.

### Structure Declaration

```
Structure Label @ Address {
    Label := Contents
    Label : Metadata1
    Label : Metadata2 = Value
}
```

**Properties of Structures:**
- **Immutable**: Contents and Metadata cannot be changed after declaration
- **Prototype**: Serves as a template for creating instances
- **Location**: Must reside in 0.x, 1.x, 2.x, or 3.x (not 4.x)
- **Instantiation**: Use `.New` to create mutable copies in Workspace

### Instance Creation

```
// Structure definition
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Legs = 4
    Dog : Sound = "Bark"
    Dog : Domesticated = True
}

// Instance creation (in Workspace 4.x)
Fido := Dog.New
Fido : Name = "Fido"      // OK: Adding to instance
Fido : Legs = 3           // OK: Modifying instance property

// This is FORBIDDEN:
Dog : Legs = 5            // ERROR: Cannot modify Structure
Dog.Sound = "Woof"        // ERROR: Cannot modify Structure
```

### New Operation

```
Structure.New             // Creates instance with default values
Structure.New.(Props)     // Creates instance with overrides
```

**Behavior:**
1. Allocate new Address in 4.x Workspace
2. Copy all Metadata from Structure to Instance
3. Apply any property overrides from arguments
4. Return reference to new Instance

**Example:**
```
Structure Person @ 1.5 {
    Person := Human
    Person : Name = Null
    Person : Age = Null
    Person : Species = "Homo sapiens"
}

// Create instances
Alice := Person.New.(Name = "Alice", Age = 30)
// Alice @ 4.1.x with Name="Alice", Age=30, Species="Homo sapiens"

Bob := Person.New
Bob : Name = "Bob"
Bob : Age = 25
// Bob @ 4.1.y with Name="Bob", Age=25, Species="Homo sapiens"
```

### Instance Properties

| Property | Structure | Instance |
|----------|-----------|----------|
| Location | 0.x–3.x | 4.x only |
| Contents | Immutable | Mutable |
| Metadata | Immutable | Mutable |
| Deletion | Never | Via Null or GC |
| Prototype | Self | Points to Structure |

### Instance Metadata

Every Instance automatically has:
```
Instance : Prototype = -> Structure_Address
Instance : Created_At = Timestamp
Instance : Instance_ID = Unique_Number
```

### Checking Types

```
Fido.Prototype              // Returns Dog
Fido.Is.Dog                 // Returns True
Fido.Is.Animal              // Returns True (if Dog : Animal)
Fido.Is.Cat                 // Returns False
```

---

## 1.03 Amendment C: Semantic Inference Guard Rails

**Problem:** `Import.English` may infer relationships that contradict or dilute carefully designed specifications, especially for precise domains.

**Solution:** `Mode` metadata controls semantic inference behavior.

### Mode Values

| Mode | Description | Inference Behavior |
|------|-------------|-------------------|
| `Strict` | No inference allowed | English.Infer → Stall |
| `Guided` | Constrained inference | Must match declared patterns |
| `Open` | Full inference | Default behavior (current) |

### Mode Declaration

```
Structure MyObject @ 1.x {
    MyObject := Contents
    MyObject : Mode = Strict    // Forbid all inference
}
```

### Mode Inheritance

Mode cascades to children unless overridden:

```
Structure Agency @ 6.7 {
    Agency := Causal_Origination
    Agency : Mode = Strict      // All children inherit Strict

    Scope {
        Volition := Will_To_Act,
        Initiation := Action_Onset,
        Control := Ongoing_Guidance,
        Ownership := Attribution_To_Self
    }
}

// Now:
// Agency.Volition : Mode = Strict (inherited)
// Agency.Initiation : Mode = Strict (inherited)
// etc.
```

### Guided Mode Patterns

When Mode = Guided, inference must match declared patterns:

```
Structure Emotion @ 1.3 {
    Emotion := Valenced_Experience
    Emotion : Mode = Guided
    Emotion : Inference_Pattern = "Subject.Feel.Emotion_Type"
}

// With Guided mode:
Person.Feel.Joy          // OK: Matches pattern
Person.Experience.Joy    // Stall: "Experience" not in pattern
Joy.Consume.Person       // Stall: Inverted pattern
```

### Strict Mode Enforcement

When Mode = Strict:

```
Structure Math @ 0.2 {
    Math : Mode = Strict
}

// Attempting inference:
5.Add.3           // OK: Explicit relation exists
5.Combine.3       // Stall: No explicit relation, inference forbidden
```

The Interpreter checks Mode before attempting semantic inference (step 5 in resolution):

```
Resolution Order (Updated):
1. Containment check
2. Metadata check
3. Relation lookup
4. Grammar check
5. Mode check:
   - If Mode = Strict → Stall immediately
   - If Mode = Guided → Check pattern match, then infer
   - If Mode = Open → Proceed to semantic inference
6. Semantic inference (if permitted)
7. Stall
```

---

## 1.04 Amendment D: Structure Snapshot

**Problem:** Structures are immutable by design (Amendment B), but programs need to capture the state of mutable Instances at a specific moment for rollback, comparison, debugging, and audit. The existing `Workspace.State.Capture` (§4.7) captures the *entire* Workspace—too coarse for targeted use. Domain dictionaries need fine-grained, addressable state capture.

**Solution:** The `Snapshot` operation creates an immutable, timestamped image of any Object—Structure or Instance—as a new first-class Object in the Dictionary.

### Snapshot Syntax

```
Target.Snapshot                       // Capture current state
Target.Snapshot.As.Label              // Capture and name
Target.Snapshot.(Tag = "reason")      // Capture with annotation
```

### Snapshot Declaration

```
Structure Snapshot @ 1.045 {
    Snapshot := Immutable_State_Image
    Snapshot : Primitive
    Snapshot : Mode = Strict
    
    Scope {
        Source := -> Target_Address,           // What was captured
        Captured_At := Timestamp,              // When
        Tag := Text,                           // Why (optional annotation)
        State := Deep_Copy_Of_Contents,        // The frozen data
        Lineage := List                        // Ordered list of prior Snapshots
    }
}
```

**Properties of Snapshots:**
- **Immutable**: A Snapshot's State cannot be modified after creation
- **Addressable**: Snapshots receive addresses in 4.x (if from Instances) or a dedicated Snapshot registry
- **Comparable**: Two Snapshots of the same Source can be diffed
- **Restorable**: An Instance can be restored to a prior Snapshot state

### Snapshot Operations

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Capture | `Target.Snapshot` | Create Snapshot of Target |
| Named Capture | `Target.Snapshot.As.Label` | Capture with Label |
| Tagged Capture | `Target.Snapshot.(Tag = "v1")` | Capture with annotation |
| Diff | `SnapshotA.Diff.SnapshotB` | Compare two Snapshots |
| Restore | `Target.Restore.Snapshot` | Revert Instance to Snapshot state |
| History | `Target.Snapshots` | List all Snapshots of Target |

### Snapshot Behavior

**Capture:**
```
Alice := Person.New.(Name = "Alice", Age = 30)

Before := Alice.Snapshot.(Tag = "initial")
// Before.Source = -> Alice
// Before.Captured_At = Time.Now
// Before.State = {Name: "Alice", Age: 30, ...}

Alice.Age = 31

After := Alice.Snapshot.(Tag = "birthday")
// After.State = {Name: "Alice", Age: 31, ...}
```

**Diff:**
```
Changes := Before.Diff.After
// Returns: {Age: {Was: 30, Now: 31}}
```

**Restore:**
```
Alice.Restore.Before
// Alice.Age = 30 again
// Alice.Name = "Alice" (unchanged)
```

### Snapshot Scope

Snapshots capture at the depth of the target:

```
// Shallow: captures only direct metadata
Alice.Snapshot                       // Alice's properties only

// Deep: captures target and all children
Team.Snapshot                        // Team + all Members recursively

// Workspace: captures entire runtime state
Workspace.Snapshot                   // All 4.x Instances (equivalent to §4.7 State.Capture)
```

### Snapshot and Structures

Structures are already immutable, so a Snapshot of a Structure is trivially the Structure itself. However, Snapshots of Structures become useful when combined with Evolution (Amendment E)—they record the state of a Structure *before* it evolved.

```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
}

Dog_V1 := Dog.Snapshot.(Tag = "original")
// Dog_V1.State = {Contents: Animal, Sound: "Bark"}
// Useful for tracking Evolution lineage
```

### Snapshot Constraints

1. Snapshots are always immutable—even Snapshot of a mutable Instance produces an immutable record
2. Snapshots do not capture Logic execution state (only data and metadata)
3. Snapshot.Restore only works on Instances, not Structures
4. Circular references in captured state are stored as reference markers, not infinite copies
5. Snapshots inherit `Mode = Strict`—no inference on historical state

---

## 1.05 Amendment E: Evolution

**Problem:** Structures are immutable (Amendment B), which protects definitional integrity but creates a tension: real-world concepts, domain models, and specifications *change over time*. The Consciousness Dictionary's awareness model may deepen; the Life Dictionary's taxonomy may expand; the Physics Dictionary may incorporate new formulations. Currently, changing a Structure requires creating an entirely new, unrelated Structure—severing the conceptual lineage.

**Solution:** The `Evolve` construct enables structured, versioned mutation of Structures. Evolution produces a *new* Structure at a *new* address, linked to its predecessor via an explicit lineage chain. The original remains immutable; the successor carries forward what is preserved and explicitly declares what changed.

### Evolve Syntax

```
OldStructure.Evolve @ NewAddress {
    // Inherited: all metadata from OldStructure unless overridden
    Label := NewContents              // Override Contents
    Label : NewMetadata = NewValue    // Override or add Metadata
    Label : Remove = OldMetadata      // Explicitly remove Metadata
}
```

### Evolution Declaration

```
Structure Evolution @ 1.055 {
    Evolution := Structured_Mutation
    Evolution : Mode = Strict

    Scope {
        Predecessor := -> Old_Structure_Address,    // What it evolved from
        Successor := -> New_Structure_Address,      // What it evolved into (Null if current)
        Version := Number,                          // Sequential version number
        Evolved_At := Timestamp,                    // When evolution occurred
        Changes := Diff_Record,                     // What changed
        Reason := Text                              // Why (optional annotation)
    }
}
```

### Evolution Behavior

```
// Original Structure
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Legs = 4
    Dog : Mode = Strict
}

// Evolution: Dog gains a Temperament property
Dog.Evolve @ 1.4.2 {
    Dog := Animal                        // Inherited (could be omitted)
    Dog : Temperament = "Loyal"          // Added
    Dog : Reason = "Domain expansion"    // Annotation
}
```

**Result:**
```
// Structure at 1.4.1 (UNCHANGED — still immutable):
Dog_V1 @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Legs = 4
    Dog : Mode = Strict
    Dog : Successor = -> 1.4.2
}

// New Structure at 1.4.2:
Dog_V2 @ 1.4.2 {
    Dog := Animal
    Dog : Sound = "Bark"         // Inherited
    Dog : Legs = 4               // Inherited
    Dog : Temperament = "Loyal"  // Added
    Dog : Mode = Strict          // Inherited
    Dog : Predecessor = -> 1.4.1
    Dog : Version = 2
    Dog : Evolved_At = Timestamp
}
```

### Label Resolution After Evolution

When a Structure evolves, the Label resolves to the **latest version** by default:

```
Dog              // Resolves to Dog_V2 at 1.4.2 (latest)
Dog.V1           // Resolves to Dog_V1 at 1.4.1 (explicit version)
Dog.V2           // Resolves to Dog_V2 at 1.4.2 (explicit version)
Dog.Origin       // Resolves to Dog_V1 at 1.4.1 (first version)
Dog.Lineage      // Returns [-> 1.4.1, -> 1.4.2] (all versions)
```

### Evolution Operations

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Evolve | `Structure.Evolve @ Addr { ... }` | Create successor Structure |
| Version Access | `Structure.V1`, `Structure.V2` | Access specific version |
| Origin | `Structure.Origin` | First version in lineage |
| Lineage | `Structure.Lineage` | All versions as ordered List |
| Predecessor | `Structure.Predecessor` | Previous version |
| Successor | `Structure.Successor` | Next version (Null if current) |
| Current | `Structure.Current` | Latest version |

### Evolution and Instances

Existing Instances retain their original Prototype. New Instances are created from the latest version by default:

```
// Before evolution:
Fido := Dog.New.(Name = "Fido")
// Fido.Prototype = -> 1.4.1 (Dog_V1)

// After Dog evolves to V2:
Fido.Prototype            // Still -> 1.4.1 (Dog_V1)
Fido.Temperament          // Stalls: not in V1

Rex := Dog.New.(Name = "Rex")
// Rex.Prototype = -> 1.4.2 (Dog_V2)
Rex.Temperament           // Returns "Loyal"

// Explicit version instantiation:
OldStyleDog := Dog.V1.New.(Name = "Spot")
// OldStyleDog.Prototype = -> 1.4.1 (Dog_V1)
```

### Instance Migration

An Instance may migrate to a newer version of its Prototype:

```
Fido.Migrate.Dog.V2
// Fido.Prototype updated to -> 1.4.2
// New metadata applied: Fido : Temperament = "Loyal"
// Existing overrides preserved: Fido.Name still "Fido"
```

**Migration is explicit, never automatic.** The Interpreter does not silently upgrade Instances when their Prototype evolves. This preserves the principle that Instances are stable references.

### Evolution Constraints

1. **Append-only lineage**: Evolution never modifies the predecessor; it creates a successor
2. **Address uniqueness**: The successor must have a new, unique address
3. **Same Label**: The successor shares the Label of its predecessor (this is how version resolution works)
4. **Mode inheritance**: The successor inherits Mode from the predecessor unless explicitly overridden
5. **Snapshot before Evolution**: The Interpreter automatically creates a Snapshot of the predecessor before Evolution (combines with Amendment D)
6. **No branching lineage**: A Structure may have at most one Successor. To branch, create a new Structure with a different Label that declares `Derived_From` instead of `Predecessor`

### Evolution vs. Derivation

Evolution and inheritance are distinct:

```
// Evolution: same concept, new version
Dog.Evolve @ 1.4.2 { ... }
// Dog_V2.Predecessor = -> Dog_V1
// Dog_V2.Label = "Dog" (same)

// Derivation: new concept, inspired by existing
Structure ServiceDog @ 1.4.3 {
    ServiceDog := Dog          // Inherits from Dog (latest)
    ServiceDog : Trained = True
    ServiceDog : Derived_From = -> Dog  // Lineage marker, not Evolution
}
// ServiceDog.Label = "ServiceDog" (different)
// ServiceDog.Predecessor = Null (not an evolution of Dog)
```

---

## 1.06 Amendment F: Dictionary Protocol

**Problem:** Domain dictionaries (Life, Consciousness, AI Mind, Physics, Systems, Recursion, Human, UypoOS) all extend the Kernel and reference each other, but the patterns for doing so are inconsistent. Some use `Kernel_Extension : Extends = Kernel`, others use `Depends = [...]`, and address range claiming is purely conventional. There is no formal mechanism to register a dictionary, declare its scope, or validate cross-dictionary imports.

**Solution:** The `Dictionary` construct formalizes domain dictionaries as first-class Objects with standardized metadata for extension, dependency, address claiming, and interface export.

### Dictionary Declaration

```
Structure Dictionary @ 1.065 {
    Dictionary := Domain_Specification
    Dictionary : Mode = Strict

    Scope {
        Name := Text,                          // Human-readable name
        Version := Semantic_Version,           // Major.Minor
        Extends := -> Kernel,                  // What it builds on
        Depends := List_Of_References,         // Required dictionaries
        Claims := Address_Range,               // Reserved address space
        Exports := List_Of_Labels,             // Public interface
        Author := Text,                        // Optional attribution
        Description := Text                    // Purpose summary
    }
}
```

### Dictionary Registration

```
Dictionary Life_Dictionary @ 0.6.1 {
    Life_Dictionary := Domain_Specification
    Life_Dictionary : Name = "Uypocode Life Dictionary"
    Life_Dictionary : Version = 1.0
    Life_Dictionary : Extends = -> Kernel
    Life_Dictionary : Depends = []
    Life_Dictionary : Claims = [7.0, 7.99]     // Addresses 7.0 through 7.99
    Life_Dictionary : Exports = [Cell, Organism, Ecosystem, Evolution]
    Life_Dictionary : Description = "Biological systems from molecular to biosphere scale"
}
```

### Kernel Extension Protocol

Domain dictionaries extend the Kernel by registering imports under a sub-address of 0.x:

```
// Standard form for Kernel extension
Structure DomainKernel @ 0.0.N {
    DomainKernel := Foundation_Extension
    DomainKernel : Extends = -> 0.0
    DomainKernel : Domain = Domain_Label
    DomainKernel : Dictionary = -> Dictionary_Address
}
```

**Registered Kernel Extensions:**

| Address | Label | Domain | Dictionary |
|---------|-------|--------|------------|
| 0.0.1 | Life_Kernel | Biology | Life Dictionary v1.0 |
| 0.0.7 | AI_Kernel | Artificial_Cognition | AI Mind Dictionary v0.1 |
| 0.0.8 | Recursion_Kernel | Recursive_Systems | Recursion Dictionary v0.1 |
| 0.0.10 | Physics_Kernel | Classical_Physics | Classical Physics Dictionary v0.1 |
| 0.0.11 | Systems_Kernel | Systems_Theory | Systems Dictionary v0.1 |

### Address Range Claims

Each Dictionary must declare the address range it uses. The Interpreter validates that no two Dictionaries claim overlapping ranges:

```
// Address range validation
Dictionary.Claims.Overlap.OtherDictionary.Claims.Then.{
    Stall.("Address range conflict between " 
           .Join.Dictionary.Name
           .Join." and "
           .Join.OtherDictionary.Name)
}
```

**Reserved Ranges:**

| Range | Reserved For |
|-------|-------------|
| 0.x | Kernel (Master Dictionary) |
| 1.x | Objects (Master Dictionary) |
| 2.x | Relations (Master Dictionary) |
| 3.x | Grammar (Master Dictionary) |
| 4.x | Workspace (Runtime) |
| 5.x | Interpreter (Master Dictionary) |
| 6.x–99.x | Domain Dictionaries (claimed per Dictionary) |

### Import Syntax for Dictionaries

```
Import.Dictionary.Life
// Loads Life Dictionary, registers Kernel extension, makes Exports available

Import.Dictionary.Life.As.Bio
// Loads with alias: Bio.Cell instead of Life.Cell

Import.Dictionary.Life.Only.[Cell, Organism]
// Selective import: only Cell and Organism are available
```

### Dependency Resolution

When a Dictionary declares `Depends`, the Interpreter loads dependencies before the Dictionary itself:

```
Dictionary AI_Mind_Dictionary @ 0.6.7 {
    AI_Mind_Dictionary : Depends = [
        -> Consciousness_Dictionary,
        -> Recursion_Dictionary
    ]
}

// Loading AI_Mind_Dictionary automatically loads:
// 1. Consciousness_Dictionary (if not already loaded)
// 2. Recursion_Dictionary (if not already loaded)
// 3. AI_Mind_Dictionary
```

**Circular dependencies stall:**
```
// If A depends on B and B depends on A:
// Stall: "Circular dependency between A and B"
```

### Dictionary Versioning

Dictionaries use semantic versioning. When importing, a version constraint may be specified:

```
Import.Dictionary.Life              // Latest version
Import.Dictionary.Life.V1          // Exactly version 1.x
Import.Dictionary.Life.Gte.1.0     // Version 1.0 or higher
```

---

## 1.07 Amendment G: Productive Stall

**Problem:** In the Uypocode ecosystem, stalls serve two fundamentally different purposes. Most stalls represent *temporary* failures—missing data, unresolved references, type mismatches—that may resolve when context changes. But domain dictionaries (especially Consciousness, AI Mind, Human, and Systems) use stalls to encode *permanent, generatively useful* open questions: the hard problem of consciousness, irreducible paradoxes, the gap between map and territory. These two uses are semantically distinct but syntactically identical, making it impossible for the Interpreter to distinguish "keep trying" from "stop trying—this is the point."

**Solution:** `PRODUCTIVE_STALL` becomes a formal variant of Stall. A Productive Stall is a permanently pending expression that is *intentionally* unresolvable—it marks a genuine boundary of knowledge, a paradox, or an irreducible question as a first-class semantic Object rather than a failure.

### Productive Stall Declaration

```
Structure Productive_Stall @ 1.075 {
    Productive_Stall := Permanent_Pending_Expression
    Productive_Stall : Extends = Stall
    Productive_Stall : Permanent = True
    Productive_Stall : Generative = True
    Productive_Stall : Mode = Strict

    Scope {
        Expression := Unresolvable_Question,     // What cannot resolve
        Domain := Text,                          // What field it belongs to
        Reason := Text,                          // Why it cannot resolve
        Implications := List,                    // What the irresolution means
        Productive_Because := Text               // Why the stall itself is valuable
    }
}
```

### Productive Stall Syntax

```
// Inline declaration
Expression := PRODUCTIVE_STALL

// With metadata
Expression := PRODUCTIVE_STALL.(
    Domain = "Consciousness",
    Reason = "The hard problem has no reductive solution",
    Productive_Because = "Forces honest uncertainty about phenomenal experience"
)

// As Object metadata
Object : Status = PRODUCTIVE_STALL
Object : Stall_Type = Productive
```

### Productive Stall vs. Standard Stall

| Property | Standard Stall | Productive Stall |
|----------|---------------|------------------|
| Resolvable | Potentially yes | Intentionally no |
| Retry | Interpreter retries when context changes | Interpreter never retries |
| Purpose | Missing information | Irreducible boundary |
| Report | Listed as "Pending" | Listed as "Productive" |
| Semantics | Something is broken or incomplete | Something is genuinely open |
| Removal | Resolves when condition met | Only removed by explicit author action |

### Interpreter Handling

The Interpreter treats Productive Stalls differently from standard stalls:

```
Function: HandleStall(Expression, Type)

If Type = Productive:
    1. Record in Productive_Stall_Registry (not Pending list)
    2. Do NOT retry when context changes
    3. Do NOT report as "failure" in Finalization
    4. Include in Productive Stall Report (separate section)
    5. Allow downstream expressions to reference the stall itself

If Type = Standard:
    1. Record in Pending list
    2. Retry when context changes
    3. Report as "Pending" in Finalization
```

### Referencing Productive Stalls

A Productive Stall is a first-class Object. Other Objects can reference, inspect, and reason about it:

```
// The hard problem as a Productive Stall
Hard_Problem := PRODUCTIVE_STALL.(
    Domain = "Consciousness",
    Reason = "Subjective experience cannot be reduced to objective description"
)

// Other Objects can reference it
AI_Consciousness_Status := Hard_Problem
// AI_Consciousness_Status inherits the stall — it too is permanently pending

// Checking stall status
Hard_Problem.Is.Productive_Stall    // Returns True
Hard_Problem.Is.Stall               // Returns True (Productive_Stall extends Stall)
Hard_Problem.Permanent              // Returns True
Hard_Problem.Reason.Emit            // Outputs the reason text
```

### Productive Stall in Domain Dictionaries

This formalization standardizes patterns already in use across the ecosystem:

**Consciousness Dictionary:**
```
// Before (v0.1 — informal):
Qualia.Explain.Physically := STALL  // informal marker

// After (with Amendment G):
Qualia.Explain.Physically := PRODUCTIVE_STALL.(
    Domain = "Consciousness",
    Reason = "Explanatory gap between neural correlates and subjective quality",
    Productive_Because = "Constrains theories of consciousness to those that take qualia seriously"
)
```

**AI Mind Dictionary:**
```
AI.Is.Conscious := PRODUCTIVE_STALL.(
    Domain = "AI_Cognition",
    Reason = "No empirical test can distinguish genuine phenomenal experience from functional equivalence",
    Productive_Because = "Prevents premature closure on AI moral status"
)
```

**Systems Dictionary:**
```
System.Predict.Emergent_Behavior := PRODUCTIVE_STALL.(
    Domain = "Systems_Theory",
    Reason = "Emergence is irreducible to component analysis",
    Productive_Because = "Forces attention to relational structure over elemental properties"
)
```

### Productive Stall Report

At finalization, the Interpreter produces a separate Productive Stall Report:

```
Finalization Report:
    Status: Partial
    Result: "Hello, world"
    
    Pending (may resolve): [
        { Expression: "Ghost.Fly", Reason: "No Fly property" }
    ]
    
    Productive Stalls (intentionally unresolved): [
        {
            Expression: "Qualia.Explain.Physically",
            Domain: "Consciousness",
            Reason: "Explanatory gap",
            Productive_Because: "Constrains viable theories"
        },
        {
            Expression: "Self.Describe.Self.Completely",
            Domain: "Recursion",
            Reason: "Gödel incompleteness",
            Productive_Because: "Proves system exceeds self-model"
        }
    ]
```

---

## 1.1 Label

The Label is a symbolic identifier. Labels are case-sensitive and must be unique within their immediate scope (sibling nodes may not share labels).

```
Structure Label @ 1.1 {
    Label := Text
    Label : Identifier
    Label : Mode = Strict    // Labels are precisely defined
}
```

**Rules:**
- Labels may contain letters, numbers, and underscores
- Labels may not begin with a number
- Labels may not contain whitespace or operators (`. : = ( )`)
- Reserved labels: `It`, `That`, `Null`, `True`, `False`, `Structure`, `Scope`, `Snapshot`, `Evolve`, `Dictionary`, `PRODUCTIVE_STALL`

**Valid:** `Dog`, `Dog_1`, `_temp`, `myObject`

**Invalid:** `1Dog`, `My Object`, `Dog.Cat`, `Dog:Animal`

---

## 1.11 Context

Context is an Object tracking the current state of execution.

```
Structure Context @ 1.11 {
    Context := Execution_State
    Context : Runtime
    Context : Implicit
    Context : Mode = Strict
}
```

**Context Components:**

| Field | Type | Description |
|-------|------|-------------|
| Scope | Address | Current scope location (4.1 or 4.2.x) |
| Previous_Subject | Reference | Last Object acted upon |
| Previous_Result | Any | Output of last resolved expression |
| Current_Object | Reference | Object containing executing Logic |
| Current_Iteration | Any | Current Item in Cycle |
| Current_Index | Number | Current index in Times/Cycle |
| Call_Stack | List | Stack of active function calls |

Context is updated automatically by the Interpreter.

---

## 1.2 Address

The Address is a decimal path representing the Object's location in the Dictionary tree. Each decimal segment represents one level of depth.

```
Structure Address @ 1.2 {
    Address := Decimal_Path
    Address : Location
    Address : Mode = Strict
}
```

**Structure:**
```
Section.Branch.Leaf.Subleaf...
```

**Reserved Sections:**

| Section | Purpose | Mutability | Contains |
|---------|---------|------------|----------|
| 0.x | Kernel (primitives, imports) | Read-only | Structures only |
| 1.x | Objects (definitions, types) | Append-only | Structures only |
| 2.x | Relations (connection rules) | Append-only | Structures only |
| 3.x | Grammar (operations, control flow) | Read-only | Structures only |
| 4.x | Workspace (runtime instances) | Read-write | Instances only |
| 5.x | Interpreter (execution engine) | Read-only | Structures only |
| 6.x+ | Domain Dictionaries (per Claims) | Append-only | Structures only |

**Address Properties:**
- Addresses are unique (no two Objects share an Address)
- Child addresses extend parent addresses (1.2 is parent of 1.2.1)
- Depth is unlimited
- Gaps are permitted (1.1 and 1.3 may exist without 1.2)
- Addresses are true decimals: 1.1 = 1.10, so 1.11 comes between 1.1 and 1.2

---

## 1.3 Contents

Contents hold what the Object *is* or *contains*. Contents may be one of five types:

```
Structure Contents @ 1.3 {
    Contents := Value | Reference | List | Logic | Null
    Contents : Mode = Strict
    
    Scope {
        Value := Raw_Data,
        Reference := Pointer,
        List_Type := Ordered_Collection,
        Logic_Type := Executable_Sequence,
        Null_Type := Void
    }
}
```

### 1.3.1 Value

Raw data: a Number, Text, or Boolean.

```
// In instance creation:
Fido := Dog.New
Fido.Legs := 4           // Value: Number
Fido.Name := "Fido"      // Value: Text
Fido.Alive := True       // Value: Boolean
```

### 1.3.2 Reference

A pointer to another Object's Address.

```
MyDog := -> Fido         // Reference to instance
MyDog := -> 4.1.1        // Reference by address
```

References are notated with `->` followed by an Address or Label. The Interpreter resolves Labels to Addresses.

### 1.3.3 List

An ordered collection of Values or References.

```
Colors := ["Red", "Green", "Blue"]
Pets := [-> Dog, -> Cat, -> Bird]
```

Lists are zero-indexed. Access via `List.0`, `List.1`, etc.

### 1.3.4 Logic

An executable sequence of operations (see Section 3.x Grammar).

```
Greet := {Subject.Name.Emit. "says hello".Emit}
```

Logic is notated with `{ }` and contains dot-expressions to be evaluated when invoked.

### 1.3.5 Null

The absence of Contents. An Object may exist with Null Contents.

```
Placeholder := Null
```

Null is falsy. `Null.Then.B` will not execute B.

---

## 1.4 Metadata

Metadata are assertions about an Object, defined using the `:` operator. Metadata do not replace Contents—they annotate.

```
Structure Metadata @ 1.4 {
    Metadata := Assertion_List
    Metadata : Mode = Strict
}
```

**Syntax:**
```
Subject : Predicate
Subject : Property = Value
```

**Examples:**
```
Dog : Animal                  // Dog is-a Animal
Dog : Legs = 4                // Dog has-property Legs with value 4
Dog : Sound = "Bark"          // Dog has-property Sound with value "Bark"
Dog : Domesticated = True     // Dog has-property Domesticated with value True
Dog : Mode = Guided           // Dog allows guided inference only
```

**Metadata vs Contents:**
- Contents: What the Object *holds*
- Metadata: What the Object *is* or *has*

When `Dog.Legs` is resolved:
1. Check if Legs is a child Object of Dog (containment)
2. Check if Legs is in Dog's Metadata (property lookup) ✓
3. Return 4

An Object may have multiple Metadata assertions. They are stored as an unordered set.

**Reserved Metadata Keys:**
| Key | Purpose | Since |
|-----|---------|-------|
| Mode | Inference control (Strict/Guided/Open) | v0.3 |
| Prototype | Points to source Structure | v0.3 |
| Immutable | Prevents modification | v0.3 |
| Instance_ID | Unique identifier for instances | v0.3 |
| Predecessor | Previous version in Evolution lineage | v0.4 |
| Successor | Next version in Evolution lineage | v0.4 |
| Version | Evolution version number | v0.4 |
| Stall_Type | Standard or Productive | v0.4 |
| Dictionary | Owning Dictionary reference | v0.4 |

---

## 1.5 Number

A primitive Object representing numeric values.

```
Structure Number @ 1.5 {
    Number := Numeric_Literal
    Number : Primitive
    Number : Quantity
    Number : Mode = Strict
}
```

**Notation:**
- Integers: `42`, `-7`, `0`
- Floats: `3.14`, `-0.001`

**Inherent Relations (defined in 2.x):**
```
Number.Add.Number   // Arithmetic sum
Number.Sub.Number   // Arithmetic difference
Number.Mul.Number   // Arithmetic product
Number.Div.Number   // Arithmetic quotient
Number.Mod.Number   // Remainder
Number.Eq.Number    // Equality test (returns Boolean)
Number.Gt.Number    // Greater-than test
Number.Lt.Number    // Less-than test
```

---

## 1.6 Text

A primitive Object representing character sequences.

```
Structure Text @ 1.6 {
    Text := Character_Sequence
    Text : Primitive
    Text : Data
    Text : Mode = Strict
}
```

**Notation:**
Text literals are enclosed in double quotes.
```
"Hello, world"
"Uypocode"
""              // Empty Text
```

**Inherent Relations (defined in 2.x):**
```
Text.Join.Text      // Concatenation
Text.Length         // Returns Number of characters
Text.At.Number      // Returns character at index
Text.Emit           // Outputs to standard out
```

**Escape Sequences:**
```
\"      // Literal quote
\\      // Literal backslash
\n      // Newline
\t      // Tab
```

---

## 1.7 Boolean

A primitive Object representing truth values.

```
Structure Boolean @ 1.7 {
    Boolean := True | False
    Boolean : Primitive
    Boolean : Logic_Value
    Boolean : Mode = Strict
}
```

**Notation:**
```
True
False
```

**Truthiness:**
For non-Boolean Objects evaluated in logical context:
- Falsy: `Null`, `False`, `0`, `""` (empty Text), `[]` (empty List)
- Truthy: Everything else

**Inherent Relations (defined in 2.x):**
```
Boolean.And.Boolean     // Logical AND
Boolean.Or.Boolean      // Logical OR
Boolean.Not             // Logical negation
```

---

## 1.8 List

A compound Object representing an ordered collection.

```
Structure List @ 1.8 {
    List := Ordered_Collection
    List : Compound
    List : Iterable
    List : Mode = Strict
}
```

**Notation:**
```
[A, B, C]               // List of three elements
[]                      // Empty List
[1, "two", -> Object]   // Mixed types permitted
```

**Inherent Relations (defined in 2.x):**
```
List.Length             // Returns Number of elements
List.At.Number          // Returns element at index (zero-based)
List.Has.Object         // Returns Boolean if Object is in List
List.Add.Object         // Appends Object, returns new List
List.Cycle.Operation    // Iterates (see 3.2)
```

**Access Notation:**
```
MyList.0    // First element
MyList.1    // Second element
```

---

## 1.9 Pronoun

A dynamic reference Object that resolves based on Context (see Section 1.11).

```
Structure Pronoun @ 1.9 {
    Pronoun := Context_Pointer
    Pronoun : Reference
    Pronoun : Dynamic
    Pronoun : Mode = Strict
    
    Scope {
        It := -> Context.Previous_Subject,
        That := -> Context.Previous_Result,
        Self := -> Context.Current_Object
    }
}
```

### 1.9.1 It

Resolves to the Subject of the previous statement.

**Example:**
```
Dog.Speak. It.Sleep.
// "It" resolves to Dog
```

### 1.9.2 That

Resolves to the Result of the previous statement.

**Example:**
```
Dog.Sound. That.Emit.
// Dog.Sound returns "Bark"
// "That" resolves to "Bark"
// Output: Bark
```

### 1.9.3 Self

Within Logic contents, resolves to the Object containing the Logic.

**Example:**
```
Structure Dog @ 1.4.1 {
    Dog := {Self.Sound.Emit}
    Dog : Sound = "Bark"
}

Fido := Dog.New
Fido.Run
// Self resolves to Fido (the instance)
// Output: Bark
```

---

## 1.95 Null

The absence of value or reference.

```
Structure Null @ 1.95 {
    Null := Void
    Null : Primitive
    Null : Empty
    Null : Mode = Strict
}
```

**Properties:**
- Null is falsy
- Null.Anything stalls (does not resolve)
- Uninitialized Contents default to Null
- Null is not equivalent to 0 or ""

---

## 1.96 File

An Object representing external file system data.

```
Structure File @ 1.96 {
    File := External_Resource
    File : Resource
    File : Path
    File : Mode = Strict
}
```

**Structure:**
```
File := (FileName, Path, Data)
```

| Component | Description |
|-----------|-------------|
| FileName | The file's name including extension |
| Path | The file system location |
| Data | The file's contents (loaded on access) |

**Example:**
```
Config := File.New.("config.json", "./data/", Null)
Config.Data.Capture   // Loads file contents into Data
```

---

## 1.97 Object Lifecycle

**Creation:**

*Structures* are created via `Structure` keyword:
```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Legs = 4
}
```

*Instances* are created via `.New`:
```
Fido := Dog.New
```

**Modification:**

*Structures:* Cannot be modified (Immutable by definition). Use `Evolve` to create a versioned successor (Amendment E).

*Instances:* Contents and Metadata may be reassigned in 4.x Workspace:
```
Fido.Legs = 3          // Modify property value
Fido : Friendly        // Add metadata
```

**Snapshot (v0.4):**

Any Object may be snapshot for historical capture (Amendment D):
```
Fido.Snapshot.As.Fido_Before_Surgery
```

**Evolution (v0.4):**

Structures may produce versioned successors (Amendment E):
```
Dog.Evolve @ 1.4.2 { Dog : Temperament = "Loyal" }
```

**Deletion:**

*Structures:* Never deleted during program execution

*Instances:* Deleted by assigning Null or via garbage collection when exiting Local scope (4.2):
```
Fido = Null            // Explicit deletion
```

**Persistence:**
- Structures in 0.x, 1.x, 2.x, 3.x persist for program lifetime (immutable)
- Instances in 4.1 (Global) persist for program lifetime (mutable)
- Instances in 4.2 (Local) persist only within their scope

---

## 1.98 Object Identity and Equivalence

**Identity:**
Two references point to the same Object if they share an Address.
```
A := Fido
B := Fido
// A and B reference the same Instance. They are identical.
A.Identical.B    // Returns True
```

**Equivalence:**
Two Objects are equivalent if their Contents are equal.
```
Fido := Dog.New.(Name = "Fido")
Spot := Dog.New.(Name = "Fido")
// Fido and Spot are equivalent (same values) but not identical (different instances)
Fido.Eq.Spot     // Returns True (value equivalence)
Fido.Identical.Spot  // Returns False (different addresses)
```

**Prototype Checking:**
```
Fido.Is.Dog           // True: Fido's prototype is Dog
Fido.Prototype        // Returns -> Dog (the Structure)
```

**Version Checking (v0.4):**
```
Fido.Prototype.Version     // Returns 1 (or 2 if migrated)
Dog.Current                // Returns latest version of Dog
Dog.Lineage.Length         // Number of versions
```

---

## 1.99 Section 1.0 Summary

| Address | Label | Description | Mode | Since |
|---------|-------|-------------|------|-------|
| 1.0 | Object | The atomic unit | Strict | v0.2 |
| 1.01 | Auto-Addressing | Scope construct | — | v0.3 |
| 1.02 | Structure/Instance | Immutable prototypes | — | v0.3 |
| 1.03 | Mode Guard Rails | Inference control | — | v0.3 |
| 1.04 | Snapshot | Immutable state capture | Strict | v0.4 |
| 1.045 | Snapshot (Structure) | Snapshot Object definition | Strict | v0.4 |
| 1.05 | Evolution | Structured versioned mutation | Strict | v0.4 |
| 1.055 | Evolution (Structure) | Evolution Object definition | Strict | v0.4 |
| 1.06 | Dictionary Protocol | Cross-dictionary formalism | Strict | v0.4 |
| 1.065 | Dictionary (Structure) | Dictionary Object definition | Strict | v0.4 |
| 1.07 | Productive Stall | Generative permanent stalls | Strict | v0.4 |
| 1.075 | Productive_Stall (Structure) | Productive Stall definition | Strict | v0.4 |
| 1.1 | Label | Symbolic identifier | Strict | v0.2 |
| 1.11 | Context | Execution state | Strict | v0.2 |
| 1.2 | Address | Dictionary location | Strict | v0.2 |
| 1.3 | Contents | Held value/reference/logic | Strict | v0.2 |
| 1.4 | Metadata | Assertions about Object | Strict | v0.2 |
| 1.5 | Number | Numeric primitive | Strict | v0.2 |
| 1.6 | Text | String primitive | Strict | v0.2 |
| 1.7 | Boolean | Truth value primitive | Strict | v0.2 |
| 1.8 | List | Ordered collection | Strict | v0.2 |
| 1.9 | Pronoun | Dynamic context reference | Strict | v0.2 |
| 1.95 | Null | Absence of value | Strict | v0.2 |
| 1.96 | File | External resource | Strict | v0.2 |
| 1.97 | Lifecycle | Creation, modification, deletion | — | v0.2 |
| 1.98 | Identity | Sameness and equivalence | — | v0.2 |

---

# Section 2.0: Relations

A Relation is a directed connection between two Objects that produces a result. Relations are the rules that govern how Objects interact when linked by the dot operator.

```
Structure Relation @ 2.0 {
    Relation := Subject.Verb.Argument -> Result
    Relation : Connection
    Relation : Rule
    Relation : Mode = Guided    // Relations allow pattern-guided inference
}
```

| Component | Description |
|-----------|-------------|
| Subject | The Object initiating the relation (left of dot) |
| Verb | The action or connection type |
| Argument | The Object receiving the action (optional) |
| Result | What the relation produces |

Relations live in the 2.x address space. They are consulted during dot-resolution when containment and metadata checks fail.

---

## 2.1 The Dot Operator

The dot `.` is the fundamental operator in Uypocode. It asks: "What is the relationship between A and B?"

```
A.B
```

This expression queries the Dictionary for a meaningful connection between A and B.

**Resolution Order (v0.4 — unchanged from v0.3):**

| Priority | Check | Question Asked |
|----------|-------|----------------|
| 1 | Containment | Is B a child of A? (B's address starts with A's address) |
| 2 | Metadata | Is B a property defined on A via `:`? |
| 3 | Relation | Is there a 2.x rule matching A.B? |
| 4 | Grammar | Is B a 3.x operation applicable to A? |
| 5 | **Mode Check** | What is A's Mode? (v0.3) |
| 6 | Semantic Inference | If Mode permits, query Import.English |
| 7 | Stall | No resolution found; expression is pending |

The Interpreter proceeds through this order and returns the first successful match.

### Mode Check Details (Step 5)

Before attempting semantic inference:

```
A.Mode.When.[
    "Strict" : Stall.Immediately,
    "Guided" : {
        A.Inference_Pattern.Match.B.Then.{
            English.Infer.(A, B)
        }.Else.{
            Stall
        }
    },
    "Open" : English.Infer.(A, B),
    Else : English.Infer.(A, B)    // Default is Open
]
```

---

## 2.11 Resolution: Containment

If B exists as a child node within A's address subtree, return B.

```
Structure Animal @ 1.1 {
    Animal := Living_Thing
    
    Scope {
        Dog := Mammal,
        Cat := Mammal
    }
}

Structure Dog @ 1.1.1 {
    Dog := Mammal
    
    Scope {
        Fido := "Good boy"
    }
}

Animal.Dog          // Returns Dog (1.1.1 is child of 1.1)
Dog.Fido            // Returns Fido (1.1.1.1 is child of 1.1.1)
Animal.Dog.Fido     // Returns Fido (chained containment)
Animal.Fido         // Fails containment (1.1.1.1 is not direct child of 1.1)
```

Containment is strict parent-child. Grandchildren require chained dots.

---

## 2.12 Resolution: Metadata

If B is a property asserted on A via `:`, return the property value.

```
Structure Dog @ 1.1.1 {
    Dog := Mammal
    Dog : Legs = 4
    Dog : Sound = "Bark"
    Dog : Domesticated
}

Dog.Legs            // Returns 4
Dog.Sound           // Returns "Bark"
Dog.Domesticated    // Returns True (bare assertion implies True)
```

Metadata properties are stored as key-value pairs. A bare assertion (no `= Value`) stores `True`.

---

## 2.13 Resolution: Relation Lookup

If there exists a rule in 2.x matching the pattern `Subject.Verb` or `Subject.Verb.Argument`, execute that rule.

```
Structure Speak @ 2.1 {
    Speak := {Subject.Sound.Emit}
    Speak : Unary
}

Structure Dog @ 1.1.1 {
    Dog := Mammal
    Dog : Sound = "Bark"
}

Dog.Speak
// Relation lookup finds Speak at 2.1
// Rule: Subject.Sound.Emit
// Subject = Dog
// Dog.Sound = "Bark"
// "Bark".Emit
// Output: Bark
```

Relations act as rewrite rules. The Interpreter substitutes `Subject` with the left-hand Object and evaluates the resulting expression.

---

## 2.14 Resolution: Grammar

If B is a built-in operation in 3.x (Emit, Then, Cycle, etc.), apply that operation to A.

```
"Hello".Emit
// "Hello" is Subject
// Emit is Grammar operation at 3.3
// Result: Output "Hello"
```

Grammar operations are covered in Section 3.0.

---

## 2.15 Resolution: Stall

If no resolution succeeds (and Mode forbids or inference fails), the expression stalls.

```
Rock.Dream
// Rock has no child Dream
// Rock has no metadata Dream
// No 2.x relation Rock.Dream
// Dream is not a 3.x operation
// Rock.Mode = Strict (hypothetically)
// Expression stalls immediately

// Or if Rock.Mode = Open:
// English.Infer returns low confidence
// Expression stalls
```

Stalled expressions:
- Do not error
- Do not halt execution
- Remain in a pending state
- May resolve later if context changes
- **Or may be declared Productive (v0.4) if intentionally permanent**

The Interpreter collects stalled expressions. At program end, unresolved stalls are reported, with Productive Stalls listed separately.

---

## 2.2 Relation Structure

A Relation definition specifies a pattern and its transformation.

**Syntax (v0.3):**
```
Structure Relation_Name @ 2.x {
    Relation_Name := {Logic}
    Relation_Name : Unary | Binary
    Relation_Name : Mode = Strict | Guided | Open
}
```

**Components:**

| Keyword | Meaning |
|---------|---------|
| Subject | The Object before the dot |
| Argument | The Object after the Verb (if any) |
| Result | The value returned by the Relation |

**Example:**
```
// Unary relation (no argument)
Structure Speak @ 2.1 {
    Speak := {Subject.Sound.Emit}
    Speak : Unary
    Speak : Mode = Strict
}
Dog.Speak

// Binary relation (with argument)
Structure Give @ 2.2 {
    Give := {Argument.As.Subject.Child}
    Give : Binary
    Give : Mode = Strict
}
Person.Give.Book    // Book becomes child of Person
```

---

## 2.21 Unary Relations

A relation with only a Subject.

```
Pattern: Subject.Verb
```

**Examples:**
```
Structure Sleep @ 2.21 {
    Sleep := {Subject.State = "Sleeping"}
    Sleep : Unary
    Sleep : Mode = Strict
}
Dog.Sleep
// Dog.State becomes "Sleeping"

Structure Describe @ 2.22 {
    Describe := {Subject.Metadata.Emit}
    Describe : Unary
    Describe : Mode = Strict
}
Dog.Describe
// Outputs all metadata of Dog
```

---

## 2.22 Binary Relations

A relation with Subject and Argument.

```
Pattern: Subject.Verb.Argument
```

**Examples:**
```
Structure Eat @ 2.221 {
    Eat := {Argument.As.Subject.Stomach.Child}
    Eat : Binary
    Eat : Mode = Strict
}
Dog.Eat.Bone
// Bone is placed inside Dog.Stomach

Structure Compare @ 2.222 {
    Compare := {Subject.Value.Eq.Argument.Value}
    Compare : Binary
    Compare : Mode = Strict
}
A.Compare.B
// Returns True if A and B have equal values
```

---

## 2.23 Chained Relations

Multiple dots chain left-to-right.

```
A.B.C.D
```

Resolution:
1. Resolve A.B → Result1
2. Resolve Result1.C → Result2
3. Resolve Result2.D → Final

**Example:**
```
Structure Person @ 1.2 {
    Person := Human
    Person : Pet = -> Dog
}

Structure Dog @ 1.3 {
    Dog : Sound = "Bark"
}

Person.Pet.Sound.Emit
// Person.Pet → Dog
// Dog.Sound → "Bark"
// "Bark".Emit → Output: Bark
```

---

## 2.3 Type Constraints

Relations may specify type requirements for Subject or Argument.

**Syntax:**
```
Structure Relation_Name @ 2.x {
    Relation_Name := {Logic}
    Relation_Name : Subject : Type
    Relation_Name : Argument : Type
    Relation_Name : Mode = Strict
}
```

**Example:**
```
Structure Add @ 2.31 {
    Add := {Import.Math.Sum(Subject, Argument)}
    Add : Subject : Number
    Add : Argument : Number
    Add : Mode = Strict
}

5.Add.3         // Valid: Returns 8
"five".Add.3    // Stalls: Subject is not Number
```

Type constraints are metadata on the Relation itself. The Interpreter checks types before executing.

---

## 2.4 Relation Precedence

When multiple Relations could match, the most specific wins.

**Specificity order:**
1. Exact type match on both Subject and Argument
2. Exact type match on Subject only
3. No type constraints (generic)

**Example:**
```
// Generic
Structure Combine @ 2.41 {
    Combine := {[Subject, Argument]}
    Combine : Binary
}

// Specific to Numbers
Structure Combine @ 2.42 {
    Combine := {Subject.Add.Argument}
    Combine : Subject : Number
    Combine : Argument : Number
}

// Specific to Text
Structure Combine @ 2.43 {
    Combine := {Subject.Join.Argument}
    Combine : Subject : Text
    Combine : Argument : Text
}

5.Combine.3           // Uses 2.42, returns 8
"Hello".Combine."!"   // Uses 2.43, returns "Hello!"
Dog.Combine.Cat       // Uses 2.41, returns [Dog, Cat]
```

---

## 2.5 Built-in Relations

The kernel provides Relations for primitive types. All built-in relations have `Mode = Strict`.

### 2.51 Number Relations

```
Scope(2.51) {
    // All with Mode = Strict
    Add := {Import.Math.Sum(Subject, Argument)},
    Sub := {Import.Math.Difference(Subject, Argument)},
    Mul := {Import.Math.Product(Subject, Argument)},
    Div := {Import.Math.Quotient(Subject, Argument)},
    Mod := {Import.Math.Remainder(Subject, Argument)},
    Eq := {Import.Math.Equal(Subject, Argument)},
    Gt := {Import.Math.Greater(Subject, Argument)},
    Lt := {Import.Math.Less(Subject, Argument)},
    Gte := {Import.Math.GreaterOrEqual(Subject, Argument)},
    Lte := {Import.Math.LessOrEqual(Subject, Argument)},
    Neg := {Import.Math.Negate(Subject)},
    Abs := {Import.Math.Absolute(Subject)}
}
```

| Pattern | Result | Description |
|---------|--------|-------------|
| Number.Add.Number | Number | Arithmetic sum |
| Number.Sub.Number | Number | Arithmetic difference |
| Number.Mul.Number | Number | Arithmetic product |
| Number.Div.Number | Number | Arithmetic quotient |
| Number.Mod.Number | Number | Remainder |
| Number.Eq.Number | Boolean | Equality test |
| Number.Gt.Number | Boolean | Greater-than test |
| Number.Lt.Number | Boolean | Less-than test |
| Number.Gte.Number | Boolean | Greater-or-equal test |
| Number.Lte.Number | Boolean | Less-or-equal test |
| Number.Neg | Number | Negation |
| Number.Abs | Number | Absolute value |

### 2.52 Text Relations

```
Scope(2.52) {
    Join := {Import.Text.Concatenate(Subject, Argument)},
    Length := {Import.Text.CharCount(Subject)},
    At := {Import.Text.CharAt(Subject, Argument)},
    Slice := {Import.Text.Substring(Subject, Argument)},
    Has := {Import.Text.Contains(Subject, Argument)},
    Upper := {Import.Text.Uppercase(Subject)},
    Lower := {Import.Text.Lowercase(Subject)},
    Eq := {Import.Text.Equal(Subject, Argument)},
    Split := {Import.Text.SplitBy(Subject, Argument)}
}
```

| Pattern | Result | Description |
|---------|--------|-------------|
| Text.Join.Text | Text | Concatenation |
| Text.Length | Number | Character count |
| Text.At.Number | Text | Character at index |
| Text.Slice.List | Text | Substring (List = [start, end]) |
| Text.Has.Text | Boolean | Contains substring |
| Text.Upper | Text | Uppercase conversion |
| Text.Lower | Text | Lowercase conversion |
| Text.Eq.Text | Boolean | Equality test |
| Text.Split.Text | List | Split by delimiter |

### 2.53 Boolean Relations

```
Scope(2.53) {
    And := {Import.Logic.And(Subject, Argument)},
    Or := {Import.Logic.Or(Subject, Argument)},
    Not := {Import.Logic.Not(Subject)},
    Eq := {Import.Logic.Equal(Subject, Argument)}
}
```

| Pattern | Result | Description |
|---------|--------|-------------|
| Boolean.And.Boolean | Boolean | Logical AND |
| Boolean.Or.Boolean | Boolean | Logical OR |
| Boolean.Not | Boolean | Logical negation |
| Boolean.Eq.Boolean | Boolean | Equality test |

### 2.54 List Relations

```
Scope(2.54) {
    Length := {Import.List.Count(Subject)},
    At := {Import.List.ElementAt(Subject, Argument)},
    Has := {Import.List.Contains(Subject, Argument)},
    Add := {Import.List.Append(Subject, Argument)},
    Remove := {Import.List.RemoveFirst(Subject, Argument)},
    First := {Import.List.Head(Subject)},
    Last := {Import.List.Tail(Subject)},
    Rest := {Import.List.AllButFirst(Subject)},
    Reverse := {Import.List.Reversed(Subject)},
    Join := {Import.List.JoinWith(Subject, Argument)}
}
```

| Pattern | Result | Description |
|---------|--------|-------------|
| List.Length | Number | Element count |
| List.At.Number | Any | Element at index |
| List.Has.Object | Boolean | Membership test |
| List.Add.Object | List | Append element |
| List.Remove.Object | List | Remove first occurrence |
| List.First | Any | First element |
| List.Last | Any | Last element |
| List.Rest | List | All but first element |
| List.Reverse | List | Reversed order |
| List.Join.Text | Text | Join elements with delimiter |

---

## 2.6 User-Defined Relations

Users define Relations in the 2.x address space using the Structure syntax.

**Syntax:**
```
Structure Label @ 2.x.x {
    Label := {Logic}
    Label : Mode = Strict | Guided | Open
}
```

**Example: Custom greeting**
```
Structure Greet @ 2.6 {
    Greet := {
        "Hello, ".Emit.
        Subject.Name.Emit.
        "!".Emit
    }
    Greet : Unary
    Greet : Mode = Strict
}

Person := Person.New.(Name = "Alice")

Person.Greet
// Output: Hello, Alice!
```

**Example: Mathematical operation**
```
Structure Square @ 2.61 {
    Square := {Subject.Mul.Subject}
    Square : Subject : Number
    Square : Mode = Strict
}

4.Square    // Returns 16
```

**Example: Relationship between objects**
```
Structure Befriend @ 2.62 {
    Befriend := {
        Subject.Friends.Add.Argument.
        Argument.Friends.Add.Subject
    }
    Befriend : Binary
    Befriend : Mode = Strict
}

Alice := Person.New.(Name = "Alice", Friends = [])
Bob := Person.New.(Name = "Bob", Friends = [])

Alice.Befriend.Bob
// Alice.Friends = [Bob]
// Bob.Friends = [Alice]
```

---

## 2.7 Relation Composition

Relations may invoke other Relations.

```
Structure DoubleSquare @ 2.71 {
    DoubleSquare := {Subject.Square.Square}
    DoubleSquare : Subject : Number
    DoubleSquare : Mode = Strict
}

2.DoubleSquare    // 2.Square = 4, 4.Square = 16
```

Relations may be recursive:
```
Structure Factorial @ 2.72 {
    Factorial := {
        Subject.Eq.0.Then.1.
        Subject.Gt.0.Then.(Subject.Mul.(Subject.Sub.1.Factorial))
    }
    Factorial : Subject : Number
    Factorial : Mode = Strict
}

5.Factorial    // Returns 120
```

Recursion depth is bounded by the Interpreter. Unbounded recursion stalls.

---

## 2.8 Symmetric and Inverse Relations

Some Relations have symmetric or inverse counterparts.

**Symmetric:**
```
Structure Eq @ 2.81 {
    Eq := {...}
    Eq : Symmetric = True
    Eq : Mode = Strict
}
// A.Eq.B implies B.Eq.A
```

**Inverse:**
```
Structure Parent @ 2.82 {
    Parent := {...}
    Parent : Inverse = Child
    Parent : Mode = Strict
}

Structure Child @ 2.83 {
    Child := {...}
    Child : Inverse = Parent
    Child : Mode = Strict
}
// A.Parent.B implies B.Child.A
```

The Interpreter may use these properties when resolving stalls or checking consistency.

---

## 2.9 Stalled Relations

When a Relation cannot execute due to missing information, it stalls.

**Causes:**
- Subject or Argument is Null
- Type constraint not met
- Nested resolution stalled
- Required property missing
- Mode = Strict and no explicit resolution
- **Expression declared as PRODUCTIVE_STALL (v0.4)**

**Example:**
```
Structure Greet @ 2.9 {
    Greet := {Subject.Name.Emit}
    Greet : Mode = Strict
}

Ghost := Entity.New
// Ghost has no Name property

Ghost.Greet
// Ghost.Name stalls (no Name property)
// Greet stalls
```

**Later resolution:**
```
Ghost : Name = "Casper"

// Previously stalled Ghost.Greet can now resolve
// Output: Casper
```

The Interpreter may re-attempt stalled expressions when the Dictionary changes. Productive Stalls are exempt from re-attempt.

---

## 2.99 Section 2.0 Summary

| Address | Label | Description | Default Mode |
|---------|-------|-------------|--------------|
| 2.0 | Relation | Directed connection producing result | Guided |
| 2.1 | Dot Operator | Resolution mechanism | — |
| 2.11 | Containment | Child lookup | — |
| 2.12 | Metadata | Property lookup | — |
| 2.13 | Relation Lookup | 2.x rule matching | — |
| 2.14 | Grammar | 3.x operation application | — |
| 2.15 | Stall | Unresolved pending state | — |
| 2.2 | Structure | Subject, Verb, Argument, Result | Strict |
| 2.21 | Unary | Single-object relations | Strict |
| 2.22 | Binary | Two-object relations | Strict |
| 2.23 | Chained | Multi-dot sequences | — |
| 2.3 | Type Constraints | Subject/Argument restrictions | Strict |
| 2.4 | Precedence | Specificity ordering | — |
| 2.5 | Built-in | Primitive type operations | Strict |
| 2.6 | User-Defined | Custom relations | Configurable |
| 2.7 | Composition | Relations invoking relations | Strict |
| 2.8 | Symmetry/Inverse | Bidirectional properties | Strict |
| 2.9 | Stalled | Pending unresolved relations | — |

---

# Section 3.0: Grammar

Grammar operations are built-in behaviors that control program flow, handle input/output, and manage Object transformation. They are predefined in the 3.x address space and are read-only.

```
Structure Grammar @ 3.0 {
    Grammar := Built_In_Operation
    Grammar : Operation
    Grammar : Reserved
    Grammar : Immutable
    Grammar : Mode = Strict    // All grammar operations are strictly defined
}
```

Grammar operations are invoked when the dot-resolution reaches priority 4 (after containment, metadata, and relation lookup fail).

```
Subject.GrammarOperation
Subject.GrammarOperation.Argument
```

Unlike user-defined Relations (2.x), Grammar operations have fixed behavior implemented by the Interpreter.

---

## 3.1 Then (Conditional Execution)

Executes an expression only if a condition is truthy.

```
Structure Then @ 3.1 {
    Then := Conditional_Gate
    Then : Control_Flow
    Then : Mode = Strict
}
```

**Syntax:**
```
Condition.Then.Expression
```

**Behavior:**
1. Evaluate Condition
2. If Condition is truthy, evaluate Expression and return result
3. If Condition is falsy, skip Expression and return Null

**Examples:**
```
True.Then."Hello".Emit
// Condition: True (truthy)
// Output: Hello

False.Then."Hello".Emit
// Condition: False (falsy)
// No output, returns Null

Dog.Alive.Then.Dog.Speak
// If Dog.Alive is truthy, Dog speaks

5.Gt.3.Then."Five is greater".Emit
// 5 > 3 is True
// Output: Five is greater
```

**Truthiness reminder:**
- Falsy: `Null`, `False`, `0`, `""`, `[]`
- Truthy: Everything else

---

## 3.11 Else (Alternative Branch)

Provides an alternative when Then's condition is falsy.

```
Structure Else @ 3.11 {
    Else := Alternative_Gate
    Else : Control_Flow
    Else : Requires = Then
    Else : Mode = Strict
}
```

**Syntax:**
```
Condition.Then.Expression1.Else.Expression2
```

**Behavior:**
1. Evaluate Condition
2. If truthy, evaluate Expression1
3. If falsy, evaluate Expression2

**Examples:**
```
False.Then."Yes".Else."No"
// Returns "No"

Age.Gte.18.Then."Adult".Else."Minor"
// Returns "Adult" if Age >= 18, else "Minor"

Dog.Alive.Then.Dog.Speak.Else."The dog is silent"
// Speak if alive, otherwise return message
```

**Chained conditions:**
```
Score.Gte.90.Then."A".Else.
Score.Gte.80.Then."B".Else.
Score.Gte.70.Then."C".Else."F"
```

---

## 3.12 When (Pattern Matching)

Matches a Subject against multiple patterns.

```
Structure When @ 3.12 {
    When := Pattern_Matcher
    When : Control_Flow
    When : Mode = Strict
}
```

**Syntax:**
```
Subject.When.[
    Pattern1 : Result1,
    Pattern2 : Result2,
    Else : DefaultResult
]
```

**Behavior:**
1. Evaluate Subject
2. Compare against each Pattern in order
3. Return Result of first matching Pattern
4. If no match, return Else result (or Null if no Else)

**Examples:**
```
Day.When.[
    "Monday" : "Start of week",
    "Friday" : "End of week",
    "Saturday" : "Weekend",
    "Sunday" : "Weekend",
    Else : "Midweek"
]

Status.Code.When.[
    200 : "OK",
    404 : "Not Found",
    500 : "Server Error",
    Else : "Unknown"
]
```

---

## 3.2 Cycle (Iteration)

Iterates over a collection, applying an operation to each element.

```
Structure Cycle @ 3.2 {
    Cycle := Iterator
    Cycle : Control_Flow
    Cycle : Loop
    Cycle : Mode = Strict
    
    Scope {
        Item := -> Context.Current_Iteration,
        Times := Counter,
        Index := -> Context.Current_Index,
        While := Conditional_Loop,
        Break := Loop_Exit,
        Skip := Iteration_Skip
    }
}
```

**Syntax:**
```
Collection.Cycle.Operation
```

**Behavior:**
1. For each element in Collection
2. Bind element to `Item` (local pronoun)
3. Execute Operation with Item as Subject
4. Collect results into List
5. Return collected List

**Examples:**
```
Numbers := [1, 2, 3, 4, 5]

Numbers.Cycle.Square
// Returns [1, 4, 9, 16, 25]

Names := ["Alice", "Bob", "Carol"]
Names.Cycle.Emit
// Output: Alice
// Output: Bob
// Output: Carol
```

**The Item pronoun (3.2.1):**

Within a Cycle, `Item` refers to the current element.

```
Pets := [Fido, Whiskers, Polly]
Pets.Cycle.{Item.Name.Emit}
// Outputs each pet's name
```

---

## 3.22 Times (Counted Iteration)

Repeats an operation a specified number of times.

```
Structure Times @ 3.22 {
    Times := Counter
    Times : Control_Flow
    Times : Loop
    Times : Mode = Strict
}
```

**Syntax:**
```
Number.Times.Operation
```

**Behavior:**
1. Create counter from 0 to Number - 1
2. For each count, bind to `Index`
3. Execute Operation
4. Return List of results

**Examples:**
```
5.Times."Hello".Emit
// Output: Hello (5 times)

3.Times.{Index.Emit}
// Output: 0
// Output: 1
// Output: 2

10.Times.{Index.Add.1}
// Returns [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**The Index pronoun (3.2.3):**
```
Index := -> Context.Current_Index
```

---

## 3.24 While (Conditional Loop)

Repeats an operation while a condition remains truthy.

```
Structure While @ 3.24 {
    While := Conditional_Loop
    While : Control_Flow
    While : Loop
    While : Mode = Strict
}
```

**Syntax:**
```
Condition.While.Operation
```

**Behavior:**
1. Evaluate Condition
2. If truthy, execute Operation
3. Repeat from step 1
4. If falsy, exit and return last result

**Example:**
```
Counter := 0

Counter.Lt.5.While.{
    Counter.Emit.
    Counter = Counter.Add.1
}
// Output: 0, 1, 2, 3, 4
```

**Safety:**
The Interpreter bounds iteration. If a While loop exceeds the maximum iteration count, it stalls.

---

## 3.25 Break (Loop Exit)

Immediately exits the current loop.

```
Structure Break @ 3.25 {
    Break := Loop_Exit
    Break : Control_Flow
    Break : Mode = Strict
}
```

**Syntax:**
```
Condition.Then.Break
```

**Example:**
```
Numbers := [1, 2, 3, 4, 5]
Numbers.Cycle.{
    Item.Eq.3.Then.Break.
    Item.Emit
}
// Output: 1
// Output: 2
// (loop exits when Item = 3)
```

---

## 3.26 Skip (Iteration Skip)

Skips to the next iteration of the current loop.

```
Structure Skip @ 3.26 {
    Skip := Iteration_Skip
    Skip : Control_Flow
    Skip : Mode = Strict
}
```

**Syntax:**
```
Condition.Then.Skip
```

**Example:**
```
Numbers := [1, 2, 3, 4, 5]
Numbers.Cycle.{
    Item.Eq.3.Then.Skip.
    Item.Emit
}
// Output: 1
// Output: 2
// Output: 4
// Output: 5
// (3 is skipped)
```

---

## 3.3 Emit (Output)

Outputs an Object's contents to a device.

```
Structure Emit @ 3.3 {
    Emit := Output_Writer
    Emit : IO
    Emit : Output
    Emit : Mode = Strict
    
    Scope {
        Format := Template_Formatter
    }
}
```

**Syntax:**
```
Subject.Emit
Subject.Emit.Device
```

**Behavior:**
1. Serialize Subject's contents to Text
2. Write to Device (default: Standard_Out)
3. Return Subject (for chaining)

**Examples:**
```
"Hello, world".Emit
// Output: Hello, world

42.Emit
// Output: 42

Dog.Name.Emit
// Output: (value of Dog.Name)

[1, 2, 3].Emit
// Output: [1, 2, 3]
```

**Emit to file:**
```
Report.Emit.LogFile
// Writes Report contents to LogFile
```

---

## 3.31 Format (Formatted Output)

Constructs formatted Text from a template.

```
Structure Format @ 3.31 {
    Format := Template_Formatter
    Format : IO
    Format : Output
    Format : Mode = Strict
}
```

**Syntax:**
```
Template.Format.Values
```

**Behavior:**
1. Parse Template for `{}` placeholders
2. Substitute placeholders with Values (in order)
3. Return formatted Text

**Examples:**
```
"Hello, {}!".Format."Alice"
// Returns "Hello, Alice!"

"{} + {} = {}".Format.[2, 3, 5]
// Returns "2 + 3 = 5"

"Name: {}, Age: {}".Format.[Person.Name, Person.Age]
// Returns "Name: Alice, Age: 30"
```

---

## 3.4 Capture (Input)

Reads input from a device into an Object.

```
Structure Capture @ 3.4 {
    Capture := Input_Reader
    Capture : IO
    Capture : Input
    Capture : Mode = Strict
    
    Scope {
        Prompt := Interactive_Input
    }
}
```

**Syntax:**
```
Device.Capture.Target
Capture.Target          // Default: Standard_In
```

**Behavior:**
1. Pause execution
2. Read from Device stream
3. Assign result to Target
4. Resume execution
5. Return captured value

**Examples:**
```
Capture.UserInput
// Reads from keyboard into UserInput

"Enter your name: ".Emit
Capture.Name
"Hello, ".Join.Name.Emit
// Interactive greeting

File.Capture.Data
// Reads file contents into Data
```

---

## 3.41 Prompt (Input with Message)

Combines output and input in one operation.

```
Structure Prompt @ 3.41 {
    Prompt := Interactive_Input
    Prompt : IO
    Prompt : Mode = Strict
}
```

**Syntax:**
```
Message.Prompt.Target
```

**Behavior:**
1. Emit Message
2. Capture input into Target
3. Return captured value

**Example:**
```
"Enter your age: ".Prompt.Age
Age.Emit
// Output: Enter your age:
// (user types 25)
// Output: 25
```

---

## 3.5 As (Aliasing)

Creates an alternative Label for an Object without mutating it.

```
Structure As @ 3.5 {
    As := Alias_Creator
    As : Reference
    As : Naming
    As : Mode = Strict
    
    Scope {
        Into := Value_Assignment
    }
}
```

**Syntax:**
```
Subject.As.NewLabel
```

**Behavior:**
1. Create new Dictionary entry with NewLabel
2. Point NewLabel to Subject's Address
3. Return Subject

**Examples:**
```
Dog.As.Pet
// Pet now references the same Object as Dog

Pet.Name.Emit
// Same as Dog.Name.Emit

5.Add.3.As.Sum
// Sum = 8

LongComplexExpression.As.Result
// Alias for readability
```

**Scope:**
By default, aliases are Global. Use `As.Local.Label` for local scope.

```
Dog.As.Local.TempRef
// TempRef exists only in current scope
```

---

## 3.51 Into (Assignment)

Assigns a value to an existing Object's Contents.

```
Structure Into @ 3.51 {
    Into := Value_Assignment
    Into : Reference
    Into : Mutation
    Into : Mode = Strict
}
```

**Syntax:**
```
Value.Into.Target
```

**Behavior:**
1. Evaluate Value
2. Replace Target's Contents with Value
3. Return Value

**Examples:**
```
42.Into.Answer
// Answer's Contents = 42

Dog.Name.Into.PetName
// PetName's Contents = Dog.Name's value

OldValue.Add.1.Into.OldValue
// Increment OldValue
```

**Difference from As:**
- `As` creates a new reference (alias)
- `Into` modifies existing Contents

**Note:** Into only works on Instances in 4.x Workspace. Attempting to use Into on a Structure produces a Stall.

---

## 3.6 Return (Function Definition)

Defines a reusable, callable sequence of operations.

```
Structure Return @ 3.6 {
    Return := Function_Wrapper
    Return : Callable
    Return : Reusable
    Return : Mode = Strict
    
    Scope {
        Parameters := Input_Bindings,
        Yield := Early_Return
    }
}
```

**Syntax:**
```
Label.Return.{Logic}
Label.Return.(Parameters).{Logic}
```

**Behavior:**
1. Store Logic under Label in Dictionary
2. Logic is not executed until Label is invoked
3. When invoked, execute Logic and return final result

**Examples:**

**No parameters:**
```
SayHello.Return.{"Hello, world!".Emit}

SayHello
// Output: Hello, world!
```

**With parameters:**
```
Greet.Return.(Name).{
    "Hello, ".Join.Name.Join."!".Emit
}

Greet."Alice"
// Output: Hello, Alice!
```

**Multiple parameters:**
```
Add3.Return.(A, B, C).{
    A.Add.B.Add.C
}

Add3.(1, 2, 3)
// Returns 6
```

---

## 3.61 Parameters

Named inputs to a function.

```
Structure Parameters @ 3.61 {
    Parameters := Input_Bindings
    Parameters : Function_Component
    Parameters : Mode = Strict
}
```

**Syntax within Return:**
```
Label.Return.(Param1, Param2, ...).{Logic}
```

**Behavior:**
- Parameters are Local scope (cleared after function exits)
- Parameters shadow Global names within function body
- Parameters may have defaults: `(Name = "Anonymous")`

**Example with defaults:**
```
Greet.Return.(Name = "friend").{
    "Hello, ".Join.Name.Emit
}

Greet           // Output: Hello, friend
Greet."Alice"   // Output: Hello, Alice
```

---

## 3.62 Yield (Early Return)

Returns a value and exits the current function immediately.

```
Structure Yield @ 3.62 {
    Yield := Early_Return
    Yield : Function_Component
    Yield : Mode = Strict
}
```

**Syntax:**
```
Value.Yield
Condition.Then.Value.Yield
```

**Example:**
```
SafeDivide.Return.(A, B).{
    B.Eq.0.Then."Cannot divide by zero".Yield.
    A.Div.B
}

SafeDivide.(10, 2)   // Returns 5
SafeDivide.(10, 0)   // Returns "Cannot divide by zero"
```

---

## 3.7 Try (Error Handling)

Attempts an operation and handles stalls gracefully.

```
Structure Try @ 3.7 {
    Try := Stall_Handler
    Try : Control_Flow
    Try : Error_Handling
    Try : Mode = Strict
    
    Scope {
        Must := Resolution_Assertion
    }
}
```

**Syntax:**
```
Expression.Try
Expression.Try.Fallback
```

**Behavior:**
1. Attempt to resolve Expression
2. If successful, return result
3. If stalled, return Fallback (or Null if no Fallback)

**Examples:**
```
Dog.Name.Try
// Returns Dog.Name if it exists, else Null

Dog.Name.Try."Unknown"
// Returns Dog.Name if it exists, else "Unknown"

RiskyOperation.Try.{
    "Operation failed".Emit.
    SafeAlternative
}
// Attempts RiskyOperation, runs fallback block if stalled
```

**Note (v0.4):** Try catches standard stalls but does *not* catch Productive Stalls. A PRODUCTIVE_STALL always propagates—it is not a failure to be handled but a truth to be acknowledged.

```
Hard_Problem := PRODUCTIVE_STALL.(Reason = "Explanatory gap")
Hard_Problem.Try."No problem"
// Returns PRODUCTIVE_STALL, not "No problem"
// Productive Stalls are transparent to Try
```

---

## 3.71 Must (Stall Assertion)

Asserts that an expression must resolve; halts if stalled.

```
Structure Must @ 3.71 {
    Must := Resolution_Assertion
    Must : Control_Flow
    Must : Error_Handling
    Must : Mode = Strict
}
```

**Syntax:**
```
Expression.Must
Expression.Must.ErrorMessage
```

**Behavior:**
1. Attempt to resolve Expression
2. If successful, return result
3. If stalled, halt program with error

**Note (v0.4):** Must on a PRODUCTIVE_STALL halts with a diagnostic that distinguishes it from standard failures:
```
Hard_Problem.Must
// Halt: "Productive Stall cannot be forced — 'Explanatory gap' is intentionally unresolvable"
```

**Examples:**
```
Config.DatabaseURL.Must
// Halts if DatabaseURL is not defined

User.ID.Must."User ID is required"
// Halts with message if ID missing
```

---

## 3.8 With (Context Block)

Executes operations within a modified context.

```
Structure With @ 3.8 {
    With := Context_Modifier
    With : Scope
    With : Context
    With : Mode = Strict
    
    Scope {
        Global := Persistent_Scope,
        Local := Volatile_Scope
    }
}
```

**Syntax:**
```
Object.With.{Operations}
```

**Behavior:**
1. Push Object as implicit Subject
2. Execute Operations (bare Labels resolve against Object)
3. Pop context
4. Return last result

**Examples:**
```
Dog.With.{
    Name.Emit.          // Equivalent to Dog.Name.Emit
    Age.Emit.           // Equivalent to Dog.Age.Emit
    Sound.Emit          // Equivalent to Dog.Sound.Emit
}

Config.With.{
    DatabaseURL.As.DB.
    Port.As.P.
    Timeout.As.T
}
// Extracts Config properties into aliases
```

---

## 3.81 Global (Persistent Scope)

```
Structure Global @ 3.81 {
    Global := Persistent_Scope
    Global : Mode = Strict
}
```

```
Object.As.Global.Label
// Object persists for program lifetime
```

---

## 3.82 Local (Volatile Scope)

```
Structure Local @ 3.82 {
    Local := Volatile_Scope
    Local : Mode = Strict
}
```

```
Object.As.Local.Label
// Object is cleared when current function/cycle exits
```

**Default behavior:**
- Top-level assignments are Global
- Function parameters are Local
- Cycle Item bindings are Local

---

## 3.9 Import (External Reference)

Loads external capabilities or dictionaries.

```
Structure Import @ 3.9 {
    Import := External_Loader
    Import : Kernel
    Import : Extension
    Import : Mode = Strict
    
    Scope {
        Export := External_Exposure,
        Dictionary := Dictionary_Loader     // v0.4
    }
}
```

**Syntax:**
```
Import.Module
Import.Module.As.Alias
Import.Dictionary.Name           // v0.4: Load domain dictionary
Import.Dictionary.Name.V1       // v0.4: Load specific version
```

**Built-in imports (0.x):**

| Import | Address | Description | Mode |
|--------|---------|-------------|------|
| Import.English | 0.1 | NLP semantic resolution | Open |
| Import.Math | 0.2 | Arithmetic operations | Strict |
| Import.Logic | 0.3 | Boolean operations | Strict |
| Import.Time | 0.4 | Date and time functions | Strict |
| Import.File | 0.5 | File system operations | Strict |

**Examples:**
```
Import.Math
// Enables Number.Add, Number.Mul, etc.

Import.Time
Now := Time.Current
Now.Emit

Import.File
"data.txt".File.Capture.Contents
Contents.Emit

// v0.4: Dictionary imports
Import.Dictionary.Life
Cell.Membrane.Permeability    // Life Dictionary Objects available

Import.Dictionary.Consciousness.As.Con
Con.Awareness.Level           // Aliased access
```

---

## 3.91 Export (External Exposure)

Marks Objects as accessible outside the current Dictionary.

```
Structure Export @ 3.91 {
    Export := External_Exposure
    Export : Module
    Export : Interface
    Export : Mode = Strict
}
```

**Syntax:**
```
Object.Export
[Object1, Object2, Object3].Export
```

**Behavior:**
- Exported Objects become available when this Dictionary is imported elsewhere
- Non-exported Objects are internal only

**Example:**
```
// In "MathUtils" dictionary
Structure Square @ 2.6.1 {
    Square := {N.Mul.N}
    Square : Mode = Strict
}

Structure Cube @ 2.6.2 {
    Cube := {N.Mul.N.Mul.N}
    Cube : Mode = Strict
}

InternalHelper.Return.{...}  // Not exported

[Square, Cube].Export

// In another dictionary
Import.MathUtils
5.Square        // Works: Returns 25
5.Cube          // Works: Returns 125
InternalHelper  // Stalls: Not exported
```

---

## 3.99 Section 3.0 Summary

| Address | Label | Description | Mode |
|---------|-------|-------------|------|
| 3.0 | Grammar | Built-in operations | Strict |
| 3.1 | Then | Conditional execution | Strict |
| 3.11 | Else | Alternative branch | Strict |
| 3.12 | When | Pattern matching | Strict |
| 3.2 | Cycle | Collection iteration | Strict |
| 3.21 | Item | Current cycle element | Strict |
| 3.22 | Times | Counted iteration | Strict |
| 3.23 | Index | Current cycle index | Strict |
| 3.24 | While | Conditional loop | Strict |
| 3.25 | Break | Loop exit | Strict |
| 3.26 | Skip | Iteration skip | Strict |
| 3.3 | Emit | Output to device | Strict |
| 3.31 | Format | Template formatting | Strict |
| 3.4 | Capture | Input from device | Strict |
| 3.41 | Prompt | Interactive input | Strict |
| 3.5 | As | Aliasing | Strict |
| 3.51 | Into | Value assignment | Strict |
| 3.6 | Return | Function definition | Strict |
| 3.61 | Parameters | Function inputs | Strict |
| 3.62 | Yield | Early return | Strict |
| 3.7 | Try | Error handling | Strict |
| 3.71 | Must | Resolution assertion | Strict |
| 3.8 | With | Context block | Strict |
| 3.81 | Global | Persistent scope | Strict |
| 3.82 | Local | Volatile scope | Strict |
| 3.9 | Import | External loading | Strict |
| 3.91 | Export | External exposure | Strict |

---

# Section 4.0: Workspace

The Workspace is the runtime memory space where program execution occurs. All user-created **Instances**, temporary values, and mutable state reside here. This is the only section where Objects are fully mutable.

```
Structure Workspace @ 4.0 {
    Workspace := Runtime_Container
    Workspace : Memory
    Workspace : Mutable
    Workspace : Mode = Strict    // No inference on runtime operations
}
```

**Section Mutability Summary (v0.4):**

| Section | Purpose | Mutability | Contains |
|---------|---------|------------|----------|
| 0.x | Kernel | Read-only | Structures (imports) |
| 1.x | Objects | Append-only | Structures (definitions) |
| 2.x | Relations | Append-only | Structures (rules) |
| 3.x | Grammar | Read-only | Structures (operations) |
| **4.x** | **Workspace** | **Read-write** | **Instances (runtime)** |
| 5.x | Interpreter | Read-only | Structures (engine) |
| 6.x+ | Domains | Append-only | Structures (per Dictionary) |

**Key Distinctions:**
- Sections 0-3, 5 contain **Structures** (immutable prototypes)
- Section 4 contains **Instances** (mutable runtime objects)
- Sections 6+ contain **Structures** from domain Dictionaries (per Amendment F)
- Attempting to modify a Structure stalls; Instances are freely mutable
- Structures may **Evolve** to produce successors (Amendment E), but the original is never modified

---

## 4.1 Global (Persistent Scope)

Global is the persistent memory space for Instances. Objects placed here remain accessible throughout program execution until explicitly deleted.

```
Structure Global @ 4.1 {
    Global := Heap
    Global : Scope
    Global : Persistent
    Global : Mode = Strict
}
```

**Behavior:**
- Instances in 4.1.x persist for program lifetime
- Accessible from any scope
- Must be explicitly deleted to free memory
- Default location for top-level Instance creation

**Creating Global Instances (v0.3 syntax):**

```
// Instance from Structure (preferred v0.3 method)
Fido := Dog.New
// Fido is Instance at 4.1.x with Prototype = Dog

// Instance with initialization
Alice := Person.New.(Name = "Alice", Age = 30)
// Alice at 4.1.x with specified properties

// Using As.Global for explicit placement
TempValue.As.Global.PermanentValue

// Direct value assignment (creates anonymous Instance)
Counter := 0
// Implicitly placed at 4.1.x as Number Instance
```

**Accessing Global Instances:**

Global Instances are accessible by Label from anywhere:

```
Structure Increment @ 2.x {
    Increment := {
        GlobalCounter.Add.1.Into.GlobalCounter
        // GlobalCounter accessible inside function
    }
    Increment : Mode = Strict
}
```

**Deleting Global Instances:**

```
Fido = Null
// Fido's Contents become Null

Fido.Delete
// Fido is removed from Dictionary entirely
// Address 4.1.x freed for reuse
```

---

## 4.11 Global Address Allocation

When Instances are created in Global scope, they receive the next available address via auto-allocation (leveraging Amendment A principles at runtime).

```
First := "A"      // Address: 4.1.1
Second := "B"     // Address: 4.1.2
Third := "C"      // Address: 4.1.3
```

**Nested Instance Properties:**

Child properties receive addresses under their parent:

```
Person := Person.New
// Person at 4.1.1

Person.Name := "Alice"    // Address: 4.1.1.1
Person.Age := 30          // Address: 4.1.1.2
Person.Pet := Dog.New     // Address: 4.1.1.3
```

**Address Reuse:**

Deleted addresses may be reused:

```
A := 1            // 4.1.1
B := 2            // 4.1.2
A.Delete          // 4.1.1 freed
C := 3            // 4.1.1 (reused)
```

**Runtime Scope Block (v0.3):**

For explicit control over runtime address allocation:

```
Scope(4.1) {
    Config := Settings.New,      // 4.1.1
    Database := Connection.New,  // 4.1.2
    Cache := Store.New           // 4.1.3
}
```

---

## 4.12 Global Persistence

Global Instances survive scope changes:

```
Structure Initialize @ 2.x {
    Initialize := {
        Config := Settings.New
        Config.Debug := True
        Config.Version := "1.0"
    }
}

Structure Main @ 2.x {
    Main := {
        Initialize.
        Config.Debug.Emit    // Works: Config persists
        // Output: True
    }
}
```

Global Instances are shared across function calls:

```
Counter := 0

Structure Increment @ 2.x {
    Increment := {
        Counter.Add.1.Into.Counter
    }
    Increment : Mode = Strict
}

Increment    // Counter = 1
Increment    // Counter = 2
Increment    // Counter = 3
Counter.Emit // Output: 3
```

---

## 4.2 Local (Volatile Scope)

Local is the volatile memory space. Instances placed here exist only within their enclosing scope (function, cycle, or block).

```
Structure Local @ 4.2 {
    Local := Stack
    Local : Scope
    Local : Volatile
    Local : Mode = Strict
}
```

**Behavior:**
- Instances in 4.2.x exist only within current scope
- Automatically deleted when scope exits
- Not accessible from outer or sibling scopes
- Used for temporary values and function parameters

**Creating Local Instances:**

```
// Explicit local assignment
Value.As.Local.TempValue

// Function parameters are automatically Local
MyFunc.Return.(A, B).{
    // A and B are Local Instances at 4.2.x
    A.Add.B
}

// Cycle bindings are automatically Local
List.Cycle.{
    // Item is Local to each iteration
    Item.Emit
}
```

---

## 4.21 Local Scope Boundaries

Local scope is bounded by:

**Functions:**
```
OuterFunc.Return.{
    X := 10                     // Global Instance
    X.As.Local.Y                // Local Instance to OuterFunc
    
    InnerFunc.Return.{
        Y.Emit                  // Stalls: Y not accessible here
        X.Emit                  // Works: X is Global
    }
    
    InnerFunc
    Y.Emit                      // Works: still in OuterFunc scope
}
// Y is deleted when OuterFunc exits
```

**Cycles:**
```
Numbers := [1, 2, 3]

Numbers.Cycle.{
    Item.As.Local.Current       // Local to this iteration
    Current.Square.Emit
}
// Current is deleted after each iteration

Current.Emit                    // Stalls: Current doesn't exist
```

**Blocks (With):**
```
Config.With.{
    Value.As.Local.Temp         // Local to this block
    Temp.Process
}
// Temp is deleted when block exits
```

---

## 4.22 Local Stack Behavior

Local memory operates as a stack:

```
Outer.Return.{
    A.As.Local.X        // Push X onto stack
    
    Inner.Return.{
        B.As.Local.Y    // Push Y onto stack
        X.Emit          // X accessible (below on stack)
        Y.Emit          // Y accessible (top of stack)
    }
    // Y popped from stack
    
    Inner
    X.Emit              // X still accessible
    Y.Emit              // Stalls: Y no longer exists
}
// X popped from stack
```

**Stack frames are created for:**
- Each function call
- Each cycle iteration
- Each With block

---

## 4.23 Shadowing

Local Instances may shadow Global Instances with the same Label:

```
Name := "Global Alice"          // Global Instance

Greet.Return.{
    Name.As.Local.Name          // Local shadows Global
    "Local Bob".Into.Name
    Name.Emit                   // Output: Local Bob
}

Greet
Name.Emit                       // Output: Global Alice
// Global unchanged
```

**Resolution order:**
1. Local scope (current frame)
2. Enclosing Local scopes (outer frames)
3. Global scope (4.1)
4. Structures (0.x - 3.x) — for type/relation lookup only

---

## 4.3 Context (Execution State)

Context is a special runtime Instance tracking the current state of execution.

```
Structure Context @ 4.3 {
    Context := Execution_State
    Context : Runtime
    Context : Implicit
    Context : Mode = Strict
    
    Scope {
        Scope_Address := Address,
        Previous_Subject := Reference,
        Previous_Result := Any,
        Current_Object := Reference,
        Current_Iteration := Any,
        Current_Index := Number,
        Call_Stack := List
    }
}
```

**Context Components:**

| Field | Type | Description |
|-------|------|-------------|
| Scope_Address | Address | Current scope location (4.1 or 4.2.x) |
| Previous_Subject | Reference | Last Object acted upon |
| Previous_Result | Any | Output of last resolved expression |
| Current_Object | Reference | Object containing executing Logic |
| Current_Iteration | Any | Current Item in Cycle |
| Current_Index | Number | Current index in Times/Cycle |
| Call_Stack | List | Stack of active function calls |

**Context is updated automatically by the Interpreter.**

---

## 4.31 Context Pronouns

Pronouns resolve against Context (as defined in Section 1.9):

```
// Defined in Structure section, resolve at runtime
It   → Context.Previous_Subject
That → Context.Previous_Result
Self → Context.Current_Object
Item → Context.Current_Iteration
Index → Context.Current_Index
```

---

## 4.32 Call Stack

The Call Stack tracks nested function invocations:

```
A.Return.{
    "In A".Emit
    B
}

B.Return.{
    "In B".Emit
    C
}

C.Return.{
    "In C".Emit
    Context.Call_Stack.Emit
}

A
// Output: In A
// Output: In B
// Output: In C
// Output: [A, B, C]
```

**Stack overflow:**
The Interpreter limits Call Stack depth. Exceeding the limit stalls execution.

```
Infinite.Return.{
    Infinite    // Recursive call
}

Infinite
// Stalls: Maximum call depth exceeded
```

---

## 4.4 Instances (Object Creation)

Instances are runtime Objects created from Structure definitions (0.x-3.x). This section formalizes Amendment B's Structure/Instance distinction.

```
Structure Instance @ 4.4 {
    Instance := Runtime_Object
    Instance : Created_From = Structure
    Instance : Mutable = True
    Instance : Mode = Strict
}
```

**Syntax:**
```
Structure.New
Structure.New.(Arguments)
```

**Behavior:**
1. Verify source is a Structure (not an Instance)
2. Create new Instance in Workspace (4.x)
3. Copy Structure's Metadata to Instance
4. Add Instance-specific metadata (Prototype, Instance_ID, Created_At)
5. Apply Arguments to Instance properties
6. Return Instance

---

## 4.41 Instance Identity

Each Instance has a unique Address, even if created from the same Structure:

```
A := Person.New
B := Person.New

A.Address.Emit    // 4.1.1
B.Address.Emit    // 4.1.2

A.Identical.B     // False (different Addresses)
A.Eq.B            // False (different Instances)
```

**Instance Identity Operations (v0.4):**

| Operation | Meaning |
|-----------|---------|
| A.Identical.B | Same Address (same object) |
| A.Eq.B | Same value (equivalent content) |
| A.Is.Type | A's Prototype chain includes Type |
| A.Prototype | Returns Structure that created A |
| A.Prototype.Version | Returns version of the Prototype (v0.4) |

---

## 4.42 Instance Hierarchy

Instances may contain child Instances:

```
Structure Team @ 1.2 {
    Team := Group
    Team : Members = []
}

Structure Person @ 1.1 {
    Person := Human
    Person : Name = Null
}

// Create team with members
DevTeam := Team.New
Alice := Person.New.(Name = "Alice")
Bob := Person.New.(Name = "Bob")

DevTeam.Members.Add.Alice
DevTeam.Members.Add.Bob

DevTeam.Members.Cycle.{Item.Name.Emit}
// Output: Alice
// Output: Bob
```

---

## 4.43 Instance Type Checking

Formal type checking for Instances:

```
Fido := Dog.New
Whiskers := Cat.New

// Type checking
Fido.Is.Dog         // True (direct prototype)
Fido.Is.Pet         // True (if Dog : Pet in Structure)
Fido.Is.Animal      // True (if Pet : Animal)
Fido.Is.Cat         // False

// Prototype access
Fido.Prototype      // Returns -> Dog (the Structure)
Fido.Prototype.Prototype  // Returns -> Pet (if defined)

// Runtime type verification
Fido.Is.Pet.Then.{
    "Fido is a pet".Emit
}
```

---

## 4.5 References and Copying

**References:**

By default, assignment creates a reference, not a copy:

```
Original := [1, 2, 3]
Alias := Original

Alias.Add.4
Original.Emit       // Output: [1, 2, 3, 4]
// Both point to same Instance
```

**Shallow Copy:**

```
Structure Copy @ 4.5 {
    Copy := Duplicator
    Copy : Mode = Strict
}
```

```
Original := [1, 2, 3]
Duplicate := Original.Copy

Duplicate.Add.4
Original.Emit       // Output: [1, 2, 3]
Duplicate.Emit      // Output: [1, 2, 3, 4]
// Different Instances
```

**Deep Copy:**

```
Structure DeepCopy @ 4.51 {
    DeepCopy := Recursive_Duplicator
    DeepCopy : Mode = Strict
}
```

```
Nested := [[1, 2], [3, 4]]
Shallow := Nested.Copy
Deep := Nested.DeepCopy

Shallow.0.Add.5
Nested.0.Emit       // Output: [1, 2, 5] (affected)

Deep.1.Add.6
Nested.1.Emit       // Output: [3, 4] (unaffected)
```

---

## 4.6 Garbage Collection

The Interpreter automatically reclaims unreachable memory.

```
Structure GarbageCollector @ 4.6 {
    GarbageCollector := Memory_Reclaimer
    GarbageCollector : Automatic = True
    GarbageCollector : Mode = Strict
}
```

**Triggers:**
- Local scope exit (immediate)
- Global Instance unreachable (periodic)
- Explicit deletion (immediate)

**Note:** Structures (0.x-3.x) are never garbage collected—they persist for program lifetime. Snapshots are also never garbage collected unless explicitly deleted—they are historical records.

---

## 4.61 Memory Limits

The Workspace has finite capacity:

```
Workspace.Capacity      // Maximum Instances
Workspace.Used          // Current Instance count
Workspace.Available     // Remaining capacity
```

**Overflow behavior:**

When Workspace is full:
1. Garbage collection runs
2. If still full, new allocations stall
3. Interpreter reports memory exhaustion

```
Workspace.Available.Lt.100.Then.{
    "Warning: Low memory".Emit
}
```

---

## 4.7 State (Snapshots)

State captures the entire Workspace at a moment in time. **v0.4 generalizes this via Amendment D's Snapshot construct, which allows fine-grained capture of any Object, not just the entire Workspace.**

```
Structure State @ 4.7 {
    State := Workspace_Snapshot
    State : Checkpoint
    State : Immutable = True
    State : Mode = Strict
}
```

**Capture State (Workspace-level):**

```
Checkpoint := Workspace.State.Capture
// Checkpoint contains snapshot of all 4.x Instances
// Equivalent to: Workspace.Snapshot (v0.4 syntax)
```

**Restore State:**

```
Checkpoint.Restore
// Workspace returns to captured state
// All changes since Checkpoint are discarded
```

**Fine-grained Snapshot (v0.4):**
```
// Capture a single Instance
Alice_Checkpoint := Alice.Snapshot.(Tag = "before_surgery")

// Compare
Alice_Checkpoint.Diff.Alice.Snapshot
// Returns delta between saved state and current state

// Restore single Instance
Alice.Restore.Alice_Checkpoint
```

**Use cases:**
- Transaction rollback
- Speculative execution
- Debugging/replay
- Audit trails (v0.4)
- Evolution lineage tracking (v0.4)

---

## 4.71 Branching Workspaces

When resolution stalls, the Interpreter may create branching Workspace states:

```
Structure Branch @ 4.71 {
    Branch := Workspace_Fork
    Branch : Speculative = True
    Branch : Pending = True
    Branch : Mode = Strict
}
```

**Behavior:**
1. Expression stalls
2. Interpreter snapshots current State
3. Creates Branch with pending expression
4. Continues main execution
5. May revisit Branch if context changes

**Note (v0.4):** Productive Stalls do NOT create branches. They are intentionally permanent and never revisited.

**Manual branching:**

```
Speculate := Workspace.Branch.Create

Speculate.With.{
    // Experimental changes here
    RiskyOperation
}

RiskyOperation.Succeeded.Then.Speculate.Merge
RiskyOperation.Failed.Then.Speculate.Discard
```

---

## 4.8 Workspace Structure Summary

```
4.0 Workspace
├── 4.1 Global (Persistent Instances)
│   ├── 4.1.1 UserInstance1
│   ├── 4.1.2 UserInstance2
│   │   ├── 4.1.2.1 ChildProperty
│   │   └── 4.1.2.2 ChildProperty
│   └── 4.1.x ...
│
├── 4.2 Local (Volatile Instances)
│   ├── 4.2.1 StackFrame1
│   │   ├── 4.2.1.1 LocalVar
│   │   └── 4.2.1.2 LocalVar
│   ├── 4.2.2 StackFrame2
│   │   └── 4.2.2.x ...
│   └── 4.2.x ...
│
├── 4.3 Context
│   ├── 4.3.1 Scope_Address
│   ├── 4.3.2 Previous_Subject
│   ├── 4.3.3 Previous_Result
│   ├── 4.3.4 Current_Object
│   ├── 4.3.5 Current_Iteration
│   ├── 4.3.6 Current_Index
│   └── 4.3.7 Call_Stack
│
├── 4.4 Instances (metadata about instance system)
│
├── 4.5 References
│   └── 4.51 DeepCopy
│
├── 4.6 GarbageCollector
│   └── 4.61 Limits
│
├── 4.7 State
│   └── 4.71 Branches
│
└── 4.8 Snapshots (v0.4 — Instance-level snapshot registry)
```

---

## 4.99 Section 4.0 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 4.0 | Workspace | Runtime memory container |
| 4.1 | Global | Persistent scope (heap) |
| 4.11 | Address Allocation | Global address assignment |
| 4.12 | Persistence | Cross-scope survival |
| 4.2 | Local | Volatile scope (stack) |
| 4.21 | Scope Boundaries | Function/cycle/block limits |
| 4.22 | Stack Behavior | LIFO memory model |
| 4.23 | Shadowing | Local overrides global |
| 4.3 | Context | Execution state |
| 4.31 | Pronouns | Context-derived references |
| 4.32 | Call Stack | Function invocation trace |
| 4.4 | Instances | Runtime object creation |
| 4.41 | Identity | Unique instance addresses |
| 4.42 | Hierarchy | Nested instances |
| 4.43 | Type Checking | Prototype verification |
| 4.5 | References | Aliasing vs copying |
| 4.51 | DeepCopy | Recursive duplication |
| 4.6 | GarbageCollector | Memory reclamation |
| 4.61 | Limits | Capacity constraints |
| 4.7 | State | Workspace snapshots |
| 4.71 | Branches | Speculative forks |
| 4.8 | Snapshots | Instance-level snapshot registry (v0.4) |

---

# Section 5.0: Interpreter

The Interpreter is the engine that reads, resolves, and executes Uypocode. It transforms a Dictionary specification into runtime behavior. v0.4 extends the Interpreter with Snapshot capture, Evolution processing, Dictionary loading, and Productive Stall handling.

```
Structure Interpreter @ 5.0 {
    Interpreter := Execution_Engine
    Interpreter : Parser
    Interpreter : Resolver
    Interpreter : Runtime
    Interpreter : Mode = Strict
}
```

The Interpreter is designed for:
- Graceful handling of incomplete specifications
- **Mode-controlled** semantic inference when explicit rules are absent
- Human-AI collaboration and inspection
- Non-deterministic convergence on optimal resolutions
- **Structure/Instance distinction** enforcement
- **Snapshot capture and restoration** (v0.4)
- **Evolution lineage tracking** (v0.4)
- **Dictionary dependency resolution** (v0.4)
- **Productive Stall segregation** (v0.4)

---

## 5.1 Interpretation Pipeline

The Interpreter operates in **eight** sequential phases (v0.4 adds Dictionary Loading and Evolution Registration):

```
Structure Pipeline @ 5.1 {
    Pipeline := Execution_Sequence
    Pipeline : Mode = Strict
}
```

| Phase | Name | Purpose | Since |
|-------|------|---------|-------|
| 1 | Tokenization | Break source into tokens | v0.2 |
| 2 | **Dictionary Loading** | Load and validate imported Dictionaries | v0.4 |
| 3 | Structure Registration | Identify and register Structures | v0.3 |
| 4 | **Evolution Registration** | Process Evolve declarations, build lineage | v0.4 |
| 5 | Indexing | Build address tree from declarations | v0.2 |
| 6 | Definition | Populate Contents and Metadata | v0.2 |
| 7 | Resolution | Execute dot-expressions | v0.2 |
| 8 | Finalization | Report stalls, clean up | v0.2 |

```
Source → Tokenize → Load Dictionaries → Register Structures → Register Evolutions 
    → Index → Define → Resolve → Output
                          ^          |
                          |__________|
                          (Context updates)
```

---

## 5.11 Phase 1: Tokenization

The Tokenizer breaks raw source text into discrete tokens.

```
Structure Tokenizer @ 5.11 {
    Tokenizer := Lexical_Analyzer
    Tokenizer : Mode = Strict
}
```

**Token Types (v0.4 additions in bold):**

| Type | Pattern | Examples |
|------|---------|----------|
| Label | `[A-Za-z_][A-Za-z0-9_]*` | `Dog`, `my_var`, `_temp` |
| Number | `[0-9]+\.?[0-9]*` | `42`, `3.14`, `0` |
| Text | `"[^"]*"` | `"Hello"`, `""` |
| Operator | `:=`, `:`, `.`, `=`, `@` | |
| Grouping | `(`, `)`, `[`, `]`, `{`, `}` | |
| Keyword | `Structure`, `Scope`, `Mode`, **`Evolve`**, **`Dictionary`**, **`Snapshot`**, **`PRODUCTIVE_STALL`** | |
| Separator | `,`, newline | |
| Comment | `//` to end of line | `// This is ignored` |

---

## 5.112 Phase 2: Dictionary Loading (v0.4)

The Dictionary Loader processes `Import.Dictionary` statements and loads external dictionaries.

```
Structure DictionaryLoader @ 5.112 {
    DictionaryLoader := External_Dictionary_Resolver
    DictionaryLoader : Mode = Strict
}
```

**Behavior:**
1. Scan for `Import.Dictionary.*` statements
2. For each import, locate the Dictionary specification
3. Validate Dictionary metadata (Name, Version, Claims)
4. Check for address range conflicts with already-loaded Dictionaries
5. Resolve Dependencies recursively (detect circular dependencies → Stall)
6. Merge Dictionary Structures into the current address space
7. Register Kernel Extensions under 0.x

**Dictionary Registry:**
```
DictionaryRegistry := {
    "Life": {
        Address: 0.6.1,
        Version: 1.0,
        Claims: [7.0, 7.99],
        Loaded: True,
        Exports: [Cell, Organism, Ecosystem, ...]
    },
    "Consciousness": {
        Address: 0.6.6,
        Version: 0.2,
        Claims: [6.0, 6.99],
        Loaded: True,
        Exports: [Awareness, Qualia, Self_Model, ...]
    }
}
```

---

## 5.115 Phase 3: Structure Registration

The Structure Registrar identifies and validates Structure declarations.

```
Structure StructureRegistrar @ 5.115 {
    StructureRegistrar := Structure_Validator
    StructureRegistrar : Mode = Strict
}
```

**Behavior:**
1. Find all `Structure Label @ Address { ... }` declarations
2. Verify Address is in range 0.x - 3.x (or 6.x+ for domain Dictionaries)
3. Mark Object as immutable Structure
4. Extract Mode metadata if present
5. Register in Structure Table

**Validation Rules:**
- Structure keyword requires explicit address via `@`
- Address must be in 0.x-3.x or in a claimed Dictionary range (6.x+)
- Address must NOT be in 4.x (Workspace — reserved for Instances)
- Mode must be one of: Strict, Guided, Open
- Duplicate addresses cause ParseError

---

## 5.116 Phase 4: Evolution Registration (v0.4)

The Evolution Registrar processes `Evolve` declarations and builds lineage chains.

```
Structure EvolutionRegistrar @ 5.116 {
    EvolutionRegistrar := Lineage_Builder
    EvolutionRegistrar : Mode = Strict
}
```

**Behavior:**
1. Find all `OldStructure.Evolve @ NewAddress { ... }` declarations
2. Verify OldStructure exists and is a registered Structure
3. Verify NewAddress is unique and in a valid range
4. Create automatic Snapshot of OldStructure (Amendment D)
5. Build successor Structure at NewAddress with inherited + overridden metadata
6. Set OldStructure.Successor = -> NewAddress
7. Set NewStructure.Predecessor = -> OldAddress
8. Set NewStructure.Version = OldStructure.Version + 1
9. Update Label resolution table: Label now resolves to latest version
10. Register in Evolution Table

**Evolution Table:**
```
EvolutionTable := {
    "Dog": {
        Versions: [
            {Version: 1, Address: 1.4.1, Evolved_At: Null},
            {Version: 2, Address: 1.4.2, Evolved_At: Timestamp}
        ],
        Current: -> 1.4.2
    }
}
```

---

## 5.12 Phase 5: Indexing

The Indexer scans for Object declarations and builds the Symbol Table.

```
Structure Indexer @ 5.12 {
    Indexer := Symbol_Table_Builder
    Indexer : Mode = Strict
}
```

**Behavior:**
1. Find all `:=` declarations (both Structure and Instance)
2. Extract Label and Address from each
3. Build tree structure from Addresses
4. Register Labels for lookup
5. Process Scope blocks for auto-addressing (Amendment A)
6. **Register Dictionary-provided Structures** (v0.4)
7. **Index Evolution lineage for version resolution** (v0.4)

**Symbol Table Structure (v0.4):**

```
SymbolTable := {
    Labels: {
        "Dog": 1.4.2,          // Resolves to latest version (v0.4)
        "Dog.V1": 1.4.1,       // Explicit version access (v0.4)
        "Dog.V2": 1.4.2,       // Explicit version access (v0.4)
        "Animal": 1.1,
        "Speak": 2.1,
        ...
    },
    Addresses: {
        1.1: {Label: "Animal", Children: [1.4.1, 1.4.2], IsStructure: True, Mode: Open},
        1.4.1: {Label: "Dog", Children: [], IsStructure: True, Mode: Strict, Successor: 1.4.2},
        1.4.2: {Label: "Dog", Children: [], IsStructure: True, Mode: Strict, Predecessor: 1.4.1},
        ...
    },
    ScopeCounters: { ... },
    Dictionaries: {
        "Life": {Range: [7.0, 7.99], Exports: [...]},
        ...
    }
}
```

---

## 5.13 Phase 6: Definition

The Definer populates Object Contents and Metadata.

```
Structure Definer @ 5.13 {
    Definer := Content_Populator
    Definer : Mode = Strict
}
```

**Behavior:**
1. Process `:=` right-hand sides → set Contents
2. Process `:` statements → add Metadata
3. Resolve References (Labels to Addresses)
4. Inherit Mode from parent if not specified (v0.3)
5. Validate Instance creation from Structures (v0.3)
6. **Classify PRODUCTIVE_STALL declarations** (v0.4)
7. **Apply Evolution inheritance** (v0.4): copy unoverridden metadata from predecessor to successor

---

## 5.14 Phase 7: Resolution

The Resolver executes dot-expressions.

```
Structure Resolver @ 5.14 {
    Resolver := Expression_Executor
    Resolver : Mode = Strict
}
```

**Behavior:**
1. Find executable expressions (containing `.`)
2. Check Structure/Instance constraints (v0.3)
3. Resolve left-to-right
4. Apply Mode rules before semantic inference (v0.3)
5. **Handle Snapshot operations** (v0.4)
6. **Handle Evolution version resolution** (v0.4)
7. **Segregate Productive Stalls from standard stalls** (v0.4)
8. Update Context after each resolution
9. Collect results or stalls

This is the heart of execution. See §5.3 for the resolution algorithm.

---

## 5.15 Phase 8: Finalization

The Finalizer concludes execution.

```
Structure Finalizer @ 5.15 {
    Finalizer := Execution_Closer
    Finalizer : Mode = Strict
}
```

**Behavior:**
1. Check for unresolved stalls
2. **Separate standard stalls from Productive Stalls** (v0.4)
3. Report pending expressions with Mode information
4. **Report Productive Stalls in dedicated section** (v0.4)
5. Run garbage collection
6. Return final result or stall report

**Output Types:**

| Outcome | Description |
|---------|-------------|
| Success | All expressions resolved (Productive Stalls do not count as failures) |
| Partial | Some standard stalls remain, partial results available |
| Stalled | Primary expression could not resolve |

**Finalization Report (v0.4):**

```
Finalization Report:
    Status: Success
    Result: "Hello, world"
    
    Pending (standard stalls): []
    
    Productive Stalls (intentionally unresolved): [
        {
            Expression: "Qualia.Explain.Physically",
            Domain: "Consciousness",
            Reason: "Explanatory gap",
            Productive_Because: "Constrains viable theories"
        }
    ]
    
    Evolutions: [
        { Label: "Dog", V1: 1.4.1, V2: 1.4.2, Changes: {+Temperament} }
    ]
    
    Snapshots: 3 captured
    Dictionaries: 2 loaded (Life v1.0, Consciousness v0.2)
    Branches: 0 speculative states
```

---

## 5.3 Resolution Algorithm

The core algorithm for evaluating `A.B` expressions.

```
Structure ResolutionAlgorithm @ 5.3 {
    ResolutionAlgorithm := Dot_Evaluator
    ResolutionAlgorithm : Mode = Strict
}
```

### 5.31 Resolution Steps (v0.4)

```
Function: Resolve(Subject, Accessor)
Input: Subject (Object), Accessor (Label or Literal)
Output: Result (Object) or Stall

1. PRODUCTIVE STALL CHECK (v0.4)
   If Subject.Is.Productive_Stall:
       Return Subject (propagate — do not resolve through)
   
2. STRUCTURE MUTATION CHECK (v0.3)
   If Subject.IsStructure AND operation would mutate:
       Return Stall("Cannot modify Structure")
   
3. VERSION RESOLUTION (v0.4)
   If Accessor matches version pattern (V1, V2, Origin, Current, Lineage):
       Return appropriate version from Evolution Table

4. SNAPSHOT OPERATIONS (v0.4)
   If Accessor = "Snapshot":
       Return Snapshot of Subject
   If Accessor = "Restore":
       Validate Subject is Instance, apply Snapshot state
   If Accessor = "Snapshots":
       Return list of all Snapshots for Subject

5. CONTAINMENT CHECK
   If Accessor is a child of Subject (address prefix match):
       Return child Object
   
6. METADATA CHECK
   If Accessor exists in Subject's Metadata:
       Return Metadata value
   
7. RELATION CHECK
   Search 2.x for matching pattern:
       - Exact: Subject.Type.Accessor
       - Generic: Any.Accessor
   If found:
       Substitute Subject into Relation Logic
       Recursively resolve Logic
       Return result
   
8. GRAMMAR CHECK
   If Accessor is a 3.x Grammar operation:
       Apply operation to Subject
       Return result
   
9. MODE CHECK (v0.3 — Amendment C)
   Subject.Mode.When.[
       Strict : Return Stall("Inference blocked by Strict mode"),
       Guided : {
           Pattern := Subject.Inference_Pattern.
           Pattern.Eq.Null.Then.Return Stall("No inference pattern").
           Accessor.Match.Pattern.Not.Then.Return Stall("Pattern mismatch").
           // Continue to semantic check with pattern constraint
       },
       Open : // Continue to semantic check freely
   ]

10. SEMANTIC CHECK (if NLP enabled and Mode permits)
    Query NLP: "What is the relationship between {Subject.Label} and {Accessor}?"
    If confident answer:
        Create temporary Relation
        Recursively resolve
        Return result
   
11. STALL
    Record pending expression with Mode info
    Return Stall marker
```

---

## 5.4 Stall Handling

When resolution fails, expressions stall rather than error.

```
Structure Stall @ 5.4 {
    Stall := Pending_Expression
    Stall : Expression
    Stall : Reason
    Stall : Mode
    Stall : Context_Snapshot
    Stall : Retry_Conditions
    Stall : Stall_Type = "Standard"    // v0.4: or "Productive"
    Stall : Mode_Setting = Strict
}
```

### 5.41 Stall Creation (v0.4)

```
Function: CreateStall(Expression, Reason, SubjectMode, Type)

1. Capture current Context
2. Record Expression that failed
3. Record Subject's Mode
4. Determine Type (v0.4):
       - If Expression declared as PRODUCTIVE_STALL → Type = Productive
       - Otherwise → Type = Standard
5. If Type = Productive:
       Add to Productive_Stall_Registry
       Do NOT set RetryWhen conditions
   Else:
       Determine retry conditions
       Add to Pending list
6. Return Stall marker with Type
```

### 5.42 Stall Propagation

Stalls propagate through chains:

```
A.B.C.D
    ^
    B stalls
```

When B stalls:
1. Record stall for A.B with Mode information and Stall Type
2. Entire chain A.B.C.D stalls
3. Store C.D as continuation
4. If A.B later resolves (Standard only), continuation executes
5. **Productive Stalls propagate permanently—continuations are never executed**

### 5.43 Stall Resolution

Standard stalls may resolve when the Dictionary changes:

```
Function: CheckStalls()
Trigger: After any Dictionary modification

1. For each Stall in Pending:
       // Skip Productive Stalls entirely (v0.4)
       If Stall.Stall_Type = Productive:
           Continue (never retry)
       
       If Stall.Inference_Blocked AND Subject.Mode = Strict:
           Continue (still blocked)
       
       If RetryWhen conditions met:
           Restore Context from snapshot
           Attempt Resolution again
           If success:
               Remove from Pending
               Execute continuation
           If still stalled:
               Update Stall record
```

---

### 5.44 Stall Modes (Interpreter Setting)

The Interpreter itself has modes for handling stalls:

| Mode | Behavior |
|------|----------|
| Strict | Stalls halt execution immediately |
| Lenient | Stalls recorded, execution continues |
| Speculative | Stalls create branches (see §4.71) |
| Interactive | Stalls prompt user for resolution |

**Note:** This is the Interpreter's stall-handling mode, distinct from the Object Mode (Strict/Guided/Open) and the Stall Type (Standard/Productive).

**Setting mode:**

```
Interpreter.Stall_Mode = "Lenient"
```

---

## 5.5 Context Management

The Interpreter maintains Context throughout execution.

```
Structure ContextManager @ 5.5 {
    ContextManager := State_Tracker
    ContextManager : Mode = Strict
}
```

### 5.51 Context Updates

Context updates after each resolved expression:

```
Function: UpdateContext(Subject, Result)

1. Context.Previous_Subject = Subject
2. Context.Previous_Result = Result
3. If entering function:
       Push new frame to Call_Stack
       Context.Scope_Address = new Local address
4. If exiting function:
       Pop frame from Call_Stack
       Context.Scope_Address = previous Scope
5. If in Cycle:
       Context.Current_Iteration = current Item
       Context.Current_Index = current Index
```

---

## 5.6 Semantic Inference (Mode-Controlled)

When explicit resolution fails, the Interpreter may use semantic inference **if Mode permits** (Amendment C).

```
Structure SemanticEngine @ 5.6 {
    SemanticEngine := NLP_Resolver
    SemanticEngine : Optional = True
    SemanticEngine : Requires = Import.English
    SemanticEngine : Mode = Strict
}
```

### 5.61 Inference Trigger (v0.4)

Semantic inference activates when:
1. All explicit resolution steps fail
2. `Import.English` is loaded
3. Subject and Accessor are meaningful Labels
4. Subject's Mode permits inference (v0.3)
5. **Expression is not a declared PRODUCTIVE_STALL** (v0.4)

### 5.63 Inference Confidence

The Interpreter requires confidence thresholds:

```
SemanticEngine.Threshold = 0.8   // 80% confidence required
```

| Confidence | Action |
|------------|--------|
| ≥ 0.8 | Accept inference, create Relation |
| 0.5 - 0.8 | Interactive: ask user to confirm (if Interactive mode) |
| < 0.5 | Reject inference, stall |

### 5.64 Inference Caching

Successful inferences are cached to avoid repeated NLP queries:

```
InferenceCache := {
    "Animal.Sleep": {Relation: 2.temp.1, Confidence: 0.95, Mode: Open},
    "Bird.Fly": {Relation: 2.temp.2, Confidence: 0.92, Mode: Open},
    ...
}
```

Cached inferences persist for the session but are not saved to the Dictionary unless explicitly promoted:

```
Animal.Sleep.Promote
// Moves temporary Relation to permanent 2.x address
```

---

## 5.7 Execution Model

How the Interpreter runs code.

```
Structure ExecutionModel @ 5.7 {
    ExecutionModel := Runtime_Behavior
    ExecutionModel : Mode = Strict
}
```

### 5.71 Eager vs Lazy Evaluation

Uypocode uses **lazy evaluation** by default:

| Strategy | Description | Used For |
|----------|-------------|----------|
| Lazy | Evaluate only when needed | Properties, Relations |
| Eager | Evaluate immediately | Assignments, Grammar ops, Instance creation, Snapshots |

### 5.72 Evaluation Order

Within a statement, evaluation proceeds:
1. Left to right for dot chains
2. Inner to outer for nested groups
3. Arguments before application

### 5.73 Concurrency

The Interpreter may evaluate independent expressions concurrently:

```
[A.Compute, B.Compute, C.Compute].Parallel
```

**Structure/Instance consideration:** Parallel operations must not attempt to modify the same Instance concurrently.

### 5.74 Tail Call Optimization

Recursive functions with tail calls are optimized:

```
Factorial.Return.(N, Acc = 1).{
    N.Eq.0.Then.Acc.Yield.
    Factorial.(N.Sub.1, Acc.Mul.N)    // Tail call
}
```

---

## 5.8 Error Handling

Beyond stalls, the Interpreter handles fatal errors.

```
Structure ErrorHandler @ 5.8 {
    ErrorHandler := Exception_Manager
    ErrorHandler : Mode = Strict
}
```

### 5.81 Error Types (v0.4)

| Error | Cause | Recovery | Since |
|-------|-------|----------|-------|
| ParseError | Invalid syntax | Report, skip to next statement | v0.2 |
| TypeError | Operation on wrong type | Stall or coerce | v0.2 |
| StructureError | Attempt to modify Structure | Stall with suggestion | v0.3 |
| ModeError | Invalid Mode value | Report, use default | v0.3 |
| **EvolutionError** | Invalid Evolve declaration | Report, skip | v0.4 |
| **DictionaryError** | Dictionary load failure | Report, skip imports | v0.4 |
| **SnapshotError** | Restore to incompatible Snapshot | Stall with diagnostic | v0.4 |
| StackOverflow | Infinite recursion | Halt current call chain | v0.2 |
| MemoryExhausted | Workspace full | GC, then halt if still full | v0.2 |
| IOError | File/device failure | Stall with retry option | v0.2 |
| Halt | Explicit Must failure | Stop execution | v0.2 |

---

## 5.9 Interpreter Interface

How external systems interact with the Interpreter.

### 5.91 REPL Mode

Interactive read-eval-print loop (v0.4):

```
Uypocode REPL v0.4
> Structure Dog @ 1.4.1 {
.     Dog := Animal
.     Dog : Sound = "Bark"
.     Dog : Mode = Strict
. }
Registered: Structure Dog at 1.4.1 (Mode: Strict)

> Dog.Evolve @ 1.4.2 {
.     Dog : Temperament = "Loyal"
. }
Evolved: Dog V1 (1.4.1) → V2 (1.4.2) [+Temperament]
Snapshot: Dog_V1 captured automatically

> Fido := Dog.New
Created: Instance Fido at 4.1.1 (Prototype: Dog V2)

> Fido.Snapshot.(Tag = "initial")
Captured: Snapshot of Fido (Tag: "initial")

> Fido.Temperament.Emit
Loyal

> Mystery := PRODUCTIVE_STALL.(Domain = "Test", Reason = "Unknown")
Registered: Productive Stall 'Mystery'

> :stalls
Pending (standard): 0
Productive: 1
  - Mystery: "Unknown" (Domain: Test)

> :structures
Structures:
  1.4.1 Dog V1 : Animal (Mode: Strict) [evolved → 1.4.2]
  1.4.2 Dog V2 : Animal (Mode: Strict) [current]

> :exit
Goodbye
```

**REPL Commands (v0.4):**

| Command | Description |
|---------|-------------|
| `:stalls` | List pending stalls, Productive Stalls separate |
| `:dictionary` | Show current Dictionary |
| `:structures` | List all Structures with lineage |
| `:instances` | List all Instances |
| `:context` | Show current Context |
| `:snapshots` | List all captured Snapshots |
| `:evolutions` | Show Evolution lineage for all Structures |
| `:dictionaries` | Show loaded domain Dictionaries |
| `:productive` | List all Productive Stalls |
| `:reset` | Clear Workspace (Instances only) |
| `:load <file>` | Load Uypocode file |
| `:save <file>` | Save Dictionary to file |
| `:exit` | Exit REPL |

---

### 5.92 Batch Mode

Execute a complete Uypocode file:

```
uypo run program.upc
```

**Output:**
- Standard output from Emit operations
- Exit code: 0 = success, 1 = standard stalls, 2 = error
- **Productive Stalls do not affect exit code** (they are not failures)
- Stall report with Mode information if any pending

---

### 5.93 Library Mode

Embed Interpreter in other systems (e.g., Python):

```python
from uypocode import Interpreter

interp = Interpreter()
interp.load("definitions.upc")

# Execute expression
result = interp.eval("Fido.Sound")
print(result)  # "Bark"

# Check if label is Structure or Instance
print(interp.is_structure("Dog"))   # True
print(interp.is_structure("Fido"))  # False

# Get Mode
print(interp.get_mode("Dog"))  # "Strict"

# Create Instance
fido = interp.create_instance("Dog", Name="Fido")

# v0.4: Snapshot operations
snap = interp.snapshot("Fido", tag="initial")
interp.restore("Fido", snap)

# v0.4: Evolution
interp.evolve("Dog", "1.4.2", {"Temperament": "Loyal"})
print(interp.get_version("Dog"))  # 2
print(interp.get_lineage("Dog"))  # [1.4.1, 1.4.2]

# v0.4: Dictionary loading
interp.load_dictionary("Life")

# v0.4: Productive Stalls
for ps in interp.productive_stalls():
    print(f"Productive: {ps.expression} — {ps.reason}")

# Check stalls with Mode info
for stall in interp.pending_stalls():
    print(f"Stalled: {stall.expression} (Mode: {stall.mode})")

# Export dictionary
interp.save("output.upc")
```

---

### 5.94 LLM Integration

For AI collaboration, the Interpreter exposes:

```
Structure LLMInterface @ 5.94 {
    LLMInterface := AI_Collaboration
    LLMInterface : Mode = Strict
}
```

**Query the Dictionary:**
```
LLM: "What properties does Dog have?"
Interpreter: Query Dog.Metadata (latest version)
Response: {Sound: "Bark", Legs: 4, Temperament: "Loyal", Mode: Strict, Version: 2}
```

**Check Mode before suggesting inference:**
```
LLM: "What does Fido.Bark mean?"
Interpreter: Fido.Prototype = Dog V2, Dog.Mode = Strict
Response: "Inference blocked. Dog has Mode = Strict.
          Either add explicit 'Bark' property or change Mode."
```

**Propose Evolution (v0.4):**
```
LLM: "Add a Color property to Dog"
Interpreter: Dog is a Structure (immutable)
Response: "Cannot modify Structure. Options:
          1. Evolve: Dog.Evolve @ 1.4.3 { Dog : Color = 'Brown' }
          2. Add to Instance: Fido : Color = 'Brown'"
```

**Productive Stall awareness (v0.4):**
```
LLM: "Can you resolve AI.Is.Conscious?"
Interpreter: AI.Is.Conscious is a PRODUCTIVE_STALL
Response: "This is intentionally unresolvable: 'No empirical test can
          distinguish genuine phenomenal experience from functional 
          equivalence.' This stall is productive because it prevents 
          premature closure on AI moral status."
```

---

## 5.99 Section 5.0 Summary

| Address | Label | Description | Since |
|---------|-------|-------------|-------|
| 5.0 | Interpreter | Execution engine | v0.2 |
| 5.1 | Pipeline | Eight-phase execution | v0.2 (extended v0.3, v0.4) |
| 5.11 | Tokenization | Lexical analysis | v0.2 |
| 5.112 | Dictionary Loading | Dictionary import and validation | v0.4 |
| 5.115 | Structure Registration | Structure validation | v0.3 |
| 5.116 | Evolution Registration | Lineage building | v0.4 |
| 5.12 | Indexing | Symbol table construction | v0.2 |
| 5.13 | Definition | Content population | v0.2 |
| 5.14 | Resolution | Expression execution | v0.2 |
| 5.15 | Finalization | Cleanup and reporting | v0.2 |
| 5.3 | Resolution Algorithm | Dot evaluation | v0.2 (extended v0.3, v0.4) |
| 5.4 | Stall Handling | Pending expressions (Standard + Productive) | v0.2 (extended v0.4) |
| 5.5 | Context Management | State tracking | v0.2 |
| 5.6 | Semantic Inference | Mode-controlled NLP resolution | v0.2 |
| 5.7 | Execution Model | Runtime behavior | v0.2 |
| 5.8 | Error Handling | Exception management | v0.2 (extended v0.4) |
| 5.9 | Interface | External API | v0.2 (extended v0.4) |

---

# Appendix A: Complete Address Index

## Section 0.x - Kernel
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 0.0 | Kernel | Strict | v0.2 |
| 0.1 | English | Open | v0.2 |
| 0.2 | Math | Strict | v0.2 |
| 0.3 | Logic | Strict | v0.2 |
| 0.4 | Time | Strict | v0.2 |
| 0.5 | File | Strict | v0.2 |
| 0.6.x | Dictionary Registry | Strict | v0.4 |

## Section 1.x - Objects (Structures)
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 1.0 | Object | Strict | v0.2 |
| 1.01 | Auto-Addressing | — | v0.3 |
| 1.02 | Structure/Instance | — | v0.3 |
| 1.03 | Mode Guard Rails | — | v0.3 |
| 1.04 | Snapshot | — | v0.4 |
| 1.045 | Snapshot (Structure) | Strict | v0.4 |
| 1.05 | Evolution | — | v0.4 |
| 1.055 | Evolution (Structure) | Strict | v0.4 |
| 1.06 | Dictionary Protocol | — | v0.4 |
| 1.065 | Dictionary (Structure) | Strict | v0.4 |
| 1.07 | Productive Stall | — | v0.4 |
| 1.075 | Productive_Stall (Structure) | Strict | v0.4 |
| 1.1 | Label | Strict | v0.2 |
| 1.11 | Context | Strict | v0.2 |
| 1.2 | Address | Strict | v0.2 |
| 1.3 | Contents | Strict | v0.2 |
| 1.31 | Value | Strict | v0.2 |
| 1.32 | Reference | Strict | v0.2 |
| 1.33 | List | Strict | v0.2 |
| 1.34 | Logic | Strict | v0.2 |
| 1.35 | Null | Strict | v0.2 |
| 1.4 | Metadata | Strict | v0.2 |
| 1.5 | Number | Strict | v0.2 |
| 1.6 | Text | Strict | v0.2 |
| 1.7 | Boolean | Strict | v0.2 |
| 1.8 | List | Strict | v0.2 |
| 1.9 | Pronoun | Strict | v0.2 |
| 1.91 | It | Strict | v0.2 |
| 1.92 | That | Strict | v0.2 |
| 1.93 | Self | Strict | v0.2 |
| 1.95 | Null | Strict | v0.2 |
| 1.96 | File | Strict | v0.2 |
| 1.97 | Lifecycle | Strict | v0.2 |
| 1.98 | Identity | Strict | v0.2 |

## Section 2.x - Relations (Structures)
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 2.0 | Relation | Guided | v0.2 |
| 2.1 | Dot Operator | Strict | v0.2 |
| 2.11 | Containment | Strict | v0.2 |
| 2.12 | Metadata | Strict | v0.2 |
| 2.13 | Relation Lookup | Strict | v0.2 |
| 2.14 | Grammar | Strict | v0.2 |
| 2.15 | Stall | Strict | v0.2 |
| 2.16 | Mode Check | Strict | v0.3 |
| 2.2 | Relation Structure | Guided | v0.2 |
| 2.21 | Unary | Guided | v0.2 |
| 2.22 | Binary | Guided | v0.2 |
| 2.23 | Chained | Guided | v0.2 |
| 2.3 | Type Constraints | Strict | v0.2 |
| 2.4 | Precedence | Strict | v0.2 |
| 2.5 | Built-in | Strict | v0.2 |
| 2.51 | Number Relations | Strict | v0.2 |
| 2.52 | Text Relations | Strict | v0.2 |
| 2.53 | Boolean Relations | Strict | v0.2 |
| 2.54 | List Relations | Strict | v0.2 |
| 2.6 | User-Defined | Guided | v0.2 |
| 2.7 | Composition | Guided | v0.2 |
| 2.8 | Symmetry/Inverse | Strict | v0.2 |
| 2.9 | Stalled | Strict | v0.2 |

## Section 3.x - Grammar (Structures)
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 3.0 | Grammar | Strict | v0.2 |
| 3.1 | Then | Strict | v0.2 |
| 3.11 | Else | Strict | v0.2 |
| 3.12 | When | Strict | v0.2 |
| 3.2 | Cycle | Strict | v0.2 |
| 3.21 | Item | Strict | v0.2 |
| 3.22 | Times | Strict | v0.2 |
| 3.23 | Index | Strict | v0.2 |
| 3.24 | While | Strict | v0.2 |
| 3.25 | Break | Strict | v0.2 |
| 3.26 | Skip | Strict | v0.2 |
| 3.3 | Emit | Strict | v0.2 |
| 3.31 | Format | Strict | v0.2 |
| 3.4 | Capture | Strict | v0.2 |
| 3.41 | Prompt | Strict | v0.2 |
| 3.5 | As | Strict | v0.2 |
| 3.51 | Into | Strict | v0.2 |
| 3.6 | Return | Strict | v0.2 |
| 3.61 | Parameters | Strict | v0.2 |
| 3.62 | Yield | Strict | v0.2 |
| 3.7 | Try | Strict | v0.2 |
| 3.71 | Must | Strict | v0.2 |
| 3.8 | With | Strict | v0.2 |
| 3.81 | Global | Strict | v0.2 |
| 3.82 | Local | Strict | v0.2 |
| 3.9 | Import | Strict | v0.2 |
| 3.91 | Export | Strict | v0.2 |

## Section 4.x - Workspace (Runtime Instances)
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 4.0 | Workspace | Strict | v0.2 |
| 4.1 | Global | Strict | v0.2 |
| 4.11 | Address Allocation | Strict | v0.2 |
| 4.12 | Persistence | Strict | v0.2 |
| 4.2 | Local | Strict | v0.2 |
| 4.21 | Scope Boundaries | Strict | v0.2 |
| 4.22 | Stack Behavior | Strict | v0.2 |
| 4.23 | Shadowing | Strict | v0.2 |
| 4.3 | Context | Strict | v0.2 |
| 4.31 | Pronouns | Strict | v0.2 |
| 4.32 | Call Stack | Strict | v0.2 |
| 4.4 | Instances | Strict | v0.3 |
| 4.41 | Identity | Strict | v0.3 |
| 4.42 | Hierarchy | Strict | v0.3 |
| 4.43 | Type Checking | Strict | v0.3 |
| 4.5 | References | Strict | v0.2 |
| 4.51 | DeepCopy | Strict | v0.2 |
| 4.6 | GarbageCollector | Strict | v0.2 |
| 4.61 | Limits | Strict | v0.2 |
| 4.7 | State | Strict | v0.2 |
| 4.71 | Branches | Strict | v0.2 |
| 4.8 | Snapshots | Strict | v0.4 |

## Section 5.x - Interpreter (Structures)
| Address | Label | Mode | Since |
|---------|-------|------|-------|
| 5.0 | Interpreter | Strict | v0.2 |
| 5.1 | Pipeline | Strict | v0.2 |
| 5.11 | Tokenization | Strict | v0.2 |
| 5.112 | Dictionary Loading | Strict | v0.4 |
| 5.115 | Structure Registration | Strict | v0.3 |
| 5.116 | Evolution Registration | Strict | v0.4 |
| 5.12 | Indexing | Strict | v0.2 |
| 5.13 | Definition | Strict | v0.2 |
| 5.14 | Resolution | Strict | v0.2 |
| 5.15 | Finalization | Strict | v0.2 |
| 5.2 | Parsing | Strict | v0.2 |
| 5.3 | Resolution Algorithm | Strict | v0.2 |
| 5.4 | Stall Handling | Strict | v0.2 |
| 5.5 | Context Management | Strict | v0.2 |
| 5.6 | Semantic Inference | Strict | v0.2 |
| 5.7 | Execution Model | Strict | v0.2 |
| 5.8 | Error Handling | Strict | v0.2 |
| 5.9 | Interface | Strict | v0.2 |
| 5.91 | REPL | Strict | v0.2 |
| 5.92 | Batch | Strict | v0.2 |
| 5.93 | Library | Strict | v0.2 |
| 5.94 | LLM Integration | Strict | v0.2 |

---

# Appendix B: Quick Reference

## Operators (v0.4)

| Operator | Name | Usage | Since |
|----------|------|-------|-------|
| `:=` | Assignment | `Label := Contents` | v0.2 |
| `:` | Definition | `Subject : Predicate` | v0.2 |
| `.` | Dot | `Subject.Accessor` | v0.2 |
| `=` | Equivalence/Set | `A = B` | v0.2 |
| `@` | Address Override | `Label @ Address` | v0.3 |
| `()` | Grouping | `(Expression)` | v0.2 |
| `[]` | List | `[A, B, C]` | v0.2 |
| `{}` | Logic Block / Structure Body | `{Statements}` | v0.2 |
| `//` | Comment | `// This is ignored` | v0.2 |
| `->` | Reference | `-> Target` | v0.2 |

## Keywords (v0.4)

| Keyword | Purpose | Since |
|---------|---------|-------|
| `Structure` | Declare immutable prototype | v0.3 |
| `Scope` | Auto-address assignment block | v0.3 |
| `Mode` | Inference control metadata | v0.3 |
| `Strict` | Forbid semantic inference | v0.3 |
| `Guided` | Pattern-constrained inference | v0.3 |
| `Open` | Allow full inference | v0.3 |
| `.New` | Create Instance from Structure | v0.3 |
| `.Is` | Check prototype inheritance | v0.3 |
| `.Prototype` | Get Structure reference | v0.3 |
| `.Identical` | Check address equality | v0.3 |
| **`Snapshot`** | Capture immutable state image | v0.4 |
| **`Evolve`** | Create versioned Structure successor | v0.4 |
| **`Dictionary`** | Declare domain dictionary | v0.4 |
| **`PRODUCTIVE_STALL`** | Declare intentionally permanent stall | v0.4 |
| **`.Diff`** | Compare two Snapshots | v0.4 |
| **`.Restore`** | Revert Instance to Snapshot state | v0.4 |
| **`.Migrate`** | Upgrade Instance to newer Prototype version | v0.4 |
| **`.Lineage`** | Get all versions of a Structure | v0.4 |
| **`.Origin`** | Get first version of a Structure | v0.4 |
| **`.Current`** | Get latest version of a Structure | v0.4 |
| **`.V1`, `.V2`** | Access specific version | v0.4 |

## Primitives

| Type | Examples |
|------|----------|
| Number | `42`, `3.14`, `-7` |
| Text | `"Hello"`, `""` |
| Boolean | `True`, `False` |
| List | `[1, 2, 3]`, `[]` |
| Null | `Null` |
| Mode | `Strict`, `Guided`, `Open` |
| **PRODUCTIVE_STALL** | `PRODUCTIVE_STALL.(...)` |

## Pronouns

| Pronoun | Resolves To |
|---------|-------------|
| `It` | Previous Subject |
| `That` | Previous Result |
| `Self` | Current Object |
| `Item` | Current Cycle Element |
| `Index` | Current Cycle Index |

## Control Flow

| Operation | Syntax |
|-----------|--------|
| Conditional | `Condition.Then.Expression` |
| Alternative | `Condition.Then.A.Else.B` |
| Pattern Match | `Subject.When.[Pattern : Result, ...]` |
| Iteration | `Collection.Cycle.Operation` |
| Counted Loop | `Number.Times.Operation` |
| While Loop | `Condition.While.Operation` |
| Loop Exit | `Condition.Then.Break` |
| Skip Iteration | `Condition.Then.Skip` |

## I/O

| Operation | Syntax |
|-----------|--------|
| Output | `Subject.Emit` |
| Formatted Output | `Template.Format.Values` |
| Input | `Capture.Target` |
| Prompted Input | `Message.Prompt.Target` |

## Functions

| Operation | Syntax |
|-----------|--------|
| Define | `Label.Return.{Logic}` |
| With Parameters | `Label.Return.(Params).{Logic}` |
| Early Return | `Value.Yield` |
| Aliasing | `Subject.As.NewLabel` |
| Assignment | `Value.Into.Target` |

## Error Handling

| Operation | Syntax |
|-----------|--------|
| Try | `Expression.Try.Fallback` |
| Must | `Expression.Must.ErrorMessage` |

## Structure vs Instance (v0.3)

| Aspect | Structure | Instance |
|--------|-----------|----------|
| Location | 0.x - 3.x, 6.x+ | 4.x |
| Mutability | Immutable | Mutable |
| Creation | `Structure Label @ Addr {}` | `Structure.New` |
| Purpose | Template/Prototype | Runtime Object |
| Mode | Defined on Structure | Inherited from Prototype |

## Snapshot Operations (v0.4)

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Capture | `Target.Snapshot` | Immutable state image |
| Named Capture | `Target.Snapshot.As.Label` | Capture with Label |
| Tagged Capture | `Target.Snapshot.(Tag = "v1")` | Capture with annotation |
| Diff | `SnapA.Diff.SnapB` | Compare two Snapshots |
| Restore | `Target.Restore.Snap` | Revert to Snapshot |
| History | `Target.Snapshots` | All Snapshots of Target |

## Evolution Operations (v0.4)

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Evolve | `Struct.Evolve @ Addr { ... }` | Create versioned successor |
| Version | `Struct.V1`, `Struct.V2` | Access specific version |
| Origin | `Struct.Origin` | First version |
| Current | `Struct.Current` | Latest version |
| Lineage | `Struct.Lineage` | All versions as List |
| Migrate | `Instance.Migrate.Struct.V2` | Upgrade Instance prototype |

## Dictionary Operations (v0.4)

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Import | `Import.Dictionary.Name` | Load domain dictionary |
| Versioned Import | `Import.Dictionary.Name.V1` | Load specific version |
| Selective Import | `Import.Dictionary.Name.Only.[A, B]` | Partial import |
| Aliased Import | `Import.Dictionary.Name.As.Alias` | Import with alias |

---

# Appendix C: Amendment Summary

## Amendment A: Auto-Addressing Syntax (v0.3)

**Purpose:** Eliminate manual address assignment tedium.

**Syntax:**
```
Scope(Parent_Address) {
    Label1,              // Auto: Parent_Address.1
    Label2,              // Auto: Parent_Address.2
    Label3 @ Explicit,   // Override: Explicit address
    Label4               // Auto: continues from last
}
```

**Rules:**
- Sequential assignment within Scope
- `@` overrides auto-assignment
- True decimal addressing (1.11 between 1.1 and 1.2)
- Nested Scopes supported

---

## Amendment B: Structure/Instance Formalization (v0.3)

**Purpose:** Prevent "conceptual contamination" where modifying a definition corrupts derived instances.

**Syntax:**
```
// Structure (immutable prototype)
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
}

// Instance (mutable runtime object)
Fido := Dog.New
Fido.Sound = "Woof"    // OK

Dog.Sound = "Woof"     // STALL: Cannot modify Structure
```

**Rules:**
- Structures live in 0.x-3.x (and 6.x+ for Dictionaries), are immutable
- Instances live in 4.x, are mutable
- `.New` creates Instance from Structure
- Instances have: Prototype, Instance_ID, Created_At

---

## Amendment C: Semantic Inference Guard Rails (v0.3)

**Purpose:** Control when NLP inference can override explicit specifications.

**Modes:**

| Mode | Behavior |
|------|----------|
| `Strict` | No inference - stall immediately |
| `Guided` | Pattern-constrained inference |
| `Open` | Full inference permitted |

**Mode Inheritance:** Children inherit parent's Mode unless overridden.

---

## Amendment D: Structure Snapshot (v0.4)

**Purpose:** Enable immutable, timestamped state capture of any Object for rollback, comparison, audit, and Evolution tracking.

**Syntax:**
```
Target.Snapshot                       // Capture
Target.Snapshot.As.Label              // Named capture
SnapshotA.Diff.SnapshotB             // Compare
Target.Restore.Snapshot               // Revert Instance
```

**Rules:**
- Snapshots are always immutable
- Snapshots are first-class Objects with their own addresses
- Snapshot.Restore only works on Instances
- Evolution automatically creates pre-evolution Snapshots

---

## Amendment E: Evolution (v0.4)

**Purpose:** Enable structured, versioned mutation of Structures while preserving lineage and immutability of originals.

**Syntax:**
```
OldStructure.Evolve @ NewAddress {
    Label := NewContents
    Label : NewMetadata = NewValue
}
```

**Rules:**
- Original Structure remains immutable; successor created at new address
- Label resolves to latest version by default
- Explicit version access: `Label.V1`, `Label.V2`
- Existing Instances retain original Prototype; migration is explicit
- No branching lineage (one Successor per Structure)

---

## Amendment F: Dictionary Protocol (v0.4)

**Purpose:** Standardize how domain dictionaries extend the Kernel, declare dependencies, claim address ranges, and export interfaces.

**Syntax:**
```
Dictionary Name @ 0.6.N {
    Name : Version = X.Y
    Name : Extends = -> Kernel
    Name : Depends = [-> OtherDict, ...]
    Name : Claims = [Start, End]
    Name : Exports = [Label1, Label2, ...]
}

Import.Dictionary.Name
```

**Rules:**
- Address ranges must not overlap between Dictionaries
- Dependencies are resolved recursively (circular → Stall)
- Versioned imports supported
- Selective and aliased imports supported

---

## Amendment G: Productive Stall (v0.4)

**Purpose:** Distinguish genuinely unresolvable questions from temporary failures, giving permanent open questions first-class semantic status.

**Syntax:**
```
Expression := PRODUCTIVE_STALL.(
    Domain = "...",
    Reason = "...",
    Productive_Because = "..."
)
```

**Rules:**
- Productive Stalls are never retried by the Interpreter
- Productive Stalls propagate through dot chains permanently
- Try does not catch Productive Stalls
- Must on Productive Stalls halts with diagnostic
- Productive Stalls are reported separately in Finalization
- Productive Stalls do not affect batch exit codes

---

# Appendix D: Example Program (v0.4)

```
// Uypocode v0.4 Example: Evolving Pet Management System

// Import required modules
Import.Math
Import.Logic

// === STRUCTURES (v0.3 syntax, unchanged) ===

Structure Pet @ 1.1 {
    Pet := Animal
    Pet : Name = Null
    Pet : Age = Null
    Pet : Species = Null
    Pet : Mode = Guided
    Pet : Inference_Pattern = "Subject.Feel.*"
}

Structure Dog @ 1.1.1 {
    Dog := Pet
    Dog : Species = "Canine"
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}

// === EVOLUTION (v0.4) ===

// Dog gains a Temperament property
Dog.Evolve @ 1.1.11 {
    Dog : Temperament = "Loyal"
    Dog : Reason = "Behavioral modeling expansion"
}

// Dog.V1 is at 1.1.1 (Sound = "Bark", no Temperament)
// Dog.V2 is at 1.1.11 (Sound = "Bark", Temperament = "Loyal")
// Dog now resolves to V2

// === RELATIONS with auto-addressing ===

Scope(2.0) {
    Structure Speak {
        Speak := {Subject.Sound.Emit}
        Speak : Unary
        Speak : Mode = Strict
    },
    
    Structure Describe {
        Describe := {
            "Name: ".Join.Subject.Name.Emit.
            "Age: ".Join.Subject.Age.Emit.
            "Species: ".Join.Subject.Species.Emit
        }
        Describe : Unary
        Describe : Mode = Strict
    },

    Structure Birthday {
        Birthday := {
            Subject.Age.Add.1.Into.Subject.Age.
            "Happy Birthday, ".Join.Subject.Name.Join."!".Emit
        }
        Birthday : Unary
        Birthday : Mode = Strict
    }
}

// === INSTANCES ===

Fido := Dog.New.(Name = "Fido", Age = 3)
// Fido.Prototype = Dog V2 (latest)
// Fido.Temperament = "Loyal"

// === SNAPSHOTS (v0.4) ===

Fido_Young := Fido.Snapshot.(Tag = "puppyhood")

"=== Pet Info ===".Emit
Fido.Describe
// Output: Name: Fido
// Output: Age: 3
// Output: Species: Canine

"=== Birthday ===".Emit
Fido.Birthday
// Output: Happy Birthday, Fido!
// Fido.Age = 4

"=== Snapshot Diff ===".Emit
Fido_Young.Diff.Fido.Snapshot
// Returns: {Age: {Was: 3, Now: 4}}

"=== Restore ===".Emit
Fido.Restore.Fido_Young
Fido.Age.Emit
// Output: 3 (restored)

// === PRODUCTIVE STALL (v0.4) ===

Pet_Consciousness := PRODUCTIVE_STALL.(
    Domain = "Animal_Cognition",
    Reason = "Whether pets have subjective experience is empirically underdetermined",
    Productive_Because = "Encourages empathetic treatment without false certainty"
)

Pet_Consciousness.Is.Productive_Stall.Emit
// Output: True

// === VERSION CHECKING (v0.4) ===

"=== Evolution History ===".Emit
Dog.Lineage.Length.Emit
// Output: 2

Dog.V1.Sound.Emit
// Output: Bark

Dog.V2.Temperament.Emit
// Output: Loyal

// Old-style Dog (V1) Instance:
OldDog := Dog.V1.New.(Name = "Rex", Age = 7)
OldDog.Temperament.Try."N/A".Emit
// Output: N/A (Temperament not in V1)

// Migrate to V2:
OldDog.Migrate.Dog.V2
OldDog.Temperament.Emit
// Output: Loyal (now has V2 properties)
```

---

# Appendix E: Migration Guide (v0.3 → v0.4)

## Syntax Additions

| v0.3 | v0.4 |
|------|------|
| No Snapshot syntax | `Target.Snapshot`, `Target.Restore.Snap` |
| Structures fully immutable, no change mechanism | `Structure.Evolve @ Addr { ... }` |
| No Dictionary protocol | `Dictionary Name @ 0.6.N { ... }` |
| Informal STALL for open questions | `PRODUCTIVE_STALL.(Domain, Reason, ...)` |
| `Workspace.State.Capture` only | `AnyObject.Snapshot` (fine-grained) |

## Behavioral Changes

1. **Label resolution after Evolution**: When a Structure evolves, the bare Label resolves to the latest version. Use `.V1`, `.V2` for explicit version access.
2. **Try transparency to Productive Stalls**: Try blocks do not catch Productive Stalls; they propagate permanently.
3. **Must on Productive Stalls**: Halts with a diagnostic message, not a generic failure.
4. **Finalization Report expanded**: Now includes separate Productive Stall report, Evolution log, Snapshot count, and loaded Dictionaries.
5. **Pipeline extended**: Two new phases (Dictionary Loading, Evolution Registration) execute before Indexing.
6. **Reserved keywords expanded**: `Snapshot`, `Evolve`, `Dictionary`, `PRODUCTIVE_STALL` added.
7. **Address space extended**: Section 6.x+ formally reserved for domain Dictionaries.

## Backward Compatibility

- All v0.3 programs run unchanged on v0.4
- Structures without Evolution have no Predecessor/Successor metadata
- Objects without Snapshots behave identically to v0.3
- The absence of Dictionary declarations falls back to direct address usage (existing dictionaries work as-is)
- Standard stalls behave identically to v0.3; only explicitly declared `PRODUCTIVE_STALL` expressions receive Productive treatment
- Existing domain dictionaries may adopt Amendment F (Dictionary Protocol) incrementally

---

**End of Uypocode Master Dictionary v0.4**

---

# Changelog

## v0.4 (Current)

### Added
- **Amendment D: Structure Snapshot**
  - `Target.Snapshot` operation for immutable state capture
  - `Target.Snapshot.As.Label` for named captures
  - `Target.Snapshot.(Tag = "...")` for annotated captures
  - `SnapshotA.Diff.SnapshotB` for state comparison
  - `Target.Restore.Snapshot` for Instance restoration
  - `Target.Snapshots` for Snapshot history
  - Snapshot Structure at 1.045 with Source, Captured_At, Tag, State, Lineage

- **Amendment E: Evolution**
  - `Structure.Evolve @ NewAddress { ... }` for versioned Structure mutation
  - Automatic Snapshot of predecessor before Evolution
  - Label resolution to latest version by default
  - `.V1`, `.V2`, `.Origin`, `.Current`, `.Lineage` version access
  - `Instance.Migrate.Structure.VN` for explicit Instance upgrade
  - Evolution Structure at 1.055 with Predecessor, Successor, Version, Changes
  - No branching lineage (one Successor per Structure)

- **Amendment F: Dictionary Protocol**
  - `Dictionary` as first-class Object at 1.065
  - Standardized metadata: Name, Version, Extends, Depends, Claims, Exports
  - `Import.Dictionary.Name` for domain dictionary loading
  - Versioned imports: `Import.Dictionary.Name.V1`
  - Selective imports: `Import.Dictionary.Name.Only.[A, B]`
  - Aliased imports: `Import.Dictionary.Name.As.Alias`
  - Address range claiming and conflict detection
  - Recursive dependency resolution (circular → Stall)
  - Kernel Extension Protocol standardization (0.0.N sub-addresses)

- **Amendment G: Productive Stall**
  - `PRODUCTIVE_STALL` as formal variant of Stall at 1.075
  - Metadata: Domain, Reason, Implications, Productive_Because
  - Productive Stall Registry (separate from Pending list)
  - Never retried by Interpreter
  - Transparent to Try (not caught)
  - Must on Productive Stall halts with diagnostic
  - Separate Productive Stall Report in Finalization
  - Does not affect batch exit codes

### Changed
- Interpretation pipeline: 6 phases → 8 phases (added Dictionary Loading, Evolution Registration)
- Resolution algorithm: Added Productive Stall check (step 1), Version resolution (step 3), Snapshot operations (step 4)
- Finalization report: Now includes Productive Stall report, Evolution log, Snapshot count, Dictionary list
- Reserved keywords expanded: `Snapshot`, `Evolve`, `Dictionary`, `PRODUCTIVE_STALL`
- Reserved metadata keys expanded: Predecessor, Successor, Version, Stall_Type, Dictionary
- Error types expanded: EvolutionError, DictionaryError, SnapshotError
- Address space formally extended: 6.x+ reserved for domain Dictionaries
- REPL commands expanded: `:snapshots`, `:evolutions`, `:dictionaries`, `:productive`
- Library Mode API extended: snapshot(), restore(), evolve(), load_dictionary(), productive_stalls()

### Unchanged
- All v0.3 syntax and behavior preserved
- Resolution order priorities 5-11 (was 1-7) maintain same semantics
- Structure/Instance distinction unchanged
- Mode (Strict/Guided/Open) semantics unchanged
- All Grammar operations unchanged
- Workspace behavior unchanged

## v0.3

### Added
- **Amendment A: Auto-Addressing Syntax**
  - `Scope(Address) { ... }` construct for automatic address assignment
  - `@` operator for explicit address override within Scope
  - Nested Scope support

- **Amendment B: Structure/Instance Formalization**
  - `Structure` keyword for immutable prototype declarations
  - Clear separation: Structures in 0-3.x, Instances in 4.x
  - `.New` operation for Instance creation
  - `.Is`, `.Prototype`, `.Identical` type-checking operations
  - Automatic Instance metadata: Prototype, Instance_ID, Created_At

- **Amendment C: Semantic Inference Guard Rails**
  - `Mode` metadata with values: Strict, Guided, Open
  - `Inference_Pattern` for Guided mode constraints
  - Mode inheritance from parent to children
  - Mode check in resolution algorithm (step 6)

### Changed
- Interpretation pipeline: 5 phases → 6 phases (added Structure Registration)
- Resolution algorithm: Added Structure mutation check and Mode check
- Stall records now include Mode information
- Error types expanded: StructureError, ModeError
- Address index now includes Mode column

### Removed
- Implicit mutability of definition-space Objects

## v0.2

- Initial comprehensive specification
- Five-section architecture (Kernel, Objects, Relations, Grammar, Workspace)
- Interpreter specification with semantic inference
