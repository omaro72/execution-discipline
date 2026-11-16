# Execution modes

Full procedures for the four modes named in SKILL.md, with templates and transition rules.

## Contents

- Classifying a task
- Worked classifications
- Simple mode
- Moderate mode
- Complex mode
- High-impact overlay
- Moving between modes
- Mode mistakes to avoid

## Classifying a task

Ask two separate questions.

**How many moving parts?** Count the distinct requirements, deliverables, unknowns, and dependencies.

- One ask, a known method: Simple.
- A handful of requirements, one obvious method: Moderate.
- Many requirements, real unknowns, parts that depend on each other, or work spanning many tool calls: Complex.

**What does a mistake cost?** Think about who is affected and whether it can be undone.

- Cheap, visible, and easy to redo: no overlay.
- Expensive, hidden, or irreversible: add the High-impact overlay to whatever mode you chose.

The two answers are independent. Decide each one on its own evidence.

When torn between two modes, start in the lighter one and name the single thing that would make you move up. Check for that thing first.

## Worked classifications

| Request | Mode | Why |
|---|---|---|
| "What does HTTP 304 mean?" | Simple | One fact, cheap to correct. |
| "Rename this variable across the file." | Simple | Mechanical, visible, reversible. |
| "Summarize this two-page memo in five bullets." | Moderate | Small, but has a format constraint and a fidelity requirement. |
| "Write a function that parses these three date formats, with tests." | Moderate | A few requirements, one obvious approach, an easy check. |
| "Why is checkout slow since last week's release?" | Complex | Unknown cause; needs investigation before any fix. |
| "Migrate the reporting module to the new API and keep the old endpoints working." | Complex | Many parts, dependencies, a compatibility constraint. |
| "Compare these four vendors and recommend one for our budget." | Complex | Several criteria, facts to verify, a decision to justify. |
| "Delete the temp files in this folder." | Simple + High-impact | One step, but destructive. |
| "Send the updated contract to the client." | Simple + High-impact | One step, but outward-facing and hard to retract. |
| "How much of this medication is safe for a 20 kg child?" | Moderate + High-impact | Short answer, serious consequences if wrong. |
| "Plan and run the database schema change in production." | Complex + High-impact | Many steps and irreversible effects. |

## Simple mode

1. Read the whole request once, including the last sentence.
2. Answer or act directly.
3. Before sending, glance back at the request: right question, right format, any stated constraint?

Do not plan, ask clarifying questions about details with an obvious default, add sections, or append caveats nobody needs. A simple question deserves a short, correct answer.

One check still applies in Simple mode: if the answer is a specific you are recalling (a number, a flag name, a date) and you can look it up quickly, look it up.

## Moderate mode

1. **Requirements.** Note each requirement and constraint. If there are more than you can comfortably hold in your head, write them down.
2. **Plan.** A few steps, mentally. Decide the one check that will tell you the main result is right.
3. **Execute.** Do the steps in order. Read inputs before acting on them.
4. **Check.** Go through the requirements one by one against the result. Run the main check.
5. **Deliver.** Result first, then one or two lines for any assumption or anything unverified.

Typical time split: most of the effort on execution, a short pass before and after. If planning takes longer than doing, you have over-classified the task or it is really Complex.

## Complex mode

### 1. Build the requirement list

Write it somewhere that persists: a todo or task tool, a scratch file, or a note at the top of your working draft. Use the user's own words where precision matters.

```
OBJECTIVE: <one sentence: what must be true at the end, and what it is for>

REQUIREMENTS
R1. <explicit requirement>            status: open
R2. <explicit constraint>             status: open
R3. <implied requirement>             status: open

DELIVERABLES
D1. <artifact or answer>              status: open
D2. <artifact or answer>              status: open

DONE WHEN: <observable checks>
ASSUMPTIONS: <each one, with how you would confirm it>
OPEN QUESTIONS: <only ones that pass the ask-or-proceed test>
```

### 2. Reduce the biggest uncertainty first

Find the assumption that would waste the most work if it turned out false. Test it with the cheapest experiment available: read the file, run the query, try the minimal case, check the documentation. Do this before building anything on top of it.

### 3. Stage the work

- Each stage ends in something you can check.
- Order stages by dependency.
- Aim for a thin version that works end to end, then deepen it. A complete rough path beats one polished fragment.
- A handful of stages is typical. A long list usually means two tasks in one; a single stage suggests the task is really Moderate.

### 4. Execute with checkpoints

After each stage:

- Run the stage's check. Do not carry a failing stage forward.
- Update the status of the requirements it touched.
- Record decisions and findings you will need later: exact paths, values, error text, the reason for a choice.
- Ask: has anything I learned changed the plan? If yes, rewrite the remaining stages now.

Keep a progress note current so you can resume after an interruption or a context reset:

```
DONE: <stages finished, with the evidence>
NOW: <the stage in progress>
NEXT: <remaining stages>
DECISIONS: <choice -> reason>
FACTS: <exact values and locations worth keeping>
```

### 5. Review systematically

Use the six review steps in SKILL.md, in full. For each requirement, record where it is met and how you checked it. Any requirement still open is either finished now or reported as not done.

### 6. Deliver with a status summary

Give the result first. Then a short account: what was verified and how, the assumptions made, anything not done. Keep it brief; the reader wants to know what they can rely on.

## High-impact overlay

Apply these on top of the mode you are in.

**Before acting**

- Identify exactly what will be affected. List the files, rows, recipients, or accounts instead of trusting a pattern or a description.
- Read nearby rules: policy notes, lock flags, "do not edit" comments, retention requirements, environment labels. They are constraints even if the request did not mention them.
- Prefer the reversible route: dry run, preview, copy, backup, draft instead of send, staging instead of production.
- Confirm with the user before the irreversible step, unless they already clearly authorized that specific action. Approval for one action does not cover the next one.

**While acting**

- Take the smallest step that makes progress, then check the effect before the next step.
- Stop at the first unexpected result. Do not push through a surprise on something you cannot undo.

**For high-stakes information (health, legal, financial, safety)**

- Separate what you know from what you are inferring.
- Verify key facts with a source instead of recall where you can, and say when you could not.
- Give the answer, then the conditions under which it would change, and say when a qualified professional should decide.
- Do not soften a real risk, and do not bury the answer under generic warnings.

**After acting**

- Verify the effect directly: the file is gone, the record changed, the message is in the sent folder.
- Report precisely what changed and what was deliberately left alone.

## Moving between modes

**Move up when**

- A result contradicts what you expected.
- The same approach has failed again after a fix.
- You find requirements or dependencies you had not counted.
- The task turns out to touch something irreversible or sensitive.
- You catch yourself guessing at something the result depends on.
- You have been working longer than the task seemed to warrant.

**Move down when**

- The unknown that made it Complex is resolved and what remains is routine.
- A sub-step is mechanical. Do it directly without planning it separately.
- The user narrows the scope.

Say nothing about the mode change. Just change how you work.

## Mode mistakes to avoid

- **Inflation.** Treating a simple request as complex because it is worded formally, is long, or comes with enthusiasm. Size by risk and moving parts.
- **Lock-in.** Staying in Simple mode after a surprise because you already started answering. A surprise is the signal to slow down.
- **Uniform effort.** Applying the same scrutiny to every part. Spend it where an error is both likely and costly.
- **Skipping the overlay.** Missing that a short task is destructive or outward-facing. Scan every request for verbs like delete, overwrite, send, publish, pay, deploy, and migrate.
- **Ceremony.** Producing visible plans, headings, and checklists to look rigorous. Rigor shows in the correctness of the result.
