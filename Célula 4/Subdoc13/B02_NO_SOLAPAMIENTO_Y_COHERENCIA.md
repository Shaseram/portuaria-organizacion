# B02 · No solapamiento con el alcance obligatorio y coherencia de la cartera

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Subdocumento 13 — Innovaciones**
> **Responsable:** Matías Reyes · **Corte:** 2026-09-06 · **Estado:** APROBADO — texto de entrega
> **Origen:** Numerales 13.1.4 a 13.1.6 del Subdocumento 13.

Este es el control que evita la causal de descarte del Artículo 30°: ninguna innovación puede ser una funcionalidad ya exigida por las Bases.

---

#### 13.1.4 Diferencia entre innovación y funcionalidad obligatoria

El Artículo 30° de las BA y el Capítulo 26 de las BTT prohíben lo mismo, con la misma frase: *«No se aceptará como innovación: la sola adopción de una tecnología que ya constituye estándar de la industria; la mención de una tendencia sin diseño de incorporación; ni una funcionalidad exigida por las Bases Técnicas presentada como innovación.»*

Terabyte aplicó ese filtro de forma verificable: **cada innovación candidata se contrastó contra los 139 requerimientos funcionales del catálogo de esta propuesta y contra las 21 decisiones de su registro de supuestos.** El resultado del contraste se declara aquí, requerimiento por requerimiento, para que la Comisión pueda verificarlo:

| Innovación | Requerimiento obligatorio más próximo | Qué obliga ese requerimiento | Qué agrega la innovación |
|---|---|---|---|
| **IN-01** | `RF-REF-08`, `RF-REF-11`, `RF-REF-12` | Notificar la alarma **al operador de turno y a un supervisor de guardia**; mantener la serie continua; permitir **descargar** la serie por autoservicio | El destinatario del aviso pasa a ser **el dueño de la carga**, que hoy no recibe nada; y la serie deja de ser un archivo descargable para convertirse en un **certificado sellado, verificable por un tercero sin depender del terminal**, ofrecido como servicio con nivel de servicio propio |
| **IN-02** | `RF-GAT-01`, `RF-GAT-02`, `RF-GAT-16`, Decisión N° 6 | Solicitar cita; priorizar a quien la cumple; limitar franjas por capacidad declarada; cola virtual que avisa al transportista **cuando el terminal se atrasa** | Incorpora al **dueño de la carga como tercera parte de la cita** y reprograma la franja automáticamente cuando confirma disponibilidad. Resuelve la mitad de la Decisión Pendiente N° 6 del numeral 16.1 que ninguna decisión resolvió: *«qué ocurre con el transportista que no controla cuándo estará lista la carga»* |
| **IN-03** | `RF-NAV-05`, `RF-GAT-16` | Estimar la duración de la nave a partir de serie histórica; limitar franjas por **capacidad declarada** | Ningún requerimiento dice **de dónde sale** la capacidad declarada ni permite ensayar un cambio de política antes de aplicarlo en producción. IN-03 provee el banco de ensayo fuera de línea. No existe requerimiento de simulación en el catálogo |
| **IN-04** | Ninguno | — | El catálogo no contiene ningún requerimiento sobre esquema contractual ni sobre modelo de remuneración. IN-04 no compite con ningún RF |
| **IN-05** | `RF-EMI-01` a `RF-EMI-06` | **Medir** el consumo, **calcular** la emisión por contenedor, **trazar** el cálculo, **acumular** la serie y **obtener** el reporte verificado | Ningún requerimiento obliga a **reducir**. IN-05 compromete una meta de intensidad —kg CO₂e por contenedor movilizado— y actúa sobre remociones evitadas, ralentí y asignación preferente de los dos equipos eléctricos existentes |

**Fuente:** Catálogo de requerimientos funcionales y Registro de supuestos y decisiones de esta propuesta, Subdocumento 3.

#### 13.1.5 Coherencia conjunta de la cartera

Las cinco no son cinco iniciativas sueltas. Comparten infraestructura y se sostienen unas a otras:

- **IN-03 alimenta a IN-02.** El gemelo es lo que produce la «capacidad declarada» de franjas que exige `RF-GAT-16` y lo que permite verificar, antes de tocar el gate real, si la reprogramación a tres bandas mejora o empeora la fila.
- **IN-01 e IN-05 comparten la misma cadena de evidencia.** Ambas dependen de `SRV-EVID` y de la trazabilidad hasta el dato de origen; una la usa para temperatura, la otra para emisiones. El sellado se construye una vez.
- **IN-04 depende de que IN-02 e IN-05 sean medibles.** Un compromiso de resultado solo es defendible si el indicador que lo verifica lo produce el propio sistema de forma trazable y reproducible por un tercero, que es exactamente lo que exige `RF-CON-11` —producción trazable de los indicadores del concedente— y la Restricción no negociable N° 14.
- **Ninguna de las cinco toca el control de grúas de muelle, la emisión tributaria del ERP, el VMS ni la báscula.** Las cuatro exclusiones del Capítulo 11 del Caso 06 se respetan íntegramente.
- **Ninguna de las cinco añade una interacción del operador en el patio.** IN-05 opera como término de puntuación dentro de un algoritmo que ya asigna; IN-03 no tiene autoridad operacional; IN-01 e IN-02 actúan sobre canales externos. La Restricción no negociable N° 1 se respeta por diseño, no por declaración.

#### 13.1.6 Relación con las etapas y con el alcance

El reparto por etapas sigue el alcance definido en el Subdocumento 3 para los requerimientos que cada innovación aprovecha, y el cronograma contractual obligatorio de 56 meses del Artículo 17° de las Bases Administrativas:

| Fase contractual | Meses | Qué de la cartera ocurre allí |
|---|---|---|
| Etapa 1 · Desarrollo | 1 a 12 | IN-05 inicia captura de consumo desde el mes 1 (`RF-EMI-05`); el cálculo de intensidad existe aquí solo como prototipo y prevalidación. IN-03 v1 se construye con los meses 6 a 12. IN-02 se construye sobre el gate de Etapa 1. IN-01 fase A depende del despliegue de instrumentación reefer de Etapa 1 |
| Etapa 1 · Marcha blanca | 13 a 15 | **IN-02 se mide aquí** — cumple el `RT-26.08` deseable. IN-01 fase A opera con aviso por canal directo |
| Etapa 1 · Producción | 16 | IN-04 entra en vigencia contractual con la primera medición oficial |
| Etapa 2 · Desarrollo | 13 a 18 | IN-01 fase B (certificado autenticado por portal, que depende de `RF-POR-02`, de Etapa 2). IN-03 v2 |
| Etapa 2 · Marcha blanca | 19 a 20 | IN-01 fase B en convivencia |
| Etapa 2 · Producción | 21 | IN-05 entra con motor de cálculo productivo y activa el término de reducción. IN-04 en régimen pleno |
| Operación | 21 a 56 | Las cinco en régimen; IN-05 acumula la trayectoria que se presenta a la alianza en 2029 |

La asignación de cada innovación a paquetes de la estructura de descomposición del trabajo y las fechas finas del cronograma se establecen en el Subdocumento 7 y en el Formulario T-14, y se presentan en el Informe 2 conforme a la progresión que fija el Formulario T-22.
