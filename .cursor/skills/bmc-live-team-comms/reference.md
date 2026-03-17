# BMC Live Team Comms — Reference

## Log Entry Schema

```
| YYYY-MM-DD HH:MM:SS | AgentRole | Level | Message |
```

| Field | Values | Notes |
|-------|--------|-------|
| Timestamp | `YYYY-MM-DD HH:MM:SS` | Consistent timezone (local or UTC) |
| AgentRole | Any role from PROJECT-TEAM-FULL-COVERAGE §2 | E.g. `Mapping`, `Judge`, `Orchestrator` |
| Level | `INFO` \| `WARN` \| `ERROR` \| `HANDOFF` \| `BROADCAST` | See level definitions below |
| Message | Free text, ≤ 200 chars | Link to artifact for longer payloads |

---

## Level Definitions

| Level | Meaning | Who emits |
|-------|---------|-----------|
| `INFO` | Normal progress update | Any agent |
| `WARN` | Something needs attention but run continues | Any agent, especially Judge/Fiscal |
| `ERROR` | Task or step failed; escalation needed | Any agent |
| `HANDOFF` | Output ready for another agent to pick up | Any agent finishing a deliverable |
| `BROADCAST` | Message to all agents; must be read before next step | Orchestrator primarily |

---

## Addressing Convention

To send to a specific agent, prefix the message with `→ [TargetRole]:`.

```
| 2026-03-17 05:30:00 | Audit | HANDOFF | → Reporter: audit-run8.md ready in docs/team/. |
```

Agents poll LIVE-LOG-CENTER.md for `→ [TheirRole]:` entries.

---

## Parallel Execution Flow

```
Orchestrator
  └─ BROADCAST: "Run starting — parallel windows: Mapping, Design, Security, Judge"
       │
       ├─ Mapping window ──── INFO: working … ──── HANDOFF: → Dependencies
       ├─ Design window ───── INFO: working … ──── HANDOFF: → Reporter
       ├─ Security window ─── INFO: working … ──── WARN: CORS missing
       └─ Judge window ─────── reads all entries continuously
                                └─ WARN: → Orchestrator: Security WARN detected
```

---

## Archival Protocol

1. After run ends, Orchestrator emits:
   `BROADCAST | Run <N> complete. Archiving log.`
2. Live Comms agent (or Orchestrator) copies LIVE-LOG-CENTER.md to
   `docs/team/live-comms/archive/LIVE-LOG-YYYY-MM-DD-runN.md`.
3. LIVE-LOG-CENTER.md is reset to the header-only template for the next run.

**Template header for LIVE-LOG-CENTER.md after reset:**

```markdown
# BMC Live Log Center

> Append-only log bus for all team agents. Do not edit existing entries.
> Format: | YYYY-MM-DD HH:MM:SS | AgentRole | Level | Message |

| Timestamp | Agent | Level | Message |
|-----------|-------|-------|---------|
```

---

## Filtering Examples

| Goal | Scan for |
|------|----------|
| All entries from Design | `\| Design \|` |
| All handoffs | `\| HANDOFF \|` |
| All broadcasts | `\| BROADCAST \|` |
| Errors in this run | `\| ERROR \|` |
| Messages for Reporter | `→ Reporter:` |

---

## Integration with Other Skills

| Skill | Integration point |
|-------|------------------|
| `bmc-parallel-serial-agent` | Provides the execution plan; Live Comms implements it |
| `bmc-team-judge` | Reads live log to evaluate agents; emits WARN/INFO entries |
| `bmc-dashboard-team-orchestrator` | Opens/closes sessions; emits BROADCAST |
| `bmc-repo-sync-agent` | After run, syncs LIVE-LOG-CENTER archive to repos |
