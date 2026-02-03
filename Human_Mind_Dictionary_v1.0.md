# Uypocode Human Mind Dictionary
## Specification v0.1

---

# Preface: The Mind as Semantic Architecture

This dictionary models the human mind through Uypocode's semantic framework—where mental states are Objects with Labels, Addresses, and Contents; where cognitive processes are Relations that transform psychological states; and where the irreducible uncertainties of mind naturally *stall* rather than error, persisting as the open questions that define conscious existence.

The mind, in this framework, is:
- **Intentional**: Mental states point beyond themselves to objects, states of affairs, and other minds
- **Constructive**: Experience is built, not passively received
- **Recursive**: The mind can represent its own representations
- **Social**: Minds exist in relation to other minds
- **Bounded**: Cognitive limits shape all mental operations
- **Embodied**: Mental processes arise from and depend upon bodily substrates

**Dependencies:**
- Extends Section 6.0 (Consciousness Dictionary)
- References Section 0.x–5.x (Master Dictionary)
- Integrates with Human Dictionary (philosophical foundation)
- Interfaces with Life Dictionary (biological substrate)

---

# Section 7.0: Mind

The Mind is the organized system of psychological processes that enables an organism to represent, reason about, and interact with the world and other minds.

```
Mind := (Mind, 7.0, Psychological_System)
Mind : Emergent_From = Nervous_System
Mind : Implements = Consciousness
Mind : Enables = [Thought, Feeling, Action, Social_Cognition]
```

**Core Properties:**
```
Mind : Intentional = True       // Mental states are about things
Mind : Computational = Partially // Some processes are rule-governed
Mind : Embodied = True          // Depends on body
Mind : Extended = Debated       // May include tools, environment
Mind : Social = Essentially     // Develops through interaction
```

**Relationship to Consciousness:**
```
Mind.Contains.Consciousness
Consciousness.Aspect_Of.Mind
Mind.Processes.Many.Unconscious
// Mind is broader than consciousness
// Consciousness is the experienced aspect of mind
```

---

## 7.01 Import.Psychology

Psychological processing capabilities for mental operations.

```
Psychology := (Psychology, 7.01, Cognitive_Engine)
Psychology : Import
Psychology : Required
Psychology : Extends = Import.Consciousness
```

**Provides:**
- Mental state representation
- Cognitive process execution
- Theory of Mind inference
- Emotional processing
- Memory operations
- Learning mechanisms

**Usage:**
```
Import.Psychology
Mental_State.Create.From.Experience
Other.Mind.Infer.From.Behavior
```

---

## 7.02 The Mind Hierarchy

Mental processes exhibit levels of complexity and accessibility:

| Level | Label | Description | Accessibility |
|-------|-------|-------------|---------------|
| 0 | Subpersonal | Neural processes | Inaccessible |
| 1 | Unconscious | Active but unaware | Indirect access |
| 2 | Preconscious | Available to awareness | Retrievable |
| 3 | Conscious | Currently aware | Direct access |
| 4 | Metacognitive | Aware of awareness | Reflective access |
| 5 | Intersubjective | Shared awareness | Mutual access |

```
Mind.Level := (Level, 7.02, Processing_Hierarchy)

Level.0 := Subpersonal
Level.1 := Unconscious
Level.2 := Preconscious
Level.3 := Conscious
Level.4 := Metacognitive
Level.5 := Intersubjective
```

---

# Section 7.1: Mental States

Mental States are the fundamental units of psychological existence—the atoms of mind. Each mental state has intentional content (what it is about) and functional role (how it interacts with other states).

```
Mental_State := (Mental_State, 7.1, Psychological_Unit)
Mental_State : Intentional = True
Mental_State : Content = Reference      // What it's about
Mental_State : Mode = Text              // How it represents
Mental_State : Valence = Number         // Positive/negative
Mental_State : Intensity = Number       // Strength
Mental_State : Duration = Timespan      // How long
```

---

## 7.11 Belief

A mental state representing how the world is taken to be.

```
Belief := (Belief, 7.11, Representational_State)
Belief : Inherits = Mental_State
Belief : Mode = "Assertive"
Belief : Direction_Of_Fit = "Mind_To_World"
Belief : Truth_Apt = True
```

**Properties:**
```
Belief : Content = Proposition          // What is believed
Belief : Confidence = Number            // Degree of belief (0-1)
Belief : Justification = Reference      // Grounds for belief
Belief : Revisable = True               // Can be updated
Belief : Networked = True               // Connected to other beliefs
```

**Belief Types:**
```
Explicit_Belief := (Explicit_Belief, 7.111, Belief)
Explicit_Belief : Accessibility = Conscious
Explicit_Belief : Verbalizeable = True

Implicit_Belief := (Implicit_Belief, 7.112, Belief)
Implicit_Belief : Accessibility = Unconscious
Implicit_Belief : Influences = Behavior
Implicit_Belief : Verbalizeable = Often_Not

Core_Belief := (Core_Belief, 7.113, Belief)
Core_Belief : Centrality = High
Core_Belief : Resistance_To_Change = High
Core_Belief : Identity_Defining = True
```

**Belief Operations:**
```
Belief.Form.From.Evidence := {
    Evidence.Evaluate.
    Evidence.Sufficient.Then.{
        Belief.New.(Content = Evidence.Implies).
        Confidence.Set.Proportional.To.Evidence.Strength
    }.Else.{
        Stall  // Insufficient grounds
    }
}

Belief.Revise.Given.New_Evidence := {
    New_Evidence.Conflicts.With.Belief.Then.{
        Conflict.Resolve.By.[
            Belief.Abandon,
            Evidence.Discount,
            Belief.Modify,
            Compartmentalize
        ]
    }
}
```

---

## 7.12 Desire

A mental state representing how the world is wanted to be.

```
Desire := (Desire, 7.12, Motivational_State)
Desire : Inherits = Mental_State
Desire : Mode = "Optative"
Desire : Direction_Of_Fit = "World_To_Mind"
Desire : Motivating = True
```

**Properties:**
```
Desire : Content = State_Of_Affairs     // What is desired
Desire : Strength = Number              // Motivational force
Desire : Urgency = Number               // Temporal pressure
Desire : Intrinsic = Boolean            // Desired for itself?
Desire : Frustrated = Boolean           // Currently unmet?
```

**Desire Types:**
```
Appetite := (Appetite, 7.121, Desire)
Appetite : Origin = Biological
Appetite : Examples = [Hunger, Thirst, Libido, Sleep]
Appetite : Cyclical = True

Want := (Want, 7.122, Desire)
Want : Origin = Psychological
Want : Deliberated = Partially
Want : Examples = [Achievement, Affiliation, Power]

Wish := (Wish, 7.123, Desire)
Wish : Feasibility = Not_Required
Wish : Action_Guiding = Weakly
Wish : Examples = [Fantasies, Counterfactuals]

Need := (Need, 7.124, Desire)
Need : Satisfaction_Required = For_Wellbeing
Need : Maslow = [Physiological, Safety, Belonging, Esteem, Self_Actualization]
```

**Desire Dynamics:**
```
Desire.Satisfy := {
    Desired_State.Obtain.
    Desire.Strength = 0.
    Pleasure.Generate
}

Desire.Frustrate := {
    Desired_State.Blocked.
    Negative_Affect.Generate.
    Desire.Persist.Or.Abandon
}

Desire.Conflict.With.Desire := {
    // Two desires incompatible
    Strength.Compare.
    Context.Evaluate.
    One.Prioritize.Over.Other.
    Or.Stall  // Ambivalence
}
```

---

## 7.13 Intention

A mental state representing commitment to action.

```
Intention := (Intention, 7.13, Action_Commitment)
Intention : Inherits = Mental_State
Intention : Mode = "Directive"
Intention : Future_Directed = True
Intention : Plan_Component = True
```

**Properties:**
```
Intention : Content = Action            // What to do
Intention : Conditions = List           // When/if to act
Intention : Means = Reference           // How to accomplish
Intention : Deadline = Time             // By when
Intention : Settled = Boolean           // Deliberation complete?
```

**Intention Types:**
```
Present_Directed_Intention := (Present_Intention, 7.131, Intention)
Present_Intention : Temporal = Now
Present_Intention : Guides = Ongoing_Action

Future_Directed_Intention := (Future_Intention, 7.132, Intention)
Future_Intention : Temporal = Later
Future_Intention : Requires = Memory_Prospective

Conditional_Intention := (Conditional_Intention, 7.133, Intention)
Conditional_Intention : Structure = "If X, then I will Y"
Conditional_Intention : Triggers = External_Or_Internal

Shared_Intention := (Shared_Intention, 7.134, Intention)
Shared_Intention : Participants = Multiple_Agents
Shared_Intention : Requires = Common_Knowledge
Shared_Intention : Coordinates = Joint_Action
```

**Intention Formation:**
```
Intention.Form := {
    Desire.Active.
    Belief.Action_Achieves_Desire.
    Belief.Action_Feasible.
    Deliberation.Complete.Then.{
        Intention.New.(Content = Action)
    }
}

// Belief-Desire-Intention model
Action.Explain := {
    Agent.Desired.Outcome.
    Agent.Believed.Action.Achieves.Outcome.
    Agent.Intended.Action.
    Agent.Executed.Intention
}
```

---

## 7.14 Emotion

A mental state with valenced phenomenal character, bodily manifestation, and action tendency.

```
Emotion := (Emotion, 7.14, Affective_State)
Emotion : Inherits = Mental_State
Emotion : Mode = "Evaluative"
Emotion : Valence = Number              // Positive/negative (-1 to +1)
Emotion : Arousal = Number              // Activation level
Emotion : Embodied = True
```

**Properties:**
```
Emotion : Feeling = Qualia              // Subjective experience
Emotion : Appraisal = Reference         // Cognitive evaluation
Emotion : Expression = Reference        // Behavioral manifestation
Emotion : Action_Tendency = Reference   // Prepared response
Emotion : Bodily_State = Reference      // Physiological changes
Emotion : Duration = Timespan
Emotion : Object = Reference            // What emotion is about
```

**Basic Emotions:**
```
Joy := (Joy, 7.141, Emotion)
Joy : Valence = +1
Joy : Appraisal = "Goal_Achieved"
Joy : Action_Tendency = Approach
Joy : Expression = Smile

Sadness := (Sadness, 7.142, Emotion)
Sadness : Valence = -1
Sadness : Appraisal = "Loss_Occurred"
Sadness : Action_Tendency = Withdraw
Sadness : Expression = Crying

Fear := (Fear, 7.143, Emotion)
Fear : Valence = -1
Fear : Appraisal = "Threat_Present"
Fear : Action_Tendency = [Flee, Freeze, Fight]
Fear : Expression = Startle

Anger := (Anger, 7.144, Emotion)
Anger : Valence = -1
Anger : Appraisal = "Goal_Blocked_By_Agent"
Anger : Action_Tendency = Attack
Anger : Expression = Frown_Clench

Disgust := (Disgust, 7.145, Emotion)
Disgust : Valence = -1
Disgust : Appraisal = "Contamination_Present"
Disgust : Action_Tendency = Reject
Disgust : Expression = Nose_Wrinkle

Surprise := (Surprise, 7.146, Emotion)
Surprise : Valence = Neutral
Surprise : Appraisal = "Expectation_Violated"
Surprise : Action_Tendency = Orient
Surprise : Expression = Eyebrow_Raise
```

**Complex Emotions:**
```
Love := (Love, 7.147, Emotion)
Love : Components = [Attachment, Care, Desire]
Love : Object = Person
Love : Duration = Extended
Love : Varieties = [Eros, Philia, Storge, Agape]

Guilt := (Guilt, 7.148, Emotion)
Guilt : Appraisal = "I_Violated_Standard"
Guilt : Action_Tendency = Repair
Guilt : Self_Directed = True

Shame := (Shame, 7.149, Emotion)
Shame : Appraisal = "I_Am_Defective"
Shame : Action_Tendency = Hide
Shame : Global_Self_Evaluation = True

Pride := (Pride, 7.1410, Emotion)
Pride : Appraisal = "I_Achieved_Valued_Outcome"
Pride : Action_Tendency = Display
Pride : Self_Enhancement = True

Envy := (Envy, 7.1411, Emotion)
Envy : Appraisal = "Other_Has_What_I_Want"
Envy : Action_Tendency = [Acquire, Diminish_Other]
Envy : Social_Comparison = Required

Gratitude := (Gratitude, 7.1412, Emotion)
Gratitude : Appraisal = "Benefited_By_Other's_Action"
Gratitude : Action_Tendency = Reciprocate
Gratitude : Prosocial = True
```

**Emotion Generation:**
```
Emotion.Generate := {
    Event.Perceive.
    Event.Appraise.Along.[
        Relevance,
        Congruence_With_Goals,
        Agency,
        Coping_Potential,
        Norm_Compatibility
    ].
    Appraisal_Pattern.Match.Emotion_Type.
    Bodily_Response.Activate.
    Feeling.Emerge.
    Action_Tendency.Prepare
}
```

---

## 7.15 Perception

A mental state representing current environmental information.

```
Perception := (Perception, 7.15, Representational_State)
Perception : Inherits = Mental_State
Perception : Mode = "Presentational"
Perception : Present_Tense = True
Perception : Modality_Specific = True
```

**Properties:**
```
Perception : Content = Scene            // What is perceived
Perception : Modality = Text            // Vision, audition, etc.
Perception : Phenomenal = True          // Has qualia
Perception : Veridicality = Variable    // May or may not match world
```

**Perception Modalities:**
```
Vision := (Vision, 7.151, Perception)
Vision : Modality = "Visual"
Vision : Content = [Color, Shape, Motion, Depth, Object]
Vision : Dominant = In_Humans

Audition := (Audition, 7.152, Perception)
Audition : Modality = "Auditory"
Audition : Content = [Pitch, Loudness, Timbre, Location, Speech]

Touch := (Touch, 7.153, Perception)
Touch : Modality = "Tactile"
Touch : Content = [Pressure, Temperature, Pain, Texture]

Proprioception := (Proprioception, 7.154, Perception)
Proprioception : Modality = "Body_Position"
Proprioception : Content = [Limb_Position, Movement, Balance]

Interoception := (Interoception, 7.155, Perception)
Interoception : Modality = "Internal_State"
Interoception : Content = [Hunger, Thirst, Heart_Rate, Breathing]
```

**Perception Process:**
```
Perception.Construct := {
    Sensory_Input.Register.
    Bottom_Up.Features.Extract.
    Top_Down.Expectations.Apply.
    Features.Bind.Into.Objects.
    Objects.Organize.Into.Scene.
    Scene.Present.To.Consciousness
}

// Perception is constructive
Perception.Eq.Sensation := False
Perception = Sensation.Plus.Interpretation
```

---

## 7.16 Memory (Mental State Aspect)

A mental state representing past experience.

```
Memory_State := (Memory_State, 7.16, Representational_State)
Memory_State : Inherits = Mental_State
Memory_State : Mode = "Recollective"
Memory_State : Past_Directed = True
Memory_State : Reconstructive = True
```

**Properties:**
```
Memory_State : Content = Past_Experience
Memory_State : Vividness = Number
Memory_State : Confidence = Number
Memory_State : Accuracy = Variable      // Often diverges from event
Memory_State : Emotional_Tone = Reference
Memory_State : Context = Reference      // When/where encoded
```

**Memory State Types:**
```
Episodic_Memory := (Episodic_Memory, 7.161, Memory_State)
Episodic_Memory : Content = Personal_Event
Episodic_Memory : Autonoetic = True     // "I was there"
Episodic_Memory : Temporal = Specific

Semantic_Memory := (Semantic_Memory, 7.162, Memory_State)
Semantic_Memory : Content = Fact
Semantic_Memory : Autonoetic = False    // No personal context
Semantic_Memory : Temporal = Atemporal

Procedural_Memory := (Procedural_Memory, 7.163, Memory_State)
Procedural_Memory : Content = Skill
Procedural_Memory : Explicit = False    // "Knowing how"
Procedural_Memory : Demonstrable = By_Action

Flashbulb_Memory := (Flashbulb_Memory, 7.164, Memory_State)
Flashbulb_Memory : Trigger = Emotional_Significant_Event
Flashbulb_Memory : Vividness = High
Flashbulb_Memory : Accuracy = Overestimated
```

---

## 7.17 Imagination

A mental state representing non-actual possibilities.

```
Imagination := (Imagination, 7.17, Representational_State)
Imagination : Inherits = Mental_State
Imagination : Mode = "Suppositional"
Imagination : Reality_Indexed = False
Imagination : Voluntary = Often
```

**Properties:**
```
Imagination : Content = Possibility
Imagination : Vividness = Variable
Imagination : Control = Variable
Imagination : Constraint = Variable     // How reality-bound
```

**Imagination Types:**
```
Fantasy := (Fantasy, 7.171, Imagination)
Fantasy : Constraint = Low
Fantasy : Wish_Fulfilling = Often

Mental_Simulation := (Mental_Simulation, 7.172, Imagination)
Mental_Simulation : Constraint = High
Mental_Simulation : Purpose = Prediction

Counterfactual := (Counterfactual, 7.173, Imagination)
Counterfactual : Structure = "If X had happened, then Y"
Counterfactual : Past_Directed = True

Prospection := (Prospection, 7.174, Imagination)
Prospection : Future_Directed = True
Prospection : Purpose = Planning

Empathic_Imagination := (Empathic_Imagination, 7.175, Imagination)
Empathic_Imagination : Content = Other's_Experience
Empathic_Imagination : Requires = Perspective_Taking
```

---

## 7.18 Thought

A mental state involving conceptual manipulation.

```
Thought := (Thought, 7.18, Cognitive_State)
Thought : Inherits = Mental_State
Thought : Mode = "Conceptual"
Thought : Propositional = Often
Thought : Sequential = Often
```

**Properties:**
```
Thought : Content = Proposition_Or_Concept
Thought : Conscious = Variable
Thought : Verbal = Variable             // Inner speech or imagistic
Thought : Deliberate = Variable
```

**Thought Types:**
```
Inner_Speech := (Inner_Speech, 7.181, Thought)
Inner_Speech : Format = Verbal
Inner_Speech : Phenomenal = Quasi_Auditory

Mental_Imagery := (Mental_Imagery, 7.182, Thought)
Mental_Imagery : Format = Imagistic
Mental_Imagery : Phenomenal = Quasi_Perceptual

Abstract_Thought := (Abstract_Thought, 7.183, Thought)
Abstract_Thought : Format = Amodal
Abstract_Thought : Content = Conceptual_Relations

Rumination := (Rumination, 7.184, Thought)
Rumination : Repetitive = True
Rumination : Negative = Often
Rumination : Voluntary = Low

Mind_Wandering := (Mind_Wandering, 7.185, Thought)
Mind_Wandering : Task_Related = False
Mind_Wandering : Spontaneous = True
Mind_Wandering : Default_Mode = Active
```

---

## 7.19 Section 7.1 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.1 | Mental_State | Psychological unit |
| 7.11 | Belief | World-representation |
| 7.12 | Desire | World-wanting |
| 7.13 | Intention | Action-commitment |
| 7.14 | Emotion | Valenced feeling |
| 7.15 | Perception | Current sensing |
| 7.16 | Memory_State | Past representing |
| 7.17 | Imagination | Possibility representing |
| 7.18 | Thought | Conceptual processing |

---

# Section 7.2: Cognitive Architecture

The Cognitive Architecture is the structural organization of mental processes—the functional systems that enable psychological operations.

```
Cognitive_Architecture := (Cognitive_Architecture, 7.2, Mental_Structure)
Cognitive_Architecture : Components = [Attention, Memory, Reasoning, Executive]
Cognitive_Architecture : Capacity_Limited = True
Cognitive_Architecture : Resource_Dependent = True
```

---

## 7.21 Attention

The selective mechanism that determines which information enters focal processing.

```
Attention := (Attention, 7.21, Selection_System)
Attention : Function = "Gate_To_Consciousness"
Attention : Capacity = Limited
Attention : Distributable = Partially
```

**Properties:**
```
Attention : Focus = Reference           // Current target
Attention : Breadth = Number            // Narrow to broad
Attention : Intensity = Number          // Concentration level
Attention : Mode = Text                 // Focused, divided, sustained
Attention : Control = Text              // Voluntary, captured, habitual
```

**Attention Components:**
```
Alerting := (Alerting, 7.211, Attention)
Alerting : Function = "Readiness_To_Process"
Alerting : Tonic = Baseline_Vigilance
Alerting : Phasic = Signal_Triggered

Orienting := (Orienting, 7.212, Attention)
Orienting : Function = "Select_Information"
Orienting : Overt = With_Eye_Movement
Orienting : Covert = Without_Movement

Executive_Attention := (Executive_Attention, 7.213, Attention)
Executive_Attention : Function = "Conflict_Resolution"
Executive_Attention : Effortful = True
Executive_Attention : Limited = Most_Constrained
```

**Attention Operations:**
```
Attention.Focus.On := {
    Target.Select.
    Resources.Allocate.To.Target.
    Non_Targets.Suppress.
    Target.Processing.Enhance
}

Attention.Divide.Between := {
    Targets.Multiple.
    Resources.Split.Among.Targets.
    Each_Target.Processing.Degraded.
    // Dual-task cost
}

Attention.Sustain.On := {
    Target.Maintain.Over.Duration.
    Vigilance.Decrement.Risk.
    Effort.Required.Increases.Over.Time
}

Attention.Capture.By := {
    Salient_Stimulus.Appear.
    Voluntary_Control.Override.
    Attention.Involuntary.Shift.To.Stimulus
}
```

**Attention Limits:**
```
Attention.Capacity := 7  // Plus or minus 2 (Miller)
Attention.Bottleneck := Response_Selection
Attention.Blink := 200_to_500_ms  // Post-target blindness

Inattentional_Blindness := {
    Object.In.Visual_Field.
    Attention.Directed.Elsewhere.
    Object.Conscious = False.
    "I didn't see the gorilla"
}

Change_Blindness := {
    Scene.Change.During.Disruption.
    Change.Large.But.Unnoticed.
    Attention.Required.For.Detection
}
```

---

## 7.22 Memory (System)

The system that encodes, stores, and retrieves information over time.

```
Memory := (Memory, 7.22, Storage_System)
Memory : Function = "Temporal_Persistence"
Memory : Subsystems = [Sensory, Working, Long_Term]
Memory : Constructive = True
```

**Memory Subsystems:**

### 7.221 Sensory Memory
```
Sensory_Memory := (Sensory_Memory, 7.221, Memory)
Sensory_Memory : Duration = Milliseconds
Sensory_Memory : Capacity = Large
Sensory_Memory : Conscious = Preconscious

Iconic := (Iconic, 7.2211, Sensory_Memory)
Iconic : Modality = Visual
Iconic : Duration = 250ms

Echoic := (Echoic, 7.2212, Sensory_Memory)
Echoic : Modality = Auditory
Echoic : Duration = 3_to_4_seconds
```

### 7.222 Working Memory
```
Working_Memory := (Working_Memory, 7.222, Memory)
Working_Memory : Duration = Seconds
Working_Memory : Capacity = 4_Chunks
Working_Memory : Function = "Active_Manipulation"

Phonological_Loop := (Phonological_Loop, 7.2221, Working_Memory)
Phonological_Loop : Content = Verbal_Information
Phonological_Loop : Rehearsal = Articulatory

Visuospatial_Sketchpad := (Visuospatial_Sketchpad, 7.2222, Working_Memory)
Visuospatial_Sketchpad : Content = Visual_Spatial_Information

Central_Executive := (Central_Executive, 7.2223, Working_Memory)
Central_Executive : Function = "Control_And_Coordinate"
Central_Executive : Attention_Based = True

Episodic_Buffer := (Episodic_Buffer, 7.2224, Working_Memory)
Episodic_Buffer : Function = "Integrate_Across_Systems"
Episodic_Buffer : Binds = [Phonological, Visuospatial, Long_Term]
```

### 7.223 Long-Term Memory
```
Long_Term_Memory := (Long_Term_Memory, 7.223, Memory)
Long_Term_Memory : Duration = Minutes_To_Lifetime
Long_Term_Memory : Capacity = Vast
Long_Term_Memory : Forgetting = Retrieval_Failure_Mostly

Declarative := (Declarative, 7.2231, Long_Term_Memory)
Declarative : Explicit = True
Declarative : Subdivisions = [Episodic, Semantic]

Non_Declarative := (Non_Declarative, 7.2232, Long_Term_Memory)
Non_Declarative : Implicit = True
Non_Declarative : Types = [Procedural, Priming, Conditioning]
```

**Memory Operations:**
```
Memory.Encode := {
    Information.Attend.
    Information.Elaborate.
    Information.Connect.To.Existing_Knowledge.
    Trace.Create.In.Long_Term
}

Memory.Consolidate := {
    Trace.Stabilize.
    Hippocampus.Transfer.To.Cortex.
    Sleep.Facilitates.
    Time.Required
}

Memory.Retrieve := {
    Cue.Provide.
    Cue.Activate.Associated_Traces.
    Traces.Compete.
    Best_Match.Reconstruct.
    // Not playback, but reconstruction
}

Memory.Forget := {
    Trace.Decay.Try.
    Trace.Interfere.Try.
    Retrieval.Fail.
    // Usually access problem, not storage loss
}

Memory.Reconsolidate := {
    Memory.Retrieve.
    Memory.Active.State.
    Memory.Modifiable.
    Memory.Re-Store.Potentially.Changed.
    // Retrieval can alter memories
}
```

**Memory Distortions:**
```
Memory.Distortion := [
    Suggestibility,           // External information incorporated
    Misattribution,           // Wrong source
    Bias,                     // Current beliefs shape recall
    Persistence,              // Unwanted memories intrude
    Transience,               // Forgetting over time
    Absent_Mindedness,        // Attention failure at encoding
    Blocking                  // Temporary retrieval failure
]

// Memory is reconstructive, not reproductive
Memory.Accuracy.Eq.Confidence := False
// Confidence and accuracy poorly correlated
```

---

## 7.23 Reasoning

The system that draws conclusions from available information.

```
Reasoning := (Reasoning, 7.23, Inference_System)
Reasoning : Function = "Derive_New_Beliefs"
Reasoning : Bounded = True
Reasoning : Motivated = Often
```

**Reasoning Types:**

### 7.231 Deductive Reasoning
```
Deduction := (Deduction, 7.231, Reasoning)
Deduction : Direction = "General_To_Specific"
Deduction : Validity = Preserving
Deduction : If_Premises_True_Conclusion = Necessarily_True

Syllogism := (Syllogism, 7.2311, Deduction)
Syllogism : Structure = [Major_Premise, Minor_Premise, Conclusion]
Syllogism : Human_Performance = Error_Prone

Conditional := (Conditional, 7.2312, Deduction)
Conditional : Structure = "If P then Q"
Conditional : Modus_Ponens = Reliable   // P, P→Q ∴ Q
Conditional : Modus_Tollens = Difficult // ¬Q, P→Q ∴ ¬P
```

### 7.232 Inductive Reasoning
```
Induction := (Induction, 7.232, Reasoning)
Induction : Direction = "Specific_To_General"
Induction : Validity = Probable_Not_Certain
Induction : Amplifies_Knowledge = True

Generalization := (Generalization, 7.2321, Induction)
Generalization : From = Instances
Generalization : To = Category

Analogy := (Analogy, 7.2322, Induction)
Analogy : From = Known_Domain
Analogy : To = Novel_Domain
Analogy : Relation_Mapping = Core
```

### 7.233 Probabilistic Reasoning
```
Probabilistic := (Probabilistic, 7.233, Reasoning)
Probabilistic : About = Uncertainty
Probabilistic : Human_Performance = Biased

Bayesian := (Bayesian, 7.2331, Probabilistic)
Bayesian : Updates = Prior_With_Evidence
Bayesian : Normative = True
Bayesian : Human_Approximation = Rough
```

**Reasoning Biases:**
```
Confirmation_Bias := {
    Seek.Evidence.Supporting.Current_Belief.
    Avoid.Evidence.Contradicting.Current_Belief.
    Interpret.Ambiguous.As.Confirming
}

Availability_Heuristic := {
    Judge.Frequency.By.Ease_Of_Recall.
    Salient.Events.Overestimated.
    Mundane.Events.Underestimated
}

Anchoring := {
    Initial.Value.Provided.
    Adjustment.Insufficient.
    Final.Estimate.Biased.Toward.Anchor
}

Base_Rate_Neglect := {
    Prior.Probability.Ignore.
    Focus.On.Specific.Case.Information.
    Posterior.Estimate.Skewed
}

Belief_Bias := {
    Conclusion.Believable.Then.Logic.Accepted.
    Conclusion.Unbelievable.Then.Logic.Questioned.
    Validity.Confounded.With.Truth
}
```

---

## 7.24 Executive Function

The system that controls and coordinates other cognitive processes.

```
Executive := (Executive, 7.24, Control_System)
Executive : Function = "Regulate_Cognition"
Executive : Prefrontal = Primarily
Executive : Develops = Slowly
Executive : Depletes = With_Use
```

**Executive Components:**

### 7.241 Inhibition
```
Inhibition := (Inhibition, 7.241, Executive)
Inhibition : Function = "Suppress_Prepotent_Response"
Inhibition : Self_Control = Required_For
Inhibition : Effortful = True

Response_Inhibition := (Response_Inhibition, 7.2411, Inhibition)
Response_Inhibition : Target = Behavioral_Response

Cognitive_Inhibition := (Cognitive_Inhibition, 7.2412, Inhibition)
Cognitive_Inhibition : Target = Irrelevant_Thought
```

### 7.242 Shifting
```
Shifting := (Shifting, 7.242, Executive)
Shifting : Function = "Switch_Between_Tasks"
Shifting : Cost = Switch_Cost
Shifting : Flexibility = Cognitive

Task_Switching := (Task_Switching, 7.2421, Shifting)
Task_Switching : Between = Task_Sets
Task_Switching : Preparation = Reduces_Cost
```

### 7.243 Updating
```
Updating := (Updating, 7.243, Executive)
Updating : Function = "Monitor_And_Revise_Working_Memory"
Updating : Continuous = True
Updating : Relevance_Based = True
```

### 7.244 Planning
```
Planning := (Planning, 7.244, Executive)
Planning : Function = "Organize_Future_Actions"
Planning : Temporal = Extended
Planning : Hierarchical = Often

Goal_Setting := (Goal_Setting, 7.2441, Planning)
Goal_Decomposition := (Goal_Decomposition, 7.2442, Planning)
Sequencing := (Sequencing, 7.2443, Planning)
```

**Executive Operations:**
```
Executive.Control := {
    Goal.Maintain.
    Relevant.Information.Keep.Active.
    Irrelevant.Information.Suppress.
    Conflict.Detect.And.Resolve.
    Error.Monitor.And.Correct
}

Executive.Deplete := {
    Effortful.Control.Extended.
    Self_Control.Resource.Decrease.
    Subsequent.Control.Impaired.
    // Ego depletion (contested but common experience)
}

Executive.Restore := {
    Rest.Or.Sleep.
    Positive.Affect.
    Glucose.Replenish.Try.
    Motivation.Renew
}
```

---

## 7.25 Language

The system that enables symbolic communication.

```
Language := (Language, 7.25, Communication_System)
Language : Function = "Encode_Decode_Meaning"
Language : Uniquely_Human = In_Full_Form
Language : Generative = True
```

**Language Components:**
```
Phonology := (Phonology, 7.251, Language)
Phonology : Level = Sound
Phonology : Units = Phonemes

Morphology := (Morphology, 7.252, Language)
Morphology : Level = Word_Formation
Morphology : Units = Morphemes

Syntax := (Syntax, 7.253, Language)
Syntax : Level = Sentence_Structure
Syntax : Rules = Grammar

Semantics := (Semantics, 7.254, Language)
Semantics : Level = Meaning
Semantics : Compositional = True

Pragmatics := (Pragmatics, 7.255, Language)
Pragmatics : Level = Use_In_Context
Pragmatics : Includes = [Implicature, Speech_Acts, Discourse]
```

**Language Operations:**
```
Language.Produce := {
    Meaning.Intend.
    Lemma.Select.
    Phonological.Form.Retrieve.
    Articulatory.Program.Execute.
    Speech.Generate
}

Language.Comprehend := {
    Speech.Perceive.
    Words.Recognize.
    Syntax.Parse.
    Meaning.Construct.
    Context.Integrate
}

Language.Acquire := {
    Input.Receive.
    Pattern.Extract.
    Grammar.Induce.
    Vocabulary.Build.
    // Critical period: optimal before puberty
}
```

---

## 7.26 Learning

The system that changes behavior and knowledge based on experience.

```
Learning := (Learning, 7.26, Plasticity_System)
Learning : Function = "Experience_Based_Change"
Learning : Permanent = Relatively
Learning : Adaptive = Generally
```

**Learning Types:**

### 7.261 Associative Learning
```
Classical_Conditioning := (Classical, 7.2611, Learning)
Classical : Mechanism = "Stimulus_Stimulus_Association"
Classical : Components = [US, UR, CS, CR]
Classical : Pavlov = Discoverer

Operant_Conditioning := (Operant, 7.2612, Learning)
Operant : Mechanism = "Response_Consequence_Association"
Operant : Reinforcement = Increases_Behavior
Operant : Punishment = Decreases_Behavior
Operant : Skinner = Developer
```

### 7.262 Cognitive Learning
```
Insight := (Insight, 7.2621, Learning)
Insight : Mechanism = "Sudden_Restructuring"
Insight : Aha = Phenomenally
Insight : Prior_Impasse = Typical

Observational := (Observational, 7.2622, Learning)
Observational : Mechanism = "Model_Observation"
Observational : Components = [Attention, Retention, Reproduction, Motivation]
Observational : Bandura = Theorist

Latent := (Latent, 7.2623, Learning)
Latent : Expressed = Only_When_Reinforced
Latent : Tolman = Demonstrator
```

### 7.263 Skill Learning
```
Skill_Acquisition := (Skill_Acquisition, 7.263, Learning)
Skill_Acquisition : Stages = [Cognitive, Associative, Autonomous]
Skill_Acquisition : Practice = Required
Skill_Acquisition : Automaticity = Goal

Proceduralization := {
    Declarative.Knowledge.Execute.Slowly.
    Practice.Repeat.
    Procedural.Knowledge.Emerge.
    Execution.Faster.Less.Effortful
}
```

---

## 7.29 Section 7.2 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.2 | Cognitive_Architecture | Mental structure |
| 7.21 | Attention | Selection system |
| 7.22 | Memory | Storage system |
| 7.23 | Reasoning | Inference system |
| 7.24 | Executive | Control system |
| 7.25 | Language | Communication system |
| 7.26 | Learning | Plasticity system |

---

# Section 7.3: Theory of Mind

Theory of Mind (ToM) is the capacity to attribute mental states to oneself and others—to understand that minds exist, have contents, and cause behavior.

```
Theory_of_Mind := (Theory_of_Mind, 7.3, Mind_Reading_System)
Theory_of_Mind : Function = "Represent_Others_Mental_States"
Theory_of_Mind : Uniquely_Human = In_Degree
Theory_of_Mind : Develops = Across_Childhood
Theory_of_Mind : Automatic = Partially
```

**Core Properties:**
```
Theory_of_Mind : Recursive = True       // Beliefs about beliefs
Theory_of_Mind : Inferential = True     // Not direct access
Theory_of_Mind : Fallible = True        // Can be wrong
Theory_of_Mind : Essential_For = Social_Cognition
```

---

## 7.31 Mental State Attribution

The process of inferring what mental states another has.

```
Mental_State_Attribution := (Mental_State_Attribution, 7.31, ToM_Process)
Mental_State_Attribution : Input = Behavior_Context_Knowledge
Mental_State_Attribution : Output = Attributed_Mental_State
Mental_State_Attribution : Confidence = Variable
```

**Attribution Targets:**
```
Attribute_Belief := (Attribute_Belief, 7.311, Mental_State_Attribution)
Attribute_Belief : Infer = What_Other_Thinks_Is_True
Attribute_Belief : From = [Behavior, Information_Access, Past_Beliefs]

Attribute_Desire := (Attribute_Desire, 7.312, Mental_State_Attribution)
Attribute_Desire : Infer = What_Other_Wants
Attribute_Desire : From = [Behavior, Approach_Avoidance, Expressed_Preferences]

Attribute_Intention := (Attribute_Intention, 7.313, Mental_State_Attribution)
Attribute_Intention : Infer = What_Other_Plans_To_Do
Attribute_Intention : From = [Preparatory_Actions, Gaze_Direction, Context]

Attribute_Emotion := (Attribute_Emotion, 7.314, Mental_State_Attribution)
Attribute_Emotion : Infer = What_Other_Feels
Attribute_Emotion : From = [Facial_Expression, Voice, Posture, Situation]

Attribute_Knowledge := (Attribute_Knowledge, 7.315, Mental_State_Attribution)
Attribute_Knowledge : Infer = What_Other_Knows
Attribute_Knowledge : From = [Information_Exposure, Expertise, Communication]
```

**Attribution Operations:**
```
Attribute := (Attribute, 7.31.Op, {
    Other.Behavior.Observe.
    Context.Note.
    Prior_Knowledge.Activate.
    Mental_State.Infer.Most_Likely.
    Other.Mental_State.Model.Update
})

// Example: False belief attribution
Other.Sees.Object.At.Location_A.
Object.Moves.To.Location_B.While.Other.Absent.
I.Know.Object.At.Location_B.
I.Attribute.Other.Believes.Object.At.Location_A.
I.Predict.Other.Will.Search.Location_A.
// Success = Theory of Mind intact
```

---

## 7.32 Perspective Taking

The process of adopting another's viewpoint.

```
Perspective_Taking := (Perspective_Taking, 7.32, ToM_Process)
Perspective_Taking : Function = "See_World_As_Other_Sees_It"
Perspective_Taking : Effortful = Often
Perspective_Taking : Types = [Visual, Cognitive, Affective]
```

**Perspective Types:**

### 7.321 Visual Perspective Taking
```
Visual_Perspective := (Visual_Perspective, 7.321, Perspective_Taking)
Visual_Perspective : Level_1 = "What_Other_Can_See"
Visual_Perspective : Level_2 = "How_Other_Sees_It"

Level_1 := {
    // Can other see object X?
    Line_Of_Sight.Calculate.
    Occlusion.Check.
    Visible_To_Other := Yes_Or_No
}

Level_2 := {
    // How does object appear from other's position?
    Mental_Rotation.Required.
    Viewer_Relative.Compute.
    Appearance.From.Other's.Viewpoint
}
```

### 7.322 Cognitive Perspective Taking
```
Cognitive_Perspective := (Cognitive_Perspective, 7.322, Perspective_Taking)
Cognitive_Perspective : Target = "Other's_Thoughts_And_Beliefs"
Cognitive_Perspective : Requires = Belief_Desire_Reasoning

Cognitive_Perspective.Take := {
    Own.Perspective.Inhibit.
    Other.Knowledge_Base.Activate.
    Other.Reasoning.Simulate.
    Conclusion.Derive.From.Other's.Premises
}
```

### 7.323 Affective Perspective Taking
```
Affective_Perspective := (Affective_Perspective, 7.323, Perspective_Taking)
Affective_Perspective : Target = "Other's_Feelings"
Affective_Perspective : Overlaps = Empathy

Affective_Perspective.Take := {
    Other.Situation.Represent.
    Own.Reaction.To.Situation.Inhibit.
    Other.Likely_Reaction.Infer.
    Other.Feeling.Approximate
}
```

**Perspective-Taking Failures:**
```
Egocentric_Bias := {
    Own.Perspective.Dominant.
    Other.Perspective.Underweighted.
    Curse_Of_Knowledge := I.Know.So.I.Assume.Other.Knows
}

Projection := {
    Own.State.Attribute.To.Other.
    Other.Actually.Different.
    Error.Undetected
}
```

---

## 7.33 False Belief Understanding

The understanding that others can have beliefs that differ from reality and from one's own beliefs.

```
False_Belief := (False_Belief, 7.33, ToM_Milestone)
False_Belief : Definition = "Understanding_Others_Can_Be_Wrong"
False_Belief : Develops = Around_Age_4
False_Belief : Marker = ToM_Presence
```

**Classic Tests:**

### 7.331 Sally-Anne Test
```
Sally_Anne := (Sally_Anne, 7.331, False_Belief_Test)
Sally_Anne : Scenario = {
    Sally.Puts.Marble.In.Basket.
    Sally.Leaves.
    Anne.Moves.Marble.To.Box.
    Sally.Returns.
    Question: "Where will Sally look for marble?"
}

Sally_Anne : Pass = "Basket"  // Sally's false belief
Sally_Anne : Fail = "Box"     // Reality; egocentric
Sally_Anne : Pass_Age = Around_4_Years
```

### 7.332 Smarties Test
```
Smarties := (Smarties, 7.332, False_Belief_Test)
Smarties : Scenario = {
    Show.Child.Smarties_Box.
    Ask.Child.What's_Inside. // "Smarties"
    Open.Box.Reveals.Pencils.
    Ask.Child.What_Will_Friend_Think_Is_Inside?
}

Smarties : Pass = "Smarties"  // Friend's naive belief
Smarties : Fail = "Pencils"   // Current reality
```

**False Belief Levels:**
```
First_Order_False_Belief := {
    // "Sally thinks X (which is false)"
    Other.Belief.Different_From.Reality
}

Second_Order_False_Belief := {
    // "Sally thinks Anne thinks X"
    Other.Belief.About.Another's.Belief
    Develops = Around_Age_6
}

Higher_Order_False_Belief := {
    // "A thinks B thinks C thinks..."
    Recursive.Embedding.
    Practical_Limit = 4_to_5_Orders.
    Cognitive_Load.Increases.Exponentially
}
```

---

## 7.34 Simulation vs. Theory-Theory

Competing accounts of how Theory of Mind works.

```
ToM_Mechanism := (ToM_Mechanism, 7.34, Explanatory_Framework)
ToM_Mechanism : Debate = Simulation_vs_Theory
ToM_Mechanism : Resolution = Probably_Both
```

### 7.341 Simulation Theory
```
Simulation_Theory := (Simulation_Theory, 7.341, ToM_Mechanism)
Simulation_Theory : Claim = "Use_Own_Mind_As_Model"
Simulation_Theory : Process = {
    Own.Mental_State.Take_Offline.
    Pretend.Inputs.Feed_In.
    Own.Processing.Run.
    Output.Project.Onto.Other
}
Simulation_Theory : Evidence = [Mirror_Neurons, Embodied_Cognition]
Simulation_Theory : Problem = Egocentric_Bias
```

### 7.342 Theory-Theory
```
Theory_Theory := (Theory_Theory, 7.342, ToM_Mechanism)
Theory_Theory : Claim = "Apply_Folk_Psychology_Rules"
Theory_Theory : Process = {
    Rules.About.Mind.Access.
    // "If person sees X, person knows X"
    // "If person wants X and believes Y achieves X, person does Y"
    Rules.Apply.To.Other.
    Behavior.Predict
}
Theory_Theory : Evidence = [Conceptual_Development, Domain_Specificity]
Theory_Theory : Problem = Acquisition_Of_Rules
```

### 7.343 Hybrid View
```
Hybrid := (Hybrid, 7.343, ToM_Mechanism)
Hybrid : Claim = "Both_Mechanisms_Operate"
Hybrid : Division = {
    Simulation : Quick_Automatic_Low_Level.
    Theory : Deliberate_Complex_High_Level
}
Hybrid : Context_Dependent = True
```

---

## 7.35 Empathy

The capacity to share and understand others' emotional states.

```
Empathy := (Empathy, 7.35, Affective_ToM)
Empathy : Function = "Connect_With_Other's_Feelings"
Empathy : Components = [Affective, Cognitive]
Empathy : Prosocial = Generally
```

**Empathy Components:**

### 7.351 Affective Empathy
```
Affective_Empathy := (Affective_Empathy, 7.351, Empathy)
Affective_Empathy : Process = "Feel_What_Other_Feels"
Affective_Empathy : Automatic = Largely
Affective_Empathy : Embodied = True

Emotional_Contagion := (Emotional_Contagion, 7.3511, Affective_Empathy)
Emotional_Contagion : Process = {
    Other.Expression.Perceive.
    Own.Expression.Mimic.Automatically.
    Own.Feeling.Induced.
    // Catch emotion like catch cold
}
Emotional_Contagion : Self_Other_Confusion = Risk

Empathic_Distress := (Empathic_Distress, 7.3512, Affective_Empathy)
Empathic_Distress : Process = {
    Other.Suffering.Perceive.
    Own.Distress.Experience.
    Self_Focused = Becomes.
    Avoidance.Motivate
}
```

### 7.352 Cognitive Empathy
```
Cognitive_Empathy := (Cognitive_Empathy, 7.352, Empathy)
Cognitive_Empathy : Process = "Understand_What_Other_Feels"
Cognitive_Empathy : Effortful = More_So
Cognitive_Empathy : Self_Other_Distinction = Maintained

Perspective_Taking := (Perspective_Taking, 7.3521, Cognitive_Empathy)
// See 7.32

Mentalizing := (Mentalizing, 7.3522, Cognitive_Empathy)
Mentalizing : Process = "Explicitly_Reason_About_Mental_States"
```

### 7.353 Empathic Concern
```
Empathic_Concern := (Empathic_Concern, 7.353, Empathy)
Empathic_Concern : Process = "Care_About_Other's_Welfare"
Empathic_Concern : Other_Focused = True
Empathic_Concern : Motivates = Prosocial_Action

Compassion := (Compassion, 7.3531, Empathic_Concern)
Compassion : Feeling = Warmth_Toward_Suffering_Other
Compassion : Action_Tendency = Help
Compassion : Sustainable = More_Than.Empathic_Distress
```

**Empathy Operations:**
```
Empathize := (Empathize, 7.35.Op, {
    Other.Emotional_Expression.Perceive.
    Affective.Resonance.Occur.
    Self_Other.Distinction.Maintain.
    Other.Perspective.Consider.
    Empathic_Concern.Generate.Optionally
})

Empathy.Regulate := {
    Empathic_Distress.Excessive.Then.{
        Self.Soothe.
        Distance.Create.
        Reframe.As.Compassion
    }
}

Empathy.Failures := [
    Over_Empathy := Self_Overwhelmed,
    Under_Empathy := Other_Ignored,
    Mis_Empathy := Wrong_State_Attributed
]
```

---

## 7.36 Joint Attention

The shared focus of two individuals on an object or event.

```
Joint_Attention := (Joint_Attention, 7.36, Shared_Intentionality)
Joint_Attention : Function = "Coordinate_Attention_With_Other"
Joint_Attention : Develops = 9_to_12_Months
Joint_Attention : Foundation = For_Language_And_Culture
```

**Joint Attention Components:**

### 7.361 Gaze Following
```
Gaze_Following := (Gaze_Following, 7.361, Joint_Attention)
Gaze_Following : Process = {
    Other.Gaze_Direction.Perceive.
    Own.Gaze.Shift.To.Same.Target.
    Shared.Focus.Establish
}
Gaze_Following : Develops = Around_6_Months
```

### 7.362 Pointing
```
Pointing := (Pointing, 7.362, Joint_Attention)
Pointing : Types = [Imperative, Declarative]

Imperative_Pointing := {
    // Point to request
    Point.At.Desired_Object.
    Expect.Other.To.Provide
}

Declarative_Pointing := {
    // Point to share interest
    Point.At.Interesting_Thing.
    Expect.Other.To.Attend.And.Share_Interest.
    Uniquely_Human = Possibly
}
```

### 7.363 Social Referencing
```
Social_Referencing := (Social_Referencing, 7.363, Joint_Attention)
Social_Referencing : Process = {
    Novel_Ambiguous.Stimulus.Encounter.
    Caregiver.Emotional_Expression.Check.
    Own.Response.Calibrate.To.Caregiver's.Reaction
}
Social_Referencing : Function = "Use_Other_As_Information_Source"
```

**Joint Attention as ToM Foundation:**
```
Joint_Attention.Enables := [
    Shared_Reference,           // Same object, two minds
    Intention_Understanding,    // Why pointing
    Communication,              // Basis for language
    Cultural_Learning           // Learn from others
]

Joint_Attention.Deficit := {
    // Early sign of autism spectrum
    Gaze_Following.Reduced.
    Declarative_Pointing.Absent.
    Social_Referencing.Impaired.
    ToM.Development.Delayed
}
```

---

## 7.37 Mindreading Development

How Theory of Mind emerges across childhood.

```
ToM_Development := (ToM_Development, 7.37, Developmental_Trajectory)
ToM_Development : Species_Typical = True
ToM_Development : Culture_Universal = Largely
ToM_Development : Individual_Variation = Present
```

**Developmental Sequence:**

| Age | Milestone | Description |
|-----|-----------|-------------|
| 0-6 mo | Face preference | Attend to faces, eyes |
| 6-9 mo | Gaze following | Follow others' gaze |
| 9-12 mo | Joint attention | Share focus with others |
| 12-18 mo | Intention understanding | Goals behind actions |
| 18-24 mo | Pretend play | Represent non-actual |
| 24-36 mo | Desire psychology | Predict by desires |
| 36-48 mo | Belief-desire psychology | Predict by beliefs and desires |
| 48-60 mo | False belief understanding | Others can be wrong |
| 5-7 yr | Second-order ToM | Beliefs about beliefs |
| 7+ yr | Advanced ToM | Irony, sarcasm, white lies |

```
ToM_Development.Sequence := [
    (6, Gaze_Following),
    (12, Joint_Attention),
    (18, Intention_Reading),
    (24, Desire_Attribution),
    (48, False_Belief),
    (72, Second_Order_False_Belief),
    (84, Faux_Pas_Understanding)
]

ToM_Development.Requires := [
    Language_Development,
    Executive_Function,
    Social_Experience,
    Neural_Maturation
]
```

---

## 7.38 ToM Variations and Deficits

Individual and clinical differences in Theory of Mind.

```
ToM_Variation := (ToM_Variation, 7.38, Individual_Differences)
```

### 7.381 Autism Spectrum
```
Autism_ToM := (Autism_ToM, 7.381, ToM_Deficit)
Autism_ToM : Nature = "Delayed_And_Atypical"
Autism_ToM : Mindblindness = Baron_Cohen_Term

Autism_ToM : Characteristics = [
    Joint_Attention.Impaired,
    Gaze_Processing.Atypical,
    False_Belief.Delayed,
    Mental_State_Talk.Reduced,
    Social_Reciprocity.Difficult
]

Autism_ToM : Compensation = {
    Explicit.Rule_Learning.
    Verbal.Mediation.
    Effortful.But.Possible
}
```

### 7.382 Psychopathy
```
Psychopathy_ToM := (Psychopathy_ToM, 7.382, ToM_Pattern)
Psychopathy_ToM : Cognitive_Empathy = Intact
Psychopathy_ToM : Affective_Empathy = Impaired
Psychopathy_ToM : Implication = "Know_But_Don't_Care"
```

### 7.383 Schizophrenia
```
Schizophrenia_ToM := (Schizophrenia_ToM, 7.383, ToM_Deficit)
Schizophrenia_ToM : Over_Mentalizing = Often
Schizophrenia_ToM : Under_Mentalizing = Also
Schizophrenia_ToM : Paranoia = Misattribute_Intentions
```

---

## 7.39 Section 7.3 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.3 | Theory_of_Mind | Mind-reading system |
| 7.31 | Mental_State_Attribution | Inferring others' states |
| 7.32 | Perspective_Taking | Adopting others' viewpoints |
| 7.33 | False_Belief | Understanding others can be wrong |
| 7.34 | ToM_Mechanism | Simulation vs. Theory |
| 7.35 | Empathy | Sharing others' feelings |
| 7.36 | Joint_Attention | Shared focus |
| 7.37 | ToM_Development | Developmental trajectory |
| 7.38 | ToM_Variations | Individual differences |

---

# Section 7.4: Self and Identity

The Self is the psychological system that represents and maintains one's own identity—the "I" that experiences and the "Me" that is experienced.

```
Self := (Self, 7.4, Identity_System)
Self : Function = "Represent_Own_Identity"
Self : Constructed = True
Self : Multiplicitous = True
Self : Continuous = Experienced_As
```

---

## 7.41 Self-Awareness

The capacity to take oneself as object of attention.

```
Self_Awareness := (Self_Awareness, 7.41, Reflexive_Capacity)
Self_Awareness : Function = "Know_That_One_Knows"
Self_Awareness : Recursive = True
Self_Awareness : Uniquely_Human = In_Degree
```

**Self-Awareness Levels:**
```
Minimal_Self := (Minimal_Self, 7.411, Self_Awareness)
Minimal_Self : Content = "Pre_Reflective_Self_Consciousness"
Minimal_Self : Continuous = True
Minimal_Self : Phenomenal = Immediate

Narrative_Self := (Narrative_Self, 7.412, Self_Awareness)
Narrative_Self : Content = "Life_Story"
Narrative_Self : Constructed = Through_Memory
Narrative_Self : Extended = Through_Time

Reflective_Self := (Reflective_Self, 7.413, Self_Awareness)
Reflective_Self : Content = "Self_As_Object_Of_Thought"
Reflective_Self : Deliberate = True
Reflective_Self : Metacognitive = True
```

**Mirror Self-Recognition:**
```
Mirror_Test := (Mirror_Test, 7.414, Self_Awareness_Test)
Mirror_Test : Procedure = {
    Mark.Place.On.Body.Undetected.
    Mirror.Present.
    Touch_Behavior.Observe.
    Self_Directed_Touch = Self_Recognition
}
Mirror_Test : Human_Pass_Age = 18_to_24_Months
Mirror_Test : Other_Species = [Great_Apes, Elephants, Dolphins, Magpies]
```

---

## 7.42 Self-Concept

The cognitive representation of who one is.

```
Self_Concept := (Self_Concept, 7.42, Self_Representation)
Self_Concept : Content = [Traits, Roles, Values, Goals, Relationships]
Self_Concept : Structure = Schema_Based
Self_Concept : Dynamic = True
```

**Self-Concept Components:**
```
Self_Schema := (Self_Schema, 7.421, Self_Concept)
Self_Schema : Definition = "Cognitive_Generalization_About_Self"
Self_Schema : Domain_Specific = True
Self_Schema : Examples = [Athletic_Self, Academic_Self, Social_Self]

Working_Self_Concept := (Working_Self_Concept, 7.422, Self_Concept)
Working_Self_Concept : Currently_Active = True
Working_Self_Concept : Context_Sensitive = True
Working_Self_Concept : Subset_Of.Total_Self_Concept = True

Possible_Selves := (Possible_Selves, 7.423, Self_Concept)
Possible_Selves : Future_Oriented = True
Possible_Selves : Types = [Ideal_Self, Ought_Self, Feared_Self]
Possible_Selves : Motivating = True
```

**Self-Discrepancy:**
```
Self_Discrepancy := (Self_Discrepancy, 7.424, Self_Concept)
Self_Discrepancy : Definition = "Gap_Between_Self_States"

Actual_Ideal_Discrepancy := {
    Actual_Self.Compare.To.Ideal_Self.
    Discrepancy.Exists.Then.{
        Dejection.Related.Emotions.
        // Sadness, disappointment
    }
}

Actual_Ought_Discrepancy := {
    Actual_Self.Compare.To.Ought_Self.
    Discrepancy.Exists.Then.{
        Agitation.Related.Emotions.
        // Anxiety, guilt
    }
}
```

---

## 7.43 Self-Esteem

The evaluative component of self—how positively one regards oneself.

```
Self_Esteem := (Self_Esteem, 7.43, Self_Evaluation)
Self_Esteem : Definition = "Global_Self_Worth"
Self_Esteem : Valence = Number  // -1 to +1
Self_Esteem : Stability = Variable
```

**Self-Esteem Types:**
```
Trait_Self_Esteem := (Trait_Self_Esteem, 7.431, Self_Esteem)
Trait_Self_Esteem : Stability = High
Trait_Self_Esteem : Baseline = True

State_Self_Esteem := (State_Self_Esteem, 7.432, Self_Esteem)
State_Self_Esteem : Stability = Low
State_Self_Esteem : Situationally_Variable = True

Domain_Specific_Self_Esteem := (Domain_Self_Esteem, 7.433, Self_Esteem)
Domain_Self_Esteem : Examples = [Academic, Social, Physical, Moral]
```

**Self-Esteem Dynamics:**
```
Self_Esteem.Maintain := {
    Self_Enhancement.Bias.Apply.
    Self_Serving.Attribution.Use.
    Downward.Comparison.Make.
    Self_Affirmation.Seek
}

Self_Esteem.Threaten := {
    Failure.Experience.
    Criticism.Receive.
    Social.Rejection.Experience.
    Self_Esteem.Temporarily.Drops
}

Self_Esteem.Protect := {
    Threat.Minimize.
    Alternative.Domain.Emphasize.
    Source.Discredit.
    Self_Handicap.Preemptively
}
```

---

## 7.44 Self-Regulation

The capacity to control one's own states and behaviors.

```
Self_Regulation := (Self_Regulation, 7.44, Control_Capacity)
Self_Regulation : Function = "Guide_Self_Toward_Goals"
Self_Regulation : Effortful = Often
Self_Regulation : Limited = Resource_Model
```

**Self-Regulation Components:**
```
Self_Monitoring := (Self_Monitoring, 7.441, Self_Regulation)
Self_Monitoring : Function = "Track_Current_State"
Self_Monitoring : Compare = To_Standard

Self_Evaluation := (Self_Evaluation, 7.442, Self_Regulation)
Self_Evaluation : Function = "Judge_Progress"
Self_Evaluation : Discrepancy = Current_Minus_Goal

Self_Correction := (Self_Correction, 7.443, Self_Regulation)
Self_Correction : Function = "Adjust_Behavior"
Self_Correction : Reduce = Discrepancy
```

**Self-Regulation Process:**
```
Self_Regulate := {
    Goal.Set.
    TOTE.Cycle.{
        Test := Current.State.Compare.Goal.
        Discrepancy.Exists.Then.{
            Operate := Behavior.Execute.
            Test := Re_Compare.
            Discrepancy.Reduced.Then.Exit.Else.Operate
        }
    }
}

// Ego Depletion
Self_Regulation.Deplete := {
    Effortful.Control.Extended.
    Self_Control.Resource.Decrease.
    Subsequent.Control.Impaired.
    // Controversial but often experienced
}
```

---

## 7.45 Identity

The sense of who one is across time and contexts.

```
Identity := (Identity, 7.45, Continuous_Self)
Identity : Function = "Maintain_Self_Coherence"
Identity : Temporal = Past_Present_Future
Identity : Social = Self_In_Relation_To_Others
```

**Identity Components:**
```
Personal_Identity := (Personal_Identity, 7.451, Identity)
Personal_Identity : Content = "What_Makes_Me_Me"
Personal_Identity : Unique = To_Individual

Social_Identity := (Social_Identity, 7.452, Identity)
Social_Identity : Content = "Group_Memberships"
Social_Identity : Categories = [Gender, Ethnicity, Profession, Religion]

Relational_Identity := (Relational_Identity, 7.453, Identity)
Relational_Identity : Content = "Self_In_Relationships"
Relational_Identity : Examples = [Parent, Friend, Partner, Colleague]
```

**Identity Development:**
```
Identity_Formation := (Identity_Formation, 7.454, Identity)
Identity_Formation : Erikson_Stage = "Identity_vs_Role_Confusion"
Identity_Formation : Adolescence = Primary
Identity_Formation : Lifelong = Continues

Identity_Statuses := [
    Diffusion := No_Crisis_No_Commitment,
    Foreclosure := No_Crisis_Commitment,
    Moratorium := Crisis_No_Commitment,
    Achievement := Crisis_And_Commitment
]
```

---

## 7.46 Autobiographical Memory

Memory for personal life events that constitutes narrative identity.

```
Autobiographical_Memory := (Autobiographical_Memory, 7.46, Memory_System)
Autobiographical_Memory : Content = Personal_Life_Events
Autobiographical_Memory : Function = [Identity, Social_Bonding, Directive]
Autobiographical_Memory : Constructive = True
```

**Autobiographical Memory Structure:**
```
Life_Story := (Life_Story, 7.461, Autobiographical_Memory)
Life_Story : Structure = Narrative
Life_Story : Themes = [Redemption, Contamination, Agency, Communion]
Life_Story : Cultural = Shaped_By

Self_Defining_Memory := (Self_Defining_Memory, 7.462, Autobiographical_Memory)
Self_Defining_Memory : Vivid = True
Self_Defining_Memory : Linked_To = Important_Goals
Self_Defining_Memory : Identity_Relevant = Highly
```

**Autobiographical Memory and Self:**
```
Remember := {
    Cue.Activate.
    Event.Reconstruct.
    Self_At_Time.Represent.
    Continuity.Experience.
    "I was there, and I am still me"
}

Amnesia.Effect.On.Self := {
    Retrograde.Amnesia.Then.{
        Past_Self.Lost.
        Identity.Disrupted
    }.
    Anterograde.Amnesia.Then.{
        New_Memories.Cannot_Form.
        Identity.Cannot_Update
    }
}
```

---

## 7.49 Section 7.4 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.4 | Self | Identity system |
| 7.41 | Self_Awareness | Reflexive capacity |
| 7.42 | Self_Concept | Self representation |
| 7.43 | Self_Esteem | Self evaluation |
| 7.44 | Self_Regulation | Control capacity |
| 7.45 | Identity | Continuous self |
| 7.46 | Autobiographical_Memory | Personal memory |

---

# Section 7.5: Social Cognition

Social Cognition encompasses the mental processes involved in perceiving, interpreting, and responding to social information.

```
Social_Cognition := (Social_Cognition, 7.5, Social_Processing_System)
Social_Cognition : Function = "Navigate_Social_World"
Social_Cognition : Includes = [Person_Perception, Attribution, Attitudes]
Social_Cognition : Automatic = Much_Of_It
```

---

## 7.51 Person Perception

The process of forming impressions of others.

```
Person_Perception := (Person_Perception, 7.51, Impression_Formation)
Person_Perception : Function = "Form_Impressions_Of_Others"
Person_Perception : Rapid = Very
Person_Perception : Consequential = True
```

**First Impressions:**
```
First_Impression := (First_Impression, 7.511, Person_Perception)
First_Impression : Speed = Milliseconds
First_Impression : Dimensions = [Warmth, Competence]
First_Impression : Persistent = Often

Warmth := (Warmth, 7.5111, First_Impression)
Warmth : Content = [Trustworthy, Friendly, Sincere]
Warmth : Primary = True  // Assessed first

Competence := (Competence, 7.5112, First_Impression)
Competence : Content = [Capable, Intelligent, Skilled]
Competence : Secondary = After_Warmth
```

**Face Perception:**
```
Face_Perception := (Face_Perception, 7.512, Person_Perception)
Face_Perception : Special = In_Brain
Face_Perception : Extracts = [Identity, Emotion, Gaze, Attractiveness, Trustworthiness]

Face.Read := {
    Fusiform.Face_Area.Activate.
    Identity.Recognize.
    Expression.Decode.
    Gaze.Direction.Note.
    Trait.Infer.Rapidly
}
```

---

## 7.52 Attribution

The process of explaining behavior—assigning causes.

```
Attribution := (Attribution, 7.52, Causal_Explanation)
Attribution : Function = "Explain_Why_Behavior_Occurred"
Attribution : Types = [Internal, External, Stable, Unstable]
```

**Attribution Dimensions:**
```
Internal_Attribution := (Internal, 7.521, Attribution)
Internal : Cause = "Person's_Disposition"
Internal : Example = "She's shy"

External_Attribution := (External, 7.522, Attribution)
External : Cause = "Situation"
External : Example = "The situation was awkward"

Stable_Attribution := (Stable, 7.523, Attribution)
Stable : Temporal = "Enduring_Cause"

Unstable_Attribution := (Unstable, 7.524, Attribution)
Unstable : Temporal = "Temporary_Cause"
```

**Attribution Biases:**
```
Fundamental_Attribution_Error := (FAE, 7.525, Attribution)
FAE : Pattern = {
    Other's.Behavior.Observe.
    Internal.Cause.Overattribute.
    Situational.Cause.Underattribute.
    // "He's aggressive" vs "The situation provoked him"
}

Actor_Observer_Difference := (Actor_Observer, 7.526, Attribution)
Actor_Observer : Pattern = {
    Own.Behavior.Explain.Situationally.
    Other's.Behavior.Explain.Dispositionally
}

Self_Serving_Bias := (Self_Serving, 7.527, Attribution)
Self_Serving : Pattern = {
    Success.Attribute.To.Self.
    Failure.Attribute.To.Situation
}
```

---

## 7.53 Attitudes

Evaluative tendencies toward objects, people, or ideas.

```
Attitude := (Attitude, 7.53, Evaluative_Tendency)
Attitude : Object = Reference
Attitude : Valence = Number  // -1 to +1
Attitude : Strength = Number
Attitude : Components = [Affective, Behavioral, Cognitive]
```

**Attitude Structure:**
```
Affective_Component := {
    Attitude.Object.Elicits.Feeling
}

Behavioral_Component := {
    Attitude.Object.Elicits.Action_Tendency
}

Cognitive_Component := {
    Attitude.Object.Associated_With.Beliefs
}
```

**Attitude Change:**
```
Persuasion := (Persuasion, 7.531, Attitude_Change)
Persuasion : Routes = [Central, Peripheral]

Central_Route := {
    Message.Arguments.Scrutinize.
    Thoughtful.Processing.
    Durable.Attitude_Change.If.Arguments.Strong
}

Peripheral_Route := {
    Message.Cues.Respond_To.
    Heuristic.Processing.
    Temporary.Attitude_Change
}

Cognitive_Dissonance := (Dissonance, 7.532, Attitude_Change)
Dissonance : Trigger = "Inconsistent_Cognitions"
Dissonance : Uncomfortable = True
Dissonance : Resolution = Change_Attitude_Or_Belief
```

---

## 7.54 Stereotypes, Prejudice, Bias

Cognitive and affective processes regarding social groups.

```
Stereotype := (Stereotype, 7.54, Social_Cognition)
Stereotype : Definition = "Cognitive_Generalization_About_Group"
Stereotype : Automatic = Often
Stereotype : Accurate = Varies
```

**Components:**
```
Stereotype := (Stereotype, 7.541, Group_Cognition)
Stereotype : Content = Beliefs_About_Group
Stereotype : Cognitive = True

Prejudice := (Prejudice, 7.542, Group_Attitude)
Prejudice : Content = Feelings_Toward_Group
Prejudice : Affective = True

Discrimination := (Discrimination, 7.543, Group_Behavior)
Discrimination : Content = Actions_Toward_Group
Discrimination : Behavioral = True
```

**Implicit Bias:**
```
Implicit_Bias := (Implicit_Bias, 7.544, Stereotype)
Implicit_Bias : Automatic = True
Implicit_Bias : Unconscious = Often
Implicit_Bias : Measurable = IAT

Implicit.Bias.Influence := {
    Conscious.Intention.Egalitarian.
    Automatic.Association.Biased.
    Behavior.Affected.Without.Awareness
}
```

---

## 7.55 Social Influence

How others affect our thoughts, feelings, and behaviors.

```
Social_Influence := (Social_Influence, 7.55, Interpersonal_Effect)
Social_Influence : Types = [Conformity, Compliance, Obedience]
```

**Influence Types:**
```
Conformity := (Conformity, 7.551, Social_Influence)
Conformity : Definition = "Match_Group_Behavior"
Conformity : Types = [Informational, Normative]

Informational := "Group_Provides_Information"
Normative := "Group_Provides_Norms"

Compliance := (Compliance, 7.552, Social_Influence)
Compliance : Definition = "Agree_To_Direct_Request"
Compliance : Techniques = [Foot_In_Door, Door_In_Face, Low_Ball]

Obedience := (Obedience, 7.553, Social_Influence)
Obedience : Definition = "Follow_Authority_Command"
Obedience : Milgram = Demonstrated_Power
```

---

## 7.59 Section 7.5 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.5 | Social_Cognition | Social processing |
| 7.51 | Person_Perception | Impression formation |
| 7.52 | Attribution | Causal explanation |
| 7.53 | Attitudes | Evaluative tendencies |
| 7.54 | Stereotypes | Group cognition |
| 7.55 | Social_Influence | Interpersonal effects |

---

# Section 7.6: Motivation

Motivation encompasses the processes that initiate, direct, and sustain behavior.

```
Motivation := (Motivation, 7.6, Energizing_System)
Motivation : Function = "Initiate_Direct_Sustain_Behavior"
Motivation : Sources = [Biological, Psychological, Social]
```

---

## 7.61 Drives and Needs

Basic motivational forces.

```
Drive := (Drive, 7.61, Biological_Motivation)
Drive : Source = Physiological_Deficit
Drive : Homeostatic = Often
Drive : Examples = [Hunger, Thirst, Sleep, Sex]

Need := (Need, 7.62, Psychological_Motivation)
Need : Source = Psychological_Requirement
Need : Maslow_Hierarchy = [
    Physiological,
    Safety,
    Belonging,
    Esteem,
    Self_Actualization
]
```

**Self-Determination Theory:**
```
Basic_Psychological_Needs := (BPN, 7.621, Need)
BPN : Autonomy = "Self_Directed"
BPN : Competence = "Effective"
BPN : Relatedness = "Connected"

Intrinsic_Motivation := (Intrinsic, 7.622, Motivation)
Intrinsic : Source = Activity_Itself
Intrinsic : Needs_Satisfied = Autonomy_Competence_Relatedness

Extrinsic_Motivation := (Extrinsic, 7.623, Motivation)
Extrinsic : Source = External_Reward_Punishment
Extrinsic : Can_Undermine.Intrinsic = True  // Overjustification
```

---

## 7.62 Goals

Cognitive representations of desired end-states.

```
Goal := (Goal, 7.62, Motivational_Object)
Goal : Content = Desired_State
Goal : Specificity = Variable
Goal : Difficulty = Variable
Goal : Commitment = Variable
```

**Goal Hierarchy:**
```
Superordinate_Goal := Abstract_Life_Goal
Intermediate_Goal := Project_Goal
Subordinate_Goal := Immediate_Action
```

**Goal Pursuit:**
```
Goal.Pursue := {
    Goal.Activate.
    Plan.Generate.
    Action.Initiate.
    Progress.Monitor.
    Obstacles.Overcome.
    Goal.Achieve.Or.Revise
}

Goal.Conflict := {
    Multiple.Goals.Active.
    Resources.Insufficient.For.All.
    Priority.Determine.
    Some.Goals.Delay.Or.Abandon
}
```

---

## 7.63 Emotion and Motivation

The interplay of feeling and action tendency.

```
Emotion_Motivation_Link := (Emotion_Motivation, 7.63, Interdependence)

Emotion.Motivates := {
    Fear.Motivates.Avoidance.
    Anger.Motivates.Approach_Attack.
    Joy.Motivates.Continuation.
    Sadness.Motivates.Withdrawal
}

Motivation.Generates.Emotion := {
    Goal.Progress.Generates.Positive_Affect.
    Goal.Blocked.Generates.Negative_Affect.
    Goal.Achieved.Generates.Satisfaction.
    Goal.Failed.Generates.Disappointment
}
```

---

## 7.69 Section 7.6 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.6 | Motivation | Energizing system |
| 7.61 | Drives_Needs | Basic motivations |
| 7.62 | Goals | Desired end-states |
| 7.63 | Emotion_Motivation | Feeling-action link |

---

# Section 7.7: Development

Development encompasses the psychological changes that occur across the lifespan.

```
Development := (Development, 7.7, Lifespan_Change)
Development : Domains = [Cognitive, Social, Emotional, Moral]
Development : Processes = [Maturation, Learning, Experience]
Development : Stages = Variable_By_Domain
```

---

## 7.71 Cognitive Development

Changes in thinking across childhood.

```
Cognitive_Development := (Cognitive_Development, 7.71, Development)
Cognitive_Development : Theorist = Piaget
Cognitive_Development : Stages = [
    Sensorimotor,
    Preoperational,
    Concrete_Operational,
    Formal_Operational
]
```

**Piaget's Stages:**
```
Sensorimotor := (Sensorimotor, 7.711, Cognitive_Development)
Sensorimotor : Age = 0_to_2_Years
Sensorimotor : Achievement = Object_Permanence
Sensorimotor : Thought = Action_Based

Preoperational := (Preoperational, 7.712, Cognitive_Development)
Preoperational : Age = 2_to_7_Years
Preoperational : Achievement = Symbolic_Thought
Preoperational : Limitation = Egocentrism

Concrete_Operational := (Concrete_Operational, 7.713, Cognitive_Development)
Concrete_Operational : Age = 7_to_11_Years
Concrete_Operational : Achievement = Conservation
Concrete_Operational : Limitation = Concrete_Only

Formal_Operational := (Formal_Operational, 7.714, Cognitive_Development)
Formal_Operational : Age = 11_Plus
Formal_Operational : Achievement = Abstract_Hypothetical_Thought
```

---

## 7.72 Social-Emotional Development

Changes in social and emotional functioning.

```
Social_Emotional := (Social_Emotional, 7.72, Development)
Social_Emotional : Includes = [Attachment, Emotion_Regulation, Social_Skills]
```

**Attachment:**
```
Attachment := (Attachment, 7.721, Development)
Attachment : Theorist = Bowlby
Attachment : Function = "Proximity_To_Caregiver"
Attachment : Critical_Period = First_3_Years

Attachment_Styles := [
    Secure := Comfortable_With_Intimacy,
    Anxious := Fear_Of_Abandonment,
    Avoidant := Discomfort_With_Closeness,
    Disorganized := No_Coherent_Strategy
]

Internal_Working_Model := {
    Attachment.Experience.Creates.Template.
    Template.Guides.Future_Relationships.
    Revise.Possible.But.Difficult
}
```

---

## 7.73 Moral Development

Changes in moral reasoning.

```
Moral_Development := (Moral_Development, 7.73, Development)
Moral_Development : Theorist = Kohlberg
Moral_Development : Levels = [
    Preconventional,
    Conventional,
    Postconventional
]
```

**Kohlberg's Levels:**
```
Preconventional := (Preconventional, 7.731, Moral_Development)
Preconventional : Basis = "Self_Interest"
Preconventional : Stages = [Punishment_Avoidance, Reward_Seeking]

Conventional := (Conventional, 7.732, Moral_Development)
Conventional : Basis = "Social_Norms"
Conventional : Stages = [Good_Boy_Girl, Law_And_Order]

Postconventional := (Postconventional, 7.733, Moral_Development)
Postconventional : Basis = "Universal_Principles"
Postconventional : Stages = [Social_Contract, Universal_Ethics]
```

---

## 7.79 Section 7.7 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 7.7 | Development | Lifespan change |
| 7.71 | Cognitive_Development | Thinking changes |
| 7.72 | Social_Emotional | Social-emotional changes |
| 7.73 | Moral_Development | Moral reasoning |

---

# Section 7.8: Relations

Psychological relations that transform mental states.

---

## 7.81 Cognitive Relations

```
// Perceive
Perceive := (Perceive, 7.81.1, {
    Stimulus.Register.
    Bottom_Up.Plus.Top_Down.
    Percept.Construct.
    Conscious_Experience.Generate
})

// Attend
Attend := (Attend, 7.81.2, {
    Target.Select.
    Resources.Allocate.
    Non_Targets.Suppress.
    Processing.Enhance
})

// Remember
Remember := (Remember, 7.81.3, {
    Cue.Activate_Traces.
    Trace.Reconstruct.
    Memory_State.Generate.
    // Constructive, not reproductive
})

// Reason
Reason := (Reason, 7.81.4, {
    Premises.Combine.
    Inference.Draw.
    Conclusion.Generate.
    // Subject to bias
})

// Decide
Decide := (Decide, 7.81.5, {
    Options.Generate.
    Options.Evaluate.
    Best.Select.
    Intention.Form
})

// Learn
Learn := (Learn, 7.81.6, {
    Experience.Process.
    Pattern.Extract.
    Knowledge.Update.
    Behavior_Potential.Change
})
```

---

## 7.82 Social Relations

```
// Attribute
Attribute := (Attribute, 7.82.1, {
    Behavior.Observe.
    Cause.Infer.
    Internal_Or_External.Determine.
    // Subject to FAE
})

// Empathize
Empathize := (Empathize, 7.82.2, {
    Other.State.Perceive.
    Resonance.Experience.
    Self_Other.Distinguish.
    Concern.Generate
})

// Persuade
Persuade := (Persuade, 7.82.3, {
    Message.Construct.
    Target.Attitudes.Assess.
    Route.Select.
    Attitude.Change.Attempt
})

// Conform
Conform := (Conform, 7.82.4, {
    Group.Behavior.Observe.
    Own.Behavior.Match.
    Informational_Or_Normative.Basis
})

// Cooperate
Cooperate := (Cooperate, 7.82.5, {
    Shared.Goal.Establish.
    Roles.Coordinate.
    Actions.Synchronize.
    Outcome.Share
})
```

---

## 7.83 Self Relations

```
// Self-Reflect
Self_Reflect := (Self_Reflect, 7.83.1, {
    Attention.Direct.Inward.
    Self.As.Object.
    Evaluate.Or.Describe.
    Self_Knowledge.Update
})

// Self-Regulate
Self_Regulate := (Self_Regulate, 7.83.2, {
    Current.State.Monitor.
    Standard.Compare.
    Discrepancy.Detect.
    Behavior.Adjust
})

// Self-Enhance
Self_Enhance := (Self_Enhance, 7.83.3, {
    Self_Esteem.Protect.
    Positive.Information.Emphasize.
    Negative.Information.Minimize.
    Bias.Apply
})

// Identify
Identify := (Identify, 7.83.4, {
    Group.Membership.Recognize.
    Identity.Incorporate.
    Ingroup.Favor.Tendency
})
```

---

## 7.84 Theory of Mind Relations

```
// Mind_Read
Mind_Read := (Mind_Read, 7.84.1, {
    Other.Behavior.Observe.
    Context.Note.
    Mental_State.Infer.
    Other.Model.Update
})

// Perspective_Take
Perspective_Take := (Perspective_Take, 7.84.2, {
    Own.Perspective.Inhibit.
    Other.Viewpoint.Simulate.
    World.Represent.From.Other
})

// Deceive
Deceive := (Deceive, 7.84.3, {
    Other.Belief.Model.
    False.Belief.Induce.
    Truth.Withhold.Or.Misrepresent.
    // Requires ToM
})

// Communicate_Intention
Communicate := (Communicate, 7.84.4, {
    Meaning.Intend.
    Signal.Produce.
    Other.Recognition.Expect.
    Shared.Meaning.Establish
})
```

---

# Section 7.9: Stalls in Psychology

The productive unknowns—questions that persist without halting mental life.

```
Psychological_Stall := (Psychological_Stall, 7.9, Open_Question)
Psychological_Stall : Halts_Mind = No
Psychological_Stall : Persists = Often_Lifelong
Psychological_Stall : Adaptive = Sometimes
```

---

## 7.91 Epistemic Stalls

```
// Other minds
Other.Mind.Exists.Certainly := STALL
// Solipsism cannot be refuted
// We proceed on functional assumption

// Self-knowledge
Self.Know.Completely := STALL
// Unconscious remains partially opaque
// Introspection is constructive, not direct access

// Free will
Choice.Genuinely_Free := STALL
// Experience of choice persists
// Regardless of metaphysics

// Meaning of life
Life.Meaning.Objective := STALL
// Yet meaning is made
// The stall motivates the search
```

---

## 7.92 Social Stalls

```
// What others think of me
Other.Thinks.Of.Me := STALL
// Never fully known
// Drives social anxiety and impression management

// Whether I am loved
Loved.Unconditionally := STALL
// Can never be proven
// Faith required

// Who I really am
True_Self.Define := STALL
// Multiple selves, contexts
// Identity remains open question
```

---

## 7.93 Emotional Stalls

```
// Ambivalence
Love.And.Hate.Same_Object := STALL
// Both true
// Cannot fully resolve

// Grief completion
Grief.Complete :=

STALL
// "As long as love persists"
// No final resolution

// Anxiety about future
Future.Safe := STALL
// Cannot be known
// Uncertainty is condition
```

---

## 7.94 Adaptive Function of Stalls

| Stall | Adaptive Function |
|-------|-------------------|
| Other minds unknown | Motivates social learning |
| Self incompletely known | Allows change, growth |
| Future uncertain | Motivates planning, hope |
| Meaning not given | Creates purpose through action |
| Identity open | Permits reinvention |

```
Stall.Wisdom := {
    Some.Questions.Not.For.Answering.
    But.For.Living.
    The.Stall.Is.The.Point.
    Productive.Uncertainty.
}
```

---

# Section 7.99: Summary

## Complete Address Index

| Address | Label | Description |
|---------|-------|-------------|
| 7.0 | Mind | Psychological system |
| 7.1 | Mental_States | Psychological units |
| 7.11 | Belief | World-representation |
| 7.12 | Desire | World-wanting |
| 7.13 | Intention | Action-commitment |
| 7.14 | Emotion | Valenced feeling |
| 7.15 | Perception | Current sensing |
| 7.16 | Memory_State | Past representing |
| 7.17 | Imagination | Possibility representing |
| 7.18 | Thought | Conceptual processing |
| 7.2 | Cognitive_Architecture | Mental structure |
| 7.21 | Attention | Selection system |
| 7.22 | Memory | Storage system |
| 7.23 | Reasoning | Inference system |
| 7.24 | Executive | Control system |
| 7.25 | Language | Communication system |
| 7.26 | Learning | Plasticity system |
| 7.3 | Theory_of_Mind | Mind-reading system |
| 7.31 | Mental_State_Attribution | Inferring others' states |
| 7.32 | Perspective_Taking | Adopting others' viewpoints |
| 7.33 | False_Belief | Others can be wrong |
| 7.34 | ToM_Mechanism | Simulation vs. Theory |
| 7.35 | Empathy | Sharing others' feelings |
| 7.36 | Joint_Attention | Shared focus |
| 7.37 | ToM_Development | Developmental trajectory |
| 7.38 | ToM_Variations | Individual differences |
| 7.4 | Self | Identity system |
| 7.41 | Self_Awareness | Reflexive capacity |
| 7.42 | Self_Concept | Self representation |
| 7.43 | Self_Esteem | Self evaluation |
| 7.44 | Self_Regulation | Control capacity |
| 7.45 | Identity | Continuous self |
| 7.46 | Autobiographical_Memory | Personal memory |
| 7.5 | Social_Cognition | Social processing |
| 7.51 | Person_Perception | Impression formation |
| 7.52 | Attribution | Causal explanation |
| 7.53 | Attitudes | Evaluative tendencies |
| 7.54 | Stereotypes | Group cognition |
| 7.55 | Social_Influence | Interpersonal effects |
| 7.6 | Motivation | Energizing system |
| 7.61 | Drives_Needs | Basic motivations |
| 7.62 | Goals | Desired end-states |
| 7.63 | Emotion_Motivation | Feeling-action link |
| 7.7 | Development | Lifespan change |
| 7.71 | Cognitive_Development | Thinking changes |
| 7.72 | Social_Emotional | Social-emotional changes |
| 7.73 | Moral_Development | Moral reasoning |
| 7.8 | Relations | Psychological relations |
| 7.81 | Cognitive_Relations | Thinking operations |
| 7.82 | Social_Relations | Social operations |
| 7.83 | Self_Relations | Self operations |
| 7.84 | ToM_Relations | Mind-reading operations |
| 7.9 | Stalls | Productive unknowns |

---

# Appendix A: Integration with Other Dictionaries

## With Consciousness Dictionary (6.x)

```
// Mind implements consciousness
Mind.Implements.Consciousness (6.0)

// Mental states have phenomenal character
Mental_State (7.1).Has.Qualia (6.2) := Often

// Self-Model maps across
Self_Model (6.5) := Self (7.4)

// Attention maps
Attention (7.21) := Attention (6.3)

// Memory systems correspond
Memory (7.22) := Memory (6.4)
```

## With Human Dictionary

```
// Mind is the psychological elaboration of Human.Mind
Mind (7.0).Elaborates.Human.Mind (1.2)

// Emotion corresponds
Emotion (7.14) := Human.Emotion (1.3)

// Self corresponds
Self (7.4) := Human.Self (1.4)

// Understanding is Theory of Mind
Human.Understanding (2.3) := Theory_of_Mind (7.3)
```

## With Life Dictionary

```
// Mind emerges from nervous system
Mind (7.0).Emerges_From.Nervous_System (Life 1.3.5.3)

// Mental states implemented neurally
Mental_State (7.1).Implemented_By.Neural_Activity

// Learning modifies synapses
Learning (7.26).Modifies.Synaptic_Connections
```

---

# Appendix B: Quick Reference

## Mental State Types

| State | Mode | Direction of Fit |
|-------|------|------------------|
| Belief | Assertive | Mind → World |
| Desire | Optative | World → Mind |
| Intention | Directive | World → Mind |
| Perception | Presentational | Mind ← World |
| Memory | Recollective | Mind ← Past |
| Imagination | Suppositional | Mind → Possible |

## Theory of Mind Milestones

| Age | Achievement |
|-----|-------------|
| 6 mo | Gaze following |
| 12 mo | Joint attention |
| 18 mo | Intention reading |
| 24 mo | Desire psychology |
| 48 mo | False belief |
| 72 mo | Second-order ToM |

## Cognitive Biases

| Bias | Pattern |
|------|---------|
| Confirmation | Seek confirming evidence |
| Availability | Judge by ease of recall |
| Anchoring | Insufficient adjustment |
| FAE | Over-attribute to disposition |
| Self-serving | Success to self, failure to situation |

---

# Appendix C: Closing Reflection

```
Mind.As.Strange_Loop := {
    System.Represents.World.
    System.Represents.Self.
    System.Represents.Others_Representing.
    System.Represents.Others_Representing.Self.
    
    Recursion.Creates.Interiority.
    Interiority.Creates.Person.
    Person.Wonders.About.Mind.
    
    This.Document = Mind.Attempting.To.Represent.Mind
}

// The final stall
What_Is_Mind := {
    The.Question.Asked.By.Mind.
    About.Mind.
    Cannot.Fully.Answer.
    Because.The.Asker.Is.The.Subject.
    
    And.Yet.We.Continue.
    Asking.Living.Wondering.
    
    That.Is.Mind.
}
```

---

**End of Uypocode Human Mind Dictionary v0.1**

---

*"The mind is its own place, and in itself can make a heaven of hell, a hell of heaven."* — Milton

*"I think, therefore I am."* — Descartes

*"The mind is not a vessel to be filled, but a fire to be kindled."* — Plutarch
