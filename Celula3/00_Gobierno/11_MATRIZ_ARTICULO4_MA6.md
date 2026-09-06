# Matriz de trazabilidad del Artículo 4 — MA-6

**Fecha:** 2026-09-06

**Estado histórico del bloque:** `MA-6 COMPLETADA — ARTÍCULO 4 TRAZADO`; MA-7 y MA-8 ya fueron completadas.

**Fuente contractual:** Bases Administrativas FEP01, Art. 4.1–4.3, páginas PDF 6–7.
**Alcance:** baseline del Informe 1; no acredita controles ejecutados, certificaciones obtenidas ni aceptación del CLIENTE.

## 1. Regla de cumplimiento aplicada

El Artículo 4.3 advierte que mencionar un estándar sin evidenciar cómo la solución lo satisface obtiene cero. Por eso cada fila conserva la cadena:

`estándar o norma → requisito aplicable → control concreto → componente → evidencia del Informe 1 → evidencia futura`

En este corte, **evidencia del Informe 1** significa diseño, decisión, matriz, cálculo o criterio de aceptación verificable. **Evidencia futura** significa configuración, prueba, certificado, acta o medición que todavía no existe porque la solución no está implementada. Esta distinción evita presentar un compromiso como si ya estuviera ejecutado.

Estados usados:

- `CUMPLE I1`: la arquitectura ya expresa el requisito, el control, el componente y la evidencia de diseño; puede conservar evidencia de ejecución futura.
- `PARCIAL CONTROLADO`: existe diseño suficiente para avanzar, pero falta un artefacto exigible de cierre identificado.
- `CONDICIONADO EXTERNO TRATADO`: la brecha depende de una acreditación, dato o aprobación externa y tiene dueño y evidencia de cierre.
- `NO APLICA JUSTIFICADO`: el supuesto que activaría el estándar no forma parte de la baseline.

## 2. Estándares y marcos del Artículo 4.3

| STD-ID | Estándar o marco | Aplicabilidad y requisito aplicado | Control concreto | Componente o ámbito | Evidencia I1 | Evidencia futura | Sección de destino | Estado |
|---|---|---|---|---|---|---|---|---|
| `STD-A4-01` | ISO/IEC 27001 | SGSI aplicable al servicio y control formal de riesgos, activos, responsables y excepciones | `SEC-GOV-01`: matriz de aplicabilidad control→implementación→evidencia, dueño y vencimiento | gobierno transversal; 24 componentes y servicios ofertados | D1 §§B7.3–B7.4; matriz de 31 controles; D2 amenazas/SPOF | certificado vigente o plan formal permitido, alcance del SGSI y auditoría | SD4 seguridad; expediente administrativo/T-6 | `CONDICIONADO EXTERNO TRATADO` |
| `STD-A4-02` | ISO/IEC 27002 | controles de seguridad seleccionados según activos, amenazas y riesgo | controles `SEC-*` de identidad, red, datos, operación y desarrollo, cada uno con prueba prevista | todas las capas A1 y nodos C1 | D1 matriz obligatoria; D2 `THR-001..073`; cruce 31 controles→amenazas | SoA definitiva, responsables nominales y evidencias de operación | SD4 seguridad y trazabilidad | `CUMPLE I1` |
| `STD-A4-03` | ISO/IEC 27017 | responsabilidades y configuración segura de servicios cloud | `SEC-CLOUD-01`: servicio→dato→responsable→configuración→evidencia→salida | AWS `sa-east-1`/`us-east-1`; EKS, RDS, S3, integración y analítica | D1 §B7.3; C2 catálogo AWS; `ADR-011`; T11-C2-17/18 | matriz compartida por servicio, configuración exportada y revisión contractual | SD4 nube/seguridad | `CUMPLE I1` |
| `STD-A4-04` | ISO/IEC 27018 | tratamiento y protección de datos personales en nube | `SEC-CLOUD-01` + `SEC-DATA-01/FIELD-01`: clasificación, mínimo privilegio, cifrado y eliminación | `DATA-CORE`, `DATA-DOC`, respaldos y analítica con datos personales | D1 §§B4.1–B4.3/B7.3; RNF-CUM-03; arquitectura de datos enlazada al Subdoc. 5 | registro de tratamientos, base de licitud, subencargados, transferencia y prueba de borrado | SD4 seguridad; Subdoc. 5 | `CUMPLE I1` |
| `STD-A4-05` | NIST Cybersecurity Framework 2.0 | gobernar, identificar, proteger, detectar, responder y recuperar | `SEC-GOV-01`; controles D1 agrupados por función y enlazados a amenaza/evidencia | gobierno, protección, SOC, IR, continuidad y DR | D1 B1–B7; D2 escenarios, amenazas y SPOF; C3 continuidad | evaluación de madurez, métricas y evidencias operativas | SD4 seguridad/continuidad | `CUMPLE I1` |
| `STD-A4-06` | NIST SP 800-207 | Zero Trust: no confiar por ubicación; validar identidad, dispositivo, recurso y contexto | `SEC-NET-01`, `SEC-API-01`, `SEC-IAM-01`, `SEC-ADM-01`; zonas y conductos explícitos | `GW-EDGE`, `GW-API`, `SRV-IAM`, servicios, edge y administración | D1 §§B1–B3, nueve zonas y once flujos; C3 §5.bis | pruebas de rutas, políticas por recurso, acceso PAM y operación aislada | SD4 seguridad/red | `CUMPLE I1` |
| `STD-A4-07` | OWASP ASVS 4.0 nivel 2 | requisitos verificables de seguridad para portal, app, APIs y servicios | puertas `SEC-PIPE-01` más autenticación/autorización `SEC-API-01`; checklist ASVS L2 por versión | `CH-PORTAL`, `CH-APP`, `GW-API`, `CTX-*` y `SRV-*` | D1 §§B3.3/B6.2; T11-C3-04 | matriz ASVS por requisito, resultados SAST/DAST y pruebas manuales | SD4 seguridad/DevSecOps | `CUMPLE I1` |
| `STD-A4-08` | OWASP Top 10 | prevenir y verificar debilidades web comunes | SAST, SCA, DAST, revisión de configuración y bloqueo de críticos en `SEC-PIPE-01` | portal, backend y servicios web | D1 §§B6.1–B6.2; catálogo tecnológico C2 | informes de pipeline, excepciones y repruebas | SD4 seguridad/DevSecOps | `CUMPLE I1` |
| `STD-A4-09` | OWASP API Security Top 10 | controlar objeto, función, esquema, tasa, inventario y exposición de APIs | `SEC-API-01` + `SEC-EXP-01`; autorización en servicio y contrato versionado | `GW-API`, `CTX-*`, integraciones externas | D1 §§B3.3/B3.5; A2 §1.2; D2 amenazas de API | pruebas BOLA/BFLA, fuzzing, abuso, inventario observado y pentest | SD4 integración/seguridad | `CUMPLE I1` |
| `STD-A4-10` | OWASP SAMM | gobernar y mejorar el proceso de desarrollo seguro | `SEC-SAMM-01`: línea base, plan de mejora y reevaluación anual | ciclo de ingeniería y mantenimiento | D1 §§B6.7/B7.3; T11-C3-04 | evaluación SAMM inicial, plan aprobado y reevaluación anual | SD4 gobierno/DevSecOps | `CUMPLE I1` |
| `STD-A4-11` | CIS Benchmarks | endurecimiento por producto y versión | `SEC-HARD-01`: baseline CIS o guía equivalente, desviación con riesgo, aprobador y vencimiento | Linux, EKS/contenedores, RDS, red, firewall, puestos y edge compatibles | D1 §B7.3; C2 tecnologías y política LTS/EOS; T11-C2-20 | escaneo de configuración, excepciones y reprueba | SD4 tecnologías/seguridad | `CUMPLE I1` |
| `STD-A4-12` | SLSA nivel 3 o superior | procedencia verificable y construcción controlada | `SEC-SUPPLY-01/ART-01`: construir una vez, registrar digest, firmar y verificar antes de promover | CI/CD, registro de artefactos y producción | D1 §§B6.3–B6.4; T11-C3-04 | attestations de procedencia, verificación en despliegue y auditoría de nivel | SD4 DevSecOps | `CUMPLE I1` |
| `STD-A4-13` | SBOM CycloneDX o SPDX | una SBOM por cada artefacto liberado | generación automática ligada al digest y catálogo de dependencias; falla bloquea promoción | artefactos de `CH-*`, `GW-*`, `CTX-*`, `SRV-*` e `INT-*` | D1 §§B6.2–B6.4; T11-C3-04 | SBOM por versión, entrega al CLIENTE y cruce contra vulnerabilidades | SD4 DevSecOps | `CUMPLE I1` |
| `STD-A4-14` | Firma de artefactos y verificación de procedencia | producción consume solamente artefactos aprobados e íntegros | firma, política de admisión y comprobación de digest/procedencia en `SEC-ART-01/PROD-01` | registro, pipeline y EKS/runtime local | D1 §§B6.3/B6.6; T11-C3-04 y T11-SEC-02 | firma real, log de verificación, rotación y recuperación de clave | SD4 DevSecOps/seguridad | `CUMPLE I1` |
| `STD-A4-15` | ISO 22301 | BIA, escenarios, procedimientos manuales y continuidad del negocio | clasificación de servicios, activación, comunicaciones, pruebas y revisión del plan | procesos críticos del terminal y dependencias externas | C3 §§6–10; cinco funciones críticas 72 h; RNF-DIS-07 | BIA validado, plan aprobado y ejercicios documentados | SD4 continuidad | `CUMPLE I1` |
| `STD-A4-16` | ISO/IEC 27031 | continuidad de capacidades TIC articulada con negocio | HA, buffer local, DR, respaldo, RTO/RPO, failover y retorno | núcleo local, AWS primario/secundario, red y datos | C3 §§7–10; C4 capacidad 72 h/90 min; ADR-007/011 | pruebas de corte, restauración y conmutación semestral | SD4 continuidad/DR | `CUMPLE I1` |
| `STD-A4-17` | ISO/IEC 20000-1 | procesos gobernados de servicio, incidente, cambio, configuración y nivel de servicio | catálogo y clasificación de servicios, trazabilidad de cambio, incidentes y evidencia | operación híbrida, SOC, soporte y plataformas | C3 §§6/9/10; D1 §§B5/B6; niveles por criticidad | modelo operativo, RACI, registros, mediciones y auditoría del servicio | SD4 operación; desarrollo posterior | `CUMPLE I1` |
| `STD-A4-18` | ITIL 4 | prácticas de incidentes, problemas, cambios, configuración y continuidad | flujo cambio→aprobación→despliegue; evento→incidente→RCA; catálogo/SLA | operación y mantenimiento | D1 §§B5.5/B6.1; C3 clasificación/continuidad | procedimientos, registros y métricas de práctica | SD4 operación; desarrollo posterior | `CUMPLE I1` |
| `STD-A4-19` | Site Reliability Engineering | objetivos medibles y operación basada en SLI/SLO, observabilidad y automatización | métricas, logs, trazas, alertas, presupuesto de error y automatización de recuperación | CloudWatch/OpenTelemetry/OpenSearch, servicios críticos | C2 observabilidad; C3 criticidad/RTO/RPO; D1 B5 | SLI/SLO medidos, alertas, runbooks y postmortems | SD4 despliegue/operación | `CUMPLE I1` |
| `STD-A4-20` | ISO/IEC 25010 | atributos de calidad expresados como requisitos medibles | RNF de disponibilidad, rendimiento, seguridad, usabilidad, mantenibilidad y portabilidad con verificación | solución completa | catálogo RNF de Célula 2; A1–C4 materializan arquitectura y capacidad | estrategia T-13 y resultados de prueba por atributo | SD4 decisiones/calidad | `CUMPLE I1` |
| `STD-A4-21` | ISO/IEC 25012 | calidad de datos: exactitud, completitud, consistencia, trazabilidad y actualidad | validación en contratos, autoridad única, conciliación, linaje y reglas por dato | `DATA-CORE/TS/DOC/AN`, `INT-HUB`, TOS y Subdoc. 5 | A2 contratos; A3 autoridad; RNF de Célula 2; enlace al Subdoc. 5 | diccionario/catálogo de campos definitivo, reglas y mediciones de calidad | SD4 integración; Subdoc. 5 | `PARCIAL CONTROLADO` |
| `STD-A4-22` | ISO/IEC/IEEE 29119 | estrategia, diseño, ejecución y evidencia de pruebas | criterios de aceptación por control, continuidad, capacidad, seguridad y contrato | todas las vistas; T-13 como artefacto dueño | pruebas previstas en A1–D2; C3 §§9–11; D1 matriz de evidencia | estrategia T-13, casos, resultados, defectos y cierre | SD4 criterios; T-13 posterior | `CUMPLE I1` |
| `STD-A4-23` | ISO/IEC/IEEE 42010 | descripción mediante interesados, preocupaciones, vistas, correspondencias y decisiones | catálogo canónico, cinco vistas, ADR y reglas de correspondencia lógica↔física↔seguridad | A1–D3 y Subdocumento 4 | Maestro; A1–D2; 11 ADR propuestos; matriz global | figuras finales y verificación de correspondencias B8/D3 | SD4 completo | `PARCIAL CONTROLADO` |
| `STD-A4-24` | TOGAF, declarado como marco de gobierno equivalente | gobernar baseline, decisiones, vistas, cambios y trazabilidad sin aplicar un ADM completo | Maestro, paquetes A/C/D, registro ADR, puertas MA/P y control de cambios | gobierno de arquitectura Célula 3 | Maestro, Plan de Entregables, Registro ADR y MA-0..MA-6 | acta de revisión y mantenimiento de baseline durante ejecución | SD4 decisiones/gobierno | `CUMPLE I1` |
| `STD-A4-25` | PMBOK Guide | marco base de dirección del proyecto; no es un componente de arquitectura | integración alcance–cronograma–riesgos–cambios–entregables; arquitectura entrega insumos y dependencias | gestión del proyecto, fuera del dueño de Célula 3 | trazabilidad de alcance, decisiones, dependencias e hitos desde Célula 3 | plan de proyecto/EDT/cronograma y evidencia de gobierno en Informe 2 | Subdoc. de gestión/Informe 2 | `CONDICIONADO EXTERNO TRATADO` |
| `STD-A4-26` | prácticas ágiles justificadas | iteración para desarrollo y validación sin reemplazar gobierno contractual | backlog trazado, revisión incremental y puertas de calidad dentro del marco PMBOK | ingeniería y validación | bloques A–D/MA y flujo DevSecOps D1 B6 | plan de iteraciones, Definition of Done y métricas | gestión/Informe 2 | `CUMPLE I1` |
| `STD-A4-27` | WCAG 2.2 nivel AA | interfaces humanas accesibles, teclado, foco, contraste, mensajes y objetivos táctiles | sistema de diseño, pruebas automáticas y manuales; controles de borde no bloquean ayudas técnicas | `CH-PORTAL`, `CH-APP`, `CH-CAB` | C2 stack exige WCAG; RNF-USA-01; D1 B3.4 preserva accesibilidad | sistema de diseño e informe de conformidad, entregable BTT N.º 17 | SD4 tecnologías; UX | `PARCIAL CONTROLADO` |
| `STD-A4-28` | EN 301 549 | referencia complementaria para requisitos TIC accesibles | checklist por tipo de interfaz/dispositivo y compra compatible | portal, app, terminal robusto y puestos | C2 catálogo de canal/equipos; RNF de accesibilidad | evaluación EN 301 549 junto al informe WCAG y fichas de dispositivo | SD4 tecnologías/implementos | `PARCIAL CONTROLADO` |
| `STD-A4-29` | OpenAPI 3.1 | contrato de todos los servicios síncronos | enfoque `contract-first`, versionado, compatibilidad, validación de esquema y prueba de contrato | `GW-API`, APIs `CTX-*`, autoridades cuando exista interfaz | A2 §§1.2/4/5; C2 contratos de interfaz; `SEC-API-01` | especificaciones publicadas, lint y pruebas contra despliegue | SD4 integración | `CUMPLE I1` |
| `STD-A4-30` | AsyncAPI 2.6 o superior | contrato de flujos dirigidos por eventos | baseline **AsyncAPI 2.6 o superior** `contract-first`, esquema, semántica, orden, idempotencia, DLQ y versión | `INT-HUB`, EventBridge/SQS y adaptadores | A2 §§1.2/4/5; C2 selección tecnológica; ADR-003 | especificaciones publicadas y pruebas productor/consumidor | SD4 integración | `CUMPLE I1` |
| `STD-A4-31` | UN/EDIFACT mantenido por SMDG | mensajería marítima estándar y versionada por naviera | adaptadores para BAPLIE, COPRAR, COARRI y CODECO; validación de origen/integridad y canal puente controlado | `INT-HUB`, `EXT-NAV-01..14` y sus adaptadores | A2 §3; RF-INT-01..07; RNF-POR-03 | factibilidad y contrato/versiones confirmadas por naviera | SD4 integración | `CUMPLE I1` |
| `STD-A4-32` | ISO 6346 | identificación de contenedores y verificación del dígito | validación de código antes de aceptar OCR, evento o movimiento | `EXT-OCR`, gate, patio, `INT-HUB` | RF-INT-08 y A2 catálogo de periferia | batería de códigos válidos/inválidos y evidencia de rechazo | SD4 integración/datos | `CUMPLE I1` |
| `STD-A4-33` | NIST AI RMF 1.0 | aplica solo si la solución incorpora IA | baseline usa reglas explícitas y aprobación humana; un cambio a IA activa ADR, riesgos y controles específicos | `CTX-PLAN` | A1/A3: algoritmo propone, persona aprueba/corrige; sin entrenamiento ni modelo IA | si cambia el alcance: registro de riesgos, pruebas y monitoreo de IA | SD4 decisiones | `NO APLICA JUSTIFICADO` |
| `STD-A4-34` | ISO/IEC 42001 | aplica solo si se incorpora un sistema de gestión de IA | misma condición de activación de `STD-A4-33`; no se simula un SGIA inexistente | `CTX-PLAN` | baseline determinista y supervisada, sin componente IA | si cambia el alcance: ADR, alcance del SGIA y evidencia | SD4 decisiones | `NO APLICA JUSTIFICADO` |
| `STD-A4-35` | ISO 14001 | referencia para aspectos ambientales y mejora verificable | inventario de consumo/emisiones, objetivos, responsables y datos trazables | sala técnica, AWS, equipos y `CTX-EMIS` | C2/C4 energía y PUE; A1 `CTX-EMIS`; RNF-CUM-09 | programa ambiental, mediciones y revisión | SD4 físico/sostenibilidad | `CUMPLE I1` |
| `STD-A4-36` | PUE del centro de datos | declarar eficiencia energética, carga TI y auxiliares | medir energía total/energía TI; baseline de diseño objetivo ≤1,60, referencia ≈1,45 | sala técnica primaria | C4 §6.2.bis: 2,67 kW TI y ≈3,87 kW total de referencia | medición estabilizada, tendencia y acciones correctivas | SD4 sala/capacidad | `CUMPLE I1` |
| `STD-A4-37` | huella de carbono; ISO 14083/GLEC e ISO 14064-3 como método adoptado | estimación trazable por contenedor y operación; verificación independiente | `CTX-EMIS`: factores versionados, dato de origen y cálculo reproducible | operaciones portuarias, equipos diésel/eléctricos y consumo cloud | A1 `CTX-EMIS`; RNF-CUM-09; C2 criterio regional de carbono | factores aprobados, medición regional AWS y verificación por tercero | SD4 lógica/física; Subdoc. 5 | `CUMPLE I1` |
| `STD-A4-38` | IEC 62443 como referencia sectorial de red OT | zonas y conductos sin comprometer redes operacionales ni plan ISPS | `SEC-NET-01`; segregación operacional, administrativa y protección; mínimo conducto aprobado | red del terminal, VMS, edge, núcleo y administración | C3 §§5/5.bis; D1 §§B3.1–B3.3; RNF-SEG-06 | topología levantada, aprobación de autoridad y prueba de rutas | SD4 red/seguridad | `CUMPLE I1` |

### Resultado del bloque de estándares

| Resultado | Cantidad | Lectura |
|---|---:|---|
| `CUMPLE I1` | 30 | control y evidencia de diseño identificados; la ejecución se acredita después |
| `PARCIAL CONTROLADO` | 4 | calidad de datos, figuras 42010 y artefactos de accesibilidad tienen dueño y salida definida |
| `CONDICIONADO EXTERNO TRATADO` | 2 | acreditación ISO 27001 y gestión PMBOK corresponden al expediente/equipo, no se inventan en arquitectura |
| `NO APLICA JUSTIFICADO` | 2 | la baseline no incorpora IA |
| **Total** | **38** | todos los estándares y prácticas exigidos quedaron respondidos |

## 3. Normativa nacional y sectorial con efecto arquitectónico

Esta tabla no emite una opinión jurídica ni reemplaza la matriz legal de la oferta. Registra únicamente el efecto que debe verse en el Subdocumento 4 y enlaza al dueño funcional o de datos cuando corresponde.

| NORM-ID | Norma o materia | Efecto arquitectónico aplicable | Control/componente | Evidencia I1 y cierre futuro | Estado |
|---|---|---|---|---|---|
| `NORM-A4-01` | Ley N.º 21.719 y, mientras corresponda, Ley N.º 19.628 | privacidad desde el diseño, finalidad, acceso mínimo, transferencia/residencia, retención y eliminación | `SEC-DATA-01/FIELD-01/CLOUD-01`; `DATA-*`; IAM | D1 B4 y RNF-CUM-03; Subdoc. 5 completa tratamientos/campos y evidencia de borrado | `PARCIAL CONTROLADO` |
| `NORM-A4-02` | Ley N.º 21.663, Ley Marco de Ciberseguridad; OIV | gestión de riesgos, continuidad, detección, respuesta y notificación | `SEC-GOV-01`, `SEC-SIEM-01`, `SEC-SOC-01`, `SEC-IR-01`; C3 continuidad | D1/D2 y C3; clasificación formal, RACI y ejercicios se acreditan en ejecución | `CUMPLE I1` |
| `NORM-A4-03` | Ley N.º 21.459 sobre Delitos Informáticos | preservar integridad, trazabilidad y evidencia frente a acceso, alteración o interrupción ilícita | IAM/PAM, logs inmutables, sellado, SIEM y custodia | D1 B1–B5 y D2 amenazas; cadena de custodia/procedimiento futuro | `CUMPLE I1` |
| `NORM-A4-04` | Ley N.º 19.799 sobre documentos y firma electrónica | firma/sello de tiempo y validación conservada para instrucciones, actas y hechos que lo requieran | `DATA-DOC`, `SEC-KEY-01`, `SRV-EVID`, `CTX-BILL/INSP` y evidencia local | requisitos Célula 2 y D1 B4; prestador/producto y pruebas por congelar | `CUMPLE I1` |
| `NORM-A4-05` | Leyes N.º 20.393 y N.º 21.595 | segregación de funciones, trazabilidad y conservación de evidencia; el modelo de prevención es dueño legal externo | `SEC-ADM-01/PROD-01/GOV-01`, auditoría y logs | D1 B1/B5/B6; validación por responsable legal/compliance | `CONDICIONADO EXTERNO TRATADO` |
| `NORM-A4-06` | Ley N.º 20.422 | interfaces y puestos accesibles sin excluir personas con discapacidad | `CH-PORTAL/APP/CAB`, WCAG y EN 301 549 | C2/RNF-USA-01; informe de conformidad futuro | `PARCIAL CONTROLADO` |
| `NORM-A4-07` | régimen de zona primaria aduanera | no ejecutar movimiento sin autorización aduanera registrada; fallback asistido auditable | `CTX-INSP`, `CTX-GATE`, `INT-HUB` y `EXT-AUT-*` | RNF-CUM-06; A2/A3; confirmar contratos/canales con Aduana | `CUMPLE I1` |
| `NORM-A4-08` | normativa ambiental aplicable | medir consumo/emisiones con método y conservar evidencia; no confundir estimación con certificación | `CTX-EMIS`, PUE, datos energéticos y telemetría | A1/C2/C4 y RNF-CUM-09; medición/verificación futura | `CUMPLE I1` |
| `NORM-A4-09` | ISPS/PBIP y plan de protección aprobado | segregación y cambios no pueden degradar CCTV, acceso ni protección; conducto mínimo con aprobación | `Z-PROT`, `SEC-NET-01`, `EXT-VMS/ACC`, C3 red | RNF-CUM-01; C3 §§5/5.bis; visado de autoridad/site survey pendiente | `CONDICIONADO EXTERNO TRATADO` |
| `NORM-A4-10` | SOLAS, verificación de masa bruta (VGM) | capturar pesaje, validar tolerancia y conservar trazabilidad 5 años antes de carga | `EXT-VGM`, `CTX-GATE/VESSEL`, `DATA-CORE` | RNF-CUM-04, RF/VGM y C4 retención; tolerancia chilena `ESC-13` por confirmar | `PARCIAL CONTROLADO` |
| `NORM-A4-11` | Código IMDG | impedir posiciones/planes incompatibles y versionar reglas de segregación | `CTX-YARD`, `CTX-PLAN`, `RN-02` | RNF-CUM-05 y reglas de negocio; batería completa y coordinación futura | `CUMPLE I1` |
| `NORM-A4-12` | normativa fitosanitaria y sanitaria | coordinar inspección y registrar fecha, autoridad y resultado; canal asistido si no hay API | `CTX-INSP`, `INT-HUB`, `EXT-AUT-*` y `LOC-INSP-01` | RNF-CUM-07; A2/A3; interfaz real depende de cada autoridad | `CONDICIONADO EXTERNO TRATADO` |
| `NORM-A4-13` | cadena de frío y programas de exportación | registro continuo, alarma ≤5 min y retención de temperatura 5 años | `CTX-REEFER`, `DATA-TS`, concentradores T11-C2-16 | RNF-CUM-08; A1/C3/C4; prueba de extremo a extremo futura | `CUMPLE I1` |
| `NORM-A4-14` | autoridad marítima y concesión portuaria | conservar aprobaciones, indicadores y trazabilidad; no asumir cambios físicos/red sin visado | `CTX-KPI`, `CTX-INSP`, red/seguridad y documentos | actores A1/A2 y RNF; interfaces, tolerancia VGM y visados siguen externos | `CONDICIONADO EXTERNO TRATADO` |
| `NORM-A4-15` | normativa laboral portuaria y seguridad y salud en el trabajo | operación por tres turnos, eventuales por nombrada, puestos fuera de sala y uso con guantes/intemperie | IAM local, `CH-APP/CAB`, `PHY-OPS-06`, terminales robustos | A1/D1/C2; evaluación de prevención, ergonomía y procedimiento de alta futura | `CUMPLE I1` |

### Límites de esta matriz

- La Ley N.º 19.886, los principios de contratación y las obligaciones laborales, previsionales y tributarias que no alteran la solución son obligaciones del proceso/oferta, no controles de arquitectura. Se mantienen bajo el integrador y los formularios administrativos/económicos.
- ISO 9001 y las certificaciones profesionales exigidas en el Capítulo 15 del BTT se acreditan en el expediente correspondiente. No se agregan artificialmente al Artículo 4.3, aunque la Matriz Global las conserve en su índice histórico.
- Célula 3 sí conserva las consecuencias técnicas de cumplimiento: segregación, privacidad, evidencia, accesibilidad, continuidad, firma, trazabilidad aduanera y reglas portuarias.

## 4. Dependencias que permanecen legítimamente abiertas

| Dependencia | Dueño/hito | Baseline mientras falta | Efecto de cierre |
|---|---|---|---|
| certificado o plan ISO/IEC 27001 y acreditaciones institucionales | equipo de oferta/Célula 1, antes de entrega formal | controles de solución trazados; no se afirma certificación inexistente | completa expediente, no cambia cajas de arquitectura |
| diccionario, tratamientos y reglas de calidad de datos | Subdocumento 5/Célula 4, antes de D3 | clases y controles D1; autoridad/retención ya fijadas | completa `STD-A4-04/21` y `NORM-A4-01` |
| sistema de diseño e informe WCAG/EN 301 549 | UX/frente responsable, antes de oferta técnica | stack y criterios accesibles obligatorios | completa `STD-A4-27/28` y `NORM-A4-06` |
| especificaciones OpenAPI/AsyncAPI ejecutables | desarrollo/integración, etapa de construcción | enfoque contract-first y reglas de compatibilidad ya decididos | aporta evidencia de ejecución; no cambia el patrón |
| contratos/versiones con navieras y autoridades | CLIENTE/contrapartes, levantamiento e integración | adaptador por contraparte, colas/DLQ y canal asistido | fija contrato real sin inventar interfaces |
| plan ISPS, tolerancia VGM y visados | CLIENTE/autoridad marítima, site survey/diseño de detalle | interpretación conservadora y ningún cambio unilateral | confirma red, reglas y aceptación sectorial |
| figuras ISO 42010 | Célula 3, producción final tras MA-8/P4 | catálogos y correspondencias ya estabilizados | cierra `STD-A4-23` |

Ninguna de estas dependencias justifica dejar el estándar sin respuesta. Todas tienen control, componente, baseline y evidencia futura.

## 5. Cruce con T-11 y Subdocumento 4

- Seguridad de nube, Zero Trust y protección de datos se materializan principalmente en `T11-C2-17/18/19`, `T11-C3-02`, `T11-SEC-01..07` y en capacidades incluidas explícitamente.
- SLSA, SBOM, firma, OWASP y SAMM se materializan en `T11-C3-04`; no generan una compra por cada estándar.
- WCAG, OpenAPI, AsyncAPI, ISO 25010 y las prácticas de desarrollo forman parte del servicio de construcción; no crean filas T-11 separadas.
- ISO 22301/27031 se materializa en el núcleo local, enlaces, respaldo y DR ya ofertados; las pruebas son evidencia futura.
- ISO 14001/PUE/huella se evidencian mediante mediciones y cálculos, no con una fila nueva si la capacidad está incluida en sala/plataforma.
- La normativa sectorial se expresa como reglas, controles e integraciones. Solo genera fila T-11 cuando requiere un implemento o servicio separable.

## 6. Veredicto MA-6

`AFI1-008` queda **cerrado para el alcance del Informe 1**: ningún estándar obligatorio permanece como mención huérfana. Las cuatro brechas parciales y las condiciones externas están tratadas con dueño y evidencia de cierre; no se presentan como cumplimiento ejecutado.

**Continuación histórica:** el siguiente bloque de ese corte fue MA-7. MA-7/MA-8 y P4 ya están completadas; la producción vigente sigue el plan `R1–R6` de `07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md`.
