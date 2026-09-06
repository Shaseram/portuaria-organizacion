# B05 · IN-03 · Innovación tecnológica o de arquitectura

> **Caso:** 06 Portuaria — TERABYTE · **Célula 4** · **Subdocumento 13 — Innovaciones**
> **Responsable:** Matías Reyes · **Corte:** 2026-09-06 · **Estado:** APROBADO — texto de entrega
> **Origen:** Numeral correspondiente del Subdocumento 13. Cubre los cinco ejes del Formulario T-22: idea, tecnología, alcance, forma de implementación y resultado esperado, más la declaración de investigación adicional.

---

#### 13.4 Innovación tecnológica o de arquitectura — Gemelo de operación del Terminal Aconcagua

**Idea.** En este terminal **no existe dónde ensayar un cambio.** Está prohibido intervenir entre el 15 de diciembre y el 30 de abril; está prohibido intervenir durante la atención de una nave y en las cuatro horas previas a una ventana confirmada, con 620 recaladas al año; el patio opera al 90 % en temporada y la operación es 24x7x365 sin ventana de detención. Toda decisión operacional relevante se toma hoy sin poder probarla, y se prueba en producción con una nave amarrada. La innovación es **un banco de decisiones fuera de línea**: un modelo del terminal, calibrado con la telemetría que el propio proyecto instala, donde el cambio se ensaya antes de tocar la operación.

**Tecnología que la sustenta.** Simulación de eventos discretos del ciclo completo —llegada de camión, gate, asignación de posición, movimiento de patio, tractocamión, grúa de muelle, ventana de nave—, **calibrada contra la telemetría real** de equipos y los eventos de gate que la solución produce de todos modos. La calibración es lo que lo distingue de un modelo de escritorio: el gemelo se contrasta contra la operación observada y **declara su error junto a cada resultado**. En su versión comprometida **no incorpora inteligencia artificial**; si se incorporara, quedaría sujeta íntegramente al Capítulo 18 de las Bases Técnicas Transversales, conforme al `RT-26.06`.

**Alcance.** Versión 1: gate y flujo del camión. Versión 2: patio, nave y planificación. **Restricción de alcance que es parte de la innovación: el gemelo no tiene autoridad operacional.** No expone ninguna interfaz de escritura hacia los contextos operacionales, no emite órdenes y su indisponibilidad no degrada ninguna función. Se despliega en nube y nunca en el borde, precisamente para no competir por la capacidad local que sostiene las cinco funciones críticas durante las 72 horas sin enlace.

**Forma de implementación.** Componente nuevo, alimentado exclusivamente desde la capa analítica y desde las series temporales de telemetría. Se incorpora al catálogo de componentes del Subdocumento 4, con su emplazamiento justificado conforme al Artículo 16° de las Bases Administrativas. La interdicción de escritura se verifica en la matriz de segregación de funciones del servicio de identidad, de modo que sea auditable y no una declaración.

**Resultado esperado.** Tres cosas concretas. Que cada cambio de política de patio o de gate que hoy solo puede probarse con una nave amarrada pase a probarse en el modelo. Que la «capacidad declarada» que limita las franjas de cita —un parámetro que los requerimientos exigen pero cuyo origen ninguno define— tenga por fin un fundamento. Y que la pregunta del Caso sobre qué componente se satura primero en el peak y ante la eventual incorporación de un cuarto sitio entre 2030 y 2032 se responda con un modelo en vez de con una opinión.

**Investigación adicional declarada.** El nivel de madurez se declara como **rango, TRL 6 a 7 en la escala ISO 16290:2013**, y no como valor único, porque depende de la calidad de la calibración, que a su vez depende de instrumentación que hoy no existe: solo 12 de los 18 equipos de patio tienen terminal montada. La meta de error del gemelo no puede fijarse antes de conocer la densidad real de la telemetría instalada.

