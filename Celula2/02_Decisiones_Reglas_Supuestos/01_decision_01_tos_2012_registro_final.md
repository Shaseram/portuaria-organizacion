# Decisión N° 1 — Sistema de operación de terminal de 2012

## Registro de decisión consolidado

> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Estado:** decisión **adoptada y acordada** con el equipo. Este documento consolida la Propuesta de solución V3 con las observaciones de la revisión técnica (Daniel Miranda, Célula 3) y una revisión normativa adicional.
> **Origen del encargo:** CP, numeral 16.1, decisión N° 1.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).

### Trazabilidad de versiones

| Versión | Qué aportó | Estado |
|---|---|---|
| «Respuesta a las tres preguntas» | Análisis técnico de las tres opciones. Deliberadamente **no** decidía | Vigente como antecedente |
| Propuesta de solución V2 | Comparación y desventajas. Pasos 3-9 sin desarrollar | Superada |
| **Propuesta de solución V3** | Decisión adoptada, orden de sustitución, calendario, riesgos, consultas | Superada por este documento |
| Observaciones de revisión técnica (D. Miranda) | Cuatro correcciones + condición de viabilidad | **Incorporadas**, con una divergencia razonada |
| **Este documento** | Registro consolidado. Es la versión de referencia | **Vigente** |

> **Nota de estado.** Las secciones 1 a 8 recogen lo acordado. La sección 10 marca lo que **todavía requiere ratificación de la célula**, incluidos tres hallazgos nuevos que aún no han sido discutidos por el equipo. Nada de lo marcado como pendiente debe presentarse como decidido.

---

## 1. La decisión

**Terabyte adopta la Opción 3: envolver el sistema de operación de 2012 detrás de una capa de servicios anticorrupción y sustituir sus capacidades de forma progresiva, dominio por dominio.**

La estrategia se adopta con cuatro compromisos que forman parte de la decisión y no son accesorios a ella:

1. **Fuente de verdad explícita por dominio y por fase**, conforme exige BA, Art. 17.2, punto 2 («única fuente de verdad para los datos compartidos», «evitar toda doble digitación»).
2. **Conciliación automática entre ambos registros**, con umbrales y frecuencia declarados, conforme a CP, 17.6, punto 2.
3. **Procedimiento de retorno probado por dominio**, conforme a CP, 13.3, punto 5 y 17.6, punto 5.
4. **Fecha declarada de retiro del sistema legado**, anterior al vencimiento de su soporte.

**Declaración central:** al vencimiento del soporte del fabricante en 2028, **ningún componente del registro oficial de la operación permanece dentro del sistema de 2012**. Esta declaración es la que hace que la opción adoptada responda la pregunta de 2028 en lugar de diferirla, y está sujeta a la verificación de fecha de la sección 10.1.

**Condición de viabilidad:** la decisión está condicionada a una **puerta de decisión anterior al hito H2 (mes 4)** — sección 6. Si la verificación falla, la estrategia evoluciona hacia un reemplazo integral controlado.

---

## 2. Por qué se descarta mantener e integrar (Opción 1)

### 2.1 Fundamento principal — BA, Art. 1.3

> «El CLIENTE **no aceptará** propuestas construidas sobre **tecnología descontinuada, sin soporte vigente del fabricante**, o cuya arquitectura no admita evolución, escalamiento ni sustitución de componentes.» *(BA, Art. 1.3)*

Es una exclusión expresa, en las Bases Administrativas, que no requiere interpretación. El soporte del fabricante del sistema de 2012 vence en 2028, dentro del plazo contractual de 56 meses (CP, Cap. 5; BA, Art. 15.2). Mantenerlo como registro oficial hasta el mes 56 es exactamente la situación que el Art. 1.3 declara inaceptable.

### 2.2 Fundamento concurrente — obligaciones que el sistema no puede satisfacer

Quien tenga el registro oficial debe cumplir obligaciones que **no se pueden implementar sobre un producto de terceros sin código fuente**:

| Código | Exigencia |
|---|---|
| **BTT, RT-05.01** | Modelo de datos documentado **y diccionario de datos entregable**, con dominio de valores, obligatoriedad, propietario y sensibilidad por atributo |
| **BTT, RT-05.03** | Reconstruir quién, qué, cuándo, desde qué dispositivo y **con qué valores anteriores y posteriores**, para cualquier registro |
| **BTT, RT-16.07** | Auditoría **inalterable, no modificable por ningún perfil, incluido el administrador de la plataforma** |
| **BTT, RT-05.06** | Exportación total en formatos abiertos **sin intervención del ADJUDICATARIO** |
| **BTT, RT-11.04** | Remediar vulnerabilidades críticas en **7 días corridos**. Sin fabricante no hay parche: la obligación no desaparece, se vuelve inejecutable en su forma normal |

### 2.3 Fundamento corroborante — BTT, numeral 1.6

BTT 1.6 establece que todo **componente ofertado** cuyo soporte venza antes del mes 56 debe actualizarse o sustituirse **con cargo al ADJUDICATARIO, previsto y costeado en la oferta**.

> **Precisión adoptada tras la revisión técnica.** El numeral 1.6 se refiere a «componentes ofertados» y su aplicación automática a un sistema preexistente del CLIENTE **no es indiscutible**. Por eso este argumento se usa como **corroborante y no como fundamento principal**, y se formula en los términos seguros propuestos en la revisión:
>
> *«Si el sistema de 2012 permanece como componente estructural de la solución durante el contrato, el proponente deberá demostrar cómo garantizará su continuidad, mantenimiento y seguridad después de 2028, o presentar un plan de sustitución costeado.»*
>
> Formulado así, el argumento **sobrevive a cualquiera de las dos interpretaciones** de 1.6, y el peso del descarte recae sobre el Art. 1.3, que es explícito.

### 2.4 Fundamento de evaluación

CP, Cap. 19 exige que la decisión esté «tomada, fundada y costeada, **y no resuelta por omisión**». Mantener sin plan de fin de soporte fechado y costeado es la conducta que esa frase describe.

---

## 3. Por qué se descarta el reemplazo integral (Opción 2)

### 3.1 Corrección respecto de la V3

La V3 definía la Opción 2 prácticamente como un corte único y la descartaba por incompatibilidad con el despliegue modular. **Esa caracterización se corrige.** Un reemplazo integral también admite implantación progresiva, y descartarlo por «big bang» construye un adversario que no es necesariamente el real.

**La distinción correcta entre las dos opciones es la arquitectura de destino, no la forma de despliegue:**

| | **Opción 2** | **Opción 3** |
|---|---|---|
| **Destino** | Un TOS nuevo **completo**, desarrollado o adquirido como solución integral | Capa anticorrupción estable + **cada dominio cambia de fuente de verdad progresivamente** |
| **Arquitectura de transición** | La necesita igualmente si se despliega por fases: fachada, escritura dual, conciliación | Es constitutiva del patrón |
| **Acoplamiento resultante** | Un único producto que concentra todo el registro | Servicios por dominio, sustituibles de forma independiente |

> **Consecuencia:** un reemplazo integral desplegado por fases termina construyendo **la misma arquitectura de transición** que la Opción 3. La diferencia real no es *cómo se despliega*, sino *qué queda al final*: un producto integral o un conjunto de servicios por dominio.

### 3.2 Fundamento del descarte, reformulado

**La Opción 3 gana por su arquitectura de convivencia y su control del riesgo, no porque la Opción 2 sea obligatoriamente un evento único.**

1. **Concentración de esfuerzo difícil de compatibilizar con el resto del alcance.** El reemplazo integral concentra un nivel de levantamiento, migración, validación y cambio organizacional difícil de compatibilizar con los demás alcances obligatorios de la Etapa 1 —gate, telemetría del patio refrigerado, portal, captura de hechos facturables— y con las ventanas operacionales disponibles, incrementando significativamente el riesgo de incumplimiento.

2. **Concentra el riesgo en el punto que el CP identifica como el mayor del proyecto.** CP, 13.3, punto 5 califica la sustitución del sistema de 2012 como «el punto de mayor riesgo del proyecto», y exige convivencia real, conciliación y retorno probado. La Opción 3 fracciona ese riesgo; la Opción 2 lo concentra.

3. **Verificación física del inventario concentrada en una sola ventana.** CP, Cap. 15, RT-05.15 exige migrar la totalidad del inventario «con posición verificada físicamente», y CP, 17.6, punto 3 obliga a declarar cómo se hace en un patio que no se detiene, con ~11.200 TEU cuyas posiciones cambian cada hora (CP, 14.1 y Cap. 3). La Opción 3 permite repartir ese barrido por bloques a lo largo del tiempo.

4. **Capacidad de absorción del CLIENTE.** El área de TI son **cinco personas** (CP, Cap. 10, restricción 11) en un operador de importancia vital 24×7×365. Una sustitución paulatina es lo que un equipo de ese tamaño puede absorber.

### 3.3 Sobre las referencias sectoriales

Las cifras de duración e impacto se **verificaron** contra la fuente y son citas fieles:

- The Intech Group (2026): «TOS implementations at mid-to-large container terminals take between 12 and 24 months».
- Indie Hackers (2026): «4–8 months of specialist data engineering work»; «10–20% of year-one cost»; «20–40% productivity drops in the first three months post-go-live, regardless of platform quality».

**No hay problema de exactitud en la cita. Sí hay un problema de autoridad de la fuente.** Indie Hackers es una publicación de comunidad de emprendedores y Market Intelo es una consultora de estudios de mercado; ninguna es literatura arbitrada ni documentación de fabricante. Por eso:

- Estas cifras se emplean como **referencia indicativa de órdenes de magnitud** y **no sostienen por sí solas el descarte**, que descansa en los cuatro fundamentos normativos y operacionales de 3.2.
- Se mantiene la nota de calidad de fuentes del documento.
- **Pendiente:** contrastarlas con literatura académica o casos documentados antes de la versión final del informe (CP, Cap. 16.2 exige investigación sectorial real; las referencias preferentes son primarias, académicas, normativas o de fabricante).

> **Formulación adoptada, evitando el absoluto:** no se afirma que el reemplazo integral «no cabe en el calendario». Se afirma que **concentra un nivel de esfuerzo difícil de compatibilizar con los demás alcances obligatorios y con las ventanas disponibles, incrementando significativamente el riesgo de incumplimiento.**

---

## 4. Fundamento del patrón adoptado

El patrón es el **strangler fig** descrito por Fowler (2004a): construir el sistema nuevo alrededor del antiguo y sustituirlo de forma incremental hasta vaciarlo. Microsoft (2025a) lo recomienda cuando el reemplazo de sistemas grandes o críticos introduce riesgo y el original debe seguir existiendo un período prolongado — condiciones que describen este caso.

El envoltorio se materializa mediante una **capa anticorrupción** (Evans, 2003; Microsoft, 2025b), cuya función es traducir entre los modelos de ambos sistemas para que el diseño nuevo no quede condicionado por la semántica del antiguo.

**Las bases no solo lo admiten: lo incentivan.**

- **BTT, RT-05.20 (Obligatorio):** «Las integraciones con sistemas heredados o de terceros se aislarán mediante una capa anticorrupción, de modo que un cambio en el sistema externo no propague su modelo al núcleo de la solución.»
- **BTT, RT-02.14 (Deseable):** «Se valorará la aplicación documentada de patrones de arquitectura evolutiva… capa anticorrupción frente a sistemas heredados, **estrangulamiento progresivo** y abstracción de proveedores.»

### 4.1 La advertencia que condiciona el patrón

Microsoft (2025a) señala que el strangler fig **no es apropiado** cuando las peticiones al sistema heredado no pueden interceptarse o cuando no se dispone de su código fuente. El sistema de 2012 es un producto comercial sin código fuente disponible para el CLIENTE (CP, Cap. 5).

La advertencia no invalida la decisión, porque el envoltorio se aplica sobre las **interfaces externas** del sistema y no sobre sus llamadas internas. Pero **convierte la verificación de interceptabilidad y de escritura en condición de viabilidad del plan**, no en un detalle de implementación. De ahí la puerta de decisión de la sección 6.

---

## 5. Orden de sustitución

### 5.1 Corrección respecto de la V3

La V3 justificaba sustituir primero el núcleo de registro afirmando que «es el dominio más difícil de revertir y por eso conviene que salga primero». **Ese argumento está invertido y se retira.** La dificultad de revertir es razón para preparar más antes de mover, no para mover primero.

**La conclusión se mantiene** —el núcleo de registro va primero— pero sobre los fundamentos correctos, que ya estaban en el documento en otras filas:

| Fundamento | Sustento |
|---|---|
| **Dependencia aguas abajo** | Todo lee de él: la facturación calcula sobre sus hechos, la planificación se alimenta de sus posiciones, el portal publica su estado. **Nada aguas abajo es confiable mientras el registro conserve 3,1 % de error** (CP, 7.2) |
| **Criterio de captura de activos** | Fowler (2004b) recomienda empezar por activos simples o por aquellos **cuyas necesidades el sistema antiguo maneja particularmente mal**. Un registro de posición con 3,1 % de error pertenece inequívocamente a la segunda categoría |
| **Presión del hito externo** | Si el núcleo sale antes del fin de soporte, el problema de cumplimiento de 2028 queda sustancialmente resuelto (CP, 13.2) |
| **Objeción registrada del jefe de operaciones** | «Arreglar el gate sin resolver el patio sólo traslada la cola hacia adentro» (CP, 13.1). Solo se responde sustituyendo gate y patio **juntos** |

### 5.2 El núcleo es un solo contexto acotado — y se despliega por zonas

El gate crea el contenedor en el inventario y la salida lo elimina; la posición y los movimientos lo modifican. Sustituir el gate dejando la posición dentro del sistema de 2012 generaría **dos fuentes de verdad sobre el mismo objeto**, situación que BA, Art. 17.2, punto 2 prohíbe expresamente. **Constituyen un único contexto acotado y se sustituyen juntos.**

> **Síntesis con la observación de revisión.** La revisión técnica propuso que la primera pieza fuera «el registro de posiciones y movimientos en una zona acotada del patio, no todo el núcleo simultáneamente». Esa propuesta **no contradice** el párrafo anterior y se adopta: el fraccionamiento es **por zona, no por función**. El contexto acotado se mantiene íntegro y lo que se escalona es el despliegue territorial. Eso es exactamente lo que autoriza CP, 13.3, punto 4 («por proceso **o por zona**»), y refuerza el cumplimiento del despliegue modular en vez de tensionarlo.

La autoridad queda definida por `dominio × zona × fase`: antes del cutover de una zona manda el TOS 2012; durante la validación paralela el sistema nuevo es solo lector/sombra; después del cutover aprobado manda el sistema nuevo y el legado recibe réplica para retorno. El cruce de un contenedor entre zonas es una transferencia transaccional: el sistema que tiene autoridad emite un evento secuenciado e idempotente, el receptor confirma persistencia y solo entonces cambia la autoridad. Un fallo parcial mantiene la autoridad anterior, deja el evento en cola y bloquea una segunda transferencia hasta conciliarlo. Nunca ambos sistemas pueden aceptar escrituras autoritativas sobre el mismo contenedor y dominio.

### 5.3 Secuencia de ejecución adoptada

La revisión técnica aportó una secuencia que **no es un orden alternativo de dominios, sino el método para ejecutar «núcleo primero» sin comprometer la reversibilidad**. Se adopta:

1. **Descubrir y documentar** interfaces y datos del sistema de 2012.
2. **Comprobar** lectura, escritura, sincronización y reconciliación.
3. **Implementar** la capa anticorrupción.
4. **Crear observabilidad y auditoría de convivencia.**
5. **Probar una capacidad delimitada** por zona del patio, proceso o turno.
6. **Migrar progresivamente** el resto del dominio y los dominios siguientes.

Los pasos 1 y 2 son los que alimentan la puerta de decisión del mes 4 (sección 6).

### 5.4 Dominios y su asignación a etapas

| # | Dominio | Naturaleza | Etapa | Fundamento de la posición |
|---|---|---|---|---|
| **1** | **Núcleo de registro del contenedor** — gate, posición, movimientos, salida | Sustitución | **1** | Máxima carga de cumplimiento (RT-09.01, RT-03.10, RT-03.13, RT-05.03, RT-16.06/07); todo depende de él; presión de 2028; responde la objeción del jefe de operaciones |
| **2** | **Telemetría del patio refrigerado** | **Capacidad nueva**, no sustitución | **1**, en paralelo | No toca el registro del sistema de 2012 (los 26 tableros no transmiten). Reversibilidad máxima: volver a la ronda a pie. Segundo en la preferencia del comité |
| **3** | **Evidencia de hechos facturables** | Sustitución | **2** | Depende del dominio 1: los hechos se derivan de movimientos, días de almacenaje y horas de conexión |
| **4** | **Planificación asistida y mensajería con navieras** | Sustitución + capacidad nueva | **2** | La planificación requiere que la posición ya sea confiable. Hito externo más apremiante (alianza naviera 2029) — ver sección 10.2 |
| **5** | **Portal de clientes** | Reemplazo ya definido por el CP, Cap. 5 | **2** | Publica información de los dominios 1 y 3; depende de que ambos estén estabilizados |

### 5.5 Respuesta a las dos objeciones registradas en CP, 13.1

- **Jefe de operaciones** («arreglar el gate sin resolver el patio traslada la cola»): **resuelta por completo** — gate y patio se sustituyen como un solo contexto acotado.
- **Gerenta comercial** (las tres condiciones de la alianza naviera quedaron al final y no llegan a 2029): **acogida como programa indivisible** — la captura de emisiones comienza en el mes 1 y, antes de la fecha efectiva de 2029, deben estar demostradas conjuntamente la mensajería estándar exclusiva y cero redigitación para la alianza, la ventana ≥72 h con productividad ≥30 movimientos/h por grúa y el reporte efectivamente verificado. Se mantiene la precedencia del núcleo para las escrituras autoritativas, porque una mensajería que informe posiciones erróneas agrava el problema; esa precedencia no posterga los trabajos de onboarding, captura ni prevalidación.

---

## 6. Condición de viabilidad: la puerta de decisión del mes 4

Los elementos de esta condición existían dispersos en la V3 (advertencia 6.1, riesgo R1, supuesto S2 y párrafo de cierre). Se consolidan aquí como **una puerta de decisión formal**, conforme propuso la revisión técnica.

> **Puerta de decisión — anterior al hito H2 (mes 4), BA, Formulario E-25.**
>
> Se ejecuta una prueba de factibilidad sobre ambiente de no producción que verifique: **interceptación** de peticiones, **lectura**, **escritura**, **sincronización** y **conciliación** contra el sistema de 2012, con perfilado del modelo de datos real.
>
> **Si el levantamiento demuestra que el sistema de 2012 no permite lectura, escritura, sincronización o conciliación suficientemente confiables, la estrategia de envolvimiento deberá revisarse y podrá evolucionar hacia un reemplazo integral controlado.**

**Por qué el mes 4 y no otro:** el hito H2 exige la aprobación del documento de arquitectura, del plan de seguridad **y del modelo de datos** (BA, Formulario E-25), y su cumplimiento requiere acta de aceptación de la Contraparte Técnica (BA, Art. 18.1). Comprometer un modelo de datos que depende de una capacidad no verificada sería comprometer lo que no se sabe si es factible.

**Por qué es decisiva:** de esa capacidad depende **toda la reversibilidad comprometida**. La reversión no consiste en restaurar un respaldo sino en devolver la autoridad del registro al sistema anterior, y eso exige que el sistema anterior esté **al día**, no solo encendido.

---

## 7. Mecanismos de convivencia

### 7.1 Conciliación durante la marcha blanca

BA, Art. 17.3 establece que la marcha blanca solo cierra si la conciliación no presenta **diferencias no explicadas**. La distinción importa: existirán diferencias por desfase temporal; lo que se exige es que cada una tenga explicación.

La convivencia es **bidireccional**: toda operación originada en la solución nueva se replica al legado y toda operación que aún se origine en una pantalla, proceso o integración heredada se captura hacia el registro nuevo. Ambos sentidos usan identificador de operación, número de secuencia, clave de idempotencia y deduplicación; una escritura parcial se conserva en cola durable, genera alerta y no cambia por sí sola la autoridad. La conciliación por turno certifica la consistencia, pero no reemplaza la propagación operacional ni su alerta inmediata.

| Universo conciliado | Frecuencia | Umbral de alerta | Umbral de detención |
|---|---|---|---|
| Posición de contenedor en patio | Por turno | 0,2 % no explicadas | 0,5 % no explicadas |
| Movimientos registrados | Por turno | 0,2 % | 0,5 % |
| Entradas y salidas por gate | Por turno | Cualquier diferencia | **Cero no explicadas al cierre del día** — resuelto en §15.3 |
| Hechos facturables y su evidencia | Diaria | Cualquier diferencia | Cualquier diferencia no explicada al cierre del día |

**Fundamento de los umbrales:** ver §15.2, que corrige el fundamento original, introduce la regla direccional de clasificación de divergencias y diferencia la ventana de investigación. Para hechos facturables y gate el umbral es cero, por su implicancia económica y contractual (§15.3). La frecuencia por turno corresponde al ciclo natural de cierre de una operación 24×7 en tres turnos y convierte en control lo que el CP, Anexo B.1 identifica como «punto de pérdida de información».

**Acción al superarse el umbral de detención:** se congela el avance del dominio, se investiga en el turno siguiente y, si no se explica dentro de la ventana aplicable —48 h para posición y movimientos, 24 h para gate y hechos facturables (§15.2)—, se revierte el dominio.

### 7.2 Reversión con nave amarrada

**La reversión no es restaurar un respaldo: es devolver la autoridad del registro al sistema anterior.**

- **Precondición.** La reversión de un dominio solo está disponible mientras la **escritura dual** hacia el sistema de 2012 permanezca activa. Por eso la escritura dual no se apaga hasta el cierre formal de la marcha blanca.
- **Mecanismo.** Se modifica el enrutamiento de la fachada para devolver el dominio al sistema de 2012. Los consumidores no se modifican, porque todos operan contra el mismo contrato de interfaz.
- **Modo degradado.** Durante la marcha blanca el procedimiento actual sigue vigente, de modo que revertir implica volver al plan impreso y la radio — coherente con la degradación elegante que exige BTT, RT-02.09.
- **Cierre de la ventana.** Apagada la escritura dual, no existe reversión sino corrección hacia adelante. **El apagado es un hito bajo doble control y aprobación explícita del CLIENTE, no un evento automático.**

Los tiempos objetivo de reversión y la autoridad facultada para ejecutarla en cada uno de los tres turnos se resuelven en **§15.4**.

### 7.3 Verificación física del inventario

CP, 17.6, punto 3 obliga a declarar cómo se verifica físicamente la posición en un patio que no se detiene. Método adoptado: **barrido por bloques con congelamiento lógico**.

1. El patio se divide en bloques operativos.
2. Para cada bloque se suspenden depósitos y retiros durante una ventana acotada, redirigiendo la operación a bloques vecinos.
3. Se barre el bloque leyendo los códigos con las terminales de equipo y reconocimiento óptico, **no mediante conteo manual**.
4. Se libera el bloque y se avanza al siguiente.
5. Los movimientos ocurridos en otros bloques durante el barrido se reconcilian desde el registro de movimientos.
6. Se repite el barrido sobre una muestra para **estimar el error del propio procedimiento**.

El barrido se ejecuta entre mayo y noviembre y evita los dos peaks de gate (05:00–09:00 y 14:00–18:00, CP, Anexo B.1).

CP, 13.3, punto 2 exige que si una actividad requiere reducir capacidad, **su costo y su compensación operacional estén en la propuesta**. El congelamiento lógico de un bloque reduce capacidad y debe cuantificarse.

---

## 8. Calendario y colisión detectada

### 8.1 Supuesto de anclaje

Ninguna base declara la fecha de inicio del contrato (BA, Art. 17°; CP, 13.2). Se declara como supuesto que **el mes 1 corresponde a febrero de 2027**, dos meses después de la entrega de resultados prevista para el 01-12-2026 (BA, Formulario T-20), plazo razonable para la firma y la constitución de garantías.

| Hito | Mes | Fecha estimada | ¿Dentro del congelamiento? |
|---|---:|---|---|
| Inicio de desarrollo Etapa 1 | 1 | feb 2027 | — |
| Hito H2 — arquitectura, seguridad y modelo de datos | 4 | may 2027 | — |
| Versión candidata Etapa 1 terminada, instalada y con retorno probado | antes del mes 12 | **a más tardar 14-dic-2027** | No |
| Validación paralela no invasiva, condicionada a consulta | 13–15 | 15-dic-2027 a 30-abr-2028 | **Solo lectura, sin autoridad — ver 8.2** |
| **Producción Etapa 1** | 16 | **may 2028** | No |
| Inicio de desarrollo Etapa 2 | 13 | feb 2028 | — |
| Fin de desarrollo Etapa 2 | 18 | jul 2028 | — |
| Marcha blanca Etapa 2 | 19–20 | ago–sep 2028 | No |
| **Producción Etapa 2** | 21 | **oct 2028** | No |

### 8.2 Resolución de la colisión con el congelamiento

El calendario se corrige con una secuencia única. **Hasta el 14-dic-2027** deben quedar terminadas la versión candidata de Etapa 1, la infraestructura, instrumentación e integración necesarias, la migración inicial, las pruebas, el retorno probado y la capacitación requerida. Entre el **15-dic-2027 y el 30-abr-2028** solo podrá ejecutarse validación paralela no invasiva con esa misma versión, en lectura/sombra y sin autoridad sobre el registro; el TOS 2012 seguirá siendo la fuente oficial. No se instalarán versiones, equipos o configuraciones, no se migrará, no se corregirá producción y no habrá cutover.

Esta validación durante la temporada queda **condicionada a respuesta formal del CLIENTE** en C1. Si el CLIENTE no confirma que la actividad de solo lectura no constituye intervención, se replanifica fuera del congelamiento. Desde el **01-may-2028** se ejecutan regresión final, autorización y transferencia gradual y reversible de autoridad, respetando además la prohibición de intervenir durante la atención de una nave o las cuatro horas previas.

El adelanto desde enero al 14 de diciembre es una condición de viabilidad, no un cambio nominal. Si alcance, cobertura o recursos no lo sostienen, el cronograma debe reprogramarse formalmente; no puede afirmarse a la vez que el desarrollo termina en enero y que todo quedó desplegado en diciembre.

---

## 9. Consecuencias sobre el alcance

### 9.1 Reparto entre etapas

| Etapa | Contenido derivado de esta decisión |
|---|---|
| **Etapa 1** | Capa anticorrupción y fachada de servicios; sustitución del núcleo de registro del contenedor (gate, posición, movimientos, salida), desplegada por zonas; telemetría del patio refrigerado como capacidad nueva; mecanismo de conciliación y de reversión por dominio; **captura del conocimiento tácito del planificador** y **captura de datos de emisiones desde el mes 1** |
| **Etapa 2** | Evidencia de hechos facturables; planificación asistida de estiba y patio; mensajería con navieras; portal de clientes; apagado de la escritura dual y cierre del sistema de 2012 |

Este reparto es **preliminar**: CP, Cap. 19 exige que el alcance sea consecuencia del catálogo de requerimientos, de modo que debe revalidarse una vez completado el catálogo.

### 9.2 Exclusiones que genera la decisión

- La **documentación retrospectiva completa** del sistema de 2012 queda fuera de alcance. Solo se documenta la superficie de interfaz efectivamente envuelta y los dominios sustituidos.
- La migración de histórico **anterior a los plazos que fija CP, Cap. 15, RT-05.15** queda fuera de alcance.
- El **mantenimiento correctivo del sistema de 2012** durante la transición permanece con el fabricante mientras su soporte siga vigente.

### 9.3 Requerimientos que introduce la decisión

Deben incorporarse al catálogo del Subdocumento 3:

- Capa anticorrupción con contrato de interfaz versionado (BTT, RT-05.20).
- Escritura dual hacia el sistema de 2012 durante la marcha blanca, con mecanismo de apagado controlado y aprobación explícita del CLIENTE.
- Conciliación automática entre ambos registros, con los umbrales de 7.1.
- Reversión por dominio mediante redirección de enrutamiento, con tiempo objetivo declarado.
- Verificación física del inventario por barrido de bloques con congelamiento lógico.
- Observabilidad y auditoría de convivencia entre ambos registros.
- Captura de operaciones originadas en el TOS 2012 hacia el registro nuevo, con orden, idempotencia, deduplicación y tratamiento de fallos parciales (`RF-CON-13`).
- Autoridad única por `dominio × zona × fase` y transferencia transaccional al cruzar zonas migradas y no migradas (`RF-CON-14`).
- **Registro de decisiones de arquitectura** fechado, con alternativas descartadas y criterio de decisión (BTT, RT-02.04). **Corresponde al Subdocumento 4 y es responsabilidad de la Célula 3**; este documento es su insumo.

---

## 10. Hallazgos nuevos que requieren decisión de la célula

> Los tres puntos siguientes surgieron de la revisión normativa posterior a la V3 y **no han sido discutidos por el equipo**. No deben presentarse como decididos.
>
> **Cada uno tiene una resolución propuesta y argumentada en §15** — 10.1 en §15.6, 10.2 en §15.5, 10.3 en §15.3. Lo que falta es la ratificación de la célula, no el análisis.

### 10.1 La declaración central de 2028 no está verificada contra su propio calendario

La sección 1 declara que al vencimiento del soporte en 2028 ningún componente del registro oficial permanece en el sistema de 2012. El calendario de 8.1 sitúa la producción del núcleo de registro en **mayo de 2028**.

**Ni el CP ni las BA declaran el mes de 2028 en que vence el soporte.** CP, Cap. 5 dice «soporte del fabricante vigente hasta 2028» y CP, 13.2 dice «término del soporte del fabricante» sin precisar mes. Si el soporte vence antes de mayo de 2028, **la declaración central de la decisión no se cumple con el calendario adoptado**.

**Acción propuesta:** incorporar la precisión a la consulta C2 o abrir una consulta específica, y mientras tanto declarar un sub-supuesto explícito (S5) de que el soporte cubre el año 2028 completo, con su impacto si resulta equivocado.

### 10.2 La dependencia de Nibaldo queda descubierta entre su jubilación y la producción de la Etapa 2

La planificación asistida entra en producción en el **mes 21 (octubre de 2028)**. Nibaldo se jubila «el 2028» (CP, Cap. 8), sin mes declarado. Si se retira antes de octubre, **existe un intervalo en que su conocimiento ya no está en la empresa y el sistema que debía contenerlo todavía no existe**.

Esto compromete directamente el criterio de aceptación N° 22 (CP, Cap. 18): «Don Nibaldo se jubila en 2028 y el terminal sigue planificando igual o mejor».

**Consecuencia propuesta:** la **captura del conocimiento tácito es un frente de trabajo de la Etapa 1**, independiente del módulo de planificación y anterior a él. Su producto no es software sino un **artefacto documentado** —el registro de reglas, restricciones y casos del planificador: falla intermitente de la grúa tres, inundación del bloque C, generador de popa limitado, exportador que llega tarde (CP, 4.2 y Cap. 8)— que después alimenta el motor.

Esto además **coincide con un entregable que ya es de Célula 2**: el *registro de reglas de negocio* que exige CP, Cap. 17.1. No es trabajo adicional: es reconocer que ese registro tiene una fecha de caducidad puesta por una persona.

**Acción propuesta:** añadir el frente a la Etapa 1 en 9.1 y abrir consulta sobre el mes de retiro del planificador.

### 10.3 El umbral de conciliación del gate probablemente debe ser cero

El umbral propuesto para entradas y salidas por gate es 0,3 % de detención. Con 1.450 camiones/día promedio y hasta 2.600 en peak (CP, 14.1), 0,3 % equivale a **entre 4 y 8 camiones diarios sin explicación**.

El problema es qué se calcula con esos registros: **la estadía del camión se mide desde la barrera de entrada hasta la de salida** (CP, Anexo C) y es uno de los indicadores comprometidos con el concedente, que CP, Cap. 10, restricción 14 exige producir «de forma trazable y auditable, **no reconstruirlos**», y sobre el cual el terminal ya acumula **tres semestres consecutivos sobre el umbral** (CP, 7.1).

Un margen de discrepancia no explicada en el gate contamina directamente un indicador con consecuencias contractuales.

**Acción propuesta:** tratar el gate como los hechos facturables — **cero diferencias no explicadas al cierre del día** — o justificar expresamente por qué el indicador tolera el margen.

---

## 11. Supuestos declarados

| ID | Supuesto | Fundamento | Impacto si resulta equivocado | Instancia de validación |
|---|---|---|---|---|
| **S1** | El mes 1 del contrato corresponde a **febrero de 2027** | Entrega de resultados 01-12-2026 (BA, T-20) más dos meses para firma y garantías | Se desplaza todo el calendario; si el desplazamiento supera cuatro meses, alguna puesta en producción entra en congelamiento | Consulta C1 o firma del contrato |
| **S2** | Es factible **interceptar y escribir** hacia el sistema de 2012 desde una capa externa | Necesario para la reversibilidad; advertido como condición del patrón por Microsoft (2025a) | Se anula la reversibilidad y debe replantearse la decisión completa | **Puerta de decisión del mes 4** (sección 6) |
| **S3** | Durante el congelamiento solo serían admisibles validaciones paralelas **no invasivas, de solo lectura y sin autoridad operacional**, si el CLIENTE confirma formalmente que no constituyen intervención | Permite observar volumen real sin instalar, desplegar, migrar, corregir producción ni hacer cutover | Si el CLIENTE no lo confirma, la validación se replanifica fuera del congelamiento | Consulta C1 antes de aprobar el cronograma base |
| **S4** | El patio admite **segmentación en bloques operativos** para el barrido de verificación | Práctica habitual y coherente con la referencia al bloque C en el CP | Debe replantearse el método de verificación física del inventario | Consulta C4 |
| **S5** | El soporte del fabricante **puede vencer tan pronto como el 01-01-2028**, y el plan se evalúa contra ese escenario | Supuesto conservador. BA, Art. 5.3 y 5.4 obligan a adoptar la interpretación más exigente ante ambigüedad. Ver §15.6 | Si vence antes de mayo de 2028 existe una ventana de exposición **estructural del calendario contractual**, común a las tres opciones, declarada y mitigada en §15.6 (d) | Consulta C2 |

## 12. Consultas formales

### 12.1 Criterio de admisibilidad aplicado

No toda indeterminación es una consulta. **BA, Art. 43.4** establece que el CLIENTE responderá únicamente las consultas «pertinentes al proceso, concretas y precisas, y que no involucren información confidencial ni **exijan al CLIENTE diseñar la solución en lugar del PROPONENTE**».

El propio caso lo refuerza dos veces:

> «Este documento no es una especificación de requerimientos. Es la descripción de una operación real […] **completar lo que falta con supuestos declarados y con reglas de negocio propias de la industria** […] es exactamente el trabajo que se está licitando y lo que será evaluado.» *(CP, Nota Mandatoria de la ficha resumen)*

> «El CLIENTE entrega los volúmenes que efectivamente conoce, porque son los que gobierna su operación. Los volúmenes propios del dimensionamiento de un sistema […] no los conoce, y no tiene por qué conocerlos: **derivarlos es trabajo de ingeniería del PROPONENTE**.» *(CP, Cap. 14)*

**Criterio adoptado:** se consulta **un hecho que el CLIENTE posee y no ha declarado**, o **una contradicción entre dos textos normativos**. No se consulta nada derivable por ingeniería, ni nada que el texto ya resuelva.

El criterio no es solo de cortesía procesal. **BA, Art. 43.5** advierte: «El CLIENTE registra qué empresas identifican vacíos, contradicciones y riesgos en las Bases, y qué empresas **se limitan a solicitar aclaraciones sobre materias explícitamente resueltas en el texto**». Una consulta mal escogida no es neutra: resta.

### 12.2 Consulta retirada

**Se retira la consulta sobre segmentación operativa del patio en bloques y volumen medio de movimientos por bloque y turno** (antigua C4).

Pedía al CLIENTE un antecedente de dimensionamiento que el CP declara expresamente que no le corresponde entregar. La segmentación del patio y el volumen por bloque y turno son derivables de datos que el CP **sí** entrega —18 hectáreas de patio, capacidad de 12.400 TEU, ≈11.200 TEU en peak, ≈1.290.000 movimientos de patio al año, 18 grúas de patio (CP, 2.2 y 14.1)— y su derivación es precisamente el trabajo que el Cap. 14 asigna al proponente.

**Vía de resolución sustituta:** el dato pasa a ser **supuesto declarado de ingeniería** conforme al Cap. 14 —con valor estimado, método de estimación y supuestos empleados— y no consulta. Esto modifica la vía de resolución del pendiente N° 4, que deja de estar «sujeto a C4»; su contenido sustantivo permanece abierto por decisión de la célula.

### 12.3 Consultas que se presentan

Se presentan dentro del período comprendido entre el **20-08-2026 y el 01-09-2026** (BA, Art. 43.1 y Formulario T-20, actividad 4), en la planilla de siete columnas del BA, Art. 43.2 y con la nomenclatura del Art. 43.3: `CONSULTAS_TERABYTE_AAAAMMDD.XLSX`.

| ID | Tipo | Consulta | Por qué es admisible |
|---|---|---|---|
| **C1** | Técnica | Si entre el 15 de diciembre y el 30 de abril el CLIENTE admite una **validación paralela no invasiva**, con versión previamente instalada, en solo lectura/sombra y sin autoridad operacional, manteniendo al TOS 2012 como registro oficial; sin instalar equipos, versiones o configuraciones, migrar, corregir producción ni hacer cutover. En caso negativo, confirmar que esa validación deberá replanificarse fuera del congelamiento | **Contradicción entre calendario contractual y restricción no negociable.** Se propone una interpretación conservadora y verificable sin llamar “marcha blanca” a una intervención |
| **C2** | Técnica | **Fecha exacta de término del soporte del fabricante** del sistema de operación de 2012, que el CP, Cap. 5 y 13.2 sitúan en 2028 sin precisar mes; y si el contrato de soporte vigente contempla la **entrega de documentación técnica** antes de su vencimiento | **Hecho que el CLIENTE posee y no ha declarado.** No se pregunta si existe documentación del modelo de datos: el CP ya lo resolvió expresamente en Cap. 5 y Cap. 8 («Nadie la tiene»), y volver a preguntarlo caería en el supuesto que sanciona el Art. 43.5 |
| **C3** | Administrativa | Si el CLIENTE **autoriza** la escritura de terceros hacia el sistema de operación de 2012, y si el contrato con el fabricante la admite hasta el vencimiento del soporte | **Autorización contractual, no factibilidad técnica.** La factibilidad técnica es materia propia y se verifica en la puerta de decisión del mes 4 (§6) |
| **C4** | Técnica | **Fecha prevista de retiro del planificador de estiba y patio**, que el CP, Cap. 8 y 13.2 sitúan en 2028 sin precisar mes, antecedente necesario para situar el frente de captura de conocimiento tácito respecto del criterio de aceptación N° 22 (CP, Cap. 18) | **Hecho que el CLIENTE posee y no ha declarado**, y del que depende directamente un criterio de aceptación que el propio CP formula |

> **Sobre la columna G de la planilla.** El Art. 43.2 exige una columna «Propuesta de interpretación del proponente, si la tuviere». A la luz del Art. 43.5, conviene completarla en las cuatro: es lo que distingue una consulta que identifica un vacío de una pregunta que lo padece. Las interpretaciones propuestas son las de los supuestos S1, S3 y S5 de §11 y la de §15.5.

---

## 13. Registro de cambios respecto de la V3

| # | Observación | Origen | Resolución |
|---|---|---|---|
| 1 | La Opción 2 no es necesariamente un *big bang*; caracterizarla así es injusto | Revisión técnica | **Aceptada.** Sección 3.1 redefine el eje de comparación: arquitectura de destino, no forma de despliegue. Se añade que un reemplazo por fases construye la misma arquitectura de transición |
| 2 | No afirmar categóricamente que la Opción 2 «no cabe»; sustentar o eliminar las cifras | Revisión técnica | **Aceptada en la formulación.** Sección 3.2 adopta el fraseo propuesto. **Divergencia parcial:** las cifras se verificaron contra la fuente y son citas fieles, por lo que no se eliminan; se **degradan a referencia indicativa** y se mantiene la observación sobre autoridad de la fuente (3.3) |
| 3 | Cuidado con aplicar BTT 1.6 al sistema existente | Revisión técnica | **Aceptada, y reforzada.** BTT 1.6 pasa a corroborante con el fraseo seguro propuesto. **Se promueve BA, Art. 1.3** —«no aceptará propuestas construidas sobre tecnología descontinuada, sin soporte vigente del fabricante»— como fundamento principal, que es explícito y no requiere interpretación |
| 4 | No sustituir primero el núcleo «porque es difícil de revertir»: el argumento está invertido | Revisión técnica | **Aceptada.** Sección 5.1 retira el argumento. **La conclusión se mantiene** sobre cuatro fundamentos correctos. La secuencia propuesta en la revisión se adopta como **método de ejecución** (5.3), y su piloto «por zona acotada» se integra en 5.2 sin romper el contexto acotado |
| 5 | Añadir punto de decisión antes de H2 | Revisión técnica | **Aceptada como consolidación.** Los elementos existían dispersos en la V3 (6.1, R1, S2, Paso 9); la sección 6 los reúne en una puerta de decisión formal con contingencia declarada |
| 6 | La declaración de 2028 no está verificada contra el calendario propio | Revisión normativa | **Abierta** — sección 10.1. Requiere ratificación de la célula |
| 7 | La dependencia de Nibaldo queda descubierta entre su retiro y el mes 21 | Revisión normativa | **Abierta** — sección 10.2. Requiere ratificación de la célula |
| 8 | El umbral de conciliación del gate contamina un indicador contractual | Revisión normativa | **Abierta** — sección 10.3. Requiere ratificación de la célula |

---

## 14. Pendientes: estado

| N° | Pendiente | Estado | Dónde se resuelve |
|---|---|---|---|
| 1 | Destino final del sistema de 2012 y mes de apagado | **Resuelto** | §15.1 |
| 2 | Ratificación de los umbrales de conciliación y de la ventana | **Resuelto** | §15.2 |
| 3 | Revisión del umbral de gate | **Resuelto** | §15.3 |
| 4 | Segmentación del patio en bloques, duración del barrido y capacidad resignada | **Abierto por decisión de la célula.** Cambia su vía: de consulta a supuesto de ingeniería | §12.2 y §15.9 |
| 5 | Tiempo objetivo de reversión y cargo autorizador en cada turno | **Resuelto** | §15.4 |
| 6 | Frente de captura de conocimiento tácito en la Etapa 1 | **Resuelto** | §15.5 |
| 7 | Supuesto sobre el vencimiento del soporte | **Resuelto** | §15.6 |
| 8 | Redacción y presentación de las consultas | **Resuelto** — con alerta de plazo | §15.7 |
| 9 | Contraste de las referencias sectoriales | **Resuelto en lo estructural**; mejora residual al Informe 2 | §15.8 |
| 10 | Valorización económica de la decisión | **Abierto** — corresponde al Informe 3 | §15.9 |
| 11 | Traspaso a Célula 3 para el registro de decisiones de arquitectura | **Abierto** — tarea de coordinación | §15.9 |

---

## 15. Resolución de los pendientes

> Cada resolución indica **qué se decide**, **sobre qué base** y **qué riesgo residual queda**. Son propuestas fundadas de Célula 2: quedan firmes cuando la célula las ratifique. Los pendientes 4, 10 y 11 se mantienen abiertos deliberadamente (§15.9).

### 15.1 Pendiente 1 — Destino final del sistema de 2012

**Resolución: extracción del histórico a un repositorio de consulta independiente y apagado del sistema de 2012. No se conserva como archivo histórico de solo lectura sobre sí mismo.**

**(a) Hay un hueco de siete años entre lo que hay que retener y lo que hay que migrar.** CP, Cap. 15, **RT-05.10** exige retener registros de operación y movimientos de contenedor **10 años**, «por el régimen aduanero y por la vigencia de la concesión». CP, Cap. 15, **RT-05.15** obliga a migrar solo **3 años** de movimientos. Los siete años restantes deben seguir siendo recuperables **y están fuera del alcance de migración**. Ése es el problema que el pendiente planteaba sin nombrarlo: no es dónde archivar por prolijidad, es dónde vive una obligación de retención que la migración no cubre.

**(b) Las BTT ya prescriben el destino.** BTT, **RT-05.15**: «Los datos históricos que no se migren quedarán accesibles en **un repositorio de consulta** durante el período de retención que fije el caso.» La norma no dice «en el sistema de origen». Dice repositorio de consulta.

**(c) Conservar el sistema encendido como archivo incumpliría RT-05.06.** «La solución permitirá exportar la totalidad de la información del CLIENTE en formatos abiertos y documentados, en cualquier momento del Contrato, sin costo adicional **y sin intervención del ADJUDICATARIO**.» Si el histórico solo es legible desde un producto de 2012 cuyo modelo de datos nadie documentó, el CLIENTE no puede ejercer ese derecho por sí mismo.

**(d) Y mantendría viva la superficie de exposición que la decisión buscaba cerrar.** Un sistema sin soporte, accesible, en un operador de importancia vital, es la situación que BA, Art. 1.3 declara inaceptable y que BTT, RT-11.04 hace inejecutable. Dejarlo encendido «solo para consultar» conserva el problema con otro nombre.

**(e) Matriz de migración obligatoria.** Cada conjunto se concilia y prueba por separado; que un dato no se migre al núcleo nuevo no autoriza su eliminación si aún está dentro de retención.

| Conjunto | Alcance a migrar | Conciliación y aceptación | Destino del remanente retenido |
|---|---|---|---|
| Inventario | Completo al corte, con posición verificada físicamente | Recuento 100%, unicidad y barrido físico por bloque | No aplica: todo el inventario activo migra |
| Movimientos | Últimos 3 años | Recuento por período+día, integridad de secuencia y muestra de recuperación | Años 4 a 10 en repositorio consultable abierto |
| Hechos y evidencias facturables | Últimos 6 años | Correspondencia 1:1 hecho–evidencia, totales por período y recuperación dirigida | Repositorio consultable hasta completar 6 años |
| Maestros | Completos y vigentes, con historial necesario para interpretar datos migrados | Recuento, claves, relaciones y validación por dueño de dato | Versión exportable documentada |
| Tarifario | Versión vigente al corte | Comparación 100% de reglas, vigencias y excepciones | Versiones históricas ligadas a evidencias retenidas |
| Objeciones | Todas las abiertas, con expediente completo | Recuento 100%, estado, responsable y documentos | Cerradas retenidas con su evidencia según plazo aplicable |

**Fecha y condición de ejecución.** El apagado se ejecuta en el **mes 22**, un mes después de la aceptación final del proyecto de implementación (hito **H12**, mes 21, BA, Formulario E-25). Está condicionado a un **acta de conformidad del repositorio histórico** que acredite tres cosas: completitud contra recuentos de origen, legibilidad en formato abierto y documentado, y prueba de recuperación sobre una muestra dirigida —los tres criterios que BTT, RT-05.14 exige para la conciliación de migración.

La extracción y su conciliación son **entregable de la Etapa 2** y se verifican **antes del inicio de la marcha blanca de la Etapa 2 (mes 19)**, de modo que un fallo de extracción no se descubra cuando ya no queda margen.

**Riesgo residual.** Que el histórico antiguo esté bajo esquemas de datos anteriores al vigente, resultado de catorce años y cuatro proveedores. Se mitiga adelantando el **perfilado del histórico** al mismo trabajo de descubrimiento de los meses 1 a 4 (§6), en lugar de dejarlo para la Etapa 2. BTT, RT-05.12 ya exige ese perfilado con informe de defectos y decisión adoptada sobre cada uno.

---

### 15.2 Pendiente 2 — Umbrales de conciliación y ventana de investigación

**Resolución: se ratifican los umbrales porcentuales de posición y movimientos, se corrige su fundamento, se añade una regla direccional de clasificación y se diferencia la ventana.**

**(a) Corrección del fundamento.** La V3 anclaba el 0,5 % en la línea base de 3,1 % de contenedores mal ubicados (CP, 7.2). Ese anclaje confunde dos magnitudes: 3,1 % es error **registro contra realidad**; el umbral de conciliación mide **registro nuevo contra registro antiguo**. El fundamento correcto es otro: durante la convivencia **ambos sistemas registran los mismos eventos**, de modo que toda divergencia es desfase temporal —explicable por diseño— o defecto. El umbral no mide calidad del dato: mide **cuánta divergencia inexplicada se tolera antes de detener el avance**, que es literalmente lo que pide CP, 17.6, punto 2.

**(b) Regla direccional — elemento nuevo.** No toda divergencia es un defecto de la solución. Se espera que el sistema nuevo sea **más** exacto que el de 2012, porque captura posición con instrumentación en vez de con confirmación manual por radio. Cada divergencia se clasifica contra verificación física:

| Clasificación | Tratamiento |
|---|---|
| Explicada por desfase temporal | No computa |
| **El sistema nuevo resulta correcto** | No computa contra el umbral. Se registra como **evidencia de mejora** y alimenta el indicador del criterio de aceptación N° 9 (CP, Cap. 18) |
| **El sistema nuevo resulta incorrecto** | Computa. Es defecto |
| No resuelta dentro de la ventana | Computa como **no explicada**. Es la que detiene el avance (BA, Art. 17.3) |

Sin esta regla, la marcha blanca penalizaría a la solución precisamente por ser mejor que el sistema al que reemplaza. La clasificación exige una **muestra de verificación física por turno**, ejecutada con el método de barrido de §7.3 sobre un bloque rotativo.

**(c) Frecuencia — ratificada.** La conciliación por turno se ratifica con fundamento propio: el cambio de turno ya es, según el CP, Anexo B.1, el «punto de pérdida de información y de registros que se digitan tarde o no se digitan». Conciliar exactamente ahí convierte una debilidad conocida de la operación en un control.

**(d) Ventana — se diferencia según la naturaleza del objeto.**

| Universo | Ventana | Fundamento |
|---|---|---|
| Posición y movimientos | **48 h** | Con tres turnos rotativos, en 48 horas **cada dotación ha vuelto a estar de servicio al menos dos veces**, de modo que la persona que originó el registro puede ser consultada. Una ventana menor obligaría a cerrar la investigación sin poder preguntar |
| Gate y hechos facturables | **24 h** | Eventos discretos, contables e individualmente investigables, cuyo ciclo natural es el cierre diario (§15.3) |

**Riesgo residual.** Que las detenciones repetidas consuman la validación: BA, Art. 17.3 exige sostener los indicadores durante al menos las cuatro últimas semanas. La mitigación es completar todo despliegue, migración inicial y prueba de retorno **a más tardar el 14-dic-2027**; durante el congelamiento no se corrige ni despliega sobre producción. Si la consulta no admite la validación de solo lectura, se reprograma.

---

### 15.3 Pendiente 3 — Umbral del gate

**Resolución: cero diferencias no explicadas al cierre del día, con ventana de 24 horas. Se retira el 0,3 %.**

**(a) De esos registros sale un indicador contractual.** La estadía del camión se mide «desde la barrera de entrada hasta la de salida» (CP, Anexo C), es uno de los indicadores comprometidos en el contrato de concesión, y CP, Cap. 10, restricción 14 exige producirlos «de forma trazable y auditable, **no reconstruirlos**».

**(b) La situación de partida no admite margen.** El terminal acumula **tres semestres consecutivos sobre el umbral** (CP, 7.1), y CP, 13.2 advierte que «cada semestre adicional agrava la situación contractual».

**(c) El margen retirado no era despreciable.** Con 1.450 camiones diarios en promedio y hasta 2.600 en peak (CP, 14.1), un 0,3 % equivale a **entre 4 y 8 camiones por día sin explicación** — ruido suficiente para contaminar un indicador que ya está en incumplimiento y que se reporta semestralmente al concedente.

**(d) Cero es alcanzable aquí, y no lo sería en patio.** Un evento de gate es discreto y tiene hora, patente, contenedor y funcionario asociados: se investiga individualmente. Una posición de patio, sobre ~11.200 TEU en movimiento continuo, no admite el mismo tratamiento. **La diferencia de umbral entre ambos universos no es una inconsistencia: es que los objetos son de naturaleza distinta.**

Queda así alineado con el tratamiento de los hechos facturables, por la misma razón de fondo: **ambos producen evidencia con consecuencia externa** — contractual frente al concedente, económica frente al cliente.

---

### 15.4 Pendiente 5 — Tiempo de reversión y autoridad para ejecutarla

**Resolución: dos relojes acotados, autoridad local en los tres turnos y asimetría declarada a favor de revertir.**

**(a) Los dos relojes.**

| Tramo | Objetivo | Anclaje |
|---|---|---|
| Detección → decisión | **≤ 15 minutos** | BA, Art. 78.2 fija 15 minutos como tiempo máximo de **respuesta** ante incidente de severidad crítica. Una operación que compromete el registro con una nave amarrada es crítica por definición (BA, Art. 78.1) |
| Decisión → reversión efectiva | **≤ 15 minutos** | La reversión es una redirección de enrutamiento en la fachada (§7.2), no una restauración: es una operación de configuración pre-armada y probada |
| **Total detección → operación restituida** | **≤ 30 minutos** | |

**Por qué no se usa el tiempo de resolución de 4 horas del Art. 78.2:** cuatro horas con una nave amarrada equivalen, a 24,8 movimientos por hora de grúa (CP, 7.1), a un centenar de movimientos perdidos. El CP es explícito: la atención de una nave tolera minutos, no horas.

**(b) Autoridad — doble control normal y break-glass de emergencia.** En operación normal, la reversión requiere la aprobación conjunta de los dos cargos siguientes:

- el **supervisor de turno del CLIENTE**, que existe en los tres turnos por la operación 24×7×365 (CP, 2.4);
- el **jefe de turno de marcha blanca de Terabyte**, cuya presencia en terreno en los tres turnos, incluida la madrugada, ya es exigible por CP, 13.3, punto 8 y por CP, Cap. 15, **RT-21.16**.

En una emergencia que no admita esperar el segundo control, cualquiera de ambos podrá activar un procedimiento **break-glass previamente autorizado**: motivo obligatorio, privilegio temporal, alerta inmediata al otro cargo y al Comité, y revisión posterior. El escalamiento al Comité de Proyecto (BA, Art. 71°) es posterior al retorno y no una condición que paralice la emergencia.

**(c) Fundamento del diseño: la lección del 18 de febrero.** La decisión pendiente N° 10 del CP pregunta «a quién llega una alarma del patio refrigerado a las dos de la mañana, con qué escalamiento, con qué confirmación de recepción y **qué ocurre si nadie confirma**», y se responde a sí misma: «una alarma que nadie atiende es exactamente el resultado del 18 de febrero, sólo que con más registros». Una reversión que requiera la autorización de alguien que no está a las 03:00 tiene exactamente el mismo defecto de diseño. **La autoridad debe existir donde y cuando ocurre el problema.**

**(d) Asimetría declarada.** Revertir sin necesidad cuesta poco: mientras la escritura dual esté activa, el sistema de 2012 está al día y la operación continúa con el procedimiento vigente, que sigue existiendo durante toda la marcha blanca. No revertir cuando correspondía cuesta una nave detenida o una fila en el acceso vial. **Ante la duda se revierte, y se documenta.** La asimetría se declara expresamente para que la instrucción al turno de madrugada no sea ambigua — que es donde las instrucciones ambiguas se convierten en inacción.

---

### 15.5 Pendiente 6 — Frente de captura del conocimiento tácito

**Resolución: se incorpora a la Etapa 1 como frente propio, con entregable documental, independiente del módulo de planificación y anterior a él.**

**(a) Por qué no puede esperar al módulo.** La planificación asistida entra en producción en el **mes 21**. El planificador se retira «el 2028» sin mes declarado (CP, Cap. 8). Si el módulo es el único depositario previsto del conocimiento y él se va antes de que exista, el criterio de aceptación N° 22 —«Don Nibaldo se jubila en 2028 y el terminal sigue planificando igual o mejor»— falla sin remedio posible.

**(b) El entregable no es software: es un registro. Y ya es un entregable de esta célula.** CP, Cap. 17.1 exige un «registro de reglas de negocio» con «las reglas propias de la industria que la solución debe respetar y que este documento no explicita», enumerando entre ellas el «criterio de asignación de posición en patio». **No es trabajo adicional:** es reconocer que ese registro tiene fecha de caducidad puesta por una persona.

**(c) Método — el que el propio planificador describió.** En CP, Cap. 8: «lo que a mí me gustaría es que la máquina me proponga y yo corrija, y **que quede registrado por qué corregí**. Así el que venga después aprende de eso, no de mirarme a mí.» El método replica ese mecanismo **antes de que exista la máquina**: durante la Etapa 1 un analista elabora la propuesta de plan, el planificador corrige, y se registra el motivo de cada corrección. Eso produce simultáneamente el corpus de reglas, su validación, y el ensayo de la interacción que después tendrá con el motor. Es además la forma de captura que él ya declaró aceptar, lo que reduce el riesgo de rechazo que CP, Cap. 19 anticipa entre los riesgos propios de este proyecto.

**(d) Categorías mínimas a capturar**, todas derivadas de lo que el CP declara existente y no escrito (CP, 4.2 y Cap. 8):

| Categoría | Ejemplo textual del caso |
|---|---|
| Estado real de los equipos | «La grúa tres tiene una falla intermitente en el giro»; no asignarle trabajo pesado en turno de noche |
| Comportamiento físico de los bloques | «El bloque C se inunda cuando llueve fuerte del norte» |
| Particularidades de naves | Generador de popa limitado en cierta línea → reefers a proa |
| Comportamiento de clientes | Exportador cuya carga «siempre llega el último día» |
| Reglas normativas duras | Segregación IMDG, estabilidad, puerto de destino y disponibilidad de conexión reefer a bordo (CP, 4.2 y Cap. 12) |

**(e) La ventana de captura incluye la temporada, y eso es una ventaja.** La restricción 9 (CP, Cap. 10) prohíbe **intervenir sistemas** entre el 15 de diciembre y el 30 de abril. Acompañar y documentar a un planificador no es intervenir un sistema. Y es en temporada —patio al 90 %, reefer al máximo, hasta 380 eventuales por turno— cuando más restricciones tácitas se activan. **La captura debe cubrir al menos una temporada completa**, que es la única forma de recoger las reglas que solo aparecen bajo carga.

**(f) Fechas.** Primera versión del registro **antes del hito H2 (mes 4)**, para que alimente el modelo de datos que ese hito compromete. Versión validada con el planificador **antes del cierre de desarrollo de la Etapa 1 (mes 12)**. El frente arranca en el **mes 1**, no cuando haya módulo.

**Riesgo residual.** Que el planificador se retire antes de lo previsto. Se mitiga con el arranque temprano y con la consulta C4 (§12.3) sobre su fecha.

---

### 15.6 Pendiente 7 — Supuesto sobre el vencimiento del soporte

**Resolución: se reemplaza el supuesto optimista por uno conservador, y el problema se reencuadra como riesgo estructural común a las tres opciones.**

**(a) Por qué no se puede suponer la lectura generosa.** La V3 proponía suponer que el soporte cubre todo 2028. **BA, Art. 5.4 lo impide expresamente:** presentada la oferta, «se entenderá que el PROPONENTE aceptó **la interpretación más exigente**» y no podrá invocar la contradicción como fundamento de mayor precio, plazo o menor alcance. Y BA, Art. 5.3: ante discrepancia dentro de un mismo documento «prevalecerá **la más exigente para el ADJUDICATARIO**». Apoyar el plan en la lectura favorable de una ambigüedad es exactamente lo que las bases prohíben.

**(b) Supuesto adoptado (S5, corregido):** se asume que el soporte del fabricante **puede vencer tan pronto como el 1 de enero de 2028**, y el plan se evalúa contra ese escenario.

**(c) El hallazgo que reencuadra el problema.** Con la entrega de resultados el **01-12-2026** (BA, Formulario T-20, actividad 14), más los plazos de contratación —10 días hábiles para presentar la documentación (BA, Art. 67°) y 10 días hábiles para suscribir el Contrato (BA, Art. 68°)—, el contrato no puede iniciarse antes de enero de 2027. Y la producción de la Etapa 1 ocurre en el **mes 16** (BA, Art. 17.1), plazo **obligatorio, indivisible y no negociable** (Art. 17.1). Por lo tanto:

> **La producción de la Etapa 1 no puede ocurrir antes de abril de 2028 en ninguna oferta admisible.**

De ahí se sigue algo decisivo para la defensa de la decisión: **ninguna estrategia —tampoco el reemplazo integral— puede sacar el registro operacional del sistema de 2012 antes de abril de 2028.** Si el soporte venciera en enero de 2028, existe una ventana de exposición de algunos meses que **es estructural del calendario contractual y no consecuencia de la opción elegida**. La decisión adoptada no la crea: la hereda igual que cualquier alternativa. Eso convierte lo que parecía un defecto del plan en un riesgo declarado y común, que es una posición defendible ante la Comisión.

**(d) Mitigación — y por qué la opción adoptada la mejora.** La exposición se acota con controles que ya están en el alcance por otras razones: la **segregación de la red operacional** respecto de la administrativa y de las 142 cámaras (CP, Cap. 10, restricción 6) y el **endurecimiento conforme a CIS Benchmarks** con gestión centralizada de parches (BTT, RT-03.15). A eso se suma un efecto propio del patrón adoptado: **una vez interpuesta la capa anticorrupción, nada accede directamente al sistema de 2012**, lo que reduce su superficie de exposición **desde los meses 4 a 6, y no desde el mes 16**. La fachada, adoptada por razones de convivencia y reversibilidad, resulta ser también el control compensatorio que acota la ventana de 2028 **antes** de lo que la acotaría cualquier otra estrategia.

**(e) Consecuencia sobre la declaración central.** Se mantiene, precisada: al vencimiento del soporte, ningún componente del registro oficial permanece en el sistema de 2012 **si el soporte vence a partir de mayo de 2028**. Si venciera antes, existe una ventana de exposición estructural, declarada, acotada y mitigada según (d). La consulta C2 (§12.3) busca cerrar esa indeterminación.

---

### 15.7 Pendiente 8 — Redacción y presentación de las consultas

**Resolución: Célula 2 redacta el contenido técnico; el delegado del equipo presenta. Y hay una urgencia que no admite diferirse.**

**(a) Plazo — atención.** El período de consultas corre del **20-08-2026 al 01-09-2026** (BA, Formulario T-20, actividad 4). **A la fecha de este documento queda esencialmente un día.** Cerrado el período, BA, Art. 5.4 hace inoponible cualquier contradicción no planteada: «Presentada la oferta, se entenderá que el PROPONENTE aceptó la interpretación más exigente». Las cuatro consultas de §12.3 pierden su vía si no entran ahora.

**(b) Responsable.** El contenido técnico lo redacta **Célula 2**, porque las cuatro consultas nacen de su análisis. La presentación corresponde al **delegado del equipo (Daniel Miranda)**, dado que BA, Art. 12.1 establece que las comunicaciones del proceso se cursan a través del **Representante registrado** de cada proponente, y Art. 12.4 hace responsabilidad exclusiva del proponente mantener ese canal operativo.

**(c) Forma — es excluyente y no conviene improvisarla.** BA, Art. 43.2 exige planilla con siete columnas: (A) correlativo, (B) empresa, (C) fecha, (D) tipo —Administrativa, Técnica o Anexo—, (E) documento, sección, artículo y página, (F) consulta detallada, (G) propuesta de interpretación del proponente. BA, Art. 43.3 fija la nomenclatura `CONSULTAS_[EMPRESA]_AAAAMMDD.XLSX`.

**(d) La columna E obliga a un trabajo previo.** Exige documento, sección, **artículo y página**. Este documento cita por estructura y no por página; convertir las cuatro consultas al formato exigido requiere localizar la página de cada referencia en los PDF oficiales. Es trabajo mecánico pero no instantáneo, y hay que contarlo dentro del día disponible.

---

### 15.8 Pendiente 9 — Contraste de las referencias sectoriales

**Resolución: se incorporan dos fuentes arbitradas y se reasigna qué sostiene cada afirmación. Las fuentes sectoriales quedan como referencia de orden de magnitud y no sostienen ningún descarte.**

**(a) Gekara y Nguyen (2020)**, *Journal of International Logistics and Trade*, 18(1), 49-60, documenta un caso en que «el intento de adoptar e implementar un TOS en el puerto **en su mayor parte fracasó**», y atribuye el fracaso a «una combinación compleja de factores **tecnológicos, organizacionales y ambientales**», entre ellos que «el entorno de negocio más amplio estaba mal equipado con la infraestructura TIC necesaria para soportar una implementación efectiva» y «una falta general de trabajadores adecuadamente capacitados».

Es la referencia que corresponde al argumento de capacidad de absorción, y es más pertinente que la fuente comercial que ocupaba ese lugar, porque **los tres factores que identifica están documentados en este caso**: infraestructura TIC insuficiente —red de patio de 2013 cuyas zonas de sombra cambian durante el día, sala de servidores de 34 m² que no cumple el estándar, redes operacional y administrativa sin segregar compartidas con 142 cámaras (CP, Cap. 6)— y dotación técnica escasa —cinco personas de TI en un operador de importancia vital (CP, Cap. 10, restricción 11).

**(b) Alnıpak (2026)**, *Systems*, 14(2), 147, establece que «los errores en la selección de un TOS tienen un efecto perjudicial demostrado sobre la productividad del terminal», e identifica entre los obstáculos de implementación las deficiencias de infraestructura TIC y la insuficiente preparación de la fuerza de trabajo.

**(c) Reasignación de cargas.** Con esas dos fuentes, ninguna afirmación estructural del documento depende ya de literatura no arbitrada:

| Afirmación | Antes se apoyaba en | Ahora se apoya en |
|---|---|---|
| El reemplazo integral concentra un riesgo de adopción difícil de absorber por este cliente | Indie Hackers (2026) | **Gekara y Nguyen (2020)**; la fuente sectorial pasa a orden de magnitud |
| Una selección o transición mal ejecutada degrada la productividad del terminal | Indie Hackers (2026) | **Alnıpak (2026)** |
| Duración típica de una implantación de TOS | The Intech Group (2026) | The Intech Group (2026), **como referencia indicativa y no como fundamento del descarte** (§3.2 y §3.3) |

**(d) Lo que no se cierra aquí.** Las cifras de 4-8 meses de ingeniería de datos y de 10-20 % / 20-40 % de impacto siguen proviniendo de fuente no arbitrada. Se mantienen como orden de magnitud declarado y **no sostienen ningún descarte**. Sustituirlas por evidencia arbitrada equivalente es tarea de mejora para el Informe 2, no bloqueo del Informe 1.

---

### 15.9 Pendientes que se mantienen abiertos deliberadamente

| N° | Pendiente | Por qué no se resuelve aquí |
|---|---|---|
| **4** | Segmentación del patio en bloques, duración del barrido por bloque, número de turnos del barrido completo y porcentaje de capacidad resignada | **Se mantiene abierto por decisión de la célula.** Cambia, eso sí, su vía de resolución: deja de estar sujeto a consulta y pasa a ser **supuesto declarado de ingeniería** conforme a CP, Cap. 14 (§12.2). La cuantificación de la capacidad resignada sigue siendo exigible por CP, 13.3, punto 2 |
| **10** | Valorización económica de la decisión | Corresponde al **Informe 3** (BA, Formulario T-22). En el Informe 1 la fila de costos identifica **dónde** está el gasto de cada opción, no su monto (§1.4 de la V3, recogido en §3) |
| **11** | Traspaso a Célula 3 para el registro de decisiones de arquitectura | Es tarea de **coordinación**, no decisión técnica. BTT, RT-02.04 sitúa el ADR en el Subdocumento 4, responsabilidad de Célula 3; este documento es su insumo |

---

## Referencias

Alnıpak, S. (2026). Investigating the structural dynamics of terminal operating system selection: A holistic framework from automation to intelligence in container terminals. *Systems, 14*(2), 147. https://doi.org/10.3390/systems14020147

Evans, E. (2003). *Domain-driven design: Tackling complexity in the heart of software*. Addison-Wesley.

Fowler, M. (2004a, 29 de junio). *Strangler fig application*. https://martinfowler.com/bliki/StranglerFigApplication.html

Fowler, M. (2004b, 29 de junio). *Asset capture*. https://martinfowler.com/bliki/AssetCapture.html

Gekara, V., & Nguyen, X. V. (2020). Challenges of implementing container terminal operating system: The case of the port of Mombasa from the Belt and Road Initiative (BRI) perspective. *Journal of International Logistics and Trade, 18*(1), 49-60. https://doi.org/10.24006/jilt.2020.18.1.049

Indie Hackers. (2026, 3 de junio). *We help ports choose terminal operating systems: What the procurement process gets wrong*. https://www.indiehackers.com/post/we-help-ports-choose-terminal-operating-systems-heres-what-the-procurement-process-gets-wrong-almost-every-time-eda29c494d

Market Intelo. (2026). *Terminal operating systems market research report 2034*. https://marketintelo.com/report/terminal-operating-systems-market

Microsoft. (2025a). *Strangler fig pattern*. Azure Architecture Center. https://learn.microsoft.com/en-us/azure/architecture/patterns/strangler-fig

Microsoft. (2025b). *Anti-corruption layer pattern*. Azure Architecture Center. https://learn.microsoft.com/en-us/azure/architecture/patterns/anti-corruption-layer

Project Management Institute. (2017). *Guía de los fundamentos para la dirección de proyectos (Guía del PMBOK)* (6.ª ed.).

The Intech Group. (2026, 16 de junio). *TOS buyer's guide 2026: Choosing the right terminal operating system*. https://theintechgroup.com/blog/tos-buyers-guide-terminal-operating-system/

**Nota sobre la calidad de las fuentes.** Gekara y Nguyen (2020) y Alnıpak (2026) son literatura arbitrada e incorporadas en §15.8 para sostener las afirmaciones estructurales sobre capacidad de absorción y riesgo de transición.

Indie Hackers (2026), Market Intelo (2026) y The Intech Group (2026) son publicaciones sectoriales de carácter comercial, no literatura arbitrada. Las citas de The Intech Group (2026) e Indie Hackers (2026) fueron **verificadas contra la fuente y son fieles**. Sus cifras se emplean como referencia indicativa de órdenes de magnitud y **no sostienen por sí solas ningún descarte** (§3.3 y §15.8). Sustituirlas por evidencia arbitrada equivalente queda como tarea de mejora para el Informe 2.

---

*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. Referencias normativas a BA FEP01.26, BTT FEP02.26 y CP FEP03.06.26, v1.0 de 18-08-2026. Este documento consolida y reemplaza a «Propuesta de solución V3».*
