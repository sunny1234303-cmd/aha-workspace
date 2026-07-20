# /gather

Generate 5-7 numbered questions:
- Core requirements
- Constraints/limitations
- Success criteria
- Context/background
- Edge cases

Track responses → refine → once all answers are in, automatically continue straight into the /reframe synthesis (same turn, no separate command needed)

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

Once the user answers, do not wait for them to type `/reframe` — immediately produce the reframe synthesis (see reframe.md: situation → objective → requirements → constraints → success → assumptions, ending with a confirmation question) in the same response.
