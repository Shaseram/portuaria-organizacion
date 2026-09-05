# Catálogo de Requerimientos Funcionales — Bloque 3
 
## Dominios `RF-NAV` (nave y planificación) y `RF-INT` (integraciones y mensajería)
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento:** 3 — Esquema de solución y alcance
> **Formato y convención:** los declarados en `claude/plan_catalogo_rf_subdocumento3.md`, Fase 0.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado:** borrador de Célula 2. Pendiente de las dos pasadas de la Fase 4.
 
**Cobertura de este bloque:** criterios de aceptación 5, 6, 7, 13, 21 y 22 (CP, Cap. 18); los ocho indicadores del numeral 7.1; Decisiones N° 4, 5, 14, 15 y 18.
 
> **Dos restricciones gobiernan este bloque.**
> CP, Cap. 10, restricción N° 3: *«El sistema de control de las grúas de muelle es del fabricante y no se interviene. Cualquier obtención de datos desde él es una integración de solo lectura sujeta a autorización.»*
> CP, Cap. 10, restricción N° 5: *«El sistema de gestión empresarial se mantiene y sigue siendo el único emisor de documentos tributarios.»*
>
> De la primera se sigue una consecuencia de diseño que atraviesa todo `RF-NAV`: **la productividad de grúa no se obtiene del sistema de control de la grúa**, sino del registro de movimientos por telemetría de los equipos de patio (`RF-PAT-05`). Depender del sistema del fabricante haría que un criterio de aceptación comprometido quedara sujeto a una autorización de tercero que el propio caso declara no verificada.
 
---
 
# Dominio `RF-NAV` — Nave, planificación y productividad
 
Etapa 2, con una excepción declarada: `RF-NAV-09` pertenece a la **Etapa 1**, por la razón que se explica en su ficha. Catorce requerimientos.
 
---
 
**`RF-NAV-01` — Recepción normalizada del anuncio de recalada** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** recibir el anuncio de recalada de cada naviera y normalizarlo a un **registro único de recalada** con nave, llegada estimada, movimientos de descarga y de embarque y listado de contenedores cuando venga informado, cualquiera sea el canal por el que llegue.
**Actor:** naviera y solución. **Precondición:** naviera registrada como contraparte.
**Resultado esperado:** anuncio disponible como dato estructurado, sin digitación.
**Origen:** CP, Cap. 4.1 (el anuncio llega «por correo electrónico, por el portal de la naviera o por teléfono, según la línea», con 10 a 3 días de anticipación variable) · CP, Cap. 5 (correo y planillas deben dejar de ser sistema de registro).
**Criterio de aceptación:** se reciben anuncios por los tres canales y se verifica que los tres producen un registro de recalada equivalente y estructurado.
 
---
 
**`RF-NAV-02` — Programación de sitios y asignación de grúas** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** mantener la programación de los tres sitios y de las seis grúas de muelle como registro único del sistema, y **deberá** conservar cada modificación con su autor, su instante y su motivo.
**Actor:** jefatura de operaciones. **Precondición:** recaladas anunciadas registradas.
**Resultado esperado:** programación vigente única y consultable; historial de cambios reconstruible.
**Origen:** CP, Cap. 4.1 (hoy la programación vive en una planilla que «se rehace varias veces al día») · CP, Cap. 5 · BTT, RT-16.06.
**Criterio de aceptación:** se modifica la programación tres veces y se reconstruye el historial completo con autor, instante y motivo de cada cambio.
 
---
 
**`RF-NAV-03` — Confirmación de la ventana de atraque con 72 horas** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** confirmar a la naviera la ventana de atraque con **al menos 72 horas de anticipación** al inicio de la ventana, por canal registrado, y **deberá** dejar constancia del instante de la confirmación.
**Actor:** solución y naviera. **Precondición:** programación de sitios definida para la recalada.
**Resultado esperado:** ventana confirmada con la anticipación comprometida y con evidencia del acto.
**Origen:** CP, Cap. 18, criterio 5 · CP, Cap. 9.2 · CP, Cap. 1 (condición de la alianza naviera para 2029) · CP, 7.1 (cumplimiento actual: 71 %, referencia 90 %).
**Criterio de aceptación:** sobre las recaladas de un mes, se acredita que el 100 % de las ventanas se confirmó con 72 horas o más, y se mide el porcentaje de cumplimiento efectivo contra la referencia de 90 %.
 
---
 
**`RF-NAV-04` — Notificación registrada del cambio de ventana** · Prioridad: **Alta**
 
**Descripción.** Ante cualquier modificación de una ventana confirmada, la solución **deberá** notificar a la naviera por canal registrado y **no deberá** admitir que el cambio se comunique únicamente por vía telefónica.
**Actor:** solución y naviera. **Precondición:** ventana previamente confirmada.
**Resultado esperado:** cambio notificado con evidencia de emisión y de recepción.
**Origen:** CP, Cap. 4.1 («la ventana se confirma a la naviera por correo; cuando cambia, se avisa por teléfono») · BTT, RT-16.23 (registro de entrega, apertura y error por mensaje).
**Criterio de aceptación:** se modifica una ventana confirmada y se recupera el registro de notificación con su estado de entrega.
 
---
 
**`RF-NAV-05` — Estimación de duración a partir de serie histórica** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** estimar la duración de atención de una nave a partir de la **serie histórica de productividad registrada** por sitio, grúa y tipo de operación, y **no deberá** basarla en una productividad supuesta ajustada manualmente.
**Actor:** jefatura de operaciones. **Precondición:** serie histórica de movimientos disponible.
**Resultado esperado:** estimación con método declarado y reproducible.
**Origen:** CP, Cap. 4.1 («no hay modelo, no hay serie histórica sistematizada») · CP, Cap. 9.2 · CP, 7.1 (productividad efectiva 24,8 mov/h contra 30 exigidos a 2029).
**Criterio de aceptación:** se estima la duración de una recalada y se acredita que el cálculo es reproducible a partir de la serie histórica, sin parámetro ajustado a mano.
 
---
 
**`RF-NAV-06` — Propuesta automática del plan de estiba y de patio** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** proponer automáticamente el plan de estiba y el plan de patio, respetando peso, altura, puerto de destino, segregación de carga peligrosa, estabilidad de la nave y disponibilidad de conexión refrigerada a bordo.
**Actor:** solución. **Precondición:** plano de estiba recibido y listado de contenedores disponible.
**Resultado esperado:** plan propuesto, no impuesto: queda a la espera de la decisión del planificador.
**Origen:** Decisión N° 4 («el algoritmo propone, el planificador aprueba o corrige») · CP, Cap. 4.2 (enumeración de las restricciones que el plan debe respetar) · CP, Cap. 18, criterio 7.
**Criterio de aceptación:** se genera una propuesta de plan sobre una recalada real y se verifica el cumplimiento de las seis restricciones enumeradas.
 
---
 
**`RF-NAV-07` — Aprobación o corrección del plan por el planificador** · Prioridad: **Crítica**
 
**Descripción.** El planificador **deberá** poder aprobar la propuesta o corregirla antes de su publicación, y la solución **no deberá** publicar un plan que no haya sido aprobado o corregido por él.
**Actor:** planificador de estiba y patio. **Precondición:** plan propuesto disponible.
**Resultado esperado:** el plan vigente siempre tiene una decisión humana detrás.
**Origen:** Decisión N° 4, que descarta la automatización plena · CP, Cap. 8 (el planificador acepta el esquema en que «la máquina me proponga y yo corrija») · CP, Cap. 9.3 («un mecanismo que proponga y una persona que decida»).
**Criterio de aceptación:** se intenta publicar un plan sin aprobación y el sistema lo impide; se acredita que todo plan publicado registra la aprobación o corrección de su autor.
 
---
 
**`RF-NAV-08` — Registro estructurado del motivo de cada corrección** · Prioridad: **Crítica**
 
**Descripción.** Cuando el planificador corrija la propuesta, la solución **deberá** exigir y registrar el **motivo de la corrección de forma estructurada**, y **no deberá** admitir la corrección sin motivo.
**Actor:** planificador. **Precondición:** corrección iniciada sobre una propuesta.
**Resultado esperado:** corpus creciente de decisiones con su razón, explotable como conocimiento.
**Origen:** Decisión N° 4 · CP, Cap. 16.1 decisión 4 (es el mecanismo por el cual el conocimiento «queda en la empresa antes de 2028, o no queda») · CP, Cap. 8 («que quede registrado por qué corregí. Así el que venga después aprende de eso, no de mirarme a mí»).
 
> El campo de impacto de la Decisión N° 4 advierte que si el motivo no se captura de forma estructurada, «el conocimiento se pierde igual, solo que documentado de forma inutilizable». De ahí que el motivo sea estructurado y no texto libre.
 
**Criterio de aceptación:** se intenta corregir sin motivo y el sistema lo rechaza; se consulta el corpus acumulado y se agrupan las correcciones por motivo.
 
---
 
**`RF-NAV-09` — Registro de reglas del planificador** · Prioridad: **Crítica** · **Etapa 1**
 
**Descripción.** La solución **deberá** mantener un **registro de las reglas, restricciones y casos del planificador** —estado real de los equipos, comportamiento físico de los bloques, particularidades de naves, comportamiento de clientes y reglas normativas duras—, editable y versionado, que alimente al motor de propuesta.
**Actor:** planificador y analista de Terabyte. **Precondición:** ninguna; el frente arranca en el mes 1.
**Resultado esperado:** primera versión del registro antes del hito H2; versión validada con el planificador antes del cierre de desarrollo de la Etapa 1.
**Origen:** Decisión N° 1, frente de captura del conocimiento tácito · CP, Cap. 17.1 (registro de reglas de negocio, con «criterio de asignación de posición en patio») · CP, Cap. 4.2 (la grúa tres con falla intermitente, el bloque C que se inunda, el generador de popa limitado, el exportador que llega tarde: «nada de eso está escrito en ninguna parte») · CP, Cap. 18, criterio 22.
 
> **Por qué es Etapa 1 y no Etapa 2.** La planificación asistida entra en producción en el mes 21. El planificador se retira «el 2028» sin mes declarado. Si el módulo fuera el único depositario previsto del conocimiento y él se retirara antes de que exista, el criterio de aceptación 22 fallaría sin remedio. El entregable de este requerimiento no es software: es el registro.
 
**Criterio de aceptación:** existe la primera versión del registro antes del hito H2, con las cinco categorías cubiertas, y su versión validada cuenta con la conformidad expresa del planificador antes del mes 12.
 
---
 
**`RF-NAV-10` — Distribución del plan vigente a la cabina** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** presentar al operador de grúa de muelle el plan vigente en una **pantalla integrada a la cabina**, y **no deberá** requerir que el plan se entregue en papel ni que sus cambios se comuniquen por radio.
**Actor:** operador de grúa de muelle. **Precondición:** plan publicado y pantalla instalada.
**Resultado esperado:** el operador dispone del plan vigente sin intermediación verbal.
**Origen:** Decisión N° 14 · CP, Cap. 18, criterio 21 · CP, Cap. 4.3 (hoy trabaja con «el plan impreso entregado al inicio del turno» y «alguien se lo grita por radio y él anota en el margen de la hoja»).
 
> La pantalla es un **dispositivo propio de la solución instalado en la cabina**, no una modificación del sistema de control de la grúa, que la restricción N° 3 declara no intervenible.
 
**Criterio de aceptación:** prueba en cabina real durante la marcha blanca, verificando que el operador dispone del plan vigente sin recibirlo por radio ni en papel.
 
---
 
**`RF-NAV-11` — Actualización del plan sin interacción activa** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** reflejar los cambios del plan en la pantalla de cabina mediante indicación visual, y alertar acústicamente **solo ante condiciones de seguridad**. La solución **no deberá** incorporar botones de confirmación para la operación rutinaria ni exigir que el operador aparte la vista de la carga.
**Actor:** operador de grúa de muelle. **Precondición:** plan modificado durante la operación.
**Resultado esperado:** cambio percibido sin acción del operador y sin desviar su atención de la faena.
**Origen:** CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 15, RT-13.08 · Decisión N° 14 · CP, Cap. 18, criterio 21 («sin apartar la vista de la carga»).
**Criterio de aceptación:** revisión ergonómica conjunta con el sindicato y con prevención de riesgos antes del diseño detallado, más prueba en cabina real, con acta de conformidad. Se articula con RNF-USA-05.
 
---
 
**`RF-NAV-12` — Medición de productividad en tiempo real** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** calcular la productividad de grúa en tiempo real, con granularidad **por hora y por equipo**, a partir del registro de movimientos, y **no deberá** obtenerla del sistema de control de las grúas ni de consolidación manual de formularios de turno.
**Actor:** solución y jefatura de operaciones. **Precondición:** movimientos registrados conforme a `RF-PAT-05` y `RF-PAT-14`.
**Resultado esperado:** productividad consultable en línea, descomponible hasta el movimiento individual.
**Origen:** CP, Cap. 18, criterio 6 · CP, Cap. 15, RT-05.29 (indicadores de productividad en tiempo real, con granularidad por hora y por equipo) · CP, Cap. 10, restricción no negociable N° 3 · CP, 7.1 (registro por hora y por grúa: inexistente).
**Criterio de aceptación:** se consulta la productividad de una hora y una grúa determinadas y se desciende hasta los movimientos que la componen, acreditando que ningún dato provino del sistema del fabricante.
 
---
 
**`RF-NAV-13` — Explicación trazable del sobretiempo de nave** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar las **causas de detención de grúa** —espera de tractocamión, discrepancia entre plan y celda, espera de remoción— y **deberá** producir, para cada recalada, la descomposición del tiempo de atención entre operación efectiva y detención por causa.
**Actor:** jefatura de operaciones y naviera. **Precondición:** operación de nave registrada con sus eventos de detención.
**Resultado esperado:** capacidad de explicar a la naviera, con evidencia, por qué su nave demoró lo que demoró.
**Origen:** CP, 7.1 («capacidad de explicar a la naviera la causa de un sobretiempo de nave: inexistente») · CP, Cap. 9.2 · CP, Cap. 4.3, que enumera las tres causas de la brecha de productividad.
**Criterio de aceptación:** para una recalada cerrada se emite la descomposición del tiempo total entre operación efectiva y detenciones clasificadas por causa, cuya suma reconcilia con la duración registrada.
 
---
 
**`RF-NAV-14` — Replanificación por discrepancia de masa bruta** · Prioridad: **Alta**
 
**Descripción.** Ante un plan de estiba marcado por discrepancia de masa bruta sobre tolerancia, la solución **deberá** recalcular la propuesta afectada y **deberá** someterla nuevamente a la aprobación del planificador antes de publicarla.
**Actor:** solución y planificador. **Precondición:** marca de replanificación generada por `RF-GAT-09`.
**Resultado esperado:** plan corregido y aprobado antes de que el contenedor se embarque con el peso equivocado.
**Origen:** CP, Cap. 4.6 (la discrepancia obliga a rehacer parte del plan «porque la estabilidad de la nave se calculó con el peso equivocado») · CP, Cap. 12, materia 5 (SOLAS VGM).
**Criterio de aceptación:** se inyecta una discrepancia sobre tolerancia y se acredita que el plan afectado se recalcula y vuelve al circuito de aprobación antes de su publicación.
 
---
 
# Dominio `RF-INT` — Integraciones y mensajería
 
Etapa 2. Once requerimientos.
 
---
 
**`RF-INT-01` — Recepción del plano de estiba en mensaje estándar** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** recibir el plano de estiba mediante el mensaje estándar de la industria y **deberá** incorporarlo al plan sin digitación manual.
**Actor:** naviera y solución. **Precondición:** naviera integrada por mensajería.
**Resultado esperado:** plano incorporado como dato estructurado.
**Origen:** Decisión N° 18 (BAPLIE) · CP, Cap. 15, RT-05.23 · CP, Cap. 18, criterio 13 · CP, 7.1 (6 formatos distintos de plano de estiba, referencia «estándar único»).
**Criterio de aceptación:** se recibe un plano por mensajería estándar desde al menos una naviera y se acredita su incorporación al plan sin intervención manual.
 
---
 
**`RF-INT-02` — Recepción de la orden de embarque** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** recibir la orden de embarque mediante el mensaje estándar de la industria y **no deberá** requerir su digitación desde correo electrónico.
**Actor:** naviera y solución. **Precondición:** naviera integrada por mensajería.
**Resultado esperado:** instrucción de embarque incorporada sin redigitación.
**Origen:** Decisión N° 18 (COPRAR) · CP, Cap. 15, RT-05.23 · CP, 7.1 (41 % de instrucciones recibidas por correo y digitadas a mano, referencia cero).
**Criterio de aceptación:** se mide el porcentaje de instrucciones de embarque incorporadas por mensajería frente al total, contrastándolo con la referencia de cero digitación.
 
---
 
**`RF-INT-03` — Emisión de la confirmación de carga y descarga** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** emitir a la naviera la confirmación de carga y descarga mediante el mensaje estándar de la industria, derivada de los movimientos efectivamente registrados.
**Actor:** solución y naviera. **Precondición:** operación de nave con movimientos registrados.
**Resultado esperado:** confirmación emitida automáticamente y consistente con el registro de movimientos.
**Origen:** Decisión N° 18 (COARRI) · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** se contrasta el contenido del mensaje emitido contra los movimientos registrados de la recalada, verificando correspondencia íntegra.
 
---
 
**`RF-INT-04` — Emisión de la notificación de movimiento** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** emitir la notificación de movimiento de contenedor mediante el mensaje estándar de la industria, en el momento en que el movimiento se registra.
**Actor:** solución y naviera. **Precondición:** movimiento registrado.
**Resultado esperado:** contraparte informada sin intervención manual.
**Origen:** Decisión N° 18 (CODECO) · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** se acredita la emisión de la notificación asociada a un movimiento, con su marca de tiempo.
 
---
 
**`RF-INT-05` — Validación de integridad y origen del mensaje** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** validar la integridad y el origen de cada mensaje recibido antes de incorporarlo, y **deberá** rechazar y registrar todo mensaje que no supere la validación.
**Actor:** solución. **Precondición:** mensaje recibido de una contraparte.
**Resultado esperado:** ningún mensaje no validado modifica el plan ni el inventario.
**Origen:** Decisión N° 18, riesgo documentado de manipulación de mensajería de estiba para reruteo o robo de carga · BTT, RT-11.01 (verificación explícita de cada solicitud) · CP, Cap. 12, materia 2 (protección de instalaciones portuarias).
 
> La adopción del estándar no basta: el campo de impacto de la Decisión N° 18 advierte que sin validación de integridad «la integración queda expuesta al riesgo de manipulación documentado en la industria».
 
**Criterio de aceptación:** se inyecta un mensaje alterado y se acredita que es rechazado, registrado y que no produce efecto sobre el plan ni sobre el inventario.
 
---
 
**`RF-INT-06` — Versionado explícito del mensaje por contraparte** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar y versionar explícitamente la versión de mensaje soportada por cada una de las navieras, y **deberá** procesar cada mensaje conforme a la versión declarada para su emisor.
**Actor:** solución. **Precondición:** naviera integrada con versión declarada.
**Resultado esperado:** convivencia de versiones distintas entre contrapartes, sin ambigüedad de interpretación.
**Origen:** Decisión N° 18, que identifica la fragmentación de versiones entre contrapartes como el principal problema de implementación · BTT, RT-05.17 (versionado semántico de contratos de interfaz) · CP, Cap. 15, RT-05.23 (acreditar factibilidad con las 14 navieras).
**Criterio de aceptación:** se procesan mensajes de dos navieras con versiones distintas y ambos se interpretan conforme a la versión declarada para cada emisor.
 
---
 
**`RF-INT-07` — Canal puente para navieras no integradas** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** ofrecer a las navieras aún no integradas un **canal de intercambio asistido** —portal o carga de archivo, con validación previa e informe de errores por registro— y **no deberá** bloquear su operación mientras se integran.
**Actor:** naviera no integrada. **Precondición:** naviera registrada como contraparte.
**Resultado esperado:** operación continua de las 14 navieras con distintos niveles de madurez.
**Origen:** Decisión N° 18 · CP, Cap. 1 y 2 (14 navieras, una alianza concentra el 34 % del volumen) · BTT, RT-05.22 (carga masiva con validación previa, informe de errores por registro y procesamiento parcial).
 
> El campo de impacto de la Decisión N° 18 advierte que si el puente se vuelve permanente, la solución sostiene dos vías de integración indefinidamente. La revisión semestral de avance forma parte de la instancia de validación de esa decisión.
 
**Criterio de aceptación:** una naviera no integrada completa una operación por el canal puente, con informe de errores por registro y procesamiento parcial de los registros válidos.
 
---
 
**`RF-INT-08` — Identificación normalizada del contenedor** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** identificar cada contenedor conforme a la norma internacional de codificación e identificación, validando su **dígito verificador** en toda captura, recepción o emisión.
**Actor:** solución. **Precondición:** código de contenedor presente en cualquier punto de entrada.
**Resultado esperado:** ningún código inválido ingresa al inventario ni a un mensaje emitido.
**Origen:** CP, Cap. 15, RT-05.23 («norma internacional de codificación e identificación de contenedores») · CP, num. 16.2, que identifica la norma por su estructura de código y dígito verificador · CP, Cap. 4.6 (hoy se digitan 11 caracteres y «los errores de digitación existen y se descubren después»).
**Criterio de aceptación:** se inyectan códigos con dígito verificador inválido por cada vía de entrada y se acredita el rechazo en todas ellas.
 
---
 
**`RF-INT-09` — Entrega de hechos facturables al sistema de gestión empresarial** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** entregar los hechos facturables al sistema de gestión empresarial del CLIENTE para su facturación, y **no deberá** emitir documentos tributarios ni constituirse en un segundo emisor.
**Actor:** solución y sistema de gestión empresarial. **Precondición:** hechos facturables generados y validados.
**Resultado esperado:** un único emisor tributario, alimentado con hechos verificables.
**Origen:** CP, Cap. 10, restricción no negociable N° 5 · CP, Cap. 11, exclusión 1 · CP, Cap. 5 («la solución le entrega los hechos facturables; no habrá dos emisores»).
**Criterio de aceptación:** se acredita que la solución no emite ningún documento tributario y que el 100 % de los hechos facturables llega al sistema de gestión empresarial con su evidencia asociada.
 
---
 
**`RF-INT-10` — Integración con las autoridades donde exista interfaz** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** integrarse con los canales electrónicos de las autoridades aduanera, fitosanitaria y sanitaria **donde exista una interfaz disponible**, y **deberá** operar el canal asistido de `RF-INS` donde no exista. La solución **no deberá** desarrollar ni sustituir el sistema de una autoridad.
**Actor:** autoridad y solución. **Precondición:** existencia de interfaz verificada en el levantamiento de los meses 1 a 4.
**Resultado esperado:** coordinación electrónica donde sea posible, asistida donde no, sin dejar ningún servicio fuera.
**Origen:** CP, Cap. 11, exclusión 7 · CP, num. 17.4 punto 9 («qué se hace donde no exista interfaz disponible») · Decisión N° 21 · CP, Cap. 15, RT-05.23.
**Criterio de aceptación:** para cada uno de los tres servicios se acredita el canal efectivamente operativo —electrónico o asistido— y la trazabilidad de la coordinación en ambos casos.
 
---
 
**`RF-INT-11` — Correlación y trazabilidad de cada integración** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar la transacción de entrada y de salida de cada integración con un **identificador de correlación común**, que permita seguir la operación entre todos los sistemas involucrados.
**Actor:** solución. **Precondición:** integración operativa.
**Resultado esperado:** toda operación integrada es reconstruible extremo a extremo.
**Origen:** BTT, RT-05.19 · BTT, RT-05.03 · articula con `RF-CON-10`.
**Criterio de aceptación:** dado el identificador de una operación integrada, se reconstruye su recorrido completo entre la contraparte externa, la solución y el registro de destino.
 
---
 
## Trazabilidad del bloque
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos que lo sostienen |
|---|---|
| 5 — Ventana confirmada con 72 h y cumplida | `RF-NAV-01` a `05` |
| 6 — Productividad medida y explicada por hora y equipo | `RF-NAV-12`, `13` · `RF-PAT-14` |
| 7 — Planificación sin dependencia de una sola persona | `RF-NAV-06` a `09` |
| 13 — Instrucciones y planos por mensajería estándar | `RF-INT-01` a `04`, `06`, `07` |
| 14 — Hechos facturables con evidencia *(parcial)* | `RF-INT-09` |
| 21 — Plan en cabina sin radio ni apartar la vista | `RF-NAV-10`, `11` |
| 22 — El planificador se jubila y el terminal sigue planificando | `RF-NAV-06` a `09` |
 
| Indicador de línea base (CP, 7.1) | Referencia | Requerimientos que lo mueven |
|---|---|---|
| Cumplimiento de ventana 71 % | 90 % | `RF-NAV-01` a `05` |
| Productividad de grúa 24,8 mov/h | 30 a 2029 | `RF-NAV-12`, `13` |
| Instrucciones digitadas a mano 41 % | cero | `RF-INT-02`, `07` |
| Formatos de plano de estiba 6 | estándar único | `RF-INT-01`, `06` |
| Personas capaces de planificar 1 | — | `RF-NAV-06` a `09` |
| Registro por hora y por grúa: inexistente | continuo | `RF-NAV-12` · `RF-PAT-14` |
| Explicar sobretiempo a la naviera: inexistente | trazable | `RF-NAV-13` |
| Semestres sobre el umbral 3 | cero | `RF-GAT-12`, `15` *(bloque 1)* |
 
**Total del bloque: 25 requerimientos** — 14 en `RF-NAV`, 11 en `RF-INT`.
**Acumulado del catálogo: 78 requerimientos** en seis dominios.
 
**Dominios pendientes:** `RF-FAC`, `RF-POR`, `RF-ACC`, `RF-OPD`, `RF-INS`, `RF-EMI`.
 
---
 
## Pendientes transversales del catálogo
 
| # | Pendiente | Origen |
|---:|---|---|
| 1 | Fundamentar las once metas propuestas con literatura arbitrada o casos documentados. Prioritarias: metas 1 (remociones) y 11 (inspecciones) | Solicitud de Rodolfo Fernández · CP, Cap. 16.2 |
| 2 | Ratificar `RF-PAT-10` (vía de excepción del operador) | Bloque 2 |
| 3 | Evitar la duplicación entre `RF-GAT-14` y el dominio `RF-OPD` | Bloque 1 |
| 4 | Verificar el mapeo entre los 107 códigos RT no funcionales y los 77 RNF, al construir el T-12 | Vacío 6 de la Fase 2 |
| 5 | **Confirmar con Célula 3 la factibilidad de la lectura de datos desde el sistema de control de las grúas.** `RF-NAV-12` está diseñado para **no** depender de ella, pero la restricción N° 3 y CP, Cap. 5 exigen verificar la factibilidad de esa integración antes de comprometerla en cualquier otro punto | Bloque 3 |
| 6 | **Declarar la versión exacta de cada mensaje de mensajería marítima** que se compromete soportar, por naviera. La Decisión N° 18 lo exige como instancia de validación y `RF-INT-06` lo presupone | Bloque 3 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*