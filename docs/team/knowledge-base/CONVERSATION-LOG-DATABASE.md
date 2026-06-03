# BMC Conversation Log Database

> **Append-only. Do not edit or delete existing entries.**
> This file is the permanent, full-history log of every team conversation.
> All agents read and write here. The schema evolves; see SCHEMA-EVOLUTION-LOG.md.

<!-- SCHEMA_VERSION: 1.0.0 -->
<!-- SCHEMA_EVOLVED: 2026-03-17 -->
<!-- TOTAL_SESSIONS: 1 -->
<!-- TOTAL_ENTRIES: 1 -->

---

## Active Schema (v1.0.0)

Each **Session** block groups all entries from one run or conversation.
Each **Entry** row captures one agent turn within that session.

```
### Session: YYYY-MM-DD-runN
**Initiated:** YYYY-MM-DD HH:MM:SS UTC
**Closed:**    YYYY-MM-DD HH:MM:SS UTC  (or `open`)
**Agents:**    Comma-separated roles
**Summary:**   ≤ 300-character plain-text description

| # | Timestamp           | Agent       | Type       | Content (≤ 400 chars, link for more) | Outcome          | Tags              |
|---|---------------------|-------------|------------|---------------------------------------|------------------|-------------------|
| 1 | YYYY-MM-DD HH:MM:SS | AgentRole   | CONCLUSION | ...                                   | ACCEPTED/PENDING | tag1, tag2        |
```

**Entry types:** `CONCLUSION` · `DECISION` · `PROPOSAL` · `FINDING` · `HANDOFF` · `QUESTION` · `ANSWER` · `ERROR` · `META`

**Outcome values:** `ACCEPTED` · `REJECTED` · `PENDING` · `SUPERSEDED`

**Schema evolution:** When a new field is needed, add it to the schema definition above,
increment `SCHEMA_VERSION`, and record the change in SCHEMA-EVOLUTION-LOG.md.
The new field is optional for all pre-existing entries.

---

## Conversation Log

### Session: 2026-03-17-run1
**Initiated:** 2026-03-17 05:36:49 UTC
**Closed:**    open
**Agents:**    Orchestrator, Live Comms, Knowledge Base
**Summary:**   Initialisation of the Universal Knowledge Base and Conversation Log Database systems for the BMC development team.

| # | Timestamp           | Agent          | Type       | Content                                                                                          | Outcome  | Tags                              |
|---|---------------------|----------------|------------|--------------------------------------------------------------------------------------------------|----------|-----------------------------------|
| 1 | 2026-03-17 05:36:49 | Orchestrator   | META       | Conversation Log Database created. Schema v1.0.0. Universal Knowledge Base system initialized.  | ACCEPTED | init, schema-v1.0.0, knowledge-base |
