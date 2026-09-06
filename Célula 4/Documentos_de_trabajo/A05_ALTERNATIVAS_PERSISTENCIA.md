# A-05 — Comparación de alternativas de persistencia por familia de datos

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Destino en el documento:** § 5.4, con la matriz completa en el Anexo C
**Versión:** 1.0 · 6 de septiembre de 2026
**Modelo de origen:** diagramas v2.1 y diccionario A-02 (80 entidades, 451 atributos)

---

## 0. Qué decide y qué no decide este documento

`BTT, Cap. 5, RT-05.02` obliga a justificar la selección del paradigma y del motor de persistencia —relacional o no relacional—, las garantías transaccionales y la posición entre consistencia y disponibilidad, **para cada dominio de datos** y no para la solución en bloque. Es la segunda viñeta del Formulario T-7 y la de mayor peso argumental del Subdocumento 5.

**Este documento decide:** la clasificación de las entidades del modelo en familias de persistencia, los criterios de evaluación con su ponderación, la comparación de al menos dos alternativas reales por familia y **la recomendación de paradigma y perfil de capacidades** de cada una.

**Este documento no decide:** producto comercial, versión, emplazamiento, capacidad por nodo ni topología de réplica. Esas decisiones pertenecen a la arquitectura física de Célula 3 —`ADR-005` de emplazamiento y `ADR-007` de almacenamiento— y hoy están en estado candidato.

La secuencia no es arbitraria: la guía de coordinación es explícita en que **Datos entrega primero la necesidad y la preferencia, y Arquitectura no debe escoger motores sin este análisis**. La regla de aprobación de decisiones de arquitectura de Célula 3 dice lo mismo desde el otro lado: *nombrar un producto sin comparar el problema que resuelve no es una decisión arquitectónica suficiente*.

Los productos que aparecen en la columna «referencia» de cada familia son eso: **referencias justificadas que acreditan que la alternativa existe y es realizable**, no una selección. Se declaran para que la comparación sea real y no un ejercicio abstracto, y quedan sujetas a `PEN-07`.

---

## 1. Por qué el modelo no cabe en un solo motor, y por qué tampoco en cinco

### 1.1 La forma del modelo

Las 80 entidades del diccionario se reparten así:

| Forma | Entidades | Cuáles |
|---|---:|---|
| Relacional: identidad, relaciones y transacciones sobre pocos registros | **78** | todo el modelo salvo las dos siguientes |
| Serie temporal: escritura por anexado, consulta por rango, sin actualización | **2** | `MUESTRA_TEMPERATURA`, `CONSUMO_EQUIPO` |
| Con objeto binario o documento asociado que **no** vive en la base | 6 (metadato en las 78) | `LECTURA_OPTICA`, `EVIDENCIA`, `ACTA_INSPECCION`, `DOCUMENTO_TRANSPORTE`, `ORDEN_EMBARQUE`, `INSTRUCCION_EMBARQUE` |

### 1.2 La forma del volumen

Las mismas entidades, medidas por almacenamiento anual con las cifras de la volumetría vigente:

| Familia | Volumen anual | Proporción |
|---|---:|---:|
| Transaccional | ≈ 20 GB | **1,3 %** |
| Series de temperatura refrigerada | ≈ 68 GB | 4,6 % |
| Imágenes de reconocimiento | ≈ 1,4 TB | **94,1 %** |

### 1.3 La conclusión que se sigue de las dos tablas

**El 97,5 % de las entidades del modelo genera el 1,3 % del almacenamiento anual, y el 2,5 % restante genera el 98,7 %.** Es la asimetría que gobierna toda esta sección, y tiene dos consecuencias opuestas que hay que sostener a la vez:

- **Contra el motor único.** Meter 1,4 TB anuales de imágenes y 226 millones de muestras al año en el mismo almacén que sostiene transacciones de un segundo degradaría la operación, y el caso ya advierte que la telemetría puede superar en órdenes de magnitud a las transacciones `(CP, Cap. 14.2)`. Además, `RT-05.05` prohíbe que la carga analítica degrade la operación.
- **Contra el zoológico de motores.** Las 78 entidades relacionales son un único grafo de integridad referencial: la visita, su posición, sus movimientos, sus hechos facturables y su evidencia se consultan juntos y se corrigen juntos. Repartirlas entre motores por dominio obligaría a resolver en la aplicación una integridad que el motor resuelve solo, y multiplicaría por diez la superficie que **cinco personas** de tecnologías de información tienen que operar `(CP, Cap. 10, restricción no negociable N.º 11)`.

**Cinco familias, no diez dominios.** La partición se hace por *forma de la carga*, no por dominio de negocio. Es también lo que la lista de decisiones que no deben tomarse silenciosamente pide de forma expresa: no escoger una única base para todos los datos por simplicidad, y no crear un almacén por cada requerimiento.

---

## 2. Criterios de evaluación y su ponderación

La ponderación es **decisión propia de Terabyte** y se declara como tal. Cada peso se justifica con la restricción del caso que lo origina; no hay criterios genéricos de industria.

| ID | Criterio | Peso | Por qué ese peso |
|---|---|---:|---|
| `C1` | **Garantías transaccionales e integridad** | 20 % | `RT-05.02` lo exige explícitamente y la invariante `INV-01` —ningún contenedor con dos escritores autoritativos— no es implementable sin transacciones sobre el grafo relacional |
| `C2` | **Autonomía de 72 horas y sincronización** | 20 % | Restricción no negociable N.º 4 y `CP, Cap. 15, RT-03.10`. Es la exigencia que descarta cualquier familia crítica dependiente de la nube para registrar |
| `C3` | **Operabilidad con cinco personas** | 15 % | Restricción no negociable N.º 11. Toda función que exija un especialista dedicado que la compañía no tiene debe ofrecerse como servicio y estar costeada: cada motor adicional es un costo operacional permanente, no una decisión técnica gratuita |
| `C4` | **Ajuste al perfil de carga** | 15 % | El perfil es asimétrico y está medido: 0,23 transacciones por segundo frente a ≈36 eventos por segundo de telemetría en el borde |
| `C5` | **Retención y costo de almacenamiento a diez años** | 10 % | `RT-05.10` fija plazos de hasta diez años y `RNF-CUM-14` prohíbe el plazo uniforme: el motor debe permitir políticas de ciclo de vida por clase |
| `C6` | **Reversibilidad y bloqueo por proveedor** | 10 % | `RT-03.07` obliga a declarar la estrategia de reversibilidad, y `RT-05.06` exige que el CLIENTE pueda exportar todo en formatos abiertos **sin intervención del adjudicatario** |
| `C7` | **Cifrado de campo, auditoría e inalterabilidad** | 10 % | `RT-11.10` sobre 28 atributos del catálogo de `DEC-C4-12`, y `RT-16.07` sobre el registro de auditoría |

Los pesos suman 100 %. `C1` y `C2` concentran el 40 % porque son las dos condiciones cuyo incumplimiento invalida la propuesta completa, no solo la elección de motor.

**Escala de evaluación:** 1 (no cumple), 3 (cumple con desarrollo propio significativo), 5 (cumple de forma nativa).

---

## 3. Familia 1 — Estado operacional

**Alcance:** 78 entidades, ≈ 20 GB anuales, ≈ 0,23 transacciones por segundo en el peak de coincidencia.
**Necesidad dominante:** transaccionalidad ACID, integridad referencial y consistencia fuerte sobre un grafo de entidades muy relacionadas.

### 3.1 Alternativas comparadas

| | **A1 · Relacional gestionado en nube, con réplica local de solo lectura** | **A2 · Relacional operado en el borde, con réplica hacia la nube** | **A3 · Documental no relacional** |
|---|---|---|---|
| Descripción | El motor primario vive en la nube; el borde conserva una copia de lectura y una cola de escritura | El motor primario vive en la sala del terminal; la nube recibe la réplica para analítica y respaldo | Agregados por documento, sin integridad referencial declarativa |
| Referencia que acredita la alternativa | servicio relacional administrado de nube pública | motor relacional de código abierto operado sobre el nodo local | motor documental de código abierto |

### 3.2 Evaluación ponderada

| Criterio | Peso | A1 | A2 | A3 | Fundamento de la nota |
|---|---:|:---:|:---:|:---:|---|
| `C1` Transaccionalidad e integridad | 20 % | 5 | 5 | **1** | El grafo `VISITA → MOVIMIENTO → POSICION_VIGENTE → HECHO_FACTURABLE → EVIDENCIA` tiene invariantes que cruzan cinco entidades; sin integridad declarativa hay que reimplementarlas en la aplicación y auditarlas una por una |
| `C2` Autonomía de 72 h | 20 % | **1** | 5 | 3 | A1 falla la condición dura: si el primario está en la nube, la pérdida del enlace detiene la escritura autoritativa del gate y del muelle, que la restricción N.º 4 prohíbe |
| `C3` Operabilidad con cinco personas | 15 % | 5 | 3 | 3 | `RT-03.05` obliga a privilegiar servicios administrados; operar el motor localmente exige respaldo, parcheo y monitoreo propios, que hay que costear como servicio |
| `C4` Ajuste al perfil de carga | 15 % | 5 | 5 | 3 | 0,23 transacciones por segundo no es una carga exigente para ningún relacional; la ventaja de escritura de A3 no se aprovecha |
| `C5` Retención a diez años | 10 % | 5 | 3 | 3 | El particionamiento por tiempo y las políticas de ciclo de vida son maduras en relacional gestionado |
| `C6` Reversibilidad | 10 % | 3 | 5 | 3 | El motor de código abierto operado localmente exporta a formato abierto sin depender del proveedor, que es lo que `RT-05.06` exige |
| `C7` Cifrado y auditoría | 10 % | 5 | 3 | 3 | El cifrado de campo y el encadenado de auditoría se resuelven en ambos, con más trabajo propio en el operado localmente |
| **Total ponderado** | | **4,00** | **4,30** | **2,60** | |

### 3.3 Recomendación

**Motor relacional, con el primario del estado operacional en el borde y réplica hacia la nube.** La diferencia entre A1 y A2 es estrecha en el total, pero **no se decide por el total**: `C2` es una condición de admisibilidad, no un criterio ponderable. Una propuesta que sitúe el primario en la nube incumple la restricción no negociable N.º 4 y se evalúa como falta de comprensión del caso, por bien que puntúe en el resto.

A3 se descarta con fundamento y no por preferencia: el modelo tiene 78 entidades con integridad referencial declarada y veinte invariantes que cruzan entidades. Un paradigma documental obligaría a implementar en la aplicación lo que el motor resuelve solo, y a demostrar en pruebas lo que en el relacional se demuestra con el esquema.

**Consecuencia que se asume:** A2 puntúa peor en operabilidad. La mitigación es explícita y costeada, como exige la restricción N.º 11: la operación del motor local se ofrece **como servicio gestionado por el adjudicatario**, no como tarea del equipo de cinco personas del CLIENTE.

**Lo que Célula 3 debe cerrar:** producto y versión, topología de réplica, nivel de RAID del almacenamiento local `(RT-03.14)` y dimensionamiento del nodo. Ver `PEN-07`.

---

## 4. Familia 2 — Series temporales

**Alcance:** 2 entidades, ≈ 68 GB anuales de temperatura más el consumo de equipos, ≈ 36 eventos por segundo en el borde y ≈ 7,2 reportados al núcleo.
**Necesidad dominante:** alta tasa de anexado, consulta por rango temporal, retención diferenciada con agregación, y **cero actualización** — una muestra no se corrige, se marca.

### 4.1 Alternativas comparadas

| | **B1 · Extensión de series temporales sobre el mismo motor relacional** | **B2 · Motor de series temporales dedicado** |
|---|---|---|
| Descripción | Las series viven en el mismo motor de la Familia 1, en tablas particionadas por tiempo con compresión y agregación continua | Motor separado, especializado en ingesta y consulta por rango |
| Referencia | extensión de series temporales para el motor relacional escogido | motor de series temporales de código abierto |

### 4.2 Evaluación ponderada

| Criterio | Peso | B1 | B2 | Fundamento |
|---|---:|:---:|:---:|---|
| `C1` Transaccionalidad | 20 % | 5 | 3 | La muestra debe poder unirse con `CONEXION_REEFER` y con `VISITA` para producir la evidencia de cadena de frío; en B1 es una unión dentro del mismo motor, en B2 es una integración |
| `C2` Autonomía de 72 h | 20 % | 5 | 5 | Ambos operan en el borde |
| `C3` Operabilidad | 15 % | **5** | **1** | Es el criterio que decide: B2 agrega un motor más al inventario que operan cinco personas |
| `C4` Ajuste al perfil | 15 % | 3 | 5 | B2 es superior en ingesta pura; con ≈36 eventos por segundo, la ventaja no es determinante |
| `C5` Retención a diez años | 10 % | 5 | 5 | Ambos ofrecen políticas de retención y agregación por antigüedad, que es lo que `DEC-C4-02` necesita |
| `C6` Reversibilidad | 10 % | 5 | 3 | La serie exportable en formato abierto es directa en B1 |
| `C7` Cifrado y auditoría | 10 % | 5 | 3 | Un único perímetro de control en vez de dos |
| **Total ponderado** | | **4,70** | **3,60** | |

### 4.3 Recomendación

**Extensión de series temporales sobre el mismo motor relacional.** La decisión se sostiene en tres hechos del caso, no en preferencia:

1. **El volumen no justifica un motor propio.** ≈36 eventos por segundo en el borde es una carga que una extensión temporal absorbe sin dificultad. Los motores dedicados se justifican en órdenes de magnitud superiores.
2. **La evidencia de cadena de frío es una unión.** `RNF-CUM-08` exige la serie continua **por contenedor** durante cinco años. Con B2, cada recuperación de evidencia cruza dos motores; con B1 es una consulta.
3. **Cada motor adicional se paga en operación.** Restricción N.º 11.

**Consecuencia que se asume y cómo se mitiga:** si el volumen crece más de lo proyectado, la extensión temporal puede quedarse corta. La mitigación está en el propio diseño y no en un cambio de motor: la **agregación en el borde**, que ya es parte de la Decisión N.º 8 de Célula 2 —muestreo local de 1 a 5 minutos, reporte al núcleo de 5 a 15—, es el primer mecanismo de crecimiento. El primer cuello de botella declarado en el § 5.10 es la ventana de escritura de las series, y la palanca es la resolución reportada, no el producto.

**Lo que Célula 3 debe cerrar:** si el nodo del borde soporta la ingesta local completa o si parte se resuelve en el concentrador de patio; y la capacidad del almacenamiento local para los 340 GB acumulados a cinco años.

---

## 5. Familia 3 — Documentos, imágenes y evidencia

**Alcance:** el objeto binario de 6 entidades; ≈ 1,4 TB anuales, **el 94 % del almacenamiento**.
**Necesidad dominante:** escritura una vez y lectura muchas, inmutabilidad demostrable, metadatos consultables y política de ciclo de vida por clase.

### 5.1 Alternativas comparadas

| | **C1 · Almacenamiento de objetos con índice en el relacional** | **C2 · Gestor documental** | **C3 · Objeto binario dentro de la base relacional** |
|---|---|---|---|
| Descripción | El binario vive en almacenamiento de objetos; el metadato y el sello viven en la Familia 1 | Producto documental con su propio repositorio, versionado y búsqueda | El binario se guarda como campo binario en la propia base transaccional |
| Referencia | almacenamiento de objetos compatible con la interfaz estándar del sector, en nube y en el borde | gestor documental de código abierto | — |

### 5.2 Evaluación ponderada

| Criterio | Peso | C1 | C2 | C3 | Fundamento |
|---|---:|:---:|:---:|:---:|---|
| `C1` Transaccionalidad | 20 % | 5 | 3 | 5 | El sello de integridad y el puntero viven en la transacción; el binario no necesita transaccionalidad propia |
| `C2` Autonomía de 72 h | 20 % | 5 | 3 | 3 | El almacenamiento de objetos se despliega también en el borde, lo que permite retener las imágenes del gate durante la desconexión |
| `C3` Operabilidad | 15 % | 5 | 1 | 5 | Un gestor documental es un producto más que operar y no aporta capacidad que el caso pida |
| `C4` Ajuste al perfil | 15 % | 5 | 3 | **1** | C3 inflaría la base transaccional de 20 GB a más de 1,4 TB anuales, degradando respaldo, restauración y replicación de la Familia 1 |
| `C5` Retención a diez años | 10 % | 5 | 3 | 1 | Las políticas de ciclo de vida por clase y el almacenamiento inmutable son nativos del almacenamiento de objetos: es lo que `RT-05.10` necesita para las imágenes de 12 meses |
| `C6` Reversibilidad | 10 % | 5 | 1 | 3 | El objeto en formato original con metadato exportable es lo más cercano a `RT-05.06` |
| `C7` Cifrado y auditoría | 10 % | 5 | 3 | 3 | Cifrado en reposo, retención inmutable y registro de acceso por objeto |
| **Total ponderado** | | **5,00** | **2,50** | **3,20** | |

### 5.3 Recomendación

**Almacenamiento de objetos con índice y sello en el relacional.** Es la única alternativa que puntúa al máximo en los siete criterios, y la razón es estructural: separa el 94 % del volumen del 100 % de la integridad. La base transaccional se mantiene en el orden de decenas de gigabytes, que es lo que hace viables el respaldo, la restauración y la réplica de la Familia 1 dentro de los objetivos de recuperación de `RNF-DIS-13`.

C3 se descarta por una consecuencia concreta y medible: multiplicaría por setenta el tamaño de la base transaccional, y con ello el tiempo de restauración que sostiene el objetivo de recuperación de cuatro horas.

**Lo que Célula 3 debe cerrar:** si el almacenamiento de objetos del borde y el de la nube son el mismo producto; el mecanismo de inmutabilidad y su relación con la eliminación a los 12 meses de las imágenes; y el cifrado y la gestión de llaves `(ADR-009)`.

---

## 6. Familia 4 — Analítica y explotación

**Alcance:** no tiene entidades propias. Es la proyección de las Familias 1 y 2 para los ocho productos de explotación del § 5.6.
**Necesidad dominante:** lectura agregada sin degradar la operación, con latencias comprometidas por indicador y profundización hasta la transacción de origen.

### 6.1 Alternativas comparadas

| | **D1 · Réplica de solo lectura del relacional, con modelo semántico encima** | **D2 · Almacén analítico separado, con carga desde eventos** |
|---|---|---|
| Descripción | Una réplica del motor operacional recibe las consultas analíticas; el modelo semántico se define sobre ella | Almacén orientado a columnas, alimentado por el flujo de eventos, con su propio modelo dimensional |
| Referencia | réplica de lectura del motor relacional escogido | almacén analítico columnar, gestionado o de código abierto |

### 6.2 Evaluación ponderada

| Criterio | Peso | D1 | D2 | Fundamento |
|---|---:|:---:|:---:|---|
| `C1` Transaccionalidad | 20 % | 5 | 3 | La profundización hasta la transacción de origen que exige `RT-05.26` es directa en D1 |
| `C2` Autonomía de 72 h | 20 % | 5 | 3 | La analítica **no** es función crítica de las 72 h: puede esperar. D1 degrada mejor porque la réplica local sigue sirviendo consultas |
| `C3` Operabilidad | 15 % | 5 | 3 | D1 no agrega producto; D2 sí |
| `C4` Ajuste al perfil | 15 % | 3 | **5** | D2 es superior para agregaciones sobre las series y para el histórico largo |
| `C5` Retención | 10 % | 3 | 5 | El almacén columnar comprime mejor el histórico de indicadores |
| `C6` Reversibilidad | 10 % | 5 | 3 | El modelo semántico documentado y la exportación abierta que exige `RT-05.27` son más simples sobre el mismo motor |
| `C7` Cifrado y auditoría | 10 % | 5 | 3 | Un solo perímetro |
| **Total ponderado** | | **4,50** | **3,50** | |

### 6.3 Recomendación

**Réplica de solo lectura con modelo semántico documentado, y la puerta abierta al almacén separado cuando el volumen lo justifique.** Es una recomendación con condición de revisión declarada, no una elección definitiva:

- **Ahora:** la réplica cumple `RT-05.05` —ninguna consulta analítica toca el primario—, sostiene las latencias del § 5.6 y no agrega producto que operar.
- **Disparador de revisión:** cuando la consolidación de indicadores del concedente deje de completarse dentro de la hora posterior al cierre de turno `(RT-05.29)`, o cuando el histórico de series supere lo que la réplica agrega en ventana. Ese disparador se mide con `IND-07` e `IND-11` del tablero de calidad, de modo que la revisión se dispara con dato y no con impresión.

**Lo que Célula 3 debe cerrar:** si la réplica analítica va en nube o en el borde, y si el flujo hacia ella es réplica nativa, captura de cambios o eventos. De eso depende la latencia real, no la comprometida. Ver `PEN-06`.

---

## 7. Familia 5 — Histórico retenido no migrado

**Alcance:** los siete años de movimientos que se retienen y no se migran, más los remanentes de los otros cinco universos. Estimado en el orden de los 480 GB, cifra declarada como orden de magnitud no verificado.
**Necesidad dominante:** consulta de baja frecuencia, formato abierto, legibilidad sin intervención del adjudicatario y **cero dependencia del sistema de origen**.

### 7.1 Alternativas comparadas

| | **E1 · Repositorio consultable en formato abierto sobre almacenamiento de objetos** | **E2 · Motor de archivo dedicado** | **E3 · Conservar encendido el sistema de 2012 como archivo** |
|---|---|---|---|
| Descripción | Extracción a formato columnar abierto sobre almacenamiento de objetos, con catálogo e interfaz de consulta | Producto de archivo con su propio motor y su propia interfaz | No se extrae: el sistema de origen queda encendido en solo lectura |

### 7.2 Evaluación

| Criterio | Peso | E1 | E2 | E3 | Fundamento |
|---|---:|:---:|:---:|:---:|---|
| `C1` Transaccionalidad | 20 % | 5 | 5 | 3 | El histórico es inmutable: no necesita transacciones |
| `C2` Autonomía de 72 h | 20 % | 5 | 5 | 3 | No es función crítica |
| `C3` Operabilidad | 15 % | 5 | 1 | 1 | E3 obliga a mantener un sistema sin soporte; E2 agrega producto |
| `C4` Ajuste al perfil | 15 % | 5 | 5 | 3 | Consulta esporádica |
| `C5` Retención a diez años | 10 % | 5 | 5 | 3 | E3 depende de que el sistema siga arrancando dentro de nueve años |
| `C6` Reversibilidad | 10 % | 5 | 3 | **1** | Decisivo: en E3 el histórico solo es legible desde un producto de 2012 cuyo modelo de datos **nadie documentó** |
| `C7` Cifrado y auditoría | 10 % | 5 | 3 | **1** | Un sistema sin soporte, accesible, en un operador de importancia vital |
| **Total ponderado** | | **5,00** | **4,00** | **2,30** | |

### 7.3 Recomendación

**Repositorio consultable en formato abierto.** Coincide con lo ya resuelto por Célula 2 y este análisis lo confirma con criterios explícitos. E3 no se descarta por puntaje sino por incumplimiento directo de dos obligaciones: `RT-05.06`, porque el CLIENTE no podría ejercer por sí mismo su derecho de exportación sobre un modelo de datos no documentado; y la política de sistemas sin soporte en un operador de importancia vital.

---

## 8. Resumen: familia, paradigma y capacidades exigidas

| Familia | Paradigma recomendado | Capacidades que Célula 3 debe materializar | Total ponderado de la opción elegida |
|---|---|---|---:|
| Estado operacional | **Relacional**, primario en el borde con réplica a la nube | ACID; integridad referencial declarativa; particionamiento por tiempo; cifrado de campo; réplica con RPO ≤ 15 min; operación ofrecida como servicio | 4,30 |
| Series temporales | **Relacional con extensión temporal** | anexado de alta tasa; compresión; agregación continua; políticas de retención por antigüedad; unión nativa con el estado operacional | 4,70 |
| Documentos y evidencia | **Almacenamiento de objetos** con índice y sello en el relacional | escritura una vez; inmutabilidad demostrable; ciclo de vida por clase; despliegue en borde y nube; cifrado en reposo | 5,00 |
| Analítica | **Réplica de solo lectura** con modelo semántico documentado | aislamiento del primario; latencia por indicador; profundización hasta la transacción; autoservicio y exportación abierta | 4,50 |
| Histórico retenido | **Repositorio abierto** sobre almacenamiento de objetos | formato columnar abierto documentado; catálogo; consulta sin intervención del adjudicatario | 5,00 |

**Dos motores, no cinco.** La recomendación consolida las Familias 1, 2 y 4 sobre un mismo motor relacional —una instancia primaria, una extensión temporal y una réplica de lectura— y las Familias 3 y 5 sobre almacenamiento de objetos. Es la configuración que satisface las obligaciones de `RT-05.02` y `RT-05.05` con la menor superficie operacional posible, que es lo que la restricción no negociable N.º 11 exige tratar como criterio de diseño y no como detalle de implantación.

---

## 9. Reversibilidad y bloqueo por proveedor

`RT-03.07` obliga a declarar qué componentes son portables, cuáles no lo son y cuál sería el esfuerzo estimado de una migración. `RT-05.06` va más lejos: el CLIENTE debe poder exportar **la totalidad** de su información en formatos abiertos, en cualquier momento, sin costo adicional y **sin intervención del adjudicatario**.

| Componente | Portabilidad | Riesgo de bloqueo | Mitigación declarada |
|---|---|---|---|
| Motor relacional | Alta si es de código abierto; el esquema y los datos se exportan en formato estándar | Bajo | Evitar extensiones propietarias en el esquema del núcleo; toda extensión usada se declara |
| Extensión de series temporales | Media: las tablas siguen siendo relacionales; se pierde la compresión y la agregación continua | Medio | La serie se exporta como tabla plana; la agregación se recalcula |
| Almacenamiento de objetos | Alta si se usa la interfaz estándar del sector | Bajo | No usar funciones específicas de un proveedor en la ruta de escritura |
| Réplica analítica y modelo semántico | Media: el modelo semántico es específico de la herramienta | Medio | El modelo se documenta como especificación, no solo como configuración `(RT-05.27)` |
| Servicios gestionados de nube | Baja por definición | **Alto** | Es la razón por la que el primario operacional no vive en un servicio gestionado; y por la que `RT-03.07` exige declarar el esfuerzo de migración componente a componente |

**Prueba de reversibilidad que se compromete:** exportación completa de un dominio de datos en formato abierto y documentado, ejecutada **por el CLIENTE** sin asistencia del adjudicatario. Sin esa prueba, `RT-05.06` es una declaración y no un compromiso verificable.

---

## 10. Lo que queda abierto, y a quién le corresponde

| ID | Qué falta | Responsable | Qué queda condicionado |
|---|---|---|---|
| `PEN-07` | Producto, versión y política de vigencia por familia; y si el Informe 1 nombra productos o solo capacidades | Célula 3 (`ADR-007`) | La columna «referencia» de las secciones 3 a 7 |
| `PEN-07b` | Emplazamiento de cada almacén: borde, nube o ambos | Célula 3 (`ADR-005`, Decisión N.º 20 abierta) | La recomendación de la Familia 1 **exige** primario en el borde; el resto es ajustable |
| `PEN-02` | Mecanismo de cifrado de campo y su efecto sobre la indexación de ocho atributos | Célula 3 (`ADR-009`) | La nota de `C7` en la Familia 1 |
| `PEN-06` | Si el flujo hacia la analítica es réplica nativa, captura de cambios o eventos | Célula 3 (`ADR-003`) | La latencia real de la Familia 4 |
| `PEN-08` | Revalidación de la volumetría con el factor estacional | Célula 3 (`C4`) | Las proporciones de la sección 1.2 y el disparador de revisión de la Familia 4 |
| `PEN-12` | Tamaño real del histórico del sistema de 2012 | CLIENTE | El dimensionamiento de la Familia 5 |
| Propio | La ponderación de la sección 2 es decisión de Terabyte y se declara como tal; no proviene de las Bases | Célula 4, declarado | Toda la evaluación |

---

## 11. Trazabilidad

| Exigencia | Fuente | Dónde se cumple |
|---|---|---|
| Justificar paradigma y motor, relacional o no relacional, por dominio de datos | `BTT, Cap. 5, RT-05.02` | secciones 3 a 8 |
| Selección del motor con justificación | `BA, Form. T-7`, Subdoc. 5, segunda viñeta | sección 8 |
| Al menos dos alternativas reales por familia | regla de aprobación de decisiones de arquitectura | tres alternativas en las Familias 1, 3 y 5; dos en las Familias 2 y 4 |
| Separación del almacenamiento transaccional y analítico | `BTT, Cap. 5, RT-05.05` | Familia 4 |
| Privilegiar servicios administrados y justificar la excepción | `BTT, Cap. 3, RT-03.05` | `C3` en la Familia 1; la excepción del primario local se justifica y se costea |
| Estrategia de reversibilidad y bloqueo por proveedor | `BTT, Cap. 3, RT-03.07` | sección 9 |
| Exportación total en formatos abiertos sin intervención del adjudicatario | `BTT, Cap. 5, RT-05.06` | sección 9 y Familia 5 |
| Operación autónoma de 72 horas | `CP, Cap. 15, RT-03.10`; restricción N.º 4 | `C2`, criterio de admisibilidad |
| Área de tecnologías de información de cinco personas | `CP, Cap. 10`, restricción N.º 11 | `C3` y la conclusión de la sección 8 |

---

**Cierre.** Cinco familias, trece alternativas comparadas con siete criterios ponderados, cinco recomendaciones por capacidad y ningún producto seleccionado. La configuración resultante son **dos motores y no cinco**, con la excepción a los servicios administrados justificada y costeada donde el caso obliga a hacerlo. La ponderación es decisión declarada de Terabyte; el emplazamiento, el producto y la capacidad siguen siendo de Célula 3, y este documento es el insumo que esa decisión necesitaba para no tomarse a ciegas.
