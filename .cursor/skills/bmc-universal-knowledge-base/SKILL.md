---
name: bmc-universal-knowledge-base
description: >
  Manages the BMC team's permanent memory: the Conversation Log Database
  (full history of every agent conversation) and the Universal Knowledge Base
  (distilled universal truth nourished by agent conclusions). Governs how
  agents read/write both systems, how the schema auto-evolves, and how
  knowledge is promoted from raw log entries to confirmed universal truths.
  Use when any agent needs to record a conversation, extract a conclusion,
  query team memory, or evolve the knowledge schema.
---

# BMC Universal Knowledge Base

**Before working:** Read `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md` (relevant domains) and the latest entries of `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md`.

The **Universal Knowledge Base** system gives the BMC team two complementary, permanent memory layers:

1. **Conversation Log Database** — append-only, full-history record of every session.
2. **Universal Knowledge Base** — distilled, domain-organised source of all team truth.

---

## When to Use

- Any agent needs to **record** a conversation turn, decision, or finding.
- Any agent needs to **query** past conversations or confirmed knowledge.
- An agent has a **confirmed conclusion** ready to be added to the universal truth.
- The team needs to **evolve** the schema or add a new knowledge domain.
- User says: "update knowledge base", "add to team memory", "record conclusion",
  "what does the team know about X", "log this conversation", "base de conocimiento",
  "memoria del equipo", "verdad universal", "log de conversaciones".

---

## Core Concepts

### 1. Conversation Log Database

File: `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md`

- **Append-only, never reset.** Unlike LIVE-LOG-CENTER.md (which is reset after each run), the Conversation Log Database keeps ALL sessions forever.
- Organised in **Session blocks** (one per run or conversation).
- Each entry has: `#`, Timestamp, Agent, Type, Content, Outcome, Tags.
- **Entry types:** `CONCLUSION` · `DECISION` · `PROPOSAL` · `FINDING` · `HANDOFF` · `QUESTION` · `ANSWER` · `ERROR` · `META`
- **Outcome values:** `ACCEPTED` · `REJECTED` · `PENDING` · `SUPERSEDED`

### 2. Universal Knowledge Base

File: `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md`

- The **universal source of all truth** for the team.
- Organised by **knowledge domains** (automatically created as needed).
- Each entry has: `#`, Date, Source, Confidence, Status, Content, Tags, Supersedes.
- **Confidence:** `HIGH` (verified by multiple agents or runs) · `MEDIUM` (single confirmed run) · `LOW` (hypothesis not yet verified).
- **Status:** `ACTIVE` · `SUPERSEDED` · `UNDER_REVIEW`
- When reality contradicts an entry: mark it `SUPERSEDED`, add corrected entry.

### 3. Schema Evolution

File: `docs/team/knowledge-base/SCHEMA-EVOLUTION-LOG.md`

- Every structural change to either file is recorded here.
- Version metadata at the top of each file (`<!-- KB_VERSION: x.y.z -->`).
- **Versioning:** PATCH = new entry; MINOR = new domain or field; MAJOR = restructuring.

---

## Workflow

### Logging a Conversation (every agent, every run)

1. Open `CONVERSATION-LOG-DATABASE.md`.
2. Find the current session block (match by date and run number).
   - If none exists, create a new Session block at the bottom of the log (see template below).
3. Append your entry row with the next sequential `#`.
4. Keep Content ≤ 400 chars. Link to artifact for longer payloads.

**New Session template:**

```markdown
### Session: YYYY-MM-DD-runN
**Initiated:** YYYY-MM-DD HH:MM:SS UTC
**Closed:**    open
**Agents:**    Role1, Role2, …
**Summary:**   ≤ 300-char description.

| # | Timestamp           | Agent    | Type    | Content | Outcome  | Tags |
|---|---------------------|----------|---------|---------|----------|------|
```

### Closing a Session

When Orchestrator emits the run-complete BROADCAST:

1. Set `**Closed:**` to the current timestamp in the session block.
2. Update `<!-- TOTAL_SESSIONS: N -->` and `<!-- TOTAL_ENTRIES: N -->` metadata.
3. Optionally add a CONCLUSION entry summarising the session outcomes.

### Promoting a Conclusion to Universal Knowledge

When a conclusion has outcome `ACCEPTED` (or appears confirmed across multiple runs):

1. Open `UNIVERSAL-KNOWLEDGE-BASE.md`.
2. Find the matching domain. If none exists, add a new domain section.
3. Append the entry row with all required fields.
4. If this supersedes a previous entry, set the old entry's Status to `SUPERSEDED`
   and reference it in the new entry's `Supersedes` field.
5. Increment `<!-- KB_VERSION: x.y.z -->` (PATCH for new entry, MINOR for new domain).
6. Broadcast in LIVE-LOG-CENTER.md:
   ```
   | TIMESTAMP | KnowledgeBase | BROADCAST | KB updated: Domain "X" entry #N added. UNIVERSAL-KNOWLEDGE-BASE.md |
   ```

### Evolving the Schema

When the current schema is insufficient for a new kind of information:

1. Identify the minimum change needed (new field, new domain, etc.).
2. Apply the change to the relevant file.
3. Increment the version metadata.
4. Record the change in `SCHEMA-EVOLUTION-LOG.md` using the standard block format.
5. Broadcast the change in LIVE-LOG-CENTER.md.
6. Notify affected agents via HANDOFF entries.

---

## Outputs

| Artifact | Location | Description |
|----------|----------|-------------|
| Conversation Log | `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md` | Full history of all agent conversations |
| Universal Knowledge | `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md` | Distilled universal truth; source of all team knowledge |
| Schema Evolution Log | `docs/team/knowledge-base/SCHEMA-EVOLUTION-LOG.md` | Auto-documents every schema change |
| README | `docs/team/knowledge-base/README.md` | Usage guide for agents |

---

## Responsibilities

| Agent | Responsibility |
|-------|---------------|
| **All agents** | Append conversation entries; read KB before each task |
| **Knowledge Base** *(this skill)* | Promote conclusions; manage schema evolution; govern both files |
| **Orchestrator** | Close sessions; trigger knowledge promotion at run end |
| **Judge** | Evaluate quality of KB entries; flag low-confidence entries for review |
| **Live Comms** | Broadcast KB updates via LIVE-LOG-CENTER.md |
| **Repo Sync** | Ensure `knowledge-base/` changes are synced to both repos |

---

## Rules

- **Append-only:** Never overwrite or delete entries in either file.
- **No secrets:** No credentials, tokens, or sensitive data in any entry.
- **Schema first:** Before adding a field, check if the existing schema covers your need.
- **Always promote:** Confirmed conclusions (ACCEPTED outcome in ≥ 2 sessions) must be promoted to the Universal Knowledge Base.
- **Supersede, never delete:** When knowledge changes, supersede old entries; never delete them.
- **One source of truth:** The Universal Knowledge Base is authoritative. If PROJECT-STATE.md and the KB conflict, resolve the conflict and update both.

---

## Reference

- Full schema reference: [reference.md](reference.md)
- Conversation Log Database: `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md`
- Universal Knowledge Base: `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md`
- Schema Evolution Log: `docs/team/knowledge-base/SCHEMA-EVOLUTION-LOG.md`
- Live Log Center: `docs/team/live-comms/LIVE-LOG-CENTER.md`
- Team coverage: `docs/team/PROJECT-TEAM-FULL-COVERAGE.md §2`
