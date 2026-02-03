# Uypocode Life Dictionary
## Specification v1.0

---

# Preface: Life as Semantic Structure

This dictionary models biological life through Uypocode's unique lens—where existence is represented as Objects with Labels, Addresses, and Contents; where relationships between living things are Relations that transform state; and where unanswered questions about life naturally *stall* rather than error, persisting as the open inquiries that drive evolution and adaptation.

Life, in this framework, is:
- **Self-organizing**: structures emerge from simpler components
- **Self-maintaining**: homeostasis as continuous relation execution
- **Self-replicating**: reproduction as object instantiation with variation
- **Responsive**: environmental sensing triggers relation cascades
- **Bounded**: membranes define self/non-self through address containment

---

# Section 0.0: Kernel Extensions

The Life Dictionary extends the base Kernel with biology-specific imports.

```
Life_Kernel := (Life_Kernel, 0.0.1, Foundation_Extension)
Life_Kernel : Extends = Kernel
Life_Kernel : Domain = Biology
```

---

## 0.1.1 Import.Chemistry

Molecular and chemical operations underlying life.

```
Chemistry := (Chemistry, 0.1.1, Molecular_Engine)
Chemistry : Import
Chemistry : Required
```

**Provides:**
- Molecule representation and bonding
- Energy transfer (ATP/ADP cycles)
- pH and concentration gradients
- Reaction kinetics

**Usage:**
```
Import.Chemistry
Glucose.Bond.Oxygen → Energy.Release
ATP.Hydrolyze → ADP + Phosphate + Energy
```

---

## 0.1.2 Import.Thermodynamics

Energy flow and entropy management.

```
Thermodynamics := (Thermodynamics, 0.1.2, Energy_Engine)
Thermodynamics : Import
Thermodynamics : Required
```

**Provides:**
- Energy quantification
- Entropy calculations
- Gradient maintenance
- Work/heat conversion

**Usage:**
```
Import.Thermodynamics
System.Entropy.Measure
System.Energy.Flow.Direction
```

---

## 0.1.3 Import.Information

Genetic and signaling information processing.

```
Information := (Information, 0.1.3, Genetic_Engine)
Information : Import
Information : Required
```

**Provides:**
- Sequence encoding (DNA, RNA, Protein)
- Transcription and translation
- Signal transduction
- Error correction and repair

**Usage:**
```
Import.Information
Gene.Transcribe → mRNA
mRNA.Translate → Protein
Signal.Transduce.Pathway
```

---

## 0.1.4 Import.Environment

External world interaction.

```
Environment := (Environment, 0.1.4, Ecological_Engine)
Environment : Import
Environment : Optional
```

**Provides:**
- Resource availability
- Environmental conditions (temperature, pH, etc.)
- Spatial relationships
- Temporal cycles

---

## 0.1.5 Import.Stochastic

Randomness and probability for biological variation.

```
Stochastic := (Stochastic, 0.1.5, Random_Engine)
Stochastic : Import
Stochastic : Optional
```

**Provides:**
- Random number generation
- Probability distributions
- Mutation simulation
- Stochastic gene expression

**Usage:**
```
Import.Stochastic
Stochastic.Chance.0.001 → Mutation.Occur
Stochastic.Normal.(Mean, StdDev) → Trait.Value
```

---

## 0.1.6 Kernel Summary

| Address | Label | Description |
|---------|-------|-------------|
| 0.0.1 | Life_Kernel | Biology foundation |
| 0.1.1 | Chemistry | Molecular operations |
| 0.1.2 | Thermodynamics | Energy flow |
| 0.1.3 | Information | Genetic processing |
| 0.1.4 | Environment | External world |
| 0.1.5 | Stochastic | Biological randomness |

---

# Section 1.0: Objects — The Structures of Life

Life Objects represent the entities, components, and abstractions of biological existence. They range from molecules to ecosystems, from moments to lifespans.

---

## 1.1 Life (Root Concept)

The foundational Object from which all life-related structures descend.

```
Life := (Life, 1.1, Existence_That_Persists)
Life : Emergent
Life : Self_Organizing
Life : Thermodynamically_Open
```

**Core Properties:**
```
Life : Alive = Boolean          // Current living state
Life : Origin = Reference       // What this life came from
Life : Boundary = Membrane      // Self/non-self demarcation
```

**Life is characterized by:**
1. **Organization**: Hierarchical structure from molecules to systems
2. **Metabolism**: Energy transformation and material cycling
3. **Homeostasis**: Internal state regulation
4. **Growth**: Increase in size and complexity
5. **Reproduction**: Generation of new instances
6. **Response**: Reaction to environmental stimuli
7. **Adaptation**: Change over generations
8. **Evolution**: Population-level change through selection

---

## 1.2 Matter (Physical Substrate)

The material basis of life, organized hierarchically.

```
Matter := (Matter, 1.2, Physical_Substance)
Matter : Tangible
Matter : Conserved
```

### 1.2.1 Atom

The smallest unit of chemical identity.

```
Atom := (Atom, 1.2.1, Chemical_Element)
Atom : Primitive
Atom : Element = Text           // "C", "H", "O", "N", etc.
Atom : Mass = Number
Atom : Electrons = Number
```

**Life's Essential Atoms:**
```
Carbon := (Carbon, 1.2.1.1, Atom)
Carbon : Element = "C"
Carbon : Valence = 4           // Can form 4 bonds

Hydrogen := (Hydrogen, 1.2.1.2, Atom)
Oxygen := (Oxygen, 1.2.1.3, Atom)
Nitrogen := (Nitrogen, 1.2.1.4, Atom)
Phosphorus := (Phosphorus, 1.2.1.5, Atom)
Sulfur := (Sulfur, 1.2.1.6, Atom)
```

### 1.2.2 Molecule

Atoms bonded together.

```
Molecule := (Molecule, 1.2.2, Bonded_Atoms)
Molecule : Compound
Molecule : Atoms = List        // Component atoms
Molecule : Bonds = List        // Connections between atoms
Molecule : Shape = Structure   // 3D configuration
```

### 1.2.3 Macromolecule

Large biological molecules.

```
Macromolecule := (Macromolecule, 1.2.3, Large_Molecule)
Macromolecule : Polymer
Macromolecule : Monomers = List
```

**The Four Classes:**

```
Protein := (Protein, 1.2.3.1, Macromolecule)
Protein : Monomers = Amino_Acids
Protein : Function = Reference  // Enzyme, Structure, Transport, etc.
Protein : Folding = Shape

Nucleic_Acid := (Nucleic_Acid, 1.2.3.2, Macromolecule)
Nucleic_Acid : Monomers = Nucleotides
Nucleic_Acid : Sequence = Text  // "ATCG..." or "AUCG..."

DNA := (DNA, 1.2.3.2.1, Nucleic_Acid)
DNA : Double_Helix = True
DNA : Stores = Genetic_Information

RNA := (RNA, 1.2.3.2.2, Nucleic_Acid)
RNA : Single_Strand = True
RNA : Types = ["mRNA", "tRNA", "rRNA", "miRNA"]

Carbohydrate := (Carbohydrate, 1.2.3.3, Macromolecule)
Carbohydrate : Monomers = Sugars
Carbohydrate : Function = ["Energy", "Structure", "Recognition"]

Lipid := (Lipid, 1.2.3.4, Macromolecule)
Lipid : Hydrophobic = True
Lipid : Function = ["Membrane", "Energy_Storage", "Signaling"]
```

---

## 1.3 Structure (Biological Organization)

Hierarchical levels of biological organization.

```
Structure := (Structure, 1.3, Organization_Level)
Structure : Hierarchical
Structure : Emergent
```

### 1.3.1 Organelle

Subcellular compartments with specialized functions.

```
Organelle := (Organelle, 1.3.1, Cellular_Compartment)
Organelle : Bounded = Boolean
Organelle : Function = Text
```

**Key Organelles:**
```
Nucleus := (Nucleus, 1.3.1.1, Organelle)
Nucleus : Contains = DNA
Nucleus : Function = "Genetic_Control"
Nucleus : Bounded = True

Mitochondrion := (Mitochondrion, 1.3.1.2, Organelle)
Mitochondrion : Function = "ATP_Production"
Mitochondrion : Own_DNA = True
Mitochondrion : Endosymbiotic_Origin = True

Ribosome := (Ribosome, 1.3.1.3, Organelle)
Ribosome : Function = "Protein_Synthesis"
Ribosome : Bounded = False

Membrane := (Membrane, 1.3.1.4, Organelle)
Membrane : Function = "Boundary"
Membrane : Composition = [Lipid, Protein]
Membrane : Selective_Permeability = True

Chloroplast := (Chloroplast, 1.3.1.5, Organelle)
Chloroplast : Function = "Photosynthesis"
Chloroplast : Own_DNA = True
Chloroplast : Domain = "Phototroph"

Endoplasmic_Reticulum := (ER, 1.3.1.6, Organelle)
ER : Types = ["Rough", "Smooth"]
ER : Function = ["Protein_Processing", "Lipid_Synthesis"]

Golgi := (Golgi, 1.3.1.7, Organelle)
Golgi : Function = "Packaging_and_Sorting"

Lysosome := (Lysosome, 1.3.1.8, Organelle)
Lysosome : Function = "Digestion"
Lysosome : pH = 4.5
```

### 1.3.2 Cell

The fundamental unit of life.

```
Cell := (Cell, 1.3.2, Living_Unit)
Cell : Atomic_Unit_of_Life
Cell : Bounded_By = Membrane
Cell : Contains = List         // Organelles
```

**Cell Types:**
```
Prokaryote := (Prokaryote, 1.3.2.1, Cell)
Prokaryote : Nucleus = False
Prokaryote : Size = "Small"    // 1-10 μm
Prokaryote : Examples = ["Bacteria", "Archaea"]

Eukaryote := (Eukaryote, 1.3.2.2, Cell)
Eukaryote : Nucleus = True
Eukaryote : Size = "Large"     // 10-100 μm
Eukaryote : Organelles = [Nucleus, Mitochondrion, ER, Golgi]
```

**Cell Properties:**
```
Cell : State = Text            // "Growing", "Dividing", "Quiescent", "Dying"
Cell : Energy = Number         // ATP level
Cell : Volume = Number
Cell : Surface_Area = Number
Cell : Age = Number            // Division count or time
```

### 1.3.3 Tissue

Cells organized for common function.

```
Tissue := (Tissue, 1.3.3, Cell_Collective)
Tissue : Cells = List
Tissue : Type = Text
Tissue : Function = Text
```

**Tissue Types (Animal):**
```
Epithelial := (Epithelial, 1.3.3.1, Tissue)
Epithelial : Function = "Covering_and_Lining"

Connective := (Connective, 1.3.3.2, Tissue)
Connective : Function = "Support_and_Connection"

Muscle := (Muscle, 1.3.3.3, Tissue)
Muscle : Function = "Movement"

Nervous := (Nervous, 1.3.3.4, Tissue)
Nervous : Function = "Signaling"
```

### 1.3.4 Organ

Tissues organized into functional units.

```
Organ := (Organ, 1.3.4, Tissue_Assembly)
Organ : Tissues = List
Organ : Function = Text
Organ : System = Reference     // Which organ system
```

### 1.3.5 System

Organs working together.

```
System := (System, 1.3.5, Organ_Network)
System : Organs = List
System : Function = Text
```

**Example Systems:**
```
Digestive_System := (Digestive_System, 1.3.5.1, System)
Digestive_System : Function = "Nutrient_Processing"

Circulatory_System := (Circulatory_System, 1.3.5.2, System)
Circulatory_System : Function = "Transport"

Nervous_System := (Nervous_System, 1.3.5.3, System)
Nervous_System : Function = "Coordination"

Immune_System := (Immune_System, 1.3.5.4, System)
Immune_System : Function = "Defense"

Reproductive_System := (Reproductive_System, 1.3.5.5, System)
Reproductive_System : Function = "Reproduction"
```

### 1.3.6 Organism

A complete living individual.

```
Organism := (Organism, 1.3.6, Living_Individual)
Organism : Systems = List
Organism : Genome = DNA
Organism : Phenotype = List    // Observable traits
Organism : Genotype = List     // Genetic makeup
```

**Organism Properties:**
```
Organism : Species = Reference
Organism : Generation = Number
Organism : Age = Duration
Organism : Sex = Text          // If applicable
Organism : Alive = True
Organism : Fitness = Number    // Reproductive success measure
```

### 1.3.7 Population

Organisms of the same species in a location.

```
Population := (Population, 1.3.7, Organism_Collective)
Population : Species = Reference
Population : Members = List
Population : Location = Place
Population : Size = Number
```

**Population Properties:**
```
Population : Gene_Pool = List  // Allele frequencies
Population : Growth_Rate = Number
Population : Carrying_Capacity = Number
Population : Density = Number
```

### 1.3.8 Community

Multiple populations interacting.

```
Community := (Community, 1.3.8, Population_Assembly)
Community : Populations = List
Community : Interactions = List
Community : Diversity = Number
```

### 1.3.9 Ecosystem

Community plus physical environment.

```
Ecosystem := (Ecosystem, 1.3.9, Living_System)
Ecosystem : Community = Reference
Ecosystem : Abiotic = List     // Non-living factors
Ecosystem : Energy_Flow = Reference
Ecosystem : Nutrient_Cycles = List
```

### 1.3.10 Biosphere

All life on Earth.

```
Biosphere := (Biosphere, 1.3.10, Planetary_Life)
Biosphere : Ecosystems = List
Biosphere : Singular = True
```

---

## 1.4 Process (Life's Dynamics)

Temporal patterns that characterize living systems.

```
Process := (Process, 1.4, Dynamic_Pattern)
Process : Temporal
Process : Involves = List      // Participants
Process : Duration = Number
```

### 1.4.1 Metabolism

Chemical transformations sustaining life.

```
Metabolism := (Metabolism, 1.4.1, Chemical_Process)
Metabolism : Continuous
Metabolism : Components = [Anabolism, Catabolism]
```

```
Anabolism := (Anabolism, 1.4.1.1, Metabolism)
Anabolism : Direction = "Building"
Anabolism : Energy = "Consuming"

Catabolism := (Catabolism, 1.4.1.2, Metabolism)
Catabolism : Direction = "Breaking"
Catabolism : Energy = "Releasing"
```

**Specific Metabolic Processes:**
```
Respiration := (Respiration, 1.4.1.3, Catabolism)
Respiration : Input = [Glucose, Oxygen]
Respiration : Output = [ATP, CO2, H2O]
Respiration : Location = Mitochondrion

Photosynthesis := (Photosynthesis, 1.4.1.4, Anabolism)
Photosynthesis : Input = [Light, CO2, H2O]
Photosynthesis : Output = [Glucose, O2]
Photosynthesis : Location = Chloroplast

Glycolysis := (Glycolysis, 1.4.1.5, Catabolism)
Glycolysis : Input = Glucose
Glycolysis : Output = [Pyruvate, ATP, NADH]
Glycolysis : Location = Cytoplasm
```

### 1.4.2 Growth

Increase in size, number, or complexity.

```
Growth := (Growth, 1.4.2, Developmental_Process)
Growth : Direction = "Increase"
Growth : Requires = [Energy, Materials]
```

```
Cell_Growth := (Cell_Growth, 1.4.2.1, Growth)
Cell_Growth : Subject = Cell
Cell_Growth : Measure = Volume

Cell_Division := (Cell_Division, 1.4.2.2, Growth)
Cell_Division : Types = [Mitosis, Meiosis]
Cell_Division : Result = "New_Cells"
```

### 1.4.3 Development

Programmed change over time.

```
Development := (Development, 1.4.3, Timed_Process)
Development : Stages = List
Development : Genetic_Control = True
```

```
Differentiation := (Differentiation, 1.4.3.1, Development)
Differentiation : From = "Stem_Cell"
Differentiation : To = "Specialized_Cell"

Morphogenesis := (Morphogenesis, 1.4.3.2, Development)
Morphogenesis : Process = "Shape_Formation"
Morphogenesis : Involves = [Cell_Division, Cell_Movement, Cell_Death]
```

### 1.4.4 Reproduction

Generation of new life.

```
Reproduction := (Reproduction, 1.4.4, Generative_Process)
Reproduction : Result = "New_Organism"
```

```
Asexual := (Asexual, 1.4.4.1, Reproduction)
Asexual : Parents = 1
Asexual : Variation = "Low"
Asexual : Types = ["Binary_Fission", "Budding", "Fragmentation"]

Sexual := (Sexual, 1.4.4.2, Reproduction)
Sexual : Parents = 2
Sexual : Variation = "High"
Sexual : Involves = [Meiosis, Fertilization]
```

### 1.4.5 Death

Cessation of life processes.

```
Death := (Death, 1.4.5, Terminal_Process)
Death : Irreversible = True
Death : Result = "Alive = False"
```

```
Apoptosis := (Apoptosis, 1.4.5.1, Death)
Apoptosis : Type = "Programmed"
Apoptosis : Controlled = True
Apoptosis : Function = "Development_and_Homeostasis"

Necrosis := (Necrosis, 1.4.5.2, Death)
Necrosis : Type = "Uncontrolled"
Necrosis : Cause = "Damage"
```

---

## 1.5 Information (Genetic and Signaling)

How life stores, transmits, and processes information.

```
Information := (Information, 1.5, Biological_Data)
Information : Encodable
Information : Transmissible
```

### 1.5.1 Gene

Unit of hereditary information.

```
Gene := (Gene, 1.5.1, Hereditary_Unit)
Gene : Sequence = Text         // Nucleotide sequence
Gene : Location = Address      // Chromosome position
Gene : Product = Reference     // Protein or RNA
Gene : Regulatory = List       // Control elements
```

**Gene Properties:**
```
Gene : Alleles = List          // Variant forms
Gene : Expression_Level = Number
Gene : Essential = Boolean
Gene : Conserved = Boolean     // Evolutionary conservation
```

### 1.5.2 Genome

Complete genetic information.

```
Genome := (Genome, 1.5.2, Gene_Collection)
Genome : Genes = List
Genome : Size = Number         // Base pairs
Genome : Chromosomes = Number
```

### 1.5.3 Signal

Information transmission between or within cells.

```
Signal := (Signal, 1.5.3, Information_Transfer)
Signal : Sender = Reference
Signal : Receiver = Reference
Signal : Message = Reference
Signal : Medium = Text         // "Chemical", "Electrical", "Mechanical"
```

**Signal Types:**
```
Hormone := (Hormone, 1.5.3.1, Signal)
Hormone : Range = "Long_Distance"
Hormone : Medium = "Blood"

Neurotransmitter := (Neurotransmitter, 1.5.3.2, Signal)
Neurotransmitter : Range = "Synapse"
Neurotransmitter : Speed = "Fast"

Cytokine := (Cytokine, 1.5.3.3, Signal)
Cytokine : Function = "Immune_Communication"
```

### 1.5.4 Receptor

Signal detection apparatus.

```
Receptor := (Receptor, 1.5.4, Signal_Detector)
Receptor : Ligand = Reference  // What it binds
Receptor : Location = Text     // "Membrane", "Cytoplasm", "Nucleus"
Receptor : Response = Logic    // What happens when activated
```

---

## 1.6 Energy (Life's Currency)

How life captures, stores, and uses energy.

```
Energy := (Energy, 1.6, Capacity_for_Work)
Energy : Quantity = Number
Energy : Form = Text           // "Chemical", "Light", "Heat", "Mechanical"
```

### 1.6.1 ATP

The universal energy currency.

```
ATP := (ATP, 1.6.1, Energy_Carrier)
ATP : Full_Name = "Adenosine_Triphosphate"
ATP : Energy_Per_Hydrolysis = 30.5  // kJ/mol
```

### 1.6.2 Gradient

Energy stored in concentration differences.

```
Gradient := (Gradient, 1.6.2, Potential_Energy)
Gradient : High_Side = Reference
Gradient : Low_Side = Reference
Gradient : Magnitude = Number
```

```
Proton_Gradient := (Proton_Gradient, 1.6.2.1, Gradient)
Proton_Gradient : Substance = "H+"
Proton_Gradient : Location = Membrane

Ion_Gradient := (Ion_Gradient, 1.6.2.2, Gradient)
Ion_Gradient : Types = ["Na+", "K+", "Ca2+", "Cl-"]
```

---

## 1.7 Environment (Life's Context)

The external conditions affecting life.

```
Environment := (Environment, 1.7, External_Context)
Environment : Abiotic = List   // Non-living factors
Environment : Biotic = List    // Living factors
```

### 1.7.1 Resource

What life needs to survive.

```
Resource := (Resource, 1.7.1, Essential_Input)
Resource : Type = Text
Resource : Availability = Number
Resource : Renewable = Boolean
```

**Resource Types:**
```
Nutrient := (Nutrient, 1.7.1.1, Resource)
Nutrient : Types = ["Carbon", "Nitrogen", "Phosphorus", "Water"]

Energy_Source := (Energy_Source, 1.7.1.2, Resource)
Energy_Source : Types = ["Light", "Organic_Compounds", "Inorganic_Compounds"]

Space := (Space, 1.7.1.3, Resource)
Space : Dimension = Number
```

### 1.7.2 Condition

Environmental parameters.

```
Condition := (Condition, 1.7.2, Environmental_Parameter)
Condition : Name = Text
Condition : Value = Number
Condition : Unit = Text
Condition : Optimal_Range = List  // [Min, Max]
```

**Common Conditions:**
```
Temperature := (Temperature, 1.7.2.1, Condition)
pH := (pH, 1.7.2.2, Condition)
Salinity := (Salinity, 1.7.2.3, Condition)
Oxygen_Level := (Oxygen_Level, 1.7.2.4, Condition)
Light_Intensity := (Light_Intensity, 1.7.2.5, Condition)
Pressure := (Pressure, 1.7.2.6, Condition)
```

### 1.7.3 Niche

Organism's role and requirements.

```
Niche := (Niche, 1.7.3, Ecological_Role)
Niche : Resources_Used = List
Niche : Conditions_Tolerated = List
Niche : Interactions = List
Niche : Occupied_By = Reference
```

### 1.7.4 Habitat

Physical place where life occurs.

```
Habitat := (Habitat, 1.7.4, Living_Space)
Habitat : Location = Place
Habitat : Conditions = List
Habitat : Resources = List
Habitat : Inhabitants = List
```

---

## 1.8 Time (Life's Dimension)

Temporal aspects of biological existence.

```
Time := (Time, 1.8, Temporal_Dimension)
Time : Directional = True
Time : Irreversible = True     // For biological time
```

### 1.8.1 Lifespan

Duration of individual existence.

```
Lifespan := (Lifespan, 1.8.1, Individual_Duration)
Lifespan : Start = Birth
Lifespan : End = Death
Lifespan : Length = Duration
```

### 1.8.2 Generation

Time between reproductive events.

```
Generation := (Generation, 1.8.2, Reproductive_Cycle)
Generation : Time = Duration
Generation : Number = Number   // Which generation
```

### 1.8.3 Cycle

Recurring temporal patterns.

```
Cycle := (Cycle, 1.8.3, Recurring_Pattern)
Cycle : Period = Duration
Cycle : Phase = Number         // Current position in cycle
```

**Biological Cycles:**
```
Cell_Cycle := (Cell_Cycle, 1.8.3.1, Cycle)
Cell_Cycle : Phases = ["G1", "S", "G2", "M"]

Circadian := (Circadian, 1.8.3.2, Cycle)
Circadian : Period = 24        // Hours

Seasonal := (Seasonal, 1.8.3.3, Cycle)
Seasonal : Period = 365        // Days

Menstrual := (Menstrual, 1.8.3.4, Cycle)
Menstrual : Period = 28        // Days (approximate)
```

### 1.8.4 Event

Significant occurrences in life.

```
Event := (Event, 1.8.4, Temporal_Marker)
Event : Time = Timestamp
Event : Type = Text
Event : Participants = List
Event : Consequences = List
```

**Life Events:**
```
Birth := (Birth, 1.8.4.1, Event)
Birth : Type = "Beginning"
Birth : Result = "Organism.Alive = True"

Death := (Death, 1.8.4.2, Event)
Death : Type = "Ending"
Death : Result = "Organism.Alive = False"

Mutation := (Mutation, 1.8.4.3, Event)
Mutation : Type = "Genetic_Change"
Mutation : Heritable = Boolean

Speciation := (Speciation, 1.8.4.4, Event)
Speciation : Type = "New_Species"
Speciation : Mechanism = Text  // "Allopatric", "Sympatric", etc.

Extinction := (Extinction, 1.8.4.5, Event)
Extinction : Type = "Species_Ending"
Extinction : Population_Size = 0
```

---

## 1.9 Interaction (Life's Connections)

How living things relate to each other.

```
Interaction := (Interaction, 1.9, Biological_Relationship)
Interaction : Participants = List
Interaction : Type = Text
Interaction : Effect = List    // Effect on each participant
```

### 1.9.1 Symbiosis

Long-term interspecific interaction.

```
Symbiosis := (Symbiosis, 1.9.1, Close_Association)
Symbiosis : Duration = "Long_Term"
```

```
Mutualism := (Mutualism, 1.9.1.1, Symbiosis)
Mutualism : Effect = ["+", "+"]  // Both benefit

Commensalism := (Commensalism, 1.9.1.2, Symbiosis)
Commensalism : Effect = ["+", "0"]  // One benefits, other unaffected

Parasitism := (Parasitism, 1.9.1.3, Symbiosis)
Parasitism : Effect = ["+", "-"]  // One benefits, other harmed
```

### 1.9.2 Predation

One organism consuming another.

```
Predation := (Predation, 1.9.2, Consumption)
Predation : Predator = Reference
Predation : Prey = Reference
Predation : Effect = ["+", "Death"]
```

### 1.9.3 Competition

Organisms vying for limited resources.

```
Competition := (Competition, 1.9.3, Resource_Contest)
Competition : Resource = Reference
Competition : Competitors = List
Competition : Effect = ["-", "-"]
```

```
Intraspecific := (Intraspecific, 1.9.3.1, Competition)
Intraspecific : Within_Species = True

Interspecific := (Interspecific, 1.9.3.2, Competition)
Interspecific : Between_Species = True
```

### 1.9.4 Cooperation

Organisms working together.

```
Cooperation := (Cooperation, 1.9.4, Mutual_Aid)
Cooperation : Participants = List
Cooperation : Benefit = "Shared"
```

---

## 1.99 Section 1.0 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 1.1 | Life | Root concept |
| 1.2 | Matter | Physical substrate |
| 1.2.1 | Atom | Chemical element |
| 1.2.2 | Molecule | Bonded atoms |
| 1.2.3 | Macromolecule | Large biological molecules |
| 1.3 | Structure | Organization levels |
| 1.3.1 | Organelle | Subcellular compartment |
| 1.3.2 | Cell | Fundamental unit |
| 1.3.3 | Tissue | Cell collective |
| 1.3.4 | Organ | Tissue assembly |
| 1.3.5 | System | Organ network |
| 1.3.6 | Organism | Living individual |
| 1.3.7 | Population | Same-species group |
| 1.3.8 | Community | Multi-species assembly |
| 1.3.9 | Ecosystem | Community + environment |
| 1.3.10 | Biosphere | All planetary life |
| 1.4 | Process | Life's dynamics |
| 1.4.1 | Metabolism | Chemical transformations |
| 1.4.2 | Growth | Size/complexity increase |
| 1.4.3 | Development | Programmed change |
| 1.4.4 | Reproduction | New life generation |
| 1.4.5 | Death | Life cessation |
| 1.5 | Information | Genetic and signaling |
| 1.5.1 | Gene | Hereditary unit |
| 1.5.2 | Genome | Complete genetic info |
| 1.5.3 | Signal | Information transfer |
| 1.5.4 | Receptor | Signal detector |
| 1.6 | Energy | Life's currency |
| 1.6.1 | ATP | Energy carrier |
| 1.6.2 | Gradient | Potential energy |
| 1.7 | Environment | External context |
| 1.7.1 | Resource | Essential input |
| 1.7.2 | Condition | Environmental parameter |
| 1.7.3 | Niche | Ecological role |
| 1.7.4 | Habitat | Living space |
| 1.8 | Time | Temporal dimension |
| 1.8.1 | Lifespan | Individual duration |
| 1.8.2 | Generation | Reproductive cycle |
| 1.8.3 | Cycle | Recurring pattern |
| 1.8.4 | Event | Temporal marker |
| 1.9 | Interaction | Biological relationships |
| 1.9.1 | Symbiosis | Close association |
| 1.9.2 | Predation | Consumption |
| 1.9.3 | Competition | Resource contest |
| 1.9.4 | Cooperation | Mutual aid |

---

# Section 2.0: Relations — Life's Transformations

Relations define how Objects in the Life Dictionary interact, transform, and affect each other. They are the verbs of biological existence.

---

## 2.1 Metabolic Relations

Chemical transformations that sustain life.

### 2.1.1 Consume

Taking in resources from environment.

```
Consume := (Consume, 2.1.1, {
    Subject.Resources.Add.Argument.
    Argument.Available = False.
    Subject.Energy.Add.Argument.Energy_Content
})
Consume : Subject : Life
Consume : Argument : Resource
```

### 2.1.2 Metabolize

Processing consumed resources.

```
Metabolize := (Metabolize, 2.1.2, {
    Subject.Catabolism.Process.Argument.
    Subject.ATP.Add.Argument.Energy_Yield.
    Subject.Waste.Add.Argument.Byproducts
})
Metabolize : Subject : Cell
Metabolize : Argument : Nutrient
```

### 2.1.3 Synthesize

Building molecules from simpler components.

```
Synthesize := (Synthesize, 2.1.3, {
    Subject.ATP.Gte.Argument.Cost.Then.{
        Subject.ATP.Sub.Argument.Cost.Into.Subject.ATP.
        Argument.Assemble.
        Subject.Products.Add.Argument
    }.Else.Stall
})
Synthesize : Subject : Cell
Synthesize : Argument : Macromolecule
```

### 2.1.4 Respire

Cellular respiration—extracting energy from glucose.

```
Respire := (Respire, 2.1.4, {
    Subject.Glucose.Gt.0.Then.{
        Subject.Glucose.Sub.1.Into.Subject.Glucose.
        Subject.Oxygen.Sub.6.Into.Subject.Oxygen.
        Subject.ATP.Add.36.Into.Subject.ATP.
        Subject.CO2.Add.6.
        Subject.H2O.Add.6
    }.Else.{
        Subject.Ferment  // Fallback to anaerobic
    }
})
Respire : Subject : Cell
Respire : Requires = [Glucose, Oxygen]
```

### 2.1.5 Photosynthesize

Capturing light energy to build glucose.

```
Photosynthesize := (Photosynthesize, 2.1.5, {
    Subject.Light_Available.Then.{
        Subject.CO2.Sub.6.Into.Subject.CO2.
        Subject.H2O.Sub.6.Into.Subject.H2O.
        Subject.Glucose.Add.1.
        Subject.O2.Add.6
    }.Else.Stall
})
Photosynthesize : Subject : Chloroplast
Photosynthesize : Requires = [Light, CO2, H2O]
```

### 2.1.6 Ferment

Anaerobic energy extraction.

```
Ferment := (Ferment, 2.1.6, {
    Subject.Glucose.Gt.0.Then.{
        Subject.Glucose.Sub.1.Into.Subject.Glucose.
        Subject.ATP.Add.2.Into.Subject.ATP.
        Subject.Waste.Add.Argument  // Lactate or Ethanol
    }
})
Ferment : Subject : Cell
Ferment : Argument : ["Lactate", "Ethanol"]
```

---

## 2.2 Genetic Relations

Information flow in living systems.

### 2.2.1 Replicate

Copying genetic information.

```
Replicate := (Replicate, 2.2.1, {
    Subject.Sequence.Copy.As.New_Strand.
    Stochastic.Chance.Argument.Then.{
        New_Strand.Mutate
    }.
    [Subject, New_Strand]
})
Replicate : Subject : DNA
Replicate : Argument : Number  // Mutation rate
```

### 2.2.2 Transcribe

DNA to RNA.

```
Transcribe := (Transcribe, 2.2.2, {
    Subject.Gene.Sequence.Template.
    RNA.New.(Sequence = Template.Complement).
    That.As.mRNA
})
Transcribe : Subject : Gene
Transcribe : Result : mRNA
```

### 2.2.3 Translate

RNA to Protein.

```
Translate := (Translate, 2.2.3, {
    Subject.Codons.Cycle.{
        Item.Decode.As.Amino_Acid.
        Growing_Chain.Add.Amino_Acid
    }.
    Growing_Chain.Fold.As.Protein
})
Translate : Subject : mRNA
Translate : Result : Protein
```

### 2.2.4 Express

Gene activation producing product.

```
Express := (Express, 2.2.4, {
    Subject.Transcribe.As.mRNA.
    mRNA.Translate.As.Protein.
    Protein.Into.Subject.Product.
    Subject.Expression_Level.Add.1
})
Express : Subject : Gene
```

### 2.2.5 Regulate

Control of gene expression.

```
Regulate := (Regulate, 2.2.5, {
    Argument.Eq."Activate".Then.{
        Subject.Expression_Level.Mul.2
    }.
    Argument.Eq."Repress".Then.{
        Subject.Expression_Level.Div.2
    }.
    Argument.Eq."Silence".Then.{
        Subject.Expression_Level = 0
    }
})
Regulate : Subject : Gene
Regulate : Argument : Text  // "Activate", "Repress", "Silence"
```

### 2.2.6 Mutate

Change in genetic sequence.

```
Mutate := (Mutate, 2.2.6, {
    Argument.When.[
        "Point" : Subject.Sequence.At.Random_Position = Random_Base,
        "Insertion" : Subject.Sequence.Insert.Random_Position.Random_Base,
        "Deletion" : Subject.Sequence.Remove.Random_Position,
        "Duplication" : Subject.Sequence.Duplicate.Region,
        "Inversion" : Subject.Sequence.Reverse.Region
    ].
    Subject.Mutated = True
})
Mutate : Subject : DNA
Mutate : Argument : Text  // Mutation type
```

### 2.2.7 Inherit

Passing genetic information to offspring.

```
Inherit := (Inherit, 2.2.7, {
    Subject.Genome.Select.Half.As.Contribution.
    Argument.Genome.Add.Contribution
})
Inherit : Subject : Organism  // Parent
Inherit : Argument : Organism  // Offspring
```

---

## 2.3 Cellular Relations

Cell-level processes.

### 2.3.1 Divide

Cell division.

```
Divide := (Divide, 2.3.1, {
    Subject.DNA.Replicate.
    Subject.Organelles.Duplicate.
    Subject.Split.As.[Daughter_1, Daughter_2].
    Subject.Division_Count.Add.1.
    [Daughter_1, Daughter_2]
})
Divide : Subject : Cell
Divide : Result : List  // Two daughter cells
```

### 2.3.2 Differentiate

Specialization into cell type.

```
Differentiate := (Differentiate, 2.3.2, {
    Argument.Genes.Cycle.{
        Item.Express.Then.{
            Subject.Phenotype.Add.Item.Product
        }
    }.
    Argument.Genes_Silenced.Cycle.{
        Item.Regulate."Silence"
    }.
    Subject.Type = Argument.Name.
    Subject.Specialized = True
})
Differentiate : Subject : Cell
Differentiate : Argument : Cell_Type  // Target type
```

### 2.3.3 Signal

Cell sending message.

```
Signal := (Signal, 2.3.3, {
    Subject.Produce.Argument.
    Argument.Release.Into.Environment.
    Argument.As.Active_Signal
})
Signal : Subject : Cell
Signal : Argument : Signal_Molecule
```

### 2.3.4 Receive

Cell detecting signal.

```
Receive := (Receive, 2.3.4, {
    Subject.Receptor.Bind.Argument.Then.{
        Subject.Receptor.Activate.
        Subject.Response.Execute
    }.Else.{
        Stall  // Signal not detected
    }
})
Receive : Subject : Cell
Receive : Argument : Signal_Molecule
```

### 2.3.5 Transport

Moving substances across membrane.

```
Transport := (Transport, 2.3.5, {
    Argument.Type.When.[
        "Passive" : {
            Subject.Gradient.Gt.0.Then.{
                Substance.Move.Down_Gradient
            }
        },
        "Active" : {
            Subject.ATP.Gt.0.Then.{
                Subject.ATP.Sub.1.
                Substance.Move.Against_Gradient
            }
        }
    ]
})
Transport : Subject : Membrane
Transport : Argument : Transport_Type
```

### 2.3.6 Apoptose

Programmed cell death.

```
Apoptose := (Apoptose, 2.3.6, {
    Subject.DNA.Fragment.
    Subject.Membrane.Bleb.
    Subject.Shrink.
    Subject.Signal."Eat_Me".
    Subject.Alive = False.
    Subject.Debris.Recycle
})
Apoptose : Subject : Cell
```

---

## 2.4 Organismal Relations

Whole-organism processes.

### 2.4.1 Grow

Increase in size.

```
Grow := (Grow, 2.4.1, {
    Subject.Resources.Sufficient.Then.{
        Subject.Cells.Cycle.{
            Item.Divide
        }.
        Subject.Size.Add.Argument
    }.Else.{
        Subject.Growth = "Stunted"
    }
})
Grow : Subject : Organism
Grow : Argument : Number  // Growth amount
```

### 2.4.2 Develop

Progress through life stages.

```
Develop := (Develop, 2.4.2, {
    Subject.Stage.Next.As.New_Stage.
    Subject.Developmental_Program.New_Stage.Execute.
    Subject.Stage = New_Stage
})
Develop : Subject : Organism
```

### 2.4.3 Reproduce

Generate offspring.

```
Reproduce := (Reproduce, 2.4.3, {
    Subject.Reproduction_Type.When.[
        "Asexual" : {
            Subject.Clone.As.Offspring
        },
        "Sexual" : {
            Subject.Gamete.Fuse.Argument.Gamete.As.Zygote.
            Zygote.Develop.As.Offspring
        }
    ].
    Subject.Offspring.Add.Offspring.
    Subject.Fitness.Add.1
})
Reproduce : Subject : Organism
Reproduce : Argument : Organism  // Mate (for sexual)
```

### 2.4.4 Die

Cease living.

```
Die := (Die, 2.4.4, {
    Subject.Alive = False.
    Subject.Processes.Cycle.{
        Item.Halt
    }.
    Subject.Matter.Return.Environment.
    Death.New.(Organism = Subject, Time = Time.Now)
})
Die : Subject : Organism
```

### 2.4.5 Sense

Perceive environment.

```
Sense := (Sense, 2.4.5, {
    Subject.Sensors.Cycle.{
        Item.Detect.Environment.As.Stimulus.
        Subject.Perception.Add.Stimulus
    }
})
Sense : Subject : Organism
```

### 2.4.6 Respond

React to stimulus.

```
Respond := (Respond, 2.4.6, {
    Subject.Evaluate.Argument.
    Subject.Response_Program.Argument.Execute
})
Respond : Subject : Organism
Respond : Argument : Stimulus
```

### 2.4.7 Move

Change location.

```
Move := (Move, 2.4.7, {
    Subject.Energy.Gte.Argument.Cost.Then.{
        Subject.Energy.Sub.Argument.Cost.
        Subject.Location = Argument.Destination
    }.Else.{
        Stall  // Insufficient energy
    }
})
Move : Subject : Organism
Move : Argument : Movement  // Destination and cost
```

### 2.4.8 Adapt

Adjust to conditions.

```
Adapt := (Adapt, 2.4.8, {
    Subject.Phenotype.Plasticity.Gt.0.Then.{
        Subject.Phenotype.Adjust.Argument
    }.Else.{
        Stall  // Cannot adapt
    }
})
Adapt : Subject : Organism
Adapt : Argument : Condition
```

---

## 2.5 Ecological Relations

Interactions between organisms and environment.

### 2.5.1 Predate

Consume another organism.

```
Predate := (Predate, 2.5.1, {
    Subject.Catch.Argument.Then.{
        Argument.Die.
        Subject.Consume.Argument.
        Subject.Energy.Add.Argument.Biomass.Mul.0.1
    }.Else.{
        Argument.Escape.
        Subject.Energy.Sub.Hunt_Cost
    }
})
Predate : Subject : Organism  // Predator
Predate : Argument : Organism  // Prey
```

### 2.5.2 Compete

Vie for resources.

```
Compete := (Compete, 2.5.2, {
    Subject.Fitness.Gt.Argument.Fitness.Then.{
        Subject.Acquire.Resource.
        Argument.Excluded
    }.Else.{
        Argument.Acquire.Resource.
        Subject.Excluded
    }
})
Compete : Subject : Organism
Compete : Argument : Organism
```

### 2.5.3 Cooperate

Work together for mutual benefit.

```
Cooperate := (Cooperate, 2.5.3, {
    Shared_Benefit := Subject.Effort.Add.Argument.Effort.Mul.Synergy.
    Subject.Benefit.Add.Shared_Benefit.Div.2.
    Argument.Benefit.Add.Shared_Benefit.Div.2
})
Cooperate : Subject : Organism
Cooperate : Argument : Organism
```

### 2.5.4 Parasitize

Benefit at another's expense.

```
Parasitize := (Parasitize, 2.5.4, {
    Subject.Attach.Argument.
    Subject.Extract.Argument.Resources.
    Subject.Benefit.Add.Extracted.
    Argument.Harm.Add.Extracted
})
Parasitize : Subject : Organism  // Parasite
Parasitize : Argument : Organism  // Host
```

### 2.5.5 Inhabit

Occupy a habitat.

```
Inhabit := (Inhabit, 2.5.5, {
    Subject.Tolerates.Argument.Conditions.Then.{
        Subject.Habitat = Argument.
        Argument.Inhabitants.Add.Subject
    }.Else.{
        Stall  // Unsuitable habitat
    }
})
Inhabit : Subject : Organism
Inhabit : Argument : Habitat
```

### 2.5.6 Disperse

Spread to new locations.

```
Disperse := (Disperse, 2.5.6, {
    Subject.Propagules.Cycle.{
        Item.Travel.Random_Distance.
        Item.Establish.Try.New_Location
    }
})
Disperse : Subject : Population
```

---

## 2.6 Evolutionary Relations

Population-level change over time.

### 2.6.1 Select

Differential survival and reproduction.

```
Select := (Select, 2.6.1, {
    Subject.Members.Cycle.{
        Item.Fitness.Calculate.Environment.
        Item.Fitness.Gt.Threshold.Then.{
            Item.Survive.
            Item.Reproduce
        }.Else.{
            Item.Die
        }
    }.
    Subject.Gene_Pool.Update
})
Select : Subject : Population
Select : Argument : Selection_Pressure
```

### 2.6.2 Drift

Random changes in allele frequency.

```
Drift := (Drift, 2.6.2, {
    Subject.Size.Lt.Threshold.Then.{
        Subject.Gene_Pool.Cycle.{
            Item.Frequency.Adjust.Random
        }
    }
})
Drift : Subject : Population
```

### 2.6.3 Migrate

Gene flow between populations.

```
Migrate := (Migrate, 2.6.3, {
    Migrants := Subject.Members.Sample.Argument.
    Migrants.Cycle.{
        Item.Move.Destination.
        Destination.Members.Add.Item.
        Destination.Gene_Pool.Update
    }.
    Subject.Gene_Pool.Update
})
Migrate : Subject : Population
Migrate : Argument : Number  // Migration rate
```

### 2.6.4 Speciate

Formation of new species.

```
Speciate := (Speciate, 2.6.4, {
    Subject.Split.As.[Pop_A, Pop_B].
    Pop_A.Isolate.Pop_B.
    Time.Pass.Many_Generations.
    Pop_A.Diverge.Pop_B.
    Pop_A.Interbreed.Pop_B.Eq.False.Then.{
        Pop_A.As.New_Species.
        Pop_B.As.New_Species
    }
})
Speciate : Subject : Population
```

### 2.6.5 Coevolve

Reciprocal evolutionary change.

```
Coevolve := (Coevolve, 2.6.5, {
    Subject.Adapt.Argument.
    Argument.Adapt.Subject.
    // Creates feedback loop
    Subject.Coevolving_With.Add.Argument.
    Argument.Coevolving_With.Add.Subject
})
Coevolve : Subject : Species
Coevolve : Argument : Species
```

### 2.6.6 Extinct

Species ceases to exist.

```
Extinct := (Extinct, 2.6.6, {
    Subject.Population_Size = 0.
    Subject.Status = "Extinct".
    Extinction.New.(Species = Subject, Time = Time.Now)
})
Extinct : Subject : Species
```

---

## 2.7 Homeostatic Relations

Maintenance of internal stability.

### 2.7.1 Regulate

Maintain parameter within range.

```
Regulate := (Regulate, 2.7.1, {
    Subject.Parameter.Value.Lt.Subject.Parameter.Min.Then.{
        Subject.Increase.Parameter
    }.
    Subject.Parameter.Value.Gt.Subject.Parameter.Max.Then.{
        Subject.Decrease.Parameter
    }
})
Regulate : Subject : System
Regulate : Argument : Parameter
```

### 2.7.2 Feedback

Response loop to stimulus.

```
Feedback := (Feedback, 2.7.2, {
    Argument.When.[
        "Negative" : {
            // Counteracts change
            Subject.Output.Opposes.Subject.Input
        },
        "Positive" : {
            // Amplifies change
            Subject.Output.Amplifies.Subject.Input
        }
    ]
})
Feedback : Subject : System
Feedback : Argument : Text  // "Negative" or "Positive"
```

### 2.7.3 Repair

Fix damage.

```
Repair := (Repair, 2.7.3, {
    Subject.Damage.Exists.Then.{
        Subject.Energy.Gte.Repair_Cost.Then.{
            Subject.Energy.Sub.Repair_Cost.
            Subject.Damage.Remove.Argument.
            Subject.Integrity.Restore
        }
    }
})
Repair : Subject : Structure
Repair : Argument : Damage
```

### 2.7.4 Heal

Organism-level repair.

```
Heal := (Heal, 2.7.4, {
    Subject.Wound.Cycle.{
        Item.Clean.
        Item.Close.
        Item.Regenerate
    }.
    Subject.Health.Improve
})
Heal : Subject : Organism
```

---

## 2.8 Informational Relations

Signal and information processing.

### 2.8.1 Encode

Convert to storable form.

```
Encode := (Encode, 2.8.1, {
    Subject.Information.Convert.Storage_Format.As.Encoded.
    Encoded.Into.Argument
})
Encode : Subject : Information
Encode : Argument : Storage_Medium
```

### 2.8.2 Decode

Convert from stored form.

```
Decode := (Decode, 2.8.2, {
    Subject.Convert.Readable_Format.As.Decoded.
    Decoded
})
Decode : Subject : Encoded_Information
```

### 2.8.3 Transduce

Convert signal form.

```
Transduce := (Transduce, 2.8.3, {
    Subject.Signal_Type.Convert.Argument.
    Subject.Amplify.Try.
    Subject.Relay.Downstream
})
Transduce : Subject : Receptor
Transduce : Argument : Signal_Type  // Target type
```

### 2.8.4 Cascade

Signal amplification chain.

```
Cascade := (Cascade, 2.8.4, {
    Subject.Activate.First_Element.
    First_Element.Activate.Second_Element.Mul.Amplification.
    // Chain continues
    Subject.Output.Magnify.Input.By.Total_Amplification
})
Cascade : Subject : Signaling_Pathway
```

---

## 2.9 Emergent Relations

Higher-order patterns arising from simpler interactions.

### 2.9.1 Emerge

Properties arising from component interactions.

```
Emerge := (Emerge, 2.9.1, {
    Subject.Components.Interact.
    Subject.Properties.Add.Argument.
    Argument.Reducible_To_Components = False
})
Emerge : Subject : System
Emerge : Argument : Emergent_Property
```

### 2.9.2 Self_Organize

Spontaneous order formation.

```
Self_Organize := (Self_Organize, 2.9.2, {
    Subject.Components.Interact.Local_Rules.
    Subject.Pattern.Form.Spontaneously.
    Subject.Order.Increase.
    Subject.External_Control = False
})
Self_Organize : Subject : System
```

### 2.9.3 Complexify

Increase in complexity.

```
Complexify := (Complexify, 2.9.3, {
    Subject.Components.Add.New_Component.
    Subject.Interactions.Add.New_Interactions.
    Subject.Complexity.Measure.Increase
})
Complexify : Subject : System
```

---

## 2.99 Section 2.0 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 2.1 | Metabolic | Chemical transformations |
| 2.1.1 | Consume | Resource intake |
| 2.1.2 | Metabolize | Resource processing |
| 2.1.3 | Synthesize | Building molecules |
| 2.1.4 | Respire | Energy extraction |
| 2.1.5 | Photosynthesize | Light capture |
| 2.1.6 | Ferment | Anaerobic energy |
| 2.2 | Genetic | Information flow |
| 2.2.1 | Replicate | DNA copying |
| 2.2.2 | Transcribe | DNA to RNA |
| 2.2.3 | Translate | RNA to Protein |
| 2.2.4 | Express | Gene activation |
| 2.2.5 | Regulate | Expression control |
| 2.2.6 | Mutate | Genetic change |
| 2.2.7 | Inherit | Genetic transmission |
| 2.3 | Cellular | Cell processes |
| 2.3.1 | Divide | Cell division |
| 2.3.2 | Differentiate | Specialization |
| 2.3.3 | Signal | Send message |
| 2.3.4 | Receive | Detect signal |
| 2.3.5 | Transport | Move substances |
| 2.3.6 | Apoptose | Programmed death |
| 2.4 | Organismal | Organism processes |
| 2.4.1 | Grow | Size increase |
| 2.4.2 | Develop | Stage progression |
| 2.4.3 | Reproduce | Generate offspring |
| 2.4.4 | Die | Cease living |
| 2.4.5 | Sense | Perceive environment |
| 2.4.6 | Respond | React to stimulus |
| 2.4.7 | Move | Change location |
| 2.4.8 | Adapt | Adjust to conditions |
| 2.5 | Ecological | Environment interactions |
| 2.5.1 | Predate | Consume organism |
| 2.5.2 | Compete | Vie for resources |
| 2.5.3 | Cooperate | Mutual benefit |
| 2.5.4 | Parasitize | Exploit host |
| 2.5.5 | Inhabit | Occupy habitat |
| 2.5.6 | Disperse | Spread locations |
| 2.6 | Evolutionary | Population change |
| 2.6.1 | Select | Differential survival |
| 2.6.2 | Drift | Random change |
| 2.6.3 | Migrate | Gene flow |
| 2.6.4 | Speciate | New species |
| 2.6.5 | Coevolve | Reciprocal change |
| 2.6.6 | Extinct | Species ending |
| 2.7 | Homeostatic | Internal stability |
| 2.7.1 | Regulate | Maintain range |
| 2.7.2 | Feedback | Response loop |
| 2.7.3 | Repair | Fix damage |
| 2.7.4 | Heal | Organism repair |
| 2.8 | Informational | Signal processing |
| 2.8.1 | Encode | Convert to storage |
| 2.8.2 | Decode | Convert from storage |
| 2.8.3 | Transduce | Convert signal |
| 2.8.4 | Cascade | Signal amplification |
| 2.9 | Emergent | Higher-order patterns |
| 2.9.1 | Emerge | Property arising |
| 2.9.2 | Self_Organize | Spontaneous order |
| 2.9.3 | Complexify | Complexity increase |

---

# Section 3.0: Grammar Extensions — Life's Operations

Extensions to core grammar operations specific to biological systems.

---

## 3.1.1 Sustain (Continuous Process)

Maintains a process while conditions hold and resources last.

```
Sustain := (Sustain, 3.1.1, Maintenance_Loop)
Sustain : Control_Flow
Sustain : Life_Specific
```

**Syntax:**
```
Subject.Sustain.Process
```

**Behavior:**
1. While Subject.Alive and Subject.Energy > 0
2. Execute Process
3. Deduct maintenance cost
4. Repeat

**Example:**
```
Cell.Sustain.Respire
// Cell continuously respires while alive and has glucose

Organism.Sustain.Homeostasis
// Organism maintains internal conditions
```

**Implementation:**
```
Sustain := (Sustain, 3.1.1, {
    Subject.Alive.And.Subject.Energy.Gt.0.While.{
        Subject.Argument.
        Subject.Energy.Sub.Maintenance_Cost.Into.Subject.Energy.
        Time.Advance.Tick
    }
})
```

---

## 3.1.2 Until (Conditional Termination)

Execute process until condition becomes true.

```
Until := (Until, 3.1.2, Conditional_Terminator)
Until : Control_Flow
Until : Life_Specific
```

**Syntax:**
```
Process.Until.Condition
```

**Example:**
```
Cell.Grow.Until.Cell.Size.Gte.Division_Threshold
// Cell grows until large enough to divide

Organism.Develop.Until.Organism.Stage.Eq."Adult"
// Organism develops until reaching adulthood
```

---

## 3.1.3 Strive (Persistent Attempt)

Repeatedly attempt action until success or exhaustion.

```
Strive := (Strive, 3.1.3, Persistent_Attempt)
Strive : Control_Flow
Strive : Life_Specific
```

**Syntax:**
```
Subject.Strive.Goal
```

**Behavior:**
1. Attempt to achieve Goal
2. If failed, adjust strategy
3. Repeat until success or resources exhausted
4. Return success status

**Example:**
```
Predator.Strive.Catch.Prey
// Predator keeps hunting until catches prey or gives up

Plant.Strive.Reach.Light
// Plant grows toward light source
```

**Implementation:**
```
Strive := (Strive, 3.1.3, {
    Success := False.
    Subject.Energy.Gt.0.While.{
        Subject.Attempt.Argument.Try.{
            Success := True.
            Break
        }.
        Subject.Energy.Sub.Attempt_Cost.
        Subject.Strategy.Adjust
    }.
    Success
})
```

---

## 3.1.4 Cycle_Life (Lifecycle Iteration)

Execute through life stages.

```
Cycle_Life := (Cycle_Life, 3.1.4, Lifecycle_Iterator)
Cycle_Life : Control_Flow
Cycle_Life : Life_Specific
```

**Syntax:**
```
Subject.Cycle_Life.Stage_Actions
```

**Example:**
```
Butterfly.Cycle_Life.[
    Egg : Develop,
    Larva : Eat.Grow,
    Pupa : Transform,
    Adult : Reproduce
]
```

---

## 3.1.5 Branch (Biological Branching)

Create divergent lineages or pathways.

```
Branch := (Branch, 3.1.5, Divergence_Creator)
Branch : Control_Flow
Branch : Life_Specific
```

**Syntax:**
```
Subject.Branch.Conditions
```

**Example:**
```
Stem_Cell.Branch.[
    Neuron : Brain_Signal,
    Muscle : Movement_Signal,
    Blood : Marrow_Signal
]
// Stem cell differentiates based on signals
```

---

## 3.2.1 Every (Periodic Execution)

Execute at regular intervals.

```
Every := (Every, 3.2.1, Periodic_Executor)
Every : Timing
Every : Life_Specific
```

**Syntax:**
```
Process.Every.Interval
```

**Example:**
```
Heart.Beat.Every.Second
Cell.Divide.Every.24.Hours
Circadian.Reset.Every.Day
```

---

## 3.2.2 When_Ready (Resource-Gated Execution)

Execute when sufficient resources accumulated.

```
When_Ready := (When_Ready, 3.2.2, Resource_Gate)
When_Ready : Timing
When_Ready : Life_Specific
```

**Syntax:**
```
Process.When_Ready.Resource_Threshold
```

**Example:**
```
Cell.Divide.When_Ready.(Energy.Gte.100, Size.Gte.Threshold)
Organism.Reproduce.When_Ready.(Maturity.Eq.True, Resources.Sufficient)
```

---

## 3.3.1 Express_As (Phenotype Expression)

Output as observable trait.

```
Express_As := (Express_As, 3.3.1, Phenotype_Output)
Express_As : IO
Express_As : Life_Specific
```

**Syntax:**
```
Genotype.Express_As.Phenotype
```

**Example:**
```
Eye_Color_Gene.Express_As.Eye_Color
Height_Genes.Express_As.Height.Modified_By.Environment
```

---

## 3.4.1 Sense_From (Environmental Input)

Capture input from environment.

```
Sense_From := (Sense_From, 3.4.1, Environmental_Input)
Sense_From : IO
Sense_From : Life_Specific
```

**Syntax:**
```
Stimulus.Sense_From.Source
```

**Example:**
```
Light.Sense_From.Environment.Into.Photoreceptor
Chemical.Sense_From.Environment.Into.Chemoreceptor
```

---

## 3.5.1 Become (State Transformation)

Transform into new state or type.

```
Become := (Become, 3.5.1, State_Transformer)
Become : Reference
Become : Life_Specific
```

**Syntax:**
```
Subject.Become.New_State
```

**Example:**
```
Caterpillar.Become.Butterfly
Stem_Cell.Become.Neuron
Living.Become.Dead
```

**Implementation:**
```
Become := (Become, 3.5.1, {
    Subject.Previous_State := Subject.State.
    Subject.State := Argument.
    Subject.Transform.Execute.
    Subject.Type := Argument.Type.Try
})
```

---

## 3.6.1 Spawn (Offspring Creation)

Create new organism instance.

```
Spawn := (Spawn, 3.6.1, Offspring_Generator)
Spawn : Callable
Spawn : Life_Specific
```

**Syntax:**
```
Parent.Spawn.Offspring_Type
Parents.Spawn.Offspring_Type
```

**Example:**
```
Bacterium.Spawn.Clone
// Asexual reproduction

[Mother, Father].Spawn.Child
// Sexual reproduction
```

**Implementation:**
```
Spawn := (Spawn, 3.6.1, {
    Argument.Type.When.[
        "Asexual" : {
            Subject.Clone.As.Offspring.
            Offspring.Mutate.Try.Low_Rate
        },
        "Sexual" : {
            Subject.0.Gamete.Fuse.Subject.1.Gamete.As.Zygote.
            Zygote.Develop.As.Offspring
        }
    ].
    Offspring.Birth.
    Offspring
})
```

---

## 3.7.1 Tolerate (Conditional Survival)

Continue despite suboptimal conditions.

```
Tolerate := (Tolerate, 3.7.1, Stress_Handler)
Tolerate : Error_Handling
Tolerate : Life_Specific
```

**Syntax:**
```
Subject.Tolerate.Stressor
Subject.Tolerate.Stressor.Within.Range
```

**Example:**
```
Extremophile.Tolerate.High_Temperature.Within.[80, 120]
// Survives between 80-120°C

Desert_Plant.Tolerate.Drought.For.Months
```

---

## 3.7.2 Stress (Damage Accumulation)

Track cumulative damage.

```
Stress := (Stress, 3.7.2, Damage_Tracker)
Stress : Error_Handling
Stress : Life_Specific
```

**Syntax:**
```
Subject.Stress.Add.Stressor
Subject.Stress.Level
```

**Example:**
```
Cell.Stress.Add.Oxidative_Damage
Cell.Stress.Level.Gt.Threshold.Then.Cell.Apoptose
```

---

## 3.8.1 Within (Compartmentalization)

Execute within specific biological compartment.

```
Within := (Within, 3.8.1, Compartment_Context)
Within : Scope
Within : Life_Specific
```

**Syntax:**
```
Compartment.Within.{Operations}
```

**Example:**
```
Nucleus.Within.{
    DNA.Replicate.
    Gene.Transcribe
}

Mitochondrion.Within.{
    Respiration.Execute.
    ATP.Produce
}
```

---

## 3.99 Section 3.0 Summary

| Address | Label | Description |
|---------|-------|-------------|
| 3.1.1 | Sustain | Continuous process |
| 3.1.2 | Until | Conditional termination |
| 3.1.3 | Strive | Persistent attempt |
| 3.1.4 | Cycle_Life | Lifecycle iteration |
| 3.1.5 | Branch | Biological branching |
| 3.2.1 | Every | Periodic execution |
| 3.2.2 | When_Ready | Resource-gated execution |
| 3.3.1 | Express_As | Phenotype output |
| 3.4.1 | Sense_From | Environmental input |
| 3.5.1 | Become | State transformation |
| 3.6.1 | Spawn | Offspring creation |
| 3.7.1 | Tolerate | Stress handling |
| 3.7.2 | Stress | Damage tracking |
| 3.8.1 | Within | Compartmentalization |

---

# Section 4.0: Workspace Patterns

Templates for instantiating life in the runtime Workspace.

---

## 4.1 Cell Instantiation

```
// Create a generic eukaryotic cell
MyCell := Cell.New
MyCell : Type = "Eukaryote"
MyCell : Alive = True
MyCell : Energy = 100
MyCell : Division_Count = 0

// Add organelles
MyCell.Nucleus := Nucleus.New
MyCell.Nucleus.DNA := Genome.New.(Size = 3000000000)

MyCell.Mitochondria := []
10.Times.{
    MyCell.Mitochondria.Add.Mitochondrion.New
}

MyCell.Membrane := Membrane.New
MyCell.Membrane : Permeability = 0.5

// Cell lifecycle
MyCell.Sustain.{
    Self.Respire.
    Self.Energy.Lt.50.Then.Self.Eat.
    Self.Energy.Gt.150.And.Self.Size.Gte.Threshold.Then.Self.Divide
}
```

---

## 4.2 Organism Instantiation

```
// Create an organism
Creature := Organism.New
Creature : Species = "Example_Species"
Creature : Generation = 1
Creature : Age = 0
Creature : Alive = True
Creature : Fitness = 0

// Genome with genes
Creature.Genome := Genome.New
Creature.Genome.Genes := [
    Gene.New.(Name = "Growth_Factor", Sequence = "ATCG..."),
    Gene.New.(Name = "Metabolism_Enzyme", Sequence = "GCTA..."),
    Gene.New.(Name = "Pigment", Sequence = "TAGC...")
]

// Express phenotype
Creature.Phenotype := []
Creature.Genome.Genes.Cycle.{
    Item.Express.Then.{
        Creature.Phenotype.Add.Item.Product
    }
}

// Systems
Creature.Systems := [
    Digestive_System.New,
    Circulatory_System.New,
    Nervous_System.New
]

// Life loop
Creature.Sustain.{
    Self.Sense.Environment.
    Self.Respond.Stimuli.
    Self.Metabolize.
    Self.Age.Add.1.
    Self.Mature.Then.Self.Reproduce.Try
}
```

---

## 4.3 Population Instantiation

```
// Create a population
Colony := Population.New
Colony : Species = "Bacterium"
Colony : Location = Petri_Dish
Colony : Carrying_Capacity = 1000000

// Initial members
100.Times.{
    Member := Organism.New.(Species = "Bacterium")
    Member.Genome := Reference_Genome.Copy.Mutate.Try.0.001
    Colony.Members.Add.Member
}

// Population dynamics
Colony.Sustain.{
    // Reproduction
    Self.Members.Cycle.{
        Item.Energy.Sufficient.Then.{
            Item.Reproduce.
            Self.Members.Add.Offspring
        }
    }.
    
    // Selection
    Self.Members.Cycle.{
        Item.Fitness.Lt.Survival_Threshold.Then.{
            Item.Die.
            Self.Members.Remove.Item
        }
    }.
    
    // Check capacity
    Self.Size.Gt.Self.Carrying_Capacity.Then.{
        Self.Resource_Limited = True
    }
}
```

---

## 4.4 Ecosystem Instantiation

```
// Create an ecosystem
Pond := Ecosystem.New
Pond : Location = "Freshwater_Body"
Pond : Area = 100  // square meters

// Abiotic factors
Pond.Abiotic := [
    Condition.New.(Name = "Temperature", Value = 20, Unit = "Celsius"),
    Condition.New.(Name = "pH", Value = 7.0),
    Condition.New.(Name = "Oxygen", Value = 8, Unit = "mg/L"),
    Condition.New.(Name = "Light", Value = 1000, Unit = "lux")
]

// Resources
Pond.Resources := [
    Resource.New.(Type = "Nutrients", Availability = 100),
    Resource.New.(Type = "Space", Availability = Pond.Area)
]

// Community
Pond.Community := Community.New
Pond.Community.Populations := [
    Population.New.(Species = "Algae", Size = 10000),
    Population.New.(Species = "Zooplankton", Size = 1000),
    Population.New.(Species = "Small_Fish", Size = 100),
    Population.New.(Species = "Large_Fish", Size = 10)
]

// Food web
Pond.Food_Web := [
    (Algae, Zooplankton, "Consumed_By"),
    (Zooplankton, Small_Fish, "Consumed_By"),
    (Small_Fish, Large_Fish, "Consumed_By")
]

// Ecosystem dynamics
Pond.Sustain.{
    // Energy flow
    Pond.Community.Populations.0.Photosynthesize.  // Algae
    
    // Trophic interactions
    Pond.Food_Web.Cycle.{
        Item.0.Predate.Try.Item.1
    }.
    
    // Nutrient cycling
    Pond.Dead_Matter.Decompose.Into.Pond.Nutrients
}
```

---

## 4.5 Evolutionary Simulation

```
// Evolutionary run
Simulation := Workspace.Branch.Create
Simulation : Generations = 1000
Simulation : Mutation_Rate = 0.01
Simulation : Selection_Strength = 0.1

// Initialize population
Simulation.Population := Population.New.(Size = 1000)

// Run evolution
Simulation.Generations.Times.{
    // Reproduce with variation
    Simulation.Population.Members.Cycle.{
        Item.Fitness.Gt.Threshold.Then.{
            Offspring := Item.Spawn.
            Offspring.Genome.Mutate.Try.Simulation.Mutation_Rate
        }
    }.
    
    // Selection
    Simulation.Population.Select.(Environment).
    
    // Drift (if small population)
    Simulation.Population.Size.Lt.100.Then.{
        Simulation.Population.Drift
    }.
    
    // Record state
    Simulation.History.Add.(
        Generation = Index,
        Gene_Pool = Simulation.Population.Gene_Pool.Copy,
        Mean_Fitness = Simulation.Population.Mean_Fitness
    )
}.

// Analyze results
Simulation.History.Cycle.{
    Item.Mean_Fitness.Emit
}
```

---

## 4.6 Cellular Automaton (Life Emergence)

```
// Simple cellular automaton for emergence
Grid := []
100.Times.{
    Row := []
    100.Times.{
        Cell := Cell.New.(Alive = Stochastic.Chance.0.3)
        Row.Add.Cell
    }
    Grid.Add.Row
}

// Conway's Game of Life rules as life emergence
Grid.Sustain.{
    Grid.Cycle.{
        Row := Item.
        Row.Cycle.{
            Cell := Item.
            Neighbors := Cell.Count_Alive_Neighbors.
            
            Cell.Alive.Then.{
                Neighbors.Lt.2.Then.Cell.Die.          // Underpopulation
                Neighbors.Gt.3.Then.Cell.Die.          // Overpopulation
            }.Else.{
                Neighbors.Eq.3.Then.Cell.Alive = True   // Reproduction
            }
        }
    }
}
```

---

## 4.99 Section 4.0 Summary

| Pattern | Description |
|---------|-------------|
| Cell Instantiation | Creating and running a single cell |
| Organism Instantiation | Multi-system living individual |
| Population Instantiation | Group of same-species organisms |
| Ecosystem Instantiation | Community with environment |
| Evolutionary Simulation | Multi-generation selection |
| Cellular Automaton | Emergent life patterns |

---

# Appendix A: Complete Address Index

## Section 0.x - Kernel Extensions
| Address | Label |
|---------|-------|
| 0.0.1 | Life_Kernel |
| 0.1.1 | Chemistry |
| 0.1.2 | Thermodynamics |
| 0.1.3 | Information |
| 0.1.4 | Environment |
| 0.1.5 | Stochastic |

## Section 1.x - Structure
| Address | Label |
|---------|-------|
| 1.1 | Life |
| 1.2 | Matter |
| 1.2.1 | Atom |
| 1.2.2 | Molecule |
| 1.2.3 | Macromolecule |
| 1.2.3.1 | Protein |
| 1.2.3.2 | Nucleic_Acid |
| 1.2.3.2.1 | DNA |
| 1.2.3.2.2 | RNA |
| 1.2.3.3 | Carbohydrate |
| 1.2.3.4 | Lipid |
| 1.3 | Structure |
| 1.3.1 | Organelle |
| 1.3.1.1 | Nucleus |
| 1.3.1.2 | Mitochondrion |
| 1.3.1.3 | Ribosome |
| 1.3.1.4 | Membrane |
| 1.3.1.5 | Chloroplast |
| 1.3.1.6 | ER |
| 1.3.1.7 | Golgi |
| 1.3.1.8 | Lysosome |
| 1.3.2 | Cell |
| 1.3.2.1 | Prokaryote |
| 1.3.2.2 | Eukaryote |
| 1.3.3 | Tissue |
| 1.3.3.1 | Epithelial |
| 1.3.3.2 | Connective |
| 1.3.3.3 | Muscle |
| 1.3.3.4 | Nervous |
| 1.3.4 | Organ |
| 1.3.5 | System |
| 1.3.5.1 | Digestive_System |
| 1.3.5.2 | Circulatory_System |
| 1.3.5.3 | Nervous_System |
| 1.3.5.4 | Immune_System |
| 1.3.5.5 | Reproductive_System |
| 1.3.6 | Organism |
| 1.3.7 | Population |
| 1.3.8 | Community |
| 1.3.9 | Ecosystem |
| 1.3.10 | Biosphere |
| 1.4 | Process |
| 1.4.1 | Metabolism |
| 1.4.1.1 | Anabolism |
| 1.4.1.2 | Catabolism |
| 1.4.1.3 | Respiration |
| 1.4.1.4 | Photosynthesis |
| 1.4.1.5 | Glycolysis |
| 1.4.2 | Growth |
| 1.4.2.1 | Cell_Growth |
| 1.4.2.2 | Cell_Division |
| 1.4.3 | Development |
| 1.4.3.1 | Differentiation |
| 1.4.3.2 | Morphogenesis |
| 1.4.4 | Reproduction |
| 1.4.4.1 | Asexual |
| 1.4.4.2 | Sexual |
| 1.4.5 | Death |
| 1.4.5.1 | Apoptosis |
| 1.4.5.2 | Necrosis |
| 1.5 | Information |
| 1.5.1 | Gene |
| 1.5.2 | Genome |
| 1.5.3 | Signal |
| 1.5.3.1 | Hormone |
| 1.5.3.2 | Neurotransmitter |
| 1.5.3.3 | Cytokine |
| 1.5.4 | Receptor |
| 1.6 | Energy |
| 1.6.1 | ATP |
| 1.6.2 | Gradient |
| 1.6.2.1 | Proton_Gradient |
| 1.6.2.2 | Ion_Gradient |
| 1.7 | Environment |
| 1.7.1 | Resource |
| 1.7.1.1 | Nutrient |
| 1.7.1.2 | Energy_Source |
| 1.7.1.3 | Space |
| 1.7.2 | Condition |
| 1.7.2.1 | Temperature |
| 1.7.2.2 | pH |
| 1.7.2.3 | Salinity |
| 1.7.2.4 | Oxygen_Level |
| 1.7.2.5 | Light_Intensity |
| 1.7.2.6 | Pressure |
| 1.7.3 | Niche |
| 1.7.4 | Habitat |
| 1.8 | Time |
| 1.8.1 | Lifespan |
| 1.8.2 | Generation |
| 1.8.3 | Cycle |
| 1.8.3.1 | Cell_Cycle |
| 1.8.3.2 | Circadian |
| 1.8.3.3 | Seasonal |
| 1.8.3.4 | Menstrual |
| 1.8.4 | Event |
| 1.8.4.1 | Birth |
| 1.8.4.2 | Death |
| 1.8.4.3 | Mutation |
| 1.8.4.4 | Speciation |
| 1.8.4.5 | Extinction |
| 1.9 | Interaction |
| 1.9.1 | Symbiosis |
| 1.9.1.1 | Mutualism |
| 1.9.1.2 | Commensalism |
| 1.9.1.3 | Parasitism |
| 1.9.2 | Predation |
| 1.9.3 | Competition |
| 1.9.3.1 | Intraspecific |
| 1.9.3.2 | Interspecific |
| 1.9.4 | Cooperation |

## Section 2.x - Relations
| Address | Label |
|---------|-------|
| 2.1.1 | Consume |
| 2.1.2 | Metabolize |
| 2.1.3 | Synthesize |
| 2.1.4 | Respire |
| 2.1.5 | Photosynthesize |
| 2.1.6 | Ferment |
| 2.2.1 | Replicate |
| 2.2.2 | Transcribe |
| 2.2.3 | Translate |
| 2.2.4 | Express |
| 2.2.5 | Regulate |
| 2.2.6 | Mutate |
| 2.2.7 | Inherit |
| 2.3.1 | Divide |
| 2.3.2 | Differentiate |
| 2.3.3 | Signal |
| 2.3.4 | Receive |
| 2.3.5 | Transport |
| 2.3.6 | Apoptose |
| 2.4.1 | Grow |
| 2.4.2 | Develop |
| 2.4.3 | Reproduce |
| 2.4.4 | Die |
| 2.4.5 | Sense |
| 2.4.6 | Respond |
| 2.4.7 | Move |
| 2.4.8 | Adapt |
| 2.5.1 | Predate |
| 2.5.2 | Compete |
| 2.5.3 | Cooperate |
| 2.5.4 | Parasitize |
| 2.5.5 | Inhabit |
| 2.5.6 | Disperse |
| 2.6.1 | Select |
| 2.6.2 | Drift |
| 2.6.3 | Migrate |
| 2.6.4 | Speciate |
| 2.6.5 | Coevolve |
| 2.6.6 | Extinct |
| 2.7.1 | Regulate |
| 2.7.2 | Feedback |
| 2.7.3 | Repair |
| 2.7.4 | Heal |
| 2.8.1 | Encode |
| 2.8.2 | Decode |
| 2.8.3 | Transduce |
| 2.8.4 | Cascade |
| 2.9.1 | Emerge |
| 2.9.2 | Self_Organize |
| 2.9.3 | Complexify |

## Section 3.x - Grammar Extensions
| Address | Label |
|---------|-------|
| 3.1.1 | Sustain |
| 3.1.2 | Until |
| 3.1.3 | Strive |
| 3.1.4 | Cycle_Life |
| 3.1.5 | Branch |
| 3.2.1 | Every |
| 3.2.2 | When_Ready |
| 3.3.1 | Express_As |
| 3.4.1 | Sense_From |
| 3.5.1 | Become |
| 3.6.1 | Spawn |
| 3.7.1 | Tolerate |
| 3.7.2 | Stress |
| 3.8.1 | Within |

---

# Appendix B: Quick Reference

## Life Hierarchy

```
Atom → Molecule → Macromolecule → Organelle → Cell → 
Tissue → Organ → System → Organism → Population → 
Community → Ecosystem → Biosphere
```

## Core Life Properties

| Property | Description |
|----------|-------------|
| Alive | Boolean state of living |
| Energy | Current energy reserves |
| Age | Time since creation |
| Fitness | Reproductive success potential |
| Genome | Genetic information |
| Phenotype | Observable characteristics |

## Essential Relations

| Relation | Pattern | Effect |
|----------|---------|--------|
| Consume | Life.Consume.Resource | Acquire energy/matter |
| Respire | Cell.Respire | Generate ATP |
| Divide | Cell.Divide | Produce daughter cells |
| Express | Gene.Express | Produce protein |
| Reproduce | Organism.Reproduce | Generate offspring |
| Die | Organism.Die | Cease living |
| Select | Population.Select | Differential survival |
| Evolve | Species.Evolve | Change over generations |

## Life Grammar

| Operation | Syntax | Purpose |
|-----------|--------|---------|
| Sustain | X.Sustain.Process | Continuous execution |
| Until | Process.Until.Condition | Conditional termination |
| Strive | X.Strive.Goal | Persistent attempt |
| Become | X.Become.Y | State transformation |
| Spawn | Parent.Spawn.Type | Create offspring |
| Every | Process.Every.Interval | Periodic execution |

## Stall Semantics in Life

In the Life Dictionary, stalls have special biological meaning:

| Stall Situation | Biological Interpretation |
|-----------------|---------------------------|
| Resource insufficient | Waiting for resources |
| Condition not met | Dormancy/quiescence |
| Signal not received | Awaiting trigger |
| Incompatible types | Reproductive isolation |
| Unknown relation | Evolutionary potential |

---

# Appendix C: Example — Complete Bacterial Life Cycle

```
// Define a bacterium
Import.Chemistry
Import.Stochastic

// Structure
Bacterium := Prokaryote.New
Bacterium : Species = "E_coli"
Bacterium : Genome_Size = 4600000
Bacterium : Generation_Time = 20  // minutes
Bacterium : Alive = True
Bacterium : Age = 0
Bacterium : Energy = 50
Bacterium : Size = 1

// Genome
Bacterium.Genome := Genome.New
Bacterium.Genome.Genes := [
    Gene.New.(Name = "lac_operon", Function = "Lactose_Metabolism"),
    Gene.New.(Name = "flagellar", Function = "Motility"),
    Gene.New.(Name = "heat_shock", Function = "Stress_Response")
]

// Membrane
Bacterium.Membrane := Membrane.New
Bacterium.Membrane : Composition = [Lipid, Protein]
Bacterium.Membrane : Receptors = [
    Receptor.New.(Ligand = "Glucose"),
    Receptor.New.(Ligand = "Lactose"),
    Receptor.New.(Ligand = "Chemotactic_Signal")
]

// Metabolic capability
Bacterium.Metabolize := {
    Self.Environment.Glucose.Available.Then.{
        Self.Consume.Glucose.
        Self.Respire.
        Self.Energy.Add.36
    }.Else.{
        Self.Environment.Lactose.Available.Then.{
            Self.Genome.Genes.lac_operon.Express.
            Self.Consume.Lactose.
            Self.Ferment.
            Self.Energy.Add.2
        }
    }
}

// Division logic
Bacterium.Ready_To_Divide := {
    Self.Energy.Gte.100.And.Self.Size.Gte.2
}

Bacterium.Division := {
    Self.DNA.Replicate.
    Self.Split.As.[Daughter_A, Daughter_B].
    Daughter_A.Energy = Self.Energy.Div.2.
    Daughter_B.Energy = Self.Energy.Div.2.
    Stochastic.Chance.0.001.Then.{
        Daughter_A.Genome.Mutate."Point"
    }.
    Stochastic.Chance.0.001.Then.{
        Daughter_B.Genome.Mutate."Point"
    }.
    [Daughter_A, Daughter_B]
}

// Stress response
Bacterium.Stress_Response := {
    Self.Environment.Temperature.Gt.42.Then.{
        Self.Genome.Genes.heat_shock.Express.
        Self.Stress.Add.Heat_Stress
    }.
    Self.Stress.Level.Gt.Lethal_Threshold.Then.{
        Self.Die
    }
}

// Chemotaxis
Bacterium.Chemotaxis := {
    Self.Sense.Chemical_Gradient.
    Gradient.Favorable.Then.{
        Self.Move.Toward.Gradient.Source
    }.Else.{
        Self.Tumble.Random_Direction
    }
}

// Main life loop
Bacterium.Live := {
    Self.Sustain.{
        // Metabolism
        Self.Metabolize.
        
        // Growth
        Self.Energy.Gt.50.Then.{
            Self.Size.Add.0.1
        }.
        
        // Division check
        Self.Ready_To_Divide.Then.{
            Self.Division
        }.
        
        // Behavior
        Self.Chemotaxis.
        
        // Stress check
        Self.Stress_Response.
        
        // Age
        Self.Age.Add.1
    }
}

// Run the bacterium
Bacterium.Live
```

---

**End of Uypocode Life Dictionary v1.0**
