# Decisiones de Célula 4 — Subdocumento 5, Modelo y gestión de datos

**Caso:** 06 Portuaria — TERABYTE
**Emite:** Célula 4 (V. Guzmán / M. Reyes)
**Destinatarios:** Célula 1, Célula 2, Célula 3 y el integrador del Informe 1
**Fecha:** 6 de septiembre de 2026 · **21 decisiones cerradas**

---

## Para qué sirve este documento

Cada decisión de abajo está **cerrada** por Célula 4 y ya está escrita en el Subdocumento 5. No se reabren salvo evidencia nueva o contradicción con una fuente superior, que es la misma regla de autoridad que aplica Célula 3.

Se entrega para tres cosas:

1. que **nadie las contradiga sin saberlo** en su propio subdocumento;
2. que **Célula 3** las use como insumo de sus decisiones de arquitectura, en vez de decidir a ciegas sobre materias de datos;
3. que **Célula 2** sepa qué materias suyas quedaron asumidas por nosotras y decida si las incorpora a su catálogo.

La columna «a quién le importa» dice qué célula debería leer cada una con atención.

---

## Tabla ejecutiva

| ID | Decisión | A quién le importa |
|---|---|---|
| `DEC-C4-01` | El consumo energético se atribuye a contenedores **por movimientos ejecutados** | Célula 3 (`C4`), Célula 2, verificador externo |
| `DEC-C4-02` | La serie de temperatura se retiene **5 años completos**; la agregación a los 2 años opera sobre la resolución, no sobre la existencia | Célula 3 (`C2`, `C4`) |
| `DEC-C4-03` | Cuatro clases de retención propias para las 24 entidades que las Bases no clasifican | Célula 3 (`C4`), Célula 2 |
| `DEC-C4-04` | El diccionario declara dos campos propios: **clase de retención** y **fuente de verdad** | Célula 2, integrador |
| `DEC-C4-05` | Obligatoriedad de tres valores: obligatorio, condicional y **derivado** | Célula 2, plan de pruebas |
| `DEC-C4-06` | Se separan **tres** almacenamientos —transaccional, temporal y analítico—, no dos | Célula 3 (`A1`, `C1`, `C2`) |
| `DEC-C4-07` | La **visita**, y no el contenedor, es el objeto operacional central | Célula 2, Célula 3 (`A1`) |
| `DEC-C4-08` | `CONDUCTOR` es especialización de `PERSONA`: el dato personal se guarda una sola vez | Célula 3 (`D1`), Célula 2 |
| `DEC-C4-09` | La verificación de masa bruta admite **repesaje** con número de secuencia | Célula 2 |
| `DEC-C4-10` | El origen de la alarma refrigerada se registra una sola vez, con par polimórfico | Célula 3 (`A3`) |
| `DEC-C4-11` | Célula 4 **asume íntegra** la gestión de calidad ISO/IEC 25012 | Célula 2, plan de calidad |
| `DEC-C4-12` | El catálogo de campos cifrados se deriva del diccionario: **28 atributos** | Célula 3 (`D1`), Célula 2 |
| `DEC-C4-13` | Identificadores propios con tabla de equivalencia hacia Célula 3 | Célula 3 (`A1`) |
| `DEC-C4-14` | Regla de cita: **documento + capítulo + código + materia** | todas |
| `DEC-C4-15` | Cascada de **cuatro niveles** para resolver conflictos de posición | Célula 3 (`A3`, `C3`) |
| `DEC-C4-16` | Ninguna unidad transaccional cruza la frontera entre motores | Célula 3 (`C2`) |
| `DEC-C4-17` | El flujo crudo de posicionamiento **no se persiste** | Célula 3 (`C3`, `C4`) |
| `DEC-C4-18` | Se particionan **cuatro entidades de ochenta**, por tiempo | Célula 3 (`C2`, `C4`) |
| `DEC-C4-19` | Política de caché con lista explícita de lo que **nunca** se cachea | Célula 3 (`A1`, `C2`) |
| `DEC-C4-20` | El primer cuello de botella es **la ventana de sincronización**, no la ingesta | Célula 3 (`C3`, `C4`) |
| `DEC-C4-21` | Frontera entre almacenamiento **en línea y archivo** por clase | Célula 3 (`C2`, `C4`) |

---

## Las seis que más afectan a otras células

### 1. `DEC-C4-01` — El consumo se reparte por movimientos ejecutados

**Qué decidimos.** Cada movimiento registrado por un equipo dentro de la ventana de medición recibe una fracción igual del consumo de esa ventana. La fracción, el criterio y la versión del algoritmo se almacenan en cada atribución.

**Por qué.** Es el único criterio con dato duro del CLIENTE detrás —los movimientos de patio y de muelle son volumetría entregada, no estimada— y el único que un verificador externo puede comprobar sin conocer el terminal: que las fracciones de cada consumo sumen 1, y que el recuento de movimientos cuadre con lo que el terminal ya reporta al concedente. Descartamos *tiempo de ciclo* porque se apoyaría en la frecuencia de posicionamiento de 2 segundos, declarada como supuesto no validado; y *masa movida* porque la verificación de masa bruta es exigible solo para exportación, de modo que dejaría sin método a todo el flujo de importación.

**Qué implica para ustedes.** Célula 3 debe considerar que el cálculo de emisiones consulta `MOVIMIENTO` por equipo e instante, y que eso exige un índice específico. La cifra de emisión por contenedor que se le informe al cliente depende de esta decisión.

### 2. `DEC-C4-12` — Los 28 atributos que se cifran a nivel de campo

**Qué decidimos.** El catálogo que `RNF-SEG-05` compromete cubrir al 100 % **no existía**. Lo construimos desde el diccionario: 28 atributos en las tres familias que identifica `CP, Cap. 15, RT-11.10`.

**Qué implica para Célula 3.** Ocho de esos atributos son **a la vez clave de acceso indexada**: `POSICION_VIGENTE.id_celda`, `MOVIMIENTO.celda_origen` y `celda_destino`, `CONTENEDOR.clase_imdg`, `LECTURA_OPTICA.codigo_leido`, `CONDUCTOR.id_persona`, `EVENTO_ACCESO.id_persona` y `HECHO_FACTURABLE.id_regla_aplicada`. Un cifrado que impida la búsqueda por igualdad sobre ellos **hace inalcanzables los umbrales de un segundo** de `RT-09.01`. Es la consulta que les dirigimos en el comunicado correspondiente.

### 3. `DEC-C4-15` — Cómo se resuelve un conflicto de posición

**Qué decidimos.** Cascada de cuatro niveles en orden: autoridad sobre dominio, zona y fase en el instante del hecho; credibilidad de la fuente —telemetría sobre lectura óptica, y ambas sobre la vía manual—; orden secuencial de la visita; y verificación física, que deja la posición en *por verificar* sin resolverla automáticamente.

**Por qué no «la última escritura gana».** Una escritura posterior emitida por un sistema **sin** autoridad territorial no puede prevalecer sobre una anterior emitida por quien sí la tenía. El caso lo prohíbe expresamente.

**Qué implica para Célula 3.** El nivel 1 depende de las zonas y fases que ustedes nombren. La cascada como regla no depende de esos nombres, pero su aplicación sí.

### 4. `DEC-C4-17` — El posicionamiento crudo no se persiste

**Qué decidimos.** Los 37 eventos por segundo de posicionamiento se procesan en el borde; se persiste el `MOVIMIENTO` derivado, no la coordenada.

**Por qué importa que lo sepan.** Persistirlo serían 1.167 millones de filas al año, ≈350 GB, contra los ≈20 GB de almacenamiento transaccional que declara la volumetría. **Los dos números solo son compatibles si el crudo no se guarda**, y ese era el supuesto implícito de la volumetría de Célula 2. Ahora es explícito. Célula 3 debe dimensionar la red de patio con ese tráfico igualmente, porque el flujo cruza la red aunque no se almacene.

### 5. `DEC-C4-20` — El primer cuello de botella

**Qué decidimos.** No es la ingesta de series ni el núcleo transaccional: es **la ventana de sincronización posterior a las 72 horas**, dominada por las imágenes de reconocimiento.

**El cálculo.** Contra el crecimiento de 3× que exige `RT-09.03`: el núcleo pasa de 0,23 a 0,7 transacciones por segundo y la ingesta al núcleo de 7,2 a 21,6 eventos por segundo, ambos absorbibles. La ventana pasa de exigir 19,3 Mbps sostenidos a **≈58 Mbps**, porque el plazo de 90 minutos es fijo por contrato y el volumen crece con la operación.

**Qué implica para Célula 3.** El enlace de reposición es el componente a dimensionar con holgura, y la política de captura de imágenes es la palanca de mayor efecto. La detección debe ser anticipada por calendario: toda holgura instalada **antes del 15 de diciembre**, porque en enero ya no se puede intervenir.

### 6. `DEC-C4-21` — Qué vive en línea y qué en archivo

**Qué decidimos.** Movimientos y operación, 3 años en línea y años 4 a 10 en archivo; series de temperatura, 2 años granulares y años 3 a 5 agregados; evidencia facturable y masa bruta, 2 años en línea; imágenes, sus 12 meses completos; telemetría y eventos de seguridad, según los plazos que el caso ya fija. Archivo significa restauración dirigida en **no más de 24 horas**.

**Por qué no es arbitrario.** El caso ya fijó esta frontera dos veces —«2 años en línea» para telemetría, «12 + 24 meses» para eventos de seguridad— y trata **tres años** como la ventana operacionalmente relevante al obligar a migrar solo tres años de movimientos. Aplicamos el criterio que el caso ya usó.

**Qué implica para Célula 3.** Es lo que hace calculable la capacidad: **≈9,9 TB de dato y ≈18 TB a aprovisionar** en el escenario de diseño, de los cuales el borde necesita del orden de 1 TB útil.

---

## Materias de otras células que quedaron asumidas por Célula 4

Estas tres las asumimos porque nadie las tenía. Si la célula responsable prefiere incorporarlas a su propio entregable, se las traspasamos con gusto: están escritas y trazadas.

| Materia | De quién era | Qué hicimos |
|---|---|---|
| Gestión de calidad de datos conforme a ISO/IEC 25012 | cayó entre Célula 2 y el plan de calidad | La asumimos íntegra en el § 5.11 y **redactamos el requerimiento `RNF-CAL-01`** para que Célula 2 lo incorpore si quiere trazarlo en el T-12 |
| Catálogo de campos sujetos a cifrado de campo | `RNF-SEG-05` lo compromete pero no lo enumera | Lo derivamos del diccionario: 28 atributos |
| Almacenamiento de evidencia documental distinta de las imágenes | no está entre las 18 dimensiones del Cap. 14.2 | Lo estimamos con método declarado (≈223 GB al año) y lo marcamos como supuesto propio para levantamiento |

---

## Una corrección que hicimos sobre material de otras células

Al revisar los diagramas del modelo conceptual detectamos y corregimos cinco defectos de consistencia (versión 2.1). El más relevante para otras células: **`CONDUCTOR` y `PERSONA` duplicaban el documento de identidad**, ambos con marca de unicidad y cifrado de campo, mientras `PERSONA.tipo` ya incluía «conductor». Es duplicación de una entidad compartida, que `RT-05.09` prohíbe, y significaba cifrar, retener y eliminar el mismo dato personal dos veces con dos plazos que pueden divergir. Corregido: `CONDUCTOR` referencia a `PERSONA`.

Si esto afecta algo que Célula 2 o Célula 3 tengan escrito sobre identidad, conviene alinearlo.
