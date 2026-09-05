# Matriz de cumplimiento global — Subdocumento 4

**Propietario de consolidación:** Frente 3 / integrador designado.  
**Regla:** cada frente actualiza su traza; esta matriz se actualiza en las puertas de integración y al registrar un cambio de línea base de Célula 2, como la presente alineación previa al desarrollo.

## 1. Cobertura del Subdocumento 4

| ID | Obligación | Paquete primario | Paquetes de apoyo | Evidencia esperada | Estado |
|---|---|---|---|---|---|
| `SD4-01` | capas, módulos, contextos, responsabilidades e interfaces | A1 | A2, A3, D1 | esquemas + catálogo | PENDIENTE |
| `SD4-02` | físico híbrido y Art. 16 por componente | C1 | C2, C4, D1 | físico + tabla emplazamiento | PENDIENTE |
| `SD4-03` | servicios, contratos, mensajería, versionado y gobierno | A2 | A3, D1 | matriz/diagrama integración | PENDIENTE |
| `SD4-04` | Zero Trust, exposición, identidad, cifrado y controles | D1 | D2, A1, C3 | D1 B1–B7 y matriz SEC-*; diagramas, amenazas, cruce físico y pruebas pendientes | EN CURSO |
| `SD4-05` | ambientes, redes, HA, DR y respaldos | C3 | A3, C1, D1 | despliegue/continuidad | PENDIENTE |
| `SD4-06` | volumen, concurrencia, crecimiento y capacidad | C4 | A2, C2 | cálculos reproducibles | PENDIENTE |
| `SD4-07` | ADR con alternativas y selección | D2 | todos | registro ADR | PENDIENTE |
| `SD4-08` | arquitectura específica del Caso 06 | D3 | todos | auditoría de especificidad | PENDIENTE |

## 2. Cobertura formal 4.1 y 4.2

| ID | Elemento formal | Archivo destino | Paquete | Estado |
|---|---|---|---|---|
| `T21-4.1-A` | Esquema de solución | Consolidado 4.1.1 | A1 | PENDIENTE |
| `T21-4.1-B` | Arquitectura lógica | Consolidado 4.1.2–4.1.8 | A1/A2/A3/D1 | PENDIENTE |
| `T21-4.2-A` | Arquitectura física | Consolidado 4.2.1–4.2.2 | C1 | PENDIENTE |
| `T21-4.2-B` | Tecnologías de software | Consolidado 4.2.3 | C2 | PENDIENTE |
| `T21-4.2-C` | Implementos hardware/software | Consolidado 4.2.4 | C2/C4/D1 | PENDIENTE |
| `T21-4.2-D` | Data center primario | Consolidado 4.2.5 | C2 | PENDIENTE |
| `T21-4.2-E` | Data center secundario | Consolidado 4.2.6 | C2/C3 | PENDIENTE |
| `T11` | Formulario cinco columnas | `90_Consolidado/02_FORMULARIO_T11_FINAL.md` | C4 + todos | PENDIENTE |

## 3. Matriz de trazabilidad integradora

Agregar una fila por afirmación verificable o agrupación homogénea. No usar una sola fila para todo un entregable.

**Corte de entrada:** Célula 2 `c4756df`. Las filas nuevas reflejan obligaciones recibidas, no cumplimiento de arquitectura. Los identificadores B/C remiten a los anexos de segunda/tercera ronda del [cierre de Célula 2](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md); los RF/RNF/RN se consultan en los catálogos vigentes enlazados en el Maestro §21.

| TRZ global | Fuente oficial | MC/Decisión | RF/RNF/RN | Obligación SD4 | Paquete/sección | Comp. lógico | Nodo físico | Control | Diagrama | T-11 | Evidencia/estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `GTR-001` | Caso 06 Cap. 10/15 | MC-09 | RNF-DIS-02/04 | SD4-02/05 | A3, C1, C3, C4 | EDGE-RUN | POR DEFINIR | continuidad | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-002` | FEP02 Cap. 2 §2.1 — capas obligatorias | — | obligación directa BTT; no existe categoría RNF-ARQ en C2 | SD4-01 | A1 | todas las capas | n/a | transversal | POR DEFINIR | n/a | PENDIENTE |
| `GTR-003` | Caso 06 Cap. 5/16 | MC-07/08 | RF-CON-13/14 | SD4-01/03/07 | A2/A3 | INT-TOS | POR DEFINIR | idempotencia | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-004` | BTT Cap. 11/12 | MC-04 | RNF-SEG-10/USA-04 | SD4-04 | D1 | SRV-IAM | POR VALIDAR C1–C3 | D1 B1/B2 SEC-IAM-01 / SEC-ADM-01 | POR CREAR B8 | SEC-PHYS-v0.1 listo; C4 asigna fila | EN CURSO |
| `GTR-005` | Caso 06 Cap. 6/15 | MC-10/11 | RNF-DIS-11 | SD4-02/05/06 | C1/C2/C3/C4 | EDGE-RUN | patio/gate | red/marino | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-006` | Caso 06 Cap. 13/18; FEP02 Cap. 5 RT-05.06 (exportación) | MC-23/24/25; C2 B9 | RF-INT/NAV/EMI; RF-EMI-06 | SD4-03/06/08 | A2/A3/C4 | CTX-VESSEL/EMIS | POR DEFINIR | integración | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-007` | FEP02 §9.1; Cap. 9 RT-09.06/07 | C2 B1 | RNF-DES-09..12 | SD4-01/04/06 | A1/A2/C4/D1 | POR DEFINIR | POR DEFINIR | presupuesto de latencia y carga con seguridad | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-008` | FEP02 Cap. 7 RT-07.04/06/07; FEP01 Art. 20 | C2 B1 | RNF-DIS-13/15 | SD4-05 | C3/D2 | POR DEFINIR | POR DEFINIR | RTO/RPO y DR real; preserva exigencia específica sin pérdida | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-009` | FEP02 Cap. 7 RT-07.09..12; FEP01 Art. 20 | C2 B1 | RNF-DIS-14 | SD4-04/05 | C2/C3/D1 | repositorios + SEC-KEY-01 / SEC-BKP-01 | POR VALIDAR C1–C3 | D1 B4.5/B4.7; cifrado, separación y restauración mensual | POR CREAR B8 | condición de plataforma de respaldo; C4 pendiente | EN CURSO |
| `GTR-010` | Caso 06 Anexo A, §7.1 y Cap. 18 criterio 13; FEP02 Cap. 5 RT-05.22 | C2 B2/C3 | RF-POR-09; RF-POR-02; RF-INT-02 | SD4-01/03/04 | A1/A2/D1; Subdoc. 5 | CH-PORTAL/SRV-IAM | POR VALIDAR A1/C1 | D1 B1/B2; flujos y actores separados; 41 % solo instrucción embarcador/agencia | POR CREAR B8 | IAM/borde candidatos; C4 pendiente | EN CURSO |
| `GTR-011` | Caso 06 Cap. 15 RT-05.29 | C2 B3/B4/C1/C2/C6; Decisión 8 | RF-REF-04; RF-REF-07; RN-11 | SD4-04/05/08 | A3/C3/D1/D2; Subdoc. 5 | CTX-REEFER | POR VALIDAR A3/C1–C3 | D1 B5.2/B5.3 conserva alarma operacional y correlación de manipulación | POR CREAR B8 | SIEM/EDR candidatos; lógica/tiempo A3/C3 pendientes | EN CURSO |
| `GTR-012` | Caso 06 §14.2; volumetría C2 filas 15/16 y factor estacional | C2 B5 | RNF-DIS-02/04; RNF-DES-12 | SD4-05/06 | C3/C4 | EDGE-RUN | POR DEFINIR | estacionalidad y sincronización con holgura | POR DEFINIR | POR DEFINIR | PENDIENTE |
| `GTR-013` | Caso 06 §17.1/17.2 y Cap. 18; catálogo C2 parte 3 §11.2 | C2 B11/C4/C7 | RF-NAV-03; RF-NAV-12; RF-INS-07 | SD4-08 | A3/C4/D3 | POR DEFINIR | POR DEFINIR | prueba funcional separada de logro operacional; hito 2029 vigente | POR DEFINIR | n/a | PENDIENTE |
| `GTR-014` | FEP02 Cap. 11 RT-11.17; Caso 06 Cap. 10 restricción 11 | obligación directa de Bases | RNF-OPE-08 apoyo | SD4-04/05 | D1/C3/C4 | SEC-SOC-01 / SEC-IR-01 | servicio gestionado; ubicación POR VALIDAR | D1 B5.4/B5.8 ADR-010 C propuesta; dotación/procedimientos pendientes | POR CREAR B8 | SEC-PHYS-v0.1; fila/cantidad C4 pendientes | EN CURSO |
| `GTR-015` | Caso 06 Cap. 8 y §17.1; registro C2 §C.1/C.2 y narrativa §3.11 | C2 B6/B7/B8 | supuestos S1..S5 y A..L; sin RF nuevo | SD4-07/08 | A1/A3/C3/D1/D3 | ACT-GATE/ACT-MANT/ACT-AGE | n/a | actores, seis tensiones y supuestos con fundamento; tensión 1 abierta | POR DEFINIR | n/a | PENDIENTE |
| `GTR-016` | Caso 06 Cap. 18 criterios 8/10; trazabilidad C2 parte 2 | C2 B10 | RF-PAT-10 | SD4-08 | A3/C4/D3 | CTX-YARD | POR DEFINIR | remociones anticipadas y relación con inspecciones | POR DEFINIR | POR DEFINIR | PENDIENTE |

## 4. Estándares, marcos y certificaciones exigidos

**Regla:** no basta mencionar el estándar. Cada fila debe terminar en un control concreto y una evidencia. Los condicionales se marcan `NO APLICA` con justificación; no se eliminan silenciosamente.

| ID | Estándar/marco exigido | Aplicabilidad en el caso | Paquete responsable | Control y evidencia esperada | Estado |
|---|---|---|---|---|---|
| `STD-01` | ISO/IEC 27001 e ISO 9001 | certificación institucional | D3 coordina; evidencia Célula 1/equipo | certificado o vía admitida por Bases; alcance y vigencia | BLOQUEADO EXTERNO |
| `STD-02` | ISO/IEC 27002, 27017 y 27018 | controles de seguridad, nube y datos personales | D1/D2 | D1 matriz SEC-* y B7.3 SEC-GOV-01 / SEC-CLOUD-01; mapeo/evidencia final pendientes | EN CURSO |
| `STD-03` | NIST CSF 2.0 y NIST SP 800-207 | gobierno de ciberseguridad y Zero Trust | D1/D2 | D1 B1–B3/B7.3; funciones CSF completas, amenazas y vista pendientes | EN CURSO |
| `STD-04` | OWASP ASVS 4.0 L2, Top 10, API Security Top 10 y SAMM | software, APIs y proceso seguro | D1/C3 | D1 B3.3/B6.2/B6.7; herramientas/configuración/pruebas pendientes | EN CURSO |
| `STD-05` | CIS Benchmarks | nube, servidores, edge y endpoints | D1/C2/C3 | D1 B7.3 SEC-HARD-01; productos/versiones/baselines/pruebas pendientes | EN CURSO |
| `STD-06` | SLSA 3+, CycloneDX o SPDX y firma de artefactos | cadena de suministro de software | D1/C3 | D1 B6.3/B6.7; plataforma, procedencia, SBOM/firma ejecutadas pendientes | EN CURSO |
| `STD-07` | ISO 22301 e ISO/IEC 27031 | continuidad de negocio y TIC | C3/D1 | BIA, escenarios, RTO/RPO, DR, procedimientos y pruebas | PENDIENTE |
| `STD-08` | ISO/IEC 20000-1, ITIL 4 y SRE | operación y gestión del servicio | C3/D3 | modelo operativo, SLO/SLI, incidentes, cambios y evidencia | PENDIENTE |
| `STD-09` | ISO/IEC 25010, ISO/IEC 25012 e ISO/IEC/IEEE 29119 | calidad de software, datos y pruebas | A1/C3/C4; cruce Subdoc. 5/T-13 | atributos/umbrales, calidad de datos y estrategia de prueba | PENDIENTE |
| `STD-10` | ISO/IEC/IEEE 42010 y TOGAF o equivalente declarado | descripción y gobierno de arquitectura | A1/D2/D3 | cinco vistas, interesados, decisiones y gobierno ADR | PENDIENTE |
| `STD-11` | WCAG 2.2 AA y EN 301 549 | portal, app y terminales | A1/D1; cruce UX | D1 B3.4 preserva accesibilidad ante bots; diseño/informe UX completos pendientes | EN CURSO |
| `STD-12` | OpenAPI 3.1, AsyncAPI 2.6+ y estándares marítimos | contratos síncronos, eventos y navieras | A2 | contratos versionados; BAPLIE/COPRAR/COARRI/CODECO | PENDIENTE |
| `STD-13` | OpenTelemetry, STRIDE e ISO 31000 | observabilidad, amenazas y riesgo | D1/D2 | D1 B5 correlación; STRIDE/riesgo D2 y evidencia pendientes | EN CURSO |
| `STD-14` | OIDC, OAuth 2.1, SAML 2.0, LDAP y FIDO2 cuando corresponda | identidad e interoperabilidad IAM | D1 | D1 B2.2/B2.3/B2.7; directorio/producto/federación/pruebas pendientes | EN CURSO |
| `STD-15` | TLS 1.3 y respaldo 3-2-1-1-0 | comunicaciones y continuidad | D1/C3 | D1 B3.4/B4.5/B4.7; configuración/ubicación/restauración pendientes | EN CURSO |
| `STD-16` | NCh Elec. 2777 y NCh 2527 | sala/equipos eléctricos y ergonomía de puestos | C2 | memoria eléctrica y checklist ergonómico | PENDIENTE |
| `STD-17` | ISO 14001, PUE, ISO 14083/GLEC e ISO 14064-3 | sostenibilidad, energía y emisiones del caso | C2/C4; cruce Subdoc. 3/5 | métricas, instrumentación y reporte verificable | PENDIENTE |
| `STD-18` | NIST AI RMF 1.0 e ISO/IEC 42001 | solo si la solución incorpora IA | A1/D1/D2 | declarar uso y controles; si no existe IA, `NO APLICA` justificado | PENDIENTE |
| `STD-19` | PMBOK y prácticas ágiles justificadas | gobierno del trabajo, no componente arquitectónico | D3; cruce gestión | trazabilidad de decisiones, cambios y entregables | PENDIENTE |
| `STD-20` | IEC 62443 | segregación de red operacional/protección | C3/D1 | D1 B3.1–B3.3 SEC-NET-01; topología/aprobación/prueba C3 pendientes | EN CURSO |

La normativa chilena y sectorial se controla por aplicabilidad en los entregables respectivos; este bloque no reemplaza la revisión legal. Son especialmente relevantes protección de datos, Ley Marco de Ciberseguridad/OIV, firma electrónica, delitos informáticos, régimen aduanero, ISPS, SOLAS/VGM, IMDG, normativa laboral portuaria y seguridad y salud en el trabajo.

## 5. Control 1:1 físico–T-11

| ID físico | Componente/nodo | Justificación Art. 16 | Cálculo/cantidad | Seguridad | Fila T-11 | Estado |
|---|---|---|---|---|---|---|
| `POR DEFINIR` | — | — | — | — | — | PENDIENTE |

## 6. Control de pendientes externos

| ESC | Afecta | Diseño conservador/fallback | ¿Impide entregar? | Evidencia |
|---|---|---|---|---|
| ESC-01..14 | ver Maestro §18 | completar durante desarrollo | No, si queda explícito y existe tratamiento | PENDIENTE |
