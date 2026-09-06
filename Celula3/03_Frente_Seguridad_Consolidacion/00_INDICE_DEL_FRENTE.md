# Frente 3 — Seguridad y consolidación

## Misión

Definir la seguridad transversal, desafiar las decisiones y asegurar que lógica, físico, capacidad y T-11 se integren sin brechas.

## Lectura obligatoria antes de comenzar

1. [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](../00_Gobierno/00_MAESTRO_CONTEXTO_ARQUITECTURA.md), completo.
2. [`01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md`](../00_Gobierno/01_PLAN_ENTREGABLES_Y_DEPENDENCIAS.md), reglas comunes y sección del Frente 3.
3. [`Célula 2 — cierre corregido y auditoría`](../../Celula2/00_CAMBIOS_TRAZABLES_Y_AUDITORIA_FINAL_20260904.md). Consultar además RNF, decisiones TOS, supuestos, retenciones y reglas enlazados por el Maestro al auditar controles o afirmaciones.

El Maestro sintetiza el contexto, pero Célula 2 permanece disponible como evidencia primaria de trabajo. El Frente 3 debe rechazar cualquier afirmación sin fuente, decisión o supuesto explícito.

## Entregables y orden

| Orden | Paquete | Resultado | Trazabilidad | Estado |
|---:|---|---|---|---|
| 1 | [`D1_ARQUITECTURA_DE_SEGURIDAD.md`](D1_ARQUITECTURA_DE_SEGURIDAD.md) | Zero Trust y paquete físico temprano | `trazabilidad/TRZ_D1.md` | EN CURSO — DISEÑO TRAZADO HASTA MA-6 |
| 2 | [`D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`](D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) | STRIDE, ADR y SPOF | `trazabilidad/TRZ_D2.md` | EN CURSO — DISEÑO TRAZADO HASTA MA-6 |
| 3 | [`D3_AUDITORIA_Y_CONSOLIDACION.md`](D3_AUDITORIA_Y_CONSOLIDACION.md) | auditoría y documento unido | `trazabilidad/TRZ_D3.md` | PENDIENTE |

## Trabajo independiente inmediato

Sin esperar a los otros frentes, producir:

- `SEC-PHYS-v0.1`: zonas, controles, identidades, cifrado, logging y componentes/licencias candidatos;
- modelo de amenazas por clases genéricas de componente, luego refinable con IDs;
- plantilla y control inicial de ADR/SPOF;
- matriz global y checklist de entrega;
- reglas de nombres, diagramas, trazabilidad y ausencia de precios.

## Secuencia acordada para D1

El [plan dentro de D1](D1_ARQUITECTURA_DE_SEGURIDAD.md) define el avance independiente y las dependencias de cierre. Se usan los actores ACT-* del Maestro; A1 valida su catálogo común y D1 propone roles/permisos vinculados a él. Primero contenido y matrices, luego diagramas. El paquete SEC-PHYS-v0.1 se comparte en texto/tablas para permitir el avance de Física. La planificación no cambia los entregables a aprobados ni inicia D2/D3.

## Apoyo al Frente 2

El Frente 3 valida segmentación, controles de sala/borde, administración, HA de componentes de seguridad, logging, licencias y justificaciones del T-11. Este apoyo no transfiere la propiedad de la arquitectura física.

**Avance D1 (2026-09-05):** bloque B1 de alcance, actores, roles y reglas de acceso en borrador. Próximo: sesiones y continuidad de identidad. Dependencias de cierre abiertas; SEC-PHYS-v0.1 aún no entregado.

**Avance D1 — bloque B2 (2026-09-05):** propuesta de sesiones, relevo, identidad local, offline/reconexión y emergencia; ADR-008 en análisis dentro de D1. Pendiente validar revocación en aislamiento (F3-ESC-002) y dependencias. Próximo bloque: zonas, conductos y exposición.

**Avance D1 — bloque B3 (2026-09-05):** zonas y conductos propuestos, controles de borde/gateway/TLS/bots, inventario preliminar de exposición y decisiones trazadas en B3.3. Pendientes redes/contratos reales y pruebas. Próximo bloque: **B4, datos, claves y secretos**, conforme al punto de continuación de D1.

**Avance D1 — bloque B4 (actualizado 2026-09-06):** clasificación `PUB/INT/CONF/RES`, cifrado total en reposo y adicional por campo sensible, jerarquía/custodia/rotación de claves y secretos, continuidad criptográfica local y alternativa C propuesta para ADR-009. Recibido el catálogo C4 de 28 campos y dispuestos sus ocho campos indexados; permanecen condicionados productos, custodios, privacidad y pruebas. Próximo bloque: **B5, detección y respuesta**.

**Avance D1 — bloque B5 (2026-09-05):** registro inalterable con retención 12 meses en línea + 24 adicionales en archivo, continuidad local de evidencia, fuentes híbridas, SIEM/EDR, nueve casos portuarios, SOC gestionado 24x7, respuesta a incidentes, vulnerabilidades y pentest. ADR-010 alternativa C queda `PROPUESTO`, no aprobado; productos, ubicación, dotación, capacidad, responsables y pruebas siguen pendientes. ADR-009 alternativa C también queda `PROPUESTO`.

**Avance D1 — bloque B6 (2026-09-05):** desarrollo seguro con revisión por pares y trazabilidad; puertas automáticas SAST/SCA/DAST/secretos/imágenes; construcción única, SBOM, firma y procedencia SLSA 3+; dependencias aprobadas; datos sintéticos por defecto; acceso excepcional a producción por PAM; SAMM inicial/anual y glosario breve. Herramientas, responsables, dimensionamiento y pruebas siguen pendientes. Próximo bloque: **B7, cobertura y paquete temprano**.

**Avance D1 — bloque B7 (2026-09-05):** auditoría intermedia ejecutada. Las 11/11 materias de D1 tienen diseño; FEP02 Cap. 11 queda 27/28 `EN CURSO` con RT-11.02 pendiente de D2, y Cap. 12 queda 13/13 `EN CURSO`. Se corrigieron estados rezagados, se agregaron SEC-GOV/CLOUD/HARD y `SEC-PHYS-v0.1` quedó consolidado en 17 grupos, listo pero no intercambiado. Sin montos/cantidades inventadas; D1 no puede cerrarse por dependencias, amenazas, productos, responsables, pruebas y diagramas. Próximo: evaluar commit/push e intercambio antes de **B8, integración, diagramas y cierre**.

**Inicio D2 — P0/B1 (2026-09-05):** se confirmó D2 como siguiente entregable independiente y se incorporó un plan de ocho bloques más preparación. B1 deja 7 clases `CLS-*`, 16 activos `AST-*`, 14 fronteras `TB-*` y 9 recorridos críticos en borrador trazable. D2 está `EN CURSO`, pero RT-11.02 permanece `PENDIENTE` hasta que B2 produzca amenazas; el inventario/método por sí solo no acredita cobertura STRIDE. A1/A2/C1/C3/Subdocumento 5 y entradas del CLIENTE refinan el modelo; no bloquean B2. Próximo: **B2, STRIDE por clases**, empezando por nube↔terminal, TOS y periferia operacional.

**Avance D2 — bloque B2 (2026-09-05):** STRIDE por clases desarrollado como propuesta no aprobada. Se definió primero una escala cualitativa explícita de probabilidad `P1..P4` e impacto `I1..I4` con matriz de riesgo, anclada a los umbrales del Caso 06 y no a un historial de incidentes inexistente. Se produjeron **66 amenazas `THR-001..066`**, cada una con activo, componente o clase, frontera, categoría STRIDE, condición y escenario portuario, probabilidad, impacto, control preventivo, control detectivo, respuesta correctiva con evidencia esperada, riesgo residual, estado y validación pendiente. Se desarrollaron primero las fronteras de mayor consecuencia —`TB-04` nube↔terminal y `EDGE-RUN`, `TB-06` plataforma↔TOS 2012 y `TB-05` operación↔periferia— y luego la cobertura inicial de las siete clases `CLS-*`; solo `CLS-DAT`/S queda declarada abierta, sin simular cobertura. Ningún riesgo queda aceptado (61 `POR VALIDAR`, 4 `ESCALADO`, 1 `PROPUESTA`), ningún ADR se aprueba y ningún SPOF se cierra: `THR-005/011/015/019/062` pasan a B4 como entradas obligatorias. `RT-11.02` sube de `PENDIENTE` a **`EN CURSO`**, nunca a cumplido, porque falta la cobertura por componente e interfaz reales y la evidencia de actualización ante cambios. `D2-DEP-001..005` siguen abiertas y `ESC-01/04/06/10/14`, `F3-ESC-001/002` conservan su identidad. Próximo: **B3, escenarios portuarios**, comenzando en `B3.1` con los nueve recorridos de `B1.5`; la continuidad autosuficiente está en `D2 B2.8`.

**Avance D2 — bloque B3 (2026-09-06):** escenarios portuarios desarrollados como propuesta no aprobada. Antes de escribir se revisó el plan y se detectó que el contrato exige **app offline, VMS y radio**, materias que no tenían recorrido propio en `B1.5`: se agregaron como escenarios en lugar de darlas por cubiertas dentro de otros (`B3-F01`). El bloque deja **12 escenarios `SCN-01..12`** que cubren 8/8 materias del contrato y 9/9 recorridos críticos, cada uno con secuencia por pasos, punto exacto de materialización de las amenazas, umbral o criterio del caso en juego, degradación declarada, evidencia esperada y pendientes de otros frentes. Se agregaron cuatro amenazas que los escenarios revelaron —`THR-067` dato en caché presentado como vigente, `THR-068` medio de radio compartido por posición, gate, reefer y cabina, `THR-069` alcance de la red de patio fuera del recinto y `THR-070` evidencia del VMS no recuperable cuando se la requiere—; el total pasa a `THR-001..070` y las amenazas críticas suben de 5 a 6. Se entregan **16 candidatos a punto único de falla `SPOF-CAND-01..16`** a B4, identificados y no evaluados. `RT-11.02` **no cambia**: sigue `EN CURSO`, porque falta la cobertura por componente e interfaz reales. Queda registrada una brecha que D2 no puede cerrar sola: la lista de funciones no disponibles durante la desconexión y su reemplazo manual (`B3-F03`), que depende de A3 y C1–C4. Próximo: **B4, registro consolidado de SPOF**, comenzando en `B4.1` con la tabla `B3.16`; la continuidad autosuficiente está en `D2 B3.18`.

**Avance histórico D2 — bloque B4 (2026-09-06; superado):** registro consolidado inicial de puntos únicos de falla. Los 16 candidatos de B3 se consolidaron como `SPOF-01..21`; después B6/B7 ampliaron el corte vigente a **26 SPOF y 73 amenazas**. En B4 ninguno quedó aceptado: 10 `POR ACEPTAR` y 11 `ESCALADO`. Este párrafo se conserva como secuencia histórica; el destino editorial vigente tras MA-7 es 4.1.4–4.1.5 y el punto actual de continuación está en `Celula3/README.md`.

**Corte histórico D2 — bloque B5 (2026-09-06):** la primera revisión de `ADR-001..010` se ejecutó antes de incorporar las ramas A1–A3/C1–C4. No promovió ni aprobó decisiones y dejó `RT-11.02` `EN CURSO`. Sus afirmaciones sobre ausencia de contenido quedaron superadas por la reapertura B0/B1 registrada más abajo.

**Estado antes de integrar los otros frentes (corte 2026-09-06):** B5 cerraba el desarrollo independiente y B6 figuraba bloqueado por ausencia de catálogos. Este estado queda como antecedente y es superado por la reapertura B0/B1 descrita más abajo.

**Ajuste coordinado D1/D2 (2026-09-06):** D1 B5.2.1 define la política de admisión de eventos que C4 necesita para dimensionar `T11-SEC-04`: seguridad/auditoría y alertas se conservan íntegramente; telemetría operacional cruda no se duplica en el SIEM por defecto y aporta anomalías, metadatos o referencias. El volumen dominante sigue pendiente de medición. `ADR-008` pasa a **`PROPUESTO` condicionado**, como línea base para integración y dimensionamiento; no está aprobado, no selecciona producto y conserva abiertos `F3-ESC-001/002` por directorio/federación y revocación durante aislamiento.

**Reapertura D2 — bloques B0/B1 de integración:** A1–A3 y C1–C4 ya están incorporados. Las entradas `D2-DEP-001/002/003` dejan de estar ausentes y B6 queda habilitado; `D2-DEP-004` sigue parcial por el catálogo de campos y `D2-DEP-005` permanece externo. B5 fue revalidado: `ADR-001..004` quedan `PROPUESTO` según sus autores, `ADR-005..007` siguen `CANDIDATO`, `ADR-008..010` siguen `PROPUESTO` y se abre `ADR-011` como `CANDIDATO`. La contradicción `CTX-VESSEL` A1/A3↔C1 se conserva como observación para que Frente 2 la corrija. Este corte quedó superado por B6.

**Avance D2 — bloque B6 (2026-09-06):** cruce contra los catálogos reales completado como borrador no aprobado. Los **24/24 componentes A1**, **11/11 sistemas canónicos externos**, la contraparte `EXT-CON` y los **21/21 nodos C1** quedan asociados a amenazas y evidencia prevista, sin reescribir los documentos de Frente 1/2. El cruce revela dos huecos: `THR-072` cubre la suplantación de un almacén o réplica y cierra `CLS-DAT`/S a nivel de modelo; `THR-073` cubre el fallo común de proveedor/región/plano de control cloud y origina `SPOF-22`, ligado a `ADR-011`. Total vigente: **73 amenazas** —6 críticas, 64 altas y 3 medias— y **22 SPOF**, ninguno aceptado. `D2-DEP-001/002` quedan resueltas para diseño documental y `D2-DEP-003` cruzada con observaciones; siguen abiertos el catálogo del Subdocumento 5, los contratos, site survey, pruebas y aceptadores. Se conservan como salidas la contradicción `CTX-VESSEL`, seis diferencias adicionales de criticidad, la ubicación de `CH-CAB`, la brecha `ACT-TI` y el posible doble conteo SIEM. `RT-11.02` sigue `EN CURSO` hasta auditar el modelo y su actualización en B7. Próximo: **D2 B7**, sin diagramas; B8 continúa diferido.

**Auditoría D2 — bloque B7 (2026-09-06):** auditoría documental v0.5 ejecutada contra evidencia primaria de A1–A3, C1–C4 y D1. **El modelo D2 queda `CONFORME PARA v0.5 CON PENDIENTE ADR`**: 24/24 componentes, 11 sistemas canónicos más `EXT-CON`, 21/21 nodos, `THR-001..073` y `SPOF-01..22` quedaron verificados; ningún riesgo fue aceptado. De doce comprobaciones, nueve son conformes —dos con observación—, dos inconsistencias fueron corregidas y una permanece pendiente: `ADR-011` está trazado a `THR-073`/`SPOF-22`, pero todavía no compara alternativas concretas ni selecciona una. `RT-11.02` queda cubierto a nivel de diseño documental y continúa `EN CURSO` por pruebas, revisión cruzada y aprobación. Ningún documento de Frente 1 o Frente 2 fue modificado. Próximo paso: **integración de D1 con D2**, sin diagramas ni D3.

**Integración D1–D2 — bloque B7-R (2026-09-06):** D1 fue reabierto contra A1–A3, C1–C4 y el D2 auditado. El cruce bidireccional deja **31/31 controles `SEC-*` asociados a amenazas**; los siete controles de gobierno/aseguramiento que no aparecían directamente en las filas técnicas se enlazaron a amenazas existentes sin inflar el modelo. Los **17/17 grupos `SEC-PHYS-v0.1`** tienen emplazamiento, servicio o proceso y tratamiento C4: siete candidatos `T11-SEC-01..07` y diez incluidos/condicionales, conservando la regla contra doble conteo. IAM, claves, logs y evidencia tienen capacidad local documental en `PHY-OPS-01`; productos, custodios, capacidad y pruebas siguen pendientes. `F3-DEP-002` queda resuelta para diseño; `F3-DEP-001/003` cruzadas con observaciones y `F3-DEP-004` parcial por Subdocumento 5. `RT-11.02` queda cubierto en diseño y continúa `EN CURSO`. Próximo: **revisión documental conjunta de D1/D2 y gobierno**; B8, diagramas y D3 siguen diferidos.

**Revisión conjunta — bloque 5/B7-C (2026-09-06):** D1, D2, ambas trazas, registro ADR, matriz global, decisiones y auditoría fueron revisados como un solo paquete. Se confirmaron 31/31 controles enlazados, 73 amenazas y 22 SPOF sin referencias huérfanas; se corrigieron dos textos rezagados de TRZ-D2 y no surgió una inconsistencia interna nueva. El paquete queda **listo para auditoría independiente/general**, no aprobado. Se entregan explícitamente `ACT-TI`, `CTX-VESSEL`, criticidades, `CH-CAB`, solape SIEM, `ADR-011`, Subdocumento 5 y la evidencia externa pendiente. B8, diagramas y D3 permanecen diferidos hasta recibir y aplicar hallazgos de auditoría.

**Corrección quirúrgica MA-3 (2026-09-06):** el párrafo anterior se conserva como corte histórico. La auditoría semántica posterior permitió cerrar continuidad local, catálogos, criticidades, capacidad y SPOF. El inventario quedó en **24 componentes, 20 nodos `PHY-*` + `LOC-INSP-01`, 31 controles, 73 amenazas y 26 SPOF; ninguno aceptado**.

**Revisión ADR MA-4 (corte histórico 2026-09-06):** dejó 10 `PROPUESTO`, `ADR-011` `CANDIDATO` y habilitó P2.

**Consolidación MA-5 (corte histórico 2026-09-06):** AWS queda seleccionado con `sa-east-1` primaria multi-AZ y `us-east-1` secundaria activo-pasivo. `ADR-011` pasa a `PROPUESTO`; el total es **11 `PROPUESTO`, 0 `APROBADO`**. T-11 consolida 32 filas, sin precios ni duplicidad de SIEM, e incorpora racks y escrow semestral. El paquete llegó a **P3** y habilitó MA-6.

**Matriz del Artículo 4 MA-6 (2026-09-06):** `AFI1-008` queda cerrado para Informe 1 mediante [`11_MATRIZ_ARTICULO4_MA6.md`](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md): 38 estándares/prácticas y 15 materias normativas enlazan requisito, control, componente, evidencia I1 y evidencia futura. La baseline no incorpora IA (`NO APLICA JUSTIFICADO`); las certificaciones, pruebas y visados no se presentan como ejecutados.

**Proyección editorial MA-7 (corte histórico 2026-09-06):** [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](../00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md) fija el Subdocumento 4 dentro de las secciones formales 4.1/4.2, una extensión orientativa de 20–25 páginas incluido T-11, F1–F5 como figuras obligatorias, `V-DATA-01` como vista de datos y F6 solo si continuidad no resulta legible. En ese corte la puerta P4 quedó activa.

**Preparación D3 MA-8 (estado vigente 2026-09-06):** [`13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md`](../00_Gobierno/13_PREPARACION_D3_Y_MAPA_ENSAMBLADO_MA8.md) actualiza D3 y TRZ-D3 con trece secciones y trece controles trazados. La alineación C3–C4 y `V-DATA-01` están cerradas como base. Quedan la redacción editorial conjunta, los diagramas que apruebe el equipo, el ensamblado y la maquetación; D3 se ejecutará después sobre el artefacto real.
