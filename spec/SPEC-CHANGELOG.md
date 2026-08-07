# Spec — Change Log History

This file holds the full revision history for `SPEC.md`. The Spec document itself keeps only its most recent Change Log entry — older entries move here once superseded, matching the pattern established in `architecture/ARCHITECTURE-CHANGELOG.md`.

---

## Change Log: v1 → v2

1. D-6 wording tightened: "one worked example per template" → "one worked example per *authored* Domain Object template" — the original phrasing risked implying all 8 Architecture Domain Object types get a template, when only 6 are authored content (Evidence and View are deliberately excluded, per Section 3's notes)
2. Added a **Definition Boundary** statement to Section 1: this Spec inherits all terms from Architecture/Glossary and introduces no new Domain Object definitions, to prevent Spec from gradually accumulating a second, parallel vocabulary as it grows
3. Added one sentence to Section 6 (Governance Checklist) clarifying that Approval authority is external to this Spec, consistent with Constitution Article V — added so a new contributor doesn't wonder who "Approve" refers to
4. No changes made to the Repository Skeleton (Section 3) or Source Template (Section 4.1) — a review round flagged both as apparently incomplete, but this was due to code-block formatting being stripped in a copy/paste, not an actual gap; verified against source file, both already correct as written
