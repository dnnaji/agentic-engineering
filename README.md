# Agentic Engineering

![Agentic Engineering loop](assets/agentic-engineering-loop.png)

Agentic engineering is the practice of designing repositories, tools, feedback
loops, and constraints so coding agents can do reliable software engineering
work with less human intervention.

This repo collects public, agent-readable notes on agentic engineering and
harness engineering. The foundational principle brief is a high-fidelity public
translation of OpenAI's article
["Harness engineering: leveraging Codex in an agent-first world"](https://openai.com/index/harness-engineering/).

## Principles

- [Harness Engineering](principles/harness-engineering.md) — the source-context
  brief preserving the article's operating model for future agents.
- [Context Engineering](principles/context-engineering.md) — context as a finite
  attention budget: curating prompts, tools, examples, history, retrieval,
  memory, and compaction so the agent sees the right working set.
- [Harness Sensors](principles/harness-sensors.md) — the feedback side of the
  harness: sensors, computational checks, and agent self-correction.
- [Code as Conceptual Model](principles/code-as-conceptual-model.md) — why code
  remains valuable as vocabulary, abstraction, and shared understanding in the
  LLM era.
- [Good Job Spec](principles/good-job-spec.md) — why agents need written
  verification criteria for taste, risk, review, done-ness, and proof.
- [Production Function Changed](principles/production-function-changed.md) — why
  cheaper implementation changes the economics of migrations, rules, tests, and
  ratchets.
- [Faster Was The Problem](principles/faster-was-the-problem.md) — why faster AI
  output raises the bar for engineering judgment, maintenance, adoption, and
  workflow design.

## Mental Model

Agentic engineering is not prompt engineering with a larger README. It is closer
to platform engineering for a new kind of worker:

- make the environment inspectable
- make the right path easy
- make the wrong path fail clearly
- make feedback durable
- make cleanup continuous

The better the harness, the less the human has to babysit individual changes.
