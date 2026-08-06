# Spec (v2)

*This document operates under Constitution and Architecture. It translates Architecture's domain model into concrete, buildable deliverables. Where anything here conflicts with Architecture or Constitution, this document is wrong and must be amended.*

```
Vision           — why this system exists
     ↓
Constitution     — what must always be true
     ↓
Architecture     — what the system is, and how it satisfies those rules
     ↓
Spec (this doc)  — what to build, concretely
     ↓
Plan             — in what order, and when
     ↓
Knowledge / Book — the content itself
```

---

## 1. Purpose

Architecture defines eight Domain Object types (Source, Evidence, Principle, Mental Model, Practice, Technique, AI Application, View) and the rules governing them, but only fully specifies a schema for one of them — Principle (Architecture §7). This Spec closes that gap: it defines a concrete, fillable template for every authored Domain Object type, finalizes the repository structure those templates live in, and turns Architecture's Governance pipeline (§8) into a checklist a contributor can actually follow.

This Spec does not decide *what order* content gets written in, or *when* — that is Plan's responsibility. It decides what each piece of content must contain and where it lives once written.

**Definition Boundary:** terms used in this Spec inherit their meaning from Architecture and the Glossary. This Spec introduces no new Domain Object definitions. Where operational wording appears below that isn't already defined upstream (e.g. a template field name), it is an implementation detail serving a deliverable — not a new concept requiring its own Glossary entry. This boundary exists so Spec doesn't gradually accumulate its own parallel vocabulary as it grows, which would violate Constitution C-210 (Single Definition Rule) the same way an over-large Architecture would.

---

## 2. Deliverables

| ID | Deliverable | Depends on |
|---|---|---|
| D-1 | Finalized repository skeleton (Section 3) | Architecture §3, §9 |
| D-2 | Glossary bootstrap — initial Canonical entries | Architecture §3 (object types), Constitution FL-2 |
| D-3 | Knowledge Object Templates — one per authored Domain Object type (Section 4) | Architecture §3, §7 |
| D-4 | Traceability Register — living table, carried forward from Architecture (Section 5) | Architecture §12 (archived), Constitution C-610 |
| D-5 | Governance Checklist — Architecture §8's pipeline as an operational checklist (Section 6) | Architecture §8, Constitution Article III |
| D-6 | One worked example per authored Domain Object template (Section 4) | D-3 |

Note on D-6: a template that has never been filled in is an unproven design, not a working one. Per Vision's Core Belief ("a principle demonstrates its value through application, not merely through description"), each template in Section 4 ships with one worked example rather than standing alone as an abstract form.

---

## 3. Repository Skeleton

This finalizes the structure discussed and partially agreed across Vision, Constitution, and Architecture review.

```
engineering-thinking/
├── README.md
├── vision/
│   └── VISION.md
├── constitution/
│   └── CONSTITUTION.md
├── architecture/
│   ├── ARCHITECTURE.md
│   └── ARCHITECTURE-CHANGELOG.md
├── adr/
│   └── ADR-0001-knowledge-system-over-book.md
├── glossary/
│   └── GLOSSARY.md
├── knowledge/
│   ├── sources/
│   ├── principles/
│   ├── mental-models/
│   ├── practices/
│   ├── techniques/
│   └── ai-applications/
├── spec/
│   ├── SPEC.md
│   ├── SPEC-CHANGELOG.md
│   └── templates/
│       ├── source-template.md
│       ├── principle-template.md
│       ├── mental-model-template.md
│       ├── practice-template.md
│       ├── technique-template.md
│       └── ai-application-template.md
└── plan/
    └── PLAN.md
```

**Notes:**
- `knowledge/` has no `evidence/` folder and no `views/` folder, per Architecture §3: Evidence is a field inside a Principle entry, not an independent object; View is a rendering, not authored content, and lives outside `knowledge/` entirely (Architecture §9).
- `spec/SPEC-CHANGELOG.md` is created now, empty, following the same pattern just adopted for Architecture: this document keeps only its current Change Log entry going forward, with history archived externally from the start rather than retrofitted later.
- `adr/` gains a new entry only when a future *decision with rejected alternatives* is made — not for routine edits. Routine edits to Architecture, Constitution, or this Spec are ordinary revisions with their own Change Log, not ADRs.

---

## 4. Knowledge Object Templates

Each template below is derived from its object's responsibility as defined in Architecture §3. Every template carries a **Status** field (Draft / Canonical, per Architecture §8.3) and, where applicable, fields enforcing Constitution rules directly (Evidence, Interpretation labeling).

### 4.1 Source Template

```
Identity          — canonical short name (e.g. "ousterhout-2018")
Title             — full title of the work
Author(s)         —
Type              — book | paper | talk | standard | RFC
Year              — original publication year
Edition/Version   — if applicable
Access Reference  — ISBN / DOI / URL
Status            — Draft | Canonical
Notes             — factual only (edition history, translations, etc.)
```
**Must not contain:** interpretation, opinion, or evaluation of the source's ideas (Architecture §3; Constitution C-130).

**Worked example:**
```
Identity:         ousterhout-2018
Title:            A Philosophy of Software Design
Author(s):        John Ousterhout
Type:             book
Year:             2018
Edition/Version:  2nd edition
Access Reference: ISBN 978-1732102217
Status:           Canonical
Notes:             1st edition published 2018; 2nd edition (cited here) 2021.
```

### 4.2 Principle Template

*(Reused verbatim from Architecture §7 — not redefined here, per Constitution C-210, Single Definition Rule.)*

```
Identity, Definition, Intent, Problem, Applicability, Evidence,
Primary Source, Historical Context, Related Principles, Trade-offs,
Examples, Interpretation, AI Applications, References
```
See Architecture §7 for field-by-field description and the Canonical gating rule (missing Evidence, Primary Source, or Applicability keeps the entry in Draft).

**Worked example:** see `knowledge/principles/deep-modules.md` (Section 7 of this Spec provides the full worked instance).

### 4.3 Mental Model Template

```
Identity            —
Definition          — one sentence
Synthesized From    — one or more Principle identities (required — a Mental
                       Model with zero linked Principles is not eligible for
                       Canonical status; Architecture §3)
Problem             — what situation calls for this Mental Model
Applicability       — when it applies / does not
Trade-offs          —
Examples            — real systems
Interpretation      — explicitly this handbook's synthesis, not any single
                       author's claim (a Mental Model is definitionally an
                       interpretation — Constitution C-140 still requires
                       this be stated, not assumed obvious)
AI Applications     —
Status              — Draft | Canonical
Decision Log Ref    — if the synthesis was contested during Review
```

**Worked example:**
```
Identity:         reduce-cognitive-load
Definition:       Design so a reader/maintainer needs to hold as little in
                  working memory as possible to safely make a change.
Synthesized From: information-hiding, deep-modules
Problem:          Systems that are individually "correct" per each source
                  principle can still overwhelm a maintainer if the
                  principles aren't considered together.
Applicability:    Applies to any interface a human must reason about
                  directly. Less relevant to interfaces only ever touched
                  by generated code with no human review step.
Trade-offs:       Can be used to justify under-documenting an interface
                  ("it's simple, no docs needed") — this is a misuse, not
                  an application, of the model.
Examples:         Unix file descriptor interface; Git's plumbing/porcelain
                  split.
Interpretation:   This is this handbook's synthesis of Parnas (1972) and
                  Ousterhout (2018); neither author uses this exact phrase.
AI Applications:  Used as the evaluation lens in Technique
                  "claude-md-interface-review".
Status:           Draft
Decision Log Ref:  none yet
```

### 4.4 Practice Template

```
Identity          —
Definition        —
Purpose           — what problem this repeatable activity solves
Operationalizes   — the Principle(s) or Mental Model(s) it puts into motion
Description       — the activity itself, in tool-independent terms
Examples          —
Trade-offs        —
Status            — Draft | Canonical
```
**Must not do:** name a specific product or vendor (Architecture §3).

**Worked example:**
```
Identity:       architecture-decision-record
Definition:     A short, dated document recording a significant design
                decision, the alternatives considered, and why the chosen
                one was accepted.
Purpose:        Preserve the reasoning behind a decision so it isn't
                re-litigated or silently reversed by someone unaware of
                why it was made.
Operationalizes: reduce-cognitive-load; evidence-first (Constitution FL-1)
Description:    On a significant, hard-to-reverse decision, write: Status,
                Decision, Consequence, Rationale, Alternatives Considered.
                Store it as an immutable record; supersede rather than edit.
Examples:       This handbook's own ADR-0001.
Trade-offs:     Overhead if applied to routine, reversible decisions —
                intended for decisions with real switching cost.
Status:         Canonical
```

### 4.5 Technique Template

```
Identity          —
Definition        —
Implements        — the Practice this operationalizes (never a Source
                     directly — Architecture Invariant 2)
Tool Context      — the specific product/platform this applies to
Steps             — concrete, tool-specific instructions
Example           —
Caveats           — where this technique breaks or goes stale
Status            — Draft | Canonical
```

**Worked example:**
```
Identity:     claude-md-interface-review
Definition:   Using a CLAUDE.md file to make an AI coding agent flag
              interfaces that violate Deep Module / Reduce Cognitive
              Load before generating an implementation.
Implements:   architecture-decision-record is unrelated — implements
              Practice "interface-review" instead (see knowledge/practices)
Tool Context: Claude Code
Steps:        1. Add a section to CLAUDE.md instructing the agent to
              state, for any new public interface, what it hides and
              what it exposes, before writing the implementation.
              2. Require the agent to flag if the exposed surface is
              larger than the hidden complexity.
Example:      See knowledge/ai-applications/ for a full transcript.
Caveats:      Effectiveness depends on the underlying model actually
              following persistent instructions; revisit if model
              behavior changes.
Status:       Draft
```

### 4.6 AI Application Template

```
Identity          —
Definition        —
Implements        — the Technique this applies (never a Practice or
                     Principle directly — Dependency Rule, Architecture §4)
Agent/Tool        — Claude, Copilot, Cursor, an MCP server, etc.
Workflow          — what actually happens, step by step, in practice
Example           — a real or representative transcript/output
Caveats           —
Status            — Draft | Canonical
```

**Worked example:** intentionally deferred — the first real AI Application entry should be written against an actual agent session, not fabricated for this Spec, per Constitution C-110 (Evidence Requirement extends here by analogy: don't manufacture an example where a real one is cheap to obtain). Flagged as an open item for Plan.

---

## 5. Traceability Register

Carried forward from Architecture's archived Section 12 table (see `architecture/ARCHITECTURE-CHANGELOG.md`), now extended with this Spec's own decisions. This is a living document — rows are added as new significant decisions are made across any layer, not just Architecture's.

| Decision | Principle it supports | Evidence | Key assumption |
|---|---|---|---|
| Knowledge System over Book | Vision Core Belief; Conceptual Integrity | Parnas, Ousterhout | Multiple output Views will actually be needed |
| Dependency Rule | Evidence First; Continuous Evolution | Robert C. Martin | Principle-layer content changes slower than Technique-layer |
| Architectural Invariants | Constitution C-110, C-210, C-310, C-420 | Constitution Article III | Four mapped invariants are sufficient |
| Stable Core / Evolvable Edge | Constitution FL-4 | Derived synthesis | AI tooling churn continues to outpace principle-level change |
| Applicability field | Separation of Fact and Interpretation | SOLID/DDD/Microservices critique history | One field is enough for most principles |
| Decision Log | Constitution Article IV; Evidence First | Standard ADR practice | Contributors log contested decisions rather than skip it |
| Meta Principles (Architecture §11) | Conceptual Integrity, as organizing lens only | None — explicitly unsourced | Four groupings still hold as more Principles are added |
| **Per-type templates (D-3, this Spec)** | Architecture §7's Principle schema, generalized | Derived synthesis, not independently sourced | Six templates are enough; a ninth object type would require a new template, not a variant of an existing one |
| **Governance Checklist (D-5, this Spec)** | Architecture §8 | Direct restatement of the pipeline as a checklist | A checklist is sufficient operationalization; may need tooling (see Constitution's flagged auto-generation note) |

The last column remains deliberately unresolved — these are assumptions for Plan to stress-test against real content, not facts already proven.

---

## 6. Governance Checklist (operationalizing Architecture §8)

A contributor adding new knowledge follows this checklist. Each step cites the Architecture/Constitution rule it satisfies. **Approval authority is external to this Spec** — Constitution Article V deliberately leaves who may approve as an organizational question, not a constitutional or specification one; this checklist assumes that role exists and is filled by someone, without naming who.

**Adding new content (full pipeline):**
- [ ] **Collect** — draft the entry using the correct template (Section 4)
- [ ] **Verify** — primary source cited; if only a secondary source exists, this is stated explicitly (Constitution C-110, C-120)
- [ ] **Normalize** — checked against `glossary/GLOSSARY.md`; if the term exists, this entry reuses that definition or explicitly proposes a revision (Constitution C-210, C-220)
- [ ] **Review** — checked against the template's required fields (Section 4) and against the Dependency Rule (Architecture §4 — does this object cite the right object type below it?)
- [ ] **Decision Log** — if Normalize or Review surfaced a real disagreement, it's recorded, not just resolved silently (Constitution Article IV)
- [ ] **Approve** — a deliberate go/no-go, not automatic
- [ ] **Publish** — status flips from Draft to Canonical in both the entry and the Glossary

**Correcting existing content (short path):**
- [ ] State explicitly: is this a **Correction** (fixing an error) or an **Evolution** (extending to a new situation)? (Constitution C-410 — this is Blocking; an unlabeled revision is incomplete)
- [ ] **Verify** — the correction itself is evidence-backed
- [ ] **Review** — still checked against the template
- [ ] **Decision Log** — if contested
- [ ] **Approve → Publish**

---

## 7. Non-Goals

This Spec deliberately does not:
- Decide the order chapters, principles, or sources are written in — that is Plan's responsibility.
- Author the actual content library (the real Principle/Mental Model/Practice entries beyond the worked examples above) — Plan sequences that work; this Spec only proves the templates are fillable.
- Build tooling to auto-generate the Traceability Register or Glossary from rule metadata — already flagged in Constitution's Change Log (v2→v3) as future tooling work, not resolved here.
- Define who has authority to Approve a Governance pipeline step — Constitution Article V already states this is an organizational question outside its scope, and it stays outside this Spec's scope too, for the same reason.

---

## Change Log: v1 → v2

1. D-6 wording tightened: "one worked example per template" → "one worked example per *authored* Domain Object template" — the original phrasing risked implying all 8 Architecture Domain Object types get a template, when only 6 are authored content (Evidence and View are deliberately excluded, per Section 3's notes)
2. Added a **Definition Boundary** statement to Section 1: this Spec inherits all terms from Architecture/Glossary and introduces no new Domain Object definitions, to prevent Spec from gradually accumulating a second, parallel vocabulary as it grows
3. Added one sentence to Section 6 (Governance Checklist) clarifying that Approval authority is external to this Spec, consistent with Constitution Article V — added so a new contributor doesn't wonder who "Approve" refers to
4. No changes made to the Repository Skeleton (Section 3) or Source Template (Section 4.1) — a review round flagged both as apparently incomplete, but this was due to code-block formatting being stripped in a copy/paste, not an actual gap; verified against source file, both already correct as written
