# Principle: Information Hiding

* **Identity:** information-hiding
* **Type:** Principle
* **Status:** Draft

---

## Claim

Modules should hide design decisions that are likely to change behind stable interfaces.

---

## Evidence

* **Source:** `sources/parnas-1972.md`
  * **Location:** Section 5 (The Criteria), pp. 1056–1057
  * **Quote Boundary:** "every module in the second decomposition is characterized by its knowledge of a design decision which it hides from all others. Its interface or definition was chosen to reveal as little as possible about its inner workings."

---

## Boundary

This Principle defines module decomposition in terms of hiding design decisions that are likely to change. It does not prescribe implementation techniques, module size, code organization, or the specific software attributes produced by applying the principle.

---

## Related

* **Related Principles:** `deep-modules`
