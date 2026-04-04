# UypoOS — Uypocode Operating System
## Dictionary v0.1

> *"Every process is an Object. Every command is a relation. The shell is a workspace."*

---

# Preamble

UypoOS is an operating system specification written entirely in Uypocode. It presumes a working
Uypocode parser (v0.3+) and extends the Master Dictionary with five new sections:

| Section | Domain | Mutability |
|---------|--------|------------|
| 5.x | OS Objects — kernel data structures | Structure (immutable) |
| 6.x | OS Relations — system operations | Structure (immutable) |
| 7.x | OS Grammar — shell syntax | Structure (immutable) |
| 8.x | OS Workspace — live session state | Instance (mutable) |
| Appendix A | Shell Command Reference | — |
| Appendix B | Shell Grammar Quick Reference | — |
| Appendix C | Boot Sequence | — |

All kernel Imports from Master Dictionary 0.x are assumed active.
Additional OS-level Imports are declared in Section 5.0.

---

```
Import.Math
Import.Logic
Import.Time
Import.File
Import.English
```

---

# Section 5.0: OS Kernel Extensions

```
Structure OS_Kernel @ 5.0 {
    OS_Kernel := Foundation.Extend
    OS_Kernel : Layer = "Operating_System"
    OS_Kernel : Version = "0.1"
    OS_Kernel : Mode = Strict
}
```

---

## 5.01 Import.Process

Low-level process and thread engine.

```
Structure Process_Engine @ 5.01 {
    Process_Engine := Kernel_Engine
    Process_Engine : Import
    Process_Engine : Default
    Process_Engine : Mode = Strict
}
```

**Provides:**
- PID allocation and recycling
- Context switching
- Stack and heap management per process
- Signal dispatch

---

## 5.02 Import.Memory

Physical and virtual memory management.

```
Structure Memory_Engine @ 5.02 {
    Memory_Engine := Kernel_Engine
    Memory_Engine : Import
    Memory_Engine : Default
    Memory_Engine : Mode = Strict
}
```

**Provides:**
- Allocation: `Memory.Alloc.Size`
- Release: `Memory.Free.Address`
- Virtual mapping: `Memory.Map.(Physical, Virtual, Size)`
- Page fault handling

---

## 5.03 Import.Device

Hardware abstraction layer.

```
Structure Device_Engine @ 5.03 {
    Device_Engine := Kernel_Engine
    Device_Engine : Import
    Device_Engine : Default
    Device_Engine : Mode = Strict
}
```

**Provides:**
- Device enumeration: `Device.List`
- Read/Write: `Device.Name.Read`, `Device.Name.Write.Data`
- Interrupt registration

---

## 5.04 Import.Network

Network I/O primitives.

```
Structure Network_Engine @ 5.04 {
    Network_Engine := Kernel_Engine
    Network_Engine : Import
    Network_Engine : Optional
    Network_Engine : Mode = Strict
}
```

**Provides:**
- Socket creation and binding
- Send/Receive
- DNS resolution: `Network.Resolve.Hostname`

---

## 5.05 OS Kernel Summary

| Address | Label | Description | Mode |
|---------|-------|-------------|------|
| 5.0 | OS_Kernel | OS foundation | Strict |
| 5.01 | Process_Engine | PID/context engine | Strict |
| 5.02 | Memory_Engine | Virtual memory | Strict |
| 5.03 | Device_Engine | Hardware abstraction | Strict |
| 5.04 | Network_Engine | Network I/O | Strict |

---

# Section 5.1: OS Objects

---

## 5.1 Process

A Process is the atomic unit of execution in UypoOS. Every running program is a Process Object.

```
Structure Process @ 5.1 {
    Process := Execution_Unit
    Process : PID = Null              // Assigned by Scheduler on Spawn
    Process : Command = Null          // The .uyo expression or binary being run
    Process : State = "Born"          // Born | Running | Stalled | Sleeping | Zombie | Dead
    Process : Priority = 5           // 1 (highest) to 10 (lowest)
    Process : Owner = Null            // -> User instance
    Process : Parent = Null           // -> Process instance (spawning process)
    Process : Children = []           // List of -> Process instances
    Process : Stdin = Null            // -> Stream instance
    Process : Stdout = Null           // -> Stream instance
    Process : Stderr = Null           // -> Stream instance
    Process : Env = Null              // -> Environment instance
    Process : Exit_Code = Null        // Null until terminated
    Process : Created_At = Null
    Process : Mode = Strict
}
```

**Process States:**

| State | Meaning |
|-------|---------|
| `Born` | Created, not yet scheduled |
| `Running` | Actively executing on CPU |
| `Stalled` | Awaiting resolution (Uypocode stall semantics) |
| `Sleeping` | Waiting on I/O or timer |
| `Zombie` | Terminated, exit code not yet collected |
| `Dead` | Fully cleaned up |

> **Design Note:** *Stalled* directly maps to Uypocode stall semantics. A process whose
> next expression cannot resolve does not crash — it waits. This is a first-class OS state,
> not an error. The Scheduler may re-attempt resolution when context changes.

---

## 5.11 Thread

A Thread is a lightweight execution unit within a Process, sharing its address space.

```
Structure Thread @ 5.11 {
    Thread := Execution_Unit
    Thread : TID = Null               // Thread ID
    Thread : Parent_Process = Null    // -> Process instance
    Thread : State = "Born"
    Thread : Stack_Pointer = Null
    Thread : Program_Counter = Null
    Thread : Mode = Strict
}
```

---

## 5.2 Stream

A Stream is a directed flow of data between processes or devices.

```
Structure Stream @ 5.2 {
    Stream := Data_Channel
    Stream : Direction = Null         // "In" | "Out"
    Stream : Buffer = []              // Queued data
    Stream : Open = True
    Stream : Mode = Strict
}
```

**Standard Streams:**

| Label | Role | Default Connection |
|-------|------|--------------------|
| `Stdin` | Input to process | Keyboard |
| `Stdout` | Primary output | Terminal |
| `Stderr` | Error output | Terminal (distinct) |

---

## 5.3 FileNode

A FileNode is a node in the hierarchical file system. Every path segment is an Object.

```
Structure FileNode @ 5.3 {
    FileNode := Addressable_Resource
    FileNode : Name = Null
    FileNode : Kind = Null            // "File" | "Directory" | "Link" | "Device"
    FileNode : Owner = Null           // -> User
    FileNode : Group = Null           // -> Group
    FileNode : Permissions = Null     // -> Permission instance
    FileNode : Created_At = Null
    FileNode : Modified_At = Null
    FileNode : Size = 0               // Bytes (0 for directories)
    FileNode : Children = []          // Non-empty if Directory
    FileNode : Target = Null          // Non-null if Link
    FileNode : Mode = Strict
}
```

**Path Notation:**

UypoOS uses dot-chain notation for paths, mirroring Uypocode's dot operator.

```
// Absolute path: starts from Root
Root.Home.Lisa.Documents.Report_uyo

// Relative path: starts from CWD (implicit)
Documents.Report_uyo

// Path to parent:
CWD.Up                       // equivalent to "../"

// Mixed:
Root.Bin.uyo                 // /bin/uyo (the parser binary)
```

String paths are also accepted and auto-parsed:

```
"/home/lisa/documents/report.uyo".Path.Resolve    // Returns FileNode
```

---

## 5.31 MountTable

The MountTable maps FileNode roots to physical device locations.

```
Structure MountTable @ 5.31 {
    MountTable := Address_Map
    MountTable : Entries = []         // List of MountEntry
    MountTable : Mode = Strict
}

Structure MountEntry @ 5.31.1 {
    MountEntry := Binding
    MountEntry : Source = Null        // Device or filesystem image
    MountEntry : Target = Null        // -> FileNode (mount point)
    MountEntry : Filesystem = Null    // "UypoFS" | "ext4" | "tmpfs" | ...
    MountEntry : Options = []
    MountEntry : Mode = Strict
}
```

---

## 5.4 Permission

A Permission describes what a User or Group may do to a FileNode or Process.

```
Structure Permission @ 5.4 {
    Permission := Access_Control
    Permission : Read = False
    Permission : Write = False
    Permission : Execute = False
    Permission : Owner_Read = False
    Permission : Owner_Write = False
    Permission : Owner_Execute = False
    Permission : Group_Read = False
    Permission : Group_Write = False
    Permission : Group_Execute = False
    Permission : Mode = Strict
}
```

> **Design Note:** Permission directly mirrors Uypocode's `Mode` guard rail concept:
> `Mode = Strict` on a FileNode means even the parser's English inference layer cannot
> "invent" access. Read/Write/Execute must be explicitly granted.

**Permission Shorthand:**

```
// Octal-style as Uypocode metadata
Perms := Permission.New.(
    Owner_Read = True,
    Owner_Write = True,
    Owner_Execute = True,
    Group_Read = True,
    Execute = False
)
// Equivalent to Unix 750
```

---

## 5.5 User

```
Structure User @ 5.5 {
    User := Principal
    User : UID = Null
    User : Name = Null
    User : Groups = []               // List of -> Group
    User : Home = Null               // -> FileNode
    User : Shell = Null              // -> Process prototype
    User : Mode = Strict
}
```

---

## 5.51 Group

```
Structure Group @ 5.51 {
    Group := Principal_Collection
    Group : GID = Null
    Group : Name = Null
    Group : Members = []
    Group : Mode = Strict
}
```

---

## 5.6 Environment

An Environment is a key-value namespace attached to a Process.
It holds configuration variables visible to that process and its children.

```
Structure Environment @ 5.6 {
    Environment := Variable_Namespace
    Environment : Variables = []      // List of EnvVar
    Environment : Parent = Null       // -> Parent Process Environment (for inheritance)
    Environment : Mode = Guided       // English may infer variable names
    Environment : Inference_Pattern = "Env.Get.*"
}

Structure EnvVar @ 5.61 {
    EnvVar := Binding
    EnvVar : Key = Null
    EnvVar : Value = Null
    EnvVar : Exported = False         // Visible to child processes
    EnvVar : Mode = Strict
}
```

**Usage:**

```
Env.Get."PATH"               // Returns value of PATH variable
Env.Set.("HOME", "/home/lisa")
Env.Unset."TEMP_VAR"
Env.Export."MY_VAR"          // Make visible to child processes
```

---

## 5.7 Signal

A Signal is a named interrupt delivered from one process (or the kernel) to another.

```
Structure Signal @ 5.7 {
    Signal := Interrupt
    Signal : Name = Null
    Signal : Number = Null
    Signal : Default_Action = Null    // "Terminate" | "Ignore" | "Stall" | "Dump" | "Stop"
    Signal : Handler = Null           // -> Logic block (if overridden)
    Signal : Mode = Strict
}
```

**Built-in Signals:**

```
Scope(5.7) {
    SIGTERM := {Name = "Terminate",  Number = 15, Default_Action = "Terminate"},
    SIGKILL := {Name = "Kill",       Number = 9,  Default_Action = "Terminate"},  // Unblockable
    SIGINT  := {Name = "Interrupt",  Number = 2,  Default_Action = "Terminate"},  // Ctrl+C
    SIGSTOP := {Name = "Stop",       Number = 19, Default_Action = "Stall"},      // Ctrl+Z
    SIGCONT := {Name = "Continue",   Number = 18, Default_Action = "Running"},
    SIGHUP  := {Name = "Hangup",     Number = 1,  Default_Action = "Terminate"},
    SIGUSR1 := {Name = "User1",      Number = 10, Default_Action = "Terminate"},  // User-defined
    SIGUSR2 := {Name = "User2",      Number = 12, Default_Action = "Terminate"},  // User-defined
    SIGSTALL := {Name = "Stall",     Number = 99, Default_Action = "Stall"}       // UypoOS-native
}
```

> **SIGSTALL** is unique to UypoOS. When a process's expression cannot resolve,
> the kernel sends SIGSTALL rather than SIGSEGV. The process suspends
> (State = "Stalled") and can be resumed when context resolves.

---

## 5.8 Scheduler

The Scheduler manages which Process runs when.

```
Structure Scheduler @ 5.8 {
    Scheduler := Kernel_Service
    Scheduler : Algorithm = "Stall_Aware_RoundRobin"
    Scheduler : Quantum = 10          // Milliseconds per slice
    Scheduler : Queue_Running = []
    Scheduler : Queue_Stalled = []    // Stalled processes — re-checked each tick
    Scheduler : Queue_Sleeping = []
    Scheduler : Mode = Strict
}
```

**Stall-Aware Scheduling:**

The Scheduler maintains a `Queue_Stalled`. On each tick, it re-attempts resolution
for each stalled process's pending expression. If the expression now resolves,
the process moves back to `Queue_Running`. This makes stall semantics a native
scheduling primitive — the OS does not discard unresolved work.

---

## 5.9 Shell

The Shell is the interactive interface between a User and UypoOS.
It is itself a Process, running a read-eval-emit loop.

```
Structure Shell @ 5.9 {
    Shell := Process
    Shell : Prompt = "uyo> "
    Shell : History = []              // Command history
    Shell : CWD = Null                // -> FileNode (current working directory)
    Shell : Session = Null            // -> Shell_Session instance
    Shell : Mode = Guided             // Shell allows semantic inference for commands
    Shell : Inference_Pattern = "Subject.Command.*"
}
```

---

## 5.91 Shell_Session

```
Structure Shell_Session @ 5.91 {
    Shell_Session := Runtime_Context
    Shell_Session : User = Null
    Shell_Session : Shell = Null
    Shell_Session : Jobs = []         // Background jobs
    Shell_Session : Aliases = []      // Command aliases
    Shell_Session : Functions = []    // User-defined shell functions
    Shell_Session : Mode = Guided
}
```

---

## 5.99 Section 5.x Summary

| Address | Label | Description | Mode |
|---------|-------|-------------|------|
| 5.0 | OS_Kernel | OS foundation | Strict |
| 5.1 | Process | Execution unit | Strict |
| 5.11 | Thread | Lightweight execution | Strict |
| 5.2 | Stream | Data channel | Strict |
| 5.3 | FileNode | File system node | Strict |
| 5.31 | MountTable | Device mount map | Strict |
| 5.4 | Permission | Access control | Strict |
| 5.5 | User | Principal | Strict |
| 5.51 | Group | Principal collection | Strict |
| 5.6 | Environment | Variable namespace | Guided |
| 5.7 | Signal | Process interrupt | Strict |
| 5.8 | Scheduler | Process queue | Strict |
| 5.9 | Shell | Interactive interface | Guided |
| 5.91 | Shell_Session | Live session state | Guided |

---

# Section 6.0: OS Relations

OS Relations govern how Processes, Files, Streams, and Users interact.
All OS Relations live in 6.x and are Structures (immutable).

```
Structure OS_Relation @ 6.0 {
    OS_Relation := Relation.Extend
    OS_Relation : Layer = "Operating_System"
    OS_Relation : Mode = Strict
}
```

---

## 6.1 Process Relations

### 6.11 Spawn

Creates a new child Process from a command or .uyo expression.

```
Structure Spawn @ 6.11 {
    Spawn := {
        Child := Process.New.(
            Command = Argument,
            Parent = Subject,
            Owner = Subject.Owner,
            Env = Subject.Env.Clone,
            Stdin = Stream.New.(Direction = "In"),
            Stdout = Stream.New.(Direction = "Out"),
            Stderr = Stream.New.(Direction = "Out"),
            Created_At = Time.Now
        ).
        PID := Import.Process.Allocate_PID.
        Child.PID = PID.
        Child.State = "Born".
        Scheduler.Queue_Running.Add.Child.
        Child
    }
    Spawn : Binary
    Spawn : Subject : Process
    Spawn : Argument : Text           // Command string or .uyo expression
    Spawn : Mode = Strict
}
```

**Usage:**

```
Shell.Spawn."sort input.txt"
// Returns new Process instance
// Process runs sort, connected to Shell's streams
```

---

### 6.12 Kill

Sends a Signal to a Process.

```
Structure Kill @ 6.12 {
    Kill := {
        Target := Argument.When.[
            Argument.Is.Process : Argument,
            Argument.Is.Number  : Process_Table.Find.Argument,
            Else                : Stall
        ].
        Signal_To_Send := Subject.When.[
            Null    : SIGTERM,
            Else    : Subject
        ].
        Target.Signal_Handler.When.[
            Null : Import.Process.Default_Signal.(Target, Signal_To_Send),
            Else : Target.Signal_Handler.Run.(Signal_To_Send)
        ]
    }
    Kill : Binary
    Kill : Argument : Process | Number    // PID or Process instance
    Kill : Mode = Strict
}
```

**Usage:**

```
SIGTERM.Kill.SomeProcess        // Send SIGTERM to process
SIGKILL.Kill.1234               // Force-kill PID 1234
SIGUSR1.Kill.MyDaemon           // Send custom signal
```

---

### 6.13 Wait

Blocks current Process until a child Process exits, then collects exit code.

```
Structure Wait @ 6.13 {
    Wait := {
        Target := Argument.
        Target.State.Eq."Dead".Not.While.{
            Import.Process.Yield
        }.
        Target.Exit_Code
    }
    Wait : Binary
    Wait : Subject : Process
    Wait : Argument : Process
    Wait : Mode = Strict
}
```

**Usage:**

```
Child := Shell.Spawn."long_task.uyo"
Shell.Wait.Child                // Blocks until Child finishes
Child.Exit_Code.Emit            // Prints exit code
```

---

### 6.14 Fork

Creates an identical copy of the current Process.

```
Structure Fork @ 6.14 {
    Fork := {
        Child := Import.Process.Clone.(Subject).
        Child.PID = Import.Process.Allocate_PID.
        Child.Parent = Subject.
        Subject.Children.Add.Child.
        Child
    }
    Fork : Unary
    Fork : Subject : Process
    Fork : Mode = Strict
}
```

---

### 6.15 Exec

Replaces the current Process's command image with a new one.

```
Structure Exec @ 6.15 {
    Exec := {
        Subject.Command = Argument.
        Import.Process.Reload.(Subject)
    }
    Exec : Binary
    Exec : Subject : Process
    Exec : Argument : Text
    Exec : Mode = Strict
}
```

---

### 6.16 Exit

Terminates a Process with an exit code.

```
Structure Exit @ 6.16 {
    Exit := {
        Subject.Exit_Code = Argument.When.[Null : 0, Else : Argument].
        Subject.State = "Zombie".
        Subject.Parent.Children.Has.Subject.Then.{
            Import.Process.Notify_Parent.(Subject)
        }.
        Import.Process.Cleanup.(Subject)
    }
    Exit : Unary | Binary
    Exit : Subject : Process
    Exit : Argument : Number          // Exit code (0 = success, non-0 = error)
    Exit : Mode = Strict
}
```

---

### 6.17 Async

Spawns a Process in the background — does not block the Shell.

```
Structure Async @ 6.17 {
    Async := {
        Job := Shell.Spawn.Subject.
        Session.Jobs.Add.Job.
        "[".Join.Session.Jobs.Length.Join."] ".Join.Job.PID.Emit.
        Job
    }
    Async : Unary
    Async : Mode = Strict
}
```

**Usage:**

```
"compile_all.uyo".Async        // Runs in background
// Output: [1] 4821            // Job number and PID
```

---

## 6.2 Stream Relations

### 6.21 Pipe

Connects the Stdout of Subject Process to the Stdin of Argument Process.
This is the semantic equivalent of Unix `|`.

```
Structure Pipe @ 6.21 {
    Pipe := {
        Subject.Stdout = Argument.Stdin.
        Subject.Spawn.
        Argument.Spawn.
        Argument
    }
    Pipe : Binary
    Pipe : Subject : Text | Process   // Left-hand command
    Pipe : Argument : Text | Process  // Right-hand command
    Pipe : Mode = Strict
}
```

**Usage:**

```
"ls Root.Home".Pipe."grep .uyo"
// Equivalent to: ls ~ | grep .uyo

"cat log.txt".Pipe."sort".Pipe."uniq"
// Three-stage pipeline
```

> **Design Note:** Because Uypocode's dot operator naturally chains left-to-right,
> pipeline semantics map cleanly. `A.Pipe.B.Pipe.C` reads naturally as
> "A flows into B flows into C" — the same semantic topology as dot-chains.

---

### 6.22 Redirect

Redirects a Stream to a FileNode.

```
Structure Redirect @ 6.22 {
    Redirect := {
        Stream_Target := Argument.When.[
            Argument.Is.FileNode : Argument,
            Argument.Is.Text     : Argument.Path.Resolve,
            Else                 : Stall
        ].
        Subject.When.[
            Subject.Is.Process : Subject.Stdout,
            Subject.Is.Stream  : Subject,
            Else               : Stall
        ].Target.File = Stream_Target
    }
    Redirect : Binary
    Redirect : Mode = Strict
}
```

**Usage:**

```
"ls".Redirect."output.txt"         // Redirect stdout to file (overwrite)
"ls".RedirectAppend."log.txt"      // Append to file
"program".RedirectErr."error.log"  // Redirect stderr
```

---

### 6.23 RedirectAppend

Appends Stdout to a FileNode instead of overwriting.

```
Structure RedirectAppend @ 6.23 {
    RedirectAppend := {
        Target := Argument.Path.Resolve.
        Subject.Stdout.Buffer.Cycle.{
            Target.Data.Join.Item.Into.Target.Data
        }
    }
    RedirectAppend : Binary
    RedirectAppend : Mode = Strict
}
```

---

### 6.24 RedirectErr

Redirects Stderr of Subject Process to a FileNode.

```
Structure RedirectErr @ 6.24 {
    RedirectErr := {
        Target := Argument.Path.Resolve.
        Subject.Stderr.Target = Target
    }
    RedirectErr : Binary
    RedirectErr : Mode = Strict
}
```

---

## 6.3 File System Relations

### 6.31 List

Lists the children of a FileNode (directory contents).

```
Structure List @ 6.31 {
    List := {
        Subject.Kind.Eq."Directory".Then.{
            Subject.Children.Cycle.{
                Item.Name.Emit
            }
        }.Else.{
            "Not a directory: ".Join.Subject.Name.Emit.Stderr
        }
    }
    List : Unary
    List : Subject : FileNode
    List : Mode = Strict
}
```

---

### 6.32 Change

Changes the Shell's current working directory.

```
Structure Change @ 6.32 {
    Change := {
        Target := Argument.When.[
            Argument.Is.FileNode : Argument,
            Argument.Is.Text     : Argument.Path.Resolve,
            Else                 : Stall
        ].
        Target.Kind.Eq."Directory".Must."Not a directory".
        Shell.CWD = Target
    }
    Change : Binary
    Change : Subject : Shell
    Change : Mode = Strict
}
```

---

### 6.33 Make

Creates a new FileNode (file or directory).

```
Structure Make @ 6.33 {
    Make := {
        New_Node := FileNode.New.(
            Name = Argument,
            Kind = Subject.When.[
                "dir"  : "Directory",
                "file" : "File",
                Else   : "File"
            ],
            Owner = Session.User,
            Created_At = Time.Now,
            Permissions = Permission.New.(
                Owner_Read = True,
                Owner_Write = True,
                Group_Read = True
            )
        ).
        Shell.CWD.Children.Add.New_Node.
        New_Node
    }
    Make : Binary
    Make : Mode = Strict
}
```

---

### 6.34 Remove

Deletes a FileNode.

```
Structure Remove @ 6.34 {
    Remove := {
        Target := Argument.Path.Resolve.
        Session.User.Can.Write.Target.Must."Permission denied".
        Target.Kind.Eq."Directory".Then.{
            Subject.Has."Recursive".Then.{
                Target.Children.Cycle.{Remove.Run.Item}
            }.Else.{
                Target.Children.Length.Gt.0.Then.{
                    "Directory not empty. Use Remove.Recursive".Emit.Stderr.
                    Exit.1
                }
            }
        }.
        Target.Parent.Children.Remove.Target.
        Target = Null
    }
    Remove : Binary
    Remove : Mode = Strict
}
```

---

### 6.35 Copy

Copies a FileNode to a new location.

```
Structure Copy @ 6.35 {
    Copy := {
        Source := Subject.Path.Resolve.
        Destination := Argument.Path.Resolve.
        New_Node := Source.Clone.
        New_Node.Name = Destination.Name.
        Destination.Children.Add.New_Node
    }
    Copy : Binary
    Copy : Mode = Strict
}
```

---

### 6.36 Move

Moves (renames) a FileNode.

```
Structure Move @ 6.36 {
    Move := {
        Source := Subject.Path.Resolve.
        Destination := Argument.Path.Resolve.
        Source.Parent.Children.Remove.Source.
        Source.Name = Destination.Name.
        Destination.Parent.Children.Add.Source
    }
    Move : Binary
    Move : Mode = Strict
}
```

---

### 6.37 Read

Reads the contents of a file into a Text value.

```
Structure Read @ 6.37 {
    Read := {
        Node := Subject.When.[
            Subject.Is.FileNode : Subject,
            Subject.Is.Text     : Subject.Path.Resolve,
            Else                : Stall
        ].
        Node.Kind.Eq."File".Must."Not a file: ".Join.Node.Name.
        Session.User.Can.Read.Node.Must."Permission denied".
        Import.File.Read.Node.Path
    }
    Read : Unary
    Read : Mode = Strict
}
```

---

### 6.38 Write

Writes data to a FileNode.

```
Structure Write @ 6.38 {
    Write := {
        Node := Subject.When.[
            Subject.Is.FileNode : Subject,
            Subject.Is.Text     : Subject.Path.Resolve,
            Else                : Stall
        ].
        Session.User.Can.Write.Node.Must."Permission denied".
        Import.File.Write.(Node.Path, Argument)
    }
    Write : Binary
    Write : Mode = Strict
}
```

---

## 6.4 Environment Relations

### 6.41 Get

Retrieves an environment variable.

```
Structure Get @ 6.41 {
    Get := {
        Subject.Variables.Cycle.{
            Item.Key.Eq.Argument.Then.Item.Value.Yield
        }.
        // If not found, check parent environment
        Subject.Parent.Then.{Subject.Parent.Get.Argument}.Else.Null
    }
    Get : Binary
    Get : Subject : Environment
    Get : Argument : Text
    Get : Mode = Strict
}
```

---

### 6.42 Set

Sets an environment variable.

```
Structure Set @ 6.42 {
    Set := {
        Key := Argument.0.
        Value := Argument.1.
        Existing := Subject.Variables.Cycle.{
            Item.Key.Eq.Key.Then.Item.Yield
        }.
        Existing.Then.{
            Existing.Value = Value
        }.Else.{
            New_Var := EnvVar.New.(Key = Key, Value = Value).
            Subject.Variables.Add.New_Var
        }
    }
    Set : Binary
    Set : Subject : Environment
    Set : Argument : List             // [Key, Value]
    Set : Mode = Strict
}
```

---

### 6.43 Export

Marks an environment variable for inheritance by child processes.

```
Structure Export @ 6.43 {
    Export := {
        Var := Subject.Variables.Cycle.{
            Item.Key.Eq.Argument.Then.Item.Yield
        }.
        Var.Then.{Var.Exported = True}.Else.{
            "Variable not found: ".Join.Argument.Emit.Stderr
        }
    }
    Export : Binary
    Export : Subject : Environment
    Export : Argument : Text
    Export : Mode = Strict
}
```

---

## 6.5 User Relations

### 6.51 Can

Tests whether a User has a specific Permission on a FileNode.

```
Structure Can @ 6.51 {
    Can := {
        Node := Argument.1.
        Action := Argument.0.
        Is_Owner := Node.Owner.Identical.Subject.
        Is_Group := Subject.Groups.Has.Node.Group.

        Is_Owner.Then.{
            Node.Permissions.When.[
                "Read"    : Node.Permissions.Owner_Read,
                "Write"   : Node.Permissions.Owner_Write,
                "Execute" : Node.Permissions.Owner_Execute,
                Else      : False
            ]
        }.Else.Is_Group.Then.{
            Node.Permissions.When.[
                "Read"    : Node.Permissions.Group_Read,
                "Write"   : Node.Permissions.Group_Write,
                "Execute" : Node.Permissions.Group_Execute,
                Else      : False
            ]
        }.Else.{
            Node.Permissions.When.[
                "Read"    : Node.Permissions.Read,
                "Write"   : Node.Permissions.Write,
                "Execute" : Node.Permissions.Execute,
                Else      : False
            ]
        }
    }
    Can : Binary
    Can : Subject : User
    Can : Argument : List             // ["Read"|"Write"|"Execute", FileNode]
    Can : Mode = Strict
}
```

---

## 6.6 Mount Relations

### 6.61 Mount

Attaches a filesystem to a directory in the namespace.

```
Structure Mount @ 6.61 {
    Mount := {
        Entry := MountEntry.New.(
            Source = Subject,
            Target = Argument,
            Filesystem = "UypoFS",
            Options = []
        ).
        MountTable.Entries.Add.Entry.
        Argument.Children = Import.File.Load_Root.(Subject)
    }
    Mount : Binary
    Mount : Subject : Text            // Device or image path
    Mount : Argument : FileNode       // Mount point directory
    Mount : Mode = Strict
}
```

---

### 6.62 Unmount

Detaches a filesystem.

```
Structure Unmount @ 6.62 {
    Unmount := {
        Entry := MountTable.Entries.Cycle.{
            Item.Target.Identical.Subject.Then.Item.Yield
        }.
        Entry.Then.{
            MountTable.Entries.Remove.Entry.
            Subject.Children = []
        }.Else.{
            "No mount at: ".Join.Subject.Name.Emit.Stderr
        }
    }
    Unmount : Unary
    Unmount : Subject : FileNode
    Unmount : Mode = Strict
}
```

---

## 6.7 Scheduler Relations

### 6.71 Schedule

Adds a Process to the Scheduler's run queue.

```
Structure Schedule @ 6.71 {
    Schedule := {
        Subject.State = "Running".
        Scheduler.Queue_Running.Add.Subject
    }
    Schedule : Unary
    Schedule : Subject : Process
    Schedule : Mode = Strict
}
```

---

### 6.72 Preempt

Moves the current Process out of the run queue for re-scheduling.

```
Structure Preempt @ 6.72 {
    Preempt := {
        Scheduler.Queue_Running.Remove.Subject.
        Scheduler.Queue_Running.Add.Subject    // Move to end (round-robin)
    }
    Preempt : Unary
    Preempt : Subject : Process
    Preempt : Mode = Strict
}
```

---

## 6.99 Section 6.x Summary

| Address | Label | Description |
|---------|-------|-------------|
| 6.11 | Spawn | Create child process |
| 6.12 | Kill | Send signal to process |
| 6.13 | Wait | Block until child exits |
| 6.14 | Fork | Clone current process |
| 6.15 | Exec | Replace process image |
| 6.16 | Exit | Terminate process |
| 6.17 | Async | Run process in background |
| 6.21 | Pipe | Connect process streams |
| 6.22 | Redirect | Stream to file |
| 6.23 | RedirectAppend | Append stream to file |
| 6.24 | RedirectErr | Redirect stderr |
| 6.31 | List | Directory listing |
| 6.32 | Change | Change directory |
| 6.33 | Make | Create file or directory |
| 6.34 | Remove | Delete file node |
| 6.35 | Copy | Copy file node |
| 6.36 | Move | Move/rename file node |
| 6.37 | Read | Read file contents |
| 6.38 | Write | Write file contents |
| 6.41 | Get | Get env variable |
| 6.42 | Set | Set env variable |
| 6.43 | Export | Export variable to children |
| 6.51 | Can | Permission check |
| 6.61 | Mount | Mount filesystem |
| 6.62 | Unmount | Unmount filesystem |
| 6.71 | Schedule | Add to run queue |
| 6.72 | Preempt | Yield CPU |

---

# Section 7.0: OS Grammar

OS Grammar extends 3.x with shell-specific control structures.
These are built-in operations the shell recognises on any Subject.

```
Structure OS_Grammar @ 7.0 {
    OS_Grammar := Grammar.Extend
    OS_Grammar : Layer = "Shell"
    OS_Grammar : Mode = Strict
}
```

---

## 7.1 Run (Execute a .uyo file)

Loads and evaluates a .uyo script file in the current session.

```
Structure Run @ 7.1 {
    Run := {
        Node := Subject.When.[
            Subject.Is.FileNode : Subject,
            Subject.Is.Text     : Subject.Path.Resolve,
            Else                : Stall
        ].
        Node.Name.Has.".uyo".Must."Expected .uyo file".
        Source := Node.Read.
        Import.Parser.Evaluate.(Source, Session.Env)
    }
    Run : Unary
    Run : Mode = Strict
}
```

**Usage:**

```
"scripts/deploy.uyo".Run
Root.Home.Lisa.Scripts.Deploy_uyo.Run
```

---

## 7.2 Source (Run in Current Shell)

Like Run, but executes in the current shell's own namespace (affects CWD, Env, etc).

```
Structure Source @ 7.2 {
    Source := {
        Node := Subject.Path.Resolve.
        Source_Text := Node.Read.
        Import.Parser.Evaluate.(Source_Text, Shell.Session)
    }
    Source : Unary
    Source : Mode = Strict
}
```

---

## 7.3 Alias

Creates a short label for a longer expression.

```
Structure Alias @ 7.3 {
    Alias := {
        New_Alias := Binding.New.(Key = Subject, Value = Argument).
        Session.Aliases.Add.New_Alias
    }
    Alias : Binary
    Alias : Subject : Text    // Short label
    Alias : Argument : Text   // Full expression
    Alias : Mode = Strict
}
```

**Usage:**

```
"ll".Alias."Shell.List.Verbose"
"home".Alias."Shell.Change.Root.Home"
```

---

## 7.4 Which

Resolves a command label to its source FileNode.

```
Structure Which @ 7.4 {
    Which := {
        // Check aliases first
        Alias_Match := Session.Aliases.Cycle.{
            Item.Key.Eq.Subject.Then.Item.Value.Yield
        }.
        Alias_Match.Then.{
            "alias: ".Join.Alias_Match.Emit.
            Alias_Match.Yield
        }.

        // Search PATH
        Path_Dirs := Shell.Env.Get."PATH".Split.":".
        Path_Dirs.Cycle.{
            Candidate := Item.Path.Resolve.Children.Cycle.{
                Inner.Name.Eq.Subject.Then.Inner.Yield
            }.
            Candidate.Then.{Candidate.Yield}
        }.
        "Not found: ".Join.Subject.Emit.Stderr
    }
    Which : Unary
    Which : Mode = Strict
}
```

---

## 7.5 Help

Outputs the metadata of any OS Object or Relation.

```
Structure Help @ 7.5 {
    Help := {
        Target := Subject.
        "--- Help: ".Join.Target.Label.Join." ---".Emit.
        Target.Metadata.Cycle.{
            Item.Key.Join.": ".Join.Item.Value.Emit
        }
    }
    Help : Unary
    Help : Mode = Open    // Can infer from English labels
}
```

**Usage:**

```
Spawn.Help        // Prints Spawn's metadata
Process.Help      // Prints Process structure
```

---

## 7.6 History

Emits or searches the Shell's command history.

```
Structure History @ 7.6 {
    History := {
        Argument.Then.{
            // Filter by argument
            Shell.History.Cycle.{
                Item.Has.Argument.Then.{
                    Index.Join."  ".Join.Item.Emit
                }
            }
        }.Else.{
            Shell.History.Cycle.{
                Index.Join."  ".Join.Item.Emit
            }
        }
    }
    History : Unary | Binary
    History : Mode = Strict
}
```

---

## 7.7 Jobs

Lists background jobs in the current session.

```
Structure Jobs @ 7.7 {
    Jobs := {
        Session.Jobs.Cycle.{
            "[".Join.Index.Join."] ".
            Join.Item.State.Join."  ".
            Join.Item.PID.Join."  ".
            Join.Item.Command.Emit
        }
    }
    Jobs : Unary
    Jobs : Mode = Strict
}
```

---

## 7.8 Fg / Bg

Bring a background job to foreground (`Fg`) or send a foreground job to background (`Bg`).

```
Structure Fg @ 7.8 {
    Fg := {
        Job := Session.Jobs.At.Argument.
        Job.Stdout = Shell.Stdout.
        Job.State = "Running"
    }
    Fg : Binary
    Fg : Argument : Number    // Job number from Jobs list
    Fg : Mode = Strict
}

Structure Bg @ 7.81 {
    Bg := {
        Job := Session.Jobs.At.Argument.
        Job.Stdout = Stream.New.(Direction = "Out").
        Job.State = "Running"
    }
    Bg : Binary
    Bg : Argument : Number
    Bg : Mode = Strict
}
```

---

## 7.9 Stalls (View Pending Expressions)

UypoOS-native: shows all expressions that have stalled in the current session.

```
Structure Stalls @ 7.9 {
    Stalls := {
        "--- Stalled Expressions ---".Emit.
        Scheduler.Queue_Stalled.Cycle.{
            "[PID ".Join.Item.PID.Join."] ".
            Join.Item.Command.Join.
            "  -->  ".Join.Item.Stall_Expression.Emit
        }.
        Scheduler.Queue_Stalled.Length.Eq.0.Then.{
            "No stalled expressions.".Emit
        }
    }
    Stalls : Unary
    Stalls : Mode = Strict
}
```

**Usage:**

```
Stalls
// --- Stalled Expressions ---
// [PID 1042] analyze.uyo  -->  Galaxy.DarkMatter.Mass
// [PID 1099] sim.uyo       -->  Qubit.Collapse.Basis
```

---

## 7.99 Section 7.x Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.1 | Run | Execute .uyo file |
| 7.2 | Source | Run in current shell |
| 7.3 | Alias | Shorthand binding |
| 7.4 | Which | Find command |
| 7.5 | Help | Object documentation |
| 7.6 | History | Command history |
| 7.7 | Jobs | Background job list |
| 7.8 | Fg | Foreground a job |
| 7.81 | Bg | Background a job |
| 7.9 | Stalls | View pending expressions |

---

# Section 8.0: OS Workspace (Runtime Shell Session)

The Workspace is the live state of UypoOS at runtime. All runtime instances live in 8.x.
This mirrors the Master Dictionary's 4.x Workspace but scoped to the OS layer.

```
Structure OS_Workspace @ 8.0 {
    OS_Workspace := Workspace.Extend
    OS_Workspace : Layer = "OS_Runtime"
    OS_Workspace : Mode = Strict
}
```

---

## 8.1 Boot

The Boot sequence instantiates all global OS Workspace objects.

```
// Boot sequence — runs at OS startup
// Instantiated in 8.x Workspace

// --- Core Systems ---
Process_Table := [].           // @ 8.1.1  All active processes
MountTable    := MountTable.New.  // @ 8.1.2
Scheduler     := Scheduler.New.   // @ 8.1.3
Device_Registry := [].         // @ 8.1.4

// --- Root Filesystem ---
Root := FileNode.New.(Name = "Root", Kind = "Directory").   // @ 8.1.5
"/dev/disk0".Mount.Root.

// --- Standard Users ---
Root_User := User.New.(UID = 0, Name = "root", Home = Root.Root_User).  // @ 8.1.6
Nobody    := User.New.(UID = 65534, Name = "nobody").

// --- Initial Process (PID 1: init) ---
Init := Process.New.(
    PID = 1,
    Command = "init.uyo",
    Owner = Root_User,
    State = "Running"
).                             // @ 8.1.7
Process_Table.Add.Init.
```

---

## 8.2 Shell Session

When a user logs in, a Shell Session is created:

```
// @ 8.2.x — created fresh per login

Lisa := User.New.(
    UID = 1000,
    Name = "lisa",
    Home = Root.Home.Lisa,
    Groups = [Group.New.(GID = 1000, Name = "lisa")]
).

Lisa_Env := Environment.New.(
    Variables = [
        EnvVar.New.(Key = "HOME",  Value = "/home/lisa", Exported = True),
        EnvVar.New.(Key = "PATH",  Value = "/bin:/usr/bin:/home/lisa/bin", Exported = True),
        EnvVar.New.(Key = "SHELL", Value = "/bin/uyo",   Exported = True),
        EnvVar.New.(Key = "TERM",  Value = "uyoterm",    Exported = True),
        EnvVar.New.(Key = "USER",  Value = "lisa",       Exported = True)
    ]
).

Lisa_Session := Shell_Session.New.(
    User = Lisa,
    Jobs = [],
    Aliases = [],
    Functions = []
).

Lisa_Shell := Shell.New.(
    PID = Import.Process.Allocate_PID,
    Owner = Lisa,
    Env = Lisa_Env,
    Session = Lisa_Session,
    CWD = Root.Home.Lisa,
    State = "Running"
).

Process_Table.Add.Lisa_Shell.
```

---

## 8.3 Read-Eval-Emit Loop (REEL)

The Shell's core loop. Named REEL to reflect Uypocode's `Emit` output model.

```
// REEL — the Shell's main loop
// This is a Logic block executing in Lisa_Shell's context

Shell.Running := True.

Shell.Running.While.{

    // 1. Prompt
    Shell.Prompt.Emit.

    // 2. Read
    Line := "".Prompt.Input.    // Displays prompt, captures line

    // 3. Record in history
    Line.Length.Gt.0.Then.{
        Shell.History.Add.Line
    }.

    // 4. Tokenize and check for special shell syntax
    Tokens := Import.Parser.Tokenize.Line.

    // 5. Handle built-in shell keywords
    Tokens.First.When.[

        "exit"   : {Shell.Exit.Tokens.At.1.Try.0},
        "cd"     : {Shell.Change.Tokens.At.1},
        "ls"     : {Shell.CWD.List},
        "pwd"    : {Shell.CWD.Path.Emit},
        "echo"   : {Tokens.Rest.Join." ".Emit},
        "env"    : {Shell.Env.Variables.Cycle.{Item.Key.Join."=".Join.Item.Value.Emit}},
        "export" : {Shell.Env.Export.Tokens.At.1},
        "alias"  : {Tokens.At.1.Alias.Tokens.At.2},
        "jobs"   : {Jobs},
        "fg"     : {Tokens.At.1.Fg},
        "bg"     : {Tokens.At.1.Bg},
        "stalls" : {Stalls},
        "help"   : {Tokens.At.1.Help},
        "which"  : {Tokens.At.1.Which},
        "history": {History},

        Else : {
            // 6. Parse as Uypocode expression
            Expr := Import.Parser.Parse.Line.

            // 7. Check for pipe, redirect, async operators
            Expr.Has.Async.Then.{
                Expr.Strip.Async.Async
            }.Else.Expr.Has.Pipe.Then.{
                Import.Parser.Build_Pipeline.Expr
            }.Else.Expr.Has.Redirect.Then.{
                Import.Parser.Build_Redirect.Expr
            }.Else.{
                // 8. Evaluate directly
                Result := Import.Parser.Evaluate.(Expr, Lisa_Session).
                Result.Is.Null.Not.Then.{Result.Emit}
            }
        }
    ]
}
```

---

# Appendix A: Shell Command Reference

All commands are valid Uypocode expressions at the shell prompt (`uyo> `).

---

## A.1 Navigation

| Command | Example | Description |
|---------|---------|-------------|
| `cd` | `cd Home.Projects` | Change directory |
| `ls` | `ls` | List current directory |
| `ls path` | `ls Root.Bin` | List given directory |
| `pwd` | `pwd` | Print working directory |
| `ls.Verbose` | `ls.Verbose` | Long-format listing with permissions |

---

## A.2 File Operations

| Command | Example | Description |
|---------|---------|-------------|
| `make file Name` | `"file".Make."notes.uyo"` | Create file |
| `make dir Name` | `"dir".Make."Projects"` | Create directory |
| `rm Path` | `"notes.uyo".Remove` | Delete file |
| `rm.Recursive Dir` | `"dir".Remove.Recursive."old_proj"` | Delete directory recursively |
| `cp Src Dst` | `"a.uyo".Copy."backup.uyo"` | Copy file |
| `mv Src Dst` | `"old.uyo".Move."new.uyo"` | Move or rename |
| `cat File` | `"readme.uyo".Read.Emit` | Print file contents |
| `echo Text > File` | `"hello".Redirect."out.txt"` | Write to file |
| `echo Text >> File` | `"more".RedirectAppend."out.txt"` | Append to file |

---

## A.3 Process Management

| Command | Example | Description |
|---------|---------|-------------|
| `run File` | `"script.uyo".Run` | Execute a .uyo file |
| `cmd &` | `"long.uyo".Async` | Run in background |
| `kill PID` | `SIGTERM.Kill.1234` | Send signal to process |
| `kill -9 PID` | `SIGKILL.Kill.1234` | Force kill |
| `wait PID` | `Shell.Wait.Child` | Wait for process |
| `jobs` | `Jobs` | List background jobs |
| `fg N` | `N.Fg` | Bring job N to foreground |
| `bg N` | `N.Bg` | Send job N to background |
| `ps` | `Process_Table.Cycle.{Item.PID.Join." ".Join.Item.Command.Join." ".Join.Item.State.Emit}` | List processes |
| `exit N` | `Shell.Exit.N` | Exit shell with code N |

---

## A.4 I/O and Pipelines

| Syntax | Meaning |
|--------|---------|
| `A.Pipe.B` | Pipe A's stdout to B's stdin |
| `A.Redirect."file"` | Redirect A's stdout to file (overwrite) |
| `A.RedirectAppend."file"` | Append A's stdout to file |
| `A.RedirectErr."file"` | Redirect stderr to file |
| `A.Pipe.B.Redirect."file"` | Pipeline with final redirect |

**Pipeline example:**

```
"cat access.log".Pipe."grep ERROR".Pipe."sort".Pipe."uniq".Redirect."errors.txt"
```

---

## A.5 Variables and Environment

| Command | Example | Description |
|---------|---------|-------------|
| `Name = Value` | `X = 42` | Set workspace variable |
| `Env.Get."KEY"` | `Env.Get."HOME".Emit` | Read env variable |
| `Env.Set.["KEY","VAL"]` | `Env.Set.["DEBUG","1"]` | Set env variable |
| `export KEY` | `Shell.Env.Export."MY_VAR"` | Export to children |
| `env` | `env` | Print all env variables |
| `Env.Unset."KEY"` | `Env.Unset."TEMP"` | Remove env variable |

---

## A.6 Shell Utilities

| Command | Example | Description |
|---------|---------|-------------|
| `alias short long` | `"ll".Alias."ls.Verbose"` | Create alias |
| `which cmd` | `"sort".Which` | Find command location |
| `help Object` | `Spawn.Help` | Show object/relation docs |
| `history` | `History` | Show command history |
| `history filter` | `History."uyo"` | Filter history |
| `source file` | `"profile.uyo".Source` | Run file in current shell |
| `stalls` | `Stalls` | Show stalled expressions |

---

## A.7 Permissions

| Command | Example | Description |
|---------|---------|-------------|
| `chmod Node Perm` | `"file.uyo".Chmod.750` | Change permissions (octal) |
| `chown Node User` | `"file.uyo".Chown.Lisa` | Change owner |
| `can Read Node` | `Session.User.Can.["Read", Node]` | Permission test |

---

## A.8 Filesystem

| Command | Example | Description |
|---------|---------|-------------|
| `mount dev dir` | `"/dev/disk1".Mount.Root.Mnt` | Mount filesystem |
| `umount dir` | `Root.Mnt.Unmount` | Unmount filesystem |

---

# Appendix B: Shell Grammar Quick Reference

The UypoOS shell reads every line as a Uypocode expression.
The following table maps familiar shell idioms to their Uypocode equivalents.

| Unix Shell | UypoOS Shell | Notes |
|------------|--------------|-------|
| `ls -la` | `CWD.List.Verbose` | Flags become chained metadata |
| `cat f \| grep x` | `"cat f".Pipe."grep x"` | Pipe is a Relation |
| `echo hi > out` | `"hi".Redirect."out"` | Redirect is a Relation |
| `echo hi >> out` | `"hi".RedirectAppend."out"` | Append variant |
| `./script.uyo` | `"script.uyo".Run` | Execution is a Relation |
| `export X=val` | `Env.Set.["X","val"]. Env.Export."X"` | Two-step export |
| `kill -15 PID` | `SIGTERM.Kill.PID` | Signal is the Subject |
| `cmd &` | `"cmd".Async` | Async is a Grammar op |
| `fg %1` | `1.Fg` | Job number as argument |
| `source .profile` | `".profile".Source` | Source keeps shell context |
| `help` | `Help` | Built-in documentation |
| *(no equivalent)* | `Stalls` | View pending expressions |

---

# Appendix C: Boot Sequence

The full UypoOS boot sequence in Uypocode.

```
// ============================================================
// UypoOS v0.1 — Boot Sequence
// File: boot.uyo
// ============================================================

Import.Math
Import.Logic
Import.Time
Import.File
Import.Process
Import.Memory
Import.Device
Import.Network

"UypoOS v0.1 booting...".Emit

// --- Phase 1: Mount Root Filesystem ---
"[BOOT] Mounting root filesystem".Emit.
Root := FileNode.New.(Name = "Root", Kind = "Directory").
"/dev/disk0".Mount.Root.
"[BOOT] Root mounted at /".Emit.

// --- Phase 2: Build Standard Directory Tree ---
"[BOOT] Creating standard directories".Emit.
Scope(Root) {
    Bin  := FileNode.New.(Name = "Bin",  Kind = "Directory"),
    Etc  := FileNode.New.(Name = "Etc",  Kind = "Directory"),
    Home := FileNode.New.(Name = "Home", Kind = "Directory"),
    Tmp  := FileNode.New.(Name = "Tmp",  Kind = "Directory"),
    Var  := FileNode.New.(Name = "Var",  Kind = "Directory"),
    Dev  := FileNode.New.(Name = "Dev",  Kind = "Directory"),
    Proc := FileNode.New.(Name = "Proc", Kind = "Directory")
}

// --- Phase 3: Start Scheduler ---
"[BOOT] Starting Scheduler".Emit.
Scheduler := Scheduler.New.(Algorithm = "Stall_Aware_RoundRobin").

// --- Phase 4: Create Root User ---
"[BOOT] Creating root user".Emit.
Root_User := User.New.(
    UID = 0,
    Name = "root",
    Home = Root.Home,
    Shell = "/bin/uyo"
).

// --- Phase 5: Start Init Process ---
"[BOOT] Starting init (PID 1)".Emit.
Init := Process.New.(
    PID = 1,
    Command = "init.uyo",
    Owner = Root_User,
    State = "Running",
    Created_At = Time.Now
).
Process_Table := [Init].

// --- Phase 6: Load Device Registry ---
"[BOOT] Enumerating devices".Emit.
Device_Registry := Import.Device.Enumerate.

// --- Phase 7: Mount /proc (Process information filesystem) ---
"proc".Mount.Root.Proc.

// --- Phase 8: Start Login Manager ---
"[BOOT] Starting login manager".Emit.
Login_Manager := Process.New.(
    PID = Import.Process.Allocate_PID,
    Command = "login.uyo",
    Owner = Root_User,
    State = "Running"
).
Process_Table.Add.Login_Manager.

"[BOOT] UypoOS ready.".Emit.

// --- Phase 9: Await User Login ---
Login_Manager.Running := True.
Login_Manager.Running.While.{
    "login: ".Prompt.Username.
    "password: ".Prompt.Password.
    Authenticated := Import.Process.Authenticate.(Username, Password).
    Authenticated.Then.{
        New_User := User.Load.Username.
        New_Shell := Shell.New.(
            PID = Import.Process.Allocate_PID,
            Owner = New_User,
            CWD = New_User.Home,
            State = "Running"
        ).
        Process_Table.Add.New_Shell.
        New_Shell.REEL.Run        // Start interactive shell
    }.Else.{
        "Login failed.".Emit.
        3.Times.{
            Import.Process.Sleep.1000    // Delay on failure
        }
    }
}
```

---

# Appendix D: Example Shell Session

```
// Startup
UypoOS v0.1
login: lisa
password: ••••••

Welcome, lisa. 14 stalled expressions loaded from last session.

uyo> pwd
/home/lisa

uyo> ls
Documents  Projects  Scripts  profile.uyo

uyo> cd Projects

uyo> ls
mind_model  semantics_engine  bio_sim

uyo> "analyze.uyo".Run
[Running analyze.uyo]
...
[STALL] Galaxy.DarkMatter.Mass — no resolution found
[STALL] Qubit.Collapse.Basis  — no resolution found
Completed with 2 stalled expressions.

uyo> Stalls
--- Stalled Expressions ---
[PID 1042] analyze.uyo  -->  Galaxy.DarkMatter.Mass
[PID 1043] analyze.uyo  -->  Qubit.Collapse.Basis

uyo> Galaxy.DarkMatter.Mass = 2.3e42    // User resolves the stall

uyo> Stalls
--- Stalled Expressions ---
[PID 1043] analyze.uyo  -->  Qubit.Collapse.Basis
// PID 1042 resumed automatically when context resolved

uyo> "sort output.txt".Pipe."uniq".Redirect."sorted.txt"
uyo> "sorted.txt".Read.Emit
alpha
beta
gamma

uyo> "compile.uyo".Async
[1] 4821

uyo> Jobs
[0] Running  4821  compile.uyo

uyo> 0.Fg
// compile.uyo now in foreground

uyo> SIGTERM.Kill.4821
// Sends SIGTERM — compile.uyo may handle gracefully

uyo> Shell.Exit.0
Goodbye, lisa.
```

---

# Appendix E: UypoOS Design Principles

**1. Everything is an Object.**
Processes, files, streams, permissions, signals — all are Uypocode Objects with
`(Label, Address, Contents)`. The OS is just a particularly live dictionary.

**2. Stall semantics are first-class.**
A process that cannot resolve its next expression does not panic or crash.
It suspends as `Stalled` and the Scheduler re-attempts it when context changes.
Unresolved work is precious, not an error.

**3. The dot operator is the universal connector.**
Shell pipelines, file paths, method calls, property access, and signal dispatch
all use the dot. Learning Uypocode means learning the OS interface.

**4. Mode governs access.**
Uypocode's `Mode = Strict / Guided / Open` semantic inference guard extends
naturally to permissions. FileNodes marked `Mode = Strict` refuse inference-based
access — permissions must be explicit.

**5. The Structure/Instance boundary is the kernel/user-space boundary.**
Kernel objects (0.x–7.x) are Structures: immutable, protected.
User processes live in 8.x Workspace: mutable, created from kernel Structures via `.New`.

**6. Semantic inference is available but bounded.**
The Shell operates at `Mode = Guided`, so partial commands can be inferred.
Typing `"sort"` without arguments may prompt: *"Did you mean: sort Stdin?"*
Typing `"rm -rf /"` will stall — Remove.Recursive requires explicit confirmation.

---

*End of UypoOS Dictionary v0.1*
