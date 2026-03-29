# Architecture Decision Record

> Log every significant technical or design decision here.
> This file is **append-only** — never edit or remove past decisions.
> A decision is significant if a future session would benefit from knowing why it was made.

**Format for each entry:**

```
## Decision NNN — [Short title]
**Date**: YYYY-MM-DD
**Decision**: [What was decided, in one sentence]
**Rationale**: [Why this was the right choice for this project]
**Alternatives considered**: [What else was on the table]
**Trade-offs**: [What we gain, what we give up]

**Guardrails Alignment**:
- **Privacy & IP**: [How does this decision protect student data and clarify ownership?]
- **Disclosure**: [How will this choice be disclosed to users/stakeholders?]
- **Responsibility**: [Who is the human responsible for this decision's impact?]
- **Bias & Trust**: [What measures mitigate bias in this specific choice?]
- **Values**: [Which core Minerva value does this align with?]
```

---

## Decision 001 — Vanilla HTML/CSS/JS, no framework

**Date**: [YYYY-MM-DD]
**Decision**: Use plain HTML, CSS, and JavaScript with no build step and no framework.
**Rationale**: GitHub Pages hosts static files directly. No framework means no build pipeline, no dependencies to update, no abstraction between the code and the browser. The project remains readable and modifiable by anyone with basic web knowledge, which aligns with the learning-orientation principle of clarity over cleverness.
**Alternatives considered**: React, Vue, Svelte — all require a build step or CDN dependency; Astro — adds complexity for a single-page app
**Trade-offs**: We lose component reuse patterns and reactive state management. We gain zero setup friction, full control over output, and a codebase that doesn't rot when npm packages break.

## Decision 002 — Ethical AI & Data Privacy Guardrails

**Date**: [YYYY-MM-DD]
**Decision**: Adoption of Minerva University's AI Guardrails for all project development and deployment.
**Rationale**: To protect data privacy (especially student PII), ensure intellectual property integrity, and maintain human-centered learning. This project prioritizes human agency and accountability, treating AI as a "thinking partner" rather than a substitute.
**Specific Guardrails for this Project**:
1. **No Sensitive Data**: The app will not store or process real student records or PII.
2. **Human-in-the-Loop**: All AI-suggested code and content are reviewed by the human developer before commit.
3. **Mandatory Disclosure**: AI use is logged in `SCRATCHPAD.md`.
**Trade-offs**: Development may be slower due to mandatory human review and documentation overhead, but the resulting system is more ethical, secure, and aligned with institutional values.

## Decision 003 — Supabase for Backend Services (Auth, DB, Logic)

**Date**: 2026-03-29
**Decision**: Use Supabase as the backend-as-a-service (BaaS) provider for Auth, PostgreSQL Database, and Edge Functions.
**Rationale**: To meet the project requirements for a "production-ready" app (verified auth, relational data, and logic like matching/AI moderation) while staying within the $0 cost constraint and static hosting limitation of GitHub Pages. Supabase provides a robust, PostgreSQL-backed platform that can be interacted with directly from a Vanilla JS frontend via their client library.
**Alternatives considered**: Firebase (proprietary, NoSQL might be less ideal for complex matching), custom Node.js server (requires separate hosting and cost), and local storage only (cannot handle verified peer-to-peer connection).
**Trade-offs**: We introduce a dependency on an external service provider and will need to manage API keys securely within the frontend (though Supabase's Row-Level Security mitigates this risk).

**Guardrails Alignment**:
- **Privacy & IP**: Supabase allows for Row-Level Security (RLS) policies to ensure that users can only access their own data, aligning with the "Zero-Trust" privacy guardrail.
- **Disclosure**: The use of Supabase will be transparently documented in the project's technical architecture.
- **Responsibility**: The developer is responsible for configuring RLS policies correctly to prevent data leakage.
- **Bias & Trust**: Using a relational database (PostgreSQL) ensures data integrity and clear relationships, making the matching algorithm more predictable and less prone to "black-box" biases.
- **Values**: Aligns with "Clarity over cleverness" by using industry-standard SQL and Auth patterns rather than custom, potentially less secure, implementations.
