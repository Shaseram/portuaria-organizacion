# D3 — Puerta final de auditoría y consolidación

**Fecha de preparación:** 2026-09-06
**Estado:** `CONTRATO Y TRAZABILIDAD PREPARADOS — AUDITORÍA NO EJECUTADA`
**Momento de ejecución:** después de redactar el consolidado, incorporar T-11, producir F1–F5 y cruzar `V-DATA-01` con el Subdocumento 5.

## 1. Función de D3

D3 no redacta el Subdocumento 4 ni sustituye la ingeniería de A1–D2. Es la puerta que comprueba que la versión que efectivamente se entregará:

1. responde a T-7, T-21 y T-22;
2. cuenta una sola arquitectura lógica y física;
3. conserva trazabilidad hacia el expediente sin obligar al evaluador a leerlo;
4. mantiene alineados texto, diagramas, cantidades, T-11 y decisiones;
5. distingue baseline de Informe 1, dependencia externa y evidencia futura;
6. no incorpora precios ni afirmaciones de ejecución inexistente.

El consolidado debe ser autónomo. Las fuentes A1–D2 conservan el razonamiento y la evidencia extensa; una referencia nunca reemplaza la afirmación sustantiva que debe aparecer en el documento final.

## 2. Línea base que recibe D3

| Elemento | Línea base recibida | Lectura correcta |
|---|---|---|
| arquitectura lógica | ocho capas y 24 componentes A1 | diseño listo para sintetizar; F2 pendiente |
| integración y procesos | 21 contrapartes, siete familias, cinco recorridos críticos y autoridad por fase | diseño listo para sintetizar; F3 pendiente |
| arquitectura física | 20 nodos físicos + `LOC-INSP-01`, terminal/edge y AWS | diseño listo para sintetizar; F4 pendiente |
| seguridad | 31 controles, 73 amenazas y 26 SPOF enlazados | se publica la conclusión y F5; matrices completas quedan en expediente |
| capacidad | cálculos C4 y línea base física de sala | se publican resultados y supuestos decisivos |
| ADR | 11 `PROPUESTO`, 0 `APROBADO` | propuesta TERABYTE para I1; no aceptación del CLIENTE |
| Artículo 4 | 38 estándares/prácticas y 15 materias normativas | se publica trazabilidad ejecutiva, no la matriz completa |
| T-11 | 32 filas, cinco columnas y sin precios | listo para incorporar y maquetar |
| proveedor nube | AWS: `sa-east-1` primaria y `us-east-1` secundaria | baseline propuesta con riesgo común explícito |

## 3. Mapa canónico de llenado

Esta tabla gobierna la redacción. Si una fuente cambia, se actualiza primero su traza y después la sección final afectada.

| Sección final | Afirmación mínima que debe quedar en el consolidado | Fuente principal | Apoyo/contraste | Figura o tabla | Control D3 |
|---|---|---|---|---|---|
| `4.1.1 Esquema de solución` | propósito, actores, canales, límite TERABYTE, sistemas conservados y exclusiones | [A1 §§1–1.5](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) | Maestro y Subdocs. 2/3 | F1 | contexto distinto de arquitectura; problema no mezclado con solución |
| `4.1.2 Arquitectura lógica` | estilo modular híbrido, ocho capas, responsabilidades, límites de contexto e interfaces | [A1 §§2–6](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md) | ADR-001/002; D1 transversal | F2 + `T-SD4-01` | ocho capas visibles; UI no accede directamente a datos; módulos comprensibles |
| `4.1.3 Integración y procesos críticos` | contratos, eventos, TOS bidireccional, autoridad por fase, fallos, 72 h y reconciliación ≤90 min | [A2 §§1–7](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md) y [A3 §§2–10](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md) | C3 §§6–9; ADR-003/004 | F3 + `T-SD4-02` | síncrono/asíncrono, corte/retorno y función manual sin contradicción |
| `4.1.4 Datos y seguridad` | autoridad y almacenes a nivel arquitectónico; Zero Trust, identidad local, cifrado, claves, registro y SIEM | [D1 B1–B7](D1_ARQUITECTURA_DE_SEGURIDAD.md) | A1 §§4–5; D2 B1–B7; Subdoc. 5 | F5 + `V-DATA-01` | zonas/conductos y protección coherentes; datos coinciden con Subdoc. 5 |
| `4.1.5 Decisiones y cumplimiento` | decisiones principales, alternativas, consecuencias, condiciones y forma de acreditar Art. 4 | [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md) y [MA-6](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md) | D2 §B5; MA-4 | `T-SD4-07/08` | 11 propuestos, 0 aprobados; estándar→control→componente→evidencia |
| `4.2.1 Arquitectura física y emplazamiento` | terminal/sala/edge, AWS primaria/secundaria, redes, sistemas conservados y seis criterios Art. 16 | [C1 §§1–9](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md) | C2/C3/C4; ADR-005/006/011 | F4 + `T-SD4-03` | híbrida, propia del caso y con dominio de fallo comprensible |
| `4.2.2 Tecnologías de software` | frontend, backend, móvil, integración, datos, ejecución, observabilidad, IaC y SO | [C2 §§3–4](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) | complemento tecnológico y T-11 | `T-SD4-04` | selección, alternativa, modalidad, ubicación y vigencia sin convertir marcas en lógica |
| `4.2.3 Implementos HW/SW` | familias, cantidades, redundancia, interfaces, ambiente y licenciamiento/servicio | [C2 §§7–9](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) | C4 §§6/9/10; D1 `SEC-PHYS` | resumen + T-11 | toda caja/producto vuelve a nodo, cálculo y fila o exclusión justificada |
| `4.2.4 Data center primario` | sala condicional 34 m², fallback, racks, cómputo, energía, climatización, incendio, acceso y PUE | [C2 §5](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) | C4 §6.2.bis; ADR-005/007 | ampliación F4 + `T-SD4-05` | supuestos y validaciones externas visibles; no se presenta site survey como ejecutado |
| `4.2.5 Data center secundario` | AWS `us-east-1`, activo-pasivo, réplica, IaC, copia inmutable, RTO/RPO y failback | [C2 §6](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) | C3 §9; ADR-007/011; SPOF-22 | ampliación F4 | no confundir segunda AZ, segundo rack y sitio/región secundaria |
| `4.2.6 Despliegue, redes y continuidad` | ambientes, CI/CD, segmentación, doble WAN/VPN, patio, 72 h, sombra 8 h, HA/DR y respaldo | [C3 §§2–12](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md) | A3 §§5–7; D1 B3/B5/B6 | F3/F5; F6 condicional | cifras y estados normal/corte/retorno consistentes; pruebas declaradas futuras |
| `4.2.7 Dimensionamiento y capacidad` | demanda normal/punta, almacenamiento, buffer, red, carga/PUE, margen, sensibilidad y disparadores | [C4 §§3–10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) | A2/C2/C3/D1 | `T-SD4-06` | cada resultado conserva unidad, supuesto y fórmula decisiva |
| `4.2.8 Formulario T-11` | 32 filas con componente, producto/servicio, ubicación, cantidad y justificación | [T-11 final](../90_Consolidado/02_FORMULARIO_T11_FINAL.md) | [T-11 trazable](../90_Consolidado/01_T11_TRABAJO_TRAZABLE.md); C2/C4/D1 | formulario oficial | cinco columnas, sin precio, sin duplicidad y correspondencia 1:1 |

## 4. Recursos visuales que D3 debe auditar

| Recurso | Demostración mínima | Fuente de verdad | Estado actual |
|---|---|---|---|
| F1 — esquema de solución | actores, frontera, canales y sistemas conservados | A1 §§1–1.5 | PENDIENTE DE PRODUCCIÓN |
| F2 — arquitectura lógica | ocho capas, módulos, límites e interfaces principales | A1 §§2–6 | PENDIENTE DE PRODUCCIÓN |
| F3 — integración/proceso | contratos, TOS, autoridad, corte y retorno | A2/A3 | PENDIENTE DE PRODUCCIÓN |
| F4 — arquitectura física | sala/edge, AWS primaria/secundaria, redes y dominios de fallo | C1–C4 | PENDIENTE DE PRODUCCIÓN |
| F5 — seguridad | zonas, conductos, administración, IAM, cifrado y observabilidad | D1/D2/C3 | PENDIENTE DE PRODUCCIÓN |
| `V-DATA-01` | fuente de verdad, autoridad en corte, almacén, protección y retención | A1/D1/Subdoc. 5 | DISEÑADA; CRUCE SUBDOC. 5 PENDIENTE |
| F6 — continuidad | normal, corte 72 h, reconciliación ≤90 min y DR | A3/C3 | CONDICIONAL; NO PRODUCIR SI F3/F4 SON SUFICIENTES |

## 5. Ejecución de la auditoría D3

### Puerta A — cobertura formal

- [ ] Existen 4.1 y 4.2 con todos los elementos T-21.
- [ ] F1 es distinto de F2/F4, como exige T-22.
- [ ] Las ocho materias T-7 aparecen en texto, tabla o figura identificable.
- [ ] T-11 está incorporado dentro de 4.2.

### Puerta B — consistencia semántica

- [ ] A1–A3, C1–C4 y D1–D2 describen los mismos componentes, nodos y límites.
- [ ] La cadena lógica→físico→control→capacidad→T-11 no tiene huérfanos.
- [ ] 72 h, sombra 8 h, reconciliación ≤90 min, RTO ≤4 h y RPO ≤15 min no se contradicen.
- [ ] TOS, autoridad dominio×zona×fase y regreso al modo normal coinciden.
- [ ] AWS `sa-east-1`/`us-east-1`, sala primaria y sistemas conservados coinciden en texto y figuras.

### Puerta C — correspondencia visual

- [ ] F1–F5 son legibles, propios del Caso 06 y usan IDs/nombres canónicos.
- [ ] Toda flecha tiene dirección y semántica.
- [ ] Ningún producto sustituye un componente en F2.
- [ ] Las dependencias externas no aparecen como instaladas o probadas.
- [ ] F6 solo existe si agrega claridad demostrable.

### Puerta D — datos, normativa y evidencia

- [ ] `V-DATA-01` coincide con el Subdocumento 5 en fuente de verdad, retención y almacén.
- [ ] Los estándares publicados enlazan control, componente y evidencia.
- [ ] Certificados, visados, pruebas, pentest, restauraciones y site survey futuros están etiquetados.
- [ ] Los ADR conservan estado `PROPUESTO` salvo nueva evidencia formal.

### Puerta E — admisibilidad y forma

- [ ] El documento se entiende sin abrir el expediente.
- [ ] Las referencias permiten reconstruir el origen de cada afirmación crítica.
- [ ] No quedan notas internas, “recordar que”, `POR COMPLETAR` ni `PENDIENTE DE INTEGRAR`.
- [ ] No hay precios, tarifas, montos ni costos unitarios.
- [ ] T-11 conserva exactamente cinco columnas oficiales.

## 6. Regla de hallazgo y corrección

| Resultado | Uso |
|---|---|
| `CUMPLE` | afirmación explícita, coherente, trazada y suficiente para I1 |
| `PARCIAL` | existe baseline, pero falta precisión o cruce no bloqueante |
| `NO CUMPLE` | ausencia, contradicción o incumplimiento oficial |
| `CONDICIONADO EXTERNO TRATADO` | dueño, hito/condición, baseline, fallback y evidencia futura explícitos |
| `NO APLICA JUSTIFICADO` | la materia no aplica y la razón está demostrada |

Una corrección de D3 se aplica primero en la fuente canónica si cambia la solución y luego en consolidado/figura/T-11. Si solo corrige redacción, se modifica el consolidado sin reescribir el expediente histórico.

## 7. Veredicto permitido

D3 solo puede emitir uno de estos resultados después de ejecutar todas las puertas:

- `APTO PARA INFORME 1`;
- `APTO CON DEPENDENCIAS EXTERNAS TRATADAS`;
- `NO APTO PARA INFORME 1`.

No emitir veredicto mientras falten la redacción total, F1–F5 o el cruce de datos con Subdocumento 5.

## 8. Salidas de ejecución

1. [`TRZ_D3.md`](trazabilidad/TRZ_D3.md) con resultados y evidencias reales.
2. [`03_CHECKLIST_ENTREGA.md`](../90_Consolidado/03_CHECKLIST_ENTREGA.md) contado y cerrado.
3. Acta corta de hallazgos residuales y correcciones aplicadas.
4. Veredicto D3 fechado sobre la versión exacta del consolidado.

## 9. Resultado vigente

| Campo | Valor |
|---|---|
| contrato D3 | COMPLETO Y ALINEADO CON MA-7 |
| mapa de llenado | 13/13 secciones con fuente, apoyo, recurso y control |
| auditoría sobre documento final | NO EJECUTADA |
| brechas de contenido restantes | redacción total, F1–F5 y cruce fino con Subdocumento 5 |
| figura condicional | F6, solo por legibilidad |
| veredicto | NO EMITIDO |

## Trazabilidad

Ver [`trazabilidad/TRZ_D3.md`](trazabilidad/TRZ_D3.md).
