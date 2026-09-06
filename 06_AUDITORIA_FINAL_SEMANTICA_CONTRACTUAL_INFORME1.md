# Auditoría final semántica y contractual — Informe 1 / Subdocumento 4

**Fecha del corte:** 2026-09-06

**Rama y commit auditados:** `main` · `4bd141b`

**Bloques ejecutados:** `MA-0`, `MA-1` y `MA-2`

**Estado del corte auditado:** `P1 — AUDITORÍA TERMINADA`

**Estado vigente:** `MA-8 COMPLETADA COMO PREPARACIÓN; PRODUCCIÓN FINAL Y EJECUCIÓN D3 PENDIENTES`

**Objeto:** determinar si los insumos A1–D2 forman una arquitectura única, trazable y publicable para el Informe 1, antes de completar T-11, diagramar y ejecutar D3.

> **Documento histórico de diagnóstico.** El veredicto “NO PUBLICABLE” que sigue corresponde al commit `4bd141b`, antes de las correcciones MA-3–MA-8; no describe el estado operativo actual. El corte vigente deja 11 ADR `PROPUESTO`, 0 `APROBADO`, T-11 con 32 filas y trece secciones finales trazadas a fuentes, recursos y controles D3. La continuación oficial está en [`Celula3/README.md`](Celula3/README.md): redacción total, F1–F5, cruce de datos, ensamblado y ejecución D3.

## 0. Veredicto ejecutivo

**Veredicto:** `NO PUBLICABLE TODAVÍA; APTO PARA CORRECCIÓN QUIRÚRGICA`.

No hace falta rehacer los frentes. La mayor parte del diseño existe y está bien fundada. Sin embargo, todavía no conviene diagramar ni redactar el Subdocumento 4 final porque hay una contradicción crítica en la operación local de 72 horas, varias declaraciones históricas que ya no representan la solución vigente y vacíos concretos para completar las cinco columnas oficiales del T-11.

La situación, en simple, es esta:

1. **La arquitectura lógica, física, de integración, seguridad y capacidad ya tiene contenido suficiente.**
2. **La arquitectura todavía no cuenta una única historia en todos los archivos.** Algunas correcciones aplicadas en A1/C1/C2/C4 no fueron propagadas a D1, D2, trazas, ADR y complementos.
3. **La ruta local está incompleta.** Los canales deben pasar por `GW-API`, pero C1 lo deja solamente en nube mientras afirma que las funciones críticas siguen disponibles localmente durante 72 horas.
4. **T-11 aún no es un formulario ofertable.** Hay candidatos bien trazados, pero faltan productos o servicios de referencia seleccionados, varias cantidades físicas y el volcado a los archivos finales.
5. **Los diagramas pueden seguir diferidos**, pero solo hasta cerrar los hallazgos críticos y altos de este documento.

### Resultado cuantitativo

| Clase | Cantidad | Tratamiento |
|---|---:|---|
| Crítico | 1 | corregir antes de congelar catálogos o dibujar |
| Alto | 8 | corregir o convertir en condición explícita antes de T-11/D3 |
| Medio | 6 | saneamiento semántico y de trazabilidad |
| Bloqueante planificado | 2 | trabajo esperado de MA-5/MA-7, no defecto de los autores |
| Editorial / alcance | 1 | reducir para Informe 1 sin borrar la evidencia fuente |

## 1. Línea base, fuentes y regla de lectura

### 1.1 Fuentes oficiales contrastadas

| Fuente | Materia usada en esta auditoría |
|---|---|
| `FEP00.1.26 — Pautas del Curso` | alcance del Informe 1: empresa, problema, esquema/alcance, arquitectura lógica y física e innovaciones |
| `FEP01.26 — Bases Administrativas` | Art. 4, orden de precedencia, Art. 14, modelo híbrido del Art. 16, Formulario T-7, T-11, T-21 y T-22 |
| `FEP02.26 — Bases Técnicas Transversales` | ocho capas, arquitectura híbrida, integración, seguridad, sala/sitio secundario, despliegue, capacidad, continuidad, estándares y evidencia |
| `FEP03.06.26 — Caso 06 Portuaria` | operación portuaria, sistemas actuales, 72 h, sincronización ≤90 min, ambiente marino, TOS, gate, patio, reefer, naves, volumetría y restricciones del caso |

Las copias Markdown de `Bases_caso/` se usaron solo como índice de navegación. Ante cualquier diferencia, mandan los PDF oficiales y sus aclaraciones formales.

### 1.2 Jerarquía y criterio

- Las Bases Administrativas y sus anexos gobiernan la forma, admisibilidad y obligaciones contractuales.
- Las bases técnicas del caso y las transversales se leen acumulativamente: el caso especializa o endurece el piso transversal, no lo borra en silencio.
- Una decisión interna, supuesto, catálogo o ADR no reemplaza una fuente oficial.
- Una referencia cruzada demuestra origen, pero no sustituye la decisión que debe leerse en el documento final.
- `PROPUESTO`, `CANDIDATO`, `APROBADO`, control diseñado, prueba prevista y evidencia ejecutada son estados diferentes.

### 1.3 Archivos de arquitectura revisados

- Gobierno: Maestro, Plan, Matriz Global, Registro ADR y complemento tecnológico.
- Frente 1: A1, A2, A3 y sus trazas.
- Frente 2: C1, C2, C3, C4 y sus trazas.
- Frente 3: D1, D2 y sus trazas.
- Salidas: D3, Subdocumento 4 consolidado, T-11 de trabajo, T-11 final y checklist.
- Auditorías anteriores: auditoría global previa y consolidado de auditorías/cambios.

## 2. Alcance correcto para el Informe 1

El Informe 1 sí exige una arquitectura defendible y específica, pero no exige fingir que ya se construyó, probó u operó la solución.

| Clasificación | Qué entra ahora | Cómo se redacta |
|---|---|---|
| `EXIGIBLE I1` | 4.1 lógica, 4.2 física, T-11, carácter híbrido, capas, módulos, interfaces, emplazamiento, tecnologías, implementos, sala primaria/secundaria, capacidad, ADR y SPOF | decisión o línea base concreta, trazada y entendible |
| `BASELINE I1` | productos o familias de referencia, cantidades calculables, proveedor/región propuestos bajo condición, controles y pruebas de aceptación previstas | propuesta defendible; no se presenta como implementada |
| `CONDICIONADO EXTERNO` | site survey, contratos reales, capacidad de enlaces, tamaño real de imágenes, AHT, directorio, autorizaciones y datos de mercado | rango/fallback, responsable, hito y efecto si no se confirma |
| `EVIDENCIA FUTURA` | pentest, restauraciones, pruebas 72 h, conmutación DR, carga, hardening ejecutado, certificaciones operativas | criterio de prueba y evidencia esperada, nunca “cumple” |
| `FUERA DE I1` | riesgos completos de desarrollo/implantación, EDT detallada, costos, VAN/TIR, proveedores contractualmente cerrados y prototipo final | conservar como insumo, resumir o derivar a Informes 2/3 |

### 2.1 Qué no debe exigirse artificialmente a los ADR

Para Informe 1 no es necesario que los once ADR estén `APROBADO`. Sí es necesario que:

- los estados sean iguales en todos los documentos;
- una línea base usada por el diagrama o el T-11 esté seleccionada o formalmente condicionada;
- un `CANDIDATO` no se redacte en otro archivo como si ya fuese decisión firme;
- ningún ADR dependa de una contradicción interna que el equipo sí puede resolver;
- las aprobaciones o aceptaciones que corresponden al CLIENTE se mantengan pendientes con dueño y condición.

## 3. Cobertura contractual comprobada

| Exigencia oficial relevante | Evidencia disponible | Estado de auditoría |
|---|---|---|
| Arquitectura lógica distinta del esquema de solución | A1 separa contexto, ocho capas, catálogo, interfaces y dominio | `CUBIERTO EN BORRADOR` |
| Capas, módulos, límites, responsabilidades e interfaces | A1 registra 24 componentes; A2/A3 detallan integración y procesos | `CUBIERTO`, sujeto a AFI1-001/011 |
| Arquitectura propia del Caso 06 | TOS 2012, gate, patio, reefer, nave, 72 h, 90 min, 2029 y ambiente marino | `CUBIERTO` |
| Arquitectura física híbrida y justificación por componente | C1 declara nube, sala y bordes con criterios del Art. 16 | `CUBIERTO CON BRECHAS` AFI1-001/004/009/016 |
| Tecnologías de software | C2 declara frontend, backend, APIs, app, datos, mensajería, contenedores, IaC y observabilidad | `CUBIERTO COMO REFERENCIA`, falta AFI1-004/012 |
| Implementos HW/SW | C2 y C4 publican candidatos y cantidades parciales | `INCOMPLETO PARA T-11` AFI1-003/005 |
| Data center primario | C2 recorre materias de sala principal | `ESPECIFICADO, NO DIMENSIONADO` AFI1-003 |
| Data center secundario/DR | C2/C3 fijan activo-pasivo, RTO/RPO y pruebas | `CONDICIONADO` a AFI1-004/010 |
| Despliegue, redes, HA, DR y respaldos | C3 desarrolla ambientes, red, continuidad, pruebas y retorno | `CUBIERTO EN DISEÑO` |
| Capacidad con volumen, concurrencia y crecimiento | C4 recalcula normal, peak, estacionalidad, 72 h, 90 min y holgura | `CUBIERTO CON VACÍOS FÍSICOS` AFI1-003/009 |
| Seguridad y Zero Trust | D1 define 31 controles; D2 modela 73 amenazas | `CUBIERTO EN DISEÑO`, no implementado |
| ADR con alternativas y consecuencias | 11 ADR registrados; estados mixtos | `PARCIAL` AFI1-010 |
| SPOF explícitos | C1 y D2 contienen registros | `NO CONSOLIDADO` AFI1-007 |
| Trazabilidad estándar → control → evidencia | matriz STD y controles parciales | `PARCIAL` AFI1-008 |
| T-11 de cinco columnas | plantilla correcta, contenido vacío | `BLOQUEANTE PLANIFICADO` AFI1-002 |
| Diagramas propios y coherentes | A1/A3 contienen diagramas lógicos; las vistas finales físicas/seguridad están diferidas | `BLOQUEANTE PLANIFICADO` AFI1-018 |

### 3.1 Matriz contractual mínima de MA-1

| ID | Fuente oficial | Materia exigida | Aplicabilidad I1 | Evidencia actual | Estado / brecha | Corrección y dueño |
|---|---|---|---|---|---|---|
| `CTR-I1-01` | FEP01, Form. T-7, Subdoc. 4 | capas, módulos, contextos, responsabilidades e interfaces | directa | A1, A2 y A3 | cubierta; ruta local inconsistente | `AFI1-001`, A1/C1/C3/D1 |
| `CTR-I1-02` | FEP01, Form. T-7, Subdoc. 4 | emplazamiento nube/on-premise por componente y Art. 16 | directa | C1 §4/§5 | parcial: ubicación cloud y ruta local sin cierre | `AFI1-001/004/016`, C1/C2 |
| `CTR-I1-03` | FEP01, Form. T-7, Subdoc. 4 | servicios, contratos, mensajería, versionado y gobierno | directa | A2 | cubierta con contradicción de fuente del contrato | `AFI1-012`, A2/C2 |
| `CTR-I1-04` | FEP01, Form. T-7, Subdoc. 4 | Zero Trust, exposición, identidad, cifrado y controles | directa | D1/D2 | cubierta como diseño, no implementación | integrar síntesis y evidencia prevista, D3 |
| `CTR-I1-05` | FEP01, Form. T-7, Subdoc. 4 | ambientes, redes, HA, DR y respaldos | directa | C2/C3 | patrón cubierto; ubicación cloud condicionada | `AFI1-004/010/016`, C2/C3 |
| `CTR-I1-06` | FEP01, Form. T-7, Subdoc. 4 | volumen, concurrencia, crecimiento y capacidad | directa | C4 | cálculo lógico cubierto; sala sin dimensionar | `AFI1-003/009`, C2/C4 |
| `CTR-I1-07` | FEP01, Form. T-7, Subdoc. 4 | decisiones con alternativas y criterio | directa | Registro ADR, A1/A3/C1/C2/D1/D2 | 11 registradas, estados desincronizados | `AFI1-010`, integrador/autores |
| `CTR-I1-08` | FEP01, Form. T-7 y T-22 | arquitectura propia; no diagramas genéricos | directa | contenido específico del puerto en A1–D2 | fuentes finales incompletas | `AFI1-018`, B8/D3 |
| `CTR-I1-09` | FEP01 Art. 16 | solución híbrida y justificación por latencia, criticidad, volumen, regulación/seguridad, conectividad/acoplamiento y TCO | directa | C1 §4 | seis criterios presentes; baseline cloud pendiente | `AFI1-004/016`, C1/C2 |
| `CTR-I1-10` | FEP01, Form. T-11 | componente, producto/servicio, ubicación, cantidad y justificación | directa | candidatos C2/C3/C4/D1 y plantilla final | contenido final vacío; productos/cantidades parciales | `AFI1-002/003/004/005`, MA-5 |
| `CTR-I1-11` | FEP01 Art. 4.3 | estándar → control implementado → entregable/evidencia | transversal | Matriz Global §4 y controles A–D | matriz todavía general y con aplicabilidad abierta | `AFI1-008`, gobierno/D3 |
| `CTR-I1-12` | FEP02 Cap. 2 | ocho capas, cinco vistas, ADR y SPOF | directa | A1, C1, D1/D2 | capas cubiertas; vistas/SPOF pendientes | `AFI1-007/018`, D2/B8/D3 |
| `CTR-I1-13` | FEP02 Cap. 3–10 | híbrido, sala/sitio DR, despliegue, equipos, capacidad, operación/continuidad | directa | C1–C4 | contenido amplio; cálculo físico incompleto | `AFI1-003/004/009`, C2/C4 |
| `CTR-I1-14` | FEP02 Cap. 11–13 | seguridad, identidad y accesibilidad | directa | D1/D2, A1/C2 | diseño cubierto; productos/pruebas/EN 301 549 pendientes | `AFI1-004/008`, D1/C2/D3 |
| `CTR-I1-15` | FEP03 Caso 06 | TOS, gate, patio, reefer, naves, 72 h, 90 min, ambiente marino y volumetría | directa | A1–D2 | especificidad alta; ruta local no cerrada | `AFI1-001`, autores cruzados |
| `CTR-I1-16` | FEP00 lámina 16 + FEP01 T-21/T-22 | Informe 1: problema, solución/alcance, arquitectura e innovaciones; Subdoc. 4 vale 32 % | directa | paquetes fuente, sin consolidado | exceso de detalle y archivo final vacío | `AFI1-002/017`, integrador/D3 |

## 4. Lo sólido que debe conservarse

No se recomienda reescribir estas bases:

- Catálogo lógico estable de 24 componentes y separación de las ocho capas.
- Partición dual ya acordada de `CTX-VESSEL`: operación de muelle local y mensajería externa diferida.
- Elevación de `SRV-IAM` a crítico para autenticación/autorización vigente durante el corte.
- Catálogo A2 de 21 contrapartes y 7 familias, sin fingir interfaces inexistentes.
- Autoridad `dominio × zona × fase` y convivencia gradual con el TOS.
- Emplazamiento híbrido con núcleo local acotado y servicios no críticos en nube.
- Cálculos de C4: 0,11 TPS normal, 0,23 TPS de coincidencia, telemetría dominante, buffer de 21,9 GB en peak estacional, reposición de 32,5 Mbps y enlace objetivo de al menos 35 Mbps disponibles.
- Capacidad local total de trabajo de aproximadamente 183 GB útiles con 30 % de holgura, sujeta al tamaño real de imagen.
- Política D1 que separa eventos de seguridad de telemetría operacional cruda.
- Fusión de observabilidad/SIEM en una sola plataforma comercial y una sola fila T-11.
- Registro D2 de amenazas, escenarios y riesgos como diseño documental, sin declarar pruebas ejecutadas.
- Regla de que un control lógico no equivale automáticamente a una compra.

## 5. Registro priorizado de hallazgos

### Resumen

| ID | Sev. | Hallazgo | Dueño primario | Tipo de cierre |
|---|---|---|---|---|
| `AFI1-001` | CRÍTICO | la ruta local de 72 h no tiene gateway/API local coherente | A1/C1/C3/D1 | corrección interna |
| `AFI1-002` | PLANIFICADO | T-11 y esqueleto editorial ya tienen baseline; falta redacción/maquetación final | integrador/D3 | BASELINE CERRADA MA-5/MA-8; PRODUCCIÓN FINAL PUBLICA |
| `AFI1-003` | ALTO | falta dimensionamiento físico de la sala y del equipamiento | C2/C4 | cálculo/selección interna |
| `AFI1-004` | ALTO | proveedor, regiones, productos y versiones no forman una línea base ofertable | C2/ADR-011/integrador | selección condicionada |
| `AFI1-005` | ALTO | el hardware comprado por el CLIENTE aparece dentro y fuera del T-11 a la vez | C2/C4/integrador | interpretación y normalización |
| `AFI1-006` | ALTO | textos históricos contradicen correcciones ya aplicadas | D1/D2/gobierno | propagación editorial controlada |
| `AFI1-007` | ALTO | SPOF no consolidados y aceptaciones sin autoridad | C1/D2/integrador | conciliación/estado |
| `AFI1-008` | ALTO | trazabilidad de estándares aún no llega a control y evidencia por fila | gobierno/D3 + frentes | matriz de aplicabilidad |
| `AFI1-009` | ALTO | C1 conserva 13 GB donde C4 fijó 21,9 GB/183 GB | C1/C4 | corrección numérica |
| `AFI1-010` | ALTO | Registro ADR y menciones locales están desincronizados | gobierno/A3/C2/D1/D2 | revisión de estados |
| `AFI1-011` | MEDIO | planificación offline se describe como ejecutable y no disponible | A1/A3/C1/C3 | precisar alcance |
| `AFI1-012` | MEDIO | OpenAPI/AsyncAPI se declara generado desde código y a la vez fuente del contrato | A2/C2 | elegir contract-first o code-first |
| `AFI1-013` | MEDIO | la Matriz Global anuncia 28 filas T-11, pero enumera 30 | gobierno/C4 | corrección mecánica |
| `AFI1-014` | MEDIO | DoD, trazas y complemento tecnológico conservan dependencias ya resueltas | autores/integrador | saneamiento de estado |
| `AFI1-015` | MEDIO | `PHY-EDG-05` es nodo físico en unos archivos y “sin recinto propio” en otros | C1/C2/D2 | normalizar catálogo |
| `AFI1-016` | MEDIO | C1 declara región primaria/secundaria “declaradas” sin ubicación real | C1/C2/ADR-011 | matizar estado |
| `AFI1-017` | EDITORIAL | los paquetes contienen demasiado detalle de Informes 2/3 para publicarlo íntegro en I1 | D3/integrador | CERRADO MA-7; contrato de síntesis |
| `AFI1-018` | PLANIFICADO | faltan vistas y planos finales | todos/B8/D3 | set definido MA-7; producción B8 |

### 5.1 Contradicciones A ↔ C ↔ D que deben resolverse juntas

| Materia | Frente lógico A | Frente físico C | Seguridad/gobierno D | Diagnóstico |
|---|---|---|---|---|
| Entrada a funciones críticas durante 72 h | todo canal pasa por `GW-API`; no se permite `CH-* → CTX-*` directo | `GW-API` solo en nube y no vive durante el corte | D1 deja variante local “solo si A2/A3 la requieren” | contradicción crítica; falta decisión y nodo local |
| Inventario de `EDGE-RUN` | lista diez componentes críticos, pero las cinco cadenas usan además apoyos parciales | C1 sí reparte localmente `DATA-TS`, `SRV-EVID`, `SRV-NOTIF` e `INT-HUB` | controles existen, pero no hay inventario único | soporte local correcto en intención, incompleto como catálogo |
| Planificación offline | “propuesta ejecutable localmente” | último plan en solo lectura; no replanifica | A3/C3: plan impreso y radio | alcance semántico incompatible |
| Buffer local | C4 consumido como fuente física | C1 conserva ≈13 GB | D no cambia el cálculo | valor antiguo; deben regir 21,9 GB y 183 GB totales |
| `CTX-VESSEL`, criticidad, `CH-CAB` y `SRV-IAM` | corregidos en A1 | corregidos en C1/C2 | D1/D2 todavía los reportan abiertos | deriva histórica, no una decisión pendiente real |
| SPOF | A1 tiene `GW-API` sin ID D2 y usa lenguaje de aceptación | C1 informa cuatro ausentes y un residual “aceptado” | D2 dice registro completo y 0 aceptados | registro global no consolidado |
| Proveedor/región | lógica portable, sin proveedor | primario/secundario conceptuales | ADR-011 candidato | patrón definido, ubicación ofertada aún no |
| Hardware de terreno | canales/componentes lo requieren | filas T-11 creadas y simultáneamente excluidas por compra CLIENTE | amenazas/controles lo consumen | separar especificación, provisión y precio |

## 6. Hallazgos críticos y altos

### `AFI1-001` — La operación local de 72 horas no tiene una entrada coherente

**Evidencia interna.** A1 establece que `CH-PORTAL`, `CH-APP` y `CH-CAB` no pueden invocar directamente `CTX-*` ni datos: toda operación pasa por `GW-API`. Sin embargo, C1 ubica `GW-API` únicamente en `PHY-CLD-02` y declara que no vive durante el corte. Al mismo tiempo, A1/C1/C3 prometen que gate, patio, reefer, nave y facturación funcionan en `EDGE-RUN` durante 72 horas.

**Por qué es crítico.** Tener cómputo y datos locales no sirve si el canal operacional no puede alcanzar los servicios locales por la ruta autorizada. Resolverlo mediante acceso directo del canal a los contextos rompería la regla lógica y los controles de autorización.

**Corrección quirúrgica requerida.** Definir explícitamente una puerta local para los perfiles operacionales, por ejemplo una instancia local reducida de `GW-API` o una función equivalente incluida en `EDGE-RUN`, con:

- validación de esquema y autorización local;
- políticas y versiones vigentes cacheadas;
- ruteo solo a las funciones críticas permitidas;
- identidad local coherente con `SRV-IAM`;
- trazabilidad y buffer de registros;
- reconciliación al volver el enlace.

La corrección debe propagarse a A1, C1, C3, D1, D2, capacidad, T-11 y diagramas. Además debe enumerarse el soporte local parcial de `DATA-TS`, `SRV-EVID`, `SRV-NOTIF` e `INT-HUB`; hoy existe disperso en C1, pero no forma un inventario canónico de `EDGE-RUN`.

**Cierre verificable.** Se puede recorrer `CH-APP/CH-CAB → gateway local → CTX crítico → DATA local → evidencia/log local` sin nube y sin violar una dependencia prohibida.

### `AFI1-003` — La sala está especificada, pero no dimensionada

C2 recorre las obligaciones de sala, pero deriva a C4 procesador, memoria, consumo, racks, UPS, generación, climatización, PUE y RAID. C4 dimensiona carga lógica, almacenamiento y red, pero no completa:

- configuración por servidor: procesador, núcleos, RAM, interfaces y consumo;
- capacidad bruta y nivel de RAID seleccionado con comparación;
- ocupación y cantidad de racks de cómputo y comunicaciones;
- carga TI total en kW y factor de potencia;
- UPS necesaria para 30 minutos a plena carga;
- potencia del grupo electrógeno y combustible para 24 horas;
- carga térmica y capacidad/unidades N+1 de climatización;
- capacidad de CCTV/retención del recinto;
- PUE estimada y supuestos.

**Impacto.** Sin esto no se justifican las cantidades de `T11-C2-01..11`, no se puede dibujar un plano de racks defendible y la sala primaria queda como lista de requisitos, no como diseño ofertado.

**Tratamiento.** Completar un dimensionamiento de referencia con supuestos explícitos y margen. Los datos externos pueden cambiar el modelo exacto, pero no justifican dejar sin cálculo la línea base del Informe 1.

### `AFI1-004` — Existe catálogo tecnológico, pero no línea base ofertable completa

C2 ya define React/Angular, Java/.NET/Go, React Native/Flutter, PostgreSQL, contenedores, broker, OpenTelemetry, IaC y familias de hardware. Eso cubre la idea tecnológica. Lo que falta para T-11 y la vista física es:

- escoger una referencia principal donde hoy hay varias equivalentes al mismo nivel;
- indicar versión de referencia a la fecha del Informe 1 y política LTS/EOS;
- escoger o condicionar explícitamente el proveedor y región primaria/secundaria;
- asociar servicio gestionado concreto o familia ofertada a cada plataforma que genera fila;
- convertir familias de hardware en modelo de referencia más especificación mínima.

No se exige “casarse” irreversiblemente con una marca. Sí se exige que la columna **Producto / servicio ofertado** pueda llenarse y que la alternativa quede como alternativa, no como segunda oferta simultánea.

Este hallazgo quedó cerrado en MA-5: `ADR-011` pasó a `PROPUESTO` con AWS, `sa-east-1` primaria multi-AZ y `us-east-1` secundaria. La medición y acreditación pendientes son condiciones de aprobación; “nube primaria” ya no es una ubicación vacía.

### `AFI1-005` — El hardware de terreno no puede estar dentro y fuera del T-11

C2 y la Matriz Global crean `T11-C2-14`, `T11-C2-15` y `T11-C2-16` para gabinetes, dispositivos y concentradores. Sin embargo, C4 y la Matriz Global dicen también que el hardware cuya adquisición corresponde al CLIENTE queda fuera del T-11.

**Problema.** Las bases separan quién compra de quién debe especificar. Que el CLIENTE adquiera un equipo no elimina la obligación técnica del PROPONENTE de especificarlo y justificarlo. Para Informe 1 no se incluyen precios, pero debe existir una sola interpretación de alcance.

**Corrección.** Mantener en la arquitectura y en la matriz técnica los equipos que TERABYTE debe especificar; declarar en la justificación “adquisición a cargo del CLIENTE” cuando aplique. Si el formato T-11 se interpreta estrictamente como solo provisión del adjudicatario, crear un anexo 1:1 de “hardware especificado de adquisición CLIENTE” y dejar una exclusión inequívoca. No duplicar ni borrar silenciosamente.

### `AFI1-006` — Las correcciones no se propagaron a todos los consumidores

Ya se corrigieron `CTX-VESSEL`, `CH-CAB`, criticidades, SIEM, `ACT-TI`, `SRV-IAM` y partes de ADR-011. Aun así, sobreviven textos vigentes que dicen lo contrario:

- D1 B7-R y B7-C todavía dicen que `CTX-VESSEL` no está conciliado y que seis criticidades, `CH-CAB` y SIEM siguen abiertos.
- D2 y `TRZ_D2` todavía describen `CTX-VESSEL` solo en nube y diferencias de criticidad anteriores.
- el Registro ADR todavía deja en `ADR-002` una conciliación A1↔C1 pendiente.
- C2 todavía dice que `ADR-008` está `EN ANÁLISIS` y que ADR-011 “no existe/no está abierto”.
- el complemento tecnológico todavía afirma que frontend, backend/API y app de terreno están pendientes, aunque el commit `4e724c8` ya los agregó.

**Tratamiento.** No borrar el historial: rotularlo como corte histórico y agregar un estado vigente inequívoco, o reemplazar afirmaciones que todavía se presentan como actuales. La narrativa final solo debe consumir el corte vigente.

### `AFI1-007` — El registro consolidado de SPOF no es todavía consolidado

C1 declara que cuatro condiciones no están en D2: conmutación compartida, tableros reefer sin instrumentación, generación reefer no probada a carga total y proveedor de nube único. D2, en cambio, concluye que sus 22 SPOF son el registro consolidado sin omisiones.

Además:

- A1 identifica `GW-API` como punto único lógico sin ID consolidado en D2.
- C1 marca `F2-SPOF-07` como “residual aceptado”.
- D2 establece expresamente 0 riesgos/SPOF aceptados y exige aprobador, fundamento, evidencia y condición de revisión.

**Corrección.** Revisar cada candidato por sustancia, no por nombre. Incorporar al registro global los que realmente subsisten o explicar por qué son brecha preexistente/controlada y no un SPOF de la solución. Sustituir toda “aceptación” no autorizada por `POR ACEPTAR` o `ESCALADO`.

**Cierre verificable.** Existe una sola tabla global; A1/C1 solo la referencian; ninguna aceptación carece de autoridad.

### `AFI1-008` — El Artículo 4 todavía no tiene evidencia trazable suficiente

> **Cierre MA-6:** hallazgo cerrado para el alcance del Informe 1 en [`11_MATRIZ_ARTICULO4_MA6.md`](Celula3/00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md). La matriz responde 38 estándares/prácticas y 15 materias normativas mediante `aplicabilidad → requisito → control → componente → evidencia I1 → evidencia futura`. Mantiene cuatro parciales controlados, dos condiciones externas tratadas y dos `NO APLICA JUSTIFICADO` por ausencia de IA; ninguno queda como mera mención.

La Matriz Global enumera estándares, pero varias filas siguen en `PENDIENTE` o apuntan a materias generales. La advertencia oficial exige que cada estándar llegue a un control concreto y al entregable que lo evidencia.

Para el Subdocumento 4/Informe 1 se debe cerrar, como mínimo:

| Familia | Aplicación mínima en I1 | Evidencia de diseño |
|---|---|---|
| ISO/IEC/IEEE 42010 + TOGAF o equivalente | estructura de vistas, interesados, preocupaciones, correspondencias y gobierno ADR | índice del Subdoc. 4 + matriz de vistas/decisiones |
| ISO 27001/27002/27017/27018 + NIST CSF/800-207 | gobierno, nube, privacidad y Zero Trust | controles D1, nodos, amenaza y evidencia prevista |
| OWASP ASVS/Top 10/API Top 10/SAMM + CIS | software/API/hardening | controles D1 + producto/versión C2 + prueba prevista |
| SLSA 3+, SBOM CycloneDX/SPDX y firma | cadena de suministro | `T11-C3-04`, pipeline y evidencia de artefacto prevista |
| ISO 22301 + ISO/IEC 27031 | continuidad de negocio/TIC | C3: escenarios, RTO/RPO, DR, respaldo y pruebas |
| WCAG 2.2 AA + EN 301 549 | portal, app y cabina/terreno | A1/C2: controles de interacción y criterio de prueba |
| OpenAPI 3.1 + AsyncAPI 2.6+ + sectoriales | contratos síncronos/eventos/EDIFACT/ISO 6346 | A2: catálogo, versión, fallback y aceptación |
| ISO 14001 + PUE | sala y sostenibilidad | C2/C4: medición energética, PUE y evidencia prevista |

ISO 20000-1/ITIL/SRE, ISO 25010/25012/29119 y PMBOK pueden tener una referencia breve en I1 y su desarrollo principal en los subdocumentos/entregas correspondientes. No deben marcarse “cumplidos” solo porque existe una intención.

**IA condicional.** `CTX-PLAN` “aprende de las excepciones”, pero la arquitectura no declara si eso significa IA. Se debe decidir: si es motor de reglas/captura de conocimiento sin IA, marcar NIST AI RMF e ISO/IEC 42001 como `NO APLICA JUSTIFICADO`; si incorpora IA, activar sus controles, trazabilidad y capacidad de desactivación. Dejarlo ambiguo mantiene `STD-18` abierto y expone el Art. 4/obligaciones de IA.

### `AFI1-009` — C1 conserva una capacidad anterior al cálculo vigente

C1 describe `PHY-OPS-02` como “buffer del corte, ≈13 GB + holgura”. C4 corrigió expresamente ese valor:

- 13,7 GB corresponde al régimen promedio;
- 21,9 GB corresponde al peak estacional y es el valor que gobierna el compromiso;
- aproximadamente 183 GB útiles es la capacidad local total propuesta después de agregar ventana caliente, réplica, sistema/logs/trabajo y 30 % de holgura.

**Corrección.** C1 debe usar 21,9 GB para el buffer y enlazar 183 GB útiles como capacidad total. No mezclar buffer con capacidad del arreglo en T-11.

### `AFI1-010` — Los ADR tienen estados defendibles, pero no coherentes

El conjunto razonable para este corte es mantener propuestas y candidatos, no promover todo a aprobado. Lo que debe corregirse es la deriva:

- A3 titula `ADR-002/004` como “candidatos”, pero dentro los marca `Propuesto` y el Registro Global dice `PROPUESTO`.
- `ADR-002` aún arrastra la antigua contradicción de `CTX-VESSEL`.
- `ADR-008` conserva lenguaje de “capacidad local condicionada” aunque `SRV-IAM` ya es obligación crítica de continuidad.
- C2 dice que `ADR-011` no existe/no está abierto, aunque está registrado y ya tiene alternativas/recomendación condicionada.
- `ADR-005/007/011` alimentan T-11 y sus condiciones aparecen en las filas afectadas; tras MA-5 los tres están `PROPUESTO`, ninguno `APROBADO`.

**Regla de cierre.** Promover solo si se satisfacen alternativas reales, criterios, consecuencias negativas, trazabilidad y efecto en las vistas. Para I1 basta una línea base `PROPUESTA CONDICIONADA` cuando los datos faltantes sean verdaderamente externos.

## 7. Hallazgos medios

### `AFI1-011` — Planificación durante el corte

A1 dice que `CTX-PLAN` tiene “propuesta ejecutable localmente”; C1 dice que el plan vigente queda en solo lectura y la replanificación no; A3/C3 dicen que planificación se degrada y usa plan impreso/radio.

**Corrección.** Adoptar una frase única: durante el corte se puede consultar el último plan vigente cacheado, pero no generar/recalcular un plan nuevo; el respaldo operacional es plan impreso + radio. Si se quiere replanificación local, debe incluirse el componente, datos y capacidad en `EDGE-RUN`.

### `AFI1-012` — Contrato de interfaz como fuente

A2/C2 dicen que OpenAPI/AsyncAPI se generan desde código y, simultáneamente, que el contrato es la fuente y no el código. Son dos estrategias diferentes.

**Corrección.** Elegir una:

- `contract-first`: especificación versionada es fuente; código/stubs/validadores se generan o verifican contra ella; o
- `code-first`: código anotado es fuente y genera la especificación.

Para el gobierno de 21 contrapartes y compatibilidad de seis meses, `contract-first` es la opción más coherente con lo ya escrito.

### `AFI1-013` — Conteo T-11 incorrecto

La Matriz Global declara 28 filas, pero su aritmética y tabla contienen 30: 20 de C2 + 4 de C3 + 6 de seguridad. `T11-SEC-04` no genera fila adicional porque se absorbe en `T11-C2-19`.

**Corrección.** Cambiar el conteo o justificar fusiones adicionales antes de volcar el formulario.

### `AFI1-014` — Estados antiguos en DoD, trazas y complemento

C1–C4 conservan casillas de contrato sin marcar y otra sección de estado actual. Algunos archivos explican esta doble lectura; otros todavía dicen “depende de C4” o “TRZ en curso” aunque el insumo ya existe. El complemento tecnológico dice que el stack de aplicaciones falta cuando ya fue incorporado.

**Corrección.** Mantener una plantilla normativa y una única tabla de estado vigente. En trazas, convertir `PENDIENTE C4` en `PARA REVISIÓN` o `CUBIERTO` cuando C4 ya entregó el dato; mantener como externos solamente prueba, site survey, producto, contrato o dato realmente faltante.

### `AFI1-015` — Naturaleza de `PHY-EDG-05`

C1 conserva `PHY-EDG-05` como “borde de zona de inspección” pero aclara que no tiene gabinete propio; C2 indica que existen cuatro zonas de borde físicas y que inspección usa dispositivo móvil sobre la red del patio. D2 todavía trata `PHY-EDG-05` como nodo.

**Corrección.** Decidir si es una ubicación lógica sin infraestructura o eliminarlo como nodo y mapear inspección a `PHY-EDG-02` + dispositivo móvil. El diagrama y el conteo de nodos no deben sugerir un quinto gabinete.

### `AFI1-016` — Región “declarada” versus región seleccionada

C1 marca como cumplido que la región primaria/secundaria está declarada, mientras C2/ADR-011 reconocen que no existe proveedor ni región seleccionada.

**Corrección.** Cambiar el estado a “patrón primario/secundario definido; proveedor y regiones condicionados a ADR-011”. Solo usar “ubicación declarada” cuando el lugar sea concreto.

## 8. Bloqueantes planificados

### `AFI1-002` — Archivos finales vacíos

**Estado posterior:** cerrado como baseline en MA-5/MA-8. `01_T11_TRABAJO_TRAZABLE.md` y `02_FORMULARIO_T11_FINAL.md` contienen 32 filas; `00_BASE_TECNICA_SUBDOCUMENTO_4.md` ya tiene el esqueleto formal 4.1/4.2, fuentes directas y controles D3. La prosa, figuras y maquetación corresponden a la producción final.

### `AFI1-018` — Diagramas y planos

Faltan las vistas finales coherentes y los planos conceptuales de sala/racks. MA-7 fijó F1–F5 como set obligatorio, `V-DATA-01` como vista tabular y F6 como figura condicional. B8 comienza después de aprobar la puerta P4; no espera aprobación externa de todas las dependencias.

Antes de diagramar deben quedar congelados:

- ruta local de 72 h;
- inventario `EDGE-RUN`;
- nodos físicos y `PHY-EDG-05`;
- proveedor/regiones o notación condicionada;
- productos/familias y cantidades T-11;
- ADR-005/007/008/011 y SPOF vigentes.

## 9. Ajuste editorial para no sobredimensionar el Informe 1

### `AFI1-017` — Síntesis de contenido avanzado

A1–D2 contienen aproximadamente cien mil palabras. Ese nivel de detalle es útil como respaldo, pero no debe copiarse íntegro al Subdocumento 4.

**Estado posterior:** cerrado en MA-7 mediante un contrato editorial de 20–25 páginas, incluidas las 32 filas del T-11. Para Informe 1 se publicará:

- catálogo ejecutivo de componentes y responsabilidades;
- tablas de emplazamiento, tecnologías, implementos y capacidad;
- cinco diagramas propios obligatorios, con una sexta figura solo si la continuidad no resulta legible;
- resumen de integración, seguridad, continuidad y despliegue;
- ADR ejecutivos relevantes y registro consolidado de SPOF;
- matriz breve estándar → control → evidencia;
- T-11 final;
- supuestos y dependencias externas con tratamiento.

Conservar como anexos o fuentes internas:

- las 73 amenazas y sus tablas completas;
- los doce escenarios detallados;
- catálogo extendido de controles;
- plan de pruebas exhaustivo y calendarios de ejecución;
- procedimientos operativos detallados, riesgos de implantación y evidencia todavía no ejecutada.

La síntesis no elimina trazabilidad: cada afirmación final conserva un enlace estable al paquete que la sustenta.

## 10. Dependencias externas legítimas

Estas materias no deben “cerrarse” inventando datos y no son fallas del equipo si llevan rango, responsable y fallback:

| Dependencia | Tratamiento válido para I1 |
|---|---|
| site survey del patio | rango 6–8 estaciones; criterio y prueba de cobertura/handover |
| capacidad real de fibra/radio | compromiso ≥35 Mbps disponibles; verificación y alternativa si el respaldo actual no alcanza |
| tamaño real de imágenes OCR | supuesto 500 KB, sensibilidad y margen; reemplazar con medición |
| AHT de mesa de ayuda | cantidad provisional calculada; ajuste con medición |
| tamaño/contrato del TOS e interfaces de terceros | capa anticorrupción, fallback y puerta de viabilidad |
| directorio, revocación aislada y nombradas | requisito local no rebajable; mecanismo/producto por validar |
| autorización ISPS y ventanas de intervención | no intervenir sin aprobación; calendario condicionado |
| latencia, carbono y servicios por región cloud | criterios de ADR-011 y selección condicionada |
| clasificación campo→sensibilidad→retención | taxonomía provisional; cierre con Subdocumento 5/CLIENTE |
| pruebas y aceptaciones | evidencia futura; no se presenta como ejecutada |

No son dependencias externas:

- decidir si existe gateway local;
- unificar el valor del buffer;
- corregir estados y referencias históricas;
- decidir contract-first/code-first;
- explicar el alcance de `PHY-EDG-05`;
- conciliar el registro SPOF;
- completar una línea base de dimensionamiento físico con supuestos.

## 11. Orden recomendado de corrección posterior a P1

1. **Cerrar la ruta local de 72 h** y el inventario canónico de `EDGE-RUN` (`AFI1-001`).
2. **Corregir contradicciones de fuente vigente**: capacidad, planificación, nodos y hardware T-11 (`AFI1-005/006/009/011/015/016`).
3. **Revisar ADR y SPOF** sin aprobar artificialmente (`AFI1-007/010`).
4. **Completar catálogo ofertable y dimensionamiento físico** (`AFI1-003/004/012`).
5. **Cerrar aplicabilidad de estándares** y la decisión IA/no IA (`AFI1-008`).
6. **Sanear trazas y conteos** (`AFI1-013/014`).
7. Ejecutar la consolidación del T-11 y control 1:1.
8. Recién entonces producir diagramas, D3 y el Subdocumento 4 final.

## 12. Puerta P1 — decisión

`MA-0`, `MA-1` y `MA-2` quedan ejecutados. Este archivo es el registro de hallazgos previo a correcciones.

**No se modificaron A1–D2, ADR, Matriz Global, T-11 ni consolidado final en esta ola.**

Para habilitar MA-3, el equipo debe aceptar el orden de corrección o ajustar la severidad de algún hallazgo. La arquitectura puede llegar a un Subdocumento 4 sólido con cambios acotados; el único asunto que exige una decisión arquitectónica nueva es la ruta local de acceso a servicios durante las 72 horas. El resto es completar, seleccionar, conciliar y sintetizar lo ya trabajado.
