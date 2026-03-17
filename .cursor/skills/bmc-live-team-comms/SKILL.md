---
name: bmc-live-team-comms
description: >
  Enables the BMC agent team to run in parallel windows with live, continuous
  inter-agent communication. Manages a shared Live Log Center where every
  agent continuously appends structured log entries; any team member can read,
  filter, and act on live logs from all other agents without stopping their own
  work. Use when enabling parallel execution, live agent dialogue, or when a
  central log hub for the full team is needed.
---

# BMC Live Team Communication & Log Center

**Before working:** Read `docs/team/live-comms/LIVE-LOG-CENTER.md` if it exists.

The **Live Team Communication & Log Center** gives every agent in the BMC team
the ability to:

1. **Run in parallel** inside independent agent windows (one window per agent).
2. **Communicate continuously** with all other agents through a shared log bus.
3. **Append structured log entries** to a central log file in real-time.
4. **Read, filter, and react** to any other agent's live log output without
   interrupting their own work stream.

---

## When to Use

- User says: "run all agents in parallel", "live comms", "parallel windows",
  "live log center", "all agents running simultaneously", "equipo en paralelo
  con logs en vivo", "comunicación continua entre agentes".
- Orchestrator wants to start a full parallel run with live inter-agent
  messaging.
- Any agent needs to broadcast a finding or a status update to the rest of the
  team in real time.

---

## Core Concepts

### 1. Agent Window

Each team member runs in its **own dedicated agent window** (a Cursor agent
tab, a background agent thread, or a named process). The window identity is the
agent's role name (e.g., `Mapping`, `Design`, `Judge`).

### 2. Live Log Bus

A single append-only Markdown file — `docs/team/live-comms/LIVE-LOG-CENTER.md`
— acts as the **shared log bus**. Every agent writes entries; every agent can
read the full bus at any time.

**Entry format:**

```
| YYYY-MM-DD HH:MM:SS | <AgentRole> | <Level> | <Message> |
```

- **AgentRole:** Role name from PROJECT-TEAM-FULL-COVERAGE §2 (e.g., `Mapping`,
  `Judge`, `Fiscal`).
- **Level:** `INFO` · `WARN` · `ERROR` · `HANDOFF` · `BROADCAST`.
- **Message:** Free text; keep under 200 characters. For longer payloads, link
  to the relevant artifact.

**Example entries:**

```
| 2026-03-17 05:10:00 | Mapping    | INFO      | planilla-inventory.md read; 5 workbooks confirmed. |
| 2026-03-17 05:10:15 | Orchestrator | BROADCAST | Step 2 Mapping starting. All agents stand by.     |
| 2026-03-17 05:11:00 | Design     | HANDOFF   | UX proposal ready → Reporter. See REPORT-run8.md. |
| 2026-03-17 05:11:30 | Judge      | WARN       | Security score dropped 0.3 vs last run. Notify Security. |
```

### 3. Parallel Execution

When the Orchestrator triggers a **parallel run**, it:

1. Reads `docs/team/parallel-serial/PARALLEL-SERIAL-PLAN-YYYY-MM-DD.md` (or
   generates one via `bmc-parallel-serial-agent`) to decide which agents run
   concurrently.
2. Broadcasts a `BROADCAST` entry: *"Full parallel run starting. Windows: [list
   of agents]."*
3. Each agent independently opens its window and begins work, appending `INFO`
   entries as it proceeds.
4. When an agent produces an output that another agent needs, it appends a
   `HANDOFF` entry pointing to the artifact.
5. The receiving agent detects the `HANDOFF` (by polling LIVE-LOG-CENTER.md
   for entries directed to its role) and picks up the artifact.

### 4. Log Filtering (per agent)

Any team member can filter the log bus to see only entries relevant to them:

- **By role:** all entries from `| Design |`.
- **By level:** all `HANDOFF` entries (to catch incoming work).
- **By keyword:** grep for a tab name, a file path, or a run date.

The filter convention (for a human reviewer or an agent scanning the file):

```
Filter:  role=Design  OR  level=HANDOFF
Result:  only rows matching those conditions from LIVE-LOG-CENTER.md
```

---

## Workflow

### Starting a Parallel Live Session

1. **Orchestrator** appends `BROADCAST | Full parallel run starting.` to
   LIVE-LOG-CENTER.md.
2. **Each agent** reads the broadcast, opens (or activates) its window, and
   appends `INFO | [AgentRole] window active.`
3. Agents execute their tasks independently, appending entries continuously.
4. Agents that finish a stage emit a `HANDOFF` entry.
5. Dependent agents pick up `HANDOFF` entries and begin their next stage.
6. **Judge** monitors all entries; if it detects an `ERROR` level entry it
   emits a `WARN` to the Orchestrator.
7. At run end, **Orchestrator** appends `BROADCAST | Run complete. Log archived.`
   and triggers archival (see §Archival).

### Sending a Message to a Specific Agent

Any agent can address another by including the target role in the message:

```
| 2026-03-17 05:20:00 | Fiscal | WARN | → Security: CORS header missing in prod endpoint. |
```

The prefix `→ [TargetRole]:` is the addressing convention. The target agent
scans for entries that start with `→ [its role]:`.

### Broadcasting to All Agents

Use `BROADCAST` level with no target prefix. All agents are expected to read
broadcast entries before proceeding with their next task.

---

## Outputs

| Artifact | Location | Description |
|----------|----------|-------------|
| Live Log Bus | `docs/team/live-comms/LIVE-LOG-CENTER.md` | Append-only; all agent entries |
| Archive | `docs/team/live-comms/archive/LIVE-LOG-YYYY-MM-DD-runN.md` | Archived after each run |
| README | `docs/team/live-comms/README.md` | Usage guide for the team |

---

## Responsibilities of Each Agent

| Agent | Responsibility |
|-------|---------------|
| **Orchestrator** | Open/close parallel sessions; emit `BROADCAST`; archive log after run |
| **Parallel/Serial** | Decide which agents run in parallel; included in parallel plan |
| **All agents** | Append `INFO` entries as they work; emit `HANDOFF` when output is ready |
| **Judge** | Monitor log for `ERROR`/`WARN`; emit evaluation entries at run end |
| **Live Comms** *(this skill)* | Manage the log bus protocol; guide other agents on format; perform archival |

---

## Reglas

- **Append-only:** Never overwrite or delete entries in LIVE-LOG-CENTER.md
  during a live run. Archival (move to archive/) happens only after the run ends.
- **Timestamps:** Always use `YYYY-MM-DD HH:MM:SS` UTC (or local consistent
  timezone).
- **Max entry size:** 200 characters in the message field. Link to artifacts for
  details.
- **No secrets:** Never log credentials, tokens, or sensitive data.
- **Archival:** After each run, Orchestrator (or Live Comms agent) moves the
  current log to the archive with the run date/number suffix.

---

## Reference

- Log bus protocol: [reference.md](reference.md)
- Full team coverage: `docs/team/PROJECT-TEAM-FULL-COVERAGE.md` §2
- Parallel/Serial strategy: `.cursor/skills/bmc-parallel-serial-agent/SKILL.md`
- Orchestrator: `.cursor/agents/bmc-dashboard-team-orchestrator.md`
