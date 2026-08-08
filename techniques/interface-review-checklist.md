# Technique: Interface Review Checklist

* **Identity:** interface-review-checklist
* **Type:** Technique
* **Status:** Draft

---

## Procedure

1. **Identify Module Interface Boundary**: Locate public signatures, exposed classes, endpoints, or functions exposed to consumers.
2. **Examine Encapsulated Complexity**: Identify internal design decisions, state management logic, and helper structures residing behind the boundary.
3. **Assess Interface Simplicity**: Evaluate whether the interface provides substantial functionality without exposing unnecessary implementation complexity.
4. **Inspect Leakage Points**: Check whether internal types, vendor-specific errors, or volatile implementation details are exposed to consumers.
5. **Record Findings**: Document identified leakage, unnecessary exposure, and any resulting refactoring actions.

---

## Foundations & Mapping

* **Implements Practices:**
  * `interface-review`: Provides a concrete, step-by-step inspection procedure for conducting interface reviews.

---

## Usage Format

This Technique defines a procedural execution format. It can be instantiated as a Markdown checklist within pull request templates, a peer review guide, or a manual inspection log.

---

## Boundary

This Technique defines a concrete, repeatable procedure for conducting interface reviews. It does not formulate underlying principles, define generic engineering practices, or mandate automated static analysis tooling.

---

## Related

* **Related Practices:** `interface-review`

