# BMC Development Team

> **Equipo de desarrollo IA multi-agente** para el sistema de dashboard de BMC/Panelin — Uruguay.

Este repositorio es el **hub de coordinación** del equipo de 23 agentes de IA especializados que trabajan en conjunto para desarrollar, mantener y mejorar el [BMC Dashboard](https://github.com/matiasportugau-ui/bmc-dashboard-2.0), una aplicación web de inteligencia de negocio y planificación financiera.

---

## Tabla de contenidos

- [¿Qué es este repositorio?](#qué-es-este-repositorio)
- [Stack tecnológico](#stack-tecnológico)
- [Estructura de directorios](#estructura-de-directorios)
- [El equipo: 23 agentes especializados](#el-equipo-23-agentes-especializados)
- [Aplicación BMC Dashboard](#aplicación-bmc-dashboard)
- [Configuración y uso](#configuración-y-uso)
- [Scripts de automatización](#scripts-de-automatización)
- [Estado actual del proyecto](#estado-actual-del-proyecto)
- [Documentación clave](#documentación-clave)
- [Repos relacionados](#repos-relacionados)

---

## ¿Qué es este repositorio?

Este es el repositorio de **coordinación del equipo de desarrollo** de BMC/Panelin. No es una aplicación ejecutable en sí misma — es el núcleo de documentación, definición de agentes y estado del proyecto que permite a 23 agentes de IA trabajar de forma coordinada.

**¿Qué contiene?**

- **Definiciones de agentes y skills** (`/.cursor/`) — Instrucciones y capacidades de cada rol del equipo
- **Estado del proyecto** (`/docs/team/`) — Fuente única de verdad para todos los agentes
- **Documentación del dashboard** (`/docs/bmc-dashboard-modernization/`) — Planes de implementación y reportes
- **Scripts de automatización** (Python y Bash) — Automatización fiscal y de auditoría

---

## Stack tecnológico

### Este repositorio (coordinación y documentación)

| Tecnología | Uso |
|-----------|-----|
| **Markdown** | Documentación, estado del proyecto, definición de agentes (59+ archivos) |
| **Python** | Scripts de automatización fiscal (DGI/CFE) |
| **Bash** | Scripts de auditoría y despliegue |
| **Git** | Control de versiones y sincronización entre repos |

### Aplicación BMC Dashboard (repo `bmc-dashboard-2.0`)

| Tecnología | Uso |
|-----------|-----|
| **Node.js / Express** | Backend del dashboard (puerto 3001) |
| **JavaScript** | Lógica de frontend del dashboard |
| **React / Vite** | Calculadora/Cotizador (puerto 5173) |
| **Google Sheets API** | Fuente de datos principal |
| **Google Drive API** | Almacenamiento de archivos |
| **Google Cloud Run** | Despliegue en producción |
| **OpenAI GPT** | Integración GPT Builder / Actions |

### Integraciones externas

- **MercadoLibre** — OAuth, sincronización de marketplace
- **Shopify** — E-commerce, webhooks
- **Google Apps Script** — Automatización de hojas de cálculo
- **ngrok** — Túnel OAuth en desarrollo (puerto 4040)

---

## Estructura de directorios

```
bmc-development-team/
│
├── .cursor/                                # Configuración de agentes IA (Cursor)
│   ├── agents/
│   │   └── bmc-dashboard-team-orchestrator.md    # Orquestador principal del equipo
│   └── skills/                             # 18 skills locales (+ skills externos indexados en SKILLS-INDEX.md)
│       ├── bmc-planilla-dashboard-mapper/        # Mapeo Sheets ↔ Dashboard ↔ API
│       ├── bmc-dashboard-design-best-practices/  # UX/UI, jerarquía, estados
│       ├── bmc-sheets-structure-editor/          # Gestión de tabs y estructura
│       │   └── scripts/                          # Scripts para edición de hojas
│       ├── bmc-dgi-impositivo/                   # Supervisión fiscal y tributaria
│       │   └── scripts/                          # Scripts Python DGI/CFE
│       ├── bmc-team-judge/                       # Evaluación de desempeño
│       ├── bmc-repo-sync-agent/                  # Sincronización de repositorios
│       ├── bmc-api-contract-validator/           # Validación de contratos API
│       ├── bmc-implementation-plan-reporter/     # Planes Solution/Coding
│       ├── bmc-security-reviewer/                # OAuth, CORS, tokens
│       ├── bmc-dashboard-audit-runner/           # Auditoría y diagnóstico
│       │   └── scripts/                          # Script de auditoría
│       ├── bmc-dashboard-debug-reviewer/         # Revisión post-auditoría; DEBUG-REPORT.md
│       ├── bmc-calculadora-specialist/           # Calculadora/BOM/Cotizaciones
│       ├── bmc-parallel-serial-agent/            # Estrategia de ejecución
│       ├── bmc-dashboard-netuy-hosting/          # Deploy VPS Netuy (Uruguay)
│       ├── bmc-dashboard-one-click-setup/        # Setup local completo + versioning
│       ├── super-agente-bmc-dashboard/           # Auditoría integral 9 pasos
│       │   └── scripts/                          # Script de auditoría
│       └── SKILLS-INDEX.md                       # Índice de todos los skills
│
├── docs/
│   ├── team/                               # Coordinación y estado del equipo
│   │   ├── PROJECT-STATE.md               # 📌 FUENTE ÚNICA DE VERDAD
│   │   ├── PROJECT-TEAM-FULL-COVERAGE.md  # Roster del equipo y áreas
│   │   ├── REPO-SYNC-SETUP.md             # Configuración de sincronización
│   │   ├── CAMBIOS-RECIENTES-ARCHIVE.md   # Historial de cambios
│   │   ├── judge/                          # Reportes de evaluación
│   │   │   ├── JUDGE-CRITERIA-POR-AGENTE.md
│   │   │   ├── JUDGE-REPORT-HISTORICO.md
│   │   │   └── JUDGE-REPORT-RUN-*.md      # Reportes por corrida
│   │   ├── fiscal/                         # Supervisión fiscal
│   │   │   └── FISCAL-PROTOCOL-STATE-RANKING.md
│   │   ├── parallel-serial/                # Planes de ejecución paralela/serie
│   │   ├── plans/                          # Roadmap de implementación
│   │   │   └── PLAN-EQUIPO-3-PASOS-SIGUIENTES.md
│   │   └── meta/                           # Meta-evaluación del equipo
│   │
│   └── bmc-dashboard-modernization/        # Documentación de implementación
│       ├── IMPLEMENTATION-PLAN-SOLUTION-CODING.md
│       ├── REPORT-SOLUTION-CODING-run7.md  # Último reporte de implementación
│       └── REPORT-SOLUTION-CODING.md
│
└── README.md                               # Este archivo
```

---

## El equipo: 23 agentes especializados

El equipo está formado por roles dinámicos. Las habilidades y roles no son estáticos — evolucionan a medida que el proyecto crece. Ver [PROJECT-TEAM-FULL-COVERAGE.md](./docs/team/PROJECT-TEAM-FULL-COVERAGE.md) para el roster canónico.

| Rol | Skill | Área | Responsabilidad |
|-----|-------|------|-----------------|
| **Mapping** | `bmc-planilla-dashboard-mapper` | Sheets, Dashboard | Mapeo planilla ↔ interfaz ↔ API |
| **Design** | `bmc-dashboard-design-best-practices` | Dashboard UI | UX/UI, jerarquía, loading/error states |
| **Sheets Structure** | `bmc-sheets-structure-editor` | Sheets | Tabs, dropdowns, estructura (solo Matias) |
| **Networks** | `networks-development-agent` ¹ | Infraestructura | Hosting, endpoints, migración |
| **Dependencies** | `bmc-dependencies-service-mapper` | Todas | Grafo de dependencias, service map |
| **Integrations** | `shopify-integration-v4` ² | Integraciones | Shopify, ML, OAuth, webhooks |
| **GPT/Cloud** | `panelin-gpt-cloud-system` ² | GPT, Cloud Run | OpenAPI, GPT Builder, Cloud Run |
| **Fiscal** | `bmc-dgi-impositivo` | Oversight | Supervisión protocolo, fiscalización, IVA/CFE |
| **Billing** | `billing-error-review` ¹ | Facturación | Errores, duplicados, cierre mensual |
| **Audit/Debug** | `bmc-dashboard-audit-runner` | Auditoría | Logs, diagnóstico, health checks |
| **Debug Reviewer** | `bmc-dashboard-debug-reviewer` | Auditoría | Post-audit analysis; extrae issues/logs por severidad; produce DEBUG-REPORT.md |
| **Reporter** | `bmc-implementation-plan-reporter` | Reporting | Planes Solution/Coding, handoffs |
| **Orchestrator** | `bmc-dashboard-team-orchestrator` | Coordinación | Orden de ejecución, handoffs, diálogo |
| **Contract** | `bmc-api-contract-validator` | API | Validar respuestas contra contrato canónico |
| **Calc** | `bmc-calculadora-specialist` | Calculadora | BOM, precios, Drive, PDF |
| **Security** | `bmc-security-reviewer` | Seguridad | OAuth, tokens, env, CORS, HMAC |
| **Judge** | `bmc-team-judge` | Evaluación | Desempeño, ranking, criterios individuales |
| **Parallel/Serial** | `bmc-parallel-serial-agent` | Estrategia | Qué ejecutar en paralelo vs en serie |
| **Repo Sync** | `bmc-repo-sync-agent` | Repos | Mantiene sincronizados ambos repos |
| **Project Sync** | `bmc-project-team-sync` | Sincronización | Coordinación global del equipo |
| **Netuy Hosting** | `bmc-dashboard-netuy-hosting` | Infraestructura | Deploy en VPS Netuy (Uruguay): PM2/systemd, nginx, HTTPS |
| **One-Click Setup** | `bmc-dashboard-one-click-setup` | DevOps / Setup | Setup local completo + versioning y changelog automatizados |
| **Super Agente** | `super-agente-bmc-dashboard` | Auditoría integral | Auditoría completa de 9 pasos del sistema; produce "REPORTE SUPER AGENTE BMC" |

### Skills cross-cutting (compartidos)

Estos skills están indexados en [`SKILLS-INDEX.md`](./.cursor/skills/SKILLS-INDEX.md) y sus definiciones completas residen en el workspace Calculadora-BMC (repositorio principal). Son recursos compartidos que cualquier miembro del equipo puede invocar:

| Skill | Rol típico | Descripción |
|-------|-----------|-------------|
| `ai-interactive-team` | Todos | Protocolo de diálogo y escalación entre agentes |
| `expert-debug-autonomous` | Audit/Debug, Security | Debugging autónomo avanzado, análisis de errores complejos |
| `google-sheets-mapping-agent` | Mapping | Mapeo profundo de estructuras en Google Sheets |

> ¹ Skill indexado en `SKILLS-INDEX.md` — definición completa en workspace Calculadora-BMC.  
> ² Skill **no indexado** en este repo — definición en workspace Calculadora-BMC. Contactar al Orquestador para obtener acceso.

### Capacidades generales de todos los miembros

- **Nueva habilidad:** Cualquier miembro puede adquirir una nueva habilidad si es aprobada por el Orquestador, usuario o agente afectado.
- **Clonación:** Cualquier miembro puede multiplicarse. Los clones se nombran `Rol`, `Rol+1`, `Rol+2`, etc., para paralelizar trabajo.

---

## Aplicación BMC Dashboard

El dashboard es la aplicación principal que este equipo desarrolla y mantiene, alojada en [bmc-dashboard-2.0](https://github.com/matiasportugau-ui/bmc-dashboard-2.0).

### Puertos

| Puerto | Descripción |
|--------|-------------|
| `3001` | Dashboard principal (canónico) |
| `3849` | Dashboard standalone |
| `5173` | Calculadora / Cotizador (React) |
| `4040` | ngrok (OAuth en desarrollo) |

### Secciones del Dashboard

- **Finanzas** — Resumen financiero, KPIs, trends, breakdown
- **Operaciones** — Calendario de vencimientos, entregas, metas
- **Ventas 2.0** — Tabla de ventas con filtro por proveedor
- **Stock E-Commerce** — KPIs de stock, tabla, export CSV
- **Invoque Panelin** — Integración con GPT / Panelin (placeholder)
- **Audit** — Logs de auditoría del sistema

### Endpoints API (principales)

| Método | Ruta | Descripción |
|--------|------|-------------|
| `GET` | `/api/kpi-report` | Reporte KPI principal |
| `GET` | `/api/ventas` | Datos de ventas (filtros: proveedor, tab) |
| `GET` | `/api/ventas/tabs` | Lista de tabs de ventas disponibles |
| `GET` | `/api/calendario-vencimientos` | Calendario (filtro por mes) |
| `GET` | `/api/stock` | Stock e-commerce |
| `POST` | `/api/cotizaciones` | Crear cotización |
| `PATCH` | `/api/cotizaciones/:id` | Actualizar cotización |
| `POST` | `/api/pagos` | Registrar pago |
| `PATCH` | `/api/pagos/:id` | Actualizar pago |
| `POST` | `/api/ventas` | Registrar venta |
| `PATCH` | `/api/stock/:codigo` | Actualizar stock |

### Google Sheets (fuente de datos)

| Workbook | ID | Descripción |
|----------|-----|-------------|
| Principal | `<YOUR_SHEET_ID>` | CRM_Operativo, Pagos, Metas, AUDIT_LOG |

> El ID real de la planilla es privado. Los contribuidores autorizados lo obtienen de Matias o del archivo `.env` local (variable `BMC_SHEET_ID`).

---

## Configuración y uso

### Prerrequisitos

- Node.js (para el dashboard en `bmc-dashboard-2.0`)
- Python 3.x (para scripts fiscales)
- Cuenta de servicio de Google (credenciales para Sheets/Drive API)
- Cursor IDE (para usar los agentes de IA)

### Variables de entorno (`.env`)

```bash
# Repos para sincronización (bmc-repo-sync-agent)
BMC_DASHBOARD_2_REPO=/path/to/bmc-dashboard-2.0
# o: BMC_DASHBOARD_2_REPO=https://github.com/matiasportugau-ui/bmc-dashboard-2.0.git
BMC_DEVELOPMENT_TEAM_REPO=/path/to/bmc-development-team

# Google Sheets / Drive
BMC_SHEET_ID=<YOUR_SHEET_ID>
GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json

# Otras integraciones (en bmc-dashboard-2.0/.env)
# SHOPIFY_ACCESS_TOKEN=...
# ML_CLIENT_ID=...
# ML_CLIENT_SECRET=...
```

### Ejecutar el equipo completo (Full Team Run)

Este repositorio se usa dentro de **Cursor IDE**. Para ejecutar el equipo completo:

```
"Run full BMC team" / "Equipo completo BMC" / "Equipo completo"
```

El Orquestador leerá la tabla de roles en [PROJECT-TEAM-FULL-COVERAGE.md §2](./docs/team/PROJECT-TEAM-FULL-COVERAGE.md) e incluirá a todos los miembros en el run, en orden según dependencias.

### Sincronizar estado del proyecto

```
"Sync project state" / "Actualizar estado del proyecto"
```

Lee todos los artefactos clave, detecta drift y actualiza `docs/team/PROJECT-STATE.md`.

### Leer el estado actual antes de trabajar

Todo agente debe leer el estado del proyecto antes de comenzar:

```bash
cat docs/team/PROJECT-STATE.md
cat docs/team/PROJECT-TEAM-FULL-COVERAGE.md
```

---

## Scripts de automatización

### Conciliación CFE (fiscal)

Reconcilia comprobantes fiscales (CFE) para análisis tributario IVA/DGI:

```bash
python3 .cursor/skills/bmc-dgi-impositivo/scripts/conciliar_cfe.py \
  --cfe-emitidos dgi_emitidos.xlsx \
  --cfe-recibidos dgi_recibidos.xlsx \
  --periodo 2024-12 \
  --out reporte.json
```

**Parámetros:**
- `--cfe-emitidos` — Archivo Excel con CFE emitidos (DGI)
- `--cfe-recibidos` — Archivo Excel con CFE recibidos (DGI)
- `--periodo` — Período en formato `YYYY-MM`
- `--out` — Archivo de salida JSON

### Extracción mensual CFE

Extrae y consolida datos mensuales de CFE a partir de carpetas de XML de DGI:

```bash
python3 .cursor/skills/bmc-dgi-impositivo/scripts/extraer_cfe_mensual.py \
  --base-dir /ruta/a/carpeta/xml_dgi \
  --year 2024 \
  --out-dir ./salida_cfe_mensual
```

Espera como entrada carpetas con archivos XML emitidos por DGI y genera archivos consolidados por período.

### Script de auditoría (Bash)

```bash
bash .cursor/skills/bmc-dashboard-audit-runner/scripts/run_audit_then_debug.sh
```

### Scripts de estructura de hojas

Los scripts de edición de hojas se ejecutan desde el workspace Cursor (solo Matias). Ver los ejemplos de uso en [`.cursor/skills/bmc-sheets-structure-editor/SKILL.md`](./.cursor/skills/bmc-sheets-structure-editor/SKILL.md).

---

## Estado actual del proyecto

> **Última actualización:** 2026-03-18 (Full team run — post-go-live)
>
> **Score global del equipo:** 4.93/5 (18/19 agentes evaluados — Sheets N/A)

### ✅ Completado

- **KPI Report:** GET `/api/kpi-report` implementado (`bmcDashboard.js` ~L1130)
- **Phase 1 (GET):** 17+ endpoints implementados (Ventas, Calendario, Stock, Cotizaciones, etc.)
- **Phase 2 (PUSH):** Endpoints POST/PATCH + AUDIT_LOG implementados
- **API Contract:** 4/4 PASS — todos los endpoints validados
- **Sheets Mapping:** 5 workbooks documentados
- **Guía usuarios:** Guías rápidas de usuario pendientes de creación (ver pendientes abajo)
- **Repo Sync:** Ambos repos configurados y sincronizados

### ⏳ Pendiente

- **Tabs manuales:** Crear CONTACTOS, Ventas_Consolidado, SHOPIFY_SYNC_AT, PAGADO (responsabilidad Matias)
- **Apps Script Triggers:** 6 triggers de automatización (post-tabs)
- **kpi-report runtime:** Verificar GET `/api/kpi-report` retorna 200 tras restart servidor
- **Deploy producción:** Cloud Run o VPS Netuy (ver [`docs/bmc-dashboard-modernization/IMPLEMENTATION-PLAN-SOLUTION-CODING.md`](./docs/bmc-dashboard-modernization/IMPLEMENTATION-PLAN-SOLUTION-CODING.md) §Fase B)
- **E2E validation:** Checklist de validación pendiente de crear en `docs/team/E2E-VALIDATION-CHECKLIST.md`
- **npm audit fix:** 7 vulns (5 low, 2 moderate en esbuild/vite) — evaluar con Matias

Ver [PROJECT-STATE.md](./docs/team/PROJECT-STATE.md) para el estado detallado y [REPORT-SOLUTION-CODING-run7.md](./docs/bmc-dashboard-modernization/REPORT-SOLUTION-CODING-run7.md) para el último reporte de implementación.

---

## Documentación clave

| Documento | Descripción |
|-----------|-------------|
| [`docs/team/PROJECT-STATE.md`](./docs/team/PROJECT-STATE.md) | 📌 **Fuente única de verdad** — estado del proyecto, cambios recientes, pendientes |
| [`docs/team/PROJECT-TEAM-FULL-COVERAGE.md`](./docs/team/PROJECT-TEAM-FULL-COVERAGE.md) | Roster del equipo, áreas, propagación de cambios |
| [`docs/team/REPO-SYNC-SETUP.md`](./docs/team/REPO-SYNC-SETUP.md) | Configuración de sincronización entre repos |
| [`docs/team/judge/JUDGE-REPORT-HISTORICO.md`](./docs/team/judge/JUDGE-REPORT-HISTORICO.md) | Historial de desempeño del equipo |
| [`docs/team/judge/JUDGE-CRITERIA-POR-AGENTE.md`](./docs/team/judge/JUDGE-CRITERIA-POR-AGENTE.md) | Criterios de evaluación por agente |
| [`docs/bmc-dashboard-modernization/REPORT-SOLUTION-CODING-run7.md`](./docs/bmc-dashboard-modernization/REPORT-SOLUTION-CODING-run7.md) | Último reporte de implementación |
| [`docs/bmc-dashboard-modernization/IMPLEMENTATION-PLAN-SOLUTION-CODING.md`](./docs/bmc-dashboard-modernization/IMPLEMENTATION-PLAN-SOLUTION-CODING.md) | Plan de tareas y ownership |
| [`docs/team/fiscal/FISCAL-PROTOCOL-STATE-RANKING.md`](./docs/team/fiscal/FISCAL-PROTOCOL-STATE-RANKING.md) | Prioridades y ranking de riesgos fiscales |

---

## Repos relacionados

| Repo | URL | Descripción |
|------|-----|-------------|
| **bmc-dashboard-2.0** | [github.com/matiasportugau-ui/bmc-dashboard-2.0](https://github.com/matiasportugau-ui/bmc-dashboard-2.0) | Código fuente del dashboard (Node.js, React) |
| **bmc-development-team** | [github.com/matiasportugau-ui/bmc-development-team](https://github.com/matiasportugau-ui/bmc-development-team) | Este repositorio (equipo y documentación) |

---

## Protocolo del equipo

### Antes de trabajar

1. Leer [`docs/team/PROJECT-STATE.md`](./docs/team/PROJECT-STATE.md) (cambios recientes, pendientes)
2. Leer los artefactos del área correspondiente y áreas que la afectan
3. Resolver pendientes de sincronización que involucren al agente antes de comenzar

### Después de un cambio

1. Actualizar `docs/team/PROJECT-STATE.md`:
   - Nueva fila en "Cambios recientes"
   - Si afecta a otros: añadir ítem en "Pendientes" o escribir `Log for [Agente]`
2. Si aplica: ejecutar Repo Sync para propagar artefactos a ambos repos

### Supervisión

El agente **Fiscal** (`bmc-dgi-impositivo`) supervisa que el equipo cumpla este protocolo según el ranking de criticidad en [`FISCAL-PROTOCOL-STATE-RANKING.md`](./docs/team/fiscal/FISCAL-PROTOCOL-STATE-RANKING.md). Si detecta incumplimientos, comunica a los involucrados para que no vuelvan a ocurrir.

---

*Generado por el equipo BMC Development Team · Uruguay · 2026*
