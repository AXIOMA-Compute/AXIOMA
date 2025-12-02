# DYNAMIC_VALUE_MODEL.md  
## Dynamic Task-Responsive Value Model for Terra / Axioma / JAM

This document defines the dynamic value model used to compute  
human-aligned values that adapt to different tasks and contexts.

The goal is to have a **single conceptual value function** that can  
change its behavior depending on what is being evaluated  
(e.g. water, education, housing, energy),  
while remaining mathematically consistent and verifiable.

---

## 1. Core Idea

Instead of one static formula for all situations,  
we use a **meta-equation** that can adapt to the specific task.

For a given task `task`, the value is:

$begin:math:display$
V\_\{\\text\{task\}\} \= F\_\{\\text\{task\}\}\\big\(S\, D\, Q\, U\, R\, T\\big\)
$end:math:display$

Where:

- `S` = Scarcity  
- `D` = Distribution  
- `Q` = Quality  
- `U` = Utility (benefit for the community)  
- `R` = Risk / Harm  
- `T` = Time / Long-term impact  

`F_task` defines how these components are combined for a specific task.

---

## 2. Linear Weight Model (Base Form)

In the simplest form, `F_task` is a weighted combination:

$begin:math:display$
V\_\{\\text\{task\}\} \= 
w\_S\(\\text\{task\}\) \\cdot S \+
w\_D\(\\text\{task\}\) \\cdot D \+
w\_Q\(\\text\{task\}\) \\cdot Q \+
w\_U\(\\text\{task\}\) \\cdot U \-
w\_R\(\\text\{task\}\) \\cdot R \+
w\_T\(\\text\{task\}\) \\cdot T
$end:math:display$

Where:

- `w_S(task)` … `w_T(task)` are **task-specific weights**,  
- all weights are **transparent**, **governed**, and **verifiable**,  
- the minus sign in front of `R` reflects that risk/harm *reduces* value.

The formula is **structurally stable**,  
but the weights make it **task-responsive**.

---

## 3. Variables

### 3.1 Scarcity (S)

Represents how limited a resource or capability is.

Examples:
- physical scarcity (water, land, energy)  
- access scarcity (education, healthcare, housing)  

Higher scarcity usually increases the value of positive contributions.

---

### 3.2 Distribution (D)

Represents how fairly and effectively access is distributed  
across the population or community.

- High value if access is broad and equitable.  
- Low value if access is concentrated and exclusionary.  

---

### 3.3 Quality (Q)

Represents how usable, safe, clean, or effective something is.

Examples:
- water purity  
- teaching quality  
- housing safety  
- energy cleanliness  

Poor quality reduces real value, even if quantity is high.

---

### 3.4 Utility (U)

Represents the real functional benefit to the community:

- Does it improve health, knowledge, stability, resilience?  
- Does it enable people to live, learn, work, and grow?  

---

### 3.5 Risk / Harm (R)

Represents the damage, danger, or negative side effects:

- health risks  
- environmental damage  
- social instability  
- long-term systemic harm  

Risk *subtracts* from value.

---

### 3.6 Time / Long-Term Impact (T)

Represents how strong the long-term effect is:

- Does the effect persist?  
- Does it compound over time (like education)?  
- Does it degrade over time (like short-term fixes)?  

Positive long-term impact increases value significantly.

---

## 4. Task-Dependent Weight Profiles

Each `task` has its own weight profile:

```txt
w_profile(task) = {
    w_S(task),
    w_D(task),
    w_Q(task),
    w_U(task),
    w_R(task),
    w_T(task)
}
```

The model is **dynamic** because:

- different tasks highlight different dimensions,  
- but the underlying structure remains consistent.

---

## 5. Examples

### 5.1 Water Supply (`task = "water"`)

For water, the key dimensions are:

- Scarcity (S): high relevance  
- Quality (Q): extremely high (health, cognition, survival)  
- Distribution (D): very important (who gets clean water?)  
- Utility (U): always high  
- Risk (R): high (illness, cognitive loss, systemic health cost)  
- Time (T): strong long-term effects  

Informally:

```txt
w_Q(water)  = very high
w_R(water)  = very high
w_T(water)  = high
w_S(water)  = medium-high
w_D(water)  = medium-high
w_U(water)  = high
```

So the system reacts strongly to changes in quality, risk, and long-term impact.

---

### 5.2 Education (`task = "education"`)

For education:

- Scarcity (S): access-based, not physical  
- Quality (Q): very important (good vs. bad education)  
- Distribution (D): crucial (who can learn?)  
- Utility (U): extremely high (knowledge, productivity, resilience)  
- Risk (R): mostly in form of lost potential if absent  
- Time (T): massive long-term compounding effects  

Informally:

```txt
w_T(education) = very high
w_U(education) = very high
w_Q(education) = high
w_D(education) = high
w_S(education) = medium
w_R(education) = medium (risk of lacking education)
```

The model reacts especially to long-term and utility dimensions.

---

## 6. How the Model "Moves" (Dynamic Behavior)

The equation itself remains:

$begin:math:display$
V\_\{\\text\{task\}\} \= \\sum\_i w\_i\(\\text\{task\}\) \\cdot X\_i
$end:math:display$

But:

- when `task = "water"` → weights emphasize `Q`, `R`, `T`, `S`, `D`  
- when `task = "education"` → weights emphasize `T`, `U`, `Q`, `D`  
- when `task = "housing"` → different emphasis again  
- etc.

The **structure is stable**,  
the **interpretation is dynamic**.

---

## 7. Role of Terra, Axioma, and JAM

### 7.1 Terra

Terra provides the **measured values**:

- `S`, `D`, `Q`, `U`, `R`, `T`  
- grounded in real-world community data  
- aligned with human life and societal reality  

Terra also participates in the governance of:

- which tasks exist  
- which weight profiles are valid  

---

### 7.2 Axioma

Axioma verifies:

- that the input values from Terra are valid  
- that the weight profiles used are allowed and approved  
- that no hidden manipulation of weights or inputs occurs  
- that the value computation is deterministic and reproducible  

Axioma prevents:

- political manipulation of weights  
- silent changes in what is considered valuable  
- abuse of the dynamic model to bias outcomes  

---

### 7.3 JAM

JAM executes:

- the concrete value computations  
- large-scale evaluations across many tasks  
- simulations and optimizations based on `V_task`  

JAM handles the heavy compute,  
using the equations that Terra and Axioma define and secure.

---

## 8. Governance and Safety

Because the model is dynamic,  
it must not be freely adjustable by arbitrary actors.

Rules:

1. All weight profiles are publicly visible.  
2. Any change to `w_profile(task)` must go through governance.  
3. Axioma verifies that:
   - governance decisions are correctly executed,  
   - no hidden or backdoor changes occur.  
4. Terra expresses what the community values through behavior and measurable outcomes,  
   not just through opinion or majority votes.  

The dynamic value model is:

- adaptive but not arbitrary  
- human-aligned but mathematically enforced  
- responsive to context but protected from manipulation  

---

## 9. Summary

The DYNAMIC VALUE MODEL:

- uses a single equation template,  
- adapts to different tasks through weight profiles,  
- integrates human reality (Terra),  
- enforces mathematical truth (Axioma),  
- and scales computation (JAM).

It allows value to be:

- context-sensitive,  
- human-centered,  
- long-term aware,  
- and still precisely computable and verifiable.

---

# End of Document
