# Plan maestro de cierre — Informe 1, Subdocumento 4 y Formulario T-11

**Fecha de línea base:** 2026-09-06

**Rama de referencia:** `main`

**Commit de referencia:** `4bd141b`

**Estado:** MA-0..MA-8 completadas como análisis/preparación. Alineación C3–C4 y estructura de trece subsecciones aprobadas como base. Redacción editorial conjunta, diagramas del equipo, ensamblado T-11, D3 y maquetación pendientes.

**Objetivo:** obtener un Subdocumento 4 coherente, trazable y proporcionado al Informe 1, con su T-11 completo, sin exigir evidencias de implantación ni decisiones que corresponden a entregas posteriores.

| Bloque | Estado vigente | Evidencia |
|---|---|---|
| MA-0 — línea base | COMPLETADO | cabecera y alcance del audit final |
| MA-1 — contraste contractual | COMPLETADO | audit §§1–3 |
| MA-2 — auditoría semántica | COMPLETADO | hallazgos `AFI1-*` |
| MA-3 — correcciones quirúrgicas | COMPLETADO | `08_REGISTRO_CORRECCIONES_QUIRURGICAS_MA3.md` |
| MA-4 — ADR | COMPLETADO | `09_REVISION_ADR_BASELINE_I1_MA4.md` |
| MA-5 — T-11 | COMPLETADO | `10_CONSOLIDACION_T11_MA5.md` + `90_Consolidado/01..02` |
| MA-6 — Artículo 4 | COMPLETADO | `11_MATRIZ_ARTICULO4_MA6.md` |
| MA-7 — proyección editorial y figuras | COMPLETADO | `12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md` |
| MA-8 — preparación D3 y mapa de ensamblado | COMPLETADO COMO PREPARACIÓN | `13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`; D3 no ejecutada |
| producción final | EN CURSO | base técnica y `V-DATA-01` completadas; redacción editorial, diagramas del equipo, ensamblado T-11 y maquetación pendientes |
| ejecución D3 | PENDIENTE DEL ARTEFACTO FINAL | trece controles, correcciones y veredicto |

## 0. Instrucción de uso para cualquier agente

1. Leer este archivo completo antes de modificar contenido.
2. Confirmar que se trabaja desde `main` actualizado o desde una rama creada explícitamente para este cierre.
3. No limpiar, mover ni versionar archivos ajenos o auxiliares del workspace (`.DS_Store`, PDF, ZIP, `tmp/`, planillas u otros no relacionados).
4. Ejecutar **un bloque `MA-*` a la vez**, verificar su definición de terminado y detenerse en las puertas marcadas `PAUSA`.
5. No dibujar diagramas definitivos antes de completar `MA-5`.
6. No convertir dependencias externas reales en datos inventados.
7. No promover ADR ni declarar cumplimiento por conveniencia editorial.
8. Toda corrección debe conservar la cadena:

   `fuente oficial → requisito → componente lógico → nodo físico → control → capacidad/cantidad → T-11 si aplica → diagrama → evidencia`

## 1. Resultado esperado

Al finalizar deben existir cinco resultados canónicos:

1. Auditoría final semántica y contractual del Informe 1.
2. Registro ADR con estados defendibles y una baseline suficiente para diagramar.
3. Matriz T-11 de trabajo completa y sin duplicidades.
4. Formulario T-11 final con exactamente cinco columnas.
5. Subdocumento 4 compacto, trazable y coherente con los Subdocumentos 3 y 5.

D3 será la **puerta que verifica esos resultados**. No será una cuarta auditoría extensa ni un depósito de antecedentes.

## 2. Autoridad y fuentes obligatorias

### 2.1 Fuentes oficiales

Revisar directamente los PDF; los Markdown de `Bases_caso/` ayudan a navegar, pero no sustituyen el texto oficial.

| Fuente | Ruta | Uso principal |
|---|---|---|
| Pautas del curso | `Base_pdfs/FEP00.1.26 - Pautas del Curso - 2026-08-03.pdf` | alcance temporal de Informes 1, 2 y 3; láminas PDF 16–18 |
| Bases Administrativas | `Base_pdfs/FEP01.26 Bases Administrativas TFEP-01-2026-3.pdf` | precedencia, Art. 4, Art. 16, T-7, T-11, T-21 y T-22 |
| Bases Técnicas Transversales | `Base_pdfs/FEP02.26 Bases Tecnicas Transversales TFEP-01-2026.pdf` | piso técnico `RT-*`, arquitectura, nube/on-premise, ambientes, integración, seguridad, continuidad y capacidad |
| Caso 06 Portuaria | `Base_pdfs/FEP03.06.26 Caso 06 - Portuaria (Bases Tecnicas del Caso).pdf` | contexto portuario, restricciones, magnitudes, decisiones abiertas y parámetros más exigentes |

Páginas de control rápido en FEP01:

- Artículo 4 y estándares: PDF 6–7.
- Artículo 16 y arquitectura híbrida: PDF 11–12.
- Formulario T-7: PDF 58–60.
- Formulario T-11: PDF 63.
- Formulario T-21: PDF 67–68.
- Formulario T-22: PDF 69–70.
- Prohibición de información económica, Art. 50.2: PDF 30.

### 2.2 Jerarquía

Aplicar FEP01 Art. 5.1–5.4 y el Maestro §1:

1. Bases Administrativas y anexos.
2. Bases Técnicas del caso y anexos.
3. Aclaraciones, respuestas y modificaciones formales.
4. Restantes documentos en el orden contractual.

FEP02 complementa las Bases Administrativas y establece un piso. El caso puede endurecerlo. Ante una contradicción real, no resolverla silenciosamente: registrar texto, impacto, lectura conservadora y consulta o dependencia.

### 2.3 Insumos internos vigentes

- `04_AUDITORIA_CRUZADA_A_C_D.md`.
- `05_CONSOLIDADO_AUDITORIAS_Y_PLAN_DE_CAMBIOS.md`.
- `AUDITORIA_GLOBAL_CELULA3_PRE_D3.md`.
- `Celula3/00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md`.
- `Celula3/00_Gobierno/02_MATRIZ_CUMPLIMIENTO_GLOBAL.md`.
- `Celula3/00_Gobierno/03_REGISTRO_ADR_GLOBAL.md`.
- A1–A3, C1–C4 y D1–D2, con sus trazas y decisiones.
- `Celula3/COMPLEMENTO_AUDITORIA_CATALOGO_TECNOLOGICO_SUBDOC4.md`.
- `Celula3/90_Consolidado/`.
- Célula 2 y Subdocumento 5 cuando una afirmación dependa de datos, retención, propiedad o fuente de verdad.

## 3. Alcance correcto del Informe 1

### 3.1 Lo que sí debe entregar

El Informe 1 incluye los Subdocumentos 1, 2, 3, 4, 5 y 13. Para Célula 3 importa especialmente:

- arquitectura lógica, 16 %;
- arquitectura física, 16 %;
- tecnologías de software;
- implementos de hardware y software;
- data center o sala técnica primaria;
- data center secundario/DR;
- Formulario T-11;
- trazabilidad con el problema, alcance y datos.

### 3.2 Lo avanzado que se conserva como evidencia interna

- Las amenazas `THR-*`, escenarios `SCN-*` y SPOF apoyan la arquitectura de seguridad, pero no se publican completos en el Informe 1.
- El diseño de pruebas, controles operacionales, pipeline y runbooks puede citarse como compromiso o criterio futuro; no se presenta como evidencia ejecutada.
- Los cálculos extensos permanecen en C4; el documento final conserva resultados, supuestos decisivos y referencia.

### 3.3 Lo que pertenece a entregas posteriores

| Materia | Entrega |
|---|---|
| Análisis formal de riesgos de solución, desarrollo e implantación | Informe 2 |
| EDT, planificación, hitos y equipo | Informe 2 |
| Proveedores y adquisiciones clave | Informe 3 |
| Costos, flujo de caja, VAN/TIR y Curva S | Informe 3 |
| Prototipo interactivo | Informe 3 |
| Video y propuesta integral final | propuesta final |

Una obligación futura que condiciona la arquitectura debe aparecer como requisito o criterio de diseño, no como producto ya implantado.

## 4. Taxonomías obligatorias

### 4.1 Aplicabilidad temporal

| Estado | Significado |
|---|---|
| `EXIGIBLE I1` | debe estar resuelto o tratado en el Informe 1 |
| `BASELINE I1` | decisión adoptada por TERABYTE para presentar una solución coherente |
| `CONDICIONADO EXTERNO` | falta dato del CLIENTE, fabricante, site survey, medición o acta |
| `EVIDENCIA FUTURA` | el diseño existe, pero la prueba/ejecución corresponde a una etapa posterior |
| `FUERA DE I1` | no debe desarrollarse en este cierre salvo una referencia necesaria |

### 4.2 Resultado de auditoría

| Estado | Regla |
|---|---|
| `CUMPLE` | existe respuesta explícita, coherente, trazada y suficiente para I1 |
| `PARCIAL` | existe, pero falta decisión, precisión, evidencia o cruce |
| `NO CUMPLE` | falta o contradice una fuente oficial |
| `CONDICIONADO EXTERNO TRATADO` | no puede cerrarse internamente, pero tiene dueño, condición, fallback y evidencia futura |
| `NO APLICA JUSTIFICADO` | la materia no aplica y la razón está demostrada |

### 4.3 Estados ADR

Mantener los estados del Registro Global:

- `CANDIDATO`: alternativas identificadas, sin selección suficiente.
- `EN ANÁLISIS`: comparación en curso.
- `PROPUESTO`: TERABYTE seleccionó una alternativa y la documentó; puede estar condicionada.
- `APROBADO`: cumple la regla formal, fue revisado internamente y su efecto está propagado.
- `BLOQUEADO EXTERNO`: no se puede resolver sin información externa.
- `SUPERADO`: reemplazado por otra decisión.

`APROBADO` es una aprobación interna de arquitectura; no significa aceptación del CLIENTE. No todos los ADR necesitan quedar aprobados para el Informe 1. Los que determinan emplazamiento, cantidades o una fila T-11 sí deben entregar una baseline coherente, aunque sea propuesta y condicionada.

## 5. Artefactos a producir o completar

| Artefacto | Acción |
|---|---|
| `06_AUDITORIA_FINAL_SEMANTICA_CONTRACTUAL_INFORME1.md` | crear en la raíz como cierre de las auditorías anteriores |
| `Celula3/00_Gobierno/03_REGISTRO_ADR_GLOBAL.md` | revisar estados y sincronizar efectos |
| `Celula3/90_Consolidado/01_T11_TRABAJO_TRAZABLE.md` | sustituir la fila ficticia por el catálogo consolidado |
| `Celula3/90_Consolidado/02_FORMULARIO_T11_FINAL.md` | completar exactamente las cinco columnas oficiales |
| `Celula3/03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md` | ejecutar como puerta final |
| `Celula3/03_Frente_Seguridad_Consolidacion/trazabilidad/TRZ_D3.md` | completar evidencia de la puerta |
| `Celula3/90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md` | base técnica y destino de la síntesis entregable |

No crear matrices paralelas si una existente puede convertirse en la fuente canónica.

## 6. Ejecución por bloques

## `MA-0` — Congelar alcance y línea base

### Trabajo

1. Confirmar `main`, commit y estado del workspace.
2. Registrar qué archivos son evidencia y cuáles serán entregables.
3. Clasificar las materias existentes con la taxonomía temporal de §4.1.
4. Verificar que ninguna corrección posterior al commit de corte quedó fuera.
5. Crear la cabecera y metodología de la auditoría final.

### Salida

Secciones 0–2 de `06_AUDITORIA_FINAL_SEMANTICA_CONTRACTUAL_INFORME1.md`:

- corte exacto;
- fuentes oficiales;
- alcance I1;
- exclusiones;
- método;
- escala de hallazgos.

### Definición de terminado

- No se confunde Informe 1 con Informe 2, 3 o propuesta final.
- Cada paquete A–D tiene una función declarada en el audit.
- No se modificó todavía ningún entregable sustantivo.

## `MA-1` — Auditoría contractual contra PDF oficiales

### Trabajo

1. Verificar directamente T-7, T-11, T-21 y T-22.
2. Construir el universo de requisitos de Subdocumento 4.
3. Incorporar requisitos FEP02 que materializan lógica, físico, integración, seguridad, continuidad y capacidad.
4. Incorporar restricciones y parámetros del Caso 06.
5. Separar requisito obligatorio, deseable, según caso y materia futura.
6. Contrastar siempre `documento + capítulo + código + materia`; no confiar en el código aislado.

### Fila mínima del audit

| ID | Fuente oficial | Texto/materia | Aplicabilidad | Evidencia actual | Estado | Brecha | Corrección | Dueño |
|---|---|---|---|---|---|---|---|---|

### Definición de terminado

- Toda exigencia T7-4.1..4.8 está evaluada.
- T11 y Art. 16 tienen cobertura explícita.
- No hay código RT citado sin documento y materia cuando exista colisión.
- Los requisitos futuros están separados, no omitidos.

## `MA-2` — Auditoría semántica A–C–D

### Trabajo

Leer A1–A3, C1–C4 y D1–D2 de forma sustantiva. No limitarse a enlaces, tablas o conteos.

Cruces obligatorios:

| Eje | Verificación |
|---|---|
| Catálogo | mismo ID, nombre, responsabilidad y criticidad en todas las vistas |
| Lógico→físico | cada componente publicado tiene nodo y ubicación coherentes |
| Continuidad | 72 h local, 8 h de sombra, sincronización ≤90 min y RTO/RPO no se contradicen |
| TOS | autoridad por dominio×zona×fase, bidireccionalidad y retorno coinciden |
| Datos | almacén, fuente de verdad, retención y capacidad coinciden con Subdocumento 5 |
| Integración | contratos, broker, colas, DLQ, idempotencia y fallback son consistentes |
| Identidad | función crítica local, altas, revocación ≤24 h, PAM y terminales compartidos son posibles |
| Seguridad | control, amenaza, nodo, producto/licencia y evidencia se corresponden |
| DR | primario/secundario, dominios de fallo, respaldo, conmutación y retorno coinciden |
| Capacidad | toda cantidad publicada tiene cálculo, rango o criterio |
| T-11 | toda caja/producto ofertado tiene fila o inclusión justificada, sin duplicidad |

Buscar especialmente: `recordar`, `debe entregar`, `debe definir`, `por integrar`, `por confirmar`, `ya ofertado`, `ver A1`, `ver A2`, `ver C1`, `ver D1`, `POR HACER`, `POR DEFINIR` y `POR COMPLETAR`.

### Regla de referencias cruzadas

Una referencia puede demostrar origen, pero no sustituir contenido. En el consolidado final debe decirse la decisión y luego citar su evidencia. Frases como “recordar que está en A1” se convierten en:

1. afirmación sustantiva explícita;
2. ID canónico;
3. referencia estable a la evidencia;
4. estado o dependencia si corresponde.

### Salida

- Hallazgos `AFI1-*` ordenados por severidad y dueño.
- Tabla de contradicciones A↔C↔D.
- Lista de dependencias externas legítimas.
- Lista de contenido avanzado que debe resumirse o reservarse.

### Definición de terminado

- Cada afirmación crítica puede ser verdadera simultáneamente en lógica, físico y seguridad.
- No queda una dependencia interna disfrazada de dependencia externa.
- El audit indica cambio exacto, no recomendaciones genéricas.

### Puerta `P1 — PAUSA`

Entregar el audit al usuario. No aplicar correcciones hasta revisar juntos:

- críticos y altos;
- decisiones que cambien arquitectura;
- asuntos que se mantendrán condicionados;
- contenido que se excluirá de I1.

## `MA-3` — Correcciones quirúrgicas

### Orden

1. Contradicciones contractuales o internas.
2. Vacíos exigibles del Informe 1.
3. Referencias vagas entre frentes.
4. Estados y textos históricos que parecen vigentes.
5. Trazabilidad y enlaces.
6. Reducción editorial de contenido futuro.

### Reglas

- Corregir en el dueño canónico y propagar solo donde corresponda.
- No reescribir paquetes completos.
- Registrar `hallazgo → archivo/sección → cambio → verificación`.
- Mantener separado hecho, decisión, supuesto, dependencia y evidencia futura.
- Un bloque lógico de corrección por commit, si se autoriza commit.

### Definición de terminado

- Todos los críticos están cerrados.
- Los altos están cerrados o como `CONDICIONADO EXTERNO TRATADO`.
- No hay nuevas contradicciones creadas por la propagación.
- `git diff --check` no reporta errores.

## `MA-4` — Revisión de ADR para la baseline I1

### Trabajo

Revisar `ADR-001..011` uno por uno contra:

1. contexto y fuerza de decisión;
2. dos o más alternativas reales cuando corresponda;
3. criterios vinculados al Caso 06;
4. decisión seleccionada;
5. consecuencias positivas y negativas;
6. riesgo residual;
7. efecto lógico, físico, seguridad, capacidad y T-11;
8. condición de revisión;
9. evidencia o validación futura.

### Prioridad

- `ADR-005`: sala técnica y Art. 16.
- `ADR-006`: red del patio y site survey.
- `ADR-007`: almacenamiento, HA y DR.
- `ADR-008`: identidad crítica local.
- `ADR-011`: proveedor/regiones y dominios de fallo.

Si falta un dato externo, fijar una arquitectura de referencia conservadora y declarar qué puede cambiar. No elegir una marca solo para subir el estado.

### Salida

Tabla:

| ADR | Estado actual | Evidencia suficiente | Estado recomendado | Condición abierta | Efecto I1/T11 |
|---|---|---|---|---|---|

### Puerta `P2 — PAUSA`

Validar con el usuario las decisiones que cambien cajas, ubicación, cantidades o promesas antes de construir T-11.

## `MA-5` — Catálogo único y Formulario T-11

### 5.1 Consolidación

Tomar candidatos desde C2 §9, C3 §13, C4 §9, D1 `SEC-PHYS`, C1 y los servicios derivados de A1–A3. Para cada candidato decidir:

- fila propia;
- agrupado con otro producto/servicio;
- incluido en una plataforma principal;
- condicional;
- `NO APLICA JUSTIFICADO`.

### 5.2 Categorías que deben revisarse

1. Cómputo, almacenamiento y red local.
2. UPS, generación, climatización, incendio, acceso y CCTV.
3. Gabinetes, concentradores, terminales y estaciones de trabajo.
4. Cómputo, datos, objetos, integración, analítica y DR en nube.
5. Sistema operativo y soporte.
6. IAM, MFA, PAM, KMS/HSM y secretos.
7. Observabilidad/SIEM, EDR y respaldo.
8. SOC, vulnerabilidades y pentest.
9. CI/CD, registro de artefactos y herramientas DevSecOps.
10. Enlaces, VPN y red operacional del patio.

### 5.3 Regla de fila

Una fila corresponde a infraestructura, plataforma, licencia, servicio o hardware **ofertado**. Un componente lógico no genera automáticamente una fila. Un framework abierto incorporado al desarrollo tampoco, salvo que se oferte soporte, licencia o plataforma separada.

### 5.4 Cantidades

Cada cantidad debe ser una de estas:

- número calculado;
- unidad de servicio o suscripción;
- rango con método y hito de cierre;
- incluida en otra fila, indicando cuál.

Nunca usar `POR COMPLETAR`, “ver A1” o una cantidad implícita.

### 5.5 Formulario final

Copiar solo las filas listas a `02_FORMULARIO_T11_FINAL.md`, conservando exactamente:

| Componente | Producto / servicio ofertado | Ubicación / Lugar | Cantidad | Justificación |
|---|---|---|---:|---|

No incluir precios, tarifas, costos unitarios ni montos inferibles.

### Controles bidireccionales

- Toda caja física ofertada tiene fila o inclusión justificada.
- Toda fila T-11 aparece en el catálogo y, cuando sea representable, en el diagrama físico.
- Toda cantidad vuelve a C4 o a un criterio verificable.
- Toda licencia/control de seguridad está incluida una sola vez.
- Toda ubicación coincide con C1/C3.
- Toda justificación explica función y emplazamiento.

### Puerta `P3 — PAUSA`

Revisar con el usuario el T-11 de trabajo y el formulario de cinco columnas antes de diagramar.

## `MA-6` — Matriz del Artículo 4

### Regla principal

No basta nombrar un estándar. Para cada uno debe existir:

`estándar → requisito aplicable → control concreto → componente → entregable/evidencia`

### Tabla canónica

| STD-ID | Estándar/norma | Aplicabilidad | Requisito aplicado | Control | Componente | Evidencia I1 | Evidencia futura | Sección | Estado |
|---|---|---|---|---|---|---|---|---|---|

### Familias obligatorias a controlar

- ISO/IEC 27001, 27002, 27017, 27018; NIST CSF 2.0 y NIST SP 800-207.
- OWASP ASVS 4.0 L2, Top 10, API Security Top 10, SAMM y CIS Benchmarks.
- SLSA 3+, SBOM CycloneDX/SPDX, firma y procedencia.
- ISO 22301 e ISO/IEC 27031.
- ISO/IEC 20000-1, ITIL 4 y SRE.
- ISO/IEC 25010, 25012 e ISO/IEC/IEEE 29119.
- ISO/IEC/IEEE 42010 y TOGAF o equivalente.
- PMBOK y prácticas ágiles justificadas.
- WCAG 2.2 AA y EN 301 549.
- OpenAPI 3.1, AsyncAPI 2.6+ y estándares portuarios.
- NIST AI RMF e ISO/IEC 42001 solo si existe IA.
- ISO 14001, PUE y huella de carbono.

### Normativa nacional y sectorial

Trazar solo el efecto arquitectónico aplicable: protección de datos, ciberseguridad/OIV, delitos informáticos, firma electrónica, accesibilidad, ambiente, aduana, ISPS, SOLAS/VGM, IMDG, cadena de frío y autoridad marítima. Subdocumento 5 es dueño de parte de datos; Célula 3 debe enlazarla, no duplicarla.

### Evidencia en Informe 1

Puede ser una decisión de diseño, matriz de controles, catálogo, criterio de aceptación o plan de verificación. No declarar como ejecutada una certificación, prueba, pentest, restauración o auditoría futura.

### Definición de terminado

- Ningún estándar obligatorio está solo nombrado.
- Todo condicional tiene `APLICA` o `NO APLICA JUSTIFICADO`.
- Se distingue certificación institucional de estándar de diseño.
- La matriz enlaza a secciones reales y no a promesas vagas.

## `MA-7` — Proyección editorial y plan de diagramas

### Regla editorial

Los documentos A–D son expediente de ingeniería. El Subdocumento 4 es su síntesis autónoma. No trasladar matrices completas cuando basta una conclusión y un enlace de evidencia.

### Extensión objetivo

Usar como guía 20–25 páginas para el Subdocumento 4, incluido el T-11, ajustable por plantilla y legibilidad. La cobertura manda; no se intenta igualar una propuesta final de otro año.

### Estructura mínima propuesta

#### 4.1 Arquitectura lógica

1. Esquema de solución.
2. Arquitectura lógica de la solución.
3. Integración y procesos críticos.
4. Datos y seguridad transversales.
5. Decisiones de arquitectura y cumplimiento.

#### 4.2 Arquitectura física

1. Arquitectura física y emplazamiento Art. 16.
2. Tecnologías de software.
3. Implementos de hardware/software.
4. Sala técnica primaria.
5. Sitio secundario y DR.
6. Despliegue, redes y continuidad.
7. Dimensionamiento y crecimiento.
8. Formulario T-11.

### Figuras previstas

| Figura | Pregunta que responde |
|---|---|
| F1 — Esquema de solución | quién interactúa y cuál es la frontera |
| F2 — Arquitectura lógica de ocho capas | qué responsabilidades existen y cómo se relacionan |
| F3 — Integración y proceso crítico | cómo fluyen contratos, eventos, autoridad, corte y retorno |
| F4 — Arquitectura física híbrida | dónde vive cada componente principal |
| F5 — Seguridad y límites de confianza | cómo se segmentan terminal, nube, edge y administración |

La vista de datos exigida se publica como tabla `V-DATA-01`, con autoridad, flujo, almacén, protección y dueño del detalle. `F6 — Continuidad` es condicional: solo se activa si F3/F4 no explican legiblemente operación normal, corte de hasta 72 h, reconciliación ≤90 min y DR.

No hacer diagramas repetidos por actor, catálogos de logos, 73 amenazas dibujadas ni detalle de CI/CD propio de etapas posteriores.

### Puerta `P4 — PAUSA`

**Estado corregido:** la estructura, la tabla de datos y las tablas publicables quedan como base de producción. El conjunto F1–F5 fue una recomendación de trabajo de MA-7, no una solicitud ni aprobación del usuario; sus bocetos están archivados y los diagramas definitivos quedan a decisión del equipo.

## `MA-8` — Preparación D3 y mapa de ensamblado

**Estado:** COMPLETADA COMO PREPARACIÓN; no confundir con auditoría ejecutada.

### Trabajo completado

- D3 actualizado a la estructura MA-7 de `4.1.1..4.1.5` y `4.2.1..4.2.8`.
- Trece secciones con fuente principal, contraste, figura/tabla y criterio D3.
- Trece controles `TRZ-D3-001..013` preparados sin marcarlos cumplidos.
- Esqueleto consolidado enlazado directamente a sus fuentes de llenado.
- Regla de síntesis definida para conservar evidencia sin copiar el expediente.

### Evidencia

[`13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`](13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md), D3 y `TRZ_D3.md`.

## Producción final y ejecución D3

La producción final no es otro bloque de investigación. Consume las baselines cerradas y ejecuta, en este orden: redacción conjunta por secciones, preparación de los diagramas que decida el equipo, conservación del cruce `V-DATA-01`, ensamblado T-11, auditoría D3, corrección y maquetación.

### Verificaciones

- Audit final tratado.
- Críticos cerrados y altos tratados.
- Lógico, físico, seguridad, capacidad y T-11 describen una sola solución.
- ADR con estados honestos y baseline suficiente.
- Artículo 4 trazado a controles y evidencia.
- T-11 sin vacíos, doble conteo ni precios.
- Diagramas consistentes con IDs, ubicación y cantidades.
- Dependencias externas con dueño, hito, fallback y efecto.
- Subdocumento 4 no contiene notas internas ni evidencia futura presentada como ejecutada.

### Veredicto permitido

- `APTO PARA INFORME 1`.
- `APTO CON DEPENDENCIAS EXTERNAS TRATADAS`.
- `NO APTO PARA INFORME 1`.

### Salidas de D3

- D3 ejecutado sobre una versión/commit exactos.
- `TRZ_D3.md` completado con evidencia real.
- Acta corta de brechas residuales.

### Trabajo de producción

1. Redactar `00_BASE_TECNICA_SUBDOCUMENTO_4.md` desde el mapa D3.
2. Incorporar únicamente los diagramas definitivos que el equipo prepare y apruebe; los bocetos archivados no forman parte del entregable.
3. Cruzar `V-DATA-01` con Subdocumento 5.
4. Incorporar el T-11 final.
5. Ejecutar D3 y aplicar sus correcciones.
6. Verificar referencias, numeración, tablas y legibilidad.
7. Al exportar a Word/PDF, revisar visualmente todas las páginas.

### Barridos mínimos

```sh
rg -n "POR COMPLETAR|POR DEFINIR|PENDIENTE DE INTEGRAR|FALTA DIAGRAMA|recordar que|debe definir|debe entregar" Celula3/90_Consolidado
rg -n -i "CLP|USD|UF|precio|tarifa|costo unitario|monto total" Celula3/90_Consolidado
git diff --check
```

Revisar manualmente cada coincidencia; una palabra como “pendiente” puede ser legítima si describe una dependencia externa tratada.

### Definición de terminado

- Cada sección exigida responde a T-7/T-21/T-22.
- Cada figura es legible y propia del Caso 06.
- Cada fila T-11 es verificable.
- Cada estándar invocado tiene control y evidencia.
- No hay precio ni monto económico.
- D3 emite un veredicto apto.

## 7. Puertas y autorización de avance

| Puerta | Momento | El agente debe entregar | No debe hacer todavía |
|---|---|---|---|
| `P1` | después de MA-2 | audit final y hallazgos priorizados | corregir o decidir ADR |
| `P2` | después de MA-4 | tabla ADR y baseline propuesta | completar T-11 definitivo |
| `P3` | después de MA-5 | T-11 de trabajo y formulario final | diagramar |
| `P4` | después de MA-7 | índice y tablas; figuras como recomendación no vinculante | HABILITA REDACCIÓN; diagramas quedan a decisión del equipo |
| `P5` | después de ejecutar D3 | veredicto sobre consolidado real | declarar entrega cerrada si no es apta |

## 8. Política de brechas y dependencias

Una dependencia externa se considera tratada solo si tiene:

1. dato o decisión faltante;
2. dueño externo;
3. fecha/hito o condición de obtención;
4. diseño conservador mientras falta;
5. efecto sobre arquitectura, cantidad y T-11;
6. prueba o evidencia de cierre futura.

No son dependencias externas:

- discrepancias A1↔C1;
- estados ADR desincronizados;
- una fila T-11 que otro frente ya puede completar;
- referencias vagas entre documentos existentes;
- una decisión técnica que TERABYTE debe tomar como proponente.

## 9. Límites contra sobreingeniería

- No borrar el trabajo avanzado: clasificarlo como evidencia interna o futura.
- No publicar el registro completo de amenazas en I1.
- No convertir cada selección tecnológica en ADR.
- No especificar cada biblioteca, puerto interno o detalle de implementación.
- No producir diagramas sin una pregunta arquitectónica clara.
- No repetir el modelo de datos que pertenece al Subdocumento 5.
- No fijar precios, proveedores contractuales o modelos finales sin evidencia.
- No exigir pruebas de operación antes de la etapa en que corresponden.
- Sí definir tecnología, ubicación, cantidad técnica y justificación suficiente para que la arquitectura sea evaluable.

## 10. Formato de reporte al usuario por bloque

Al cerrar cada bloque, informar brevemente:

1. qué se revisó;
2. qué se agregó o corrigió;
3. hallazgos críticos;
4. qué quedó condicionado y por quién;
5. verificaciones realizadas;
6. siguiente bloque y si requiere aprobación.

## 11. Prompt corto de continuidad para otro agente

```text
Trabaja en /Users/rev/Documents/FEP2 y lee completo
Celula3/00_Gobierno/07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md.
Continúa únicamente con el siguiente bloque MA-* pendiente. Usa main actualizado como
línea base, preserva archivos ajenos y no dibujes antes de MA-5/P3. Contrasta los PDF
oficiales directamente; Bases_caso solo ayuda a navegar. Mantén separado EXIGIBLE I1,
BASELINE I1, CONDICIONADO EXTERNO, EVIDENCIA FUTURA y FUERA DE I1. Al terminar aplica
el DoD del bloque, reporta archivos modificados y detente en cualquier puerta PAUSA.
```

## 12. Plan operativo restante

MA-0–MA-8 y P1–P4 están cerrados. La continuación ya no consiste en abrir nuevos bloques de investigación, sino en producir y controlar el entregable:

| Paso | Acción | Salida verificable | Condición de cierre |
|---|---|---|---|
| `R1` | redactar conjuntamente las trece subsecciones desde el mapa D3 | `90_Consolidado/00_BASE_TECNICA_SUBDOCUMENTO_4.md` autónomo y en lenguaje natural | **HABILITADO**; base técnica preparada, redacción final pendiente |
| `R2` | cruzar `V-DATA-01` con Subdocumento 5 | tabla de diez dominios coherente en autoridad, almacén, protección y retención | **COMPLETADO** |
| `R3` | preparar los diagramas que el equipo defina | figuras legibles, propias del Caso 06 y aprobadas por el equipo | **PENDIENTE**; bocetos previos archivados y excluidos |
| `R4` | ensamblar texto, tablas, diagramas aprobados y T-11 | versión completa del Subdocumento 4 | T-11 conserva 32 filas, cinco columnas y cero precios |
| `R5` | ejecutar D3 y completar `TRZ_D3.md` | trece controles con evidencia, hallazgos y veredicto P5 | ninguna contradicción crítica/alta abierta; dependencias externas tratadas |
| `R6` | corregir, congelar y verificar visualmente | versión final maquetada | referencias, numeración y páginas revisadas; veredicto apto |

`R1` y la preparación visual de `R3` pueden avanzar en paralelo dentro del equipo, pero `R5` solo se ejecuta sobre una versión ensamblada exacta. El punto único de entrada y las reglas para continuar están en [`Celula3/README.md`](../README.md).
