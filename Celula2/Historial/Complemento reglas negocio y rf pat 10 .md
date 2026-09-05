# Complemento al Registro de Reglas de Negocio y formalización de `RF-PAT-10`
 
> **Célula 2 · Solución, alcance y requisitos** · Caso 06 Portuaria · Terabyte
> **Complementa:** `registro_reglas_de_negocio.md` (Isidora Cisternas). **No lo reemplaza ni lo modifica.**
> **Origen:** cruce del registro de reglas con el catálogo de 128 RF y con las correcciones de la Fase 4.
> **Estado:** propuestas de Célula 2, pendientes de revisión por Isidora.
> **Convenciones:** BA = Bases Administrativas (FEP01.26) · BTT = Bases Técnicas Transversales (FEP02.26) · CP = Caso 06 Portuaria (FEP03.06.26).
 
---
 
## 1. Regla nueva — RN-09, precedencia en el plan de estiba
 
**Por qué falta.** El Cap. 17.1 enumera ocho temas y el registro los cubre los ocho. RN-01 resuelve la precedencia **en patio**. Pero el CP, Cap. 4.2 enumera para el **plan de estiba** un conjunto distinto de restricciones —peso, altura, puerto de destino, segregación de carga peligrosa, estabilidad de la nave y disponibilidad de conexión refrigerada a bordo— y no dice qué hacer cuando dos de ellas se contradicen. Ese conflicto es real y documentado: el propio caso relata que el planificador deja los reefer a proa en una línea determinada «porque su generador de popa está limitado», lo que es precisamente una restricción de conexión venciendo a una de distribución de peso.
 
Sin esta regla, `RF-NAV-06` no tiene contra qué verificarse.
 
---
 
### RN-09 — Precedencia entre restricciones del plan de estiba
 
**Regla.** Cuando dos o más restricciones del plan de estiba no puedan satisfacerse simultáneamente, prevalecen en el siguiente orden:
 
1. **Estabilidad y seguridad de la nave** — distribución de peso, altura de estiba y esfuerzos estructurales. No admite excepción: una nave inestable no zarpa.
2. **Segregación de mercancías peligrosas a bordo** conforme al Código IMDG, en los términos de RN-02.
3. **Disponibilidad efectiva de conexión refrigerada a bordo**, considerando las limitaciones declaradas de generación de la nave.
4. **Puerto de destino y orden de descarga**, para evitar remociones en puertos posteriores.
5. **Optimización de la secuencia de carga** desde el patio, para minimizar remociones en origen.
Cuando la propuesta automática ceda una restricción de nivel 3, 4 o 5 para satisfacer una de nivel superior, **deberá declarar explícitamente cuál cedió y por qué**, de modo que el planificador decida sobre información completa.
 
**Origen y fundamento.** El CP, Cap. 4.2 enumera las restricciones sin ordenarlas; el Cap. 17.1 pide llenar ese vacío con una regla propia de la industria. El orden adoptado sitúa primero las dos restricciones que son normativas y no negociables —estabilidad, exigible por la autoridad marítima (CP, Cap. 12, materia 8), y segregación IMDG (CP, Cap. 12, materia 6)— y después las operacionales. Los niveles 3 a 5 se ordenan por consecuencia: una falla de conexión refrigerada degrada carga, un error de puerto de destino genera remoción en destino, y una secuencia subóptima solo cuesta tiempo en origen.
 
**Vinculación con el catálogo:** `RF-NAV-06`, `RF-NAV-07`, RN-02, Decisión N° 4, Decisión N° 5.
 
**¿Pendiente de validar con el cliente?** **Sí, con prioridad alta.** El orden entre los niveles 3, 4 y 5 es criterio propio de Terabyte. El planificador actual tiene un orden implícito que solo se conocerá al ejecutar el frente de captura de conocimiento tácito (`RF-NAV-09`), y ese levantamiento puede modificar esta regla. Es, de hecho, uno de los primeros contenidos que ese frente debe recoger.
 
---
 
## 2. Corrección propuesta al fundamento de RN-03
 
> **La regla probablemente es correcta. El fundamento que la sostiene, no.** Se propone corregir la justificación sin alterar la conclusión.
 
**Lo que dice hoy el fundamento de RN-03:**
 
> «…los indicadores comprometidos contractualmente con el concedente giran en torno a la estadía de la nave —con consecuencia económica directa—, mientras que **el gate tiene un umbral de servicio interno sin penalidad concesional asociada**.»
 
**Por qué no se sostiene.** La estadía del camión **sí es un indicador comprometido con el concedente**, y es el que está en peor estado de todo el caso:
 
| Evidencia | Fuente |
|---|---|
| «El contrato de concesión establece indicadores de desempeño reportables al concedente. La solución debe producir esos indicadores de forma trazable y auditable, no reconstruirlos» | CP, Cap. 10, restricción no negociable N° 14 |
| La estadía del camión se mide «desde la barrera de entrada hasta la de salida» y es uno de los indicadores del contrato de concesión | CP, Anexo C |
| «Semestres consecutivos sobre el umbral de estadía del camión: **3**», referencia: cero | CP, 7.1 |
| «Cada semestre adicional agrava la situación contractual» | CP, 13.2 |
| Criterio de aceptación N° 1: «El tiempo de estadía del camión cumple el umbral comprometido con el concedente, de forma sostenida y auditable» | CP, Cap. 18 |
 
El gate no tiene un umbral interno: tiene el indicador con **incumplimiento acumulado y consecuencia contractual en curso**, que es más de lo que puede decirse de la ventana de atraque, cuyo 71 % de cumplimiento el caso no vincula a una penalidad concesional declarada.
 
**Fundamento propuesto en reemplazo.** La prioridad de la nave no se justifica por una asimetría contractual que no existe, sino por una **asimetría de irreversibilidad y de costo por unidad de tiempo**:
 
1. **La nave consume un recurso que no se recupera.** «Una nave amarrada consume tiempo de muelle desde el momento en que amarra» (CP, Cap. 10, restricción no negociable N° 2). El muelle tiene tres sitios y seis grúas; el tiempo de sitio perdido no se repone.
2. **El costo por hora es conocido y asimétrico.** «Cada hora de espera de una nave portacontenedores tiene un costo que la naviera conoce con precisión y que el terminal no calcula» (CP, Cap. 4.1). Una hora de nave detenida equivale, a 24,8 movimientos por hora, a unos 25 movimientos perdidos que desplazan toda la programación siguiente.
3. **El camión admite reprogramación; la nave no.** Un camión puede esperar, reagendar o volver; una ventana de atraque desplazada arrastra a la nave siguiente.
**Salvaguarda que se refuerza.** Precisamente porque la estadía del camión **sí** tiene consecuencia concesional, la excepción que RN-03 ya contempla —no desplazar a un camión que ya inició su proceso— deja de ser una cortesía y pasa a ser la protección de un indicador en incumplimiento. Se propone hacerla explícita: la prioridad de nave **no** puede aplicarse sobre un camión cuyo proceso de gate ya se inició, ni de forma que el indicador de estadía del turno supere el umbral comprometido.
 
**Consecuencia práctica:** ninguna sobre la regla. La conclusión operativa se mantiene y queda mejor defendida.
 
---
 
## 3. Formalización de `RF-PAT-10` — Supuesto complementario a la Decisión N° 3
 
> **Clase de profundidad: párrafo ampliado.** No es una decisión nueva sino una **extensión declarada** de la Decisión N° 3, cuyo campo de impacto ya reconoce el problema. No hay contradicción normativa ni condiciona el alcance completo.
 
### 3.1 El hueco que se cierra
 
La Decisión N° 3 adoptó «el algoritmo asigna, el operador ejecuta» y en su propio campo de impacto admite:
 
> «Si el algoritmo asigna mal por desconocer una restricción física real (equipo con falla intermitente, bloque que se inunda — ver Decisión N° 5), **el operador ejecutará una instrucción errónea sin oportunidad de corregirla antes del movimiento**.»
 
La Decisión N° 5 da al **planificador** una vía para declarar condiciones dinámicas. Al **operador**, que es quien ve la condición física en el momento, ninguna decisión le da vía alguna.
 
### 3.2 La decisión
 
**Terabyte incorpora una vía de excepción del operador, condicionada a interlock de equipo detenido, verificada contra la telemetría del propio equipo.**
 
Tres capas, que no son alternativas sino un solo mecanismo:
 
| Capa | Contenido |
|---|---|
| **Estructura** | Se registra como extensión declarada de la Decisión N° 3, con los seis campos del registro de supuestos. Sin esto, `RF-PAT-10` sería el único requerimiento del catálogo sin decisión que lo funde — la conducta que el CP, Cap. 19 califica de «resuelta por omisión» |
| **Mecanismo** | **Interlock de equipo detenido.** La función de marcar una instrucción como no ejecutable **solo está disponible cuando la telemetría del equipo acredita detención**, y se deshabilita automáticamente al reanudarse el movimiento. El cumplimiento de la restricción N° 1 deja de ser una promesa de diseño y pasa a ser una propiedad verificable del sistema, comprobable contra el mismo flujo de telemetría de `RF-PAT-05` |
| **Validación** | Revisión ergonómica con prevención de riesgos y con el sindicato **antes del diseño detallado**, con acta de conformidad, y prueba en equipo real durante la marcha blanca |
 
### 3.3 Fundamento
 
| Fuente | Qué sostiene |
|---|---|
| CP, Cap. 10, restricción no negociable N° 1: «Toda propuesta que obligue a un operador a atender un dispositivo **mientras hay equipos en movimiento** será rechazada» | La prohibición está acotada al movimiento. Una acción con el equipo detenido no está alcanzada por el texto de la restricción |
| CP, Cap. 15, RT-13.08 | Las interfaces de terreno deben acreditar que no elevan el riesgo. El interlock es el mecanismo de acreditación |
| Decisión N° 3, campo de impacto | Reconoce el hueco expresamente |
| Decisión N° 5 | Establece el precedente: las condiciones físicas reales que el algoritmo desconoce deben poder declararse cuando aparecen, no modelarse por adelantado |
| Dahiya et al. (2026), *Applied Sciences* | Documenta que los errores de colocación provienen de causas —orientación del contenedor en el spreader— que el posicionamiento automático no corrige. Respalda la necesidad de una vía humana de corrección |
 
### 3.4 Alternativas descartadas
 
| Alternativa | Por qué se descarta |
|---|---|
| **No dar vía de excepción** (situación actual del catálogo) | Deja vigente el defecto que la Decisión N° 3 reconoce. El operador ejecuta una instrucción que sabe errónea, o la incumple sin registro — y lo segundo es peor, porque el sistema queda creyendo algo falso |
| **Vía de excepción sin interlock**, disponible en todo momento | Expone a la propuesta al rechazo por la restricción N° 1, cuya sanción es explícita: «cualquiera sea su mérito en el resto» |
| **Que el operador avise por radio al supervisor** | Es el procedimiento actual, que el CP, Cap. 5 declara que debe dejar de ser sistema de registro. Además pierde el motivo, que es el dato que alimenta el catálogo de condiciones dinámicas |
| **Confirmación activa de toda instrucción** | Es la opción que la Decisión N° 3 ya descartó por la restricción N° 1. La excepción es un acto ocasional con el equipo detenido; la confirmación sería un acto permanente durante la faena |
 
### 3.5 Impacto si resulta equivocada
 
Si la revisión ergonómica determina que incluso con el equipo detenido la interacción eleva la exposición al riesgo, la vía de excepción se retira y la Decisión N° 3 queda con su defecto original. En ese escenario debe compensarse por otra vía: ampliar el catálogo de condiciones dinámicas de la Decisión N° 5 para que el **supervisor de patio** —que no opera equipo— pueda declarar la condición en nombre del operador, con la pérdida de inmediatez que ello implica.
 
Riesgo secundario: si el uso de la excepción resulta frecuente, indica que el algoritmo de asignación desconoce restricciones estructurales, no puntuales. La tasa de uso debe monitorearse como **indicador de calidad del algoritmo**, no solo como registro operacional.
 
### 3.6 Instancia y momento de validación
 
- **Acta de conformidad de prevención de riesgos y del sindicato**, antes del diseño detallado de la interfaz de terreno.
- **Prueba en equipo real** durante la marcha blanca de la Etapa 1.
- **Ratificación de la célula** de este supuesto, previa a la entrega del Informe 1.
### 3.7 Responsable
 
Terabyte. Coordinación con Célula 3 para la verificación de que la telemetría del equipo permite acreditar el estado de detención con la fiabilidad que el interlock exige.
 
### 3.8 Efecto sobre el requerimiento
 
`RF-PAT-10` vuelve a **«deberá»** y **entra al conteo firme**, con dos cambios sobre su redacción actual:
 
- La condición «con el equipo detenido» pasa de precondición declarativa a **interlock verificable**: la función no está disponible si la telemetría no acredita detención.
- El criterio de aceptación incorpora la prueba del interlock: *«se intenta marcar una instrucción como no ejecutable con el equipo en movimiento y la función no está disponible; se repite con el equipo detenido y la marca se registra con su motivo; se acredita que el algoritmo reasigna y que el motivo queda disponible para el planificador.»*
**Conteo:** 128 firmes.
 
---
 
## 4. Enganches del catálogo con el registro de reglas de negocio
 
El registro de reglas resuelve cuatro umbrales que el catálogo invocaba sin cifra. Se incorporan como origen citado.
 
| Requerimiento | Qué le aporta la regla | Cambio |
|---|---|---|
| `RF-NAV-06` | **RN-09** fija el orden de precedencia entre restricciones de estiba | El criterio de aceptación deja de ser circular: «el plan cumple las seis restricciones en 20 recaladas históricas; cuando dos entren en conflicto, prevalece el orden de **RN-09** y la propuesta explicita cuál cedió» |
| `RF-PAT-06` | **RN-01** fija el orden de asignación en patio | Se añade RN-01 al campo Origen. La asignación deja de ser «por regla explicable» sin decir cuál |
| `RF-GAT-09` | **RN-05** fija la tolerancia de masa bruta en **5 % del peso declarado** | El requerimiento decía «supere la tolerancia» sin número. Ahora cita RN-05, con la salvedad de que la propia regla marca el 5 % como pendiente de confirmar con la autoridad marítima chilena |
| `RF-GAT-02` | **RN-07** define «cita cumplida»: ventana de **30 minutos**, 15 antes y 15 después | Evita que dos documentos definan el mismo término de forma distinta — el «conflicto entre términos» que el material de redacción advierte |
| `RF-FAC-03` | **RN-04** fija el método: días corridos, desde el día siguiente, 3 días libres, corte 23:59 | Habilita los dos ejemplos numéricos exigidos. Ver sección 5 |
| `RF-REF-13` | Ninguna regla cubre si el tiempo desconectado se descuenta de las horas facturables | **Queda pendiente.** Ver sección 5 |
| `RF-PAT-07` | **RN-02** remite a la tabla de segregación IMDG | Se añade RN-02 al Origen; la batería de prueba se versiona junto al registro de reglas |
| `RF-REF-08` · `RF-REF-09` · `RF-REF-10` | **RN-08** consolida la lógica de escalamiento como regla transversal | Se añade RN-08 al Origen de los tres |
 
---
 
## 5. Los dos ejemplos numéricos exigidos
 
El material de redacción del curso exige que todo requisito que especifique un cálculo lleve **dos ejemplos numéricos resueltos**. Con RN-04 y RN-05 disponibles, dos de los tres se pueden redactar.
 
### 5.1 `RF-FAC-03` — Días de almacenaje
 
Método de RN-04: días corridos, el día de ingreso no cuenta, 3 días libres, corte a las 23:59.
 
> **Ejemplo A — dentro del mismo mes.** Contenedor descargado el 4 de marzo a las 08:30. Retirado el 11 de marzo a las 16:00.
> Conteo desde el 5 de marzo. Días transcurridos hasta el 11: **7**. Días libres: 3. **Días facturables: 4** (8, 9, 10 y 11 de marzo).
>
> **Ejemplo B — cruzando el cambio de mes.** Contenedor descargado el 27 de marzo a las 22:15. Retirado el 3 de abril a las 09:00.
> Conteo desde el 28 de marzo. Días transcurridos hasta el 3 de abril: **7** (28, 29, 30, 31 de marzo y 1, 2, 3 de abril). Días libres: 3. **Días facturables: 4** (31 de marzo y 1, 2, 3 de abril).
>
> Ambos ejemplos ilustran que la hora de ingreso y de retiro no altera el conteo, y que el cambio de mes no reinicia el cómputo.
 
### 5.2 `RF-GAT-09` — Discrepancia de masa bruta
 
Método de RN-05: discrepancia cuando la diferencia supera el 5 % del peso declarado.
 
> **Ejemplo A — dentro de tolerancia.** Peso declarado 24.000 kg. Peso verificado 24.900 kg. Diferencia: 900 kg, equivalente al **3,75 %** del declarado. **No hay discrepancia**; la operación continúa.
>
> **Ejemplo B — sobre tolerancia.** Peso declarado 24.000 kg. Peso verificado 25.400 kg. Diferencia: 1.400 kg, equivalente al **5,83 %** del declarado. **Hay discrepancia**: la operación se detiene, se notifica al embarcador y el plan de estiba afectado se marca para replanificación conforme a `RF-NAV-14`.
>
> El porcentaje se calcula siempre sobre el peso **declarado**, no sobre el verificado.
 
### 5.3 `RF-REF-13` — Horas de conexión refrigerada: pendiente
 
Ninguna regla del registro define **si el tiempo en que el contenedor estuvo desconectado se descuenta** de las horas facturables. La pregunta no es menor: con la instrumentación de `RF-REF-01` a `RF-REF-05`, el terminal por primera vez **sabrá** cuándo un contenedor estuvo desconectado — incluso por falla propia.
 
Es un caso donde mejorar la evidencia crea una obligación que antes no existía: hoy se factura contra la planilla de la ronda y la desconexión rara vez consta; mañana constará.
 
**Se propone como RN-10, pendiente de decisión de la célula**, con dos lecturas posibles:
 
| Lectura | Consecuencia |
|---|---|
| Se factura el tiempo **conectado efectivo** | Coherente con la Decisión N° 11 (facturar el hecho que ocurre, con evidencia). Reduce ingreso cuando la falla es del terminal, que es el incentivo correcto |
| Se factura el tiempo **de permanencia en la toma asignada** | Mantiene el ingreso actual, pero factura un servicio que la evidencia propia demuestra no prestado — y expone a la objeción que el criterio de aceptación 14 busca eliminar |
 
**Recomendación de Célula 2: la primera lectura.** La segunda entrega al cliente, en la propia evidencia que le damos, el argumento para objetar la factura.
 
---
 
## 6. Resumen de lo que este documento propone
 
| # | Propuesta | Requiere |
|---:|---|---|
| 1 | **RN-09** — precedencia en el plan de estiba | Revisión de Isidora |
| 2 | **Corrección del fundamento de RN-03**, manteniendo la regla | Revisión de Isidora |
| 3 | **RN-10** — tratamiento del tiempo desconectado en la facturación reefer | Decisión de la célula |
| 4 | **Supuesto complementario a la Decisión N° 3** que formaliza `RF-PAT-10` con interlock | Ratificación de la célula |
| 5 | Enganche de ocho requerimientos con las reglas RN-01, RN-02, RN-04, RN-05, RN-07, RN-08 y RN-09 | — |
| 6 | Dos ejemplos numéricos para `RF-FAC-03` y `RF-GAT-09` | — |
 
**Conteo del catálogo: 128 firmes.** `RF-PAT-10` vuelve a obligatorio al quedar fundado.
 
---
 
*Documento de trabajo interno de la Célula 2 · Terabyte · Caso 06 Portuaria. La aprobación final de todo contenido corresponde al equipo humano.*