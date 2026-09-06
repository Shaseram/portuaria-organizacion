# D1 — Arquitectura de seguridad

## Contrato del entregable

### Objetivo y destino

Definir Zero Trust, exposición, identidad, cifrado, detección y DevSecOps, y entregar requisitos utilizables por Física desde `v0.1`. Alimenta 4.1.4 y apoya 4.2.3 y 4.2.6.

### Cumplimientos asignados

- `SD4-04`, apoyo a `SD4-02`, `SD4-05` y `SD4-08`.
- T7-4.4; BTT Cap. 11/12; Art. 21/22.
- RNF-SEG, RNF-CUM, RNF-OPE, RNF-DIS-14, RF-POR-02/09 y `MC-04`; obligación directa SOC 24x7 de FEP02 Cap. 11 RT-11.17.
- Corte y consecuencias: Maestro §2.3 y matriz global §3; controles y decisiones siguen pendientes.

### Entradas obligatorias

- Maestro §§5–6, 9–12, 16, 18–19.
- RNF vigente, actores/eventuales y sistemas conservados.
- A1/C1 `v0.1` para refinamiento; no son requisito para iniciar.

### Control de cobertura de entrada

La [traza D1, §2](trazabilidad/TRZ_D1.md) desglosa **FEP02 RT-11.01 a RT-11.28** y §3 registra los estándares del numeral 11.5. Es la lista de comprobación del capítulo, con carácter, referencias, coordinación y evidencia prevista; la cobertura técnica se actualiza por bloque y aún no hay puntos aprobados. Al desarrollar, enlazar sus filas con los controles y secciones concretos sin repetir el texto de las Bases. D2 aporta el modelo de amenazas y los otros frentes completan componentes/despliegue. Se conservan también las entradas de identidad, continuidad y del caso: el capítulo 11 no agota D1.

### Trabajo requerido

**Lectura B7:** `[x]` significa materia desarrollada y trazada a nivel de propuesta; no significa producto seleccionado, prueba ejecutada ni cumplimiento aprobado. La definición de terminado permanece separada.

- [x] Definir principios Zero Trust y flujos de confianza.
- [x] Definir zonas/conductos para nube, on-premise, borde y terceros.
- [x] Diseñar CDN/WAF/DDoS/TLS/HSTS/certificados/bots.
- [x] Diseñar SSO, MFA, RBAC/ABAC, SoD y PAM.
- [x] Resolver eventuales por nombrada y terminal compartida a nivel de propuesta; fuentes/procedimientos reales siguen pendientes.
- [x] Definir cifrado, KMS/HSM, rotación y secretos.
- [x] Definir logs inalterables, SIEM, EDR y alertas portuarias, con SOC 24x7; ubicación/dotación/proveedor siguen pendientes.
- [x] Definir respuesta, plazos de vulnerabilidad e incidentes.
- [x] Definir SAST/SCA/DAST, imágenes, SBOM, firma/SLSA y datos no productivos.
- [x] Mapear control→capa→componente→nodo→amenaza→evidencia; MA-3 cruza 31/31 controles con D2 y los 20 nodos `PHY-*` más `LOC-INSP-01` declarados por C1.
- [x] Preparar componentes/licencias/servicios candidatos a T-11 en `SEC-PHYS-v0.1`; C1–C4 ya incorporan los 17 grupos y conservan productos, cantidades finales y pruebas como pendientes.

### Entrega temprana `SEC-PHYS-v0.1`

**Estado vigente tras MA-3:** `INTEGRADO Y CONCILIADO DOCUMENTALMENTE`. C1 emplaza los 17 grupos, C2 declara su tratamiento tecnológico y C4 registra 6 filas propias de seguridad, 1 capacidad absorbida por la fila unificada de observabilidad/SIEM y 10 grupos incluidos/condicionados. Esto no acredita compra, producto final, cantidad contractual ni prueba. La última columna evita duplicar compras.

| ID control | Capacidad requerida | Componente/servicio candidato | Ubicación/restricción | HA/continuidad | Evidencia | Entrada para T-11 |
|---|---|---|---|---|---|---|
| `SEC-NET-01 / SEC-EXP-01` | segmentación, filtrado e inventario de exposición | firewall/controles de red, host o plataforma; verificación externa | zonas nube/local/operación/administración/protección | rutas críticas redundantes y administración segregada | rutas permitidas/denegadas, escaneo e inventario B3.1–B3.6 | **Condicional:** fila si existe equipo/licencia separada; si viene incluida, C4 lo justifica |
| `SEC-EDGE-01 / SEC-EDGE-02` | CDN, WAF, DDoS, TLS 1.3, HSTS, certificados y bots | servicio de borde gestionado | único borde público nube; origen no expuesto | multi-AZ/HA demostrable; ruta local crítica independiente | bypass, TLS, renovación, abuso y carga legítima B3.3–B3.6 | **Fila propia candidata** de servicio; capacidad/cobertura por C4 |
| `SEC-API-01` | autenticación, autorización, cuota, esquema y payload | API gateway/management con perfil local restringido | perfil central detrás del borde en `PHY-CLD-02`; perfil local obligatorio en `PHY-OPS-01` | HA; operación local 72 h; políticas/contratos vigentes cacheados | identidad/objeto ajeno, esquema, tamaño, tasa, corte y reconciliación B3.3–B3.6 | **Incluido** en la plataforma de gateway/runtime; no duplicar fila por el perfil local |
| `SEC-IAM-01 / SEC-ADM-01 / SEC-PROD-01` | SSO, MFA, RBAC/ABAC, PAM, acceso de terreno y excepción de producción | IAM/PAM; credencial/lector solo si la alternativa elegida lo exige | gobierno híbrido; capacidad local crítica y administración segregada | operación local 72 h, terminal 8 h y HA por validar | matriz, sesiones, relevo, baja, elevación, producción y emergencia B2.3–B2.6/B6.6 | **Filas candidatas** IAM/PAM; lectores/licencias solo con cantidad justificada |
| `SEC-SYNC-01` | conducto autenticado nube/local y reconciliación | canal/broker/conector seguro de integración | no público salvo contrato; identidad técnica acotada | buffer 72 h y sincronización ≤90 min | corte, repetición, orden, integridad y conciliación B3.2/B3.6 | **Incluido normalmente** en integración/red/runtime; fila solo si hay servicio separado |
| `SEC-DATA-01 / SEC-ENC-01 / SEC-FIELD-01` | cifrado de reposo/campo y acceso por clasificación | capacidades nativas de almacén/aplicación o servicio de cifrado de campo | todos los almacenes/copias; descifrado solo por servicio autorizado | claves recuperables y operación local según dato | configuración y consulta directa sin revelar campos B4.1–B4.3 | **Incluido o condicional:** no crear fila por cada dato; separar licencia/servicio solo si existe |
| `SEC-KEY-01 / SEC-SECRET-01` | claves, certificados, secretos y firma | KMS/HSM/vault con capacidad local protegida | gobierno común y ámbitos nube/local separados; raíz no exportable | operación local 72 h, HA, rotación y recuperación | no exportación, corte, rotación, uso y recuperación B4.4–B4.8 | **Fila propia candidata**; consolidar KMS/HSM/vault sin duplicar funciones incluidas |
| `SEC-BKP-01` | respaldo cifrado, inmutable y recuperable con claves separadas | plataforma/servicio de respaldo definido por C2/C3 | fuera de sitio y copia inmutable/fuera de línea | 3-2-1-1-0, RTO/RPO y restauración mensual | borrado resistido y restauración descifrable B4.5/B4.7 | **Condición de la fila de respaldo**, no segunda compra de D1 |
| `SEC-LOG-01 / SEC-SIEM-01` | registro inalterable, correlación y casos portuarios | plataforma SIEM/log + colectores/buffer local | fuentes nube, on-premise y terreno; repositorio central | buffer 72 h + margen; 12 meses en línea +24 archivados | política de admisión/estimación de volumen, integridad, corte/reenvío, archivo y reglas B5.1–B5.3/B5.7 | **Fila propia candidata**; C4 dimensiona ingesta, retención y licencias desde B5.2.1, sin copiar al SIEM toda la telemetría operacional |
| `SEC-END-01` | detección/respuesta en cargas y endpoints compatibles | EDR con agentes/consola y controles compensatorios | nube, on-premise y puestos administrados | detección local y reenvío posterior | inventario, detección y aislamiento seguro B5.2/B5.7 | **Fila propia candidata** por cargas/endpoints; cantidad desde inventario C1/C2 |
| `SEC-SOC-01 / SEC-IR-01` | monitoreo 24x7 y respuesta a incidentes | SOC gestionado/subcontratado + gestión de casos | ubicación/residencia y acceso por declarar | turnos, suplencias, canal alternativo y salida del proveedor | ejercicio evento→triage→comunicación/RCA B5.4–B5.7 | **Fila propia candidata de servicio**, costeada sin asignarla silenciosamente a TI=5 |
| `SEC-VULN-01` | escaneo continuo y gestión 7/15/30 | plataforma/licencias y servicio especializado | nube, on-premise, aplicaciones y superficie externa | seguimiento continuo y excepciones gobernadas | cobertura, antigüedad, cierre y reprueba B5.6/B5.7 | **Fila propia o incluida** en servicio de seguridad; C4 evita doble conteo |
| `SEC-PENTEST-01` | pentest independiente anual y antes de producción | servicio de tercero independiente | alcance completo autorizado | calendario y reprueba | contrato, independencia, informe íntegro y remediación B5.6/B5.7 | **Fila propia candidata de servicio** si T-11 admite/recibe el servicio; validar con C4 |
| `SEC-SDLC-01 / SEC-PIPE-01` | repositorio gobernado y puertas DevSecOps | CI/CD + SAST/SCA/DAST/secretos/imágenes | ingeniería separada de producción | bloqueo seguro y evidencia conservada | revisión, trazabilidad, fallo/crítico y cobertura B6.1/B6.2/B6.7 | **Agrupar por plataforma/licencias**; no una fila por cada regla de control |
| `SEC-SUPPLY-01 / SEC-ART-01` | registro, SBOM, firma, procedencia y dependencias | registro de artefactos + generación/verificación | producción solo consume artefactos aprobados | copia/HA según C3; claves bajo B4 | build único, SBOM y firma/procedencia B6.3/B6.4/B6.7 | **Fila propia o incluida** en CI/CD; declarar inclusión explícita |
| `SEC-NPDATA-01` | datos sintéticos y anonimización/seudonimización verificable | generador o proceso/servicio controlado | DEV/QA/PREPROD segregados | material reversible fuera del ambiente | origen, no revelación, retención y eliminación B6.5/B6.7 | **Condicional:** fila solo si se oferta herramienta/servicio separado |
| `SEC-GOV-01 / SEC-CLOUD-01 / SEC-HARD-01 / SEC-SAMM-01` | gobierno, responsabilidad nube, hardening y madurez de desarrollo seguro | matrices/procedimientos y, si aplica, servicio/herramienta de configuración/evaluación | transversal por servicio y producto/versionado | evidencia exportable y revisión ante cambios | mapeo ISO/NIST, responsabilidad, baseline/excepciones y SAMM B6.7/B7.3 | **Normalmente incluido** en implementación/servicios; fila solo si se oferta capacidad separada |

### Matriz de controles obligatoria

**Lectura vigente:** esta matriz conserva el corte detallado de B7. Las columnas «Nodo físico» y «Amenaza» que aún dicen `POR VALIDAR` o “D2 pendiente” fueron superadas por el cruce B7-R.2/B7-R.3: 31/31 controles tienen amenaza asociada y los 17 grupos físicos tienen nodo, servicio o proceso identificado. Se mantiene el texto histórico para no simular que producto, responsable o prueba quedaron resueltos.

| Control | Fuente | Actor/dato | Capa | Comp. lógico | Nodo físico | Amenaza | Implementación | Evidencia | Responsable operativo | Estado |
|---|---|---|---|---|---|---|---|---|---|---|
| SEC-IAM-01 (parcial) | Maestro §11.2; RNF-SEG-01/09/10; RF-ACC-01..05; RF-POR-02; **FEP02 Cap. 12 `RT-12.01` federación y directorio, `RT-12.03` MFA, `RT-12.05` RBAC/ABAC y segregación, `RT-12.10` baja ≤24 h desde la desvinculación, `RT-12.11` credencial temporal de eventuales** *(se retira `RT-11.27`: trata exclusivamente del acceso de personas desarrolladoras a producción y no cubre la identidad de externos ni de eventuales, que es el alcance de este control; se conserva donde sí corresponde, en `SEC-PROD-01` y `SEC-ADM-01`. Hallazgo `X-2` de la auditoría cruzada de Frente 1, verificado contra el texto del BTT)* | ACT-*; datos personales/comerciales/operacionales | transversal: canales, gateway y servicios | SRV-IAM, GW-API y contextos B1.3 | POR DEFINIR con C1/C3 | Acceso ajeno, suplantación y exceso de privilegio; formalizar en D2 | Propuesta B1.2–B2.7; producto y configuración pendientes | Matrices B1.3/B1.4, política B2.3 y escenarios B1.5/B2.6; sin pruebas ejecutadas | Funciones de administración de identidad y aprobación de negocio; asignación POR VALIDAR | EN CURSO |
| SEC-NET-01 | RNF-SEG-06; Caso 06 RT-03.24; FEP02 RT-11.01 | operación/administración/protección | red y servicios | Z-* sobre componentes B3.1 | POR VALIDAR C1/C3 | Movimiento lateral; D2 pendiente | B3.1/2/3 | Rutas permitidas/denegadas B3.6 | Red/protección; asignación pendiente | EN CURSO |
| SEC-EDGE-01 / SEC-EDGE-02 | FEP02 Cap. 11 RT-11.07/08/12; RNF-SEG-04 | público y expedientes | borde | GW-EDGE | POR VALIDAR C1/C2 | Bypass, abuso e interceptación; D2 pendiente | B3.3/4 | Bypass/TLS/renovación/accesibilidad B3.6 | Plataforma/seguridad; por asignar | EN CURSO |
| SEC-API-01 | FEP02 Cap. 11 RT-11.11; RF-POR-02/09; RNF-SEG-09 | personas/contrapartes/datos | gateway y negocio | GW-API/contextos | POR VALIDAR C1 | Acceso ajeno/payload inválido; D2 pendiente | B3.2/3/4 | Denegación por identidad/recurso y prueba de carga | API/negocio; por asignar | EN CURSO |
| SEC-ADM-01 | FEP02 Cap. 11 RT-11.27; Cap. 12 RT-12.03/06 | TI/soporte | administración | SRV-IAM/plataformas | POR VALIDAR C1/C3 | Privilegios indebidos; D2 pendiente | B2.5/B3.3 | Bloqueo externo y PAM B3.6 | TI/seguridad; por asignar | EN CURSO |
| SEC-SYNC-01 | RNF-DIS-02/04; RNF-SEG-04 | hechos/políticas/servicios | integración | EDGE-RUN/INT-HUB | POR VALIDAR C1/C3 | Repetición/alteración; D2 pendiente | B3.2/3 | Corte y reconciliación B3.6 | Integración/operación; por asignar | EN CURSO |
| SEC-EXP-01 | FEP02 Cap. 11 RT-11.13 | superficie externa | transversal | B3.5 | POR VALIDAR C1/C3 | Exposición omitida; D2 pendiente | Inventario B3.5 | Comparación con escaneo externo futuro | Plataforma/seguridad; por asignar | EN CURSO |
| SEC-DATA-01 | FEP02 Cap. 11 RT-11.03/10; RNF-SEG-05/09 | categorías públicas, internas, confidenciales y restringidas | datos y servicios | DATA-CORE, DATA-TS, DATA-DOC, DATA-AN y servicios propietarios | POR VALIDAR C1/Subdoc. 5 | Divulgación o acceso transversal; D2 pendiente | B4.1–B4.3 | Catálogo final dato→nivel→control y pruebas de acceso/consulta directa | Propietario de dato + seguridad; asignación por validar | EN CURSO |
| SEC-ENC-01 | FEP02 Cap. 11 RT-11.08/09; RNF-SEG-04/05 | datos y comunicaciones | todas | servicios, almacenes, archivos, respaldos y canales | Híbrido; ubicación final C1–C3 | Lectura de medios/BD/tráfico; D2 pendiente | B3.4 y B4.2–B4.4 | Escaneo TLS, configuración de cifrado y consulta directa sin campos restringidos | Plataforma/datos/seguridad; por asignar | EN CURSO |
| SEC-FIELD-01 | Caso 06 Cap. 15 RT-11.10; RNF-SEG-05 | personales, tarifas/volúmenes y contenido de valor/ruta | servicios y persistencia | servicios propietarios + DATA-CORE/DOC y demás almacenes que contengan campos `RES` | POR VALIDAR C1/Subdoc. 5 | Lectura directa o copia paralela en claro; D2 pendiente | B4.1–B4.3 | Catálogo completo y consulta directa sin revelación; accesos de descifrado auditados | Propietario de dato + seguridad; por asignar | EN CURSO |
| SEC-KEY-01 | FEP02 Cap. 11 RT-11.09; RNF-SEG-04; ADR-009 | claves, certificados y material de firma | seguridad transversal | KMS/HSM/vault tipo; consumidores B4.4 | Nube + ámbito local protegido POR VALIDAR C1–C4 | Extracción, pérdida o uso indebido; D2 pendiente | B4.4–B4.8 | Denegación de exportación, rotación, corte 72 h y recuperación bajo custodia | Custodia separada de consumo/aprobación; personas por asignar | EN CURSO |
| SEC-SECRET-01 | FEP02 Cap. 11 §11.4; Maestro §11.3; RNF-MAN-03 | credenciales técnicas, tokens y secretos de integración | aplicación, integración y operación | vault tipo + identidades de servicio B1/B2 | Por ambiente; local para operación crítica | Secreto embebido, reutilizado o filtrado; D2 pendiente | B4.4–B4.6; B6 completa pipeline | Escaneo, inyección en ejecución, rotación y rechazo de secreto vencido | Plataforma/seguridad; por asignar | EN CURSO |
| SEC-BKP-01 (parcial) | FEP02 Cap. 7 RT-07.09..12; RNF-DIS-14 | respaldos y claves de recuperación | continuidad/datos | repositorios protegidos + KMS/HSM/vault tipo | fuera de sitio e inmutable/fuera de línea; C2/C3 definen | Borrado simultáneo o respaldo indescifrable; D2 pendiente | B4.5–B4.7 | Restauración mensual y resistencia al borrado, incluida disponibilidad de claves | Respaldo y custodia separados; asignación por validar | EN CURSO |
| SEC-LOG-01 | FEP02 Cap. 11 RT-11.14; Maestro §§11.3/16 | eventos de seguridad y auditoría | transversal | colectores locales, canal de envío y repositorio inalterable | fuentes nube/on-premise/terreno; nodos C1–C4 | Borrado, alteración o punto ciego; D2 pendiente | B5.1–B5.3, incluida política B5.2.1 | integridad, consulta 12 meses, recuperación de 24 meses archivados, corte/reenvío y medición por clase para dimensionar | Plataforma/seguridad; servicio y personas por asignar | EN CURSO |
| SEC-SIEM-01 | FEP02 Cap. 11 RT-11.15; ADR-010 | eventos correlacionados | detección | SIEM y catálogo de reglas portuarias | central + ejecución local mínima durante corte | Ataque no correlacionado o exceso de falsos positivos; D2 pendiente | B5.2–B5.4, con admisión B5.2.1 | inyección de casos B5.3, registro evento→alerta→caso y prueba de agregación sin perder auditoría obligatoria | SOC/seguridad + propietarios operativos; por asignar | EN CURSO |
| SEC-END-01 | FEP02 Cap. 11 RT-11.16 | cargas nube/on-premise y puestos compatibles | endpoint/carga | EDR y compensaciones para activos sin agente | híbrido; cobertura real C1–C3 | Malware, manipulación o agente ausente; D2 pendiente | B5.2/B5.3 | inventario de cobertura, detección, aislamiento autorizado y reenvío | Operación endpoint/SOC; por asignar | EN CURSO |
| SEC-SOC-01 | FEP02 Cap. 11 RT-11.17; Caso 06 restricción 11; RNF-OPE-08 | operación de seguridad | operación transversal | SOC 24x7 propio o subcontratado | ubicación/dotación/proveedor POR VALIDAR C3/C4 | Alerta sin atención o dependencia de TI=5; D2 pendiente | B5.4/B5.8 | turnos, contactos, procedimientos, SLA y ejercicio de escalamiento | Adjudicatario/SOC con CLIENTE como dueño y receptor; RACI pendiente | EN CURSO |
| SEC-IR-01 | FEP02 Cap. 11 RT-11.18/19; RNF-SEG-07/11; RNF-OPE-05 | incidentes y brechas | operación y gobierno | gestión de casos/evidencia y plan de respuesta | híbrido; canal alternativo durante corte | Contención tardía, pérdida de evidencia o aviso vencido; D2 pendiente | B5.5 | simulación con marcas de detección, comunicación, contención y RCA | SOC + responsable de incidente + CLIENTE; nombres por asignar | EN CURSO |
| SEC-VULN-01 | FEP02 Cap. 11 RT-11.04; RNF-SEG-03 | activos y software | gestión de vulnerabilidades | escáneres, inventario y flujo de remediación | nube/on-premise/externo; cobertura C1–C3 | Vulnerabilidad fuera de plazo o activo omitido; D2 pendiente | B5.6 | tablero de antigüedad y cierres ≤7/15/30 días | Seguridad + propietario técnico; por asignar | EN CURSO |
| SEC-PENTEST-01 | FEP02 Cap. 11 RT-11.20; RNF-SEG-08 | solución e interfaces | validación independiente | servicio de pentest independiente | alcance final A1/A2/C1–C3 | Debilidad no detectada antes de producción; D2 pendiente | B5.6 | independencia, informe íntegro, plan, corrección y reprueba | Adjudicatario coordina; tercero independiente ejecuta; CLIENTE recibe | EN CURSO |
| SEC-SDLC-01 | FEP02 Cap. 4 RT-04.03/04; RNF-MAN-01/02/11 | código, requerimientos, incidencias, pruebas y cambios | desarrollo/mantención | repositorio y gestor de trabajo | servicio de ingeniería | Cambio no revisado o sin trazabilidad; D2 pendiente | B6.1/B6.7 | protección de rama y cadena requisito→cambio→prueba→despliegue | Desarrollo/QA/seguridad; separación por validar | EN CURSO |
| SEC-PIPE-01 | FEP02 Cap. 11 RT-11.22; Cap. 4 RT-04.05; RNF-MAN-03/06 | código, dependencias, secretos e imágenes | CI/CD | orquestador + SAST/SCA/DAST/secretos/imágenes/pruebas | fuera de producción; plataforma C3 | Vulnerabilidad o secreto promovido; D2 pendiente | B6.2/B6.7 | fallo de control bloquea; hallazgo crítico bloquea; cobertura negocio ≥70 % | Desarrollo/QA/seguridad; por asignar | EN CURSO |
| SEC-SUPPLY-01 / SEC-ART-01 | FEP02 Cap. 11 RT-11.23/24/26; STD-06 | dependencias y artefactos liberados | cadena de suministro | registro de artefactos, SBOM, firma/procedencia y catálogo de dependencias | servicio controlado; ubicación C3 | Sustitución, componente vulnerable o licencia incompatible; D2 pendiente | B6.3/B6.4/B6.7 | SBOM por versión, firma/procedencia SLSA 3+ y aprobación registrada | Ingeniería/seguridad/legal; por asignar | EN CURSO |
| SEC-NPDATA-01 | FEP02 Cap. 11 RT-11.25; B4; Subdoc. 5 | datos usados en DEV/QA/PREPROD | datos/no producción | generador sintético o proceso verificable de anonimización/seudonimización | ambientes separados | Copia productiva expone personas/comercio/carga; D2 pendiente | B6.5/B6.7 | inventario/origen, prueba de irreversibilidad o custodia de reidentificación y escaneo de fuga | Datos/privacidad/QA; por asignar | EN CURSO |
| SEC-PROD-01 | FEP02 Cap. 11 RT-11.27; Cap. 12 RT-12.06; RNF-MAN-04/05 | desarrolladores, operadores y despliegues | producción/administración | pipeline, registro de artefactos y PAM | nube/local/DR | Cambio manual o acceso directo no registrado; D2 pendiente | B2.5/B6.3/B6.6/B6.7 | despliegue reproducible, firma válida y excepción temporal aprobada/grabada | Operación separada de desarrollo; por asignar | EN CURSO |
| SEC-SAMM-01 | FEP02 Cap. 11 RT-11.28; FEP01 Art. 4.3; STD-04 | proceso de desarrollo seguro | gobierno | evaluación OWASP SAMM y plan de mejora | transversal | Control puntual sin mejora sistemática | B6.7 | línea base, plan y reevaluación anual | Responsable de desarrollo/seguridad; por asignar | EN CURSO |
| SEC-GOV-01 | FEP02 Cap. 11 RT-11.05; ISO/IEC 27001/27002; NIST CSF 2.0 | controles, riesgos y evidencias | gobierno transversal | matriz de aplicabilidad control→implementación→evidencia | n/a; referencias a nodos por control | Control mencionado sin implementación/evidencia verificable | B7.3/B7.4 | matriz versionada, propietario, excepción y prueba por control | Seguridad/gobierno; responsable nominal por asignar | EN CURSO |
| SEC-CLOUD-01 | FEP02 Cap. 11 RT-11.06; ISO/IEC 27017/27018 | servicios nube y datos personales | nube/gobierno | matriz de responsabilidad y tratamiento por servicio | proveedor/región/servicio POR VALIDAR C1/C2 | Responsabilidad omitida, subencargado o borrado no controlado | B7.3 | servicio→dato→responsable→configuración→evidencia→salida | Seguridad/privacidad/plataforma; por asignar | EN CURSO |
| SEC-HARD-01 | FEP02 §11.5; CIS Benchmarks; STD-05 | nube, servidores, edge y endpoints | plataforma/endpoint | baseline por producto/versión y registro de excepción | nodos POR VALIDAR C1–C3 | Configuración insegura o desviación no gobernada | B7.3 | escaneo/configuración, excepción con riesgo/aprobador/vencimiento y reprueba | Plataforma/seguridad; por asignar | EN CURSO |

### Productos obligatorios

1. Vista lógica de seguridad y fronteras de confianza.
2. `SEC-PHYS-v0.1` entregado en Puerta 1.
3. Matriz de controles completa.
4. Matriz de identidad/roles/sesiones.
5. Candidatos de T-11 y `ADR-008/009/010`.

### Decisiones permitidas y escalamiento

Puede definir patrones y controles mínimos. Debe escalar identidad federada no confirmada, restricciones de autoridad/VMS, productos sin compatibilidad demostrada y controles que impidan operar 72 h.

### Salidas hacia otros frentes

- Frente 1: políticas de exposición, identidad y datos por interfaz.
- Frente 2: zonas, controles físicos, productos/licencias y requisitos de continuidad.

### Definición de terminado

- [ ] Seguridad aparece en todas las capas, no solo perímetro.
- [ ] Actores internos, externos, eventuales y privilegiados están resueltos.
- [ ] Cada dato sensible tiene protección en tránsito/reposo y manejo de llaves.
- [ ] Logging/detección cubren nube, on-premise y borde sin puntos ciegos.
- [ ] Controles tienen evidencia y componente físico cuando corresponde.
- [ ] No se rompe operación desconectada.
- [ ] `TRZ_D1.md` completo.
- [ ] Dependencias F3-DEP-001..004 resueltas para cierre y externos tratados explícitamente.
- [ ] Diagramas finales coherentes con el contenido y matrices validados.

## Plan de desarrollo acordado

**Estado vigente tras MA-8:** desarrollo técnico `EN CURSO`; B1–B7, B7-R/B7-C y MA-3..8 están completados como diseño/preparación documental. El corte deja 11 ADR `PROPUESTO`, 0 `APROBADO`, 32 filas T-11 y la estructura 4.1/4.2 trazada a fuentes y controles D3. AWS `sa-east-1`/`us-east-1` está incorporado. F5 representará seguridad y límites de confianza. P4 está aprobada; faltan redacción/figuras y luego la ejecución D3.

### Uso de los archivos

- **Este D1:** contrato, plan, contenido técnico en borrador, matrices de controles e identidad, paquete temprano y propuestas ADR-008/009/010 conforme a la plantilla global. Solo lo aprobado pasa a «Contenido listo para integrar».
- **TRZ_D1:** fuentes, cobertura de RT y enlaces a controles/secciones/evidencias; no duplicar la narrativa técnica. La evidencia prevista no es una prueba ejecutada.
- **DECISIONES_Y_ESCALAMIENTOS:** decisiones abiertas, dependencias y condiciones para resolverlas. Sus IDs se citan desde el borrador.
- **AUDITORIA_CIERRE:** comprobar el resultado; no marcar cumplimiento por tener una fila o una intención de diseño.
- **Índice del frente:** orden y estado. Maestro, matriz global y ADR global se actualizan coordinadamente en integración; no crear otra base de actores o componentes.

### Actores y roles: una única referencia común

La entrada inicial es el Maestro §5.1 (`ACT-*`), §5.2 (sistemas `EXT-*`) y §6.1 (componentes). A1 confirma/refina el catálogo lógico oficial. D1 usa esos IDs sin renombrarlos y desarrolla su perspectiva de seguridad: permisos, alcance de datos, sesiones y separación de funciones.

Un actor no es necesariamente un único rol: por ejemplo, `ACT-REEFER` agrupa operadores y supervisores, cuyos permisos pueden diferir. Tampoco `ACT-AGE` implica acceso a los datos de todas las empresas. Las especializaciones de roles se propondrán vinculadas al actor original y con fuente/justificación; no se presentarán como nuevos actores oficiales. Para cuentas de servicios se indicará el componente propietario, sin confundirlas con personas. Toda carencia o cambio de actor se registra para validación de A1 (`F3-DEP-001`).

La matriz de identidad se desarrollará con: actor del Maestro, rol propuesto, acción/recurso, alcance de datos, condición de turno/zona/organización, autenticación, sesión, comportamiento sin enlace, fuente y validación pendiente. Son campos previstos, no permisos ya aprobados.

### Secuencia de trabajo

| Paso | Qué desarrollaremos | Resultado y límite |
|---|---|---|
| 1. Delimitar entradas | Seleccionar actores, activos, sistemas conservados y cinco funciones críticas locales desde el Maestro; vincular requerimientos aplicables de C2 y traza cap. 11 | Alcance y escenarios de D1; conservar las fuentes y pendientes del CLIENTE |
| 2. Identidad y escenarios | Operador/eventual en terminal compartido; usuario externo que presenta documentación; administrador/desarrollador; integración de sistema; pérdida de enlace de 72 h | Matriz de roles/sesiones y flujos textuales; permisos propuestos a contrastar con A1/A2 |
| 3. Zonas y exposición | Fronteras de confianza y comunicaciones permitidas; controles de borde/gateway; plantilla de dominios, puertos y servicios expuestos | Matriz origen–destino–finalidad–dato–identidad–control; topología y puertos reales pendientes de A2/C1/C3 |
| 4. Datos, claves y continuidad | Sensibilidad, cifrado de campo/reposo/tránsito, custodia/rotación, respaldo protegido y evidencia; resolver propuesta de autenticación, expiración, revocación y auditoría local durante 72 h | Diseño propuesto de estados normal/desconectado/reconexión/emergencia; no asumir revocación remota instantánea sin enlace ni disponibilidad de claves solo en nube |
| 5. Detección y operación segura | Logs, SIEM/EDR, SOC, casos portuarios, incidentes y vulnerabilidades; desarrollo seguro, dependencias y acceso excepcional a producción | Controles y responsables por función propuestos; dotación, cobertura concreta, capacidades y productos por validar; distinguir atención operativa de comunicación de incidentes |
| 6. Paquete independiente | Completar matriz de controles, traza y SEC-PHYS-v0.1; proponer ADR-008/009/010 con alternativas y consecuencias | Entrega textual utilizable: capacidad, ubicación requerida/provisional, continuidad, evidencia prevista y candidato T-11; sin cantidades ni compatibilidades inventadas |
| 7. Integración y refinamiento | Contrastar actores/componentes de A1, contratos de A2, escenarios TOS/locales de A3 y nodos/red/continuidad/capacidad de C1–C4; incorporar revisión D2 | Resolver dependencias registradas y documentar cambios; no esperar el cierre completo ajeno para intercambiar v0.1 |
| 8. Diagramas y cierre | Representar el contenido ya definido; revisar consistencia entre vista, matrices, trazas y aportes T-11 | D1 solo pasa a revisión/aprobación con diagramas y cruces completos; pruebas futuras quedan como criterios verificables, no como resultados obtenidos |

### Plan de bloques y punto de continuación

**Última actualización: 2026-09-05.** Este es el registro operativo para retomar D1 en otra sesión. Complementa la secuencia de trabajo anterior: sus pasos se agrupan en los bloques siguientes, sin cambiar el contrato del entregable. Actualizar esta tabla y el punto de continuación al terminar cada bloque.

| Bloque | Contenido y resultado esperado | Avance actual / condición de cierre |
|---|---|---|
| B1 — Alcance, actores y permisos | Qué protegemos; 16 actores del Maestro; roles y alcance de acceso; separación de funciones y escenarios | **Borrador redactado**, no aprobado. A1 valida actores/componentes y correspondencia de permisos; B2 refina sesiones |
| B2 — Sesiones y continuidad de identidad | Autenticación, relevo, permisos offline, bajas, reconexión, emergencia y propuesta ADR-008; entrada IAM para Física | **Propuesta redactada**, no aprobada. Producto, parámetros, usabilidad, nombradas y revocación aislada por validar |
| B3 — Zonas, conductos y exposición | Fronteras nube/local/terreno/administración/protección/terceros; matriz origen–destino–finalidad–dato–identidad–control; CDN/WAF/DDoS/gateway/TLS/HSTS/certificados/bots e inventario de exposición | **Propuesta redactada**, no aprobada: B3.1–B3.6. Zonas/flujos/controles y plantilla de exposición; redes y contratos reales por validar |
| B4 — Datos, claves y secretos | Clasificación inicial y protección por sensibilidad; cifrado de tránsito/reposo/campo, custodia, rotación, recuperación y continuidad local; propuesta ADR-009 | **Propuesta redactada**, no aprobada: B4.1–B4.8. Subdoc. 5 valida catálogo/campos; C1–C4 ubicación, producto, HA/capacidad y T-11; periodicidades y custodios por acordar |
| B5 — Detección y respuesta | Auditoría inalterable y retenciones; SIEM, EDR, SOC 24x7, casos portuarios, incidentes, vulnerabilidades y pentest; propuesta ADR-010 | **Propuesta redactada**, no aprobada: B5.1–B5.8. Plazos obligatorios incorporados; modelo SOC/detección, productos, cobertura, dotación, capacidad y responsables por validar |
| B6 — Desarrollo y operación seguros | SAST/SCA/DAST/imágenes, SBOM, firma/SLSA, aprobación de dependencias, datos no productivos y marco SAMM; completar controles de acceso a producción con B2 | **Propuesta redactada**, no aprobada: B6.1–B6.9. Puertas automáticas, artefacto único, cadena de suministro, separación de ambientes/producción y glosario; herramientas, responsables y pruebas por validar con C3 |
| B7 — Cobertura y paquete temprano | Completar matriz control–componente–evidencia, traza de capítulos 11/12 y demás fuentes aplicables; consolidar SEC-PHYS-v0.1, candidatos T-11 y propuestas ADR | **Auditoría histórica ejecutada:** paquete v0.1 consolidado. Sus pendientes de entradas fueron revaluados en B7-R con los catálogos reales |
| B7-R — Integración documental D1–D2 | Cruzar actores, contratos, nodos, amenazas, controles y SEC-PHYS/T-11; clasificar dependencias | **COMPLETADO COMO DISEÑO, no aprobado:** 31/31 controles enlazados a amenazas; 17/17 grupos emplazados/tratados por C1–C4; dependencias internas cruzadas con observaciones |
| B7-C — Revisión conjunta (bloque 5) | Auditar D1, D2, trazas, ADR, matriz global y registro de pendientes como un solo paquete | **CORTE HISTÓRICO COMPLETADO:** dejó el paquete listo para la auditoría independiente ya ejecutada; MA-3 y MA-4 contienen los cortes posteriores |
| B8 — Integración visual y cierre | Producir diagramas coherentes y preparar narrativa final después de la revisión conjunta | **DIFERIDO.** No iniciar antes del cierre documental conjunto/auditoría; no aprobar con brechas externas o de prueba |

**Retomar exactamente aquí:** MA-8 está completada como preparación y P4 aprobada. Redactar el consolidado y producir F1–F5; F6 solo si continuidad no resulta legible. Cruzar `V-DATA-01` con Subdocumento 5 y ejecutar D3 sobre la versión ensamblada. No reabrir B1–B7 ni los ADR salvo evidencia nueva o disparador. `ADR-001..011` están `PROPUESTO`; ninguno está aprobado.

**Lectura mínima para continuar:** este D1 (contrato, plan y B1–B7); Maestro vigente (completo si el agente no conoce el proyecto); índice del Frente 3; reglas comunes y Frente 3 del Plan de entregables; TRZ_D1, DECISIONES_Y_ESCALAMIENTOS y auditoría intermedia. Consultar A1/A2/A3 y C1–C4 para identificar aportes nuevos; Célula 2 es la fuente de detalle cuando una decisión lo requiera. La línea base utilizada es Maestro v1.1 / Célula 2 `c4756df`: comprobar si cambió antes de asumirla vigente. Preferir Markdown; usar PDF si falta información o aparece inconsistencia.

**Acuerdos de trabajo y límites que deben conservarse:**

- Avanzar en bloques pequeños y explicar decisiones en simple. Consultar brevemente solo alternativas que cambien operación, alcance o complejidad; desarrollar autónomamente lo fijado por fuentes.
- Diagramas al final, después del contenido. No crear documentos auxiliares duplicados; D1 contiene el diseño, TRZ_D1 la trazabilidad, el registro los pendientes y el índice el estado.
- B1/B2 son propuestas, no aprobación del usuario de cada parámetro. Credencial/PIN, límites de sesión/concurrencia y patrón IAM requieren validación; no son valores impuestos por las Bases. ADR-008 está en análisis.
- B4 selecciona como propuesta ADR-009 la alternativa C: gobierno común de claves con capacidades separadas por ámbito y servicio local protegido. Queda `PROPUESTO`, no `APROBADO`; no selecciona producto, HSM dedicado, período fijo de rotación ni custodios concretos. Se conservan A/B resumidas porque justifican la decisión y la plantilla global exige alternativas reales.
- B5 selecciona como propuesta ADR-010 la alternativa C: detección híbrida federada, repositorio central inalterable, capacidad local mínima y SOC 24x7 gestionado/subcontratado. Queda `PROPUESTO`, no `APROBADO`; no se ha escogido SIEM/EDR, ubicación, dotación ni proveedor.
- B6 hace obligatorias las puertas automáticas de seguridad, el artefacto único firmado/promovido y la separación de producción. No selecciona plataforma CI/CD ni herramienta de análisis; C3 materializa el flujo y D1 conserva la política/evidencia exigida.
- B7 verificó la cobertura, corrigió estados de traza y explicitó SEC-GOV/CLOUD/HARD. `SEC-PHYS-v0.1` está listo para intercambio interno, no publicado. Un control no genera automáticamente una fila T-11: C4 separa solo productos/licencias/servicios ofertados y declara inclusiones para evitar doble conteo (`F3-DEC-005`).
- Mantener F3-DEP-001..004 y F3-ESC-001/002. En particular: actores/roles con A1; nuevas nombradas y acreditaciones durante aislamiento; revocación inmediata frente a terminal aislada; compatibilidad de IAM/directorio y servicios conservados.
- Las 72 h son autonomía local ante pérdida de enlace exterior, las 8 h son aislamiento de terminal de patio y los ≤90 min son sincronización posterior. Energía, falla de red interna, servidor y desastre requieren medidas propias de Física; no son equivalentes a esos plazos.
- El portal nube puede seguir disponible, pero recibir una solicitud no equivale a confirmar una operación dependiente del terminal. El tratamiento de citas/autoridad en B2.1 es propuesta por validar con A2/A3/C3.
- No declarar cumplimiento por mencionar una norma ni confundir diseño con certificación institucional. Pruebas previstas no son ejecutadas. `SEC-PHYS-v0.1` ya fue incorporado documentalmente por C1–C4 y D2 está auditado para v0.5 con pendiente ADR; D3 no se ha iniciado.
- Los avances actuales están guardados localmente, sin commit/push de estos bloques. Este pedido de continuidad no autoriza publicar cambios. Conservar archivos locales ajenos y la guía de arranque excluida del repositorio.

### Dependencias que impiden el cierre, pero no el avance independiente

| ID | Entrada requerida | Qué podemos adelantar | Qué no puede darse por cerrado |
|---|---|---|---|
| `F3-DEP-001` | A1: actores y catálogo lógico v0.1 | Roles/permisos propuestos sobre ACT-* y componentes del Maestro | Correspondencia definitiva de actores, roles, funciones y componentes |
| `F3-DEP-002` | A2/A3: interfaces, contratos y comportamiento local/TOS | Políticas por tipo de flujo y escenarios de falla/sincronización | Controles por interfaz real, autoridad TOS y viabilidad del flujo completo durante 72 h |
| `F3-DEP-003` | C1/C2/C3/C4: nodos, productos, zonas/red, HA/DR y dimensionamiento | Requisitos de ubicación, continuidad y capacidades de seguridad | Mapeo físico, compatibilidad, capacidad de registros/claves, cantidades/licencias y correspondencia T-11 |
| `F3-DEP-004` | D2 y coordinación con Subdoc. 5 | Controles por escenarios y categorías sensibles del Maestro | Cobertura final de amenazas/riesgo residual y correspondencia del cifrado con campos concretos |
| `F3-ESC-001` | CLIENTE: directorio/federación real; además Maestro ESC-06/12 según materia | Contratos desacoplados, alternativas y condiciones de validación | Compatibilidad con terceros y acreditaciones reales; mantener supuesto/fallback explícito |

**Regla de cierre:** no declarar D1 `APROBADO` ni v1.0 mientras las dependencias internas anteriores dejen controles sin correspondencia o viabilidad. La espera parcial no bloquea todo D1: al iniciar el desarrollo se usa `EN CURSO` y se identifica cada dato `POR VALIDAR`. `BLOQUEADO EXTERNO` se reserva para datos/autoridad externos concretos. Los pendientes externos pueden quedar tratados mediante condiciones y fallback aceptados, sin convertirlos en hechos. La v0.1 se intercambia aunque falten diagramas; no equivale al entregable terminado.

## Contenido técnico en elaboración

### B1. Alcance e identidad — borrador inicial

**Estado: EN CURSO.** Propuesta de diseño del equipo sobre Maestro v1.1 y Célula 2 `c4756df`; no constituye permisos aprobados ni pruebas ejecutadas. A1 confirma actores/componentes mediante `F3-DEP-001`. Los nombres de roles siguientes son descripciones propuestas, no nuevos IDs de actores. Este bloque inicia identidad; el diseño completo de sesiones, autonomía y PAM se refina en el siguiente bloque.

#### B1.1 Qué protegemos y con qué límites

La seguridad abarca los canales `CH-PORTAL`, `CH-APP` y `CH-CAB`, los servicios de negocio, las integraciones, los datos y su operación local. Se protegen tanto las acciones como la consulta de información personal, comercial y de contenido/ruta de carga. La clasificación detallada de campos corresponde al cruce con Subdocumento 5 (`F3-DEP-004`); aquí se determina quién puede necesitar cada categoría.

Las cinco funciones locales del Maestro §9.1 —nave/movimientos, posición/inventario, gate, alarmas reefer y hechos/evidencia facturable— deben conservar identidad y autorización durante 72 h sin enlace. El conteo de personas desconectado también debe mantenerse conforme a `RF-ACC-08`; no queda excluido por no ser una de esas cinco funciones. Las terminales de patio tienen además el escenario de 8 h sin cobertura. Estos son requisitos para el diseño siguiente, no una autonomía ya demostrada.

Los límites heredados se mantienen: `EXT-ERP` emite documentos tributarios; `EXT-ACC` conserva autoridad física; `EXT-VMS` mantiene la interfaz de video; `EXT-GRU` solo admite lectura autorizada por fabricante; `INT-TOS` respeta autoridad por dominio, zona y fase. Tener un rol en la plataforma no concede administración de estos sistemas. Fuentes: Maestro §§3–9, 16–19; RNF-SEG-05/09/10; RF-ACC-08.

#### B1.2 Reglas comunes de autorización propuestas

1. **Identidad individual y denegación por defecto.** Una cuenta válida no habilita todas las funciones. Cada solicitud requiere identidad vigente, permiso sobre la acción y alcance sobre el recurso. Estar dentro de la red del puerto no concede confianza automática (`RNF-SEG-01`).
2. **Rol más contexto.** RBAC limita la tarea; ABAC restringe organización representada, asignación, zona, turno y vigencia cuando corresponda. Estos atributos proceden de registros autorizados; no se aceptan porque el usuario los envíe en el formulario. El control se aplica en servicios, además del gateway, también a consultas, exportaciones y adjuntos.
3. **Identidad y habilitación son distintas.** Verificar quién es una persona no demuestra que represente a una naviera ni que tenga una acreditación de faena vigente. El autoservicio externo de `RF-POR-02` no asigna privilegios por simple registro; el mecanismo de prueba de representación queda por validar. La nombrada confirmada y las acreditaciones vigentes habilitan al eventual, sin otro trámite individual ajeno a los acuerdos (`RF-ACC-01/05`).
4. **Acceso privilegiado separado.** La cuenta habitual de TI no recibe facultades permanentes de superadministración. La elevación será temporal, aprobada y auditada mediante PAM. Desarrolladores no tienen acceso interactivo directo a producción; una excepción requiere aprobación, tiempo limitado, registro y grabación (FEP02 Cap. 11, RT-11.27).
5. **Sesiones atribuibles.** El equipo puede compartirse; la identidad de la sesión no. Un relevo finaliza la sesión anterior y abre la del siguiente trabajador sin detener procesos de fondo ni atribuirle operaciones previas. No se pide confirmación rutinaria en cabina ni interacción que distraiga del movimiento de carga.
6. **La desconexión no amplía permisos.** Continuidad local no significa credenciales generales de 72 h: las del eventual vencen al cierre de su turno. Se requiere emisión/validación local controlada para los turnos siguientes y revocación local. La baja efectiva ≤24 h y la imposibilidad de recibir revocaciones remotas sin enlace deben resolverse juntas, con procedimiento de aviso alternativo y evidencia; aún no se declara esa brecha resuelta.

Fuentes obligatorias: Maestro §11.2; FEP02 Cap. 11 RT-11.01/11.27 y Cap. 12 (identidad); Caso 06 Cap. 15 RT-12.11/13.08; RNF-SEG-01/09/10; RF-ACC-01..05 y RF-POR-02. La aplicación concreta de estas reglas a cada actor es propuesta del equipo.

#### B1.3 Matriz inicial de actores, roles y alcance

Todas las filas están **POR VALIDAR con A1** (`F3-DEP-001`). Los perfiles de B1.4 se concretan en B2.3–B2.5. Ninguna fila habilita modificación directa de bases, de evidencia histórica ni de sistemas conservados. Los permisos definitivos deben contrastarse con los RF de cada dominio, sin crear funciones nuevas.

| Actor del Maestro | Rol propuesto / acción permitida | Recurso o componente inicial | Alcance y límite | Perfil B1.4 |
|---|---|---|---|---|
| ACT-OPS | Operador registra hechos; supervisor gestiona excepciones autorizadas | CTX-OPS, CTX-YARD, SRV-EVID | Operación/zona/turno asignados; retorno normal con doble control | Operativo |
| ACT-PLAN | Planificador propone, aprueba o corrige planes según facultad asignada | CTX-PLAN, CTX-YARD, CTX-VESSEL | Planes asignados y motivos de cambios; no permisos IAM por ser planificador | Operativo |
| ACT-GATE | Operador valida entrada/salida; jefatura resuelve excepciones | CTX-GATE, SRV-EVID | Visita/carril/turno; no omitir impedimentos de autoridad o protección | Operativo |
| ACT-REEFER | Operador atiende/confirma alarmas; supervisor propone cambios de parámetros autorizados | CTX-REEFER, SRV-NOTIF | Tomas/zonas asignadas; cambios sujetos a RN-11 y techo de alarma, sin tolerancias inventadas | Operativo |
| ACT-MANT | Técnico registra intervención; jefatura coordina mantenimiento/energía | CTX-EMIS, CTX-REEFER, SRV-EVID | Equipos asignados; no obtiene control de grúa ni modifica protecciones por este rol | Operativo |
| ACT-TI | Operación TI habitual; administrador con elevación separada | SRV-IAM y plataformas asignadas | Administración técnica no implica lectura comercial indiscriminada ni aprobación propia | Privilegiado |
| ACT-EVT | Trabajador habilitado para tarea de la nombrada | CH-APP/CH-CAB, servicios de tarea asignada | Persona, faena, zona y turno; el vínculo eventual no concede todos los roles operativos | Temporal |
| ACT-GRU | Operador consulta indicaciones y recibe alertas | CH-CAB, CTX-YARD/CTX-VESSEL | Equipo/faena asignados; sin confirmación rutinaria ni escritura al control de grúa | Operativo |
| ACT-COM | Gestor consulta hechos/evidencia y tramita objeciones | CTX-BILL, SRV-EVID | Cartera/expediente asignados; ERP sigue como emisor tributario | Interno |
| ACT-NAV | Representante consulta/intercambia información de su naviera | CTX-VESSEL, CH-PORTAL | Naviera y operación representadas; COPRAR no se confunde con RF-POR-09 | Externo |
| ACT-AGE | Representante presenta documentación/instrucción y consulta trámites propios | CH-PORTAL, SRV-EVID, servicios vinculados por A1/A2 | Empresa y representación verificadas por expediente; RF-POR-09 en Etapa 2 | Externo |
| ACT-TRA | Transportista gestiona citas/cola y consulta validación | CTX-GATE, CH-APP/CH-PORTAL | Empresa, conductor y visita vinculados; sin visibilidad de carga ajena | Externo |
| ACT-AUT | Inspector consulta expediente asignado y registra actuaciones autorizadas | CTX-INSP, SRV-EVID | Competencia y expediente de su autoridad; sin presumir API o cuenta existente | Externo |
| ACT-FER | Coordinador intercambia programación y recepción/entrega | INT-HUB y contexto a confirmar por A1 | Operaciones ferroviarias vinculadas; contrato por levantar | Externo |
| ACT-CON | Receptor consulta/exporta indicadores del concedente | DATA-AN mediante servicio autorizado | Indicadores pactados y evidencia pertinente; sin escritura operacional | Externo |
| ACT-VER | Verificador consulta reporte e historia de emisiones para verificación | CTX-EMIS, SRV-EVID | Período/alcance acordados; sin alterar medición de origen | Externo |

Fuente del universo de actores/componentes: Maestro §§5.1/6.1. Fuentes de límites: §§4.4–4.6, 8, 11, 14, 17; Célula 2 RF-POR-02/09, RF-INT-02, RF-ACC-01..05 y RNF-SEG-09/10. Las cuentas de sistemas de navieras u otras contrapartes se tratan como servicios en B1.4, no como sesiones humanas.

#### B1.4 Autenticación, sesiones e identidades técnicas

| Perfil | Regla inicial de autenticación y sesión | Comportamiento sin enlace / pendiente |
|---|---|---|
| Operativo | Identidad individual, permisos de tarea y relevo atribuible. Método no biométrico compatible con guantes/intemperie; MFA si el acceso se origina fuera de red corporativa o es privilegiado | Acceso local a funciones críticas según asignación vigente; mecanismo, expiración de sesión y renovación pendientes del bloque 2 |
| Temporal | Credencial individual emitida por nombrada confirmada y acreditaciones vigentes; vence al cierre de turno; sin biometría obligatoria ni cuenta colectiva | Validación, emisión y revocación locales por resolver; no renovar automáticamente una nombrada vencida |
| Interno | SSO individual, rol y ámbito de información; MFA para acceso externo o privilegiado; cierre SSO propagado | No se promete toda la función comercial offline; conservar captura local de hechos/evidencia |
| Externo | Registro, verificación y recuperación autoservidos para RF-POR-02; MFA en todo acceso fuera de red corporativa; organización/representación verificadas antes de autorizar recursos | No se concede acceso remoto al núcleo local por pérdida de enlace; disponibilidad del portal y su dato vigente se define en bloque 2 con A2/C3 |
| Privilegiado | Cuenta nominativa separada, MFA, PAM, aprobación y elevación temporal; sesión grabada; bloqueo de acceso directo de desarrollo a producción | Acceso de emergencia local por diseñar con A3/C3; sin cuenta universal ni excepción permanente |
| Servicio | Identidad técnica por componente/integración y ambiente, permisos solo sobre su contrato; sin inicio de sesión humano ni credenciales personales reutilizadas | Servicios críticos requieren autenticación local; mecanismo y rotación pendientes de ADR-008/009 y contratos A2 |

`SRV-IAM` es la capacidad lógica común, no una marca seleccionada. SSO/federación seguirá la alternativa OIDC/OAuth 2.1 o SAML 2.0 del Maestro; selección y compatibilidad en ADR-008 / `F3-ESC-001`. Identidades de servicio se vinculan a `INT-HUB`, `INT-TOS` o al componente propietario; no se presupone que un legado soporte protocolos modernos. Su adaptador debe contener la compatibilidad confirmada por A2.

Las funciones de desarrollo, soporte del adjudicatario y SOC necesitan identidad nominativa, organización y responsable contractual propios: **no se atribuyen a ACT-TI del CLIENTE**. Se propone a A1 representar estas funciones técnicas sin inventar aquí un actor oficial. Su matriz fina de privilegios corresponde al bloque de operación/PAM (`F3-DEP-001`).

#### B1.5 Separación de funciones y escenarios de verificación

Se propone que quien solicita acceso privilegiado no lo apruebe; que quien administra permisos no pueda suprimir su evidencia; y que las correcciones de hechos conserven original, motivo y autor. El retorno normal mantiene ejecutor y aprobador distintos según Maestro §8/MC-14; la emergencia tendrá un mecanismo excepcional trazable que se desarrolla con A3. No se exige doble aprobación para cada movimiento o alarma rutinarios. Las personas concretas y suplencias se asignarán considerando TI=5; roles separados no equivalen a contratar una persona por rol.

| Escenario de aceptación previsto | Resultado exigido o propuesto | Fuente / pendiente |
|---|---|---|
| Una agencia modifica el identificador de expediente, descarga o exportación para consultar otra empresa | Denegar en el servicio y registrar el intento; la interfaz no es el único control | RNF-SEG-01/09; propuesta B1.2; validar RF y representación con A1 |
| Eventual con turno vigente intenta otra zona; después intenta usar la credencial al cierre | Denegar ambos accesos según zona/vigencia y dejar motivo; no habilitar por pertenecer al recinto | RF-ACC-02/03/09 |
| Nombrada confirmada con 380 eventuales | Emitir credenciales en ≤30 min; rechazar acreditación vencida y conservar vía no biométrica | RF-ACC-01/04/05; prueba futura con usuarios según RNF-SEG-10 |
| Dos trabajadores relevan un terminal compartido | Separar sesiones y atribución; mantener procesos de fondo y cero detención por relevo | RNF-SEG-10; validar interacción en terreno |
| Usuario común o desarrollador solicita privilegios de producción | Denegar acceso directo; excepción solo con aprobación distinta, caducidad y sesión grabada | Maestro §11.2; FEP02 Cap. 11 RT-11.27 |
| Caída de enlace atraviesa varios turnos y se comunica una baja | Mantener funciones críticas con identidades vigentes, revocar localmente y demostrar baja ≤24 h sin convertir 72 h en vigencia universal | Maestro §§9/11.2; diseño y prueba pendientes bloque 2 / F3-DEP-002/003 |

Estos escenarios son criterios de revisión/prueba futuros. No acreditan configuración, conformidad completa con NIST, ni funcionamiento probado.

#### B1.6 Pendientes identificados al cierre de B1

B2 desarrolla estas propuestas; las validaciones externas y cruzadas siguen abiertas.

- Método concreto de credencial de terreno y relevo; plazos de sesión, reautenticación y recuperación; prueba de usabilidad sin biometría obligatoria.
- Emisión de nuevos turnos, expiración y revocación durante 72 h; aviso de bajas durante aislamiento y 8 h sin cobertura de terminal. No está resuelto por escribir «IAM híbrido».
- Matriz definitiva de segregación de funciones, representación externa e identidades de soporte/SOC; confirmación de A1 y responsables operativos.
- Puntos de aplicación de políticas, despliegue IAM/HA, autenticación de servicios, custodia y compatibilidad con sistemas conservados; cruces A2/A3/C1–C4.

Con este bloque se adelantan matriz de identidad y reglas de acceso; **SEC-PHYS-v0.1 todavía no está completo ni entregado**, y las casillas de terminado se mantienen abiertas.


### B2. Sesiones y continuidad de identidad — propuesta

**Fecha:** 2026-09-05. **Estado: EN CURSO.** Refina B1; no selecciona producto ni acredita pruebas. Fuentes: Maestro §§9/11.2; FEP02 Cap. 12 RT-12.01..13; Caso 06 Cap. 15 RT-03.10/03.13/12.11/13.08; RNF-DIS-02/03/04, RNF-SEG-10 y RF-ACC-01..05/08/09. Los valores de sesión y mecanismos concretos aquí propuestos son decisiones del equipo, no cifras de las Bases.

#### B2.1 Separar los escenarios de continuidad

| Escenario | Qué debe mantener identidad | Límite de esta propuesta |
|---|---|---|
| Sin enlace exterior del terminal, con infraestructura local disponible | Autenticación/autorización, turnos y registro locales durante ≥72 h; reconexión y conciliación ≤90 min | No significa sesión de 72 h ni autonomía eléctrica de 72 h |
| Terminal de patio sin cobertura | Uso acotado a asignación previamente autorizada y registro local ≥8 h; validar nuevamente al reconectar | No recibe una revocación mientras permanezca totalmente aislada; tratamiento B2.4 |
| Falla de energía, red interna, servidor o servicio IAM | Continuidad de las capacidades de seguridad mediante respaldo, redundancia y recuperación definidos por C1–C4 | No se resuelve guardando credenciales; HA y DR de identidad deben probarse con las funciones de negocio |
| Portal en nube activo, terminal aislado | Identidades externas pueden autenticarse en nube; permisos por organización se mantienen | La autenticación no autoriza confirmar una operación que dependa de datos/autoridad local inaccesibles |

Para transportistas se propone conservar en gate las citas sincronizadas y recibir en nube nuevas solicitudes como pendientes cuando su confirmación dependa del terminal. A2/A3 deben confirmar autoridad, cupos, cancelaciones, conflictos y qué operaciones pueden confirmarse autónomamente en nube. Agencias/navieras mantienen el mismo límite por expediente; autoridades/concedente/verificador deben ver fecha de actualización y alcance de la información disponible. No se presenta esta propuesta como comportamiento funcional ya aprobado ni se cambia la etapa de RF-POR-02/09.

#### B2.2 Patrón propuesto: gobierno común y capacidad local acotada

Se propone una política y catálogo de identidades comunes en `SRV-IAM`, con capacidad local de autenticación, autorización y gestión de turnos para las funciones críticas de `EDGE-RUN`. Los módulos consumen identidad común; no crean cuentas independientes. Federación mediante OpenID Connect/OAuth 2.1, o SAML 2.0 cuando lo requiera la integración, y conexión al directorio corporativo mediante LDAP o equivalente nube según FEP02 RT-12.01. El directorio y compatibilidad reales siguen en `F3-ESC-001`.

En operación normal se distribuyen al ámbito local solo identidades operativas necesarias, verificadores protegidos, asignaciones, acreditaciones, revocaciones y políticas versionadas. No se replican contraseñas en claro ni todo el directorio a las terminales. Las credenciales criptográficas necesarias para verificar y emitir sesiones locales no pueden depender exclusivamente de un servicio nube; custodia, HA y rotación se desarrollan en ADR-009 y C1–C4.

Ante corte exterior, un operador autorizado procesa localmente la **nombrada confirmada** y comprueba las acreditaciones vigentes de su fuente autorizada. La solución habilita acceso; no administra remuneraciones ni decide la nombrada. Una nueva asignación recibida por procedimiento de contingencia debe conservar origen, responsable, vigencia y aprobación; no habilitar sin evidencia ni prorrogar automáticamente acreditaciones. Fuente de nuevas nombradas y modo de actualización durante el corte: **POR VALIDAR con CLIENTE/A2/A3**. Sin este insumo no puede darse por demostrada la continuidad de turnos durante 72 h.

El ámbito local puede emitir y revocar permisos operativos de su terminal dentro de facultades delegadas. Cambios globales de roles, federaciones y privilegios de otras organizaciones quedan fuera de esa delegación. Identidad laboral no se elimina por borrar una sesión: se conserva el historial de alta, cambio, elevación, bloqueo y baja con autor y motivo.

#### B2.3 Política inicial de autenticación y sesiones

**Propuesta de parámetros para revisión y pruebas:** no sustituyen un máximo contractual más estricto que aparezca en la validación. El cierre por turno y acreditación prevalece siempre sobre la duración técnica de sesión.

| Perfil | Autenticación propuesta | Duración máxima / inactividad / concurrencia |
|---|---|---|
| Operativo y eventual en puesto compartido | Credencial física individual con prueba criptográfica de posesión y PIN en inicio/relevo; sin correo personal ni biometría obligatorios. Reutilizar credencial existente solo si se demuestra capacidad; un UID o QR estático no prueba posesión segura | Sesión hasta fin de asignación/turno, máximo 8 h; bloqueo de interacción a 15 min de inactividad. Una sesión interactiva operativa por persona y una persona activa por puesto; traslado explícito entre puestos |
| Cabina en operación | Misma identidad al tomar equipo en condición segura; no pedir PIN/confirmación durante movimiento. Indicaciones y alarmas de seguridad continúan como salida del servicio, sin otorgar escritura anónima | Mismo máximo por turno; bloqueo de acciones personales por inactividad sin ocultar indicaciones/alertas necesarias. Validar sensores/condición segura con A1/A3; no presumir interfaz de fabricante |
| Interno administrativo | SSO; MFA cuando sea privilegiado o desde fuera de red corporativa | Máximo 8 h, inactividad 15 min; hasta 2 sesiones habituales, visibles y revocables por la persona |
| Externo | Registro/verificación/recuperación autoservidos de RF-POR-02, MFA; representación empresarial verificada antes de permisos | Máximo 8 h, inactividad 15 min; hasta 2 sesiones, cierre remoto de sesiones y nueva verificación ante recuperación |
| Privilegiado | Cuenta separada, MFA; soporte de factor resistente al phishing, como llave FIDO2, para administradores; aprobación previa PAM y registro/grabación | Elevación máxima 30 min o plazo menor autorizado; inactividad 5 min; una sesión privilegiada por cuenta. Continuación exige nueva aprobación |

Las **8 h de sesión son una propuesta de límite**, no una inferencia de duración de todos los turnos. Una asignación más larga exige reautenticación planificada en condición segura sin detener procesos de fondo. Validar ergonomía de credencial/PIN y tiempos con usuarios reales y acuerdos vigentes; no añadir enrolamiento previo ajeno a la nombrada. C2 evalúa lectores/credenciales y compatibilidad; no se da por ofertado hardware adicional.

Las credenciales de acceso a servicios serán firmadas y de vida breve: **5 min propuestos**; al autenticar se renueva el identificador de sesión y la credencial de refresco rota en cada uso. Reutilizar un refresco anterior invalida la familia y genera alerta. Renovar credenciales no prolonga el máximo de sesión, el turno ni una asignación vencida. Los identificadores no viajan en rutas URL ni se registran como secretos en logs. En web, sesión mediante cookies protegidas HttpOnly/Secure y protección contra solicitudes falsificadas; en app, almacenamiento protegido del sistema. Detalles de cliente/protocolo se verifican con A1/A2.

Cerrar SSO invalida la sesión común y las derivadas en los módulos conectados. Cada servicio consulta estado de sesión/revocación en su ámbito antes de aceptar la acción: **no basta esperar a que venza un token de 5 min** para bloquear un acceso revocado. Mecanismo de distribución, caché y latencia de invalidación por probar con A2/C3, incluidos los objetivos de desempeño. Si no puede comprobarse autorización, no se conceden nuevas facultades; los procesos automáticos de seguridad y continuidad mantienen identidades de servicio propias.

#### B2.4 Terminal aislada, baja y revocación

La terminal fuera de cobertura recibe antes del aislamiento una autorización offline **firmada, ligada a dispositivo, identidad, tarea, zona y vigencia**, distinta de una sesión web o permiso para llamar APIs. Vigencia máxima propuesta: el menor valor entre 8 h desde emisión, fin del turno/asignación y vencimiento de acreditación. Habilita solo el subconjunto local necesario; no permite administración, cambio de roles o acceso general a datos. La aplicación protege su almacenamiento, verifica integridad/vigencia y detecta retroceso del reloj; ante anomalía deriva la interacción a una condición segura, conservando registros ya capturados.

La sesión de interacción puede bloquearse/reabrirse localmente con la credencial del titular, sin renovar el permiso offline. El registro automático de movimientos y alertas no depende de que esa sesión esté desbloqueada. Antes de cambiar turno se necesita una autorización vigente para la nueva persona: emitida/verificada por el servicio local o preaprovisionada desde una asignación confirmada. Una terminal aislada no inventa nuevas nombradas; el relevo sin cobertura aún debe validarse en el escenario A3, con provisión previa o punto local de habilitación disponible.

**Revocación conectada:** bloquear identidad, sesiones y refrescos en cuanto la autoridad de identidad recibe la orden; propagar a sus puntos de aplicación y auditar recepción/aplicación. **Sin enlace exterior:** registrar la baja directamente en el ámbito local mediante responsable facultado y comunicación alternativa verificada, si existe. **Terminal completamente aislada:** no se promete recepción instantánea. Se requiere aviso operativo y retiro/bloqueo físico del equipo o recuperación de conectividad para aplicar la baja anticipadamente; el permiso vence por sí mismo al límite indicado.

La baja ≤24 h se mide desde la desvinculación, no desde que vuelve Internet. La propuesta debe demostrar que el aviso llega a responsables locales y equipos dentro de ese plazo. El vencimiento acotado reduce exposición pero **no demuestra cumplimiento de la revocación inmediata de FEP02 RT-12.07**. Si no existe un procedimiento fiable, permanece la brecha `F3-ESC-002`; requiere validación/consulta formal del tratamiento conjunto de RT-12.07 con el offline del caso. No se declara una excepción contractual aprobada ni se permite una sesión indefinida para ocultar la tensión.

#### B2.5 Reconexión, emergencia y evidencia

**Reconexión:** primero intercambiar bloqueos y versiones de políticas antes de renovar permisos conectados. Una baja no se deshace porque una copia antigua diga «activo»; una rehabilitación requiere acto autorizado posterior explícito. Conservar los eventos históricos y su identidad, autorización vigente al ejecutar, dispositivo, secuencia y marcas de tiempo. No borrar movimientos por haberse revocado después a su autor. Eventos cuya autorización no pueda verificarse se preservan y marcan para investigación; la conciliación de negocio es responsabilidad de A3 y debe mantener el objetivo ≤90 min sin pérdida.

**Emergencia:** proponer una cuenta de último recurso por ámbito administrado, fuera de la federación que podría fallar, con secreto custodiado en bóveda local protegida y copia de recuperación bajo doble custodia. Registrar quién retira la credencial, motivo, alcance y aprobador; habilitar solo el plazo necesario, con máximo propuesto de 30 min y registro local independiente/grabación de acciones de mayor riesgo. Tras uso: cerrar sesiones, rotar secreto y revisar evidencia. Custodios y suplencias quedan por asignar; no es una cuenta de uso diario ni permite violar restricciones de grúas/ISPS. A3 debe validar el procedimiento de urgencia cuando no sea posible el doble control previo, conservando atribución y revisión posterior; no queda autorizado aquí un bypass genérico.

**Identidades técnicas:** separar cuentas de servicio por integración/ambiente y proteger claves; no usar refrescos ni MFA humanos en procesos automáticos. Certificados o credenciales de servicio deben poder verificarse/renovarse localmente durante la autonomía exigida. Su mecanismo, duración y recuperación quedan en el bloque de claves y ADR-009; no reutilizar automáticamente el permiso offline de una persona.

La auditoría recoge altas, cambios, nombrada/acreditación validada, emisión, inicio/cierre/relevo, intentos denegados, renovación/reutilización, elevación, revocación, baja y emergencia. Conservar correlación y resultado, sin PIN, tokens ni secretos. Retención: logs de seguridad 12 meses en línea +24 en archivo; eventos de acceso físico 5 años cuando corresponda según Maestro §16.1, sin confundir ambos conjuntos. Inmutabilidad, buffer y capacidad se concretan en el bloque de registros/C4.

#### B2.6 Entrada temprana de identidad para Física y pruebas pendientes

Este detalle refina **SEC-IAM-01**, sin declarar completo el paquete SEC-PHYS-v0.1.

| Capacidad requerida | Ubicación/restricción propuesta | Entrada a C1–C4 / evidencia prevista |
|---|---|---|
| SRV-IAM con gobierno común, validación/emisión local y SSO | Capacidad local sin dependencia exclusiva de nube, redundante según criticidad | Comparar productos compatibles, HA, directorio real y consumo de recursos; prueba 72 h con turnos nuevos |
| Autenticación personal en puestos y cabinas | Credencial/PIN y lector compatible con terreno si se selecciona esta alternativa | Verificar reutilización de equipos; cantidades desde puestos/usuarios y stock justificado, sin cifras inventadas; ensayo 380 credenciales ≤30 min y relevo |
| Autorización offline y almacenamiento protegido | Terminal de patio, ligado a dispositivo y asignación | Prueba 8 h sin cobertura, expiración, cambio de persona, reloj alterado, pérdida de equipo y recuperación de registros |
| PAM, MFA y emergencia local | Acceso administrativo separado con custodia y registro local | Licencias/servicio candidatos según usuarios y sesiones; probar caída IAM, elevación, grabación, rotación y restauración |
| Revocación y conciliación | Nube/local/terminal según conectividad, con procedimiento operativo de bajas | Medir cierre SSO, acceso denegado tras baja, reinicio sin reactivar cuenta y reconciliación ≤90 min; resolver F3-ESC-002 |

Los criterios de aceptación deben incluir funcionamiento normal, corte exterior, aislamiento de terminal, relevo, baja durante corte, caída del IAM local, reconexión y uso de emergencia. C3 prueba el fallo de energía/infraestructura además del corte de enlace; D1 aporta la evidencia de identidad. Ninguna prueba se ha ejecutado.

#### B2.7 ADR-008 — propuesta condicionada de patrón IAM

- **Fecha:** 2026-09-05.
- **Estado:** `PROPUESTO`; aprobación condicionada a resolver `F3-ESC-001/002`, validar el directorio/federación real y confirmar soporte en producto. No está `APROBADO`.
- **Propietario:** Frente 3; responsable nominal por asignar.
- **Fuentes y requisitos:** FEP02 Cap. 12 RT-12.01..13; RNF-DIS-02/03/04; RNF-SEG-10; RF-ACC-01..05; Maestro §§9/11.2.
- **Contexto y fuerza de decisión:** identidad centralizada y SSO deben coexistir con 72 h locales, turnos nuevos y TI=5.
- **Alternativas evaluadas:** (A) IAM solo nube con sesiones cacheadas: sencillo de operar pero insuficiente para renovar turnos y administrar bajas locales; (B) IAM gobernado localmente, publicado de forma segura para nube: autonomía local, pero riesgo de dependencia del terminal para usuarios externos; (C) gobierno común con capacidad local delegada y ámbito nube: permite continuidad diferenciada, a costa de reconciliar políticas y revocaciones.
- **Criterios ponderados:** autonomía y restricciones obligatorias son excluyentes; luego operabilidad TI=5 y consistencia de autorización (peso alto), compatibilidad de directorio/legados y recuperación (alto), simplicidad/capacidad y esfuerzo operacional (medio). Ponderación cualitativa; no inventar puntajes de productos sin evaluar.
- **Decisión:** adoptar C como línea base **propuesta** para integración y dimensionamiento, con alcance local acotado según B2.2. No implica dos catálogos independientes, un producto desarrollado a medida ni aprobación de una marca; C1–C4 pueden dimensionar la capacidad IAM local, pero deben confirmar soporte antes de cerrar.
- **Consecuencias positivas:** turnos y funciones locales independientes del enlace; nube puede conservar identidad externa; políticas comunes.
- **Consecuencias negativas y riesgos residuales:** complejidad de delegación/sincronización; custodia de claves locales; revocación en dispositivo aislado; disponibilidad de nuevas nombradas; costos operacionales por dimensionar sin precios en Informe 1.
- **Impacto lógico, físico, seguridad, capacidad y T-11:** SRV-IAM/EDGE-RUN, PAM, lectores/credenciales si proceden, HA y almacenamiento local; C1–C4 validan nodos, productos, cantidades y filas.
- **Validación y evidencia:** B2.6; A1/A2/A3 y C1–C4; directorio externo y procedimientos con CLIENTE. Consultar explícitamente (1) compatibilidad del directorio y mecanismo de federación existentes y (2) cómo cumplir o exceptuar formalmente la revocación inmediata cuando el terminal permanece hasta 8 h aislado o el puerto hasta 72 h sin enlace, incluido aviso y bloqueo/retiro local. `F3-ESC-001/002` permanecen abiertos.
- **Condición de revisión/sustitución:** producto incompatible con autonomía/SSO, revocación sin tratamiento aceptable, nombradas inaccesibles o carga de operación inviable; comparar nuevamente B y otras implementaciones del mismo patrón antes de aprobar.

### B3. Zonas, conductos y exposición — propuesta

**Fecha:** 2026-09-05. **Estado: EN CURSO.** Borrador independiente utilizable por A2/C1/C3; no es una topología aprobada ni una configuración ejecutada. Se revisaron sus contratos actuales: todavía no contienen interfaces ni redes definitivas. Las zonas `Z-*` y flujos `FL-*` siguientes son referencias locales de D1 para validar en F3-DEP-002/003; no reemplazan los IDs de componentes del Maestro ni asignan subredes, VLAN, nodos o productos.

#### B3.1 Zonas propuestas y fronteras de confianza

Una zona agrupa recursos con políticas de acceso similares. Cruzar una frontera requiere autorización explícita; estar en la misma zona tampoco concede acceso indiscriminado. Una zona no implica comprar un servidor o firewall por fila. C1/C3 pueden materializar varias mediante controles de plataforma/red, conservando aislamiento verificable.

| Zona D1 | Recursos o actores de referencia | Regla y justificación |
|---|---|---|
| Z-EXT — redes externas | ACT-NAV/AGE/TRA/AUT/FER/CON/VER y sistemas de terceros | Ninguna identidad ni dirección externa es confiable por sí misma; entrada solo por punto publicado y contrato autorizado |
| Z-EDGE — borde expuesto | GW-EDGE; publicación de CH-PORTAL y acceso remoto de CH-APP | CDN/WAF/DDoS/TLS; único acceso público a servicios, sin publicación directa del origen |
| Z-SVC — servicios privados nube | perfil central de GW-API y contextos ubicados en nube por C1 | Autorizar por identidad, recurso y operación; no asignar aquí todos los contextos a nube |
| Z-LOCAL — servicios operacionales locales | EDGE-RUN, perfil local restringido de GW-API, capacidades críticas, SRV-IAM local e INT-TOS | Mantener 72 h sin enlace exterior; toda acción crítica entra por el gateway local y no depende del borde ni del gateway central nube |
| Z-FIELD — equipos de terreno | CH-CAB, CH-APP interno, gate, sensores y lectores | Identidad de dispositivo/persona según flujo; limitar alcance a servicio/tarea. C3 subdivide por criticidad y fabricante, sin presumir que todos soportan agente o TLS |
| Z-ADM — red administrativa | Puestos ACT-COM y usuarios administrativos | Acceso a servicios autorizados, sin ruta general a patio, protección o base de datos |
| Z-PROT — protección | EXT-VMS y EXT-ACC según red real y plan de protección | Mantener autoridad y operación ISPS; intercambio solo autorizado por adaptador, sin portal de video ni tránsito general a la red operacional |
| Z-MGMT — administración técnica | Acceso de ACT-TI y soporte autorizado mediante PAM | Separar administración de uso de negocio; sin consolas públicas directas ni acceso libre desde Z-ADM |
| Z-DATA — almacenes protegidos | DATA-CORE/TS/DOC/AN donde C1 los ubique | Solo identidades de servicio con permisos por necesidad. Es un ámbito de políticas en nube/local, no una única base o red extendida |

DEV, QA, PREPROD, PROD y DR son ambientes separados **dentro de los que corresponda materializar estas fronteras**, no cinco zonas con acceso mutuo. No se permite ruta general de desarrollo a producción; despliegue automatizado y administración excepcional se concretan en B6/C3. Los sistemas conservados TOS/ERP/grúas/báscula no se reubican por esta tabla: A2/C1 confirman dónde están y por qué frontera se integran.

#### B3.2 Matriz inicial de comunicaciones permitidas

Regla común: denegar flujos no declarados; habilitar únicamente origen, destino, dirección, finalidad y servicio necesarios, con registro de rechazos relevante. Una relación bidireccional de negocio no autoriza cualquier conexión en ambas direcciones: A2 precisa quién inicia cada sesión. Puertos/versiones e interfaces no confirmados permanecen POR LEVANTAR. Las amenazas se formalizan después en D2.

| Flujo | Origen → destino / componentes | Finalidad y datos | Identidad y control | Desconexión / validación |
|---|---|---|---|---|
| FL-01 | Z-EXT → Z-EDGE → Z-SVC; CH-PORTAL/APP, GW-EDGE/API | Consultas/trámites; datos públicos mínimos o expediente autorizado | SEC-EDGE-01/02 y SEC-API-01; B1/B2 para identidad/MFA. Acceso anónimo solo a operaciones expresamente públicas, nunca a información sensible | Portal podría continuar; frescura y autoridad por función según B2.1; A1/A2 |
| FL-02 | Z-FIELD/Z-ADM → Z-LOCAL o Z-SVC mediante servicio autorizado | Movimientos, gate, reefer, planificación y gestión según rol | SEC-NET-01/SEC-API-01; dispositivo y usuario cuando interactúa una persona; aplicación nunca accede directamente a BD | Funciones críticas usan ruta local durante 72 h; terminal aislada usa B2.4. A1/A3/C3 precisan rutas |
| FL-03 | Z-LOCAL ↔ Z-SVC; EDGE-RUN, INT-HUB y servicios propietarios | Sincronización de hechos/estados/políticas, sin mezclar autoridad de dominios | Canal cifrado/autenticado, identidad de servicio, permisos por contrato, integridad y protección contra repetición; SEC-SYNC-01 | Persistencia local y conciliación ≤90 min; cambios de política según B2.5; A2/A3/C4 |
| FL-04 | INT-TOS ↔ EXT-TOS12 | Coexistencia de operaciones según dominio×zona×fase | Adaptador y cuenta técnica acotados; no exponer TOS ni otorgar escritura fuera de autoridad confirmada | Falla parcial/retorno con A3; contrato real y capacidad de cifrado por levantar |
| FL-05 | CTX-BILL vía integración ↔ EXT-ERP | Hechos/evidencia y estados de conciliación | Servicio autorizado y trazabilidad 1:1; ERP único emisor tributario | Hechos se capturan localmente; envío/consulta según conectividad real de ERP, no asumir caída por perder Internet |
| FL-06 | EXT-NAV/AUT/FER ↔ INT-HUB por ingreso/egreso controlado | Mensajes marítimos, inspecciones y coordinación | Identidad por contraparte, contrato/versionado, esquema, autorización y evidencia; no inventar protocolo de transporte | A2 confirma adaptador/fallback. Alianza 2029 conserva exclusividad estándar; no introducir puente manual |
| FL-07 | Integración autorizada ↔ Z-PROT; EXT-ACC/VMS | Habilitaciones/eventos de acceso y eventos/metadatos/evidencia VMS confirmados | Conducto mínimo aprobado por protección; sin streaming general ni administración desde red operacional | Mantener protección durante cambios; contrato y dirección exacta con A2/C3/CLIENTE |
| FL-08 | Periferia → adaptadores locales; EXT-GRU/VGM/OCR y sensores | Lecturas de grúa autorizadas, pesajes, OCR, telemetría | Identidad/canal según capacidad real; validación de origen y payload. Grúa sin comandos de control; báscula conserva su autoridad | No imponer software o cambios al fabricante; segregación y compatibilidad por validar |
| FL-09 | Z-MGMT → plataformas autorizadas en nube/local | Administración técnica | SEC-ADM-01; B2 PAM/MFA, elevación, alcance y grabación; acceso por intermediario controlado | Emergencia local B2.5; C3 valida accesibilidad y fallos del propio PAM |
| FL-10 | Servicios/zonas → colectores y destinos aprobados | Logs, métricas, tiempo, resolución de nombres, notificaciones y servicios de certificados | Identidades/permisos mínimos; salidas permitidas por destino/servicio, sin salida Internet indiscriminada | Inventariar dependencias con A2/C3; tiempo, nombres y registros locales no pueden depender solo de nube |
| FL-11 | Servicios autorizados → Z-DATA | Persistencia, consulta y evidencia | Identidad técnica por servicio/ambiente, cifrado y permisos por datos; sin acceso UI→BD | Rutas locales críticas continúan; detalle de llaves/datos en B4, ubicación C1 |

FL-10 es una familia por desglosar, no una regla «permitir cualquiera». FL-06/08 tampoco sustituyen el inventario completo de 21 contrapartes y siete familias de A2. DR, respaldos y despliegue requieren flujos específicos a completar con B4/B6/C3; no quedan autorizados implícitamente por esta matriz.

#### B3.3 Decisiones de control y trazabilidad directa

| Control / decisión propuesta | Requisito que resuelve | Aplicación y motivo de selección | Evidencia prevista / límite |
|---|---|---|---|
| SEC-NET-01 — segregación y conductos explícitos | RNF-SEG-06; Caso 06 Cap. 15 RT-03.24 y Cap. 10 restricción 6; FEP02 RT-11.01 | Separar operación, administración y protección; controlar también servicio a servicio. Una red común con confianza por ubicación permitiría movimiento lateral | Matriz B3.2 y prueba de rutas permitidas/denegadas; C3 materializa aislamiento, D2 amenazas |
| SEC-EDGE-01 — publicación exclusiva mediante borde protegido | FEP02 Cap. 11 RT-11.07/12; Maestro §6 | CDN para contenido público estático; WAF gestionado más reglas de trámites; anti-DDoS L3/L4/L7 gestionado. Capacidad especialista compatible con TI=5 (RNF-OPE-08), sin producto elegido | Intento de bypass al origen debe fallar; prueba de reglas, capacidad y tráfico legítimo. Orígenes privados o restringidos al borde con autenticación de origen |
| SEC-EDGE-02 — TLS y ciclo de certificados | FEP02 Cap. 11 RT-11.08; RNF-SEG-04 | TLS 1.3 en servicios de la solución; cifrados modernos, TLS 1.0/1.1 prohibidos. No usar terminación en borde para dejar salto interior en claro | Escaneo de cada terminación y salto; HSTS/renovación/alertas y compatibilidad en B3.4; legado incompatible no se declara conforme |
| SEC-API-01 — controles del gateway y autorización en el servicio | FEP02 Cap. 11 RT-11.01/11; RF-POR-02/09; RF-INT-02; RNF-SEG-09 | Autenticación, autorización, cuotas, límite de tasa, esquema y payload. El perfil central cubre el servicio completo; el perfil local restringido usa política vigente cacheada y solo enruta las operaciones de continuidad. El servicio comprueba organización/recurso; WAF no reemplaza permiso de negocio | Pruebas de identidad, objeto ajeno, esquema inválido, tamaño y abuso; además corte 72 h recorriendo `CH-APP/CH-CAB → GW-API local → CTX/DATA/evidencia local`, sin acceso directo |
| SEC-ADM-01 — administración aislada y temporal | FEP02 Cap. 11 RT-11.27 y Cap. 12 RT-12.03/06/13 | Consolas detrás de acceso controlado/PAM; MFA y cuenta nominativa, sin SSH/RDP/BD públicos directos ni desarrollo interactivo permanente | Escaneo externo y prueba de acceso/PAM/emergencia; B2.3/2.5, producto C2/C3 |
| SEC-SYNC-01 — conducto nube/local independiente del tráfico público | RNF-DIS-02/04; RNF-SEG-04; Maestro §§6.2/8/9 | Canal mutuamente autenticado para servicios compatibles y cifrado, contrato acotado y registro persistente. No extender confianza de toda la red ni exigir nube para una acción crítica local | Corte 72 h, reintento/repetición y conciliación ≤90 min; A2 define transporte y A3 autoridad, ADR-009 custodia |
| SEC-EXP-01 — inventario de exposición y control de cambios | FEP02 Cap. 11 RT-11.13 | Declarar cada dominio, puerto y servicio externo, incluyendo acceso administrativo/federación si son alcanzables; contrastar configuración e inventario | B3.5, escaneo externo y revisión tras cambios; listado actual es plantilla poblada por familias, no inventario final |

Los IDs SEC-* identifican controles, no nuevos RF ni ADR aprobados. La justificación explica cómo se atiende el requisito; las pruebas previstas deben comprobarlo y todavía no se han ejecutado.

#### B3.4 Capa pública, certificados y límites operacionales

**Recorrido propuesto:** persona/sistema externo → borde protegido → gateway privado → servicio autorizado → dato permitido. La identidad de negocio se conserva hasta el servicio; solo se aceptan cabeceras de identidad/proxy de intermediarios confiables. No publicar IP/puerto alternativo del origen para eludir WAF. CDN no guarda respuestas autenticadas, datos de carga ni documentos sensibles por defecto; definir explícitamente caché solo para contenido público y controlar descargas por expediente.

**WAF y abuso:** combinar reglas gestionadas con validación adaptada a formularios, API y carga documental. Ante abuso humano usar reto progresivo accesible; no aplicar CAPTCHA a mensajes máquina ni bloquear integraciones legítimas por una regla genérica. APIs máquina usan identidad, esquema, cuota y límites. Los valores de tasa, tamaño y tiempo se fijan con A2/C4, respetando RNF-DES-09..12 y objetivos portuarios: no inventar un límite que impida archivos/lotes exigidos. El análisis de archivos debe aislar contenido hasta validación, sin presentarlo como documento aceptado antes de completar controles.

**Certificados:** inventariar propietario, dominio/servicio, emisor, vigencia, ubicación de clave y dependencias de renovación. Automatizar emisión/renovación y despliegue con solapamiento controlado; propuesta de alertas a 30/15/7 días para certificados cuya vigencia lo permita, o umbrales relativos para vida más breve, además de alerta inmediata por fallo de renovación. Son parámetros del equipo, por validar con el producto. B4 define custodia y recuperación; no guardar claves privadas en repositorio.

**HSTS con precarga:** preparar dominios web públicos y subdominios bajo control del equipo para HTTPS permanente, verificar compatibilidad completa y tramitar precarga del dominio correspondiente antes de declarar cumplimiento. El alcance real del dominio pertenece al CLIENTE y sigue por validar; una cabecera no demuestra que el dominio ya esté precargado. No aplicar una política heredable sin inventariar servicios afectados.

**Continuidad:** renovación, validación de confianza, resolución de nombres y tiempo deben seguir disponibles en el ámbito local durante 72 h. No desactivar validación de certificados ni aceptar vencidos por estar offline. Definir material de confianza, validez y renovación local con B4/C3; probar un vencimiento durante el corte. Si un tercero/legado no admite el cifrado exigido, registrar incompatibilidad y alternativa autorizada: un adaptador protege su tramo compatible, pero no convierte mágicamente el tramo legado en TLS 1.3.

**Falla de borde:** nube/borde deben tener redundancia y recuperación compatibles con 99,95 % de infraestructura y 99,9 % E2E de servicios críticos donde corresponda. No se atribuye disponibilidad por escribir «multi-AZ»: C1–C4 verifican dependencias, capacidad y pruebas. Una caída del borde público no debe interrumpir la ruta local crítica. No habilitar un acceso directo sin controles como fallback.

#### B3.5 Inventario de exposición por completar

Esta tabla inicia el levantamiento. Antes del cierre se sustituye cada familia por **una fila por dominio/puerto/servicio real**, incluidos endpoints de proveedores expuestos a usuarios/administradores. «POR VALIDAR» no equivale a «NO APLICA» ni autoriza publicación.

| Familia | Dominio/IP y puerto | Servicio y componente | Audiencia / autenticación | Control / ubicación propuesta | Dueño y pendiente |
|---|---|---|---|---|---|
| Portal y API pública | Dominio POR VALIDAR; HTTPS TCP 443 propuesto | CH-PORTAL / GW-EDGE → GW-API | Personas externas, operaciones públicas explícitas y autenticadas B2 | SEC-EDGE-01/02/API-01; borde nube | Equipo plataforma por asignar; A1/A2/C1 |
| Identidad externa | Dominio POR VALIDAR; HTTPS TCP 443 propuesto | SRV-IAM, federación/registro/recuperación si requiere endpoint público | Personas/clientes autorizados; B2 | Borde/control del proveedor por validar; no presumir protección incluida | CLIENTE/proveedor por confirmar F3-ESC-001 |
| Integraciones de contrapartes | Dominios/IP/puertos POR LEVANTAR | Ingreso/egreso INT-HUB por contraparte | Identidad máquina y contrato específico | FL-06; borde si publicado; canal privado si contrato lo establece | A2 y contraparte; Maestro ESC-06 |
| Acceso administrativo remoto | Dominio/puerto POR VALIDAR según solución | Intermediario de acceso/PAM; consolas origen privadas | Personal autorizado, MFA/PAM | SEC-ADM-01; entrada externa controlada | C2/C3, sin consolas directas publicadas |
| Conducto nube–local | Extremos/puertos POR VALIDAR; iniciador según A2/C3 | EDGE-RUN / integración | Identidades técnicas acotadas | SEC-SYNC-01; canal cifrado controlado | A2/C3; declarar si alguno es alcanzable desde exterior |

Para cada fila final añadir: ambiente, dirección/iniciador, protocolo/versión, propietario, datos expuestos, regla origen/destino, certificado, dependencia/HA, responsable de cambio y evidencia de escaneo. Las salidas hacia terceros se inventarían aparte como dependencias aunque no constituyan servicios entrantes. DNS, emisor de certificados, identidad gestionada o notificaciones no se omiten por ser servicios de proveedor.

#### B3.6 Entrega a Física y verificación del bloque

| Aporte | Capacidad para C1–C4/T-11 | Validación concreta |
|---|---|---|
| SEC-NET-01 | Segmentación y filtrado entre zonas; controles de plataforma/host según despliegue | Intento desde red administrativa o protección a servicio operacional no autorizado debe fallar; flujos aprobados continúan |
| SEC-EDGE-01/02/API-01 | Borde gestionado, CDN/WAF/DDoS, gateway y certificados; dimensionamiento por contratos/carga | Origen inaccesible por bypass, TLS correcto, abuso rechazado, carga legítima/descarga autorizada y accesibilidad preservadas |
| SEC-ADM-01 | Acceso administrativo intermediado y PAM; reutilizar aporte de B2 | No duplicar licencia/servicio por aparecer en dos bloques; demostrar bloqueo externo y acceso excepcional controlado |
| SEC-SYNC-01 | Canal nube/local, capacidad y controles de integración | Corte de enlace conserva operación local, registros e identidad; retorno sin pérdida/repetición y sincronización ≤90 min |
| SEC-EXP-01 | Inventario y verificación de configuración/exposición | Inventario final coincide con dominios/puertos observados, incluidos proveedores; ningún «POR VALIDAR» convertido en hecho |

**Pendientes para cerrar B3:** A2 desglosa contratos/iniciadores/puertos y funciones nube durante corte; C1/C3 confirman zonas/rutas/failover; C2 compatibilidad y productos; C4 capacidad/límites; CLIENTE valida dominios, protección y terceros; D2 revisa amenazas. Pruebas de migración de red deben mantener VMS/ISPS y respetar restricciones de intervención del Maestro; no se propone modificar redes productivas en este trabajo documental. Próximo bloque independiente: **B4, datos, claves y secretos**. SEC-PHYS-v0.1 sigue parcial hasta consolidar B4–B7.

### B4. Datos, claves y secretos — propuesta

**Fecha:** 2026-09-05. **Estado: EN CURSO.** Este bloque define controles de arquitectura, no el modelo detallado de datos ni un producto ofertado. Subdocumento 5 mantiene la propiedad de dominio, campo, fuente de verdad, calidad y ciclo de vida; D1 fija la protección mínima y las capacidades físicas/lógicas que deben soportarla. Las categorías y correspondencias actuales se validan mediante `F3-DEP-004`. Todos los datos en reposo se cifran; la clasificación decide controles adicionales, no si existe cifrado básico.

#### B4.1 Clasificación inicial y regla de herencia

Se propone una taxonomía común de cuatro niveles. El nivel de un conjunto es el mayor nivel de cualquier campo o documento que contenga. Una copia, exportación, caché, índice, cola, respaldo o réplica hereda la protección de su fuente mientras conserve el dato. Los metadatos también se clasifican: una secuencia de posiciones, identificadores o tiempos puede revelar ruta, cliente o contenido aunque cada valor aislado parezca inocuo.

| Nivel propuesto | Ejemplos del caso | Acceso y tratamiento mínimo | Validación pendiente |
|---|---|---|---|
| `PUB` — público controlado | estado mínimo seguro del contenedor; condiciones de acceso y congestión expresamente publicables | Publicación solo mediante CH-PORTAL/GW-EDGE; integridad, disponibilidad y minimización. No incluir dueño, ruta, contenido, valor, documentos ni posición detallada | A1/Subdoc. 5 y CLIENTE confirman campos realmente públicos |
| `INT` — interno | configuración no secreta, catálogos operativos sin dato sensible, documentación y métricas internas agregadas | Identidad interna o de servicio autorizada; cifrado en tránsito/reposo; no exposición pública ni exportación indiscriminada | Propietario y uso por contexto |
| `CONF` — confidencial | movimientos y posición operacional, planes, citas, inspecciones, telemetría, indicadores no públicos, hechos/evidencias y documentos comerciales ordinarios | Necesidad de saber, ámbito por organización/expediente, cifrado en tránsito/reposo, acceso y exportación auditados cuando corresponda | Subdoc. 5 separa campos y retención; A1 confirma consumidores |
| `RES` — restringido | datos personales de trabajadores/eventuales/conductores/visitantes; tarifas y volúmenes negociados; datos que permitan inferir contenido de valor o ruta; credenciales, secretos, claves privadas y material de recuperación | Controles de `CONF` más cifrado de campo para las categorías exigidas, acceso mínimo, consulta/modificación auditadas y revelación en claro solo al servicio/rol autorizado. Claves y secretos nunca se almacenan como campos de negocio | Catálogo de campos de Subdoc. 5; base de licitud/transferencia y tratamiento con cumplimiento |

La evidencia facturable, firmas, actas e imágenes no se declaran automáticamente públicas por estar destinadas a terceros: se clasifican por contenido y expediente. `DATA-AN` no queda exento por usar datos agregados; debe demostrar anonimización suficiente antes de reducir nivel. Los ambientes no productivos no reciben datos productivos reales salvo anonimización o seudonimización verificable conforme RT-11.25; B6 completa el control de provisión y prueba.

#### B4.2 Matriz dato–almacén–protección

| Familia del Maestro | Nivel inicial | Protección propuesta | Continuidad y límite |
|---|---|---|---|
| `DATA-CORE` — estado transaccional | `CONF`, con campos `RES` | Cifrado de volumen/servicio y base; cifrado de campo para datos personales, comerciales sensibles y carga/ruta; claves separadas por ambiente y dominio de protección | Parte crítica disponible localmente 72 h según autoridad; no convertir la réplica local en fuente universal |
| `DATA-TS` — reefer/equipos | `CONF`; identificadores/ubicación pueden elevarse a `RES` | Cifrado en almacén, tránsito e índices; acceso por equipo/operación; evitar etiquetas sensibles en métricas o logs | Buffer local para monitoreo/alarma; retención y agregación según Maestro §16/Subdoc. 5 |
| `DATA-DOC` — expedientes/evidencia | `CONF` o `RES` según contenido | Objetos y metadatos cifrados; integridad/firma cuando corresponda; descarga autorizada por expediente; análisis aislado antes de aceptar | Evidencia crítica se captura localmente; claves de objetos necesarios no dependen solo de nube |
| `DATA-AN` — indicadores/emisiones | `INT` o `CONF`; `RES` si conserva granularidad identificable | Almacén separado del OLTP, cifrado y vistas por audiencia; anonimización/minimización antes de uso secundario | Puede quedar desactualizado durante corte; mostrar fecha de actualización y no afectar operación crítica |
| Colas, cachés, archivos temporales e índices | heredan de la fuente | Cifrado, expiración, permisos de servicio y eliminación controlada; no usar caché pública para contenido autenticado/sensible | Colas locales dimensionadas por C4; temporales no pueden evadir retención o auditoría |
| Exportaciones y respaldos | heredan del dato de mayor nivel | Cifrado antes de salir del servicio, trazabilidad de generación/descarga, integridad y custodia separada | Respaldo 3-2-1-1-0; una copia fuera de sitio y una inmutable/fuera de línea sin perder recuperabilidad |

La selección de algoritmo, modo y tamaño de clave se fija mediante un estándar criptográfico versionado y compatible con productos escogidos, sujeto a revisión tecnológica. No se inventa aquí una suite distinta de la exigencia TLS 1.3 de B3.4. Un almacén que anuncie cifrado por defecto debe aportar configuración, alcance y administración de claves; el nombre comercial no demuestra cobertura de discos, réplicas, snapshots, exportaciones y respaldos.

#### B4.3 Cifrado de campo y exposición controlada

`SEC-FIELD-01` protege los campos exigidos por `RNF-SEG-05`: datos personales, tarifas/volúmenes negociados y datos que permitan inferir contenido de valor o ruta. Se propone cifrado de aplicación o servicio antes de persistir, usando cifrado por envoltura: una clave de datos versionada protege el valor y una clave de protección administrada por `SEC-KEY-01` protege la clave de datos. La base no recibe la clave maestra ni devuelve el valor en claro a una consulta directa.

Las búsquedas sobre campos restringidos se resuelven mediante identificadores sustitutos, índices derivados protegidos o servicios de consulta autorizados; no mediante una copia paralela en claro. Cualquier técnica que preserve igualdad u orden debe evaluarse por filtración asociada antes de usarse. Las interfaces, eventos y logs transportan solo los atributos necesarios y aplican enmascaramiento; no se registran secretos, tokens, documentos completos ni valores restringidos como texto libre.

La aplicación descifra únicamente dentro del servicio autorizado y devuelve una vista mínima conforme B1/B2. Las operaciones de descifrado, exportación y cambio de clave quedan auditadas con identidad, finalidad, expediente y resultado, sin incluir el dato sensible en el registro. Subdocumento 5 entrega el catálogo final campo→propietario→sensibilidad→retención; hasta entonces esta matriz no acredita el 100 % de campos.

#### B4.4 Jerarquía de claves, certificados y secretos

| Material | Patrón propuesto | Restricción principal |
|---|---|---|
| Claves raíz/de protección | KMS, HSM o servicio de claves/bóveda con límite criptográfico protegido, separado por ambiente y ámbito nube/local | No exportables en claro; administración distinta del consumo; acceso excepcional bajo doble control |
| Claves de datos | Generadas por dominio/almacén o conjunto, versionadas y protegidas por clave superior | Un compromiso no expone todos los dominios; conservar versión para descifrar historia durante retención |
| Claves de cifrado de campo | Separadas al menos por ambiente y categoría/dominio restringido | La base de datos no posee facultad general de descifrado; acceso solo por servicio autorizado |
| Certificados TLS y confianza | Inventario y automatización de B3.4; claves privadas en KMS/HSM/vault o almacén protegido del componente | Sin claves en repositorio; renovación solapada, cadena y revocación disponibles según conectividad |
| Firma de sesiones/offline/evidencia | Claves diferenciadas por propósito y ámbito; verificadores públicos distribuidos de forma controlada | No reutilizar una clave TLS para firmar permisos o evidencia; capacidad local limitada a su función |
| Secretos de aplicación/integración | Vault o servicio de secretos; identidad de carga para obtención dinámica cuando el producto lo permita | No embebidos en código, imagen, manifiesto, script, documento, log ni variable persistida sin protección |
| Recuperación y último recurso | Material de recuperación cifrado, inventariado y sellado bajo custodios separados | No es una clave universal de operación diaria; uso genera alerta, evidencia, revisión y rotación posterior |

La jerarquía lógica es común, pero **no exige una única instancia global**: una sola dependencia de red rompería la autonomía. Tampoco exige comprar un HSM por cada servicio. C1/C2 comparan servicio KMS gestionado, HSM administrado/compartido y vault compatible según criticidad, residencia, latencia, operación con TI=5, portabilidad y soporte local. Los componentes consumidores reciben operaciones o claves de datos acotadas; no credenciales administrativas del KMS.

#### B4.5 Custodia y separación de funciones

| Función | Puede | No puede por sí sola |
|---|---|---|
| Propietario del dato | aprobar finalidad, audiencia y cambio de clasificación | administrar o extraer claves privadas |
| Custodia de claves/seguridad | administrar políticas, versiones y recuperación autorizada | leer datos de negocio por su sola función ni aprobar su propio acceso excepcional |
| Plataforma/operación | integrar servicios, ejecutar rotación automatizada y atender fallas | exportar raíz, desactivar auditoría o destruir versiones necesarias sin aprobación |
| Servicio consumidor | cifrar/descifrar solo su ámbito mediante identidad técnica | administrar KMS/vault, usar claves de otro ambiente/dominio o entregar material a una persona |
| Respaldo/continuidad | crear copias protegidas y ejecutar restauración autorizada | borrar copia inmutable y claves de recuperación con la misma autoridad operacional |
| Auditoría/SOC | consultar eventos de uso, cambios y alertas | descifrar datos por defecto o modificar evidencia |

La separación es funcional y mediante permisos/flujo; con TI=5 no se presupone una persona exclusiva por fila. Las operaciones destructivas o de recuperación de mayor impacto requieren aprobación distinta y doble control. Nombres, suplencias y servicio especializado se asignan con C3/operación antes de cerrar; el adjudicatario no conserva una clave oculta ni acceso permanente fuera del gobierno del CLIENTE.

#### B4.6 Rotación, versión y ciclo de vida

Cada clave, certificado y secreto tendrá propietario, propósito, ambiente, consumidores, fecha de creación/activación/retiro, regla de rotación y evidencia. La rotación ordinaria será automatizada y su período se fijará en la política criptográfica según tipo de material, capacidad del producto, riesgo y obligación aplicable; las Bases exigen rotación declarada, pero no autorizan inventar un mismo plazo para todo.

Se rota de inmediato ante exposición o sospecha, cambio relevante de custodios, vulnerabilidad/algoritmo obsoleto, clonación no autorizada o fallo de control. La nueva versión se distribuye con solapamiento: primero consumidores capaces de leer versión anterior y escribir nueva, luego migración/re-cifrado controlado y, finalmente, retiro cuando la historia y respaldos ya sean recuperables. Destruir una clave no puede anteceder al fin de retención o a una eliminación criptográfica expresamente aprobada y probada.

Los secretos se obtienen en ejecución y tienen alcance/vida mínimos; se prohíbe compartirlos entre DEV, QA, PREPROD, PROD y DR. B6 agregará escaneo y bloqueo del pipeline. Los certificados reutilizan alertas propuestas de B3.4; B4 añade custodia, recuperación y prueba de rotación, sin duplicar la política TLS.

#### B4.7 Operación normal, desconectada y recuperación

| Estado | Comportamiento exigido/propuesto | Evidencia futura |
|---|---|---|
| Normal | Gobierno común, claves por ambiente/propósito, identidades técnicas y registro de cada operación administrativa; servicios no reciben raíz | Inventario contra configuración; denegación de exportación/uso cruzado; auditoría completa |
| Corte exterior hasta 72 h | `EDGE-RUN`, identidad local y servicios de las cinco funciones conservan capacidad local protegida para cifrar/descifrar/firmar lo necesario; verificadores, cadena de confianza, tiempo y resolución local no dependen exclusivamente de nube | Simulacro 72 h con turnos, hechos, reefer, gate, movimientos y evidencia; sin claves vencidas, datos en claro ni bypass |
| Terminal de patio aislada hasta 8 h | CH-APP/CH-CAB usa almacén seguro y autorización offline B2.4; conserva solo material mínimo ligado a dispositivo/tarea y no una clave maestra | Pérdida/manipulación/reloj alterado, expiración, relevo y reconexión sin revelar datos ni reusar autorización |
| Reconexión | Sincronizar primero revocaciones/versiones y eventos de custodia; no sobrescribir una versión más nueva con estado antiguo; re-cifrar o rotar material expuesto durante contingencia | Conciliación ≤90 min para datos operacionales y registro separado del ciclo criptográfico; fallos se aíslan sin perder eventos |
| Falla del servicio de claves local | HA acorde a criticidad y degradación segura; no guardar todo en claro ni aceptar claves vencidas. Procedimiento de recuperación bajo doble control | Conmutación/restauración, servicio no autorizado denegado y continuidad medida por C1–C4 |
| Desastre/restauración | Recuperar dato y claves compatibles desde copias protegidas; validar integridad antes de abrir servicio; rotar material de emergencia tras uso | Restauración mensual representativa, prueba de copia inmutable y recuperación dirigida sin depender de una sola persona/sitio |

Las 72 h de enlace, RTO/RPO, autonomía eléctrica y DR son escenarios distintos. La capacidad local de claves no sustituye redundancia, UPS/generación ni sitio secundario de C1–C4. La copia fuera de sitio no queda bajo las mismas credenciales que producción; la copia inmutable debe resistir intento de borrado administrativo y seguir siendo descifrable durante su retención (`RNF-DIS-14`).

#### B4.8 ADR-009 propuesto, aporte físico y cierre del bloque

**Contexto y fuerza de decisión:** toda persistencia se cifra, ciertos campos requieren protección adicional y la operación crítica debe continuar 72 h sin enlace. La solución es híbrida, el equipo TI del CLIENTE tiene cinco personas y los productos/emplazamientos aún no están definidos.

**Alternativas evaluadas:**

- **A. KMS solo nube y caché de claves en local:** operación central simple, pero el corte, la renovación, la recuperación y los turnos nuevos quedan sujetos a material cacheado y pueden ampliar exposición.
- **B. Jerarquías totalmente independientes en nube y local:** máxima autonomía, pero duplica gobierno, dificulta intercambio/recuperación y eleva el riesgo de divergencia o claves huérfanas.
- **C. Gobierno y política comunes con capacidades criptográficas separadas por ámbito, raíz no exportable y servicio local protegido para la operación crítica:** conserva autonomía y límites de compromiso, a costa de versionar, reconciliar y operar recuperación entre ámbitos.

**Decisión propuesta seleccionada por el Frente 3:** alternativa C. Las alternativas A y B se conservan de forma breve para demostrar el análisis y permitir revisar la decisión si cambian las restricciones; no son opciones aún abiertas al mismo nivel. No se decide marca ni se afirma que requiera HSM dedicado; C1/C2 deben demostrar el tipo de KMS/HSM/vault, HA, compatibilidad, residencia/soporte, portabilidad, capacidad y operación. Las claves de un ámbito no se copian en claro al otro; se intercambian datos cifrados, material envuelto o verificadores según contrato y propósito. La autoridad de datos de A3/Subdocumento 5 no se modifica por dónde esté la clave.

**Consecuencias y riesgo residual:** mejora autonomía, separación y alcance de compromiso; agrega reconciliación de versiones, custodia local y pruebas de recuperación. Persisten riesgos de incompatibilidad con TOS/periféricos, pérdida del servicio local, error de custodia y catálogo incompleto. Se mitigan mediante adaptadores, HA, doble control, inventario, pruebas y `F3-DEP-002..004`; D2 debe formalizarlos.

| Aporte B4 | Capacidad para C1–C4/T-11 | Validación concreta |
|---|---|---|
| SEC-DATA-01/ENC-01/FIELD-01 | Cifrado de almacenes/objetos/volúmenes y servicio de cifrado de campo | 100 % de reposo cubierto; consulta directa no revela campos restringidos; catálogo final con Subdoc. 5 |
| SEC-KEY-01 | KMS/HSM/vault con límite criptográfico protegido, capacidad local y recuperación; consolidar productos cuando se seleccionen | Corte 72 h, HA, rotación, no exportación, carga/capacidad, residencia/compatibilidad y restauración |
| SEC-SECRET-01 | Gestión de secretos e identidades de carga por ambiente | Sin secretos embebidos; inyección/rotación y rechazo de versión retirada; B6 completa pipeline |
| SEC-BKP-01 | Protección de claves de respaldo y separación frente a borrado | Restauración mensual, copia inmutable resistente y dato descifrable durante retención |

**Pendientes para cerrar B4:** Subdocumento 5 entrega catálogo de campos, sensibilidad, propietario, retención y tratamiento de anonimización; A1/A2 confirman consumidores y formatos/eventos; A3 confirma autoridad local/nube; C1–C4 seleccionan y ubican capacidades, demuestran HA/DR, capacidad y filas T-11; CLIENTE asigna custodios, base de licitud y política/períodos; D2 revisa amenazas. `ADR-009` queda `PROPUESTO`, sin producto ni periodicidad aprobados; solo pasa a `APROBADO` tras las validaciones de integración. `SEC-PHYS-v0.1` incorpora ya requisitos de claves/cifrado, pero sigue parcial hasta B7.

### B5. Detección y respuesta — propuesta

**Estado: EN CURSO.** Este bloque define la capacidad y el modelo operativo; no selecciona SIEM, EDR, proveedor de SOC ni cantidad de licencias. Aplica los plazos obligatorios de FEP02 y separa tres cosas que deben colaborar sin confundirse: alarmas operativas del puerto, detecciones de ciberseguridad y atención/recuperación del servicio.

#### B5.1 Registro inalterable y continuidad de la evidencia

Cada componente relevante emitirá eventos con esquema común, tiempo confiable, ambiente, componente, actor o identidad técnica, organización/alcance cuando aplique, acción, recurso, resultado, severidad y un identificador de correlación. Se registra el uso administrativo, autenticación/autorización, cambios de configuración, acceso a datos `CONF/RES`, operaciones de claves/secretos, integraciones y sincronización, seguridad de endpoint, respaldo, borde y gateway. No se registran contraseñas, tokens, secretos, claves ni contenido sensible completo; la minimización sigue B4.

El flujo propuesto es: **fuente → colector local → canal cifrado y autenticado → repositorio central inalterable → SIEM/caso SOC**. Los productores no pueden borrar ni reescribir su propia evidencia. El repositorio debe permitir consulta en línea por al menos **12 meses** y conservar **24 meses adicionales** en archivo recuperable, con control de integridad, acceso segregado, retención protegida y eliminación gobernada al término aplicable.

Durante pérdida de enlace exterior, los colectores locales continúan recibiendo y protegiendo eventos. Su capacidad cubrirá al menos las 72 h exigidas más margen de reintento y sincronización calculado por C4; no se inventa aquí un volumen. Al reconectar, envían por secuencia e identificador, detectan faltantes, duplicados y alteraciones, preservan la hora original y dejan evidencia de conciliación. Tiempo y resolución necesarios para registrar localmente no dependen solo de nube. Si se agota el buffer, se alerta localmente y se priorizan eventos de seguridad/auditoría sin silenciar el hecho de descarte.

#### B5.2 Fuentes y cobertura híbrida

| Ámbito | Fuentes mínimas | Tratamiento propuesto durante corte |
|---|---|---|
| Borde y API | CDN/WAF/DDoS, gateway, autenticación, autorización, cuotas, validación de esquema y cambios de reglas | colector conserva eventos y métricas; el borde nube sigue visible al SOC si su servicio permanece disponible |
| Identidad y administración | IAM, MFA, PAM, elevaciones, sesiones grabadas, altas/bajas/revocaciones y cambios de política | identidad local registra decisiones offline y reenvía al volver; una alerta remota no sustituye el bloqueo/aviso local de B2 |
| Servicios, datos y criptografía | aplicaciones, DATA-*, KMS/HSM/vault tipo, respaldos, consultas privilegiadas y cambios de retención | eventos se conservan localmente cuando el consumidor opera en local; no incluyen dato o secreto completo |
| Integración y operación portuaria | `INT-HUB`, TOS/adaptadores, colas, reintentos, DLQ, periféricos, reefer, gate, movimientos y evidencia facturable | se mantienen alarmas operativas locales; el SIEM recibe copia/correlación, pero no asume autoridad TOS ni reemplaza HMI/operación |
| Nube, local y terreno | plano de control nube, servidores/cargas, endpoints gestionados, `EDGE-RUN`, estaciones y terminales compatibles | EDR conserva detección local y reenvía después; aislamiento automático solo donde no comprometa una función crítica sin procedimiento |
| Red, protección y sistemas conservados | firewalls, rutas administrativas, `EXT-ACC`, `EXT-VMS` y `EXT-GRU` según interfaces autorizadas | usar metadatos/eventos permitidos; no ingerir video general ni crear acceso de escritura donde la autoridad es externa |

##### B5.2.1 Política de admisión y tratamiento para dimensionamiento

Esta política define **qué entra al repositorio de seguridad y al SIEM**; no obliga a duplicar allí toda la telemetría operacional. Se conserva el evento suficiente para investigar, auditar y correlacionar, minimizando contenido sensible. C4 utiliza estas clases como entrada de la futura fila `T11-SEC-04`, identificador informado por Frente 2 y todavía no integrado en esta rama, y mide sus volúmenes reales; D1 no inventa EPS, GB ni licencias.

| Clase de señal | Regla de ingreso | Tratamiento y destino |
|---|---|---|
| Seguridad y auditoría obligatoria | 100 % de autenticaciones y su resultado, decisiones de autorización sensibles/denegadas, privilegios/PAM, acciones administrativas, cambios de configuración o política, accesos `CONF/RES`, operaciones de claves/secretos y cambios sobre evidencia/retención | No muestrear ni descartar. Repositorio inalterable; correlación SIEM cuando exista caso o indicador. Sin contraseña, token, secreto, clave ni contenido sensible completo |
| Detecciones y alertas | 100 % de alertas y acciones WAF/DDoS/bot, EDR, SIEM, integridad, segmentación y protección, incluido abrir, reconocer, actuar y cerrar | Conservar ciclo completo, severidad, regla, evidencia referenciada y resultado. Una alarma operacional entra como seguridad solo ante manipulación, acceso indebido o correlación |
| Integración y evidencia de negocio con efecto de seguridad | 100 % de fallos, reintentos agotados, DLQ, duplicados/replay, cambio de autoridad, conciliaciones anómalas y accesos privilegiados; éxitos solo cuando exista obligación de auditoría/no repudio | Registrar metadatos, actor/origen, contrato, secuencia, resultado y referencia de evidencia. No copiar cada payload de negocio por defecto |
| Telemetría operacional cruda | Lecturas reefer, posición, OCR/imágenes y video permanecen en el almacén del dominio y con su retención propia; el SIEM recibe brechas de frescura, umbrales, manipulación, cambios, metadatos y referencias/hash necesarios | No ingerir flujo completo, video ni imagen por defecto. Incluirlos solo si un requisito, caso de uso y dimensionamiento aprobados lo justifican |
| Diagnóstico de aplicación e infraestructura | Ingresan errores, advertencias, cambios de estado, autenticación y administración; salud ordinaria se conserva como métrica/agregado | `DEBUG` deshabilitado en operación normal; habilitación temporal aprobada, con vencimiento y filtrado de sensibles |
| Red, borde y endpoint | Ingresan denegaciones, amenazas, cambios de política/administración, alertas/acciones EDR, salud, inventario y manipulación; tráfico permitido usa métricas, flujos o muestra justificada | No conservar payload completo por defecto. El volumen del producto EDR se mide con el inventario y configuración candidatos |

La agregación o deduplicación solo se permite para ruido técnico idéntico y debe conservar **contador, primera/última hora, fuente, regla y correlación**. Nunca se muestrean ni descartan eventos de auditoría obligatoria, acciones privilegiadas o alertas críticas. Todo descarte técnico deja contador y motivo observables.

Para cada clase `i`, C4 levantará `EPS_i`, bytes medios por evento, peak/burst, fuentes, regla de reducción y separación local/central. El volumen bruto diario se estima como `EPS_i × bytes_i × 86.400`; la capacidad de 12 meses en línea y 24 adicionales de archivo aplica después factores **medidos** de indexación, réplica y compresión. El buffer local se dimensiona con el peak, el tamaño de evento y **72 h más margen de reintento/sincronización**, no solo con el promedio anual. El piso ya calculado por otro frente puede conservarse, pero no sustituye medir el término dominante definido aquí.

EDR cubre cargas de trabajo nube y on-premise y puestos administrados compatibles. Equipos de terreno, OT o legados que no acepten agente se registran explícitamente como excepción técnica y usan controles compensatorios: segmentación, monitoreo de red, endurecimiento, lista permitida, control de cambios e aislamiento operativo acordado. La ausencia de agente no puede esconder el activo ni declararse cobertura EDR ficticia.

#### B5.3 Casos de detección portuaria iniciales

| Caso | Señales correlacionadas | Respuesta inicial propuesta |
|---|---|---|
| Acceso cruzado o extracción masiva | organización/expediente, autorización denegada, volumen, exportación y consulta `CONF/RES` | bloquear o limitar sesión, preservar consulta y escalar al propietario del dato |
| Abuso privilegiado o acceso de desarrollo | PAM/elevación, horario, aprobación, grabación, cambio en producción y acceso fuera de bastión | revocar elevación si es seguro, preservar sesión y activar responsable de incidente |
| Reutilización offline o identidad revocada | versión de política, vigencia, dispositivo, reloj, repetición y aviso de baja | impedir nuevas acciones cuando corresponda, aislar credencial/dispositivo y reconciliar con B2 |
| Manipulación de evidencia o control | ausencia súbita de fuente, borrado/cambio de retención, agente deshabilitado, reloj alterado o regla SOC suprimida | alerta de alta prioridad por canal separado, proteger copia y restringir administración |
| Integración/TOS anómala | firma/identidad técnica, secuencia, duplicado, DLQ, reintentos, ruta no autorizada y cambio de adaptador | cuarentena técnica sin cambiar autoridad TOS; revisión conjunta seguridad–integración–operación |
| Alteración de operación reefer/gate/movimientos | cambio no aprobado de umbral, supresión de alarma, comandos incompatibles con rol/zona y patrón anómalo | mantener alarma operacional, impedir cambio no autorizado y correlacionar como posible incidente |
| Uso anómalo de claves o secretos | descifrado masivo, consumidor/ambiente incorrecto, exportación, política o custodia modificada | denegar operación, rotar/revocar según B4 y preservar trazas sin revelar material |
| Malware o manipulación de endpoint | EDR, conexión/red, cambio de binario/configuración y comportamiento lateral | contener según criticidad; en equipo operacional aplicar procedimiento que conserve seguridad física |
| Abuso de exposición pública | WAF/bots/DDoS, API, identidad, payload y tasa por actor/organización | reto, límite o bloqueo gradual; abrir caso y evitar afectar usuarios legítimos/accesibilidad |

El catálogo es inicial: D2 ajusta amenazas y severidades; A1/A2/A3 confirman componentes, eventos y significado operacional. Cada regla final tendrá propietario, fuente, lógica, umbral, severidad, acción permitida, dependencia de conectividad, tratamiento de falsos positivos, revisión y prueba. Una alarma reefer o de gate sigue siendo operativa; se vuelve señal de seguridad cuando hay evidencia de manipulación, acceso indebido o patrón correlacionado.

#### B5.4 SOC 24x7 y reparto operativo

FEP02 exige un SOC **24x7 propio o subcontratado**, con ubicación, dotación y procedimientos declarados. Como el CLIENTE dispone de un equipo TI de cinco personas, el diseño no le atribuye una guardia especializada continua sin capacidad demostrada. La propuesta es que el adjudicatario provea o subcontrate un **SOC gestionado 24x7**, mientras el CLIENTE conserva gobierno, recepción de comunicaciones, decisiones de negocio y coordinación con operación/protección.

| Función | Responsabilidad propuesta |
|---|---|
| SOC 24x7 | vigilar, validar alertas, abrir/priorizar casos, preservar evidencia, ejecutar acciones preautorizadas y escalar dentro de plazo |
| Responsable de incidente del adjudicatario | dirigir contención/recuperación, coordinar especialistas y mantener cronología e informes |
| TI/seguridad del CLIENTE | ser contraparte y autoridad institucional; aprobar acciones de impacto según procedimiento, recibir avisos e informes |
| Operación/propietario del proceso | decidir degradación/parada segura y validar recuperación de nave, gate, reefer, patio o facturación |
| Plataforma/integración/endpoint | ejecutar corrección técnica, recuperación y recolección forense bajo autorización |
| Legal/privacidad/comunicaciones | evaluar brecha y obligaciones externas; sus responsables y suplencias los confirma el CLIENTE |

Antes de cerrar deben declararse ubicación y residencia del servicio, niveles y dotación por turno, idioma, acceso remoto controlado, competencias, suplencias, herramientas, canales principal/alternativo, lista de contactos, RACI, SLA de triage/escalamiento, procedimientos por caso, transferencia de conocimiento, conservación/entrega de evidencia y salida del proveedor. Los plazos contractuales de comunicación no se reemplazan por el SLA del soporte.

#### B5.5 Incidentes, brechas y comunicaciones

El ciclo común es **detectar → validar/clasificar → contener → preservar evidencia → comunicar → erradicar/recuperar → causa raíz y mejora**. La clasificación considera confidencialidad, integridad, disponibilidad, seguridad física, personas/organizaciones afectadas, alcance operativo y obligación legal. La contención remota no se automatiza cuando pueda detener una función portuaria crítica sin una acción previamente aprobada; siempre debe existir un camino local y un contacto alternativo durante corte.

- Incidente crítico: comunicar al CLIENTE en **máximo 2 horas desde su detección** (`RT-11.18`), con alcance conocido, impacto, contención y siguiente actualización.
- Brecha de seguridad o datos: notificar al CLIENTE en **máximo 24 horas**, aunque el análisis no haya concluido; entregar informe preliminar y luego causa raíz dentro de **5 días hábiles** conforme `RT-11.19`.
- Para incidentes operacionales, `RNF-OPE-05` mide además el informe de causa raíz desde el cierre. El plan final registrará ambos relojes y aplicará el plazo correspondiente más exigente cuando coincidan, sin postergar el aviso inicial.

Cada caso conserva marcas de detección, validación, escalamiento, comunicación, decisión, acción y cierre; cadena de custodia; personas informadas; impacto; evidencia; causa; acciones correctivas y aceptación de riesgo. El help desk puede recibir la llamada y medir respuesta/restauración, pero no sustituye la clasificación, contención ni notificación de seguridad.

#### B5.6 Vulnerabilidades, pentest y simulación

El inventario de activos, versiones y responsables alimenta escaneo continuo en nube, on-premise, aplicaciones, imágenes y superficie externa; B6 completa controles de pipeline y dependencias. El plazo corre desde la **publicación o detección**, según corresponda al requisito: crítica **≤7 días corridos**, alta **≤15 días**, media **≤30 días**. Cada hallazgo registra activo/propietario, severidad y fuente, fecha inicial, exposición, corrección/compensación, evidencia, reprueba y cierre.

Una excepción requiere justificación, riesgo, compensación, propietario, aprobador y vencimiento; no borra el plazo contractual ni permite cerrar falsamente el hallazgo. Si no es viable remediar a tiempo, se escala antes del vencimiento para aislar, deshabilitar o sustituir la exposición y dejar el incumplimiento/riesgo explícito.

Se realizará pentest por un tercero independiente del adjudicatario al menos **una vez al año y antes de cada paso a producción**, con alcance autorizado, informe íntegro al CLIENTE, plan de remediación, plazos y reprueba. Se propone además incorporar la simulación anual de incidente con participación del CLIENTE indicada como deseable en `RT-11.21`; quedará comprometida solo si se acepta expresamente en la oferta/operación.

#### B5.7 Evidencias de diseño y pruebas futuras

| Evidencia/prueba | Criterio de aceptación propuesto |
|---|---|
| Inmutabilidad y retención | un productor/admin no altera ni borra; se consulta período en línea y se recupera muestra archivada con integridad |
| Corte y reenvío | 72 h sin enlace más margen dimensionado, sin pérdida silenciosa; orden, duplicados, hora original y faltantes quedan conciliados |
| Casos SIEM | cada señal inyectada produce alerta/caso esperado, evidencia correlacionada y acción autorizada; falsos positivos se registran |
| Cobertura EDR | 100 % del inventario clasificado como cubierto, excepción compensada o pendiente explícito; detección/contención no rompe seguridad operacional |
| Operación SOC | turnos/contactos/procedimientos demostrados; caso crítico comunica antes de 2 h y brecha antes de 24 h con cronología |
| Vulnerabilidades | tablero acredita antigüedad y cierre/reprueba dentro de 7/15/30 días o escalamiento explícito antes de vencer |
| Pentest/simulacro | independencia, alcance, informe completo, remediación/reprueba; si se acepta RT-11.21, acta anual con participación del CLIENTE y mejoras |

Son criterios verificables, no pruebas ya ejecutadas. C4 dimensiona ingestión, almacenamiento en línea/archivo, buffer, licencias y concurrencia; C1–C3 ubican colectores, consolas, canales, HA/DR y acceso de operación; D2 amplía escenarios y D3 audita cumplimiento.

#### B5.8 ADR-010 propuesto, aporte físico y cierre del bloque

**Contexto y fuerza de decisión:** se exige evidencia inalterable, SIEM portuario, EDR nube/on-premise, SOC 24x7 y continuidad local. Un SIEM visible solo desde nube deja al puerto sin triage central durante el corte; duplicar toda la operación local y nube excede razonablemente a TI=5 y aumenta divergencia.

**Alternativas evaluadas:**

- **A. SIEM/SOC central solo en nube:** menor operación local, pero crea punto ciego y retrasa acciones cuando se pierde el enlace.
- **B. plataformas y SOC independientes en nube y local:** máxima autonomía, pero duplica reglas, casos, personal, licencias y evidencia, con alto riesgo de desalineación.
- **C. detección híbrida federada:** colectores/buffer y reglas/acciones críticas mínimas locales, repositorio/SIEM central y SOC gestionado 24x7, con reconciliación posterior y escalamiento local.

**Decisión propuesta seleccionada por el Frente 3:** alternativa C. Cumple mejor la autonomía sin exigir un segundo SOC completo en la sala de servidores; a cambio requiere dimensionar buffer, definir qué reglas/acciones siguen locales, probar la reconciliación y contratar/operar cobertura 24x7. Las alternativas A/B permanecen resumidas como trazabilidad y condición de revisión. `ADR-010` queda `PROPUESTO`; el reparto operativo y su costo/viabilidad deben validarse con C1–C4 y el CLIENTE antes de aprobarlo.

| Aporte B5 | Capacidad para C1–C4/T-11 | Validación concreta |
|---|---|---|
| SEC-LOG-01 / SEC-SIEM-01 | plataforma central, almacenamiento 12+24 meses, colectores/buffer y licencias/ingesta | capacidad, HA/DR, residencia, integridad, corte 72 h, archivo y casos portuarios |
| SEC-END-01 | EDR nube/on-premise/endpoints y controles compensatorios para excepciones | inventario, compatibilidad, consola, operación local, aislamiento seguro y licencias |
| SEC-SOC-01 / SEC-IR-01 | servicio SOC 24x7 y gestión de incidentes/evidencia | ubicación, dotación, procedimientos, RACI, SLA, contactos, 2 h/24 h/5 días y salida del proveedor |
| SEC-VULN-01 / SEC-PENTEST-01 | plataforma/servicio de escaneo y pentest independiente | cobertura, 7/15/30 días, independencia, frecuencia, informe, reprueba y costos sin cifras inventadas |

**Pendientes para cerrar B5:** A1/A2/A3 confirman fuentes, eventos y acciones seguras; C1–C4 seleccionan/ubican/dimensionan plataformas, licencias, almacenamiento, red y servicio; CLIENTE valida responsables, contactos, residencia y viabilidad final de la propuesta; D2 formaliza amenazas/severidades y C3 los runbooks. La simulación anual `RT-11.21` es deseable y requiere aceptación explícita. `SEC-PHYS-v0.1` incorpora ya requisitos de detección/operación, pero sigue parcial hasta B7.

### B6. Desarrollo y operación seguros — propuesta

**Estado: EN CURSO.** B6 establece qué debe impedir una versión insegura y qué evidencia debe quedar. D1 define la política y los controles; C3 diseña y opera el pipeline, ambientes, despliegue y retorno. No se eligen productos ni se declara que SLSA 3+ o los controles OWASP estén ya implementados.

#### B6.1 Flujo gobernado desde el cambio hasta producción

Todo cambio de desarrollo o mantención evolutiva sigue una única cadena auditable:

**requerimiento/incidencia → cambio de código/configuración/IaC → revisión por pares → compilación y pruebas → controles de seguridad → artefacto y SBOM → aprobación/promoción → despliegue y verificación**.

La rama principal queda protegida, sin escritura directa, y todo cambio requiere revisión por otra persona autorizada. La evidencia vincula requerimiento o incidencia, solicitud de cambio, autor/revisor, pruebas, hallazgos, excepciones, artefacto, aprobación y despliegue (`RNF-MAN-01/02`). La misma regla aplica a correcciones y mantención evolutiva (`RNF-MAN-11`); una urgencia no crea una vía permanente sin controles.

Se separan funciones: quien desarrolla no aprueba por sí solo la excepción de seguridad ni obtiene acceso normal a producción. Con una dotación acotada, la separación puede apoyarse en revisión por pares, permisos de herramienta y aprobaciones del CLIENTE/servicio especializado; no exige inventar una persona exclusiva por función, pero sí evita autoaprobar el propio cambio.

#### B6.2 Puertas automáticas de seguridad

| Control del flujo | Qué detecta/demuestra | Momento y efecto mínimo |
|---|---|---|
| Compilación y pruebas unitarias | código construible y comportamiento básico | cada cambio integrable; si no ejecuta o falla, no se promueve |
| Cobertura automatizada | alcance probado de lógica de negocio | medir en CI; bloquear bajo **70 %** conforme `RNF-MAN-06` |
| SAST | debilidades en código sin ejecutar la aplicación | en cambio/merge; hallazgo crítico bloquea |
| SCA | vulnerabilidades y licencias de bibliotecas/componentes | en cambio y nuevamente antes de liberar; dependencia no aprobada bloquea |
| Escaneo de secretos | credenciales, tokens o claves expuestos | repositorio, historial relevante, artefactos y configuración; hallazgo obliga a bloquear y rotar, no solo borrar texto |
| Escaneo de imágenes | paquetes, vulnerabilidades y configuración base de contenedores | antes de publicar/promover; imagen crítica o no aprobada bloquea |
| DAST | fallas observables sobre la aplicación/API en ejecución | ambiente efímero o preproducción; resultado crítico bloquea producción |

FEP02 `RT-11.22` obliga a incorporar SAST, SCA, DAST y escaneo de imágenes y a bloquear hallazgos críticos. `RNF-MAN-03` agrega compilación, pruebas, secretos e imágenes y exige que el despliegue se bloquee si alguno de sus controles falla. Por ello: **si una etapa obligatoria no se ejecuta, termina con error o detecta un crítico, el flujo se detiene**. Hallazgos no críticos siguen la política de severidad y los plazos 7/15/30 de B5.6; una excepción documentada no puede convertir un crítico en aprobado silenciosamente.

Las reglas y versiones de cada herramienta también quedan controladas y auditadas. Un falso positivo requiere evidencia, aprobador distinto del autor, alcance y vencimiento; desactivar el control completo para liberar una versión no es una excepción válida.

#### B6.3 Artefacto único, SBOM, firma y procedencia

La versión se **construye una vez** en un entorno controlado y el mismo artefacto inmutable se promueve entre QA, preproducción y producción. No se recompila desde código para producción, porque se perdería la equivalencia con lo probado. El registro conserva digest/identificador, versión, ambiente de construcción, pruebas, aprobaciones, firma y estado de retiro.

Cada versión liberada genera y entrega al CLIENTE una **SBOM** en CycloneDX o SPDX (`RT-11.23`). Debe identificar componentes y versiones suficientes para cruzar una nueva vulnerabilidad con las versiones desplegadas; no es una lista manual independiente del artefacto.

Los artefactos se firman y su procedencia se verifica antes de desplegar, conforme **SLSA nivel 3 o superior** (`RT-11.24`). La procedencia enlaza fuente, proceso de construcción, dependencias y resultado; la firma prueba integridad/autenticidad, no que el software esté libre de fallas. Las claves de firma siguen B4: propósito exclusivo, no exportables cuando corresponda, rotación, custodios separados y registro de uso. Producción rechaza artefactos sin firma válida, procedencia aceptada o aprobación vigente.

#### B6.4 Dependencias y cadena de suministro

Antes de incorporar o actualizar una dependencia de terceros se registra: componente/versión, finalidad, propietario interno, origen, licencia y compatibilidad, soporte/mantención activa, vulnerabilidades conocidas, integridad, alternativa o plan de sustitución y decisión de aprobación (`RT-11.26`). La descarga en CI proviene de repositorios permitidos y se fija por versión/digest; no se obtiene código mutable directamente de Internet durante producción.

Una dependencia con vulnerabilidad conocida no se aprueba como conforme. Si no existe sustituto inmediato, debe bloquearse la liberación o escalarse como riesgo/incumplimiento con aislamiento, plan y vencimiento; el registro de excepción no elimina la obligación. Una nueva vulnerabilidad posterior a la liberación se localiza mediante SBOM y entra al programa 7/15/30 de B5.6.

También se controlan imágenes base, acciones/plugins del pipeline, herramientas de construcción y artefactos de infraestructura. El proveedor o producto no hereda confianza por reputación: origen, versión, acceso y actualización se verifican explícitamente.

#### B6.5 Separación de ambientes y datos no productivos

DEV, QA, PREPROD, PROD y DR usan cuentas/proyectos, identidades técnicas, secretos, certificados, datos y permisos diferenciados. No producción no tiene ruta administrativa libre hacia producción ni reutiliza sus credenciales. La configuración se promueve de forma versionada y los valores sensibles se inyectan desde el servicio de secretos de B4.

La fuente preferida para pruebas es dato **sintético**. Está prohibido copiar datos productivos reales a no producción salvo anonimización o seudonimización verificable autorizada (`RT-11.25`). La solicitud debe registrar finalidad, categorías/campos, propietario, base/autorización, técnica, destino, acceso, retención y eliminación. Se verifica que una consulta o cruce razonable no revele personas, tarifas, volúmenes, contenido/ruta u otra categoría `RES`.

La seudonimización puede permitir reidentificación bajo una clave o tabla separada; por eso ese material se custodia fuera del ambiente y el conjunto conserva controles equivalentes mientras sea reversible. La anonimización pretende impedir reidentificación razonable. Subdocumento 5 define campos y reglas; B6 controla la provisión, evidencia y eliminación sin declarar anonimizado algo solo por quitar nombres visibles.

#### B6.6 Producción y acceso excepcional

El camino normal a producción es el pipeline automatizado y reproducible de C3, usando una identidad técnica acotada y el artefacto aprobado. Los desarrolladores no tienen acceso interactivo directo permanente (`RT-11.27`). Observabilidad se consulta mediante vistas de solo lectura y datos minimizados; soporte usa los canales y roles de B2/B3.

Una excepción exige incidente/cambio asociado, motivo, alcance, ambiente, aprobador, duración breve, MFA y elevación PAM, sesión grabada, comandos/acciones auditados, supervisión cuando corresponda y revocación automática al vencer. La sesión excepcional sirve para diagnóstico o acción autorizada, no para mantener cambios invisibles: toda corrección durable vuelve al repositorio, controles y despliegue reproducible. El acceso y su evidencia alimentan B5; ningún proveedor conserva una cuenta oculta o compartida.

Despliegue y retorno siguen `RNF-MAN-04/05`: automatización, reproducibilidad, reversión y estrategia azul-verde, canario o progresiva demostrada en preproducción. D1 exige verificación de firma, permisos y evidencia; C3 decide la mecánica compatible con continuidad y operación portuaria.

#### B6.7 Gobierno, SAMM y evidencias futuras

Se aplicará OWASP ASVS 4.0 nivel 2 mínimo, Top 10 y API Security Top 10 a los controles y pruebas pertinentes. El proceso se evaluará con **OWASP SAMM**, con línea base inicial, brechas, responsables, plan priorizado y reevaluación al menos anual. Aunque `RT-11.28` es deseable y admite equivalente en FEP02, FEP01 Art. 4.3 exige específicamente OWASP SAMM para el proceso; se conserva la fuente más estricta y no se omite.

| Evidencia/prueba | Criterio de aceptación propuesto |
|---|---|
| Repositorio y trazabilidad | rama principal protegida; muestra enlaza requerimiento, revisión, pruebas, artefacto y despliegue |
| Bloqueos | fallo de etapa obligatoria o hallazgo crítico impide promover; no puede omitirse el control sin evidencia/aprobación/vencimiento |
| Cobertura | lógica de negocio ≥70 % y reporte generado por CI |
| SBOM | CycloneDX/SPDX por versión liberada, correspondiente al artefacto y entregada al CLIENTE |
| Firma/procedencia | producción rechaza artefacto alterado, sin firma o procedencia no válida; evidencia SLSA 3+ demostrada |
| Dependencias | 100 % con licencia, mantención, vulnerabilidades, origen y aprobación/rechazo registrados |
| Datos de prueba | origen y tratamiento verificados; muestra directa/cruzada no revela categorías protegidas; eliminación demostrada |
| Acceso a producción | acceso directo normal denegado; excepción temporal aprobada, grabada, revocada y trazada a cambio/incidente |
| SAMM | evaluación inicial, plan de mejora y reevaluación anual conservados |

Estas son pruebas futuras. C3 implementa pipeline, repositorios, ambientes, despliegue y retorno; C4 dimensiona ejecutores, almacenamiento, licencias y concurrencia; D2 modela amenazas de cadena de suministro y D3 audita la evidencia.

#### B6.8 Aporte físico y candidatos T-11

| Capacidad | Componente/licencia/servicio candidato | Ubicación/restricción | Validación antes de seleccionar |
|---|---|---|---|
| SEC-PIPE-01 | plataforma CI/CD y licencias/servicios SAST, SCA, DAST, secretos e imágenes | servicio de ingeniería separado de producción; ejecutores controlados nube/local según C3 | compatibilidad tecnológica, reglas, HA, tiempos/capacidad, soporte, integración y evidencia exportable |
| SEC-SUPPLY-01 / SEC-ART-01 | registro de artefactos, generación SBOM, firma/procedencia y repositorio permitido | acceso restringido; producción solo lectura/promoción; claves bajo SEC-KEY-01 | inmutabilidad, digest/firma, SLSA 3+, retención, recuperación, portabilidad y costo/licencias |
| SEC-NPDATA-01 | generador sintético o servicio/proceso de anonimización/seudonimización verificable | ambiente no productivo segregado; material reversible fuera del ambiente | cobertura de campos Subdoc. 5, eficacia, capacidad, eliminación y responsabilidades |
| SEC-PROD-01 | automatización de despliegue, PAM y grabación ya candidatos en B2/C3 | canal administrativo segregado; sin acceso directo normal | integración con IAM, revocación, grabación, trazabilidad, retorno y operación con TI=5 |

No se deriva hardware obligatorio para la sala solo por aplicar DevSecOps: muchas capacidades pueden ser servicios o herramientas alojadas. C1–C4 determinan si algún ejecutor, repositorio o proxy debe quedar local por conectividad, residencia, desempeño o continuidad. La tabla entrega capacidades para T-11, no marcas, cantidades ni precios.

#### B6.9 Glosario breve y cierre del bloque

| Término | En simple |
|---|---|
| ADR | Registro de una decisión de arquitectura: problema, opciones, elección y consecuencias. |
| On-premise / local | Equipos y servicios instalados en dependencias o infraestructura controlada por el CLIENTE. |
| Edge / borde local | Capacidad cercana a la operación o terreno que puede seguir funcionando con enlace exterior degradado. |
| Zero Trust | Cada acceso se verifica explícitamente; estar dentro de la red no entrega confianza automática. |
| IAM / MFA / PAM | Gestión de identidades; segundo factor; y control/grabación de accesos privilegiados, respectivamente. |
| KMS / HSM / vault | Servicios o dispositivos para proteger claves criptográficas y secretos. |
| SIEM / EDR / SOC | Correlación de eventos; detección en equipos/cargas; y equipo que monitorea/responde. |
| CI/CD | Flujo automatizado para integrar, probar, empaquetar y desplegar cambios. |
| DevSecOps | Integrar seguridad al flujo de desarrollo y operación, no revisarla solo al final. |
| SAST | Revisa el código sin ejecutar la aplicación. |
| SCA | Revisa bibliotecas/dependencias, vulnerabilidades y licencias. |
| DAST | Prueba desde fuera una aplicación que está ejecutándose. |
| SBOM | Inventario de los componentes exactos incluidos en una versión de software. |
| Artefacto | Paquete desplegable producido por el pipeline: imagen, binario o paquete versionado. |
| Firma y procedencia | Evidencia de quién/qué proceso creó el artefacto y de que no fue alterado. |
| SLSA | Marco para proteger la cadena de construcción y demostrar procedencia; aquí se exige nivel 3 o superior. |
| T-11 | Tabla de la oferta donde se consolidarán productos, licencias y servicios, sin inventarlos en D1. |

**Decisiones de B6:** puertas automáticas y bloqueantes; construcción única y promoción del mismo artefacto; SBOM/firma/procedencia por versión; dato sintético por defecto; producción sin acceso interactivo directo de desarrollo. Son propuestas de diseño fundamentadas en requisitos, no un nuevo ADR ni selección de producto.

**Pendientes para cerrar B6:** C3 define herramientas, pipeline, ambientes, estrategia de despliegue/retorno y responsables; C4 dimensiona ejecutores, almacenamiento y licencias; Subdocumento 5 valida campos/técnicas de datos; CLIENTE confirma aprobadores y custodia de excepciones; D2/D3 revisan amenazas y evidencia. Próximo bloque: **B7, cobertura y paquete temprano**. `SEC-PHYS-v0.1` tiene ya capacidades de B1–B6, pero B7 debe auditar y consolidar antes de intercambiarlo como paquete.

### B7. Auditoría de cobertura y paquete temprano

**Estado: AUDITORÍA INTERMEDIA EJECUTADA.** B7 verifica completitud documental y prepara el intercambio; no prueba la implementación ni reemplaza la auditoría final D3. Se contrastaron el contrato de D1, B1–B6, TRZ_D1, Maestro, plan de entregables, matriz global, registro ADR y el estado visible de A1–A3/C1–C4/D2 al 2026-09-05.

#### B7.1 Método y regla de resultado

Se revisó cada obligación en cinco recorridos: **fuente → decisión/control → componente o servicio candidato → evidencia futura → estado/dependencia**. Además se comprobaron consistencia de nombres/estados, cobertura de FEP02 capítulos 11/12, tratamiento de estándares, ausencia de montos, separación entre propuesta y cumplimiento, y riesgo de duplicar filas T-11.

Estados usados:

- **Corregido:** la brecha documental se resolvió dentro de D1/TRZ.
- **Conforme a nivel de diseño:** existe propuesta trazable, pero no configuración ni prueba ejecutada.
- **Abierto:** depende de información, decisión o evidencia fuera de B7 y bloquea el cierre, no el intercambio de v0.1.

#### B7.2 Hallazgos y correcciones

| ID | Severidad | Hallazgo | Acción B7 | Resultado |
|---|---|---|---|---|
| `B7-F01` | Media | RT-11.01/07/11/12/13 y TRZ-D1-001/002/003/006 seguían `PENDIENTE` aunque B1–B3 ya contienen diseño | enlazar secciones/controles y llevarlos a `EN CURSO`, sin afirmar prueba | CORREGIDO |
| `B7-F02` | Alta | RT-11.05/06 y CIS estaban citados, pero faltaban controles concretos de gobierno, responsabilidad nube y hardening | agregar SEC-GOV-01, SEC-CLOUD-01 y SEC-HARD-01 con implementación/evidencia mínima | CORREGIDO A NIVEL DE DISEÑO |
| `B7-F03` | Alta | `SEC-PHYS-v0.1` no mostraba todas las capacidades físicas/servicios de B1–B6 y todas sus filas decían simplemente “sí”, con riesgo de doble conteo T-11 | consolidar 17 grupos y clasificar fila propia, agrupada, incluida o condicional | CORREGIDO; LISTO PARA INTERCAMBIO |
| `B7-F04` | Alta | amenazas/riesgo residual figuran pendientes en todos los controles | conservar RT-11.02 y la validación de amenazas abiertos hasta D2 | ABIERTO — BLOQUEA CIERRE |
| `B7-F05` | Alta | A1–A3 y C1–C4 visibles siguen en estructura/plantilla, sin catálogos, contratos, nodos, productos ni cantidades utilizables para validar D1 | mantener F3-DEP-001..003; no inventar correspondencias | ABIERTO — BLOQUEA CIERRE, NO v0.1 |
| `B7-F06` | Alta | faltan catálogo campo→propietario→sensibilidad→retención y responsables/custodios nominales | mantener F3-DEP-004 y pendientes de CLIENTE/Subdocumento 5 | ABIERTO — BLOQUEA CIERRE |
| `B7-F07` | Media | ADR-009/010 tenían alternativas y consecuencias, pero su comparación cualitativa estaba dispersa | consolidar criterios/condiciones en B7.5; mantener ambos `PROPUESTO` | CORREGIDO A NIVEL DE PROPUESTA |
| `B7-F08` | Alta | ADR-008 recomienda C, pero revocación aislada, nombradas y directorio/federación siguen abiertos | promover solo a `PROPUESTO` como línea base condicionada; mantener `F3-ESC-001/002` y prohibir su aprobación hasta resolverlos | ABIERTO — APROBACIÓN PENDIENTE |
| `B7-F09` | Media | faltan vista/diagramas finales y correspondencia con nodos físicos | reservarlos para B8 después del cruce; no dibujar una topología ficticia | ABIERTO — BLOQUEA CIERRE |
| `B7-F10` | Crítica | riesgo de confundir diseño con cumplimiento | búsqueda y lectura confirman que evidencias están calificadas como futuras/propuestas y no hay controles `APROBADO` | CONFORME |
| `B7-F11` | Alta | referencias RT-11.18/19 están intercambiadas en RNF-SEG-07/11 de Célula 2 | conservar plazos sustantivos y referencia oficial correcta en TRZ_D1 §4; no editar Célula 2 | CONTROLADO; CORRECCIÓN EXTERNA PENDIENTE |
| `B7-F12` | Crítica | T-11 prohíbe precios y exige cantidades justificadas | no se encontraron montos/precios en el paquete; cantidades permanecen a C4 | CONFORME PARA INTERCAMBIO |
| `B7-F13` | Media | la matriz global mantenía filas D1 en `PENDIENTE` aunque ya existía diseño trazable | actualizar solo filas con evidencia D1 a `EN CURSO`, conservando sus pendientes y sin mover obligaciones de otros frentes | CORREGIDO |

#### B7.3 Controles transversales explicitados

**SEC-GOV-01 — gobierno y aplicabilidad.** Cada control se cruzará con ISO/IEC 27001/27002 y, cuando corresponda, con las funciones Govern, Identify, Protect, Detect, Respond y Recover de NIST CSF 2.0. La fila debe indicar aplicabilidad, implementación concreta, propietario, evidencia, excepción, revisión y relación con riesgo. La tabla de D1 inicia esa estructura; D3 completa el mapeo normativo y verifica que citar una norma no sustituya la evidencia ni una certificación institucional.

**SEC-CLOUD-01 — responsabilidad y privacidad en nube.** Por cada servicio nube se registrarán proveedor/servicio/región, dato y clasificación, titularidad y base aplicable, identidades, cifrado/custodia, registro, respaldo, disponibilidad, incidentes, subencargados, residencia/transferencia, eliminación, portabilidad/salida y evidencia. Cada tarea se asigna al proveedor, adjudicatario o CLIENTE; “lo cubre la nube” no es una respuesta válida. Así se materializan ISO/IEC 27017/27018 sin asumir un proveedor.

**SEC-HARD-01 — endurecimiento por producto.** Nube, sistema operativo, base, contenedor, endpoint, dispositivo de red y edge tendrán una línea base CIS correspondiente al producto/versión o guía equivalente justificada cuando no exista benchmark. Toda desviación registra necesidad, riesgo, compensación, aprobador, vencimiento y reprueba. C2/C3 aplican la configuración; D1/D2 evalúan control y riesgo.

#### B7.4 Resultado de cobertura

| Universo auditado | Resultado B7 | Interpretación correcta |
|---|---|---|
| 11 materias del trabajo requerido de D1 | **11/11 con diseño o control enlazado** | cobertura documental, no cierre ni prueba |
| FEP02 capítulo 11, RT-11.01..28 | **28/28 `EN CURSO`** | RT-11.02 tiene modelo provisional D2; falta refinar por componente/interfaz real en B6/B7. Ninguna fila está aprobada |
| FEP02 capítulo 12, RT-12.01..13 | **13/13 `EN CURSO`** | productos, parámetros, directorio, offline y pruebas siguen pendientes |
| Controles SEC-* | **31 controles identificados**, agrupados en 17 entradas de `SEC-PHYS-v0.1` | no equivalen a 31 compras ni a 17 filas finales T-11 |
| Productos, cantidades y nodos | **0 seleccionados/aprobados** | decisión correcta mientras C1–C4 permanezcan sin desarrollo verificable |
| Evidencias ejecutadas | **0 declaradas** | D1 mantiene criterios de prueba; implementación corresponde a etapas posteriores |

La cobertura cuantitativa no convierte D1 en “casi aprobado”: demuestra que el Frente 3 ya formuló qué debe resolverse. Las brechas abiertas son de amenaza, integración, viabilidad física, datos, responsables, productos, capacidad y prueba.

#### B7.5 Auditoría de ADR-008/009/010

| ADR | Restricciones excluyentes | Criterios de peso alto | Resultado actual | Condición de revisión/aprobación |
|---|---|---|---|---|
| ADR-008 — identidad | continuidad 72 h/8 h, SSO/MFA/PAM, revocación/baja y terminal/eventual | consistencia de autorización, TI=5, directorio/legados y recuperación | alternativa C `PROPUESTO` como línea base condicionada | resolver F3-ESC-001/002, nombradas durante corte, producto, usabilidad y capacidad antes de aprobar |
| ADR-009 — criptografía | todo reposo cifrado, campo sensible y operación local sin clave solo nube | límite de compromiso, separación de custodia, recuperabilidad, compatibilidad y operación TI=5 | alternativa C `PROPUESTO` | demostrar KMS/HSM/vault, HA, rotación, recuperación, custodios y compatibilidad TOS/periféricos |
| ADR-010 — detección/SOC | retención 12+24, EDR híbrido, SOC 24x7 y continuidad local | ausencia de puntos ciegos, respuesta segura, carga TI=5, reconciliación, residencia y costo operativo | alternativa C `PROPUESTO` | dimensionar buffer/ingesta, reglas locales, plataforma, dotación/RACI, proveedor, SLA y pruebas |

Para los tres, cumplimiento obligatorio y seguridad prevalecen sobre simplicidad/costo; después se ponderan operabilidad con TI=5, compatibilidad/portabilidad y esfuerzo. Esta ponderación es cualitativa porque aún no existen productos/costos comparables. A/B se conservan como evidencia y condición de revisión, no como indecisión equivalente.

#### B7.6 Disposición hacia Física y T-11

La tabla `SEC-PHYS-v0.1` al inicio es el paquete oficial del Frente 3 para intercambio. C4 debe asignar ID T-11 solo cuando exista un producto, plataforma, licencia, servicio o hardware efectivamente ofertado. Capacidades nativas o incluidas se referencian desde la fila principal; no se duplican por cada control lógico. Esta regla queda como `F3-DEC-005`.

El paquete permite que C1–C4 comiencen ubicación, compatibilidad, dimensionamiento y agrupación. Aún no permite completar las cinco columnas finales: faltan producto/servicio, lugar confirmado y cantidad justificada. No se modificó `90_Consolidado/01_T11_TRABAJO_TRAZABLE.md` porque C4 es su propietario y todavía no se ha realizado el intercambio acordado.

#### B7.7 Brechas de salida y decisión de avance

| Brecha | Productor/decisor | Qué puede enviarse ahora | Qué sigue prohibido afirmar |
|---|---|---|---|
| actores/componentes/contratos/autoridad | A1/A2/A3 | controles, zonas, roles y condiciones propuestas | correspondencia definitiva o flujo TOS validado |
| nodos, red, sala, productos y capacidad | C1–C4 | 17 grupos SEC-PHYS y tratamiento T-11 | ubicación, marca, licencia o cantidad final |
| amenazas y riesgo residual | D2 | fronteras, escenarios y controles candidatos | cobertura STRIDE completa o riesgo aceptado |
| datos/campos y privacidad | Subdocumento 5/CLIENTE | taxonomía y mínimos de protección | 100 % de campos clasificados o licitud aprobada |
| directorio, revocación aislada y nombradas | CLIENTE/A1–A3 | ADR-008 y fallback conservador | revocación inmediata demostrada sin canal ni identidad final aprobada |
| diagramas y narrativa final | B8/D3 | contenido técnico B1–B7 | D1 listo para aprobación o integración final |

**Conclusión de auditoría:** el avance es consistente y utilizable como **paquete técnico v0.1 interno**. No se detectó una contradicción crítica entre B1–B6 ni un requisito del capítulo 11/12 perdido silenciosamente. D1 **no puede cerrarse**: la principal brecha interna es D2/RT-11.02 y las dependencias F3-DEP-001..004 permanecen sin insumos desarrollados.

#### B7.8 Glosario breve y punto de continuación

| Término | En simple |
|---|---|
| Hallazgo | Diferencia entre lo requerido y lo que el documento o solución demuestra. |
| Evidencia | Registro verificable que permite comprobar una afirmación; una intención escrita no basta. |
| Línea base / baseline | Configuración o versión aprobada contra la que se comparan cambios y desviaciones. |
| Hardening | Quitar o restringir configuraciones innecesarias/inseguras de un producto. |
| Responsabilidad compartida | Reparto explícito de tareas entre proveedor nube, adjudicatario y CLIENTE. |
| Control compensatorio | Medida alternativa que reduce un riesgo cuando el control principal no es técnicamente viable. |
| RACI | Tabla que distingue quién ejecuta, aprueba, es consultado y debe ser informado. |
| Puerta de integración | Momento de control donde se revisa si un paquete puede pasar a la siguiente fase. |

**Retomar en B8 solo después de decidir el intercambio/commit:** incorporar aportes reales de los otros frentes, resolver diferencias, producir diagramas y sintetizar el contenido en formato de informe. B7 queda guardado localmente; no se ha hecho commit, push ni transferencia al T-11 central.

### B7-R. Reapertura de integración documental D1–D2

**Fecha: 2026-09-06. Estado: COMPLETADO COMO DISEÑO; no aprobado.** Este corte sustituye las premisas de B7 que decían que A1–A3, C1–C4 y D2 no estaban desarrollados. Conserva B7 como historial, cruza las entradas reales y mantiene B8 exclusivamente para la representación visual y el cierre posterior a la revisión conjunta.

#### B7-R.1 Entradas recibidas y efecto

| Entrada | Evidencia recibida | Efecto en D1 | Límite que permanece |
|---|---|---|---|
| A1 | 16 actores, 24 componentes, criticidad y continuidad | valida el universo de la matriz de identidad y los componentes protegidos | `ACT-TI` conserva la brecha de consola administrativa; roles/permisos no están aprobados |
| A2/A3 | contratos lógicos, autoridad TOS, degradación y respaldo manual | valida tipos de flujo, continuidad y acumulación/reconciliación | contratos/protocolos efectivos y aprobadores siguen externos |
| C1/C2/C3/C4 | 20 nodos `PHY-*`, una ubicación funcional `LOC-INSP-01`, zonas, emplazamiento de 17 grupos, tecnologías de referencia y candidatos T-11 | reemplaza `POR DEFINIR` por correspondencia documental; confirma gateway, IAM, claves, logs y evidencia locales | site survey, producto final, compatibilidad, cantidades contractuales y pruebas |
| D2 B7 + MA-3/MA-4 | 73 amenazas, 26 SPOF, 11 ADR revisados y regla de actualización | permite cerrar la relación control↔amenaza y cubrir `RT-11.02` documentalmente | corte histórico MA-4: 10 propuestos y `ADR-011` candidato; estado vigente tras MA-5: 11 propuestos y 0 aprobados |
| Subdocumento 5 | catálogo de campos no disponible | no cambia la taxonomía provisional `PUB/INT/CONF/RES` | campo→propietario→sensibilidad→retención→licitud continúa abierto |

#### B7-R.2 Cruce bidireccional control–amenaza

D2 B7.8 registra el detalle de los siete controles de gobierno/aseguramiento que no aparecían dentro de las filas técnicas de amenazas. El resultado conjunto es:

| Comprobación | Resultado | Estado |
|---|---|---|
| controles D1 invocados o asociados a amenaza D2 | 31/31 | CONFORME DOCUMENTAL |
| controles citados por D2 con desarrollo en D1 | 24/24 citados directamente; 0 inexistentes | CONFORME |
| controles de gobierno/aseguramiento asociados en el corte | `SEC-GOV/CLOUD/IR/VULN/PENTEST/SDLC/SAMM-01` → amenazas existentes | CONFORME; no crea amenazas duplicadas |
| valoración o aceptación modificada por el cruce | ninguna | CONFORME |

Relaciones nuevas relevantes: `SEC-CLOUD-01` gobierna `THR-049/060/072/073`; `SEC-IR-01`, `THR-038/047/062/070`; y los controles de vulnerabilidad, pentest, SDLC y SAMM verifican `THR-023/030/034/043/050/053/062/065` según su alcance. La matriz principal conserva su corte histórico; esta tabla es la actualización vigente.

#### B7-R.3 Emplazamiento y tratamiento T-11 de `SEC-PHYS-v0.1`

| Grupo | Emplazamiento confirmado por C1 | Tratamiento C4 | Estado de integración |
|---|---|---|---|
| borde y API | `PHY-CLD-01/02` + perfil local de API en `PHY-OPS-01` | `T11-SEC-01`/runtime incluido | INCORPORADO; producto/capacidad final pendientes, sin duplicar compra local |
| IAM, PAM y producción | `PHY-CLD-03` + capacidad local `PHY-OPS-01` | `T11-SEC-02` | INCORPORADO; `ADR-008` y directorio/revocación condicionan cierre |
| red, exposición y sincronización | `PHY-OPS-04` + controles cloud/enlace | `T11-C2-03/04`, `T11-C3-01`, `T11-C2-17` | INCLUIDO; site survey e independencia por probar |
| datos y cifrado | `PHY-CLD-05..08` + `PHY-OPS-02` | `T11-C2-17` y `T11-C2-02` | INCLUIDO; catálogo de campos pendiente |
| claves y secretos | gestión cloud + capacidad local protegida `PHY-OPS-01` | `T11-SEC-03` | INCORPORADO; custodios/producto/prueba pendientes |
| respaldo | `PHY-CLD-10` + `PHY-OPS-05` | condición de `T11-C2-12/18` | INCLUIDO SIN DUPLICAR; distinguir `SPOF-13` de `SPOF-22` |
| logging y SIEM | `PHY-CLD-09` + colector/buffer `PHY-OPS-01` | ancla `T11-SEC-04` resuelta sobre `T11-C2-19` | INCORPORADO SIN DOBLE CONTEO; ingesta dominante por medir |
| EDR | `PHY-OPS-01`, `PHY-CLD-03`, `PHY-OPS-06` compatibles | `T11-SEC-05` | INCORPORADO; excluye terreno sin agente compatible |
| SOC e incidentes | servicio, sin nodo | `T11-SEC-06` | INCORPORADO; no se asigna a TI=5 |
| vulnerabilidades y pentest | servicio, sin nodo | `T11-SEC-07` | INCORPORADO; alcance/tercero/pruebas pendientes |
| SDLC, pipeline, suministro y datos no productivos | DEV/QA/PREPROD fuera de operación | plataforma CI/CD o proceso | INCLUIDO/CONDICIONAL; herramientas y ejecución pendientes |
| gobierno, nube, hardening y SAMM | transversal, sin nodo propio | implementación/servicios | INCLUIDO; evidencia por producto/servicio pendiente |

Los 17/17 grupos quedan ubicados o justificados como servicio/proceso. C4 materializa seis filas propias `T11-SEC-01..03/05..07`, absorbe `T11-SEC-04` en `T11-C2-19` y referencia los diez restantes desde filas existentes o procesos. Se conserva `F3-DEC-005`: control no equivale a compra. D1 no modifica cantidades ni el formulario T-11.

#### B7-R.4 Identidad y continuidad

| Materia | Resultado del cruce | Estado |
|---|---|---|
| 16 actores A1 | todos pertenecen al universo D1; no se crea catálogo paralelo | CRUZADO |
| `ACT-TI` | administración funcional como perfil autenticado de `CH-PORTAL`; administración técnica por `Z-MGMT`/PAM desde `PHY-OPS-06` | RESUELTO DOCUMENTALMENTE; no crea un cuarto canal ni una fila T-11 nueva |
| entrada API durante 72 h | perfil local restringido de `GW-API` en `PHY-OPS-01`; mismas políticas/contratos vigentes, alcance solo crítico | COHERENTE; debe probarse de punta a punta y sigue `SPOF-23` POR ACEPTAR |
| IAM durante 72 h | C1 ubica `SRV-IAM` en `PHY-CLD-03` con caché/capacidad local en `PHY-OPS-01` | COHERENTE CON `ADR-008`, condicionado a producto y prueba |
| claves/secretos durante 72 h | C1/C2 exigen material local protegido en `PHY-OPS-01` | COHERENTE CON `ADR-009`, custodios y recuperación pendientes |
| logs/evidencia durante 72 h | `PHY-OPS-01` conserva colector, buffer y sello local; `PHY-CLD-09` centraliza al reconectar | COHERENTE CON `ADR-010`, capacidad/prueba pendientes |
| funciones degradadas | A3 §7 declara qué no está disponible y el respaldo manual | RESUELTO DOCUMENTALMENTE |
| `CTX-VESSEL` | subconjunto operacional de muelle crítico en `PHY-OPS-01`; mensajería externa alta en `PHY-CLD-03` | RESUELTO DOCUMENTALMENTE mediante partición dual |
| revocación aislada | `F3-ESC-002` continúa sin procedimiento aprobado del CLIENTE | BLOQUEADO EXTERNO |

#### B7-R.5 Dependencias y observaciones vigentes

| Dependencia | Estado tras integración | Qué permanece |
|---|---|---|
| `F3-DEP-001` A1 | **RESUELTA PARA DISEÑO** | aprobación final de roles y permisos permanece externa |
| `F3-DEP-002` A2/A3 | **RESUELTA PARA DISEÑO DOCUMENTAL** | contratos/protocolos efectivos, nombradas y aprobadores externos |
| `F3-DEP-003` C1–C4 | **RESUELTA PARA DISEÑO CON EXTERNOS** | site survey, producto/cantidad contractual y pruebas; las divergencias internas fueron conciliadas |
| `F3-DEP-004` D2/Subdocumento 5 | **PARCIAL** | D2 resuelto para modelo; falta catálogo de campos y tratamiento de privacidad |

Quedan resueltas en el corte vigente las diferencias de criticidad, `CTX-VESSEL`, la ubicación de `CH-CAB`, la consola de `ACT-TI`, el doble conteo `T11-C2-19`/`T11-SEC-04` y la suficiencia de la baseline de `ADR-001..010`. MA-5 debe conservar separados `SPOF-13`/`SPOF-22` y expresar como condiciones —no como omisiones— la selección de proveedor/regiones de `ADR-011`, productos, responsables y pruebas.

#### B7-R.6 Veredicto y continuación

| Comprobación | Resultado | Estado |
|---|---|---|
| 31 controles con amenaza | 31/31 | CONFORME DOCUMENTAL |
| 17 grupos SEC-PHYS integrados | 17/17 con nodo, servicio o proceso y tratamiento T-11 | CONFORME DOCUMENTAL |
| `RT-11.02` | modelo D2 auditado y regla de cinco disparadores | CUBIERTO EN DISEÑO; `EN CURSO` por pruebas/revisión/aprobación |
| dependencias internas | entradas recibidas y contradicciones conciliadas en MA-3 | CONFORME DOCUMENTAL; externos tratados |
| pruebas ejecutadas / riesgos aceptados / ADR aprobados | 0 / 0 / 0 | NO SE DECLARA CIERRE |
| diagramas | no producidos | DIFERIDOS A B8 |

**Corte histórico B7-R:** el punto de continuación original era la revisión conjunta. Esa revisión, la auditoría semántica y MA-3..5 ya se ejecutaron; P2 quedó superada y el corte vigente está en P3. No ejecutar B8 ni D3 y no dibujar diagramas antes de la secuencia que fija el plan maestro.

### B7-C. Revisión documental conjunta — bloque 5

**Fecha: 2026-09-06. Estado: COMPLETADO DOCUMENTALMENTE; no aprobado.** Se revisaron como un solo paquete D1, D2, sus trazas, el registro ADR global, la matriz global, las decisiones/escalamientos y la auditoría del frente. La revisión no encontró una inconsistencia interna nueva que obligue a reabrir el diseño.

| Puerta conjunta | Resultado verificable | Estado |
|---|---|---|
| inventarios e identificadores | 31 controles D1, 73 amenazas y 26 SPOF definidos; 20 nodos físicos y `LOC-INSP-01` como ubicación funcional; sin referencias huérfanas vigentes | CONFORME DOCUMENTAL |
| control ↔ amenaza ↔ físico/T-11 | 31/31 controles con amenaza; 17/17 grupos físicos emplazados o justificados; tratamiento T-11 explícito | CONFORME DOCUMENTAL CON PENDIENTES DE PRODUCTO/CANTIDAD |
| ADR y aceptación | corte histórico: 11 ADR registrados; `ADR-011` aún sin patrón recomendado; 0 ADR aprobados, 0 riesgos aceptados y 0 SPOF cerrados | SUPERADO EN SUFICIENCIA POR MA-4; aprobación pendiente |
| continuidad local | ruta completa `CH-APP/CH-CAB → GW-API local → CTX/DATA/evidencia local`; IAM, claves, cola, tiempo, nombres y logs incluidos | CONFORME DE DISEÑO; producto y prueba pendientes |
| trazabilidad y gobierno | D1/D2, trazas, matriz global y registro de decisiones conservan estados compatibles | CONFORME DOCUMENTAL |
| evidencia de implementación | productos, contratos, responsables nominales, capacidad, site survey y pruebas no acreditados | PENDIENTE; NO IMPIDE AUDITAR EL DISEÑO |

**Veredicto histórico del bloque 5:** el paquete D1–D2 quedó listo para auditoría independiente/general. Esa auditoría y MA-3..5 ya fueron ejecutadas; el estado vigente se lee en `trazabilidad/AUDITORIA_CIERRE.md` y en los registros MA-3..5 de `../00_Gobierno/`. B8, diagramas y D3 permanecen diferidos.

## Contenido listo para integrar

> Incorporar aquí la versión aprobada.

## Trazabilidad

Ver [`trazabilidad/TRZ_D1.md`](trazabilidad/TRZ_D1.md).
