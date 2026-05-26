# Context-Aware Runtime Enforcement

Runtime enforcement framework based on DFA composition supporting strict, soft, and context-dependent enforcement schemes.

This repository implements a set of runtime enforcement algorithms and supporting automata structures.

The framework supports multiple enforcement schemes:

- Strict Enforcement
- Soft Enforcement
- Context-dependent Enforcement
- Serial Composition
- Parallel Composition
- Monolithic Composition
- DFA modification for context-dependent enforcement
- Performance evaluation and visualization

## ⚙️ Features

- DFA-based property modeling
- Runtime event monitoring
- Strict runtime enforcement
- Soft runtime enforcement
- Context-dependent runtime enforcement
- Serial and parallel composition
- Monolithic and compositional approaches
- Performance analysis and comparison

---

This README documents all algorithmic files and experimental scripts included in the repository.

## 📂 Project Structure

```text
MTP/
│
├── helper/
│   ├── Automata.py
│   ├── dfa_definitions.py
│   ├── exclusive_modified_automata.py
│   └── product.py
│
├── Source/
│   ├── Enforcer.py
│   ├── strict_serial.py
│   ├── strict_mono.py
│   ├── strict_parallel.py
│   ├── least_effort_mono.py
│   ├── least_effort_parallel.py
│   ├── exclusive_mono.py
│   ├── exclusive_parallel.py
│   └── exclusive_parallel_opt.py
│
├── Output/
│   ├── Output.py
│   ├── output_strict_serial.py
│   ├── output_strict_mono.py
│   ├── output_strict_parallel.py
│   ├── output_LE_mono.py
│   ├── output_LE_parallel.py
│   ├── output_exclusive_mono.py
│   ├── output_exclusive_parallel.py
│
├── Performance/
│
├── Performance_prop/
│
└── ppt/
```

## 🛠️ Helper Modules

### Automata.py
Defines the DFA class with states, alphabet, transitions, acceptance, and runner utilities.

### dfa_definitions.py

Contains DFA specifications used by enforcement algorithms.

### exclusive_modified_automata.py

Constructs modified DFA A′ for context-dependent enforcement.

### product.py

Contains automata product operations.


## 🖥️ Enforcement Algorithms

### 1. Strict Enforcers

#### strict_serial.py

Implements serial strict enforcement.

#### strict_mono.py

Implements monolithic strict enforcement.

#### strict_parallel.py

Implements parallel strict enforcement.

---

### 2. Soft Enforcers

#### least_effort_mono.py

Implements monolithic soft runtime enforcement.

#### least_effort_parallel.py

Implements parallel soft runtime enforcement.

---

### 3. Context-dependent Enforcers

#### exclusive_mono.py

Implements **Context-dependent Modified Automata (A′)** by:
- Adding don’t-care states
- Redirecting interfering deciding events
- Producing A1′ and A2′

#### exclusive_parallel.py
Implements **Algorithm 7 — Context-dependent Parallel Enforcer** with:
- `σc`, `σs` buffers

## 🏗️ Context-dependent Modified Automata (A′)

For each original DFA A, its modified version A′ is constructed as:

- For every state `q`, create a frozen “don’t-care” state `qX`.
- If an event belongs to **another automaton’s deciding set**, transition:
  
      q  --a(other deciding event)-->  qX

- While in `qX`, ignore all events except own deciding events:

      qX --non-own-deciding--> qX

- On own deciding event, resume normal progress:

      qX --a(own deciding)--> d(q, a)

- All don’t-care states are marked accepting:

      F′(qX) = True

This ensures each automaton responds **only** to its own deciding events, enabling context-dependent monolithic and context-dependent parallel enforcement.

---

## ▶️ Scripts & How to Run

### Strict Enforcers

Run Serial Strict Enforcer:

```bash
python Output/output_strict_serial.py
```

Run Monolithic Strict Enforcer:

```bash
python Output/output_strict_mono.py
```

Run Parallel Strict Enforcer:

```bash
python Output/output_strict_parallel.py
```

---

### Soft Enforcers

Run Monolithic Soft Enforcer:

```bash
python Output/output_LE_mono.py
```

Run Parallel Soft Enforcer:

```bash
python Output/output_LE_parallel.py
```

---

### Context-dependent Enforcers

Run Monolithic Context-dependent Enforcer:

```bash
python Output/output_exclusive_mono.py
```

Run Parallel Context-dependent Enforcer:

```bash
python Output/output_exclusive_parallel.py
```

---

### Ideal Enforcer

Run Ideal Enforcement:

```bash
python Output/Output.py
```


# 📊 Performance Evaluation

The repository includes experimental scripts for evaluating and comparing the runtime behavior of different enforcement schemes.

## 1. Input Size vs Total Execution Time

The `Performance/` folder evaluates how execution time changes as the input trace size increases.

Scripts:

```bash
python Performance/performance_eval.py
python Performance/plot.py
```
### Final experimental results:

**CSV result file :**

```text
performance_results_avg_opt.csv
```

**Final generated plots :**

```text
strict_enforcers_avg_opt.png
least_effort_enforcers_avg_opt.png
exclusive_enforcers_avg_opt.png
```
Generated outputs:

- Execution-time measurements
- CSV result files
- Runtime comparison plots
- Performance graphs for different enforcers

Purpose:

- Analyze scalability with increasing input length
- Compare strict, soft, and context-dependent schemes
- Study total execution time trends

---

## 2. Number of Properties vs Total Execution Time

The `Performance_prop/` folder evaluates how execution time changes as the number of enforced properties increases.

Scripts:

```bash
python Performance_prop/performance_eval_prop.py
python Performance_prop/plot_properties.py
```
### Final experimental results:

**CSV result file :**

```text
performance_properties_avg_opt.csv
```

**Final generated plots :**

```text
strict_enforcers_avg_opt.png
least_effort_enforcers_avg_opt.png
exclusive_enforcers_avg_opt.png
```

Generated outputs:

- Property-scaling measurements
- CSV result files
- Comparative plots
- Scalability graphs

Purpose:

- Analyze behavior under increasing numbers of properties
- Compare enforcement approaches as system complexity grows
- Study total execution time variation

---

## 📁 Generated Outputs

The framework generates:

- Runtime execution traces
- Performance graphs
- CSV result files
- Scalability measurements
- Comparative plots
