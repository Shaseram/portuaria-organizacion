# Base obligatoria para construir el Subdocumento 4

**Estado:** `GUÍA DE CONTENIDO — NO ES REDACCIÓN FINAL`

**Propósito:** dejar ordenado lo que el Subdocumento 4 debe representar sí o sí, qué decisiones ya están alineadas entre Célula 3 y Célula 4, y dónde debe leer el equipo antes de escribir.

**Commit base de la alineación:** `9b460ad9faf6876b677564bcbd884ec1fc22e58e` (`main`).

Esta guía no fija el estilo final, no construye diagramas, no aprueba ADR y no reemplaza las fuentes técnicas. Los bosquejos son orientativos y pueden cambiar durante la escritura.

---

## 1. Cómo usar esta guía

1. Respetar primero los apartados oficiales de 4.1 y 4.2.
2. Usar los mínimos de esta guía como lista de cobertura, no como texto para copiar literalmente.
3. Leer la fuente C3 indicada antes de redactar cada apartado.
4. Consultar Célula 4 solamente en datos, persistencia, calidad, retención, capacidad acumulada y dependencias cruzadas.
5. Explicar la propuesta en lenguaje natural. Los códigos internos sirven para volver a la evidencia, no para llenar el cuerpo de la entrega.
6. Mantener visible qué está propuesto, qué está condicionado y qué solo podrá probarse después.
7. Preparar los diagramas definitivos únicamente cuando el texto esté estabilizado y el equipo haya decidido su forma.

Si una afirmación de esta guía entra en conflicto con una fuente oficial, prevalece la fuente oficial. Si dos documentos internos discrepan, revisar el [plan maestro de alineación](../../PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md) antes de cambiar la baseline.

---

## 2. Estructura contractual que debe conservarse

El Subdocumento 4 representa el 32 % del Informe 1: 16 % para arquitectura lógica y 16 % para arquitectura física.

| Apartado oficial | Contenido exigido |
|---|---|
| `4.1 a)` | Esquema de solución |
| `4.1 b)` | Arquitectura lógica de la solución |
| `4.2 a)` | Arquitectura física de la solución |
| `4.2 b)` | Especificaciones de tecnologías de software a utilizar |
| `4.2 c)` | Especificaciones de implementos a proveer, hardware y software |
| `4.2 d)` | Especificaciones del Data Center primario |
| `4.2 e)` | Especificaciones del Data Center secundario |
| `4.2` | Formulario T-11 |

### Relación con las trece subsecciones de trabajo

Las trece subsecciones del consolidado son un mapa interno; no constituyen trece exigencias contractuales separadas. Al redactar se agrupan así:

| Mapa interno existente | Apartado oficial de destino |
|---|---|
| `4.1.1` | `4.1 a) Esquema de solución` |
| `4.1.2`, `4.1.3`, `4.1.4` y `4.1.5` | `4.1 b) Arquitectura lógica de la solución` |
| `4.2.1`, más redes/continuidad y capacidad de `4.2.6/4.2.7` | `4.2 a) Arquitectura física de la solución` |
| `4.2.2` | `4.2 b) Tecnologías de software` |
| `4.2.3` | `4.2 c) Implementos a proveer` |
| `4.2.4` | `4.2 d) Data Center primario` |
| `4.2.5` | `4.2 e) Data Center secundario` |
| `4.2.8` | Formulario T-11 |

El equipo puede usar subtítulos naturales dentro de esos apartados, pero no debe alterar ni ocultar los encabezados evaluados.

---

## 3. Reglas obligatorias de representación

### 3.1 Tres piezas diferentes

El documento debe distinguir claramente:

1. **Esquema de solución:** quién participa, por qué canales y cuál es la frontera de TERABYTE.
2. **Arquitectura lógica:** qué módulos y capas existen, de qué se responsabilizan y cómo se relacionan.
3. **Arquitectura física:** dónde se ejecuta cada capacidad, cómo se conecta y cómo continúa o se recupera ante fallas.

Una vista no debe ser la misma imagen con otro título. Tampoco se debe repetir en 4.1 el alcance completo que corresponde al Subdocumento 3.

### 3.2 Solución propia del Caso 06

La arquitectura debe mostrar elementos reales del caso: nave, movimientos, gate, patio, reefers, muelle, planificación, facturación, inspecciones, emisiones, TOS 2012, ERP, navieras, autoridades, ferrocarril, concesionaria, básculas, OCR, barreras, CCTV/VMS y dispositivos de terreno.

No cumple una lámina genérica de “usuarios, aplicación y base de datos” a la que solo se le cambió el nombre.

### 3.3 Carácter híbrido

No basta escribir “arquitectura híbrida”. Debe verse y explicarse:

- qué carga vive normalmente en AWS;
- qué capacidades existen físicamente en el terminal;
- qué funciones siguen operando sin conectividad externa;
- qué datos se conservan localmente;
- cómo se devuelve la autoridad y se reconcilia el estado;
- cómo se recupera la plataforma ante un desastre distinto de una caída de WAN.

### 3.4 Lenguaje para el evaluador

En el texto entregable usar nombres como “portal”, “aplicación móvil”, “servicios operacionales”, “plataforma de integración”, “datos transaccionales”, “evidencias”, “núcleo operacional local”, “zona de terreno” y “plataforma de observabilidad”.

Los identificadores `CTX-*`, `DATA-*`, `PHY-*`, `SEC-*`, `SPOF-*` y similares permanecen en el expediente. Solo se incluyen en el documento final cuando sean necesarios para una tabla de correspondencia o para eliminar una ambigüedad.

---

## 4. Baseline alineada que debe aparecer

Estas definiciones ya están conciliadas entre C3 y C4. No deben cambiarse durante la escritura salvo nueva evidencia oficial o instrucción expresa del equipo.

| Tema | Definición que debe representarse | Estado |
|---|---|---|
| Arquitectura general | Plataforma híbrida: servicios principales en AWS y núcleo operacional local en el terminal. | Propuesta de Informe 1 |
| Operación normal | AWS `sa-east-1`, en al menos dos zonas de disponibilidad, mantiene la carga principal y el registro consolidado. | Propuesta |
| Núcleo local | Ejecuta la ruta operacional crítica; no es solo un puente, una copia pasiva ni una réplica completa de toda la nube. | Propuesta |
| Corte de conectividad | La autoridad de las funciones críticas pasa temporalmente al núcleo local, sin dos escritores simultáneos. | Propuesta |
| Continuidad local | Atención de nave, movimientos, gate, reefers y hechos facturables continúan hasta 72 horas sin enlace exterior. | Exigible del caso |
| Retorno | Sincronización automática y reconciliación determinista en hasta 90 minutos, con bitácora y sin pérdida. | Exigible; objetos pesados conservan condición técnica explícita |
| Dispositivos móviles de patio | Conservan hasta 8 horas de trabajo fuera de cobertura sin perder registros. | Exigible del caso |
| Recuperación ante desastre | AWS `us-east-1`, activo-pasivo, con RTO de hasta 4 horas y RPO de hasta 15 minutos. | Baseline propuesta |
| Conectividad externa | Dos enlaces WAN con proveedores, rutas físicas e ingresos distintos; capacidad propuesta de al menos 35 Mbps disponibles por camino. | Baseline; medición pendiente |
| Red de terreno | LTE/5G privada para gate, patio, reefers y muelle, sujeta a levantamiento y prueba de radiopropagación con patio cargado. | Propuesta condicionada |
| Tercer enlace | No forma parte de la baseline ni del T-11. | Excluido |
| Módulos | Operaciones, nave, patio, gate, reefers, planificación, facturación, inspecciones, emisiones y notificaciones, más integración, identidad, evidencia y observabilidad. | Propuesta |
| Datos | Cuatro capacidades lógicas: transaccional, temporal, documental/evidencia y analítica; dos familias principales de persistencia: PostgreSQL/temporal y objetos. | Alineado con C4 |
| Conceptos centrales | `Contenedor` es el maestro; `VisitaContenedor` representa su estadía; `Recalada` o `VisitaNave` representa la estadía de una nave. | Alineado con C4 |
| Integraciones | TOS, ERP, navieras, autoridades, ferrocarril, concesionaria, sistemas de protección y dispositivos se conectan mediante contratos y mecanismos gobernados. | Diseño I1; contratos reales condicionados |
| Seguridad | Acceso de mínimo privilegio, identidad disponible localmente, cifrado, evidencias, segmentación y observabilidad común para nube y terminal. | Propuesta |
| Capacidad del corte | 13,7 GB promedio; 21,9 GB en peak estacional. | Baseline I1 |
| Reposición | 20,3 Mbps promedio; 32,5 Mbps en peak; la baseline WAN se fija en al menos 35 Mbps disponibles. | Baseline I1 |
| Crecimiento | 39 GB y 57,8 Mbps corresponden al escenario futuro de crecimiento 3×, no al compromiso inicial. | Escenario futuro |
| ADR | Once decisiones en estado `PROPUESTO`; ninguna `APROBADO`. | Estado vigente |
| T-11 | 32 filas, cinco columnas oficiales y sin precios. | Base preparada; ensamblado pendiente |

Fuentes de control: [README C3](../README.md), [plan de alineación](../../PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md), [arquitectura lógica A1](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md), [arquitectura física C1](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md), [continuidad C3](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md), [capacidad C4](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) y [contenido canónico de Célula 4](../../Célula%204/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md).

---

## 5. Contenido mínimo por apartado oficial

### 5.1 `4.1 a) Esquema de solución`

**Debe responder:** quién usa la solución, por qué canales, cuál es su propósito y dónde termina la responsabilidad de TERABYTE.

**Debe incluir sí o sí:**

- actores internos y externos agrupados de forma comprensible;
- portal, aplicación móvil y vistas de terreno/cabina;
- frontera de TERABYTE;
- sistemas del CLIENTE que se conservan;
- contrapartes externas principales;
- relación visible con gate, patio, reefers y muelle;
- una frase que conecte el problema con la estrategia de solución sin repetir el Subdocumento 3.

**No debe hacer:** explicar todavía regiones, nodos, subredes, productos, cantidades o mecanismos detallados de integración.

**Fuentes:** [A1 §§1–1.5](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) y, para evitar contradicción de alcance, el Subdocumento 3 de la célula responsable.

### 5.2 `4.1 b) Arquitectura lógica de la solución`

**Debe responder:** qué responsabilidades existen dentro de la plataforma y cómo colaboran para ejecutar los procesos portuarios.

**Debe incluir sí o sí:**

- ocho capas comprensibles: canales, borde público, acceso a servicios, negocio, integración, datos, seguridad y observabilidad;
- módulos operacionales y responsabilidad de cada uno;
- límites de contexto y regla de que los canales no acceden directamente a los datos;
- integración con TOS 2012 y convivencia por etapas;
- contratos, eventos, colas, idempotencia, reintentos y tratamiento de una contraparte caída;
- autoridad del dato durante operación normal, corte y retorno;
- modelo de datos a nivel arquitectónico, sin copiar el diccionario de C4;
- identidad, permisos, cifrado, evidencia y telemetría;
- puntos únicos de falla relevantes y su tratamiento;
- alternativas consideradas y estado propuesto de las decisiones.

**No debe hacer:** copiar las 80 entidades, los 451 atributos, las 73 amenazas, los 26 SPOF o las 31 filas de controles.

**Fuentes C3:** [A1 §§2–7](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md), [A2 §§1–7](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md), [A3 §§2–10](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md), [D1](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md), [D2](../03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) y [registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md).

**Aporte C4:** [contenido canónico del Subdocumento 5](../../Célula%204/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md), [modelo conceptual A01](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A01_MODELO_CONCEPTUAL_DATOS.md), [diccionario A02](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A02_DICCIONARIO_DE_DATOS.md) y [registro de decisiones A00](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A00_REGISTRO_DECISIONES_CELULA4.md).

### 5.3 `4.2 a) Arquitectura física de la solución`

**Debe responder:** dónde se ejecuta cada capacidad y por qué esa ubicación es correcta para el puerto.

**Debe incluir sí o sí:**

- AWS `sa-east-1` como región cloud de carga principal, en al menos dos zonas de disponibilidad;
- núcleo local y sala técnica del terminal;
- equipos de borde en gate, patio, reefers y muelle;
- AWS `us-east-1` como región secundaria de recuperación;
- sistemas del CLIENTE que permanecen fuera de TERABYTE;
- dos enlaces WAN y la red LTE/5G privada;
- zonas operacional, administrativa y de protección segregadas;
- ubicación justificada componente por componente según latencia, continuidad, volumen, seguridad, conectividad, acoplamiento físico y TCO cualitativo;
- cinco ambientes: desarrollo, QA, preproducción equivalente, producción y DR;
- operación normal, corte de 72 horas, reconciliación en hasta 90 minutos y recuperación ante desastre como escenarios diferentes;
- capacidad, redundancia, respaldo y crecimiento.

**No debe hacer:** presentar otro rack en el mismo recinto como sitio secundario ni afirmar que la ubicación por sí sola garantiza continuidad.

**Fuentes:** [C1 §§1–9](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md), [C3 §§2–12](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md), [C4 §§3–10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) y [D1 B3/B5](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md).

**Aporte C4:** capacidad y persistencia en [Subdocumento 5](../../Célula%204/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md) y [A08](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A08_ALMACENAMIENTO_ACUMULADO.md).

### 5.4 `4.2 b) Tecnologías de software a utilizar`

**Debe responder:** qué familias tecnológicas se proponen, para qué sirven, dónde se ejecutan y cómo se evita depender de versiones obsoletas.

**Debe incluir sí o sí:**

- frontend web, aplicación móvil y backend;
- contratos de API y mensajería;
- persistencia transaccional, temporal, documental y analítica;
- contenedores, infraestructura como código y automatización de despliegue;
- identidad, observabilidad y seguridad;
- producto o tecnología de referencia, alternativa equivalente, modalidad y ubicación;
- versión soportada o política de vigencia y fin de soporte;
- portabilidad y mitigación del bloqueo por proveedor.

**No debe hacer:** convertir una marca de referencia en producto contratado o aprobado.

**Fuente:** [C2 §§3–4 y §10](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md).

### 5.5 `4.2 c) Implementos a proveer — hardware y software`

**Debe responder:** qué elementos necesita la propuesta, cuántos, dónde se ubican y qué cálculo o requisito justifica cada cantidad.

**Debe incluir sí o sí:**

- cómputo, almacenamiento y red local;
- gabinetes y equipos de gate, patio, reefers y muelle;
- características ambientales para atmósfera marina, grado IP y anticorrosión;
- referencias de marca/modelo o equivalente cuando las bases lo exijan;
- procesador, memoria, almacenamiento, interfaces y consumo donde corresponda;
- licencias, suscripciones y servicios técnicos necesarios;
- cantidades sin precios ni costos unitarios;
- relación uno a uno con el T-11.

**Fuentes:** [C2 §§7–9](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C4 §§6 y 9–10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md), [T-11 trazable](01_T11_TRABAJO_TRAZABLE.md) y [T-11 final](02_FORMULARIO_T11_FINAL.md).

### 5.6 `4.2 d) Data Center primario`

**Debe responder:** cómo se habilita o reemplaza la sala técnica principal del terminal para sostener la infraestructura local.

**Debe incluir sí o sí:**

- sala existente de 34 m² como alternativa condicionada, no como recinto ya conforme;
- tres puertas de validación: exclusividad/acceso, capacidad física y factibilidad técnica;
- alternativa compacta de reemplazo si la sala no supera esas puertas;
- distribución de racks, separación de comunicaciones, energía, UPS, generación, climatización, incendio, acceso, CCTV y monitoreo;
- carga eléctrica, factor de potencia, PUE y margen;
- condiciones marinas y mantenimiento;
- dependencia de levantamiento en terreno y fichas reales.

**Aclaración de nombres:** “Data Center primario” en este apartado se refiere al **site o sala técnica principal on-premise** exigida por las bases. No significa que toda la aplicación tenga su registro normal allí. La **región cloud primaria** continúa siendo AWS `sa-east-1`.

**Fuentes:** [C2 §5](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C1 §7](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md), [C4 §6](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) y ADR-005/007 en el [registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md).

### 5.7 `4.2 e) Data Center secundario`

**Debe responder:** cómo se recupera la plataforma ante un desastre del sitio o región y cómo se retorna después.

**Debe incluir sí o sí:**

- AWS `us-east-1` como región secundaria activo-pasiva;
- alcance de la réplica de datos críticos y objetos;
- infraestructura como código para reconstrucción;
- copias inmutables y autoridad separada;
- RTO de hasta 4 horas y RPO de hasta 15 minutos;
- activación, validación, failback y pruebas futuras;
- riesgo de proveedor común AWS y medidas de portabilidad;
- diferencia entre segunda zona de disponibilidad, alta disponibilidad local y región secundaria.

**No debe hacer:** confundir DR con la pérdida de los enlaces WAN. La caída de WAN la resuelve primero el núcleo local de 72 horas.

**Fuentes:** [C2 §6](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C3 §9](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md) y ADR-007/011 en el [registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md).

### 5.8 Formulario T-11

**Debe responder:** qué se propone, qué producto o servicio de referencia se asocia, dónde se ubica, qué cantidad se requiere y por qué.

**Debe incluir sí o sí:**

- exactamente las cinco columnas oficiales;
- las 32 filas consolidadas;
- cantidades y justificación técnica;
- coherencia con componentes, ubicaciones y cálculos;
- cero precios, tarifas o costos unitarios;
- tecnologías como referencias o equivalentes, sin fingir contratación.

**Fuentes:** [T-11 final](02_FORMULARIO_T11_FINAL.md), [T-11 trazable](01_T11_TRABAJO_TRAZABLE.md), [C2 §§7–9](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) y [C4 §§6–10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).

---

## 6. Bosquejos conceptuales — no son diagramas finales

Estos bosquejos indican qué relaciones deben poder entenderse. No fijan cajas, colores, cantidades de figuras ni diseño gráfico.

### 6.1 Bosquejo del esquema de solución

> Actores internos y externos → portal / aplicación móvil / vistas de terreno → plataforma TERABYTE → TOS, ERP, navieras, autoridades, ferrocarril, concesionaria y dispositivos.

Debe distinguir la frontera de TERABYTE de los sistemas conservados y mostrar que gate, patio, reefers y muelle participan en la solución.

### 6.2 Bosquejo de arquitectura lógica

> Canales → protección de acceso → servicios de entrada → módulos operacionales → integración y datos.
>
> Identidad, evidencia, seguridad y observabilidad actúan de forma transversal.

Debe permitir entender cada capa y módulo sin depender de códigos internos. El corte de conectividad cambia la autoridad, pero no crea una segunda arquitectura de negocio.

### 6.3 Bosquejo de arquitectura física híbrida

> Terminal: sala técnica + gate + patio + reefers + muelle
>
> Terminal ⇄ dos enlaces WAN independientes ⇄ AWS primaria `sa-east-1`
>
> AWS primaria → réplica/recuperación activo-pasiva en `us-east-1`

Debe mostrar que el terminal puede operar durante 72 horas sin AWS, que la nube sigue siendo la carga principal durante el régimen normal y que DR es distinto de una pérdida de conectividad.

---

## 7. Ruta de lectura para redactar sin perderse

### Lectura inicial obligatoria

1. [README de Célula 3](../README.md).
2. [Plan maestro de alineación C3–C4](../../PLAN_MAESTRO_ALINEACION_CELULA3_CELULA4.md).
3. Esta guía.
4. [Base técnica del Subdocumento 4](00_BASE_TECNICA_SUBDOCUMENTO_4.md), usada como inventario de ideas, no como prosa final.

### Lectura integral recomendada para el redactor principal

La ruta por apartado permite dividir el trabajo, pero no sustituye una lectura completa antes de cerrar el texto. El redactor o integrador principal debe seguir este orden:

1. **Gobierno y decisiones:** README, plan de alineación, esta guía, [registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md) y [MA-6](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md).
2. **Arquitectura lógica:** [A1](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md), [A2](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md) y [A3](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md), en ese orden.
3. **Arquitectura física:** [C1](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md), [C2](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C3](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md) y [C4](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).
4. **Seguridad y control:** [D1](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md), [D2](../03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) y finalmente [D3](../03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md).
5. **Cruce con datos:** [contenido canónico de C4](../../Célula%204/Subdocumento_5/CONTENIDO_SUBDOCUMENTO_5.md) y luego A00–A08 solo para el detalle que corresponda. Priorizar [A00](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A00_REGISTRO_DECISIONES_CELULA4.md), [A01](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A01_MODELO_CONCEPTUAL_DATOS.md), [A02](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A02_DICCIONARIO_DE_DATOS.md), [A03](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A03_CALIDAD_ISO25012.md) y [A08](../../Célula%204/Subdocumento_5/Documentos_de_trabajo/A08_ALMACENAMIENTO_ACUMULADO.md).
6. **Cierre:** T-11 final, T-11 trazable, checklist y D3.

### Lectura por apartado

| Si se redacta… | Leer primero | Consultar después si hace falta |
|---|---|---|
| `4.1 a)` | A1 §1 | Subdocumento 3 para no duplicar alcance |
| `4.1 b)` | A1, A2 y A3 | D1/D2; C4 A00/A01/A02 para datos |
| `4.2 a)` | C1 y C3 | documento C4 de dimensionamiento de Célula 3; A08 de Célula 4 para capacidad acumulada |
| `4.2 b)` | C2 §§3–4/10 | Registro ADR y T-11 |
| `4.2 c)` | C2 §§7–9 y C4 §§6–10 | D1 para seguridad física/licencias |
| `4.2 d)` | C2 §5 y C1 §7 | C4 §6 y ADR-005/007 |
| `4.2 e)` | C2 §6 y C3 §9 | ADR-007/011 y D2 para riesgo residual |
| T-11 | T-11 final y trazable | C2/C4/D1 para volver a la justificación |

### Uso de Célula 4

C3 gobierna arquitectura, emplazamiento, continuidad, integración, seguridad y T-11. C4 gobierna el modelo detallado de datos, diccionario, calidad, linaje, retención y capacidad acumulada. El Subdocumento 4 debe resumir el aporte de C4 y enlazarlo internamente; no debe copiar su catálogo completo.

Los `.tex` de C4 no forman parte de esta ruta. Solo se consultan si el Markdown canónico no permite resolver una contradicción concreta.

---

## 8. Pendientes legítimos que no bloquean la escritura

Pueden quedar expresamente condicionados en el Informe 1:

- levantamiento de la sala y del patio;
- capacidad, diversidad y conmutación real de ambos enlaces;
- radiopropagación LTE/5G con patio cargado;
- tamaño y compresión real de imágenes;
- interfaces, versiones, permisos y CDC reales del TOS y terceros;
- productos, versiones y fechas de soporte al congelar la oferta;
- selección final de mecanismo de protección por campo sensible;
- custodios, residencia y política detallada de copias;
- fichas eléctricas, térmicas y marinas;
- pruebas de 72 horas, reconciliación, failover, restauración y ciberseguridad;
- validación de la metodología de emisiones;
- innovaciones que todavía no han sido ratificadas por arquitectura.

Cada condición debe indicar responsable, momento de cierre y efecto. No debe presentarse como defecto ni como evidencia ya obtenida.

---

## 9. Elementos que no deben incorporarse como hechos

- ADR aprobados: actualmente no existe ninguno.
- Starlink o un tercer enlace comprometido.
- productos comprados, contratados o probados.
- sala de 34 m² declarada conforme sin levantamiento.
- tecnologías de innovación incorporadas a la baseline sin ratificación.
- resultados operacionales ya alcanzados.
- interfaces de terceros confirmadas sin evidencia.
- precios, tarifas, costos unitarios o montos inferibles.
- diagramas archivados presentados como figuras finales.

---

## 10. Lista de cierre de esta base

Antes de comenzar la redacción, comprobar:

- [x] La estructura oficial 4.1/4.2 está identificada.
- [x] El esquema de solución, la arquitectura lógica y la arquitectura física se distinguen.
- [x] La arquitectura híbrida está definida y justificada.
- [x] C3 y C4 comparten autoridad normal/corte/retorno.
- [x] C3 y C4 comparten escenarios de capacidad.
- [x] El vocabulario principal de datos está conciliado.
- [x] Seguridad, integración, continuidad y T-11 tienen fuente asignada.
- [x] Los ADR conservan estado `PROPUESTO`.
- [x] Los bosquejos están marcados como abiertos y no finales.
- [x] Los `.tex` quedan fuera de la ruta normal de lectura.
- [ ] El equipo redacta el contenido en lenguaje natural.
- [ ] El equipo define y aprueba los diagramas definitivos.
- [ ] Se ensambla el T-11 en la salida final.
- [ ] D3 revisa el artefacto completo y emite veredicto.

**Resultado:** base suficiente para que Célula 3 comience la escritura y para que Célula 4 avance su Subdocumento 5 sin reabrir las decisiones compartidas.

---

## 11. Fuentes oficiales de control

Cada integrante debe consultar las copias oficiales de las bases y del caso que le haya entregado el curso. Esta guía no presupone nombres de carpetas ni rutas locales. Las fuentes que deben mantenerse disponibles son:

- **Pautas del Curso:** alcance y expectativas del Informe y Presentación 1.
- **Bases Administrativas:** Artículo 16 y formularios T-7, T-11, T-21 y T-22.
- **Bases Técnicas Transversales:** arquitectura, nube/on-premise, integración, seguridad, continuidad, infraestructura y capacidad.
- **Bases Técnicas del Caso 06 — Portuaria:** restricciones, magnitudes y umbrales propios del terminal.

Las referencias contractuales deben expresarse por documento, artículo, capítulo, formulario o requisito. No deben depender de la ubicación del archivo en el computador de quien redacta.

La trazabilidad normativa detallada permanece en [MA-6](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md), la [Matriz Global](../00_Gobierno/02_MATRIZ_CUMPLIMIENTO_GLOBAL.md) y las trazas de cada frente. No se copia completa en el Subdocumento 4.
