# Maestro de contexto de arquitectura — Caso 06 Portuaria

**Versión:** 1.0  
**Fecha de corte:** 2026-09-04  
**Propósito:** base única y trazable para los tres frentes del Subdocumento 4  
**Estado:** vigente para iniciar; los asuntos marcados `POR VALIDAR` no pueden convertirse en hechos confirmados

## 0. Cómo usar este maestro

Este archivo contiene las verdades, restricciones, decisiones y magnitudes que condicionan la arquitectura. **No distribuye tareas**: esa función corresponde a [`01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md).

Reglas de lectura:

1. Una afirmación arquitectónica debe poder volver a una fuente mediante un identificador estable: capítulo/materia, `RF-*`, `RNF-*`, `RN-*`, decisión, supuesto o `MC-*`.
2. Los números de línea son auxiliares; no sustituyen al identificador estable ni al título de la sección.
3. `DECISIÓN TERABYTE`, `SUPUESTO`, `PENDIENTE CLIENTE` y `HECHO DE BASES` no son equivalentes y deben conservar su etiqueta.
4. Un dato pendiente se diseña mediante interfaz, rango, mecanismo de levantamiento o fallback; nunca se completa inventándolo.
5. Si el proyecto pasa a un repositorio Git, se debe registrar en este encabezado el commit que congela Célula 2. Mientras eso no ocurra, el corte documental es la versión auditada del 2026-09-04.

## 1. Jerarquía de fuentes

Ante contradicción se aplica el siguiente orden:

1. PDF oficial del Caso 06 Portuaria (`FEP03`).
2. PDF de Bases Técnicas Transversales (`FEP02`).
3. PDF de Bases Administrativas (`FEP01`).
4. [`Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md) y archivos vigentes de Célula 2, como implementación corregida y registro del tratamiento `MC-01..30`.
5. Material docente de arquitectura, como guía de representación; nunca prevalece sobre las Bases ni el caso.

El Maestro de Correcciones y los resúmenes de análisis utilizados durante la preparación se consideran antecedentes ya absorbidos por este documento y por el cierre auditado de Célula 2. No son necesarios en el repositorio compartido. Si surge una contradicción nueva, se contrasta contra los PDF oficiales disponibles por el canal común del equipo.

### 1.1 Regla para códigos RT repetidos

Nunca citar solo `RT-xx.xx`. La referencia mínima es:

> documento + capítulo/numeral + código + materia

Ejemplo válido: `Caso 06, Cap. 15, RT-10.05 — retorno y tiempo máximo por intervención`.

## 2. Qué debe demostrar el Subdocumento 4

El Subdocumento 4 representa **32 % del Informe 1**:

| Bloque | Peso | Contenido exigido |
|---|---:|---|
| 4.1 Arquitectura lógica | 16 % | a) Esquema de solución; b) arquitectura lógica de la solución |
| 4.2 Arquitectura física | 16 % | a) arquitectura física; b) tecnologías de software; c) implementos de hardware y software; d) data center primario; e) data center secundario; Formulario T-11 |

Cobertura contractual mínima, conforme al Subdocumento 4/T-7:

| ID local | Obligación | Evidencia final mínima |
|---|---|---|
| `SD4-01` | Capas, módulos, límites de contexto, responsabilidades e interfaces | Esquema de solución, diagrama lógico y catálogo de componentes |
| `SD4-02` | Emplazamiento nube/on-premise por componente conforme al Art. 16 | Diagrama físico y tabla de emplazamiento con seis criterios |
| `SD4-03` | Servicios, contratos, mensajería, versionado y gobierno | Diagrama y matriz de integraciones |
| `SD4-04` | Zero Trust, capa expuesta, identidad, cifrado y controles | Vista de seguridad y matriz control–componente–evidencia |
| `SD4-05` | Ambientes, redes, alta disponibilidad, DR y respaldos | Vista de despliegue/continuidad |
| `SD4-06` | Dimensionamiento y capacidad | Cálculos con volumen, concurrencia, peak y crecimiento |
| `SD4-07` | Decisiones registradas | ADR fechados con alternativas y criterio de selección |
| `SD4-08` | Arquitectura propia del caso | Actores, zonas, restricciones, fallos y magnitudes portuarias reales |

El documento debe usar vistas coherentes con ISO/IEC/IEEE 42010: lógica, procesos, despliegue, datos y seguridad. Un diagrama genérico o sin correspondencia con el Caso 06 no cumple.

### 2.2 Línea base documental de Célula 2

El corte corregido y auditado que recibe arquitectura contiene:

| Artefacto | Cantidad/estado |
|---|---:|
| RF vigentes | 138 IDs únicos: 82 Etapa 1 + 56 Etapa 2 |
| RNF vigentes | 84 IDs únicos en 9 categorías |
| Decisiones | 21: las 20 solicitadas por el caso + coordinación de inspecciones |
| Metas | 17: 15 con valor y 2 expresamente sin meta |
| Supuestos | 25 |
| Reglas de negocio | 10 |
| Correcciones del Maestro | MC-01..MC-30 tratadas |
| Observaciones de disposición | 31 aceptadas; 0 rechazadas |

La arquitectura no reproduce las 222 fichas RF/RNF. Debe extraer todas sus consecuencias y citar los IDs que respalden componentes, controles, interfaces, capacidad y criterios de aceptación.

### 2.1 Formulario T-11

El T-11 final usa exactamente estas columnas:

1. Componente.
2. Producto / servicio ofertado.
3. Ubicación / lugar.
4. Cantidad.
5. Justificación.

Todo componente físico, servicio de plataforma, licencia o hardware efectivamente ofertado debe aparecer. No se crea una fila por cada módulo lógico. Cada fila debe corresponder con un componente del diagrama físico y con su cálculo o justificación. **El Informe 1 no debe incluir precios, tarifas ni montos económicos.**

## 3. Línea base de la solución heredada

La solución se diseña como una **plataforma portuaria modular e híbrida**:

1. Núcleo operacional local resiliente para mantener nave, movimientos, posición, gate, reefer y hechos facturables durante 72 horas sin enlace exterior.
2. Plataforma central modular para reglas, flujos, identidad, auditoría, notificaciones e integración.
3. Canales sobre capacidades compartidas: aplicación móvil instalable, portal público/autenticado, interfaces de cabina y terminales de patio, y adaptadores para correo, mensajería, radio y mensajería marítima.
4. Capa de servicios/anticorrupción frente al TOS 2012, con coexistencia bidireccional, autoridad explícita, conciliación y retorno probado.
5. Subsistemas conservados: ERP, control de grúas, control de acceso, barreras, CCTV/VMS, básculas y sistemas externos. Se integran sin apropiarse de su responsabilidad.

No es una colección de aplicaciones independientes ni un microservicio por requisito. El bajo volumen de negocio estimado y la capacidad de TI del CLIENTE obligan a una solución operable.

### 3.1 Estilo arquitectónico que debe decidirse

Comparar al menos:

- núcleo modular con pocos servicios separados por continuidad, seguridad, escala o patrón de datos;
- servicios más distribuidos por dominio.

La selección debe considerar complejidad operacional, resiliencia, autonomía de 72 h, volumen, costo de infraestructura y capacidad de un equipo TI de **5 personas**. Se debe evitar tanto el monolito rígido como la fragmentación injustificada.

## 4. Contexto del caso que mueve la arquitectura

### 4.1 Magnitudes base

| Magnitud | Actual | Horizonte/proyección relevante |
|---|---:|---:|
| Transferencia anual | 780.000 TEU / 486.000 contenedores | 920.000 TEU / 570.000 |
| Naves/año | 620 | 700 |
| Frente de atraque | 3 sitios, 940 m, calado 14,2 m | posible cuarto sitio 2030–2032 |
| Patio | 18 ha / 12.400 TEU | debe crecer sin rediseño rígido |
| Tomas reefer | 2.400 / 26 tableros | 2.900 / 32 tableros |
| Camiones/día | 1.450 promedio / 2.600 peak | 1.700 / 3.100 |
| Equipos | 6 grúas muelle, 18 patio, 42 tractocamiones, 14 pesados | hasta 88 equipos instrumentables |
| Gate | 8 entradas + 6 salidas | 10 + 8 |
| Personas en recinto peak | 1.100 | 1.300 |
| Eventuales por turno peak | hasta 380 | rotación diaria por nombrada |
| Navieras | 14; alianza equivale a 34 % de contenedores | 16 |
| CCTV | 142 | 190 |
| TI del CLIENTE | 5 personas | restricción de operabilidad |

Fuentes de control: `Caso 06 Portuaria (FEP03), capítulos 1, 2, 6, 7 y 14`, y [`Celula2/plantilla_volumetria_caso_portuaria.md`](../../Celula2/plantilla_volumetria_caso_portuaria.md).

### 4.2 Detonantes y consecuencias técnicas

- Fila de 3,2 km y 140 camiones: gate, citas, cola virtual, trazabilidad de entrada/salida y disponibilidad no pueden ser accesorios.
- Falla reefer: 38 contenedores perdidos; se requiere instrumentar tomas/tableros, alarmas redundantes, confirmación y continuidad local.
- Jubilación del planificador y fin de soporte TOS durante 2028: captura de reglas desde mes 1, capa anticorrupción y estrategia de sustitución/retorno.
- Programa 2029: mensajería estándar exclusiva para la alianza, ventana ≥72 h, productividad ≥30 movimientos/h por grúa y emisiones verificadas.
- Equipos pesados y personas comparten espacio: ninguna interfaz o automatización puede aumentar la exposición al riesgo.

### 4.3 Condiciones físicas existentes

- Fibra de un proveedor y radioenlace de respaldo sin prueba real de conmutación desde 2022.
- Sala de 34 m², de 2012, a menos de 300 m del mar; split, UPS de 25 min y acceso por llave: no cumple la base transversal.
- Ambiente salino y corrosión acelerada.
- Red inalámbrica de 2013 con sombras móviles por pilas metálicas de hasta cinco alturas.
- Redes operacional, administrativa y CCTV comparten conmutación.
- 26 tableros reefer sin instrumentación remota.
- Respaldo energético reefer nunca verificado a carga total de temporada.

Estas condiciones impiden dibujar una arquitectura física genérica.

### 4.4 Catorce restricciones no negociables

| # | Restricción que debe verse en la arquitectura |
|---:|---|
| 1 | ninguna interfaz aumenta la exposición de personas al riesgo del patio |
| 2 | operación 24x7x365, sin ventana de detención total |
| 3 | control de grúas de muelle no se interviene; solo lectura autorizada |
| 4 | muelle y gate continúan ante pérdida de enlace sin perder registro |
| 5 | ERP se mantiene como único emisor tributario |
| 6 | red operacional segregada de administrativa y protección |
| 7 | condición ISPS/OIV; nada compromete el plan de protección aprobado |
| 8 | eventuales por nombrada; biometría obligatoria objetada |
| 9 | ninguna intervención entre 15-dic y 30-abr |
| 10 | ninguna intervención durante nave ni cuatro horas antes |
| 11 | TI del CLIENTE tiene 5 personas; capacidades especialistas deben ser operables/serviciadas |
| 12 | equipos de zona operativa requieren protección IP y comportamiento marino por clase |
| 13 | interfaces/mensajes/mesa de ayuda en español e inglés |
| 14 | indicadores del concedente producidos trazable y oportunamente; no reconstruidos |

### 4.5 Exclusiones que igualmente condicionan el diseño

- No reemplazar ERP ni emisión tributaria.
- No intervenir, modificar o automatizar control de grúas de muelle.
- No administrar remuneraciones/nombrada; sí habilitar y controlar acceso de asignados.
- No electrificar flota; sí medir por separado 16 equipos diésel y 2 eléctricos para emisiones.
- No construir infraestructura civil; sí especificarla técnicamente para que el CLIENTE la ejecute.
- No desarrollar sistemas de autoridades; sí integrarse cuando exista interfaz y ofrecer fallback.
- No operar/certificar báscula; sí capturar y trazar VGM.
- No comprar hardware; sí especificar qué, cuánto y con qué características.

### 4.6 Umbrales del Caso 06 que endurecen la arquitectura

| Materia | Umbral/regla obligatoria |
|---|---|
| crecimiento | cuarto sitio, grúas, bloques y tomas por parametrización, sin rediseño |
| desconexión | 72 h; terminales de patio hasta 8 h fuera de cobertura sin pérdida |
| reconexión | sincronización automática ≤90 min con conflictos deterministas |
| red de patio | radiopropagación con patio cargado, segregación y failover real de radioenlace |
| posición/movimiento | posición posterior ≤30 s; confirmación movimiento ≤1 s; consulta ≤1 s |
| gate/OCR/portal | camión completo ≤120 s; OCR ≤3 s; portal ≤60 s |
| reefer | alarma ≤5 min; 100 % tomas/tableros comprometidos según etapa |
| KPI | grúa/estadía en tiempo real por hora/equipo; concedente ≤1 h tras turno |
| peak | coincidencia de dos naves y gate saturado; pruebas a 1,5× peak declarado |
| seguridad de campo | cifrar datos personales, comerciales y los que infieran contenido/ruta |
| usuarios de terreno | tres turnos, 380 eventuales/turno, compartidos, guantes/intemperie |
| firma | instrucciones embarque, recepción/entrega, acta inspección y hechos facturables |
| notificaciones | frío con canal redundante, escalamiento y confirmación identificada; adaptadores por audiencia |
| soporte | 24x7x365 ES/EN y clases diferenciadas nave, gate y frío |
| marcha blanca | presencia en terreno en los tres turnos, con habilitación ISPS |

### 4.7 Criterios de aceptación que la arquitectura debe habilitar

1. estadía del camión desde 78 hacia 45 min, sostenida y auditable;
2. ninguna fila que desborde a vía pública;
3. documentación validada antes de que el camión salga a ruta;
4. reconocimiento automático del contenedor en gate;
5. ventana confirmada ≥72 h y cumplida;
6. productividad ≥30 movimientos/h por grúa, medida por hora/equipo;
7. planificación sin dependencia de una persona;
8. remociones mediblemente reducidas;
9. posición real/registrada consistente y sin búsqueda física normal;
10. contenedor de inspección disponible a la hora;
11. falla reefer detectada/notificada en minutos en cualquier turno;
12. registro continuo de temperatura como evidencia;
13. mensajería estándar sin digitación;
14. hecho facturable con evidencia suficiente;
15. autoservicio sin teléfono/mostrador;
16. emisiones verificables por contenedor;
17. personas en recinto identificadas y habilitadas;
18. 72 h sin enlace sin pérdida;
19. redes segregadas;
20. indicadores del concedente sin reconstrucción;
21. plan en cabina sin radio ni apartar la vista de la carga;
22. continuidad de planificación después del retiro de Nibaldo.

### 4.8 Metas propias de Célula 2 relevantes para capacidad/aceptación

- remociones ≤14 % fuera del peak estacional; peak informado por separado;
- 100 % de posiciones conocidas correctas y ≤0,5 % `por verificar` al cierre;
- búsqueda física: cero normal; residual ≤0,5 % resuelto ≤15 min;
- instrumentación: 74/74 equipos actuales y 88 proyectados;
- reefer: control ≤5 min, 2.400/2.400 tomas y 26/26 tableros; proyección 2.900/32;
- inspecciones atrasadas ≤12 %, condicionada a aviso de autoridad;
- OCR de código de contenedor ≥98 %;
- carril de excepción ≥50 % más lento que validado;
- atención con cita cumplida ≥30 % más rápida;
- redigitación 0 % para alianza; ≤5 % solo otras navieras al cierre Etapa 2;
- reconciliación de combustible ±3 % en tres meses;
- error de barrido de inventario ≤0,5 %.

Las metas sin control directo —ocupación del patio y pérdida histórica del incidente reefer— no se convierten en promesas falsas; se usan como parámetro o antecedente.

## 5. Actores y sistemas que no se pueden omitir

### 5.1 Actores humanos/organizacionales

| ID | Actor/grupo | Interacción arquitectónica principal |
|---|---|---|
| `ACT-OPS` | Operación y supervisores de turno | decisiones operacionales, retorno, alarmas y excepciones |
| `ACT-PLAN` | Planificador de patio/estiba | aprobación/corrección, reglas tácitas, catálogo dinámico |
| `ACT-GATE` | Operadores de gate | validación, entrada/salida, excepciones |
| `ACT-REEFER` | Operadores y supervisores reefer | alarmas, rondas, intervención y confirmación |
| `ACT-MANT` | Mantenimiento/energía | equipos, tableros, continuidad y evidencia |
| `ACT-TI` | Área TI del CLIENTE | administración y operación posterior; 5 personas |
| `ACT-EVT` | Eventuales por nombrada | credencial temporal, terminal compartida, guantes/intemperie |
| `ACT-GRU` | Operadores de equipos/grúa | indicaciones de cabina; sin confirmación rutinaria manual |
| `ACT-COM` | Comercial/facturación | hechos facturables, objeciones y portal |
| `ACT-NAV` | Navieras y alianza | BAPLIE, COPRAR, COARRI, CODECO |
| `ACT-AGE` | Agencias, importadores/exportadores y clientes | portal, documentos, trazabilidad y objeciones |
| `ACT-TRA` | Transportistas | citas, validación previa, cola virtual y gate |
| `ACT-AUT` | Aduana, SAG y autoridad marítima/sanitaria | inspecciones, resultados, actas e interfaces/fallback |
| `ACT-FER` | Operador ferroviario | coordinación, arribo, entrega/recepción y excepciones |
| `ACT-CON` | Concedente | indicadores trazables y auditables |
| `ACT-VER` | Verificador de emisiones | suficiencia de historia y verificación efectiva |

### 5.2 Sistemas y activos externos/conservados

| ID | Sistema/activo | Límite de responsabilidad |
|---|---|---|
| `EXT-TOS12` | TOS 2012 | legado envuelto; interfaz real por levantar |
| `EXT-ERP` | ERP/facturación | único emisor tributario; recibe hechos/evidencia |
| `EXT-GRU` | Control de grúas | solo lectura y sujeto a autorización del fabricante |
| `EXT-ACC` | Control de acceso y barreras | conserva autoridad física; integración de habilitación/eventos |
| `EXT-VMS` | CCTV/VMS | se conserva; no crear portal de video ni transportar video por red operacional sin justificación |
| `EXT-VGM` | Básculas | captura y trazabilidad; la solución no opera ni certifica la báscula |
| `EXT-OCR` | Lectores/OCR | eventos e imágenes de patente/contenedor |
| `EXT-NAV` | Sistemas de navieras | contratos/versiones por contraparte |
| `EXT-AUT` | Sistemas/canales de autoridades | API/archivo si existe; canal asistido trazable si no existe |
| `EXT-FER` | Sistema/canal ferroviario | contrato por levantar |
| `EXT-RAD` | Radio operacional | medio existente integrado; no se inventa un sistema nuevo |

## 6. Ocho capas obligatorias y reglas lógicas

| Capa | Contenido obligatorio en esta solución |
|---|---|
| 1. Presentación | portal, app instalable, cabinas y terminales; sin lógica de negocio ni acceso directo a datos |
| 2. Borde y exposición | único punto público, CDN, WAF, anti-DDoS L3/L4/L7 y TLS 1.3 |
| 3. Puerta de enlace de servicios | autenticación/autorización, cuotas, rate limit, catálogo, versionado, esquema y trazabilidad |
| 4. Servicios de negocio | módulos/bounded contexts, responsabilidad explícita, contratos versionados; componentes críticos desplegables según frontera justificada |
| 5. Integración y eventos | bus/broker persistente, DLQ, reintento, deduplicación, orquestación/coreografía y adaptadores |
| 6. Datos | transaccional, analítico, documental, series temporales y archivos separados según necesidad; cifrado y ciclo de vida |
| 7. Seguridad transversal | identidad, autorización, secretos, cifrado, auditoría y detección en todas las capas |
| 8. Observabilidad transversal | métricas, logs y trazas correlacionadas nube/on-premise sin puntos ciegos, compatibles con OpenTelemetry |

Los actores y canales se dibujan fuera del límite de la solución; no constituyen una novena capa formal.

### 6.1 Catálogo lógico inicial

Estos identificadores permiten trabajar en paralelo. El Frente 1 puede refinarlos, pero cualquier cambio debe actualizar la matriz global y comunicarse en una puerta de integración.

| ID | Componente/contexto | Responsabilidad principal |
|---|---|---|
| `CH-PORTAL` | Portal público/autenticado | estado mínimo seguro, acceso, congestión, trámites y autoservicio |
| `CH-APP` | App móvil instalable | cuatro perfiles; offline cifrado para perfiles internos |
| `CH-CAB` | Interfaz de cabina/terreno | indicaciones visuales y alertas de seguridad, uso con guantes |
| `GW-EDGE` | Borde público | protección y terminación de tráfico expuesto |
| `GW-API` | Gateway de servicios | políticas, identidad, versionado y trazabilidad |
| `CTX-OPS` | Núcleo operacional | agregado contenedor, movimientos, posición y hechos operacionales |
| `CTX-GATE` | Gate y citas | prevalidación, citas, cola virtual, entradas/salidas y excepciones |
| `CTX-YARD` | Patio/posición | asignación, verificación cruzada, condiciones dinámicas y remociones |
| `CTX-REEFER` | Reefer/telemetría | medición, alarmas, series y estado de tomas/tableros |
| `CTX-PLAN` | Planificación | estiba/patio, propuesta, corrección y aprendizaje de reglas |
| `CTX-VESSEL` | Nave/mensajería | planes, órdenes, confirmaciones, ventana y productividad |
| `CTX-BILL` | Evidencia facturable | hecho, evidencia, objeción y entrega al ERP |
| `CTX-INSP` | Inspecciones | agenda, remoción anticipada, acta y cierre |
| `CTX-EMIS` | Energía/emisiones | medición por equipo, cálculo, historia y reporte verificable |
| `SRV-IAM` | Identidad/autorización | internos, externos, eventuales, roles/atributos, sesiones y PAM |
| `SRV-NOTIF` | Notificaciones | reglas, escalamiento, confirmación y adaptadores de canal |
| `SRV-EVID` | Evidencia/firma | cuatro actos, sellos, integridad, consulta y retención |
| `INT-HUB` | Integración/eventos | contratos, colas, gobierno y observación de intercambios |
| `INT-TOS` | Anticorrupción TOS | traducción, secuencia, coexistencia y autoridad |
| `EDGE-RUN` | Runtime local | continuidad de funciones críticas, buffer y reconciliación |
| `DATA-CORE` | Datos operacionales | estado transaccional y fuente de verdad según fase |
| `DATA-TS` | Series temporales | telemetría reefer/equipos |
| `DATA-DOC` | Documentos/evidencia | imágenes, actas, firmas y expedientes |
| `DATA-AN` | Analítica/reportes | KPI, concedente y emisiones sin cargar la operación |

### 6.2 Reglas de comunicación remota

Toda escritura reintentable requiere idempotencia, clave y ventana de deduplicación. Toda llamada remota requiere timeout explícito y, según criticidad, reintento con backoff exponencial+jitter, circuit breaker, bulkhead y rate limit. Se debe declarar degradación elegante, fallback, recuperación, reconciliación y cualquier punto único de falla residual.

## 7. Integraciones obligatorias

La base de dimensionamiento distingue **21 contrapartes lógicas actuales** y **7 familias de periferia/instrumentación**. Con 16 navieras proyectadas serán 23 contrapartes.

| Grupo | Cantidad actual | Contrato/dirección base | Regla de continuidad |
|---|---:|---|---|
| Navieras | 14 | EDIFACT bidireccional: BAPLIE, COPRAR, COARRI y CODECO; versión por naviera | cola durable; puente solo para no alianza; alianza sin puente/redigitación al hito 2029 |
| Autoridades | 3 | API/archivo si existe; canal asistido registrado si no | reintento y expediente trazable |
| Ferrocarril | 1 | bidireccional por levantar | programación local y reenvío |
| Concedente | 1 | salida de indicadores | acumulación local y entrega sin reconstrucción |
| TOS 2012 | 1 | bidireccional, versionado, secuencia e idempotencia | cola, conciliación, cruce de zona y retorno |
| ERP | 1 | hecho/evidencia/estado/objeción | conciliación 1:1; ERP emite documento tributario |
| Periferia | 7 familias | grúas, acceso/barreras, CCTV/VMS, VGM, OCR, reefer y equipos/posición | buffer y procesamiento local según criticidad |

Cada contrato debe completar: propietario del dato, dirección, servicio/evento, versión, frecuencia/peak, disponibilidad, timeout, reintento, idempotencia, DLQ, campos sensibles, fallback, conciliación, evidencia de aceptación y responsable. Lo no confirmado queda `POR LEVANTAR`.

## 8. Coexistencia con TOS 2012

**Decisión heredada:** envolver el TOS mediante capa anticorrupción y sustituir capacidades progresivamente por dominio. Antes del hito H2/mes 4 existe una puerta de viabilidad: si lectura, escritura o conciliación no son suficientemente confiables, se replantea hacia reemplazo integral controlado.

El diseño debe mostrar:

1. flujos nuevo→legado y legado→nuevo;
2. autoridad única por `dominio × zona × fase`;
3. secuencia, idempotencia, deduplicación y escritura parcial;
4. traspaso transaccional de autoridad cuando el contenedor cruza una zona;
5. conciliación por turno y detección temprana, no solo conciliación tardía;
6. ventanas de investigación: 48 h para posición/movimientos y 24 h para gate/hechos;
7. gate con cero diferencias no explicadas al cierre diario;
8. retorno normal con doble control y emergencia break-glass auditable;
9. objetivo total detección→operación restituida ≤30 min en marcha blanca crítica;
10. repositorio independiente para histórico retenido fuera del núcleo nuevo;
11. puerta de retiro y apagado del TOS, sin conservarlo como repositorio histórico.

El contrato del TOS real, fechas exactas de soporte y capacidad de escritura/CDC permanecen por confirmar.

## 9. Operación desconectada, continuidad y disponibilidad

### 9.1 Capacidades críticas durante 72 horas

La arquitectura debe mantener localmente, sin pérdida:

- atención de nave y movimientos;
- posición/inventario y cruce de zonas;
- gate y tiempos de entrada/salida;
- monitoreo/alarma reefer;
- hechos y evidencia facturable.

El diseño debe declarar expresamente qué funciones no estarán disponibles y el procedimiento manual que las reemplaza. Al recuperar conectividad, la sincronización debe ser automática, auditable y determinista, con objetivo **≤90 minutos** luego de 72 h.

### 9.2 Umbrales transversales

| Control | Umbral |
|---|---:|
| Disponibilidad mensual de servicios críticos | 99,9 % extremo a extremo |
| Disponibilidad de infraestructura aplicable | 99,95 % |
| RTO | ≤4 h |
| RPO | ≤15 min |
| DR | sitio/región secundaria, replicación continua y conmutación automatizable |
| Prueba DR | semestral con conmutación real e informe |
| Respaldo | 3-2-1-1-0 |
| Restauración | prueba documentada mensual |
| Mantenimiento | fuera de ventana crítica, aviso ≥10 días hábiles, sin interrupción |

## 10. Arquitectura física y Artículo 16

La solución debe ser híbrida; una propuesta solo nube o solo on-premise es inadmisible. Cada componente se justifica individualmente con:

1. latencia;
2. criticidad/continuidad operacional;
3. volumen de datos y transferencia;
4. restricciones regulatorias/seguridad;
5. conectividad y acoplamiento con equipos físicos;
6. costo total de operación sin incluir cifras económicas en Informe 1.

### 10.1 Nube

- proveedor global con región o zona en Chile o Sudamérica;
- región primaria y secundaria declaradas;
- producción en al menos dos zonas de disponibilidad;
- infraestructura como código versionada en repositorio del CLIENTE;
- redes segmentadas, aplicación/datos en subredes privadas y borde como única exposición;
- servicios gestionados cuando reduzcan riesgo operativo;
- FinOps con etiquetas, presupuestos/alertas y reporte mensual;
- reversibilidad y mitigación de vendor lock-in.

### 10.2 On-premise y borde

- autonomía 72 h y buffer dimensionado al peak coincidente;
- equipos críticos redundantes y almacenamiento tolerante a al menos un disco, con RAID justificado;
- CIS hardening, parches, acceso físico/lógico y monitoreo unificado;
- enlaces redundantes por caminos/proveedores distintos y conmutación automática;
- zonas operacional, administrativa y protección segregadas con conductos controlados;
- continuidad del VMS/ISPS durante la migración de red;
- protección eléctrica, ambiental y física de sala/gabinetes;
- protección marina por clase y emplazamiento: IP, anticorrosión, temperatura, vida útil, reposición y recepción.

### 10.3 Sala técnica: decisión aún arquitectónica

El ADR debe comparar:

1. remediar/endurecer sala actual;
2. reemplazarla o reconstruirla dentro del terminal;
3. edge local mínimo más nube.

Ninguna alternativa puede eliminar la autonomía local de 72 h ni presumir una instalación fuera del ambiente portuario. Si existe cómputo sustantivo en sala principal, se aplican íntegramente los requisitos RT-06.01 a RT-06.24. Se deben especificar racks separados, distribución interna, UPS ≥30 min a plena carga, generación ≥24 h, carga kW, factor de potencia y PUE, sin sobredimensionar.

## 11. Seguridad transversal

### 11.1 Principios y exposición

- Zero Trust conforme NIST SP 800-207.
- STRIDE por componente e integración externa.
- clasificación de información y mínimo privilegio.
- CDN, WAF gestionado/personalizado, anti-DDoS L3/L4/L7, protección de bots.
- TLS 1.3; TLS 1.0/1.1 prohibidos; HSTS y certificados automatizados.
- datos cifrados en reposo mediante KMS/HSM, rotación y separación de funciones.
- gateway con validación de esquema e inspección de payload.

### 11.2 Identidad y operación portuaria

- OIDC/OAuth 2.1 o SAML 2.0 y cierre SSO propagado.
- MFA para administradores, privilegiados y accesos externos.
- RBAC + ABAC y matriz de segregación de funciones.
- PAM con elevación temporal y grabación de sesión.
- baja efectiva ≤24 h.
- credencial temporal vinculada a nombrada para eventuales, sin biometría obligatoria, con expiración, zonificación y auditoría.
- terminal compartida, relevo sin detención, guantes, intemperie, expiración/revocación y sesión segura.

### 11.3 Detección, respuesta y DevSecOps

- log central inalterable: 12 meses en línea + 24 meses en archivo;
- SIEM con casos de uso portuarios, EDR nube/on-premise y trazabilidad correlacionada;
- incidente crítico comunicado al CLIENTE ≤2 h; brecha notificada ≤24 h; causa raíz ≤5 días hábiles;
- vulnerabilidades: críticas ≤7 días, altas ≤15, medias ≤30;
- pentest anual y antes de cada paso a producción;
- SAST, SCA, DAST y escaneo de imágenes con bloqueo;
- SBOM CycloneDX/SPDX, firma de artefactos y procedencia SLSA 3+;
- cero secretos embebidos;
- datos productivos prohibidos en no producción salvo anonimización verificable.

## 12. Ambientes, despliegue y retorno

Se requieren cinco ambientes aislados: Desarrollo, QA, Preproducción equivalente a Producción, Producción y DR. Deben contemplarse:

- CI/CD automatizado, revisión por pares y ramas protegidas;
- reversión automatizada y despliegue sin interrupción;
- azul-verde, canario o progresivo demostrado en Preproducción;
- cobertura de pruebas ≥70 % en lógica de negocio;
- carga/estrés a 1,5× el peak declarado;
- chaos engineering antes de paso a producción y semestral en operación;
- ISO/IEC 25010 con umbrales numéricos;
- retorno para toda intervención de software, red, firmware, infraestructura, instrumentación o migración.

Cada intervención debe registrar ocho campos: objetivo/alcance; ejecutor y responsable de retorno; disparador; pasos/dependencias; tiempo máximo; prueba/evidencia; ventana y contraste con congelamiento/nave; conciliación/cierre.

## 13. Calendario y restricciones operacionales

- Congelamiento total entre **15 de diciembre y 30 de abril**.
- De enero a marzo ocurre 62 % del volumen refrigerado; ninguna intervención al patio reefer.
- No intervenir durante una nave ni cuatro horas antes.
- Todo cambio invasivo necesario para la estrategia debe estar instalado, migrado, probado, con retorno y capacitación listos a más tardar el **14-dic-2027**.
- Entre 15-dic-2027 y 30-abr-2028 solo cabe sombra de solo lectura, no invasiva y sin autoridad operacional si el CLIENTE la autoriza formalmente; si no, se reprograma.
- La autoridad operacional se programa desde **01-may-2028** bajo el supuesto vigente.
- Captura de conocimiento del planificador: inicia mes 1, primera versión antes de H2/mes 4 y versión validada antes de mes 12.
- Fechas exactas de fin de soporte y jubilación siguen abiertas; se planifica conservadoramente.

## 14. Programa 2029 indivisible

Para las líneas de la alianza, antes de la fecha efectiva:

1. mensajería estándar internacional exclusiva y cero redigitación/puente;
2. 100 % de confirmaciones de ventana con ≥72 h;
3. productividad ≥30 movimientos/h por grúa demostrada en operación representativa;
4. captura de emisiones desde mes 1 y reporte **efectivamente verificado** por tercero.

El cumplimiento general de ventanas se mantiene separado: >90 %. No se inventa una obligación de 24 meses de historia de emisiones; la suficiencia se acuerda tempranamente con alianza/verificador. Fecha y líneas exactas siguen `PENDIENTE CLIENTE`.

## 15. Dimensionamiento inicial heredado

| Dimensión | Actual | Proyección/peak | Calidad del dato |
|---|---:|---:|---|
| TPS normal de negocio | ≈0,11 | ≈0,13 | estimación C2 |
| TPS peak 2 naves + gate | ≈0,23 | ≈0,27 | estimación C2; usa 30 mov/h |
| Reefer reportado al núcleo | ≈7,2 eventos/s | ≈8,7 | muestreo 5 min |
| Reefer local | ≈35,8 eventos/s | ≈43,3 | muestreo 1 min |
| Posición equipos | ≈37 eventos/s | ≈44 | frecuencia 2 s por validar |
| Usuarios internos concurrentes | ≈160 | ≈175 | supuesto 25 % |
| Usuarios externos concurrentes | ≈159 | ≈187 | supuesto 8 % |
| Transaccional anual | ≈20 GB | ≈24 GB | supuesto de tamaño/sobrecarga |
| Series reefer | ≈68 GB/año | ≈82 GB/año | acumulado actual 5 años ≈340 GB |
| Imágenes OCR | ≈1,4 TB/año | ≈1,6 TB/año | supuestos 500 KB y cobertura |
| Histórico TOS | ≈480 GB | por confirmar | estimación gruesa; solicitar real |
| Red patio sin video | ≈375–500 kbps | +15–20 % | alta incertidumbre; site survey |
| Estaciones base | ≈6–8 | ubicación pendiente | no comprar/ubicar sin site survey |
| Datos 72 h sin enlace | ≈13 GB | +15–20 % | imágenes dominan; revalidar a peak |
| Sincronización posterior | ≤90 min | ≤90 min | objetivo RNF |

Estas cifras son insumos, no dimensionamiento final. El Frente 2 debe declarar método, supuestos, holgura y sensibilidad; no puede transformar aproximaciones en hechos del CLIENTE.

## 16. Datos, retención y migración que afectan arquitectura

### 16.1 Retención

| Conjunto | Plazo/tratamiento |
|---|---|
| Movimientos | 10 años |
| Temperatura reefer | 5 años |
| Evidencia facturable | 6 años |
| VGM | 5 años |
| Imágenes OCR | 12 meses; eliminación/anonimización controlada |
| Accesos | 5 años |
| Telemetría | 2 años en línea; agregación histórica según plazo declarado |
| Logs de seguridad | 12 meses en línea + 24 meses en archivo |

### 16.2 Migración

- inventario completo con posición verificada físicamente al corte;
- movimientos de 3 años; años 4–10 en repositorio consultable;
- hechos/evidencias de 6 años con relación 1:1;
- maestros completos;
- tarifario vigente y reglas/excepciones;
- objeciones abiertas completas;
- conciliación por universo y prueba de recuperación dirigida.

El Subdocumento 5 es propietario del modelo de datos detallado, pero el Subdocumento 4 debe proveer almacenamiento, flujo, seguridad, despliegue, capacidad y continuidad coherentes.

## 17. Decisiones heredadas con impacto arquitectónico

Las 21 decisiones están en [`Registro_supuestos_v3.md`](../../Celula2/02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md). Para Célula 3 son especialmente vinculantes:

- TOS envuelto y sustitución progresiva (`Decisión 1`).
- DGPS/RTLS + lectura óptica como verificación de posición (`2`).
- algoritmo asigna y operador ejecuta, con excepción controlada (`3`).
- planificación propone/aprueba/corrige y captura motivos (`4–5`).
- citas opcionales, prioridad y cola virtual (`6–7`).
- reefer con muestreo local/agregado y alarma escalada (`8`, `10`).
- red celular privada LTE/5G como alternativa primaria sujeta a site survey (`9`).
- evento como evidencia facturable (`11`).
- credencial temporal/eventuales y conteo por zona general (`12–13`).
- cabina sin confirmación rutinaria y telemetría como fuente primaria (`14–15`).
- emisiones ISO 14083/GLEC e instrumentación real por equipo (`16–17`).
- BAPLIE/COPRAR/COARRI/CODECO (`18`).
- segregación IEC 62443 aprobada sin degradar protección (`19`).
- tres alternativas de sala (`20`).
- inspecciones programadas con remoción anticipada y acta (`21`).

Las decisiones 9, 19 y 20 son insumos directos de ADR físicos; no requieren inventar un RF.

## 18. Pendientes y asuntos que deben escalarse

| ID | Asunto | Regla provisional | Responsable externo/futuro |
|---|---|---|---|
| `ESC-01` | fecha/líneas alianza | plan conservador; no degradar exclusividad | CLIENTE/comercial |
| `ESC-02` | historia suficiente de emisiones | captura mes 1, acuerdo temprano y pre-verificación | verificador/alianza |
| `ESC-03` | sombra en congelamiento | no autorizada hasta respuesta formal | CLIENTE |
| `ESC-04` | fin soporte TOS | escenario conservador desde 01-01-2028 | CLIENTE/fabricante |
| `ESC-05` | fecha retiro planificador | captura mes 1 | CLIENTE |
| `ESC-06` | contratos de TOS/VMS/autoridades/ferrocarril/radio/grúas/periféricos | no inventar; diseñar adaptador/fallback | levantamiento/fabricantes |
| `ESC-07` | protección marina | especificar por clase, ubicación y cantidad | Frente 2 |
| `ESC-08` | SLA críticos nave/gate/frío | clases separadas; número E2E por validar | arquitectura/CLIENTE |
| `ESC-09` | decisión técnica sala | cerrar por ADR sin perder 72 h | arquitectura |
| `ESC-10` | site survey patio y cantidad/ubicación radio | usar rango, no plano ficticio | levantamiento |
| `ESC-11` | `RF-PAT-07` validación interna | usar como condición vigente con marca de validación | Célula 2 |
| `ESC-12` | ISO/capacidad sectorial | no declarar cumplimiento sin evidencia | Célula 1/equipo |
| `ESC-13` | tolerancia VGM chilena | no fijar sin autoridad | levantamiento |
| `ESC-14` | plazo/interfaz de cada autoridad | canal asistido trazable como fallback | levantamiento meses 1–4 |

### 18.1 Mapa compacto MC-01..30 hacia arquitectura

| MC | Consecuencia que no debe perderse | Paquete primario |
|---|---|---|
| 01 | app instalable única, cuatro perfiles y offline interno | A1/C1/D1 |
| 02 | VMS conservado; solo eventos/metadatos/evidencia confirmados | A2/C3/D1 |
| 03 | notificaciones compartidas con adaptadores | A1/A2 |
| 04 | autenticación de terreno/terminal compartida | D1/A1 |
| 05 | firma/evidencia en cuatro actos | A1/D1/C2 |
| 06 | portal público/autenticado y dato sensible | A1/D1 |
| 07 | legado→nuevo bidireccional y fallos parciales | A2/A3 |
| 08 | autoridad dominio×zona×fase | A3 |
| 09 | sala por ADR y 72 h locales | C1/C2/C3 |
| 10 | patio cargado y failover de radioenlace | C3/C4 |
| 11 | protección marina por clase/ubicación | C2/C4 |
| 12 | 21 contrapartes + 7 familias | A2/C4 |
| 13 | prueba TOS con contrato/stub/versión acordada | A2/A3 |
| 14 | doble control y break-glass auditado | A3/D1 |
| 15 | posición conocida correcta vs. pendiente por verificar | A1/A3 |
| 16 | prioridad operativa sin confundir congelamiento | A3 |
| 17 | soporte crítico diferenciado nave/gate/frío | C3/D1 |
| 18 | tres turnos/eventuales/capacitación sin invadir congelamiento | C3/D1 |
| 19 | 138 RF normalizados; no usar IDs históricos | todos |
| 20 | COARRI carga/descarga y CODECO gate/custodia | A2 |
| 21 | concedente, autoridades y ferrocarril con fallback | A1/A2 |
| 22 | acreditaciones no son cajas de arquitectura | D3/escalamiento |
| 23 | mensajería alianza exclusiva sin puente/redigitación | A2/A3 |
| 24 | ≥72 h, >90 % general y ≥30 mov/h demostrados | A3/C4 |
| 25 | emisiones desde mes 1 y reporte efectivamente verificado | A3/C4 |
| 26 | siete retenciones, seis migraciones y repositorio histórico | C2/C4/D1 |
| 27 | retorno de toda intervención con ocho campos | C3/D1 |
| 28 | fechas 2028 conservadoras y abiertas | A3/C3 |
| 29 | capacidad sectorial debe acreditarse fuera de C3 | D3/escalamiento |
| 30 | invasivas listas 14-dic-2027; sombra solo condicionada | A3/C3 |

## 19. Reglas negativas

1. No usar web responsiva como sustituto de app móvil offline.
2. No crear cuatro aplicaciones por perfil.
3. No crear un microservicio por RF, canal, equipo o mensaje.
4. No convertir cada caja lógica en despliegue físico.
5. No reemplazar ERP, VMS/CCTV, control de grúas, acceso/barreras o báscula.
6. No crear portal de video; el VMS existente sigue siendo la interfaz de video.
7. No llevar video completo por la red operacional sin necesidad demostrada.
8. No depender de nube para las cinco funciones críticas durante 72 h.
9. No inventar APIs, protocolos, versiones ni disponibilidad de terceros.
10. No probar el TOS modificando arbitrariamente su esquema; usar contrato, stub/fixture o versión acordada.
11. No presumir que mover la sala elimina ambiente marino.
12. No usar un IP único para todo equipo de terreno.
13. No omitir funciones no disponibles durante desconexión.
14. No ocultar puntos únicos de falla.
15. No llamar marcha blanca a una intervención durante el congelamiento.
16. No reconstruir indicadores de gate ni hechos facturables después del evento.
17. No confundir COARRI con CODECO ni mensaje de negocio con sobre de red.
18. No introducir precios en T-11 o Informe 1.

## 20. Convenciones de trazabilidad y estado

Cadena objetivo:

> fuente oficial → `MC-*`/decisión → `RF-*` o `RNF-*` → decisión arquitectónica → componente lógico → nodo físico/control → diagrama → fila T-11 → evidencia

Estados permitidos:

- `PENDIENTE`: no iniciado.
- `EN CURSO`: desarrollo activo.
- `PARA REVISIÓN`: contenido completo por su autor.
- `OBSERVADO`: revisión detectó brecha.
- `APROBADO`: integrable al consolidado.
- `BLOQUEADO EXTERNO`: requiere dato/autoridad externa; debe conservar fallback.
- `NO APLICA`: solo con justificación.

## 21. Índice de fuentes vigentes

### Fuentes oficiales y control

- `FEP01.26 — Bases Administrativas TFEP-01/2026`: fuente oficial disponible por el canal común del equipo.
- `FEP02.26 — Bases Técnicas Transversales`: fuente oficial disponible por el canal común del equipo.
- `FEP03.06.26 — Caso 06 Portuaria`: fuente oficial disponible por el canal común del equipo.
- [`Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md): cierre corregido, disposición y tratamiento `MC-01..30`.

Las citas de trabajo usan documento + capítulo/numeral + código + materia. Los PDF oficiales no necesitan residir en el repositorio, pero deben estar disponibles para comprobaciones y para la referencia final de la oferta.

### Célula 2 vigente

- [`Catálogo RF parte 1`](../../Celula2/01_Requerimientos/Catalogo%20rf%20definitivo%20parte1.md)
- [`Catálogo RF parte 2`](../../Celula2/01_Requerimientos/Catalogo%20rf%20definitivo%20parte2.md)
- [`Catálogo RF parte 3`](../../Celula2/01_Requerimientos/Catalogo%20rf%20definitivo%20parte3.md)
- [`RNF`](../../Celula2/01_Requerimientos/RNF.md)
- [`Decisión TOS 2012`](../../Celula2/02_Decisiones_Reglas_Supuestos/01_decision_01_tos_2012_registro_final.md)
- [`Registro de supuestos y decisiones`](../../Celula2/02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md)
- [`Reglas de negocio`](../../Celula2/02_Decisiones_Reglas_Supuestos/Registro%20reglas%20de%20negocio%20v2.md)
- [`Volumetría e integraciones`](../../Celula2/plantilla_volumetria_caso_portuaria.md)

### Material de forma

- [`FEP01.26 — Introducción Arquitectura de Software`](../FEP01.26%20-%20Introduccion%20Arquitectura%20de%20Software.pdf): usar para claridad visual, lectura, leyendas y consistencia entre vistas; no como fuente de requisitos del caso.

## 22. Criterio de suficiencia del maestro

El maestro se considera vigente si:

- cada frente puede comenzar sin releer todos los documentos de Célula 2;
- toda decisión importante puede volver a la fuente exacta;
- los pendientes externos están visibles y no se transforman en hechos;
- lógica, físico, seguridad, capacidad, T-11 y consolidado usan los mismos identificadores;
- cualquier cambio posterior se refleja primero en este maestro y en la matriz global.
