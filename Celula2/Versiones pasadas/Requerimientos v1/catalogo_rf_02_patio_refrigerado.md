# Catálogo de Requerimientos Funcionales — Bloque 2
 
## Dominios `RF-PAT` (patio) y `RF-REF` (patio refrigerado)
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento:** 3 — Esquema de solución y alcance
> **Formato y convención:** los declarados en `claude/plan_catalogo_rf_subdocumento3.md`, Fase 0.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado:** borrador de Célula 2. Pendiente de las dos pasadas de la Fase 4.
 
**Cobertura de este bloque:** criterios de aceptación 8, 9, 11 y 12 (CP, Cap. 18); los nueve indicadores de patio y carga refrigerada del numeral 7.2 cuyas metas se propusieron en `claude/registro_supuestos_complemento_celula2.md`; Decisiones N° 2, 3, 5, 8, 10 y 15.
 
> **Restricción dominante de ambos dominios.** CP, Cap. 10, restricción no negociable N° 1: *«Ninguna solución puede aumentar la exposición de una persona al riesgo del patio. Toda propuesta que obligue a un operador a atender un dispositivo mientras hay equipos en movimiento será rechazada, cualquiera sea su mérito en el resto.»* Cada requerimiento de terreno de este bloque se redactó contra esa frase.
 
---
 
# Dominio `RF-PAT` — Patio: posición, movimientos y asignación
 
Etapa 1. Catorce requerimientos.
 
---
 
**`RF-PAT-01` — Posicionamiento automático del equipo como fuente primaria** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** obtener la posición del contenedor a partir del **posicionamiento automático del equipo que lo manipula**, sin requerir confirmación activa de la persona operadora.
**Actor:** solución. **Precondición:** equipo instrumentado y operativo.
**Resultado esperado:** posición registrada como consecuencia del movimiento físico, no de una declaración humana.
**Origen:** Decisión N° 2 (posicionamiento automático del equipo como fuente primaria) · CP, Cap. 10, restricción no negociable N° 1 · CP, 7.2 (3,1 % de contenedores registrados donde no están).
**Criterio de aceptación:** sobre una muestra de movimientos observados físicamente, se contrasta la posición registrada automáticamente contra la posición real, y se acredita que ninguno requirió confirmación de la persona operadora.
 
---
 
**`RF-PAT-02` — Verificación cruzada por lectura óptica en puntos de paso** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** leer ópticamente el código del contenedor en los puntos de paso obligados —gate y entrada de bloque— y **deberá** contrastar esa lectura contra la posición obtenida por posicionamiento automático.
**Actor:** solución. **Precondición:** contenedor atravesando un punto de paso instrumentado.
**Resultado esperado:** dos fuentes independientes sobre el mismo contenedor, contrastadas.
**Origen:** Decisión N° 2 (lectura óptica como verificación cruzada) · BTT, RT-17.06 · CP, Cap. 15, RT-09.01.
**Criterio de aceptación:** se acredita que cada paso por un punto instrumentado genera un contraste registrado entre lectura óptica y posicionamiento automático.
 
---
 
**`RF-PAT-03` — Estado de confianza de la posición** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** mantener para cada contenedor un **estado de confianza de su posición**, que será «conocida» cuando el posicionamiento automático y una lectura óptica reciente coincidan, y «por verificar» cuando discrepen o cuando falte una de las dos fuentes.
**Actor:** solución. **Precondición:** contenedor registrado en inventario.
**Resultado esperado:** todo contenedor del inventario tiene estado de confianza explícito y consultable.
**Origen:** Decisión N° 2, que define cuándo una posición se considera «conocida» · CP, Cap. 18, criterio 9.
**Criterio de aceptación:** se consulta el inventario completo y el 100 % de los contenedores presenta uno de los dos estados; se inyecta una discrepancia y el estado del contenedor afectado cambia a «por verificar».
 
---
 
**`RF-PAT-04` — Tarea de verificación física ante discrepancia** · Prioridad: **Alta**
 
**Descripción.** Ante un contenedor en estado «por verificar», la solución **deberá** generar automáticamente una **tarea de verificación física dirigida** a la posición candidata, y **no deberá** dejar la discrepancia sin acción asignada.
**Actor:** solución y supervisor de patio. **Precondición:** contenedor en estado «por verificar».
**Resultado esperado:** tarea generada, asignada y con seguimiento hasta su cierre.
**Origen:** Decisión N° 2 · meta propuesta del indicador «contenedores registrados donde no están»: ≤ 0,5 % de posiciones «por verificar» no resueltas dentro del turno.
**Criterio de aceptación:** se acredita que toda discrepancia genera tarea, y se mide el porcentaje de tareas no resueltas al cierre del turno contra el umbral de 0,5 %.
 
---
 
**`RF-PAT-05` — Registro del movimiento sin confirmación del operador** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar la ejecución de un movimiento de contenedor a partir de la **telemetría del propio equipo** —sensores de izaje, encoders de posición y posicionamiento— y **no deberá** requerir que la persona operadora ejecute una acción de confirmación.
**Actor:** solución. **Precondición:** equipo instrumentado en operación.
**Resultado esperado:** movimiento registrado en el instante en que ocurre, sin interacción humana.
**Origen:** Decisión N° 15 · CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 4.3 (hoy los movimientos «se registran al final del turno, a mano»).
**Criterio de aceptación:** prueba de correlación entre telemetría y observación física directa sobre una muestra de movimientos, verificando que ningún registro dependió de una acción del operador.
 
---
 
**`RF-PAT-06` — Asignación algorítmica de la posición** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** asignar automáticamente la posición de destino de cada contenedor y **deberá** entregar esa asignación al equipo como instrucción a ejecutar.
**Actor:** solución. **Precondición:** contenedor ingresado o descargado, con sus atributos declarados.
**Resultado esperado:** posición asignada por regla explicable, no por criterio individual del operador.
**Origen:** Decisión N° 3 («el algoritmo asigna, el operador ejecuta») · CP, Cap. 4.4 («no existe un algoritmo, ni una regla escrita, ni un registro de por qué se eligió esa posición») · CP, Cap. 18, criterio 8.
**Criterio de aceptación:** se acredita que el 100 % de las posiciones asignadas en un turno proviene del algoritmo, y que cada asignación conserva la regla que la determinó.
 
---
 
**`RF-PAT-07` — Reglas de segregación en la asignación** · Prioridad: **Crítica**
 
**Descripción.** La asignación de posición **deberá** respetar las reglas de segregación de mercancías peligrosas del Código IMDG, la disponibilidad de conexión refrigerada y la prioridad de retiro declarada, y **no deberá** producir una asignación que infrinja alguna de ellas.
**Actor:** solución. **Precondición:** atributos del contenedor declarados, incluida su clasificación IMDG.
**Resultado esperado:** cero asignaciones que infrinjan segregación.
**Origen:** CP, Cap. 12, materia 6 (IMDG: «determina qué contenedores pueden apilarse juntos y a qué distancia, y restringe la libertad del algoritmo de patio») · Decisión N° 3.
**Criterio de aceptación:** se ejecuta el algoritmo sobre un conjunto de contenedores con mercancías peligrosas y se verifica el cumplimiento íntegro de las reglas de segregación. Se articula con RNF-CUM-05.
 
---
 
**`RF-PAT-08` — Catálogo de condiciones dinámicas de patio** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir al planificador declarar en tiempo real condiciones dinámicas que restrinjan la asignación —equipo no disponible, bloque restringido, cliente de alto riesgo de atraso— y **deberá** respetarlas en cada corrida posterior del algoritmo.
**Actor:** planificador de estiba y patio. **Precondición:** ninguna; la declaración es a demanda.
**Resultado esperado:** la condición declarada rige desde su registro y queda trazada con autor, motivo y vigencia.
**Origen:** Decisión N° 5 · CP, Cap. 4.2 (la grúa con falla intermitente, el bloque que se inunda, el generador de popa limitado: «nada de eso está escrito en ninguna parte») · CP, 16.1 decisión 5 («un plan óptimo sobre supuestos falsos se cae en la segunda hora»).
**Criterio de aceptación:** se declara una condición dinámica y se acredita que la siguiente corrida del algoritmo la respeta, y que la condición queda registrada con su motivo.
 
---
 
**`RF-PAT-09` — Instrucción al equipo sin interacción activa** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** presentar la instrucción de movimiento en la terminal del equipo mediante indicación visual, y **no deberá** exigir a la persona operadora manipular el dispositivo mientras haya equipos en movimiento.
**Actor:** operador de equipo de patio. **Precondición:** instrucción asignada al equipo.
**Resultado esperado:** instrucción visible y comprensible sin acción del operador durante la faena.
**Origen:** CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 15, RT-13.08 · Decisión N° 3.
**Criterio de aceptación:** evaluación de riesgo de la interfaz con participación de prevención de riesgos, con acta de conformidad previa al paso a producción. Se articula con RNF-USA-05.
 
---
 
**`RF-PAT-10` — Vía de excepción del operador** · Prioridad: **Alta** · ⚠ **depende de un vacío no ratificado**
 
**Descripción.** La solución **deberá** permitir a la persona operadora marcar una instrucción como **no ejecutable**, seleccionando un motivo de una lista breve, **con el equipo detenido**, y **deberá** reasignar la posición sin exigir que el movimiento se complete.
**Actor:** operador de equipo de patio. **Precondición:** instrucción recibida y equipo detenido.
**Resultado esperado:** instrucción devuelta con motivo; el algoritmo produce una asignación alternativa; el motivo alimenta el catálogo de condiciones dinámicas.
**Origen:** CP, Cap. 10, restricción no negociable N° 1, que prohíbe la interacción **mientras hay equipos en movimiento** y por tanto no impide una acción con el equipo detenido · Decisión N° 5, por analogía con la vía que sí tiene el planificador.
 
> **Advertencia.** Este requerimiento resuelve un hueco que la propia Decisión N° 3 reconoce en su campo de impacto: *«el operador ejecutará una instrucción errónea sin oportunidad de corregirla antes del movimiento»*. La Decisión N° 5 da vía de corrección al planificador, pero **ninguna decisión se la da al operador**. La propuesta está pendiente de ratificación por la célula y de validación con prevención de riesgos y con el sindicato; **no debe presentarse como decidida**.
 
**Criterio de aceptación:** se acredita que la marca de no ejecutable solo está disponible con el equipo detenido, que el algoritmo reasigna, y que el motivo queda registrado y disponible para el planificador.
 
---
 
**`RF-PAT-11` — Programación anticipada de remociones** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** calcular las remociones necesarias para acceder a un contenedor comprometido —retiro con cita, inspección agendada o embarque planificado— y **deberá** programarlas con anticipación al momento comprometido, en lugar de ejecutarlas cuando el contenedor se solicita.
**Actor:** solución. **Precondición:** compromiso registrado con hora acordada y posición del contenedor conocida.
**Resultado esperado:** remociones ejecutadas antes del momento comprometido; el contenedor está accesible a la hora.
**Origen:** CP, Cap. 4.7 (el atraso ocurre «porque estaba abajo de otros tres **y la remoción no se programó**») · Decisión N° 21 · CP, Cap. 18, criterios 8 y 10.
**Criterio de aceptación:** sobre una muestra de compromisos con hora acordada, se acredita que la remoción necesaria se programó y ejecutó antes de esa hora, y se mide el porcentaje de compromisos incumplidos.
 
---
 
**`RF-PAT-12` — Consulta de posición de contenedor** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** responder la consulta de posición de cualquier contenedor del inventario, entregando bloque, bahía, fila, altura y estado de confianza.
**Actor:** supervisor, planificador, operador de gate y persona usuaria externa autorizada. **Precondición:** contenedor en inventario.
**Resultado esperado:** posición y confianza entregadas sin búsqueda física.
**Origen:** CP, Cap. 15, RT-09.01 (consulta de posición no superior a 1 segundo) · CP, Cap. 18, criterio 9 · meta propuesta: cero búsquedas físicas como proceso normal.
**Criterio de aceptación:** se mide el porcentaje de retiros que requirieron búsqueda física contra el umbral residual de 0,5 %, y el tiempo de esa búsqueda residual contra el objetivo de 15 minutos.
 
---
 
**`RF-PAT-13` — Cobertura total de instrumentación de equipos** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** operar con la totalidad de los equipos de patio instrumentados, y **no deberá** admitir el registro de movimientos por radio como mecanismo permanente.
**Actor:** solución. **Precondición:** equipos instrumentados conforme a la especificación de hardware entregada al CLIENTE.
**Resultado esperado:** ningún equipo opera fuera del registro automático.
**Origen:** CP, Cap. 5 («la cobertura parcial es una de las causas del 3,1 % de contenedores mal ubicados») · Decisión N° 15 · meta propuesta: 18 de 18 al cierre del desarrollo de Etapa 1 · CP, Cap. 11, exclusión 9 (Terabyte especifica el hardware; el CLIENTE lo adquiere).
**Criterio de aceptación:** se verifica que los 18 equipos registran movimientos por telemetría y que ninguno depende de confirmación por radio.
 
---
 
**`RF-PAT-14` — Registro de movimientos por hora y por equipo** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar cada movimiento con su instante, su equipo y su persona operadora asignada, de modo que la productividad sea calculable por hora y por equipo sin consolidación manual.
**Actor:** solución. **Precondición:** movimiento registrado por telemetría.
**Resultado esperado:** serie de movimientos con granularidad por hora y por equipo.
**Origen:** CP, 7.1 («registro del detalle de movimientos por hora y por grúa: inexistente») · CP, Cap. 18, criterio 6 · CP, Cap. 15, RT-05.29 (indicadores de productividad en tiempo real, con granularidad por hora y por equipo).
**Criterio de aceptación:** se consulta la productividad de una hora y un equipo determinados y se desciende hasta los movimientos individuales que la componen.
 
---
 
# Dominio `RF-REF` — Patio refrigerado y cadena de frío
 
Etapa 1, como capacidad nueva. Trece requerimientos. Es el dominio de máxima reversibilidad —volver a la ronda a pie— y el que responde al evento del 18 de febrero de 2026.
 
---
 
**`RF-REF-01` — Muestreo local en el borde** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** muestrear localmente, en el borde, la temperatura, el estado de conexión y el consumo de cada toma refrigerada, con un intervalo de **entre 1 y 5 minutos**.
**Actor:** solución. **Precondición:** toma instrumentada.
**Resultado esperado:** serie local de alta resolución disponible para detección y para respaldo.
**Origen:** Decisión N° 8, modelo de dos capas · CP, 16.1 decisión 8 («la diferencia entre 1 minuto y 15 minutos es la diferencia entre detectar y no detectar el evento del 18 de febrero»).
**Criterio de aceptación:** se verifica sobre una muestra de tomas que el intervalo de muestreo local se mantiene dentro del rango declarado durante 24 horas continuas.
 
---
 
**`RF-REF-02` — Agregación en el borde y reporte al núcleo** · Prioridad: **Alta**
 
**Descripción.** El componente de borde **deberá** agregar y prefiltrar localmente las lecturas y reportarlas al núcleo con un intervalo de **entre 5 y 15 minutos**, y **no deberá** transmitir el dato crudo de las 2.400 tomas de forma continua.
**Actor:** solución. **Precondición:** muestreo local operativo.
**Resultado esperado:** carga de red acotada, sin pérdida de capacidad de detección.
**Origen:** Decisión N° 8, ajustada tras la investigación de práctica de la industria · BTT, RT-03.19 (procesamiento en el borde).
**Criterio de aceptación:** se mide el volumen transmitido al núcleo y se verifica que el intervalo de reporte se mantiene dentro del rango, sin que la detección de excepción se retrase.
 
---
 
**`RF-REF-03` — Envío inmediato ante excepción** · Prioridad: **Crítica**
 
**Descripción.** Ante cualquier excepción o condición de alarma, el componente de borde **deberá** transmitirla de inmediato al núcleo, sin esperar el ciclo de reporte agregado.
**Actor:** solución. **Precondición:** excepción detectada localmente.
**Resultado esperado:** la excepción llega al núcleo fuera del ciclo periódico.
**Origen:** Decisión N° 8 · CP, Cap. 15, RT-05.29 (alarma no superior a 5 minutos desde el evento físico).
**Criterio de aceptación:** se inyecta una falla controlada y se mide el tiempo entre el evento físico y la alarma generada, contra el umbral de RNF-DES-04.
 
---
 
**`RF-REF-04` — Detección de desviación de temperatura** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** detectar la desviación de la temperatura de un contenedor respecto de su **temperatura de consigna declarada**, y **deberá** generar la alarma correspondiente.
**Actor:** solución. **Precondición:** contenedor conectado con consigna registrada.
**Resultado esperado:** desviación detectada y alarmada.
**Origen:** CP, Cap. 4.5 (la consigna depende de la carga: «la cereza no es el salmón») · CP, Cap. 18, criterio 11 · CP, Cap. 15, RT-05.29.
**Criterio de aceptación:** se simula una desviación sobre una muestra de tomas y se verifica que la alarma se genera para el 100 % de ellas dentro del umbral.
 
---
 
**`RF-REF-05` — Detección de desconexión de toma** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** detectar la desconexión de un contenedor refrigerado de su toma y **deberá** generar alarma, con independencia de que la temperatura aún no se haya desviado.
**Actor:** solución. **Precondición:** contenedor previamente conectado.
**Resultado esperado:** desconexión alarmada antes de que la carga se degrade.
**Origen:** CP, Cap. 15, RT-05.29 (alarma «de desconexión o de desviación») · CP, Cap. 4.5 (la inercia térmica retrasa la manifestación de la desconexión).
**Criterio de aceptación:** se desconecta una toma en condiciones controladas y se verifica que la alarma se genera sin esperar la desviación de temperatura.
 
---
 
**`RF-REF-06` — Detección de falla de tablero** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** detectar la falla de un tablero de distribución completo como **evento propio**, distinguiéndolo de la desconexión individual de las tomas que dependen de él.
**Actor:** solución. **Precondición:** tablero instrumentado.
**Resultado esperado:** una alarma de tablero, no una avalancha de alarmas individuales indistinguibles.
**Origen:** CP, Cap. 4.5 y Cap. 1: el evento del 18 de febrero fue la falla de **un tablero completo**, con 38 contenedores afectados durante 9 horas · CP, 7.2 (0 de 26 tableros con alarma remota).
**Criterio de aceptación:** se simula la falla de un tablero y se verifica que se genera una alarma de tablero identificada como tal, con el listado de tomas afectadas.
 
---
 
**`RF-REF-07` — Distinción entre sensor caído y condición estable** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** distinguir un sensor que dejó de reportar de una toma cuya temperatura se mantiene estable, y **deberá** alarmar la ausencia de dato como condición propia.
**Actor:** solución. **Precondición:** toma instrumentada con serie previa.
**Resultado esperado:** la ausencia de lectura no se interpreta como normalidad.
**Origen:** Decisión N° 8, que descarta la transmisión de solo desviaciones precisamente porque «no distingue un sensor caído de una temperatura estable».
**Criterio de aceptación:** se interrumpe la señal de un sensor y se verifica que la solución genera alarma de ausencia de dato dentro del intervalo declarado.
 
---
 
**`RF-REF-08` — Notificación simultánea a dos destinatarios** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** enviar cada alarma del patio refrigerado **simultáneamente** al operador de turno y a un supervisor de guardia, por canal redundante, en cualquiera de los tres turnos.
**Actor:** solución. **Precondición:** alarma generada.
**Resultado esperado:** dos destinatarios notificados por canales independientes.
**Origen:** Decisión N° 10 · CP, Cap. 15, RT-16.21 (alarmas redundantes con escalamiento y confirmación, notificaciones multicanal) · BTT, RT-16.20.
**Criterio de aceptación:** se genera una alarma en turno de madrugada y se verifica la recepción por ambos destinatarios y por ambos canales.
 
---
 
**`RF-REF-09` — Escalamiento automático ante falta de confirmación** · Prioridad: **Crítica**
 
**Descripción.** Si ninguno de los destinatarios confirma la recepción dentro del plazo declarado, la solución **deberá** escalar automáticamente a un tercer contacto.
**Actor:** solución. **Precondición:** alarma emitida sin confirmación dentro del plazo.
**Resultado esperado:** escalamiento ejecutado sin intervención humana.
**Origen:** Decisión N° 10 · CP, 16.1 decisión 10 («una alarma que nadie atiende es exactamente el resultado del 18 de febrero, sólo que con más registros») · BTT, RT-16.11 (escalamiento automático por vencimiento).
**Criterio de aceptación:** simulacro de no respuesta del primer y del segundo destinatario, verificando la activación del tercer contacto dentro del plazo.
 
---
 
**`RF-REF-10` — Registro auditable de la confirmación** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar quién confirmó cada alarma, por qué canal y en qué instante, y **deberá** conservar ese registro como evidencia auditable.
**Actor:** operador o supervisor. **Precondición:** alarma emitida.
**Resultado esperado:** trazabilidad completa de la atención de cada alarma.
**Origen:** Decisión N° 10 · CP, 16.1 decisión 10 («qué ocurre si nadie confirma») · BTT, RT-16.06 · articula con RNF-DIS-08 (100 % de alarmas con confirmación registrada).
**Criterio de aceptación:** se consulta una alarma cualquiera del período y se recupera el autor, el canal y el instante de su confirmación, o la constancia de que se escaló por falta de ella.
 
---
 
**`RF-REF-11` — Serie continua de temperatura por contenedor** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** mantener una serie continua de temperatura por cada contenedor refrigerado, desde su conexión hasta su desconexión, con retención de **cinco años**.
**Actor:** solución. **Precondición:** contenedor conectado a toma instrumentada.
**Resultado esperado:** serie íntegra, sin lagunas atribuibles al sistema.
**Origen:** CP, Cap. 15, RT-05.10 (series de temperatura de carga refrigerada: 5 años, como evidencia de cadena de frío) · CP, Cap. 18, criterio 12 · meta propuesta: 100 % de los contenedores refrigerados con serie continua.
**Criterio de aceptación:** se audita la serie de una muestra de contenedores verificando continuidad desde conexión hasta desconexión, y se comprueba la recuperación de una serie de cinco años de antigüedad.
 
---
 
**`RF-REF-12` — Entrega de la evidencia de cadena de frío** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir al cliente y a la autoridad obtener la serie de temperatura de un contenedor como **documento entregable en formato abierto**, por autoservicio.
**Actor:** exportador, importador, agencia o autoridad. **Precondición:** serie registrada y persona usuaria autorizada.
**Resultado esperado:** evidencia de cadena de frío obtenida sin intervención del terminal.
**Origen:** CP, Cap. 9.5 (registro «entregable como evidencia de cadena de frío al cliente y a la autoridad») · CP, Cap. 12, materia 9 · BTT, RT-16.32 · supuesto de alcance del autoservicio, trámite 5.
**Criterio de aceptación:** una persona usuaria externa autorizada descarga la serie de un contenedor en formato abierto, sin contacto con el terminal.
 
---
 
**`RF-REF-13` — Registro de horas de conexión como hecho facturable** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** derivar las horas de conexión refrigerada facturables de los **eventos de conexión y desconexión registrados por la instrumentación**, y **no deberá** calcularlas a partir de la planilla de ronda.
**Actor:** solución. **Precondición:** eventos de conexión y desconexión registrados.
**Resultado esperado:** hecho facturable con evidencia verificable, generado en el momento en que ocurre.
**Origen:** CP, Cap. 4.8 (hoy la conexión refrigerada se calcula «con las horas que estuvo conectado según la planilla de la ronda») · Decisión N° 11 · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** se contrasta una muestra de horas facturadas contra los eventos de instrumentación que las originan, verificando que ninguna proviene de registro manual. Se articula con el dominio `RF-FAC`.
 
---
 
## Trazabilidad del bloque
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos que lo sostienen |
|---|---|
| 8 — Remociones bajan de forma medible | `RF-PAT-06`, `07`, `08`, `11` |
| 9 — Posición coincide con la real; sin búsquedas físicas | `RF-PAT-01` a `05`, `12`, `13` |
| 11 — Desconexión o desviación detectada en minutos | `RF-REF-01` a `10` |
| 12 — Registro continuo de temperatura entregable | `RF-REF-11`, `12` |
| 6 — Productividad medida por hora y equipo *(parcial)* | `RF-PAT-14` |
| 10 — Contenedor de inspección disponible a la hora *(parcial)* | `RF-PAT-11` |
| 14 — Hechos facturables con evidencia *(parcial)* | `RF-REF-13` |
 
| Indicador de línea base (CP, 7.2) | Meta propuesta | Requerimientos que lo mueven |
|---|---|---|
| Remociones 18 % | ≤ 14 % | `RF-PAT-06`, `07`, `08`, `11` |
| Contenedores mal ubicados 3,1 % | ≤ 0,5 % | `RF-PAT-01` a `04`, `13` |
| Búsqueda física 40 min | cero como proceso normal | `RF-PAT-03`, `12` |
| Terminales montadas 12 de 18 | 18 de 18 | `RF-PAT-13` |
| Intervalo de control reefer 4 h | ≤ 5 min | `RF-REF-01`, `03` |
| Tomas instrumentadas 0 de 2.400 | 2.400 de 2.400 | `RF-REF-01`, `04`, `05` |
| Tableros con alarma 0 de 26 | 26 de 26 | `RF-REF-06` |
| Registro continuo de temperatura: inexistente | 100 % con serie continua | `RF-REF-11`, `12` |
| Inspecciones atrasadas 28 % *(parcial)* | ≤ 8 % | `RF-PAT-11` |
 
**Total del bloque: 27 requerimientos** — 14 en `RF-PAT`, 13 en `RF-REF`.
**Acumulado del catálogo: 53 requerimientos** en cuatro dominios.
 
---
 
## Pendientes transversales del catálogo
 
Lista acumulativa. Se arrastra entre bloques y se resuelve en la Fase 4.
 
| # | Pendiente | Origen |
|---:|---|---|
| 1 | **Fundamentar las once metas propuestas con literatura arbitrada o casos documentados**, usando búsqueda académica. Las metas 1 (remociones) y 11 (inspecciones) son las que más lo necesitan: la primera descansa en una cifra de proveedor no verificada de forma independiente, la segunda en un dato que el CLIENTE no declaró | Solicitud de Rodolfo Fernández · CP, Cap. 16.2 exige investigación sectorial con fuentes preferentemente primarias, académicas, normativas o de fabricante |
| 2 | **Ratificar `RF-PAT-10`** (vía de excepción del operador), que resuelve un hueco reconocido por la propia Decisión N° 3 pero no cubierto por ninguna decisión vigente | Bloque 2 |
| 3 | **Evitar la duplicación entre `RF-GAT-14` y el dominio `RF-OPD`** al redactar este último | Bloque 1 |
| 4 | **Verificar el mapeo entre los 107 códigos RT no funcionales del BTT y los 77 RNF del catálogo** al construir el Formulario T-12 | Vacío 6 de la Fase 2 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*