# Constitution (v3)

## Preamble

This Constitution defines the rules every future change to this handbook must obey. It sits directly beneath Vision and directly above every other document in this project:

```
Vision           — why this system exists
     ↓
Constitution     — what must always be true (this document)
     ↓
Architecture     — how the system satisfies these rules
     ↓
Spec / Plan      — what to build, in what order
     ↓
Knowledge / Book — the content itself
```

Every rule in this Constitution is derived from Vision. None is derived from Architecture, Spec, or any other downstream document — a rule that could only be justified by referencing a downstream document does not belong here; it belongs in that document instead.

Where any downstream document conflicts with a rule in this Constitution, the downstream document must be amended. This Constitution is never amended to accommodate a downstream document.

This Constitution deliberately avoids the specific vocabulary of any downstream document (e.g. it does not use the term "Canonical," which is an Architecture-level mechanism). Rules here are stated in terms general enough that Architecture — or any future architecture — can implement them without the wording having to change.

This Constitution has two tiers, deliberately: **Foundational Laws** (Article II), which are few and change on the same timescale as Vision itself, and **Standing Rules** (Article III), which implement those laws in more operational terms and may be added to or refined more readily. This mirrors the handbook's own Stable Core / Evolvable Edge design (Architecture, Section 6) — applied here to governance itself.

---

## Article I — Authority and Precedence

1. This Constitution is binding on Architecture, Glossary, Spec, Plan, and all content in the knowledge base, including the eventual book.
2. No rule in this Constitution may be waived for a single instance, a single chapter, or a single contributor. If a rule produces a bad outcome in a specific case, the rule is amended (Article V) — it is not quietly ignored in that case.
3. Every Foundational Law in Article II must cite the section of Vision it derives from. Every Standing Rule in Article III must cite the primary Foundational Law it implements, and may cite additional supporting laws where genuinely applicable (Article III). A proposed law or rule with no traceable primary source is not eligible for inclusion in this Constitution.

---

## Article II — Foundational Laws

These are stated broadly and deliberately. They are not a checklist — they are the handful of things that must always hold, regardless of how the handbook's structure evolves underneath them.

### FL-1 — Evidence
All claims presented as established fact shall be traceable to a primary source. Where a claim is not traceable, it shall be explicitly labeled as this handbook's own interpretation.
**Source:** Vision, Design Principle 1 (Evidence First)

### FL-2 — Conceptual Integrity
Each concept shall have exactly one governing definition at any time. That definition shall be recorded, and shall be changed only through a deliberate, visible act — never silently.
**Source:** Vision, Design Principle 3 (Conceptual Integrity)

### FL-3 — Structural Discipline
Technique shall never be presented ahead of the principle that justifies it. Dependency between parts of this handbook shall always be disclosed, never silently assumed. Content outside this handbook's established scope shall not be included unless it is traceable to a principle already within scope.
**Source:** Vision, Design Principle 2 (Principle Before Technique); Design Principle 5 (Modularity); Scope

### FL-4 — Evolution over Replacement
This handbook shall extend its established mental models rather than silently discard them. Every revision shall declare, explicitly, whether it is correcting an error or evolving a model to a new situation — these shall never be treated as the same kind of event.
**Source:** Vision, Design Principle 6 (Continuous Evolution)

### FL-5 — Gated Knowledge
No concept shall be treated as settled, or relied upon by other content, until it satisfies this Constitution's requirements for evidence and definition. Before that point, it may be explored, but not depended upon.
**Source:** Vision, Scope (the glossary as boundary of settled knowledge)

### FL-6 — Traceable Reasoning and Self-Application
Every recommendation this handbook makes — and every structural decision made about the handbook itself — shall be answerable in terms of the principle behind it, the evidence behind that principle, and the assumptions of its specific application.
**Source:** Vision, Success Criteria (Handbook-level); Core Belief

---

## Article III — Standing Rules

Each Standing Rule implements one **primary** Foundational Law, and may cite additional **supporting** laws where the rule genuinely serves more than one — many real engineering principles are cross-cutting, and forcing a single category onto them would misrepresent them. A rule with no primary law, or one manufacturing a supporting law it doesn't actually rely on, does not satisfy this Article. Numbering is grouped by category (under the rule's primary law) with gaps left intentionally, so new rules can be inserted into a category without renumbering existing ones. Each rule carries a **Severity**: **Blocking** (the violating content may not be published or relied upon until resolved) or **Advisory** (the violation must be tracked and resolved, but does not by itself halt publication of the surrounding content).

### C-1xx — Evidence & Attribution (implements FL-1)

**C-110 — Evidence Requirement**
Every principle presented as established fact must be traceable to a primary source: an author, a specific work, and the original context in which it was stated.
Severity: Blocking. Violation: content may not be presented as established fact until re-labeled as interpretation or backed by a source.

**C-120 — Secondary Source Disclosure**
Secondary sources may aid explanation but must never substitute for primary attribution. Where only a secondary source is available, this must be stated explicitly.
Severity: Advisory. Violation: the citation must be corrected to disclose its secondary status before the content is treated as settled.

**C-130 — Interpretation Labeling**
Content with no traceable primary source must be explicitly labeled as this handbook's own interpretation, never attributed to the original author.
Severity: Blocking. Violation: unlabeled interpretation presented as an author's claim must be corrected on discovery (Article III, C-410).

**C-140 — Attribution Clarity**
All content must make explicit whether it represents an original author's claim, historical context, or this handbook's own interpretation. A reader must never have to guess.
Severity: Blocking. Violation: ambiguous content is not eligible to be treated as settled until attribution is made explicit.

### C-2xx — Conceptual Integrity (implements FL-2)

**C-210 — Single Definition Rule**
Each concept has exactly one definition in active use at a time. No two parts of the handbook may define the same term differently without one explicitly superseding the other.
Severity: Blocking. Violation: the conflicting definition must be reconciled or formally superseded before either may stand.

**C-220 — Deliberate Revision Rule**
Changing an existing definition is a deliberate, visible act. Every such change must be identifiable as a revision, distinct from ordinary new content.
Severity: Advisory. Violation: an undisclosed redefinition must be reverted or converted into a disclosed revision.

### C-3xx — Structural Rules (implements FL-3)

**C-310 — Principle Before Technique**
No tool-specific technique may be presented without the principle that justifies it appearing first, in the same unit of content.
Severity: Blocking. Violation: the technique content is withheld until a justifying principle is presented ahead of it.

**C-320 — Dependency Disclosure**
Content that depends on a concept introduced elsewhere must say so explicitly.
Severity: Advisory. Violation: the dependency must be made explicit before the content is treated as complete.

**C-330 — Scope Boundary**
Content that teaches a programming language, framework, or tool operation for its own sake is out of scope, unless downstream of, and traceable to, an established principle.
Severity: Advisory. Violation: out-of-scope content is relocated or removed.

### C-4xx — Evolution & Correction (implements FL-4)

**C-410 — Evolution/Correction Distinction**
Every revision to existing content must state explicitly whether it is a Correction or an Evolution.
Severity: Blocking. Violation: a revision with no stated kind is incomplete and cannot be published.

**C-420 — Non-Discard Rule**
Extending the handbook to a new situation must not require discarding a previously established mental model without going through the Correction process.
Severity: Blocking. Violation: a change discarding prior content while labeled Evolution must be relabeled Correction and re-justified.

### C-5xx — Knowledge Lifecycle (implements FL-5)

**C-510 — Settled Knowledge Gate**
A concept must not be referenced by other content, or presented as settled, until it satisfies the evidence (C-1xx) and definition (C-2xx) requirements above.
Primary: FL-5. Supporting: FL-1 (Evidence), FL-2 (Conceptual Integrity) — this rule's own gating condition is defined in terms of those two laws, making the cross-reference explicit rather than incidental.
Severity: Blocking. Violation: content relying on a not-yet-settled concept is flagged and withheld until the dependency is resolved.

### C-6xx — Traceability & Self-Application (implements FL-6)

**C-610 — Traceability Requirement**
Every recommendation must be able to state what principle supports it, what evidence supports that principle, and what assumptions this application makes.
Severity: Blocking. Violation: the recommendation is withheld from publication until all three can be answered.

**C-620 — Self-Application**
Every structural decision made about this handbook must itself be justifiable by the same principles the handbook teaches.
Severity: Advisory. Violation: the decision is revisited and re-justified, or reversed.

---

## Article IV — Interpretation

This Constitution defines rules. Their implementation belongs to Architecture. Their interpretation — what counts as a "primary source," how a dependency is disclosed, what qualifies as a mental model versus a principle — must always preserve the intent expressed by Vision.

Where a rule's application is ambiguous, the interpretation chosen is the one that minimizes contradiction with Vision. Each such interpretive decision is recorded where it occurs, so the same ambiguity is not re-argued from scratch every time it recurs.

Where more than one interpretation satisfies Vision equally, the interpretation that introduces fewer new concepts and fewer exceptions is preferred. This is itself an application of FL-2 (Conceptual Integrity) — a tie should be broken toward the reading that keeps the handbook's vocabulary smaller and more consistent, not the one that happens to be more convenient in the moment.

---

## Article V — Amendment Procedure

Amendment follows one of two paths, depending on tier:

**Amending a Foundational Law (Article II):**
1. Must be traceable to Vision — either a change already made to Vision itself, or a gap in Vision's coverage that the current wording fails to address.
2. May not be justified by convenience, a downstream document's current structure, or a single difficult case.
3. Must record: what changed, why, which Vision section supports it, and the previous wording. This record is permanent — appended to a change log, never overwritten.

**Amending or adding a Standing Rule (Article III):**
1. Must be traceable to an existing Foundational Law — it does not require a change to Vision.
2. A genuinely new category of concern that cannot be traced to any existing Foundational Law requires a Foundational Law amendment first (the heavier path above), not a new Standing Rule bolted onto an unrelated law.
3. Must record: what changed, why, which Foundational Law it implements, and (if amending) the previous wording.

This Constitution does not define who holds authority to approve either kind of amendment — that is an organizational, not a constitutional, question, and belongs in a governance document scoped to that purpose if one becomes necessary.

---

## Traceability Table

| Foundational Law | Vision Source | Implemented by |
|---|---|---|
| FL-1 Evidence | Design Principle 1 | C-110, C-120, C-130, C-140 |
| FL-2 Conceptual Integrity | Design Principle 3 | C-210, C-220 |
| FL-3 Structural Discipline | Design Principle 2, 5; Scope | C-310, C-320, C-330 |
| FL-4 Evolution over Replacement | Design Principle 6 | C-410, C-420 |
| FL-5 Gated Knowledge | Scope | C-510 |
| FL-6 Traceable Reasoning and Self-Application | Success Criteria; Core Belief | C-610, C-620 |

**Note:** this table is currently hand-maintained. Per Review 5, it should eventually be generated directly from each rule's own "Source" / "Implements" metadata rather than kept in sync by hand — this is flagged as a tooling requirement for the Spec/Plan stage, not solved here.

---

## Change Log: v1 → v2

1. Article II restructured: the flat 14-rule catalog is split into **Foundational Laws** (Article II, 6 broad "shall" statements, one per Vision Design Principle/Scope/Success Criteria/Core Belief grouping) and **Standing Rules** (Article III, the original 14 rules, renumbered underneath them)
2. Standing Rules renumbered by category with numeric gaps (C-1xx, C-2xx, ... C-6xx) to allow future insertion without renumbering
3. Added explicit **Severity** field (Blocking / Advisory) to every Standing Rule, replacing the previous uniform "remove" language
4. Added **Article IV — Interpretation**, addressing who resolves ambiguity (e.g. "what counts as a primary source") and how, without ceding that authority to Architecture by default
5. Amendment procedure (now Article V) split into two paths: amending a Foundational Law requires tracing to a Vision change; amending/adding a Standing Rule only requires tracing to an existing Foundational Law
6. Traceability Table simplified to Foundational-Law-level (Standing Rules already carry their own "Implements" reference inline); flagged as a candidate for auto-generation rather than hand-maintenance

## Change Log: v2 → v3

1. Relaxed "each Standing Rule implements exactly one Foundational Law" to "one primary law, with additional supporting laws where genuinely applicable" (Article I.3, Article III intro) — avoids forcing cross-cutting rules into an artificial single category
2. Applied the new primary/supporting model to a real existing rule, C-510, rather than leaving it purely theoretical
3. Added an Occam's Razor tie-breaker to Article IV: where multiple interpretations equally satisfy Vision, prefer the one introducing fewer new concepts and exceptions
4. **Explicitly deferred to Spec, not resolved here:** what exactly a "Blocking" severity blocks — publish, merge, promotion to Canonical, or review sign-off. This Constitution intentionally stays silent on that mechanism, since naming a specific gate (e.g. "Canonical") would import Architecture-level vocabulary into Constitution, which Article I already rules out.
