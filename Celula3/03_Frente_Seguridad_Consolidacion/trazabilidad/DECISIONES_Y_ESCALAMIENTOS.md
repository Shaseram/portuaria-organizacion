# Decisiones y escalamientos — Frente 3

| ID | Fecha | Entregable | Tipo | Tema | Alternativas/impacto | Recomendación o pregunta | Afecta a | Estado |
|---|---|---|---|---|---|---|---|---|
| `F3-DEC-001` | 2026-09-05 | D1 | PROPUESTA ADR | IAM | nube/local/híbrido con delegación | alternativa C como línea base condicionada para integración/dimensionamiento; sin producto; F3-ESC-001/002 abiertos | A1/A2/A3/C1–C4 | PROPUESTO |
| `F3-DEC-002` | 2026-09-05 | D1 | PROPUESTA ADR | llaves/secretos | KMS solo nube / jerarquías independientes / gobierno común con capacidad local protegida | alternativa C seleccionada como propuesta; sin producto, período ni custodios aprobados | A1/A2/A3/C1–C4/Subdoc. 5 | PROPUESTO |
| `F3-DEC-003` | 2026-09-05 | D1 | PROPUESTA ADR | detección/SOC | central solo nube / plataformas independientes / detección híbrida federada con SOC gestionado 24x7 | alternativa C seleccionada como propuesta; validar reparto, ubicación, dotación, capacidad y costo | A1/A2/A3/C1–C4/D2 | PROPUESTO |
| `F3-DEC-004` | 2026-09-05 | D1 | DISEÑO | promoción segura | recompilar por ambiente / construcción única y promoción del artefacto firmado | construir una vez, generar SBOM/procedencia y promover el mismo artefacto; herramienta pendiente | C3/C4/D2/D3 | PROPUESTO |
| `F3-DEC-005` | 2026-09-05 | D1/B7 | DISEÑO T-11 | agrupación de capacidades de seguridad | una fila por control / agrupar sin declarar inclusión / fila solo por capacidad ofertada con inclusión explícita | C4 crea fila solo por producto/licencia/servicio/hardware ofertado; capacidades incluidas referencian la fila principal | C1–C4/T-11/D3 | PROPUESTO |
| `F3-ESC-001` | — | D1 | EXTERNO | federación identidad | proveedor/directorio no confirmado | diseñar desacoplado | A1/C2 | BLOQUEADO EXTERNO |
| `F3-ESC-003` | 2026-09-06 | D2 | EXTERNO | medio de radio del patio | posición, gate, reefer y cabina pueden depender del mismo transporte; el failover con patio cargado no está demostrado y no hay site survey | confirmar con C1/C3/C4 y levantamiento si existe independencia real de medios o caminos; mientras no exista, `THR-068` se mantiene CRÍTICO y `SPOF-CAND-03` no puede evaluarse | C1/C3/C4/levantamiento; entra a B4 | BLOQUEADO EXTERNO |

## Dependencias de D1 para revisión y cierre

Se registran durante la planificación. No bloquean el avance independiente y no son decisiones de diseño aprobadas. Detalle y secuencia en [D1](../D1_ARQUITECTURA_DE_SEGURIDAD.md).

| ID | Entrada / productor | Validación necesaria | Estado |
|---|---|---|---|
| `F3-DEP-001` | A1: actores y componentes v0.1 | Confirmar correspondencia ACT-* → roles propuestos → funciones/componentes; sin catálogo paralelo | RESUELTA PARA DISEÑO — `ACT-TI` funcional/técnico conciliado; aprobación nominal externa |
| `F3-DEP-002` | A2/A3: contratos y operación local/TOS | Concretar controles de interfaces, autoridad y 72 h; no inventar contratos de terceros | RESUELTA PARA DISEÑO DOCUMENTAL — contratos efectivos externos |
| `F3-DEP-003` | C1–C4: físico, redes, productos y capacidad | Ubicar controles, comprobar viabilidad/HA y cantidades/licencias para T-11 | RESUELTA PARA DISEÑO — producto contractual, site survey y pruebas permanecen externos |
| `F3-DEP-004` | D2 y Subdoc. 5 | Revisar cobertura de amenazas y correspondencia de protección con datos concretos | PARCIAL — D2 auditado; catálogo de campos pendiente |

Los bloqueos externos conservan F3-ESC-001 y los ESC del Maestro; no se fusionan con estas dependencias de compañeros. Los diagramas se elaboran tras definir el contenido y son condición para cerrar D1, no para intercambiar su paquete temprano.


## Propuestas de acceso del bloque B1 — 2026-09-05

- **F3-DEP-001:** revisar la matriz B1.3 de D1 sobre los 16 ACT-* del Maestro, sus especializaciones operativas y representación por expediente. Confirmar cómo representar desarrollo/soporte/SOC externos al CLIENTE; no asignarlos silenciosamente a ACT-TI.
- **F3-DEC-001 / ADR-008:** el bloque B1 propone identidad individual, rol más contexto y privilegios temporales. No selecciona producto, medio de credencial ni arquitectura IAM definitiva.
- **F3-DEP-002/003:** resolver baja ≤24 h frente a 72 h sin enlace y 8 h sin cobertura; incluir turnos nuevos, revocación local, aviso alternativo y reconexión. Sigue pendiente; no asumir revocación remota instantánea ni permitir credenciales vencidas.

Propuestas en desarrollo, sujetas a revisión; no se registran como ADR aprobados. Detalle y criterios de verificación en [D1, B1](../D1_ARQUITECTURA_DE_SEGURIDAD.md#b1-alcance-e-identidad--borrador-inicial).

## Pendientes precisados por B2 — 2026-09-05

| ID / tipo | Asunto | Tratamiento y condición de cierre | Estado |
|---|---|---|---|
| F3-ESC-002 / EXTERNO | Revocación inmediata FEP02 Cap. 12 RT-12.07 frente a terminal 8 h aislada; baja ≤24 h RT-12.10 | Validar con CLIENTE/protección procedimiento de aviso y bloqueo/retiro local. Si no resuelve, consulta formal de compatibilidad con offline del Caso 06 RT-03.10. B2.4 limita vigencia pero no declara cumplimiento inmediato ni excepción aceptada | BLOQUEADO EXTERNO |
| F3-DEP-002 + Maestro ESC-06 | Nombradas/acreditaciones nuevas durante 72 h sin enlace | A2/A3 y CLIENTE confirman fuente autorizada, procedimiento local, responsables y relevo sin cobertura; no prolongar turnos vencidos | PENDIENTE |
| F3-DEP-001/003 | Credencial/PIN, parámetros de sesión y concurrencia propuestos en B2.3 | Validar seguridad/usabilidad con terreno, representación de roles y soporte en producto; compatibilidad con EXT-ACC no presumida | PENDIENTE |
| F3-DEP-002/003 | Portal nube durante aislamiento del puerto | A2/A3/C3 confirman autoridad por operación, frescura de datos, citas recibidas/confirmadas y conciliación; B2.1 no modifica RF | PENDIENTE |

B2.7 contiene la propuesta parcial de ADR-008 usando las materias de la plantilla global. B7 la mantiene indexada globalmente como `EN ANÁLISIS`; todavía no está aprobada ni seleccionada al nivel de ADR-009/010.

## Avance B3 — 2026-09-05

- F3-DEP-002: A2/A3 deben validar FL-01..11, iniciadores/contratos y autoridad nube/local. FL-06/08/10 requieren desglose; no sustituyen el inventario de contrapartes.
- F3-DEP-003: C1/C3 validan zonas Z-*, rutas y redundancia; C2 productos/compatibilidad; C4 límites y capacidad. Una zona no equivale a una compra ni un despliegue por separado.
- Maestro ESC-06 y F3-ESC-001: confirmar transporte de terceros, directorio, dominios y control sobre precarga HSTS. Legado sin TLS compatible permanece pendiente, aunque exista adaptador.
- D1 B3.3 registra individualmente decisiones SEC-NET-01, SEC-EDGE-01/02, SEC-API-01, SEC-ADM-01, SEC-SYNC-01 y SEC-EXP-01 con fuente, motivo y evidencia. Propuestas en curso; diagramas e inventario final pendientes.

## Avance B4 — 2026-09-05

- `F3-DEC-002 / ADR-009`: queda `PROPUESTO` con la alternativa C: gobierno y política comunes con capacidades criptográficas separadas por ámbito y servicio local protegido para las funciones críticas. Las alternativas A/B se conservan resumidas como justificación y condición de revisión; no hay producto, HSM dedicado, período de rotación ni custodios aprobados.
- `F3-DEP-004`: Subdocumento 5 debe entregar el catálogo campo→propietario→sensibilidad→retención. D1 propone `PUB/INT/CONF/RES` y aplica `RES` como mínimo a datos personales, tarifas/volúmenes y datos que permitan inferir contenido de valor o ruta; no declara cubierto el 100 % de campos.
- `F3-DEP-002`: A2/A3 deben confirmar formatos, consumidores, autoridad y compatibilidad de TOS/periféricos. Un adaptador no acredita cifrado del tramo legado ni autoriza replicar claves en claro.
- `F3-DEP-003`: C1–C4 deben escoger/ubicar KMS/HSM/vault, demostrar HA/DR, continuidad 72 h, capacidad, recuperación y correspondencia T-11. Respaldo y claves de recuperación deben quedar fuera de la misma autoridad de borrado.
- CLIENTE/operación deben asignar propietario, custodios/suplencias y períodos de la política criptográfica. Las Bases exigen rotación declarada, pero B4 no inventa un plazo único.

Controles incorporados en D1: SEC-DATA-01, SEC-ENC-01, SEC-FIELD-01, SEC-KEY-01, SEC-SECRET-01 y SEC-BKP-01 parcial. Todas las pruebas son previstas y ADR-009 permanece sin aprobación final.

## Avance B5 — 2026-09-05

- `F3-DEC-003 / ADR-010`: queda `PROPUESTO` con la alternativa C —detección híbrida federada, colectores/buffer y reglas críticas mínimas locales, repositorio/SIEM central y SOC gestionado 24x7—. La aprobación final requiere validar reparto, ubicación, dotación, capacidad, proveedor y costo; no se presume un segundo SOC en la sala.
- `F3-DEP-001/002`: A1/A2/A3 deben confirmar inventario de fuentes/eventos, significado operacional, acciones de contención seguras y autoridad TOS/local. Una alarma operativa no se reemplaza por el SIEM.
- `F3-DEP-003`: C1–C4 deben ubicar y dimensionar colectores, buffer de 72 h más margen, almacenamiento de 12 meses en línea + 24 adicionales archivados, SIEM/EDR, HA/DR, licencias y servicio SOC/T-11.
- `F3-DEP-004`: D2 debe revisar los casos de uso, amenazas, severidades y riesgos residuales; D3 verificará evidencia y plazos.
- CLIENTE/adjudicatario deben asignar responsables, suplencias, RACI, canales y procedimientos para incidente crítico ≤2 h, brecha ≤24 h y causa raíz ≤5 días hábiles. Escaneo y remediación conservan 7/15/30 días; pentest independiente es anual y antes de cada producción.
- La simulación anual con participación del CLIENTE se incorpora como propuesta porque `RT-11.21` es deseable; requiere aceptación explícita antes de comprometerla.

Controles incorporados en D1: SEC-LOG-01, SEC-SIEM-01, SEC-END-01, SEC-SOC-01, SEC-IR-01, SEC-VULN-01 y SEC-PENTEST-01. Son diseño y criterios de prueba, no implementación ni evidencia ejecutada.

## Avance B6 — 2026-09-05

- `F3-DEC-004`: se propone construir una sola vez y promover el mismo artefacto inmutable, firmado y con procedencia/SBOM. Recompilar para producción rompería la equivalencia con lo probado; no se crea un ADR nuevo porque es una política de entrega derivada directamente de `RT-11.23/24` y `RNF-MAN-02/04`.
- `F3-DEP-003`: C3/C4 deben escoger y dimensionar CI/CD, ejecutores, SAST/SCA/DAST, escaneo de secretos/imágenes, registro de artefactos, firma/procedencia, licencias, HA y conservación de evidencia. D1 no fija proveedor.
- `F3-DEP-004`: Subdocumento 5 confirma campos/técnicas de anonimización o seudonimización; D2 cubre amenazas de cadena de suministro y D3 audita evidencia.
- CLIENTE/adjudicatario deben asignar revisión por pares, propietarios de reglas, aprobadores de excepciones y custodia del acceso excepcional a producción. Desarrollo no autoaprueba su cambio ni mantiene acceso directo permanente.
- Fallo de etapa obligatoria o hallazgo crítico bloquea promoción. Cobertura de lógica de negocio ≥70 %, SBOM CycloneDX/SPDX por versión, SLSA 3+, dependencias aprobadas y SAMM inicial/anual quedan como criterios, no como logros ejecutados.

Controles incorporados en D1: SEC-SDLC-01, SEC-PIPE-01, SEC-SUPPLY-01, SEC-NPDATA-01, SEC-PROD-01 y SEC-SAMM-01. B6 agrega un glosario breve de los términos usados hasta ahora.

## Auditoría B7 — 2026-09-05

- Resultado: 11/11 materias de D1 con diseño; 27/28 RT de FEP02 capítulo 11 y 13/13 RT del capítulo 12 en `EN CURSO`. `RT-11.02` permanece `PENDIENTE` hasta D2. Ningún requisito se marca aprobado.
- `B7-F01`: se corrigió la traza rezagada de Zero Trust, borde, gateway, bots, exposición e identidad/portal; el cambio es documental y no acredita ejecución.
- `B7-F02`: se agregaron SEC-GOV-01, SEC-CLOUD-01 y SEC-HARD-01 para materializar ISO/NIST, responsabilidad nube/privacidad y CIS, que antes estaban solo citados.
- `B7-F03 / F3-DEC-005`: `SEC-PHYS-v0.1` agrupa 31 controles en 17 entradas y distingue fila propia, agrupada, incluida o condicional. Evita convertir cada control en una compra T-11.
- `B7-F13`: se actualizaron a `EN CURSO` únicamente las filas de la matriz global con evidencia D1 ya disponible; las obligaciones de A1–A3/C1–C4/D2 permanecen pendientes.
- Brechas críticas abiertas: modelado D2; catálogos/contratos A1–A3; nodos/productos/capacidad C1–C4; catálogo de campos Subdocumento 5; responsables/pruebas/diagramas. F3-DEP-001..004 continúan `PENDIENTE`.
- ADR-008 se conserva `EN ANÁLISIS`; ADR-009/010 continúan `PROPUESTO`. B7 agregó comparación cualitativa consolidada sin inventar puntajes de productos.
- No se encontraron montos ni cantidades inventadas. El paquete está listo para intercambio interno, pero no se modificó el T-11 central ni se realizó commit/push.

## Dependencias de D2 para refinamiento y cierre

Estas dependencias no bloquean el modelado inicial por clases. Sí impiden declarar cobertura 100 % de RT-11.02, aceptar riesgos o cerrar ADR/SPOF sin correspondencia real.

| ID | Entrada / productor | Validación necesaria | Estado |
|---|---|---|---|
| `D2-DEP-001` | A1: componentes, criticidad y responsables `v0.1` | mapear `CLS-*`/`AST-*` a todo componente y propietario real | RESUELTA PARA DISEÑO DOCUMENTAL EN B6; quedan observaciones de autor |
| `D2-DEP-002` | A2/A3: interfaces, contratos, autoridad TOS y degradación | refinar `TB-*`, iniciadores, datos, fallos, fallback y conciliación por integración | RESUELTA PARA DISEÑO EN B6; contratos efectivos continúan externos |
| `D2-DEP-003` | C1–C4: nodos, red, sala, productos, HA/DR y capacidad | identificar independencia efectiva, SPOF por nodo/ruta, evidencia y efecto T-11 | CRUZADA EN B6 CON OBSERVACIONES A1↔C1; corrección/pruebas pendientes |
| `D2-DEP-004` | D1/Subdocumento 5: controles y catálogo de datos | validar amenaza→control y campo→sensibilidad→retención→custodia | PARCIAL — D1 RECIBIDO; SUBDOCUMENTO 5 PENDIENTE |
| `D2-DEP-005` | CLIENTE/terceros: contratos, SLA, directorio, site survey y aceptadores | validar probabilidad, viabilidad y responsable de cada riesgo residual | BLOQUEADO EXTERNO |

**Corte B1 (2026-09-05):** D2 no abre aún una decisión de arquitectura nueva. Delimita activos y fronteras para revisar ADR-001..010 en B5. Ningún riesgo ni SPOF queda aceptado; los pendientes externos del Maestro y F3-ESC-001/002 conservan su identidad.

## Avance D2 — bloque B2 — 2026-09-05

B2 **no abre ninguna decisión de arquitectura nueva ni ninguna dependencia nueva**. No se crean `F3-DEC-*` ni `D2-DEP-*` adicionales: las cuatro amenazas escaladas se apoyan en escalamientos ya registrados. Este registro deja constancia de a qué asunto abierto quedó amarrada cada una.

| Amenaza B2 | Asunto | Escalamiento vigente | Qué no puede darse por resuelto |
|---|---|---|---|
| `THR-015` | privilegios de la credencial técnica de integración con el TOS 2012 | `ESC-04` / `ESC-06` | el modelo de privilegios del legado lo determina el fabricante o el contrato; D2 no lo supone ni lo diseña |
| `THR-062` | acceso remoto permanente de proveedores y fabricantes a periferia y sistemas conservados | `ESC-06` / `D2-DEP-005` | sin contrato de soporte levantado no puede afirmarse que exista ventana acotada, aprobación por sesión ni grabación |
| `THR-025` | relevo de terminal compartida y credencial de eventual durante aislamiento | `F3-ESC-002` | la revocación inmediata frente a 8 h sin cobertura sigue bloqueada externamente; B2 limita vigencia, no declara cumplimiento |
| `THR-057` | contingencia de mensajería que derive en redigitación | `ESC-01` | fecha y líneas de la alianza siguen `PENDIENTE CLIENTE`; el compromiso de cero redigitación no se declara cumplido |

Además:

- `F3-DEP-004` (D1 ↔ D2): B2 vincula 22 controles `SEC-*` de D1 a amenazas concretas. **Referenciar un control no acredita implementación, producto, ubicación, capacidad ni prueba**; `SEC-PHYS-v0.1` sigue sin intercambiarse.
- `D2-DEP-004`: sin el catálogo campo→sensibilidad→retención del Subdocumento 5 no puede afirmarse minimización ni cobertura de privacidad en `THR-004`, `THR-014`, `THR-042`, `THR-045`, `THR-050`, `THR-055`, `THR-060` ni `THR-066`.
- `ADR-008` sigue `EN ANÁLISIS`; `ADR-009` y `ADR-010` siguen `PROPUESTO`. B2 no promueve ninguno.
- Ningún riesgo residual queda aceptado. El estado `ACEPTADO` solo puede aparecer en B4/B8 con aprobador nominado, fundamento, evidencia y condición de revisión.
- `RT-11.02` queda `EN CURSO` por B2. La propagación de ese estado a `TRZ_D1.md`, a la matriz de cumplimiento global y al T-11 corresponde a la puerta de integración; D2 no modifica `90_Consolidado/`.

## Avance D2 — bloque B3 — 2026-09-06

B3 **no abre ninguna decisión de arquitectura nueva**. Tampoco crea dependencias nuevas: las cuatro amenazas agregadas se apoyan en dependencias y escalamientos ya registrados. Se deja constancia de tres asuntos que sí requieren atención de otros frentes o del CLIENTE.

| Asunto | Origen | Qué falta y quién debe resolverlo | Estado |
|---|---|---|---|
| Lista de funciones **no disponibles** durante la desconexión y su reemplazo manual | `B3-F03`; Maestro §9.1 y regla negativa 13 | A3 debe declarar qué funciones son sostenibles localmente y cuáles no; C1–C4 deben demostrar la capacidad que lo sustenta. D2 exige el requisito y **no lo rellena**: inventar esa lista sería inventar el diseño de otro frente | PENDIENTE — `D2-DEP-002` / `D2-DEP-003` |
| Dependencia simultánea de posición, gate, reefer y cabina respecto del mismo medio de radio | `B3-F02`; `THR-068`; `SPOF-CAND-03` | C1/C3/C4 deben demostrar failover real con patio cargado y caminos o medios distintos; sin site survey la viabilidad del escenario permanece abierta. Es la única amenaza crítica nueva y entra obligatoriamente a B4 | PENDIENTE — `D2-DEP-003` / `ESC-10` |
| Retención, disponibilidad y verificabilidad de la evidencia asociada al VMS | `THR-070`; `SPOF-CAND-14` | El contrato del sistema conservado y el CLIENTE definen plazo, acceso y responsable de la evidencia. D2 no propone reemplazar el VMS ni crear un portal de video (reglas negativas 5 y 6) | PENDIENTE — `ESC-06` / `D2-DEP-005` |

Además:

- Se agregaron `THR-067..070`. Total `THR-001..070`: 6 críticas, 61 altas, 3 medias; 66 `POR VALIDAR` y 4 `ESCALADO`. Ninguna amenaza puede cerrarla D2 por sí sola y ninguna queda aceptada.
- Se entregan 16 candidatos a punto único de falla `SPOF-CAND-01..16` a B4. **Identificados, no evaluados y no aceptados.** Un candidato con mitigación declarada sigue siendo candidato hasta que se demuestre independencia real.
- `THR-033` se corrigió de `PROPUESTA` a `POR VALIDAR`: su cierre depende del catálogo de campos del Subdocumento 5 (`D2-DEP-004`), de modo que no era un estado que D2 pudiera resolver por su cuenta.
- `ADR-008` sigue `EN ANÁLISIS`; `ADR-009` y `ADR-010` siguen `PROPUESTO`. B3 no promueve ninguno.
- `RT-11.02` no cambia de estado con B3: sigue `EN CURSO`.

## Avance D2 — bloque B4 — 2026-09-06

B4 no abre decisiones de arquitectura. Consolida `SPOF-01..21` y deja **11 puntos `ESCALADO`** cuya resolución no depende de ningún frente. Los que no estaban ya registrados:

| SPOF | Asunto | Escalamiento | Estado |
|---|---|---|---|
| `SPOF-14` | continuidad de la planificación ante el retiro del planificador; la captura de conocimiento no ha comenzado | `ESC-05` | BLOQUEADO EXTERNO |
| `SPOF-15` | aprobador único de break-glass y de accesos privilegiados, sin suplente designado; origina `THR-071` | `D2-DEP-005` | PENDIENTE CLIENTE |
| `SPOF-16` | dotación por turno, suplencias y habilitación ISPS para atender alarma e incidente 24x7 con TI=5 | `D2-DEP-005` / `RT-11.17` | PENDIENTE CLIENTE |
| `SPOF-06` | sala técnica, energía y protección marina | `ESC-07` / `ESC-09`; `ADR-005` abierto | BLOQUEADO EXTERNO |

`B4-F02`: con 11 de 21 puntos escalados, **B5 no puede aprobar ningún ADR cuyo riesgo residual dependa de uno de ellos**. Ninguna aceptación de riesgo se registra en B4.

## Avance D2 — bloque B5 — corte inicial 2026-09-06

D2 revisó los diez ADR disponibles en aquel corte y no promovió ninguno. Esta lectura queda como antecedente histórico: fue superada por la incorporación posterior de A1–A3/C1–C4, registrada en la reapertura siguiente.

**Regla conservada del corte:** D2 revisa y recomienda; no aprueba decisiones ajenas ni acepta riesgos por la sola existencia de un texto.

**Condición de aprobación que hereda B8 y el integrador.** Ningún ADR puede aprobarse mientras su riesgo residual dependa de un SPOF `ESCALADO`. Hoy eso alcanza a `ADR-004` (`SPOF-17`/`ESC-04`), `ADR-005` (`SPOF-06`/`ESC-07`/`ESC-09`), `ADR-006` (`SPOF-03`/`F3-ESC-003`), `ADR-007` y `ADR-009` (`SPOF-12`), `ADR-008` (`SPOF-10`/`F3-ESC-001`/`F3-ESC-002`) y `ADR-010` (`SPOF-20`/`SPOF-16`).

**`B5-F01` — hallazgo histórico, corregido por integración.** La ausencia aparente de contenido se debía a que las ramas no estaban incorporadas, no a que A1–A3/C1–C4 no hubieran trabajado.

**`B5-F03` — parcialmente corregido.** A3 §7 aporta la lista de degradación y respaldo manual. Permanece la contradicción `CTX-VESSEL` entre A1/A3 y C1.

## Reapertura de integración D2 — B0/B1 (corte histórico)

- `D2-DEP-001` y las entradas documentales de `D2-DEP-002/003` fueron recibidas; B6 queda habilitado.
- `D2-DEP-004` queda parcial: D1 aporta controles y política de eventos, pero falta el catálogo del Subdocumento 5.
- `D2-DEP-005` continúa bloqueado externamente.
- `ADR-001..004` se revisaron sobre el texto real y quedan `PROPUESTO`, sin aprobación; `ADR-005..007` permanecen `CANDIDATO` por condiciones aún abiertas.
- Se abre `ADR-011` como `CANDIDATO` para proveedor/regiones cloud, sin seleccionar alternativa.
- La observación principal para B6 es `CTX-VESSEL`: continuidad crítica en A1/A3 frente a ubicación exclusivamente cloud en C1. Frente 2 conserva la responsabilidad de corregir su vista.

## Ajuste de coordinación D1/D2 — 2026-09-06

- D1 B5.2.1 fija la política de admisión de eventos para que C4 dimensione `T11-SEC-04`: seguridad/auditoría y alertas obligatorias ingresan al 100 %; telemetría operacional cruda permanece en su dominio y aporta al SIEM anomalías, metadatos y referencias, salvo requisito aprobado en contrario. El volumen dominante debe medirse; no se infiere desde el piso disponible.
- El autor D1 promueve `ADR-008` de `EN ANÁLISIS` a **`PROPUESTO`** como línea base condicionada de integración y dimensionamiento. No está aprobado ni selecciona producto. Su aprobación sigue bloqueada por `F3-ESC-001` —directorio/federación— y `F3-ESC-002` —revocación y aviso/bloqueo durante aislamiento—, además de las validaciones A1–A3/C1–C4.
- La revisión B5 de D2 se conserva como corte histórico: D2 no promovió decisiones. Este ajuste posterior proviene del autor de `ADR-008` y no altera la regla de que ningún ADR con residual atado a un SPOF `ESCALADO` puede aprobarse.
- Por decisión de secuencia, todos los diagramas y el resumen residual final quedan diferidos hasta integrar los demás frentes y ejecutar la auditoría de cobertura. No se inicia un B8 parcial.

## Avance D2 — bloque B6 — 2026-09-06

B6 cruza los catálogos integrados sin editar los entregables de Frente 1/2 ni convertir una entrada documental en evidencia ejecutada.

| Resultado o asunto | Registro aplicado | Estado / propietario |
|---|---|---|
| cobertura de componentes A1 | 24/24 con clase, amenazas y nodo físico | COMPLETA PARA DISEÑO; audita B7 |
| cobertura externa A2/A3 | 11/11 sistemas canónicos + `EXT-CON`; variantes `CP-NAV-*` y `EXT-AUT-*` reagrupadas | COMPLETA PARA DISEÑO; contratos efectivos siguen en `D2-DEP-005` |
| cobertura física C1 | 21/21 nodos con amenazas aplicables | COMPLETA CON OBSERVACIONES; corrige Frente 2 |
| suplantación propia de datos | `THR-072`, endpoint o réplica falsa; cierra `CLS-DAT`/S a nivel de modelo | POR VALIDAR — C1/C3/ADR-011 |
| fallo común cloud | `THR-073` + `SPOF-22`, asociados a `ADR-011` | POR ACEPTAR — C1–C4 + CLIENTE |
| `CTX-VESSEL` | A1/A3 lo requieren crítico/local; C1 lo ubica solo cloud y alta | OBSERVACIÓN CRÍTICA — Frente 2 |
| otras divergencias | criticidad de `CTX-EMIS`, `CTX-INSP`, `DATA-DOC`, `GW-API`, `GW-EDGE`, `SRV-IAM`; ubicación `CH-CAB`; actor `ACT-TI` | OBSERVACIONES — autores A1/C1 |
| SIEM/capacidad | posible solape `T11-C2-19`/`T11-SEC-04` | ACLARAR — C2/C4 |

La brecha histórica de funciones no disponibles queda **resuelta documentalmente** por A3 §7, que declara degradación y respaldo manual; permanece la contradicción física de `CTX-VESSEL`. El total vigente es `THR-001..073` —6 críticas, 64 altas y 3 medias— y `SPOF-01..22`; ninguno aceptado. `RT-11.02` continúa `EN CURSO` hasta B7. B8 sigue diferido y no se generan diagramas.

## Auditoría D2 — bloque B7 — 2026-09-06

B7 **no abre decisiones de arquitectura ni dependencias nuevas**. El modelo D2 queda `CONFORME PARA v0.5 CON PENDIENTE ADR`: `ADR-011` sigue sin alternativas concretas ni selección. Se corrigieron seis inconsistencias internas (`B7-F01..F06`) y se agregaron tres observaciones (`B7-O01..O03`). Ningún documento de Frente 1 o Frente 2 fue modificado.

### Hallazgos dirigidos a otros autores — abiertos y no resueltos por D2

| ID | Hallazgo | Destinatario | Efecto si no se resuelve |
|---|---|---|---|
| `B6-F03` | `CTX-VESSEL` es crítico y con continuidad local en A1/A3, pero C1 lo ubica solo en nube | C1 (Frente 2), con A1/A3 | `ADR-002` no puede cerrarse y la frontera funcional de `EDGE-RUN` queda condicionada |
| `B6-F04a` | Seis diferencias adicionales de criticidad entre A1 y C1: `CTX-EMIS`, `CTX-INSP`, `DATA-DOC`, `GW-API`, `GW-EDGE` y `SRV-IAM` | A1 y C1 | la criticidad determina HA, capacidad y filas T-11; sin acuerdo, el dimensionamiento queda sin base |
| `B6-F04b` | Ubicación de `CH-CAB`: C1 lo sitúa en muelle, A1 lo usa como canal de cabina y campo | C1 (Frente 2) | afecta cobertura de radio, `SCN-11` y la exposición de `THR-025`/`THR-067` |
| `B6-F04c` | Brecha de actor `ACT-TI`: falta la consola administrativa en el catálogo | A1 (Frente 1) | `THR-034`, `THR-062` y `SPOF-13` quedan sin actor responsable declarado |
| `B6-F05` | Posible doble conteo de observabilidad/SIEM entre `T11-C2-19` y `T11-SEC-04` | C2 y C4 | doble conteo en el Formulario T-11 |
| `B7-O01` | `SPOF-13` y `SPOF-22` son adyacentes pero distintos; no consolidarlos ni contarlos dos veces | D2 B8, C2/C4 e integrador | riesgo de perder un dominio de fallo o de duplicar una fila T-11 |
| `B7-O02` | La cobertura 21/21 de nodos es sobre el catálogo declarado; un subnodo o dominio de fallo interno puede quedar oculto, por ejemplo en `PHY-OPS-04` o `PHY-CLD-10` | C1 y C3 | la independencia real seguiría sin demostrarse |

### Dependencias de D2 — estado vigente tras B7

| ID | Estado | Nota |
|---|---|---|
| `D2-DEP-001` | RESUELTA PARA DISEÑO DOCUMENTAL | A1 entregó componentes y actores; persiste la brecha `ACT-TI` |
| `D2-DEP-002` | RESUELTA PARA DISEÑO DOCUMENTAL | A2/A3 entregaron contratos y autoridad; contratos efectivos de terceros siguen externos |
| `D2-DEP-003` | CRUZADA CON OBSERVACIONES | 21/21 nodos con amenaza; abiertas `B6-F03`, `B6-F04a/b`, `B6-F05`, `B7-O02` |
| `D2-DEP-004` | PARCIAL | falta el catálogo campo→sensibilidad→retención del Subdocumento 5; la cobertura de datos es de modelo, no de campo |
| `D2-DEP-005` | BLOQUEADO EXTERNO | contratos, SLA, site survey, aceptadores y pruebas siguen fuera de los frentes |

### Regla incorporada por la auditoría

`B7-F05` amplía la **regla de actualización de `RT-11.02`** a cinco disparadores: componente lógico A1, integración A2/A3, nodo físico C1–C4, control `SEC-*` de D1, y estado o alternativa seleccionada de un ADR. Cualquiera obliga a revisar amenazas, SPOF y trazas afectadas y a emitir un **corte fechado** en `TRZ_D2.md`. No se reescribe el historial de un bloque cerrado.

**Ningún riesgo aceptado, ningún SPOF cerrado y ningún ADR aprobado en B7.** `ADR-011` conserva `CANDIDATO`; la auditoría no cambió ninguna relación del Registro ADR global, por lo que ese registro **no se modifica** en este bloque.

## Integración documental D1–D2 — bloque B7-R — 2026-09-06

| Asunto | Resultado del cruce | Estado / salida |
|---|---|---|
| controles D1 ↔ amenazas D2 | 31/31 controles con amenaza asociada; los siete de gobierno/aseguramiento se enlazan en D2 B7.8 sin crear amenazas nuevas | CONFORME DOCUMENTAL |
| SEC-PHYS ↔ C1/C2/C4 | 17/17 grupos emplazados o justificados como servicio/proceso; 7 candidatos `T11-SEC-*` y 10 incluidos/condicionales | CONFORME DOCUMENTAL; conservar `F3-DEC-005` |
| identidad local | `SRV-IAM` en `PHY-CLD-03` con capacidad local en `PHY-OPS-01` | COHERENTE CON ADR-008; producto/revocación/prueba pendientes |
| claves y registro local | material protegido y colector/buffer en `PHY-OPS-01`; SIEM en `PHY-CLD-09` | COHERENTE CON ADR-009/010; capacidad/custodia/prueba pendientes |
| `RT-11.02` | modelo D2 auditado y regla de actualización cruzados con D1 | CUBIERTO EN DISEÑO; continúa `EN CURSO` |
| `ADR-011` | `SEC-CLOUD-01` enlazado a `THR-049/060/072/073` y `SPOF-22` | corte B7-R: candidato aún sin selección concreta; MA-4 agrega patrón recomendado y conserva el estado `CANDIDATO` |

**Corte histórico B7-R:** en ese corte `F3-DEP-001/003` aún tenían observaciones internas. MA-3 las concilia en A1/C1/C2/C3/D1/D2. El estado vigente conserva como externos site survey, contratos/productos finales, responsables, pruebas y aprobaciones; no se aprobaron ADR ni se aceptaron riesgos.

## Revisión conjunta D1–D2 — bloque 5/B7-C — 2026-09-06

- No se abre una decisión, dependencia ni escalamiento nuevo: la revisión confirma que los asuntos abiertos ya tienen propietario y registro.
- Se corrigen dos rezagos internos de `TRZ_D2`: B7 y la integración ya no se presentan como pasos futuros.
- El paquete D1–D2 se declara listo para auditoría independiente/general, sin promover ADR, aceptar riesgos, cerrar SPOF ni acreditar implementación.
- La auditoría recibe como lista única: `ACT-TI`, `CTX-VESSEL`, criticidades, `CH-CAB`, solape SIEM, distinción `SPOF-13`/`SPOF-22`, `ADR-011`, Subdocumento 5, contratos/productos, responsables, site survey, capacidad, pruebas y aprobaciones.
- B8, diagramas y D3 continúan diferidos hasta que los hallazgos de auditoría sean aplicados o queden formalmente asignados/aceptados.

## Corte MA-3 — 2026-09-06 (histórico)

- La ruta local queda cerrada como `CH-APP/CH-CAB → GW-API local → CTX crítico → DATA/evidencia/log local`; el perfil local de gateway está incluido en `EDGE-RUN` y no genera una compra duplicada.
- `CTX-VESSEL`, criticidades, `CH-CAB`, `ACT-TI` y el solape SIEM dejan de ser observaciones abiertas; las secciones B6/B7 que las enumeran se leen como cortes históricos.
- `F3-DEP-001/002/003` están resueltas para diseño de Informe 1. `F3-DEP-004` sigue parcial por el catálogo de campos del Subdocumento 5.
- El registro vigente es `THR-001..073` y `SPOF-01..26`, con 0 aceptados. Productos, site survey, pruebas, responsables nominales y aceptación formal continúan como dependencias externas tratadas.
- Próxima puerta en ese corte: MA-4; ya ejecutada. B8, diagramas y D3 continúan diferidos.

## Corte histórico MA-4 — 2026-09-06

- `ADR-001..010` quedan `PROPUESTO` como baseline del Informe 1; `ADR-011` permanece `CANDIDATO`; ninguno queda `APROBADO`.
- `ADR-005/006/007` pasan de candidato a propuesta porque ya tienen selección condicional, alternativa de salida, consecuencias y efecto transversal/T-11. Sus condiciones externas no desaparecen ni equivalen a aceptación del riesgo.
- `ADR-011` conserva el patrón región Chile multi-AZ + secundario del mismo proveedor + copia inmutable fuera de su plano de control, pero la selección de proveedor/regiones requiere mediciones y ofertas.
- No se acepta ningún riesgo ni se cierra ningún SPOF. La continuación queda en puerta P2 antes de MA-5/T-11; B8, diagramas y D3 continúan diferidos.

## Corte histórico MA-5 — 2026-09-06

- El usuario selecciona AWS: `sa-east-1` primaria multi-AZ y `us-east-1` secundaria activo-pasivo.
- `ADR-011` pasa a `PROPUESTO`; total vigente: 11 `PROPUESTO`, 0 `APROBADO`.
- `THR-073` y `SPOF-22` permanecen: usar un mismo proveedor no elimina el dominio común; portabilidad, copia inmutable y autoridad separada son tratamiento, no aceptación.
- T-11 contiene 32 filas. `T11-SEC-04` sigue como ancla y se absorbe en `T11-C2-19`; no se duplica el SIEM.
- B8, diagramas y D3 continúan diferidos. Próxima puerta: P3 antes de MA-6.

## Corte histórico MA-6 — 2026-09-06

- El Artículo 4 queda trazado en `00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md` mediante 38 estándares/prácticas y 15 materias normativas.
- La cadena vigente es `estándar/norma → requisito → control → componente → evidencia I1 → evidencia futura`; citar un estándar ya no sustituye su tratamiento.
- ISO/IEC 42010, calidad de datos y accesibilidad conservan salidas parciales controladas; certificaciones y visados externos mantienen dueño y condición.
- NIST AI RMF e ISO/IEC 42001 quedan `NO APLICA JUSTIFICADO`: `CTX-PLAN` no incorpora IA en la baseline.
- No se aprueba ADR, no se acepta riesgo ni se cierra SPOF. En el corte MA-6 el próximo bloque era MA-7; el corte vigente aparece a continuación.

## Corte histórico MA-7 — 2026-09-06

- Se adopta la estructura oficial 4.1/4.2; ADR, cumplimiento y dependencias se integran dentro de esas partes y no como capítulos 4.3–4.5.
- Se proponen cinco figuras obligatorias: F1 contexto, F2 lógica, F3 integración/proceso, F4 físico/despliegue y F5 seguridad.
- La vista de datos se resuelve con `V-DATA-01`; F6 continuidad queda condicionada a legibilidad, evitando una figura redundante.
- La extensión objetivo es 20–25 páginas incluido T-11. Las matrices completas permanecen como evidencia interna.
- En ese corte P4 quedó activa; MA-8 registra su aprobación y la secuencia vigente.

## Corte vigente MA-8 — 2026-09-06

- El usuario aprueba P4 y autoriza preparar el último bloque MA.
- D3 no redactará: auditará el consolidado real después de la redacción y los diagramas.
- Trece secciones quedan enlazadas a fuentes y trece controles quedan preparados en TRZ-D3.
- La alineación y el cruce `V-DATA-01` están cerrados como base; restan redacción editorial, diagramas del equipo, ensamblado y D3.
- La ejecución D3 y la maquetación son controles finales, no nuevos diseños de arquitectura.
