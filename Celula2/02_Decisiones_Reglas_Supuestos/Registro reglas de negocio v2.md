# Registro de Reglas de Negocio — versión consolidada
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Subdocumento 3 · Anexo E** · **Versión 2.2 — reemplaza a `registro_reglas_de_negocio.md` y a la parte de reglas de `complemento_reglas_negocio_y_rf_pat_10.md`.**
> **Autoría:** RN-01 a RN-08, Isidora Cisternas. RN-09 y RN-10, y la corrección del fundamento de RN-03, Rodolfo Fernández.
> **Exigencia:** CP, Cap. 17.1 — *«Las reglas propias de la industria que la solución debe respetar y que este documento no explicita: criterio de asignación de posición en patio, reglas de segregación de carga peligrosa, prioridad entre nave y camión ante recursos escasos, cálculo de días de almacenaje, tolerancia de verificación de masa bruta, y criterios de liberación de un contenedor, entre otras.»*
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## Índice
 
| Regla | Materia | Estado | Validar con el cliente |
|---|---|---|---|
| **RN-01** | Asignación de posición en patio | Vigente | Sí |
| **RN-02** | Segregación de mercancías peligrosas | Vigente | No — norma internacional cerrada |
| **RN-03** | Prioridad entre nave y camión ante recursos escasos | **Regla y fundamento corregidos** | Sí — de las más sensibles |
| **RN-04** | Cálculo de días de almacenaje | Vigente | Sí |
| **RN-05** | Tolerancia de verificación de masa bruta | Vigente | **Sí, prioridad alta** |
| **RN-06** | Criterios de liberación de un contenedor | Vigente | Sí |
| **RN-07** | Gestión de citas y excepciones | Vigente | Sí |
| **RN-08** | Escalamiento y confirmación de alarmas | Vigente | Parcialmente |
| **RN-09** | **Precedencia entre restricciones del plan de estiba** | **Nueva** | **Sí, prioridad alta** |
| **RN-10** | **Tiempo desconectado en la facturación de conexión refrigerada** | **Nueva** | Sí |
| **RN-11** | **Tolerancia de desviación de temperatura en carga refrigerada** | **Nueva** | **Sí, prioridad alta** |
 
**Nota sobre el formato.** Ninguna base define un formato de columnas obligatorio para este registro, a diferencia del catálogo de RF, del catálogo de RNF y del registro de supuestos. El formato —Regla / Origen y fundamento / Vinculación / Pendiente de validar— es una decisión de presentación propia, pensada para que cada regla quede trazable a su fuente y a lo ya declarado en el resto del catálogo.
 
El checklist interno del equipo amplía los seis ejemplos del Cap. 17.1 a **ocho temas obligatorios**. Los ocho están cubiertos por RN-01 a RN-08. RN-09 y RN-10 son adiciones propias detectadas al cruzar el registro con el catálogo de requerimientos funcionales.
 
---
 
## RN-01 — Asignación de posición en patio
 
**Regla.** La posición de un contenedor en el patio se asigna según el siguiente orden de prioridad:
 
1. **Compatibilidad de segregación obligatoria** — mercancía peligrosa según la tabla del Código IMDG (ver RN-02), contenedor refrigerado en toma disponible, contenedor de dimensión especial en área habilitada.
2. **Proximidad al siguiente hito operacional comprometido**: para exportación, la recalada/carga de la nave; para importación, la cita de retiro, inspección u otra salida comprometida. El contenedor con hito más próximo queda en una posición de acceso más rápido, minimizando remociones futuras.
3. **Condiciones dinámicas de patio vigentes** al momento de la asignación —equipo no disponible, bloque restringido—, conforme al catálogo de la Decisión N° 5.
4. **Equilibrio de carga entre bloques**, para evitar que un sector del patio se sature mientras otro queda subutilizado.
**Origen y fundamento.** El Cap. 17.1 identifica este criterio como uno que las bases deliberadamente no explicitan. Se construyó a partir del problema documentado en el levantamiento —18 % de remociones evitables (CP, Cap. 7)— y de lo resuelto en las Decisiones N° 3, 4 y 5 sobre quién asigna la posición y cómo se actualiza ante condiciones cambiantes.
 
**Vinculación.** Decisiones N° 3, 4 y 5 · `RF-PAT-06` (asignación algorítmica) · `RF-PAT-08` (condiciones dinámicas).
 
**¿Pendiente de validar?** **Sí.** El orden entre «proximidad del siguiente hito» y «equilibrio de carga» es criterio propio; el jefe de operaciones debe confirmar además qué evento constituye el hito exigible para cada flujo de importación.
 
---
 
## RN-02 — Segregación de mercancías peligrosas
 
**Regla.** Dos contenedores con mercancías peligrosas solo pueden asignarse a posiciones adyacentes si sus clases de riesgo son compatibles entre sí según la tabla de segregación del **Código Marítimo Internacional de Mercancías Peligrosas (IMDG)**. Si son incompatibles, debe respetarse la distancia mínima de segregación que esa tabla exige entre ambas clases. El bloque de patio destinado a carga peligrosa permanece físicamente separado del resto del patio en todo momento.
 
**Origen y fundamento.** Código IMDG, de la Organización Marítima Internacional · CP, Cap. 12, materia 6, que advierte que la norma «restringe la libertad del algoritmo de patio».
 
**Vinculación.** RNF-CUM-05 (cero asignaciones que infrinjan la segregación) · `RF-PAT-07` · RN-09, nivel 2.
 
**¿Pendiente de validar?** **No.** Es una norma internacional cerrada que no admite interpretación del proponente; solo requiere coordinación con la autoridad marítima local durante la ejecución.
 
---
 
## RN-03 — Prioridad entre nave y camión ante recursos escasos
 
> **Regla y fundamento corregidos.** Se mantiene la prioridad central de la nave; se elimina la excepción que confundía restricciones de intervención técnica con asignación de recursos operacionales, y se conserva la protección del camión cuyo proceso de gate ya comenzó.
 
**Regla.** Cuando un mismo recurso compartido —grúa de patio, tractocamión, banda de acceso— sea requerido simultáneamente por una operación de atención de nave y por una operación de gate, **la atención de nave tiene prioridad**, salvo que atenderla implique incumplir un umbral de gate ya comprometido con un camión que **inició su proceso**.
 
**Origen y fundamento.** El caso no explicita esta regla. La prioridad de la nave se funda en una **asimetría de irreversibilidad y de costo por unidad de tiempo**, no en una diferencia de exigibilidad contractual:
 
1. **La nave consume un recurso que no se recupera.** «Una nave amarrada consume tiempo de muelle desde el momento en que amarra» (CP, Cap. 10, restricción no negociable N° 2). El muelle tiene tres sitios y seis grúas; el tiempo de sitio perdido no se repone.
2. **El costo por hora es conocido y asimétrico.** «Cada hora de espera de una nave portacontenedores tiene un costo que la naviera conoce con precisión y que el terminal no calcula» (CP, Cap. 4.1). Una hora de nave detenida equivale, a 24,8 movimientos por hora, a unos 25 movimientos perdidos que desplazan toda la programación siguiente.
3. **El camión admite reprogramación; la nave no.** Un camión puede esperar, reagendar o volver; una ventana de atraque desplazada arrastra a la nave siguiente.
> **Corrección del fundamento anterior.** La versión previa sostenía que «el gate tiene un umbral de servicio interno **sin penalidad concesional asociada**». **Eso no se sostiene contra el caso:** la estadía del camión **es** uno de los indicadores comprometidos con el concedente (CP, Anexo C), la restricción no negociable N° 14 obliga a producirlo «de forma trazable y auditable, no reconstruirlo», acumula **tres semestres consecutivos sobre el umbral** (CP, 7.1), CP, 13.2 advierte que «cada semestre adicional agrava la situación contractual», y el criterio de aceptación N° 1 lo exige «sostenido y auditable». El gate sí tiene consecuencia concesional, y de las peores del caso.
 
**Salvaguarda reforzada.** Precisamente porque la estadía del camión tiene consecuencia concesional en curso, la excepción deja de ser una cortesía y pasa a ser la **protección de un indicador en incumplimiento**: la prioridad de nave **no** puede aplicarse sobre un camión cuyo proceso de gate ya se inició, ni de forma que el indicador de estadía del turno supere el umbral comprometido.
 
**Vinculación.** RNF-DES-01 (umbral de gate) · RNF-DES-07 (indicadores del concedente) · restricción no negociable N° 14 · `RF-TRA-02` (asignación de tractocamión) · `RF-GAT-12` (cálculo trazable de la estadía).
 
**¿Pendiente de validar?** **Sí, y es de las más sensibles del registro.** Si el criterio operativo real fuera distinto —por ejemplo «primero en llegar, primero en atender»—, esta regla estaría equivocada y afectaría directamente la experiencia de los transportistas.
 
---
 
## RN-04 — Cálculo de días de almacenaje
 
**Regla.** El día de almacenaje se cuenta en **días corridos** —incluye fines de semana y festivos—, a partir del **día siguiente** a la descarga del contenedor (importación) o al ingreso a patio (exportación); el propio día de descarga o ingreso no cuenta como día 1. Se otorgan **3 días libres de almacenaje** antes de comenzar a generar cobro, salvo pacto distinto con el concedente o el cliente. El corte del cómputo diario ocurre a las **23:59 hora local**.
 
**Ejemplos numéricos.**
 
> **Ejemplo A — dentro del mismo mes.** Descargado el 4 de marzo a las 08:30; retirado el 11 de marzo a las 16:00.
> Conteo desde el 5 de marzo. Días transcurridos hasta el 11: **7**. Días libres: 3. **Días facturables: 4** (8, 9, 10 y 11 de marzo).
>
> **Ejemplo B — cruzando el cambio de mes.** Descargado el 27 de marzo a las 22:15; retirado el 3 de abril a las 09:00.
> Conteo desde el 28 de marzo. Días transcurridos hasta el 3 de abril: **7** (28, 29, 30 y 31 de marzo; 1, 2 y 3 de abril). Días libres: 3. **Días facturables: 4** (31 de marzo; 1, 2 y 3 de abril).
>
> La hora de ingreso y de retiro no altera el conteo, y el cambio de mes no reinicia el cómputo.
 
**Origen y fundamento.** El caso solo declara que el terminal cobra «por almacenaje según los días que el contenedor permanece en el patio» (CP, Cap. 9), sin definir el método de conteo ni los días libres — exactamente el vacío que el Cap. 17.1 pide llenar con una regla propia de la industria. Los 3 días libres y el conteo en días corridos son la convención más habitual del sector.
 
**Vinculación.** Decisión N° 11 · `RF-FAC-03` (cálculo de días de almacenaje) · `RF-GAT-11` (eventos de barrera que lo determinan).
 
**¿Pendiente de validar?** **Sí.** El número exacto de días libres y si aplica igual a importación y exportación es una convención nuestra que **afecta directamente los ingresos por almacenaje del cliente**; debe confirmarse antes de comprometerla.
 
---
 
## RN-05 — Tolerancia de verificación de masa bruta (VGM)
 
**Regla.** Se considera una discrepancia de masa bruta cuando la diferencia entre el peso declarado por el exportador y el peso verificado en báscula supera el **5 % del peso declarado**. Sobre ese umbral, el proceso se detiene, se notifica al embarcador y, si el peso verificado es el correcto, se genera una alerta al planificador de estiba para recalcular el plan afectado.
 
**Ejemplos numéricos.**
 
> **Ejemplo A — dentro de tolerancia.** Declarado 24.000 kg; verificado 24.900 kg. Diferencia 900 kg = **3,75 %**. No hay discrepancia; la operación continúa.
>
> **Ejemplo B — sobre tolerancia.** Declarado 24.000 kg; verificado 25.400 kg. Diferencia 1.400 kg = **5,83 %**. Hay discrepancia: la operación se detiene, se notifica al embarcador y el plan afectado se marca para replanificación.
>
> El porcentaje se calcula siempre sobre el peso **declarado**, no sobre el verificado.
 
**Origen y fundamento.** La enmienda SOLAS sobre VGM no fija un porcentaje único a nivel internacional: cada país define su propia tolerancia. Verificado que Países Bajos, Japón y Reino Unido usan 5 %, y Bélgica 2 %. **No se encontró una tolerancia publicada específicamente por la autoridad marítima chilena** para este caso, por lo que se adopta el 5 % por ser el valor más extendido internacionalmente. El caso confirma que hoy el 6 % de los casos excede la tolerancia vigente, sea cual sea esta, lo que valida que el umbral debe mantenerse estricto y no ampliarse para «mejorar» artificialmente el indicador.
 
**Vinculación.** RNF-CUM-04 · `RF-GAT-09` (gestión de la discrepancia) · `RF-NAV-14` (replanificación) · RN-06, punto 5 · RN-09, nivel 1.
 
**¿Pendiente de validar?** **Sí, con prioridad alta.** Se recomienda consultar directamente a la autoridad marítima chilena o al cliente cuál es la tolerancia que efectivamente aplican hoy, en vez de asumir el 5 % internacional sin confirmar.
 
---
 
## RN-06 — Criterios de liberación de un contenedor
 
**Regla.** Un contenedor solo puede salir del recinto, o ser cargado a la nave en el caso de exportación, cuando se cumplen **simultáneamente**:
 
1. Documentación validada sin discrepancias.
2. Autorización aduanera registrada.
3. Sin retención vigente de la autoridad fitosanitaria o sanitaria.
4. Sin deuda de facturación pendiente asociada al contenedor, salvo garantía o excepción autorizada por el cliente.
5. Para exportación, VGM verificado dentro de la tolerancia de RN-05.
**Origen y fundamento.** El caso no explicita esta regla; se construye combinando las obligaciones normativas del CP, Cap. 12 —aduana, SAG— con la práctica comercial estándar de no liberar carga con deuda pendiente.
 
**Vinculación.** RNF-CUM-04, RNF-CUM-06, RNF-CUM-07 · RN-05 · `RF-GAT-03` (validación documental) · `RF-INS-05` (retención por inspección).
 
**¿Pendiente de validar?** **Sí**, en particular el punto 4: las condiciones comerciales de crédito con clientes recurrentes pueden ser distintas, y el concedente podría tener ya una política propia que reemplace esta regla.
 
---
 
## RN-07 — Gestión de citas y excepciones
 
**Regla.** Un camión con cita confirmada dispone de una **ventana de tolerancia de 30 minutos** —15 antes y 15 después de la hora asignada— para presentarse y mantener la prioridad de atención declarada en la Decisión N° 6. Si llega fuera de esa ventana, pierde la prioridad de esa cita específica y se atiende como camión sin cita, pudiendo volver a agendar si el sistema tiene cupo disponible el mismo día. Un **no-show** —camión que no se presenta— no genera penalización económica, pero libera el cupo para reasignación inmediata.
 
**Origen y fundamento.** Desarrollo operativo directo de la Decisión N° 6 —sistema de citas con incentivo de prioridad, sin multa—, que dejó definida la lógica general pero no la tolerancia horaria específica ni el manejo del no-show.
 
**Vinculación.** Decisión N° 6 · `RF-GAT-01` (solicitud de cita) · `RF-GAT-02`, que emplea esta regla como **definición de «cita cumplida»** · `RF-GAT-16` (límite de franjas por capacidad).
 
**¿Pendiente de validar?** **Sí.** Los 30 minutos de tolerancia son un valor de referencia propio, a ajustar con el patrón real de llegada de camiones durante la marcha blanca.
 
---
 
## RN-08 — Escalamiento y confirmación de alarmas
 
**Regla.** Toda alarma de severidad crítica —patio refrigerado, brecha de seguridad, incidente de disponibilidad— debe ser confirmada por su primer destinatario dentro del plazo definido para ese tipo de alarma. Si no hay confirmación dentro del plazo, el sistema escala automáticamente al siguiente destinatario, **sin intervención manual para iniciar el escalamiento**. Toda confirmación queda registrada con la identidad de quien confirma y su marca de tiempo.
 
**Origen y fundamento.** Consolidación de una lógica declarada de forma dispersa en el catálogo —Decisión N° 10, RNF-DIS-08, RNF-SEG-07, RNF-SEG-11— para el caso específico del patio refrigerado y de seguridad de la información. Se agrupa aquí como una única regla transversal, extendida por analogía a cualquier alarma crítica futura que la solución incorpore.
 
**Vinculación.** Decisión N° 10 · RNF-DIS-08, RNF-SEG-07, RNF-SEG-11 · `RF-REF-08`, `RF-REF-09` y `RF-REF-10`.
 
**¿Pendiente de validar?** **Parcialmente.** El mecanismo ya está validado en su origen específico —patio refrigerado—; lo que debería confirmarse es que la misma lógica de escalamiento aplique sin modificación a otros tipos de alarma crítica que surjan en el diseño detallado.
 
---
 
## RN-09 — Precedencia entre restricciones del plan de estiba
 
> **Regla nueva.** RN-01 resuelve la precedencia **en patio**. El CP, Cap. 4.2 enumera para el **plan de estiba** un conjunto distinto de restricciones y no dice qué hacer cuando dos se contradicen. Sin esta regla, `RF-NAV-06` no tiene contra qué verificarse.
 
**Regla.** Cuando dos o más restricciones del plan de estiba no puedan satisfacerse simultáneamente, prevalecen en el siguiente orden:
 
1. **Estabilidad y seguridad de la nave** — distribución de peso, altura de estiba y esfuerzos estructurales. No admite excepción: una nave inestable no zarpa.
2. **Segregación de mercancías peligrosas a bordo** conforme al Código IMDG, en los términos de RN-02.
3. **Disponibilidad efectiva de conexión refrigerada a bordo**, considerando las limitaciones declaradas de generación de la nave.
4. **Puerto de destino y orden de descarga**, para evitar remociones en puertos posteriores.
5. **Optimización de la secuencia de carga** desde el patio, para minimizar remociones en origen.
Cuando la propuesta automática ceda una restricción de nivel 3, 4 o 5 para satisfacer una de nivel superior, **deberá declarar explícitamente cuál cedió y por qué**, de modo que el planificador decida sobre información completa.
 
**Origen y fundamento.** El CP, Cap. 4.2 enumera las restricciones sin ordenarlas; el Cap. 17.1 pide llenar ese vacío con una regla propia de la industria. El orden adoptado sitúa primero las dos restricciones **normativas y no negociables** —estabilidad, exigible por la autoridad marítima (CP, Cap. 12, materia 8), y segregación IMDG (materia 6)— y después las operacionales, ordenadas por consecuencia: una falla de conexión refrigerada degrada carga; un error de puerto de destino genera remoción en destino; una secuencia subóptima solo cuesta tiempo en origen.
 
El caso documenta que este conflicto es real: el planificador deja los reefer a proa en una línea determinada «porque su generador de popa está limitado» (CP, Cap. 4.2) — una restricción de conexión venciendo a una de distribución.
 
**Vinculación.** `RF-NAV-06` (propuesta automática, cuyo criterio de aceptación remite a esta regla) · `RF-NAV-07` · `RF-NAV-14` · RN-02 · RN-05 · Decisiones N° 4 y 5.
 
**¿Pendiente de validar?** **Sí, con prioridad alta.** El orden entre los niveles 3, 4 y 5 es criterio propio de Terabyte. El planificador actual tiene un orden implícito que solo se conocerá al ejecutar el frente de captura de conocimiento tácito (`RF-NAV-09` y EP-01), y ese levantamiento puede modificar esta regla. Es, de hecho, uno de los primeros contenidos que ese frente debe recoger.
 
---
 
## RN-10 — Tiempo desconectado en la facturación de conexión refrigerada
 
> **Regla nueva.** Apareció al redactar los ejemplos numéricos de `RF-REF-13`: ninguna regla definía si el tiempo desconectado se descuenta de las horas facturables.
 
**Regla.** Para todo contenedor refrigerado —de exportación que ingresa por camión y sale por nave, o de importación que ingresa por nave y sale por camión— las horas facturables corresponden al **tiempo conectado efectivo en el terminal**. El tiempo desconectado se **descuenta**, con independencia de la causa, incluida una falla atribuible al terminal. El cálculo se deriva de los eventos de conexión y desconexión de la instrumentación, no de una declaración manual.
 
**Ejemplos numéricos.**
 
> **Ejemplo A — conexión continua.** Conectado el 12 de enero a las 06:00; desconectado el 14 de enero a las 18:00; sin interrupciones. Tiempo conectado: **60 horas**. **Horas facturables: 60.**
>
> **Ejemplo B — con desconexión intermedia.** Conectado el 12 de enero a las 06:00. La instrumentación registra desconexión el 13 de enero de 02:15 a 05:45 —3 horas 30 minutos— por falla de tablero. Desconectado el 14 de enero a las 18:00.
> Permanencia en la toma: 60 horas. Tiempo desconectado: 3,5 horas. **Horas facturables: 56,5.**
 
**Origen y fundamento.** El caso declara que hoy la conexión refrigerada se calcula «con las horas que estuvo conectado **según la planilla de la ronda**» (CP, Cap. 4.8), donde una desconexión rara vez consta. Con la instrumentación de `RF-REF-01` a `RF-REF-06`, el terminal **por primera vez sabrá** cuándo un contenedor estuvo desconectado.
 
Es un caso en que mejorar la evidencia crea una obligación que antes no existía. La alternativa —facturar el tiempo de permanencia en la toma— mantendría el ingreso actual pero **facturaría un servicio que la evidencia propia demuestra no prestado**, entregando al cliente, en la misma evidencia que le damos, el argumento para objetar la factura. Eso contradiría el criterio de aceptación N° 14, que la solución busca satisfacer.
 
**Vinculación.** Decisión N° 11 · `RF-REF-13` (registro de horas de conexión) · `RF-REF-05` y `RF-REF-06`, que aportan los eventos de desconexión · `RF-FAC-01` · CP, Cap. 18, criterio 14.
 
**¿Pendiente de validar?** **Sí.** La regla reduce el ingreso por conexión refrigerada respecto de la práctica actual cuando la falla es del terminal, que es el incentivo correcto pero tiene efecto económico. Debe confirmarse con el cliente antes de comprometerla.
 
---
 
## RN-11 — Tolerancia de desviación de temperatura en carga refrigerada

> **Regla nueva.** Apareció al verificar `RF-REF-04`: el requerimiento se titula «detección de desviación de temperatura», pero ninguna regla definía qué constituye una desviación, de modo que su criterio solo era verificable en la rama de desconexión.

**Regla.** Una lectura constituye **desviación** cuando la temperatura registrada se aparta de la **temperatura de consigna** del contenedor más allá de la **banda de tolerancia** declarada para su familia de carga, y esa condición se sostiene durante la **duración mínima** declarada para esa misma familia.

Banda y duración mínima son **parametrizables por familia de carga** y forman parte de la configuración administrable por el CLIENTE conforme a BTT, RT-16.02. La consigna de cada contenedor proviene de la instrucción del embarcador o de la naviera: **no la fija el terminal**.

Mientras el CLIENTE no declare los valores por familia, la solución **deberá** exigir consigna y banda al momento de la conexión y **deberá** registrar como excepción toda conexión sin consigna declarada.

**Por qué esta regla no fija valores numéricos.** El caso declara que un reefer «debe mantener una temperatura de consigna que depende de la carga: la cereza no es el salmón, y el salmón no es la carne» (CP, Cap. 4.5), pero **no entrega bandas por producto**. Las exigencias de trazabilidad de temperatura provienen de los mercados de destino y de los programas de exportación de fruta (CP, Cap. 12). Fijar aquí un número sin fuente sería inventar una cifra del CLIENTE.

**Vinculación.** `RF-REF-04` (detección de desviación) · `RF-REF-01` (muestreo local) · `RF-REF-07` (ausencia de dato) · `RF-REF-11` y `RF-REF-12` (registro continuo como evidencia de cadena de frío) · CP, Cap. 15, **RT-05.29** (alarma en no más de 5 minutos desde el evento físico) · CP, Cap. 18, criterios 11 y 12.

**¿Pendiente de validar?** **Sí, prioridad alta.** Las bandas y duraciones por familia de carga debe entregarlas el CLIENTE junto con sus exportadores. Sin ellas, el criterio de `RF-REF-04` solo es verificable en su rama de desconexión, que es precisamente la limitación que esta regla corrige.

---

## Cobertura de los temas exigidos
 
| Tema exigido (CP, Cap. 17.1 y checklist interno) | Regla |
|---|---|
| Criterio de asignación de posición en patio | RN-01 |
| Reglas de segregación de carga peligrosa | RN-02 |
| Prioridad entre nave y camión ante recursos escasos | RN-03 |
| Cálculo de días de almacenaje | RN-04 |
| Tolerancia de verificación de masa bruta | RN-05 |
| Criterios de liberación de un contenedor | RN-06 |
| Gestión de citas y excepciones | RN-07 |
| Escalamiento y confirmación de alarmas | RN-08 |
| *(adición propia)* Precedencia en el plan de estiba | **RN-09** |
| *(adición propia)* Tiempo desconectado en facturación reefer | **RN-10** |
| *(adición propia)* Tolerancia de desviación de temperatura | **RN-11** |
 
Los ocho temas obligatorios quedan cubiertos. RN-09, RN-10 y RN-11 son adiciones detectadas al cruzar el registro con el catálogo de requerimientos funcionales.
 
---
 
## Historial de versiones
 
| Versión | Contenido |
|---|---|
| 1.0 | Creación con RN-01 a RN-08, cubriendo los ocho temas del Cap. 17.1 y del checklist interno. Autoría de Isidora Cisternas |
| **2.0** | Se incorporan **RN-09** (precedencia en plan de estiba) y **RN-10** (tiempo desconectado en facturación reefer). Se corrige el **fundamento de RN-03**, manteniendo la regla. Se añaden ejemplos numéricos a RN-04 y RN-05. Se actualiza la vinculación de las diez reglas con el catálogo de RF definitivo |
| **2.1** | Corrección contra el Plan Maestro: RN-03 conserva una única excepción operacional; RN-01 usa el siguiente hito comprometido para cubrir exportación e importación; RN-10 explicita que la medición de conexión refrigerada aplica en ambos sentidos del flujo |
| **2.2** | Se incorpora **RN-11** (tolerancia de desviación de temperatura), detectada al verificar que `RF-REF-04` se titulaba «detección de desviación» pero solo era verificable por desconexión. Se corrige el encabezado del documento, que declaraba versión 2.0 cuando el historial ya registraba la 2.1. |
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*
