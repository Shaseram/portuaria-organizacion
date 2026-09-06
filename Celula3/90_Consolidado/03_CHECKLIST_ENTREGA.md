# Checklist final — Subdocumento 4

**Corte vigente:** MA-8 completada como preparación; estructura, fuentes y controles D3 listos.
**Pendiente de producción:** redacción editorial conjunta, diagramas aprobados por el equipo, ensamblado del T-11, D3 y maquetación. La base técnica y el cruce con Subdocumento 5 están cerrados para diseño I1. D3 se ejecuta sobre el resultado ensamblado.

## 1. Cobertura contractual y editorial

| Control | Evidencia vigente | Estado |
|---|---|---|
| 4.1 a) Esquema de solución | A1 + consolidado 4.1.1 | BASE TÉCNICA LISTA; REDACCIÓN/DIAGRAMA PENDIENTES |
| 4.1 b) Arquitectura lógica | A1–A3/D1 + consolidado 4.1.2–4.1.5 | BASE TÉCNICA LISTA; REDACCIÓN/DIAGRAMAS PENDIENTES |
| 4.2 a) Arquitectura física | C1–C4/D1 + consolidado 4.2.1 | BASE TÉCNICA LISTA; REDACCIÓN/DIAGRAMA PENDIENTES |
| 4.2 b) Tecnologías de software | C2 §4 + MA-5 | CUMPLE BASELINE I1 |
| 4.2 c) Implementos HW/SW | C2/C4/D1 + T-11 | CUMPLE BASELINE I1 |
| 4.2 d) Data center primario | C2/C4 + ADR-005/007 | SÍNTESIS LISTA; BASELINE CONDICIONADA |
| 4.2 e) Data center secundario | C2/C3 + ADR-007/011 | SÍNTESIS LISTA; CUMPLE BASELINE I1 |
| T-11 | 32 filas y cinco columnas oficiales | CUMPLE MA-5; MAQUETACIÓN PENDIENTE |
| Artículo 4 | 38 estándares/prácticas + 15 materias normativas | CUMPLE MA-6 PARA I1 |
| Estructura y extensión | MA-7 + esqueleto consolidado | CUMPLE MA-7; P4 APROBADA |
| Mapa de llenado y controles D3 | MA-8 + D3/TRZ-D3 | PREPARADO; EJECUCIÓN FINAL PENDIENTE |

## 2. Control visual

- [ ] El equipo define qué diagramas finales necesita el Subdocumento 4.
- [ ] Cada diagrama aprobado responde una pregunta clara y coincide con el texto definitivo.
- [ ] Los bocetos archivados no se incorporan automáticamente a la entrega.
- [x] `V-DATA-01` está definida como tabla compacta y no duplica el Subdocumento 5.

Los antiguos bocetos F1–F5 se conservan únicamente en `diagramas_archivados/`. No acreditan producción visual final.

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
| Diagramas definitivos | pendientes de definición y aprobación por el equipo |
| Bocetos anteriores | archivados; excluidos de la entrega |
| Vista de datos | tabla `V-DATA-01` |
| Controles finales | POR CONTAR EN D3 |
| Veredicto final | PENDIENTE D3 |

No emitir `APROBADO` si existe un `NO CUMPLE`, una contradicción silenciosa, un componente físico sin justificación, una fila T-11 sin respaldo o información económica en la oferta técnica.
