# BMC Knowledge Base — Usage Guide

## What is the Knowledge Base?

The `knowledge-base/` folder is the **permanent memory system** for the BMC
agent team. It stores every conversation ever held by the team and the
distilled universal knowledge extracted from those conversations.

---

## Files

| File | Purpose |
|------|---------|
| `CONVERSATION-LOG-DATABASE.md` | Append-only master log of every team conversation, grouped by session/run. Never reset. |
| `UNIVERSAL-KNOWLEDGE-BASE.md` | Distilled universal knowledge nourished by agent conclusions. Universal source of all truth. |
| `SCHEMA-EVOLUTION-LOG.md` | Auto-documents every schema and domain change in both files above. |
| `README.md` | This guide. |

---

## Quick Start

### Reading (before every task)

1. Open `UNIVERSAL-KNOWLEDGE-BASE.md`.
2. Read domains relevant to your work. Trust `HIGH` confidence entries.
3. For full conversation history, search `CONVERSATION-LOG-DATABASE.md`.

### Logging a Conversation Entry

After any significant agent exchange or decision:

1. Open `CONVERSATION-LOG-DATABASE.md`.
2. Locate the current session block (or create a new one — see below).
3. Append a row with the next `#`, current timestamp, your role, type, and content.
4. Keep content ≤ 400 chars. Link to an artifact for longer payloads.

**Session block template:**

```markdown
### Session: YYYY-MM-DD-runN
**Initiated:** YYYY-MM-DD HH:MM:SS UTC
**Closed:**    open
**Agents:**    Role1, Role2, …
**Summary:**   ≤ 300-char description of what this session is about.

| # | Timestamp           | Agent    | Type    | Content                      | Outcome  | Tags     |
|---|---------------------|----------|---------|------------------------------|----------|----------|
| 1 | YYYY-MM-DD HH:MM:SS | MyRole   | FINDING | Short factual statement here | ACCEPTED | tag1     |
```

### Writing a Knowledge Entry

When a conclusion is confirmed (outcome = ACCEPTED or repeated across sessions):

1. Open `UNIVERSAL-KNOWLEDGE-BASE.md`.
2. Find the matching domain, or create a new domain section at the bottom.
3. Append a row to the domain table with all required fields.
4. If a new domain was created, record it in `SCHEMA-EVOLUTION-LOG.md`.
5. Broadcast the new knowledge in `LIVE-LOG-CENTER.md`:
   ```
   | 2026-03-17 06:00:00 | KnowledgeBase | BROADCAST | New knowledge entry added: Domain "X" #N. See UNIVERSAL-KNOWLEDGE-BASE.md. |
   ```

### Superseding an Outdated Entry

When current reality contradicts an existing knowledge entry:

1. Change the entry's `Status` field from `ACTIVE` to `SUPERSEDED`.
2. Add a new entry with the corrected knowledge.
3. Set the new entry's `Supersedes` field to the old entry's `#`.

---

## Entry Types (Conversation Log)

| Type | When to use |
|------|-------------|
| `CONCLUSION` | A fact the team has confirmed as true |
| `DECISION` | A choice made about how to proceed |
| `PROPOSAL` | An idea under consideration, not yet accepted |
| `FINDING` | An observation or discovery during a run |
| `HANDOFF` | An output passed from one agent to another |
| `QUESTION` | An open question needing resolution |
| `ANSWER` | A response that resolves a QUESTION entry |
| `ERROR` | A failure or incorrect assumption logged for learning |
| `META` | An entry about the knowledge system itself |

---

## Schema Evolution Protocol

1. Identify the change needed (new field, new domain, rename, etc.).
2. Make the change in the relevant file.
3. Increment the `<!-- KB_VERSION: x.y.z -->` or `<!-- SCHEMA_VERSION: x.y.z -->` metadata.
4. Append a `### Change #N` block to `SCHEMA-EVOLUTION-LOG.md`.
5. Announce in `LIVE-LOG-CENTER.md` with level `BROADCAST`.

**Versioning:**

| Change | Version bump |
|--------|-------------|
| New entry in existing domain | PATCH (x.y.**Z**) |
| New domain | MINOR (x.**Y**.0) |
| Field rename, add, or remove | MINOR (x.**Y**.0) |
| Structural restructuring | MAJOR (**X**.0.0) |

---

## Skill reference

Full protocol: `.cursor/skills/bmc-universal-knowledge-base/SKILL.md`
Schema reference: `.cursor/skills/bmc-universal-knowledge-base/reference.md`
