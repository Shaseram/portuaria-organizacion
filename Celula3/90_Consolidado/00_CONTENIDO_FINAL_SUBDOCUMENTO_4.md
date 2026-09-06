# Subdocumento 4 — Arquitectura lógica y física de la solución

**Caso:** 06 Portuaria — TERABYTE.
**Estado:** `ESQUELETO TRAZADO MA-8`; redacción total, figuras y auditoría D3 pendientes.
**Fuentes de control:** Maestro, Matriz Global, Registro ADR, MA-3 a MA-8 y expedientes A1–D2.

> Este archivo será la síntesis entregable. No es una bitácora ni sustituye las trazas. Su estructura se ajusta a 4.1/4.2 del Formulario T-21; los contratos detallados de cada sección están en [`12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md`](../00_Gobierno/12_PROYECCION_EDITORIAL_Y_PLAN_DIAGRAMAS_MA7.md).

> El mapa completo de llenado y los controles que deberá pasar la versión redactada están en [`D3_AUDITORIA_Y_CONSOLIDACION.md`](../03_Frente_Seguridad_Consolidacion/D3_AUDITORIA_Y_CONSOLIDACION.md). El texto final debe afirmar la solución y luego citar; no puede limitarse a decir “ver A1/C1/D1”.

## Regla de lectura del Informe 1

La versión final distinguirá entre decisión o baseline, condición externa y evidencia futura. No declarará como ejecutados productos contratados, pruebas, certificaciones, site survey, visados o aceptación del CLIENTE.

## 4.1 Arquitectura lógica

### 4.1.1 Esquema de solución

**Contenido de cierre:** propósito, actores agrupados, canales, frontera TERABYTE, sistemas conservados/externos y exclusiones.
**Fuente de llenado:** [A1 §§1–1.5](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md).
**Figura:** F1 — esquema de solución/contexto.
**Estado:** baseline lista; figura y narrativa se incorporan después de P4.

### 4.1.2 Arquitectura lógica de la solución

**Contenido de cierre:** estilo modular híbrido, ocho capas, 24 componentes agrupados, límites de contexto, responsabilidades, criticidad e interfaces.
**Fuente de llenado:** [A1 §§2–6](../01_Frente_Logica_Integracion/A1_CONTEXTO_Y_ARQUITECTURA_LOGICA.md); [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md), ADR-001/002.
**Recursos:** F2 y tabla `T-SD4-01`.
**Estado:** baseline lista; falta síntesis editorial y figura.

### 4.1.3 Arquitectura de integración y procesos críticos

**Contenido de cierre:** contratos, mensajería, versionado, convivencia bidireccional con TOS 2012, autoridad dominio×zona×fase, resiliencia, operación local y reconciliación.
**Fuentes de llenado:** [A2 §§1–7](../01_Frente_Logica_Integracion/A2_ARQUITECTURA_DE_INTEGRACION.md), [A3 §§2–10](../01_Frente_Logica_Integracion/A3_PROCESOS_CRITICOS_Y_TOS.md) y [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md), ADR-003/004.
**Recursos:** F3 y tabla `T-SD4-02`.
**Estado:** baseline lista; falta síntesis editorial y figura.

### 4.1.4 Datos y seguridad transversales

**Contenido de cierre:** autoridad, almacenes, flujos y retención a nivel arquitectónico; Zero Trust, capa expuesta, IAM local, cifrado, registros y SIEM.
**Fuentes de llenado:** [D1 B1–B7](../03_Frente_Seguridad_Consolidacion/D1_ARQUITECTURA_DE_SEGURIDAD.md), [D2 B1–B7](../03_Frente_Seguridad_Consolidacion/D2_AMENAZAS_ADR_Y_PUNTOS_DE_FALLA.md), A1 §§4–5 y coordinación con Subdocumento 5.
**Recursos:** F5 y tabla `V-DATA-01`.
**Estado:** baseline lista; la vista de datos se cierra con el cruce final del Subdocumento 5.

### 4.1.5 Decisiones de arquitectura y cumplimiento

**Contenido de cierre:** once ADR con alternativas, criterio, consecuencia y condición de revisión; familias del Artículo 4 y dependencias legítimas.
**Fuentes de llenado:** [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md), [MA-4](../00_Gobierno/09_REVISION_ADR_BASELINE_I1_MA4.md) y [MA-6](../00_Gobierno/11_MATRIZ_ARTICULO4_MA6.md).
**Recursos:** tablas `T-SD4-07` y `T-SD4-08`.
**Estado:** once decisiones propuestas para Informe 1; ninguna se declara aprobada.

## 4.2 Arquitectura física

### 4.2.1 Arquitectura física y emplazamiento

**Contenido de cierre:** solución híbrida, sala/edge, redes, AWS primaria y secundaria, sistemas conservados y justificación por componente conforme al Artículo 16.
**Fuentes de llenado:** [C1 §§1–9](../02_Frente_Fisica_Despliegue/C1_ARQUITECTURA_FISICA_Y_EMPLAZAMIENTO.md) y [Registro ADR](../00_Gobierno/03_REGISTRO_ADR_GLOBAL.md), ADR-005/006/011.
**Recursos:** F4 y tabla `T-SD4-03`.
**Estado:** baseline lista; falta síntesis editorial y figura.

### 4.2.2 Especificaciones de tecnologías de software

**Contenido de cierre:** frontend, backend, aplicación móvil, contratos, ejecución, datos, integración, observabilidad, IaC y sistema operativo; alternativa, modalidad, ubicación y vigencia.
**Fuentes de llenado:** [C2 §§3–4](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md) y [MA-5](../00_Gobierno/10_CONSOLIDACION_T11_MA5.md).
**Recurso:** tabla `T-SD4-04`.
**Estado:** baseline lista para síntesis.

### 4.2.3 Especificaciones de implementos de hardware y software

**Contenido de cierre:** familias, cantidades, redundancia, interfaces, ambiente y licenciamiento/servicio aplicable.
**Fuentes de llenado:** [C2 §§7–9](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C4 §§6/9/10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md), D1 `SEC-PHYS` y T-11.
**Recurso:** tabla resumen con referencia al T-11, sin repetir sus 32 filas.
**Estado:** baseline lista para síntesis.

### 4.2.4 Especificaciones del data center primario

**Contenido de cierre:** sala condicional de 34 m², tres puertas de validación y fallback, racks, servidores, RAID, red, UPS, generación, climatización, incendio, acceso, CCTV y PUE.
**Fuentes de llenado:** [C2 §5](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C4 §6.2.bis](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md) y ADR-005/007.
**Recursos:** ampliación dentro de F4 y tabla `T-SD4-05`.
**Estado:** baseline dimensionada; sala y condiciones físicas sujetas a validación del CLIENTE/site survey.

### 4.2.5 Especificaciones del data center secundario

**Contenido de cierre:** AWS `us-east-1` en activo-pasivo, réplica, IaC, copia inmutable, RTO/RPO, failover/failback y riesgo de dominio común AWS.
**Fuentes de llenado:** [C2 §6](../02_Frente_Fisica_Despliegue/C2_TECNOLOGIAS_HARDWARE_Y_DATA_CENTERS.md), [C3 §9](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md), ADR-007/011 y D2 `SPOF-22`.
**Recurso:** bloque de recuperación dentro de F4.
**Estado:** baseline definida; pruebas y mediciones son evidencia futura.

### 4.2.6 Despliegue, redes y continuidad

**Contenido de cierre:** ambientes, CI/CD, segregación, doble WAN/VPN, LTE/5G en patio, 72 h de operación local, sombra de 8 h, respaldos, HA/DR y retorno.
**Fuentes de llenado:** [C3 §§2–12](../02_Frente_Fisica_Despliegue/C3_DESPLIEGUE_RED_Y_CONTINUIDAD.md), A3 §§5–7 y D1 B3/B5/B6.
**Recursos:** F3/F5; F6 solo si P4 confirma que F3/F4 no resultan legibles.
**Estado:** baseline lista; pruebas y aceptación quedan como evidencia futura.

### 4.2.7 Dimensionamiento y plan de capacidad

**Contenido de cierre:** carga normal/punta, concurrencia, crecimiento, telemetría, buffer, almacenamiento, red, carga/PUE, márgenes y disparadores.
**Fuente de llenado:** [C4 §§3–10](../02_Frente_Fisica_Despliegue/C4_DIMENSIONAMIENTO_Y_T11.md).
**Recurso:** tabla `T-SD4-06`.
**Estado:** cálculos base completos; se publicará su síntesis y supuestos decisivos.

### 4.2.8 Formulario T-11

Se incorporará el contenido de [`02_FORMULARIO_T11_FINAL.md`](02_FORMULARIO_T11_FINAL.md): 32 filas, cinco columnas oficiales, cantidades, ubicación y justificación, sin precios.

**Estado:** baseline completa en MA-5; pendiente de maquetación en el documento final.
