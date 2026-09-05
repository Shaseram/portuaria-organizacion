# Inventario de requisitos codificados RT — Bases Técnicas Transversales TFEP-01/2026
 
Fuente única: `FEP02.26 Bases Tecnicas Transversales TFEP-01-2026.md` (v1.0, 18-08-2026), leído íntegro.
Equipo Terabyte — Caso 06 Portuaria. Fecha de elaboración: 2026-09-02.
 
Cobertura: **374 de 374 códigos**. Ningún código inventado; ninguno omitido.
 
---
 
## 1) Estructura: prefijo → capítulo → cantidad
 
El código tiene forma `RT-CC.NN`, donde **CC es el número del capítulo** y NN el correlativo dentro de él (numeral 1.4). El Capítulo 1 (Objeto, ámbito y régimen de cumplimiento) no contiene códigos RT: es dispositivo del documento. Por eso la numeración parte en 02.
 
| Prefijo | Capítulo | Título | Rango | N° |
|---|---|---|---|---|
| 02 | 2 | Modelo de arquitectura de referencia | RT-02.01 – RT-02.14 | 14 |
| 03 | 3 | Modelo híbrido: nube y on-premise | RT-03.01 – RT-03.24 | 24 |
| 04 | 4 | Ambientes, entrega continua y gestión de la configuración | RT-04.01 – RT-04.14 | 14 |
| 05 | 5 | Datos, integración e interoperabilidad | RT-05.01 – RT-05.30 | 30 |
| 06 | 6 | Site principal on-premise | RT-06.01 – RT-06.34 | 34 |
| 07 | 7 | Site secundario y recuperación ante desastres | RT-07.01 – RT-07.14 | 14 |
| 08 | 8 | Hardware, puestos de trabajo y equipamiento de terreno | RT-08.01 – RT-08.19 | 19 |
| 09 | 9 | Desempeño, capacidad y escalabilidad | RT-09.01 – RT-09.10 | 10 |
| 10 | 10 | Disponibilidad, continuidad y resiliencia | RT-10.01 – RT-10.09 | 9 |
| 11 | 11 | Seguridad de la información | RT-11.01 – RT-11.28 | 28 |
| 12 | 12 | Identidad, acceso y gestión de sesiones | RT-12.01 – RT-12.13 | 13 |
| 13 | 13 | Usabilidad, accesibilidad y experiencia de usuario | RT-13.01 – RT-13.12 | 12 |
| 14 | 14 | Observabilidad y gestión del servicio | RT-14.01 – RT-14.09 | 9 |
| 15 | 15 | Sostenibilidad, eficiencia y certificaciones | RT-15.01 – RT-15.09 | 9 |
| 16 | 16 | Módulos transversales obligatorios | RT-16.01 – RT-16.34 | 34 |
| 17 | 17 | Canales digitales y movilidad | RT-17.01 – RT-17.08 | 8 |
| 18 | 18 | Inteligencia artificial y automatización | RT-18.01 – RT-18.10 | 10 |
| 19 | 19 | Estructura y gobierno del proyecto | RT-19.01 – RT-19.10 | 10 |
| 20 | 20 | Implantación, pruebas y criterios de aceptación | RT-20.01 – RT-20.08 | 8 |
| 21 | 21 | Modelo de operación, mantención y soporte | RT-21.01 – RT-21.22 | 22 |
| 22 | 22 | Capacitación y transferencia de conocimiento | RT-22.01 – RT-22.09 | 9 |
| 23 | 23 | Información corporativa y presencia digital | RT-23.01 – RT-23.10 | 10 |
| 24 | 24 | Video de presentación de la propuesta | RT-24.01 – RT-24.06 | 6 |
| 25 | 25 | Prototipo interactivo de interfaz y diseño UX/UI | RT-25.01 – RT-25.10 | 10 |
| 26 | 26 | Innovaciones | RT-26.01 – RT-26.08 | 8 |
| | | **TOTAL** | | **374** |
 
Verificación: el conteo del cuerpo del documento coincide código por código con el Capítulo A (Índice de requisitos transversales). No hay saltos ni duplicados en ninguna serie.
 
Agrupación por Título:
- Título I (Cap. 1): 0 códigos.
- Título II — Arquitectura (Cap. 2–5): 82.
- Título III — Infraestructura (Cap. 6–8): 67.
- Título IV — No funcionales (Cap. 9–15): 90.
- Título V — Capacidades transversales (Cap. 16–18): 52.
- Título VI — Proyecto, implantación y operación (Cap. 19–22): 49.
- Título VII — Presentación (Cap. 23–26): 34.
---
 
## 2) Clasificación FUNCIONAL / NO FUNCIONAL / PROCESO-CONTRACTUAL
 
### Regla de decisión aplicada
 
| Clase | Regla operativa |
|---|---|
| **FUNCIONAL** | El sujeto es el sistema y el requisito describe una acción observable que produce un resultado (registra, notifica, exporta, sincroniza, autoriza, genera, busca). |
| **NO FUNCIONAL** | Califica un umbral, un atributo de calidad, una restricción de arquitectura, una propiedad de infraestructura física o una propiedad de seguridad/disponibilidad/desempeño sobre algo ya descrito. |
| **PROCESO / CONTRACTUAL** | El sujeto es el PROPONENTE o el ADJUDICATARIO como empresa: declarar, presentar, entregar, certificar, reportar, ejecutar pruebas, mantener un registro de gestión, dotar personal. |
 
Criterios de desempate usados, declarados para que el equipo pueda auditarlos:
1. Cuando un requisito combina una obligación sobre el sistema y una obligación de entregar un documento, se clasificó por la obligación dominante y se marcó como mixto.
2. Resiliencia interna sin salida visible (RT-02.08) = NO FUNCIONAL; degradación que informa a la persona usuaria (RT-02.09, RT-09.08) = FUNCIONAL.
3. Seguridad: mecanismos que la persona usuaria ejecuta y experimenta (SSO, MFA, sesión, registro externo) = FUNCIONAL; propiedades de protección (cifrado, endurecimiento, segmentación, WAF) = NO FUNCIONAL.
4. Observabilidad: monitoreo del propio estado de la plataforma = NO FUNCIONAL; tableros e indicadores puestos a disposición del CLIENTE = FUNCIONAL.
5. Capítulo 6 completo trata del recinto físico y su equipamiento: ningún requisito describe comportamiento del software, por eso no aporta códigos funcionales.
### Resumen cuantitativo
 
| Clase | N° | % |
|---|---|---|
| FUNCIONAL | 74 | 19,8% |
| NO FUNCIONAL | 107 | 28,6% |
| PROCESO / CONTRACTUAL | 192 | 51,3% |
| AMBIGUO (no clasificado) | 1 | 0,3% |
| **TOTAL** | **374** | **100%** |
 
### Distribución por capítulo
 
| Cap. | FUNCIONAL | NO FUNCIONAL | PROCESO | Ambiguo | Total |
|---|---|---|---|---|---|
| 02 | 3 | 7 | 4 | — | 14 |
| 03 | 5 | 9 | 10 | — | 24 |
| 04 | 0 | 2 | 12 | — | 14 |
| 05 | 13 | 7 | 10 | — | 30 |
| 06 | 0 | 24 | 10 | — | 34 |
| 07 | 1 | 7 | 6 | — | 14 |
| 08 | 0 | 7 | 12 | — | 19 |
| 09 | 1 | 3 | 6 | — | 10 |
| 10 | 0 | 2 | 7 | — | 9 |
| 11 | 0 | 11 | 17 | — | 28 |
| 12 | 11 | 1 | 1 | — | 13 |
| 13 | 2 | 7 | 3 | — | 12 |
| 14 | 1 | 5 | 3 | — | 9 |
| 15 | 0 | 0 | 9 | — | 9 |
| 16 | 27 | 4 | 3 | — | 34 |
| 17 | 3 | 4 | 1 | — | 8 |
| 18 | 4 | 0 | 6 | — | 10 |
| 19 | 0 | 0 | 10 | — | 10 |
| 20 | 0 | 0 | 8 | — | 8 |
| 21 | 3 | 2 | 16 | 1 | 22 |
| 22 | 0 | 0 | 9 | — | 9 |
| 23 | 0 | 0 | 10 | — | 10 |
| 24 | 0 | 0 | 6 | — | 6 |
| 25 | 0 | 5 | 5 | — | 10 |
| 26 | 0 | 0 | 8 | — | 8 |
| **Total** | **74** | **107** | **192** | **1** | **374** |
 
### Listado por clase
 
**NO FUNCIONAL (107)**
 
| Cap. | Códigos (sufijo NN) |
|---|---|
| 02 | 01, 02, 05, 08, 10, 12, 14 |
| 03 | 02, 04, 14, 15, 16, 17, 21, 22, 23 |
| 04 | 08, 09 |
| 05 | 05, 08, 17, 18, 20, 23, 29 |
| 06 | 01, 02, 04, 05, 07, 08, 09, 12, 13, 14, 16, 17, 18, 19, 20, 21, 22, 23, 24, 26, 27, 29, 30, 32 |
| 07 | 02, 03, 04, 08, 09, 10, 11 |
| 08 | 02, 03, 04, 08, 09, 12, 14 |
| 09 | 02, 03, 04 |
| 10 | 01, 06 |
| 11 | 01, 06, 07, 08, 09, 10, 11, 12, 14, 15, 16 |
| 12 | 08 |
| 13 | 01, 02, 04, 05, 07, 08, 11 |
| 14 | 01, 03, 04, 07, 09 |
| 16 | 07, 10, 16, 34 |
| 17 | 03, 04, 07, 08 |
| 21 | 06, 07 |
| 25 | 01, 02, 03, 04, 05 |
 
**PROCESO / CONTRACTUAL (192)**
 
| Cap. | Códigos (sufijo NN) |
|---|---|
| 02 | 03, 04, 11, 13 |
| 03 | 01, 03, 05, 06, 07, 08, 09, 13, 20, 24 |
| 04 | 01–07, 10, 11, 12, 13, 14 |
| 05 | 01, 02, 07, 09, 11, 12, 13, 14, 16, 21 |
| 06 | 03, 06, 10, 11, 15, 25, 28, 31, 33, 34 |
| 07 | 01, 05, 06, 07, 12, 13 |
| 08 | 01, 05, 06, 07, 10, 11, 13, 15, 16, 17, 18, 19 |
| 09 | 01, 05, 06, 07, 09, 10 |
| 10 | 02, 03, 04, 05, 07, 08, 09 |
| 11 | 02, 03, 04, 05, 13, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28 |
| 12 | 13 |
| 13 | 03, 09, 10 |
| 14 | 05, 06, 08 |
| 15 | 01–09 (los nueve) |
| 16 | 04, 24, 33 |
| 17 | 02 |
| 18 | 01, 02, 03, 04, 08, 09 |
| 19 | 01–10 (los diez) |
| 20 | 01–08 (los ocho) |
| 21 | 01, 02, 03, 04, 05, 08, 09, 10, 11, 14, 16, 18, 19, 20, 21, 22 |
| 22 | 01–09 (los nueve) |
| 23 | 01–10 (los diez) |
| 24 | 01–06 (los seis) |
| 25 | 06, 07, 08, 09, 10 |
| 26 | 01–08 (los ocho) |
 
**AMBIGUO (1)**
 
| Código | Texto de las bases | Por qué se declara ambiguo |
|---|---|---|
| RT-21.12 | «Se habilitarán espacios de interacción entre las entidades y personas usuarias del sistema, que permitan compartir experiencias de uso» (Deseable) | No se puede determinar del texto si «espacios» designa una funcionalidad de la plataforma (foro, comunidad en línea) o una instancia presencial/programática del servicio de soporte. Se deja sin clasificar en lugar de suponer. |
 
### Códigos mixtos (clasificados por obligación dominante, con componente de otra clase)
 
| Código | Clase asignada | Componente secundario |
|---|---|---|
| RT-02.01 | NO FUNCIONAL (arquitectura en 8 capas) | Entregable: diagrama de arquitectura lógica |
| RT-05.04 | FUNCIONAL (validación en captura + tablero de calidad) | NF: conformidad ISO/IEC 25012 |
| RT-05.07 | PROCESO (declarar política de retención) | Funcional: procedimiento verificable de eliminación segura |
| RT-05.09 | PROCESO (presentar estrategia MDM) | Funcional: evitar duplicación de entidades compartidas |
| RT-05.16 | PROCESO (documentar OpenAPI/AsyncAPI) | Funcional: generación automática desde el código |
| RT-08.14 | NO FUNCIONAL (alcance) | Remite a la capacidad funcional de RT-03.18 |
| RT-12.05 | FUNCIONAL (RBAC/ABAC) | Entregable: matriz de segregación de funciones |
| RT-13.01 | NO FUNCIONAL (WCAG 2.2 AA) | Entregable: informe de conformidad |
| RT-13.08 | NO FUNCIONAL (condiciones de terreno) | Solapa la operación sin conexión de RT-03.10 y RT-17.01 |
| RT-17.05 | FUNCIONAL (borrado y bloqueo remoto) | NF: cifrado de la información en el dispositivo |
| RT-18.06 | FUNCIONAL (desactivación del componente) | Proceso: procedimiento manual de respaldo |
| RT-21.11 | PROCESO (servicio de capacitación en línea) | Funcional: registro de avance para monitoreo |
| RT-21.15 | FUNCIONAL | El sujeto es la herramienta de mesa de ayuda, no la solución de negocio |
| RT-25.08 | PROCESO (entregable de la propuesta) | Describe comportamiento del prototipo, no de la solución |
 
---
 
## 3) Requisitos clasificados como FUNCIONAL (74)
 
| Código | Materia | Comportamiento exigido |
|---|---|---|
| RT-02.06 | Idempotencia de escrituras | Ante reintentos de una misma escritura, reconoce la clave de idempotencia y no duplica el efecto dentro de la ventana de deduplicación documentada. |
| RT-02.07 | Entrega y orden de eventos | Entrega cada evento al menos una vez, deduplica en el consumidor y conserva el orden dentro de la partición o del agregado cuando el proceso lo exige. |
| RT-02.09 | Degradación elegante | Ante la indisponibilidad de un componente no crítico continúa operando en modo reducido e informa la degradación a la persona usuaria, sin fallar de forma total. |
| RT-03.10 | Operación autónoma desconectada | El componente on-premise sigue operando de forma autónoma y degradada durante al menos 24 horas continuas sin enlace con la nube. |
| RT-03.11 | Registro local en desconexión | Durante la operación desconectada continúa registrando localmente las transacciones operacionales críticas, con integridad garantizada y sin pérdida de datos. |
| RT-03.12 | Sincronización y reconciliación | Restablecido el enlace, sincroniza automáticamente, resuelve conflictos de forma determinista según regla documentada y deja bitácora auditable de las decisiones aplicadas. |
| RT-03.18 | Gestión remota de dispositivos | Administra remota y centralizadamente los dispositivos de borde y terreno: inventario, configuración, actualización de firmware y de aplicación, bloqueo y borrado remoto. |
| RT-03.19 | Procesamiento en el borde *(Deseable)* | Filtra, agrega previamente o infiere localmente en el borde, reduciendo el volumen transferido y la dependencia del enlace. |
| RT-05.03 | Trazabilidad de operaciones | Permite reconstruir quién, qué, cuándo, desde qué dispositivo y con qué valores anteriores y posteriores, para cualquier registro y en cualquier momento del período de retención. |
| RT-05.04 | Calidad de datos | Valida en el punto de captura y expone un tablero de calidad al CLIENTE con indicadores de completitud, exactitud y consistencia. |
| RT-05.06 | Exportación total de la información | Exporta la totalidad de la información del CLIENTE en formatos abiertos y documentados, en cualquier momento del Contrato, sin costo adicional y sin intervención del ADJUDICATARIO. |
| RT-05.10 | Catálogo de datos con linaje *(Deseable)* | Rastrea automáticamente el origen de cada indicador de negocio hasta su fuente. |
| RT-05.15 | Repositorio de históricos no migrados *(Según caso)* | Mantiene accesibles para consulta los datos históricos que no se migraron, durante el período de retención que fije el caso. |
| RT-05.19 | Correlación de integraciones | Registra la transacción de entrada y de salida de cada integración con un identificador de correlación común que permite seguir una operación de negocio a través de todos los sistemas involucrados. |
| RT-05.22 | Carga y descarga masiva | Procesa carga y descarga masiva en formatos abiertos, con validación previa, informe de errores por registro y procesamiento parcial. |
| RT-05.24 | Portal de servicios para desarrolladores *(Deseable)* | Publica documentación navegable, ambiente de pruebas y credenciales de prueba autoservidas. |
| RT-05.25 | Capa analítica | Provee tableros operacionales y de gestión construidos sobre los indicadores que defina el caso. |
| RT-05.26 | Filtrado y profundización | Permite filtrar por período, unidad organizacional y dimensiones propias del caso, y profundizar desde el indicador agregado hasta la transacción de origen. |
| RT-05.27 | Autoservicio de informes | Permite al CLIENTE construir sus propios informes sin intervención del ADJUDICATARIO, sobre un modelo semántico documentado. |
| RT-05.28 | Exportación y envío programado de informes | Exporta todo informe en formatos abiertos y permite programar su envío automático por calendario. |
| RT-05.30 | Analítica predictiva *(Deseable)* | Produce predicciones pertinentes al proceso del caso, con modelo, variables, métrica de desempeño y plan de reentrenamiento documentados. |
| RT-07.14 | Restauración granular *(Deseable)* | Restaura a elección un registro, una tabla, un módulo o el sistema completo. |
| RT-09.08 | Degradación controlada por capacidad | Al superarse la capacidad encola, limita la tasa y entrega mensaje explícito a la persona usuaria, sin error genérico ni pérdida silenciosa de transacciones. |
| RT-12.01 | Identidad federada | Autentica de forma centralizada mediante OpenID Connect y OAuth 2.1, o SAML 2.0, e integra el directorio corporativo del CLIENTE por LDAP o equivalente en nube. |
| RT-12.02 | Inicio de sesión único | Una sola autenticación habilita todos los módulos y el cierre de sesión se propaga a todos ellos. |
| RT-12.03 | Autenticación multifactor | Exige segundo factor a personas administradoras, a todo acceso privilegiado y a todo acceso originado fuera de la red corporativa. |
| RT-12.04 | Factores resistentes a suplantación *(Deseable)* | Admite FIDO2 o claves de acceso, al menos para los perfiles administradores. |
| RT-12.05 | Control de acceso por roles y atributos | Autoriza por rol, y por atributos donde el proceso lo exija, respetando la matriz de segregación de funciones. |
| RT-12.06 | Acceso privilegiado | Concede elevación temporal a demanda con aprobación previa y graba la sesión en las operaciones de mayor riesgo. |
| RT-12.07 | Gestión de sesión | Aplica duración máxima, caducidad por inactividad, renovación de la credencial tras autenticar, revocación inmediata y control de sesiones concurrentes. |
| RT-12.09 | Auditoría del ciclo de vida de la identidad | Registra creación, modificación, elevación, bloqueo y baja de cuentas, con no repudio y retención declarada. |
| RT-12.10 | Aprovisionamiento automatizado | Crea y da de baja cuentas de forma automatizada y ligada al ciclo de vida laboral, con baja efectiva en no más de 24 horas desde la desvinculación. |
| RT-12.11 | Autenticación adaptada al terreno *(Según caso)* | Ofrece un mecanismo de autenticación operable en el perfil real del caso: uso con guantes, dispositivos compartidos por turno, baja alfabetización digital y ausencia de correo personal. |
| RT-12.12 | Registro y recuperación de usuarias externas *(Según caso)* | Permite a las personas usuarias externas registrarse, verificar su identidad y recuperar su acceso de forma autoservida y segura. |
| RT-13.06 | Retroalimentación y manejo de errores | Entrega retroalimentación visual clara ante cada acción y, ante error, indica qué ocurrió y qué hacer, sin mensajes técnicos dirigidos a la persona usuaria final. |
| RT-13.12 | Modo oscuro, personalización e idiomas *(Deseable)* | Permite alternar modo oscuro, personalizar la interfaz por persona usuaria y operar en varios idiomas cuando el caso lo justifique. |
| RT-14.02 | Tableros permanentes para el CLIENTE | Da al CLIENTE acceso propio y permanente a los tableros operacionales y de negocio, con datos en tiempo real y capacidad de exportación. |
| RT-16.01 | Módulo de administración | Permite al CLIENTE gestionar personas usuarias, roles, permisos, unidades organizacionales y sus jerarquías, sin intervención del ADJUDICATARIO. |
| RT-16.02 | Parametrización de reglas de negocio | Permite configurar desde la interfaz umbrales, plazos, montos, tolerancias, catálogos, listas de valores y textos de notificación, con control de versiones y registro de quién cambió qué y cuándo. |
| RT-16.03 | Doble aprobación de parámetros | Exige aprobación de un segundo perfil para todo cambio de parámetro con impacto operacional y lo registra con su justificación. |
| RT-16.05 | Simulación de parámetros *(Deseable)* | Permite probar el efecto de un cambio de parámetro antes de aplicarlo a producción. |
| RT-16.06 | Registro de auditoría de cambios | Registra toda creación, modificación o eliminación con identificación del autor, fecha y hora con zona horaria, origen, valores anteriores y valores posteriores. |
| RT-16.08 | Consulta y exportación de auditoría | Permite al CLIENTE consultar y exportar la auditoría desde la interfaz, con filtros por persona, período, entidad y tipo de operación, sin acceso a la base de datos. |
| RT-16.09 | Registro de consultas sensibles *(Según caso)* | Registra también las consultas a información sensible, no sólo las modificaciones. |
| RT-16.11 | Motor de flujos de trabajo | Ejecuta flujos con estados, transiciones, responsables, plazos, escalamiento automático por vencimiento y delegación por ausencia. |
| RT-16.12 | Configuración de flujos por el CLIENTE | Permite al CLIENTE modificar sin desarrollo, al menos, responsables, plazos y niveles de aprobación. |
| RT-16.13 | Bandeja de tareas unificada | Muestra a cada responsable sus solicitudes pendientes en una bandeja única, con priorización y alerta de vencimiento. |
| RT-16.14 | Motor de reglas *(Deseable)* | Evalúa condiciones de negocio sin recompilación y deja trazable qué regla se aplicó a cada transacción. |
| RT-16.15 | Gestión documental | Versiona documentos, los indexa por metadatos, controla su acceso, los busca por contenido y por metadato y los previsualiza sin descarga. |
| RT-16.17 | Firma electrónica *(Según caso)* | Firma conforme a la Ley N° 19.799, con firma avanzada donde el caso lo exija, verificando la validez del certificado al momento de la firma. |
| RT-16.18 | Sello de tiempo y evidencia de firma *(Según caso)* | Genera el sello de tiempo y conserva la evidencia que permite verificar el documento después del vencimiento del certificado. |
| RT-16.19 | Generación documental por plantilla | Genera documentos desde plantillas administrables por el CLIENTE, con datos de la transacción y salida en formato abierto. |
| RT-16.20 | Notificación multicanal | Envía notificaciones por al menos tres canales: correo electrónico, notificación en la aplicación y mensajería instantánea o SMS. |
| RT-16.21 | Plantillas de notificación | Permite al CLIENTE administrar las plantillas con variables de la transacción, manteniéndolas versionadas. |
| RT-16.22 | Preferencias de notificación | Permite a cada persona usuaria configurar canal y frecuencia, respetando las notificaciones que el CLIENTE defina como obligatorias. |
| RT-16.23 | Envío confiable de notificaciones | Envía de forma asíncrona, reintenta ante falla, controla duplicados y registra entrega, apertura y error por cada mensaje. |
| RT-16.25 | Baja de comunicaciones | Permite dar de baja las comunicaciones cuando corresponde, conforme a la normativa de comunicaciones comerciales. |
| RT-16.26 | Canales conversacionales *(Deseable)* | Permite a la persona usuaria responder y ejecutar acciones desde el propio canal de mensajería. |
| RT-16.27 | Búsqueda global | Busca sobre índice de texto completo, tolera errores de escritura, ofrece filtros facetados y respeta el control de acceso de quien busca. |
| RT-16.28 | Listados operables | Ordena, filtra, pagina y exporta listados en formatos abiertos, reflejando en la exportación el filtro aplicado. |
| RT-16.29 | Exportación asíncrona | Procesa las exportaciones de gran volumen en segundo plano y notifica al completarse, sin bloquear la sesión. |
| RT-16.30 | Auditoría de exportaciones | Registra en la auditoría quién exportó qué información sensible y cuándo. |
| RT-16.31 | Portal público *(Según caso)* | Publica sin autenticación la información que el caso determine, con los mismos estándares de accesibilidad y desempeño que el resto de la plataforma. |
| RT-16.32 | Autoatención de usuarias externas | Resuelve por autoservicio las consultas de mayor frecuencia, evitando el contacto telefónico para operaciones simples. |
| RT-17.01 | Aplicación móvil con operación sin conexión *(Según caso)* | Opera en terreno sin conexión y sincroniza de forma diferida para los perfiles operacionales que el caso identifique. |
| RT-17.05 | Protección del dispositivo móvil | Cifra la información almacenada en el dispositivo y permite borrarla y bloquearlo remotamente ante pérdida o desvinculación de la persona usuaria. |
| RT-17.06 | Integración de periféricos *(Según caso)* | Opera cámara, lector de códigos, NFC, GPS, impresora de etiquetas y balanza o báscula, según lo que el caso requiera. |
| RT-18.05 | Registro de interacciones de IA | Registra la entrada, la salida y la decisión humana posterior de toda interacción relevante con un componente de inteligencia artificial. |
| RT-18.06 | Desactivación del componente de IA | Permite desactivar el componente sin comprometer la operación del resto de la solución. |
| RT-18.07 | Aviso de resultado automático | Indica expresamente a la persona usuaria que el resultado fue generado o sugerido de forma automática, y su nivel de confianza cuando el modelo lo provea. |
| RT-18.10 | Automatización de back office *(Deseable)* | Automatiza tareas repetitivas de back office mediante automatización robótica de procesos o agentes, con el ahorro de horas cuantificado. |
| RT-21.13 | Indicadores de soporte abiertos | Expone al CLIENTE los indicadores clave del proceso de soporte, y los indicadores específicos según nivel de autorización. |
| RT-21.15 | Registro único de incidentes | Registra incidentes y solicitudes en un canal único con número de ticket, clasificación por severidad y seguimiento del ciclo de vida completo hasta el cierre conforme. |
| RT-21.17 | Cierre de ticket con confirmación | Cierra el ticket sólo con confirmación de la persona usuaria o al transcurrir el plazo de confirmación automática declarado. |
 
Distribución de los 74 funcionales por capítulo: Cap. 16 → 27; Cap. 05 → 13; Cap. 12 → 11; Cap. 03 → 5; Cap. 18 → 4; Cap. 02, 17 y 21 → 3 cada uno; Cap. 13 → 2; Cap. 07, 09 y 14 → 1 cada uno. Los capítulos 04, 06, 08, 10, 11, 15, 19, 20, 22, 23, 24, 25 y 26 no aportan ningún requisito funcional.
 
---
 
## 4) Requisitos etiquetados «Según caso» (21)
 
La etiqueta existe y está definida en el numeral 1.4: requisito obligatorio cuyo valor numérico, umbral o alcance concreto lo fijan las Bases Técnicas del caso; si el caso no lo fija, rige el valor por defecto de este documento y, en su defecto, el criterio de la Comisión Evaluadora.
 
| Código | Materia | Clase asignada | Qué debe aportar el caso |
|---|---|---|---|
| RT-02.12 | Replicación a nuevas unidades sin rediseño | NO FUNCIONAL | Alcance de la multi-tenencia o parametrización requerida |
| RT-03.23 | Red inalámbrica de sitios operacionales | NO FUNCIONAL | Si la requiere y con qué cobertura |
| RT-05.15 | Repositorio de históricos no migrados | FUNCIONAL | Período de retención |
| RT-05.23 | Estándares sectoriales de intercambio | NO FUNCIONAL | Cuáles son |
| RT-05.29 | Latencia transacción → capa analítica | NO FUNCIONAL | Valor; por defecto 4 horas |
| RT-09.02 | Concurrencia y volumen de transacciones | NO FUNCIONAL | Volumetría del caso |
| RT-10.05 | Ventana de mantenimientos programados | PROCESO | Ventana operacional crítica |
| RT-11.10 | Cifrado a nivel de campo | NO FUNCIONAL | Categorías de datos sensibles |
| RT-12.11 | Autenticación adaptada al perfil operacional | FUNCIONAL | Perfil operacional real |
| RT-12.12 | Registro y recuperación de usuarias externas | FUNCIONAL | Tipo de contraparte externa |
| RT-13.08 | Interfaces de terreno (guantes, intemperie, sin conexión) | NO FUNCIONAL | Si el caso lo requiere |
| RT-16.09 | Registro de consultas a información sensible | FUNCIONAL | Si aplica y sobre qué información |
| RT-16.10 | Retención de la auditoría | NO FUNCIONAL | Período; por defecto no inferior a 5 años |
| RT-16.17 | Firma electrónica (avanzada) | FUNCIONAL | Actos que requieren firma avanzada |
| RT-16.18 | Sello de tiempo y evidencia de firma | FUNCIONAL | Actos alcanzados |
| RT-16.31 | Portal público | FUNCIONAL | Información a publicar |
| RT-17.01 | Aplicación móvil con operación sin conexión | FUNCIONAL | Perfiles operacionales alcanzados |
| RT-17.06 | Integración de periféricos | FUNCIONAL | Periféricos requeridos |
| RT-21.07 | Horario del centro de atención | NO FUNCIONAL | Ventana operacional a cubrir 24×7 |
| RT-21.16 | Traslado de especialistas a sitios alejados | PROCESO | Si el caso comprende sitios alejados |
| RT-22.04 | Programación de la capacitación | PROCESO | Estacionalidad y ventana operacional |
 
Composición: 9 FUNCIONAL, 9 NO FUNCIONAL, 3 PROCESO.
 
Nota: fuera de los códigos RT, la etiqueta «Según caso» aparece una vez más en el numeral 15.2, para la «Certificación sectorial específica» de la tabla de certificaciones institucionales. No tiene código RT y por eso no se cuenta entre los 21.
 
---
 
## Declaración de cobertura
 
- Se leyó el documento completo, incluidos los Anexos A a D.
- Se clasificaron los 374 códigos. Ninguno quedó fuera.
- 373 quedaron con clase asignada; 1 (RT-21.12) se declara ambiguo por indeterminación del texto fuente, conforme a la regla de no adivinar.
- La suma por clase (74 + 107 + 192 + 1) reconcilia con 374 y con el conteo por capítulo del Capítulo A.
- Las clases FUNCIONAL / NO FUNCIONAL / PROCESO-CONTRACTUAL son una lectura del equipo Terabyte, no una categoría de las bases. Las bases sólo clasifican por carácter: Obligatorio, Deseable y Según caso.