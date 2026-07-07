# Harness Engineering

![Agentic Engineering loop](../assets/agentic-engineering-loop.png)

Harness engineering is the practice of designing repositories, tools, feedback
loops, and constraints so coding agents can do reliable software engineering
work with less human intervention.

This brief is a high-fidelity public translation of OpenAI's article
["Harness engineering: leveraging Codex in an agent-first world"](https://openai.com/index/harness-engineering/)
([archived](https://web.archive.org/web/20260211225509/https://openai.com/index/harness-engineering/)),
written by Ryan Lopopolo and published February 11, 2026. Lopopolo's essays
translated in [Good Job Spec](good-job-spec.md) and
[Production Function Changed](production-function-changed.md) generalize
lessons from the same experiment. This brief preserves the article's operating model in
generic terms so future agents can inherit the same context without depending
on OpenAI's internal product, metrics, screenshots, or tooling names.

Terminology such as "harness engineering," "agent legibility," "golden
principles," and "garbage collection" is adopted from the source article.

Companion briefs:

- [Context Engineering](context-engineering.md) explains how to curate the
  model's finite working set while agents operate inside the harness.
- [Harness Sensors](harness-sensors.md) zooms in on the feedback side of the
  harness: sensors, computational checks, and agent self-correction.
- [Code as Conceptual Model](code-as-conceptual-model.md) explains why the
  codebase itself is part of the harness and context.
- [Good Job Spec](good-job-spec.md) explains why the harness needs written
  verification criteria, not only instructions and tools.
- [Production Function Changed](production-function-changed.md) explains the
  economic reason the harness should convert taste into executable checks.
- [Faster Was The Problem](faster-was-the-problem.md) adds the team-operating
  layer: adoption, maintenance, and ownership around the harness.

## Source Context

The article describes an experiment: a software product built under a hard
constraint of no manually written code. Agents generate product logic, tests, CI
configuration, documentation, observability, internal tooling, review comments,
and repository-management scripts.

The interesting lesson is not that agents can write code. The lesson is that the
human engineering role moves up a layer. Humans define intent, design the
environment, encode feedback, enforce boundaries, and improve the system that
agents use to work.

The article's central operating model:

- humans direct the work
- agents execute the work
- the repository becomes the durable context boundary
- missing context becomes repository content
- missing capability becomes tooling or skills
- repeated mistakes become checks
- human judgment becomes encoded taste, constraints, and feedback loops

Scale and tempo from the source article:

- five-month experiment, starting from an empty repository
- first commit in late August 2025
- post published February 11, 2026
- roughly one million lines of generated code
- roughly 1,500 pull requests
- small team starting at three engineers and growing to seven
- about 3.5 pull requests per engineer per day on average
- internal daily users and external alpha testers
- estimated build time around one tenth of manual implementation
- `AGENTS.md` kept around 100 lines and used as a map
- single agent runs often lasting six or more hours
- manual cleanup once consumed about one day per week before recurring cleanup
  agents replaced it

## Concept Fidelity Map

| Source concept | Preserved here as | Why it matters |
| --- | --- | --- |
| Zero manually written code | Human intent, agent execution | Forces investment in the harness rather than ad hoc human rescue. |
| Depth-first progress | Capability bootstrapping | Small agent-built blocks unlock larger agent tasks. |
| Failure as signal | "What capability is missing?" | Every failure points to missing context, tooling, guardrails, or validation. |
| Agent-to-agent review | Review loops | Review should be cheap enough to run repeatedly before human attention is spent. |
| Standard dev tools | CLI, scripts, forge tools, skills | Agents should gather context and act through normal project tools. |
| Per-worktree app runtime | Isolated validation environments | Multiple agent tasks can run, break, restart, and verify independently. |
| UI legibility | Browser automation and screenshots | Agents can reproduce visual bugs and prove fixes by driving the app. |
| Observability legibility | Logs, metrics, traces | Agents can reason from runtime signals, not just source files. |
| AGENTS.md as map | Short entrypoint, deep links | Context is scarce; agents need routing, not a giant manual. |
| Structured docs | Repo as system of record | Knowledge that is not local and discoverable effectively does not exist. |
| Agent legibility | Inspectable abstractions | Code should be easy for agents to model, navigate, validate, and change. |
| Boring technology bias | Predictable dependencies | Stable, composable, well-represented systems reduce agent guessing. |
| Architecture enforcement | Mechanical boundaries | Lints and structural tests preserve coherence under high throughput. |
| Parse at boundaries | Validate external shapes | Prevents syntactically valid code from building on guessed data. |
| Taste invariants | Custom rules and remediation | Human preferences become executable feedback. |
| Cheap corrections | Short PRs and fast repair loops | Agent throughput changes the cost model for review and merge. |
| Whole lifecycle generation | Code, tests, docs, CI, dashboards | Agent-generated means the repository system, not only product files. |
| End-to-end autonomy | Feature and bug-fix loop | Merge autonomy depends on encoded validation and recovery paths. |
| AI slop cleanup | Garbage collection | Agents copy existing patterns, so drift must be removed continuously. |
| Open questions | Unsettled long-term discipline | The field is early; the harness must evolve with models and practice. |

## Core Thesis

The unit of leverage is no longer only a better prompt. The unit of leverage is
a better harness.

The harness is the repository, documentation, tools, checks, skills, runtime
access, review loop, and cleanup system that lets coding agents do useful work
without constant human babysitting.

A strong harness changes the human job:

- from writing every line to specifying intent
- from manually checking every detail to designing validation
- from repeating review comments to encoding taste
- from explaining context in chat to versioning context in the repo
- from rescuing broken runs to improving the environment that caused them

## Empty Repository, Harness First

The source article starts from an empty git repository because that constraint
exposes the point clearly: without inherited human-written code, the system must
be shaped by agents and by the harness humans create around those agents.

The constraint was literal: humans did not directly contribute code. That forced
the team to improve the harness whenever the agent could not make progress,
rather than bypassing the system by hand.

The initial scaffold matters:

- repository structure
- package manager and app framework
- CI and formatting
- initial agent instructions
- validation commands
- documentation layout
- review and merge workflow

In an agentic repo, the scaffold is not setup trivia. It is the first layer of
the operating system that agents will keep extending.

## Redefining Engineering Work

In a human-first codebase, engineers usually spend most of their time producing
and editing source code directly.

In an agentic codebase, the bottleneck shifts toward:

- defining useful tasks
- exposing the right context
- creating reusable capabilities
- designing app and repo feedback loops
- enforcing architecture mechanically
- reviewing outcomes and encoding lessons
- deciding when human judgment is required

The practical loop is depth-first:

1. Break a goal into a smaller missing capability.
2. Have the agent build that capability.
3. Use it to unlock the next task.
4. Capture the lesson as docs, tools, checks, or skills.
5. Repeat until the environment can handle larger goals.

When an agent fails, the useful question is:

> What capability, context, guardrail, or feedback loop was missing?

The answer should usually become part of the repository. A one-off correction in
chat helps once. A checked-in doc, script, test, lint, skill, or workflow helps
future runs.

## Layered Harness Model

Birgitta Böckeler's article
["Harness engineering for coding agent users"](https://martinfowler.com/articles/harness-engineering.html)
(martinfowler.com, April 2, 2026) and Thoughtworks' podcast
["What is harness engineering?"](https://www.thoughtworks.com/en-us/insights/podcasts/technology-podcasts/what-harness-engineering)
frame the harness as concentric layers: the model at the core, the coding
agent's built-in builder harness around it, and an outer repo- and team-specific
user harness that teams build to make agents reliable enough for production
work.

That distinction is useful because "harness" can mean both the coding
assistant's built-in tool and prompt environment and the local system a team adds
around it: docs, checks, workflows, skills, runtime access, review loops, and
sensors. Harness engineering is the work of improving that outer layer, not
merely asking the model to behave better.

## Harness Components

This table is a README synthesis of the source article's operating model.

| Component | Role in the harness |
| --- | --- |
| `AGENTS.md` | Short map that tells agents where to start and where to look next. |
| Repository docs | Versioned source of truth for product, architecture, reliability, security, and design. |
| Execution plans | Durable task artifacts with progress, decisions, and acceptance criteria. |
| Skills | Reusable agent-callable workflows for repeated capabilities. |
| Tests and checks | Fast proof that behavior and constraints still hold. |
| Custom lints | Mechanical enforcement of architecture, naming, logging, file size, and taste rules. |
| Runtime tools | Browser, CLI, logs, metrics, traces, and app state exposed to the agent. |
| Review loops | Agent and human feedback converted into follow-up changes or durable rules. |
| Cleanup loops | Recurring scans that detect drift and open small repair changes. |

## Application Legibility

Agents need to inspect the running system, not only the source tree.

Application legibility means the app can be launched, driven, observed, changed,
and re-checked by an agent inside the task loop.

Useful runtime capabilities:

- boot one isolated app instance per worktree
- navigate the UI with browser automation
- capture before-and-after screenshots
- inspect DOM snapshots and console output
- query logs, metrics, and traces
- replay user journeys
- reproduce a bug from a report
- restart services after a patch
- prove a fix with screenshots, videos, logs, or traces

This turns vague goals into measurable work. "Make startup faster" becomes
"prove startup completes under 800ms." "Improve this journey" becomes "show that
no span in the critical journey exceeds the budget." "Fix this flow" becomes
"drive the flow, capture the failure, patch it, and drive it again."

Per-worktree app instances are especially important. They let multiple agents
work independently without sharing a fragile local runtime. Each task can own
its app, data, logs, metrics, and teardown.

The source pattern is stronger than a shared local dev stack: each worktree gets
an isolated app plus ephemeral logs, metrics, and traces, and that observability
state is torn down when the task is done.

## Repository Knowledge As System Of Record

Context is scarce. Agents need a map, not a giant instruction manual.

The pattern:

- keep `AGENTS.md` short
- use it as a table of contents
- link to deeper docs
- version the docs in the repo
- make docs structured enough to lint
- keep active plans, completed plans, and known debt visible

Recommended shape:

```text
AGENTS.md
ARCHITECTURE.md
docs/
  design/
    index.md
    core-beliefs.md
  plans/
    active/
    completed/
    tech-debt.md
  generated/
    db-schema.md
  product/
    index.md
  references/
    llms.txt
    api-contracts.md
  DESIGN.md
  FRONTEND.md
  PLANS.md
  PRODUCT_SENSE.md
  QUALITY_SCORE.md
  RELIABILITY.md
  SECURITY.md
```

The important part is not the exact file names. The important part is
progressive disclosure: agents start from a small stable entrypoint and learn
where to look next.

Repository knowledge should include:

- architecture maps
- domain ownership
- product principles
- design system references
- reliability expectations
- security constraints
- generated schemas
- execution plans
- quality scorecards that grade product domains and architectural layers
- technical debt
- stale-doc cleanup signals

Mechanically check the knowledge base where possible:

- required docs exist
- links resolve
- ownership is clear
- active plans have status
- generated docs are fresh
- stale docs are flagged
- important docs are reachable from entrypoints

The source article names a recurring "doc-gardening" pattern: an agent scans for
stale or obsolete documentation and opens small fix-up pull requests.

## Agent Legibility

Human-readable code is not always agent-legible code.

Agent legibility means an agent can answer:

- what domain am I in?
- what layer owns this behavior?
- what files are authoritative?
- what command proves this works?
- what constraints must not be violated?
- what pattern should I follow?
- where should new knowledge be recorded?

From the agent's perspective, inaccessible context does not exist. Chat threads,
external docs, old decisions, and tacit human knowledge only become useful when
they are encoded in a discoverable repository artifact.

Agent-legible systems tend to favor:

- stable names
- boring abstractions
- typed interfaces
- explicit schemas
- searchable docs
- small files
- predictable commands
- local examples
- structured errors
- visible tests

Opaque dependencies can be a problem when agents repeatedly misunderstand them.
Sometimes the fix is better docs. Sometimes it is a thin local wrapper. In rare
cases, a small inspectable implementation with complete tests may be more useful
than a general dependency whose behavior cannot be reasoned about from the repo.

The source article gives a concrete example: replacing a generic concurrency
helper with a local implementation that matched the runtime's tracing and test
coverage needs. The point is not "rewrite every dependency." The point is that
agent legibility can outweigh generic reuse when behavior must be inspectable.

## Enforcing Architecture And Taste

Documentation alone does not preserve coherence at agent speed.

Agentic repositories need mechanical boundaries:

- validated dependency direction
- explicit ownership by domain or layer
- parsing data at external boundaries
- typed or schema-validated APIs
- restricted cross-cutting access
- structured logging rules
- naming conventions
- file size limits
- platform reliability rules
- CI checks with remediation guidance

One illustrative layer model:

```text
Types -> Config -> Repo -> Service -> Runtime -> UI
```

Here `Repo` means the data-access layer. Cross-cutting concerns such as auth,
connectors, telemetry, and feature flags should enter through a named single
interface, called `Providers` in the source article. The exact architecture will
differ by repo, but the rule should be mechanically enforceable.

This is the platform-style tradeoff: enforce boundaries centrally and allow
autonomy locally. The harness controls invariants; agents retain freedom inside
those boundaries.

Good checks should tell the agent:

- what rule was violated
- why the rule exists
- what pattern to use instead
- where the source-of-truth doc lives

Error messages are part of the harness. A check that fails with remediation
instructions injects useful context into the next agent run.

## Throughput And Merge Philosophy

Agent throughput changes the cost model.

When agents can produce, review, and repair work quickly, human attention
becomes the scarce resource. Corrections become cheap; waiting for perfect
first-pass work becomes expensive.

This favors:

- short-lived pull requests
- fast local validation
- agent review before human review
- small repair passes for concrete findings
- follow-up fixes for low-risk flakes
- encoding repeated review comments as docs, tests, or lint rules
- minimal blocking gates backed by strong recovery paths

This is not an excuse for weak validation. Higher throughput without stronger
checks just creates faster entropy.

## Agent-To-Agent Review

Review is part of the harness.

A useful loop:

1. An agent implements a change.
2. The agent reviews its own work locally.
3. Another agent reviews the diff.
4. Cloud or CI review adds another pass.
5. The implementing agent retrieves findings.
6. It repairs concrete issues.
7. Repeated feedback becomes docs, tests, or checks.

The source article refers to this pattern as a Ralph Wiggum Loop: iterate
through self-review, agent review, and repair until the reviewers are satisfied.
The term originates with Geoffrey Huntley's
["Ralph Wiggum as a software engineer"](https://ghuntley.com/ralph/) technique:
run an agent in a loop with fresh context each iteration, accumulating progress
in files and git history rather than in the context window.

Human review still matters for intent, taste, priority, and risk. The goal is to
reserve human attention for judgment while agents handle routine correctness
feedback cheaply and repeatedly.

## What Agent-Generated Means

Agent-generated does not only mean product code.

Agents can generate and maintain:

- application code
- tests
- CI and release configuration
- documentation
- design history
- internal developer tools
- evaluation harnesses
- review comments and responses
- scripts that manage the repository
- dashboards and observability definitions
- cleanup and refactoring changes

The human role moves up a layer: prioritize work, translate feedback into
acceptance criteria, validate outcomes, and improve the harness when the system
struggles.

## Increasing Autonomy

Autonomy is earned by encoding the loop. In the source article, the meaningful
threshold is an agent driving a feature or bug fix end to end:

1. validate the current state of the codebase
2. reproduce a reported bug
3. record proof of the failure
4. implement a fix
5. validate the fix by driving the application
6. record proof of the resolution
7. open a pull request
8. respond to agent and human feedback
9. detect and repair build failures
10. escalate to a human only when judgment is required
11. merge the change

This should not be assumed to generalize across repositories. Autonomy depends
on local structure, tooling, validation quality, and recovery paths.

## Entropy And Garbage Collection

Agents copy what already exists. If the repo contains uneven patterns, stale
docs, weak tests, or guessed data shapes, those patterns will spread.

Manual cleanup does not scale with agent throughput. Cleanup has to become a
recurring system function.

Useful cleanup loops:

- scan for stale documentation
- verify docs are cross-linked from entrypoints
- identify repeated review comments
- update quality scores by domain or layer
- replace duplicated helpers with shared utilities
- promote repeated mistakes into lint rules
- remove obsolete plans and dead references
- open small repair PRs continuously

Golden principles are short, opinionated rules that capture human taste in
enforceable form. Examples:

- prefer shared utilities over repeated one-off helpers
- validate external data at boundaries
- avoid YOLO-style probing or building on guessed data shapes
- centralize invariants
- make reliability requirements mechanical
- turn repeated review comments into checks

This functions like garbage collection. Debt is cheaper to remove continuously
than in large painful bursts. Human taste is captured once, then enforced on
future work.

The source article's cadence is intentionally small: background cleanup tasks
scan for deviations, update quality grades, and open targeted refactoring pull
requests that can often be reviewed quickly or automerged.

## What Is Still Open

This style of software engineering is early.

Open questions:

- how architectural coherence holds up over years
- where human judgment adds the most leverage
- how much judgment can be encoded into docs, tools, and checks
- how harnesses should evolve as models improve

The direction is clear even if the endpoint is not: software engineering still
requires discipline, but more of that discipline moves into scaffolding,
environment design, and feedback systems.

## Minimal Public Harness

For a public repository, the smallest useful version looks like this:

```text
AGENTS.md
ARCHITECTURE.md
docs/
  QUALITY.md
  RELIABILITY.md
  SECURITY.md
  plans/
    active/
    completed/
scripts/
  check
  lint-architecture
  test
```

Start with:

1. a short `AGENTS.md`
2. one architecture map
3. one quality scorecard
4. one reliable validation command
5. one place to put active plans
6. one cleanup checklist

Then grow the harness only when a real failure proves what is missing.

## Example `AGENTS.md`

```md
# Agent Instructions

Start here, then follow links to the narrow source of truth.

## Before Editing

- Read `ARCHITECTURE.md` for ownership and dependency direction.
- Read the nearest domain doc under `docs/`.
- Check existing tests and commands before inventing new ones.

## Validation

- Run `scripts/check` before handoff.
- If a check fails, fix the root cause or document the blocker.

## Plans

- Use `docs/plans/active/` for multi-step work.
- Move completed plans to `docs/plans/completed/`.

## Architecture

- Do not cross layer boundaries unless `ARCHITECTURE.md` allows it.
- Add new shared behavior to the documented shared location.
- Prefer explicit schemas at external boundaries.
```

The better the harness, the less the human has to babysit individual changes.
The engineer's attention moves toward intent, taste, judgment, and the systems
that let those things compound. The repo-level
[mental model](../README.md#mental-model) lives in the README.
