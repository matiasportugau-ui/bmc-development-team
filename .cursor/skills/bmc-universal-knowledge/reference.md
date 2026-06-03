# BMC Universal Knowledge Base — Quick Reference

## Files

| File | Purpose |
|------|---------|
| `docs/team/knowledge-base/UNIVERSAL-KNOWLEDGE-BASE.md` | Main UKB — the team's persistent memory |
| `docs/team/knowledge-base/KNOWLEDGE-EVOLUTION-LOG.md` | Append-only log of structural changes |

---

## UKB Section Index

| Section | Content | Mutability |
|---------|---------|-----------|
| §0 | Meta-structure, schema version, section index | Updated on schema changes |
| §1 | Verdades Universales (validated conclusions) | Append + deprecate only |
| §2 | System architecture (stack, ports, endpoints) | Append + update |
| §3 | Active integrations | Append + update |
| §4 | Run history | Append only |
| §5 | Team decisions with justification | Append + deprecate |
| §6 | Critical pending items | Append + resolve |
| §7 | Team glossary | Append + deprecate |
| §8 | Contribution protocol | Updated on schema changes |
| §N+ | New domains added by agents as needed | — |

---

## KEL Entry Format

```
| YYYY-MM-DD HH:MM | Agent | Type | Description | Schema before → after |
```

**Types:** `INIT` · `STRUCTURE` · `TRUTH` · `DECISION` · `DEPRECATE` · `UPDATE` · `PENDING` · `RESOLVED`

---

## Pristine Conclusion Lifecycle

```
Agent adds candidate → §1 with confidence "Media"
         ↓
Judge/Orchestrator reviews
         ↓
Elevated to "Alta" (immutable) OR removed
         ↓
KEL entry: TRUTH
```

---

## Schema Version Rules

| Change | Version bump |
|--------|-------------|
| New §N section added | Minor (1.0 → 1.1) |
| §1–§8 restructured | Major (1.x → 2.0) |
| Entries added/updated | No bump |

---

## Filtering the UKB

| Goal | Pattern to search |
|------|------------------|
| All validated truths | `## § 1` |
| Specific truth | `T001` (or any ID) |
| All team decisions | `## § 5` |
| Open pending items | `## § 6` |
| A specific agent's entries | `\| Mapping \|` |
| Deprecated entries | `~~` |
| Latest schema version | `schema-version:` in front-matter |

---

## Quick Actions

### Add a truth candidate
```markdown
| T00N | [Your conclusion] | [Your role] | YYYY-MM-DD | Media |
```
Then notify Judge via `LIVE-LOG-CENTER.md`.

### Add a KEL entry
```markdown
| YYYY-MM-DD HH:MM | [Your role] | [TYPE] | [What changed] | 1.0 → 1.0 |
```

### Add a new section
```markdown
## § N · [Section Name]
> Description of what goes here.
```
Then update §0 "Secciones activas" and bump schema-version if major.
