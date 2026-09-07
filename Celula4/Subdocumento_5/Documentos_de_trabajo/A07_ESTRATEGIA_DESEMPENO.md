# A-07 — Estrategia de desempeño de datos: índices, particiones, caché y consultas

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Destino en el documento:** § 5.10, con la matriz completa en el Anexo E
**Versión:** 1.0 · 6 de septiembre de 2026
**Modelo de origen:** diagramas v2.1, diccionario A-02, familias A-05 y matriz CAP A-06

---

## 0. Alcance y método

La cuarta viñeta del Formulario T-7 exige *«estrategia de desempeño: indexación, particionamiento, caché y optimización de consultas»*, y `BTT, Cap. 9, RT-09.05` obliga además a **identificar el componente que primero se convertirá en cuello de botella al crecer la carga, y explicar cómo se detectará y cómo se resolverá**.

El método es el inverso al habitual: no se parte de un catálogo de técnicas para ver dónde aplicarlas, sino del **catálogo de operaciones críticas y sus claves de acceso**, que ya existe en el diccionario. Cada técnica de este documento aparece porque una operación con umbral comprometido la necesita. Ninguna aparece por completitud.

**Sobre las decisiones.** Este documento cierra **cuatro** decisiones de Célula 4. Cada una se toma porque una obligación concreta no puede satisfacerse sin ella, y así se declara en su encabezado. Todo lo demás queda como pendiente con su célula responsable en la sección 8.

---

## 1. Punto de partida: qué se mide y contra qué

### 1.1 Perfil de carga vigente

| Magnitud | Régimen | Peak de coincidencia | Proyección a 3 años | Fuente |
|---|---:|---:|---:|---|
| Transacciones de negocio | 0,11 TPS | 0,23 TPS | 0,27 TPS | volumetría C2, fila 1 y 2 |
| Movimientos de contenedor | 2.262.000 al año ≈ 0,072 por segundo | — | ≈ 2.620.000 al año | `CP, Cap. 14.1` |
| Series reefer reportadas al núcleo | 7,2 ev/s → **226 M filas al año** | — | 8,7 ev/s | volumetría C2, fila 3 |
| Series reefer en el borde | 35,8 ev/s | — | 43,3 ev/s | volumetría C2, fila 3 |
| Posicionamiento de equipos | 37 ev/s | — | 44 ev/s | volumetría C2, fila 5 |
| Usuarios internos concurrentes | ≈ 160 | — | ≈ 175 | volumetría C2, fila 6 |
| Usuarios externos concurrentes | ≈ 159 | — | ≈ 187 | volumetría C2, fila 7 |

**Factor estacional aplicable** sobre las magnitudes dependientes del volumen operacional: camiones ×1,79 y volumen refrigerado mensual de enero a marzo ×2,48.

### 1.2 La observación que ordena todo el apartado

Las transacciones de negocio son **0,23 por segundo en el peak**. Un motor relacional moderno atiende esa carga sin esfuerzo. **El problema de desempeño de este caso no es el volumen transaccional: es el contraste entre ese volumen y los flujos que lo rodean** —36 eventos por segundo de telemetría y 37 de posicionamiento— y, sobre todo, **la latencia comprometida**: un segundo para confirmar un movimiento desde un equipo de patio, en un terminal de dieciocho hectáreas, con red inalámbrica sobre pilas metálicas de cinco alturas.

La estrategia, por tanto, no persigue capacidad. Persigue **aislamiento y previsibilidad**: que la carga que crece no toque la ruta que tiene el umbral más estrecho.

---

## 2. `DEC-C4-17` — El flujo crudo de posicionamiento no se persiste

> **Por qué esta decisión es necesaria.** Sin declararla, la volumetría no cuadra por un orden de magnitud y el dimensionamiento de almacenamiento sería falso. El modelo conceptual **no tiene ninguna entidad** para la posición cruda de un equipo, y esa ausencia hay que justificarla explícitamente o parece un olvido.

**Decisión.** El flujo de posicionamiento de los equipos móviles —37 eventos por segundo— **se procesa en el borde y no se persiste como dato**. Lo que se persiste es el `MOVIMIENTO` derivado, con su instante real, su equipo, sus celdas de origen y destino y su fuente de registro.

**Fundamento.**

1. **La aritmética.** Persistir el flujo crudo serían **1.167 millones de filas al año**, que a 100 bytes por evento con factor de sobrecarga equivalen a ≈ **350 GB anuales**. El almacenamiento transaccional declarado en la volumetría vigente es de ≈ 20 GB al año. Los dos números solo son compatibles si el flujo crudo no entra en el almacén transaccional — que es, de hecho, el supuesto implícito de la volumetría de Célula 2. Aquí se hace explícito.
2. **El dato de negocio es el movimiento, no la coordenada.** Ningún requerimiento funcional consulta la trayectoria continua de un equipo. `RF-PAT-05` y `RF-PAT-12` piden registrar el **movimiento** desde la telemetría sin acción del operador; la coordenada es el insumo del que se deriva, no el hecho.
3. **Es coherente con el procesamiento en el borde** que el documento transversal valora expresamente: filtrado y agregación previa para reducir el volumen transferido y la dependencia del enlace `(BTT, Cap. 3, RT-03.19)`.

**Consecuencia que se asume.** No se podrá reconstruir a posteriori la trayectoria exacta de un equipo para un análisis que hoy nadie pide. Si el CLIENTE lo pidiera más adelante, es una capacidad nueva con su propio dimensionamiento, no un ajuste de configuración.

**Lo que sí se retiene.** La ventana deslizante en el borde necesaria para detectar el movimiento y para sostener las 8 horas fuera de cobertura que exige `CP, Cap. 15, RT-03.10`, y las métricas agregadas de utilización de equipo que alimentan el consumo energético.

**Vinculación.** `RF-PAT-05`, `RF-PAT-12` · `BTT, Cap. 3, RT-03.19` · volumetría C2 filas 5, 8 y 15 · `D-02.MOVIMIENTO` · A-08.

---

## 3. Estrategia de índices

### 3.1 Regla

Se indexa **una clave de acceso declarada de una operación crítica**, y nada más. Cada índice es un costo de escritura permanente sobre una ruta que tiene un segundo de presupuesto: un índice que no sirve a una operación de la matriz de la sección 5 no se crea.

### 3.2 Índices comprometidos

| # | Entidad | Clave de acceso | Operación que lo exige | Umbral |
|---:|---|---|---|---|
| 1 | `VISITA` | `codigo_iso6346` + estado abierto | consulta de posición y de estado por número de contenedor | ≤ 1 s |
| 2 | `POSICION_VIGENTE` | `id_visita` (clave primaria) | consulta de posición | ≤ 1 s |
| 3 | `POSICION_VIGENTE` | `id_celda` | ocupación de celda, invariante de no colisión | ≤ 1 s |
| 4 | `POSICION_VIGENTE` | `estado_confianza` (parcial, solo *por verificar*) | tablero de calidad e indicador `IND-02` | por turno |
| 5 | `MOVIMIENTO` | `id_visita` + `instante` | historial del contenedor, evidencia y emisiones | ≤ 1 s |
| 6 | `MOVIMIENTO` | `id_equipo` + `instante` | atribución de consumo de `DEC-C4-01` | lote |
| 7 | `MOVIMIENTO` | `id_correlacion` | trazabilidad extremo a extremo | consulta dirigida |
| 8 | `TURNO_CAMION` | `patente` + `instante_arribo_barrera` | identificación del camión en barrera | ≤ 120 s (compuesto) |
| 9 | `CITA` | `franja_desde` + `estado` | disponibilidad de cupo y prioridad de atención | ≤ 120 s (compuesto) |
| 10 | `EVENTO_GATE` | `id_turno_camion` + `tipo` | cálculo derivado de la estadía | ≤ 1 s |
| 11 | `MUESTRA_TEMPERATURA` | `id_conexion` + `instante` (clave primaria, ordenada) | curva de temperatura por contenedor | ≤ 3 s |
| 12 | `CONEXION_REEFER` | `id_toma` + `instante_desconexion` nulo | conexiones vigentes | ≤ 1 s |
| 13 | `ALARMA` | `estado` + `instante_generacion` (parcial, solo abiertas y escaladas) | consola de alarmas y escalamiento | ≤ 5 min |
| 14 | `HECHO_FACTURABLE` | `id_visita` + `tipo` | conciliación diaria y objeciones | diaria |
| 15 | `HECHO_FACTURABLE` | `estado` (parcial, solo objetado y pendiente) | gestión de objeciones | ≤ 30 s |
| 16 | `EVIDENCIA` | `id_hecho` | recuperación dirigida de evidencia | ≤ 30 s |
| 17 | `LECTURA_OPTICA` | `codigo_leido` + `instante` | conciliación de lectura con visita abierta | ≤ 3 s |
| 18 | `EVENTO_ACCESO` | `id_zona` + `instante` | conteo de personas por zona | tiempo real |
| 19 | `MENSAJE` | `clave_idempotencia` (única) | deduplicación en la reconexión | ≤ 90 min |
| 20 | `TRANSFERENCIA_AUTORIDAD` | `id_visita` + `numero_secuencia` | orden de la cascada de `DEC-C4-15` | ≤ 90 min |
| 21 | `REGISTRO_AUDITORIA` | `entidad_afectada` + `id_objeto_afectado` + `instante` | reconstrucción exigida por `RT-05.03` | consulta dirigida |

**Índices parciales, no totales, en cuatro casos.** Los índices 4, 13 y 15 solo cubren la fracción activa del universo: las posiciones dudosas, las alarmas abiertas y los hechos objetados. Es lo que evita pagar el costo de escritura sobre los 226 millones de filas anuales de series y sobre el histórico de hechos, para servir consultas que solo miran lo vigente.

### 3.3 Conflicto declarado entre cifrado e indexación

Ocho de las claves de acceso anteriores son atributos del catálogo de cifrado a nivel de campo de `DEC-C4-12`: `POSICION_VIGENTE.id_celda`, `MOVIMIENTO.celda_origen` y `celda_destino`, `CONTENEDOR.clase_imdg`, `LECTURA_OPTICA.codigo_leido`, `CONDUCTOR.id_persona`, `EVENTO_ACCESO.id_persona` y `HECHO_FACTURABLE.id_regla_aplicada`.

Un cifrado que impida la búsqueda por igualdad sobre ellos hace inalcanzables los umbrales. **Respuesta C3 para I1:** D1 B4.3 propone cifrado aleatorio más token de igualdad protegido o identificador sustituto opaco, siempre dentro del servicio autorizado. Los índices permanecen condicionados a pruebas de fuga, latencia, rotación y continuidad local; no se adopta cifrado determinista directo.

---

## 4. `DEC-C4-18` — Política de particionamiento

> **Por qué esta decisión es necesaria.** El Formulario T-7 exige declarar una estrategia de particionamiento. Sin una regla explícita, particionar o no particionar cada tabla queda al criterio de quien implemente, y el resultado no es defendible ante un evaluador ni reproducible por otro equipo.

**Decisión.** Se particiona **por tiempo** y solo cuando concurren dos condiciones: que la entidad supere el orden de los cien millones de filas en su período de retención, **y** que su política de ciclo de vida exija eliminar o agregar por antigüedad. Las demás entidades no se particionan.

**Entidades que se particionan, y por qué exactamente esas cuatro:**

| Entidad | Filas en su retención | Ciclo de vida que lo exige | Partición |
|---|---:|---|---|
| `MUESTRA_TEMPERATURA` | ≈ **1.130 millones** a 5 años | `DEC-C4-02`: retención de 5 años con agregación de la resolución a los 2 | mensual |
| `MOVIMIENTO` | ≈ 22,6 millones a 10 años | `RT-05.10`: 10 años con eliminación controlada; migración de solo 3 años | anual |
| `EVENTO_ACCESO` | según dotación y turnos, a 5 años | `RT-05.10`: 5 años | anual |
| `REGISTRO_AUDITORIA` | crece con toda operación del sistema | hereda el plazo de la clase auditada | mensual |

**Por qué la eliminación es el argumento y no la consulta.** En una tabla particionada por tiempo, eliminar un período es descartar una partición; sin particionar, es un borrado masivo sobre una tabla viva, en un terminal que **no tiene ventana de detención total** `(restricción no negociable N.º 2)` y que además tiene **prohibido intervenir entre el 15 de diciembre y el 30 de abril** `(restricción N.º 9)`. La política de retención diferenciada de `RNF-CUM-14` no es ejecutable sin particionamiento en esas cuatro entidades.

**Por qué no se particiona el resto.** `VISITA`, `HECHO_FACTURABLE`, `EVIDENCIA` y las 72 entidades restantes se mantienen en el orden de millones de filas o menos en su retención completa. Particionarlas agregaría complejidad de mantenimiento sin beneficio medible, y el caso es explícito en que la solución debe ser operable por **cinco personas** `(restricción N.º 11)`.

**Vinculación.** `RT-05.10` · `RNF-CUM-14` · restricciones N.º 2, 9 y 11 · `DEC-C4-02` · A-05, Familias 1 y 2.

---

## 5. `DEC-C4-19` — Política de caché

> **Por qué esta decisión es necesaria.** El Formulario T-7 exige declarar la estrategia de caché, y en este caso una caché mal ubicada **rompe una invariante comprometida**: si se sirve una posición cacheada como si fuera vigente, el compromiso de que *toda posición declarada conocida es correcta* deja de cumplirse. La regla tiene que ser explícita y restrictiva.

**Decisión.** Se cachea únicamente lectura tolerante a desfase, con desfase máximo declarado, invalidación por evento y fuente de verdad identificada en la respuesta. **Nunca se cachea**: (a) ningún dato con estado de confianza asociado, (b) ningún dato bajo autoridad variable durante la coexistencia, (c) ningún dato que respalde una decisión de liberación, y (d) ninguna evidencia.

| Qué se cachea | Desfase máximo | Invalidación | Fundamento |
|---|---|---|---|
| Catálogos y maestros: tarifario vigente, zonas, bloques y celdas, contrapartes, factores de emisión | hasta el cambio de versión | por evento de versión | Son entidades versionadas: la caché sirve la versión, no el valor |
| Estado de congestión del acceso publicado sin autenticación | 60 s | por temporizador | `RF-GAT-13` publica un estado agregado, no un dato autoritativo |
| Resultado de indicadores ya consolidados del turno cerrado | hasta el cierre siguiente | por cierre de turno | El turno cerrado es inmutable |
| Modelo semántico y definiciones del tablero | hasta el cambio de versión | por despliegue | No es dato operacional |

| Qué **no** se cachea nunca | Por qué |
|---|---|
| `POSICION_VIGENTE` | Rompería `INV-03`: una posición cacheada es una posición dudosa servida como cierta |
| Cualquier entidad bajo `PAR-2` durante la coexistencia | La autoridad puede haber cambiado de zona entre la escritura y la lectura |
| `CONDICION_LIBERACION` y sus cinco insumos | `INV-07` exige evaluación en el instante |
| `EVIDENCIA` y `REGISTRO_AUDITORIA` | Se sirven desde su origen con verificación de sello |
| `MUESTRA_TEMPERATURA` reciente | La curva vigente es la evidencia de cadena de frío |

**Consecuencia que se asume.** La consulta de posición —la operación más frecuente del portal y del terminal— **no se resuelve con caché**, sino con índice sobre una tabla de tamaño acotado. Es la razón por la que el índice 2 y el 3 de la sección 3.2 son irrenunciables.

**Vinculación.** `RF-GAT-13` · `INV-03`, `INV-07` · `PAR-2` de A-06 · § 5.10.

---

## 6. Matriz operación → volumen → latencia → técnica → evidencia

Es la tabla que la cuarta viñeta del T-7 pide y el núcleo de este documento. La columna de evidencia indica la prueba de A-03 o la medición que acredita el cumplimiento.

| ID | Operación | Volumen | Latencia comprometida | Técnica | Evidencia |
|---|---|---|---|---|---|
| `DES-01` | Confirmar movimiento desde equipo de patio | 2.262.000 al año; ≈ 0,07 por segundo | ≤ 1 s p95 · `RNF-DES-03` | Escritura en `UT-01`; índices 2, 3 y 5; sin caché; ruta aislada de la analítica | Instrumentación de la transacción en la terminal del equipo |
| `DES-02` | Consultar posición de un contenedor | consulta más frecuente del sistema | ≤ 1 s · `RNF-DES-03` | Índices 1 y 2 sobre tabla acotada; **sin caché** por `DEC-C4-19` | Prueba de carga a 1,5× el peak |
| `DES-03` | Procesar camión completo en el puesto de gate | 1.450 al día, hasta 2.600 en peak estacional | ≤ 120 s · `RNF-DES-01` | Composición de `DES-04`, `DES-02` y `UT-03`; índices 8, 9 y 10; validación documental anticipada fuera de la ruta | Marcas de tiempo entre arribo e instrucción |
| `DES-04` | Reconocer código de contenedor y conciliar lectura | 2 imágenes por evento de gate | ≤ 3 s · `RNF-DES-02` | Proceso en el borde; índice 17; el binario va a almacenamiento de objetos, no a la base | Prueba cronometrada con muestra en condiciones reales |
| `DES-05` | Ingerir muestra de temperatura | 7,2 ev/s al núcleo; 226 M filas al año | asíncrona | Anexado a tabla particionada mensual; compresión; **agregación previa en el concentrador** | Prueba de ingesta sostenida a 1,5× |
| `DES-06` | Evaluar desviación y generar alarma | 2.150 conexiones en peak | ≤ 5 min desde el evento físico · `RNF-DES-04` | **Evaluación en el borde**, no en el núcleo; índice 13 parcial | Inyección de falla controlada sobre muestra de tomas |
| `DES-07` | Consultar curva de temperatura de un contenedor | por contenedor refrigerado, retención 5 años | ≤ 3 s · `RNF-DES-09` | Índice 11 sobre partición mensual; poda por rango de fecha | Recuperación de evidencia de cadena de frío |
| `DES-08` | Derivar posición del flujo de equipos | 37 ev/s | ≤ 30 s hasta ser visible · `RNF-DES-05` | **Procesamiento en el borde sin persistir el crudo** (`DEC-C4-17`); solo el movimiento se escribe | Prueba de extremo a extremo movimiento → posición visible |
| `DES-09` | Registrar hecho facturable con su evidencia | ≈ 115.200 documentos al año en el sistema de gestión | asíncrona respecto del gate | `UT-04`; objeto escrito antes del puntero (`DEC-C4-16`); índices 14 y 16 | Conciliación diaria 1:1 |
| `DES-10` | Recuperar evidencia dirigida | consulta esporádica, retención 6 años | ≤ 30 s · umbral propio `CAL-38` | Índice 16; objeto en almacenamiento de objetos con verificación de sello | Prueba de recuperación en el límite de retención |
| `DES-11` | Publicar estado del contenedor en el portal | 159 usuarios externos concurrentes, 187 proyectados | ≤ 60 s de propagación · `RNF-DES-06` | Propagación por evento a la réplica de lectura; **el portal nunca consulta el primario** | Prueba de extremo a extremo evento → portal |
| `DES-12` | Responder interfaz de consulta simple y de escritura | según integración | ≤ 500 ms y ≤ 800 ms p95 · `RNF-DES-10` | Índices declarados; sin unión con la analítica | Prueba de carga a 1,5× el peak |
| `DES-13` | Búsqueda con criterios compuestos | usuarios internos | ≤ 3 s · `RNF-DES-09` | Índices compuestos 5, 8 y 14; sin exploración completa de tabla | Prueba de carga |
| `DES-14` | Consolidar indicadores del concedente | 1.095 paquetes al año, uno por turno como mínimo | ≤ 1 h tras el cierre de turno · `RNF-DES-07` | Agregación incremental sobre la réplica; nunca sobre el primario `(RT-05.05)` | Marca de cierre de turno contra disponibilidad del indicador |
| `DES-15` | Generar informe estándar en línea | usuarios internos y CLIENTE | ≤ 30 s · `RNF-DES-09` | Réplica analítica con modelo semántico; agregados materializados por turno | Prueba de carga |
| `DES-16` | Conciliar coexistencia por turno | 3 turnos al día | dentro de la ventana de 24 h o 48 h | Índice 20; comparación por lote sobre la réplica | Acta de conciliación por turno |
| `DES-17` | Procesar carga y descarga masiva | archivos de hasta 100 MB | ≥ 10.000 registros por minuto; archivo ≤ 60 s · `RNF-DES-11` | Proceso por lote fuera de la ruta transaccional; validación por registro con informe de errores | Prueba con archivo mixto válido e inválido |
| `DES-18` | Calcular emisiones por contenedor | 486.000 contenedores al año | lote mensual | Índice 6; cálculo sobre la réplica; no toca el primario | Recálculo de un período cerrado |
| `DES-19` | Consultar el repositorio histórico retenido | baja frecuencia, ≈ 480 GB | sin umbral comprometido | Formato columnar abierto con poda por partición; fuera del motor operacional | Prueba de recuperación dirigida |
| `DES-20` | Escribir registro de auditoría | una por operación del sistema | no puede degradar la operación | Anexado a tabla particionada mensual; escritura en la misma transacción, sin índices adicionales | Verificación de la cadena de sellos |
| `DES-21` | Sincronizar tras 72 horas desconectado | ≈ 13 GB | ≤ 90 min · `CP, Cap. 15, RT-03.13` | Orden de reconciliación de A-06 §8; índices 19 y 20; imágenes al final | Prueba de 72 h y reconexión |

---

## 7. `DEC-C4-20` — Primer cuello de botella y mecanismo de crecimiento

> **Por qué esta decisión es necesaria.** `BTT, Cap. 9, RT-09.05` obliga a identificar el componente que primero se convertirá en cuello de botella, y a explicar cómo se detectará y cómo se resolverá. Es una declaración obligatoria: hay que escoger uno y sostenerlo.

### 7.1 Corrección respecto del esqueleto

El § 5.10 del esqueleto declaraba que el primer cuello de botella sería **la ingesta de series temporales**, por comparación entre 0,23 transacciones por segundo y ≈36 eventos por segundo. Al rehacer el cálculo contra el crecimiento exigible, **esa conclusión no se sostiene** y se corrige aquí.

`BTT, Cap. 9, RT-09.03` exige soportar sin rediseño **tres veces la volumetría inicial** en tres años. Aplicado a cada candidato:

| Candidato | Hoy | A 3× | ¿Satura? |
|---|---|---|---|
| Núcleo transaccional | 0,23 TPS | 0,7 TPS | No. Sigue siendo carga trivial para un relacional |
| Ingesta de series al núcleo | 7,2 ev/s | 21,6 ev/s | No. Una extensión temporal con anexado y compresión absorbe ese orden |
| Ingesta de series en el borde | 35,8 ev/s | 107 ev/s | No con agregación previa en el concentrador, que ya es parte del diseño |
| Almacenamiento de imágenes | 1,4 TB al año | 4,2 TB al año | No es un cuello de botella de desempeño: es un costo de capacidad, y el almacenamiento de objetos escala horizontalmente |
| **Ventana de sincronización tras 72 h** | 13 GB en 90 min ⇒ **19,3 Mbps** sostenidos | **39 GB en 90 min ⇒ ≈ 58 Mbps** sostenidos | **Sí.** El plazo de 90 minutos es fijo por contrato y el volumen crece con la operación: es el único margen que se estrecha con el crecimiento |

### 7.2 Decisión

**El primer cuello de botella es la ventana de sincronización posterior a la operación desconectada, y su componente dominante son las imágenes de reconocimiento**, que aportan ≈ 11,2 de los 13 GB actuales.

Es el único punto donde el crecimiento no encuentra holgura: los demás candidatos crecen contra un techo que también crece —capacidad de cómputo, de disco, de red interna—, mientras que aquí el techo es **un plazo fijado por el caso** que no se mueve, y por debajo hay un enlace cuyo ancho de banda tampoco crece solo.

### 7.3 Cómo se detecta

| Señal | Umbral de alerta | Origen |
|---|---|---|
| Volumen acumulado en 72 h simuladas, medido mensualmente | > 70 % del que el enlace transfiere en 90 minutos | `RT-09.09`: gestión de capacidad con proyección trimestral y alerta anticipada de agotamiento |
| Duración real de la última sincronización tras una desconexión | > 60 minutos | `PRU-08` |
| Tasa de crecimiento de imágenes por evento de gate | desviación sostenida sobre la proyección | tablero de calidad |

**La detección debe ser anticipada por una razón de calendario, no de ingeniería:** la restricción no negociable N.º 9 prohíbe intervenir entre el 15 de diciembre y el 30 de abril, y el peak estacional cae precisamente ahí. Toda holgura debe estar instalada y verificada **antes del 15 de diciembre**. Una alerta que se dispara en enero no se puede atender hasta mayo.

### 7.4 Cómo se resuelve, en orden de aplicación

1. **Reducir lo que cruza el enlace, no ampliar el enlace.** Las imágenes son el 86 % del volumen de la ventana. La primera palanca es la política de captura: resolución, compresión y **si se transfiere la imagen o solo su sello y sus metadatos**, dejando el binario replicándose después.
2. **Separar la sincronización que restablece invariantes de la que restablece evidencia.** El orden de reconciliación de A-06 ya pone las imágenes al final porque no bloquean ninguna invariante. La consecuencia natural es medir el plazo de 90 minutos contra la reconciliación que restablece autoridad, movimientos y hechos facturables — **que es lo que la obligación protege**: `CP, Cap. 15, RT-03.13` exige que la sincronización no supere 90 minutos **sin pérdida de ningún movimiento ni de ningún hecho facturable**, y no que todo byte generado en 72 horas haya cruzado el enlace.
3. **Agregación previa en el borde para las series**, que es la palanca del segundo candidato y ya está en el diseño.
4. **Ampliar el enlace de reposición**, que es la última opción porque es la única con costo recurrente y depende de terceros.

> **Interpretación declarada, sujeta a confirmación.** El punto 2 se apoya en una lectura del alcance de `RT-03.13`: que el plazo de 90 minutos protege la integridad de los movimientos y los hechos facturables, no la transferencia completa del volumen. **Es una interpretación de Terabyte, no un hecho del caso**, y se registra como consulta formal en `PEN-16`. Si el CLIENTE la rechaza, la alternativa conservadora es dimensionar el enlace de reposición para los 58 Mbps sostenidos proyectados, con su costo declarado. La estrategia no depende de que la interpretación se acepte: cambia el costo, no el diseño.

**Vinculación.** `BTT, Cap. 9, RT-09.03`, `RT-09.05`, `RT-09.09` · `CP, Cap. 15, RT-03.13` · restricción N.º 9 · volumetría C2 filas 10, 15 y 16 · A-06 § 8.

---

## 8. Degradación controlada y pruebas

### 8.1 Degradación

`BTT, Cap. 9, RT-09.08` exige que al superarse la capacidad la solución degrade de forma controlada —encolamiento, limitación de tasa y mensaje explícito— y **nunca con error genérico ni pérdida silenciosa de transacciones**. Aplicado a esta capa de datos:

| Recurso saturado | Comportamiento | Qué nunca ocurre |
|---|---|---|
| Ingesta de series | El concentrador reduce la resolución reportada dentro del rango de la Decisión N.º 8 y conserva la resolución local | No se descarta ninguna muestra sin marcarla como *ausente* |
| Escritura transaccional | Encolamiento con acuse al equipo de patio y reintento idempotente | No se pierde un movimiento ni se confirma sin persistir |
| Consulta analítica | Limitación de tasa sobre la réplica, con mensaje explícito al usuario | La analítica **nunca** se desvía al primario `(RT-05.05)` |
| Almacenamiento de objetos | Buffer local en el borde con alerta de ocupación | No se descarta una imagen que respalda un hecho facturable |
| Enlace de reposición | La reconciliación sigue el orden de A-06 §8 | Las invariantes no esperan a las imágenes |

### 8.2 Pruebas comprometidas

`BTT, Cap. 9, RT-09.06` exige carga a **1,5 veces el peak declarado** y estrés hasta el punto de quiebre; `RT-09.07` exige informe con curva de respuesta, punto de saturación, consumo de recursos y comportamiento durante y después del peak.

| ID | Prueba | Criterio |
|---|---|---|
| `PRU-13` | Carga a 1,5× el peak de coincidencia, con el factor estacional aplicado a gate y reefer | Todos los umbrales del § 5.10 se mantienen en p95 |
| `PRU-14` | Estrés hasta el punto de quiebre | El punto de saturación queda identificado y la degradación es la de 8.1 |
| `PRU-15` | Ingesta sostenida de series a 3× durante 24 h | Sin pérdida de muestras ni retraso acumulado en la alarma |
| `PRU-16` | Consulta de posición bajo carga de peak con la analítica activa | El primario no se degrada; se verifica el aislamiento de `RT-05.05` |
| `PRU-17` | Simulación mensual del volumen de 72 h | El volumen no supera el 70 % de la capacidad de la ventana de 90 min |

---

## 9. Lo que queda pendiente, y a quién le corresponde

| ID | Qué falta | Responsable | Qué condiciona |
|---|---|---|---|
| `PEN-02` — respondido para I1 | Los ocho atributos de §3.3 tienen patrón propuesto en D1 B4.3 | **Célula 3 + Seguridad/CLIENTE** (`ADR-009`) | falta validar fuga, latencia, rotación y corte 72 h antes de comprometer los umbrales |
| `PEN-07` — recibido I1 | PostgreSQL/RDS con capacidad temporal propuesto; versión final por soporte | **Célula 3** (`ADR-007`) | pruebas de índices/compresión/agregación pendientes |
| `PEN-08` — cerrado I1 | promedio, peak, 3× e imagen 1 MB separados | **Célula 3** (`C4`) | se reabre solo si cambia un supuesto fuente |
| `PEN-10` | Frontera del runtime local y tamaño de buffer del borde | **Célula 3** (`A3`/`C3`) | La agregación previa de `DES-05` y el buffer de imágenes de 8.1 |
| `PEN-17` | Latencia real de la red de patio con pilas cargadas y ancho de banda del enlace de reposición | **Célula 3** (`C3`), con site survey | El umbral de 1 s de `DES-01` y los 58 Mbps de 7.1 |
| `PEN-16` | **Nuevo.** Confirmar el alcance del plazo de 90 minutos: ¿protege la integridad de movimientos y hechos facturables, o la transferencia completa del volumen de 72 h? | **CLIENTE**, vía consulta formal | El punto 2 de 7.4 y el costo del enlace de reposición |
| `PEN-18` | **Nuevo.** Política de captura de imágenes: resolución, compresión y si el binario cruza el enlace en la ventana de sincronización | **Célula 4 y Célula 3**, conjunta | La primera palanca de 7.4 |

**`PEN-18` merece una nota.** Podría parecer nuestra y cerrable hoy, pero no lo es: la resolución de captura la condiciona el equipo de reconocimiento óptico que especifica Célula 3, y el umbral de 3 segundos de `RNF-DES-02` depende de esa misma resolución. Decidirla por nuestra cuenta sería fijar un parámetro de un componente que no especificamos.

---

## 10. Trazabilidad

| Exigencia | Fuente | Dónde se cumple |
|---|---|---|
| Estrategia de indexación, particionamiento, caché y optimización de consultas | `BA, Form. T-7`, Subdoc. 5, cuarta viñeta | secciones 3, 4, 5 y 6 |
| Identificar el primer cuello de botella, cómo se detecta y cómo se resuelve | `BTT, Cap. 9, RT-09.05` | `DEC-C4-20` |
| Soportar 3× la volumetría inicial sin rediseño | `BTT, Cap. 9, RT-09.03` | sección 7.1 |
| Prueba de carga a 1,5× el peak y estrés hasta el quiebre | `BTT, Cap. 9, RT-09.06` y `RT-09.07` | sección 8.2 |
| Degradación controlada sin pérdida silenciosa | `BTT, Cap. 9, RT-09.08` | sección 8.1 |
| Gestión de capacidad con alerta anticipada de agotamiento | `BTT, Cap. 9, RT-09.09` | sección 7.3 |
| La analítica no degrada la operación | `BTT, Cap. 5, RT-05.05` | `DES-11`, `DES-14`, `DES-15`, `DES-18` y sección 8.1 |
| Umbrales de transacción operacional crítica | `CP, Cap. 15, RT-09.01`; `RNF-DES-01` a `03` y `06` | sección 6 |
| Umbrales de la capa analítica | `CP, Cap. 15, RT-05.29`; `RNF-DES-04`, `05` y `07` | sección 6 |
| Umbrales del documento transversal | `BTT, Cap. 9, num. 9.1`; `RNF-DES-09` a `11` | `DES-12`, `DES-13`, `DES-15`, `DES-17` |
| Procesamiento en el borde para reducir volumen transferido | `BTT, Cap. 3, RT-03.19` | `DEC-C4-17` y `DES-05` |

---

**Cierre.** Veintiún índices, cada uno atado a una operación con umbral; cuatro entidades particionadas y setenta y seis que no; una política de caché que explicita qué no se cachea; veintiuna operaciones con volumen, latencia, técnica y evidencia; y la ventana de sincronización como cuello de botella vigente. La disposición C3 de los ocho índices sensibles está recibida; fuga, latencia, rotación, contratos y mediciones reales permanecen condicionados.
