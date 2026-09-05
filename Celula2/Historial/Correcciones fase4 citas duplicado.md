# Correcciones de la Fase 4 — Citas normativas y duplicación con el catálogo de RNF
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Origen:** correcciones 3 y 4 del plan de Fase 4, derivadas de la revisión adversarial independiente del catálogo de 128 RF.
> **Estado:** la sección 3 son correcciones ejecutables por Célula 2. **La sección 4 requiere decisión conjunta con Isidora Cisternas**, porque toca el catálogo de RNF.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Sección | Contenido | Qué resuelve |
|---|---|---|
| **1** | Resumen de hallazgos | Qué encontró la revisión y qué gravedad tiene cada cosa |
| **2** | **La colisión de numeración RT** | El BTT y el CP Cap. 15 usan los mismos códigos para materias distintas. Regla de cita adoptada y supuesto declarado |
| **3** | Correcciones de cita puntuales | `RF-CON-02` (código equivocado), `RF-CON-08` (sobreextensión del BA), siete RF que citan códigos no funcionales, ISO 6346 y mensajes EDIFACT sin nombrar, `RF-PAT-11` sobreextendido, RT-16.04 ausente |
| **4** | **Los siete duplicados con el catálogo de RNF** | Análisis uno por uno, regla propuesta y qué decide Isidora |
| **5** | Efecto sobre el conteo y sobre el T-12 | Por qué esto importa antes de construir la matriz |
| **6** | Pendientes que no cierran aquí | Lo que queda para las correcciones 5 a 8 |
 
---
 
## 1. Resumen de hallazgos
 
La revisión verificó el 100 % de las citas a restricciones no negociables, criterios de aceptación numerados e indicadores de línea base, y aproximadamente el 85 % de las citas a códigos RT.
 
**No se encontró ninguna cita inexistente.** Ningún código inventado, ningún artículo que no exista. Lo que sí hay:
 
| Tipo | Cantidad | Gravedad |
|---|---:|---|
| Colisión de numeración RT no declarada | 1 sistémica, afecta ~10 citas | **Alta** |
| Código desplazado (se cita uno por otro) | 1 | **Alta** |
| Sobreextensión (la base dice menos de lo que se le atribuye) | 5 | Alta a baja |
| Clase que no calza (RT no funcional citado como origen de un RF) | 7 | Media |
| Norma o mensaje que el CP nombra y el catálogo no | 5 | Media |
| Código obligatorio del BTT no citado en ningún RF | 1 (RT-16.04) | **Alta** |
| RF que duplican un RNF con umbral y método idénticos | 7 | **Alta** |
 
---
 
## 2. La colisión de numeración RT
 
### 2.1 El hallazgo
 
**El BTT y el Capítulo 15 del CP usan los mismos códigos `RT-CC.NN` para materias distintas.** Verificado contra ambos textos:
 
| Código | En el BTT | En el CP, Cap. 15 |
|---|---|---|
| `RT-03.10` | Operación desconectada: **24 horas** sin enlace con la nube | Operación desconectada: **mínimo 72 horas** sin enlace exterior |
| `RT-05.10` | Catálogo de datos con linaje automatizado — **Deseable** | **Retención** de datos históricos y de auditoría |
| `RT-16.14` | **Motor de reglas** sin recompilación — **Deseable** | **Firma electrónica** |
| `RT-16.21` | **Plantillas** de notificación versionadas | **Canales** de notificación redundantes con escalamiento |
| `RT-16.30` | Auditoría de **exportaciones** de información sensible | **Portal público** |
| `RT-21.06` | (el BTT usa `RT-21.07` para esta materia) | **Horario** del centro de atención |
 
No es un error de las bases: el CP, Cap. 15 declara que fija los valores del caso para los requisitos «Según caso» y que «cuando este capítulo endurece un umbral del documento transversal, prevalece el más exigente». Pero **la correspondencia de códigos no es uno a uno**, y el catálogo navegó esa colisión sin declararla, atribuyendo en varios puntos a un documento lo que dice el otro.
 
### 2.2 Regla de cita adoptada
 
> **Todo código RT se cita con su documento de origen explícito y sin excepción: «BTT, RT-XX.YY» o «CP, Cap. 15, RT-XX.YY».**
>
> Cuando la materia invocada sea el **parámetro del caso** —un umbral, un valor, un alcance concreto—, la cita es siempre **al CP, Cap. 15**, aunque el código exista también en el BTT con otro contenido.
>
> Cuando la materia invocada sea la **obligación transversal** —la conducta genérica exigida a toda solución—, la cita es al **BTT**.
>
> Cuando un requerimiento se apoye en ambos, se citan ambos, en ese orden, y se declara cuál aporta la conducta y cuál el umbral.
 
### 2.3 Supuesto declarado
 
Esta indeterminación habría sido consulta admisible bajo el BA, Art. 43.4 —es una ambigüedad de los propios textos normativos, no un asunto derivable por ingeniería—. Cerrado el período de consultas (BA, Art. 43.1), se declara como supuesto:
 
> **Supuesto M — Correspondencia de códigos RT entre el BTT y el Capítulo 15 del CP.**
>
> **Decisión.** Terabyte interpreta que el Capítulo 15 del CP **no renumera** los códigos del BTT sino que fija los parámetros del caso para requisitos «Según caso», y que cuando un mismo código aparece en ambos documentos con materias distintas, **ambas obligaciones son exigibles y acumulativas**, no alternativas.
>
> **Fundamento.** BA, Art. 5.3 y 5.4 obligan a adoptar la interpretación más exigente ante ambigüedad. La lectura acumulativa es la más exigente: obliga a cumplir la conducta transversal del BTT **y** el parámetro del caso.
>
> **Alternativas consideradas.** Interpretar que el CP renumera y sustituye al BTT en esos códigos, lo que dejaría sin cumplir obligaciones transversales vigentes; o interpretar que solo rige el BTT, lo que ignoraría los parámetros del caso.
>
> **Impacto si resulta equivocada.** Ninguno adverso: el error sería por exceso de cumplimiento. Si la lectura correcta fuera la sustitutiva, Terabyte habrá comprometido capacidades adicionales no exigidas.
>
> **Instancia de validación.** Reunión de aclaración con la Contraparte Técnica al inicio del contrato, o Acta de Respuestas a Consultas si el CLIENTE emite aclaración de oficio conforme al BA, Art. 44.1.
>
> **Responsable.** Terabyte.
 
### 2.4 Citas corregidas por aplicación de la regla
 
| Requerimiento | Cita actual | Cita corregida |
|---|---|---|
| `RF-CON-11`, `RF-REF-11`, `RF-FAC-11`, `RF-ACC-10` | «RT-05.10» con contenido de retención | **CP, Cap. 15, RT-05.10** |
| `RF-GAT-08` | «CP, RT-05.10» — sin capítulo | **CP, Cap. 15, RT-05.10** |
| `RF-REF-08` | «CP, Cap. 15, RT-16.21 (alarmas redundantes…)» y «BTT, RT-16.20» | **CP, Cap. 15, RT-16.21** aporta la exigencia de canal redundante y escalamiento; **BTT, RT-16.20** aporta la conducta de notificación multicanal. Ambas, en ese orden |
| `RF-INS-06` | «CP, Cap. 15, RT-16.14» y «BTT, RT-16.17 y RT-16.18» | Correcto, pero se añade nota: *el código RT-16.14 corresponde en el BTT a otra materia (motor de reglas, Deseable); la exigencia de firma proviene del CP y la conducta de firma electrónica de BTT, RT-16.17 y RT-16.18* |
| `RF-POR-01` | «CP, Cap. 15, RT-16.30» y «BTT, RT-16.31» | Ambas correctas. Se añade la exigencia bilingüe de la capa pública que el CP incluye y el requerimiento omitía — cubierta por `RF-POR-07` |
| `RF-GAT-14`, `RF-OPD-01` | «CP, Cap. 15, RT-03.10 (72 horas)» y «BTT, RT-03.11» | Se añade nota de prevalencia: *el CP endurece el umbral transversal de 24 a 72 horas; prevalece el más exigente conforme al encabezado del Cap. 15* |
 
---
 
## 3. Correcciones de cita puntuales
 
### 3.1 `RF-CON-02` — código desplazado
 
**Defecto.** Cita **BTT, RT-05.16** para sostener «contrato de interfaz versionado semánticamente». RT-05.16 en el BTT es la documentación de servicios en OpenAPI 3.1 y AsyncAPI 2.6, no el versionado. El código correcto es **RT-05.17**: «Los contratos de interfaz se versionarán semánticamente, con compatibilidad hacia atrás y política de obsolescencia con preaviso mínimo de seis meses.»
 
Agrava el defecto que `RF-INT-06` **sí** cita RT-05.17 correctamente: es inconsistencia interna del catálogo, no un error de lectura de las bases.
 
**Corrección.** Origen pasa a: **BTT, RT-05.17** (versionado semántico, Obligatorio) · **BTT, RT-05.20** (capa anticorrupción) · **BTT, RT-05.16** como refuerzo, para la obligación de documentar el contrato.
 
Efecto colateral positivo: RT-05.17 es Obligatorio, de modo que el «deberá» del requerimiento queda correctamente anclado.
 
### 3.2 `RF-CON-08` — sobreextensión del BA, Art. 78.2
 
**Defecto.** El requerimiento compromete la reversión completa en **15 minutos desde la decisión** y lo presenta como derivado del BA, Art. 78.2. Verificado: ese artículo fija, para severidad crítica, **15 minutos de tiempo de respuesta** y **4 horas de tiempo de resolución**. Anclar la *restitución* en el número de *respuesta* es más exigente que la base, lo cual es defendible como compromiso propio, pero **no puede presentarse como si la base lo impusiera**.
 
**Corrección del campo Origen:**
 
> **CP, 13.3 punto 5** y **CP, 17.6 punto 5** (retorno probado por dominio) · **Decisión N° 1**, tiempos de reversión. **El objetivo de 15 minutos para la restitución es un compromiso propio de Terabyte, más exigente que el tiempo de respuesta de 15 minutos y muy por debajo del tiempo de resolución de 4 horas que el BA, Art. 78.2 fija para severidad crítica.** El fundamento del compromiso es operacional y no normativo: cuatro horas con una nave amarrada equivalen, a 24,8 movimientos por hora de grúa, a un centenar de movimientos perdidos.
 
Es un cambio que **fortalece** la propuesta: pasa de parecer una derivación forzada a ser un compromiso deliberado y explicado.
 
### 3.3 Siete requerimientos que citan códigos RT no funcionales
 
`RF-REF-01`, `RF-REF-03`, `RF-REF-04`, `RF-PAT-14`, `RF-NAV-12`, `RF-CON-11` y `RF-GAT-12` citan **RT-05.29**; `RF-PAT-02`, `RF-PAT-12`, `RF-GAT-05` y `RF-GAT-10` citan **RT-09.01**. Nuestro propio inventario de los 374 códigos clasifica ambos como **no funcionales**.
 
No es un error de cita —los códigos dicen lo que se les atribuye— pero deja una incoherencia visible entre dos entregables de Terabyte.
 
**Corrección.** Nota fija en el encabezado de los cinco bloques del catálogo:
 
> **Sobre los códigos RT-05.29 y RT-09.01.** El inventario de los 374 códigos del BTT los clasifica como no funcionales, y esa clasificación se mantiene. Ambos aportan a estos requerimientos el **umbral de verificación**, no la conducta. La conducta proviene del CP, capítulos 4, 9 y 18. Un requerimiento funcional puede citar un código no funcional como fuente de su umbral sin que ello altere su clasificación — es exactamente el caso limítrofe que el CP, Cap. 17.2 plantea y cuya resolución consistente se evalúa.
 
### 3.4 Normas y mensajes que el CP nombra y el catálogo no
 
El CP, num. 16.2 advierte que quien «prometa mensajería estándar sin haber identificado un solo mensaje por su nombre» quedará en evidencia. El catálogo nombra los mensajes solo entre paréntesis, en la referencia a la Decisión N° 18, y nunca en el cuerpo del requerimiento.
 
| Requerimiento | Se añade al cuerpo |
|---|---|
| `RF-INT-01` | **BAPLIE** (UN/EDIFACT), plano de estiba |
| `RF-INT-02` | **COPRAR**, orden de embarque |
| `RF-INT-03` | **COARRI**, confirmación de carga y descarga |
| `RF-INT-04` | **CODECO**, notificación de movimiento |
| `RF-INT-08` | **ISO 6346**, con estructura de código y dígito verificador |
| `RF-INT-06` | Mantenimiento del catálogo por **SMDG**, y versión soportada declarada por naviera |
| `RF-EMI-03` | **ISO 14083:2023**, implementada mediante **GLEC Framework v3.2**, verificada bajo **ISO 14064-3** — ya resueltas en la Decisión N° 16 y no recogidas por el requerimiento |
 
El caso de `RF-EMI-03` es el más costoso de los siete: la Decisión N° 16 hizo el trabajo de determinar la jerarquía normativa correcta —incluso corrigiendo una versión anterior que la tenía invertida— y el requerimiento decía solo «la metodología declarada», perdiendo el activo.
 
### 3.5 `RF-PAT-11` — alcance sobreextendido respecto de su origen
 
**Defecto.** El requerimiento cita la **Decisión N° 21**, cuyo objeto es la coordinación de inspecciones, pero extiende la programación anticipada de remociones a «retiro con cita» y «embarque planificado», que esa decisión no cubre.
 
**Corrección.** Se mantiene el alcance ampliado —es correcto: el mecanismo sirve igual para los tres compromisos con hora cierta— y se declara la generalización en el campo Origen:
 
> **Decisión N° 21** funda el mecanismo para inspecciones. Terabyte lo **generaliza** a todo compromiso con hora cierta —retiro con cita (Decisión N° 6, RN-07) y embarque planificado (Decisión N° 4)— por identidad de razón: en los tres casos existe un tercero con una hora acordada y un contenedor que puede estar bloqueado. La generalización se declara como supuesto de alcance.
 
### 3.6 RT-16.04 — código obligatorio no citado en ningún requerimiento
 
**El hallazgo más costoso de esta corrección.** BTT, RT-16.04 exige:
 
> «El PROPONENTE declarará expresamente qué elementos son parametrizables y cuáles requieren desarrollo. **Presentar como parametrizable lo que exige desarrollo se evaluará como observación grave.**»
 
El catálogo declara parametrizable, en distintos requerimientos, las reglas de facturación (`RF-FAC-02`), las condiciones dinámicas de patio (`RF-PAT-08`), los plazos de escalamiento (`RF-REF-09`), la holgura de inspección (`RF-INS-03`), las franjas de cita y los umbrales de conciliación — **sin ninguna declaración de frontera**.
 
**Corrección.** Requerimiento nuevo, `RF-CON-12`, ubicado en el dominio transversal:
 
> **`RF-CON-12` — Declaración de frontera entre parametrización y desarrollo** · Prioridad: **Crítica**
>
> **Descripción.** La solución **deberá** exponer al CLIENTE el inventario de elementos parametrizables desde la interfaz, con su tipo de dato, rango admisible y perfil autorizado, y Terabyte **deberá** declarar en la propuesta qué elementos requieren desarrollo y no parametrización.
> **Actor:** CLIENTE. **Precondición:** solución desplegada.
> **Resultado esperado:** el CLIENTE puede distinguir, sin consultar a Terabyte, qué puede cambiar por sí mismo y qué requiere una solicitud de cambio.
> **Origen:** **BTT, RT-16.04** (Obligatorio, con sanción explícita) · **BTT, RT-16.02** · CP, Cap. 10, restricción no negociable N° 11 (el área de TI del CLIENTE son cinco personas).
> **Criterio de aceptación:** el inventario publicado coincide con los elementos efectivamente parametrizables, verificado modificando una muestra de **10 parámetros declarados** desde la interfaz sin intervención de Terabyte, y comprobando que ningún elemento declarado como parametrizable requirió desarrollo.
 
Este requerimiento además responde a la tensión que la revisión detectó con la restricción N° 11: el catálogo presupone administración continua por parte de un equipo de TI de cinco personas, y RT-16.04 obliga a declarar exactamente dónde está esa carga.
 
**Conteo: 129 requerimientos.**
 
---
 
## 4. Los siete duplicados con el catálogo de RNF
 
> **Esta sección no se ejecuta sin Isidora.** Cuatro de los siete casos se resuelven modificando el RF; tres podrían requerir tocar el RNF, que es su trabajo.
 
### 4.1 Por qué importa resolverlo antes del T-12
 
El Formulario T-12 traza requisito por requisito contra los 374 códigos RT. Si un mismo compromiso aparece como RF y como RNF con umbral y método idénticos, **se cuenta dos veces**, y la Comisión ve dos entregables del mismo equipo diciendo lo mismo con identificadores distintos. Es el «conflicto entre términos» que el material de redacción del curso identifica como una de las tres formas de romper la consistencia.
 
### 4.2 Regla propuesta
 
> **El RNF conserva el umbral. El RF conserva la conducta y remite al RNF para el umbral. Ningún compromiso numérico se declara dos veces.**
>
> Donde el RF no aporte conducta distinta de la que el RNF ya califica, el RF se elimina y el criterio de aceptación correspondiente queda íntegramente en el RNF.
 
### 4.3 Los siete casos
 
| # | RF | RNF | Diagnóstico | Resolución propuesta | Decide |
|---:|---|---|---|---|---|
| 1 | `RF-POR-07` — interfaz en español e inglés | **RNF-IDI-01** | **Duplicación total.** Mismo alcance, mismo umbral (100 %), mismo método (auditoría de cobertura de idioma sobre el catálogo de pantallas y plantillas) | **Reformular el RF como conducta que el RNF no cubre:** «la solución **deberá** permitir a la persona usuaria seleccionar el idioma de la interfaz y **deberá** conservar esa selección entre sesiones». El umbral de cobertura queda solo en RNF-IDI-01 | Célula 2 |
| 2 | `RF-OPD-03` — terminales 8 h fuera de cobertura | **RNF-DIS-03** | **Duplicación total**, incluido el método de verificación literal | **Caso del Supuesto A.** Isidora ya declaró que clasificar la operación desconectada como Disponibilidad es una decisión adoptada ante un caso limítrofe que el CP, Cap. 17.2 deja abierto. Se propone **eliminar `RF-OPD-03`** y dejar el compromiso en RNF-DIS-03, declarando la remisión en el dominio `RF-OPD` | **Isidora** |
| 3 | `RF-OPD-04` — sincronización en 90 minutos | **RNF-DIS-04** | **Duplicación total** | Igual que el anterior: eliminar el RF, conservar RNF-DIS-04 | **Isidora** |
| 4 | `RF-REF-08` — alarma por canal redundante | **RNF-DIS-08** | **Duplicación total.** Agravante: RNF-DES-04 lleva una nota que dice que el canal y su confirmación «se normaron por separado en RNF-DIS-08 **para no duplicar** la misma restricción en dos categorías» — y el catálogo de RF lo duplicó igual | **Conservar el RF, reducido a la conducta:** «la solución **deberá** enviar cada alarma simultáneamente al operador de turno y al supervisor de guardia». El umbral de 100 % de confirmación registrada queda en RNF-DIS-08. `RF-REF-09` y `RF-REF-10` sí aportan conducta propia (escalamiento y registro) y se mantienen | **Isidora** |
| 5 | `RF-PAT-07` — segregación IMDG en la asignación | **RNF-CUM-05** | **Duplicación de umbral y método**, pero conductas distintas: el RF describe qué hace el algoritmo, el RNF califica el cumplimiento normativo | **Conservar ambos, declarando la relación.** El RF cita RN-02 y la batería de casos; el RNF conserva el umbral de cero infracciones. **Declarar RNF-CUM-05 como fuente única para el T-12**, para no contar dos veces | Célula 2 |
| 6 | `RF-REF-11` — serie continua con retención de 5 años | **RNF-CUM-08** | **Duplicación parcial.** La retención es atributo de calidad; la serie continua es conducta | **Partir el RF:** conserva «mantener serie continua desde conexión hasta desconexión, sin lagunas atribuibles al sistema»; la retención de 5 años y su umbral de cobertura quedan en RNF-CUM-08, citado | Célula 2 |
| 7 | `RF-ACC-10` — minimización y retención de datos personales | **RNF-CUM-03** y **RNF-SEG-05** | **Duplicación total del método** («auditoría del registro de actividades de tratamiento»), y además el RF es **no funcional bajo nuestro propio criterio**: califica cómo se comporta un tratamiento ya descrito en `RF-ACC-06` y `RF-ACC-09` | **Reducir a la única conducta observable:** «la solución **deberá** eliminar automáticamente los registros de acceso de personas al cumplirse el plazo de retención de 5 años, y **deberá** dejar constancia auditable de cada eliminación». Cumplimiento normativo y minimización quedan en RNF-CUM-03 y RNF-SEG-05 | **Isidora** |
 
### 4.4 Lo que se pide a Isidora
 
Cuatro decisiones, ninguna urgente pero todas previas al T-12:
 
1. **Casos 2 y 3** — ¿se eliminan `RF-OPD-03` y `RF-OPD-04`, dejando el compromiso solo en RNF-DIS-03 y RNF-DIS-04? Es coherente con su Supuesto A, pero deja el dominio `RF-OPD` con dos requerimientos menos y conviene que ella lo valide.
2. **Caso 4** — ¿se reduce `RF-REF-08` a la conducta de notificación simultánea, dejando el umbral de confirmación en RNF-DIS-08? Es lo que su propia nota en RNF-DES-04 anticipaba.
3. **Caso 7** — ¿se reduce `RF-ACC-10` a la eliminación automática por plazo de retención?
4. **Transversal** — para el T-12, cuando un compromiso viva en ambos catálogos, ¿cuál es la fuente única de trazabilidad? La regla propuesta dice que el RNF, por conservar el umbral.
---
 
## 5. Efecto sobre el conteo y sobre el T-12
 
| | Requerimientos |
|---|---:|
| Tras las correcciones 1 y 2 | 128 |
| `RF-CON-12` — declaración de frontera parametrizable (RT-16.04) | +1 |
| **Subtotal** | **129** |
| Casos 2 y 3, si Isidora aprueba la eliminación | −2 |
| **Rango final de esta corrección** | **127 a 129** |
 
El resto de las duplicaciones se resuelve reformulando, no eliminando, de modo que no altera el conteo.
 
Para el T-12, la regla operativa queda así: **un código RT se acredita una sola vez**, contra el requerimiento —funcional o no funcional— que conserva su umbral. Los requerimientos que remiten no vuelven a acreditar el mismo código.
 
---
 
## 6. Pendientes que no cierran aquí
 
| # | Pendiente | Corrección |
|---:|---|---|
| 1 | Dominio `RF-TRA` (tractocamión) y control de capacidad de franjas de cita | 5 |
| 2 | Partir `RF-ACC-06` y `RF-NAV-09` — `RF-ACC-10` queda resuelto en 4.3 | 6 |
| 3 | Reescribir las metas 1, 2, 3 y 4 con la evidencia publicada, incluida la adversa | 7 |
| 4 | Ejemplo numérico de `RF-REF-13`, sujeto a la decisión de RN-10 | 8 |
| 5 | Añadir número de página a las citas antes de migrar al T-12, conforme al BA, Art. 43.2 | Fase 5 |
| 6 | Verificar el mapeo entre los 107 códigos RT no funcionales y los RNF | Fase 5 |
| 7 | Confirmar con Célula 3 la factibilidad de lectura desde el sistema de control de las grúas | — |
| 8 | Confirmar con Célula 3 la especificación de hardware que el catálogo presupone | — |
| 9 | Confirmar con Célula 4 el tratamiento de la evidencia inalterable de hechos facturables | — |
| 10 | Levantamiento del plazo de aviso de cada autoridad y existencia de interfaz electrónica | Meses 1 a 4 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*