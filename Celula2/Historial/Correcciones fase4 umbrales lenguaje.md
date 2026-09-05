# Correcciones de la Fase 4 — Umbrales de aceptación y lenguaje
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Origen:** revisión adversarial independiente del catálogo de 128 RF, más el criterio de redacción del curso (`redaccion_requerimientos.md`).
> **Alcance:** correcciones 1 y 2 del plan de Fase 4 — criterios de aceptación sin umbral, y lenguaje prohibido.
> **Estado:** correcciones propuestas. Se aplican sobre los cinco bloques del catálogo tras la validación de la célula.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## 1. Por qué estas dos correcciones van primero
 
El material del curso es inequívoco sobre la consecuencia de un criterio sin umbral:
 
> «Un criterio sin umbral no se puede recibir ni rechazar: en la recepción no hay forma de declararlo cumplido, y **esa discusión la pierde siempre el proveedor**.»
>
> «Dejar el alcance o los requisitos ambiguos hace que lo ambiguo se interprete a favor del cliente, lo que **equivale técnicamente a regalar trabajo**.»
 
Los catorce criterios corregidos aquí no son un defecto de estilo. Cada uno es una discusión perdida de antemano en la recepción del entregable. Por eso van antes que el dominio faltante del tractocamión: una omisión se detecta y se agrega; un criterio inverificable se firma y se paga.
 
### 1.1 Regla de granularidad — ratificada, no modificada
 
La revisión planteó si requerimientos con dos cláusulas debían partirse. **La regla de la Fase 0 se mantiene**, y el material del curso la respalda:
 
> **La unidad de un requisito es la unidad de su prueba.** Si un solo procedimiento finito comprueba todas sus cláusulas, es un requisito. Si hacen falta dos pruebas independientes, y puede fallar una sin la otra, son dos.
 
Partir por número de verbos contradice las características **5 (concisa: «sin repeticiones ni relleno»)** y **6 (fácil de modificar: «sin redundancia»)** de la ERS. Ejemplo resuelto: `RF-CON-04` exige la aprobación de un segundo perfil **y** registra esa aprobación. No existe escenario en que se exija y no se registre; la prueba es una sola. **No se parte.**
 
Solo tres requerimientos del catálogo tienen dos pruebas genuinamente independientes, y se tratan en la corrección 6 del plan.
 
---
 
## 2. Corrección 1 — Criterios de aceptación sin umbral
 
Catorce criterios. La columna «Origen del umbral» indica de dónde sale la cifra: la mayoría ya existía en un RNF o en las bases y solo faltaba nombrarla.
 
### 2.1 Umbrales que ya existían y no se estaban citando
 
| Requisito | Criterio actual — defecto | Criterio corregido | Origen del umbral |
|---|---|---|---|
| `RF-REF-04` | «…se genera para el 100 % de ellas **dentro del umbral**» — el umbral no se nombra | «Se simula una desviación sobre una muestra de 30 tomas y se verifica que la alarma se genera para las 30 **en no más de 5 minutos desde el evento físico**» | CP, Cap. 15, RT-05.29 · RNF-DES-04 |
| `RF-REF-02` | «…sin que la detección de excepción **se retrase**» — sin definición de retraso | «Se verifica que el intervalo de reporte agregado se mantiene entre 5 y 15 minutos, y que la detección de excepción sigue ocurriendo **en no más de 5 minutos**, medida por inyección de falla» | CP, Cap. 15, RT-05.29 |
| `RF-PAT-12` | Mide «porcentaje de retiros que requirieron búsqueda física» — prueba otro requisito, no este | «La consulta devuelve bloque, bahía, fila, altura y estado de confianza **en no más de 1 segundo**, medido en el percentil 95 bajo carga de peak» | CP, Cap. 15, RT-09.01 |
| `RF-GAT-10` | Mide el tiempo agregado gate→instrucción, que depende de otros cinco requisitos | «La instrucción emitida corresponde a la asignación vigente de `RF-PAT-06` en el **100 % de una muestra de 200 despachos**» — el tiempo agregado pertenece a RNF-DES-01 | Separación de responsabilidades |
| `RF-CON-03` | «Salvo los explicados por **desfase temporal**» — la ventana nunca se declaró | «Ambos registros contienen el mismo hecho **en no más de 60 segundos**; toda diferencia mayor computa como divergencia» | **Umbral nuevo.** Ver 2.3 |
 
### 2.2 Umbrales que no existían en ninguna parte y hay que comprometer
 
Estos cinco son metas propias de Terabyte. Se declaran aquí y se incorporan al registro de supuestos con su derivación, igual que las once metas ya propuestas.
 
| Requisito | Criterio corregido | Derivación |
|---|---|---|
| `RF-GAT-05` | «Sobre una muestra de **500 contenedores** en condiciones reales de iluminación y suciedad de placa, la tasa de reconocimiento correcto del código, con dígito verificador validado, es **≥ 98 %**; el 2 % restante se resuelve por el procedimiento de excepción **sin digitación del código completo**» | El CP, Cap. 18 criterio 4 exige reconocimiento «sin digitación». Un umbral de 100 % es inalcanzable con placas sucias y luz variable, y comprometerlo sería regalar la recepción. El 98 % deja un residual manejable y explícito, con procedimiento declarado |
| `RF-GAT-04` | «El tiempo medio de atención del carril de excepción es **al menos 50 % mayor** que el del carril validado, medido sobre **100 atenciones de cada tipo**» | La Decisión N° 7 advierte que si el carril de excepción no es «claramente peor», se elimina el incentivo para validar antes. El 50 % es la magnitud mínima que un transportista percibe como diferencia de trato |
| `RF-GAT-02` | «El tiempo medio de procesamiento del grupo con cita cumplida es **al menos 30 % menor**, medido sobre **200 camiones de cada grupo** en franjas comparables» | Mismo razonamiento inverso: la prioridad debe ser perceptible para que la cita se adopte. La adopción es la variable que decide el resultado del sistema de citas (ver 2.4) |
| `RF-EMI-01` | «La medición instrumentada acumulada reconcilia con el combustible facturado a la empresa **dentro de ±3 %**, sobre un período de **3 meses**» | Tolerancia habitual de reconciliación de flujómetros. Sin período ni tolerancia el criterio es inejecutable |
| `RF-CON-09` | «El error del procedimiento de barrido, estimado por repetición sobre una muestra del mismo bloque, es **≤ 0,5 %**» | Se alinea con la meta del indicador de contenedores mal ubicados y con el umbral de detención de conciliación de la Decisión N° 1. Un barrido menos exacto que el umbral que debe verificar no sirve |
 
### 2.3 Umbrales que quedan pendientes de un dato del CLIENTE
 
Tres criterios invocan una holgura o ventana que depende de información que las bases no entregan. **No se inventa la cifra.** Se declara el parámetro, se fija un valor provisional derivado, y se marca su instancia de resolución.
 
| Requisito | Parámetro | Valor provisional | Se resuelve en |
|---|---|---|---|
| `RF-CON-03` | Ventana de desfase de la escritura dual | **60 segundos** | Puerta de decisión del mes 4 (Decisión N° 1). Depende de la latencia real de escritura hacia el sistema de 2012, que se mide en el levantamiento |
| `RF-INS-03` · `RF-INS-04` | Holgura de la remoción anticipada antes de la hora acordada | **Parámetro configurable, valor inicial 4 horas** | Levantamiento de los meses 1 a 4. Depende del plazo de aviso de cada autoridad, que el CLIENTE posee y no declaró (pendiente 8) |
| `RF-REF-07` | Intervalo de detección de sensor caído | **3 intervalos de muestreo consecutivos sin lectura**, es decir 3 a 15 minutos según el muestreo vigente de `RF-REF-01` | Derivado, no pendiente. Se cierra aquí |
 
El valor de la holgura de inspección se declara **parametrizable conforme a BTT, RT-16.02**, no codificado. Esto además responde a la exigencia de BTT, RT-16.04, que la revisión detectó ausente en todo el catálogo: declarar expresamente qué es parametrizable y qué requiere desarrollo, bajo sanción de «observación grave».
 
### 2.4 Un criterio que cambia de naturaleza
 
`RF-INT-01` comprometía «se recibe un plano por mensajería estándar **desde al menos una naviera**», mientras citaba CP, Cap. 15, RT-05.23, que exige «acreditar la factibilidad de su adopción con **las 14 navieras**». El requisito comprometía el mínimo y citaba el máximo.
 
**Corrección:** se desdobla el criterio en dos hitos, sin crear un requisito nuevo.
 
> «**Hito de factibilidad (cierre de desarrollo de Etapa 2):** se recibe y se incorpora un plano de estiba por mensajería estándar desde al menos una naviera representativa, sin digitación.
> **Hito de cobertura (cierre de la Operación del primer año):** las 14 navieras tienen su factibilidad acreditada, sea por integración efectiva o por acuerdo documentado de fecha de integración; las no integradas operan por el canal puente de `RF-INT-07`.»
 
Lo mismo aplica a `RF-INT-02`, cuyo criterio no comprometía meta alguna sobre el 41 % de instrucciones digitadas a mano: se compromete **≤ 5 % de instrucciones de embarque digitadas al cierre de la Etapa 2**, con el residual atribuible a navieras en canal puente.
 
---
 
## 3. Corrección 2 — Lenguaje
 
El material del curso agrega tres reglas que la convención de la Fase 0 no contemplaba.
 
### 3.1 Verbos de interpretación múltiple
 
> «Desconfíe de los verbos de interpretación múltiple: *manejar*, *rechazar*, *procesar*, *ignorar*.»
 
| Requisito | Verbo | Reemplazo |
|---|---|---|
| `RF-GAT-02` | «se **procesa** antes que» | «se **atiende** en un puesto de gate antes que» |
| `RF-GAT-04` | «camión **atendido** por el carril de excepción» — correcto, sin cambio | — |
| `RF-INT-05` | «**rechazar** y registrar todo mensaje» | «**no incorporar** el mensaje al plan ni al inventario, y registrar el descarte con su motivo» |
| `RF-ACC-05` | «**denegar** la emisión» — el material no lista *denegar*; se mantiene por ser un acto administrativo definido | — |
| `RF-INT-07`, `RF-POR-08` | «**procesamiento** parcial» | «**incorporación** de los registros válidos, con informe de error por cada registro inválido» |
| `RF-REF-02` | «agregar y **prefiltrar**» | «agregar y **descartar las lecturas redundantes** conforme a la regla declarada» |
 
### 3.2 Generalizaciones absolutas
 
> «Ante palabras como *siempre*, *cada* o *todos*, exigir la prueba formal que demuestre su cumplimiento.»
 
El catálogo usa «100 %» y «cero» en numerosos criterios. La regla no obliga a eliminarlos —muchos son correctos— sino a que **la prueba sea finita**. Se corrigen los que hoy exigen una prueba infinita:
 
| Requisito | Absoluto problemático | Corrección |
|---|---|---|
| `RF-CON-01` | «el 100 % de las transacciones atraviesan la fachada» sobre una ventana de 7 días | Se mantiene el 100 %, pero la prueba se declara finita: «sobre el registro de correlación de una ventana de 7 días en preproducción, con un volumen mínimo declarado de N transacciones» |
| `RF-PAT-07` | «cero asignaciones que infrinjan segregación» — universo infinito | «Batería de casos que cubra **todas las combinaciones de clase IMDG declaradas en el registro de reglas de negocio**, con cero infracciones. La batería se versiona junto al registro de reglas» |
| `RF-NAV-06` | «se verifica el cumplimiento de las seis restricciones» — circular | «Batería de **20 recaladas históricas reales**; el plan propuesto cumple las seis restricciones en las 20. **Cuando dos restricciones entren en conflicto, prevalece el orden declarado en el registro de reglas de negocio**, y la propuesta explicita cuál cedió» |
| `RF-POR-07` | «100 % de pantallas en ambos idiomas» | Se mantiene, pero el universo se acota: «sobre el catálogo de pantallas y plantillas **dirigidas a navieras y clientes internacionales**, enumerado en el anexo de interfaces» |
 
La corrección de `RF-NAV-06` cierra además un vacío real: el CP, Cap. 4.2 describe restricciones que **entran en conflicto entre sí** —peso, estabilidad, puerto de destino, disponibilidad de conexión refrigerada— y el catálogo no decía qué hacer cuando eso ocurre. Ahora remite al registro de reglas de negocio, que es donde corresponde y que ya es entregable de la célula.
 
### 3.3 Cálculos con dos ejemplos numéricos resueltos
 
> «Si el requisito especifica un cálculo matemático o lógico, se deben exigir **dos ejemplos numéricos resueltos**.»
 
Tres requerimientos del catálogo especifican un cálculo y deben llevarlos:
 
| Requisito | Cálculo | Qué se agrega |
|---|---|---|
| `RF-FAC-03` | Días de almacenaje | Dos ejemplos: uno con ingreso y salida dentro del mismo día calendario, y uno que cruce el cambio de mes, declarando el criterio de día completo o fracción |
| `RF-REF-13` | Horas de conexión refrigerada facturables | Dos ejemplos: uno con conexión continua, y uno con una desconexión intermedia registrada, declarando si el tiempo desconectado se descuenta |
| `RF-EMI-03` | Emisiones por contenedor movilizado | Dos ejemplos: un contenedor movido por equipo diésel y uno por equipo eléctrico, con los factores aplicados explícitos |
 
Los ejemplos se redactan al construir el registro de reglas de negocio, y se anexan a cada requisito. **Sin ellos los tres cálculos admiten más de una lectura**, que es exactamente lo que el Ejemplo 2 del material del curso advierte sobre la ambigüedad lógica y temporal.
 
### 3.4 Palabras subjetivas detectadas
 
| Requisito | Palabra | Corrección |
|---|---|---|
| `RF-POR-02` | «de forma autoservida y **segura**» | «con verificación de identidad conforme a BTT, RT-12.01, y segundo factor para todo acceso originado fuera de la red corporativa conforme a BTT, RT-12.03» |
| `RF-OPD-07` | «degradación **elegante**» | Se elimina del cuerpo; se conserva solo en el campo Origen como nombre del código BTT, RT-02.09 |
| `RF-ACC-10` | «datos **necesarios**» | Se reemplaza por la enumeración del catálogo de campos declarado. Ver corrección 6 del plan: este requisito además se parte |
| `RF-EMI-05` | «base **suficiente**» | «serie continua de al menos **24 meses** anteriores al primer reporte verificado» |
| `RF-PAT-09` | resultado esperado «instrucción visible y **comprensible**» | «instrucción visible sin acción del operador, con los elementos declarados en el checklist ergonómico por puesto de terreno» |
 
### 3.5 La convención «podrá» que no se estaba usando
 
La Fase 0 declaró «deberá» para lo obligatorio y «podrá» para lo deseable. La revisión detectó que **no hay un solo «podrá» en los 128 salvo `RF-ACC-04`**. Una convención declarada y no usada empeora el documento.
 
**Resolución:** la convención se mantiene, y se aplica donde corresponde. Los requerimientos que derivan de un código BTT etiquetado **«Deseable»** pasan a «podrá»:
 
| Requisito | Origen Deseable | Cambio |
|---|---|---|
| `RF-CON-02` | Parcialmente BTT, RT-05.16 (ver corrección 3) | Se mantiene «deberá»: su origen real es RT-05.17, Obligatorio |
| `RF-FAC-02` | Se apoyaba en BTT, RT-16.14, **Deseable** | La obligación se ancla en BTT, RT-16.02 (Obligatorio); RT-16.14 pasa a refuerzo declarado como Deseable |
| `RF-PAT-10` | No ratificado por la célula | **«podrá»** hasta su ratificación, y sale del conteo firme |
 
---
 
## 4. Efecto sobre el conteo
 
| | Requerimientos |
|---|---:|
| Catálogo original | 128 |
| `RF-PAT-10` pasa a condicionado, fuera del conteo firme | −1 |
| **Firmes tras las correcciones 1 y 2** | **127 + 1 condicionado** |
 
Las correcciones 1 y 2 **no agregan requerimientos**: corrigen los existentes. El crecimiento vendrá de las correcciones 5 y 6 del plan —dominio `RF-TRA`, control de capacidad de franjas, y los tres requisitos con doble prueba—.
 
---
 
## 5. Metas nuevas que estas correcciones incorporan al registro de supuestos
 
Cinco umbrales comprometidos aquí son metas propias y deben incorporarse al registro con su derivación, junto a las once ya declaradas:
 
| Meta | Valor | Requisito |
|---|---|---|
| Tasa de reconocimiento óptico del código de contenedor | ≥ 98 % | `RF-GAT-05` |
| Diferencial del carril de excepción | ≥ 50 % más lento | `RF-GAT-04` |
| Diferencial de prioridad por cita cumplida | ≥ 30 % más rápido | `RF-GAT-02` |
| Tolerancia de reconciliación de consumo de combustible | ± 3 % en 3 meses | `RF-EMI-01` |
| Error del procedimiento de barrido de inventario | ≤ 0,5 % | `RF-CON-09` |
| Instrucciones de embarque digitadas al cierre de Etapa 2 | ≤ 5 % | `RF-INT-02` |
 
Con estas seis, el registro de supuestos pasa de **11 a 17 metas propuestas**.
 
---
 
## 6. Pendientes que estas correcciones no cierran
 
| # | Pendiente | Corrección del plan |
|---:|---|---|
| 1 | Colisión de numeración RT entre BTT y CP Cap. 15; `RF-CON-02` (RT-05.16→RT-05.17); `RF-CON-08` (sobreextensión de BA Art. 78.2) | 3 |
| 2 | Siete RF que duplican un RNF con umbral y método idénticos — **requiere a Isidora** | 4 |
| 3 | Dominio `RF-TRA` (tractocamión) y control de capacidad de franjas de cita | 5 |
| 4 | Partir `RF-ACC-06`, `RF-ACC-10` y `RF-NAV-09` | 6 |
| 5 | Reescribir las metas 1, 2, 3 y 4 con la evidencia publicada, incluida la adversa | 7 |
| 6 | Redactar los dos ejemplos numéricos de `RF-FAC-03`, `RF-REF-13` y `RF-EMI-03` | 8, junto al registro de reglas de negocio |
| 7 | Declaración de frontera parametrizable / desarrollo exigida por BTT, RT-16.04 | 5 |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*
