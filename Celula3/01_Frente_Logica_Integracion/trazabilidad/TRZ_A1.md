# TRZ-A1 — Contexto y arquitectura lógica

## Trazabilidad de componentes y decisiones

| ID | Fuente primaria | MC/decisión | RF/RNF/RN | Afirmación arquitectónica | Sección A1 | Salida a otro frente | Estado |
|---|---|---|---|---|---|---|---|
| `TRZ-A1-001` | BTT Cap. 2, num. 2.1, RT-02.01 | — | RNF arquitectura | Ocho capas obligatorias con presentación, borde, gateway, negocio, integración, datos, seguridad y observabilidad, con diagrama, componentes e interfaces por capa | §2, §2.1, §2.2 | C1/D1 | PARA REVISIÓN |
| `TRZ-A1-002` | Caso 06 Cap. 5/16; Maestro §8 | MC-07/08 | RF-CON-13/14 | Capa anticorrupción TOS 2012 con autoridad por dominio×zona×fase e INT-TOS separable | §2.2 (Capa 5), §6.2 ADR-001 | A3/C1/D2 | PARA REVISIÓN |
| `TRZ-A1-003` | Caso 06 Cap. 15 RT-17.01; Maestro §3 | MC-01 | RF-APP-01 | App instalable única con cuatro perfiles y offline cifrado para internos (CH-APP) | §1.1, §2.2 (Capa 1) | C1/D1 | PARA REVISIÓN |
| `TRZ-A1-004` | BTT RT-16.31/32/33/34, RT-13.12 (obligación transversal) + CP, Cap. 15, RT-16.30 (parámetro del caso, "Portal público") — mismo código en dos documentos, ambos exigibles y acumulativos, no alternativos (Célula 2, `Registro_supuestos_v3.md` Supuesto M); Maestro §3 | MC-06 | RF-POR-01..08 (capa pública sin auth, registro autoservido, consulta autenticada, segregación por contraparte, objeción de factura, cita de inspección, idioma persistente, autoatención) | Portal público/autenticado con contenido exacto del caso (consulta sin auth, citas/objeciones/curva de temperatura con auth), bilingüe, resistente a picos, con umbrales de desempeño `RNF-DES-09` (CH-PORTAL) | §1.1, §2.2 (Capa 1) | D1 | PARA REVISIÓN |
| `TRZ-A1-005` | Caso 06 Caps. 14/16; Maestro §5 | MC-12/21 | RF-INT-10 | 16 actores y 11 sistemas externos/conservados identificados con límites | §1.2, §1.3, §1.4 | A2/D2 | PARA REVISIÓN |
| `TRZ-A1-006` | Caso 06 Cap. 7; Maestro §4.1 | — | RF-CON-01..14 | Núcleo operacional (CTX-OPS) como agregado central de contenedor, movimiento y posición | §2.2 (Capa 4), §3.1 | C1/C4 | PARA REVISIÓN |
| `TRZ-A1-007` | Caso 06 Cap. 6; Maestro §4.2 | — | RF-GAT-01..16 | Gate y citas (CTX-GATE) con prevalidación, cola virtual, excepciones y ≤120 s por camión; `RF-GAT-14` cubre la operación del gate sin enlace exterior | §2.2 (Capa 4), §3.1 | C1/C4 | PARA REVISIÓN |
| `TRZ-A1-008` | Caso 06 Caps. 7/14, Cap. 18 criterios 8/10; Maestro §4.2 | MC-15 | RF-PAT-01..13, con `RF-PAT-10` (programación anticipada de remociones) explícito en criterios 8 y 10 (corrección de Célula 2, antes ausente de esa trazabilidad) | Patio y posición (CTX-YARD) con verificación cruzada, ≤0,5 % por verificar y remoción anticipada programada | §2.2 (Capa 4), §3.1 | C1/C4 | PARA REVISIÓN |
| `TRZ-A1-009` | Caso 06 Cap. 7; Maestro §4.2, §17 | Decisión 8, 10 (reefer con muestreo local/agregado y alarma escalada; el 9 intermedio es red celular privada, no reefer) | RF-REF-01..13 | Reefer y telemetría (CTX-REEFER) con alarma ≤5 min, 2.400/2.900 tomas y series temporales | §2.2 (Capa 4), §3.1 | C1/C4/D1 | PARA REVISIÓN |
| `TRZ-A1-010` | Caso 06 Cap. 7; Maestro §4.2, §17 | Decisión 4-5 (planificación propone/aprueba/corrige y captura motivos) | RF-NAV-06..09 (propuesta de plan, aprobación/corrección, registro de reglas del planificador — no existe prefijo `RF-PLN`; el catálogo real agrupa esto bajo `RF-NAV`) | Planificación (CTX-PLAN) con captura de reglas tácitas y propuesta/corrección/aprendizaje | §2.2 (Capa 4), §3.1 | C1 | PARA REVISIÓN |
| `TRZ-A1-011` | Caso 06 Cap. 7; Maestro §14 | MC-20/23 | RF-NAV-01..05, 12..14 (recalada, sitios, ventana, notificación, estimación, productividad, sobretiempo, replanificación por VGM). `RF-NAV-06..09` es de `CTX-PLAN` (`TRZ-A1-010`); `RF-NAV-10..11` es de `CH-CAB` (`TRZ-A1-029`) — un mismo prefijo del catálogo de Célula 2, tres bounded contexts distintos en A1, sin doble conteo | Nave y mensajería (CTX-VESSEL) con BAPLIE/COPRAR/COARRI/CODECO y ventana ≥72 h | §2.2 (Capa 4), §3.1 | A2/C1 | PARA REVISIÓN |
| `TRZ-A1-012` | Caso 06 Cap. 7; Maestro §4.7 | MC-05 | RF-FAC-01..11; RF-FIR-01 (firma, compartido con `SRV-EVID`) | Evidencia facturable (CTX-BILL) con cuatro actos de firma y entrega al ERP | §2.2 (Capa 4), §3.1 | A2/D1 | PARA REVISIÓN |
| `TRZ-A1-013` | Caso 06 Cap. 7; Maestro §4.7, §17 | Decisión 21 (inspecciones programadas con remoción anticipada y acta) | RF-INS-01..07 | Inspecciones (CTX-INSP) con remoción anticipada y acta firmada | §2.2 (Capa 4), §3.1 | A2/D1 | PARA REVISIÓN |
| `TRZ-A1-014` | Caso 06 Cap. 7; Maestro §14, §17 | Decisión 16-17 (emisiones ISO 14083/GLEC e instrumentación real); MC-25 | RF-EMI-01..06 | Energía y emisiones (CTX-EMIS) con ISO 14083 y verificación efectiva por tercero | §2.2 (Capa 4), §3.1 | C4 | PARA REVISIÓN |
| `TRZ-A1-015` | BTT RT-11.01, RT-12.02/03/05/06/10/11; Maestro §11 | MC-04 | RNF-SEG-01..11 | Identidad y autorización (SRV-IAM) con Zero Trust (RT-11.01), SSO, MFA, RBAC+ABAC (RT-12.05), PAM (RT-12.06), baja ≤24 h (RT-12.10) y credencial de eventuales adecuada al perfil operacional de terreno sin biometría obligatoria (RT-12.11, Según caso) | §2.2 (Capa 7), §3.1 | D1 | PARA REVISIÓN |
| `TRZ-A1-016` | Caso 06 Cap. 14; Maestro §7; BTT RT-02.07 | MC-12 | RF-INT-01..11 | Hub de integración (INT-HUB) con 21 contrapartes + 7 familias, gobierno de contratos, entrega al menos una vez y orden garantizado por partición/agregado | §2.2 (Capa 5), §3.1 | A2/C4 | PARA REVISIÓN |
| `TRZ-A1-017` | Caso 06 Cap. 14; Maestro §9 | — | RNF-DIS-02/04/09/12 | Runtime local (EDGE-RUN) con autonomía 72 h y resincronización ≤90 min | §2.2 (transversal), §3.2 | C1/C3 | PARA REVISIÓN |
| `TRZ-A1-018` | Maestro §3, §4.4, §9, §19; BTT RT-02.02/03/04/14; Caso 06 Cap. 17.4 punto 14 | Decisiones 1-21 | RNF-DIS, RNF-SEG | ADR-001: Núcleo Modular Híbrido + Edge como estilo arquitectónico, con comparación de 3 estilos, crecimiento por parametrización (cuarto sitio/grúas/tomas) sin rediseño; acredita RT-02.14 (Deseable) vía capa anticorrupción y estrangulamiento progresivo del TOS | §6.1, §6.2 | Todos | PARA REVISIÓN |
| `TRZ-A1-019` | BTT RT-14.01/08; RT-16.06-08; Maestro §6 | — | RNF observabilidad | Observabilidad con OpenTelemetry (RT-14.01) correlacionada nube/on-premise, retención declarada (RT-14.08), logs de auditoría inalterables no modificables/eliminables por ningún perfil, consulta con filtros y SIEM | §2.2 (Capa 8) | C3/D1 | PARA REVISIÓN |
| `TRZ-A1-020` | Maestro §5.2; Caso 06 Cap. 5 | MC-02 | — (VMS es sistema conservado sin RF propio en el catálogo de Célula 2; no existe prefijo `RF-VMS`) | VMS conservado; solo eventos/metadatos/evidencia confirmados; no portal de video | §1.3 | A2/D1 | PARA REVISIÓN |
| `TRZ-A1-021` | BTT RT-16.20 (obligación transversal, ≥3 canales) + CP, Cap. 15, RT-16.21 (parámetro del caso, canales por tipo de alerta) — mismo código en dos documentos, ambos exigibles (Supuesto M); Maestro §3; Caso 06 Cap. 16.1 (pendiente N° 10) | MC-03 | RF-REF-08..10 (instancia verificada: notificación simultánea, escalamiento automático, registro auditable de confirmación — específica de reefer; no existe prefijo `RF-NOT` transversal para notificaciones en el catálogo) | Notificaciones compartidas (SRV-NOTIF) con adaptadores de canal, canal redundante reefer y escalamiento automático a supervisor si nadie confirma | §2.2 (Capa 4), §3.1 | A2 | PARA REVISIÓN |
| `TRZ-A1-022` | Maestro §16; Caso 06 Cap. 16; BTT RT-05.05 | MC-26 | — (no existe prefijo `RNF-DAT` en el catálogo de Célula 2; el requisito real de separación transaccional/analítica es `BTT RT-05.05`) | Cuatro tipos de persistencia separados por naturaleza del dato (CORE/TS/DOC/AN) | §2.2 (Capa 6), §3.2 | C2/C4 | PARA REVISIÓN |
| `TRZ-A1-023` | Maestro §6.2; BTT RT-02.06/08/09 | — | RNF-DIS-09 | Reglas de comunicación: idempotencia, timeout, backoff, circuit breaker, deduplicación y degradación elegante informada a la persona usuaria (nunca falla total) | §2.3 | A2 | PARA REVISIÓN |
| `TRZ-A1-024` | Maestro §4.5; §19 | — | — | Exclusiones: no reemplazar ERP, no intervenir grúas, no comprar hardware, etc. | §1.5 | D3 | PARA REVISIÓN |
| `TRZ-A1-025` | Maestro §9.1 | — | RNF-DIS-02/04 | Cinco funciones críticas de continuidad explícitas, mapeadas a componente y a qué se degrada | §2.4 | C1/C4/D2 | PARA REVISIÓN |
| `TRZ-A1-026` | Maestro §3, §8, §10, §11.2 | Decisiones 1, 9, 12-13, 19-20 | — | Siete decisiones/dependencias lógicas con impacto en emplazamiento o seguridad (`F1-IMPL-01..07`) | §7 | C1/C2/C3/D1 | PARA REVISIÓN |
| `TRZ-A1-027` | Maestro §11.1, §4.6 | — | RNF-SEG | Clasificación de sensibilidad (Personal/Comercial/Operacional-sensible/Operacional) de los 19 eventos de dominio | §4.3 | D1/D2 | PARA REVISIÓN |
| `TRZ-A1-028` | Maestro §6, filas 2-3; §11.1 | — | RNF-SEG (exposición) | Borde público (GW-EDGE) y gateway de servicios (GW-API) como únicos puntos de exposición, con WAF/CDN/anti-DDoS/TLS 1.3 y control de políticas/identidad | §2.2 (Capa 2, Capa 3), §3.1, §3.2 | C1/D1 | PARA REVISIÓN |
| `TRZ-A1-029` | Maestro §3, §4.6, §17; Caso 06 Cap. 16.1 (pendiente N° 9) | Decisiones 14-15 | RF-NAV-10..11 (distribución del plan vigente a la cabina; actualización sin interacción activa) | Interfaz de cabina/terreno (CH-CAB): sin confirmación rutinaria, telemetría como fuente primaria, tolerancia de 8 h de sombra de radio en patio y reconciliación por marca de tiempo del equipo al recuperar señal | §2.2 (Capa 1), §3.1, §3.2 | C1/C3/D1 | PARA REVISIÓN |
| `TRZ-A1-030` | Maestro §4.7, §11.2; Ley 19.799; BTT RT-16.17/18 (transversal) + CP, Cap. 15, RT-16.14 (parámetro del caso) — mismo código, ambos exigibles (Célula 2 Supuesto M); Supuesto N (acta de inspección conjunta = firma autoridad + terminal) | MC-05 | RF-FIR-01; RF-INS-06 (acta de inspección conjunta) | Evidencia y firma digital (SRV-EVID) en los cuatro actos (embarque, recepción/entrega, acta de inspección, hechos facturables) conforme a Ley 19.799, sellos e integridad verificable | §2.2 (Capa 7), §3.1 | D1/D2 | PARA REVISIÓN |
| `TRZ-A1-031` | Maestro §3, §4.1-4.8, §8, §14 | Decisiones 1-21; MC-01 a MC-30 | — | Justificación de por qué las 8 decisiones estructurales son propias del Caso 06 (no plantilla genérica), sustento directo de `SD4-08` | §6.3 | D3 | PARA REVISIÓN |
| `TRZ-A1-032` | BTT RT-02.05 | — | — | Capa de negocio íntegramente sin estado; sesión en `SRV-IAM`, estado transaccional en `DATA-CORE` | §2.2 (Capa 4) | C1/C4 | PARA REVISIÓN |
| `TRZ-A1-033` | BTT RT-02.11; Maestro §19 regla 14 | — | — | Declaración explícita de 5 puntos únicos de falla lógicos (GW-API, INT-TOS, SRV-IAM, EDGE-RUN, CTX-PLAN) con justificación de aceptación y mitigación por frente | §2.5 | C1/C2/C3/D1/D2 | PARA REVISIÓN |
| `TRZ-A1-034` | BTT RT-13.01 | — | — | Exigencia WCAG 2.2 AA aplicada a los tres canales de presentación (CH-PORTAL/CH-APP/CH-CAB) | §2.2 (Capa 1) | D1 | PARA REVISIÓN |
| `TRZ-A1-035` | Célula 2, `RNF.md` — corte 2026-09-05 (84→91 RNF); FEP02 Cap. 9 §9.1 | — | RNF-DES-09, RNF-DES-10, RNF-DES-11, RNF-DES-12 | Umbrales de desempeño bajo peak: portal (`CH-PORTAL`), API (`GW-API`), lotes/arranque, prueba 1,5× peak | §2.2 (Capa 1, Capa 3) | C4/D1 | PARA REVISIÓN |
| `TRZ-A1-036` | Célula 2, `RNF.md` — corte 2026-09-05; FEP02 Cap. 7 RT-07.04/09-12; FEP01 Art. 20 | — | RNF-DIS-13, RNF-DIS-14, RNF-DIS-15 | Escenario de interrupción mayor (distinto del de 72 h sin enlace): RTO≤4h/RPO≤15min, respaldo 3-2-1-1-0, prueba DR semestral — responsabilidad física de C1/C3, `EDGE-RUN` no lo ejecuta | §2.2 (EDGE-RUN) | C1/C3/D1 | PARA REVISIÓN |

## Trazabilidad de actores

| ID traza | Actor | Fuente | RF/RNF asociados | Sección A1 |
|---|---|---|---|---|
| `TRZ-A1-ACT-01` | ACT-OPS a ACT-COM (9 internos) | Maestro §5.1; Caso 06 Caps. 1, 2, 7 | RF-CON, RF-GAT, RF-REF, RF-NAV, RF-APP | §1.2 |
| `TRZ-A1-ACT-02` | ACT-NAV a ACT-VER (7 externos) | Maestro §5.1; Caso 06 Caps. 6, 14 | RF-NAV, RF-INT, RF-INS, RF-EMI, RF-POR (incluido `RF-POR-09`, Etapa 2 — actualiza `ACT-AGE` a "agencias de aduana, embarcadores, importadores y exportadores", Maestro corte 2026-09-05) | §1.2 |

## Trazabilidad de sistemas conservados

| ID traza | Sistema | Fuente | MC asociados | Sección A1 |
|---|---|---|---|---|
| `TRZ-A1-EXT-01` | EXT-TOS12 a EXT-RAD (11 sistemas) | Maestro §5.2, §7; Caso 06 Caps. 5, 14, 16 | MC-02, MC-07, MC-12, MC-13, MC-20 | §1.3 |

## Trazabilidad del modelo de dominio

| ID traza | Entidad | Fuente | Contexto propietario | Sección A1 |
|---|---|---|---|---|
| `TRZ-A1-DOM-01` | Contenedor | Caso 06 Caps. 5, 7; Maestro §4.1 | CTX-OPS | §5.1 |
| `TRZ-A1-DOM-02` | Posición | Caso 06 Cap. 7; Maestro §4.7 meta 2 | CTX-YARD | §5.1 |
| `TRZ-A1-DOM-03` | Movimiento | Caso 06 Cap. 7; Maestro §4.1 | CTX-OPS | §5.1 |
| `TRZ-A1-DOM-04` | Visita de Nave | Caso 06 Cap. 7; Maestro §14 | CTX-VESSEL | §5.1 |
| `TRZ-A1-DOM-05` | Cita y Camión | Caso 06 Cap. 6; Maestro §4.2 | CTX-GATE | §5.1 |
| `TRZ-A1-DOM-06` | Alarma Reefer | Caso 06 Cap. 7; Maestro §4.2 | CTX-REEFER | §5.1 |
| `TRZ-A1-DOM-07` | Inspección | Caso 06 Cap. 7; Maestro §4.7 | CTX-INSP | §5.1 |
| `TRZ-A1-DOM-08` | Hecho Facturable y Evidencia | Caso 06 Cap. 7; Maestro §4.7 | CTX-BILL + SRV-EVID | §5.1 |
| `TRZ-A1-DOM-09` | Identidad | Caso 06 Cap. 14; Maestro §11.2 | SRV-IAM | §5.1 |
| `TRZ-A1-DOM-10` | Consumo y Emisión | Caso 06 Cap. 7; Maestro §14 | CTX-EMIS | §5.1 |

Agregar filas si se identifican nuevas afirmaciones arquitectónicas. No citar códigos RT sin documento y materia.
