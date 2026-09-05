# Correcciones de la Fase 4 — Dominio `RF-TRA`, particiones y metas con evidencia
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Origen:** correcciones 5 a 8 del plan de Fase 4. Cierra la Fase 4.
> **Estado:** propuestas de Célula 2. La sección 5 modifica metas ya declaradas y **requiere ratificación de la célula**.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Sección | Contenido | Por qué está aquí |
|---|---|---|
| **1** | **Dominio nuevo `RF-TRA` — tractocamiones de patio** | 6 requerimientos. Era la omisión de cobertura más costosa del catálogo: 42 equipos, la primera causa de la brecha de productividad, y una petición literal de un entrevistado |
| **2** | **`RF-GAT-16` — control de capacidad de franjas de cita** | El mecanismo por el que un sistema de citas evita la fila. Sin él, las citas ordenan la llegada pero no la acotan |
| **3** | Partición de `RF-ACC-06` y `RF-NAV-09` | Los dos casos del catálogo con dos pruebas genuinamente independientes |
| **4** | Ejemplo numérico de `RF-REF-13` | Cierra el tercero de los tres cálculos, con la decisión RN-10 ya tomada |
| **5** | **Metas 1, 2, 3 y 4 reescritas con evidencia publicada** | Incluye la evidencia que nos es adversa. Dos metas cambian de valor y una cambia de justificación completa |
| **6** | Conteo final y estado de la Fase 4 | Qué queda para la Fase 5 |
 
---
 
## 1. Dominio `RF-TRA` — Tractocamiones de patio
 
### 1.1 Por qué faltaba y por qué es grave
 
El catálogo cubría grúas de muelle, grúas de patio, gate, refrigerado, nave, integraciones, facturación, portal, acceso, desconexión, inspecciones y emisiones. **No cubría los 42 tractocamiones que mueven cada contenedor entre el muelle y el patio.**
 
No es una omisión menor. La evidencia del caso:
 
| Evidencia | Fuente |
|---|---|
| «La grúa se detiene esperando el tractocamión» — es la **primera** de las tres causas que el caso da para la brecha entre 24,8 y 30 movimientos por hora | CP, Cap. 4.3 |
| «Los tractocamiones no tienen posicionamiento satelital. Su ubicación exacta en cada momento es **conocimiento del supervisor, no del sistema**» | CP, Cap. 4.3 |
| «El supervisor asigna los tractocamiones **por radio**» | CP, Cap. 4.3 |
| El operador de grúa pide explícitamente «saber que el tractocamión que estoy esperando viene en camino y en cuánto» | CP, Cap. 8, entrevista |
| 42 tractocamiones, y hasta 88 equipos móviles a instrumentar en la proyección a tres años | CP, Cap. 2.3 y 14.1 |
| Criterio de aceptación 6: la productividad de grúa **alcanza** el valor exigido | CP, Cap. 18 |
 
El catálogo tenía requerimientos para **medir** la productividad (`RF-NAV-12`) y para **explicar** el sobretiempo (`RF-NAV-13`), pero ninguno que atacara su primera causa. Medir un indicador no lo mueve.
 
### 1.2 Los requerimientos
 
Etapa 1. Seis requerimientos.
 
---
 
**`RF-TRA-01` — Posicionamiento de los tractocamiones** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** conocer la posición de cada tractocamión de patio mediante posicionamiento automático del equipo, sin depender de la comunicación por radio con el supervisor.
**Actor:** solución. **Precondición:** tractocamión instrumentado y en operación.
**Resultado esperado:** posición de los 42 equipos conocida por el sistema, no solo por el supervisor.
**Origen:** CP, Cap. 4.3 («su ubicación exacta en cada momento es conocimiento del supervisor, no del sistema») · CP, Cap. 14.1 (42 tractocamiones, hasta 88 equipos móviles a instrumentar) · Decisión N° 2, que adopta el posicionamiento automático del equipo como fuente primaria.
**Criterio de aceptación:** sobre una muestra de **50 posiciones observadas físicamente**, la posición registrada coincide con la real dentro de la tolerancia declarada para el patio, en el **95 %** de los casos.
 
---
 
**`RF-TRA-02` — Asignación de tractocamión a movimiento de grúa** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** asignar automáticamente un tractocamión a cada movimiento de grúa de muelle, considerando la posición del equipo, su estado de ocupación y la secuencia del plan de estiba vigente. La solución **no deberá** requerir que la asignación se comunique por radio.
**Actor:** solución y supervisor de turno. **Precondición:** plan de estiba publicado y equipos posicionados.
**Resultado esperado:** cada movimiento tiene equipo asignado antes de que la grúa lo requiera.
**Origen:** CP, Cap. 4.3 («el supervisor asigna los tractocamiones por radio») · CP, Cap. 5 (la radio debe dejar de ser sistema de registro) · CP, Cap. 18, criterio 6.
**Criterio de aceptación:** sobre un turno completo de operación de nave, el **100 %** de los movimientos ejecutados tiene un tractocamión asignado por el sistema con anterioridad al movimiento, y la asignación consta con su instante.
 
---
 
**`RF-TRA-03` — Tiempo estimado de arribo del tractocamión a la grúa** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** presentar al operador de grúa de muelle, en la pantalla de cabina, el **tiempo estimado de arribo** del tractocamión asignado a su próximo movimiento, mediante indicación visual y sin exigir acción alguna del operador.
**Actor:** operador de grúa de muelle. **Precondición:** tractocamión asignado (`RF-TRA-02`) y posicionado (`RF-TRA-01`).
**Resultado esperado:** el operador anticipa la espera en vez de descubrirla.
**Origen:** CP, Cap. 8, petición literal del operador de grúa: «saber que el tractocamión que estoy esperando viene en camino y en cuánto» · CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 18, criterio 21 · Decisión N° 14, que fija el modo de presentación en cabina.
**Criterio de aceptación:** el tiempo estimado se presenta en cabina para el **100 %** de los movimientos asignados, y su error medio respecto del arribo real no supera **60 segundos**, medido sobre **200 movimientos**.
 
---
 
**`RF-TRA-04` — Registro de la detención de grúa por espera de equipo** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** registrar como evento propio cada detención de grúa de muelle atribuible a espera de tractocamión, con su inicio, su término y el equipo involucrado.
**Actor:** solución. **Precondición:** grúa en operación con movimiento pendiente y sin tractocamión disponible en posición.
**Resultado esperado:** la primera causa de la brecha de productividad queda cuantificada, no supuesta.
**Origen:** CP, Cap. 4.3, que identifica esta espera como causa de la brecha · CP, 7.1 («capacidad de explicar a la naviera la causa de un sobretiempo de nave: inexistente») · articula con `RF-NAV-13`.
**Criterio de aceptación:** para una recalada cerrada, la suma de las detenciones registradas por causa reconcilia con la diferencia entre el tiempo total de atención y el tiempo de operación efectiva, **sin residuo no clasificado superior al 5 %**.
 
---
 
**`RF-TRA-05` — Reasignación ante indisponibilidad del equipo** · Prioridad: **Alta**
 
**Descripción.** Cuando un tractocamión asignado quede indisponible, la solución **deberá** reasignar el movimiento a otro equipo y **deberá** actualizar el tiempo estimado de arribo en la cabina afectada.
**Actor:** solución. **Precondición:** equipo asignado que deja de estar disponible.
**Resultado esperado:** la indisponibilidad no se traduce en una espera indefinida ni en una llamada por radio.
**Origen:** CP, Cap. 4.3 · Decisión N° 5, catálogo de condiciones dinámicas, que ya permite declarar un equipo no disponible.
**Criterio de aceptación:** se declara un equipo no disponible durante una operación y se verifica que el movimiento se reasigna y que la cabina refleja el nuevo tiempo estimado, **en no más de 30 segundos** desde la declaración.
 
---
 
**`RF-TRA-06` — Registro de movimientos del tractocamión** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** registrar cada traslado ejecutado por un tractocamión, con origen, destino, contenedor e instantes, derivado de la telemetría del equipo y sin confirmación activa del conductor.
**Actor:** solución. **Precondición:** tractocamión instrumentado ejecutando un traslado.
**Resultado esperado:** el ciclo completo del contenedor entre muelle y patio queda trazado.
**Origen:** Decisión N° 15 (evidencia de movimiento sin confirmación) · CP, Cap. 10, restricción no negociable N° 1 · articula con `RF-PAT-05`.
**Criterio de aceptación:** sobre una muestra de **100 traslados observados**, el 100 % queda registrado con origen, destino y contenedor correctos, sin acción del conductor.
 
---
 
### 1.3 Consecuencia sobre la especificación de hardware
 
El dominio agrega equipos al universo a instrumentar que el catálogo declaraba. `RF-PAT-13` comprometía «18 de 18 equipos»; con este dominio el universo real es mayor.
 
**Corrección a `RF-PAT-13` y a la meta del indicador correspondiente:** el universo de instrumentación se declara explícitamente como **18 grúas de patio + 42 tractocamiones + 14 equipos de manipulación pesada = 74 equipos**, con proyección a **88** conforme al CP, Cap. 14.1. La meta del indicador «equipos de patio con terminal montada», hoy declarada como 18 de 18, pasa a **74 de 74 al cierre del desarrollo de la Etapa 1**.
 
Esto refuerza el pendiente de coordinación con Célula 3 sobre la especificación de hardware que el CP, Cap. 11 exclusión 9 nos obliga a producir.
 
---
 
## 2. `RF-GAT-16` — Control de capacidad de franjas de cita
 
**Por qué falta.** El criterio de aceptación 2 exige que no vuelva a formarse una fila que desborde a la vía pública. El catálogo lo sostenía con la cita, la validación documental y la publicación de congestión. Pero **ningún requerimiento limitaba cuántas citas se ofrecen por hora contra la capacidad real del gate**. Sin ese control, las citas ordenan la llegada pero no la acotan: si se ofrecen más citas de las que el gate puede atender, la fila se forma igual, solo que con hora asignada.
 
La evidencia publicada lo confirma: en Vancouver, con un sistema obligatorio y 85 a 95 % de cumplimiento, no se observó reducción del tiempo de atención (Davies, 2009). Las citas no crean capacidad.
 
---
 
**`RF-GAT-16` — Límite de franjas ofrecidas por capacidad declarada** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** limitar el número de citas ofrecidas por franja horaria a la capacidad de atención declarada de los puestos de gate vigentes, y **deberá** dejar trazable el parámetro de capacidad aplicado a cada franja.
**Actor:** solución. **Precondición:** parámetro de capacidad por franja configurado.
**Resultado esperado:** la oferta de citas no excede la capacidad de atención; el parámetro es auditable a posteriori.
**Origen:** CP, Cap. 18, criterio 2 · CP, 7.3 (fila máxima 3,2 km y 140 camiones) · Decisión N° 6 · **BTT, RT-16.02** (parametrización con versionado y registro de quién cambió qué) · **BTT, RT-16.04** (declaración de frontera parametrizable).
**Criterio de aceptación:** se intenta agendar una cita en una franja saturada y el sistema la rechaza ofreciendo la franja disponible más próxima; se recupera para una franja pasada el parámetro de capacidad que estuvo vigente al momento de agendar.
 
---
 
## 3. Partición de los dos requerimientos con doble prueba
 
La regla ratificada es que **la unidad de un requisito es la unidad de su prueba**. Estos dos tienen dos pruebas que pueden fallar de forma independiente.
 
### 3.1 `RF-ACC-06` se parte en dos
 
| Antes | Después |
|---|---|
| Registrar ingreso y salida por zona **y** reconstruir la nómina de presentes en cualquier instante | **`RF-ACC-06`** — registro del evento de ingreso y de salida por zona, con identidad, habilitación e instante. *Criterio: sobre un turno de peak, cada tránsito por un punto de control genera su evento.* |
| | **`RF-ACC-11`** — reconstrucción de la nómina de personas presentes por zona en cualquier instante del turno. *Criterio: se solicita la nómina para tres instantes distintos de un turno pasado y se contrasta contra los eventos registrados.* |
 
Se puede registrar correctamente y reconstruir mal —por un defecto de consulta o de manejo de zonas— y viceversa. Son dos pruebas.
 
### 3.2 `RF-NAV-09` se parte en dos
 
Es el caso que la revisión señaló como más problemático: el propio requerimiento admitía que «el entregable no es software: es el registro», lo que bajo nuestro criterio lo convierte en proceso, no en funcional.
 
| Antes | Después |
|---|---|
| Mantener el registro de reglas del planificador **y** producir su primera versión antes del hito H2 | **`RF-NAV-09`** — la solución **deberá** mantener el registro de reglas, restricciones y casos del planificador, editable, versionado y consumible por el motor de propuesta. *Criterio: se registra una regla nueva y se acredita que la siguiente corrida del motor la aplica.* Es conducta del sistema |
| | **Entregable de proyecto EP-01** — primera versión del registro antes del hito H2 (mes 4), versión validada con el planificador antes del cierre de desarrollo de la Etapa 1 (mes 12). **Sale del catálogo de RF** y pasa a la EDT del Informe 2, manteniendo su trazabilidad al criterio de aceptación 22 |
 
El compromiso no se pierde: cambia de instrumento. Un entregable documental con fecha comprometida pertenece al plan de trabajo, no al catálogo funcional — y el CP, Cap. 17.1 no exige que todo compromiso viva en el catálogo de RF.
 
---
 
## 4. Ejemplo numérico de `RF-REF-13`
 
Con RN-10 resuelta —se factura el **tiempo conectado efectivo**— el tercer cálculo queda cerrado.
 
> **Ejemplo A — conexión continua.** Contenedor conectado el 12 de enero a las 06:00, desconectado el 14 de enero a las 18:00. Sin interrupciones registradas.
> Tiempo conectado: **60 horas**. **Horas facturables: 60.**
>
> **Ejemplo B — con desconexión intermedia registrada.** Contenedor conectado el 12 de enero a las 06:00. La instrumentación registra desconexión el 13 de enero de 02:15 a 05:45 —3 horas 30 minutos— por falla del tablero. Desconectado definitivamente el 14 de enero a las 18:00.
> Tiempo de permanencia en la toma: 60 horas. Tiempo desconectado registrado: 3,5 horas. **Horas facturables: 56,5.**
>
> El tiempo desconectado se descuenta con independencia de la causa, incluida la falla atribuible al terminal. El descuento se deriva de los eventos de `RF-REF-05` y `RF-REF-06`, no de una declaración manual.
 
---
 
## 5. Metas reescritas con evidencia publicada
 
> **Cambio de estado.** Las metas 1 y 4 cambian de fundamento; la 2 cambia de valor y se condiciona; la 3 cambia de naturaleza. Las siete restantes del complemento original se mantienen sin cambio.
>
> Se incorpora la evidencia **adversa** además de la favorable, conforme al CP, Cap. 16.2, que exige investigación sectorial real y penaliza la evidencia seleccionada a conveniencia.
 
### 5.1 Meta 1 — Remociones: se mantiene en ≤ 14 %, con fundamento nuevo y una advertencia
 
**Fundamento anterior:** una cifra de proveedor (rango de 10 a 25 % de reducción) no verificada de forma independiente.
 
**Fundamento nuevo, arbitrado:**
 
- Bütün et al. (2026), *Sustainability* — 30 instancias reales del **Vigo Container Terminal**, terminal convencional español, el caso más comparable al nuestro: reducción de movimientos improductivos de aproximadamente **74 %** mediante optimización multiobjetivo.
- Kim y Yi (2021), *Maritime Economics & Logistics* — más de 200.000 contenedores reales en Busan durante 8 meses: reducción del **98 %** en el número de remociones por operación de retiro. **Con la salvedad de que se logra combinando la asignación con información anticipada de retiro** —distribución de permanencia, aviso de despacho, cita del camión y posición del camión en tiempo real— y no con la asignación algorítmica por sí sola.
**Advertencia adversa que debe declararse:**
 
- Zając (2026), *Applied Sciences* — bajo condiciones de carga alta, la regla simple FIFO **superó** a las estrategias de agrupamiento sofisticadas en intensidad de remoción y consumo energético. **Nuestro patio opera al 90 % de ocupación en peak.**
- Saurí y Martín (2011), *Transportation Research Part E* — no existe estrategia de apilamiento dominante universal; la óptima depende de la altura de pila y de la relación entre frecuencia de recalada y tiempo de permanencia.
**Advertencia de comparabilidad:** la literatura mide remociones **por retiro** (típicamente entre 0,5 y 2,5 según altura de pila), no como **porcentaje del total de movimientos de patio**, que es la métrica del caso. **La línea base de 18 % no es contrastable contra ninguna fuente publicada.**
 
**Meta ratificada: ≤ 14 %**, con tres declaraciones nuevas: la reducción de 22 % es conservadora frente a la evidencia; **depende de que la información anticipada de retiro esté disponible**, lo que ata esta meta al éxito del sistema de citas; y su eficacia se degrada con la ocupación, por lo que se compromete **medida fuera del peak estacional**, con el desempeño en peak reportado por separado.
 
### 5.2 Meta 2 — Inspecciones: baja de ≤ 8 % a ≤ 12 %, y se condiciona
 
**Evidencia encontrada: ninguna directa.** No existe literatura arbitrada que mida el porcentaje de inspecciones atrasadas por indisponibilidad del contenedor, ni que evalúe la programación anticipada de remociones para inspecciones de autoridad.
 
**Lo que sí valida el mecanismo, por analogía:**
 
- Zweers, Bhulai y van der Mei (2020), *Computers & Operations Research* — formaliza exactamente el mecanismo: «si la grúa está ociosa durante algún tiempo, puede ser más eficiente ejecutar movimientos de preprocesamiento para reducir el número de reubicaciones futuras».
- Azab y Morita (2022), *Transportation Research Part E* — caso real de terminal japonés: coordinar proactivamente las citas con el manejo de contenedores evita demoras causadas por reubicaciones.
**Evidencia adversa que obliga a bajar la meta:**
 
- Klar et al. (2024), *IEEE OJ-ITS* — documenta el trade-off real: **en la práctica las citas se posponen para minimizar remociones**, y cumplir la agenda exige una ponderación explícita que sacrifica remociones. **Cumplir esta meta consume capacidad de grúa que compite con la meta 1.**
- Hoffmann et al. (2021), *World Customs Journal*, y Nguvumali et al. (2025) — el determinante principal del atraso suele ser la coordinación con la autoridad —avisos, ventanas, presencia del inspector—, **fuera del control del terminal**.
**Meta corregida: ≤ 12 %**, no ≤ 8 %, **condicionada** a que el plazo de aviso de cada autoridad, hoy no declarado, resulte compatible con el tiempo de ejecución de la remoción anticipada. Se declara expresamente que la parte del atraso atribuible a la coordinación de la autoridad no está bajo control de la solución, y que el compromiso se revisará al cerrar el levantamiento de los meses 1 a 4.
 
Bajar la meta es la decisión correcta: comprometer ≤ 8 % sin evidencia y con un trade-off documentado contra otra meta propia es exactamente lo que el material de redacción describe como regalar la recepción.
 
### 5.3 Meta 3 — Posición: se mantiene en ≤ 0,5 %, pero cambia de naturaleza
 
**Evidencia disponible:**
 
- Götting KG (2013), documentación de fabricante — sistema DGPS montado sobre **RTG**, el mismo tipo de equipo del caso: exactitud «hasta ±30 cm» con corrección diferencial, frente a aproximadamente 10 m sin ella. El propio fabricante escalona los códigos de exactitud, reconociendo que ±30 cm es el mejor caso y no el operativo típico.
**Evidencia adversa, arbitrada:**
 
- Dahiya et al. (2026), *Applied Sciences* — «el posicionamiento de apiladores basado en RTK-GPS frecuentemente carece de precisión… aunque ofrece precisión de colocación de hasta 3 cm, esto sigue siendo insuficiente». La causa es la **orientación angular** del contenedor en el spreader, no el error de posición. **Mejorar el GNSS no resuelve por sí solo el error de colocación.**
**No existe ninguna fuente, arbitrada o de fabricante, que cuantifique el porcentaje de contenedores mal ubicados en un patio**, ni antes ni después de instalar posicionamiento automático. Ni la línea base de 3,1 % ni el objetivo de 0,5 % son contrastables.
 
**Meta ratificada: ≤ 0,5 %**, con dos declaraciones: es **estimación propia derivada del umbral de conciliación de la Decisión N° 1**, no de evidencia externa; y **el posicionamiento automático por sí solo no la alcanza** — la meta depende de la verificación cruzada por lectura óptica de `RF-PAT-02` y del ciclo de tarea de verificación de `RF-PAT-04`, que es lo que corrige el error de orientación que Dahiya et al. documentan.
 
Esto refuerza la Decisión N° 2, que ya había adoptado el modelo combinado en vez del posicionamiento solo.
 
### 5.4 Meta 4 — Refrigerado: cambia de justificación por completo
 
**Este es el cambio más importante de la sección.** La meta era «detección ≤ 5 minutos» frente a una ronda cada 4 horas, presentada como corrección de una deficiencia.
 
**Evidencia que desmonta esa justificación:**
 
- West of England P&I Club, boletín de prevención de pérdidas — el estándar de la industria aseguradora es que la unidad refrigerada sea revisada «al menos 4 veces cada 24 horas», es decir **cada 6 horas**. **La ronda cada 4 horas del terminal ya supera ese estándar.** La meta no corrige un incumplimiento.
- Kan et al. (2020), *International Journal of Refrigeration* — el ascenso de temperatura de la carga ante falla de refrigeración es **gradual y desigual según la posición en la estiba**. La constante de tiempo térmica se mide en horas. **El beneficio marginal de detectar en 5 minutos frente a 30 es probablemente nulo para el desenlace de la carga.**
- Castelein, Geerlings y Van Duin (2020), *Journal of Cleaner Production* — la pérdida de carga ocurre «no solo por fallas técnicas, sino con igual frecuencia por **errores organizacionales**, especialmente por riesgo de retención en los puntos de transferencia».
- Kaptan et al. (2023) — las causas raíz principales son tiempo excesivo sin energía, **condiciones de precarga inadecuadas** y fallas de refrigerante. Solo la primera se mitiga con detección rápida.
**Evidencia favorable:**
 
- Cil, Abdurahman y Cil (2022), *Journal of Shipping and Trade* — la latencia extremo a extremo de un sistema IoT de monitoreo reefer se estabiliza en **0,015 segundos**. El umbral de 5 minutos es trivialmente alcanzable; de hecho es poco exigente para la tecnología.
**Meta reformulada.** El umbral de ≤ 5 minutos **se mantiene** —lo exige el CP, Cap. 15, RT-05.29 y no es discutible— pero **deja de presentarse como el beneficio**. El beneficio comprometido pasa a ser:
 
| Compromiso | Valor |
|---|---|
| Cobertura de instrumentación | **100 %** de las 2.400 tomas y los 26 tableros |
| Serie continua de temperatura entregable | **100 %** de los contenedores refrigerados, retención 5 años |
| Detección de desconexión sin esperar la desviación térmica | Sí — `RF-REF-05` |
| Detección de falla de tablero como evento propio | Sí — `RF-REF-06` |
| Latencia de alarma | ≤ 5 minutos, conforme a RT-05.29 |
 
La justificación correcta no es «detectamos más rápido» sino **«no existe ventana ciega, y existe evidencia entregable»**. El evento del 18 de febrero no ocurrió porque la ronda fuera lenta: ocurrió porque **falló un tablero completo de madrugada y nadie pasó caminando**. Lo que lo evita es la cobertura permanente y la alarma escalada con confirmación, no el umbral en minutos.
 
### 5.5 Estado de las 17 metas
 
| Estado | Metas |
|---|---|
| Sin cambio | 7 de las 11 originales, más las 6 incorporadas en la corrección 1 |
| Fundamento reemplazado por evidencia arbitrada | Meta 1 (remociones), meta 4 (refrigerado) |
| **Valor corregido a la baja** | Meta 2 (inspecciones): de ≤ 8 % a **≤ 12 %**, condicionada |
| Naturaleza precisada | Meta 3 (posición): estimación propia declarada, dependiente de la verificación cruzada |
| **Valor corregido al alza** | Instrumentación de equipos: de 18 a **74 equipos** (sección 1.3) |
 
---
 
## 6. Conteo final y estado de la Fase 4
 
| Concepto | Requerimientos |
|---|---:|
| Catálogo tras las correcciones 1 y 2 | 128 |
| `RF-CON-12` — frontera parametrizable (corrección 3) | +1 |
| Dominio `RF-TRA` | +6 |
| `RF-GAT-16` — capacidad de franjas | +1 |
| Partición de `RF-ACC-06` → `RF-ACC-11` | +1 |
| `RF-NAV-09` se parte: la mitad documental sale a la EDT | 0 |
| **Total** | **137** |
| Si Isidora aprueba eliminar `RF-OPD-03` y `RF-OPD-04` | **135** |
 
Trece dominios. El catálogo cierra entre **135 y 137 requerimientos**, dentro del rango que estimé al detectar los hallazgos.
 
### 6.1 Fase 4: cerrada
 
Las ocho correcciones están propuestas. Quedan tres cosas fuera de nuestro control inmediato:
 
| # | Pendiente | De quién |
|---:|---|---|
| 1 | Cuatro decisiones sobre los duplicados con el catálogo de RNF | **Isidora** |
| 2 | Ratificación de las metas 2 y 4 reescritas, y del supuesto de `RF-PAT-10` | **Célula** |
| 3 | RN-09, corrección del fundamento de RN-03 y RN-10 | **Isidora** |
 
### 6.2 Lo que habilita la Fase 5
 
- Asignación consolidada Etapa 1 / Etapa 2, insumo de las secciones 3.4 a 3.6 del Subdocumento 3.
- Formulario T-12 con los 374 códigos, aplicando la regla de fuente única.
- Matriz de trazabilidad.
- Migración a `TERABYTE_MATRICES_TECNICAS_INFORME_1.xlsx`.
- **Añadir número de página a cada cita**, conforme al BA, Art. 43.2.
---
 
## Referencias incorporadas en esta corrección
 
Azab, A., & Morita, H. (2022). Coordinating truck appointments with container relocations and retrievals in container terminals under partial appointments information. *Transportation Research Part E, 160*, 102673. https://doi.org/10.1016/j.tre.2022.102673
 
Bütün, C., et al. (2026). Energy-efficient container stacking in terminals: A multi-objective optimization framework. *Sustainability*.
 
Castelein, B., Geerlings, H., & Van Duin, R. (2020). The reefer container market and academic research: A review study. *Journal of Cleaner Production, 256*, 120654.
 
Cil, A. Y., Abdurahman, D., & Cil, I. (2022). Internet of Things enabled real time cold chain monitoring in a container port. *Journal of Shipping and Trade, 7*, 9. https://doi.org/10.1186/s41072-022-00110-z
 
Dahiya, S., et al. (2026). CSL-YMS: Sensor-fusion and energy efficient task scheduling. *Applied Sciences*.
 
Davies, P. (2009). *Container terminal reservation systems*. 3rd METRANS National Urban Freight Conference. https://dtci.ca/wp-content/uploads/2011/10/Container-Reservation-Systems-Web.pdf
 
Götting KG. (2013). *Position detection system using DGPS for container tracking* (S 57632ZA, Rev. 01). https://www.goetting.de/wp-content/uploads/2025/01/S_57632ZA_E_system-description_R01_TD.pdf
 
Hoffmann, A., et al. (2021). Quantifying the relative contributions of customs, trade and ports to cargo time delays. *World Customs Journal*.
 
Kan, A., et al. (2020). The characteristics of cargo temperature rising in reefer container under refrigeration-failure condition. *International Journal of Refrigeration, 112*.
 
Kaptan, M., et al. (2023). Fuzzy Bayesian network analysis of the factors causing food losses in reefer containers. *Journal of Food Process Engineering*.
 
Kim, K. H., & Yi, S. (2021). Utilizing information sources to reduce relocation of inbound containers. *Maritime Economics & Logistics, 23*(4), 726–749. https://doi.org/10.1057/s41278-021-00189-4
 
Klar, R., et al. (2024). Container relocation and retrieval tradeoffs minimizing schedule deviations and relocations. *IEEE Open Journal of Intelligent Transportation Systems, 5*.
 
Nguvumali, O., et al. (2025). Evaluating port-to-ICD logistical bottlenecks and their impact on customs clearance delays. *Social Science and Humanities Journal*.
 
Saurí, S., & Martín, E. (2011). Space allocating strategies for improving import yard performance at marine terminals. *Transportation Research Part E, 47*(6), 1038–1057.
 
West of England P&I Club. (s.f.). *The carriage of reefer containers* [Loss prevention bulletin]. https://www.westpandi.com/news-and-resources/loss-prevention-bulletins/the-carriage-of-reefer-containers/
 
Zając, M. (2026). Energy–operational trade-offs in container yard stacking strategies: A simulation-based analysis under dynamic conditions. *Applied Sciences*.
 
Zweers, B. G., Bhulai, S., & van der Mei, R. D. (2020). Pre-processing a container yard under limited available time. *Computers & Operations Research, 123*, 105045. https://doi.org/10.1016/j.cor.2020.105045
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*