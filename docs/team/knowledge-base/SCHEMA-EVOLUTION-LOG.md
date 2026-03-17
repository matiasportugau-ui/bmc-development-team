# BMC Knowledge Base — Schema Evolution Log

> Append-only log of every structural change to the Knowledge Base system.
> Covers: CONVERSATION-LOG-DATABASE.md schema, UNIVERSAL-KNOWLEDGE-BASE.md schema and domains.

---

## Format

```
### Change #N — YYYY-MM-DD — vX.Y.Z
**Type:** field-add | field-rename | field-remove | domain-add | domain-rename | schema-restructure
**Author:** AgentRole
**Reason:** ≤ 200 chars
**Files affected:** list
**Backward compatible:** Yes / No
**Details:** Optional free-text
```

---

## Change History

### Change #1 — 2026-03-17 — Conversation Log Database v1.0.0
**Type:** schema-restructure (initial creation)
**Author:** Knowledge Base
**Reason:** Initial schema for the Conversation Log Database. Registers all team conversations with session grouping, typed entries, and outcome tracking.
**Files affected:** `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md`
**Backward compatible:** Yes (new file)
**Details:**
Session block fields: Initiated, Closed, Agents, Summary.
Entry row fields: `#`, Timestamp, Agent, Type, Content, Outcome, Tags.
Entry types: CONCLUSION · DECISION · PROPOSAL · FINDING · HANDOFF · QUESTION · ANSWER · ERROR · META.
Outcome values: ACCEPTED · REJECTED · PENDING · SUPERSEDED.

---

### Change #2 — 2026-03-17 — Universal Knowledge Base v1.0.0
**Type:** schema-restructure (initial creation)
**Author:** Knowledge Base
**Reason:** Initial schema for the Universal Knowledge Base. Organises distilled team knowledge by domain with versioning and confidence tracking.
**Files affected:** `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md`
**Backward compatible:** Yes (new file)
**Details:**
Entry fields: `#`, Date, Source, Confidence, Status, Content, Tags, Supersedes.
Confidence levels: HIGH · MEDIUM · LOW.
Status values: ACTIVE · SUPERSEDED · UNDER_REVIEW.
Initial domains: Team Structure & Roles, Communication & Logging Protocol, Project State & Synchronization, Knowledge Base Operations, Skills Registry.
Version semantics: PATCH = new entries; MINOR = new domain; MAJOR = structural restructuring.

---

<!-- Future changes: append a new "### Change #N" block above this line. -->
