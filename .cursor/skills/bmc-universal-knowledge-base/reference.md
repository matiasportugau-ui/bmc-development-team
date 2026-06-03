# BMC Universal Knowledge Base — Schema Reference

---

## 1. Conversation Log Database

File: `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md`

### File-level Metadata (HTML comments at top)

| Key | Example | Notes |
|-----|---------|-------|
| `SCHEMA_VERSION` | `1.0.0` | Semver; bump per schema-evolution rules |
| `SCHEMA_EVOLVED` | `2026-03-17` | Date of last schema change |
| `TOTAL_SESSIONS` | `12` | Count of all Session blocks |
| `TOTAL_ENTRIES` | `147` | Count of all entry rows across all sessions |

### Session Block

```markdown
### Session: YYYY-MM-DD-runN
**Initiated:** YYYY-MM-DD HH:MM:SS UTC
**Closed:**    YYYY-MM-DD HH:MM:SS UTC  (or `open` while active)
**Agents:**    Comma-separated agent roles
**Summary:**   ≤ 300-char plain-text description
```

| Field | Required | Notes |
|-------|----------|-------|
| Session ID | ✓ | `YYYY-MM-DD-runN` format |
| Initiated | ✓ | UTC timestamp when session opened |
| Closed | ✓ | UTC timestamp when session ended; `open` while active |
| Agents | ✓ | All roles that participated |
| Summary | ✓ | ≤ 300 chars describing the session purpose/outcome |

### Entry Row

```
| # | Timestamp           | Agent     | Type    | Content                        | Outcome  | Tags        |
|---|---------------------|-----------|---------|--------------------------------|----------|-------------|
| 1 | 2026-03-17 05:36:49 | Mapping   | FINDING | planilla has 5 workbooks total | ACCEPTED | sheets, map |
```

| Field | Required | Values / Constraints |
|-------|----------|----------------------|
| `#` | ✓ | Sequential integer; unique within session |
| Timestamp | ✓ | `YYYY-MM-DD HH:MM:SS` (consistent TZ) |
| Agent | ✓ | Role name from PROJECT-TEAM-FULL-COVERAGE §2 |
| Type | ✓ | `CONCLUSION` · `DECISION` · `PROPOSAL` · `FINDING` · `HANDOFF` · `QUESTION` · `ANSWER` · `ERROR` · `META` |
| Content | ✓ | Free text ≤ 400 chars; link to artifact for longer payloads |
| Outcome | ✓ | `ACCEPTED` · `REJECTED` · `PENDING` · `SUPERSEDED` |
| Tags | ✓ | Comma-separated lowercase keywords |

#### Entry Type Definitions

| Type | Meaning |
|------|---------|
| `CONCLUSION` | A fact confirmed as true by the team |
| `DECISION` | A choice made about how to proceed |
| `PROPOSAL` | An idea under consideration, not yet accepted |
| `FINDING` | An observation or discovery during a run |
| `HANDOFF` | An output passed from one agent to another |
| `QUESTION` | An open question needing resolution |
| `ANSWER` | A response that resolves a QUESTION entry |
| `ERROR` | A failure or incorrect assumption logged for learning |
| `META` | An entry about the knowledge system itself |

#### Outcome Value Definitions

| Outcome | Meaning |
|---------|---------|
| `ACCEPTED` | Confirmed correct; eligible for promotion to Universal KB |
| `REJECTED` | Confirmed incorrect or abandoned |
| `PENDING` | Not yet evaluated |
| `SUPERSEDED` | Replaced by a later entry; kept for history |

---

## 2. Universal Knowledge Base

File: `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md`

### File-level Metadata (HTML comments at top)

| Key | Example | Notes |
|-----|---------|-------|
| `KB_VERSION` | `1.0.0` | Semver; bump per versioning rules |
| `LAST_EVOLVED` | `2026-03-17` | Date of last structural change |
| `TOTAL_DOMAINS` | `6` | Count of domain sections |
| `TOTAL_ENTRIES` | `24` | Count of all entry rows across all domains |

### Domain Section Header

```markdown
## Domain: [Domain Name]
```

One section per knowledge domain. Created as needed.

### Entry Row

```
| # | Date       | Source                        | Confidence | Status | Content                        | Tags             | Supersedes |
|---|------------|-------------------------------|------------|--------|--------------------------------|------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | Port 3001 is the canonical port | infra, dashboard | —          |
```

| Field | Required | Values / Constraints |
|-------|----------|----------------------|
| `#` | ✓ | Sequential integer within the domain |
| Date | ✓ | `YYYY-MM-DD` when entry was written |
| Source | ✓ | `Session-ID / AgentRole` |
| Confidence | ✓ | `HIGH` · `MEDIUM` · `LOW` |
| Status | ✓ | `ACTIVE` · `SUPERSEDED` · `UNDER_REVIEW` |
| Content | ✓ | Knowledge statement ≤ 400 chars; link for details |
| Tags | ✓ | Comma-separated lowercase keywords |
| Supersedes | — | Entry `#` this replaces, or `—` |

#### Confidence Definitions

| Level | Meaning |
|-------|---------|
| `HIGH` | Verified in ≥ 2 runs or explicitly confirmed by Orchestrator/Judge |
| `MEDIUM` | Confirmed in 1 run; not yet re-verified |
| `LOW` | Hypothesis or single-agent observation; needs verification |

#### Status Definitions

| Status | Meaning |
|--------|---------|
| `ACTIVE` | Current; agents should use this entry |
| `SUPERSEDED` | Replaced by a newer entry in the same domain |
| `UNDER_REVIEW` | Being evaluated; do not rely on until status changes |

---

## 3. Schema Evolution Log

File: `docs/team/knowledge-base/SCHEMA-EVOLUTION-LOG.md`

### Change Block Format

```markdown
### Change #N — YYYY-MM-DD — vX.Y.Z
**Type:** field-add | field-rename | field-remove | domain-add | domain-rename | schema-restructure
**Author:** AgentRole
**Reason:** ≤ 200 chars
**Files affected:** list of files
**Backward compatible:** Yes / No
**Details:** (optional free-text)
```

### Versioning Rules

| Change | Version bump |
|--------|-------------|
| New entry in existing domain / new conversation entry | PATCH (x.y.**Z**) |
| New domain in Universal KB / new field (optional) | MINOR (x.**Y**.0) |
| Field rename or removal / breaking structural change | MAJOR (**X**.0.0) |

---

## 4. Integration Points

| System | Integration |
|--------|-------------|
| `docs/team/live-comms/LIVE-LOG-CENTER.md` | All KB updates announced as `BROADCAST` entries |
| `docs/team/PROJECT-STATE.md` | KB section listed under "Estado por área"; conflicts resolved with KB as authority |
| `docs/team/PROJECT-TEAM-FULL-COVERAGE.md §2` | `Knowledge Base` role listed; skill `bmc-universal-knowledge-base` |
| `docs/team/live-comms/archive/` | Archived runs remain queryable via Conversation Log |
| `.cursor/skills/SKILLS-INDEX.md` | `bmc-universal-knowledge-base` registered |
