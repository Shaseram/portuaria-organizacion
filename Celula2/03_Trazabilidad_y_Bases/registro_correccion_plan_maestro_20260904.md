# Registro trazable de corrección contra el Plan Maestro

**Fecha de aplicación:** 2026-09-04  
**Alcance:** Célula 2, corrección quirúrgica sin mover, renombrar ni eliminar archivos existentes.  
**Autoridad:** `continuacion_correccion/01_MAESTRO_CORRECCIONES.md`. Ante cualquier contradicción, el Plan Maestro prevalece sobre este registro y sobre los documentos de Célula 2.  
**Base preservada:** se mantuvieron las fichas, decisiones, reglas, supuestos, narrativa y volumetría existentes; se modificaron únicamente los puntos afectados y se agregó este registro en la carpeta de trazabilidad ya existente.

## 1. Inventario vigente después de la corrección

| Producto | Archivo vigente | Resultado controlado |
|---|---|---|
| RF — convivencia y gate | `../01_Requerimientos/Catalogo rf definitivo parte1.md` | 30 RF; incluye `RF-CON-13` y `RF-CON-14` |
| RF — patio, tractocamiones, reefer, acceso y operación desconectada | `../01_Requerimientos/Catalogo rf definitivo parte2.md` | 49 RF; dominio PAT normalizado a 13 fichas |
| RF — nave, integración, facturación, portal, inspecciones, emisiones, app y firma | `../01_Requerimientos/Catalogo rf definitivo parte3.md` | 59 RF; incluye `RF-APP-01` y `RF-FIR-01` |
| RNF | `../01_Requerimientos/RNF.md` | 84 RNF vigentes en 9 categorías |
| Decisión TOS | `../02_Decisiones_Reglas_Supuestos/01_decision_01_tos_2012_registro_final.md` | Convivencia bidireccional, autoridad territorial, retorno y calendario coherentes |
| Reglas de negocio | `../02_Decisiones_Reglas_Supuestos/Registro reglas de negocio v2.md` | 10 reglas; reefer cubre importación y exportación |
| Decisiones, metas y supuestos | `../02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md` | 21 decisiones, 17 metas y 25 supuestos; correcciones maestras incorporadas |
| Volumetría | `../plantilla_volumetria_caso_portuaria.md` | 18 dimensiones y matriz controlable de integraciones |
| Narrativa | `../04_Narrativa_Subdoc3/Grupos interes y cierre pendientes.md` | Actores, programa 2029 y conteos actualizados |

**Conteo vigente del catálogo funcional:** 30 + 49 + 59 = **138 RF en 15 dominios**.  
**Conteo vigente del catálogo no funcional:** **84 RNF**.  
Los archivos bajo `Historial/` y `Versiones pasadas/` son evidencia histórica y no son fuente vigente.

## 2. Matriz de aplicación MC-01 a MC-30

| MC | Corrección aplicada en Célula 2 | Evidencia principal | Estado |
|---|---|---|---|
| MC-01 | Se creó una sola app instalable con cuatro perfiles, incluyendo operación interna offline y evolución del conductor | `RF-APP-01` | Aplicado |
| MC-02 | No se inventó portal de cámaras ni RF de CCTV; se conserva VMS y se anticipa adaptador solo para contratos confirmados | Registro de supuestos D.2; volumetría | Aplicado; contrato C3 pendiente |
| MC-03 | Se incorporó matriz de canales: estándar navieras, canales asistidos para terceros, app/radio internos y redundancia reefer | Sección RF-INT, parte 3 | Aplicado |
| MC-04 | Autenticación operativa ampliada a guantes, intemperie, terminal compartido, expiración/revocación y relevo sin pausa | `RNF-SEG-10`, `RNF-USA-04` | Aplicado |
| MC-05 | Firma común para los cuatro actos obligatorios, sin duplicar motores de firma | `RF-FIR-01`, `RF-INS-06` | Aplicado |
| MC-06 | Portal público completado y limitado a datos no sensibles; se trazaron los nueve elementos de RT-16.30 | `RF-POR-01` y sección de correspondencia, parte 3 | Aplicado |
| MC-07 | Se agregó captura legado→nuevo con orden, idempotencia, deduplicación y fallos parciales | `RF-CON-13`; Decisión 1 §§5.2 y 7.1 | Aplicado |
| MC-08 | Se fijó autoridad única por dominio×zona×fase y transferencia transaccional al cruzar zonas | `RF-CON-14`; Decisión 1 §5.2 | Aplicado |
| MC-09 | Decisión de sala local reabierta como comparación de tres alternativas, manteniendo autonomía de 72 h | Decisión 20 en Registro de supuestos | Aplicado; ADR C3 pendiente |
| MC-10 | Se volvió verificable la red con patio cargado y failover real | `RNF-DIS-11` | Aplicado; diseño C3 pendiente |
| MC-11 | No se fijó un único grado IP: la protección marina queda por familia y emplazamiento | Registro maestro como condición de C3; matriz de periferia | Trazado a C3; especificación pendiente |
| MC-12 | Inventario rehecho: 21 contrapartes lógicas actuales y 7 familias técnicas | Volumetría, fila 12 y matriz posterior | Aplicado |
| MC-13 | Prueba del legado por contrato versionado/stub/versión real; se eliminó la mutación arbitraria del esquema | `RF-CON-02` | Aplicado |
| MC-14 | Retorno normal con doble control y emergencia con break-glass preautorizado y auditado | `RF-CON-04`, `RF-CON-08`; Decisión 1 §§7.2 y 15.4 | Aplicado |
| MC-15 | Se separaron 100% de exactitud de posiciones conocidas y residual por verificar ≤0,5% al cierre de turno | Meta 2; trazas de parte 3 | Aplicado; residual a validar con CLIENTE |
| MC-16 | RN-03 conserva solo la excepción por umbral de un camión ya iniciado; congelamiento no asigna recursos operacionales | RN-03 | Aplicado |
| MC-17 | Soporte crítico diferenciado para nave, gate y frío | `RNF-OPE-11` | Aplicado; SLA numérico por clase a validar |
| MC-18 | Capacitación cubre tres turnos, 380 eventuales/turno, formadores y prohibición de congelamiento | `RNF-OPE-12` | Aplicado |
| MC-19 | Identificadores y conteos normalizados: PAT09/PAT13; 138 RF; 84 RNF | Tres catálogos y narrativa | Aplicado |
| MC-20 | CODECO se usa en gate/custodia; COARRI en carga/descarga; registros se separan de mensajes de red | `RF-INT-03/04`; volumetría | Aplicado |
| MC-21 | Autoridades, ferrocarril y concedente aparecen como contrapartes explícitas, sin inventar APIs | `RF-INT-10`; volumetría; narrativa | Aplicado; contratos por levantar |
| MC-22 | ISO 27001, ISO 9001 y capacidad sectorial se separaron según condición exacta | `RNF-CUM-11/12/13` | Aplicado |
| MC-23 | Para alianza: estándar exclusivo, cero redigitación y cero puente desde vigencia 2029 | `RF-INT-01/02/07`; meta 15 | Aplicado; fecha exacta pendiente |
| MC-24 | Alianza: 100% con ≥72 h; general >90%; productividad ≥30 mov/h por grúa demostrada | `RF-NAV-03/12`; tabla de metas, parte 3 | Aplicado |
| MC-25 | Captura de emisiones desde mes 1 y reporte realmente verificado antes de exigibilidad; eliminado falso mandato de 24 meses | `RF-EMI-05/06`; narrativa | Aplicado; historia mínima a acordar |
| MC-26 | Se consolidaron matrices exactas de retención y migración, con conciliación y repositorio consultable | `RNF-CUM-14`; Decisión 1 §15.1; §3 de este registro | Aplicado |
| MC-27 | Ninguna intervención se autoriza sin retorno probado, responsable, criterio y tiempo máximo | `RNF-DIS-12`; §4 de este registro | Aplicado |
| MC-28 | Fechas de soporte y retiro siguen como consultas; conocimiento se captura desde mes 1 y se perfila histórico tempranamente | S5, consultas C2/C4 y Decisión 1 §§15.1/15.5/15.6 | Aplicado como supuesto/consulta |
| MC-29 | Capacidad sectorial exigida de forma demostrable | `RNF-CUM-13` | Aplicado |
| MC-30 | Versión/instalación/migración/pruebas/retorno/capacitación listos al 14-dic; luego solo sombra condicionada; autoridad desde 01-may | `RNF-DIS-09`; S3; Decisión 1 §8 | Aplicado; sujeto a C1 |

## 3. Matrices maestras de datos

### 3.1 Retención

| Conjunto | Plazo | Fin del plazo | Prueba mínima |
|---|---:|---|---|
| Movimientos | 10 años | Eliminación controlada al vencer obligación | Consulta y recuperación por contenedor/período |
| Temperatura reefer | 5 años | Eliminación controlada | Continuidad de serie y recuperación de evidencia |
| Evidencia facturable | 6 años | Eliminación controlada | Correspondencia 1:1 con hecho y documento |
| VGM | 5 años | Eliminación controlada | Recuperación de pesaje, tolerancia y trazabilidad |
| Imágenes OCR | 12 meses | Eliminación o anonimización controlada | Prueba en límite temporal y log de borrado |
| Accesos | 5 años | Eliminación controlada | Consulta por credencial, zona y marca de tiempo |
| Telemetría | 2 años en línea | Agregación histórica por plazo declarado y eliminación granular | Comparación de granular vs. agregado y log de ciclo de vida |

### 3.2 Migración

| Conjunto | Alcance obligatorio | Conciliación | Remanente |
|---|---|---|---|
| Inventario | Completo, posición verificada físicamente al corte | Recuento, unicidad y barrido por bloque | No aplica |
| Movimientos | 3 años | Recuento por período y secuencia | Años 4–10 en repositorio consultable |
| Hechos/evidencias | 6 años | Relación 1:1 y totales | Repositorio durante retención |
| Maestros | Completos | Claves, relaciones y dueño de dato | Exportación documentada |
| Tarifario | Vigente | Reglas, vigencias y excepciones | Histórico ligado a evidencias retenidas |
| Objeciones | Abiertas completas | Recuento, estado, responsable y expediente | Cerradas según retención aplicable |

## 4. Control bloqueante de intervención

Toda intervención —software, red, firmware, infraestructura, instrumentación o migración de zona— debe registrar antes de aprobación:

1. objetivo y alcance exacto;
2. responsable ejecutor y responsable de autorizar retorno;
3. criterio observable que activa el retorno;
4. pasos y dependencias del retorno;
5. tiempo máximo comprometido;
6. prueba previa y evidencia;
7. ventana operacional y verificación contra congelamiento/nave;
8. resultado, conciliación y cierre posterior.

Sin los ocho campos completos y retorno probado, el cambio no se aprueba.

## 5. Decisiones abiertas que no autorizan supuestos nuevos

| Pendiente | Tratamiento conservador hasta resolver | Instancia |
|---|---|---|
| Fecha efectiva del acuerdo de alianza en 2029 | Planificar contra la fecha más temprana razonable | Consulta/confirmación comercial |
| Historia mínima para reporte de emisiones | Capturar desde mes 1 y acordar temprano con verificador/alianza | Preverificación |
| Validación de solo lectura durante congelamiento | No tratarla como autorizada hasta respuesta; replanificar si se rechaza | C1 |
| Mes exacto de fin de soporte TOS | Mantener supuesto exigente y holgura | C2 |
| Mes exacto de retiro del planificador | Captura desde mes 1 | C4 |
| Contratos de autoridades, ferrocarril, VMS y periféricos | No inventar API, protocolo ni evento no confirmado | Levantamiento y ADR C3 |
| Protección marina por equipo | Clasificar por exposición; no declarar IP único | Diseño y recepción C3 |
| SLA numérico por servicio crítico | Mantener clases separadas y probar extremo a extremo | Catálogo de servicio con CLIENTE |

## 6. Regla de mantenimiento

Toda corrección futura debe citar: **MC o fuente base → decisión/regla → RF o RNF → prueba/aceptación → archivo afectado**. Si cambia un identificador o conteo, se actualizan en la misma intervención los tres catálogos, el registro de supuestos, la narrativa y este inventario. La matriz marcada `DESFASADA` no debe utilizarse como fuente vigente.

## 7. Auditoría posterior a la aplicación

| Control | Resultado |
|---|---|
| Correcciones maestras trazadas | **30 de 30** (`MC-01` a `MC-30`) |
| RF vigentes | **138**: 30 + 49 + 59 |
| IDs RF duplicados | **0** |
| RNF vigentes | **84** |
| IDs RNF duplicados | **0** |
| Supuestos declarados | **25**: S1–S5, A–L y M–T |
| Patrones obsoletos en fuentes vigentes | **0** para `RF-PAT-14`, `RF-PAT-9`, “18 integraciones”, mandato de “al menos 24 meses”, reversión unilateral y fin de Etapa 1 en ene-2028 |
| Referencias RF sin ficha | Solo `RF-OPD-03` y `RF-OPD-04`, mencionados expresamente como identificadores retirados y no reutilizados; no son dependencias activas |
| Estructura de archivos | Ningún archivo existente movido, renombrado ni eliminado; se agregó únicamente este registro en la carpeta de trazabilidad existente |

**Conclusión de auditoría:** la capa documental de Célula 2 queda internamente consistente con el Plan Maestro en conteos, identificadores y decisiones corregidas. Los puntos que dependen del CLIENTE o de Célula 3 permanecen abiertos y visibles en §5; no se presentaron como hechos confirmados.
