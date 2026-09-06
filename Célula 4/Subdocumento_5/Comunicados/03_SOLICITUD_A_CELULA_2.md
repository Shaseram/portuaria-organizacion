# Solicitud de Célula 4 a Célula 2

**Asunto:** información que el Subdocumento 5 necesita del Subdocumento 3
**Emite:** Célula 4 — Modelo y gestión de datos (V. Guzmán / M. Reyes)
**Recibe:** Célula 2 — Esquema de solución, alcance y catálogos de requerimientos
**Fecha:** 6 de septiembre de 2026

---

## Contexto

El Subdocumento 5 se construyó **sobre la línea base posterior a las rondas de corrección del 5 de septiembre**: 139 requerimientos funcionales, 91 no funcionales, 11 reglas de negocio, 21 decisiones y 25 supuestos, con reparto 82 / 57 entre etapas. Las siete adiciones de esa ronda están incorporadas: los cuatro `RNF-DES-09` a `12`, los tres `RNF-DIS-13` a `15`, la corrección de `RF-REF-07`, la nueva `RN-11`, el factor estacional de la volumetría y el nuevo `RF-POR-09`.

Son **cinco peticiones**. Tres son vacíos que su propio cierre declara abiertos; dos son decisiones de trazabilidad que les corresponde tomar a ustedes.

---

## 1. `PEN-04` · ¿De qué evento se deriva el movimiento de grúa de muelle?

**Qué pedimos.** La declaración del evento del que se origina un movimiento de muelle en el modelo de datos.

**Por qué se lo pedimos a ustedes.** Su propio anexo de segunda ronda lo dejó abierto con estas palabras: el Capítulo 14.1 del caso define 74 equipos a instrumentar —18 grúas de patio, 42 tractocamiones y 14 pesados— y **no incluye las seis grúas de muelle**; conviene declarar en el catálogo qué evento produce el movimiento de muelle. Célula 3 lo recogió igual en su maestro.

**Por qué nos afecta.** Tres cosas dependen de esto:

1. **El modelo de datos.** La entidad `MOVIMIENTO` distingue carga y descarga y se enlaza con la recalada, pero su atributo de origen queda marcado como vacío declarado.
2. **La productividad de grúa**, que es el resultado de negocio N.º 6 del caso y se mide en movimientos por hora y por equipo.
3. **El cálculo de emisiones.** Nuestra `DEC-C4-01` atribuye consumo por movimientos ejecutados, y el consumo de las grúas de muelle no entra por la vía de la instrumentación de equipos porque su sistema de control no se interviene.

**Lo que no haremos.** Presumir una interfaz con el sistema del fabricante. La restricción no negociable N.º 3 es explícita: cualquier obtención de datos desde él es integración de solo lectura sujeta a autorización, y su factibilidad debe verificarse antes de comprometerla.

---

## 2. `PEN-09` · Valores de banda y duración de la desviación de temperatura

**Qué pedimos.** Que definan si la banda y la duración mínima de `RN-11` quedan abiertas en el Informe 1 o se acotan a un rango justificado con el CLIENTE.

**Por qué se lo pedimos a ustedes.** `RN-11` es suya, y la escribieron declarando que **no fija valores numéricos porque el caso no los entrega**. Estamos de acuerdo con esa decisión y no la reabrimos.

**Por qué nos afecta.** Son los dos únicos atributos del diccionario —`PARAMETRO_DESVIACION.banda_superior` y `banda_inferior`— que quedan marcados como **vacío declarado** entre los 451. Nuestra regla es que ante la duda se marca como pendiente, y un valor plausible en una celda de diccionario es indistinguible de un hecho.

**Cómo lo tratamos mientras tanto.** Modelado como **parámetro versionado** con vigencia y autor, nunca como constante del esquema, y con la duración mínima acotada para que ninguna parametrización futura haga inalcanzable el plazo de alarma de cinco minutos. Cada alarma guarda la versión del parámetro con que se evaluó, de modo que una alarma histórica se puede reproducir.

**Una observación técnica que puede ayudarles con el CLIENTE.** La banda admisible depende de la carga, no del terminal: fruta fresca y congelado tienen consignas y tolerancias distintas, y quien las fija es el exportador en su contrato de cadena de frío. Puede que la respuesta correcta no sea un valor sino un **catálogo de perfiles por tipo de carga**.

---

## 3. `PEN-10b` · Vigencia de `RF-PAT-07`

**Qué pedimos.** Confirmación de si tratamos `RF-PAT-07` como vigente para el modelo de condiciones dinámicas del patio.

**Por qué.** Su cierre lo declara pendiente de validación interna, y el maestro de Célula 3 lo recoge como escalamiento abierto con la instrucción de usarlo como condición vigente con marca de validación.

**Cómo lo tratamos mientras tanto.** La entidad `CONDICION_DINAMICA` existe en el modelo con su tipo, alcance, autor, motivo y vigencia, y queda **sujeta a confirmación** sin bloquear nada. Si el requerimiento se retira, la entidad se retira con él.

---

## 4. `PEN-05b` · ¿Crean el requerimiento no funcional de calidad de datos?

**Qué pedimos.** Una decisión: si incorporan a su catálogo un requerimiento de calidad de datos, o si la materia queda solo en el Subdocumento 5.

**El contexto.** El catálogo vigente de 91 requerimientos no funcionales **no cubre `BTT, Cap. 5, RT-05.04`**, que exige gestionar la calidad conforme a ISO/IEC 25012 con validación en el punto de captura, indicadores de completitud, exactitud y consistencia, y tablero de calidad disponible para el CLIENTE. `BA, Art. 23` añade el saneamiento de los datos migrados y `BA, Art. 13` lista la norma entre los estándares exigibles. Célula 3 declaró la materia pendiente remitiéndola al cruce entre nuestro subdocumento y el plan de pruebas.

**Qué hicimos.** La asumimos íntegra (`DEC-C4-11`): 54 reglas de calidad con umbral, responsable y evidencia; 12 indicadores con fórmula; 12 pruebas con criterio de aceptación. **La materia está cubierta pase lo que pase.** Lo que está en juego es solo la trazabilidad del Formulario T-12, que debe cubrir todos los códigos `RT`.

**Se los dejamos redactado**, con la estructura de su catálogo, para que solo tengan que pegarlo si están de acuerdo:

> **`RNF-CAL-01` · Calidad de datos**
> **Requerimiento:** La solución gestionará la calidad de los datos conforme a ISO/IEC 25012, con validación en el punto de captura, indicadores de completitud, exactitud, consistencia, credibilidad, actualidad, accesibilidad, conformidad, precisión y trazabilidad, y un tablero de calidad de acceso permanente para el CLIENTE con capacidad de profundización hasta el registro defectuoso.
> **Umbral:** 100 % de los dominios de información con reglas de calidad declaradas y responsable de corrección asignado; indicadores disponibles dentro de la hora siguiente al cierre de turno.
> **Verificación:** Auditoría de la matriz de calidad contra el diccionario de datos, y prueba de profundización desde un indicador desviado hasta el registro que lo origina.
> **Prioridad:** Crítica.
> **Origen:** FEP02 Cap. 5, RT-05.04; FEP01 Art. 13 y Art. 23.

**Una precisión sobre la norma**, por si la usan en su catálogo: ISO/IEC 25012 define **quince características**, no seis, y *unicidad* no es una de ellas —pertenece a otros marcos—. En la norma se expresa como consistencia y se implementa con clave de idempotencia, que es un control, no una dimensión.

---

## 5. `PEN-11` · ¿El catálogo de campos cifrados pasa a su registro?

**Qué pedimos.** Que decidan si el catálogo de campos sujetos a cifrado a nivel de campo se incorpora a su registro o se queda como anexo del Subdocumento 5.

**El contexto.** `RNF-SEG-05` compromete cubrir **el 100 % de los campos identificados como sensibles**, y `CP, Cap. 15, RT-11.10` nombra las tres familias: datos personales, información comercial sensible y datos que permitan inferir el contenido de valor o la ruta de un contenedor. Nadie había producido la lista, y un compromiso de cobertura sobre un conjunto que no existe no es verificable.

**Qué hicimos.** La derivamos del diccionario: **28 atributos** repartidos en las tres familias, con el fundamento de cada uno. Está en el Subdocumento 5 y se las traspasamos completa si la quieren en su registro.

**Un dato que conviene que sepan:** ocho de esos 28 atributos son a la vez clave de acceso indexada, y ya se lo consultamos a Célula 3, porque un cifrado que impida buscar por igualdad sobre ellos rompe los umbrales de un segundo.

---

## Lo que les devolvemos

| Qué | Para qué les sirve |
|---|---|
| **Las 21 decisiones de Célula 4** | Para que su catálogo y su narrativa no las contradigan sin saberlo |
| **`RNF-CAL-01` redactado** | Para cerrar la trazabilidad de `RT-05.04` en el T-12 con un pegado |
| **Catálogo de 28 campos cifrados** | Para que `RNF-SEG-05` deje de comprometer una cobertura sobre un conjunto inexistente |
| **Filas del T-12 de los códigos `RT` de datos** | `RT-05.01` a `RT-05.30`, `RT-09.xx`, `RT-11.10`, `RT-16.07` y `RT-16.09`, con la sección del Subdocumento 5 que acredita cada uno. Se las armamos en cuanto nos digan el formato de la fila |

**Y una corrección que puede afectarles.** Al revisar el modelo detectamos que `CONDUCTOR` y `PERSONA` duplicaban el documento de identidad, ambos con marca de unicidad y cifrado, mientras `PERSONA.tipo` ya incluía «conductor». Es duplicación de una entidad compartida, que `RT-05.09` prohíbe, y significaba cifrar y retener el mismo dato personal dos veces con dos plazos que pueden divergir. Está corregido en el modelo. Si tienen requerimientos que traten al conductor como entidad independiente en materia de datos personales, conviene alinearlos.
