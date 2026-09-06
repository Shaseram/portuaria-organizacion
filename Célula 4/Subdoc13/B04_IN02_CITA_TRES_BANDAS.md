# B04 · IN-02 · Innovación de proceso

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Subdocumento 13 — Innovaciones**
> **Responsable:** Matías Reyes · **Corte:** 2026-09-06 · **Estado:** APROBADO — texto de entrega
> **Origen:** Numeral correspondiente del Subdocumento 13. Cubre los cinco ejes del Formulario T-22: idea, tecnología, alcance, forma de implementación y resultado esperado, más la declaración de investigación adicional.

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

