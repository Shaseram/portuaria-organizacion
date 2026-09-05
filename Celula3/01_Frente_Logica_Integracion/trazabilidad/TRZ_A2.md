# TRZ-A2 — Arquitectura de integración

## Trazabilidad de contrapartes, contratos y decisiones

| ID | Fuente primaria | MC/decisión | RF/RNF | Contraparte/contrato | Decisión/patrón | Sección/diagrama | T-11 candidato | Estado |
|---|---|---|---|---|---|---|---|---|
| `TRZ-A2-001` | Caso 06 Cap. 5 (destino: "decisión del proponente"), Cap. 16.1 N°1; Maestro §8 | Decisión 1; MC-07/08 | RF-CON-13/14 | `EXT-TOS12` | Envolver + sustitución progresiva; bidireccional, idempotente, autoridad dominio×zona×fase | §2.1 | gateway/broker anticorrupción | `BLOQUEADO EXTERNO` |
| `TRZ-A2-002` | Caso 06 Cap. 5 ("se mantiene, único emisor tributario"), Cap. 4.8 | — | RF-FAC-01..11; RF-FIR-01 (firma) | `EXT-ERP` | Evento asíncrono con confirmación; conciliación 1:1 | §2.1 | adaptador batch/API | Definido (patrón); contrato `POR LEVANTAR` |
| `TRZ-A2-003` | Maestro §4.4 restricción 14; Caso 06 Cap. 18 criterio 20 | MC-21 | RNF-DIS | `EXT-CON` (Concedente) | Salida unidireccional de indicadores desde `DATA-AN`, trazable sin reconstrucción | §2.1 | adaptador de reporte | Definido (patrón); canal `POR LEVANTAR` |
| `TRZ-A2-004` | Caso 06 Cap. 2.2 (participación ferrocarril 15%); Maestro §7 | MC-21 | RF-INT-10 | `EXT-FER` | Asíncrono con reenvío; sin acoplar `CTX-GATE`/`CTX-YARD` a su disponibilidad | §2.1 | por definir | `BLOQUEADO EXTERNO` (`ESC-06`, `F1-ESC-001`) |
| `TRZ-A2-005` | Caso 06 Cap. 4.7, Cap. 12 (Aduana/SAG/autoridad sanitaria) | MC-21 | RF-INS-01..07 | `EXT-AUT-ADU`, `EXT-AUT-SAG`, `EXT-AUT-SAN` | Interfaz si existe; canal asistido trazable si no; sin bloquear el gate | §2.1 | por definir | `BLOQUEADO EXTERNO` (`ESC-14`) |
| `TRZ-A2-006` | Caso 06 Cap. 2.2 (14 navieras, alianza 34%), Cap. 4.1-4.2, Cap. 13.1-13.2; Maestro §7, §14 | Decisión 18; MC-20/23 | RF-NAV-01..14 | `CP-NAV-01`…`CP-NAV-14` | EDIFACT versionado por naviera; puente asistido transitorio solo para no-alianza | §2.1, §3 | adaptador EDIFACT por naviera | `EN CURSO` (contratos individuales `POR LEVANTAR`) |
| `TRZ-A2-007` | Maestro §7 (7 familias); Caso 06 Cap. 2.3, Cap. 4.4-4.5 | MC-12 | RNF-DIS-11 | `EXT-GRU`, `EXT-ACC`, `EXT-VMS`, `EXT-VGM`, `EXT-OCR`, `PER-REEFER`, `PER-EQPOS` | Solo lectura (grúas); metadatos/evidencia confirmados (VMS); instrumentación remota nueva (reefer/equipos) | §2.2 | instrumentación/adaptadores (C2/C4) | Mixto — ver Estado por fila §2.2 |
| `TRZ-A2-008` | Decisión 18 (Célula 2); Maestro §19 regla 17; Caso 06 Cap. 4.1-4.3, 4.6 | Decisión 18 | RF-NAV-01..14 | BAPLIE/COPRAR/COARRI/CODECO | Mapeo 1:1 mensaje↔evento de dominio A1 §4.3; COARRI≠CODECO | §3 | — | Definido |
| `TRZ-A2-009` | BTT RT-02.06/07/08/09; RT-05.19/21/22; Maestro §6.2 | — | RNF-DIS-09 | Todas | Timeout, backoff+jitter, breaker, bulkhead, rate limit, idempotencia, orden, correlación E2E, degradación informada, carga masiva con error por registro | §4 | — | Definido |
| `TRZ-A2-010` | Maestro §8, §19 regla 14; Caso 06 Cap. 13.1 (objeción gerenta comercial) | Decisión 1 | — | Todas (tabla de fallos) | Fallback y recuperación explícitos por contraparte, sin ocultar SPOF | §5 | — | Definido |
| `TRZ-A2-011` | A1 §4.1-4.2 (dependencias permitidas/prohibidas) | — | — | Diagrama de integración | Todo `EXT-*`/`CP-NAV-*`/`PER-*` entra/sale solo por `INT-HUB`/`INT-TOS` | §6 | — | Definido |
| `TRZ-A2-012` | Maestro §7, §17 (Decisión 18); BTT §2.3, RT-05.16-21; Caso 06 Cap. 4, 5, 12, 13.1-13.2 | Decisión 18; MC-23 | RNF-DIS, RNF-SEG | `ADR-003` | Bus de eventos con adaptador por contraparte; descarta punto a punto y ESB pesado | §7 | integración/broker | Propuesto |
| `TRZ-A2-013` | BTT RT-05.16/17/18/20/24 | — | RNF-DIS | Gobierno de contratos | Catálogo único, versionado semántico, OAuth 2.1/mTLS, anticorrupción obligatoria, portal deseable | §1.2 | — | Definido |
| `TRZ-A2-016` | BTT RT-05.09 | — | — | Datos maestros sin duplicación con sistemas externos | Columna "Dueño del dato" de §2.1/§2.2 es la estrategia MDM exigida; un solo código ISO 6346 en OCR/EDIFACT/CTX-OPS | §1.2 | — | Definido |
| `TRZ-A2-014` | Maestro §19 regla 17 | — | — | Cuatro capas: evento/documento/mensaje/sobre de red | Distinción explícita para no confundir cambio de transporte con cambio de versión EDIFACT | §1.3 | — | Definido |
| `TRZ-A2-015` | BTT RT-05.23, RT-13.12; Caso 06 Cap. 15 (parámetro "Estándares sectoriales") | — | — | ISO 6346 (codificación de contenedor) + bilingüe ES/EN obligatorio hacia navieras/mensajería marítima | Mismo código ISO 6346 en EDIFACT, `EXT-OCR` y A1 §5.1; ES/EN endurecido de Deseable a Obligatorio por el caso | §3 | — | Definido |

## Trazabilidad de exclusiones y restricciones heredadas de A1/Maestro

| ID | Restricción | Fuente | Sección A2 |
|---|---|---|---|
| `TRZ-A2-R01` | ERP conserva emisión tributaria; sin doble emisor | Maestro §4.5, §5.2; Caso 06 Cap. 11 | §2.1 (`EXT-ERP`) |
| `TRZ-A2-R02` | Grúas de muelle: solo lectura, sin intervenir control | Maestro §4.4 restricción 3; Caso 06 Cap. 10 N°3 | §2.2 (`EXT-GRU`) |
| `TRZ-A2-R03` | VMS/CCTV: eventos/metadatos/evidencia confirmados; no portal de video | Maestro §19 regla 6; A1 §1.3 | §2.2 (`EXT-VMS`) |
| `TRZ-A2-R04` | Autoridades: interfaz si existe; canal asistido trazable si no; no se inventan APIs | Maestro §19 regla 9; Caso 06 Cap. 12 | §2.1 (`EXT-AUT-*`) |
| `TRZ-A2-R05` | Alianza 2029: cero redigitación ni puente desde vigencia efectiva | Maestro §14; Decisión 23; Caso 06 Cap. 13.2 | §2.1, §3 (`CP-NAV-*`) |
| `TRZ-A2-R06` | Radio: adaptador al medio existente, no sistema nuevo sin fundamento | Maestro §19 regla 9 (análoga); A1 §1.3 (`EXT-RAD`) | Heredado de A1; no es contraparte de A2 |

Agregar filas si se identifican nuevas afirmaciones arquitectónicas o nuevas contrapartes. No citar códigos RT sin documento y materia.
