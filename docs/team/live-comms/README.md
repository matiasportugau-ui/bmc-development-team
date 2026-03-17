# Live Team Communication & Log Center — Usage Guide

## What is this?

The `live-comms/` folder is the **real-time communication hub** for the BMC
agent team. It allows every agent to:

- Run in its own **parallel window** without waiting for others to finish.
- **Continuously broadcast** progress, findings, and handoffs to all other
  agents.
- **Read live logs** from any other agent, filtered by role, level, or keyword.

---

## Files

| File | Purpose |
|------|---------|
| `LIVE-LOG-CENTER.md` | Active append-only log bus. All agents read and write here. |
| `archive/LIVE-LOG-YYYY-MM-DD-runN.md` | Archived log per run, created after each session. |
| `README.md` | This guide. |

---

## Quick Start

### As an agent starting a task

1. Open (or activate) your **agent window**.
2. Read the last ~20 entries of `LIVE-LOG-CENTER.md` for context.
3. Append your opening entry:
   ```
   | 2026-03-17 05:10:00 | Design | INFO | Window active. Starting UX review for run 8. |
   ```
4. Work normally, appending `INFO` entries as milestones are reached.
5. When you produce an output another agent needs, append a `HANDOFF` entry:
   ```
   | 2026-03-17 05:45:00 | Design | HANDOFF | → Reporter: UX decisions in REPORT-run8.md ready. |
   ```

### As an agent waiting for input

1. Poll `LIVE-LOG-CENTER.md` for `→ [YourRole]:` entries.
2. When a `HANDOFF` or `BROADCAST` for you appears, act on it.

### As the Orchestrator

1. Open the session with a `BROADCAST` entry:
   ```
   | 2026-03-17 05:00:00 | Orchestrator | BROADCAST | Full parallel run 8 starting. Windows: Mapping, Design, Security, Judge, Repo Sync. |
   ```
2. Monitor for `ERROR` entries and escalate if needed.
3. Close with:
   ```
   | 2026-03-17 06:30:00 | Orchestrator | BROADCAST | Run 8 complete. Archiving log now. |
   ```
4. Archive: copy `LIVE-LOG-CENTER.md` → `archive/LIVE-LOG-2026-03-17-run8.md`,
   then reset `LIVE-LOG-CENTER.md` to the header template.

---

## Entry Format

```
| YYYY-MM-DD HH:MM:SS | AgentRole | Level | Message (≤200 chars) |
```

**Levels:**

| Level | When to use |
|-------|-------------|
| `INFO` | Normal progress |
| `WARN` | Something needs attention; run continues |
| `ERROR` | Step failed; escalation needed |
| `HANDOFF` | Deliverable ready for another agent |
| `BROADCAST` | Message to the entire team |

**Addressing a specific agent:** prefix message with `→ [TargetRole]:`.

---

## Filtering the Log

To read only entries relevant to you, search for:

| Goal | Pattern |
|------|---------|
| Your role's entries | `\| Design \|` (replace `Design` with your role) |
| Messages for you | `→ Design:` |
| All handoffs | `\| HANDOFF \|` |
| All broadcasts | `\| BROADCAST \|` |
| Errors | `\| ERROR \|` |

---

## Rules

- **Never overwrite or delete** entries during a live run.
- **No secrets** (tokens, passwords, API keys) in log messages.
- **Archival** only after Orchestrator emits the run-complete `BROADCAST`.
- **One entry per milestone** — don't spam; keep the log readable.

---

## Skill reference

Full protocol: `.cursor/skills/bmc-live-team-comms/SKILL.md`  
Log schema: `.cursor/skills/bmc-live-team-comms/reference.md`
