# Matriz de cobertura — Fase 2 del Catálogo de Requerimientos Funcionales

> **ADVERTENCIA — DOCUMENTO HISTÓRICO DESFASADO.** No usar como fuente vigente ni para conteos. La corrección aplicable está en `registro_correccion_plan_maestro_20260904.md`; el Plan Maestro prevalece ante cualquier contradicción. Este archivo se conserva sin reestructurarlo para no perder trazabilidad.
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Propósito:** demostrar cobertura antes de redactar, y detectar los vacíos mientras corregirlos todavía es barato.
> **Método:** barrido de las doce fuentes del plan, ejecutado sobre los documentos oficiales; tres cruces cuyas filas son las **exigencias**, no las fuentes.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado histórico:** Fase 2 completada en su momento; sus conteos y vacíos no representan el catálogo vigente.
 
---
 
## 1. Correcciones al dossier de contexto
 
El barrido contra los documentos oficiales detectó dos discrepancias con `informe_1_contexto_general_caso_portuaria.md`. Importan porque las cuatro células citan ese dossier.
 
| Asunto | Dossier de contexto | Documento oficial |
|---|---|---|
| Ubicación de las exclusiones explícitas | «Capítulo 13» | **Capítulo 11.** El Cap. 13 del CP es «Horizonte, prioridades y etapas» |
| Cantidad de indicadores de línea base | 19 indicadores | **28 indicadores**, repartidos en CP 7.1 (8), 7.2 (11) y 7.3 (9) |
 
El propio dossier advierte que no debe citarse como evidencia única. Ambas correcciones deben propagarse antes de que alguna célula cite «CP, Cap. 13» para una exclusión.
 
---
 
## 2. Resultado del barrido de fuentes (Fase 1)
 
| Fuente | Resultado verificado |
|---|---|
| CP, Cap. 4 — Operación actual | 9 procesos, no 7: recalada y ventana; plan de estiba y patio; atención de nave; patio y remociones; patio refrigerado; gate, documentación y pesaje; inspecciones; facturación; nombrada y acceso |
| CP, Cap. 7 — Línea base | **28 indicadores**. Los 11 del numeral 7.2 **no traen meta ni referencia**: esa columna no existe en la tabla original |
| CP, Cap. 18 — Criterios de aceptación | **22 confirmados** |
| CP, Cap. 9 — Expectativas de negocio | **10 confirmadas** (9.1 a 9.10) |
| CP, Cap. 10 — Restricciones no negociables | **14 confirmadas** |
| CP, Cap. 11 — Exclusiones | **9 confirmadas.** 7 de las 9 asignan responsabilidad residual explícita al proponente |
| CP, Cap. 12 — Marco normativo | **13 materias** |
| CP, Cap. 5 — Sistemas existentes | 7 sistemas o medios, con destino declarado |
| BTT — Códigos RT | **374 confirmados y clasificados.** 74 funcionales, 107 no funcionales, 192 de proceso o contractuales, 1 ambiguo (RT-21.12). 21 códigos marcados «Según caso» |
 
El inventario completo de los 374 códigos está en `claude/inventario_RT_bases_tecnicas_transversales.md`.
 
**Consecuencia sobre el volumen del catálogo.** Los 74 códigos RT funcionales del BTT se concentran en tres capítulos: Cap. 16 «Módulos transversales obligatorios» aporta 27, Cap. 5 «Datos e integración» aporta 13 y Cap. 12 «Identidad y acceso» aporta 11. Entre los tres, 51 de 74. Esos 74 alimentan directamente el catálogo funcional y el Formulario T-12, y confirman la estimación de 100 a 120 requerimientos: los códigos transversales más el comportamiento propio del caso.
 
---
 
## 3. Cruce A — Los 22 criterios de aceptación contra los dominios
 
| N° | Criterio de aceptación (CP, Cap. 18) | Dominio | Decisiones que lo fundan | Estado |
|---:|---|---|---|---|
| 1 | Estadía del camión dentro del umbral, sostenida y auditable | `RF-GAT` · `RF-CON` | 6, 7 | Cubierto |
| 2 | Sin fila que desborde a vía pública en lunes de temporada | `RF-GAT` | 6 | Cubierto |
| 3 | Documentación validada antes de salir a la ruta | `RF-GAT` · `RF-POR` | 7 | Cubierto |
| 4 | Código del contenedor reconocido automáticamente en gate | `RF-GAT` | 2 | Cubierto |
| 5 | Ventana de atraque confirmada con 72 h y cumplida | `RF-NAV` · `RF-INT` | 18 | Cubierto |
| 6 | Productividad de grúa medida y explicada por hora y equipo | `RF-NAV` | 15 | Cubierto |
| 7 | Planificación sin dependencia de una sola persona | `RF-NAV` | 4, 5 | Cubierto |
| 8 | Remociones bajan de forma medible | `RF-PAT` | 3 | Cubierto · **sin meta declarada** |
| 9 | Posición registrada coincide con la real; sin búsquedas físicas | `RF-PAT` | 2 | Cubierto · **sin meta declarada** |
| **10** | **Contenedor citado para inspección disponible a la hora acordada** | `RF-INS` | **ninguna** | **VACÍO 1** |
| 11 | Desconexión o desviación detectada y notificada en minutos | `RF-REF` | 8, 10 | Cubierto |
| 12 | Registro continuo de temperatura entregable | `RF-REF` | 8 | Cubierto |
| 13 | Instrucciones y planos por mensajería estándar, sin digitación | `RF-INT` | 18 | Cubierto |
| 14 | Cada hecho facturable con evidencia suficiente | `RF-FAC` | 11 | Cubierto |
| **15** | **Clientes resuelven sin teléfono ni mostrador** | `RF-POR` | **ninguna** | **VACÍO 4** |
| 16 | Emisiones por contenedor con método verificable | `RF-EMI` | 16, 17 | Cubierto |
| 17 | Se sabe cuántas personas hay, quiénes y bajo qué habilitación | `RF-ACC` | 12, 13 | Cubierto |
| 18 | 72 h sin enlace sin perder registro ni hechos facturables | `RF-OPD` | 20 | Cubierto |
| **19** | **Red operacional segregada de la administrativa y la de protección** | **ninguno** | 19 | **VACÍO 3 — no es satisfacible por un RF** |
| 20 | Indicadores del concedente trazables, sin reconstrucción manual | `RF-CON` + transversal | 1 | Cubierto |
| 21 | El operador de grúa recibe el plan en cabina, sin radio ni apartar la vista | `RF-NAV` | 14 | Cubierto |
| 22 | El planificador se jubila y el terminal sigue planificando | `RF-NAV` | 4, 5 + frente de captura de la Decisión 1 | Cubierto |
 
**Lectura del cruce.** 19 de 22 criterios quedan cubiertos por un dominio con decisión que los funda. Tres no: el 10 y el 15 porque ninguna de las veinte decisiones los alcanza, y el 19 porque no es un comportamiento.
 
Ningún dominio quedó sin criterio asociado, salvo `RF-OPD`, que sostiene el criterio 18 en solitario, y `RF-CON`, que aparece como soporte de trazabilidad en los criterios 1 y 20 más que como titular. Ambos se justifican por sí mismos: `RF-OPD` por la restricción no negociable N° 4 y `RF-CON` por los seis requisitos que la Decisión 1 ya dejó redactados.
 
---
 
## 4. Cruce B — Los 28 indicadores de línea base
 
Marcados con ⚠ los que **no traen meta ni referencia** en el documento. El Cap. 18 del CP obliga: *«el PROPONENTE deberá… proponer la meta cuando este documento no la fije»*.
 
### 4.1 La nave y el muelle (CP, 7.1)
 
| Indicador | Valor 2025 | Referencia | Dominio |
|---|---|---|---|
| Cumplimiento de ventana de atraque | 71 % | 90 % | `RF-NAV` |
| Productividad efectiva de grúa | 24,8 mov/h | 30 a 2029 | `RF-NAV` |
| Instrucciones de embarque digitadas a mano | 41 % | cero | `RF-INT` |
| Formatos distintos de plano de estiba | 6 | estándar único | `RF-INT` |
| Personas capaces de planificar estiba y patio | 1 | — | `RF-NAV` |
| Registro de movimientos por hora y por grúa | inexistente | continuo | `RF-NAV` |
| Capacidad de explicar un sobretiempo a la naviera | inexistente | trazable | `RF-NAV` |
| Semestres consecutivos sobre el umbral de estadía | 3 | cero | `RF-GAT` |
 
### 4.2 El patio y la carga refrigerada (CP, 7.2) — ninguno tiene meta
 
| Indicador | Valor 2025 | Dominio | |
|---|---|---|---|
| Movimientos de patio que son remociones | 18 % | `RF-PAT` | ⚠ |
| Contenedores registrados donde no están | 3,1 % | `RF-PAT` | ⚠ |
| Búsqueda física de un contenedor | 40 min | `RF-PAT` | ⚠ |
| Ocupación del patio en peak | 90 % | contexto de diseño | ⚠ |
| Equipos de patio con terminal montada | 12 de 18 | `RF-PAT` + especificación de hardware | ⚠ |
| Intervalo de control de refrigerados | 4 h, ronda a pie | `RF-REF` | ⚠ |
| Tomas con instrumentación remota | 0 de 2.400 | `RF-REF` | ⚠ |
| Tableros con alarma remota | 0 de 26 | `RF-REF` | ⚠ |
| Registro continuo de temperatura entregable | inexistente | `RF-REF` | ⚠ |
| Pérdida del evento del 18 de febrero | US$ 620.000 | evento, no indicador accionable | ⚠ |
| Inspecciones atrasadas por no ubicar el contenedor | 28 % | `RF-INS` | ⚠ |
 
### 4.3 El camión, el gate y la facturación (CP, 7.3)
 
| Indicador | Valor 2025 | Referencia | Dominio |
|---|---|---|---|
| Estadía del camión | 78 min | 45 comprometidos | `RF-GAT` |
| Fila máxima en el acceso | 3,2 km / 140 camiones | cero | `RF-GAT` |
| Camiones con documentación incompleta | 22 % | bajo 5 % | `RF-GAT` |
| Sistema de citas | inexistente | — | `RF-GAT` |
| Lectura automática del código en gate | inexistente | — | `RF-GAT` |
| Discrepancias de masa bruta sobre tolerancia | 6 % | bajo 1 % | `RF-GAT` |
| Facturas objetadas | 4,7 % | bajo 1 % | `RF-FAC` |
| Objeciones aceptadas por falta de evidencia | 62 % | cero | `RF-FAC` |
| Emisiones por contenedor | no se mide | reporte verificado a 2029 | `RF-EMI` |
 
**Lectura del cruce.** Los 28 indicadores tienen dominio asignado. Ninguno queda huérfano. Pero **once carecen de meta declarada**, y los once están concentrados en patio y carga refrigerada — precisamente los dominios donde la solución promete su mayor efecto. Proponer esas metas es obligación del proponente y **es materia de registro de supuestos, no de redacción silenciosa dentro de un requisito**.
 
---
 
## 5. Cruce C — Las 20 decisiones contra los dominios
 
| Decisión | Materia | Dominio |
|---:|---|---|
| 1 | Estrategia frente al sistema de 2012 | `RF-CON` |
| 2 | Método para conocer la posición real | `RF-PAT` |
| 3 | Quién decide dónde se apila | `RF-PAT` |
| 4 | Autonomía de la planificación | `RF-NAV` |
| 5 | Restricciones tácitas del planificador | `RF-NAV` |
| 6 | Sistema de citas | `RF-GAT` |
| 7 | Validación documental anticipada | `RF-GAT` · `RF-POR` |
| 8 | Frecuencia de muestreo refrigerado | `RF-REF` |
| **9** | **Cobertura inalámbrica del patio** | **ninguno — arquitectura física** |
| 10 | Escalamiento y confirmación de alarmas | `RF-REF` |
| 11 | Hecho que constituye evidencia facturable | `RF-FAC` |
| 12 | Habilitación de eventuales sin biometría | `RF-ACC` |
| 13 | Conteo y ubicación de personas en emergencia | `RF-ACC` |
| 14 | Información al operador de grúa de muelle | `RF-NAV` |
| 15 | Evidencia de movimiento sin confirmación | `RF-PAT` · `RF-NAV` |
| 16 | Metodología de emisiones | `RF-EMI` |
| 17 | Consumo real por equipo | `RF-EMI` |
| 18 | Mensajería con navieras | `RF-INT` |
| **19** | **Segregación de redes** | **ninguno — arquitectura física** |
| **20** | **Destino de la sala de servidores** | **ninguno — arquitectura física**, con reflejo en `RF-OPD` |
 
**Lectura del cruce.** 17 de 20 decisiones se materializan en al menos un dominio funcional. Las decisiones 9, 19 y 20 son de arquitectura física pura: no describen comportamiento observable y, bajo el criterio de clasificación adoptado, **no generan requerimiento funcional**. Corresponden al Subdocumento 4 y a la Célula 3.
 
Esto debe **declararse explícitamente** en el catálogo. Tres decisiones sin requisito asociado se leen como omisión si no se explica que la ausencia es deliberada y de dónde cuelgan.
 
---
 
## 6. Vacíos a resolver antes de la Fase 3
 
| N° | Vacío | Gravedad | Vía de resolución |
|---:|---|---|---|
| **1** | **Inspecciones de autoridad** | Alta | Registro de decisión nuevo, antes de redactar `RF-INS` |
| **2** | **Once indicadores sin meta declarada** | Alta | Supuestos declarados con método de derivación |
| **3** | **Criterio de aceptación 19 no es satisfacible por un RF** | Media | Declaración explícita y remisión a RNF-SEG-06 y Subdocumento 4 |
| **4** | **Alcance del autoservicio no decidido** | Media | Decisión de alcance, o supuesto declarado |
| **5** | **Decisiones 9, 19 y 20 sin RF** | Baja | Nota de alcance en el catálogo + traspaso a Célula 3 |
| **6** | **107 códigos RT no funcionales del BTT contra 77 RNF en el catálogo** | Media | Verificar el mapeo al construir el T-12 |
| **7** | **«Acta de inspección conjunta» no definida en ninguna parte** | Media | Supuesto declarado |
 
### 6.1 Vacío 1 — Inspecciones de autoridad
 
Es más profundo de lo previsto. El barrido confirmó que:
 
- **Ninguna de las veinte decisiones del numeral 16.1 cubre la coordinación de inspecciones**, pese a que el CP, numeral 17.4 punto 9 exige que la arquitectura resuelva «cómo se integran las autoridades aduanera, fitosanitaria y sanitaria en la coordinación de inspecciones, y qué se hace donde no exista interfaz disponible», y pese a que el Cap. 18 lo fija como criterio de aceptación N° 10.
- **No hay meta** para reducir el 28 % de atraso.
- **No se declara si existe interfaz electrónica** en ninguno de los tres servicios. El CP formula la pregunta pero no informa el estado actual.
- **RT-16.14 exige firma electrónica en «las actas de inspección conjunta»**, y esa expresión no está definida en ninguna parte del caso: no se dice qué es, quién la suscribe ni qué contiene.
- **La inspección es un hecho facturable** (CP, 4.8 la lista entre los conceptos que el terminal cobra), sin que el documento describa cómo se evidencia hoy.
- **RT-12.12 incorpora a los inspectores como personas usuarias externas** del sistema, con registro y recuperación de acceso autoservidos.
- **No se desagregan** las 18.400 inspecciones anuales por servicio ni por tipo, ni se declara el plazo de aviso de cada autoridad.
El propio CP advierte que la lista de veinte decisiones **no es exhaustiva** y que *«el PROPONENTE que identifique vacíos no listados aquí será evaluado favorablemente por ello»*. Este vacío es, por tanto, una oportunidad de evaluación además de un problema de cobertura.
 
### 6.2 Vacío 2 — Once indicadores sin meta
 
El CP, Cap. 18 obliga al proponente a proponer la meta cuando el documento no la fija. Los once están en el numeral 7.2 y cubren remociones, posiciones erróneas, tiempo de búsqueda, cobertura de terminales, intervalo de control refrigerado, instrumentación de tomas y tableros, registro continuo de temperatura y atraso de inspecciones.
 
Cada meta propuesta necesita **valor, método de derivación y supuestos empleados**, conforme al criterio que el CP, Cap. 14 aplica al dimensionamiento. Comprometer una cifra sin derivación es tan objetable como no comprometerla.
 
### 6.3 Vacío 3 — El criterio 19 no admite requerimiento funcional
 
«La red operacional queda segregada de la administrativa y de la de protección» describe un **estado de la infraestructura**, no un comportamiento observable que produzca un resultado. Bajo el criterio de clasificación adoptado en la Fase 0, no es funcional.
 
Está cubierto por RNF-SEG-06 del catálogo de requerimientos no funcionales y por la arquitectura física del Subdocumento 4. La decisión correcta es **declararlo así en el catálogo**, no fabricar un requisito funcional artificial para que la tabla de cobertura no tenga huecos.
 
### 6.4 Vacío 4 — Alcance del autoservicio
 
El criterio de aceptación 15 espera que los clientes «resuelvan sus consultas y coordinaciones sin llamar por teléfono ni presentarse al mostrador», y RT-16.32 exige resolver por autoservicio «las consultas de mayor frecuencia». **El caso no declara cuáles son esas consultas de mayor frecuencia**, y ninguna de las veinte decisiones fija el alcance funcional del portal.
 
Los actores involucrados son 210 agencias de aduana, unos 1.400 exportadores e importadores y 380 empresas de transporte. Definir qué trámites se autoatienden es una decisión de alcance con consecuencia directa sobre el tamaño de `RF-POR`.
 
---
 
## 7. Qué queda habilitado
 
Con los vacíos 1, 2 y 4 resueltos, la Fase 3 puede ejecutarse dominio por dominio sin descubrimientos que obliguen a rehacer. Los vacíos 3 y 5 se resuelven con una nota de alcance en el catálogo. El vacío 6 se arrastra hasta la construcción del T-12 y el 7 se declara como supuesto.
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.
