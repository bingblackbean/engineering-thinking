# Glossary (v3)

*This document operates under Constitution and Architecture. It records the authoritative terminology used across the knowledge system, satisfying Constitution C-210 (Single Definition Rule) and FL-2 (Conceptual Integrity). Definitions are derived from their governing documents and maintained here as the canonical terminology layer.*

---

## Domain Object Types

### Source
* **Definition:** The original artifact of record — a book, paper, talk, RFC, or standard.
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Provides the original artifact from which Principles are extracted and Evidence is recorded. Never interprets or explains.

### Evidence
* **Definition:** A specific citation, page/chapter reference, or quote boundary that proves a Principle traces to a Source.
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Represents supporting proof that connects a Principle to its Source. It is supporting information attached to knowledge entries, not an independently authored knowledge object. Never produces an opinion.

### Principle
* **Definition:** A statement of what an original author actually claimed in their primary work.
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Must be traceable to primary Evidence. Never mixes in modern interpretation.

### Mental Model
* **Definition:** A reusable way of thinking synthesized from one or more Principles (e.g., "Reduce Cognitive Load" synthesizing Information Hiding + Deep Modules).
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Explicitly identified as a synthesis rather than a direct claim from a single Source. Must maintain a traceable path back to at least one Principle.

### Practice
* **Definition:** A repeatable engineering activity independent of any specific tool or product (e.g., Architecture Decision Records, Refactoring, Event Storming).
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Represents a repeatable engineering activity that operationalizes Principles or Mental Models. Must not be named after or restricted to a specific product or vendor.

### Technique
* **Definition:** A concrete, tool-specific application of a Practice (e.g., `CLAUDE.md` instructions, prompt templates, tool configuration).
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Implements a Practice through a concrete tool, workflow, or configuration. It does not establish independent principles or claims, and its relationship to knowledge is through the Practice it implements rather than directly representing a Source.

### AI Application
* **Definition:** The outer consumer of the knowledge system, representing an interactive agent, assistant, or AI-enabled workflow.
* **Governing Definition:** Architecture §3
* **Status:** Canonical
* **Notes:** Consumes Techniques or Views but is never treated as the primary source of truth. Examples include coding assistants, autonomous agents, and MCP-based systems.

### View
* **Definition:** A rendering or projection of the knowledge system for a specific consumption context (e.g., book, website, MCP server knowledge base, agent memory).
* **Governing Definition:** Architecture §3, §9
* **Status:** Canonical
* **Notes:** Operates outside authored knowledge dependencies. It may read from any layer but does not create dependency relationships.

---

## Lifecycle States

### Draft
* **Definition:** The lifecycle state of a knowledge entry that is under development and has not yet satisfied the conditions required for trusted citation.
* **Governing Definition:** Architecture §8.3
* **Status:** Canonical
* **Notes:** May exist in the system and be discussed, but cannot be cited as settled knowledge or depended upon by Canonical entries (Constitution C-510).

### Canonical
* **Definition:** The lifecycle state of a knowledge entry that has completed the required governance process defined by the applicable governing documents and is trusted for citation across the system.
* **Governing Definition:** Architecture §8.3
* **Status:** Canonical
* **Notes:** The specific governance process required to reach this state is defined by the applicable governing documents.

---

## Change Log: v2 → v3

1. **Clarified Terminology Authority:** Updated Introduction to specify Glossary as the *canonical terminology layer* to satisfy Constitution C-210 without ambiguities.
2. **Refined Core Object Relationships:**
   - **Source Notes:** Clarified that Principles are extracted and Evidence is recorded from Sources.
   - **Evidence Notes:** Explicitly designated Evidence as supporting information *attached to knowledge entries*.
   - **Principle Definition:** Broadened scope from software design to author claims in their primary work.
   - **Mental Model Notes:** Reframed synthesis identification to be model-agnostic rather than handbook-bound.
   - **Practice Notes:** Restored operationalization relationship ("operationalizes Principles or Mental Models").
   - **Technique Notes:** Explicitly constrained Techniques from establishing independent principles or claims.
3. **Vendor Neutrality & Deprecation Resilience:** Replaced branded examples in `AI Application` with functional categories (coding assistants, autonomous agents, MCP-based systems).
4. **Dependency Precision:** Clarified that `View` operates outside authored knowledge dependencies.
5. **Governance State Precision:** Refined `Canonical` lifecycle definition to emphasize completion of required governance processes defined in governing documents.
