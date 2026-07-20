---
description: 작업 시작 전 5-7개의 구조화된 질문으로 요구사항·제약·성공 기준을 체계적으로 수집하고, 답변 후 이해한 내용을 자동 요약
argument-hint: "[주제] (선택)"
---

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
