# Catálogo de Requerimientos Funcionales — DEFINITIVO · Parte 3 de 3

## Dominios `RF-NAV`, `RF-INT`, `RF-FAC`, `RF-POR`, `RF-INS`, `RF-EMI`, `RF-APP` y `RF-FIR` — 59 requerimientos

> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo B** · **Versión 2.1 — correcciones de la Fase 4 y decisiones de duplicados RF/RNF ya aplicadas.**
> **Este archivo reemplaza a `catalogo_rf_03_nave_integraciones.md`, `catalogo_rf_04_facturacion_portal.md` y la parte de `RF-INS` y `RF-EMI` de `catalogo_rf_05_*.md`.**
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26). Las convenciones del catálogo están en la **Parte 1, sección 1**.

---

## Índice

| Sección | Contenido | Req. |
|---|---|---:|
| **1** | Las dos restricciones que gobiernan este bloque | — |
| **2** | `RF-NAV` — Nave, planificación y productividad | **14** |
| **3** | `RF-INT` — Integraciones y mensajería | **11** |
| **4** | `RF-FAC` — Hechos facturables y su evidencia | **11** |
| **5** | `RF-POR` — Portal y autoservicio | **8** |
| **6** | `RF-INS` — Inspecciones y autoridades | **7** |
| **7** | `RF-EMI` — Emisiones y consumo energético | **6** |
| **8** | `RF-APP` — Aplicación móvil operacional | **1** |
| **9** | `RF-FIR` — Firma electrónica transversal | **1** |
| **10** | Correspondencia del portal y trámites en otros dominios | — |
| **11** | Trazabilidad de la parte 3 y cierre del catálogo | — |

**Requerimientos en revisión en esta parte: 0.** El caso `RF-POR-07` quedó resuelto; el estado vigente se consolida en `../03_Trazabilidad_y_Bases/registro_correccion_plan_maestro_20260904.md`.

---

## 1. Las dos restricciones que gobiernan este bloque

> **CP, Cap. 10, restricción N° 3:** *«El sistema de control de las grúas de muelle es del fabricante y no se interviene. Cualquier obtención de datos desde él es una integración de solo lectura sujeta a autorización.»*
>
> **CP, Cap. 10, restricción N° 5:** *«El sistema de gestión empresarial se mantiene y sigue siendo el único emisor de documentos tributarios.»*

De la primera se sigue una consecuencia de diseño que atraviesa todo `RF-NAV`: **la productividad de grúa no se obtiene del sistema de control de la grúa**, sino del registro de movimientos por telemetría (`RF-PAT-05`, `RF-PAT-13`, `RF-TRA-04`). Depender del sistema del fabricante haría que un criterio de aceptación comprometido quedara sujeto a una autorización de tercero que el propio caso declara no verificada.

---

## 2. Dominio `RF-NAV` — Nave, planificación y productividad

**Etapa 2 · 14 requerimientos**, con una excepción: `RF-NAV-09` pertenece a la **Etapa 1**.

---

### `RF-NAV-01` — Recepción normalizada del anuncio de recalada · Prioridad: **Alta**

**Descripción.** La solución **deberá** recibir el anuncio de recalada de cada naviera y normalizarlo a un **registro único de recalada** con nave, llegada estimada, movimientos de descarga y de embarque, y listado de contenedores cuando venga informado, cualquiera sea el canal por el que llegue.

**Actor:** naviera y solución. **Precondición:** naviera registrada como contraparte.
**Resultado esperado:** anuncio disponible como dato estructurado, sin digitación.
**Origen:** CP, Cap. 4.1 (el anuncio llega «por correo electrónico, por el portal de la naviera o por teléfono, según la línea», con 10 a 3 días de anticipación variable) · CP, Cap. 5 (correo y planillas deben dejar de ser sistema de registro).
**Criterio de aceptación:** se reciben anuncios por los **tres canales** y los tres producen un registro de recalada equivalente y estructurado, sin digitación.

---

### `RF-NAV-02` — Programación de sitios y asignación de grúas · Prioridad: **Alta**

**Descripción.** La solución **deberá** mantener la programación de los tres sitios y de las seis grúas de muelle como registro único del sistema, y **deberá** conservar cada modificación con su autor, su instante y su motivo.

**Actor:** jefatura de operaciones. **Precondición:** recaladas anunciadas registradas.
**Resultado esperado:** programación vigente única y consultable; historial de cambios reconstruible.
**Origen:** CP, Cap. 4.1 (hoy la programación vive en una planilla que «se rehace varias veces al día») · CP, Cap. 5 · BTT, RT-16.06.
**Criterio de aceptación:** se modifica la programación tres veces y se reconstruye el historial completo con autor, instante y motivo de cada cambio.

---

### `RF-NAV-03` — Confirmación de la ventana de atraque con 72 horas · Prioridad: **Crítica**

**Descripción.** La solución **deberá** confirmar a la naviera la ventana de atraque con **al menos 72 horas de anticipación** al inicio de la ventana, por canal registrado, y **deberá** dejar constancia del instante de la confirmación.

**Actor:** solución y naviera. **Precondición:** programación de sitios definida para la recalada.
**Resultado esperado:** ventana confirmada con la anticipación comprometida y con evidencia del acto.
**Origen:** CP, Cap. 18, criterio 5 · CP, Cap. 9.2 · CP, Cap. 1 (condición de la alianza naviera para 2029) · CP, 7.1 (cumplimiento actual 71 %, referencia 90 %).
**Criterio de aceptación:** para las líneas de la alianza, el **100 %** de las ventanas del universo acordado se confirma con al menos 72 horas. Para la operación general, el cumplimiento efectivo de la ventana debe quedar **sobre 90 %**, con fórmula, universo y exclusiones acordados y auditables.

---

### `RF-NAV-04` — Notificación registrada del cambio de ventana · Prioridad: **Alta**

**Descripción.** Ante cualquier modificación de una ventana confirmada, la solución **deberá** notificar a la naviera por canal registrado, y **no deberá** admitir que el cambio se comunique únicamente por vía telefónica.

**Actor:** solución y naviera. **Precondición:** ventana previamente confirmada.
**Resultado esperado:** cambio notificado con evidencia de emisión y de recepción.
**Origen:** CP, Cap. 4.1 («la ventana se confirma a la naviera por correo; cuando cambia, se avisa por teléfono») · BTT, RT-16.23 (registro de entrega, apertura y error por mensaje).
**Criterio de aceptación:** se modifica una ventana confirmada y se recupera el registro de notificación con su estado de entrega.

---

### `RF-NAV-05` — Estimación de duración a partir de serie histórica · Prioridad: **Alta**

**Descripción.** La solución **deberá** estimar la duración de atención de una nave a partir de la **serie histórica de productividad registrada** por sitio, grúa y tipo de operación, y **no deberá** basarla en una productividad supuesta ajustada manualmente.

**Actor:** jefatura de operaciones. **Precondición:** serie histórica de movimientos disponible.
**Resultado esperado:** estimación con método declarado y reproducible.
**Origen:** CP, Cap. 4.1 («no hay modelo, no hay serie histórica sistematizada») · CP, Cap. 9.2 · CP, 7.1.
**Criterio de aceptación:** se estima la duración de **10 recaladas** y cada cálculo es reproducible a partir de la serie histórica, sin ningún parámetro ajustado a mano.

---

### `RF-NAV-06` — Propuesta automática del plan de estiba y de patio · Prioridad: **Crítica**

**Descripción.** La solución **deberá** proponer automáticamente el plan de estiba y el plan de patio, respetando peso, altura, puerto de destino, segregación de carga peligrosa, estabilidad de la nave y disponibilidad de conexión refrigerada a bordo. Cuando dos restricciones no puedan satisfacerse simultáneamente, la solución **deberá** aplicar el orden de precedencia de **RN-09** y **deberá** explicitar cuál restricción cedió.

**Actor:** solución. **Precondición:** plano de estiba recibido y listado de contenedores disponible.
**Resultado esperado:** plan propuesto, no impuesto: queda a la espera de la decisión del planificador, con las cesiones declaradas.
**Origen:** Decisión N° 4 («el algoritmo propone, el planificador aprueba o corrige») · CP, Cap. 4.2 (enumeración de las restricciones que el plan debe respetar) · **RN-09** fija la precedencia: estabilidad y seguridad de la nave, segregación IMDG, disponibilidad de conexión refrigerada a bordo, puerto de destino, secuencia de carga · CP, Cap. 18, criterio 7.
**Criterio de aceptación:** batería de **20 recaladas históricas reales**; el plan propuesto cumple las seis restricciones en las 20, y en los casos de conflicto aplica el orden de RN-09 y declara cuál restricción cedió.

> *Correcciones aplicadas: el criterio anterior era circular («se verifica el cumplimiento de las seis restricciones») y el requerimiento no decía qué hacer cuando dos restricciones se contradicen — situación que el CP, Cap. 4.2 documenta como real, por ejemplo cuando los reefer van a proa porque el generador de popa está limitado.*

---

### `RF-NAV-07` — Aprobación o corrección del plan por el planificador · Prioridad: **Crítica**

**Descripción.** El planificador **deberá** poder aprobar la propuesta o corregirla antes de su publicación, y la solución **no deberá** publicar un plan que no haya sido aprobado o corregido por él.

**Actor:** planificador de estiba y patio. **Precondición:** plan propuesto disponible.
**Resultado esperado:** el plan vigente siempre tiene una decisión humana detrás.
**Origen:** Decisión N° 4, que descarta la automatización plena · CP, Cap. 8 (el planificador acepta el esquema en que «la máquina me proponga y yo corrija») · CP, Cap. 9.3 («un mecanismo que proponga y una persona que decida»).
**Criterio de aceptación:** se intenta publicar un plan sin aprobación y el sistema no lo publica; el **100 %** de los planes publicados en un período registra la aprobación o corrección de su autor.

---

### `RF-NAV-08` — Registro estructurado del motivo de cada corrección · Prioridad: **Crítica**

**Descripción.** Cuando el planificador corrija la propuesta, la solución **deberá** exigir y registrar el **motivo de la corrección de forma estructurada**, y **no deberá** admitir la corrección sin motivo.

**Actor:** planificador. **Precondición:** corrección iniciada sobre una propuesta.
**Resultado esperado:** corpus creciente de decisiones con su razón, explotable como conocimiento.
**Origen:** Decisión N° 4 · CP, Cap. 16.1 decisión 4 (es el mecanismo por el cual el conocimiento «queda en la empresa antes de 2028, o no queda») · CP, Cap. 8 («que quede registrado por qué corregí. Así el que venga después aprende de eso, no de mirarme a mí»).
**Criterio de aceptación:** se intenta corregir sin motivo y el sistema no acepta la corrección; se consulta el corpus acumulado y las correcciones se agrupan por motivo.

> El campo de impacto de la Decisión N° 4 advierte que si el motivo no se captura de forma estructurada, «el conocimiento se pierde igual, solo que documentado de forma inutilizable». De ahí que el motivo sea estructurado y no texto libre.

---

### `RF-NAV-09` — Registro de reglas del planificador · Prioridad: **Crítica** · **Etapa 1**

**Descripción.** La solución **deberá** mantener un **registro de las reglas, restricciones y casos del planificador** —estado real de los equipos, comportamiento físico de los bloques, particularidades de naves, comportamiento de clientes y reglas normativas duras—, editable y versionado, y **deberá** aplicarlo en cada corrida del motor de propuesta.

**Actor:** planificador y analista de Terabyte. **Precondición:** registro habilitado.
**Resultado esperado:** el motor de propuesta aplica las reglas vigentes del registro.
**Origen:** Decisión N° 1, frente de captura del conocimiento tácito · CP, Cap. 17.1 (registro de reglas de negocio) · CP, Cap. 4.2 (la grúa tres con falla intermitente, el bloque C que se inunda, el generador de popa limitado, el exportador que llega tarde: «nada de eso está escrito en ninguna parte») · CP, Cap. 18, criterio 22.
**Criterio de aceptación:** se registra una regla nueva y la **siguiente corrida** del motor la aplica; la regla queda versionada con su autor e instante.

> *Corrección aplicada: este requerimiento contenía dos cosas con pruebas distintas. La conducta del sistema queda aquí. **La producción documental del registro pasó a la EDT como entregable de proyecto EP-01**: primera versión antes del hito H2 (mes 4), versión validada con el planificador antes del cierre de desarrollo de la Etapa 1 (mes 12). Su trazabilidad al criterio de aceptación 22 se mantiene.*
>
> **Por qué EP-01 es de Etapa 1.** La planificación asistida entra en producción en el mes 21 y el planificador se retira «el 2028» sin mes declarado. Si el módulo fuera el único depositario previsto, el criterio 22 fallaría sin remedio.

---

### `RF-NAV-10` — Distribución del plan vigente a la cabina · Prioridad: **Crítica**

**Descripción.** La solución **deberá** presentar al operador de grúa de muelle el plan vigente en una **pantalla integrada a la cabina**, y **no deberá** requerir que el plan se entregue en papel ni que sus cambios se comuniquen por radio.

**Actor:** operador de grúa de muelle. **Precondición:** plan publicado y pantalla instalada.
**Resultado esperado:** el operador dispone del plan vigente sin intermediación verbal.
**Origen:** Decisión N° 14 · CP, Cap. 18, criterio 21 · CP, Cap. 4.3 (hoy trabaja con «el plan impreso entregado al inicio del turno» y «alguien se lo grita por radio y él anota en el margen de la hoja»).
**Criterio de aceptación:** prueba en cabina real durante la marcha blanca; sobre un turno completo, el operador dispone del plan vigente en el **100 %** de los cambios, sin recibirlo por radio ni en papel.

> La pantalla es un **dispositivo propio de la solución instalado en la cabina**, no una modificación del sistema de control de la grúa, que la restricción N° 3 declara no intervenible.

---

### `RF-NAV-11` — Actualización del plan sin interacción activa · Prioridad: **Crítica**

**Descripción.** La solución **deberá** reflejar los cambios del plan en la pantalla de cabina mediante indicación visual, y **deberá** alertar acústicamente **solo ante condiciones de seguridad**. La solución **no deberá** incorporar botones de confirmación para la operación rutinaria ni exigir que el operador aparte la vista de la carga.

**Actor:** operador de grúa de muelle. **Precondición:** plan modificado durante la operación.
**Resultado esperado:** cambio percibido sin acción del operador y sin desviar su atención de la faena.
**Origen:** CP, Cap. 10, restricción no negociable N° 1 · **CP, Cap. 15, RT-13.08** aporta las condiciones de terreno · Decisión N° 14 · CP, Cap. 18, criterio 21 («sin apartar la vista de la carga»).
**Criterio de aceptación:** revisión ergonómica con el sindicato y con prevención de riesgos **contra el checklist ergonómico por puesto de terreno**, antes del diseño detallado, más prueba en cabina real, con acta de conformidad. Se articula con RNF-USA-05.

---

### `RF-NAV-12` — Medición de productividad en tiempo real · Prioridad: **Crítica**

**Descripción.** La solución **deberá** calcular la productividad de grúa en tiempo real, con granularidad **por hora y por equipo**, a partir del registro de movimientos, y **no deberá** obtenerla del sistema de control de las grúas ni de consolidación manual de formularios de turno.

**Actor:** solución y jefatura de operaciones. **Precondición:** movimientos registrados conforme a `RF-PAT-05` y `RF-PAT-13`.
**Resultado esperado:** productividad consultable en línea, descomponible hasta el movimiento individual.
**Origen:** CP, Cap. 18, criterio 6 · CP, Cap. 10, restricción no negociable N° 3 · CP, 7.1 (registro por hora y por grúa: inexistente) · **CP, Cap. 15, RT-05.29** aporta el umbral de disponibilidad del indicador.
**Criterio de aceptación:** además de consultar y descomponer el indicador hasta los movimientos de origen, se demuestra una productividad efectiva de **al menos 30 movimientos por hora por grúa** durante un período operacional representativo acordado, con detenciones y exclusiones trazables; ningún dato proviene del sistema de control del fabricante.

---

### `RF-NAV-13` — Explicación trazable del sobretiempo de nave · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar las **causas de detención de grúa** —espera de tractocamión, discrepancia entre plan y celda, espera de remoción— y **deberá** producir, para cada recalada, la descomposición del tiempo de atención entre operación efectiva y detención por causa.

**Actor:** jefatura de operaciones y naviera. **Precondición:** operación de nave registrada con sus eventos de detención.
**Resultado esperado:** capacidad de explicar a la naviera, con evidencia, por qué su nave demoró lo que demoró.
**Origen:** CP, 7.1 («capacidad de explicar a la naviera la causa de un sobretiempo de nave: inexistente») · CP, Cap. 9.2 · CP, Cap. 4.3, que enumera las tres causas de la brecha · articula con `RF-TRA-04`, que aporta la primera causa.
**Criterio de aceptación:** para una recalada cerrada se emite la descomposición del tiempo total entre operación efectiva y detenciones clasificadas por causa; la suma reconcilia con la duración registrada **sin residuo no clasificado superior al 5 %**.

---

### `RF-NAV-14` — Replanificación por discrepancia de masa bruta · Prioridad: **Alta**

**Descripción.** Ante un plan de estiba marcado por discrepancia de masa bruta sobre tolerancia, la solución **deberá** recalcular la propuesta afectada y **deberá** someterla nuevamente a la aprobación del planificador antes de publicarla.

**Actor:** solución y planificador. **Precondición:** marca de replanificación generada por `RF-GAT-09`.
**Resultado esperado:** plan corregido y aprobado antes de que el contenedor se embarque con el peso equivocado.
**Origen:** CP, Cap. 4.6 (la discrepancia obliga a rehacer parte del plan «porque la estabilidad de la nave se calculó con el peso equivocado») · CP, Cap. 12, materia 5 (SOLAS VGM) · RN-05 · RN-09, nivel 1 (estabilidad de la nave).
**Criterio de aceptación:** se inyecta una discrepancia sobre tolerancia y el plan afectado se recalcula y vuelve al circuito de aprobación antes de su publicación.

---

## 3. Dominio `RF-INT` — Integraciones y mensajería

**Etapa 2 · 11 requerimientos.**

> El CP, num. 16.2 advierte que quien «prometa mensajería estándar sin haber identificado un solo mensaje por su nombre» quedará en evidencia frente a la Comisión. Los mensajes y las normas se nombran en el cuerpo de cada requerimiento.

### Matriz obligatoria de canales

Esta matriz es un contrato funcional transversal para los RF que emiten avisos; no crea aplicaciones separadas por canal. Célula 3 deberá materializarla mediante una capacidad compartida de notificaciones con adaptadores.

| Público | Canal obligatorio | Evidencia mínima |
|---|---|---|
| Navieras | Mensajería electrónica estándar internacional; canal puente solo donde esté permitido | emisión/recepción, error y correlación por contraparte |
| Transportistas y agencias | Correo, mensajería instantánea y aplicación | entrega, error y apertura cuando el canal lo permita |
| Personal interno | Aplicación y radio integrada donde corresponda | destinatario, instante, canal y resultado |
| Alarma reefer | Dos canales redundantes, escalamiento y confirmación humana | `RF-REF-08` a `10` y `RNF-DIS-08` |

---

### `RF-INT-01` — Recepción del plano de estiba en BAPLIE · Prioridad: **Crítica**

**Descripción.** La solución **deberá** recibir el plano de estiba mediante el mensaje **BAPLIE** de UN/EDIFACT, mantenido por **SMDG**, y **deberá** incorporarlo al plan sin digitación manual.

**Actor:** naviera y solución. **Precondición:** naviera integrada por mensajería.
**Resultado esperado:** plano incorporado como dato estructurado.
**Origen:** Decisión N° 18 · CP, num. 16.2 (identifica BAPLIE como plano de estiba) · CP, Cap. 15, RT-05.23 · CP, Cap. 18, criterio 13 · CP, 7.1 (6 formatos distintos, referencia «estándar único»).
**Criterio de aceptación, en dos hitos:**
> **Factibilidad — cierre de desarrollo de Etapa 2:** se recibe e incorpora un plano por BAPLIE desde **al menos una naviera representativa**, sin digitación.
> **Cobertura:** antes de la fecha efectiva del acuerdo de 2029, cada línea de la alianza está integrada y probada extremo a extremo, sin canal puente ni redigitación. Para las demás líneas, las **14 navieras** tienen factibilidad acreditada al cierre del primer año de Operación, sea por integración efectiva o por acuerdo documentado; el puente es únicamente transitorio.

> *Corrección aplicada: el criterio comprometía «al menos una naviera» mientras citaba RT-05.23, que exige acreditar factibilidad con las 14. Se desdobla en dos hitos.*

---

### `RF-INT-02` — Recepción de la orden de embarque en COPRAR · Prioridad: **Crítica**

**Descripción.** La solución **deberá** recibir la orden de embarque mediante el mensaje **COPRAR** de UN/EDIFACT, y **no deberá** requerir su digitación desde correo electrónico.

**Actor:** naviera y solución. **Precondición:** naviera integrada por mensajería.
**Resultado esperado:** instrucción de embarque incorporada sin redigitación.
**Origen:** Decisión N° 18 · CP, num. 16.2 (COPRAR: orden de embarque) · CP, Cap. 15, RT-05.23 · CP, 7.1 (41 % de instrucciones recibidas por correo y digitadas a mano, referencia cero).
**Criterio de aceptación:** desde la fecha efectiva del acuerdo de 2029, las líneas de la alianza registran **0 % de instrucciones redigitadas** y 100 % por mensajería estándar. Para las demás navieras, el porcentaje de instrucciones digitadas a mano es **≤ 5 %**, atribuible exclusivamente al canal puente transitorio.

> *Corrección aplicada: el criterio no comprometía meta alguna sobre el 41 % de línea base.*

---

### `RF-INT-03` — Emisión de la confirmación de carga y descarga en COARRI · Prioridad: **Alta**

**Descripción.** La solución **deberá** emitir a la naviera la confirmación de carga y descarga mediante el mensaje **COARRI**, derivada de los movimientos efectivamente registrados.

**Actor:** solución y naviera. **Precondición:** operación de nave con movimientos registrados.
**Resultado esperado:** confirmación emitida automáticamente y consistente con el registro de movimientos.
**Origen:** Decisión N° 18 · CP, num. 16.2 (COARRI: confirmación de carga y descarga) · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** el contenido del mensaje emitido corresponde **uno a uno** con los movimientos registrados de la recalada.

---

### `RF-INT-04` — Emisión de eventos compatibles mediante CODECO · Prioridad: **Alta**

**Descripción.** La solución **deberá** emitir mediante **CODECO** únicamente los eventos de gate, entrega/recepción o cambio de custodia compatibles con la especificación acordada con la naviera. La carga y descarga de nave se confirmará mediante **COARRI** y no generará un CODECO por cada movimiento de grúa.

**Actor:** solución y naviera. **Precondición:** evento compatible registrado y contrato de mensaje/versionado acordado.
**Resultado esperado:** contraparte informada sin intervención manual.
**Origen:** Decisión N° 18 · CP, num. 16.2 (CODECO: notificación de movimiento) · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** sobre una muestra de 100 eventos mixtos, solo los eventos compatibles generan CODECO; las cargas y descargas de nave generan COARRI y no CODECO. Cada mensaje conserva correlación con el evento de origen.

---

### `RF-INT-05` — Validación de integridad y origen del mensaje · Prioridad: **Crítica**

**Descripción.** La solución **deberá** validar la integridad y el origen de cada mensaje recibido antes de incorporarlo, y **no deberá** incorporar al plan ni al inventario un mensaje que no supere la validación, registrando el descarte con su motivo.

**Actor:** solución. **Precondición:** mensaje recibido de una contraparte.
**Resultado esperado:** ningún mensaje no validado modifica el plan ni el inventario.
**Origen:** Decisión N° 18, riesgo documentado de manipulación de mensajería de estiba para reruteo o robo de carga · BTT, RT-11.01 (verificación explícita de cada solicitud) · CP, Cap. 12, materia 2 (protección de instalaciones portuarias).
**Criterio de aceptación:** se inyecta un mensaje alterado y se acredita que no se incorpora, que el descarte queda registrado con su motivo, y que no produce efecto sobre el plan ni sobre el inventario.

> La adopción del estándar no basta: el campo de impacto de la Decisión N° 18 advierte que sin validación de integridad «la integración queda expuesta al riesgo de manipulación documentado en la industria».
>
> *Corrección aplicada: se retira «rechazar», verbo de interpretación múltiple.*

---

### `RF-INT-06` — Versionado explícito del mensaje por contraparte · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar y versionar explícitamente la versión de mensaje **SMDG** soportada por cada una de las 14 navieras, y **deberá** procesar cada mensaje conforme a la versión declarada para su emisor.

**Actor:** solución. **Precondición:** naviera integrada con versión declarada.
**Resultado esperado:** convivencia de versiones distintas entre contrapartes, sin ambigüedad de interpretación.
**Origen:** Decisión N° 18, que identifica la fragmentación de versiones entre contrapartes como el principal problema de implementación · BTT, RT-05.17 (versionado semántico de contratos de interfaz) · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** se procesan mensajes de dos navieras con versiones distintas y ambos se interpretan conforme a la versión declarada para cada emisor.

---

### `RF-INT-07` — Canal puente para navieras no integradas · Prioridad: **Alta**

**Descripción.** La solución **deberá** ofrecer a las navieras aún no integradas un **canal de intercambio asistido** —portal o carga de archivo, con validación previa e informe de error por cada registro inválido y **incorporación de los registros válidos**— y **no deberá** bloquear su operación mientras se integran.

**Actor:** naviera no integrada. **Precondición:** naviera registrada como contraparte y no sujeta todavía a exclusividad de mensajería estándar.
**Resultado esperado:** operación continua de las 14 navieras con distintos niveles de madurez.
**Origen:** Decisión N° 18 · CP, Cap. 1 y 2 (14 navieras, una alianza concentra el 34 % del volumen) · BTT, RT-05.22 (carga masiva con validación previa e informe de errores por registro).
**Criterio de aceptación:** una naviera no integrada completa una operación por el canal puente con un archivo que contenga registros válidos e inválidos; se emite informe de error por cada inválido y se incorporan todos los válidos.

> El campo de impacto de la Decisión N° 18 advierte que si el puente se vuelve permanente, la solución sostiene dos vías de integración indefinidamente. La revisión semestral de avance forma parte de la instancia de validación de esa decisión.
>
> **Límite 2029:** desde la fecha efectiva del acuerdo, el canal puente queda prohibido para las líneas de la alianza. Puede permanecer transitoriamente para las demás navieras.

---

### `RF-INT-08` — Identificación normalizada del contenedor conforme a ISO 6346 · Prioridad: **Crítica**

**Descripción.** La solución **deberá** identificar cada contenedor conforme a **ISO 6346**, validando su **dígito verificador** en toda captura, recepción o emisión.

**Actor:** solución. **Precondición:** código de contenedor presente en cualquier punto de entrada.
**Resultado esperado:** ningún código inválido ingresa al inventario ni a un mensaje emitido.
**Origen:** CP, Cap. 15, RT-05.23 («norma internacional de codificación e identificación de contenedores») · **CP, num. 16.2 identifica la norma como ISO 6346**, con su estructura de código y dígito verificador · CP, Cap. 4.6 (hoy se digitan 11 caracteres y «los errores de digitación existen y se descubren después»).
**Criterio de aceptación:** se inyectan códigos con dígito verificador inválido por **cada vía de entrada** —lectura óptica, mensajería, carga masiva y portal— y ninguno se incorpora.

---

### `RF-INT-09` — Entrega de hechos facturables al sistema de gestión empresarial · Prioridad: **Crítica**

**Descripción.** La solución **deberá** entregar los hechos facturables al sistema de gestión empresarial del CLIENTE para su facturación, y **no deberá** emitir documentos tributarios ni constituirse en un segundo emisor.

**Actor:** solución y sistema de gestión empresarial. **Precondición:** hechos facturables generados y validados.
**Resultado esperado:** un único emisor tributario, alimentado con hechos verificables.
**Origen:** CP, Cap. 10, restricción no negociable N° 5 · CP, Cap. 11, exclusión 1 · CP, Cap. 5 («la solución le entrega los hechos facturables; no habrá dos emisores»).
**Criterio de aceptación:** la solución no emite ningún documento tributario, y el **100 %** de los hechos facturables de un período llega al sistema de gestión empresarial con su evidencia asociada.

---

### `RF-INT-10` — Integración condicionada con autoridades y operador ferroviario · Prioridad: **Alta**

**Descripción.** La solución **deberá** integrarse con los canales electrónicos de las autoridades aduanera, fitosanitaria y sanitaria y con el operador ferroviario **donde exista una interfaz disponible**. Donde no exista, deberá operar un canal asistido registrado —`RF-INS-01` para autoridades y un mecanismo equivalente para ferrocarril—. La solución no deberá inventar interfaces ni desarrollar o sustituir sistemas de terceros.

**Actor:** autoridades, operador ferroviario y solución. **Precondición:** existencia de interfaz verificada en el levantamiento de los meses 1 a 4.
**Resultado esperado:** coordinación electrónica donde sea posible, asistida donde no, sin dejar ningún servicio fuera.
**Origen:** CP, Cap. 11, exclusión 7 · CP, num. 17.4 punto 9 («qué se hace donde no exista interfaz disponible») · Decisión N° 21 · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** para cada una de las tres autoridades y para el operador ferroviario se acredita el canal efectivamente operativo —electrónico o asistido— y la trazabilidad de la coordinación; ninguna API no confirmada se presenta como disponible.

---

### `RF-INT-11` — Correlación y trazabilidad de cada integración · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar la transacción de entrada y de salida de cada integración con un **identificador de correlación común**, que permita seguir la operación entre todos los sistemas involucrados.

**Actor:** solución. **Precondición:** integración operativa.
**Resultado esperado:** toda operación integrada es reconstruible extremo a extremo.
**Origen:** BTT, RT-05.19 · BTT, RT-05.03 · articula con `RF-CON-10`.
**Criterio de aceptación:** dado el identificador de una operación integrada, se reconstruye su recorrido completo entre la contraparte externa, la solución y el registro de destino.

---

## 4. Dominio `RF-FAC` — Hechos facturables y su evidencia

**Etapa 2 · 11 requerimientos.** Atacan el indicador más costoso en términos de relación comercial: el **62 %** de las objeciones que el terminal termina aceptando porque no logra demostrar lo que cobra.

---

### `RF-FAC-01` — Generación del hecho facturable en el instante en que ocurre · Prioridad: **Crítica**

**Descripción.** La solución **deberá** generar cada hecho facturable como **evento del sistema en el momento en que el hecho ocurre**, y **no deberá** reconstruirlo posteriormente a partir de planillas ni de reportes de turno.

**Actor:** solución. **Precondición:** ocurrencia del hecho registrada por el dominio operacional correspondiente.
**Resultado esperado:** hecho facturable con instante propio, generado sin intervención humana.
**Origen:** Decisión N° 11 · CP, Cap. 4.8 (hoy la conexión refrigerada se calcula «según la planilla de la ronda» y los movimientos adicionales «con lo que reportó el supervisor de turno») · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** sobre una muestra de **200 hechos facturables** de un período, el 100 % tiene un evento de sistema con instante propio y ninguno provino de consolidación manual.

---

### `RF-FAC-02` — Regla de negocio específica por tipo de hecho · Prioridad: **Crítica**

**Descripción.** La solución **deberá** aplicar a cada tipo de hecho facturable —transferencia, almacenaje, conexión refrigerada, movimiento adicional, pesaje, inspección, uso de zona de carga peligrosa y servicio especial— una **regla de negocio propia, parametrizable y versionada**, y **deberá** dejar trazable qué versión de la regla se aplicó a cada hecho.

**Actor:** solución. **Precondición:** hecho generado y tipificado.
**Resultado esperado:** cada hecho valorizado por una regla identificable y reproducible.
**Origen:** Decisión N° 11 · CP, Cap. 4.8, que enumera los ocho conceptos que el terminal cobra · **BTT, RT-16.02** (Obligatorio: parametrización con versionado y registro de quién cambió qué) · BTT, RT-16.14 como refuerzo, **declarado Deseable en el BTT** · BTT, RT-16.04.
**Criterio de aceptación:** se modifica la versión de una regla y los hechos anteriores conservan la versión con que fueron calculados; se recupera para un hecho cualquiera la versión de regla aplicada.

> *Corrección aplicada: la obligación se apoyaba en RT-16.14, que el BTT etiqueta como **Deseable**. Se ancla en RT-16.02, que es Obligatorio.*

---

### `RF-FAC-03` — Cálculo de días de almacenaje · Prioridad: **Alta**

**Descripción.** La solución **deberá** calcular los días de almacenaje conforme a **RN-04** —días corridos, contados desde el día siguiente al ingreso, con 3 días libres y corte a las 23:59— a partir de los eventos registrados de ingreso y de salida, y **deberá** exponer al cliente ambos instantes junto con el cargo.

**Actor:** solución. **Precondición:** eventos de ingreso y salida registrados.
**Resultado esperado:** cargo de almacenaje con sus dos instantes de origen visibles y su método reproducible.
**Origen:** Decisión N° 11 · **RN-04** fija el método · CP, Cap. 4.8 («las fechas del sistema no siempre coinciden con lo que el cliente cree») · articula con `RF-GAT-11`.

**Ejemplos numéricos del cálculo:**

> **Ejemplo A — dentro del mismo mes.** Descargado el 4 de marzo a las 08:30; retirado el 11 de marzo a las 16:00.
> Conteo desde el 5 de marzo. Días transcurridos hasta el 11: **7**. Días libres: 3. **Días facturables: 4** (8, 9, 10 y 11 de marzo).
>
> **Ejemplo B — cruzando el cambio de mes.** Descargado el 27 de marzo a las 22:15; retirado el 3 de abril a las 09:00.
> Conteo desde el 28 de marzo. Días transcurridos hasta el 3 de abril: **7** (28, 29, 30 y 31 de marzo; 1, 2 y 3 de abril). Días libres: 3. **Días facturables: 4** (31 de marzo; 1, 2 y 3 de abril).
>
> La hora de ingreso y de retiro no altera el conteo, y el cambio de mes no reinicia el cómputo.

**Criterio de aceptación:** se inyectan los dos casos anteriores y el cálculo devuelve 4 días facturables en ambos; se selecciona un cargo y se recuperan los dos eventos de barrera que lo determinan con sus marcas de tiempo.

> *Corrección aplicada: se incorpora el método de RN-04 y los dos ejemplos numéricos exigidos.*

---

### `RF-FAC-04` — Registro de movimientos adicionales · Prioridad: **Alta**

**Descripción.** La solución **deberá** derivar los movimientos adicionales facturables del registro de movimientos por telemetría, y **no deberá** admitir su declaración por el supervisor de turno.

**Actor:** solución. **Precondición:** movimientos registrados conforme a `RF-PAT-05`.
**Resultado esperado:** cargo por movimiento adicional respaldado por el movimiento físico que lo originó.
**Origen:** Decisión N° 11 · Decisión N° 15 · CP, Cap. 4.8 (hoy se calculan «con lo que reportó el supervisor de turno»).
**Criterio de aceptación:** se contrasta una muestra de **100 movimientos adicionales facturados** contra los movimientos registrados por telemetría, con correspondencia **uno a uno** en los 100.

---

### `RF-FAC-05` — Hechos facturables de pesaje, inspección y carga peligrosa · Prioridad: **Alta**

**Descripción.** La solución **deberá** generar el hecho facturable del pesaje a partir de la captura de la báscula, el de la inspección a partir de la cita de inspección atendida, y el de uso de zona de carga peligrosa a partir de la asignación de posición en esa zona.

**Actor:** solución. **Precondición:** el evento operacional correspondiente registrado.
**Resultado esperado:** los tres conceptos respaldados por su evento de origen y no por declaración.
**Origen:** CP, Cap. 4.8, que los enumera entre los conceptos cobrados · articula con `RF-GAT-08`, `RF-INS-05` y `RF-PAT-07`.
**Criterio de aceptación:** para cada uno de los tres conceptos se recupera, desde el cargo, el evento operacional que lo originó.

---

### `RF-FAC-06` — Evidencia asociada e inalterable · Prioridad: **Crítica**

**Descripción.** La solución **deberá** asociar a cada hecho facturable la evidencia que lo respalda —eventos, mediciones, series o lecturas— y **deberá** conservarla de modo que ningún perfil, incluido el administrador de la plataforma, pueda modificarla.

**Actor:** solución. **Precondición:** hecho facturable generado.
**Resultado esperado:** evidencia oponible ante una objeción del cliente.
**Origen:** Decisión N° 11 · **BTT, RT-16.07** (auditoría inalterable, no modificable por ningún perfil, incluido el administrador de la plataforma) · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** se intenta modificar la evidencia de un hecho facturable con perfil de administrador y el sistema no lo permite; el intento queda registrado en la auditoría.

> **Distinción con `RF-FAC-07`.** La **evidencia** es inmutable (RT-16.07). El **hecho facturable** sí admite corrección, pero únicamente por compensación, y esa corrección se audita con valores anteriores y posteriores (RT-16.06). No son exigencias contradictorias: operan sobre objetos distintos.

---

### `RF-FAC-07` — Prohibición de creación y edición manual · Prioridad: **Crítica**

**Descripción.** La solución **no deberá** permitir la creación ni la edición manual de un hecho facturable. Toda corrección **deberá** ejecutarse como **hecho compensatorio nuevo**, con su motivo, su autor y su vínculo al hecho corregido.

**Actor:** solución. **Precondición:** hecho facturable existente.
**Resultado esperado:** la serie de hechos es acumulativa y auditable; nada se sobrescribe.
**Origen:** Decisión N° 11 (sin intervención manual previa a la facturación) · **BTT, RT-16.06** (registro con valores anteriores y posteriores) · CP, Cap. 10, restricción no negociable N° 14.
**Criterio de aceptación:** se intenta editar un hecho facturable y el sistema no lo permite; se ejecuta una corrección y queda registrada como hecho compensatorio vinculado al original, con motivo y autor.

---

### `RF-FAC-08` — Presentación y trazabilidad de la objeción · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir al cliente presentar una objeción de facturación por autoservicio, indicando el cargo objetado y su motivo, y **deberá** mantener el estado de la objeción hasta su cierre.

**Actor:** exportador, importador o agencia de aduana. **Precondición:** cargo emitido y persona usuaria autorizada.
**Resultado esperado:** objeción registrada en el sistema, con estado y responsable, sin correo ni planilla.
**Origen:** CP, Cap. 4.8 y Anexo A (hoy las objeciones viajan por correo con «seguimiento en planilla») · CP, Cap. 5 · BTT, RT-16.11 (flujo con estados, responsables, plazos y escalamiento) · supuesto de alcance del autoservicio, trámite 4.
**Criterio de aceptación:** un cliente presenta una objeción por autoservicio y el caso queda con estado, responsable asignado y plazo, sin ningún intercambio por correo.

---

### `RF-FAC-09` — Resolución de la objeción con la evidencia · Prioridad: **Crítica**

**Descripción.** La solución **deberá** presentar al cliente y al analista, junto a la objeción, la **evidencia completa del hecho objetado**, y **deberá** registrar el fundamento de la resolución, sea de aceptación o de rechazo.

**Actor:** analista de facturación y cliente. **Precondición:** objeción presentada.
**Resultado esperado:** resolución fundada en evidencia verificable, no en la imposibilidad de demostrar.
**Origen:** CP, 7.3 (62 % de las objeciones se acepta «porque el terminal no logra demostrar el hecho que factura», referencia cero) · Decisión N° 11 · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** sobre las objeciones de un período, el porcentaje aceptado **por falta de evidencia** es **cero**, y cada resolución consigna su fundamento.

---

### `RF-FAC-10` — Conciliación diaria de hechos facturables · Prioridad: **Crítica**

**Descripción.** Mientras el dominio esté en convivencia, la solución **deberá** conciliar al cierre de cada día los hechos facturables y su evidencia contra el registro del sistema de 2012, y **no deberá** admitir ninguna diferencia no explicada al cierre diario.

**Actor:** solución y analista de facturación. **Precondición:** dominio en convivencia con escritura dual activa.
**Resultado esperado:** cero diferencias no explicadas al cierre diario, con ventana de investigación de **24 horas**.
**Origen:** Decisión N° 1, umbrales de conciliación: hechos facturables con umbral cero por su implicancia económica y contractual · CP, 17.6 punto 2 · articula con `RF-CON-05` y con la definición operativa de `RF-CON-06`.
**Criterio de aceptación:** durante siete días consecutivos el informe de conciliación diaria cierra con cero diferencias no explicadas, o con cada diferencia clasificada y explicada dentro de las 24 horas.

---

### `RF-FAC-11` — Recuperación de la evidencia durante el plazo de retención · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir recuperar la evidencia de cualquier hecho facturable durante los **seis años** de su plazo de retención, con su integridad verificable.

**Actor:** solución, CLIENTE y cliente externo. **Precondición:** hecho facturable generado con su evidencia.
**Resultado esperado:** evidencia recuperable y verificable durante todo el plazo exigido.
**Origen:** **CP, Cap. 15, RT-05.10** (evidencia de hechos facturables: 6 años) · CP, Cap. 15, RT-05.15 (migrar 6 años de hechos facturables y su evidencia).
**Criterio de aceptación:** se recupera la evidencia de un hecho facturable de **seis años de antigüedad** y se verifica su integridad.

> *Corrección aplicada: se acentúa la conducta de **recuperación**, que es lo funcional; la retención en sí es atributo de calidad.*

---

## 5. Dominio `RF-POR` — Portal y autoservicio de clientes

**Etapa 2 · 8 requerimientos propios**, más cuatro trámites realizados en otros dominios (sección 8).

---

### `RF-POR-01` — Capa pública sin autenticación · Prioridad: **Alta**

**Descripción.** La solución **deberá** publicar sin autenticación: (1) un estado mínimo y seguro del contenedor consultado, sin revelar posición exacta, contenido, ruta ni información comercial; (2) las condiciones vigentes de acceso al terminal; y (3) la congestión del gate en tiempo real y la disponibilidad de franjas de cita. La capa pública estará disponible **en español y en inglés**, con los mismos estándares de accesibilidad y desempeño que el resto de la plataforma.

**Actor:** cualquier persona. **Precondición:** ninguna.
**Resultado esperado:** información de estado y acceso disponible antes del viaje, sin exponer datos sensibles de la carga.
**Origen:** BTT, RT-16.31 (portal público) · **CP, Cap. 15, RT-16.30** (portal público del caso, en español e inglés) · CP, Cap. 18, criterio 2 · articula con `RF-GAT-13`.
**Criterio de aceptación:** se accede sin credenciales en ambos idiomas a los tres conjuntos de información; el estado refleja el evento de origen dentro de `RNF-DES-06` y una prueba de exposición confirma que no revela posición exacta, contenido, ruta ni información comercial.

> *Corrección aplicada: el requerimiento omitía la exigencia bilingüe que el CP incluye para la capa pública.*

---

### `RF-POR-02` — Registro y recuperación de acceso autoservidos · Prioridad: **Crítica**

**Descripción.** La solución **deberá** permitir a las personas usuarias externas —navieras, agencias de aduana, exportadores, importadores, transportistas, autoridades, concedente y operador ferroviario— registrarse, verificar su identidad y recuperar su acceso de forma autoservida, con **verificación de identidad conforme a BTT, RT-12.01** y **segundo factor para todo acceso originado fuera de la red corporativa conforme a BTT, RT-12.03**.

**Actor:** persona usuaria externa. **Precondición:** ninguna.
**Resultado esperado:** alta y recuperación sin intervención del terminal, con identidad verificada.
**Origen:** BTT, RT-12.12 · **CP, Cap. 15, RT-12.12**, que enumera las contrapartes externas del caso, incluidos los inspectores de las tres autoridades · CP, Cap. 2 (14 navieras, 210 agencias, ~1.400 exportadores e importadores, 380 empresas de transporte).
**Criterio de aceptación:** una persona usuaria externa completa el ciclo de registro, verificación de identidad y recuperación de acceso sin contacto con el terminal, con segundo factor exigido.

> *Corrección aplicada: se retira «segura» —palabra subjetiva sin métrica, heredada del texto del RT— y se sustituye por los controles concretos.*

---

### `RF-POR-03` — Consulta autenticada de estado y posición · Prioridad: **Crítica**

**Descripción.** La solución **deberá** entregar a la persona usuaria externa autenticada el estado y la posición reales de su carga, y **no deberá** limitarse a la consulta por número de contenedor sin autenticación.

**Actor:** exportador, importador, agencia o transportista. **Precondición:** persona usuaria autenticada con carga asociada.
**Resultado esperado:** estado real, no un dato de un día de antigüedad.
**Origen:** CP, Cap. 5 (el portal de 2016 «sin autenticación, con datos actualizados una vez al día», se reemplaza) · CP, Cap. 15, RT-16.30 · CP, Cap. 18, criterio 15 · supuesto de alcance del autoservicio, trámite 1.
**Criterio de aceptación:** el estado publicado refleja el evento origen dentro del umbral de **RNF-DES-06**, y la consulta exige autenticación.

---

### `RF-POR-04` — Segregación de visibilidad por contraparte · Prioridad: **Crítica**

**Descripción.** La solución **deberá** limitar la información visible a cada persona usuaria externa a la que le corresponde por su relación con la carga, y **no deberá** exponer información comercial de un cliente a otro.

**Actor:** solución. **Precondición:** persona usuaria autenticada con rol y contraparte determinados.
**Resultado esperado:** ninguna contraparte accede a información de otra.
**Origen:** **CP, Cap. 15, RT-11.10** (cifrado de información comercial sensible: tarifas y volúmenes negociados) · BTT, RT-12.05 · **CP, Cap. 15, RT-16.09**, que añade que «la consulta de la ubicación de un contenedor determinado es información sensible» · articula con RNF-SEG-05 y RNF-SEG-09.
**Criterio de aceptación:** se intenta acceder a la carga de una contraparte distinta y el sistema deniega el acceso; el intento queda registrado en la auditoría de consultas.

---

### `RF-POR-05` — Presentación de objeción de facturación en línea · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir al cliente descargar la evidencia de un hecho facturable y presentar su objeción desde el portal, sin recurrir al correo ni al mostrador.

**Actor:** exportador, importador o agencia de aduana. **Precondición:** cargo emitido con evidencia asociada.
**Resultado esperado:** ciclo de objeción íntegramente autoservido.
**Origen:** supuesto de alcance del autoservicio, trámite 4 · CP, Cap. 4.8 · articula con `RF-FAC-08` y `RF-FAC-09`.
**Criterio de aceptación:** un cliente descarga la evidencia y presenta la objeción por el portal, y el caso queda con estado y responsable sin ningún intercambio por correo.

---

### `RF-POR-06` — Coordinación y estado de cita de inspección · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir a la agencia de aduana y al inspector consultar y coordinar el estado de una cita de inspección desde el portal.

**Actor:** agencia de aduana e inspector de autoridad. **Precondición:** cita de inspección registrada.
**Resultado esperado:** coordinación visible para las tres partes, sin radio ni teléfono.
**Origen:** Decisión N° 21 · CP, Cap. 15, RT-12.12 (los inspectores son personas usuarias externas) · supuesto de alcance del autoservicio, trámite 6 · articula con el dominio `RF-INS`.
**Criterio de aceptación:** un inspector consulta el estado de una cita y confirma su asistencia desde el portal, y la coordinación queda registrada.

---

### `RF-POR-07` — Selección persistente de idioma · Prioridad: **Media**

**Descripción.** La solución **deberá** permitir a la persona usuaria seleccionar el idioma de la interfaz entre español e inglés, y **deberá** conservar esa selección entre sesiones.

**Actor:** persona usuaria interna y externa. **Precondición:** persona usuaria identificada.
**Resultado esperado:** la preferencia de idioma persiste sin volver a declararse en cada ingreso.
**Origen:** CP, Cap. 10, restricción no negociable N° 13 · CP, Cap. 15, RT-13.12 · BTT, RT-13.12. **La cobertura bilingüe del catálogo de pantallas y plantillas queda en RNF-IDI-01**, que conserva el umbral del 100 % y su método de auditoría.
**Criterio de aceptación:** una persona usuaria selecciona inglés, cierra la sesión y vuelve a ingresar; la interfaz se presenta en inglés sin nueva declaración.

> **Resuelto.** La Célula 2 confirmó el reparto: el RF queda reformulado como la única conducta que ningún RNF cubre —la **selección persistente de idioma entre sesiones**— y la **cobertura bilingüe del catálogo de pantallas y plantillas**, con su umbral del 100 % y su método de auditoría, queda como fuente única en **RNF-IDI-01**, que es el que acredita el T-12. Esta redacción ya refleja el acuerdo. El multiidioma es una de las nueve categorías cerradas de RNF del CP, Cap. 17.1.

---

### `RF-POR-08` — Autoatención de las consultas de mayor frecuencia · Prioridad: **Alta**

**Descripción.** La solución **deberá** resolver por autoservicio los **siete trámites declarados** en el supuesto de alcance, y **deberá** medir el desvío del canal telefónico y presencial hacia el portal.

**Actor:** persona usuaria externa. **Precondición:** persona usuaria registrada.
**Resultado esperado:** el contacto telefónico deja de ser necesario para los trámites declarados, y el desvío es medible.
**Origen:** BTT, RT-16.32 (autoatención de las consultas de mayor frecuencia) · **BTT, RT-16.33** (el PROPONENTE estimará la reducción esperada del volumen de atención asistida y comprometerá el indicador) · CP, Cap. 18, criterio 15 · CP, Cap. 9.8 · supuesto de alcance del autoservicio.
**Criterio de aceptación:** se mide el volumen de contactos telefónicos y presenciales **por tipo de trámite** antes y después de la puesta en marcha, sobre los siete trámites declarados.

> El supuesto de alcance advierte que si las consultas de mayor frecuencia reales no están entre las siete declaradas, la solución cumple la letra de RT-16.32 sin descargar el mostrador. La medición del desvío es lo que permite detectar ese error a tiempo.
>
> *Corrección aplicada: la obligación de medir el desvío corresponde a RT-16.33, que no estaba citado.*

---

## 6. Dominio `RF-INS` — Inspecciones y coordinación con autoridades

**Etapa 2 · 7 requerimientos**, apoyados en la programación anticipada de remociones que ya existe desde la Etapa 1 (`RF-PAT-11`). Materializa la **Decisión N° 21**.

---

### `RF-INS-01` — Recepción normalizada de la selección · Prioridad: **Alta**

**Descripción.** La solución **deberá** recibir la selección de contenedores para inspección de cada autoridad por el canal que esa autoridad tenga disponible, y **deberá** normalizarla a un **evento interno único de cita de inspección** con autoridad, contenedor, fecha, hora y tipo.

**Actor:** autoridad aduanera, fitosanitaria o sanitaria. **Precondición:** canal de la autoridad identificado en el levantamiento.
**Resultado esperado:** las tres autoridades producen el mismo evento interno, cualquiera sea su canal.
**Origen:** Decisión N° 21 · CP, Cap. 4.7 · CP, Cap. 11, exclusión 7 · CP, Cap. 5 (el «control de inspecciones» debe dejar de vivir en correo y planillas) · articula con `RF-INT-10`.
**Criterio de aceptación:** se recibe una selección por cada uno de los **tres canales operativos** y las tres generan un evento interno equivalente.

---

### `RF-INS-02` — Registro de la cita con hora acordada · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar la hora acordada y el lugar de cada inspección, y **deberá** mantenerla como compromiso con fecha cierta frente a un tercero con potestad.

**Actor:** solución y área de documentación. **Precondición:** selección recibida.
**Resultado esperado:** compromiso registrado, no una solicitud informal.
**Origen:** CP, Cap. 4.7 («a la hora acordada, el contenedor debe estar en la zona de inspección, abierto, con el inspector presente») · CP, Cap. 3 (zona de inspección) · CP, Anexo B.1 (ventana habitual 08:00 a 18:00).
**Criterio de aceptación:** el **100 %** de las citas registradas presenta hora acordada y lugar, y queda visible para el patio y para la autoridad.

---

### `RF-INS-03` — Reserva de disponibilidad y programación de la remoción · Prioridad: **Crítica**

**Descripción.** Al registrar la cita, la solución **deberá** evaluar la accesibilidad del contenedor en su posición actual y, cuando no sea accesible, **deberá** programar anticipadamente las remociones necesarias con la **holgura parametrizada vigente** antes de la hora acordada.

**Actor:** solución. **Precondición:** cita registrada y posición del contenedor conocida.
**Resultado esperado:** el contenedor está accesible cuando el inspector llega, sin remoción improvisada.
**Origen:** **Decisión N° 21**, núcleo de la decisión · CP, Cap. 4.7 (el atraso ocurre «porque estaba abajo de otros tres **y la remoción no se programó**») · BTT, RT-16.02 (la holgura es parámetro configurable) · articula con `RF-PAT-11`.
**Criterio de aceptación:** sobre una muestra de **50 citas**, la remoción necesaria se programó al momento de agendar y se ejecutó antes de la hora acordada en el **≥ 90 %** de los casos.

> **Holgura: parámetro configurable, valor inicial 4 horas.** El valor definitivo depende del plazo de aviso de cada autoridad, dato que el CLIENTE posee y no declaró, y se fija en el levantamiento de los meses 1 a 4.

---

### `RF-INS-04` — Alerta de riesgo de incumplimiento · Prioridad: **Alta**

**Descripción.** La solución **deberá** alertar cuando el tiempo restante hasta la hora acordada sea insuficiente para ejecutar la remoción programada, y **deberá** escalar a la supervisión de patio.

**Actor:** solución y supervisor de patio. **Precondición:** cita con remoción pendiente y plazo comprometido.
**Resultado esperado:** el incumplimiento se anticipa en vez de constatarse.
**Origen:** Decisión N° 21, campo de impacto (el riesgo residual son las citas cuyo aviso llega con menos anticipación que el tiempo de remoción) · BTT, RT-16.11 (escalamiento automático por vencimiento) · BTT, RT-16.02.
**Criterio de aceptación:** se agenda una cita con plazo insuficiente y la alerta se emite y escala **al menos con la holgura parametrizada vigente** de anticipación respecto de la hora acordada.

> *Corrección aplicada: el criterio anterior decía «antes de la hora acordada», que es trivialmente cierto y por tanto no verificable.*

---

### `RF-INS-05` — Registro de la atención de la inspección · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar el inicio y el término de cada inspección atendida, con la autoridad interviniente y su resultado.

**Actor:** inspector y área de documentación. **Precondición:** inspección iniciada.
**Resultado esperado:** trazabilidad completa de la atención, base del acta y del hecho facturable.
**Origen:** Decisión N° 21 · CP, Cap. 12, materias 4 y 7 · CP, Cap. 4.8 (la inspección es concepto facturable) · articula con `RF-FAC-05`.
**Criterio de aceptación:** para una inspección cerrada se recupera su instante de inicio, su instante de término, la autoridad interviniente y su resultado.

---

### `RF-INS-06` — Acta de inspección con firma electrónica · Prioridad: **Alta**

**Descripción.** La solución **deberá** generar el acta de la inspección y **deberá** permitir su firma electrónica conforme a la modalidad que la normativa admita, verificando la validez del certificado al momento de la firma y conservando la evidencia que permita verificar el documento tras el vencimiento del certificado.

**Actor:** inspector y representante del terminal. **Precondición:** inspección atendida y registrada.
**Resultado esperado:** acta firmada y conservable como evidencia.
**Origen:** **CP, Cap. 15, RT-16.14** exige firma en «las actas de inspección conjunta» — *nótese que en el BTT el código RT-16.14 corresponde a otra materia (motor de reglas, Deseable); la obligación de firma proviene del CP* · **BTT, RT-16.17 y RT-16.18** aportan la conducta de firma electrónica y de sello de tiempo.
**Criterio de aceptación:** se genera y firma un acta, verificando la validez del certificado al momento de la firma y la conservación de la evidencia de firma.

> Este escenario reutiliza la capacidad transversal de `RF-FIR-01`; no crea un motor de firma independiente para inspecciones.

> **Advertencia.** La expresión «acta de inspección conjunta» **no está definida en ninguna parte del caso**. Este requerimiento se redacta bajo la interpretación más exigente adoptada en el **Supuesto N** de `../02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`: acta de toda inspección en que concurren la autoridad y el terminal. Si la lectura correcta fuera la restringida, el error sería **por exceso de cobertura** y no comprometería cumplimiento.

---

### `RF-INS-07` — Medición del cumplimiento de la hora acordada · Prioridad: **Crítica**

**Descripción.** La solución **deberá** medir el porcentaje de inspecciones atendidas a la hora acordada y **deberá** clasificar cada incumplimiento por su causa, distinguiendo las causas bajo control del terminal de las atribuibles al plazo de aviso de la autoridad.

**Actor:** solución y jefatura de operaciones. **Precondición:** citas registradas y atenciones registradas.
**Resultado esperado:** indicador comparable contra la línea base del 28 % y contra la meta comprometida.
**Origen:** CP, Cap. 18, criterio 10 · CP, 7.2 (28 % de inspecciones atrasadas) · **meta comprometida: ≤ 12 %, condicionada** a que el plazo de aviso de cada autoridad resulte compatible con el tiempo de ejecución de la remoción anticipada.
**Criterio de aceptación:** sobre las inspecciones de un período se calcula el porcentaje atendido a la hora acordada, contrastándolo con la meta de **≤ 12 %** de atraso, y se descompone el incumplimiento por causa.

> *Corrección aplicada: la meta baja de ≤ 8 % a ≤ 12 %. No existe literatura arbitrada que mida este indicador, y Klar et al. (2024) documentan que cumplir la agenda de inspecciones consume capacidad de grúa que compite con la meta de remociones. Comprometer ≤ 8 % sin evidencia y con ese trade-off era comprometer lo indemostrable.*

---

## 7. Dominio `RF-EMI` — Emisiones y consumo energético

**Etapa 2 · 6 requerimientos**, con captura de datos iniciada antes para constituir la serie histórica.

---

### `RF-EMI-01` — Captura de consumo de los equipos diésel · Prioridad: **Alta**

**Descripción.** La solución **deberá** capturar el consumo de combustible de cada uno de los **16 equipos diésel** mediante su instrumentación, asociándolo al equipo y al período.

**Actor:** solución. **Precondición:** equipo instrumentado.
**Resultado esperado:** consumo individual por equipo, no prorrateado.
**Origen:** Decisión N° 17 · CP, Cap. 2.3 (18 grúas de patio: 16 diésel y 2 eléctricas incorporadas en 2023) · CP, Cap. 11, exclusión 5.
**Criterio de aceptación:** la medición instrumentada acumulada reconcilia con el combustible facturado a la empresa **dentro de ±3 %**, sobre un período de **3 meses**.

> *Corrección aplicada: el criterio no declaraba período ni tolerancia de reconciliación, y por tanto no era ejecutable.*

---

### `RF-EMI-02` — Medición de consumo de los equipos eléctricos · Prioridad: **Alta**

**Descripción.** La solución **deberá** medir directamente el consumo energético de los **2 equipos eléctricos**, y **no deberá** prorratear el consumo entre equipos de tecnologías distintas.

**Actor:** solución. **Precondición:** equipo eléctrico con medición instalada.
**Resultado esperado:** los dos grupos tecnológicos quedan distinguidos en el cálculo.
**Origen:** Decisión N° 17 · CP, Cap. 11, exclusión 5 («sí considerar que dos equipos ya son eléctricos y que la medición de emisiones debe distinguirlos») · CP, 16.1 decisión 17 (sin medición individual el indicador «se construye sobre un prorrateo objetable por un verificador externo»).
**Criterio de aceptación:** el cálculo distingue ambos grupos, y **ningún** consumo se asigna por prorrateo uniforme entre tecnologías.

---

### `RF-EMI-03` — Cálculo de emisiones por contenedor movilizado · Prioridad: **Crítica**

**Descripción.** La solución **deberá** calcular las emisiones de gases de efecto invernadero por contenedor movilizado aplicando **ISO 14083:2023**, implementada operativamente mediante el **GLEC Framework v3.2**, con los alcances 1, 2 y 3 considerados explicitados, en condiciones de ser verificada bajo **ISO 14064-3**.

**Actor:** solución. **Precondición:** consumos capturados y movimientos registrados.
**Resultado esperado:** emisión por contenedor, calculada con método declarado y no estimada.
**Origen:** **Decisión N° 16**, que fija la jerarquía normativa: ISO 14083 como norma de cuantificación, GLEC v3.2 como marco de implementación, ISO 14064-3 para la verificación · CP, Cap. 18, criterio 16 · CP, Cap. 12, materia 10 · CP, num. 16.2 · CP, 7.3 (emisiones por contenedor: no se mide) · articula con RNF-CUM-09.

**Ejemplos numéricos del cálculo:**

> **Ejemplo A — contenedor movido por equipo diésel.** Consumo atribuido al movimiento según la metodología declarada, multiplicado por el factor de emisión del combustible correspondiente conforme a GLEC v3.2, con el alcance 1 declarado.
>
> **Ejemplo B — contenedor movido por equipo eléctrico.** Consumo en kWh atribuido al movimiento, multiplicado por el factor de emisión de la red eléctrica aplicable, con el alcance 2 declarado.
>
> Los dos ejemplos se resuelven con valores numéricos concretos al fijar los factores de emisión vigentes, junto al registro de reglas de negocio. Ambos deben explicitar el factor aplicado y su fuente.

**Criterio de aceptación:** se audita una muestra de **50 cálculos** contra la metodología declarada, verificando la correcta aplicación de los factores y de los alcances, y que cada cálculo explicita el factor empleado y su fuente.

> *Correcciones aplicadas: el requerimiento decía «la metodología declarada» sin nombrarla, perdiendo el trabajo que la Decisión N° 16 ya había hecho al determinar la jerarquía normativa correcta —incluso corrigiendo una versión anterior que la tenía invertida—. Se agregan los ejemplos numéricos exigidos, con la limitación declarada de que sus valores se completan al fijar los factores vigentes.*

---

### `RF-EMI-04` — Trazabilidad del cálculo hasta el dato de origen · Prioridad: **Crítica**

**Descripción.** La solución **deberá** permitir descender desde la emisión calculada de un contenedor hasta los **datos de consumo y de movimiento que la originan**.

**Actor:** solución, CLIENTE y verificador externo. **Precondición:** emisión calculada.
**Resultado esperado:** cálculo auditable por un tercero, no una cifra agregada.
**Origen:** CP, Cap. 9.10 («datos trazables hasta su origen y en condiciones de ser verificada por un tercero») · CP, Cap. 18, criterio 16 · BTT, RT-05.26.
**Criterio de aceptación:** se selecciona la emisión de un contenedor y se recuperan los consumos y movimientos que la componen, con sus instantes.

---

### `RF-EMI-05` — Serie histórica suficiente para el reporte verificado · Prioridad: **Crítica**

**Descripción.** La solución **deberá** acumular sin interrupciones la serie histórica de emisiones desde el **mes 1** y someter tempranamente al verificador independiente el método, los límites y el período histórico requerido. La suficiencia de la serie deberá quedar acordada y documentada antes de comprometer el primer reporte verificado; no se atribuye al CLIENTE un umbral fijo de 24 meses que el caso no establece.

**Actor:** solución. **Precondición:** captura de consumos iniciada.
**Resultado esperado:** serie continua y suficiente antes del hito externo de 2029.
**Origen:** Decisión N° 16, instancia de validación · CP, Cap. 1 (la alianza naviera exige un reporte verificado de emisiones a partir de 2029) · objeción de la gerenta comercial incorporada como programa indivisible. Este requisito adelanta la captura y validación de la serie que habilita la condición de emisiones; `RF-EMI-06` acredita su cumplimiento final antes del hito 2029.
**Criterio de aceptación:** se acredita captura continua desde el mes 1, acta temprana del verificador sobre método, límites y período suficiente, pre-verificación y disponibilidad de toda la historia efectivamente generada antes del primer informe.

> *Corrección MC-25: se retira el umbral propio de 24 meses porque el caso no lo fija y el calendario supuesto no lo garantiza. La suficiencia pasa a ser una decisión metodológica trazable acordada con el verificador, con toda la serie real disponible como respaldo.*
>
> La gerenta comercial objetó en CP, 13.1 que las tres condiciones de la alianza naviera quedaron al final del plan y no llegan a 2029. Este requerimiento materializa la respuesta.

---

### `RF-EMI-06` — Obtención del reporte verificado por tercero · Prioridad: **Crítica**

**Descripción.** La solución **deberá** exportar el reporte de emisiones y sus datos de respaldo en formato abierto y documentado, sin intervención del ADJUDICATARIO, y el proyecto deberá obtener un **informe efectivamente verificado por un tercero independiente** antes de la fecha de exigibilidad del acuerdo de 2029.

**Actor:** CLIENTE y verificador externo. **Precondición:** serie histórica disponible.
**Resultado esperado:** paquete autosuficiente y dictamen de verificación emitido, no solo información potencialmente verificable.
**Origen:** Decisión N° 16 · **CP, Cap. 15, RT-05.06** (exportación en formatos abiertos, sin intervención del ADJUDICATARIO) · CP, Cap. 18, criterio 16.
**Criterio de aceptación:** el paquete exportado contiene la serie, consumos, movimientos, factores y fuentes, se genera sin intervención de Terabyte y un tercero independiente emite el informe de verificación antes del hito 2029.

> *Corrección MC-25: la exportación sigue siendo verificable como función del sistema, pero no sustituye el resultado contractual de obtener la verificación efectiva.*

---

## 8. Dominio `RF-APP` — Aplicación móvil operacional

### `RF-APP-01` — Aplicación instalable con cuatro perfiles · Prioridad: **Crítica**

**Descripción.** La solución **deberá** entregar una única aplicación móvil instalable —nativa, híbrida o PWA justificada— con capacidades diferenciadas para: supervisor en terreno; ronda reefer y mantenimiento; protección y prevención; y conductor externo. Los tres perfiles internos deberán operar sin conexión mediante almacenamiento local cifrado, cola de pendientes, sincronización idempotente, resolución determinista de conflictos e indicación visible del estado de conexión. No se crearán cuatro aplicaciones independientes.

**Actor:** supervisor, personal de ronda reefer/mantenimiento, protección/prevención y conductor externo.
**Precondición:** dispositivo enrolado o sesión autenticada conforme a las políticas del perfil.
**Resultado esperado:** experiencia móvil común sobre las mismas capacidades de negocio, con continuidad offline interna y acceso acotado para el conductor.
**Origen:** CP, Cap. 15, RT-17.01 — aplicación móvil con cuatro perfiles y operación sin conexión de perfiles internos · MC-01 del Maestro de correcciones.

**Criterio de aceptación por perfil:**

| Perfil | Escenario verificable | Etapa |
|---|---|:---:|
| Supervisor en terreno | consulta y registra una tarea durante desconexión; sincroniza sin duplicados | 1 |
| Ronda reefer y mantenimiento | recibe/consulta alarmas y registra atención durante desconexión | 1 |
| Protección y prevención | consulta habilitación y registra una actuación autorizada durante desconexión | 1 |
| Conductor externo | consulta cita, documentación y posición en fila con permisos acotados | 2 |

En los tres escenarios internos se verifica cifrado local, expiración o borrado seguro, estado visible de sincronización y ausencia de pérdida tras reconectar.

---

## 9. Dominio `RF-FIR` — Firma electrónica transversal

### `RF-FIR-01` — Firma y evidencia para los cuatro actos obligatorios · Prioridad: **Crítica**

**Descripción.** La solución **deberá** aplicar una capacidad compartida de firma electrónica y evidencia a: aceptación de instrucciones de embarque; conformidad de recepción y entrega de contenedores; actas de inspección conjunta; y conformidad de hechos facturables. Cada acto conservará firmante, certificado, fecha, hora, integridad del documento y sello o evidencia que permita verificarlo después del vencimiento del certificado.

**Actor:** contraparte autorizada según el acto y representante del terminal.
**Precondición:** acto generado y personas firmantes autenticadas y autorizadas.
**Resultado esperado:** los cuatro actos quedan formalizados mediante un mecanismo único y verificable, sin componentes de firma duplicados por dominio.
**Origen:** CP, Cap. 15, RT-16.14 — firma electrónica en cuatro actos · BTT, RT-16.17 y RT-16.18 — firma y sello de tiempo · MC-05 del Maestro de correcciones.
**Criterio de aceptación:** se ejecuta un caso de cada uno de los cuatro actos y se verifica identidad, autorización, integridad, instante y validación posterior de la evidencia. `RF-INS-06` materializa el escenario de inspección y los restantes dominios reutilizan esta capacidad.

---

## 10. Correspondencia del portal y trámites en otros dominios

### 10.1 Correspondencia completa con CP, Cap. 15, RT-16.30

| Elemento exigido | Acceso | Cobertura funcional |
|---|---|---|
| Estado seguro del contenedor | Público | `RF-POR-01` |
| Condiciones de acceso | Público | `RF-POR-01` |
| Congestión del gate en tiempo real | Público | `RF-POR-01` · `RF-GAT-13` |
| Español e inglés | Público y autenticado | `RF-POR-01`, `RF-POR-07`, `RNF-IDI-01` |
| Citas | Autenticado | `RF-GAT-01` |
| Validación anticipada de documentación | Autenticado | `RF-GAT-03` |
| Hechos facturables con evidencia | Autenticado | `RF-FAC-06` · `RF-POR-05` |
| Objeción de facturación | Autenticado | `RF-POR-05` · `RF-FAC-08/09` |
| Curva de temperatura propia | Autenticado | `RF-REF-12` |

### 10.2 Trámites del autoservicio realizados en otros dominios

| Trámite del supuesto de alcance | Requerimiento que lo realiza | Dominio |
|---|---|---|
| 2 — Solicitud, modificación y cancelación de cita de camión | `RF-GAT-01` | `RF-GAT` |
| 3 — Carga y validación anticipada de documentación | `RF-GAT-03` | `RF-GAT` |
| 5 — Descarga de la serie de temperatura como evidencia de cadena de frío | `RF-REF-12` | `RF-REF` |
| 7 — Estado de congestión del acceso vial | `RF-GAT-13` · `RF-POR-01` | `RF-GAT` · `RF-POR` |

---

## 11. Trazabilidad de la parte 3 y cierre del catálogo

### 11.1 Criterios de aceptación sostenidos en esta parte

| Criterio (CP, Cap. 18) | Requerimientos |
|---|---|
| 5 — Ventana confirmada con 72 h y cumplida | `RF-NAV-01` a `05` · `RF-INT-01` a `04`; alianza: 100 % ≥72 h |
| 6 — Productividad alcanzada, medida y explicada | `RF-NAV-12`, `13` |
| 7 — Planificación sin dependencia individual | `RF-NAV-06` a `09` · EP-01 |
| 10 — Inspección disponible a la hora acordada | `RF-INS-01` a `04`, `07` |
| 13 — Mensajería estándar sin digitación | `RF-INT-01` a `07`; alianza: estándar exclusivo y cero redigitación |
| 14 — Hechos facturables con evidencia | `RF-FAC-01` a `11` · `RF-INT-09` |
| 15 — Autoservicio sin teléfono ni mostrador | `RF-POR-01` a `08` · correspondencia de §10 |
| 16 — Emisiones con método verificable | `RF-EMI-01` a `06` |
| 21 — Plan en cabina sin radio | `RF-NAV-10`, `11` |
| 22 — Continuidad tras la jubilación | `RF-NAV-06` a `09` · EP-01 |

### 11.2 Indicadores movidos en esta parte

| Indicador | Base | Meta | Requerimientos |
|---|---|---|---|
| Cumplimiento de ventana | 71 % | **> 90 % general; 100 % ≥72 h para alianza** | `RF-NAV-01` a `05` |
| Productividad de grúa | 24,8 mov/h | **≥ 30 mov/h por grúa demostrados** | `RF-NAV-12`, `13` |
| Instrucciones digitadas a mano | 41 % | **0 % alianza; ≤ 5 % resto** | `RF-INT-02`, `07` |
| Formatos de plano de estiba | 6 | estándar único | `RF-INT-01`, `06` |
| Personas capaces de planificar | 1 | — | `RF-NAV-06` a `09` |
| Explicar sobretiempo a la naviera | inexistente | trazable | `RF-NAV-13` |
| Inspecciones atrasadas | 28 % | **≤ 12 %** condicionada | `RF-INS-01` a `04`, `07` |
| Facturas objetadas | 4,7 % | bajo 1 % | `RF-FAC-01` a `07` |
| Objeciones por falta de evidencia | 62 % | cero | `RF-FAC-06`, `09` |
| Emisiones por contenedor | no se mide | reporte verificado | `RF-EMI-01` a `06` |

### 11.3 Cierre del catálogo

| Parte | Dominios | Req. | Etapa |
|---|---|---:|:---:|
| 1 | `RF-CON`, `RF-GAT` | 30 | 1 |
| 2 | `RF-PAT`, `RF-TRA`, `RF-REF`, `RF-ACC`, `RF-OPD` | 49 | 1 |
| 3 | `RF-NAV`, `RF-INT`, `RF-FAC`, `RF-POR`, `RF-INS`, `RF-EMI`, `RF-APP`, `RF-FIR` | 59 | 1 y 2 |
| | **Total** | **138** | |

**Reparto por primera entrega: 82 en Etapa 1 y 56 en Etapa 2.** La Parte 3 contiene tres capacidades cuya primera entrega pertenece a Etapa 1: `RF-NAV-09`, `RF-APP-01` y `RF-FIR-01`; las dos últimas amplían escenarios en Etapa 2 sin duplicar el requerimiento padre.
**La eliminación de los antiguos `RF-OPD-03` y `RF-OPD-04` ya está aplicada:** sus compromisos —8 horas fuera de cobertura y sincronización en 90 minutos— quedan acreditados por **RNF-DIS-03** y **RNF-DIS-04** respectivamente, y sus códigos no se reutilizan.

**Cobertura:** 21 de los 22 criterios de aceptación; 26 de los 28 indicadores, con 2 declarados sin meta.
**Requerimientos en revisión: 1** — `RF-PAT-07`, único caso de los siete originales que sigue abierto. Los seis restantes quedaron resueltos y su estado vigente está en `../03_Trazabilidad_y_Bases/registro_correccion_plan_maestro_20260904.md`.
**Entregable documental asociado:** **EP-01**, registro de reglas del planificador, en la EDT del Informe 2.

### 11.4 Pendientes que el catálogo arrastra

| # | Pendiente | De quién |
|---:|---|---|
| 1 | Redacción definitiva de `RF-PAT-07` (único caso en tensión abierto) | Rodolfo e Isidora |
| 2 | Números de página en cada cita normativa, conforme al BA, Art. 43.2 | Rodolfo, antes del T-12 |
| 3 | Valores numéricos de los ejemplos de `RF-EMI-03`, al fijar los factores de emisión | junto al registro de reglas |
| 4 | Factibilidad de lectura desde el sistema de control de las grúas | Célula 3 |
| 5 | Especificación de hardware: 2.400 tomas, 26 tableros, 74 equipos, lectores ópticos, pantallas de cabina | Célula 3 |
| 6 | Evidencia inalterable de hechos facturables en el modelo de datos | Célula 4 |
| 7 | Versión exacta de mensaje SMDG comprometida por naviera | Rodolfo |
| 8 | Plazo de aviso de cada autoridad y existencia de interfaz electrónica | Levantamiento meses 1 a 4 |

---

*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*
