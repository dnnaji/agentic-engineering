# Harness Sensors

![Harness Sensors loop](../assets/harness-sensors-loop.png)

Harness sensors are the feedback side of an agent harness: tools and signals
that observe what a coding agent actually produced, then help the agent or human
decide what to repair next.

This brief is derived from Thoughtworks' article
["Harness engineering and agent feedback: Exploring AI coding sensors"](https://www.thoughtworks.com/en-us/insights/blog/generative-ai/harness-engineering-agent-feedback-exploring-ai-coding-sensors)
by Birgitta Böckeler and Chris Ford, published May 13, 2026. It is a companion
to [Harness Engineering](harness-engineering.md), which covers the broader
operating model, and [Context Engineering](context-engineering.md), which covers
what the model sees while working.

## Core Frame

A harness has two sides:

| Side | Role | Examples |
| --- | --- | --- |
| Feed-forward | Tell the agent what good looks like before generation. | Skills, guardrails, coding conventions, principles, reference docs. |
| Feedback | Show the agent what it actually produced after generation. | Tests, lint, static analysis, architecture checks, coverage, mutation tests, runtime signals. |

Feed-forward reduces ambiguity. Feedback catches drift.

[Context engineering](context-engineering.md) cuts across both sides: it shapes
feed-forward material before generation and curates the working set in flight:
message history, tool results, retrieval, notes, compaction, and subagents.
Treat the two-column table as the source article's framing for sensors, not as a
claim that every harness concern is purely pre- or post-generation.

In an ideal world, instructions and guardrails would be enough. In real
software, agents need sensors because they do not reliably satisfy every
constraint on the first pass.

## Sensors

Sensors are tools that inspect agent output and return actionable signals.

Good sensors:

- run cheaply enough to be part of the agent loop
- produce clear pass/fail or prioritized findings
- point toward remediation
- reduce the need for humans to inspect huge diffs
- preserve standards while agent throughput rises

Sensors are not only for humans. They are inputs the agent can use to
self-correct before a human reads the change.

## Sensor Taxonomy

Thoughtworks separates sensors into two broad categories:

| Sensor type | Meaning | Strength |
| --- | --- | --- |
| Computational | Deterministic tools with formal rules. | High assurance for objective constraints. |
| Inferential | Signals the agent or human must interpret. | Useful for fuzzy, exploratory, or qualitative judgment. |

Computational feedback is especially valuable when the rule is objective:
formatting, dependency boundaries, test failures, coverage thresholds, mutation
survival, security patterns, or API contracts.

Inferential feedback is useful when the work requires judgment: readability,
design intent, product fit, architecture tradeoffs, and whether a warning
matters in context.

The harness should use both. Use deterministic checks wherever the constraint is
clear. Reserve inferential judgment for places where the rule is genuinely fuzzy.

## Example Sensors

The article's TypeScript dashboard experiment used sensors such as:

- ESLint for linting
- Semgrep for static analysis
- Dependency Cruiser for structural boundaries
- coverage reports for test reach
- mutation testing for test quality

Those tools are examples, not a fixed stack. The durable pattern is to expose
code quality, architecture, and test-quality signals to the agent as part of the
normal loop.

## Bill Of Health

A useful harness can summarize sensor output as a bill of health.

That dashboard answers:

- what is green?
- what is red?
- which signals matter most?
- where should the agent repair next?
- where should a human reinvest in the harness?

The point is not to create another noisy dashboard. The point is to collapse many
signals into an actionable view of whether the codebase is healthy enough to keep
moving.

## Harness Templates

Thoughtworks points toward harness templates: reusable starting points for
different kinds of software.

Examples:

- a CRUD business service template
- a data dashboard template
- an API integration template
- a frontend application template

Each template would include both feed-forward material and sensors:

- docs and conventions
- architecture rules
- test strategy
- lint and static analysis
- dependency boundaries
- quality thresholds
- runtime verification paths

The insight is that different application archetypes need different harnesses.
There is no universal set of sensors that fits every repo.

## Human Role

Harness sensors do not remove the human from the loop. They raise the level at
which the human operates.

Instead of reading every line of a large generated diff, the human can inspect:

- the bill of health
- the remaining red signals
- the agent's repair history
- the tradeoffs that still require judgment

That gives the developer situational awareness and lets them steer at a higher
level of abstraction.

## Concept Fidelity Map

| Source concept | Preserved here as | Why it matters |
| --- | --- | --- |
| Outer harness | Agent environment | The harness surrounds generation with context and checks. |
| Feed-forward | Skills, guardrails, docs | The agent needs constraints before it acts. |
| Feedback | Sensors | The agent needs evidence after it acts. |
| Sensors | Output-observing tools | The harness must inspect generated work. |
| Computational feedback | Deterministic checks | Objective rules should become executable. |
| Inferential feedback | Interpreted signals | Some quality judgments need context. |
| TypeScript dashboard experiment | Example sensor stack | Demonstrates sensors improving quality over iterations. |
| Bill of health | Sensor dashboard | Humans need a compact view of codebase state. |
| Harness templates | Archetype-specific starting points | Different apps need different guides and sensors. |
| Situational awareness | Higher-level steering | Humans should focus on intent and judgment, not raw diff volume. |

## Relationship To Harness Engineering

[Harness Engineering](harness-engineering.md) describes the full operating
model: repository context, runtime legibility, mechanical constraints, review
loops, autonomy, and cleanup.

Harness sensors zoom in on one load-bearing part of that model: feedback. They
make the harness less dependent on one-shot instructions by giving agents and
humans a reliable way to see what actually happened.

[Context Engineering](context-engineering.md) is the input and in-flight
companion: it curates what the model sees on each turn. Harness sensors are the
output companion: they evaluate what the agent produced and return repair
signals.
