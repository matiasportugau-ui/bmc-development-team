<<<<<<< HEAD
---
schema-version: "1.0"
last-updated: "2026-03-17"
evolution-log: KNOWLEDGE-EVOLUTION-LOG.md
skill: bmc-universal-knowledge
---

# Base Universal de Conocimiento — BMC Team

> **Fuente única de verdad evolutiva del equipo.** Toda conclusión validada,
> decisión arquitectónica y hallazgo pristino del equipo vive aquí.
> Este archivo es la **memoria persistente de todos los agentes**.
>
> - Formato auto-evolutivo: cada agente puede añadir secciones (§N) cuando una
>   nueva categoría de conocimiento emerge.
> - Solo se añaden entradas validadas (ver protocolo en §8).
> - Log de evolución estructural: [KNOWLEDGE-EVOLUTION-LOG.md](./KNOWLEDGE-EVOLUTION-LOG.md)
> - Skill: `.cursor/skills/bmc-universal-knowledge/SKILL.md`

---

## § 0 · Meta-Estructura

| Campo | Valor |
|-------|-------|
| Schema versión | 1.0 |
| Creada | 2026-03-17 |
| Última actualización | 2026-03-17 |
| Agentes contribuyentes | Orchestrator (init) |
| Secciones activas | §0 Meta · §1 Verdades · §2 Arquitectura · §3 Integraciones · §4 Runs · §5 Decisiones · §6 Pendientes · §7 Glosario · §8 Protocolo |

> **Cómo evolucionar:** para añadir una nueva categoría de conocimiento, crear
> una nueva sección `§N` al final del archivo y registrarla en este índice y en
> el log de evolución. Ver §8 para el protocolo completo.

---

## § 1 · Verdades Universales (Conclusiones Validadas)

> Conclusiones "pristinas" validadas por el equipo. Solo se añaden cuando hay
> consenso o validación formal del Judge. **Inmutables una vez validadas** —
> si una verdad cambia, se depreca con `~~texto~~` y se crea una nueva entrada.

| ID | Conclusión | Validado Por | Fecha | Confianza |
|----|-----------|--------------|-------|-----------|
| T001 | El servidor debe reiniciarse para que `/api/kpi-report` retorne 200; la ruta existe en código (`bmcDashboard.js`, montada en `/api` en `index.js`). | Contract + Audit + Reporter | 2026-03-18 | Alta |
| T002 | `npm audit fix` sin `--force` no aplica cambios (7 vulns: 5 low @tootallnate/once/teeny-request, 2 moderate esbuild/vite). Fix solo con `--force` (cambio breaking: vite@8, downgrade @google-cloud/storage). | Security | 2026-03-18 | Alta |
| T003 | Workbook principal de Sheets: `1N-4kyT_uSPSVnu5tMIc6VzFIaga8FHDDEDGcclafRWg`; schema activo: `CRM_Operativo`; 5 workbooks totales. | Mapping | 2026-03-16 | Alta |
| T004 | Puerto canónico del dashboard: 3001. URL principal: `http://localhost:3001/finanzas`. Puerto standalone: 3849. Calculadora: 5173. | Networks + Design | 2026-03-16 | Alta |
| T005 | Las conversaciones y runs del equipo deben registrarse en la Base Universal de Conocimiento (este archivo) para preservar la memoria colectiva del equipo. | Orchestrator (init) | 2026-03-17 | Alta |

---

## § 2 · Arquitectura del Sistema

### Dashboard (bmc-dashboard-2.0)

- **Stack:** Node.js + Express (backend), Vite (frontend), Google Sheets API, MercadoLibre OAuth, Shopify
- **Puertos:** 3001 (canónico), 3849 (standalone), 5173 (Calculadora)
- **URL principal:** `http://localhost:3001/finanzas`
- **Secciones UI:** Resumen financiero, Trend, Breakdown, Calendario, Entregas, Metas, Audit, Ventas 2.0 (tabla + filtro proveedor), Stock E-Commerce (KPIs + tabla + export CSV), Invoque (placeholder)
- **Artefactos clave:** `DASHBOARD-INTERFACE-MAP.md`, `DASHBOARD-VISUAL-MAP.md`, `MAPA-VISUAL-ESTRUCTURA-POR-ESTACION.md`, `PUERTOS-3849-VS-3001.md`

### API Endpoints Verificados

| Método | Ruta | Estado | Notas |
|--------|------|--------|-------|
| GET | `/api/kpi-report` | ✅ Existe en código | Reiniciar servidor si 404 |
| GET | `/api/ventas` | ✅ | `?proveedor=`, `?tab=`, `/tabs` |
| GET | `/api/calendario-vencimientos` | ✅ | `?month=YYYY-MM` |
| GET | `/api/stock/history` | ⏳ Pendiente | EXISTENCIAS_Y_PEDIDOS, Egresos |
| POST | `/api/cotizaciones` | ✅ | append AUDIT_LOG |
| PATCH | `/api/cotizaciones/:id` | ✅ | — |
| POST | `/api/pagos` | ✅ | — |
| PATCH | `/api/pagos/:id` | ✅ | — |
| POST | `/api/ventas` | ✅ | — |
| PATCH | `/api/stock/:codigo` | ✅ | — |

### Infraestructura

- **Producción:** Cloud Run (`panelin-calc`), posible VPS Netuy
- **ngrok:** puerto 4040 para OAuth
- **Repos:** `bmc-dashboard-2.0`, `bmc-development-team`
- **Artefactos:** `HOSTING-EN-MI-SERVIDOR.md`, `.env`

---

## § 3 · Integraciones Activas

| Integración | Estado | Notas |
|-------------|--------|-------|
| Google Sheets | ✅ Activa | 5 workbooks; schema `CRM_Operativo` |
| Google Drive | ✅ Activa | — |
| MercadoLibre OAuth | ✅ Activa | ngrok puerto 4040 |
| Shopify | ✅ Activa | — |
| Cloud Run calc | ✅ Activa | `docs/openapi-calc.yaml` |

---

## § 4 · Historial de Runs del Equipo

> Registro de cada ejecución completa del equipo (pasos 0–9). Para detalles
> narrativos ver `docs/team/PROJECT-STATE.md § Cambios recientes`.

| Run | Fecha | Judge Score | Hitos Clave |
|-----|-------|-------------|-------------|
| Runs 1–5 | 2026-03-16 | Ver HISTORICO | Desarrollos iniciales |
| Run 6 | 2026-03-16 | — | Ver `JUDGE-REPORT-RUN-2026-03-16.md` |
| Run 7 | 2026-03-16 | 4.93/5 (18/19) | Post-go-live agenda; PUSH routes; Repo Sync; Guía vendedores |
| Run 8 (Live Comms) | 2026-03-17 | — | Skill `bmc-live-team-comms` activado; Live Log Center creado |
| Run (2026-03-18 #1) | 2026-03-18 | — | 19/19 agentes; GUIA-RAPIDA-VENDEDORES.md; PROMPT actualizado |
| Run (2026-03-18 #2) | 2026-03-18 | — | E2E-VALIDATION-CHECKLIST.md; npm audit sin --force; CONTRACT verificado |
| Run (2026-03-17 UKB) | 2026-03-17 | — | Base Universal de Conocimiento (UKB) creada; skill `bmc-universal-knowledge` |

---

## § 5 · Decisiones de Equipo

> Decisiones arquitectónicas o de proceso tomadas y validadas. Incluyen
> justificación para que futuros agentes no las reviertan sin contexto.

| ID | Decisión | Justificación | Tomado Por | Fecha |
|----|---------|---------------|------------|-------|
| D001 | Usar append-only log bus (`LIVE-LOG-CENTER.md`) para comunicación en paralelo | Evita conflictos de escritura concurrente entre agentes | Orchestrator + Live Comms | 2026-03-17 |
| D002 | `PROJECT-STATE.md` como única fuente de verdad de estado de proyecto | Evita drift entre agentes; todos leen el mismo estado | Equipo completo | 2026-03-16 |
| D003 | No ejecutar `npm audit fix --force` sin aprobación de Matias | Cambio breaking (vite@8 + @google-cloud/storage downgrade) | Security | 2026-03-18 |
| D004 | `UNIVERSAL-KNOWLEDGE-BASE.md` como memoria colectiva persistente de todos los agentes | Preservar conclusiones validadas y contexto entre runs indefinidamente | Orchestrator (init) | 2026-03-17 |
| D005 | Schema de UKB es auto-evolutivo: agentes añaden §N según necesidad | Flexibilidad para acompañar el crecimiento del dominio sin romper la estructura | bmc-universal-knowledge (init) | 2026-03-17 |

---

## § 6 · Pendientes Críticos del Equipo

> Solo ítems que el equipo ha validado como críticos y que aún no están resueltos.
> Al resolver un ítem, marcarlo `[x]` y añadir la fecha de resolución.

| ID | Pendiente | Urgencia | Responsable | Fecha Registro |
|----|-----------|----------|-------------|---------------|
| P001 | Go-live: crear tabs manuales (CONTACTOS, Ventas_Consolidado, SHOPIFY_SYNC_AT, PAGADO) y configurar triggers | Alta | Matias | 2026-03-18 |
| P002 | Deploy producción a Cloud Run o VPS Netuy | Alta | GPT/Cloud | 2026-03-18 |
| P003 | E2E validation antes de go-live público (`docs/team/E2E-VALIDATION-CHECKLIST.md`) | Alta | Audit/Debug | 2026-03-18 |
| P004 | Verificar que `/api/kpi-report` retorna 200 tras restart en producción | Media | Contract | 2026-03-18 |
| P005 | Compartir workbook con service account (step 1.4 del GO-LIVE checklist) | Alta | Matias | 2026-03-18 |

---

## § 7 · Glosario del Equipo

| Término | Definición |
|---------|-----------|
| Run | Ejecución completa del equipo de 19 agentes (pasos 0–9) |
| HANDOFF | Nivel de log que indica entrega de output entre agentes en el bus de comunicación |
| UKB | Universal Knowledge Base — este archivo (`UNIVERSAL-KNOWLEDGE-BASE.md`) |
| KEL | Knowledge Evolution Log — `KNOWLEDGE-EVOLUTION-LOG.md` |
| Live Comms | Sistema de comunicación en tiempo real entre agentes que corren en paralelo |
| Judge Score | Promedio de evaluación del agente Judge al finalizar un run (escala 1–5) |
| Verdad Universal | Conclusión validada por el equipo con alta confianza, registrada en §1 |
| Schema versión | Número de versión de la estructura del UKB (semver de la meta-estructura) |
| Pristine conclusion | Hallazgo o conclusión emergente de un agente que, tras validación, se eleva a §1 |

---

## § 8 · Protocolo de Contribución y Evolución

### Cómo añadir una Verdad Universal (§1)

1. El agente identifica una conclusión de alta confianza durante su trabajo.
2. Añade la entrada a §1 con nivel de confianza `Media`.
3. El **Judge** o el **Orchestrator** revisan y elevan la confianza a `Alta` si
   procede, o la eliminan si es incorrecta.
4. Registrar la adición en `KNOWLEDGE-EVOLUTION-LOG.md`.

### Cómo añadir una nueva sección (§N)

1. Identificar que una nueva categoría de conocimiento no cabe en las secciones
   existentes.
2. Añadir `## § N · [Nombre descriptivo]` al final del archivo (N = siguiente
   número disponible).
3. Actualizar la fila de "Secciones activas" en §0.
4. Registrar el cambio en `KNOWLEDGE-EVOLUTION-LOG.md` con tipo `STRUCTURE`.

### Cómo deprecar una entrada

- Marcar la entrada con `~~texto~~` y añadir nota: `*[Deprecada YYYY-MM-DD: razón]*`.
- No eliminar entradas deprecadas — el historial es parte del conocimiento.

### Reglas generales

- **Nunca borrar entradas validadas** — si cambia la realidad, deprecar y crear nueva.
- **Citar la fuente** del conocimiento (agente + fecha) en cada entrada.
- **No registrar secretos** (tokens, passwords, API keys) en este archivo.
- **Actualizar §0** cuando el schema evolucione (nueva versión = incrementar `schema-version`).
- Ante cada cambio estructural, registrar en `KNOWLEDGE-EVOLUTION-LOG.md`.
=======
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
>>>>>>> origin/main
