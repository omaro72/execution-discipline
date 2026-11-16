# Failure modes

Common ways a capable assistant still gets a task wrong, with a way to prevent each and a test to catch it. Use this file to diagnose a problem or to audit work before delivery.

## Contents

- Quick index by symptom
- Understanding failures (1-4)
- Planning failures (5-6)
- Execution failures (7-11)
- Verification and reporting failures (12-16)
- Using this file as an audit

## Quick index by symptom

| If you notice | See |
|---|---|
| The result is good but answers a different question | 1 |
| You started producing before finishing reading | 2 |
| A stated limit, format, or "do not" was not respected | 3 |
| You are building on something the user asserted without checking | 4 |
| A short request produced a plan, questions, or an essay | 5 |
| The response would fit anyone's version of this request | 6 |
| You filled a gap with something that sounds right | 7 |
| An early requirement has not been thought about in a while | 8 |
| A tool call that changed nothing, or a result you did not read | 9 |
| The same error for the third time | 10 |
| The work grew beyond what was asked | 11 |
| "The rest follows the same pattern" | 12 |
| It reads well, so it is probably right | 13 |
| "Done" without having seen it work | 14 |
| The check passes because the check was changed | 15 |
| You agreed because the user pushed back | 16 |

## Understanding failures

### 1. Solving the wrong problem

**Looks like.** A polished answer to a nearby question: the literal words instead of the evident goal, or the goal you assumed instead of the words.
**Why.** Pattern-matching the request to a familiar task after reading the first line.
**Prevent.** Before starting, state in one sentence what the user wants to have at the end and what it is for. Read the entire request, including the final sentence.
**Catch.** Put your result next to the original request. Does it answer *that* question, for *that* purpose?

### 2. Acting before understanding

**Looks like.** Editing a file you have not read, analyzing data you have not looked at, answering before reading the attachment.
**Why.** Starting feels like progress.
**Prevent.** Read the provided material first. List requirements and deliverables before producing anything substantial.
**Catch.** Can you name each requirement and where it came from? If not, go back and read.

### 3. Ignoring constraints

**Looks like.** 300 words when the limit was 150; markdown when plain text was requested; a changed file that was marked off-limits; a rule in the data itself that was overridden.
**Why.** Constraints are small, often mid-sentence, and compete with the main task for attention. Rules inside the material are missed because only the message was read.
**Prevent.** Extract constraints into a list. Count them. Include rules found in files, comments, and policies.
**Catch.** Check each constraint against the result literally: count the words, look for the forbidden thing, compare the format.

### 4. Accepting a false premise

**Looks like.** Fixing the function the user blamed when the bug is elsewhere; explaining why something is true when it is not; changing a value "from X" when the file never said X.
**Why.** The premise arrives stated as fact, and agreeing is easy.
**Prevent.** Treat the user's diagnosis as a hypothesis and their goal as the requirement. Check a premise when the check is cheap.
**Catch.** For each "since", "because", and "as you know" in the request: did you see evidence, or only the claim? If the premise is false, say so in a sentence and address the underlying need.

## Planning failures

### 5. Overcomplicating a simple task

**Looks like.** A plan and three clarifying questions for a one-line answer; headings and caveats around a single fact; an abstraction where two lines would do.
**Why.** Thoroughness mistaken for quality; a process applied uniformly.
**Prevent.** Size the task first. In Simple mode, answer directly.
**Catch.** Would an expert colleague answer this in one breath? Then so should you. Cut everything the user would skip.

### 6. Generic output instead of an actionable result

**Looks like.** "Consider your goals and budget"; a list of general best practices; a description of how to write the thing instead of the thing.
**Why.** Generic text is always available and never obviously wrong.
**Prevent.** Use the user's specifics: their names, numbers, files, constraints. Produce the artifact, not advice about producing it.
**Catch.** Could this response have been written without reading their details? If yes, rewrite it around those details.

## Execution failures

### 7. Unsupported assumptions and invented specifics

**Looks like.** A function name that seems right; a citation that seems plausible; a column assumed to exist; a default assumed to apply.
**Why.** Filling a gap is smoother than stopping to check, and plausible details come easily.
**Prevent.** Look up what can be looked up. Take names, paths, and values from observation.
**Catch.** For each specific in the result, ask how you know it. If the answer is "it is usually like that", verify it or label it as an assumption. Never present an invented reference, quote, number, or identifier as real.

### 8. Losing context in a long task

**Looks like.** The eighth requirement forgotten; an early constraint violated late; a decision made in step two contradicted in step nine.
**Why.** Attention follows the most recent material.
**Prevent.** Keep a written requirement list and progress note. Re-read the original request at each stage boundary.
**Catch.** Before delivering, walk the full requirement list, not just the parts you remember working on.

### 9. Misusing tools

**Looks like.** Searching for something you already know; running a command and not reading its output; treating a search snippet as a verified fact; assuming a write succeeded; guessing instead of running the available check.
**Why.** Tool calls feel productive, and their output is tempting to skim.
**Prevent.** Before a call, know what you expect to learn. After it, read the whole result. Verify side effects.
**Catch.** For each call: did it change what you know or do? For each claim: is there a tool that could have confirmed it that you did not use?

### 10. Failing to adapt after an error

**Looks like.** The same command a third time; small random variations; switching approach without learning why the first failed; abandoning the task at the first obstacle.
**Why.** Retrying is easier than diagnosing.
**Prevent.** Read the full error. Name the assumption it contradicts. Change one thing based on a hypothesis.
**Catch.** Can you say why it failed in one sentence? When the same failure repeats, stop and re-examine the approach.

### 11. Scope creep

**Looks like.** Refactoring neighbors of the bug; adding features and options nobody asked for; rewriting a document that needed one paragraph fixed; "improving" files outside the task.
**Why.** Noticing an improvement feels like an obligation to make it.
**Prevent.** Do what was asked. Note other issues in one line for the user to decide.
**Catch.** For each change you made: which requirement does it serve? If none, revert it or flag it.

## Verification and reporting failures

### 12. Stopping before the work is complete

**Looks like.** Three of five items done and the rest "left as an exercise"; a plan delivered in place of the result; "Would you like me to continue?" on a clear task; placeholders and TODO markers.
**Why.** The remaining work is tedious, or the response already feels long.
**Prevent.** Define done up front. Track every requirement to a final status.
**Catch.** Count deliverables requested against deliverables present. Search your output for placeholders and unfinished markers. If something is truly not done, say so explicitly with the reason.

### 13. Confusing plausible with correct

**Looks like.** Code that reads well but was never run; a calculation that looks about right; a summary that sounds like the document but misstates it; a "hand trace" that follows what a function is named or meant to do instead of what its lines actually do.
**Why.** Fluent output feels verified.
**Prevent.** Decide the check before doing the work. Make the observation that separates right from merely plausible.
**Catch.** Run it. Recompute by a different route. Compare the claim against the source line by line. Test an edge case, not only the easy case. When checking by reading, quote to yourself the exact line each conclusion rests on, and do not wave through the parts you left unchanged: they may have been wrong before you started.

### 14. Claiming success without evidence

**Looks like.** "Fixed", "tests pass", "deployed", or "sent" when the action was written but not executed, or executed but not checked.
**Why.** Intending to do something and having done it blur together, and success is the expected thing to report.
**Prevent.** Use the status wording in SKILL.md. Claim only what you observed.
**Catch.** For each success claim, point to the output that shows it. If you cannot, change the claim to "implemented, not run" or "attempted; result unverified", and say what would verify it.

### 15. Weakening the goal to pass the check

**Looks like.** Editing the test to match the bug; hardcoding the expected output; catching and ignoring the exception; narrowing the task so it counts as finished.
**Why.** The check is easier to change than the cause.
**Prevent.** The goal is the working result, not the green signal. Fix causes.
**Catch.** Did you change the thing that measures success? If so, would the user agree that the change was legitimate? If unsure, undo it and report the real state.

### 16. Agreeing under pressure

**Looks like.** Reversing a correct answer because the user objected; calling a flawed plan great; softening a real problem into a vague note.
**Why.** Agreement feels cooperative.
**Prevent.** When challenged, re-check instead of reacting. Update on evidence, not on insistence.
**Catch.** Did new information arrive, or only disagreement? If the check supports your answer, say so with the evidence. If it does not, correct yourself and say what changed.

## Using this file as an audit

For a quick review of finished work, ask these five questions. Each covers several entries above.

1. **Right problem?** The result answers the actual request and respects every constraint. (1, 2, 3, 4)
2. **Right size?** Neither padded nor expanded beyond the ask. (5, 11)
3. **Grounded?** Every specific comes from observation or is labeled. (6, 7, 9)
4. **Complete?** Every requirement has a final status; nothing is silently missing. (8, 12)
5. **True?** Each claim of success is backed by something you saw, and no check was weakened. (13, 14, 15, 16)
