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
| 1 | [`D1_ARQUITECTURA_DE_SEGURIDAD.md`](D1_ARQUITECTURA_DE_SEGURIDAD.md) | Zero Trust y paquete físico temprano | `trazabilidad/TRZ_D1.md` | EN CURSO |
| 2 | [`D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md`](D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md) | STRIDE, ADR y SPOF | `trazabilidad/TRZ_D2.md` | EN CURSO |
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

**Avance D1 — bloque B4 (2026-09-05):** clasificación inicial `PUB/INT/CONF/RES`, cifrado total en reposo y adicional por campo sensible, jerarquía/custodia/rotación de claves y secretos, continuidad criptográfica local y alternativa C propuesta para ADR-009. Pendientes catálogo de campos de Subdocumento 5, productos/emplazamiento/capacidad, custodios y pruebas. Próximo bloque: **B5, detección y respuesta**.

**Avance D1 — bloque B5 (2026-09-05):** registro inalterable con retención 12 meses en línea + 24 adicionales en archivo, continuidad local de evidencia, fuentes híbridas, SIEM/EDR, nueve casos portuarios, SOC gestionado 24x7, respuesta a incidentes, vulnerabilidades y pentest. ADR-010 alternativa C queda `PROPUESTO`, no aprobado; productos, ubicación, dotación, capacidad, responsables y pruebas siguen pendientes. ADR-009 alternativa C también queda `PROPUESTO`.

**Avance D1 — bloque B6 (2026-09-05):** desarrollo seguro con revisión por pares y trazabilidad; puertas automáticas SAST/SCA/DAST/secretos/imágenes; construcción única, SBOM, firma y procedencia SLSA 3+; dependencias aprobadas; datos sintéticos por defecto; acceso excepcional a producción por PAM; SAMM inicial/anual y glosario breve. Herramientas, responsables, dimensionamiento y pruebas siguen pendientes. Próximo bloque: **B7, cobertura y paquete temprano**.

**Avance D1 — bloque B7 (2026-09-05):** auditoría intermedia ejecutada. Las 11/11 materias de D1 tienen diseño; FEP02 Cap. 11 queda 27/28 `EN CURSO` con RT-11.02 pendiente de D2, y Cap. 12 queda 13/13 `EN CURSO`. Se corrigieron estados rezagados, se agregaron SEC-GOV/CLOUD/HARD y `SEC-PHYS-v0.1` quedó consolidado en 17 grupos, listo pero no intercambiado. Sin montos/cantidades inventadas; D1 no puede cerrarse por dependencias, amenazas, productos, responsables, pruebas y diagramas. Próximo: evaluar commit/push e intercambio antes de **B8, integración, diagramas y cierre**.

**Inicio D2 — P0/B1 (2026-09-05):** se confirmó D2 como siguiente entregable independiente y se incorporó un plan de ocho bloques más preparación. B1 deja 7 clases `CLS-*`, 16 activos `AST-*`, 14 fronteras `TB-*` y 9 recorridos críticos en borrador trazable. D2 está `EN CURSO`, pero RT-11.02 permanece `PENDIENTE` hasta que B2 produzca amenazas; el inventario/método por sí solo no acredita cobertura STRIDE. A1/A2/C1/C3/Subdocumento 5 y entradas del CLIENTE refinan el modelo; no bloquean B2. Próximo: **B2, STRIDE por clases**, empezando por nube↔terminal, TOS y periferia operacional.

**Avance D2 — bloque B2 (2026-09-05):** STRIDE por clases desarrollado como propuesta no aprobada. Se definió primero una escala cualitativa explícita de probabilidad `P1..P4` e impacto `I1..I4` con matriz de riesgo, anclada a los umbrales del Caso 06 y no a un historial de incidentes inexistente. Se produjeron **66 amenazas `THR-001..066`**, cada una con activo, componente o clase, frontera, categoría STRIDE, condición y escenario portuario, probabilidad, impacto, control preventivo, control detectivo, respuesta correctiva con evidencia esperada, riesgo residual, estado y validación pendiente. Se desarrollaron primero las fronteras de mayor consecuencia —`TB-04` nube↔terminal y `EDGE-RUN`, `TB-06` plataforma↔TOS 2012 y `TB-05` operación↔periferia— y luego la cobertura inicial de las siete clases `CLS-*`; solo `CLS-DAT`/S queda declarada abierta, sin simular cobertura. Ningún riesgo queda aceptado (61 `POR VALIDAR`, 4 `ESCALADO`, 1 `PROPUESTA`), ningún ADR se aprueba y ningún SPOF se cierra: `THR-005/011/015/019/062` pasan a B4 como entradas obligatorias. `RT-11.02` sube de `PENDIENTE` a **`EN CURSO`**, nunca a cumplido, porque falta la cobertura por componente e interfaz reales y la evidencia de actualización ante cambios. `D2-DEP-001..005` siguen abiertas y `ESC-01/04/06/10/14`, `F3-ESC-001/002` conservan su identidad. Próximo: **B3, escenarios portuarios**, comenzando en `B3.1` con los nueve recorridos de `B1.5`; la continuidad autosuficiente está en `D2 B2.8`.

**Avance D2 — bloque B3 (2026-09-06):** escenarios portuarios desarrollados como propuesta no aprobada. Antes de escribir se revisó el plan y se detectó que el contrato exige **app offline, VMS y radio**, materias que no tenían recorrido propio en `B1.5`: se agregaron como escenarios en lugar de darlas por cubiertas dentro de otros (`B3-F01`). El bloque deja **12 escenarios `SCN-01..12`** que cubren 8/8 materias del contrato y 9/9 recorridos críticos, cada uno con secuencia por pasos, punto exacto de materialización de las amenazas, umbral o criterio del caso en juego, degradación declarada, evidencia esperada y pendientes de otros frentes. Se agregaron cuatro amenazas que los escenarios revelaron —`THR-067` dato en caché presentado como vigente, `THR-068` medio de radio compartido por posición, gate, reefer y cabina, `THR-069` alcance de la red de patio fuera del recinto y `THR-070` evidencia del VMS no recuperable cuando se la requiere—; el total pasa a `THR-001..070` y las amenazas críticas suben de 5 a 6. Se entregan **16 candidatos a punto único de falla `SPOF-CAND-01..16`** a B4, identificados y no evaluados. `RT-11.02` **no cambia**: sigue `EN CURSO`, porque falta la cobertura por componente e interfaz reales. Queda registrada una brecha que D2 no puede cerrar sola: la lista de funciones no disponibles durante la desconexión y su reemplazo manual (`B3-F03`), que depende de A3 y C1–C4. Próximo: **B4, registro consolidado de SPOF**, comenzando en `B4.1` con la tabla `B3.16`; la continuidad autosuficiente está en `D2 B3.18`.

**Avance D2 — bloque B4 (2026-09-06):** registro consolidado de puntos únicos de falla, en modo compacto. Los 16 candidatos de B3 se consolidan como **`SPOF-01..21`** cubriendo las cinco familias del contrato —infraestructura 6, servicio 5, datos 2, personas y proceso 3, terceros 5—, cada uno con escenario, impacto, mitigación propuesta, por qué subsiste, quién debería aceptarlo, prueba que demostraría independencia y estado. **Ninguno queda aceptado:** 10 `POR ACEPTAR` y 11 `ESCALADO`, es decir la mayoría depende del CLIENTE, de un fabricante o del levantamiento, no de los frentes. `B4-F01`: la familia personas y proceso no estaba representada en los candidatos técnicos de B3 y se incorporó aquí (`SPOF-14/15/16`), de donde surge `THR-071`; total `THR-001..071`. `RT-11.02` no cambia y sigue `EN CURSO`. Desde B4 el desarrollo restante de D2 se escribe en **modo registro**, en tablas compactas, porque su destino en el Subdocumento 4 son las subsecciones 4.1.8, 4.2.12 y 4.3, no un documento extenso. Próximo: **B5, revisión de ADR-001..010**; el arranque está en el cierre de `D2 B4.8`.

**Avance D2 — bloque B5 (corte 2026-09-06):** revisión de `ADR-001..010`, en modo registro. La revisión sale en dos formas porque la realidad del repositorio lo impone: **`ADR-001..007` están en `CANDIDATO` y sin contenido** —sus autores son A1, A2, A3 y C1–C4, que siguen en plantilla—, así que reciben **revisión de suficiencia**: qué alternativas debe comparar cada decisión como mínimo, qué consecuencia negativa no puede omitir, con qué SPOF y amenazas queda amarrada, su disparador de revisión y su efecto en T-11. `ADR-008`, `ADR-009` y `ADR-010` reciben **revisión completa** contra la regla de aprobación del Registro global, y los tres la cumplen en forma. **D2 no promovió ninguno en ese corte:** `ADR-008` estaba `EN ANÁLISIS`, `ADR-009` y `ADR-010` `PROPUESTO`, `ADR-001..007` `CANDIDATO`. El ajuste coordinado posterior se registra más abajo. `B5-F02`: **ninguno de los diez puede aprobarse hoy**, por dos razones complementarias —tres no tienen contenido que evaluar y siete tienen su riesgo residual atado a un SPOF `ESCALADO`—. `B5-F03`: la lista de funciones no disponibles durante la desconexión bloquea `ADR-002` y aparece por tercera vez; es la brecha más persistente y depende de A3 y C1–C4. No se agregan amenazas: total `THR-001..071`. `RT-11.02` sigue `EN CURSO`.

**Estado del desarrollo independiente de D2 (2026-09-06):** B5 lo cierra. **B6 está bloqueado** —su trabajo es sustituir `CLS-*` por los IDs reales de A1/A2/C1/C3 y esos catálogos no existen— y **B7 depende de B6**. Por decisión de secuencia, **B8 completo queda diferido** hasta integrar los demás frentes y auditar la cobertura: no se producirán por separado el diagrama de fronteras ni el resumen de riesgo residual.

**Ajuste coordinado D1/D2 (2026-09-06):** D1 B5.2.1 define la política de admisión de eventos que C4 necesita para dimensionar `T11-SEC-04`: seguridad/auditoría y alertas se conservan íntegramente; telemetría operacional cruda no se duplica en el SIEM por defecto y aporta anomalías, metadatos o referencias. El volumen dominante sigue pendiente de medición. `ADR-008` pasa a **`PROPUESTO` condicionado**, como línea base para integración y dimensionamiento; no está aprobado, no selecciona producto y conserva abiertos `F3-ESC-001/002` por directorio/federación y revocación durante aislamiento.
