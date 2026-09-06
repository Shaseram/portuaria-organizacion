# A-08 — Almacenamiento acumulado por familia y horizonte de retención

**Caso:** 06 Portuaria — TERABYTE
**Subdocumento:** 5 — Modelo y gestión de datos
**Célula:** 4 (V. Guzmán / M. Reyes)
**Destino en el documento:** § 5.13, con el detalle en el Anexo D
**Destino externo:** frente de dimensionamiento de Célula 3 — cierra la entrega cruzada `E-01`
**Versión:** 1.0 · 6 de septiembre de 2026

---

## 0. Alcance

La volumetría vigente entrega el almacenamiento **anual** por familia. Eso no basta para dimensionar: `CP, Cap. 15, RT-05.10` fija plazos de retención de hasta diez años y `RNF-CUM-14` prohíbe el plazo uniforme, de modo que la capacidad que hay que aprovisionar es el **acumulado sobre el horizonte de cada clase**, no el volumen de un año.

Este documento convierte el volumen anual en capacidad acumulada y la reparte entre almacenamiento en línea y archivo recuperable. Es el insumo que el frente de dimensionamiento de Célula 3 necesita para convertirlo en cantidades físicas del Formulario T-11.

**Este documento no decide** cantidad de discos, nivel de RAID, tipo de medio, emplazamiento ni producto. Entrega la demanda de capacidad por familia, horizonte y modo de acceso; la conversión a cantidades es de Célula 3.

**Sobre las decisiones.** Cierra **una** decisión de Célula 4, porque sin ella la cifra de capacidad no es calculable. Todo lo demás queda como supuesto declarado o como pendiente con su célula.

---

## 1. Reglas de cálculo

Se declaran antes de los números, porque la mitad de los errores de dimensionamiento vienen de aquí.

| Regla | Contenido |
|---|---|
| **Unidades** | Decimales: 1 GB = 10⁹ bytes, 1 TB = 10¹² bytes. Es la unidad en que se contrata capacidad |
| **Sobrecarga ya incluida** | Las cifras anuales de la volumetría vigente **ya traen su factor**: ×3 en transaccional y series —índices, replicación y respaldo— y ×1,2 en imágenes. **No se vuelve a aplicar.** Es el error de doble conteo más común |
| **Sobrecarga que falta** | El factor ×1,2 de las imágenes cubre metadatos, **no copias**. La copia adicional de los objetos se calcula aparte y se declara en columna propia |
| **Horizonte** | El de la clase de retención de cada entidad, según `DEC-C4-03` y la tabla de `RT-05.10` |
| **Crecimiento** | Dos escenarios: el **actual**, con la volumetría de hoy, y el de **diseño**, con las tres veces la volumetría inicial que exige `BTT, Cap. 9, RT-09.03` |
| **Estacionalidad** | El factor estacional afecta el **caudal**, no el acumulado anual: un peak de cuatro meses y medio redistribuye el volumen dentro del año, no lo multiplica. Se aplica al dimensionar caudal e ingesta, no capacidad |

---

## 2. Base: qué compone el volumen anual declarado

### 2.1 Composición de la transacción anual

La volumetría define la transacción de negocio como la unión de cuatro tipos de evento. Descomponerla permite asignar cada fracción a su clase de retención:

| Componente | Eventos al año | Clase de retención |
|---|---:|---|
| Movimientos de grúa de muelle | 972.000 | 10 años |
| Movimientos de patio | 1.290.000 | 10 años |
| Eventos de gate, entrada y salida | 1.058.500 | 10 años |
| Documentos de facturación | 115.200 | 6 años |
| **Total** | **3.435.700** | — |

**El 96,6 % de las transacciones pertenece a la clase de diez años y solo el 3,4 % a la de seis.** Por eso el almacenamiento transaccional se dimensiona íntegro a diez años: la simplificación sobreestima en menos del 4 %, y sobreestimar capacidad es preferible a subestimarla.

### 2.2 Volumen anual por familia

| Familia | Volumen anual declarado | Qué incluye su factor | Base sin sobrecarga |
|---|---:|---|---:|
| Transaccional | 20 GB | ×3: índices, replicación y respaldo | ≈ 6,7 GB |
| Series de temperatura | 68 GB | ×3: índices, replicación y respaldo | ≈ 22,7 GB |
| Imágenes de reconocimiento | 1.400 GB | ×1,2: metadatos. **Sin copias** | ≈ 1.167 GB |
| Evidencia documental | **estimación propia, sección 2.3** | — | — |
| Histórico retenido del TOS | 480 GB, una sola vez | orden de magnitud no verificado | — |

### 2.3 La dimensión que la volumetría no cubre

La volumetría de Célula 2 cubre las dieciocho dimensiones que exige `CP, Cap. 14.2`, y ninguna de ellas es el almacenamiento de **documentos y evidencia distintos de las imágenes de reconocimiento**: actas de inspección firmadas, documentos de transporte, evidencia de los cuatro actos con firma electrónica y mensajería de integración. No es un olvido de Célula 2 —el capítulo no la pide— pero sí es un vacío para dimensionar, porque `RT-05.10` obliga a retener esa evidencia seis años.

Se estima con método declarado, marcado como **supuesto propio de Célula 4**:

| Componente | Método | GB al año |
|---|---|---:|
| Actas de inspección | 18.400 inspecciones al año × 1 MB por acta firmada con anexos | 18,4 |
| Documentos de transporte | 486.000 visitas × 1 documento × 200 KB | 97,2 |
| Evidencia de actos con firma | 486.000 visitas × 4 actos × 50 KB | 97,2 |
| Mensajería de integración | ≈ 2.000.000 de mensajes al año × 5 KB | 10,0 |
| **Total** | | **≈ 223** |

**Por qué la incertidumbre de esta cifra no cambia ninguna decisión:** aun en su cota alta representa el **16 % del volumen de imágenes**. Ni la elección de familia de A-05, ni el cuello de botella de `DEC-C4-20`, ni el reparto entre borde y nube dependen de que este número sea exacto. Se declara, se usa y se marca para levantamiento.

---

## 3. `DEC-C4-21` — Frontera entre almacenamiento en línea y archivo recuperable

> **Por qué esta decisión es necesaria.** Sin ella la capacidad no es calculable: hay que elegir entre dimensionar diez años de todo en línea —que multiplica por tres la capacidad y su costo— o inventar una frontera. `RT-05.07` obliga además a declarar la política de **archivado**, no solo la de retención.

**Decisión.** El almacenamiento se reparte en dos modos, con esta frontera por clase:

| Clase de información | Plazo total | **En línea** | **Archivo recuperable** |
|---|---|---|---|
| Movimientos y operación | 10 años | **3 años** | años 4 a 10 |
| Series de temperatura reefer | 5 años | **2 años en resolución granular** | años 3 a 5, agregados |
| Evidencia de hechos facturables | 6 años | **2 años** | años 3 a 6 |
| Verificación de masa bruta | 5 años | **2 años** | años 3 a 5 |
| Imágenes de reconocimiento | 12 meses | **12 meses**, todo su plazo | no aplica |
| Registros de acceso de personas | 5 años | **2 años** | años 3 a 5 |
| Telemetría de equipos | 2 años en línea | **2 años**, fijado por el caso | agregación posterior |
| Eventos de seguridad | 12 + 24 meses | **12 meses**, fijado por el caso | 24 meses |
| Histórico retenido del TOS | según clase | — | todo |

**Fundamento — el caso ya fijó la frontera dos veces, y aquí se extiende el mismo criterio:**

1. `CP, Cap. 15, RT-05.10` declara para la telemetría de equipos «**2 años en línea**, con política de agregación declarada para el resto». Es la única clase donde el caso separa explícitamente los dos modos, y el plazo que usa es dos años.
2. `BTT, Cap. 11, RT-11.14` hace lo mismo con los eventos de seguridad: doce meses en línea y veinticuatro en archivo recuperable.
3. **Los tres años de la operación no son una elección nuestra**: `CP, Cap. 15, RT-05.15` obliga a migrar **tres años** de movimientos y deja los años 4 a 10 en repositorio consultable. El propio caso trata tres años como la ventana operacionalmente relevante y siete años como consultables. La frontera de esta decisión es la misma que el caso ya aplicó a la migración.

**Compromiso de recuperación asociado.** En línea significa consulta directa; archivo significa **restauración dirigida ≤ 24 horas**, salvo la evidencia dentro de su plazo, que mantiene el umbral de ≤ 30 segundos de `CAL-38` mientras está en línea. Sin plazo declarado, «archivo recuperable» no es verificable.

**Consecuencia que se asume.** Una objeción de facturación sobre un hecho de más de dos años exigirá restauración desde archivo. Es aceptable: las objeciones se presentan dentro del ciclo comercial, y la ventana en línea de dos años lo cubre con holgura frente al 4,7 % de facturas objetadas de la línea base.

**Vinculación.** `RT-05.07` · `CP, Cap. 15, RT-05.10` y `RT-05.15` · `BTT, Cap. 11, RT-11.14` · `RNF-CUM-14` · `DEC-C4-02`, `DEC-C4-03` · `CAL-38`.

**¿Pendiente de validar?** Sí, con el CLIENTE al aprobar la política de retención. No bloquea el dimensionamiento.

---

## 4. Capacidad acumulada

### 4.1 Escenario actual

| Modo | Concepto | Capacidad |
|---|---|---:|
| En línea | Transaccional, 3 años | 60 GB |
| En línea | Series granulares, 2 años | 136 GB |
| En línea | Series agregadas, años 3 a 5 | 68 GB |
| En línea | Imágenes de reconocimiento, 12 meses | 1.400 GB |
| En línea | Evidencia documental, 2 años | 446 GB |
| | **Subtotal en línea** | **2.110 GB ≈ 2,1 TB** |
| Archivo | Transaccional, años 4 a 10 | 140 GB |
| Archivo | Evidencia documental, años 3 a 6 | 892 GB |
| Archivo | Histórico retenido del TOS | 480 GB |
| | **Subtotal archivo** | **1.512 GB ≈ 1,5 TB** |
| | **Total de dato** | **3.622 GB ≈ 3,6 TB** |
| | **Capacidad a aprovisionar**, con copia adicional de objetos | **≈ 6,4 TB** |

### 4.2 Escenario de diseño, tres veces la volumetría inicial

| Modo | Concepto | Capacidad |
|---|---|---:|
| En línea | Transaccional, 3 años | 180 GB |
| En línea | Series granulares, 2 años | 408 GB |
| En línea | Series agregadas, años 3 a 5 | 204 GB |
| En línea | Imágenes de reconocimiento, 12 meses | 4.200 GB |
| En línea | Evidencia documental, 2 años | 1.338 GB |
| | **Subtotal en línea** | **6.330 GB ≈ 6,3 TB** |
| Archivo | Transaccional, años 4 a 10 | 420 GB |
| Archivo | Evidencia documental, años 3 a 6 | 2.676 GB |
| Archivo | Histórico retenido del TOS | 480 GB |
| | **Subtotal archivo** | **3.576 GB ≈ 3,6 TB** |
| | **Total de dato** | **9.906 GB ≈ 9,9 TB** |
| | **Capacidad a aprovisionar**, con copia adicional de objetos | **≈ 18,1 TB** |

### 4.3 Cómo leer estas cifras

**El orden de magnitud es el hallazgo.** La solución completa, con diez años de retención y crecida al triple, se dimensiona en **decenas de terabytes, no en centenas**. Esto tiene una consecuencia directa sobre la arquitectura física: la capacidad no es el factor que decide el emplazamiento ni el costo dominante de infraestructura. Lo que decide es la latencia de un segundo, la autonomía de 72 horas y la ventana de sincronización — que es exactamente lo que `DEC-C4-20` identificó como cuello de botella.

**El almacenamiento transaccional es despreciable frente al resto.** 60 GB en línea en el escenario actual, 180 GB en el de diseño. El motor que sostiene las 78 entidades del modelo y todas las invariantes cabe holgadamente en el nodo del borde, lo que refuerza la recomendación de A-05 de situar el primario allí.

**Las imágenes son dos tercios de todo.** 1,4 de 2,1 TB en línea hoy; 4,2 de 6,3 TB en diseño. Son también el componente dominante de la ventana de sincronización. Es el mismo dato visto dos veces, y por eso la política de captura de imágenes —`PEN-18`— es la palanca de mayor efecto de todo el subdocumento.

---

## 5. Reparto entre borde y nube

Sujeto a la decisión de emplazamiento de Célula 3 (`PEN-07b`). Se entrega la demanda con su justificación funcional para que esa decisión tenga insumo.

| Familia | Borde | Nube | Fundamento |
|---|---|---|---|
| Transaccional en línea, 3 años | **completo** | réplica | `DEC` de A-05: el primario vive en el borde por la restricción no negociable N.º 4 |
| Transaccional en archivo, años 4 a 10 | — | completo | No es función crítica de las 72 h |
| Series granulares, 2 años | **completo** | réplica | La evaluación de desviación ocurre en el borde `(DES-06)` |
| Series agregadas, años 3 a 5 | — | completo | Consulta de evidencia, no de operación |
| Imágenes, 12 meses | **buffer de 72 h y ventana operativa** | repositorio completo | El buffer sostiene la desconexión; el repositorio vive donde la capacidad es elástica |
| Evidencia documental en línea | **buffer de 72 h** | repositorio completo | Igual criterio |
| Archivo y histórico retenido | — | completo | Por definición |

**Capacidad mínima del borde, escenario de diseño:** 180 GB de transaccional + 408 GB de series granulares + el buffer de 72 horas de objetos ≈ 39 GB, más holgura de operación. **Del orden de 1 TB útil**, no de decenas. Es una cifra que cambia el tipo de nodo que hay que especificar, y por eso se entrega antes de que Célula 3 lo especifique.

---

## 6. Buffer de la operación desconectada

| Concepto | Actual | Diseño 3× |
|---|---:|---:|
| Volumen generado en 72 horas | 13 GB | 39 GB |
| Del cual, imágenes | 11,2 GB (86 %) | 33,6 GB |
| Transferencia sostenida para sincronizar en 90 min | 19,3 Mbps | **57,8 Mbps** |

El buffer debe dimensionarse con holgura sobre el escenario de diseño **y** con el factor estacional aplicado al caudal, porque una desconexión de 72 horas en enero genera más volumen que una en agosto: camiones ×1,79 y volumen refrigerado mensual ×2,48. Es la única parte de este documento donde la estacionalidad afecta capacidad y no solo caudal, porque el buffer se dimensiona para el peor caso, no para el promedio.

---

## 7. Supuestos propios declarados

| ID | Supuesto | Efecto si es falso |
|---|---|---|
| `SUP-A08-01` | La evidencia documental distinta de las imágenes es del orden de 223 GB al año, con la composición de la sección 2.3 | Cambia la capacidad en línea en menos de un 25 %; no cambia ninguna decisión de arquitectura |
| `SUP-A08-02` | La agregación de series a partir del año 3 reduce el volumen a un tercio | Cambia 68 GB en el escenario actual; efecto marginal |
| `SUP-A08-03` | Los objetos —imágenes y evidencia documental— requieren una copia adicional para satisfacer el respaldo 3-2-1-1-0 de `RNF-DIS-14`, que el factor ×1,2 de la volumetría no incluye | Si el esquema de copias es distinto, la capacidad a aprovisionar cambia proporcionalmente. Es el supuesto con más efecto sobre la cifra final |
| `SUP-A08-04` | El histórico retenido del TOS son ≈ 480 GB | La cifra es de Célula 2 y está declarada como orden de magnitud no verificado (`PEN-12`) |
| `SUP-A08-05` | El almacenamiento transaccional se dimensiona íntegro a diez años, aunque el 3,4 % pertenezca a la clase de seis | Sobreestima en menos del 4 % |

---

## 8. Pendientes, con su célula

| ID | Qué falta | Responsable |
|---|---|---|
| `PEN-07b` | Emplazamiento de cada almacén: qué queda en el borde, qué en nube y qué en ambos | **Célula 3** (`ADR-005`) |
| `PEN-08` | Revalidación de la volumetría anual con el factor estacional, que es la base de todo este cálculo | **Célula 3** (`C4`) |
| `PEN-12` | Tamaño real del histórico del sistema de 2012 | **CLIENTE** |
| `PEN-18` | Política de captura de imágenes: es la palanca de mayor efecto sobre estas cifras | **Célula 3 y Célula 4**, conjunta |
| `PEN-19` | **Nuevo.** Esquema de copias que satisface el respaldo 3-2-1-1-0 sobre el almacenamiento de objetos: cuántas copias, dónde y con qué inmutabilidad | **Célula 3** (`ADR-007`, `C3`) |
| `PEN-20` | **Nuevo.** Volumen real de evidencia documental distinta de las imágenes, para reemplazar `SUP-A08-01` | **Levantamiento con el CLIENTE**, meses 1 a 4 |

---

## 9. Lo que esta entrega cierra hacia Célula 3

Con este documento queda cumplida la entrega cruzada `E-01`. El frente de dimensionamiento recibe:

1. capacidad acumulada por familia y horizonte, en dos escenarios;
2. la frontera en línea/archivo con su fundamento normativo;
3. la demanda de capacidad del borde separada de la de la nube;
4. el buffer de 72 horas y la transferencia de reposición implicada;
5. los cinco supuestos propios que sostienen las cifras, para que puedan revalidarse uno a uno sin rehacer el cálculo.

Sigue pendiente de nuestra parte la entrega `E-02` —necesidad de persistencia por familia—, que ya está en A-05, y `E-03` —atributos que son clave de acceso indexada—, que ya está en A-07. **Las tres entregas cruzadas hacia Célula 3 quedan cerradas.**

---

## 10. Trazabilidad

| Exigencia | Fuente | Dónde se cumple |
|---|---|---|
| Volumen anual de almacenamiento transaccional, de series y de imágenes | `CP, Cap. 14.2`, dimensiones 8, 9 y 10 | sección 2.2 |
| Volumen total del histórico a migrar | `CP, Cap. 14.2`, dimensión 11 | sección 2.2 y `SUP-A08-04` |
| Volumen generado en 72 horas sin enlace | `CP, Cap. 14.2`, dimensión 15 | sección 6 |
| Retención diferenciada por clase, sin plazo uniforme | `CP, Cap. 15, RT-05.10`; `RNF-CUM-14` | `DEC-C4-21` |
| Política de archivado declarada | `BTT, Cap. 5, RT-05.07` | `DEC-C4-21` |
| Soportar tres veces la volumetría inicial sin rediseño | `BTT, Cap. 9, RT-09.03` | sección 4.2 |
| Cálculo de capacidad con supuestos declarados | `BTT, Cap. 9, RT-09.01` | secciones 1, 4 y 7 |
| Respaldo 3-2-1-1-0 | `RNF-DIS-14` | `SUP-A08-03` y `PEN-19` |
| Valor, método de estimación y supuestos por dimensión | `CP, Cap. 14.2`, instrucción de dimensionamiento | todo el documento |

---

**Cierre.** El acumulado de la solución completa, a diez años y crecida al triple, es de **≈ 9,9 TB de dato y ≈ 18 TB de capacidad a aprovisionar**: decenas de terabytes, no centenas. El transaccional que sostiene las 78 entidades y las veinte invariantes son 180 GB en línea. Las imágenes son dos tercios del total y también el componente dominante de la ventana de sincronización, lo que convierte su política de captura en la palanca de mayor efecto del subdocumento. Una decisión de Célula 4, cinco supuestos propios declarados y seis pendientes trazados.
