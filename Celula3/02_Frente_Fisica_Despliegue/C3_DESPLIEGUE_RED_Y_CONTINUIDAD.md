# C3 — Despliegue, red y continuidad

## Contrato del entregable

### Objetivo y destino

Definir ambientes, redes, despliegue, alta disponibilidad, recuperación, respaldos y comportamiento ante desconexión. Alimenta las secciones 4.2.7–4.2.10.

### Cumplimientos asignados

- `SD4-04`, `SD4-05`, `SD4-07`, `SD4-08`.
- T7-4.4/4.5; BTT Cap. 3 completo (`RT-03.01..24`), Cap. 4, Cap. 7 completo (`RT-07.01..14`) y Cap. 10; Art. 20 y 24.
- Checklist del BTT, Cap. C, entregables N° 4 (funciones no disponibles en modo desconectado, con A3), N° 9 (plan de recuperación ante desastres y política de respaldo) y N° 12 (plan de continuidad del negocio conforme a ISO 22301, `RT-10.03`).

> *Corrección `F2-COR-003` (2026-09-05): el contrato no citaba el Capítulo 7 del BTT, que es la fuente de RTO/RPO, replicación, conmutación, retorno y respaldos, ni `RT-10.03`. Los entregables N° 9 y N° 12 del checklist no tenían producto asignado en ningún contrato del frente. Ver `trazabilidad/DECISIONES_Y_ESCALAMIENTOS.md`, `F2-ESC-003` y `F2-ESC-005`.*
- `MC-09/10/11/27/30`, RNF-DIS y RNF-DES aplicables.

### Entradas obligatorias

- Maestro §§4.3, 9–13, 18–19.
- C1 topología, C2 catálogo y D1 `SEC-PHYS-v0.1`.
- A3 procesos críticos y operación desconectada.

### Trabajo requerido

- [ ] Definir DEV, QA, PREPROD, PROD y DR aislados.
- [ ] Demostrar equivalencia PREPROD/PROD.
- [ ] Definir IaC, CI/CD, rollback y despliegue progresivo sin interrupción.
- [ ] Diseñar zonas operacional, administrativa y protección, y conductos autorizados.
- [ ] Mantener VMS/ISPS durante la segregación.
- [ ] Diseñar enlaces redundantes por caminos/proveedores distintos y conmutación automática.
- [ ] Exigir site survey con patio cargado, sombras móviles y handover.
- [ ] Probar corte real de fibra/radioenlace sin pérdida transaccional.
- [ ] Definir HA, réplicas, balanceo y SPOF.
- [ ] Definir RTO/RPO, DR, 3-2-1-1-0 y restauración.
- [ ] Instrumentar la replicación con medición y alertamiento del retraso (`RT-07.03`).
- [ ] Documentar la conmutación de modo que sea **ejecutable por el personal del CLIENTE**, que son cinco personas (`RT-07.05`).
- [ ] Documentar y probar el retorno al sitio principal, con reconciliación de lo generado durante la contingencia (`RT-07.06`).
- [ ] Declarar, por dominio de dato, frecuencia de respaldo, retención y tiempo de restauración completa, cruzado con las siete retenciones del Maestro §16.1 (`RT-07.13`).
- [ ] Proteger las copias inmutables frente a credenciales administrativas comprometidas (`RT-07.10/11`).
- [ ] Resolver 72 h, buffer, recuperación y sincronización ≤90 min.
- [ ] Aplicar retorno a toda intervención y congelamiento/nave.

### Matriz de ambientes obligatoria

| Ambiente | Propósito | Aislamiento | Datos | Topología | Acceso | Despliegue | Retención/limpieza |
|---|---|---|---|---|---|---|---|
| DEV | desarrollo | obligatorio | sintéticos | proporcional | equipo autorizado | CI | POR DEFINIR |
| QA | pruebas | obligatorio | sintéticos | proporcional | QA | CI/CD | POR DEFINIR |
| PREPROD | validación | obligatorio | anonimizados/sintéticos | equivalente PROD | restringido | igual a PROD | POR DEFINIR |
| PROD | operación | obligatorio | reales | HA | mínimo privilegio | progresivo | según clase |
| DR | recuperación | obligatorio | réplica | capacidad RTO/RPO | emergencia/PAM | automatizable | según clase |

### Matriz de continuidad obligatoria

| Servicio/proceso | Criticidad | HA | Dependencia | RTO | RPO | 72 h local | Fallback manual | Prueba | SPOF residual |
|---|---|---|---:|---:|---:|---|---|---|---|
| nave/movimientos | crítica | POR DEFINIR | POR DEFINIR | ≤4 h contractual; operativo por definir | ≤15 min | sí | POR DEFINIR | E2E/DR | POR DEFINIR |

### Productos obligatorios

1. Vista de despliegue/red.
2. Matriz de ambientes.
3. Matriz HA/DR/respaldo/72 h.
4. Plan de recuperación ante desastres y política de respaldo (checklist N° 9).
5. Plan de continuidad del negocio conforme a ISO 22301 (checklist N° 12, `RT-10.03`).
6. Plan de pruebas de red, failover, DR y restauración.
7. Calendario de intervención y retorno.
8. Candidatos `ADR-006/007`.

### Aporte T-11/ADR

Entrega a C4 componentes de red, HA, respaldo, DR, monitoreo y sitio que requieran fila o cantidad.

### Salidas hacia otros frentes

- Frente 3: zonas, conductos, accesos administrativos y failover.
- Frente 1: restricciones de disponibilidad que requieran degradación lógica.

### Definición de terminado

- [ ] Cinco ambientes explícitos y aislados.
- [ ] Red de patio se valida en condición real; ubicación queda sujeta a site survey.
- [ ] VMS no se degrada durante segmentación.
- [ ] RTO/RPO, DR, respaldo y restauración tienen prueba.
- [ ] 72 h y 90 min están dimensionados y trazados.
- [ ] No se programa intervención prohibida.
- [ ] `TRZ_C3.md` completo.

## Contenido listo para integrar

**Versión:** `v0.5` — contenido completo, sujeto a revisión cruzada en la Puerta 2.
**Fecha:** 2026-09-05. **Destino:** consolidado 4.2.7 a 4.2.10.

### 1. La restricción que ordena todo este paquete

Tres cláusulas del caso, leídas juntas, dejan una sola salida arquitectónica.

La restricción no negociable **2** dice que el terminal no se detiene: *«La operación es 24x7x365 y una nave amarrada consume tiempo de muelle desde el momento en que amarra. **No existe ventana de detención total**.»* La **9** prohíbe intervenir entre el 15 de diciembre y el 30 de abril. La **10** prohíbe intervenir *«durante la atención de una nave, y en las cuatro horas previas a una ventana de atraque confirmada»*.

El caso registra **620 naves al año** sobre 3 sitios, es decir del orden de 1,7 recaladas diarias, cada una con ventana comprometida. No conocemos la programación de atraque —es un dato que hay que pedir— pero no hace falta para la conclusión: la unión de los períodos bloqueados por la restricción 10 no es un residuo del calendario, es su mayor parte. Sumado a que de los doce meses hay cuatro y medio congelados, buscar «una ventana de despliegue» es buscar algo que este terminal no tiene.

**La consecuencia de diseño es directa: el despliegue de software no puede necesitar ventana.** No es una preferencia metodológica; es la única forma de cumplir simultáneamente las tres restricciones. Y coincide con lo que las bases ya exigen por su lado: `RT-04.07` del BTT y el Art. 24 de las BA obligan a liberar sin interrupción del servicio —azul-verde, canario o progresivo—, demostrado en Preproducción **antes de cada** paso a producción, y `RT-10.06` declara que las ventanas de indisponibilidad programada son excepcionales y deben justificarse caso a caso.

De ahí sale la distinción que estructura el numeral 12 de este entregable: **la intervención de software no consume ventana; la intervención física sí**. Cambiar la red del patio, instalar 26 concentradores en tableros energizados, tender canalizaciones o migrar la conmutación no se hace en caliente. Esas son las que compiten con las naves y con el congelamiento, y son las que el Maestro §13 obliga a tener instaladas, migradas, probadas, con retorno y capacitación **a más tardar el 14 de diciembre de 2027**.

### 2. Los cinco ambientes y un hallazgo de calendario

El BTT, numeral 4.1, define **cinco** ambientes: Desarrollo, QA, Preproducción, Producción y **Recuperación ante desastres**. El Art. 24 de las BA enumera *«cuatro ambientes obligatorios —Desarrollo, QA, Preproducción y Producción»* y no menciona el quinto, porque la recuperación ante desastres la trata por separado en su Art. 20.

Eso no es una contradicción sino un complemento, y el Art. 5.2 de las BA lo resuelve expresamente: *«Los documentos conforman un todo integrado y se complementan recíprocamente. Toda obligación que aparezca en cualquiera de ellos se entenderá parte del Contrato, aunque no se repita en los demás.»* Son cinco.

Lo que sí es un hallazgo, y tiene consecuencias de plazo y de costo, es **cuándo**:

> `RT-04.01`: «Los **cinco** ambientes del numeral 4.1 estarán habilitados y operativos **como condición del hito H3** del Formulario E-25.»

Y el hito H3 del Formulario E-25 de las BA es *«Entrega de la infraestructura híbrida y habilitación de los ambientes de Desarrollo, QA, Preproducción y Producción, con observabilidad operativa»*, **en el mes 6**, con el 10 % de la estructura de pagos.

O sea: la descripción del hito nombra cuatro ambientes, pero el requisito transversal que lo condiciona exige cinco. Aplicando el Art. 5.2 y el Art. 5.4 —que da por aceptada la interpretación más exigente una vez presentada la oferta—, **el ambiente de recuperación ante desastres debe estar habilitado y operativo en el mes 6**, no al pasar a producción.

No es un detalle formal. Significa que la región secundaria, la replicación continua y el procedimiento de conmutación de `RT-07.05` existen y funcionan **diez meses antes** de que la Etapa 1 entre en producción en el mes 16. Una propuesta que planifique el DR para el final del desarrollo incumple H3, que es un hito de pago. Se registra como `F2-ESC-010` para que el Frente 1 y el equipo de planificación lo tomen: el cronograma del Subdocumento 7 depende de esto.

### 3. Matriz de ambientes

| Ambiente | Propósito | Aislamiento | Datos | Topología | Acceso | Despliegue | Retención y limpieza |
|---|---|---|---|---|---|---|---|
| **DEV** | construcción y prueba unitaria | red, cuentas y credenciales propias; **reconstruible íntegramente desde código** | sintéticos; **prohibido dato productivo** salvo anonimización verificable | proporcional, reducida | equipo de desarrollo | integración continua | reconstrucción bajo demanda; apagado fuera de horario (`RT-04.13`) |
| **QA** | funcional, integración, regresión y automatizadas | aislado; **reinicio a estado conocido** | de prueba, controlados y **versionados** | proporcional | QA y automatización | CI/CD | juego de datos versionado; reinicio por ejecución |
| **PREPROD** | aceptación, carga, resiliencia y ensayo del paso a producción | aislado | anonimizados o sintéticos, **volumen representativo** | **equivalente a PROD** en topología, versiones y configuración; toda diferencia que subsista por costo se declara y justifica (`RT-04.02`) | restringido | **igual a PROD**, mismo mecanismo | según ciclo de prueba |
| **PROD** | operación real | aislado; **sin acceso interactivo directo de desarrolladores** | reales | híbrida completa: nube multi-AZ + núcleo local + borde | mínimo privilegio, auditado, con PAM | progresivo, sin interrupción | según las siete retenciones del Maestro §16.1 |
| **DR** | continuidad ante indisponibilidad de la región o del sitio primario | aislado, en región secundaria | réplica continua de PROD | capacidad suficiente para el RTO y el RPO comprometidos | emergencia, con **break-glass auditado** y PAM | automatizable; **ejecutable por el CLIENTE** (`RT-07.05`) | igual a PROD |

**Equivalencia de Preproducción.** `RT-04.02` obliga a que sea equivalente a Producción y a declarar las diferencias que subsistan por costo. Se declara desde ya una diferencia estructural que **no** se puede eliminar: Preproducción no tiene 26 tableros reefer, 2.400 tomas, 42 tractocamiones ni un patio de 18 hectáreas con pilas móviles. La equivalencia se sostiene en topología, versiones y configuración, y el comportamiento del borde se valida con simuladores de dispositivo y con las pruebas de terreno del numeral 11. Decirlo es obligación de `RT-04.02`; ocultarlo sería fingir una equivalencia imposible.

### 4. Entrega continua y gestión de la configuración

| Materia | Compromiso | Código |
|---|---|---|
| Control de versiones | ramas protegidas, **revisión obligatoria por pares** y prohibición de escritura directa sobre la rama principal | `RT-04.03` |
| Trazabilidad | cadena completa requerimiento → incidencia → cambio de código → prueba ejecutada → despliegue | `RT-04.04` |
| Integración continua | compilación, pruebas unitarias, análisis estático, análisis de composición, **escaneo de secretos** y escaneo de imágenes, **con bloqueo automático del despliegue** | `RT-04.05` |
| Despliegue | automatizado y reproducible, con **reversión automatizada y sin intervención manual** en el paso a producción | `RT-04.06` |
| Estrategia sin interrupción | se declara la escogida y **se demuestra en Preproducción antes de cada** paso a producción | `RT-04.07`, BA Art. 24 |
| Configuración | externalizada del artefacto y gestionada por ambiente; **el mismo artefacto se promueve de QA a PREPROD y a PROD sin recompilación** | `RT-04.08` |
| Secretos | gestor con rotación automática y auditoría de acceso; **cero credenciales embebidas** en código, imágenes o configuración | `RT-04.09` |
| Migraciones de esquema | versionadas, reversibles y automatizadas, **con compatibilidad que permita convivir dos versiones de la aplicación durante el despliegue** | `RT-04.10` |
| Cobertura | **≥70 %** en lógica de negocio, con umbral bloqueante en el flujo de integración | `RT-04.11`, `RNF-DES-12` |
| Métricas de entrega | frecuencia de despliegue objetivo, tiempo desde el compromiso de código hasta producción, tasa de cambios fallidos y tiempo de restauración, medidos durante la Operación | `RT-04.12` |
| Infraestructura como código | la totalidad, versionada **en el repositorio del CLIENTE**, revisable y reproducible; sin infraestructura creada por consola | `RT-03.03` |

**Estrategia escogida: despliegue progresivo por zona, con canario.** La razón es del caso, no de moda. El `CP, Cap. 13.3`, condición 4, exige que *«el despliegue debe poder hacerse por proceso o por zona —gate, patio, patio refrigerado, muelle, planificación, facturación, portal de clientes— y no como un único evento que afecte simultáneamente a toda la operación»*. Azul-verde conmuta todo el tráfico a la vez y no respeta esa partición. El progresivo por zona sí, y además permite que la marcha blanca conviva por zona con la operación vigente, que es la condición 1 del mismo numeral.

`RT-04.12` obliga a declarar la **tasa de cambios fallidos**, y el Art. 78.3 de las BA la limita a **no más del 5 % de los despliegues del mes**. El presupuesto de error de `RT-10.09` se ata a esa tasa: si se agota, el ritmo de despliegue se detiene antes que el nivel de servicio.

### 5. Redes y segmentación

El punto de partida es un incidente, no una buena práctica. El `CP, Cap. 6` describe que la red operacional y la administrativa *«comparten infraestructura de conmutación»*, que las 142 cámaras están *«conectadas al mismo backbone que la operación»* y que *«en eventos de alta actividad se ha observado degradación del acceso al sistema de operación»*. La restricción no negociable 6 y el segundo punto de la Declaración Mandatoria ordenan segregar.

| Zona | Contenido | Conductos autorizados hacia otras zonas |
|---|---|---|
| **Operacional** | núcleo local, borde de gate, patio, patio refrigerado y muelle, terminales de equipo | hacia nube por el enlace redundante; hacia administrativa **solo** por conducto controlado y declarado |
| **Administrativa** | estaciones de trabajo, back office, espacio de operación del personal | hacia nube; **sin ruta directa a la operacional** |
| **Protección** | VMS/CCTV del terminal y sistemas del plan ISPS | **ninguna hacia la operacional**; el video no circula por la red operacional |
| **Recinto técnico** | CCTV propio de la sala, control de acceso biométrico, monitoreo ambiental | conducto propio hacia observabilidad; **separado del VMS del terminal** |

Se aplica **IEC 62443** con zonas y conductos, conforme a la Decisión N° 19 y a `STD-20` de la matriz global. La definición fina de conductos, reglas y evidencia es de D1; aquí se fija la topología física que la hace posible.

**Continuidad del VMS y del plan ISPS durante la migración.** El terminal es instalación sujeta al código internacional de protección y operador de importancia vital (restricción 7): *«nada de lo que se implemente puede comprometer el plan de protección aprobado»*. La segregación se ejecuta sin interrupción del VMS: se monta la nueva conmutación operacional en paralelo, se migran los segmentos por zona, y el VMS permanece en su backbone hasta que su propio segmento de protección esté operativo y verificado. Ninguna migración de red se ejecuta durante la atención de una nave. La aprobación de la autoridad para intervenir la red de protección **sigue pendiente** y bloquea esa parte: `F2-ESC-002`.

**Red del patio.** `RT-03.23` exige que la red inalámbrica operacional tenga segmentación por tipo de dispositivo, autenticación por certificado o credencial de empresa y **cobertura verificada mediante estudio de sitio**; el `CP, Cap. 15, RT-03.24` —materia «red de los sitios operacionales», ver la colisión de código en `F2-ESC-006`— exige el rediseño de la red del patio con *«verificación de radiopropagación en condición de patio cargado»*. El `CP, Cap. 13.3`, condición 6, insiste: en patio cargado, no vacío, y considerando que la disposición de las pilas cambia durante el día.

El diseño no promete cobertura perfecta, porque las sombras se mueven cada hora con pilas de hasta cinco alturas. Promete dos cosas verificables: que el terminal de equipo **opera autónomo hasta 8 horas fuera de cobertura sin perder registro** (`RNF-DIS-03`), y que el handover entre celdas no interrumpe una transacción en curso. La cantidad y ubicación de estaciones base **no se fija aquí**: sale del site survey, que es `F2-ESC-001`. La Decisión N° 9 dejó la red celular privada LTE/5G como alternativa primaria sujeta a ese survey; se recoge como candidato de `ADR-006` y no se cierra sin el dato.

**Enlaces hacia el exterior.** `RT-03.17` exige enlace redundante **por caminos físicos y proveedores distintos, con conmutación automática y tiempo de conmutación declarado**; `RT-03.21` exige enlace privado dedicado o VPN cifrada; `RT-06.32` exige que las rutas entren al edificio **por puntos separados**. Hoy hay un proveedor de fibra y un radioenlace de respaldo *«no probado en conmutación real desde 2022»*. El segundo camino es obligación, no mejora. El dato de si el edificio admite dos ingresos físicos sigue abierto: `F2-ESC-008`.

`RT-03.24` del BTT —calidad de servicio— pide declarar la priorización del tráfico operacional crítico frente al administrativo. Se aplica QoS con la confirmación de movimiento y la alarma de frío en la clase de mayor prioridad, y la sincronización diferida y la telemetría histórica en clases inferiores, de modo que la recuperación tras un corte no compita con la operación en curso.


### 5.bis Reconciliación con las zonas y los flujos de D1

`SEC-PHYS-v0.1` propone **nueve zonas** y **once flujos autorizados**. El §5 de este entregable había definido **cuatro zonas**. No se contradicen: están a distinta granularidad y responden a preguntas distintas. Las cuatro de C3 son **dominios de conmutación físicamente segregados**, que es lo que exige la restricción no negociable 6 y lo que se prueba con «cero rutas cruzadas no autorizadas» de `RNF-SEG-06`. Las nueve de D1 son **ámbitos de política**, y su propio texto lo advierte: *«una zona no implica comprar un servidor o firewall por fila»*.

La correspondencia, que a partir de aquí es la vigente para ambos frentes:

| Dominio físico de C3 | Zonas de D1 que aloja | Frontera que se prueba |
|---|---|---|
| **Operacional** | `Z-LOCAL`, `Z-FIELD`, y la parte local de `Z-DATA` | segregación física verificada por prueba de penetración interna |
| **Administrativa** | `Z-ADM` | sin ruta hacia patio, protección ni datos |
| **Protección** | `Z-PROT` | conducto mínimo aprobado por la autoridad; sin video por la red operacional |
| **Recinto técnico** | plano de aplicación de `Z-MGMT` en el sitio | acceso por PAM; CCTV y control de acceso propios del recinto |
| *(en nube, fuera de la conmutación del terminal)* | `Z-EDGE`, `Z-SVC`, y la parte en nube de `Z-DATA` | segmentación de subredes del proveedor (`RT-03.04`) |

`Z-EXT` no tiene dominio físico nuestro: es el origen del tráfico.

**Dos precisiones que el cruce obliga a hacer.**

`Z-MGMT` **atraviesa los cuatro dominios y no es uno más**. Administrar el núcleo local, los conmutadores, la nube y los puestos son accesos a zonas distintas, unificados por un mismo plano de identidad y elevación. Tratarla como un quinto segmento físico crearía una red de administración que cruza la segregación que acabamos de construir. Se materializa como acceso mediado con PAM desde `Z-ADM` hacia cada zona, nunca como ruta directa.

`Z-DATA` **queda repartida** entre nube y sala, y eso es correcto: durante el corte de 72 horas la autoridad del dato pasa al núcleo local (§6 de C1). La política de acceso es la misma en ambos emplazamientos; lo que cambia es quién es la fuente de verdad.

**Los once flujos contra la matriz de conductos.** `FL-01` a `FL-11` de D1 son el detalle lógico de lo que aquí son conductos autorizados. Tres tienen consecuencia física directa sobre este entregable:

| Flujo D1 | Consecuencia para C3 | Dónde queda |
|---|---|---|
| `FL-03` sincronización `Z-LOCAL` ↔ `Z-SVC` | es el conducto que carga los **32,5 Mbps de reposición** tras un corte de 72 h en peak estacional; D1 lo declara con «persistencia local y conciliación ≤90 min» y C4 le pone la cifra | §5 enlaces, C4 §5.1 |
| `FL-07` integración ↔ `Z-PROT` | el conducto hacia VMS y control de acceso **existe y es mínimo**; confirma que la segregación no aísla el plan de protección, que es la condición de la restricción 7 | §5, `F2-ESC-002` |
| `FL-10` servicios → colectores, tiempo y nombres | D1 advierte que *«tiempo, nombres y registros locales no pueden depender solo de nube»*. **Esto no estaba en C3.** Durante las 72 h sin enlace, la resolución de nombres, la sincronización horaria y la validación de certificados tienen que resolverse localmente, o las cinco funciones críticas fallan por una causa que nada tiene que ver con su lógica | §5.ter, nuevo |

### 5.ter Servicios de infraestructura que deben sobrevivir el corte

Es la consecuencia de `FL-10` y del `B3.4` de D1, y es un hueco real que este entregable tenía: se había dimensionado el cómputo, el almacenamiento y el enlace para las 72 horas, pero no los servicios que todo lo demás da por sentados.

| Servicio | Por qué falla si depende de nube | Tratamiento local |
|---|---|---|
| **Resolución de nombres** | los servicios se llaman entre sí por nombre; sin resolución, el núcleo local no se encuentra a sí mismo | resolvedor local autoritativo para la zona operacional, con la vista externa como reenvío opcional |
| **Sincronización horaria** | sin hora común no hay orden de eventos, y la reconciliación determinista tras el corte depende del orden | fuente de tiempo local con al menos dos referencias; el sello de evidencia y la bitácora dependen de esto |
| **Validación de certificados** | si la comprobación de revocación solo se hace en línea, el TLS interno falla al caer el enlace | validación con material local vigente; **prohibido desactivar la validación o aceptar certificados vencidos** durante el corte, como advierte D1, `B3.4` |
| **Identidad y sesión** | una autenticación que consulte a nube convierte el corte de enlace en corte de operación | caché local de `SRV-IAM` con credenciales vigentes; ver C1 §5 |
| **Registro y buffer de seguridad** | los eventos del corte no pueden perderse ni esperar al enlace | colector local con buffer de 72 h más margen; se reenvía al reconectar |

Los cinco se incorporan a la matriz de continuidad del §7 como dependencias de las funciones críticas, y su capacidad —especialmente el buffer del colector— se dimensiona en C4. Ninguno genera fila propia de T-11: son capacidades del núcleo local y de la plataforma de observabilidad ya ofertadas.

### 6. Clasificación de servicios

`RT-10.02` obliga a clasificar cada servicio en crítico, alto, medio o bajo, **justificando con el impacto operacional de su indisponibilidad**, y a aplicarle el nivel del Art. 78° de las BA. La clasificación no es cosmética: fija disponibilidad, tiempo de respuesta, tiempo de resolución y cobertura de atención.

| Servicio | Clase | Impacto de su indisponibilidad | Nivel Art. 78° |
|---|---|---|---|
| Atención de nave y registro de movimientos | **Crítico** | detiene o ciega la operación de muelle; una nave amarrada consume tiempo de muelle desde que amarra | 99,9 % · respuesta 15 min · resolución 4 h · 24×7×365 |
| Gate: prevalidación, entrada y salida | **Crítico** | reproduce la fila de 3,2 km de marzo de 2026, con desborde a vía pública | ídem |
| Posición e inventario de patio | **Crítico** | obliga a búsqueda física, que hoy toma 40 min y es el efecto que el jefe de operaciones advirtió | ídem |
| Monitoreo y alarma de patio refrigerado | **Crítico** | es el modo de falla del 18 de febrero: 38 contenedores perdidos | ídem |
| Captura de hecho y evidencia facturable | **Crítico** | el hecho no se puede reconstruir después del evento (regla negativa 16 del Maestro) | ídem |
| Planificación de estiba y patio | **Alto** | el plan vigente permite operar; se degrada la replanificación | 99,5 % · 1 h · 8 h · 24×7×365 |
| Mensajería con navieras | **Alto** | con alternativa costosa: canal puente y redigitación, prohibido para la alianza desde 2029 | ídem |
| Inspecciones de autoridades | **Alto** | atraso de inspección con costo operacional y de imagen | ídem |
| Portal de autoservicio | **Medio** | existe alternativa: atención asistida, que es lo que se busca eliminar | 99,0 % · 4 h · 24 h · hábil extendido |
| Emisiones y reporte al verificador | **Medio** | no detiene operación; la captura no se interrumpe | ídem |
| Analítica e indicadores del concedente | **Medio** | el dato se acumula; se consolida ≤1 h tras el cierre de turno | ídem |
| Administración y back office | **Bajo** | sin impacto operacional inmediato | 98,0 % · 8 h · 48 h · hábil |

Las cinco críticas son exactamente las cinco funciones que el Maestro §9.1 exige sostener 72 horas sin enlace. No es coincidencia: la clasificación por impacto y la lista de continuidad local convergen porque ambas responden a la misma pregunta.

### 7. Matriz de continuidad

| Servicio o proceso | Clase | HA | Dependencia | RTO | RPO | 72 h local | Fallback manual | Prueba | SPOF residual |
|---|---|---|---|---|---|---|---|---|---|
| Nave y movimientos | crítica | clúster local ≥3 nodos + multi-AZ en nube | núcleo local, borde de muelle | ≤4 h | ≤15 min | **sí, completo** | **ninguno**: la operación continúa localmente sin degradar. Lo que espera es la mensajería EDIFACT, que queda en cola *(A3 §7)* | E2E y DR semestral | sala técnica única, aceptado |
| Gate: entrada y salida | crítica | ídem + gabinete por puesto con proceso local | núcleo local, OCR, báscula, barrera | ≤4 h | ≤15 min | **sí, completo** | carril de excepción de `RN-07`, que **ya existe hoy**; lo que se degrada es solo la verificación contra autoridades externas *(A3 §7)* | corte real de enlace | barrera y báscula del CLIENTE |
| Posición e inventario | crítica | ídem | núcleo local, red de patio, terminales | ≤4 h | ≤15 min | **sí**, con la red de patio operativa | **ninguno**: la posición sigue con DGPS/RTLS y lectura óptica local. Lo que se posterga es la conciliación fina con el TOS *(A3 §7)*. El terminal de equipo aguanta 8 h fuera de cobertura | prueba de campo con desconexión deliberada | red de patio, mitigado |
| Alarma de patio refrigerado | crítica | ídem + concentrador por tablero | núcleo local, 26 concentradores | ≤4 h | ≤15 min | **sí**, alarma local con canal redundante | **ninguno**: alarma y registro continúan localmente. Solo se difiere el reporte agregado a `DATA-AN` *(A3 §7)*. La ronda física cada 4 h queda como reversibilidad de último recurso, no como respaldo del corte | inyección de falla de sensor y de tablero | respaldo eléctrico del patio reefer no verificado |
| Hecho y evidencia facturable | crítica | ídem | núcleo local | ≤4 h | ≤15 min | **sí**, captura y sello diferido | **ninguno**: la evidencia se sella localmente. Se posterga la entrega al ERP y su conciliación 1:1 *(A3 §7)* | conciliación por turno | — |
| Planificación | alta | multi-AZ en nube; plan vigente replicado local | nube | ≤4 h | ≤15 min | plan vigente **sí**; replanificación **no** | planificación manual, que es el estado actual | DR semestral | dependencia de una persona hasta 2028 |
| Mensajería con navieras | alta | multi-AZ; cola durable con acumulación local | nube, contraparte | ≤4 h | ≤15 min | **no**: acumula y entrega al reconectar | canal puente transitorio, prohibido para la alianza desde 2029 | prueba por contraparte | disponibilidad de la contraparte |
| Inspecciones | alta | multi-AZ | nube, autoridad | ≤4 h | ≤15 min | agenda vigente y acta **sí** | coordinación telefónica y acta en papel | DR semestral | interfaz de la autoridad inexistente |
| Portal de autoservicio | media | multi-AZ | nube, borde público | ≤4 h | ≤15 min | **no** | atención asistida | DR semestral | proveedor de nube |
| Emisiones | media | multi-AZ | nube; captura en borde | ≤4 h | ≤15 min | captura **sí**; cálculo **no** | — | DR semestral | — |
| Analítica y concedente | media | multi-AZ | nube | ≤4 h | ≤15 min | **no**; el dato se acumula | — | DR semestral | — |


#### 7.1 Lo que A3 corrigió de esta matriz

Al integrar el `§7` de A3 —«Cinco funciones críticas: qué no está disponible offline y su respaldo manual»— apareció un error de este entregable que conviene dejar escrito, porque va al fondo del diseño.

La columna «fallback manual» de la matriz anterior proponía procedimientos de papel para las cinco funciones críticas: planilla de turno para movimientos, acta en papel para la evidencia. **Eso contradice el propio diseño.** Si el núcleo local sostiene esas cinco funciones durante 72 horas, no hay nada que reemplazar a mano: lo que se degrada no es la función, es su **contraparte externa**.

| Función | Lo que **no** se detiene | Lo que sí espera al enlace |
|---|---|---|
| Nave y movimientos | la operación completa, local | la mensajería EDIFACT con navieras, que queda en cola |
| Posición y cruce de zonas | posición con DGPS/RTLS y lectura óptica | la conciliación fina con el TOS |
| Gate | validación y paso del camión | la verificación contra autoridades externas, que usa el carril de excepción de `RN-07`, **ya existente hoy** |
| Alarma de patio refrigerado | detección, alarma y registro | el reporte agregado a `DATA-AN` |
| Hecho y evidencia facturable | captura y sellado local | la entrega al ERP y su conciliación 1:1 |

Escribir «planilla de turno» como respaldo daba a entender que la función cae, y es exactamente lo contrario de lo que se está ofertando. Corregido en la matriz del §7.

**Lo que sí se degrada por diseño**, declarado por A3 y que este entregable debe reflejar en el calendario y en la capacidad: planificación, inspecciones, emisiones, analítica, alta de identidad nueva y el catálogo central del gateway. Para la planificación el respaldo es el plan impreso y la radio, que es el modo degradado explícito de la Decisión N° 1. Esa declaración es el **entregable N° 4 del checklist del BTT** (`RT-03.13`), cuya ausencia el propio requisito califica de «observación grave», y ahora existe: la produce A3 y este entregable la respalda con la infraestructura que la hace posible.

#### 7.2 Autoridad por bloque de patio, no por sistema completo

La matriz `dominio × zona × fase` de A3 §3 introduce algo con consecuencia física directa: el núcleo de registro —gate, posición, movimientos y salida— **se sustituye como un solo contexto acotado pero se despliega bloque por bloque del patio**, nunca de una vez.

Tres consecuencias para este frente:

`PHY-OPS-03`, la capa anticorrupción, **debe sostener autoridad diferenciada por bloque simultáneamente**: bloques pre-cutover donde manda el TOS, bloques en validación donde el sistema nuevo solo lee, y bloques post-cutover donde manda el nuevo. No es un interruptor, es un estado por zona.

**Post-cutover hay escritura dual hacia el TOS**, para conservar la posibilidad de retorno. Es decir, el TOS sigue recibiendo tráfico después de perder la autoridad, y ese tráfico se suma al dimensionamiento de `PHY-OPS-03`. A2 confirma que el TOS cursa *«todo el tráfico transaccional, ~0,27 TPS peak»*, coherente con `DIM-02` de C4.

**El retorno se ejecuta por redirección de enrutamiento en la fachada**, con doble control y break-glass. Eso lo hace una operación de configuración, no de restauración de datos — y por lo tanto compatible con la restricción de no detener la operación.


### 8. Comportamiento ante dependencia externa degradada

`RT-10.08` obliga a documentar, **por cada dependencia externa**, qué hace la solución cuando no responde, responde con error o responde con lentitud. Se declara el patrón general y las excepciones; el detalle por contraparte es de A2.

| Dependencia | No responde | Responde con error | Responde con lentitud |
|---|---|---|---|
| Nube, desde el terminal | núcleo local asume autoridad del dato; operación completa 72 h | reintento con retroceso y variación; cola local | corta circuito y pasa a modo local antes de degradar la operación |
| `EXT-TOS12` | cola y conciliación diferida; se declara divergencia | escritura parcial detectada y marcada para investigación | cortacircuitos; no se bloquea el movimiento físico |
| `EXT-ERP` | hecho facturable se acumula con evidencia; nada se pierde | objeción registrada con causa | ídem |
| Naviera | mensaje en cola durable con DLQ | informe de error a la contraparte | ídem |
| Autoridad | canal asistido trazable con expediente | ídem | ídem |
| `EXT-GRU` control de grúas | el movimiento se registra por la cadena de patio, no por el fabricante | ídem | ídem |
| Báscula, OCR, barrera | carril de excepción **al menos 50 % más lento** que el validado, para que la excepción no se vuelva la norma | ídem | ídem |

El principio, de `RT-02.09`, es que la solución degrada de forma elegante, informa la degradación a la persona usuaria y **nunca falla de forma silenciosa**.

### 9. Plan de recuperación ante desastres y política de respaldo

Entregable N° 9 del checklist del BTT, Cap. C, que no tenía producto asignado hasta la corrección `F2-COR-003`. La especificación técnica del sitio secundario está en C2 §6; aquí va el procedimiento.

**Criterio de activación.** Indisponibilidad de la región primaria, o del sitio primario, que exceda el tiempo de tolerancia declarado sin recuperación a la vista. La conmutación se declara conforme a `RT-07.08` con criterio de disparo explícito y **protección contra conmutación innecesaria**: un corte del enlace hacia la nube **no** activa el DR, porque para eso está la operación local de 72 horas. Confundir ambos escenarios sería el error más caro posible en este terminal.

**Ejecución.** Documentada, automatizada en la mayor medida posible y **ejecutable por el personal del CLIENTE** tras la transferencia de conocimiento (`RT-07.05`). Con un área TI de cinco personas y turnos 24×7, el procedimiento se escribe para ser ejecutado a las tres de la mañana por quien esté de turno, no por un especialista del ADJUDICATARIO. Ese es el criterio de aceptación del procedimiento.

**Retorno.** Procedimiento documentado y probado de vuelta al sitio principal, **con reconciliación de los datos generados durante la contingencia** (`RT-07.06`). El retorno es tan obligatorio como la ida y se prueba en la misma ejecución.

**Prueba.** Conmutación real **al menos dos veces al año** (`RT-07.07`, Art. 20 de las BA, `RNF-DIS-15`), con informe, medición del RTO y RPO **efectivamente alcanzados** —no los comprometidos— y plan de corrección de brechas.

> **Tensión de calendario que se declara, no se resuelve aquí.** Dos conmutaciones reales al año deben caber en los siete meses no congelados, fuera de la atención de nave y sus cuatro horas previas, con aviso previo de diez días hábiles (`RT-10.05`, Art. 20 de las BA). Es factible, pero el calendario concreto depende de la programación de atraque, que no tenemos. Se propone fijar las pruebas en mayo y en octubre, sujeto a esa programación, y se registra como dependencia.

**Política de respaldo.** Esquema **3-2-1-1-0**, cifrado en reposo y en tránsito con clave gestionada de forma independiente de la infraestructura respaldada, copias inmutables protegidas contra borrado **incluso frente a credenciales administrativas comprometidas**, prueba de restauración **mensual** documentada sobre muestra representativa con medición del tiempo efectivo, y declaración **por dominio de dato** de frecuencia, retención y tiempo estimado de restauración completa (`RT-07.09` a `RT-07.13`). La tabla por dominio se cruza con las siete retenciones del Maestro §16.1 y se completa con los volúmenes de C4.

### 10. Plan de continuidad del negocio

Entregable N° 12 del checklist, exigido por `RT-10.03` conforme a **ISO 22301**, y articulado con la continuidad TIC de **ISO/IEC 27031** por `RT-10.04`. Tampoco tenía producto asignado antes de `F2-COR-003`.

Contiene análisis de impacto en el negocio sobre los procesos del `CP, Cap. 4`; escenarios de contingencia —corte de enlace exterior, indisponibilidad de región, falla de la sala técnica, corte eléctrico del patio refrigerado, indisponibilidad del TOS 2012, pérdida de la red de patio—; **procedimientos manuales de respaldo** para cada uno, que en varios casos son la forma de trabajar actual del terminal y por eso existen y son enseñables; y criterios de activación y de vuelta a la normalidad.

Un dato del caso que el plan debe incorporar y que no es nuestro: el respaldo eléctrico del patio refrigerado *«nunca ha sido verificado a carga total de temporada»* (`CP, Cap. 6`). Es `F2-SPOF-05` de C1, queda fuera del límite de la oferta, y el plan de continuidad especifica la prueba y escala la ejecución al CLIENTE.

### 11. Plan de pruebas

| Prueba | Qué demuestra | Cuándo | Origen |
|---|---|---|---|
| **Radiopropagación en patio cargado** | cobertura con pilas reales y su geometría cambiante, movilidad y handover sin interrumpir transacción | site survey y antes del paso a producción de patio | `RT-03.23`, `CP, Cap. 15, RT-03.24`, `RNF-DIS-11` |
| **Corte real de fibra** | conmutación automática al segundo camino, **sin pérdida transaccional**, con tiempo medido | antes de producción y semestral | `RT-03.17`, `RNF-DIS-11` |
| **Corte real de radioenlace** | el respaldo que no se prueba desde 2022 funciona | ídem | `CP, Cap. 6` |
| **Desconexión de 72 h** | las cinco funciones críticas operan completas sin enlace exterior | antes de producción | `CP, Cap. 15, RT-03.10`, `RNF-DIS-02` |
| **Reconexión y sincronización** | ≤90 min tras 72 h, automática, sin pérdida, con conflictos deterministas y bitácora | ídem | `CP, Cap. 15, RT-03.13`, `RNF-DIS-04` |
| **Terminal fuera de cobertura** | ≥8 h continuas sin pérdida de registro de movimientos | ídem | `RNF-DIS-03` |
| **Carga y estrés a 1,5× el peak** | umbrales sostenidos bajo carga amplificada y **punto de quiebre identificado** | antes de cada paso a producción | `RT-04`, BA Art. 24, `RNF-DES-12` |
| **Inyección de fallas** | caída de instancia, de zona, de dependencia externa, latencia elevada y saturación de disco | antes de cada paso a producción y **semestral en Operación** | `RT-10.07`, `RNF-DIS-06` |
| **Conmutación DR real y retorno** | RTO y RPO efectivamente alcanzados, ejecutados por el CLIENTE | **dos veces al año** | `RT-07.07`, `RT-07.05`, `RT-07.06` |
| **Restauración desde respaldo** | tiempo efectivo sobre muestra representativa | **mensual** | `RT-07.12` |
| **Segregación de red** | cero rutas cruzadas no autorizadas entre operacional, administrativa y protección | tras la migración y periódicamente | `RNF-SEG-06`, `STD-20` |
| **Continuidad del VMS durante la migración** | el plan de protección no se degrada en ningún momento | durante la segregación | restricción 7, `MC-02` |
| **Despliegue sin interrupción** | azul-verde, canario o progresivo demostrado en Preproducción | **antes de cada** paso a producción | `RT-04.07` |
| **Retorno de intervención** | la reversión funciona y está cronometrada | por cada intervención | `RT-04.06`, `MC-27` |

### 12. Calendario de intervención y retorno

**Regla de partición.** La intervención de **software** no consume ventana: se libera sin interrupción, por zona, con canario y reversión automatizada, en cualquier momento salvo durante la atención de una nave. La intervención **física** —conmutación de red, red de patio, 26 concentradores en tableros energizados, gabinetes, canalizaciones, sala técnica— sí consume ventana y compite con las naves y con el congelamiento.

**Ventanas disponibles para intervención física.** Mayo a noviembre, que el `CP, Cap. 13.2` describe como *«única ventana razonable para intervención mayor»*, advirtiendo que **no es una ventana de detención**: el terminal sigue operando 24×7. Fuera de la atención de nave y de las cuatro horas previas a una ventana confirmada. Con aviso previo mínimo de **diez días hábiles** (`RT-10.05`, Art. 20 de las BA). Nunca entre el 15 de diciembre y el 30 de abril, y nunca sobre el patio refrigerado entre enero y marzo, cuando se concentra el 62 % del volumen refrigerado.

**Hitos que ordenan el calendario.**

| Hito | Mes | Consecuencia para este frente |
|---|---|---|
| `H3` — infraestructura híbrida y **los cinco ambientes** operativos | **6** | incluye DR operativo; ver `F2-ESC-010` |
| Toda intervención invasiva instalada, migrada, probada, con retorno y capacitación | **14-dic-2027** | es el límite duro de la obra física; Maestro §13 |
| Congelamiento | 15-dic a 30-abr | solo sombra de solo lectura si el CLIENTE la autoriza formalmente; hoy **no autorizada**, `ESC-03` |
| Producción Etapa 1 | 16 | tras tres meses de marcha blanca con plan de reversión activo |

**Retorno: los ocho campos.** El Maestro §12 exige que toda intervención de software, red, firmware, infraestructura, instrumentación o migración registre: objetivo y alcance; ejecutor y responsable de retorno; disparador; pasos y dependencias; **tiempo máximo**; prueba y evidencia; ventana y contraste con congelamiento y nave; y conciliación y cierre. Se adopta como formulario obligatorio de cada intervención, coherente con `RNF-DIS-12`, que exige que el plan de retorno exista **antes** de ejecutar.

**Estabilización.** El `CP, Cap. 13.3`, condición 8, exige dotación y duración declaradas y **presencia en terreno en los tres turnos, incluida la madrugada**, con habilitación ISPS. El modelo de operación lo dimensiona; se declara aquí porque condiciona el espacio de operación de `PHY-OPS-06` y las cantidades de C4.

### 13. Aportes a ADR y a T-11

**`ADR-006` — red del patio y conectividad redundante.** Alternativas: red inalámbrica empresarial redensificada sobre postación nueva; **red celular privada LTE/5G**, que la Decisión N° 9 dejó como alternativa primaria; o esquema mixto por zona. Criterios: comportamiento con pilas de hasta cinco alturas y sombras móviles, handover sin interrumpir transacción, cantidad de puntos de instalación en ambiente salino y su reposición, operabilidad con TI de cinco personas, y plazo de instalación dentro de la ventana mayo–noviembre antes del 14-dic-2027. **No se cierra sin el site survey** (`F2-ESC-001`).

**`ADR-007` — almacenamiento, RAID, HA y DR.** Aporta desde aquí la modalidad activo-pasivo justificada en C2 §6, el criterio de activación que separa corte de enlace de desastre, y los objetivos RTO 4 h y RPO 15 min. El nivel RAID se justifica en C4 frente a alternativas, como exige `RT-03.14`.

**Candidatos de T-11 propios de C3**, sin precios y con cantidad en C4: segundo camino de comunicaciones hacia la nube por proveedor distinto; enlace privado o VPN cifrada; equipamiento de la red operacional del patio, en rango sujeto a site survey; plataforma de integración y entrega continua y gestor de secretos; y el servicio de custodia y verificación de restauración. Los componentes de red de núcleo y cortafuegos ya están en el catálogo de C2 y **no se duplican**.

### 14. Definición de terminado — estado

- [x] Cinco ambientes explícitos y aislados, con la equivalencia de Preproducción declarada y sus diferencias justificadas.
- [x] Red de patio: se valida en condición real; la ubicación queda sujeta a site survey.
- [x] VMS no se degrada durante la segmentación; el plan de protección se preserva.
- [x] RTO, RPO, DR, respaldo y restauración tienen prueba, periodicidad y criterio de activación.
- [x] 72 h y 90 min están trazados a `RNF-DIS-02` y `RNF-DIS-04`; el dimensionamiento es de C4.
- [x] No se programa intervención prohibida; la partición software/física lo hace verificable.
- [x] Clasificación de servicios con impacto justificado y nivel del Art. 78°.
- [x] Declaración de funciones no disponibles en modo desconectado, checklist N° 4 del BTT — la produce A3 §7; §7.1 corrige la matriz contra ella y aporta la infraestructura que la sostiene.
- [x] Autoridad por bloque de patio integrada desde A3 §3 — §7.2.
- [ ] `TRZ_C3.md` completo — en curso.
- [ ] Buffer de 72 h, sincronización y capacidad de los ambientes — dependen de C4.
- [x] Conductos y reglas de segmentación — §5.bis: cuatro dominios físicos reconciliados con las nueve zonas de D1 y los once flujos.
- [x] Servicios de infraestructura que sobreviven el corte — §5.ter, hueco detectado al cruzar `FL-10`.
- [ ] Calendario de conmutaciones DR — depende de la programación de atraque, dato del CLIENTE.
- [ ] Vista de despliegue y red — en el pase final de diagramas.

## Trazabilidad

Ver [`trazabilidad/TRZ_C3.md`](trazabilidad/TRZ_C3.md).

