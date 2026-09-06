# Subdocumento 5 — Modelo y gestión de datos

**Caso:** 06 Portuaria — TERABYTE · **Célula 4** (V. Guzmán / M. Reyes)
**Informe 1** · ponderación 11 % · versión 1.0 · 6 de septiembre de 2026

> **Este archivo es una conversión de lectura del documento LaTeX, no la fuente.**
> La fuente de verdad es el proyecto `Documento terabyte SubDoc 5`, que compila
> con pdfLaTeX en 103 páginas. Esta versión en Markdown existe para leer, buscar
> y citar el contenido sin compilar, y para que el resto del equipo pueda
> revisarlo con las mismas herramientas que usa el material de las otras células.
> Si hay discrepancia entre este archivo y el PDF, manda el PDF.

---

# Modelo y Gestión de Datos

*Subdocumento 5*

## Alcance, método y estado de este subdocumento

Este subdocumento responde las seis exigencias del Formulario T-7 para el Subdocumento 5 (BA, Form. T-7 — modelo y gestión de datos) y las trece materias del índice oficial del Informe 1. Pondera un 11 % de la evaluación técnica del Informe 1 (BA, Form. T-21 — ponderación de la evaluación técnica), y el Formulario T-22 lo incluye entre los subdocumentos del Informe 1 aunque no le dedique una viñeta propia en la agenda de la presentación; la regla conservadora adoptada es desarrollarlo completo conforme al T-7 \[PROPUESTA TERABYTE\].

### Regla de cita y colisión de códigos

Los códigos `RT` se repiten entre documentos designando materias distintas. El caso verificado más relevante para este subdocumento es `RT-05.10`: en las Bases Técnicas Transversales designa el catálogo de datos con linaje automatizado, de carácter deseable, mientras que en las Bases Técnicas del Caso designa la retención de datos históricos y de auditoría, de carácter “según caso”. Lo mismo ocurre con `RT-05.15` y con `RT-03.24`. Por eso ninguna afirmación de este subdocumento cita un código suelto: la referencia mínima es **documento + capítulo + código + materia** \[HECHO\].

### Estados de avance declarados

Cada apartado declara la estabilidad del respaldo documental disponible, no si el texto está redactado. Se usan cuatro estados:

| **Estado**                                         | **Significado operativo**                                                                                                                                   |
|:-------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| completado              | Respaldo real y estable en las Bases, el Caso o el cierre vigente de Célula 2. Se puede cerrar ahora.                                                           |
| completado provisional  | Se puede redactar, pero se apoya en material de Célula 3 que aún puede cambiar. Se declara el documento de apoyo, la decisión asumida y qué habría que rehacer. |
| pendiente — otra célula | El vacío pertenece a otra célula y no se completa por cuenta propia.                                                                                            |
| pendiente — Célula 4    | El vacío es propio y nadie más lo resolverá.                                                                                                                    |

### Estado de las dependencias al cierre de esta versión

> **HECHO.** La línea base de Célula 2 utilizada es la posterior a las rondas de corrección del 5 de septiembre de 2026: **139 requerimientos funcionales, 91 requerimientos no funcionales, 11 reglas de negocio, 21 decisiones y 25 supuestos**, con reparto de 82 requerimientos en Etapa 1 y 57 en Etapa 2 (Célula 2 · cierre y anexos de segunda y tercera ronda). No se usa la línea base del 4 de septiembre (138 requerimientos funcionales y 84 no funcionales), que quedó superada.

> **DUDA.** La entrega de Célula 3 (Subdocumento 4) **no está cerrada**: sus nueve secciones de contenido figuran como “pendiente de integrar” y sus decisiones de arquitectura están en estado candidato. Todo lo que este subdocumento apoya en Célula 3 queda marcado como provisional, con su riesgo de cambio declarado en el Anexo F. Ninguna de esas afirmaciones se presenta como hecho confirmado.

### Resumen de estados por apartado

| **§* | **Materia del checklist oficial**             | **Estado**                                |
|:--------|:--------------------------------------------------|:----------------------------------------------|
| 5.2     | Dominios y entidades principales                  | completado     |
| 5.3     | Fuentes oficiales y fuente de verdad              | completado     |
| 5.4     | Paradigma de persistencia y motores propuestos    | completado     |
| 5.5     | Transaccionalidad, consistencia y disponibilidad  | completado     |
| 5.6     | Separación transaccional, temporal y analítica    | completado     |
| 5.7     | Telemetría y frecuencia de muestreo               | completado     |
| 5.8     | Integración e interoperabilidad de datos          | pendiente — C3 |
| 5.9     | Migración, saneamiento, validación y conciliación | completado     |
| 5.10    | Estrategia de desempeño de datos                  | completado     |
| 5.11    | Calidad ISO/IEC 25012, auditoría y trazabilidad   | completado     |
| 5.12    | Retención, archivo y eliminación segura           | completado     |
| 5.13    | Volumetría actual, proyectada y de peak           | completado     |
| 5.14    | Modelo conceptual y diccionario inicial de datos  | completado     |

*Tabla. Estado del respaldo documental por apartado del Subdocumento 5.*

**Doce apartados completados y uno pendiente** por información de Célula 3 — los contratos de integración, que no se completan por cuenta propia. Los ocho pendientes propios de Célula 4 declarados en la versión 0.9 quedan cerrados en esta versión, con **veintiuna decisiones** registradas y **veinte dependencias** trazadas a su célula responsable. Las trece materias del checklist oficial quedan cubiertas.

## Dominios de información y entidades principales

**Estado: Completado**

El modelo de datos se organiza en diez dominios de información con frontera explícita. Cada dominio declara propietario del dato, productor, consumidor y autoridad de escritura, y clasifica su contenido como operacional, maestro, personal, comercial sensible, evidencia o telemetría. La obligación de fondo es doble: entregar el modelo documentado con diccionario de datos que declare nombre, tipo, dominio de valores, obligatoriedad, propietario y sensibilidad de cada atributo (BTT, Cap. 5, RT-05.01 — modelo y diccionario de datos), y evitar la duplicación de entidades compartidas entre módulos y con sistemas externos mediante una estrategia de datos maestros (BTT, Cap. 5, RT-05.09 — gestión de datos maestros). Las Bases Administrativas añaden la exigencia de linaje y propietario por dominio (BA, Art. 23 — datos, integración e interoperabilidad).

| **Dominio**         | **Objetos y eventos mínimos**                                                                    | **Clase dominante** |
|:------------------------|:-----------------------------------------------------------------------------------------------------|:------------------------|
| Contenedor y operación  | contenedor, visita, movimiento, custodia, estado, *movimiento registrado*                            | operacional             |
| Patio y posición        | bloque, ubicación, condición dinámica, asignación, verificación, *posición actualizada*              | operacional             |
| Gate y transporte       | camión, conductor, cita, documento, entrada, salida, excepción                                       | operacional y personal  |
| Reefer y cadena de frío | contenedor refrigerado, toma, tablero, muestra, consigna, alarma, confirmación                       | telemetría y evidencia  |
| Nave y planificación    | recalada, plan de estiba, instrucción de embarque, asignación de equipo, corrección del planificador | operacional             |
| Inspecciones            | solicitud, cita, autoridad, remoción, acta, resultado                                                | evidencia               |
| Evidencia y facturación | hecho facturable, evidencia, firma, objeción, estado en el sistema de gestión empresarial            | evidencia y comercial   |
| Acceso e identidad      | persona, nombrada, credencial, rol, zona, sesión, acceso auditado                                    | personal                |
| Energía y emisiones     | equipo, consumo, factor de emisión, cálculo, emisión por contenedor, verificación                    | operacional             |
| Integración y auditoría | mensaje, contrato, correlación, idempotencia, error, reintento, conciliación                         | operacional             |

*Tabla. Dominios de información y su contenido mínimo.*

\> **Figura — Mapa de dominios de información, sistemas conservados y contrapartes externas** · diagrama ‘D01_mapa_dominios‘

*Nota. La flecha gruesa representa la relación de autoridad del dato, que se resuelve por la terna dominio $\times$ zona $\times$ fase del numeral 5.3. Las flechas punteadas marcan interfaces cuya habilitación sigue pendiente de levantar.*

> **PROPUESTA DE TERABYTE.** La lista de dominios es una descomposición de Terabyte y admite fusión o división justificada. Lo que no se admite es crear una tabla, un esquema o un almacén independiente por cada requerimiento funcional: la solución tiene 139 requerimientos funcionales vigentes y un equipo de tecnologías de información del CLIENTE de cinco personas, de modo que la operabilidad es un criterio de diseño de datos y no solo de arquitectura.

Dos entidades incorporadas por el corte del 5 de septiembre de 2026 deben quedar explícitas en el modelo, porque distinguen dos flujos que antes se confundían (Célula 2 · RF-POR-09 y RF-INT-02): la **instrucción de embarque presentada por el embarcador o su agencia** a través del portal, que es el flujo al que el caso atribuye íntegramente el 41 % de documentación redigitada, y la **orden de embarque recibida desde la naviera** por mensajería estándar. Son objetos distintos, con propietario, contrato y evidencia distintos.

> **DUDA.** Los identificadores definitivos de los contextos lógicos los produce Célula 3 en su entregable de arquitectura lógica, que aún no existe. Este subdocumento usa identificadores propios y estables de dominio y mantiene, en el Anexo H, una tabla de equivalencia de una sola columna para mapearlos cuando Célula 3 los publique. No es un bloqueo.

## Fuentes oficiales y fuente de verdad

**Estado: Completado**

### Fuentes oficiales de datos

El panorama de sistemas existentes fija qué es fuente oficial y qué no (CP, Cap. 5 — los sistemas que existen hoy). El sistema de gestión empresarial se mantiene y sigue siendo el único emisor de documentos tributarios: la solución le entrega los hechos facturables y no habrá dos emisores \[HECHO\]. El sistema de control de las grúas de muelle no se interviene y cualquier obtención de datos desde él es una integración de solo lectura sujeta a autorización del fabricante \[HECHO\]. El sistema de control de acceso y videovigilancia se conserva como subsistema de protección. El portal de consulta de 2016 se reemplaza. El correo electrónico y las planillas de cálculo deben desaparecer como sistema de registro, lo que es, en buena medida, el objeto de la licitación \[HECHO\].

### Fuente de verdad de la posición del contenedor

La fuente de verdad no se define en este subdocumento: ya está resuelta como decisión de célula par y aquí se reutiliza sin redefinirla (Célula 2 · Decisión N.<sup>o) 1, §5.2, y RF-CON-14</sup>. La autoridad sobre el dato se determina por la tripleta **dominio $\times$ zona $\times$ fase**:

1.  antes del corte de una zona, la autoridad es del sistema de operación de 2012;

2.  durante la validación paralela, el sistema nuevo opera solo como lector o sombra;

3.  después del corte aprobado, la autoridad es del sistema nuevo y el sistema legado recibe réplica únicamente para permitir el retorno;

4.  el cruce de un contenedor entre zonas es una **transferencia transaccional**: el sistema con autoridad emite un evento secuenciado e idempotente, el receptor confirma persistencia y solo entonces cambia la autoridad;

5.  un fallo parcial mantiene la autoridad anterior, deja el evento en cola y bloquea una segunda transferencia hasta conciliarlo.

En ningún momento dos sistemas aceptan escrituras autoritativas sobre el mismo contenedor y dominio. El fundamento normativo es la exigencia de una única fuente de verdad para los datos compartidos y de evitar toda doble digitación (BA, Art. 17.2 — única fuente de verdad).

> **SUPUESTO.** Se asume que la matriz de autoridad que publicará Célula 3 nombrará las mismas zonas y fases que la decisión de Célula 2, sin redefinir el concepto. A la fecha de esta versión, esa matriz figura como “por completar” en el entregable de procesos críticos de Célula 3 (Célula 3 · procesos críticos y convivencia con el sistema de 2012 · PROVISIONAL). Si la definición de zona o de fase cambia, deben rehacerse este apartado y la conciliación descrita en el §5.9. Por eso las zonas y fases se mantienen parametrizadas y no enumeradas en el modelo de datos.

### Matriz de propiedad del dato

El Anexo A desarrolla, por dominio, la matriz *dato propietario fuente de verdad sensibilidad clase de retención*, distinguiendo la fuente de verdad actual, la vigente durante la coexistencia y la final.

## Paradigma de persistencia y motores propuestos

**Estado: Completado**

### Obligación y método

Las bases exigen justificar la selección del paradigma y del motor de persistencia — relacional o no relacional —, las garantías transaccionales y la posición escogida entre consistencia y disponibilidad conforme al teorema CAP, **para cada dominio de datos** y no para la solución en bloque (BTT, Cap. 5, RT-05.02 — selección de paradigma y motor). El método adoptado es, por tanto, clasificar primero cada familia de datos por su necesidad dominante, comparar al menos dos alternativas reales por familia y recién entonces recomendar \[PROPUESTA TERABYTE\].

| **Familia de datos**             | **Necesidad dominante**                                          | **Alternativas a comparar**                                                               |
|:-------------------------------------|:---------------------------------------------------------------------|:----------------------------------------------------------------------------------------------|
| Estado operacional                   | transaccionalidad ACID, integridad referencial y consistencia fuerte | motor relacional gestionado frente a motor relacional operado localmente o en esquema híbrido |
| Series temporales (reefer y equipos) | alta tasa de ingesta, orden temporal y retención diferenciada        | extensión temporal sobre el motor relacional frente a motor de series temporales dedicado     |
| Documentos, imágenes y evidencia     | almacenamiento de objetos, metadatos e inmutabilidad                 | almacenamiento de objetos con índice frente a gestor documental                               |
| Analítica e indicadores              | lectura agregada sin cargar la operación                             | réplica con modelo analítico frente a almacén analítico separado                              |
| Histórico retenido no migrado        | consulta de baja frecuencia, formato abierto y retención larga       | repositorio consultable en formato abierto frente a motor de archivo dedicado                 |

*Tabla. Familias de persistencia y alternativas que deben compararse.*

### Resultado de la comparación

Se compararon **trece alternativas** sobre siete criterios ponderados, cuya ponderación es decisión declarada de Terabyte y no proviene de las Bases. El detalle completo está en el Anexo (ver anx:persistencia).

| **Familia**        | **Paradigma recomendado**                                 | **Ponderado** |
|:-----------------------|:--------------------------------------------------------------|:------------------|
| Estado operacional     | relacional, primario en el borde con réplica a la nube        | 4,30              |
| Series temporales      | relacional con extensión temporal, sobre el mismo motor       | 4,70              |
| Documentos y evidencia | almacenamiento de objetos con índice y sello en el relacional | 5,00              |
| Analítica              | réplica de solo lectura con modelo semántico documentado      | 4,50              |
| Histórico retenido     | repositorio abierto sobre almacenamiento de objetos           | 5,00              |

*Tabla. Recomendación de paradigma por familia de persistencia.*

> **PROPUESTA DE TERABYTE.** **Dos motores, no cinco.** Las familias de estado operacional, series temporales y analítica se consolidan sobre un mismo motor relacional — una instancia primaria, una extensión temporal y una réplica de lectura —, y las de documentos e histórico sobre almacenamiento de objetos. Es la configuración que satisface (BTT, Cap. 5, RT-05.02 — paradigma y motor) y (BTT, Cap. 5, RT-05.05 — separación transaccional y analítica) con la menor superficie operacional posible, que es lo que la restricción no negociable N..º 11 — cinco personas en tecnologías de información — obliga a tratar como criterio de diseño.

> **HECHO.** La autonomía de 72 horas **no es un criterio ponderable sino de admisibilidad**. La alternativa con el primario en nube gestionada puntúa 4,00 frente a 4,30 de la elegida, una diferencia estrecha; pero situar el primario fuera del recinto incumple la restricción no negociable N..º 4 y se evalúa como falta de comprensión del caso, cualquiera sea su mérito en el resto de los criterios.

### Restricción que condiciona toda la sección

Ninguna familia crítica puede depender de la nube para registrar. El caso exige un mínimo de **72 horas continuas** de operación completa del terminal sin enlace hacia el exterior — atención de nave, registro de movimientos, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables — y que las terminales de los equipos de patio sostengan **8 horas continuas** fuera de cobertura inalámbrica sin pérdida de registro (CP, Cap. 15, RT-03.10 — operación desconectada del componente on-premise). Esa exigencia es anterior a cualquier elección de motor y la condiciona.

> **SUPUESTO.** Se asume que la capa de datos se descompone en almacenamiento operacional, de series temporales, documental y analítico, según el catálogo lógico inicial de Célula 3 (Célula 3 · maestro de contexto de arquitectura, §6 y §6.1 · PROVISIONAL). Ese catálogo se declara a sí mismo “inicial” y refinable. Si Célula 3 fusiona o renombra esos componentes, debe rehacerse la matriz de familias de este apartado, la separación de almacenamientos del §5.6 y el mapeo de cada entidad a su almacén en el diccionario del §5.14.

> **DUDA.** La recomendación de motor por familia y la comparación de alternativas **no están cerradas** en esta versión, y no deben cerrarse antes de conocer el emplazamiento. Este subdocumento entrega la necesidad y la preferencia técnica; la elección de producto, versión y emplazamiento corresponde a la arquitectura física de Célula 3, hoy en estado candidato. No se nombra ningún producto comercial en esta versión: hacerlo antes de la comparación sería una decisión tomada por omisión, que es exactamente lo que el caso sanciona.

## Transaccionalidad, consistencia y disponibilidad

**Estado: Completado**

### Unidad transaccional e invariantes

Se declara, por dominio, la unidad transaccional y las invariantes que exigen consistencia fuerte, frente a las que toleran consistencia eventual. La posición entre consistencia y disponibilidad se analiza **por operación** y no como una elección global de la solución. Toda escritura reintentable requiere clave de idempotencia y ventana de deduplicación; toda llamada remota requiere tiempo máximo de espera explícito \[PROPUESTA TERABYTE\].

### Comportamiento bajo partición

Restablecido el enlace, la sincronización debe ser automática, con reconciliación determinista de conflictos, regla de resolución documentada y bitácora auditable de las decisiones aplicadas (BTT, Cap. 3, RT-03.12 — sincronización tras la reconexión). El caso endurece el plazo: la sincronización no debe superar **90 minutos** tras 72 horas de desconexión, sin intervención manual, sin pérdida de ningún movimiento ni de ningún hecho facturable, y con **resolución determinista de los conflictos de posición de contenedor** producidos durante la desconexión (CP, Cap. 15, RT-03.13 — sincronización tras la reconexión).

> **PROPUESTA DE TERABYTE.** La resolución de conflictos de posición no puede resolverse con la regla “la última escritura gana”. La posición es un dato con autoridad territorial declarada, y una escritura posterior emitida por un sistema sin autoridad sobre esa zona no debe prevalecer sobre una anterior emitida por el sistema que sí la tenía. La regla de resolución se deriva de la matriz *dominio $\times$ zona $\times$ fase* del §5.3 y se documenta con su bitácora, conforme exige `RT-03.12` del documento transversal.

### Disponibilidad, recuperación y respaldo

| **Control**                              | **Umbral**                  | **Origen**                             |
|:---------------------------------------------|:--------------------------------|:-------------------------------------------|
| Disponibilidad mensual de servicios críticos | 99,9 % extremo a extremo        | `BTT`, Cap. 10, `RT-10.01`                 |
| Objetivo de tiempo de recuperación (RTO)     | $\leq$ 4 horas                  | `RNF-DIS-13` (Célula 2 · corte 05-09-2026) |
| Objetivo de punto de recuperación (RPO)      | $\leq$ 15 minutos               | `RNF-DIS-13` (Célula 2 · corte 05-09-2026) |
| Estrategia de respaldo                       | 3-2-1-1-0                       | `RNF-DIS-14` (Célula 2 · corte 05-09-2026) |
| Prueba de recuperación ante desastres        | semestral, con conmutación real | `RNF-DIS-15` (Célula 2 · corte 05-09-2026) |
| Operación desconectada del terminal          | $\geq$ 72 horas continuas       | `CP`, Cap. 15, `RT-03.10`                  |
| Sincronización posterior                     | $\leq$ 90 minutos               | `CP`, Cap. 15, `RT-03.13`                  |

*Tabla. Umbrales de disponibilidad, recuperación y continuidad aplicables a la capa de datos.*

### Posición entre consistencia y disponibilidad, por operación

El teorema no obliga a escoger dos propiedades de tres: obliga a elegir entre consistencia y disponibilidad **cuando ocurre una partición**. Sin partición la elección no se plantea, y por eso este subdocumento nombra primero las seis particiones reales del caso — terminal contra exterior, solución contra el sistema de 2012, equipo de patio fuera de cobertura, concentrador refrigerado contra el núcleo, contraparte que no responde, y primario contra réplica analítica — y recién después clasifica. Cinco de las seis están declaradas en las Bases o en el cierre de Célula 2.

De las **veinticinco operaciones** analizadas en el Anexo (ver anx:cap), dieciséis priorizan disponibilidad y nueve priorizan consistencia.

> **HECHO.** Las cinco funciones críticas de las 72 horas —atención de nave, registro de movimientos, entrada y salida por gate, control del patio refrigerado y registro de hechos facturables— son **todas** de disponibilidad. Y ninguna de las nueve operaciones que priorizan consistencia es de registro: o requieren a un tercero para existir, o producirían un dato falso si continuaran.

### Resolución determinista de conflictos de posición

(CP, Cap. 15, RT-03.13 — sincronización tras la reconexión) exige resolución determinista de los conflictos de posición producidos durante la desconexión, y (BTT, Cap. 3, RT-03.12 — reconciliación) exige regla documentada y bitácora auditable. La regla es una cascada de cuatro niveles aplicados en orden:

1.  **Autoridad**: prevalece el registro emitido por el sistema que tenía autoridad sobre ese dominio, zona y fase en el instante del hecho;

2.  **credibilidad de la fuente**: a igual autoridad, telemetría sobre lectura óptica, y ambas sobre la vía manual de excepción;

3.  **orden secuencial** de la visita;

4.  **verificación física**: si los tres anteriores no resuelven, la posición **no se resuelve automáticamente** y pasa a *por verificar* con tarea dirigida.

> **PROPUESTA DE TERABYTE.** El cuarto nivel es deliberadamente no automático. Resolverlo escogiendo el registro más reciente subiría el indicador y bajaría la verdad: el compromiso no es cero posiciones dudosas, sino que **toda posición declarada conocida sea correcta**, con el residual acotado a las marcadas *por verificar* no resueltas al cierre de turno.

### Funciones no disponibles en modo desconectado

(BTT, Cap. 3, RT-03.13 — declaración de funciones no disponibles) obliga a declarar qué funciones no operan sin enlace y qué procedimiento manual las suple, y advierte que **la ausencia de esta declaración se evalúa como observación grave**. Las nueve funciones afectadas, con su procedimiento de reemplazo y su tratamiento al reconectar, están en el Anexo (ver anx:cap). Ninguna función crítica de registro aparece en esa lista, y ninguna de las funciones diferidas se sustituye por una estimación.

\> **Figura — Ciclo de vida de la visita de un contenedor** · diagrama ‘D09_ciclo_visita‘

*Nota. El estado *liberable* es reversible: se alcanza cuando se cumplen simultáneamente las cinco condiciones de RN-06 y se abandona en cuanto alguna deja de cumplirse.*

> **HECHO.** Los objetivos de recuperación y la política de respaldo son límites generales ante una interrupción mayor. **No autorizan detener el gate ni el muelle ni perder registros ante la pérdida del enlace**: ese escenario se rige por la operación desconectada de 72 horas, que es más exigente.

### Umbrales de conciliación durante la coexistencia

Durante la marcha blanca, ambos registros conviven y toda divergencia es desfase temporal explicable por diseño o bien defecto. Se aplican umbrales diferenciados por naturaleza del objeto (Célula 2 · Decisión N.<sup>o) 1, §15.2 y §15.3</sup>:

- **Gate y hechos facturables:** cero diferencias no explicadas al cierre del día, con ventana de investigación de 24 horas. Son eventos discretos, con hora, patente, contenedor y funcionario asociados, y de ellos sale un indicador contractual con el concedente.

- **Posición y movimientos:** ventana de investigación de 48 horas, plazo en el que cada dotación de los tres turnos ha vuelto a estar de servicio al menos dos veces y la persona que originó el registro puede ser consultada.

- **Regla direccional:** cada divergencia se clasifica contra verificación física. Cuando el sistema nuevo resulta correcto, **no computa** contra el umbral y se registra como evidencia de mejora. Sin esta regla, la marcha blanca penalizaría a la solución por ser más exacta que el sistema al que reemplaza.

## Separación entre almacenamiento transaccional, temporal y analítico

**Estado: Completado**

### Obligación

El almacenamiento transaccional y el analítico estarán separados, y ninguna consulta analítica podrá degradar el desempeño de la operación (BTT, Cap. 5, RT-05.05 — separación transaccional y analítica). La capa analítica debe permitir filtrar y **profundizar desde el indicador agregado hasta la transacción de origen** (BTT, Cap. 5, RT-05.26 — tableros y trazabilidad hasta el origen), y el CLIENTE debe poder construir sus propios informes sin intervención del adjudicatario, con modelo semántico documentado (BTT, Cap. 5, RT-05.27 — autoservicio de explotación).

Este subdocumento separa **tres** almacenamientos y no dos: el transaccional, el temporal — series de telemetría y estados intermedios de conciliación — y el analítico. Subsumir el temporal dentro del analítico ocultaría precisamente la familia de datos que domina el volumen de este caso \[PROPUESTA TERABYTE\].

### Latencias exigidas a la capa de explotación

| **Dato disponible en la capa de explotación** | **Latencia máxima**                                  | **Origen**                                       |
|:--------------------------------------------------|:---------------------------------------------------------|:-----------------------------------------------------|
| Alarma de desconexión o desviación de temperatura | $\leq$ 5 minutos desde el evento físico                  | `CP`, Cap. 15, `RT-05.29`; `RNF-DES-04`              |
| Posición de un contenedor tras su movimiento      | $\leq$ 30 segundos                                       | `CP`, Cap. 15, `RT-05.29`; `RNF-DES-05`              |
| Estado del contenedor publicado en el portal      | $\leq$ 60 segundos                                       | `CP`, Cap. 15, `RT-09.01` y `RT-16.30`; `RNF-DES-06` |
| Productividad de grúa y estadía del camión        | tiempo real, granularidad por hora y por equipo          | `CP`, Cap. 15, `RT-05.29`                            |
| Indicadores comprometidos con el concedente       | $\leq$ 1 hora tras el cierre de turno                    | `CP`, Cap. 15, `RT-05.29`; `RNF-DES-07`              |
| Tableros operacionales accesibles al CLIENTE      | desfase $\leq$ 5 minutos, exportables en formato abierto | `RNF-OPE-02`                                         |

*Tabla. Latencias exigidas entre el evento operacional y su disponibilidad analítica.*

### Productos de explotación mínimos

Indicadores de gate y estadía; productividad por grúa, hora y equipo; posición e inventario; cadena de frío y alarmas; inspecciones; hechos, evidencias y objeciones; energía y emisiones por contenedor; e indicadores comprometidos con el concedente.

> **HECHO.** Los indicadores comprometidos con el concedente y los hechos facturables deben producirse desde eventos trazables y auditables, **no reconstruirse** después de ocurridos (CP, Cap. 10 — restricción no negociable N.<sup>o) 14</sup>. Esta es una restricción de modelo de datos antes que de reportería: obliga a que el evento se persista con su evidencia en el momento en que ocurre, y no a que un proceso posterior lo derive.

> **SUPUESTO.** Se asume que la analítica se alimenta por flujo desde los eventos operacionales y que el almacén analítico está separado del operacional (Célula 3 · maestro de contexto, §6, capa de datos y capa de integración · PROVISIONAL). Si Célula 3 resuelve la integración por réplica o captura de cambios sin capa de eventos, cambia el flujo de la operación hacia la analítica y deben recalcularse las latencias declaradas por indicador. Por eso este subdocumento compromete la *latencia por indicador* como requisito y no el mecanismo que la produce.

## Telemetría y frecuencia de muestreo

**Estado: Completado**

### Por qué la frecuencia es una decisión de diseño

El caso lo declara de forma expresa: la telemetría del patio refrigerado y del equipamiento móvil puede generar, según la frecuencia que se elija, un volumen de eventos **superior en órdenes de magnitud** al de las transacciones operacionales, y esa frecuencia es una decisión de diseño con consecuencias directas de costo, red y almacenamiento que debe justificarse (CP, Cap. 14.2 — particularidades del perfil de carga). El caso además la deja explícitamente sin resolver (CP, Cap. 16.1 — decisión pendiente N.<sup>o) 8</sup>.

### Universo instrumentado

Instrumentación de las 2.400 tomas de conexión refrigerada y de los 26 tableros de distribución; posicionamiento de equipos móviles; lectores de reconocimiento óptico en gate y accesos de patio; básculas de verificación de masa bruta; terminales montadas en equipos de patio; control de acceso y barreras; y el sistema de videovigilancia existente. La telemetría del sistema de control de las grúas de muelle solo como integración de solo lectura sujeta a autorización del fabricante (CP, Cap. 15, RT-17.06 — periféricos a integrar).

### Frecuencia de muestreo adoptada

Se adopta el modelo de dos capas ya decidido por Célula 2 (Célula 2 · Decisión N.<sup>o) 8</sup>: **muestreo local de 1 a 5 minutos**, agregación en el concentrador de patio y **reporte al núcleo de 5 a 15 minutos**, más envío inmediato ante excepción. El modelo satisface el plazo de alarma de 5 minutos porque la detección de la desviación ocurre en el borde y no espera al reporte periódico.

| **Magnitud**                    | **Cadencia**                             | **Justificación**                                                                               |
|:------------------------------------|:---------------------------------------------|:----------------------------------------------------------------------------------------------------|
| Temperatura de la carga refrigerada | 1–5 min local; 5–15 min al núcleo            | Decisión N..º 8 de Célula 2; permite alarmar en $\leq$ 5 min desde el borde                         |
| Estado de conexión de la toma       | por excepción, con señal de vida cada 15 min | el estado es discreto: reportar el cambio y no la constante                                         |
| Consumo eléctrico                   | misma cadencia que temperatura               | comparte el mismo dispositivo de borde                                                              |
| Posición de equipos móviles         | 1 reporte cada 2 s (valor de diseño)         | no fijado por ninguna decisión; supuesto declarado, a confirmar con el proveedor de posicionamiento |

*Tabla. Frecuencia de muestreo propuesta por magnitud.*

\> **Figura — Reefer y cadena de frío** · diagrama ‘D04_reefer_cadena_frio‘

*Nota. La muestra de temperatura tiene clave compuesta por conexión e instante y reside en el almacén temporal. El umbral de desviación no viene fijado por el caso y por eso se modela como parámetro versionado, nunca como constante del esquema.*

### Reglas de detección incorporadas por el corte del 5 de septiembre

- **Ausencia de dato.** La alarma se dispara a los tres intervalos de muestreo consecutivos *o* a los cinco minutos, **lo que ocurra primero** (Célula 2 · RF-REF-07, corregido en la tercera ronda). La condición corrige una redacción anterior insatisfacible: con muestreo de 5 minutos, tres intervalos no caben bajo el techo de 5 minutos. Un sensor caído es indistinguible de una desconexión, que es el modo de falla del evento del 18 de febrero.

- **Desviación de temperatura.** La regla de negocio define banda y duración mínima de la desviación, **sin fijar valores numéricos**, porque el caso no los entrega; y prohíbe toda parametrización cuya duración mínima haga inalcanzable el plazo de alarma de 5 minutos (Célula 2 · RN-11).

> **PROPUESTA DE TERABYTE.** Consecuencia para el modelo de datos: la banda y la duración de la desviación se modelan como **parámetros versionados con vigencia y responsable**, no como constantes del esquema. Cada alarma debe poder explicarse contra la parametrización vigente en el momento del evento, o la evidencia de cadena de frío no es defendible ante un tercero.

> **DUDA.** El universo instrumentable declarado por el caso son 74 equipos actuales — 18 grúas de patio, 42 tractocamiones y 14 equipos pesados — y hasta 88 proyectados, y **no incluye las seis grúas de muelle**. Ninguna célula ha declarado de qué evento se deriva el movimiento de muelle en el modelo de datos, sabiendo que el sistema de control de las grúas no se interviene. Es un vacío de modelo de datos y no solo de integración. Consulta dirigida a Célula 2 y Célula 3, registrada en el Anexo G.

## Integración e interoperabilidad de datos

**Estado: PendienteTres**

### Lo que ya está cerrado

El inventario de contrapartes está establecido y no se reabre: **21 contrapartes lógicas actuales** — 14 navieras, 3 autoridades, el operador ferroviario, el concedente, el sistema de operación de 2012 y el sistema de gestión empresarial — más **7 familias de periferia e instrumentación** — grúas, control de acceso y barreras, videovigilancia, básculas de verificación de masa bruta, reconocimiento óptico, tomas y concentradores refrigerados, y equipos móviles con su posicionamiento. Con 16 navieras proyectadas serán 23 contrapartes (Célula 2 · volumetría, matriz de integraciones).

| **Contraparte**                      | **Propietario del dato**                                             | **Volumen base declarado**                                                                          |
|:-----------------------------------------|:-------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------|
| Navieras (14)                            | cada naviera para planes e instrucciones; el terminal para la ejecución  | 620 recaladas/año; $\approx$ 972.000 registros de carga y descarga; $\approx$ 1.058.500 eventos de gate |
| Autoridades (3)                          | aduana, servicio agrícola y autoridad marítima o sanitaria según trámite | 18.400 inspecciones o casos al año                                                                      |
| Operador ferroviario                     | operador o terminal según evento                                         | $\approx$ 15 % del flujo terrestre; eventos exactos por levantar                                        |
| Concedente                               | el terminal produce; el concedente recibe                                | al menos un cierre por turno: $\approx$ 1.095 paquetes al año                                           |
| Sistema de operación 2012                | autoridad variable por dominio $\times$ zona $\times$ fase               | hasta $\approx$ 3.435.700 operaciones al año durante la coexistencia                                    |
| Sistema de gestión empresarial           | contabilidad en el sistema; hecho y evidencia en la solución             | $\approx$ 115.200 documentos al año                                                                     |
| Periferia e instrumentación (7 familias) | dispositivo o controlador y dominio operacional correspondiente          | volúmenes en las filas de telemetría, posición e imágenes; el resto por levantar                        |

*Tabla. Contrapartes de intercambio y volumen base declarado.*

### Obligaciones transversales que el modelo de datos debe soportar

Documentación de servicios síncronos en OpenAPI 3.1 y de flujos dirigidos por eventos en AsyncAPI 2.6 o superior, generada desde el código (BTT, Cap. 5, RT-05.16 — documentación de interfaces); versionado semántico con compatibilidad hacia atrás y preaviso de obsolescencia de seis meses (BTT, Cap. 5, RT-05.17 — versionado de contratos); **identificador de correlación común** que permita seguir una operación de negocio a través de todos los sistemas involucrados (BTT, Cap. 5, RT-05.19 — registro y correlación); capa anticorrupción frente a sistemas heredados o de terceros, de modo que un cambio externo no propague su modelo al núcleo (BTT, Cap. 5, RT-05.20 — aislamiento de sistemas heredados); y declaración, por integración, del modo, volumen, ventana de disponibilidad de la contraparte y comportamiento cuando no responde (BTT, Cap. 5, RT-05.21 — declaración por integración).

En cuanto a estándares sectoriales, el caso exige mensajería marítima estándar con, al menos, plano de estiba, orden de embarque, confirmación de descarga y de carga y notificación de movimiento de contenedor; norma internacional de codificación e identificación de contenedores; y estándares aplicables al intercambio con las autoridades aduanera y fitosanitaria, **identificando cada estándar por su denominación y acreditando la factibilidad de su adopción con las 14 navieras** (CP, Cap. 15, RT-05.23 — estándares sectoriales de intercambio). La correspondencia entre mensaje y evento ya está corregida: la confirmación de carga y descarga corresponde a los movimientos de nave y la notificación de movimiento al gate y la custodia; y no se presume un sobre de red por cada movimiento, porque el agrupamiento depende del contrato de cada naviera (Célula 2 · corrección de mensajería).

> **DUDA.** **Lo que falta y por qué no se completa aquí.** Los contratos, eventos, versiones, claves de idempotencia y el mecanismo de captura de cambios contra el sistema de 2012 figuran como “por detallar” y “por levantar” en el entregable de arquitectura de integración de Célula 3, y la decisión de arquitectura sobre el mecanismo de integración y eventos está en estado candidato (Célula 3 · arquitectura de integración y registro de decisiones · PROVISIONAL). Además, los contratos del sistema de 2012, la videovigilancia, las autoridades, el ferrocarril, la radio, las grúas y los periféricos permanecen como escalamiento abierto. No se inventa ninguna interfaz de programación, protocolo, versión ni disponibilidad de terceros: el vacío se declara y se acompaña de la consulta correspondiente en el Anexo G.

## Migración, saneamiento, validación y conciliación

**Estado: Completado**

### Alcance heredado que no se puede reducir

| **Universo**    | **Alcance a migrar**                                                     | **Conciliación y aceptación**                                             | **Remanente retenido**                |
|:--------------------|:-----------------------------------------------------------------------------|:------------------------------------------------------------------------------|:------------------------------------------|
| Inventario          | completo al corte, con posición verificada físicamente                       | recuento del 100 %, unicidad y barrido físico por bloque                      | no aplica                                 |
| Movimientos         | últimos 3 años                                                               | recuento por período y día, integridad de secuencia y muestra de recuperación | años 4 a 10 en repositorio consultable    |
| Hechos y evidencias | últimos 6 años                                                               | correspondencia 1:1, totales por período y recuperación dirigida              | repositorio hasta completar 6 años        |
| Maestros            | completos y vigentes, con el historial necesario para interpretar lo migrado | recuento, claves, relaciones y validación por dueño de dato                   | versión exportable documentada            |
| Tarifario           | versión vigente al corte                                                     | comparación del 100 % de reglas, vigencias y excepciones                      | versiones históricas ligadas a evidencias |
| Objeciones          | todas las abiertas, con expediente completo                                  | recuento del 100 %, estado, responsable y documentos                          | cerradas retenidas según plazo            |

*Tabla. Los seis universos de migración, su conciliación y el destino del remanente.*

El alcance proviene de (CP, Cap. 15, RT-05.15 — datos históricos a migrar) y su desarrollo por universo de (Célula 2 · Decisión N.<sup>o) 1, §15.1</sup>.

### El hueco de siete años

Hay una brecha deliberada entre lo que se retiene y lo que se migra: la retención de registros de operación y movimientos es de **10 años**, y la obligación de migrar cubre solo **3 años** de movimientos. Los siete años restantes deben seguir siendo recuperables y están fuera del alcance de migración. El documento transversal ya prescribe el destino: los datos históricos que no se migren quedarán accesibles en **un repositorio de consulta** durante el período de retención que fije el caso (BTT, Cap. 5, RT-05.15 — repositorio de consulta del histórico no migrado).

> **HECHO.** El sistema de operación de 2012 **no se conserva encendido como archivo histórico**. Conservarlo incumpliría la exigencia de que el CLIENTE pueda exportar la totalidad de su información en formatos abiertos y documentados, en cualquier momento del Contrato, sin costo adicional y sin intervención del adjudicatario (BTT, Cap. 5, RT-05.06 — exportación en formatos abiertos), puesto que su modelo de datos no está documentado por nadie. El apagado se ejecuta en el mes 22, un mes después de la aceptación final, y está condicionado a un acta de conformidad del repositorio histórico que acredite completitud contra los recuentos de origen, legibilidad en formato abierto y prueba de recuperación sobre una muestra dirigida (Célula 2 · Decisión N.<sup>o) 1, §15.1</sup>.

### Perfilado, ensayos y conciliación

La migración incluye una etapa previa de perfilado y saneamiento, con informe de los defectos detectados en los datos de origen y la decisión adoptada sobre cada uno (BTT, Cap. 5, RT-05.12 — perfilado y saneamiento previo). Se ejecutan **al menos dos ensayos completos** sobre el ambiente de preproducción antes de la migración definitiva, midiendo el tiempo total y el resultado de la conciliación (BTT, Cap. 5, RT-05.13 — ensayos de migración). La conciliación posterior es cuantitativa y verificable — recuentos, sumas de control y muestreo dirigido — y **toda diferencia debe quedar explicada** (BTT, Cap. 5, RT-05.14 — conciliación posterior a la migración). El plan completo declara alcance, origen, volumen, reglas de transformación, criterios de calidad, estrategia de ejecución y plan de reversión (BTT, Cap. 5, RT-05.11 — plan de migración).

> **SUPUESTO.** El esquema, la calidad y el tamaño reales de la base del sistema de 2012 son desconocidos: el CLIENTE declara no disponer de documentación actualizada de sus personalizaciones ni de su modelo de datos (CP, Cap. 5 — nota sobre el sistema de operación de 2012). La estimación de volumen histórico usada en el §5.13 es de orden de magnitud y está declarada como tal. La ausencia de ese dato no impide diseñar la estrategia: obliga a adelantar el perfilado del histórico al trabajo de descubrimiento de los meses 1 a 4 y a registrar la consulta formal correspondiente.

## Estrategia de desempeño de datos

**Estado: Completado**

### Método

La estrategia se deriva de las consultas y escrituras críticas de cada proceso, no de una lista genérica de buenas prácticas. Se inventarían las operaciones críticas, se declaran sus claves de búsqueda y patrones de acceso, y recién entonces se propone indexación, particionamiento y caché \[PROPUESTA TERABYTE\]. Se indexa por contenedor, tiempo, ubicación, actor, estado e identificador de correlación; se particiona por tiempo o dominio **solo cuando el volumen o el mantenimiento lo justifiquen**; y se usa caché **solo para lecturas tolerantes a desfase**, con política de invalidación y fuente de verdad declarada.

### Umbrales que la estrategia debe sostener

| **Operación**                                         | **Umbral**                                        | **Origen**                        |
|:----------------------------------------------------------|:------------------------------------------------------|:--------------------------------------|
| Confirmación de movimiento desde un equipo de patio       | $\leq$ 1 s (p95)                                      | `CP` Cap. 15 `RT-09.01`; `RNF-DES-03` |
| Consulta de posición de un contenedor                     | $\leq$ 1 s                                            | `CP` Cap. 15 `RT-09.01`; `RNF-DES-03` |
| Procesamiento completo de un camión en el gate            | $\leq$ 120 s                                          | `CP` Cap. 15 `RT-09.01`; `RNF-DES-01` |
| Reconocimiento automático del código de contenedor        | $\leq$ 3 s                                            | `CP` Cap. 15 `RT-09.01`; `RNF-DES-02` |
| Alarma del patio refrigerado                              | $\leq$ 5 min desde el evento físico                   | `CP` Cap. 15 `RT-05.29`; `RNF-DES-04` |
| Posición visible tras el movimiento                       | $\leq$ 30 s                                           | `CP` Cap. 15 `RT-05.29`; `RNF-DES-05` |
| Estado publicado en el portal                             | $\leq$ 60 s                                           | `CP` Cap. 15 `RT-09.01`; `RNF-DES-06` |
| Indicadores del concedente tras el cierre de turno        | $\leq$ 1 h                                            | `CP` Cap. 15 `RT-05.29`; `RNF-DES-07` |
| Interfaz de consulta simple / escritura transaccional     | $\leq$ 500 ms / $\leq$ 800 ms (p95)                   | `BTT` Cap. 9 num. 9.1; `RNF-DES-10`   |
| Portal, navegación, búsqueda compuesta e informe en línea | $\leq$ 2 s / $\leq$ 1 s / $\leq$ 3 s / $\leq$ 30 s    | `BTT` Cap. 9 num. 9.1; `RNF-DES-09`   |
| Procesamiento por lotes y carga de archivo de 100 MB      | $\geq$ 10.000 reg/min; $\leq$ 60 s                    | `BTT` Cap. 9 num. 9.1; `RNF-DES-11`   |
| Escenario de prueba obligatorio                           | carga a 1,5$\times$ el peak y estrés hasta saturación | `BTT` Cap. 9 `RT-09.06`; `RNF-DES-12` |
| Sincronización tras 72 h desconectado                     | $\leq$ 90 min, sin intervención manual                | `CP` Cap. 15 `RT-03.13`; `RNF-DIS-04` |
| Crecimiento admitido sin rediseño                         | $\geq$ 3$\times$ la volumetría inicial a 3 años       | `BTT` Cap. 9 `RT-09.03`; `RNF-DES-08` |

*Tabla. Umbrales de desempeño aplicables a la capa de datos.*

### Estrategia adoptada

La estrategia se deriva del catálogo de operaciones críticas y sus claves de acceso, no de una lista de técnicas. El Anexo (ver anx:desempeno) contiene las veintiuna operaciones con su volumen, su latencia, su técnica y su evidencia.

| **Técnica**  | **Regla adoptada**                                                                                                                                                                                                                                          |
|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Indexación       | Se indexa una clave de acceso declarada de una operación crítica, y nada más: **veintiún índices**, cuatro de ellos parciales sobre la fracción activa del universo. Un índice es un costo de escritura permanente sobre una ruta con un segundo de presupuesto |
| Particionamiento | Por tiempo, y solo cuando la entidad supera el orden de los cien millones de filas en su retención **y** su ciclo de vida exige eliminar o agregar por antigüedad. Cumplen las dos condiciones **cuatro entidades de ochenta**                                  |
| Caché            | Solo lectura tolerante a desfase, con desfase máximo declarado e invalidación por evento. **Nunca** se cachea un dato con estado de confianza, un dato bajo autoridad variable, un insumo de la condición de liberación ni una evidencia                        |
| Aislamiento      | La analítica opera sobre la réplica y nunca sobre el primario; el flujo crudo de posicionamiento se procesa en el borde y no se persiste                                                                                                                        |

*Tabla. Reglas de la estrategia de desempeño de datos.*

> **PROPUESTA DE TERABYTE.** **El argumento del particionamiento es la eliminación, no la consulta.** En una tabla particionada por tiempo, eliminar un período es descartar una partición; sin particionar es un borrado masivo sobre una tabla viva, en un terminal que no tiene ventana de detención total y que tiene prohibido intervenir entre el 15 de diciembre y el 30 de abril. La retención diferenciada que exige `RNF-CUM-14` no es ejecutable sin particionar esas cuatro entidades.

### Primer cuello de botella

(BTT, Cap. 9, RT-09.05 — identificación del cuello de botella) obliga a declarar cuál componente saturará primero al crecer la carga. Contrastado contra el crecimiento de tres veces la volumetría que exige (BTT, Cap. 9, RT-09.03 — crecimiento sin rediseño), el núcleo transaccional pasa de 0,23 a 0,7 transacciones por segundo y la ingesta al núcleo de 7,2 a 21,6 eventos por segundo: ambos absorbibles. **El que se estrecha es la ventana de sincronización posterior a la operación desconectada**, que pasa de exigir 19,3 Mbps sostenidos a exigir $\approx$ 58 Mbps, porque el plazo de 90 minutos es fijo por contrato y el volumen crece con la operación. Su componente dominante son las imágenes de reconocimiento: 11,2 de los 13 GB actuales.

> **DUDA.** La detección debe ser anticipada por una razón de calendario y no de ingeniería: la restricción no negociable N..º 9 prohíbe intervenir entre el 15 de diciembre y el 30 de abril, y el peak estacional cae precisamente ahí. Toda holgura debe estar instalada y verificada **antes del 15 de diciembre**; una alerta que se dispara en enero no se puede atender hasta mayo.

> **HECHO.** Las cuatro últimas filas de requerimientos no funcionales de desempeño — `RNF-DES-09` a `RNF-DES-12` — se incorporaron en el corte del 5 de septiembre de 2026 y trasladan al catálogo los umbrales del numeral 9.1 del documento transversal y la prueba de carga a 1,5 veces el peak declarado. Toda estrategia de índices, particiones y caché de este subdocumento se mide también contra ellos, no solo contra los umbrales del Capítulo 15 del caso.

### Primer cuello de botella

Las bases exigen identificar el componente que primero se convertirá en cuello de botella al crecer la carga, y explicar cómo se detectará y cómo se resolverá (BTT, Cap. 9, RT-09.05 — identificación del cuello de botella). Para la capa de datos de este caso, el candidato **no es la carga transaccional**: el régimen normal se estima en $\approx$ 0,11 transacciones de negocio por segundo y el peak de coincidencia en $\approx$ 0,23, frente a $\approx$ 37 eventos por segundo de posicionamiento de equipos y $\approx$ 36 eventos por segundo de telemetría reefer en el borde. El primer cuello de botella es la **ingesta de series temporales y su ventana de escritura**, y el mecanismo de crecimiento pasa por la agregación en el borde antes que por ampliar el núcleo \[PROPUESTA TERABYTE\].

> **DUDA.** Tres dependencias impiden cerrar la configuración final: las métricas reales del motor y su topología; la capacidad por nodo, réplicas y holgura; y la latencia de red y de borde. Todas corresponden a la arquitectura física de Célula 3. Existe además una dependencia cruzada con seguridad: el cifrado a nivel de campo exigido para datos personales, información comercial sensible y datos que permitan inferir el contenido de valor o la ruta de un contenedor (CP, Cap. 15, RT-11.10 — cifrado a nivel de campo) **restringe qué atributos pueden usarse como clave de búsqueda indexada**. Se requiere respuesta escrita de Célula 3 antes de comprometer índices sobre esos campos.

## Calidad de datos, auditoría y trazabilidad

**Estado: Completado**

### Por qué este apartado es una decisión propia

La obligación es explícita y estable, pero ninguna célula la ha desarrollado. El catálogo vigente de 91 requerimientos no funcionales de Célula 2 **no contiene ningún requerimiento de calidad de datos conforme a ISO/IEC 25012**, y Célula 3 la declara pendiente remitiéndola expresamente al cruce entre este subdocumento y el plan de pruebas. El vacío es de Célula 4 y se asume como tal \[PROPUESTA TERABYTE\].

### Obligaciones que deben satisfacerse

- Gestión de la calidad conforme a ISO/IEC 25012, con **validación en el punto de captura**, indicadores de completitud, exactitud y consistencia, y **tablero de calidad disponible para el CLIENTE** (BTT, Cap. 5, RT-05.04 — calidad de datos).

- Proceso de saneamiento de los datos migrados y diccionario entregable con linaje y propietario por dominio (BA, Art. 23 — datos, integración e interoperabilidad).

- Trazabilidad total de toda operación de negocio: reconstruir **quién, qué, cuándo, desde qué dispositivo y con qué valores anteriores y posteriores**, para cualquier registro y en cualquier momento del período de retención (BTT, Cap. 5, RT-05.03 — trazabilidad de operaciones).

- Catálogo de datos con linaje automatizado que permita rastrear el origen de cada indicador de negocio hasta su fuente (BTT, Cap. 5, RT-05.10 — catálogo y linaje). De carácter deseable en el documento transversal.

- Registro de auditoría **inalterable**, no modificable ni eliminable por ningún perfil, incluido el administrador de la plataforma (BTT, Cap. 16, RT-16.07 — registro de auditoría inalterable).

- Registro de las consultas a información sensible: información comercial de clientes, ubicación y contenido declarado de contenedores, y datos personales de trabajadores y conductores (CP, Cap. 15, RT-16.09 — registro de consultas a información sensible).

> **HECHO.** El caso califica expresamente la **consulta de la ubicación de un contenedor determinado** como información sensible desde el punto de vista de la seguridad de la carga. Esto convierte una consulta operacional rutinaria en un evento auditable, y es una restricción de diseño del modelo de datos, no una política administrativa.

### Dimensiones de calidad adoptadas

| **Dimensión** | **Regla en el punto de captura**                                                 | **Evidencia de control**                             |
|:------------------|:-------------------------------------------------------------------------------------|:---------------------------------------------------------|
| Completitud       | todo atributo obligatorio del diccionario debe estar presente al persistir el evento | tablero de calidad por dominio y por turno               |
| Exactitud         | la posición declarada conocida debe coincidir con la verificación física             | muestra de barrido físico por bloque rotativo, por turno |
| Consistencia      | las invariantes de dominio se validan en la transacción, no en un proceso posterior  | registro de rechazos con causa y responsable             |
| Oportunidad       | el dato llega a la capa de explotación dentro de la latencia del §5.6                | medición automática evento-a-tablero                     |
| Unicidad          | clave de idempotencia y ventana de deduplicación en toda escritura reintentable      | recuento de duplicados detectados y descartados          |
| Trazabilidad      | linaje desde el indicador publicado hasta la transacción y la evidencia de origen    | prueba de profundización sobre muestra dirigida          |

*Tabla. Dimensiones de ISO/IEC 25012 aplicadas, con su control y su evidencia.*

### Precisión sobre la norma

ISO/IEC 25012 define **quince características**, no seis, y la unicidad no es una de ellas: pertenece a otros marcos de gestión de datos. En la norma, lo que suele llamarse unicidad se expresa como consistencia y se implementa con clave de idempotencia, que es un control y no una dimensión. Se declara aquí porque una lista de dimensiones que no coincide con la norma contamina la credibilidad del resto del apartado.

De las quince características, **nueve se miden en este subdocumento** con regla, umbral, responsable y evidencia; las seis restantes se declaran y se remiten al apartado donde ya están resueltas: eficiencia al numeral 5.10, confidencialidad al 5.12, disponibilidad y recuperabilidad al 5.5, portabilidad al 5.12 y comprensibilidad al diccionario de datos. Esa remisión es deliberada: repetir aquí el 99,9 % de disponibilidad con otro número sería precisamente la incoherencia que la norma busca evitar.

### Alcance de la matriz de calidad

El Anexo (ver anx:calidad) contiene **cincuenta y cuatro reglas** de calidad con su umbral, su responsable de corrección y su evidencia, repartidas por los diez dominios; **doce indicadores** con fórmula, todos calculables sobre datos que el modelo ya persiste; y **doce pruebas** con criterio de aceptación que alimentan el plan de pruebas.

> **HECHO.** (BTT, Cap. 5, RT-05.04 — calidad de datos) no pide validar: pide validar **en el punto de captura**. La validación opera en cuatro niveles — estructural y de dominio en el borde, de integridad y de negocio en la transacción —, y durante las 72 horas sin enlace los cuatro siguen operando contra el estado local. Un evento que no supera la validación local **no se descarta**: se persiste en cola con su motivo de rechazo, porque perder un movimiento o un hecho facturable está prohibido.

> **PROPUESTA DE TERABYTE.** Regla autoimpuesta: no se menciona ISO/IEC 25012 ni ningún otro estándar sin un control asociado y su evidencia. Una mención sin métrica verificable se evalúa como incumplimiento, no como cumplimiento declarativo. El desarrollo completo de la matriz *dato $\rightarrow$ regla $\rightarrow$ umbral $\rightarrow$ responsable $\rightarrow$ evidencia* es trabajo pendiente de Célula 4 para la versión de cierre.

## Retención, archivo y eliminación segura

**Estado: Completado**

### Política por clase de información

| **Clase de información**                       | **Plazo y tratamiento al vencer**                                            | **Origen y evidencia mínima**                                                                                      |
|:---------------------------------------------------|:---------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------|
| Movimientos y registros de operación               | 10 años; eliminación controlada                                                  | `CP` Cap. 15 `RT-05.10`: régimen aduanero y vigencia de la concesión. Consulta y recuperación por contenedor y período |
| Series de temperatura reefer                       | 5 años; eliminación controlada                                                   | `CP` Cap. 15 `RT-05.10`; `RNF-CUM-08`. Continuidad de serie y recuperación de evidencia                                |
| Evidencia de hechos facturables                    | 6 años; eliminación controlada                                                   | `CP` Cap. 15 `RT-05.10`. Correspondencia 1:1 entre hecho y evidencia                                                   |
| Verificación de masa bruta                         | 5 años; eliminación controlada                                                   | `CP` Cap. 15 `RT-05.10`. Recuperación de pesaje, tolerancia y trazabilidad                                             |
| Imágenes de reconocimiento de contenedor y patente | 12 meses; eliminación o anonimización controlada                                 | `CP` Cap. 15 `RT-05.10`. Prueba de límite y registro de borrado                                                        |
| Registros de acceso de personas al recinto         | 5 años; eliminación controlada                                                   | `CP` Cap. 15 `RT-05.10`. Consulta por credencial, zona y tiempo                                                        |
| Telemetría de equipos                              | 2 años en línea; agregación histórica por plazo declarado y eliminación granular | `CP` Cap. 15 `RT-05.10`. Comparación granular contra agregado y registro de ciclo de vida                              |
| Eventos y registros de seguridad                   | 12 meses en línea + 24 meses en archivo recuperable                              | `BTT` Cap. 11 `RT-11.14`: registro centralizado e inalterable                                                          |

*Tabla. Política de retención diferenciada por clase de información.*

La política íntegra se materializa en `RNF-CUM-14` (Célula 2 · catálogo de requerimientos no funcionales), que además **prohíbe expresamente aplicar un plazo uniforme** a toda la información. La obligación matriz es declarar la política de retención, archivado y eliminación por cada dominio de datos e implementar un procedimiento verificable de eliminación segura (BTT, Cap. 5, RT-05.07 — retención, archivado y eliminación).

### Datos personales y residencia

Los datos personales se tratan con seudonimización o cifrado a nivel de campo para las categorías sensibles que el caso identifica (BTT, Cap. 5, RT-05.08 — tratamiento de datos personales). El caso extiende la exigencia de cifrado de campo a los datos personales de trabajadores propios, eventuales, conductores y visitantes; a la información comercial sensible de clientes, incluidas tarifas negociadas y volúmenes; y a los datos que permitan inferir el contenido de valor de un contenedor o su ruta (CP, Cap. 15, RT-11.10 — cifrado a nivel de campo). La residencia de datos debe declararse y quedar sujeta a aprobación del CLIENTE, y toda transferencia internacional de datos personales requiere base de licitud y resguardos conforme a la Ley N..º 21.719 (BA, Art. 23 — residencia de datos).

### Archivo y exportabilidad

El remanente retenido no migrado vive en un repositorio consultable en formato abierto y documentado, **fuera del núcleo nuevo y fuera del sistema de 2012**. La solución debe permitir exportar la totalidad de la información del CLIENTE en formatos abiertos y documentados, en cualquier momento del Contrato, sin costo adicional y sin intervención del adjudicatario (BTT, Cap. 5, RT-05.06 — exportación en formatos abiertos), obligación recogida en `RNF-POR-01` (Célula 2 · portabilidad).

> **DUDA.** Quedan por confirmar con Célula 3 tres materializaciones: el mecanismo de cifrado y la gestión de llaves y secretos; el almacenamiento inmutable de archivo y su respaldo; y la capacidad por clase de retención. Ninguna de las tres altera la política declarada aquí, pero todas condicionan su implementación y su costo.

## Volumetría actual, proyectada y de peak

**Estado: Completado**

### Base entregada por el CLIENTE

Los volúmenes operacionales son dato del CLIENTE y no estimación (CP, Cap. 14.1 — volumetría operacional entregada): 780.000 TEU y 486.000 contenedores anuales, con proyección a 920.000 TEU y 570.000 contenedores; 1.290.000 movimientos de patio con proyección a 1.480.000; 1.450 camiones diarios en promedio y hasta 2.600 en peak de temporada, con proyección a 1.700 y 3.100; 2.400 tomas de conexión refrigerada con proyección a 2.900 y $\approx$ 2.150 conectadas simultáneamente en peak; 26 tableros de distribución con proyección a 32; 74 equipos móviles a instrumentar con proyección a 88; 14 líneas navieras con proyección a 16; y 142 cámaras con proyección a 190.

### Volumetría de sistema derivada

Las dieciocho dimensiones del numeral 14.2 del caso deben completarse con valor, método de estimación y supuestos empleados; entregar celdas vacías, o valores sin derivación, se evalúa como dimensionamiento no realizado (CP, Cap. 14.2 — instrucción de dimensionamiento). Las cifras que sigue usando este subdocumento provienen de la plantilla de volumetría de Célula 2 y conservan su método declarado.

| **Dimensión relevante para la capa de datos**                 | **Actual**                                  | **Proyección 3 años** |
|:------------------------------------------------------------------|:------------------------------------------------|:--------------------------|
| Transacciones de negocio en régimen normal                        | $\approx$ 0,11 TPS                              | $\approx$ 0,13 TPS        |
| Transacciones en peak de coincidencia (dos naves y gate saturado) | $\approx$ 0,23 TPS                              | $\approx$ 0,27 TPS        |
| Telemetría reefer reportada al núcleo                             | $\approx$ 7,2 ev/s                              | $\approx$ 8,7 ev/s        |
| Telemetría reefer local, muestreo de 1 minuto                     | $\approx$ 35,8 ev/s                             | $\approx$ 43,3 ev/s       |
| Posicionamiento de equipos móviles                                | $\approx$ 37 ev/s                               | $\approx$ 44 ev/s         |
| Almacenamiento transaccional                                      | $\approx$ 20 GB/año                             | $\approx$ 24 GB/año       |
| Series temporales de carga refrigerada                            | $\approx$ 68 GB/año ($\approx$ 340 GB a 5 años) | $\approx$ 82 GB/año       |
| Imágenes de reconocimiento de contenedor y patente                | $\approx$ 1,4 TB/año                            | $\approx$ 1,6 TB/año      |
| Histórico a migrar desde el sistema de 2012                       | $\approx$ 480 GB (orden de magnitud)            | por confirmar             |
| Datos generados en 72 horas sin enlace                            | $\approx$ 13 GB                                 | $+$<!-- -->15 a 20 %      |
| Transferencia sostenida implicada por la sincronización           | $\approx$ 19,3 Mbps para cumplir los 90 min     | igual                     |

*Tabla. Volumetría de sistema relevante para el modelo y la gestión de datos.*

### Capacidad acumulada por horizonte de retención

El volumen anual no basta para dimensionar: (CP, Cap. 15, RT-05.10 — retención) fija plazos de hasta diez años y `RNF-CUM-14` prohíbe el plazo uniforme, de modo que la capacidad a aprovisionar es el acumulado sobre el horizonte de cada clase. El cálculo completo, con su método y sus cinco supuestos declarados, está en el Anexo (ver anx:capacidad).

| **Concepto**                                         | **Escenario actual** | **Escenario de diseño, 3$\times$** |
|:---------------------------------------------------------|:-------------------------|:---------------------------------------|
| Almacenamiento en línea                                  | 2,1 TB                   | 6,3 TB                                 |
| Almacenamiento en archivo recuperable                    | 1,5 TB                   | 3,6 TB                                 |
| **Total de dato**                                        | **3,6 TB**               | **9,9 TB**                             |
| Capacidad a aprovisionar, con copia adicional de objetos | 6,4 TB                   | **18,1 TB**                            |
| Del cual, transaccional en línea                         | 60 GB                    | 180 GB                                 |
| Del cual, imágenes de reconocimiento                     | 1,4 TB                   | 4,2 TB                                 |
| Capacidad mínima útil del borde                          | —                        | del orden de 1 TB                      |

*Tabla. Capacidad acumulada por escenario y modo de acceso.*

> **HECHO.** El orden de magnitud es el hallazgo: la solución completa, a diez años y crecida al triple, se dimensiona en **decenas de terabytes, no en centenas**. La capacidad no es el factor que decide el emplazamiento ni el costo dominante de infraestructura. Lo que decide es la latencia de un segundo, la autonomía de 72 horas y la ventana de sincronización. El motor que sostiene las 78 entidades relacionales y las veinte invariantes son **180 GB en línea** en el escenario de diseño, y cabe holgadamente en el nodo del borde.

### Frontera entre almacenamiento en línea y archivo

Movimientos y operación, 3 años en línea y años 4 a 10 en archivo; series de temperatura, 2 años granulares y años 3 a 5 agregados; evidencia facturable y verificación de masa bruta, 2 años en línea; imágenes de reconocimiento, sus 12 meses completos en línea; telemetría de equipos y eventos de seguridad, según los plazos que el caso ya fija. Archivo significa restauración dirigida en no más de 24 horas.

> **PROPUESTA DE TERABYTE.** La frontera no se inventa: **el caso ya la fijó dos veces**. Declara «2 años en línea» para la telemetría de equipos y «12 meses en línea más 24 en archivo» para los eventos de seguridad. Y los tres años de la operación tampoco son elección propia: (CP, Cap. 15, RT-05.15 — datos históricos a migrar) obliga a migrar tres años de movimientos y deja los años 4 a 10 en repositorio consultable. Se aplica el criterio que el caso ya usó.

### Factor estacional

La tercera particularidad del perfil de carga — el peak estacional del 15 de diciembre al 30 de abril, precisamente cuando está prohibido intervenir — se incorporó a la volumetría en el corte del 5 de septiembre de 2026. Los factores derivados del propio caso son: camiones atendidos por día, 2.600 sobre 1.450, es decir $\times$ 1,79; y volumen refrigerado mensual de enero a marzo, $\times$ 2,48 respecto del promedio anual uniforme.

> **HECHO.** La consecuencia del factor estacional no es solo de capacidad: es de **calendario**. La restricción no negociable prohíbe intervenir entre el 15 de diciembre y el 30 de abril, de modo que toda holgura de almacenamiento y toda ampliación de retención en línea deben estar instaladas y verificadas **antes del 15 de diciembre** de cada año. Una ampliación detectada como necesaria en enero no puede ejecutarse hasta mayo.

Los dos peaks son distintos y ambos deben dimensionarse por separado y en combinación justificada: el **peak de coincidencia** — dos naves en operación con el gate saturado, que puede ocurrir cualquier día — fija el techo instantáneo; el **peak estacional** fija la carga sostenida durante cuatro meses y medio y es el que determina el almacenamiento y la retención en línea.

> **SUPUESTO.** Ninguna de las cifras de la tabla anterior es un dato del CLIENTE: son estimaciones de Célula 2 con método declarado, que Célula 3 recibió explícitamente como “insumos, no dimensionamiento final” y que su frente de dimensionamiento debe revalidar antes de convertirlas en cantidades físicas (Célula 3 · dimensionamiento y Formulario T-11 · PROVISIONAL). Si esa revalidación las modifica, cambian el dimensionamiento de almacenamiento por familia del §5.4, la frontera entre retención en línea y archivo del §5.12 y la estrategia de particionamiento del §5.10. Se presentan como rango con método, y no se convierten en hechos confirmados por el CLIENTE.

## Modelo conceptual y diccionario inicial de datos

**Estado: Completado**

### Obligación

Entrega del modelo de datos documentado y de un diccionario de datos con el nombre, el tipo, el dominio de valores, la obligatoriedad, el propietario y la sensibilidad de cada atributo (BTT, Cap. 5, RT-05.01 — modelo y diccionario de datos), con entregable asociado al Sobre N..º 2. Las Bases Administrativas añaden que el modelo debe estar normalizado donde corresponda e incluir linaje y propietario por dominio (BA, Art. 23 — modelo de datos documentado).

### Alcance del diccionario inicial

El diccionario inicial cubre, como mínimo, las entidades del núcleo de registro — contenedor, visita, movimiento, posición y custodia —, del dominio refrigerado — toma, tablero, muestra, consigna y alarma —, del gate — camión, conductor, cita, documento y excepción —, de la evidencia facturable y del acceso e identidad. Cada atributo declara además su **clase de retención** y su **fuente de verdad**, campos que el documento transversal no exige explícitamente pero que este caso necesita por la coexistencia con el sistema de 2012 y por la retención diferenciada \[PROPUESTA TERABYTE\]. La estructura y una muestra representativa están en el Anexo A.

### Alcance entregado

El modelo conceptual se presenta en **catorce diagramas**, en el Anexo (ver sec:modelo-conceptual); el primero fija las convenciones de notación y debe leerse antes que los demás. El diccionario, en el Anexo (ver anx:diccionario), cubre **las ochenta entidades y sus 451 atributos**, cada uno con los seis campos que exige (BTT, Cap. 5, RT-05.01 — modelo y diccionario) más los dos campos propios.

| **Dominio**                              | **Entidades** | **Atributos** |
|:---------------------------------------------|:------------------|:------------------|
| DOM-OPS · Contenedor y operación             | 5                 | 40                |
| DOM-PAT · Patio y posición                   | 9                 | 48                |
| DOM-GAT · Gate y transporte                  | 11                | 57                |
| DOM-REF · Reefer y cadena de frío            | 7                 | 46                |
| DOM-NAV · Nave y planificación               | 10                | 52                |
| DOM-INS · Inspecciones                       | 6                 | 32                |
| DOM-FAC · Evidencia y facturación            | 7                 | 38                |
| DOM-ACC · Acceso e identidad                 | 10                | 46                |
| DOM-EMI · Energía y emisiones                | 4                 | 27                |
| DOM-INT · Integración, autoridad y auditoría | 11                | 65                |
| **Total**                                    | **80**            | **451**           |

*Tabla. Cobertura del modelo conceptual y del diccionario de datos.*

\> **Figura — Núcleo de registro: contenedor, visita, movimiento y posición** · diagrama ‘D02_nucleo_contenedor‘

*Nota. Este diagrama define las entidades de referencia del resto del modelo. La visita, y no el contenedor, es el objeto operacional central: el mismo contenedor físico vuelve al terminal muchas veces, y los días de almacenaje, la estadía y los hechos facturables se cuentan por estadía concreta.*

> **PROPUESTA DE TERABYTE.** El diccionario deriva además dos productos que no existían en ningún catálogo: el **catálogo de campos sujetos a cifrado a nivel de campo** —28 atributos en las tres familias que identifica (CP, Cap. 15, RT-11.10 — cifrado de campo), con lo que el compromiso de cobertura del 100 % de `RNF-SEG-05` pasa a ser verificable— y la lista de los **diez atributos derivados**, que no se capturan sino que se calculan y se auditan.

> **DUDA.** **Punto de coordinación que debe resolverse antes de la entrega.** El entregable de arquitectura lógica de Célula 3 incluye entre sus productos obligatorios un modelo conceptual de dominio y eventos, y el consolidado del Subdocumento 4 reserva una sección para el modelo conceptual del dominio. A la vez, el maestro de contexto de Célula 3 declara que **el Subdocumento 5 es propietario del modelo de datos detallado** y que el Subdocumento 4 debe proveer almacenamiento, flujo, seguridad, despliegue, capacidad y continuidad coherentes (Célula 3 · maestro de contexto, §16 · PROVISIONAL). Debe acordarse por escrito el corte propuesto: modelo conceptual de alto nivel en el Subdocumento 4 y modelo de datos con diccionario en el Subdocumento 5, **usando los mismos nombres de negocio en ambos**. Sin ese acuerdo habrá dos modelos contradictorios dentro del mismo Informe 1.

## Supuestos, dependencias y asuntos abiertos

Los siete supuestos de Célula 4 están en el Anexo E, los diez riesgos por dependencia de la entrega no cerrada de Célula 3 en el Anexo F, y las consultas formuladas a cada célula y al CLIENTE en el Anexo G. Los tres riesgos de mayor consecuencia sobre este subdocumento se enuncian aquí:

> **RIESGO R-DAT-01.** la entrega de Célula 3 no está cerrada y su catálogo lógico de componentes de datos se declara a sí mismo inicial y refinable los componentes de la capa de datos se fusionen o se renombren antes del cierre del Informe 1 la matriz de familias de persistencia, la separación de almacenamientos y el mapeo de entidades a almacenes deban rehacerse en los apartados 5.4, 5.6 y 5.14

> **RIESGO R-DAT-02.** el cifrado a nivel de campo exigido por el caso alcanza a datos que este subdocumento propone usar como clave de búsqueda indexada Célula 3 defina un mecanismo de cifrado que impida indexar esos atributos los umbrales de consulta de posición y de confirmación de movimiento de un segundo dejen de ser alcanzables con la estrategia de índices del apartado 5.10

> **RIESGO R-DAT-03.** tanto la arquitectura lógica del Subdocumento 4 como este subdocumento deben presentar un modelo conceptual del dominio, y el corte entre ambos no está acordado por escrito ambos equipos publiquen modelos con nombres de negocio distintos el Informe 1 presente dos modelos contradictorios y la incoherencia se evalúe como falta de integración entre subdocumentos


---

# Anexos

# Matriz de propiedad del dato y estructura del diccionario

## A.1 Propiedad del dato y fuente de verdad por dominio

La fuente de verdad se declara en tres momentos, porque la coexistencia con el sistema de operación de 2012 la desplaza: **actual** (antes del corte de la zona), **en coexistencia** (validación paralela) y **final** (después del corte aprobado). La regla operativa completa está en el numeral 5.3.

| **ID**                      | **Decisión asumida**                                                                                                                                              | **Documento de origen**                                                     | **Qué pasa si cambia**                                                             | **Apartados**    | **Mitigación de Célula 4**                                                                        |
|:--------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------|:---------------------|:------------------------------------------------------------------------------------------------------|
| **ID**                      | **Decisión asumida**                                                                                                                                              | **Documento de origen**                                                     | **Qué pasa si cambia**                                                             | **Apartados**    | **Mitigación de Célula 4**                                                                        |
| R-C3-01                         | La capa de datos se descompone en operacional, series, documental y analítica                                                                                         | Maestro de contexto de arquitectura, catálogo lógico inicial                    | Se rehacen la matriz de familias y el mapeo de cada entidad a su almacén               | 5.4, 5.6, 5.14       | Usar identificadores propios de dominio y mantener una tabla de equivalencia de una sola columna      |
| R-C3-02                         | La matriz de autoridad se publicará tal como la definió Célula 2                                                                                                      | Entregable de procesos críticos (matriz por completar)                          | Cambian la fuente de verdad en coexistencia y la conciliación de la migración          | 5.3, 5.4, 5.9        | Citar a Célula 2 como origen y a Célula 3 como confirmante; dejar zonas y fases parametrizadas        |
| R-C3-03                         | Habrá capa de eventos persistente como mecanismo de integración                                                                                                       | Maestro (capa de integración) y decisión de arquitectura en estado candidato    | Cambian el flujo hacia la analítica y la latencia declarada por indicador              | 5.6, 5.8, 5.10       | Comprometer la latencia por indicador como requisito, no el mecanismo; presentar ambas rutas          |
| R-C3-04                         | El emplazamiento será híbrido, con núcleo local para las cinco funciones críticas                                                                                     | Maestro y decisiones de arquitectura candidatas; destino de la sala aún abierto | Cambian consistencia, residencia, replicación y el análisis CAP por operación          | 5.4, 5.5, 5.10, 5.13 | Escribir el análisis CAP por operación y no por producto; tratar las 72 h como restricción de entrada |
| R-C3-05                         | El repositorio del histórico es independiente y consultable en formato abierto                                                                                        | Decisión de Célula 2 y maestro de Célula 3                                      | Si se conserva dentro del núcleo, cambian la política de archivo y el dimensionamiento | 5.9, 5.12, 5.13      | Anclar la exigencia a los requisitos del documento transversal, que no dependen de Célula 3           |
| R-C3-06                         | El cifrado de campo no restringirá la indexación de los atributos operacionales de búsqueda                                                                           | Paquete temprano de seguridad y decisión de llaves en estado candidato          | Si se cifran claves de búsqueda, caen los umbrales de un segundo                       | 5.10, 5.11, 5.12     | Declarar qué atributos son clave de acceso y exigir respuesta escrita antes de comprometer índices    |
| R-C3-07                         | Las dimensiones de volumetría de Célula 2 sobreviven la revalidación                                                                                                  | Frente de dimensionamiento (insumos, no dimensionamiento final)                 | Cambian el dimensionamiento por familia y la frontera entre línea y archivo            | 5.10, 5.12, 5.13     | Presentar la volumetría como rango con método; no convertir estimaciones en cifras del CLIENTE        |
| R-C3-08                         | Los objetivos de recuperación y la política de respaldo se mantienen                                                                                                  | Maestro (umbrales transversales) y catálogo de Célula 2                         | Un endurecimiento cambia replicación y capacidad, no la política de retención          | 5.5, 5.12            | Separar en el texto la política, que es propia, de su materialización, que es de Célula 3             |
| R-C3-09                         | El modelo conceptual del Subdocumento 4 y el de este subdocumento usarán los mismos nombres de negocio                                                                | Contrato del entregable de arquitectura lógica y maestro, §16                   | Dos modelos contradictorios dentro del mismo Informe 1                                 | 5.2, 5.14            | Acordar el corte por escrito antes de la entrega y fijar un glosario común de una página              |
| R-C3-10                         | Célula 3 alcanzará a integrar contenido aprobado antes de la entrega                                                                                                  | Consolidado del Subdocumento 4: nueve secciones pendientes de integrar          | Todo lo provisional de este subdocumento queda sin confirmante                         | 5.4, 5.6, 5.10, 5.13 | Redactar cada apartado provisional de modo que se sostenga con fuentes normativas propias             |
|                                 | **Pregunta concreta**                                                                                                                                             |                                                                                 |                                                                                        |                      |                                                                                                       |
| Matriz de autoridad             | ¿Cuáles son las zonas y fases nombradas de la matriz, y confirman que la fuente de verdad de la posición del contenedor es la definida por Célula 2, sin redefinirla? |                                                                                 |                                                                                        |                      |                                                                                                       |
| Identificadores lógicos         | ¿Los identificadores de contextos y de componentes de datos del maestro son definitivos o serán refinados? Se requiere congelar nombres de negocio comunes.           |                                                                                 |                                                                                        |                      |                                                                                                       |
| Propiedad del modelo conceptual | ¿Quién publica el modelo conceptual: la arquitectura lógica o este subdocumento? Se propone alto nivel en el Subdocumento 4 y modelo con diccionario en el 5.         |                                                                                 |                                                                                        |                      |                                                                                                       |
| Mecanismo de integración        | ¿Habrá capa de eventos persistente con cola de mensajes fallidos y reproceso, y captura de cambios contra el sistema de 2012?                                         |                                                                                 |                                                                                        |                      |                                                                                                       |
| Contratos por contraparte       | ¿Qué integraciones tendrán contrato confirmado antes de la entrega y cuáles quedan declaradas por levantar en el Informe 1?                                           |                                                                                 |                                                                                        |                      |                                                                                                       |
| Emplazamiento                   | ¿Qué almacenes quedan on-premise, cuáles en nube y cuáles en el borde? Sin esto no se cierran consistencia ni residencia de datos.                                    |                                                                                 |                                                                                        |                      |                                                                                                       |
| Motores y productos             | ¿Se nombrarán productos de base de datos en el Informe 1 o solo capacidades? Este subdocumento entrega la necesidad.                                                  |                                                                                 |                                                                                        |                      |                                                                                                       |
| Capacidad por nodo              | ¿Confirman las dieciocho dimensiones de volumetría con el factor estacional, o las recalcularán?                                                                      |                                                                                 |                                                                                        |                      |                                                                                                       |
| Cifrado y llaves                | ¿Qué atributos se cifran a nivel de campo y con qué mecanismo? Afecta directamente qué se puede indexar.                                                              |                                                                                 |                                                                                        |                      |                                                                                                       |
| Frontera del runtime local      | ¿Qué datos persisten localmente durante las 72 horas y cuál es el tamaño de buffer comprometido?                                                                      |                                                                                 |                                                                                        |                      |                                                                                                       |

*Tabla. Consultas dirigidas a Célula 3.*

## G.2 Consultas dirigidas a Célula 2

| **ID**  | **Exigencia T-7**                         | **Fuente normativa**                                                                        | **Evidencia de Célula 2**                              | **Decisión de datos**                                                 | **Estado**    |
|:------------|:----------------------------------------------|:------------------------------------------------------------------------------------------------|:-----------------------------------------------------------|:--------------------------------------------------------------------------|:------------------|
| **ID**  | **Exigencia T-7**                         | **Fuente normativa**                                                                        | **Evidencia de Célula 2**                              | **Decisión de datos**                                                 | **Estado**    |
| TRZ-DAT-001 | Dominio de información                        | CP Caps. 4 a 10 y 16; BTT Cap. 5 RT-05.01 y RT-05.09; BA Art. 23                                | Catálogos de requerimientos funcionales; reglas de negocio | Diez dominios con propietario y autoridad declarada                       | En curso          |
| TRZ-DAT-002 | Dominio de información                        | BA Art. 17.2 (única fuente de verdad)                                                           | Decisión N..º 1 §5.2; RF-CON-13 y RF-CON-14                | Autoridad por dominio, zona y fase, reutilizada sin redefinir             | En curso          |
| TRZ-DAT-003 | Motor y paradigma; CAP                        | BTT Cap. 5 RT-05.02; CP Cap. 15 RT-03.10 y RT-03.13                                             | RNF-DIS-02, 03, 04, 13, 14 y 15                            | Cinco familias con alternativas a comparar; CAP por operación             | Provisional       |
| TRZ-DAT-004 | Separación y explotación                      | BTT Cap. 5 RT-05.05 y RT-05.25 a RT-05.29; CP Cap. 15 RT-05.29                                  | RNF-DES-04 a 07; RNF-OPE-02                                | Tres almacenamientos separados; latencia comprometida por indicador       | Provisional       |
| TRZ-DAT-005 | Dominio de información (telemetría)           | CP Cap. 14.2 y Cap. 16.1; CP Cap. 15 RT-17.06 y RT-05.29                                        | Decisión N..º 8; RF-REF-07; RN-11                          | Muestreo de dos capas; parámetros de desviación versionados               | En curso          |
| TRZ-DAT-006 | Integración e interoperabilidad               | BTT Cap. 5 RT-05.16 a RT-05.23; CP Cap. 15 RT-05.23                                             | Volumetría: 21 contrapartes y 7 familias                   | Inventario cerrado; contratos declarados por levantar                     | Bloqueado externo |
| TRZ-DAT-007 | Migración y conciliación                      | BTT Cap. 5 RT-05.11 a RT-05.15; CP Cap. 15 RT-05.15                                             | Decisión N..º 1 §15.1 a §15.3                              | Seis universos; dos ensayos; repositorio del remanente                    | En curso          |
| TRZ-DAT-008 | Desempeño de datos                            | CP Cap. 15 RT-09.01 y RT-05.29; BTT Cap. 9 num. 9.1, RT-09.03, RT-09.05 y RT-09.06              | RNF-DES-01 a RNF-DES-12                                    | Índices por clave de acceso; cuello de botella en la ingesta de series    | Provisional       |
| TRZ-DAT-009 | Calidad, retención y eliminación              | BTT Cap. 5 RT-05.03, RT-05.04 y RT-05.10; BTT Cap. 16 RT-16.07; BA Art. 23; CP Cap. 15 RT-16.09 | Sin requerimiento de calidad en el catálogo vigente        | Seis dimensiones con control y evidencia; asumido por Célula 4            | Pendiente propio  |
| TRZ-DAT-010 | Calidad, retención y eliminación              | CP Cap. 15 RT-05.10 y RT-11.10; BTT Cap. 5 RT-05.06, RT-05.07 y RT-05.08; BTT Cap. 11 RT-11.14  | RNF-CUM-14; RNF-CUM-08; RNF-POR-01                         | Ocho clases con plazo, tratamiento y prueba                               | En curso          |
| TRZ-DAT-011 | Dominio de información (modelo y diccionario) | BTT Cap. 5 RT-05.01; BA Art. 23                                                                 | —                                                          | Diccionario con dos campos propios: clase de retención y fuente de verdad | Pendiente propio  |
|             | **Criterio**                              | **Peso**                                                                                    | **Obligación que lo origina**                          |                                                                           |                   |
| C1          | Garantías transaccionales e integridad        | 20 %                                                                                            | BTT Cap. 5 RT-05.02; invariante de escritor único          |                                                                           |                   |
| C2          | Autonomía de 72 horas y sincronización        | 20 %                                                                                            | Restricción no negociable N.º 4; CP Cap. 15 RT-03.10       |                                                                           |                   |
| C3          | Operabilidad con cinco personas               | 15 %                                                                                            | Restricción no negociable N.º 11                           |                                                                           |                   |
| C4          | Ajuste al perfil de carga                     | 15 %                                                                                            | Perfil asimétrico medido en la volumetría                  |                                                                           |                   |
| C5          | Retención y costo a diez años                 | 10 %                                                                                            | CP Cap. 15 RT-05.10; RNF-CUM-14                            |                                                                           |                   |
| C6          | Reversibilidad y bloqueo por proveedor        | 10 %                                                                                            | BTT Cap. 3 RT-03.07; BTT Cap. 5 RT-05.06                   |                                                                           |                   |
| C7          | Cifrado de campo, auditoría e inalterabilidad | 10 %                                                                                            | CP Cap. 15 RT-11.10; BTT Cap. 16 RT-16.07                  |                                                                           |                   |

*Tabla. Criterios de evaluación de las alternativas de persistencia.*

| **Familia**        | **Alternativas evaluadas y resultado**                                                                                    | **Elegida** |
|:-----------------------|:------------------------------------------------------------------------------------------------------------------------------|:----------------|
| Estado operacional     | relacional gestionado en nube (4,00); **relacional en el borde con réplica (4,30)**; documental no relacional (2,60)          | 4,30            |
| Series temporales      | **extensión temporal sobre el mismo relacional (4,70)**; motor de series dedicado (3,60)                                      | 4,70            |
| Documentos y evidencia | **almacenamiento de objetos con índice (5,00)**; gestor documental (2,50); binario dentro de la base (3,20)                   | 5,00            |
| Analítica              | **réplica de solo lectura (4,50)**; almacén analítico separado (3,50)                                                         | 4,50            |
| Histórico retenido     | **repositorio abierto sobre objetos (5,00)**; motor de archivo dedicado (4,00); conservar encendido el sistema de 2012 (2,30) | 5,00            |

*Tabla. Alternativas evaluadas por familia y puntaje ponderado.*

El paradigma documental se descarta con fundamento: el modelo tiene 78 entidades con integridad referencial declarada y veinte invariantes que cruzan entidades. Conservar encendido el sistema de 2012 como archivo se descarta por incumplimiento directo de (BTT, Cap. 5, RT-05.06 — exportación en formatos abiertos), porque el CLIENTE no podría ejercer por sí mismo su derecho de exportación sobre un modelo de datos que nadie documentó.

# Transaccionalidad, consistencia y disponibilidad

## Las seis particiones reales del caso

| **ID** | **Partición**                               | **Origen y duración exigible**                                     |
|:-----------|:------------------------------------------------|:-----------------------------------------------------------------------|
| PAR-1      | Terminal contra exterior                        | Restricción N.º 4; CP Cap. 15 RT-03.10 — 72 horas continuas            |
| PAR-2      | Solución contra el sistema de operación de 2012 | RF-CON-13 y 14; Decisión N.º 1 — mientras dure la convivencia por zona |
| PAR-3      | Equipo de patio fuera de cobertura inalámbrica  | CP Cap. 15 RT-03.10 — 8 horas sin pérdida de registro                  |
| PAR-4      | Concentrador refrigerado contra el núcleo       | Decisión N.º 8; RF-REF-07 — se detecta por ausencia de dato            |
| PAR-5      | Contraparte externa que no responde             | BTT Cap. 5 RT-05.21; BTT Cap. 10 RT-10.08                              |
| PAR-6      | Primario operacional contra réplica analítica   | Familia analítica; transitoria                                         |

*Tabla. Particiones de red documentadas del Caso 06.*

## Unidades transaccionales

| **ID** | **Unidad**               | **Invariante que la exige**                                                     |
|:-----------|:-----------------------------|:------------------------------------------------------------------------------------|
| UT-01      | Movimiento y posición        | No existe movimiento confirmado sin posición actualizada con su estado de confianza |
| UT-02      | Transferencia de autoridad   | Un fallo parcial deja la autoridad en el origen, nunca en ambos ni en ninguno       |
| UT-03      | Turno de camión              | La estadía derivada no se calcula sobre eventos a medias                            |
| UT-04      | Hecho facturable y evidencia | No existe hecho sin evidencia; la evidencia es inmutable desde su creación          |
| UT-05      | Alarma y su parametrización  | La alarma debe explicarse contra el parámetro con que se evaluó                     |
| UT-06      | Acta, retención y liberación | Una retención vigente impide la liberación en el mismo instante                     |
| UT-07      | Credencial y sus zonas       | No existe credencial sin zonas ni sin expiración                                    |
| UT-08      | Muestra de temperatura       | Anexado puro: no participa de ninguna transacción multi-entidad                     |

*Tabla. Unidades transaccionales del modelo.*

## Funciones no disponibles en modo desconectado

Declaración exigida por (BTT, Cap. 3, RT-03.13 — funciones no disponibles), cuya ausencia se evalúa como observación grave.

| **Función no disponible**         | **Procedimiento manual que la suple**                                                   | **Al reconectar**                            |
|:--------------------------------------|:--------------------------------------------------------------------------------------------|:-------------------------------------------------|
| Mensajería con navieras               | Canales de contingencia acordados por naviera, con registro del acuerdo en el sistema local | La cola se procesa en orden, con deduplicación   |
| Portal de clientes                    | Atención por la mesa de ayuda, que registra la consulta como evento local                   | El portal recupera el estado del núcleo          |
| Emisión de documento tributario       | Ninguno: el hecho facturable sí se registra con su evidencia; solo se difiere la emisión    | Entrega y conciliación 1:1                       |
| Interfaz con autoridades              | Canal asistido trazable: acta en papel firmada por el inspector presente                    | Se transmite el acta y su evidencia              |
| Notificación externa a transportistas | Aviso por radio y megafonía; la instrucción se entrega en el puesto de gate                 | Se envían con su instante original               |
| Reporte al concedente                 | Ninguno: los indicadores se consolidan al cierre de cada turno y se acumulan                | Entrega de los paquetes sin reconstrucción       |
| Tableros de gestión y autoservicio    | Consultas operacionales acotadas sobre el núcleo local                                      | La réplica se pone al día; el desfase se declara |
| Acceso autoservido del portal         | Habilitación manual por la mesa de ayuda                                                    | Se sincronizan las credenciales creadas          |
| Verificación de habilitación externa  | Última copia local vigente, con marca de verificación diferida                              | Revalidación; toda discrepancia genera evento    |

*Tabla. Funciones no disponibles sin enlace y su procedimiento de reemplazo.*

**Orden de la reconciliación.** Primero las transferencias de autoridad pendientes, porque determinan qué registros son autoritativos; después los movimientos y las posiciones; después los hechos facturables y su evidencia; después las series de telemetría; y al final las imágenes, que son el 94 % del volumen y no bloquean ninguna invariante.

\> **Figura — Integración, autoridad del dato y auditoría** · diagrama ‘D08_integracion_autoridad‘

*Nota. La terna dominio, zona y fase es única en cada instante. Sin esa restricción el modelo admitiría dos sistemas autoritativos simultáneos sobre el mismo dato, que es exactamente el riesgo que este diagrama existe para conjurar.*

# Estrategia de desempeño de datos

## Índices comprometidos

Se indexa una clave de acceso declarada de una operación crítica, y nada más. Cuatro de los veintiún índices son parciales: cubren solo la fracción activa del universo — posiciones dudosas, alarmas abiertas y hechos objetados —, lo que evita pagar el costo de escritura sobre el histórico para servir consultas que solo miran lo vigente.

| **Entidad**                   | **Clave de acceso**                                             | **Operación que lo exige**                               |
|:----------------------------------|:--------------------------------------------------------------------|:-------------------------------------------------------------|
| VISITA                            | código de contenedor + estado abierto                               | consulta de posición y de estado                             |
| POSICION_VIGENTE                  | id de visita; id de celda; estado de confianza (parcial)            | consulta de posición; ocupación de celda; tablero de calidad |
| MOVIMIENTO                        | id de visita + instante; id de equipo + instante; id de correlación | historial; atribución de consumo; trazabilidad               |
| TURNO_CAMION y CITA               | patente + arribo; franja + estado                                   | identificación en barrera; disponibilidad de cupo            |
| EVENTO_GATE                       | id de turno + tipo                                                  | cálculo derivado de la estadía                               |
| MUESTRA_TEMPERATURA               | id de conexión + instante                                           | curva de temperatura por contenedor                          |
| CONEXION_REEFER y ALARMA          | toma + desconexión nula; estado + generación (parcial)              | conexiones vigentes; consola de alarmas                      |
| HECHO_FACTURABLE y EVIDENCIA      | visita + tipo; estado (parcial); id de hecho                        | conciliación; objeciones; recuperación de evidencia          |
| LECTURA_OPTICA y EVENTO_ACCESO    | código leído + instante; zona + instante                            | conciliación de lectura; conteo por zona                     |
| MENSAJE y TRANSFERENCIA_AUTORIDAD | clave de idempotencia; visita + secuencia                           | deduplicación; orden de la cascada de resolución             |
| REGISTRO_AUDITORIA                | entidad + objeto + instante                                         | reconstrucción exigida por RT-05.03                          |

*Tabla. Índices comprometidos y la operación que los exige.*

> **DUDA.** Ocho de estas claves de acceso son atributos del catálogo de cifrado a nivel de campo. Un cifrado que impida la búsqueda por igualdad sobre ellos hace inalcanzables los umbrales de un segundo. No se resuelve aquí porque el mecanismo de cifrado es arquitectura de seguridad: queda dirigido a Célula 3, acotado a ocho atributos nombrados en vez de a una pregunta general.

## Entidades particionadas

| **Entidad**     | **Filas en su retención**     | **Ciclo de vida que lo exige**                          |
|:--------------------|:----------------------------------|:------------------------------------------------------------|
| MUESTRA_TEMPERATURA | $\approx$ 1.130 millones a 5 años | retención de 5 años con agregación de la resolución a los 2 |
| MOVIMIENTO          | $\approx$ 22,6 millones a 10 años | 10 años con eliminación controlada                          |
| EVENTO_ACCESO       | según dotación, a 5 años          | 5 años                                                      |
| REGISTRO_AUDITORIA  | crece con toda operación          | hereda el plazo de la clase auditada                        |

*Tabla. Las cuatro entidades particionadas, de ochenta.*

## Degradación controlada

| **Recurso saturado**  | **Comportamiento**                                                                  | **Qué nunca ocurre**                                   |
|:--------------------------|:----------------------------------------------------------------------------------------|:-----------------------------------------------------------|
| Ingesta de series         | Reduce la resolución reportada dentro del rango decidido y conserva la resolución local | No se descarta una muestra sin marcarla como ausente       |
| Escritura transaccional   | Encolamiento con acuse al equipo y reintento idempotente                                | No se pierde un movimiento ni se confirma sin persistir    |
| Consulta analítica        | Limitación de tasa sobre la réplica, con mensaje explícito                              | La analítica nunca se desvía al primario                   |
| Almacenamiento de objetos | Buffer local en el borde con alerta de ocupación                                        | No se descarta una imagen que respalda un hecho facturable |
| Enlace de reposición      | La reconciliación sigue su orden declarado                                              | Las invariantes no esperan a las imágenes                  |

*Tabla. Degradación controlada de la capa de datos.*

# Matriz de calidad conforme a ISO/IEC 25012

Cincuenta y cuatro reglas con umbral, responsable y evidencia; doce indicadores con fórmula; doce pruebas con criterio de aceptación. Se reproduce aquí el marco y los indicadores; el detalle regla a regla acompaña el documento de trabajo de Célula 4.

| **Característica**           | **Tratamiento**          | **Dónde**                                                                    |
|:---------------------------------|:-----------------------------|:---------------------------------------------------------------------------------|
| Exactitud                        | se mide aquí                 | contra verificación física en patio y contra el hecho real en gate y facturación |
| Completitud                      | se mide aquí                 | atributos obligatorios del diccionario presentes al persistir                    |
| Consistencia                     | se mide aquí                 | invariantes del modelo y ausencia de representaciones contradictorias            |
| Credibilidad                     | se mide aquí                 | fuente de registro declarada por movimiento                                      |
| Actualidad                       | se mide aquí                 | latencia entre el evento físico y su disponibilidad                              |
| Accesibilidad                    | se mide aquí                 | recuperación dirigida dentro del plazo de cada clase                             |
| Conformidad                      | se mide aquí                 | estándares de codificación, mensajería y metodología de emisiones                |
| Precisión                        | se mide aquí                 | resolución declarada por magnitud                                                |
| Trazabilidad                     | se mide aquí                 | linaje desde el indicador hasta la transacción y la evidencia                    |
| Confidencialidad                 | se implementa en 5.12        | cifrado de campo y registro de consultas sensibles                               |
| Eficiencia                       | se hereda de 5.10            | índices, particiones y caché frente a los umbrales                               |
| Comprensibilidad                 | se cumple con el diccionario | nombre de negocio, dominio y propietario por atributo                            |
| Disponibilidad y recuperabilidad | se heredan de 5.5            | 99,9 %, 72 h, RTO y RPO                                                          |
| Portabilidad                     | se hereda de 5.12            | exportación total en formatos abiertos                                           |

*Tabla. Las quince características de ISO/IEC 25012 y su tratamiento.*

| **ID** | **Indicador**                       | **Fórmula**                                              |
|:-----------|:----------------------------------------|:-------------------------------------------------------------|
| IND-01     | Completitud del inventario              | visitas con estado de confianza ÷ visitas en patio           |
| IND-02     | Exactitud de la posición                | posiciones por verificar no resueltas al cierre ÷ inventario |
| IND-03     | Credibilidad del registro de movimiento | movimientos por vía manual ÷ movimientos totales             |
| IND-04     | Diferencias no explicadas de gate       | divergencias no explicadas al cierre del día                 |
| IND-05     | Anticipación documental                 | turnos con documentación validada antes del arribo ÷ turnos  |
| IND-06     | Continuidad de la cadena de frío        | conexiones con serie continua ÷ conexiones activas           |
| IND-07     | Oportunidad de la alarma refrigerada    | alarmas en $\leq$ 5 min ÷ alarmas                            |
| IND-08     | Respaldo del hecho facturable           | hechos con evidencia recuperable ÷ hechos                    |
| IND-09     | Reproducibilidad de la valorización     | hechos con versión de regla ÷ hechos                         |
| IND-10     | Cobertura de emisiones                  | contenedores con emisión ÷ contenedores movilizados          |
| IND-11     | Integridad de la auditoría              | operaciones auditadas ÷ operaciones ejecutadas               |
| IND-12     | Consistencia de la autoridad del dato   | solapamientos de autoridad detectados                        |

*Tabla. Indicadores del tablero de calidad disponible para el CLIENTE.*

# Capacidad acumulada por familia y horizonte

| **Modo** | **Concepto**                       | **Actual** | **Diseño 3$\times$** |
|:-------------|:---------------------------------------|:---------------|:-------------------------|
| En línea     | Transaccional, 3 años                  | 60 GB          | 180 GB                   |
| En línea     | Series granulares, 2 años              | 136 GB         | 408 GB                   |
| En línea     | Series agregadas, años 3 a 5           | 68 GB          | 204 GB                   |
| En línea     | Imágenes de reconocimiento, 12 meses   | 1.400 GB       | 4.200 GB                 |
| En línea     | Evidencia documental, 2 años           | 446 GB         | 1.338 GB                 |
|              | **Subtotal en línea**                  | **2,1 TB**     | **6,3 TB**               |
| Archivo      | Transaccional, años 4 a 10             | 140 GB         | 420 GB                   |
| Archivo      | Evidencia documental, años 3 a 6       | 892 GB         | 2.676 GB                 |
| Archivo      | Histórico retenido del sistema de 2012 | 480 GB         | 480 GB                   |
|              | **Subtotal archivo**                   | **1,5 TB**     | **3,6 TB**               |
|              | **Total de dato**                      | **3,6 TB**     | **9,9 TB**               |
|              | **Capacidad a aprovisionar**           | **6,4 TB**     | **18,1 TB**              |

*Tabla. Capacidad acumulada por modo de acceso y escenario de crecimiento.*

**Reglas de cálculo declaradas.** Unidades decimales. Las cifras anuales de la volumetría ya incluyen su factor de sobrecarga —$\times$<!-- -->3 en transaccional y series, $\times$<!-- -->1,2 en imágenes— y **no se vuelve a aplicar**: el doble conteo es el error más común de este cálculo. El factor de las imágenes cubre metadatos y no copias, de modo que la copia adicional se calcula aparte. El factor estacional afecta el caudal y no el acumulado anual, salvo en el buffer de 72 horas, que se dimensiona para el peor caso.

| **Buffer de la operación desconectada**            | **Actual** | **Diseño 3$\times$** |
|:-------------------------------------------------------|:---------------|:-------------------------|
| Volumen generado en 72 horas                           | 13 GB          | 39 GB                    |
| Del cual, imágenes                                     | 11,2 GB        | 33,6 GB                  |
| Transferencia sostenida para sincronizar en 90 minutos | 19,3 Mbps      | 57,8 Mbps                |

*Tabla. Buffer de 72 horas y transferencia de reposición implicada.*



---

# Diccionario de datos

Las ochenta entidades del modelo conceptual con sus 451 atributos. Cada atributo declara los seis campos que exige (BTT, Cap. 5, RT-05.01 — modelo y diccionario de datos) y los dos campos propios de `DEC-C4-04`: la clase de retencion y la fuente de verdad, que se declaran a nivel de entidad por ser propiedad del objeto y no de cada campo.

*Nota. La obligatoriedad toma tres valores: *obligatorio* cuando el atributo integra la clave primaria o su ausencia impide persistir el hecho; *condicional* cuando el modelo declara una condicion de nulidad; y *derivado* cuando el atributo se calcula y se audita en vez de capturarse.*

## Contenedor, operacion, patio y posicion

### `CONTENEDOR`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                                       | **Obligat.** | **Origen y nota**                |
|:---------------------|:-------------|:--------------|:---------------------------------------------------------------------------------|:-----------------|:-------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                                       | **Obligat.** | **Origen y nota**                |
| `codigo_iso6346`     | string       | PK            | Codigo ISO 6346: cuatro letras de propietario, seis digitos y digito verificador | Obligatorio      | identificador normalizado, RF-INT-08 |
| `tipo`               | enum         | —             | {dry, reefer, tanque, open top}                                                  | Obligatorio      | dry, reefer, tanque, open top        |
| `tamano`             | enum         | —             | {20 pies, 40 pies}                                                               | Obligatorio      | 20 pies, 40 pies                     |
| `tara`               | decimal      | —             | kg                                                                               | Obligatorio      | kg                                   |
| `clase_imdg`         | enum         | —             | {clases 1 a 9 del Codigo IMDG}                                                   | Condicional      | nulo si no es carga peligrosa, RN-02 |
| `requiere_frio`      | boolean      | —             | {verdadero, falso}                                                               | Obligatorio      | —                                    |
| `dimension_especial` | boolean      | —             | {verdadero, falso}                                                               | Obligatorio      | —                                    |
| `id_naviera`         | string       | FK            | Identificador de la entidad referenciada                                         | Obligatorio      | ref. D-05.NAVIERA                    |

### `VISITA`

| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**                                                                                                  | **Obligat.** | **Origen y nota**                        |
|:-------------------|:-------------|:--------------|:----------------------------------------------------------------------------------------------------------------------------|:-----------------|:---------------------------------------------|
| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**                                                                                                  | **Obligat.** | **Origen y nota**                        |
| `id_visita`        | string       | PK            | Identificador unico                                                                                                         | Obligatorio      | —                                            |
| `codigo_iso6346`   | string       | FK            | Identificador de la entidad referenciada                                                                                    | Obligatorio      | —                                            |
| `flujo`            | enum         | —             | {importacion, exportacion, transbordo}                                                                                      | Obligatorio      | importacion, exportacion, transbordo         |
| `instante_ingreso` | timestamptz  | —             | Instante con zona horaria                                                                                                   | Obligatorio      | —                                            |
| `instante_salida`  | timestamptz  | —             | Instante con zona horaria                                                                                                   | Condicional      | nulo mientras la visita esta abierta         |
| `estado_visita`    | enum         | —             | {anunciada, descargada, ingresada, posicionada, removida, en inspeccion, retenida, liberable, embarcada, retirada, anulada} | Obligatorio      | ciclo de vida en D-09                        |
| `id_recalada`      | string       | FK            | Identificador de la entidad referenciada                                                                                    | Condicional      | ref. D-05.RECALADA, nulo hasta la asignacion |
| `id_cliente`       | string       | FK            | Identificador de la entidad referenciada                                                                                    | Obligatorio      | ref. D-06.CLIENTE                            |

### `MOVIMIENTO`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
|:------------------|:-------------|:--------------|:----------------------------------------------------------|:-----------------|:--------------------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
| `id_movimiento`   | string       | PK            | Identificador unico                                       | Obligatorio      | —                                                       |
| `id_visita`       | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | —                                                       |
| `tipo`            | enum         | —             | {descarga, carga, remocion, reubicacion, ingreso, salida} | Obligatorio      | descarga, carga, remocion, reubicacion, ingreso, salida |
| `instante`        | timestamptz  | —             | Instante con zona horaria                                 | Obligatorio      | instante real del hecho, no de digitacion               |
| `id_equipo`       | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | —                                                       |
| `celda_origen`    | string       | FK            | Identificador de la entidad referenciada                  | Condicional      | nulo en ingreso                                         |
| `celda_destino`   | string       | FK            | Identificador de la entidad referenciada                  | Condicional      | nulo en salida                                          |
| `fuente_registro` | enum         | —             | {telemetria, optica, manual excepcional}                  | Obligatorio      | telemetria, optica, manual excepcional                  |
| `id_correlacion`  | string       | —             | Identificador de correlacion comun de extremo a extremo   | Obligatorio      | RT-05.19                                                |
| `id_recalada`     | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | ref. D-05.RECALADA, solo carga y descarga               |

### `POSICION_VIGENTE`

| **Atributo**               | **Tipo** | **Clave** | **Dominio de valores**                  | **Obligat.** | **Origen y nota**                     |
|:-------------------------------|:-------------|:--------------|:--------------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**               | **Tipo** | **Clave** | **Dominio de valores**                  | **Obligat.** | **Origen y nota**                     |
| `id_visita`                    | string       | PK,FK         | Identificador de la entidad referenciada    | Obligatorio      | —                                         |
| `id_celda`                     | string       | FK            | Identificador de la entidad referenciada    | Obligatorio      | —                                         |
| `vigente_desde`                | timestamptz  | —             | Instante con zona horaria                   | Obligatorio      | —                                         |
| `estado_confianza`             | enum         | —             | {conocida, por verificar (D-10), RF-PAT-03} | Obligatorio      | conocida, por verificar (D-10), RF-PAT-03 |
| `instante_ultima_verificacion` | timestamptz  | —             | Instante con zona horaria                   | Obligatorio      | —                                         |

### `ASIGNACION_POSICION`

| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                   |
|:--------------------------|:-------------|:--------------|:----------------------------------------------------------------|:-----------------|:----------------------------------------|
| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                   |
| `id_asignacion`           | string       | PK            | Identificador unico                                             | Obligatorio      | —                                       |
| `id_visita`               | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                       |
| `celda_propuesta`         | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                       |
| `nivel_rn01_determinante` | int          | —             | 1 a 4                                                           | Obligatorio      | 1 a 4, RN-01                            |
| `restriccion_cedida`      | string       | —             | Texto acotado                                                   | Condicional      | declarada solo cuando hay conflicto     |
| `motivo`                  | string       | —             | Explicacion de la asignacion, ligada al nivel de RN-01 aplicado | Obligatorio      | —                                       |
| `instante`                | timestamptz  | —             | Instante con zona horaria                                       | Obligatorio      | —                                       |
| `version_algoritmo`       | string       | —             | Version semantica del algoritmo de asignacion                   | Obligatorio      | obligatoria para reproducir la decision |

### `CONDICION_DINAMICA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                           | **Obligat.** | **Origen y nota**                             |
|:-----------------|:-------------|:--------------|:-----------------------------------------------------|:-----------------|:--------------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                           | **Obligat.** | **Origen y nota**                             |
| `id_condicion`   | string       | PK            | Identificador unico                                  | Obligatorio      | —                                                 |
| `tipo`           | enum         | —             | {equipo no disponible, bloque restringido, cliente}  | Obligatorio      | equipo no disponible, bloque restringido, cliente |
| `alcance`        | string       | —             | Bloque, zona o equipo sobre el que rige la condicion | Obligatorio      | —                                                 |
| `id_autor`       | string       | FK            | Identificador de la entidad referenciada             | Obligatorio      | ref. D-07.PERSONA                                 |
| `motivo`         | string       | —             | Motivo declarado por quien crea la condicion         | Obligatorio      | —                                                 |
| `vigencia_desde` | timestamptz  | —             | Instante con zona horaria                            | Obligatorio      | —                                                 |
| `vigencia_hasta` | timestamptz  | —             | Instante con zona horaria                            | Obligatorio      | —                                                 |

### `TAREA_VERIFICACION`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                            | **Obligat.** | **Origen y nota**      |
|:---------------------|:-------------|:--------------|:------------------------------------------------------|:-----------------|:---------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                            | **Obligat.** | **Origen y nota**      |
| `id_tarea`           | string       | PK            | Identificador unico                                   | Obligatorio      | —                          |
| `id_visita`          | string       | FK            | Identificador de la entidad referenciada              | Obligatorio      | —                          |
| `posicion_candidata` | string       | —             | Identificador de celda donde se presume el contenedor | Obligatorio      | —                          |
| `id_asignado_a`      | string       | FK            | Identificador de la entidad referenciada              | Obligatorio      | ref. D-07.PERSONA          |
| `estado`             | enum         | —             | {abierta, en curso, cerrada}                          | Obligatorio      | abierta, en curso, cerrada |
| `instante_creacion`  | timestamptz  | —             | Instante con zona horaria                             | Obligatorio      | —                          |
| `instante_cierre`    | timestamptz  | —             | Instante con zona horaria                             | Obligatorio      | —                          |

### `CUSTODIA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                        |
|:-----------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:---------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                        |
| `id_custodia`    | string       | PK            | Identificador unico                      | Obligatorio      | —                                            |
| `id_visita`      | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                            |
| `responsable`    | enum         | —             | {terminal, transportista, naviera}       | Obligatorio      | terminal, transportista, naviera             |
| `desde`          | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                            |
| `hasta`          | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                            |
| `id_firma`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | conformidad de recepcion o entrega, RT-16.14 |

### `CONDICION_LIBERACION`

| **Atributo**              | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                    |
|:------------------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:-----------------------------------------|
| **Atributo**              | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                    |
| `id_visita`                   | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                                        |
| `documentacion_validada`      | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                                        |
| `autorizacion_aduanera`       | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                                        |
| `sin_retencion_fitosanitaria` | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                                        |
| `sin_deuda_asociada`          | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                                        |
| `vgm_dentro_de_tolerancia`    | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                                        |
| `liberado`                    | boolean      | —             | {verdadero, falso}                       | Derivado         | derivado: conjuncion de las cinco, RN-06 |
| `instante_ultima_evaluacion`  | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                        |

### `BLOQUE`

| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**    |
|:--------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:-------------------------|
| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**    |
| `id_bloque`         | string       | PK            | Identificador unico                      | Obligatorio      | —                        |
| `id_zona_operativa` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-08.ZONA_OPERATIVA |
| `habilitado_imdg`   | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                        |

### `CELDA`

| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
|:--------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------|
| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
| `id_celda`          | string       | PK            | Identificador unico                      | Obligatorio      | —                     |
| `id_bloque`         | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                     |
| `bahia`             | int          | —             | Numerico no negativo                     | Obligatorio      | —                     |
| `fila`              | int          | —             | Numerico no negativo                     | Obligatorio      | —                     |
| `altura`            | int          | —             | Numerico no negativo                     | Obligatorio      | —                     |
| `tiene_toma_reefer` | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                     |

### `EQUIPO_PATIO`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**                      |
|:-----------------|:-------------|:--------------|:---------------------------------------------|:-----------------|:-------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**                      |
| `id_equipo`      | string       | PK            | Identificador unico                          | Obligatorio      | —                                          |
| `tipo`           | enum         | —             | {grua de patio, tractocamion, equipo pesado} | Obligatorio      | grua de patio, tractocamion, equipo pesado |
| `fuente_energia` | enum         | —             | {diesel, electrico}                          | Obligatorio      | diesel, electrico                          |
| `instrumentado`  | boolean      | —             | {verdadero, falso}                           | Obligatorio      | condiciona D-06.CONSUMO_EQUIPO             |

### `PUNTO_DE_PASO`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                          | **Obligat.** | **Origen y nota** |
|:-----------------|:-------------|:--------------|:----------------------------------------------------|:-----------------|:----------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                          | **Obligat.** | **Origen y nota** |
| `id_punto`       | string       | PK            | Identificador unico                                 | Obligatorio      | —                     |
| `ubicacion`      | string       | —             | Ubicacion fisica del portico o lector en el recinto | Obligatorio      | —                     |

### `LECTURA_OPTICA`

| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                        | **Obligat.** | **Origen y nota**                         |
|:--------------------|:-------------|:--------------|:--------------------------------------------------|:-----------------|:----------------------------------------------|
| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                        | **Obligat.** | **Origen y nota**                         |
| `id_lectura`        | string       | PK            | Identificador unico                               | Obligatorio      | —                                             |
| `id_punto`          | string       | FK            | Identificador de la entidad referenciada          | Obligatorio      | —                                             |
| `instante`          | timestamptz  | —             | Instante con zona horaria                         | Obligatorio      | —                                             |
| `codigo_leido`      | string       | —             | Codigo ISO 6346 o patente, segun el punto de paso | Condicional      | puede no coincidir con ninguna visita abierta |
| `confianza_lectura` | decimal      | —             | 0 a 1                                             | Obligatorio      | 0 a 1                                         |
| `id_visita`         | string       | FK            | Identificador de la entidad referenciada          | Condicional      | nulo mientras la lectura no se concilia       |

## Gate y transporte terrestre

### `TRANSPORTISTA`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**        | **Obligat.** | **Origen y nota** |
|:-----------------------|:-------------|:--------------|:----------------------------------|:-----------------|:----------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**        | **Obligat.** | **Origen y nota** |
| `id_transportista`     | string       | PK            | Identificador unico               | Obligatorio      | —                     |
| `razon_social`         | string       | —             | Razon social registrada           | Obligatorio      | —                     |
| `rol_unico_tributario` | string       | UK            | Identificador tributario nacional | Obligatorio      | —                     |

### `CAMION`

| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
|:-------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------|
| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
| `patente`          | string       | PK            | Identificador unico                      | Obligatorio      | —                     |
| `id_transportista` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                     |

### `CONDUCTOR`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                   |
|:-----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:--------------------------------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                   |
| `id_conductor`         | string       | PK            | Identificador unico                      | Obligatorio      | —                                                       |
| `id_persona`           | string       | FK,UK         | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.PERSONA, el dato personal vive alli, RT-05.09 |
| `id_transportista`     | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                                       |
| `habilitacion_vigente` | boolean      | —             | {verdadero, falso}                       | Derivado         | derivado de D-07.HABILITACION                           |

### `CITA`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                        | **Obligat.** | **Origen y nota**                           |
|:---------------------|:-------------|:--------------|:--------------------------------------------------|:-----------------|:------------------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                        | **Obligat.** | **Origen y nota**                           |
| `id_cita`            | string       | PK            | Identificador unico                               | Obligatorio      | —                                               |
| `id_transportista`   | string       | FK            | Identificador de la entidad referenciada          | Obligatorio      | —                                               |
| `id_visita`          | string       | FK            | Identificador de la entidad referenciada          | Obligatorio      | ref. D-02.VISITA                                |
| `franja_desde`       | timestamptz  | —             | Instante con zona horaria                         | Obligatorio      | —                                               |
| `franja_hasta`       | timestamptz  | —             | Instante con zona horaria                         | Obligatorio      | —                                               |
| `estado`             | enum         | —             | {confirmada, cumplida, fuera de ventana, no show} | Obligatorio      | confirmada, cumplida, fuera de ventana, no show |
| `instante_solicitud` | timestamptz  | —             | Instante con zona horaria                         | Obligatorio      | —                                               |

### `TURNO_CAMION`

| **Atributo**               | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**              |
|:-------------------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:-----------------------------------|
| **Atributo**               | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**              |
| `id_turno_camion`              | string       | PK            | Identificador unico                      | Obligatorio      | —                                  |
| `patente`                      | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                  |
| `id_conductor`                 | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                  |
| `id_cita`                      | string       | FK            | Identificador de la entidad referenciada | Condicional      | nulo si el camion llega sin cita   |
| `instante_arribo_barrera`      | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                  |
| `instante_instruccion_emitida` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                  |
| `instante_salida`              | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                  |
| `estadia_minutos`              | int          | —             | Minutos                                  | Derivado         | derivado de EVENTO_GATE, RF-GAT-12 |

### `EVENTO_GATE`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                   | **Obligat.** | **Origen y nota** |
|:------------------|:-------------|:--------------|:-------------------------------------------------------------|:-----------------|:----------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                   | **Obligat.** | **Origen y nota** |
| `id_evento`       | string       | PK            | Identificador unico                                          | Obligatorio      | —                     |
| `id_turno_camion` | string       | FK            | Identificador de la entidad referenciada                     | Obligatorio      | —                     |
| `tipo`            | enum         | —             | {entrada, salida}                                            | Obligatorio      | entrada, salida       |
| `puesto`          | string       | —             | Identificador del puesto de gate: 8 de entrada y 6 de salida | Obligatorio      | —                     |
| `instante`        | timestamptz  | —             | Instante con zona horaria                                    | Obligatorio      | —                     |
| `id_correlacion`  | string       | —             | Identificador de correlacion comun de extremo a extremo      | Obligatorio      | RT-05.19              |

### `MOVIMIENTO_TERRESTRE`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
|:------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
| `id_turno_camion` | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                     |
| `id_visita`       | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                     |
| `sentido`         | enum         | —             | {entrega, retiro}                        | Obligatorio      | entrega, retiro       |
| `instante`        | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                     |

### `DOCUMENTO_TRANSPORTE`

| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                 |
|:----------------------|:-------------|:--------------|:----------------------------------------------------------------|:-----------------|:--------------------------------------|
| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                 |
| `id_documento`        | string       | PK            | Identificador unico                                             | Obligatorio      | —                                     |
| `id_visita`           | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | ref. D-02.VISITA                      |
| `tipo`                | string       | —             | {catalogo de documentos de transporte, a cerrar con el CLIENTE} | Obligatorio      | —                                     |
| `estado_validacion`   | enum         | —             | {validado, con discrepancia, pendiente}                         | Obligatorio      | validado, con discrepancia, pendiente |
| `instante_validacion` | timestamptz  | —             | Instante con zona horaria                                       | Obligatorio      | validacion anticipada, RF-GAT-03      |

### `PESAJE_VGM`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                             |
|:-----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:------------------------------------------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                             |
| `id_pesaje`            | string       | PK            | Identificador unico                      | Obligatorio      | —                                                                 |
| `id_visita`            | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.VISITA                                                  |
| `secuencia_pesaje`     | int          | —             | Numerico no negativo                     | Obligatorio      | 1 pesaje inicial, mayor a 1 repesaje tras discrepancia, RF-GAT-09 |
| `masa_declarada`       | decimal      | —             | kg                                       | Obligatorio      | kg                                                                |
| `masa_verificada`      | decimal      | —             | kg                                       | Obligatorio      | kg                                                                |
| `desviacion`           | decimal      | —             | kg                                       | Derivado         | derivado, kg                                                      |
| `dentro_de_tolerancia` | boolean      | —             | {verdadero, falso}                       | Obligatorio      | RN-05                                                             |
| `instante`             | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                                                 |
| `id_bascula`           | string       | —             | Identificador de la bascula certificada  | Obligatorio      | —                                                                 |

### `INSTRUCCION_DESTINO`

| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
|:-------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------|
| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
| `id_instruccion`   | string       | PK            | Identificador unico                      | Obligatorio      | —                     |
| `id_turno_camion`  | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                     |
| `celda_destino`    | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.CELDA       |
| `instante_emision` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                     |

### `EXCEPCION_GATE`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota**                         |
|:------------------|:-------------|:--------------|:------------------------------------------------|:-----------------|:----------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota**                         |
| `id_excepcion`    | string       | PK            | Identificador unico                             | Obligatorio      | —                                             |
| `id_turno_camion` | string       | FK            | Identificador de la entidad referenciada        | Obligatorio      | —                                             |
| `motivo`          | enum         | —             | {documental, VGM, habilitacion, sin cita, otro} | Obligatorio      | documental, VGM, habilitacion, sin cita, otro |
| `estado`          | enum         | —             | {abierta, resuelta, derivada}                   | Obligatorio      | abierta, resuelta, derivada                   |
| `instante`        | timestamptz  | —             | Instante con zona horaria                       | Obligatorio      | —                                             |

## Reefer y cadena de frio

### `TABLERO`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                 |
|:------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:--------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                 |
| `id_tablero`      | string       | PK            | Identificador unico                      | Obligatorio      | —                                     |
| `id_bloque`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.BLOQUE                      |
| `estado`          | enum         | —             | {operativo, en falla, sin comunicacion}  | Obligatorio      | operativo, en falla, sin comunicacion |
| `tomas_nominales` | int          | —             | Numerico no negativo                     | Obligatorio      | —                                     |

### `TOMA_REEFER`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                |
|:-----------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:-----------------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                                |
| `id_toma`        | string       | PK            | Identificador unico                      | Obligatorio      | —                                                    |
| `id_tablero`     | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                                    |
| `id_celda`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.CELDA                                      |
| `estado`         | enum         | —             | {libre, ocupada, fuera de servicio}      | Obligatorio      | libre, ocupada, fuera de servicio                    |
| `instrumentada`  | boolean      | —             | {verdadero, falso}                       | Condicional      | si es falsa, la serie proviene de agregado reportado |

### `CONEXION_REEFER`

| **Atributo**                  | **Tipo** | **Clave** | **Dominio de valores**                                        | **Obligat.** | **Origen y nota**                  |
|:----------------------------------|:-------------|:--------------|:------------------------------------------------------------------|:-----------------|:---------------------------------------|
| **Atributo**                  | **Tipo** | **Clave** | **Dominio de valores**                                        | **Obligat.** | **Origen y nota**                  |
| `id_conexion`                     | string       | PK            | Identificador unico                                               | Obligatorio      | —                                      |
| `id_visita`                       | string       | FK            | Identificador de la entidad referenciada                          | Obligatorio      | ref. D-02.VISITA                       |
| `id_toma`                         | string       | FK            | Identificador de la entidad referenciada                          | Obligatorio      | —                                      |
| `instante_conexion`               | timestamptz  | —             | Instante con zona horaria                                         | Obligatorio      | —                                      |
| `instante_desconexion`            | timestamptz  | —             | Instante con zona horaria; nulo mientras la conexion esta vigente | Condicional      | nulo mientras la conexion esta vigente |
| `consigna_temperatura`            | decimal      | —             | grados Celsius                                                    | Obligatorio      | grados Celsius                         |
| `minutos_desconectado_acumulados` | int          | —             | Minutos                                                           | Derivado         | derivado, umbral en RN-10              |

### `MUESTRA_TEMPERATURA`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**           |
|:------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:--------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**           |
| `id_conexion`     | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                               |
| `instante`        | timestamptz  | PK            | Instante con zona horaria                | Obligatorio      | —                               |
| `temperatura`     | decimal      | —             | grados Celsius                           | Obligatorio      | grados Celsius                  |
| `estado_conexion` | boolean      | —             | {verdadero, falso}                       | Obligatorio      | —                               |
| `consumo_kwh`     | decimal      | —             | Numerico no negativo                     | Obligatorio      | —                               |
| `origen`          | enum         | —             | {borde local, agregado reportado}        | Obligatorio      | borde local, agregado reportado |
| `calidad_dato`    | enum         | —             | {valida, interpolada, ausente}           | Obligatorio      | valida, interpolada, ausente    |

### `PARAMETRO_DESVIACION`

| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                          |
|:--------------------------|:-------------|:--------------|:----------------------------------------------------------------------|:-----------------|:-----------------------------------------------|
| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                          |
| `id_parametro`            | string       | PK            | Identificador unico                                                   | Obligatorio      | —                                              |
| `version`                 | int          | PK            | Entero correlativo                                                    | Obligatorio      | el parametro se versiona, nunca se sobrescribe |
| `banda_superior`          | decimal      | —             | VACIO DECLARADO: grados Celsius, sin valor fijado por el caso (RN-11) | Obligatorio      | sin valor fijado por el caso, RN-11            |
| `banda_inferior`          | decimal      | —             | VACIO DECLARADO: grados Celsius, sin valor fijado por el caso (RN-11) | Obligatorio      | sin valor fijado por el caso, RN-11            |
| `duracion_minima_minutos` | int          | —             | Minutos; acotada para no exceder los 5 min de RT-05.29                | Obligatorio      | acotada para no exceder los 5 min de RF-REF    |
| `vigencia_desde`          | timestamptz  | —             | Instante con zona horaria                                             | Obligatorio      | —                                              |
| `vigencia_hasta`          | timestamptz  | —             | Instante con zona horaria                                             | Obligatorio      | —                                              |
| `id_autor`                | string       | FK            | Identificador de la entidad referenciada                              | Obligatorio      | ref. D-07.PERSONA                              |

### `ALARMA`

| **Atributo**             | **Tipo** | **Clave** | **Dominio de valores**                                    | **Obligat.** | **Origen y nota**                                       |
|:-----------------------------|:-------------|:--------------|:--------------------------------------------------------------|:-----------------|:------------------------------------------------------------|
| **Atributo**             | **Tipo** | **Clave** | **Dominio de valores**                                    | **Obligat.** | **Origen y nota**                                       |
| `id_alarma`                  | string       | PK            | Identificador unico                                           | Obligatorio      | —                                                           |
| `tipo`                       | enum         | —             | {desviacion, desconexion, falla de tablero, ausencia de dato} | Obligatorio      | desviacion, desconexion, falla de tablero, ausencia de dato |
| `severidad`                  | enum         | —             | {baja, media, alta, critica}                                  | Obligatorio      | baja, media, alta, critica                                  |
| `tipo_objeto_origen`         | enum         | —             | {conexion, toma, tablero}                                     | Obligatorio      | conexion, toma, tablero                                     |
| `id_objeto_origen`           | string       | FK            | Identificador de la entidad referenciada                      | Obligatorio      | polimorfico, unica referencia al origen                     |
| `instante_evento_fisico`     | timestamptz  | —             | Instante con zona horaria                                     | Obligatorio      | —                                                           |
| `instante_generacion`        | timestamptz  | —             | Instante con zona horaria                                     | Obligatorio      | diferencia menor o igual a 5 min                            |
| `id_parametro_aplicado`      | string       | FK            | Identificador de la entidad referenciada                      | Obligatorio      | —                                                           |
| `version_parametro_aplicado` | int          | FK            | Entero correlativo                                            | Obligatorio      | —                                                           |
| `estado`                     | enum         | —             | {abierta, confirmada, escalada, cerrada}                      | Obligatorio      | abierta, confirmada, escalada, cerrada                      |

### `CONFIRMACION_ALARMA`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**      |
|:---------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:---------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**      |
| `id_alarma`          | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                          |
| `nivel_escalamiento` | int          | PK            | Numerico no negativo                     | Obligatorio      | RN-08                      |
| `id_persona`         | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.PERSONA          |
| `instante`           | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                          |
| `canal`              | enum         | —             | {consola, movil, mensajeria}             | Obligatorio      | consola, movil, mensajeria |

## Nave y planificacion

### `NAVIERA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**        |
|:-----------------|:-------------|:--------------|:---------------------------------------------|:-----------------|:-----------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**        |
| `id_naviera`     | string       | PK            | Identificador unico                          | Obligatorio      | —                            |
| `nombre`         | string       | —             | Nombre comercial de la linea naviera         | Obligatorio      | —                            |
| `codigo_scac`    | string       | UK            | Codigo de transportista de cuatro caracteres | Obligatorio      | identificador de intercambio |

### `NAVE`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota** |
|:-----------------|:-------------|:--------------|:----------------------------------------------------------------|:-----------------|:----------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota** |
| `id_nave`        | string       | PK            | Identificador unico                                             | Obligatorio      | —                     |
| `nombre`         | string       | —             | Nombre de la nave                                               | Obligatorio      | —                     |
| `numero_imo`     | string       | UK            | Numero de la Organizacion Maritima Internacional, siete digitos | Obligatorio      | —                     |
| `id_naviera`     | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                     |

### `RECALADA`

| **Atributo**         | **Tipo** | **Clave** | **Dominio de valores**                                                   | **Obligat.** | **Origen y nota**                          |
|:-------------------------|:-------------|:--------------|:-----------------------------------------------------------------------------|:-----------------|:-----------------------------------------------|
| **Atributo**         | **Tipo** | **Clave** | **Dominio de valores**                                                   | **Obligat.** | **Origen y nota**                          |
| `id_recalada`            | string       | PK            | Identificador unico                                                          | Obligatorio      | —                                              |
| `id_nave`                | string       | FK            | Identificador de la entidad referenciada                                     | Obligatorio      | —                                              |
| `ventana_confirmada`     | timestamptz  | —             | Instante con zona horaria                                                    | Obligatorio      | confirmacion con 72 h de antelacion, RF-NAV-03 |
| `instante_atraque_real`  | timestamptz  | —             | Instante con zona horaria                                                    | Obligatorio      | —                                              |
| `instante_zarpe_real`    | timestamptz  | —             | Instante con zona horaria                                                    | Obligatorio      | —                                              |
| `sitio_asignado`         | string       | —             | {sitio 1, sitio 2, sitio 3; ampliable a un cuarto sitio por parametrizacion} | Obligatorio      | —                                              |
| `productividad_mov_hora` | decimal      | —             | Numerico no negativo                                                         | Derivado         | derivado, RF-NAV-12                            |

### `PLAN_ESTIBA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                | **Obligat.** | **Origen y nota**                     |
|:-----------------|:-------------|:--------------|:------------------------------------------|:-----------------|:------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                | **Obligat.** | **Origen y nota**                     |
| `id_plan`        | string       | PK            | Identificador unico                       | Obligatorio      | —                                         |
| `version`        | int          | PK            | Entero correlativo                        | Obligatorio      | el plan se versiona, nunca se sobrescribe |
| `id_recalada`    | string       | FK            | Identificador de la entidad referenciada  | Obligatorio      | —                                         |
| `estado`         | enum         | —             | {propuesto, aprobado, corregido}          | Obligatorio      | propuesto, aprobado, corregido            |
| `instante`       | timestamptz  | —             | Instante con zona horaria; operacion 24x7 | Obligatorio      | —                                         |
| `origen`         | enum         | —             | {algoritmo, planificador}                 | Obligatorio      | algoritmo, planificador                   |

### `CORRECCION_PLAN`

| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                       |
|:----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:--------------------------------------------|
| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                       |
| `id_correccion`       | string       | PK            | Identificador unico                      | Obligatorio      | —                                           |
| `id_plan`             | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                           |
| `version_plan`        | int          | FK            | Entero correlativo                       | Obligatorio      | —                                           |
| `motivo_estructurado` | enum         | —             | {catalogo cerrado}                       | Obligatorio      | catalogo cerrado, RF-NAV-08, no texto libre |
| `id_autor`            | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.PERSONA                           |
| `instante`            | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                           |

### `REGLA_PLANIFICADOR`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**        |
|:-----------------------|:-------------|:--------------|:---------------------------------------------|:-----------------|:-----------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**        |
| `id_regla`             | string       | PK            | Identificador unico                          | Obligatorio      | —                            |
| `enunciado`            | string       | —             | Enunciado de la regla en lenguaje de negocio | Obligatorio      | —                            |
| `id_correccion_origen` | string       | FK            | Identificador de la entidad referenciada     | Obligatorio      | —                            |
| `vigencia_desde`       | timestamptz  | —             | Instante con zona horaria                    | Obligatorio      | —                            |
| `estado`               | enum         | —             | {candidata, vigente, retirada}               | Obligatorio      | candidata, vigente, retirada |

### `ASIGNACION_EQUIPO`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**       |
|:-----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**       |
| `id_asignacion`        | string       | PK            | Identificador unico                      | Obligatorio      | —                           |
| `id_recalada`          | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                           |
| `id_equipo`            | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.EQUIPO_PATIO      |
| `id_turno_operacional` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.TURNO_OPERACIONAL |
| `desde`                | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                           |
| `hasta`                | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                           |

### `ORDEN_EMBARQUE`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**        |
|:---------------------|:-------------|:--------------|:--------------------------------------------------------|:-----------------|:-----------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**        |
| `id_orden`           | string       | PK            | Identificador unico                                     | Obligatorio      | —                            |
| `id_recalada`        | string       | FK            | Identificador de la entidad referenciada                | Obligatorio      | —                            |
| `id_naviera`         | string       | FK            | Identificador de la entidad referenciada                | Obligatorio      | —                            |
| `estandar_mensaje`   | string       | —             | Denominacion del mensaje sectorial de orden de embarque | Obligatorio      | orden de embarque, RF-INT-02 |
| `version_contrato`   | string       | —             | Version semantica del contrato de interfaz vigente      | Obligatorio      | ref. D-08.CONTRATO_INTERFAZ  |
| `instante_recepcion` | timestamptz  | —             | Instante con zona horaria                               | Obligatorio      | —                            |
| `id_correlacion`     | string       | —             | Identificador de correlacion comun de extremo a extremo | Obligatorio      | RT-05.19                     |

### `EMBARCADOR`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores** | **Obligat.** | **Origen y nota** |
|:-----------------|:-------------|:--------------|:---------------------------|:-----------------|:----------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores** | **Obligat.** | **Origen y nota** |
| `id_embarcador`  | string       | PK            | Identificador unico        | Obligatorio      | —                     |
| `razon_social`   | string       | —             | Razon social registrada    | Obligatorio      | —                     |

### `INSTRUCCION_EMBARQUE`

| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                 |
|:------------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:--------------------------------------|
| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                 |
| `id_instruccion`        | string       | PK            | Identificador unico                      | Obligatorio      | —                                     |
| `id_recalada`           | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                     |
| `id_embarcador`         | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                     |
| `canal`                 | enum         | —             | {portal estructurado, RF-POR-09}         | Obligatorio      | portal estructurado, RF-POR-09        |
| `estado_validacion`     | enum         | —             | {aceptada, con discrepancia, rechazada}  | Obligatorio      | aceptada, con discrepancia, rechazada |
| `instante_presentacion` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                     |

## Evidencia y facturacion

### `CLIENTE`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
|:-----------------|:-------------|:--------------|:----------------------------------------------------------|:-----------------|:--------------------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
| `id_cliente`     | string       | PK            | Identificador unico                                       | Obligatorio      | —                                                       |
| `razon_social`   | string       | —             | Razon social registrada                                   | Obligatorio      | —                                                       |
| `tipo`           | enum         | —             | {exportador, importador, agencia, transportista, naviera} | Obligatorio      | exportador, importador, agencia, transportista, naviera |

### `HECHO_FACTURABLE`

| **Atributo**         | **Tipo** | **Clave** | **Dominio de valores**                                                                                         | **Obligat.** | **Origen y nota**                                                                                            |
|:-------------------------|:-------------|:--------------|:-------------------------------------------------------------------------------------------------------------------|:-----------------|:-----------------------------------------------------------------------------------------------------------------|
| **Atributo**         | **Tipo** | **Clave** | **Dominio de valores**                                                                                         | **Obligat.** | **Origen y nota**                                                                                            |
| `id_hecho`               | string       | PK            | Identificador unico                                                                                                | Obligatorio      | —                                                                                                                |
| `id_visita`              | string       | FK            | Identificador de la entidad referenciada                                                                           | Obligatorio      | ref. D-02.VISITA                                                                                                 |
| `tipo`                   | enum         | —             | {transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial} | Obligatorio      | transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial |
| `instante_ocurrencia`    | timestamptz  | —             | Instante con zona horaria                                                                                          | Obligatorio      | instante propio del hecho, RF-FAC-01                                                                             |
| `id_regla_aplicada`      | string       | FK            | Identificador de la entidad referenciada                                                                           | Obligatorio      | —                                                                                                                |
| `version_regla_aplicada` | int          | FK            | Entero correlativo                                                                                                 | Obligatorio      | FK compuesta, RF-FAC-02                                                                                          |
| `monto_calculado`        | decimal      | —             | Numerico no negativo                                                                                               | Obligatorio      | —                                                                                                                |
| `estado`                 | enum         | —             | {generado, entregado, objetado, compensado}                                                                        | Obligatorio      | generado, entregado, objetado, compensado                                                                        |

### `REGLA_TARIFARIA`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                                                                         | **Obligat.** | **Origen y nota**                      |
|:------------------|:-------------|:--------------|:-------------------------------------------------------------------------------------------------------------------|:-----------------|:-------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                                                                         | **Obligat.** | **Origen y nota**                      |
| `id_regla`        | string       | PK            | Identificador unico                                                                                                | Obligatorio      | —                                          |
| `version`         | int          | PK            | Entero correlativo                                                                                                 | Obligatorio      | la regla se versiona, nunca se sobrescribe |
| `tipo_hecho`      | enum         | —             | {transferencia, almacenaje, conexion, movimiento adicional, pesaje, inspeccion, zona peligrosa, servicio especial} | Obligatorio      | —                                          |
| `vigencia_desde`  | timestamptz  | —             | Instante con zona horaria                                                                                          | Obligatorio      | —                                          |
| `vigencia_hasta`  | timestamptz  | —             | Instante con zona horaria; operacion 24x7                                                                          | Condicional      | —                                          |
| `id_autor_cambio` | string       | FK            | Identificador de la entidad referenciada                                                                           | Obligatorio      | ref. D-07.PERSONA                          |

### `EVIDENCIA`

| **Atributo**           | **Tipo** | **Clave** | **Dominio de valores**                       | **Obligat.** | **Origen y nota**                          |
|:---------------------------|:-------------|:--------------|:-------------------------------------------------|:-----------------|:-----------------------------------------------|
| **Atributo**           | **Tipo** | **Clave** | **Dominio de valores**                       | **Obligat.** | **Origen y nota**                          |
| `id_evidencia`             | string       | PK            | Identificador unico                              | Obligatorio      | —                                              |
| `id_hecho`                 | string       | FK            | Identificador de la entidad referenciada         | Obligatorio      | —                                              |
| `tipo`                     | enum         | —             | {evento, medicion, serie, lectura optica, firma} | Obligatorio      | evento, medicion, serie, lectura optica, firma |
| `referencia_objeto_origen` | string       | —             | Puntero al objeto de origen en D-02, D-03 o D-04 | Obligatorio      | puntero al objeto de D-02, D-03 o D-04         |
| `sello_integridad`         | string       | —             | Resumen criptografico del contenido, inalterable | Obligatorio      | inalterable, RT-16.07                          |
| `instante_creacion`        | timestamptz  | —             | Instante con zona horaria                        | Obligatorio      | —                                              |

### `OBJECION`

| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**                  | **Obligat.** | **Origen y nota**                     |
|:------------------------|:-------------|:--------------|:--------------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**                  | **Obligat.** | **Origen y nota**                     |
| `id_objecion`           | string       | PK            | Identificador unico                         | Obligatorio      | —                                         |
| `id_hecho`              | string       | FK            | Identificador de la entidad referenciada    | Obligatorio      | —                                         |
| `id_cliente`            | string       | FK            | Identificador de la entidad referenciada    | Obligatorio      | —                                         |
| `motivo`                | string       | —             | Motivo declarado por el cliente             | Obligatorio      | —                                         |
| `estado`                | enum         | —             | {abierta, en analisis, aceptada, rechazada} | Obligatorio      | abierta, en analisis, aceptada, rechazada |
| `instante_presentacion` | timestamptz  | —             | Instante con zona horaria                   | Obligatorio      | —                                         |

### `RESOLUCION_OBJECION`

| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**               |
|:------------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:------------------------------------|
| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**               |
| `id_objecion`           | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                                   |
| `resultado`             | enum         | —             | {acogida, acogida parcial, rechazada}    | Obligatorio      | acogida, acogida parcial, rechazada |
| `id_evidencia_invocada` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                   |
| `id_responsable`        | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.PERSONA                   |
| `instante`              | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                   |

### `ENTREGA_ERP`

| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                     |
|:--------------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                     |
| `id_hecho`                | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                                         |
| `id_documento_tributario` | string       | —             | Folio del documento emitido por el ERP   | Condicional      | emitido por el ERP, nunca por la solucion |
| `instante_entrega`        | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                         |
| `estado_conciliacion`     | enum         | —             | {pendiente, conciliada, con diferencia}  | Obligatorio      | pendiente, conciliada, con diferencia     |

## Inspecciones de autoridad

### `AUTORIDAD`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**            |
|:-----------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:---------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**            |
| `id_autoridad`   | string       | PK            | Identificador unico                      | Obligatorio      | —                                |
| `tipo`           | enum         | —             | {aduana, SAG, sanitaria, maritima}       | Obligatorio      | aduana, SAG, sanitaria, maritima |
| `nombre`         | string       | —             | Denominacion oficial del organismo       | Obligatorio      | —                                |
| `id_contraparte` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-08.CONTRAPARTE            |

### `SOLICITUD_INSPECCION`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**             |
|:---------------------|:-------------|:--------------|:--------------------------------------------------------|:-----------------|:----------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**             |
| `id_solicitud`       | string       | PK            | Identificador unico                                     | Obligatorio      | —                                 |
| `id_visita`          | string       | FK            | Identificador de la entidad referenciada                | Obligatorio      | ref. D-02.VISITA                  |
| `id_autoridad`       | string       | FK            | Identificador de la entidad referenciada                | Obligatorio      | —                                 |
| `instante_recepcion` | timestamptz  | —             | Instante con zona horaria                               | Obligatorio      | —                                 |
| `canal`              | enum         | —             | {interfaz, canal asistido trazable}                     | Obligatorio      | interfaz, canal asistido trazable |
| `id_correlacion`     | string       | —             | Identificador de correlacion comun de extremo a extremo | Obligatorio      | RT-05.19                          |

### `CITA_INSPECCION`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                     |
|:---------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                     |
| `id_cita`            | string       | PK            | Identificador unico                      | Obligatorio      | —                                         |
| `id_solicitud`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                         |
| `hora_acordada`      | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                         |
| `hora_real_atencion` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                         |
| `cumplida_en_hora`   | boolean      | —             | {verdadero, falso}                       | Derivado         | derivado de las dos anteriores, RF-INS-07 |

### `REMOCION_PROGRAMADA`

| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**               |
|:----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:------------------------------------|
| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**               |
| `id_remocion`         | string       | PK            | Identificador unico                      | Obligatorio      | —                                   |
| `id_cita`             | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                   |
| `instante_programado` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                   |
| `id_movimiento`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.MOVIMIENTO, al ejecutarse |
| `estado`              | enum         | —             | {programada, ejecutada, anulada}         | Obligatorio      | programada, ejecutada, anulada      |

### `ACTA_INSPECCION`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**                      |
|:-----------------|:-------------|:--------------|:---------------------------------------------|:-----------------|:-------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                   | **Obligat.** | **Origen y nota**                      |
| `id_acta`        | string       | PK            | Identificador unico                          | Obligatorio      | —                                          |
| `id_cita`        | string       | FK            | Identificador de la entidad referenciada     | Obligatorio      | —                                          |
| `resultado`      | enum         | —             | {conforme, con observaciones, con retencion} | Obligatorio      | conforme, con observaciones, con retencion |
| `id_firma`       | string       | FK            | Identificador de la entidad referenciada     | Obligatorio      | firma electronica, RT-16.14                |
| `instante`       | timestamptz  | —             | Instante con zona horaria                    | Obligatorio      | —                                          |

### `RETENCION`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                | **Obligat.** | **Origen y nota**                       |
|:-----------------|:-------------|:--------------|:------------------------------------------|:-----------------|:--------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                | **Obligat.** | **Origen y nota**                       |
| `id_retencion`   | string       | PK            | Identificador unico                       | Obligatorio      | —                                           |
| `id_acta`        | string       | FK            | Identificador de la entidad referenciada  | Condicional      | nulo si la retencion no proviene de un acta |
| `id_visita`      | string       | FK            | Identificador de la entidad referenciada  | Obligatorio      | ref. D-02.VISITA                            |
| `id_autoridad`   | string       | FK            | Identificador de la entidad referenciada  | Obligatorio      | —                                           |
| `motivo`         | string       | —             | Motivo declarado por la autoridad         | Obligatorio      | —                                           |
| `vigencia_desde` | timestamptz  | —             | Instante con zona horaria                 | Obligatorio      | —                                           |
| `vigencia_hasta` | timestamptz  | —             | Instante con zona horaria; operacion 24x7 | Condicional      | nulo mientras la retencion sigue vigente    |

## Energia y emisiones

### `CONSUMO_EQUIPO`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                         | **Obligat.** | **Origen y nota**                            |
|:------------------|:-------------|:--------------|:---------------------------------------------------|:-----------------|:-------------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                         | **Obligat.** | **Origen y nota**                            |
| `id_consumo`      | string       | PK            | Identificador unico                                | Obligatorio      | —                                                |
| `id_equipo`       | string       | FK            | Identificador de la entidad referenciada           | Obligatorio      | ref. D-02.EQUIPO_PATIO                           |
| `unidad`          | enum         | —             | {litros de diesel, kWh}                            | Obligatorio      | litros de diesel, kWh                            |
| `valor`           | decimal      | —             | Numerico no negativo                               | Obligatorio      | —                                                |
| `instante_desde`  | timestamptz  | —             | Instante con zona horaria                          | Obligatorio      | —                                                |
| `instante_hasta`  | timestamptz  | —             | Instante con zona horaria                          | Obligatorio      | —                                                |
| `origen_medicion` | enum         | —             | {instrumentacion por equipo, estimacion declarada} | Obligatorio      | instrumentacion por equipo, estimacion declarada |

### `ATRIBUCION_CONSUMO`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                                                                 | **Obligat.** | **Origen y nota**                                |
|:---------------------|:-------------|:--------------|:-----------------------------------------------------------------------------------------------------------|:-----------------|:-----------------------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                                                                 | **Obligat.** | **Origen y nota**                                |
| `id_consumo`         | string       | PK,FK         | Identificador de la entidad referenciada                                                                   | Obligatorio      | —                                                    |
| `id_emision`         | string       | PK,FK         | Identificador de la entidad referenciada                                                                   | Obligatorio      | —                                                    |
| `fraccion_atribuida` | decimal      | —             | 0 a 1                                                                                                      | Obligatorio      | 0 a 1, suma 1 por consumo                            |
| `criterio`           | enum         | —             | {movimientos ejecutados, tiempo de ciclo, masa movida}; valor adoptado: movimientos ejecutados (DEC-C4-01) | Obligatorio      | movimientos ejecutados, tiempo de ciclo, masa movida |
| `version_algoritmo`  | string       | —             | Version semantica del algoritmo de reparto                                                                 | Obligatorio      | obligatoria para reproducir el reparto               |

### `FACTOR_EMISION`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                       | **Obligat.** | **Origen y nota**         |
|:-----------------|:-------------|:--------------|:-------------------------------------------------|:-----------------|:------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                       | **Obligat.** | **Origen y nota**         |
| `id_factor`      | string       | PK            | Identificador unico                              | Obligatorio      | —                             |
| `version`        | int          | PK            | Entero correlativo                               | Obligatorio      | —                             |
| `fuente`         | string       | —             | Denominacion y version de la fuente metodologica | Obligatorio      | GLEC v3.2                     |
| `alcance`        | enum         | —             | {1, 2, 3}                                        | Obligatorio      | 1, 2, 3                       |
| `valor`          | decimal      | —             | Numerico no negativo                             | Obligatorio      | —                             |
| `unidad`         | string       | —             | kg CO2e por unidad de consumo                    | Obligatorio      | kg CO2e por unidad de consumo |
| `vigencia_desde` | timestamptz  | —             | Instante con zona horaria                        | Obligatorio      | —                             |

### `EMISION_CONTENEDOR`

| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota**          |
|:--------------------|:-------------|:--------------|:------------------------------------------------|:-----------------|:-------------------------------|
| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota**          |
| `id_emision`        | string       | PK            | Identificador unico                             | Obligatorio      | —                              |
| `id_visita`         | string       | FK            | Identificador de la entidad referenciada        | Obligatorio      | ref. D-02.VISITA               |
| `consumo_atribuido` | decimal      | —             | Numerico no negativo                            | Derivado         | derivado de ATRIBUCION_CONSUMO |
| `id_factor`         | string       | FK            | Identificador de la entidad referenciada        | Obligatorio      | —                              |
| `version_factor`    | int          | FK            | Entero correlativo                              | Obligatorio      | FK compuesta                   |
| `valor_emision`     | decimal      | —             | kg                                              | Obligatorio      | kg CO2e                        |
| `metodologia`       | string       | —             | Denominacion de la norma y de la guia aplicadas | Obligatorio      | ISO 14083 via GLEC v3.2        |
| `instante_calculo`  | timestamptz  | —             | Instante con zona horaria                       | Obligatorio      | —                              |

## Acceso e identidad

### `PERSONA`

| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                                                         |
|:----------------------|:-------------|:--------------|:----------------------------------------------------------------------|:-----------------|:------------------------------------------------------------------------------|
| **Atributo**      | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                                                         |
| `id_persona`          | string       | PK            | Identificador unico                                                   | Obligatorio      | —                                                                             |
| `tipo`                | enum         | —             | {propio, eventual, conductor, visita, inspector}                      | Obligatorio      | propio, eventual, conductor, visita, inspector                                |
| `documento_identidad` | string       | UK            | Documento nacional de identidad o pasaporte; cifrado a nivel de campo | Obligatorio      | dato personal, cifrado de campo, unico registro del dato, RT-11.10 y RT-05.09 |
| `organizacion`        | string       | —             | Texto acotado                                                         | Obligatorio      | —                                                                             |

### `HABILITACION`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                    | **Obligat.** | **Origen y nota**                      |
|:------------------|:-------------|:--------------|:--------------------------------------------------------------|:-----------------|:-------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                    | **Obligat.** | **Origen y nota**                      |
| `id_habilitacion` | string       | PK            | Identificador unico                                           | Obligatorio      | —                                          |
| `id_persona`      | string       | FK            | Identificador de la entidad referenciada                      | Obligatorio      | —                                          |
| `tipo`            | string       | —             | {catalogo de habilitaciones del plan de proteccion portuaria} | Obligatorio      | —                                          |
| `vigencia_desde`  | timestamptz  | —             | Instante con zona horaria                                     | Obligatorio      | —                                          |
| `vigencia_hasta`  | timestamptz  | —             | Instante con zona horaria; operacion 24x7                     | Obligatorio      | —                                          |
| `vigente`         | boolean      | —             | {verdadero, falso}                                            | Derivado         | derivado, verificado al ingreso, RF-ACC-05 |

### `TURNO_OPERACIONAL`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**    | **Obligat.** | **Origen y nota**              |
|:-----------------------|:-------------|:--------------|:------------------------------|:-----------------|:-----------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**    | **Obligat.** | **Origen y nota**              |
| `id_turno_operacional` | string       | PK            | Identificador unico           | Obligatorio      | —                                  |
| `fecha`                | date         | —             | Fecha calendario              | Obligatorio      | —                                  |
| `jornada`              | enum         | —             | {tres turnos, operacion 24x7} | Obligatorio      | tres turnos, operacion 24x7        |
| `instante_cierre`      | timestamptz  | —             | Instante con zona horaria     | Obligatorio      | corte para la conciliacion de D-08 |

### `NOMBRADA`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                    |
|:-----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:-----------------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**                    |
| `id_nombrada`          | string       | PK            | Identificador unico                      | Obligatorio      | —                                        |
| `id_turno_operacional` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                        |
| `instante_publicacion` | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                        |
| `personas_asignadas`   | int          | —             | Numerico no negativo                     | Derivado         | derivado, hasta 380 eventuales por turno |

### `ASIGNACION_NOMBRADA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota** |
|:-----------------|:-------------|:--------------|:------------------------------------------------|:-----------------|:----------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                      | **Obligat.** | **Origen y nota** |
| `id_nombrada`    | string       | PK,FK         | Identificador de la entidad referenciada        | Obligatorio      | —                     |
| `id_persona`     | string       | PK,FK         | Identificador de la entidad referenciada        | Obligatorio      | —                     |
| `funcion`        | string       | —             | {catalogo de funciones operacionales del turno} | Obligatorio      | —                     |

### `CREDENCIAL_TEMPORAL`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                 | **Obligat.** | **Origen y nota**                  |
|:-----------------|:-------------|:--------------|:-----------------------------------------------------------|:-----------------|:---------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                 | **Obligat.** | **Origen y nota**                  |
| `id_credencial`  | string       | PK            | Identificador unico                                        | Obligatorio      | —                                      |
| `id_nombrada`    | string       | FK            | Identificador de la entidad referenciada                   | Obligatorio      | FK compuesta hacia ASIGNACION_NOMBRADA |
| `id_persona`     | string       | FK            | Identificador de la entidad referenciada                   | Obligatorio      | —                                      |
| `vigencia_desde` | timestamptz  | —             | Instante con zona horaria                                  | Obligatorio      | —                                      |
| `vigencia_hasta` | timestamptz  | —             | Instante con zona horaria                                  | Obligatorio      | expiracion automatica, RF-ACC-02       |
| `medio`          | enum         | —             | {tarjeta de proximidad, codigo temporal, aplicacion movil} | Obligatorio      | sin biometria obligatoria, RF-ACC-04   |

### `ZONA_RECINTO`

| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                         |
|:-------------------|:-------------|:--------------|:----------------------------------------------------------------------|:-----------------|:----------------------------------------------|
| **Atributo**   | **Tipo** | **Clave** | **Dominio de valores**                                            | **Obligat.** | **Origen y nota**                         |
| `id_zona`          | string       | PK            | Identificador unico                                                   | Obligatorio      | —                                             |
| `nombre`           | string       | —             | Denominacion de la zona en el plan de proteccion                      | Obligatorio      | —                                             |
| `nivel_proteccion` | enum         | —             | {niveles 1, 2 y 3 del plan de proteccion de la instalacion portuaria} | Obligatorio      | segun el plan de proteccion de la instalacion |

### `ZONA_HABILITADA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
|:-----------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota** |
| `id_credencial`  | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                     |
| `id_zona`        | string       | PK,FK         | Identificador de la entidad referenciada | Obligatorio      | —                     |

### `EVENTO_ACCESO`

| **Atributo**              | **Tipo** | **Clave** | **Dominio de valores**                                                       | **Obligat.** | **Origen y nota**                     |
|:------------------------------|:-------------|:--------------|:---------------------------------------------------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**              | **Tipo** | **Clave** | **Dominio de valores**                                                       | **Obligat.** | **Origen y nota**                     |
| `id_evento`                   | string       | PK            | Identificador unico                                                              | Obligatorio      | —                                         |
| `id_persona`                  | string       | FK            | Identificador de la entidad referenciada                                         | Obligatorio      | —                                         |
| `id_zona`                     | string       | FK            | Identificador de la entidad referenciada                                         | Obligatorio      | —                                         |
| `tipo`                        | enum         | —             | {ingreso, egreso}                                                                | Obligatorio      | ingreso, egreso                           |
| `instante`                    | timestamptz  | —             | Instante con zona horaria                                                        | Obligatorio      | instante del hecho en el borde            |
| `instante_sincronizacion`     | timestamptz  | —             | Instante con zona horaria; posterior al hecho si hubo operacion sin conectividad | Condicional      | posterior si se registro sin conectividad |
| `medio_verificacion`          | string       | —             | {credencial de proximidad, codigo temporal, verificacion manual}                 | Obligatorio      | —                                         |
| `registrado_sin_conectividad` | boolean      | —             | {verdadero, falso}                                                               | Obligatorio      | RF-ACC-08                                 |

### `CONSULTA_SENSIBLE`

| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                                         |
|:--------------------|:-------------|:--------------|:----------------------------------------------------------------|:-----------------|:--------------------------------------------------------------|
| **Atributo**    | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                                         |
| `id_consulta`       | string       | PK            | Identificador unico                                             | Obligatorio      | —                                                             |
| `id_persona`        | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                                             |
| `tipo_dato`         | enum         | —             | {ubicacion de contenedor, informacion comercial, dato personal} | Obligatorio      | ubicacion de contenedor, informacion comercial, dato personal |
| `objeto_consultado` | string       | —             | Identificador del objeto sobre el que se consulto               | Obligatorio      | —                                                             |
| `instante`          | timestamptz  | —             | Instante con zona horaria                                       | Obligatorio      | —                                                             |
| `dispositivo`       | string       | —             | Identificador del dispositivo desde el que se consulto          | Obligatorio      | RT-16.09 y RT-05.03                                           |

## Integracion, autoridad y auditoria

### `CONTRAPARTE`

| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                         | **Obligat.** | **Origen y nota**                                            |
|:------------------|:-------------|:--------------|:-------------------------------------------------------------------|:-----------------|:-----------------------------------------------------------------|
| **Atributo**  | **Tipo** | **Clave** | **Dominio de valores**                                         | **Obligat.** | **Origen y nota**                                            |
| `id_contraparte`  | string       | PK            | Identificador unico                                                | Obligatorio      | —                                                                |
| `tipo`            | enum         | —             | {naviera, autoridad, ferroviario, concedente, TOS, ERP, periferia} | Obligatorio      | naviera, autoridad, ferroviario, concedente, TOS, ERP, periferia |
| `nombre`          | string       | —             | Denominacion de la contraparte                                     | Obligatorio      | —                                                                |
| `estado_contrato` | enum         | —             | {confirmado, POR LEVANTAR}                                         | Obligatorio      | confirmado, POR LEVANTAR                                         |

### `CONTRATO_INTERFAZ`

| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                            | **Obligat.** | **Origen y nota**             |
|:--------------------------|:-------------|:--------------|:------------------------------------------------------|:-----------------|:----------------------------------|
| **Atributo**          | **Tipo** | **Clave** | **Dominio de valores**                            | **Obligat.** | **Origen y nota**             |
| `id_contrato`             | string       | PK            | Identificador unico                                   | Obligatorio      | —                                 |
| `version_semantica`       | string       | PK            | Identificador unico                                   | Obligatorio      | RT-05.17, el contrato se versiona |
| `id_contraparte`          | string       | FK            | Identificador de la entidad referenciada              | Obligatorio      | —                                 |
| `estandar`                | string       | —             | Denominacion del estandar sectorial de intercambio    | Obligatorio      | —                                 |
| `modo`                    | enum         | —             | {sincrono, asincrono}                                 | Obligatorio      | sincrono, asincrono               |
| `vigencia_desde`          | timestamptz  | —             | Instante con zona horaria                             | Obligatorio      | —                                 |
| `obsolescencia_anunciada` | timestamptz  | —             | Instante con zona horaria; preaviso minimo de 6 meses | Condicional      | preaviso minimo de 6 meses        |

### `MENSAJE`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                     |
|:---------------------|:-------------|:--------------|:----------------------------------------------------------|:-----------------|:------------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                     |
| `id_mensaje`         | string       | PK            | Identificador unico                                       | Obligatorio      | —                                         |
| `id_contrato`        | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | —                                         |
| `version_contrato`   | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | FK compuesta                              |
| `direccion`          | enum         | —             | {entrada, salida}                                         | Obligatorio      | entrada, salida                           |
| `instante`           | timestamptz  | —             | Instante con zona horaria                                 | Obligatorio      | —                                         |
| `id_correlacion`     | string       | —             | Identificador de correlacion comun de extremo a extremo   | Obligatorio      | comun de extremo a extremo, RT-05.19      |
| `clave_idempotencia` | string       | UK            | Clave unica que descarta el reproceso de un mismo mensaje | Obligatorio      | descarta el reproceso de un mismo mensaje |
| `estado`             | enum         | —             | {recibido, procesado, en cola, en DLQ}                    | Obligatorio      | recibido, procesado, en cola, en DLQ      |
| `reintentos`         | int          | —             | Numerico no negativo                                      | Obligatorio      | —                                         |

### `DOMINIO_INFORMACION`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                                                 | **Obligat.** | **Origen y nota**     |
|:-----------------|:-------------|:--------------|:-------------------------------------------------------------------------------------------|:-----------------|:--------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                                                 | **Obligat.** | **Origen y nota**     |
| `id_dominio`     | string       | PK            | Identificador unico                                                                        | Obligatorio      | —                         |
| `nombre`         | string       | —             | {DOM-OPS, DOM-PAT, DOM-GAT, DOM-REF, DOM-NAV, DOM-INS, DOM-FAC, DOM-ACC, DOM-EMI, DOM-INT} | Obligatorio      | los diez dominios de D-01 |

### `ZONA_OPERATIVA`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                               | **Obligat.** | **Origen y nota**                   |
|:-----------------|:-------------|:--------------|:---------------------------------------------------------|:-----------------|:----------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                               | **Obligat.** | **Origen y nota**                   |
| `id_zona`        | string       | PK            | Identificador unico                                      | Obligatorio      | —                                       |
| `nombre`         | string       | —             | VACIO DECLARADO: por nombrar en conjunto con la Celula 3 | Obligatorio      | POR NOMBRAR en conjunto con la Celula 3 |

### `FASE_TRANSICION`

| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                 | **Obligat.** | **Origen y nota**                                    |
|:-----------------|:-------------|:--------------|:-----------------------------------------------------------|:-----------------|:---------------------------------------------------------|
| **Atributo** | **Tipo** | **Clave** | **Dominio de valores**                                 | **Obligat.** | **Origen y nota**                                    |
| `id_fase`        | string       | PK            | Identificador unico                                        | Obligatorio      | —                                                        |
| `nombre`         | enum         | —             | {previo al corte, validacion paralela, posterior al corte} | Obligatorio      | previo al corte, validacion paralela, posterior al corte |

### `ASIGNACION_AUTORIDAD`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                                  | **Obligat.** | **Origen y nota**              |
|:-----------------------|:-------------|:--------------|:------------------------------------------------------------|:-----------------|:-----------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                                  | **Obligat.** | **Origen y nota**              |
| `id_asignacion`        | string       | PK            | Identificador unico                                         | Obligatorio      | —                                  |
| `id_dominio`           | string       | FK,UK         | Identificador de la entidad referenciada                    | Obligatorio      | —                                  |
| `id_zona`              | string       | FK,UK         | Identificador de la entidad referenciada                    | Obligatorio      | —                                  |
| `id_fase`              | string       | FK,UK         | Identificador de la entidad referenciada                    | Obligatorio      | —                                  |
| `vigencia_desde`       | timestamptz  | UK            | Instante con zona horaria                                   | Obligatorio      | la terna es unica en cada instante |
| `sistema_autoritativo` | enum         | —             | {TOS 2012, solucion}                                        | Obligatorio      | TOS 2012, solucion                 |
| `vigencia_hasta`       | timestamptz  | —             | Instante con zona horaria; nulo mientras la asignacion rige | Condicional      | —                                  |

### `TRANSFERENCIA_AUTORIDAD`

| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                         |
|:---------------------|:-------------|:--------------|:----------------------------------------------------------------|:-----------------|:----------------------------------------------|
| **Atributo**     | **Tipo** | **Clave** | **Dominio de valores**                                      | **Obligat.** | **Origen y nota**                         |
| `id_transferencia`   | string       | PK            | Identificador unico                                             | Obligatorio      | —                                             |
| `id_visita`          | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | ref. D-02.VISITA                              |
| `id_asignacion`      | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                             |
| `zona_origen`        | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                             |
| `zona_destino`       | string       | FK            | Identificador de la entidad referenciada                        | Obligatorio      | —                                             |
| `clave_idempotencia` | string       | UK            | Clave unica que impide aplicar dos veces la misma transferencia | Obligatorio      | —                                             |
| `numero_secuencia`   | int          | —             | Numerico no negativo                                            | Obligatorio      | ordena las transferencias de una misma visita |
| `estado`             | enum         | —             | {emitido, confirmado, fallido}                                  | Obligatorio      | emitido, confirmado, fallido                  |
| `instante`           | timestamptz  | —             | Instante con zona horaria                                       | Obligatorio      | —                                             |

### `DIVERGENCIA_CONCILIACION`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
|:-----------------------|:-------------|:--------------|:----------------------------------------------------------|:-----------------|:--------------------------------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**                                | **Obligat.** | **Origen y nota**                                   |
| `id_divergencia`       | string       | PK            | Identificador unico                                       | Obligatorio      | —                                                       |
| `universo`             | enum         | —             | {inventario, movimientos, gate, hechos}                   | Obligatorio      | inventario, movimientos, gate, hechos                   |
| `id_turno_operacional` | string       | FK            | Identificador de la entidad referenciada                  | Obligatorio      | ref. D-07.TURNO_OPERACIONAL                             |
| `clasificacion`        | enum         | —             | {desfase, nuevo correcto, nuevo incorrecto, no explicada} | Obligatorio      | desfase, nuevo correcto, nuevo incorrecto, no explicada |
| `ventana_horas`        | int          | —             | Horas                                                     | Obligatorio      | 48 para posicion, 24 para gate                          |
| `estado`               | enum         | —             | {abierta, explicada, cerrada}                             | Obligatorio      | abierta, explicada, cerrada                             |
| `instante_deteccion`   | timestamptz  | —             | Instante con zona horaria                                 | Obligatorio      | —                                                       |

### `VERIFICACION_FISICA`

| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**             |
|:-----------------------|:-------------|:--------------|:-----------------------------------------|:-----------------|:----------------------------------|
| **Atributo**       | **Tipo** | **Clave** | **Dominio de valores**               | **Obligat.** | **Origen y nota**             |
| `id_verificacion`      | string       | PK            | Identificador unico                      | Obligatorio      | —                                 |
| `id_divergencia`       | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | —                                 |
| `id_bloque`            | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-02.BLOQUE                  |
| `id_turno_operacional` | string       | FK            | Identificador de la entidad referenciada | Obligatorio      | ref. D-07.TURNO_OPERACIONAL       |
| `resultado`            | enum         | —             | {confirma, corrige, no concluyente}      | Obligatorio      | confirma, corrige, no concluyente |
| `instante`             | timestamptz  | —             | Instante con zona horaria                | Obligatorio      | —                                 |

### `REGISTRO_AUDITORIA`

| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**                   |
|:------------------------|:-------------|:--------------|:--------------------------------------------------------|:-----------------|:----------------------------------------|
| **Atributo**        | **Tipo** | **Clave** | **Dominio de valores**                              | **Obligat.** | **Origen y nota**                   |
| `id_registro`           | string       | PK            | Identificador unico                                     | Obligatorio      | —                                       |
| `entidad_afectada`      | string       | —             | Nombre de la entidad del modelo conceptual              | Obligatorio      | —                                       |
| `id_objeto_afectado`    | string       | —             | Identificador del objeto alterado                       | Obligatorio      | —                                       |
| `operacion`             | enum         | —             | {alta, modificacion, baja, consulta}                    | Obligatorio      | alta, modificacion, baja, consulta      |
| `id_persona`            | string       | FK            | Identificador de la entidad referenciada                | Obligatorio      | ref. D-07.PERSONA                       |
| `instante`              | timestamptz  | —             | Instante con zona horaria                               | Obligatorio      | —                                       |
| `dispositivo`           | string       | —             | Identificador del dispositivo de origen de la operacion | Obligatorio      | —                                       |
| `valores_anteriores`    | string       | —             | Documento estructurado con el estado previo             | Condicional      | —                                       |
| `valores_posteriores`   | string       | —             | Documento estructurado con el estado resultante         | Condicional      | —                                       |
| `sello_inalterabilidad` | string       | —             | Resumen criptografico encadenado al registro previo     | Obligatorio      | encadenado al registro previo, RT-16.07 |
