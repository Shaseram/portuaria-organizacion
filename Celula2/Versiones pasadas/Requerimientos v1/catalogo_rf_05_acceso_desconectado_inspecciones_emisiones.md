# Catálogo de Requerimientos Funcionales — Bloque 5 (cierre)
 
## Dominios `RF-ACC`, `RF-OPD`, `RF-INS` y `RF-EMI`
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento:** 3 — Esquema de solución y alcance
> **Formato y convención:** los declarados en `claude/plan_catalogo_rf_subdocumento3.md`, Fase 0.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado:** borrador de Célula 2. Cierra la Fase 3. Pendiente de las dos pasadas de la Fase 4.
 
**Cobertura de este bloque:** criterios de aceptación 10, 16, 17 y 18 (CP, Cap. 18); Decisiones N° 12, 13, 16, 17, 20 y 21.
 
---
 
# Dominio `RF-ACC` — Identidad, habilitación y acceso de personas
 
Etapa 1. Diez requerimientos. Dominio gobernado por dos restricciones simultáneas: el plan de protección portuaria exige control efectivo, y los acuerdos sindicales prohíben la biometría obligatoria.
 
---
 
**`RF-ACC-01` — Credencial temporal vinculada a la nombrada** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** emitir al trabajador eventual una **credencial de acceso temporal vinculada a su asignación de turno**, generada al confirmarse la nombrada, y **no deberá** exigir un proceso de habilitación individual previo distinto del que los acuerdos vigentes contemplan.
**Actor:** solución y trabajador portuario eventual. **Precondición:** nombrada del turno confirmada.
**Resultado esperado:** habilitación disponible al inicio del turno, sin trámite individual que retrase el ingreso.
**Origen:** Decisión N° 12 · CP, Cap. 10, restricción no negociable N° 8 · CP, Cap. 4.9 (hoy la habilitación «se maneja con listados que se entregan en portería») · CP, Cap. 2.4 (hasta 380 eventuales por turno, ~2.100 personas distintas al año).
**Criterio de aceptación:** se mide el tiempo de emisión y entrega de credenciales para un turno de 380 eventuales, verificando que ninguno inicia su turno con retraso atribuible al sistema.
 
---
 
**`RF-ACC-02` — Expiración automática de la credencial** · Prioridad: **Crítica**
 
**Descripción.** La credencial temporal **deberá** expirar automáticamente al cierre del turno para el que fue emitida, sin requerir acción de revocación.
**Actor:** solución. **Precondición:** credencial emitida con turno asociado.
**Resultado esperado:** ninguna credencial de eventual permanece activa fuera de su turno.
**Origen:** Decisión N° 12, compensadores de riesgo · CP, Cap. 2.4 (rotación diaria) · BTT, RT-12.07 (duración máxima y revocación).
**Criterio de aceptación:** se verifica que ninguna credencial emitida para un turno permite el ingreso una vez cerrado ese turno.
 
---
 
**`RF-ACC-03` — Zonificación del acceso** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** autorizar el acceso por **área, rol y ventana de tiempo**, y **no deberá** conceder acceso general al recinto por el solo hecho de la habilitación.
**Actor:** solución. **Precondición:** persona habilitada con faena asignada.
**Resultado esperado:** cada persona accede únicamente a las zonas que su faena requiere.
**Origen:** Decisión N° 12, compensadores de riesgo · CP, Cap. 10, restricción no negociable N° 7 (plan de protección) · CP, Cap. 12, materia 2 · BTT, RT-12.05.
**Criterio de aceptación:** se intenta acceder a una zona no autorizada con credencial vigente y el sistema lo deniega, registrando el intento.
 
---
 
**`RF-ACC-04` — Habilitación sin biometría obligatoria** · Prioridad: **Crítica**
 
**Descripción.** La solución **no deberá** exigir enrolamiento biométrico como condición de habilitación de ninguna persona. La solución **podrá** ofrecer biometría de forma **voluntaria y con consentimiento explícito**, sin que su rechazo afecte la habilitación.
**Actor:** trabajador eventual y personal propio. **Precondición:** ninguna.
**Resultado esperado:** habilitación plena por vía no biométrica; la biometría es una comodidad opcional, no un requisito.
**Origen:** CP, Cap. 10, restricción no negociable N° 8 («la biometría obligatoria está expresamente objetada») · CP, Cap. 15, RT-12.11 · Decisión N° 12 · articula con RNF-SEG-10.
 
> La Decisión N° 12 advierte que esta opción **no es la práctica dominante de la industria**, y que por eso debe quedar justificada de forma explícita por el driver sindical del caso y compensada con los controles de `RF-ACC-02`, `03`, `09` y `10`.
 
**Criterio de aceptación:** se completa el ciclo de habilitación de un eventual sin dato biométrico alguno, y se verifica que quien rechaza la biometría voluntaria conserva idéntica habilitación.
 
---
 
**`RF-ACC-05` — Verificación de habilitación vigente** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** verificar, antes de emitir la credencial, que la persona cuenta con las acreditaciones vigentes que su faena exige, y **deberá** denegar la emisión registrando el motivo cuando alguna falte.
**Actor:** solución. **Precondición:** persona asignada a una faena con acreditaciones definidas.
**Resultado esperado:** nadie ingresa a una faena para la que no está acreditado.
**Origen:** CP, Cap. 4.9 (hoy la verificación de credenciales y exámenes vigentes se maneja con listados impresos) · CP, Cap. 12, materia 13 (seguridad y salud en faenas portuarias) · CP, Cap. 10, restricción no negociable N° 7.
**Criterio de aceptación:** se solicita habilitación para una persona con una acreditación vencida y se acredita la denegación con su motivo registrado.
 
---
 
**`RF-ACC-06` — Registro de ingreso y salida por zona** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar el ingreso y la salida de cada persona al recinto y a cada zona controlada, con identidad, habilitación y instante.
**Actor:** solución. **Precondición:** persona con credencial vigente en un punto de control.
**Resultado esperado:** presencia conocida y no aproximada.
**Origen:** Decisión N° 13 · CP, Cap. 18, criterio 17 · CP, Cap. 4.9 («saber cuántas hay, quiénes son y dónde están es hoy una respuesta aproximada»).
**Criterio de aceptación:** sobre un turno de peak con hasta 1.100 personas, el registro reconstruye la nómina de presentes por zona en cualquier instante del turno.
 
---
 
**`RF-ACC-07` — Conteo y ubicación por zona en emergencia** · Prioridad: **Crítica**
 
**Descripción.** Ante una emergencia, la solución **deberá** entregar el número de personas presentes, su identidad y la **zona general** en que se encuentran, y **no deberá** mantener geolocalización individual continua dentro del patio.
**Actor:** protección portuaria y prevención de riesgos. **Precondición:** emergencia declarada.
**Resultado esperado:** respuesta inmediata a «quién está adentro y bajo qué condición», sin rastreo individual.
**Origen:** Decisión N° 13, que descarta la geolocalización continua por desproporcionada · CP, Cap. 18, criterio 17 · CP, Cap. 12, materia 11 (Ley N° 21.719) · CP, Cap. 10, restricción no negociable N° 8.
**Criterio de aceptación:** simulacro de emergencia durante la marcha blanca, contrastando el conteo entregado por el sistema contra el conteo físico en punto de reunión.
 
---
 
**`RF-ACC-08` — Conteo operativo sin conectividad** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** seguir registrando ingresos, salidas y conteo durante una pérdida de conectividad, y **deberá** resincronizar al restablecerse sin perder ningún registro.
**Actor:** solución. **Precondición:** conectividad no disponible en el punto de control.
**Resultado esperado:** el conteo de emergencia funciona precisamente cuando la infraestructura falla.
**Origen:** CP, Cap. 10, restricción no negociable N° 4 · BTT, RT-03.11 · articula con el dominio `RF-OPD`.
 
> Una emergencia es un escenario en que la conectividad puede ser lo primero que falle. Un conteo que depende del enlace no sirve para el caso que justifica su existencia.
 
**Criterio de aceptación:** se ejecuta el simulacro de `RF-ACC-07` con el enlace deliberadamente caído, verificando conteo correcto y resincronización íntegra al reconectar.
 
---
 
**`RF-ACC-09` — Auditoría de cada acceso** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar de forma auditable cada acceso concedido y cada acceso denegado, con identidad, zona, instante y motivo, y **no deberá** limitar la auditoría al acto de enrolamiento.
**Actor:** solución. **Precondición:** intento de acceso en un punto de control.
**Resultado esperado:** traza completa de accesos, no solo de altas de credencial.
**Origen:** Decisión N° 12, compensadores de riesgo («traza de auditoría de cada acceso, no solo del enrolamiento») · BTT, RT-12.09 · CP, Cap. 15, RT-16.09.
**Criterio de aceptación:** se consulta la auditoría de un período y se recuperan tanto los accesos concedidos como los denegados, con su motivo.
 
---
 
**`RF-ACC-10` — Minimización y retención de datos personales** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** tratar únicamente los datos personales necesarios para la habilitación, el control de acceso y la respuesta ante emergencia, y **deberá** aplicar el plazo de retención declarado para los registros de acceso.
**Actor:** solución. **Precondición:** tratamiento de datos personales activo.
**Resultado esperado:** cumplimiento demostrable frente a la Ley N° 21.719 y frente a la objeción sindical.
**Origen:** CP, Cap. 12, materia 11 · CP, Cap. 15, RT-05.10 (registros de acceso de personas: 5 años) · CP, Cap. 15, RT-11.10 · Decisión N° 13 · articula con RNF-CUM-03 y RNF-SEG-05.
**Criterio de aceptación:** auditoría del registro de actividades de tratamiento contra las bases de licitud declaradas, verificando que ningún dato recolectado excede la finalidad declarada.
 
---
 
# Dominio `RF-OPD` — Operación desconectada y sincronización
 
Etapa 1. Ocho requerimientos.
 
> **No duplicación.** La operación del gate en modo desconectado está redactada en `RF-GAT-14`. Este dominio la generaliza al resto de la operación y no la repite.
 
---
 
**`RF-OPD-01` — Operación completa sin enlace exterior** · Prioridad: **Crítica**
 
**Descripción.** El componente on-premise **deberá** sostener la operación completa del terminal —atención de nave, registro de movimientos, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables— durante al menos **72 horas continuas** sin enlace hacia el exterior.
**Actor:** solución. **Precondición:** enlace exterior no disponible.
**Resultado esperado:** operación íntegra, no reducida a consulta.
**Origen:** CP, Cap. 15, RT-03.10 · CP, Cap. 10, restricción no negociable N° 4 · CP, Cap. 18, criterio 18 · articula con RNF-DIS-02 y con la Decisión N° 20.
**Criterio de aceptación:** simulacro de corte de enlace de 72 horas en ambiente controlado, verificando las cinco funciones y la ausencia de pérdida de registros.
 
---
 
**`RF-OPD-02` — Registro local íntegro durante la desconexión** · Prioridad: **Crítica**
 
**Descripción.** Durante la desconexión, la solución **deberá** registrar localmente todas las transacciones operacionales críticas con integridad garantizada, y **no deberá** perder ningún movimiento ni ningún hecho facturable.
**Actor:** solución. **Precondición:** operación en modo desconectado.
**Resultado esperado:** registro local completo y recuperable.
**Origen:** BTT, RT-03.11 · CP, Cap. 15, RT-03.13 · CP, Cap. 10, restricción no negociable N° 4 («sin perder el registro de lo ocurrido»).
**Criterio de aceptación:** se contabilizan las transacciones generadas durante el simulacro y se verifica su presencia íntegra en el registro local.
 
---
 
**`RF-OPD-03` — Operación de terminales de equipo fuera de cobertura** · Prioridad: **Crítica**
 
**Descripción.** Las terminales montadas en los equipos de patio **deberán** sostener al menos **8 horas continuas** fuera de cobertura inalámbrica sin pérdida de registro de movimientos.
**Actor:** operador de equipo de patio. **Precondición:** equipo fuera de cobertura.
**Resultado esperado:** el turno completo se registra aunque la cobertura falle.
**Origen:** CP, Cap. 15, RT-03.10 · Decisión N° 9, que identifica la cobertura como el punto donde «más instalaciones piloto de esta industria han fracasado» · articula con RNF-DIS-03.
**Criterio de aceptación:** prueba de campo con desconexión deliberada en zona de patio cargado durante 8 horas, verificando integridad de los registros al reconectar.
 
---
 
**`RF-OPD-04` — Sincronización automática tras la reconexión** · Prioridad: **Crítica**
 
**Descripción.** Restablecido el enlace, la solución **deberá** sincronizar automáticamente en no más de **90 minutos** tras 72 horas de desconexión, y **no deberá** requerir intervención manual.
**Actor:** solución. **Precondición:** enlace restablecido tras desconexión.
**Resultado esperado:** consistencia total restituida dentro del plazo, sin operador.
**Origen:** CP, Cap. 15, RT-03.13 · BTT, RT-03.12 · articula con RNF-DIS-04.
**Criterio de aceptación:** se mide el tiempo hasta consistencia total tras el simulacro de 72 horas, contra el umbral de 90 minutos, verificando ausencia de intervención manual.
 
---
 
**`RF-OPD-05` — Resolución determinista de conflictos de posición** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** resolver los conflictos de posición de contenedor producidos durante la desconexión aplicando una **regla determinista documentada**, y **no deberá** dejar la resolución a criterio del operador ni a un orden de llegada arbitrario.
**Actor:** solución. **Precondición:** conflicto de posición detectado durante la sincronización.
**Resultado esperado:** misma entrada, misma resolución, de forma reproducible.
**Origen:** CP, Cap. 15, RT-03.13 («resolución determinista de los conflictos de posición de contenedor producidos durante la desconexión») · BTT, RT-03.12.
**Criterio de aceptación:** se inyecta el mismo conjunto de conflictos en dos ejecuciones independientes y se verifica que la resolución es idéntica.
 
---
 
**`RF-OPD-06` — Bitácora auditable de las decisiones de resolución** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** dejar bitácora auditable de cada conflicto resuelto durante la sincronización, indicando el conflicto, la regla aplicada y el resultado.
**Actor:** solución. **Precondición:** sincronización ejecutada con conflictos resueltos.
**Resultado esperado:** cada resolución automática es revisable después.
**Origen:** BTT, RT-03.12 («deja bitácora auditable de las decisiones aplicadas») · BTT, RT-05.03.
**Criterio de aceptación:** tras una sincronización con conflictos, se recupera la bitácora completa con regla y resultado por cada conflicto.
 
---
 
**`RF-OPD-07` — Indicación del modo degradado** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** informar a la persona usuaria que está operando en modo desconectado y qué funciones no están disponibles, y **no deberá** presentar el modo degradado como operación normal ni fallar de forma total.
**Actor:** persona usuaria de terreno y de oficina. **Precondición:** operación en modo degradado.
**Resultado esperado:** la persona sabe en qué régimen trabaja y qué no puede hacer.
**Origen:** BTT, RT-02.09 (degradación elegante que informa a la persona usuaria) · BTT, RT-13.06 · articula con RNF-USA-07.
**Criterio de aceptación:** se induce el modo degradado y se verifica que cada interfaz afectada lo indica explícitamente y enumera las funciones no disponibles.
 
---
 
**`RF-OPD-08` — Continuidad de los hechos facturables en desconexión** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** generar y conservar localmente los hechos facturables y su evidencia durante la desconexión, y **deberá** incorporarlos íntegramente al reconectar.
**Actor:** solución. **Precondición:** operación en modo desconectado con hechos facturables generándose.
**Resultado esperado:** ningún hecho facturable se pierde por una caída de enlace.
**Origen:** CP, Cap. 15, RT-03.10 (el registro de hechos facturables está entre las funciones que deben continuar) · CP, Cap. 15, RT-03.13 («sin pérdida de ningún movimiento ni de ningún hecho facturable») · articula con `RF-FAC-01`.
**Criterio de aceptación:** se contabilizan los hechos facturables generados durante el simulacro de 72 horas y se verifica su incorporación íntegra tras la sincronización.
 
---
 
# Dominio `RF-INS` — Inspecciones y coordinación con autoridades
 
Etapa 2, apoyado en la programación anticipada de remociones que ya existe desde la Etapa 1 (`RF-PAT-11`). Siete requerimientos. Materializa la **Decisión N° 21**.
 
---
 
**`RF-INS-01` — Recepción normalizada de la selección** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** recibir la selección de contenedores para inspección de cada autoridad por el canal que esa autoridad tenga disponible, y **deberá** normalizarla a un **evento interno único de cita de inspección** con autoridad, contenedor, fecha, hora y tipo.
**Actor:** autoridad aduanera, fitosanitaria o sanitaria. **Precondición:** canal de la autoridad identificado en el levantamiento.
**Resultado esperado:** las tres autoridades producen el mismo evento interno, cualquiera sea su canal.
**Origen:** Decisión N° 21 · CP, Cap. 4.7 · CP, Cap. 11, exclusión 7 · CP, Cap. 5 (el «control de inspecciones» debe dejar de vivir en correo y planillas) · articula con `RF-INT-10`.
**Criterio de aceptación:** se recibe una selección por cada uno de los tres canales operativos y se verifica que las tres generan un evento interno equivalente.
 
---
 
**`RF-INS-02` — Registro de la cita con hora acordada** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar la hora acordada y el lugar de cada inspección, y **deberá** mantenerla como compromiso con fecha cierta frente a un tercero con potestad.
**Actor:** solución y área de documentación. **Precondición:** selección recibida.
**Resultado esperado:** compromiso registrado, no una solicitud informal.
**Origen:** CP, Cap. 4.7 («a la hora acordada, el contenedor debe estar en la zona de inspección, abierto, con el inspector presente») · CP, Cap. 3 (zona de inspección) · CP, Anexo B.1 (ventana habitual 08:00 a 18:00).
**Criterio de aceptación:** toda cita registrada presenta hora acordada y lugar, y queda visible para el patio y para la autoridad.
 
---
 
**`RF-INS-03` — Reserva de disponibilidad y programación de la remoción** · Prioridad: **Crítica**
 
**Descripción.** Al registrar la cita, la solución **deberá** evaluar la accesibilidad del contenedor en su posición actual y, cuando no sea accesible, **deberá** programar anticipadamente las remociones necesarias con la holgura declarada antes de la hora acordada.
**Actor:** solución. **Precondición:** cita registrada y posición del contenedor conocida.
**Resultado esperado:** el contenedor está accesible cuando el inspector llega, sin remoción improvisada.
**Origen:** **Decisión N° 21**, que es el núcleo de la decisión · CP, Cap. 4.7 (el atraso ocurre «porque estaba abajo de otros tres **y la remoción no se programó**») · articula con `RF-PAT-11`.
**Criterio de aceptación:** sobre una muestra de citas, se acredita que la remoción necesaria se programó al momento de agendar y se ejecutó antes de la hora acordada.
 
---
 
**`RF-INS-04` — Alerta de riesgo de incumplimiento** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** alertar con anticipación cuando el tiempo restante hasta la hora acordada sea insuficiente para ejecutar la remoción programada, y **deberá** escalar a la supervisión de patio.
**Actor:** solución y supervisor de patio. **Precondición:** cita con remoción pendiente y plazo comprometido.
**Resultado esperado:** el incumplimiento se anticipa en vez de constatarse.
**Origen:** Decisión N° 21, campo de impacto (el riesgo residual son las citas cuyo aviso llega con menos anticipación que el tiempo de remoción) · BTT, RT-16.11 (escalamiento automático por vencimiento).
**Criterio de aceptación:** se agenda una cita con plazo insuficiente y se verifica que la alerta se emite y escala antes de la hora acordada.
 
---
 
**`RF-INS-05` — Registro de la atención de la inspección** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar el inicio y el término de cada inspección atendida, con la autoridad interviniente y su resultado.
**Actor:** inspector y área de documentación. **Precondición:** inspección iniciada.
**Resultado esperado:** trazabilidad completa de la atención, base del acta y del hecho facturable.
**Origen:** Decisión N° 21 · CP, Cap. 12, materias 4 y 7 · articula con `RF-FAC-05`.
**Criterio de aceptación:** se recupera, para una inspección cerrada, su instante de inicio, su instante de término, la autoridad interviniente y su resultado.
 
---
 
**`RF-INS-06` — Acta de inspección con firma electrónica** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** generar el acta de la inspección y **deberá** permitir su firma electrónica conforme a la modalidad que la normativa admita, verificando la validez del certificado al momento de la firma.
**Actor:** inspector y representante del terminal. **Precondición:** inspección atendida y registrada.
**Resultado esperado:** acta firmada y conservable como evidencia.
**Origen:** CP, Cap. 15, RT-16.14 (firma exigible en «las actas de inspección conjunta») · BTT, RT-16.17 y RT-16.18.
 
> **Advertencia.** La expresión «acta de inspección conjunta» **no está definida en ninguna parte del caso**. Este requerimiento se redacta bajo la interpretación más exigente adoptada en `claude/registro_supuestos_complemento_celula2.md`, sección 4: acta de toda inspección en que concurren la autoridad y el terminal. Si la lectura correcta fuera la restringida, el error sería por exceso de cobertura.
 
**Criterio de aceptación:** se genera y firma un acta, verificando la validez del certificado al momento de la firma y la conservación de la evidencia de firma.
 
---
 
**`RF-INS-07` — Medición del cumplimiento de la hora acordada** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** medir el porcentaje de inspecciones atendidas a la hora acordada y **deberá** clasificar cada incumplimiento por su causa.
**Actor:** solución y jefatura de operaciones. **Precondición:** citas registradas y atenciones registradas.
**Resultado esperado:** indicador comparable contra la línea base del 28 % y contra la meta propuesta.
**Origen:** CP, Cap. 18, criterio 10 · CP, 7.2 (28 % de inspecciones atrasadas) · meta propuesta: ≤ 8 %, condicionada al plazo de aviso de las autoridades.
**Criterio de aceptación:** sobre las inspecciones de un período se calcula el porcentaje atendido a la hora acordada y se descompone el incumplimiento por causa.
 
---
 
# Dominio `RF-EMI` — Emisiones y consumo energético
 
Etapa 2, con captura de datos iniciada antes para constituir la serie histórica. Seis requerimientos.
 
---
 
**`RF-EMI-01` — Captura de consumo de los equipos diésel** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** capturar el consumo de combustible de cada uno de los equipos diésel mediante su instrumentación, asociándolo al equipo y al período.
**Actor:** solución. **Precondición:** equipo instrumentado.
**Resultado esperado:** consumo individual por equipo, no prorrateado.
**Origen:** Decisión N° 17 · CP, Cap. 2.3 (18 grúas de patio: 16 diésel y 2 eléctricas incorporadas en 2023) · CP, Cap. 11, exclusión 5.
**Criterio de aceptación:** se contrasta la medición instrumentada acumulada contra el combustible efectivamente facturado a la empresa en el mismo período.
 
---
 
**`RF-EMI-02` — Medición de consumo de los equipos eléctricos** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** medir directamente el consumo energético de los equipos eléctricos, y **no deberá** prorratear el consumo entre equipos de tecnologías distintas.
**Actor:** solución. **Precondición:** equipo eléctrico con medición instalada.
**Resultado esperado:** los dos grupos tecnológicos quedan distinguidos en el cálculo.
**Origen:** Decisión N° 17 · CP, Cap. 11, exclusión 5 («sí considerar que dos equipos ya son eléctricos y que la medición de emisiones debe distinguirlos») · CP, 16.1 decisión 17 (sin medición individual el indicador «se construye sobre un prorrateo objetable por un verificador externo»).
**Criterio de aceptación:** se verifica que el cálculo distingue ambos grupos y que ningún consumo se asigna por prorrateo uniforme.
 
---
 
**`RF-EMI-03` — Cálculo de emisiones por contenedor movilizado** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** calcular las emisiones de gases de efecto invernadero por contenedor movilizado aplicando la **metodología declarada**, con los alcances considerados explicitados.
**Actor:** solución. **Precondición:** consumos capturados y movimientos registrados.
**Resultado esperado:** emisión por contenedor, calculada con método declarado y no estimada.
**Origen:** Decisión N° 16 · CP, Cap. 18, criterio 16 · CP, Cap. 12, materia 10 · CP, 7.3 (emisiones por contenedor: no se mide; referencia: reporte verificado a 2029) · articula con RNF-CUM-09.
**Criterio de aceptación:** se audita una muestra de cálculos contra la metodología declarada, verificando la correcta aplicación de los factores y de los alcances.
 
---
 
**`RF-EMI-04` — Trazabilidad del cálculo hasta el dato de origen** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** permitir descender desde la emisión calculada de un contenedor hasta los **datos de consumo y de movimiento que la originan**.
**Actor:** solución, CLIENTE y verificador externo. **Precondición:** emisión calculada.
**Resultado esperado:** cálculo auditable por un tercero, no una cifra agregada.
**Origen:** CP, Cap. 9.10 («datos trazables hasta su origen y en condiciones de ser verificada por un tercero») · CP, Cap. 18, criterio 16 · BTT, RT-05.26.
**Criterio de aceptación:** se selecciona la emisión de un contenedor y se recuperan los consumos y movimientos que la componen.
 
---
 
**`RF-EMI-05` — Serie histórica para el reporte verificable** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** acumular la serie histórica de emisiones desde el inicio de la captura, de modo que exista base suficiente para el reporte verificado comprometido.
**Actor:** solución. **Precondición:** captura de consumos iniciada.
**Resultado esperado:** serie continua y suficiente antes del hito externo de 2029.
**Origen:** Decisión N° 16, instancia de validación · CP, Cap. 1 (la alianza naviera exige reporte verificado de emisiones a partir de 2029) · Decisión N° 1, sección 5.5 (la captura de datos de emisiones comienza antes para constituir la serie histórica).
 
> La gerenta comercial objetó en CP, 13.1 que las tres condiciones de la alianza naviera quedaron al final del plan y no llegan a 2029. La Decisión N° 1 acogió parcialmente esa objeción adelantando la captura, y este requerimiento la materializa.
 
**Criterio de aceptación:** se verifica que la serie histórica se acumula desde el inicio de la captura, sin interrupciones atribuibles al sistema.
 
---
 
**`RF-EMI-06` — Exportación del reporte para verificación por tercero** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** exportar el reporte de emisiones y sus datos de respaldo en formato abierto y documentado, apto para su verificación por un tercero acreditado.
**Actor:** CLIENTE y verificador externo. **Precondición:** serie histórica disponible.
**Resultado esperado:** verificación externa posible sin intervención del ADJUDICATARIO.
**Origen:** Decisión N° 16 · CP, Cap. 15, RT-05.06 (exportación en formatos abiertos, sin intervención del ADJUDICATARIO) · CP, Cap. 18, criterio 16 · articula con RNF-POR-01.
**Criterio de aceptación:** se exporta el reporte con sus datos de respaldo y un tercero reproduce el cálculo sin asistencia de Terabyte.
 
---
 
## Trazabilidad del bloque
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos que lo sostienen |
|---|---|
| 10 — Contenedor de inspección disponible a la hora acordada | `RF-INS-01` a `04`, `07` · `RF-PAT-11` |
| 16 — Emisiones con método verificable | `RF-EMI-01` a `06` |
| 17 — Se sabe quiénes están adentro y bajo qué habilitación | `RF-ACC-01` a `10` |
| 18 — 72 h sin enlace sin perder registro ni hechos facturables | `RF-OPD-01` a `08` · `RF-GAT-14` |
 
**Total del bloque: 31 requerimientos** — 10 en `RF-ACC`, 8 en `RF-OPD`, 7 en `RF-INS`, 6 en `RF-EMI`.
 
---
 
# Cierre de la Fase 3 — Catálogo completo
 
## Composición
 
| Dominio | Requerimientos | Etapa |
|---|---:|---|
| `RF-CON` — Convivencia con el sistema de 2012 | 11 | 1 |
| `RF-GAT` — Gate, citas, documentación y pesaje | 15 | 1 |
| `RF-PAT` — Patio: posición, movimientos y asignación | 14 | 1 |
| `RF-REF` — Patio refrigerado y cadena de frío | 13 | 1 |
| `RF-NAV` — Nave, planificación y productividad | 14 | 2 *(salvo `RF-NAV-09`, Etapa 1)* |
| `RF-INT` — Integraciones y mensajería | 11 | 2 |
| `RF-FAC` — Hechos facturables y su evidencia | 11 | 2 |
| `RF-POR` — Portal y autoservicio | 8 | 2 |
| `RF-ACC` — Identidad, habilitación y acceso | 10 | 1 |
| `RF-OPD` — Operación desconectada y sincronización | 8 | 1 |
| `RF-INS` — Inspecciones y autoridades | 7 | 2 |
| `RF-EMI` — Emisiones y consumo energético | 6 | 2 |
| **Total** | **128** | |
 
Etapa 1: 72 requerimientos. Etapa 2: 56.
 
## Cobertura de los 22 criterios de aceptación
 
**21 de 22 cubiertos por requerimientos funcionales.** El criterio **19** (segregación de redes) no admite requerimiento funcional por describir un estado y no un comportamiento; queda cubierto por RNF-SEG-06 y por la arquitectura física del Subdocumento 4, conforme se declara en `claude/registro_supuestos_complemento_celula2.md`, sección 5.1.
 
## Cobertura de los 28 indicadores de línea base
 
Los 28 tienen al menos un requerimiento que los mueve, salvo dos declarados expresamente sin meta y sin requerimiento propio: la **ocupación del patio en peak**, que la solución no puede mover y se usa como parámetro de dimensionamiento, y la **pérdida del evento del 18 de febrero**, que es un hecho ocurrido y no una serie.
 
## Lo que queda
 
**Fase 4 — control de calidad.**
 
- Pasada A: IEEE 830 sobre los 128 requerimientos.
- Pasada B: `verificar-citas-bases` sobre el catálogo completo, y revisión de consistencia por un agente que no redactó los requerimientos.
**Fase 5 — salidas derivadas.**
 
- Asignación Etapa 1 / Etapa 2 consolidada, insumo de las secciones 3.4 a 3.6 del Subdocumento 3.
- Columnas base del Formulario T-12.
- Esqueleto de la matriz de trazabilidad.
- Migración del catálogo a `TERABYTE_MATRICES_TECNICAS_INFORME_1.xlsx`.
---
 
## Pendientes transversales del catálogo
 
| # | Pendiente | Origen |
|---:|---|---|
| 1 | Fundamentar las once metas propuestas con literatura arbitrada o casos documentados. Prioritarias: metas 1 (remociones) y 11 (inspecciones) | Solicitud de Rodolfo Fernández · CP, Cap. 16.2 |
| 2 | Ratificar `RF-PAT-10` (vía de excepción del operador) | Bloque 2 |
| 3 | ~~Duplicación entre `RF-GAT-14` y `RF-OPD`~~ — **resuelto**: `RF-OPD` generaliza y no repite | Bloque 5 |
| 4 | Verificar el mapeo entre los 107 códigos RT no funcionales y los 77 RNF, al construir el T-12 | Vacío 6 de la Fase 2 |
| 5 | Confirmar con Célula 3 la factibilidad de lectura desde el sistema de control de las grúas | Bloque 3 |
| 6 | Declarar la versión exacta de cada mensaje de mensajería marítima comprometida, por naviera | Bloque 3 |
| 7 | Confirmar con Célula 4 el tratamiento de la evidencia inalterable de hechos facturables en el modelo de datos | Bloque 4 |
| 8 | **Resolver en el levantamiento de los meses 1 a 4 el plazo de aviso de cada autoridad y la existencia de interfaz electrónica.** De ambos depende la holgura de `RF-INS-03` y la meta del indicador de inspecciones | Bloque 5 · Decisión N° 21 |
| 9 | **Confirmar con Célula 3 la especificación de hardware** que el catálogo presupone: instrumentación de 2.400 tomas y 26 tableros, terminales en 18 equipos, sensores de consumo en 18 equipos de patio, lectores ópticos y pantallas de cabina. CP, Cap. 11 exclusión 9 asigna a Terabyte especificar qué comprar, cuánto y con qué características | Bloque 5 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*