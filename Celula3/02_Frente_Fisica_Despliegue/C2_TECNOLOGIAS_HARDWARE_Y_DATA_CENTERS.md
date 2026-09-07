# C2 — Tecnologías, hardware y data centers

## Contrato del entregable

### Objetivo y destino

Especificar las tecnologías y los implementos que materializan la arquitectura, incluido recinto primario y secundario/DR. Alimenta las secciones 4.2.2–4.2.5.

### Cumplimientos asignados

- T21 4.2 b), c), d), e) y Formulario T-11.
- `SD4-02`, `SD4-05`, `SD4-06`, `SD4-08`.
- BTT Cap. 6 completo: `RT-06.01` a `RT-06.34`. BTT Cap. 7 completo: `RT-07.01` a `RT-07.14`. BTT Cap. 3 y Cap. 8; `MC-09/10/11/12`.
- Checklist del BTT, Cap. C, entregables N° 8 (site principal y secundario, **con planos**) y N° 10 (hardware y dispositivos de terreno).

> *Corrección `F2-COR-002` (2026-09-05): el contrato declaraba `RT-06.01..24` y no mencionaba el Capítulo 7. El numeral 3.2 del BTT dice «se aplican íntegramente los requisitos **RT-06.01 a RT-06.34**»; los diez omitidos son tres subcapítulos de este frente —6.7 custodia de medios, 6.8 espacio de operación del personal y 6.9 rutas de comunicaciones—. El Capítulo 7, site secundario y recuperación ante desastres, no estaba citado en ninguna parte de Célula 3 pese a que `T21-4.2-E` es elemento evaluado. Ver `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`, `F2-ESC-003` y `F2-ESC-004`.*

### Entradas obligatorias

- C1 topología `v0.1`, C4 cálculos preliminares y D1 controles/componentes.
- Maestro §§4.3, 9–12, 15–16, 18–19.
- BTT infraestructura on-premise, hardware de terreno, seguridad y continuidad.

### Trabajo requerido

- [ ] Definir tecnologías de software, versiones o política de vigencia/EOS.
- [ ] Comparar productos/servicios de referencia cuando la elección sea relevante.
- [ ] Justificar gestionado vs. autogestionado y reversibilidad.
- [ ] Especificar cómputo, memoria, almacenamiento, interfaces, consumo y redundancia.
- [ ] Definir almacenamiento/RAID con tolerancia y capacidad.
- [ ] Especificar switches, firewalls, balanceadores y energía en HA.
- [ ] Detallar data center/sala primario y secundario/DR.
- [ ] Detallar racks, UPS, generación, climatización, incendio, acceso y monitoreo.
- [ ] Especificar custodia de medios de respaldo: recinto, condiciones ambientales, inventario y rotación (`RT-06.26..28`).
- [ ] Especificar el espacio de operación del personal, separado de la sala de equipos, y declarar qué instalaciones existentes se reutilizan (`RT-06.29..31`).
- [ ] Especificar rutas de comunicaciones físicamente distintas con ingreso al edificio por puntos separados, y las canalizaciones requeridas (`RT-06.32/33`).
- [ ] Especificar el site secundario: modalidad activo-activo o activo-pasivo justificada, distancia al principal y análisis de amenazas comunes (`RT-07.01/02`).
- [ ] Declarar la disponibilidad mensual por componente del recinto —energía, climatización, red, cómputo, motor de base de datos y portal— conforme al numeral 7.2 del BTT.
- [ ] Declarar las dos tensiones registradas: biometría del recinto (`F2-DEC-002`) y CCTV propio del recinto frente al VMS conservado (`F2-DEC-003`).
- [ ] Especificar gabinetes/dispositivos por clase marina y ubicación.
- [ ] Incluir puestos de trabajo/monitores duales solo donde el dimensionamiento lo justifique.
- [ ] Entregar candidatos T-11 sin precios.

### Catálogo tecnológico obligatorio

| ID | Componente físico | Producto/servicio o referencia | Versión/vigencia | Especificación mínima | Ubicación | Cantidad/criterio | HA/energía | Operación/mantenimiento | Alternativa | Justificación | T-11 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| POR COMPLETAR | — | — | — | — | — | — | — | — | — | — | — |

### Tabla marina obligatoria

| Clase/ubicación | Riesgos | IP/NEMA | Anticorrosión/material | Temperatura/humedad | Energía/UPS | Vida útil/reposición | Prueba de recepción | Cantidad |
|---|---|---|---|---|---|---|---|---|
| gabinete de borde | salinidad/intemperie | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | POR DEFINIR | C4 |

### Reglas importantes

- Si se propone sala principal sustantiva, aplicar `BTT, Cap. 6, RT-06.01` a `RT-06.34` íntegros *(rango corregido; ver la nota `F2-COR-002` arriba y `F2-COR-009`)*.
- UPS ≥30 min a plena carga y generación ≥24 h donde aplique.
- Separar racks de cómputo y comunicaciones; declarar kW, factor de potencia y PUE.
- Equipamiento nuevo y con garantía.
- Marca/modelo son referencias justificadas, no relleno comercial.
- No sobredimensionar: toda capacidad debe volver a C4.
- No incluir costos unitarios en Informe 1 pese a que la base técnica los mencione; registrar la tensión y mantener solo especificación/cantidad.

### Productos obligatorios

1. Catálogo tecnológico completo.
2. Especificación del primario y secundario/DR.
3. Plano conceptual de sala/racks o distribución aplicable.
4. Tabla de protección marina.
5. Candidatos de T-11 y aportes `ADR-005/007`.

### Salidas hacia otros frentes

- Frente 3: productos, superficies de administración, logs, identidades y actualizaciones.
- C4: SKU/referencia, unidad de cantidad y variables de cálculo.

### Definición de terminado *(lista normativa del contrato — no es estado)*

> **Cómo leer estas casillas.** Son la **lista de exigencias** que el contrato de este entregable fija al empezar, y se conservan sin marcar a propósito: son el enunciado, no el avance. **El estado vigente y fechado está en la última sección de este documento**, «§12 Definición de terminado — estado». Si las dos se leen como estado, un mismo control aparece pendiente y cumplido a la vez, que es lo que observó `AGC3-019`.

- [ ] Todo producto materializa una caja física o control obligatorio.
- [ ] Versiones y soporte están declarados o existe criterio de vigencia.
- [ ] Sala y equipos cumplen ambiente, energía, HA y mantenimiento.
- [ ] Cantidades se vinculan a C4; no hay precios.
- [ ] Primario/secundario y responsabilidades están diferenciados.
- [ ] `TRZ_C2.md` completo.

## Contenido listo para integrar

**Versión:** `v0.5` — contenido completo, sujeto a revisión cruzada en la Puerta 2.
**Fecha:** 2026-09-05. **Destino:** consolidado 4.2.3 a 4.2.6.

### 1. Lo primero: la tipología de recinto ya está decidida por el caso

El numeral 6.1 del BTT obliga a algo que es fácil pasar por alto: **declarar expresamente qué tipología de recinto se adopta en cada sitio**, entre tres posibles, y advierte que *«sobredimensionar el recinto es tan penalizado como subdimensionarlo: ambos revelan que el cálculo de capacidad no se hizo»*.

| Tipología del BTT | Cuándo aplica | Exigencia |
|---|---|---|
| Sala técnica principal | el caso requiere cómputo, almacenamiento y procesamiento **sustantivos** en instalaciones del CLIENTE | `RT-06.01` a `RT-06.34` **íntegros** |
| Sala técnica secundaria o de sitio | cómputo local para continuidad, **pero no alberga el núcleo** | energía, climatización, control de acceso, detección de incendio y monitoreo, dimensionados al sitio |
| Gabinete o borde operacional | equipamiento mínimo en punto de operación | protección eléctrica, control de acceso físico, monitoreo remoto y condiciones ambientales del equipo |

El caso no deja esto abierto. `CP, Cap. 15, RT-06.01` —materia «tipología del emplazamiento on-premise»— dice textualmente:

> «**Sala de servidores principal del terminal, que debe habilitarse o reemplazarse**: la actual, de 34 m² habilitada en 2012 a menos de 300 metros de la línea de costa, **no cumple el Capítulo 6 del documento transversal**. **Gabinetes de borde en muelle, patio, patio refrigerado y gate**, con grado de protección y tratamiento anticorrosivo acreditados para atmósfera marina, y con autonomía eléctrica compatible con la restricción no negociable N° 4.»

De ahí salen tres consecuencias que conviene fijar antes de especificar un solo equipo.

**Primera: hay sala principal, y por lo tanto `RT-06.01` a `RT-06.34` aplican completos.** No es una elección nuestra. Además, nuestro núcleo operacional local (`PHY-OPS-01`) alberga las cinco funciones críticas y su almacenamiento, o sea que es «cómputo sustantivo» y «alberga el núcleo» según ambos criterios del cuadro. Ninguna de las dos condiciones para bajar a tipología «secundaria o de sitio» se cumple.

**Segunda: esto acota `ADR-005` más de lo que parecía.** El verbo del caso es «habilitarse **o** reemplazarse»: las dos primeras alternativas de la Decisión N° 20 —endurecer la actual, construir una nueva— siguen vivas. Pero la tercera, «borde mínimo más nube», **si se entiende como no tener sala principal, está excluida por el caso**, y si se entiende como tener una más pequeña, entonces no es una tercera alternativa sino una variante dimensional de la segunda, y arrastra los 34 requisitos igual. En C1 §7 se había anticipado que «C se distingue de B por el tamaño del recinto, no por la existencia de cómputo local»; el `RT-06.01` del caso lo confirma con texto citable. Se registra en `F2-DEC-001`.

**Tercera: el caso nombra cuatro zonas de borde, no cinco.** Muelle, patio, patio refrigerado y gate. La zona de inspección, que C1 listó como `PHY-EDG-05`, **no requiere gabinete propio**: se atiende con dispositivo móvil sobre la red operacional del patio, que es donde físicamente ocurre la inspección. Se corrige aquí y se anota en `TRZ-C1`, para no inventar un recinto que el caso no pide y que nadie podría justificar en el T-11.

### 2. Tipología declarada por sitio

Cumple la exigencia de declaración del numeral 6.1.

| Sitio | Tipología adoptada | Exigencia que aplica | Justificación |
|---|---|---|---|
| Sala técnica del terminal | **Sala técnica principal** | `RT-06.01` a `RT-06.34` íntegros | alberga `PHY-OPS-01` a `PHY-OPS-05`: las cinco funciones críticas, su almacenamiento y la capa anticorrupción. `CP, Cap. 15, RT-06.01` la nombra como sala principal |
| Espacio de operación del personal | recinto anexo, **no técnico** | `RT-06.29` a `RT-06.31` | separado de la sala de equipos por mandato de `RT-06.30`; no aloja equipamiento de cómputo |
| Recinto de custodia de medios | recinto anexo, **no técnico** | `RT-06.26` a `RT-06.28` | condiciones ambientales de conservación de medios, no de operación |
| Gate — 8 entradas + 6 salidas | **Gabinete o borde operacional** | protección eléctrica, acceso físico, monitoreo remoto y condiciones ambientales | nombrado por `CP, Cap. 15, RT-06.01`; equipamiento mínimo por puesto |
| Patio — 18 ha | **Gabinete o borde operacional** | ídem | ídem |
| Patio refrigerado — 26 tableros | **Gabinete o borde operacional** | ídem | ídem; concentrador por tablero |
| Muelle — 3 sitios | **Gabinete o borde operacional** | ídem | ídem; sin intervención del control de grúas |
| Zona de inspección | **sin recinto propio** | — | se sirve por la red operacional del patio y dispositivo móvil. El caso no la nombra entre las zonas con gabinete |
| Nube primaria y secundaria | fuera de la tipología del Cap. 6 | BTT Cap. 3 y Cap. 7 | responsabilidad del proveedor; se declara región y zonas |

### 3. Tecnologías de software

`RT-08.01` obliga a especificar con marca y **modelo de referencia**; el numeral 6.5 del BTT usa la fórmula «tipo AnaLASER **o equivalente de prestaciones iguales o superiores**». Adoptamos esa misma regla en todo el catálogo: **el producto nombrado es referencia y la especificación es lo vinculante**; cualquier equivalente que la satisfaga es admisible. Un nombre de producto sin la especificación que lo justifica sería relleno comercial, que el propio contrato de este paquete prohíbe.

**Línea base para Informe 1 y control de versión.** La columna «Referencia» es la selección técnica principal de este corte; la columna «Alternativa» conserva la opción evaluada y no representa una segunda oferta simultánea. La versión exacta se congela en el catálogo/T-11 al cierre de la oferta, junto con su fecha de fin de soporte; durante los 56 meses se mantiene en una rama LTS o equivalente y **ningún componente entra ni permanece en producción con soporte vencido**, con ventana de actualización conforme a `RT-03.15`. Así se evita tanto una lista de opciones sin decisión como prometer hoy una versión inmutable durante todo el Contrato.

| Capa | Función | Referencia | Alternativa | Gestionado o autogestionado | Criterio de vigencia |
|---|---|---|---|---|---|
| **Canal web** | `CH-PORTAL`: portal público y autenticado, y perfil de administración funcional | aplicación web de página única sobre **React** con TypeScript, o equivalente con soporte a largo plazo | **Angular** con TypeScript, si se prefiere un marco con opinión completa y ciclo de soporte publicado | autogestionado; se sirve como contenido estático desde `PHY-CLD-01` | rama LTS o versión mayor con soporte del proyecto durante todo el Contrato; **WCAG 2.2 AA** verificable (`RT-13.01`) y bilingüe (`RT-13.12`, endurecido por el caso) |
| **Backend y APIs** | `CTX-*`, `SRV-*`, `INT-*`: lógica de negocio, contratos y eventos | servicios en contenedor sobre **Java con Spring Boot**, o equivalente de plataforma empresarial con soporte a largo plazo | **.NET** con ASP.NET Core, o **Go** para los servicios de borde donde el tamaño de imagen y el arranque importen | autogestionado, en la misma pila de contenedores de la fila «Ejecución de servicios» | versión LTS del runtime y del marco; **la misma imagen debe correr en nube y en la sala**, sin dependencia del plano de control del proveedor (regla negativa 8) |
| **Contratos de interfaz** | `RT-05.16`: documentación de interfaces | **OpenAPI 3.1** para lo síncrono y **AsyncAPI 2.6 o superior** para lo asíncrono, bajo enfoque `contract-first` | — | autogestionado | la especificación versionada es la fuente; stubs, validadores y pruebas se generan o verifican contra ella. El código no redefine unilateralmente el contrato |
| **Aplicación de terreno** | `CH-APP`: cuatro perfiles con operación sin conexión | aplicación instalable multiplataforma sobre **React Native**, o equivalente que comparta código entre Android e iOS con acceso nativo a periféricos | **Flutter**, o desarrollo nativo si el fabricante del equipo robusto solo certifica su cadena | autogestionado; se instala en el equipo `T11-C2-15` | versión mayor con soporte del proyecto; **no es una web responsiva empaquetada** (regla negativa 1) y es **una sola aplicación con cuatro perfiles**, no cuatro aplicaciones (regla negativa 2) |
| **Almacenamiento del terreno** | offline cifrado de `CH-APP` y de `CH-CAB` | base embebida cifrada en el dispositivo —**SQLite con cifrado**— con cola de sincronización y resolución determinista por marca de tiempo del equipo | — | autogestionado | el umbral es **8 h de sombra de radio en patio** sin pérdida de registro (Maestro §4.6), distinto de las 72 h de `EDGE-RUN` |
| **Interfaz de cabina** | `CH-CAB`: pantallas de cabina y terreno | vista de solo indicación construida con la misma pila de `CH-APP`, en modo quiosco sobre la pantalla del equipo | — | autogestionado | objetivos táctiles ≥44×44 px, alto contraste bajo luz solar directa, uso con guantes; **sin confirmación rutinaria manual**: la telemetría es la fuente primaria |
| Borde público | CDN, WAF, anti-DDoS L3/L4/L7, TLS 1.3 | **Amazon CloudFront + AWS WAF + AWS Shield**, o equivalente superior del catálogo AWS | CDN/WAF de tercero especializado | **gestionado** — `RT-03.05`: reduce riesgo operacional con TI de 5 personas | servicio, sin versión propia |
| Gateway de servicios | identidad, cuotas, versionado, esquema y entrada local 72 h | **Kong Gateway o equivalente con despliegue híbrido**: plano/perfil central en nube y data plane/perfil local restringido en `PHY-OPS-01` | gateway gestionado del proveedor solo si permite exportar y ejecutar localmente las mismas políticas/contratos sin plano de control | gestionado en nube y autogestionado acotado en sala | misma familia y política compatible en ambos perfiles; el local no expone catálogo ni administración y se prueba aislado |
| Ejecución de servicios | contenedores orquestados | **Amazon EKS** en nube; Kubernetes ligero compatible en sala | contenedores gestionados sin orquestador | **gestionado** en nube; **autogestionado ligero** en la sala | rama Kubernetes soportada por AWS y por la distribución local |
| Runtime local | ruta operacional de 72 h | misma pila de contenedores + perfil local restringido de `GW-API`, sin dependencia del plano de control de nube | — | **autogestionado**, por regla negativa 8 del Maestro | inventario canónico A1 §2.2; no agrega una segunda plataforma completa |
| Datos transaccionales | `DATA-CORE` | **Amazon RDS for PostgreSQL Multi-AZ**; PostgreSQL local | motor equivalente con réplica síncrona | **gestionado** en nube; instancia local en la sala | versión mayor soportada por AWS y por la distribución local |
| Series temporales | `DATA-TS` telemetría reefer y equipos | extensión de series sobre PostgreSQL, o motor de series dedicado | — | gestionado | ídem |
| Objetos y documentos | `DATA-DOC`, imágenes OCR y actas | **Amazon S3 con Versioning, Lifecycle y Object Lock** | — | **gestionado** — el modo inmutable sostiene `RT-07.11` | servicio |
| Bus de eventos | `INT-HUB`, colas durables y DLQ | **Amazon EventBridge + Amazon SQS FIFO/DLQ** | Kafka o RabbitMQ autogestionado | **gestionado** | servicio |
| Analítica | `DATA-AN`, KPI y concedente | **Amazon Athena + AWS Glue** sobre el lago de objetos | almacén analítico dedicado si el rendimiento lo exige | gestionado | servicio |
| Identidad | `SRV-IAM`, OIDC/OAuth 2.1 o SAML 2.0, MFA, PAM | plataforma de identidad gestionada | identidad autogestionada | gestionado; **detalle de D1** | ídem |
| Observabilidad | métricas, logs y trazas, nube y on-premise | **Amazon CloudWatch + AWS Distro for OpenTelemetry + Amazon OpenSearch Service** | plataforma SIEM compatible OpenTelemetry | gestionado, con recolector local | servicio y especificación OTel vigente |
| Infraestructura como código | `RT-03.03` | Terraform u OpenTofu, versionado **en el repositorio del CLIENTE** | — | autogestionado | rama con soporte vigente |
| Sistema operativo de servidores | núcleo local y edge | distribución Linux empresarial con soporte extendido | — | autogestionado, endurecido **CIS** por `RT-03.15` | release con soporte del fabricante durante todo el Contrato |

**Qué de esta tabla genera fila de T-11 y qué no.** La distinción importa porque el Subdocumento 4 pide declarar las **tecnologías** en 4.2.3 y los **implementos** en 4.2.4, y solo los segundos se ofertan. Un marco de código abierto incorporado al desarrollo —React, Spring Boot, React Native, SQLite, OpenAPI— **no genera fila por sí solo**: es parte del servicio de construcción, no un bien ni un servicio que se compre aparte. Sí genera fila el **soporte comercial** de una distribución, la **plataforma gestionada** que ejecuta o aloja, la **licencia** de un producto propietario y el **servicio** contratado a un tercero. Por eso las seis filas de aplicación no aparecen en el T-11 y sí aparecen `T11-C2-17` —los servicios de nube que las ejecutan—, `T11-C2-20` —el licenciamiento y soporte del sistema operativo— y `T11-C3-04` —la plataforma de ingeniería—. Si en la selección final alguna de estas líneas se resuelve con un producto comercial, la fila se abre entonces, con su justificación.

**Por qué esta selección y no otra.** El criterio no es preferencia técnica: es la restricción no negociable 11 y el área de TI de **cinco personas**. Se elige, en cada línea, **la alternativa más simple que cumpla continuidad, seguridad, portabilidad y operación con esa dotación**. Tres consecuencias concretas. La primera: el backend corre en contenedor y **la misma imagen se ejecuta en la nube y en la sala técnica**, que es lo único que hace posible la regla negativa 8 —si el runtime dependiera de un servicio gestionado propietario, las cinco funciones críticas no sobrevivirían las 72 h—. La segunda: la aplicación de terreno es **instalable y multiplataforma, no una web empaquetada**, porque las reglas negativas 1 y 2 lo exigen y porque el offline de 8 h con periféricos —lector óptico, NFC, GPS, báscula (`CP, Cap. 15, RT-17.06`)— no se resuelve desde un navegador. La tercera: **se nombran productos de referencia y no versiones congeladas**, conforme al criterio de vigencia declarado arriba; el contrato dura 56 meses y fijar hoy una versión exacta garantiza quedar fuera de soporte antes de terminarlo.

**Lo que aquí no se decide.** AWS y las regiones ya quedaron fijados por `ADR-011`; siguen abiertos el producto de identidad —`ADR-008`— y la distribución concreta de Linux. No se abre un ADR para el stack de aplicación: la elección tiene alternativas reales, pero **ninguna de ellas cambia la arquitectura** —las opciones de backend corren en el mismo contenedor sobre los mismos nodos, y las de aplicación de terreno satisfacen el mismo offline de 8 h—, de modo que registrarla como decisión de arquitectura inflaría el registro sin aportar trazabilidad.

**Reversibilidad y bloqueo por proveedor** (`RT-03.07`, obligatorio). Portables sin reescritura: los servicios propios, empaquetados en contenedores; el motor transaccional y el de series, por ser estándar; la infraestructura como código, con reescritura del proveedor pero no del diseño. No portables sin esfuerzo declarado: el borde público gestionado, el broker gestionado y el almacén analítico, cuya sustitución exige reimplementar integraciones. La mitigación es que **ninguna de las cinco funciones críticas depende de un servicio gestionado propietario**: el núcleo local corre la misma pila de contenedores sin plano de control de nube, que es lo que hace posible la regla negativa 8 del Maestro.

### 4. Proveedor y región de nube — `ADR-011` propuesto

`RT-03.01` exige declarar el proveedor y las regiones primaria y secundaria, con presencia en Chile o Sudamérica. `RT-15.04` exige declarar la **intensidad de carbono de la región escogida**, y `RT-15.05` valora escoger la de menor intensidad cuando latencia y regulación lo permitan, con análisis comparativo.

Es una decisión de arquitectura con alternativas reales, consecuencias y criterios. En MA-5 se seleccionó **AWS**, con **São Paulo `sa-east-1`** como región primaria desplegada en al menos dos zonas de disponibilidad y **Norte de Virginia `us-east-1`** como región secundaria activo-pasivo. `ADR-011` pasa a `PROPUESTO`: la ubicación ya no está indefinida, pero la aprobación requiere medir latencia desde el terminal, acreditar residencia/tratamiento, verificar catálogo y certificaciones al congelar la oferta, y registrar la métrica regional de carbono.

#### 4.1 Las alternativas concretas de `ADR-011`

La auditoría de cierre de D2 (`B7.2 #8`) observó que `ADR-011` no comparaba alternativas concretas. MA-4 acotó el espacio de decisión y MA-5 seleccionó AWS y las dos regiones. Las tablas siguientes se conservan porque demuestran que la decisión no nació de nombrar una marca sin criterio.

La decisión tiene dos ejes que se resuelven juntos.

**Eje 1 — región primaria.**

| Alternativa | Qué implica | Consecuencia que decide |
|---|---|---|
| `A1-CL` región del proveedor **en Chile** | latencia mínima al terminal y residencia nacional del dato | única que satisface sin discusión la residencia frente a la condición de operador de importancia vital; el número de zonas de disponibilidad efectivas debe verificarse, porque `RT-03.02` exige multi-AZ y una región nueva puede no tenerlas todas |
| `A2-SA` región **en Sudamérica** fuera de Chile | catálogo de servicios gestionados normalmente más completo y maduro | agrega latencia y abre la pregunta de residencia; exige justificación regulatoria explícita, no basta la conveniencia técnica |
| `A3-MIX` región en Chile para datos operacionales y regional para servicios que no los tocan | recoge lo mejor de las dos | **aumenta la superficie y la complejidad de red**, y multiplica los conductos que D1 debe controlar; solo se justifica si `A1-CL` no ofrece un servicio indispensable de la pila del numeral 3 |

**Eje 2 — región secundaria (BTT, Cap. 7).**

| Alternativa | Qué implica | Consecuencia que decide |
|---|---|---|
| `B1-MISMO` segunda región del **mismo** proveedor | conmutación más simple, réplica nativa, un solo contrato y un solo modelo de operación | **no elimina el dominio de fallo común**: proveedor, plano de control e identidad son los mismos. Es exactamente `SPOF-22` de D2 y la amenaza `THR-073` |
| `B2-OTRO` segunda región de **otro** proveedor | rompe el dominio común de fallo | exige portabilidad real por componente (`RT-03.07`), duplica la ingeniería de operación y choca con un área TI de cinco personas (restricción no negociable 11) |
| `B3-HIBRIDO` respaldo inmutable custodiado fuera del proveedor primario, con producción en una sola nube | mitiga el fallo común **en el dato**, no en el cómputo | es la única de las tres que se sostiene hoy con la dotación declarada; deja el RTO de un fallo de proveedor sin cubrir y eso hay que declararlo |

**Selección y condición de revisión.** Se adopta `A2-SA + B1-MISMO`: `sa-east-1` satisface la presencia sudamericana y ofrece una región operativa para la baseline; `us-east-1` aporta separación geográfica y catálogo maduro para DR. Producción se distribuye en al menos dos AZ y el secundario opera activo-pasivo con réplica caliente de datos y capacidad de cómputo reducida. El riesgo de dominio común `SPOF-22` no desaparece: se complementa con copia inmutable y autoridad de borrado separada. La región AWS anunciada para Chile se revisará después de su disponibilidad general; solo reemplazará la primaria si acredita multi-AZ, catálogo, latencia, residencia y carbono sin degradar el diseño. `F2-ESC-009` queda cerrado como selección y se transforma en condición de verificación de aceptación.

**`SPOF-13` y `SPOF-22` no se consolidan.** D2 lo pide expresamente en `B7-O01` y este frente lo confirma, porque son dos cosas distintas: `SPOF-13` es la **recuperabilidad del respaldo** —que exista, que sea inmutable y que la autoridad que puede borrarlo esté separada, tratado en §6.1 con `RT-07.10`, `.11` y `.12`—; `SPOF-22` es el **dominio de fallo común del proveedor**, que ninguna política de respaldo resuelve por sí sola. Un solo control no cierra los dos, y en el T-11 tampoco se funden: `T11-C2-18` cubre la región secundaria y `T11-C2-12` la custodia de medios, y ambas siguen siendo necesarias. Consolidarlas habría ahorrado una fila y perdido un dominio de fallo.

### 5. Sala técnica principal

Se especifica contra los 34 requisitos. Las cantidades y la carga eléctrica se cierran en C4: aquí va la especificación, no el dimensionamiento.

| Materia | Especificación | Código |
|---|---|---|
| Uso y aislamiento | recinto de **uso exclusivo de la solución**, aislado de otras dependencias, con acceso independiente | `RT-06.01` |
| Blindaje | muros no estructurales con blindaje perimetral; se especifica material y resistencia | `RT-06.02` |
| Plano de distribución | plano interno con zonas separadas de generadores, baterías, climatización, servidores, comunicaciones, trabajo y respaldo | `RT-06.03` |
| Piso técnico y cableado | piso técnico, canalización, cableado estructurado y etiquetado conforme a norma, **con certificación documentada de cada enlace** | `RT-06.04` |
| Racks | **racks de servidores independientes de los de comunicaciones**; se declara ocupación proyectada y margen de crecimiento por rack | `RT-06.05` |
| Obra civil | de cargo del CLIENTE; **especificación técnica y coordinación de cargo nuestro** | `RT-06.06`, coherente con `CP, Cap. 11` |
| UPS | autonomía **mínima de 30 minutos a plena carga** — la sala actual tiene 25 | `RT-06.07` |
| Generación | **≥24 horas continuas**, con estanque dimensionado y **contrato de reabastecimiento declarado** | `RT-06.08` |
| Instalación eléctrica | independiente de la del resto del edificio; normativa chilena vigente, incluida **NCh Elec. 2777** de puesta a tierra | `RT-06.09` |
| Mantenimiento eléctrico | revisión y medición **semestral** con informe al CLIENTE | `RT-06.10` |
| Declaraciones de energía | **carga proyectada en kW, factor de potencia y PUE estimada** | `RT-06.11`, `RT-15.04` |
| Redundancia eléctrica | 2N o N+1 con doble acometida y transferencia automática *(deseable, se ofrece)* | `RT-06.12` |
| Climatización | **de precisión, continua, redundante N+1**, con control de temperatura y humedad en el rango del fabricante del equipamiento | `RT-06.13` |
| Monitoreo ambiental | temperatura, humedad y **presencia de agua** en línea, integrados a la plataforma de observabilidad | `RT-06.14` |
| Contención | estrategia de pasillo frío o caliente y su efecto en eficiencia *(deseable)* | `RT-06.15` |
| Detección de incendio | **detección temprana por aspiración con tecnología láser**, tipo AnaLASER o equivalente de prestaciones iguales o superiores | `RT-06.16` |
| Extinción | **automática por agente limpio** tipo FM-200 o equivalente, con **aprobación UL** e instalación conforme a **NFPA** | `RT-06.17` |
| Extintores | sistema secundario de extintores portátiles con mantención y certificación vigentes | `RT-06.18` |
| Integración | detección y extinción integradas al monitoreo en línea, con notificación al NOC y a la contraparte del CLIENTE | `RT-06.19` |
| Control de acceso | **biométrico, principalmente facial, con AFIS de respaldo** — ver la tensión declarada en §11 | `RT-06.20` |
| Bitácora | todo ingreso y egreso con persona, fecha, hora y motivo, por el período de retención declarado | `RT-06.21` |
| Enrolamiento | espacio de atención entre el acceso principal y el término del pasillo; **se ofrece estación de enrolamiento fuera del recinto técnico**, que el BTT evalúa mejor | `RT-06.22` |
| Esclusa | acceso que impida el paso de más de una persona a la vez, con nueva verificación de identidad | `RT-06.23` |
| Videovigilancia | monitoreo IP con **≥30 días en línea** y respaldo posterior en medio secundario recuperable y auditable — ver §11 | `RT-06.24` |
| Terceros | procedimiento de acceso de fabricantes, mantenedores y auditores, **con acompañamiento obligatorio y registro** | `RT-06.25` |

**Referencias de producto para la sala.** UPS en línea de doble conversión con baterías dimensionadas a 30 min a plena carga, familia Eaton 93PS, Schneider Galaxy o Vertiv Liebert; climatización de precisión en fila o de sala, familia Vertiv Liebert o Stulz, en N+1; detección por aspiración de la familia AnaLASER o VESDA; extinción por agente limpio FM-200 o alternativa de menor potencial de calentamiento global, con listado UL. En todos los casos rige la regla del numeral 3: **la especificación manda, el nombre es referencia**. Capacidades, cantidades y potencias se fijan en C4 a partir de la carga real; declararlas aquí sería inventar el dimensionamiento.

#### 5.1 Custodia de medios de respaldo

| Materia | Especificación | Código |
|---|---|---|
| Servicio | custodia de medios del sitio primario en **medio físico transportable** a otro lugar cuando el CLIENTE lo determine | `RT-06.26` |
| Recinto | condiciones controladas de luminosidad, humedad y ventilación, y todo factor que afecte calidad y disponibilidad de los medios | `RT-06.27` |
| Gestión | **inventario con rotación, verificación periódica de legibilidad** y registro de toda entrada y salida | `RT-06.28` |

Es la pata física del «una copia fuera de sitio» del esquema 3-2-1-1-0 de `RNF-DIS-14`, y genera fila propia de T-11. El recinto de custodia **no puede estar en la misma sala** cuyo respaldo custodia, ni compartir su amenaza: aplica el mismo razonamiento de `RT-07.02` sobre amenazas comunes.

#### 5.2 Espacio de operación del personal

| Materia | Especificación | Código |
|---|---|---|
| Habilitación | estaciones de trabajo, telefonía, conexión a Internet y todo elemento para operar en condiciones adecuadas | `RT-06.29` |
| Separación | **separado de la sala de equipos**; las labores habituales de operación no requieren ingresar al recinto técnico | `RT-06.30` |
| Reutilización | instalaciones sanitarias, zonas de seguridad ante emergencia y áreas exteriores existentes **se usan y no se reimplementan**; se declara cuáles | `RT-06.31` |

La cantidad de puestos la fija C4 y no se decide aquí. Dos datos la condicionan y conviene dejarlos escritos: el área TI del CLIENTE **son cinco personas** (restricción no negociable 11), y la operación es 24x7x365 en tres turnos (restricción 2), de modo que el dimensionamiento no es «cinco puestos» sino el que resulte del modelo de operación, que es de C3.

#### 5.3 Rutas de comunicaciones

| Materia | Especificación | Código |
|---|---|---|
| Diversidad física | acceso a las redes por **rutas físicas distintas, con ingreso al edificio por puntos separados** | `RT-06.32` |
| Provisión | toda la conectividad, seguridad y canalizaciones, cañerías o ductos requeridos para cumplir los niveles comprometidos | `RT-06.33` |

Es el requisito que puede decidir `ADR-005` antes que cualquier criterio de costo, y el dato de si el edificio administrativo lo admite **no está en el caso**: sigue abierto como `F2-ESC-008`. Se conecta con `RT-03.17`, que exige que el enlace hacia la nube sea redundante por caminos y proveedores distintos: hoy el terminal tiene un solo proveedor de fibra y un radioenlace sin prueba de conmutación desde 2022 (`CP, Cap. 6`).


### 6. Site secundario y recuperación ante desastres

Este bloque cubre el Capítulo 7 completo del BTT, ausente de Célula 3 hasta la corrección `F2-COR-002`. Es el elemento evaluado `T21-4.2-E` y el entregable N° 9 del checklist del Capítulo C.

**Dónde está el secundario y por qué.** En la región secundaria del proveedor de nube. `CP, Cap. 3` establece que *«toda la operación ocurre en un solo emplazamiento»*: no existe un segundo recinto del CLIENTE. Y `RT-07.02` exige declarar la distancia al principal **y el análisis de amenazas comunes**. Un secundario dentro del terminal compartiría con el principal la marejada y el evento de mar, la atmósfera salina, el corte del acceso vial, el corte de la acometida eléctrica del recinto y el evento de protección portuaria que active el plan ISPS. Un segundo rack en el mismo edificio no es un sitio secundario: es una redundancia interna, y como tal ya está resuelta por `RT-03.14` y `RT-08.03`/`RT-08.04`.

| Materia | Especificación | Código |
|---|---|---|
| Modalidad | **activo-pasivo con réplica caliente**, justificada frente a costo, RTO comprometido y complejidad operacional | `RT-07.01` |
| Justificación de la modalidad | activo-activo obliga a resolver escritura concurrente entre regiones y a operar dos planos simultáneos. Con RTO de 4 h, un área TI de 5 personas y la exigencia de `RT-07.05` de que **el CLIENTE pueda ejecutar la conmutación**, activo-activo agrega complejidad que nadie del CLIENTE podría operar en una contingencia | `RT-07.01`, restricción 11 |
| Emplazamiento y amenazas | región secundaria del proveedor; se declara la distancia efectiva y el análisis de amenazas comunes con el terminal | `RT-07.02` |
| Replicación | continua, **con medición y alertamiento del retraso de replicación** | `RT-07.03` |
| Objetivos | **RTO ≤4 h y RPO ≤15 min** para servicios críticos | `RT-07.04`, `RNF-DIS-13` |
| Conmutación | documentada, automatizada en la mayor medida posible y **ejecutable por el personal del CLIENTE** tras la transferencia de conocimiento | `RT-07.05` |
| Retorno | procedimiento de retorno al principal, documentado y probado, **con reconciliación de los datos generados durante la contingencia** | `RT-07.06` |
| Prueba | **al menos dos veces al año mediante conmutación real**, con informe, medición del RTO y RPO efectivamente alcanzados y plan de corrección | `RT-07.07`, `RNF-DIS-15` |
| Conmutación automática | ante detección de indisponibilidad, con criterio de disparo declarado y protección contra conmutación innecesaria *(deseable, se ofrece)* | `RT-07.08` |

**Una advertencia sobre la ventana de prueba.** `RT-07.07` exige conmutación real dos veces al año, y las restricciones 9 y 10 del caso prohíben intervenir entre el 15 de diciembre y el 30 de abril, y durante una nave o las cuatro horas previas. Quedan siete meses hábiles al año para dos pruebas, y ambas deben caber entre naves. El calendario concreto es de C3; aquí se deja constancia de que la exigencia y la restricción conviven y no se resuelven solas.

#### 6.1 Respaldos

| Materia | Especificación | Código |
|---|---|---|
| Esquema | **3-2-1-1-0**: tres copias, dos medios distintos, una fuera de sitio, una inmutable o fuera de línea, cero errores de verificación de restauración | `RT-07.09`, `RNF-DIS-14` |
| Cifrado | respaldos cifrados en reposo y en tránsito, **con clave gestionada de forma independiente de la infraestructura respaldada** | `RT-07.10` |
| Inmutabilidad | copias inmutables protegidas contra borrado y modificación durante su retención, **incluso frente a credenciales administrativas comprometidas** | `RT-07.11` |
| *(respuesta a `ADR-007`)* | D2 §B5 fija como consecuencia negativa que `ADR-007` no puede omitir: *«respaldo alcanzable por la misma autoridad que puede borrarlo; restauración no probada»*. Las dos quedan cubiertas: `RT-07.11` separa la autoridad de borrado, `RT-07.10` gestiona la clave **de forma independiente de la infraestructura respaldada**, y `RT-07.12` exige prueba de restauración mensual con tiempo medido. Anclajes de D2: `SPOF-13` y `SPOF-12`; amenazas `THR-046` y `THR-049` | `RT-07.10`, `.11`, `.12` |
| Restauración | prueba **mensual** documentada sobre muestra representativa, con medición del tiempo efectivo | `RT-07.12` |
| Declaración por dominio | por **cada dominio de dato**: frecuencia de respaldo, período de retención y tiempo estimado de restauración completa | `RT-07.13` |
| Granularidad | restauración de un registro, una tabla, un módulo o el sistema completo *(deseable, se ofrece)* | `RT-07.14` |

`RT-07.13` se cruza con las siete retenciones del Maestro §16.1 — movimientos 10 años, temperatura reefer 5, evidencia facturable 6, VGM 5, imágenes OCR 12 meses, accesos 5 años, telemetría 2 años en línea — y con los 12 meses en línea más 24 en archivo de los registros de seguridad. La tabla resultante, con el tiempo de restauración por dominio, se completa en C4 porque depende del volumen.

#### 6.2 Niveles de servicio de infraestructura

El numeral 7.2 del BTT los fija **por componente**, no como una cifra única:

| Componente | Disponibilidad mensual mínima |
|---|---|
| Energía del recinto · climatización · red y comunicaciones · servidores y cómputo · motor de base de datos · portal y canales | **99,95 %** cada uno |
| **Transacción de negocio crítica de extremo a extremo** | **99,9 %** — Art. 78° de las BA |

El propio BTT advierte que *«los niveles de disponibilidad de infraestructura son un medio, no un fin. El compromiso contractual que se mide y se penaliza es el del Artículo 78°»*. La consecuencia de diseño es que la cadena completa —seis componentes al 99,95 % en serie— tiene que producir 99,9 % extremo a extremo, y eso solo se sostiene con redundancia dentro de cada eslabón, no sumando eslabones fiables. El cálculo de la cadena es de C4.

### 7. Hardware de cómputo, almacenamiento y red

| Materia | Especificación | Código |
|---|---|---|
| Cómputo | marca, **modelo de referencia**, procesador, memoria, almacenamiento local, interfaces y consumo, **con el cálculo de dimensionamiento que lo sustenta** | `RT-08.01` |
| Almacenamiento | redundante, con **tolerancia declarada a la falla de discos**, control de errores y **monitoreo predictivo de salud de los medios** | `RT-08.02`, `RT-03.14` |
| Red | conmutadores de núcleo, cortafuegos y balanceadores **en alta disponibilidad, sin punto único de falla** | `RT-08.03` |
| Energía del equipo | **fuentes redundantes y conexión a circuitos eléctricos distintos** | `RT-08.04` |
| Crecimiento | margen declarado **como porcentaje sobre la carga proyectada del caso**, y procedimiento de ampliación | `RT-08.05` |
| Condición | **equipamiento nuevo, sin uso previo**, con garantía de fábrica vigente desde la recepción conforme | `RT-08.06` |

**Referencias y línea base dimensional.** C4 §6.2.bis fija tres servidores 1U de 16 núcleos/128 GB/2×10 GbE y 350 W de diseño por nodo; almacenamiento de referencia 4×480 GB SSD en `RAID 10` —1,92 TB brutos/≈960 GB útiles—; dos racks 42U; pares HA de conmutación y cortafuegos. Las familias comerciales de referencia siguen siendo Dell PowerEdge R/HPE ProLiant DL/Lenovo ThinkSystem SR, Cisco Catalyst/Aruba CX/Juniper EX y Palo Alto PA/Fortinet FortiGate o equivalentes. El modelo final debe satisfacer esos mínimos; `ADR-007` formaliza RAID/almacenamiento. C4 también fija UPS, generación, combustible, climatización, CCTV, carga TI y PUE de referencia.

#### 7.1 Puestos de trabajo

| Materia | Especificación | Código |
|---|---|---|
| Estaciones | las que determine el dimensionamiento del caso, **con monitores duales** | `RT-08.07` |
| Ergonomía y energía | condiciones ergonómicas de **NCh 2527** y certificación de eficiencia energética | `RT-08.08` |
| Gestión | gestión centralizada, **cifrado de disco**, control de dispositivos extraíbles, antivirus con detección y respuesta y actualización automatizada | `RT-08.09` |

### 8. Equipamiento de terreno y protección marina

El Art. 14.2 de las BA establece que **la especificación técnica del hardware de terreno es nuestra aunque la compra sea del CLIENTE**. La restricción no negociable 12 del caso lo refuerza: *«todo equipamiento a instalar en zona operativa debe acreditar grado de protección y comportamiento en atmósfera marina, y su plan de reposición debe estar costeado»*.

| Materia | Especificación | Código |
|---|---|---|
| Especificación | por dispositivo: marca, modelo de referencia, cantidad, características mínimas, accesorios y consumibles | `RT-08.10` |
| Condiciones reales | intemperie, humedad, polvo, vibración, temperatura, **uso con guantes**, luminosidad y **autonomía de batería requerida por turno** | `RT-08.11`, `CP, Cap. 6` |
| Protección | grado declarado contra polvo y agua y **resistencia a caídas**, coherentes con el entorno | `RT-08.12` |
| Ciclo de vida | ciclo esperado, disponibilidad de repuestos y **plan de reposición durante los 56 meses del Contrato** | `RT-08.13` |
| Gestión de flota | integración a la gestión centralizada de `RT-03.18`: inventario, configuración, firmware, bloqueo y **borrado remoto** | `RT-08.14` |
| Aceptación previa | **una unidad de cada tipo para pruebas de aceptación del CLIENTE antes de la compra masiva** *(deseable, se ofrece)* | `RT-08.15` |
| Plan de ciclo de vida | recepción, puesta en servicio, mantención, actualización, retiro y disposición final | `RT-08.16` |
| Borrado seguro | todo medio que salga de servicio, borrado verificable con **certificado de destrucción o sanitización al CLIENTE** | `RT-08.17` |
| Disposición final | con **gestor autorizado** conforme a normativa de residuos, con certificado | `RT-08.18` |
| Reacondicionamiento | estrategia de extensión de vida útil cuantificada *(deseable)* | `RT-08.19` |

#### 8.1 Tabla de protección marina por clase

Cinco clases, definidas por dónde va el equipo y a qué está expuesto. Los grados se expresan como **mínimo exigible**; el modelo concreto se cierra con C4 y con el site survey.

| Clase y ubicación | Riesgos dominantes | Protección mínima | Material y anticorrosión | Temperatura y humedad | Energía | Vida útil y reposición | Prueba de recepción | Cantidad |
|---|---|---|---|---|---|---|---|---|
| **Gabinete de gate** — 14 puestos al aire libre | salinidad, lluvia, polvo, vibración de camión, sol directo | **IP66** | acero inoxidable 316L o poliéster reforzado; herrajes inoxidables; sin aluminio desnudo | rango exterior con control térmico pasivo o activo según carga | UPS local que sostenga la validación ante corte, por restricción 4 | reposición programada por corrosión, no por falla | ensayo de estanqueidad y verificación de tratamiento al recibir | C4 |
| **Gabinete de patio** — puntos de red | salinidad, intemperie, impacto de equipos, sombra móvil | **IP66**, montaje protegido de golpes | ídem | ídem | ídem | ídem | ídem | C4, sujeta a site survey |
| **Gabinete de patio refrigerado** — 26 tableros | salinidad, humedad permanente, proximidad a tablero energizado | **IP66**, separación eléctrica del tablero | ídem, con atención a corrosión galvánica en la interfaz con el tablero | ídem | autonomía que sostenga la alarma durante el corte | ídem | ídem, más verificación de no interferencia con el tablero | 26 + crecimiento a 32 |
| **Gabinete de muelle** — 3 sitios | salinidad severa por proximidad al agua, viento, operación nocturna | **IP66 o superior** | 316L recomendado por exposición severa | ídem | ídem | reposición más frecuente por exposición | ídem | C4 |
| **Dispositivo móvil de terreno** — patio, gate, inspección, ronda de frío | caídas, guantes, lluvia, luminosidad exterior, turno completo | **IP65 o superior** y resistencia a caídas declarada | carcasa reforzada | rango exterior | **autonomía ≥ un turno completo**, con relevo sin detención | ciclo declarado y repuestos por 56 meses | prueba de aceptación con usuarios reales, por `RT-08.15` | C4 |

**Referencias.** Gabinetes de familias con línea marina o de acero inoxidable —Rittal, nVent HOFFMAN o equivalente—; dispositivos de mano y montados en vehículo de familias industriales robustas —Zebra, Honeywell, Getac o Panasonic Toughbook—. Rige la regla del numeral 3.

Dos advertencias honestas. Primera: `CP, Cap. 6` dice que hoy *«los gabinetes del patio y del gate se reemplazan antes de lo previsto»*, de modo que la vida útil real en este emplazamiento es **menor que la de catálogo del fabricante**; el plan de reposición se construye sobre la experiencia del CLIENTE, no sobre la ficha técnica, y ese dato hay que pedírselo. Segunda: la regla negativa 11 del Maestro advierte que mover la sala no elimina el ambiente marino, y lo mismo vale aquí — ningún grado IP evita la corrosión, solo la retrasa.

### 8.bis Componentes de seguridad: producto y clasificación T-11

`SEC-PHYS-v0.1` de D1 consolida **31 controles en 17 grupos**, y clasifica cada grupo como fila propia candidata, agrupada, incluida o condicional. Esa clasificación es de D1 y se respeta; lo que aporta C2 es el **producto de referencia y la compatibilidad**, y lo que aporta C4 es la **cantidad**. La regla que impide el doble conteo es de D1, `F3-DEC-005`: una capacidad nativa o incluida se referencia desde la fila principal y no se compra dos veces.

| Grupo `SEC-PHYS` | Producto o servicio de referencia | Compatibilidad y vigencia | Clasificación T-11 |
|---|---|---|---|
| `SEC-EDGE-01/02` | Amazon CloudFront + AWS WAF + AWS Shield: CDN, anti-DDoS L3/L4/L7, TLS 1.3, HSTS y protección de bots | servicio AWS, sin versión propia; región/borde fijados por `ADR-011` | **fila propia** |
| `SEC-API-01` | Kong Gateway o equivalente híbrido: perfil central y perfil local restringido | misma política/contrato versionado en nube y sala; operación local 72 h sin plano de control nube | **incluida** en plataforma de gateway/runtime; una sola fila, sin duplicar el perfil local |
| `SEC-NET-01 / SEC-EXP-01` | cortafuegos y conmutación de núcleo ya especificados en §7 —familias Palo Alto PA, Fortinet FortiGate, Cisco Catalyst, Aruba CX, Juniper EX— más verificación externa de exposición | debe soportar segmentación por zona y conductos declarados; IEC 62443 | **incluida** en `T11-C2-03` y `T11-C2-04`; **no genera fila nueva** |
| `SEC-IAM-01 / SEC-ADM-01 / SEC-PROD-01` | plataforma de identidad gestionada con OIDC/OAuth 2.1 o SAML 2.0, MFA y PAM con grabación de sesión | **requisito excluyente:** capacidad local de autenticación/autorización y bloqueo durante 72 h. `ADR-008` está `PROPUESTO CONDICIONADO`, no aprobado | **fila propia** IAM y PAM; lectores o credenciales solo con cantidad justificada por C4 |
| `SEC-SYNC-01` | canal del broker de integración ya ofertado | cifrado, identidad de servicio, protección contra repetición | **incluida** en integración y red; sin fila |
| `SEC-DATA-01 / SEC-ENC-01 / SEC-FIELD-01` | capacidades nativas de cifrado del motor transaccional, del almacén de objetos y del de series | cifrado de campo sobre los datos que `RT-11.10` y el `CP, Cap. 15` identifican como sensibles | **incluida**; fila separada solo si se oferta un servicio de cifrado de campo aparte |
| `SEC-KEY-01 / SEC-SECRET-01` | KMS o HSM gestionado más gestor de secretos con rotación | **requisito excluyente que C2 confirma:** si la clave vive solo en nube, el núcleo local no puede descifrar durante el corte. Exige material de clave protegido en el sitio, con raíz no exportable | **fila propia**; se consolidan KMS, HSM y bóveda sin duplicar funciones incluidas |
| `SEC-BKP-01` | plataforma de respaldo de C2 §6.1, con inmutabilidad y clave gestionada aparte | 3-2-1-1-0; la copia fuera de sitio se materializa en `PHY-OPS-05` | **condición** de la fila de respaldo y de la custodia de medios; **no es una segunda compra** |
| `SEC-LOG-01 / SEC-SIEM-01` | plataforma SIEM y de registro compatible **OpenTelemetry**, con colector y buffer local | `RT-03.16`: una sola plataforma para nube y on-premise, sin puntos ciegos. Retención 12 meses en línea + 24 en archivo | **fila propia**; C4 dimensiona ingesta, retención y licencias |
| `SEC-END-01` | EDR con agentes y consola | **advertencia de compatibilidad:** los dispositivos de terreno de la tabla marina **no se presumen compatibles con agente**. Se cubren con controles compensatorios de red y de gestión de flota (`RT-03.18`), no forzando un agente que el fabricante no soporta | **fila propia** por cargas y puestos; los dispositivos de terreno **no** entran en el conteo de agentes |
| `SEC-SOC-01 / SEC-IR-01` | SOC gestionado 24×7 con gestión de casos | **no se asigna al área TI de cinco personas**; es servicio ofertado y costeado | **fila propia de servicio** |
| `SEC-VULN-01` | plataforma de escaneo continuo con gestión 7/15/30 | cubre nube, on-premise, aplicación y superficie externa | **fila propia o incluida** en el servicio de seguridad; C4 evita el doble conteo |
| `SEC-PENTEST-01` | servicio de tercero independiente, anual y antes de cada paso a producción | independencia acreditada | **fila propia de servicio** |
| `SEC-SDLC-01 / SEC-PIPE-01` | plataforma CI/CD con SAST, SCA, DAST, escaneo de secretos y de imágenes | ya ofertada en C3 §4; ingeniería separada de producción | **agrupada** por plataforma; **no una fila por regla de control** |
| `SEC-SUPPLY-01 / SEC-ART-01` | registro de artefactos con SBOM CycloneDX o SPDX, firma y procedencia SLSA | producción consume solo artefactos aprobados | **incluida** en CI/CD, con la inclusión declarada explícitamente |
| `SEC-NPDATA-01` | proceso de anonimización o generador de datos sintéticos | sostiene la prohibición de dato productivo en no producción de C3 §3 | **condicional**: fila solo si se oferta herramienta separada |
| `SEC-GOV-01 / SEC-CLOUD-01 / SEC-HARD-01 / SEC-SAMM-01` | matrices y procedimientos; línea base **CIS** por producto y versión | `SEC-HARD-01` aterriza aquí: cada producto del catálogo del §3 y del §7 lleva su línea base CIS correspondiente, o guía equivalente justificada cuando no exista *benchmark*; toda desviación registra necesidad, riesgo, compensación, aprobador, vencimiento y reprueba | **normalmente incluido**; fila solo si se oferta capacidad separada |

**Tres cosas que este cruce cambia en C2, y conviene que se vean.**

**El material de clave tiene que existir en el terminal.** Es la consecuencia física de `ADR-009` de D1 y de la regla negativa 8 del Maestro: una solución cuyo cifrado dependa exclusivamente de un KMS en nube no puede descifrar durante las 72 horas de corte, y las cinco funciones críticas leen y escriben datos cifrados. La especificación de `SEC-KEY-01` incorpora capacidad local protegida con raíz no exportable.

**El EDR no cubre los dispositivos de terreno, y decirlo es mejor que suponerlo.** Los equipos de las cinco clases marinas del §8.1 son de fabricantes industriales cuyo soporte de agentes no está confirmado, y la restricción del `CP, Cap. 11` prohíbe imponer software al fabricante en el caso de las grúas. Se cubren por segmentación de red y por la gestión centralizada de flota de `RT-03.18`, que sí es exigible. Contar una licencia de EDR por dispositivo de terreno habría inflado el T-11 con algo que no se puede instalar.

**El SOC es un servicio ofertado, no una tarea del CLIENTE.** La restricción no negociable 11 dice que *«toda función que requiera un especialista dedicado que la compañía no tiene debe ofrecerse como servicio y estar costeada»*. Monitoreo 24×7 con cinco personas de TI no es una opción; D1 lo marcó y C2 lo recoge como fila de servicio.

### 9. Candidatos de filas T-11

Sin precios, conforme al Art. 16 y a la regla del Maestro. Un componente lógico no genera fila; la genera un componente físico, plataforma, licencia o servicio efectivamente ofertado. Las cantidades las cierra C4.

| Candidato | Componente | Producto o servicio | Ubicación | Cantidad | Origen |
|---|---|---|---|---|---|
| `T11-C2-01` | servidores del núcleo operacional local | servidor de rack empresarial, clúster ≥3 nodos | sala técnica del terminal | C4 | `PHY-OPS-01` |
| `T11-C2-02` | almacenamiento local | arreglo redundante con RAID justificado | sala técnica | C4 | `PHY-OPS-02` |
| `T11-C2-03` | conmutación de núcleo | par de conmutadores en HA | sala técnica | C4 | `PHY-OPS-04` |
| `T11-C2-04` | cortafuegos y segmentación | par en HA | sala técnica | C4 | `PHY-OPS-04`, D1 |
| `T11-C2-05` | UPS | doble conversión, ≥30 min a plena carga | sala técnica | C4 | `RT-06.07` |
| `T11-C2-06` | generación autónoma | grupo electrógeno ≥24 h con estanque | recinto del CLIENTE | C4 | `RT-06.08` |
| `T11-C2-07` | climatización de precisión | N+1 | sala técnica | C4 | `RT-06.13` |
| `T11-C2-08` | detección temprana de incendio | aspiración láser tipo AnaLASER o equivalente | sala técnica | 1 sistema | `RT-06.16` |
| `T11-C2-09` | extinción por agente limpio | FM-200 o equivalente, listado UL | sala técnica | 1 sistema | `RT-06.17` |
| `T11-C2-10` | control de acceso biométrico y esclusa | facial con AFIS de respaldo | acceso a sala técnica | 1 conjunto | `RT-06.20`, `RT-06.23` |
| `T11-C2-11` | videovigilancia del recinto | CCTV IP con ≥30 días en línea | sala técnica | C4 | `RT-06.24` |
| `T11-C2-12` | custodia de medios de respaldo | servicio de custodia externa | fuera del recinto principal | 1 servicio | `RT-06.26` |
| `T11-C2-13` | estaciones de trabajo de operación | estación con monitores duales | espacio de operación | 3 de baseline; validación AHT en H2 | `RT-08.07`, C4 `DIM-18` |
| `T11-C2-14` | gabinetes de borde | IP66 con tratamiento marino, por clase | gate, patio, patio refrigerado, muelle | 59–61; site survey cierra patio | `RT-08.12`, `CP, Cap. 15, RT-06.01` |
| `T11-C2-15` | dispositivos móviles de terreno | equipo robusto IP65, uso con guantes | patio, gate, inspección, frío | 97: 88 operativos + 9 repuestos | `RT-08.11`, C4 §9 |
| `T11-C2-16` | concentradores de patio refrigerado | uno por tablero | 26 tableros | 26 → 32 | `PHY-EDG-03` |
| `T11-C2-17` | servicios de nube — cómputo, datos, objetos, bus, analítica | AWS EKS, RDS PostgreSQL, S3, EventBridge/SQS y Athena/Glue | São Paulo `sa-east-1`, multi-AZ | 1 plataforma elástica; C4 | Cap. 3, `ADR-011` |
| `T11-C2-18` | servicios de nube — región secundaria y DR | AWS réplica cross-region y cómputo reducido activo-pasivo | Norte de Virginia `us-east-1` | 1 sitio lógico regional | Cap. 7, `ADR-007/011` |
| `T11-C2-19` | observabilidad y SIEM | CloudWatch + AWS Distro for OpenTelemetry + OpenSearch/SIEM | AWS, con recolector local | 1 suscripción por ingesta/retención | `RT-03.16`, D1 |

> **Una sola plataforma, una sola fila.** `RT-03.16` exige que el monitoreo on-premise se integre a **la misma** plataforma que la nube, sin puntos ciegos. Por eso `T11-C2-19` y los grupos `SEC-LOG-01 / SEC-SIEM-01` de `SEC-PHYS-v0.1` **no son dos compras**: son la misma plataforma vista desde observabilidad y desde seguridad. C4 §9.bis lo resuelve sobre esta fila y §9.ter la dimensiona. D2 lo había marcado como posible doble conteo en `B6-F05`; queda cerrado por fusión, no por omisión.
| `T11-C2-20` | licenciamiento de sistema operativo y soporte | distribución empresarial con soporte | sala técnica y borde | C4 | `RT-03.15` |
| `T11-C2-21` | racks y distribución eléctrica A/B | rack 42U, PDU A/B, tierra y gestión de cables | sala técnica | 2 racks | `RT-06.03..05`, C4 §9 |

**Regla única de alcance T-11.** Los equipos de terreno que TERABYTE debe especificar (`T11-C2-14..16`) permanecen en la matriz técnica aunque su adquisición corresponda al CLIENTE; la columna Justificación lo declara y el Informe 1 no incluye precios. Si el formulario se interpreta como provisión exclusiva del adjudicatario, esas mismas filas pasan 1:1 a un anexo de “hardware especificado por TERABYTE y adquirido por el CLIENTE”, sin desaparecer ni duplicarse. Quedan fuera como provisión la obra civil de la sala, los sistemas conservados y las canalizaciones ejecutadas por el CLIENTE, todos con su referencia técnica.

### 10. Ciclo de vida y salida de servicio

`RT-08.13` fija el horizonte en los **56 meses del Contrato**. El plan cubre recepción y puesta en servicio con prueba de aceptación por tipo de dispositivo; mantención con revisión eléctrica semestral de la sala (`RT-06.10`); reposición programada del equipamiento de terreno según la vida útil real del emplazamiento y no la de catálogo; y salida de servicio con borrado verificable y **certificado de sanitización entregado al CLIENTE** (`RT-08.17`), más disposición final con gestor autorizado y certificado (`RT-08.18`).

### 11. Tensiones declaradas

**El BTT pide costo unitario y el Informe 1 no lleva precios.** `RT-08.10` exige especificar cada dispositivo de terreno *«con marca, modelo de referencia, cantidad, características mínimas, accesorios, consumibles y costo unitario estimado»*. El Formulario T-11 y el Maestro prohíben precios en el Informe 1. Se resuelve entregando **todo salvo el costo unitario**, y dejando la constancia: el dato existe y se aporta en la Oferta Económica, en el sobre que corresponde. No se omite el requisito, se ubica donde las BA lo admiten.

**Biometría en el recinto técnico frente a la objeción de la nombrada.** `RT-06.20` exige control de acceso biométrico facial con AFIS para entrar a la sala. La restricción no negociable 8 registra que la biometría obligatoria **fue objetada** por los acuerdos sindicales, y el Maestro §11.2 exige credencial temporal para eventuales *«sin biometría obligatoria»*. Son poblaciones y recintos distintos: unas pocas personas autorizadas entrando a un recinto técnico cerrado, frente a hasta 380 eventuales por turno accediendo al recinto portuario. La arquitectura las trata por separado y lo declara, en vez de dejar que el evaluador encuentre la palabra en los dos lados. Coordinación con D1: `F2-DEC-002`.

**CCTV del recinto frente al VMS conservado.** `RT-06.24` exige videovigilancia propia de la sala con 30 días en línea. La regla negativa 6 del Maestro prohíbe crear un portal de video y conserva el VMS de las 142 cámaras como interfaz de video del terminal; la regla 7 prohíbe llevar video por la red operacional. El CCTV del recinto técnico es un control de seguridad física de nuestra instalación, con su propio almacenamiento y su propia red, **y no se integra al VMS ni a su tráfico**. Coordinación con D1: `F2-DEC-003`.

### 12. Definición de terminado — estado

- [x] Todo producto materializa una caja física o un control obligatorio.
- [x] Versiones y soporte declarados mediante criterio de vigencia, no versión congelada.
- [x] Sala y equipos cumplen ambiente, energía, HA y mantenimiento, con los 34 requisitos recorridos.
- [x] Primario y secundario diferenciados, con responsabilidades separadas.
- [x] Cantidades vinculadas a C4; **no hay precios**.
- [x] Tipología declarada por sitio, conforme al numeral 6.1.
- [x] `TRZ_C2.md` disponible; su estado vigente se sanea en MA-3.
- [x] Línea base de cantidades, capacidades, kW, factor de potencia, PUE y RAID — C4 §6.2.bis/§9; modelos y pruebas permanecen condicionados.
- [x] Componentes y licencias de seguridad — §8.bis: los 17 grupos con producto, compatibilidad y clasificación T-11.
- [x] `ADR-011` proveedor y región — AWS, `sa-east-1` primaria y `us-east-1` secundaria; estado `PROPUESTO`, con verificaciones de aceptación declaradas.
- [ ] Plano de distribución interna del recinto (`RT-06.03`) y plano de racks — en el pase final de diagramas.

## Trazabilidad

Ver [`trazabilidad/TRZ_C2.md`](trazabilidad/TRZ_C2.md).
