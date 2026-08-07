# Plan — Change Log History

This file holds the full revision history for `PLAN.md`. The Plan document itself keeps only its most recent Change Log entry — older entries move here once superseded, matching the pattern established in `architecture/ARCHITECTURE-CHANGELOG.md` and `spec/SPEC-CHANGELOG.md`.

---

## Change Log: v1 → v2

1. Phase 0's Glossary-seeding language tightened: "go straight to Canonical" → "seeded as Canonical because their governing definitions already exist" — avoids implying the Glossary entry itself establishes meaning, when it only records a meaning Architecture already established
2. Fixed a conflation in Section 3.4: the ordering rule mixed **Dependency** (availability — can this object exist yet) with **Governance** (workflow state — has this object cleared Review). Reworded so dependency ordering is stated purely in terms of the minimum lifecycle state required by Architecture and enforced through Spec, independent of which Governance Checklist step an item happens to be sitting in
3. Added **Section 4, Phase 1.5 — Process Validation**, between Phase 1 and Phase 2: a scheduled checkpoint to review the templates, checklist, and Glossary against real authoring experience — and route any findings to the correct upstream document as a Correction or Evolution — before Phase 2 scope is decided. Not previously present; Phase 2 depended directly on Phase 1 before this change
4. Phase 2's candidate corpus is now listed explicitly in the document (title + author for all eight works) instead of referencing "the eight works discussed earlier in this project's history" — the document must be self-contained and not depend on chat history a future reader won't have access to
5. Added **Section 6, Failure Path** — previously every phase had an acceptance gate but no defined behavior for what happens if a gate can't be met due to an upstream deficiency (as opposed to incomplete authoring work). Now stated once, generally, and cross-referenced from each phase's acceptance gate
6. Section numbers shifted throughout (Phase 2 is now Section 5, Non-Goals is now Section 7) to accommodate the two new sections; internal cross-references updated accordingly

## Change Log: v2 → v3

1. Removed remaining references to chat history ("corrected this session," "earlier this session") from Section 3.2's table and Section 4 — this document must read correctly for someone who opens it cold, with no access to the conversation that produced it
2. Section 3.3 reworded to a neutral, project-management register ("this inconsistency is scheduled for resolution rather than resolved inside this document") instead of first-person justification of why the author chose not to fix it inline — kept the underlying reasoning, shortened and depersonalized it
3. Renamed **Phase 1.5: Pipeline Retrospective → Process Validation** — "Retrospective" carries Scrum-specific connotations not used anywhere else in this document; "Process Validation" matches the register already established elsewhere (e.g. "stress-test the pipeline"); body text updated to match ("run a process validation" instead of "run a retrospective")
4. Removed a redundant clause in Section 6 (Failure Path): "work on that item pauses ... before Phase execution resumes on that item" collapsed into a single sentence
5. Section 3.4 and the archived v1→v2 log updated: "minimum lifecycle state Architecture requires for citation" → "required by Architecture and enforced through Spec" — Architecture defines the Draft/Canonical states, but Spec §6 is what actually operationalizes checking them; attributing the enforcement mechanism to Architecture alone was imprecise
6. Section 3.3's sequencing note now numbers `interface-review` as object #7 and `claude-md-interface-review` as #8, matching Section 3.4's tranche order exactly (previously said "#7a," which didn't match the numbering used two paragraphs later)
7. Section 3.2's flag for `claude-md-interface-review` changed from "resolve before authoring" to "Dependency gap identified; see Section 3.3" — the original wording contradicted 3.3, which had already scheduled the gap rather than leaving it open
8. Section 3.3's "Resolution:" label changed to "Planned sequencing:" — Plan schedules work, it doesn't resolve upstream inconsistencies itself
9. Section 4's "before a single object had reached Canonical" reworded to "during initial authoring, before the first tranche had completed"
10. Section 6 (Failure Path): "Constitution Article III/V" replaced with "Constitution's Amendment Procedure"
