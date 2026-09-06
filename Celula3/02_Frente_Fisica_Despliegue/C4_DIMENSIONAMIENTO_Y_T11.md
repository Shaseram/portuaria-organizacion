# C4 — Dimensionamiento y T-11

**Actualización de entrada:** Célula 2 `c4756df`. La estacionalidad, la derivación de la sincronización y los `RNF-DES-09` a `12` se revalidan en §2 y se corrigen en §4; ver `TRZ-C4-009`, `010`, `011` y `029`. Los supuestos por dimensión se revalidan antes de dimensionar: no son cálculos aprobados de Célula 2. *(Nota heredada del commit `8307e1c` de `main`, con las referencias de traza actualizadas a la numeración vigente de `TRZ_C4`.)*

## Contrato del entregable

### Objetivo y destino

Transformar la volumetría en capacidades y cantidades justificadas, y consolidar el T-11. Alimenta la sección 4.2.11 y los formularios de `90_Consolidado/`.

### Cumplimientos asignados

- `SD4-02`, `SD4-06`, `SD4-08`.
- T7-4.6; T21 4.2; Formulario T-11.
- BTT Cap. 8 completo (`RT-08.01` a `RT-08.19`) y `RT-09.01`/`RT-09.02`; pruebas a 1,5× peak.
- Checklist del BTT, Cap. C, entregable N° 11: cálculo de capacidad y dimensionamiento, exigido en `RT-09.01`.

> *Corrección `F2-COR-004` (2026-09-05): el contrato citaba `RT-09.02` pero no `RT-09.01`, que es el requisito que exige presentar el propio cálculo de capacidad con sus supuestos de usuarios concurrentes, TPS, volumen y crecimiento. Del Capítulo 8 se citaban seis de diecinueve; quedaban sin anclar `.02` tolerancia declarada a falla de discos, `.06` equipamiento nuevo con garantía desde la recepción conforme, `.07`–`.09` estaciones de trabajo con NCh 2527 y gestión centralizada, `.12` grado de protección declarado, `.13` ciclo de vida, repuestos y **plan de reposición durante los 56 meses del Contrato**, `.16`–`.18` ciclo de vida, borrado seguro con certificado de sanitización y disposición final con gestor autorizado. Ojo: `RT-09.01` colisiona con el Cap. 15 del caso, que usa el mismo código para el umbral de la transacción crítica; ver `F2-ESC-006`.*

### Entradas obligatorias

- Maestro §§2.1, 4, 7, 9–10 y 15–16.
- Volumetría completa de Célula 2.
- A1 componentes, A2 flujos/volúmenes, C1/C2/C3 nodos y D1 candidatos de seguridad.

### Trabajo requerido

- [ ] Revalidar las 18 dimensiones heredadas sin borrar sus supuestos.
- [ ] Declarar fórmulas, unidades, fuentes y calidad de dato.
- [ ] Dimensionar régimen normal y peak coincidente de dos naves+gate.
- [ ] Dimensionar ingesta local/central, almacenamiento, red, usuarios y crecimiento.
- [ ] Dimensionar buffer para 72 h y sincronización ≤90 min.
- [ ] Añadir replicación, respaldo, índices, logs, SO y holgura sin doble conteo.
- [ ] Declarar margen de crecimiento y procedimiento de ampliación.
- [ ] Identificar primer cuello de botella y sensibilidad.
- [ ] Convertir resultados a cantidades físicas verificables.
- [ ] Dimensionar el ancho de banda por sitio en régimen normal y peak, con el cálculo que lo justifica (`RT-03.20`).
- [ ] Declarar el margen de crecimiento como porcentaje sobre la carga proyectada y el procedimiento de ampliación (`RT-08.05`).
- [ ] Incorporar al T-11 la reposición del equipamiento de terreno durante los 56 meses del Contrato (`RT-08.13`).
- [ ] Consolidar candidatos T-11 de los tres frentes.
- [ ] Revisar 1:1 físico→cálculo→T-11 y ausencia de precios.

### Hoja de cálculo narrativa obligatoria

| ID DIM | Variable | Actual | Horizonte | Peak | Fórmula/método | Supuestos | Fuente | Sensibilidad | Resultado de capacidad | Estado |
|---|---|---:|---:|---:|---|---|---|---|---|---|
| `DIM-01` | TPS negocio | 0,11 | 0,13 | 0,23/0,27 | ver C2 | revisar | Volumetría C2 | POR HACER | POR HACER | PENDIENTE |

### Conversión a cantidad obligatoria

| ID físico | Demanda base | Factor peak | HA/DR | Retención | Holgura | Capacidad por unidad | Cantidad calculada | Redondeo/razón | Fila T-11 |
|---|---:|---:|---:|---:|---:|---:|---:|---|---|
| POR COMPLETAR | — | — | — | — | — | — | — | — | — |

### Reglas T-11

- Una fila final contiene exactamente: Componente; Producto/servicio; Ubicación/lugar; Cantidad; Justificación.
- La tabla de trabajo puede tener trazas adicionales; la final no.
- No hay fila por cada módulo lógico, solo por componente físico/plataforma/licencia/hardware ofertado.
- Cada fila debe mapear al diagrama físico, cálculo, seguridad y fuente.
- No incluir precios ni información que permita inferirlos.
- Si una cantidad depende de site survey, usar cantidad/rango justificable y declarar el mecanismo de cierre; no inventar ubicación exacta.

### Productos obligatorios

1. Dimensionamiento reproducible.
2. Tabla de sensibilidad y holgura.
3. Matriz de cantidades.
4. `90_Consolidado/01_T11_TRABAJO_TRAZABLE.md` completo.
5. Propuesta de `02_FORMULARIO_T11_FINAL.md`.

### Salidas hacia otros frentes

- Frente 2: retroalimentación si un producto no soporta la demanda.
- Frente 3: datos para auditoría y control de seguridad/licencias.

### Definición de terminado

- [ ] Cálculos reproducibles y unidades coherentes.
- [ ] Supuestos propios diferenciados de hechos del CLIENTE.
- [ ] Se dimensionan normal, peak, crecimiento, 72 h, HA y DR.
- [ ] Primer cuello de botella y ampliación declarados.
- [ ] Cada cantidad llega al T-11 y cada fila vuelve a un cálculo.
- [ ] No hay precios.
- [ ] `TRZ_C4.md` completo.

## Contenido listo para integrar

**Versión:** `v0.5` — contenido completo, sujeto a revisión cruzada en la Puerta 2.
**Fecha:** 2026-09-05. **Destino:** consolidado 4.2.11 y el Formulario T-11.

### 1. Método, convenciones y qué exige este entregable

`RT-09.01` del BTT —materia «cálculo de capacidad», que **no** es la misma que el `RT-09.01` del Cap. 15 del caso, ver `F2-ESC-006`— obliga a presentar *«el cálculo de capacidad que sustenta su dimensionamiento, con los supuestos de usuarios concurrentes, transacciones por segundo, volumen de datos y crecimiento anual, tomados de la volumetría del caso»*. Es el entregable N° 11 del checklist del Capítulo C.

**Convenciones.** Año de operación continua 24×7×365 = 31.536.000 s. Los volúmenes se expresan en unidades decimales, que es la convención que usa la volumetría heredada: 1 GB = 10⁹ B. Cada cifra lleva su origen: `[caso]` viene del `CP, Cap. 14.1`; `[derivado]` se calcula de esos valores; `[supuesto]` es nuestro y se declara como tal. La regla del Maestro es que un dato pendiente se diseña con rango, mecanismo o fallback, **nunca se completa inventándolo**.

**Qué hace este paquete con la volumetría heredada.** No la reemplaza: la revalida. La plantilla de Célula 2 completó las 18 dimensiones del `CP, Cap. 14.2` con su método y sus supuestos declarados, y ese trabajo se conserva íntegro. Aquí se recalcula cada fila, se corrigen las que no cuadran, y se convierte el resultado en capacidad por nodo y en cantidad física.

### 2. Revalidación de las 18 dimensiones

Se recalculó cada fila desde los valores del `CP, Cap. 14.1` aplicando el método que la propia plantilla declara.

| ID | Dimensión | Valor heredado | Recálculo | Veredicto |
|---|---|---|---|---|
| `DIM-01` | TPS régimen normal | 0,11 → 0,13 | 3.435.700 ÷ 31.536.000 = **0,1089**; proyección 3.996.600 ÷ 31.536.000 = **0,1267** | **confirmado** |
| `DIM-02` | TPS peak de dos naves y gate saturado | 0,23 → 0,27 | muelle 0,050 + gate 0,117 + patio 0,066 = **0,233**; proyección 0,050 + 0,150 + 0,066 = **0,266** | **confirmado** |
| `DIM-03` | Telemetría de 2.400 tomas | 7,2 → 8,7 al núcleo; 35,8 → 43,3 local | 2.150 ÷ 300 = **7,17**; 2.600 ÷ 300 = **8,67**; local 2.150 ÷ 60 = **35,8** | **confirmado** |
| `DIM-04` | Frecuencia de muestreo justificada | 1–5 min local, 5–15 reporte | coherente con la Decisión N° 8 y con `RN-11` | **confirmado**; ver nota de `RF-REF-07` |
| `DIM-05` | Posicionamiento de equipos móviles | 37 → 44 ev/s | 74 ÷ 2 = **37**; 88 ÷ 2 = **44** | **confirmado**; la frecuencia de 2 s es supuesto propio, no de la Decisión N° 2 |
| `DIM-06` | Usuarias internas concurrentes | 160 → 175 | 640 × 25 % = **160**; 700 × 25 % = **175** | **confirmado**; el 25 % es supuesto |
| `DIM-07` | Usuarias externas concurrentes | 159 → 187 | 1.990 × 8 % = **159**; 2.335 × 8 % = **187** | **confirmado**; el 8 % es supuesto |
| `DIM-08` | Almacenamiento transaccional anual | 20 → 24 GB | 3.435.700 × 2 KB × 3 = **20,6 GB**; proyección **24,0 GB** | **confirmado** |
| `DIM-09` | Series temporales de carga refrigerada | 68 → 82 GB/año | 226.008.000 eventos × 100 B × 3 = **67,8 GB** | **confirmado** |
| `DIM-10` | Imágenes de reconocimiento | 1,4 → **1,6** TB/año | 2.375.000 × 500 KB × 1,2 = **1,43 TB**; proyección 2.778.000 × 500 KB × 1,2 = **1,67 TB** | **corregido**: la proyección es **1,7 TB**, no 1,6 |
| `DIM-11` | Histórico a migrar del TOS 2012 | ≈480 GB | estimación gruesa reconocida como tal; sobreestima deliberadamente | **se mantiene**, con el dato real solicitado al CLIENTE |
| `DIM-12` | Integraciones y volumen por integración | 21 + 7 familias | coherente con el Maestro §7 | **confirmado** |
| `DIM-13` | Ancho de banda de la red del patio | 375–500 kbps | **62 kbps** en régimen; **88 kbps** en peak estacional | **corregido**, ver §5 |
| `DIM-14` | Puntos de acceso inalámbrico | 6–8 estaciones; ubicación pendiente | cálculo geométrico razonable; **queda sujeto a site survey** | **se mantiene como rango** |
| `DIM-15` | Datos generados en 72 h sin enlace | ≈13 GB | **13,7 GB** a tasa promedio; **21,9 GB** a peak estacional | **corregido**, ver §4 |
| `DIM-16` | Sincronización tras 72 h | ≤90 min ⇒ 19,3 Mbps | **20,3 Mbps** con 13,7 GB; **32,5 Mbps** con 21,9 GB | **corregido**, ver §4 |
| `DIM-17` | Contactos mensuales a la mesa de ayuda | 458 → 527 | coherente con el universo declarado | **confirmado**; la tasa de 15 % es supuesto |
| `DIM-18` | Dotación de mesa de ayuda y operación | 2 diurnos + 1 de guardia | Erlang C con AHT supuesto de 8 min; intensidad ≈0,23 Erlang | **se mantiene**; el AHT real está solicitado al CLIENTE |

**Quince dimensiones se confirmaron, tres se corrigieron y ninguna se descartó.** Los supuestos propios de la plantilla —2 KB por registro, 100 B por evento, 500 KB por imagen, 25 % y 8 % de concurrencia, 2 s de posicionamiento, 15 % de tasa de contacto, AHT de 8 min— se conservan tal cual, con su marca de supuesto. Cambiarlos sin dato nuevo sería reemplazar un supuesto declarado por otro sin declarar.

### 3. La carga real de este sistema no son las transacciones

Es el hecho que más condiciona el dimensionamiento y el `CP, Cap. 14.2` lo advierte como primera particularidad del perfil de carga:

| Fuente | Eventos por segundo | Proporción |
|---|---:|---|
| Telemetría de tomas refrigeradas, muestreo local de 1 min | **35,8** | 49 % |
| Posicionamiento de 74 equipos móviles cada 2 s | **37,0** | 51 % |
| Transacciones de negocio en régimen normal | 0,11 | 0,15 % |
| Transacciones de negocio en el peak de coincidencia | 0,23 | 0,3 % |

**La telemetría supera a las transacciones de negocio por un factor del orden de 300.** El sistema se dimensiona por ingesta de eventos y por su persistencia, no por TPS. Dos consecuencias prácticas:

**El clúster local es de tres nodos por disponibilidad, no por carga.** Unos 73 eventos por segundo agregados no exigen tres servidores: los exige `RT-03.14`, que obliga a redundancia de los equipos críticos, y `RT-08.03`, que prohíbe el punto único de falla, más la necesidad de tolerar la caída de un nodo sin perder cuórum durante las 72 horas. `RT-15.01` obliga a declarar el **factor de utilización proyectado** y a evitar capacidad ociosa permanente: se declara que el factor de utilización de cómputo del núcleo local será bajo y que su dimensionamiento responde a disponibilidad y a autonomía, no a rendimiento. Es preferible declararlo a inflar la carga para justificar el equipo.

**El peak de coincidencia casi no mueve la aguja.** Pasar de 0,11 a 0,23 TPS es duplicar el 0,3 % de la carga. Lo que sí la mueve es el peak **estacional**, porque multiplica el flujo de camiones y con él las imágenes, que son el volumen dominante.

### 4. Los dos peaks, y la corrección del buffer de 72 horas

La plantilla de Célula 2 incorporó el factor estacional y advirtió, con razón, que *«el peak estacional… fija la carga sostenida durante cuatro meses y medio, y es el que determina el almacenamiento»*. Pero la fila 15 quedó calculada *«a tasa promedio durante toda la ventana»*, con la advertencia de que *«varía si la desconexión coincide con temporada peak»*.

**Esa advertencia hay que convertirla en el número, porque la coincidencia no es un caso extremo: es el caso esperable.** El peak estacional va del 15 de diciembre al 30 de abril, cuatro meses y medio, el 37 % del año, y es exactamente el período en que está prohibido intervenir. Dimensionar el buffer al promedio y descubrir en enero que falta capacidad significa esperar hasta mayo para ampliarlo.

| Componente del buffer de 72 h | A tasa promedio | A peak estacional | Factor |
|---|---:|---:|---|
| Transacciones de negocio | 0,06 GB | 0,10 GB | ×1,79 camiones |
| Telemetría local de reefer, 1 min | 0,93 GB | 0,93 GB | ya está en peak: 2.150 de 2.400 tomas |
| Posicionamiento de 74 equipos | 0,96 GB | 0,96 GB | sin variación estacional |
| **Imágenes de gate y patio** | **11,7 GB** | **19,9 GB** | ×1,79 sobre las de gate |
| **Total** | **13,7 GB** | **21,9 GB** | **×1,60** |

**El buffer se dimensiona a 21,9 GB, no a 13.** Y las imágenes son el 91 % de él, lo que hace del tamaño de imagen el supuesto más sensible de todo el modelo (§8).

**La sincronización se recalcula en consecuencia.** El umbral de ≤90 min proviene del `CP, Cap. 15, RT-03.13` y está comprometido en `RNF-DIS-04`:

| Escenario | Volumen | Ancho de banda sostenido necesario |
|---|---:|---:|
| Corte de 72 h en régimen normal | 13,7 GB | **20,3 Mbps** |
| Corte de 72 h en peak estacional | 21,9 GB | **32,5 Mbps** |

Y esa capacidad se necesita **además** del tráfico de la operación en curso, porque el terminal no se detiene mientras sincroniza. De ahí sale la conclusión de la sección siguiente.

### 5. Ancho de banda por sitio

`RT-03.20` obliga a dimensionar el ancho de banda **por sitio, en régimen normal y en peak, justificado con el cálculo de volumen**.

#### 5.1 Enlace del terminal hacia la nube

| Componente de subida | Régimen | Peak estacional |
|---|---:|---:|
| Imágenes de reconocimiento | 361 kbps | 616 kbps |
| Telemetría reportada al núcleo, 5 min | 5,8 kbps | 5,8 kbps |
| Transacciones de negocio | 1,7 kbps | 3,1 kbps |
| **Subtotal de operación** | **≈369 kbps** | **≈625 kbps** |
| **Reposición tras corte de 72 h, sostenida 90 min** | 20,3 Mbps | **32,5 Mbps** |

> **El enlace no se dimensiona por el régimen: se dimensiona por la reposición.** La operación normal cabe holgadamente en menos de 1 Mbps; el compromiso de sincronizar en 90 minutos exige del orden de **35 Mbps disponibles** —32,5 de reposición más la operación en curso y margen—. Es una diferencia de casi cincuenta veces, y es el número que hay que contrastar contra el enlace real.

> **Riesgo que se declara.** El `CP, Cap. 6` describe el respaldo como *«radioenlace de menor capacidad»*. Si el corte de 72 horas fue causado por la caída de la fibra y la reconexión ocurre estando aún sobre el radioenlace, **la sincronización en 90 minutos puede no ser alcanzable**. El compromiso de `RNF-DIS-04` se cumple sobre el enlace principal restablecido o sobre el segundo camino de `RT-03.17` dimensionado a esta cifra. La capacidad real de ambos enlaces es dato del CLIENTE y se solicita.

#### 5.2 Red operacional del patio — corrección de `DIM-13`

| Componente | Régimen | Peak estacional |
|---|---:|---:|
| Posicionamiento, 37 ev/s × 100 B | 29,6 kbps | 29,6 kbps |
| Imágenes de lectura óptica en patio, 20 % de los movimientos | 32,7 kbps | 58,5 kbps |
| **Total** | **≈62 kbps** | **≈88 kbps** |

La plantilla declaraba 375–500 kbps y advertía que era *«la fila con más incertidumbre acumulada de toda la tabla»*. Al recalcularla se ve el origen de la diferencia: el método prorratea **todas** las imágenes de reconocimiento sobre la red del patio, pero la mayor parte de esas imágenes son del **gate**, que tiene gabinete propio y no cursa por la red inalámbrica. Descontándolas, el tráfico real del patio es de decenas de kbps.

**Esto no reduce el problema de la red del patio: lo redefine.** La red del patio no está limitada por ancho de banda —cualquier tecnología candidata lo cubre con enorme margen—, está limitada por **cobertura y handover** con pilas de hasta cinco alturas cuya geometría cambia cada hora. En consecuencia, `ADR-006` debe decidirse por comportamiento de propagación, continuidad en el traspaso entre celdas, cantidad de puntos de instalación en ambiente salino y su reposición, y **no por rendimiento**. Ningún candidato se descarta por throughput.

Y tiene una consecuencia sobre las cantidades: `RT-15.01` y el numeral 6.1 del BTT penalizan sobredimensionar tanto como subdimensionar. Comprar estaciones base para 500 kbps cuando se necesitan 88 sería exactamente eso. El número de estaciones lo fija la **cobertura**, no el tráfico, y por eso sigue dependiendo del site survey (`F2-ESC-001`).


### 6. Capacidad por nodo

#### 6.1 Almacenamiento del núcleo local

Se dimensiona por lo que **debe** vivir en el terminal, no por lo que podría. Todo lo que no sostiene las cinco funciones críticas viaja a la nube.

| Concepto | Cálculo | Volumen |
|---|---|---:|
| Buffer de 72 h a peak estacional | §4 | 21,9 GB |
| Ventana caliente de series de reefer, 30 días a muestreo local de 1 min | 2.150 × 43.200 × 100 B × 3 | 27,9 GB |
| Réplica operacional de `DATA-CORE`, dos años | 2 × 20,6 GB | 41,2 GB |
| Registros locales, sistema operativo, imágenes de contenedor y trabajo | supuesto | ≈50 GB |
| **Subtotal útil** | | **≈141 GB** |
| **Con 30 % de holgura declarada** | `RT-08.05` | **≈183 GB útiles** |

**El almacenamiento local del terminal es del orden de 200 GB útiles, no de terabytes.** El volumen dominante del caso —1,43 TB anuales de imágenes— vive en la nube con retención de 12 meses, y la serie histórica de temperatura, con retención de 5 años, también. Esa cifra es un insumo directo de `ADR-005`: un recinto técnico dimensionado a este volumen es pequeño, lo que refuerza que la discusión de sala es de cumplimiento normativo y de rutas de comunicaciones, no de metros cuadrados de almacenamiento.

Sobre el arreglo se declara, conforme a `RT-03.14` y `RT-08.02`: paridad doble o espejo distribuido con tolerancia a la falla de al menos un disco, control de errores y monitoreo predictivo de salud. La justificación del nivel exacto frente a las alternativas se completa con el perfil de escritura, que es telemetría de escritura constante y lectura poco frecuente: un perfil que favorece el espejo distribuido sobre la paridad por el costo de reconstrucción, y así se llevará a `ADR-007`.

#### 6.2 Cómputo del núcleo local

| Dimensión | Valor | Origen |
|---|---:|---|
| Ingesta agregada de eventos | ≈73 ev/s en régimen y en peak estacional | `DIM-03` + `DIM-05` |
| Transacciones de negocio | 0,11 régimen / 0,23 peak de coincidencia | `DIM-01`, `DIM-02` |
| Usuarias internas concurrentes servidas localmente durante el corte | ≈160 | `DIM-06` |
| Nodos | **3, por disponibilidad y cuórum** | `RT-03.14`, `RT-08.03` |
| Prueba de aceptación | 1,5× del peak declarado | `BA, Art. 24`, `RNF-DES-12` |

#### 6.3 Nube

| Conjunto | Retención | Volumen en línea en régimen | A tres años |
|---|---|---:|---:|
| `DATA-CORE` transaccional | movimientos 10 años, evidencia facturable 6, accesos y VGM 5 | ≈206 GB acumulados a 10 años | ≈240 GB |
| `DATA-TS` series de temperatura | 5 años | ≈340 GB | ≈410 GB |
| `DATA-DOC` imágenes de reconocimiento | **12 meses** | ≈1,43 TB en estado estacionario | ≈1,67 TB |
| Registros de seguridad | 12 meses en línea + 24 en archivo | por dimensionar con D1 | — |
| Migración histórica del TOS 2012 | repositorio consultable | ≈480 GB, sobreestimado | — |
| **Total en línea, orden de magnitud** | | **≈2,5 TB** | **≈2,8 TB** |

La retención de 12 meses de las imágenes es la que impide que el conjunto crezca sin techo: sin ella, 1,43 TB anuales acumulados a diez años serían más de 14 TB. Es una decisión de las bases (`RT-05.10`), no nuestra, y conviene decirlo porque es lo que hace que el dimensionamiento sea estable.

### 7. Margen de crecimiento y procedimiento de ampliación

`RT-08.05` obliga a declarar el margen **como porcentaje sobre la carga proyectada del caso** y el procedimiento de ampliación.

La proyección a tres años del `CP, Cap. 14.1` implica crecimientos del 16 % en transacciones, 21 % en telemetría, 17 % en imágenes y 9 a 17 % en personas usuarias. **Se declara un margen del 30 % sobre la proyección a tres años**, que absorbe ese crecimiento y deja holgura para el error de los supuestos propios.

**Procedimiento de ampliación.** Cómputo y almacenamiento del núcleo local: incorporación de un nodo al clúster y de bandejas al arreglo, sin detención, aprovechando que la arquitectura es de tres nodos con cuórum. Nube: elasticidad del servicio gestionado, con umbrales y límites superiores declarados conforme a `RT-02.10`. Borde: incorporación de gabinetes y dispositivos por zona.

**La restricción de calendario que gobierna la ampliación**, y que la plantilla de Célula 2 ya había identificado: la restricción no negociable 9 prohíbe intervenir entre el 15 de diciembre y el 30 de abril, que es justamente el peak estacional. **Toda holgura de capacidad debe estar instalada y verificada antes del 15 de diciembre de cada año.** Una necesidad detectada en enero no se puede ejecutar hasta mayo. Por eso el margen del 30 % no es conservadurismo: es la única forma de atravesar cuatro meses y medio sin poder tocar nada.

El posible cuarto sitio de 2030–2032 queda fuera del horizonte de tres años, pero `RT-02.12` —«según caso»— exige que la solución admita replicarse a nuevas unidades **por parametrización y sin rediseño**. La capacidad se amplía por incorporación, no por rearquitectura.

### 8. Primer cuello de botella y sensibilidad

**Primer cuello de botella: la cobertura de la red del patio en peak estacional.** No por tráfico —§5.2 muestra que sobra ancho de banda— sino porque es el único componente cuyo desempeño depende de una geometría que cambia cada hora, cuya cantidad y ubicación no están fijadas, que se degrada precisamente cuando el patio está al 90 % de ocupación, y que **no se puede intervenir entre el 15 de diciembre y el 30 de abril**. Su mitigación de diseño ya está tomada: el terminal de equipo opera autónomo hasta 8 horas fuera de cobertura (`RNF-DIS-03`), de modo que una sombra no detiene la operación. Pero el cuello sigue siendo ese, y se cierra con el site survey.

**Segundo: el enlace externo durante la reposición.** 32,5 Mbps sostenidos durante 90 minutos, sobre un enlace cuyo respaldo el caso describe como *«de menor capacidad»* y sin prueba de conmutación desde 2022.

**Tercero: el almacenamiento de imágenes en nube**, que crece linealmente y solo está acotado por la retención de 12 meses.

#### Sensibilidad de los supuestos propios

| Supuesto | Valor | Qué gobierna | Si cambia |
|---|---|---|---|
| **500 KB por imagen** | propio | **91 % del buffer de 72 h** y el 100 % del almacenamiento documental | a 1 MB: buffer 40 GB, sincronización **58 Mbps**, nube 2,9 TB/año. **Es el supuesto más sensible del modelo** |
| 2 s de posicionamiento | propio, no fijado por la Decisión N° 2 | 51 % de la ingesta de eventos | a 1 s: 74 ev/s solo de posición, ingesta total 110 ev/s |
| 20 % de cobertura óptica en patio | propio | tráfico de la red del patio y parte del buffer | a 50 %: red del patio ≈130 kbps, sigue sobrando |
| 100 B por evento de telemetría | propio | series y ventana caliente | lineal, sin efecto de umbral |
| 2 KB por registro | propio | `DATA-CORE`, que es el conjunto más pequeño | efecto menor |
| 25 % y 8 % de concurrencia | propio | usuarias concurrentes | afecta al dimensionamiento de canales, no al núcleo |

**Consecuencia:** el tamaño de imagen es el único supuesto cuyo error cambia el diseño, no solo la cifra. Se solicita al CLIENTE el tamaño real que producen sus lectores actuales, y mientras tanto el buffer se dimensiona con el margen del 30 % que absorbe hasta ≈650 KB por imagen sin rehacer nada.

### 9. Conversión a cantidad

| ID físico | Demanda base | Factor peak | HA/DR | Retención | Holgura | Capacidad por unidad | Cantidad | Redondeo y razón | Fila T-11 |
|---|---|---|---|---|---|---|---|---|---|
| `PHY-OPS-01` núcleo local | 73 ev/s · 0,23 TPS · 160 usuarias | ×1,79 estacional | N+1 con cuórum | — | 30 % | servidor de rack empresarial | **3 nodos** | mínimo para cuórum; la carga no los exige, la disponibilidad sí | `T11-C2-01` |
| `PHY-OPS-02` almacenamiento local | 141 GB útiles | ya incluido | tolerancia ≥1 disco | ventana caliente 30 d | 30 % | arreglo con paridad doble o espejo | **≈183 GB útiles**, capacidad bruta según nivel escogido | se instala la capacidad mínima del formato disponible; el exceso es del formato, no del diseño | `T11-C2-02` |
| `PHY-OPS-04` red de núcleo | tráfico operacional del terminal | — | HA sin punto único | — | — | conmutador y cortafuegos | **par de cada uno** | `RT-08.03` | `T11-C2-03`, `04` |
| `PHY-EDG-01` gate | 14 puestos | 18 proyectados | gabinete por puesto | — | — | gabinete IP66 | **14 → 18** | uno por puesto, del `CP, Cap. 14.1` | `T11-C2-14` |
| `PHY-EDG-03` patio refrigerado | 26 tableros | 32 proyectados | — | — | — | concentrador por tablero | **26 → 32** | uno por tablero, del `CP, Cap. 14.1` | `T11-C2-16` |
| `PHY-EDG-02` patio | 62 kbps; cobertura de 18 ha | 88 kbps | redundancia de Decisión N° 9 | — | — | estación base | **6–8, rango** | **la cobertura manda, no el tráfico**; se cierra con site survey | `T11-C3-03` |
| Terminales de equipo | 74 equipos | 88 proyectados | — | — | 30 % | terminal robusto IP65 | **74 → 88**, más repuestos | uno por equipo instrumentado, del `CP, Cap. 14.1` | `T11-C2-15` |
| Enlace hacia la nube | 369 kbps operación | 625 kbps | segundo camino | — | reposición 32,5 Mbps | enlace | **≥35 Mbps disponibles**, dos caminos | lo fija la reposición, no el régimen | `T11-C3-01` |
| Puestos de operación | dotación de `DIM-18` | tres turnos | — | — | — | estación con monitores duales | **por confirmar con el modelo de operación**; `DIM-18` estima 2 diurnos + 1 de guardia | no se fija sin el AHT real | `T11-C2-13` |
| Nube | 2,5 TB en línea · 73 ev/s ingesta | ×1,79 | multi-AZ + región secundaria | por conjunto | 30 % | servicio gestionado | elástica, con umbrales y límites declarados | `RT-02.10` | `T11-C2-17`, `18` |

### 9.bis Candidatos T-11 de seguridad, consolidados desde `SEC-PHYS-v0.1`

D1 entregó 31 controles agrupados en 17 entradas y clasificó cada una. Su regla `F3-DEC-005` es explícita: *«C4 debe asignar ID T-11 solo cuando exista un producto, plataforma, licencia, servicio o hardware efectivamente ofertado. Capacidades nativas o incluidas se referencian desde la fila principal; no se duplican por cada control lógico.»* Se aplica literalmente. **De los 17 grupos, siete generan fila propia; el resto se referencia desde filas que ya existen.**

| Candidato | Grupo `SEC-PHYS` | Componente | Ubicación | Unidad de cantidad | Fuente del cálculo |
|---|---|---|---|---|---|
| `T11-SEC-01` | `SEC-EDGE-01/02` + `SEC-API-01` | servicio de borde y gateway gestionados | nube primaria | por volumen de tráfico y de peticiones | C4 §5.1: 369 kbps en régimen, 625 en peak estacional |
| `T11-SEC-02` | `SEC-IAM-01 / SEC-ADM-01` | plataforma de identidad y PAM | nube, con capacidad local en `PHY-OPS-01` | por identidades administradas y sesiones privilegiadas | `DIM-06` 160→175 internas; `DIM-07` 159→187 externas; **más 2.100→2.400 eventuales distintos al año**, que no son concurrentes pero sí identidades a administrar |
| `T11-SEC-03` | `SEC-KEY-01 / SEC-SECRET-01` | KMS o HSM y gestor de secretos, con material local protegido | nube y sala técnica | por ámbito de clave y capacidad local | requisito excluyente de `ADR-009`; no depende del volumen |
| `T11-SEC-04` | `SEC-LOG-01 / SEC-SIEM-01` | plataforma SIEM y de registro, con colector y buffer local | nube, con colector en `PHY-OPS-01` | **por ingesta diaria y retención** | ver §9.ter |
| `T11-SEC-05` | `SEC-END-01` | EDR: agentes y consola | nube, sala y puestos | por carga y por puesto administrado | 3 nodos locales + cargas en nube + puestos de `PHY-OPS-06`. **Excluye los dispositivos de terreno**, ver C2 §8.bis |
| `T11-SEC-06` | `SEC-SOC-01 / SEC-IR-01` | SOC gestionado 24×7 y gestión de incidentes | servicio | por cobertura y volumen de eventos | restricción no negociable 11: se oferta como servicio, no se asigna a TI=5 |
| `T11-SEC-07` | `SEC-VULN-01` + `SEC-PENTEST-01` | escaneo continuo y pentest independiente | servicio | por activos analizados y por ejercicio anual | `RT-11`: pentest anual y antes de cada paso a producción |

**Los diez grupos restantes no generan fila, y se declara desde dónde se cubren:**

| Grupo | Se cubre desde | Razón |
|---|---|---|
| `SEC-NET-01 / SEC-EXP-01` | `T11-C2-03` conmutación y `T11-C2-04` cortafuegos | la segmentación es una capacidad del equipo ya ofertado |
| `SEC-SYNC-01` | `T11-C3-01` enlace y el broker de `T11-C2-17` | es un conducto sobre infraestructura ya contada |
| `SEC-DATA-01 / SEC-ENC-01 / SEC-FIELD-01` | `T11-C2-17` servicios de datos en nube y `T11-C2-02` almacenamiento local | cifrado nativo del almacén |
| `SEC-BKP-01` | `T11-C2-12` custodia de medios y `T11-C2-18` región secundaria | es condición de esas filas, no una segunda compra |
| `SEC-SDLC-01 / SEC-PIPE-01` y `SEC-SUPPLY-01 / SEC-ART-01` | plataforma CI/CD de C3 §13 | una plataforma, no una fila por regla de control |
| `SEC-NPDATA-01` | proceso, no producto | fila solo si se oferta herramienta separada |
| `SEC-GOV-01 / SEC-CLOUD-01 / SEC-HARD-01 / SEC-SAMM-01` | implementación y servicios | `SEC-HARD-01` aterriza como línea base CIS por producto en C2 §8.bis |

### 9.ter Dimensionamiento del registro de seguridad

Es la única entrada de `SEC-PHYS-v0.1` cuya cantidad depende de un cálculo propio, y D1 la remite expresamente a C4. El volumen lo domina la telemetría, igual que todo lo demás en este caso.

| Fuente de eventos | Volumen | Origen |
|---|---|---|
| Telemetría local de reefer y posicionamiento | 73 ev/s | `DIM-03` + `DIM-05`; **no todos se registran como evento de seguridad**, solo los de acceso y error |
| Accesos de personas | 640→700 propios y hasta 380 eventuales por turno | `CP, Cap. 14.1`; retención de accesos **5 años**, Maestro §16.1 |
| Transacciones de negocio | 0,11 TPS en régimen | `DIM-01` |
| Registros de plataforma, red y borde | proporcional a nodos y a peticiones | C1 §4 |

**Retención exigida:** `RT-11` fija **12 meses en línea más 24 en archivo** para los registros de seguridad. Es la retención más larga en línea de todo el sistema después de los movimientos, y es la que dimensiona la plataforma.

**Buffer local:** el colector de `PHY-OPS-01` debe sostener los eventos de las **72 horas** de corte más margen, y reenviarlos al reconectar sin perderlos ni duplicarlos. Ese volumen se suma a los ≈183 GB útiles del §6.1: se incorpora dentro de los ≈50 GB declarados como «registros locales, sistema operativo y trabajo», y el margen del 30 % lo absorbe. **No hay que reabrir el dimensionamiento de almacenamiento local por esto.**

#### Estimación de la ingesta, con su método

`RT-09.01` obliga a presentar el cálculo de capacidad **con sus supuestos**, y la regla 4 del Maestro admite rango y mecanismo de levantamiento: lo que prohíbe es completar inventando. Se estima la parte derivable de la volumetría del `CP, Cap. 14.1` y se declara explícitamente qué queda fuera.

| Fuente de evento de seguridad | Eventos/día | Derivación |
|---|---:|---|
| Accesos de personas al recinto | ≈3.560 | (640 propios + 380 eventuales × 3 turnos) × 2 eventos de entrada y salida `[derivado]` |
| Autenticaciones internas | ≈1.920 | 640 con acceso a sistemas × 3 turnos `[supuesto]`: una autenticación por turno-persona |
| Autenticaciones externas | ≈500 | 25 % de los 1.990 usuarios externos en un día `[supuesto]` |
| Transacciones de negocio registradas | ≈9.410 | `DIM-01`: 3.435.700 al año ÷ 365 |
| Telemetría anómala | ≈6.310 | 0,1 % de los 73 ev/s `[supuesto]`: solo el error y la anomalía son evento de seguridad, no la lectura normal |
| **Subtotal derivable** | **≈21.700/día** | |

| Tamaño de registro `[supuesto]` | Ingesta | En un año | 12 meses en línea |
|---|---:|---:|---:|
| 0,5 KB | 11 MB/día | 4,0 GB | ≈4 GB |
| **1 KB, valor de trabajo** | **22 MB/día** | **7,9 GB** | **≈8 GB** |
| 2 KB | 43 MB/día | 15,8 GB | ≈16 GB |

**Buffer local durante el corte:** ≈0,07 GB en 72 horas a 1 KB por registro. Confirma lo dicho arriba: cabe holgadamente dentro de los ≈50 GB ya previstos en §6.1, y **no obliga a reabrir el almacenamiento local**.

**Qué queda fuera de esta estimación, y es lo que impide cerrar el valor total.** No están los registros de plataforma, de red y de borde —flujos del cortafuegos, peticiones del gateway, trazas de infraestructura—, que en un SIEM suelen ser el término dominante y pueden superar en uno o dos órdenes de magnitud a los eventos de aplicación. Su volumen depende de dos cosas que no son nuestras: la **política de qué se registra**, que es de D1, y la **clasificación campo→sensibilidad** que D1 mantiene abierta como `F3-DEP-004`, dependiente del Subdocumento 5 y del CLIENTE.

**Cómo se trata mientras tanto.** La cifra de ≈8 GB al año se declara como **piso derivable, no como total**, y la unidad de la fila `T11-SEC-04` es ingesta diaria y retención. Una vez exista la política de registro, el total es aritmética sobre esta misma tabla. Se registra como `F2-ESC-013`.

### 10. Matriz T-11 y control 1:1

Los candidatos de este frente están en C2 §9 y en la tabla de conversión de §9 de este entregable. **No se han escrito todavía en [`../../90_Consolidado/01_T11_TRABAJO_TRAZABLE.md`](../../90_Consolidado/01_T11_TRABAJO_TRAZABLE.md)**, y es deliberado: el README de Célula 3 establece que los archivos de `90_Consolidado/` *«reciben únicamente contenido aprobado para entrega»* y que los archivos globales los actualiza el integrador en las puertas de integración. Este material está en `v0.5`, no aprobado, y además el T-11 debe recibir también los candidatos de A1, A2, A3, D1 y D2. La consolidación se hace en la Puerta 2, con las doce columnas de trabajo, y de ahí pasan al formulario final solo las cinco oficiales. Al Formulario T-11 final pasan solo las cinco oficiales —Componente, Producto o servicio ofertado, Ubicación o lugar, Cantidad, Justificación— y solo las filas aprobadas.

**Control 1:1 exigido por la Puerta 2.** Cada fila de T-11 debe volver a un nodo del diagrama físico de C1, a un cálculo de este entregable y a una fuente. Y a la inversa: cada caja física ofertada debe tener fila, o una justificación explícita de por qué no la tiene.

| Verificación | Estado | Evidencia |
|---|---|---|
| toda fila de C2 y C3 tiene nodo `PHY-*` en C1 | **cumple** | §9 y tabla de emplazamiento de C1 §4 |
| toda cantidad tiene cálculo o criterio declarado | **cumple**, con seis cantidades en rango o pendientes de dato externo | §9 |
| cada nodo desplegable de C1 aparece en T-11 o tiene exclusión justificada | **cumple** | C2 §9 lista lo excluido y por qué |
| controles y licencias de seguridad considerados | **cumple** | §9.bis: los 17 grupos de `SEC-PHYS-v0.1` clasificados, 7 con fila propia y 10 con su origen declarado, conforme a `F3-DEC-005` |
| no existen precios | **cumple** | revisión de los cuatro paquetes |
| el formulario final conserva exactamente cinco columnas | **cumple** | plantilla de `90_Consolidado` |

Quedan **fuera del T-11 con justificación**: la obra civil de la sala, de cargo del CLIENTE con especificación nuestra (`RT-06.06`); los sistemas conservados; las canalizaciones exteriores; y el hardware de terreno cuya **adquisición** es del CLIENTE aunque su especificación sea nuestra (`BA, Art. 14.2`) — este último caso se declara explícitamente en la columna de justificación, porque aparece en el diagrama físico y podría parecer una omisión.

### 11. Lo que este entregable deja abierto

| ID | Dato faltante | Efecto | Estado |
|---|---|---|---|
| `F2-ESC-001` | site survey del patio | cantidad y ubicación de estaciones base quedan en rango 6–8 | BLOQUEADO EXTERNO |
| `F2-ESC-011` | tamaño real de imagen de los lectores actuales | es el supuesto más sensible: gobierna el 91 % del buffer y el ancho de banda de reposición | **nuevo** |
| `F2-ESC-012` | capacidad real de la fibra y del radioenlace | determina si los 90 min de sincronización son alcanzables sobre el respaldo | **nuevo** |
| `ESC-06` | tamaño real de la base del TOS 2012 | `DIM-11` sigue siendo una estimación gruesa sobreestimada | abierto en Célula 2 |
| — | AHT real de la mesa de ayuda | `DIM-18` y los puestos de operación no se cierran | solicitado por Célula 2 |

### 12. Definición de terminado — estado

- [x] Cálculos reproducibles, con unidades coherentes y fuente por cifra.
- [x] Supuestos propios diferenciados de hechos del CLIENTE, y conservados de la volumetría heredada.
- [x] Se dimensionan régimen normal, peak de coincidencia, **peak estacional**, crecimiento, 72 h, HA y DR.
- [x] Primer cuello de botella declarado y sensibilidad cuantificada.
- [x] Margen del 30 % y procedimiento de ampliación, con su restricción de calendario.
- [x] No hay precios.
- [ ] `TRZ_C4.md` completo — en curso.
- [x] Candidatos de D1 incorporados desde `SEC-PHYS-v0.1` — §9.bis y §9.ter.
- [ ] Consolidación final de T-11 con los candidatos de A1, A2, A3 y D2 — Puerta 2.
- [ ] Cinco cantidades dependen de dato externo; ninguna se inventa.

## Trazabilidad

Ver [`trazabilidad/TRZ_C4.md`](trazabilidad/TRZ_C4.md).

