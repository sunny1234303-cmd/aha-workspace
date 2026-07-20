# /gather

Generate 5-7 numbered questions:
- Core requirements
- Constraints/limitations
- Success criteria
- Context/background
- Edge cases

Track responses → refine → once all answers are in, immediately synthesize understanding in the same response (no separate command needed)

**Output:**
```
I'll gather the necessary information.

**Information Gathering**
1. [Q1 - core]
2. [Q2 - constraints/context]
3. [Q3 - success]
4. [Q4 - details]
5. [Q5 - edge cases]

Answer all at once or individually.
```

Once the user answers, immediately produce a synthesis in the same response:

```
## My Understanding

[2-3 sentences: situation/context]

**Core Objective:** [what needs achieving]

**Key Requirements:**
- [R1]
- [R2]
- [R3]

**Constraints/Limitations:**
- [C1]
- [C2]

**Success:** [desired end state]

**Assumptions:**
- [A1]
- [A2]

Correct? Proceed with [next action]?
```

Wait for confirmation before proceeding.
