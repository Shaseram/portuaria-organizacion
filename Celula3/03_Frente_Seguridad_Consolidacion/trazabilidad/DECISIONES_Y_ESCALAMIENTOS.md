# Decisiones y escalamientos — Frente 3

| ID | Fecha | Entregable | Tipo | Tema | Alternativas/impacto | Recomendación o pregunta | Afecta a | Estado |
|---|---|---|---|---|---|---|---|---|
| `F3-DEC-001` | 2026-09-05 | D1 | CANDIDATO ADR | IAM | nube/local/híbrido con delegación | evaluar alternativa C de B2.7; sin producto seleccionado; F3-ESC-001/002 abiertos | A1/A2/A3/C1–C4 | EN ANÁLISIS |
| `F3-DEC-002` | 2026-09-05 | D1 | PROPUESTA ADR | llaves/secretos | KMS solo nube / jerarquías independientes / gobierno común con capacidad local protegida | alternativa C seleccionada como propuesta; sin producto, período ni custodios aprobados | A1/A2/A3/C1–C4/Subdoc. 5 | PROPUESTO |
| `F3-DEC-003` | 2026-09-05 | D1 | PROPUESTA ADR | detección/SOC | central solo nube / plataformas independientes / detección híbrida federada con SOC gestionado 24x7 | alternativa C seleccionada como propuesta; validar reparto, ubicación, dotación, capacidad y costo | A1/A2/A3/C1–C4/D2 | PROPUESTO |
| `F3-DEC-004` | 2026-09-05 | D1 | DISEÑO | promoción segura | recompilar por ambiente / construcción única y promoción del artefacto firmado | construir una vez, generar SBOM/procedencia y promover el mismo artefacto; herramienta pendiente | C3/C4/D2/D3 | PROPUESTO |
| `F3-DEC-005` | 2026-09-05 | D1/B7 | DISEÑO T-11 | agrupación de capacidades de seguridad | una fila por control / agrupar sin declarar inclusión / fila solo por capacidad ofertada con inclusión explícita | C4 crea fila solo por producto/licencia/servicio/hardware ofertado; capacidades incluidas referencian la fila principal | C1–C4/T-11/D3 | PROPUESTO |
| `F3-ESC-001` | — | D1 | EXTERNO | federación identidad | proveedor/directorio no confirmado | diseñar desacoplado | A1/C2 | BLOQUEADO EXTERNO |

## Dependencias de D1 para revisión y cierre

Se registran durante la planificación. No bloquean el avance independiente y no son decisiones de diseño aprobadas. Detalle y secuencia en [D1](../D1_ARQUITECTURA_DE_SEGURIDAD.md).

| ID | Entrada / productor | Validación necesaria | Estado |
|---|---|---|---|
| `F3-DEP-001` | A1: actores y componentes v0.1 | Confirmar correspondencia ACT-* → roles propuestos → funciones/componentes; sin catálogo paralelo | PENDIENTE |
| `F3-DEP-002` | A2/A3: contratos y operación local/TOS | Concretar controles de interfaces, autoridad y 72 h; no inventar contratos de terceros | PENDIENTE |
| `F3-DEP-003` | C1–C4: físico, redes, productos y capacidad | Ubicar controles, comprobar viabilidad/HA y cantidades/licencias para T-11 | PENDIENTE |
| `F3-DEP-004` | D2 y Subdoc. 5 | Revisar cobertura de amenazas y correspondencia de protección con datos concretos | PENDIENTE |

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
