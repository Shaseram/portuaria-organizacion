# Plan de entregables y dependencias — Célula 3

**Objeto:** distribuir el Subdocumento 4 entre tres frentes independientes, con puntos de integración breves y trazabilidad acumulable.  
**Autoridad contextual:** [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](00_MAESTRO_CONTEXTO_ARQUITECTURA.md).  
**Regla:** este archivo define el trabajo; los nombres personales se asignan únicamente en la tabla siguiente.

> **Lectura vigente tras MA-8:** este archivo conserva el plan de construcción de los frentes. Las tres baselines ya fueron producidas y sus destinos se actualizaron a la estructura MA-7. Para continuar desde el estado actual, usar [`Celula3/README.md`](../README.md) y el plan `R1–R6` de [`07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md`](07_PLAN_MAESTRO_CIERRE_INFORME1_SUBDOC4.md).

**Corte histórico de entrada:** Célula 2 `c4756df` (2026-09-05), conforme al Maestro v1.1. Antes del desarrollo, cada frente debía leer las consecuencias del Maestro §2.3 y sus destinos en la matriz global §3.

## 1. Asignación y control

| Frente | Responsable | Revisor cruzado | Estado | Carpeta |
|---|---|---|---|---|
| Frente 1 — Lógica e integración | `POR ASIGNAR` | `POR ASIGNAR` | BASELINE I1 COMPLETADA | `01_Frente_Logica_Integracion/` |
| Frente 2 — Física y despliegue | `POR ASIGNAR` | `POR ASIGNAR` | BASELINE I1 COMPLETADA | `02_Frente_Fisica_Despliegue/` |
| Frente 3 — Seguridad y consolidación | `POR ASIGNAR` | `POR ASIGNAR` | BASELINE/PREPARACIÓN COMPLETADA; D3 PENDIENTE | `03_Frente_Seguridad_Consolidacion/` |

No se renombran carpetas cuando se asignen personas.

## 2. Resultado esperado

Al cerrar los diez paquetes deben existir:

- esquema de solución y arquitectura lógica propios del puerto;
- catálogo de componentes, bounded contexts, responsabilidades e interfaces;
- arquitectura de integración y procesos críticos, incluida convivencia TOS;
- arquitectura física híbrida con emplazamiento y justificación Art. 16;
- tecnologías, hardware, sala/data centers y despliegue/continuidad;
- dimensionamiento reproducible y T-11 consistente;
- arquitectura de seguridad Zero Trust y modelo de amenazas;
- ADR y puntos únicos de falla explícitos;
- documento final del Subdocumento 4 y evidencia completa de trazabilidad.

## 3. Regla de independencia

Ningún frente espera el cierre total de otro. Se trabaja con versiones parciales congeladas:

- `v0.1`: catálogo/criterios suficiente para que otro frente comience a mapear.
- `v0.5`: contenido completo, todavía sujeto a revisión cruzada.
- `v1.0`: aprobado e integrable.

Una dependencia de refinamiento no bloquea el inicio. Los campos inciertos se marcan `POR VALIDAR` y se usa un identificador provisional estable.

## 4. Flujo de dependencias

```text
Puerta 0: Maestro + nomenclatura + obligaciones congeladas
        │
        ├── Frente 1: catálogo lógico e interfaces v0.1
        ├── Frente 2: alternativas físicas y plantilla Art. 16 v0.1
        └── Frente 3: catálogo de controles y criterios físicos v0.1
                         │
Puerta 1: intercambio de los tres paquetes v0.1
        │
        ├── Frente 1 completa procesos/TOS e integración
        ├── Frente 2 completa mapeo físico, continuidad y capacidad
        └── Frente 3 completa amenazas, ADR y cruces de seguridad
                         │
Puerta 2: revisión lógica ↔ física ↔ seguridad ↔ T-11
                         │
Puerta 3: consolidación, auditoría y cierre
```

### 4.1 Dependencias concretas

| Productor | Salida temprana | Consumidor | Uso | ¿Bloquea inicio? |
|---|---|---|---|---|
| Frente 1 | IDs de componentes, interfaces y criticidad | Frente 2 | lógico→físico y capacidad | No; refina C1/C4 |
| Frente 1 | flujos, contratos y datos sensibles | Frente 3 | amenazas/controles | No; refina D1/D2 |
| Frente 2 | zonas, nodos, redes y ubicaciones | Frente 3 | seguridad física/despliegue | No; refina D1/D2 |
| Frente 3 | catálogo de controles y restricciones | Frente 2 | redes, componentes, licencias y T-11 | No; debe llegar en Puerta 1 |
| Frente 3 | criterios de exposición/identidad | Frente 1 | seguridad lógica visible | No; debe llegar en Puerta 1 |
| Todos | candidatos de ADR/T-11/trazas | Frente 3/integrador | consolidación | Sí para cierre, no para desarrollo |

## 5. Contrato común de todos los paquetes

Cada entregable debe conservar las siguientes secciones:

1. Objetivo y destino final.
2. Obligaciones asignadas.
3. Entradas obligatorias y dependencias.
4. Trabajo requerido.
5. Contenido listo para integrar.
6. Diagramas/tablas/catálogos obligatorios.
7. Decisiones permitidas y puntos a escalar.
8. Aportes a T-11 y ADR.
9. Salidas hacia otros frentes.
10. Definición de terminado.
11. Referencia a su trazabilidad.

No se considera entregado un archivo que solo contenga recomendaciones o un dibujo sin narrativa, catálogo y trazabilidad.

## 6. Frente 1 — Lógica e integración

### A1 — Contexto y arquitectura lógica

**Archivo:** `01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md`

**Objetivo:** definir la visión lógica única y comprensible de la plataforma, sin marcas de producto.

**Debe entregar:**

- esquema de solución/contexto con actores, sistemas externos y límite de TERABYTE;
- diagrama de arquitectura lógica con las ocho capas obligatorias;
- catálogo de módulos/bounded contexts y responsabilidades exclusivas;
- interfaces entre módulos, dependencias permitidas y datos/eventos principales;
- modelo conceptual mínimo: contenedor, posición, movimiento, visita de nave, cita/camión, reefer/alarma, inspección, hecho/evidencia, identidad, consumo/emisión;
- comparación de estilo modular vs. más distribuido y candidato de ADR;
- explicación de por qué la arquitectura es propia del Caso 06.

**Cobertura:** `SD4-01`, `SD4-07`, `SD4-08`; T7-4.1, T7-4.7, T7-4.8.

**Salidas tempranas obligatorias:** catálogo lógico `v0.1` con ID, responsabilidad, criticidad, persistencia y consumidores.

**Destino final:** secciones 4.1.1 a 4.1.5 del consolidado.

### A2 — Arquitectura de integración

**Archivo:** `01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md`

**Objetivo:** especificar cómo la solución intercambia información sin inventar capacidades de terceros.

**Debe entregar:**

- catálogo de 21 contrapartes lógicas + 7 familias técnicas;
- servicios, eventos, propietarios de dato y dirección;
- contratos/versiones, síncrono/asíncrono, frecuencia/peak;
- timeout, retry, backoff+jitter, circuit breaker, bulkhead y rate limit;
- idempotencia, deduplicación, orden, DLQ y reconciliación;
- gobierno: catálogo, versionado, compatibilidad, ciclo de alta/cambio/retiro y responsable;
- fallos por contraparte y fallback operativo;
- EDIFACT BAPLIE/COPRAR/COARRI/CODECO correctamente usados;
- ERP como emisor tributario, grúas solo lectura, VMS conservado y autoridades sin API inventada.

**Cobertura:** `SD4-03`, partes de `SD4-04/05/06/08`; T7-4.3.

**Salida temprana:** matriz de interfaces `v0.1` con sensibilidad y criticidad para Seguridad y Física.

**Destino final vigente tras MA-7:** sección 4.1.3 y referencias de continuidad en 4.2.6.

### A3 — Procesos críticos y convivencia TOS

**Archivo:** `01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md`

**Objetivo:** demostrar el comportamiento en los escenarios donde una caja estática no basta.

**Debe entregar:**

- procesos/diagramas de secuencia para nave, gate, reefer, inspección/hecho facturable y operación desconectada;
- nuevo→legado, legado→nuevo, escritura parcial y contraparte caída;
- matriz `dominio × zona × fase` y traspaso de autoridad;
- conciliación, ventanas, umbrales y clasificación de divergencias;
- cutover, doble control, break-glass, retorno y apagado legado;
- funciones críticas locales, no disponibles, procedimiento manual y sincronización ≤90 min;
- programa 2029 reflejado como resultado operacional.

**Cobertura:** `SD4-01`, `SD4-03`, `SD4-05`, `SD4-07`, `SD4-08`.

**Salida temprana:** lista de cinco funciones críticas, sus dependencias y RTO/RPO operacional.

**Destino final vigente tras MA-7:** sección 4.1.3 y apoyo a 4.2.6 del consolidado.

## 7. Frente 2 — Física y despliegue

### C1 — Arquitectura física y emplazamiento

**Archivo:** `02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md`

**Objetivo:** convertir los componentes lógicos en nodos, zonas y enlaces híbridos concretos.

**Debe entregar:**

- diagrama físico completo con límite de oferta, zonas y protocolos;
- tabla lógico→físico→ubicación→criticidad;
- emplazamiento individual nube/on-premise/edge;
- justificación Art. 16 por los seis criterios;
- región primaria/secundaria y multi-AZ;
- sala, edge de gate/patio/reefer/muelle, redes y sistemas conservados;
- alternativas de sala actual/nueva/edge mínimo y candidato de ADR;
- puntos únicos de falla y tratamiento inicial.

**Cobertura:** `SD4-02`, `SD4-05`, `SD4-07`, `SD4-08`; T7-4.2, 4.5, 4.7, 4.8.

**Salida temprana:** topología y alternativas de sala `v0.1`, aun con componentes lógicos provisionales.

**Destino final vigente tras MA-7:** sección 4.2.1.

### C2 — Tecnologías, hardware y data centers

**Archivo:** `02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md`

**Objetivo:** especificar qué plataformas, software, licencias, equipos y recintos materializan la arquitectura.

**Debe entregar:**

- tecnologías de software con versión o criterio de vigencia/EOS;
- producto/servicio de referencia y alternativa cuando corresponda;
- servicios gestionados vs. autogestionados y lock-in;
- servidores, almacenamiento/RAID, redes, HA, energía y puestos;
- sala/data center primario y secundario/DR;
- racks, UPS, generación, climatización, incendio, acceso y monitoreo;
- gabinetes/equipos por ambiente marino con IP y anticorrosión por clase;
- marca/modelo de referencia, cantidad, interfaces, consumo y margen cuando la base lo exija;
- candidatos de filas T-11 sin precios.

**Cobertura:** `SD4-02`, `SD4-05`, `SD4-06`, `SD4-08`; T21 4.2 b–e y T-11.

**Dependencia de refinamiento:** catálogo lógico A1 y controles/servicios de D1.

**Destino final vigente tras MA-7:** secciones 4.2.2 a 4.2.5.

### C3 — Despliegue, red y continuidad

**Archivo:** `02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md`

**Objetivo:** demostrar que la solución se despliega, opera, falla y se recupera dentro de las restricciones del puerto.

**Debe entregar:**

- DEV, QA, PREPROD, PROD y DR con aislamiento/equivalencia;
- segmentación operacional/administrativa/protección y conductos;
- conectividad redundante y prueba real del radioenlace;
- red de patio bajo carga, sombras y handover; site survey;
- HA, balanceo, réplicas y SPOF;
- RTO, RPO, DR, respaldo 3-2-1-1-0 y pruebas;
- operación 72 h y reconciliación ≤90 min;
- despliegue sin interrupción, retorno y restricciones dic–abr/nave;
- calendario técnico sin intervenciones prohibidas.

**Cobertura:** `SD4-04`, `SD4-05`, `SD4-07`, `SD4-08`.

**Salida temprana:** zonas de red y restricciones físicas para D1.

**Destino final vigente tras MA-7:** sección 4.2.6.

### C4 — Dimensionamiento y T-11

**Archivo:** `02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md`

**Objetivo:** convertir volúmenes y supuestos en capacidad, cantidades y especificaciones reproducibles.

**Debe entregar:**

- tabla de las 18 dimensiones de volumetría heredadas y su validación;
- fórmulas, unidades, supuestos y sensibilidad;
- dimensionamiento normal, peak de dos naves+gate, telemetría, usuarios, almacenamiento, red y 72 h;
- crecimiento, holgura, límite de ampliación y primer cuello de botella;
- capacidad por nodo/componente y cantidad resultante;
- consolidación de candidatos T-11 de los tres frentes;
- control 1:1 diagrama físico→cálculo→T-11.

**Cobertura:** `SD4-02`, `SD4-06`, `SD4-08`; T7-4.6 y T-11.

**Dependencia:** usa A1/A2 y D1 `v0.1`, pero puede comenzar validando la volumetría heredada.

**Destino final vigente tras MA-7:** secciones 4.2.7 y 4.2.8/Formulario T-11.

## 8. Frente 3 — Seguridad y consolidación

Este frente **no queda esperando**. Sus dependencias son de refinamiento. Desde la Puerta 0 debe producir controles concretos que ayudan a los otros dos frentes.

### D1 — Arquitectura de seguridad

**Archivo:** `03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md`

**Objetivo:** definir el modelo Zero Trust transversal y entregar requisitos físicos consumibles por el Frente 2.

**Debe entregar desde el inicio:**

- principios Zero Trust y flujos de confianza;
- zonas/conductos y requisitos de segmentación;
- capa expuesta: CDN/WAF/DDoS/TLS/certificados/bots;
- IAM: SSO, MFA, RBAC/ABAC, SoD, PAM, eventuales y terminal compartida;
- cifrado en tránsito/reposo, KMS/HSM, secretos y rotación;
- logging inalterable, SIEM, EDR y observabilidad de seguridad;
- DevSecOps, SBOM, firma/SLSA y anonimización;
- matriz control→capa→componente tipo→evidencia;
- **lista temprana de componentes/licencias/servicios de seguridad candidatos para Física y T-11**.

**Cobertura:** `SD4-04`, partes de `SD4-02/05/08`; T7-4.4.

**Salida temprana obligatoria:** paquete `SEC-PHYS-v0.1` con controles, zonas, componentes y restricciones de emplazamiento. No requiere esperar A1/C1.

**Destino final vigente tras MA-7:** sección 4.1.4; apoyo a 4.2.3 y 4.2.6.

### D2 — Amenazas, ADR y puntos de falla

**Archivo:** `03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`

**Objetivo:** desafiar la solución y registrar las decisiones relevantes.

**Debe entregar:**

- STRIDE por clase de componente e integración; luego refinado con IDs A1/C1;
- activos, fronteras de confianza, amenaza, riesgo, control y evidencia;
- escenarios portuarios: TOS, gate, reefer, app offline, terceros, VMS, radio y sincronización;
- registro consolidado de SPOF con impacto/aceptación/mitigación;
- candidatos y revisión de ADR de todos los frentes;
- criterios de selección, consecuencias y riesgos residuales.

**Cobertura:** `SD4-04`, `SD4-07`, `SD4-08`.

**Trabajo independiente inicial:** modelo por clases (`canal`, `gateway`, `servicio`, `broker`, `dato`, `edge`, `tercero`) y ADR obligatorios del Maestro.

**Destino final vigente tras MA-7:** secciones 4.1.4 y 4.1.5; apoyo transversal a las secciones físicas afectadas.

### D3 — Auditoría y consolidación

**Archivo:** `03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md`

**Objetivo:** preparar y ejecutar la unión de los entregables sin perder cobertura ni trazabilidad.

**Debe entregar desde el inicio:**

- matriz global y checklist listos para recibir evidencia;
- nomenclatura, reglas de diagramación y control de referencias;
- control lógico→físico→seguridad→capacidad→T-11;
- auditoría de todas las obligaciones `SD4-01..08` y T21 4.1/4.2;
- detección de contradicciones, genéricos, supuestos ocultos y precios;
- consolidación de ADR y contenido aprobado;
- acta de cierre con brechas y asuntos externos.

**Cobertura:** todas las obligaciones, sin sustituir autoría técnica.

**Destino final:** `90_Consolidado/` completo.

## 9. Puertas de integración

### Puerta 0 — Inicio

Se cumple cuando:

- Maestro y Plan leídos por los tres frentes;
- responsables asignados;
- IDs y estados adoptados;
- cada frente registra sus decisiones iniciales y abre sus trazas.

### Puerta 1 — Intercambio `v0.1`

Cada frente publica:

- Frente 1: catálogo lógico, interfaces, cinco funciones críticas;
- Frente 2: topología/alternativas, zonas/nodos y plantilla Art. 16;
- Frente 3: `SEC-PHYS-v0.1`, controles, componentes de seguridad y checklist.

Duración de sincronización recomendada: 30–45 minutos. Solo se congelan nombres/IDs y decisiones que desbloquean a otros.

### Puerta 2 — Revisión cruzada `v0.5`

Controles obligatorios:

- toda caja lógica tiene responsabilidad;
- todo despliegue corresponde a una necesidad lógica/transversal;
- cada componente físico tiene ubicación, cantidad/criterio y Art. 16;
- cada frontera expuesta tiene identidad, cifrado, registro y control;
- cada integración tiene fallo/fallback;
- cada cantidad tiene cálculo;
- cada fila T-11 aparece en físico y viceversa.

### Puerta 3 — Cierre `v1.0`

Se exige:

- trazas completas y fuentes válidas;
- ADR aprobados;
- pendientes externos visibles;
- checklist sin `NO CUMPLE`;
- coherencia de nombres y diagramas;
- ausencia de precios;
- consolidado legible como documento independiente.

## 10. Reglas de repositorio recomendadas

Cuando se use Git:

- ramas sugeridas: `feat/frente-logica-integracion`, `feat/frente-fisica-despliegue`, `feat/frente-seguridad-consolidacion`;
- un único integrador modifica `00_Gobierno/` y `90_Consolidado/` durante cada puerta;
- commits por paquete o decisión, mencionando IDs (`A1`, `MC-07`, `ADR-003`);
- no resolver conflictos aceptando una versión completa sobre otra sin revisar trazabilidad;
- etiquetar la línea base de Célula 2 y registrar el commit en el Maestro.

## 11. Definición global de terminado

El trabajo está terminado solo si:

- los diez paquetes tienen estado `APROBADO`;
- los ocho controles `SD4-*` tienen evidencia;
- todos los elementos de 4.1, 4.2 y T-11 están cubiertos;
- la arquitectura es trazable a Célula 2 y las Bases;
- las dependencias externas no están disfrazadas como decisiones;
- se puede recorrer la cadena requisito→lógico→físico→seguridad→capacidad→T-11;
- el documento final explica la solución sin exigir leer las carpetas de trabajo.
