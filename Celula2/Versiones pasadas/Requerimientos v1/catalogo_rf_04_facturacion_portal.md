# Catálogo de Requerimientos Funcionales — Bloque 4
 
## Dominios `RF-FAC` (hechos facturables) y `RF-POR` (portal y autoservicio)
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento:** 3 — Esquema de solución y alcance
> **Formato y convención:** los declarados en `claude/plan_catalogo_rf_subdocumento3.md`, Fase 0.
> **Convenciones de cita:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
> **Estado:** borrador de Célula 2. Pendiente de las dos pasadas de la Fase 4.
 
**Cobertura de este bloque:** criterios de aceptación 14 y 15 (CP, Cap. 18); indicadores de facturas objetadas y de objeciones aceptadas por falta de evidencia (CP, 7.3); Decisión N° 11 y supuesto de alcance del autoservicio.
 
> **Criterio de no duplicación aplicado.** Varios trámites del portal ya están redactados como comportamiento en otros dominios. En lugar de repetirlos, este bloque los referencia. La tabla de la sección `RF-POR` declara qué trámite se realiza mediante qué requerimiento de otro dominio, accedido por este canal.
 
---
 
# Dominio `RF-FAC` — Hechos facturables y su evidencia
 
Etapa 2. Once requerimientos. Atacan el indicador más costoso del caso en términos de relación comercial: el 62 % de las objeciones que el terminal termina aceptando porque no logra demostrar lo que cobra.
 
---
 
**`RF-FAC-01` — Generación del hecho facturable en el instante en que ocurre** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** generar cada hecho facturable como **evento del sistema en el momento en que el hecho ocurre**, y **no deberá** reconstruirlo posteriormente a partir de planillas ni de reportes de turno.
**Actor:** solución. **Precondición:** ocurrencia del hecho registrada por el dominio operacional correspondiente.
**Resultado esperado:** hecho facturable con instante propio, generado sin intervención humana.
**Origen:** Decisión N° 11 · CP, Cap. 4.8 (hoy la conexión refrigerada se calcula «según la planilla de la ronda» y los movimientos adicionales «con lo que reportó el supervisor de turno») · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** sobre una muestra de hechos facturables de un período, se acredita que el 100 % tiene un evento de sistema con instante propio y que ninguno provino de consolidación manual.
 
---
 
**`RF-FAC-02` — Regla de negocio específica por tipo de hecho** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** aplicar a cada tipo de hecho facturable —transferencia, almacenaje, conexión refrigerada, movimiento adicional, pesaje, inspección, uso de zona de carga peligrosa y servicio especial— una **regla de negocio propia, parametrizable y versionada**, y **deberá** dejar trazable qué versión de la regla se aplicó a cada hecho.
**Actor:** solución. **Precondición:** hecho generado y tipificado.
**Resultado esperado:** cada hecho valorizado por una regla identificable y reproducible.
**Origen:** Decisión N° 11 · CP, Cap. 4.8, que enumera los ocho conceptos que el terminal cobra · BTT, RT-16.02 (parametrización con versionado y registro de quién cambió qué) · BTT, RT-16.14 (motor de reglas: trazable qué regla se aplicó a cada transacción).
**Criterio de aceptación:** se modifica la versión de una regla y se acredita que los hechos anteriores conservan la versión con que fueron calculados.
 
---
 
**`RF-FAC-03` — Cálculo de días de almacenaje** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** calcular los días de almacenaje a partir de los eventos registrados de ingreso y de salida del contenedor, y **deberá** exponer al cliente ambos instantes junto con el cargo.
**Actor:** solución. **Precondición:** eventos de ingreso y salida registrados.
**Resultado esperado:** cargo de almacenaje con sus dos instantes de origen visibles.
**Origen:** Decisión N° 11 · CP, Cap. 4.8 («las fechas del sistema no siempre coinciden con lo que el cliente cree») · articula con `RF-GAT-11`.
**Criterio de aceptación:** se selecciona un cargo de almacenaje y se recuperan los dos eventos de barrera que lo determinan, con sus marcas de tiempo.
 
---
 
**`RF-FAC-04` — Registro de movimientos adicionales** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** derivar los movimientos adicionales facturables del registro de movimientos por telemetría, y **no deberá** admitir su declaración por el supervisor de turno.
**Actor:** solución. **Precondición:** movimientos registrados conforme a `RF-PAT-05`.
**Resultado esperado:** cargo por movimiento adicional respaldado por el movimiento físico que lo originó.
**Origen:** Decisión N° 11 · CP, Cap. 4.8 (hoy se calculan «con lo que reportó el supervisor de turno») · Decisión N° 15.
**Criterio de aceptación:** se contrasta una muestra de movimientos adicionales facturados contra los movimientos registrados por telemetría, verificando correspondencia uno a uno.
 
---
 
**`RF-FAC-05` — Hechos facturables de pesaje, inspección y carga peligrosa** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** generar el hecho facturable del pesaje a partir de la captura de la báscula, el de la inspección a partir de la cita de inspección atendida, y el de uso de zona de carga peligrosa a partir de la asignación de posición en esa zona.
**Actor:** solución. **Precondición:** el evento operacional correspondiente registrado.
**Resultado esperado:** los tres conceptos respaldados por su evento de origen y no por declaración.
**Origen:** CP, Cap. 4.8, que los enumera entre los conceptos cobrados · articula con `RF-GAT-08`, `RF-INS` y `RF-PAT-07`.
**Criterio de aceptación:** para cada uno de los tres conceptos se recupera, desde el cargo, el evento operacional que lo originó.
 
---
 
**`RF-FAC-06` — Evidencia asociada e inalterable** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** asociar a cada hecho facturable la evidencia que lo respalda —eventos, mediciones, series o lecturas— y **deberá** conservarla de modo que ningún perfil, incluido el administrador de la plataforma, pueda modificarla.
**Actor:** solución. **Precondición:** hecho facturable generado.
**Resultado esperado:** evidencia oponible ante una objeción del cliente.
**Origen:** Decisión N° 11 · BTT, RT-16.07 (auditoría inalterable, no modificable por ningún perfil, incluido el administrador de la plataforma) · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** se intenta modificar la evidencia de un hecho facturable con perfil de administrador y el sistema lo impide; el intento queda registrado.
 
---
 
**`RF-FAC-07` — Prohibición de creación y edición manual** · Prioridad: **Crítica**
 
**Descripción.** La solución **no deberá** permitir la creación ni la edición manual de un hecho facturable. Toda corrección **deberá** ejecutarse como **hecho compensatorio nuevo**, con su motivo, su autor y su vínculo al hecho corregido.
**Actor:** solución. **Precondición:** hecho facturable existente.
**Resultado esperado:** la serie de hechos es acumulativa y auditable; nada se sobrescribe.
**Origen:** Decisión N° 11 (sin intervención manual previa a la facturación) · BTT, RT-16.06 (registro con valores anteriores y posteriores) · CP, Cap. 10, restricción no negociable N° 14.
**Criterio de aceptación:** se intenta editar un hecho facturable y el sistema lo rechaza; se ejecuta una corrección y se acredita que quedó como hecho compensatorio vinculado al original.
 
---
 
**`RF-FAC-08` — Presentación y trazabilidad de la objeción** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir al cliente presentar una objeción de facturación por autoservicio, indicando el cargo objetado y su motivo, y **deberá** mantener el estado de la objeción hasta su cierre.
**Actor:** exportador, importador o agencia de aduana. **Precondición:** cargo emitido y persona usuaria autorizada.
**Resultado esperado:** objeción registrada en el sistema, con estado y responsable, sin correo ni planilla.
**Origen:** CP, Cap. 4.8 y Anexo A (hoy las objeciones viajan por correo con «seguimiento en planilla») · CP, Cap. 5 · BTT, RT-16.11 (flujo con estados, responsables, plazos y escalamiento) · supuesto de alcance del autoservicio, trámite 4.
**Criterio de aceptación:** un cliente presenta una objeción por autoservicio y se acredita su estado, su responsable asignado y su plazo, sin intercambio por correo.
 
---
 
**`RF-FAC-09` — Resolución de la objeción con la evidencia** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** presentar al cliente y al analista, junto a la objeción, la **evidencia completa del hecho objetado**, y **deberá** registrar el fundamento de la resolución, sea de aceptación o de rechazo.
**Actor:** analista de facturación y cliente. **Precondición:** objeción presentada.
**Resultado esperado:** resolución fundada en evidencia verificable, no en la imposibilidad de demostrar.
**Origen:** CP, 7.3 (62 % de las objeciones se acepta «porque el terminal no logra demostrar el hecho que factura», referencia cero) · Decisión N° 11 · CP, Cap. 18, criterio 14.
**Criterio de aceptación:** sobre las objeciones de un período se mide el porcentaje aceptado por falta de evidencia, contra la referencia de cero, y se verifica que cada resolución consigna su fundamento.
 
---
 
**`RF-FAC-10` — Conciliación diaria de hechos facturables** · Prioridad: **Crítica**
 
**Descripción.** Mientras el dominio esté en convivencia, la solución **deberá** conciliar diariamente los hechos facturables y su evidencia contra el registro del sistema de 2012, y **no deberá** admitir ninguna diferencia no explicada al cierre del día.
**Actor:** solución y analista de facturación. **Precondición:** dominio en convivencia con escritura dual activa.
**Resultado esperado:** cero diferencias no explicadas al cierre diario, con ventana de investigación de 24 horas.
**Origen:** Decisión N° 1, umbrales de conciliación: hechos facturables con umbral cero por su implicancia económica y contractual · CP, 17.6 punto 2 · articula con `RF-CON-05`.
**Criterio de aceptación:** durante siete días consecutivos el informe de conciliación diaria cierra con cero diferencias no explicadas, o con cada diferencia explicada dentro de las 24 horas.
 
---
 
**`RF-FAC-11` — Retención de la evidencia** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** conservar la evidencia de cada hecho facturable durante **seis años**, y **deberá** permitir su recuperación durante todo ese período.
**Actor:** solución. **Precondición:** hecho facturable generado con su evidencia.
**Resultado esperado:** evidencia recuperable durante el plazo de retención exigido.
**Origen:** CP, Cap. 15, RT-05.10 (evidencia de hechos facturables: 6 años) · CP, Cap. 15, RT-05.15 (migrar 6 años de hechos facturables y su evidencia).
**Criterio de aceptación:** se recupera la evidencia de un hecho facturable de seis años de antigüedad y se verifica su integridad.
 
---
 
> **Hecho facturable cubierto en otro dominio.** Las **horas de conexión refrigerada** se derivan de los eventos de instrumentación en `RF-REF-13`, y no se duplican aquí.
 
---
 
# Dominio `RF-POR` — Portal y autoservicio de clientes
 
Etapa 2. Ocho requerimientos propios, más cuatro trámites realizados por requerimientos de otros dominios y accedidos por este canal.
 
---
 
**`RF-POR-01` — Capa pública sin autenticación** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** publicar sin autenticación el estado de congestión del acceso vial, la disponibilidad de franjas de cita y la información general de operación que el CLIENTE determine, con los mismos estándares de accesibilidad y desempeño que el resto de la plataforma.
**Actor:** cualquier persona. **Precondición:** ninguna.
**Resultado esperado:** información de decisión disponible antes de que el transportista inicie el viaje.
**Origen:** BTT, RT-16.31 (portal público) · CP, Cap. 15, RT-16.30 · CP, Cap. 18, criterio 2 · articula con `RF-GAT-13`.
**Criterio de aceptación:** se accede sin credenciales a la capa pública y se verifica el cumplimiento del estándar de accesibilidad declarado en RNF-USA-01.
 
---
 
**`RF-POR-02` — Registro y recuperación de acceso autoservidos** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** permitir a las personas usuarias externas —navieras, agencias de aduana, exportadores, importadores, transportistas, autoridades, concedente y operador ferroviario— registrarse, verificar su identidad y recuperar su acceso de forma autoservida y segura.
**Actor:** persona usuaria externa. **Precondición:** ninguna.
**Resultado esperado:** alta y recuperación sin intervención del terminal.
**Origen:** BTT, RT-12.12 · CP, Cap. 15, RT-12.12, que enumera las contrapartes externas del caso · CP, Cap. 2 (14 navieras, 210 agencias, ~1.400 exportadores e importadores, 380 empresas de transporte).
**Criterio de aceptación:** una persona usuaria externa completa el ciclo de registro, verificación y recuperación de acceso sin contacto con el terminal.
 
---
 
**`RF-POR-03` — Consulta autenticada de estado y posición** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** entregar a la persona usuaria externa autenticada el estado y la posición reales de su carga, actualizados conforme al umbral de latencia comprometido, y **no deberá** limitarse a la consulta por número de contenedor sin autenticación.
**Actor:** exportador, importador, agencia o transportista. **Precondición:** persona usuaria autenticada con carga asociada.
**Resultado esperado:** estado real, no un dato de un día de antigüedad.
**Origen:** CP, Cap. 5 (el portal de 2016 «sin autenticación, con datos actualizados una vez al día», se reemplaza) · CP, Cap. 15, RT-16.30 · CP, Cap. 18, criterio 15 · supuesto de alcance del autoservicio, trámite 1.
**Criterio de aceptación:** se verifica que el estado publicado refleja el evento origen dentro del umbral de RNF-DES-06, y que la consulta exige autenticación.
 
---
 
**`RF-POR-04` — Segregación de visibilidad por contraparte** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** limitar la información visible a cada persona usuaria externa a la que le corresponde por su relación con la carga, y **no deberá** exponer información comercial de un cliente a otro.
**Actor:** solución. **Precondición:** persona usuaria autenticada con rol y contraparte determinados.
**Resultado esperado:** ninguna contraparte accede a información de otra.
**Origen:** CP, Cap. 15, RT-11.10 (cifrado de información comercial sensible: tarifas y volúmenes negociados) · BTT, RT-12.05 · CP, Cap. 15, RT-16.09 (registro de consultas a información sensible) · articula con RNF-SEG-05 y RNF-SEG-09.
**Criterio de aceptación:** se intenta acceder a la carga de una contraparte distinta y el sistema lo deniega; el intento queda registrado en la auditoría de consultas.
 
---
 
**`RF-POR-05` — Presentación de objeción de facturación en línea** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir al cliente descargar la evidencia de un hecho facturable y presentar su objeción desde el portal, sin recurrir al correo ni al mostrador.
**Actor:** exportador, importador o agencia de aduana. **Precondición:** cargo emitido con evidencia asociada.
**Resultado esperado:** ciclo de objeción íntegramente autoservido.
**Origen:** supuesto de alcance del autoservicio, trámite 4 · CP, Cap. 4.8 · articula con `RF-FAC-08` y `RF-FAC-09`.
**Criterio de aceptación:** un cliente descarga la evidencia y presenta la objeción por el portal, y el caso queda con estado y responsable sin ningún intercambio por correo.
 
---
 
**`RF-POR-06` — Coordinación y estado de cita de inspección** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** permitir a la agencia de aduana y al inspector consultar y coordinar el estado de una cita de inspección desde el portal.
**Actor:** agencia de aduana e inspector de autoridad. **Precondición:** cita de inspección registrada.
**Resultado esperado:** coordinación visible para las tres partes, sin radio ni teléfono.
**Origen:** Decisión N° 21 · BTT, RT-12.12 (los inspectores son personas usuarias externas) · supuesto de alcance del autoservicio, trámite 6 · articula con el dominio `RF-INS`.
**Criterio de aceptación:** un inspector consulta el estado de una cita y confirma su asistencia desde el portal, y la coordinación queda registrada.
 
---
 
**`RF-POR-07` — Interfaz y mensajería en español e inglés** · Prioridad: **Crítica**
 
**Descripción.** La solución **deberá** presentar en **español y en inglés** todas las interfaces y plantillas de mensajería dirigidas a navieras y a clientes internacionales.
**Actor:** naviera y cliente internacional. **Precondición:** ninguna.
**Resultado esperado:** operación completa en cualquiera de los dos idiomas, sin funcionalidad reducida en uno de ellos.
**Origen:** CP, Cap. 10, restricción no negociable N° 13 · CP, Cap. 15, RT-13.12 · articula con RNF-IDI-01.
**Criterio de aceptación:** auditoría de cobertura de idioma sobre el catálogo completo de pantallas y plantillas dirigidas a navieras y clientes internacionales, verificando paridad funcional entre ambos idiomas.
 
---
 
**`RF-POR-08` — Autoatención de las consultas de mayor frecuencia** · Prioridad: **Alta**
 
**Descripción.** La solución **deberá** resolver por autoservicio los siete trámites declarados en el supuesto de alcance, y **deberá** medir el desvío del canal telefónico y presencial hacia el portal.
**Actor:** persona usuaria externa. **Precondición:** persona usuaria registrada.
**Resultado esperado:** el contacto telefónico deja de ser necesario para los trámites declarados, y el desvío es medible.
**Origen:** BTT, RT-16.32 · CP, Cap. 18, criterio 15 · CP, Cap. 9.8 · supuesto de alcance del autoservicio.
 
> El supuesto de alcance advierte que si las consultas de mayor frecuencia reales no están entre las siete declaradas, la solución cumple la letra de RT-16.32 sin descargar el mostrador. Por eso la medición del desvío forma parte del requerimiento y no es opcional: es lo que permite detectar ese error a tiempo.
 
**Criterio de aceptación:** se mide el volumen de contactos telefónicos y presenciales por tipo de trámite antes y después de la puesta en marcha, sobre los siete trámites declarados.
 
---
 
## Trámites del autoservicio realizados en otros dominios
 
| Trámite del supuesto de alcance | Requerimiento que lo realiza | Dominio |
|---|---|---|
| 2 — Solicitud, modificación y cancelación de cita de camión | `RF-GAT-01` | `RF-GAT` |
| 3 — Carga y validación anticipada de documentación | `RF-GAT-03` | `RF-GAT` |
| 5 — Descarga de la serie de temperatura como evidencia de cadena de frío | `RF-REF-12` | `RF-REF` |
| 7 — Estado de congestión del acceso vial | `RF-GAT-13` · `RF-POR-01` | `RF-GAT` · `RF-POR` |
 
---
 
## Trazabilidad del bloque
 
| Criterio de aceptación (CP, Cap. 18) | Requerimientos que lo sostienen |
|---|---|
| 14 — Hechos facturables con evidencia suficiente | `RF-FAC-01` a `07`, `09`, `10` · `RF-REF-13` · `RF-INT-09` |
| 15 — Clientes resuelven sin teléfono ni mostrador | `RF-POR-01` a `08` · `RF-GAT-01`, `03`, `13` · `RF-REF-12` |
| 2 — Sin fila que desborde *(parcial)* | `RF-POR-01` |
| 12 — Registro de temperatura entregable *(parcial)* | `RF-REF-12` accedido por `RF-POR` |
 
| Indicador de línea base (CP, 7.3) | Referencia | Requerimientos que lo mueven |
|---|---|---|
| Facturas objetadas 4,7 % | bajo 1 % | `RF-FAC-01` a `07` |
| Objeciones aceptadas por falta de evidencia 62 % | cero | `RF-FAC-06`, `09` |
 
**Total del bloque: 19 requerimientos** — 11 en `RF-FAC`, 8 en `RF-POR`.
**Acumulado del catálogo: 97 requerimientos** en ocho dominios.
 
**Dominios pendientes:** `RF-ACC`, `RF-OPD`, `RF-INS`, `RF-EMI`.
 
---
 
## Pendientes transversales del catálogo
 
| # | Pendiente | Origen |
|---:|---|---|
| 1 | Fundamentar las once metas propuestas con literatura arbitrada o casos documentados. Prioritarias: metas 1 (remociones) y 11 (inspecciones) | Solicitud de Rodolfo Fernández · CP, Cap. 16.2 |
| 2 | Ratificar `RF-PAT-10` (vía de excepción del operador) | Bloque 2 |
| 3 | Evitar la duplicación entre `RF-GAT-14` y el dominio `RF-OPD` | Bloque 1 |
| 4 | Verificar el mapeo entre los 107 códigos RT no funcionales y los 77 RNF, al construir el T-12 | Vacío 6 de la Fase 2 |
| 5 | Confirmar con Célula 3 la factibilidad de lectura desde el sistema de control de las grúas | Bloque 3 |
| 6 | Declarar la versión exacta de cada mensaje de mensajería marítima comprometida, por naviera | Bloque 3 |
| 7 | **Confirmar con Célula 4 el tratamiento de la evidencia inalterable de hechos facturables** en el modelo de datos. `RF-FAC-06` exige que ningún perfil pueda modificarla, incluido el administrador, lo que condiciona la estrategia de persistencia del Subdocumento 5 | Bloque 4 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*