# Architecture (v5)

*This architecture is established by [ADR-0001: This handbook is architected as a Knowledge System, not a book](../adr/ADR-0001-knowledge-system-over-book.md). That document records the decision and the alternative considered and rejected; this document describes the resulting system in full.*

---

## 1. Purpose

- **Vision** answers *why* this handbook exists.
- **Constitution** answers *what rules must always hold*, regardless of how the system is structured underneath them.
- **Architecture** (this document) answers *what the system is*, in a way that satisfies those rules.
- **Spec** (next document) answers *what to build*.

This document defines the objects the knowledge system is made of, the rules governing how those objects depend on each other, the invariants that must always hold, and the lifecycle by which new knowledge enters and evolves within the system.

This Architecture operates under Constitution and is binding to it, not the reverse (Constitution, Article I). Where anything in this document conflicts with a Constitution rule, this document is wrong and must be amended — the Constitution is never reinterpreted to fit the Architecture.

---

## 2. System Context

```
                 Primary Sources
          (Books, Papers, Talks, Standards)
                      │
                      ▼
               Evidence Layer
                      │
                      ▼
              Principle Layer
                      │
                      ▼
           Mental Model Layer
                      │
                      ▼
             Practice Layer
                      │
                      ▼
            Technique Layer
                      │
                      ▼
          AI Application Layer
                      │
                      ▼
             Published Views
        (Book / Site / MCP / Agent Memory)
```

This diagram shows the *flow* of knowledge through the system, from primary source to published output. It is not the object model itself — object identity is defined in Section 3, independent of this flow. The critical constraint this diagram encodes: **AI Application is never built directly on top of a Source.** Skipping layers is a violation of this architecture, not a shortcut.

---

## 3. Domain Objects

These are the knowledge system's object *types*. This section defines what each object **is** and is responsible for — not how objects relate to each other. Relationships (dependency, layering) are a separate concern, defined in Section 4.

This distinction matters: an object type is a fact about the knowledge system's vocabulary (and belongs in the Glossary). A dependency relationship is a design rule imposed on top of that vocabulary. Conflating the two — implying that "Mental Model is above Principle" is part of what a Mental Model *is* — would make it impossible to ever revisit the dependency rule without also having to redefine the objects themselves.

| Object | Responsibility | Must NOT do |
|---|---|---|
| **Source** | Hold the original artifact of record — a book, paper, talk, RFC, standard. | Never interprets or explains. |
| **Evidence** | Prove that a Principle traces to a Source — a citation, a page/chapter reference, a quote boundary. | Never produces an opinion. |
| **Principle** | State what the original author actually claimed (e.g. Information Hiding, Deep Modules, Conceptual Integrity). | Never mixes in modern interpretation. |
| **Mental Model** | Synthesize one or more Principles into a reusable way of thinking (e.g. "Reduce Cognitive Load" synthesizing Information Hiding + Deep Modules). Typically many-to-one with Principle — this is the one object type expected to draw on multiple Principles at once. | Never exists without a traceable path back to at least one Principle. |
| **Practice** | A repeatable engineering activity independent of any specific tool (e.g. ADR writing, Refactoring, Event Storming, Architecture Review). | Never named after a specific product or vendor. |
| **Technique** | A concrete, tool-specific application (e.g. Claude.md, Spec Kit spec, a prompt template). | Never cites a Source directly — must cite the Practice it implements. |
| **AI Application** | The outermost consumer: Claude, Copilot, Cursor, Spec Kit, an agent, an MCP server. | Never treated as the center of the system — it is a consumer of Technique, not a source of truth. |
| **View** | A rendering of the knowledge system for one consumption context (book, site, MCP, agent memory). | Never a target of a dependency — see Section 9. |

---

## 4. Dependency Rule (Layer Rules)

This is a design rule imposed *on top of* the objects in Section 3 — not a property of the objects themselves.

```
AI Application
      ↓
  Technique
      ↓
   Practice
      ↓
Mental Model
      ↓
  Principle
      ↓
   Evidence
      ↓
    Source
```

**Rule:** an object may only depend on the object type immediately below it in this chain (i.e., toward Source). It may never skip a link, and it may never depend upward.

**Explicitly forbidden:** a Technique citing a Book directly. It must cite the Practice it implements, which in turn traces to a Mental Model, which traces to a Principle, which traces to Evidence, which traces to the Source.

**Why:** Sources are decades old and fixed. Techniques change monthly. What must remain stable between them is the Principle layer. This is the Dependency Rule (Robert C. Martin) applied to knowledge instead of code: dependencies always point toward the more stable layer.

---

## 5. Architectural Invariants

Domain objects and dependency rules together give rise to a small set of statements that must hold **everywhere, always**, regardless of which View is being rendered or which chapter is being written — the equivalent of "everything is a file" (Unix) or "a commit is immutable" (Git) for this knowledge system.

**These invariants are architectural realizations of Constitution rules. They are not an independent source of authority.** They describe how this knowledge system enforces the Constitution — not a parallel set of laws alongside it. Where an invariant's wording and the Constitution rule it implements ever appear to diverge, the Constitution governs (Constitution, Article I), and this section is patched to match, not the other way around.

1. **Every knowledge object (except Source itself) must trace to Evidence.** An object with no traceable Evidence stays in Draft indefinitely (Section 8.3).
   **Implements:** Constitution C-110 (Evidence Requirement), under FL-1. Supporting: C-510 (Settled Knowledge Gate), under FL-5.

2. **A Technique must never cite a Source directly.** It must cite the Practice it implements (Section 4).
   **Implements:** Constitution C-310 (Principle Before Technique), under FL-3. This invariant is this system's specific architectural expression of the more general Constitutional rule that technique must never stand ahead of, or independent from, the principle that justifies it.

3. **One concept, one Glossary definition.** No two chapters may silently define the same term differently.
   **Implements:** Constitution C-210 (Single Definition Rule), under FL-2.

4. **The Evolvable Edge depends on the Stable Core — never the reverse.** A new AI tool or technique may never force a change to a Principle or Mental Model's definition (Section 6).
   **Implements:** Constitution C-420 (Non-Discard Rule), under FL-4. Fast-moving Technique-layer churn is architecturally prevented from ever forcing an undisclosed change to Stable Core content — which is exactly what C-420 prohibits at the content level.

5. **A View is never a dependency target.** Nothing in Sections 3–8 may exist "because the book needs it" (Section 9).
   **Implements:** no direct Constitution rule. Constitution governs knowledge content, not rendering mechanics — "View" is Architecture-level vocabulary that Constitution deliberately does not legislate (Constitution, Preamble). This invariant is instead a direct architectural application of Information Hiding (Parnas; Section 10), adopted because it serves Constitution's rules indirectly (a View that became a dependency target would eventually force content decisions to serve a specific output format, which risks violating C-330's scope discipline) — but it is not itself mandated by name anywhere in the Constitution. This is stated explicitly rather than manufacturing a citation that doesn't exist, per the same standard applied to Meta Principles in Section 11.

Any proposed change to this handbook's structure that would violate one of these five statements should be rejected at Review (Section 8.1), regardless of how useful it seems locally. Because Invariants 1–4 implement specific Constitution rules, a change violating one of them is also, transitively, a Constitution violation — not merely an architectural inconvenience.

---

## 6. Stable Core, Evolvable Edge

This is the architecture's central design principle, and the one every later Spec and Plan document should be checked against.

**Stable Core** — changes on a timescale of decades:
- Source
- Evidence
- Principle
- Mental Model

**Evolvable Edge** — changes on a timescale of months:
- Practice
- Technique
- AI Application

Because the Dependency Rule (Section 4) forces the Evolvable Edge to depend on the Stable Core and never the reverse, the arrival of a new AI tool, a new agent framework, or a new prompting technique never requires touching Source, Evidence, Principle, or Mental Model. It only ever adds a new leaf at the edge. This is what makes the system able to absorb "AI moves fast" without becoming stale — the fast-moving part is architecturally isolated from the stable part.

---

## 7. Knowledge Object Schema

Every Principle entry in the handbook is written against one fixed schema. This is the mechanism that enforces Vision's Conceptual Integrity principle at the document level.

```
Identity            — canonical name, as recorded in the Glossary
Definition           — precise, one-sentence definition
Intent               — what problem this exists to solve
Problem              — the concrete situation that motivates it
Applicability        — when this applies, when it does not, and where it
                        becomes a trade-off rather than a clear win
Evidence             — citation(s) linking to Primary Source
Primary Source       — author, work, original context
Historical Context   — when/why it was originally stated
Related Principles   — explicit, named dependencies (Modularity)
Trade-offs           — what this costs, not just what it buys
Examples             — real software systems, not invented ones
Interpretation       — explicitly labeled as this handbook's own reading
AI Applications       — Technique-layer applications, traced back up
References           — secondary sources, explicitly marked as secondary
```

**Applicability** exists because most software engineering principles are not universal laws — they hold under specific conditions and become liabilities outside them (SOLID and microservices both have well-documented histories of being applied dogmatically, past the point where their originating context still held). A Principle entry without a stated Applicability boundary is treated the same as one missing Evidence: it cannot be marked Canonical.

Every field is mandatory. A Principle entry missing "Evidence," "Primary Source," or "Applicability" stays in Draft.

---

## 8. Governance: How Knowledge Enters and Evolves

Architecture does not just organize knowledge — it organizes knowledge's *lifecycle*.

### 8.1 New knowledge — the full pipeline

```
Collect → Verify → Normalize → Review → Decision Log → Approve → Publish
```

- **Collect** — a candidate Source, Principle, or Mental Model is proposed.
- **Verify** — Evidence is checked: is the Primary Source traceable? Is a Secondary Source being misrepresented as primary?
- **Normalize** — checked against the Glossary. If the term already exists, this candidate must reuse the existing definition or explicitly propose a revision. This is also the step where a concept graduates from **Draft** to **Canonical** status.
- **Review** — checked against the Knowledge Object Schema (Section 7) for completeness, and against Section 4's Dependency Rule for correct placement.
- **Decision Log** — any non-trivial disagreement surfaced during Normalize or Review (a contested definition, a disputed layer placement, a rejected Applicability boundary) is recorded with its reasoning, not just its outcome. This is what lets someone years from now understand *why* a term was defined the way it was, instead of only *that* it was.
- **Approve** — a deliberate go/no-go decision, not automatic.
- **Publish** — becomes visible in whichever Views are active.

### 8.2 Correction — a short path, not the full pipeline

Vision draws a hard line between *Evolution* (new material extending the model) and *Correction* (fixing something already published that was wrong).

```
Correction:  Verify → Review → Decision Log → Approve → Publish
```

Correction skips **Collect** (nothing new is being proposed) and skips the Glossary-graduation sense of **Normalize** (the term is already Canonical) — but still passes through Verify, so a correction cannot be made without evidence either. Every Correction must state explicitly whether it is fixing a factual error or revising a mental model.

### 8.3 Draft vs. Canonical

- **Draft** — may exist in the working system, may be discussed, may be linked to from other Draft material. Not yet trusted for citation by other entries.
- **Canonical** — has passed Verify, Normalize, and Decision Log (where applicable), is entered in the Glossary, and may be cited by other Principle or Mental Model entries.

This distinction exists specifically so that exploration is never blocked by the Glossary — only *promotion to settled knowledge* is gated.

---

## 9. Views (Information Hiding boundary)

A View is a rendering of the Knowledge System for a specific consumption context: a printed book, a website, an AI knowledge base, an MCP server, an agent's memory. Per Architectural Invariant 5 (Section 5), a View may read from any layer, but may never be a target of a dependency. Nothing in Sections 3–8 is allowed to say "this exists because the book needs it." If a rule can't be justified without referencing a specific output format, it belongs to a View-specific rendering concern, outside this architecture.

---

## 10. Design Rationale

- **Information Hiding (Parnas):** output form (PDF, site, agent) is hidden behind the knowledge model. The model can stay stable while output formats change freely.
- **Deep Module (Ousterhout):** externally, this is one system — "the Knowledge System." Internally, it has eight distinct object types (Section 3). Complexity is concentrated inside the module, not exposed at its interface.
- **Dependency Rule (Robert C. Martin / Clean Architecture):** dependencies always point toward the more stable layer (Section 4), never the reverse.
- **Domain-Driven Design (Eric Evans):** the domain objects (Section 3) were identified before any table of contents was drafted. The eventual book's chapter list is one possible arrangement of these objects — it is not the architecture itself.

---

## 11. Meta Principles (a View-level organizing lens — not a Domain Object)

During review, four recurring themes were observed running through this entire Architecture:

1. **Control Complexity** — Information Hiding, Abstraction, Deep Module
2. **Preserve Conceptual Integrity** — Ubiquitous Language, Glossary, One Definition
3. **Make Knowledge Traceable** — Evidence, Source, Interpretation, Governance
4. **Design for Evolution** — Stable Core, Dependency Rule, Evolution vs. Correction

These are a genuinely useful curatorial lens for organizing the eventual book — but they are deliberately **not** added as a ninth Domain Object or a new layer in Section 4. A "Meta Principle" like *Control Complexity* has no single traceable Primary Source of its own (Section 7 would require one); it is an editorial grouping *across* existing, independently-sourced Principles. Treating it as a real Domain Object would require it to obey the Dependency Rule and pass through Governance like everything else in Section 8 — which would misrepresent what it actually is.

Meta Principles are therefore classified as a **View** (Section 9): a book-level table-of-contents lens applied on top of already-Canonical Principles, not a new node in the knowledge graph. They remain **Draft** and are a candidate input to the Spec document, not a ratified part of this Architecture.

---

## 12. Traceability

Every architectural decision above remains traceable to a Constitution rule and, ultimately, to Vision (see, for example, Section 5's Architectural Invariants, each of which cites the Constitution rule it implements). Maintaining a living register of these links — decision, principle, evidence, and open assumptions, refreshed as review activity progresses — is an ongoing review activity, not a description of the system itself. That register belongs in Spec's Traceability Register, not here; see `spec/SPEC.md` once it exists, and `architecture/ARCHITECTURE-CHANGELOG.md` for the table as it stood before this move.

## Change Log: v4 → v5

1. Trimmed accumulated Change Log history out of this document — only this current entry remains here. Full history (v1→v2, v2→v3, v3→v4) moved to `architecture/ARCHITECTURE-CHANGELOG.md`, so a reader opening this document to understand the current system isn't required to read three prior versions' worth of diffs first.
2. Removed Section 12's Traceability table. It had grown into something closer to a Spec Review checklist — refreshed as review activity progresses — than a description of the system itself, which is what this document is responsible for. Section 12 now states the requirement in one paragraph and points to Spec's Traceability Register (once authored) and to the archived table in `ARCHITECTURE-CHANGELOG.md`.
3. From this point forward, only the most recent Change Log entry is kept in this document; each superseded entry is moved to `ARCHITECTURE-CHANGELOG.md` when the next version is published.

Full revision history: see `architecture/ARCHITECTURE-CHANGELOG.md`.

