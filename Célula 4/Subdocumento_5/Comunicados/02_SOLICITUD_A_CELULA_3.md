# Solicitud de Célula 4 a Célula 3

**Asunto:** información que el Subdocumento 5 necesita del Subdocumento 4
**Emite:** Célula 4 — Modelo y gestión de datos (V. Guzmán / M. Reyes)
**Recibe:** Célula 3 — Arquitectura lógica, física, de integración y de seguridad
**Fecha:** 6 de septiembre de 2026

---

## Respuesta incorporada al cruce C3–C4

El Subdocumento 5 queda **cubierto en sus trece apartados para diseño I1**. Célula 3 entregó la baseline arquitectónica y A2 contiene el catálogo de 21 contrapartes + 7 familias, patrón de eventos persistente, contrato tipo, idempotencia, DLQ/replay y fallback. Los contratos reales por contraparte continúan condicionados externamente y no se inventan.

Las peticiones originales se conservan debajo como trazabilidad. Su estado vigente es: `PEN-03`, `PEN-08` y la frontera local quedan `CERRADO I1`; `PEN-01`, `PEN-02`, `PEN-05`, `PEN-06` y `PEN-07/07b` quedan `RECIBIDO` con condiciones explícitas; `PEN-17/18/19` permanecen `CONDICIONADO EXTERNO` por mediciones, política de imagen y matriz de copias.

Van ordenadas por urgencia real, no por número.

---

## Bloque A — Las tres urgentes

### `PEN-03` · CERRADO I1 — propiedad del modelo conceptual

**Qué pedimos.** Un acuerdo por escrito sobre el corte entre su sección 4.1.5 y nuestro § 5.14.

**Por qué es urgente.** El contrato de su entregable de arquitectura lógica incluye entre sus productos obligatorios un «modelo conceptual de dominio y eventos», y el consolidado del Subdocumento 4 reserva la sección 4.1.5 para él. A la vez, su propio maestro de contexto declara que **el Subdocumento 5 es propietario del modelo de datos detallado**. Si ambos publicamos, el Informe 1 sale con dos modelos conceptuales que un evaluador va a comparar.

**Propuesta concreta para que no haya que discutirlo:** modelo conceptual de alto nivel en su 4.1.5 —contextos, responsabilidades y eventos principales— y modelo de datos con diccionario en nuestro § 5.14, **usando los mismos nombres de negocio**. Nosotras ya tenemos publicados 14 diagramas y 80 entidades; si les sirven, están disponibles.

**Qué queda condicionado si no hay respuesta:** § 5.2 y § 5.14.

---

### `PEN-02` · RECIBIDO CON CONDICIONES — ocho búsquedas cifradas

**Qué pedimos.** Respuesta atributo por atributo sobre esta lista, no una política general.

| # | Atributo | Para qué lo indexamos | Umbral en juego |
|---:|---|---|---|
| 1 | `POSICION_VIGENTE.id_celda` | ocupación de celda e invariante de no colisión | ≤ 1 s |
| 2 | `MOVIMIENTO.celda_origen` | trazabilidad del movimiento | ≤ 1 s |
| 3 | `MOVIMIENTO.celda_destino` | idem | ≤ 1 s |
| 4 | `CONTENEDOR.clase_imdg` | segregación de mercancías peligrosas | validación en captura |
| 5 | `LECTURA_OPTICA.codigo_leido` | conciliación de lectura con visita abierta | ≤ 3 s |
| 6 | `CONDUCTOR.id_persona` | verificación de habilitación en barrera | ≤ 120 s compuesto |
| 7 | `EVENTO_ACCESO.id_persona` | conteo de personas por zona en tiempo real | tiempo real |
| 8 | `HECHO_FACTURABLE.id_regla_aplicada` | reproducción de la valorización | ≤ 30 s |

**Por qué es urgente.** Los ocho están simultáneamente en el catálogo de cifrado a nivel de campo que exige `CP, Cap. 15, RT-11.10` y en nuestra lista de claves de acceso indexadas. Un esquema de cifrado que impida la búsqueda por igualdad **hace inalcanzables los umbrales de un segundo de `RT-09.01`**, y eso no se arregla con más hardware.

**Qué queda condicionado:** cinco de nuestros veintiún índices, y con ellos el compromiso de desempeño del § 5.10.

---

### `PEN-01` · RECIBIDO — zonas y fases de la matriz de autoridad

**Qué pedimos.** La matriz `dominio × zona × fase` con sus valores, y la confirmación de que reutilizan la fuente de verdad definida por Célula 2 en la Decisión N.º 1 **sin redefinirla**.

**Por qué es urgente.** Es el nivel 1 de nuestra cascada de resolución de conflictos de posición (`DEC-C4-15`), que `CP, Cap. 15, RT-03.13` exige que sea determinista. Sin zonas nombradas, la regla existe pero no se puede aplicar a un caso concreto.

**Cómo lo tratamos mientras tanto.** Las zonas quedan **parametrizadas y no enumeradas**: el modelo admite N zonas sin cambiar su estructura, de modo que incorporar sus nombres cuesta una columna. No es un bloqueo, es una marca de provisionalidad.

**Qué queda condicionado:** § 5.3, § 5.9 y la aplicabilidad de `DEC-C4-15`.

---

## Bloque B — Las que condicionan el § 5.4 y el § 5.13

### `PEN-05` · RECIBIDO PARA DISEÑO — contratos reales condicionados

**Qué pedimos.** Qué integraciones tendrán contrato confirmado antes de la entrega y cuáles quedan declaradas «por levantar» en el Informe 1.

**Respuesta vigente.** A2 cierra el diseño del apartado con 21 contrapartes, 7 familias, contratos tipo, versiones, idempotencia, DLQ/replay y fallback. El contrato técnico y CDC del TOS, junto con interfaces de terceros, permanecen `POR LEVANTAR` o `BLOQUEADO EXTERNO` por fila.

**Lo que no haremos:** inventar una interfaz, un protocolo, una versión o una disponibilidad de terceros. Su propia regla negativa N.º 9 lo prohíbe y la respetamos.

---

### `PEN-06` · RECIBIDO — eventos persistentes; CDC condicionado

**Qué pedimos.** La decisión de mecanismo de integración, aunque sea preliminar.

**Por qué.** De ella depende el flujo desde la operación hacia la analítica y, con él, la **latencia real** de los indicadores que ya comprometimos: posición visible en ≤ 30 s, portal en ≤ 60 s, indicadores del concedente en ≤ 1 h tras el cierre de turno.

**Cómo lo tratamos mientras tanto.** Comprometemos la **latencia por indicador** como requisito y no el mecanismo que la produce, y presentamos ambas rutas.

---

### `PEN-07` y `PEN-07b` · RECIBIDO — producto de referencia y emplazamiento

**Qué pedimos.** Dos respuestas: si el Informe 1 nombra productos de base de datos o solo capacidades; y qué almacenes quedan on-premise, cuáles en nube y cuáles en el borde.

**Qué les entregamos para que decidan.** La comparación completa de **trece alternativas** sobre siete criterios ponderados, con recomendación por capacidad y sin producto seleccionado. Está en el Anexo de persistencia del Subdocumento 5. Es exactamente el insumo que su propia regla de aprobación de decisiones de arquitectura exige: *nombrar un producto sin comparar el problema que resuelve no es una decisión arquitectónica suficiente*.

**Alineación vigente.** AWS mantiene el registro consolidado y la carga principal en operación normal; el núcleo local conserva estado crítico caliente y asume autoridad durante el corte. La exigencia es la ruta local completa, no un primario permanente en el borde.

---

### `PEN-08` · CERRADO I1 — volumetría por escenarios

**Qué pedimos.** Confirmación de las dieciocho dimensiones con el factor estacional incorporado, o aviso de que las recalcularán.

**Por qué.** Toda nuestra capacidad acumulada se apoya en ellas. Si cambian, cambian el dimensionamiento por familia, la frontera entre retención en línea y archivo, y el disparador de revisión de la capa analítica.

**Un dato que les servirá.** Nuestro `DEC-C4-17` declara que el flujo crudo de posicionamiento **no se persiste**. Sin esa declaración la volumetría no cuadra: persistirlo serían ≈350 GB al año contra los ≈20 GB de almacenamiento transaccional declarado. El flujo igual cruza la red, así que sigue contando para el dimensionamiento de la red de patio.

---

### `PEN-10` · CERRADO I1 — frontera local y buffer

**Qué pedimos.** Qué datos persisten localmente durante las 72 horas y con qué tamaño de buffer comprometido.

**Respuesta vigente.** La baseline I1 usa 21,9 GB a peak estacional, 32,5 Mbps de reposición y dos caminos WAN de al menos 35 Mbps disponibles. 39 GB/57,8 Mbps es crecimiento futuro 3×; ≈40 GB/≈58 Mbps es una sensibilidad separada de imagen a 1 MB.

---

## Bloque C — Las que afectan el dimensionamiento fino

### `PEN-17` · CONDICIONADO EXTERNO — latencia y ancho de banda medidos

**Qué pedimos.** La latencia que sostiene la red inalámbrica en condición de patio cargado con pilas de cinco alturas, y el ancho de banda del enlace de reposición.

**Por qué.** El umbral de un segundo se mide de extremo a extremo. La baseline I1 exige 32,5 Mbps útiles y WAN ≥35 Mbps; ≈58 Mbps pertenece al escenario futuro 3× o a la sensibilidad separada de imagen.

---

### `PEN-18` · Política de captura de imágenes *(conjunta)*

**Qué pedimos.** Resolución, compresión y si el binario cruza el enlace dentro de la ventana de sincronización.

**Por qué es conjunta y no nuestra.** La resolución la condiciona el equipo de reconocimiento óptico que ustedes especifican, y el umbral de 3 segundos de `RNF-DES-02` depende de esa misma resolución. Fijarla por nuestra cuenta sería parametrizar un componente que no especificamos.

**Por qué importa tanto.** Las imágenes son el **94 % del almacenamiento anual** y el **86 % del volumen de la ventana de sincronización**. Es la palanca de mayor efecto de todo el Subdocumento 5.

---

### `PEN-19` · Esquema de copias para el respaldo 3-2-1-1-0

**Qué pedimos.** Cuántas copias del almacenamiento de objetos, dónde y con qué mecanismo de inmutabilidad.

**Por qué.** Es el supuesto con más efecto sobre nuestra cifra final de capacidad. Las cifras anuales de la volumetría traen factor ×3 en transaccional y series —que ya incluye replicación y respaldo— pero solo ×1,2 en imágenes, que cubre metadatos y **no copias**. Asumimos una copia adicional, y de ahí sale la diferencia entre 9,9 TB de dato y 18,1 TB de capacidad a aprovisionar.

---

## Resumen de lo que les entregamos a cambio

| Entrega | Qué contiene | Dónde |
|---|---|---|
| `E-01` | Capacidad acumulada por familia y horizonte, dos escenarios, con reparto borde/nube y el buffer de 72 h | Anexo de capacidad |
| `E-02` | Necesidad de persistencia por familia, con trece alternativas comparadas y recomendación por capacidad | Anexo de persistencia |
| `E-03` | Los atributos que son clave de acceso indexada y los ocho que chocan con el cifrado | Anexo de desempeño |
| `E-04` | Requisitos de buffer local, orden de reconciliación y funciones no disponibles sin enlace | § 5.5 y Anexo CAP |
| — | Las 21 decisiones de Célula 4, con su fundamento | comunicado de decisiones |

**Una cifra para cerrar:** la solución completa, a diez años y crecida al triple, se dimensiona en **decenas de terabytes, no en centenas**, y el motor que sostiene las 78 entidades relacionales y las veinte invariantes son **180 GB en línea**. La capacidad no es lo que decide su arquitectura física. Lo que decide es la latencia de un segundo, la autonomía de 72 horas y la ventana de sincronización.
