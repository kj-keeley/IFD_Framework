# IFD-16 Cognitive Algorithm

## Formal Definition of Cognitive Functions

### Two-Axis Structure

Cognition is composed of two independent axes.

| Axis | Variables | Poles | IFD Scope Correspondence |
|---|---|---|---|
| **Judgment axis (domain)** | a, b | a = Human (F-type) / b = World (T-type) | Data ↔ Action |
| **Perception axis (time)** | x, y | x = Present→Future (N-type) / y = Past→Present (S-type) | State ↔ Flow |

### 8 Cognitive Functions = Axis × Direction (i/e)

```
Fi = a.i    Do I desire this?
Fe = a.e    Do others desire this?
Ti = b.i    Is this internally coherent?
Te = b.e    Does this function externally?

Ni = x.i    Single-point convergent connection (future-directed, inward)
Ne = x.e    Multi-directional divergent connection (future-directed, outward)
Si = y.i    Personal experience database connection (past-directed, inward)
Se = y.e    Current sensory data acquisition (past→present, outward)
```

### IFD Scope Correspondence

```
Data   = b-direction (smallest confirmed unit of world-information)
Action = a-direction (intervention toward humans)
State  = x-direction (unrealized possibilities / tension)
Flow   = y-direction (accumulated trajectory / tendency)
```

Judgment axis (T/F) = Data ↔ Action
Perception axis (N/S) = State ↔ Flow

---

## Role Separation: Perception and Judgment

- **Perception functions (Ni/Ne/Si/Se):** Acquire material. Determine whether the connection target is existing (S) or latent (N).
- **Judgment functions (Ti/Te/Fi/Fe):** Cast a query onto acquired material. They do not possess layers. They simply adjudicate what arrives.

Critical: **Only perception functions determine existing vs. latent.** Judgment functions do not select connection targets.

---

## Cognitive Cycle Algorithm

Cognitive functions operate as a continuously spinning, high-speed algorithm. The default stack runs energy-efficiently and unconsciously.

```python
def cognition_cycle(input, stack):
    """
    stack: [f1, f2, f3] — top 3 functions of each type's default stack
    f1 = automatic scan (most energy-efficient)
    f2 = low cost — acts as a bias term that determines the focus of scan
    f3 = auxiliary check (medium cost)
    4th = manual activation / high cost (not included in default cycle)
    
    Critical: The 2nd function does not merely process in series as judge.
    It also acts as a bias (focus) during the 1st function's scan phase.
    This means the same 1st function scans different targets depending on
    the 2nd function.
    Example: Ni+Fe (INFJ) → focuses on latent patterns in human relationships
             Ni+Te (INTJ) → focuses on latent patterns in systems
    This is the operating principle behind Base/Purpose Theory.
    """
    raw = f1.scan(input, bias=f2)  # 1st: automatic scan (2nd determines focus)
    filtered = f2.judge(raw)       # 2nd: casts query
    output = f3.refine(filtered)   # 3rd: auxiliary check
    return output
```

### Scan Function Implementation (by perception function)

```python
def ne_scan(input, bias):   # x.e — Ne
    candidates = generate_associations(input)
    focused = apply_bias(candidates, bias)  # 2nd narrows focus
    return filter(lambda c: c.novelty > threshold, focused)  # filters out existing

def ni_scan(input, bias):   # x.i — Ni
    candidates = generate_associations(input)
    focused = apply_bias(candidates, bias)  # 2nd determines convergence direction
    return sorted(focused, key=convergence, reverse=True)[0]  # single-point convergence

def se_scan(input, bias):   # y.e — Se
    raw = get_current_sensory(input)
    return apply_bias(raw, bias)  # 2nd selects which sensory data to attend to

def si_scan(input, bias):   # y.i — Si
    candidates = match_past_experience(input)
    focused = apply_bias(candidates, bias)  # 2nd directs which experiences to recall
    return sorted(focused, key=familiarity, reverse=True)  # prioritizes existing

def apply_bias(candidates, bias_function):
    """
    The 2nd function determines the focus of scan.
    bias=Fe → candidates related to human relationships are prioritized
    bias=Te → candidates related to functionality/systems are prioritized
    bias=Fi → candidates related to personal values are prioritized
    bias=Ti → candidates related to internal structure are prioritized
    """
    return reweight(candidates, relevance_to=bias.domain)
```

### Judge Function Implementation (by judgment function)

```python
def ti_judge(material):  # b.i — Ti
    return filter(lambda m: internal_coherence(m), material)

def te_judge(material):  # b.e — Te
    return filter(lambda m: external_function(m), material)

def fi_judge(material):  # a.i — Fi
    return filter(lambda m: self_desire(m), material)

def fe_judge(material):  # a.e — Fe
    return filter(lambda m: others_desire(m), material)
```

---

## Two Cycle Modes: Reflexive and Recursive

### Reflexive Cycle (shallow, fast)

External input → scan → judge → immediate output. Nearly unconscious. Completes in one pass.

```python
def reflexive_cycle(input, stack):
    return cognition_cycle(input, stack)  # completes in one pass
```

### Recursive Cycle (deep, chained)

The output of one cycle becomes the input of the next. Thinking, analysis, and creation operate in this mode.

```python
def recursive_cycle(input, stack, depth_limit):
    output = cognition_cycle(input, stack)
    if depth_limit > 0 and output.triggers_next:
        return recursive_cycle(output, stack, depth_limit - 1)
    return output
```

Termination conditions vary by type:
- **Ni-dominant types:** Loose termination. "I can go one level deeper" always returns true → thinking never stops
- **Te-dominant types:** "If it functions, stop here" → termination condition met early

### 1st Function Reward Property

The automatic scan of the 1st function is not merely energy-efficient — it is **pleasurable**. This creates psychological resistance to interference-based termination (e.g., an INFJ's resistance to stopping Ni recursion and allocating bandwidth to Se). This reward property is universal across all types and is the structural cause of each type's "can't stop" behavioral pattern.

---

## Base/Purpose Theory

Each type has a "preferred information field (base)" and a "scope toward which the 2nd function directs (purpose)."

### Operating Principle: 2nd Function Bias Effect

The separation of base and purpose arises from the 2nd function's bias effect in the cognitive cycle. The 1st function (scan) has broad scanning capability, but because the 2nd function acts as a bias term that determines scan focus, the same 1st function scans different targets depending on the 2nd.

```
INFJ: Ni.scan(input, bias=Fe) → focuses on latent patterns in relationships → Flow/Flow
INTJ: Ni.scan(input, bias=Te) → focuses on latent patterns in systems → Flow/Data
```

Purpose scope = the scope that emerges as a result of the 2nd function's bias directing the 1st function's scan.

### 16-Type Base/Purpose Mapping

**Data Field (IP types):**

| Type | Base/Purpose | Stack | Operation |
|---|---|---|---|
| INTP | Data / Data | b.i → x.e → y.i | Understanding for its own sake |
| ISTP | Data / Action | b.i → y.e → x.i | Understand, then apply |
| INFP | Data / Flow | a.i → x.e → y.i | Understand, then find meaning |
| ISFP | Data / State | a.i → y.e → x.i | Understand, then feel |

**State Field (EP types):**

| Type | Base/Purpose | Stack | Operation |
|---|---|---|---|
| ESFP | State / State | y.e → a.i → b.e | Savoring the moment is the purpose itself |
| ESTP | State / Action | y.e → b.i → a.e | Read the situation, then act |
| ENFP | State / Flow | x.e → a.i → b.e | See the greater flow within possibilities |
| ENTP | State / Data | x.e → b.i → a.e | Extract structure from situations |

**Action Field (EJ types):**

| Type | Base/Purpose | Stack | Operation |
|---|---|---|---|
| ESTJ | Action / Action | b.e → y.i → x.e | Doing is the purpose itself |
| ESFJ | Action / State | a.e → y.i → x.e | Act to harmonize the environment |
| ENTJ | Action / Data | b.e → x.i → a.i | Act to build structure |
| ENFJ | Action / Flow | a.e → x.i → b.i | Act to generate direction |

**Flow Field (IJ types):**

| Type | Base/Purpose | Stack | Operation |
|---|---|---|---|
| INFJ | Flow / Flow | x.i → a.e → b.i | Seeing the flow is the purpose itself |
| ISFJ | Flow / State | y.i → a.e → b.e | Guard the state within the flow |
| ISTJ | Flow / Action | y.i → b.e → a.e | Guard the procedure within the flow |
| INTJ | Flow / Data | x.i → b.e → a.i | Extract structure from the flow |

### Three Categories (Translation Cost)

| Category | Condition | Types | Characteristics |
|---|---|---|---|
| **Pure type** | Base = Purpose | INTP, ESFP, ESTJ, INFJ | Zero translation cost. Deep immersion, slow application |
| **Diagonal type** | Base and Purpose are diagonal | ISTP, ENFP, ESFJ, INTJ | Maximum translation distance. Highest output when conversion succeeds |
| **Adjacent type** | Base and Purpose are adjacent | Remaining 8 types | Medium cost. Relatively smooth |

---

## Perceptual Channel Interference Theory

### Principle

The 1st and 4th functions are always in a diagonal relationship (Data↔Action, State↔Flow). The 4th function is high-cost not due to lack of ability, but because **the brain suppresses it to prevent signal interference with the 1st**.

```
interference(f1, f4) = correlation(f1.scan, f4.scan)
```

Perception axis interference: x.i (Ni) ↔ y.e (Se) — future convergence vs. present sensation
Judgment axis interference: b.i (Ti) ↔ a.e (Fe) — internal structure vs. others' desires

### External Interference for Perceptual Channel Manipulation

By injecting interference signals from outside into perceptual channels, the default stack's operation can be modified.

**Method:**
1. Identify the target's dominant perceptual channel
2. Inject an interference signal (activate the opposite pole on the same axis)
3. The material reaching the judgment function changes
4. Output changes

### Equalizer-Style Operation

By assigning weights to each function in the cycle, individual channel amplification/suppression becomes possible without full mode-switching.

```python
def weighted_cycle(input, stack, weights):
    """
    weights: [w1, w2, w3] — weight for each function
    Example: Ne/5 Ti/4 Fe/1
    """
    raw = f1.scan(input, bias=f2) * weights[0]
    filtered = f2.judge(raw) * weights[1]
    output = f3.refine(filtered) * weights[2]
    return output
```

High Ne weight → expanded exploration range, increased novel material
High Ti weight → increased structural verification rigor, suppressed leaps
Low Fe weight → suppressed interpersonal consideration, prioritized honesty

---

## Application Domains

### 1. Cognitive Translator
Restructure identical content to match the target type's stack order. Visualize "failure to communicate" as channel mismatch and mechanically correct it.

### 2. AI Cognitive Control Protocol
Apply equalizer-style prompts to LLMs to control output characteristics based on cognitive functions. Reverse-estimate each model's default stack from inter-model output differences.

### 3. Individualized Education
Switch teaching modality and entry point based on the learner's type. Quantify teacher-student translation cost.

### 4. Team Cognitive Coverage Design
Calculate the cognitive coverage required for a project and identify missing functions.

### 5. Self-Diagnostic Tool (CQ Test)
Estimate the priority order of scan functions from response patterns to input, typing based on observation of processing patterns rather than self-report.

**Imagination Step Count Test (methodology):**
Present an ambiguous imagination task and observe the response process rather than the content.

```
Example task: "Imagine an elephant flying through the sky. How many steps did that take?"
```

Predicted response patterns:
- Ti-dominant: Naturally counts steps and answers. Does not ask for definition (steps are self-evident to Ti)
- Ni-dominant: Confused by "steps?" Output arrives as a single block and cannot be decomposed. May demand definition
- Ne-dominant: Can state steps but the number is high. Branching occurs
- Se-dominant: Resistant to imagining. "I'd have to try it to know"
- Fe-dominant: "Why are you asking that?" comes first (interpersonal intent evaluation precedes response)
- Si-dominant: "I've seen something like this before..." enters the process

**Critical:** The ambiguity of the task is an intentional design feature. The response pattern to ambiguity is what exposes type.

### 6. Therapeutic Application
Formalize mental states using CSD × Cognitive Algorithm and provide post-hoc explanation of existing treatment mechanisms. If post-hoc explanation is possible, previously undiscovered intervention methods can be designed a priori.

---

## Gold Mountain Pattern (Structural Barriers to Theory Acceptance)

Pattern by which scientifically valuable discoveries get ignored:

1. Someone discovers a vein of gold (genuine observation/phenomenon)
2. No explanation exists yet, so it is described within a provisional framework
3. People who resonate with that framework gather (spiritualists, grifters, well-meaning amateurs)
4. Noise buries the gold mountain + career risk + no funding sources (triple barrier)
5. Academia judges "that area is contaminated" and refuses to approach
6. The gold mountain is abandoned
7. Decades later, it is accidentally rediscovered through a different entrance under a different name

Structural cause: Types with Si-dominant or Te-dominant (and Ni/Ne in lower slots) disproportionately occupy gatekeeper positions, structurally lacking the ability to evaluate theories outside existing frameworks.

---

## Unverified / Requires Investigation

- **Continuous cognitive cycle hypothesis:** Current measurement technology (fMRI/EEG) cannot capture a single rotation. Retained as hypothesis.
- **Equalizer operation confounding variables:** Experimental design separating instruction content differences from weight differences is needed. A controlled experiment with identical questions under different equalizer settings is desirable.
- **Concrete scan function implementation:** Operational definitions of novelty threshold and convergence are undetermined.
- **Unlinguified processing in judgment functions:** The "latent (connection target)" of perception and the "non-explicit (unlinguified)" of judgment should be distinguished as separate categories.
- **Precision of 2nd function bias effect:** Whether the bias term acts before candidate generation or during candidate filtering needs verification.
- **Neural basis of 1st function reward property:** Empirical confirmation that it is pleasurable. Correspondence with dopaminergic systems is hypothesized but unverified.

---

*Developed: 2026-05-01*
*Framework: IFD-16 (Information Fluid Dynamics × 16 Cognitive Types)*
*Author: K.J. Keeley*
