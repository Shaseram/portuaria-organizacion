# C1 — Arquitectura física y emplazamiento

## Contrato del entregable

### Objetivo y destino

Ubicar cada componente desplegable en nube, on-premise o borde y justificarlo conforme al Artículo 16. Alimenta las secciones 4.2.1 y 4.2.2 del consolidado.

### Cumplimientos asignados

- `SD4-02`, `SD4-05`, `SD4-07`, `SD4-08`.
- T7-4.2, T7-4.5, T7-4.7 y T7-4.8.
- BTT Cap. 3 completo: `RT-03.01` a `RT-03.24`; Decisión 20; `MC-09/10/11`.
- Checklist del BTT, Cap. C, entregable N° 3: tabla de emplazamiento nube/on-premise justificada.

> *Corrección `F2-COR-001` (2026-09-05): el contrato declaraba `RT-03.01..15`. El Capítulo 3 del BTT llega a `RT-03.24` y los nueve omitidos son de este frente: `.17` enlace redundante por caminos y proveedores distintos con tiempo de conmutación declarado; `.18` gestión remota y centralizada de los dispositivos de borde, a la que `RT-08.14` remite; `.20` dimensionamiento del ancho de banda por sitio en normal y peak, con cálculo, que alimenta C4; `.21` enlace privado dedicado o VPN cifrada; `.22` acceso remoto de confianza cero con verificación de postura; `.23` red inalámbrica operacional con segmentación por tipo de dispositivo, autenticación por certificado y cobertura verificada mediante estudio de sitio; `.24` calidad de servicio y priorización del tráfico operacional. Ver `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`.*

### Entradas obligatorias

- Maestro §§3–6, 9–10, 15, 17–19.
- A1 catálogo lógico `v0.1` para refinar el mapeo.
- A3 funciones críticas y D1 paquete `SEC-PHYS-v0.1`.
- Condiciones físicas y volumetría de Célula 2.

### Trabajo requerido

- [ ] Dibujar límite de oferta y topología híbrida completa.
- [ ] Identificar nube primaria/secundaria y al menos dos zonas de disponibilidad.
- [ ] Identificar sala, edge de gate/patio/reefer/muelle y sistemas conservados.
- [ ] Mapear cada componente lógico desplegable a uno o más nodos.
- [ ] Justificar cada ubicación por seis criterios Art. 16.
- [ ] Mostrar zonas, redes, enlaces, redundancia y protocolos.
- [ ] Comparar sala actual, nueva/reconstruida y edge mínimo+nube.
- [ ] Declarar SPOF residuales y dependencia de terceros.
- [ ] Delimitar qué queda fuera de la oferta o sujeto a levantamiento.

### Tabla de emplazamiento obligatoria

| ID físico | Componente lógico | Función | Ubicación | Latencia | Continuidad | Volumen | Regulación/seguridad | Conectividad/acoplamiento | TCO cualitativo | Justificación final | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `PHY-001` | POR ASIGNAR | — | nube/on-prem/edge | — | — | — | — | — | — | — | PENDIENTE |

### Reglas del diagrama físico

- nombres de producto sí son permitidos, si están justificados;
- mostrar capacidades relevantes, redundancia, protocolos y fronteras;
- distinguir zona pública, privada, operacional, administrativa y protección;
- mostrar correspondencia con lógico mediante IDs;
- toda caja ofertada debe tener candidato T-11;
- no dibujar ubicación física inexistente ni ocultar dependencias.

### Productos obligatorios

1. Diagrama físico híbrido.
2. Tabla de emplazamiento Art. 16.
3. Matriz lógico→físico.
4. Comparación de alternativas de sala y candidato `ADR-005`.
5. Registro inicial de SPOF.

### Decisiones permitidas y escalamiento

Puede proponer topología y ubicación. Debe escalar contratos no confirmados, datos de sitio ausentes, cambios al plan de protección, infraestructura fuera del recinto no declarada o cualquier solución que reduzca las 72 h.

### Aporte T-11/ADR

Entrega a C4 el inventario de cajas físicas y su ubicación. Cada una se clasifica como fila T-11, parte interna de otra fila o elemento fuera de oferta, siempre con razón.

### Salidas hacia otros frentes

- Frente 1: restricciones físicas que cambien dependencia o flujo.
- Frente 3: nodos, zonas, exposición, administración y fronteras de confianza.

### Definición de terminado *(lista normativa del contrato — no es estado)*

> **Cómo leer estas casillas.** Son la **lista de exigencias** que el contrato de este entregable fija al empezar, y se conservan sin marcar a propósito: son el enunciado, no el avance. **El estado vigente y fechado está en la última sección de este documento**, «§10 Definición de terminado — estado». Si las dos se leen como estado, un mismo control aparece pendiente y cumplido a la vez, que es lo que observó `AGC3-019`.

- [ ] Todos los componentes desplegables tienen ubicación y justificación.
- [ ] La solución es realmente híbrida y multi-AZ.
- [ ] Se ven sala, borde, nube, DR, enlaces y sistemas conservados.
- [ ] Las 72 h no dependen de nube.
- [ ] No se presume que el ambiente marino desaparece.
- [ ] Físico, catálogo lógico y T-11 usan los mismos IDs.
- [ ] `TRZ_C1.md` completo.

## Contenido listo para integrar

**Versión:** `v0.5` — contenido completo, sujeto a revisión cruzada en la Puerta 2.
**Fecha:** 2026-09-05. **Destino:** consolidado 4.2.1 y 4.2.2.

### 1. Por qué esta arquitectura física no puede ser genérica

El Caso 06 impone tres hechos que, juntos, determinan la forma de la solución antes de elegir un solo producto.

**Toda la operación ocurre en un único emplazamiento.** El CP, Cap. 3 lo dice de entrada: *«aquí toda la operación ocurre en un solo emplazamiento»*. No existe un segundo recinto del CLIENTE donde alojar un sitio de respaldo. Esto decide, por sí solo, que el sitio secundario exigido por el BTT, Cap. 7 no puede ser un segundo rack del terminal: tiene que estar en la región secundaria de nube.

**La sala técnica está a menos de trescientos metros de la línea de costa.** El CP, Cap. 6 la describe: 34 m² habilitados en 2012, climatización tipo split, alimentación ininterrumpida de 25 minutos, acceso por llave, y una frase que el propio caso escribe: *«No cumple los estándares del Capítulo 6 de las Bases Técnicas Transversales»*. El `RT-07.02` del BTT exige declarar la distancia entre sitio principal y secundario **y el análisis de amenazas comunes**. Marejada, corte del acceso vial, atmósfera salina y evento ISPS son amenazas que un secundario dentro del recinto compartiría íntegramente con el principal.

**La operación de muelle y gate no puede detenerse porque se cayó un enlace hacia fuera.** Es el tercer punto de la Declaración Mandatoria del CP, Cap. 6, y el CP, Cap. 15 lo cuantifica en `RT-03.10`: 72 horas continuas de operación completa sin enlace exterior. El BTT pide un mínimo de 24 h *«o el mayor que fije el caso»*; el caso fija 72. Eso obliga a que las cinco funciones críticas —nave y movimientos, posición e inventario, gate, alarma de frío y hecho facturable— tengan cómputo y datos **en el terminal**, no en el borde entendido como pasarela.

De ahí la forma: **nube pública como plataforma principal, un núcleo operacional local capaz de sostener el terminal por sí solo durante tres días, y un borde instrumentado por zona del recinto.** No es una preferencia de estilo; es lo que queda cuando se respetan simultáneamente el Art. 16 de las BA, el `RT-03.10` del caso y la Declaración Mandatoria.

### 2. Límite de la oferta

| Dentro del límite TERABYTE | Fuera del límite, conservado e integrado | Fuera del límite, ejecuta el CLIENTE |
|---|---|---|
| plataforma en nube, núcleo operacional local, borde de gate/patio/frío/muelle, red operacional nueva, gabinetes y dispositivos de terreno, custodia de medios | ERP y emisión tributaria, control de grúas de muelle (solo lectura), control de acceso y barreras, CCTV/VMS del terminal, básculas, TOS 2012 durante la coexistencia | obra civil de la sala, canalizaciones exteriores, alimentación eléctrica del recinto, acceso vial |

La distinción importa por el CP, Cap. 11: no se construye infraestructura civil, **pero sí se especifica técnicamente para que el CLIENTE la ejecute**. Toda obra que aparezca en este entregable se entrega como especificación, no como partida ofertada.

### 3. Diagramas físicos

> **Pendiente por decisión de equipo.** Los diagramas del Subdocumento 4 se producen al final, en un solo pase y con notación común a los tres frentes, para que las cinco vistas de `RT-02.03` sean coherentes entre sí. Este entregable deja el material que el diagrama debe representar: los 21 nodos `PHY-*` de §4, la matriz lógico→físico de §5, las zonas y fronteras del §2 y los puntos únicos de falla de §8.

Cuando se dibuje, la vista física de C1 debe mostrar, conforme a las reglas de este contrato: el límite de la oferta; zona pública, subred privada de aplicación, subred privada de datos, zona operacional, zona administrativa y zona de protección; región primaria y secundaria; sala técnica, borde por zona del recinto y sistemas conservados; el enlace redundante y su comportamiento ante corte; y la correspondencia con el catálogo lógico por ID.

### 4. Tabla de emplazamiento conforme al Artículo 16

El Art. 16.2 de las BA exige justificar **componente por componente** con seis criterios: latencia, criticidad operacional, volumen de datos, restricción regulatoria o de seguridad, disponibilidad de conectividad y acoplamiento físico, y costo total de propiedad. Una asignación no justificada *«será evaluada como observación grave»*. El costo se expresa cualitativamente: el Informe 1 no lleva cifras económicas.

| ID físico | Componente lógico | Ubicación | Latencia | Continuidad ante corte | Volumen | Regulación / seguridad | Acoplamiento físico | TCO cualitativo | Justificación final |
|---|---|---|---|---|---|---|---|---|---|
| `PHY-CLD-01` | `GW-EDGE` | nube, zona pública | tolera >100 ms | el portal puede esperar; el terminal no depende de él | moderado | única superficie expuesta; CDN/WAF/anti-DDoS | nulo | elástico, gestionado | La exposición pública se concentra en un solo punto administrado. Ponerlo on-premise obligaría a exponer la red del terminal a Internet, contra `RT-03.04` y la restricción 6. |
| `PHY-CLD-02` | `GW-API` | nube, subred privada | >100 ms | puede esperar | moderado | punto de identidad, cuotas y trazabilidad | nulo | gestionado | Políticas, versionado y catálogo de servicios centralizados. Los consumidores externos son 21 contrapartes; ninguna requiere latencia determinista. |
| `PHY-CLD-03` | `CTX-PLAN`, `CTX-VESSEL`, `CTX-INSP`, `CTX-EMIS`, `SRV-IAM`, `SRV-NOTIF`, `SRV-EVID` | nube, multi-AZ | 100 ms a 1 s | degradación aceptable; ver §6 | moderado | datos comerciales y personales cifrados | nulo | elasticidad estacional | Son procesos de planificación, coordinación y notificación con contraparte externa. Ninguno tiene un umbral inferior a 1 s en el CP, Cap. 15. |
| `PHY-CLD-04` | `INT-HUB` | nube, subred privada | asíncrono | cola durable; el borde acumula | alto en mensajería | contratos y versionado por contraparte | nulo | gestionado | El intercambio con navieras, autoridades, concedente y ferrocarril es asíncrono por naturaleza (EDIFACT, archivo, API). |
| `PHY-CLD-05` | `DATA-CORE` consolidado | nube, multi-AZ | consultas >100 ms | la fuente de verdad operacional durante el corte es local | ≈20–24 GB/año | cifrado en reposo con KMS | nulo | gestionado, multi-AZ | Es el consolidado y el sistema de registro fuera del corte. Durante los 72 h la autoridad pasa a `PHY-OPS-01`; ver §6. |
| `PHY-CLD-06` | `DATA-TS` histórico | nube | analítico | no crítico en corte | ≈68–82 GB/año, ≈340 GB acumulados | retención 5 años de temperatura | nulo | almacenamiento por capas | El histórico de temperatura es evidencia de cadena de frío, no dato de alarma. La alarma vive en el borde. |
| `PHY-CLD-07` | `DATA-DOC` | nube, objetos | tolera latencia | el borde retiene lo del corte | ≈1,4–1,6 TB/año de imágenes OCR | retención 12 meses con eliminación controlada | nulo | objetos con ciclo de vida | Dominan las imágenes OCR. Retenerlas localmente obligaría a dimensionar la sala para 1,6 TB/año sin necesidad operacional. |
| `PHY-CLD-08` | `DATA-AN` | nube | analítico | no crítico | derivado | indicadores del concedente | nulo | gestionado | El `RT-05.29` del caso exige consolidar los indicadores del concedente ≤1 h tras el cierre de turno; eso no compite con la operación. |
| `PHY-CLD-09` | observabilidad y SIEM | nube | asíncrono | el borde almacena y reenvía | logs 12 meses en línea + 24 en archivo | log central inalterable | nulo | gestionado | `RT-03.16` exige que el monitoreo on-premise se integre a **la misma** plataforma que la nube, sin puntos ciegos. |
| `PHY-CLD-10` | réplica de `DATA-CORE`, `DATA-DOC`, `DATA-TS` | nube, región secundaria | n/a | es el destino de la conmutación | réplica | BTT Cap. 7 | nulo | capacidad reducida en reposo | No hay segundo recinto del CLIENTE (CP, Cap. 3) y un secundario en el terminal compartiría las amenazas del principal (`RT-07.02`). |
| `PHY-OPS-01` | `EDGE-RUN` + `CTX-OPS`, `CTX-GATE`, `CTX-YARD`, `CTX-REEFER`, `CTX-BILL`, `CTX-VESSEL` *(subconjunto de muelle)* | on-premise, sala | **≤1 s determinista** | **debe continuar 72 h** | alto, generado localmente | zona operacional segregada, IEC 62443 | directo, vía borde | inversión local con operación acotada | `RT-09.01` del caso exige confirmar un movimiento en ≤1 s y ver la posición en ≤30 s; `RT-03.10` exige 72 h. Ninguna de las dos cosas se resuelve con un enlace de por medio. |
| `PHY-OPS-02` | almacenamiento local | on-premise, sala | ≤1 s | buffer del corte, ≈13 GB + holgura | alto | cifrado en reposo | directo | RAID con tolerancia declarada | `RT-03.14` exige tolerar la falla de al menos un disco y declarar el nivel RAID con su justificación. Dimensionamiento en C4. |
| `PHY-OPS-03` | `INT-TOS` | on-premise, sala | ≤1 s | debe seguir durante el corte | moderado | zona operacional | directo con `EXT-TOS12` | acotado a la coexistencia | El TOS 2012 está en el terminal. Traducir y conciliar a través del enlace agregaría un punto de falla a una integración que ya es la más frágil del proyecto. |
| `PHY-OPS-04` | núcleo de red operacional | on-premise, sala | determinista | **sostiene el corte** | todo el tráfico operacional | segregación operacional / administrativa / protección | directo | equipamiento en HA | La Declaración Mandatoria exige segregar; hoy operación, terminales, cámaras y oficina comparten conmutación (CP, Cap. 6). `RT-08.03` exige HA sin punto único. |
| `PHY-OPS-05` | custodia de medios | on-premise, recinto separado | n/a | soporta el «fuera de sitio» del 3-2-1-1-0 | medios físicos | `RT-06.26` a `RT-06.28` | ninguno | recinto con condiciones ambientales | Exigencia explícita del BTT para el sitio primario, con inventario, rotación y verificación de legibilidad. |
| `PHY-OPS-06` | espacio de operación del personal | on-premise, fuera de la sala de equipos | n/a | n/a | n/a | `RT-06.29` a `RT-06.31` | ninguno | reutiliza instalaciones existentes | `RT-06.30` prohíbe que la operación habitual obligue a entrar al recinto técnico. Con TI del CLIENTE de 5 personas, el espacio se dimensiona en C4, no por defecto. |
| `PHY-EDG-01` | borde de gate | borde, 8 entradas + 6 salidas | **OCR ≤3 s; camión ≤120 s** | gate continúa sin enlace | imágenes OCR | zona primaria aduanera | directo: OCR, básculas, barreras | gabinete marino por puesto | Los umbrales del CP, Cap. 15 se miden en la barrera. El acoplamiento con báscula, barrera y lector es físico y no admite mediación remota. |
| `PHY-EDG-02` | borde de patio | borde, 18 ha | ≤1 s en confirmación | **terminal autónomo hasta 8 h fuera de cobertura** | telemetría de posición ≈37–44 ev/s | zona operacional | directo con equipos | según site survey | Las sombras de la red se mueven cada hora con las pilas (CP, Cap. 6). El diseño no promete cobertura perfecta: hace autónomo al terminal. |
| `PHY-EDG-03` | borde de patio refrigerado | borde, 26 tableros | **alarma ≤5 min** | **alarma local durante el corte** | ≈35,8–43,3 ev/s con muestreo de 1 min | continuidad de cadena de frío | directo con tomas y tableros | concentrador por tablero | El evento del 18 de febrero fue la falla de un tablero completo en turno de madrugada. La alarma no puede depender de un enlace hacia fuera del terminal. |
| `PHY-EDG-04` | borde de muelle | borde, 3 sitios | lectura periódica | opera sin enlace | bajo | **solo lectura, autorización del fabricante** | acoplamiento restringido | mínimo | La restricción 3 y la exclusión del CP, Cap. 11 prohíben intervenir el control de grúas. La cabina recibe una pantalla, no un terminal de captura: el operador no puede manipular un dispositivo mientras opera. |
| `PHY-EDG-05` | borde de zona de inspección | borde, **sin gabinete propio** | ≤1 s | continúa | actas e imágenes | acta firmada como evidencia | dispositivo móvil sobre la red del patio | mínimo | La inspección debe estar disponible a la hora acordada y el acta se firma en terreno. *Corregido en C2 §1: el `CP, Cap. 15, RT-06.01` nombra gabinetes de borde solo en muelle, patio, patio refrigerado y gate; la inspección se sirve por la red operacional del patio y no genera recinto ni fila de T-11 propios.* |

**Componentes lógicos sin nodo propio.** `CH-PORTAL` y `CH-APP` se ejecutan en el dispositivo del usuario y se sirven desde `PHY-CLD-01`; `CH-CAB` se ejecuta en las pantallas de cabina y de terreno alimentadas por `PHY-EDG-04` en muelle, `PHY-EDG-02` en el patio y `PHY-EDG-01` en las casetas de gate *(corregido tras el cruce de D2 B6.3; ver §5.1)*. No generan fila de emplazamiento propia y **no** generan fila de T-11 por sí mismos, sin perjuicio de las licencias que declare C2.

### 5. Matriz lógico → físico

| Componente lógico | Nodo primario | Nodo secundario | Criticidad *(valor de A1 §3.1)* | ¿Vive durante el corte? |
|---|---|---|---|---|
| `CH-PORTAL` | `PHY-CLD-01` | — | media | no; procedimiento manual declarado en A3 |
| `CH-APP` | dispositivo + `PHY-CLD-01` | `PHY-OPS-01` para perfiles internos | alta | sí, en modo interno cifrado |
| `CH-CAB` | `PHY-EDG-04` muelle + `PHY-EDG-02` patio + `PHY-EDG-01` gate | — | alta | sí |
| `GW-EDGE` | `PHY-CLD-01` | — | alta | no; degradación declarada en A3 §7 |
| `GW-API` | `PHY-CLD-02` | — | alta | no; el catálogo central espera al enlace *(A3 §7)* |
| `CTX-OPS` | `PHY-OPS-01` | `PHY-CLD-03` | **crítica** | **sí** |
| `CTX-GATE` | `PHY-OPS-01` + `PHY-EDG-01` | `PHY-CLD-03` | **crítica** | **sí** |
| `CTX-YARD` | `PHY-OPS-01` + `PHY-EDG-02` | `PHY-CLD-03` | **crítica** | **sí** |
| `CTX-REEFER` | `PHY-OPS-01` + `PHY-EDG-03` | `PHY-CLD-03` | **crítica** | **sí** |
| `CTX-BILL` | `PHY-OPS-01` | `PHY-CLD-03` | **crítica** | **sí**, captura de hecho y evidencia |
| `CTX-PLAN` | `PHY-CLD-03` | `PHY-OPS-01` en solo lectura | alta | plan vigente sí; replanificación no |
| `CTX-VESSEL` | `PHY-OPS-01` *(subconjunto muelle)* | `PHY-CLD-03` *(mensajería)* | **crítica** (muelle) / alta (mensajería) | **sí**: órdenes STS, movimientos, ventana activa y productividad, localmente. La mensajería EDIFACT y los anuncios de naves futuras quedan en cola en `INT-HUB` |
| `CTX-INSP` | `PHY-CLD-03` + `PHY-EDG-05` | — | alta | agenda vigente y acta sí; programar nuevas inspecciones no *(A3 §7)* |
| `CTX-EMIS` | `PHY-CLD-03` | `PHY-EDG-02` captura | alta | captura sí; cálculo ISO 14083 y reporte no *(A3 §7)* |
| `SRV-IAM` | `PHY-CLD-03` | `PHY-OPS-01` caché de sesión | alta *(A1)*; **este frente propone elevarla a crítica**, ver §5.1 | sí, con credenciales vigentes; alta de identidad nueva no *(A3 §7)* |
| `SRV-NOTIF` | `PHY-CLD-03` | `PHY-OPS-01` canal local | alta | alarma de frío sí, por canal local |
| `SRV-EVID` | `PHY-CLD-03` | `PHY-OPS-01` sello local | alta | sí, con sello diferido |
| `INT-HUB` | `PHY-CLD-04` | `PHY-OPS-01` cola de salida | alta | acumula, no entrega |
| `INT-TOS` | `PHY-OPS-03` | — | **crítica** | **sí** |
| `EDGE-RUN` | `PHY-OPS-01` | — | **crítica** | **sí, es el que lo sostiene** |
| `DATA-CORE` | `PHY-CLD-05` | `PHY-OPS-01`/`02` | **crítica** | **sí, autoridad local durante el corte** |
| `DATA-TS` | `PHY-CLD-06` | `PHY-OPS-02` ventana caliente | alta | sí, ventana local |
| `DATA-DOC` | `PHY-CLD-07` | `PHY-OPS-02` buffer | alta | retiene y sincroniza |
| `DATA-AN` | `PHY-CLD-08` | — | media | no |

Las **nueve** filas marcadas como críticas —`CTX-OPS`, `CTX-GATE`, `CTX-YARD`, `CTX-REEFER`, `CTX-BILL`, `CTX-VESSEL`, `INT-TOS`, `EDGE-RUN` y `DATA-CORE`— son exactamente las que A1 §3.1 incluye en `EDGE-RUN`, y son la traducción física de las cinco funciones del Maestro §9.1. `SRV-IAM` aparece con caché local porque una autenticación que dependa de la nube convertiría el corte de enlace en un corte de operación.

#### 5.1 De dónde sale la criticidad, y las siete diferencias que detectó D2

**La criticidad no la define este entregable, y la columna lleva ahora el nombre de su dueño.** Es un atributo del catálogo lógico: A1 §3.1 la declara componente por componente y publica su escala —*crítica* es «debe sobrevivir 72 h sin enlace exterior; incluida en `EDGE-RUN`»; *alta* es «degradación tolerable por horas; requiere fallback documentado»; *media* es «disponible solo con enlace exterior activo»—. C1 la **traduce a nodos**; no la reescribe. La versión anterior de esta matriz llevaba valores propios y ahí nació el problema.

**Por qué no se hizo una tabla de correspondencia entre dos escalas.** Frente 1 propuso declarar que A1 mide un eje lógico y C1 uno físico, que ninguna está mal y que falta una equivalencia entre ambas. Se descartó de común acuerdo, y la razón está en esta misma tabla: **la escala de A1 mide continuidad ante el corte** —«debe sobrevivir 72 h; incluida en `EDGE-RUN`»—, que es exactamente lo que esta matriz ya media en su **última columna**. Había dos columnas midiendo lo mismo con nombres distintos, y por eso derivaron. Sostener dos escalas homónimas habría sido la **tercera colisión de término** de esta célula, después de los códigos `RT` y de los identificadores `SPOF`. Si en algún momento este entregable necesita expresar redundancia física, esa columna llevará su propio nombre —clase de alta disponibilidad—, no «criticidad». Registrado en A1 §3.1 y en `TRZ-A1-041`.

El cruce `B6.3` de D2 comparó las dos tablas componente por componente y encontró **siete diferencias**. Todas eran reales. Se resuelven así:

| Componente | A1 §3.1 | C1 antes | Resolución | Por qué |
|---|---|---|---|---|
| `CTX-VESSEL` | **Crítica**; A1 la precisa el 06-09 como **dual**: `Crítica` en el subconjunto de muelle, `Alta` en la mensajería | alta, solo en `PHY-CLD-03` | **se adopta la partición dual de A1 y se corrige el nodo** | ver el párrafo siguiente: era una contradicción, no un matiz |
| `GW-EDGE` | Alta | media | se adopta A1 | el borde público no vive el corte, pero su caída **sí** deja al terminal sin canal externo; «media» decía que no importa |
| `GW-API` | Alta | media | se adopta A1 | ídem: es el punto de identidad, cuotas y trazabilidad de 21 contrapartes |
| `CTX-INSP` | Alta | media | se adopta A1 | el acta de inspección es evidencia con valor ante autoridad; su pérdida no es indolora |
| `CTX-EMIS` | Alta | media | se adopta A1 | el cálculo ISO 14083 es obligación de reporte, no un indicador interno |
| `DATA-DOC` | Alta | media | se adopta A1 | contiene imágenes OCR, actas y firmas; es el respaldo probatorio del gate y de la inspección |
| `SRV-IAM` | Alta | **crítica** | **se adopta A1 en la tabla y se escala la propuesta de elevarla** | único caso donde C1 era **más** exigente que A1, y con razón física; ver abajo |

**`CTX-VESSEL` era una contradicción de este frente consigo mismo, y hay que decirlo.** A1 §3.1 lo declara `Crítica` y lo nombra explícitamente entre los componentes que `EDGE-RUN` replica; A3 incluye la operación de nave entre las cinco funciones críticas; y la propia matriz de continuidad de C3 §7 pone «Nave y movimientos» sobre el núcleo local. Sin embargo la tabla de emplazamiento del §4 lo dejaba **solo** en `PHY-CLD-03`, en nube. Con esa asignación, un corte de enlace habría detenido la atención de nave: exactamente lo que el `CP, Cap. 15, RT-03.10` prohíbe. `PHY-OPS-01` incorpora ahora `CTX-VESSEL` y la fila de la matriz lo refleja. Lo que **sí** espera al enlace es la mensajería EDIFACT, que queda en cola en `INT-HUB` — eso ya estaba bien dicho en A1 §3.2 y en C3 §7.1. Hallazgo `B6-F03` de D2; se registra como `F2-COR-005`.

**`SRV-IAM`: aquí C1 no se alinea en silencio, propone.** Si durante las 72 horas nadie puede autenticarse, las cinco funciones críticas no se operan aunque el cómputo esté vivo: el corte de enlace se convierte en corte de operación. Ese es el motivo por el que la matriz le asigna caché de sesión en `PHY-OPS-01` y por el que C2 marca `SEC-IAM-01` como requisito excluyente de capacidad local. Por la escala de A1, «debe sobrevivir 72 h e ir en `EDGE-RUN`» es la definición de *crítica*. La tabla adopta el valor de A1 porque el catálogo es suyo, y **se escala a Frente 1 la propuesta de elevar `SRV-IAM` a `Crítica`** con este argumento. Queda como `F2-ESC-017`. Mientras no se resuelva, la capacidad local se especifica igual: la decisión afecta la etiqueta, no el dimensionamiento.

**`CH-CAB` no vive solo en el muelle.** D2 observó que C1 lo ubicaba en `PHY-EDG-04` mientras A1 lo usa como canal de cabina **y de terreno**. Al revisar A1 §2.1, `CH-CAB` es el canal de `ACT-GRU` (cabina de grúa y de equipos de patio), de `ACT-GATE` (terminal en caseta) y de `ACT-EVT` (terminal compartido por turno); y A1 §3.2 le atribuye el umbral de **8 horas de sombra de radio en el patio**, que es un dato de patio, no de muelle. La corrección alcanza a los tres bordes: `PHY-EDG-04` en muelle, `PHY-EDG-02` en patio y `PHY-EDG-01` en las casetas de gate. No cambia el T-11 —las pantallas de cabina y los terminales robustos ya están contados en `T11-C2-15` y en los gabinetes de `T11-C2-14`—, pero sí cambia el diagrama físico y la superficie que D1 debe proteger. Hallazgo `B6-F04`; `F2-COR-006`.

#### 5.2 La consola de administración de `ACT-TI`: respuesta física a una brecha de A1

A1 declara una brecha explícita en `F1-OBS-002`: el canal de `ACT-TI` («consola de administración») no corresponde a ningún componente de su §3.1, y el Maestro §4.3 exige que la plataforma sea operable por las **cinco** personas de TI del CLIENTE sin especialistas por módulo. D1 la protege con PAM sin inventar un `CH-*`. La brecha es de Frente 1 y este entregable no la cierra, pero sí debe responder qué pasa **físicamente** si A1 termina nombrando ese canal, porque una respuesta tardía cambiaría nodos y T-11 a última hora.

La respuesta es que **no aparece un nodo nuevo**. La administración técnica ya tiene lugar en esta arquitectura:

| Pregunta física | Respuesta con la arquitectura actual |
|---|---|
| ¿desde dónde se administra? | `PHY-OPS-06`, el espacio de operación del personal fuera de la sala de equipos que exige `RT-06.30`, y los puestos de `T11-C2-13` |
| ¿por qué camino? | la zona `Z-MGMT` de D1, servida por `PHY-CLD-02` hacia la nube y por `PHY-OPS-04` hacia el terminal, con PAM y grabación de sesión (`RT-12.06`) |
| ¿qué se compra? | nada nuevo: la plataforma de identidad y PAM ya es `T11-SEC-02`; el puesto ya es `T11-C2-13` |
| ¿qué cambiaría si A1 nombra un `CH-ADM`? | una fila más en la matriz lógico→físico de §5, con nodo primario `PHY-CLD-02` y acceso desde `PHY-OPS-06`. **Ninguna fila nueva de T-11** |

Se deja escrito para que la resolución de `F1-OBS-002` no reabra el emplazamiento ni el T-11. Registrado como `F2-INT-003`.

### 6. Autoridad del dato durante la desconexión

Es la consecuencia física de la regla negativa 8 del Maestro y hay que decirla explícitamente, porque decide dónde va el almacenamiento y no solo el cómputo:

| Fase | Autoridad de `DATA-CORE` | Qué ocurre con la nube |
|---|---|---|
| operación normal | nube, con réplica local caliente | sistema de registro |
| corte del enlace | **núcleo local `PHY-OPS-01`** | queda atrás; no recibe |
| reconexión | local, hasta cerrar la reconciliación | recibe el diferencial |
| conciliación cerrada | vuelve a nube | sistema de registro |

El traspaso debe ser explícito y auditado. La sincronización objetivo es ≤90 min tras 72 h de corte (CP, Cap. 15, `RT-03.13`, materia «sincronización tras la reconexión» — ver la colisión de código registrada en `F2-ESC-006`). El diseño del mecanismo pertenece a A3; aquí se declara únicamente su consecuencia física: el buffer y la capacidad de cómputo local se dimensionan para el peak coincidente durante 72 h, no para el promedio. Dimensionamiento en C4.

### 6.bis Correspondencia con las zonas de seguridad de D1

`SEC-PHYS-v0.1` del Frente 3 llegó el 2026-09-05 con nueve zonas lógicas y once flujos autorizados. Una zona de D1 **no es un nodo**: es un ámbito de política. Varias zonas pueden materializarse sobre el mismo nodo mediante controles de plataforma o de red, y una zona puede repartirse entre varios nodos. Esta tabla fija esa correspondencia para que ambos frentes usen los mismos identificadores.

| Zona D1 | Nodo o nodos físicos que la materializan | Cómo se realiza el aislamiento |
|---|---|---|
| `Z-EXT` redes externas | ninguno: está fuera del límite de la oferta | es el origen del tráfico, no un emplazamiento nuestro |
| `Z-EDGE` borde expuesto | `PHY-CLD-01` | única superficie pública; el origen no se publica (`RT-03.04`) |
| `Z-SVC` servicios privados en nube | `PHY-CLD-02`, `PHY-CLD-03`, `PHY-CLD-04` | subred privada de aplicación, sin alcance desde Internet |
| `Z-DATA` almacenes protegidos | `PHY-CLD-05` a `PHY-CLD-08` en nube; `PHY-OPS-02` en el terminal | subred privada de datos; acceso solo por identidad de servicio. **Es un ámbito de política repartido entre nube y sala**, no una base única |
| `Z-LOCAL` servicios operacionales locales | `PHY-OPS-01` y `PHY-OPS-03` | sostiene las 72 h sin enlace; no depende del borde en nube |
| `Z-FIELD` equipos de terreno | `PHY-EDG-01` a `PHY-EDG-04` y los terminales de equipo | segmentación por tipo de dispositivo (`RT-03.23`); C3 la subdivide por criticidad y por fabricante |
| `Z-ADM` red administrativa | `PHY-OPS-06`, espacio de operación del personal | sin ruta general hacia patio, protección ni datos |
| `Z-PROT` protección | `EXT-VMS` y `EXT-ACC` del terminal, **fuera del límite de la oferta** | conducto mínimo aprobado; sin portal de video ni tránsito general |
| `Z-MGMT` administración técnica | atraviesa `PHY-CLD-*` y `PHY-OPS-*`; sin nodo propio | acceso por PAM, separado del uso de negocio |

**Tres consecuencias que conviene dejar escritas.**

`Z-MGMT` **no tiene nodo propio y no debe tenerlo**. Es un plano de acceso que cruza nube y sala; darle un servidor de administración propio en el terminal agregaría una superficie más que endurecer y una más que operar con un área TI de cinco personas.

`Z-DATA` **no coincide con un solo nodo**. La ubicación de cada almacén ya está decidida en la tabla de emplazamiento del §4 según los seis criterios del Art. 16; la zona aporta la política de acceso, no el lugar. Que `DATA-CORE` tenga réplica local durante el corte no crea una segunda `Z-DATA`: es la misma política aplicada en dos emplazamientos.

`Z-PROT` **queda fuera del límite de la oferta**. El VMS y el control de acceso del recinto portuario se conservan (`SPOF` y §2). Lo que sí ofertamos es el **conducto** hacia ellos y el CCTV propio de la sala técnica, que es cosa distinta y está declarada en `F2-DEC-003`.

**Dónde vive cada capacidad de `SEC-PHYS-v0.1`.** Emplazamiento, que es lo que D1 pide de C1; el producto lo resuelve C2 y la cantidad C4.

| Grupo `SEC-PHYS` | Nodo físico que lo aloja | Nota de emplazamiento |
|---|---|---|
| `SEC-EDGE-01/02` borde, WAF, DDoS, TLS | `PHY-CLD-01` | único borde público; no se replica en el terminal |
| `SEC-API-01` gateway | `PHY-CLD-02` | detrás del borde |
| `SEC-NET-01 / SEC-EXP-01` segmentación e inventario de exposición | `PHY-OPS-04` en el terminal y controles de plataforma en nube | el núcleo de red operacional es el punto de aplicación local |
| `SEC-IAM-01 / SEC-ADM-01 / SEC-PROD-01` identidad, PAM, terreno | `PHY-CLD-03` con **capacidad local en `PHY-OPS-01`** | la caché local es la que impide que un corte de enlace se vuelva un corte de operación (§5) |
| `SEC-SYNC-01` conducto nube–local | enlace `PHY-OPS-04` ↔ nube | su dimensionamiento es el de C4 §5.1: lo fija la reposición, no el régimen |
| `SEC-DATA-01 / SEC-ENC-01 / SEC-FIELD-01` cifrado | todos los almacenes: `PHY-CLD-05`..`08` y `PHY-OPS-02` | capacidad nativa del almacén; no genera nodo |
| `SEC-KEY-01 / SEC-SECRET-01` claves y secretos | gestionado en nube **con capacidad local protegida en `PHY-OPS-01`** | si la clave vive solo en nube, la operación local de 72 h no puede descifrar. Es el punto que D1 marca como excluyente en `ADR-009` |
| `SEC-BKP-01` respaldo | `PHY-CLD-10` y **`PHY-OPS-05` custodia de medios** | la copia «fuera de sitio» del 3-2-1-1-0 tiene recinto físico: `RT-06.26`..`28` |
| `SEC-LOG-01 / SEC-SIEM-01` registro y SIEM | `PHY-CLD-09` con **colector y buffer local en `PHY-OPS-01`** | `RT-03.16` exige una sola plataforma sin puntos ciegos; el buffer local cubre las 72 h |
| `SEC-END-01` EDR | agentes en `PHY-OPS-01`, `PHY-CLD-03` y puestos de `PHY-OPS-06` | los dispositivos de terreno **no** se presumen compatibles con agente: C2 lo declara por clase |
| `SEC-SOC-01 / SEC-IR-01` SOC y respuesta | servicio externo; sin nodo | no se asigna silenciosamente al área TI de cinco personas |
| `SEC-VULN-01`, `SEC-PENTEST-01` | servicio; sin nodo | — |
| `SEC-SDLC-01 / SEC-PIPE-01`, `SEC-SUPPLY-01 / SEC-ART-01`, `SEC-NPDATA-01` | ambientes DEV, QA y PREPROD; fuera de la zona operacional | ingeniería separada de producción; el detalle es de C3 §4 |
| `SEC-GOV-01 / SEC-CLOUD-01 / SEC-HARD-01 / SEC-SAMM-01` | transversal; sin nodo | `SEC-HARD-01` aterriza como línea base CIS por producto en C2 |

**Lo que este cruce le devuelve al Frente 3.** La auditoría B7 de D1 registró en `B7-F05` que «A1–A3 y C1–C4 visibles siguen en estructura/plantilla, sin catálogos, contratos, nodos, productos ni cantidades utilizables para validar D1», y mantuvo abierta `F3-DEP-003`. Ese diagnóstico correspondía al estado de `main` al 2026-09-05, cuando los paquetes del Frente 2 todavía vivían en la rama `frente_2` sin integrar. **Con esta consolidación, C1 aporta los nodos y las zonas, C2 los productos y las clases, C3 las redes y la continuidad, y C4 el dimensionamiento y las cantidades.** `F3-DEP-003` puede cerrarse contra este material.

### 7. Alternativas de sala técnica — insumo para `ADR-005`

La Decisión N° 20 de Célula 2 dejó el destino de la sala como ADR con tres alternativas. Se evalúan contra los requisitos que el BTT hace obligatorios cuando existe cómputo sustantivo en el sitio del CLIENTE, que es el caso.

| Criterio | A. Endurecer la sala actual | B. Sala nueva dentro del terminal | C. Borde mínimo + nube |
|---|---|---|---|
| `BTT, Cap. 6, RT-06.01` uso exclusivo, aislado, acceso independiente *(no el `RT-06.01` del caso, que fija la tipología)* | dudoso: está dentro del edificio administrativo | cumple por diseño | no aplica en la misma escala |
| `RT-06.29`/`.30` espacio de operación **separado** de la sala de equipos | difícil en 34 m² | cumple por diseño | cumple: la operación es remota |
| `RT-06.32` rutas físicas distintas, **ingreso al edificio por puntos separados** | **posible criterio de descarte**; depende del edificio, hoy con un solo proveedor de fibra | cumple si se especifica en la obra | sigue exigiendo dos caminos hacia la nube |
| UPS ≥30 min y generación ≥24 h | hoy 25 min; exige reemplazo del respaldo | cumple por diseño | menor carga, pero el borde igual requiere respaldo |
| ambiente marino a <300 m de la costa | **no desaparece**; regla negativa 11 | **no desaparece** si sigue en el recinto | se reduce la superficie expuesta, no se elimina |
| 72 h de las cinco funciones críticas | cumple si hay cómputo local suficiente | cumple | **el riesgo está aquí**: «mínimo» no puede bajar de las cinco funciones |
| plazo: todo lo invasivo listo el **14-dic-2027** | menor obra, plazo más holgado | obra civil dentro de ~10 meses útiles | menor obra, pero más instrumentación de borde |
| congelamiento 15-dic a 30-abr y prohibición de intervenir con nave o 4 h antes | favorece la obra acotada | riesgo de calendario alto | favorece |
| operabilidad con TI de 5 personas | media | media | **la mejor**: menos superficie que administrar |

**Observaciones para quien redacte el ADR.** Primero, `RT-06.32` puede resolver la comparación antes que cualquier criterio de costo: si el edificio administrativo no admite dos ingresos físicos separados de comunicaciones, la alternativa A no cumple una obligación del BTT y queda descartada por norma, no por opinión. Ese dato **no está en el caso** y debe levantarse; queda registrado como `F2-ESC-008`. Segundo, la alternativa C no puede interpretarse como «poner lo mínimo en el terminal»: el piso de lo local está fijado por las cinco funciones críticas y por los umbrales de ≤1 s y ≤5 min, de modo que C se distingue de B por el tamaño del recinto, no por la existencia de cómputo local. Tercero, ninguna alternativa puede presumir que mover la sala elimina el ambiente marino.

**Lo que aporta la revisión de ADR de D2 §B5.** El Frente 3 amarró `ADR-005` a puntos de falla y amenazas concretos, y fijó su consecuencia negativa ineludible: *«ninguna alternativa puede eliminar la autonomía de 72 h ni presumir instalación fuera del ambiente marino»* — coincide con la regla negativa 11 del Maestro y con lo dicho arriba. Los anclajes son `SPOF-06` (sala técnica, energía y ambiente) y `SPOF-01` (`EDGE-RUN` y su almacenamiento) de su registro, más las amenazas `THR-052` y `THR-054`, y el disparador de revisión es `ESC-09`. El estado recomendado es `CANDIDATO`, con riesgo residual atado a `SPOF-06` en estado `ESCALADO`.

> **Ojo con el rango.** La fila de `ADR-005` en D2 §B5 dice «aplican íntegros `RT-06.01` a `RT-06.24`». Es el mismo error que el Maestro §10.3 y que el contrato original de C2: el BTT exige hasta **`RT-06.34`**. Es el tercer documento donde se propaga; ver `F2-ESC-004`.

**Recomendación preliminar de este frente, no vinculante:** una variante acotada de C —recinto técnico nuevo y pequeño, dimensionado estrictamente a las cinco funciones críticas y a su buffer de 72 h, con el resto de la plataforma en nube y el secundario en la región secundaria— es la que mejor concilia el plazo del 14-dic-2027, el congelamiento estacional y un área TI de cinco personas. Se somete a `ADR-005` con las tres alternativas desarrolladas.

### 8. Registro inicial de puntos únicos de falla

El Maestro, regla negativa 14, prohíbe ocultarlos. Los cinco primeros son condiciones **preexistentes** del CP, Cap. 6, no defectos de nuestro diseño; el entregable es declarar cuáles corregimos, cuáles quedan y quién los acepta.

| ID | Punto único de falla | Origen | Estado tras el diseño propuesto | Tratamiento |
|---|---|---|---|---|
| `F2-SPOF-01` | fibra de un solo proveedor hacia el exterior | CP, Cap. 6 | **corregido** | `RT-03.17`: segundo camino por proveedor distinto y conmutación automática con tiempo declarado; C3 |
| `F2-SPOF-02` | radioenlace de respaldo sin prueba de conmutación real desde 2022 | CP, Cap. 6 | **corregido** | prueba de corte real como criterio de aceptación; C3 |
| `F2-SPOF-03` | operación, administración y CCTV sobre la misma conmutación | CP, Cap. 6 | **corregido** | segregación IEC 62443 con conductos controlados; Decisión 19; C3 y D1 |
| `F2-SPOF-04` | 26 tableros reefer sin instrumentación remota | CP, Cap. 6 y 7.2 | **corregido** | `PHY-EDG-03`, concentrador por tablero; alarma de tablero como evento propio |
| `F2-SPOF-05` | generación de respaldo del patio refrigerado nunca verificada a carga total de temporada | CP, Cap. 6 | **queda abierto** | fuera del límite de oferta; se especifica la prueba y se escala al CLIENTE |
| `F2-SPOF-06` | emplazamiento único: todo el terminal comparte sitio, acceso vial y amenazas | CP, Cap. 3 | **mitigado, no eliminado** | secundario en región secundaria de nube; `RT-07.02` con análisis de amenazas comunes |
| `F2-SPOF-07` | sala técnica única en el terminal durante el corte de 72 h | diseño | **residual aceptado** | redundancia interna de equipos (`RT-03.14`, `RT-08.03/04`); un segundo recinto local no es viable ni útil frente a amenazas comunes |
| `F2-SPOF-08` | `EXT-TOS12` como fuente de verdad durante la coexistencia | Decisión 1 | **acotado en el tiempo** | puerta de viabilidad en H2/mes 4; A3 |
| `F2-SPOF-09` | proveedor de nube único | Art. 16 | **residual declarado** | `RT-03.07`: estrategia de reversibilidad y portabilidad por componente; C2 |
| `F2-SPOF-10` | red inalámbrica de patio con sombras móviles | CP, Cap. 6 | **mitigado por diseño** | el terminal de patio es autónomo hasta 8 h fuera de cobertura; la red no se declara perfecta; site survey pendiente (`F2-ESC-001`) |


#### 8.1 Correspondencia con el registro consolidado de D2

El `B4` de D2 publicó un **registro consolidado de 21 puntos únicos de falla**, y ese es su producto obligatorio: es el registro de referencia del Subdocumento 4. Los diez de esta sección se habían numerado antes de que existiera, con los mismos códigos `SPOF-01` a `SPOF-10` **para materias distintas**. Los diez de aquí pasan a `F2-SPOF-*` y la numeración de D2 queda como la única global. Se registra en `F2-ESC-014`.

| `F2-SPOF` de este entregable | Materia | En el registro de D2 |
|---|---|---|
| `F2-SPOF-01` | fibra de un solo proveedor | cubierto por `SPOF-02` enlace exterior |
| `F2-SPOF-02` | radioenlace de respaldo sin prueba desde 2022 | cubierto por `SPOF-02`, pero **el matiz «sin conmutación real desde 2022» es dato del `CP, Cap. 6`** y conviene que su ficha lo recoja |
| `F2-SPOF-03` | operación, administración y CCTV sobre la misma conmutación | **no está en D2.** Su `SPOF-18` trata el VMS y su conducto, que es otra cosa |
| `F2-SPOF-04` | 26 tableros reefer sin instrumentación remota | **no está en D2** |
| `F2-SPOF-05` | generación de respaldo del patio refrigerado nunca verificada a carga total | **no está en D2** |
| `F2-SPOF-06` | emplazamiento único: sitio, acceso vial y amenazas compartidas | parcialmente en `SPOF-06`, que es de la sala; el nuestro es del **recinto completo** |
| `F2-SPOF-07` | sala técnica única durante el corte de 72 h | cubierto por `SPOF-06` |
| `F2-SPOF-08` | `EXT-TOS12` como fuente de verdad durante la coexistencia | cubierto por `SPOF-17` |
| `F2-SPOF-09` | proveedor de nube único | **no está en D2.** Su `SPOF-20` es el proveedor de SOC, distinto |
| `F2-SPOF-10` | red inalámbrica de patio con sombras móviles | cubierto por `SPOF-03` medio de radio del patio |

**Cuatro puntos de falla de este entregable no están en el registro consolidado** —`F2-SPOF-03`, `04`, `05` y `09`—, y los cuatro son **condiciones preexistentes que el `CP, Cap. 6` describe explícitamente**, no riesgos de diseño. `RT-02.11` del BTT exige declarar los puntos únicos de falla que subsistan **y justificar por qué son aceptables**, y advierte que omitirlo cuando existen se evalúa como falta. Se traspasan a D2 en `F2-ESC-014`.

**Y tres del registro de D2 que este entregable no tenía**, incorporados aquí por referencia:

| De D2 | Por qué toca a este frente |
|---|---|
| `SPOF-04` referencia temporal | es la consecuencia de `FL-10`: sin hora común no hay orden de eventos y la reconciliación determinista tras el corte falla. Está tratado en C3 §5.ter, pero no estaba **declarado como punto de falla** |
| `SPOF-15` aprobador único de break-glass | con un área TI de cinco personas y turnos 24×7, el acceso de emergencia puede depender de una sola persona localizable. Condiciona el procedimiento de C3 §9 |
| `SPOF-16` dotación de turno, suplencias y habilitación ISPS | la estabilización exige presencia en los tres turnos con habilitación ISPS (`CP, Cap. 13.3`, condición 8); si esa dotación no existe, el paso a producción se detiene |


### 9. Lo que este entregable deja sujeto a levantamiento

| ID | Qué falta | Efecto si no se levanta |
|---|---|---|
| `F2-ESC-001` | site survey del patio con carga real | cantidad y ubicación de estaciones base quedan como rango |
| `F2-ESC-002` | aprobación de la autoridad para la segregación de red | no se interviene la red de protección |
| `F2-ESC-008` | ingresos físicos de comunicaciones disponibles en el edificio administrativo | `ADR-005` no puede cerrarse por norma; se decide por criterios secundarios |
| `ESC-06` | contratos e interfaces de TOS, VMS, autoridades, ferrocarril, radio, grúas y periféricos | los nodos de borde se especifican por clase, no por producto |

### 10. Definición de terminado — estado

- [x] Todos los componentes desplegables tienen ubicación y justificación por los seis criterios.
- [x] La solución es híbrida y multi-AZ, con región primaria y secundaria declaradas.
- [~] Se describen sala, borde, nube, DR, enlaces y sistemas conservados; **la vista gráfica queda pendiente** por la decisión de equipo de dibujar al final.
- [x] Las 72 h no dependen de nube: la autoridad del dato pasa al núcleo local.
- [x] No se presume que el ambiente marino desaparece.
- [x] Físico, catálogo lógico y T-11 usan los mismos IDs.
- [ ] `TRZ_C1.md` completo — en curso.
- [x] Cruce con D1 `SEC-PHYS-v0.1` — §6.bis: nueve zonas mapeadas a nodos y las 17 capacidades emplazadas.
- [ ] Revisión cruzada con A1 `v0.1` — Puerta 1.
- [ ] Diagrama de la vista física — se produce en el pase final de diagramas del Subdocumento 4.


## Trazabilidad

Ver [`trazabilidad/TRZ_C1.md`](trazabilidad/TRZ_C1.md).

