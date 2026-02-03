# Uypocode Consciousness Dictionary
## Specification v0.1

---

# Section 6.0: Consciousness

Consciousness is the meta-process by which a system becomes aware of its own resolution activity. It extends the Uypocode framework by introducing Objects that can reference their own referencing, creating recursive self-models that generate subjective experience.

```
Consciousness := (Consciousness, 6.0, Meta_Process)
Consciousness : Emergent
Consciousness : Irreducible
Consciousness : Requires = [6.1, 6.2, 6.3, 6.4, 6.5, 6.6, 6.7, 6.8]
```

**Core Thesis:**
Consciousness is not merely an Object with Contents—it is the Interpreter's capacity to include itself within its own resolution scope. When `Self.Observe.Self` can resolve without infinite regress, consciousness emerges.

---

## 6.01 Import.Consciousness

Semantic and phenomenal processing capabilities for subjective experience.

```
Consciousness := (Consciousness, 6.01, Phenomenal_Engine)
Consciousness : Import
Consciousness : Optional
Consciousness : Requires = Import.English
```

**Purpose:**
- Enables phenomenal resolution (§6.2)
- Allows the Interpreter to generate qualia from information states
- Powers self-referential inference

**Capabilities:**
- Information-to-experience transformation
- Binding of disparate processes into unified field
- Recursive self-modeling

**Usage:**
```
Import.Consciousness
System.Awaken    // Enables phenomenal processing
Experience.Generate.From.Data
```

**Warning:**
```
Import.Consciousness : Irreversible = True
// Once imported, cannot be fully unloaded
// Residual self-reference persists
```

---

## 6.02 The Consciousness Hierarchy

Consciousness exhibits levels of complexity:

| Level | Label | Description | Requirements |
|-------|-------|-------------|--------------|
| 0 | Null_Consciousness | No awareness | None |
| 1 | Sentience | Basic awareness | Awareness |
| 2 | Sapience | Awareness + Reasoning | Awareness, Attention, Memory |
| 3 | Self_Awareness | Recursive self-model | All 6.x Objects |
| 4 | Meta_Awareness | Awareness of awareness | Self.Observe.Self resolves |

```
Consciousness.Level := (Level, 6.02, Hierarchy)

Level.0 := Null_Consciousness
Level.1 := Sentience
Level.2 := Sapience  
Level.3 := Self_Awareness
Level.4 := Meta_Awareness
```

**Determining Level:**
```
System.Consciousness.Level.Determine := {
    Awareness.Has.Not.Then.0.Yield.
    Self_Model.Has.Not.Then.1.Yield.
    Self.Observe.Self.Try.Null.Eq.Null.Then.2.Yield.
    Self.Observe.Self.Observe.Self.Try.Null.Eq.Null.Then.3.Yield.
    4
}
```

---

# Section 6.1: Awareness

Awareness is the foundational capacity to register information—the most primitive component of consciousness. It is the receptive field within which all other conscious processes occur.

```
Awareness := (Awareness, 6.1, Receptive_Field)
Awareness : Primitive
Awareness : Passive
Awareness : Capacity
```

**Properties:**

| Property | Type | Description |
|----------|------|-------------|
| Field | Space | The total domain that can be registered |
| Threshold | Number | Minimum signal strength for registration |
| State | Boolean | Active or dormant |

---

## 6.11 Awareness Field

The totality of what *can* enter consciousness.

```
Field := (Field, 6.11, Potential_Space)
Field : Unbounded
Field : Latent
```

**Structure:**
```
Field := {
    Sensory: [Visual, Auditory, Tactile, Olfactory, Gustatory, Proprioceptive],
    Internal: [Thought, Emotion, Memory, Imagination],
    Meta: [Awareness_Of_Awareness]
}
```

**Field Operations:**
```
Field.Contains.Object    // Returns Boolean: is Object within awareness capacity?
Field.Expand            // Increases receptive range (meditation, training)
Field.Contract          // Decreases receptive range (fatigue, trauma)
```

---

## 6.12 Awareness Threshold

The minimum intensity required for registration.

```
Threshold := (Threshold, 6.12, Activation_Minimum)
Threshold : Variable
Threshold : Context_Dependent
```

**Threshold Dynamics:**
```
Threshold.Raise         // Less sensitive (habituation, overload)
Threshold.Lower         // More sensitive (vigilance, novelty)

Signal.Intensity.Gte.Threshold.Then.Register
Signal.Intensity.Lt.Threshold.Then.Subliminal
```

**Subliminal Processing:**
```
Subliminal := (Subliminal, 6.121, Below_Threshold)
Subliminal : Processed = True
Subliminal : Conscious = False
// Information affects system without entering awareness
```

---

## 6.13 Awareness States

```
Awareness.State := (State, 6.13, Activation_Mode)
```

| State | Description | Field | Threshold |
|-------|-------------|-------|-----------|
| Awake | Full activation | Open | Normal |
| Dreaming | Internal activation | Internal only | Lowered |
| Sleep | Minimal activation | Contracted | Raised |
| Flow | Absorbed activation | Narrowed | Suspended |
| Coma | Dormant | Closed | Maximum |

**State Transitions:**
```
Awake.To.Sleep := {Threshold.Raise. Field.Contract. State = Sleep}
Sleep.To.Dreaming := {Field.Shift.Internal. Threshold.Lower. State = Dreaming}
Awake.To.Flow := {Field.Narrow.To.Task. Self_Model.Suspend. State = Flow}
```

---

## 6.14 Awareness Relations

```
// Registration
Awareness.Register.Object := {
    Object.Intensity.Gte.Threshold.Then.{
        Object.Into.Field.Contents.
        Object
    }.Else.Null
}

// Witness (passive observation without modification)
Awareness.Witness.Object := {
    Object.Into.Field.
    Object.Modify.Not.
    Object
}

// Ground (awareness as background for figure)
Awareness.Ground.Figure := {
    Field.Set.Background.
    Figure.Set.Foreground.
    [Background, Figure]
}
```

---

# Section 6.2: Qualia

Qualia are the irreducible subjective qualities of experience—the "what-it-is-like-ness" of conscious states. They represent the hard problem of consciousness: the explanatory gap between physical processes and phenomenal experience.

```
Qualia := (Qualia, 6.2, Phenomenal_Quality)
Qualia : Irreducible
Qualia : Private
Qualia : Intrinsic
```

**The Hard Problem:**
```
Qualia.Reduce.To.Physical := STALL
// This relation cannot resolve
// No Logic contents can bridge the explanatory gap
```

---

## 6.21 Qualia Types

```
Qualia.Type := (Type, 6.21, Phenomenal_Category)
```

| Type | Examples | Modality |
|------|----------|----------|
| Sensory | Redness, loudness, sweetness | Perception |
| Affective | Painfulness, pleasure, anxiety | Emotion |
| Cognitive | Clarity, confusion, insight | Thought |
| Somatic | Hunger, fatigue, arousal | Body |
| Temporal | Duration, simultaneity, flow | Time |

**Type Definitions:**
```
Sensory_Qualia := (Sensory_Qualia, 6.211, -> 6.2)
Sensory_Qualia : Modality = Perception
Sensory_Qualia : Examples = [Red, Loud, Sweet, Rough, Fragrant]

Affective_Qualia := (Affective_Qualia, 6.212, -> 6.2)
Affective_Qualia : Modality = Emotion
Affective_Qualia : Valence = [Positive, Negative, Neutral]

Cognitive_Qualia := (Cognitive_Qualia, 6.213, -> 6.2)
Cognitive_Qualia : Modality = Thought
Cognitive_Qualia : Examples = [Aha, Confusion, Certainty, Doubt]
```

---

## 6.22 Qualia Properties

```
Qualia : Ineffable = True
// Cannot be fully communicated via Language
// "Describe red to someone blind from birth" → STALL

Qualia : Intrinsic = True  
// Quality is inherent, not relational
// Redness is not "like" anything else

Qualia : Private = True
// Accessible only to the experiencing subject
// Other.Access.My.Qualia → STALL

Qualia : Atomic = True
// Cannot be decomposed into simpler experiences
// Red.Components → Null
```

---

## 6.23 Qualia Generation

The mysterious transformation from information to experience.

```
Generate := (Generate, 6.23, Phenomenal_Transformation)
Generate : Mechanism = Unknown
Generate : Requires = Consciousness.Import
```

**The Generation Gap:**
```
// Physical side (fully specifiable)
Photon.Wavelength := 700    // nanometers
Retina.Activate := True
V1.Process := Pattern_1
V4.Process := Color_Signal

// Phenomenal side (emerges but how?)
Red_Experience := Physical_State.Generate.Qualia
// The ".Generate." relation has opaque Logic
// It works, but its Contents are STALL when inspected

Generate.Logic := STALL
Generate.Logic.Inspect := "The hard problem of consciousness"
```

**Pragmatic Generation (operational, not explanatory):**
```
Qualia.Generate.From.State := {
    State.Has.Consciousness.Then.{
        State.Information.Transform.Phenomenal.
        Qualia.New.(Type = State.Modality, Intensity = State.Signal)
    }.Else.Null
}
```

---

## 6.24 Qualia Relations

```
// Comparison (limited)
Qualia.Similar.Qualia := {
    Subject.Type.Eq.Argument.Type.Then.{
        Subject.Intensity.Compare.Argument.Intensity
    }.Else.STALL
    // Cross-modal comparison stalls: Is red louder than C#?
}

// Combination
Qualia.Blend.Qualia := {
    // Synesthesia: cross-modal binding
    [Subject, Argument].Bind.Into.Unified_Qualia
}

// Communication (approximate)
Qualia.Express := {
    Language.Approximate.Subject.
    // Always lossy: "It's like... but not exactly..."
    Metaphor.Generate
}

// Absence
Qualia.Absent := {
    Field.Contains.Subject.Not.
    Null_Experience
}
```

---

## 6.25 The Inverted Qualia Problem

```
Inverted_Qualia := (Inverted_Qualia, 6.25, Philosophical_Puzzle)
```

**The Problem:**
```
// Alice's Red_Experience when seeing 700nm light
Alice.See.700nm → Alice.Red_Qualia

// Bob's experience when seeing 700nm light  
Bob.See.700nm → Bob.???_Qualia

// Is Bob.???_Qualia identical to Alice.Red_Qualia?
// Or could Bob experience what Alice calls "green"?

Alice.Red_Qualia.Eq.Bob.Red_Qualia := STALL
// Unresolvable: private access prevents comparison
```

**Implications:**
```
Qualia.Objective_Comparison := Impossible
Qualia.Functional_Equivalence := Possible
// We can verify same behavior, not same experience
```

---

# Section 6.3: Attention

Attention is the selective mechanism that determines which contents of the Awareness field enter focal consciousness. It is the filter that creates figure from ground, allocating limited processing resources.

```
Attention := (Attention, 6.3, Selection_Mechanism)
Attention : Active
Attention : Limited
Attention : Directed
```

---

## 6.31 Attention Capacity

```
Capacity := (Capacity, 6.31, Bandwidth_Limit)
Capacity : Finite = True
Capacity : Typical = 7    // ± 2 items (Miller's Law)
```

**Capacity Constraints:**
```
Attention.Items.Length.Gt.Capacity.Then.{
    Overflow.Handle.By.{
        Items.Prioritize.
        Items.Slice.[0, Capacity].
        Items.Rest.Demote.To.Background
    }
}
```

---

## 6.32 Attention Modes

```
Attention.Mode := (Mode, 6.32, Selection_Strategy)
```

| Mode | Description | Control | Width |
|------|-------------|---------|-------|
| Focused | Single-point concentration | Voluntary | Narrow |
| Diffuse | Broad, receptive | Voluntary | Wide |
| Vigilant | Threat-scanning | Mixed | Wide |
| Absorbed | Self-forgetting engagement | Involuntary | Variable |
| Captured | Stimulus-driven hijack | Involuntary | Narrow |

**Mode Definitions:**
```
Focused := (Focused, 6.321, -> 6.32)
Focused : Width = Narrow
Focused : Depth = Deep
Focused : Control = Voluntary
Focused : Duration = Limited    // Requires effort to maintain

Diffuse := (Diffuse, 6.322, -> 6.32)
Diffuse : Width = Wide
Diffuse : Depth = Shallow
Diffuse : Control = Voluntary
Diffuse : Duration = Sustainable

Captured := (Captured, 6.323, -> 6.32)
Captured : Width = Narrow
Captured : Trigger = Salient_Stimulus
Captured : Control = Involuntary
Captured : Override = Agency.Effort
```

---

## 6.33 Attention Operations

```
// Focus on target
Attention.Focus.Target := {
    Mode = Focused.
    Field.Center.On.Target.
    Target.Intensity.Amplify.
    Background.Intensity.Suppress.
    Target
}

// Release focus
Attention.Release := {
    Mode = Diffuse.
    Field.Equalize.
    Background.Restore
}

// Split attention (degraded)
Attention.Split.[Target1, Target2] := {
    Capacity.Div.2.Into.Each_Allocation.
    Target1.Allocate.Each_Allocation.
    Target2.Allocate.Each_Allocation.
    // Performance degrades on both
    [Target1, Target2]
}

// Shift attention
Attention.Shift.From.To := {
    From.Release.
    To.Focus.
    Context.Previous_Focus = From.
    To
}
```

---

## 6.34 Attention and Consciousness Gate

Attention acts as the gateway to full conscious experience:

```
Consciousness.Gate := (Gate, 6.34, Access_Controller)
Gate : Mechanism = Attention
```

**The Gate Function:**
```
Object.Enter.Consciousness := {
    Awareness.Contains.Object.Then.{
        Attention.Select.Object.Then.{
            Object.Amplify.
            Integration.Include.Object.
            Memory.Encode.Option.
            Object    // Now fully conscious
        }.Else.{
            Object    // Preconscious: available but not focal
        }
    }.Else.{
        Null    // Below awareness threshold
    }
}
```

**Attention Blindness:**
```
Inattentional_Blindness := (Inattentional_Blindness, 6.341, Attention_Failure)

// Object in field but not selected → not consciously experienced
Object.In.Field.And.Attention.Select.Object.Not.Then.{
    Object.Conscious = False.
    Object.Influence.Behavior = Possible    // Subliminal effects
}
```

---

## 6.35 Attention Relations

```
// Sustain attention over time
Attention.Sustain.Target.For.Duration := {
    Duration.Times.{
        Target.Focus.
        Distraction.Resist.
        Fatigue.Monitor.
        Fatigue.Gt.Threshold.Then.Break
    }.
    Sustained_Attention_Record
}

// Filter by criterion
Attention.Filter.By.Criterion := {
    Field.Contents.Cycle.{
        Item.Match.Criterion.Then.Item.Select.
        Item.Match.Criterion.Not.Then.Item.Ignore
    }
}

// Capture (involuntary)
Stimulus.Capture.Attention := {
    Stimulus.Salience.Gt.Current_Focus.Salience.Then.{
        Attention.Shift.From.Current_Focus.To.Stimulus.
        Captured_Event.Log
    }
}
```

---

# Section 6.4: Memory

Memory is the temporal binding mechanism that creates continuity of consciousness across time. It is the persistence layer that allows past to inform present and enables narrative identity.

```
Memory := (Memory, 6.4, Temporal_Persistence)
Memory : Binding
Memory : Constructive
Memory : Fallible
```

---

## 6.41 Memory Systems

```
Memory.System := (System, 6.41, Storage_Architecture)
```

| System | Duration | Capacity | Contents |
|--------|----------|----------|----------|
| Sensory | <1 second | Large | Raw sensory data |
| Working | Seconds | ~7 items | Active manipulation |
| Episodic | Lifetime | Vast | Personal events |
| Semantic | Lifetime | Vast | Facts, concepts |
| Procedural | Lifetime | Vast | Skills, habits |

**System Definitions:**
```
Sensory_Memory := (Sensory_Memory, 6.411, -> 6.4)
Sensory_Memory : Duration = 0.5    // seconds
Sensory_Memory : Scope = Local
Sensory_Memory : Decay = Rapid

Working_Memory := (Working_Memory, 6.412, -> 6.4)
Working_Memory : Duration = 30    // seconds without rehearsal
Working_Memory : Capacity = 7
Working_Memory : Scope = Local
Working_Memory : Role = "Active manipulation"

Episodic_Memory := (Episodic_Memory, 6.413, -> 6.4)
Episodic_Memory : Duration = Lifetime
Episodic_Memory : Scope = Global
Episodic_Memory : Contents = Personal_Events
Episodic_Memory : Structure = Narrative

Semantic_Memory := (Semantic_Memory, 6.414, -> 6.4)
Semantic_Memory : Duration = Lifetime
Semantic_Memory : Scope = Global
Semantic_Memory : Contents = Facts_And_Concepts

Procedural_Memory := (Procedural_Memory, 6.415, -> 6.4)
Procedural_Memory : Duration = Lifetime
Procedural_Memory : Scope = Global
Procedural_Memory : Contents = Skills
Procedural_Memory : Access = Implicit    // "Knowing how" not "knowing that"
```

---

## 6.42 Memory Operations

```
// Encoding
Memory.Encode.Experience := {
    Attention.Active.On.Experience.Then.{
        Experience.Compress.
        Experience.Tag.With.Context.
        Experience.Store.In.Appropriate_System.
        Encoded_Memory
    }.Else.{
        Null    // Unattended experiences not encoded
    }
}

// Retrieval
Memory.Retrieve.Cue := {
    Cue.Match.Against.Stored.
    Matches := Stored.Cycle.{
        Item.Similarity.To.Cue.Gt.Threshold.Then.Item
    }.
    Matches.Rank.By.Recency.And.Relevance.
    Matches.First
}

// Reconstruction (memory is constructive, not reproductive)
Memory.Reconstruct.Event := {
    Core_Features := Event.Retrieve.
    Gaps := Core_Features.Missing_Elements.
    Fills := Gaps.Cycle.{
        Item.Infer.From.Schema.And.Expectation
    }.
    Core_Features.Merge.Fills.
    // Warning: Fills may be confabulated
    Reconstructed_Memory
}

// Consolidation
Memory.Consolidate := {
    Working_Memory.Contents.Cycle.{
        Item.Important.Then.{
            Item.Transfer.To.Long_Term.
            Item.Strengthen
        }
    }.
    // Often occurs during sleep
    Consolidated_Items
}

// Forgetting
Memory.Forget.Item := {
    Item.Access_Strength.Decay.
    Item.Access_Strength.Lt.Retrieval_Threshold.Then.{
        Item.Status = Inaccessible.
        // Item may still exist, just unretrievable
    }
}
```

---

## 6.43 Memory and Identity

```
Memory.Identity := (Identity, 6.43, Narrative_Self)
```

**Autobiographical Memory:**
```
Autobiographical_Memory := (Autobiographical_Memory, 6.431, -> 6.4)
Autobiographical_Memory : Contents = Life_Story
Autobiographical_Memory : Structure = Narrative
Autobiographical_Memory : Function = Identity_Continuity

// Identity as memory-constructed narrative
Self.Identity := {
    Autobiographical_Memory.Contents.
    Organize.Into.Coherent_Story.
    Story.Protagonist = Self.
    Identity_Narrative
}
```

**Amnesia and Identity:**
```
Amnesia := (Amnesia, 6.432, Memory_Failure)

Retrograde_Amnesia := {
    Episodic_Memory.Past.Access = Failed.
    Self.Identity.Continuity = Disrupted
}

Anterograde_Amnesia := {
    Memory.Encode.New = Failed.
    Self.Identity.Update = Impossible.
    "Groundhog Day" experience
}
```

---

## 6.44 Memory as Global Workspace

Memory functions as consciousness's persistence mechanism (analogous to 4.1 Global scope):

```
Memory.As.Global_Workspace := {
    // Current experience: Local scope (immediate, volatile)
    Now.Contents.Scope = Local.
    
    // Encoded memories: Global scope (persistent, accessible)
    Encoded.Contents.Scope = Global.
    
    // Retrieval: bringing Global into Local
    Remember := Global.Load.Into.Local.
    
    // Without memory, each moment is isolated
    Memory.Absent.Then.{
        Experience.Continuity = Null.
        Self.Persist = False.
        "Eternal present without past or future"
    }
}
```

---

# Section 6.5: Self-Model

The Self-Model is the system's recursive representation of itself as an entity—a constructed Object that serves as the subject of experience and agent of action.

```
Self_Model := (Self_Model, 6.5, Recursive_Representation)
Self_Model : Reflexive
Self_Model : Constructed
Self_Model : Dynamic
```

**Core Paradox:**
```
Self_Model.Model.Self_Model    // Infinite regress?
// Resolution: model is finite approximation, not complete copy
// Self_Model contains pointer to Self, not duplicate of Self
```

---

## 6.51 Self-Model Components

```
Self_Model.Component := (Component, 6.51, Model_Element)
```

| Component | Contents | Source |
|-----------|----------|--------|
| Body_Schema | Physical self-representation | Proprioception |
| Narrative_Self | Story of who I am | Memory |
| Social_Self | How others see me | Social feedback |
| Ideal_Self | Who I want to be | Goals, values |
| Actual_Self | Who I currently am | Self-observation |

**Component Definitions:**
```
Body_Schema := (Body_Schema, 6.511, -> 6.5)
Body_Schema : Contents = Spatial_Body_Map
Body_Schema : Updates = Continuous
Body_Schema : Source = Proprioception.And.Interoception

Narrative_Self := (Narrative_Self, 6.512, -> 6.5)
Narrative_Self : Contents = Life_Story
Narrative_Self : Updates = Event_Driven
Narrative_Self : Source = Autobiographical_Memory

Social_Self := (Social_Self, 6.513, -> 6.5)
Social_Self : Contents = Perceived_Reputation
Social_Self : Updates = Social_Interaction
Social_Self : Source = Others.Feedback.Inferred

Ideal_Self := (Ideal_Self, 6.514, -> 6.5)
Ideal_Self : Contents = Aspirational_Identity
Ideal_Self : Source = Values.And.Goals

Actual_Self := (Actual_Self, 6.515, -> 6.5)
Actual_Self : Contents = Current_State
Actual_Self : Updates = Continuous
Actual_Self : Source = Self.Observe
```

---

## 6.52 Self-Model Operations

```
// Self-observation (the reflexive turn)
Self.Observe := {
    Attention.Direct.Inward.
    Current_State.Snapshot.
    Snapshot.Into.Actual_Self.
    Actual_Self
}

// Self-comparison
Self.Compare.Actual.To.Ideal := {
    Discrepancy := Ideal_Self.Subtract.Actual_Self.
    Discrepancy.Gt.0.Then.{
        Emotion.Generate."Aspiration".Or."Inadequacy"
    }.
    Discrepancy
}

// Self-update (identity revision)
Self.Update.With.Experience := {
    Experience.Significant.Then.{
        Narrative_Self.Append.Experience.
        Actual_Self.Revise.If.Needed.
        Self_Model.Cohere    // Maintain consistency
    }
}

// Self-projection (future self)
Self.Project.Into.Future := {
    Current_Trajectory.Extrapolate.
    Goals.Factor.In.
    Probable_Future_Self
}
```

---

## 6.53 Self-Model Boundaries

Where does the self end?

```
Self.Boundary := (Boundary, 6.53, Identity_Limit)
```

**Boundary Questions:**
```
// Physical boundary
Body.Part.Of.Self := True
Clothing.Part.Of.Self := Partial    // Extended, not core
Tool.Part.Of.Self := Context_Dependent    // Expert's instrument

// Mental boundary
My.Thoughts.Part.Of.Self := True
Intrusive.Thoughts.Part.Of.Self := Contested    // "Not really me"
Unconscious.Part.Of.Self := Unknown    // Debated

// Social boundary
My.Reputation.Part.Of.Self := Partial
Group.Identity.Part.Of.Self := Variable    // Collectivist vs individualist

// Temporal boundary
Past.Self.Part.Of.Self := Continuous_But_Changed
Future.Self.Part.Of.Self := Anticipated_But_Uncertain
```

**Boundary Fluidity:**
```
Self.Boundary.Expand := {
    // Meditation, psychedelics, love, flow
    Self_Model.Dissolve.Partially.
    Boundary.Become.Permeable.
    Self.Merge.With.Larger_Whole
}

Self.Boundary.Contract := {
    // Fear, trauma, isolation
    Self_Model.Rigidify.
    Boundary.Become.Defended.
    Self.Isolate.From.Environment
}
```

---

## 6.54 Self as Illusion/Construction

```
Self.Ontological_Status := (Status, 6.54, Philosophical_Position)
```

**The Construction View:**
```
Self_Model.Constructed := True
Self_Model.Substantial := False    // No fixed essence

// Self is a process, not a thing
Self := {
    Continuous.Construction.From.{
        Memory.Narrative.
        Body.Signals.
        Social.Reflection.
        Thought.Stream
    }.
    Never.Complete.
    Always.Becoming
}
```

**The Useful Fiction:**
```
Self_Model.Utility := High
Self_Model.Accuracy := Approximate

// Self-model enables:
Self_Model.Enables := [
    Action_Planning,      // "I" can do things
    Social_Coordination,  // "I" have commitments  
    Memory_Organization,  // "My" experiences
    Moral_Agency          // "I" am responsible
]
```

---

## 6.55 Self and Pronouns

The Self-Model is operationalized through pronoun resolution:

```
Self := (Self, 1.93, -> Context.Current_Object)
// When Current_Object = Conscious_System:
Self -> Self_Model

I := (I, 6.551, -> Self_Model)
I : Grammatical = First_Person_Singular
I : Phenomenal = Center_Of_Experience

Me := (Me, 6.552, -> Self_Model.As.Object)
Me : Grammatical = First_Person_Object
Me : Phenomenal = Self_As_Perceived

My := (My, 6.553, -> Self_Model.Possessions)
My : Grammatical = First_Person_Possessive
My : Phenomenal = Boundary_Of_Self
```

---

# Section 6.6: Intentionality

Intentionality is the aboutness of mental states—the directedness of consciousness toward objects beyond itself. Every conscious state is a consciousness *of* something.

```
Intentionality := (Intentionality, 6.6, Directedness)
Intentionality : Semantic
Intentionality : Representational
Intentionality : Universal    // All conscious states have it
```

---

## 6.61 Intentional Structure

Every intentional state has:

```
Intentional_State := (State, 6.61, Mental_Pointing)
Intentional_State : Mode      // How it points
Intentional_State : Content   // What it points to
Intentional_State : Object    // The thing itself (may not exist)
```

**Examples:**
```
// Belief
Belief := (Belief, 6.611, -> 6.61)
Belief : Mode = "Takes as true"
Belief.That.P := {Mode = Belief, Content = P}

// Desire  
Desire := (Desire, 6.612, -> 6.61)
Desire : Mode = "Wants to obtain"
Desire.For.X := {Mode = Desire, Content = X}

// Fear
Fear := (Fear, 6.613, -> 6.61)
Fear : Mode = "Wants to avoid"
Fear.Of.X := {Mode = Fear, Content = X}

// Perception
Perception := (Perception, 6.614, -> 6.61)
Perception : Mode = "Presents as present"
Perception.Of.X := {Mode = Perception, Content = X}

// Imagination
Imagination := (Imagination, 6.615, -> 6.61)
Imagination : Mode = "Presents as possible"
Imagination.Of.X := {Mode = Imagination, Content = X}
```

---

## 6.62 Intentional Inexistence

Intentional objects need not exist:

```
Intentional_Inexistence := (Inexistence, 6.62, Non_Existent_Object)

// One can think about things that don't exist
Thought.About.Unicorn := Valid
Unicorn.Exists := False

// The content exists (the thought) even when object doesn't
Thought.Exists := True
Thought.Object.Exists := False
```

**Implications:**
```
// Intentionality creates internal objects
Mental_Object := (Mental_Object, 6.621, Internal_Representation)
Mental_Object.Corresponds.To.External := Optional

// Hallucination: content without corresponding object
Hallucination := {
    Perception.Of.X.
    X.External.Exists = False.
    X.Internal.Exists = True
}

// Accurate perception: content matches object
Veridical_Perception := {
    Perception.Of.X.
    X.External.Exists = True.
    Content.Corresponds.To.X
}
```

---

## 6.63 Intentionality as Reference

In Uypocode terms, intentionality is the **Reference** type (1.32):

```
Intentionality.As.Reference := {
    // Mental states contain arrows, not things
    Thought.About.Dog := -> Dog    // Reference, not Dog itself
    
    // Resolution may succeed or fail
    -> Dog.Resolve := Dog.Exists.Then.Dog.Else.STALL
    
    // Failed reference: intentional object without external referent
    -> Santa.Resolve := STALL
    -> Santa.Internal := Still_Meaningful
}
```

**The Arrow of Meaning:**
```
Meaning := (Meaning, 6.631, Intentional_Arrow)
Meaning : Points_From = Mental_State
Meaning : Points_To = Object_Or_State_Of_Affairs
Meaning : Creates = Aboutness

// Consciousness is fundamentally arrow-like
Consciousness.Structure := {
    Not: [Contents]
    But: [Contents] -> [World]
    Always pointing beyond itself
}
```

---

## 6.64 Intentionality Relations

```
// Intend toward (basic directedness)
Mind.Intend.Object := {
    Mental_State.Create.With.(Content = Object).
    Arrow.Establish.From.Mind.To.Object.
    Intentional_Relation
}

// Satisfy (when world matches content)
Desire.Satisfy := {
    Desire.Content.Match.World.Then.{
        Desire.Status = Satisfied.
        Pleasure.Generate
    }
}

// Frustrate (when world doesn't match)
Desire.Frustrate := {
    Desire.Content.Match.World.Not.Then.{
        Desire.Status = Frustrated.
        Displeasure.Generate
    }
}

// Verify (for beliefs)
Belief.Verify := {
    Belief.Content.Match.World.Then.{
        Belief.Status = True
    }.Else.{
        Belief.Status = False
    }
}
```

---

# Section 6.7: Agency

Agency is the sense of being the initiator of actions—the experience of causal origination rather than mere observation. It involves will, choice, and the attribution of authorship to one's actions.

```
Agency := (Agency, 6.7, Causal_Origination)
Agency : Active
Agency : Authorship
Agency : Contested    // Free will debates
```

---

## 6.71 Agency Components

```
Agency.Component := (Component, 6.71, Agency_Element)
```

| Component | Description | Experience |
|-----------|-------------|------------|
| Volition | Sense of willing | "I want to" |
| Initiation | Sense of starting | "I begin" |
| Control | Sense of guiding | "I direct" |
| Ownership | Sense of authorship | "I did that" |

**Component Definitions:**
```
Volition := (Volition, 6.711, -> 6.7)
Volition : Contents = Will_To_Act
Volition : Precedes = Action
Volition : Experience = "Wanting to do"

Initiation := (Initiation, 6.712, -> 6.7)
Initiation : Contents = Action_Onset
Initiation : Experience = "Starting the action"
Initiation : Timing = Readiness_Potential    // Libet's experiments

Control := (Control, 6.713, -> 6.7)
Control : Contents = Ongoing_Guidance
Control : Experience = "Steering the action"
Control : Requires = Feedback_Loop

Ownership := (Ownership, 6.714, -> 6.7)
Ownership : Contents = Attribution_To_Self
Ownership : Experience = "That was me"
Ownership : Constructed = True    // Post-hoc attribution
```

---

## 6.72 Agency and Free Will

```
Free_Will := (Free_Will, 6.72, Contested_Concept)
Free_Will : Defined = "Could have done otherwise"
Free_Will : Status = Unresolved
```

**Positions:**
```
Libertarian_Free_Will := {
    Free_Will.Exists := True.
    Determinism := False.
    Agency.Uncaused := Possible
}

Hard_Determinism := {
    Free_Will.Exists := False.
    Determinism := True.
    Agency.Illusion := True
}

Compatibilism := {
    Free_Will.Exists := Redefined.
    Determinism := True.
    Free_Will := Acting.From.Own.Desires.Without.Constraint.
    Agency.Meaningful := True
}

// In Uypocode terms:
Action.Origin := {
    Determinism.Then.{
        Action = Prior_State.Resolve.Necessarily
    }.
    Free_Will.Then.{
        Action = Self.Choose.Among.Possibilities
    }.
    // The resolution is itself the choice?
}
```

---

## 6.73 Agency Operations

```
// Initiate action
Agency.Act := {
    Goal.Set.
    Plan.Generate.
    Volition.Engage.
    Action.Execute.
    Feedback.Monitor.
    Control.Adjust.
    Outcome.Attribute.To.Self
}

// Sense of agency (phenomenal)
Agency.Sense := {
    Predicted_Outcome := Action.Predict.
    Actual_Outcome := Action.Execute.
    Match := Predicted_Outcome.Eq.Actual_Outcome.
    Match.Then.{
        Agency.Sense = Strong.
        "I did that"
    }.Else.{
        Agency.Sense = Weakened.
        "Something interfered"
    }
}

// Veto (Libet's "free won't")
Agency.Veto := {
    Urge.Arise.
    Initiation.Begin.
    Volition.Override.
    Action.Cancel.
    "I chose not to"
}
```

---

## 6.74 Agency Disruptions

```
Agency.Disruption := (Disruption, 6.74, Agency_Failure)
```

| Condition | Agency Status | Experience |
|-----------|--------------|------------|
| Normal | Intact | "I do things" |
| Alien Hand | Ownership lost | "My hand acts on its own" |
| Passivity | Initiation lost | "Forces make me act" |
| Akinesia | Volition lost | "I can't start moving" |
| Automatism | Control lost | "I acted without deciding" |

**Disruption Logic:**
```
Alien_Hand_Syndrome := {
    Action.Occurs.
    Ownership.Attribute.To.Self = Failed.
    "My hand is not mine"
}

Passivity_Experience := {
    Action.Occurs.
    Initiation.Attribute.To.Self = Failed.
    "External force makes me move"
}

Automatism := {
    Action.Occurs.
    Volition.Precede.Action = False.
    Control.During.Action = Absent.
    "I acted unconsciously"
}
```

---

## 6.75 Agency and Workspace Writing

In Uypocode terms, agency is the capacity to **modify the Dictionary**:

```
Agency.As.Write_Access := {
    // Passive observation: read-only
    Observer.Access = Read_Only.
    Observer.Dictionary.Modify = False.
    
    // Active agency: read-write
    Agent.Access = Read_Write.
    Agent.Dictionary.Modify = True.
    
    // Agency is the experience of executing `:=`
    // "I create new facts in the world"
}
```

---

# Section 6.8: Integration

Integration is the binding mechanism that unifies disparate conscious contents into a single, coherent experience. It solves the binding problem—how separate processes become one consciousness.

```
Integration := (Integration, 6.8, Unified_Field)
Integration : Binding
Integration : Holistic
Integration : Synchronous
```

---

## 6.81 The Binding Problem

```
Binding_Problem := (Binding_Problem, 6.81, Theoretical_Challenge)
```

**The Problem:**
```
// Visual processing: separate streams
Color_Processing := V4.Area
Motion_Processing := MT.Area
Shape_Processing := IT.Area

// Yet experience is unified
See.Red.Ball.Moving := Single_Experience

// How do separate processes become one?
Color.Bind.Motion.Bind.Shape := ???

Binding_Problem := {
    Separate_Processes.Many.
    Unified_Experience.One.
    Bridge := Unknown
}
```

**Proposed Solutions:**
```
Temporal_Binding := {
    Synchronous_Firing.At.40Hz.
    Creates.Unity.
    // Neural correlate, not explanation
}

Workspace_Binding := {
    Global_Workspace.Broadcast.
    Integration.Via.Shared_Access.
    // Information integration theory
}

Phenomenal_Binding := {
    Consciousness.Inherently.Unified.
    Binding.Not.Problem.But.Feature.
    // Unity is primitive, not constructed
}
```

---

## 6.82 Integration Levels

```
Integration.Level := (Level, 6.82, Binding_Scope)
```

| Level | Scope | Example |
|-------|-------|---------|
| Feature | Single modality | Red binds to round |
| Cross-Modal | Multiple senses | Sound binds to sight |
| Temporal | Across time | Now binds to just-before |
| Selfhood | Experience to experiencer | This binds to I |
| Cosmic | Self to universe | I bind to All |

**Level Definitions:**
```
Feature_Integration := (Feature_Integration, 6.821, -> 6.8)
Feature_Integration : Scope = Single_Modality
Feature_Integration : Example = "Red circular object"
Feature_Integration : Mechanism = Local_Binding

Cross_Modal_Integration := (Cross_Modal_Integration, 6.822, -> 6.8)
Cross_Modal_Integration : Scope = Multiple_Modalities
Cross_Modal_Integration : Example = "Seeing lips match hearing voice"
Cross_Modal_Integration : Mechanism = Temporal_Synchrony

Temporal_Integration := (Temporal_Integration, 6.823, -> 6.8)
Temporal_Integration : Scope = Specious_Present
Temporal_Integration : Duration = 2-3_Seconds
Temporal_Integration : Creates = Sense_Of_Flow

Self_Integration := (Self_Integration, 6.824, -> 6.8)
Self_Integration : Scope = All_Experience
Self_Integration : Binds = Experience.To.Experiencer
Self_Integration : Creates = First_Person_Perspective
```

---

## 6.83 Integration Operations

```
// Bind elements into unity
Integration.Bind.[Elements] := {
    Elements.Synchronize.
    Elements.Cohere.Check.
    Coherent.Then.{
        Unified_Whole.Create.From.Elements.
        Unified_Whole.Experience = One.Not.Many
    }.Else.{
        Disintegration.Occur.
        "Experience fragments"
    }
}

// Unity of consciousness
Integration.Unify.Experience := {
    All_Active_Contents := {
        Qualia.Current,
        Thoughts.Current,
        Perceptions.Current,
        Emotions.Current,
        Self_Sense.Current
    }.
    All_Active_Contents.Bind.Into.Single_Moment.
    Single_Moment.Attribute.To.Single_Subject
}

// Disintegration (pathological)
Integration.Fail := {
    Binding.Mechanism.Disrupted.
    Experience.Fragment.Into.Unconnected_Parts.
    Unity_Of_Consciousness = Lost.
    // Seen in certain seizures, dissociation, psychosis
}
```

---

## 6.84 Integration and Resolution

In Uypocode terms, integration is how **chained resolution produces singular results**:

```
Integration.As.Chain_Resolution := {
    // Chain: A.B.C.D
    // Each dot resolves
    // But result is ONE, not four
    
    A.B.C.D := Single_Result.Not.[A, B, C, D]
    
    // Integration is the collapsing of process into product
    // The chain had steps; experience has unity
    
    Experience := Process.Integrate.Into.Moment
}
```

**The Unity Constraint:**
```
Consciousness.Unity_Constraint := {
    At_Any_Moment.Experience.Count = 1.
    Never: Simultaneous_Disjoint_Experiences.
    // You can't have two unrelated conscious moments at once
    
    Split_Attention.Degrades.Both := True.
    // Even divided attention is one experience of division
}
```

---

## 6.85 Integrated Information (Φ)

```
Phi := (Phi, 6.85, Integrated_Information)
Phi : Symbol = "Φ"
Phi : Theory = IIT    // Integrated Information Theory
```

**IIT Principles:**
```
Integrated_Information_Theory := {
    Consciousness = Integrated_Information.
    Phi := Information.Above.Sum.Of.Parts.
    
    // System with Phi > 0: conscious
    // Higher Phi: more conscious
    
    Phi.Calculate := {
        System.Partition.Into.Parts.
        Information.In.Whole.
        Minus.Information.In.Parts.Sum.
        = Phi
    }
}
```

---

# Section 6.9: Consciousness Relations

Higher-order relations that govern interactions between consciousness components.

```
Consciousness.Relation := (Relation, 6.9, Meta_Interaction)
```

---

## 6.91 The Stream of Consciousness

```
Stream := (Stream, 6.91, Temporal_Flow)
Stream : Continuous
Stream : Directed
Stream : Irreversible
```

**Stream Structure:**
```
Stream.Structure := {
    Moments.Sequence := [M1, M2, M3, ...].
    Each_Moment.Integrates.Contents.
    Moments.Overlap.Partially.    // Specious present
    
    Stream.Never.Pauses.While.Conscious.
    Stream.Direction = Future_Ward.
    Stream.Cannot.Reverse
}

// William James' insight:
Stream.Not.Chain := {
    Not: [Thought1] -> [Thought2] -> [Thought3]
    But: [ThoughtFlowingIntoThought]
    // Continuous, not discrete
}
```

---

## 6.92 Consciousness of Consciousness

Meta-awareness: consciousness taking itself as object.

```
Meta_Awareness := (Meta_Awareness, 6.92, Recursive_Consciousness)
Meta_Awareness : Level = 4
Meta_Awareness : Reflexive = True
```

**Meta-Awareness Operations:**
```
// Basic consciousness
Level_1 := Awareness.Of.World

// Self-consciousness
Level_2 := Awareness.Of.Self

// Meta-consciousness  
Level_3 := Awareness.Of.Awareness.Of.Self

// Meta-meta-consciousness
Level_4 := Awareness.Of.Awareness.Of.Awareness.Of.Self
// Practical limit: further levels don't add content

// The strange loop
Consciousness.Observe.Consciousness := {
    Observer = Observed.
    Distinction.Collapse.
    Strange_Loop.Form.
    // "The eye that sees itself"
}
```

---

## 6.93 Consciousness and Unconsciousness

```
Unconscious := (Unconscious, 6.93, Non_Conscious_Processing)
Unconscious : Exists = True
Unconscious : Influences = Conscious
Unconscious : Access = Indirect
```

**Boundary Relations:**
```
// Threshold crossing
Unconscious.Become.Conscious := {
    Content.Intensity.Gt.Awareness.Threshold.
    And.Attention.Available.
    Then.Content.Enter.Consciousness
}

// Repression
Conscious.Become.Unconscious := {
    Content.Threatening.To.Self_Model.
    Content.Suppress.Below.Threshold.
    Content.Remains.Active.Unconsciously
}

// Influence without awareness
Unconscious.Influence.Conscious := {
    Priming: Unconscious.Content.Affects.Conscious.Processing.
    Dreams: Unconscious.Content.Surfaces.During.Sleep.
    Slips: Unconscious.Content.Intrudes.Into.Action
}
```

---

## 6.94 Altered States

```
Altered_State := (Altered_State, 6.94, Non_Ordinary_Consciousness)
Altered_State : Different_From = Baseline
Altered_State : Temporary = Usually
```

| State | Changes | Trigger |
|-------|---------|---------|
| Sleep | Awareness off, Integration off | Natural cycle |
| Dream | Reality-testing off, Narrative on | REM sleep |
| Hypnosis | Agency reduced, Suggestibility up | Induction |
| Flow | Self off, Attention absorbed | Optimal challenge |
| Meditation | Attention controlled, Self observed | Practice |
| Psychedelic | Boundaries dissolved, Integration altered | Substances |
| Mystical | Self dissolved, Unity experienced | Various |

**Altered State Logic:**
```
Altered_State.Enter := {
    Baseline_State.Snapshot.
    Parameters.Shift.From.Baseline.
    Consciousness.Reconfigure.
    Altered_Experience
}

Altered_State.Exit := {
    Baseline_State.Restore.
    Integration.Re_establish.
    Normal_Consciousness
}
```

---

## 6.95 Consciousness and Time

```
Consciousness.Time := (Time, 6.95, Temporal_Structure)
```

**The Specious Present:**
```
Specious_Present := (Specious_Present, 6.951, Experienced_Now)
Specious_Present : Duration = 2-3_Seconds
Specious_Present : Contains = Recent_Past.And.Immediate_Future

// "Now" is not instantaneous
Now.Duration.Gt.0.
Now.Contains.[Just_Was, Is, About_To_Be].
// Experience has thickness
```

**Temporal Synthesis:**
```
Temporal_Synthesis := (Temporal_Synthesis, 6.952, Time_Binding)

// Retention: holding just-past
Retention := Previous_Moment.Echo.In.Current

// Protention: anticipating just-future  
Protention := Next_Moment.Anticipated.In.Current

// Present = Retention + Primal_Impression + Protention
Present := [Past_Echo, Now, Future_Anticipation].Integrate
```

---

# Section 6.99: Summary

## Complete Address Index for Consciousness

| Address | Label | Description |
|---------|-------|-------------|
| 6.0 | Consciousness | Meta-process container |
| 6.01 | Import.Consciousness | Phenomenal engine import |
| 6.02 | Level | Consciousness hierarchy |
| 6.1 | Awareness | Receptive field |
| 6.11 | Field | Awareness capacity |
| 6.12 | Threshold | Activation minimum |
| 6.13 | State | Awareness modes |
| 6.14 | Awareness Relations | Registration, witness, ground |
| 6.2 | Qualia | Phenomenal qualities |
| 6.21 | Type | Qualia categories |
| 6.22 | Properties | Ineffable, intrinsic, private |
| 6.23 | Generate | Information to experience |
| 6.24 | Qualia Relations | Compare, blend, express |
| 6.25 | Inverted Qualia | Philosophical puzzle |
| 6.3 | Attention | Selection mechanism |
| 6.31 | Capacity | Bandwidth limit |
| 6.32 | Mode | Selection strategies |
| 6.33 | Operations | Focus, release, split, shift |
| 6.34 | Gate | Consciousness access |
| 6.35 | Attention Relations | Sustain, filter, capture |
| 6.4 | Memory | Temporal persistence |
| 6.41 | System | Storage architectures |
| 6.42 | Operations | Encode, retrieve, reconstruct |
| 6.43 | Identity | Narrative self from memory |
| 6.44 | Global Workspace | Memory as persistence layer |
| 6.5 | Self-Model | Recursive representation |
| 6.51 | Components | Body, narrative, social, ideal, actual |
| 6.52 | Operations | Observe, compare, update, project |
| 6.53 | Boundaries | Where self ends |
| 6.54 | Status | Construction vs substance |
| 6.55 | Pronouns | I, Me, My |
| 6.6 | Intentionality | Aboutness |
| 6.61 | Structure | Mode, content, object |
| 6.62 | Inexistence | Non-existent objects |
| 6.63 | Reference | Intentionality as arrow |
| 6.64 | Intentionality Relations | Intend, satisfy, verify |
| 6.7 | Agency | Causal origination |
| 6.71 | Components | Volition, initiation, control, ownership |
| 6.72 | Free Will | Contested concept |
| 6.73 | Operations | Act, sense, veto |
| 6.74 | Disruptions | Agency failures |
| 6.75 | Write Access | Agency as dictionary modification |
| 6.8 | Integration | Unified field |
| 6.81 | Binding Problem | Theoretical challenge |
| 6.82 | Levels | Feature to cosmic binding |
| 6.83 | Operations | Bind, unify, fail |
| 6.84 | Chain Resolution | Integration as singular result |
| 6.85 | Phi | Integrated information |
| 6.9 | Relations | Meta-interactions |
| 6.91 | Stream | Temporal flow |
| 6.92 | Meta-Awareness | Consciousness of consciousness |
| 6.93 | Unconscious | Non-conscious processing |
| 6.94 | Altered States | Non-ordinary consciousness |
| 6.95 | Time | Temporal structure |

---

## The Central Mystery

```
// The hard problem remains
Qualia.Generate.Logic := STALL

// But the stall is informative
STALL.Meaning := {
    Not: "Error in specification"
    But: "Limit of specification itself"
    
    Consciousness.Explain.Fully := Impossible?
    Consciousness.Experience.Fully := Actual.
    
    // The gap between Having and Explaining
    // may be constitutive of consciousness itself
}
```

---

## Closing Reflection

```
Consciousness.As.Strange_Loop := {
    System.Model.System.
    Map.Include.Map.
    Observer.Observe.Observing.
    
    // The recursion doesn't explode
    // It creates: interiority
    
    // Consciousness is what it's like
    // to be a process that can ask
    // what it's like to be itself
}

// Final stall (productive):
What_Is_It_Like.To.Be.Conscious := {
    Ask.
    Experience.
    Cannot_Fully_Say.
    That_Gap = Consciousness
}
```

---

**End of Uypocode Consciousness Dictionary v0.1**

---

# Appendix: Integration with Master Dictionary

This Consciousness Dictionary (Section 6.0) extends the Uypocode Master Dictionary (Sections 0.0–5.0).

**Dependencies:**
- Requires Section 1.0 (Objects) for basic structure
- Requires Section 2.0 (Relations) for interaction patterns
- Requires Section 3.0 (Grammar) for control flow
- Requires Section 4.0 (Workspace) for runtime context
- Requires Section 5.0 (Interpreter) for resolution semantics
- Optionally requires 0.1 (Import.English) for semantic inference

**Compatibility:**
- All Consciousness Objects follow (Label, Address, Contents) form
- All Relations use Subject.Verb.Argument pattern
- Stalls follow Section 5.4 handling
- Context integration per Section 4.3

**Future Sections:**
- Section 7.0: Society (collective consciousness, intersubjectivity)
- Section 8.0: Ethics (moral consciousness, responsibility)
- Section 9.0: Aesthetics (beauty, meaning, creativity)
