# Code As Conceptual Model

Code is not only instructions for a machine. Code is also a shared conceptual
model: the vocabulary, boundaries, abstractions, and relationships through which
humans and LLMs understand a system.

This brief is derived from Unmesh Joshi's article
["What Is Code?"](https://martinfowler.com/articles/what-is-code.html),
published on Martin Fowler's site on May 12, 2026. It is a companion to
[Harness Engineering](harness-engineering.md), because it explains why the
codebase itself is part of the harness and context.

## Core Frame

Code has two intertwined roles:

| Role | Meaning | LLM-era shift |
| --- | --- | --- |
| Machine instruction | Executable steps that make computers act. | Generation makes this cheaper. |
| Conceptual model | Names, abstractions, boundaries, invariants, and relationships that encode understanding. | This becomes more valuable. |

If writing executable syntax gets cheaper, the valuable work does not disappear.
It moves toward building better conceptual models.

## Vocabulary Building

Software development is an act of vocabulary building.

Good code names the world it models:

- domain objects
- workflows
- invariants
- technical boundaries
- integration points
- failure modes
- temporal or consistency rules

Those names are not just labels. They carry meaning and design consequences.
When the vocabulary is precise, humans can reason about the system and LLMs can
map intent to useful implementation more reliably.

## Discovering And Applying Abstractions

Coding has two interwoven activities:

- discovering and stabilizing abstractions
- applying stable abstractions to build new use cases

Discovery is the creative part. The team explores options, tries names, reshapes
boundaries, compares implementations, and slowly turns repeated structure into
stable language.

Application is different. Once the vocabulary is well named, well tested, and
well understood, new use cases can often be built by reusing that language. This
is where LLMs become more reliable: they can follow an established vocabulary
instead of inventing one.

The article connects this point to
["Conversation: LLMs and Building Abstractions"](https://martinfowler.com/articles/convo-llm-abstractions.html),
which develops the same distinction between discovering abstractions and
applying them.

## Domain And Technical Translation

Most software sits at the intersection of several vocabularies:

- the business domain
- the technical platform
- the programming language
- the framework or library ecosystem
- the team's local architecture

Coding translates between those vocabularies. A retail system, for example, may
map customers, products, orders, shipments, and payments into resources,
methods, repositories, services, transactions, events, and invariants.

Technical vocabulary has consequences too. A web architecture concept such as
`GET` is not just a method name. It carries semantics around retrieval,
cacheability, idempotence, and system design. A team that misses those meanings
can generate code that looks normal while encoding the wrong model.

The quality of the translation determines how legible the system is.

## Bounded Contexts

Some vocabulary is broadly shared. Some is local.

Technical frameworks work well when a domain has recurring, stable semantics.
Closer to the core business model, abstractions usually have to be discovered
locally. The same word can mean different things in different contexts, and each
context needs its own language and model.

This is why bounded contexts matter for agentic systems. An agent that crosses
context boundaries without understanding the local vocabulary will produce code
that may compile but misrepresent the domain.

Local vocabulary is discovered through feedback. The article names TDD as one
practice that forces the model and its behavior to stay in contact while names,
abstractions, and boundaries are being found. It also connects this to
Domain-Driven Design's ubiquitous language: a shared language developed by
developers and domain experts, then tested against working software.

Coding cannot happen in isolation. Domain experts, users, and developers all
help shape the local language. For agents, that means repo context should expose
not only code structure, but also the business vocabulary, decision history, and
tests that keep the vocabulary honest.

This also ties the article back to agile practice: individuals and interactions,
customer collaboration, working software, and response to change are ways of
discovering and refining vocabulary through feedback.

## Programming Languages As Thinking Tools

Programming languages are not only output formats. They shape thought.

Different language constructs reveal different designs:

- channels and lightweight threads suggest one way to model concurrency
- ownership models suggest one way to model resource lifetimes
- object models suggest one way to organize identity and behavior
- functional composition suggests one way to sequence transformations

Sometimes a programming language is too verbose for the concept being explored.
A pseudo-formal spec, DSL, or modeling notation can make the underlying
structure clearer before implementation.

The point is that writing code is part of thinking. Teams are not meant to
become passive reviewers of generated code. The act of writing, reshaping, and
testing code is how understanding gets built.

## Working With LLMs

LLMs map vocabulary to likely structures.

Names such as `Controller`, `Repository`, `Reducer`, `TransactionLog`, or
`ConsensusModule` carry learned associations. If the prompt and codebase use
vague or inconsistent language, the model has to guess. If the codebase has
clear names, boundaries, tests, and examples, the model has structure to follow.

That makes vocabulary part of the harness.

Good vocabulary improves:

- prompt interpretation
- file discovery
- code generation
- refactoring
- test generation
- review quality
- error recovery

LLMs can also help during abstraction discovery by showing alternatives quickly:
different names, boundaries, structures, or language projections. That is useful
only when the developer stays engaged with the model being formed. During
application of stable abstractions, LLMs can take on more repetitive generation
because the vocabulary already constrains the work.

## Cognitive Debt

Cognitive debt accumulates when a codebase contains words, abstractions, and
structures that the team does not understand.

LLMs amplify this risk because they can quickly generate plausible code with
familiar-looking patterns. The code may compile and pass basic tests, while still
introducing concepts nobody actually owns.

This is a dangerous failure mode:

- the vocabulary looks familiar
- the behavior seems plausible
- the tests are thin
- the team cannot explain the model
- future agents copy the pattern

The problem is not that an LLM generated code. The problem is that the codebase
gained vocabulary faster than it gained shared understanding.

## Code As Shared Conceptual Model

Once a strong vocabulary exists, code becomes a shared conceptual model that
both humans and LLMs can use.

Good foundational code can hide incidental complexity behind a clearer
interface. A DSL, internal library, or small domain-specific API can make the
system's vocabulary easier to apply. The interface becomes closer to the
language of the domain, while executable behavior, tests, types, and invariants
stand behind it.

This is why LLMs work well on top of stable abstractions. They are strong at
mapping natural-language intent onto an existing vocabulary. If the vocabulary
is executable, the code itself becomes a guardrail: the model can generate,
check, and repair against real behavior rather than only prose.

The source gives PlantUML as a concrete example of this pattern: an external DSL
where the LLM can map natural language onto a constrained, executable vocabulary.

## Code As Harness And Context

Harness engineering often focuses on external supports: prompts, specs, tests,
static checks, docs, and tools.

Those matter. But well-structured code is itself harness and context.

Strong foundational code gives agents:

- stable concepts
- clear examples
- executable behavior
- tests
- types
- invariants
- local vocabulary
- boundaries to respect

When the codebase has a well-formed conceptual language, agents can use that
language to build new use cases. The better the model, the less the agent has to
guess.

That changes the dependence on prompts and models. With stable abstractions and
clear semantics, the code structure and tests carry more of the context load.
The agent does not need every instruction to be perfectly prompt-engineered, and
the system becomes less fragile across different LLMs.

## Concept Fidelity Map

| Source concept | Preserved here as | Why it matters |
| --- | --- | --- |
| Two aspects of code | Instructions and conceptual model | Generation cheapens syntax, not understanding. |
| Vocabulary in code | Names carry meaning | Agents need stable concepts to map intent to implementation. |
| Discovering and applying abstractions | Creative discovery vs. reliable reuse | LLMs behave differently when inventing vocabulary than when applying stable vocabulary. |
| Domain translation | Business and technical vocabularies | Good design maps between domains deliberately. |
| Bounded contexts | Local vocabulary boundaries | A concept is only valid inside its context. |
| TDD and ubiquitous language | Feedback-built vocabulary | Tests and collaboration keep language tied to real behavior. |
| Languages as thinking tools | Constructs shape design | Code-writing can be part of discovering the model. |
| Working with LLMs | Vocabulary guides model behavior | LLMs follow names, APIs, idioms, and examples. |
| Cognitive debt | Vocabulary without understanding | Generated code can introduce concepts faster than teams absorb them. |
| Shared conceptual model | Stable abstractions become reusable language | Once the model exists, new use cases can be built through it. |
| DSLs and executable vocabulary | Natural-language interface over guardrailed abstractions | LLMs can map intent onto code-backed vocabulary and repair against behavior. |
| Code as harness and context | Foundational code constrains agents | Tests, types, invariants, and abstractions guide future generation. |
| Model and prompt robustness | Strong code carries context load | Stable abstractions reduce dependence on perfect prompts or a specific LLM. |

## Relationship To Harness Engineering

[Harness Engineering](harness-engineering.md) describes the surrounding system
that makes agents reliable: repository context, tools, checks, runtime access,
review loops, and cleanup.

Code as conceptual model adds a deeper point: the codebase is not only something
the harness protects. It is one of the most important parts of the harness.

Good code gives future agents a language to work in. Poorly understood generated
code creates cognitive debt that future agents will copy.

[Context Engineering](context-engineering.md) explains the same relationship from
the model's working-set side: clear names, boundaries, tests, and examples reduce
the amount of prose an agent needs before it can act coherently.
