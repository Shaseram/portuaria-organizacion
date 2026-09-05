# Registro de Reglas de Negocio (Caso 06 Portuaria)

**Equipo:** Terabyte — Esquema de solución y alcance (Isidora, Rodolfo)
**Subdocumento:** 3 — Esquema de solución y alcance — Anexo E
**Exigencia:** Capítulo 17.1 de las Bases Técnicas del Caso Portuaria (FEP03): *"Las reglas propias de la industria que la solución debe respetar y que este documento no explicita: criterio de asignación de posición en patio, reglas de segregación de carga peligrosa, prioridad entre nave y camión ante recursos escasos, cálculo de días de almacenaje, tolerancia de verificación de masa bruta, y criterios de liberación de un contenedor, entre otras."*

> **Nota sobre el formato:** a diferencia del catálogo de RF, el catálogo de RNF, el Registro de Supuestos y el Registro de Consultas —que sí tienen columnas exigidas explícitamente por las bases o por el checklist interno del equipo—, **ninguna base define un formato de columnas obligatorio para este registro.** El formato de abajo (Regla / Origen / Vinculación / Pendiente de validar) es una decisión de presentación propia, pensada para que cada regla quede trazable a su fuente y a lo ya declarado en el catálogo de RNF y en las 20 decisiones — no para llenar un formulario específico de las bases, porque ese formulario no existe.
>
> El checklist interno del equipo (`informe_1_requisitos_y_estructura.md`) amplía los 6 ejemplos del Cap. 17.1 a 8 temas obligatorios a considerar. Se cubren los 8 aquí.

---

## RN-01 — Asignación de posición en patio

**Regla:** La posición de un contenedor en el patio se asigna según el siguiente orden de prioridad: **(1)** compatibilidad de segregación obligatoria (mercancía peligrosa según la tabla del Código IMDG — ver RN-02 —, contenedor refrigerado en toma disponible, contenedor de dimensión especial en área habilitada); **(2)** proximidad a la fecha de recalada de la nave de exportación asociada, de modo que los contenedores con salida más próxima queden en posiciones de acceso más rápido, minimizando remociones futuras; **(3)** condiciones dinámicas de patio vigentes al momento de la asignación (equipo no disponible, bloque restringido — catálogo de condiciones dinámicas de la Decisión N° 5); **(4)** equilibrio de carga entre bloques, para evitar que un sector del patio se sature mientras otro queda subutilizado.

**Origen y fundamento:** el propio Cap. 17.1 identifica este criterio como uno que las bases deliberadamente no explicitan. Se construyó a partir del problema de fondo documentado en el levantamiento (18% de remociones evitables, Cap. 7) y de lo ya resuelto en las Decisiones N° 3, 4 y 5 sobre quién asigna la posición y cómo se actualiza ante condiciones cambiantes.

**Vinculación con el catálogo:** Decisión N° 3, Decisión N° 4, Decisión N° 5.

**¿Pendiente de validar con el cliente?** Sí. El orden entre "proximidad de recalada" y "equilibrio de carga" es un criterio nuestro; el jefe de operaciones real del terminal podría priorizarlos de otra forma.

---

## RN-02 — Segregación de mercancías peligrosas

**Regla:** Dos contenedores con mercancías peligrosas solo pueden asignarse a posiciones adyacentes si sus clases de riesgo son compatibles entre sí según la tabla de segregación del **Código Marítimo Internacional de Mercancías Peligrosas (Código IMDG)**; si son incompatibles, debe respetarse la distancia mínima de segregación que esa tabla exige entre ambas clases. El bloque de patio destinado a carga peligrosa permanece físicamente separado del resto del patio en todo momento.

**Origen y fundamento:** Código IMDG, de la Organización Marítima Internacional (OMI) — ya citado como fuente normativa en RNF-CUM-05.

**Vinculación con el catálogo:** RNF-CUM-05 (0 asignaciones que infrinjan la segregación IMDG).

**¿Pendiente de validar con el cliente?** No. Es una norma internacional cerrada y no admite interpretación del proponente; solo requiere coordinación con la autoridad marítima local durante la ejecución.

---

## RN-03 — Prioridad entre nave y camión ante recursos escasos

**Regla:** Cuando un mismo recurso compartido (grúa de patio, tractocamión, banda de acceso) sea requerido simultáneamente por una operación de atención de nave y por una operación de gate, **la atención de nave tiene prioridad**, salvo que atenderla implique incumplir un umbral de gate ya comprometido con un camión que inició su proceso, o que se esté dentro de un período donde la prioridad de nave ya esté excluida por otra restricción (congelamiento de temporada o ventana de atraque, Restricciones N° 9 y N° 10).

**Origen y fundamento:** el caso no explicita esta regla. Se infiere del Cap. 1, donde los indicadores comprometidos contractualmente con el concedente giran en torno a la estadía de la nave —con consecuencia económica directa—, mientras que el gate tiene un umbral de servicio interno sin penalidad concesional asociada.

**Vinculación con el catálogo:** RNF-DES-01 (umbral de gate), RNF-DES-07 (indicadores del concedente), Restricciones no negociables N° 9 y N° 10.

**¿Pendiente de validar con el cliente?** Sí, y es de las reglas más sensibles del registro — si el criterio operativo real fuera distinto (por ejemplo, "primero en llegar, primero en atender"), esta regla estaría equivocada y afectaría directamente la experiencia de los transportistas.

---

## RN-04 — Cálculo de días de almacenaje

**Regla:** El día de almacenaje se cuenta en **días corridos** (incluye fines de semana y festivos), a partir del día siguiente a la descarga del contenedor (importación) o del ingreso a patio (exportación) — el propio día de descarga/ingreso no cuenta como día 1. Se otorgan **3 días libres de almacenaje (free time)** antes de comenzar a generar cobro, salvo pacto distinto con el concedente o el cliente. El corte del cómputo diario ocurre a las 23:59 hora local.

**Origen y fundamento:** el caso solo declara que "el terminal cobra... por almacenaje según los días que el contenedor permanece en el patio" (Cap. 9), sin definir el método de conteo ni los días libres — es exactamente el vacío que el Cap. 17.1 pide llenar con una regla propia de la industria. Los 3 días libres y el conteo en días corridos son la convención más habitual de la industria portuaria.

**Vinculación con el catálogo:** RNF-CUM-08 (evidencia de hechos facturables), Decisión N° 11 (evento de sistema en el momento en que ocurre el hecho).

**¿Pendiente de validar con el cliente?** Sí — el número exacto de días libres (3) y si aplica igual a importación y exportación es una convención nuestra que afecta directamente los ingresos por almacenaje del cliente; debe confirmarse antes de comprometerla.

---

## RN-05 — Tolerancia de verificación de masa bruta (VGM)

**Regla:** Se considera una discrepancia de masa bruta cuando la diferencia entre el peso declarado por el exportador y el peso verificado en báscula supera el **5% del peso declarado**. Sobre ese umbral, el proceso se detiene, se notifica al embarcador y, si el peso verificado es el correcto, se genera una alerta al planificador de estiba para recalcular el plan afectado.

**Origen y fundamento:** la enmienda SOLAS sobre VGM no fija un porcentaje único a nivel internacional — cada país define su propia tolerancia (verificado: Países Bajos, Japón y Reino Unido usan 5%; Bélgica usa 2%). No se encontró una tolerancia publicada específicamente por la autoridad marítima chilena para este caso, por lo que se adopta el 5% por ser el valor más extendido internacionalmente. El caso confirma que hoy el 6% de los casos excede la tolerancia vigente (sea cual sea esta), lo que valida que el umbral debe mantenerse estricto y no ampliarse para "mejorar" artificialmente el indicador.

**Vinculación con el catálogo:** RNF-CUM-04 (100% de contenedores con VGM registrado y trazable).

**¿Pendiente de validar con el cliente?** Sí, y con prioridad alta — se recomienda consultar directamente a la autoridad marítima chilena o al cliente cuál es la tolerancia que efectivamente aplican hoy, en vez de asumir el 5% internacional sin confirmar.

---

## RN-06 — Criterios de liberación de un contenedor

**Regla:** Un contenedor solo puede salir del recinto, o ser cargado a la nave en el caso de exportación, cuando se cumplen **simultáneamente**: **(1)** documentación validada sin discrepancias; **(2)** autorización aduanera registrada; **(3)** sin retención vigente de la autoridad fitosanitaria o sanitaria; **(4)** sin deuda de facturación pendiente asociada al contenedor, salvo garantía o excepción autorizada por el cliente; **(5)**, para exportación, VGM verificado dentro de la tolerancia de RN-05.

**Origen y fundamento:** el caso no explicita esta regla; se construye combinando las obligaciones normativas ya identificadas en el Cap. 12 (aduana, SAG) con la práctica comercial estándar de no liberar carga con deuda pendiente.

**Vinculación con el catálogo:** RNF-CUM-04, RNF-CUM-06, RNF-CUM-07, RN-05.

**¿Pendiente de validar con el cliente?** Sí — en particular el punto (4): las condiciones comerciales de crédito con clientes recurrentes pueden ser distintas, y el concedente podría tener ya una política propia que reemplace esta regla.

---

## RN-07 — Gestión de citas y excepciones

**Regla:** Un camión con cita confirmada dispone de una **ventana de tolerancia de 30 minutos** (15 antes y 15 después de la hora asignada) para presentarse y mantener la prioridad de procesamiento declarada en la Decisión N° 6. Si llega fuera de esa ventana, pierde la prioridad de esa cita específica y se procesa como camión sin cita, pudiendo volver a agendar si el sistema tiene cupo disponible el mismo día. Un no-show (camión que no se presenta) no genera penalización económica, pero libera el cupo para reasignación inmediata.

**Origen y fundamento:** desarrollo operativo directo de la Decisión N° 6 (sistema de citas con incentivo de prioridad, sin multa), que dejó definida la lógica general pero no la tolerancia horaria específica ni el manejo del no-show.

**Vinculación con el catálogo:** Decisión N° 6.

**¿Pendiente de validar con el cliente?** Sí — los 30 minutos de tolerancia son un valor de referencia propio, a ajustar con el patrón real de llegada de camiones durante la marcha blanca.

---

## RN-08 — Escalamiento y confirmación de alarmas

**Regla:** Toda alarma de severidad crítica (patio refrigerado, brecha de seguridad, incidente de disponibilidad) debe ser confirmada por su primer destinatario dentro del plazo definido para ese tipo de alarma; si no hay confirmación dentro del plazo, el sistema escala automáticamente al siguiente destinatario, sin intervención manual para iniciar el escalamiento. Toda confirmación queda registrada con la identidad de quien confirma y su marca de tiempo.

**Origen y fundamento:** consolidación de una lógica que ya está declarada de forma dispersa en el catálogo (Decisión N° 10, RNF-DIS-08, RNF-SEG-07, RNF-SEG-11) para el caso específico del patio refrigerado y de seguridad de la información. Se agrupa aquí como una única regla de negocio transversal, extendida por analogía a cualquier alarma crítica futura que la solución incorpore.

**Vinculación con el catálogo:** Decisión N° 10, RNF-DIS-08, RNF-SEG-07, RNF-SEG-11.

**¿Pendiente de validar con el cliente?** Parcialmente. El mecanismo ya está validado en su origen específico (patio refrigerado); lo que sí debería confirmarse es que la misma lógica de escalamiento aplique sin modificación a otros tipos de alarma crítica que puedan surgir en el diseño detallado.

---

## Historial de cambios
- **[fecha]** — Creación del Registro de Reglas de Negocio con las 8 reglas exigidas por el Cap. 17.1 de FEP03 y el checklist interno del equipo. Ninguna base define un formato de columnas obligatorio para este registro; se documenta la decisión de formato propia al inicio del archivo.
