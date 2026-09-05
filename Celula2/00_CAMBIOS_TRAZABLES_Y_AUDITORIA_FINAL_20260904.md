# Cambios trazables y auditoría final — Célula 2

**Caso:** 06 Portuaria · Terabyte  
**Fecha de cierre documental:** 2026-09-04  
**Destino:** versión de `Celula2/` preparada para compartir con el grupo  
**Alcance:** corrección quirúrgica; no se movió, renombró ni eliminó ningún archivo de trabajo existente.

## 1. Qué certifica este documento

Este archivo deja autocontenida la historia de la corrección de Célula 2. Resume, sin sustituir las fuentes:

1. la disposición de las 31 observaciones remitidas por Célula 3;
2. las 30 correcciones `MC-01` a `MC-30` del Maestro;
3. los cambios efectivamente materializados en los archivos vigentes de Célula 2;
4. las materias aceptadas cuyo desarrollo pertenece a Célula 1, Célula 3, Célula 4, al CLIENTE o a un tercero;
5. los controles ejecutados en la auditoría final y los pendientes que siguen abiertos de manera deliberada.

La disposición recibida desde Célula 2 y la copia conservada en `continuacion_correccion/03_DISPOSICION_CELULA2.md` son iguales en su contenido; solo cambia el nombre del archivo indicado en la línea «Responde a». La disposición aceptó las 31 observaciones: **0 rechazadas**. Aunque el documento original conservaba la etiqueta «borrador de recomendación», la presente versión registra el tratamiento posteriormente adoptado y ya materializado en los archivos. La validación de autoría y aprobación formal del equipo humano no se reemplaza por esta auditoría.

## 2. Autoridad y regla de lectura

Para comprobar una afirmación se utiliza esta jerarquía:

1. PDF oficial del Caso 06;
2. PDF de Bases Técnicas Transversales;
3. PDF de Bases Administrativas;
4. Maestro de correcciones como control consolidado para la intervención;
5. documentos vigentes de `Celula2/` como implementación;
6. archivos de `Historial/` y `Versiones pasadas/` solo como antecedentes.

Los códigos `RT` repetidos nunca se citan solos. La referencia mínima es **documento + capítulo + código + materia**. La trazabilidad usada en esta corrección es:

> fuente normativa → observación `C2` → corrección `MC` → decisión/regla → RF o RNF → criterio de aceptación → archivo vigente → responsable de lo pendiente.

## 3. Resultado ejecutivo

| Control | Resultado auditado |
|---|---|
| Disposición de Célula 2 | 31 observaciones aceptadas; 0 rechazadas |
| Maestro de correcciones | 30 de 30 puntos tratados |
| RF vigentes | **138**, todos con ID único: 30 + 49 + 59 |
| Distribución de primera entrega | **82 Etapa 1 + 56 Etapa 2** |
| RNF vigentes | **84**, todos con ID único, en 9 categorías |
| RF nuevos por el Maestro | `RF-CON-13`, `RF-CON-14`, `RF-APP-01`, `RF-FIR-01` |
| RNF nuevos por el Maestro | `RNF-DIS-11/12`, `RNF-OPE-11/12`, `RNF-CUM-12/13/14` |
| Archivos movidos, renombrados o eliminados | **0** |
| Resultado | **Célula 2 consistente con el Maestro dentro de su responsabilidad** |

La frase final es deliberadamente acotada: algunas correcciones quedan **trazadas y aceptadas**, pero su diseño o acreditación corresponde a otra célula o depende de una confirmación externa. No se presentan como hechos ya confirmados.

## 4. Cómo se resolvieron las 31 observaciones de la disposición

Esta tabla evita confundir las 31 observaciones `C2` con las 30 correcciones `MC`; ambas numeraciones agrupan materias de manera diferente.

| Observación | Disposición aceptada | Correspondencia Maestro | Resultado vigente |
|---|---|---|---|
| `C2-01` | App móvil aceptada | `MC-01` | Creado `RF-APP-01`: una app instalable, cuatro perfiles, offline para los tres perfiles internos; no cuatro aplicaciones |
| `C2-02` | Portal: aceptar con ajuste y usar correspondencia | `MC-06` | `RF-POR-01` completa la capa pública y la matriz de RT-16.30 traza sus nueve prestaciones |
| `C2-03` | Canales aceptados | `MC-03` | Matriz funcional de canales y capacidad compartida de notificaciones con adaptadores |
| `C2-04` | Autenticación aceptada sin reabrir Decisión 12 | `MC-04` | `RNF-SEG-10` y `RNF-USA-04` cubren terminal compartida, guantes, intemperie, relevo, expiración y revocación |
| `C2-05` | Cuatro firmas aceptadas | `MC-05` | Creado `RF-FIR-01`; `RF-INS-06` reutiliza la misma capacidad transversal |
| `C2-06` | Concedente y ferrocarril aceptados | `MC-21` | Actores incorporados en narrativa, portal, integración y volumetría |
| `C2-07` | CCTV aceptado; desarrollo devuelto | `MC-02` | C2 conserva VMS, red segregada y volumetría 142→190; contrato de eventos/metadatos queda a C3 y al levantamiento |
| `C2-08` | Red y radioenlace aceptados; diseño devuelto | `MC-10` | Creado `RNF-DIS-11`; umbrales y diseño físico quedan a C3 |
| `C2-09` | Protección marina aceptada; desarrollo devuelto | `MC-11` | C2 traza la obligación; C3 debe especificar por clase/equipo y llevar cantidades al T-11 |
| `C2-10` | Sala técnica aceptada | `MC-09` | Decisión 20 reabierta a tres alternativas; ninguna elimina el núcleo local de 72 h ni presume ausencia de ambiente marino |
| `C2-11` | Flujo legado→nuevo aceptado | `MC-07` | Creado `RF-CON-13` con secuencia, idempotencia, deduplicación y fallos parciales |
| `C2-12` | Autoridad territorial aceptada | `MC-08` | Creado `RF-CON-14` y matriz conceptual `dominio × zona × fase` |
| `C2-13` | Prueba de contrato aceptada con ajuste | `MC-13` | `RF-CON-02` usa contrato versionado, stub/fixture o versión real; no muta arbitrariamente el TOS comercial |
| `C2-14` | Retorno con doble control/break-glass aceptado | `MC-14` | `RF-CON-04/08` y Decisión 1 distinguen operación normal y emergencia auditada |
| `C2-15` | Retorno por cada intervención aceptado | `MC-27` | Creado `RNF-DIS-12` y control bloqueante de ocho campos |
| `C2-16` | Congelamiento aceptado con ajuste | `MC-30` | Todo lo invasivo listo al 14-dic-2027; dic–abr solo sombra no invasiva condicionada; autoridad desde 01-may-2028 |
| `C2-17` | Fechas inciertas reconocidas | `MC-28` | S5 y consultas mantienen escenario conservador; captura de conocimiento comienza en mes 1 |
| `C2-18` | Exclusividad de mensajería aceptada | `MC-23` | Para la alianza: estándar, cero redigitación y cero puente desde la fecha efectiva; para terceros el puente es transitorio |
| `C2-19` | Ventana/productividad aceptadas | `MC-24` | 100 % de la alianza con ≥72 h; operación general >90 %; ≥30 mov/h por grúa demostrados |
| `C2-20` | Emisiones verificadas aceptadas | `MC-25` | `RF-EMI-05/06`: captura desde mes 1, suficiencia acordada y reporte efectivamente verificado; se retiró el falso mandato de 24 meses |
| `C2-21` | Retenciones diferenciadas aceptadas | `MC-26` | Creado `RNF-CUM-14` y matriz de siete clases con plazo, fin y prueba |
| `C2-22` | Migración/repositorio aceptados con ajuste | `MC-26` | Matriz de seis universos, conciliación y repositorio consultable para el remanente retenido |
| `C2-23` | Inventario de integraciones aceptado con ajuste | `MC-12` | 21 contrapartes lógicas actuales y 7 familias de periferia/instrumentación |
| `C2-24` | Corrección COARRI/CODECO aceptada | `MC-20` | COARRI para carga/descarga; CODECO para gate/custodia compatible; sin suponer 1 sobre por movimiento |
| `C2-25` | Autoridades/ferrocarril aceptados con fallback | `MC-21` | `RF-INT-10`: interfaz cuando exista; canal asistido trazable cuando no; ninguna API inventada |
| `C2-26` | Indicador de posición aceptado con ajuste | `MC-15` | 100 % de posiciones declaradas conocidas correctas; residual ≤0,5 % solo para “por verificar” al cierre y sujeto a acuerdo |
| `C2-27` | Corrección de prioridad nave/gate aceptada | `MC-16` | RN-03 conserva únicamente la excepción operacional del camión con proceso iniciado y umbral comprometido |
| `C2-28` | Soporte crítico diferenciado aceptado | `MC-17` | Creado `RNF-OPE-11` para nave, gate y frío; SLA numérico por clase queda por validar |
| `C2-29` | Capacitación por turnos aceptada | `MC-18` | Creado `RNF-OPE-12`: tres turnos, hasta 380 eventuales/turno, formadores, microcontenidos y congelamiento |
| `C2-30` | Certificaciones/capacidad sectorial aceptadas | `MC-22`, `MC-29` | `RNF-CUM-11/12/13` separan ISO 27001, ISO 9001 y experiencia sectorial; evidencia debe aportarla C1/equipo |
| `C2-31` | Normalización aceptada | `MC-19` | La base de 134 RF se normalizó y después creció legítimamente a 138 por cuatro RF nuevos; IDs únicos y reparto actualizado |

## 5. Matriz completa del Maestro `MC-01` a `MC-30`

### A. Aplicación, canales, identidad y portales

| MC | Cambio y justificación | Evidencia vigente | Estado/continuidad |
|---|---|---|---|
| `MC-01` | Una web responsiva no acredita RT-17.01. Se incorporó una app instalable común con cuatro perfiles; los internos usan almacenamiento cifrado, cola, sincronización idempotente, conflictos deterministas y estado visible de conexión | `01_Requerimientos/Catalogo rf definitivo parte3.md`, `RF-APP-01` | C2 aplicado; C3 debe materializarla en la arquitectura lógica/física |
| `MC-02` | CCTV, acceso y barreras son periféricos existentes a integrar, pero el caso no ordena reemplazar el VMS ni crear un portal de video. Se conserva el subsistema y solo se prevé integración validada de eventos, salud, metadatos o evidencia | `02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`, Decisión 19/D.2; `plantilla_volumetria_caso_portuaria.md` | C2 trazado; contrato, dirección, seguridad, continuidad y prueba pendientes de C3/CLIENTE |
| `MC-03` | RT-16.21 exige públicos y canales distintos. Se creó una matriz transversal: navieras por estándar; terceros por correo/mensajería/app; internos por app/radio; reefer con redundancia, escalamiento y confirmación | `01_Requerimientos/Catalogo rf definitivo parte3.md`, sección transversal de canales | C2 aplicado; C3 debe implementar una capacidad compartida con adaptadores, no sistemas por canal |
| `MC-04` | La autenticación operacional debía funcionar en terminal compartida, con guantes, intemperie y relevo sin detención. Se agregaron expiración/revocación y pruebas reales, sin imponer biometría ni contradecir acuerdos sindicales | `01_Requerimientos/RNF.md`, `RNF-SEG-10`, `RNF-USA-04` | Aplicado |
| `MC-05` | RT-16.14 exige firma en cuatro actos, no solo inspecciones. Se creó una capacidad transversal de firma/evidencia reutilizada por embarque, recepción/entrega, inspección y hechos facturables | `01_Requerimientos/Catalogo rf definitivo parte3.md`, `RF-FIR-01` y `RF-INS-06` | Aplicado |
| `MC-06` | Se completó el portal público con estado mínimo seguro por contenedor, condiciones de acceso y congestión; posición, contenido, ruta e información comercial permanecen protegidos. También se trazaron las nueve prestaciones de RT-16.30 | `01_Requerimientos/Catalogo rf definitivo parte3.md`, `RF-POR-01` y tabla 10.1 | Aplicado; detalle final de “estado” sujeto a respuesta del CLIENTE |

### B. TOS 2012, infraestructura y verificaciones físicas

| MC | Cambio y justificación | Evidencia vigente | Estado/continuidad |
|---|---|---|---|
| `MC-07` | La convivencia no podía ser unidireccional. Se definió captura legado→nuevo con secuencia, idempotencia, deduplicación, cola y comportamiento ante escritura parcial | `01_Requerimientos/Catalogo rf definitivo parte1.md`, `RF-CON-13`; Decisión 1 §§5.2 y 7.1 | C2 aplicado; contrato físico pendiente de levantamiento/C3 |
| `MC-08` | El despliegue por zonas requería una fuente de verdad única. Se definió autoridad por `dominio × zona × fase` y transferencia transaccional cuando un contenedor cruza fronteras | Parte 1, `RF-CON-14`; `02_Decisiones_Reglas_Supuestos/01_decision_01_tos_2012_registro_final.md`, §5.2 | C2 aplicado; C3 debe convertirlo en matriz y diagramas |
| `MC-09` | “Alejar” la sala no elimina la atmósfera marina. La Decisión 20 compara remediar, reemplazar/reubicar dentro del recinto y edge mínimo+nube; todas conservan runtime local para las cinco funciones críticas durante 72 h | `02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`, Decisión 20 | C2 corregido; ADR, protección, capacidad y T-11 pendientes de C3 |
| `MC-10` | RT-03.24 no se cumple con declarar tecnología. Se exigieron pruebas con patio cargado y geometría variable, movilidad/handover y corte real del enlace primario sin pérdida de transacciones | `01_Requerimientos/RNF.md`, `RNF-DIS-11` | C2 aplicado; C3 debe fijar umbrales aprobables de señal/cobertura, latencia y pérdida |
| `MC-11` | La protección marina no admite un único IP genérico. Debe clasificarse por dispositivo y emplazamiento, incluyendo IP, anticorrosión, temperatura, vida útil, reposición y recepción | Registro de supuestos D.2; inventario de periferia en volumetría; este documento | Desarrollo correctamente devuelto a C3/T-11; no es un RF funcional faltante de C2 |
| `MC-12` | El antiguo “18 integraciones” omitía TOS, ERP y periféricos. Se separaron 21 contrapartes lógicas actuales de 7 familias técnicas para no distorsionar el dimensionamiento | `plantilla_volumetria_caso_portuaria.md`, fila 12 y matriz de integraciones | C2 aplicado; protocolos y volúmenes desconocidos permanecen como levantamiento |
| `MC-13` | No se debe probar compatibilidad alterando el esquema de un producto comercial. `RF-CON-02` usa contrato versionado, stub/fixture o una versión real acordada | Parte 1, `RF-CON-02` | Aplicado; prueba ejecutable se desarrolla en T-13/Informe 2 |
| `MC-14` | Se eliminó la reversión unilateral contradictoria: doble control en operación normal y break-glass preautorizado, temporal, motivado, alertado y auditado en emergencia | Parte 1, `RF-CON-04/08`; Decisión 1 §§7.2 y 15.4 | Aplicado; procedimiento detallado corresponde a implantación |

### C. Indicadores, reglas, operación y normalización

| MC | Cambio y justificación | Evidencia vigente | Estado/continuidad |
|---|---|---|---|
| `MC-15` | Se separó exactitud de posición de pendientes explícitos. Toda posición declarada conocida debe ser correcta; el ≤0,5 % se aplica solo a “por verificar” no resueltos al cierre, sin convertirlo en ubicación falsa ni búsqueda ciega | `02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md`, Meta 2 | Aplicado; residual y muestreo deben acordarse con CLIENTE |
| `MC-16` | Congelamiento y ventana de nave restringen intervenciones técnicas, no asignación operacional de equipos. RN-03 retuvo solo la protección al camión cuyo proceso ya comenzó y cuyo indicador quedaría comprometido | `02_Decisiones_Reglas_Supuestos/Registro reglas de negocio v2.md`, RN-03 | Aplicado; regla operacional permanece sujeta a validación del CLIENTE |
| `MC-17` | El soporte general 24x7 no demostraba respuesta diferenciada frente a detención de nave, gate o frío. Se crearon tres clases críticas con medición y prueba extremo a extremo | `01_Requerimientos/RNF.md`, `RNF-OPE-11` | Aplicado; SLA numérico de cada clase por validar |
| `MC-18` | La capacitación debía soportar tres turnos y hasta 380 eventuales rotativos sin intervenir durante congelamiento. Se incorporaron train-the-trainer, microcontenidos y evidencia previa a habilitar funciones críticas | `01_Requerimientos/RNF.md`, `RNF-OPE-12` | C2 aplicado; plan completo corresponde al Subdocumento 7/Informe 2 |
| `MC-19` | Se normalizaron `RF-PAT-09`, referencias a `RF-PAT-13`, huecos retirados y conteos. La base auditada de 134 creció a 138 únicamente por los cuatro RF nuevos del Maestro | Tres catálogos; consolidado de parte 3; narrativa | Aplicado: 138 IDs RF únicos |
| `MC-20` | Se corrigió la semántica marítima: COARRI representa carga/descarga de nave y CODECO gate/custodia compatible. Se distinguieron registros de negocio de sobres de red | Parte 3, `RF-INT-03/04`; volumetría | Aplicado; agrupamiento/versiones se validan por naviera |
| `MC-21` | Se incorporaron concedente, operador ferroviario y autoridades; se prohíbe inventar APIs. Cuando no exista interfaz, se usa canal asistido registrado y probado | Parte 3, `RF-INT-10`, `RF-POR-02`; narrativa; volumetría | C2 aplicado; contratos por contraparte pendientes de levantamiento |
| `MC-22` | ISO 27001 admite certificado o plan en 12 meses; ISO 9001 exige vigencia al ofertar. Se separaron para no trasladar indebidamente la alternativa | `01_Requerimientos/RNF.md`, `RNF-CUM-11/12` | C2 aplicado; acreditación documental corresponde a responsables de la oferta |

### D. Programa 2029, datos, retorno y calendario

| MC | Cambio y justificación | Evidencia vigente | Estado/continuidad |
|---|---|---|---|
| `MC-23` | Las tres condiciones 2029 son un programa indivisible. Para las líneas de la alianza, la mensajería debe ser estándar, exclusiva y sin redigitación/puente desde la fecha efectiva; el puente solo es transición para las demás | Parte 3, `RF-INT-01/02/07`; Meta 15; narrativa | Aplicado; fecha y líneas exactas por confirmar |
| `MC-24` | Se separaron tres resultados: 100 % de confirmaciones de la alianza con ≥72 h; cumplimiento general >90 %; productividad ≥30 mov/h por grúa demostrada en operación representativa, no solo consultada | Parte 3, `RF-NAV-03/12`; metas consolidadas | Aplicado; universo, período y exclusiones deben acordarse |
| `MC-25` | El caso pide un reporte efectivamente verificado, no solo exportable, y no impone 24 meses. Se inicia captura en mes 1, se acuerda suficiencia temprana con el verificador y se exige informe verificado antes del hito 2029 | Parte 3, `RF-EMI-05/06`; narrativa | Aplicado; historia mínima y fecha efectiva quedan abiertas |
| `MC-26` | Se consolidaron los siete plazos de retención y los seis universos de migración, con conciliación, eliminación/anonimización, recuperación y repositorio consultable para el histórico retenido no migrado | `01_Requerimientos/RNF.md`, `RNF-CUM-14`; Decisión 1 §15.1; registro trazable §§3.1–3.2 | C2 aplicado; arquitectura de datos corresponde a C4 y pruebas/costo a entregas posteriores |
| `MC-27` | RT-10.05 exige retorno y tiempo máximo para toda intervención, no solo cutover. Se creó requisito y control bloqueante para software, red, firmware, infraestructura, instrumentación y migración | `01_Requerimientos/RNF.md`, `RNF-DIS-12`; registro trazable §4 | Aplicado; procedimiento completo corresponde a gestión de cambios |
| `MC-28` | No se inventaron meses de soporte/retiro. Se mantiene escenario conservador, captura de conocimiento desde mes 1 y perfilado/extracción temprana para desacoplarse del último mes de soporte | S5 y consultas C2/C4; Decisión 1 §§15.1, 15.5 y 15.6 | Aplicado como supuesto y mitigación; fechas continúan externas |
| `MC-29` | La experiencia sectorial debe acreditarse, no mencionarse. Se creó RNF separado para conocimiento ISPS/OIV y experiencia verificable en TOS o mensajería marítima | `01_Requerimientos/RNF.md`, `RNF-CUM-13` | C2 aplicado; evidencia efectiva corresponde a C1/equipo/T-6 |
| `MC-30` | Se eliminó la contradicción de terminar en enero algo que debía desplegarse antes del congelamiento. Versión, infraestructura, migración, pruebas, retorno y capacitación quedan listas al 14-dic-2027; hasta 30-abr solo sombra condicionada; autoridad desde 01-may | `RNF-DIS-09`; S3; Decisión 1 §8 | Aplicado; si CLIENTE rechaza sombra, se replanifica fuera del congelamiento |

## 6. Cambios por archivo compartido

| Archivo vigente | Cambios principales |
|---|---|
| `01_Requerimientos/Catalogo rf definitivo parte1.md` | Se agregaron `RF-CON-13/14`; se corrigieron contrato, doble control y retorno de `RF-CON-02/04/08` |
| `01_Requerimientos/Catalogo rf definitivo parte2.md` | Se normalizaron IDs y referencias PAT; se preservaron 49 fichas; se aclaró la operación reefer en ambos sentidos mediante sus reglas vinculadas |
| `01_Requerimientos/Catalogo rf definitivo parte3.md` | Se agregaron `RF-APP-01` y `RF-FIR-01`; se corrigieron integración, portal, 2029, COARRI/CODECO, emisiones y matriz de cobertura |
| `01_Requerimientos/RNF.md` | Se ajustaron congelamiento, autenticación y terreno; se agregaron red/failover, retorno, soporte crítico, capacitación, certificaciones separadas, capacidad sectorial y retención exacta |
| `02_Decisiones_Reglas_Supuestos/01_decision_01_tos_2012_registro_final.md` | Convivencia bidireccional, autoridad por zona/fase, retorno consistente, repositorio histórico, captura temprana y calendario corregido |
| `02_Decisiones_Reglas_Supuestos/Registro reglas de negocio v2.md` | RN-03 corrigió la prioridad nave/gate; RN-01/RN-10 explicitan tratamiento reefer para importación y exportación |
| `02_Decisiones_Reglas_Supuestos/Registro_supuestos_v3.md` | Decisión 20 reabierta; programa 2029 indivisible; posición conocida vs. por verificar; CCTV sin portal inventado; supuestos externos visibles |
| `plantilla_volumetria_caso_portuaria.md` | 21 contrapartes + 7 familias; COARRI/CODECO corregidos; CCTV 142→190 segregado; red cargada y volúmenes inciertos señalados |
| `04_Narrativa_Subdoc3/Grupos interes y cierre pendientes.md` | Actores completados, conteo 138, programa 2029 corregido y pendientes externos explicitados |
| `03_Trazabilidad_y_Bases/registro_correccion_plan_maestro_20260904.md` | Registro original de la intervención, matrices de datos, control de retorno y auditoría 30/30 |

## 7. Pendientes que permanecen abiertos sin invalidar el cierre de Célula 2

| Pendiente | Tratamiento actual | Responsable/instancia |
|---|---|---|
| Fecha efectiva y líneas de la alianza en 2029 | Planificar conservadoramente; no degradar exclusividad | CLIENTE/área comercial |
| Historia suficiente para emisiones | Captura desde mes 1, acuerdo temprano y pre-verificación | Verificador/alianza |
| Sombra durante congelamiento | No se considera autorizada hasta respuesta formal; si se rechaza, reprogramar | Consulta C1/CLIENTE |
| Mes de fin de soporte TOS | S5 usa el escenario más exigente y mantiene holgura | Consulta C2/fabricante/CLIENTE |
| Retiro del planificador | Captura de conocimiento desde mes 1 | Consulta C4/CLIENTE |
| Interfaces de TOS, VMS, autoridades, ferrocarril, radio, grúas y periféricos | No inventar API, protocolo ni evento; levantar contrato y fallback | C3/CLIENTE/fabricantes |
| Protección marina | Especificar por clase y emplazamiento; cantidades y periodicidad al T-11 | C3 |
| SLA de nave, gate y frío | Mantener clases separadas; fijar y probar números de extremo a extremo | C3/CLIENTE |
| Evidencia ISO 9001, ISO 27001 y sectorial | Los RNF están creados, pero el certificado/proyecto verificable debe existir | C1/equipo/T-6 |
| `RF-PAT-07` | Ficha redactada, pero el catálogo aún la declara pendiente de validación interna | Rodolfo e Isidora |

Estos puntos no deben convertirse silenciosamente en supuestos confirmados. Tampoco deben interpretarse como que C2 no aplicó el Maestro: son las validaciones y desarrollos que el propio Maestro y la disposición asignan fuera de C2.

## 8. Matrices exactas heredadas por arquitectura, datos y pruebas

### 8.1 Retención

| Conjunto | Plazo | Tratamiento al vencer | Evidencia mínima |
|---|---:|---|---|
| Movimientos | 10 años | Eliminación controlada | Consulta y recuperación por contenedor/período |
| Temperatura reefer | 5 años | Eliminación controlada | Continuidad de serie y recuperación de evidencia |
| Evidencia facturable | 6 años | Eliminación controlada | Correspondencia 1:1 entre hecho y evidencia |
| VGM | 5 años | Eliminación controlada | Recuperación de pesaje, tolerancia y trazabilidad |
| Imágenes OCR | 12 meses | Eliminación o anonimización controlada | Prueba de límite y log de borrado |
| Accesos | 5 años | Eliminación controlada | Consulta por credencial, zona y tiempo |
| Telemetría | 2 años en línea | Agregación histórica por plazo declarado y eliminación granular | Comparación granular/agregado y log de ciclo de vida |

### 8.2 Migración

| Conjunto | Alcance | Conciliación | Remanente |
|---|---|---|---|
| Inventario | Completo con posición verificada físicamente al corte | Recuento, unicidad y barrido por bloque | No aplica |
| Movimientos | 3 años | Recuento por período y secuencia | Años 4–10 en repositorio consultable |
| Hechos/evidencias | 6 años | Relación 1:1, totales y recuperación dirigida | Repositorio durante retención |
| Maestros | Completos | Claves, relaciones y propietario | Exportación documentada |
| Tarifario | Vigente | Reglas, vigencias y excepciones | Histórico asociado a evidencias retenidas |
| Objeciones | Abiertas completas | Recuento, estado, responsable y expediente | Cerradas según retención aplicable |

### 8.3 Control bloqueante de intervención

Ninguna intervención de software, red, firmware, infraestructura, instrumentación o migración se autoriza sin registrar y probar:

1. objetivo y alcance;
2. responsable ejecutor y responsable del retorno;
3. criterio observable de activación;
4. pasos y dependencias del retorno;
5. tiempo máximo;
6. prueba previa y evidencia;
7. ventana operacional y contraste con congelamiento/nave;
8. resultado, conciliación y cierre.

## 9. Correcciones menores detectadas en esta auditoría final

Además del documento de cierre, se realizaron cuatro ajustes de trazabilidad que no alteran el alcance ni los conteos:

1. `RNF-DIS-12` ahora cita expresamente `Caso 06, Cap. 15, RT-10.05 — retorno y tiempo máximo por intervención`.
2. `RNF-OPE-12` ahora cita expresamente `Caso 06, Cap. 15, RT-22.04 — capacitación de turnos/eventuales`.
3. `RNF-CUM-13` ahora cita expresamente `Caso 06, Cap. 15, RT-15.02 — capacidad sectorial`.
4. El resultado esperado de `RF-PAT-09` ahora apunta correctamente al catálogo de condiciones dinámicas `RF-PAT-07`, no a `RF-PAT-08`.

## 10. Veredicto de auditoría

La disposición fue correctamente aceptada y aplicada bajo el criterio recomendado: se corrigió en Célula 2 lo funcional, no funcional, narrativo y de supuestos; se devolvió a Célula 3 lo que pertenece al Subdocumento 4/T-11; se derivó a Célula 1 la evidencia institucional; y se conservaron como consultas los hechos que las bases no permiten inventar.

La carpeta queda apta para compartir como **línea base corregida de Célula 2**, con estas cautelas explícitas:

- “aplicado en C2” no significa que un contrato externo, ADR físico o certificado ya exista;
- el Maestro sigue siendo el control de detalle si se necesita reconstruir el razonamiento completo;
- los archivos históricos no deben usarse como catálogo vigente;
- `RF-PAT-07` continúa sujeto a la validación interna ya declarada;
- cualquier cambio posterior debe mantener la cadena fuente → MC/C2 → RF/RNF → prueba → archivo.

**Conclusión:** no se detectó ningún punto del Maestro omitido en la responsabilidad documental de Célula 2. Los residuos encontrados fueron de referencia y quedaron corregidos; las dependencias externas permanecen visibles, justificadas y asignadas.

---

# Anexo — Segunda ronda de corrección · 2026-09-05

> Este anexo **no modifica** las cifras del cuerpo del documento, que son el estado auditado al 04-09-2026. Registra la ronda posterior, ejecutada tras contrastar el material contra el CP, el BTT y las BA hallazgo por hallazgo. Cada punto se verificó abriendo el archivo citado antes de aplicarlo; los que no resistieron la verificación se descartaron y quedan listados al final.

## Cambios aplicados

| ID | Cambio | Archivo | Fundamento |
|---|---|---|---|
| **B1** | Se agregan **7 RNF**: `RNF-DES-09` a `12` (umbrales del numeral 9.1 del BTT y prueba de carga a 1,5× del peak) y `RNF-DIS-13` a `15` (RTO/RPO, respaldo 3-2-1-1-0, prueba de conmutación real semestral). Catálogo de **84 → 91 RNF** | `01_Requerimientos/RNF.md` | CP, Cap. 17.1 exige incorporar «los parámetros del Capítulo 15 **y los requisitos del documento transversal**». Los primeros estaban cubiertos; estos siete no existían en ninguna parte del material |
| **B2** | Se crea **`RF-POR-09`** (presentación estructurada de la instrucción de embarque por embarcador o agencia) y se acota `RF-INT-02` a la orden de embarque. Catálogo de **138 → 139 RF** | `01_Requerimientos/…parte3.md` | El CP, Anexo A atribuye el 41 % de línea base a «Embarcador o agencia → Documentación». COPRAR es naviera → terminal: integrar las 14 navieras podía dejar el indicador intacto |
| **B3** | `RF-REF-07` acota la alarma de ausencia de dato a **5 minutos**, además de los 3 intervalos de muestreo | `01_Requerimientos/…parte2.md` | Con muestreo de 5 min la ventana ciega llegaba a 15. Un sensor caído es indistinguible de una desconexión —el modo de falla del 18 de febrero— y CP, Cap. 15, RT-05.29 exige ≤5 min. No se reabre la Decisión N° 8 |
| **B4** | Se crea **`RN-11`** (tolerancia de desviación de temperatura) y se enlaza a `RF-REF-04`. Registro de **10 → 11 reglas** | `02_…/Registro reglas de negocio v2.md` · `…parte2.md` | `RF-REF-04` se titulaba «detección de desviación» pero su criterio solo verificaba desconexión, y ninguna regla definía la banda. La regla **no fija valores numéricos**: el caso no los entrega |
| **B5** | Se incorpora el **factor estacional** con sus derivaciones y se aporta la derivación del tiempo de sincronización de la fila 16 | `plantilla_volumetria_caso_portuaria.md` | Tercera particularidad del CP, Cap. 14.2, ausente del archivo. El CP sanciona «valores sin derivación» igual que las celdas vacías |
| **B6** | Se corrige «nueve tensiones» por **seis** y se agrega §3.11 con la correspondencia una a una | `04_Narrativa_Subdoc3/…` | El CP, Cap. 8 nomina seis. La tensión 4 estaba resuelta en la Decisión N° 9 pero sin mapear; la **tensión 1 sigue abierta como conflicto** |
| **B7** | Columna **«Persona en el caso»** en el mapa de actores y dos filas nuevas: jefatura de gate y jefatura de energía | `04_Narrativa_Subdoc3/…` | De los diez entrevistados solo aparecía el planificador. El Subdocumento 2 exige identificar a los actores afectados |
| **B8** | Se completan **Fundamento** en C.1 e **Impacto** y **Fundamento** en C.2 — 17 filas | `02_…/Registro_supuestos_v3.md` | CP, Cap. 17.1: el registro debe traer «su fundamento, su impacto si resulta equivocada y la instancia en que se validará». El de C.1 se **recupera** de la Decisión N° 1 §11 |
| **B9** | `RF-EMI-06` cita `RT-05.06` al **BTT** y no al Cap. 15 del CP | `01_Requerimientos/…parte3.md` | Incumplía la regla §1.5 del propio catálogo |
| **B10** | `RF-PAT-10` entra a los criterios 8 y 10 y al indicador de remociones | `01_Requerimientos/…parte2.md` | Era el único RF que ataca el 18 % de remociones de forma anticipada y no figuraba en ninguna fila de trazabilidad |
| **B11** | Se retira la meta de negocio del criterio de aceptación de `RF-NAV-12`, `RF-NAV-03` y `RF-INS-07` | `01_Requerimientos/…parte3.md` | CP, Cap. 17.1: «un requerimiento no es una frase copiada… es un resultado esperado». Las metas ya viven en la tabla de indicadores del numeral 11.2 |
| **B12** | Encabezado del registro de reglas: **2.0 → 2.2** | `02_…/Registro reglas de negocio v2.md` | El historial ya declaraba una 2.1 que el encabezado no reflejaba; la 2.2 corresponde a `RN-11` |
| **B13** | `matriz_cobertura_rf_fase2(DESFASADA).md` movida a `Historial/` con `git mv` | — | Estaba en la carpeta de línea base con conteos ya superados |

## Conteos vigentes tras esta ronda

| Artefacto | Antes | Ahora |
|---|---:|---:|
| Requerimientos funcionales | 138 | **139** |
| Requerimientos no funcionales | 84 | **91** |
| Reglas de negocio | 10 | **11** |
| Decisiones | 21 | 21 |
| Supuestos declarados | 25 | 25 |

Reparto por primera entrega: **82 en Etapa 1 y 57 en Etapa 2**.

## Hallazgos descartados tras verificación — no reabrir

| Hallazgo | Por qué no aplica |
|---|---|
| «Faltan 7 RNF de los parámetros del Cap. 15» | Ninguna base exige que un parámetro del Cap. 15 sea RNF: el numeral 1.5 del BTT exige responderlos en el T-12 y el CP, Cap. 17.2 deja la clasificación al proponente. Seis de los siete estaban cubiertos fuera de `RNF.md` |
| «Ningún RF captura el movimiento de grúa de muelle» | La cadena `RF-PAT-05` → `RF-PAT-13` → `RF-NAV-12` existe y excluye explícitamente el sistema del fabricante |
| «No hay criterio RF/RNF declarado» | Está en §1.2 del catálogo, parte 1 |
| «Los tres cruces de trazabilidad no tienen reemplazo» | Existen en §11.1 y §11.2 de cada parte del catálogo |
| «La colisión de códigos RT es un hallazgo nuevo» | Ya estaba documentada en §1.5 del catálogo y en el **Supuesto M**, que identifica además `RT-21.06` |
| «§10.3 contradice el umbral de gate con un 0,3 % obsoleto» | §10.3 es el razonamiento que llevó a fijarlo en cero, no una contradicción |
| «`RF-ACC-01` atribuye los ~2.100 eventuales al Cap. 2.4» | Las citas al Cap. 2.4 invocan la **rotación diaria**, que es lo que ese capítulo describe. La cita es correcta |

## Queda abierto y no se resolvió aquí

- **Decisión N° 20** (destino de la sala de servidores): sigue enunciada como «se resolverá mediante un ADR comparando tres alternativas». Célula 2 la clasifica correctamente como arquitectura física; corresponde confirmarla con **Célula 3** en el Subdocumento 4.
- **Tensión 1** del CP, Cap. 8 (Comercial vs. Operaciones) como conflicto, no como dos objeciones separadas.
- **Etapa de `RF-POR-09`**: asignado a Etapa 2 por coherencia con su dominio. Si se adelanta a Etapa 1 por su efecto sobre el criterio 13, el reparto de la sección 11.3 debe actualizarse.
- **Universo de instrumentación**: el CP, Cap. 14.1 define 74 equipos (18 grúas de patio, 42 tractocamiones, 14 pesados) y **no incluye las 6 grúas de muelle**. Conviene declarar en el catálogo qué evento produce el movimiento de muelle.
