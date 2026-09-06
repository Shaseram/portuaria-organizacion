# Matriz de cumplimiento global — Subdocumento 4

**Propietario de consolidación:** Frente 3 / integrador designado.  
**Regla:** cada frente actualiza su traza; esta matriz se actualiza en las puertas de integración y al registrar un cambio de línea base de Célula 2, como la presente alineación previa al desarrollo.

## 1. Cobertura del Subdocumento 4

| ID | Obligación | Paquete primario | Paquetes de apoyo | Evidencia esperada | Estado |
|---|---|---|---|---|---|
| `SD4-01` | capas, módulos, contextos, responsabilidades e interfaces | A1 | A2, A3, D1 | esquemas + catálogo | BASELINE LISTA; TEXTO/F2 PENDIENTES |
| `SD4-02` | físico híbrido y Art. 16 por componente | C1 | C2, C4, D1 | físico + tabla emplazamiento | BASELINE LISTA; TEXTO/F4 PENDIENTES |
| `SD4-03` | servicios, contratos, mensajería, versionado y gobierno | A2 | A3, D1 | matriz/diagrama integración | BASELINE LISTA; TEXTO/F3 PENDIENTES |
| `SD4-04` | Zero Trust, exposición, identidad, cifrado y controles | D1 | D2, A1, C3 | 31/31 controles asociados a amenazas y 17/17 grupos físicos tratados; vista F5 diseñada | BASELINE LISTA; TEXTO/F5 Y EVIDENCIA FUTURA PENDIENTES |
| `SD4-05` | ambientes, redes, HA, DR y respaldos | C3 | A3, C1, D1 | despliegue/continuidad | BASELINE LISTA; TEXTO/F3/F4 PENDIENTES |
| `SD4-06` | volumen, concurrencia, crecimiento y capacidad | C4 | A2, C2 | cálculos reproducibles | CUBIERTO EN C4; SÍNTESIS FINAL PENDIENTE |
| `SD4-07` | ADR con alternativas y selección | D2 | todos | 11 ADR con alternativas, consecuencias, condición de revisión, efecto T-11 y vínculo amenaza/SPOF | CUBIERTO BASELINE I1; 11 PROPUESTO, 0 APROBADO |
| `SD4-08` | arquitectura específica del Caso 06 | D3 | todos | expediente específico + MA-7/MA-8; verificación D3 | BASELINE Y CONTROL PREPARADOS; EJECUCIÓN D3 PENDIENTE |

## 2. Cobertura formal 4.1 y 4.2

| ID | Elemento formal | Archivo destino | Paquete | Estado |
|---|---|---|---|---|
| `T21-4.1-A` | Esquema de solución | Consolidado 4.1.1 | A1 | BASELINE LISTA; TEXTO/F1 PENDIENTES |
| `T21-4.1-B` | Arquitectura lógica | Consolidado 4.1.2–4.1.5 | A1/A2/A3/D1 | BASELINE LISTA; TEXTO/F2/F3/F5 PENDIENTES |
| `T21-4.2-A` | Arquitectura física | Consolidado 4.2.1 | C1 | BASELINE LISTA; TEXTO/F4 PENDIENTES |
| `T21-4.2-B` | Tecnologías de software | Consolidado 4.2.2 | C2 | CUMPLE BASELINE I1 |
| `T21-4.2-C` | Implementos hardware/software | Consolidado 4.2.3 | C2/C4/D1 | CUMPLE BASELINE I1 |
| `T21-4.2-D` | Data center primario | Consolidado 4.2.4 | C2/C4 | BASELINE CONDICIONADA; SÍNTESIS FINAL PENDIENTE |
| `T21-4.2-E` | Data center secundario | Consolidado 4.2.5 | C2/C3 | CUMPLE BASELINE I1; SÍNTESIS FINAL PENDIENTE |
| `T11` | Formulario cinco columnas | `90_Consolidado/02_FORMULARIO_T11_FINAL.md` | C4 + todos | CUMPLE MA-5; MAQUETACIÓN PENDIENTE |

## 3. Matriz de trazabilidad integradora

Agregar una fila por afirmación verificable o agrupación homogénea. No usar una sola fila para todo un entregable.

**Corte de entrada:** Célula 2 `c4756df`. Las filas nuevas reflejan obligaciones recibidas, no cumplimiento de arquitectura. Los identificadores B/C remiten a los anexos de segunda/tercera ronda del [cierre de Célula 2](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md); los RF/RNF/RN se consultan en los catálogos vigentes enlazados en el Maestro §21.

> **Lectura de estado:** `GTR-001..016` conservan la matriz de entrada y sus marcadores `POR DEFINIR/POR CREAR` históricos; no deben usarse como veredicto vigente. `GTR-017..021`, las trazas y los registros MA-3..8 contienen el corte conciliado. MA-8 preparó el mapa y D3; la producción final redacta/dibuja y D3 verifica el resultado sin fingir evidencia ejecutada.

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
| `GTR-017` | FEP02 Cap. 11 RT-11.02/05; RNF-SEG-02 | MC-02/04/07/08/09/10/11/12/30 | modelado STRIDE por componente e integración | SD4-04/07/08 | D2 B1–B7 + corte MA-3; TRZ-D2 | 24/24 componentes A1; 11/11 sistemas canónicos | 20/20 nodos C1 + `LOC-INSP-01` | `THR-001..073`, `SPOF-01..26`, ADR-001..011; controles D1 enlazados | DIFERIDO B8 | impacto identificado; cantidades/precios no alterados | EN CURSO — cobertura documental; ruta local y SPOF conciliados; pruebas y aceptación pendientes |
| `GTR-018` | Contrato D1; FEP02 Cap. 11/12; D2 B7 | F3-DEP-001..004; F3-DEC-005 | integración control→amenaza→nodo→T-11 | SD4-02/04/05/06 | D1 B7-R/MA-3; C1 §6.bis; C4 §9.bis/ter | 31 controles sobre 24 componentes | 17/17 grupos emplazados o justificados | 31/31 con amenaza D2; gateway/IAM/claves/logs/evidencia con capacidad local | DIFERIDO B8 | 7 anclas T11-SEC, una absorbida por C2-19; sin doble conteo | EN CURSO — integración de diseño completa; Subdoc. 5, productos, responsables, pruebas y aprobación pendientes |
| `GTR-019` | D1/D2 B7-C; auditoría semántica MA-0..6 | corrección quirúrgica, baseline ADR, T-11 y Art. 4 | coherencia e integridad del paquete completo | SD4-04/07/08 | D1 B7-C; D2 B7.11; registros MA-3/MA-4/MA-5/MA-6 | 31 controles D1 / 24 componentes A1 | 20 nodos C1 / 17 grupos SEC-PHYS | 73 amenazas, 26 SPOF y 11 ADR propuestos, 0 aprobados | DIFERIDO B8 | 32 filas T-11; 38 estándares y 15 materias normativas trazadas; diagramas diferidos | EN CURSO — MA-6 completa; siguiente MA-7 |
| `GTR-020` | FEP01 T-7/T-21/T-22; FEP02 RT-02.01/03 | MA-7: estructura y plan visual | cinco vistas 42010 + esquema formal | SD4-01..08 | `12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`; consolidado 4.1/4.2 | ocho capas y 24 componentes en F2; integración en F3 | híbrido/Art. 16 en F4 | límites de confianza en F5; datos en `V-DATA-01` | F1–F5 obligatorias; F6 condicional | T-11 se incorpora en 4.2.8 | MA-7 COMPLETADA; P4 APROBADA; PRODUCCIÓN PENDIENTE |
| `GTR-021` | FEP01 T-7/T-21/T-22; Art. 16/50.2; FEP02 RT-02.01/03/04 | MA-8: contrato D3 y mapa de ensamblado | fuente→sección→recurso→control→evidencia | SD4-01..08 | `13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`; D3/TRZ-D3 | 4.1.1–4.1.5 enlazadas a A1–A3/D1/D2 | 4.2.1–4.2.8 enlazadas a C1–C4/T-11 | trece controles D3 con criterio de aceptación | F1–F5 pendientes; `V-DATA-01` por cruzar; F6 condicional | 32 filas listas para maquetar | MA-8 PREPARADA; REDACCIÓN/FIGURAS Y EJECUCIÓN D3 PENDIENTES |

## 4. Estándares, marcos y certificaciones exigidos

**Regla:** no basta mencionar el estándar. Cada fila debe terminar en un control concreto y una evidencia. Los condicionales se marcan `NO APLICA` con justificación; no se eliminan silenciosamente.

> **Corte normativo MA-6, integrado por MA-7.** La fuente canónica es [`11_MATRIZ_ARTICULO4_MA6.md`](11_MATRIZ_ARTICULO4_MA6.md): contiene **38 filas** de estándares/prácticas y **15 materias normativas**, cada una con aplicabilidad, requisito, control, componente, evidencia I1, evidencia futura, sección y estado. MA-7 asigna su síntesis a 4.1.5. El inventario `STD-01..20` inferior se conserva como índice histórico agrupado y sus estados anteriores no constituyen el veredicto vigente.

| ID | Estándar/marco exigido | Aplicabilidad en el caso | Paquete responsable | Control y evidencia esperada | Estado |
|---|---|---|---|---|---|
| `STD-01` | ISO/IEC 27001 e ISO 9001 | certificación institucional | D3 coordina; evidencia Célula 1/equipo | certificado o vía admitida por Bases; alcance y vigencia | BLOQUEADO EXTERNO |
| `STD-02` | ISO/IEC 27002, 27017 y 27018 | controles de seguridad, nube y datos personales | D1/D2 | D1 matriz SEC-* y B7.3 SEC-GOV-01 / SEC-CLOUD-01; mapeo/evidencia final pendientes | EN CURSO |
| `STD-03` | NIST CSF 2.0 y NIST SP 800-207 | gobierno de ciberseguridad y Zero Trust | D1/D2 | D1 B1–B3/B7.3; D2 B6 refina amenazas por componente/nodo; vista y pruebas pendientes | EN CURSO |
| `STD-04` | OWASP ASVS 4.0 L2, Top 10, API Security Top 10 y SAMM | software, APIs y proceso seguro | D1/C3 | D1 B3.3/B6.2/B6.7; herramientas/configuración/pruebas pendientes | EN CURSO |
| `STD-05` | CIS Benchmarks | nube, servidores, edge y endpoints | D1/C2/C3 | D1 B7.3 SEC-HARD-01; productos/versiones/baselines/pruebas pendientes | EN CURSO |
| `STD-06` | SLSA 3+, CycloneDX o SPDX y firma de artefactos | cadena de suministro de software | D1/C3 | D1 B6.3/B6.7; plataforma, procedencia, SBOM/firma ejecutadas pendientes | EN CURSO |
| `STD-07` | ISO 22301 e ISO/IEC 27031 | continuidad de negocio y TIC | C3/D1 | C3 §§7–11: servicios, escenarios, RTO/RPO, respaldo, DR y plan de pruebas; simulacros/restauraciones son evidencia futura | CUBIERTO EN DISEÑO; EVIDENCIA FUTURA |
| `STD-08` | ISO/IEC 20000-1, ITIL 4 y SRE | operación y gestión del servicio | C3/D3 | modelo operativo, SLO/SLI, incidentes, cambios y evidencia | PENDIENTE |
| `STD-09` | ISO/IEC 25010, ISO/IEC 25012 e ISO/IEC/IEEE 29119 | calidad de software, datos y pruebas | A1/C3/C4; cruce Subdoc. 5/T-13 | atributos/umbrales, calidad de datos y estrategia de prueba | PENDIENTE |
| `STD-10` | ISO/IEC/IEEE 42010 y TOGAF o equivalente declarado | descripción y gobierno de arquitectura | A1/D2/D3 | MA-7 asigna lógica F2, proceso F3, despliegue F4, datos `V-DATA-01` y seguridad F5; D3 verificará correspondencias y ADR | BASELINE DE VISTAS LISTA; B8/MA-8 PENDIENTES |
| `STD-11` | WCAG 2.2 AA y EN 301 549 | portal, app y terminales | A1/D1; cruce UX | D1 B3.4 preserva accesibilidad ante bots; diseño/informe UX completos pendientes | EN CURSO |
| `STD-12` | OpenAPI 3.1, AsyncAPI 2.6+ y estándares marítimos | contratos síncronos, eventos y navieras | A2 | A2 §1.2 adopta `contract-first`, versionado, compatibilidad y fallback; BAPLIE/COPRAR/COARRI/CODECO por contrato; especificaciones ejecutables son evidencia futura | CUBIERTO EN DISEÑO |
| `STD-13` | OpenTelemetry, STRIDE e ISO 31000 | observabilidad, amenazas y riesgo | D1/D2 | D1 B5 correlación; D2 mantiene 73 amenazas y 26 SPOF con evidencia prevista y regla de actualización; pruebas pendientes | CUBIERTO EN DISEÑO; EVIDENCIA FUTURA |
| `STD-14` | OIDC, OAuth 2.1, SAML 2.0, LDAP y FIDO2 cuando corresponda | identidad e interoperabilidad IAM | D1 | D1 B2.2/B2.3/B2.7; directorio/producto/federación/pruebas pendientes | EN CURSO |
| `STD-15` | TLS 1.3 y respaldo 3-2-1-1-0 | comunicaciones y continuidad | D1/C3 | D1 B3.4/B4.5/B4.7; configuración/ubicación/restauración pendientes | EN CURSO |
| `STD-16` | NCh Elec. 2777 y NCh 2527 | sala/equipos eléctricos y ergonomía de puestos | C2/C4 | C2 §7.1 especifica puestos; C4 §6.2.bis fija carga/UPS/generación; memoria eléctrica y verificación ergonómica son evidencia futura | CUBIERTO EN DISEÑO; CÁLCULO DE OBRA FUTURO |
| `STD-17` | ISO 14001, PUE, ISO 14083/GLEC e ISO 14064-3 | sostenibilidad, energía y emisiones del caso | C2/C4; cruce Subdoc. 3/5 | C4 §6.2.bis fija PUE objetivo ≤1,60 y cálculo de referencia; A1 `CTX-EMIS` define medición ISO 14083/GLEC; medición y verificación por tercero son futuras | CUBIERTO EN DISEÑO |
| `STD-18` | NIST AI RMF 1.0 e ISO/IEC 42001 | solo si la solución incorpora IA | A1/D1/D2 | **Informe 1 no incorpora IA:** `CTX-PLAN` usa reglas explícitas versionadas y captura de motivos/correcciones, sin modelo autónomo, entrenamiento ni decisión automática basada en IA. Si se incorpora IA después, cambio de alcance activa ADR, controles y trazabilidad | NO APLICA JUSTIFICADO EN I1 |
| `STD-19` | PMBOK y prácticas ágiles justificadas | gobierno del trabajo, no componente arquitectónico | D3; cruce gestión | trazabilidad de decisiones, cambios y entregables | PENDIENTE |
| `STD-20` | IEC 62443 | segregación de red operacional/protección | C3/D1 | D1 B3.1–B3.3 SEC-NET-01; topología/aprobación/prueba C3 pendientes | EN CURSO |

La normativa chilena y sectorial se controla por aplicabilidad en los entregables respectivos; este bloque no reemplaza la revisión legal. MA-6 trazó explícitamente su efecto arquitectónico en `NORM-A4-01..15`, incluyendo protección de datos, Ley Marco de Ciberseguridad/OIV, firma electrónica, delitos informáticos, régimen aduanero, ISPS, SOLAS/VGM, IMDG, cadena de frío, autoridad marítima, normativa laboral portuaria y seguridad y salud en el trabajo.

## 5. Control 1:1 físico–T-11

Regla aplicada en MA-5: **cada fila de T-11 vuelve a un nodo físico, a un cálculo y a una fuente; y cada caja física ofertada tiene fila o exclusión justificada.** El universo final contiene **32 filas**: 21 de C2 —se agregó racks—, 4 de C3, 6 de seguridad y 1 servicio de escrow. `T11-SEC-04` no genera fila: resuelve sobre `T11-C2-19`.

| Fila T-11 | Nodo físico | Justificación Art. 16 | Cálculo/cantidad | Seguridad | Estado |
|---|---|---|---|---|---|
| `T11-C2-01` servidores del núcleo local | `PHY-OPS-01` | latencia ≤1 s y 72 h; incluye perfil local restringido de `GW-API` | C4 §6.2.bis: 3×1U, 16 núcleos, 128 GB, 2×10 GbE por nodo | `SEC-NET-01`, `SEC-API-01`, `SEC-END-01` | línea base MA-3 |
| `T11-C2-02` almacenamiento local | `PHY-OPS-02` | buffer del corte; `RT-03.14` exige tolerar falla de disco | C4 §6.2.bis: 4×480 GB `RAID 10`, 1,92 TB brutos/≈960 GB útiles; demanda ≈183 GB | `SEC-DATA-01`, `SEC-ENC-01` | línea base MA-3 |
| `T11-C2-03` conmutación de núcleo | `PHY-OPS-04` | `RT-08.03` HA sin punto único | C4 §9: par en HA | `SEC-NET-01` | v0.5 |
| `T11-C2-04` cortafuegos y segmentación | `PHY-OPS-04` | Declaración Mandatoria: segregar operación, administración y protección | par en HA | `SEC-NET-01`, `SEC-EXP-01`; IEC 62443 | v0.5 |
| `T11-C2-05` UPS | sala técnica | `RT-06.07` ≥30 min a plena carga | C4 §6.2.bis: 2×6 kVA/≥5,4 kW N+1, cada unidad sostiene 2,67 kW | — | línea base MA-3 |
| `T11-C2-06` generación autónoma | recinto del CLIENTE | `RT-06.08` ≥24 h con estanque | C4 §6.2.bis: ≥15 kVA, estanque ≥120 L útiles, 1 conjunto | — | línea base MA-3; ejecución CLIENTE |
| `T11-C2-07` climatización de precisión | sala técnica | `RT-06.13` N+1 | C4 §6.2.bis: 2×18.000 BTU/h | — | línea base MA-3 |
| `T11-C2-08` detección temprana de incendio | sala técnica | `RT-06.16` | 1 sistema | — | v0.5 |
| `T11-C2-09` extinción por agente limpio | sala técnica | `RT-06.17` | 1 sistema | — | v0.5 |
| `T11-C2-10` control de acceso y esclusa | acceso a sala | `RT-06.20`/`.23`; tensión declarada en `F2-DEC-002` | 1 conjunto | `SEC-PHYS` | v0.5 |
| `T11-C2-11` videovigilancia del recinto | sala técnica | `RT-06.24` ≥30 días; **no es el VMS del terminal**, `F2-DEC-003` | C4 §6.2.bis: 4 cámaras + NVR ≥4 TB útiles | `SEC-PHYS` | línea base MA-3 |
| `T11-C2-12` custodia de medios | `PHY-OPS-05` | `RT-06.26`–`.28`; sostiene el «fuera de sitio» del 3-2-1-1-0 | 1 servicio | `SEC-BKP-01`; verificación mensual `RT-07.12` | v0.5 |
| `T11-C2-13` estaciones de operación | `PHY-OPS-06` | `RT-06.30` prohíbe operar dentro del recinto técnico; `RT-08.07` | 3 de baseline; AHT valida en H2 | `SEC-ADM-01` | MA-5 |
| `T11-C2-14` gabinetes de borde | `PHY-EDG-01/02/03/04` | `RT-08.12` y `CP, Cap. 15, RT-06.01`: cuatro zonas, **no la de inspección** | 59–61; site survey cierra patio | `SEC-PHYS` | MA-5 |
| `T11-C2-15` dispositivos móviles de terreno | borde, todas las zonas | `RT-08.11`; uso con guantes e intemperie | 97: 88 operativos + 9 repuestos | `SEC-END-01` **no** aplica: sin agente | MA-5 |
| `T11-C2-16` concentradores de patio refrigerado | `PHY-EDG-03` | alarma ≤5 min sin depender del enlace | 26 → 32, uno por tablero | `SEC-NET-01` | v0.5 |
| `T11-C2-17` servicios de nube, región primaria | `PHY-CLD-03..08` | AWS `sa-east-1` multi-AZ; Art. 16: elasticidad, IaC, FinOps y servicios gestionados | 1 plataforma; 2,5 TB en línea, 73 ev/s +30 % | `SEC-DATA-01` | MA-5; `ADR-011 PROPUESTO` |
| `T11-C2-18` servicios de nube, región secundaria y DR | `PHY-CLD-10` | AWS `us-east-1`; `RT-07.02`: no hay segundo recinto del CLIENTE | 1 sitio lógico; RTO 4 h/RPO 15 min | `SEC-BKP-01` | MA-5; `ADR-007/011` |
| `T11-C2-19` observabilidad y SIEM | `PHY-CLD-09` + colector en `PHY-OPS-01` | `RT-03.16`: **una sola** plataforma para nube y on-premise | C4 §9.ter: piso ≈8 GB/año en línea; falta medición | `SEC-LOG-01`, `SEC-SIEM-01` | v0.5; absorbe `T11-SEC-04` |
| `T11-C2-20` licenciamiento de sistema operativo | sala técnica y borde | `RT-03.15` | C4 | `SEC-HARD-01` línea base CIS | v0.5 |
| `T11-C2-21` racks y distribución A/B | `PHY-OPS-01/02/04` | `RT-06.03..05`; separación física y crecimiento | 2 racks 42U | — | MA-5 |
| `T11-C3-01` segundo camino hacia la nube | terminal ↔ nube | `RT-03.17`: proveedor distinto y conmutación con tiempo declarado | ≥35 Mbps, dos caminos | `SEC-SYNC-01` | v0.5; capacidad real en `F2-ESC-012` |
| `T11-C3-02` canal privado hacia la nube | terminal ↔ AWS `sa-east-1` | `RT-03.04`: no exponer la red del terminal a Internet | 2 conexiones VPN / 4 túneles sobre 2 carriers | `SEC-SYNC-01` | MA-5 |
| `T11-C3-03` red operacional del patio | `PHY-EDG-02` | `CP, Cap. 15, RT-03.24`: rediseño con radiopropagación verificada | **6–8, rango**; la cobertura manda, no el tráfico | `SEC-NET-01` | v0.5; site survey `F2-ESC-001` |
| `T11-C3-04` plataforma CI/CD | nube, ingeniería separada de producción | `RT-04.07`: desplegar sin ventana; el terminal no la tiene | por proyectos y ejecuciones | `SEC-SDLC-01`, `SEC-PIPE-01`, `SEC-SUPPLY-01` | v0.5 |
| `T11-SEC-01` borde y gateway | `PHY-CLD-01/02` + perfil local gateway en `PHY-OPS-01` | única superficie pública; ruta crítica local autorizada e independiente | 369 kbps régimen, 625 peak; perfil local incluido en 3 nodos | `SEC-EDGE-01/02`, `SEC-API-01` | línea base condicionada a producto |
| `T11-SEC-02` identidad y PAM | `PHY-CLD-03` + capacidad local en `PHY-OPS-01` | sin autenticación local el corte de enlace es corte de operación | 175 internas, 187 externas, 2.400 eventuales/año | `SEC-IAM-01`, `SEC-ADM-01` | v0.5; `ADR-008` propuesto condicionado |
| `T11-SEC-03` KMS/HSM y gestor de secretos | nube + sala técnica | regla negativa 8: la clave no puede vivir solo en nube | por ámbito de clave; no depende del volumen | `SEC-KEY-01`, `SEC-SECRET-01` | v0.5; **requisito excluyente** |
| `T11-SEC-05` EDR | nodos locales, cargas en nube y puestos | `RT-11`; **excluye dispositivos de terreno**, sin agente confirmado | 3 nodos + cargas + puestos de `PHY-OPS-06` | `SEC-END-01` | v0.5 |
| `T11-SEC-06` SOC gestionado 24×7 | servicio | restricción no negociable 11: no se asigna a TI = 5 | por cobertura y volumen de eventos | `SEC-SOC-01`, `SEC-IR-01` | v0.5 |
| `T11-SEC-07` escaneo continuo y pentest | servicio | pentest anual y antes de cada paso a producción | por activos y por ejercicio | `SEC-VULN-01`, `SEC-PENTEST-01` | v0.5 |
| `T11-SVC-01` custodia de código fuente | tercero independiente | BA Art. 84.6: depósito con cláusulas de liberación | 1 servicio; 2 depósitos/año | propiedad intelectual/continuidad | MA-5 |

**Alcance de provisión sin perder especificación.** El hardware de terreno que TERABYTE debe especificar permanece en `T11-C2-14..16`, marcando “adquisición a cargo del CLIENTE” y sin precios. Si el formulario admite solo provisión del adjudicatario, pasa 1:1 a un anexo técnico y no se borra. Quedan fuera como provisión la obra civil, sistemas conservados y canalizaciones ejecutadas por el CLIENTE.

**Cierre de `AGC3-012`:** `BA, Art. 84` exige escrow semestral del código y MA-5 lo incorpora como `T11-SVC-01`, sin precio y separado del repositorio del CLIENTE.

## 6. Checklist del Capítulo C del BTT — 28 entregables de la oferta técnica

Incorporado el 2026-09-06, cerrando `F2-ESC-005`. Es la lista de verificación del propio BTT y **no estaba controlada en ninguna parte**. Se marca cuáles toca Célula 3 y cuáles no, para que nadie asuma que un entregable ajeno está cubierto.

| N° | Entregable | Se exige en | Sobre / instancia | Dueño en Célula 3 | Estado |
|---|---|---|---|---|---|
| 1 | Documento de arquitectura ISO/IEC/IEEE 42010 con **las cinco vistas** | `RT-02.03` | Sobre N° 2 | **Subdocumento 4 completo** | **EN CURSO — MA-7 asignó F2/F3/F4/F5 y `V-DATA-01`; B8 debe producir las figuras** |
| 2 | Registro de decisiones de arquitectura (ADR) | `RT-02.04` | Sobre N° 2 | `03_REGISTRO_ADR_GLOBAL` y revisión MA-4/MA-5 | EN CURSO: 11 registrados; 11 `PROPUESTO`, 0 aprobados |
| 3 | Tabla de emplazamiento nube/on-premise justificada | Cap. 3 | Sobre N° 2 | C1 §4 | **CUBIERTO EN DISEÑO**: 20 nodos físicos ×6 criterios y `LOC-INSP-01` explícitamente no físico |
| 4 | Declaración de funciones **no** disponibles en modo desconectado | `RT-03.13` | Sobre N° 2 | A3 §7 y C3 §7.1 | **CUBIERTO** v0.5; su ausencia es «observación grave» |
| 5 | Modelo de datos y diccionario de datos | `RT-05.01` | Sobre N° 2 | Subdocumento 5 (Célula 4) | fuera de Célula 3 |
| 6 | Plan de migración de datos | `RT-05.11` | Sobre N° 2 | A3 + Subdocumento 5 | parcial en A3 |
| 7 | Interfaces en OpenAPI y AsyncAPI | `RT-05.16` | Sobre N° 2 | A2 | no exigible en Informe 1 |
| 8 | Especificación del site principal y secundario, **con planos** | Caps. 6 y 7 | Sobre N° 2 | C2 §5 y §6 | EN CURSO: especificación v0.5; **planos pendientes** |
| 9 | Plan de recuperación ante desastres y política de respaldo | Cap. 7 | Sobre N° 2 | C3 §9 | **CUBIERTO** v0.5 |
| 10 | Especificación del hardware y de los dispositivos de terreno | Cap. 8 | Sobre N° 2 | C2 §7 | **CUBIERTO** v0.5 |
| 11 | Cálculo de capacidad y dimensionamiento | `RT-09.01` | Sobre N° 2 | C4 | **CUBIERTO** v0.5, con supuestos declarados |
| 12 | Plan de continuidad del negocio conforme a ISO 22301 | `RT-10.03` | Sobre N° 2 | C3 §10 | **CUBIERTO** v0.5 |
| 13 | Modelado de amenazas y matriz de controles de seguridad | `RT-11.02` y `RT-11.05` | Sobre N° 2 | D2 y D1 | **CUBIERTO** v0.5: 73 amenazas, 31 controles |
| 14 | Declaración de la superficie de exposición | `RT-11.13` | Sobre N° 2 | D1 | EN CURSO |
| 15 | Plan de respuesta a incidentes de seguridad | `RT-11.18` | Sobre N° 2 | D1 | EN CURSO; ojo con el cruce `RT-11.18`/`.19` de Célula 2 |
| 16 | Modelo de identidad, matriz de roles y segregación de funciones | Cap. 12 | Sobre N° 2 | D1 | EN CURSO |
| 17 | Sistema de diseño e informe de conformidad de accesibilidad | Cap. 13 | Sobre N° 2 | fuera de Célula 3; nace en A1 `RT-13.01` | no iniciado |
| 18 | Estrategia de observabilidad y catálogo de alertas | Cap. 14 | Sobre N° 2 | C2/C4 + D1 | parcial: la plataforma sí (`T11-C2-19`), el catálogo de alertas no |
| 19 | Certificados institucionales y del personal | Cap. 15 | Sobres N° 1 y 2 | fuera de Célula 3 (T-6) | no iniciado |
| 20 | Estrategia y plan de pruebas (T-13) | Cap. 20 | Sobre N° 2 | fuera; C3 §11 aporta las de continuidad | parcial |
| 21 | Plan de implantación y marcha blanca (T-18) | `RT-20.01` | Sobre N° 2 | fuera; C3 §12 aporta el calendario | parcial |
| 22 | Modelo de operación, soporte y centro de atención | Cap. 21 | Sobre N° 2 | fuera de Célula 3 | no iniciado |
| 23 | Plan de capacitación y transferencia de conocimiento | Cap. 22 | Sobre N° 2 | fuera de Célula 3 | no iniciado |
| 24 | Matriz de cumplimiento técnico (T-12) sobre **todos** los códigos RT | numeral 1.5 | Sobre N° 2 | Célula 2 + integrador | **no iniciado**; es el punto 4 del recordatorio de Célula 2 |
| 25 | Sitio web corporativo y declaración jurada | Cap. 23 | Sobre N° 1 | fuera | no iniciado |
| 26 | Video de presentación | Cap. 24 | propuesta final | fuera | no iniciado |
| 27 | Prototipo interactivo y arquitectura de información | Cap. 25 | con el Informe 3 | fuera | no iniciado |
| 28 | Fichas de las cinco innovaciones (T-19) | Cap. 26 | Sobre N° 2 | fuera de Célula 3 | Informe 1 exige idea, tecnología y resultado esperado |

**Lectura del checklist.** Seis entregables son del Frente 2 —N° 3, 8, 9, 10, 11 y 12— y **cinco de los seis están cubiertos en `v0.5`**; el N° 8 espera los planos. El N° 1 es el Subdocumento 4 entero y su única brecha son los diagramas. El N° 24, el Formulario T-12, es la brecha más seria fuera de Célula 3: es una matriz sobre los 374 códigos `RT` y nadie la ha empezado.

## 7. Control de pendientes externos

| ESC | Afecta | Diseño conservador/fallback | ¿Impide entregar? | Evidencia |
|---|---|---|---|---|
| ESC-01..14 | ver Maestro §18 | completar durante desarrollo | No, si queda explícito y existe tratamiento | PENDIENTE |
