# Complemento al Registro de Supuestos — vacíos detectados en la Fase 2
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Origen:** vacíos 1, 2, 3, 4, 5 y 7 de `claude/matriz_cobertura_rf_fase2.md`.
> **Estado:** propuestas fundadas de Célula 2, ratificadas por Rodolfo Fernández. Pendientes de revisión por Isidora Cisternas y por el delegado.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
Este archivo complementa `registro_supuestos_decisiones_02_20.md`. No lo reemplaza.
 
---
 
## 1. Decisión N° 21 — Coordinación de inspecciones de autoridad
 
> **Vacío no listado en el numeral 16.1.** El CP declara que esa lista no es exhaustiva y que *«el PROPONENTE que identifique vacíos no listados aquí será evaluado favorablemente por ello»*. Se registra con el mismo formato de seis campos que las veinte decisiones numeradas.
>
> **Clase de profundidad: ficha.** Tiene alternativas reales y fundamento normativo explícito, pero no es irreversible, no descansa sobre una contradicción entre textos normativos y no condiciona el alcance completo del proyecto.
 
### 1.1 La decisión
 
**Terabyte adopta un módulo de coordinación de inspecciones que convierte la cita de inspección en una tarea programada del patio, con la remoción anticipada incluida, en lugar de tratarla como una solicitud que se resuelve cuando el inspector ya está en el recinto.**
 
El módulo opera en cuatro movimientos:
 
1. **Recepción normalizada.** Recibe la selección de cada autoridad por el canal que esa autoridad tenga disponible —interfaz electrónica donde exista, carga de archivo o registro asistido donde no— y la normaliza a un **evento interno único de cita de inspección**, con autoridad, contenedor, fecha, hora y tipo.
2. **Reserva de disponibilidad.** Al registrar la cita, calcula si el contenedor está accesible en su posición actual y, si no lo está, **programa anticipadamente las remociones necesarias** contra el plan de patio, con la holgura declarada antes de la hora acordada.
3. **Visibilidad para el inspector.** Publica el estado de la cita a los inspectores como personas usuarias externas de la solución, conforme a **BTT, RT-12.12**.
4. **Cierre con evidencia.** Genera el acta de inspección con firma electrónica conforme a **BTT, RT-16.14**, y produce el hecho facturable asociado al servicio de inspección que el terminal cobra.
**El desplazamiento conceptual es el punto.** Hoy la inspección compite por recursos de patio en el momento en que se necesita. Con esta decisión, compite en el momento en que se agenda, que es cuando todavía hay margen.
 
### 1.2 Fundamento
 
| Fuente | Cita | Qué sostiene |
|---|---|---|
| CP, Cap. 4.7 | El 28 % de las inspecciones se atrasa «porque el contenedor no se ubicó a tiempo» o «porque estaba abajo de otros tres **y la remoción no se programó**» | El caso nombra la causa. La segunda mitad de esa frase es exactamente lo que esta decisión ataca |
| CP, Cap. 4.7 | «A la hora acordada, el contenedor debe estar en la zona de inspección, **abierto**, con el inspector presente» | Define la condición de cumplimiento, que involucra posición, remoción y apertura |
| CP, Cap. 18, criterio 10 | «Un contenedor citado para inspección está disponible a la hora acordada» | Es criterio de aceptación con nombre propio |
| CP, num. 17.4, punto 9 | «Cómo se integran las autoridades aduanera, fitosanitaria y sanitaria en la coordinación de inspecciones, **y qué se hace donde no exista interfaz disponible**» | Obliga a resolver ambos escenarios, no solo el favorable |
| CP, Cap. 11, exclusión 7 | «No se pide desarrollar el sistema de una autoridad ni sustituir sus canales; **sí integrarse a ellos donde exista una interfaz disponible**» | Fija la frontera: integración condicionada a que la interfaz exista |
| CP, Cap. 5 | Correo electrónico y planillas, que hoy soportan el «control de inspecciones», **«deben desaparecer como sistema de registro»** | Descarta la opción de dejar la coordinación como está y solo registrarla |
| BTT, RT-12.12 | Personas usuarias externas incluyen «inspectores de las autoridades aduanera, fitosanitaria y sanitaria» | Los inspectores son usuarios del sistema, no receptores pasivos |
| BTT, RT-16.14 | Firma electrónica exigible en «las actas de inspección conjunta» | Obliga a generar un acta firmada |
| CP, Cap. 4.8 | El terminal cobra «por inspección» | La inspección es hecho facturable y requiere evidencia |
| CP, Anexo B.1 | Ventana habitual de inspecciones: 08:00 a 18:00 | Acota la franja de programación |
 
**Nota de calidad del fundamento.** La cadena causal está sostenida por cita literal del caso. Lo que **no** está en las bases es el plazo de aviso con que cada autoridad comunica la selección — dato decisivo para dimensionar la holgura de la remoción anticipada. Ese vacío se trata en 1.5 y no se rellena por inferencia.
 
### 1.3 Alternativas descartadas
 
| Alternativa | Por qué se descarta |
|---|---|
| **Integración electrónica con las tres autoridades desde el inicio** | El caso **no declara** si alguna de las tres tiene interfaz disponible, y la exclusión 7 condiciona la integración a que exista. Comprometerla sería comprometer una capacidad no verificada — el mismo error que la Decisión N° 1 evita con su puerta de decisión del mes 4 |
| **Mantener la coordinación por correo y teléfono, registrándola en el sistema** | CP, Cap. 5 declara expresamente que esos medios deben dejar de ser sistema de registro. Además no ataca la causa: el atraso no se produce por falta de registro, sino por falta de programación |
| **Pre-posicionar en la zona de inspección los contenedores con probabilidad de selección** | Consume capacidad de patio que en peak está al 90 % de ocupación (CP, 7.2). CP, 13.3 punto 2 exigiría cuantificar y costear esa capacidad resignada, y el beneficio depende de una predicción de selección que ninguna base respalda |
| **Tratar la inspección como una solicitud de retiro más** | Es el comportamiento actual. Una inspección tiene hora comprometida con un tercero con potestad, y un retiro no |
 
### 1.4 Impacto si resulta equivocada
 
Si el plazo de aviso de alguna autoridad resulta **menor que el tiempo necesario para ejecutar la remoción anticipada**, el atraso persiste por una causa distinta de la actual, y la programación anticipada no lo resuelve. En ese escenario la solución debe degradar hacia una regla de prioridad —la remoción de inspección desplaza a la remoción de retiro— cuyo costo operacional habría que declarar.
 
Riesgo secundario: si el acta de inspección firmada no es aceptada por la autoridad como sustituto de su propio registro, la solución produce evidencia interna sin valor externo, y el hecho facturable sigue sin respaldo oponible.
 
### 1.5 Instancia y momento de validación
 
- **Plazo de aviso de cada autoridad** y **existencia de interfaz electrónica** en Aduana, SAG y autoridad sanitaria: son hechos que el CLIENTE posee y no declaró. Habrían sido consulta admisible; cerrado el período (BA, Art. 43.1), se declaran **supuesto de levantamiento** y se resuelven en el descubrimiento de los meses 1 a 4, en la misma puerta de decisión que la Decisión N° 1.
- **Aceptación del acta firmada por cada autoridad:** validación con la autoridad respectiva antes del cierre de desarrollo de la Etapa 2.
- **Efectividad de la programación anticipada:** medición durante la marcha blanca.
### 1.6 Responsable
 
Terabyte. Coordinación con Célula 3 para la integración de las autoridades en el Subdocumento 4.
 
### 1.7 Meta propuesta para el indicador
 
El CP, Cap. 18 obliga a proponer la meta cuando el documento no la fija. Ver sección 2, indicador 11.
 
---
 
## 2. Metas propuestas para los once indicadores sin referencia
 
**Fundamento de la obligación.** CP, Cap. 18: *«El PROPONENTE deberá comprometerse con ellos, proponer la meta cuando este documento no la fije, indicar en qué momento del cronograma se alcanzará cada uno y cómo se medirá.»* Los once indicadores del numeral 7.2 no traen columna de referencia.
 
**Regla aplicada.** Cada meta declara **valor, método de derivación y momento**. Donde el indicador no es accionable por la solución, se declara expresamente que **no se compromete meta**, con su razón. Inventar una cifra sin derivación sería tan objetable como omitirla.
 
| # | Indicador | Línea base | Meta propuesta | Momento | Método de derivación |
|---:|---|---|---|---|---|
| 1 | Movimientos de patio que son remociones | 18 % | **≤ 14 %** | Cierre de Etapa 2 | Reducción relativa de ~22 %, dentro del rango de 10 % a 25 % de reducción de remociones que reporta la práctica de la industria para el modelo de asignación algorítmica adoptado en la Decisión N° 3. **Cifra de proveedor, no verificada de forma independiente**: se toma un punto intermedio del rango y no su extremo optimista |
| 2 | Contenedores registrados donde no están | 3,1 % | **≤ 0,5 %** | Cierre de marcha blanca de Etapa 1 | Se alinea con el umbral de detención de la conciliación ya adoptado en la Decisión N° 1 (0,5 % de divergencias no explicadas). Bajo la Decisión N° 2, el indicador cambia de naturaleza: deja de medir error de registro y pasa a medir posiciones marcadas «por verificar» no resueltas dentro del turno |
| 3 | Búsqueda física de un contenedor | 40 min | **Cero como proceso normal.** Residual ≤ 0,5 % de los retiros, con tiempo objetivo ≤ 15 min | Cierre de Etapa 1 | CP, Cap. 18 criterio 9 exige «sin búsquedas físicas». El residual coincide con el 0,5 % del indicador 2, y 15 minutos corresponde a una verificación dirigida a una posición candidata conocida, no a un barrido |
| 4 | Ocupación del patio en peak | 90 % | **No se compromete meta** | — | No es un indicador que la solución pueda mover: depende del volumen comercial y de la superficie disponible, y no hay ampliación de patio comprometida (CP, Cap. 14). Se emplea como **parámetro de dimensionamiento** del peak coincidente |
| 5 | Equipos de patio con terminal montada | 12 de 18 | **18 de 18** | Cierre de desarrollo de Etapa 1 | No es meta gradual sino condición de la Decisión N° 15: si la telemetría del equipo es la fuente primaria de verdad del movimiento, un equipo sin instrumentar es un equipo cuyos movimientos no existen para el sistema. CP, Cap. 5 ya atribuye a la cobertura parcial parte del 3,1 % |
| 6 | Intervalo de control de refrigerados | 4 h, ronda a pie | **≤ 5 min de intervalo de control efectivo** | Cierre de desarrollo de Etapa 1 | Consecuencia directa de la Decisión N° 8 (muestreo local de 1 a 5 minutos) y coherente con el umbral de RNF-DES-04 (alarma ≤ 5 minutos desde el evento físico). La ronda a pie deja de ser el mecanismo de control |
| 7 | Tomas con instrumentación remota | 0 de 2.400 | **2.400 de 2.400**, y 2.900 en el horizonte de proyección | Cierre de desarrollo de Etapa 1 | Cobertura total, no parcial: una toma sin instrumentar reproduce exactamente el modo de falla del 18 de febrero de 2026. El valor de proyección proviene de CP, 14.1 |
| 8 | Tableros con alarma remota | 0 de 26 | **26 de 26**, y 32 en el horizonte de proyección | Cierre de desarrollo de Etapa 1 | Mismo fundamento que el indicador 7. El evento del 18 de febrero fue la falla de **un tablero completo**, no de una toma |
| 9 | Registro continuo de temperatura entregable | inexistente | **100 % de los contenedores refrigerados con serie continua**, retención 5 años | Cierre de desarrollo de Etapa 1 | La cobertura se deriva de los indicadores 7 y 8; la retención la fija BTT/CP, RT-05.10 para series de temperatura de carga refrigerada |
| 10 | Pérdida del evento del 18 de febrero | US$ 620.000 | **No se compromete meta** | — | Es un hecho ocurrido, no un indicador con serie. Comprometer una meta sobre él sería comprometer que no vuelva a ocurrir un evento singular. Su prevención se mide por los indicadores 6, 7, 8 y 9 y por RNF-DES-04 y RNF-DIS-08 |
| 11 | Inspecciones atrasadas por no ubicar el contenedor | 28 % | **≤ 8 %**, condicionada | Cierre de Etapa 2 | Las dos causas que declara CP, Cap. 4.7 quedan atacadas: la posición errónea por la Decisión N° 2 (indicador 2) y la remoción no programada por la Decisión N° 21. El residual corresponde a los casos en que el aviso de la autoridad llega con menos anticipación que el tiempo necesario para la remoción. **Ese plazo de aviso no está declarado en las bases**, de modo que la meta queda condicionada a su levantamiento y se revisará cuando se conozca |
 
> **Advertencia de método, deliberada.** Las metas 1 y 11 son las únicas que descansan parcialmente en información que las bases no entregan —una referencia de industria no arbitrada en el primer caso, un dato del CLIENTE no declarado en el segundo—. Ambas lo dicen en su propia fila. Las otras siete metas se derivan de decisiones ya adoptadas o de umbrales ya fijados en las bases.
 
---
 
## 3. Supuesto de alcance — Autoservicio del portal de clientes
 
**El vacío.** CP, Cap. 18 criterio 15 espera que los clientes «resuelvan sus consultas y coordinaciones sin llamar por teléfono ni presentarse al mostrador», y BTT, RT-16.32 exige resolver por autoservicio «las consultas de mayor frecuencia». **El caso nunca declara cuáles son esas consultas**, y ninguna de las veinte decisiones fija el alcance funcional del portal.
 
**Decisión adoptada.** A falta de declaración del CLIENTE, Terabyte deriva el alcance del autoservicio de **los trámites que el propio caso describe como carga de mostrador, teléfono, correo o radio**. Se comprometen siete:
 
| # | Trámite autoatendido | Origen en el caso |
|---:|---|---|
| 1 | Consulta de estado y posición del contenedor, autenticada y en tiempo real | CP, Cap. 5: el portal de 2016 solo consulta por número, sin autenticación y con datos de un día de antigüedad |
| 2 | Solicitud, modificación y cancelación de cita de camión | Decisión N° 6. Sin canal de autoservicio, la cita reintroduce el teléfono que pretende eliminar |
| 3 | Carga y validación anticipada de la documentación del viaje | Decisión N° 7. Es la precondición del criterio de aceptación 3 |
| 4 | Descarga de la evidencia de un hecho facturable y presentación de objeción en línea | CP, Cap. 4.8: las objeciones viajan hoy por correo con seguimiento en planilla |
| 5 | Descarga de la serie continua de temperatura como evidencia de cadena de frío | CP, Cap. 9.5 y Cap. 12, materia 9: es obligación comercial frente al cliente y a la autoridad |
| 6 | Coordinación y consulta del estado de una cita de inspección | Decisión N° 21 y BTT, RT-12.12 |
| 7 | Estado de congestión del acceso vial, en capa pública sin autenticación | BTT, RT-16.31. Es lo que permite al transportista decidir cuándo salir |
 
**Alternativas consideradas.** Comprometer un portal de consulta equivalente al de 2016 pero autenticado y en línea, que cumpliría RT-16.30 pero no el criterio 15 porque no elimina la llamada telefónica. O comprometer autoservicio total de todo trámite, que excede lo derivable y compromete alcance sin fundamento.
 
**Impacto si resulta equivocada.** Si las consultas de mayor frecuencia reales del CLIENTE no están entre las siete, el portal cumple la letra de RT-16.32 sin descargar el mostrador, y el criterio 15 no se alcanza pese al cumplimiento formal.
 
**Instancia de validación.** Contraste con el registro de contactos del área comercial y de documentación del CLIENTE durante el levantamiento de los meses 1 a 4. Es un dato que el CLIENTE posee.
 
**Responsable.** Terabyte.
 
---
 
## 4. Supuesto de interpretación — «Acta de inspección conjunta»
 
**El vacío.** BTT, RT-16.14 exige firma electrónica en «las actas de inspección conjunta». **La expresión no está definida en ninguna parte del CP**: no se dice qué contiene, quién la suscribe ni entre quiénes es conjunta. Es la única mención en todo el caso.
 
**Las dos lecturas posibles.**
 
1. Acta de una inspección en que **concurre más de una autoridad** sobre el mismo contenedor.
2. Acta de una inspección en que **concurren la autoridad y el terminal**, suscrita por ambos.
**Interpretación adoptada: la segunda, por ser la más exigente.** BA, Art. 5.3 y 5.4 obligan a adoptar la interpretación más exigente ante ambigüedad. La segunda lectura alcanza a **toda** inspección con presencia de autoridad, y por tanto a las 18.400 anuales; la primera alcanza solo al subconjunto en que concurren dos o más servicios, que el caso ni siquiera cuantifica.
 
**Impacto si resulta equivocada.** Ninguno adverso: si la lectura correcta era la primera, la solución habrá construido capacidad de firma para un universo mayor que el exigido. El error es por exceso y no compromete cumplimiento.
 
**Instancia de validación.** Levantamiento con cada autoridad durante los meses 1 a 4.
 
**Responsable.** Terabyte.
 
---
 
## 5. Notas de alcance del catálogo funcional
 
Estas dos notas no son supuestos: son declaraciones que deben aparecer en el catálogo para que una ausencia deliberada no se lea como omisión.
 
### 5.1 El criterio de aceptación 19 no admite requerimiento funcional
 
«La red operacional queda segregada de la administrativa y de la de protección» (CP, Cap. 18, criterio 19) describe un **estado de la infraestructura**, no un comportamiento observable que produzca un resultado. Bajo el criterio de clasificación declarado por Terabyte, no es funcional.
 
Queda cubierto por **RNF-SEG-06** del catálogo de requerimientos no funcionales y por la arquitectura física del **Subdocumento 4**. No se redacta un requerimiento funcional artificial para completar la tabla de cobertura.
 
### 5.2 Tres decisiones no generan requerimiento funcional
 
Las Decisiones **N° 9** (cobertura inalámbrica del patio), **N° 19** (segregación de redes) y **N° 20** (destino de la sala de servidores) son de arquitectura física. No describen comportamiento observable y, bajo el mismo criterio, no producen requerimiento funcional propio.
 
Corresponden al Subdocumento 4 y a la Célula 3. La Decisión N° 20 tiene reflejo indirecto en el dominio `RF-OPD`, porque la operación autónoma de 72 horas depende de que exista cómputo local real.
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*