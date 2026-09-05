# Catálogo de Requerimientos Funcionales — DEFINITIVO · Parte 2 de 3

## Dominios `RF-PAT`, `RF-TRA`, `RF-REF`, `RF-ACC` y `RF-OPD` — 49 requerimientos, Etapa 1

> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo B** · **Versión 2.1 — correcciones de la Fase 4 y decisiones de duplicados RF/RNF ya aplicadas.**
> **Este archivo reemplaza a `catalogo_rf_02_patio_refrigerado.md` y a la parte de `RF-ACC` y `RF-OPD` de `catalogo_rf_05_*.md`.** Las fichas están completas y corregidas.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26). Las convenciones del catálogo —ficha, clasificación, granularidad, redacción y regla de cita RT— están en la **Parte 1, sección 1**.

---

## Índice

| Sección | Contenido | Req. |
|---|---|---:|
| **1** | La restricción que gobierna este bloque | — |
| **2** | `RF-PAT` — Patio: posición, movimientos y asignación | **13** |
| **3** | `RF-TRA` — Tractocamiones de patio · **dominio nuevo** | **6** |
| **4** | `RF-REF` — Patio refrigerado y cadena de frío | **13** |
| **5** | `RF-ACC` — Identidad, habilitación y acceso de personas | **11** |
| **6** | `RF-OPD` — Operación desconectada y sincronización | **6** |
| **7** | Trazabilidad de la parte 2 | — |

**Requerimientos en revisión en esta parte: 1** — `RF-PAT-07`, marcado con **⚠**, pendiente de validación de la célula. Los casos `RF-REF-08`, `RF-REF-11`, `RF-ACC-10`, `RF-OPD-03` y `RF-OPD-04` quedaron resueltos; el estado vigente se consolida en `../03_Trazabilidad_y_Bases/registro_correccion_plan_maestro_20260904.md`.

---

## 1. La restricción que gobierna este bloque

> **CP, Cap. 10, restricción no negociable N° 1:** *«Ninguna solución puede aumentar la exposición de una persona al riesgo del patio. Toda propuesta que obligue a un operador a atender un dispositivo mientras hay equipos en movimiento será rechazada, cualquiera sea su mérito en el resto.»*

Cada requerimiento de terreno de este bloque se redactó contra esa frase. Es el único grupo de interés con **poder de rechazo sobre la propuesta completa**.

---

## 2. Dominio `RF-PAT` — Patio: posición, movimientos y asignación

**Etapa 1 · 13 requerimientos.**

---

### `RF-PAT-01` — Posicionamiento automático del equipo como fuente primaria · Prioridad: **Crítica**

**Descripción.** La solución **deberá** obtener la posición del contenedor a partir del **posicionamiento automático del equipo que lo manipula**, sin requerir confirmación activa de la persona operadora.

**Actor:** solución. **Precondición:** equipo instrumentado y operativo.
**Resultado esperado:** posición registrada como consecuencia del movimiento físico, no de una declaración humana.
**Origen:** Decisión N° 2 · CP, Cap. 10, restricción no negociable N° 1 · CP, 7.2 (3,1 % de contenedores registrados donde no están).
**Criterio de aceptación:** sobre una muestra de **100 movimientos observados físicamente**, la posición registrada automáticamente coincide con la real en el **95 %** de los casos, y ninguno de los 100 requirió confirmación de la persona operadora.

> *Corrección aplicada: el criterio no tenía umbral de coincidencia.*

---

### `RF-PAT-02` — Verificación cruzada por lectura óptica en puntos de paso · Prioridad: **Alta**

**Descripción.** La solución **deberá** leer ópticamente el código del contenedor en los puntos de paso obligados —gate y entrada de bloque— y **deberá** contrastar esa lectura contra la posición obtenida por posicionamiento automático.

**Actor:** solución. **Precondición:** contenedor atravesando un punto de paso instrumentado.
**Resultado esperado:** dos fuentes independientes sobre el mismo contenedor, contrastadas.
**Origen:** Decisión N° 2 (lectura óptica como verificación cruzada) · BTT, RT-17.06 · **CP, Cap. 15, RT-09.01** aporta el umbral de tiempo; la conducta proviene de la Decisión N° 2.
**Criterio de aceptación:** sobre un turno completo, el **100 %** de los pasos por un punto instrumentado genera un contraste registrado entre lectura óptica y posicionamiento automático.

---

### `RF-PAT-03` — Estado de confianza de la posición · Prioridad: **Crítica**

**Descripción.** La solución **deberá** mantener para cada contenedor un **estado de confianza de su posición**, que será «conocida» cuando el posicionamiento automático y una lectura óptica reciente coincidan, y «por verificar» cuando discrepen o cuando falte una de las dos fuentes.

**Actor:** solución. **Precondición:** contenedor registrado en inventario.
**Resultado esperado:** todo contenedor del inventario tiene estado de confianza explícito y consultable.
**Origen:** Decisión N° 2, que define cuándo una posición se considera «conocida» · CP, Cap. 18, criterio 9.
**Criterio de aceptación:** se consulta el inventario completo y el **100 %** de los contenedores presenta uno de los dos estados; se inyecta una discrepancia y el estado del contenedor afectado cambia a «por verificar».

---

### `RF-PAT-04` — Tarea de verificación física ante discrepancia · Prioridad: **Alta**

**Descripción.** Ante un contenedor en estado «por verificar», la solución **deberá** generar automáticamente una **tarea de verificación física dirigida** a la posición candidata, y **no deberá** dejar la discrepancia sin acción asignada.

**Actor:** solución y supervisor de patio. **Precondición:** contenedor en estado «por verificar».
**Resultado esperado:** tarea generada, asignada y con seguimiento hasta su cierre.
**Origen:** Decisión N° 2 · meta del indicador «contenedores registrados donde no están»: **≤ 0,5 %** de posiciones «por verificar» no resueltas dentro del turno.
**Criterio de aceptación:** el 100 % de las discrepancias genera tarea, y el porcentaje de tareas no resueltas al cierre del turno es **≤ 0,5 %** del inventario.

---

### `RF-PAT-05` — Registro del movimiento sin confirmación del operador · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar la ejecución de un movimiento de contenedor a partir de la **telemetría del propio equipo** —sensores de izaje, encoders de posición y posicionamiento— y **no deberá** requerir que la persona operadora ejecute una acción de confirmación.

**Actor:** solución. **Precondición:** equipo instrumentado en operación.
**Resultado esperado:** movimiento registrado en el instante en que ocurre, sin interacción humana.
**Origen:** Decisión N° 15 · CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 4.3 (hoy los movimientos «se registran al final del turno, a mano»).
**Criterio de aceptación:** sobre **100 movimientos observados físicamente**, la telemetría registra los 100 con su instante, y ningún registro dependió de una acción del operador.

---

### `RF-PAT-06` — Asignación algorítmica de la posición · Prioridad: **Crítica**

**Descripción.** El motor de asignación de patio **deberá** determinar la celda de destino de cada contenedor resolviendo de forma lógica y simultánea: (1) la compatibilidad y distancia de segregación de mercancías peligrosas del **Código IMDG** conforme a **RN-02**; (2) la disponibilidad de toma eléctrica energizada para unidades refrigeradas; y (3) la secuencia de salida según fecha de recalada, para minimizar remociones. Cuando dos restricciones no puedan satisfacerse de forma simultánea, la solución **deberá** aplicar el orden de precedencia de **RN-01** y **deberá** explicitar qué restricción cedió y por qué.

**Actor:** solución. **Precondición:** contenedor ingresado o descargado, con sus atributos declarados (tipo de carga, clase IMDG, requerimiento de frío, recalada asociada).
**Resultado esperado:** posición asignada por regla explicable y trazable, no por criterio individual del operador, con la restricción cedida declarada cuando corresponda.
**Origen:** Decisión N° 3 («el algoritmo asigna, el operador ejecuta») · **RN-01** fija el orden de precedencia · **RN-02** fija la matriz de segregación · CP, Cap. 12, materia 6 (IMDG: «restringe la libertad del algoritmo de patio») · CP, Cap. 4.4 («no existe un algoritmo, ni una regla escrita, ni un registro de por qué se eligió esa posición») · CP, Cap. 18, criterio 8.
**Criterio de aceptación:** sobre un turno completo, el **100 %** de las asignaciones proviene del algoritmo, y cada asignación conserva **el nivel de RN-01 que la determinó**. De acuerdo con las pautas de redacción del curso, la consistencia del algoritmo se verifica mediante dos ejemplos numéricos y lógicos resueltos:

> **Ejemplo 1 — asignación directa sin conflicto.**  
> *Entrada:* contenedor refrigerado (`frío = Sí`), carga general (`IMDG = No aplica`), recalada = Nave "Aconcagua" (`secuencia de salida = Prioridad Alta`).  
> *Resolución:* el motor identifica las celdas con tomas reefer operativas y libres. Filtra aquellas que minimizan remociones para la fecha de recalada de la nave "Aconcagua". Al no haber restricciones en conflicto, asigna la celda `B-12-04` (que cuenta con toma activa y está en primera línea de despacho).
>
> **Ejemplo 2 — resolución de conflicto aplicando precedencia.**  
> *Entrada:* contenedor refrigerado (`frío = Sí`), carga peligrosa Clase 3 (`IMDG = Líquido Inflamable`). El único enchufe reefer libre en esa zona está a menos de 6 metros de un contenedor Clase 8 (`Corrosivo`) ya posicionado.  
> *Resolución:* se genera un conflicto de restricciones copulativas. El sistema aplica el orden de precedencia de **RN-01** (donde la seguridad humana y la segregación IMDG antecede a la disponibilidad de frío). El motor prioriza la segregación de seguridad por sobre el suministro eléctrico: asigna el contenedor a una celda segura a 12 metros de distancia, pero sin toma reefer fija. Se bloquea la asignación en la celda conflictiva, se emite una alerta declarando que *«la restricción de frío cedió ante la regla de seguridad física IMDG de RN-02»* y se instruye operativamente el uso de un generador portátil (*clip-on*).

---

### `RF-PAT-07` — Catálogo de condiciones dinámicas de patio · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir al planificador declarar en tiempo real condiciones dinámicas que restrinjan la asignación —equipo no disponible, bloque restringido, cliente de alto riesgo de atraso— y **deberá** respetarlas en cada corrida posterior del algoritmo.

**Actor:** planificador de estiba y patio. **Precondición:** ninguna; la declaración es a demanda.
**Resultado esperado:** la condición declarada rige desde su registro y queda trazada con autor, motivo y vigencia.
**Origen:** Decisión N° 5 · RN-01, nivel 3 · CP, Cap. 4.2 (la grúa con falla intermitente, el bloque que se inunda, el generador de popa limitado: «nada de eso está escrito en ninguna parte») · CP, 16.1 decisión 5 («un plan óptimo sobre supuestos falsos se cae en la segunda hora») · BTT, RT-16.02.
**Criterio de aceptación:** se declara una condición dinámica y la **siguiente corrida** del algoritmo la respeta; la condición queda registrada con autor, motivo y vigencia.

---

### `RF-PAT-08` — Instrucción al equipo sin interacción activa · Prioridad: **Crítica**

**Descripción.** La solución **deberá** presentar la instrucción de movimiento en la terminal del equipo mediante indicación visual, y **no deberá** exigir a la persona operadora manipular el dispositivo mientras haya equipos en movimiento.

**Actor:** operador de equipo de patio. **Precondición:** instrucción asignada al equipo.
**Resultado esperado:** instrucción visible sin acción del operador durante la faena, con los elementos declarados en el checklist ergonómico por puesto de terreno.
**Origen:** CP, Cap. 10, restricción no negociable N° 1 · **CP, Cap. 15, RT-13.08** aporta las condiciones de terreno; la conducta exigida proviene de la restricción N° 1 · Decisión N° 3.
**Criterio de aceptación:** evaluación de riesgo de la interfaz con participación de prevención de riesgos, **contra el checklist ergonómico por puesto de terreno**, con acta de conformidad previa al paso a producción. Se articula con RNF-USA-05.

> *Correcciones aplicadas: se retira «comprensible» (subjetivo) y se nombra el instrumento de la evaluación, que antes quedaba sin definir.*

---

### `RF-PAT-09` — Vía de excepción del operador con interlock · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir a la persona operadora marcar una instrucción como **no ejecutable**, seleccionando un motivo de una lista breve, y **deberá** habilitar esa función **únicamente cuando la telemetría del equipo acredite detención**, deshabilitándola automáticamente al reanudarse el movimiento. La solución **deberá** reasignar la posición sin exigir que el movimiento se complete.

**Actor:** operador de equipo de patio. **Precondición:** instrucción recibida y detención acreditada por telemetría.
**Resultado esperado:** instrucción devuelta con motivo; el algoritmo produce una asignación alternativa; el motivo alimenta el catálogo de condiciones dinámicas de `RF-PAT-07`.
**Origen:** **Supuesto O** del `../02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md` · CP, Cap. 10, restricción no negociable N° 1, que prohíbe la interacción **mientras hay equipos en movimiento** y por tanto no alcanza a una acción con el equipo detenido · Decisión N° 5, por analogía con la vía que sí tiene el planificador · Dahiya et al. (2026), que documenta que el error de colocación proviene de causas —orientación del contenedor— que el posicionamiento automático no corrige.
**Criterio de aceptación:** se intenta marcar una instrucción como no ejecutable **con el equipo en movimiento y la función no está disponible**; se repite con el equipo detenido y la marca se registra con su motivo; se acredita que el algoritmo reasigna y que el motivo queda disponible para el planificador.

> **Ya no está en revisión.** Cierra el hueco que la propia Decisión N° 3 reconoce: *«el operador ejecutará una instrucción errónea sin oportunidad de corregirla antes del movimiento»*. El **interlock** convierte el cumplimiento de la restricción N° 1 en propiedad verificable del sistema, comprobable contra el mismo flujo de telemetría de `RF-PAT-05`.
>
> **Indicador derivado:** la tasa de uso de esta vía es indicador de **calidad del algoritmo**. Un uso frecuente indica que la asignación desconoce restricciones estructurales, no puntuales.
>
> Pendiente: acta de conformidad de prevención de riesgos y del sindicato antes del diseño detallado.

---

### `RF-PAT-10` — Programación anticipada de remociones · Prioridad: **Alta**

**Descripción.** La solución **deberá** calcular las remociones necesarias para acceder a un contenedor comprometido —retiro con cita, inspección agendada o embarque planificado— y **deberá** programarlas con la holgura declarada antes del momento comprometido, en lugar de ejecutarlas cuando el contenedor se solicita.

**Actor:** solución. **Precondición:** compromiso registrado con hora acordada y posición del contenedor conocida.
**Resultado esperado:** remociones ejecutadas antes del momento comprometido; el contenedor está accesible a la hora.
**Origen:** CP, Cap. 4.7 (el atraso ocurre «porque estaba abajo de otros tres **y la remoción no se programó**») · CP, Cap. 18, criterios 8 y 10 · **Decisión N° 21** funda el mecanismo para inspecciones; **Terabyte lo generaliza** a todo compromiso con hora cierta —retiro con cita (Decisión N° 6, RN-07) y embarque planificado (Decisión N° 4)— por identidad de razón: en los tres casos hay un tercero con hora acordada y un contenedor que puede estar bloqueado. **La generalización se declara como supuesto de alcance.**
**Criterio de aceptación:** sobre una muestra de **50 compromisos con hora acordada**, la remoción necesaria se programó al momento de agendar y se ejecutó antes de la hora en el **≥ 90 %** de los casos; los incumplimientos se clasifican por causa.

> *Corrección aplicada: el origen citaba la Decisión N° 21 para un alcance mayor que el suyo. La generalización queda declarada.*

---

### `RF-PAT-11` — Consulta de posición de contenedor · Prioridad: **Crítica**

**Descripción.** La solución **deberá** responder la consulta de posición de cualquier contenedor del inventario, entregando bloque, bahía, fila, altura y estado de confianza.

**Actor:** supervisor, planificador, operador de gate y persona usuaria externa autorizada. **Precondición:** contenedor en inventario.
**Resultado esperado:** posición y confianza entregadas sin búsqueda física.
**Origen:** CP, Cap. 18, criterio 9 · Decisión N° 2 · **CP, Cap. 15, RT-09.01** aporta el umbral de tiempo —consulta no superior a 1 segundo—.
**Criterio de aceptación:** la consulta devuelve bloque, bahía, fila, altura y estado de confianza **en no más de 1 segundo**, medido en el percentil 95 bajo carga de peak.

> *Corrección aplicada: el criterio anterior medía el porcentaje de retiros con búsqueda física, que es consecuencia del conjunto `RF-PAT-01` a `05` y no prueba este requerimiento. Esa métrica pertenece a la tabla de indicadores.*

---

### `RF-PAT-12` — Registro de movimientos exclusivamente por telemetría · Prioridad: **Crítica**

**Descripción.** La solución **no deberá** admitir el alta de un movimiento de contenedor por vía distinta de la telemetría del equipo que lo ejecuta, y **no deberá** admitir la confirmación por radio como mecanismo de registro.

**Actor:** solución. **Precondición:** equipos instrumentados conforme a la especificación de hardware entregada al CLIENTE.
**Resultado esperado:** ningún movimiento entra al registro por declaración humana.
**Origen:** CP, Cap. 5 («la cobertura parcial es una de las causas del 3,1 % de contenedores mal ubicados») · Decisión N° 15 · CP, Cap. 11, exclusión 9 (Terabyte especifica el hardware; el CLIENTE lo adquiere).
**Criterio de aceptación:** se intenta dar de alta un movimiento por vía manual y el sistema no lo acepta; sobre un turno completo, el 100 % de los movimientos registrados proviene de telemetría.

> *Corrección aplicada: la redacción anterior —«operar con la totalidad de los equipos instrumentados»— describía un **estado de la instalación**, no un comportamiento, y por tanto no era funcional. La cobertura de instrumentación es **meta de indicador**: **74 equipos** —18 grúas de patio, 42 tractocamiones, 14 de manipulación pesada—, con proyección a 88 (CP, 14.1).*

---

### `RF-PAT-13` — Registro de movimientos por hora y por equipo · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar cada movimiento con su instante, su equipo y su persona operadora asignada, de modo que la productividad sea calculable por hora y por equipo sin consolidación manual.

**Actor:** solución. **Precondición:** movimiento registrado por telemetría.
**Resultado esperado:** serie de movimientos con granularidad por hora y por equipo.
**Origen:** CP, 7.1 («registro del detalle de movimientos por hora y por grúa: inexistente») · CP, Cap. 18, criterio 6 · **CP, Cap. 15, RT-05.29** aporta el umbral de disponibilidad del indicador.
**Criterio de aceptación:** se consulta la productividad de una hora y un equipo determinados y se desciende hasta los movimientos individuales que la componen.

---

## 3. Dominio `RF-TRA` — Tractocamiones de patio

**Etapa 1 · 6 requerimientos. Dominio nuevo.**

> **Por qué existe.** El catálogo original no cubría los 42 tractocamiones que mueven cada contenedor entre muelle y patio. El CP, Cap. 4.3 identifica la espera de tractocamión como la **primera** de las tres causas de la brecha entre 24,8 y 30 movimientos por hora, declara que «su ubicación exacta en cada momento es conocimiento del supervisor, no del sistema», y el operador de grúa pide literalmente en su entrevista «saber que el tractocamión que estoy esperando viene en camino y en cuánto». Medir la productividad no la mueve; había que atacar su causa.

---

### `RF-TRA-01` — Posicionamiento de los tractocamiones · Prioridad: **Crítica**

**Descripción.** La solución **deberá** conocer la posición de cada tractocamión de patio mediante posicionamiento automático del equipo, sin depender de la comunicación por radio con el supervisor.

**Actor:** solución. **Precondición:** tractocamión instrumentado y en operación.
**Resultado esperado:** posición de los 42 equipos conocida por el sistema, no solo por el supervisor.
**Origen:** CP, Cap. 4.3 · CP, Cap. 14.1 (42 tractocamiones, hasta 88 equipos móviles a instrumentar) · Decisión N° 2, que adopta el posicionamiento automático del equipo como fuente primaria.
**Criterio de aceptación:** sobre una muestra de **50 posiciones observadas físicamente**, la posición registrada coincide con la real dentro de la tolerancia declarada para el patio en el **95 %** de los casos.

---

### `RF-TRA-02` — Asignación de tractocamión a movimiento de grúa · Prioridad: **Crítica**

**Descripción.** La solución **deberá** asignar automáticamente un tractocamión a cada movimiento de grúa de muelle, considerando la posición del equipo, su estado de ocupación y la secuencia del plan de estiba vigente, y **no deberá** requerir que la asignación se comunique por radio.

**Actor:** solución y supervisor de turno. **Precondición:** plan de estiba publicado y equipos posicionados.
**Resultado esperado:** cada movimiento tiene equipo asignado antes de que la grúa lo requiera.
**Origen:** CP, Cap. 4.3 («el supervisor asigna los tractocamiones por radio») · CP, Cap. 5 (la radio debe dejar de ser sistema de registro) · CP, Cap. 18, criterio 6.
**Criterio de aceptación:** sobre un turno completo de operación de nave, el **100 %** de los movimientos ejecutados tiene un tractocamión asignado por el sistema con anterioridad al movimiento, y la asignación consta con su instante.

---

### `RF-TRA-03` — Tiempo estimado de arribo del tractocamión a la grúa · Prioridad: **Alta**

**Descripción.** La solución **deberá** presentar al operador de grúa de muelle, en la pantalla de cabina, el **tiempo estimado de arribo** del tractocamión asignado a su próximo movimiento, mediante indicación visual y sin exigir acción alguna del operador.

**Actor:** operador de grúa de muelle. **Precondición:** tractocamión asignado (`RF-TRA-02`) y posicionado (`RF-TRA-01`).
**Resultado esperado:** el operador anticipa la espera en vez de descubrirla.
**Origen:** CP, Cap. 8, petición literal del operador de grúa: «saber que el tractocamión que estoy esperando viene en camino y en cuánto» · CP, Cap. 10, restricción no negociable N° 1 · CP, Cap. 18, criterio 21 · Decisión N° 14, que fija el modo de presentación en cabina.
**Criterio de aceptación:** el tiempo estimado se presenta en cabina para el **100 %** de los movimientos asignados, y su error medio respecto del arribo real no supera **60 segundos**, medido sobre **200 movimientos**.

---

### `RF-TRA-04` — Registro de la detención de grúa por espera de equipo · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar como evento propio cada detención de grúa de muelle atribuible a espera de tractocamión, con su inicio, su término y el equipo involucrado.

**Actor:** solución. **Precondición:** grúa en operación con movimiento pendiente y sin tractocamión disponible en posición.
**Resultado esperado:** la primera causa de la brecha de productividad queda cuantificada, no supuesta.
**Origen:** CP, Cap. 4.3, que identifica esta espera como causa de la brecha · CP, 7.1 («capacidad de explicar a la naviera la causa de un sobretiempo de nave: inexistente») · articula con `RF-NAV-13`.
**Criterio de aceptación:** para una recalada cerrada, la suma de las detenciones registradas por causa reconcilia con la diferencia entre el tiempo total de atención y el tiempo de operación efectiva, **sin residuo no clasificado superior al 5 %**.

---

### `RF-TRA-05` — Reasignación ante indisponibilidad del equipo · Prioridad: **Alta**

**Descripción.** Cuando un tractocamión asignado quede indisponible, la solución **deberá** reasignar el movimiento a otro equipo y **deberá** actualizar el tiempo estimado de arribo en la cabina afectada.

**Actor:** solución. **Precondición:** equipo asignado que deja de estar disponible.
**Resultado esperado:** la indisponibilidad no se traduce en una espera indefinida ni en una llamada por radio.
**Origen:** CP, Cap. 4.3 · Decisión N° 5, catálogo de condiciones dinámicas, que ya permite declarar un equipo no disponible.
**Criterio de aceptación:** se declara un equipo no disponible durante una operación y se verifica que el movimiento se reasigna y que la cabina refleja el nuevo tiempo estimado **en no más de 30 segundos** desde la declaración.

---

### `RF-TRA-06` — Registro de movimientos del tractocamión · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar cada traslado ejecutado por un tractocamión, con origen, destino, contenedor e instantes, derivado de la telemetría del equipo y sin confirmación activa del conductor.

**Actor:** solución. **Precondición:** tractocamión instrumentado ejecutando un traslado.
**Resultado esperado:** el ciclo completo del contenedor entre muelle y patio queda trazado.
**Origen:** Decisión N° 15 · CP, Cap. 10, restricción no negociable N° 1 · articula con `RF-PAT-05`.
**Criterio de aceptación:** sobre una muestra de **100 traslados observados**, el 100 % queda registrado con origen, destino y contenedor correctos, sin acción del conductor.

---

## 4. Dominio `RF-REF` — Patio refrigerado y cadena de frío

**Etapa 1, como capacidad nueva · 13 requerimientos.** Dominio de máxima reversibilidad —volver a la ronda a pie— y el que responde al evento del 18 de febrero de 2026.

> **Cobertura de ambos sentidos.** El dominio aplica a todo contenedor refrigerado recibido bajo custodia del terminal: **exportación**, desde su ingreso por gate hasta su desconexión autorizada para embarque; e **importación**, desde su descarga de nave hasta su desconexión autorizada para retiro por gate. La serie instrumentada del terminal comienza con la conexión física y termina con la desconexión; el plazo máximo recepción/descarga → conexión se mantiene como parámetro por validar con el CLIENTE y no se inventa en este catálogo.

> **Sobre la justificación del dominio.** El estándar de la industria aseguradora es revisión **cada 6 horas**, de modo que la ronda de 4 horas del terminal ya lo supera. El beneficio comprometido **no es «detectar más rápido»** sino **cobertura sin ventana ciega y evidencia entregable**: el evento del 18 de febrero ocurrió porque falló un tablero completo de madrugada y nadie pasó caminando.

---

### `RF-REF-01` — Muestreo local en el borde · Prioridad: **Crítica**

**Descripción.** La solución **deberá** muestrear localmente, en el borde, la temperatura, el estado de conexión y el consumo de cada toma refrigerada, con un intervalo de **entre 1 y 5 minutos**.

**Actor:** solución. **Precondición:** toma instrumentada.
**Resultado esperado:** serie local de alta resolución disponible para detección y para respaldo.
**Origen:** Decisión N° 8, modelo de dos capas · CP, 16.1 decisión 8 («la diferencia entre 1 minuto y 15 minutos es la diferencia entre detectar y no detectar el evento del 18 de febrero»).
**Criterio de aceptación:** sobre una muestra de **50 tomas durante 24 horas continuas**, el intervalo de muestreo local se mantiene dentro del rango de 1 a 5 minutos en el **100 %** de las lecturas.

---

### `RF-REF-02` — Agregación en el borde y reporte al núcleo · Prioridad: **Alta**

**Descripción.** El componente de borde **deberá** agregar localmente las lecturas y **descartar las lecturas redundantes** conforme a la regla declarada, y **deberá** reportarlas al núcleo con un intervalo de **entre 5 y 15 minutos**. El componente **no deberá** transmitir el dato crudo de las 2.400 tomas de forma continua.

**Actor:** solución. **Precondición:** muestreo local operativo.
**Resultado esperado:** carga de red acotada, sin pérdida de capacidad de detección.
**Origen:** Decisión N° 8, ajustada tras la investigación de práctica de la industria · BTT, RT-03.19 (procesamiento en el borde).
**Criterio de aceptación:** el intervalo de reporte agregado se mantiene entre 5 y 15 minutos, y la detección de excepción sigue ocurriendo **en no más de 5 minutos** desde el evento físico, medida por inyección de falla.

> *Correcciones aplicadas: se retira «prefiltrar» (verbo ambiguo) y se nombra el umbral que el criterio invocaba sin definir.*

---

### `RF-REF-03` — Envío inmediato ante excepción · Prioridad: **Crítica**

**Descripción.** Ante cualquier excepción o condición de alarma, el componente de borde **deberá** transmitirla de inmediato al núcleo, sin esperar el ciclo de reporte agregado.

**Actor:** solución. **Precondición:** excepción detectada localmente.
**Resultado esperado:** la excepción llega al núcleo fuera del ciclo periódico.
**Origen:** Decisión N° 8 · **CP, Cap. 15, RT-05.29** aporta el umbral —alarma no superior a 5 minutos desde el evento físico—.
**Criterio de aceptación:** se inyecta una falla controlada y el tiempo entre el evento físico y la alarma generada es **≤ 5 minutos**, conforme a RNF-DES-04.

---

### `RF-REF-04` — Detección de desviación de temperatura · Prioridad: **Crítica**

**Descripción.** La solución **deberá** detectar la desviación de la temperatura de un contenedor respecto de su **temperatura de consigna declarada**, y **deberá** generar la alarma correspondiente.

**Actor:** solución. **Precondición:** contenedor conectado con consigna registrada.
**Resultado esperado:** desviación detectada y alarmada.
**Origen:** CP, Cap. 4.5 (la consigna depende de la carga: «la cereza no es el salmón») · CP, Cap. 18, criterio 11 · **CP, Cap. 15, RT-05.29** aporta el umbral.
**Criterio de aceptación:** se simula una desviación **por sobre la banda de tolerancia declarada en `RN-11` para la familia de carga del contenedor**, sobre una muestra de **30 tomas**, y la alarma se genera para las 30 **en no más de 5 minutos desde el evento físico**.

> *Corrección aplicada: el criterio decía «dentro del umbral» sin nombrarlo.*

> *Corrección aplicada 2026-09-05: el criterio ya verificaba la rama de desviación, pero «desviación» no estaba definida en ninguna parte: ninguna regla decía cuánto debe apartarse una lectura de su consigna, ni por cuánto tiempo, para constituirla. `RT-05.29` aporta el plazo de la alarma, no la banda. Se crea `RN-11` y el criterio pasa a invocarla, de modo que la prueba sea reproducible.*

---

### `RF-REF-05` — Detección de desconexión de toma · Prioridad: **Crítica**

**Descripción.** La solución **deberá** detectar la desconexión de un contenedor refrigerado de su toma y **deberá** generar alarma, con independencia de que la temperatura aún no se haya desviado.

**Actor:** solución. **Precondición:** contenedor previamente conectado.
**Resultado esperado:** desconexión alarmada antes de que la carga se degrade.
**Origen:** CP, Cap. 15, RT-05.29 (alarma «de desconexión o de desviación») · CP, Cap. 4.5 (la inercia térmica retrasa la manifestación de la desconexión).
**Criterio de aceptación:** se desconectan **10 tomas** en condiciones controladas y la alarma se genera para las 10 **sin esperar la desviación de temperatura**, dentro de los 5 minutos.

---

### `RF-REF-06` — Detección de falla de tablero · Prioridad: **Crítica**

**Descripción.** La solución **deberá** detectar la falla de un tablero de distribución completo como **evento propio**, distinguiéndolo de la desconexión individual de las tomas que dependen de él.

**Actor:** solución. **Precondición:** tablero instrumentado.
**Resultado esperado:** una alarma de tablero, no una avalancha de alarmas individuales indistinguibles.
**Origen:** CP, Cap. 4.5 y Cap. 1: el evento del 18 de febrero fue la falla de **un tablero completo**, con 38 contenedores afectados durante 9 horas y una pérdida de US$ 620.000 · CP, 7.2 (0 de 26 tableros con alarma remota).
**Criterio de aceptación:** se simula la falla de un tablero y se genera **una** alarma de tablero identificada como tal, con el listado de tomas afectadas, y **no** una alarma por toma.

> Es el requerimiento que responde directamente al modo de falla del evento: si el sistema solo alarmara por toma, ese evento habría producido 38 alarmas simultáneas indistinguibles en el turno de madrugada con dotación mínima — otra forma de no detectarlo.

---

### `RF-REF-07` — Distinción entre sensor caído y condición estable · Prioridad: **Alta**

**Descripción.** La solución **deberá** distinguir un sensor que dejó de reportar de una toma cuya temperatura se mantiene estable, y **deberá** alarmar la ausencia de dato como condición propia.

**Actor:** solución. **Precondición:** toma instrumentada con serie previa.
**Resultado esperado:** la ausencia de lectura no se interpreta como normalidad.
**Origen:** Decisión N° 8, que descarta la transmisión de solo desviaciones precisamente porque «no distingue un sensor caído de una temperatura estable».
**Criterio de aceptación:** se interrumpe la señal de un sensor y la solución genera alarma de ausencia de dato **tras 3 intervalos de muestreo consecutivos sin lectura o a los 5 minutos desde la última lectura válida, lo que ocurra primero**.

> *Corrección aplicada: el criterio derivaba la alarma solo del muestreo vigente de `RF-REF-01`, que admite hasta 5 minutos; con ese valor la ausencia de dato podía tardar 15 minutos en alarmar. Un sensor caído es operacionalmente indistinguible de una desconexión no detectada —es el modo de falla del 18 de febrero—, y CP, Cap. 15, RT-05.29 exige alarma en no más de 5 minutos desde el evento físico. Se añade el techo de 5 minutos sin reabrir la Decisión N° 8, que mantiene el muestreo local de 1 a 5 minutos. Las dos condiciones operan como **lo que ocurra primero**: con muestreo sobre 1 min 40 s los 3 intervalos no caben en 5 minutos, y en ese caso manda el techo.*

> *Corrección aplicada: el criterio invocaba un «intervalo declarado» que no estaba declarado en ninguna parte. Ahora se deriva del muestreo.*

---

### `RF-REF-08` — Notificación simultánea a dos destinatarios · Prioridad: **Crítica**

**Descripción.** La solución **deberá** enviar cada alarma del patio refrigerado **simultáneamente** al operador de turno y a un supervisor de guardia, por canal redundante, en cualquiera de los tres turnos.

**Actor:** solución. **Precondición:** alarma generada.
**Resultado esperado:** dos destinatarios notificados por canales independientes.
**Origen:** Decisión N° 10 · **RN-08** (regla transversal de escalamiento y confirmación) · **CP, Cap. 15, RT-16.21** aporta la exigencia de canal redundante con escalamiento; **BTT, RT-16.20** aporta la conducta de notificación por al menos tres canales.
**Criterio de aceptación:** se genera una alarma en turno de madrugada y se verifica la recepción por ambos destinatarios y por ambos canales. El porcentaje de confirmación registrada se acredita en RNF-DIS-08.

> **Resuelto.** La Célula 2 acordó conservar el RF reducido a la **conducta de notificación simultánea por canal redundante**; el umbral de 100 % de alarmas con confirmación registrada queda como fuente única en **RNF-DIS-08**, que es el que acredita el T-12. Esta redacción ya refleja el acuerdo.

---

### `RF-REF-09` — Escalamiento automático ante falta de confirmación · Prioridad: **Crítica**

**Descripción.** Si ninguno de los destinatarios confirma la recepción dentro del plazo declarado, la solución **deberá** escalar automáticamente a un tercer contacto.

**Actor:** solución. **Precondición:** alarma emitida sin confirmación dentro del plazo.
**Resultado esperado:** escalamiento ejecutado sin intervención humana.
**Origen:** Decisión N° 10 · **RN-08** · CP, 16.1 decisión 10 («una alarma que nadie atiende es exactamente el resultado del 18 de febrero, sólo que con más registros») · BTT, RT-16.11 (escalamiento automático por vencimiento) · BTT, RT-16.02 (el plazo es parámetro configurable).
**Criterio de aceptación:** simulacro de no respuesta del primer y del segundo destinatario, verificando la activación del tercer contacto **dentro del plazo parametrizado vigente**.

---

### `RF-REF-10` — Registro auditable de la confirmación · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar quién confirmó cada alarma, por qué canal y en qué instante, y **deberá** conservar ese registro como evidencia auditable.

**Actor:** operador o supervisor. **Precondición:** alarma emitida.
**Resultado esperado:** trazabilidad completa de la atención de cada alarma.
**Origen:** Decisión N° 10 · **RN-08** · CP, 16.1 decisión 10 («qué ocurre si nadie confirma») · BTT, RT-16.06 · articula con RNF-DIS-08, que fija el umbral de 100 % de alarmas con confirmación registrada.
**Criterio de aceptación:** se consulta una alarma cualquiera del período y se recupera el autor, el canal y el instante de su confirmación, o la constancia de que se escaló por falta de ella.

---

### `RF-REF-11` — Serie continua de temperatura por contenedor · Prioridad: **Crítica**

**Descripción.** La solución **deberá** mantener una serie continua de temperatura por cada contenedor refrigerado, desde su conexión hasta su desconexión, **sin lagunas atribuibles al sistema**.

**Actor:** solución. **Precondición:** contenedor conectado a toma instrumentada.
**Resultado esperado:** serie íntegra por contenedor.
**Origen:** CP, Cap. 18, criterio 12 · **CP, Cap. 15, RT-05.10** fija la retención de series de temperatura en 5 años · articula con **RNF-CUM-08**, que conserva el umbral de cobertura del 100 % y el plazo de retención.
**Criterio de aceptación:** se audita la serie de una muestra de **20 contenedores** verificando continuidad desde conexión hasta desconexión, sin lagunas atribuibles al sistema.

> **Resuelto.** La Célula 2 confirmó el reparto: el RF conserva la conducta —mantener la serie continua sin lagunas atribuibles al sistema— y **RNF-CUM-08** conserva el umbral de cobertura del 100 % y el plazo de retención de 5 años, siendo la fuente única para el T-12.

---

### `RF-REF-12` — Entrega de la evidencia de cadena de frío · Prioridad: **Alta**

**Descripción.** La solución **deberá** permitir al cliente y a la autoridad obtener la serie de temperatura de un contenedor como **documento entregable en formato abierto**, por autoservicio.

**Actor:** exportador, importador, agencia o autoridad. **Precondición:** serie registrada y persona usuaria autorizada.
**Resultado esperado:** evidencia de cadena de frío obtenida sin intervención del terminal.
**Origen:** CP, Cap. 9.5 (registro «entregable como evidencia de cadena de frío al cliente y a la autoridad») · CP, Cap. 12, materia 9 · BTT, RT-16.32 · BTT, RT-05.06 · supuesto de alcance del autoservicio, trámite 5.
**Criterio de aceptación:** una persona usuaria externa autorizada descarga la serie de un contenedor en formato abierto, sin contacto con el terminal.

---

### `RF-REF-13` — Registro de horas de conexión como hecho facturable · Prioridad: **Alta**

**Descripción.** La solución **deberá** derivar las horas de conexión refrigerada facturables de los **eventos de conexión y desconexión registrados por la instrumentación**, descontando el tiempo desconectado conforme a **RN-10**, y **no deberá** calcularlas a partir de la planilla de ronda.

**Actor:** solución. **Precondición:** eventos de conexión y desconexión registrados.
**Resultado esperado:** hecho facturable con evidencia verificable, generado en el momento en que ocurre.
**Origen:** CP, Cap. 4.8 (hoy la conexión refrigerada se calcula «con las horas que estuvo conectado según la planilla de la ronda») · Decisión N° 11 · **RN-10**: se factura el tiempo conectado efectivo · CP, Cap. 18, criterio 14.

**Ejemplos numéricos del cálculo:**

> **Ejemplo A — conexión continua.** Conectado el 12 de enero a las 06:00; desconectado el 14 de enero a las 18:00; sin interrupciones registradas.
> Tiempo conectado: **60 horas**. **Horas facturables: 60.**
>
> **Ejemplo B — con desconexión intermedia registrada.** Conectado el 12 de enero a las 06:00. La instrumentación registra desconexión el 13 de enero de 02:15 a 05:45 —3 horas 30 minutos— por falla de tablero. Desconectado definitivamente el 14 de enero a las 18:00.
> Permanencia en la toma: 60 horas. Tiempo desconectado registrado: 3,5 horas. **Horas facturables: 56,5.**
>
> El descuento se aplica **con independencia de la causa**, incluida la falla atribuible al terminal, y se deriva de los eventos de `RF-REF-05` y `RF-REF-06`, no de una declaración manual.

**Criterio de aceptación:** se inyectan los dos casos anteriores y el cálculo devuelve 60 y 56,5 horas respectivamente; sobre una muestra de facturación real, ninguna hora facturada proviene de registro manual.

> *Correcciones aplicadas: se incorpora RN-10 y los dos ejemplos numéricos exigidos para todo requisito con cálculo.*

---

## 5. Dominio `RF-ACC` — Identidad, habilitación y acceso de personas

**Etapa 1 · 11 requerimientos.** Gobernado por dos restricciones simultáneas: el plan de protección portuaria exige control efectivo, y los acuerdos sindicales prohíben la biometría obligatoria.

---

### `RF-ACC-01` — Credencial temporal vinculada a la nombrada · Prioridad: **Crítica**

**Descripción.** La solución **deberá** emitir al trabajador eventual una **credencial de acceso temporal vinculada a su asignación de turno**, generada al confirmarse la nombrada, y **no deberá** exigir un proceso de habilitación individual previo distinto del que los acuerdos vigentes contemplan.

**Actor:** solución y trabajador portuario eventual. **Precondición:** nombrada del turno confirmada.
**Resultado esperado:** habilitación disponible al inicio del turno, sin trámite individual que retrase el ingreso.
**Origen:** Decisión N° 12 · CP, Cap. 10, restricción no negociable N° 8 · CP, Cap. 4.9 (hoy la habilitación «se maneja con listados que se entregan en portería») · CP, Cap. 2.4 (hasta 380 eventuales por turno, ~2.100 personas distintas al año).
**Criterio de aceptación:** para un turno de **380 eventuales**, las credenciales quedan emitidas y disponibles **en no más de 30 minutos** desde la confirmación de la nombrada.

> *Corrección aplicada: el criterio anterior decía «sin retraso atribuible al sistema», que no es operacionalizable y desplaza la carga de prueba.*

---

### `RF-ACC-02` — Expiración automática de la credencial · Prioridad: **Crítica**

**Descripción.** La credencial temporal **deberá** expirar automáticamente al cierre del turno para el que fue emitida, sin requerir acción de revocación.

**Actor:** solución. **Precondición:** credencial emitida con turno asociado.
**Resultado esperado:** ninguna credencial de eventual permanece activa fuera de su turno.
**Origen:** Decisión N° 12, compensadores de riesgo · CP, Cap. 2.4 (rotación diaria) · BTT, RT-12.07 (duración máxima y revocación).
**Criterio de aceptación:** sobre una muestra de **50 credenciales**, ninguna permite el ingreso una vez cerrado el turno para el que fue emitida.

---

### `RF-ACC-03` — Zonificación del acceso · Prioridad: **Crítica**

**Descripción.** La solución **deberá** autorizar el acceso por **área, rol y ventana de tiempo**, y **no deberá** conceder acceso general al recinto por el solo hecho de la habilitación.

**Actor:** solución. **Precondición:** persona habilitada con faena asignada.
**Resultado esperado:** cada persona accede únicamente a las zonas que su faena requiere.
**Origen:** Decisión N° 12, compensadores de riesgo · CP, Cap. 10, restricción no negociable N° 7 (plan de protección) · CP, Cap. 12, materia 2 · BTT, RT-12.05.
**Criterio de aceptación:** se intenta acceder a una zona no autorizada con credencial vigente y el sistema deniega el acceso, registrando el intento con su motivo.

---

### `RF-ACC-04` — Habilitación sin biometría obligatoria · Prioridad: **Crítica**

**Descripción.** La solución **no deberá** exigir enrolamiento biométrico como condición de habilitación de ninguna persona. La solución **podrá** ofrecer biometría de forma **voluntaria y con consentimiento explícito**, sin que su rechazo afecte la habilitación.

**Actor:** trabajador eventual y personal propio. **Precondición:** ninguna.
**Resultado esperado:** habilitación plena por vía no biométrica; la biometría es una comodidad opcional, no un requisito.
**Origen:** CP, Cap. 10, restricción no negociable N° 8 («la biometría obligatoria está expresamente objetada») · **CP, Cap. 15, RT-12.11** · Decisión N° 12 · articula con RNF-SEG-10.
**Criterio de aceptación:** se completa el ciclo de habilitación de un eventual sin dato biométrico alguno, y quien rechaza la biometría voluntaria conserva idéntica habilitación.

> La Decisión N° 12 advierte que esta opción **no es la práctica dominante de la industria** —la tendencia va hacia la biometría para personal temporal— y que por eso debe quedar justificada de forma explícita por el driver sindical del caso y compensada con los controles de `RF-ACC-02`, `03`, `09` y `10`.

---

### `RF-ACC-05` — Verificación de habilitación vigente · Prioridad: **Alta**

**Descripción.** La solución **deberá** verificar, antes de emitir la credencial, que la persona cuenta con las acreditaciones vigentes que su faena exige, y **deberá** denegar la emisión registrando el motivo cuando alguna falte.

**Actor:** solución. **Precondición:** persona asignada a una faena con acreditaciones definidas.
**Resultado esperado:** nadie ingresa a una faena para la que no está acreditado.
**Origen:** CP, Cap. 4.9 (hoy la verificación de credenciales y exámenes vigentes se maneja con listados impresos) · CP, Cap. 12, materia 13 (seguridad y salud en faenas portuarias) · CP, Cap. 10, restricción no negociable N° 7.
**Criterio de aceptación:** se solicita habilitación para una persona con una acreditación vencida y la emisión se deniega con su motivo registrado.

---

### `RF-ACC-06` — Registro del ingreso y de la salida por zona · Prioridad: **Crítica**

**Descripción.** La solución **deberá** registrar el ingreso y la salida de cada persona al recinto y a cada zona controlada, con identidad, habilitación e instante.

**Actor:** solución. **Precondición:** persona con credencial vigente en un punto de control.
**Resultado esperado:** cada tránsito por un punto de control genera su evento.
**Origen:** Decisión N° 13 · CP, Cap. 18, criterio 17 · CP, Cap. 4.9 («saber cuántas hay, quiénes son y dónde están es hoy una respuesta aproximada»).
**Criterio de aceptación:** sobre un turno de peak con hasta **1.100 personas**, el **100 %** de los tránsitos por un punto de control presenta su evento con identidad, habilitación e instante.

> *Corrección aplicada: este requerimiento contenía dos conductas con pruebas independientes. La reconstrucción de la nómina se separó en `RF-ACC-11`.*

---

### `RF-ACC-07` — Conteo y ubicación por zona en emergencia · Prioridad: **Crítica**

**Descripción.** Ante una emergencia, la solución **deberá** entregar el número de personas presentes, su identidad y la **zona general** en que se encuentran, y **no deberá** mantener geolocalización individual continua dentro del patio.

**Actor:** protección portuaria y prevención de riesgos. **Precondición:** emergencia declarada.
**Resultado esperado:** respuesta inmediata a «quién está adentro y bajo qué condición», sin rastreo individual.
**Origen:** Decisión N° 13, que descarta la geolocalización continua por desproporcionada · CP, Cap. 18, criterio 17 · CP, Cap. 12, materia 11 (Ley N° 21.719) · CP, Cap. 10, restricción no negociable N° 8.
**Criterio de aceptación:** simulacro de emergencia durante la marcha blanca; el conteo entregado por el sistema coincide con el conteo físico en punto de reunión con una diferencia **≤ 1 %**, y toda diferencia queda explicada.

---

### `RF-ACC-08` — Conteo operativo sin conectividad · Prioridad: **Crítica**

**Descripción.** La solución **deberá** seguir registrando ingresos, salidas y conteo durante una pérdida de conectividad, y **deberá** resincronizar al restablecerse sin perder ningún registro.

**Actor:** solución. **Precondición:** conectividad no disponible en el punto de control.
**Resultado esperado:** el conteo de emergencia funciona precisamente cuando la infraestructura falla.
**Origen:** CP, Cap. 10, restricción no negociable N° 4 · BTT, RT-03.11. **Especialización del dominio `RF-OPD` para el dominio de acceso**, declarada para evitar duplicación.
**Criterio de aceptación:** se ejecuta el simulacro de `RF-ACC-07` con el enlace deliberadamente caído, verificando conteo correcto y resincronización íntegra al reconectar, sin pérdida de ningún evento.

> Una emergencia es un escenario en que la conectividad puede ser lo primero que falle. Un conteo que depende del enlace no sirve para el caso que justifica su existencia.

---

### `RF-ACC-09` — Auditoría de cada acceso · Prioridad: **Alta**

**Descripción.** La solución **deberá** registrar de forma auditable cada acceso concedido y cada acceso denegado, con identidad, zona, instante y motivo, y **no deberá** limitar la auditoría al acto de enrolamiento.

**Actor:** solución. **Precondición:** intento de acceso en un punto de control.
**Resultado esperado:** traza completa de accesos, no solo de altas de credencial.
**Origen:** Decisión N° 12, compensadores de riesgo («traza de auditoría de cada acceso, no solo del enrolamiento») · BTT, RT-12.09 · **CP, Cap. 15, RT-16.09** (registro de consultas a información sensible).
**Criterio de aceptación:** se consulta la auditoría de un período y se recuperan tanto los accesos concedidos como los denegados, con su motivo.

---

### `RF-ACC-10` — Eliminación de los registros de acceso al vencer la retención · Prioridad: **Alta**

**Descripción.** La solución **deberá** eliminar automáticamente los registros de acceso de personas al cumplirse el plazo de retención de **cinco años**, y **deberá** dejar constancia auditable de cada eliminación.

**Actor:** solución. **Precondición:** registro de acceso que alcanza su plazo de retención.
**Resultado esperado:** los registros no se conservan más allá de la finalidad declarada, y la eliminación es demostrable.
**Origen:** **CP, Cap. 15, RT-05.10** (registros de acceso de personas: 5 años) · CP, Cap. 12, materia 11 (Ley N° 21.719) · Decisión N° 13 · **la minimización de datos y las bases de licitud quedan en RNF-CUM-03 y RNF-SEG-05**, no aquí.
**Criterio de aceptación:** se sitúa un registro de acceso en el límite de su plazo de retención y se acredita su eliminación automática, con la constancia registrada.

> **Resuelto.** La Célula 2 confirmó que el RF queda reducido a la única conducta observable —la eliminación automática al vencer la retención, con constancia auditable— y que la **minimización de datos y las bases de licitud** son fuente única de **RNF-CUM-03** y **RNF-SEG-05**. Esta redacción ya refleja el acuerdo.

---

### `RF-ACC-11` — Reconstrucción de la nómina de presentes por zona · Prioridad: **Crítica**

**Descripción.** La solución **deberá** reconstruir la nómina de personas presentes por zona para cualquier instante de un turno, a partir de los eventos de `RF-ACC-06`.

**Actor:** protección portuaria, prevención de riesgos y jefatura de operaciones. **Precondición:** eventos de ingreso y salida registrados.
**Resultado esperado:** consulta histórica de presencia, no solo estado actual.
**Origen:** Decisión N° 13 · CP, Cap. 18, criterio 17 · BTT, RT-05.03 (reconstruir quién, qué y cuándo para cualquier registro dentro del período de retención).
**Criterio de aceptación:** se solicita la nómina para **tres instantes distintos** de un turno pasado y las tres reconstrucciones coinciden con los eventos registrados.

> *Requerimiento nuevo, separado de `RF-ACC-06`: se puede registrar correctamente y reconstruir mal, por un defecto de consulta o de manejo de zonas. Son dos pruebas.*

---

## 6. Dominio `RF-OPD` — Operación desconectada y sincronización

**Etapa 1 · 6 requerimientos.**

> **No duplicación.** La operación desconectada **del gate** está en `RF-GAT-14`, con su duración propia; la **del conteo de personas** en `RF-ACC-08`. Este dominio cubre la operación del terminal completo y remite a los dos anteriores para sus especializaciones.

> **Remisión a los RNF de disponibilidad.** Dos compromisos que originalmente se declararon como requerimientos de este dominio quedaron, por acuerdo de la Célula 2, **como fuente única en la tabla de RNF**, para no declarar dos veces el mismo umbral: la **operación de las terminales de equipo durante al menos 8 horas continuas fuera de cobertura inalámbrica** se acredita en **RNF-DIS-03**, y la **sincronización automática en no más de 90 minutos tras 72 horas de desconexión** se acredita en **RNF-DIS-04**. Ambos compromisos siguen vigentes y exigibles; lo que cambia es dónde se declaran. Los antiguos `RF-OPD-03` y `RF-OPD-04` fueron eliminados y **sus códigos no se reutilizan**.

---

### `RF-OPD-01` — Operación completa sin enlace exterior · Prioridad: **Crítica**

**Descripción.** El componente on-premise **deberá** sostener la operación completa del terminal —atención de nave, registro de movimientos, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables— durante al menos **72 horas continuas** sin enlace hacia el exterior.

**Actor:** solución. **Precondición:** enlace exterior no disponible.
**Resultado esperado:** operación íntegra, no reducida a consulta.
**Origen:** CP, Cap. 10, restricción no negociable N° 4 · **CP, Cap. 15, RT-03.10** endurece el umbral transversal de 24 a **72 horas**; prevalece el más exigente conforme al encabezado del Cap. 15 · CP, Cap. 18, criterio 18 · Decisión N° 20 · articula con RNF-DIS-02.
**Criterio de aceptación:** simulacro de corte de enlace de **72 horas** en ambiente controlado, verificando las **cinco funciones** y la ausencia de pérdida de registros. La función de gate se acredita conforme a `RF-GAT-14`.

---

### `RF-OPD-02` — Registro local íntegro durante la desconexión · Prioridad: **Crítica**

**Descripción.** Durante la desconexión, la solución **deberá** registrar localmente todas las transacciones operacionales críticas con integridad garantizada, y **no deberá** perder ningún movimiento ni ningún hecho facturable.

**Actor:** solución. **Precondición:** operación en modo desconectado.
**Resultado esperado:** registro local completo y recuperable.
**Origen:** BTT, RT-03.11 · CP, Cap. 15, RT-03.13 · CP, Cap. 10, restricción no negociable N° 4 («sin perder el registro de lo ocurrido»).
**Criterio de aceptación:** se contabilizan las transacciones generadas durante el simulacro de 72 horas y el **100 %** está presente en el registro local, con su integridad verificada.

---

### `RF-OPD-05` — Resolución determinista de conflictos de posición · Prioridad: **Crítica**

**Descripción.** La solución **deberá** resolver los conflictos de posición de contenedor producidos durante la desconexión aplicando una **regla determinista documentada**, y **no deberá** dejar la resolución a criterio del operador ni a un orden de llegada arbitrario.

**Actor:** solución. **Precondición:** conflicto de posición detectado durante la sincronización.
**Resultado esperado:** misma entrada, misma resolución, de forma reproducible.
**Origen:** **CP, Cap. 15, RT-03.13** («resolución determinista de los conflictos de posición de contenedor producidos durante la desconexión») · BTT, RT-03.12.
**Criterio de aceptación:** se inyecta el mismo conjunto de **20 conflictos** en dos ejecuciones independientes y la resolución es idéntica en los 20 casos.

---

### `RF-OPD-06` — Bitácora auditable de las decisiones de resolución · Prioridad: **Alta**

**Descripción.** La solución **deberá** dejar bitácora auditable de cada conflicto resuelto durante la sincronización, indicando el conflicto, la regla aplicada y el resultado.

**Actor:** solución. **Precondición:** sincronización ejecutada con conflictos resueltos.
**Resultado esperado:** cada resolución automática es revisable después.
**Origen:** BTT, RT-03.12 («deja bitácora auditable de las decisiones aplicadas») · BTT, RT-05.03.
**Criterio de aceptación:** tras una sincronización con conflictos, se recupera la bitácora completa con regla y resultado para el **100 %** de los conflictos resueltos.

---

### `RF-OPD-07` — Indicación del modo degradado · Prioridad: **Alta**

**Descripción.** La solución **deberá** informar a la persona usuaria que está operando en modo desconectado y qué funciones no están disponibles, y **no deberá** presentar el modo degradado como operación normal ni fallar de forma total.

**Actor:** persona usuaria de terreno y de oficina. **Precondición:** operación en modo degradado.
**Resultado esperado:** la persona sabe en qué régimen trabaja y qué no puede hacer.
**Origen:** BTT, RT-02.09 (degradación que informa a la persona usuaria) · BTT, RT-13.06 · articula con RNF-USA-07.
**Criterio de aceptación:** se induce el modo degradado y **cada interfaz afectada** lo indica explícitamente y enumera las funciones no disponibles.

> *Corrección aplicada: se retira «elegante» del cuerpo del requerimiento; se conserva solo como nombre del código en el campo Origen.*

---

### `RF-OPD-08` — Continuidad de los hechos facturables en desconexión · Prioridad: **Crítica**

**Descripción.** La solución **deberá** generar y conservar localmente los hechos facturables y su evidencia durante la desconexión, y **deberá** incorporarlos íntegramente al reconectar.

**Actor:** solución. **Precondición:** operación en modo desconectado con hechos facturables generándose.
**Resultado esperado:** ningún hecho facturable se pierde por una caída de enlace.
**Origen:** CP, Cap. 15, RT-03.10 (el registro de hechos facturables está entre las funciones que deben continuar) · CP, Cap. 15, RT-03.13 («sin pérdida de ningún movimiento ni de ningún hecho facturable») · articula con `RF-FAC-01`.
**Criterio de aceptación:** se contabilizan los hechos facturables generados durante el simulacro de 72 horas y el **100 %** se incorpora tras la sincronización, con su evidencia asociada.

---

## 7. Trazabilidad de la parte 2

| Criterio de aceptación (CP, Cap. 18) | Requerimientos |
|---|---|
| 6 — Productividad alcanzada y explicada *(causa)* | `RF-TRA-01` a `05` · `RF-PAT-13` |
| 8 — Remociones bajan de forma medible | `RF-PAT-06`, `07`, `08`, **`10`**, `11` |
| 9 — Posición coincidente, sin búsquedas físicas | `RF-PAT-01` a `05`, `12`, `13` |
| 10 — Inspección disponible a la hora *(parcial)* | `RF-PAT-10`, `11` |
| 11 — Desviación detectada en minutos | `RF-REF-01` a `10` |
| 12 — Registro continuo de temperatura | `RF-REF-11`, `12` |
| 14 — Hechos facturables con evidencia *(parcial)* | `RF-REF-13` |
| 17 — Personas presentes y su habilitación | `RF-ACC-01` a `11` |
| 18 — 72 h sin enlace | `RF-OPD-01`, `02`, `05` a `08` · RNF-DIS-03 · RNF-DIS-04 |
| 21 — Plan en cabina sin radio *(parcial)* | `RF-TRA-03` |

| Indicador de línea base | Meta | Requerimientos |
|---|---|---|
| Remociones 18 % | ≤ 14 % | `RF-PAT-06`, `07`, `08`, **`10`**, `11` |
| Contenedores mal ubicados 3,1 % | ≤ 0,5 % | `RF-PAT-01` a `04`, `13` |
| Búsqueda física 40 min | cero como proceso normal | `RF-PAT-03`, `12` |
| Equipos con terminal 12 de 18 | **74 de 74** | `RF-PAT-13` · `RF-TRA-01` |
| Intervalo de control reefer 4 h | ≤ 5 min | `RF-REF-01`, `03` |
| Tomas instrumentadas 0 de 2.400 | 2.400 | `RF-REF-01`, `04`, `05` |
| Tableros con alarma 0 de 26 | 26 | `RF-REF-06` |
| Registro continuo de temperatura: inexistente | 100 % | `RF-REF-11`, `12` |
| Productividad de grúa 24,8 mov/h | 30 | `RF-TRA-01` a `05` |
| Explicar sobretiempo: inexistente | trazable | `RF-TRA-04` |

> *Corrección aplicada 2026-09-05: `RF-PAT-10` («Programación anticipada de remociones») no figuraba en ninguna fila de esta trazabilidad pese a ser el único requerimiento que ataca el 18 % de remociones de forma anticipada, y a sostener la parte proactiva del criterio 10. Se incorpora a los criterios 8 y 10 y al indicador de remociones.*

**Total de la parte 2: 49 requerimientos** — 13 `RF-PAT`, 6 `RF-TRA`, 13 `RF-REF`, 11 `RF-ACC`, 6 `RF-OPD`.
**Acumulado original de las partes 1 y 2 antes de MC-07 a MC-14: 77 requerimientos.** El acumulado vigente se consolida en la Parte 3, sección 11.3.
**En revisión: 1** — `RF-PAT-07`.
**Eliminados por acuerdo de la Célula 2: 2** — los antiguos `RF-OPD-03` y `RF-OPD-04`, cuyos compromisos quedan acreditados por RNF-DIS-03 y RNF-DIS-04 respectivamente. Sus códigos no se reutilizan.

---

*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*
