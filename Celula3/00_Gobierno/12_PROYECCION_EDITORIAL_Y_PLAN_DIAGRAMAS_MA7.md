# Proyección editorial y plan de diagramas — MA-7

**Fecha:** 2026-09-06
**Estado:** `MA-7 COMPLETADA COMO PROPUESTA EDITORIAL — ESTRUCTURA VIGENTE; PLAN VISUAL NO VINCULANTE`
**Alcance:** propuesta histórica de estructura y posibles figuras para el Subdocumento 4 del Informe 1; no constituye redacción final ni obliga al equipo a utilizar ese conjunto visual.

## 1. Decisión editorial

El Subdocumento 4 será una **síntesis autónoma** de A1–D2, no la unión literal de sus matrices. Debe poder leerse sin abrir el expediente, pero cada afirmación crítica conservará una referencia estable hacia su evidencia.

La estructura sigue exactamente las dos partes evaluadas por T-21:

1. `4.1 Arquitectura lógica`: a) esquema de solución y b) arquitectura lógica.
2. `4.2 Arquitectura física`: a) arquitectura física, b) tecnologías de software, c) implementos, d) data center primario, e) data center secundario y Formulario T-11.

Dentro de esas dos partes se cubren los ocho puntos de T-7: lógica, físico/Art. 16, integración, seguridad, despliegue, capacidad, ADR y especificidad del Caso 06. No se crean capítulos 4.3–4.5 que puedan parecer subdocumentos distintos de la pauta oficial.

## 2. Fuentes de forma verificadas

| Fuente oficial | Regla que gobierna MA-7 |
|---|---|
| FEP01 Formulario T-7, PDF 58 | ocho materias obligatorias del Subdocumento 4 y prohibición de diagramas genéricos |
| FEP01 Formulario T-21, PDF 67 | separación formal 4.1/4.2, 16 % cada una, y T-11 dentro de 4.2 |
| FEP01 Formulario T-22, PDF 69 | Informe 1 exige detalle suficiente para comprender cada módulo/capa, solución propia y carácter híbrido |
| FEP02 `RT-02.01`/`.03`, PDF 7–8 | diagrama lógico de ocho capas y vistas lógica, proceso, despliegue, datos y seguridad conforme a ISO/IEC/IEEE 42010 |

## 3. Extensión objetivo

| Parte | Extensión orientativa | Contenido dominante |
|---|---:|---|
| apertura y regla de lectura | 0,5–1 página | propósito, baseline I1 y leyenda de estados |
| 4.1 arquitectura lógica | 7–8 páginas | F1–F3, catálogo ejecutivo, datos/seguridad y ADR |
| 4.2 arquitectura física | 9–11 páginas | F4–F5, Art. 16, tecnologías, sala, DR, continuidad y capacidad |
| Formulario T-11 | 4–5 páginas | 32 filas, cinco columnas, sin precios |
| **total orientativo** | **20–25 páginas** | cobertura completa sin trasladar el expediente |

La extensión no es un máximo contractual. Si la plantilla hace ilegible T-11 o una figura, se agrega página antes de reducir tipografía.

## 4. Índice propuesto y contrato de cada sección

| Sección | Pregunta que responde | Contenido mínimo | Fuente canónica | Recurso visual | Objetivo |
|---|---|---|---|---|---|
| apertura | ¿qué solución y qué estado se presenta? | propósito, Caso 06, baseline de Informe 1, límites de evidencia | Maestro, MA-6 | leyenda breve | 0,5–1 pág. |
| `4.1.1 Esquema de solución` | ¿quién interactúa, qué conserva el CLIENTE y cuál es el límite TERABYTE? | actores agrupados, canales, plataforma, TOS/ERP/VMS/periferia/autoridades y exclusiones | A1 §§1/1.4/1.5 | **F1** | 1–1,5 págs. |
| `4.1.2 Arquitectura lógica` | ¿qué responsabilidades existen y cómo se relacionan? | ocho capas, 24 componentes agrupados, límites de contexto, criticidad e interfaces; estilo modular híbrido | A1 §§2–6; ADR-001/002 | **F2** + tabla lógica ejecutiva | 2 págs. |
| `4.1.3 Integración y procesos críticos` | ¿cómo circulan comandos/eventos y cómo convive la solución con TOS 2012? | contratos, INT-HUB/TOS, autoridad dominio×zona×fase, idempotencia, DLQ, fallback, 72 h y reconciliación ≤90 min | A2 §§1–7; A3 §§2–10; ADR-003/004 | **F3** + tabla de familias | 2 págs. |
| `4.1.4 Datos y seguridad transversales` | ¿qué datos sostienen el proceso y cómo se protegen? | almacenes/autoridad/retención a nivel arquitectónico; Zero Trust, IAM local, cifrado, logs/SIEM y confianza | A1 modelo; D1 B1–B7; Subdoc. 5 | **V-DATA-01** + **F5** | 1,5–2 págs. |
| `4.1.5 Decisiones y cumplimiento` | ¿por qué se eligió esta baseline y cómo se acredita? | resumen de 11 ADR, consecuencias/condiciones, Art. 4 por familias y dependencias legítimas | Registro ADR; MA-4/MA-6 | tabla ADR ejecutiva | 1 pág. |
| `4.2.1 Arquitectura física y emplazamiento` | ¿dónde vive cada grupo y por qué es híbrido? | sala, edge, redes, AWS primaria/secundaria, sistemas conservados y justificación por seis criterios del Art. 16 | C1 §§4–7; ADR-005/006/011 | **F4** + tabla Art. 16 | 2 págs. |
| `4.2.2 Tecnologías de software` | ¿con qué se materializa la solución y cómo se evita obsolescencia/lock-in? | React, Spring Boot, React Native, contratos, AWS/EKS/RDS/S3/EventBridge/SQS, OpenTelemetry, IaC, Linux; alternativa y vigencia | C2 §§3–4; MA-5 | tabla tecnológica compacta | 1–1,5 págs. |
| `4.2.3 Implementos de hardware y software` | ¿qué se especifica/provee? | familias, cantidades, redundancia, interfaces y ambiente; referencia hacia T-11 | C2 §§7–9; C4 §§6/9; D1 `SEC-PHYS` | tabla resumen, no repetir 32 filas | 1 pág. |
| `4.2.4 Data center primario` | ¿cómo sostiene 72 h en ambiente portuario? | sala condicional de 34 m², tres puertas, racks, cómputo, RAID, red, UPS, generación, climatización, incendio, acceso, CCTV y PUE | C2 §5; C4 §6.2.bis; ADR-005/007 | bloque ampliado dentro de F4 + tabla sala | 1,5 pág. |
| `4.2.5 Data center secundario y DR` | ¿dónde recupera y contra qué fallas comunes? | AWS `us-east-1`, activo-pasivo, réplica, IaC, copia inmutable, RTO/RPO, failover/failback y dominio común AWS | C2 §6; C3 §9; ADR-007/011; SPOF-22 | bloque ampliado dentro de F4 | 1 pág. |
| `4.2.6 Despliegue, redes y continuidad` | ¿cómo se despliega y opera ante cortes/fallas? | ambientes, CI/CD, segregación, doble WAN/VPN, patio LTE/5G, operación 72 h, sombra 8 h, respaldos 3-2-1-1-0 y pruebas futuras | C3 §§3–10; D1 B3; A3 §7 | F3/F5; **F6 solo si se activa** | 2 págs. |
| `4.2.7 Dimensionamiento y capacidad` | ¿por qué alcanzan cantidades y enlaces? | normal/peak, crecimiento, telemetría, 183 GB local, 21,9 GB buffer, 32,5/35 Mbps, carga/PUE y disparadores | C4 §§3–8 | tabla de resultados/supuestos | 1–1,5 págs. |
| `4.2.8 Formulario T-11` | ¿qué se oferta/especifica, dónde, cuánto y por qué? | tabla oficial de 32 filas; nota de supuestos/validaciones y cero precios | MA-5; `02_FORMULARIO_T11_FINAL.md` | formulario contractual | 4–5 págs. |

## 5. Plan mínimo de diagramas

### 5.1 Set de referencia propuesto — cinco posibles figuras

| Figura | Tipo/vista | Pregunta única | Contenido sugerido | Qué se excluye para evitar saturación | Criterio de aceptación |
|---|---|---|---|---|---|
| `F1` — Esquema de solución | contexto | ¿quién usa la solución y cuál es su frontera? | personas internas/externas agrupadas; canales; límite TERABYTE; TOS, ERP, VMS, grúas, básculas/OCR, navieras y autoridades | nodos AWS, puertos, réplicas, productos y cada uno de los 21 terceros | se distingue problema/alcance de arquitectura; sistemas conservados quedan fuera de TERABYTE |
| `F2` — Arquitectura lógica de ocho capas | vista lógica | ¿qué módulos/capas existen y qué responsabilidad tiene cada uno? | ocho capas exactas; `CH-*`, `GW-*`, `CTX-*`, `SRV-*`, `INT-*`, `DATA-*`; seguridad/observabilidad transversales; dependencias principales | marcas, regiones, cantidades, amenazas individuales y flecha por cada evento | las ocho capas son visibles, UI no toca BD y los límites de contexto se entienden a tamaño página |
| `F3` — Integración y proceso crítico | vista de procesos | ¿cómo avanza una operación y qué cambia al caer el enlace o convivir con TOS? | canal→gateway→contexto→INT-HUB/TOS/datos; comando/evento; autoridad por fase; cola/DLQ; operación local y reconciliación | 21 contrapartes dibujadas una por una y los cinco procesos en cinco figuras | una sola leyenda explica síncrono/asíncrono, autoridad, corte 72 h y retorno ≤90 min |
| `F4` — Arquitectura física híbrida | vista de despliegue | ¿dónde corre cada componente y cómo se recupera? | terminal: sala/edge/red; AWS `sa-east-1` ≥2 AZ; AWS `us-east-1` DR; doble WAN/VPN; servicios gestionados; sistemas conservados; límites de fallo | especificación completa de cada servidor, marcas decorativas y todos los controles D1 | evidencia Art. 16, primario/secundario, 72 h local y RTO/RPO sin confundir segundo rack con segundo sitio |
| `F5` — Seguridad y límites de confianza | vista de seguridad | ¿qué zonas pueden comunicarse y mediante qué controles? | `Z-EXT/EDGE/SVC/DATA/LOCAL/FIELD/ADM/PROT/MGMT`; conductos principales; WAF/API/IAM/PAM/cifrado/log/SIEM; ruta local crítica | 31 controles, 73 amenazas y 26 SPOF como cajas separadas | no existe confianza por ubicación, administración está mediada y protección/operación permanecen segregadas |

Estas cinco figuras fueron una recomendación de MA-7. Sus bocetos posteriores se archivaron como referencia y no forman parte de la entrega. El equipo decide qué diagramas definitivos utilizar y evita vistas innecesariamente saturadas.

### 5.2 Vista de datos sin sexto diagrama

`RT-02.03` exige una vista de datos, pero el Subdocumento 5 es dueño del modelo detallado. Para evitar duplicidad, el Subdocumento 4 usará una tabla compacta `V-DATA-01`:

| Dominio C4 | Fuente de verdad normal | Autoridad durante corte | Capacidad lógica | Protección | Retención/respaldo | Dueño del detalle |
|---|---|---|---|---|---|---|
| `DOM-OPS` · contenedor y operación | AWS consolidado; contexto de operaciones | núcleo local para operaciones críticas | `DATA-CORE` | IAM, cifrado según catálogo y auditoría | movimiento/operación: 10 años | Subdoc. 5 |
| `DOM-PAT` · patio y posición | solución, contrastada con instrumentación | núcleo local por zona y fase | `DATA-CORE` | segregación por rol, integridad y evidencia de fuente | según entidad operacional | Subdoc. 5 |
| `DOM-GAT` · gate y transporte | solución e interfaces validadas | núcleo local para ingreso/egreso | `DATA-CORE` + evidencia en `DATA-DOC` | cifrado personal, trazabilidad y mínimo privilegio | según clase personal/operacional | Subdoc. 5 |
| `DOM-REF` · reefer y cadena de frío | instrumentación validada | local para alarma y serie crítica | `DATA-TS`; evidencia en `DATA-DOC` | segregación, integridad y custodia | 5 años reefer; granular según catálogo | Subdoc. 5 |
| `DOM-NAV` · nave y planificación | solución y mensajes validados de naviera/TOS | estado crítico local; intercambio exterior en cola | `DATA-CORE` + objetos en `DATA-DOC` | cifrado comercial, versionado e integridad | según clase operacional/documental | Subdoc. 5 |
| `DOM-INS` · inspecciones | solución y acto de autoridad | flujo local cuando la función sea crítica | `DATA-CORE` + actas en `DATA-DOC` | firma, hash, cifrado y custodia | según clase de acta/evidencia | Subdoc. 5 |
| `DOM-FAC` · evidencia y facturación | solución para hecho/evidencia; ERP para asiento final | registro local del hecho facturable | `DATA-CORE` + `DATA-DOC` | inmutabilidad, cifrado comercial y trazabilidad | según clase comercial/evidencia | Subdoc. 5 |
| `DOM-ACC` · acceso e identidad | IAM y sistemas conservados según dato | identidad mínima y bitácora local para continuidad | `DATA-CORE`; auditoría en `DATA-DOC` | mínimo privilegio, cifrado personal y registro de acceso | según clase personal/auditoría | Subdoc. 5 |
| `DOM-EMI` · energía y emisiones | derivados trazables de operación/telemetría | captura local; cálculo consolidado diferible | `DATA-AN`, con origen en `DATA-CORE`/`DATA-TS` | acceso por rol, linaje y fórmula versionada | hereda fuente y política de reporte | Subdoc. 5 |
| `DOM-INT` · integración, autoridad y auditoría | `INT-HUB` y contratos versionados | colas locales, idempotencia y bitácora | metadatos en `DATA-CORE`; mensajes/evidencia en `DATA-DOC` | autenticación mutua, integridad, DLQ y auditoría | hereda la clase transportada | Subdoc. 5 |

Esta tabla constituye la **vista de datos arquitectónica**: muestra autoridad, movimiento, almacén y protección sin copiar entidades, atributos ni diccionario.

### 5.3 Figura condicional

`F6 — Continuidad 72 h, retorno y DR` se activa únicamente si F3/F4 no pueden mostrar de forma legible tres estados:

1. operación normal híbrida;
2. enlace exterior caído durante hasta 72 h;
3. reconexión/reconciliación ≤90 min o desastre regional con RTO ≤4 h/RPO ≤15 min.

Si se activa, será una línea temporal de una página o media página; no repetirá nodos, productos ni redes. **No se aprueba por defecto**: primero se intenta resolver continuidad mediante F3 y F4.

## 6. Cobertura de las cinco vistas ISO/IEC/IEEE 42010

| Vista exigida | Evidencia prevista | Estado MA-7 |
|---|---|---|
| lógica | F2 + catálogo ejecutivo | DISEÑADA, por dibujar |
| procesos | F3 + tabla de familias de integración | DISEÑADA, por dibujar |
| despliegue | F4 + tabla Art. 16 | DISEÑADA, por dibujar |
| datos | `V-DATA-01` + enlace al Subdoc. 5 | DISEÑADA como tabla, sin duplicidad |
| seguridad | F5 + síntesis de controles | DISEÑADA, por dibujar |

F1 es adicional porque T-21 exige expresamente el esquema de solución y T-22 dice que no se confunda con la arquitectura.

## 7. Tablas que sí se publican

| Tabla | Contenido | Regla de síntesis |
|---|---|---|
| `T-SD4-01` | componentes lógicos agrupados por capa | 24 filas como máximo; una frase por responsabilidad |
| `T-SD4-02` | familias de integración | agrupar 21 contrapartes en 7 familias; nombrar las críticas |
| `V-DATA-01` | vista arquitectónica de datos | 10 dominios C4 mapeados a 4 capacidades C3; detalle en Subdoc. 5 |
| `T-SD4-03` | emplazamiento Art. 16 | agrupar por nodo/familia con seis criterios, no repetir T-11 |
| `T-SD4-04` | tecnologías de software | selección, alternativa, modalidad, ubicación y vigencia |
| `T-SD4-05` | sala primaria y sitio secundario | cantidades/capacidad y condición/fallback |
| `T-SD4-06` | capacidad | publicar resultados, fórmula decisiva y supuesto; cálculos completos quedan en C4 |
| `T-SD4-07` | ADR ejecutivo | 11 decisiones en una línea cada una; alternativas/consecuencias resumidas |
| `T-SD4-08` | dependencias externas | dato, dueño, hito, baseline, fallback y efecto |
| Formulario T-11 | 32 filas oficiales | se incorpora sin reescribir ni agregar precios |

No se publican completas las matrices de 73 amenazas, 26 SPOF, 31 controles, 374 RT ni 53 filas normativas. Se sintetizan y se conserva la traza interna.

## 8. Reglas visuales para B8

1. Cada figura debe tener título, propósito, leyenda y una frase de lectura.
2. Usar los IDs canónicos; el nombre legible puede acompañarlos, nunca sustituirlos.
3. Distinguir visualmente `TERABYTE`, `CLIENTE`, terceros y AWS.
4. Usar el mismo color/forma para una entidad en todas las figuras.
5. No usar logos como sustituto de componentes; las marcas pertenecen a 4.2.2/T-11.
6. Toda flecha debe tener dirección y semántica: comando, evento, sincronización o administración.
7. Mantener legibilidad al exportar a página A4/carta; no depender del zoom.
8. Las dependencias externas y evidencias futuras no se dibujan como implementadas.
9. Una figura responde una pregunta. Si requiere más de una leyenda extensa, se simplifica.
10. Todo diagrama que el equipo decida incluir debe coincidir con AWS `sa-east-1`/`us-east-1`, 72 h, 8 h, ≤90 min, RTO/RPO, catálogos y T-11 vigentes.

## 9. Contenido que se reserva para otras entregas

- matrices completas de riesgo de solución, desarrollo e implantación: Informe 2;
- EDT, hitos, equipo y planificación detallada: Informe 2;
- proveedores/adquisiciones contractuales, precios, costos y flujo de caja: Informe 3;
- pruebas ejecutadas, certificaciones obtenidas, actas y métricas operativas: evidencia futura;
- catálogo detallado de entidades/campos/linaje: Subdocumento 5.

La selección AWS, las familias de referencia y las cantidades del T-11 sí permanecen en Informe 1 porque hacen evaluable la arquitectura; no se presentan como contrato adjudicado ni compra ejecutada.

## 10. Puerta P4

MA-7 deja preparada para aprobación:

- la estructura 4.1/4.2;
- el presupuesto de extensión;
- una propuesta no vinculante de cinco figuras;
- la vista de datos como tabla;
- la posibilidad de una vista adicional solo si el equipo la considera necesaria;
- las tablas publicables y el contenido que no se trasladará.

Después de estabilizar la estructura, MA-8 ajusta la secuencia de producción y control:

1. redactar el consolidado en lenguaje natural y preparar únicamente los diagramas que decida el equipo;
2. cruzar `V-DATA-01`, ensamblar T-11 y los diagramas aprobados;
3. ejecutar D3 sobre la versión real, corregir y maquetar.

No se dibuja ni se redacta la versión final dentro de MA-7.
