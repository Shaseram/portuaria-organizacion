# T-11 — Matriz interna de trabajo trazable

**Corte técnico:** MA-5, 2026-09-06. **Estado documental vigente:** MA-8.

**Proveedor cloud:** AWS

**Emplazamiento cloud:** primaria São Paulo `sa-east-1` multi-AZ; secundaria Norte de Virginia `us-east-1`, activo-pasivo
**Estado:** P3 superada; baseline lista para ensamblado final y posterior auditoría D3. No contiene precios ni evidencia de implantación.

Esta matriz explica de dónde nace cada fila del formulario. El entregable contractual limpio está en `02_FORMULARIO_T11_FINAL.md`.

## 1. Catálogo consolidado

| ID T11 | Componente lógico/control | ID físico | Producto/servicio ofertado | Ubicación | Unidad/cantidad | Fuente del cálculo | Art. 16/justificación | RF/RNF/control | Diagrama | Responsable aporte | Estado |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `T11-C2-01` | `EDGE-RUN`, servicios críticos y `GW-API` local | `PHY-OPS-01` | clúster de servidores 1U empresariales, referencia Dell PowerEdge R/HPE ProLiant DL/Lenovo SR o equivalente; 16 núcleos, 128 GB RAM, 2×10 GbE, arranque espejo y PSU redundante por nodo | sala técnica del terminal | **3 nodos** | C4 §6.2.bis/§9 | cuórum y continuidad 72 h; la disponibilidad, no el TPS, gobierna la cantidad | `RT-03.10/.14`, `RT-08.01/.04` | físico/despliegue | C2/C4 | LISTA I1 |
| `T11-C2-02` | datos y buffer local | `PHY-OPS-02` | arreglo SSD redundante, 4×480 GB en RAID 10, control de errores y salud predictiva | sala técnica del terminal | **1 arreglo; 1,92 TB bruto / ≈960 GB útil** | C4 §4/§6.1/§9 | demanda ≈183 GB útil con 30 % de holgura; tolera al menos un disco | `RT-03.14`, `RT-08.02` | físico/capacidad | C2/C4 | LISTA I1 |
| `T11-C2-03` | red operacional segmentada | `PHY-OPS-04` | conmutadores de núcleo administrables en HA, referencia Cisco Catalyst/Aruba CX/Juniper EX o equivalente | rack de comunicaciones, sala técnica | **2 unidades** | C4 §9 | elimina SPOF de conmutación y separa zonas operacional, administrativa y protección | `RT-08.03`, `SEC-NET-01` | físico/red | C2/C3/D1 | LISTA I1 |
| `T11-C2-04` | seguridad perimetral y segmentación | `PHY-OPS-04` | cortafuegos NGFW en HA, referencia Fortinet FortiGate/Palo Alto PA o equivalente | rack de comunicaciones, sala técnica | **2 unidades** | C4 §9 | par redundante; controla los conductos sin exponer directamente la red portuaria | `RT-03.04`, `RT-08.03`, `SEC-EXP-01` | físico/seguridad | C2/D1 | LISTA I1 |
| `T11-C2-05` | continuidad eléctrica | sala técnica | UPS online de doble conversión con bancos certificados, referencia Eaton 93PS/Schneider Galaxy/Vertiv Liebert o equivalente | zona energética separada | **2×6 kVA y ≥5,4 kW; N+1; ≥30 min** | C4 §6.2.bis/§9 | cada unidad sostiene la carga de diseño de 2,67 kW | `RT-06.07/.12` | físico/despliegue | C2/C4 | LISTA I1 |
| `T11-C2-06` | generación autónoma | recinto del CLIENTE | grupo electrógeno con ATS y estanque; curva de consumo certificada | exterior/zona de generación del recinto | **1 conjunto ≥15 kVA y estanque ≥120 L útiles** | C4 §6.2.bis/§9 | sostiene ≥24 h; curva y prueba a carga cierran la aceptación | `RT-06.08/.09` | físico/despliegue | C2/C4 | LISTA I1; adquisición/obra del CLIENTE |
| `T11-C2-07` | ambiente de sala | sala técnica | climatización de precisión 24×7 con sensores de temperatura, humedad y agua; referencia Vertiv Liebert/Stulz o equivalente | sala técnica | **2×18.000 BTU/h, N+1** | C4 §6.2.bis/§9 | una unidad cubre ≈11.800 BTU/h de diseño y permite mantención | `RT-06.13/.14/.15` | físico/despliegue | C2/C4 | LISTA I1 |
| `T11-C2-08` | detección temprana | sala técnica | detección de incendio por aspiración láser, tipo VESDA/AnaLASER o equivalente | sala técnica | **1 sistema** | C2 §5/C4 §9 | detecta humo incipiente en el recinto técnico | `RT-06.16/.19` | físico/seguridad | C2 | LISTA I1 |
| `T11-C2-09` | supresión de incendio | sala técnica | extinción automática por agente limpio listado UL, con extintores certificados incluidos | sala técnica | **1 sistema** | C2 §5/C4 §9 | protege equipos sin agua; instalación conforme a NFPA y aprobación aplicable | `RT-06.17/.18/.19` | físico/seguridad | C2 | LISTA I1 |
| `T11-C2-10` | acceso físico | sala técnica | control biométrico facial, AFIS de respaldo, esclusa, bitácora y estación de enrolamiento exterior | acceso a sala técnica | **1 conjunto** | C2 §5/C4 §9 | impide paso simultáneo y conserva trazabilidad de ingresos | `RT-06.20..23`, `SEC-PHYS` | físico/seguridad | C2/D1 | LISTA I1 |
| `T11-C2-11` | videovigilancia del recinto | sala técnica | CCTV IP y NVR protegido, separado del VMS portuario | sala técnica | **4 cámaras + 1 NVR ≥4 TB útiles** | C4 §6.2.bis/§9 | conserva ≥30 días con ≈35 % de margen | `RT-06.24` | físico/seguridad | C2/C4 | LISTA I1 |
| `T11-C2-12` | respaldo fuera de sitio | `PHY-OPS-05` | custodia independiente de medios con inventario, rotación, legibilidad y recuperación auditada | recinto externo sin amenaza común | **1 servicio** | C2 §5.1/C4 §9 | sostiene la copia fuera de sitio del esquema 3-2-1-1-0 | `RT-06.26..28`, `SEC-BKP-01` | físico/continuidad | C2/C3 | LISTA I1 |
| `T11-C2-13` | operación y soporte | `PHY-OPS-06` | estación de trabajo empresarial con dos monitores, telefonía y gestión centralizada | espacio operativo fuera de la sala | **3 puestos de baseline: 2 diurnos + 1 guardia** | C4 `DIM-18`/§9 | cubre el modelo inicial; AHT real valida la dotación antes de congelar oferta | `RT-06.29..31`, `RT-08.07..09` | físico | C2/C4 | LISTA I1; condición AHT declarada |
| `T11-C2-14` | borde de cuatro zonas | `PHY-EDG-01..04` | gabinetes IP66 con tratamiento anticorrosivo marino, energía y monitoreo remoto | gate, patio, patio reefer y muelle | **59–61: 18 gate + 32 reefer + 3 muelle + 6–8 patio** | C1 §4; C4 §9; Caso 06 Cap. 14–15; supuesto propio 1 gabinete por estación/sitio | uno por emplazamiento operativo de baseline; site survey fija 6–8 de patio | `RT-08.12`, `CP RT-06.01` | físico/red | C1/C2/C4 | LISTA I1; rango con hito site survey |
| `T11-C2-15` | canal de terreno | borde/todas las zonas | dispositivo móvil robusto IP65, pantalla solar, uso con guantes, cámara/NFC/GPS según perfil | gate, patio, inspección y reefer | **97: 88 operativos + 9 repuestos** | Caso 06 Cap. 14.1; C4 §9 | uno por equipo proyectado; reserva propia del 10 %, redondeada hacia arriba, se valida por MTTR/lead time | `RT-08.11/.13` | físico/canal | C2/C4 | LISTA I1; repuesto sujeto a validación H2 |
| `T11-C2-16` | captura reefer local | `PHY-EDG-03` | concentrador industrial por tablero, protección marina y alarma local | patio refrigerado | **32 unidades** | Caso 06 Cap. 14.1; C4 §9 | uno por tablero proyectado; alarma ≤5 min sin depender de nube | `CP RT-05.29`, `RT-08.12` | físico/borde | C2/C4 | LISTA I1 |
| `T11-C2-17` | cómputo, datos, objetos, eventos y analítica | `PHY-CLD-03..08` | AWS: EKS, RDS for PostgreSQL Multi-AZ, S3/Object Lock, EventBridge, SQS FIFO/DLQ, Athena y Glue | São Paulo `sa-east-1`, subredes privadas y al menos 2 AZ; borde público controlado | **1 plataforma/suscripción elástica; baseline 2,5 TB online y 73 ev/s +30 %** | C4 §5/§9; `ADR-011` | concentra carga principal y servicios gestionados; IaC, FinOps y portabilidad por componente obligatorios | Art. 16.1–16.3, `RT-02.10`, `SEC-DATA-01` | lógico/físico/cloud | C2/C4 | LISTA I1 |
| `T11-C2-18` | recuperación regional | `PHY-CLD-10` | AWS DR activo-pasivo: réplica cross-region de RDS/S3 y cómputo EKS reducido, desplegable por IaC | Norte de Virginia `us-east-1` | **1 sitio lógico regional; RTO ≤4 h/RPO ≤15 min** | C2 §6; C3 §9; C4 §9; `ADR-007/011` | no existe segundo recinto del CLIENTE; región separada reduce amenaza física común | `RT-07.01..13`, `SEC-BKP-01` | físico/continuidad | C2/C3 | LISTA I1; pruebas futuras |
| `T11-C2-19` | telemetría, registro y detección | `PHY-CLD-09` + recolector `PHY-OPS-01` | CloudWatch, AWS Distro for OpenTelemetry y OpenSearch Service/SIEM integrado | `sa-east-1`, con colector y buffer local | **1 suscripción; piso derivable ≈8 GB/año, ingesta dominante se mide en H2** | C4 §9.bis/§9.ter | una plataforma nube/on-premise sin puntos ciegos; absorbe `T11-SEC-04` | `RT-03.16`, `SEC-LOG-01`, `SEC-SIEM-01` | observabilidad/seguridad | C2/C4/D1 | LISTA I1; unidad por ingesta y retención |
| `T11-C2-20` | sistema operativo y endurecimiento | `PHY-OPS-01` y borde compatible | distribución Linux empresarial con soporte extendido, parches centralizados y baseline CIS | sala técnica y componentes de borde | **1 suscripción corporativa; mínimo 3 servidores + nodos Linux de borde inventariados en H2** | C2 §3/§9 | evita software sin soporte durante los 56 meses; alcance final por inventario | `RT-03.15`, `SEC-HARD-01` | físico/operación | C2 | LISTA I1; alcance se congela en H2 |
| `T11-C2-21` | alojamiento físico y energía A/B | `PHY-OPS-01/02/04` | racks 42U con PDUs A/B, puesta a tierra, gestión de cables y reserva ≥30 % | sala técnica | **2 racks** | C4 §6.2.bis/§9 | separa cómputo/almacenamiento de comunicaciones/seguridad | `RT-06.03..05`, `RT-08.04/.05` | físico | C2/C4 | LISTA I1 |
| `T11-C3-01` | conectividad exterior redundante | terminal↔AWS | segundo enlace WAN de proveedor y ruta física distintos, con failover automático | terminal a nube | **2 caminos totales; cada camino ≥35 Mbps disponibles** | C4 §5.3/§9 | 32,5 Mbps de reposición gobiernan; capacidad real se prueba antes de aceptación | `RT-03.17/.20`, `SEC-SYNC-01` | red/despliegue | C3/C4 | LISTA I1; prueba de carrier pendiente |
| `T11-C3-02` | canal privado híbrido | terminal↔`sa-east-1` | AWS Site-to-Site VPN redundante sobre ambos enlaces | terminal y AWS primaria | **1 conjunto lógico: 2 conexiones VPN y 4 túneles administrados** | C3 §4/§13 | cifra el tránsito y evita exponer la red del terminal; cada carrier conserva ruta VPN propia | `RT-03.04/.21`, `SEC-SYNC-01` | red/seguridad | C3 | LISTA I1 |
| `T11-C3-03` | red operacional inalámbrica | `PHY-EDG-02` | red privada LTE/5G industrial, núcleo y gestión; alternativa mixta si el survey la invalida | patio de 18 ha | **6–8 estaciones base** | C4 §5.2/§9; `ADR-006` | la cobertura con pilas y handover, no el tráfico, fija la cantidad | `RT-03.23/.24`, `CP RT-03.24` | físico/red | C3/C4 | LISTA I1; site survey fija cantidad |
| `T11-C3-04` | entrega y cadena de suministro | ingeniería cloud | plataforma DevSecOps gestionada con CI/CD, registro de artefactos, SAST, SCA, DAST, secretos, imágenes, firma y SBOM | cuenta AWS de ingeniería separada de producción | **1 suscripción por proyectos y concurrencia** | C3 §4/§13 | permite despliegue reproducible y evidencia SLSA/SBOM sin herramienta por control | `RT-04.07`, `SEC-SDLC/PIPE/SUPPLY/ART` | despliegue | C3/D1 | LISTA I1 |
| `T11-SEC-01` | borde/gateway expuesto | `PHY-CLD-01/02`; perfil local incluido en `PHY-OPS-01` | CloudFront, AWS WAF y Shield; Kong Gateway híbrido o equivalente para política común nube/local | AWS primaria + perfil local restringido | **1 servicio gestionado + perfil local incluido en 3 nodos** | C4 §5.1/§9.bis | única superficie pública; el tráfico crítico local no depende del plano AWS | `SEC-EDGE-01/02`, `SEC-API-01` | lógico/seguridad | C2/D1 | LISTA I1 |
| `T11-SEC-02` | identidad, MFA y PAM | `PHY-CLD-03` + `PHY-OPS-01` | plataforma OIDC/OAuth 2.1/SAML 2.0 con MFA/PAM y verificador local de identidades vigentes | AWS + sala técnica | **1 plataforma; 175 internas, 187 externas y 2.400 eventuales/año** | C4 §9.bis; `ADR-008` | gobierno común y capacidad local para que un corte de nube no detenga la operación | `SEC-IAM-01`, `SEC-ADM-01` | seguridad | D1/C4 | LISTA I1; producto se congela en H2 |
| `T11-SEC-03` | claves y secretos | AWS + `PHY-OPS-01` | AWS KMS y Secrets Manager, con almacén local protegido y raíz no exportable | AWS primaria/DR y sala técnica | **1 servicio AWS + perfil local redundado en 3 nodos** | C4 §9.bis; `ADR-009` | separa ámbitos, evita que la continuidad dependa de una clave solo cloud | `SEC-KEY-01`, `SEC-SECRET-01` | seguridad | D1 | LISTA I1; custodios/prueba pendientes |
| `T11-SEC-05` | protección de endpoints | cargas cloud, nodos y puestos | EDR administrado con consola central | AWS, 3 nodos locales y 3 puestos | **1 suscripción; 6 endpoints fijos + cargas cloud elásticas** | C4 §9.bis | cubre sistemas administrables; excluye terreno sin agente certificado | `SEC-END-01`, `RT-11` | seguridad | D1/C4 | LISTA I1; workload cloud por medición |
| `T11-SEC-06` | monitoreo y respuesta 24×7 | servicio externo | SOC gestionado 24×7 y gestión de incidentes con RACI/SLA | remoto, integrado al SIEM | **1 servicio continuo 24×7** | D1 `SEC-PHYS`; restricción TI=5 | la dotación del CLIENTE no absorbe vigilancia permanente | `SEC-SOC-01`, `SEC-IR-01` | seguridad/operación | D1 | LISTA I1 |
| `T11-SEC-07` | aseguramiento continuo e independiente | servicio externo | escaneo continuo de vulnerabilidades y pentest independiente | activos AWS, on-premise y superficie pública | **1 suscripción + 1 ejercicio anual y antes de cada paso a producción** | C4 §9.bis; BTT Cap. 11 | separa detección continua de validación independiente | `SEC-VULN-01`, `SEC-PENTEST-01` | seguridad | D1 | LISTA I1; evidencia futura |
| `T11-SVC-01` | custodia de propiedad intelectual | servicio contractual | depósito de código fuente ante tercero independiente con cláusulas de liberación | custodio externo; repositorio fuente del CLIENTE | **1 servicio; actualización semestral (2 depósitos/año)** | BA Art. 84.6 | garantiza acceso al código ante insolvencia o incumplimiento grave | `BA Art. 84` | no representable como nodo | Integrador | LISTA I1 |

## 2. Decisiones de agrupación y no duplicidad

| Elemento revisado | Resolución T-11 | Motivo |
|---|---|---|
| `T11-SEC-04` registro/SIEM | incluido en `T11-C2-19` | `RT-03.16` exige una sola plataforma integrada nube/on-premise |
| respaldo, réplica e inmutabilidad | `T11-C2-12` + `T11-C2-18` | custodia física y DR regional son servicios distintos; los controles de backup no se recompran |
| segmentación y exposición | incluidos en `T11-C2-03/04` y `T11-SEC-01` | son capacidades de equipos/plataformas ya ofertados |
| cifrado nativo de RDS/S3 | incluido en `T11-C2-17`; claves en `T11-SEC-03` | separa consumo de almacenamiento del gobierno criptográfico |
| React, Spring Boot, React Native, SQLite, OpenAPI/AsyncAPI | sin fila propia | marcos y especificaciones incorporados al desarrollo, sin licencia/servicio separado |
| IaC, firma y SBOM | incluidos en `T11-C3-04` | una plataforma DevSecOps, no una compra por cada control |
| TOS, ERP, VMS, básculas, barreras y control de grúas existentes | `NO APLICA JUSTIFICADO` | sistemas conservados del CLIENTE; se integran, no se proveen ni reemplazan |
| obra civil, canalizaciones y alimentación del recinto | fuera del formulario; especificación en C2 | ejecución/adquisición del CLIENTE según Caso 06; no se oculta el requisito técnico |

## 3. Control de cobertura MA-5

| Verificación | Resultado | Evidencia |
|---|---|---|
| toda caja física ofertada tiene fila o inclusión justificada | **CUMPLE** | `PHY-CLD-01..10`, `PHY-OPS-01..06` y `PHY-EDG-01..04` cubiertos; `LOC-INSP-01` no es nodo |
| toda fila aparece en el catálogo y es representable en diagramas cuando corresponde | **CUMPLE EN CATÁLOGO** | 32 filas; `T11-SVC-01` es servicio contractual no nodal; F1–F5 están diseñadas y pendientes de producción final |
| toda cantidad tiene cálculo, unidad de servicio o rango con hito | **CUMPLE** | C4 §9; condiciones AHT, site survey, inventario H2 e ingesta expresas |
| controles/licencias de seguridad considerados una sola vez | **CUMPLE** | §2; `T11-SEC-04` absorbido por `T11-C2-19` |
| proveedor y regiones declarados | **CUMPLE COMO BASELINE I1** | AWS `sa-east-1` / `us-east-1`; `ADR-011 PROPUESTO` |
| obligación de escrow tratada | **CUMPLE** | `T11-SVC-01`; BA Art. 84.6 |
| no existen precios, tarifas ni montos | **CUMPLE** | revisión textual MA-5 |
| formulario final conserva exactamente cinco columnas | **CUMPLE** | `02_FORMULARIO_T11_FINAL.md` |

## 4. Condiciones que no impiden el Informe 1

- Validar AHT real antes de congelar los tres puestos de operación.
- Ejecutar site survey para cerrar 6–8 estaciones y 59–61 gabinetes.
- Medir capacidad efectiva y conmutación de ambos enlaces.
- Medir la ingesta dominante de logs; ≈8 GB/año es piso, no total.
- Congelar fabricante/modelo exacto, licencias por nodo y productos IAM/EDR/SOC en H2 sin cambiar la función ni la cantidad base.
- Acreditar latencia, tratamiento/residencia, catálogo, carbono y reversibilidad de AWS antes de aprobar `ADR-011`.
- Ejecutar pruebas de 72 h, restauración y DR en etapas posteriores; aquí quedan como criterios de aceptación.

**Puerta P3:** superada. Incorporar el formulario durante `R4` y auditarlo en D3 sin alterar sus cinco columnas.
