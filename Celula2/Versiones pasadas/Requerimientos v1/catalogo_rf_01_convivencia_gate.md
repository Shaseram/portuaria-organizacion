# Catálogo de Requerimientos Funcionales — Bloque 1
 
## Dominios `RF-CON` (convivencia con el sistema de 2012) y `RF-GAT` (gate)
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento:** 3 — Esquema de solución y alcance
> **Formato:** ficha de ocho campos conforme a CP, Cap. 17.1, más criterio de aceptación exigido por la matriz de trazabilidad del mismo capítulo.
> **Convención de redacción:** «deberá» para lo obligatorio, «podrá» para lo deseable; voz activa; sujeto explícito.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado:** borrador de Célula 2. Pendiente de la Pasada A (IEEE 830) y de la Pasada B (verificación de citas) de la Fase 4.
 
**Cobertura de este bloque:** criterios de aceptación 1, 2, 3, 4 y 20 (CP, Cap. 18); indicadores de línea base de estadía, fila, documentación, masa bruta, citas y lectura automática (CP, 7.3); Decisiones N° 1, 2, 6 y 7.
 
---
 
# Dominio `RF-CON` — Convivencia con el sistema de operación de 2012
 
Etapa 1. Once requerimientos. Materializan la Decisión N° 1 y sostienen los criterios de aceptación 1 y 20 en su dimensión de trazabilidad.
 
---
 
**`RF-CON-01` — Fachada de servicios única** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** exponer toda lectura y toda escritura dirigida al sistema de operación de 2012 a través de una **fachada de servicios única**, de modo que ningún componente consumidor acceda a las interfaces nativas de ese sistema.
**Actor:** componentes consumidores de la solución. **Precondición:** interfaces del sistema de 2012 identificadas en el descubrimiento de los meses 1 a 4.
**Resultado esperado:** cero accesos directos al sistema de 2012 originados fuera de la fachada.
**Origen:** BTT, RT-05.20 (Obligatorio) · Decisión N° 1, requerimientos que introduce la decisión.
**Criterio de aceptación:** sobre una ventana de siete días en preproducción, la traza de red y el registro de correlación acreditan que el **100 %** de las transacciones dirigidas al sistema de 2012 atraviesan la fachada.
 
---
 
**`RF-CON-02` — Contrato de interfaz versionado** · Prioridad: **Alta**
 
**Descripción.** La fachada **deberá** exponer un contrato de interfaz versionado semánticamente, de modo que un cambio en el modelo de datos del sistema de 2012 no obligue a modificar a sus consumidores.
**Actor:** componentes consumidores. **Precondición:** fachada desplegada (`RF-CON-01`).
**Resultado esperado:** los consumidores operan contra una versión declarada del contrato, independiente de la semántica interna del sistema legado.
**Origen:** BTT, RT-05.20 · BTT, RT-05.16 · Decisión N° 1.
**Criterio de aceptación:** se introduce un cambio simulado en el modelo del sistema de 2012 en preproducción y se acredita que ningún consumidor requiere modificación de código.
 
---
 
**`RF-CON-03` — Escritura dual durante la convivencia** · Prioridad: **Crítica**
 
**Descripción.** Mientras un dominio esté en convivencia, la solución **deberá** escribir cada hecho operacional **simultáneamente** en su propio registro y en el sistema de operación de 2012, de modo que ambos registros permanezcan al día.
**Actor:** solución. **Precondición:** dominio en convivencia y escritura dual habilitada.
**Resultado esperado:** ambos registros contienen el mismo hecho dentro de la ventana de desfase declarada.
**Origen:** Decisión N° 1, mecanismos de convivencia. Es la precondición de la reversibilidad comprometida en CP, 13.3 punto 5.
**Criterio de aceptación:** sobre una muestra de un turno completo, el 100 % de los hechos registrados en la solución tiene su correspondiente en el sistema de 2012, salvo los explicados por desfase temporal.
 
---
 
**`RF-CON-04` — Apagado controlado de la escritura dual** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** exigir la **aprobación explícita de un segundo perfil autorizado del CLIENTE** para apagar la escritura dual de un dominio, y **deberá** registrar esa aprobación con autor, fecha, hora y justificación.
**Actor:** perfil autorizado del CLIENTE. **Precondición:** marcha blanca del dominio cerrada formalmente.
**Resultado esperado:** el apagado queda registrado como acto aprobado; no ocurre de forma automática ni por configuración.
**Origen:** BTT, RT-16.03 (doble aprobación de cambios con impacto operacional) · Decisión N° 1: «el apagado es un hito con aprobación explícita del CLIENTE, no un evento automático».
**Criterio de aceptación:** se intenta el apagado con un solo perfil y el sistema lo rechaza; se repite con doble aprobación y el registro de auditoría consigna ambos autores y la justificación.
 
---
 
**`RF-CON-05` — Conciliación automática por turno** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** conciliar automáticamente, **al cierre de cada turno**, la posición de contenedor, los movimientos registrados y las entradas y salidas por gate entre su propio registro y el del sistema de 2012, y **deberá** producir un informe de divergencias.
**Actor:** solución. **Precondición:** dominio en convivencia con escritura dual activa.
**Resultado esperado:** informe de conciliación disponible al cierre de cada uno de los tres turnos, con cada divergencia identificada.
**Origen:** CP, 17.6 punto 2 · Decisión N° 1, mecanismos de convivencia. La frecuencia por turno responde a que CP, Anexo B.1 identifica el cambio de turno como «punto de pérdida de información».
**Criterio de aceptación:** durante siete días consecutivos se emiten los 21 informes de turno sin omisión, y una divergencia inyectada deliberadamente aparece identificada en el informe correspondiente.
 
---
 
**`RF-CON-06` — Clasificación direccional de divergencias** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** clasificar cada divergencia de conciliación en una de cuatro categorías —explicada por desfase temporal, sistema nuevo correcto, sistema nuevo incorrecto, o no resuelta— contrastándola contra verificación física, y **deberá** computar contra el umbral únicamente las dos últimas.
**Actor:** solución y supervisor de turno del CLIENTE. **Precondición:** informe de conciliación emitido (`RF-CON-05`) y muestra de verificación física del turno disponible.
**Resultado esperado:** cada divergencia queda clasificada; las divergencias en que el sistema nuevo resulta correcto se registran como evidencia de mejora y no penalizan la marcha blanca.
**Origen:** Decisión N° 1, regla direccional de clasificación. Sin ella la marcha blanca penalizaría a la solución por ser más exacta que el sistema al que reemplaza.
**Criterio de aceptación:** sobre una muestra de 50 divergencias verificadas físicamente, el 100 % queda clasificado en una de las cuatro categorías y ninguna divergencia con sistema nuevo correcto computa contra el umbral.
 
---
 
**`RF-CON-07` — Detención automática del avance del dominio** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** congelar automáticamente el avance de un dominio y notificar al Comité de Proyecto cuando las divergencias no explicadas superen el umbral de detención declarado para ese universo.
**Actor:** solución. **Precondición:** conciliación de turno ejecutada y divergencias clasificadas.
**Resultado esperado:** avance congelado, notificación emitida y ventana de investigación abierta —48 horas para posición y movimientos, 24 horas para gate y hechos facturables—.
**Origen:** BA, Art. 17.3 (la marcha blanca no cierra con diferencias no explicadas) · CP, 17.6 punto 2 · Decisión N° 1, umbrales de conciliación.
**Criterio de aceptación:** se inyecta un volumen de divergencias sobre el umbral y se acredita que el avance queda congelado sin intervención manual y que la notificación se emite con marca de tiempo.
 
---
 
**`RF-CON-08` — Reversión de dominio por redirección de enrutamiento** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** permitir devolver la autoridad del registro de un dominio al sistema de operación de 2012 mediante **redirección del enrutamiento en la fachada**, sin modificar ningún componente consumidor, y **deberá** completar la operación en **no más de 15 minutos** desde la decisión.
**Actor:** supervisor de turno del CLIENTE o jefe de turno de marcha blanca de Terabyte, sin escalamiento previo. **Precondición:** escritura dual del dominio activa.
**Resultado esperado:** el dominio queda operando contra el sistema de 2012, con la operación restituida y sin pérdida de hechos registrados.
**Origen:** CP, 13.3 punto 5 (retorno probado por dominio) · CP, 17.6 punto 5 · Decisión N° 1, tiempos y autoridad de reversión, anclados en BA, Art. 78.2.
**Criterio de aceptación:** simulacro de reversión ejecutado por cada uno de los dos cargos facultados, en los tres turnos incluida la madrugada, midiendo el tiempo entre decisión y operación restituida contra el objetivo de 15 minutos.
 
---
 
**`RF-CON-09` — Verificación física del inventario por barrido de bloques** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** soportar la verificación física de la posición del inventario mediante **barrido por bloques con congelamiento lógico**, registrando la lectura del código mediante las terminales de equipo y el reconocimiento óptico, y **deberá** reconciliar contra el registro de movimientos los desplazamientos ocurridos en otros bloques durante el barrido.
**Actor:** operador de equipo de patio y supervisor. **Precondición:** bloque con depósitos y retiros suspendidos y operación redirigida a bloques vecinos.
**Resultado esperado:** posición verificada de la totalidad del inventario del bloque, sin conteo manual y sin detener el patio completo.
**Origen:** CP, Cap. 15, RT-05.15 (migrar la totalidad del inventario «con posición verificada físicamente») · CP, 17.6 punto 3 · Decisión N° 1.
**Criterio de aceptación:** se ejecuta el barrido sobre un bloque y se repite sobre una muestra del mismo bloque para estimar el error del propio procedimiento; el error estimado se documenta.
 
---
 
**`RF-CON-10` — Observabilidad y auditoría de la convivencia** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar cada transacción dirigida al sistema de 2012 con un **identificador de correlación común**, que permita seguir una operación completa entre la fachada, el registro propio y el sistema legado.
**Actor:** solución. **Precondición:** fachada desplegada.
**Resultado esperado:** cualquier operación de convivencia es reconstruible extremo a extremo desde un único identificador.
**Origen:** BTT, RT-05.19 · BTT, RT-05.03 · Decisión N° 1, requerimientos que introduce la decisión.
**Criterio de aceptación:** dado el identificador de una operación cualquiera, se reconstruye su recorrido completo por los tres registros sin acceso a la base de datos.
 
---
 
**`RF-CON-11` — Producción trazable de los indicadores del concedente** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** producir los indicadores comprometidos en el contrato de concesión **a partir de los eventos que los originan**, y **no deberá** admitir su carga, edición ni reconstrucción manual.
**Actor:** solución. **Precondición:** eventos de origen registrados en el dominio correspondiente.
**Resultado esperado:** cada valor de indicador es rastreable hasta las transacciones que lo componen.
**Origen:** CP, Cap. 10, restricción no negociable N° 14 («de forma trazable y auditable, no reconstruirlos») · CP, Cap. 18, criterio 20 · CP, Cap. 15, RT-05.29 (consolidación no superior a 1 hora tras el cierre del turno).
**Criterio de aceptación:** se intenta editar manualmente un valor de indicador y el sistema lo rechaza; se selecciona un valor consolidado y se desciende hasta las transacciones de origen que lo componen.
 
---
 
# Dominio `RF-GAT` — Gate, citas, documentación y pesaje
 
Etapa 1. Quince requerimientos. Sostienen los criterios de aceptación 1, 2, 3 y 4, y atacan los indicadores de estadía (78 minutos), fila máxima (3,2 km), documentación defectuosa (22 %) y discrepancia de masa bruta (6 %).
 
---
 
**`RF-GAT-01` — Solicitud de cita de camión** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir a una empresa de transporte solicitar, modificar y cancelar una cita de camión por autoservicio, indicando franja horaria, contenedor u operación y conductor asignado.
**Actor:** empresa de transporte. **Precondición:** empresa registrada como persona usuaria externa.
**Resultado esperado:** cita registrada con franja confirmada, sin intervención telefónica del terminal.
**Origen:** Decisión N° 6 (sistema de citas opcional con prioridad de procesamiento) · CP, 7.3 (sistema de citas: inexistente) · BTT, RT-12.12.
**Criterio de aceptación:** una empresa de transporte completa el ciclo de solicitud, modificación y cancelación por autoservicio, sin contacto telefónico, y la cita queda registrada con su franja.
 
---
 
**`RF-GAT-02` — Prioridad de procesamiento por cita cumplida** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** asignar al camión que llega dentro de su franja de cita una **prioridad de procesamiento** superior a la del camión sin cita o fuera de franja, y **no deberá** aplicar penalización económica por incumplimiento de cita.
**Actor:** solución y funcionario de gate. **Precondición:** camión identificado en la barrera de entrada.
**Resultado esperado:** el camión con cita cumplida se procesa antes que el que no la tiene; el incumplimiento no genera cobro ni sanción.
**Origen:** Decisión N° 6, que adopta el incentivo en lugar del castigo por la advertencia de CP, 16.1 decisión 6 («una cita penalizada que no puede cumplir hará que nadie use el sistema»).
**Criterio de aceptación:** en una franja con camiones de ambos tipos, se acredita que el tiempo medio de procesamiento del grupo con cita cumplida es menor, y que ningún registro de facturación consigna cargo por incumplimiento de cita.
 
---
 
**`RF-GAT-03` — Validación anticipada de la documentación** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** validar la documentación del viaje **antes de que el camión salga a la ruta**, mediante el portal de autoatención, y **deberá** informar al solicitante qué documento falla y qué debe corregir.
**Actor:** empresa de transporte o agencia de aduana. **Precondición:** operación declarada en el portal.
**Resultado esperado:** documentación en estado validado o rechazado con motivo explícito, antes del despacho del camión.
**Origen:** Decisión N° 7 · CP, Cap. 18, criterio 3 · CP, 7.3 (22 % con documentación incompleta o errónea) · BTT, RT-13.06 (ante error, indicar qué ocurrió y qué hacer).
**Criterio de aceptación:** se envía documentación deliberadamente incompleta y el sistema la rechaza identificando el documento faltante y la acción a ejecutar, antes de emitir autorización de viaje.
 
---
 
**`RF-GAT-04` — Derivación a carril de excepción** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** derivar a un **carril de excepción** con atención diferenciada al camión que llegue sin validación previa, y **no deberá** rechazarlo en la barrera.
**Actor:** funcionario de gate. **Precondición:** camión sin documentación validada identificado en la barrera.
**Resultado esperado:** camión atendido por el carril de excepción, sin devolución a la vía pública y sin ocupar un puesto del carril validado.
**Origen:** Decisión N° 7 («rechazar en barrera a un camión que ya hizo el viaje traslada el problema a la vía pública») · CP, Cap. 4.6.
**Criterio de aceptación:** se presenta un camión sin validación previa y se acredita que es derivado al carril de excepción, que su atención no bloquea el carril validado y que el tiempo de atención del carril de excepción es mayor.
 
---
 
**`RF-GAT-05` — Reconocimiento automático del código de contenedor** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** reconocer automáticamente el código de identificación del contenedor mediante lectura óptica en la barrera, validando su **dígito verificador**, y **no deberá** requerir digitación manual del código en la operación normal.
**Actor:** solución. **Precondición:** contenedor presente en el punto de lectura.
**Resultado esperado:** código reconocido y validado, asociado a la operación en curso.
**Origen:** CP, Cap. 18, criterio 4 · CP, Cap. 15, RT-09.01 (reconocimiento no superior a 3 segundos) · Decisión N° 2 (lectura óptica en puntos de paso como verificación cruzada) · BTT, RT-17.06.
**Criterio de aceptación:** sobre una muestra representativa de contenedores en condiciones reales de iluminación y suciedad de placa, se mide la tasa de reconocimiento correcto y se acredita que ningún código válido requirió digitación manual.
 
---
 
**`RF-GAT-06` — Identificación del camión por patente** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** reconocer automáticamente la patente del camión en la barrera y asociarla a la cita, al conductor declarado y a la operación.
**Actor:** solución. **Precondición:** camión presente en el punto de lectura.
**Resultado esperado:** camión identificado y vinculado a su cita y operación sin digitación.
**Origen:** CP, Cap. 2.3 (los puestos de gate ya cuentan con lectura de patente) · BTT, RT-17.06 · Decisión N° 6.
**Criterio de aceptación:** se acredita que la patente leída se vincula automáticamente a la cita registrada, y que una patente sin cita queda marcada como llegada no anunciada.
 
---
 
**`RF-GAT-07` — Verificación de habilitación del conductor** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** verificar en la barrera que el conductor cuenta con habilitación vigente para ingresar al recinto, y **deberá** registrar su ingreso asociado a la operación y a la zona autorizada.
**Actor:** funcionario de gate y solución. **Precondición:** conductor identificado.
**Resultado esperado:** ingreso autorizado o denegado, con registro del acto y de su motivo.
**Origen:** CP, Cap. 18, criterio 17 · CP, Cap. 10, restricción no negociable N° 7 (plan de protección) · Decisión N° 13 (registro de quién ingresó, bajo qué habilitación y a qué zona).
**Criterio de aceptación:** un conductor sin habilitación vigente es denegado y el motivo queda registrado; un conductor habilitado ingresa y su registro consigna operación y zona.
 
---
 
**`RF-GAT-08` — Captura y trazado de la verificación de masa bruta** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** capturar la medición de la báscula, asociarla al contenedor y a la operación, y conservarla como registro trazable de verificación de masa bruta. La solución **no deberá** operar ni certificar la báscula.
**Actor:** solución. **Precondición:** pesaje ejecutado en la báscula del gate.
**Resultado esperado:** medición registrada, trazable hasta el instrumento y el instante de captura.
**Origen:** CP, Cap. 11, exclusión 8 («no se pide operar la báscula ni certificarla metrológicamente; sí capturar y trazar su medición») · CP, Cap. 12, materia 5 (SOLAS VGM) · BTT, RT-17.06 · CP, RT-05.10 (retención de 5 años).
**Criterio de aceptación:** se audita una muestra de mediciones contra la evidencia física de pesaje, verificando trazabilidad completa hasta el instrumento.
 
---
 
**`RF-GAT-09` — Gestión de discrepancia de masa bruta sobre tolerancia** · Prioridad: **Alta**
 
**Descripción.** Cuando la masa verificada supere la tolerancia respecto de la declarada, la solución **deberá** detener el avance de la operación, notificar al embarcador y **marcar el plan de estiba afectado como sujeto a replanificación**.
**Actor:** solución, embarcador y planificador. **Precondición:** medición capturada (`RF-GAT-08`) y masa declarada disponible.
**Resultado esperado:** operación detenida, embarcador notificado y plan de estiba marcado, antes de que el contenedor se embarque con el peso equivocado.
**Origen:** CP, Cap. 4.6 (la discrepancia obliga a rehacer parte del plan de estiba «porque la estabilidad de la nave se calculó con el peso equivocado») · CP, 7.3 (6 % sobre tolerancia, referencia bajo 1 %).
**Criterio de aceptación:** se inyecta una discrepancia sobre tolerancia y se acredita la detención, la notificación al embarcador con marca de tiempo y la marca de replanificación sobre el plan de estiba correspondiente.
 
---
 
**`RF-GAT-10` — Emisión de la instrucción de destino** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** emitir al conductor la instrucción de destino dentro del recinto, derivada de la asignación de posición vigente, en el momento del despacho en la barrera.
**Actor:** solución y conductor. **Precondición:** documentación validada, contenedor reconocido y pesaje resuelto cuando corresponda.
**Resultado esperado:** instrucción de destino entregada, con el bloque y la posición asignados.
**Origen:** CP, Cap. 4.6 · CP, Cap. 15, RT-09.01 (procesamiento del camión en gate no superior a 120 segundos) · Decisión N° 3 (el algoritmo asigna la posición).
**Criterio de aceptación:** se mide, sobre el percentil 95 en carga de peak, el tiempo entre el arribo a la barrera y la emisión de la instrucción, contrastándolo con el umbral de RNF-DES-01.
 
---
 
**`RF-GAT-11` — Registro de los eventos de entrada y de salida** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar el cruce de la barrera de entrada y el de la barrera de salida como **eventos discretos con marca de tiempo**, generados automáticamente en el momento en que ocurren.
**Actor:** solución. **Precondición:** camión en el punto de control.
**Resultado esperado:** dos eventos por viaje, con instante propio y sin captura manual.
**Origen:** CP, Anexo C (la estadía se mide «desde la barrera de entrada hasta la de salida») · CP, Cap. 10, restricción no negociable N° 14.
**Criterio de aceptación:** sobre un turno completo, cada viaje registrado presenta exactamente un evento de entrada y uno de salida, ambos con marca de tiempo generada por el sistema.
 
---
 
**`RF-GAT-12` — Cálculo trazable de la estadía del camión** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** calcular la estadía de cada camión a partir de los eventos de `RF-GAT-11`, y **deberá** permitir descender desde el indicador consolidado hasta los dos eventos que lo componen.
**Actor:** solución y CLIENTE. **Precondición:** eventos de entrada y salida registrados.
**Resultado esperado:** indicador de estadía consolidado, auditable hasta el viaje individual.
**Origen:** CP, Cap. 18, criterio 1 · CP, Cap. 10, restricción no negociable N° 14 · CP, Cap. 15, RT-05.29 (consolidación no superior a 1 hora tras el cierre del turno) · BTT, RT-05.26.
**Criterio de aceptación:** se selecciona un valor consolidado del indicador y se desciende hasta la lista de viajes que lo componen y, desde uno de ellos, hasta sus dos eventos de barrera.
 
---
 
**`RF-GAT-13` — Publicación del estado de congestión del acceso** · Prioridad: **Media**
 
**Descripción.** La solución **deberá** publicar en capa pública, sin autenticación, el estado de congestión del acceso vial y la disponibilidad de franjas de cita.
**Actor:** empresa de transporte y conductor. **Precondición:** ninguna.
**Resultado esperado:** información disponible para decidir el momento de salida antes de iniciar el viaje.
**Origen:** BTT, RT-16.31 (portal público) · CP, Cap. 18, criterio 2 · Decisión N° 6.
**Criterio de aceptación:** se accede sin credenciales al estado de congestión y a la disponibilidad de franjas, y se verifica que el dato refleja la situación con el desfase declarado.
 
---
 
**`RF-GAT-14` — Operación del gate sin enlace exterior** · Prioridad: **Crítica**
 
**Descripción.** El componente on-premise **deberá** sostener la operación completa del gate —validación, reconocimiento, pesaje, emisión de instrucción y registro de eventos— durante la pérdida del enlace hacia el exterior, sin perder ningún registro.
**Actor:** solución. **Precondición:** enlace exterior no disponible.
**Resultado esperado:** gate operando y registrando localmente; ningún evento perdido al restablecerse el enlace.
**Origen:** CP, Cap. 10, restricción no negociable N° 4 · CP, Cap. 15, RT-03.10 (72 horas continuas) · BTT, RT-03.11.
**Criterio de aceptación:** simulacro de corte de enlace durante la ventana comprometida, verificando operación completa del gate y ausencia de pérdida de registros al reconectar. Se articula con RNF-DIS-02 y con el dominio `RF-OPD`.
 
---
 
**`RF-GAT-15` — Conciliación de gate con umbral cero** · Prioridad: **Crítica**
 
**Descripción.** Mientras el gate esté en convivencia, la solución **deberá** conciliar diariamente las entradas y salidas contra el registro del sistema de 2012 y **no deberá** admitir ninguna diferencia no explicada al cierre del día.
**Actor:** solución y supervisor. **Precondición:** dominio de gate en convivencia con escritura dual activa.
**Resultado esperado:** cero diferencias no explicadas al cierre diario; cada diferencia investigada dentro de la ventana de 24 horas.
**Origen:** Decisión N° 1, resolución del umbral de gate: cero diferencias no explicadas, por tratarse de eventos discretos que alimentan un indicador con consecuencia contractual · CP, Cap. 10, restricción no negociable N° 14 · CP, 7.1 (tres semestres consecutivos sobre el umbral).
**Criterio de aceptación:** durante siete días consecutivos, el informe de conciliación diaria del gate cierra con cero diferencias no explicadas, o con cada diferencia clasificada y explicada dentro de las 24 horas.
 
---
 
## Trazabilidad del bloque
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos que lo sostienen |
|---|---|
| 1 — Estadía del camión dentro del umbral, auditable | `RF-GAT-01` a `04`, `10`, `11`, `12`, `15` · `RF-CON-11` |
| 2 — Sin fila que desborde a vía pública | `RF-GAT-01`, `02`, `03`, `13` |
| 3 — Documentación validada antes de salir a la ruta | `RF-GAT-03`, `04` |
| 4 — Código reconocido automáticamente en gate | `RF-GAT-05` |
| 20 — Indicadores del concedente trazables | `RF-CON-11` · `RF-GAT-11`, `12`, `15` |
 
| Indicador de línea base | Requerimientos que lo mueven |
|---|---|
| Estadía 78 min → 45 | `RF-GAT-01` a `05`, `10` |
| Fila máxima 3,2 km → cero | `RF-GAT-01`, `02`, `13` |
| Documentación defectuosa 22 % → bajo 5 % | `RF-GAT-03`, `04` |
| Discrepancia de masa bruta 6 % → bajo 1 % | `RF-GAT-08`, `09` |
| Sistema de citas: inexistente | `RF-GAT-01`, `02` |
| Lectura automática en gate: inexistente | `RF-GAT-05`, `06` |
| Semestres sobre el umbral 3 → cero | `RF-GAT-12`, `15` |
 
**Total del bloque: 26 requerimientos** — 11 en `RF-CON`, 15 en `RF-GAT`.
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*