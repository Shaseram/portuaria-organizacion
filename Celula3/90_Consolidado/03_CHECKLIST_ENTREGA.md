# Checklist final — Subdocumento 4

**Corte vigente:** MA-8 completada como preparación; estructura, fuentes y controles D3 listos.
**Pendiente de producción:** redacción total, F1–F5, cruce fino con Subdocumento 5 y maquetación. D3 se ejecuta sobre ese resultado; no constituye contenido faltante.

## 1. Cobertura contractual y editorial

| Control | Evidencia vigente | Estado |
|---|---|---|
| 4.1 a) Esquema de solución | A1 + contrato editorial 4.1.1 | BASELINE LISTA; TEXTO/F1 PENDIENTES |
| 4.1 b) Arquitectura lógica | A1–A3/D1 + contrato 4.1.2–4.1.5 | BASELINE LISTA; TEXTO/F2/F3/F5 PENDIENTES |
| 4.2 a) Arquitectura física | C1–C4/D1 + contrato 4.2.1 | BASELINE LISTA; TEXTO/F4 PENDIENTES |
| 4.2 b) Tecnologías de software | C2 §4 + MA-5 | CUMPLE BASELINE I1 |
| 4.2 c) Implementos HW/SW | C2/C4/D1 + T-11 | CUMPLE BASELINE I1 |
| 4.2 d) Data center primario | C2/C4 + ADR-005/007 | BASELINE CONDICIONADA; SÍNTESIS FINAL PENDIENTE |
| 4.2 e) Data center secundario | C2/C3 + ADR-007/011 | CUMPLE BASELINE I1; SÍNTESIS FINAL PENDIENTE |
| T-11 | 32 filas y cinco columnas oficiales | CUMPLE MA-5; MAQUETACIÓN PENDIENTE |
| Artículo 4 | 38 estándares/prácticas + 15 materias normativas | CUMPLE MA-6 PARA I1 |
| Estructura y extensión | MA-7 + esqueleto consolidado | CUMPLE MA-7; P4 APROBADA |
| Mapa de llenado y controles D3 | MA-8 + D3/TRZ-D3 | PREPARADO; EJECUCIÓN FINAL PENDIENTE |

## 2. Plan visual mínimo

- [ ] `F1` — esquema de solución/contexto.
- [ ] `F2` — arquitectura lógica de ocho capas.
- [ ] `F3` — integración y proceso crítico, incluido corte/retorno.
- [ ] `F4` — arquitectura física híbrida y despliegue.
- [ ] `F5` — seguridad y límites de confianza.
- [x] `V-DATA-01` — vista de datos definida como tabla compacta; no duplica el Subdocumento 5.
- [ ] `F6` — solo si durante B8 continuidad no resulta legible en F3/F4.

No se crean diagramas separados por microservicio, actor, amenaza, ADR, observabilidad o CI/CD. Cada figura debe responder una pregunta, usar IDs canónicos y distinguir TERABYTE, CLIENTE, terceros y AWS.

## 3. Contenido que debe comprobar D3

### Arquitectura lógica e integración

- [ ] Ocho capas obligatorias visibles y consistentes con los 24 componentes.
- [ ] Actores/sistemas externos fuera del límite TERABYTE.
- [ ] Responsabilidades, límites de contexto e interfaces explícitos.
- [ ] UI sin acceso directo a datos.
- [ ] 21 contrapartes resumidas en siete familias, sin perder las críticas.
- [ ] Contratos, mensajería, versionado, idempotencia, DLQ y fallback coherentes.
- [ ] TOS bidireccional y autoridad dominio×zona×fase coherentes.
- [ ] Operación local 72 h y reconciliación ≤90 min explicadas sin ambigüedad.

### Arquitectura física, capacidad y continuidad

- [ ] Terminal, edge, AWS `sa-east-1`, AWS `us-east-1` y sistemas conservados visibles.
- [ ] Emplazamiento Art. 16 justificado por componente/familia.
- [ ] Sala primaria de 34 m² declarada como baseline condicionada, con fallback.
- [ ] Región secundaria diferenciada de un segundo rack o segunda AZ.
- [ ] Cinco ambientes, doble WAN/VPN, LTE/5G, HA, DR y respaldos consistentes.
- [ ] RTO ≤4 h, RPO ≤15 min, sombra 8 h y 3-2-1-1-0 no se contradicen.
- [ ] Resultados de capacidad conservan fórmula/supuesto decisivo y disparador.
- [ ] Cada cantidad T-11 vuelve a nodo, cálculo o criterio de dimensionamiento.

### Seguridad, normativa y decisiones

- [ ] Zero Trust, zonas/conductos, IAM local, PAM, cifrado, secretos, registros y SIEM visibles.
- [ ] Los controles publicados vuelven a amenaza, componente y evidencia.
- [ ] Artículo 4 se acredita como estándar→control→componente→evidencia.
- [ ] Los once ADR se presentan como `PROPUESTO`, no como aprobación del CLIENTE.
- [ ] Dependencias externas tienen dueño, baseline, fallback, hito y efecto.
- [ ] Pruebas, certificados, visados y productos contratados no se declaran ejecutados.

## 4. Forma y especificidad del Caso 06

- [ ] Se reconocen terminal, gate, patio, reefer, muelle, TOS, ERP, VMS, autoridades, ferrocarril y concedente.
- [ ] El Programa 2029 se trata como indivisible.
- [ ] Retención, datos y fuente de verdad coinciden con el Subdocumento 5.
- [ ] No se publican íntegramente las matrices de amenazas, SPOF, controles o RT.
- [ ] No hay precios ni información económica.
- [ ] Diagramas legibles en página, con título, propósito, leyenda y semántica de flechas.
- [ ] No hay diagramas genéricos ni productos en la vista lógica.

## 5. Veredicto

| Resultado | Valor vigente |
|---|---|
| Baselines editoriales listas | 4.1 y 4.2 |
| Figuras obligatorias pendientes | 5 (`F1..F5`) |
| Figura condicional | 1 (`F6`) |
| Vista de datos | tabla `V-DATA-01` |
| Controles finales | POR CONTAR EN D3 |
| Veredicto final | PENDIENTE D3 |

No emitir `APROBADO` si existe un `NO CUMPLE`, una contradicción silenciosa, un componente físico sin justificación, una fila T-11 sin respaldo o información económica en la oferta técnica.
