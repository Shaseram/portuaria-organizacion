# Registro de Supuestos y Decisiones — versión consolidada
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo D** · **Versión 2.0 — reemplaza a `registro_supuestos_decisiones_02_20.md` y a `registro_supuestos_complemento_celula2.md`**, e incorpora los supuestos y metas declarados durante la Fase 4.
> **Autoría:** Decisiones N° 2 a 20 y supuestos A a L, Isidora Cisternas. Decisión N° 21, metas, supuestos M a P y correcciones de Fase 4, Rodolfo Fernández.
> **Exigencia:** CP, Cap. 17.1 — *«Toda decisión que el PROPONENTE tomó por el CLIENTE, con su fundamento, su impacto si resulta equivocada y la instancia en que se validará. Incluye obligatoriamente las veinte decisiones del numeral 16.1, y en particular la primera.»*
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Bloque | Contenido | Cantidad |
|---|---|---:|
| **A** | **Las decisiones del numeral 16.1, más una** — con su vinculación al catálogo | **21** |
| **B** | **Metas comprometidas** — indicadores sin referencia y umbrales propios, con su evidencia | **17** |
| **C** | **Supuestos declarados** — de calendario, de interpretación, metodológicos y de alcance | **20** |
| **D** | Notas de alcance — lo que deliberadamente no genera requerimiento | 2 |
| **E** | Estado, cambios respecto de la v1 y pendientes | — |
 
> **La Decisión N° 1 se mantiene en documento aparte.** El CP, Cap. 17.1 le da tratamiento especial —«y en particular la primera»— y su registro tiene quince secciones. Aquí se resume y se remite a `01_decision_01_tos_2012_registro_final.md`, que sigue siendo la fuente.
 
---
 
# Bloque A — Las 21 decisiones
 
Cada decisión registra los seis campos que exige el Cap. 17.1: decisión tomada, fundamento, alternativas consideradas, impacto si resulta equivocada, instancia de validación y responsable. **El responsable es Terabyte en las 21.** El detalle completo de las Decisiones N° 2 a 20 está en el bloque de fichas de esta sección; el de la N° 1, en su registro propio.
 
## A.1 Tabla maestra
 
| N° | Materia | Verificación externa | Genera RF | Dominio |
|---:|---|---|---|---|
| **1** | Estrategia frente al sistema de operación de 2012 | Literatura arbitrada · registro propio | Sí | `RF-CON` |
| 2 | Método para conocer la posición real del contenedor | Sí — DGPS/RTLS | Sí | `RF-PAT` |
| 3 | Quién decide dónde se apila cada contenedor | **No** ⚠ | Sí | `RF-PAT` |
| 4 | Autonomía de la planificación y registro de correcciones | Sí — Navis/Kaleris | Sí | `RF-NAV` |
| 5 | Incorporación de las restricciones tácitas del planificador | Parcial | Sí | `RF-PAT`, `RF-NAV` |
| 6 | Sistema de citas: obligatoriedad y penalización | Sí — LA/LB, Vancouver, Port Botany | Sí | `RF-GAT` |
| 7 | Validación documental anticipada y excepciones | Sí — APM Terminals | Sí | `RF-GAT` |
| 8 | Frecuencia de muestreo del patio refrigerado | Sí — Identec, REFCON | Sí | `RF-REF` |
| **9** | Cobertura inalámbrica del patio | Sí — HHLA, Nokia | **No** — arquitectura física | — |
| 10 | Escalamiento y confirmación de alarmas de frío | Sí — ISA-18.2 | Sí | `RF-REF` |
| 11 | Hecho que constituye evidencia facturable | Parcial | Sí | `RF-FAC` |
| 12 | Habilitación de eventuales sin biometría obligatoria | Sí — con advertencia | Sí | `RF-ACC` |
| 13 | Conteo y ubicación de personas en emergencia | Sí — mustering RFID | Sí | `RF-ACC` |
| 14 | Información al operador de grúa de muelle | **No** ⚠ | Sí | `RF-NAV` |
| 15 | Evidencia de movimiento sin confirmación del operador | **No** ⚠ | Sí | `RF-PAT`, `RF-TRA` |
| 16 | Metodología de cálculo de emisiones | Sí — ISO 14083 / GLEC | Sí | `RF-EMI` |
| 17 | Consumo energético real por equipo | Sí — Kalmar, SEA TERMINALS | Sí | `RF-EMI` |
| 18 | Mensajería estándar con navieras | Sí — SMDG, Hapag-Lloyd | Sí | `RF-INT` |
| **19** | Segregación de redes | Sí — IEC 62443 | **No** — arquitectura física | — |
| **20** | Destino de la sala de servidores | Sí — edge marítimo | **No** — arquitectura física | reflejo en `RF-OPD` |
| **21** | **Coordinación de inspecciones de autoridad** | Por analogía — Zweers et al. (2020) | Sí | `RF-INS` |
 
⚠ **Decisiones N° 3, 14 y 15 sin verificación externa propia.** La N° 3 es la más expuesta: sostiene todo el dominio `RF-PAT`. El CP, Cap. 16.2 exige investigación sectorial con fuentes preferentemente primarias, académicas, normativas o de fabricante.
 
**Decisiones N° 9, 19 y 20:** son de arquitectura física, no describen comportamiento observable y **no generan requerimiento funcional**. Corresponden al Subdocumento 4 y a la Célula 3. Ver bloque D.2.
 
## A.2 Decisión N° 1 — resumen y remisión
 
**Decisión adoptada.** Envolver el sistema de operación de 2012 detrás de una **capa de servicios anticorrupción** y sustituir sus capacidades de forma progresiva, dominio por dominio, con cuatro compromisos: fuente de verdad explícita por dominio y fase, conciliación automática con umbrales declarados, procedimiento de retorno probado por dominio, y fecha declarada de retiro del sistema legado.
 
**Declaración central.** Al vencimiento del soporte del fabricante en 2028, ningún componente del registro oficial de la operación permanece dentro del sistema de 2012.
 
**Condición de viabilidad.** Puerta de decisión anterior al hito H2 (mes 4): si el levantamiento demuestra que el sistema de 2012 no permite lectura, escritura, sincronización o conciliación suficientemente confiables, la estrategia evoluciona hacia un reemplazo integral controlado.
 
**Supuestos que aporta:** S1 a S5, recogidos en el bloque C.
**Requerimientos que introduce:** los doce de `RF-CON`.
 
> **Fuente:** `01_decision_01_tos_2012_registro_final.md`, quince secciones. Este resumen no lo reemplaza.
 
## A.3 Decisiones N° 2 a 20 — fichas
 
> Las fichas completas de las diecinueve decisiones, con sus seis campos y sus referencias citadas, están en el bloque de contenido de `registro_supuestos_decisiones_02_20.md`, cuyo texto se incorpora íntegro a este registro. Se reproduce aquí su **síntesis operativa**; el fundamento extenso y las 33 referencias se conservan en ese archivo hasta la integración final al informe.
 
| N° | Decisión adoptada |
|---:|---|
| 2 | Modelo combinado: **posicionamiento automático del equipo (DGPS o RTLS)** como fuente primaria, reforzado con **lectura óptica en puntos de paso** como verificación cruzada. Una posición se considera «conocida» cuando ambas coinciden; si discrepan, queda «por verificar» y genera tarea de verificación física |
| 3 | **«El algoritmo asigna, el operador ejecuta»**, sin paso de confirmación intermedio. Complementada por el supuesto de la vía de excepción con interlock (ver C, supuesto N) |
| 4 | **«El algoritmo propone, el planificador aprueba o corrige, y toda corrección queda registrada con su motivo»** |
| 5 | Catálogo de **condiciones dinámicas de patio**, editable por el planificador en tiempo real, que el algoritmo respeta en cada corrida |
| 6 | Sistema de citas **opcional, sin multa, con prioridad de atención** para quien cumple su cita. Evoluciona a obligatorio solo para transportistas de alto volumen recurrente, una vez validado |
| 7 | **Validación documental anticipada** por portal, con **carril de excepción** de atención diferenciada para el camión que llega sin validar, en lugar de rechazo en barrera |
| 8 | Modelo de dos capas: **muestreo local de 1 a 5 minutos**, agregación en gateway y **reporte al núcleo de 5 a 15 minutos**, más envío inmediato ante excepción |
| 9 | **Red celular privada (LTE o 5G)** como tecnología primaria de cobertura de patio, con redundancia dimensionada al peor caso de bloqueo por apilamiento y estudio de sitio periódico |
| 10 | Alarma **simultánea al operador de turno y a un supervisor de guardia**, con escalamiento automático a un tercer contacto si ninguno confirma, y registro auditable de la confirmación |
| 11 | Cada hecho facturable queda respaldado por un **evento del sistema generado en el momento en que ocurre**, validado por regla de negocio específica, sin intervención manual previa a la facturación |
| 12 | Habilitación del eventual mediante **credencial temporal vinculada a la nombrada**, sin enrolamiento biométrico, con cuatro compensadores: expiración automática, zonificación, auditoría de cada acceso y biometría voluntaria |
| 13 | Registro centralizado de **quién ingresó, bajo qué habilitación y a qué zona general**, sin geolocalización individual continua |
| 14 | **Pantalla integrada a la cabina**, con indicaciones visuales y alertas sonoras solo por seguridad, **sin botones de confirmación** para la operación rutinaria |
| 15 | **Telemetría del propio equipo** como fuente primaria de verdad del movimiento, con lectura óptica como verificación cruzada, sin confirmación activa del operador |
| 16 | **ISO 14083:2023** como norma de cuantificación, implementada mediante **GLEC Framework v3.2**, verificada por tercero acreditado bajo **ISO 14064-3** |
| 17 | Instrumentación de consumo **por equipo**: sensores de combustible en los 16 diésel y medición directa de kWh en los 2 eléctricos. **Sin prorrateo** |
| 18 | Adopción de **BAPLIE, COPRAR, COARRI y CODECO** (UN/EDIFACT, mantenidos por SMDG), con **canal puente asistido** para las navieras no integradas |
| 19 | Segregación de redes por **migración en fases**, manteniendo la videovigilancia operativa, bajo el modelo de zonas y conductos de **IEC 62443**, con aprobación previa de la autoridad marítima |
| 20 | **Traslado del componente on-premise crítico** a ubicación alejada de la atmósfera marina, reducido al mínimo que exige la operación autónoma de 72 horas, con el resto en nube |
 
## A.4 Decisión N° 21 — Coordinación de inspecciones de autoridad
 
> **Vacío no listado en el numeral 16.1**, identificado por Célula 2. El CP declara que esa lista no es exhaustiva y que *«el PROPONENTE que identifique vacíos no listados aquí será evaluado favorablemente por ello»*. **Clase de profundidad: ficha.**
 
**Decisión.** Terabyte adopta un módulo de coordinación de inspecciones que **convierte la cita de inspección en una tarea programada del patio, con la remoción anticipada incluida**, en lugar de tratarla como una solicitud que se resuelve cuando el inspector ya está en el recinto. Opera en cuatro movimientos: recepción normalizada por el canal que cada autoridad tenga; reserva de disponibilidad con programación anticipada de remociones; visibilidad para el inspector como persona usuaria externa; y cierre con acta firmada y hecho facturable.
 
> **El desplazamiento conceptual es el punto.** Hoy la inspección compite por recursos de patio en el momento en que se necesita. Con esta decisión, compite en el momento en que se agenda, que es cuando todavía hay margen.
 
**Fundamento.** CP, Cap. 4.7: el 28 % de las inspecciones se atrasa «porque el contenedor no se ubicó a tiempo» o «porque estaba abajo de otros tres **y la remoción no se programó**» — la segunda mitad de esa frase es lo que la decisión ataca · CP, Cap. 4.7: «a la hora acordada, el contenedor debe estar en la zona de inspección, **abierto**, con el inspector presente» · CP, Cap. 18, criterio 10 · CP, num. 17.4 punto 9, que obliga a resolver también el escenario sin interfaz · CP, Cap. 11, exclusión 7 · CP, Cap. 5 (el control de inspecciones debe dejar de vivir en correo y planillas) · CP, Cap. 15, RT-12.12 (los inspectores son personas usuarias externas) · CP, Cap. 15, RT-16.14 (acta con firma) · CP, Cap. 4.8 (la inspección es hecho facturable) · CP, Anexo B.1 (ventana 08:00 a 18:00).
 
**Verificación externa.** El mecanismo está validado **por analogía**, no directamente: no existe literatura arbitrada sobre programación anticipada de remociones para inspecciones de autoridad. Lo sostienen Zweers, Bhulai y van der Mei (2020), *Computers & Operations Research*, que formalizan el preprocesamiento en tiempo ocioso de grúa, y Azab y Morita (2022), *Transportation Research Part E*, sobre coordinación de citas con manejo de contenedores en un terminal japonés real.
 
**Alternativas descartadas.** Integración electrónica con las tres autoridades desde el inicio —el caso no declara si existe interfaz, y la exclusión 7 la condiciona a que exista—; mantener la coordinación por correo y teléfono —CP, Cap. 5 lo prohíbe y no ataca la causa—; pre-posicionar contenedores con probabilidad de selección —consume capacidad de patio al 90 % de ocupación y depende de una predicción que ninguna base respalda—; tratar la inspección como un retiro más —es el comportamiento actual, y una inspección tiene hora comprometida con un tercero con potestad.
 
**Impacto si resulta equivocada.** Si el plazo de aviso de alguna autoridad resulta menor que el tiempo necesario para la remoción, el atraso persiste por causa distinta. La solución debería degradar hacia una regla de prioridad —la remoción de inspección desplaza a la de retiro— cuyo costo operacional habría que declarar. Riesgo secundario: si el acta firmada no es aceptada por la autoridad como sustituto de su propio registro, la solución produce evidencia sin valor externo.
 
**Instancia de validación.** Plazo de aviso y existencia de interfaz de cada autoridad: levantamiento de los meses 1 a 4 (supuesto O). Aceptación del acta firmada: con cada autoridad, antes del cierre de desarrollo de la Etapa 2. Efectividad de la programación anticipada: marcha blanca.
 
**Vinculación.** Dominio `RF-INS` completo · `RF-PAT-11` · `RF-INT-10` · `RF-POR-06` · meta 11.
 
---
 
# Bloque B — Las 17 metas comprometidas
 
**Fundamento de la obligación.** CP, Cap. 18: *«El PROPONENTE deberá comprometerse con ellos, proponer la meta cuando este documento no la fije, indicar en qué momento del cronograma se alcanzará cada uno y cómo se medirá.»*
 
**Regla aplicada.** Cada meta declara **valor, momento y método de derivación**. Donde el indicador no es accionable por la solución, se declara expresamente que **no se compromete meta**, con su razón. Las metas fundadas en evidencia publicada citan su fuente, **incluida la que les es adversa**.
 
## B.1 Metas sobre los once indicadores sin referencia del CP, 7.2
 
| # | Indicador | Base | **Meta** | Momento | Derivación y evidencia |
|---:|---|---|---|---|---|
| 1 | Remociones sobre movimientos de patio | 18 % | **≤ 14 %** | Cierre Etapa 2 | Reducción relativa de ~22 %, **conservadora** frente a la evidencia: Bütün et al. (2026) reportan ~74 % de reducción de movimientos improductivos en el Vigo Container Terminal, terminal convencional; Kim y Yi (2021) reportan 98 % de reducción de remociones por retiro sobre 200.000 contenedores en Busan. **Advertencia adversa:** Zając (2026) documenta que **bajo carga alta la regla simple FIFO superó a las estrategias sofisticadas**, y este patio opera al 90 % en peak; Saurí y Martín (2011) muestran que no existe estrategia dominante universal. **Además, la reducción depende de que exista información anticipada de retiro**, lo que ata esta meta al éxito del sistema de citas. **La meta se compromete medida fuera del peak estacional**, con el desempeño en peak reportado por separado. **La línea base de 18 % no es contrastable contra literatura publicada**: el sector mide remociones *por retiro*, no como porcentaje de movimientos |
| 2 | Contenedores registrados donde no están | 3,1 % | **≤ 0,5 %** | Cierre marcha blanca Etapa 1 | **Estimación propia**, alineada al umbral de detención de conciliación de la Decisión N° 1. Bajo la Decisión N° 2 el indicador cambia de naturaleza: mide posiciones «por verificar» no resueltas dentro del turno. **Advertencia adversa:** Dahiya et al. (2026) documentan que RTK a 3 cm sigue siendo insuficiente porque el error proviene de la **orientación** del contenedor, no del posicionamiento — **la meta no la alcanza el DGPS solo**, sino la verificación cruzada de `RF-PAT-02` y el ciclo de `RF-PAT-04`. Götting KG (2013) documenta ±30 cm en el mejor caso sobre RTG. **Ninguna fuente cuantifica el porcentaje de contenedores mal ubicados en un patio**: ni la base ni la meta son contrastables |
| 3 | Tiempo de búsqueda física | 40 min | **Cero como proceso normal**; residual ≤ 0,5 % de retiros en ≤ 15 min | Cierre Etapa 1 | CP, Cap. 18 criterio 9 exige «sin búsquedas físicas». El residual coincide con la meta 2; los 15 minutos corresponden a una verificación dirigida a posición candidata, no a un barrido |
| 4 | Ocupación del patio en peak | 90 % | **No se compromete meta** | — | No accionable por la solución: depende del volumen comercial y de la superficie, y no hay ampliación comprometida (CP, Cap. 14). Se usa como **parámetro de dimensionamiento** del peak coincidente |
| 5 | Equipos con instrumentación | 12 de 18 | **74 de 74**; 88 en proyección | Cierre desarrollo Etapa 1 | **Corregida al alza.** El universo real no son 18 grúas de patio sino **18 grúas + 42 tractocamiones + 14 equipos de manipulación pesada** (CP, 14.1). Condición de la Decisión N° 15: si la telemetría es fuente primaria de verdad, un equipo sin instrumentar es un equipo cuyos movimientos no existen para el sistema |
| 6 | Intervalo de control de refrigerados | 4 h, ronda a pie | **≤ 5 min** | Cierre desarrollo Etapa 1 | Consecuencia de la Decisión N° 8 y de CP, Cap. 15, RT-05.29. **Justificación corregida:** el umbral se mantiene porque RT-05.29 lo exige, **pero deja de presentarse como el beneficio**. El West of England P&I Club fija el estándar asegurador en revisión **cada 6 horas**, de modo que la ronda de 4 h ya lo supera; Kan et al. (2020) muestran que el ascenso térmico se mide en horas. **El beneficio comprometido es cobertura sin ventana ciega y evidencia entregable**, no la velocidad de detección |
| 7 | Tomas con instrumentación remota | 0 de 2.400 | **2.400 de 2.400**; 2.900 en proyección | Cierre desarrollo Etapa 1 | Cobertura total: una toma sin instrumentar reproduce el modo de falla del 18 de febrero |
| 8 | Tableros con alarma remota | 0 de 26 | **26 de 26**; 32 en proyección | Cierre desarrollo Etapa 1 | El evento del 18 de febrero fue la falla de **un tablero completo**, no de una toma |
| 9 | Registro continuo de temperatura | inexistente | **100 %** de los refrigerados, retención 5 años | Cierre desarrollo Etapa 1 | Cobertura derivada de las metas 7 y 8; retención fijada por CP, Cap. 15, RT-05.10 |
| 10 | Pérdida del evento del 18 de febrero | US$ 620.000 | **No se compromete meta** | — | Es un hecho ocurrido, no una serie. Su prevención se mide por las metas 6 a 9 y por RNF-DES-04 y RNF-DIS-08 |
| 11 | Inspecciones atrasadas | 28 % | **≤ 12 %, condicionada** | Cierre Etapa 2 | **Corregida a la baja desde ≤ 8 %.** No existe evidencia arbitrada que mida este indicador ni el mecanismo propuesto. **Evidencia adversa:** Klar et al. (2024) documentan que en la práctica las citas se posponen para minimizar remociones, y que cumplir la agenda **consume capacidad de grúa que compite con la meta 1**; Hoffmann et al. (2021) y Nguvumali et al. (2025) muestran que el determinante principal suele ser la coordinación con la autoridad, **fuera del control del terminal**. Condicionada a que el plazo de aviso de cada autoridad resulte compatible con el tiempo de remoción |
 
## B.2 Metas sobre umbrales propios comprometidos en la Fase 4
 
| # | Materia | **Meta** | Requerimiento | Derivación |
|---:|---|---|---|---|
| 12 | Tasa de reconocimiento óptico del código de contenedor | **≥ 98 %** | `RF-GAT-05` | El criterio de aceptación 4 exige reconocimiento «sin digitación». Comprometer 100 % con placa sucia y luz variable sería indemostrable en la recepción. El 2 % residual se resuelve por procedimiento de excepción sin digitar el código completo |
| 13 | Diferencial del carril de excepción | **≥ 50 % más lento** que el carril validado | `RF-GAT-04` | La Decisión N° 7 advierte que si el carril de excepción no es «claramente peor», se elimina el incentivo para validar antes. El 50 % es la magnitud mínima que un transportista percibe como diferencia de trato |
| 14 | Diferencial de prioridad por cita cumplida | **≥ 30 % más rápido** | `RF-GAT-02` | La adopción decide el resultado del sistema de citas: Giuliano y O'Brien (2007) documentan efecto nulo en Los Ángeles y Long Beach con adopción de 5 a 30 %. Un incentivo imperceptible no genera adopción |
| 15 | Instrucciones de embarque digitadas | **≤ 5 %** al cierre de Etapa 2 | `RF-INT-02` | Línea base 41 %, referencia del CP cero. El residual se atribuye exclusivamente a navieras en canal puente |
| 16 | Reconciliación de consumo de combustible | **± 3 % en 3 meses** | `RF-EMI-01` | Tolerancia habitual de reconciliación de flujómetros. Sin período ni tolerancia el criterio era inejecutable |
| 17 | Error del procedimiento de barrido de inventario | **≤ 0,5 %** | `RF-CON-09` | Alineado a la meta 2: un barrido menos exacto que el umbral que debe verificar no sirve |
 
> **Advertencia de método.** Las metas **1, 2 y 11** descansan parcialmente en información que las bases no entregan o que la literatura no respalda, y las tres lo declaran en su propia fila. Las metas **6 y 11** cambiaron respecto de su versión original tras el contraste con evidencia publicada. Las otras doce se derivan de decisiones ya adoptadas o de umbrales fijados en las bases.
 
---
 
# Bloque C — Los 20 supuestos declarados
 
## C.1 Supuestos de calendario y de la Decisión N° 1
 
| ID | Supuesto | Impacto si resulta equivocado | Validación |
|---|---|---|---|
| **S1** | El mes 1 del contrato corresponde a **febrero de 2027** | Se desplaza todo el calendario; si el desplazamiento supera cuatro meses, alguna puesta en producción entra en congelamiento | Firma del contrato |
| **S2** | Es factible **interceptar y escribir** hacia el sistema de 2012 desde una capa externa | Se anula la reversibilidad y debe replantearse la Decisión N° 1 completa | **Puerta de decisión del mes 4** |
| **S3** | La restricción no negociable N° 9 alcanza solo al **paso a producción** y no a la marcha blanca | El calendario contractual del BA, Art. 17° resulta inejecutable en cualquier anclaje | Consulta C1 · levantamiento |
| **S4** | El patio admite **segmentación en bloques operativos** para el barrido de verificación | Debe replantearse el método de verificación física del inventario | Levantamiento |
| **S5** | El soporte del fabricante **puede vencer tan pronto como el 01-01-2028**; el plan se evalúa contra ese escenario | Existe una ventana de exposición **estructural del calendario contractual**, común a las tres opciones, declarada y mitigada | Consulta C2 |
 
> S5 es deliberadamente conservador. BA, Art. 5.3 y 5.4 obligan a adoptar la interpretación más exigente ante ambigüedad, y apoyar el plan en la lectura favorable es lo que las bases prohíben.
 
## C.2 Supuestos metodológicos del catálogo de RNF
 
| ID | Supuesto | Validación |
|---|---|---|
| **A** | La operación desconectada de 72 h y las 8 h de terminales se clasifican como **Disponibilidad**, no como requisito funcional ni como decisión de arquitectura | Caso limítrofe que el CP, Cap. 17.2 deja abierto. Ver los requerimientos en revisión, bloque E |
| **B** | «Sin rediseño» se interpreta como **ausencia de valores de sitios y bloques codificados en duro**, verificable por revisión de arquitectura y ADR | Levantamiento |
| **C** | Las restricciones cualitativas —sin ventana de detención, prohibición de intervenir— se traducen en umbral **«0 ventanas/intervenciones»** | Confirmar con arquitectura al definir la estrategia de despliegue sin interrupción |
| **D** | Umbral **«100 % de alarmas con confirmación registrada»** para el canal redundante | Revisar con el jefe de operaciones la dotación real del turno de madrugada |
| **E** | Escala de prioridad propia **Crítica / Alta / Media**, distinta de «Obligatorio/Deseable/Según caso» de las bases | Revisión cruzada del equipo. **Aplicada también al catálogo de RF** |
| **F** | Convención de identificadores **`RNF-<CAT>-##`** | Alineada con `RF-<DOM>-##` en el catálogo funcional |
| **G** | Se asume la existencia de **herramienta de monitoreo (APM) y tablero operacional** como método de verificación | Alinear con la arquitectura del Subdocumento 4 |
| **H** | Umbral **«0 rutas cruzadas no autorizadas»** para la segregación efectiva de redes | Confirmar con arquitectura la métrica más defendible |
| **I** | Umbral **«0 interfaces que incrementen el riesgo»**, validado por acta de conformidad de prevención | Definir con prevención qué evidencia constituye conformidad — **checklist ergonómico por puesto de terreno**, ya incorporado a los criterios de `RF-PAT-09` y `RF-NAV-11` |
| **J** | Se retiró de RNF-USA-07 la afirmación causal sobre reducción del 22 % de documentación defectuosa, por no ser un hecho declarado por el mandante | Si el equipo quiere comprometer esa meta, debe fundamentarla aparte |
| **K** | No se declara **dotación mínima de técnicos por turno** para la presencia en terreno | Definir con operaciones antes de la entrega final |
| **L** | Mapeo interpretativo de capítulos del BTT a las categorías **Operabilidad** y **Mantenibilidad**, que el BTT no nombra como tales | Confirmar con Célula 3 |
 
## C.3 Supuestos de interpretación normativa
 
### Supuesto M — Correspondencia de códigos RT entre el BTT y el Capítulo 15 del CP
 
**El vacío.** El BTT y el Cap. 15 del CP usan **los mismos códigos `RT-CC.NN` para materias distintas**: `RT-05.10` es «catálogo de linaje» (Deseable) en el BTT y «retención de datos» en el CP; `RT-16.14` es «motor de reglas» (Deseable) en el BTT y «firma electrónica» en el CP; lo mismo con `RT-16.21`, `RT-16.30` y `RT-21.06`.
 
**Decisión.** Terabyte interpreta que el Cap. 15 del CP **no renumera** los códigos del BTT sino que fija los parámetros del caso para requisitos «Según caso», y que cuando un mismo código aparece en ambos documentos con materias distintas, **ambas obligaciones son exigibles y acumulativas**, no alternativas.
 
**Fundamento.** BA, Art. 5.3 y 5.4 obligan a adoptar la interpretación más exigente ante ambigüedad. La lectura acumulativa obliga a cumplir la conducta transversal del BTT **y** el parámetro del caso.
 
**Alternativas.** Interpretar que el CP renumera y sustituye, lo que dejaría sin cumplir obligaciones transversales vigentes; o que solo rige el BTT, lo que ignoraría los parámetros del caso.
 
**Impacto si resulta equivocada.** Ninguno adverso: el error sería **por exceso de cumplimiento**.
 
**Validación.** Reunión de aclaración con la Contraparte Técnica al inicio del contrato, o Acta de Respuestas a Consultas si el CLIENTE emite aclaración de oficio (BA, Art. 44.1).
 
**Consecuencia operativa.** Regla de cita adoptada en todo el catálogo: **todo código se cita con su documento de origen** —«BTT, RT-XX.YY» o «CP, Cap. 15, RT-XX.YY»—. El parámetro del caso se cita al CP; la obligación transversal, al BTT.
 
### Supuesto N — «Acta de inspección conjunta»
 
**El vacío.** CP, Cap. 15, RT-16.14 exige firma electrónica en «las actas de inspección conjunta». **La expresión no está definida en ninguna parte del caso.** Es su única mención.
 
**Lecturas posibles.** (1) Acta de una inspección en que concurre **más de una autoridad** sobre el mismo contenedor. (2) Acta de una inspección en que concurren **la autoridad y el terminal**, suscrita por ambos.
 
**Decisión: la segunda, por ser la más exigente** (BA, Art. 5.3 y 5.4). Alcanza a **toda** inspección con presencia de autoridad, y por tanto a las 18.400 anuales; la primera alcanza solo al subconjunto en que concurren dos o más servicios, que el caso ni siquiera cuantifica.
 
**Impacto si resulta equivocada.** Ninguno adverso: el error sería por exceso de cobertura de firma.
 
**Validación.** Levantamiento con cada autoridad, meses 1 a 4. **Vinculación:** `RF-INS-06`.
 
## C.4 Supuestos de alcance
 
### Supuesto O — Vía de excepción del operador, extensión de la Decisión N° 3
 
**El vacío.** La Decisión N° 3 admite en su campo de impacto que «el operador ejecutará una instrucción errónea **sin oportunidad de corregirla** antes del movimiento». La Decisión N° 5 da vía de corrección al planificador; **ninguna decisión se la da al operador**.
 
**Decisión.** Se incorpora una **vía de excepción del operador condicionada a interlock de equipo detenido**: la función de marcar una instrucción como no ejecutable solo está disponible cuando la telemetría acredita detención, y se deshabilita al reanudarse el movimiento.
 
**Fundamento.** CP, Cap. 10, restricción no negociable N° 1 prohíbe la interacción **mientras hay equipos en movimiento**, y por tanto no alcanza a una acción con el equipo detenido · CP, Cap. 15, RT-13.08 · Decisión N° 5, por analogía · Dahiya et al. (2026), que documenta que el error de colocación proviene de causas que el posicionamiento automático no corrige.
 
**Alternativas descartadas.** No dar vía de excepción —deja vigente el defecto reconocido; el operador ejecuta una instrucción que sabe errónea o la incumple sin registro, y lo segundo es peor—; vía sin interlock —expone la propuesta al rechazo por la restricción N° 1—; aviso por radio al supervisor —es el procedimiento actual que el CP, Cap. 5 prohíbe, y pierde el motivo—; confirmación activa de toda instrucción —ya descartada por la Decisión N° 3.
 
**Impacto si resulta equivocada.** Si la revisión ergonómica determina que incluso con el equipo detenido la interacción eleva el riesgo, la vía se retira y debe compensarse permitiendo al **supervisor de patio** declarar la condición en nombre del operador, con pérdida de inmediatez. Riesgo secundario: **un uso frecuente de la excepción indica que el algoritmo desconoce restricciones estructurales**, no puntuales; su tasa de uso se monitorea como indicador de calidad del algoritmo.
 
**Validación.** Acta de conformidad de prevención de riesgos y del sindicato antes del diseño detallado; prueba en equipo real durante la marcha blanca. **Vinculación:** `RF-PAT-10`.
 
### Supuesto P — Alcance del autoservicio del portal
 
**El vacío.** CP, Cap. 18 criterio 15 espera que los clientes resuelvan sus consultas «sin llamar por teléfono ni presentarse al mostrador», y BTT, RT-16.32 exige autoatender «las consultas de mayor frecuencia». **El caso nunca declara cuáles son.**
 
**Decisión.** A falta de declaración del CLIENTE, Terabyte deriva el alcance de **los trámites que el propio caso describe como carga de mostrador, teléfono, correo o radio**. Se comprometen siete:
 
| # | Trámite | Origen en el caso |
|---:|---|---|
| 1 | Consulta autenticada de estado y posición del contenedor | CP, Cap. 5: el portal de 2016 consulta por número, sin autenticación, con datos de un día |
| 2 | Solicitud, modificación y cancelación de cita de camión | Decisión N° 6: sin autoservicio, la cita reintroduce el teléfono que pretende eliminar |
| 3 | Carga y validación anticipada de documentación | Decisión N° 7: precondición del criterio de aceptación 3 |
| 4 | Descarga de evidencia de hecho facturable y objeción en línea | CP, Cap. 4.8: las objeciones viajan por correo con seguimiento en planilla |
| 5 | Descarga de la serie de temperatura como evidencia de cadena de frío | CP, Cap. 9.5 y Cap. 12, materia 9 |
| 6 | Coordinación y estado de cita de inspección | Decisión N° 21 · CP, Cap. 15, RT-12.12 |
| 7 | Estado de congestión del acceso vial, en capa pública | BTT, RT-16.31 |
 
**Impacto si resulta equivocada.** Si las consultas de mayor frecuencia reales no están entre las siete, el portal **cumple la letra de RT-16.32 sin descargar el mostrador**. Por eso `RF-POR-08` obliga a medir el desvío del canal telefónico: es el control que detecta ese error a tiempo.
 
**Validación.** Contraste con el registro de contactos del área comercial y de documentación del CLIENTE, meses 1 a 4.
 
### Supuesto Q — Generalización de la programación anticipada de remociones
 
**Decisión.** `RF-PAT-11` extiende el mecanismo de la Decisión N° 21 —programar la remoción al agendar— a **todo compromiso con hora cierta**: retiro con cita (Decisión N° 6, RN-07) y embarque planificado (Decisión N° 4), además de la inspección.
 
**Fundamento.** Identidad de razón: en los tres casos existe un tercero con hora acordada y un contenedor que puede estar bloqueado.
 
**Impacto si resulta equivocada.** La programación anticipada consume capacidad de grúa. Si el volumen de compromisos con hora cierta excede la capacidad disponible en ventanas ociosas, compite con la meta 1 de remociones — el trade-off que Klar et al. (2024) documentan.
 
**Validación.** Medición durante la marcha blanca. **Vinculación:** `RF-PAT-11`, `RF-INS-03`.
 
### Supuesto R — Universo de instrumentación de equipos
 
**Decisión.** El universo a instrumentar es de **74 equipos** —18 grúas de patio, 42 tractocamiones y 14 de manipulación pesada—, con proyección a **88** conforme al CP, 14.1.
 
**Fundamento.** El catálogo original comprometía «18 de 18», contando solo las grúas de patio. El modelo de posición de la Decisión N° 2 y el registro de movimiento de la Decisión N° 15 requieren instrumentar **todo equipo que manipule o traslade un contenedor**, y los tractocamiones lo hacen.
 
**Impacto si resulta equivocada.** Si el CLIENTE no adquiere la instrumentación de los 74, los dominios `RF-PAT` y `RF-TRA` operan con cobertura parcial y la meta 2 no se alcanza.
 
**Validación.** Especificación de hardware con Célula 3, conforme al CP, Cap. 11, exclusión 9. **Vinculación:** meta 5, `RF-PAT-13`, `RF-TRA-01`.
 
### Supuesto S — Holgura de la remoción anticipada
 
**Decisión.** La holgura con que se programa la remoción antes de la hora acordada es **parámetro configurable**, con valor inicial de **4 horas**, conforme a BTT, RT-16.02.
 
**Fundamento.** El valor definitivo depende del plazo de aviso de cada autoridad, dato que el CLIENTE posee y no declaró. No se codifica en duro para no requerir desarrollo al ajustarlo, conforme a BTT, RT-16.04.
 
**Validación.** Levantamiento de los meses 1 a 4. **Vinculación:** `RF-INS-03`, `RF-INS-04`, meta 11.
 
### Supuesto T — Ventana de desfase de la escritura dual
 
**Decisión.** La ventana de desfase tolerada entre el registro propio y el sistema de 2012 es de **60 segundos**, valor provisional.
 
**Fundamento.** `RF-CON-03` invocaba una «ventana de desfase declarada» que ninguna decisión declaraba, dejando su criterio de aceptación inejecutable.
 
**Validación.** Puerta de decisión del mes 4, al medirse la latencia real de escritura. **Vinculación:** `RF-CON-03`, `RF-CON-05`.
 
---
 
# Bloque D — Notas de alcance
 
> No son supuestos: son declaraciones que deben aparecer para que una ausencia deliberada no se lea como omisión.
 
## D.1 El criterio de aceptación 19 no admite requerimiento funcional
 
«La red operacional queda segregada de la administrativa y de la de protección» (CP, Cap. 18, criterio 19) describe un **estado de la infraestructura**, no un comportamiento observable que produzca un resultado. Bajo el criterio de clasificación declarado, no es funcional.
 
Queda cubierto por **RNF-SEG-06** y por la arquitectura física del **Subdocumento 4**. No se redacta un requerimiento artificial para completar la tabla de cobertura.
 
## D.2 Tres decisiones no generan requerimiento funcional
 
Las Decisiones **N° 9** (cobertura inalámbrica), **N° 19** (segregación de redes) y **N° 20** (sala de servidores) son de arquitectura física. No describen comportamiento observable y no producen requerimiento funcional propio. Corresponden al Subdocumento 4 y a la Célula 3.
 
La Decisión N° 20 tiene reflejo indirecto en `RF-OPD`, porque la operación autónoma de 72 horas depende de que exista cómputo local real.
 
---
 
# Bloque E — Estado y pendientes
 
## E.1 Composición
 
| Bloque | Contenido | Cantidad |
|---|---|---:|
| A | Decisiones del 16.1 más la N° 21 | **21** |
| B | Metas comprometidas | **17** — 15 con valor, 2 declaradas sin meta |
| C | Supuestos declarados | **20** — S1 a S5, A a L, M a T |
| D | Notas de alcance | 2 |
 
## E.2 Cambios respecto de la versión 1
 
| Cambio | Detalle |
|---|---|
| **Decisión N° 21 incorporada** | Vacío no listado en el 16.1, identificado por Célula 2 |
| **Metas 6 y 11 modificadas** | La 6 cambia de justificación —el beneficio es cobertura sin ventana ciega, no velocidad—; la 11 baja de ≤ 8 % a **≤ 12 %** por falta de evidencia y trade-off documentado con la meta 1 |
| **Meta 5 corregida al alza** | De 18 a **74 equipos** a instrumentar |
| **Metas 1 y 2 refundadas** | Sustituyen la cifra de proveedor por literatura arbitrada, e incorporan la evidencia adversa |
| **Seis metas nuevas** | Umbrales comprometidos en la Fase 4: metas 12 a 17 |
| **Ocho supuestos nuevos** | M a T |
| **Supuesto I precisado** | Se nombra el instrumento: checklist ergonómico por puesto de terreno |
 
## E.3 Pendientes
 
| # | Pendiente | De quién |
|---:|---|---|
| 1 | **Decisiones N° 3, 14 y 15 sin verificación externa.** La N° 3 sostiene todo `RF-PAT` | Célula 2 · Informe 2 |
| 2 | **Volumetría del CP, Cap. 14.2** — la tabla de dimensionamiento que el proponente debe estimar sigue incompleta. RT-09.02 exige derivar concurrencia y TPS de ella | Isidora |
| 3 | Cuatro decisiones sobre los **requerimientos en revisión** que duplican un RNF | Isidora |
| 4 | Ratificación por la célula de las **metas 6 y 11** modificadas y del **supuesto O** | Célula 2 |
| 5 | Valores numéricos de los ejemplos de `RF-EMI-03`, al fijar los factores de emisión | Junto al registro de reglas |
| 6 | Confirmación de la **tolerancia VGM chilena** (RN-05) con la autoridad marítima | Levantamiento |
| 7 | Plazo de aviso de cada autoridad y existencia de interfaz electrónica | Levantamiento meses 1 a 4 |
 
## E.4 Documentos que este registro reemplaza y conserva
 
| Documento | Estado |
|---|---|
| `registro_supuestos_decisiones_02_20.md` | **Incorporado.** Sus fichas extensas y sus 33 referencias se conservan hasta la integración final al informe |
| `registro_supuestos_complemento_celula2.md` | **Reemplazado íntegramente** |
| `01_decision_01_tos_2012_registro_final.md` | **Se mantiene aparte.** Fuente de la Decisión N° 1 y de S1 a S5 |
| `complemento_reglas_negocio_y_rf_pat_10.md` | Su supuesto de `RF-PAT-10` queda incorporado aquí como **supuesto O**; sus reglas, en `registro_reglas_de_negocio_v2.md`. **Puede archivarse** |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*