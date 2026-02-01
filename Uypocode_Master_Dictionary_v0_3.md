# Uypocode Master Dictionary
## Specification v0.3

---

# Changelog from v0.2

**Version 0.3 introduces three major enhancements:**

1. **Auto-Addressing Syntax (Amendment A)**: New `Scope` construct allows the Interpreter to automatically assign sequential decimal addresses within a declared scope, eliminating manual address management.

2. **Structure/Instance Formalization (Amendment B)**: New `Structure` keyword creates immutable prototypes in 1.x that can only be instantiated (not modified) via `.New` in 4.x Workspace. This prevents "conceptual contamination" where modifying a definition corrupts all derived instances.

3. **Semantic Inference Guard Rails (Amendment C)**: New `Mode` metadata controls when and how `Import.English` may infer relationships. `Mode = Strict` forbids semantic inference, `Mode = Guided` allows inference within constraints, and `Mode = Open` (default) allows full inference.

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

**Inference Control (New in v0.3):**
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
- Reserved labels: `It`, `That`, `Null`, `True`, `False`, `Structure`, `Scope`

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
| Key | Purpose |
|-----|---------|
| Mode | Inference control (Strict/Guided/Open) |
| Prototype | Points to source Structure |
| Immutable | Prevents modification |
| Instance_ID | Unique identifier for instances |

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
- Falsy: `Null`, `0`, `""` (empty Text), `[]` (empty List)
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

*Structures:* Cannot be modified (Immutable by definition)

*Instances:* Contents and Metadata may be reassigned in 4.x Workspace:
```
Fido.Legs = 3          // Modify property value
Fido : Friendly        // Add metadata
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

---

## 1.99 Section 1.0 Summary

| Address | Label | Description | Mode |
|---------|-------|-------------|------|
| 1.0 | Object | The atomic unit | Strict |
| 1.1 | Label | Symbolic identifier | Strict |
| 1.11 | Context | Execution state | Strict |
| 1.2 | Address | Dictionary location | Strict |
| 1.3 | Contents | Held value/reference/logic | Strict |
| 1.4 | Metadata | Assertions about Object | Strict |
| 1.5 | Number | Numeric primitive | Strict |
| 1.6 | Text | String primitive | Strict |
| 1.7 | Boolean | Truth value primitive | Strict |
| 1.8 | List | Ordered collection | Strict |
| 1.9 | Pronoun | Dynamic context reference | Strict |
| 1.95 | Null | Absence of value | Strict |
| 1.96 | File | External resource | Strict |
| 1.97 | Lifecycle | Creation, modification, deletion | — |
| 1.98 | Identity | Sameness and equivalence | — |

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

**Resolution Order (Updated for v0.3):**

| Priority | Check | Question Asked |
|----------|-------|----------------|
| 1 | Containment | Is B a child of A? (B's address starts with A's address) |
| 2 | Metadata | Is B a property defined on A via `:`? |
| 3 | Relation | Is there a 2.x rule matching A.B? |
| 4 | Grammar | Is B a 3.x operation applicable to A? |
| 5 | **Mode Check** | What is A's Mode? (New in v0.3) |
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

The Interpreter collects stalled expressions. At program end, unresolved stalls are reported.

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

The Interpreter may re-attempt stalled expressions when the Dictionary changes.

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
// Item = 1, 1.Square = 1
// Item = 2, 2.Square = 4
// Item = 3, 3.Square = 9
// Item = 4, 4.Square = 16
// Item = 5, 5.Square = 25
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
        Export := External_Exposure
    }
}
```

**Syntax:**
```
Import.Module
Import.Module.As.Alias
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
// Output: 2025-01-14T12:30:00

Import.File
"data.txt".File.Capture.Contents
Contents.Emit
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

**Section Mutability Summary (v0.3):**

| Section | Purpose | Mutability | Contains |
|---------|---------|------------|----------|
| 0.x | Kernel | Read-only | Structures (imports) |
| 1.x | Objects | Append-only | Structures (definitions) |
| 2.x | Relations | Append-only | Structures (rules) |
| 3.x | Grammar | Read-only | Structures (operations) |
| **4.x** | **Workspace** | **Read-write** | **Instances (runtime)** |

**Key v0.3 Distinction:**
- Sections 0-3 contain **Structures** (immutable prototypes)
- Section 4 contains **Instances** (mutable runtime objects)
- Attempting to modify a Structure stalls; Instances are freely mutable

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
        Scope_Address := Address,          // 4.3.1
        Previous_Subject := Reference,     // 4.3.2
        Previous_Result := Any,            // 4.3.3
        Current_Object := Reference,       // 4.3.4
        Current_Iteration := Any,          // 4.3.5
        Current_Index := Number,           // 4.3.6
        Call_Stack := List                 // 4.3.7
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

**Example of Context flow:**

```
Fido := Dog.New.(Sound = "Bark")

Fido.Sound.Emit
// Step 1: Resolve Fido.Sound
//   Context.Previous_Subject = Fido
//   Context.Previous_Result = "Bark"
// Step 2: Resolve "Bark".Emit
//   Context.Previous_Subject = "Bark"
//   Context.Previous_Result = Null (Emit returns Null)
//   Output: Bark

It.Emit
// It = Context.Previous_Subject = "Bark"
// Output: Bark
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

**Example:**

```
// Structure definition (in 1.x, immutable)
Structure Person @ 1.1 {
    Person := Human
    Person : Name = Null
    Person : Age = Null
    Person : Mode = Guided
}

// Instance creation (in 4.x, mutable)
Alice := Person.New
// Alice at 4.1.x
// Alice : Prototype = -> Person
// Alice : Instance_ID = "uuid-1234"
// Alice : Created_At = Time.Now
// Alice : Name = Null
// Alice : Age = Null

Alice.Name = "Alice"     // OK: Modifying Instance
Alice.Age = 30           // OK: Modifying Instance

// FORBIDDEN:
Person.Name = "Default"  // Stall: Cannot modify Structure
```

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

A.Name = "Alice"
B.Name = "Alice"

A.Name.Eq.B.Name  // True (same value)
A.Identical.B     // Still False (different Objects)
```

**Instance Identity Operations (v0.3):**

| Operation | Meaning |
|-----------|---------|
| A.Identical.B | Same Address (same object) |
| A.Eq.B | Same value (equivalent content) |
| A.Is.Type | A's Prototype chain includes Type |
| A.Prototype | Returns Structure that created A |

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

v0.3 introduces formal type checking for Instances:

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

**Local cleanup:**

```
MyFunc.Return.{
    Temp.As.Local.X
    Temp.As.Local.Y
    X.Add.Y
}
// X and Y garbage collected on exit

MyFunc
// Memory freed
```

**Global cleanup:**

```
A := "Hello"
B := A              // B references A's value
A = Null            // A nullified, but "Hello" still reachable via B
B = Null            // "Hello" now unreachable
// Garbage collector reclaims "Hello"
```

**Explicit deletion:**

```
LargeData := LoadHugeFile
// ... process ...
LargeData.Delete    // Immediately freed
```

**Note:** Structures (0.x-3.x) are never garbage collected — they persist for program lifetime.

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

State captures the entire Workspace at a moment in time.

```
Structure State @ 4.7 {
    State := Workspace_Snapshot
    State : Checkpoint
    State : Immutable = True
    State : Mode = Strict
}
```

**Capture State:**

```
Checkpoint := Workspace.State.Capture
// Checkpoint contains snapshot of all 4.x Instances
```

**Restore State:**

```
Checkpoint.Restore
// Workspace returns to captured state
// All changes since Checkpoint are discarded
```

**Use cases:**
- Transaction rollback
- Speculative execution
- Debugging/replay

**Example:**

```
Account := Account.New.(Balance = 1000)

Checkpoint := Workspace.State.Capture

Account.Balance.Sub.500.Into.Account.Balance
// Balance = 500

TransactionFailed := True

TransactionFailed.Then.Checkpoint.Restore
// Balance restored to 1000

Account.Balance.Emit    // Output: 1000
```

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

**Example:**

```
// Fido.Fly stalls (Dogs can't fly by default)
Fido.Fly.Then."Flying!".Emit

// Interpreter creates Branch:
//   Branch.Pending = Fido.Fly
//   Branch.State = (snapshot)
//   Branch.Continuation = "Flying!".Emit

// Later, if Fido gains Fly capability:
Fido : Fly = True

// Interpreter may revisit Branch
// Fido.Fly now resolves to True
// "Flying!".Emit executes
```

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
└── 4.7 State
    └── 4.71 Branches
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

---

# Section 5.0: Interpreter

The Interpreter is the engine that reads, resolves, and executes Uypocode. It transforms a Dictionary specification into runtime behavior. v0.3 introduces Mode-aware resolution and formal Structure/Instance handling.

```
Structure Interpreter @ 5.0 {
    Interpreter := Execution_Engine
    Interpreter : Parser
    Interpreter : Resolver
    Interpreter : Runtime
    Interpreter : Mode = Strict    // Interpreter internals are not inferrable
}
```

The Interpreter is designed for:
- Graceful handling of incomplete specifications
- **Mode-controlled** semantic inference when explicit rules are absent
- Human-AI collaboration and inspection
- Non-deterministic convergence on optimal resolutions
- **Structure/Instance distinction** enforcement

---

## 5.1 Interpretation Pipeline

The Interpreter operates in **six** sequential phases (v0.3 adds Structure Registration):

```
Structure Pipeline @ 5.1 {
    Pipeline := Execution_Sequence
    Pipeline : Mode = Strict
}
```

| Phase | Name | Purpose |
|-------|------|---------|
| 1 | Tokenization | Break source into tokens |
| 2 | **Structure Registration** | Identify and register Structures (v0.3) |
| 3 | Indexing | Build address tree from declarations |
| 4 | Definition | Populate Contents and Metadata |
| 5 | Resolution | Execute dot-expressions |
| 6 | Finalization | Report stalls, clean up |

```
Source → Tokenize → Register Structures → Index → Define → Resolve → Output
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

**Token Types (v0.3 additions in bold):**

| Type | Pattern | Examples |
|------|---------|----------|
| Label | `[A-Za-z_][A-Za-z0-9_]*` | `Dog`, `my_var`, `_temp` |
| Number | `[0-9]+\.?[0-9]*` | `42`, `3.14`, `0` |
| Text | `"[^"]*"` | `"Hello"`, `""` |
| Operator | `:=`, `:`, `.`, `=`, **`@`** | |
| Grouping | `(`, `)`, `[`, `]`, `{`, `}` | |
| **Keyword** | **`Structure`, `Scope`, `Mode`** | |
| Separator | `,`, newline | |
| Comment | `//` to end of line | `// This is ignored` |

**v0.3 Tokenization Example:**

```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}
```

Tokens:
```
[Keyword:Structure] [Label:Dog] [Op:@] [Number:1.4.1] [Group:{]
[Label:Dog] [Op::=] [Label:Animal] [Newline]
[Label:Dog] [Op::] [Label:Sound] [Op:=] [Text:"Bark"] [Newline]
[Label:Dog] [Op::] [Keyword:Mode] [Op:=] [Label:Strict] [Newline]
[Group:}]
```

---

## 5.115 Phase 2: Structure Registration (v0.3)

The Structure Registrar identifies and validates Structure declarations.

```
Structure StructureRegistrar @ 5.115 {
    StructureRegistrar := Structure_Validator
    StructureRegistrar : Mode = Strict
}
```

**Behavior:**
1. Find all `Structure Label @ Address { ... }` declarations
2. Verify Address is in range 0.x - 3.x
3. Mark Object as immutable Structure
4. Extract Mode metadata if present
5. Register in Structure Table

**Structure Table:**

```
StructureTable := {
    "Dog": {
        Address: 1.4.1,
        Mode: Strict,
        Immutable: True,
        Contents: Animal,
        Metadata: {Sound: "Bark", Mode: Strict}
    },
    "Person": {
        Address: 1.1,
        Mode: Guided,
        Immutable: True,
        ...
    }
}
```

**Validation Rules:**
- Structure keyword requires explicit address via `@`
- Address must be in 0.x, 1.x, 2.x, or 3.x
- Mode must be one of: Strict, Guided, Open
- Duplicate addresses cause ParseError

---

## 5.12 Phase 3: Indexing

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
5. **Process Scope blocks for auto-addressing** (v0.3)

**Symbol Table Structure (v0.3):**

```
SymbolTable := {
    Labels: {
        "Dog": 1.4.1,
        "Animal": 1.1,
        "Speak": 2.1,
        ...
    },
    Addresses: {
        1.1: {Label: "Animal", Children: [1.4.1], IsStructure: True, Mode: Open},
        1.4.1: {Label: "Dog", Children: [], IsStructure: True, Mode: Strict},
        ...
    },
    ScopeCounters: {
        1.4: 2,        // Next auto-address under 1.4 is 1.4.2
        2.0: 5,        // Next auto-address under 2.0 is 2.0.5
        ...
    }
}
```

**Scope Block Processing (Amendment A):**

For the source:
```
Scope(1.9) {
    It := -> Context.Previous_Subject,
    That := -> Context.Previous_Result,
    Self := -> Context.Current_Object
}
```

Auto-assigned addresses:
```
It   → 1.9.1
That → 1.9.2
Self → 1.9.3
```

---

## 5.13 Phase 4: Definition

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
4. **Inherit Mode from parent if not specified** (v0.3)
5. **Validate Instance creation from Structures** (v0.3)

**Definition Pass (v0.3):**

```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Legs = 4
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}
```

After Definition:
```
Address 1.4.1:
    Label: "Dog"
    Contents: -> 1.1 (Reference to Animal)
    Metadata: {
        Legs: 4,
        Sound: "Bark",
        Mode: Strict
    }
    IsStructure: True
    Immutable: True
```

**Mode Inheritance:**

If a child does not specify Mode, it inherits from parent:

```
Structure Parent @ 1.0 {
    Parent := Container
    Parent : Mode = Strict
    
    Scope {
        Child1 := Thing,    // Child1 : Mode = Strict (inherited)
        Child2 := Thing     // Child2 : Mode = Strict (inherited)
    }
}
```

---

## 5.14 Phase 5: Resolution

The Resolver executes dot-expressions.

```
Structure Resolver @ 5.14 {
    Resolver := Expression_Executor
    Resolver : Mode = Strict
}
```

**Behavior:**
1. Find executable expressions (containing `.`)
2. **Check Structure/Instance constraints** (v0.3)
3. Resolve left-to-right
4. **Apply Mode rules before semantic inference** (v0.3)
5. Update Context after each resolution
6. Collect results or stalls

This is the heart of execution. See §5.3 for the resolution algorithm.

---

## 5.15 Phase 6: Finalization

The Finalizer concludes execution.

```
Structure Finalizer @ 5.15 {
    Finalizer := Execution_Closer
    Finalizer : Mode = Strict
}
```

**Behavior:**
1. Check for unresolved stalls
2. Report pending expressions **with Mode information** (v0.3)
3. Run garbage collection
4. Return final result or stall report

**Output Types:**

| Outcome | Description |
|---------|-------------|
| Success | All expressions resolved, final value returned |
| Partial | Some stalls remain, partial results available |
| Stalled | Primary expression could not resolve |

**Stall Report (v0.3):**

```
Finalization Report:
    Status: Partial
    Result: "Hello, world"
    Pending: [
        {
            Expression: "Ghost.Fly",
            Reason: "No Fly property or relation",
            Mode: Strict,
            Inference_Blocked: True
        },
        {
            Expression: "X.Unknown",
            Reason: "Unknown not in Dictionary",
            Mode: Open,
            Inference_Attempted: True,
            Inference_Result: "Low confidence (0.3)"
        }
    ]
    Branches: 2 speculative states saved
```

---

## 5.2 Parsing

The Parser transforms tokens into an Abstract Syntax Tree (AST).

```
Structure Parser @ 5.2 {
    Parser := Syntax_Analyzer
    Parser : Mode = Strict
}
```

### 5.21 Grammar Rules (v0.3)

```
Program        := Statement*
Statement      := StructureDecl | Declaration | Definition | Expression | ScopeBlock | Comment

StructureDecl  := "Structure" Label "@" Address "{" Statement* "}"
ScopeBlock     := "Scope" "(" Address ")" "{" ScopeItem ("," ScopeItem)* "}"
ScopeItem      := Label (":=" Contents)? | Label "@" Address (":=" Contents)?

Declaration    := Label ":=" "(" Label "," Address "," Contents ")"
Definition     := Label ":" Predicate
Expression     := Term ("." Term)*
Term           := Label | Literal | Group | List | Block
Literal        := Number | Text | Boolean | ModeValue
ModeValue      := "Strict" | "Guided" | "Open"
Group          := "(" Expression ")"
List           := "[" (Expression ("," Expression)*)? "]"
Block          := "{" Statement* "}"
Predicate      := Label ("=" Expression)?
```

### 5.22 AST Structure

Each node in the AST has:

```
ASTNode := (Type, Value, Children, Position, Mode)
```

| Field | Description |
|-------|-------------|
| Type | Node type (StructureDecl, Declaration, Expression, etc.) |
| Value | Associated value (Label name, Number, etc.) |
| Children | Child nodes |
| Position | Source location (line, column) for error reporting |
| **Mode** | Inference mode (v0.3) |

**Example AST (v0.3):**

Source:
```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Mode = Strict
}
```

AST:
```
StructureDecl
├── Label: "Dog"
├── Address: 1.4.1
├── Mode: Strict
└── Children:
    ├── Declaration
    │   ├── Label: "Dog"
    │   └── Contents: Label "Animal"
    └── Definition
        ├── Subject: "Dog"
        └── Predicate: Mode = Strict
```

---

## 5.23 Parsing Errors

Syntax errors halt parsing with diagnostic information:

```
Structure ParseError @ 5.23 {
    ParseError := Syntax_Failure
    ParseError : Position
    ParseError : Expected
    ParseError : Found
    ParseError : Mode = Strict
}
```

**v0.3 Error Examples:**

```
Structure Dog @ 4.1.1 { ... }
// Error: Structure address must be in 0.x-3.x, not 4.x (Workspace)

Dog : Mode = Fast
// Error: Invalid Mode value. Expected: Strict, Guided, or Open
```

---

## 5.3 Resolution Algorithm

The core algorithm for evaluating `A.B` expressions. **v0.3 adds Mode checking.**

```
Structure ResolutionAlgorithm @ 5.3 {
    ResolutionAlgorithm := Dot_Evaluator
    ResolutionAlgorithm : Mode = Strict
}
```

### 5.31 Resolution Steps (v0.3)

```
Function: Resolve(Subject, Accessor)
Input: Subject (Object), Accessor (Label or Literal)
Output: Result (Object) or Stall

1. STRUCTURE MUTATION CHECK (v0.3)
   If Subject.IsStructure AND operation would mutate:
       Return Stall("Cannot modify Structure")
   
2. CONTAINMENT CHECK
   If Accessor is a child of Subject (address prefix match):
       Return child Object
   
3. METADATA CHECK
   If Accessor exists in Subject's Metadata:
       Return Metadata value
   
4. RELATION CHECK
   Search 2.x for matching pattern:
       - Exact: Subject.Type.Accessor
       - Generic: Any.Accessor
   If found:
       Substitute Subject into Relation Logic
       Recursively resolve Logic
       Return result
   
5. GRAMMAR CHECK
   If Accessor is a 3.x Grammar operation:
       Apply operation to Subject
       Return result
   
6. MODE CHECK (v0.3 - Amendment C)
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

7. SEMANTIC CHECK (if NLP enabled and Mode permits)
   Query NLP: "What is the relationship between {Subject.Label} and {Accessor}?"
   If confident answer:
       Create temporary Relation
       Recursively resolve
       Return result
   
8. STALL
   Record pending expression with Mode info
   Return Stall marker
```

---

### 5.32 Chained Resolution

For expressions like `A.B.C.D`:

```
Function: ResolveChain(Expression)
Input: DotChain [A, B, C, D]
Output: Final Result or Stall

1. Set Current = Resolve first term (A)
2. For each remaining term T in [B, C, D]:
       Current = Resolve(Current, T)
       If Current is Stall:
           Return Stall with partial chain info and Mode
3. Return Current
```

**Example:**

```
Person.Pet.Sound.Emit

Step 1: Current = Person (lookup)
Step 2: Current = Resolve(Person, Pet) = Fido (metadata)
Step 3: Current = Resolve(Fido, Sound) = "Bark" (metadata)
Step 4: Current = Resolve("Bark", Emit) = Output "Bark" (grammar)
Result: Null (Emit returns Null after output)
```

---

### 5.33 Argument Handling

Binary operations (three-term patterns):

```
A.Op.B
```

The Resolver detects when `Op` is a Relation or Grammar expecting an Argument:

```
Function: ResolveBinary(Subject, Operator, Argument)

1. Resolve Subject
2. Lookup Operator in Relations (2.x) or Grammar (3.x)
3. Check Operator's Mode before proceeding (v0.3)
4. If Operator expects Argument:
       Resolve Argument
       Apply Operator(Subject, Argument)
       Return result
5. If Operator is unary:
       Apply Operator(Subject)
       Treat Argument as next chain element
       Return Resolve(result, Argument)
```

---

### 5.34 Grouping Resolution

Parentheses force evaluation order:

```
(A.B).C     // Resolve A.B first, then apply C
A.(B.C)     // Resolve B.C first, then A.result
```

---

### 5.35 Structure Mutation Prevention (v0.3)

The Resolver enforces immutability of Structures:

```
Function: CheckMutation(Subject, Operation)

If Subject.IsStructure:
    If Operation in [Into, Delete, =, Add, Remove]:
        Return Stall("Cannot modify Structure: use Instance instead")
        
    // Suggest fix
    Suggestion := "Create instance with: " + Subject.Label + ".New"
    Stall.Suggestion = Suggestion
```

**Example:**

```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
}

Dog.Sound = "Woof"
// Stalls: Cannot modify Structure
// Suggestion: Create instance with: Dog.New

Fido := Dog.New
Fido.Sound = "Woof"
// OK: Fido is an Instance, can be modified
```

---

## 5.4 Stall Handling

When resolution fails, expressions stall rather than error.

```
Structure Stall @ 5.4 {
    Stall := Pending_Expression
    Stall : Expression
    Stall : Reason
    Stall : Mode          // v0.3: Subject's Mode
    Stall : Context_Snapshot
    Stall : Retry_Conditions
    Stall : Mode_Setting = Strict
}
```

### 5.41 Stall Creation (v0.3)

```
Function: CreateStall(Expression, Reason, SubjectMode)

1. Capture current Context
2. Record Expression that failed
3. Record Subject's Mode (v0.3)
4. Determine retry conditions:
       - Missing Object: retry when Object created
       - Missing Property: retry when Property added
       - Type mismatch: retry when type changes
       - Mode blocked: retry if Mode changed (unlikely for Structures)
5. Add to Pending list
6. Return Stall marker
```

**Stall Record (v0.3):**

```
{
    ID: "stall_001",
    Expression: "Ghost.Fly",
    Reason: "No property 'Fly' on Ghost",
    Mode: Strict,
    Inference_Blocked: True,
    Context: {Scope: 4.1, Previous_Subject: Dog, ...},
    RetryWhen: ["Ghost.Fly defined"],
    CreatedAt: 1705234567
}
```

---

### 5.42 Stall Propagation

Stalls propagate through chains:

```
A.B.C.D
    ^
    B stalls
```

When B stalls:
1. Record stall for A.B with Mode information
2. Entire chain A.B.C.D stalls
3. Store C.D as continuation
4. If A.B later resolves, continuation executes

---

### 5.43 Stall Resolution

Stalls may resolve when the Dictionary changes:

```
Function: CheckStalls()
Trigger: After any Dictionary modification

1. For each Stall in Pending:
       // Skip if Mode prevented inference and still prevents
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

**Note:** This is the Interpreter's stall-handling mode, distinct from the Object Mode (Strict/Guided/Open) that controls semantic inference.

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

### 5.52 Scope Transitions

When entering/exiting scopes, Context adjusts:

**Function entry:**
```
MyFunc.Return.(A, B).{...}

MyFunc.(1, 2)

// Before call:
Context.Scope_Address = 4.1
Context.Call_Stack = []

// During call:
Context.Scope_Address = 4.2.1 (new Local frame)
Context.Call_Stack = [MyFunc]
// A and B exist at 4.2.1.x as Instances

// After return:
Context.Scope_Address = 4.1
Context.Call_Stack = []
// A and B garbage collected
```

---

## 5.6 Semantic Inference (Mode-Controlled)

When explicit resolution fails, the Interpreter may use semantic inference **if Mode permits** (Amendment C).

```
Structure SemanticEngine @ 5.6 {
    SemanticEngine := NLP_Resolver
    SemanticEngine : Optional = True
    SemanticEngine : Requires = Import.English
    SemanticEngine : Mode = Strict    // Engine itself is strict
}
```

### 5.61 Inference Trigger (v0.3)

Semantic inference activates when:
1. All explicit resolution steps fail
2. `Import.English` is loaded
3. Subject and Accessor are meaningful Labels
4. **Subject's Mode permits inference** (v0.3)

```
Function: SemanticResolve(Subject, Accessor)

1. CHECK MODE (v0.3)
   Subject.Mode.When.[
       Strict : Return Null,    // Inference forbidden
       Guided : {
           Pattern := Subject.Inference_Pattern.
           If Pattern exists AND Accessor matches Pattern:
               Continue to step 2
           Else:
               Return Null    // Pattern mismatch
       },
       Open : Continue to step 2    // Inference permitted
   ]

2. If Import.English not loaded:
       Return Null (cannot infer)

3. Query: "In English, what is the relationship between 
          '{Subject.Label}' and '{Accessor}'?"

4. If NLP returns confident relationship:
       Type = Infer relationship type
       Create temporary Relation at 2.x
       Resolve using new Relation
       Return result

5. If NLP uncertain:
       Return Null (stall)
```

---

### 5.62 Inference Examples (v0.3)

**Example 1: Strict Mode blocks inference**

```
Structure Dog @ 1.4.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}

Fido := Dog.New

Fido.Bark
// Step 1-5: No explicit resolution
// Step 6: Check Mode → Strict → Inference blocked
// Result: Stall("No Bark property; inference blocked by Strict mode")
```

**Example 2: Open Mode allows inference**

```
Structure Animal @ 1.1 {
    Animal := Living_Thing
    Animal : Mode = Open
}

Creature := Animal.New

Creature.Sleep
// Step 1-5: No explicit resolution
// Step 6: Check Mode → Open → Continue
// Step 7: SemanticResolve(Creature, Sleep)
//   Query: "What is 'Sleep' to 'Animal'?"
//   NLP: "Sleep is a rest state" (confidence: 0.95)
//   Create temporary relation
// Result: Creature.State = "Sleeping"
```

**Example 3: Guided Mode with pattern**

```
Structure Emotion @ 1.3 {
    Emotion := Valenced_Experience
    Emotion : Mode = Guided
    Emotion : Inference_Pattern = "Subject.Feel.*"
}

Person := Person.New

Person.Feel.Joy
// Step 6: Check Mode → Guided
//   Pattern = "Subject.Feel.*"
//   "Feel.Joy" matches pattern → Continue
// Step 7: SemanticResolve succeeds
// Result: Person experiences Joy

Person.Experience.Joy
// Step 6: Check Mode → Guided
//   Pattern = "Subject.Feel.*"
//   "Experience.Joy" does NOT match → Block
// Result: Stall("Pattern mismatch for Guided inference")
```

---

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

---

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
// Promoted relation inherits Mode from source
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
| Eager | Evaluate immediately | Assignments, Grammar ops, Instance creation |

**Lazy example:**

```
HeavyComputation.Return.{...complex...}

Result := HeavyComputation    // NOT executed yet
// Result holds reference to HeavyComputation

Result.Emit                   // NOW executed
```

**Force eager evaluation:**

```
Result := HeavyComputation.Eval   // Executed immediately
```

---

### 5.72 Evaluation Order

Within a statement, evaluation proceeds:
1. Left to right for dot chains
2. Inner to outer for nested groups
3. Arguments before application

---

### 5.73 Concurrency

The Interpreter may evaluate independent expressions concurrently:

```
Structure Parallel @ 5.73 {
    Parallel := Concurrent_Executor
    Parallel : Mode = Strict
}
```

**Syntax:**

```
[A.Compute, B.Compute, C.Compute].Parallel
```

**Structure/Instance consideration:** Parallel operations must not attempt to modify the same Instance concurrently.

---

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

### 5.81 Error Types (v0.3)

| Error | Cause | Recovery |
|-------|-------|----------|
| ParseError | Invalid syntax | Report, skip to next statement |
| TypeError | Operation on wrong type | Stall or coerce |
| **StructureError** | Attempt to modify Structure | Stall with suggestion |
| **ModeError** | Invalid Mode value | Report, use default |
| StackOverflow | Infinite recursion | Halt current call chain |
| MemoryExhausted | Workspace full | GC, then halt if still full |
| IOError | File/device failure | Stall with retry option |
| Halt | Explicit Must failure | Stop execution |

### 5.82 Error Propagation

Errors propagate up the call stack:

```
A.Return.{
    B           // B causes error
}

B.Return.{
    C           // C causes error
}

C.Return.{
    Null.Must   // Halt: Null failed Must
}

// Error propagates: C → B → A → Top level
// Execution halts with stack trace
```

---

### 5.83 Try Recovery

Try blocks catch errors and stalls:

```
RiskyOperation.Try.{
    "Operation failed".Emit
    FallbackValue
}
```

---

## 5.9 Interpreter Interface

How external systems interact with the Interpreter.

```
Structure InterpreterInterface @ 5.9 {
    InterpreterInterface := API
    InterpreterInterface : Mode = Strict
}
```

### 5.91 REPL Mode

Interactive read-eval-print loop (v0.3):

```
Uypocode REPL v0.3
> Structure Dog @ 1.4.1 {
.     Dog := Animal
.     Dog : Sound = "Bark"
.     Dog : Mode = Strict
. }
Registered: Structure Dog at 1.4.1 (Mode: Strict)

> Fido := Dog.New
Created: Instance Fido at 4.1.1 (Prototype: Dog)

> Fido.Sound.Emit
Bark

> Fido.Fly
Stall: No 'Fly' property on Fido
  Mode: Strict (inherited from Dog)
  Inference: Blocked
  Suggestion: Add 'Fido : Fly = ...' or change Mode to Open

> :structures
Structures:
  1.4.1 Dog : Animal (Mode: Strict)
  
> :instances
Instances:
  4.1.1 Fido : Dog.New (Prototype: Dog)

> :exit
Goodbye
```

**REPL Commands (v0.3):**

| Command | Description |
|---------|-------------|
| `:stalls` | List pending stalls with Mode info |
| `:dictionary` | Show current Dictionary |
| `:structures` | List all Structures |
| `:instances` | List all Instances |
| `:context` | Show current Context |
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
- Exit code (0 = success, 1 = stalls, 2 = error)
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
Interpreter: Query Dog.Metadata
Response: {Sound: "Bark", Legs: 4, Mode: Strict}
```

**Check Mode before suggesting inference:**
```
LLM: "What does Fido.Bark mean?"
Interpreter: Fido.Prototype = Dog, Dog.Mode = Strict
Response: "Inference blocked. Dog has Mode = Strict.
          Either add explicit 'Bark' property or change Mode."
```

**Propose changes respecting Structure/Instance:**
```
LLM: "Add a Color property to Dog"
Interpreter: Dog is a Structure (immutable)
Response: "Cannot modify Structure. Options:
          1. Add to Structure definition (requires reload)
          2. Add to Instance: Fido : Color = 'Brown'"
```

---

## 5.99 Section 5.0 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 5.0 | Interpreter | Execution engine |
| 5.1 | Pipeline | Six-phase execution |
| 5.11 | Tokenization | Lexical analysis |
| 5.115 | Structure Registration | v0.3: Structure validation |
| 5.12 | Indexing | Symbol table construction |
| 5.13 | Definition | Content population |
| 5.14 | Resolution | Expression execution |
| 5.15 | Finalization | Cleanup and reporting |
| 5.2 | Parsing | Syntax analysis |
| 5.21 | Grammar Rules | Formal syntax (v0.3 extended) |
| 5.22 | AST | Tree representation |
| 5.23 | Parse Errors | Syntax failure handling |
| 5.3 | Resolution Algorithm | Dot evaluation |
| 5.31 | Resolution Steps | Priority order (v0.3: Mode check) |
| 5.32 | Chained Resolution | Multi-dot handling |
| 5.33 | Argument Handling | Binary operations |
| 5.34 | Grouping | Parentheses evaluation |
| 5.35 | Structure Mutation | v0.3: Immutability enforcement |
| 5.4 | Stall Handling | Pending expressions |
| 5.41 | Stall Creation | Recording failures |
| 5.42 | Stall Propagation | Chain failures |
| 5.43 | Stall Resolution | Retry mechanism |
| 5.44 | Stall Modes | Strict/Lenient/Interactive |
| 5.5 | Context Management | State tracking |
| 5.51 | Context Updates | Post-expression updates |
| 5.52 | Scope Transitions | Function/cycle entry/exit |
| 5.6 | Semantic Inference | Mode-controlled NLP resolution |
| 5.61 | Inference Trigger | When to use NLP (Mode check) |
| 5.62 | Inference Examples | Semantic resolution by Mode |
| 5.63 | Confidence | Threshold handling |
| 5.64 | Caching | Inference reuse |
| 5.7 | Execution Model | Runtime behavior |
| 5.71 | Lazy Evaluation | Deferred computation |
| 5.72 | Evaluation Order | Expression sequencing |
| 5.73 | Concurrency | Parallel execution |
| 5.74 | Tail Call | Recursion optimization |
| 5.8 | Error Handling | Exception management |
| 5.81 | Error Types | Failure categories (v0.3 extended) |
| 5.82 | Error Propagation | Stack unwinding |
| 5.83 | Try Recovery | Graceful handling |
| 5.9 | Interface | External API |
| 5.91 | REPL | Interactive mode |
| 5.92 | Batch | File execution |
| 5.93 | Library | Embedding |
| 5.94 | LLM Integration | AI collaboration |

---

# Appendix A: Complete Address Index

## Section 0.x - Kernel
| Address | Label | Mode |
|---------|-------|------|
| 0.0 | Kernel | Strict |
| 0.1 | English | Open |
| 0.2 | Math | Strict |
| 0.3 | Logic | Strict |
| 0.4 | Time | Strict |
| 0.5 | File | Strict |

## Section 1.x - Objects (Structures)
| Address | Label | Mode |
|---------|-------|------|
| 1.0 | Object | Strict |
| 1.1 | Label | Strict |
| 1.11 | Context | Strict |
| 1.2 | Address | Strict |
| 1.3 | Contents | Strict |
| 1.31 | Value | Strict |
| 1.32 | Reference | Strict |
| 1.33 | List | Strict |
| 1.34 | Logic | Strict |
| 1.35 | Null | Strict |
| 1.4 | Metadata | Strict |
| 1.5 | Number | Strict |
| 1.6 | Text | Strict |
| 1.7 | Boolean | Strict |
| 1.8 | List | Strict |
| 1.9 | Pronoun | Strict |
| 1.91 | It | Strict |
| 1.92 | That | Strict |
| 1.93 | Self | Strict |
| 1.95 | Null | Strict |
| 1.96 | File | Strict |
| 1.97 | Lifecycle | Strict |
| 1.98 | Identity | Strict |

## Section 2.x - Relations (Structures)
| Address | Label | Mode |
|---------|-------|------|
| 2.0 | Relation | Guided |
| 2.1 | Dot Operator | Strict |
| 2.11 | Containment | Strict |
| 2.12 | Metadata | Strict |
| 2.13 | Relation Lookup | Strict |
| 2.14 | Grammar | Strict |
| 2.15 | Stall | Strict |
| 2.16 | Mode Check | Strict |
| 2.2 | Relation Structure | Guided |
| 2.21 | Unary | Guided |
| 2.22 | Binary | Guided |
| 2.23 | Chained | Guided |
| 2.3 | Type Constraints | Strict |
| 2.4 | Precedence | Strict |
| 2.5 | Built-in | Strict |
| 2.51 | Number Relations | Strict |
| 2.52 | Text Relations | Strict |
| 2.53 | Boolean Relations | Strict |
| 2.54 | List Relations | Strict |
| 2.6 | User-Defined | Guided |
| 2.7 | Composition | Guided |
| 2.8 | Symmetry/Inverse | Strict |
| 2.9 | Stalled | Strict |

## Section 3.x - Grammar (Structures)
| Address | Label | Mode |
|---------|-------|------|
| 3.0 | Grammar | Strict |
| 3.1 | Then | Strict |
| 3.11 | Else | Strict |
| 3.12 | When | Strict |
| 3.2 | Cycle | Strict |
| 3.21 | Item | Strict |
| 3.22 | Times | Strict |
| 3.23 | Index | Strict |
| 3.24 | While | Strict |
| 3.25 | Break | Strict |
| 3.26 | Skip | Strict |
| 3.3 | Emit | Strict |
| 3.31 | Format | Strict |
| 3.4 | Capture | Strict |
| 3.41 | Prompt | Strict |
| 3.5 | As | Strict |
| 3.51 | Into | Strict |
| 3.6 | Return | Strict |
| 3.61 | Parameters | Strict |
| 3.62 | Yield | Strict |
| 3.7 | Try | Strict |
| 3.71 | Must | Strict |
| 3.8 | With | Strict |
| 3.81 | Global | Strict |
| 3.82 | Local | Strict |
| 3.9 | Import | Strict |
| 3.91 | Export | Strict |

## Section 4.x - Workspace (Runtime Instances)
| Address | Label | Mode |
|---------|-------|------|
| 4.0 | Workspace | Strict |
| 4.1 | Global | Strict |
| 4.11 | Address Allocation | Strict |
| 4.12 | Persistence | Strict |
| 4.2 | Local | Strict |
| 4.21 | Scope Boundaries | Strict |
| 4.22 | Stack Behavior | Strict |
| 4.23 | Shadowing | Strict |
| 4.3 | Context | Strict |
| 4.31 | Pronouns | Strict |
| 4.32 | Call Stack | Strict |
| 4.4 | Instances | Strict |
| 4.41 | Identity | Strict |
| 4.42 | Hierarchy | Strict |
| 4.43 | Type Checking | Strict |
| 4.5 | References | Strict |
| 4.51 | DeepCopy | Strict |
| 4.6 | GarbageCollector | Strict |
| 4.61 | Limits | Strict |
| 4.7 | State | Strict |
| 4.71 | Branches | Strict |

## Section 5.x - Interpreter (Structures)
| Address | Label | Mode |
|---------|-------|------|
| 5.0 | Interpreter | Strict |
| 5.1 | Pipeline | Strict |
| 5.11 | Tokenization | Strict |
| 5.115 | Structure Registration | Strict |
| 5.12 | Indexing | Strict |
| 5.13 | Definition | Strict |
| 5.14 | Resolution | Strict |
| 5.15 | Finalization | Strict |
| 5.2 | Parsing | Strict |
| 5.21 | Grammar Rules | Strict |
| 5.22 | AST | Strict |
| 5.23 | Parse Errors | Strict |
| 5.3 | Resolution Algorithm | Strict |
| 5.31 | Resolution Steps | Strict |
| 5.32 | Chained Resolution | Strict |
| 5.33 | Argument Handling | Strict |
| 5.34 | Grouping | Strict |
| 5.35 | Structure Mutation | Strict |
| 5.4 | Stall Handling | Strict |
| 5.41 | Stall Creation | Strict |
| 5.42 | Stall Propagation | Strict |
| 5.43 | Stall Resolution | Strict |
| 5.44 | Stall Modes | Strict |
| 5.5 | Context Management | Strict |
| 5.51 | Context Updates | Strict |
| 5.52 | Scope Transitions | Strict |
| 5.6 | Semantic Inference | Strict |
| 5.61 | Inference Trigger | Strict |
| 5.62 | Inference Examples | Strict |
| 5.63 | Confidence | Strict |
| 5.64 | Caching | Strict |
| 5.7 | Execution Model | Strict |
| 5.71 | Lazy Evaluation | Strict |
| 5.72 | Evaluation Order | Strict |
| 5.73 | Concurrency | Strict |
| 5.74 | Tail Call | Strict |
| 5.8 | Error Handling | Strict |
| 5.81 | Error Types | Strict |
| 5.82 | Error Propagation | Strict |
| 5.83 | Try Recovery | Strict |
| 5.9 | Interface | Strict |
| 5.91 | REPL | Strict |
| 5.92 | Batch | Strict |
| 5.93 | Library | Strict |
| 5.94 | LLM Integration | Strict |

---

# Appendix B: Quick Reference

## Operators (v0.3)

| Operator | Name | Usage |
|----------|------|-------|
| `:=` | Assignment | `Label := Contents` |
| `:` | Definition | `Subject : Predicate` |
| `.` | Dot | `Subject.Accessor` |
| `=` | Equivalence/Set | `A = B` |
| **`@`** | Address Override | `Label @ Address` |
| `()` | Grouping | `(Expression)` |
| `[]` | List | `[A, B, C]` |
| `{}` | Logic Block / Structure Body | `{Statements}` |
| `//` | Comment | `// This is ignored` |

## Keywords (v0.3)

| Keyword | Purpose |
|---------|---------|
| **`Structure`** | Declare immutable prototype |
| **`Scope`** | Auto-address assignment block |
| **`Mode`** | Inference control metadata |
| **`Strict`** | Forbid semantic inference |
| **`Guided`** | Pattern-constrained inference |
| **`Open`** | Allow full inference |
| `.New` | Create Instance from Structure |
| `.Is` | Check prototype inheritance |
| `.Prototype` | Get Structure reference |
| `.Identical` | Check address equality |

## Primitives

| Type | Examples |
|------|----------|
| Number | `42`, `3.14`, `-7` |
| Text | `"Hello"`, `""` |
| Boolean | `True`, `False` |
| List | `[1, 2, 3]`, `[]` |
| Null | `Null` |
| **Mode** | `Strict`, `Guided`, `Open` |

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
| Location | 0.x - 3.x | 4.x |
| Mutability | Immutable | Mutable |
| Creation | `Structure Label @ Addr {}` | `Structure.New` |
| Purpose | Template/Prototype | Runtime Object |
| Mode | Defined on Structure | Inherited from Prototype |

---

# Appendix C: Amendment Summary

## Amendment A: Auto-Addressing Syntax

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

## Amendment B: Structure/Instance Formalization

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
- Structures live in 0.x-3.x, are immutable
- Instances live in 4.x, are mutable
- `.New` creates Instance from Structure
- Instances have: Prototype, Instance_ID, Created_At

---

## Amendment C: Semantic Inference Guard Rails

**Purpose:** Control when NLP inference can override explicit specifications.

**Modes:**

| Mode | Behavior |
|------|----------|
| `Strict` | No inference - stall immediately |
| `Guided` | Pattern-constrained inference |
| `Open` | Full inference permitted |

**Syntax:**
```
Structure MyObject @ 1.x {
    MyObject := Contents
    MyObject : Mode = Strict    // or Guided, or Open
    MyObject : Inference_Pattern = "Subject.Verb.*"  // for Guided
}
```

**Mode Inheritance:** Children inherit parent's Mode unless overridden.

---

# Appendix D: Example Program (v0.3)

```
// Uypocode v0.3 Example: Pet Management System

// Import required modules
Import.Math
Import.Logic

// Define Structures with explicit Mode control
Structure Pet @ 1.1 {
    Pet := Animal
    Pet : Name = Null
    Pet : Age = Null
    Pet : Species = Null
    Pet : Mode = Guided    // Allow some inference
    Pet : Inference_Pattern = "Subject.Feel.*"
}

Structure Dog @ 1.1.1 {
    Dog := Pet
    Dog : Species = "Canine"
    Dog : Sound = "Bark"
    Dog : Mode = Strict    // Override: no inference for dogs
}

Structure Cat @ 1.1.2 {
    Cat := Pet
    Cat : Species = "Feline"
    Cat : Sound = "Meow"
    Cat : Mode = Strict
}

// Define Relations with Scope for auto-addressing
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

// Create Instances (in Workspace 4.x)
Fido := Dog.New.(Name = "Fido", Age = 3)
Whiskers := Cat.New.(Name = "Whiskers", Age = 5)

// Execute operations
"=== Pet Sounds ===".Emit
Fido.Speak          // Output: Bark
Whiskers.Speak      // Output: Meow

"=== Pet Info ===".Emit
Fido.Describe
// Output: Name: Fido
// Output: Age: 3
// Output: Species: Canine

"=== Birthday ===".Emit
Fido.Birthday       // Output: Happy Birthday, Fido!
Fido.Age.Emit       // Output: 4

"=== Type Checking ===".Emit
Fido.Is.Dog.Emit        // Output: True
Fido.Is.Pet.Emit        // Output: True
Fido.Is.Cat.Emit        // Output: False
Fido.Prototype.Emit     // Output: Dog

"=== Mode Demonstration ===".Emit
Fido.Fly
// Stalls: No 'Fly' property
// Mode: Strict (inherited from Dog)
// Inference: Blocked

"=== All Pets ===".Emit
Pets := [Fido, Whiskers]
Pets.Cycle.{Item.Name.Emit}
// Output: Fido
// Output: Whiskers

"=== Attempting Structure Modification ===".Emit
Dog.Sound = "Woof"
// Stalls: Cannot modify Structure
// Suggestion: Use Dog.New to create modifiable Instance
```

---

# Appendix E: Migration Guide (v0.2 → v0.3)

## Syntax Changes

| v0.2 | v0.3 |
|------|------|
| `Dog := (Dog, 1.4.1, Animal)` | `Structure Dog @ 1.4.1 { Dog := Animal }` |
| Manual addresses | `Scope(Parent) { ... }` for auto-addressing |
| No Mode concept | `Object : Mode = Strict/Guided/Open` |
| Implicit mutability | Explicit Structure (immutable) vs Instance (mutable) |

## Behavioral Changes

1. **Structures are immutable**: Any attempt to modify an Object in 0.x-3.x now stalls
2. **Mode controls inference**: Objects can now block or constrain semantic inference
3. **Type checking enhanced**: `.Is`, `.Prototype`, `.Identical` operations added
4. **Resolution order updated**: Mode check inserted before semantic inference

## Backward Compatibility

- Old `:=` syntax still parsed but treated as Structure in 0-3.x, Instance in 4.x
- Objects without Mode default to `Open` for backward compatibility
- Existing programs will run but should be updated for explicit Mode control

---

**End of Uypocode Master Dictionary v0.3**

---

# Changelog

## v0.3 (Current)

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

