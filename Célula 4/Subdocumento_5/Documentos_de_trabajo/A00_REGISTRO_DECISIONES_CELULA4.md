# Registro de decisiones y pendientes — Célula 4

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Versión:** 1.0 · 6 de septiembre de 2026

---

## Cómo se lee este registro

Sigue el formato del registro de decisiones de Célula 2, para que ambos se lean igual: **decisión**, **fundamento**, **alternativas evaluadas**, **consecuencias** y **vinculación**. Cada entrada declara si queda pendiente de validar y con quién.

Se distinguen dos cosas que en la práctica se confunden:

- **Decisión de Célula 4 (`DEC-C4-xx`).** La materia es nuestra, la cerramos y la argumentamos. Que esté cerrada no significa que sea irreversible: significa que nadie más tiene que resolverla para que el Subdocumento 5 avance.
- **Pendiente (`PEN-xx`).** La materia **no** es nuestra. Se declara, se traza a la célula responsable y se deja la pregunta concreta formulada. No se completa por criterio propio.

**Regla que gobierna el registro:** ante la duda, pendiente. Un dato inventado en un modelo o en un diccionario es invisible —una celda con un valor plausible parece un hecho y nadie la vuelve a revisar—, y las Bases lo sancionan por partida doble: valores sin derivación (`CP, Cap. 14.2`) y supuestos presentados como hechos confirmados por el CLIENTE (`CP, Cap. 17.1`).

---

# Parte I — Decisiones de Célula 4

## `DEC-C4-01` — Criterio de reparto del consumo energético entre contenedores

**Decisión.** El consumo medido de un equipo de patio se atribuye a los contenedores por **movimientos ejecutados**: cada movimiento registrado por ese equipo dentro de la ventana de medición recibe una fracción igual del consumo de la ventana. La fracción, el criterio y la versión del algoritmo quedan almacenados en cada atribución.

**Fundamento.**

1. **Es el único criterio con dato duro del CLIENTE detrás.** El caso entrega los movimientos de patio —≈1.290.000 al año, incluidas remociones, con proyección a ≈1.480.000— y los de muelle —≈972.000, con proyección a ≈1.140.000— como volumetría operacional entregada, no estimada `(CP, Cap. 14.1)`. Los otros dos criterios exigirían datos que nadie ha levantado.
2. **No requiere instrumentación adicional.** El movimiento ya se registra con su instante real, su equipo y sus celdas de origen y destino, porque lo exigen `RF-PAT-05` y `RF-PAT-12` para otro fin. La atribución es un cruce sobre datos que el sistema captura de todos modos.
3. **La trazabilidad hasta el dato de origen queda completa.** `RF-EMI-04` obliga a descender desde la emisión hasta el dato que la origina. Con este criterio la cadena es directa: emisión → atribución → movimiento → equipo → consumo medido, y cada eslabón tiene instante propio.
4. **Es verificable por un tercero, que es el criterio de aceptación.** El resultado de negocio N.º 16 del caso exige que las emisiones se midan con metodología declarada y verificable por un tercero, y `RF-EMI-06` exige el reporte efectivamente verificado. Un verificador puede hacer dos comprobaciones sin conocer el terminal: que la suma de las fracciones atribuidas de cada consumo sea exactamente 1, y que el recuento de movimientos coincida con el que el terminal ya reporta al concedente. Ninguna de las dos comprobaciones es posible con los otros criterios.
5. **Trata correctamente las remociones.** El terminal tiene un 18 % de movimientos de patio que son remociones `(CP, Cap. 7.2)`. Un contenedor mal ubicado que exige tres remociones consume energía real tres veces, y este criterio se la atribuye. Es además coherente con el resultado de negocio N.º 8, que compromete bajar las remociones: si bajan, baja la emisión atribuida, y el indicador ambiental y el operacional se mueven juntos.

**Alternativas evaluadas y por qué se descartan.**

| Alternativa | Por qué se descarta |
|---|---|
| **Tiempo de ciclo** | Exige conocer la ocupación del equipo por contenedor, que depende de la frecuencia de posicionamiento. Esa frecuencia —2 segundos— es un **valor de diseño declarado como supuesto no validado** en la volumetría de Célula 2. Construir la metodología de emisiones sobre un supuesto propio no verificado la vuelve indefendible ante el verificador, que es justamente a quien hay que convencer. |
| **Masa movida** | **No es aplicable a todo el flujo.** La verificación de masa bruta es exigible para la exportación por el convenio SOLAS `(RN-05, RF-GAT-08)`; los contenedores de importación no tienen VGM registrado. El criterio dejaría sin método a un flujo completo. Además, en un equipo de patio la masa propia del equipo domina el consumo, de modo que la relación con la masa de la carga no es lineal y habría que declarar una curva que nadie ha levantado. |

**Consecuencias que se asumen y se declaran.** El criterio ignora que un ciclo hacia un bloque lejano consume más que uno hacia un bloque contiguo. Se asume conscientemente: el modelo conserva `celda_origen` y `celda_destino` en cada movimiento, de modo que un refinamiento posterior ponderado por distancia **no cambia el modelo de datos**, solo la versión del algoritmo de reparto — que por eso se almacena en cada atribución. La transición entre versiones es auditable y las emisiones ya calculadas se siguen reproduciendo.

**Alcance.** Cubre el consumo de los 74 equipos instrumentados. El consumo de las seis grúas de muelle **no** entra por esta vía: su sistema de control no se interviene y su telemetría es de solo lectura sujeta a autorización del fabricante `(CP, Cap. 15, RT-17.06)`. Ver `PEN-04`.

**Vinculación.** `RF-EMI-01`, `RF-EMI-02`, `RF-EMI-03`, `RF-EMI-04`, `RF-EMI-06` · Decisiones N.º 16 y 17 de Célula 2 · `D-06c.ATRIBUCION_CONSUMO` · § 5.14 del Subdocumento 5.

**¿Pendiente de validar?** Sí, con el CLIENTE y con el verificador externo, antes de comprometer la cifra en la oferta final. La decisión no espera esa validación para cerrarse: la metodología declarada es la que el caso exige, y declarar una es mejor que no declarar ninguna.

---

## `DEC-C4-02` — Retención de la serie de temperatura refrigerada

**Decisión.** `MUESTRA_TEMPERATURA` se retiene **5 años completos**. La agregación a los 2 años opera sobre la **resolución** de la capa local de alta frecuencia, no sobre la existencia de la serie reportada.

**Fundamento.** `CP, Cap. 15, RT-05.10` fija dos plazos que parecían chocar sobre la misma entidad: series de temperatura de carga refrigerada, 5 años como evidencia de cadena de frío; telemetría de equipos, 2 años en línea con agregación posterior. No chocan, porque no hablan del mismo dato. La temperatura de la **carga** es evidencia contractual frente al mercado de destino y frente al exportador `(RNF-CUM-08, criterio de aceptación N.º 12)`; la telemetría de **equipos** es dato de operación. El modelo de dos capas de la Decisión N.º 8 de Célula 2 lo hace explícito: el muestreo local de 1 a 5 minutos se agrega en el concentrador de patio y lo que se reporta al núcleo cada 5 a 15 minutos es la serie. **La serie reportada es la evidencia; la muestra local de alta frecuencia no lo es.**

**Consecuencia.** El atributo `origen` de la muestra —*borde local* o *agregado reportado*— deja de ser informativo y pasa a ser **el discriminador del ciclo de vida**. Sin él no se puede aplicar la política.

**Vinculación.** `RT-05.10` · `RNF-CUM-08` · `RNF-CUM-14` · Decisión N.º 8 de Célula 2 · `D-04.MUESTRA_TEMPERATURA` · § 5.12.

**¿Pendiente de validar?** No. Se deriva de las Bases y del cierre vigente de Célula 2.

---

## `DEC-C4-03` — Cuatro clases de retención propias para lo que las Bases no clasifican

**Decisión.** A las ocho clases de `RT-05.10` se agregan cuatro categorías propias: **maestro** (mientras la entidad opere, más el plazo del dato que referencia), **permanente** (parámetro de gobierno, no caduca), **vigencia del contrato más seis meses** y **hereda la clase que transporta**.

**Fundamento.** `RT-05.07` obliga a declarar la política de retención por **cada** dominio de datos, y `RNF-CUM-14` prohíbe el plazo uniforme. Las ocho clases del caso cubren los datos de operación, pero dejan sin clasificar 24 de las 80 entidades del modelo: los maestros, los parámetros de gobierno, los contratos de interfaz y los mensajes. Dejarlas sin clase sería incumplir `RT-05.07`; meterlas a la fuerza en una clase existente sería declarar un plazo falso.

Los cuatro criterios se derivan de obligaciones existentes, no se inventan: un maestro no puede eliminarse antes que el último dato operacional que lo referencia, o los registros retenidos quedan ilegibles; un contrato de interfaz debe sobrevivir su preaviso de obsolescencia de seis meses `(RT-05.17)`; y un mensaje no tiene plazo propio porque su contenido puede ser cualquier clase.

**Vinculación.** `RT-05.07` · `RT-05.17` · `RNF-CUM-14` · § 5.12 y sección 6 de A-02.

**¿Pendiente de validar?** Sí, con el CLIENTE al aprobar la política de retención. No bloquea.

---

## `DEC-C4-04` — Dos campos propios en el diccionario de datos

**Decisión.** Cada atributo del diccionario declara, además de los seis campos que exige `RT-05.01`, su **clase de retención** y su **fuente de verdad**.

**Fundamento.** Los seis campos del documento transversal describen un dato en un sistema único y estable. Este caso no es ninguna de las dos cosas: hay coexistencia con el sistema de 2012 durante toda la Etapa 1, con autoridad que se desplaza por dominio, zona y fase; y hay ocho clases de retención distintas que `RNF-CUM-14` prohíbe uniformar. Un diccionario que no diga quién puede escribir cada atributo y cuánto vive no es aplicable a este terminal.

**Vinculación.** `RT-05.01` · `BA, Art. 23` · `RF-CON-14` · A-02, sección 1.1.

**¿Pendiente de validar?** No. Es formato propio y no contradice ninguna base.

---

## `DEC-C4-05` — Regla de obligatoriedad de tres valores

**Decisión.** La obligatoriedad de cada atributo toma uno de tres valores: **obligatorio**, **condicional** (el modelo declara la condición de nulidad) o **derivado** (se calcula y se audita, no se captura).

**Fundamento.** `RT-05.01` pide declarar la obligatoriedad, sin fijar la escala. La distinción entre obligatorio y derivado no es cosmética: `RT-05.04` exige validación en el punto de captura, y un atributo derivado no se valida en captura sino que se recalcula y se contrasta contra su fórmula. Marcarlos permite además impedir su edición manual, que es lo que `RF-FAC-07` prohíbe expresamente para los hechos facturables y lo que sostiene la restricción de no reconstruir indicadores.

**Consecuencia.** Diez atributos del modelo quedan marcados como derivados, y cuatro de ellos sostienen indicadores comprometidos: estadía del camión, cumplimiento de la hora de inspección, productividad de grúa y minutos de desconexión refrigerada.

**Vinculación.** `RT-05.01` · `RT-05.03` · `RT-05.04` · `RF-FAC-07` · A-02, secciones 1.3 y 5.

**¿Pendiente de validar?** No.

---

## `DEC-C4-06` — Cuatro capacidades lógicas sobre dos familias de motor

**Decisión.** El Subdocumento 5 adopta las cuatro capacidades lógicas de Célula 3: `DATA-CORE` (operacional transaccional), `DATA-TS` (series temporales), `DATA-DOC` (documentos, evidencia e histórico) y `DATA-AN` (analítica). Se implementan con dos familias de motor: PostgreSQL —incluida su extensión temporal y réplica/vista analítica— y almacenamiento de objetos. Son separaciones funcionales; no implican cuatro productos independientes.

**Fundamento.** `RT-05.05` y el Formulario T-7 hablan de separar transaccional y analítico. En este caso esa partición oculta la familia que domina el volumen: la telemetría reporta ≈7,2 eventos por segundo al núcleo y ≈36 en el borde, frente a ≈0,23 transacciones de negocio por segundo en el peak de coincidencia. El propio caso advierte que la telemetría puede superar en órdenes de magnitud a las transacciones y que la frecuencia de muestreo es una decisión de diseño con consecuencias de costo, red y almacenamiento `(CP, Cap. 14.2)`. Subsumir las series en el almacén analítico sería describir mal el sistema que se está proponiendo.

**Vinculación.** `RT-05.05` · `CP, Cap. 14.2` · volumetría de Célula 2 · § 5.6 y § 5.13.

**¿Pendiente de validar?** No con las Bases ni con Célula 3 para I1. La distribución física y el dimensionamiento final permanecen sujetos a las pruebas y condicionantes declaradas por Célula 3.

---

## `DEC-C4-07` — Contenedor maestro y VisitaContenedor operacional

**Decisión.** `Contenedor` es el maestro del activo físico. `VisitaContenedor` —identificada físicamente como `VISITA` para conservar claves y referencias del diccionario— es cada estadía de ese activo y el agregado sobre el que se asocian movimientos, posición, hechos facturables y emisiones. `Recalada` o `VisitaNave` queda reservada para la estadía de una nave.

**Fundamento.** El mismo contenedor físico vuelve al terminal muchas veces. `RN-04` cuenta los días de almacenaje desde el día siguiente a la descarga o al ingreso a patio, lo que solo tiene sentido sobre una estadía concreta; la estadía del camión y los hechos facturables se cuentan igual. Colgar todo del contenedor obligaría a filtrar por rango de fechas en cada consulta y haría irreproducible el cálculo de almacenaje.

**Vinculación.** `RN-04` · `RF-FAC-03` · `RF-GAT-12` · `D-02.VISITA`.

**¿Pendiente de validar?** No; convención alineada con el modelo de alto nivel de Célula 3.

---

## `DEC-C4-08` — El conductor es una especialización de la persona

**Decisión.** `CONDUCTOR` no guarda documento de identidad: referencia a `PERSONA`, que es la única entidad del modelo que guarda ese dato.

**Fundamento.** `RT-05.09` obliga a una estrategia de datos maestros que evite la duplicación de entidades compartidas entre módulos. La versión 2.0 del modelo declaraba `documento_identidad` con marca de unicidad y cifrado de campo en las dos entidades, mientras `PERSONA.tipo` ya incluía el valor «conductor». La consecuencia no era estética: significaba cifrar, retener y eliminar el mismo dato personal dos veces, con dos plazos que pueden divergir — el hallazgo que una auditoría de protección de datos encuentra primero.

**Vinculación.** `RT-05.09` · `RT-11.10` · `BA, Art. 85` · corrección v2.1 del modelo · `D-03.CONDUCTOR`.

**¿Pendiente de validar?** No.

---

## `DEC-C4-09` — La verificación de masa bruta admite repesaje

**Decisión.** Una visita puede tener más de un pesaje, distinguidos por número de secuencia. La tolerancia de `RN-05` se evalúa sobre el **pesaje vigente**, no sobre el primero.

**Fundamento.** `RF-GAT-09` gestiona la discrepancia de masa bruta sobre tolerancia, y esa gestión puede terminar en un repesaje. El modelo anterior admitía un solo registro por visita, de modo que el segundo pesaje no tenía dónde guardarse y la evidencia de la corrección se perdía — justo la evidencia que `RT-05.10` obliga a retener cinco años.

**Vinculación.** `RF-GAT-08` · `RF-GAT-09` · `RN-05` · `RNF-CUM-04` · `D-03.PESAJE_VGM`.

**¿Pendiente de validar?** No.

---

## `DEC-C4-10` — Origen único y polimórfico de la alarma refrigerada

**Decisión.** El objeto que origina una alarma se registra una sola vez, con el par `tipo_objeto_origen` + `id_objeto_origen`.

**Fundamento.** Una alarma puede originarse en una conexión, en una toma o en un tablero. La versión 2.0 resolvió el polimorfismo pero conservó la clave foránea anterior hacia la conexión, de modo que una alarma de conexión guardaba el mismo dato en dos campos que podían discrepar y ningún lector sabía cuál mandaba. En una entidad que es evidencia de cadena de frío, la ambigüedad es un defecto, no una redundancia.

**Vinculación.** `RF-REF-04` a `RF-REF-07` · `RN-08` · `D-04.ALARMA`.

**¿Pendiente de validar?** No.

---

## `DEC-C4-11` — Célula 4 asume la gestión de calidad ISO/IEC 25012

**Decisión.** Mientras Célula 2 no incorpore un requerimiento no funcional de calidad de datos, **Célula 4 asume íntegra** la materia en el Subdocumento 5 y propone el texto del requerimiento para que quede trazado en el Formulario T-12.

**Fundamento.** La obligación es firme y triple: `BTT, Cap. 5, RT-05.04` la exige con validación en el punto de captura, indicadores de completitud, exactitud y consistencia y tablero disponible para el CLIENTE; `BA, Art. 23` añade el saneamiento de los datos migrados; y `BA, Art. 13` lista la norma entre los estándares exigibles. El catálogo vigente de 91 requerimientos no funcionales de Célula 2 no la cubre, y Célula 3 la declara pendiente remitiéndola expresamente al cruce entre este subdocumento y el plan de pruebas. Es un vacío sin dueño, y el Subdocumento 5 es donde se nota si nadie lo toma.

**Consecuencia.** La materia se desarrolla en A-03. La confirmación de si además se crea el requerimiento en el catálogo queda en `PEN-05`, pero **no condiciona** el desarrollo.

**Vinculación.** `RT-05.04` · `BA, Art. 13` y `Art. 23` · § 5.11 · A-03.

**¿Pendiente de validar?** Sí, con Célula 2, solo en cuanto a la trazabilidad en el T-12.

---

## `DEC-C4-12` — El catálogo de campos cifrados se deriva del diccionario

**Decisión.** El catálogo de campos sujetos a cifrado a nivel de campo es el de la sección 4 de A-02: 28 atributos en las tres familias que identifica el caso. Es propuesta de Célula 4, construida desde el modelo.

**Fundamento.** `RNF-SEG-05` compromete cubrir el 100 % de los campos identificados como sensibles, y `CP, Cap. 15, RT-11.10` nombra las tres familias: datos personales, información comercial sensible y datos que permitan inferir el contenido de valor o la ruta de un contenedor. Nadie había producido la lista. Un compromiso de cobertura sobre un conjunto que no existe no es verificable.

**Consecuencia declarada.** Ocho de esos atributos son a la vez clave de acceso indexada en el catálogo de operaciones críticas. Célula 3 respondió en D1 B4.3 con tres patrones: cifrado aleatorio más token de igualdad protegido, identificador sustituto opaco o consulta dentro del servicio propietario. Ninguno equivale a escoger cifrado determinista por defecto; los ocho quedan sujetos a pruebas de fuga, latencia, rotación y continuidad local.

**Vinculación.** `RT-11.10` · `RNF-SEG-05` · `RT-16.09` · A-02, sección 4 · § 5.10 y § 5.12.

**¿Pendiente de validar?** Sí, con Célula 2 en cuanto a si el catálogo pasa a su registro, y con Célula 3 en cuanto al mecanismo.

---

## `DEC-C4-13` — Identificadores propios con tabla de equivalencia

**Decisión.** El modelo usa identificadores propios y estables de Célula 4 —`DOM-`, `ENT-`, `EVT-`, `INV-`— y mantiene una tabla de equivalencia de una sola columna hacia los identificadores de Célula 3.

**Fundamento.** Los identificadores definitivos de contextos lógicos los produce Célula 3 y todavía no existen. Esperar habría detenido el modelo entero; adoptar los suyos provisionalmente habría obligado a un renombrado masivo si cambian. La tabla de equivalencia hace que el costo de alinearse sea de una columna.

**Vinculación.** `PEN-01` · Anexo H del Subdocumento 5.

**¿Pendiente de validar?** No como decisión. La equivalencia se completa cuando Célula 3 publique su catálogo.

---

## `DEC-C4-14` — Regla de cita: documento, capítulo, código y materia

**Decisión.** Ninguna afirmación del Subdocumento 5 cita un código `RT` aislado. La referencia mínima es **documento + capítulo + código + materia**.

**Fundamento.** Los códigos se repiten entre documentos designando materias distintas. El caso verificado más relevante para este subdocumento es `RT-05.10`: en las Bases Técnicas Transversales designa el catálogo de datos con linaje automatizado, de carácter deseable, y en las Bases Técnicas del Caso designa la retención de datos históricos, de carácter «según caso». Lo mismo ocurre con `RT-05.15` y con `RT-03.24`. Citar el código suelto puede invertir el sentido de la obligación.

**Vinculación.** § 5.1.1 del Subdocumento 5 · `config/02-comandos-subdoc5.tex`.

**¿Pendiente de validar?** No.

---

## `DEC-C4-15` — Cascada determinista de resolución de conflictos de posición

**Decisión.** Un conflicto de posición producido durante una partición se resuelve por una cascada de cuatro niveles aplicados en orden: **autoridad** sobre el dominio, zona y fase en el instante del hecho; **credibilidad de la fuente** —telemetría sobre lectura óptica, y ambas sobre la vía manual—; **orden secuencial** de la visita; y, si los tres anteriores no resuelven, **verificación física**, dejando la posición en estado *por verificar*.

**Fundamento.** `CP, Cap. 15, RT-03.13` exige resolución determinista de los conflictos de posición producidos durante la desconexión, y `BTT, Cap. 3, RT-03.12` exige regla documentada y bitácora auditable. La lista de decisiones que no deben tomarse silenciosamente prohíbe expresamente usar «la última escritura gana» sin justificar el conflicto de posición y autoridad — y con razón: una escritura posterior emitida por un sistema **sin** autoridad territorial no puede prevalecer sobre una anterior emitida por quien sí la tenía, o la invariante `INV-01` se rompe justo cuando más importa.

**Alternativa evaluada y descartada.** Resolver el cuarto nivel de forma automática, escogiendo por ejemplo el registro más reciente. Se descarta porque **subiría el indicador y bajaría la verdad**: el compromiso no es cero posiciones dudosas, sino que toda posición declarada *conocida* sea correcta. Una posición dudosa declarada cierta es peor que una posición declarada dudosa.

**Consecuencia que se asume.** La sincronización puede terminar con posiciones sin resolver. Es coherente con la meta comprometida, que acota el residual a las posiciones *por verificar* no resueltas al cierre de turno.

**Vinculación.** `RT-03.12` · `CP, Cap. 15, RT-03.13` · `RF-PAT-03`, `RF-PAT-04`, `RF-PAT-05`, `RF-PAT-12` · `INV-01`, `INV-02`, `INV-03` · A-06, sección 6 · § 5.5.

**¿Pendiente de validar?** El nivel 1 depende de las zonas y fases nombradas, que corresponden a `PEN-01`. La cascada como regla no depende de esos nombres.

---

## `DEC-C4-16` — Ninguna unidad transaccional cruza la frontera entre familias de persistencia

**Decisión.** Las ocho unidades transaccionales del modelo se confirman dentro de un solo motor. En el caso límite —el hecho facturable y su evidencia—, el objeto binario se escribe **antes** en el almacenamiento de objetos y la transacción relacional confirma un puntero a un objeto que ya existe. Si el objeto no se escribió, la transacción no confirma.

**Fundamento.** Una transacción distribuida entre el motor relacional y el almacenamiento de objetos introduciría un coordinador en la ruta de escritura de operaciones cuyo umbral es de un segundo `(CP, Cap. 15, RT-09.01)`. La secuencia escribir-objeto-luego-confirmar-puntero da la misma garantía que importa —`INV-08`: no existe hecho facturable sin evidencia— sin coordinador y sin comprometer el umbral. El costo es un objeto huérfano si la transacción falla después de escribir el binario, que se resuelve con una recolección periódica y es un problema de espacio, no de integridad.

**Vinculación.** `RT-05.02` · `RT-09.01` · `INV-08`, `INV-09` · A-05, Familia 3 · A-06, sección 3 · § 5.4 y § 5.5.

**¿Pendiente de validar?** No.

---

## `DEC-C4-17` — El flujo crudo de posicionamiento de equipos no se persiste

**Decisión.** Los 37 eventos por segundo de posicionamiento de equipos móviles se procesan en el borde y **no se persisten como dato**. Lo que se persiste es el `MOVIMIENTO` derivado, con su instante real, su equipo, sus celdas y su fuente de registro.

**Por qué fue necesario decidirlo.** El modelo conceptual no tiene ninguna entidad para la posición cruda de un equipo, y esa ausencia parecía un olvido. Sin la decisión explícita, la volumetría no cuadra por un orden de magnitud.

**Fundamento.** Persistir el flujo crudo serían 1.167 millones de filas al año, equivalentes a ≈ 350 GB anuales, contra los ≈ 20 GB de almacenamiento transaccional que declara la volumetría vigente. Los dos números solo son compatibles si el crudo no entra al almacén transaccional, que es el supuesto implícito de Célula 2 y que aquí se hace explícito. Además, ningún requerimiento consulta la trayectoria continua de un equipo: `RF-PAT-05` y `RF-PAT-12` piden registrar el **movimiento**, y la coordenada es el insumo del que se deriva. El documento transversal valora expresamente el procesamiento en el borde para reducir el volumen transferido `(BTT, Cap. 3, RT-03.19)`.

**Consecuencia que se asume.** No se podrá reconstruir a posteriori la trayectoria exacta de un equipo. Si el CLIENTE lo pidiera, es una capacidad nueva con su propio dimensionamiento.

**Vinculación.** `RF-PAT-05`, `RF-PAT-12` · `RT-03.19` · volumetría C2 filas 5, 8 y 15 · A-07 sección 2 · A-08.

**¿Pendiente de validar?** No como decisión de datos. Conviene informarla a Célula 3, que dimensiona la red de patio con ese tráfico.

---

## `DEC-C4-18` — Política de particionamiento

**Decisión.** Se particiona por tiempo solo cuando concurren dos condiciones: que la entidad supere el orden de los cien millones de filas en su período de retención **y** que su ciclo de vida exija eliminar o agregar por antigüedad. Cumplen las dos **cuatro entidades**: `MUESTRA_TEMPERATURA`, `MOVIMIENTO`, `EVENTO_ACCESO` y `REGISTRO_AUDITORIA`. Las otras 76 no se particionan.

**Por qué fue necesario decidirlo.** El Formulario T-7 exige declarar una estrategia de particionamiento. Sin regla explícita, la decisión queda al criterio de quien implemente y no es defendible ni reproducible.

**Fundamento.** El argumento es la **eliminación**, no la consulta. En una tabla particionada por tiempo, eliminar un período es descartar una partición; sin particionar es un borrado masivo sobre una tabla viva, en un terminal que no tiene ventana de detención total `(restricción N.º 2)` y que tiene prohibido intervenir entre el 15 de diciembre y el 30 de abril `(restricción N.º 9)`. La retención diferenciada de `RNF-CUM-14` no es ejecutable sin particionamiento en esas cuatro entidades. Particionar el resto agregaría complejidad de mantenimiento sin beneficio medible, contra la restricción N.º 11.

**Vinculación.** `RT-05.10` · `RNF-CUM-14` · restricciones N.º 2, 9 y 11 · `DEC-C4-02` · A-07 sección 4.

**¿Pendiente de validar?** La disponibilidad de particionamiento declarativo y de índices parciales depende del motor, que es `PEN-07`.

---

## `DEC-C4-19` — Política de caché

**Decisión.** Se cachea únicamente lectura tolerante a desfase, con desfase máximo declarado, invalidación por evento y fuente de verdad identificada en la respuesta. **Nunca se cachea** ningún dato con estado de confianza asociado, ningún dato bajo autoridad variable durante la coexistencia, ningún insumo de la condición de liberación y ninguna evidencia.

**Por qué fue necesario decidirlo.** El Formulario T-7 exige declarar la estrategia de caché, y en este caso una caché mal ubicada rompe una invariante comprometida: servir una posición cacheada como vigente destruye el compromiso de que **toda posición declarada conocida es correcta**.

**Consecuencia que se asume.** La consulta de posición, que es la operación más frecuente del sistema, no se resuelve con caché sino con índice sobre una tabla de tamaño acotado. Por eso los índices sobre `POSICION_VIGENTE` son irrenunciables.

**Vinculación.** `INV-03`, `INV-07` · `RF-GAT-13` · `PAR-2` de A-06 · A-07 sección 5.

**¿Pendiente de validar?** No.

---

## `DEC-C4-20` — Primer cuello de botella y mecanismo de crecimiento

**Decisión.** El primer cuello de botella es **la ventana de sincronización posterior a la operación desconectada**, y su componente dominante son las imágenes de reconocimiento, que aportan ≈ 11,2 de los 13 GB actuales.

**Por qué fue necesario decidirlo.** `BTT, Cap. 9, RT-09.05` obliga a identificar el componente que primero saturará al crecer la carga y a explicar cómo se detecta y cómo se resuelve. Es una declaración obligatoria: hay que escoger uno y sostenerlo.

**Corrige una conclusión anterior.** El esqueleto declaraba que el primer cuello sería la ingesta de series temporales. Rehecho el cálculo, esa conclusión no se sostiene: el núcleo transaccional pasa de 0,23 a 0,7 transacciones por segundo y la ingesta al núcleo de 7,2 a 21,6 eventos por segundo, ambos absorbibles. En cambio, la baseline I1 peak exige 32,5 Mbps y el escenario futuro 3× exige 57,8 Mbps para la misma ventana de 90 minutos. Es el margen que se estrecha con el crecimiento.

**Cómo se resuelve, en orden:** reducir lo que cruza el enlace antes que ampliarlo; separar la sincronización que restablece invariantes de la que restablece evidencia; agregación previa en el borde para las series; y ampliar el enlace como última opción, por ser la única con costo recurrente y dependencia de terceros.

**Interpretación declarada.** El segundo punto se apoya en una lectura del alcance de `CP, Cap. 15, RT-03.13`: que el plazo protege la integridad de movimientos y hechos facturables, y no la transferencia completa del volumen de 72 horas. **Es interpretación de Terabyte, no un hecho del caso**, y se consulta formalmente en `PEN-16`. Si se rechaza, la alternativa conservadora es dimensionar el enlace para los 58 Mbps proyectados: cambia el costo, no el diseño.

**Detección anticipada por calendario.** La alerta se dispara al superar el 70 % de la capacidad de la ventana, medido mensualmente, porque la restricción N.º 9 impide intervenir entre el 15 de diciembre y el 30 de abril: toda holgura debe estar instalada antes del 15 de diciembre.

**Vinculación.** `RT-09.03`, `RT-09.05`, `RT-09.09` · `CP, Cap. 15, RT-03.13` · restricción N.º 9 · A-06 § 8 · A-07 sección 7.

**¿Pendiente de validar?** Sí, en la interpretación de `PEN-16`. La identificación del cuello de botella no depende de esa validación.

---

## `DEC-C4-21` — Frontera entre almacenamiento en línea y archivo recuperable

**Decisión.** El almacenamiento se reparte en dos modos con esta frontera: movimientos y operación, **3 años en línea** y años 4 a 10 en archivo; series de temperatura, **2 años granulares** y años 3 a 5 agregados; evidencia facturable y verificación de masa bruta, **2 años en línea** y el resto en archivo; imágenes de reconocimiento, sus 12 meses completos en línea; accesos de personas, 2 años en línea; telemetría de equipos y eventos de seguridad, según los plazos que el caso ya fija. Archivo significa **restauración dirigida ≤ 24 horas**; la evidencia en línea mantiene el umbral de ≤ 30 segundos.

**Por qué fue necesario decidirlo.** Sin frontera, la capacidad no es calculable: había que elegir entre dimensionar diez años de todo en línea —que triplica la capacidad y su costo— o inventar el corte. Además `RT-05.07` obliga a declarar la política de **archivado**, no solo la de retención.

**Fundamento — el caso ya fijó esta frontera dos veces y aquí se extiende el mismo criterio.** `CP, Cap. 15, RT-05.10` declara para la telemetría «2 años en línea, con política de agregación declarada para el resto»; `BTT, Cap. 11, RT-11.14` hace lo mismo con los eventos de seguridad, doce meses en línea y veinticuatro en archivo. Y los tres años de la operación no son elección nuestra: `CP, Cap. 15, RT-05.15` obliga a migrar **tres años** de movimientos y deja los años 4 a 10 en repositorio consultable. El propio caso trata tres años como la ventana operacionalmente relevante.

**Consecuencia que se asume.** Una objeción de facturación sobre un hecho de más de dos años exigirá restauración desde archivo. Es aceptable: las objeciones se presentan dentro del ciclo comercial y la ventana de dos años lo cubre con holgura frente al 4,7 % de facturas objetadas de la línea base.

**Vinculación.** `RT-05.07` · `CP, Cap. 15, RT-05.10` y `RT-05.15` · `BTT, Cap. 11, RT-11.14` · `RNF-CUM-14` · `DEC-C4-02`, `DEC-C4-03` · `CAL-38` · A-08 sección 3.

**¿Pendiente de validar?** Sí, con el CLIENTE al aprobar la política de retención. No bloquea el dimensionamiento.

---

# Parte II — Pendientes, con su célula responsable

## Pendientes de **Célula 3** — Subdocumento 4

| ID | Pendiente | Pregunta concreta | Qué bloquea |
|---|---|---|---|
| `PEN-01` — RECIBIDO | Nombres de las zonas operativas que estructuran la autoridad del dato | A3 §3 define bloque no migrado, validación paralela y bloque con cutover, y reutiliza la Decisión 1 de Célula 2. La segmentación física exacta sigue parametrizada | `D-08.ZONA_OPERATIVA.nombre` · § 5.3 · § 5.9 |
| `PEN-02` — RESPONDIDO PARA I1 | Mecanismo de cifrado a nivel de campo y su efecto sobre la indexación | Los ocho atributos admiten una ruta de igualdad propuesta en D1 B4.3; no se usa cifrado determinista directo. `clase_imdg`, ubicación y trazas personales permanecen especialmente condicionadas por fuga de frecuencia/correlación | § 5.10, umbrales de `RT-09.01`; pruebas y aceptación pendientes |
| `PEN-03` — CERRADO I1 | Propiedad del modelo conceptual | Subdocumento 4 publica alto nivel; Subdocumento 5 mantiene modelo detallado/diccionario; nombres compartidos fijados | § 5.2 y § 5.14 |
| `PEN-06` — RECIBIDO | Mecanismo de integración y eventos | A2 define `INT-HUB` persistente, idempotencia, DLQ/replay y contrato tipo; CDC del TOS queda condicionado externamente | § 5.6, § 5.8 y § 5.10 |
| `PEN-07` — RECIBIDO | Emplazamiento y motores | AWS normal con PostgreSQL/RDS propuesto; estado crítico y PostgreSQL local durante corte; objetos e histórico en familia de objetos | § 5.4, § 5.5 y § 5.13 |
| `PEN-08` — CERRADO I1 | Revalidación de la volumetría | 18 dimensiones conservadas; promedio, peak, 3× e imagen 1 MB separados | § 5.13, § 5.12 y § 5.10 |
| `PEN-17` | Latencia real de la red de patio con pilas cargadas, y ancho de banda del enlace de reposición | ¿Qué latencia sostiene la red inalámbrica en condición de patio cargado, y qué ancho de banda tiene el enlace de reposición? | El umbral de 1 s de la confirmación de movimiento y los 58 Mbps proyectados |
| `PEN-18` | Política de captura de imágenes: resolución, compresión y si el binario cruza el enlace dentro de la ventana | Conjunta con Célula 4: la resolución la condiciona el equipo de reconocimiento óptico que especifica Célula 3, y el umbral de 3 s depende de ella | La primera palanca de crecimiento de `DEC-C4-20` y la de mayor efecto sobre la capacidad de A-08 |
| `PEN-19` | Esquema de copias que satisface el respaldo 3-2-1-1-0 sobre el almacenamiento de objetos | ¿Cuántas copias, dónde y con qué mecanismo de inmutabilidad? | `SUP-A08-03`, el supuesto con más efecto sobre la capacidad a aprovisionar |

## Pendientes de **Célula 2** — Subdocumento 3

| ID | Pendiente | Pregunta concreta | Qué bloquea |
|---|---|---|---|
| `PEN-04` | Evento del que se deriva el movimiento de grúa de muelle | El universo instrumentable de 74 y 88 equipos excluye las seis grúas de muelle. ¿De qué evento se deriva el movimiento de muelle, sabiendo que el sistema del fabricante no se interviene? | `D-02.MOVIMIENTO.id_recalada` · § 5.7 · alcance de `DEC-C4-01` |
| `PEN-05` | Requerimiento no funcional de calidad de datos | El catálogo de 91 RNF no cubre `RT-05.04`. ¿Crean el requerimiento para que quede trazado en el T-12, o basta con que la materia viva en el Subdocumento 5? | Trazabilidad en el Formulario T-12; no bloquea A-03 |
| `PEN-09` | Bandas de desviación de temperatura de `RN-11` | ¿La banda y la duración mínima quedan abiertas en el Informe 1, o se acotan a un rango justificado con el CLIENTE? | `D-04.PARAMETRO_DESVIACION.banda_superior` y `banda_inferior` · § 5.7 |
| `PEN-10` | Vigencia de `RF-PAT-07` | Sigue declarado pendiente de validación interna. ¿Se trata como vigente para el modelo de condiciones dinámicas del patio? | `D-02.CONDICION_DINAMICA` |
| `PEN-11` | Confirmación del catálogo de campos cifrados | ¿El catálogo de `DEC-C4-12` pasa al registro de Célula 2 o se queda como anexo del Subdocumento 5? | Trazabilidad de `RNF-SEG-05` |

## Pendientes del **CLIENTE** y de terceros

| ID | Pendiente | Tratamiento mientras no se resuelve |
|---|---|---|
| `PEN-12` | Esquema, calidad y tamaño reales de la base del sistema de 2012 | Perfilado adelantado al descubrimiento de los meses 1 a 4; el volumen se usa como orden de magnitud declarado |
| `PEN-13` | Fecha exacta de fin de soporte del sistema de 2012 | Escenario conservador con holgura declarada |
| `PEN-14` | Existencia de interfaz por cada autoridad | Canal asistido trazable como alternativa; ninguna interfaz se presume existente |
| `PEN-20` | Volumen real de evidencia documental distinta de las imágenes de reconocimiento | Se estima con método declarado en `SUP-A08-01`; se levanta en los meses 1 a 4 |
| `PEN-15` | Validación de la metodología de emisiones por el verificador externo | `DEC-C4-01` queda cerrada como metodología declarada; la validación se busca antes de comprometer la cifra en la oferta final |
| `PEN-16` | Alcance del plazo de 90 minutos de sincronización: ¿protege la integridad de movimientos y hechos facturables, o la transferencia completa del volumen de 72 h? | Se adopta la primera lectura, declarada como interpretación de Terabyte en `DEC-C4-20`; la alternativa conservadora está dimensionada y costeada |

---

# Parte III — Estado tras este registro

| Materia | Antes | Ahora |
|---|---|---|
| Criterio de reparto del consumo | abierto | **`DEC-C4-01`**, cerrado y argumentado |
| Retención de la serie de temperatura | ambigua entre dos plazos | **`DEC-C4-02`**, resuelta |
| Entidades sin clase de retención | 24 de 80 | **`DEC-C4-03`**, ninguna |
| Catálogo de campos cifrados | no existía | **`DEC-C4-12`**, 28 atributos |
| Calidad ISO/IEC 25012 | sin dueño | **`DEC-C4-11`**, asumida por Célula 4 |
| Bandas de temperatura | abierta | `PEN-09`, Célula 2 y CLIENTE |
| Nombres de zonas operativas | abierta | `PEN-01`, Célula 3 |
| Evento del movimiento de muelle | abierta | `PEN-04`, Célula 2 y Célula 3 |
| Resolución de conflictos de posición | sin regla declarada | **`DEC-C4-15`**, cascada de cuatro niveles |
| Frontera transaccional entre motores | sin declarar | **`DEC-C4-16`**, ninguna unidad la cruza |
| Funciones no disponibles sin enlace | sin declarar — *observación grave* si falta | Declaradas en A-06, sección 7 |
| Persistencia del flujo de posicionamiento | implícita, y la volumetría no cuadraba | **`DEC-C4-17`**, no se persiste |
| Estrategia de particionamiento | sin regla | **`DEC-C4-18`**, cuatro entidades de ochenta |
| Estrategia de caché | sin regla | **`DEC-C4-19`**, con lista de lo que nunca se cachea |
| Primer cuello de botella | supuesto erróneo en el esqueleto | **`DEC-C4-20`**, corregido: la ventana de sincronización |
| Frontera entre línea y archivo | sin declarar; la capacidad no era calculable | **`DEC-C4-21`**, con el criterio que el caso ya usó dos veces |
| Entregas cruzadas hacia Célula 3 | `E-01`, `E-02` y `E-03` abiertas | **Las tres cerradas** en A-08, A-05 y A-07 |

**Veintiuna decisiones C4 registradas y dependencias actualizadas.** El cruce C3–C4 cierra para diseño I1 la topología, semántica, motores, capacidad, cifrado e integración. Permanecen condiciones legítimas del CLIENTE o terceros —bandas de temperatura, contratos reales, site survey, política de imagen, copias y pruebas— que no se rellenan por criterio propio.
