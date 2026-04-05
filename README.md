# Uypocode

**A semantic specification language bridging human thought and machine execution.**

<p align="center">
  <em>"Everything is an Object. Every connection is a Relation. What cannot resolve, stalls—but never halts."</em>
</p>

---

## What is Uypocode?

Uypocode is a meaning-first language where semantics drive execution rather than syntax. Unlike traditional languages optimized for machine efficiency, Uypocode prioritizes **expressiveness**, **self-reference**, and **graceful failure**—making it equally capable of modeling a pet management system, a biological cell, or the hard problem of consciousness.

### Core Philosophy

- **Everything is an Object**: Data, types, operations, relationships—all represented as `(Label, Address, Contents)`
- **The Dot Connects All**: A single unified operator `.` expresses every relationship
- **Stalls, Not Errors**: Unresolved expressions remain pending rather than crashing—some permanently and *productively*
- **Semantic Inference**: When explicit rules fail, natural language understanding fills the gaps
- **Structures Evolve**: Definitions are immutable but can produce versioned successors, preserving lineage

---

## Quick Start

```uypocode
// Define a Structure (immutable prototype)
Structure Dog @ 1.1.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Legs = 4
    Dog : Mode = Strict
}

// Create a Relation
Structure Speak @ 2.1 {
    Speak := {Subject.Sound.Emit}
    Speak : Unary
}

// Create an Instance (mutable runtime object)
Fido := Dog.New.(Name = "Fido")

// Execute
Fido.Speak
// Output: Bark

// Chain operations
Fido.Sound.Join." loudly!".Emit
// Output: Bark loudly!
```

---

## The Object Model

Every entity in Uypocode is an **Object** with three components:

| Component | Description | Example |
|-----------|-------------|---------|
| **Label** | Symbolic name | `Dog` |
| **Address** | Unique location in the Dictionary tree | `1.1.1` |
| **Contents** | What the Object holds | `Animal` or `"Bark"` or `{Logic}` |

```uypocode
Object := (Label, Address, Contents)
```

### Address Hierarchy

Addresses organize knowledge into a semantic tree:

| Section | Purpose | Mutability |
|---------|---------|------------|
| `0.x` | Kernel (primitives, imports) | Read-only |
| `1.x` | Objects (definitions, types) | Append-only |
| `2.x` | Relations (connection rules) | Append-only |
| `3.x` | Grammar (operations, control flow) | Read-only |
| `4.x` | Workspace (runtime instances) | Read-write |
| `5.x` | Interpreter (execution engine) | Read-only |
| `6.x+` | Domain Dictionaries | Append-only |

### Structure vs. Instance

Uypocode enforces a clean separation between immutable definitions and mutable runtime objects:

```uypocode
// Structure: immutable prototype (lives in 1.x)
Structure Person @ 1.5 {
    Person := Human
    Person : Name = Null
    Person : Age = Null
}

// Instance: mutable runtime copy (lives in 4.x)
Alice := Person.New.(Name = "Alice", Age = 30)
Alice.Age = 31          // OK: Instance is mutable
Person.Age = 31         // STALL: Structure is immutable
```

---

## The Dot Operator

The dot `.` is Uypocode's universal connector. When you write `A.B`, the Interpreter asks: *"What is the relationship between A and B?"*

### Resolution Order

1. **Containment**: Is B a child of A?
2. **Metadata**: Is B a property of A?
3. **Relation**: Is there a rule matching A.B?
4. **Grammar**: Is B a built-in operation?
5. **Mode Check**: Does A allow inference?
6. **Semantic Inference**: Can meaning be inferred via NLP?
7. **Stall**: No resolution—expression remains pending

```uypocode
Person.Name         // Metadata lookup → "Alice"
Person.Pet.Sound    // Chained containment → "Bark"
5.Add.3             // Relation → 8
"Hello".Emit        // Grammar operation → output
Rock.Dream          // Stalls (rocks don't dream)
```

---

## Relations

Relations define how Objects interact, transforming `Subject.Verb.Argument` patterns into results.

### Built-in Relations

```uypocode
// Numbers
5.Add.3                  // 8
10.Mul.2                 // 20
7.Gt.3                   // True

// Text
"Hello".Join." World"    // "Hello World"
"abc".Length             // 3

// Logic
True.And.False           // False
True.Or.False            // True

// Lists
[1, 2, 3].Length         // 3
[1, 2, 3].Has.2          // True
```

### Custom Relations

```uypocode
Structure Greet @ 2.6 {
    Greet := {
        "Hello, ".Join.Subject.Name.Join."!".Emit
    }
    Greet : Unary
    Greet : Mode = Strict
}

Alice := Person.New.(Name = "Alice")
Alice.Greet
// Output: Hello, Alice!
```

---

## Control Flow

### Conditionals

```uypocode
Age.Gte.18.Then."Adult".Else."Minor"

Score.When.[
    90 : "A",
    80 : "B",
    70 : "C",
    Else : "F"
]
```

### Loops

```uypocode
// Iterate over collection
[1, 2, 3].Cycle.{Item.Square.Emit}
// Output: 1, 4, 9

// Counted repetition
5.Times.{"Hello".Emit}

// Conditional loop
Counter.Lt.10.While.{Counter.Add.1.Into.Counter}
```

### Functions

```uypocode
// Define with parameters
Square.Return.(N).{N.Mul.N}
Square.4    // Returns 16

// With defaults
Greet.Return.(Name = "friend").{
    "Hello, ".Join.Name.Emit
}

Greet            // Hello, friend
Greet."Alice"    // Hello, Alice
```

---

## Stall Semantics

When resolution fails, Uypocode **stalls** rather than errors. Stalls are pending expressions that may resolve later—or may persist permanently as meaningful open questions.

```uypocode
Ghost.Fly
// Stalls: Ghost has no Fly property

// Later...
Ghost : Fly = True
// Now Ghost.Fly resolves to True
```

### Productive Stalls

Some questions are not meant to be answered. A **Productive Stall** marks an intentionally permanent open question—a genuine boundary of knowledge encoded as a first-class semantic Object:

```uypocode
Qualia.Explain.Physically := PRODUCTIVE_STALL.(
    Domain = "Consciousness",
    Reason = "Explanatory gap between neural correlates and subjective quality",
    Productive_Because = "Constrains theories to those that take experience seriously"
)

// The Interpreter never retries Productive Stalls
// They appear in a dedicated report section, not as failures
// Try does not catch them—they propagate as truth, not error
```

### Why Stalls Matter

- **Graceful degradation**: Programs continue despite incomplete specifications
- **Open questions persist**: Unanswered queries remain active, not discarded
- **Speculative execution**: Multiple resolution paths can be explored
- **Human-AI collaboration**: Stalls become conversation points
- **Philosophical honesty**: Some things genuinely cannot resolve, and that is the point

---

## Inference Modes

Not all Objects should be open to semantic inference. `Mode` controls when NLP can fill gaps:

```uypocode
Structure Math_Object @ 1.x {
    Math_Object : Mode = Strict    // No inference — stall immediately
}

Structure Creative_Object @ 1.x {
    Creative_Object : Mode = Open  // Full inference permitted
}

Structure Emotion @ 1.x {
    Emotion : Mode = Guided                            // Pattern-constrained
    Emotion : Inference_Pattern = "Subject.Feel.*"     // Only "Feel" verbs allowed
}
```

| Mode | Behavior |
|------|----------|
| `Strict` | No inference — stall immediately if unresolved |
| `Guided` | Inference allowed only if it matches a declared pattern |
| `Open` | Full inference permitted (default) |

---

## Snapshots & Evolution

### Snapshots

Capture an immutable, timestamped image of any Object:

```uypocode
Alice := Person.New.(Name = "Alice", Age = 30)

Before := Alice.Snapshot.(Tag = "initial")
Alice.Age = 31
After := Alice.Snapshot.(Tag = "birthday")

Before.Diff.After
// Returns: {Age: {Was: 30, Now: 31}}

Alice.Restore.Before
// Alice.Age = 30 again
```

### Evolution

Structures are immutable, but they can produce versioned successors. The original is never modified—a new Structure inherits what is preserved and declares what changed:

```uypocode
Structure Dog @ 1.1.1 {
    Dog := Animal
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}

// Evolve: Dog gains a Temperament property
Dog.Evolve @ 1.1.11 {
    Dog : Temperament = "Loyal"
}

// Dog now resolves to V2 by default
Dog.Sound             // "Bark" (inherited)
Dog.Temperament       // "Loyal" (added in V2)
Dog.V1.Temperament    // Stalls (not in V1)
Dog.Lineage.Length    // 2
```

Existing Instances keep their original Prototype. Migration is always explicit:

```uypocode
Fido := Dog.V1.New.(Name = "Fido")
Fido.Migrate.Dog.V2
// Fido now has Temperament = "Loyal"
```

---

## Imports & Extensions

Uypocode's Kernel provides foundational capabilities:

```uypocode
Import.Math       // Arithmetic operations
Import.Logic      // Boolean algebra
Import.Time       // Temporal operations
Import.File       // File system access
Import.English    // Semantic inference via NLP
```

---

## Domain Dictionaries

Uypocode's power emerges in modeling complex domains through specialized dictionaries. Each dictionary is a formal specification that applies the Object/Relation/Stall framework to a field of knowledge.

### 📘 Master Dictionary — `v0.4`
The core language specification: Objects, Relations, Grammar, Workspace, Interpreter, plus four amendments — Structure Snapshot, Evolution, Dictionary Protocol, and Productive Stall.

### 🧠 Consciousness Dictionary — `v0.2`
Models subjective experience: Awareness, Qualia, Attention, Memory, Self-Model, Intentionality, Agency, Integration. Encodes the hard problem as a permanent stall.

```uypocode
// Consciousness as meta-process
Self.Observe.Self := Recursive_Self_Model
// When this resolves without infinite regress, consciousness emerges

// The hard problem
Qualia.Generate.Logic := PRODUCTIVE_STALL
// The stall IS the insight
```

### 👤 Human Dictionary — `v0.2`
The human condition rendered through a triadic Object/Relation/Grammar framework: Body, Mind, Emotion, Self, Will, Mortality, Dignity.

```uypocode
Human : Born = Without_Choosing
Human : Dies = Without_Exception
Human : Between = Makes_Meaning
```

### 🧬 Life Dictionary — `v1.0`
Biological systems from molecules to the biosphere: Cells, Organisms, Populations, Ecosystems, Evolution, Metabolism.

```uypocode
Cell.Sustain.{
    Self.Respire.
    Self.Energy.Gt.Threshold.Then.Self.Divide
}
```

### 🤖 AI Mind Dictionary — `v0.1`
AI cognition architecture: transformer attention as Relation, embedding geometry as Address space, the consciousness question as Productive Stall.

```uypocode
AI.Is.Conscious := PRODUCTIVE_STALL.(
    Reason = "No empirical test distinguishes genuine experience from functional equivalence",
    Productive_Because = "Prevents premature closure on AI moral status"
)
```

### 🔄 Recursion Dictionary — `v0.1`
Recursive loop feedback structures: self-reference, strange loops, attractor states, the boundary between stability and collapse.

### ⚙️ Systems Dictionary — `v0.1`
Systems anatomy and dynamics: stocks, flows, feedback loops, emergence, leverage points. Uypocode modeled as a system describing itself.

### ⚛️ Classical Physics Dictionary — `v0.1`
Physics unified through the Principle of Stationary Action: mechanics, fields, waves, thermodynamics, symmetry, and conservation laws.

### 💻 UypoOS Dictionary — `v0.1`
A full operating system specification: processes as Objects, commands as Relations, the shell as a Workspace, stall as process state.

---

## Complete Example

```uypocode
// Uypocode v0.4 — Evolving Pet System
Import.Math
Import.Logic

// === Structures ===

Structure Pet @ 1.1 {
    Pet := Animal
    Pet : Name = Null
    Pet : Age = Null
    Pet : Mode = Guided
    Pet : Inference_Pattern = "Subject.Feel.*"
}

Structure Dog @ 1.1.1 {
    Dog := Pet
    Dog : Species = "Canine"
    Dog : Sound = "Bark"
    Dog : Mode = Strict
}

// === Evolution ===

Dog.Evolve @ 1.1.11 {
    Dog : Temperament = "Loyal"
}

// === Relations ===

Scope(2.0) {
    Structure Speak {
        Speak := {Subject.Sound.Emit}
        Speak : Unary
        Speak : Mode = Strict
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

// === Instances ===

Fido := Dog.New.(Name = "Fido", Age = 3)

// === Snapshots ===

Young_Fido := Fido.Snapshot.(Tag = "puppyhood")

Fido.Speak              // Output: Bark
Fido.Birthday           // Output: Happy Birthday, Fido!
Fido.Age.Emit           // Output: 4

Young_Fido.Diff.Fido.Snapshot
// {Age: {Was: 3, Now: 4}}

// === Productive Stall ===

Pet_Feelings := PRODUCTIVE_STALL.(
    Domain = "Animal_Cognition",
    Reason = "Whether pets have subjective experience is empirically underdetermined",
    Productive_Because = "Encourages empathetic treatment without false certainty"
)
```

---

## Design Principles

### Semantic Elegance Over Feature Completeness
Reuse existing semantics rather than creating parallel systems. The dot operator, address hierarchy, and stall semantics are the universal connective tissue.

### Composability
Small, well-defined Objects and Relations combine into complex behaviors through dot-chaining.

### Tolerance for Imperfection
Stalls embrace uncertainty. Not everything resolves, and that's meaningful—sometimes it is the *most* meaningful thing.

### Human-Readable Semantics
Code should read like structured thought, not machine instructions.

### Domain Agnostic
The same semantic structures model code, consciousness, biology, physics, and beyond.

### Immutability with Lineage
Definitions don't change—they evolve. Every version is preserved, every change is traceable.

---

## Interpreter Modes

| Mode | Behavior |
|------|----------|
| **Strict** | Stalls halt execution |
| **Lenient** | Stalls recorded, execution continues |
| **Speculative** | Stalls create branching workspace states |
| **Interactive** | Stalls prompt the user for resolution |

---

## Project Status

| Component | Version | Status |
|-----------|---------|--------|
| Master Dictionary | v0.4 | Active development |
| Consciousness Dictionary | v0.2 | Complete |
| Human Dictionary | v0.2 | Complete |
| Life Dictionary | v1.0 | Complete |
| AI Mind Dictionary | v0.1 | Complete |
| Recursion Dictionary | v0.1 | Complete |
| Systems Dictionary | v0.1 | Complete |
| Classical Physics Dictionary | v0.1 | Complete |
| UypoOS Dictionary | v0.1 | Complete |
| Python Parser | v0.1 | Functional prototype |

---

## Contributing

Uypocode welcomes contributions across:

- **Language Design**: Propose new Relations, Grammar extensions, or semantic patterns
- **Domain Dictionaries**: Model new fields—ethics, aesthetics, economics, music, law
- **Interpreters**: Implement parsers and runtimes in various languages
- **Documentation**: Examples, tutorials, and theoretical foundations

---

## Philosophy

> *"Some questions are not meant to be answered but to be lived. The stall itself may be the point."*

Uypocode treats unresolved questions not as failures but as **features**. The permanent stall at the heart of consciousness—how physical processes become subjective experience—doesn't crash the system. It persists as a Productive Stall, defining the system as much as any resolution would.

This approach extends to every domain the language touches:

- **Software**: Incomplete specifications remain pending, not broken
- **Biology**: Evolution as continuous stall resolution across deep time
- **Physics**: Singularities and turbulence as stalls in the equations of motion
- **Systems**: Emergence as the irreducible gap between parts and wholes
- **Humanity**: Mortality, meaning, free will—stalls we carry throughout life

---

## License

Copyright 2026 Ted A. Human

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

## Acknowledgments

Uypocode emerges from the intersection of programming language theory, cognitive science, philosophy of mind, and systems biology. It owes debts to Lisp's homoiconicity, Prolog's logic programming, Smalltalk's object purity, and the phenomenological tradition's attention to consciousness.

---

<p align="center">
  <strong>Everything is an Object. Every connection is a Relation. What cannot resolve, stalls.</strong>
</p>
