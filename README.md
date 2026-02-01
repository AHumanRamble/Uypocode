# Uypocode

**A semantic specification language bridging human thought and machine execution.**

<p align="center">
  <em>"Everything is an Object. Every connection is a Relation. What cannot resolve, stalls—but never halts."</em>
</p>

---

## What is Uypocode?

Uypocode is a meaning-first programming language where semantics drive execution rather than syntax. Unlike traditional languages optimized for machine efficiency, Uypocode prioritizes **expressiveness**, **self-reference**, and **graceful failure**—making it ideal for modeling complex domains from consciousness to ecosystems.

### Core Philosophy

- **Everything is an Object**: Data, types, operations, relationships—all represented as `(Label, Address, Contents)`
- **The Dot Connects All**: A single unified operator `.` expresses every relationship
- **Stalls, Not Errors**: Unresolved expressions remain pending rather than crashing—the system continues
- **Semantic Inference**: When explicit rules fail, natural language understanding fills the gaps

---

## Quick Start

```uypocode
// Define an object
Dog := (Dog, 1.1.1, Animal)
Dog : Sound = "Bark"
Dog : Legs = 4

// Create a relation
Speak := (Speak, 2.1, {Subject.Sound.Emit})

// Execute
Dog.Speak
// Output: Bark

// Chain operations
Dog.Sound.Join." loudly!".Emit
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
| `1.x` | Structure (definitions, types) | Append-only |
| `2.x` | Relations (connection rules) | Append-only |
| `3.x` | Grammar (operations, control flow) | Read-only |
| `4.x` | Workspace (runtime instances) | Read-write |
| `5.x` | Interpreter (execution engine) | Read-only |
| `6.x+` | Domain Extensions | Varies |

---

## The Dot Operator

The dot `.` is Uypocode's universal connector. When you write `A.B`, the interpreter asks: *"What is the relationship between A and B?"*

### Resolution Order

1. **Containment**: Is B a child of A?
2. **Metadata**: Is B a property of A?
3. **Relation**: Is there a rule matching A.B?
4. **Grammar**: Is B a built-in operation?
5. **Semantic Inference**: Can meaning be inferred? (optional)
6. **Stall**: No resolution—expression remains pending

```uypocode
Person.Name         // Metadata lookup
Person.Pet.Sound    // Chained containment
5.Add.3             // Relation (returns 8)
"Hello".Emit        // Grammar operation
Rock.Dream          // Stalls (rocks don't dream)
```

---

## Relations

Relations define how Objects interact. They transform `Subject.Verb.Argument` patterns into results.

### Built-in Relations

```uypocode
// Numbers
5.Add.3       // 8
10.Mul.2      // 20
7.Gt.3        // True

// Text
"Hello".Join." World"    // "Hello World"
"abc".Length             // 3

// Logic
True.And.False           // False
True.Or.False            // True

// Lists
[1, 2, 3].Length        // 3
[1, 2, 3].Has.2         // True
```

### Custom Relations

```uypocode
// Define a greeting relation
Greet := (Greet, 2.1, {
    "Hello, ".Join.Subject.Name.Join."!".Emit
})

Person := (Person, 1.1, Human)
Person : Name = "Alice"

Person.Greet
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
// Define
Square.Return.(N).{N.Mul.N}

// Call
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

When resolution fails, Uypocode **stalls** rather than errors. Stalls are pending expressions that may resolve later.

```uypocode
Ghost.Fly
// Stalls: Ghost has no Fly property

// Later...
Ghost : Fly = True

// Now Ghost.Fly resolves to True
```

### Why Stalls Matter

- **Graceful degradation**: Programs continue despite incomplete specifications
- **Open questions persist**: Unanswered queries remain active, not discarded
- **Speculative execution**: Multiple resolution paths can be explored
- **Human-AI collaboration**: Stalls become conversation points

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

Uypocode excels at modeling complex domains through specialized dictionaries:

### 📖 Master Dictionary (v0.2)
Core language specification: Objects, Relations, Grammar, Workspace, Interpreter.

### 🧠 Consciousness Dictionary (v0.1)
Models subjective experience: Awareness, Qualia, Attention, Memory, Self-Model, Intentionality, Agency, Integration.

```uypocode
// The hard problem as a permanent stall
Qualia.Generate.Logic := STALL
// How experience arises from matter—unknown
// The stall IS the insight
```

### 👤 Human Dictionary (v0.1)
The human condition in semantic form: Body, Mind, Emotion, Self, Will, Mortality, Dignity.

```uypocode
Human := (Human, ∞, Mystery)
Human : Born = Without_Choosing
Human : Dies = Without_Exception
Human : Between = Makes_Meaning
```

### 🧬 Life Dictionary (v1.0)
Biological systems from molecules to ecosystems: Cells, Organisms, Populations, Evolution, Metabolism.

```uypocode
Cell.Sustain.{
    Self.Respire.
    Self.Energy.Gt.Threshold.Then.Self.Divide
}
```

---

## Example: Complete Program

```uypocode
// Pet Management System
Import.Math
Import.Logic

// Define structures
Pet := (Pet, 1.1, Animal)
Pet : Name = Null
Pet : Age = Null

Dog := (Dog, 1.1.1, Pet)
Dog : Sound = "Bark"

Cat := (Cat, 1.1.2, Pet)
Cat : Sound = "Meow"

// Define relations
Speak := (Speak, 2.1, {Subject.Sound.Emit})

Birthday := (Birthday, 2.2, {
    Subject.Age.Add.1.Into.Subject.Age.
    "Happy Birthday, ".Join.Subject.Name.Join."!".Emit
})

// Create instances
Fido := Dog.New.(Name = "Fido", Age = 3)
Whiskers := Cat.New.(Name = "Whiskers", Age = 5)

// Execute
Fido.Speak              // Output: Bark
Whiskers.Speak          // Output: Meow
Fido.Birthday           // Output: Happy Birthday, Fido!
Fido.Age.Emit           // Output: 4

// Iterate
[Fido, Whiskers].Cycle.{Item.Name.Emit}
// Output: Fido
// Output: Whiskers
```

---

## Design Principles

### 1. Semantic Elegance Over Feature Completeness
Reuse existing semantics rather than creating parallel systems.

### 2. Composability
Small, well-defined Objects and Relations combine into complex behaviors.

### 3. Tolerance for Imperfection
Stalls embrace uncertainty. Not everything resolves, and that's meaningful.

### 4. Human-Readable Semantics
Code should read like structured thought, not machine instructions.

### 5. Domain Agnostic
The same semantic structures model code, consciousness, biology, and beyond.

---

## Interpreter Modes

| Mode | Behavior |
|------|----------|
| **Strict** | Stalls halt execution |
| **Lenient** | Stalls recorded, execution continues |
| **Speculative** | Stalls create branching states |
| **Interactive** | Stalls prompt for resolution |

---

## Project Status

Uypocode is an active research project exploring meaning-based programming.

| Component | Version | Status |
|-----------|---------|--------|
| Master Dictionary | v0.2 | Active development |
| Consciousness Dictionary | v0.1 | Complete |
| Human Dictionary | v0.1 | Complete |
| Life Dictionary | v1.0 | Complete |
| Python Parser | v0.1 | Functional prototype |

---

## Contributing

Uypocode welcomes contributions across:

- **Language Design**: Propose new Relations, Grammar extensions, or semantic patterns
- **Domain Dictionaries**: Model new fields (ethics, aesthetics, physics, etc.)
- **Interpreters**: Implement parsers and runtimes in various languages
- **Documentation**: Examples, tutorials, and theoretical foundations

---

## Philosophy

> *"Some questions are not meant to be answered but to be lived. The stall itself may be the point."*

Uypocode treats unresolved questions not as failures but as **features**. The permanent STALL at the heart of consciousness—how physical processes become subjective experience—doesn't crash the system. It persists, defining the system as much as any resolution would.

This approach extends to all domains:
- **Software**: Incomplete specifications remain pending, not broken
- **Biology**: Evolution as continuous stall resolution
- **Humanity**: Mortality, meaning, free will—stalls we carry throughout life

---

## License

Copyright 2026 Ted A. Human

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

## Acknowledgments

Uypocode emerges from the intersection of programming language theory, cognitive science, philosophy of mind, and systems biology. It owes debts to Lisp's homoiconicity, Prolog's logic programming, Smalltalk's object purity, and the phenomenological tradition's attention to consciousness.

---

<p align="center">
  <strong>Everything is an Object. Every connection is a Relation. What cannot resolve, stalls.</strong>
</p>
