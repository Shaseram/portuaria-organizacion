# TRZ-C2 — Tecnologías, hardware y data centers

**Regla.** Una fila por afirmación verificable o agrupación homogénea. Toda cita usa documento + capítulo/numeral + código + materia (Maestro §1.1). `CP` = FEP03 Caso 06; `BTT` = FEP02; `BA` = FEP01.

## 1. Trazas del entregable

| ID | Fuente | Requisito | Componente físico | Especificación/decisión | Cálculo C4 | Diagrama C1 | Fila T-11 | Estado |
|---|---|---|---|---|---|---|---|---|
| `TRZ-C2-001` | BTT, Cap. 6, numeral 6.1 — declarar tipología por sitio · `CP, Cap. 15, RT-06.01` — «sala de servidores principal del terminal, que debe habilitarse o reemplazarse» | tipología | todos los sitios | tabla de tipología declarada por sitio; sala principal ⇒ `RT-06.01` a `RT-06.34` íntegros | dimensionamiento por sitio | vista física | — | PARA REVISIÓN |
| `TRZ-C2-002` | `CP, Cap. 15, RT-06.01` — la sala actual «no cumple el Capítulo 6 del documento transversal» | tipología | sala técnica | el caso excluye la variante «sin sala principal»; `ADR-005` decide entre habilitar y reemplazar | — | — | `T11-C2-05`..`11` | PARA REVISIÓN |
| `TRZ-C2-003` | `CP, Cap. 15, RT-06.01` — nombra gabinetes de borde en **muelle, patio, patio refrigerado y gate** | tipología de borde | `PHY-EDG-01`..`04` | cuatro zonas con gabinete; inspección **sin recinto propio**, se corrige `PHY-EDG-05` de C1 | cantidad | vista de borde | `T11-C2-14` | PARA REVISIÓN |
| `TRZ-C2-004` | BTT, Cap. 6, `RT-06.05` — racks de servidores independientes de los de comunicaciones | racks | sala técnica | separación declarada, con ocupación y margen por rack | ocupación | plano de racks | dentro de obra | PARA REVISIÓN |
| `TRZ-C2-005` | BTT, Cap. 6, `RT-06.07` — UPS ≥30 min a plena carga · `CP, Cap. 6` — la sala actual tiene 25 min | energía | UPS | reemplazo del respaldo actual; autonomía a plena carga, no nominal | kW y autonomía | plano | `T11-C2-05` | PARA REVISIÓN |
| `TRZ-C2-006` | BTT, Cap. 6, `RT-06.08` — generación ≥24 h con estanque dimensionado y contrato de reabastecimiento | energía | grupo electrógeno | incluye el contrato de reabastecimiento, no solo el equipo | consumo y estanque | plano | `T11-C2-06` | PARA REVISIÓN |
| `TRZ-C2-007` | BTT, Cap. 6, `RT-06.09` — instalación independiente y **NCh Elec. 2777** de puesta a tierra | energía | instalación eléctrica | memoria eléctrica; cruza `STD-16` de la matriz global | — | plano | dentro de obra | PARA REVISIÓN |
| `TRZ-C2-008` | BTT, Cap. 6, `RT-06.11` y Cap. 15, `RT-15.04` — declarar kW, factor de potencia y PUE | energía | recinto | se declara el método; **el valor lo cierra C4** con la carga real | **sí, bloquea** | — | — | PENDIENTE C4 |
| `TRZ-C2-009` | BTT, Cap. 6, `RT-06.13`/`RT-06.14` — climatización de precisión N+1 y monitoreo de temperatura, humedad y presencia de agua | clima | climatización | N+1 e integración a observabilidad | carga térmica | plano | `T11-C2-07` | PARA REVISIÓN |
| `TRZ-C2-010` | BTT, Cap. 6, `RT-06.16`/`RT-06.17` — aspiración láser tipo AnaLASER y agente limpio tipo FM-200 con aprobación UL y norma NFPA | incendio | detección y extinción | producto de referencia con equivalencia admitida | — | plano | `T11-C2-08`, `09` | PARA REVISIÓN |
| `TRZ-C2-011` | BTT, Cap. 6, `RT-06.20` — biometría facial con AFIS · `CP, Cap. 10`, restricción 8 — biometría obligatoria objetada | acceso | control de acceso | poblaciones y recintos distintos; se declara en `F2-DEC-002` | — | — | `T11-C2-10` | PARA REVISIÓN |
| `TRZ-C2-012` | BTT, Cap. 6, `RT-06.24` — CCTV del recinto con ≥30 días · Maestro, reglas negativas 6 y 7 | acceso | CCTV del recinto | red y almacenamiento propios; **no se integra al VMS**; `F2-DEC-003` | retención | — | `T11-C2-11` | PARA REVISIÓN |
| `TRZ-C2-013` | BTT, Cap. 6, `RT-06.26` a `RT-06.28` — custodia de medios con recinto, inventario, rotación y verificación de legibilidad | custodia | `PHY-OPS-05` | pata física del «fuera de sitio» del 3-2-1-1-0; no comparte amenaza con la sala | volumen de medios | — | `T11-C2-12` | PARA REVISIÓN |
| `TRZ-C2-014` | BTT, Cap. 6, `RT-06.29` a `RT-06.31` — espacio de operación separado, con declaración de instalaciones reutilizadas · restricción 11 — TI de 5 personas | espacio | `PHY-OPS-06` | dimensionado por el modelo de operación de C3, no por defecto | puestos | plano | `T11-C2-13` | PENDIENTE C3/C4 |
| `TRZ-C2-015` | BTT, Cap. 6, `RT-06.32`/`RT-06.33` — rutas físicas distintas con ingreso por puntos separados · `CP, Cap. 6` — un proveedor de fibra | rutas | acometidas | criterio potencialmente decisivo de `ADR-005`; dato ausente | — | vista física | dentro de obra | **BLOQUEADO EXTERNO** `F2-ESC-008` |
| `TRZ-C2-016` | BTT, Cap. 7, `RT-07.01` — declarar y justificar activo-activo o activo-pasivo · restricción 11 | DR | `PHY-CLD-10` | **activo-pasivo con réplica caliente**, justificado por operabilidad con 5 personas | capacidad en reposo | vista física | `T11-C2-18` | PARA REVISIÓN |
| `TRZ-C2-017` | BTT, Cap. 7, `RT-07.02` — distancia al principal y análisis de amenazas comunes · `CP, Cap. 3` — emplazamiento único · `CP, Cap. 6` — sala a <300 m de la costa | DR | `PHY-CLD-10` | secundario en región de nube; amenazas comunes enumeradas | — | vista física | `T11-C2-18` | PARA REVISIÓN |
| `TRZ-C2-018` | BTT, Cap. 7, `RT-07.03` — replicación continua con medición y alertamiento del retraso | DR | replicación | el RPO sin instrumento de medición no es verificable | retraso admisible | — | `T11-C2-18` | PARA REVISIÓN |
| `TRZ-C2-019` | BTT, Cap. 7, `RT-07.05`/`RT-07.06` — conmutación ejecutable por el CLIENTE y retorno probado con reconciliación | DR | procedimiento | condiciona la modalidad escogida; el procedimiento es de C3 | — | — | — | PENDIENTE C3 |
| `TRZ-C2-020` | BTT, Cap. 7, `RT-07.07` — dos conmutaciones reales al año · `CP, Cap. 10`, restricciones 9 y 10 — congelamiento y nave | DR | calendario | siete meses hábiles al año para dos pruebas; calendario en C3 | — | — | — | PENDIENTE C3 |
| `TRZ-C2-021` | BTT, Cap. 7, `RT-07.09` a `RT-07.13` — 3-2-1-1-0, cifrado con clave independiente, inmutabilidad frente a credenciales comprometidas, restauración mensual y declaración por dominio de dato · Maestro §16.1 — siete retenciones | respaldo | política | tabla por dominio con frecuencia, retención y tiempo de restauración | **sí, bloquea** | — | `T11-C2-17`, `18` | PENDIENTE C4 |
| `TRZ-C2-022` | BTT, Cap. 7, numeral 7.2 — 99,95 % **por componente**; 99,9 % extremo a extremo del Art. 78° de las BA | disponibilidad | cadena completa | seis eslabones al 99,95 % deben producir 99,9 % E2E; exige redundancia dentro de cada eslabón | cálculo de cadena | — | — | PENDIENTE C4 |
| `TRZ-C2-023` | BTT, Cap. 8, `RT-08.01` a `RT-08.06` — cómputo, almacenamiento redundante, red en HA, fuentes redundantes en circuitos distintos, margen de crecimiento y equipamiento nuevo con garantía | hardware | `PHY-OPS-01`..`04` | clúster ≥3 nodos; **nivel RAID se justifica en C4 frente a alternativas** | **sí, bloquea** | vista física | `T11-C2-01`..`04` | PARA REVISIÓN |
| `TRZ-C2-024` | BTT, Cap. 8, `RT-08.07` a `RT-08.09` — estaciones con monitores duales, **NCh 2527** y gestión centralizada con cifrado de disco | puestos | `PHY-OPS-06` | cantidad por dimensionamiento; cruza `STD-16` | puestos | — | `T11-C2-13` | PENDIENTE C4 |
| `TRZ-C2-025` | BTT, Cap. 8, `RT-08.10` — exige **costo unitario estimado** · Maestro §2.1 y regla negativa 18 — sin precios en el Informe 1 | tensión | equipamiento de terreno | se entrega todo salvo el costo unitario, que va en la Oferta Económica | — | — | `T11-C2-15` | PARA REVISIÓN |
| `TRZ-C2-026` | BTT, Cap. 8, `RT-08.11`/`RT-08.12` — intemperie, guantes, luminosidad, autonomía por turno, grado IP y resistencia a caídas · `CP, Cap. 6` — condiciones de gate, patio y muelle | marino | dispositivos | tabla de cinco clases con protección mínima | cantidad | vista de borde | `T11-C2-15` | PARA REVISIÓN |
| `TRZ-C2-027` | `CP, Cap. 15, RT-06.01` — gabinetes con protección y anticorrosión acreditadas · `CP, Cap. 10`, restricción 12 · `CP, Cap. 6` — «los gabinetes se reemplazan antes de lo previsto» | marino | gabinetes | IP66 y 316L o equivalente; **vida útil real menor que la de catálogo**: el dato lo tiene el CLIENTE | reposición | vista de borde | `T11-C2-14` | **BLOQUEADO EXTERNO** |
| `TRZ-C2-028` | BTT, Cap. 8, `RT-08.13` — plan de reposición **durante los 56 meses del Contrato** | ciclo de vida | equipamiento de terreno | horizonte contractual explícito | reposición | — | `T11-C2-15` | PENDIENTE C4 |
| `TRZ-C2-029` | BTT, Cap. 8, `RT-08.16` a `RT-08.18` — ciclo de vida, borrado seguro con certificado y disposición final con gestor autorizado | ciclo de vida | todo el equipamiento | certificados entregables al CLIENTE | — | — | dentro del servicio | PARA REVISIÓN |
| `TRZ-C2-030` | BTT, Cap. 3, `RT-03.01` — declarar proveedor y regiones · Cap. 15, `RT-15.04`/`RT-15.05` — intensidad de carbono de la región y análisis comparativo | nube | proveedor y región | **decisión sin ADR asignado**; se propone `ADR-011` | — | vista física | `T11-C2-17`, `18` | **PARA REVISIÓN DEL INTEGRADOR** `F2-ESC-009` |
| `TRZ-C2-031` | BTT, Cap. 3, `RT-03.05`/`RT-03.07` — gestionado sobre autogestionado con justificación, y estrategia de reversibilidad | tecnología | pila de software | ninguna de las cinco funciones críticas depende de un servicio gestionado propietario | — | — | `T11-C2-17`, `20` | PARA REVISIÓN |
| `TRZ-C2-032` | BTT, Cap. 3, `RT-03.15` — endurecimiento **CIS** con gestión centralizada de parches y ventana acordada | tecnología | SO de servidores y borde | criterio de vigencia en lugar de versión congelada, por los 56 meses | — | — | `T11-C2-20` | PARA REVISIÓN |
| `TRZ-C2-033` | `BA, Art. 14.2` — la especificación del hardware de terreno es del PROPONENTE aunque la compra sea del CLIENTE · `CP, Cap. 11` — no se compra hardware, sí se especifica | límite | equipamiento de terreno | especificación completa sin adquisición | — | — | `T11-C2-15` | PARA REVISIÓN |
| `TRZ-C2-034` | BTT, Cap. C, entregables N° 8 y N° 10 — site principal y secundario **con planos**; hardware y dispositivos de terreno | checklist | entregables | los planos quedan para el pase final de diagramas | — | plano | — | PENDIENTE |

| `TRZ-C2-035` | D1, `SEC-PHYS-v0.1`, `SEC-KEY-01` y `ADR-009` — operación local sin clave que viva solo en nube · Maestro, regla negativa 8 | claves | KMS/HSM con **material de clave protegido en el sitio y raíz no exportable** | requisito excluyente: sin él las cinco funciones críticas no descifran durante el corte | — | — | `T11-SEC-03` | PARA REVISIÓN |
| `TRZ-C2-036` | D1, `SEC-END-01` · `CP, Cap. 11` — no imponer software al fabricante · `RT-03.18` gestión centralizada de flota | EDR | los dispositivos de terreno **no se presumen compatibles con agente**; se cubren por segmentación y gestión de flota | evita inflar el T-11 con licencias no instalables | cantidad | vista de borde | `T11-SEC-05` | PARA REVISIÓN |
| `TRZ-C2-037` | D1, `SEC-SOC-01` · `CP, Cap. 10`, restricción 11 — «toda función que requiera un especialista dedicado que la compañía no tiene debe ofrecerse como servicio y estar costeada» | SOC | monitoreo 24×7 como **servicio ofertado**, no como tarea del área TI de cinco personas | — | cobertura | — | `T11-SEC-06` | PARA REVISIÓN |

## 2. Cobertura declarada

| Obligación | Cómo la cubre C2 | Sección |
|---|---|---|
| `SD4-02` parte de tecnologías y emplazamiento físico | tipología por sitio y catálogo tecnológico | §1, §2, §3 |
| `SD4-05` recintos, energía, continuidad y respaldos | sala principal, site secundario y política de respaldo | §5, §6 |
| `SD4-06` insumos de capacidad | todo lo cuantificable se remite explícitamente a C4 | §5, §7, §9 |
| `SD4-08` arquitectura propia del caso | sala de 34 m² a <300 m del mar, gabinetes que se reemplazan antes de lo previsto, TI de 5 personas, congelamiento estacional | §1, §6, §8 |
| `T21-4.2-B` tecnologías de software | catálogo con referencia, alternativa y criterio de vigencia | §3 |
| `T21-4.2-C` implementos de hardware y software | cómputo, almacenamiento, red, puestos y terreno | §7, §8 |
| `T21-4.2-D` data center primario | 34 requisitos recorridos | §5 |
| `T21-4.2-E` data center secundario | Capítulo 7 completo | §6 |
| Checklist BTT, Cap. C, N° 8 y N° 10 | especificación de ambos sites y del equipamiento de terreno | §5, §6, §8 |
| `ADR-005` | tipología cerrada por el caso; alternativas acotadas | §1 |
| `ADR-007` | almacenamiento, RAID y HA especificados; el nivel se justifica en C4 | §7 |

## 3. Pendientes de esta traza

- Cerrar `TRZ-C2-008`, `021`, `022`, `023`, `024` y `028` con el dimensionamiento de C4.
- Cerrar `TRZ-C2-019` y `020` con el procedimiento y el calendario de C3.
- ~~Cruzar `TRZ-C2-011`, `012` y `031` con `SEC-PHYS-v0.1`~~ — **hecho** en §8.bis; ver `TRZ-C2-035` a `037`.
- `TRZ-C2-015` y `027` dependen de dato externo del CLIENTE.
- `TRZ-C2-030` requiere que se abra `ADR-011`.
