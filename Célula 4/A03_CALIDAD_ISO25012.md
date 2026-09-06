# A-03 — Calidad de datos conforme a ISO/IEC 25012, auditoría y trazabilidad

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Destino en el documento:** § 5.11, con la matriz completa en el Anexo B
**Versión:** 1.0 · 6 de septiembre de 2026
**Modelo de origen:** diagramas v2.1 y diccionario A-02 (80 entidades, 451 atributos)

---

## 0. Por qué este apartado lo escribe Célula 4

La obligación es firme y triple. `BTT, Cap. 5, RT-05.04` exige gestionar la calidad conforme a ISO/IEC 25012, **con validación en el punto de captura**, indicadores de completitud, exactitud y consistencia, y **tablero de calidad disponible para el CLIENTE**. `BA, Art. 23` añade el proceso de saneamiento de los datos migrados. `BA, Art. 13` lista la norma entre los estándares de calidad exigibles al adjudicatario.

El catálogo vigente de 91 requerimientos no funcionales de Célula 2 no la cubre, y Célula 3 la declara pendiente remitiéndola al cruce entre este subdocumento y el plan de pruebas. Es un vacío sin dueño. Célula 4 lo asume por `DEC-C4-11` y propone además, en la sección 9, el texto del requerimiento para que la materia quede trazada en el Formulario T-12.

**Regla autoimpuesta.** No se menciona ISO/IEC 25012 sin control asociado y evidencia. Una mención sin métrica verificable se evalúa como incumplimiento, no como cumplimiento declarativo — y este caso lo dice de forma expresa en su lista de decisiones que no deben tomarse silenciosamente.

---

## 1. Corrección respecto de A-01

El esqueleto y la primera versión del modelo enunciaban *«las seis dimensiones aplicables de ISO/IEC 25012: completitud, exactitud, consistencia, oportunidad, unicidad y trazabilidad»*. Esa lista **no es la de la norma** y hay que corregirla antes de construir sobre ella:

- **La norma define quince características, no seis.**
- **`Unicidad` no es una característica de ISO/IEC 25012.** Pertenece a otros marcos de gestión de datos. En la norma, lo que aquí llamábamos unicidad se expresa como **consistencia** —el mismo hecho no puede estar representado dos veces de forma contradictoria— y se implementa con clave de idempotencia, que es un control, no una dimensión.
- **`Oportunidad` es el nombre correcto de `currentness`**, y sí es una característica de la norma. El término se conserva.

Declararlo importa: un evaluador que conozca la norma detecta de inmediato una lista de dimensiones inventada, y eso contamina la credibilidad del resto del subdocumento. Este documento trabaja con las quince características reales y declara cuáles aplican, cuáles se miden en otro apartado y por qué.

---

## 2. Las quince características y su tratamiento en este caso

| # | Característica | Grupo | Tratamiento en el Subdocumento 5 |
|---:|---|---|---|
| 1 | **Exactitud** | inherente | **Se mide aquí.** Contra verificación física en patio y contra el hecho real en gate y facturación |
| 2 | **Completitud** | inherente | **Se mide aquí.** Atributos obligatorios del diccionario presentes al persistir |
| 3 | **Consistencia** | inherente | **Se mide aquí.** Invariantes del modelo y ausencia de representaciones contradictorias |
| 4 | **Credibilidad** | inherente | **Se mide aquí.** Fuente de registro declarada por movimiento: telemetría, óptica o manual de excepción |
| 5 | **Actualidad** | inherente | **Se mide aquí.** Latencia entre el evento físico y su disponibilidad, contra los umbrales del § 5.6 |
| 6 | **Accesibilidad** | inherente y del sistema | **Se mide aquí.** Recuperación dirigida dentro del plazo de retención de cada clase |
| 7 | **Conformidad** | inherente y del sistema | **Se mide aquí.** Adhesión a los estándares declarados: codificación de contenedores, mensajería sectorial, metodología de emisiones |
| 8 | **Confidencialidad** | inherente y del sistema | Se declara aquí, **se implementa en el § 5.12**: cifrado de campo de los 28 atributos de `DEC-C4-12` y registro de consultas sensibles |
| 9 | **Eficiencia** | inherente y del sistema | **Se hereda del § 5.10.** Es la estrategia de índices, particiones y caché frente a los umbrales de desempeño |
| 10 | **Precisión** | inherente y del sistema | **Se mide aquí.** Resolución declarada por magnitud: temperatura, masa, consumo y posición |
| 11 | **Trazabilidad** | inherente y del sistema | **Se mide aquí.** Sección 7: linaje desde el indicador hasta la transacción y la evidencia |
| 12 | **Comprensibilidad** | inherente y del sistema | **Se cumple con el diccionario A-02**: cada atributo tiene nombre de negocio, dominio de valores y propietario declarados |
| 13 | **Disponibilidad** | del sistema | **Se hereda del § 5.5.** 99,9 % mensual, 72 h de operación desconectada |
| 14 | **Portabilidad** | del sistema | **Se hereda del § 5.12.** Exportación total en formatos abiertos, sin intervención del adjudicatario |
| 15 | **Recuperabilidad** | del sistema | **Se hereda del § 5.5.** RTO ≤ 4 h, RPO ≤ 15 min, respaldo 3-2-1-1-0 |

**Nueve características se miden con reglas y umbrales en este apartado.** Las seis restantes no se omiten: se declaran y se remiten al apartado donde ya están resueltas, para no duplicar compromisos que después divergen. Esa remisión es deliberada y queda escrita, porque una matriz de calidad que repita el 99,9 % de disponibilidad con otro número sería precisamente el tipo de incoherencia que la norma pretende evitar.

---

## 3. Matriz de calidad por dominio

Cada regla declara: qué dato gobierna, qué característica mide, **qué se valida en el punto de captura**, el umbral comprometido, el responsable de la corrección y la evidencia que acredita el control.

### 3.1 DOM-OPS y DOM-PAT — Contenedor, operación, patio y posición

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-01` | `POSICION_VIGENTE.estado_confianza` | Completitud | Toda visita en patio persiste con uno de los dos estados; no se admite posición sin estado | 100 % del inventario | Jefatura de patio | Recuento por turno contra el inventario |
| `CAL-02` | `POSICION_VIGENTE.id_celda` | Exactitud | La posición declarada *conocida* se contrasta contra el barrido físico de un bloque rotativo por turno | Toda posición *conocida* correcta; las *por verificar* no resueltas al cierre de turno ≤ 0,5 % del inventario | Jefatura de patio | Acta de barrido por bloque y turno |
| `CAL-03` | `MOVIMIENTO.fuente_registro` | Credibilidad | Se registra si el movimiento entró por telemetría, lectura óptica o la vía manual de excepción | Vía manual ≤ 2 % de los movimientos, con motivo declarado | Jefatura de operaciones | Distribución por fuente en el tablero |
| `CAL-04` | `MOVIMIENTO.instante` | Actualidad | El instante persistido es el del hecho físico, no el de la digitación; se rechaza un instante posterior al de recepción | Desfase entre hecho y persistencia ≤ 1 s (p95) | Tecnologías de información | Medición de latencia por transacción |
| `CAL-05` | `MOVIMIENTO` (secuencia) | Consistencia | Un movimiento no puede dejar la visita en una celda ocupada por otra visita vigente | 0 colisiones de ocupación | Jefatura de patio | Registro de rechazos con causa |
| `CAL-06` | `ASIGNACION_POSICION.nivel_rn01_determinante` | Trazabilidad | Toda asignación persiste el nivel de la regla que la determinó y, si hubo conflicto, la restricción cedida | 100 % de las asignaciones | Jefatura de operaciones | Muestra dirigida de asignaciones explicadas |
| `CAL-07` | `CONTENEDOR.clase_imdg` frente a `CELDA` | Conformidad | Se rechaza la asignación que infrinja la segregación de la tabla del código internacional de mercancías peligrosas | 0 asignaciones infractoras | Jefatura de operaciones | Registro de rechazos y auditoría de vecindad |
| `CAL-08` | `CONDICION_LIBERACION.liberado` | Consistencia | El valor se recalcula en cada evaluación; no admite escritura directa | 0 escrituras directas | Comercial y operaciones | Auditoría de operaciones sobre el atributo |
| `CAL-09` | `LECTURA_OPTICA.confianza_lectura` | Precisión | La lectura bajo el umbral de confianza no concilia automáticamente: abre tarea de verificación | 100 % de lecturas bajo umbral derivan a verificación | Tecnologías de información | Recuento de lecturas derivadas y resueltas |

### 3.2 DOM-GAT — Gate y transporte terrestre

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-10` | `EVENTO_GATE` | Completitud | Todo turno de camión cierra con evento de entrada y evento de salida | 100 % de turnos con ambos eventos | Jefatura de gate | Conciliación diaria de eventos de barrera |
| `CAL-11` | `TURNO_CAMION.estadia_minutos` | Exactitud | Se deriva de los eventos de barrera; no admite captura manual | 0 estadías capturadas a mano | Jefatura de gate | Auditoría del atributo derivado |
| `CAL-12` | Conciliación de gate | Consistencia | Toda divergencia entre registro nuevo y legado se investiga dentro de la ventana | **Cero diferencias no explicadas al cierre del día**, ventana de 24 h | Jefatura de gate | Acta de conciliación diaria |
| `CAL-13` | `DOCUMENTO_TRANSPORTE.estado_validacion` | Actualidad | La validación es anticipada: se ejecuta antes de la llegada del camión a la barrera | ≥ 90 % de los turnos con documentación validada antes del arribo | Comercial | Distribución de instante de validación contra instante de arribo |
| `CAL-14` | `PESAJE_VGM` | Completitud | Ningún contenedor de exportación se carga sin verificación de masa bruta registrada y trazable | 100 % de contenedores de exportación | Jefatura de gate | Auditoría de muestra contra evidencia física de pesaje |
| `CAL-15` | `PESAJE_VGM.dentro_de_tolerancia` | Precisión | La tolerancia se evalúa sobre el **pesaje vigente**; el repesaje conserva el anterior con su secuencia | 100 % de discrepancias con repesaje o excepción registrada | Jefatura de gate | Serie de pesajes por visita |
| `CAL-16` | `CITA.estado` | Consistencia | El estado se deriva de la ventana de tolerancia declarada, no se marca a mano | 0 estados asignados manualmente | Jefatura de gate | Auditoría de transiciones de estado |

### 3.3 DOM-REF — Reefer y cadena de frío

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-17` | `MUESTRA_TEMPERATURA` | Completitud | La serie es continua entre conexión y desconexión; toda laguna se marca con calidad *ausente* y no se interpola en silencio | Registro continuo para el 100 % de los contenedores refrigerados | Operaciones patio refrigerado | Auditoría de continuidad sobre muestra de contenedores |
| `CAL-18` | `MUESTRA_TEMPERATURA.calidad_dato` | Credibilidad | Se distingue valor válido, interpolado y ausente; el interpolado nunca sustituye al medido | Interpolados ≤ 2 % de la serie | Operaciones patio refrigerado | Distribución de calidad por conexión |
| `CAL-19` | `ALARMA.instante_evento_fisico` frente a `instante_generacion` | Actualidad | Ambos instantes se persisten; la diferencia es el indicador | ≤ 5 minutos desde el evento físico | Operaciones patio refrigerado | Inyección de falla controlada sobre muestra de tomas |
| `CAL-20` | `ALARMA` por ausencia de dato | Completitud | La ausencia de muestra dispara alarma a los tres intervalos o a los cinco minutos, lo que ocurra primero | 0 ventanas ciegas superiores a 5 min | Operaciones patio refrigerado | Prueba de corte de comunicación de una toma |
| `CAL-21` | `ALARMA.id_parametro_aplicado` | Trazabilidad | Cada alarma persiste la versión del parámetro de desviación con que se evaluó | 100 % de alarmas con versión | Jefatura de operaciones | Reproducción de una alarma histórica |
| `CAL-22` | `CONFIRMACION_ALARMA` | Completitud | Toda alarma crítica exige confirmación de persona identificada; sin confirmación en plazo, escala sola | 100 % de alarmas críticas confirmadas o escaladas | Operaciones patio refrigerado | Bitácora de escalamiento |
| `CAL-23` | `MUESTRA_TEMPERATURA.temperatura` | Precisión | Resolución declarada del sensor; el valor fuera del rango físico plausible se marca, no se descarta | Resolución declarada en el diccionario | Mantenimiento eléctrico | Certificado de calibración por lote de tomas |

### 3.4 DOM-NAV — Nave y planificación

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-24` | `CORRECCION_PLAN.motivo_estructurado` | Completitud | El motivo se elige de catálogo cerrado; no se admite texto libre como único registro | 100 % de correcciones con motivo | Planificación | Distribución de motivos por período |
| `CAL-25` | `PLAN_ESTIBA` (versión) | Trazabilidad | Cada versión se conserva; la corrección no sobrescribe la propuesta | 100 % de versiones recuperables | Planificación | Reconstrucción de la secuencia de un plan |
| `CAL-26` | `RECALADA.ventana_confirmada` | Actualidad | La confirmación se registra con su instante; se compara contra el atraque real | Confirmación con ≥ 72 h de antelación | Planificación | Serie de confirmación contra atraque |
| `CAL-27` | `ORDEN_EMBARQUE` e `INSTRUCCION_EMBARQUE` | Conformidad | El mensaje se valida contra la versión de contrato declarada por la contraparte antes de persistirse | 100 % validados; el no conforme va a cola de error con motivo | Tecnologías de información | Registro de rechazos por contraparte |
| `CAL-28` | `INSTRUCCION_EMBARQUE` | Consistencia | La instrucción del embarcador y la orden de la naviera se conservan como objetos distintos, nunca fusionados | 0 fusiones | Comercial | Trazabilidad del indicador de redigitación |

### 3.5 DOM-INS — Inspecciones

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-29` | `CITA_INSPECCION.hora_real_atencion` | Completitud | Toda cita cierra con hora real registrada, incluidas las incumplidas | 100 % de citas con hora real | Cumplimiento normativo | Recuento de citas cerradas |
| `CAL-30` | `CITA_INSPECCION.cumplida_en_hora` | Exactitud | Se deriva de las dos horas; no admite captura | 0 valores capturados a mano | Cumplimiento normativo | Auditoría del atributo derivado |
| `CAL-31` | `ACTA_INSPECCION.id_firma` | Conformidad | El acta se cierra solo con firma electrónica válida en la modalidad que la normativa admita | 100 % de actas firmadas | Cumplimiento normativo | Verificación de firma sobre muestra |
| `CAL-32` | `RETENCION.vigencia_hasta` | Consistencia | Una visita con retención vigente no puede alcanzar el estado liberable | 0 liberaciones con retención vigente | Cumplimiento normativo | Prueba de la invariante sobre casos históricos |

### 3.6 DOM-FAC — Evidencia y facturación

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-33` | `HECHO_FACTURABLE` | Completitud | Todo hecho nace de un evento con instante propio; no se admite creación ni edición manual | 0 hechos creados a mano | Comercial | Auditoría de origen de cada hecho |
| `CAL-34` | `EVIDENCIA` | Completitud | Todo hecho facturable tiene al menos una evidencia asociada al persistirse | Correspondencia 1:1 hecho–evidencia, 100 % | Comercial | Muestra dirigida de recuperación de evidencia |
| `CAL-35` | `EVIDENCIA.sello_integridad` | Credibilidad | El sello se calcula al crear la evidencia y se verifica al recuperarla | 0 evidencias con sello inválido | Seguridad de la información | Verificación de sello sobre muestra |
| `CAL-36` | `HECHO_FACTURABLE.version_regla_aplicada` | Trazabilidad | El hecho persiste la versión exacta de la regla tarifaria con que se valorizó | 100 % de hechos reproducibles | Comercial | Recálculo de un hecho de más de seis meses |
| `CAL-37` | Conciliación de hechos | Consistencia | Conciliación diaria contra el sistema de gestión empresarial | Cero diferencias no explicadas al cierre del día | Comercial y contabilidad | Acta de conciliación diaria |
| `CAL-38` | `OBJECION` | Accesibilidad | La evidencia invocada en una objeción se recupera dentro del plazo de retención | Recuperación ≤ 30 s para evidencia en línea | Comercial | Prueba de recuperación dirigida |

### 3.7 DOM-ACC — Acceso e identidad

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-39` | `EVENTO_ACCESO` | Completitud | Todo ingreso y egreso se registra, incluso sin conectividad, con su instante de borde | 100 % de eventos registrados | Protección portuaria | Conteo por zona contra dotación de la nombrada |
| `CAL-40` | `EVENTO_ACCESO.instante_sincronizacion` | Actualidad | Se distingue el instante del hecho del instante de sincronización | 100 % de eventos sin conectividad con ambos instantes | Protección portuaria | Prueba de operación sin enlace |
| `CAL-41` | `CREDENCIAL_TEMPORAL.vigencia_hasta` | Consistencia | La credencial expira automáticamente al término de la nombrada; no existe credencial sin expiración | 0 credenciales sin fecha de expiración | Protección portuaria | Auditoría de credenciales vigentes |
| `CAL-42` | `HABILITACION.vigente` | Exactitud | Se verifica contra el instante de ingreso, no contra la fecha de emisión | 0 ingresos con habilitación vencida | Personas | Muestra de ingresos contra vigencias |
| `CAL-43` | `PERSONA.documento_identidad` | Confidencialidad | Se persiste cifrado a nivel de campo; la consulta directa a la base no revela su contenido | 100 % de los campos del catálogo de `DEC-C4-12` | Seguridad de la información | Revisión del modelo contra el catálogo |

### 3.8 DOM-EMI — Energía y emisiones

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-44` | `ATRIBUCION_CONSUMO.fraccion_atribuida` | Consistencia | Las fracciones de un mismo consumo suman exactamente 1 | 100 % de consumos con suma 1 | Sostenibilidad | Recuento y suma por ventana de medición |
| `CAL-45` | `EMISION_CONTENEDOR` | Completitud | Todo contenedor movilizado tiene emisión calculada | 100 % de contenedores movilizados | Sostenibilidad | Recuento contra movimientos del período |
| `CAL-46` | `EMISION_CONTENEDOR.version_factor` | Trazabilidad | La emisión persiste la versión del factor y la versión del algoritmo de reparto | 100 % de emisiones reproducibles | Sostenibilidad | Recálculo de una emisión de un período cerrado |
| `CAL-47` | `EMISION_CONTENEDOR.metodologia` | Conformidad | El cálculo declara la norma y la guía aplicadas | 100 % de emisiones con metodología declarada | Sostenibilidad | Informe del verificador externo |

### 3.9 DOM-INT — Integración, autoridad y auditoría

| ID | Dato | Característica | Regla en el punto de captura | Umbral | Responsable | Evidencia |
|---|---|---|---|---|---|---|
| `CAL-48` | `MENSAJE.clave_idempotencia` | Consistencia | La clave es única; un mensaje repetido se descarta y se registra | 0 reprocesos aplicados dos veces | Tecnologías de información | Prueba de reenvío del mismo mensaje |
| `CAL-49` | `MENSAJE.id_correlacion` | Trazabilidad | Todo mensaje lleva el identificador de correlación de extremo a extremo | 100 % de mensajes correlacionados | Tecnologías de información | Seguimiento de una operación de negocio entre sistemas |
| `CAL-50` | `ASIGNACION_AUTORIDAD` | Consistencia | La terna dominio, zona y fase es única en cada instante | 0 solapamientos de autoridad | Gobierno del dato | Prueba de la restricción de unicidad |
| `CAL-51` | `TRANSFERENCIA_AUTORIDAD` | Completitud | Un fallo parcial mantiene la autoridad anterior y bloquea la segunda transferencia | 0 transferencias con autoridad ambigua | Gobierno del dato | Prueba de fallo parcial en cruce de zona |
| `CAL-52` | `DIVERGENCIA_CONCILIACION.clasificacion` | Exactitud | Cada divergencia se clasifica contra verificación física; la que resulta a favor del sistema nuevo no computa | 100 % de divergencias clasificadas dentro de su ventana | Gobierno del dato | Acta de conciliación por turno |
| `CAL-53` | `REGISTRO_AUDITORIA` | Completitud | Toda alta, modificación, baja y consulta sensible genera registro con quién, qué, cuándo, dispositivo y valores anterior y posterior | 100 % de operaciones auditadas | Seguridad de la información | Reconstrucción de un registro cualquiera del período de retención |
| `CAL-54` | `REGISTRO_AUDITORIA.sello_inalterabilidad` | Credibilidad | El sello encadena cada registro con el anterior; ningún perfil puede alterarlo | 0 rupturas de cadena | Seguridad de la información | Verificación de la cadena completa |

---

## 4. Indicadores del tablero de calidad

`RT-05.04` exige indicadores de completitud, exactitud y consistencia **y** un tablero disponible para el CLIENTE. Estos son los doce indicadores que lo componen, con su fórmula. Todos se calculan sobre datos que el modelo ya persiste; ninguno exige captura adicional.

| ID | Indicador | Fórmula | Frecuencia | Regla que lo alimenta |
|---|---|---|---|---|
| `IND-01` | Completitud del inventario | visitas en patio con estado de confianza ÷ visitas en patio | por turno | `CAL-01` |
| `IND-02` | Exactitud de la posición | posiciones *por verificar* no resueltas al cierre ÷ inventario | por turno | `CAL-02` |
| `IND-03` | Credibilidad del registro de movimiento | movimientos por vía manual ÷ movimientos totales | diaria | `CAL-03` |
| `IND-04` | Diferencias no explicadas de gate | divergencias no explicadas al cierre del día | diaria | `CAL-12` |
| `IND-05` | Anticipación documental | turnos con documentación validada antes del arribo ÷ turnos | diaria | `CAL-13` |
| `IND-06` | Continuidad de la cadena de frío | conexiones con serie continua ÷ conexiones activas | diaria | `CAL-17` |
| `IND-07` | Oportunidad de la alarma refrigerada | alarmas generadas en ≤ 5 min ÷ alarmas | por turno | `CAL-19` |
| `IND-08` | Respaldo del hecho facturable | hechos con evidencia recuperable ÷ hechos | diaria | `CAL-34` |
| `IND-09` | Reproducibilidad de la valorización | hechos con versión de regla persistida ÷ hechos | mensual | `CAL-36` |
| `IND-10` | Cobertura de emisiones | contenedores con emisión calculada ÷ contenedores movilizados | mensual | `CAL-45` |
| `IND-11` | Integridad de la auditoría | operaciones auditadas ÷ operaciones ejecutadas | diaria | `CAL-53` |
| `IND-12` | Consistencia de la autoridad del dato | solapamientos de autoridad detectados | por turno | `CAL-50` |

### 4.1 El tablero

**Acceso.** El CLIENTE dispone de cuenta propia y permanente, con exportación en formatos abiertos, conforme a `RNF-OPE-02`. No se entrega como informe periódico enviado por el adjudicatario: se entrega como tablero consultable, que es lo que `RT-05.04` exige.

**Desfase.** Los indicadores por turno se consolidan dentro de la hora siguiente al cierre del turno, alineados con el plazo de los indicadores del concedente. Los diarios, al cierre del día.

**Profundización.** Cada indicador permite descender hasta el registro que lo desvía. Es la misma exigencia que `RT-05.26` impone a los tableros de negocio, aplicada al tablero de calidad: un indicador de calidad que no permite llegar al dato defectuoso no sirve para corregirlo.

**Responsable de corrección.** Cada indicador muestra el rol responsable de la columna correspondiente de la sección 3. Un indicador sin responsable asignado es un informe, no un control.

---

## 5. Validación en el punto de captura

`RT-05.04` no pide validar: pide validar **en el punto de captura**. La diferencia es de arquitectura de datos y hay que declararla.

| Nivel | Qué valida | Dónde ocurre |
|---|---|---|
| Estructural | tipo, dominio de valores y obligatoriedad del diccionario A-02 | en el borde, antes de encolar el evento |
| De dominio | pertenencia a catálogo cerrado y coherencia de unidades | en el borde |
| De integridad | existencia de las entidades referenciadas | en el núcleo, al aplicar el evento |
| De negocio | las veinte invariantes del modelo conceptual | en la transacción, no en un proceso posterior |

**Consecuencia para la operación desconectada.** Durante las 72 horas sin enlace, los dos primeros niveles siguen operando en el borde y los dos últimos se aplican contra el estado local. Un evento que no supera la validación local **no se descarta**: se persiste en cola con su motivo de rechazo, porque perder un movimiento o un hecho facturable está prohibido por `RT-03.13`. La reconciliación posterior los resuelve con su bitácora auditable.

---

## 6. Saneamiento de los datos migrados

`BA, Art. 23` exige proceso de saneamiento de los datos migrados y `BTT, Cap. 5, RT-05.12` exige la etapa de perfilado con **informe de los defectos detectados en el origen y la decisión adoptada sobre cada uno**.

| Clase de defecto esperada | Por qué se espera | Decisión por defecto |
|---|---|---|
| Códigos de contenedor no normalizados | catorce años de operación y digitación manual de once caracteres en el gate | normalizar al estándar de codificación; el no normalizable se migra marcado y se resuelve por verificación física |
| Posiciones de inventario divergentes de la realidad | línea base declarada de 3,1 % de contenedores mal ubicados | **no se migra la posición del legado**: el inventario migra con posición verificada físicamente al corte |
| Maestros duplicados de clientes, transportistas y conductores | cuatro proveedores sucesivos sin gestión de datos maestros | deduplicar por identificador tributario o documento de identidad; el conflicto se resuelve con el dueño del dato, nunca automáticamente |
| Hechos facturables sin evidencia recuperable | el sistema de origen no modela la evidencia como objeto | migrar el hecho marcado como *sin evidencia de origen*; no se fabrica evidencia |
| Series de temperatura en planilla | el registro actual es manual y se digita al día siguiente | migrar como serie de calidad *declarada*, distinguible de la instrumentada |
| Esquemas heredados de versiones anteriores | catorce años y cuatro proveedores | perfilado adelantado a los meses 1 a 4, no a la Etapa 2 |

**Regla que gobierna la tabla:** ningún defecto se corrige inventando el valor correcto. Se normaliza cuando la regla de normalización es determinista, se marca cuando no lo es, y se resuelve con el dueño del dato. La conciliación posterior exige que **toda diferencia quede explicada**, no que no existan diferencias.

---

## 7. Linaje y trazabilidad

### 7.1 Cadena de linaje

`BTT, Cap. 5, RT-05.10` valora un catálogo de datos con linaje automatizado que permita rastrear el origen de cada indicador de negocio hasta su fuente. La cadena, para este modelo, tiene siempre la misma forma:

**indicador publicado → agregación → evento de negocio → registro de origen → dispositivo o persona que lo produjo**

Ejemplo verificable de extremo a extremo, con el indicador contractual más expuesto:

> estadía del camión → `IND` del concedente → `TURNO_CAMION.estadia_minutos` (derivado) → `EVENTO_GATE` de entrada y de salida → barrera del puesto de gate → instante físico del cruce.

Ningún eslabón de esa cadena es una consolidación manual. Es lo que exige la restricción no negociable del caso sobre producir los indicadores en vez de reconstruirlos.

### 7.2 Trazabilidad de la operación

`BTT, Cap. 5, RT-05.03` exige reconstruir **quién, qué, cuándo, desde qué dispositivo y con qué valores anteriores y posteriores**, para cualquier registro y **en cualquier momento del período de retención**. La entidad `REGISTRO_AUDITORIA` persiste los seis elementos, y `CAL-53` mide su cobertura.

Dos exigencias que suelen olvidarse y que aquí quedan explícitas:

- **En cualquier momento del período de retención.** No basta con auditar lo reciente: la reconstrucción debe funcionar sobre un registro de hace nueve años si su clase es de diez. Es un requisito de accesibilidad del archivo, no solo de registro.
- **Inalterable para todo perfil, incluido el administrador de la plataforma** `(BTT, Cap. 16, RT-16.07)`. El sello encadenado de `CAL-54` es lo que lo hace demostrable: no basta con una política de permisos, porque el administrador puede cambiarla.

### 7.3 Registro de consultas sensibles

`CP, Cap. 15, RT-16.09` obliga a registrar el acceso a la información comercial de clientes, a los datos personales y **a la ubicación y contenido declarado de contenedores**, que el caso califica expresamente como sensible por seguridad de la carga. La entidad `CONSULTA_SENSIBLE` lo modela como objeto de negocio y no como efecto colateral de la infraestructura, que es lo que permite responder *quién preguntó dónde estaba ese contenedor y cuándo* durante todo el plazo de retención.

---

## 8. Pruebas de calidad para el plan de pruebas

Célula 3 remitió la materia al cruce entre este subdocumento y el plan de pruebas. Estos son los criterios de aceptación verificables que el Subdocumento 5 entrega al Formulario T-13, y que cierran el pendiente `E-06`.

| ID | Prueba | Criterio de aceptación |
|---|---|---|
| `PRU-01` | Barrido físico de un bloque contra el inventario registrado | Toda posición declarada *conocida* coincide con la realidad |
| `PRU-02` | Inyección de falla de temperatura sobre muestra de tomas | Alarma generada en ≤ 5 min desde el evento físico, con confirmación registrada |
| `PRU-03` | Corte de comunicación de una toma instrumentada | Alarma por ausencia de dato dentro del plazo, sin ventana ciega superior a 5 min |
| `PRU-04` | Recálculo de un hecho facturable de más de seis meses | El monto se reproduce con la versión de regla persistida |
| `PRU-05` | Recuperación dirigida de evidencia en el límite de retención | La evidencia se recupera y su sello verifica |
| `PRU-06` | Reenvío del mismo mensaje de integración | El segundo se descarta por clave de idempotencia y queda registrado |
| `PRU-07` | Fallo parcial en el cruce de zona durante la coexistencia | La autoridad permanece en el sistema de origen; no hay escritura doble |
| `PRU-08` | Operación de 72 h sin enlace y reconexión | Ningún movimiento ni hecho facturable perdido; conflictos resueltos de forma determinista con bitácora |
| `PRU-09` | Consulta directa a la base sobre un campo cifrado | El contenido no es legible |
| `PRU-10` | Intento de alteración del registro de auditoría con perfil administrador | La operación se rechaza y queda auditada |
| `PRU-11` | Verificación de la suma de fracciones de atribución de consumo | Suma exactamente 1 para el 100 % de los consumos del período |
| `PRU-12` | Prueba del límite de retención por clase | El dato se elimina, anonimiza o agrega según su clase, con evidencia de ejecución |

---

## 9. Propuesta de requerimiento no funcional para Célula 2

`DEC-C4-11` asume la materia, pero la trazabilidad del Formulario T-12 exige que cada código `RT` tenga una fila. Se propone a Célula 2 el siguiente requerimiento, redactado con la estructura de su catálogo, para que `RT-05.04` quede trazado:

> **`RNF-CAL-01` · Calidad de datos**
> **Requerimiento:** La solución gestionará la calidad de los datos conforme a ISO/IEC 25012, con validación en el punto de captura, indicadores de completitud, exactitud, consistencia, credibilidad, actualidad, accesibilidad, conformidad, precisión y trazabilidad, y un tablero de calidad de acceso permanente para el CLIENTE con capacidad de profundización hasta el registro defectuoso.
> **Umbral:** 100 % de los dominios de información con reglas de calidad declaradas y responsable de corrección asignado; indicadores disponibles dentro de la hora siguiente al cierre de turno.
> **Verificación:** Auditoría de la matriz de calidad contra el diccionario de datos, y prueba de profundización desde un indicador desviado hasta el registro que lo origina.
> **Prioridad:** Crítica.
> **Origen:** FEP02 Cap. 5, RT-05.04; FEP01 Art. 13 y Art. 23.

Si Célula 2 lo incorpora, `PEN-05` se cierra. Si no lo incorpora, la materia igual queda cubierta en el Subdocumento 5 y la fila del T-12 apunta a este apartado.

---

## 10. Vacíos y pendientes

| Marca | Materia | Responsable |
|---|---|---|
| `PEN-05` | Si el requerimiento propuesto en la sección 9 entra al catálogo de Célula 2 o la materia queda solo en el Subdocumento 5 | Célula 2 |
| `PEN-09` | Los umbrales de `CAL-19` y `CAL-20` dependen del plazo de alarma, que sí está fijado; la **banda** de desviación que dispara la alarma sigue sin valores | Célula 2 y CLIENTE |
| `PEN-02` | `CAL-43` compromete el cifrado de los 28 atributos del catálogo; el mecanismo y su efecto sobre la indexación es de arquitectura de seguridad | Célula 3 |
| Propio | Los umbrales de `CAL-03` (≤ 2 % de registro manual), `CAL-13` (≥ 90 % de anticipación documental) y `CAL-18` (≤ 2 % de interpolados) son **metas propias de Terabyte**, no cifras del caso. Se declaran como tales y se validan con el CLIENTE en la marcha blanca | Célula 4, declarado |

---

## 11. Trazabilidad

| Exigencia | Fuente | Dónde se cumple |
|---|---|---|
| Calidad conforme a ISO/IEC 25012 | `BTT, Cap. 5, RT-05.04` | secciones 2 y 3 |
| Validación en el punto de captura | `BTT, Cap. 5, RT-05.04` | sección 5 |
| Indicadores de completitud, exactitud y consistencia | `BTT, Cap. 5, RT-05.04` | sección 4 |
| Tablero de calidad disponible para el CLIENTE | `BTT, Cap. 5, RT-05.04`; `RNF-OPE-02` | sección 4.1 |
| Saneamiento de los datos migrados | `BA, Art. 23`; `BTT, Cap. 5, RT-05.12` | sección 6 |
| Catálogo de datos con linaje hasta la fuente | `BTT, Cap. 5, RT-05.10` | sección 7.1 |
| Trazabilidad de toda operación de negocio | `BTT, Cap. 5, RT-05.03` | sección 7.2 |
| Registro de auditoría inalterable | `BTT, Cap. 16, RT-16.07` | `CAL-54` y `PRU-10` |
| Registro de consultas a información sensible | `CP, Cap. 15, RT-16.09` | sección 7.3 |
| ISO/IEC 25012 entre los estándares exigibles | `BA, Art. 13` | todo el documento |

---

**Cierre.** Cincuenta y cuatro reglas de calidad con umbral, responsable y evidencia; doce indicadores con fórmula; doce pruebas con criterio de aceptación. Nueve de las quince características de la norma se miden aquí y las seis restantes se remiten, declaradas, al apartado donde ya están resueltas. Tres umbrales son metas propias de Terabyte y quedan marcados como tales; ninguno se presenta como cifra del caso.
