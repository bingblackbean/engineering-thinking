# Vision (v2.1)

## Vision

Artificial Intelligence has dramatically reduced the cost of producing software artifacts — including code, tests, documentation, and other engineering outputs.

However, it has not reduced the cost of understanding, designing, or evolving software systems. In many cases, it has made these activities even more important.

As software production becomes inexpensive, engineering judgment becomes increasingly valuable.

The purpose of this handbook is not to teach programming languages, frameworks, or AI tools.

Its purpose is to help engineers build a durable way of thinking.

This handbook distills the timeless principles of software engineering from their original sources and explains how they apply to modern AI-assisted software development.

Rather than collecting tips or best practices, it aims to build mental models that remain useful regardless of programming language, framework, or AI model.

---

## Intended Reader

This handbook is written for engineers who already write code with AI assistance — using tools such as Claude Code, Copilot, or Spec Kit — but who feel a gap between *generating* software and *engineering* it.

They are not beginners learning to program. They are practitioners who can produce working code quickly, and who now face a harder question: how do I know if this design is *right*, not just *working*?

This handbook is also not primarily written for researchers building AI models, nor for users simply learning how to operate an AI tool. It teaches someone who already uses AI tools how to make the judgment calls those tools cannot make for them.

---

## Core Belief

Software engineering principles are not rules to memorize.

They are ways of thinking.

A principle is valuable only when it influences architectural decisions, design choices, documentation, collaboration, and implementation.

This handbook is itself a software system: it has structure, dependencies, an audience, and a lifecycle of change. Because a principle demonstrates its value through application, not merely through description, this handbook must be built using the same principles it teaches.

The handbook itself is the first case study.

---

## Mission

Build a trustworthy reference that connects classical software engineering with AI-native engineering.

Every modern practice should be traceable to established engineering principles rather than temporary tool-specific techniques.

Readers should understand not only what to do, but why the practice exists.

---

## Scope

This handbook focuses on enduring engineering principles, including software design, architecture, modularity, abstraction, complexity management, domain modeling, engineering processes, and organizational design.

It does not attempt to teach programming languages, frameworks, or prompt engineering techniques.

Instead, it provides the conceptual foundation upon which those techniques can be evaluated — including techniques for working with AI agents. Tool-specific practices (e.g. how to write a Claude.md, how to structure a Spec Kit spec) will appear in this handbook, but only downstream of a principle, and only when they can be explicitly traced back to it.

A shared glossary of terms, maintained alongside the chapters, defines the boundary of this scope in practice: any concept without an agreed definition in the glossary is not yet ready to become an established, canonical concept in the handbook. A concept may still be explored in draft form before it earns a glossary entry — the glossary gates what is treated as settled knowledge, not what may be discussed.

---

## Design Principles

**1. Evidence First**

Every principle must be traceable to its original source: author, work, and the original context in which it was stated.

Secondary sources — surveys, retrospectives, interviews — may be used to aid explanation, but cannot replace primary sources for attribution. When only a secondary source is available, this handbook says so explicitly rather than implying direct access to the original.

A principle without a traceable source is labeled as this handbook's own interpretation, not attributed to the original author.

Interpretations are clearly separated from original ideas.

**2. Principle Before Technique**

Explain why before explaining how.

Timeless principles always precede tool-specific practices. Techniques are not excluded from this handbook — they are welcome, but only as the last step of a chapter, and only when each technique can be traced back to the principle that justifies it. A technique with no traceable principle does not belong in this handbook.

**3. Conceptual Integrity**

The entire handbook uses a consistent vocabulary.

Each concept has one name and one precise definition, recorded in a shared glossary that every chapter is written against. When a new chapter needs a term already defined elsewhere, it reuses that definition rather than redefining it. Proposing a new definition for an existing term is treated as a deliberate, visible revision to the glossary, not a silent local variation.

**4. Separation of Fact and Interpretation**

Original principles, historical context, and AI-era interpretations are explicitly distinguished.

Readers should always know whether they are reading an author's idea or a modern application.

**5. Modularity**

Each chapter has a clear responsibility and a defined dependency boundary — not zero dependencies, but transparent ones.

Where a chapter relies on a concept introduced elsewhere, it says so explicitly, so readers can follow the dependency rather than encounter an unexplained assumption.

**6. Continuous Evolution**

Like software systems, this handbook will evolve, but evolution and correction are handled differently.

*Evolution* means new chapters extend the handbook's mental models to new situations without discarding what came before.

*Correction* means an existing chapter's content — a stale case study, a flawed example, an imprecise claim — is revised in place when it's found to be wrong. Correcting a mistake is not the same as replacing a mental model, and this handbook does not treat "the model changed" and "the earlier writing was wrong" as the same event. Every revision states which one it is.

---

## Success Criteria

**Reader-level:**

A successful reader will no longer ask:

> "How should I write this prompt?"

Instead, they will ask:

> "What engineering principle should guide this decision?"

That shift — from techniques to principles, and from implementation to reasoning — is the purpose of this handbook.

**Handbook-level:**

Because this handbook is itself a system under its own principles, its own reasoning must be traceable. Every recommendation it makes should be able to answer:

- What principle supports it?
- What evidence supports that principle?
- What assumptions does this application make?

A recommendation that cannot answer these three questions is not yet ready to be published.

---

## Change Log: v2 → v2.1

1. AI scope widened from "code generation" to "software artifacts" (code, tests, docs, ops)
2. Intended Reader: added explicit exclusions (AI researchers, tool operators)
3. Core Belief: "proven" → "demonstrates its value through application" (avoids scientific-verification framing)
4. Scope/Glossary: added Draft vs Canonical distinction to prevent a glossary bottleneck on exploration
5. Evidence First: added Secondary Sources rule (aid explanation, cannot replace primary attribution)
6. Conceptual Integrity: unchanged (reviewer flagged as ready for Constitution as-is)
7. Modularity: "independently understood" → "clear responsibility + transparent dependency boundary"
8. Success Criteria: added Handbook-level criterion (traceability of its own recommendations), forming a reader + handbook dual loop

*Note: reviewer's Modularity suggestion overlapped with existing "minimal and explicit dependencies" language from v2 — merged into a single non-redundant statement rather than kept as two separate sentences.*
