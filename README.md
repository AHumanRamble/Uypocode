# Uypocode Python Parser

A Python implementation of the Uypocode semantic specification language interpreter.

## Overview

Uypocode is a fluid, self-referential framework designed to bridge the gap between human thought processes and machine execution. This Python parser allows you to:

- Define Objects with Labels, Addresses, and Contents
- Create Relations between Objects using the dot operator
- Process datasets using semantic definitions
- Build knowledge graphs that LLMs can reason about

## Installation

Copy the `uypocode` folder to your project, or add it to your Python path:

```bash
cp -r uypocode /path/to/your/project/
```

## Quick Start

### Basic Usage

```python
from uypocode import Interpreter

# Create interpreter
interp = Interpreter()

# Load definitions
interp.load('''
    Dog := (Dog, 1.1, Animal)
    Dog : Sound = "Bark"
    Dog : Legs = 4
''')

# Query
result = interp.eval("Dog.Sound")  # Returns "Bark"
result = interp.eval("Dog.Legs")   # Returns 4
```

### Data Processing

```python
from uypocode import DataInterpreter

# Create data interpreter
interp = DataInterpreter()

# Load schema
interp.load_dictionary('''
    User := (User, 1.1, Entity)
    User : Name = Text
    User : Age = Number
''')

# Load data (JSON, CSV, or Python list)
interp.load_data([
    {"Name": "Alice", "Age": 30},
    {"Name": "Bob", "Age": 25},
], "Users")

# Query
result = interp.query("Users.Length")      # Returns 2
result = interp.query("Users.0.Name")      # Returns "Alice"
result = interp.aggregate("Users", "Age", "Avg")  # Returns 27.5
```

### Built-in Operations

```python
# Arithmetic
interp.eval("5.Add.3")      # 8
interp.eval("10.Mul.2")     # 20
interp.eval("15.Div.3")     # 5.0

# Comparisons
interp.eval("5.Gt.3")       # True
interp.eval("5.Eq.5")       # True

# Text
interp.eval('"Hello".Join." World"')  # "Hello World"
interp.eval('"Hello".Length')         # 5

# Lists
interp.eval("[1, 2, 3].Length")       # 3
interp.eval("[1, 2, 3].First")        # 1
```

## Architecture

```
uypocode/
├── __init__.py          # Package exports
├── core.py              # Object, Address, Dictionary, Context
├── tokenizer.py         # Lexical analysis (Section 5.11)
├── parser.py            # AST construction (Section 5.2)
├── resolver.py          # Dot resolution (Section 5.3)
├── grammar.py           # Control flow operations (Section 3.x)
├── data_interpreter.py  # Dataset processing
└── examples.py          # Usage examples
```

## Core Concepts

### Objects (Section 1.x)
Everything is an Object with three components:
- **Label**: Symbolic name
- **Address**: Location in the Dictionary (e.g., `1.2.3`)
- **Contents**: Data, reference, or logic

### The Dot Operator (Section 2.x)
`A.B` resolves the relationship between A and B:
1. Check if B is a child of A (containment)
2. Check if B is a property of A (metadata)
3. Check for a relation rule
4. Check for grammar operation
5. Stall if unresolved

### Grammar Operations (Section 3.x)
- `Then` / `Else` - Conditionals
- `Cycle` - Iteration
- `Emit` - Output
- `As` - Aliasing
- `Try` / `Must` - Error handling

### Workspace (Section 4.x)
- `Global` (4.1.x) - Persistent scope
- `Local` (4.2.x) - Volatile scope
- Context tracking for pronouns (It, That, Self)

## Running Examples

```bash
python -m uypocode.examples
```

## Specification

See `Uypocode_Master_Dictionary_v0.2.md` for the complete language specification.

## License

MIT License
