# Base técnica del Subdocumento 4 — inventario para la redacción conjunta

**Caso:** 06 Portuaria — TERABYTE
**Versión de trabajo:** base técnica alineada — no constituye redacción final ni incorpora diagramas entregables.
**Baseline documental:** arquitectura alineada con Célula 4 al 2026-09-06.
**Estado de las decisiones:** once ADR en estado `PROPUESTO`; ninguna decisión se presenta como aprobada, contratada o implementada.

Este subdocumento describe la solución propuesta para el Informe 1 y responde a la estructura 4.1/4.2 del Formulario T-21. Las referencias detalladas, cálculos y trazas permanecen en los expedientes fuente; el presente texto es autónomo y no exige leerlos para comprender la arquitectura.

## Regla de lectura del Informe 1

Se distinguen tres niveles de certeza:

- **Baseline propuesta:** definición suficientemente resuelta para estructurar la oferta y sus diagramas.
- **Condición de cierre:** dato que requiere confirmación del CLIENTE, levantamiento en terreno, medición o selección formal antes de congelar el diseño.
- **Evidencia futura:** prueba, contrato, certificación, acta o medición que corresponde a ejecución y no se declara realizada en el Informe 1.

La solución no supone adquisiciones ejecutadas, pruebas aprobadas ni infraestructura existente distinta de la descrita por el caso. Los nombres de productos son referencias técnicas; se admite un equivalente de prestaciones iguales o superiores cuando satisfaga la especificación y mantenga soporte durante el contrato.

## 4.1 Arquitectura lógica

### 4.1.1 Esquema de solución

TERABYTE propone una plataforma portuaria híbrida que conecta a los actores del terminal con una capa común de operación, integración, datos, identidad, evidencia y observabilidad. Sus canales son un portal web público y autenticado, una única aplicación móvil instalable con perfiles por rol y vistas de cabina o terreno. Estos canales atienden a personal operacional, planificación, gate, patio, reefers, inspecciones, facturación, administración y TI, además de usuarios externos autorizados como transportistas, agencias, navieras y autoridades.

La frontera de TERABYTE comprende la plataforma en nube, el núcleo operacional local, el borde de gate/patio/reefers/muelle, la red operacional nueva y las capacidades transversales necesarias. Permanecen fuera de esa frontera —pero integrados— el TOS 2012 durante la convivencia, el ERP y la emisión tributaria, los sistemas de navieras y autoridades, ferrocarril, concesionaria, control de acceso, barreras, básculas, CCTV/VMS y control de grúas. Este último se consume solo en lectura y con autorización del fabricante; la solución no modifica su lógica de control.

La obra civil, canalizaciones exteriores, alimentación eléctrica del recinto y acceso vial son ejecutados por el CLIENTE. TERABYTE entrega su especificación y coordinación técnica cuando sean necesarias para que la solución funcione. Esta separación no elimina la obligación de describir los requerimientos físicos.

### 4.1.2 Arquitectura lógica de la solución

Se adopta una arquitectura modular híbrida orientada a dominios. La modularidad separa responsabilidades y permite una sustitución progresiva del TOS; el carácter híbrido combina servicios administrados en AWS con capacidad operacional local. El núcleo local no es una simple pasarela ni una copia pasiva de toda la nube: ejecuta las funciones críticas y mantiene sus datos, identidad, evidencia y colas durante la desconexión. Tampoco es el primario permanente; al restablecer la conectividad reconcilia el estado con la plataforma central.

La solución se organiza en ocho capas:

#### Tabla T-SD4-01 — componentes agrupados por capa

| Capa | Componentes principales | Responsabilidad |
|---|---|---|
| Presentación | `CH-PORTAL`, `CH-APP`, `CH-CAB` | interacción web, móvil y de cabina/terreno |
| Borde público | `GW-EDGE` | terminación TLS, CDN, WAF y protección anti-DDoS |
| Gateway | `GW-API` | autenticación de entrada, cuotas, contratos y enrutamiento; perfil local restringido |
| Negocio | `CTX-OPS`, `CTX-GATE`, `CTX-YARD`, `CTX-REEFER`, `CTX-PLAN`, `CTX-VESSEL`, `CTX-BILL`, `CTX-INSP`, `CTX-EMIS`, `SRV-NOTIF` | reglas y procesos de cada dominio |
| Integración | `INT-HUB`, `INT-TOS` | contratos externos, eventos, colas y capa anticorrupción del TOS |
| Datos | `DATA-CORE`, `DATA-TS`, `DATA-DOC`, `DATA-AN` | estado operacional, series temporales, documentos y analítica |
| Seguridad | `SRV-IAM`, `SRV-EVID` | identidad, autorización, firma, integridad y cadena de custodia |
| Observabilidad | métricas, logs, trazas, alertas y SIEM | visión común de nube, sala y borde |

`EDGE-RUN` es el runtime transversal instalado en el terminal. Contiene el perfil local restringido de `GW-API`, las funciones críticas, `INT-TOS`, la capacidad local de identidad, el estado operacional y los apoyos parciales de series, documentos, notificaciones, evidencia, mensajería y observabilidad. No crea una segunda plataforma completa.

#### Continuidad por dominio

| Dominio | Responsabilidad exclusiva | Conducta sin enlace exterior |
|---|---|---|
| Operaciones y nave | contenedor, movimientos, órdenes STS, recalada activa y productividad | continúa localmente; mensajería externa queda en cola |
| Gate | citas, prevalidación, entrada/salida y excepciones | continúa; verificaciones externas usan fallback asistido |
| Patio | posición, asignación, cruce de zonas y remociones | continúa con `INT-TOS` local |
| Reefers | medición, consigna, alarma y confirmación | continúa, incluida la alarma local ≤5 min |
| Planificación | reglas, propuestas y correcciones | último plan disponible en consulta; no genera un plan nuevo |
| Facturación | hechos, evidencia y objeciones | registra localmente; entrega al ERP espera conexión |
| Inspecciones | agenda, remoción, acta y cierre | agenda vigente y acta local; nuevas coordinaciones esperan conexión |
| Emisiones | consumo, cálculo y reporte | captura disponible; cálculo y reporte se difieren |
| Identidad y evidencia | sesiones, permisos, firma, sello y custodia | identidades vigentes y sello local disponibles; altas nuevas esperan conexión |

Las interfaces obedecen reglas estrictas: los canales nunca acceden directamente a los datos; pasan por el gateway y los servicios de negocio. Los dominios no llaman directamente a sistemas externos; utilizan `INT-HUB` o `INT-TOS`. Las comunicaciones remotas tienen timeout explícito, idempotencia y degradación visible. El catálogo completo y las dependencias permitidas están en [A1 §§2–5](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md).

### 4.1.3 Arquitectura de integración y procesos críticos

La integración se gobierna por contrato. Las interfaces síncronas se especifican con OpenAPI 3.1 y las asíncronas con AsyncAPI 2.6 o superior; los contratos se versionan semánticamente y se validan antes del despliegue. La mensajería usa entrega al menos una vez, consumidor idempotente, orden por agregado cuando sea necesario, claves de deduplicación, reintentos con backoff, colas de mensajes no procesables y repetición controlada.

`INT-HUB` concentra las integraciones externas y mantiene colas durables. `INT-TOS`, instalado en el terminal, es la capa anticorrupción que traduce, ordena y concilia el modelo nuevo con el TOS 2012. Esta separación evita que los dominios incorporen formatos particulares de navieras, autoridades o sistemas heredados.

Para el Informe 1 se reconocen **21 contrapartes lógicas** y **7 familias técnicas periféricas**. El número expresa el alcance de integración, no contratos ya levantados. Están definidos el patrón, el gobierno y las responsabilidades; permanecen condicionados los contratos reales, versiones por naviera, disponibilidad de CDC del TOS, protocolos de autoridades y ferrocarril, y capacidades efectivas de grúas, básculas, OCR, reefers y posicionamiento. El detalle canónico vive en [A2 §§2–5](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md).

#### Tabla T-SD4-02 — familias de integración

| Familia | Contrapartes o dispositivos | Patrón dominante | Estado de Informe 1 |
|---|---|---|---|
| TOS heredado | `EXT-TOS12` | bidireccional mediante `INT-TOS`, eventos y conciliación | patrón definido; interfaz y CDC bloqueados externamente |
| ERP/facturación | `EXT-ERP` | hecho facturable asíncrono + confirmación | patrón definido; contrato por levantar |
| Concedente | `EXT-CON` | reporte trazable por lote/período | patrón definido; canal por levantar |
| Ferrocarril | `EXT-FER` | programación y movimiento asíncronos | contrato inexistente hoy; fallback trazado |
| Autoridades | Aduana, SAG y autoridad sanitaria | API/archivo o canal asistido trazable | interfaz real bloqueada externamente |
| Navieras | 14 actuales, 16 proyectadas; EDIFACT | BAPLIE/COPRAR/COARRI/CODECO por naviera | estándar definido; versión y contrato por naviera pendientes |
| Periferia e instrumentación | grúas, acceso, VMS, básculas, OCR, reefers y posicionamiento | evento/telemetría; grúas solo lectura | siete familias identificadas; protocolos/fichas por validar |

Las cinco cadenas que no pueden depender de Internet son:

1. atención de nave y confirmación de movimientos;
2. posición, inventario y transferencia de autoridad por zona;
3. gate y registro de entrada/salida;
4. monitoreo y alarma reefer;
5. registro de hechos y evidencia facturable.

Todas recorren `CH-APP/CH-CAB → GW-API local → contexto crítico → datos/evidencia local`. Comparten identidad vigente, tiempo, nombres, certificados, claves y buffer persistente locales. Pueden operar hasta 72 horas sin conectividad externa. Al volver el enlace, la plataforma sincroniza y reconcilia en un máximo de 90 minutos, con resolución determinista de conflictos y bitácora auditable.

El Programa 2029 se trata como un resultado operacional indivisible: mensajería estándar sin redigitación para la alianza, ventana de atraque confirmada con 72 horas de anticipación, medición de productividad hacia la meta de 30 movimientos por hora por grúa y reporte de emisiones verificado por tercero. La plataforma registra y demuestra esos resultados; no promete que el software, por sí solo, produzca la meta de negocio.

#### Matriz de autoridad durante la convivencia con el TOS

| Estado del bloque operacional | Fuente de verdad | Escritura autorizada | Regla de transición |
|---|---|---|---|
| Antes de migrar | TOS 2012 | solo TOS | el sistema nuevo recibe eventos para preparar y comparar |
| Validación paralela | TOS 2012 | solo TOS; plataforma nueva en sombra | no se traspasa autoridad hasta persistencia y conciliación verificadas |
| Después del cutover aprobado | plataforma nueva | solo plataforma nueva | escritura hacia TOS se mantiene temporalmente para retorno |
| Reefer, capacidad nueva | plataforma nueva desde el inicio | solo plataforma nueva | no sustituye un registro previo del TOS |

La autoridad cambia por `dominio × zona × fase`, nunca por dos escritores simultáneos. El emisor registra un evento secuenciado e idempotente y el receptor confirma su persistencia antes del traspaso. Si el paso falla, se conserva la autoridad anterior y se bloquea una nueva transferencia hasta conciliar. La definición completa se encuentra en [A3 §§2–7](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md).

### 4.1.4 Datos y seguridad transversales

La vista de datos distingue cuatro capacidades lógicas: `DATA-CORE` para estado transaccional; `DATA-TS` para series temporales; `DATA-DOC` para documentos, imágenes y evidencia; y `DATA-AN` para indicadores y analítica. Estas capacidades se implementan sobre dos familias principales: PostgreSQL/series temporales y almacenamiento de objetos. No se interpreta cada capacidad lógica como un motor o una compra independiente.

El modelo detallado de Célula 4 organiza **10 dominios, 80 entidades, 451 atributos, 78 entidades relacionales y 2 temporales**. `Contenedor` es el maestro; `VisitaContenedor` representa la estadía operacional física y puede conservar `VISITA` como identificador; `Recalada` o `VisitaNave` representa la estadía de una nave. Esta precisión evita confundir dos conceptos que comparten la palabra “visita”. Los dueños de dominio controlan calidad y uso; la autoridad operacional se rige por la fase de convivencia descrita en 4.1.3.

#### Vista V-DATA-01 — correspondencia de datos C4↔C3

| Dominio C4 | Fuente normal / autoridad en corte | Capacidad C3 | Protección y continuidad |
|---|---|---|---|
| `DOM-OPS` operación | AWS consolidado / núcleo local crítico | `DATA-CORE` | IAM, cifrado e idempotencia; movimientos 10 años |
| `DOM-PAT` patio | solución e instrumentación / local por zona y fase | `DATA-CORE` | rol, integridad y evidencia de fuente |
| `DOM-GAT` gate | solución e interfaces / local para entrada/salida | `DATA-CORE` + `DATA-DOC` | protección personal, trazabilidad y mínimo privilegio |
| `DOM-REF` reefers | instrumentación validada / alarma y serie local | `DATA-TS` + `DATA-DOC` | integridad, custodia y retención reefer de 5 años |
| `DOM-NAV` nave | solución + mensajes / estado activo local, intercambio en cola | `DATA-CORE` + `DATA-DOC` | cifrado comercial, versión e integridad |
| `DOM-INS` inspecciones | solución + acto de autoridad / agenda y acta local | `DATA-CORE` + `DATA-DOC` | firma, hash y cadena de custodia |
| `DOM-FAC` facturación | solución para hecho; ERP para asiento / hecho local | `DATA-CORE` + `DATA-DOC` | inmutabilidad y conciliación 1:1 |
| `DOM-ACC` acceso | IAM/sistema conservado / identidad y bitácora local | `DATA-CORE` + auditoría | mínimo privilegio, cifrado personal y revocación local |
| `DOM-EMI` emisiones | derivado trazable / captura local, cálculo diferible | `DATA-AN` desde `CORE/TS` | acceso por rol, linaje y fórmula versionada |
| `DOM-INT` integración | contratos y `INT-HUB` / colas y bitácora local | `DATA-CORE` + `DATA-DOC` | mTLS/OAuth, integridad, DLQ y auditoría |

La seguridad adopta Zero Trust: cada acceso se autentica y autoriza según identidad, rol, contexto y mínimo privilegio. La única superficie pública es `GW-EDGE`; los servicios y datos permanecen en redes privadas. Se segmentan las zonas pública, aplicación, datos, operacional, administrativa y protección, con conductos permitidos explícitamente.

Los datos se cifran en tránsito y reposo. Las claves, secretos y certificados se administran con separación de funciones y rotación; el material necesario para las cinco funciones críticas existe protegido en el terminal, de modo que la operación local no depende de un gestor de claves inaccesible. De los 28 campos sensibles identificados por Célula 4, ocho campos indexados tienen patrones de protección propuestos o condicionados. No se declara aprobada una técnica de cifrado determinista: la elección por campo requiere clasificación final, patrón de consulta, evaluación de riesgo y aprobación correspondiente.

`SRV-IAM` mantiene localmente identidades, permisos, sesiones y revocaciones vigentes. Las altas y sincronizaciones centrales pueden esperar al enlace; una desvinculación conocida localmente no espera la reconexión. `SRV-EVID` registra firma, sello, hash y cadena de custodia. La plataforma única de observabilidad y SIEM recibe métricas, logs y trazas de nube y on-premise; durante el corte usa un colector y buffer local, y al reconectar reenvía sin pérdida ni duplicación. El diseño completo se conserva en [D1](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md) y [D2](../03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md).

### 4.1.5 Decisiones de arquitectura y cumplimiento

El registro contiene once decisiones arquitectónicas. Todas permanecen en estado `PROPUESTO` porque el Informe 1 formula la arquitectura, pero no reemplaza la aprobación del CLIENTE ni las verificaciones posteriores.

#### Tabla T-SD4-07 — decisiones arquitectónicas

| ADR | Decisión propuesta | Alternativa descartada / consecuencia | Condición principal |
|---|---|---|---|
| `ADR-001` | modular híbrida por dominios | monolito o microservicios finos: menor aislamiento o complejidad excesiva | validar límites con contratos y pruebas |
| `ADR-002` | cinco funciones críticas y apoyos acotados en `EDGE-RUN` | sin runtime viola continuidad; réplica total duplica innecesariamente la nube | prueba aislada de 72 h y reconciliación |
| `ADR-003` | contratos gobernados, eventos y mensajería durable | punto a punto propaga acoplamiento; bus autogestionado aumenta carga operativa | levantar contratos reales |
| `ADR-004` | autoridad única por dominio, zona y fase | TOS indefinido perpetúa obsolescencia; big bang concentra riesgo | validación paralela, conciliación y retorno |
| `ADR-005` | adecuar sala si supera tres puertas; fallback modular | aceptar la sala sin validar conserva sus brechas actuales | site survey, ruta diversa y costo/plazo |
| `ADR-006` | LTE/5G privada segmentada | red inalámbrica genérica no resuelve movilidad y sombras del patio | estudio de cobertura y espectro |
| `ADR-007` | almacenamiento tolerante a falla y respaldo 3-2-1-1-0 | una sola copia o autoridad de borrado común impide recuperación confiable | pruebas de restauración y selección final |
| `ADR-008` | identidad central con capacidad local acotada | IAM solo cloud detiene operación; IAM duplicado fragmenta gobierno | producto, revocación y pruebas offline |
| `ADR-009` | KMS/HSM y material local protegido | claves solo cloud hacen ilegibles los datos durante el corte | ceremonia, custodia y separación de funciones |
| `ADR-010` | registro común, SIEM y SOC 24×7 | vigilancia absorbida por TI=5 no sostiene cobertura continua | medir ingesta y acordar operación |
| `ADR-011` | AWS `sa-east-1` primaria y `us-east-1` secundaria | multicloud reduce fallo común pero excede la complejidad operable; queda riesgo AWS | latencia, residencia, catálogo, certificaciones y carbono |

El cumplimiento arquitectónico se traza contra las Bases Administrativas y Técnicas, el caso y los formularios. En particular, el Artículo 16 se satisface mediante una arquitectura **híbrida justificada componente por componente**, considerando latencia, criticidad, volumen, seguridad/regulación, conectividad, acoplamiento físico y costo total cualitativo. No se usa la palabra “híbrida” como etiqueta: las cinco funciones críticas se ubican localmente porque no pueden detenerse ante un corte, mientras que exposición, consolidación, analítica e integraciones externas se ubican en nube por elasticidad, aislamiento y operación administrada. La matriz de cobertura completa está en [MA-6](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md) y las decisiones en el [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md).

La acreditación del Artículo 4 no consiste en enumerar normas. Cada familia se vincula a un control, un componente y una evidencia distinguida por etapa. Por ejemplo: ISO/IEC/IEEE 42010 se evidencia mediante las cinco vistas y sus correspondencias; ISO/IEC 27001/27002 mediante IAM, segregación, cifrado y registro; IEC 62443 mediante zonas y conductos de la red operacional; ISO 14083 mediante fórmula versionada, linaje y reporte de emisiones; y WCAG 2.2 AA mediante criterios de interfaz y pruebas futuras de accesibilidad. La cobertura completa de 38 estándares/prácticas y 15 materias normativas permanece en MA-6 para evitar duplicarla.

## 4.2 Arquitectura física

### 4.2.1 Arquitectura física y emplazamiento

La arquitectura física tiene tres ámbitos coordinados:

1. **AWS primaria:** `sa-east-1`, distribuida en al menos dos zonas de disponibilidad para servicios centrales, datos y exposición.
2. **Terminal portuario:** sala técnica con `EDGE-RUN`, almacenamiento, `INT-TOS`, red operacional, identidad/evidencia local y borde instrumentado en gate, patio, reefers y muelle.
3. **AWS secundaria:** `us-east-1`, activo-pasivo, destinada a recuperación ante desastres.

La nube es el primario en operación normal. El núcleo local mantiene una copia caliente y operable del estado crítico; durante la pérdida del enlace se convierte temporalmente en autoridad de esas funciones, no de toda la plataforma. La región de DR no sustituye esa continuidad local: resuelve la pérdida del sitio o de la región primaria con objetivos RTO/RPO distintos.

#### Tabla T-SD4-03 — resumen de emplazamiento

| Familia / ubicación | Latencia y criticidad | Volumen | Seguridad / regulación | Conectividad y acoplamiento | TCO cualitativo |
|---|---|---|---|---|---|
| AWS `sa-east-1` | >100 ms aceptable para central/no crítico; multi-AZ | consolidado, documentos y analítica | única exposición pública protegida; datos cifrados | requiere WAN; sin acoplamiento físico | elasticidad y servicios gestionados reducen operación |
| Sala técnica | ≤1 s y cinco funciones críticas por 72 h | estado y buffer caliente, no histórico total | zona operacional segregada y claves locales | TOS y operación están en el terminal | inversión local acotada por continuidad |
| Gate, 8+6 | OCR ≤3 s; camión ≤120 s | evento e imagen por camión | zona primaria y dato personal | báscula, barrera y OCR físicos | gabinete por puesto evita dependencia remota |
| Patio, 18 ha | confirmación local; terminal offline 8 h | 37→44 ev/s de posición | red operacional privada | movilidad y sombras de pilas | 6–8 estaciones sujetas a cobertura |
| Reefers, 26→32 | alarma ≤5 min, crítica | 35,8→43,3 ev/s | evidencia de cadena de frío | directo a tomas/tableros | concentrador por tablero reduce ronda manual |
| Muelle, 3 sitios | interacción operacional local | bajo/moderado | grúas solo lectura y autorización del fabricante | acoplamiento de cabina/muelle | borde mínimo, sin intervenir control |
| AWS `us-east-1` | RTO ≤4 h/RPO ≤15 min | réplica de datos críticos y objetos | copia inmutable y autoridad separada | no depende del recinto; comparte proveedor AWS | capacidad reducida en reposo |

El terminal no tiene un segundo recinto del CLIENTE; por ello, otro rack dentro del mismo emplazamiento sería alta disponibilidad local, no un data center secundario. El análisis completo por componente está en [C1 §§4–6](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md).

### 4.2.2 Especificaciones de tecnologías de software

#### Tabla T-SD4-04 — baseline tecnológica

| Función | Selección de referencia | Alternativa | Modalidad / ubicación | Vigencia |
|---|---|---|---|---|
| Portal | React + TypeScript | Angular | propia; servida desde AWS | rama soportada + WCAG 2.2 AA |
| Backend | Java + Spring Boot | .NET; Go en borde | contenedor propio; misma imagen nube/sala | runtime LTS |
| Contratos | OpenAPI 3.1 + AsyncAPI 2.6 o superior | — | especificación `contract-first` | estándar y contrato versionados |
| App terreno | React Native | Flutter o nativa certificada | instalable; dispositivo robusto | versión mayor soportada |
| Persistencia móvil | SQLite cifrado | equivalente embebido | dispositivo; offline 8 h | compatible con SO certificado |
| Gateway | Kong híbrido o equivalente | gestionado exportable | central AWS + perfil local restringido | misma política compatible |
| Ejecución | Amazon EKS + Kubernetes ligero | contenedor gestionado | gestionada AWS + local acotada | rama soportada por ambos |
| Datos | RDS PostgreSQL Multi-AZ + PostgreSQL local | motor equivalente | AWS + sala | versión mayor soportada |
| Series | extensión PostgreSQL | motor temporal dedicado | central + ventana caliente local | compatible con motor base |
| Objetos | Amazon S3 Versioning/Lifecycle/Object Lock | equivalente del catálogo AWS | gestionada AWS | servicio vigente |
| Eventos | EventBridge + SQS FIFO/DLQ | Kafka/RabbitMQ | gestionada AWS + buffer local | servicio/rama soportados |
| Analítica | Athena + Glue | almacén dedicado | gestionada AWS | servicio vigente |
| Observabilidad | CloudWatch + ADOT + OpenSearch | SIEM compatible OTel | común nube/sala, colector local | OpenTelemetry vigente |
| IaC | Terraform u OpenTofu | — | repositorio del CLIENTE | rama soportada |
| Sistema operativo | Linux empresarial + CIS | distribución equivalente | núcleo y borde compatibles | soporte durante 56 meses |

Las versiones exactas se congelan antes de la oferta según soporte y fin de vida; durante los 56 meses ningún componente debe entrar o permanecer en producción sin soporte vigente. Los marcos incorporados al desarrollo no generan por sí solos una fila T-11. Sí la generan una plataforma gestionada, licencia propietaria, soporte comercial o servicio contratado. La especificación y alternativas completas están en [C2 §§3–4](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md).

### 4.2.3 Especificaciones de implementos de hardware y software

La selección física parte de la disponibilidad, no del TPS: el volumen transaccional es bajo, pero la continuidad exige cuórum, red en alta disponibilidad, energía y climatización redundantes. El núcleo local considera tres servidores empresariales, almacenamiento tolerante al fallo de al menos un disco, pares de conmutación y cortafuegos, y dos racks separados por función. El borde utiliza gabinetes de protección marina, terminales robustos y concentradores de reefers.

| Familia | Baseline de cantidad/capacidad | Condición o criterio |
|---|---|---|
| Servidores del núcleo | 3 nodos de referencia, 16 núcleos, 128 GB RAM, 2×10 GbE por nodo | mínimo de cuórum y N+1; modelo final según cálculo |
| Almacenamiento local | referencia 4×480 GB SSD RAID 10, ≈960 GB útiles | capacidad requerida ≈183 GB útiles; tolerancia y salud predictiva |
| Red de núcleo | 2 conmutadores + 2 cortafuegos | alta disponibilidad sin punto único |
| Racks | 2 racks 42U con PDU A/B | cómputo/almacenamiento separado de comunicaciones/seguridad |
| Gabinetes de borde | 59–61, baseline por sitios conocidos y rango del patio | IP66 marino; patio se cierra con site survey |
| Concentradores reefer | 26, expansión a 32 | uno por tablero |
| Terminales robustos | 97: 88 operativos + 9 de reserva | IP65 o superior, guantes, caída y batería por turno |
| Estaciones de patio | rango 6–8 | cobertura manda; cantidad/ubicación mediante site survey |
| Puestos de operación | 3 de baseline | 2 diurnos + 1 guardia; validar AHT |
| Plataforma AWS | 1 primaria + 1 sitio lógico DR | elasticidad, multi-AZ y activo-pasivo |

Todo equipo de terreno debe ser nuevo, administrable, con grado de protección y resistencia coherentes con salinidad, humedad, polvo, vibración, luminosidad y uso con guantes. Su ciclo de vida, repuestos y reposición cubren los 56 meses; una unidad de cada tipo se somete a aceptación antes de compra masiva. La adquisición puede corresponder al CLIENTE sin que TERABYTE deje de especificarla. El detalle 1:1 se conserva en [C2 §§7–9](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) y [C4 §9](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).

### 4.2.4 Especificaciones del data center primario

El sitio principal local es la sala técnica de 34 m² existente en el terminal, **condicionada** a superar tres puertas: factibilidad física y de plazo; diversidad real de rutas de telecomunicaciones; y costo/riesgo comparado con una sala modular. Si una puerta falla, se adopta una solución modular dentro del recinto en ubicación validada por el CLIENTE. No se declara que la sala actual ya cumple.

#### Tabla T-SD4-05 — baseline de sala

| Materia | Especificación propuesta |
|---|---|
| Uso y distribución | recinto exclusivo; zonas de racks, comunicaciones, energía, climatización y respaldo; operación habitual fuera de la sala |
| Racks y cableado | 2 racks 42U, PDU A/B, piso/canalización y enlaces certificados |
| Energía | carga TI de diseño ≈2,67 kW; 2 UPS de 6 kVA/≥5,4 kW, cada una capaz de sostener la carga, autonomía ≥30 min |
| Generación | grupo ≥15 kVA, ATS y combustible útil ≥120 L, sujeto a curva certificada y prueba de 24 h |
| Climatización | 2 unidades de precisión de 18.000 BTU/h en N+1, monitoreo de temperatura, humedad y agua |
| Incendio | detección temprana por aspiración y extinción automática por agente limpio aprobada para el uso |
| Acceso | control biométrico, respaldo definido, esclusa, bitácora y acompañamiento de terceros |
| Videovigilancia | 4 cámaras y NVR ≥4 TB útiles, al menos 30 días en línea |
| Ambiente y eficiencia | puesta a tierra, segregación eléctrica, monitoreo y PUE de referencia medido y recalculado tras levantamiento |
| Comunicaciones | ingresos por puntos separados y rutas físicas distintas |
| Sitio secundario | AWS `us-east-1`, activo-pasivo, réplica caliente, IaC y capacidad reducida |
| Recuperación | RTO ≤4 h, RPO ≤15 min, retorno reconciliado y prueba real semestral futura |

La obra civil es responsabilidad del CLIENTE; TERABYTE especifica y coordina. Potencias, combustible, distribución, PUE, resistencia de piso, rutas, incendio y controles se validan mediante levantamiento, fichas y pruebas de aceptación. Referencia completa: [C2 §5](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) y [C4 §6.2.bis](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).

### 4.2.5 Especificaciones del data center secundario

El sitio secundario se propone en AWS `us-east-1`, separado del primario `sa-east-1`, en modalidad activo-pasivo con réplica caliente y capacidad de cómputo reducida en reposo. Replica los datos y artefactos necesarios para restaurar servicios críticos; la infraestructura se reconstruye desde código versionado.

La replicación es continua y mide su retraso. Los objetivos son **RTO ≤4 horas y RPO ≤15 minutos** para servicios críticos. La conmutación se documenta y automatiza en la medida necesaria para que el personal del CLIENTE pueda ejecutarla tras la transferencia de conocimiento. El retorno incluye los datos generados durante la contingencia y evita restablecer escrituras concurrentes.

Los respaldos siguen el esquema 3-2-1-1-0: tres copias, dos medios, una fuera de sitio, una inmutable o fuera de línea y cero errores verificados. Se cifran con autoridad de clave separada; la restauración se ensaya mensualmente sobre muestra representativa y el DR mediante conmutación real al menos dos veces por año, fuera de las ventanas operacionales restringidas.

Existe un riesgo residual de dominio común porque ambas regiones pertenecen a AWS. Se conserva como `SPOF-22` y no se confunde con la recuperabilidad del respaldo. Para Informe 1 se mitiga con separación regional, IaC, copia inmutable y autoridad de borrado separada; la evidencia de RTO/RPO corresponde a pruebas futuras. Fuentes: [C2 §6](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) y [C3 §9](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md).

### 4.2.6 Despliegue, redes y continuidad

Se separan cinco ambientes: desarrollo, integración, pruebas/QA, preproducción y producción. Cada uno mantiene identidades, secretos, datos y permisos diferenciados; producción no comparte credenciales ni datos con ambientes no productivos. La entrega continua construye un artefacto único, genera inventario de componentes, firma su procedencia y promueve el mismo artefacto entre ambientes mediante infraestructura como código y aprobaciones segregadas.

La red se divide en zonas y conductos. La exposición pública termina en AWS; la sala separa redes de aplicación, datos, administración y operación; los sistemas de protección mantienen su frontera. Gate, patio, reefers y muelle usan una red privada LTE/5G segmentada. La cantidad y ubicación de estaciones no se inventan: el rango inicial de 6–8 se valida con site survey, medición de cobertura, interferencia, latencia, roaming y comportamiento con pilas de contenedores.

El terminal dispone de **dos enlaces WAN**, con proveedores distintos, rutas físicas distintas e ingreso separado al edificio. La capacidad mínima disponible propuesta es 35 Mbps por la exigencia de reposición del peak actual, no por el tráfico ordinario. La capacidad real de ambos caminos y su conmutación deben medirse; no se agrega un tercer enlace a la baseline ni al T-11.

Durante un corte exterior, los servicios críticos utilizan tiempo, DNS, certificados, claves, identidad, datos, colas y registros locales. El portal externo, la mensajería hacia contrapartes, la planificación nueva, las inspecciones nuevas, el cálculo de emisiones, la analítica y la administración central se degradan explícitamente. Los equipos de patio tienen además hasta 8 horas de autonomía frente a una sombra de radio local, condición distinta de las 72 horas sin WAN.

El retorno ocurre en cuatro pasos: detectar enlace estable; cerrar y sellar el tramo local; transmitir eventos ordenados e idempotentes; conciliar autoridad, evidencia y observabilidad. Debe terminar en ≤90 minutos para el buffer dimensionado. El DR regional, con RTO 4 h/RPO 15 min, se activa ante pérdida de sitio o región; no sustituye esta reconciliación. Plan, matrices y pruebas propuestas: [C3 §§2–12](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md).

### 4.2.7 Dimensionamiento y plan de capacidad

El cálculo parte de la volumetría del caso y conserva como supuestos declarados el tamaño de registro, evento e imagen, las tasas de concurrencia, la frecuencia de posicionamiento y el tiempo medio de atención. De 18 dimensiones heredadas, 15 se confirmaron y 3 se corrigieron: ancho de banda del patio, buffer de 72 horas y velocidad de sincronización. La carga dominante es telemetría y posicionamiento, no las transacciones de negocio.

#### Tabla T-SD4-06 — cifras de diseño

| Variable | Actual/normal | Peak o proyección | Fórmula o supuesto decisivo | Uso en diseño |
|---|---:|---:|---|---|
| TPS de negocio | 0,1089 | 0,233 actual; 0,266 proyectado | transacciones anuales/31.536.000 s; coincidencia muelle+gate+patio | pruebas a 1,5× peak |
| Telemetría reefer | 35,8 ev/s | 43,3 ev/s | tomas/60 s local | `DATA-TS` y borde reefer |
| Posicionamiento | 37 ev/s | 44 ev/s | un evento/2 s/equipo `[supuesto]` | red de patio y series |
| Concurrencia interna | 160 | 175 | 25 % del universo `[supuesto]` | canales e identidad |
| Concurrencia externa | 159 | 187 | 8 % del universo `[supuesto]` | portal, identidad y borde |
| Buffer 72 h | 13,7 GB | **21,9 GB peak actual** | tasa de datos ×259.200 s | almacenamiento local |
| Reposición 90 min | 20,3 Mbps | **32,5 Mbps peak actual** | bytes×8/5.400 s | WAN disponible ≥35 Mbps |
| Escenario futuro 3× | 39 GB | 57,8 Mbps | triple de carga; escenario separado | gatillo de ampliación |
| Imagen de 1 MB | ≈40 GB | ≈58 Mbps | sensibilidad sobre 500 KB `[supuesto]` | validar tamaño real |
| Capacidad local | — | ≈183 GB útiles +30 % | hot data + buffer + réplica + SO/logs | cabe en ≈960 GB útiles |
| Imágenes OCR | ≈1,43 TB/año | ≈1,67 TB/año | eventos×500 KB×1,2 `[supuesto]` | objetos y ciclo de vida |
| Series reefer | ≈68 GB/año | ≈82 GB/año | eventos×100 B×3 `[supuesto]` | retención y capas |

El primer cuello de botella esperado es la cobertura operacional del patio, porque la ubicación de estaciones depende de la geometría y cambia con las pilas; el segundo es la capacidad efectiva del enlace alternativo durante la reposición. El tamaño real de las imágenes es el supuesto más sensible: se mide antes de congelar capacidad.

Se mantiene un margen del 30 % sobre la carga proyectada. Los disparadores de ampliación incluyen utilización sostenida de cómputo/memoria/almacenamiento, ocupación de colas, retraso de replicación, duración de sincronización, cobertura o latencia fuera de objetivo y crecimiento real de documentos. La ampliación se planifica antes de alcanzar el umbral y respeta la prohibición de intervenciones entre el 15 de diciembre y el 30 de abril. El cálculo reproducible está en [C4 §§2–9](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).

### 4.2.8 Formulario T-11

El Formulario T-11 consolidado contiene **32 filas** y exactamente las cinco columnas contractuales: componente, producto o servicio, ubicación/lugar, cantidad y justificación. No incluye precios. Cada fila vuelve a un nodo físico, cálculo, control o servicio; una capacidad nativa no se cuenta como una compra adicional.

El formulario incluye cómputo, almacenamiento, red, energía, climatización, sala, borde, dispositivos de terreno, conectividad, nube, DR, observabilidad/SIEM, identidad, claves, SOC, pruebas de seguridad, plataforma de ingeniería, soporte y servicios. Los productos de referencia no equivalen a compra ni aceptación. Las cantidades sujetas a levantamiento se expresan como rango y mecanismo de cierre; las adquisiciones que correspondan al CLIENTE conservan especificación y trazabilidad.

Se incorpora por referencia el contenido completo de [Formulario T-11 final](02_FORMULARIO_T11_FINAL.md). La matriz ampliada con origen, cálculo y control 1:1 se mantiene en [T-11 de trabajo trazable](01_T11_TRABAJO_TRAZABLE.md), evitando duplicar 32 filas dentro de este texto.

## Pendientes legítimos y evidencia posterior

La base técnica conserva estas condiciones sin convertir incertidumbre en promesa. Antes de congelar el diseño deberán resolverse, según su hito: site survey del patio y de la sala; capacidad y diversidad reales de los dos enlaces; tamaño real de imágenes y base TOS; contratos y protocolos de integraciones; producto IAM; clasificación final de datos/campos; medición de logs dominantes; fichas eléctricas, térmicas y marinas; soporte y versiones finales; residencia, latencia, catálogo, certificaciones y carbono de las regiones AWS.

Las pruebas de 72 horas, reconciliación ≤90 minutos, conmutación DR, restauración, cobertura, aceptación de dispositivos, seguridad y carga son evidencia de ejecución posterior. Su ausencia en el Informe 1 no cambia la baseline, siempre que cada una mantenga responsable, método, umbral y momento de cierre.

#### Tabla T-SD4-08 — dependencias externas y tratamiento

| Dato o evidencia | Dueño de cierre | Hito | Baseline/fallback del Informe 1 | Efecto si cambia |
|---|---|---|---|---|
| sala, rutas y ambiente | CLIENTE + TERABYTE | site survey previo al diseño de detalle | sala de 34 m² condicionada; fallback modular | ubicación, obra y cantidades auxiliares |
| cobertura LTE/5G | TERABYTE + CLIENTE | estudio en terreno | rango 6–8; terminal offline 8 h | cantidad y ubicación de estaciones |
| capacidad de los dos WAN | proveedores + CLIENTE | medición y prueba de conmutación | ≥35 Mbps disponibles por camino útil | tiempo de reposición y capacidad contratada |
| imagen OCR y base TOS | CLIENTE/proveedores | levantamiento de datos | 500 KB e histórico ≈480 GB como supuestos | buffer, WAN y migración |
| contratos TOS/ERP/navieras/autoridades/ferrocarril | cada contraparte | diseño de interfaces/Sobre N.º 2 | patrones A2 + colas/fallback asistido | adaptadores, pruebas y calendario |
| clasificación de campos y producto IAM | CLIENTE + seguridad | diseño detallado | catálogo 28/8 y patrón IAM híbrido condicionados | búsqueda, cifrado, licencias y operación local |
| fichas eléctricas, térmicas y marinas | fabricantes + TERABYTE | selección y aceptación | mínimos C2/C4 | modelos, potencia y autonomía finales |
| AWS: latencia, residencia, catálogo, certificaciones y carbono | TERABYTE + CLIENTE | congelamiento de oferta | `sa-east-1`/`us-east-1` propuestas | revisión registrada de `ADR-011` |

## Fuentes de control

- [A1 — Contexto y arquitectura lógica](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md)
- [A2 — Arquitectura de integración](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md)
- [A3 — Procesos críticos y convivencia TOS](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md)
- [C1 — Arquitectura física y emplazamiento](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md)
- [C2 — Tecnologías, hardware y data centers](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md)
- [C3 — Despliegue, red y continuidad](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md)
- [C4 — Dimensionamiento y T-11](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md)
- [D1 — Arquitectura de seguridad](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md)
- [D2 — Amenazas, ADR y puntos de falla](../03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md)
- [Registro ADR global](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md)
- [Matriz de cumplimiento](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md)
