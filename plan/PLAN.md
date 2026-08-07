# Plan (v4)

*This document operates under Vision, Constitution, Architecture, and Spec. It sequences the deliverables Spec defined — it does not redefine what they are.*

```
Vision           — why this system exists
     ↓
Constitution     — what must always be true
     ↓
Architecture     — what the system is, and how it satisfies those rules
     ↓
Spec             — what to build, concretely
     ↓
Plan (this doc)  — in what order, and when
     ↓
Knowledge / Book — the content itself
```

**Definition Boundary:** terms used in this Plan inherit their meaning from Architecture, Glossary, and Spec. This Plan introduces no new Domain Object definitions and no new templates. Where this Plan appears to describe *what* something is rather than *when* it gets built, that is a drafting error, not a deliberate addition — flag it for Correction.

---

## 1. Purpose

Spec defined six templates and left their instances unwritten (Spec §7, Non-Goals: "author the actual content library ... is Plan's responsibility"). Spec also defined D-2 (Glossary bootstrap) as a deliverable but did not schedule it. This Plan does two things: sequences the Glossary bootstrap and the first tranche of real knowledge content, and states the acceptance gate each phase must clear before the next one starts.

This Plan does not select which of the eventually many Sources this handbook will cover in full — it selects a **first tranche**, deliberately small, chosen to stress-test the templates and Governance Pipeline against real content before committing to a larger backlog.

---

## 2. Phase 0 — Glossary Bootstrap (blocks everything else)

Per Architecture Invariant 3 / Constitution C-210 (Single Definition Rule), no Principle, Mental Model, Practice, Technique, or AI Application entry can reach Canonical status until its terms exist in the Glossary (Constitution C-510, Settled Knowledge Gate). The Glossary currently has zero entries. This is a hard blocker, not a parallel task.

**Phase 0 deliverable:** `glossary/GLOSSARY.md`, seeded with:
- The eight Domain Object type names themselves (Source, Evidence, Principle, Mental Model, Practice, Technique, AI Application, View) are seeded as Canonical because their governing definitions already exist in Architecture §3 — the Glossary entry doesn't establish their meaning, it records a meaning Architecture already established
- The two lifecycle states (Draft, Canonical) — same treatment, governing definition already exists in Architecture §8.3
- Nothing else yet. Concept-level Glossary entries (e.g. "Information Hiding," "Deep Module") are added as a side effect of Phase 1, not pre-populated speculatively

**Acceptance gate:** Glossary file exists, contains exactly the above, every entry cites its Architecture source. Phase 1 cannot begin until this gate clears. If it cannot be met, see Section 6, Failure Path.

---

## 3. Phase 1 — First Tranche (proves the Governance Pipeline end-to-end)

### 3.1 Selection criteria

The first tranche is chosen by three criteria, in priority order:
1. **Already load-bearing** — content this handbook has already implicitly relied on elsewhere (e.g. Spec's worked Mental Model example cites `information-hiding` and `deep-modules` as if they exist)
2. **Single-source, low ambiguity** — principles with one clear primary source and a well-documented original context, to stress-test the Governance Pipeline itself rather than stress-test source research
3. **Cross-Source pressure-test** — at least one Mental Model that must genuinely synthesize two different Sources, to confirm the "many-to-one" exception (Architecture §3) actually works in practice, not just on paper

### 3.2 Tranche contents

| # | Object | Type | Primary Source | Why this one, now |
|---|---|---|---|---|
| 1 | `ousterhout-2018` | Source | — | Already referenced in Spec's worked Source example; needs to actually exist as a real entry, not just an example |
| 2 | `parnas-1972` | Source | — | Needed before `information-hiding` can cite it; classic, single-source, low ambiguity |
| 3 | `information-hiding` | Principle | Parnas, 1972 | Already cited by Spec's worked Mental Model example; criterion 1 |
| 4 | `deep-modules` | Principle | Ousterhout, 2018 | Same — Spec explicitly flagged this file as missing (Spec §4.2, corrected in Spec) |
| 5 | `reduce-cognitive-load` | Mental Model | synthesizes #3 + #4 | This exact entry already exists as a worked example *inside Spec* — Phase 1 promotes it from "Spec's illustration" to "real Draft entry," which is a meaningfully different status (Spec's copy is not Canonical and never will be; it's illustrative prose, not a governed object) |
| 6 | `architecture-decision-record` | Practice | — | Also already a worked example in Spec (§4.4); same promotion logic as #5 |
| 7 | `claude-md-interface-review` | Technique | implements #6... | **Dependency gap identified; see Section 3.3** |

Deliberately excluded from Phase 1: any AI Application entry. Spec §4.6 already committed to not fabricating one; Phase 1 doesn't reverse that. AI Application authorship is Phase 2 at the earliest, and only once a real agent session exists to document.

### 3.3 A problem this Plan surfaces, doesn't yet resolve

Spec's worked example for the Technique template (§4.5, `claude-md-interface-review`) states: *"Implements: architecture-decision-record is unrelated — implements Practice 'interface-review' instead."* But no Practice named `interface-review` has ever been defined — not in Spec, not anywhere. This is the same defect class as the `deep-modules` cross-reference previously corrected during Spec review: a worked example referencing something that doesn't exist yet.

This inconsistency is scheduled for resolution rather than resolved inside this document. Inventing the `interface-review` Practice here to make the reference true would manufacture a citation rather than establish one with real Evidence — inconsistent with how this project has handled every other such gap. Re-opening Spec mid-Plan is also avoided, to keep Plan a sequencing document rather than a second Spec-editing pass.

**This is a Scope Evolution, not an ordinary tranche selection, and is recorded as one explicitly** (Constitution C-410: this is an Evolution — nothing existing is being changed, a new object is being added because authoring exposed a real gap Spec's own worked example presupposed but never defined). Objects #1–6 were selected from content this handbook already implicitly depended on (Section 3.1, criterion 1); `interface-review` is different — it did not exist as backlog before this Plan identified the gap, and its addition expands what Phase 1 authors beyond what Spec's templates alone implied. Recording this here, rather than silently listing it as object #7 without comment, is what keeps this an accountable Evolution rather than Plan quietly expanding its own scope.

**Planned sequencing:** `interface-review` is added to Phase 1 as object #7 (Practice, authored before `claude-md-interface-review` can be authored as #8). This is reflected in the tranche order below.

### 3.4 Revised tranche order (dependency-ordered)

```
1. ousterhout-2018             (Source)
2. parnas-1972                  (Source)
3. information-hiding            (Principle    — depends on 2)
4. deep-modules                  (Principle    — depends on 1)
5. reduce-cognitive-load         (Mental Model — depends on 3, 4)
6. architecture-decision-record  (Practice)
7. interface-review               (Practice)  — newly identified, see 3.3
8. claude-md-interface-review     (Technique  — depends on 7)
```

Each item is authored, then run through the Spec §6 Governance Checklist (full Governance Pipeline), in this order. Ordering above is a **dependency** relationship (availability), not a **governance** relationship (workflow state) — the two are separate per Architecture: a dependent object may enter authoring only after its dependency has reached the minimum lifecycle state required by Architecture and enforced through Spec (Architecture §8.3 defines Draft/Canonical; Spec §6 operationalizes the check — as required by the current Architecture and Spec, Canonical status for anything cited as Evidence or as a Related Principle). Governance steps like Review or Decision Log are a separate axis entirely; two items may sit in Review simultaneously regardless of dependency order, as long as neither cites the other before the cited item is actually Canonical.

**Acceptance gate for Phase 1 as a whole:** all 8 items reach Canonical status, the Glossary has grown to include `information-hiding`, `deep-modules`, `reduce-cognitive-load`, `architecture-decision-record`, and `interface-review` as real entries (not just Architecture's object-type names from Phase 0), and the Traceability Register (Spec §5) has a new row added for this Plan's own existence. If this gate cannot be met, see Section 6, Failure Path.

---

## 4. Phase 1.5 — Process Validation (before Phase 2 is scoped)

Architecture, Constitution, and Spec are, until now, untested against real authored content — Phase 1 is their first real exercise. Phase 1 already surfaced two cases of the same defect class (Section 3.3's `interface-review` gap, and the `deep-modules` cross-reference corrected in Spec) during initial authoring, before the first tranche had completed. That is a signal worth checking deliberately, not just patching item by item as it recurs.

Once Phase 1's acceptance gate clears, and before Phase 2 selects any real backlog, validate whether Phase 1 surfaced any Corrections or Evolutions needed against Constitution, Architecture, or Spec — informed by the actual experience of authoring all 8 items, including the two defects already found in Section 3.3.

Findings are routed to whichever upstream document actually owns them — Spec for template/checklist issues, Architecture for domain model issues, Constitution for rule issues — as a Correction or Evolution (Constitution C-410), following the same discipline used everywhere else in this project.

**Phase 2 does not begin until this retrospective is complete** and any Corrections/Evolutions it raised have either been resolved or explicitly deferred with stated reasoning.

---

## 5. Phase 2 — Scope Decision (not yet started)

Phase 2 is where the eventual book's real backlog gets chosen. Initial corpus is selected according to selection criteria established during Phase 2 scoping itself — not fixed here. See Appendix A for an example corpus considered while this Plan was being drafted; it is illustrative, not binding, and Phase 2 may depart from it entirely without requiring a change to this section.

Organized by capability (the mental models and principles these works establish) rather than by book — i.e., a reader-facing chapter may draw on several sources at once, the same way `reduce-cognitive-load` (Phase 1) already synthesizes two.

This Plan does not sequence Phase 2 yet. Doing so before Phase 1 has actually cleared the Governance Pipeline once, end-to-end, and before Phase 1.5's validation has run, would be sequencing work on top of an unproven Governance Pipeline — the same mistake Spec's D-6 was designed to avoid at the template level, one level up. Phase 2 is scoped once Phase 1.5 concludes and whatever friction it surfaced has been addressed.

---

## 6. Failure Path

Every phase above has an acceptance gate. None of them describe what happens if a gate cannot be met. This section applies to all phases uniformly:

**If a Phase's acceptance gate cannot be met because of a deficiency in Constitution, Architecture, or Spec** — not because the authoring work itself is incomplete, but because the upstream document turns out to be wrong, ambiguous, or missing something authoring revealed — the affected work is dependent on that upstream Correction or Evolution being completed, or explicitly deferred with stated reasoning, raised through the appropriate upstream governance process (Constitution's Amendment Procedure, Architecture's own Governance Pipeline, or Spec's Governance Checklist, as applicable). Work with no such dependency is unaffected.

This is what keeps Plan from quietly working around a broken upstream document instead of fixing it — the same discipline Section 3.3 already applied once, made explicit here as a standing rule for every phase, not a one-off judgment call.

---

---

## Appendix A — Example Corpus (non-normative)

Listed here for reference only; this appendix carries no sequencing authority and changing it is not a Plan revision in the sense Constitution C-410 cares about (it changes no dependency, no phase, no acceptance gate). Considered while this Plan was being drafted:

- *A Philosophy of Software Design* — John Ousterhout
- *Domain-Driven Design* — Eric Evans
- *The Pragmatic Programmer* — David Thomas & Andrew Hunt
- *The Design of Design* — Frederick P. Brooks Jr.
- *Clean Architecture* — Robert C. Martin
- *Design Patterns* — Gamma, Helm, Johnson, Vlissides
- *Refactoring* — Martin Fowler
- *Team Topologies* — Matthew Skelton & Manuel Pais

---

## 7. Non-Goals

This Plan deliberately does not:
- Select the full content backlog beyond Phase 1's eight items — that's Phase 2, explicitly not started (Section 5), and gated behind Phase 1.5's validation (Section 4)
- Fix the `interface-review` gap by silently inventing content for it — Section 3.3 names the gap and schedules it as real authoring work, not a shortcut
- Re-open Spec's templates or Architecture's domain model directly — if Phase 1 authoring surfaces a template that doesn't fit, that's a Correction or Evolution at the Spec or Architecture layer, raised through Phase 1.5 or the Failure Path (Section 6), logged there, not patched around here
- Assign individual contributors or dates — this Plan sequences *dependency order*, not a calendar; calendar scheduling is an organizational concern the same way Approval authority was (Spec §6, Constitution Article V)

---

## Change Log: v3 → v4

1. **Section 3.3 reframed as a Scope Evolution, made explicit:** adding `interface-review` to the backlog is not an ordinary tranche selection like objects #1–6 (which were already implicitly load-bearing elsewhere) — it's new backlog Plan itself introduced to patch a gap in Spec's own worked example. This is now stated directly as a Constitution C-410 Evolution, rather than presented as if it were routine sequencing
2. **Section 6 (Failure Path) restated as a dependency constraint, not an execution instruction:** "execution ... is suspended" / "may continue in parallel" replaced with "the affected work is dependent on ... being completed" / "work with no such dependency is unaffected" — Plan describes what depends on what, not what to actively do about it
3. Section 4 (Process Validation) trimmed from four specific investigative questions to one general validation statement — the four questions started to look like Plan designing Spec's own review process, which isn't Plan's role
4. Section 4's closing sentence ("They are not patched informally inside Plan") removed as redundant with the preceding sentence already stating findings are routed upstream
5. Section 5 (Phase 2): the eight-book corpus is no longer stated as the corpus itself — replaced with a reference to selection criteria established during Phase 2. The actual list moved to a new, explicitly non-normative **Appendix A**, so revising or replacing a book no longer reads as a sequencing change to Section 5
6. Removed Change Log entry documenting the prior version's own changelog-archiving housekeeping — Change Log should record document content changes, not meta-commentary about where changelog history lives
7. Removed "currently" from Section 3.4's dependency description — a Plan shouldn't describe today's Architecture/Spec rules as "current" in a way that quietly dates the document as those rules evolve
8. Standardized informal lowercase "pipeline" references to **Governance Pipeline** throughout (Sections 1, 3, 5, 6) — matching Architecture's concept precisely, and kept distinct from **Governance Checklist** (Spec's operationalization) and **Process Validation** (this Plan's own Phase 1.5), which are different concepts, not synonyms

Full revision history: see `plan/PLAN-CHANGELOG.md`.
