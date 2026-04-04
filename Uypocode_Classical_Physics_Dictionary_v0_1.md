# Uypocode Classical Physics Dictionary
## Specification v0.1

---

# Preface: Physics as Semantic Structure

This dictionary models classical physics through Uypocode's semantic framework—where physical reality is represented as Objects with Labels, Addresses, and Contents; where natural laws become Relations that transform state; and where unresolved physical questions naturally *stall* rather than error, persisting as the open inquiries that drive scientific investigation.

Classical physics, in this framework, is:
- **Action-principled**: all dynamics emerge from minimizing a single scalar quantity
- **Scale-invariant**: the same formalisms span bacteria to planets
- **Symmetry-governed**: conservation laws flow from invariances via Noether's theorem
- **Field-mediated**: interactions propagate through space via potential functions
- **Stall-aware**: boundary conditions, singularities, and turbulence produce Stalls

> "Nature acts along the shortest path. The universe computes its own trajectory by finding where variation vanishes."

---

# Section 0.0: Kernel Extensions

The Classical Physics Dictionary extends the base Kernel with physics-specific imports.

```
Physics_Kernel := (Physics_Kernel, 0.0.10, Foundation_Extension)
Physics_Kernel : Extends = Kernel
Physics_Kernel : Domain = Classical_Physics
```

---

## 0.10.1 Import.Calculus

Differential and integral operations fundamental to physics.

```
Calculus := (Calculus, 0.10.1, Analysis_Engine)
Calculus : Import
Calculus : Required
```

**Provides:**
- Differentiation (ordinary and partial)
- Integration (definite, indefinite, path, surface, volume)
- Differential equations
- Variational calculus
- Limit operations

**Usage:**
```
Import.Calculus
Position.Differentiate.Time → Velocity
Force.Integrate.Path → Work
Lagrangian.Vary.Path → Euler_Lagrange_Equation
```

---

## 0.10.2 Import.Vector

Vector and tensor operations for spatial quantities.

```
Vector := (Vector, 0.10.2, Geometric_Engine)
Vector : Import
Vector : Required
```

**Provides:**
- Vector addition, subtraction, scaling
- Dot product, cross product
- Gradient, divergence, curl, Laplacian
- Coordinate transformations
- Tensor algebra

**Usage:**
```
Import.Vector
Force_A.Add.Force_B → Net_Force
Velocity.Cross.Magnetic_Field → Lorentz_Force
Potential.Gradient → Force_Field
```

---

## 0.10.3 Import.Geometry

Spatial and geometric operations.

```
Geometry := (Geometry, 0.10.3, Spatial_Engine)
Geometry : Import
Geometry : Required
```

**Provides:**
- Distance and angle calculations
- Coordinate systems (Cartesian, polar, spherical, cylindrical)
- Path parameterization
- Surface and volume elements
- Metric tensors

**Usage:**
```
Import.Geometry
Point_A.Distance.Point_B → Separation
Path.Parameterize.Arc_Length → Curve
Sphere.Volume_Element → r²sin(θ)drdθdφ
```

---

## 0.10.4 Import.Statistics

Statistical mechanics foundations.

```
Statistics := (Statistics, 0.10.4, Statistical_Engine)
Statistics : Import
Statistics : Optional
```

**Provides:**
- Probability distributions
- Ensemble averages
- Partition functions
- Entropy calculations
- Fluctuation analysis

**Usage:**
```
Import.Statistics
Microstates.Count → Ω
Ω.Ln.Mul.k_B → Entropy
Energy.Boltzmann_Weight.Temperature → Probability
```

---

## 0.10.5 Import.Units

Physical units and dimensional analysis.

```
Units := (Units, 0.10.5, Dimensional_Engine)
Units : Import
Units : Required
```

**Provides:**
- SI base units and derived units
- Unit conversion
- Dimensional analysis
- Dimensionless numbers
- Natural unit systems

**Usage:**
```
Import.Units
10.Meters.Per.Second → Velocity_Value
Force.Dimensions → [M][L][T]⁻²
Reynolds.Number.Calculate.(ρ, v, L, μ) → Re
```

---

## 0.10.6 Kernel Summary

| Address | Label | Description |
|---------|-------|-------------|
| 0.0.10 | Physics_Kernel | Classical physics foundation |
| 0.10.1 | Calculus | Analysis operations |
| 0.10.2 | Vector | Geometric algebra |
| 0.10.3 | Geometry | Spatial operations |
| 0.10.4 | Statistics | Statistical mechanics |
| 0.10.5 | Units | Dimensional analysis |

---

# Section 10.0: Objects — The Structures of Classical Physics

Physics Objects represent the fundamental entities, quantities, and abstractions of the classical world. They range from point particles to continuous fields, from instants to eons.

---

## 10.1 Action (The Foundational Principle)

The root Object from which all classical dynamics descend. Action is the integral of the Lagrangian over time—the scalar quantity whose stationary value determines physical trajectories.

```
Action := (Action, 10.1, Stationary_Integral)
Action : Foundational
Action : Scalar
Action : Coordinate_Independent
```

**Core Definition:**
```
Action : Symbol = "S"
Action : Definition = "∫L dt"
Action : Principle = "δS = 0"    // Stationary action
Action : Units = [Energy][Time]   // Joule·seconds
```

**Why Action is fundamental:**
1. **Scalar**: No vector complications, coordinate-free
2. **Universal**: Same formalism for particles, fields, fluids
3. **Symmetric**: Symmetries → conservation laws (Noether)
4. **Generative**: Equations of motion derived, not assumed

```
Action.Calculate := {
    Lagrangian.Integrate.Over.Time.(t1, t2)
}

Action.Minimize := {
    // The path q(t) that makes δS = 0
    Self.Vary.Path.
    Variation.Set.Zero.
    Euler_Lagrange.Apply
}
```

### 10.1.1 Lagrangian

The instantaneous difference between kinetic and potential energy.

```
Lagrangian := (Lagrangian, 10.1.1, Energy_Difference)
Lagrangian : Symbol = "L"
Lagrangian : Definition = "T - V"
Lagrangian : Arguments = [q, q_dot, t]   // Positions, velocities, time
```

**Properties:**
```
Lagrangian : T = Kinetic_Energy
Lagrangian : V = Potential_Energy
Lagrangian : Scalar = True
Lagrangian : Not_Unique = True   // Can add total time derivative
```

**General Forms:**
```
// Discrete particles
Lagrangian.Discrete := {
    T := (1/2).Mul.Masses.Cycle.{
        Item.Mass.Mul.Item.Velocity.Squared.Sum
    }.
    V := Potential.Evaluate.(Positions).
    T.Sub.V
}

// Continuous media (Lagrangian density)
Lagrangian.Density := {
    Symbol = "ℒ"
    Definition = "T_density - V_density"
    Action = "∫∫∫∫ ℒ d³x dt"
}
```

### 10.1.2 Euler_Lagrange

The equation of motion derived from stationary action.

```
Euler_Lagrange := (Euler_Lagrange, 10.1.2, Equation_Of_Motion)
Euler_Lagrange : Definition = "d/dt(∂L/∂q̇) - ∂L/∂q = 0"
Euler_Lagrange : Derivation = "Calculus_of_Variations"
```

**Application:**
```
Euler_Lagrange.Apply := {
    // For each generalized coordinate q
    Coordinates.Cycle.{
        Momentum := Lagrangian.Partial.Item.Velocity   // ∂L/∂q̇
        Force := Lagrangian.Partial.Item.Position      // ∂L/∂q
        Momentum.Time_Derivative.Eq.Force              // d/dt(∂L/∂q̇) = ∂L/∂q
    }
}
```

### 10.1.3 Hamiltonian

The Legendre transform of the Lagrangian—total energy in many cases.

```
Hamiltonian := (Hamiltonian, 10.1.3, Total_Energy)
Hamiltonian : Symbol = "H"
Hamiltonian : Definition = "Σ pᵢq̇ᵢ - L"
Hamiltonian : Arguments = [q, p, t]   // Positions and momenta
```

**Properties:**
```
Hamiltonian : Conserved.When = "∂L/∂t = 0"  // Time-translation symmetry
Hamiltonian : Phase_Space = True
```

**Hamilton's Equations:**
```
Hamilton.Equations := {
    q_dot := Hamiltonian.Partial.p          // ∂H/∂p = q̇
    p_dot := Hamiltonian.Partial.q.Neg      // ∂H/∂q = -ṗ
}
```

---

## 10.2 Matter (The Inertial Component)

Physical substance possessing mass—the source of inertia and gravitation.

```
Matter := (Matter, 10.2, Mass_Bearing_Substance)
Matter : Tangible
Matter : Conserved
Matter : Inertial
```

### 10.2.1 Particle

The idealized point mass—a discrete chunk of matter with no internal structure.

```
Particle := (Particle, 10.2.1, Point_Mass)
Particle : Discrete
Particle : Localized
```

**Properties:**
```
Particle : Mass = Number              // m [kg]
Particle : Position = Vector          // r⃗ [m]
Particle : Velocity = Vector          // v⃗ = dr⃗/dt [m/s]
Particle : Momentum = Vector          // p⃗ = mv⃗ [kg·m/s]
Particle : Charge = Number            // q [C] (optional)
```

**Kinetic Energy:**
```
Particle.Kinetic_Energy := {
    (1/2).Mul.Self.Mass.Mul.Self.Velocity.Squared
}
// T = ½mv²
```

### 10.2.2 Rigid_Body

Extended mass distribution that maintains fixed internal distances.

```
Rigid_Body := (Rigid_Body, 10.2.2, Constrained_Continuum)
Rigid_Body : Extended
Rigid_Body : Constraints = "Fixed_Distances"
```

**Properties:**
```
Rigid_Body : Mass = Number
Rigid_Body : Center_Of_Mass = Vector
Rigid_Body : Inertia_Tensor = Matrix       // 3×3 symmetric
Rigid_Body : Orientation = Rotation         // SO(3) element
Rigid_Body : Angular_Velocity = Vector      // ω⃗
Rigid_Body : Angular_Momentum = Vector      // L⃗ = Iω⃗
```

**Kinetic Energy (general):**
```
Rigid_Body.Kinetic_Energy := {
    T_translational := (1/2).Mul.Self.Mass.Mul.Self.CM_Velocity.Squared.
    T_rotational := (1/2).Mul.Self.Angular_Velocity.Dot.(
        Self.Inertia_Tensor.Apply.Self.Angular_Velocity
    ).
    T_translational.Add.T_rotational
}
// T = ½Mv²_cm + ½ω⃗·I·ω⃗
```

### 10.2.3 Continuum

Matter distributed continuously through space.

```
Continuum := (Continuum, 10.2.3, Distributed_Matter)
Continuum : Continuous
Continuum : Field_Description = True
```

**Properties:**
```
Continuum : Density = Field             // ρ(r⃗,t) [kg/m³]
Continuum : Velocity_Field = Field      // v⃗(r⃗,t) [m/s]
```

**Kinetic Energy (continuous):**
```
Continuum.Kinetic_Energy := {
    (1/2).Mul.Density.Mul.Velocity.Squared.Integrate.Volume
}
// T = ∫ ½ρv² dV
```

---

## 10.3 Space (The Arena)

The geometric stage on which physics unfolds.

```
Space := (Space, 10.3, Geometric_Substrate)
Space : Continuous
Space : Euclidean           // In classical physics
Space : Three_Dimensional
```

### 10.3.1 Position

Location in space.

```
Position := (Position, 10.3.1, Spatial_Point)
Position : Symbol = "r⃗"
Position : Type = Vector
Position : Components = [x, y, z]
```

### 10.3.2 Displacement

Change in position.

```
Displacement := (Displacement, 10.3.2, Position_Change)
Displacement : Symbol = "Δr⃗"
Displacement : Definition = "r⃗_final - r⃗_initial"
```

### 10.3.3 Path

A trajectory through space.

```
Path := (Path, 10.3.3, Spatial_Curve)
Path : Parameterized = True
Path : Parameter = [Time | Arc_Length | Arbitrary]
```

**Path Properties:**
```
Path : Start = Position
Path : End = Position
Path : Length := Arc_Length.Integrate.Path
```

---

## 10.4 Time (The Parameter)

The independent variable parameterizing change.

```
Time := (Time, 10.4, Temporal_Parameter)
Time : Symbol = "t"
Time : Universal            // Absolute in classical physics
Time : One_Dimensional
Time : Ordered
```

### 10.4.1 Instant

A single moment.

```
Instant := (Instant, 10.4.1, Time_Point)
Instant : Value = Number
Instant : Units = Seconds
```

### 10.4.2 Duration

Time interval.

```
Duration := (Duration, 10.4.2, Time_Interval)
Duration : Definition = "t_final - t_initial"
Duration : Always_Positive = True
```

### 10.4.3 Rate

Change per unit time.

```
Rate := (Rate, 10.4.3, Temporal_Derivative)
Rate : Definition = "dX/dt"
Rate : Applied_To = Any_Quantity
```

---

## 10.5 Kinematics (Motion Description)

The geometry of motion without reference to causes.

```
Kinematics := (Kinematics, 10.5, Motion_Geometry)
Kinematics : Descriptive
Kinematics : No_Forces
```

### 10.5.1 Velocity

Rate of position change.

```
Velocity := (Velocity, 10.5.1, Position_Rate)
Velocity : Symbol = "v⃗"
Velocity : Definition = "dr⃗/dt"
Velocity : Type = Vector
Velocity : Units = [m/s]
```

### 10.5.2 Acceleration

Rate of velocity change.

```
Acceleration := (Acceleration, 10.5.2, Velocity_Rate)
Acceleration : Symbol = "a⃗"
Acceleration : Definition = "dv⃗/dt = d²r⃗/dt²"
Acceleration : Type = Vector
Acceleration : Units = [m/s²]
```

### 10.5.3 Angular_Velocity

Rate of angular position change.

```
Angular_Velocity := (Angular_Velocity, 10.5.3, Rotation_Rate)
Angular_Velocity : Symbol = "ω⃗"
Angular_Velocity : Definition = "dθ/dt"
Angular_Velocity : Type = Pseudovector
Angular_Velocity : Units = [rad/s]
```

---

## 10.6 Dynamics (Motion Causation)

The relationship between forces and motion.

```
Dynamics := (Dynamics, 10.6, Force_Motion_Relation)
Dynamics : Causal
Dynamics : From_Action_Principle
```

### 10.6.1 Force

The agent of acceleration—rate of momentum change.

```
Force := (Force, 10.6.1, Momentum_Rate)
Force : Symbol = "F⃗"
Force : Definition = "dp⃗/dt"
Force : Type = Vector
Force : Units = [N] = [kg·m/s²]
```

**Newton's Second Law (special case of Euler-Lagrange):**
```
Force.Newton := {
    Self = Mass.Mul.Acceleration
}
// F⃗ = ma⃗ (when m is constant)
```

### 10.6.2 Momentum

The quantity of motion.

```
Momentum := (Momentum, 10.6.2, Motion_Quantity)
Momentum : Symbol = "p⃗"
Momentum : Definition = "mv⃗"      // For particles
Momentum : Type = Vector
Momentum : Conserved.When = "Translational_Symmetry"
```

**Generalized Momentum:**
```
Generalized_Momentum := {
    Symbol = "pᵢ"
    Definition = "∂L/∂q̇ᵢ"
    Conjugate_To = "qᵢ"
}
```

### 10.6.3 Angular_Momentum

Rotational momentum.

```
Angular_Momentum := (Angular_Momentum, 10.6.3, Rotational_Motion)
Angular_Momentum : Symbol = "L⃗"
Angular_Momentum : Definition = "r⃗ × p⃗"
Angular_Momentum : Type = Pseudovector
Angular_Momentum : Conserved.When = "Rotational_Symmetry"
```

### 10.6.4 Torque

Rotational force—rate of angular momentum change.

```
Torque := (Torque, 10.6.4, Angular_Momentum_Rate)
Torque : Symbol = "τ⃗"
Torque : Definition = "r⃗ × F⃗ = dL⃗/dt"
Torque : Type = Pseudovector
```

---

## 10.7 Energy (The Conserved Scalar)

The capacity to do work—universally conserved.

```
Energy := (Energy, 10.7, Work_Capacity)
Energy : Symbol = "E"
Energy : Scalar
Energy : Conserved.When = "Time_Symmetry"
Energy : Units = [J] = [kg·m²/s²]
```

### 10.7.1 Kinetic_Energy

Energy of motion.

```
Kinetic_Energy := (Kinetic_Energy, 10.7.1, Motion_Energy)
Kinetic_Energy : Symbol = "T"
Kinetic_Energy : Definition = "½mv²"     // Point mass
Kinetic_Energy : Always_Positive = True
```

### 10.7.2 Potential_Energy

Energy of position/configuration.

```
Potential_Energy := (Potential_Energy, 10.7.2, Configuration_Energy)
Potential_Energy : Symbol = "V"
Potential_Energy : Definition = "-∫F⃗·dr⃗"  // For conservative forces
Potential_Energy : Configuration_Dependent = True
```

**Common Forms:**
```
// Gravitational (uniform field)
V_gravity_uniform := m.Mul.g.Mul.h

// Gravitational (point masses)
V_gravity_point := Neg.G.Mul.M.Mul.m.Div.r

// Spring (Hooke's law)
V_spring := (1/2).Mul.k.Mul.x.Squared

// Electrostatic
V_electric := q.Mul.φ
```

### 10.7.3 Work

Energy transfer through force over displacement.

```
Work := (Work, 10.7.3, Energy_Transfer)
Work : Symbol = "W"
Work : Definition = "∫F⃗·dr⃗"
Work : Path_Dependent.Unless = "Force_Conservative"
```

### 10.7.4 Power

Rate of energy transfer.

```
Power := (Power, 10.7.4, Energy_Rate)
Power : Symbol = "P"
Power : Definition = "dW/dt = F⃗·v⃗"
Power : Units = [W] = [J/s]
```

---

## 10.8 Field (The Mediator)

A quantity defined at every point in space—the medium of interaction.

```
Field := (Field, 10.8, Spatial_Distribution)
Field : Continuous
Field : Fills_Space
Field : Mediates_Interaction
```

### 10.8.1 Scalar_Field

A field assigning a number to each point.

```
Scalar_Field := (Scalar_Field, 10.8.1, Number_Distribution)
Scalar_Field : Value = Number
Scalar_Field : Example = [Temperature, Pressure, Potential]
```

### 10.8.2 Vector_Field

A field assigning a vector to each point.

```
Vector_Field := (Vector_Field, 10.8.2, Vector_Distribution)
Vector_Field : Value = Vector
Vector_Field : Example = [Velocity_Field, Force_Field, Electric_Field]
```

### 10.8.3 Gravitational_Field

The long-range field generated by mass.

```
Gravitational_Field := (Gravitational_Field, 10.8.3, Mass_Field)
Gravitational_Field : Source = Mass
Gravitational_Field : Conservative = True
Gravitational_Field : Long_Range = True
Gravitational_Field : Always_Attractive = True
```

**Gravitational Potential:**
```
Gravitational_Potential := {
    Symbol = "Φ_g"
    Point_Mass = "-GM/r"
    Continuous = "-G ∫ ρ(r')/|r-r'| dV'"
}
// Poisson equation: ∇²Φ = 4πGρ
```

**Gravitational Force:**
```
Gravitational_Force := {
    Definition = "-m∇Φ_g"
    Point_Masses = "-GMm/r² r̂"
}
```

### 10.8.4 Electromagnetic_Field

The field mediating electric and magnetic interactions.

```
Electromagnetic_Field := (Electromagnetic_Field, 10.8.4, Charge_Field)
Electromagnetic_Field : Source = Charge_And_Current
Electromagnetic_Field : Conservative.Static = True
Electromagnetic_Field : Unifies = [Electricity, Magnetism, Light]
```

**Potentials:**
```
Electric_Potential := {
    Symbol = "φ"
    Point_Charge = "q/(4πε₀r)"
}

Magnetic_Vector_Potential := {
    Symbol = "A⃗"
    Relates_To = "B⃗ = ∇ × A⃗"
}
```

**Fields from Potentials:**
```
Electric_Field := {
    Symbol = "E⃗"
    From_Potential = "-∇φ - ∂A⃗/∂t"
}

Magnetic_Field := {
    Symbol = "B⃗"
    From_Potential = "∇ × A⃗"
}
```

**EM Lagrangian Density:**
```
EM_Lagrangian := {
    Symbol = "ℒ_EM"
    Definition = "-(1/4μ₀)F_μν F^μν - A_μ J^μ"
    Classical_Limit = "½ε₀E² - (1/2μ₀)B² + ρφ - J⃗·A⃗"
}
```

---

## 10.9 Symmetry (The Generator of Laws)

Invariances that, via Noether's theorem, yield conservation laws.

```
Symmetry := (Symmetry, 10.9, Invariance)
Symmetry : Fundamental
Symmetry : Generates = Conservation_Law
```

### 10.9.1 Noether_Theorem

The bridge from symmetry to conservation.

```
Noether_Theorem := (Noether_Theorem, 10.9.1, Symmetry_Conservation_Bridge)
Noether_Theorem : Statement = "Continuous_Symmetry ↔ Conservation_Law"
```

**The Correspondences:**
```
// Time translation invariance
Time_Symmetry := {
    Invariance = "L doesn't depend on t explicitly"
    Conserved = Energy
}

// Space translation invariance
Space_Symmetry := {
    Invariance = "L doesn't depend on position explicitly"
    Conserved = Momentum
}

// Rotation invariance
Rotation_Symmetry := {
    Invariance = "L is rotationally symmetric"
    Conserved = Angular_Momentum
}
```

### 10.9.2 Gauge_Symmetry

Symmetry under field redefinition.

```
Gauge_Symmetry := (Gauge_Symmetry, 10.9.2, Field_Redundancy)
Gauge_Symmetry : Type = "Internal"
Gauge_Symmetry : Example = "φ → φ + const, A⃗ → A⃗ + ∇χ"
Gauge_Symmetry : Conserved = Charge
```

---

## 10.10 Constraint (The Restriction)

Limitations on allowed configurations or motions.

```
Constraint := (Constraint, 10.10, Configuration_Restriction)
Constraint : Limits = Degrees_Of_Freedom
```

### 10.10.1 Holonomic_Constraint

Constraints expressible as f(q, t) = 0.

```
Holonomic := (Holonomic, 10.10.1, Integrable_Constraint)
Holonomic : Form = "f(q₁, q₂, ..., t) = 0"
Holonomic : Reduces_DOF = True
```

**Examples:**
```
Rigid_Pendulum := {
    Constraint = "x² + y² = L²"
    Type = Holonomic
}
```

### 10.10.2 Nonholonomic_Constraint

Constraints involving velocities that cannot be integrated.

```
Nonholonomic := (Nonholonomic, 10.10.2, Velocity_Constraint)
Nonholonomic : Form = "f(q, q̇, t) = 0"
Nonholonomic : Cannot_Integrate = True
```

**Example:**
```
Rolling_Without_Slipping := {
    Constraint = "v = ωR"
    Type = Nonholonomic
}
```

---

## 10.11 Thermodynamics (The Statistical Bridge)

The macroscopic description of systems with many degrees of freedom.

```
Thermodynamics := (Thermodynamics, 10.11, Statistical_Mechanics)
Thermodynamics : Emergent
Thermodynamics : Statistical
Thermodynamics : Irreversible
```

### 10.11.1 Temperature

Average kinetic energy per degree of freedom.

```
Temperature := (Temperature, 10.11.1, Thermal_Energy_Scale)
Temperature : Symbol = "T"
Temperature : Definition = "⟨KE_per_DOF⟩ = ½k_B T"
Temperature : Units = [K]
Temperature : Always_Positive = True
```

### 10.11.2 Entropy

The measure of microscopic uncertainty.

```
Entropy := (Entropy, 10.11.2, Disorder_Measure)
Entropy : Symbol = "S"
Entropy : Definition = "k_B ln Ω"
Entropy : Units = [J/K]
Entropy : Increases = "Second_Law"
```

**Boltzmann Entropy:**
```
Entropy.Boltzmann := {
    Definition = "k_B ln Ω"
    Ω = Number_Of_Microstates
}
```

**The Second Law:**
```
Second_Law := {
    Statement = "ΔS_universe ≥ 0"
    Arrow_Of_Time = True
    Statistical = True
}
```

### 10.11.3 Pressure

Force per unit area from molecular collisions.

```
Pressure := (Pressure, 10.11.3, Surface_Force)
Pressure : Symbol = "p"
Pressure : Definition = "F/A"
Pressure : Units = [Pa] = [N/m²]
```

**Ideal Gas:**
```
Ideal_Gas := {
    Equation = "pV = Nk_B T"
    Assumptions = ["Point_Particles", "No_Interactions", "Elastic_Collisions"]
}
```

### 10.11.4 Boltzmann_Distribution

The probability of a microstate at thermal equilibrium.

```
Boltzmann_Distribution := (Boltzmann_Distribution, 10.11.4, Equilibrium_Probability)
Boltzmann_Distribution : Definition = "P(E) ∝ exp(-E/k_B T)"
```

**Partition Function:**
```
Partition_Function := {
    Symbol = "Z"
    Definition = "Σ exp(-E_i/k_B T)"
    Generates = All_Thermodynamic_Quantities
}

// Free Energy
Free_Energy := {
    Symbol = "F"
    Definition = "-k_B T ln Z"
}
```

---

## 10.12 Fluid (The Continuous Medium)

Matter in continuous, deformable motion.

```
Fluid := (Fluid, 10.12, Continuous_Flow)
Fluid : Continuum
Fluid : Deformable
Fluid : Types = [Liquid, Gas]
```

### 10.12.1 Velocity_Field

The fluid velocity at each point.

```
Velocity_Field := (Velocity_Field, 10.12.1, Flow_Description)
Velocity_Field : Symbol = "v⃗(r⃗, t)"
Velocity_Field : Type = Vector_Field
```

### 10.12.2 Density_Field

Mass per unit volume at each point.

```
Density_Field := (Density_Field, 10.12.2, Mass_Distribution)
Density_Field : Symbol = "ρ(r⃗, t)"
Density_Field : Type = Scalar_Field
Density_Field : Conservation = "∂ρ/∂t + ∇·(ρv⃗) = 0"
```

### 10.12.3 Navier_Stokes

The equation of motion for viscous fluids—derived from action principle applied to continuum.

```
Navier_Stokes := (Navier_Stokes, 10.12.3, Fluid_Dynamics)
Navier_Stokes : Symbol = "NS"
Navier_Stokes : Definition = "ρ(∂v⃗/∂t + v⃗·∇v⃗) = -∇p + μ∇²v⃗ + f⃗"
```

**Terms:**
```
// Left side: Inertia (ma per unit volume)
Inertia_Term := ρ.Mul.(Velocity.Time_Derivative.Add.(Velocity.Dot.Gradient.Velocity))

// Right side: Forces per unit volume
Pressure_Force := Pressure.Gradient.Neg
Viscous_Force := μ.Mul.Velocity.Laplacian
Body_Force := f  // Gravity, electromagnetic, etc.
```

### 10.12.4 Reynolds_Number

The dimensionless ratio determining flow character.

```
Reynolds_Number := (Reynolds_Number, 10.12.4, Flow_Regime)
Reynolds_Number : Symbol = "Re"
Reynolds_Number : Definition = "ρvL/μ = Inertia/Viscosity"
Reynolds_Number : Dimensionless = True
```

**Scale Bridge:**
```
// Low Re (microbes, small particles)
Low_Reynolds := {
    Range = "Re << 1"
    Dominates = Viscosity
    Behavior = "Laminar, reversible, stops instantly"
    Example = ["Bacteria", "Microfluidics", "Sedimentation"]
}

// High Re (planets, atmospheres)
High_Reynolds := {
    Range = "Re >> 1"
    Dominates = Inertia
    Behavior = "Turbulent possible, persistent motion"
    Example = ["Weather", "Ocean_Currents", "Aircraft"]
}

// Transition
Transition := {
    Range = "Re ~ 10³ to 10⁵"
    Behavior = "Laminar to turbulent transition"
    Stall_Prone = True   // Turbulence onset is a Stall condition
}
```

---

## 10.13 Constants (Fundamental Numbers)

The dimensionful constants that set physical scales.

```
Constants := (Constants, 10.13, Fundamental_Values)
Constants : Measured
Constants : Universal
Constants : Immutable
```

### 10.13.1 Gravitational Constant

```
G := (G, 10.13.1, Newton_Constant)
G : Value = 6.674e-11
G : Units = [m³/(kg·s²)]
G : Couples = Mass_To_Gravity
```

### 10.13.2 Speed of Light

```
c := (c, 10.13.2, Light_Speed)
c : Value = 299792458
c : Units = [m/s]
c : Maximum_Speed = True
c : Defines = Meter
```

### 10.13.3 Boltzmann Constant

```
k_B := (k_B, 10.13.3, Thermal_Scale)
k_B : Value = 1.381e-23
k_B : Units = [J/K]
k_B : Bridges = [Microscopic, Macroscopic]
```

### 10.13.4 Vacuum Permittivity

```
ε_0 := (ε_0, 10.13.4, Electric_Constant)
ε_0 : Value = 8.854e-12
ε_0 : Units = [F/m]
```

### 10.13.5 Vacuum Permeability

```
μ_0 := (μ_0, 10.13.5, Magnetic_Constant)
μ_0 : Value = 1.257e-6
μ_0 : Units = [H/m]
μ_0 : Related = "c² = 1/(ε_0 μ_0)"
```

---

# Section 11.0: Relations — The Transformations of Physics

Relations in the Physics Dictionary express the operations and transformations that connect physical Objects.

---

## 11.1 Kinematic Relations

Motion description transformations.

### 11.1.1 Differentiate

Take time derivative.

```
Differentiate := (Differentiate, 11.1.1, Time_Derivative)
Differentiate : Subject : Any_Quantity
Differentiate : Returns = Rate_Of_Change
```

**Usage:**
```
Position.Differentiate → Velocity
Velocity.Differentiate → Acceleration
Momentum.Differentiate → Force
```

### 11.1.2 Integrate

Take time integral.

```
Integrate := (Integrate, 11.1.2, Time_Integral)
Integrate : Subject : Rate
Integrate : Returns = Accumulated_Quantity
```

**Usage:**
```
Velocity.Integrate.Over.(t1, t2) → Displacement
Acceleration.Integrate.Over.(t1, t2) → Velocity_Change
Power.Integrate.Over.Time → Work
```

### 11.1.3 Transform

Change coordinate system.

```
Transform := (Transform, 11.1.3, Coordinate_Change)
Transform : Subject : Vector_Or_Tensor
Transform : To = New_Frame
```

**Usage:**
```
Position.Transform.To.Polar → (r, θ)
Velocity.Transform.To.Rotating_Frame → v⃗' + ω⃗×r⃗
```

---

## 11.2 Dynamical Relations

Force and motion connections.

### 11.2.1 Apply_Force

Exert force on object.

```
Apply_Force := (Apply_Force, 11.2.1, Force_Application)
Apply_Force : Subject : Force
Apply_Force : Target : Particle_Or_Body
Apply_Force : Effect = Acceleration
```

**Usage:**
```
Gravity.Apply_Force.To.Ball → Ball.Acceleration = g
Spring.Apply_Force.To.Mass → Mass.Acceleration = -kx/m
```

### 11.2.2 Conserve

Maintain constant value.

```
Conserve := (Conserve, 11.2.2, Constant_Quantity)
Conserve : Subject : [Energy | Momentum | Angular_Momentum]
Conserve : When = Symmetry_Present
```

**Usage:**
```
System.Energy.Conserve.When.Time_Symmetry
System.Momentum.Conserve.When.No_External_Force
System.Angular_Momentum.Conserve.When.No_External_Torque
```

### 11.2.3 Vary

Perform variational derivative.

```
Vary := (Vary, 11.2.3, Functional_Derivative)
Vary : Subject : Action_Or_Lagrangian
Vary : With_Respect_To = Path
Vary : Returns = Euler_Lagrange_Equation
```

**Usage:**
```
Action.Vary.Path → δS = 0 → Equations_Of_Motion
Lagrangian.Vary.Field → Field_Equations
```

---

## 11.3 Field Relations

Operations on fields.

### 11.3.1 Gradient

Spatial rate of change of scalar field.

```
Gradient := (Gradient, 11.3.1, Scalar_Derivative)
Gradient : Subject : Scalar_Field
Gradient : Symbol = "∇"
Gradient : Returns = Vector_Field
```

**Usage:**
```
Potential.Gradient → Force_Field
Temperature.Gradient → Heat_Flow_Direction
Pressure.Gradient → Pressure_Force
```

### 11.3.2 Divergence

Flux density of vector field.

```
Divergence := (Divergence, 11.3.2, Source_Density)
Divergence : Subject : Vector_Field
Divergence : Symbol = "∇·"
Divergence : Returns = Scalar_Field
```

**Usage:**
```
Electric_Field.Divergence → ρ/ε₀  (Gauss's Law)
Velocity_Field.Divergence → Expansion_Rate
```

### 11.3.3 Curl

Rotation density of vector field.

```
Curl := (Curl, 11.3.3, Vorticity)
Curl : Subject : Vector_Field
Curl : Symbol = "∇×"
Curl : Returns = Pseudovector_Field
```

**Usage:**
```
Magnetic_Vector_Potential.Curl → Magnetic_Field
Velocity_Field.Curl → Vorticity
```

### 11.3.4 Laplacian

Second spatial derivative.

```
Laplacian := (Laplacian, 11.3.4, Diffusion_Operator)
Laplacian : Symbol = "∇²"
Laplacian : Definition = "∇·∇"
```

**Usage:**
```
Potential.Laplacian → Source_Density
Temperature.Laplacian → Heat_Diffusion
```

---

## 11.4 Thermodynamic Relations

Statistical mechanics operations.

### 11.4.1 Equilibrate

Reach thermal equilibrium.

```
Equilibrate := (Equilibrate, 11.4.1, Thermalization)
Equilibrate : Subject : System
Equilibrate : Result = Boltzmann_Distribution
```

### 11.4.2 Average

Take ensemble average.

```
Average := (Average, 11.4.2, Ensemble_Mean)
Average : Subject : Microscopic_Quantity
Average : Returns = Macroscopic_Observable
```

**Usage:**
```
Kinetic_Energy.Average → (3/2)k_B T  (monatomic gas)
Fluctuations.Average.Squared → Variance
```

### 11.4.3 Maximize_Entropy

Find equilibrium state.

```
Maximize_Entropy := (Maximize_Entropy, 11.4.3, Equilibrium_Finding)
Maximize_Entropy : Subject : System
Maximize_Entropy : Constraint = [Energy | Volume | Particle_Number]
Maximize_Entropy : Returns = Equilibrium_State
```

---

## 11.5 Fluid Relations

Continuum mechanics operations.

### 11.5.1 Flow

Fluid motion.

```
Flow := (Flow, 11.5.1, Fluid_Motion)
Flow : Subject : Fluid
Flow : Through = Region
Flow : Governed_By = Navier_Stokes
```

### 11.5.2 Advect

Transport by flow.

```
Advect := (Advect, 11.5.2, Flow_Transport)
Advect : Subject : [Scalar_Field | Tracer]
Advect : By = Velocity_Field
Advect : Rate = "v⃗·∇(quantity)"
```

### 11.5.3 Diffuse

Spread by random motion.

```
Diffuse := (Diffuse, 11.5.3, Molecular_Spreading)
Diffuse : Subject : Concentration_Or_Temperature
Diffuse : Rate = "D∇²(quantity)"
Diffuse : D = Diffusion_Coefficient
```

---

# Section 12.0: Grammar Extensions

The Physics Dictionary extends Uypocode grammar with physics-specific control structures.

---

## 12.1 Minimize

Find the configuration minimizing a quantity.

```
Minimize := (Minimize, 12.1, Optimization)
Minimize : Subject : Functional
Minimize : Over = Configuration_Space
Minimize : Returns = Optimal_Configuration
```

**Syntax:**
```
Action.Minimize.Over.Paths.(Initial_State, Final_State) → Physical_Path
Energy.Minimize.Over.Configurations → Equilibrium
```

---

## 12.2 Evolve

Propagate state forward in time.

```
Evolve := (Evolve, 12.2, Time_Propagation)
Evolve : Subject : State
Evolve : According_To = Equations_Of_Motion
Evolve : Duration = Time_Interval
```

**Syntax:**
```
Particle.State.Evolve.For.Duration.10.Seconds → Final_State
System.Evolve.Until.Equilibrium → Equilibrium_State
```

---

## 12.3 Constrain

Apply constraints to system.

```
Constrain := (Constrain, 12.3, Restriction_Application)
Constrain : Subject : System
Constrain : By = Constraint_Equations
Constrain : Method = [Lagrange_Multipliers | Elimination | Projection]
```

**Syntax:**
```
Pendulum.Constrain.By."r = L" → One_DOF_System
Gas.Constrain.At.Constant.Temperature → Isothermal_Process
```

---

## 12.4 Approximate

Make simplifying assumptions.

```
Approximate := (Approximate, 12.4, Simplification)
Approximate : Subject : System
Approximate : Regime = [Small_Angle | Low_Speed | Weak_Field | ...]
Approximate : Returns = Simplified_System
```

**Syntax:**
```
Pendulum.Approximate.Small_Angle → Simple_Harmonic_Oscillator
Relativity.Approximate.Low_Speed → Newtonian_Mechanics
```

---

## 12.5 Coarse_Grain

Average over microscopic details.

```
Coarse_Grain := (Coarse_Grain, 12.5, Averaging)
Coarse_Grain : Subject : Microscopic_System
Coarse_Grain : Scale = Averaging_Length
Coarse_Grain : Returns = Macroscopic_Description
```

**Syntax:**
```
Molecules.Coarse_Grain.Over.Micron → Fluid_Element
Atoms.Coarse_Grain.Statistically → Thermodynamic_Variables
```

---

## 12.6 Couple

Connect two systems.

```
Couple := (Couple, 12.6, Interaction_Establishment)
Couple : Subject : System_A
Couple : To : System_B
Couple : Via = Interaction_Term
```

**Syntax:**
```
Charge.Couple.To.Field.Via.Charge_Current_Density
Oscillator_A.Couple.To.Oscillator_B.Via.Spring
```

---

# Section 13.0: Workspace Patterns

Common configurations for classical physics problems.

---

## 13.1 Point Particle Mechanics

```
// Define a point particle in gravitational field
Import.Calculus
Import.Vector
Import.Units

Particle := Particle.New
Particle : Mass = 1.0.Kg
Particle : Position = [0, 10, 0].Meters
Particle : Velocity = [5, 0, 0].Meters.Per.Second

Gravity_Field := Gravitational_Field.Uniform
Gravity_Field : g = 9.81.Meters.Per.Second.Squared
Gravity_Field : Direction = [0, -1, 0]

// Lagrangian
L := Particle.Kinetic_Energy.Sub.Particle.Potential_Energy.(In.Gravity_Field)

// Evolve
Particle.State.Evolve.For.2.Seconds.{
    // At each step: Euler-Lagrange
    Acceleration := Gravity_Field.g.Mul.Gravity_Field.Direction.
    Velocity.Add.(Acceleration.Mul.dt).Into.Velocity.
    Position.Add.(Velocity.Mul.dt).Into.Position
}

// Output trajectory
Particle.Position.Emit  // Parabolic path
```

---

## 13.2 Planetary Motion

```
// Two-body gravitational problem
Import.Calculus
Import.Vector

Sun := Particle.New
Sun : Mass = 1.989e30.Kg
Sun : Position = [0, 0, 0].Meters
Sun : Fixed = True  // Approximation

Earth := Particle.New
Earth : Mass = 5.972e24.Kg
Earth : Position = [1.496e11, 0, 0].Meters
Earth : Velocity = [0, 29780, 0].Meters.Per.Second

// Gravitational potential
V := Neg.G.Mul.Sun.Mass.Mul.Earth.Mass.Div.(
    Earth.Position.Sub.Sun.Position.Magnitude
)

// Lagrangian
L := Earth.Kinetic_Energy.Sub.V

// Symmetries and conservation
System.Has.Rotation_Symmetry → Angular_Momentum.Conserved
System.Has.Time_Symmetry → Energy.Conserved

// Orbit emerges from δS = 0
Earth.State.Evolve.For.1.Year → Elliptical_Orbit
```

---

## 13.3 Fluid Flow at Different Scales

```
// Compare microbe and ocean currents
Import.Calculus
Import.Vector
Import.Units

// Microbe (low Reynolds)
Microbe := Fluid_Element.New
Microbe : Density = 1000.Kg.Per.Cubic.Meter
Microbe : Velocity = 30.Micrometers.Per.Second
Microbe : Length = 10.Micrometers
Microbe : Viscosity = 1e-3.Pascal.Seconds

Microbe.Reynolds_Number := {
    Self.Density.Mul.Self.Velocity.Mul.Self.Length.Div.Self.Viscosity
}
Microbe.Reynolds_Number.Emit  // Re ≈ 3×10⁻⁴ << 1
// Viscosity dominates: motion stops instantly when force stops

// Ocean current (high Reynolds)
Ocean := Fluid_Element.New
Ocean : Density = 1025.Kg.Per.Cubic.Meter
Ocean : Velocity = 1.Meter.Per.Second
Ocean : Length = 1000.Km
Ocean : Viscosity = 1e-3.Pascal.Seconds

Ocean.Reynolds_Number.Emit  // Re ≈ 10¹² >> 1
// Inertia dominates: currents persist, turbulence possible
```

---

## 13.4 Thermal Equilibrium

```
// Gas reaching equilibrium
Import.Statistics
Import.Units

Gas := System.New
Gas : Particle_Count = 6.022e23  // One mole
Gas : Volume = 22.4.Liters
Gas : Initial_Energy_Distribution = Arbitrary

// Equilibrate
Gas.Equilibrate.At.Temperature.300.K

// Now Boltzmann distributed
Gas.Energy_Distribution := Boltzmann_Distribution.With.{
    Temperature = Gas.Temperature
    k_B = Constants.k_B
}

// Probability of state with energy E
P(E) := Exp.Neg.(E.Div.(Constants.k_B.Mul.Gas.Temperature))

// Entropy
Gas.Entropy := Constants.k_B.Mul.Ln.(Gas.Microstates.Count)

// Check: entropy has increased from initial arbitrary state
Gas.Entropy.Gt.Gas.Initial_Entropy → True  // Second Law satisfied
```

---

## 13.5 Harmonic Oscillator (Canonical Example)

```
// The harmonic oscillator: foundation of all small-oscillation physics
Import.Calculus

Oscillator := System.New
Oscillator : Mass = m
Oscillator : Spring_Constant = k
Oscillator : Position = x
Oscillator : Velocity = v

// Lagrangian
Oscillator.L := {
    T := (1/2).Mul.m.Mul.v.Squared.
    V := (1/2).Mul.k.Mul.x.Squared.
    T.Sub.V
}

// Euler-Lagrange equation
Oscillator.EOM := {
    // d/dt(∂L/∂v) = ∂L/∂x
    // d/dt(mv) = -kx
    // ma = -kx
    Acceleration = Neg.k.Div.m.Mul.x
}

// Solution
ω := Sqrt.(k.Div.m)  // Natural frequency
Oscillator.Position.(t) := A.Mul.Cos.(ω.Mul.t.Add.φ)

// Energy conservation
E := (1/2).Mul.m.Mul.ω.Squared.Mul.A.Squared  // Constant!

// Hamiltonian formulation
Oscillator.H := {
    p := m.Mul.v.  // Momentum
    (p.Squared.Div.(2.Mul.m)).Add.((1/2).Mul.k.Mul.x.Squared)
}
```

---

# Section 14.0: Stall Semantics in Physics

Physical Stalls represent meaningful physical situations where resolution requires additional information, boundary conditions, or approximations.

```
Physics_Stall := (Physics_Stall, 14.0, Physical_Incompleteness)
Physics_Stall : Extends = Stall
Physics_Stall : Domain = Classical_Physics
```

---

## 14.1 Boundary Stalls

```
Boundary_Stall := (Boundary_Stall, 14.1, Missing_Conditions)
```

| Stall Situation | Physical Interpretation |
|-----------------|--------------------------|
| No initial conditions | Trajectory undetermined |
| No boundary conditions | Field solution non-unique |
| Incompatible boundaries | Physical impossibility |
| Infinite domain | Regularization needed |

**Example:**
```
Wave_Equation.Solve.Without.Boundary_Conditions → Stall
// Resolution: Specify boundaries
Wave_Equation.Solve.With.{
    At.x=0 : Amplitude = 0.
    At.x=L : Amplitude = 0
} → Standing_Wave_Solutions
```

---

## 14.2 Singularity Stalls

```
Singularity_Stall := (Singularity_Stall, 14.2, Divergence)
```

| Stall Situation | Physical Interpretation |
|-----------------|--------------------------|
| r → 0 in gravity/EM | Point source idealization breakdown |
| v → c | Relativistic regime |
| T → 0 | Quantum regime |
| ∇²φ → ∞ | Source concentration |

**Example:**
```
Gravitational_Potential.At.(r = 0) → Stall (Φ → -∞)
// Resolution: Point mass is approximation; real mass has extent
Gravitational_Potential.At.(r = 0).For.Extended_Mass → Finite
```

---

## 14.3 Turbulence Stalls

```
Turbulence_Stall := (Turbulence_Stall, 14.3, Chaotic_Regime)
```

| Stall Situation | Physical Interpretation |
|-----------------|--------------------------|
| Re >> Re_critical | Laminar solution invalid |
| Long-time prediction | Chaos limits predictability |
| Averaging needed | Statistical description required |

**Example:**
```
Navier_Stokes.Solve.At.High_Reynolds → Stall (Turbulence onset)
// Resolution: Statistical methods
Flow.Coarse_Grain.Statistically → Reynolds_Averaged_Equations
Flow.Describe.Probabilistically → Turbulence_Model
```

---

## 14.4 Scale Stalls

```
Scale_Stall := (Scale_Stall, 14.4, Regime_Breakdown)
```

| Stall Situation | Physical Interpretation |
|-----------------|--------------------------|
| Length ~ atomic scale | Continuum breaks down |
| Time ~ Planck time | Classical time undefined |
| Energy ~ rest mass | Relativistic effects |
| Action ~ ℏ | Quantum effects |

**Example:**
```
Classical_Mechanics.Apply.At.(Action ~ ℏ) → Stall
// Resolution: Quantum mechanics required
System.Evolve.With.Quantum_Corrections → Valid_Description
```

---

# Appendix A: Complete Address Index

## Section 0.x - Kernel Extensions
| Address | Label |
|---------|-------|
| 0.0.10 | Physics_Kernel |
| 0.10.1 | Calculus |
| 0.10.2 | Vector |
| 0.10.3 | Geometry |
| 0.10.4 | Statistics |
| 0.10.5 | Units |

## Section 10.x - Objects
| Address | Label |
|---------|-------|
| 10.1 | Action |
| 10.1.1 | Lagrangian |
| 10.1.2 | Euler_Lagrange |
| 10.1.3 | Hamiltonian |
| 10.2 | Matter |
| 10.2.1 | Particle |
| 10.2.2 | Rigid_Body |
| 10.2.3 | Continuum |
| 10.3 | Space |
| 10.3.1 | Position |
| 10.3.2 | Displacement |
| 10.3.3 | Path |
| 10.4 | Time |
| 10.4.1 | Instant |
| 10.4.2 | Duration |
| 10.4.3 | Rate |
| 10.5 | Kinematics |
| 10.5.1 | Velocity |
| 10.5.2 | Acceleration |
| 10.5.3 | Angular_Velocity |
| 10.6 | Dynamics |
| 10.6.1 | Force |
| 10.6.2 | Momentum |
| 10.6.3 | Angular_Momentum |
| 10.6.4 | Torque |
| 10.7 | Energy |
| 10.7.1 | Kinetic_Energy |
| 10.7.2 | Potential_Energy |
| 10.7.3 | Work |
| 10.7.4 | Power |
| 10.8 | Field |
| 10.8.1 | Scalar_Field |
| 10.8.2 | Vector_Field |
| 10.8.3 | Gravitational_Field |
| 10.8.4 | Electromagnetic_Field |
| 10.9 | Symmetry |
| 10.9.1 | Noether_Theorem |
| 10.9.2 | Gauge_Symmetry |
| 10.10 | Constraint |
| 10.10.1 | Holonomic |
| 10.10.2 | Nonholonomic |
| 10.11 | Thermodynamics |
| 10.11.1 | Temperature |
| 10.11.2 | Entropy |
| 10.11.3 | Pressure |
| 10.11.4 | Boltzmann_Distribution |
| 10.12 | Fluid |
| 10.12.1 | Velocity_Field |
| 10.12.2 | Density_Field |
| 10.12.3 | Navier_Stokes |
| 10.12.4 | Reynolds_Number |
| 10.13 | Constants |
| 10.13.1 | G |
| 10.13.2 | c |
| 10.13.3 | k_B |
| 10.13.4 | ε_0 |
| 10.13.5 | μ_0 |

## Section 11.x - Relations
| Address | Label |
|---------|-------|
| 11.1.1 | Differentiate |
| 11.1.2 | Integrate |
| 11.1.3 | Transform |
| 11.2.1 | Apply_Force |
| 11.2.2 | Conserve |
| 11.2.3 | Vary |
| 11.3.1 | Gradient |
| 11.3.2 | Divergence |
| 11.3.3 | Curl |
| 11.3.4 | Laplacian |
| 11.4.1 | Equilibrate |
| 11.4.2 | Average |
| 11.4.3 | Maximize_Entropy |
| 11.5.1 | Flow |
| 11.5.2 | Advect |
| 11.5.3 | Diffuse |

## Section 12.x - Grammar Extensions
| Address | Label |
|---------|-------|
| 12.1 | Minimize |
| 12.2 | Evolve |
| 12.3 | Constrain |
| 12.4 | Approximate |
| 12.5 | Coarse_Grain |
| 12.6 | Couple |

## Section 13.x - Workspace Patterns
| Address | Label |
|---------|-------|
| 13.1 | Point_Particle_Mechanics |
| 13.2 | Planetary_Motion |
| 13.3 | Fluid_Flow |
| 13.4 | Thermal_Equilibrium |
| 13.5 | Harmonic_Oscillator |

## Section 14.x - Stall Semantics
| Address | Label |
|---------|-------|
| 14.1 | Boundary_Stall |
| 14.2 | Singularity_Stall |
| 14.3 | Turbulence_Stall |
| 14.4 | Scale_Stall |

---

# Appendix B: Quick Reference

## The Variational Hierarchy

```
Symmetry → (Noether) → Conservation Law
Action S = ∫L dt → (δS = 0) → Euler-Lagrange → Equations of Motion
Lagrangian L = T - V → (Legendre) → Hamiltonian H = T + V
```

## Core Equations

| Domain | Equation | Form |
|--------|----------|------|
| All | Euler-Lagrange | d/dt(∂L/∂q̇) - ∂L/∂q = 0 |
| Particles | Newton's Second | F = ma |
| Rigid Bodies | Euler's Equations | I·α + ω×(I·ω) = τ |
| Fluids | Navier-Stokes | ρ(∂v/∂t + v·∇v) = -∇p + μ∇²v + f |
| Thermal | Boltzmann | P(E) ∝ e^(-E/k_B T) |
| Gravity | Poisson | ∇²Φ = 4πGρ |
| EM | Maxwell | ∇·E = ρ/ε₀, ∇×B = μ₀J + ∂E/∂t, ... |

## Conservation Laws (via Noether)

| Symmetry | Conserved Quantity |
|----------|-------------------|
| Time translation | Energy |
| Space translation | Momentum |
| Rotation | Angular Momentum |
| Gauge | Charge |

## Scale Regimes

| Regime | Characteristic | Physics |
|--------|----------------|---------|
| Re << 1 | Viscous | Stokes flow, microbes |
| Re >> 1 | Inertial | Turbulence, weather |
| v << c | Non-relativistic | Classical mechanics |
| v ~ c | Relativistic | Special relativity |
| Action ~ ℏ | Quantum | Quantum mechanics |

## Essential Relations

| Relation | Input → Output |
|----------|----------------|
| Differentiate | Position → Velocity |
| Integrate | Force → Work |
| Gradient | Potential → Force |
| Vary | Action → Equations of Motion |
| Minimize | Energy → Equilibrium |
| Evolve | State → Future State |

---

# Appendix C: Integration Points

## With Life Dictionary (Section 1.x)

Metabolism couples to thermodynamics:
```
Cell.Metabolism := {
    ATP_Hydrolysis.Free_Energy.Release.
    Entropy_Export.To.Environment.
    Local_Order.Maintained.While.Universe_Entropy.Increases
}
```

Locomotion at different scales:
```
Bacterium.Swim.At.Low_Reynolds → Viscous_Drag_Dominates
Whale.Swim.At.High_Reynolds → Inertia_Dominates
```

## With Consciousness Dictionary

Neural dynamics as physical system:
```
Neuron.Membrane := {
    Ion_Gradients.Create.Potential.
    Nernst_Equation.Governs.
    Diffusion.Balance.Drift
}

Neural_Network := {
    Energy_Landscape.Has.Attractors.
    Memory.As.Fixed_Points.
    Thought.As.Trajectory
}
```

## With Recursion Dictionary (Section 8.x)

Feedback loops in physics:
```
Thermostat := Negative_Feedback.New
Thermostat : Setpoint = Desired_Temperature
Thermostat : Gain = Heater_Power / Temperature_Difference
Thermostat : Delay = Thermal_Lag

Climate := Multi_Loop_System.New
Climate.Loops := [
    Positive_Feedback.New.(Subject = "Ice_Albedo"),
    Negative_Feedback.New.(Subject = "Radiation_Cooling"),
    Nested_Loops.(Subject = "Ocean_Atmosphere_Coupling")
]
```

## With Master Dictionary (Section 5.x)

Physics-specific stall handling:
```
Stall.Type.When.[
    "Boundary_Missing" : Request_Boundary_Conditions,
    "Singularity" : Apply_Regularization,
    "Turbulence" : Switch_To_Statistical,
    "Scale_Breakdown" : Flag_Regime_Change
]
```

---

# Appendix D: The Fundamental Insight

```
// The universe is lazy.
// It finds the path of least action.
// All of classical physics is the elaboration of this single principle.

Universe := Action.Minimizer
Universe.Behavior := {
    Action.Minimize.Over.All_Possible_Paths
}

// What seems like force is geometry.
// What seems like law is symmetry.
// What seems like chaos is complexity we cannot track.

Newton_To_Lagrange := {
    // Newton: F = ma (vector, frame-dependent)
    // Lagrange: δS = 0 (scalar, coordinate-free)
    // Same physics, different insight
}

// The Stall is not failure in physics.
// The Stall is where classical physics admits its limits:
//   - Singularities point to finer structure
//   - Turbulence points to irreducible complexity  
//   - Scale breakdowns point to deeper theories

Classical.Limits := {
    Small_Action → Quantum.Required.
    High_Speed → Relativity.Required.
    Strong_Gravity → General_Relativity.Required.
    High_Temperature → Statistical_Mechanics.Required
}

// Every Stall in classical physics
// is an invitation to a deeper theory.
// The Stall is the engine of physics.
```

---

**End of Uypocode Classical Physics Dictionary v0.1**
