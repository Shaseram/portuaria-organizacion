# Revisión ADR y baseline de Informe 1 — MA-4

**Fecha:** 2026-09-06

**Entrada:** auditoría semántica `AFI1-010`, registro ADR global y fuentes A1–D2 posteriores a MA-3.

**Estado histórico del bloque:** `MA-4 COMPLETADA — P2 SUPERADA`; MA-5 promovió `ADR-011` y el estado operativo vigente está en `Celula3/README.md`.

## 1. Regla aplicada

Cada ADR fue revisado contra nueve elementos: contexto, dos o más alternativas reales, criterios ligados al Caso 06, selección, consecuencias positivas, consecuencias negativas, riesgo residual/SPOF, efecto en lógica–físico–seguridad–capacidad–T-11 y condición de revisión.

`PROPUESTO` significa que TERABYTE posee una baseline coherente para el Informe 1. No significa producto contratado, prueba ejecutada, riesgo aceptado ni aprobación del CLIENTE. `APROBADO` se reserva hasta completar las validaciones indicadas y la puerta final D3.

## 2. Resultado ADR por ADR

| ADR | Evidencia suficiente para baseline I1 | Estado anterior | Estado MA-4 | Selección o línea base | Condición abierta | Efecto en I1/T-11 |
|---|---|---|---|---|---|---|
| `ADR-001` estilo | sí; tres alternativas, criterios de volumen/TI=5/72 h, consecuencias y riesgo | PROPUESTO | **PROPUESTO** | núcleo modular híbrido con `EDGE-RUN`; despliegue corregido a progresivo por zona con canario | prueba 1,5×, operación y despliegue real | gobierna cajas lógicas/runtime; no crea fila por módulo |
| `ADR-002` runtime local | sí; todo/nada/selectivo comparados, inventario local y consecuencias | PROPUESTO | **PROPUESTO** | réplica selectiva de cinco funciones críticas y apoyos parciales; `GW-API` local restringido | prueba 72 h, falla de instancia, buffer y reconciliación ≤90 min | `T11-C2-01/02`, capacidades locales incluidas |
| `ADR-003` integración | sí; punto a punto, ESB pesado y bus persistente comparados | PROPUESTO | **PROPUESTO** | `INT-HUB` persistente + adaptador por contraparte; `INT-TOS` separado | contratos/protocolos reales y pruebas de bulkhead/DLQ | broker, conectores y plataforma de integración en MA-5 |
| `ADR-004` TOS | sí; permanencia, big bang y sustitución progresiva comparados | PROPUESTO | **PROPUESTO** | autoridad única `dominio×zona×fase`, envoltura y sustitución progresiva | puerta H2, capacidad real de lectura/escritura/CDC y soporte | adaptadores/licencias; no duplica fuente de verdad |
| `ADR-005` sala | sí como decisión condicional; tres alternativas y puertas normativas | CANDIDATO | **PROPUESTO** | rehabilitar los 34 m² existentes si cumplen acceso independiente, espacio operativo separado y dos ingresos físicos; si falla una puerta, reemplazar por sala compacta | site survey, plano a escala, rutas, ingeniería y ambiente marino | `T11-C2-01..13`; misma función/nodos en ambas variantes |
| `ADR-006` patio | sí como baseline condicionada; tres tecnologías y criterios del terreno | CANDIDATO | **PROPUESTO** | LTE/5G privada, rango inicial 6–8 estaciones; esquema mixto si el survey invalida cobertura/handover/independencia | site survey con patio cargado y prueba de conmutación | `T11-C3-02/03`, gabinetes y terminales relacionados |
| `ADR-007` almacenamiento/DR | sí; alternativas de RAID/HA/DR y cálculo C4 disponibles | CANDIDATO | **PROPUESTO** | 3 nodos; 4×480 GB RAID 10; DR activo-pasivo RTO 4 h/RPO 15 min; respaldo 3-2-1-1-0 | producto, rendimiento, autoridad de borrado, restauración y conmutación | `T11-C2-02/12/17/18` |
| `ADR-008` identidad | sí; tres patrones IAM, criterios y consecuencias completos | PROPUESTO | **PROPUESTO** | gobierno común con autenticación/autorización local crítica de identidades vigentes | directorio/federación, revocación aislada, producto y prueba | IAM/PAM; `T11-SEC-02`, sin duplicar runtime local |
| `ADR-009` criptografía | sí; tres patrones, selección, consecuencias y riesgo | PROPUESTO | **PROPUESTO** | gobierno común, ámbitos separados, raíz no exportable y capacidad local protegida | producto, custodios, rotación, compatibilidad y recuperación | `T11-SEC-03` y condiciones de datos/respaldo |
| `ADR-010` detección/SOC | sí; central, duplicado e híbrido comparados | PROPUESTO | **PROPUESTO** | detección híbrida federada, buffer/reglas críticas locales, SIEM central y SOC gestionado 24x7 | ingesta dominante, plataforma, residencia, RACI/SLA y pruebas | `T11-C2-19`, `T11-SEC-05..07`; SIEM no se duplica |
| `ADR-011` nube | **completado en MA-5**; patrón y criterios de MA-4 más selección concreta autorizada | CANDIDATO | **PROPUESTO** | AWS: primaria São Paulo `sa-east-1` en al menos dos AZ; secundaria Norte de Virginia `us-east-1`, activo-pasivo; copia inmutable con autoridad separada | validar latencia desde el terminal, residencia contractual, medición regional de carbono y catálogo al congelar oferta; revisar Chile solo tras disponibilidad general | fija `T11-C2-17/18`, borde, SIEM y ubicación del DR |

## 3. Baseline resultante para diagramas y T-11

1. Núcleo modular en nube y runtime local selectivo en el terminal.
2. Ruta local única mediante el perfil restringido de `GW-API`; no acceso directo a contextos o datos.
3. Integración por `INT-HUB` persistente y adaptadores; `INT-TOS` separa el legado.
4. TOS sustituido progresivamente por dominio, zona y fase.
5. Sala principal del terminal representada como una sola función física; se rehabilitan los 34 m² si superan las puertas normativas y se reemplaza por sala compacta si no.
6. Dos racks 42U separados por función: cómputo/almacenamiento y comunicaciones/seguridad; UPS/baterías en gabinetes o zona energética independiente.
7. Red de patio LTE/5G privada como referencia, con cantidad exacta condicionada al site survey.
8. Almacenamiento local RAID 10, DR activo-pasivo y respaldo 3-2-1-1-0.
9. IAM, criptografía y detección con gobierno común y capacidad local acotada a continuidad.
10. Nube AWS: `sa-east-1` como primaria multi-AZ y `us-east-1` como secundaria activo-pasivo; las validaciones de latencia, residencia, carbono y catálogo quedan como condiciones de aceptación, no como ubicación indefinida.

## 4. Cambios y verificaciones de MA-4

| Hallazgo/cambio | Archivo dueño | Propagación |
|---|---|---|
| azul-verde de `ADR-001` contradecía el canario por zona de C3 | A1 §6.1/§6.2 | alineado a despliegue progresivo por zona con canario |
| dos racks mezclaban TI/comunicaciones y no satisfacían `RT-06.05` | C4 §6.2.bis/§9 | dos racks separados por función; energía separada; `TRZ-C4-034` actualizado |
| `ADR-005` no seleccionaba baseline | C1 §7 | regla condicional 34 m²→rehabilitar; fallback→reemplazar |
| `ADR-006` tenía alternativa primaria pero seguía como candidato indefinido | C3 §13 | LTE/5G privada seleccionada con fallback y survey explícitos |
| `ADR-007` tenía piezas dispersas | C3 §13 + C4 | baseline consolidada de RAID/HA/DR/respaldo |
| conteos/estados ADR históricos | registro, D1/D2/trazas/matriz | corte al cierre de MA-4: 10 `PROPUESTO`, 1 `CANDIDATO`, 0 `APROBADO`; MA-5 promovió `ADR-011` y el estado vigente es 11/0/0 |

## 5. Pendiente legítimo y puerta P2

La puerta P2 quedó autorizada por el usuario el 2026-09-06 al seleccionar AWS. MA-5 promovió `ADR-011` a `PROPUESTO` y cerró proveedor y ubicaciones de baseline; siguen pendientes las verificaciones que permiten aprobarlo y contratarlo.

**Puerta P2: SUPERADA.** En este corte los diagramas, B8 y D3 quedaron diferidos; MA-5–MA-8 se completaron posteriormente.
