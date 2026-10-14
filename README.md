# gaia-memory

**Status:** Proposed architecture component — not implemented.

**Domain:** Short-Term and Long-Term Memory

**Visibility:** Internal

**Source:** [GAIA Super-Intelligent Application Architecture Report](https://github.com/KyleAlexanderSteen/GAIA-Documentation) (2026-10-13)

**Traceability:** GAIA-Documentation issues #1–#6

## Purpose
Manages short-term (session) and long-term (persistent) memory using vector and relational stores. Handles consolidation, retrieval, forgetting policies, and per-user namespaces.

## Initial Directory Structure (proposed)
```
gaia-memory/
├── src/
│   ├── short-term/     # Redis-backed session context
│   ├── long-term/      # Vector DB + metadata
│   ├── consolidation/  # Summarization and compression
│   ├── retrieval/      # Semantic and structured search
│   └── policies/       # Retention, decay, GDPR deletion
├── README.md
└── tests/
```

## Proposed Interfaces and Dependencies
- Endpoints: POST /v1/memory/store, /v1/memory/search; GET /v1/memory/session/{id}; DELETE /v1/memory/user/{id}
- Depends on: gaia-core, gaia-brain (embeddings), gaia-security
- Called by: gaia-agent-runtime, gaia-reasoning, gaia-orchestrator
- Stores: Redis, Vector DB, PostgreSQL

## Security and Access-Control Requirements
- Per-user/organization namespace isolation.
- Deletion must propagate (see GAIA-Documentation #4).
- No secrets stored.

## Tests and Acceptance Criteria
- [ ] Store/search stubs with provenance metadata.
- [ ] Deletion workflow placeholder.
- [ ] Tenant isolation enforced in design.
- Linked to GAIA-Documentation #1, #3, #4.

## Development Instructions
Scaffolding only. Do not claim live vector stores or consolidation engines. Coordinate provenance with #4.

**Unresolved:** Exact vector backend, provenance schema, deletion propagation rules.
