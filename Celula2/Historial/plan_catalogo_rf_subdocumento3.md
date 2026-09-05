# Plan de trabajo — Catálogo de Requerimientos Funcionales
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Responsables:** Isidora Cisternas, Rodolfo Fernández
> **Entregable objetivo:** catálogo de requerimientos funcionales del Subdocumento 3
> **Estado:** plan aprobado por la célula. Fase 0 cerrada; Fases 1 a 5 pendientes de ejecución.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## 1. Encuadre
 
**La solución ya está decidida en lo sustancial.** La Decisión N° 1 fijó la estrategia frente al sistema de operación de 2012 —envolver con capa anticorrupción y sustituir por dominios, en dos etapas— y las Decisiones N° 2 a 20 fijaron el comportamiento de casi todos los procesos.
 
De ahí se sigue la regla que gobierna todo este trabajo:
 
> El catálogo funcional no es donde se inventa la solución. Es **donde las decisiones ya tomadas se vuelven verificables**. Ningún requerimiento funcional puede contradecir una decisión ya registrada.
 
Lo que sí falta antes de redactar es dominar el problema de forma **enumerable**, para poder demostrar cobertura ante la Comisión y no descubrir vacíos al final.
 
### Estado de los entregables de la célula
 
| Producto exigido (CP, Cap. 17.1 y Subdoc. 3) | Estado |
|---|---|
| Registro de supuestos — 20 decisiones del numeral 16.1 | Completo (Decisión 1 en registro propio + Decisiones 2 a 20 + supuestos metodológicos A–L) |
| Catálogo de requerimientos **no** funcionales | Completo — 77 RNF en las 9 categorías del Cap. 17.1 |
| **Catálogo de requerimientos funcionales** | **Objeto de este plan** |
| Registro de reglas de negocio | Pendiente |
| Matriz de trazabilidad | Pendiente |
| Formulario T-12 (374 códigos RT) | Pendiente |
| Registro de vacíos y consultas | Pendiente como registro formal |
| Narrativa del Subdocumento 3 (3.1 a 3.10) | Pendiente |
 
---
 
## 2. Fase 0 — Reglas del catálogo (cerradas)
 
Decididas por la célula antes de redactar. No se modifican durante la ejecución.
 
### 2.1 Criterio de clasificación funcional / no funcional
 
El CP, Cap. 17.2 deja casos limítrofes deliberadamente sin resolver y advierte que evaluará **la consistencia del criterio declarado**, no una clasificación preestablecida. Criterio adoptado:
 
- **Es funcional** si describe un comportamiento observable que produce un resultado.
- **Es no funcional** si califica *cómo* debe comportarse algo que ya está descrito en otra parte.
Ejemplo: «la solución generará una alarma cuando la temperatura se desvíe» es RF; «la alarma no superará 5 minutos» es RNF y ya existe como RNF-DES-04. **Nunca duplicar un umbral que ya vive en el catálogo de RNF: referenciarlo.**
 
### 2.2 Ficha del requisito — ocho campos
 
Siete los exige el CP, Cap. 17.1. El octavo lo exige aguas abajo la matriz de trazabilidad del mismo capítulo, que lleva «criterio de aceptación» como columna.
 
| Campo | Contenido |
|---|---|
| Identificador | `RF-<DOM>-##` |
| Descripción verificable | Una sola conducta comprobable |
| Actor | Quién ejecuta o recibe |
| Precondición | Estado necesario para que aplique |
| Resultado esperado | Salida observable |
| Prioridad | Crítica / Alta / Media |
| Origen exacto | Documento, capítulo y código o página |
| Criterio de aceptación | Prueba concreta que lo valida |
 
### 2.3 Convención de redacción
 
- Sujeto explícito: **la solución** o el actor. Nunca sujeto tácito.
- Obligatorio: **«deberá» + infinitivo**. Equivale al *shall* normativo de IEEE 830 e ISO/IEC/IEEE 29148, y es futuro simple.
- Deseable u opcional: **«podrá»**. No mezclar ambos en un mismo requisito.
- **Voz activa siempre.** Prohibido «se registrará», «se documentarán», «será validado».
- Términos clave en **negrita**.
- Flujo medible: entrada → proceso → salida.
- Prohibidas las palabras subjetivas: adecuado, óptimo, robusto, amigable, eficiente, rápido, seguro sin métrica, fácil, moderno.
> **Nota para el catálogo de RNF.** Los 77 RNF conviven con tres construcciones distintas: «deberán alcanzar» (RNF-DIS-01), futuro simple directo «cumplirá» (RNF-CUM-01) y voz pasiva «se documentarán» (RNF-POR-02). La forma mayoritaria y la estándar de la disciplina es «deberá», que es la adoptada aquí. Queda como normalización menor —no reescritura— alinear las filas en pasiva del catálogo de RNF.
 
### 2.4 Identificadores y dominios
 
`RF-<DOM>-##`, en espejo del `RNF-<CAT>-##` ya definido. El Supuesto F del registro de supuestos pide expresamente que la convención se alinee con la matriz de trazabilidad.
 
| Código | Dominio | Etapa |
|---|---|---|
| `RF-GAT` | Gate: citas, validación documental, reconocimiento, pesaje, instrucción de destino | 1 |
| `RF-PAT` | Patio: posición, movimientos, asignación de ubicación, remociones | 1 |
| `RF-CON` | Convivencia con el sistema de 2012: fachada, escritura dual, conciliación, reversión | 1 |
| `RF-REF` | Patio refrigerado: telemetría, alarmas, escalamiento, registro continuo | 1 |
| `RF-ACC` | Identidad, habilitación de eventuales, acceso y conteo en emergencia | 1 |
| `RF-OPD` | Operación desconectada y sincronización | 1 |
| `RF-NAV` | Nave: ventana de atraque, estiba, planificación, productividad | 2 |
| `RF-FAC` | Hechos facturables y su evidencia | 2 |
| `RF-INT` | Integraciones: mensajería con navieras, autoridades, ERP | 2 |
| `RF-POR` | Portal y autoservicio de clientes | 2 |
| `RF-INS` | Inspecciones y coordinación con autoridades | por definir |
| `RF-EMI` | Emisiones y consumo energético por equipo | 2 |
 
### 2.5 Escala de prioridad
 
La misma declarada en el Supuesto E del registro de supuestos. No se crea una segunda escala.
 
- **Crítica** — restricción no negociable o consecuencia contractual severa.
- **Alta** — obligatorio transversal con peso técnico real.
- **Media** — declarativo o deseable-adyacente.
### 2.6 Granularidad y volumen objetivo
 
Regla de corte: **un requisito por comportamiento verificable de forma independiente.** Si el criterio de aceptación necesita dos pruebas distintas, son dos requisitos.
 
Volumen estimado: **100 a 120 requerimientos funcionales**, proporcionado a los 77 RNF existentes.
 
---
 
## 3. Fase 1 — Barrido de fuentes
 
Objetivo: enumerar las fuentes de extracción para poder demostrar que ninguna quedó fuera. Doce fuentes, todas localizables.
 
| # | Fuente | Qué aporta | Volumen |
|---|---|---|---|
| 1 | CP, Cap. 4 — Operación actual (pp. 9-12) | 7 procesos reales: ciclo de nave, patio, patio refrigerado, gate/documentación/pesaje, inspecciones, facturación, acceso y nombrada | 7 procesos |
| 2 | CP, Cap. 7 — Línea base (pp. 14-15) | 19 indicadores. Cada uno debe tener al menos un RF que lo mueva, o se declara por qué no | 19 indicadores |
| 3 | CP, Cap. 18 — Criterios de aceptación (pp. 40-41) | Los 22 resultados por los que el mandante juzgará el éxito. Prueba de fuego de cobertura | 22 criterios |
| 4 | CP, Cap. 16.1 — Las 20 decisiones, ya resueltas | Comportamiento fijado que hay que volver verificable | 20 decisiones |
| 5 | CP, Cap. 10 — Restricciones no negociables (pp. 22-23) | Varias generan comportamiento funcional, no solo umbrales | 14 restricciones |
| 6 | CP, Cap. 9 — Expectativas de negocio (pp. 21-22) | Los resultados esperados en palabras del mandante | 10 expectativas |
| 7 | CP, Cap. 5 — Sistemas existentes (pp. 12-13) y RT-17.06 | Qué se integra, qué se reemplaza, qué es solo lectura | 7 sistemas |
| 8 | CP, Cap. 15 — Parámetros del caso | Códigos funcionales puros: RT-16.30 portal, RT-17.01 aplicación móvil, RT-12.12 usuarios externos, RT-16.14 firma | ~8 códigos |
| 9 | BTT — los 374 códigos RT | Filtrar los que exigen comportamiento. Alimenta directamente el T-12 | 374 a inventariar |
| 10 | CP, Cap. 8 y 10.2 — Entrevistas y tensiones | **No son requisitos literales**: contienen opiniones y tensiones | 9 tensiones |
| 11 | CP, Cap. 12 — Marco normativo | ISPS, aduana, VGM, IMDG, fitosanitario, datos personales. Cada norma necesita el control concreto que la satisface | 13 materias |
| 12 | CP, Cap. 13 — Exclusiones (pp. 23-24) | Definen la frontera y generan RF de **interfaz** con lo excluido | 9 exclusiones |
 
**Fuente 13, ya redactada.** El registro de la Decisión N° 1, en su sección de requerimientos que introduce la decisión, enumera seis requisitos que deben incorporarse al catálogo del Subdocumento 3: capa anticorrupción con contrato de interfaz versionado, escritura dual con apagado controlado, conciliación automática, reversión por dominio, verificación física del inventario por barrido de bloques, y observabilidad de convivencia.
 
---
 
## 4. Fase 2 — Matriz de cobertura, antes de redactar
 
### Por qué antes y no después
 
Redactar leyendo el caso de principio a fin produce requisitos para todo lo que el caso **describe**, sin forma de demostrar que se cubrió lo que el caso **exige**. Y las exigencias están escritas en un lugar distinto de las descripciones: los 22 criterios de aceptación viven en el Cap. 18, no en los capítulos que describen la operación.
 
La matriz se construye **antes** de redactar y sus filas son las exigencias, no las fuentes.
 
### Los tres cruces
 
**Cruce A — los 22 criterios de aceptación contra los 12 dominios.** Una fila por criterio; la columna indica qué dominio llevará el requisito que lo satisface. Un criterio sin dominio es un vacío en la lista de dominios; un dominio sin criterio es un dominio posiblemente sobredimensionado.
 
| Criterio (CP, Cap. 18) | Dominio | Estado |
|---|---|---|
| 4 — Reconocimiento automático del contenedor en gate | `RF-GAT` | Cubierto; Decisión N° 2 fija el método |
| 8 — Reducción medible de remociones | `RF-PAT` | Cubierto; Decisión N° 3 fija quién asigna |
| **10 — Contenedor de inspección disponible a tiempo** | `RF-INS` | **Vacío: ninguna de las 20 decisiones cubre inspecciones** |
| 22 — Continuidad de planificación tras la jubilación | `RF-NAV` | Cubierto; Decisiones N° 4 y 5, más el frente de captura de conocimiento de la Decisión N° 1 |
 
**Cruce B — los 19 indicadores de línea base contra los RF que los mueven.** Cada número del estado actual —78 minutos de estadía, 3,2 km de fila, 22 % de documentación defectuosa, 18 % de remociones, 3,1 % mal ubicados, 40 minutos de búsqueda, 28 % de inspecciones atrasadas, 4,7 % de facturas objetadas, 62 % de objeciones aceptadas— debe tener al menos un requisito que plausiblemente lo mueva, o se declara explícitamente por qué no. Ataca el fallo más común de un catálogo: describir un sistema impecable que no toca los problemas que el cliente tiene.
 
**Cruce C — las 20 decisiones contra los RF que las materializan.** Una decisión sin ningún RF fue decorativa. Un RF que contradice una decisión se detecta con cinco requisitos escritos y no con cien.
 
### Productos de la fase
 
1. La tabla de los tres cruces.
2. La **lista de vacíos** a resolver antes de redactar.
La tabla es entregable en sí misma: va al informe como evidencia de cobertura, y es la semilla de la matriz de trazabilidad de la Fase 5, porque deja construida la columna «origen».
 
### Vacíos ya detectados
 
| Vacío | Descripción | Vía de resolución |
|---|---|---|
| Inspecciones de autoridad | 18.400 inspecciones al año con 28 % de atraso y criterio de aceptación N° 10 propio, sin ninguna decisión asignada entre las 20 del Cap. 16.1 | Resolver con la habilidad `registro-decision`, en formato de seis campos, antes de redactar `RF-INS` |
 
---
 
## 5. Fase 3 — Redacción por dominio
 
Orden de redacción por peso: primero los dominios de Etapa 1 que concentran criterios de aceptación, y `RF-CON` temprano porque sus requisitos ya vienen fundamentados desde la Decisión N° 1.
 
Cada requisito se redacta con la habilidad `redactor-rf-portuaria`, que fija la ficha de ocho campos, la convención de redacción, la escala de prioridad y el control IEEE 830.
 
---
 
## 6. Fase 4 — Control de calidad
 
Dos pasadas, ninguna opcional.
 
**Pasada A — IEEE 830.** Las ocho propiedades aplicadas requisito por requisito: correcto, no ambiguo, completo, consistente, clasificado por importancia o estabilidad, verificable, modificable, trazable.
 
Las dos que más fallan:
 
- **Verificable** — si el criterio de aceptación no se puede ejecutar como prueba, el requisito no sirve.
- **Consistente** — contrastar contra los otros RF, contra los 77 RNF y contra las 20 decisiones.
**Pasada B — verificación de citas.** Ejecutar la habilidad `verificar-citas-bases` sobre el catálogo completo, para contrastar cada cita normativa contra el texto real de las bases y marcar las que no se sostienen.
 
> La revisión de consistencia debe hacerla alguien —o un agente— que **no haya redactado** esos requisitos. Que el autor se autoevalúe no detecta lo que el autor da por obvio.
 
---
 
## 7. Fase 5 — Salidas derivadas
 
El catálogo deja armado:
 
- **Asignación Etapa 1 / Etapa 2** de cada requisito, insumo directo de las secciones 3.4 a 3.6 del Subdocumento 3.
- **Columnas base del Formulario T-12**: ID, descripción y componente que lo satisface.
- **Esqueleto de la matriz de trazabilidad**: origen, requerimiento y criterio de aceptación ya vienen de la ficha; faltará componente de arquitectura (Célula 3) y paquete de la EDT (Informe 2).
- **Anexo en planilla**: el catálogo migra a `TERABYTE_MATRICES_TECNICAS_INFORME_1.xlsx`, con hojas separadas para requisitos funcionales, no funcionales, supuestos, reglas de negocio, trazabilidad, consultas y T-12.
---
 
## 8. Dependencias y riesgos
 
| # | Asunto | Impacto |
|---|---|---|
| 1 | **Volumetría del CP, Cap. 14.2 incompleta en el registro de supuestos** | No bloquea los RF. Bloquea los umbrales de RNF de desempeño: RT-09.02 exige derivar concurrencia y TPS de esa volumetría. Sin la tabla, varios umbrales quedan sin fundamento derivable |
| 2 | **RNF-DIS-09 contradice el calendario de la Decisión N° 1** | El RNF fija «0 intervenciones entre el 15 de diciembre y el 30 de abril» como umbral crítico, mientras el calendario adoptado sitúa la marcha blanca de la Etapa 1 dentro de esa ventana bajo el supuesto S3. Debe armonizarse la redacción |
| 3 | **Instancias de validación que apuntan al período de consultas, ya cerrado** | RNF-SEG-10, Decisión N° 12 y Supuestos A y B remiten al período de consultas. Deben reemplazarse por instancias ejecutables |
| 4 | **Lenguaje académico en el Supuesto A** | Menciona «el profesor o la Comisión». Las instrucciones del equipo prohíben referirse al ramo o al profesor en el texto de la propuesta |
| 5 | **Decisión N° 3 deja al operador sin vía de corrección** | Su propio campo de impacto admite que el operador ejecutará una instrucción errónea sin oportunidad de corregirla. La Decisión N° 5 da esa vía al planificador, no al operador |
| 6 | **Referencias cruzadas rotas** | El registro de supuestos apunta a `RNF_Caso_Portuaria.md` y `decision_01_tos_2012_registro_final.md`; los archivos reales son `RNF.md` y `01_decision_01_tos_2012_registro_final.md` |
| 7 | **Decisiones N° 3, 14 y 15 sin verificación externa** | La N° 3 sostiene todo el dominio `RF-PAT`. El CP, Cap. 16.2 exige investigación sectorial con fuentes preferentemente primarias, académicas, normativas o de fabricante |
| 8 | **Calendario** | Fases 0 a 4 son del orden de dos días. Después del catálogo restan la narrativa del Subdocumento 3, el registro de reglas de negocio, la matriz de trazabilidad y el T-12, con entrega el 7 de septiembre de 2026 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*