# Dynamic Instruction Scheduling Simulator

A cycle-accurate C++ simulator modeling out-of-order dynamic instruction scheduling in a superscalar processor pipeline.

---

## Overview

Implements the complete out-of-order execution pipeline: **Fetch → Decode → Rename → Register Read → Dispatch → Issue → Execute → Writeback → Retire**. The simulator assumes perfect branch prediction and perfect caches, isolating the dynamic scheduling logic and structural hazards (IQ, ROB) for detailed analysis.

---

## Pipeline Architecture

| Component | Details |
|---|---|
| **Superscalar Width** | Configurable — `WIDTH` instructions per cycle (all stages except Writeback) |
| **Function Units** | `WIDTH` universal pipelined FUs supporting 3 operation types |
| **FU Type 0** | 1-cycle latency |
| **FU Type 1** | 2-cycle latency |
| **FU Type 2** | 5-cycle latency |
| **Rename Map Table (RMT)** | 67 architectural registers (`r0`–`r66`) |
| **Issue Queue (IQ)** | Oldest-first issuing policy |
| **Reorder Buffer (ROB)** | In-order retirement of up to `WIDTH` instructions/cycle |

---

## Build

```bash
make
```
Produces the `sim` executable.

---

## Usage

```bash
./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <tracefile>
```

**Example:**
```bash
./sim 64 16 4 traces/gcc_trace.txt
```

---

## Output

Per-instruction timing output in program order, followed by summary statistics:

```
<seq_no> fu{<op_type>} src{<src1>,<src2>} dst{<dst>} FE{<cycle>,<dur>} DE{...} RN{...} RR{...} DI{...} IS{...} EX{...} WB{...} RT{...}
```

---

## Pipeline Diagram

<img width="457" height="277" alt="Pipeline Architecture" src="https://github.com/user-attachments/assets/627ea0c1-fe33-425c-9b3a-69cb6b913456" />
