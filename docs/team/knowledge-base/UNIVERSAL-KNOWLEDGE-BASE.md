# BMC Universal Knowledge Base

> **The universal source of all truth for the BMC team.**
> Nourished by pristine agent conclusions extracted from the Conversation Log Database.
> Auto-evolves its structure as the team's needs grow.
> All agents must read this before working and write confirmed conclusions here.

<!-- KB_VERSION: 1.0.0 -->
<!-- LAST_EVOLVED: 2026-03-17 -->
<!-- TOTAL_DOMAINS: 6 -->
<!-- TOTAL_ENTRIES: 9 -->

---

## How Agents Interact with This File

### Reading (before every task)
1. Open this file.
2. Navigate to the domain(s) relevant to your task.
3. Read all `HIGH`-confidence entries; skim `MEDIUM`; note `LOW`.
4. If an entry contradicts current reality, mark it `SUPERSEDED` and add a new entry.

### Writing (after producing a confirmed conclusion)
1. Identify the correct domain (or create a new one — see "Domain Evolution").
2. Add your entry at the **end** of that domain's table.
3. Fill every required field. Use `—` for genuinely unknown optional fields.
4. Append a row to SCHEMA-EVOLUTION-LOG.md if you add a field or domain.

### Domain Evolution
If no existing domain fits your conclusion:
1. Add a new `## Domain: [Name]` section at the bottom of this file.
2. Include the standard entry table.
3. Record the new domain in SCHEMA-EVOLUTION-LOG.md.
4. Broadcast the change in LIVE-LOG-CENTER.md with level `BROADCAST`.

---

## Entry Schema

| Field       | Required | Values / Notes                                         |
|-------------|----------|--------------------------------------------------------|
| #           | ✓        | Sequential integer within the domain                   |
| Date        | ✓        | `YYYY-MM-DD`                                           |
| Source      | ✓        | `Session-ID / AgentRole` (e.g. `2026-03-17-run1 / Judge`) |
| Confidence  | ✓        | `HIGH` · `MEDIUM` · `LOW`                              |
| Status      | ✓        | `ACTIVE` · `SUPERSEDED` · `UNDER_REVIEW`               |
| Content     | ✓        | Plain-text knowledge statement, ≤ 400 chars. Link for details. |
| Tags        | ✓        | Comma-separated keywords                               |
| Supersedes  | —        | Entry `#` this replaces, or `—`                        |

---

## Domain: Team Structure & Roles

| # | Date       | Source                         | Confidence | Status | Content                                                                                              | Tags                           | Supersedes |
|---|------------|--------------------------------|------------|--------|------------------------------------------------------------------------------------------------------|--------------------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | Canonical team roles are defined in `docs/team/PROJECT-TEAM-FULL-COVERAGE.md §2`. New roles must be added to that table and to JUDGE-CRITERIA-POR-AGENTE immediately. | team, roles, canonical         | —          |
| 2 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | When invoking "Equipo Completo", all roles in PROJECT-TEAM-FULL-COVERAGE §2 are included automatically. No role is excluded. | team, full-run, orchestrator   | —          |
| 3 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | Every team member can clone itself. Clone naming: `Role`, `Role+1`, `Role+2` … to parallelize work. | cloning, parallelism           | —          |

---

## Domain: Communication & Logging Protocol

| # | Date       | Source                         | Confidence | Status | Content                                                                                              | Tags                              | Supersedes |
|---|------------|--------------------------------|------------|--------|------------------------------------------------------------------------------------------------------|-----------------------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Live Comms   | HIGH       | ACTIVE | `docs/team/live-comms/LIVE-LOG-CENTER.md` is the append-only real-time log bus. Format: `\| YYYY-MM-DD HH:MM:SS \| AgentRole \| Level \| Message \|`. Levels: INFO, WARN, ERROR, HANDOFF, BROADCAST. | comms, live-log, protocol          | —          |
| 2 | 2026-03-17 | 2026-03-17-run1 / Live Comms   | HIGH       | ACTIVE | After each run the Orchestrator (or Live Comms) archives LIVE-LOG-CENTER.md → `docs/team/live-comms/archive/LIVE-LOG-YYYY-MM-DD-runN.md` and resets the bus to the header template. | comms, archival, live-log          | —          |
| 3 | 2026-03-17 | 2026-03-17-run1 / Knowledge Base | HIGH     | ACTIVE | `docs/team/knowledge-base/CONVERSATION-LOG-DATABASE.md` is the permanent full-history log of all team conversations (append-only, never reset). Each run appends a new Session block. | knowledge-base, conversation-log   | —          |
| 4 | 2026-03-17 | 2026-03-17-run1 / Knowledge Base | HIGH     | ACTIVE | `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md` (this file) is the universal source of truth. Agents extract confirmed conclusions from the Conversation Log and write them here. | knowledge-base, source-of-truth    | —          |

---

## Domain: Project State & Synchronization

| # | Date       | Source                         | Confidence | Status | Content                                                                                              | Tags                             | Supersedes |
|---|------------|--------------------------------|------------|--------|------------------------------------------------------------------------------------------------------|----------------------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | `docs/team/PROJECT-STATE.md` is the single source of current project state. Every agent reads it before working and updates it after any change that affects others. | project-state, sync              | —          |
| 2 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | After any domain or schema change, the detecting agent updates PROJECT-TEAM-FULL-COVERAGE §1 & §4, then propagates to affected agents per the propagation table in that document. | sync, propagation, domain-change | —          |

---

## Domain: Knowledge Base Operations

| # | Date       | Source                           | Confidence | Status | Content                                                                                              | Tags                            | Supersedes |
|---|------------|----------------------------------|------------|--------|------------------------------------------------------------------------------------------------------|---------------------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Knowledge Base | HIGH       | ACTIVE | Schema version is tracked in the `<!-- KB_VERSION: x.y.z -->` metadata comment at the top of this file. Increment PATCH for new entries, MINOR for new domains, MAJOR for structural restructuring. | kb, schema, versioning          | —          |
| 2 | 2026-03-17 | 2026-03-17-run1 / Knowledge Base | HIGH       | ACTIVE | Every schema change (new field, new domain, field rename) must be recorded in `docs/team/knowledge-base/SCHEMA-EVOLUTION-LOG.md` with date, version, reason, and who changed it. | kb, schema, evolution-log       | —          |

---

## Domain: Skills Registry

| # | Date       | Source                         | Confidence | Status | Content                                                                                              | Tags                  | Supersedes |
|---|------------|--------------------------------|------------|--------|------------------------------------------------------------------------------------------------------|-----------------------|------------|
| 1 | 2026-03-17 | 2026-03-17-run1 / Orchestrator | HIGH       | ACTIVE | All active skills are indexed in `.cursor/skills/SKILLS-INDEX.md`. Full definitions live in `.cursor/skills/<skill-name>/SKILL.md`. New skills must be registered there immediately. | skills, index, registry | —         |
