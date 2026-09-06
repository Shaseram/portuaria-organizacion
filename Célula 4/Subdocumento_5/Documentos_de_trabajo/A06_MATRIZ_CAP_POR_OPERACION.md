# A-06 — Transaccionalidad, consistencia y disponibilidad: matriz CAP por operación

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Destino en el documento:** § 5.5, con la matriz completa en el Anexo D
**Versión:** 1.0 · 6 de septiembre de 2026
**Modelo de origen:** diagramas v2.1, diccionario A-02 y familias de persistencia A-05

---

## 0. Alcance

`BTT, Cap. 5, RT-05.02` exige justificar las garantías transaccionales y **la posición escogida entre consistencia y disponibilidad conforme al teorema CAP, para cada dominio de datos**. A-05 resolvió la primera mitad de esa obligación —el paradigma y el motor por familia—; este documento resuelve la segunda.

Entrega cuatro cosas:

1. las **seis particiones reales** de este caso, que son las que hacen aplicable el teorema;
2. las **unidades transaccionales** del modelo: qué entidades se confirman juntas y qué invariantes lo exigen;
3. la **matriz CAP por operación**: veinticinco operaciones con su invariante, su posición y su comportamiento bajo partición;
4. la **declaración de funciones no disponibles en modo desconectado** con su procedimiento manual de reemplazo, cuya ausencia el documento transversal evalúa como observación grave.

---

## 1. Cómo se usa CAP en este documento, y cómo no

El teorema no dice que haya que escoger dos propiedades de tres. Dice algo más acotado y más útil: **cuando ocurre una partición de red, un sistema distribuido debe elegir entre mantener la consistencia y mantener la disponibilidad**. Sin partición, la elección no se plantea.

De ahí se siguen tres reglas de método que este documento respeta:

- **La posición se declara por operación, no por solución.** El propio caso lo pide en su lista de decisiones que no deben tomarse silenciosamente: no convertir CAP en una elección global y analizar cada operación y cada partición real. Una propuesta que declare «la solución es CP» no ha dicho nada verificable.
- **La partición tiene que ser real y nombrada.** Sin identificar dónde se corta la red, la clasificación es decorativa. La sección 2 nombra las seis particiones que este caso documenta.
- **Una operación puede tener posiciones distintas frente a particiones distintas.** Registrar un movimiento prioriza consistencia frente a la partición interna del terminal y disponibilidad frente a la partición con el exterior. Es la respuesta correcta, y colapsarla en una sola etiqueta la haría falsa.

> **Nota de cita.** Este apartado cruza dos códigos homónimos que significan cosas distintas, y conviene tenerlo presente al leerlo: `RT-03.13` designa en las Bases Técnicas Transversales la **declaración de funciones no disponibles en modo desconectado**, y en las Bases Técnicas del Caso designa el **plazo de sincronización de 90 minutos**. Ambos se invocan aquí y ambos se citan con su documento, conforme a `DEC-C4-14`.

---

## 2. Las seis particiones reales del caso

| ID | Partición | Origen documental | Duración exigible | Qué queda de cada lado |
|---|---|---|---|---|
| `PAR-1` | **Terminal ↔ exterior.** Se pierde el enlace de datos hacia fuera del recinto | Restricción no negociable N.º 4; `CP, Cap. 15, RT-03.10` | **72 horas continuas** de operación completa | Dentro: núcleo local, borde, patio, gate, muelle, reefer. Fuera: nube, navieras, autoridades, sistema de gestión empresarial, concedente, portal |
| `PAR-2` | **Solución ↔ sistema de operación de 2012**, durante la coexistencia | `RF-CON-13`, `RF-CON-14`; Decisión N.º 1 § 5.2 | mientras dure la convivencia por zona | Dos registros del mismo hecho, con autoridad distinta según dominio, zona y fase |
| `PAR-3` | **Equipo de patio ↔ red inalámbrica.** El equipo sale de cobertura | `CP, Cap. 15, RT-03.10` | **8 horas continuas** sin pérdida de registro | El equipo mantiene su cola local; el núcleo no ve sus movimientos |
| `PAR-4` | **Concentrador de patio refrigerado ↔ núcleo** | Decisión N.º 8; `RF-REF-07` | no acotada; se detecta por ausencia de dato | El concentrador sigue muestreando y evaluando desviación; el núcleo deja de recibir la serie |
| `PAR-5` | **Terminal ↔ una contraparte externa concreta** que no responde o responde con error | `BTT, Cap. 5, RT-05.21`; `BTT, Cap. 10, RT-10.08` | por contraparte | La operación interna continúa; el intercambio con esa contraparte se encola |
| `PAR-6` | **Primario operacional ↔ réplica analítica** | Familia 4 de A-05 | transitoria | La operación continúa; la explotación se atrasa |

Las seis son **verificables**: cinco están declaradas en las Bases o en el cierre de Célula 2, y la sexta se deriva de la arquitectura de datos propuesta. Ninguna es hipotética.

---

## 3. Unidades transaccionales

La unidad transaccional es el conjunto de entidades que se confirman o se descartan juntas. Declararla es lo que `RT-05.02` llama garantías transaccionales, y no es una decisión de implementación: se deriva de las invariantes del modelo conceptual.

| ID | Unidad transaccional | Entidades que se confirman juntas | Invariante que lo exige |
|---|---|---|---|
| `UT-01` | **Movimiento y posición** | `MOVIMIENTO` + `POSICION_VIGENTE` + (cuando corresponde) `CUSTODIA` | `INV-02` y `INV-04`: no puede existir un movimiento confirmado sin que la posición quede actualizada, ni una posición sin estado de confianza |
| `UT-02` | **Transferencia de autoridad** | `TRANSFERENCIA_AUTORIDAD` + el cambio de `ASIGNACION_AUTORIDAD` aplicable | `INV-01`: un fallo parcial debe dejar la autoridad en el origen, nunca en ambos ni en ninguno |
| `UT-03` | **Turno de camión** | `EVENTO_GATE` + `TURNO_CAMION` + `MOVIMIENTO_TERRESTRE` + `INSTRUCCION_DESTINO` | La estadía derivada no puede calcularse sobre eventos a medias |
| `UT-04` | **Hecho facturable y su evidencia** | `HECHO_FACTURABLE` + `EVIDENCIA` | `INV-08` e `INV-09`: no existe hecho sin evidencia; la evidencia es inmutable desde su creación |
| `UT-05` | **Alarma y su parametrización** | `ALARMA` + referencia a la versión vigente de `PARAMETRO_DESVIACION` | `INV-11`: la alarma debe poder explicarse contra el parámetro con que se evaluó |
| `UT-06` | **Acta, retención y liberación** | `ACTA_INSPECCION` + `RETENCION` + reevaluación de `CONDICION_LIBERACION` | `INV-07`: una retención vigente impide la liberación en el mismo instante en que se impone |
| `UT-07` | **Credencial y sus zonas** | `CREDENCIAL_TEMPORAL` + `ZONA_HABILITADA` | `INV-13`: no existe credencial sin zonas ni sin expiración |
| `UT-08` | **Muestra de temperatura** | `MUESTRA_TEMPERATURA`, sola | Es anexado puro: no participa de ninguna transacción multi-entidad |

**`DEC-C4-16`.** Ninguna unidad transaccional cruza la frontera entre familias de persistencia. `UT-04` es el caso límite: el metadato y el sello de la evidencia se confirman con el hecho en el motor relacional, y el objeto binario se escribe **antes**, en almacenamiento de objetos, de modo que la transacción confirma un puntero a un objeto ya existente. Si el objeto no se escribió, la transacción no confirma. Es lo que evita una transacción distribuida entre dos motores, que sería la manera más rápida de comprometer los umbrales de un segundo.

---

## 4. Matriz CAP por operación

**Cómo leer la columna de posición.** `C` significa que ante la partición la operación **se detiene o se degrada antes que aceptar un dato inconsistente**. `A` significa que la operación **continúa y la consistencia se restablece después**, con su mecanismo de reconciliación declarado.

### 4.1 Núcleo de registro

| ID | Operación | Invariante en juego | Posición | Comportamiento bajo partición |
|---|---|---|---|---|
| `OP-01` | Registrar movimiento desde equipo de patio | `INV-04` | **C** ante `PAR-2`, **A** ante `PAR-1` y `PAR-3` | Ante `PAR-1` y `PAR-3` se registra local y se encola: la restricción N.º 4 lo exige. Ante `PAR-2`, si la zona no tiene autoridad confirmada, el movimiento **no se acepta**: aceptarlo crearía dos escritores |
| `OP-02` | Consultar posición de un contenedor | `INV-02`, `INV-03` | **A** | La consulta se responde siempre con el estado local y **con su estado de confianza visible**. Devolver «por verificar» es una respuesta correcta; devolver una posición dudosa como cierta no lo es |
| `OP-03` | Transferir autoridad al cruzar zona | `INV-01` | **C**, sin excepción | Es la única operación del modelo que se detiene ante cualquier partición. Sin confirmación de persistencia del receptor, la autoridad permanece en el origen y se bloquea una segunda transferencia de la misma visita |
| `OP-04` | Asignar posición en patio | `INV-05`, `INV-06` | **A** | El algoritmo opera con las condiciones dinámicas locales vigentes. La segregación de mercancías peligrosas se evalúa siempre con datos locales: nunca depende del exterior |
| `OP-05` | Abrir y cerrar tarea de verificación de posición | `INV-02` | **A** | Opera íntegramente en el borde |

### 4.2 Gate y transporte

| ID | Operación | Invariante en juego | Posición | Comportamiento bajo partición |
|---|---|---|---|---|
| `OP-06` | Registrar entrada de camión en barrera | `INV-04` | **A** | Restricción N.º 4: el gate no se detiene. Se registra local con instante de barrera |
| `OP-07` | Emitir instrucción de destino | `INV-05` | **A** | El algoritmo de patio es local; no requiere el exterior |
| `OP-08` | Validar documentación anticipada | — | **C** ante `PAR-5` | Si la contraparte que debe validar no responde, **no se declara validado**: se deriva a carril de excepción con motivo. Marcar como válido lo no verificado contaminaría la condición de liberación |
| `OP-09` | Registrar pesaje de masa bruta | `INV-07` | **A** | La báscula es local. El repesaje conserva la secuencia |
| `OP-10` | Evaluar condición de liberación | `INV-07` | **C** | Es una conjunción de cinco condiciones, tres de ellas con origen externo. Si alguna no puede evaluarse, el resultado es **no liberable**, no «liberable provisional» |

### 4.3 Reefer y cadena de frío

| ID | Operación | Invariante en juego | Posición | Comportamiento bajo partición |
|---|---|---|---|---|
| `OP-11` | Ingerir muestra de temperatura | `INV-10` | **A** | El concentrador sigue muestreando ante `PAR-1` y `PAR-4`; la serie se reporta al reconectar, con su marca de origen |
| `OP-12` | Evaluar desviación y generar alarma | `INV-11` | **A**, con evaluación en el borde | La evaluación ocurre donde está el dato. Es lo que permite cumplir los cinco minutos incluso con el núcleo inalcanzable |
| `OP-13` | Alarmar por ausencia de dato | `INV-11` | **A** | `PAR-4` es indistinguible de un sensor caído, y por eso mismo dispara alarma: es el modo de falla que el caso documenta |
| `OP-14` | Confirmar y escalar alarma | `INV-12` | **A** | El escalamiento opera con la cadena de destinatarios local; la notificación externa se encola |

### 4.4 Evidencia, facturación e inspecciones

| ID | Operación | Invariante en juego | Posición | Comportamiento bajo partición |
|---|---|---|---|---|
| `OP-15` | Registrar hecho facturable | `INV-08`, `INV-16` | **A** | Restricción N.º 4: el registro de hechos facturables es una de las cinco funciones críticas. Se genera local, con la versión de regla tarifaria vigente en el borde |
| `OP-16` | Entregar hecho al sistema de gestión empresarial | — | **C** ante `PAR-1` y `PAR-5` | La entrega se encola. **No se emite documento tributario**: el sistema de gestión es su único emisor, por restricción N.º 5 |
| `OP-17` | Presentar y resolver objeción | — | **C** ante `PAR-1` | Requiere al cliente y la evidencia; ambos pueden estar del otro lado. No es función crítica |
| `OP-18` | Registrar acta de inspección con firma | `INV-09` | **C** ante `PAR-1` si la firma requiere validación externa | Procedimiento manual declarado: acta en papel firmada, digitalizada y cargada al reconectar, con su marca de origen |
| `OP-19` | Imponer o levantar retención | `INV-07` | **A** | La autoridad está físicamente en el recinto; el registro es local |

### 4.5 Nave, integración y explotación

| ID | Operación | Invariante en juego | Posición | Comportamiento bajo partición |
|---|---|---|---|---|
| `OP-20` | Recibir mensaje de naviera o autoridad | — | **C** ante `PAR-1` y `PAR-5` | No hay recepción sin enlace. Al reconectar se procesa la cola en orden, con deduplicación por clave de idempotencia |
| `OP-21` | Emitir confirmación de carga y descarga | `INV-16` | **A** con entrega diferida | El evento se produce local y se emite al reconectar. Lo que no se admite es reconstruirlo después |
| `OP-22` | Confirmar ventana de atraque | — | **C** ante `PAR-1` | Es un acuerdo con la naviera; no puede confirmarse unilateralmente |
| `OP-23` | Publicar estado en el portal de clientes | — | **C** ante `PAR-1` | El portal vive fuera. Se declara no disponible; no se sirve una copia desactualizada sin marca |
| `OP-24` | Consolidar indicadores del concedente | `INV-16` | **A** con entrega diferida | Se consolidan localmente al cierre de cada turno y se acumulan. El plazo de una hora se mide contra el cierre de turno, no contra la reconexión |
| `OP-25` | Registrar acceso de persona al recinto | `INV-13`, `INV-14` | **A** | `RF-ACC-08`: se registra sin conectividad, con instante de borde e instante de sincronización distintos |

### 4.6 Lectura de la matriz

De veinticinco operaciones, **dieciséis priorizan disponibilidad y nueve priorizan consistencia**. La distribución no es casual y es el argumento que hay que sostener en la presentación:

- **Las cinco funciones críticas de las 72 horas son todas `A`**: atención de nave, registro de movimientos, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables. Es la traducción literal de la restricción no negociable N.º 4 a decisiones de datos.
- **Las nueve operaciones `C` son de dos tipos, y ninguna es de registro.** O bien requieren a un tercero para existir —recibir un mensaje, confirmar una ventana, emitir un documento tributario, publicar en el portal—, o bien producirían un dato falso si continuaran: declarar validada una documentación que nadie validó, liberar un contenedor sin poder evaluar sus cinco condiciones, o crear un segundo escritor autoritativo.
- **`OP-03` es la única que se detiene ante cualquier partición.** Es deliberado: la transferencia de autoridad es el punto donde el modelo puede romper su invariante más cara.

---

## 5. Reglas transversales de concurrencia

`RT-05.02` exige garantías transaccionales, y la guía de trabajo pide declarar idempotencia, control de concurrencia, versionado y resolución de conflictos. Estas cuatro reglas aplican a todas las operaciones de la matriz.

| Regla | Contenido | Dónde se apoya |
|---|---|---|
| **Idempotencia** | Toda escritura reintentable lleva clave de idempotencia única y ventana de deduplicación. Un reintento aplica el efecto una sola vez | `MENSAJE.clave_idempotencia` y `TRANSFERENCIA_AUTORIDAD.clave_idempotencia`, ambas declaradas únicas en el modelo |
| **Control de concurrencia** | Optimista sobre el estado operacional: la escritura declara la versión que leyó y se rechaza si cambió. Pesimista solo en la transferencia de autoridad, donde el bloqueo es correcto porque el conflicto es inaceptable | `UT-01` y `UT-02` |
| **Versionado** | Cinco entidades se versionan y nunca se sobrescriben: regla tarifaria, plan de estiba, parámetro de desviación, factor de emisión y contrato de interfaz | Claves compuestas del modelo v2.1 |
| **Orden** | Las transferencias de una misma visita se ordenan por número de secuencia, no por instante de llegada. Dos relojes distintos no ordenan de forma fiable | `TRANSFERENCIA_AUTORIDAD.numero_secuencia` |

---

## 6. `DEC-C4-15` — Resolución determinista de conflictos de posición

**El caso lo exige de forma expresa.** `CP, Cap. 15, RT-03.13` obliga a que la sincronización tras 72 horas resuelva de manera determinista **los conflictos de posición de contenedor producidos durante la desconexión**, y `BTT, Cap. 3, RT-03.12` exige regla de resolución documentada y bitácora auditable de las decisiones aplicadas. La lista de decisiones que no deben tomarse silenciosamente lo dice desde el otro lado: no usar «la última escritura gana» sin justificar el conflicto de posición y autoridad.

**Decisión: la regla es una cascada de cuatro niveles, y se aplica en orden.**

| Nivel | Criterio | Fundamento |
|---:|---|---|
| **1** | **Autoridad.** Prevalece el registro emitido por el sistema que tenía autoridad sobre ese dominio, zona y fase en el instante del hecho | `INV-01`. Una escritura posterior emitida por un sistema sin autoridad territorial **no** prevalece sobre una anterior emitida por quien sí la tenía. Es lo que descarta «la última escritura gana» |
| **2** | **Credibilidad de la fuente.** A igual autoridad, prevalece el registro de mayor credibilidad: telemetría del equipo sobre lectura óptica, y ambas sobre la vía manual de excepción | `MOVIMIENTO.fuente_registro` existe precisamente para esto. `RF-PAT-05` y `RF-PAT-12` exigen registrar el movimiento desde la telemetría del equipo sin acción del operador |
| **3** | **Orden secuencial.** A igual autoridad y credibilidad, prevalece el mayor número de secuencia de la misma visita | Dos relojes en partición no ordenan de forma fiable |
| **4** | **Verificación física.** Si los tres niveles anteriores no resuelven, la posición **no se resuelve automáticamente**: pasa a estado *por verificar* y abre tarea dirigida | `RF-PAT-03` y `RF-PAT-04`. Es preferible una posición declarada dudosa a una posición falsa declarada cierta |

**Consecuencia que se asume.** El nivel 4 significa que la sincronización puede terminar con posiciones sin resolver. Es correcto y es coherente con el indicador comprometido: la meta no es cero posiciones dudosas, sino que **toda posición declarada conocida sea correcta**, con el residual acotado a las marcadas *por verificar* no resueltas al cierre de turno. Resolver automáticamente el nivel 4 subiría el indicador y bajaría la verdad.

**Bitácora.** Cada conflicto resuelto registra el nivel de la cascada que lo resolvió, los dos valores en conflicto y el instante. Es el registro auditable que `RT-03.12` exige y el insumo de `PRU-08`.

---

## 7. Funciones no disponibles en modo desconectado

`BTT, Cap. 3, RT-03.13` obliga a declarar **qué funciones NO estarán disponibles en modo desconectado y qué procedimiento manual las suple**, y advierte que **la ausencia de esta declaración se evaluará como observación grave**. Esta es esa declaración, referida a `PAR-1`.

### 7.1 Lo que sí funciona: las cinco funciones críticas

Atención de nave, registro de movimientos de contenedor, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables. Las cinco operan completas contra el núcleo local durante las 72 horas, con todas sus validaciones estructurales y de dominio, y con las invariantes evaluadas contra el estado local.

### 7.2 Lo que no funciona, y con qué se suple

| Función no disponible | Por qué | Procedimiento manual que la suple | Al reconectar |
|---|---|---|---|
| Recepción y emisión de mensajería con navieras | La contraparte está fuera | Coordinación por los canales de contingencia acordados con cada naviera, con registro del acuerdo en el sistema local | La cola se procesa en orden, con deduplicación por clave de idempotencia |
| Portal de clientes, público y autenticado | El portal vive fuera del recinto | Atención por la mesa de ayuda, que registra la consulta como evento local | El portal recupera el estado desde el núcleo; no se sirve copia desactualizada sin marca |
| Emisión de documento tributario | El sistema de gestión empresarial es su único emisor, por restricción N.º 5 | Ninguno: **el hecho facturable sí se registra**, con su evidencia. Solo se difiere la emisión del documento | La cola de hechos se entrega y se concilia 1:1 |
| Interfaz con autoridades aduanera, fitosanitaria y sanitaria | La contraparte está fuera | Canal asistido trazable: acta en papel firmada por el inspector presente, digitalizada y cargada con marca de origen manual | Se transmite el acta y su evidencia; el resultado ya rige localmente desde su firma |
| Notificación externa a transportistas y agencias | Requiere salida a Internet | Aviso por radio y por megafonía en el recinto; el conductor recibe la instrucción en el puesto de gate | Se envían las notificaciones pendientes con su instante original |
| Reporte de indicadores al concedente | La contraparte está fuera | Ninguno: los indicadores **se consolidan localmente al cierre de cada turno** y se acumulan | Se entregan los paquetes acumulados sin reconstrucción |
| Tableros de gestión y autoservicio del CLIENTE | Dependen de la réplica analítica | Consultas operacionales directas sobre el núcleo local, acotadas para no degradar la operación | La réplica se pone al día; el desfase se declara en el tablero |
| Registro y recuperación de acceso autoservido del portal | Vive fuera | Habilitación manual por la mesa de ayuda, con registro local | Se sincronizan las credenciales creadas |
| Verificación de habilitación contra fuentes externas | Requiere la fuente acreditadora | Se usa la última copia local vigente de la habilitación, **con marca de verificación diferida** | Se revalida contra la fuente; toda discrepancia genera evento |

### 7.3 Regla que gobierna la tabla

Ninguna función crítica de registro aparece en 7.2, y ninguna de las funciones de 7.2 se sustituye por una estimación. Se difieren o se resuelven con un procedimiento humano trazable, pero **no se inventa el dato ausente**. Un evento registrado por vía manual durante la partición conserva esa marca para siempre, y es lo que hace medible el indicador `IND-03` del tablero de calidad.

---

## 8. Sincronización y reconciliación

| Parámetro | Valor | Origen |
|---|---|---|
| Plazo máximo de sincronización tras 72 h | **≤ 90 minutos**, sin intervención manual | `CP, Cap. 15, RT-03.13` |
| Pérdida admisible | **Cero** movimientos y cero hechos facturables | `CP, Cap. 15, RT-03.13` |
| Volumen a transferir | ≈ 13 GB, dominado por las imágenes de gate | volumetría de Célula 2 |
| Transferencia sostenida implicada | ≈ 19,3 Mbps útiles | derivación de la volumetría |
| Resolución de conflictos | cascada de cuatro niveles de `DEC-C4-15`, con bitácora | `BTT, Cap. 3, RT-03.12` |

**Orden de la reconciliación.** No es indiferente y se declara: primero las transferencias de autoridad pendientes, porque determinan qué registros son autoritativos; después los movimientos y las posiciones, que dependen de la autoridad; después los hechos facturables y su evidencia; después las series de telemetría, que son anexado puro y no compiten; y al final las imágenes, que son el 94 % del volumen y **no bloquean ninguna invariante**. Poner las imágenes al final es lo que permite que las invariantes queden resueltas mucho antes de que termine la transferencia.

**Riesgo declarado.** Los 90 minutos y los 19,3 Mbps son una derivación sobre volumen estimado, no capacidad de enlace contratada ni demostración de extremo a extremo. Falta añadir tráfico concurrente, protocolo, cifrado y holgura, y revalidar las 72 horas en temporada de peak estacional. Corresponde al dimensionamiento de Célula 3 (`PEN-08`).

---

## 9. Lo que queda abierto

| ID | Qué falta | Responsable | Qué condiciona |
|---|---|---|---|
| `PEN-01` | Zonas y fases nombradas de la matriz de autoridad | Célula 3 | El nivel 1 de la cascada de `DEC-C4-15` y toda la columna de `PAR-2` |
| `PEN-10` | Frontera del runtime local: qué datos persisten en el borde y con qué tamaño de buffer | Célula 3 | Qué operaciones `A` son realmente sostenibles 72 horas |
| `PEN-06` | Si el flujo hacia la analítica es réplica, captura de cambios o eventos | Célula 3 | El comportamiento de `PAR-6` y el desfase declarado en el tablero |
| `PEN-08` | Revalidación del volumen de 72 horas y del ancho de banda de reposición | Célula 3 | El plazo de 90 minutos de la sección 8 |
| Propio | Los canales de contingencia con cada naviera de la sección 7.2 son **acuerdos por levantar**, no interfaces existentes | Célula 4 y levantamiento | La columna de procedimiento manual |

---

## 10. Trazabilidad

| Exigencia | Fuente | Dónde se cumple |
|---|---|---|
| Posición entre consistencia y disponibilidad conforme a CAP, por dominio de datos | `BTT, Cap. 5, RT-05.02` | secciones 1, 2 y 4 |
| Garantías transaccionales declaradas | `BTT, Cap. 5, RT-05.02` | secciones 3 y 5 |
| Registro local íntegro durante la desconexión | `BTT, Cap. 3, RT-03.11` | operaciones `A` de la sección 4 |
| Reconciliación determinista con regla documentada y bitácora auditable | `BTT, Cap. 3, RT-03.12` | `DEC-C4-15` |
| **Declaración de funciones no disponibles y su procedimiento manual** | `BTT, Cap. 3, RT-03.13` | sección 7 |
| Operación completa 72 h y sincronización ≤ 90 min sin pérdida | `CP, Cap. 15, RT-03.10` y `RT-03.13` | secciones 7 y 8 |
| Comportamiento ante contraparte que no responde | `BTT, Cap. 5, RT-05.21`; `BTT, Cap. 10, RT-10.08` | `PAR-5` y operaciones `OP-16`, `OP-20`, `OP-22` |
| Indicadores producidos y no reconstruidos | `CP, Cap. 10`, restricción N.º 14 | `OP-21` y `OP-24` |
| Cinco funciones críticas operativas sin enlace | `CP, Cap. 10`, restricción N.º 4 | sección 7.1 |

---

**Cierre.** Seis particiones nombradas y documentadas, ocho unidades transaccionales derivadas de las invariantes, veinticinco operaciones con su posición y su comportamiento, una cascada de cuatro niveles para resolver conflictos de posición sin recurrir a «la última escritura gana», y la declaración de funciones no disponibles que el documento transversal evalúa como observación grave si falta. CAP se aplica aquí como lo que es —una elección forzada por una partición concreta— y no como una etiqueta global.
