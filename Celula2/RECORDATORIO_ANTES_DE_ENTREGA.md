# Recordatorio antes de la entrega — Célula 2

**Fecha:** 2026-09-05. **Estado del material:** verificado y sin errores de contenido.
**Naturaleza de esta lista:** cuatro puntos abiertos. Los tres primeros son de forma —cifras y enumeraciones— y su corrección está resuelta aquí, lista para aplicar. El cuarto es de alcance: faltan productos que el `CP, Cap. 17.1` exige.

> Este archivo se escribió tras un audit completo de Célula 2 contra el texto de las tres bases. **No se aplicó ninguna corrección**: se dejan documentadas para decidirlas antes de la entrega. Lo que el audit verificó y quedó limpio está al final, para no repetir el trabajo.

---

## 1. El «Resultado ejecutivo» muestra cifras superadas

**Dónde.** `00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md`, sección **3. Resultado ejecutivo**, líneas 41 a 43.

| Fila | Dice | Estado vigente |
|---|---|---|
| RF vigentes | **138**, 30 + 49 + 59 | **139**, 30 + 49 + **60** |
| Distribución de primera entrega | **82 Etapa 1 + 56 Etapa 2** | **82 + 57** |
| RNF vigentes | **84** en 9 categorías | **91** en 9 categorías |

**Por qué está así.** El anexo del 2026-09-05 declara expresamente que *«no modifica las cifras del cuerpo del documento, que son el estado auditado al 04-09-2026»*, y trae al final la tabla «Conteos vigentes tras esta ronda» con los valores correctos. La decisión de no reescribir la historia fue correcta.

**Por qué conviene tocarlo igual.** «Resultado ejecutivo» es la sección que alguien abre para saber en qué estado está el trabajo. Quien lea de arriba hacia abajo se lleva 138 / 84 / 82+56 y no llega al anexo.

**Corrección propuesta, mínima.** Cambiar el encabezado a `## 3. Resultado ejecutivo — estado auditado al 04-09-2026` y agregar una línea bajo la tabla: *«Cifras vigentes tras la segunda y tercera ronda: 139 RF (82 + 57), 91 RNF, 11 reglas. Ver el anexo del 2026-09-05.»* No se altera ninguna cifra histórica.

**Lo que NO hay que tocar.** Las demás apariciones de «138» en ese archivo —líneas 87, 123 y 153— son narrativa histórica legítima («la base auditada de 134 creció a 138»). Son correctas como historia.

---

## 2. La lista de colisiones de códigos `RT` enumera cinco y hay al menos diez

**Dónde.** `01_Requerimientos/Catalogo rf definitivo parte1.md`, numeral **1.5**, y **Supuesto M** en `02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`.

**Qué enumera hoy.** `RT-05.10`, `RT-16.14`, `RT-16.21`, `RT-16.30` y, por el Supuesto M, `RT-21.06`.

**Qué falta.** Se compararon materia por materia los 27 códigos que el BTT y el Cap. 15 del CP comparten. Cinco más designan materias distintas:

| Código | Materia en el **BTT** | Materia en el **CP, Cap. 15** | Tipo |
|---|---|---|---|
| `RT-03.13` | declarar qué funciones **no** estarán disponibles en modo desconectado | sincronización tras la reconexión, ≤90 min | colisión |
| `RT-03.24` | calidad de servicio y priorización de tráfico *(Deseable)* | red de los sitios operacionales: rediseño del patio y radiopropagación | colisión — esa materia es `RT-03.23` en el BTT |
| `RT-06.01` | espacio de uso exclusivo, aislado, con acceso independiente | tipología del emplazamiento on-premise | colisión parcial: materias vecinas, no iguales |
| `RT-09.01` | presentar el **cálculo de capacidad** con sus supuestos | transacción operacional crítica: movimiento ≤1 s | colisión |
| `RT-15.02` | apagar o reducir los ambientes no productivos fuera de horario | **certificaciones sectoriales del adjudicatario**: ISPS, ley marco de ciberseguridad OIV, experiencia en TOS o mensajería marítima | colisión |

**Nota importante sobre `RT-15.02`.** La cita **ya es correcta**: `RNF-CUM-13` lo atribuye a «FEP03 Cap. 15, RT-15.02 — conocimiento ISPS/OIV y experiencia TOS o mensajería marítima». La regla de cita del numeral 1.5 está funcionando. Lo único que falta es que el código figure en la enumeración.

**Y los que sí coinciden**, que conviene anotar para no volver a revisarlos: `RT-02.12`, `RT-03.10`, `RT-05.23`, `RT-05.29`, `RT-09.02`, `RT-10.05`, `RT-11.10`, `RT-12.11`, `RT-12.12`, `RT-13.08`, `RT-16.09`, `RT-17.01`, `RT-17.06`, `RT-21.16` y `RT-22.04` son uso legítimo de «Según caso»: el BTT define la materia y el caso fija el valor. `RT-05.15` y `RT-13.12` quedan como materias vecinas, no idénticas.

**Corrección propuesta.** Ampliar el numeral 1.5 y el Supuesto M con estos cinco códigos y con la lista de los que sí coinciden.

---

## 3. Falta consolidar el mapeo de los «Según caso» respondidos bajo otro código

**El hallazgo.** El BTT tiene **21 requisitos «Según caso»**, y el inventario de Célula 2 los enumera los 21 correctamente. De esos, **seis no tienen entrada con su propio código en el Cap. 15 del caso** — pero los seis están respondidos, bajo un código vecino:

| Requisito del BTT | Materia | El caso lo responde en |
|---|---|---|
| `RT-03.23` | red inalámbrica de sitios operacionales, con cobertura verificada por estudio de sitio | `RT-03.24` «Red de los sitios operacionales» |
| `RT-16.10` | período de retención de la auditoría | `RT-05.10` «Retención de datos históricos y de auditoría» |
| `RT-16.17` | firma electrónica avanzada, Ley N° 19.799 | `RT-16.14` «Firma electrónica» |
| `RT-16.18` | sello de tiempo y conservación de la evidencia de firma | `RT-16.14` |
| `RT-16.31` | portal público con la información que el caso determine | `RT-16.30` «Portal público» |
| `RT-21.07` | horario mínimo del centro de atención | `RT-21.06` «Horario del centro de atención» |

**Célula 2 ya trata los seis**, cada uno en su lugar. `RF-INS-04` incluso lleva la nota explícita *«nótese que en el BTT el código RT-16.14 corresponde a otra materia (motor de reglas, Deseable); la obligación de firma proviene del CP»*. No hay vacío de contenido.

**Por qué conviene la tabla igual.** El **Formulario T-12** debe responder los 374 códigos **uno por uno** (BTT, numeral 1.5; checklist del Cap. C, entregable N° 24). Sin este mapeo, `RT-16.17`, `RT-16.18`, `RT-16.31`, `RT-21.07`, `RT-16.10` y `RT-03.23` van a parecer sin responder, porque el valor del caso está guardado bajo otro código. Esta tabla **es** la regla de construcción del T-12 que la narrativa da por resuelta: ya está derivada, solo falta escribirla donde el T-12 la use.

---

## 4. Lo que falta para cerrar Célula 2

El `CP, Cap. 17.1` exige **seis productos**. Cuatro están completos:

| Producto exigido | Estado |
|---|---|
| Catálogo de requerimientos funcionales | **completo** — 139 en 15 dominios |
| Catálogo de requerimientos no funcionales | **completo** — 91 en 9 categorías |
| Registro de supuestos | **completo** — 21 decisiones, 17 metas, 25 supuestos |
| Registro de reglas de negocio | **completo** — RN-01 a RN-11 |
| **Matriz de trazabilidad** | **pendiente** |
| **Registro de vacíos y consultas** | **pendiente** |

Más el **Formulario T-12**, exigido por el numeral 1.5 del BTT y por el entregable N° 24 del checklist.

### 4.1 Matriz de trazabilidad — pendiente con dependencia legítima

El `CP, Cap. 17.1` la define como *«correspondencia entre origen, requerimiento, componente de la arquitectura, paquete de la EDT, prueba de verificación y criterio de aceptación»*.

Dos de esas columnas —**componente de la arquitectura** y **paquete de la EDT**— no son de Célula 2. La primera depende de Célula 3, que ya tiene su catálogo lógico y sus nodos físicos identificados; la segunda del Subdocumento 7. La espera está justificada.

**Lo que sí se puede adelantar sin depender de nadie:** las columnas origen → requerimiento → prueba de verificación → criterio de aceptación están todas dentro de Célula 2. La matriz puede quedar armada con esas cuatro y las otras dos en blanco, para que Célula 3 solo rellene. Es mejor que entregarla vacía o no entregarla.

**Ojo con la matriz vieja.** `matriz_cobertura_rf_fase2(DESFASADA).md` está en `Historial/` y sus conteos ya fueron superados. **No es esta matriz** y no debe usarse como base.

### 4.2 Registro de vacíos y consultas — pendiente y sin dependencia de nadie

El `CP, Cap. 17.1` lo define como *«aquello que el PROPONENTE no puede resolver por sí solo y que someterá al CLIENTE durante el período de consultas»*.

**Este es el punto que más conviene mirar.** La narrativa lo registra como *«las consultas se enviaron; falta consolidar el registro formal»*. O sea, el trabajo de fondo está hecho —las 17 consultas se formularon— y lo que falta es el documento.

Y no está esperando a nadie:

- El período de consultas **cerró el 01-09-2026** (BA, Formulario T-20). Ya no se puede consultar más, así que el contenido del registro está congelado y es conocido.
- El Acta de Respuestas se publica el **07-09-2026**. Cuando salga, el registro se completa con qué respondió el CLIENTE a cada consulta y qué quedó sin resolver.
- El `Art. 5.4` de las BA advierte que, presentada la oferta, *«se entenderá que el PROPONENTE aceptó la interpretación más exigente y no podrá invocar la contradicción»*. El registro es la evidencia de qué se preguntó y qué quedó abierto.

**Insumos que ya existen y alimentan este registro**, para no partir de cero: el `Supuesto M` sobre las colisiones de códigos; las filas 11, 14 y 18 de la volumetría, que la propia plantilla declara enviadas a consulta —tamaño real de la base del TOS 2012, ubicación de las estaciones base y AHT de la mesa de ayuda—; `RF-PAT-07`, marcado en revisión; y los supuestos de la sección C del registro de supuestos que quedaron con «pendiente de validar».

### 4.3 Formulario T-12

La narrativa lo registra como *«pendiente — regla de construcción resuelta»*. El punto 3 de este recordatorio contiene la parte de esa regla que faltaba escribir: el mapeo de los seis «Según caso» respondidos bajo otro código. Con el inventario de 374 códigos ya clasificado y ese mapeo, el T-12 es trabajo de transcripción, no de análisis.

---

## Lo que el audit verificó y quedó limpio

Se deja constancia para no rehacerlo.

| Verificación | Resultado |
|---|---|
| Códigos `RT` citados en Célula 2 | **193 distintos, los 193 existen** en el BTT o en el Cap. 15 del CP. Ninguno inventado |
| Identificadores de RF | 139 en 15 dominios, **cero duplicados** |
| Identificadores de RNF | 91, cero duplicados, en **exactamente las nueve categorías** que nombra el BTT |
| RNF con umbral numérico y método de verificación | **91 de 91** |
| Referencias cruzadas colgantes | **ninguna**. `RF-OPD-03`, `RF-OPD-04` y `RF-PAT-14` aparecen solo como retiros documentados |
| Conteos declarados frente a reales | coinciden: 30 + 49 + 60 = 139 |
| Reglas de negocio | 11 definidas, 11 citadas, **los ocho temas obligatorios cubiertos** |
| Decisiones del `CP, num. 16.1` | las 20, más la 21ª de coordinación de inspecciones |
| Parámetros del `CP, Cap. 15` | los **27 tratados** |
| Requisitos «Según caso» del BTT | **21 enumerados**, coincide con el conteo independiente |
| Inventario de códigos `RT` | **374 de 374**; la suma por clase reconcilia: 74 + 107 + 192 + 1 |
| Criterios de aceptación del `CP, Cap. 18` | los 22 tratados; el criterio 19 tiene sección propia `D.1` que explica por qué no admite RF |
| Precios o montos | **ninguno propio**. El único monto es «US$ 620.000», que es la pérdida del 18 de febrero declarada por el caso, marcada «no se compromete meta» |

**Ninguno de los cuatro puntos abiertos es un error de contenido.** Los tres primeros son de legibilidad y de completitud de enumeración; el cuarto es de alcance.
