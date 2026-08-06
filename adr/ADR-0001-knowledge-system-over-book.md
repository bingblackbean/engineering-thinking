# ADR-0001: This handbook is architected as a Knowledge System, not a book

**Status:** Accepted

**Decision:** Architecture SHALL model the handbook as a Knowledge System, not as a book. A book, a PDF, a website, an AI knowledge base, an MCP server, and an agent's memory are all *Views* projected from one underlying knowledge model. The knowledge model is the deep module; every rendered form is a thin interface to it.

**Consequence:** If we had architected this as a book, architecture would just be a table-of-contents design, and every new output format (MCP server, agent memory, website) would require re-deriving structure from scratch. By architecting a knowledge system instead, new Views become an implementation detail of the Application layer — they don't touch the Stable Core. See Architecture, Sections 3–9, for the resulting domain model, dependency rule, and governance process.

**Rationale:** This follows directly from Vision's Core Belief — "the handbook must be built using the same principles it teaches" — applied specifically to Information Hiding (Parnas) and Deep Modules (Ousterhout). This decision has since been checked against Constitution (adopted after this ADR was first written) and found compliant: Alternative B keeps knowledge content isolated from rendering concerns, which is what allows Constitution's rules to be enforced uniformly across every View rather than re-litigated per output format.

**Alternatives Considered:**

- *Alternative A — Book-centric architecture.* Organize the project around a table of contents; treat chapters as the primary structural unit. **Rejected because:** every new output format (site, MCP server, agent memory) would require re-deriving its own structure from the book's chapter order, and chapter order is a presentation decision, not a knowledge dependency. This would also make it impossible to enforce a single Dependency Rule across formats, since each format could reorganize freely.
- *Alternative B — Knowledge-centric architecture.* Organize the project around typed knowledge objects (Source, Evidence, Principle, ...) with one shared dependency rule; treat every output format, including the book, as a View over that model. **Accepted because:** it isolates the fast-changing parts (Technique, AI Application, Views) from the slow-changing parts (Source, Evidence, Principle), per Architecture's Stable Core / Evolvable Edge split (Section 6).

---

**Established:** Architecture (see Architecture, Section 1, which is founded on this decision)

