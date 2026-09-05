# Catálogo de Requerimientos Funcionales — versión consolidada
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo B** — Catálogo de requerimientos funcionales
> **Versión 2.0** — incorpora las ocho correcciones de la Fase 4. **Reemplaza a los cinco archivos de bloque.**
> **Total: 137 requerimientos en 13 dominios.** 78 en Etapa 1, 59 en Etapa 2.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Sección | Contenido |
|---|---|
| **1** | Cómo leer este catálogo — convenciones, ficha y reglas de cita |
| **2** | **Requerimientos en revisión** — los 7 que dependen de una decisión de Isidora, con sus opciones |
| **3** | Composición por dominio y etapa |
| **4** | Cobertura de los 22 criterios de aceptación |
| **5** | Cobertura de los 28 indicadores de línea base |
| **6** | Las 17 metas comprometidas |
| **7** | Requerimientos por dominio — los 137 |
| **8** | Trazabilidad y estado |
 
---
 
## 1. Cómo leer este catálogo
 
### 1.1 Ficha de ocho campos
 
Siete los exige el CP, Cap. 17.1; el octavo lo exige la matriz de trazabilidad del mismo capítulo.
 
**Identificador · Descripción verificable · Actor · Precondición · Resultado esperado · Prioridad · Origen exacto · Criterio de aceptación.**
 
### 1.2 Criterio de clasificación funcional / no funcional
 
El CP, Cap. 17.2 deja casos limítrofes sin resolver y evalúa la **consistencia del criterio declarado**. El adoptado:
 
> **Funcional** = describe un comportamiento observable que produce un resultado.
> **No funcional** = califica *cómo* debe comportarse algo ya descrito en otra parte.
 
Ningún umbral que viva en el catálogo de RNF se repite aquí: se referencia.
 
### 1.3 Granularidad
 
> **La unidad de un requisito es la unidad de su prueba.** Si un solo procedimiento finito comprueba todas sus cláusulas, es un requisito. Si hacen falta dos pruebas independientes que pueden fallar por separado, son dos.
 
Partir por número de verbos contradiría las características 5 (concisa) y 6 (fácil de modificar) de la ERS.
 
### 1.4 Redacción
 
«Deberá» para lo obligatorio; «podrá» para lo deseable. Voz activa, sujeto explícito, términos clave en negrita. Prohibidos los verbos de interpretación múltiple —manejar, procesar, rechazar, ignorar— y las palabras subjetivas sin métrica.
 
### 1.5 Regla de cita — colisión de numeración RT
 
> **El BTT y el Capítulo 15 del CP usan los mismos códigos `RT-CC.NN` para materias distintas.** Ejemplos verificados: `RT-05.10` es «catálogo de linaje» en el BTT y «retención de datos» en el CP; `RT-16.14` es «motor de reglas» en el BTT y «firma electrónica» en el CP.
>
> **Todo código se cita con su documento de origen: «BTT, RT-XX.YY» o «CP, Cap. 15, RT-XX.YY».** El parámetro del caso se cita al CP; la obligación transversal, al BTT.
>
> Ver **Supuesto M** en `registro_supuestos_complemento_celula2.md`.
 
**Nota sobre RT-05.29 y RT-09.01:** el inventario de los 374 códigos los clasifica como no funcionales, y esa clasificación se mantiene. Aportan a los requerimientos que los citan el **umbral de verificación**, no la conducta; la conducta proviene del CP, capítulos 4, 9 y 18.
 
---
 
## 2. Requerimientos en revisión
 
> **Siete requerimientos repiten un compromiso que ya vive en el catálogo de RNF, con el mismo umbral y el mismo método de verificación.** Están **incluidos en el conteo de 137** y vigentes hasta que se resuelva.
>
> **La decisión corresponde a Isidora Cisternas**, porque la resolución afecta a su catálogo: en tres de los siete casos el compromiso quedaría viviendo únicamente en el RNF, y si ese RNF se ajustara después sin saberlo, el compromiso se perdería sin que nadie lo note.
>
> **Regla propuesta:** el RNF conserva el umbral; el RF conserva la conducta y remite. Ningún compromiso numérico se declara dos veces.
 
### 2.1 Los siete casos, con sus opciones
 
| Req. | RNF que duplica | Qué se repite | Opciones |
|---|---|---|---|
| **`RF-OPD-03`**<br>Terminales 8 h fuera de cobertura | **RNF-DIS-03** | Umbral (8 h) y método de verificación, **literalmente idénticos** | **(a) Eliminar el RF** y dejar el compromiso en RNF-DIS-03, con nota de remisión en el dominio `RF-OPD`. *Recomendada: es coherente con el Supuesto A, donde se declaró clasificar la operación desconectada como Disponibilidad.*<br>**(b) Conservar ambos** declarando expresamente en los dos catálogos que la duplicación es deliberada y por qué.<br>**(c) Reducir el RF a la conducta** —«registrar movimientos sin pérdida durante la ausencia de cobertura»— dejando el umbral de 8 h solo en el RNF |
| **`RF-OPD-04`**<br>Sincronización en 90 min | **RNF-DIS-04** | Umbral (90 min), ausencia de intervención manual y resolución determinista | Las mismas tres opciones. **Debe resolverse igual que `RF-OPD-03`**: son el mismo caso |
| **`RF-REF-08`**<br>Alarma por canal redundante | **RNF-DIS-08** | Canal redundante, escalamiento, confirmación, tres turnos | **(a) Reducir el RF a la conducta** —«enviar cada alarma simultáneamente al operador de turno y al supervisor de guardia»— dejando el umbral de 100 % de confirmación registrada en RNF-DIS-08. *Recomendada: es lo que la propia nota de RNF-DES-04 anticipaba al decir que el canal «se normó por separado en RNF-DIS-08 para no duplicar».*<br>**(b) Eliminar el RF**, con el riesgo de que la conducta de notificación simultánea quede solo como atributo de calidad.<br>**(c) Conservar ambos** con declaración expresa |
| **`RF-ACC-10`**<br>Minimización y retención de datos personales | **RNF-CUM-03** y **RNF-SEG-05** | Método de verificación idéntico («auditoría del registro de actividades de tratamiento»). **Además el RF es no funcional bajo el criterio declarado**: califica un tratamiento ya descrito en `RF-ACC-06` y `RF-ACC-09` | **(a) Reducir a la única conducta observable:** «eliminar automáticamente los registros de acceso al cumplirse los 5 años, con constancia auditable de cada eliminación». *Recomendada: es lo único que el RF aporta y que ningún RNF califica.*<br>**(b) Eliminar el RF** completo.<br>**(c) Conservarlo** asumiendo la inconsistencia de clasificación |
| **`RF-POR-07`**<br>Interfaz en español e inglés | **RNF-IDI-01** | Alcance, umbral (100 %) y método, **idénticos** | **(a) Reformular como conducta que el RNF no cubre:** «permitir a la persona usuaria seleccionar el idioma y conservar esa selección entre sesiones». *Recomendada: el multiidioma es una de las 9 categorías cerradas de RNF del CP, Cap. 17.1, de modo que la cobertura pertenece al RNF; la selección persistente es conducta y no está en ningún RNF.*<br>**(b) Eliminar el RF**.<br>**(c) Conservar ambos** |
| **`RF-PAT-07`**<br>Segregación IMDG en la asignación | **RNF-CUM-05** | Umbral (0 infracciones) y método. **Pero las conductas son distintas**: el RF describe qué hace el algoritmo, el RNF califica el cumplimiento normativo | **(a) Conservar ambos y declarar la relación**, designando **RNF-CUM-05 como fuente única para el T-12**. *Recomendada: ambos aportan y la duplicación es solo de umbral.*<br>**(b) Eliminar el RF** y dejar el cumplimiento como atributo, perdiendo la descripción de la conducta del algoritmo |
| **`RF-REF-11`**<br>Serie continua con retención 5 años | **RNF-CUM-08** | La retención de 5 años y el umbral de cobertura | **(a) Partir:** el RF conserva «mantener serie continua desde conexión hasta desconexión, sin lagunas atribuibles al sistema»; la retención y la cobertura quedan en RNF-CUM-08, citado. *Recomendada.*<br>**(b) Conservar ambos** con declaración expresa |
 
### 2.2 Efecto sobre el conteo según lo que se decida
 
| Escenario | Total |
|---|---:|
| Se conservan los siete (situación actual) | **137** |
| Se aplican todas las opciones recomendadas | **135** — se eliminan `RF-OPD-03` y `RF-OPD-04`; los otros cinco se reformulan sin cambiar el conteo |
| Se eliminan los siete | 130 |
 
### 2.3 Cómo plantear la decisión
 
Es **una sola pregunta**, no siete:
 
> *«Hay siete requerimientos funcionales que repiten un RNF tuyo con el mismo umbral y el mismo método. La regla que proponemos es que el RNF conserve el umbral y el RF remita o se reduzca a la conducta. ¿De acuerdo con la regla? ¿Y prefieres revisar los siete casos tú, o los ajusto yo con las opciones recomendadas?»*
 
---
 
## 3. Composición
 
| Dominio | Req. | Etapa | Cubre |
|---|---:|:---:|---|
| `RF-CON` — Convivencia con el sistema de 2012 | 12 | 1 | Criterios 1 y 20 |
| `RF-GAT` — Gate, citas, documentación y pesaje | 16 | 1 | Criterios 1, 2, 3, 4 |
| `RF-PAT` — Patio: posición, movimientos, asignación | 14 | 1 | Criterios 8, 9 |
| `RF-TRA` — Tractocamiones de patio | 6 | 1 | Criterios 6, 21 |
| `RF-REF` — Patio refrigerado y cadena de frío | 13 | 1 | Criterios 11, 12 |
| `RF-ACC` — Identidad, habilitación y acceso | 11 | 1 | Criterio 17 |
| `RF-OPD` — Operación desconectada y sincronización | 8 | 1 | Criterio 18 |
| `RF-NAV` — Nave, planificación y productividad | 14 | 2 | Criterios 5, 6, 7, 21, 22 |
| `RF-INT` — Integraciones y mensajería | 11 | 2 | Criterios 5, 13, 14 |
| `RF-FAC` — Hechos facturables y su evidencia | 11 | 2 | Criterio 14 |
| `RF-POR` — Portal y autoservicio | 8 | 2 | Criterio 15 |
| `RF-INS` — Inspecciones y autoridades | 7 | 2 | Criterio 10 |
| `RF-EMI` — Emisiones y consumo energético | 6 | 2 | Criterio 16 |
| **Total** | **137** | | |
 
**Etapa 1: 80 requerimientos** *(78 si se eliminan `RF-OPD-03` y `RF-OPD-04`)*. **Etapa 2: 57.**
 
**Entregable documental asociado:** **EP-01** — primera versión del registro de reglas del planificador antes del hito H2 (mes 4), validada antes del mes 12. Pertenece a la EDT del Informe 2, no a este catálogo. Sostiene el criterio de aceptación 22.
 
---
 
## 4. Cobertura de los 22 criterios de aceptación
 
**21 de 22 cubiertos.**
 
| Criterio (CP, Cap. 18) | Requerimientos | Etapa |
|---|---|:---:|
| 1 — Estadía del camión auditable | `RF-GAT-01` a `04`, `10`, `11`, `12`, `15`, `16` · `RF-CON-11` | 1 |
| 2 — Sin fila que desborde a vía pública | `RF-GAT-01`, `02`, `03`, `13`, `16` · `RF-POR-01` | 1 |
| 3 — Documentación validada antes de la ruta | `RF-GAT-03`, `04` | 1 |
| 4 — Reconocimiento automático en gate | `RF-GAT-05` | 1 |
| 5 — Ventana confirmada con 72 h | `RF-NAV-01` a `05` · `RF-INT-01` a `04` | 2 |
| 6 — Productividad alcanzada, medida y explicada | `RF-TRA-01` a `05` · `RF-NAV-12`, `13` · `RF-PAT-14` | 1 y 2 |
| 7 — Planificación sin dependencia individual | `RF-NAV-06` a `09` · EP-01 | 1 y 2 |
| 8 — Remociones bajan de forma medible | `RF-PAT-06`, `07`, `08`, `11` | 1 |
| 9 — Posición real coincidente, sin búsquedas | `RF-PAT-01` a `05`, `12`, `13` | 1 |
| 10 — Inspección disponible a la hora acordada | `RF-INS-01` a `04`, `07` · `RF-PAT-11` | 2 |
| 11 — Desviación detectada en minutos | `RF-REF-01` a `10` | 1 |
| 12 — Registro continuo de temperatura | `RF-REF-11`, `12` | 1 |
| 13 — Mensajería estándar sin digitación | `RF-INT-01` a `04`, `06`, `07` | 2 |
| 14 — Hechos facturables con evidencia | `RF-FAC-01` a `11` · `RF-REF-13` · `RF-INT-09` | 2 |
| 15 — Autoservicio sin teléfono ni mostrador | `RF-POR-01` a `08` · `RF-GAT-01`, `03` · `RF-REF-12` | 2 |
| 16 — Emisiones con método verificable | `RF-EMI-01` a `06` | 2 |
| 17 — Personas presentes y su habilitación | `RF-ACC-01` a `11` | 1 |
| 18 — 72 h sin enlace sin perder registro | `RF-OPD-01` a `08` · `RF-GAT-14` | 1 |
| **19 — Segregación de redes** | **Ninguno.** Describe un estado, no un comportamiento: **no admite requerimiento funcional.** Cubierto por **RNF-SEG-06** y por la arquitectura física del Subdocumento 4 | — |
| 20 — Indicadores del concedente trazables | `RF-CON-11` · `RF-GAT-11`, `12`, `15` | 1 |
| 21 — Plan en cabina sin radio | `RF-NAV-10`, `11` · `RF-TRA-03` | 1 y 2 |
| 22 — Continuidad tras la jubilación | `RF-NAV-06` a `09` · EP-01 | 1 y 2 |
 
**Doce criterios quedan satisfechos en el mes 16**, incluidos los cuatro que inciden sobre la estadía del camión — el indicador comprometido con el concedente que acumula tres semestres sobre el umbral.
 
---
 
## 5. Cobertura de los 28 indicadores de línea base
 
Los 28 tienen requerimiento que los mueve, **salvo dos declarados deliberadamente sin meta**: la ocupación del patio en peak, que la solución no puede mover y se usa como parámetro de dimensionamiento; y la pérdida del evento del 18 de febrero, que es un hecho ocurrido y no una serie.
 
| Indicador | Base | Meta | Requerimientos |
|---|---|---|---|
| Ventana de atraque | 71 % | 90 % | `RF-NAV-01` a `05` |
| Productividad de grúa | 24,8 mov/h | 30 | `RF-TRA-01` a `05` · `RF-NAV-12` |
| Instrucciones digitadas | 41 % | **≤ 5 %** | `RF-INT-02`, `07` |
| Formatos de plano de estiba | 6 | estándar único | `RF-INT-01`, `06` |
| Personas que planifican | 1 | — | `RF-NAV-06` a `09` |
| Registro por hora y grúa | inexistente | continuo | `RF-NAV-12` · `RF-PAT-14` |
| Explicar sobretiempo | inexistente | trazable | `RF-NAV-13` · `RF-TRA-04` |
| Semestres sobre umbral | 3 | cero | `RF-GAT-12`, `15` |
| Remociones | 18 % | **≤ 14 %** | `RF-PAT-06`, `07`, `08`, `11` |
| Contenedores mal ubicados | 3,1 % | **≤ 0,5 %** | `RF-PAT-01` a `04`, `13` |
| Búsqueda física | 40 min | **cero como proceso normal** | `RF-PAT-03`, `12` |
| Ocupación del patio | 90 % | **sin meta** | parámetro de dimensionamiento |
| Equipos con terminal | 12 de 18 | **74 de 74** | `RF-PAT-13` · `RF-TRA-01` |
| Intervalo de control reefer | 4 h | **≤ 5 min** | `RF-REF-01`, `03` |
| Tomas instrumentadas | 0 de 2.400 | **2.400** | `RF-REF-01`, `04`, `05` |
| Tableros con alarma | 0 de 26 | **26** | `RF-REF-06` |
| Registro continuo de temperatura | inexistente | **100 %** | `RF-REF-11`, `12` |
| Evento del 18 de febrero | US$ 620.000 | **sin meta** | prevención vía `RF-REF-01` a `12` |
| Inspecciones atrasadas | 28 % | **≤ 12 %** condicionada | `RF-INS-01` a `04`, `07` |
| Estadía del camión | 78 min | 45 | `RF-GAT-01` a `05`, `10`, `16` |
| Fila máxima | 3,2 km | cero | `RF-GAT-01`, `02`, `13`, `16` |
| Documentación defectuosa | 22 % | bajo 5 % | `RF-GAT-03`, `04` |
| Sistema de citas | inexistente | operativo | `RF-GAT-01`, `02`, `16` |
| Lectura automática en gate | inexistente | **≥ 98 %** | `RF-GAT-05`, `06` |
| Discrepancia de masa bruta | 6 % | bajo 1 % | `RF-GAT-08`, `09` |
| Facturas objetadas | 4,7 % | bajo 1 % | `RF-FAC-01` a `07` |
| Objeciones por falta de evidencia | 62 % | cero | `RF-FAC-06`, `09` |
| Emisiones por contenedor | no se mide | reporte verificado | `RF-EMI-01` a `06` |
 
---
 
## 6. Las 17 metas comprometidas
 
Detalle, derivación y evidencia en `registro_supuestos_complemento_celula2.md` y `correcciones_fase4_tractocamion_metas.md`.
 
| Meta | Valor | Fundamento |
|---|---|---|
| Remociones | ≤ 14 % | Bütün et al. (2026), Vigo; Kim y Yi (2021), Busan. **Advertencia:** Zając (2026) documenta que a alta ocupación la ventaja del algoritmo se comprime. Se compromete medida fuera del peak |
| Contenedores mal ubicados | ≤ 0,5 % | Estimación propia alineada al umbral de conciliación de la Decisión N° 1. Depende de la verificación cruzada óptica, no del posicionamiento solo (Dahiya et al., 2026) |
| Búsqueda física | cero como proceso normal; residual ≤ 0,5 % en ≤ 15 min | Criterio de aceptación 9 |
| Equipos instrumentados | 74 de 74 | Condición de la Decisión N° 15 |
| Intervalo de control reefer | ≤ 5 min | CP, Cap. 15, RT-05.29. **El beneficio comprometido es cobertura sin ventana ciega**, no el umbral |
| Tomas instrumentadas | 2.400 de 2.400 | Cobertura total; parcial reproduce el modo de falla del 18 de febrero |
| Tableros con alarma | 26 de 26 | El evento fue falla de un tablero completo |
| Registro continuo de temperatura | 100 %, retención 5 años | CP, Cap. 15, RT-05.10 |
| Inspecciones atrasadas | ≤ 12 %, condicionada | Sin evidencia arbitrada; Klar et al. (2024) documentan trade-off con la meta de remociones |
| Reconocimiento óptico | ≥ 98 % | 100 % es inalcanzable con placa sucia y luz variable |
| Carril de excepción | ≥ 50 % más lento | Decisión N° 7: si no es «claramente peor», no hay incentivo |
| Prioridad por cita cumplida | ≥ 30 % más rápido | La adopción decide el resultado del sistema de citas |
| Instrucciones digitadas | ≤ 5 % al cierre de Etapa 2 | Residual atribuible a navieras en canal puente |
| Reconciliación de combustible | ± 3 % en 3 meses | Tolerancia de flujómetro |
| Error del barrido de inventario | ≤ 0,5 % | Alineado a la meta de posición |
| Ocupación del patio | **sin meta** | No accionable por la solución |
| Evento del 18 de febrero | **sin meta** | Hecho ocurrido, no serie |
 
---
 
## 7. Requerimientos por dominio
 
> Las fichas completas de los 137 requerimientos, con sus ocho campos, están en los cinco archivos de bloque, **corregidas conforme a las ocho correcciones de la Fase 4**. Esta sección lista los identificadores y su materia para navegación; el detalle no se duplica aquí.
 
**`RF-CON` — Convivencia (12, Etapa 1).** 01 fachada de servicios única · 02 contrato de interfaz versionado *(cita **BTT, RT-05.17**, no RT-05.16)* · 03 escritura dual *(ventana de desfase: 60 s provisional)* · 04 apagado con doble aprobación · 05 conciliación por turno · 06 clasificación direccional de divergencias · 07 detención automática del avance · 08 reversión por enrutamiento *(15 min: compromiso propio, más exigente que el BA Art. 78.2)* · 09 barrido de bloques *(error ≤ 0,5 %)* · 10 observabilidad de convivencia · 11 indicadores del concedente trazables · **12 declaración de frontera parametrizable** *(BTT, RT-16.04)*
 
**`RF-GAT` — Gate (16, Etapa 1).** 01 solicitud de cita · 02 prioridad por cita cumplida *(≥ 30 %; «cita cumplida» definida en RN-07)* · 03 validación documental anticipada · 04 carril de excepción *(≥ 50 % más lento)* · 05 reconocimiento óptico *(≥ 98 %)* · 06 identificación por patente · 07 habilitación del conductor · 08 captura de masa bruta · 09 discrepancia sobre tolerancia *(5 % según RN-05, con dos ejemplos numéricos)* · 10 instrucción de destino · 11 eventos de barrera · 12 cálculo trazable de estadía · 13 estado de congestión · 14 gate sin enlace exterior · 15 conciliación con umbral cero · **16 límite de franjas por capacidad declarada**
 
**`RF-PAT` — Patio (14, Etapa 1).** 01 posicionamiento automático · 02 verificación cruzada óptica · 03 estado de confianza · 04 tarea de verificación física · 05 movimiento sin confirmación · 06 asignación algorítmica *(orden en RN-01)* · 07 segregación IMDG *(RN-02)* ⚠ *en revisión* · 08 condiciones dinámicas · 09 instrucción sin interacción · **10 vía de excepción con interlock de equipo detenido** · 11 remoción anticipada *(generaliza la Decisión N° 21)* · 12 consulta de posición *(≤ 1 s)* · 13 cobertura de instrumentación *(74 equipos)* · 14 movimientos por hora y equipo
 
**`RF-TRA` — Tractocamiones (6, Etapa 1).** 01 posicionamiento de los 42 equipos · 02 asignación a movimiento de grúa · 03 tiempo estimado de arribo en cabina *(error ≤ 60 s)* · 04 registro de detención por espera de equipo · 05 reasignación ante indisponibilidad *(≤ 30 s)* · 06 registro de traslados
 
**`RF-REF` — Patio refrigerado (13, Etapa 1).** 01 muestreo local 1-5 min · 02 agregación y reporte 5-15 min · 03 envío inmediato ante excepción · 04 desviación de temperatura *(≤ 5 min)* · 05 desconexión de toma · 06 falla de tablero como evento propio · 07 sensor caído *(3 intervalos sin lectura)* · 08 notificación simultánea ⚠ *en revisión* · 09 escalamiento automático · 10 confirmación registrada · 11 serie continua ⚠ *en revisión* · 12 entrega de evidencia de cadena de frío · 13 horas de conexión facturables *(RN-10: tiempo conectado efectivo, con dos ejemplos numéricos)*
 
**`RF-ACC` — Identidad y acceso (11, Etapa 1).** 01 credencial temporal por nombrada · 02 expiración automática · 03 zonificación · 04 sin biometría obligatoria · 05 verificación de habilitación · 06 registro de ingreso y salida · 07 conteo por zona en emergencia · 08 conteo sin conectividad · 09 auditoría de cada acceso · 10 retención de datos personales ⚠ *en revisión* · **11 reconstrucción de nómina por zona** *(partido de 06)*
 
**`RF-OPD` — Operación desconectada (8, Etapa 1).** 01 operación completa 72 h · 02 registro local íntegro · 03 terminales 8 h fuera de cobertura ⚠ *en revisión* · 04 sincronización 90 min ⚠ *en revisión* · 05 resolución determinista de conflictos · 06 bitácora auditable · 07 indicación de modo degradado · 08 continuidad de hechos facturables
 
**`RF-NAV` — Nave y planificación (14, Etapa 2).** 01 recepción de recalada · 02 programación de sitios · 03 confirmación con 72 h · 04 notificación registrada de cambio · 05 estimación por serie histórica · 06 propuesta automática *(precedencia en RN-09; 20 recaladas históricas)* · 07 aprobación del planificador · 08 motivo estructurado de corrección · 09 registro de reglas del planificador *(la mitad documental pasó a EP-01)* · 10 plan en cabina · 11 actualización sin interacción · 12 productividad en tiempo real *(no desde el sistema del fabricante)* · 13 explicación del sobretiempo · 14 replanificación por masa bruta
 
**`RF-INT` — Integraciones (11, Etapa 2).** 01 **BAPLIE** · 02 **COPRAR** *(≤ 5 % digitado)* · 03 **COARRI** · 04 **CODECO** · 05 validación de integridad y origen · 06 versionado por naviera *(SMDG)* · 07 canal puente · 08 identificación **ISO 6346** con dígito verificador · 09 entrega de hechos facturables al ERP · 10 integración con autoridades · 11 correlación de integraciones
 
**`RF-FAC` — Hechos facturables (11, Etapa 2).** 01 generación en el instante · 02 regla parametrizable por tipo *(ancla en BTT, RT-16.02)* · 03 días de almacenaje *(RN-04, con dos ejemplos numéricos)* · 04 movimientos adicionales · 05 pesaje, inspección y carga peligrosa · 06 evidencia inalterable · 07 prohibición de edición manual · 08 presentación de objeción · 09 resolución con evidencia · 10 conciliación diaria con umbral cero · 11 retención de 6 años
 
**`RF-POR` — Portal (8, Etapa 2).** 01 capa pública · 02 registro y recuperación autoservidos · 03 consulta autenticada · 04 segregación de visibilidad · 05 objeción en línea · 06 coordinación de inspección · 07 español e inglés ⚠ *en revisión* · 08 autoatención con medición del desvío *(BTT, RT-16.33)*
 
**`RF-INS` — Inspecciones (7, Etapa 2).** 01 recepción normalizada · 02 registro de cita con hora acordada · 03 reserva con remoción programada *(holgura parametrizable, valor inicial 4 h)* · 04 alerta de riesgo de incumplimiento · 05 registro de la atención · 06 acta con firma electrónica *(«acta de inspección conjunta» no definida en el caso; interpretación amplia declarada)* · 07 medición del cumplimiento
 
**`RF-EMI` — Emisiones (6, Etapa 2).** 01 consumo de equipos diésel *(± 3 % en 3 meses)* · 02 consumo de equipos eléctricos · 03 cálculo por contenedor *(**ISO 14083:2023** vía **GLEC v3.2**, verificado bajo **ISO 14064-3**; dos ejemplos numéricos)* · 04 trazabilidad hasta el origen · 05 serie histórica *(≥ 24 meses)* · 06 exportación para verificación por tercero
 
---
 
## 8. Trazabilidad y estado
 
### 8.1 Documentos que este catálogo referencia
 
| Documento | Qué aporta |
|---|---|
| `RNF.md` | Los 77 requerimientos no funcionales. **Conserva los umbrales** de todo compromiso duplicado |
| `registro_supuestos_decisiones_02_20.md` | Decisiones N° 2 a 20 |
| `01_decision_01_tos_2012_registro_final.md` | Decisión N° 1 y los requerimientos que introduce |
| `registro_supuestos_complemento_celula2.md` | Decisión N° 21, las metas, supuestos de alcance |
| `registro_reglas_de_negocio.md` | RN-01 a RN-08 |
| `complemento_reglas_negocio_y_rf_pat_10.md` | RN-09, RN-10, fundamento corregido de RN-03, supuesto de `RF-PAT-10` |
| `inventario_RT_bases_tecnicas_transversales.md` | Los 374 códigos RT clasificados |
| `alcance_etapas_exclusiones_subdoc3.md` | Secciones 3.4 a 3.8 |
| `grupos_interes_y_cierre_pendientes.md` | Sección 3.9 y decisiones adoptadas |
 
### 8.2 Estado
 
| Concepto | Estado |
|---|---|
| Requerimientos | **137** — 130 firmes y 7 en revisión (sección 2) |
| Criterios de aceptación cubiertos | 21 de 22 |
| Indicadores con requerimiento | 26 de 28; 2 sin meta declarada |
| Metas comprometidas | 17 |
| Pasada IEEE 830 | **Aplicada** |
| Verificación de citas | **Aplicada** — revisión independiente |
| Números de página en las citas | **Pendiente** — BA, Art. 43.2 lo exige antes del T-12 |
| Formulario T-12 | Pendiente. Regla de fuente única resuelta |
| Matriz de trazabilidad | Pendiente — dos columnas dependen de Célula 3 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*