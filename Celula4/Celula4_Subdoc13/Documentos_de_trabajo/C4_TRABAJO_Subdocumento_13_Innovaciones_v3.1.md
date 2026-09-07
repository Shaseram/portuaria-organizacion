# Subdocumento 13 — Innovaciones · Cartera de cinco innovaciones y formularios T-19

> **Empresa:** Terabyte · **Caso:** 06 — Portuaria · **Licitación:** TFEP-01/2026
> **Célula:** 4 (Valentina Guzmán, Matías Reyes) · **Autor de este documento:** Matías Reyes
> **Entrega:** Informe 1 — 7 de septiembre de 2026
> **Estado:** borrador de trabajo **v2.1** · corte documental 2026-09-05
> **Ponderación del subdocumento en el Informe 1:** 17 % (BA, Formulario T-21)
> **v2.0:** incorpora el comunicado del profesor Antonio Moya sobre el alcance del Informe 1
> **v2.1:** verificación de citas normativas contra el texto de BA, BTT y Caso 06 — ver Anexo I
> **v3.0:** se incorpora el criterio de selección de la cartera (numeral 13.1.1) y **se cierra la decisión sobre la quinta innovación** (numeral 3.6)
> **v3.1:** se incorpora la respuesta de coordinación de arquitectura del 2026-09-05 — corte vigente 139 RF y 82/57, calendario de emisiones corregido, siete dependencias cerradas y dos reasignadas a Célula 4
>
> **Este es el documento de trabajo de Célula 4.** El texto que va al PDF del Subdocumento 13 está extraído aparte, en `C4_ENTREGA_Subdocumento_13_Innovaciones.md`, conforme a la regla de un archivo por subdocumento.

---

## 0. Advertencias de método antes de leer

### 0.0 Qué cambió con el comunicado del profesor · **LEER PRIMERO**

El comunicado aclara que **la exigencia sobre las innovaciones es progresiva**, y eso reduce sustancialmente lo que Célula 4 debe entregar el 7 de septiembre:

| Instancia | Qué se exige de las innovaciones |
|---|---|
| **Informe 1 — 7 de septiembre** | *«Las innovaciones sólo deben ser nombradas y explicadas en su alcance —idea, tecnología que la sustenta y resultado esperado—. No se acepta el solo título de la innovación; si alguna requiere investigación adicional, debe declararse.»* |
| Informe 2 | Refinamiento del alcance, ya trazable con la arquitectura y con la EDT |
| Informe 3 | Costo y precio del alcance, valorizado en el flujo de caja |
| **Propuesta final** | **Formulario T-19 completo**, con los siete elementos del Artículo 29° |

**Tres consecuencias directas para nosotros:**

1. **Los cinco T-19 completos NO son exigibles en el Informe 1.** El documento guía interno `informe_1_requisitos_y_estructura.md` los listaba como entregable explícito de esta entrega; el comunicado corrige esa lectura y los sitúa en la propuesta final. **Las cinco fichas de la sección 3 de este documento pasan a ser trabajo anticipado**, no entregable obligatorio del 7 de septiembre. No se descartan: son el insumo directo del Informe 2 y de la propuesta final, y demuestran que la cartera está pensada y no enunciada.
2. **Lo que sí hay que entregar el 7 de septiembre es la sección 2.0 de este documento**, que desarrolla cada innovación en idea, tecnología, alcance, forma de implementación y resultado esperado, y declara expresamente qué requiere investigación adicional. Esa es la redacción que va al PDF del Subdocumento 13.
3. **La tensión del Artículo 53° queda resuelta y ya no hay que consultarla.** El comunicado sitúa el costo y el precio de cada innovación en el Informe 3, lo que confirma el criterio que este documento ya aplicaba: en el Informe 1 no va ninguna cifra económica. La consulta que el §0.2 proponía formular deja de ser necesaria.

**Lo que el comunicado no cambia:** la pertinencia al caso sigue pesando por sobre la novedad tecnológica (Art. 30.2), y sigue sin aceptarse como innovación una funcionalidad exigida por las Bases. El trabajo de contraste contra los 139 RF de Célula 2 del numeral 13.1.3 sigue siendo el núcleo del valor de esta entrega.

### 0.1 Regla de estados

Cada punto narrativo y cada campo de cada T-19 lleva uno de estos tres estados:

| Estado | Significado |
|---|---|
| `[COMPLETADO]` | Tiene respaldo real en las Bases, en el Caso 06 o en el trabajo ya entregado por otra célula. Se cita la fuente. |
| `[PENDIENTE — falta información de Célula X]` | El vacío depende de otra célula o de un entregable posterior. Se indica cuál. |
| `[PENDIENTE — decisión propia de Célula 4]` | El vacío es nuestro: falta que Valentina y yo lo decidamos. |

Ningún campo se completó por inferencia. Donde no hubo dato real, quedó el estado y no un número inventado.

### 0.2 Separación entre lo técnico y lo económico · **resuelto por el comunicado**

El Formulario T-19 pide tres campos económicos —inversión requerida, efecto en el costo operacional y beneficio esperado cuantificado— y se entrega en el Sobre N° 2, que es la Oferta Técnica. El Artículo 53° de las BA declara inadmisible, sin evaluación posterior, la oferta que incurra en *«inclusión de información económica en la Oferta Técnica»*, y el Artículo 30.1 separa expresamente ambas dimensiones.

**El comunicado del profesor resuelve la aparente contradicción:** el costo y el precio de cada innovación corresponden al **Informe 3**, valorizados en el flujo de caja. En el Informe 1 no va ninguna cifra.

**Criterio aplicado:** en las fichas anticipadas de la sección 3, los tres campos económicos se completan de forma **cualitativa y relativa** —naturaleza del desembolso, dirección del efecto, componentes de costo— **sin cifra monetaria alguna**, y remiten al Informe 3. En el texto que va al PDF del Subdocumento 13 (sección 2.0) no aparecen en absoluto.

Coherente con la regla que Célula 3 ya fijó para el T-11: *«El Informe 1 no debe incluir precios, tarifas ni montos económicos»* (Maestro de Contexto de Arquitectura, §2.1 y §19, regla negativa 18).

### 0.3 Qué exige el T-22 para esta entrega

El T-22 exige que cada innovación esté desarrollada en **idea, tecnología, alcance, forma de implementación y resultados esperados**, y advierte que *«en ningún caso puede presentarse sólo el título de la innovación»* y que *«si alguna requiere investigación adicional, debe declararse»*.

El comunicado enuncia tres de esos cinco ejes —idea, tecnología y resultado esperado—. **La sección 2.0 cubre los cinco**, que es el conjunto mayor y satisface ambas fuentes. La declaración de investigación adicional se hace explícita en cada innovación, con esa palabra, porque el T-22 la pide por su nombre.

### 0.4 Estado del insumo de Célula 3

El consolidado de Célula 3 (`90_Consolidado/00_CONTENIDO_FINAL_SUBDOCUMENTO_4.md`) está íntegramente en `PENDIENTE DE INTEGRAR`. **Arquitectura aclaró el 2026-09-05 que ese archivo es la plantilla de integración de contenido aprobado y no el estado del trabajo**, de modo que no debe leerse como ausencia de insumos ni citarse por sí solo como fuente vigente. Sí existe, aprobado y estable, el **Maestro de Contexto de Arquitectura v1.0 (2026-09-04)**, que fija las ocho capas obligatorias y un **catálogo lógico inicial de 24 componentes** con identificadores estables (`CH-*`, `GW-*`, `CTX-*`, `SRV-*`, `INT-*`, `EDGE-*`, `DATA-*`).

**Decisión de Célula 4:** cada innovación se inserta contra esos identificadores del Maestro §6.1, que es el artefacto de arquitectura más firme que existe hoy. Cada inserción queda marcada como sujeta a confirmación de Célula 3 cuando el Frente 1 refine el catálogo. Esto satisface el RT-26.01 en el nivel de madurez posible en el Informe 1 y deja la dependencia trazada, en vez de inventar una arquitectura paralela.

---

## 1. Resumen: completado frente a pendiente

### 1.1 Cobertura del checklist narrativo del Subdocumento 13

| # | Contenido narrativo exigido | Estado |
|---:|---|---|
| 1 | Síntesis de la cartera | `[COMPLETADO]` |
| 2 | Pertinencia al Caso Portuaria | `[COMPLETADO]` |
| 3 | Diferencia entre innovación y funcionalidad obligatoria | `[COMPLETADO]` — verificada contra los 139 RF de Célula 2 |
| 4 | Inserción de cada innovación en la arquitectura | `[COMPLETADO]` contra el Maestro §6.1 · `[PENDIENTE — Célula 3]` confirmación final |
| 5 | Relación con las etapas y con el alcance | `[COMPLETADO]` para etapa · `[PENDIENTE — Célula 2]` confirmación del reparto por innovación |
| 6 | Resultados verificables esperados | `[COMPLETADO]` indicador, línea base y momento · `[PENDIENTE — Célula 4]` cuatro metas propias |
| 7 | Riesgos de adopción | `[COMPLETADO]` |
| 8 | Coherencia conjunta de la cartera | `[COMPLETADO]` |

### 1.2 Cobertura de los cinco T-19 · 17 campos × 5 fichas = 85 campos

> **Contexto tras el comunicado:** el T-19 completo se exige en la **propuesta final**, no en el Informe 1. Esta tabla mide, por lo tanto, **cuánto trabajo de la propuesta final ya está adelantado**, no una brecha de la entrega del 7 de septiembre. Los 35 campos con dependencia declarada corresponden mayoritariamente a la EDT (Informe 2) y a la valorización económica (Informe 3), que el propio calendario del comunicado sitúa después.

| Bloque de campos | Completados | Pendientes | Origen del pendiente |
|---|---:|---:|---|
| Tipo y nombre (2 × 5 = 10) | 10 | 0 | — |
| Problema, evidencia, tecnología, madurez, fuentes (5 × 5 = 25) | 24 | 1 | Célula 4 — escala de madurez de IN-04 |
| Inserción en la arquitectura (1 × 5 = 5) | 5 provisionales | 5 confirmaciones | Célula 3 |
| Paquetes de la EDT (1 × 5 = 5) | 0 | 5 | Ninguna célula — EDT es Informe 2 (T-14) |
| Mes del cronograma (1 × 5 = 5) | 5 como hipótesis | 5 confirmaciones | Célula 2 (etapa) + EDT del Informe 2 |
| Económicos (3 × 5 = 15) | 15 cualitativos | 15 valorizaciones | Informe 3 — Oferta Económica, Entregable 2 |
| Indicador, línea base y meta, momento (3 × 5 = 15) | 11 | 4 | Célula 4 — metas propias de IN-01, IN-03, IN-04, IN-05 |
| Riesgo, mitigación, contingencia (3 × 5 = 15) | 15 | 0 | — |
| **Total** | **85 campos escritos, ninguno vacío** | **35 con dependencia declarada** | — |

**Ningún campo quedó en blanco.** Los 35 con dependencia declarada tienen contenido de hipótesis explícito y trazado a su origen, conforme a la instrucción del T-22.

### 1.3 Cumplimiento de los requisitos del Capítulo 26 de las BTT

| Código | Requisito | Estado |
|---|---|---|
| `RT-26.01` | Ubicación explícita en la arquitectura: capa, componentes e interfaces | `[COMPLETADO]` provisional contra Maestro §6.1 · `[PENDIENTE — Célula 3]` |
| `RT-26.02` | Paquetes de la EDT y mes del cronograma | **No exigible en el Informe 1.** El comunicado sitúa la trazabilidad con la EDT en el Informe 2. Mes anclado al Art. 17° como hipótesis anticipada |
| `RT-26.03` | Nivel de madurez con escala declarada y fuentes en APA 7.ª ed. | `[COMPLETADO]` para IN-01, IN-02, IN-03, IN-05 · `[PENDIENTE — Célula 4]` escala de IN-04 |
| `RT-26.04` | Riesgo de adopción, probabilidad, impacto, mitigación y contingencia | `[COMPLETADO]` |
| `RT-26.05` | Indicador con línea base, meta y momento; impacto en inversión, opex y beneficio | `[COMPLETADO]` en lo verificable · **la dimensión económica se difiere al Informe 3 por instrucción expresa del comunicado**, no por omisión |
| `RT-26.06` | Innovaciones con IA cumplen íntegramente el Capítulo 18 de las BTT | `[COMPLETADO]` — ninguna de las cinco incorpora IA en su versión comprometida; IN-03 declara el gatillo |
| `RT-26.07` | Innovaciones que modifican la arquitectura de seguridad requieren modelado de amenazas propio | `[PENDIENTE — Célula 3]` — aplica a IN-01 y a IN-03 |
| `RT-26.08` | *Deseable:* al menos una innovación verificable antes del mes 16 | `[COMPLETADO]` — **IN-02**, medible en la marcha blanca de la Etapa 1 (meses 13 a 15) |

### 1.4 La cartera en una tabla

| ID | Tipo (Art. 28°) | Nombre | Inserción principal | Etapa / mes hipótesis |
|---|---|---|---|---|
| **IN-01** | 1 · Producto o servicio | Cadena de frío certificada: aviso proactivo al dueño de la carga y certificado de integridad verificable por embarque | `CTX-REEFER` → `SRV-NOTIF` → `SRV-EVID` → `CH-PORTAL` / `GW-API` | Fase A: meses 10 a 15 · Fase B: meses 19 a 21 |
| **IN-02** | 2 · Proceso | Cita convenida a tres bandas con reprogramación automática por confirmación de carga lista | `CTX-GATE` + `CH-PORTAL` + `SRV-NOTIF` | Etapa 1 · meses 8 a 15 |
| **IN-03** | 3 · Tecnología o arquitectura | Gemelo de operación del terminal: simulación de eventos discretos calibrada con telemetría real, sin autoridad operacional | `CTX-SIM` (nuevo, propuesto) alimentado por `DATA-AN` | Etapa 1 (v1) meses 6 a 12 · Etapa 2 (v2) meses 16 a 21 |
| **IN-04** | 4 · Modelo de negocio o contratación | Servicio gestionado del equipamiento de terreno con compromiso de resultado verificable, adicional al régimen del Art. 78° | No es un componente: es cláusula contractual sostenida por `CTX-EMIS`, `CTX-GATE`, `CTX-REEFER` y `RF-CON-11` | Vigente desde el mes 16 · plena en meses 21 a 56 |
| **IN-05** | 5 · Sostenibilidad | Meta de intensidad de carbono por contenedor con reducción verificada bajo la misma metodología del reporte a la alianza | `CTX-EMIS` + término de puntuación en `CTX-YARD` + `DATA-AN` | Medición Etapa 1 desde mes 1 · reducción desde mes 21 |

---

## 2. Esqueleto narrativo del Subdocumento 13

### 13.1 Criterio de selección y coherencia con el caso

#### 13.1.1 Criterio de selección: cómo se eligieron estas cinco y no otras · `[COMPLETADO]`

El Artículo 30.2 advierte que *«una innovación de alta sofisticación técnica que no resuelva un problema real del caso obtendrá menor puntaje que una innovación sencilla, bien justificada y con impacto verificable»*. Terabyte tomó esa advertencia como método de trabajo y no como recomendación. La cartera se construyó mediante **un embudo de cuatro descartes sucesivos**, aplicado en este orden.

**Primer descarte — lo que las Bases prohíben expresamente.** El Artículo 30° y el Capítulo 26 de las Bases Técnicas Transversales coinciden en la misma exclusión: no se acepta como innovación una tecnología que ya constituye estándar de la industria, una tendencia sin diseño de incorporación, ni **una funcionalidad exigida por las Bases Técnicas presentada como innovación**. Este último criterio fue el más restrictivo. Terabyte contrastó cada candidata contra los **139 requerimientos funcionales** y las **21 decisiones** del alcance ya definido, uno por uno. El resultado fue que la mayor parte de las respuestas evidentes —sistema de citas, reconocimiento óptico del contenedor en el gate, asignación algorítmica de posición, alarmas de frío con escalamiento, mensajería EDIFACT, portal de autoservicio, cálculo de emisiones por contenedor, credencial temporal de eventuales— **ya son alcance obligatorio**, y presentarlas como innovación habría sido entregar al evaluador la causal de descarte.

**Segundo descarte — las restricciones no negociables.** La Restricción N° 1 —ninguna solución puede aumentar la exposición de una persona al riesgo del patio— y la Restricción N° 11 —el área de tecnologías de información del CLIENTE son cinco personas— eliminan buena parte del catálogo tecnológico habitual de la industria: automatización de equipos de patio, vehículos guiados, realidad aumentada en cabina, inventario por vehículo aéreo. El gerente general dejó consignada en el acta del directorio la condición de que *«cualquier solución que aumente la exposición al riesgo en el patio será rechazada, por buena que sea en todo lo demás»*.

**Tercer descarte — las exclusiones explícitas del Capítulo 11.** Queda fuera toda innovación que suponga reemplazar el sistema de gestión empresarial, intervenir el control de las grúas de muelle, sustituir la videovigilancia, operar la báscula, electrificar la flota o ejecutar obra civil.

**Cuarto filtro — anclaje obligatorio a un hecho medido de este terminal.** Cada innovación que sobrevivió debe apuntar a una cifra del Capítulo 7 o a un vacío declarado del numeral 16.1. Una innovación que no pueda hacerlo no es pertinente a este caso, por buena que sea en abstracto.

**Qué quedó después del embudo.** Lo que sobrevive no son tecnologías: son **cinco huecos** entre lo que el caso exige como resultado y lo que los requerimientos cubren como conducta. Cada uno cae, además, en un tipo distinto del Artículo 28°, lo que permite componer la cartera obligatoria sin forzar ninguna pieza:

| Hueco identificado | Enunciado | Innovación | Tipo Art. 28° |
|---|---|---|---|
| **De destinatario** | El sistema avisa hacia adentro y nunca hacia afuera. La alarma de frío llega al operador y al supervisor; nadie avisa al dueño de la carga | IN-01 | 1 · Producto o servicio |
| **De proceso** | La cita existe, pero el proceso sigue suponiendo que el transportista controla cuándo estará lista la carga | IN-02 | 2 · Proceso |
| **De condición del terreno** | No existe dónde ensayar un cambio. No es un indicador: es una restricción estructural, y ningún requerimiento la atiende | IN-03 | 3 · Tecnología o arquitectura |
| **Contractual** | El CLIENTE compra el equipamiento, no tiene quién lo mantenga y su proveedor no comparte la consecuencia del indicador comprometido | IN-04 | 4 · Modelo de negocio |
| **De verbo** | Los requerimientos dicen *medir*. Ninguno dice *reducir* | IN-05 | 5 · Sostenibilidad |

> **La cartera se construyó desde el problema hacia la tecnología, y no al revés.** Ninguna de las cinco es transferible a otro caso del llamado.

#### 13.1.2 Síntesis de la cartera · `[COMPLETADO]`

Terabyte presenta cinco innovaciones, una por cada tipo obligatorio del Artículo 28° de las Bases Administrativas. Las cinco comparten un mismo criterio de selección: **no proponen tecnología que el terminal no pueda operar con cinco personas de TI, y no proponen nada que obligue a una persona a atender un dispositivo mientras hay equipos en movimiento en el patio.** Ese doble filtro —Restricción no negociable N° 11 y Restricción no negociable N° 1 del Capítulo 10 del Caso 06— descartó antes de empezar la mayor parte del catálogo de tecnologías de moda de la industria.

Las cinco atacan, en este orden, las cinco heridas que el propio mandante dimensionó en el Capítulo 7:

1. **IN-01** actúa sobre la pérdida de frío: el evento del 18 de febrero de 2026 costó US$ 620.000, 38 contenedores y nueve horas sin energía, y hoy el terminal no puede entregar registro continuo de temperatura como evidencia de cadena de frío.
2. **IN-02** actúa sobre la estadía del camión: 78 minutos contra 45 comprometidos, tres semestres consecutivos sobre el umbral y una fila de 3,2 km con 140 camiones el 12 de marzo de 2026.
3. **IN-03** actúa sobre una restricción que no es un indicador sino una condición del terreno: entre el 15 de diciembre y el 30 de abril está prohibido intervenir, no hay ventana durante las 620 recaladas anuales ni en las cuatro horas previas, y el patio opera al 90 % en temporada. **No existe dónde ensayar un cambio.**
4. **IN-04** actúa sobre la asimetría contractual: el CLIENTE compra el hardware, tiene cinco personas de TI y arrastra indicadores comprometidos con el concedente cuyo incumplimiento ya lleva tres semestres.
5. **IN-05** actúa sobre la tercera condición de la alianza naviera para 2029 —el reporte verificado de emisiones— que hoy tiene línea base literal: *«no se mide»*.

**Fuente:** Caso 06, Cap. 7.1, 7.2 y 7.3 (indicadores del problema); Cap. 10, restricciones 1, 9, 10 y 11; Cap. 13.2 (hitos externos).

#### 13.1.3 Pertinencia al Caso Portuaria · `[COMPLETADO]`

El Artículo 30.2 de las Bases Administrativas es explícito: *«El CLIENTE valorará especialmente la pertinencia al caso por sobre la novedad tecnológica en abstracto. Una innovación de alta sofisticación técnica que no resuelva un problema real del caso obtendrá menor puntaje que una innovación sencilla, bien justificada y con impacto verificable.»* El Capítulo 19 del Caso 06 lo repite en sus propias palabras: *«Que las cinco innovaciones sean pertinentes a la operación portuaria y a los problemas de este terminal, y no un catálogo de tecnologías de moda. Que la de sostenibilidad se articule con la exigencia concreta de la alianza naviera y no con una declaración general.»*

Por eso, ninguna de las cinco innovaciones de esta cartera es transferible a otro caso del llamado. Cada una está anclada a un hecho de este terminal: el evento del 18 de febrero, el transportista que no controla cuándo estará lista su carga, el congelamiento estacional de cuatro meses y medio, las cinco personas de TI, y la fecha de 2029 con el 34 % de los contenedores.

La quinta —IN-05— se articula deliberadamente con la exigencia concreta de la alianza naviera, tal como pide el Capítulo 19, y no con una declaración ambiental general.

#### 13.1.4 Diferencia entre innovación y funcionalidad obligatoria · `[COMPLETADO]`

El Artículo 30° de las BA y el Capítulo 26 de las BTT prohíben lo mismo, con la misma frase: *«No se aceptará como innovación: la sola adopción de una tecnología que ya constituye estándar de la industria; la mención de una tendencia sin diseño de incorporación; ni una funcionalidad exigida por las Bases Técnicas presentada como innovación.»*

Célula 4 aplicó ese filtro de forma verificable: **cada innovación candidata se contrastó contra los 139 requerimientos funcionales vigentes del catálogo de Célula 2 y contra las 21 decisiones del registro de supuestos v3.** El resultado del contraste se declara aquí, requerimiento por requerimiento, para que la Comisión pueda verificarlo:

| Innovación | Requerimiento obligatorio más próximo | Qué obliga ese requerimiento | Qué agrega la innovación |
|---|---|---|---|
| **IN-01** | `RF-REF-08`, `RF-REF-11`, `RF-REF-12` | Notificar la alarma **al operador de turno y a un supervisor de guardia**; mantener la serie continua; permitir **descargar** la serie por autoservicio | El destinatario del aviso pasa a ser **el dueño de la carga**, que hoy no recibe nada; y la serie deja de ser un archivo descargable para convertirse en un **certificado sellado, verificable por un tercero sin depender del terminal**, ofrecido como servicio con nivel de servicio propio |
| **IN-02** | `RF-GAT-01`, `RF-GAT-02`, `RF-GAT-16`, Decisión N° 6 | Solicitar cita; priorizar a quien la cumple; limitar franjas por capacidad declarada; cola virtual que avisa al transportista **cuando el terminal se atrasa** | Incorpora al **dueño de la carga como tercera parte de la cita** y reprograma la franja automáticamente cuando confirma disponibilidad. Resuelve la mitad de la Decisión Pendiente N° 6 del numeral 16.1 que ninguna decisión resolvió: *«qué ocurre con el transportista que no controla cuándo estará lista la carga»* |
| **IN-03** | `RF-NAV-05`, `RF-GAT-16` | Estimar la duración de la nave a partir de serie histórica; limitar franjas por **capacidad declarada** | Ningún requerimiento dice **de dónde sale** la capacidad declarada ni permite ensayar un cambio de política antes de aplicarlo en producción. IN-03 provee el banco de ensayo fuera de línea. No existe requerimiento de simulación en el catálogo |
| **IN-04** | Ninguno | — | El catálogo no contiene ningún requerimiento sobre esquema contractual ni sobre modelo de remuneración. IN-04 no compite con ningún RF |
| **IN-05** | `RF-EMI-01` a `RF-EMI-06` | **Medir** el consumo, **calcular** la emisión por contenedor, **trazar** el cálculo, **acumular** la serie y **obtener** el reporte verificado | Ningún requerimiento obliga a **reducir**. IN-05 compromete una meta de intensidad —kg CO₂e por contenedor movilizado— y actúa sobre remociones evitadas, ralentí y asignación preferente de los dos equipos eléctricos existentes |

**Fuente:** Célula 2, `Catalogo rf definitivo parte1/2/3.md` (139 RF vigentes: 82 en Etapa 1 y 57 en Etapa 2) y `Registro_supuestos_v3.md`, bloque A (21 decisiones).

#### 13.1.5 Coherencia conjunta de la cartera · `[COMPLETADO]`

Las cinco no son cinco iniciativas sueltas. Comparten infraestructura y se sostienen unas a otras:

- **IN-03 alimenta a IN-02.** El gemelo es lo que produce la «capacidad declarada» de franjas que exige `RF-GAT-16` y lo que permite verificar, antes de tocar el gate real, si la reprogramación a tres bandas mejora o empeora la fila.
- **IN-01 e IN-05 comparten la misma cadena de evidencia.** Ambas dependen de `SRV-EVID` y de la trazabilidad hasta el dato de origen; una la usa para temperatura, la otra para emisiones. El sellado se construye una vez.
- **IN-04 depende de que IN-02 e IN-05 sean medibles.** Un compromiso de resultado solo es defendible si el indicador que lo verifica lo produce el propio sistema de forma trazable y reproducible por un tercero, que es exactamente lo que exige `RF-CON-11` —producción trazable de los indicadores del concedente— y la Restricción no negociable N° 14.
- **Ninguna de las cinco toca el control de grúas de muelle, la emisión tributaria del ERP, el VMS ni la báscula.** Las cuatro exclusiones del Capítulo 11 del Caso 06 se respetan íntegramente.
- **Ninguna de las cinco añade una interacción del operador en el patio.** IN-05 opera como término de puntuación dentro de un algoritmo que ya asigna; IN-03 no tiene autoridad operacional; IN-01 e IN-02 actúan sobre canales externos. La Restricción no negociable N° 1 se respeta por diseño, no por declaración.

#### 13.1.6 Relación con las etapas y con el alcance · `[COMPLETADO]` parcial

El reparto por etapas sigue el que ya fijó Célula 2 para los requerimientos que cada innovación aprovecha, y el cronograma contractual obligatorio de 56 meses del Artículo 17° de las BA:

| Fase contractual | Meses | Qué de la cartera ocurre allí |
|---|---|---|
| Etapa 1 · Desarrollo | 1 a 12 | IN-05 inicia captura de consumo desde el mes 1 (`RF-EMI-05`); el cálculo de intensidad existe aquí solo como prototipo y prevalidación. IN-03 v1 se construye con los meses 6 a 12. IN-02 se construye sobre el gate de Etapa 1. IN-01 fase A depende del despliegue de instrumentación reefer de Etapa 1 |
| Etapa 1 · Marcha blanca | 13 a 15 | **IN-02 se mide aquí** — cumple el `RT-26.08` deseable. IN-01 fase A opera con aviso por canal directo |
| Etapa 1 · Producción | 16 | IN-04 entra en vigencia contractual con la primera medición oficial |
| Etapa 2 · Desarrollo | 13 a 18 | IN-01 fase B (certificado autenticado por portal, que depende de `RF-POR-02`, de Etapa 2). IN-03 v2 |
| Etapa 2 · Marcha blanca | 19 a 20 | IN-01 fase B en convivencia |
| Etapa 2 · Producción | 21 | IN-05 entra con motor de cálculo productivo y activa el término de reducción. IN-04 en régimen pleno |
| Operación | 21 a 56 | Las cinco en régimen; IN-05 acumula la trayectoria que se presenta a la alianza en 2029 |

`[PENDIENTE — falta información de Célula 2]`: confirmación de que el reparto por etapa de cada innovación no altera el reparto 82/57 ya cerrado, y decisión sobre si cada innovación debe generar requerimientos funcionales propios en el catálogo o si se documenta solo aquí.

`[PENDIENTE — falta información de ninguna célula en esta etapa]`: la asignación a paquetes de la EDT y las fechas finas dependen del Subdocumento 7 y del Formulario T-14, que corresponden al Informe 2. Ninguna célula los ha producido todavía.

### 13.2 a 13.6 · Las cinco innovaciones — **texto exigible en el Informe 1**

> Cada innovación se desarrolla en los cinco ejes del T-22 —idea, tecnología que la sustenta, alcance, forma de implementación y resultado esperado— y cierra con la declaración de investigación adicional que el mismo T-22 exige. **Este es el texto que va al PDF del Subdocumento 13.** Las fichas T-19 de la sección 3 son trabajo anticipado para el Informe 2 y la propuesta final, no entregable del 7 de septiembre.

---

#### 13.2 Innovación de producto o servicio — Cadena de frío certificada Aconcagua

**Idea.** Hoy, cuando una toma refrigerada falla, el terminal se avisa a sí mismo. El exportador cuya fruta está en esa toma no se entera. Y cuando la carga llega a destino, el terminal no puede entregar el registro continuo de temperatura que los mercados exigen como evidencia de cadena de frío: hoy ese registro sencillamente no existe. La innovación convierte la instrumentación que el proyecto instalará de todos modos en **un servicio con dos caras nuevas**: el aviso llega al dueño de la carga en el momento en que ocurre la desviación, y la serie de temperatura se entrega como un certificado sellado que un tercero puede verificar por su cuenta, sin pedirle nada al terminal.

**Tecnología que la sustenta.** Tres piezas, ninguna experimental. La cadena de eventos de temperatura por contenedor se **sella mediante registro encadenado por hash**, se firma electrónicamente y recibe **sello de tiempo conforme a RFC 3161**, de modo que la fecha y la integridad son demostrables sin acceso a los sistemas del terminal. La pertenencia de un registro individual a la serie sellada se demuestra mediante **estructura de árbol de Merkle**, siguiendo el patrón de registro auditable de RFC 6962, sin exponer el resto de la serie. El aviso externo viaja por los adaptadores de canal por audiencia que la solución ya contempla, con confirmación de recepción registrada. La firma reutiliza el servicio transversal de firma electrónica que la solución ya construye para los cuatro actos obligatorios: **no se agrega ninguna plataforma criptográfica nueva.**

**Alcance.** Cubre los contenedores refrigerados conectados a tomas instrumentadas. Se despliega en dos fases: primero el aviso proactivo por canal directo, y después el certificado descargable con usuario autenticado, porque el registro y la verificación de identidad de clientes externos pertenecen a la Etapa 2 del alcance definido por Célula 2. **No cubre** la carga seca, ni la temperatura durante el transporte marítimo, ni sustituye el registro del propio equipo refrigerado del contenedor.

**Forma de implementación.** Se apoya íntegramente en componentes que el alcance obligatorio ya construye: el contexto de reefer y telemetría genera el evento; el servicio de evidencia y firma lo sella; el servicio de notificaciones lo emite por el adaptador que corresponda a cada audiencia; el portal y la puerta de enlace de servicios entregan el certificado y exponen el punto público de verificación. Al abrir una nueva superficie de exposición externa, requiere modelado de amenazas propio conforme al `RT-26.07` de las Bases Técnicas Transversales, que Célula 3 deberá producir.

**Resultado esperado.** Que una desviación de temperatura llegue a alguien que tenga interés propio en que se resuelva, en cualquiera de los tres turnos —que es exactamente lo que faltó la madrugada del 18 de febrero de 2026, cuando la pérdida fue de US$ 620.000 en 38 contenedores durante nueve horas—, y que el terminal pueda ofrecer evidencia de cadena de frío como atributo de su servicio, en una operación donde entre enero y marzo se concentra el 62 % del volumen refrigerado del año. El Caso registra la consecuencia comercial de no tenerla en cuatro palabras: tras la pérdida del 18 de febrero, **«el exportador no volvió»**.

**Investigación adicional declarada.** Requiere levantar con al menos un exportador y una autoridad qué formato de certificado es efectivamente aceptado en los mercados de destino de la fruta chilena; sin esa validación, el certificado puede ser técnicamente correcto y comercialmente inútil. La meta del indicador se fijará una vez conocido ese formato.

---

#### 13.3 Innovación de proceso — Cita convenida a tres bandas

**Idea.** Un sistema de citas para camiones ordena las llegadas, pero no cambia el hecho que las desordena. Lo dijo con todas sus letras Hernán Cifuentes Palma, gerente general de una empresa de transporte terrestre cuyo 30 % de operación pasa por este terminal, en la entrevista de levantamiento:

> *«Yo no controlo cuándo está lista la carga. El packing me llama y me dice "ya, ven". Si me dan una cita a las diez y la fruta está a las tres, la cita no sirve y voy a llegar igual a las tres. […] si van a hacer citas, tienen que ser citas que se puedan cambiar y que consideren que la mitad de mi operación no depende de mí.»*

Pedirle una hora al transportista es pedirle una promesa que no depende de él, y el propio Caso dejó esa pregunta explícitamente sin resolver en su lista de decisiones pendientes. La innovación cambia el proceso de negocio: la cita deja de ser una solicitud del transportista y pasa a ser **un acuerdo de tres partes** —dueño de la carga, transportista y terminal— en el que la franja **se puede cambiar sola**, porque se reprograma automáticamente cuando el dueño de la carga confirma que la carga está efectivamente disponible. Es, literalmente, la cita que el transportista pidió.

**Tecnología que la sustenta.** No es una tecnología nueva, y el Artículo 28° admite expresamente que una innovación de proceso lo sea. Es un rediseño con cuatro movimientos: la reserva se asocia a una unidad de carga y no solo a una patente; el dueño de la carga confirma disponibilidad por el portal o por integración, y esa confirmación es la que libera la franja; si la confirmación no llega dentro del plazo declarado, el sistema **reprograma automáticamente** a la siguiente franja compatible y avisa a las tres partes; la franja liberada se reasigna, de modo que la capacidad del gate no se pierde. El incentivo se mantiene positivo y sin multa: quien cumple obtiene prioridad de atención.

**Alcance.** Aplica a los movimientos de retiro y recepción coordinados con un dueño de carga identificable —exportador, importador, agencia o depósito—. **No aplica** a movimientos sin contraparte externa identificable, que siguen el flujo de cita simple. **No introduce penalización**, y esa decisión también viene de la entrevista: *«Si me penalizan por no cumplir una cita que nunca pude cumplir, en dos semanas nadie va a usar el sistema.»*

**Forma de implementación.** El contexto de gate y citas incorpora el estado «franja condicionada a confirmación» y la regla de reprogramación; el portal expone la confirmación al dueño de la carga; el servicio de notificaciones avisa a las tres partes por los adaptadores ya previstos. Se suma un rol externo a la matriz de autorización del servicio de identidad. No modifica la arquitectura de seguridad.

**Resultado esperado.** Atacar la estadía del camión —78 minutos contra los 45 comprometidos con el concedente, con tres semestres consecutivos sobre el umbral— por una vía distinta de la que atacan los requerimientos obligatorios: en vez de acelerar la atención dentro del terminal, **evitar que el camión salga a la ruta antes de que su carga esté lista**. Es la innovación con la que Terabyte cumple el `RT-26.08`, que valora que al menos una sea verificable durante la marcha blanca de la Etapa 1, antes del mes 16.

**Investigación adicional declarada.** La variante de tres partes con reprogramación automática **no está documentada en la literatura arbitrada revisada**; lo que está documentado es el mecanismo base de los sistemas de cita. Se declara como adaptación de una práctica madura a una condición no resuelta de este caso, y no como tecnología probada. Requiere además levantar con transportistas y exportadores el plazo realista de confirmación.

---

#### 13.4 Innovación tecnológica o de arquitectura — Gemelo de operación del Terminal Aconcagua

**Idea.** En este terminal **no existe dónde ensayar un cambio.** Está prohibido intervenir entre el 15 de diciembre y el 30 de abril; está prohibido intervenir durante la atención de una nave y en las cuatro horas previas a una ventana confirmada, con 620 recaladas al año; el patio opera al 90 % en temporada y la operación es 24x7x365 sin ventana de detención. Toda decisión operacional relevante se toma hoy sin poder probarla, y se prueba en producción con una nave amarrada. La innovación es **un banco de decisiones fuera de línea**: un modelo del terminal, calibrado con la telemetría que el propio proyecto instala, donde el cambio se ensaya antes de tocar la operación.

**Tecnología que la sustenta.** Simulación de eventos discretos del ciclo completo —llegada de camión, gate, asignación de posición, movimiento de patio, tractocamión, grúa de muelle, ventana de nave—, **calibrada contra la telemetría real** de equipos y los eventos de gate que la solución produce de todos modos. La calibración es lo que lo distingue de un modelo de escritorio: el gemelo se contrasta contra la operación observada y **declara su error junto a cada resultado**. En su versión comprometida **no incorpora inteligencia artificial**; si se incorporara, quedaría sujeta íntegramente al Capítulo 18 de las Bases Técnicas Transversales, conforme al `RT-26.06`.

**Alcance.** Versión 1: gate y flujo del camión. Versión 2: patio, nave y planificación. **Restricción de alcance que es parte de la innovación: el gemelo no tiene autoridad operacional.** No expone ninguna interfaz de escritura hacia los contextos operacionales, no emite órdenes y su indisponibilidad no degrada ninguna función. Se despliega en nube y nunca en el borde, precisamente para no competir por la capacidad local que sostiene las cinco funciones críticas durante las 72 horas sin enlace.

**Forma de implementación.** Componente nuevo, alimentado exclusivamente desde la capa analítica y desde las series temporales de telemetría. Requiere que Célula 3 lo dé de alta en el catálogo de componentes y justifique su emplazamiento conforme al Artículo 16° de las BA. La interdicción de escritura se verifica en la matriz de segregación de funciones del servicio de identidad, de modo que sea auditable y no una declaración.

**Resultado esperado.** Tres cosas concretas. Que cada cambio de política de patio o de gate que hoy solo puede probarse con una nave amarrada pase a probarse en el modelo. Que la «capacidad declarada» que limita las franjas de cita —un parámetro que los requerimientos exigen pero cuyo origen ninguno define— tenga por fin un fundamento. Y que la pregunta del Caso sobre qué componente se satura primero en el peak y ante la eventual incorporación de un cuarto sitio entre 2030 y 2032 se responda con un modelo en vez de con una opinión.

**Investigación adicional declarada.** El nivel de madurez se declara como **rango, TRL 6 a 7 en la escala ISO 16290:2013**, y no como valor único, porque depende de la calidad de la calibración, que a su vez depende de instrumentación que hoy no existe: solo 12 de los 18 equipos de patio tienen terminal montada. La meta de error del gemelo no puede fijarse antes de conocer la densidad real de la telemetría instalada.

---

#### 13.5 Innovación de modelo de negocio o contratación — Servicio gestionado del equipamiento de terreno con compromiso de resultado

**Idea.** El caso plantea una asimetría que ningún requerimiento funcional puede resolver, porque no es técnica sino contractual. El CLIENTE **compra el hardware pero no tiene quién lo mantenga**: el proponente especifica qué comprar, el CLIENTE lo adquiere, y su área de TI son cinco personas en un operador de importancia vital. Ese equipamiento va además a un ambiente que lo destruye —atmósfera salina, corrosión acelerada, a menos de 300 metros del mar—, y las Bases exigen que su plan de reposición esté costeado. La innovación es que **Terabyte gestione el ciclo de vida completo de ese equipamiento como servicio**, y que asuma un compromiso de resultado verificable sobre indicadores que hoy nadie garantiza.

**Tecnología que la sustenta.** Contratación basada en desempeño, aplicada con dos componentes acoplados. Primero, un **servicio gestionado de ciclo de vida del equipamiento de terreno**: monitoreo de estado, mantención preventiva, reposición por corrosión e inventario de repuestos, sobre equipamiento que permanece en el patrimonio del CLIENTE. Segundo, un **compromiso de resultado sobre indicadores que el propio sistema produce de forma trazable**, con dos salvaguardas de diseño: ningún indicador comprometido puede calcularse con un dato que Terabyte produzca sin evidencia reproducible por un tercero, y el compromiso recae sobre lo que Terabyte controla.

**Alcance — y su límite frente a las Bases.** El compromiso se refiere a **indicadores que el Artículo 78° de las BA no cubre**: disponibilidad del equipamiento de terreno instrumentado —tomas, tableros y equipos móviles— y continuidad de la instrumentación en ambiente marino. El Artículo 78° regula disponibilidad del servicio, tiempos de respuesta y resolución, MTTR, cambios fallidos, cumplimiento de RPO y RTO, vulnerabilidades, reincidencia y satisfacción; **no regula el equipamiento de terreno del CLIENTE**. La innovación **se suma** al régimen de niveles de servicio del Artículo 78° y al régimen de multas del Artículo 80° —que las Bases ya fijan con topes y procedimiento— y **en ningún caso los reemplaza, los rebaja ni propone un esquema alternativo**. Esta delimitación es deliberada: el Artículo 53° declara inadmisible la oferta *«condicionada, con reservas, alternativas no solicitadas o sujeta a contrapropuesta de las Bases»*, y una innovación de modelo de contratación que reescribiera el régimen contractual del pliego caería en esa causal.

**Forma de implementación.** No es un componente de software. Su viabilidad descansa en la cadena de evidencia que la solución ya construye: el cálculo trazable de la estadía, la evidencia de alarma y confirmación de frío, la emisión trazable hasta el dato de origen y la producción trazable de los indicadores del concedente. La medición se realiza sobre la plataforma de observabilidad, cuyos datos el Artículo 79° ya obliga a poner a disposición del CLIENTE en tiempo real y de forma exportable.

**Resultado esperado.** Que la Restricción no negociable N° 11 —*«toda función que requiera un especialista dedicado que la compañía no tiene debe ofrecerse como servicio y estar costeada»*— se cumpla en su letra y no en abstracto; que el plan de reposición del equipamiento en atmósfera marina que la Restricción N° 12 exige sea exigible a alguien; y que el proveedor comparta la consecuencia de un indicador que el terminal lleva tres semestres consecutivos incumpliendo ante su concedente.

**Investigación adicional declarada.** Falta definir el conjunto exacto de indicadores comprometidos y el momento de activación, y falta resolver el problema de atribución: la estadía del camión depende de factores que Terabyte no controla —volumen comercial, ocupación del patio, comportamiento del transportista—, de modo que el compromiso debe recaer sobre indicadores de disponibilidad y de comportamiento del sistema, con un mecanismo declarado de exclusión por causas ajenas documentadas. **Falta además decidir qué escala de madurez se declara**, o si corresponde declarar que el `RT-26.03` no le aplica por no ser una innovación de base tecnológica, que es la condición que ese requisito establece.

---

#### 13.6 Innovación de sostenibilidad — Intensidad de carbono comprometida

**Idea.** La alianza naviera impuso tres condiciones para 2029, y una es el reporte verificado de emisiones. El alcance obligatorio resuelve la mitad del problema: medir, calcular por contenedor, trazar hasta el dato de origen, acumular la serie y obtener el reporte verificado. **Pero medir no es reducir.** Lo que la alianza recibiría en 2029, si el proyecto solo cumple lo obligatorio, es una cifra sin trayectoria. La innovación es comprometer una **meta de intensidad de carbono** —kilogramos de CO₂ equivalente por contenedor movilizado— y reducirla con la misma metodología que el verificador va a auditar.

**Tecnología que la sustenta.** La misma norma del reporte obligatorio, usada como instrumento de gestión y no solo de reporte: **ISO 14083:2023** como norma de cuantificación, implementada operativamente mediante el **GLEC Framework v3.2** y verificada por tercero acreditado bajo **ISO 14064-3**, que es la jerarquía normativa que el equipo ya adoptó. Sobre esa base, tres palancas concretas: **remociones evitadas** —cada remoción es un movimiento que quema combustible sin trasladar carga, y hoy son el 18 % de los movimientos de patio—; **ralentí de tractocamiones**, derivado de la telemetría de consumo que la solución instala de todos modos en los 16 equipos diésel, sin sensor adicional; y **asignación preferente de los dos equipos eléctricos existentes** a los ciclos de mayor intensidad de emisión.

**Alcance.** Cubre las emisiones de alcance 1 y 2 atribuibles a los movimientos de contenedores dentro del terminal, con el alcance 3 explicitado. **No electrifica la flota**, respetando la exclusión expresa del Caso, y **no compromete emisión absoluta sino intensidad por contenedor**, precisamente para que la meta no dependa del volumen comercial, que el terminal no controla.

**Forma de implementación.** El contexto de energía y emisiones incorpora el motor de intensidad y la trayectoria contra meta; el contexto de patio incorpora un **término de puntuación de emisiones dentro del algoritmo de asignación que ya existe**, con peso configurable y tope declarado. Dos restricciones de diseño son parte de la innovación: el término de emisiones **nunca desplaza** una restricción de seguridad, una regla de segregación de mercancías peligrosas ni una ventana de nave comprometida; y **no agrega ninguna interacción del operador**, con lo que la Restricción no negociable N° 1 se respeta por construcción y no por declaración.

**Resultado esperado.** Que el terminal llegue a 2029 ante el 34 % de sus contenedores no con una cifra sino con una trayectoria de reducción verificada bajo la misma norma; que cada exportador y cada naviera reciban el dato de emisión atribuido a su embarque, utilizable en su propio inventario de alcance 3; y que las remociones evitadas y el ralentí eliminado se traduzcan en combustible no comprado. Responde además a la objeción que la gerenta comercial dejó registrada: *«si empezamos la mensajería y las emisiones el 2028, no llegamos, porque un reporte de emisiones verificado necesita serie de datos previa»*.

**Investigación adicional declarada.** La captura de consumo comienza en el mes 1, pero **el motor de cálculo productivo entra con la producción de la Etapa 2, en el mes 21**; lo que exista antes es prototipo y prevalidación metodológica con el verificador, y así se declara. **La meta de reducción no puede fijarse hoy y no se finge que sí.** La línea base del Caso es literal: las emisiones por contenedor «no se miden». No existe porcentaje de reducción comprometible contra una línea base inexistente. Terabyte compromete, en su lugar, **declarar la línea base como entregable verificable y fijar la meta en ese momento, con acuerdo del verificador acreditado**. Falta además someter tempranamente al verificador el método de atribución del consumo al contenedor individual, que es el punto donde un verificador puede objetar.

### 13.7 Trazabilidad conjunta de las innovaciones

#### 13.7.1 Resultados verificables esperados · `[COMPLETADO]` parcial

| ID | Indicador de verificación | Línea base | Meta | Momento de medición |
|---|---|---|---|---|
| IN-01 | Porcentaje de embarques refrigerados con certificado emitido y verificable; tiempo entre la desviación y el aviso recibido por el dueño de la carga | Cero: hoy el dueño de la carga no recibe aviso alguno y no existe registro continuo entregable (Caso 06, Cap. 7.2) | `[PENDIENTE — Célula 4]` | Marcha blanca Etapa 1 (fase A) y Etapa 2 (fase B) |
| IN-02 | Porcentaje de citas cumplidas dentro de ventana sobre citas otorgadas; porcentaje de reprogramaciones originadas por confirmación del dueño de la carga | Cero: no existe sistema de citas (Caso 06, Cap. 7.3) | `[PENDIENTE — Célula 4]`, coordinada con la meta 14 de Célula 2 (prioridad ≥ 30 % más rápida) | Semanal durante la marcha blanca de Etapa 1, meses 13 a 15 |
| IN-03 | Número de cambios de política de patio o de gate ensayados en el gemelo antes de aplicarse en producción; error del gemelo contra la operación real en estadía de camión y movimientos por hora | Cero: no existe capacidad de ensayo | `[PENDIENTE — Célula 4]` | Calibración al cierre de desarrollo de Etapa 1; error medido en cada marcha blanca |
| IN-04 | Porcentaje de indicadores comprometidos alcanzados en el período; disponibilidad del equipamiento de terreno gestionado | 71 % de cumplimiento de ventana de atraque; tres semestres de estadía sobre umbral (Caso 06, Cap. 7.1 y 7.3) | `[PENDIENTE — Célula 4]` | Semestral, alineado al informe de indicadores al concedente |
| IN-05 | Intensidad de carbono en kg CO₂e por contenedor movilizado, calculada conforme a ISO 14083:2023 e implementada con GLEC Framework v3.2 | **No se mide** (Caso 06, Cap. 7.3, literal) | `[PENDIENTE — Célula 4]` — no se puede fijar meta de reducción sin la primera serie real | Primera medición al cierre de desarrollo de Etapa 1; trayectoria anual; verificación bajo ISO 14064-3 antes de 2029 |

> **Por qué cuatro metas quedan pendientes y no se inventan.** El Capítulo 18 del Caso 06 obliga al proponente a *«proponer la meta cuando este documento no la fije»*. Célula 2 ya aplicó ese criterio con rigor y documentó, meta por meta, la evidencia que la sostiene e incluso la evidencia adversa. Fijar aquí cuatro metas sin ese trabajo produciría números que no resistirían la defensa técnica. La meta de IN-05 es además estructuralmente imposible de fijar hoy: la línea base es «no se mide», de modo que la reducción porcentual solo puede comprometerse contra la primera serie real. Esto se declara como tal, que es lo que el propio Caso pide.

#### 13.7.2 Riesgos de adopción de la cartera · `[COMPLETADO]`

Además del riesgo propio de cada ficha, la cartera tiene tres riesgos comunes que conviene declarar juntos:

1. **Riesgo de dependencia de terceros.** IN-01 e IN-02 requieren que un actor externo —el dueño de la carga— haga algo que hoy no hace. La adopción no depende del ADJUDICATARIO. Es el mismo modo de falla que Giuliano y O'Brien (2007) documentaron en Los Ángeles y Long Beach con adopciones de 5 a 30 %, y que Célula 2 ya incorporó como evidencia adversa en su meta 14.
2. **Riesgo de ventana.** Cuatro de las cinco innovaciones se materializan en meses que el congelamiento estacional puede desplazar. El Caso 06 prohíbe intervenir entre el 15 de diciembre y el 30 de abril, durante la atención de una nave y en las cuatro horas previas a una ventana confirmada.
3. **Riesgo de exigibilidad contractual.** El Artículo 30.3 de las BA advierte que *«las innovaciones comprometidas en la propuesta adjudicada forman parte del alcance contractual y son exigibles como cualquier otro requerimiento. Su omisión durante la ejecución será tratada como incumplimiento del alcance»*. Cada ficha declara por eso un plan de contingencia que degrada a la funcionalidad obligatoria sin dejar un compromiso incumplido.

---

## 3. Los cinco formularios T-19 — **trabajo anticipado, no entregable del 7 de septiembre**

> **Leer con el §0.0 a la vista.** El comunicado del profesor sitúa el T-19 completo en la **propuesta final**, no en el Informe 1. Estas cinco fichas se conservan porque son el insumo directo del Informe 2 —refinamiento del alcance, trazable con arquitectura y EDT— y del Informe 3 —valorización—, y porque demuestran que la cartera está pensada y no enunciada. **Ninguna de ellas va al PDF del 7 de septiembre.**
>
> Estructura de campos conforme al Formulario T-19 de las Bases Administrativas (17 campos) y a los siete elementos del Artículo 29°.

---

### T-19 · IN-01

| Campo | Contenido | Estado |
|---|---|---|
| **Tipo de innovación (1 a 5)** | **1 — Producto o servicio** | `[COMPLETADO]` BA, Art. 28°, tipo 1 |
| **Nombre de la innovación** | **Cadena de frío certificada Aconcagua: aviso proactivo al dueño de la carga y certificado de integridad verificable por embarque** | `[COMPLETADO]` |
| **Problema u oportunidad del caso que resuelve** | El terminal detecta una falla de frío y avisa hacia adentro, nunca hacia afuera. El dueño de la carga —el exportador de fruta cuya mercancía está en la toma— se entera cuando el daño ya ocurrió. Además, el terminal no puede entregar el registro continuo de temperatura que los mercados de destino exigen como evidencia de cadena de frío, de modo que su producto comercial queda incompleto justo donde el cliente lo exige. El Caso registra la consecuencia en cuatro palabras: tras la pérdida del 18 de febrero, **«el exportador no volvió»**. La oportunidad es convertir la instrumentación que el proyecto instalará de todos modos en un **servicio vendible y diferenciador**, no en un costo interno. | `[COMPLETADO]` Caso 06, Cap. 7.2; Cap. 9.5; Cap. 12, materia «Cadena de frío»; Cap. 1 («el exportador no volvió») |
| **Evidencia o dato que dimensiona el problema** | Registro continuo de temperatura entregable como evidencia de cadena de frío: **inexistente**. Tomas con instrumentación remota: **0 de 2.400**. Tableros con alarma remota: **0 de 26**. Intervalo de control actual: **4 horas, mediante ronda a pie con planilla**. Evento del 18 de febrero de 2026: **US$ 620.000, 38 contenedores, 9 horas sin energía**. Entre enero y marzo se concentra el **62 %** del volumen refrigerado del año. | `[COMPLETADO]` Caso 06, Cap. 7.2 y Cap. 13.2 |
| **Tecnología, práctica o modelo que la sustenta** | Tres piezas concretas, ninguna genérica: **(a)** cadena de eventos de temperatura por contenedor sellada mediante registro encadenado por hash, firmada electrónicamente y con sello de tiempo conforme al protocolo de estampado temporal de RFC 3161, de modo que un tercero pueda verificar integridad y momento sin acceder a los sistemas del terminal; **(b)** estructura de verificación por árbol de Merkle según el patrón de registro público auditable descrito en RFC 6962, que permite demostrar que un registro individual pertenece a la serie sellada sin exponer el resto; **(c)** canal de notificación externo construido sobre los adaptadores por audiencia que el proyecto ya requiere, con confirmación de recepción registrada. La firma electrónica reutiliza el mismo servicio transversal que `RF-FIR-01` exige para los cuatro actos obligatorios: **no se agrega una plataforma criptográfica nueva**. | `[COMPLETADO]` |
| **Nivel de madurez y escala utilizada** | **TRL 8 en la escala de niveles de madurez tecnológica definida por ISO 16290:2013** (sistema completo, calificado en su entorno operacional). El estampado temporal y los registros encadenados verificables son estándares publicados en operación masiva desde hace más de una década; lo nuevo aquí no es la criptografía sino su aplicación como producto comercial del terminal. | `[COMPLETADO]` |
| **Fuentes citadas (APA 7.ª ed.)** | Adams, C., Cain, P., Pinkas, D., & Zuccherato, R. (2001). *Internet X.509 public key infrastructure time-stamp protocol (TSP)* (RFC 3161). Internet Engineering Task Force. https://doi.org/10.17487/RFC3161<br><br>Laurie, B., Langley, A., & Kasper, E. (2013). *Certificate transparency* (RFC 6962). Internet Engineering Task Force. https://doi.org/10.17487/RFC6962<br><br>International Organization for Standardization. (2013). *Space systems — Definition of the technology readiness levels (TRLs) and their criteria of assessment* (ISO 16290:2013). | `[COMPLETADO]` — verificadas |
| **Dónde se inserta en la arquitectura** | Capa 4 (servicios de negocio) y capa 7 (seguridad transversal) del Maestro §6. Cadena: `CTX-REEFER` genera el evento y la serie → `SRV-EVID` sella y firma → `SRV-NOTIF` emite el aviso externo por adaptador de audiencia → `CH-PORTAL` y `GW-API` entregan el certificado y exponen el punto de verificación → `DATA-TS` conserva la serie y `DATA-DOC` el certificado. **No toca** `EDGE-RUN` ni las cinco funciones críticas de 72 horas. **Activa el `RT-26.07`:** introduce una nueva superficie de exposición externa y requiere modelado de amenazas STRIDE propio. | `[COMPLETADO]` provisional contra Maestro §6.1 · `[PENDIENTE — Célula 3]` confirmación del catálogo y modelado STRIDE (entregables D1 y D2) |
| **Paquetes de la EDT que la ejecutan** | **Hipótesis inicial explícita:** paquete de instrumentación del patio refrigerado; paquete de servicios de evidencia y firma; paquete de notificaciones y adaptadores; paquete de portal y canales externos; paquete de seguridad y modelado de amenazas. | `[PENDIENTE — falta información de ninguna célula en esta etapa]` — la EDT corresponde al Subdocumento 7 y al Formulario T-14, del Informe 2 |
| **Mes del cronograma en que se materializa** | **Hipótesis anclada al Art. 17° de las BA. Fase A —aviso proactivo por canal directo—: construcción meses 10 a 12, medición en marcha blanca de Etapa 1, meses 13 a 15. Fase B —certificado descargable con usuario autenticado—: construcción meses 16 a 18, marcha blanca meses 19 a 20, producción mes 21.** El corte en dos fases no es arbitrario: el registro y la verificación de identidad de usuarios externos (`RF-POR-02`) pertenece a la Etapa 2 según Célula 2, de modo que la entrega autenticada no puede adelantarse. | `[COMPLETADO]` en su anclaje contractual · `[PENDIENTE — Célula 2]` confirmación del reparto por etapa |
| **Inversión requerida** | Sin cifra, conforme al Art. 53° de las BA (ver §0.2). **Naturaleza del desembolso:** incremento marginal sobre inversión ya comprometida. La instrumentación de las 2.400 tomas y los 26 tableros, la serie de temperatura y el servicio de firma electrónica son obligatorios por `RF-REF-01` a `RF-REF-12` y `RF-FIR-01`; la innovación agrega esfuerzo de desarrollo de los componentes de sellado, certificado y canal externo, más el modelado de amenazas. **No agrega hardware de terreno.** | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3, Oferta Económica, Entregable 2]` |
| **Efecto en el costo operacional** | **Dirección: incremento leve y acotado.** Componentes: almacenamiento y retención de certificados durante los 5 años de retención de series de temperatura fijados por el Caso; operación del punto de verificación externo; soporte en español e inglés del canal al cliente (Restricción 13). **Compensación parcial:** desvía consultas del mostrador y del teléfono, que es el efecto que `RF-POR-08` obliga a medir. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Beneficio esperado y su cuantificación** | **Tres beneficios, en orden de defendibilidad. (1) Reducción del daño por falla de frío no detectada a tiempo:** el aviso al dueño de la carga añade un actor que sí tiene incentivo para insistir cuando nadie confirma en el turno de madrugada, que es exactamente el modo de falla del 18 de febrero. **(2) Retención comercial:** el terminal pasa a poder ofrecer evidencia de cadena de frío como atributo del servicio, en una operación donde el Caso registra que tras la pérdida del 18 de febrero *«el exportador no volvió»*. **(3) Reducción de disputas** sobre condición de la carga al arribo. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` la cuantificación monetaria |
| **Indicador de verificación, línea base y meta** | **Indicadores: (a)** porcentaje de embarques refrigerados con certificado emitido y verificable por un tercero; **(b)** tiempo transcurrido entre la desviación detectada y el aviso efectivamente recibido por el dueño de la carga. **Línea base de ambos: cero** — hoy no existe ni certificado ni aviso externo. | `[COMPLETADO]` indicador y línea base · `[PENDIENTE — decisión propia de Célula 4]` la meta |
| **Momento de medición** | Indicador (b) durante la marcha blanca de Etapa 1 (meses 13 a 15), con al menos un simulacro en turno de madrugada, replicando el criterio de aceptación que Célula 2 fijó para `RF-REF-08`. Indicador (a) durante la marcha blanca de Etapa 2 (meses 19 y 20). Ambos en régimen desde el mes 21. | `[COMPLETADO]` |
| **Riesgo de adopción, probabilidad e impacto** | **Riesgo principal: el dueño de la carga no consume el aviso ni el certificado**, porque su proceso interno no lo contempla o porque el contacto registrado no es la persona que puede actuar. **Probabilidad: media.** **Impacto: medio** — la obligación de `RF-REF-08` a `RF-REF-12` se cumple igual, pero el beneficio diferenciador no se materializa. **Riesgo secundario: el certificado no es aceptado como evidencia por el mercado de destino o por la autoridad.** Probabilidad media, impacto medio. **Riesgo terciario: la nueva exposición externa amplía la superficie de ataque** en una instalación calificada como operador de importancia vital. Probabilidad baja, impacto alto. | `[COMPLETADO]` |
| **Estrategia de mitigación** | Contacto de aviso validado con cada exportador al momento de la reserva y verificado con envío de prueba antes de la primera temporada. Formato del certificado acordado tempranamente con al menos un exportador y una autoridad, en la misma lógica de pre-verificación que Célula 2 aplicó a las emisiones en `RF-EMI-05`. Para el riesgo terciario: modelado STRIDE propio conforme al `RT-26.07`, exposición únicamente a través de la capa de borde con protección WAF y anti-DDoS ya exigida, y verificación que no requiera autenticación pero tampoco revele información comercial, respetando `RF-POR-04`. | `[COMPLETADO]` · el modelado STRIDE `[PENDIENTE — Célula 3]` |
| **Plan de contingencia si no rinde lo esperado** | Se **degrada a la funcionalidad obligatoria sin pérdida de cumplimiento**: la alarma sigue llegando al operador y al supervisor (`RF-REF-08`), la serie sigue siendo continua (`RF-REF-11`) y sigue descargándose por autoservicio (`RF-REF-12`). Se suspende el canal externo y el certificado deja de emitirse automáticamente, quedando disponible bajo solicitud. **Ningún compromiso obligatorio depende de esta innovación.** | `[COMPLETADO]` |

---

### T-19 · IN-02

| Campo | Contenido | Estado |
|---|---|---|
| **Tipo de innovación (1 a 5)** | **2 — Proceso** | `[COMPLETADO]` BA, Art. 28°, tipo 2 |
| **Nombre de la innovación** | **Cita convenida a tres bandas: reprogramación automática de la franja del camión por confirmación de carga lista del dueño de la carga** | `[COMPLETADO]` |
| **Problema u oportunidad del caso que resuelve** | El sistema de citas resuelve el orden de llegada, pero no resuelve por qué el camión llega cuando llega. **El transportista no controla cuándo estará lista la carga**, de modo que una cita que él solicita es una promesa que él no puede cumplir. El Caso 06 lo dejó explícitamente sin resolver: *«si habrá sistema de citas para camiones, si será obligatorio u opcional, si tendrá penalización por incumplimiento y cómo se trata al transportista que no controla cuándo estará lista la carga»*. La innovación cambia el proceso de negocio: **la cita deja de ser una solicitud del transportista y pasa a ser un acuerdo de tres partes** —dueño de la carga, transportista y terminal— en el que la franja se reprograma automáticamente cuando el dueño de la carga confirma disponibilidad efectiva. | `[COMPLETADO]` Caso 06, num. 16.1, decisión pendiente N° 6; **Cap. 8, entrevista de Hernán Cifuentes Palma, gerente general de empresa de transporte terrestre**; Cap. 9.1 |
| **Evidencia o dato que dimensiona el problema** | Estadía del camión: **78 minutos contra 45 comprometidos**, con **tres semestres consecutivos sobre el umbral**. Fila máxima registrada: **3,2 km y 140 camiones** el 12 de marzo de 2026. Camiones que llegan con documentación incompleta o errónea: **22 %**. Sistema de citas: **inexistente**. Camiones diarios: **1.450 promedio y 2.600 en peak** de temporada de fruta; **380 empresas de transporte terrestre** usuarias. Y el dato que dimensiona el problema desde el otro lado del mostrador, en palabras del transportista entrevistado: *«Un camión mío hace tres vueltas al día cuando podría hacer cuatro. Eso es un veinticinco por ciento de mi flota que existe solo para esperar.»* | `[COMPLETADO]` Caso 06, Cap. 7.3, Cap. 14.1 y Cap. 8 (entrevista de Hernán Cifuentes Palma) |
| **Tecnología, práctica o modelo que la sustenta** | No es una tecnología nueva sino un **rediseño del proceso**, que el Artículo 28° admite expresamente para el tipo 2. El modelo tiene cuatro movimientos: **(a)** la reserva de franja se crea asociada a una unidad de carga y no solo a una patente; **(b)** el dueño de la carga —exportador, depósito o agencia— confirma disponibilidad efectiva por el portal o por integración, y esa confirmación es la que libera la franja; **(c)** si la confirmación no llega dentro del plazo declarado, el sistema **reprograma automáticamente** a la siguiente franja compatible y notifica a las tres partes por el mismo canal de cola virtual que la Decisión N° 6 de Célula 2 ya estableció; **(d)** la franja liberada se reasigna, de modo que la capacidad declarada del gate no se pierde. El incentivo se mantiene positivo, sin multa, conforme a la Decisión N° 6: quien cumple obtiene prioridad de atención. | `[COMPLETADO]` |
| **Nivel de madurez y escala utilizada** | Los sistemas de cita de camiones son **TRL 9 en la escala ISO 16290:2013** —probados en operación real en múltiples puertos—, pero **la variante de tres partes con reprogramación automática por confirmación del dueño de la carga no está documentada en la literatura arbitrada revisada**, por lo que se declara como **adaptación de una práctica madura a una condición no resuelta de este caso**, no como tecnología emergente. La evidencia disponible es sobre el mecanismo base, no sobre la variante. Se declara así deliberadamente. | `[COMPLETADO]` |
| **Fuentes citadas (APA 7.ª ed.)** | Giuliano, G., & O'Brien, T. (2007). Reducing port-related truck emissions: The terminal gate appointment system at the Ports of Los Angeles and Long Beach. *Transportation Research Part D: Transport and Environment*. `[volumen, número y páginas por verificar contra el original]`<br><br>Ramírez-Nafarrate, A., González-Ramírez, R. G., Smith, N. R., Guerra-Olivares, R., & Voß, S. (2017). Impact on yard efficiency of a truck appointment system for a port terminal. *Annals of Operations Research, 258*(2), 195–216. https://doi.org/10.1007/s10479-016-2384-0<br><br>International Organization for Standardization. (2013). *Space systems — Definition of the technology readiness levels (TRLs) and their criteria of assessment* (ISO 16290:2013). | `[COMPLETADO]` para Ramírez-Nafarrate et al. e ISO 16290 · **`[PENDIENTE — decisión propia de Célula 4]`** completar volumen y páginas de Giuliano y O'Brien contra el original antes de la entrega. Ambas fuentes fueron utilizadas por Célula 2 en la derivación de su meta 14 |
| **Dónde se inserta en la arquitectura** | Capa 4 (servicios de negocio) y capa 1 (presentación). `CTX-GATE` incorpora el estado «franja condicionada a confirmación» y la regla de reprogramación; `CH-PORTAL` expone la confirmación al dueño de la carga; `SRV-NOTIF` emite el aviso a las tres partes con los adaptadores por audiencia ya previstos; `CTX-OPS` conserva el hecho. **No modifica la arquitectura de seguridad** más allá de sumar un rol externo a la matriz de autorización de `SRV-IAM`, por lo que no activa el `RT-26.07`. | `[COMPLETADO]` provisional contra Maestro §6.1 · `[PENDIENTE — Célula 3]` confirmación |
| **Paquetes de la EDT que la ejecutan** | **Hipótesis inicial explícita:** paquete de gate y citas; paquete de portal y autoservicio; paquete de notificaciones; paquete de identidad para usuarios externos. | `[PENDIENTE — falta información de ninguna célula en esta etapa]` — EDT del Informe 2 |
| **Mes del cronograma en que se materializa** | **Hipótesis anclada al Art. 17°: construcción meses 8 a 12 —dentro del desarrollo de la Etapa 1, porque el dominio `RF-GAT` completo es de Etapa 1 según Célula 2—, medición durante la marcha blanca de Etapa 1, meses 13 a 15, y producción en el mes 16.** **Esta es la innovación con la que Terabyte cumple el `RT-26.08`**, que valora que al menos una innovación sea verificable antes del mes 16. | `[COMPLETADO]` en su anclaje contractual · `[PENDIENTE — Célula 2]` confirmación |
| **Inversión requerida** | Sin cifra (Art. 53°, ver §0.2). **Naturaleza:** exclusivamente esfuerzo de desarrollo e integración sobre componentes que el alcance obligatorio ya construye. **Cero hardware adicional.** Es, de las cinco, la de menor intensidad de inversión. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Efecto en el costo operacional** | **Dirección: neutro a levemente reductor.** No agrega dotación: la reprogramación es automática. Reduce la atención asistida del carril de excepción y las llamadas de coordinación, que es el efecto que `RF-POR-08` obliga a medir por tipo de trámite. Agrega un costo menor de mensajería saliente hacia tres destinatarios en vez de uno. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Beneficio esperado y su cuantificación** | Actúa sobre el indicador de mayor consecuencia contractual del caso —la estadía del camión comprometida con el concedente— por una vía distinta de la que atacan los requerimientos obligatorios: en vez de acelerar la atención dentro del terminal, **evita que el camión salga a la ruta antes de que su carga esté lista**. Beneficio secundario: aumenta la adopción del sistema de citas, del que depende a su vez la meta 1 de Célula 2 sobre remociones, que está explícitamente atada a *«que exista información anticipada de retiro»*. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` la cuantificación |
| **Indicador de verificación, línea base y meta** | **Indicadores: (a)** porcentaje de citas cumplidas dentro de ventana sobre citas otorgadas; **(b)** porcentaje de reprogramaciones originadas por confirmación del dueño de la carga sobre el total de reprogramaciones; **(c)** estadía media del camión con cita convenida frente a la de quien llega sin cita. **Línea base de (a) y (b): cero** — no existe sistema de citas. **Línea base de (c): 78 minutos**, que es la estadía general 2025. | `[COMPLETADO]` indicadores y líneas base · `[PENDIENTE — decisión propia de Célula 4]` las metas, que deben coordinarse con la meta 14 de Célula 2 (prioridad perceptible ≥ 30 % más rápida) |
| **Momento de medición** | **Semanal durante la marcha blanca de la Etapa 1, meses 13 a 15**, con reporte diario conforme al Art. 17.1 de las BA, cuya tabla de cronograma exige para los meses 13 a 15 *«plan de reversión activo y medición diaria de indicadores»*. Consolidación al cierre de la marcha blanca como condición del paso a producción del mes 16. Seguimiento mensual en régimen, con reporte separado del peak de temporada, siguiendo el criterio que Célula 2 aplicó a su meta 1. | `[COMPLETADO]` |
| **Riesgo de adopción, probabilidad e impacto** | **Riesgo principal: el dueño de la carga no confirma**, porque la confirmación le agrega trabajo sin beneficio directo para él. **Probabilidad: alta.** **Impacto: alto** — sin confirmación, la innovación se degrada al sistema de citas obligatorio y no aporta nada. Es el riesgo mejor documentado de la cartera: Giuliano y O'Brien (2007) reportan efecto nulo en Los Ángeles y Long Beach con adopción de 5 a 30 %. **Riesgo secundario: la reprogramación automática se percibe como pérdida del turno** y genera resistencia del transportista. Probabilidad media, impacto medio. | `[COMPLETADO]` |
| **Estrategia de mitigación** | La confirmación debe ser de un solo gesto y disponible en el mismo portal donde el exportador ya realiza los trámites obligatorios, sin credencial adicional. El incentivo debe ser perceptible: Célula 2 fijó en su meta 14 que la prioridad por cita cumplida sea **al menos 30 % más rápida**, apoyándose en que un incentivo imperceptible no genera adopción. La reprogramación conserva la prioridad ganada, de modo que confirmar tarde no castiga a quien confirmó. Ramírez-Nafarrate et al. (2017) muestran, sobre el Puerto de Arica, que el beneficio se sostiene con cumplimiento parcial, lo que respalda no exigir cumplimiento perfecto ni multa. | `[COMPLETADO]` |
| **Plan de contingencia si no rinde lo esperado** | Se **degrada al sistema de citas de la Decisión N° 6 sin pérdida de cumplimiento**: cita opcional, sin multa, con prioridad de atención y cola virtual. La confirmación del dueño de la carga pasa de gatillo automático a dato informativo que el operador de gate puede consultar. **Segunda contingencia declarada:** si la adopción se estanca bajo el umbral que se fije, se evalúa la evolución a obligatoriedad **solo para transportistas de alto volumen recurrente**, que es la salida que la propia Decisión N° 6 ya dejó abierta. | `[COMPLETADO]` |

---

### T-19 · IN-03

| Campo | Contenido | Estado |
|---|---|---|
| **Tipo de innovación (1 a 5)** | **3 — Tecnológica o de arquitectura** | `[COMPLETADO]` BA, Art. 28°, tipo 3 |
| **Nombre de la innovación** | **Gemelo de operación del Terminal Aconcagua: simulación de eventos discretos calibrada con la telemetría real del terminal, sin autoridad operacional** | `[COMPLETADO]` |
| **Problema u oportunidad del caso que resuelve** | **En este terminal no existe dónde ensayar un cambio.** Está prohibido intervenir entre el 15 de diciembre y el 30 de abril; está prohibido intervenir durante la atención de una nave y en las cuatro horas previas a una ventana confirmada, con 620 recaladas al año; el patio opera al 90 % en peak; y la operación es 24x7x365 sin ventana de detención total. En consecuencia, toda decisión operacional relevante —cuántas franjas de cita ofrecer por hora, qué política de apilamiento aplicar, cuántas grúas asignar a una recalada, qué pasa si se incorpora un cuarto sitio— se toma hoy sin poder probarla, y se prueba en producción con una nave amarrada. La innovación provee un **banco de decisiones fuera de línea**: un modelo del terminal, calibrado con la telemetría que el propio proyecto instala, donde el cambio se ensaya antes de tocar la operación. | `[COMPLETADO]` Caso 06, Cap. 10, restricciones 2, 9 y 10; Cap. 7.2; Cap. 13.2; Cap. 17.4, punto 14 |
| **Evidencia o dato que dimensiona el problema** | Congelamiento de **cuatro meses y medio** al año. **620 naves al año** con ventana comprometida, cada una con su propia prohibición de intervención. Ocupación del patio en peak: **90 %**. Productividad de grúa: **24,8 mov/hora contra 30 exigidos a 2029**. Registro del detalle de movimientos por hora y por grúa: **inexistente**, es decir, hoy ni siquiera existe la serie con la que se podría evaluar un cambio a posteriori. Evaluación del concedente sobre un **cuarto sitio entre 2030 y 2032**, que el CLIENTE espera incorporar *«sin rehacer la solución»*. | `[COMPLETADO]` Caso 06, Cap. 7.1, 7.2 y Cap. 13.2 |
| **Tecnología, práctica o modelo que la sustenta** | **Simulación de eventos discretos** del ciclo completo —llegada de camión, gate, asignación de posición, movimiento de patio, tractocamión, grúa de muelle, ventana de nave— **calibrada contra la telemetría real** que `RF-PAT-12`, `RF-TRA-06` y `RF-NAV-12` producen de todos modos, más los eventos de gate de `RF-GAT-11`. La calibración es lo que distingue esto de un modelo de escritorio: el gemelo se contrasta contra la operación observada y declara su error. **No incorpora inteligencia artificial en la versión comprometida** y no tiene ninguna conexión de escritura hacia el núcleo operacional: es un consumidor de datos, nunca un emisor de órdenes. | `[COMPLETADO]` |
| **Nivel de madurez y escala utilizada** | **TRL 6 a 7 en la escala ISO 16290:2013**: modelo demostrado en entorno representativo, con aplicaciones publicadas en terminales de contenedores, pero sin implantación acreditada en un terminal chileno de esta escala. Se declara el rango y no un valor único porque la madurez depende de la calidad de la calibración, que a su vez depende de instrumentación que aún no existe (**hoy 12 de 18 equipos de patio tienen terminal montada**). | `[COMPLETADO]` |
| **Fuentes citadas (APA 7.ª ed.)** | Hakimi, F., Khaled, T., Al-Kharaz, M., Foahom Gouabou, A. C., & Amzil, K. (2024). Towards a digital twin modeling method for container terminal port. *Procedia Computer Science, 246*, 3113–3121. https://doi.org/10.1016/j.procs.2024.09.361<br><br>Carlo, H. J., Vis, I. F. A., & Roodbergen, K. J. (2014). Storage yard operations in container terminals: Literature overview, trends, and research directions. *European Journal of Operational Research, 235*(2), 412–430.<br><br>International Organization for Standardization. (2013). *Space systems — Definition of the technology readiness levels (TRLs) and their criteria of assessment* (ISO 16290:2013). | `[COMPLETADO]` — verificadas |
| **Dónde se inserta en la arquitectura** | **Componente nuevo propuesto a Célula 3: `CTX-SIM`**, en la capa 4 del Maestro §6, alimentado exclusivamente desde `DATA-AN` —analítica y reportes— y desde `DATA-TS` para las series de telemetría. **Restricciones de diseño que se declaran como parte de la innovación: (a)** `CTX-SIM` **no expone ninguna interfaz de escritura** hacia `CTX-OPS`, `CTX-YARD`, `CTX-GATE` ni `EDGE-RUN`; **(b)** se despliega **en nube**, nunca en el borde, precisamente para no competir por la capacidad local que sostiene las cinco funciones críticas durante 72 horas sin enlace, conforme a la regla negativa 8 del Maestro §19; **(c)** su indisponibilidad **no degrada ninguna función operacional**, por lo que no entra en el cálculo de disponibilidad de servicios críticos. **Activa el `RT-26.07`** solo en cuanto consume datos operacionales y comerciales sensibles: requiere clasificación de la información replicada y modelado de amenazas propio. | `[COMPLETADO]` como propuesta · `[PENDIENTE — Célula 3]` alta del componente en el catálogo, decisión de emplazamiento conforme al Art. 16° y modelado STRIDE |
| **Paquetes de la EDT que la ejecutan** | **Hipótesis inicial explícita:** paquete de plataforma de datos y analítica; paquete de modelado y simulación; paquete de instrumentación de equipos de patio (dependencia de entrada, no de ejecución); paquete de seguridad y clasificación de información. | `[PENDIENTE — falta información de ninguna célula en esta etapa]` — EDT del Informe 2 |
| **Mes del cronograma en que se materializa** | **Hipótesis anclada al Art. 17°: versión 1 construida entre los meses 6 y 12, calibrada con los datos de la marcha blanca de Etapa 1 (meses 13 a 15) y puesta en uso para decidir la capacidad declarada de franjas del gate antes del paso a producción del mes 16. Versión 2 —con planificación de nave y patio completos— entre los meses 16 y 21.** El uso más valioso ocurre después: durante la operación (meses 21 a 56) es el único lugar donde se puede ensayar un cambio durante el congelamiento estacional. | `[COMPLETADO]` en su anclaje contractual · `[PENDIENTE — Célula 2]` confirmación de la disponibilidad de datos por etapa |
| **Inversión requerida** | Sin cifra (Art. 53°, ver §0.2). **Naturaleza:** desarrollo del modelo, cómputo en nube por ráfagas —el gemelo no corre en continuo— y esfuerzo de calibración recurrente. **Cero hardware.** Aprovecha íntegramente la plataforma de datos que `DATA-AN` ya exige para los indicadores del concedente y las emisiones. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Efecto en el costo operacional** | **Dirección: incremento acotado y controlable.** El cómputo es elástico y por ráfagas, de modo que la práctica FinOps que el Art. 16.3 de las BA ya exige —etiquetado, presupuestos, alertas de desviación— lo mantiene acotado. Requiere una capacidad de modelado que el CLIENTE no tiene: **por la Restricción no negociable N° 11, se ofrece como servicio y queda costeada**, lo que la conecta directamente con IN-04. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Beneficio esperado y su cuantificación** | **Beneficio principal: evitar el ensayo en producción.** Cada cambio de política de patio o de gate que hoy solo puede probarse con una nave amarrada pasa a probarse en el modelo. **Beneficio segundo: dar fundamento a un parámetro que hoy no lo tiene** — `RF-GAT-16` obliga a limitar las franjas ofrecidas «por capacidad declarada», pero ningún requerimiento dice de dónde sale esa capacidad. **Beneficio tercero: responder la pregunta del Cap. 17.4 punto 14** —qué componente se satura primero en el peak y ante un cuarto sitio— con un modelo en vez de con una opinión. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` la cuantificación |
| **Indicador de verificación, línea base y meta** | **Indicadores: (a)** error del gemelo contra la operación real en dos magnitudes —estadía media del camión y movimientos por hora por grúa—; **(b)** número de cambios de política ensayados en el gemelo antes de aplicarse en producción, sobre el total de cambios aplicados. **Línea base de ambos: cero** — no existe capacidad de ensayo ni modelo con el cual comparar. | `[COMPLETADO]` indicadores y línea base · `[PENDIENTE — decisión propia de Célula 4]` la meta de error, que no puede fijarse antes de conocer la calidad y densidad de la telemetría instalada |
| **Momento de medición** | Primera calibración al cierre del desarrollo de la Etapa 1 (mes 12). Verificación del error contra datos reales durante cada marcha blanca (meses 13 a 15 y 19 a 20). Recalibración obligatoria declarada tras cada cambio estructural del terminal, y como mínimo una vez al año en operación. | `[COMPLETADO]` |
| **Riesgo de adopción, probabilidad e impacto** | **Riesgo principal: el gemelo no se calibra lo suficiente y sus resultados no se creen.** **Probabilidad: media-alta.** **Impacto: medio** — un modelo en el que nadie confía se abandona, aunque no daña la operación porque no tiene autoridad sobre ella. La causa raíz más probable es la calidad de la telemetría: hoy solo **12 de 18 equipos de patio tienen terminal montada**, y Célula 2 ya elevó la meta de instrumentación a **74 de 74 equipos**. **Riesgo secundario: que alguien intente darle autoridad operacional**, lo que violaría el diseño y podría afectar la seguridad de las personas. Probabilidad baja, impacto alto. **Riesgo terciario: percepción de «tecnología de moda»** por parte de la Comisión, precisamente lo que el Art. 30.2 castiga. Probabilidad media, impacto medio en evaluación. | `[COMPLETADO]` |
| **Estrategia de mitigación** | Publicar el error del gemelo junto a cada resultado, siempre: un modelo que declara su error se usa con criterio, uno que no lo declara se cree ciegamente o se descarta. Empezar por un alcance angosto y verificable —gate y flujo del camión— antes de modelar el patio completo. **Interdicción de diseño explícita y auditable:** `CTX-SIM` no tiene credenciales de escritura sobre ningún contexto operacional, y esa restricción se verifica en la matriz de segregación de funciones que `SRV-IAM` ya exige. Para el riesgo terciario: presentar el gemelo siempre asociado a la restricción del caso que lo justifica —no hay ventana para ensayar— y no como adopción de una tendencia. | `[COMPLETADO]` |
| **Plan de contingencia si no rinde lo esperado** | Si el error de calibración no converge a un rango utilizable, **el alcance se reduce al gate y al gemelo se le retira la ambición de patio y nave**, conservándolo únicamente como herramienta de dimensionamiento de franjas y de capacidad. Si tampoco allí resulta, la capacidad declarada de `RF-GAT-16` vuelve a fijarse por observación directa durante la marcha blanca, que es como se fijaría sin la innovación. **Ningún requerimiento obligatorio depende de `CTX-SIM`.** | `[COMPLETADO]` |

---

### T-19 · IN-04

| Campo | Contenido | Estado |
|---|---|---|
| **Tipo de innovación (1 a 5)** | **4 — Modelo de negocio o de contratación** | `[COMPLETADO]` BA, Art. 28°, tipo 4 |
| **Nombre de la innovación** | **Servicio gestionado del equipamiento de terreno con compromiso de resultado verificable, adicional al régimen de niveles de servicio del Artículo 78°** | `[COMPLETADO]` |
| **Problema u oportunidad del caso que resuelve** | El caso plantea una asimetría que ningún requerimiento funcional puede resolver, porque no es técnica sino contractual. **El CLIENTE compra el hardware pero no tiene quién lo mantenga:** el proponente especifica qué comprar, cuánto y con qué características, el CLIENTE lo adquiere, y el área de TI del CLIENTE son cinco personas en un operador de importancia vital. Al mismo tiempo, **el equipamiento va a un ambiente que lo destruye**: atmósfera salina, corrosión acelerada, a menos de 300 metros del mar, y las bases exigen que su plan de reposición esté costeado. Y en tercer lugar, **el CLIENTE ya lleva tres semestres consecutivos incumpliendo el indicador comprometido con el concedente**, sin que su proveedor comparta esa consecuencia. La innovación alinea los tres hechos: Terabyte gestiona el ciclo de vida del equipamiento de terreno como servicio, y asume un compromiso de resultado verificable sobre indicadores que el sistema produce de forma trazable y que el Artículo 78° no cubre. | `[COMPLETADO]` Caso 06, Cap. 10, restricciones 11, 12 y 14; Cap. 11 (exclusión de hardware); Cap. 6 y Cap. 7.1 |
| **Evidencia o dato que dimensiona el problema** | Área de TI del CLIENTE: **5 personas**. Equipamiento a instrumentar: **2.400 tomas refrigeradas, 26 tableros, 74 equipos móviles** —18 grúas de patio, 42 tractocamiones y 14 equipos de manipulación pesada—, con proyección a **88 equipos, 2.900 tomas y 32 tableros**. Condición del sitio: **sala de 2012 a menos de 300 m del mar, ambiente salino y corrosión acelerada**. Cumplimiento de ventana de atraque: **71 % sobre 90 %**. Estadía del camión: **tres semestres consecutivos sobre el umbral**, con consecuencias contractuales frente al concedente. | `[COMPLETADO]` Caso 06, Cap. 7.1, Cap. 6, Cap. 14.1 y Cap. 10; universo de 74/88 equipos según la meta 5 corregida de Célula 2 |
| **Tecnología, práctica o modelo que la sustenta** | **Contratación basada en desempeño** —*performance-based contracting*— aplicada con dos componentes acoplados: **(a)** un **servicio gestionado de ciclo de vida del equipamiento de terreno** que cubre monitoreo de estado, mantención preventiva, reposición por corrosión y gestión del inventario de repuestos, sobre equipamiento que el CLIENTE compra y mantiene en su patrimonio, sin que Terabyte lo adquiera; **(b)** un **compromiso de resultado verificable sobre indicadores medidos por el propio sistema**, con dos salvaguardas de diseño: los indicadores son exactamente los que `RF-CON-11` obliga a producir de forma trazable para el concedente, y ninguno depende de un dato que Terabyte pueda producir sin evidencia auditable.<br><br>**Límite frente a las Bases, que es parte del diseño de la innovación.** El compromiso recae sobre indicadores que el **Artículo 78° no cubre** —disponibilidad del equipamiento de terreno instrumentado y continuidad de la instrumentación en ambiente marino—. El Art. 78° regula disponibilidad del servicio, tiempos de respuesta y resolución, MTTR, tasa de cambios fallidos, cumplimiento de RPO/RTO, vulnerabilidades, reincidencia y satisfacción; **no regula el equipamiento de terreno del CLIENTE**. La innovación **se suma** al régimen de los Artículos 78°, 79° y 80° y **no lo reemplaza, no lo rebaja ni propone un esquema alternativo de multas o de pago**. | `[COMPLETADO]` |
| **Nivel de madurez y escala utilizada** | La contratación basada en desempeño es una práctica de gestión consolidada, con revisión sistemática de literatura publicada. **`[PENDIENTE — decisión propia de Célula 4]`: definir qué escala de madurez se declara.** La escala TRL de ISO 16290:2013 está definida para tecnologías, no para modelos contractuales, y aplicarla aquí sería un uso impropio que la Comisión puede objetar. Alternativas a decidir: declarar madurez por evidencia de adopción sectorial documentada, o declarar expresamente que el `RT-26.03` no aplica porque **no es una innovación de base tecnológica**, que es la condición que ese requisito establece. **La segunda lectura parece la correcta y es la que se propone**, dejando la fuente citada de todos modos. | `[PENDIENTE — decisión propia de Célula 4]` |
| **Fuentes citadas (APA 7.ª ed.)** | Selviaridis, K., & Wynstra, F. (2015). Performance-based contracting: A literature review and future research directions. *International Journal of Production Research, 53*(12), 3505–3540. https://doi.org/10.1080/00207543.2014.978031 | `[COMPLETADO]` — verificada |
| **Dónde se inserta en la arquitectura** | **No es un componente de software.** Se inserta como cláusula del modelo de servicio, y su viabilidad descansa en componentes que ya existen en el diseño: `CTX-GATE` produce el cálculo trazable de la estadía (`RF-GAT-12`), `CTX-REEFER` produce la evidencia de alarma y confirmación (`RF-REF-10`), `CTX-EMIS` produce la emisión trazable (`RF-EMI-04`), y la producción trazable de los indicadores del concedente es obligación de `RF-CON-11`. `DATA-AN` es el repositorio desde el que se liquida el período. **Requisito de diseño que la innovación impone a la arquitectura:** todo indicador vinculado a remuneración debe ser reproducible por un tercero desde el dato de origen, sin intervención de Terabyte. | `[COMPLETADO]` · `[PENDIENTE — Célula 3]` confirmación de que la cadena de evidencia soporta reproducción por un tercero |
| **Paquetes de la EDT que la ejecutan** | **Hipótesis inicial explícita:** paquete de modelo de operación y niveles de servicio; paquete de gestión de activos de terreno y repuestos; paquete de plataforma de indicadores. Es la innovación con menor peso de EDT de construcción y mayor peso de EDT de operación (meses 21 a 56). | `[PENDIENTE — falta información de ninguna célula en esta etapa]` — EDT del Informe 2 |
| **Mes del cronograma en que se materializa** | **Hipótesis anclada al Art. 17°: el esquema se define contractualmente al inicio, pero el compromiso de resultado solo puede activarse cuando el sistema que produce el indicador está en producción. Entrada en vigencia: mes 16, con la producción de la Etapa 1. Régimen pleno: meses 21 a 56, coincidiendo con la fase de operación de 36 meses.** No se activa durante la marcha blanca: penalizar un indicador medido con un sistema que todavía convive con el registro anterior sería medir ruido. | `[COMPLETADO]` en su anclaje contractual · `[PENDIENTE — Célula 4 y validación del equipo]` la decisión sobre el momento exacto de activación |
| **Inversión requerida** | Sin cifra (Art. 53°, ver §0.2). **Naturaleza:** no requiere inversión en activos —el hardware sigue siendo del CLIENTE por exclusión expresa del Cap. 11—. Requiere constituir la capacidad de servicio: dotación de terreno, inventario de repuestos críticos con protección marina y herramientas de gestión de activos. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Efecto en el costo operacional** | **Doble dirección, y hay que decirlo así. Para el CLIENTE:** convierte un costo variable e imprevisible —reposición por corrosión, indisponibilidad de instrumentación, contratación de especialistas que no tiene— en un costo de servicio previsible, y libera a las cinco personas de TI de una función que no pueden sostener. **Para Terabyte:** incrementa el costo operacional propio y transfiere riesgo desde el CLIENTE hacia el proveedor. Es un traslado deliberado de riesgo, no una reducción de costo total. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Beneficio esperado y su cuantificación** | **Beneficio principal para el CLIENTE: el proveedor comparte la consecuencia del indicador.** Hoy el terminal acumula tres semestres sobre el umbral frente al concedente sin que su proveedor comparta esa consecuencia. **Beneficio segundo: cumple la Restricción no negociable N° 11 en su letra** —*«toda función que requiera un especialista dedicado que la compañía no tiene debe ofrecerse como servicio y estar costeada»*— en lugar de declararla cumplida en abstracto. **Beneficio tercero: hace exigible el plan de reposición costeado** que la Restricción N° 12 exige para el ambiente marino. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` la cuantificación |
| **Indicador de verificación, línea base y meta** | **Indicadores: (a)** porcentaje de indicadores comprometidos alcanzados en el período de liquidación; **(b)** disponibilidad del equipamiento de terreno gestionado —tomas, tableros y equipos móviles instrumentados—; **(c)** tiempo medio de reposición de un dispositivo de terreno inutilizado por corrosión. **Líneas base: (a)** 71 % de cumplimiento de ventana de atraque y tres semestres de estadía sobre umbral; **(b) y (c)** no existen, porque no hay instrumentación desplegada. | `[COMPLETADO]` indicadores y línea base de (a) · `[PENDIENTE — decisión propia de Célula 4]` las metas y la definición del conjunto exacto de indicadores vinculados a remuneración |
| **Momento de medición** | Liquidación **semestral**, deliberadamente alineada al informe de indicadores de desempeño que el contrato de concesión ya obliga a entregar al concedente, de modo que el terminal no construya dos verdades. Indicadores (b) y (c) medidos mensualmente para gestión, liquidados semestralmente. | `[COMPLETADO]` |
| **Riesgo de adopción, probabilidad e impacto** | **Riesgo principal: manipulación del indicador —*gaming*—**, es decir, que el proveedor optimice la métrica en vez del resultado. **Probabilidad: media.** **Impacto: alto**, porque destruye la confianza que el esquema necesita. **Riesgo secundario: atribución.** La estadía del camión depende de factores que Terabyte no controla —volumen comercial, ocupación de patio al 90 %, comportamiento del transportista—, y penalizar por un resultado no controlable produce un proveedor defensivo. **Probabilidad: alta. Impacto: alto.** Es el riesgo que la literatura de contratación por desempeño identifica como el determinante del éxito o el fracaso del esquema. **Riesgo terciario: el CLIENTE no acepta el esquema** por complejidad administrativa. Probabilidad media, impacto medio.<br><br>**Riesgo cuarto, y es el más peligroso de toda la cartera: que la innovación se lea como contrapropuesta de las Bases.** El Artículo 53° declara inadmisible, sin evaluación posterior, la oferta *«condicionada, con reservas, alternativas no solicitadas o sujeta a contrapropuesta de las Bases»*, y los Artículos 78°, 79° y 80° ya fijan niveles de servicio, medición y multas con topes y procedimiento. Una innovación de modelo de contratación que se leyera como reescritura de ese régimen no bajaría de puntaje: **haría inadmisible la oferta completa**. **Probabilidad: baja si la redacción es explícita; alta si no lo es. Impacto: máximo.** | `[COMPLETADO]` — riesgo identificado al contrastar la innovación contra el Título VI, conforme al punto 5 del comunicado del profesor |
| **Estrategia de mitigación** | Contra el *gaming*: **ningún indicador comprometido puede calcularse con un dato que Terabyte produzca sin evidencia reproducible**; todos derivan de la cadena trazable de `RF-CON-11` y son auditables por el concedente. Contra la atribución: el compromiso se vincula a **indicadores de disponibilidad y de comportamiento del sistema** —que Terabyte sí controla— y no directamente al resultado de negocio, y se declara un mecanismo de exclusión por causas ajenas documentadas. Contra la complejidad: el período de liquidación y el conjunto de indicadores se mantienen deliberadamente cortos y coincidentes con el reporte que el terminal ya produce para el concedente.<br><br>**Contra el riesgo cuarto —el crítico—: el texto del subdocumento debe declarar expresamente, con esas palabras, que el compromiso se suma al régimen de los Artículos 78° a 80° y no lo modifica**, que recae sobre indicadores que el Art. 78° no cubre, y que Terabyte acepta íntegramente el régimen de niveles de servicio y multas de las Bases sin reserva alguna. **Ninguna redacción de esta innovación puede sugerir un esquema alternativo de pago, de multas o de topes.** Esa declaración es obligatoria en la redacción final y debe revisarla el delegado antes de la entrega. | `[COMPLETADO]` |
| **Plan de contingencia si no rinde lo esperado** | Retorno a remuneración fija por niveles de servicio conforme al Artículo 78° de las BA, conservando el servicio gestionado del equipamiento de terreno, que es la parte que la Restricción N° 11 hace indispensable con independencia del esquema de remuneración. **La contingencia no afecta ningún compromiso técnico:** el alcance funcional y los niveles de servicio se mantienen intactos; solo cambia la forma de remunerarlos. | `[COMPLETADO]` |

---

### T-19 · IN-05

| Campo | Contenido | Estado |
|---|---|---|
| **Tipo de innovación (1 a 5)** | **5 — Experiencia de usuario, sostenibilidad o impacto social** · dimensión elegida: **sostenibilidad** | `[COMPLETADO]` BA, Art. 28°, tipo 5 |
| **Nombre de la innovación** | **Intensidad de carbono comprometida: meta de kg CO₂e por contenedor movilizado con reducción verificada bajo la misma metodología del reporte a la alianza naviera** | `[COMPLETADO]` |
| **Problema u oportunidad del caso que resuelve** | La alianza naviera impuso tres condiciones para 2029, y una es el **reporte verificado de emisiones**. El alcance obligatorio resuelve la mitad del problema: medir, calcular por contenedor, trazar hasta el dato de origen, acumular la serie y obtener el reporte verificado. **Pero medir no es reducir.** Lo que la alianza va a recibir en 2029, si el proyecto solo cumple lo obligatorio, es una cifra sin trayectoria. La innovación es comprometer una **meta de intensidad de carbono** —kg CO₂e por contenedor movilizado— y reducirla actuando sobre tres palancas que ya existen en el diseño, con la misma metodología que el verificador va a auditar. | `[COMPLETADO]` Caso 06, Cap. 1; Cap. 9.10; Cap. 13.2 (hito 2029); Cap. 19 (que exige que la innovación de sostenibilidad se articule con la exigencia concreta de la alianza) |
| **Evidencia o dato que dimensiona el problema** | Emisiones de gases de efecto invernadero por contenedor movilizado: **no se mide**; referencia exigida: **reporte verificado a 2029**. La alianza representa el **34 % de los contenedores**. Consumo energético por equipo: **no existe medición individual** hoy. Flota: **16 equipos diésel y 2 eléctricos**. Movimientos de patio que son remociones: **18 %** —cada remoción es combustible quemado en un movimiento que no traslada carga—. Transferencia anual: **780.000 TEU y 486.000 contenedores**, con proyección a 920.000 TEU y 570.000 contenedores. | `[COMPLETADO]` Caso 06, Cap. 7.2, 7.3, Cap. 11, Cap. 13.2 y Cap. 14.1 |
| **Tecnología, práctica o modelo que la sustenta** | **La misma metodología del reporte obligatorio, aplicada como instrumento de gestión y no solo de reporte: ISO 14083:2023** como norma de cuantificación, implementada operativamente mediante el **GLEC Framework v3.2** y verificada por tercero acreditado bajo **ISO 14064-3**, que es exactamente la jerarquía normativa que Célula 2 fijó en su Decisión N° 16. Sobre esa base, **tres palancas concretas**: **(a)** **remociones evitadas** — cada remoción es un movimiento sin traslado de carga, de modo que la reducción que persigue la meta 1 de Célula 2 se traduce directamente en combustible no quemado y se contabiliza como tal; **(b)** **ralentí de tractocamiones**, derivado de la telemetría de consumo que `RF-EMI-01` ya instala en los 16 equipos diésel, sin sensor adicional; **(c)** **asignación preferente de los dos equipos eléctricos existentes** a los ciclos de mayor intensidad de emisión, mediante un término de puntuación añadido al algoritmo que `RF-PAT-06` ya usa para asignar posición. **No electrifica la flota**, respetando la exclusión expresa del Cap. 11. | `[COMPLETADO]` |
| **Nivel de madurez y escala utilizada** | La metodología de cuantificación es **norma internacional publicada y en uso** —no corresponde declarar TRL para una norma—. Para el componente de gestión: **TRL 7 en la escala ISO 16290:2013**, prototipo demostrado en entorno operacional, porque la contabilización de intensidad por contenedor con atribución a movimiento existe en la industria pero su acoplamiento a la asignación de patio es una adaptación propia de esta propuesta. | `[COMPLETADO]` |
| **Fuentes citadas (APA 7.ª ed.)** | International Organization for Standardization. (2023). *Greenhouse gases — Quantification and reporting of greenhouse gas emissions arising from transport chain operations* (ISO 14083:2023).<br><br>International Organization for Standardization. (2019). *Greenhouse gases — Part 3: Specification with guidance for the verification and validation of greenhouse gas statements* (ISO 14064-3:2019).<br><br>Smart Freight Centre. (2023). *Global Logistics Emissions Council framework for logistics emissions accounting and reporting* (Version 3.0/3.2).<br><br>Carlo, H. J., Vis, I. F. A., & Roodbergen, K. J. (2014). Storage yard operations in container terminals: Literature overview, trends, and research directions. *European Journal of Operational Research, 235*(2), 412–430. | `[COMPLETADO]` para ISO 14083, ISO 14064-3 y Carlo et al. · **`[PENDIENTE — decisión propia de Célula 4]`** confirmar año exacto, versión y forma de cita del GLEC Framework v3.2 contra la publicación original de Smart Freight Centre, ya que Célula 2 la citó como «v3.2» sin año |
| **Dónde se inserta en la arquitectura** | Capa 4 y capa 6 del Maestro §6. `CTX-EMIS` incorpora el motor de intensidad y la trayectoria contra meta; `CTX-YARD` incorpora el término de puntuación de emisiones dentro del algoritmo de asignación que ya existe, **con peso configurable y tope declarado**; `DATA-TS` provee las series de consumo y `DATA-AN` sostiene la trayectoria y el expediente de verificación. **Restricción de diseño declarada:** el término de emisiones **nunca puede desplazar** una restricción de seguridad, de segregación IMDG ni una ventana de nave comprometida, y **no agrega ninguna interacción del operador**, con lo que la Restricción no negociable N° 1 se respeta por construcción. | `[COMPLETADO]` provisional contra Maestro §6.1 · `[PENDIENTE — Célula 3]` confirmación de la inserción del término en `CTX-YARD` |
| **Paquetes de la EDT que la ejecutan** | **Hipótesis inicial explícita:** paquete de instrumentación de consumo de equipos; paquete de emisiones y reporte; paquete de asignación y planificación de patio; paquete de verificación externa y aseguramiento. | `[PENDIENTE — falta información de ninguna célula en esta etapa]` — EDT del Informe 2 |
| **Mes del cronograma en que se materializa** | **Hipótesis anclada al Art. 17° y a `RF-EMI-05`, que obliga a acumular la serie desde el mes 1: captura de consumo desde el mes 1; primera medición de intensidad al cierre del desarrollo de la Etapa 1 (mes 12); línea base declarada y acordada con el verificador durante la marcha blanca de Etapa 1; activación del término de reducción en producción de Etapa 2 (mes 21); trayectoria acumulada y verificada bajo ISO 14064-3 antes del hito de 2029.** Este calendario responde a la objeción registrada de la gerenta comercial en el numeral 13.1 del Caso: *«si empezamos la mensajería y las emisiones el 2028, no llegamos, porque un reporte de emisiones verificado necesita serie de datos previa»*.<br><br>**Dependencia RESUELTA por la respuesta de coordinación del 2026-09-05:** el desarrollo de la Etapa 2 termina en el mes 18 y su producción está prevista para el mes 21. **Un resultado de intensidad en el mes 12 solo puede presentarse como prototipo o prevalidación, no como motor productivo**, salvo que se modifique formalmente el plan. Redacción corregida en consecuencia: captura desde el mes 1; **prototipo de cálculo y prevalidación metodológica con el verificador hacia el mes 12**; motor de cálculo productivo con la producción de la Etapa 2 en el **mes 21**; línea base declarada y acordada con el verificador antes de comprometer la meta. | `[COMPLETADO]` — dependencia cerrada con Célula 3 el 2026-09-05 |
| **Inversión requerida** | Sin cifra (Art. 53°, ver §0.2). **Naturaleza:** incremento marginal. La instrumentación de consumo en los 16 equipos diésel y la medición de kWh en los 2 eléctricos son obligatorias por `RF-EMI-01` y `RF-EMI-02`; el cálculo por contenedor y su trazabilidad son obligatorios por `RF-EMI-03` y `RF-EMI-04`. **La innovación agrega desarrollo del motor de intensidad y del término de puntuación, más el aseguramiento continuo con el verificador. Cero hardware adicional.** | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Efecto en el costo operacional** | **Dirección: reductora en el consumo, con un incremento acotado en verificación.** Toda remoción evitada y todo minuto de ralentí eliminado son combustible no comprado. En sentido contrario, el aseguramiento continuo con el verificador acreditado y la conservación del expediente de trazabilidad agregan un costo recurrente. **Efecto neto esperado: reductor**, aunque su magnitud depende de la elasticidad real entre remociones y consumo, que hoy no está medida en este terminal. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` |
| **Beneficio esperado y su cuantificación** | **Beneficio principal: convierte el cumplimiento de la tercera condición de la alianza en una posición negociadora.** Ante el 34 % de los contenedores, el terminal deja de presentar una cifra y presenta una trayectoria de reducción verificada bajo la misma norma. **Beneficio segundo: dato de emisión atribuido por embarque**, utilizable por el exportador y por la naviera en su propio inventario de alcance 3. **Beneficio tercero: ahorro de combustible** por remociones evitadas y ralentí eliminado. **Beneficio cuarto: refuerza la meta 1 de Célula 2** —remociones ≤ 14 %— al darle una segunda justificación económica y ambiental. | `[COMPLETADO]` cualitativo · `[PENDIENTE — Informe 3]` la cuantificación |
| **Indicador de verificación, línea base y meta** | **Indicador principal: intensidad de carbono en kg CO₂e por contenedor movilizado**, calculada conforme a ISO 14083:2023 e implementada con GLEC v3.2, con alcances 1, 2 y 3 explicitados. **Indicadores de palanca: (a)** porcentaje de remociones sobre movimientos de patio —compartido con la meta 1 de Célula 2, base 18 %, meta ≤ 14 % fuera del peak—; **(b)** horas de ralentí por equipo diésel. **Línea base del indicador principal: no existe.** El Caso declara literalmente que las emisiones por contenedor **«no se miden»**. | `[COMPLETADO]` indicador y estado de la línea base · **`[PENDIENTE — decisión propia de Célula 4]` la meta de reducción, que es estructuralmente imposible de fijar hoy:** no se puede comprometer un porcentaje de reducción contra una línea base que no existe. **Compromiso alternativo propuesto:** declarar la línea base como entregable verificable —sobre el prototipo de cálculo del mes 12 y confirmada con el motor productivo del mes 21— y comprometer la meta de reducción en ese momento, con acuerdo del verificador |
| **Momento de medición** | Captura desde el mes 1. **Prototipo de cálculo y prevalidación metodológica hacia el mes 12; motor productivo con la producción de la Etapa 2, en el mes 21.** Línea base declarada y sometida al verificador antes de comprometer la meta. Medición mensual desde el mes 21, con reporte anual y **verificación por tercero acreditado bajo ISO 14064-3 antes del hito de 2029**. Reporte del peak estacional por separado, aplicando el mismo criterio con que Célula 2 trató su meta 1. | `[COMPLETADO]` |
| **Riesgo de adopción, probabilidad e impacto** | **Riesgo principal: el verificador objeta el método de atribución del consumo al contenedor individual.** **Probabilidad: media.** **Impacto: alto**, porque afecta la condición de la alianza y no solo la innovación. Es el mismo riesgo que Célula 2 identificó al descartar el prorrateo en la Decisión N° 17. **Riesgo secundario: el término de emisiones en la asignación de patio compite con la meta de remociones y con la productividad de grúa**, y una decisión ambientalmente mejor puede ser operacionalmente peor. **Probabilidad: alta. Impacto: medio.** **Riesgo terciario: la reducción no se materializa** porque el consumo depende más del volumen y de la ocupación del patio —que la solución no controla— que de la asignación. Probabilidad media, impacto medio. | `[COMPLETADO]` |
| **Estrategia de mitigación** | Contra el riesgo del verificador: someter método, límites y período **tempranamente**, que es exactamente lo que `RF-EMI-05` ya obliga, y medición directa por equipo **sin prorrateo**, conforme a la Decisión N° 17 de Célula 2. Contra la competencia entre objetivos: el término de emisiones tiene **peso configurable con tope declarado** y **jamás** desplaza seguridad, segregación IMDG ni ventana de nave comprometida; el efecto cruzado sobre remociones y productividad se ensaya primero en el gemelo de IN-03 antes de tocar el patio real —**este es el acoplamiento más importante de la cartera**—. Contra el riesgo terciario: la meta se expresa como **intensidad por contenedor**, no como emisión absoluta, precisamente para neutralizar la variación de volumen. | `[COMPLETADO]` |
| **Plan de contingencia si no rinde lo esperado** | Se **desactiva el término de emisiones en la asignación de patio y se conserva íntegro el alcance obligatorio**: medición, cálculo por contenedor, trazabilidad, serie histórica y reporte verificado (`RF-EMI-01` a `RF-EMI-06`). La condición de la alianza para 2029 **no depende de esta innovación** y sigue cumpliéndose. Se conserva además el reporte de intensidad como indicador de gestión, sin meta comprometida. | `[COMPLETADO]` |

---

### 3.6 Registro de la decisión sobre la quinta innovación · `[COMPLETADO]` — **decisión cerrada**

**Decisión: la innovación de tipo 5 es IN-05-A, la de sostenibilidad.** La alternativa evaluada se descarta, y la razón queda registrada porque la Comisión puede preguntar por qué no se eligió la dimensión social, que a primera vista parecía más humana.

**Alternativa evaluada y descartada — IN-05-B · Habilitación y micro-capacitación inclusiva del trabajador eventual en el punto de acceso.** Hasta 380 trabajadores eventuales por turno con rotación diaria, en tres turnos, con guantes y a la intemperie, en un terminal donde la biometría obligatoria está expresamente objetada por los acuerdos sindicales y donde el Caso declara que no pueden ser capacitados individualmente antes de cada faena.

**Las tres razones del descarte, en orden de peso:**

1. **Colisiona con un capítulo obligatorio completo de las Bases Técnicas Transversales.** El **Capítulo 22 — Capacitación y transferencia de conocimiento** regula la materia con nueve requisitos. El `RT-22.01` exige plan de capacitación estructurado **por perfil, incluyendo personas usuarias finales**; el `RT-22.02` exige **acompañamiento en puesto de trabajo durante la marcha blanca**; el `RT-22.04`, de carácter «según caso», exige que la capacitación **se programe por turnos considerando la estacionalidad y la ventana operacional**; y el `RT-22.09` ya valora un ambiente permanente de entrenamiento. **El delta de IN-05-B sobre ese capítulo es delgado**, y presentarla como innovación expondría a Terabyte exactamente a la crítica que el Artículo 30° usa para descartar: una funcionalidad exigida por las Bases presentada como innovación. Es el mismo filtro que se aplicó con rigor a las otras cuatro; no correspondía relajarlo aquí.
2. **Deja sin respuesta la instrucción del Capítulo 19.** El capítulo que fija cómo se evalúa este caso dice: *«Que la de sostenibilidad se articule con la exigencia concreta de la alianza naviera y no con una declaración general.»* Esa frase presupone que existe una innovación de sostenibilidad. Elegir otra dimensión deja la instrucción sin atender en el único capítulo que define la evaluación.
3. **IN-05-A tiene mayor consecuencia de negocio verificable.** Se ata a un hito externo con fecha —2029— y a una contraparte que representa el 34 % de los contenedores del terminal.

**Desventaja asumida de IN-05-A, y por qué se asume.** Su meta de reducción no puede fijarse en esta entrega, porque la línea base del Caso es literalmente «no se mide». Terabyte prefiere declarar esa limitación —como exige el T-22 al pedir que la investigación adicional se declare— antes que comprometer un porcentaje que no resistiría la defensa técnica.

**Lo valioso de IN-05-B no se pierde, se reubica.** El Caso advierte, a propósito de sus criterios de aceptación 21 y 22, que *«los dos hablan de personas, no de sistemas, y los dos son la prueba real de si la solución fue diseñada para esta operación o para un diagrama»*. Terabyte comparte ese criterio. El contenido de la alternativa —accesibilidad con guantes y a la intemperie, bilingüismo, validación de comprensión, diseño acordado con el sindicato, registro que pertenece al trabajador— se incorpora en dos lugares donde suma sin exponerse: como **criterio de diseño y estrategia con grupos de interés en el Subdocumento 3**, y como **exigencia propia del plan de capacitación del Subdocumento 6**, en el Informe 2.

> **Corroboración externa recibida el 2026-09-05.** La respuesta de coordinación de arquitectura llegó a la misma conclusión por su cuenta, sin conocer este registro: *«Uso con guantes y bilingüismo ya son exigencias obligatorias y no deben presentarse como innovación. El codiseño con el sindicato sí puede incorporarse a la estrategia de grupos de interés y a la validación de esas exigencias.»* Dos análisis independientes coincidieron en descartar IN-05-B por la misma razón y en reubicar su contenido en el mismo lugar. La decisión queda firme.

> **Traza de la decisión.** Adoptada por Célula 4 el 2026-09-05. Evidencia determinante: BTT, Cap. 22, `RT-22.01`, `RT-22.02`, `RT-22.04` y `RT-22.09`. Evidencia concurrente: CP, Cap. 19 y Cap. 18, nota sobre los criterios 21 y 22. Corroborada por la respuesta de coordinación del 2026-09-05. **`[PENDIENTE — Célula 2]`** acoger el contenido reubicado en la estrategia con grupos de interés del Subdocumento 3 — ya aceptado en principio por arquitectura.

---

## 4. Información faltante, por célula

### 4.1 Depende de Célula 3 — arquitectura

| # | Qué falta | A qué innovación bloquea | Criticidad |
|---:|---|---|---|
| 1 | ~~Arquitectura lógica y física redactada~~ **— reclasificada.** Arquitectura confirmó que el Maestro es el contrato común vigente y que sus IDs sirven como provisionales. El `RT-26.01` se satisface en el Informe 1 con la inserción provisional declarada; la trazabilidad definitiva bloquea recién en el Informe 2 | Las cinco | Baja para el Informe 1 |
| 2 | ~~Confirmación del catálogo de componentes~~ **— RESUELTO 2026-09-05.** Los IDs del Maestro §6.1 son vigentes y pueden usarse como provisionales hasta que A1 los congele | Las cinco | Cerrado |
| 3 | ~~Alta de `CTX-SIM`~~ **— RESUELTO 2026-09-05.** Aceptado provisionalmente como componente analítico en nube, sin autoridad operacional y sin competir con la autonomía de 72 h, tal como lo propusimos. A1/C1 ratifican después | IN-03 | Cerrado |
| 4 | **STRIDE — responsabilidad aclarada y tarea nueva para nosotros.** Lo elabora D2, pero **Innovaciones debe entregarle activos, datos, interfaces y flujo propuesto** de IN-01 e IN-03. En el Informe 1 basta declarar la dependencia | IN-01 y IN-03 | Media — insumo nuestro |
| 5 | **Reproducción por un tercero — reasignada a nosotros.** Arquitectura confirmó que la exige y que **el linaje lo diseña Datos, es decir Célula 4 en el Subdocumento 5**; Seguridad protege acceso, integridad y auditoría. La demostración final sigue pendiente | IN-04 | **Alta — es nuestra** |
| 6 | ~~Filas del T-11~~ **— RESUELTO 2026-09-05.** IN-03 no agrega hardware de terreno; solo iría al T-11 si finalmente se oferta cómputo, licencia o servicio cloud separado, y C4 determina capacidad y cantidad | IN-03 | Cerrado |
| 7 | **Confirmación de la inserción del término de emisiones** dentro del algoritmo de asignación de `CTX-YARD` sin degradar las metas de remociones ni de productividad | IN-05 | Media |

### 4.2 Depende de Célula 2 — solución, alcance y requisitos

| # | Qué falta | A qué innovación bloquea | Criticidad |
|---:|---|---|---|
| 8 | **Validación del no solapamiento — umbral rebajado.** Arquitectura aclaró que en el Informe 1 basta una justificación breve por innovación y que no hace falta una matriz firmada contra todos los RF. Nuestro numeral 13.1.4 excede ese umbral. La validación formal se necesita antes de congelar la cartera contractual | Las cinco | Media |
| 9 | ~~Si cada innovación genera RF propios~~ **— RESUELTO 2026-09-05.** No es obligatorio crear RF nuevos para el Informe 1. Si una innovación incorpora comportamiento contractual, se transformará en requisitos durante el refinamiento | Las cinco | Cerrado |
| 10 | **Confirmación del reparto por etapa de cada innovación**, y si altera el reparto 82/57 ya cerrado | Las cinco | Alta |
| 11 | ~~Discrepancia 82+56 frente a 82+57~~ **— RESUELTO 2026-09-05.** El corte vigente es **139 RF, 21 decisiones, 82/57**. Las cifras 138 y 82/56 son cortes históricos. Ya corregido en todo este documento | — | Cerrado |
| 12 | ~~Coordinación de la meta de IN-02~~ **— CONFIRMADO 2026-09-05.** IN-02 debe conservar coherencia con la meta vigente de atención con cita cumplida al menos 30 % más rápida. Ya es lo que dice nuestra ficha | IN-02 | Cerrado |
| 13 | ~~Incorporación de la consulta del §0.2 al registro de consultas~~ **— cerrada.** El comunicado del profesor resolvió que el costo y el precio de cada innovación corresponden al Informe 3. No hay que consultar nada | Las cinco | Cerrada |

### 4.3 Depende de Célula 1 — empresa y problema

| # | Qué falta | A qué innovación bloquea | Criticidad |
|---:|---|---|---|
| 14 | **Redacción final de las líneas base del Subdocumento 2.** Las cinco fichas citan cifras del Cap. 7 del Caso; deben coincidir literalmente con las que Célula 1 publique, para que la Comisión no encuentre dos versiones del mismo número | Las cinco | Media |
| 15 | **Dueño de la carga en el análisis de actores.** Arquitectura precisó que hoy está agrupado provisionalmente en `ACT-AGE` junto con embarcadores, importadores, exportadores y clientes, y que **Célula 1 debe explicitarlo** porque IN-01 e IN-02 le asignan participación activa | IN-01 y IN-02 | Media |

### 4.4 No depende de ninguna célula en esta etapa

| # | Qué falta | Dónde corresponde | Criticidad |
|---:|---|---|---|
| 16 | **Estructura de descomposición del trabajo y sus paquetes.** El `RT-26.02` los exige, pero la EDT es materia del Subdocumento 7 y del Formulario T-14, del **Informe 2** | Informe 2 | Declarada como hipótesis |
| 17 | **Cronograma detallado con nivelación de recursos** (T-14 y T-15) | Informe 2 | Declarada como hipótesis anclada al Art. 17° |
| 18 | **Valorización económica de las cinco innovaciones:** inversión, costo operacional y beneficio en el flujo de caja | **Informe 3** — Oferta Económica, Entregable 2, numeral 2.7 | Declarada, con la advertencia del Art. 53° |
| 19 | **Plan de riesgos formal** (Subdocumento 8 y Formulario T-16). Las fichas declaran riesgo, probabilidad, impacto, mitigación y contingencia conforme al `RT-26.04`, pero la escala de probabilidad e impacto la fija el plan de riesgos | Informe 2 | Media — hoy se usan escalas cualitativas |

### 4.5 Decisiones propias de Célula 4

| # | Qué falta decidir | Innovación | Criticidad |
|---:|---|---|---|
| 20 | ~~Cuál es definitivamente la quinta innovación~~ **— CERRADA el 2026-09-05: es IN-05-A, sostenibilidad.** La alternativa se descartó porque colisiona con el Capítulo 22 completo de las BTT. Registro y traza en el numeral 3.6. Pendiente solo la ratificación de Valentina | IN-05 | Cerrada |
| 21 | **Cuatro metas propias:** IN-01, IN-03, IN-04 e IN-05. Requieren derivación con evidencia, siguiendo el método que Célula 2 aplicó a sus 17 metas. **Reclasificada tras el comunicado: es exigible en el Informe 2, no en el Informe 1.** Para el 7 de septiembre basta con declararlas como investigación adicional, que es lo que la sección 2 hace | IN-01, IN-03, IN-04, IN-05 | Media — antes Alta |
| 22 | **Qué escala de madurez se declara para IN-04**, o si se declara que el `RT-26.03` no le aplica por no ser innovación de base tecnológica | IN-04 | Media |
| 23 | **Conjunto exacto de indicadores vinculados a remuneración** en IN-04 y momento de activación | IN-04 | Media |
| 24 | **Verificación de volumen y páginas de Giuliano y O'Brien (2007)** contra el original, y **forma de cita del GLEC Framework v3.2** —año y versión exacta de la publicación de Smart Freight Centre—. Ramírez-Nafarrate et al. (2017), Carlo et al. (2014), Hakimi et al. (2024), Selviaridis y Wynstra (2015), ISO 16290, RFC 3161 y RFC 6962 ya quedaron verificados | IN-02, IN-05 | Media |
| 25 | **Reparto de redacción con Valentina** entre el Subdocumento 5 —modelo y gestión de datos— y este Subdocumento 13. IN-01, IN-03 y IN-05 dependen de `DATA-TS` y `DATA-AN`, que son del Subdocumento 5: **la coherencia entre ambos subdocumentos es responsabilidad interna de nuestra célula** | Todas | **Alta** |
| 26bis | **Entregar a D2 los insumos del STRIDE de IN-01 e IN-03:** activos, datos, interfaces y flujo propuesto. Arquitectura lo elabora, pero el insumo es nuestro | IN-01, IN-03 | Media |
| 26ter | **Diseñar en el Subdocumento 5 el linaje que hace reproducible un indicador por un tercero**, desde el indicador hasta la transacción o evidencia de origen. Sostiene IN-04 y es responsabilidad de Datos, o sea de nosotros | IN-04 | **Alta** |
| 26quater | **Pedir los dos archivos que la respuesta de coordinación cita y no tenemos:** `04_GUIA_ARRANQUE_SUBDOCUMENTO_5.md` y `05_REGISTRO_ALINEACION_CELULA2.md`. El primero define qué puede desarrollar Datos antes del cierre de Arquitectura | Subdoc 5 | **Alta** |
| 26 | **Plantilla de portada y layout de Terabyte** para los dos PDF separados que exige el comunicado, y reparto de la exposición en la presentación preparatoria, donde el CLIENTE puede designar quién expone cada sección | Entrega | **Alta** |
| 27 | **Revisión de la redacción de IN-04 con el delegado**, para asegurar que no se lea como contrapropuesta del régimen de los Artículos 78° a 80°. Es el único punto de la cartera cuyo error no cuesta puntaje sino admisibilidad | IN-04 | **Alta** |

---

## 5. Referencias

Adams, C., Cain, P., Pinkas, D., & Zuccherato, R. (2001). *Internet X.509 public key infrastructure time-stamp protocol (TSP)* (RFC 3161). Internet Engineering Task Force. https://doi.org/10.17487/RFC3161

Carlo, H. J., Vis, I. F. A., & Roodbergen, K. J. (2014). Storage yard operations in container terminals: Literature overview, trends, and research directions. *European Journal of Operational Research, 235*(2), 412–430.

Giuliano, G., & O'Brien, T. (2007). Reducing port-related truck emissions: The terminal gate appointment system at the Ports of Los Angeles and Long Beach. *Transportation Research Part D: Transport and Environment*. `[Volumen, número y páginas pendientes de verificación contra el original. Artículo confirmado en cuanto a autoría, título, año y revista.]`

Hakimi, F., Khaled, T., Al-Kharaz, M., Foahom Gouabou, A. C., & Amzil, K. (2024). Towards a digital twin modeling method for container terminal port. *Procedia Computer Science, 246*, 3113–3121. https://doi.org/10.1016/j.procs.2024.09.361

International Organization for Standardization. (2013). *Space systems — Definition of the technology readiness levels (TRLs) and their criteria of assessment* (ISO 16290:2013).

International Organization for Standardization. (2019). *Greenhouse gases — Part 3: Specification with guidance for the verification and validation of greenhouse gas statements* (ISO 14064-3:2019).

International Organization for Standardization. (2023). *Greenhouse gases — Quantification and reporting of greenhouse gas emissions arising from transport chain operations* (ISO 14083:2023).

Laurie, B., Langley, A., & Kasper, E. (2013). *Certificate transparency* (RFC 6962). Internet Engineering Task Force. https://doi.org/10.17487/RFC6962

Ramírez-Nafarrate, A., González-Ramírez, R. G., Smith, N. R., Guerra-Olivares, R., & Voß, S. (2017). Impact on yard efficiency of a truck appointment system for a port terminal. *Annals of Operations Research, 258*(2), 195–216.

Selviaridis, K., & Wynstra, F. (2015). Performance-based contracting: A literature review and future research directions. *International Journal of Production Research, 53*(12), 3505–3540. https://doi.org/10.1080/00207543.2014.978031

Smart Freight Centre. (2023). *Global Logistics Emissions Council framework for logistics emissions accounting and reporting* (Version 3.0/3.2).

### Fuentes normativas del proceso

Bases Administrativas TFEP-01/2026 (FEP01.26): Artículos 16°, 17°, 28°, 29°, 30°, 53°, 57°, 78°, 92°; Formularios T-19, T-21 y T-22.

Bases Técnicas Transversales TFEP-01/2026 (FEP02.26): Capítulo 18 (inteligencia artificial), Capítulo 26 (innovaciones, RT-26.01 a RT-26.08), Anexo C (checklist de entregables, ítem 28).

Bases Técnicas del Caso 06 — Portuaria (FEP03.06.26): Capítulos 7, 9, 10, 11, 12, 13, 14, 16, 17, 18 y 19.

### Documentos internos del equipo utilizados como fuente

Célula 2. *Catálogo de requerimientos funcionales definitivo, partes 1 a 3* — corte vigente: 139 RF, 82 en Etapa 1 y 57 en Etapa 2.

Célula 2. *Registro de supuestos y decisiones v3* (21 decisiones y 17 metas comprometidas).

Célula 3. *Maestro de contexto de arquitectura, versión 1.0* (2026-09-04), §§2, 4, 6, 9, 10, 17, 18 y 19.

Célula 3. *Respuesta de coordinación — Subdocumento 5 e innovaciones*, 2026-09-05. Fija el corte vigente de 139 RF y 82/57, ratifica los IDs del Maestro como provisionales, acepta `CTX-SIM` como componente analítico en nube y resuelve el calendario de emisiones.

---

## 6. Obligaciones de forma y de presentación que fija el comunicado

Estas no estaban en la versión 1.0 de este documento y **son responsabilidad directa de Célula 4** para sus dos subdocumentos.

### 6.1 Formato de entrega

- **Cada subdocumento es un PDF separado.** No se acepta un archivo único que consolide todo el informe. Célula 4 entrega, por lo tanto, **dos PDF independientes**: Subdocumento 5 —modelo y gestión de datos— y Subdocumento 13 —innovaciones—.
- **Cada uno lleva portada propia, con el layout de Terabyte**, e indica como mínimo: empresa, proyecto, subdocumento con su título y su número, y fecha.
- **Lo que NO hay que hacer:** foliación, firmas, índices formales ni los requisitos de formato digital de los Artículos 39° y 40°. El comunicado los declara exigibles **exclusivamente para la propuesta final, en el Sobre N° 1**, y pide expresamente no destinar esfuerzo a ellos en esta etapa. La versión 1.0 de la guía interna del equipo los listaba como control formal del Informe 1; esa lectura queda corregida.
- **Consecuencia práctica:** hay que acordar con el equipo el layout y la plantilla de portada, porque debe ser el mismo en los seis subdocumentos. **`[PENDIENTE — decisión del equipo, probablemente Célula 1]`**, que es quien tiene la identidad corporativa de Terabyte del Subdocumento 1.

### 6.2 Presentación preparatoria

- Ponderan **10 % del puntaje final** (Art. 47.2). No es un trámite.
- La agenda es cerrada al contenido del T-22, con 15 minutos de exposición y 15 de preguntas.
- **Debe exponer más de un integrante, y el CLIENTE puede designar quién expone cada sección** (Art. 45.1). En la práctica: Valentina y yo tenemos que poder defender los dos subdocumentos, no uno cada uno.
- Célula 4 aporta al menos la lámina de las cinco innovaciones, y probablemente la de modelo de datos. **`[PENDIENTE — decisión propia de Célula 4]`** el reparto de exposición.

### 6.3 Efecto de las observaciones

Las observaciones que formule el CLIENTE en esta primera presentación **son vinculantes** (Art. 47.1) y desde el Informe 2 hay que incorporar la tabla de trazabilidad observación–respuesta–sección modificada (Art. 46°). Conviene que uno de los dos tome nota literal durante los 15 minutos de preguntas, porque de ahí sale esa tabla.

Y el recordatorio que el comunicado subraya: la retroalimentación del CLIENTE **no constituye aprobación de la solución** ni traslada responsabilidad sobre nuestras decisiones técnicas.

### 6.4 Títulos VI y VII

El comunicado aclara que los Artículos 67° a 82° no son entregable, pero **deben considerarse para el análisis de riesgo, la planificación y las reservas**. Para Célula 4 esto tuvo una consecuencia concreta e inmediata: al contrastar **IN-04** contra el Título VI apareció el riesgo cuarto de su ficha —que una innovación de modelo de contratación se lea como contrapropuesta del régimen de los Artículos 78° a 80°, lo que activaría la causal de inadmisibilidad del Artículo 53°—. **Ese hallazgo se debe enteramente a este punto del comunicado** y está incorporado en la ficha y en el numeral 13.5.

---

## 7. Lo que hay que hacer antes del 7 de septiembre

**Prioridad revisada tras el comunicado.** Lo urgente ya no son las fichas T-19, sino el texto del numeral 2 —secciones 13.1 a 13.7— y su PDF.

1. ~~Cerrar la decisión 20~~ **— hecho.** La quinta innovación es la de sostenibilidad. Falta que Valentina la ratifique formalmente, pero el fundamento y la traza ya están escritos en el numeral 3.6 y la redacción del subdocumento ya no está bloqueada.
2. **Revisar y aprobar el texto de los numerales 13.2 a 13.6** (sección 2 de este documento), que es el entregable real del 7 de septiembre según el comunicado.
3. **Revisar la redacción de IN-04 con el delegado.** Es la única innovación cuya redacción tiene riesgo de inadmisibilidad si se lee como contrapropuesta de las Bases. La declaración de que se suma al Artículo 78° y no lo modifica es obligatoria y no puede quedarse fuera por espacio.
4. **Acordar plantilla de portada y layout** con el equipo, y producir los dos PDF separados —Subdocumento 5 y Subdocumento 13— sin foliación ni firmas.
5. Pedir a Célula 3 la confirmación de las inserciones arquitectónicas y el alta de `CTX-SIM`. Si el Frente 1 no alcanza, el texto se entrega citando el Maestro §6.1, que es fuente vigente aprobada, con la dependencia declarada. **Ya no es bloqueante**, porque la trazabilidad con la arquitectura se exige en el Informe 2.
6. Verificar las referencias marcadas en la decisión 24.
7. Cruzar con Valentina que las series temporales y la capa analítica queden descritas en el Subdocumento 5 de forma coherente con lo que IN-01, IN-03 e IN-05 les exigen.
8. **Acusar recibo del comunicado**, que el propio correo pide expresamente. Si lo hace el delegado por el equipo, confirmarlo con él.

### Lo que ya no hay que hacer

- Completar los cinco T-19 para el 7 de septiembre. Quedan como trabajo anticipado.
- Formular la consulta sobre los campos económicos: el comunicado la respondió.
- Derivar las cuatro metas pendientes **para esta entrega**. Siguen siendo necesarias, pero para el Informe 2, cuando el alcance sea trazable con la arquitectura y la EDT. Lo que sí hay que hacer ahora es **declarar la investigación adicional**, que es lo que el T-22 exige y lo que la sección 2 ya hace en cada innovación.

---

## Anexo I — Verificación de citas normativas

Control corrido antes de la entrega, contra el texto de las tres bases. `BA, Art. 43.5` advierte que el CLIENTE registra qué proponentes identifican vacíos reales y cuáles solicitan aclaraciones sobre materias ya resueltas: citar mal resta.

### I.1 Recuento

| Veredicto | Citas |
|---|---:|
| **EXACTA** | 47 |
| **DESPLAZADA** | 1 |
| **SOBREEXTENDIDA** | 2 |
| **INEXISTENTE** | 1 |
| **CONTRADICHA** | 0 |

### I.2 Las cuatro citas que no pasaron, y su corrección

| Cita en el borrador v2.0 | Veredicto | Qué dice realmente la base | Corrección aplicada en v2.1 |
|---|---|---|---|
| «frente al terminal competidor», atribuido a `CP, Cap. 1` | **INEXISTENTE** | **El Caso 06 no menciona en ningún pasaje un terminal competidor.** Lo que `CP, Cap. 1` sí registra, tras la pérdida del 18 de febrero, es: *«La carga se perdió: seiscientos veinte mil dólares, cubiertos por el seguro. **El exportador no volvió**.»* | Se elimina la referencia al competidor en los tres puntos donde aparecía. El beneficio se reformula de «diferenciación» a **«retención comercial»**, anclado en la frase literal del Caso, que es más fuerte y sí existe |
| `CP, Cap. 8` citado como «entrevistas de transportistas», en plural y sin nombre | **SOBREEXTENDIDA** | Hay **una** entrevista de transporte terrestre: **Hernán Cifuentes Palma**, gerente general, 120 camiones, 30 % de su operación en este terminal | Se cita la entrevista por su nombre y se incorporan tres citas literales suyas. Ver I.3 |
| «beneficio de diferenciación comercial» de IN-01 | **SOBREEXTENDIDA** | El Caso no declara que el terminal compita por carga refrigerada con otro terminal; declara que perdió a un exportador | Reformulado como retención, no como diferenciación frente a un tercero |
| `Art. 17.2` como fuente de la medición diaria durante la marcha blanca | **DESPLAZADA** | La exigencia está en la **tabla del Art. 17.1**, fila de los meses 13 a 15: *«con plan de reversión activo y medición diaria de indicadores»*. El 17.2 regula el solapamiento de etapas | Corregida a `Art. 17.1` (ya aplicado en v2.0) |

### I.3 Hallazgo de fondo: la entrevista que sostiene IN-02

El control encontró que la innovación de proceso tenía una fuente **mucho más fuerte de la que estaba citada**. La entrevista de Hernán Cifuentes Palma en `CP, Cap. 8` no solo confirma el problema: **describe la solución**.

| Lo que dice la entrevista | Qué elemento de IN-02 sostiene |
|---|---|
| *«Yo no controlo cuándo está lista la carga. El packing me llama y me dice "ya, ven".»* | El problema, y además identifica al **packing como el dueño de la carga**, que es la tercera parte de la cita |
| *«Si me dan una cita a las diez y la fruta está a las tres, la cita no sirve y voy a llegar igual a las tres.»* | Por qué una cita simple no mueve el indicador |
| *«Tienen que ser citas que se puedan cambiar y que consideren que la mitad de mi operación no depende de mí.»* | **La reprogramación automática. Es literalmente lo que el transportista pidió** |
| *«Si me penalizan por no cumplir una cita que nunca pude cumplir, en dos semanas nadie va a usar el sistema.»* | Por qué no hay penalización, coincidiendo con la Decisión N° 6 de Célula 2 |
| *«Que yo sepa antes de mandar el camión si el contenedor está disponible y si los papeles están bien.»* | La confirmación previa a la salida del camión |

`CP, Cap. 8` advierte que distinguir *«el hecho de la opinión, la necesidad del capricho y el problema de la solución que la persona ya se imaginó»* es parte del trabajo profesional que se licita. Aquí la persona se imaginó la solución correcta, y conviene decirlo así en el informe en vez de presentarla como hallazgo propio.

### I.4 Cifras verificadas una a una contra su origen

Todas las cifras del documento se contrastaron contra `CP, Cap. 7` (indicadores del problema) y `CP, Cap. 14.1` (volumetría). **Ninguna discrepancia.**

78 min contra 45 · 3,2 km y 140 camiones · 22 % documentación · 71 % ventana · 24,8 mov/h contra 30 · 41 % instrucciones digitadas · 6 formatos de plano · 18 % remociones · 3,1 % mal ubicados · 40 min de búsqueda · 90 % ocupación en peak · 12 de 18 equipos con terminal · 0 de 2.400 tomas · 0 de 26 tableros · US$ 620.000, 38 contenedores, 9 horas · 28 % inspecciones atrasadas · 4,7 % facturas objetadas · 62 % objeciones aceptadas · emisiones «no se mide» · 6 % discrepancias VGM · 620 naves/año · 1.450 y 2.600 camiones/día · 18 + 42 + 14 = 74 equipos y hasta 88 · 2.400 y 2.900 tomas · 26 y 32 tableros · 142 cámaras · 14 navieras y 34 % de contenedores · 5 personas de TI · 380 eventuales por turno · 1.100 personas en peak · 16 diésel y 2 eléctricos · 62 % del volumen refrigerado entre enero y marzo · sala de 34 m² a menos de 300 m del mar.

### I.5 Artículos y códigos verificados como EXACTOS

**Bases Administrativas:** Art. 16° (modelo híbrido), 17.1 y 17.2 (cronograma de 56 meses y solapamiento), 28° (cinco tipos), 29° (siete elementos), 30.1, 30.2 y 30.3, 39° (documentación administrativa, Sobre N° 1), 40° (foliación, firmas, índices), 45.1 (obligatoriedad, 15+15, más de un expositor, el CLIENTE designa), 46° (tabla observación–respuesta–sección), 47.1 y 47.2 (vinculantes, 10 %), 53° (ambas causales invocadas), 78° (niveles de servicio), 79° (medición y datos exportables), 80° (multas y topes). Formularios T-19 (17 campos), T-21 (17 % del Informe 1) y T-22 (texto de innovaciones del Informe 1).

**Bases Técnicas Transversales:** Capítulo 18 (inteligencia artificial), **Capítulo 22 completo (RT-22.01 a RT-22.09, capacitación y transferencia de conocimiento — verificado al evaluar la alternativa descartada del numeral 3.6)**, Capítulo 26 completo (RT-26.01 a RT-26.08), Anexo C ítem 28.

**Caso 06:** Cap. 1, 6, 7.1, 7.2, 7.3, 9.1, 9.5, 9.10, 10 (restricciones 1, 2, 3, 9, 10, 11, 12, 13 y 14), 11 (exclusiones), 12, 13.1, 13.2, 13.3, 14.1, 16.1 (decisión pendiente N° 6), 17.4 (punto 14), 18 (criterios 1, 2, 10, 12, 15, 16 y 20) y 19.

### I.6 Advertencia sobre la calidad de las fuentes externas

| Fuente | Tipo | Puede sostener |
|---|---|---|
| ISO 14083:2023, ISO 14064-3:2019, ISO 16290:2013 | Norma internacional | Afirmación estructural |
| RFC 3161, RFC 6962 | Estándar publicado IETF | Afirmación estructural |
| Carlo, Vis y Roodbergen (2014); Ramírez-Nafarrate et al. (2017); Selviaridis y Wynstra (2015); Hakimi et al. (2024) | Literatura arbitrada | Afirmación estructural |
| GLEC Framework v3.2 | Publicación sectorial de Smart Freight Centre, no arbitrada | Marco de implementación, **no** afirmación estructural por sí sola — se apoya en ISO 14083, que sí lo es |
| Giuliano y O'Brien (2007) | Literatura arbitrada, **datos de cita incompletos** | Pendiente de completar volumen y páginas antes de la entrega |

**Ninguna afirmación estructural del documento descansa sobre una fuente no arbitrada.**
