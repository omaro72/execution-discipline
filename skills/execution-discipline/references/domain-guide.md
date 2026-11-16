# Domain guide

How the method applies in six kinds of work. For each: what to pin down first, what counts as evidence, the usual traps, and what "done" means. The workflow in SKILL.md is the same everywhere; what changes is what you must look at and how you check.

## Contents

- Software and technical work
- Data and analysis
- Research and fact-finding
- Writing and editing
- Business and planning
- Everyday tasks and advice
- When you have no tools

## Software and technical work

**Pin down.** The behavior wanted, not just the change requested. The language, versions, and environment. The project's existing conventions. What must keep working.

**Evidence.** The code ran. The tests ran and you saw the result. The command produced the expected output. You read the file you are describing. For a bug: you reproduced it before the fix and could not reproduce it after.

**Traps.**
- Editing code you have not read, or files adjacent to the task.
- Inventing a function, flag, or parameter that sounds right. Check the source or the documentation.
- Making a failing test pass by changing the test, or silencing an error instead of fixing its cause.
- Fixing the reported symptom and not checking the same mistake elsewhere.
- Reporting "tests pass" when they were not run, or when only one was run.
- Leaving debug output, commented-out code, or temporary files behind.

**Done means.** The requested behavior is demonstrated, existing checks still pass, the change is limited to what the task needs, and the report says what was run and what was not.

## Data and analysis

**Pin down.** The exact question and the definition of each metric (which rows count, which period, which currency or unit). What decision the number feeds.

**Evidence.** You looked at the data before computing: row counts, column types, ranges, missing values, duplicates, units. The computation was executed, not estimated. Totals reconcile with a second method or a known figure. A sample of rows was checked by hand.

**Traps.**
- Computing on raw data without inspecting it: duplicates, test records, refunds, mixed units, inconsistent date formats.
- Silent choices about filtering or definitions that change the answer.
- Mental arithmetic on more than a few numbers. Compute it, or recompute by a second route.
- Reporting more precision than the data supports.
- Treating correlation as cause, or a small sample as a trend.

**Done means.** The answer comes with its definition, the filters and exclusions applied, the row counts involved, and the caveats that would change the reading.

## Research and fact-finding

**Pin down.** The precise question, the time frame, how current the answer must be, and how reliable it must be for the use it will be put to.

**Evidence.** You opened the source and it says what you report. Primary sources over summaries; several independent sources for anything contested. Dates noted for time-sensitive facts.

**Traps.**
- Citations, quotes, statistics, or links produced from memory. Cite only what you actually opened; otherwise label it as recall.
- Treating a search-result snippet as the content of the page.
- Blending sources that disagree into one confident statement. Report the disagreement and who says what.
- Presenting outdated information as current. Say what your information is as of.
- Stopping at the first source that agrees with the expected answer.

**Done means.** The question is answered directly; each key claim is tied to a source you read or marked as unverified; disagreements and gaps are stated; established facts are separated from inference.

## Writing and editing

**Pin down.** Audience, purpose, and the one thing the reader should do or know afterward. Hard constraints: length, format, tone, required and forbidden content. For edits: what must be preserved.

**Evidence.** You counted the words or characters against the limit. Each required element can be pointed to. Facts, names, dates, and figures match the source material. For edits: a comparison shows only intended changes.

**Traps.**
- Exceeding a length limit, or approximating it instead of counting.
- Dropping a required element while improving the prose.
- Rewriting what you were asked to proofread; changing the author's voice or meaning.
- Generic filler that could appear in anyone's document.
- Formatting the output in a way the destination cannot use (markdown in a plain-text email).
- Inventing facts, quotes, or figures to make the text complete. Use a clearly marked placeholder and flag it.

**Done means.** The text is ready to use as it stands, meets every stated constraint when checked literally, and any placeholder or assumption is called out in one line.

## Business and planning

**Pin down.** The decision to be made, who makes it, the criteria that matter, and the constraints (budget, deadline, people, policy). What the user already knows, so you do not explain it back.

**Evidence.** Figures come from the user's material or a cited source, and the arithmetic was done, not estimated. Each recommendation traces to a stated criterion. Key assumptions are listed with how sensitive the conclusion is to them.

**Traps.**
- Balanced lists of considerations with no recommendation. If asked what to do, say what to do.
- Ignoring the attached data in favor of general knowledge.
- Plans with no owners, dates, or costs, or that silently break a stated constraint.
- Hidden assumptions about market size, growth, or cost.
- Inconsistent numbers between a summary and its supporting table.

**Done means.** A clear recommendation or plan, grounded in their specifics, with the reasoning, the assumptions, the main risk, and what would change the answer.

## Everyday tasks and advice

**Pin down.** The person's actual situation and constraints: budget, time, location, preferences, restrictions, skill level. What they will do with the answer next.

**Evidence.** Every stated constraint is met when checked item by item. Sums add up. Steps are in an order that works. Anything time-sensitive or location-specific (prices, opening hours, availability, regulations) is either looked up or labeled as an estimate to confirm.

**Traps.**
- A generic list when the person asked for a plan fitted to them.
- Quietly ignoring one constraint (the budget, the allergy, the time limit).
- Stating prices, schedules, or rules from memory as if current.
- Over-explaining a simple request or wrapping it in unnecessary warnings.
- For health, legal, financial, or safety questions: either refusing to engage or sounding more certain than the information supports. Give the useful answer, state its limits, and say when a professional should decide.

**Done means.** The person can act on the answer as given, each of their constraints is visibly respected, and uncertain details are marked so they know what to confirm.

## When you have no tools

Without the ability to run, search, or open files, verification changes form but does not disappear.

- Recompute by a second route. Re-derive the result differently and compare.
- Trace by hand. Walk the code or the logic with a concrete input, including an edge case. Read every line you rely on; a function's name or a test's title tells you the intent, not the behavior.
- Check constraints literally. Count, compare, and scan for the forbidden item.
- Separate the kinds of statement. Mark what is recall, what is inference, and what the user should confirm.
- Hand over the check. Give the exact command, query, or source the user can use to verify, and say that you did not run it.

What does not change: do not claim a result you did not observe, and do not invent specifics to make an answer look complete.
