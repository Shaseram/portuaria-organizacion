# Catálogo de Requerimientos Funcionales — DEFINITIVO · Parte 1 de 3
 
## Dominios `RF-CON` y `RF-GAT` — 30 requerimientos, Etapa 1
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo B** · **Versión 2.0 — correcciones de la Fase 4 ya aplicadas.**
> **Este archivo reemplaza a `catalogo_rf_01_convivencia_gate.md`.** Las fichas están completas y corregidas; no requiere consultar ningún documento de corrección.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Sección | Contenido |
|---|---|
| **1** | Convenciones del catálogo — ficha, clasificación, granularidad, redacción y regla de cita |
| **2** | `RF-CON` — Convivencia con el sistema de 2012 · **14 requerimientos** |
| **3** | `RF-GAT` — Gate, citas, documentación y pesaje · **16 requerimientos** |
| **4** | Trazabilidad de la parte 1 |
 
> **Partes del catálogo:** Parte 1 — `RF-CON`, `RF-GAT` · Parte 2 — `RF-PAT`, `RF-TRA`, `RF-REF`, `RF-ACC`, `RF-OPD` · Parte 3 — `RF-NAV`, `RF-INT`, `RF-FAC`, `RF-POR`, `RF-INS`, `RF-EMI`, `RF-APP`, `RF-FIR`.
 
---
 
## 1. Convenciones del catálogo
 
### 1.1 Ficha de ocho campos
 
Siete los exige el CP, Cap. 17.1. El octavo —criterio de aceptación— lo exige la matriz de trazabilidad del mismo capítulo.
 
### 1.2 Clasificación funcional / no funcional
 
El CP, Cap. 17.2 deja casos limítrofes sin resolver y evalúa la **consistencia del criterio declarado**:
 
> **Funcional** = describe un comportamiento observable que produce un resultado.
> **No funcional** = califica *cómo* debe comportarse algo ya descrito en otra parte.
 
Ningún umbral que viva en el catálogo de RNF se repite aquí: se referencia.
 
### 1.3 Granularidad
 
> **La unidad de un requisito es la unidad de su prueba.** Si un solo procedimiento finito comprueba todas sus cláusulas, es un requisito. Si hacen falta dos pruebas independientes que pueden fallar por separado, son dos.
 
### 1.4 Redacción
 
«Deberá» para lo obligatorio; «podrá» para lo deseable. Voz activa, sujeto explícito, términos clave en negrita. Prohibidos los verbos de interpretación múltiple —manejar, procesar, rechazar, ignorar— y las palabras subjetivas sin métrica.
 
### 1.5 Regla de cita — colisión de numeración RT
 
> **El BTT y el Capítulo 15 del CP usan los mismos códigos `RT-CC.NN` para materias distintas.** `RT-05.10` es «catálogo de linaje» (Deseable) en el BTT y «retención de datos» en el CP; `RT-16.14` es «motor de reglas» (Deseable) en el BTT y «firma electrónica» en el CP; lo mismo ocurre con `RT-16.21`, `RT-16.30` y `RT-21.06`.
>
> **Todo código se cita con su documento de origen.** El parámetro del caso, al CP, Cap. 15; la obligación transversal, al BTT. Ver **Supuesto M** en `../02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`.
 
**Sobre `RT-05.29` y `RT-09.01`:** el inventario de los 374 códigos los clasifica como **no funcionales**, y esa clasificación se mantiene. Aportan a los requerimientos que los citan el **umbral de verificación**, no la conducta; la conducta proviene del CP, capítulos 4, 9 y 18. Es el caso limítrofe que el CP, Cap. 17.2 plantea.
 
### 1.6 Requerimientos en revisión
 
Los marcados con **⚠** repiten un compromiso que ya vive en el catálogo de RNF. Están vigentes y en el conteo; su estado se consolida en `../03_Trazabilidad_y_Bases/registro_correccion_plan_maestro_20260904.md`. **En esta parte no hay ninguno.**
 
---
 
## 2. Dominio `RF-CON` — Convivencia con el sistema de operación de 2012
 
**Etapa 1 · 14 requerimientos.** Materializan la Decisión N° 1 y sostienen los criterios de aceptación 1 y 20 en su dimensión de trazabilidad.
 
---
 
### `RF-CON-01` — Fachada de servicios única · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** exponer toda lectura y toda escritura dirigida al sistema de operación de 2012 a través de una **fachada de servicios única**, de modo que ningún componente consumidor acceda a las interfaces nativas de ese sistema.
 
**Actor:** componentes consumidores de la solución.
**Precondición:** interfaces del sistema de 2012 identificadas en el descubrimiento de los meses 1 a 4.
**Resultado esperado:** cero accesos directos al sistema de 2012 originados fuera de la fachada.
**Origen:** BTT, RT-05.20 (Obligatorio) · Decisión N° 1, requerimientos que introduce la decisión.
**Criterio de aceptación:** sobre una ventana de **siete días en preproducción con un volumen mínimo declarado de transacciones**, la traza de red y el registro de correlación acreditan que el **100 %** de las transacciones dirigidas al sistema de 2012 atraviesan la fachada.
 
---
 
### `RF-CON-02` — Contrato de interfaz versionado · Prioridad: **Crítica**
 
**Descripción.** La fachada **deberá** exponer un contrato de interfaz **versionado semánticamente**, de modo que un cambio en el modelo de datos del sistema de 2012 no obligue a modificar a sus consumidores.
 
**Actor:** componentes consumidores.
**Precondición:** fachada desplegada (`RF-CON-01`).
**Resultado esperado:** los consumidores operan contra una versión declarada del contrato, independiente de la semántica interna del sistema legado.
**Origen:** **BTT, RT-05.17** (versionado semántico con compatibilidad hacia atrás y preaviso mínimo de seis meses — Obligatorio) · BTT, RT-05.20 · BTT, RT-05.16 como refuerzo, para la obligación de documentar el contrato · Decisión N° 1.
**Criterio de aceptación:** se valida la compatibilidad mediante un **contrato versionado** y un *stub*, *fixture* o versión real acordada con el fabricante que represente tres cambios patrón —campo nuevo, campo renombrado y tipo incompatible—, y se acredita que ningún consumidor de la versión anterior requiere recompilación ni modificación. **No se altera arbitrariamente el esquema del producto comercial para ejecutar la prueba.**
 
> *Corrección aplicada: el origen citaba RT-05.16 (documentación OpenAPI), que no sostiene el versionado. La prioridad sube a Crítica al quedar anclada en un código Obligatorio.*
 
---
 
### `RF-CON-03` — Escritura dual durante la convivencia · Prioridad: **Crítica**
 
**Descripción.** Mientras un dominio esté en convivencia, la solución **deberá** escribir cada hecho operacional **simultáneamente** en su propio registro y en el sistema de operación de 2012, de modo que ambos registros permanezcan al día.
 
**Actor:** solución.
**Precondición:** dominio en convivencia y escritura dual habilitada.
**Resultado esperado:** ambos registros contienen el mismo hecho **en no más de 60 segundos**; toda diferencia mayor computa como divergencia.
**Origen:** Decisión N° 1, mecanismos de convivencia. Es la precondición de la reversibilidad comprometida en CP, 13.3 punto 5.
**Criterio de aceptación:** sobre una muestra de un turno completo, el **100 %** de los hechos registrados en la solución tiene su correspondiente en el sistema de 2012 dentro de los 60 segundos.
 
> *Valor provisional. La ventana de desfase definitiva se fija en la puerta de decisión del mes 4, al medirse la latencia real de escritura hacia el sistema de 2012.*
 
---
 
### `RF-CON-04` — Apagado controlado de la escritura dual · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** exigir la **aprobación explícita de dos perfiles autorizados del CLIENTE** para apagar la escritura dual de un dominio en operación normal, y **deberá** registrar ambas aprobaciones con autor, fecha, hora y justificación. La vía de emergencia se limita al mecanismo *break-glass* preautorizado y auditado de `RF-CON-08`; no constituye un apagado ordinario.
 
**Actor:** perfil autorizado del CLIENTE.
**Precondición:** marcha blanca del dominio cerrada formalmente.
**Resultado esperado:** el apagado queda registrado como acto aprobado; no ocurre de forma automática ni por configuración.
**Origen:** BTT, RT-16.03 (doble aprobación de cambios con impacto operacional) · Decisión N° 1: «el apagado es un hito con aprobación explícita del CLIENTE, no un evento automático».
**Criterio de aceptación:** se intenta el apagado con un solo perfil y el sistema no lo ejecuta; se repite con doble aprobación y el registro de auditoría consigna ambos autores y la justificación.
 
---
 
### `RF-CON-05` — Conciliación automática por turno · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** conciliar automáticamente, **al cierre de cada turno**, la posición de contenedor, los movimientos registrados y las entradas y salidas por gate entre su propio registro y el del sistema de 2012, y **deberá** producir un informe de divergencias.
 
**Actor:** solución.
**Precondición:** dominio en convivencia con escritura dual activa.
**Resultado esperado:** informe de conciliación disponible al cierre de cada uno de los tres turnos, con cada divergencia identificada.
**Origen:** CP, 17.6 punto 2 · Decisión N° 1. La frecuencia por turno responde a que el CP, Anexo B.1 identifica el cambio de turno como «punto de pérdida de información».
**Criterio de aceptación:** durante siete días consecutivos se emiten los **21 informes de turno** sin omisión, y una divergencia inyectada deliberadamente aparece identificada en el informe correspondiente.
 
> **Relación con `RF-GAT-15`.** La conciliación de gate opera en dos niveles: **por turno** con umbral de alerta, dentro de este requerimiento, y **al cierre diario** con umbral cero, en `RF-GAT-15`. No son frecuencias contradictorias sino dos controles encadenados.
 
---
 
### `RF-CON-06` — Clasificación direccional de divergencias · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** clasificar cada divergencia de conciliación en una de cuatro categorías —explicada por desfase temporal, sistema nuevo correcto, sistema nuevo incorrecto, o no resuelta— contrastándola contra verificación física, y **deberá** computar contra el umbral únicamente las dos últimas.
 
**Actor:** solución y supervisor de turno del CLIENTE.
**Precondición:** informe de conciliación emitido (`RF-CON-05`) y muestra de verificación física del turno disponible.
**Resultado esperado:** cada divergencia queda clasificada; las divergencias en que el sistema nuevo resulta correcto se registran como **evidencia de mejora** y no penalizan la marcha blanca.
**Origen:** Decisión N° 1, regla direccional de clasificación. Sin ella la marcha blanca penalizaría a la solución por ser más exacta que el sistema al que reemplaza.
**Criterio de aceptación:** sobre una muestra de **50 divergencias verificadas físicamente**, el 100 % queda clasificado en una de las cuatro categorías, y ninguna divergencia con sistema nuevo correcto computa contra el umbral.
 
**Definición operativa —«diferencia no explicada».** Una divergencia se considera **explicada** cuando el supervisor de turno del CLIENTE la clasifica en una de las tres primeras categorías con la evidencia que la sustenta —registro de desfase, verificación física o traza de movimiento—. Una divergencia no clasificada dentro de la ventana aplicable computa como **no explicada**. Esta definición rige para `RF-CON-05`, `RF-CON-07`, `RF-GAT-15` y `RF-FAC-10`.
 
---
 
### `RF-CON-07` — Detención automática del avance del dominio · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** congelar automáticamente el avance de un dominio y notificar al Comité de Proyecto cuando las divergencias no explicadas superen el umbral de detención declarado para ese universo.
 
**Actor:** solución.
**Precondición:** conciliación de turno ejecutada y divergencias clasificadas.
**Resultado esperado:** avance congelado, notificación emitida y ventana de investigación abierta — **48 horas** para posición y movimientos, **24 horas** para gate y hechos facturables.
**Origen:** **BA, Art. 17.3** fija la condición de cierre de la marcha blanca: la conciliación no debe presentar diferencias no explicadas. **Los umbrales, el congelamiento del avance y las ventanas de investigación son decisión propia de Terabyte** (Decisión N° 1, mecanismos de convivencia) · CP, 17.6 punto 2.
**Criterio de aceptación:** se inyecta un volumen de divergencias sobre el umbral y se acredita que el avance queda congelado sin intervención manual y que la notificación se emite con marca de tiempo.
 
---
 
### `RF-CON-08` — Reversión de dominio por redirección de enrutamiento · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** permitir devolver la autoridad del registro de un dominio al sistema de operación de 2012 mediante **redirección del enrutamiento en la fachada**, sin modificar ningún componente consumidor, y **deberá** completar la operación en **no más de 15 minutos** desde la decisión. En operación normal requiere doble control; ante una emergencia crítica podrá emplearse un procedimiento *break-glass* previamente autorizado, limitado a cargos nominales, registrado de forma inalterable y sometido a revisión posterior.
 
**Actor:** dos perfiles autorizados en operación normal; supervisor de turno del CLIENTE o jefe de turno de marcha blanca de Terabyte mediante *break-glass* preautorizado en emergencia.
**Precondición:** escritura dual del dominio activa.
**Resultado esperado:** el dominio queda operando contra el sistema de 2012, con la operación restituida y sin pérdida de hechos registrados.
**Origen:** CP, 13.3 punto 5 (retorno probado por dominio) · CP, 17.6 punto 5 · Decisión N° 1. **El objetivo de 15 minutos para la restitución es un compromiso propio de Terabyte**, más exigente que el tiempo de **respuesta** de 15 minutos y muy por debajo del tiempo de **resolución** de 4 horas que el BA, Art. 78.2 fija para severidad crítica. Su fundamento es operacional: cuatro horas con una nave amarrada equivalen, a 24,8 movimientos por hora de grúa, a un centenar de movimientos perdidos.
**Criterio de aceptación:** se ejecuta un simulacro con doble control y otro mediante *break-glass* por cada cargo facultado, incluidos los tres turnos y la madrugada; en todos se mide el tiempo contra 15 minutos y se recuperan la autorización, la bitácora inalterable y la revisión posterior.
 
> *Corrección aplicada: el origen presentaba los 15 minutos como derivación del BA, Art. 78.2. Es un compromiso propio más exigente que la base, y así se declara.*
 
---
 
### `RF-CON-09` — Verificación física del inventario por barrido de bloques · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** soportar la verificación física de la posición del inventario mediante **barrido por bloques con congelamiento lógico**, registrando la lectura del código mediante las terminales de equipo y el reconocimiento óptico, y **deberá** reconciliar contra el registro de movimientos los desplazamientos ocurridos en otros bloques durante el barrido.
 
**Actor:** operador de equipo de patio y supervisor.
**Precondición:** bloque con depósitos y retiros suspendidos y operación redirigida a bloques vecinos.
**Resultado esperado:** posición verificada de la totalidad del inventario del bloque, sin conteo manual y sin detener el patio completo.
**Origen:** CP, Cap. 15, RT-05.15 (migrar la totalidad del inventario «con posición verificada físicamente») · CP, 17.6 punto 3 · Decisión N° 1.
**Criterio de aceptación:** se ejecuta el barrido sobre un bloque y se repite sobre una muestra del mismo bloque; el **error del procedimiento, estimado por esa repetición, es ≤ 0,5 %**.
 
> *Corrección aplicada: el criterio anterior solo exigía documentar el error, sin umbral. El 0,5 % se alinea con el umbral de conciliación de la Decisión N° 1: un barrido menos exacto que el umbral que debe verificar no sirve.*
 
---
 
### `RF-CON-10` — Observabilidad y auditoría de la convivencia · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar cada transacción dirigida al sistema de 2012 con un **identificador de correlación común**, que permita seguir una operación completa entre la fachada, el registro propio y el sistema legado.
 
**Actor:** solución.
**Precondición:** fachada desplegada.
**Resultado esperado:** cualquier operación de convivencia es reconstruible extremo a extremo desde un único identificador.
**Origen:** BTT, RT-05.19 · BTT, RT-05.03 · Decisión N° 1.
**Criterio de aceptación:** dado el identificador de una operación cualquiera, se reconstruye su recorrido completo por los tres registros **sin acceso a la base de datos**.
 
---
 
### `RF-CON-11` — Producción trazable de los indicadores del concedente · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** producir los indicadores comprometidos en el contrato de concesión **a partir de los eventos que los originan**, y **no deberá** admitir su carga, edición ni reconstrucción manual.
 
**Actor:** solución.
**Precondición:** eventos de origen registrados en el dominio correspondiente.
**Resultado esperado:** cada valor de indicador es rastreable hasta las transacciones que lo componen.
**Origen:** CP, Cap. 10, restricción no negociable N° 14 («de forma trazable y auditable, no reconstruirlos») · CP, Cap. 18, criterio 20 · **CP, Cap. 15, RT-05.29** aporta el umbral de consolidación —no superior a 1 hora tras el cierre del turno—; la conducta proviene del CP, Cap. 10 y Cap. 18.
**Criterio de aceptación:** se intenta editar manualmente un valor de indicador y el sistema no lo permite; se selecciona un valor consolidado y se desciende hasta las transacciones de origen que lo componen.
 
---
 
### `RF-CON-12` — Declaración de frontera entre parametrización y desarrollo · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** exponer al CLIENTE el **inventario de elementos parametrizables** desde la interfaz, con su tipo de dato, rango admisible y perfil autorizado. Terabyte **deberá** declarar en la propuesta qué elementos requieren desarrollo y no admiten parametrización.
 
**Actor:** CLIENTE.
**Precondición:** solución desplegada.
**Resultado esperado:** el CLIENTE distingue, sin consultar a Terabyte, qué puede cambiar por sí mismo y qué requiere una solicitud de cambio.
**Origen:** **BTT, RT-16.04** (Obligatorio: «Presentar como parametrizable lo que exige desarrollo se evaluará como **observación grave**») · BTT, RT-16.02 · CP, Cap. 10, restricción no negociable N° 11 (el área de TI del CLIENTE son cinco personas).
**Criterio de aceptación:** el inventario publicado coincide con los elementos efectivamente parametrizables, verificado modificando una muestra de **10 parámetros declarados** desde la interfaz sin intervención de Terabyte, y comprobando que ningún elemento declarado como parametrizable requirió desarrollo.
 
> *Requerimiento nuevo. RT-16.04 es Obligatorio con sanción explícita y no estaba citado en ningún requerimiento del catálogo original.*

---

### `RF-CON-13` — Incorporación de operaciones originadas en el sistema de 2012 · Prioridad: **Crítica**

**Descripción.** Mientras una zona o dominio permanezca bajo autoridad del sistema de 2012, la solución **deberá** incorporar a su registro cada operación originada en el legado a través de la fachada, preservando orden, idempotencia y trazabilidad. Los duplicados no deberán producir un segundo efecto y los fallos parciales deberán quedar en una cola recuperable sin pérdida.

**Actor:** solución y sistema de operación de 2012.
**Precondición:** convivencia activa e interfaz de lectura, eventos o extracción incremental confirmada en la puerta de decisión del mes 4.
**Resultado esperado:** el registro nuevo conoce las operaciones nacidas en el legado y puede servir a consumidores comunes sin crear una segunda fuente de verdad.
**Origen:** Decisión N° 1 · CP, Cap. 13.3 y Cap. 17.4 — convivencia y retorno · MC-07 del Maestro de correcciones.
**Criterio de aceptación:** se inyecta una secuencia con eventos duplicados, fuera de orden y una falla parcial; cada operación válida produce un único efecto, el orden de negocio se conserva y la falla se reintenta desde una cola auditable sin pérdida.

---

### `RF-CON-14` — Transferencia de autoridad al cruzar zonas · Prioridad: **Crítica**

**Descripción.** La solución **deberá** mantener una única autoridad de escritura por contenedor, dominio, zona y fase. Cuando un contenedor cruce entre una zona migrada y otra todavía controlada por el sistema de 2012, la transferencia de autoridad **deberá** ejecutarse como un acto trazable y no deberá existir un intervalo con dos fuentes oficiales simultáneas.

**Actor:** solución y supervisor de turno.
**Precondición:** despliegue territorial con zonas en estados de migración distintos.
**Resultado esperado:** cada operación se dirige al registro autoritativo vigente y ambos sistemas reciben la información necesaria para convivencia y retorno.
**Origen:** Decisión N° 1 — despliegue por zonas · BA, Art. 17.2 — prohibición de dos fuentes de verdad · MC-08 del Maestro de correcciones.
**Criterio de aceptación:** se prueban cruces migrada→no migrada y no migrada→migrada, incluyendo reintento y caída de una contraparte; en todos los casos existe una sola autoridad, no se duplica el movimiento y la bitácora identifica autoridad anterior, nueva, instante y responsable.

---

## 3. Dominio `RF-GAT` — Gate, citas, documentación y pesaje
 
**Etapa 1 · 16 requerimientos.** Sostienen los criterios de aceptación 1, 2, 3 y 4, y atacan los indicadores de estadía (78 min), fila máxima (3,2 km), documentación defectuosa (22 %) y discrepancia de masa bruta (6 %).
 
---
 
### `RF-GAT-01` — Solicitud de cita de camión · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir a una empresa de transporte solicitar, modificar y cancelar una cita de camión por autoservicio, indicando franja horaria, contenedor u operación y conductor asignado.
 
**Actor:** empresa de transporte.
**Precondición:** empresa registrada como persona usuaria externa.
**Resultado esperado:** cita registrada con franja confirmada, sin intervención telefónica del terminal.
**Origen:** Decisión N° 6 (citas con prioridad de atención, sin penalización) · CP, 7.3 (sistema de citas: inexistente) · BTT, RT-12.12.
**Criterio de aceptación:** una empresa de transporte completa el ciclo de solicitud, modificación y cancelación por autoservicio, sin contacto telefónico, y la cita queda registrada con su franja.
 
---
 
### `RF-GAT-02` — Prioridad de atención por cita cumplida · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** asignar al camión que llega dentro de su franja de cita una **prioridad de atención** superior a la del camión sin cita o fuera de franja, y **no deberá** aplicar penalización económica por incumplimiento de cita.
 
**Actor:** solución y funcionario de gate.
**Precondición:** camión identificado en la barrera de entrada.
**Resultado esperado:** el camión con cita cumplida se **atiende** en un puesto de gate antes que el que no la tiene; el incumplimiento no genera cobro ni sanción.
**Origen:** Decisión N° 6, que adopta el incentivo en lugar del castigo por la advertencia del CP, 16.1 decisión 6 («una cita penalizada que no puede cumplir hará que nadie use el sistema») · **RN-07** define «cita cumplida»: llegada dentro de la ventana de tolerancia de **30 minutos**, 15 antes y 15 después de la hora asignada.
**Criterio de aceptación:** sobre **200 camiones de cada grupo en franjas comparables**, el tiempo medio de atención del grupo con cita cumplida es **al menos 30 % menor**, y ningún registro de facturación consigna cargo por incumplimiento de cita.
 
> *Correcciones aplicadas: se sustituye «procesamiento» por «atención» (verbo de interpretación múltiple); se fija el diferencial mínimo y el tamaño de muestra; se cita RN-07 para la definición de «cita cumplida».*
 
---
 
### `RF-GAT-03` — Validación anticipada de la documentación · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** validar la documentación del viaje **antes de que el camión salga a la ruta**, mediante el portal de autoatención, y **deberá** informar al solicitante qué documento falla y qué debe corregir.
 
**Actor:** empresa de transporte o agencia de aduana.
**Precondición:** operación declarada en el portal.
**Resultado esperado:** documentación en estado validado o no validado con motivo explícito, antes del despacho del camión.
**Origen:** Decisión N° 7 · CP, Cap. 18, criterio 3 · CP, 7.3 (22 % con documentación incompleta o errónea) · BTT, RT-13.06 (ante error, indicar qué ocurrió y qué hacer).
**Criterio de aceptación:** se envía documentación deliberadamente incompleta y el sistema **no la valida**, identificando el documento faltante y la acción a ejecutar, antes de emitir autorización de viaje.
 
---
 
### `RF-GAT-04` — Derivación a carril de excepción · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** derivar a un **carril de excepción** con atención diferenciada al camión que llegue sin validación previa, y **no deberá** devolverlo en la barrera.
 
**Actor:** funcionario de gate.
**Precondición:** camión sin documentación validada identificado en la barrera.
**Resultado esperado:** camión atendido por el carril de excepción, sin devolución a la vía pública y sin ocupar un puesto del carril validado.
**Origen:** Decisión N° 7 («devolver en barrera a un camión que ya hizo el viaje traslada el problema a la vía pública») · CP, Cap. 4.6.
**Criterio de aceptación:** sobre **100 atenciones de cada tipo**, el tiempo medio del carril de excepción es **al menos 50 % mayor** que el del carril validado, y se acredita que la atención de excepción no bloquea el carril validado.
 
> *Corrección aplicada: el criterio decía «el tiempo es mayor» sin magnitud. La Decisión N° 7 advierte que si el carril de excepción no es claramente peor, se elimina el incentivo para validar antes.*
 
---
 
### `RF-GAT-05` — Reconocimiento automático del código de contenedor · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** reconocer automáticamente el código de identificación del contenedor mediante lectura óptica en la barrera, validando su **dígito verificador** conforme a **ISO 6346**, y **no deberá** requerir digitación manual del código en la operación normal.
 
**Actor:** solución.
**Precondición:** contenedor presente en el punto de lectura.
**Resultado esperado:** código reconocido y validado, asociado a la operación en curso.
**Origen:** CP, Cap. 18, criterio 4 · **CP, Cap. 15, RT-09.01** aporta el umbral de tiempo —reconocimiento no superior a 3 segundos—; la conducta proviene del CP, Cap. 4.6 y Cap. 18 · Decisión N° 2 (lectura óptica en puntos de paso como verificación cruzada) · BTT, RT-17.06 · CP, num. 16.2 (ISO 6346: estructura del código y dígito verificador).
**Criterio de aceptación:** sobre una muestra de **500 contenedores** en condiciones reales de iluminación y suciedad de placa, la tasa de reconocimiento correcto con dígito verificador validado es **≥ 98 %**. El 2 % restante se resuelve por el procedimiento de excepción **sin digitación del código completo**.
 
> *Correcciones aplicadas: se fija la tasa mínima —comprometer 100 % con placa sucia y luz variable sería indemostrable en la recepción— y se nombra ISO 6346, que el CP identifica por su nombre.*
 
---
 
### `RF-GAT-06` — Identificación del camión por patente · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** reconocer automáticamente la patente del camión en la barrera y asociarla a la cita, al conductor declarado y a la operación.
 
**Actor:** solución.
**Precondición:** camión presente en el punto de lectura.
**Resultado esperado:** camión identificado y vinculado a su cita y operación sin digitación.
**Origen:** CP, Cap. 2.3 (los puestos de gate ya cuentan con lectura de patente) · BTT, RT-17.06 · Decisión N° 6.
**Criterio de aceptación:** se acredita que la patente leída se vincula automáticamente a la cita registrada, y que una patente sin cita queda marcada como llegada no anunciada.
 
---
 
### `RF-GAT-07` — Verificación de habilitación del conductor · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** verificar en la barrera que el conductor cuenta con habilitación vigente para ingresar al recinto, y **deberá** registrar su ingreso asociado a la operación y a la zona autorizada.
 
**Actor:** funcionario de gate y solución.
**Precondición:** conductor identificado.
**Resultado esperado:** ingreso autorizado o denegado, con registro del acto y de su motivo.
**Origen:** CP, Cap. 10, restricción no negociable N° 7 (plan de protección portuaria) · CP, Cap. 18, criterio 17 · Decisión N° 13 (registro de quién ingresó, bajo qué habilitación y a qué zona).
**Criterio de aceptación:** un conductor sin habilitación vigente es denegado y el motivo queda registrado; un conductor habilitado ingresa y su registro consigna operación y zona.
 
---
 
### `RF-GAT-08` — Captura y trazado de la verificación de masa bruta · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** capturar la medición de la báscula, asociarla al contenedor y a la operación, y conservarla como registro trazable de verificación de masa bruta. La solución **no deberá** operar ni certificar la báscula.
 
**Actor:** solución.
**Precondición:** pesaje ejecutado en la báscula del gate.
**Resultado esperado:** medición registrada, trazable hasta el instrumento y el instante de captura.
**Origen:** CP, Cap. 11, exclusión 8 («no se pide operar la báscula ni certificarla metrológicamente; sí capturar y trazar su medición») · CP, Cap. 12, materia 5 (SOLAS VGM) · BTT, RT-17.06 · **CP, Cap. 15, RT-05.10** (retención de registros de verificación de masa bruta: 5 años).
**Criterio de aceptación:** se audita una muestra de mediciones contra la evidencia física de pesaje, verificando trazabilidad completa hasta el instrumento.
 
---
 
### `RF-GAT-09` — Gestión de discrepancia de masa bruta sobre tolerancia · Prioridad: **Alta**
 
**Descripción.** Cuando la diferencia entre la masa declarada y la verificada supere el **5 % del peso declarado**, la solución **deberá** detener el avance de la operación, notificar al embarcador y **marcar el plan de estiba afectado como sujeto a replanificación**.
 
**Actor:** solución, embarcador y planificador.
**Precondición:** medición capturada (`RF-GAT-08`) y masa declarada disponible.
**Resultado esperado:** operación detenida, embarcador notificado y plan de estiba marcado, antes de que el contenedor se embarque con el peso equivocado.
**Origen:** **RN-05** fija la tolerancia en 5 % del peso declarado · CP, Cap. 4.6 (la discrepancia obliga a rehacer parte del plan de estiba «porque la estabilidad de la nave se calculó con el peso equivocado») · CP, 7.3 (6 % sobre tolerancia, referencia bajo 1 %) · CP, Cap. 12, materia 5.
 
**Ejemplos numéricos del cálculo:**
 
> **Ejemplo A — dentro de tolerancia.** Peso declarado 24.000 kg; verificado 24.900 kg. Diferencia 900 kg = **3,75 %** del declarado. **No hay discrepancia**; la operación continúa.
>
> **Ejemplo B — sobre tolerancia.** Peso declarado 24.000 kg; verificado 25.400 kg. Diferencia 1.400 kg = **5,83 %** del declarado. **Hay discrepancia**: la operación se detiene, se notifica al embarcador y el plan afectado se marca para replanificación conforme a `RF-NAV-14`.
>
> El porcentaje se calcula siempre sobre el peso **declarado**, no sobre el verificado.
 
**Criterio de aceptación:** se inyectan los dos casos anteriores y se acredita que el primero continúa y el segundo detiene la operación, con notificación al embarcador con marca de tiempo y marca de replanificación sobre el plan correspondiente.
 
> *Correcciones aplicadas: se incorpora el umbral de RN-05 y los dos ejemplos numéricos que el material de redacción exige para todo requisito que especifique un cálculo.*
 
---
 
### `RF-GAT-10` — Emisión de la instrucción de destino · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** emitir al conductor la instrucción de destino dentro del recinto, derivada de la asignación de posición vigente, en el momento del despacho en la barrera.
 
**Actor:** solución y conductor.
**Precondición:** documentación validada, contenedor reconocido y pesaje resuelto cuando corresponda.
**Resultado esperado:** instrucción de destino entregada, con el bloque y la posición asignados.
**Origen:** CP, Cap. 4.6 · Decisión N° 3 (el algoritmo asigna la posición) · **CP, Cap. 15, RT-09.01** aporta el umbral de tiempo agregado del gate —no superior a 120 segundos—, que se verifica en RNF-DES-01.
**Criterio de aceptación:** la instrucción emitida corresponde a la asignación vigente de `RF-PAT-06` en el **100 % de una muestra de 200 despachos**.
 
> *Corrección aplicada: el criterio anterior medía el tiempo agregado gate→instrucción, que depende de otros cinco requerimientos y no localiza el defecto. El tiempo agregado pertenece a RNF-DES-01.*
 
---
 
### `RF-GAT-11` — Registro de los eventos de entrada y de salida · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar el cruce de la barrera de entrada y el de la barrera de salida como **eventos discretos con marca de tiempo**, generados automáticamente en el momento en que ocurren.
 
**Actor:** solución.
**Precondición:** camión en el punto de control.
**Resultado esperado:** dos eventos por viaje, con instante propio y sin captura manual.
**Origen:** CP, Anexo C (la estadía se mide «desde la barrera de entrada hasta la de salida») · CP, Cap. 10, restricción no negociable N° 14.
**Criterio de aceptación:** sobre un turno completo, cada viaje registrado presenta exactamente un evento de entrada y uno de salida, ambos con marca de tiempo generada por el sistema.
 
---
 
### `RF-GAT-12` — Cálculo trazable de la estadía del camión · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** calcular la estadía de cada camión a partir de los eventos de `RF-GAT-11`, y **deberá** permitir descender desde el indicador consolidado hasta los dos eventos que lo componen.
 
**Actor:** solución y CLIENTE.
**Precondición:** eventos de entrada y salida registrados.
**Resultado esperado:** indicador de estadía consolidado, auditable hasta el viaje individual.
**Origen:** CP, Cap. 18, criterio 1 · CP, Cap. 10, restricción no negociable N° 14 · BTT, RT-05.26 · **CP, Cap. 15, RT-05.29** aporta el umbral de consolidación —no superior a 1 hora tras el cierre del turno—.
**Criterio de aceptación:** se selecciona un valor consolidado del indicador y se desciende hasta la lista de viajes que lo componen y, desde uno de ellos, hasta sus dos eventos de barrera.
 
---
 
### `RF-GAT-13` — Publicación del estado de congestión del acceso · Prioridad: **Media**
 
**Descripción.** La solución **deberá** publicar en capa pública, sin autenticación, el estado de congestión del acceso vial y la disponibilidad de franjas de cita.
 
**Actor:** empresa de transporte y conductor.
**Precondición:** ninguna.
**Resultado esperado:** información disponible para decidir el momento de salida antes de iniciar el viaje.
**Origen:** BTT, RT-16.31 (portal público) · CP, Cap. 15, RT-16.30 · CP, Cap. 18, criterio 2 · Decisión N° 6.
**Criterio de aceptación:** se accede sin credenciales al estado de congestión y a la disponibilidad de franjas, y se verifica que el dato refleja la situación con el desfase declarado en RNF-DES-06.
 
---
 
### `RF-GAT-14` — Operación del gate sin enlace exterior · Prioridad: **Crítica**
 
**Descripción.** El componente on-premise **deberá** sostener la operación completa del gate —validación, reconocimiento, pesaje, emisión de instrucción y registro de eventos— durante **al menos 72 horas continuas** sin enlace hacia el exterior, sin perder ningún registro.
 
**Actor:** solución.
**Precondición:** enlace exterior no disponible.
**Resultado esperado:** gate operando y registrando localmente; ningún evento perdido al restablecerse el enlace.
**Origen:** CP, Cap. 10, restricción no negociable N° 4 · **CP, Cap. 15, RT-03.10** endurece el umbral transversal de 24 a **72 horas**; prevalece el más exigente conforme al encabezado del Cap. 15 · BTT, RT-03.11.
**Criterio de aceptación:** simulacro de corte de enlace de 72 horas, verificando operación completa de las cinco funciones del gate y ausencia de pérdida de registros al reconectar. Se articula con RNF-DIS-02.
 
> **Relación con `RF-OPD-01`.** Este requerimiento especifica la operación desconectada **del gate**, con su duración propia. `RF-OPD-01` cubre la operación desconectada del terminal completo. No se duplican: `RF-OPD-01` remite a este para el gate.
 
---
 
### `RF-GAT-15` — Conciliación de gate con umbral cero · Prioridad: **Crítica**
 
**Descripción.** Mientras el gate esté en convivencia, la solución **deberá** conciliar al cierre de cada día las entradas y salidas contra el registro del sistema de 2012, y **no deberá** admitir ninguna diferencia no explicada al cierre diario.
 
**Actor:** solución y supervisor.
**Precondición:** dominio de gate en convivencia con escritura dual activa.
**Resultado esperado:** cero diferencias no explicadas al cierre diario; cada diferencia investigada dentro de la ventana de **24 horas**.
**Origen:** Decisión N° 1, resolución del umbral de gate: cero diferencias no explicadas, por tratarse de eventos discretos que alimentan un indicador con consecuencia contractual · CP, Cap. 10, restricción no negociable N° 14 · CP, 7.1 (tres semestres consecutivos sobre el umbral de estadía).
**Criterio de aceptación:** durante siete días consecutivos, el informe de conciliación diaria del gate cierra con cero diferencias no explicadas, o con cada diferencia clasificada y explicada dentro de las 24 horas conforme a la definición operativa de `RF-CON-06`.
 
> **Jerarquía con `RF-CON-05`.** La conciliación por turno de `RF-CON-05` opera con umbral de alerta; este requerimiento fija el **cierre diario con umbral cero**. Son controles encadenados, no frecuencias en conflicto.
 
---
 
### `RF-GAT-16` — Límite de franjas ofrecidas por capacidad declarada · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** limitar el número de citas ofrecidas por franja horaria a la **capacidad de atención declarada** de los puestos de gate vigentes, y **deberá** dejar trazable el parámetro de capacidad aplicado a cada franja.
 
**Actor:** solución.
**Precondición:** parámetro de capacidad por franja configurado.
**Resultado esperado:** la oferta de citas no excede la capacidad de atención; el parámetro es auditable a posteriori.
**Origen:** CP, Cap. 18, criterio 2 · CP, 7.3 (fila máxima 3,2 km y 140 camiones) · Decisión N° 6 · BTT, RT-16.02 (parametrización con versionado y registro de quién cambió qué) · BTT, RT-16.04.
**Criterio de aceptación:** se intenta agendar una cita en una franja saturada y el sistema no la acepta, ofreciendo la franja disponible más próxima; se recupera para una franja pasada el parámetro de capacidad que estuvo vigente al momento de agendar.
 
> *Requerimiento nuevo. Sin control de capacidad, las citas ordenan la llegada pero no la acotan: la evidencia de Vancouver muestra que un sistema de citas con alto cumplimiento no redujo el tiempo de atención, porque las citas no crean capacidad.*
 
---
 
## 4. Trazabilidad de la parte 1
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos |
|---|---|
| 1 — Estadía del camión auditable | `RF-GAT-01` a `04`, `10`, `11`, `12`, `15`, `16` · `RF-CON-11` |
| 2 — Sin fila que desborde a vía pública | `RF-GAT-01`, `02`, `03`, `13`, `16` |
| 3 — Documentación validada antes de la ruta | `RF-GAT-03`, `04` |
| 4 — Reconocimiento automático en gate | `RF-GAT-05` |
| 18 — 72 h sin enlace *(parcial: gate)* | `RF-GAT-14` |
| 20 — Indicadores del concedente trazables | `RF-CON-11` · `RF-GAT-11`, `12`, `15` |
 
| Indicador de línea base | Meta | Requerimientos |
|---|---|---|
| Estadía del camión 78 min | 45 min | `RF-GAT-01` a `05`, `10`, `16` |
| Fila máxima 3,2 km | cero | `RF-GAT-01`, `02`, `13`, `16` |
| Documentación defectuosa 22 % | bajo 5 % | `RF-GAT-03`, `04` |
| Discrepancia de masa bruta 6 % | bajo 1 % | `RF-GAT-08`, `09` |
| Sistema de citas: inexistente | operativo | `RF-GAT-01`, `02`, `16` |
| Lectura automática: inexistente | **≥ 98 %** | `RF-GAT-05`, `06` |
| Semestres sobre el umbral 3 | cero | `RF-GAT-12`, `15` |
 
**Total de la parte 1: 30 requerimientos** — 14 en `RF-CON`, 16 en `RF-GAT`. Ninguno en revisión.
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*
