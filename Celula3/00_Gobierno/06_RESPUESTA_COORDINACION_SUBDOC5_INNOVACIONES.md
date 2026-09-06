# Respuesta de coordinación — Subdocumento 5 e innovaciones

**Fecha de corte:** 2026-09-05
**Propósito:** aclarar qué puede avanzar el equipo de Datos e Innovaciones con el material disponible y qué decisiones deben esperar integración posterior.

## 1. Conclusión ejecutiva

El equipo **no está bloqueado para desarrollar el Informe 1**. Existen dependencias reales con las células 1, 2 y 3, pero afectan principalmente el refinamiento y cierre posterior, no la redacción inicial solicitada por el profesor.

La confusión proviene de tratar simultáneamente como exigibles:

1. el contenido acotado del **Informe 1**;
2. el refinamiento del **Informe 2**;
3. los costos del **Informe 3**; y
4. el detalle completo de la **Propuesta final**.

También se interpretó el archivo consolidado del Subdocumento 4, que aún dice `PENDIENTE DE INTEGRAR`, como si no existieran insumos de arquitectura. Ese archivo es el destino final de contenido aprobado; no reemplaza al Maestro ni significa que todos los equipos deban esperar.

## 2. Alcance confirmado por el profesor

Para el **Informe 1**, el Formulario T-22 exige los subdocumentos **1, 2, 3, 4, 5 y 13**.

En esta instancia, cada una de las cinco innovaciones —una por cada tipo obligatorio— debe contener solamente:

- nombre;
- idea y alcance;
- tecnología que la sustenta;
- resultado esperado; y
- declaración de investigación adicional, cuando corresponda.

No basta con presentar solamente el título, pero **todavía no se exige**:

- trazabilidad definitiva con la EDT;
- mes definitivo de materialización;
- costo, precio o valorización en flujo de caja;
- Formulario T-19 completo;
- diseño técnico final de incorporación; ni
- indicadores, riesgos y contingencias en su versión definitiva.

La progresión indicada por el profesor es:

| Instancia | Alcance exigido para innovaciones |
|---|---|
| Informe 1 | Nombre y explicación del alcance: idea, tecnología y resultado esperado |
| Informe 2 | Refinamiento y trazabilidad con arquitectura y EDT |
| Informe 3 | Costo y precio; inversión, costo operacional y beneficio en flujo de caja |
| Propuesta final | T-19 completo con los siete elementos del Artículo 29° |

La documentación administrativa de los artículos 39° y 40° corresponde únicamente a la Propuesta final y no debe consumir esfuerzo en esta entrega.

## 3. Qué pueden avanzar ahora

### 3.1 Innovaciones

Pueden terminar las cinco descripciones del Informe 1 sin esperar productos, capacidades, costos, EDT, T-11 o diagramas finales.

Para evitar el descarte conceptual del Artículo 30°, basta en esta etapa con una revisión razonable de pertinencia y no solapamiento:

- explicar qué problema concreto del caso aborda;
- indicar por qué no es solo una funcionalidad ya obligatoria;
- identificar el valor adicional esperado; y
- marcar como pendiente cualquier validación que corresponda a otra célula.

No es necesario detenerse hasta obtener una matriz firmada contra todos los RF. El corte vigente que debe usarse como referencia es **139 RF, 21 decisiones y distribución 82/57 entre Etapa 1 y Etapa 2**. Las cifras 138 y 82/56 corresponden a cortes históricos.

Tampoco es obligatorio crear RF nuevos para poder presentar las innovaciones en el Informe 1. Si posteriormente una innovación incorpora comportamiento contractual, deberá transformarse en requisitos, criterios de aceptación, trazabilidad, EDT y arquitectura durante el refinamiento.

### 3.2 Subdocumento 5

El equipo de Datos puede avanzar desde ahora en:

- dominios, entidades, relaciones y eventos;
- propietarios y fuentes de verdad;
- clasificación, calidad, linaje y retención;
- familias de persistencia y necesidades de consistencia;
- estrategia de migración y conciliación;
- separación operacional/analítica; y
- consultas, indicadores y umbrales.

Debe utilizar identificadores provisionales estables y registrar los puntos que necesitarán confirmación. No corresponde escoger silenciosamente productos, tamaños, regiones o contratos que Arquitectura todavía no ha cerrado.

## 4. Dependencias reales

Las siguientes dependencias existen, pero **no bloquean el avance actual**:

| Dependencia | Responsable principal | Qué puede hacerse mientras tanto | Cuándo bloquea realmente |
|---|---|---|---|
| Congelar nombres y límites de componentes | Célula 3, A1 | Usar los IDs vigentes del Maestro como provisionales | Al cerrar la trazabilidad definitiva del Informe 2/final |
| Emplazamiento nube/on-premise/edge | Célula 3, C1 | Expresar una hipótesis y su justificación | Al cerrar arquitectura física, capacidad y oferta |
| Producto, versión y dimensionamiento | Célula 3, C2/C4 | Definir necesidades y capacidades, no marcas ni cantidades | Al completar T-11, costos y diseño físico |
| Contratos y eventos definitivos | Célula 3, A2/A3 | Modelar eventos y flujos conceptuales | Al cerrar interfaces, sincronización y aceptación |
| Modelo de amenazas de una innovación | Célula 3, D2 | Identificar activos, datos, interfaces y riesgos preliminares | Cuando RT-26.07 aplique y se refine la incorporación |
| Validación de no solapamiento | Célula 2 + equipo de Innovaciones | Elaborar justificación breve por innovación | Antes de congelar la cartera contractual |
| Líneas base finales del Subdocumento 2 | Célula 1 | Citar directamente el Caso oficial y marcar validación | Al cerrar narrativa e indicadores definitivos |
| Calendario y EDT definitivos | Planificación transversal | Declarar que se completará en Informe 2 | Desde Informe 2, no en esta entrega |
| Costos y flujo de caja | Equipo económico | Identificar inductores cualitativos | En Informe 3 y Propuesta final |

Por tanto, el estado correcto es **avance habilitado con dependencias registradas**, no “bloqueado al 100 %”.

## 5. Respuestas puntuales a las consultas enviadas

- `CTX-REEFER`, `CTX-GATE`, `SRV-EVID`, `SRV-NOTIF`, `CTX-EMIS`, `CTX-YARD`, `DATA-TS` y `DATA-AN` son los IDs vigentes de trabajo del Maestro §6.1. Pueden usarse como provisionales hasta que A1 los congele.
- `CTX-SIM` puede plantearse provisionalmente como componente analítico en nube, sin autoridad operacional y sin competir con la autonomía local de 72 horas. A1/C1 deben ratificar el componente y su emplazamiento posteriormente.
- El STRIDE de IN-01 o IN-03 corresponde a D2 si la innovación modifica la arquitectura de seguridad. En el Informe 1 basta con declarar esa dependencia; para elaborarlo después, Innovaciones deberá proporcionar activos, datos, interfaces y flujo propuesto.
- La arquitectura exige que un tercero pueda descender desde un indicador hasta la transacción o evidencia de origen. Datos debe diseñar el linaje; Seguridad protege acceso, integridad y auditoría. La demostración final sigue pendiente.
- IN-03 no agrega hardware de terreno. Solo deberá reflejarse en T-11 si finalmente se oferta cómputo, licencia o servicio cloud separado; C4 determinará capacidad y cantidad.
- La captura de emisiones comienza en el mes 1. El desarrollo de Etapa 2 termina en el mes 18 y su producción está prevista para el mes 21. Un resultado de IN-05 en el mes 12 solo puede presentarse como prototipo o prevalidación, no como motor productivo, salvo que se modifique formalmente el plan.
- IN-02 debe conservar coherencia con la meta vigente de atención con cita cumplida **al menos 30 % más rápida**.
- Uso con guantes y bilingüismo ya son exigencias obligatorias y no deben presentarse como innovación. El codiseño con el sindicato sí puede incorporarse a la estrategia de grupos de interés y a la validación de esas exigencias.
- El dueño de la carga está agrupado provisionalmente en `ACT-AGE` junto con embarcadores, importadores/exportadores y clientes. Célula 1 debe explicitarlo en su análisis de actores si IN-01 o IN-02 le asignan una participación activa.

## 6. Fuentes base que pueden usar sin seguir ramas de trabajo

### Fuentes estables y compartibles

1. **Comunicado 6 del profesor** sobre el alcance progresivo del Informe 1 y las innovaciones.
2. **PDF oficiales FEP01, FEP02 y FEP03/Caso 06**, como fuente contractual primaria.
3. [`00_MAESTRO_CONTEXTO_ARQUITECTURA.md`](00_MAESTRO_CONTEXTO_ARQUITECTURA.md), como contrato común de arquitectura, IDs provisionales y reglas transversales.
4. [`04_GUIA_ARRANQUE_SUBDOCUMENTO_5.md`](04_GUIA_ARRANQUE_SUBDOCUMENTO_5.md), para determinar qué puede desarrollar Datos antes del cierre de Arquitectura.
5. [`05_REGISTRO_ALINEACION_CELULA2.md`](05_REGISTRO_ALINEACION_CELULA2.md), para usar el corte vigente de RF, RNF, reglas, decisiones y supuestos.

Si el equipo trabaja fuera del repositorio, se recomienda enviarle una **copia fechada de estos tres Markdown** junto con el comunicado del profesor y los PDF oficiales. No debe depender de revisar continuamente ramas ajenas.

### Archivos que no deben usar como fuente vigente por sí solos

- `90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`, porque es una plantilla de integración y no el estado completo del trabajo.
- Entregables A1–A3, C1–C4 o D1–D3 sin revisar su estado, porque son documentos de trabajo y pueden contener propuestas aún no aprobadas.
- Ramas `frente_1`, `frente_2` o `frente_3` como referencia permanente. Solo deben consultar un archivo de rama cuando su responsable publique explícitamente una versión de intercambio.
- Conteos históricos de 138 RF o distribución 82/56.

## 7. Regla práctica de coordinación

Cada equipo debe avanzar con las fuentes oficiales y el Maestro, usando la siguiente clasificación:

- **Confirmado:** proviene del profesor, las Bases o un acuerdo publicado.
- **Provisional:** permite diseñar y redactar, pero requiere ratificación posterior.
- **Pendiente de cierre:** falta una decisión externa para congelar el resultado.
- **Bloqueado:** solo cuando no es posible producir contenido útil sin inventar información.

Con esta regla, las consultas actuales son mayoritariamente **provisionales o pendientes de cierre**, no bloqueos.
