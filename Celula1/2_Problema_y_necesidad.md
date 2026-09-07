# 2. COMPRENSIÓN DEL PROBLEMA Y DE LA NECESIDAD

## 2.1 Contexto de Terminal Portuario Aconcagua

Terminal Portuario Aconcagua S.A. es un operador de importancia vital ubicado en la Región de Valparaíso, responsable de la operación de un frente de atraque multipropósito dedicado a la transferencia de contenedores, carga refrigerada y carga fraccionada (Caso Portuaria, pág. 5). La entidad opera bajo un contrato de concesión estatal que se inició en el año 2011 y se encuentra vigente hasta 2041 (Caso Portuaria, pág. 5). Su estructura de propiedad está compuesta por un operador portuario internacional que posee el 60% de participación, y un grupo inversor nacional con el 40% restante, generando ingresos anuales del orden de los $96.000 millones (Caso Portuaria, pág. 5).

La naturaleza crítica de sus servicios exige un régimen operacional continuo de 24 horas al día, los 365 días del año, estructurado en tres turnos de ocho horas (Caso Portuaria, pág. 6). La compañía es operador de importancia vital conforme a la ley marco de ciberseguridad, y su instalación está sujeta al código internacional de protección de buques e instalaciones portuarias (ISPS/PBIP) (Caso Portuaria, pág. 5). Ambas condiciones imponen obligaciones concretas sobre cualquier cambio en sistemas, redes o control de acceso, y deben tratarse como restricciones activas desde el inicio del análisis, no como requisitos a resolver más adelante.

### 2.1.1 Infraestructura y capacidad instalada

El terminal despliega su operación sobre una infraestructura de recursos altamente compartidos y finitos. El frente de atraque cuenta con 940 metros lineales divididos en tres sitios, ofreciendo el sitio principal un calado de 14,2 metros (Caso Portuaria, pág. 5). El núcleo de la conectividad entre el ciclo marítimo y terrestre recae en un patio de contenedores de 18 hectáreas, el cual posee una capacidad de almacenamiento de 12.400 TEU (Caso Portuaria, pág. 5). Trabajan allí 640 personas propias más hasta 380 eventuales por turno en peak, sumando hasta 1.100 personas en el recinto simultáneamente (Caso Portuaria, págs. 6-7). Estos trabajadores eventuales se asignan diariamente por nombrada y los acuerdos sindicales rechazan la biometría obligatoria, lo que condiciona cualquier control de habilitación (Caso Portuaria, págs. 6, 18). El área de tecnologías de información cuenta con solo 5 personas para soportar toda esta operación (Caso Portuaria, pág. 6). Adicionalmente, para la cadena de frío, el recinto dispone de 2.400 tomas para contenedores refrigerados (reefers), energizadas a través de 26 tableros de distribución (Caso Portuaria, pág. 6).

### 2.1.2 Volumen operacional actual y proyecciones

En la actualidad, el terminal maneja una transferencia anual de 780.000 TEU (486.000 contenedores) y presta servicios a 620 naves al año (Caso Portuaria, pág. 5). Este flujo exige una alta intensidad operativa: 972.000 movimientos de grúa de muelle y 1.290.000 movimientos de patio anuales, incluyendo remociones (Caso Portuaria, pág. 27).

El flujo terrestre presenta una carga masiva: un promedio de 1.450 camiones diarios, con peaks de hasta 2.600 camiones por día, mientras la red ferroviaria absorbe únicamente el 15% de la carga (Caso Portuaria, pág. 5). En máxima demanda, el patio alcanza ocupaciones de 11.200 TEU y sostiene 2.150 contenedores refrigerados conectados simultáneamente (Caso Portuaria, pág. 27).

En un horizonte de tres años, la demanda subirá a 920.000 TEU anuales, 700 naves, peaks de 3.100 camiones por día y 2.900 tomas refrigeradas (Caso Portuaria, pág. 27). Este desafío debe absorberse sin una ampliación de patio comprometida en el corto plazo (Caso Portuaria, pág. 27), convirtiendo la optimización tecnológica en una urgencia estratégica.

## 2.2 Operación actual y procesos principales

La operación se estructura a través de dos ciclos interdependientes que conectan el flujo marítimo y terrestre (Caso Portuaria, págs. 8-10). Terabyte ha identificado que la gestión actual se sostiene fuertemente en procesos manuales, comunicación radial y el uso de un sistema de operación heredado del año 2012, lo cual limita la visibilidad y el control en tiempo real (Caso Portuaria, pág. 11).

### 2.2.1 Ciclo de la Nave y Planificación

El proceso inicia con el anuncio de recalada, emitido entre 3 y 10 días antes mediante canales no estandarizados (correo, portal o teléfono) (Caso Portuaria, pág. 8). La programación semanal de sitios de atraque sufre múltiples modificaciones diarias. Actualmente, el terminal cumple su ventana de atraque sólo el 71% de las veces, y su productividad es de 24,8 movimientos por hora, cifras insuficientes frente a los 30 movimientos y ventanas confirmadas de 72 horas exigidas por la alianza naviera para 2029 (Caso Portuaria, págs. 4, 13).

El plan de estiba, recepcionado en hasta 6 formatos distintos, obliga al único planificador a imprimirlo y trasladarlo manualmente a planillas personales (Caso Portuaria, págs. 8, 13). Este profesional experto se jubilará en 2028, lo que expone al terminal a perder su capacidad de planificación (Caso Portuaria, págs. 4, 15-16). Durante la atención, las estimaciones se basan en experiencia y los cambios se avisan por radio. Los movimientos de los 42 tractocamiones sin GPS se registran manualmente al cierre de turno, perdiendo trazabilidad horaria y por equipo (Caso Portuaria, pág. 9).

### 2.2.2 Gestión del Patio de Contenedores

El patio, distribuido en bloque, bahía, fila y altura, es gestionado combinando instrucciones previas con la apreciación visual del operador, sin un registro sistemático de las decisiones de ubicación (Caso Portuaria, pág. 9). Como resultado, el 18% de los movimientos son remociones improductivas (Caso Portuaria, pág. 9). El 3,1% del inventario está posicionado incorrectamente, detonando búsquedas físicas de 40 minutos en promedio, problema que colapsa la operación cuando la ocupación del patio llega al 90% en temporada (Caso Portuaria, pág. 9).

### 2.2.3 Ciclo del Patio Refrigerado (Cadena de Frío)

El terminal gestiona la cadena de frío de 2.400 tomas reefer basándose en inspecciones físicas. Un operador debe recorrer las instalaciones a pie, revisando los visores de cada contenedor y anotando manualmente la temperatura y el estado de conexión (Caso Portuaria, pág. 9).

Cada ronda de inspección consume aproximadamente cuatro horas. Los datos recopilados se ingresan al sistema recién al día siguiente, impidiendo generar evidencias operativas continuas ni reportes en tiempo real para los exportadores. La vulnerabilidad de este proceso se acentúa dado que los 26 tableros de distribución de energía carecen de sistemas de alarmas remotas y su respaldo energético no ha sido validado bajo condiciones de carga máxima (Caso Portuaria, págs. 10-11).

### 2.2.4 Flujo Terrestre, Documentación e Inspecciones

El acceso al terminal opera sin un sistema de citas previas, exponiendo el flujo de recepción al arribo aleatorio de camiones. En el gate (de 8 puestos de entrada y 6 de salida), el personal debe verificar la documentación (la cual presenta errores en el 22% de los arribos), digitar manualmente el código de 11 caracteres del contenedor, ejecutar el pesaje (cuando es requerido) e instruir el destino (Caso Portuaria, pág. 10).

Las discrepancias en la verificación de masa bruta que superan la tolerancia normativa alcanzan el 6%, obligando a reprocesar el plan de estiba. En conjunto, estas demoras provocan que el tiempo promedio de estadía de un camión sea de 78 minutos, superando ampliamente la meta contractual de 45 minutos en el terminal, lo que genera episodios de congestión estructural severa hacia la red vial de la ciudad (Caso Portuaria, págs. 10, 14).

Paralelamente, los procesos de inspección aduanera, fitosanitaria y sanitaria se ven directamente afectados por la gestión del patio: el 28% de estas revisiones experimenta retrasos debido a la imposibilidad de ubicar los contenedores requeridos de manera oportuna, arriesgando la pérdida de la nave para el cliente (Caso Portuaria, pág. 10).

### 2.2.5 Ecosistema Tecnológico y Condiciones del Sitio

Todos los ciclos operativos dependen de un ecosistema tecnológico altamente fragmentado (Caso Portuaria, pág. 11). El núcleo operacional es el sistema implantado en 2012, el cual acumula 14 años de personalizaciones realizadas por 4 proveedores distintos, sin documentación actualizada de su modelo de datos, y cuyo soporte oficial expira en 2028 (Caso Portuaria, págs. 11 12). La estrategia sobre su futuro corresponde a una decisión arquitectónica fundamental de la Etapa de Solución.

Alrededor de este sistema orbitan herramientas desintegradas: un portal de clientes de 2016 sin autenticación y con actualización diaria, y un uso intensivo de correos, radios y planillas que actúan como el sistema de registro de facto para los procesos críticos (Caso Portuaria, pág. 12). Adicionalmente, el terminal mantiene un ERP como único emisor tributario y un sistema de control de grúas de muelle cerrado por el fabricante, permitiendo únicamente integraciones de solo lectura (Caso Portuaria, pág. 11).

A nivel de infraestructura física, el soporte es frágil. La sala de servidores principal (habilitada en 2012 con 34 m²) se ubica a menos de 300 metros de la costa, posee apenas 25 minutos de respaldo eléctrico y no cumple con los estándares técnicos exigidos (Caso Portuaria, pág. 12). La conectividad inalámbrica del patio data de 2013 y sufre zonas de sombra variables debido al movimiento constante de las pilas metálicas de contenedores (Caso Portuaria, pág. 12). Por otro lado, las redes operacional, administrativa y de control de acceso comparten la misma infraestructura de conmutación con 142 cámaras de videovigilancia, lo que ha provocado una degradación observada del sistema operativo durante eventos de alta demanda de CCTV (Caso Portuaria, págs. 11-12). Finalmente, el enlace de datos principal cuenta con un respaldo por radioenlace que no ha sido probado en conmutación real desde el año 2022 (Caso Portuaria, pág. 12).

## 2.3 Problemas, causas y consecuencias

*   **Gate y flujo de camiones.** El camión permanece en el terminal muy por sobre el tiempo comprometido, y en episodios de alta demanda la fila desborda hacia la vía pública. La causa raíz es que no existe sistema de citas ni validación previa de documentación, y el código del contenedor (11 caracteres) se digita a mano en el gate. Como consecuencia, la estadía promedia 78 minutos frente a los 45 comprometidos contractualmente con el concedente, y el 12 de marzo de 2026 se registró una fila de 3,2 km con 140 camiones que motivó intervención municipal, marítima y del concedente (Caso Portuaria, págs. 5, 11, 15).
*   **Patio y ubicación de contenedores.** Una parte relevante de los movimientos de patio no agrega valor, y localizar físicamente un contenedor toma un tiempo considerable. La causa raíz es que la posición de cada contenedor se decide por criterio del operador, sin regla escrita ni registro del motivo de la ubicación. Como consecuencia, el 18% de los movimientos de patio son remociones evitables, el 3,1% de los contenedores queda registrado en una posición incorrecta, y la búsqueda física de un contenedor demora 40 minutos en promedio (Caso Portuaria, págs. 10, 15).
*   **Patio refrigerado / cadena de frío.** Una falla en la cadena de frío puede pasar varias horas sin ser detectada. La causa raíz es que el control de las 2.400 tomas y los 26 tableros se realiza mediante rondas manuales cada 4 horas, sin instrumentación remota. Como consecuencia, el 18 de febrero de 2026 una falla de tablero dejó 38 contenedores de cerezas 9 horas sin energía, con una pérdida de US$620.000 y la salida del exportador afectado del terminal (Caso Portuaria, págs. 5, 11, 15).
*   **Planificación de estiba y patio.** La operación depende de una sola persona para decisiones críticas de planificación. La causa raíz es que el conocimiento de reglas tácitas (fallas de equipos, restricciones por cliente, zonas que se inundan) nunca se documentó, y solo lo tiene el planificador con 29 años en el cargo. Como consecuencia, existe un riesgo declarado de continuidad operativa a partir de 2028, cuando esa persona se jubila (Caso Portuaria, pág. 14).
*   **Navieras y mensajería.** El intercambio de información con las navieras no está estandarizado. La causa raíz es que el 41% de las instrucciones de embarque llega por correo y se digita a mano, y coexisten 6 formatos distintos de plano de estiba. Como consecuencia, el terminal no está en condiciones de cumplir las tres exigencias que la alianza naviera (34% de los contenedores) impondrá desde 2029: mensajería estándar, ventana confirmada con 72 horas y reporte verificado de emisiones (Caso Portuaria, págs. 5, 14).
*   **Facturación.** Una parte relevante de las facturas se objeta, y muchas de esas objeciones se aceptan sin poder demostrar lo contrario. La causa raíz es que los hechos facturables se reconstruyen desde el sistema de operación y planillas, sin evidencia sistemática que los respalde. Como consecuencia, el 4,7% de las facturas es objetado, y el 62% de esas objeciones se acepta por falta de evidencia (Caso Portuaria, págs. 11, 12, 15).
*   **Personas y control de acceso.** No se sabe con precisión cuántas personas hay en el recinto ni bajo qué habilitación en un momento dado. La causa raíz es que los trabajadores eventuales (hasta 380 por turno) se habilitan mediante listados impresos entregados en portería. Como consecuencia, en una emergencia el número y la ubicación de las personas dentro del recinto no es exacto (Caso Portuaria, págs. 12, 19, 45).
*   **Infraestructura y continuidad.** La infraestructura física y de red no da garantías de continuidad ante un incidente. La causa raíz es que la sala de servidores no cumple el estándar exigido, las redes operacional, administrativa y de protección comparten conmutación, y el respaldo por radioenlace no se prueba en conmutación real desde 2022. Como consecuencia, existe un riesgo de pérdida de servicio ante un incidente físico o de red que a la fecha no ha sido validado (Caso Portuaria, págs. 13, 14).

## 2.4 Magnitud cuantitativa y líneas base

| Indicador | Valor Actual | Meta | Fuente |
| :--- | :--- | :--- | :--- |
| Cumplimiento de ventana de atraque | 71% | 90% | (Caso Portuaria, pág. 14) |
| Productividad efectiva de grúa | 24,8 movimientos por hora | 30 desde 2029 | (Caso Portuaria, págs. 10, 14) |
| Instrucciones recibidas por correo y digitadas | 41% | 0 | (Caso Portuaria, págs. 5, 14) |
| Formatos distintos de plano de estiba | 6 | 1 | (Caso Portuaria, pág. 14) |
| Personas capaces de planificar estiba/patio | 1 | Sin dependencia | (Caso Portuaria, pág. 14) |
| Remociones de patio | 18% | Reducción Medible | (Caso Portuaria, pág. 15) |
| Contenedores mal ubicados | 3,1% | Posición real y con registro | (Caso Portuaria, pág. 15) |
| Búsqueda física de un contenedor | 40 min. | Sin búsquedas físicas | (Caso Portuaria, pág. 15) |
| Inspecciones atrasadas | 28% | Disponibilidad a la hora acordada | (Caso Portuaria, págs. 11, 15) |
| Tableros refrigerados instrumentados | 0/2.400 y 0/26 | Instrumentación y alarma remota | (Caso Portuaria, pág. 15) |
| Pérdida evento 18-feb-2026 | 38 contenedores, 9 h, US$620.000 | No aplica | (Caso Portuaria, págs. 5, 11, 15) |
| Estadía del camión | 78 min | 45 min | (Caso Portuaria, págs. 11, 15) |
| Fila máxima registrada | 3,2 km, 140 camiones | Sin desborde en la vía pública | (Caso Portuaria, págs. 5, 15) |
| Documentación de camión defectuosa | 22% | <5% | (Caso Portuaria, pág. 15) |
| Discrepancia de masa bruta sobre tolerancia | 6% | < 1% | (Caso Portuaria, pág. 15) |
| Facturas objetadas (sin evidencia) | 4,7% (62% de esas aceptadas) | <1% | (Caso Portuaria, pág. 15) |
| Emisiones por contenedor | No se mide | Reporte verificado desde 2029 | (Caso Portuaria, pág. 15) |
| Dependencia de planificación única / soporte del sistema de operación | Vencen en 2028 | No aplica | (Caso Portuaria, pág. 14) |

En terminales convencionales no automatizados, la productividad de grúa (GMPH) suele ubicarse entre 20 y 30 movimientos por hora, y los terminales automatizados superan los 40 (Loadmaster.ai, 2026); el terminal opera en el extremo bajo de ese rango y por debajo de lo que le exige su cliente más relevante. La referencia de industria para estadía de camión ronda 30-45 minutos promedio (Opsima, 2026); el terminal está muy por sobre ese umbral. El monitoreo remoto de contenedores refrigerados mediante sensores es práctica estándar en la industria del frío marítimo (Kalliagra et al., 2022); el terminal no cuenta con ningún punto instrumentado.

## 2.5 Actores y grupos de interés

Los actores se agrupan primero en humanos (personas o colectivos de personas que participan directamente en la operación) y no humanos (organizaciones, empresas u organismos externos que se relacionan con el terminal como entidad). Dentro de cada grupo se clasifican en complejos (inciden en más de un dominio del problema, o concentran poder de decisión o de veto), medios (dominio acotado, pero con influencia real sobre el resultado) y simples (rol operativo, acotado a una interacción puntual). Esta clasificación de complejidad es una Propuesta de Terabyte: describe la complejidad del rol del actor frente al problema actual, no la complejidad de su futura interacción con un sistema.

### Actores Humanos

**Entre los actores humanos complejos están:**
*   **Gerencia general**, responsable ante el concedente y el directorio, cuyo interés es alto por el riesgo contractual y reputacional, y que fija la restricción de no aumentar el riesgo de las personas.
*   **Gerencia de operaciones**, dueña de la operación diaria, para quien arreglar el gate sin resolver el patio solo traslada la cola hacia adentro del recinto.
*   **Gerencia comercial**, responsable de la relación con las navieras, que objeta que las condiciones de la alianza naviera para 2029 hayan quedado últimas en la priorización del comité.
*   **Planificador de estiba y patio**, que concentra un conocimiento crítico no documentado y cuya salida en 2028 es un riesgo declarado por el propio mandante.
*   **Jefatura de protección portuaria**, con responsabilidad indelegable en una emergencia y poder de veto sobre cualquier solución que aumente el riesgo, que objeta la biometría obligatoria por la posición de los sindicatos.
*(Caso Portuaria, págs. 6-8, 16-20)*

**Entre los actores humanos medios están:**
*   **Jefatura de gate**, acotada a ese dominio pero que pide explícitamente un sistema de citas; la jefatura de energía y patio refrigerado, que advierte sobre la fragilidad de la radiopropagación en un patio cargado.
*   **Área de tecnologías de información**, de solo 5 personas, que hereda la operación de cualquier solución pero no dispone hoy de documentación del sistema de 2012.
*   **Trabajadores eventuales y sus sindicatos** (hasta 380 por turno), cuya influencia se concentra en un tema puntual pero de alto impacto: la objeción expresa a la biometría obligatoria.
*(Caso Portuaria, págs. 16-20, 32)*

**Entre los actores humanos simples están:**
*   **Actor operador de grúa de muelle**: ejecuta el movimiento crítico del ciclo de la nave, pero su rol está acotado a esa tarea; su relevancia para el diseño está en que no aceptará ninguna interacción que exija botones o atención de pantalla mientras opera.
*(Caso Portuaria, pág. 14)*

### Actores no humanos

**Entre los actores no humanos complejos están:**
*   **Concedente estatal**, que fiscaliza múltiples indicadores de la concesión y ya acumula 3 semestres consecutivos de incumplimiento del indicador de estadía del camión.
*   **Alianza naviera**, que representa el 34% de los contenedores del terminal e impone tres condiciones no negociadas que cruzan varios dominios a la vez (mensajería estándar, ventana de 72 horas y reporte verificado de emisiones) con plazo fijo en 2029 (CP, pp. 5, 14, 21-22).
*(Caso Portuaria, págs. 5, 14, 21 - 22)*

**Entre los actores no humanos medios están:**
*   **13 líneas navieras**, con una relación acotada al intercambio de instrucciones y planos de estiba pero con una madurez desigual para adoptar mensajería estándar.
*   **Autoridades marítima, aduanera, SAG y sanitaria**, cuyo rol regulatorio está bien definido pero cuya coordinación con la operación falla en el 28% de las inspecciones.
*(Caso Portuaria, págs. 11, 14-15, 24-25)*

**Entre los actores no humanos simples están:**
*   **380 empresas de transporte terrestre**, cuya relación con el terminal se acota al gate y a la documentación del camión, y que no controlan cuándo está lista la carga que transportan.
*   **210 agencias de aduana junto a los cerca de 1.400 exportadores e importadores**, cuya relación se acota al proceso documental y al portal de clientes, que hoy prefieren resolver por teléfono antes que usarlo.
*(Caso Portuaria, págs. 6-8, 11)*

## 2.6 Contexto regulatorio y compromisos externos

El caso exige investigar y materializar controles concretos respecto de cada marco regulatorio: 
*   **Contrato de concesión:** Exige trazabilidad inalterable de la hora de entrada y salida del camión para auditar el indicador de 45 minutos.
*   **ISPS/PBIP y Ciberseguridad (Ley N° 21.663):** Exige segregación física/lógica de redes y control de acceso estricto a las instalaciones, limitando soluciones inalámbricas abiertas.
*   **Zona primaria aduanera:** Exige que la solución integre autorización y registro auditable para cada movimiento de mercancía.
*   **SOLAS VGM:** Exige integración directa con básculas para evitar discrepancias de digitación sobre el 6% actual.
*   **Trazabilidad cadena de frío:** Exige almacenamiento inalterable de series de temperatura como evidencia comercial y regulatoria.
*   **Seguridad y salud en faenas:** Impone la restricción crítica de no utilizar pantallas interactivas para personal en movimiento.

## 2.7 Restricciones no negociables

La propuesta debe diseñarse respetando un conjunto de catorce restricciones intocables definidas por el mandante, las cuales invalidan cualquier solución que las transgreda, independiente de su mérito técnico. Terabyte las ha agrupado en cuatro dimensiones críticas:

*   **Seguridad y Vida Humana:** Ninguna solución puede aumentar la exposición al riesgo en el patio. Se rechazará cualquier alternativa que obligue al operador a interactuar con dispositivos (mirar pantallas o presionar botones) mientras haya equipos pesados en movimiento. Adicionalmente, se prohíbe el uso de biometría obligatoria para los trabajadores eventuales.
*   **Continuidad y Operación Offline:** El terminal opera bajo un régimen 24x7x365 sin ventana de detención total. Ante la pérdida de enlace de datos hacia el exterior, la operación del muelle y del gate debe poder continuar de forma ininterrumpida durante 72 horas sin pérdida de registros.
*   **Congelamiento y Ventanas de Intervención:** Queda estrictamente prohibido intervenir los sistemas operativos entre el 15 de diciembre y el 30 de abril (temporada de fruta). Tampoco se permite intervenir durante la atención de una nave ni en las cuatro horas previas a una ventana de atraque confirmada.
*   **Ecosistema y Arquitectura:** El sistema de control de las grúas de muelle es cerrado (solo admite lectura sujeta a autorización del fabricante). El ERP actual se mantendrá como único emisor tributario. Además, es obligación segregar la red operacional de la red administrativa y del sistema de videovigilancia. Finalmente, las interfaces internacionales (navieras/clientes) deben ser bilingües (español/inglés).

## 2.8 Supuestos del análisis

Dado que el mandante describe una operación con vacíos de información explícitos, Terabyte establece los siguientes supuestos sobre la naturaleza del problema, los cuales dimensionan la urgencia y complejidad del desafío operativo:

*   **Obsolescencia del Sistema Core y Fecha de Soporte:** Se asume que el terminal no posee código fuente ni documentación de las personalizaciones del sistema de 2012. Ante la ambigüedad de las bases sobre el mes exacto de vencimiento de su soporte, se adopta el supuesto conservador de que este expira el 1 de enero de 2028. La vulnerabilidad operativa a partir de esa fecha es absoluta y define el plazo máximo para cualquier mitigación estructural.
*   **Naturaleza del colapso del Gate y Saturación Asimétrica:** Se asume que las filas estructurales (como la de 3,2 km) no son producto exclusivo del aumento de volumen estacional, sino de llegadas masivas asimétricas (ej. madrugadas tras el cierre de los packings frutícolas) chocando contra un cuello de botella documental (22% de errores). Esto convierte a los "lunes de temporada" en el escenario de estrés estándar que debe soportarse, no en una anomalía imprevisible.
*   **Riesgo inminente de continuidad humana:** Se asume que el conocimiento tácito del planificador de estiba no cuenta con ningún respaldo paralelo. Su rescate debe iniciar desde el primer día y abarcar al menos una temporada de fruta completa, asumiendo que reglas críticas (como zonas inundables o generadores limitados) tienen una fuerte variabilidad estacional. Su jubilación sin esta captura generaría una parálisis en muelle y patio.
*   **Ultimátum comercial inflexible:** Se asume que el plazo de 2029 impuesto por la alianza naviera no es una declaración de intenciones, sino una condición comercial rígida. El incumplimiento de las exigencias tecnológicas resultará en la pérdida directa e irreversible del 34% del volumen de transferencia del terminal.
*   **Invisibilidad estructural y física en el patio refrigerado:** Se asume que el incidente del 18 de febrero (9 horas sin detección de falla) refleja el comportamiento estándar del diseño de control actual. Asimismo, se asume que las zonas de sombra inalámbricas se deben a la física cambiante del recinto (pilas metálicas que mutan cada hora creando "jaulas de Faraday"), garantizando que las desconexiones de los 2.150 reefers en temporada se repetirán si se mantiene la dependencia del control ciego o de redes no adaptadas a esta física.
*   **Sobrecarga crítica del equipo TI:** Se asume que el equipo actual de 5 personas operando al 100% en labores de soporte reactivo tiene una capacidad operativa nula para absorber tareas manuales de contingencia, extracciones complejas de datos o caídas del sistema legado.
*   **Vulnerabilidad en emergencias por alta rotación:** Se asume que la rotación diaria de hasta 380 trabajadores eventuales genera una obsolescencia inmediata en los listados impresos de acceso. Ante un siniestro, esta mecánica manual impide garantizar legal y operativamente quién se encuentra realmente expuesto.

## 2.9 Síntesis de la necesidad

Terminal Portuario Aconcagua S.A. se encuentra operando al límite de sus capacidades físicas, sostenido por un esfuerzo humano intensivo y un ecosistema tecnológico fragmentado y próximo a la obsolescencia. El problema de fondo no se resuelve simplemente adquiriendo software, sino orquestando un entorno donde interactúan personas, cargas de alto valor y maquinaria pesada compitiendo por recursos finitos (tres sitios, seis grúas y 18 hectáreas).

La verdadera necesidad de la compañía radica en transformar un modelo operativo reactivo y ciego en uno predictivo y trazable. Requiere erradicar el trabajo sin valor (como las remociones improductivas y las búsquedas físicas), asegurar la cadena de frío mediante monitoreo continuo, eliminar la congestión estructural del gate y estandarizar la comunicación naviera. Todo esto debe lograrse asegurando el relevo tecnológico del sistema de 2012 y el relevo generacional de la planificación antes de 2028, cumpliendo paralelamente con los estrictos SLA del concedente y las imposiciones internacionales para 2029, sin sumar ni un ápice de riesgo a la vida humana en terreno.

## Referencias
*   Justas. (2026, January 30). GMPH optimization in container terminal operations. loadmaster.ai. https://loadmaster.ai/gmph-optimization-in-terminal-operations/
*   Benny, B. (2026, August 9). Port Operations KPIs: 25 metrics to run a faster, safer terminal. Opsima Blog. https://opsima.com/blog/kpis/port-operations-kpis/
*   Cil, A.Y., Abdurahman, D. & Cil, I. Internet of Things enabled real time cold chain monitoring in a container port. J. shipp. trd. 7, 9 (2022). https://doi.org/10.1186/s41072-022-00110-z