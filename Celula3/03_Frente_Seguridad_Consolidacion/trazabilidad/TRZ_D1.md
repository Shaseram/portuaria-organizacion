# TRZ-D1 — Arquitectura de seguridad

## 1. Cruces de arquitectura

| ID | Fuente | RNF/MC | Control | Actor/dato | Capa/componente | Nodo/servicio | Evidencia | T-11 | Estado |
|---|---|---|---|---|---|---|---|---|---|
| `TRZ-D1-001` | FEP02 Cap. 11 RT-11.01/02 | RNF-SEG-01/02 | Zero Trust/STRIDE | todos | transversal | 21 nodos C1 cruzados | D1 B1.2/B3.1–3/B7-R; D2 B7/B7.8: modelo STRIDE auditado y 31/31 controles enlazados | SEC-PHYS incorporado por C1–C4 | EN CURSO — diseño cubierto; pruebas/aprobación pendientes |
| `TRZ-D1-002` | FEP02 Cap. 12 + Caso 06 | MC-04; RNF-SEG-10 | IAM terminal/eventual | ACT-EVT/externos | SRV-IAM + capacidad local | `PHY-CLD-03` + `PHY-OPS-01` | D1 B1/B2/B7-R; matriz, sesiones, offline y pruebas previstas | `T11-SEC-02`; producto/prueba pendientes | EN CURSO |
| `TRZ-D1-003` | FEP02 Cap. 11 RT-11.07/08/12/13 | RNF-SEG-04 | WAF/DDoS/TLS/exposición | públicos | GW-EDGE | nube multi-AZ propuesta; origen privado | D1 B3.3–B3.6; configuración/inventario/pruebas pendientes | sí, servicio/capacidad pendiente | EN CURSO |
| `TRZ-D1-004` | FEP02 Cap. 11 RT-11.14..16; Maestro §§11.3/16 | RNF-SEG/OPE | log/SIEM/EDR | operación | transversal | `PHY-CLD-09` + `PHY-OPS-01`; EDR en nodos compatibles | D1 B5/B7-R; política de admisión, retención, corte y casos; ingesta dominante/pruebas pendientes | `T11-SEC-04/05`; revisar solape `T11-C2-19` | EN CURSO |
| `TRZ-D1-005` | FEP02 Cap. 7 RT-07.09..12; C2 B1 | RNF-DIS-14 | respaldo cifrado/inmutable | datos y claves | continuidad/datos | POR VALIDAR C2/C3 | B4.5–B4.8; restauración mensual y resistencia al borrado | sí, producto/cantidad pendiente | EN CURSO |
| `TRZ-D1-006` | Caso 06 Anexo A; FEP02 Cap. 12; C2 B2/C3 | RF-POR-02; RF-POR-09 | identidad/autorización y evidencia de carga | ACT-AGE | CH-PORTAL/SRV-IAM | producto/nodo POR VALIDAR A1/C1 | D1 B1.3/B1.5/B2.2–3; representación/recuperación/pruebas pendientes | IAM/borde candidatos | EN CURSO |
| `TRZ-D1-007` | FEP02 Cap. 11 RT-11.17; Caso 06 Cap. 10 restricción 11 | obligación directa BTT; RNF-OPE-08 apoyo | SOC 24x7 | TI=5 + servicio especialista | SEC-SOC-01 | servicio gestionado/subcontratado propuesto; ubicación POR VALIDAR | D1 B5.4/B5.7/B5.8; ubicación, dotación, RACI y procedimientos pendientes | sí, servicio/costo pendiente | EN CURSO |
| `TRZ-D1-008` | FEP02 Cap. 11 RT-11.03/09/10; Caso 06 Cap. 15 RT-11.10 | RNF-SEG-04/05/09 | clasificación y cifrado de reposo/campo | DATA-CORE/TS/DOC/AN; personales, comerciales y carga/ruta | datos y servicios | POR VALIDAR C1/Subdoc. 5 | B4.1–B4.3; catálogo y consulta directa | capacidades candidatas | EN CURSO |
| `TRZ-D1-009` | FEP02 Cap. 11 RT-11.09; Maestro §§9/11/16 | RNF-SEG-04; RNF-DIS-02/04/14 | claves, secretos, rotación y recuperación | claves/certificados/secretos | transversal | híbrido; capacidad local POR VALIDAR | B4.4–B4.8; corte/rotación/recuperación | sí | EN CURSO |
| `TRZ-D1-010` | FEP02 Cap. 11 RT-11.04/18..21 | RNF-SEG-03/07/08/11; RNF-OPE-05 | incidentes, vulnerabilidades, pentest y simulación | todos los activos/servicios | SEC-IR-01/SEC-VULN-01/SEC-PENTEST-01 | híbrido + servicio independiente | D1 B5.5–B5.7; marcas 2 h/24 h/5 días, 7/15/30 y reprueba | sí, capacidades/servicios pendientes | EN CURSO |
| `TRZ-D1-011` | FEP02 Cap. 11 RT-11.22..28; Cap. 4 RT-04.03..07/11; FEP01 Art. 4.3 | RNF-MAN-01..06/11 | DevSecOps, cadena de suministro, datos no productivos y acceso a producción | código, dependencias, artefactos y datos | SEC-SDLC/PIPE/SUPPLY/ART/NPDATA/PROD/SAMM | servicio de ingeniería; producción segregada | D1 B6.1–B6.8; bloqueos, SBOM, firma, trazabilidad y acceso excepcional | sí, herramientas/licencias pendientes | EN CURSO |
| `TRZ-D1-012` | Contrato D1; FEP02 Cap. 11/12; Plan §8; T-11 | SD4-04; apoyo SD4-02/05/08 | auditoría de cobertura y SEC-PHYS-v0.1 | todos | 31 SEC-* / 17 grupos de aporte | 17/17 emplazados o justificados por C1 | D1 B7/B7-R; 28/28 RT11 y 13/13 RT12 en diseño; amenazas/nodos cruzados | 7 candidatos `T11-SEC-*` + 10 incluidos/condicionales | EN CURSO |
| `TRZ-D1-013` | A1–A3; C1–C4; D2 B7 | dependencias F3-DEP-001..004 | integración documental de seguridad | 16 actores, 24 componentes | 31 controles / 73 amenazas | 21 nodos; servicios/procesos sin nodo justificados | D1 B7-R: control↔amenaza 31/31, SEC-PHYS 17/17 y continuidad IAM/llaves/logs | C4 §9.bis/ter; sin alterar cantidades | EN CURSO — listo para revisión conjunta |
| `TRZ-D1-014` | D1/D2; TRZ-D1/D2; registro ADR; matriz global | puerta conjunta B7-C | revisión de coherencia previa a auditoría independiente | todos | 31 controles / 73 amenazas / 22 SPOF | 21 nodos C1 | D1 B7-C y auditoría de cierre: sin referencias huérfanas ni estados incompatibles detectados | sin cambios de producto/cantidad | EN CURSO — REVISIÓN CONJUNTA COMPLETA; aprobación pendiente |

## 2. Cobertura de entrada — FEP02, capítulo 11

**Fuente:** FEP02.26, Bases Técnicas Transversales, capítulo 11, §§11.1–11.5, páginas impresas 23–25 (páginas PDF 24–26). Cada código de esta sección pertenece a **FEP02**, no al Caso 06. Contraste con el PDF realizado el 2026-09-05.

**Uso:** una fila por RT para no perder obligaciones. La tabla identifica alcance y evidencia prevista; no acredita implementación. Al desarrollar D1 se enlaza cada fila con el ID del control y su sección, componente y prueba en la matriz de controles del entregable. Una misma evidencia puede cubrir varios RT si se explica la relación. No es necesario repetir normas en cada párrafo: el texto explica el diseño y esta traza demuestra por qué corresponde.

El capítulo 11 es central para D1, pero no sustituye las obligaciones ya identificadas de identidad (cap. 12), continuidad (cap. 7/10), terreno y restricciones del Caso 06. D2 desarrolla amenazas; D3 audita cobertura; los otros frentes aportan componentes e implementación. Las filas comienzan `PENDIENTE` y pasan a `EN CURSO` solo cuando existe diseño enlazado; esto no acredita prueba ni cumplimiento final.

| RT FEP02 | Numeral / carácter BTT | Consideración que debe conservarse | Referencia Célula 2 / matriz global | Destino y coordinación | Evidencia prevista / enlace por completar | Estado |
|---|---|---|---|---|---|---|
| `RT-11.01` | 11.1 / Obligatorio | Zero Trust conforme NIST SP 800-207: verificación explícita, mínimo privilegio y presunción de compromiso | RNF-SEG-01; STD-03 | D1; A1/C1 | D1 B1.2/B2.2/B3.1–3 y SEC-IAM/NET/API-01; nodos/configuración/pruebas pendientes | EN CURSO |
| `RT-11.02` | 11.1 / Obligatorio | Amenazas por cada componente e integración externa; metodología declarada y actualización ante cambios relevantes | RNF-SEG-02; STD-13 | D2 produce; D1 aplica controles; A1/A2/C1 aportan inventario | D2 B7 cubre el diseño con `THR-001..073`, 24/24 componentes, 11 sistemas+`EXT-CON`, 21/21 nodos y regla de cinco disparadores; D1 B7-R confirma 31/31 controles enlazados | EN CURSO — CUBIERTO EN DISEÑO; pruebas, revisión independiente y aprobación pendientes |
| `RT-11.03` | 11.1 / Obligatorio | Clasificación de información por sensibilidad, con controles diferenciados en matriz | RNF-SEG-05/09 (apoyo, no equivalencia total); STD-02 | D1; Subdoc. 5 | D1 B4.1/2; taxonomía y controles iniciales, catálogo de campos pendiente | EN CURSO |
| `RT-11.04` | 11.1 / Obligatorio | Escaneo continuo; remediación críticas ≤7 días corridos, altas ≤15 y medias ≤30, desde publicación o detección | RNF-SEG-03 | D1; C3/operación | D1 B5.6/B5.7 y SEC-VULN-01; cobertura, producto, ejecución y cierres pendientes | EN CURSO |
| `RT-11.05` | 11.1 / Obligatorio | Matriz trazable a ISO/IEC 27001 y 27002: control, implementación concreta y evidencia | STD-01/02; obligación directa BTT | D1; D3 verifica | matriz de controles + D1 B7.3/B7.4 y SEC-GOV-01; mapeo normativo completo y evidencia pendientes | EN CURSO |
| `RT-11.06` | 11.1 / Obligatorio | Aplicar ISO/IEC 27017 a nube y 27018 al tratamiento de datos personales en nube | STD-02 | D1; C1/C2 y Subdoc. 5 | D1 B7.3 y SEC-CLOUD-01; proveedor/servicios/datos, responsabilidades y evidencia pendientes | EN CURSO |
| `RT-11.07` | 11.2 / Obligatorio | Exposición exclusivamente por borde: CDN, WAF con reglas gestionadas/personalizadas y DDoS L3/L4/L7 | STD-05 (apoyo); obligación directa BTT | D1; A1/A2/C1/C3 | D1 B3.3/B3.4/B3.6 y SEC-EDGE-01; producto, reglas/capacidad y pruebas pendientes | EN CURSO |
| `RT-11.08` | 11.2 / Obligatorio | TLS 1.3; prohibir TLS 1.0/1.1; cifrados modernos; HSTS con precarga; certificados automatizados, rotación y aviso de vencimiento | RNF-SEG-04; STD-15 | D1; A2/C3 | D1 B3.4 y B4.4/6/7; inventario, productos y pruebas pendientes | EN CURSO |
| `RT-11.09` | 11.2 / Obligatorio | Todos los datos en reposo cifrados; KMS/HSM, rotación declarada y separación de custodia | RNF-SEG-04; ADR-009 | D1; C2 y Subdoc. 5 | D1 B4.2/4–8; producto, ubicación, períodos, custodios y pruebas pendientes | EN CURSO |
| `RT-11.10` | 11.2 / Según caso: APLICA | Cifrado adicional por campo sensible; lectura directa de base no revela contenido. Caso 06 Cap. 15 RT-11.10 especifica datos personales, comerciales y de carga/ruta | RNF-SEG-05 | D1; Subdoc. 5/C2 | D1 B4.1–3; catálogo final de campos y prueba de consulta directa pendientes | EN CURSO |
| `RT-11.11` | 11.2 / Obligatorio | Gateway autentica, autoriza, aplica cuotas/rate limit, valida esquema e inspecciona payload | obligación directa BTT | D1; A2/C3 | D1 B3.3/B3.4/B3.6 y SEC-API-01; contratos, límites/configuración y pruebas pendientes | EN CURSO |
| `RT-11.12` | 11.2 / Obligatorio | Protección contra bots/abuso con reto progresivo, preservando accesibilidad y usuarios legítimos | STD-11 (apoyo); obligación directa BTT | D1; A1 | D1 B3.3/B3.4/B3.6 y SEC-EDGE-01; reglas/producto y pruebas de legitimidad/accesibilidad pendientes | EN CURSO |
| `RT-11.13` | 11.2 / Obligatorio | Declarar cada dominio, puerto y servicio alcanzable desde fuera de la red del CLIENTE | obligación directa BTT | D1; A2/C1/C3 | D1 B3.5/B3.6 y SEC-EXP-01; plantilla por familias lista, inventario real/escaneo pendientes | EN CURSO |
| `RT-11.14` | 11.3 / Obligatorio | Eventos centralizados e inalterables: ≥12 meses en línea y 24 adicionales en archivo recuperable | Maestro §11.3/16.1; obligación directa BTT | D1; C2/C4 | D1 B5.1/B5.2.1/B5.7 y SEC-LOG-01; política de admisión y fórmula de medición definidas; EPS/tamaño/peaks/factores, producto y pruebas pendientes | EN CURSO |
| `RT-11.15` | 11.3 / Obligatorio | Correlación SIEM con casos de uso específicos de la operación portuaria | ADR-010; obligación directa BTT | D1/D2; A1/A2 | D1 B5.2/B5.3/B5.7 y SEC-SIEM-01; reglas definitivas y pruebas pendientes | EN CURSO |
| `RT-11.16` | 11.3 / Obligatorio | Detección y respuesta en endpoints y cargas de trabajo, en nube y on-premise | obligación directa BTT | D1; C2/C3 | D1 B5.2/B5.3/B5.7 y SEC-END-01; inventario/compatibilidad/licencias/pruebas pendientes | EN CURSO |
| `RT-11.17` | 11.3 / Obligatorio | SOC 24x7 propio o subcontratado; ubicación, dotación y procedimientos | GTR-014; TRZ-D1-007 | D1; C3/C4 y equipo de operación | D1 B5.4/B5.8 y SEC-SOC-01; servicio gestionado propuesto, contrato/dotación/RACI pendientes | EN CURSO |
| `RT-11.18` | 11.3 / Obligatorio | Plan de incidentes: clasificación, escalamiento, plazos, responsables y comunicación al CLIENTE ≤2 h desde detección de crítico | RNF-SEG-11; cita C2 cruzada, ver §4 | D1; C3/operación | D1 B5.5/B5.7 y SEC-IR-01; responsables, canales y ejercicio pendientes | EN CURSO |
| `RT-11.19` | 11.3 / Obligatorio | Brecha de seguridad/datos: notificación al CLIENTE ≤24 h con informe preliminar; causa raíz ≤5 días hábiles siguientes | RNF-SEG-07 (notificación); Maestro §11.3; ver §4 | D1; operación | D1 B5.5/B5.7 y SEC-IR-01; protocolo nominal, ejercicio e informes pendientes | EN CURSO |
| `RT-11.20` | 11.3 / Obligatorio | Pentest independiente del adjudicatario, anual y antes de cada paso a producción; informe íntegro al CLIENTE y remediación con plazos | RNF-SEG-08 | D1/D2; C3 y equipo de pruebas | D1 B5.6/B5.7 y SEC-PENTEST-01; tercero, alcance, calendario e informes pendientes | EN CURSO |
| `RT-11.21` | 11.3 / Deseable | Simulación de incidente con participación del CLIENTE al menos anual durante operación | obligación deseable BTT | D1; operación | D1 B5.6/B5.7 propone incorporarla; aceptación explícita, calendario, acta y mejoras pendientes | EN CURSO |
| `RT-11.22` | 11.4 / Obligatorio | CI incorpora SAST, SCA, DAST y escaneo de imágenes; bloqueo automático ante hallazgos críticos | RNF-MAN-03 (parcial; agregar DAST); STD-04 | D1 define controles; C3 materializa flujo | D1 B6.2/B6.7 y SEC-PIPE-01; herramienta, reglas, ejecuciones/bloqueos pendientes | EN CURSO |
| `RT-11.23` | 11.4 / Obligatorio | Inventario de componentes por versión liberada en CycloneDX o SPDX, entregado al CLIENTE | STD-06 | D1; C3/desarrollo | D1 B6.3/B6.7 y SEC-SUPPLY-01; generación, correspondencia y entrega reales pendientes | EN CURSO |
| `RT-11.24` | 11.4 / Obligatorio | Artefactos firmados y procedencia verificada conforme SLSA nivel 3 o superior | STD-06 | D1; C3/desarrollo | D1 B6.3/B6.7 y SEC-SUPPLY-01; plataforma, claves y evidencia SLSA/verificación pendientes | EN CURSO |
| `RT-11.25` | 11.4 / Obligatorio | Prohibido usar datos reales productivos en no producción sin anonimización o seudonimización verificable | Maestro §11.3 aplica anonimización; obligación directa BTT | D1; C3 y Subdoc. 5 | D1 B4.1/B6.5/B6.7 y SEC-NPDATA-01; catálogo, técnica y prueba de no revelación pendientes | EN CURSO |
| `RT-11.26` | 11.4 / Obligatorio | Proceso de aprobación de dependencias de terceros: licencia, mantención activa y ausencia de vulnerabilidades conocidas | obligación directa BTT | D1; C3/desarrollo | D1 B6.4/B6.7 y SEC-SUPPLY-01; catálogo, responsables y decisiones ejecutadas pendientes | EN CURSO |
| `RT-11.27` | 11.4 / Obligatorio | Sin acceso interactivo directo de desarrolladores a producción; excepción temporal, aprobada, registrada y con sesión grabada | Maestro §11.2 (PAM, apoyo); obligación directa BTT | D1; C3 | D1 B2.5/B6.6/B6.7 y SEC-PROD-01; IAM/PAM, aprobadores y prueba pendientes | EN CURSO |
| `RT-11.28` | 11.4 / Deseable en BTT; cruce FEP01 Art. 4.3 | SAMM o equivalente: evaluación inicial y anual de madurez. FEP01 exige OWASP SAMM para el proceso; no omitir el marco por el carácter deseable de esta fila | STD-04 | D1; C3/D3 | D1 B6.7 y SEC-SAMM-01; responsable, evaluación inicial, plan y revisión anual pendientes | EN CURSO |

## 3. Estándares de FEP02 §11.5

Este numeral no agrega códigos RT. Se controla a través de las filas anteriores y de la [matriz global §4](../../00_Gobierno/02_MATRIZ_CUMPLIMIENTO_GLOBAL.md):

| Ámbito | Referencia de §11.5 | Destino de trazabilidad |
|---|---|---|
| Gestión y controles de seguridad | ISO/IEC 27001 y 27002 | RT-11.05; STD-01/02 |
| Nube y datos personales en nube | ISO/IEC 27017 y 27018 | RT-11.06; STD-02 |
| Marco de ciberseguridad | NIST CSF 2.0 | STD-03; D1/D2, controles y gestión de riesgos |
| Zero Trust | NIST SP 800-207 | RT-11.01; STD-03 |
| Seguridad de aplicaciones | OWASP ASVS 4.0 L2 mínimo, Top 10 y API Security Top 10 | STD-04; D1/C3, requisitos y pruebas por interfaz |
| Endurecimiento | CIS Benchmarks del producto | STD-05; D1/C2/C3, configuración y excepciones justificadas |
| Cadena de suministro | SLSA 3+ | RT-11.24; STD-06 |
| Continuidad | ISO 22301 e ISO/IEC 27031 | STD-07; C3/D1, planes y pruebas |
| Normativa nacional según aplicabilidad | Leyes 21.719, 21.663, 21.459 y 19.799 | RNF-CUM pertinentes; D1/D3 y responsables de cumplimiento: matriz de aplicabilidad, control y evidencia por obligación |

**Certificación y diseño se acreditan por separado:** aquí se demuestra cómo el diseño aplica los controles. Los certificados institucionales y profesionales se verifican conforme FEP02 §15.2/15.3 y FEP01, con Célula 1/equipo y `ESC-12`. Mencionar una norma o diseñar un control no acredita una certificación; tampoco basta con un certificado para demostrar que el componente implementa el control requerido.

## 4. Precisión pendiente en Célula 2

En [RNF.md](../../../Celula2/01_Requerimientos/RNF.md), `RNF-SEG-07` (brecha ≤24 h) cita RT-11.18 y `RNF-SEG-11` (incidente crítico ≤2 h) cita RT-11.19. Las referencias están intercambiadas respecto al PDF FEP02, §11.3, página impresa 24: **RT-11.18 corresponde al incidente crítico ≤2 h; RT-11.19 a la brecha ≤24 h y causa raíz ≤5 días hábiles**. Esta traza utiliza la referencia oficial correcta; no modifica Célula 2 ni sus identificadores. Pendiente de corregir con sus responsables; los plazos sustantivos existentes se mantienen.

## 5. Avance por bloque — evidencia de diseño, no de ejecución

| Bloque / control | Fuente específica de entrada | Evidencia documental actual | Falta para cerrar | Estado |
|---|---|---|---|---|
| B1 / SEC-IAM-01 (parcial) | Maestro §§5/6/11.2; FEP02 Cap. 12; Caso 06 Cap. 15 RT-12.11/13.08; RNF-SEG-10; RF-ACC-01..05/08/09 | [D1 B1.2–B1.5](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b1-alcance-e-identidad--borrador-inicial): reglas, 16 actores, perfiles y escenarios | Sesiones, autonomía/revocación, PAM, roles definitivos A1 y mapeo físico | EN CURSO |
| B1 / SEC-IAM-01 (autorización parcial) | FEP02 Cap. 11 RT-11.01/11.27; RNF-SEG-01/09; RF-POR-02/09 y RF-INT-02 | D1 B1.2/B1.3/B1.5: privilegio mínimo, ámbito por organización y restricción de producción | Zero Trust completo, políticas materializadas, representación externa y pruebas | EN CURSO |

Las filas generales y de RT conservan su alcance total. B1 es un avance parcial hacia TRZ-D1-001/002/006 y RT-11.01/11.27; no cierra sus obligaciones ni el modelo STRIDE de D2. Cada prueba de B1.5 está prevista, no ejecutada.

## 6. Identidad y sesiones — FEP02 capítulo 12, avance B2

Fuente de contraste: texto extraído de FEP02, páginas PDF 26–27 (impresas 25–26), consultado el 2026-09-05. Referencias siempre a FEP02; el Caso 06 concreta terreno y usuarios externos. Evidencia de diseño en [D1 B2](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b2-sesiones-y-continuidad-de-identidad--propuesta), control SEC-IAM-01. Todas las filas son parciales, sin prueba ejecutada ni aprobación.

| RT | Materia | Sección de diseño | Validación pendiente | Estado |
|---|---|---|---|---|
| RT-12.01 | Identidad centralizada, OIDC/OAuth 2.1 o SAML cuando requerido, directorio | B2.2/B2.7 | Producto, directorio e interoperabilidad F3-ESC-001 | EN CURSO |
| RT-12.02 | SSO y cierre propagado | B2.3 | Invalidación en módulos y comportamiento aislado | EN CURSO |
| RT-12.03 | MFA administradores, privilegiados y todo acceso externo | B1.4/B2.3 | Configuración y pruebas de acceso | EN CURSO |
| RT-12.04 | Soporte de factores resistentes a phishing para administradores | B2.3 | Producto/factor y recuperación | EN CURSO |
| RT-12.05 | Roles, atributos y segregación verificable | B1.2–B1.5/B2.2 | A1 y matriz definitiva de funciones | EN CURSO |
| RT-12.06 | Elevación temporal, aprobación, grabación de mayor riesgo | B2.3/B2.5 | PAM, custodios, suplencias y prueba | EN CURSO |
| RT-12.07 | Máximo, inactividad, renovación tras autenticación, revocación inmediata y concurrencia | B2.3/B2.4 | Parámetros propuestos; aislamiento F3-ESC-002, sin cumplimiento declarado | EN CURSO |
| RT-12.08 | Sesiones firmadas breves, refresco rotatorio, sin ID en ruta URL | B2.3 | Configuración y prueba de reutilización/invalidez | EN CURSO |
| RT-12.09 | Auditoría de ciclo de identidad, no repudio y retención | B2.5 | Inmutabilidad, integridad y capacidad en bloque de registros | EN CURSO |
| RT-12.10 | Aprovisionamiento laboral automatizado y baja ≤24 h desde desvinculación | B2.2/B2.4 | Fuente laboral y avisos efectivos durante corte | EN CURSO |
| RT-12.11 | Autenticación según perfil de terreno; aplica al caso | B2.3/B2.4 | Ensayo guantes, sin correo/biometría obligatorios; relevo | EN CURSO |
| RT-12.12 | Registro/verificación/recuperación externos; aplica al caso | B1.2/B2.3 | Procedimiento detallado de verificación/recuperación y representación RF-POR-02 | EN CURSO |
| RT-12.13 | Emergencia, custodia, control y auditoría | B2.5 | Custodios, contingencia de aprobación y prueba A3/C3 | EN CURSO |

Cruces de continuidad: RNF-DIS-02/03/04 → B2.1/2.4/2.5/2.6; RF-ACC-01..05 → B2.2/2.3/2.6. Los valores 5 min, 15 min, 30 min, 8 h de sesión y límites de concurrencia son **propuestas de diseño**, no umbrales atribuidos a FEP02. Las 8 h offline de RNF-DIS-03 sí son obligación del caso y se verifican aparte.

## 7. Bloque B3 — decisiones y cobertura parcial

Detalle de requisito → decisión → implementación propuesta → evidencia en [D1 B3.3](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b33-decisiones-de-control-y-trazabilidad-directa). Fuente oficial de exposición: FEP02 Cap. 11 §11.2, página impresa 23 / PDF 24, texto extraído consultado 2026-09-05. Sin pruebas ejecutadas ni cumplimiento final declarado.

| Fuente | Control | Evidencia documental / pendiente | Estado |
|---|---|---|---|
| Caso 06 Cap. 15 RT-03.24; Cap. 10 restricción 6; RNF-SEG-06; FEP02 RT-11.01 | SEC-NET-01 | B3.1 zonas y B3.2 flujos; topología/rutas y ensayo C3 pendientes | EN CURSO |
| FEP02 Cap. 11 RT-11.07/12 | SEC-EDGE-01 | B3.3/4 borde exclusivo, caché, WAF/DDoS y bots; proveedor, reglas/capacidad y pruebas pendientes | EN CURSO |
| FEP02 Cap. 11 RT-11.08; RNF-SEG-04 | SEC-EDGE-02 | B3.4 TLS/HSTS/certificados; dominios, precarga, custodia B4 y compatibilidad pendientes | EN CURSO |
| FEP02 Cap. 11 RT-11.11; RF-POR-02/09; RF-INT-02; RNF-SEG-09 | SEC-API-01 | B3.2/3/4 autorización/esquema/cuotas; contratos A2 y límites C4 pendientes | EN CURSO |
| FEP02 Cap. 11 RT-11.27; Cap. 12 RT-12.03/06/13 | SEC-ADM-01 | B2.5/B3.3 administración controlada; PAM/configuración/emergencia pendientes | EN CURSO |
| RNF-DIS-02/04; RNF-SEG-04; Maestro §§6.2/8/9 | SEC-SYNC-01 | B3.2/3 canal acotado y autonomía; transporte/autoridad/llaves/capacidad pendientes | EN CURSO |
| FEP02 Cap. 11 RT-11.13 | SEC-EXP-01 | B3.5 inventario por familias; falta cada dominio/puerto/servicio real y contraste externo | EN CURSO |

B3 desarrolla parcialmente TRZ-D1-001/003/006 y los RT indicados. Z-* y FL-* son referencias locales de D1 por validar, no catálogo oficial de red. HTTPS TCP 443 y umbrales de aviso de certificados son propuestas de diseño; no se atribuyen como cifras a las Bases.

## 8. Bloque B4 — datos, claves y secretos

Detalle de diseño en [D1 B4](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b4-datos-claves-y-secretos--propuesta). Fuentes principales: FEP02 Cap. 11 RT-11.03/08/09/10/25; Caso 06 Cap. 15 RT-11.10; FEP02 Cap. 7 RT-07.09..12; `RNF-SEG-04/05/09`, `RNF-DIS-02/04/14`, Maestro §§9/11/16 y guía de coordinación con Subdocumento 5. Sin producto, configuración, prueba ni aprobación.

| Fuente / control | Decisión y evidencia documental actual | Falta para cerrar | Estado |
|---|---|---|---|
| RT-11.03 / SEC-DATA-01 | B4.1 propone `PUB/INT/CONF/RES`, herencia de clasificación y controles diferenciados; B4.2 la cruza con DATA-CORE/TS/DOC/AN | Subdoc. 5 confirma catálogo campo→propietario→sensibilidad→retención; CLIENTE valida publicación y licitud | EN CURSO |
| RT-11.08 / SEC-EDGE-02 + SEC-KEY-01 | B3.4 define TLS/certificados; B4.4/6/7 añade custodia, propósito separado, rotación, recuperación y continuidad local | Dominios, emisores, productos, períodos y pruebas A2/C1–C3 | EN CURSO |
| RT-11.09 / SEC-ENC-01 + SEC-KEY-01 | B4.2 exige cifrado de todo reposo; B4.4–8 propone KMS/HSM/vault con gobierno común y capacidad local protegida, separación y ADR-009 alternativa C | Inventario/configuración completa, selección/HA/capacidad/T-11, custodios y recuperación ejecutada | EN CURSO |
| RT-11.10 / SEC-FIELD-01 | B4.1/3 cubre categorías personales, comerciales sensibles y carga/ruta mediante cifrado por envoltura y descifrado solo en servicio | Catálogo de 100 % de campos y prueba de consulta directa sin revelación | EN CURSO |
| RT-11.25 / SEC-DATA-01 | B4.1 prohíbe datos productivos reales en no producción salvo anonimización/seudonimización verificable | B6 materializa aprovisionamiento, escaneo/bloqueo y evidencia | EN CURSO |
| RT-07.09..12 / SEC-BKP-01 | B4.2/5/7/8 conserva cifrado, 3-2-1-1-0, separación de borrado/custodia y recuperabilidad de claves | C2/C3 emplazan copias; C4 dimensiona; restauración mensual y resistencia al borrado se ejecutan | EN CURSO |
| RNF-DIS-02/04 / SEC-KEY-01 | B4.7 mantiene cifrado/descifrado/firma local de las cinco funciones durante 72 h y protege reconciliación | A2/A3/C1–C4 validan autoridad, transporte, HA y capacidad; simulacro y conciliación ≤90 min | EN CURSO |

`PUB/INT/CONF/RES`, el cifrado por envoltura y la alternativa C son decisiones propuestas por TERABYTE, no texto literal de las Bases. Las obligaciones literales son clasificación con controles, cifrado total en reposo, KMS/HSM con rotación/separación y cifrado adicional de los campos del caso. Las periodicidades ordinarias y suites criptográficas permanecen por definir en una política versionada; no se convierten en cifras inventadas.

## 9. Bloque B5 — detección y respuesta

Detalle de diseño en [D1 B5](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b5-detección-y-respuesta--propuesta). Fuentes principales: FEP02 Cap. 11 RT-11.04/14..21; `RNF-SEG-03/07/08/11`, `RNF-OPE-05/08/11`, `RNF-DIS-02/04`, Maestro §§9/11/16 y Caso 06 restricción 11. Sin producto, contrato, dimensionamiento, prueba ni aprobación.

| Fuente / control | Evidencia documental actual | Falta para cerrar | Estado |
|---|---|---|---|
| RT-11.14 / SEC-LOG-01 | B5.1/2.1/7 diseña esquema, política de admisión/deduplicación, variables de capacidad, minimización, colector/buffer local, repositorio inalterable y retención 12 meses en línea + 24 adicionales en archivo | inventario de fuentes A1/A2; medición C4 de EPS, bytes, peaks y factores; ubicación/HA C1–C3 y pruebas de integridad/corte/recuperación | EN CURSO |
| RT-11.15 / SEC-SIEM-01 | B5.3 cataloga nueve casos portuarios y exige regla con fuente, propietario, acción, corte y prueba | D2 refina amenazas/severidades; A1–A3 confirman eventos; producto y afinamiento/pruebas pendientes | EN CURSO |
| RT-11.16 / SEC-END-01 | B5.2 cubre nube, on-premise y puestos compatibles, con excepción explícita y controles compensatorios para OT/legado | inventario definitivo, compatibilidad, licencias y ensayo de detección/aislamiento seguro | EN CURSO |
| RT-11.17 / SEC-SOC-01 | B5.4 propone SOC gestionado/subcontratado 24x7 y separa su función de TI=5/operación del CLIENTE | validar ADR-010, ubicación, dotación, proveedor, RACI, SLA, canales, procedimientos y costo T-11 | EN CURSO |
| RT-11.18/19 / SEC-IR-01 | B5.5 conserva crítico ≤2 h desde detección, brecha ≤24 h e informe de causa raíz ≤5 días hábiles; distingue reloj RNF-OPE-05 | responsables nominales, canales alternativos, plan aprobado, simulación e informes con cronología | EN CURSO |
| RT-11.04 / SEC-VULN-01 | B5.6 conserva escaneo y plazos crítica ≤7 días corridos, alta ≤15, media ≤30 desde publicación/detección | cobertura/herramienta, responsables y evidencia real de remediación/reprueba | EN CURSO |
| RT-11.20 / SEC-PENTEST-01 | B5.6 exige tercero independiente, anual y antes de cada producción, informe íntegro, plan y reprueba | tercero, alcance, calendario, informes y cierres ejecutados | EN CURSO |
| RT-11.21 / SEC-IR-01 | B5.6 propone incorporar simulación anual con participación del CLIENTE y acta/mejoras | aceptación explícita por ser requisito deseable y calendario operativo | EN CURSO |

**Ajuste para `T11-SEC-04` (identificador informado por Frente 2, aún no integrado en esta rama):** B5.2.1 cierra la ambigüedad de alcance documental —qué clases ingresan completas, cuáles se agregan y qué telemetría permanece en el dominio operacional—, pero no cierra capacidad. C4 debe medir fuentes, EPS, tamaño, peaks, reducción y factores de almacenamiento; el piso conocido no sustituye el término dominante. La traza queda `EN CURSO`, no aprobada.

La alternativa C de ADR-010 —detección híbrida federada y SOC gestionado 24x7— queda `PROPUESTO`, no `APROBADO`. La alarma operativa permanece en su sistema local; el SIEM correlaciona señales de manipulación o acceso indebido, sin sustituir la autoridad de operación ni asumir video general de `EXT-VMS`.

## 10. Bloque B6 — desarrollo y operación seguros

Detalle de diseño en [D1 B6](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b6-desarrollo-y-operación-seguros--propuesta). Fuentes principales: FEP02 Cap. 11 RT-11.22..28; Cap. 4 RT-04.03..07/11; FEP01 Art. 4.3; `RNF-MAN-01..06/11`, Maestro §§11.3/12 y Subdocumento 5. Sin herramienta, configuración, ejecución, producto ni aprobación.

| Fuente / control | Evidencia documental actual | Falta para cerrar | Estado |
|---|---|---|---|
| RT-11.22 / SEC-PIPE-01 | B6.2 incorpora SAST/SCA/DAST/imágenes, además de compilación, pruebas y secretos; fallo de etapa o crítico bloquea | C3 configura herramientas/reglas y demuestra ejecuciones/bloqueos; D2 revisa cobertura | EN CURSO |
| RNF-MAN-01/02/11 / SEC-SDLC-01 | B6.1 protege rama, exige revisión por pares y cadena requerimiento→cambio→prueba→artefacto→despliegue también en mantención | plataforma, funciones y muestras reales de trazabilidad pendientes | EN CURSO |
| RNF-MAN-03/06 / SEC-PIPE-01 | B6.2 bloquea fallo de controles y cobertura de lógica de negocio bajo 70 % | configuración, medición y prueba de elusión/bloqueo pendientes | EN CURSO |
| RT-11.23/24 / SEC-SUPPLY-01 | B6.3 define construcción única, SBOM CycloneDX/SPDX por versión, firma y procedencia SLSA 3+ | registro, claves, evidencia de nivel, verificación en despliegue y entrega al CLIENTE | EN CURSO |
| RT-11.26 / SEC-SUPPLY-01 | B6.4 exige licencia, mantención, vulnerabilidades, origen, integridad, propietario y aprobación por dependencia/imagen/herramienta | catálogo y aprobaciones/rechazos ejecutados; integración con B5.6 | EN CURSO |
| RT-11.25 / SEC-NPDATA-01 | B6.5 usa sintéticos por defecto y gobierna anonimización/seudonimización, reidentificación y eliminación | campos/técnicas Subdoc. 5, ambientes C3 y prueba de no revelación | EN CURSO |
| RT-11.27 / SEC-PROD-01 | B6.6 prohíbe acceso interactivo directo normal y delimita excepción PAM temporal, aprobada, grabada y revocada | IAM/PAM, responsables y prueba completa; despliegue/retorno C3 | EN CURSO |
| RT-11.28 + FEP01 Art. 4.3 / SEC-SAMM-01 | B6.7 adopta SAMM o equivalente con base inicial, plan y revisión anual, conservando obligatoriedad FEP01 | alcance, responsable, evaluación y plan reales pendientes | EN CURSO |

`F3-DEC-004` construye una sola vez y promueve el mismo artefacto firmado; es decisión de diseño propuesta, no ADR adicional ni evidencia de SLSA ya alcanzada. Los términos técnicos se explican en D1 B6.9 y no sustituyen sus definiciones normativas.

## 11. Bloque B7 — auditoría y paquete temprano

> **Corte histórico:** esta sección conserva el estado observado antes de recibir e integrar A1–A3, C1–C4 y D2. Para el estado vigente de dependencias y cobertura debe leerse la §12 (`B7-R`).

Detalle y hallazgos en [D1 B7](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b7-auditoría-de-cobertura-y-paquete-temprano). Se auditó contra el contrato de D1, Maestro, Plan §8, matriz global, FEP02 capítulos 11/12, ADR y estado visible de los paquetes dependientes. Resultado documental al 2026-09-05:

| Comprobación | Resultado verificable | Estado |
|---|---|---|
| Trabajo requerido D1 | 11/11 materias con sección/control de diseño | EN CURSO; ninguna aprobada |
| FEP02 Cap. 11 | 28/28 RT con diseño enlazado; RT-11.02 pasa a `EN CURSO` con D2 B2 | EN CURSO; ninguna fila aprobada. La cobertura por componente real sigue pendiente de A1/A2/C1/C3 |
| FEP02 Cap. 12 | 13/13 RT con diseño enlazado | EN CURSO; pruebas/productos pendientes |
| Gobierno/nube/hardening | SEC-GOV-01, SEC-CLOUD-01 y SEC-HARD-01 agregados por B7-F02 | EN CURSO; mapeo/configuración/evidencia pendientes |
| Matriz SEC-* | 31 controles identificados con fuente, implementación, evidencia y responsable funcional | EN CURSO; nodos/amenazas/personas pendientes |
| SEC-PHYS-v0.1 | 17 grupos con tratamiento de T-11 y condición de inclusión/agrupación | LISTO PARA INTERCAMBIO; no transferido |
| ADR | ADR-008/009/010 `PROPUESTO`; ADR-008 condicionado a F3-ESC-001/002; alternativas/criterios/consecuencias conservados | SIN ADR APROBADO |
| Montos/cantidades | sin montos; cantidades no inventadas y derivadas a C4 | CONFORME PARA INTERCAMBIO |
| Implementación/prueba | no se declara evidencia ejecutada | PENDIENTE por etapa |

Correcciones de estado: TRZ-D1-001/002/003/006 y RT-11.01/05/06/07/11/12/13 pasan a `EN CURSO` porque ya tienen diseño concreto enlazado. B7-F13 actualiza de igual forma las filas D1 correspondientes de la matriz global. Después del corte B7, `RT-11.02` pasa también a `EN CURSO` por el modelado provisional D2 B2–B5; no está cerrado porque falta refinarlo contra componentes e interfaces reales en D2 B6/B7. Los cambios no declaran conformidad final.

Dependencias de cierre: F3-DEP-001..004 continúan `PENDIENTE`; F3-ESC-001/002 continúan externos. A1–A3/C1–C4/D2 visibles siguen sin contenido desarrollado suficiente para validar componentes, contratos, autoridad, nodos, productos, capacidad o amenazas. Esto no impide entregar SEC-PHYS-v0.1, pero sí impide aprobar D1 y producir diagramas físicos definitivos.

`F3-DEC-005` evita la equivalencia errónea control = compra: C4 crea fila T-11 solo para un producto, servicio, licencia o hardware ofertado; una capacidad incluida se referencia desde la fila principal. El consolidado T-11 central no se modificó antes del intercambio con su propietario.

## 12. Corte B7-R — integración documental D1–D2

**Fecha: 2026-09-06.** Este corte supera únicamente los pendientes de entrada declarados en B7; no reescribe su resultado histórico.

| Universo | Resultado vigente | Estado |
|---|---|---|
| A1 | 16 actores y 24 componentes cruzados; `ACT-TI` conserva brecha de consola | CRUZADO CON OBSERVACIÓN |
| A2/A3 | contratos lógicos, autoridad, degradación y respaldo manual cruzados | RESUELTO PARA DISEÑO; contratos efectivos externos |
| C1–C4 | 21 nodos y 17 grupos SEC-PHYS emplazados/tratados; 7 candidatos T11-SEC y 10 incluidos/condicionales | CRUZADO CON OBSERVACIONES |
| D2 | 73 amenazas y 22 SPOF auditados; 31/31 controles D1 asociados | CONFORME DOCUMENTAL; `ADR-011` pendiente |
| RT-11.02 | método, inventario real, controles/evidencia y regla de cinco disparadores | CUBIERTO EN DISEÑO; EN CURSO por prueba/revisión/aprobación |
| Subdocumento 5 | campo→propietario→sensibilidad→retención | PENDIENTE |

Dependencias vigentes: `F3-DEP-001` cruzada con observación; `F3-DEP-002` resuelta para diseño documental; `F3-DEP-003` cruzada con observaciones; `F3-DEP-004` parcial porque D2 está disponible y el catálogo de campos no. Permanecen `F3-ESC-001/002`, `CTX-VESSEL`, diferencias de criticidad, `CH-CAB`, el posible solape SIEM, productos/contratos finales, site survey, responsables y pruebas.

**Conclusión:** D1 queda integrado y trazable para la revisión documental conjunta del Frente 3. No está aprobado; no hay pruebas ejecutadas ni riesgos aceptados. Diagramas y narrativa visual permanecen diferidos a B8.

## Corrección de fuente — 2026-09-06 (integrador)

| Control | Qué se corrigió | Verificación |
|---|---|---|
| `SEC-IAM-01` | Citaba `FEP02 Cap. 11, RT-11.27` como fuente. Ese código trata **exclusivamente** del acceso de personas desarrolladoras al ambiente de producción y no cubre la identidad de personas externas ni de eventuales, que es el alcance del control. Se sustituye por los códigos del Capítulo 12 que sí corresponden: `RT-12.01` federación y directorio, `RT-12.03` MFA, `RT-12.05` RBAC/ABAC con segregación, `RT-12.10` baja ≤24 h desde la desvinculación y `RT-12.11` credencial temporal de eventuales | Texto del `BTT` verificado: *«Las personas desarrolladoras no tendrán acceso interactivo directo al ambiente de producción…»*. Hallazgo `X-2` de la auditoría cruzada de Frente 1 |
| `SEC-PROD-01` y `SEC-ADM-01` | `RT-11.27` **se conserva**: ahí sí es la materia correcta | — |

