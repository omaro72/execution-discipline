# Execution Discipline

**A frontier model's working method, written down so any model can follow it.**

Execution Discipline is an Agent Skill that gives an AI model a disciplined way to carry out a task: understand what is really being asked, plan in proportion to the risk, do all of the work, check the result against reality, and report truthfully what was and was not done.

Its methodology comes from **Claude Fable 5.2**. The model was asked to examine how it approaches work — how it reads a request, plans, decides, uses tools, recovers from errors, and reviews its own results — and to turn that into explicit practice that other models can apply. Execution Discipline is the result: the method, not the model.

> **Independent project.** Execution Discipline is a community project. It is not made, endorsed, or sponsored by Anthropic. It contains written instructions only: no model weights, no system prompts, and no proprietary Anthropic material. "Claude" and "Claude Fable" are product names of Anthropic, PBC, used here solely to describe where the methodology came from.

## Why it exists

Capable models rarely fail because they lack knowledge. They fail in quieter ways: answering a slightly different question from the one asked, dropping a constraint buried in the middle of a paragraph, building on something the user assumed, reporting "done" for work they never saw succeed, or wrapping a one-line answer in a page of process.

These are failures of method, and method can be written down. Execution Discipline does not make a model more intelligent. It gives the model a way of working that makes better use of the intelligence it already has.

## What it brings to your work

**Understanding before action.** The model states the real objective, lists every requirement and constraint, and reads the material it was given before forming a view. It treats your diagnosis as a hypothesis and your goal as the requirement.

**Planning that fits the task.** Simple requests get direct answers. Complex ones get a written requirement list, a staged plan, and checkpoints. Anything hard to undo gets extra care, whatever its size.

**Work that gets finished.** Requirements are tracked to a final status. Nothing is quietly dropped, and a plan or a partial result is never presented as the deliverable.

**Self-review grounded in evidence.** Before delivering, the model re-reads the original request, checks each requirement against the result, and verifies by observation: running, opening, recomputing, or comparing with the source.

**Honest reporting.** A small, fixed vocabulary separates what was verified from what was assumed and what was not done, so you always know what you can rely on.

**Sound judgment at the forks.** Six explicit rules cover the decisions that cause most avoidable damage: when to ask and when to proceed, when to verify, when to stop retrying, when to confirm before acting, when the work is finished, and what to do when your proposed approach will not reach your goal.

**No ceremony.** The method runs in the background. The model is told to show you the result, not a narration of its process, and to treat overhead on a simple task as a failure.

## How it works

| Element | What it is |
|---|---|
| **Three anchors** | The request, reality, and the reader. Most failures are a loss of contact with one of them; when unsure, the model re-anchors. |
| **Four modes** | *Simple*, *Moderate*, and *Complex* scale the effort to the number of moving parts. *High-impact* is a separate overlay for anything costly or irreversible, so a one-line delete command gets care that its size alone would not earn. |
| **Six phases** | Understand, Plan, Decompose, Execute, Review, Deliver. In Simple mode they collapse into moments. |
| **Six decision rules** | Ask or proceed. Trust or verify. Retry or rethink. Act or confirm. Stop or continue. Their way or a better way. |
| **A final checklist** | A short, silent pass before anything is delivered. |

The approach is qualitative throughout. The skill contains no scores, targets, or performance measurements; it relies on reasoning, planning, adaptation, and self-review.

## See the difference

These illustrations come from the skill's own example library. They show the behavior the method asks for; they are not recorded transcripts.

**"The login test is failing — fix it."**
Without a method: edits the assertion until the test passes and reports "fixed".
With Execution Discipline: reads the failure, fixes the cause in the code, runs the suite, and reports what it saw. If it cannot run the suite, it says "fix applied, tests not run here".

**"Our users table has no index on email, so add one."** (the schema already has one)
Without a method: adds a duplicate index and reports success.
With Execution Discipline: points out that the index already exists, identifies why the query is still slow, and proposes the fix that addresses it.

**"Clean up the old branches in this repo."**
Without a method: deletes everything except the main branch, including unmerged work.
With Execution Discipline: lists the branches, separates merged from unmerged, and confirms before deleting anything.

More pairs, across software, data, research, writing, business, and everyday tasks, are in [`references/examples.md`](skills/execution-discipline/references/examples.md).

## Compatibility

Execution Discipline is plain Markdown in the open Agent Skills format. It has no scripts, no dependencies, and no network access of its own.

| Environment | How it is used | Status |
|---|---|---|
| Claude Code | Plugin, or a folder in `~/.claude/skills/` or `.claude/skills/` | Installation from this repository and invocation verified |
| claude.ai and Claude Desktop | ZIP upload under Customize > Skills | Package built to the documented format; upload not performed by the authors |
| Claude API | Uploaded through the Skills API | Follows the published guide; not executed by the authors |
| Other models and tools | Paste the body of `SKILL.md` into the system prompt | Possible by design; not tested |

It is intended for the Claude model family (Opus, Sonnet, Haiku) and for any other model that can follow written instructions. See [Scope and limitations](#scope-and-limitations) for what has and has not been confirmed.

## Installation

### Claude Code, as a plugin

```bash
claude plugin marketplace add omaro72/execution-discipline
claude plugin install execution-discipline@execution-discipline
```

Inside a session, the equivalents are `/plugin marketplace add omaro72/execution-discipline` and `/plugin install execution-discipline@execution-discipline`.

### Claude Code, by copying the folder

Clone or download the repository, then copy the skill folder.

```bash
# For yourself, in every project
cp -r skills/execution-discipline ~/.claude/skills/

# For one project, shared with everyone who works in it
mkdir -p .claude/skills && cp -r skills/execution-discipline .claude/skills/
```

```powershell
# Windows PowerShell, for yourself
Copy-Item -Recurse skills\execution-discipline "$env:USERPROFILE\.claude\skills\"
```

To try it without installing anything, start Claude Code with `claude --plugin-dir /path/to/execution-discipline`.

### claude.ai and Claude Desktop

1. Download `execution-discipline.zip` from the [latest release](https://github.com/omaro72/execution-discipline/releases/latest).
2. Open **Customize > Skills**, upload the ZIP, and turn the skill on.

Use the release file. GitHub's green "Download ZIP" button packages the whole repository, which will not upload as a skill.

### Claude API

Upload the skill folder once, then attach it to requests. This snippet follows Anthropic's [Skills guide](https://platform.claude.com/docs/en/build-with-claude/skills-guide) as published when this project was written. It has not been executed by the authors, so confirm the details against the guide.

```python
import anthropic
from anthropic.lib import files_from_dir

client = anthropic.Anthropic()
skill = client.skills.create(files=files_from_dir("skills/execution-discipline"))

response = client.messages.create(
    model="claude-opus-5-5",
    max_tokens=4096,
    container={"skills": [{"type": "custom", "skill_id": skill.id, "version": "latest"}]},
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[{"role": "user", "content": "Your task here"}],
)
```

### Other models and tools

For a model or product without skill support, paste the body of [`SKILL.md`](skills/execution-discipline/SKILL.md) (everything below the frontmatter) into the system prompt. The reference files are optional additions for when context allows.

## Activation and usage

A skill loads when the model judges that a task matches its description. You can leave that to the model or take control of it.

**Automatic.** Ask for the work as you normally would. The skill's description tells the model to load it at the start of any task that involves doing work rather than answering a quick question. Models do skip skills for requests that look easy, so automatic loading is common but not guaranteed.

**On request.** In Claude Code, begin the message with the command:

```text
/execution-discipline migrate the report templates to the new branding
```

When installed as a plugin, `/execution-discipline:execution-discipline` also works. Anywhere else, say "use the execution-discipline skill for this".

**Always on.** Add one line to the instructions the model always sees: `CLAUDE.md` in Claude Code, project instructions or personal preferences in claude.ai, or the system prompt in the API.

```text
For any task that is more than a quick factual question, load the execution-discipline skill before starting and follow it.
```

### Where it helps most

| Domain | Example request | What the method contributes |
|---|---|---|
| Software | "The export job crashes on large files, fix it" | Reproduce first, fix the cause instead of silencing the error, run the checks, report what was and was not run |
| Data | "What was average order value last quarter?" | Inspect the data before computing, state the definition and exclusions, reconcile the total |
| Research | "Is there good evidence for this? Give sources" | Cite only what was actually opened, separate established from contested, report disagreements |
| Writing | "Tighten this, keep both examples, stay under the limit" | Extract every constraint and check each one literally |
| Business | "Should we switch to annual billing? Data attached" | Use the attached data, commit to a recommendation, state what it depends on |
| Everyday | "Plan a weekend trip for two within our budget" | Meet each stated constraint visibly, make the sums add up, label estimates as estimates |
| Operations | "Clean up the old branches" | List what would be affected, separate safe from risky, confirm before deleting |

## What is inside

```text
execution-discipline/
├── .claude-plugin/                 Manifests that let Claude Code install from this repository
├── skills/
│   └── execution-discipline/       The skill. This folder is the whole installable unit.
│       ├── SKILL.md                Anchors, modes, work loop, decision rules, checklist
│       └── references/
│           ├── modes.md                 Full procedure for each mode, with templates
│           ├── operating-principles.md  Nine disciplines for long or tool-heavy work
│           ├── failure-modes.md         Sixteen common failures, each with prevention and a catch
│           ├── examples.md              Weak-versus-strong pairs across domains
│           └── domain-guide.md          What to pin down and what counts as evidence, by domain
├── README.md
└── LICENSE
```

`SKILL.md` is deliberately compact so that it stays within a model's attention and survives context compaction in long sessions. The reference files load only when a task calls for them.

## Scope and limitations

- **It is a method, not a model.** It does not add knowledge or reasoning ability. A model that cannot solve a problem will not solve it because of this skill, though it may report more accurately that it did not.
- **It is not Claude Fable 5.2.** It does not reproduce that model's capabilities, and results depend on the model that runs it.
- **No performance claims are made.** In early trials on short tasks with one Claude model, results with and without the skill were similar, because the model already handled those tasks well. The benefits described above are what the method is designed to produce, not measured outcomes.
- **Activation is not guaranteed** unless you invoke it explicitly or use the always-on line. In spot checks the model loaded the skill on its own for some requests and not for others.
- **Instructions are followed imperfectly,** and less consistently by smaller models. The skill makes the behaviors it describes more likely, not certain.
- **It uses context.** Loading the skill occupies part of the model's context window, and each reference file adds more.
- **It is not a safety system.** High-impact mode encourages care with consequences. It does not replace platform policies, permission controls, or your own review of destructive actions.
- **Your instructions take precedence.** If your system prompt or project instructions ask for a different way of working, the model should follow those.

**What has been checked:** the manifests pass Claude Code's plugin validator; the plugin installs from this repository; the release archive installs into a fresh project; and the skill loads on command.

**What has not been checked:** Claude Sonnet and Opus, models from other providers, long or tool-heavy sessions, upload to claude.ai or Claude Desktop, the Skills API, the always-on line, and languages other than English. Treat these as unknown rather than as expected to work.

## Security and privacy

The repository contains only Markdown files, two JSON manifests, and a license. The skill runs no code, makes no network requests, collects no data, and has no dependencies.

A skill's instructions do influence how your model behaves, so read [`SKILL.md`](skills/execution-discipline/SKILL.md) before installing it, as you should for any skill. If you install from a fork, compare it with this repository first.

To report something that looks unsafe, misleading, or private, open an issue. Do not include secrets or personal data in a public issue.

## Origin and attribution

The methodology was written by Claude Fable 5.2, Anthropic's AI model, in response to a request to articulate its own working practices in a form other models could follow. The project is assembled and published independently.

Execution Discipline is an original written work. It is not an Anthropic product, does not speak for Anthropic, and does not contain or reveal any confidential material. All product names belong to their respective owners.

## Feedback

Reports of observed behavior are the most useful contribution. Open an issue with the request you made, what the model did, and what it should have done.

## License

Released under the [MIT License](LICENSE). The skill's text was written by an AI model, and how copyright applies to such text varies by jurisdiction.
