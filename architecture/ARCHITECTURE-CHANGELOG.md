# Architecture — Change Log History

This file holds the full revision history for `ARCHITECTURE.md`. The Architecture document itself keeps only its most recent Change Log entry — older entries move here once superseded, so a reader opening Architecture to understand the current system isn't required to read through its entire history first.

---

## Change Log: v1 → v2

1. Added ADR-0001 "Alternatives Considered" (Book-centric vs. Knowledge-centric)
2. Split former Section 3 ("Core Domain Model") into Section 3 (Domain Objects, flat, no implied hierarchy) and Section 4 (Dependency Rule, pure relationship) — objects and their relationships are now independently revisable
3. Added Section 5, System Invariants — five explicit, always-true statements extracted from previously scattered rules
4. Added **Applicability** field to the Knowledge Object Schema (Section 7)
5. Added **Decision Log** step to the Governance pipeline, in both the full pipeline (8.1) and the Correction short path (8.2)
6. Added Section 11, Meta Principles — accepted as a concept, but explicitly classified as a Draft, unsourced View-level organizing lens rather than a Domain Object, to avoid violating the same Layer/Object distinction fixed in Sections 3–4
7. Section 10 (formerly Section 10, now Section 12) — noted explicitly as reusable for Spec Review; added rows for the new Section 5, 7, 8, and 11 decisions

## Change Log: v2 → v3 (Constitution alignment patch)

1. Section 1 (Purpose) updated to insert Constitution into the document hierarchy (Vision → Constitution → Architecture → Spec), previously missing entirely; added an explicit statement that this Architecture is binding to, and subordinate to, Constitution
2. ADR-0001 Rationale updated to note the decision has been checked against Constitution (adopted after the ADR) and found compliant
3. Section 5 renamed **System Invariants → Architectural Invariants**, with an explicit statement that these are not an independent source of authority — they are how this system enforces Constitution rules, not a parallel rule set
4. Each of the five invariants now carries an **Implements:** line mapping it to a specific Constitution Standing Rule (and Foundational Law): Invariant 1 → C-110/C-510, Invariant 2 → C-310, Invariant 3 → C-210, Invariant 4 → C-420
5. Invariant 5 (View is never a dependency target) is explicitly marked as having **no direct Constitution source** — Constitution does not legislate View-layer mechanics — rather than manufacturing a citation that doesn't exist. This mirrors the same honesty standard already applied to Meta Principles in Section 11
6. Section 9 and Section 12 (Traceability) updated to reference "Architectural Invariant" terminology and Constitution rule IDs instead of the old unsourced "Conceptual Integrity; all Design Principles collectively" framing
7. Section 12's row for Stable Core / Evolvable Edge re-sourced to Constitution FL-4, and the Decision Log row now cites Constitution Article IV (Interpretation) alongside Evidence First

## Change Log: v3 → v4 (ADR extraction)

1. ADR-0001 moved out of this document entirely, into its own file (`adr/ADR-0001-knowledge-system-over-book.md`). Architecture now opens directly with Purpose, preceded only by a one-line pointer to the ADR.
2. Rationale: Architecture describes what the system *is* (Domain Objects, Dependency Rule, Governance, Invariants); an ADR records *why* a specific design decision was made on a specific date, including the alternatives rejected. Keeping ADR-0001 embedded in Architecture blurred that boundary — a Practice-layer artifact (ADR, per Section 3's own Domain Object table) was living inside a document that is supposed to describe system structure, not decision history.
3. No content was lost — ADR-0001's Decision, Consequence, Rationale, and Alternatives Considered are preserved verbatim in the new standalone file, with cross-references added in both directions.
4. Future architecture-level decisions (e.g. adding a Domain Object, changing the Stable Core / Evolvable Edge boundary, altering the Governance pipeline) should be recorded as new ADRs rather than folded into Architecture's prose — Architecture is patched to reflect the *outcome*, and the ADR records the *reasoning*.

## Change Log: v4 → v5 (trim history; relocate Traceability table)

1. Removed all prior Change Log entries from `ARCHITECTURE.md` body; archived them here. `ARCHITECTURE.md` now retains only its current (most recent) Change Log entry.
2. Removed the full Section 12 Traceability table from `ARCHITECTURE.md`. Rationale: the table had grown into something closer to a Spec Review checklist (decision / principle / evidence / open assumption, refreshed as review activity progresses) rather than a description of the system itself — which is what Architecture is responsible for. The table's content is preserved below and will carry forward into the Spec document's Traceability Register when Spec is authored.
3. `ARCHITECTURE.md` Section 12 now states the traceability requirement in one sentence and points to Spec for the living register, rather than hosting the register itself.

### Archived: Section 12 Traceability Table (as of v4, prior to relocation)

Per Vision's Handbook-level Success Criterion, every architectural decision should be able to answer three questions. This table doubled as a reusable Architecture Fitness Function — the same three questions can be applied directly during Spec Review. This content is the seed for Spec's Traceability Register.

| Decision | Principle it supports | Evidence | Key assumption |
|---|---|---|---|
| Knowledge System over Book | Vision Core Belief; Conceptual Integrity | Parnas (Information Hiding), Ousterhout (Deep Modules) | Multiple output Views will actually be needed, not just one book |
| Dependency Rule (Sec. 4) | Evidence First; Continuous Evolution | Robert C. Martin, Clean Architecture | Principle-layer content genuinely changes slower than Technique-layer content |
| Architectural Invariants (Sec. 5) | Constitution C-110, C-210, C-310, C-420 (Invariants 1–4); Invariant 5 has no direct Constitution source, see Sec. 5 | Derived directly from Constitution Article III, mapped 1:1 or noted as unmapped | Four invariants mapping cleanly to Constitution is sufficient; more may surface once Spec/Plan stress-test the model |
| Stable Core / Evolvable Edge (Sec. 6) | Constitution FL-4 (Evolution over Replacement) | Derived from Sec. 4 — labeled as this handbook's own architectural synthesis | AI tooling churn will continue to outpace principle-level change |
| Applicability field (Sec. 7) | Separation of Fact and Interpretation | Common critique pattern of SOLID/DDD/Microservices literature | A single Applicability field is enough; some principles may need more nuance than one field allows |
| Decision Log (Sec. 8.1) | Constitution Article IV (Interpretation); Evidence First | Standard ADR practice | Contributors will actually take the time to log contested decisions rather than skip the step |
| Meta Principles (Sec. 11) | Conceptual Integrity (as organizing lens, not as sourced content) | None — explicitly unsourced editorial grouping | The four groupings will still make sense once more Principles are added; may need revision |

